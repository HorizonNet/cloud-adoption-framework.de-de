---
title: Zuweisen eines neuen Hosts für eine lokale Linux-App zu Azure-VMs
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dieser Artikel enthält Informationen zum Zuweisen eines neuen Hosts für eine lokale Linux-App durch Migration zu Azure-VMs.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 078749474b13074d9196a80c10768da468e423bc
ms.sourcegitcommit: b166fe1621fe7e886616009e56b76873b8cce83c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2020
ms.locfileid: "76520207"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms"></a>Zuweisen eines neuen Hosts für eine lokale Linux-App zu Azure-VMs

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso mit Azure IaaS-VMs einer zweistufigen Linux-basierten Apache MySQL PHP (LAMP)-App einen neuen Host zuweist.

osTicket, die in diesem Beispiel verwendete Service Desk-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/osTicket/osTicket) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und Infrastrukturen unter Druck.
- **Risikobegrenzung.** Die Service Desk-App ist wichtig für das Geschäft von Contoso. Contoso möchte sie ohne jedes Risiko nach Azure verlagern.
- **Erweitern.** Contoso möchte die App derzeit nicht ändern. Es soll lediglich sichergestellt werden, dass die App stabil ist.

## <a name="migration-goals"></a>Migrationsziele

Für die Bestimmung der besten Migrationsmethode hat das Contoso-Cloudteam Ziele für diese Migration festgelegt:

- Nach der Migration sollte die App in Azure die gleichen Leistungsmerkmale aufweisen wie die lokale VMware-Umgebung heute. Die App bleibt lokal und in der Cloud gleichermaßen wichtig.
- Contoso möchte nicht in diese App investieren. Die Investition ist wichtig für das Geschäft, in ihrer derzeitigen Form soll die App jedoch lediglich sicher in die Cloud verschoben werden.
- Contoso möchte das Vorgangsmodell für diese App nicht ändern. Das Unternehmen möchte genau wie jetzt in der Cloud mit der App interagieren können.
- Contoso möchte die App-Funktionalität nicht ändern. Nur der Speicherort der App ändert sich.
- Nach Abschluss einer Reihe von Windows-App-Migrationen möchte Contoso mehr über die Verwendung einer Linux-basierten Infrastruktur in Azure erfahren.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-app"></a>Aktuelle App

- Die App „OSTicket“ ist auf zwei virtuelle Computer aufgeteilt (**OSTICKETWEB** und **OSTICKETMYSQL**).
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (**contoso-datacenter**) mit einem lokalen Domänencontroller (**contosodc1**).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Da es sich bei der App um eine Produktionsworkload handelt, befinden sich die virtuellen Computer in Azure in der Produktionsressourcengruppe **ContosoRG**.
- Die VMs werden zur primären Region (USA, Osten 2) migriert und im Produktionsnetzwerk (VNET-PROD-EUS2) platziert:
  - Die Web-VM befindet sich im Front-End-Subnetz (PROD-FE-EUS2).
  - Die Datenbank-VM befindet sich im Subnetz der Datenbank (PROD-DB-EUS2).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Szenarioarchitektur](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | Beide virtuellen Computer der App werden ohne Änderungen nach Azure verlagert, was die Migration vereinfacht.<br/><br/> Da Contoso beide virtuellen Computer der App per „Lift & Shift“-Ansatz migriert, sind für die App-Datenbank keine besonderen Konfigurations- oder Migrationstools erforderlich.<br/><br/> Contoso behält die vollständige Kontrolle über die virtuellen Computer der App in Azure. <br/><br/> Die virtuellen Computer der App führen Ubuntu 16.04-TLS aus. Dabei handelt es sich um eine unterstützte Linux-Distribution. [Weitere Informationen](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros)
**Nachteile** | Die Web- und Datenschicht der App bleiben ein Single Point of Failover. <br/><br/> Contoso muss die App weiterhin als virtuelle Azure-Computer unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service oder Azure Database for MySQL umzustellen.<br/><br/> Contoso ist sich bewusst, dass bei der Vereinfachung durch eine Migration von virtuellen Computern per „Lift & Shift“ die von [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) bereitgestellten Funktionen (integrierte Hochverfügbarkeit, vorhersagbare Leistung, einfache Skalierung, automatische Sicherungen und integrierte Sicherheit) nicht in vollem Umfang genutzt werden können.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migrationsprozess

Contoso geht bei der Migration wie folgt vor:

- Im ersten Schritt bereitet Contoso Azure-Komponenten für die Azure Migrate-Servermigration vor, richtet diese ein und bereitet die lokale VMware-Infrastruktur vor.
- Sie verfügen bereits über die [Azure-Infrastruktur](./contoso-migration-infrastructure.md), sodass Contoso nur noch die Konfiguration der Replikation der virtuellen Computer über das Tool für die Azure Migrate-Servermigration hinzufügen muss.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der virtuellen Computer beginnen.
- Wenn die Replikation aktiviert wurde und funktioniert, migriert Contoso den virtuellen Computer via Failover zu Azure.

![Migrationsprozess](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Azure Migrate-Servermigration](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm) | Der Dienst organisiert und verwaltet die Migration Ihrer lokalen Anwendungen und Workloads sowie von AWS/GCP-VM-Instanzen. | Während der Replikation in Azure fallen Gebühren für Azure Storage an. Es werden Azure-VMs erstellt, und Gebühren fallen an, sobald ein Failover erfolgt. [Weitere Informationen](https://azure.microsoft.com/pricing/details/azure-migrate) zu Gebühren und Preisen.

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes.

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Contoso hat in einem der ersten Artikel dieser Reihe Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.<br/><br/> Wenn Sie detailliertere Berechtigungen benötigen, lesen Sie [diesen Artikel](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-Infrastruktur** |  [Weitere Informationen](./contoso-migration-infrastructure.md) zur Vorgehensweise von Contoso beim Einrichten einer Azure-Infrastruktur.<br/><br/> Erfahren Sie mehr über bestimmte [Voraussetzungen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) für die Azure Migrate-Servermigration.
**Lokale Server** | Der lokale vCenter-Server muss mit Version 5.5, 6.0 oder 6.5 ausgeführt werden.<br/><br/> Einen ESXi-Host mit Version 5.5, 6.0 oder 6.5.<br/><br/> Mindestens eine VMware-VM auf dem ESXi-Host.
**Lokale VMs** | [Überprüfen Sie Linux-Computer](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten von Azure für die Azure Migrate-Servermigration.** Sie fügen das Tool für die Servermigration ihrem Azure Migrate-Projekt hinzu.
> - **Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate-Servermigration.** Sie bereiten Konten für die VM-Ermittlung sowie das Herstellen einer Verbindung mit Azure-VMs nach dem Failover vor.
> - **Schritt 3: Replizieren von VMs.** Das Unternehmen richtet die Replikation ein und startet das Replizieren von VMs in Azure-Storage.
> - **Schritt 4: Migration der virtuellen Computer mit der Azure Migrate-Servermigration.** Es wird ein Testfailover durchgeführt, um sicherzustellen, dass alles funktioniert, und anschließend wird ein vollständiges Failover für die Migration der VMs zu Azure aus.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 1: Vorbereiten von Azure für das Tool für die Azure Migrate-Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein VNET, in dem sich Azure-VMs befinden, wenn diese während eines Failovers erstellt werden.
- Das bereitgestellte Tool für die Azure Migrate-Servermigration.

Das Unternehmen geht bei der Einrichtung dieser Komponenten wie folgt vor:

1. **Einrichten eines Netzwerks:** Im Rahmen der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) hat Contoso bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann.

    - Bei der SmartHotel360-App handelt es sich um eine Produktions-App. Die VMs werden zum Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten 2“ migriert.
    - Beide VMs werden in der Ressourcengruppe ContosoRG bereitgestellt, die für Produktionsressourcen verwendet wird.
    - Die App-Front-End-VM (WEBVM) wird zum Front-End-Subnetz (PROD-FE-EUS2) im Produktionsnetzwerk migriert.
    - Die App-Datenbank-VM (SQLVM) wird zum Datenbanksubnetz (PROD-DB-EUS2) im Produktionsnetzwerk migriert.

2. **Bereitstellen des Azure Migrate-Servermigrationstools:** Nach dem Einrichten des Netzwerks und des Speicherkontos kann Contoso nun einen Recovery Services-Tresor (ContosoMigrationVault) erstellen und diesen in der Ressourcengruppe ContosoFailoverRG in der primären Region „USA, Osten 2“ platzieren.

    ![Tool für die Azure Migrate-Servermigration](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**Benötigen Sie weitere Hilfe?**

[Hier finden Sie Informationen](https://docs.microsoft.com/azure/migrate) zur Einrichtung des Tools für die Azure Migrate-Servermigration.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Vorbereiten der Verbindungsherstellung mit Azure-VMs nach dem Failover

Nach dem Failover in Azure möchte Contoso eine Verbindung mit den replizierten VMs in Azure herstellen können. Dazu müssen die Contoso-Administratoren einige Schritte durchführen:

- Für den Zugriff auf virtuelle Azure-Computer über das Internet müssen sie vor der Migration auf dem lokalen Linux-Computer SSH aktivieren. Bei Ubuntu kann dieser Vorgang mithilfe des folgenden Befehls durchgeführt werden: **Sudo apt-get ssh install -y**.
- Nach der Durchführung der Migration (Failover) können sie die **Startdiagnose** überprüfen, um einen Screenshot des virtuellen Computers anzuzeigen.
- Falls dies nicht funktioniert, müssen sie überprüfen, ob der virtuelle Computer ausgeführt wird, und sollten folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) lesen.

**Benötigen Sie weitere Hilfe?**

- [Informationen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) zum Vorbereiten von virtuellen Computern für die Migration

## <a name="step-3-replicate-the-on-premises-vms"></a>Schritt 3: Replizieren der lokalen VMs

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können Sie mit der Replikation von VMware-VMs in Azure beginnen.

1. Klicken Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** auf **Replizieren**.

    ![Replizieren von VMs](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere-Hypervisor** aus.

3. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance aus, die Sie eingerichtet haben, und dann **OK**.

    ![Quelleinstellungen](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten.
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie hierzu unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung ausgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Auswählen der Bewertung](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und aktivieren Sie alle VMs, die Sie migrieren möchten. Klicken Sie anschließend auf **Next: Zieleinstellungen**.

6. Wählen Sie unter **Zieleinstellungen** das Abonnement und die Zielregion für die Migration aus, und geben Sie die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden. Wählen Sie unter **Virtuelles Netzwerk** das Azure-VNET/-Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

7. Wählen Sie unter **Azure-Hybridvorteil** Folgendes aus:

    - die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Klicken Sie dann auf **Weiter**.
    - Wählen Sie **Ja** aus, wenn Sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Klicken Sie dann auf **Weiter**.

8. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste für die VM-Größe die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der höchsten Übereinstimmung im Azure-Abonnement aus. Alternativ können Sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

9. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen, und wählen Sie in Azure den Datenträgertyp aus (SSD Standard/HDD Standard oder Managed Disks Premium). Klicken Sie dann auf **Weiter**.
    - Sie können Datenträger von der Replikation ausschließen.
    - Wenn Sie Datenträger ausschließen, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

10. Überprüfen Sie unter **Replikation prüfen und starten** die Einstellungen, und klicken Sie auf **Replizieren**, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-4-migrate-the-vms"></a>Schritt 4: Migrieren der VMs

Contoso-Administratoren führen ein schnelles Testfailover und dann ein vollständiges Failover aus, um die virtuellen Computer zu migrieren.

### <a name="run-a-test-failover"></a>Ausführen eines Testfailovers

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** auf **Migrierte Server testen**.

     ![Testen der migrierten Server](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Klicken Sie mit der rechten Maustaste auf die zu testende VM, und klicken Sie anschließend auf **Testmigration**.

    ![Testmigration](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. Wählen Sie unter **Testmigration** das Azure VNET aus, in dem sich die Azure-VM nach der Migration befindet. Es empfiehlt sich, ein nicht für die Produktion bestimmtes VNET zu verwenden.
4. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
5. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
6. Klicken Sie nach Abschluss des Tests mit der rechten Maustaste unter **Aktuell replizierte Computer** auf die Azure-VM, und klicken Sie anschließend auf **Testmigration bereinigen**.

    ![Bereinigen der Migration](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrieren der VMs

Contoso-Administratoren führen jetzt ein vollständiges Failover aus, um die Migration abzuschließen.

1. Klicken Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** auf **Server werden repliziert**.

    ![Replizieren der Server](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. Klicken Sie unter **Aktuell replizierte Computer** mit der rechten Maustaste auf die VM und dann auf **Migrieren**.
3. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. So wird sichergestellt, dass keine Daten verloren gehen.
    - Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
4. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
5. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

### <a name="connect-the-vm-to-the-database"></a>Verbinden der VM mit der Datenbank

Der letzte Schritt im Migrationsprozess besteht in der Aktualisierung der Verbindungszeichenfolge der Anwendung, um auf die App-Datenbank zu verweisen, die auf dem virtuellen Computer **OSTICKETMYSQL** ausgeführt wird.

1. Das Unternehmen stellt über Putty oder einen anderen SSH-Client eine SSH-Verbindung mit der VM **OSTICKETWEB** her. Die VM ist privat, daher stellt Contoso eine Verbindung über die private IP-Adresse her.

    ![Herstellen einer Verbindung mit der Datenbank](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Herstellen einer Verbindung mit der Datenbank](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. Das Unternehmen muss sicherstellen, dass die VM **OSTICKETWEB** mit der VM **OSTICKETMYSQL** kommunizieren kann. Die Konfiguration ist mit der lokalen IP-Adresse 172.16.0.43 derzeit hartcodiert.

    **Vor dem Update:**

    ![Update-IP](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Nach dem Update:**

    ![Update-IP](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. Das Unternehmen startet den Dienst mit dem Befehl **systemctl restart apache2** neu.

    ![Neu starten](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Schließlich aktualisiert Contoso die DNS-Datensätze für **OSTICKETWEB** und **OSTICKETMYSQL** auf einem der Contoso-Domänencontroller.

    ![DNS-Aktualisierung](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![DNS-Aktualisierung](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Benötigen Sie weitere Hilfe?**

- [Informationen](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) zum Ausführen eines Testfailovers.
- [Informationen](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) zur Migration von virtuellen Computern zu Azure.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration werden die Schichten der App osTicket jetzt auf Azure-VMs ausgeführt.

Contoso muss nun folgende Bereinigungsmaßnahmen vornehmen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation, damit der neue Speicherort und die IP-Adressen für OSTICKETWEB und OSTICKETMYSQL angezeigt werden.
- Überprüfen sämtlicher Ressourcen, die mit den VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.
- Contoso hat mithilfe des Azure Migrate-Diensts durch die Zuordnung von Abhängigkeiten die VMs für die Migration bewertet. Administratoren müssen Microsoft Monitoring Agent und den Microsoft Dependency-Agent, die für diesen Zweck installiert wurden, vom virtuellen Computer entfernen.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die App jetzt ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die VMs OSTICKETWEB und OSTICKETMYSQL, um mögliche Sicherheitsprobleme zu ermitteln.

- Das Team überprüft die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer zur Steuerung des Zugriffs. Mithilfe von NSGs wird sichergestellt, dass nur für die App zulässiger Datenverkehr übergeben werden kann.
- Das Team zieht darüber hinaus in Betracht, die Daten über Datenträgerverschlüsselung und Azure KeyVault auf den Datenträgern des virtuellen Computers zu sichern.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>BCDR

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- **Schützen von Daten.** Contoso sichert die Daten auf den VMs mithilfe des Azure Backup-Diensts. [Weitere Informationen](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- **Sicherstellen eines unterbrechungsfreien Betriebs der Apps.** Contoso repliziert die App-VMs in Azure mithilfe von Site Recovery in einer sekundären Region. [Weitere Informationen](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nach der Bereitstellung von Ressourcen, weist der Contoso Azure Tags zu, die während der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md#set-up-tagging) definiert wurden.
- Contoso hat mit den Ubuntu-Servern keine Lizenzierungsprobleme.
- Contoso aktiviert Azure Cost Management. Es ist durch Cloudyn lizenziert, ein Tochterunternehmen von Microsoft. Dabei handelt es sich um eine Kostenverwaltungslösung mit mehreren Clouds, die Ihnen das Verwenden und Verwalten von Azure und anderen Cloudressourcen erleichtert. [Erfahren Sie mehr](https://docs.microsoft.com/azure/cost-management/overview) über die Azure Cost Management.
