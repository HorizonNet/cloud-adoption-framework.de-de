---
title: Zuweisen eines neuen Hosts für eine lokale Linux-Anwendung zu Azure-VMs
description: Dieser Artikel enthält Informationen zum Zuweisen eines neuen Hosts für eine lokale Linux-App durch Migration zu Azure-VMs.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 8272bf9084095f5b5e7bd1cd4cf6193fd7bd81c8
ms.sourcegitcommit: 26aee3c6f596bb8a9f1e16af93cdf94e41a61dee
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87400512"
---
<!-- cSpell:ignore givenscj OSTICKETWEB OSTICKETMYSQL OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc osTicket binlog systemctl NSGs distros -->

# <a name="rehost-an-on-premises-linux-application-to-azure-vms"></a>Zuweisen eines neuen Hosts für eine lokale Linux-Anwendung zu Azure-VMs

In diesem Artikel wird veranschaulicht, wie das fiktive Unternehmen Contoso für eine zweistufige [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung einen neuen Host zuweist, indem virtuelle Azure IaaS-Computer (Infrastructure-as-a-Service) verwendet werden.

Die in diesem Beispiel verwendete Service Desk-Anwendung osTicket wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/osTicket/osTicket) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und Infrastrukturen unter Druck.
- **Risikobegrenzung.** Die Service Desk-Anwendung ist wichtig für das Geschäft von Contoso. Contoso möchte sie ohne jedes Risiko nach Azure verlagern.
- **Erweitern.** Contoso möchte die Anwendung derzeit nicht ändern. Es soll sichergestellt werden, dass die Anwendung stabil ist.

## <a name="migration-goals"></a>Migrationsziele

Für die Bestimmung der besten Migrationsmethode hat das Contoso-Cloudteam Ziele für diese Migration festgelegt:

- Nach der Migration soll die Anwendung in Azure die gleichen Leistungsmerkmale wie derzeit in der lokalen VMware-Umgebung des Unternehmens aufweisen. Die Anwendung bleibt lokal und in der Cloud gleichermaßen wichtig.
- Contoso möchte nicht in diese Anwendung investieren. Die Investition ist wichtig für das Geschäft, aber in ihrer derzeitigen Form soll die Anwendung lediglich sicher in die Cloud verschoben werden.
- Contoso möchte das Vorgangsmodell für diese Anwendung nicht ändern. Das Unternehmen möchte in der Cloud genau wie jetzt mit der Anwendung interagieren können.
- Contoso möchte die Anwendungsfunktionen nicht ändern. Nur der Speicherort der Anwendung ändert sich.
- Nach Abschluss einer Reihe von Windows-Anwendungsmigrationen möchte Contoso mehr über die Verwendung einer Linux-basierten Infrastruktur in Azure erfahren.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess. Die Azure-Dienste, die von Contoso für die Migration verwendet werden sollen, werden ebenfalls identifiziert.

### <a name="current-application"></a>Aktuelle Anwendung

- Die Anwendung „osTicket“ ist auf zwei VMs aufgeteilt (`OSTICKETWEB` und `OSTICKETMYSQL`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird mit vCenter Server 6.5 (`vcenter.contoso.com`) verwaltet und auf einer VM ausgeführt.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Da es sich bei der Anwendung um eine Produktionsworkload handelt, befinden sich die virtuellen Computer in Azure in der Produktionsressourcengruppe `ContosoRG`.
- Die VMs werden zur primären Region (USA, Osten 2) migriert und im Produktionsnetzwerk (`VNET-PROD-EUS2`) platziert:
  - Die Web-VM wird sich im Front-End-Subnetz (`PROD-FE-EUS2`) befinden.
  - Die Datenbank-VM befindet sich im Subnetz der Datenbank (`PROD-DB-EUS2`).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Diagramm der Szenarioarchitektur.](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Beide virtuellen Anwendungscomputer werden unverändert in Azure verschoben. Dies vereinfacht die Migration. <br><br> Da Contoso beide virtuellen Anwendungscomputer per Lift & Shift-Vorgang migriert, sind für die Anwendungsdatenbank keine besonderen Konfigurations- oder Migrationstools erforderlich. <br><br> Contoso behält die vollständige Kontrolle über die Anwendungs-VMs in Azure. <br><br> Die Anwendungs-VMs führen Ubuntu 16.04-TLS aus, eine unterstützte Linux-Distribution. Informieren Sie sich über [von Azure unterstützte Linux-Distributionen](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros). |
| **Nachteile** | Die Web- und Datenschicht der Anwendung bleiben Single Points of Failover. <br><br> Contoso muss die Anwendung weiterhin als virtuelle Azure-Computer unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service oder Azure Database for MySQL umzustellen. <br><br> Contoso bemerkt, dass das Unternehmen bei Verwendung der einfachen Lift & Shift-VM-Migration nicht alle Vorteile der Features von [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) nutzt. Zu diesen Features gehören integrierte Hochverfügbarkeit, vorhersagbare Leistung, einfache Skalierung, automatische Sicherungen und integrierte Sicherheit. |

### <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

- Als ersten Schritt bereitet Contoso die Azure-Komponenten für die Azure Migrate- Servermigration vor und richtet sie ein. Anschließend bereitet es die lokale VMware-Infrastruktur vor.
- Das Unternehmen verfügt bereits über die [Azure-Infrastruktur](./contoso-migration-infrastructure.md), sodass es nur noch die Replikation der virtuellen Computer über das Tool für die Azure Migrate-Servermigration konfigurieren muss.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der virtuellen Computer beginnen.
- Wenn die Replikation aktiviert wurde und funktioniert, migriert Contoso den virtuellen Computer via Failover zu Azure.

![Diagramm zum Migrationsprozess.](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Migrate: Servermigration](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm) | Der Dienst orchestriert und verwaltet die Migration von Ihren lokalen Anwendungen und Workloads und von VM-Instanzen für Amazon Web Services (AWS)/Google Cloud Platform (GCP). | Während der Replikation in Azure fallen Gebühren für Azure Storage an. Es werden Azure-VMs erstellt, und Gebühren fallen an, sobald die Migration erfolgt. Informieren Sie sich über die [Gebühren und Preise](https://azure.microsoft.com/pricing/details/azure-migrate). |

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes.

Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat in einem früheren Artikel dieser Reihe Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden, aber nicht der Administrator sind, sollten Sie den Administrator bitten, Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuzuweisen. <br><br> Falls Sie präzisere Berechtigungen benötigen, helfen Ihnen die Informationen unter [Verwalten des Site Recovery-Zugriffs mit rollenbasierter Zugriffssteuerung (Role-Based Access Control, RBAC)](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control) weiter. |
| **Azure-Infrastruktur** | Informieren Sie sich darüber, [wie Contoso eine Azure-Infrastruktur einrichtet](./contoso-migration-infrastructure.md). <br><br> Erfahren Sie mehr über bestimmte [Voraussetzungen](./contoso-migration-devtest-to-iaas.md#prerequisites) für Azure Migrate: Servermigration. |
| **Lokale Server** | Auf dem lokalen vCenter-Server sollte Version 5.5, 6.0 oder 6.5 ausgeführt werden. <br><br> Ein ESXi-Host mit Version 5.5, 6.0 oder 6.5. <br><br> Mindestens eine VMware-VM auf dem ESXi-Host. |
| **Lokale VMs** | [Überprüfen Sie Linux-Distributionen](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten von Azure für die Azure Migrate- Servermigration.** Fügen Sie das Tool für die Azure Migrate- Servermigration dem Azure Migrate-Projekt hinzu.
> - **Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration.** Die Konten für die VM-Ermittlung werden vorbereitet, und die Herstellung einer Verbindung mit Azure-VMs nach der Migration wird vorbereitet.
> - **Schritt 3: Replizieren von VMs.** Einrichten der Replikation und Starten der VM-Replikation in Azure Storage
> - **Schritt 4: Migrieren der VMs mit der Azure Migrate- Servermigration.** Durchführen einer Testmigration, um sicherzustellen, dass alles funktioniert. Anschließend wird eine vollständige Migration ausgeführt, um die VMs in Azure zu verlagern.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 1: Vorbereiten von Azure für das Azure Migrate- Tool für die Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein virtuelles Netzwerk, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Azure Migrate: Das Tool für die Azure Migrate-Servermigration wurde bereitgestellt.

Diese Komponenten werden wie folgt eingerichtet:

1. Einrichten eines Netzwerks. Contoso hat bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann, als die [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) durchgeführt wurde.

    - Die Anwendung SmartHotel360 ist eine Produktionsanwendung. Die VMs werden zum Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) migriert.
    - Beide virtuellen Computer werden in der für Produktionsressourcen verwendeten Ressourcengruppe `ContosoRG` bereitgestellt.
    - Der virtuelle Computer für das Anwendungs-Front-End (`OSTICKETWEB`) wird zum Front-End-Subnetz (`PROD-FE-EUS2`) im Produktionsnetzwerk migriert.
    - Der virtuelle Computer für die Anwendungsdatenbank (`OSTICKETMYSQL`) wird zum Datenbanksubnetz (`PROD-DB-EUS2`) im Produktionsnetzwerk migriert.

1. Bereitstellen des Tools für die Azure Migrate- Servermigration“ kommunizieren kann. Nach dem Einrichten des Netzwerks und des Speicherkontos kann Contoso nun einen Recovery Services-Tresor (`ContosoMigrationVault`) erstellen und diesen in der Ressourcengruppe `ContosoFailoverRG` in der primären Region (`East US 2`) platzieren.

    ![Screenshot: Tool für die Azure Migrate-Servermigration](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über die [Einrichtung des Tools für die Azure Migrate-Servermigration](https://docs.microsoft.com/azure/migrate).

## <a name="step-2-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration

Nach der Migration zu Azure möchte Contoso eine Verbindung mit den replizierten VMs in Azure herstellen können. Hierfür müssen die Contoso-Administratoren die folgenden Schritte ausführen:

- Für den Zugriff auf virtuelle Azure-Computer über das Internet müssen sie vor der Migration auf dem lokalen Linux-Computer SSH aktivieren. Bei Ubuntu kann dieser Schritt mit dem folgenden Befehl ausgeführt werden: `sudo apt-get ssh install -y`.
- Installieren des [Azure Linux-Agents](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux)
- Nach der Durchführung der Migration können sie die **Startdiagnose** überprüfen, um einen Screenshot des virtuellen Computers anzuzeigen.
- Falls dies nicht funktioniert, müssen sie überprüfen, ob der virtuelle Computer ausgeführt wird, und sie sollten die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) lesen.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie [VMs auf die Migration vorbereiten](https://docs.microsoft.com/azure/migrate/prepare-for-migration).

## <a name="step-3-replicate-the-on-premises-vms"></a>Schritt 3: Replizieren der lokalen VMs

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, beginnen sie mit der Replikation von VMware-VMs in Azure.

1. Wechseln Sie im Azure Migrate-Projekt zu **Server** > **Azure Migrate- Servermigration**, und wählen Sie die Option **Replizieren** aus.

    ![Screenshot: Option „Replizieren“](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere** aus.

3. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance, die Sie eingerichtet haben, und dann **OK** aus.

    ![Screenshot: Registerkarte „Quelleinstellungen“](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten.
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung durchgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Screenshot: Auswählen von Bewertungen](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und wählen Sie alle VMs aus, die Sie migrieren möchten. Wählen Sie anschließend **Next: Zieleinstellungen**.

6. Wählen Sie in **Zieleinstellungen** das Abonnement und die Zielregion aus, zu der Sie migrieren. Geben Sie die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden sollen. Wählen Sie unter **Virtuelles Netzwerk** das virtuelle Azure-Netzwerk oder -Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

7. Wählen Sie unter **Azure-Hybridvorteil**

    - die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Wählen Sie **Weiter**aus.
    - Wählen Sie **Ja** aus, wenn Sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Wählen Sie **Weiter**aus.

8. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste für die VM-Größe die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der größten Übereinstimmung im Azure-Abonnement aus. Alternativ können Sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

9. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen. Wählen Sie den Datenträgertyp (SSD/HDD Standard oder verwaltete Premium-Datenträger) in Azure aus. Wählen Sie **Weiter** aus.
    - Sie können Datenträger von der Replikation ausschließen.
    - Wenn Sie Datenträger ausschließen, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

10. Überprüfen Sie die Einstellungen unter **Replikation überprüfen und starten**. Wählen Sie anschließend **Replizieren** aus, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-4-migrate-the-vms"></a>Schritt 4: Migrieren der VMs

Die Contoso-Administratoren führen eine schnelle Testmigration und dann eine Migration aus, um die VMs zu verlagern.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** die Option **Migrierte Server testen** aus.

     ![Screenshot: Option „Migrierte Server testen“](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

1. Wählen Sie die zu testende VM aus, und halten Sie sie gedrückt (oder klicken Sie mit der rechten Maustaste). Wählen Sie anschließend die Option **Testmigration** aus.

    ![Screenshot: Option „Testmigration“](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

1. Wählen Sie unter **Testmigration** das virtuelle Azure-Netzwerk aus, in dem sich der virtuelle Azure-Computer nach der Migration befindet. Wir empfehlen Ihnen, ein nicht für die Produktion bestimmtes virtuelles Netzwerk zu verwenden.
1. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
1. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
1. Wählen und halten Sie nach Abschluss des Tests unter **Aktuell replizierte Computer** die Azure-VM (oder klicken Sie mit der rechten Maustaste darauf). Wählen Sie anschließend **Testmigration bereinigen** aus.

    ![Screenshot: Option „Testmigration bereinigen“](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrieren der VMs

Die Contoso-Administratoren führen jetzt eine vollständige Migration aus, um die Verlagerung abzuschließen.

1. Wechseln Sie im Azure Migrate-Projekt zu **Server** > **Azure Migrate- Servermigration**, und wählen Sie die Option **Server werden repliziert** aus.

    ![Screenshot: Option „Server werden repliziert“](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

1. Wählen und halten Sie unter **Aktuell replizierte Computer** die VM (oder klicken Sie mit der rechten Maustaste darauf), und wählen Sie **Migrieren** aus.
1. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. Mit dieser Aktion wird sichergestellt, dass es nicht zu Datenverlusten kommt.
    - Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
1. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
1. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

### <a name="connect-the-vm-to-the-database"></a>Verbinden der VM mit der Datenbank

Der letzte Schritt im Migrationsprozess besteht in der Aktualisierung der Verbindungszeichenfolge der Anwendung durch die Contoso-Administratoren, um auf die Anwendungsdatenbank zu verweisen, die auf dem virtuellen Computer `OSTICKETMYSQL` ausgeführt wird.

1. Stellen Sie über PuTTY oder einen anderen SSH-Client eine SSH-Verbindung mit der `OSTICKETWEB`-VM her. Da die VM privat ist, sollten Sie die Verbindung über die private IP-Adresse herstellen.

    ![Screenshot: Bereich „Verbindung mit virtuellem Computer herstellen“](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Screenshot: Verbindung mit der Datenbank](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

1. Stellen Sie sicher, dass die `OSTICKETWEB`-VM mit der `OSTICKETMYSQL`-VM kommunizieren kann. Die Konfiguration ist mit der lokalen IP-Adresse `172.16.0.43` derzeit hartcodiert.

    **Vor dem Update:**

    ![Screenshot: IP-Adresse vor dem Update](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Nach dem Update:**

    ![Screenshot: IP-Adresse nach dem Update](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

1. Starten Sie den Dienst mit dem Befehl **systemctl restart apache2** neu.

    ![Screenshot: Neustart des Diensts](./media/contoso-migration-rehost-linux-vm/restart.png)

1. Aktualisieren Sie abschließend die DNS-Einträge für `OSTICKETWEB` und `OSTICKETMYSQL` auf einem der Contoso-Domänencontroller.

    ![Screenshot: Aktualisieren eines DNS-Eintrags](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Screenshot: Aktualisieren eines DNS-Eintrags](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über das [Ausführen einer Testmigration](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration).
- Informieren Sie sich über das [Migrieren von virtuellen Computern zu Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration werden die Schichten der Anwendung osTicket jetzt auf Azure-VMs ausgeführt.

Contoso muss nun die folgenden Aufgaben durchführen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation zum Anzeigen des neuen Speicherorts und der IP-Adressen für `OSTICKETWEB` und `OSTICKETMYSQL`.
- Überprüfen aller Ressourcen, die mit den VMs interagieren. Alle relevanten Einstellungen bzw. Dokumentationsinhalte müssen aktualisiert werden, um die neue Konfiguration widerzuspiegeln.
- Contoso hat den Azure Migrate-Dienst mit Management-VM verwendet, um die VMs für die Migration zu bewerten. Administratoren sollten die Migrations-VM und die Web-VMs vom VMware ESXi-Server entfernen.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die Anwendung nun ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die VMs OSTICKETWEB und OSTICKETMYSQL, um mögliche Sicherheitsprobleme zu ermitteln.

- Das Team überprüft die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer zur Steuerung des Zugriffs. Mithilfe von NSGs wird sichergestellt, dass nur für die App zulässiger Datenverkehr übergeben werden kann.
- Das Team zieht darüber hinaus in Betracht, die Daten auf den Datenträgern des virtuellen Computers mit Azure Disk Encryption und Azure Key Vault zu schützen.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

<!-- docsTest:ignore "Quickstart: Set" -->

### <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- **Schützen von Daten.** Contoso sichert die Daten auf den VMs mithilfe der [Azure-VM-Sicherung](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction).
- **Aufrechterhalten des Anwendungsbetriebs.** Contoso repliziert die virtuellen Anwendungscomputer in Azure mit Site Recovery in einer sekundären Region. Weitere Informationen finden Sie unter [Quickstart: Einrichten der Notfallwiederherstellung in einer sekundären Azure-Region für einen virtuellen Azure-Computer](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nach der Bereitstellung von Ressourcen, weist der Contoso Azure Tags zu, die während der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md#set-up-tagging) definiert wurden.
- Contoso hat mit den Ubuntu-Servern keine Lizenzierungsprobleme.
- Contoso verwendet [Azure Cost Management und Abrechnung](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget vom Unternehmen nicht überschritten wird.
