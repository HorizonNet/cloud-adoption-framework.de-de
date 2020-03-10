---
title: Rehosten einer App auf Azure-VMs mit Azure Site Recovery
description: Hier erfahren Sie, wie Contoso einer lokalen App mit einer „Lift & Shift“-Migration von lokalen Computern zu Azure mithilfe des Azure Site Recovery-Diensts einen neuen Host zuweist.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 8b704c88b2e6a161c49082301df6e6a3d7d77154
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222891"
---
# <a name="rehost-an-on-premises-app-on-azure-vms"></a>Rehosten einer lokalen App auf Azure-VMs

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso einer zweistufigen Windows.NET-Front-End-App, die auf VMware-VMs ausgeführt wird, durch Migration der App-VMs auf Azure-VMs einen neuen Host zuweist.

Die in diesem Beispiel verwendet SmartHotel360-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und Infrastrukturen unter Druck.
- **Risikobegrenzung.** Die SmartHotel360-App ist wichtig für das Geschäft von Contoso. Das Unternehmen möchte die App ohne jedes Risiko in Azure verschieben.
- **Erweitern.** Contoso möchte die App nicht ändern, möchte aber sicherstellen, dass sie stabil ist.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Diese Ziele werden verwendet, um die beste Migrationsmethode zu bestimmen:

- Nach der Migration sollte die App in Azure das gleiche Leistungsvermögen aufweisen wie derzeit in der VMware-Umgebung. Die App bleibt lokal und in der Cloud gleichermaßen wichtig.
- Contoso möchte nicht in diese App investieren. Die Investition ist wichtig für das Geschäft, in ihrer derzeitigen Form soll die App jedoch lediglich sicher in die Cloud verschoben werden.
- Contoso möchte das Vorgangsmodell für diese App nicht ändern. Contoso möchte in der Cloud wie derzeit damit interagieren können.
- Contos möchte die App-Funktionalität nicht im Geringsten ändern. Nur der Speicherort der App ändert sich.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-app"></a>Aktuelle App

- Die App ist auf zwei VMs aufgeteilt (**WEBVM** und **SQLVM**).
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (contoso-datacenter) mit einem lokalen Domänencontroller (**contosodc1**).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Da es sich bei der App um eine Produktionsworkload handelt, befinden sich die virtuellen Computer der App in Azure in der Ressourcengruppe „ContosoRG“ für die Produktion.
- Die virtuellen Computer der App werden zur primären Azure-Region (USA, Osten 2) migriert und im Produktionsnetzwerk (VNET-PROD-EUS2) platziert.
- Der virtuelle Front-End-Computer wird im Front-End-Subnetz (PROD-FE-EUS2) im Produktionsnetzwerk platziert.
- Der virtuelle Datenbankcomputer wird im Datenbanksubnetz (PROD-DB-EUS2) im Produktionsnetzwerk platziert.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Szenarioarchitektur](./media/contoso-migration-rehost-vm/architecture.png)

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Server durchgeführt. Hierbei haben die folgenden Überlegungen Contoso dabei unterstützt, sich für einen virtuellen Azure-IaaS-Computer zu entscheiden, auf dem SQL Server ausgeführt wird:

- Der Einsatz eines virtuellen Azure-Computers mit SQL Server erscheint als optimale Lösung, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen muss, oder wenn Drittanbieter-Apps auf demselben virtuellen Computer installiert und ausgeführt werden sollen.
- Dank Software Assurance kann Contoso vorhandene Lizenzen künftig mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen gegen eine verwaltete SQL-Datenbank-Instanz austauschen. So können 30% bei der verwalteten Instanz eingespart werden.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | Beide virtuellen Computer der App werden ohne Änderungen nach Azure verlagert, was die Migration vereinfacht.<br/><br/> Da Contoso beide virtuellen Computer der App per „Lift & Shift“-Ansatz migriert, sind für die App-Datenbank keine besonderen Konfigurations- oder Migrationstools erforderlich.<br/><br/> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil nutzen.<br/><br/> Contoso behält die vollständige Kontrolle über die virtuellen Computer der App in Azure.
**Nachteile** | Auf WEBVM und SQLVM wird Windows Server 2008 R2 ausgeführt. Das Betriebssystem wird für bestimmte Rollen von Azure unterstützt (Juli 2018). [Weitere Informationen](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)<br/><br/> Die Web- und Datenschichten der App bleiben ein Single Point of Failover.<br/><br/> SQLVM wird unter SQL Server 2008 R2 ausgeführt. Dieses Betriebssystem ist nicht im grundlegenden Support enthalten. Für virtuelle Azure-Computer wird es jedoch unterstützt (Juli 2018). [Weitere Informationen](https://support.microsoft.com/help/956893)<br/><br/> Contoso muss die App weiterhin als virtuelle Azure-Computer unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service oder Azure SQL-Datenbank umzustellen.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migrationsprozess

Contoso migriert das App-Front-End und die virtuellen Datenbankcomputer mit der Methode ohne Agent des Tools für die Azure Migrate-Servermigration zu virtuellen Azure-Computern.

- Im ersten Schritt bereitet Contoso Azure-Komponenten für die Azure Migrate-Servermigration vor, richtet diese ein und bereitet die lokale VMware-Infrastruktur vor.
- Sie verfügen bereits über die [Azure-Infrastruktur](./contoso-migration-infrastructure.md), sodass Contoso nur noch die Konfiguration der Replikation der virtuellen Computer über das Tool für die Azure Migrate-Servermigration hinzufügen muss.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der virtuellen Computer beginnen.
- Wenn die Replikation aktiviert wurde und funktioniert, migriert Contoso den virtuellen Computer via Failover zu Azure.

![Migrationsprozess](./media/contoso-migration-rehost-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Azure Migrate-Servermigration](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm) | Der Dienst organisiert und verwaltet die Migration Ihrer lokalen Anwendungen und Workloads sowie von AWS/GCP-VM-Instanzen. | Während der Replikation in Azure fallen Gebühren für Azure Storage an. Es werden Azure-VMs erstellt, und Gebühren fallen an, sobald ein Failover erfolgt. [Weitere Informationen](https://azure.microsoft.com/pricing/details/azure-migrate) zu Gebühren und Preisen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes.

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Contoso hat in einem früheren Artikel dieser Reihe Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.<br/><br/> Wenn Sie detailliertere Berechtigungen benötigen, lesen Sie [diesen Artikel](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-Infrastruktur** | [Weitere Informationen](./contoso-migration-infrastructure.md) zur Vorgehensweise von Contoso beim Einrichten einer Azure-Infrastruktur.<br/><br/> Erfahren Sie mehr über bestimmte [Voraussetzungen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prerequisites) für die Azure Migrate-Servermigration.
**Lokale Server** | Lokale vCenter-Server sollten als Version 5.5, 6.0 oder 6.5 ausgeführt werden.<br/><br/> ESXi-Hosts sollten Version 5.5, 6.0 oder 6.5 ausführen.<br/><br/> Mindestens eine VMware-VM sollte auf dem ESXi-Host ausgeführt werden.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso-Administratoren gehen bei der Ausführung der Migration wie folgt vor:

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

1. Einrichten eines Netzwerks: Im Rahmen der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) hat Contoso bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann.

    - Bei der SmartHotel360-App handelt es sich um eine Produktions-App. Die VMs werden zum Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten 2“ migriert.
    - Beide VMs werden in der Ressourcengruppe ContosoRG bereitgestellt, die für Produktionsressourcen verwendet wird.
    - Die App-Front-End-VM (WEBVM) wird zum Front-End-Subnetz (PROD-FE-EUS2) im Produktionsnetzwerk migriert.
    - Die App-Datenbank-VM (SQLVM) wird zum Datenbanksubnetz (PROD-DB-EUS2) im Produktionsnetzwerk migriert.

2. Bereitstellen des Tools für die Azure Migrate-Servermigration: Nach dem Einrichten des Netzwerks und des Speicherkontos kann Contoso nun einen Recovery Services-Tresor (ContosoMigrationVault) erstellen und diesen in der Ressourcengruppe „ContosoFailoverRG“ in der primären Region „USA, Osten 2“ platzieren.

    ![Tool für die Azure Migrate-Servermigration](./media/contoso-migration-rehost-vm/server-migration-tool.png)

**Benötigen Sie weitere Hilfe?**

[Hier finden Sie Informationen](https://docs.microsoft.com/azure/migrate) zur Einrichtung des Tools für die Azure Migrate-Servermigration.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Vorbereiten der Verbindungsherstellung mit Azure-VMs nach dem Failover

Nach dem Failover möchte Contoso eine Verbindung mit den Azure-VMs herstellen. Dazu führen Contoso-Administratoren vor der Migration folgende Schritte aus:

1. Für den Zugriff über das Internet:

    - Aktivieren von RDP auf dem lokalen virtuellen Computer vor dem Failover.
    - Sicherstellen, dass TCP- und UDP-Regeln zum **öffentlichen** Profil hinzugefügt wurden.
    - Bei allen Profilen unter **Windows-Firewall** > **Zugelassene Apps** überprüfen, ob RDP zulässig ist.

2. Für den Zugriff über Site-to-Site-VPN:

    - RDP auf dem lokalen Computer aktivieren.
    - RDP unter **Windows-Firewall** -> **Zugelassene Apps und Features** für **private und Domänennetzwerke** zulassen.
    - SAN-Richtlinie des Betriebssystems auf der lokalen VM auf **OnlineAll** festlegen.

Bei der Ausführung eines Failovers sind darüber hinaus folgende Aspekte zu überprüfen:

- Auf dem virtuellen Computer sollten keine ausstehenden Windows-Updates vorhanden sein, wenn Sie ein Failover auslösen. Andernfalls ist bis zum Abschluss des Updates keine Anmeldung bei dem virtuellen Computer möglich.
- Nach dem Failover kann **Startdiagnose** aktiviert werden, um einen Screenshot der VM anzuzeigen. Falls dies nicht funktioniert, sollte überprüft werden, ob die VM ausgeführt wird, und die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) gelesen werden.

**Benötigen Sie weitere Hilfe?**

- [Informationen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) zum Vorbereiten von virtuellen Computern für die Migration

## <a name="step-3-replicate-the-on-premises-vms"></a>Schritt 3: Replizieren der lokalen VMs

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können Sie mit der Replikation von VMware-VMs in Azure beginnen.

1. Wählen Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** die Option **Replizieren** aus.

    ![Replizieren von VMs](./media/contoso-migration-rehost-vm/select-replicate.png)

2. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere-Hypervisor** aus.

3. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance aus, die Sie eingerichtet haben, und dann **OK**.

    ![Quelleinstellungen](./media/contoso-migration-rehost-vm/source-settings.png)

4. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten.
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie hierzu unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung ausgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Auswählen der Bewertung](./media/contoso-migration-rehost-vm/select-assessment.png)

5. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und aktivieren Sie alle VMs, die Sie migrieren möchten. Wählen Sie anschließend **Next: Zieleinstellungen**.

6. Wählen Sie unter **Zieleinstellungen** das Abonnement und die Zielregion für die Migration aus, und geben Sie die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden. Wählen Sie unter **Virtuelles Netzwerk** das Azure-VNET/-Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

7. Wählen Sie unter **Azure-Hybridvorteil** Folgendes aus:

    - die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Wählen Sie **Weiter**aus.
    - Wählen Sie **Ja** aus, wenn Sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Wählen Sie **Weiter**aus.

8. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste für die VM-Größe die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der höchsten Übereinstimmung im Azure-Abonnement aus. Alternativ können Sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

9. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen, und wählen Sie in Azure den Datenträgertyp aus (SSD Standard/HDD Standard oder Managed Disks Premium). Wählen Sie **Weiter**aus.
    - Sie können Datenträger von der Replikation ausschließen.
    - Wenn Sie Datenträger ausschließen, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

10. Überprüfen Sie unter **Replikation prüfen und starten** die Einstellungen, und wählen Sie **Replizieren** aus, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-4-migrate-the-vms"></a>Schritt 4: Migrieren der VMs

Contoso-Administratoren führen ein schnelles Testfailover und dann ein vollständiges Failover aus, um die virtuellen Computer zu migrieren.

### <a name="run-a-test-failover"></a>Ausführen eines Testfailovers

1. Wählen Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** die Option **Migrierte Server testen** aus.

     ![Testen der migrierten Server](./media/contoso-migration-rehost-vm/test-migrated-servers.png)

2. Klicken Sie mit der rechten Maustaste auf den zu testenden virtuellen Computer, und wählen Sie anschließend **Testmigration** aus.

    ![Testmigration](./media/contoso-migration-rehost-vm/test-migrate.png)

3. Wählen Sie unter **Testmigration** das Azure VNET aus, in dem sich die Azure-VM nach der Migration befindet. Es empfiehlt sich, ein nicht für die Produktion bestimmtes VNET zu verwenden.
4. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
5. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
6. Klicken Sie nach Abschluss des Tests mit der rechten Maustaste unter **Aktuell replizierte Computer** auf den virtuellen Azure-Computer, und wählen Sie anschließend **Testmigration bereinigen** aus.

    ![Bereinigen der Migration](./media/contoso-migration-rehost-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrieren der VMs

Contoso-Administratoren führen jetzt ein vollständiges Failover aus, um die Migration abzuschließen.

1. Wählen Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** die Option **Server werden repliziert** aus.

    ![Replizieren der Server](./media/contoso-migration-rehost-vm/replicating-servers.png)

2. Klicken Sie unter **Aktuell replizierte Computer** mit der rechten Maustaste auf die VM und dann auf **Migrieren**.
3. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. So wird sichergestellt, dass keine Daten verloren gehen.
    - Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
4. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
5. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

**Benötigen Sie weitere Hilfe?**

- [Informationen](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) zum Ausführen eines Testfailovers.
- [Informationen](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) zur Migration von virtuellen Computern zu Azure.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration werden die Schichten der SmartHotel360-App jetzt auf Azure-VMs ausgeführt.

Contoso muss jetzt folgende Schritte für die Bereinigung durchführen:

- Beenden Sie nach Abschluss der Migration die Replikation.
- Entfernen des WEBVM-Computers aus dem vCenter-Bestand
- Entfernen des SQLVM-Computers aus dem vCenter-Bestand
- Entfernen von WEBVM und SQLVM aus lokalen Sicherungsaufträgen
- Aktualisieren der internen Dokumentation zum Anzeigen des neuen Speicherorts und der IP-Adressen für die VMs.
- Überprüfen sämtlicher Ressourcen, die mit den VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die App jetzt ausgeführt wird, muss Contoso sie nun vollständig in Azure operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs auf eventuell vorhandene Sicherheitsprobleme.

- Zur Steuerung des Zugriffs überprüft das Team die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer. Mithilfe von Netzwerksicherheitsgruppen wird sichergestellt, dass nur für die App zulässiger Datenverkehr die App erreichen kann.
- Das Team zieht darüber hinaus in Erwägung, die Daten mit Azure Disk Encryption und Key Vault zu sichern.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="bcdr"></a>BCDR

Für die Geschäftskontinuität und Notfallwiederherstellung (Business Continuity & Disaster Recovery, BCDR) führt Contoso die folgenden Aktionen durch:

- Schützen von Daten: Contoso sichert die Daten auf den VMs mithilfe des Azure Backup-Diensts. [Weitere Informationen](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- Sicherstellen eines unterbrechungsfreien Betriebs der Apps: Contoso repliziert die App-VMs in Azure mithilfe von Site Recovery in einer sekundären Region. [Weitere Informationen](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

1. Contoso verfügt über eine Lizenzierung für die VMs und nutzt den Azure-Hybridvorteil. Contoso wird die vorhandenen virtuellen Azure-Computer konvertieren, um von diesen Preisen zu profitieren.
2. Contoso aktiviert Azure Cost Management. Es ist durch Cloudyn lizenziert, ein Tochterunternehmen von Microsoft. Dabei handelt es sich um eine Kostenverwaltungslösung mit mehreren Clouds, die Ihnen das Verwenden und Verwalten von Azure und anderen Cloudressourcen erleichtert. [Erfahren Sie mehr](https://docs.microsoft.com/azure/cost-management/overview) über die Azure Cost Management.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat Contoso der SmartHotel360-App in Azure einen neuen Host zugewiesen, indem die virtuellen Computer der App mithilfe des Tools für die Azure Migrate-Servermigration zu Azure-VMs migriert wurden.
