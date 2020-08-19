---
title: Zuweisen eines neuen Hosts für eine lokale Linux-App zu Azure-VMs und Azure Database for MySQL
description: Dieser Artikel enthält Informationen zum Zuweisen eines neuen Hosts für eine lokale Linux-App durch Migration zu Azure-VMs und Azure Database for MySQL.
author: givenscj
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 86feba84b8bec522d887c788f4942492ffa8dce8
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88567341"
---
<!-- cSpell:ignore givenscj OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc contosoosticket osticket InnoDB binlog systemctl NSGs -->

# <a name="rehost-an-on-premises-linux-application-to-azure-vms-and-azure-database-for-mysql"></a>Zuweisen eines neuen Hosts für eine lokale Linux-App zu Azure-VMs und Azure Database for MySQL

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso einer zweistufigen [LAMP-basierten](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung einen neuen Host zuweist und sie mithilfe von virtuellen Azure-Computern (VMs) und Azure Database for MySQL aus einer lokalen Umgebung zu Azure migriert.

Die in diesem Beispiel verwendete Service Desk-Anwendung osTicket wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese Anwendung für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/osTicket/osTicket) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam arbeitet eng mit Geschäftspartnern zusammen, um genau zu verstehen, was erreicht werden soll:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und Infrastrukturen unter Druck.
- **Risikobegrenzung.** Die Service Desk-Anwendung ist wichtig für das Unternehmen. Contoso möchte sie ohne jedes Risiko nach Azure verlagern.
- **Erweitern.** Contoso möchte die Anwendung derzeit nicht ändern. Das Unternehmen möchte, dass die Anwendung weiterhin stabil ausgeführt wird.

## <a name="migration-goals"></a>Migrationsziele

Für die Bestimmung der besten Migrationsmethode hat das Contoso-Cloudteam Ziele für diese Migration festgelegt:

- Nach der Migration soll die Anwendung in Azure die gleichen Leistungsmerkmale wie derzeit in der lokalen VMware-Umgebung des Unternehmens aufweisen. Die Anwendung bleibt lokal und in der Cloud gleichermaßen wichtig.
- Contoso möchte nicht in diese Anwendung investieren. Die Investition ist wichtig für das Geschäft, aber in ihrer derzeitigen Form soll die Anwendung lediglich sicher in die Cloud verschoben werden.
- Nach Abschluss einer Reihe von Windows-Anwendungsmigrationen möchte Contoso mehr über die Verwendung einer Linux-basierten Infrastruktur in Azure erfahren.
- Contoso möchte die Administratoraufgaben für die Datenbank minimieren, nachdem die Anwendung in die Cloud verschoben wird.

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Szenario:

- Aktuell ist die App auf zwei VMs aufgeteilt (`OSTICKETWEB` und `OSTICKETMYSQL`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird mit vCenter Server 6.5 (`vcenter.contoso.com`) verwaltet und auf einer VM ausgeführt.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).
- Die Webanwendung unter `OSTICKETWEB` wird zu einer Azure-IaaS-VM (Infrastructure-as-a-Service) migriert.
- Die Anwendungsdatenbank wird zu Azure Database for MySQL (Platform-as-a-Service) migriert.
- Da Contoso eine Produktionsworkload migriert, befinden sich die Ressourcen dann in der Ressourcengruppe `ContosoRG` für die Produktion.
- Die `OSTICKETWEB`-Ressource wird in der primären Region (USA, Osten 2) repliziert und im Produktionsnetzwerk (`VNET-PROD-EUS2`) abgelegt:
  - Die Web-VM wird sich im Front-End-Subnetz (`PROD-FE-EUS2`) befinden.
- Die Anwendungsdatenbank wird mit [Azure Database Migration Service](/azure/dms/dms-overview) zu Azure Database for MySQL migriert.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

    ![Diagramm der Szenarioarchitektur.](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

Zur Migration der Web-VM:

- In einem ersten Schritt richtet Contoso die Azure-Infrastruktur und die lokale Infrastruktur ein, die für die Bereitstellung von Azure Migrate erforderlich sind.
- Das Unternehmen verfügt bereits über die [Azure-Infrastruktur](./contoso-migration-infrastructure.md), sodass es nur noch die Replikation der virtuellen Computer über das Tool für die Azure Migrate-Servermigration hinzufügen und konfigurieren muss.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren des virtuellen Computers beginnen.
- Nachdem die Replikation aktiviert wurde und funktioniert, schließt Contoso den Umzug mithilfe von Azure Migrate ab.

Zur Migration der Datenbank:

1. Contoso stellt eine MySQL-Instanz in Azure bereit.
1. Contoso richtet Database Migration Service ein und stellt so den Zugriff auf den lokalen Datenbankserver sicher.
1. Contoso migriert die Datenbank zu Azure Database for MySQL.

    ![Diagramm zum Migrationsprozess.](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Migrate](/azure/migrate/migrate-services-overview) | Contoso verwendet Azure Migrate, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | [Azure Migrate](https://azure.microsoft.com/pricing/details/azure-migrate) ist ohne Aufpreis erhältlich. Je nach den Tools (Originalanbieter oder ISV), die Sie für die Bewertung und Migration verwenden, können aber ggf. Gebühren anfallen. |
| [Azure Database Migration Service](/azure/dms/dms-overview) | Database Migration Service ermöglicht die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen bei minimaler Ausfallzeit. | Informieren Sie sich über die [unterstützten Regionen](/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Azure Database for MySQL](/azure/mysql) | Die Datenbank basiert auf der Open-Source-MySQL-Datenbank-Engine. Sie stellt eine vollständig verwaltete, unternehmensgerechte MySQL Community-Datenbank für die Entwicklung und Bereitstellung von Apps bereit. | Erfahren Sie mehr über [Preise](https://azure.microsoft.com/pricing/details/mysql) und Skalierbarkeits-Optionen zu Azure Database for MySQL. |

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden, aber nicht der Administrator sind, sollten Sie den Administrator bitten, Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuzuweisen. <br><br> Falls Sie präzisere Berechtigungen benötigen, helfen Ihnen die Informationen unter [Verwalten des Site Recovery-Zugriffs mit rollenbasierter Zugriffssteuerung (Role-Based Access Control, RBAC)](/azure/site-recovery/site-recovery-role-based-linked-access-control) weiter. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Contoso – Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) beschrieben. |
| **Lokale Server** | Auf der lokalen vCenter Server-Instanz sollte Version 5.5, 6.0, 6.5 oder 6.7 ausgeführt werden. <br><br> Ein ESXi-Host mit Version 5.5, 6.0, 6.5 oder 6.7. <br><br> Mindestens eine VMware-VM auf dem ESXi-Host. |
| **Lokale VMs** | [Überprüfen Sie Linux-Computer](/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird. |

## <a name="scenario-steps"></a>Szenarioschritte

Die Contoso-Administratoren gehen bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten von Azure für die Azure Migrate- Servermigration.** Hinzufügen des Tools für die Servermigration zum Azure Migrate-Projekt
> - **Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration.** Vorbereiten von Konten für die VM-Ermittlung sowie der Herstellung einer Verbindung mit virtuellen Azure-Computern nach der Migration
> - **Schritt 3: Replizieren von VMs.** Einrichten der Replikation und Starten der VM-Replikation in Azure Storage
> - **Schritt 4: Migrieren der App-VM mit Azure Migrate: Servermigration.** Durchführen einer Testmigration, um die allgemeine Funktionsweise sicherzustellen, und anschließendes Durchführen einer vollständigen Migration, um die VM nach Azure zu verschieben
> - **Schritt 5: Migrieren der Datenbank:** Einrichten der Migration per Azure Database Migration Service

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 1: Vorbereiten von Azure für das Azure Migrate- Tool für die Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein virtuelles Netzwerk, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Azure Migrate: Das Tool für die Azure Migrate-Servermigration (OVA) wurde bereitgestellt und konfiguriert.

Die Contoso-Administratoren führen zum Einrichten der Komponenten die folgenden Schritte aus:

1. Einrichten eines Netzwerks. Contoso hat bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann, als die [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) durchgeführt wurde.

1. Bereitstellen des Tools für die Azure Migrate- Servermigration“.

    1. Laden Sie das OVA-Image über Azure Migrate herunter, und importieren Sie es in VMware.

        ![Screenshot: Herunterladen der OVA-Datei](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    1. Starten Sie das importierte Image, und konfigurieren Sie das Tool, indem Sie die folgenden Schritte ausführen:

       1. Richten Sie die erforderlichen Komponenten ein.

          ![Screenshot: Bildschirm zum Einrichten der erforderlichen Komponenten](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

       1. Stellen Sie die Verweise des Tools auf das Azure-Abonnement ein.

          ![Screenshot: Konfigurieren des Abonnements](./media/contoso-migration-rehost-vm/migration-register-azure.png)

       1. Legen Sie die VMware vCenter-Anmeldeinformationen fest.

          ![Screenshot: Konfigurieren der Anmeldeinformationen](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

       1. Fügen Sie alle Linux-basierten Anmeldeinformationen für die Ermittlung hinzu.

          ![Screenshot: Konfigurieren der Linux-basierten Anmeldeinformationen](./media/contoso-migration-rehost-vm/migration-credentials.png)

1. Nach der Konfiguration des Tools dauert es einige Zeit, bis das Tool alle virtuellen Computer aufgelistet hat. Nachdem der Vorgang abgeschlossen ist, werden die virtuellen Computer im Azure Migrate-Tool in Azure angezeigt.

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über die Einrichtung der [Azure Migrate: Servermigration](/azure/migrate/migrate-services-overview#azure-migrate-server-migration-tool).

## <a name="step-2-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration

Nach der Migration zu Azure möchte Contoso eine Verbindung mit den replizierten VMs in Azure herstellen können. Hierfür müssen die Contoso-Administratoren die folgenden Schritte ausführen:

- Für den Zugriff auf virtuelle Azure-Computer müssen sie vor der Migration auf dem lokalen Linux-Computer SSH aktivieren. Bei Ubuntu kann dieser Schritt mit dem folgenden Befehl ausgeführt werden: `sudo apt-get ssh install -y`.
- Nach Durchführung der Migration können die Administratoren die **Startdiagnose** aktivieren, um einen Screenshot des virtuellen Computers anzuzeigen.
- Falls dies nicht funktioniert, müssen sie überprüfen, ob der virtuelle Computer ausgeführt wird, und sie sollten die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) lesen.
- Installieren des [Azure Linux Agents](/azure/virtual-machines/extensions/agent-linux).

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie [VMs auf die Migration vorbereiten](/azure/migrate/prepare-for-migration).

## <a name="step-3-replicate-vms"></a>Schritt 3: Replizieren von VMs

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können sie mit der Replikation der Anwendungs-VM in Azure beginnen.

1. Wechseln Sie im Azure Migrate-Projekt zu **Server** > **Azure Migrate- Servermigration**, und wählen Sie die Option **Replizieren** aus.

    ![Screenshot: Option „Replizieren“](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

1. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere** aus.

1. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance, die Sie eingerichtet haben, und dann **OK** aus.

    ![Screenshot: Registerkarte „Quelleinstellungen“](./media/contoso-migration-rehost-linux-vm/source-settings.png)

1. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten:
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung durchgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Screenshot: Auswählen von Bewertungen](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

1. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und wählen Sie alle VMs aus, die Sie migrieren möchten. Wählen Sie anschließend **Next: Zieleinstellungen**.

1. Wählen Sie in **Zieleinstellungen** das Abonnement und die Zielregion aus, zu der Sie migrieren. Geben Sie die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden sollen. Wählen Sie unter **Virtuelles Netzwerk** das virtuelle Azure-Netzwerk oder -Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

1. Wählen Sie unter **Azure-Hybridvorteil**

    - die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Wählen Sie **Weiter**aus.

1. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste „VM-Größe“ die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der größten Übereinstimmung im Azure-Abonnement aus. Alternativ können Sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

1. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen. Wählen Sie anschließend in Azure den Datenträgertyp (SSD/HDD Standard oder verwaltete Premium-Datenträger) und dann **Weiter** aus.
    - Sie können Datenträger von der Replikation ausschließen.
    - Wenn Sie Datenträger ausschließen, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

1. Überprüfen Sie die Einstellungen unter **Replikation überprüfen und starten**. Wählen Sie anschließend **Replizieren** aus, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-4-migrate-the-vm-with-azure-migrate-server-migration"></a>Schritt 4: Migrieren der VM mit der Azure Migrate- Servermigration

Die Contoso-Administratoren führen eine schnelle Testmigration und dann eine vollständige Migration aus, um die Web-VM zu verlagern.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** die Option **Migrierte Server testen** aus.

     ![Screenshot: Option „Migrierte Server testen“](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

1. Wählen und halten Sie (oder klicken Sie mit der rechten Maustaste auf) die zu testende VM, und wählen Sie anschließend **Testmigration** aus.

    ![Screenshot: Option „Testmigration“](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

1. Wählen Sie unter **Testmigration** das virtuelle Azure-Netzwerk aus, in dem sich der virtuelle Azure-Computer nach der Migration befindet. Wir empfehlen Ihnen, ein nicht für die Produktion bestimmtes virtuelles Netzwerk zu verwenden.
1. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
1. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
1. Wählen und halten Sie nach Abschluss des Tests unter **Aktuell replizierte Computer** die Azure-VM (oder klicken Sie mit der rechten Maustaste darauf). Wählen Sie anschließend **Testmigration bereinigen** aus.

    ![Screenshot: Option „Testmigration bereinigen“](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vm"></a>Migrieren der VM

Die Contoso-Administratoren führen jetzt eine vollständige Migration aus, um die Verlagerung abzuschließen.

1. Wechseln Sie im Azure Migrate-Projekt zu **Server** > **Azure Migrate- Servermigration**, und wählen Sie die Option **Server werden repliziert** aus.

    ![Screenshot: Option „Server werden repliziert“](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

1. Wählen und halten Sie unter **Aktuell replizierte Computer** die VM (oder klicken Sie mit der rechten Maustaste darauf), und wählen Sie dann **Migrieren** aus.
1. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. Mit dieser Aktion wird sichergestellt, dass es nicht zu Datenverlusten kommt.
    - Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
1. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
1. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

## <a name="step-5-provision-azure-database-for-mysql"></a>Schritt 5: Bereitstellen von Azure Database for MySQL

Die Administratoren von Contoso stellen eine MySQL-Datenbankinstanz in der primären Region (`East US 2`) bereit.

1. Erstellen Sie im Azure-Portal eine Azure Database for MySQL-Ressource.

    ![Screenshot: Option „Azure Database for MySQL“](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

1. Der Name `contosoosticket` wird für die Azure-Datenbank hinzugefügt. Fügen Sie die Datenbank der Produktionsressourcengruppe `ContosoRG` hinzu, und geben Sie Anmeldeinformationen dafür an.
1. Die lokale MySQL-Datenbank ist in Version 5.7 vorhanden. Wählen Sie aus Kompatibilitätsgründen daher diese Version aus. Verwenden Sie die Standardgrößen, die die Datenbankanforderungen erfüllen.

     ![Screenshot: MySQL-Anmeldeinformationen](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

1. Wählen Sie unter **Optionen für Sicherungsredundanz** die Option **Georedundant** aus. Diese Option ermöglicht es Ihnen, die Datenbank bei einem Ausfall in der sekundären Region (`Central US`) wiederherzustellen. Sie können diese Option nur konfigurieren, wenn Sie die Datenbank bereitstellen.

     ![Screenshot: Option „Georedundant“](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

1. Navigieren Sie im Netzwerk `VNET-PROD-EUS2` zu **Dienstendpunkte**, und fügen Sie einen Dienstendpunkt (ein Datenbanksubnetz) für den SQL-Dienst hinzu.

    ![Screenshot: Hinzufügen von Dienstendpunkten](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

1. Erstellen Sie nach dem Hinzufügen des Subnetzes eine VNET-Regel, die Zugriff vom Datenbanksubnetz im Produktionsnetzwerk zulässt.

    ![Screenshot: Erstellen einer VNET-Regel](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-6-migrate-the-database"></a>Schritt 6: Migrieren der Datenbank

Es gibt mehrere Möglichkeiten, die MySQL-Datenbank zu verschieben. Bei jeder Option müssen die Contoso-Administratoren eine Azure Database for MySQL-Instanz für das Ziel erstellen. Nach der Erstellung kann die Migration auf zwei Arten durchgeführt werden, die in den folgenden Schritten beschrieben sind:

- 6a: Database Migration Service
- 6b: Sicherung und Wiederherstellung von MySQL Workbench

### <a name="step-6a-migrate-the-database-via-database-migration-service"></a>Schritt 6a: Migrieren der Datenbank per Database Migration Service

Die Administratoren von Contoso migrieren die Datenbank mit Database Migration Service, indem sie die Schritte im [ausführlichen Migrationstutorial](/azure/dms/tutorial-mysql-azure-mysql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) von MySQL 5.6 oder 5.7 ausführen.

> [!NOTE]
> MySQL 8.0 wird in Azure Database for MySQL unterstützt, aber das Database Migration Service-Tool unterstützt diese Version noch nicht.

Dieser Sachverhalt lässt sich so zusammenfassen, dass die Contoso-Administratoren die folgenden Aufgaben durchführen müssen:

- Sicherstellen, dass alle Voraussetzungen für die Migration erfüllt sind:
  - Die Version der Datenbankquelle des MySQL-Servers muss mit der Version übereinstimmen, die von Azure Database for MySQL unterstützt wird. Azure Database for MySQL unterstützt die MySQL Community Edition, die InnoDB-Speicher-Engine sowie die Migration zwischen der Quelle und dem Ziel mit derselben Version.
  - Aktivieren Sie die binäre Protokollierung in `my.ini` (Windows) oder `my.cnf` (Unix). Andernfalls tritt im Migrations-Assistenten der folgende Fehler auf: „Fehler bei der binären Protokollierung. Die Variable binlog_row_image weist den Wert 'minimal' auf. Ändern Sie diesen in 'full'.“ Weitere Informationen finden Sie auf der [MySQL-Website](https://go.microsoft.com/fwlink/?linkid=873009`).
  - Der Benutzer muss über die `ReplicationAdmin`-Rolle verfügen.
  - Migrieren Sie die Datenbankschemas ohne Fremdschlüssel und Trigger.
- Erstellen Sie ein virtuelles Netzwerk, das über Azure ExpressRoute oder VPN mit Ihrem lokalen Netzwerk verbunden ist.
- Erstellen Sie eine Database Migration Service-Instanz mit einer `Premium`-SKU, die mit dem virtuellen Netzwerk verbunden ist.
- Vergewissern Sie sich, dass die Instanz über das virtuelle Netzwerk auf die MySQL-Datenbank zugreifen kann. Stellen Sie sicher, dass alle eingehenden Ports von Azure zu MySQL auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem MySQL gehostet ist, zugelassen werden.
- Ausführen des Database Migration Service-Tools:
  - Erstellen Sie ein Migrationsprojekt.

    ![Screenshot: Erstellen eines Migrationsprojekts](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-new-project.png)

    ![Screenshot: Bereich „Neues Migrationsprojekt“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-new-project-02.png)

  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.

    ![Screenshot: Bereich „Quelldetails hinzufügen“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-source.png)

  - Wählen Sie ein Ziel aus.

    ![Screenshot: Bereich „Zieldetails“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-target.png)

  - Wählen Sie die zu migrierenden Datenbanken aus.

    ![Screenshot: Bereich „Den Zieldatenbanken zuordnen“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-databases.png)

  - Konfigurieren Sie die erweiterten Einstellungen.

    ![Screenshot: Bereich „Migrationseinstellungen“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-settings.png)

  - Starten Sie die Replikation, und beheben Sie alle Fehler.

    ![Screenshot: Fehlerbehebung](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-monitor.png)

  - Führen Sie den abschließenden Cutover (Systemwechsel) durch. ![Screenshot: Abschließender Cutover](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover.png)

    ![Screenshot: Bereich „Umstellung abschließen“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-complete.png)

    ![Screenshot: Liste „Migrationsaktivitäten“](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-complete-02.png)

  - Setzen Sie alle Fremdschlüssel und Trigger wieder ein.
  - Ändern Sie die Anwendungen so, dass sie die neue Datenbank verwenden.

    ![Screenshot: Ändern von Anwendungen für die Verwendung der neuen Datenbank](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-apps.png)

### <a name="step-6b-migrate-the-database-mysql-workbench"></a>Schritt 6b: Migrieren der Datenbank (MySQL Workbench)

Die Contoso-Administratoren migrieren die Datenbank mittels Sicherung und Wiederherstellung mit MySQL-Tools. Das Unternehmen installiert MySQL Workbench, speichert die Datenbank aus `OSTICKETMYSQL` und stellt sie dann wieder in der Azure Database for MySQL-Instanz her.

### <a name="install-mysql-workbench"></a>Installieren von MySQL Workbench

1. Überprüfen Sie die [Voraussetzungen, und laden Sie MySQL Workbench herunter](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).

1. Installieren Sie MySQL Workbench für Windows, indem Sie die [Installationsanleitung](https://dev.mysql.com/doc/workbench/en/wb-installing.html) befolgen.

1. Erstellen Sie in MySQL Workbench eine MySQL-Verbindung mit OSTICKETMYSQL.

    ![Screenshot: Registerkarte „Verbindung“](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

1. Exportieren Sie die Datenbank als `osticket` in eine lokale eigenständige Datei.

    ![Screenshot: Bildschirm „Datenexport“](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

1. Erstellen Sie eine Verbindung mit der Azure Database for MySQL-Instanz, nachdem die Datenbank lokal gesichert wurde.

    ![Screenshot: Popupmeldung „Erfolgreicher Verbindungsaufbau“](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

1. Führen Sie nun den Import (die Wiederherstellung) der Datenbank aus der eigenständigen Datei in die Azure Database for MySQL-Instanz durch. Ein neues Schema (`osticket`) wird für die Instanz erstellt.

    ![Screenshot: Option für Import aus eigenständiger Datei](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

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

1. Starten Sie den Dienst mit `systemctl restart apache2` neu.

    ![Screenshot: Neustart des Diensts](./media/contoso-migration-rehost-linux-vm/restart.png)

1. Aktualisieren Sie abschließend die DNS-Einträge für `OSTICKETWEB` und `OSTICKETMYSQL` auf einem der Contoso-Domänencontroller.

    ![Screenshot: Aktualisieren eines DNS-Eintrags](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Screenshot: Aktualisieren eines DNS-Eintrags](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über das [Ausführen einer Testmigration](/azure/migrate/tutorial-migrate-vmware#run-a-test-migration).
- Informieren Sie sich über das [Migrieren von virtuellen Computern zu Azure](/azure/migrate/tutorial-migrate-vmware#migrate-vms).

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die Anwendung jetzt ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und sichern.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration werden die Ebenen der Anwendung osTicket jetzt auf Azure-VMs ausgeführt.

Contoso muss nun die folgenden Aufgaben durchführen:

- Das Unternehmen entfernt die VMware-VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation und zeigt neue Speicherorte und IP-Adressen an.
- Es überprüft alle Ressourcen, die mit den lokalen VMs interagieren. Alle relevanten Einstellungen bzw. Dokumentationsinhalte müssen aktualisiert werden, um die neue Konfiguration widerzuspiegeln.
- Contoso hat mit Azure Migrate durch die Zuordnung von Abhängigkeiten die `OSTICKETWEB`-VM für die Migration bewertet.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die VM und die Datenbank, um mögliche Sicherheitsprobleme zu ermitteln:

- Es überprüft die Netzwerksicherheitsgruppen (NSGs) für die VM zur Steuerung des Zugriffs. Mithilfe von NSGs wird sichergestellt, dass nur für die App zulässiger Datenverkehr übergeben werden kann.
- Das Sicherheitsteam erwägt darüber hinaus, die Daten auf den VM-Datenträgern mithilfe von Azure Disk Encryption und Azure Key Vault zu schützen.
- Die Kommunikation zwischen der VM und der Datenbankinstanz ist nicht für SSL konfiguriert. SSL muss konfiguriert werden, um sicherzustellen, dass der Datenbank-Datenverkehr nicht gehackt werden kann.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](/azure/security/fundamentals/iaas).

<!-- docsTest:ignore "Quickstart: Set" -->

### <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- **Schützen von Daten.** Contoso sichert die Daten auf der Anwendungs-VM mit den [Sicherungsmöglichkeiten für VMs von Azure](/azure/backup/backup-azure-vms-introduction). Das Unternehmen muss die Sicherung für die Datenbank nicht konfigurieren. Azure Database for MySQL erstellt und speichert Serversicherungen automatisch. Contoso hat sich für die Verwendung der Georedundanz für die Datenbank entschieden, damit sie resilient und einsatzbereit für die Produktion ist.
- **Aufrechterhalten des Anwendungsbetriebs.** Contoso repliziert die virtuellen Anwendungscomputer in Azure mit Site Recovery in einer sekundären Region. Weitere Informationen finden Sie unter [Quickstart: Einrichten der Notfallwiederherstellung in einer sekundären Azure-Region für einen virtuellen Azure-Computer](/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nach der Bereitstellung von Ressourcen weist Contoso Azure-Tags zu, die während der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md#set-up-tagging) definiert wurden.
- Es gibt keine Lizenzierungsprobleme für die Contoso Ubuntu-Server.
- Contoso verwendet [Azure Cost Management und Abrechnung](/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget vom Unternehmen nicht überschritten wird.
