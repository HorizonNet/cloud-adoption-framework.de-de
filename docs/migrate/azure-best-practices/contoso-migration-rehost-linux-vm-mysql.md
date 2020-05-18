---
title: Zuweisen eines neuen Hosts für eine Linux-Service Desk-App zu Azure und Azure Database for MySQL
description: Dieser Artikel enthält Informationen zum Zuweisen eines neuen Hosts für eine lokale Linux-App durch Migration zu Azure-VMs und Azure Database for MySQL.
author: givenscj
ms.author: abuck
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 61398802202a33f9c514cf5a5b6a2528e7b662e4
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215992"
---
<!-- cSpell:ignore givenscj OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc contosoosticket osticket InnoDB binlog systemctl NSGs -->

# <a name="rehost-an-on-premises-linux-app-to-azure-vms-and-azure-database-for-mysql"></a>Zuweisen eines neuen Hosts für eine lokale Linux-App zu Azure-VMs und Azure Database for MySQL

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso einer LAMP-App (Linux-basiertes Apache/MySQL/PHP) auf zwei Ebenen einen neuen Host zuweist und sie mithilfe von Azure VMs und Azure Database for MySQL aus einer lokalen Umgebung zu Azure migriert.

osTicket, die in diesem Beispiel verwendete Service Desk-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/osTicket/osTicket) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team arbeitet eng mit Geschäftspartnern zusammen, um genau zu verstehen, was sie erreichen möchten:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und Infrastrukturen unter Druck.
- **Risikobegrenzung.** Die Service Desk-App ist entscheidend für das Geschäft. Contoso möchte sie ohne jedes Risiko nach Azure verlagern.
- **Erweitern.** Contoso möchte die App derzeit nicht ändern. Die App soll einfach nur stabil laufen.

## <a name="migration-goals"></a>Migrationsziele

Für die Bestimmung der besten Migrationsmethode hat das Contoso-Cloudteam Ziele für diese Migration festgelegt:

- Nach der Migration sollte die App in Azure die gleichen Leistungsmerkmale aufweisen wie die lokale VMware-Umgebung heute. Die App bleibt lokal und in der Cloud gleichermaßen wichtig.
- Contoso möchte nicht in diese App investieren. Die App ist wichtig für das Geschäft, in ihrer derzeitigen Form sie jedoch lediglich sicher in die Cloud verschoben werden.
- Nach Abschluss einer Reihe von Windows-App-Migrationen möchte Contoso mehr über die Verwendung einer Linux-basierten Infrastruktur in Azure erfahren.
- Contoso möchte die Administratoraufgaben für die Datenbank minimieren, nachdem die Anwendung in die Cloud verschoben wird.

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Szenario:

- Aktuell ist die App auf zwei VMs aufgeteilt (`OSTICKETWEB` und `OSTICKETMYSQL`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).
- Die App `OSTICKETWEB` auf zwei Anwendungsebenen soll zu einer Azure-IaaS-VM migriert werden.
- Die App-Datenbank wird zum Dienst Azure Database for MySQL PaaS migriert.
- Da Contoso eine Produktionsworkload migriert, werden sich die Ressourcen in der Ressourcengruppe `ContosoRG` für die Produktion befinden.
- Die `OSTICKETWEB`-Ressource wird in der primären Region (USA, Osten 2) repliziert und im Produktionsnetzwerk (`VNET-PROD-EUS2`) abgelegt:
  - Die Web-VM wird sich im Front-End-Subnetz (`PROD-FE-EUS2`) befinden.
- Die App-Datenbank wird mit dem [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) zu Azure Database for MySQL migriert.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

    ![Szenarioarchitektur](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

Zur Migration der Web-VM:

- In einem ersten Schritt richtet Contoso die Azure-Infrastruktur und die lokale Infrastruktur ein, die für die Bereitstellung von Azure Migrate erforderlich sind.
- Contoso verfügt bereits über die [Azure-Infrastruktur](./contoso-migration-infrastructure.md), sodass es nur noch die Replikation der virtuellen Computer über das Tool für die Azure Migrate-Servermigration hinzufügen und konfigurieren muss. Servermigration“ kommunizieren kann.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren des virtuellen Computers beginnen.
- Nachdem die Replikation aktiviert wurde und funktioniert, schließt Contoso den Umzug mithilfe von Azure Migrate ab.

Zur Migration der Datenbank:

1. Contoso stellt eine MySQL-Instanz in Azure bereit.
2. Contoso richtet den Azure Database Migration Service (DMS) ein und stellt so den Zugriff auf den lokalen Datenbankserver sicher.
3. Contoso migriert die Datenbank zu Azure Database for MySQL.

    ![Migrationsprozess](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | Contoso nutzt den Azure Migrate-Dienst, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | [Azure Migrate](https://azure.microsoft.com/pricing/details/azure-migrate) steht Ihnen ohne Zusatzgebühr zur Verfügung, jedoch können durch die Tools (Originalanbieter oder ISV), die Sie zur Bewertung und Migration verwenden, Gebühren anfallen.
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Der Azure Database Migration Service ermöglicht die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen bei minimaler Ausfallzeit. | Informieren Sie sich über die [unterstützten Regionen](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Die Datenbank basiert auf der Open Source-MySQL-Server-Engine. Sie stellt eine vollständig verwaltete, unternehmensgerechte MySQL Community-Datenbank für die Entwicklung und Bereitstellung von Apps bereit. | Erfahren Sie mehr über [Preise](https://azure.microsoft.com/pricing/details/mysql) und Skalierbarkeits-Optionen zu Azure Database for MySQL.

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes.

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. <br><br> Wenn Sie detailliertere Berechtigungen benötigen, lesen Sie [diesen Artikel](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Contoso – Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) beschrieben.
**Lokale Server** | Auf dem lokalen vCenter-Server sollte Version 5.5, 6.0, 6.5 oder 6.7 ausgeführt werden. <br><br> Ein ESXi-Host mit Version 5.5, 6.0, 6.5 oder 6.7. <br><br> Mindestens eine VMware-VM auf dem ESXi-Host.
**Lokale VMs** | [Überprüfen Sie Linux-Computer](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Die Contoso-Administratoren gehen bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten von Azure für die Azure Migrate- Servermigration.** Sie fügen das Tool für die Servermigration ihrem Azure Migrate-Projekt hinzu.
> - **Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration.** Sie bereiten Konten für die VM-Ermittlung sowie das Herstellen einer Verbindung mit Azure-VMs nach der Migration vor.
> - **Schritt 3: Replizieren von VMs.** Das Unternehmen richtet die Replikation ein und startet das Replizieren von VMs in Azure-Storage.
> - **Schritt 4: Migrieren der App-VM mit der Azure Migrate- Servermigration.** Es wird eine Testmigration durchgeführt, um sicherzustellen, dass alles funktioniert, und anschließend wird eine vollständige Migration ausgeführt, um die VMs in Azure zu verlagern.
> - **Schritt 5: Migrieren der Datenbank:** Die Migration wurde mithilfe des Azure Database Migration Service (DMS) eingerichtet.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 1: Vorbereiten von Azure für das Azure Migrate- Tool für die Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein VNET, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Azure Migrate: Das Tool für die Azure Migrate-Servermigration (OVA) wurde bereitgestellt und konfiguriert.

Das Unternehmen geht bei der Einrichtung dieser Komponenten wie folgt vor:

1. Einrichten eines Netzwerks – Contoso hat bereits ein Netzwerk eingerichtet, das verwendet werden kann für die Azure Migrate- Servermigration bei der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md).

2. Bereitstellen des Tools für die Azure Migrate- Servermigration“ kommunizieren kann.

    - Laden Sie das OVA-Image von Azure Migrate herunter, und importieren Sie es in VMware.

        ![Herunterladen der OVA-Datei](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    - Starten Sie das importierte Image, und konfigurieren Sie das Tool, einschließlich der folgenden Schritte:

      - Einrichten der erforderlichen Komponenten

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

      - Verweisen des Tools auf das Azure-Abonnement

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-register-azure.png)

      - Legen Sie die VMWare vCenter-Anmeldeinformationen fest.

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

      - Fügen Sie alle Linux-basierten Anmeldeinformationen für die Ermittlung hinzu.

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-credentials.png)

3. Nach der Konfiguration dauert es einige Zeit, bis das Tool alle virtuellen Computer auflistet. Nach Abschluss des Vorgangs sehen Sie, dass sie im Azure Migrate-Tool in Azure aufgefüllt werden.

**Benötigen Sie weitere Hilfe?**

[Informieren Sie sich](https://docs.microsoft.com/azure/migrate) zum Einrichten des Tools für die Azure Migrate- Servermigration“ kommunizieren kann.

## <a name="step-2-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration

Nach der Migration zu Azure möchte Contoso eine Verbindung mit den replizierten VMs in Azure herstellen können. Dazu müssen die Contoso-Administratoren einige Schritte durchführen:

- Für den Zugriff auf virtuelle Azure-Computer müssen sie vor der Migration auf dem lokalen Linux-Computer SSH aktivieren. Bei Ubuntu kann dieser Vorgang mithilfe des folgenden Befehls durchgeführt werden: `sudo apt-get ssh install -y`.

- Nach Durchführung der Migration können sie **Startdiagnose** aktivieren, um einen Screenshot des virtuellen Computers anzuzeigen.

- Falls dies nicht funktioniert, müssen sie überprüfen, ob der virtuelle Computer ausgeführt wird, und sollten folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) lesen.

- Installieren des [Azure Linux Agents](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux).

**Benötigen Sie weitere Hilfe?**

- [Informationen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) zum Vorbereiten von virtuellen Computern für die Migration.

## <a name="step-3-replicate-vm"></a>Schritt 3: Replikation der VM

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können sie mit der Replikation von App-VMs zu Azure beginnen.

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

## <a name="step-4-migrate-the-vm-with-azure-migrate-server-migration"></a>Schritt 4: Migrieren der VM mit der Azure Migrate- Servermigration

Die Contoso-Administratoren führen eine schnelle Testmigration und dann eine vollständige Migration aus, um die Web-VM zu verlagern.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** auf **Migrierte Server testen**.

     ![Testen der migrierten Server](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Klicken Sie mit der rechten Maustaste auf die zu testende VM, und klicken Sie anschließend auf **Testmigration**.

    ![Testmigration](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. Wählen Sie unter **Testmigration** das Azure VNET aus, in dem sich die Azure-VM nach der Migration befindet. Es empfiehlt sich, ein nicht für die Produktion bestimmtes VNET zu verwenden.
4. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
5. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
6. Klicken Sie nach Abschluss des Tests mit der rechten Maustaste unter **Aktuell replizierte Computer** auf die Azure-VM, und klicken Sie anschließend auf **Testmigration bereinigen**.

    ![Bereinigen der Migration](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vm"></a>Migrieren der VM

Die Contoso-Administratoren führen jetzt eine vollständige Migration aus, um die Verlagerung abzuschließen.

1. Klicken Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** auf **Server werden repliziert**.

    ![Replizieren der Server](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. Klicken Sie unter **Aktuell replizierte Computer** mit der rechten Maustaste auf die VM und dann auf **Migrieren**.
3. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. So wird sichergestellt, dass keine Daten verloren gehen.
    - Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
4. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
5. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

## <a name="step-5-provision-azure-database-for-mysql"></a>Schritt 5: Bereitstellen von Azure Database for MySQL

Die Administratoren von Contoso stellen eine MySQL-Datenbankinstanz in „USA, Osten 2“ bereit, der primären Region.

1. Im Azure-Portal erstellen die Verantwortlichen von Contoso eine Azure Database for MySQL-Ressource.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

2. Sie fügen den Namen **contosoosticket** für die Azure-Datenbank hinzu. Sie fügen die Datenbank zur Ressourcengruppe für die Produktion **ContosoRG** hinzu, und geben Anmeldeinformationen für sie an.
3. Die lokale MySQL-Datenbank ist in Version 5.7 vorhanden. Deshalb wählen sie diese Version für Kompatibilitätszwecke. Sie verwenden die Standardgrößen, die ihren Datenbankanforderungen entsprechen.

     ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

4. Bei den **Optionen für Sicherungsredundanz** entscheiden sie sich für die Verwendung von **Georedundanz**. Mit dieser Option können sie ihre Datenbank in der sekundären Region „USA Mitte“ wiederherstellen, wenn ein Ausfall auftritt. Sie können diese Option nur konfigurieren, wenn sie die Datenbank zur Verfügung stellen.

     ![Redundanz](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

5. Im Netzwerk **VNET-PROD-EUS2** > **Dienstendpunkte** fügen sie einen Dienstendpunkt (ein Datenbanksubnetz) für den SQL-Dienst hinzu.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

6. Nach dem Hinzufügen des Subnetzes erstellen sie eine VNET-Regel, die Zugriff vom Datenbanksubnetz im Produktionsnetzwerk zulässt.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-6-migrate-the-database"></a>Schritt 6: Migrieren der Datenbank

Es gibt mehrere Möglichkeiten, die MySQL-Datenbank zu verschieben. Für jede müssen Sie für das Ziel eine Azure DB for MySQL-Instanz erstellen. Nach der Erstellung können Sie die Migration auf zweierlei Weise durchführen:

- 6a: Azure Database Migration Service
- 6b: Sicherung und Wiederherstellung von MySQL Workbench

### <a name="step-6a-migrate-the-database-azure-database-migration-service"></a>Schritt 6a: Migrieren der Datenbank (Azure Database Migration Service)

Die Administratoren von Contoso migrieren die Datenbank mithilfe von Azure Database Migration Services anhand des [Schritt-für-Schritt-Tutorials für die Migration](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online). Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) von MySQL 5.6 oder 5.7 ausführen.

> [!NOTE]
> MySQL 8.0 wird in Azure Database for MySQL unterstützt, aber das DMS-Tool unterstützt diese Version noch nicht.

Zusammenfassend müssen Sie die folgenden Schritte ausführen:

- Sicherstellen, dass alle Voraussetzungen für die Migration erfüllt sind:

  - Die Version der MySQL-Serverquelle muss mit der Version übereinstimmen, die von Azure Database for MySQL unterstützt wird. Azure Database for MySQL unterstützt die MySQL Community Edition, die InnoDB-Engine und die Migration zwischen Quelle und Ziel derselben Version.
  - Aktivieren Sie die binäre Protokollierung in „my.ini“ (Windows) oder „my.cnf“ (Unix). Wenn Sie dies versäumen, tritt im Migrations-Assistenten ein `Error in binary logging. Variable binlog_row_image has value 'minimal'. Please change it to 'full. For more information, see https://go.microsoft.com/fwlink/?linkid=873009`-Fehler auf.
  - Der Benutzer muss über die `ReplicationAdmin`-Rolle verfügen.
  - Migrieren Sie die Datenbankschemas ohne Fremdschlüssel und Trigger.

- Erstellen Sie ein virtuelles Netzwerk, das über ExpressRoute oder VPN mit Ihrem lokalen Netzwerk verbunden ist.

- Erstellen Sie einen Azure Database Migration Service mit einer `Premium`-SKU, der mit dem VNet verbunden ist.

- Vergewissern Sie sich, dass der Azure Database Migration Service über das virtuelle Netzwerk auf die MySQL-Datenbank zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu MySQL auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem MySQL gehostet ist, zugelassen werden.

- Ausführen des Azure Database Migration Service-Tools:

  - Erstellen Sie ein Migrationsprojekt.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-new-project.png)

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-new-project-02.png)

  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-source.png)

  - Wählen Sie ein Ziel aus.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-target.png)

  - Wählen Sie die zu migrierende(n) Datenbank(en) aus.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-databases.png)

  - Konfigurieren Sie die erweiterten Einstellungen.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-settings.png)

  - Starten Sie die Replikation, und beheben Sie alle Fehler.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-monitor.png)

  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.
  
    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover.png)

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-complete.png)

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-complete-02.png)
  
  - Setzen Sie alle Fremdschlüssel und Trigger wieder ein.

  - Ändern Sie die Anwendungen so, dass sie die neue Datenbank verwenden.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-apps.png)

### <a name="step-6b-migrate-the-database-mysql-workbench"></a>Schritt 6b: Migrieren der Datenbank (MySQL Workbench)

Die Contoso-Administratoren migrieren die Datenbank mittels Sicherung und Wiederherstellung mit MySQL-Tools. Das Unternehmen installiert MySQL Workbench, speichert die Datenbank aus OSTICKETMYSQL und stellt sie dann wieder in der Azure Database for MySQL Server her.

### <a name="install-mysql-workbench"></a>Installieren von MySQL Workbench

1. Sie überprüfen die [Voraussetzungen und laden MySQL Workbench herunter](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).

2. Die Verantwortlichen bei Contoso installieren MySQL Workbench for Windows entsprechend den [Installationsanweisungen](https://dev.mysql.com/doc/workbench/en/wb-installing.html).

3. In MySQL Workbench erstellen sie eine MySQL-Verbindung mit OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

4. Sie exportieren die Datenbank als **Osticket** in eine lokale, eigenständige Datei.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

5. Nachdem die Datenbank lokal gesichert wurde, erstellen sie eine Verbindung mit der Azure Database for MySQL-Instanz.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

6. Nun können sie die Datenbank aus der eigenständigen Datei in die Azure Database for MySQL-Instanz importieren (wiederherstellen). Ein neues Schema (Osticket) wird für die Instanz erstellt.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

### <a name="connect-the-vm-to-the-database"></a>Verbinden der VM mit der Datenbank

Der letzte Schritt im Migrationsprozess besteht in der Aktualisierung der Verbindungszeichenfolge der Anwendung durch die Contoso-Administratoren, um auf die App-Datenbank zu verweisen, die auf dem virtuellen Computer **OSTICKETMYSQL** ausgeführt wird.

1. Das Unternehmen stellt über Putty oder einen anderen SSH-Client eine SSH-Verbindung mit der VM **OSTICKETWEB** her. Die VM ist privat, daher stellt Contoso eine Verbindung über die private IP-Adresse her.

    ![Herstellen einer Verbindung mit der Datenbank](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Herstellen einer Verbindung mit der Datenbank](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. Das Unternehmen muss sicherstellen, dass die VM **OSTICKETWEB** mit der VM **OSTICKETMYSQL** kommunizieren kann. Die Konfiguration ist mit der lokalen IP-Adresse 172.16.0.43 derzeit hartcodiert.

    **Vor dem Update:**

    ![Update-IP](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Nach dem Update:**

    ![Update-IP](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. Sie starten den Dienst mit `systemctl restart apache2` neu.

    ![Neu starten](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Schließlich aktualisiert Contoso die DNS-Datensätze für **OSTICKETWEB** und **OSTICKETMYSQL** auf einem der Contoso-Domänencontroller.

    ![DNS-Aktualisierung](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![DNS-Aktualisierung](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Benötigen Sie weitere Hilfe?**

- [Erfahren Sie mehr](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) zum Ausführen einer Testmigration.
- [Informationen](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) zur Migration von virtuellen Computern zu Azure.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die App jetzt ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und sichern.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration werden die Stufen der App „osTicket“ auf Azure-VMs ausgeführt.

Contoso muss nun wie folgt vorgehen:

- Das Unternehmen entfernt die VMware-VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation und zeigt neue Speicherorte und IP-Adressen an.
- Das Unternehmen überprüft sämtliche Ressourcen, die mit den lokalen VMs interagieren, und aktualisiert sämtliche relevanten Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.
- Contoso hat mithilfe des Azure Migrate-Diensts durch die Zuordnung von Abhängigkeiten die VM **OSTICKETWEB** für die Migration bewertet.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die VM und die Datenbank, um mögliche Sicherheitsprobleme zu ermitteln.

- Es überprüft die Netzwerksicherheitsgruppen (NSGs) für die VM zur Steuerung des Zugriffs. Mithilfe von NSGs wird sichergestellt, dass nur für die App zulässiger Datenverkehr übergeben werden kann.
- Das Sicherheitsteam erwägt darüber hinaus, die Daten auf den VM-Datenträgern mithilfe von Datenträgerverschlüsselung und Azure Key Vault zu schützen.
- Die Kommunikation zwischen der VM und der Datenbankinstanz ist nicht für SSL konfiguriert. Das Team muss dies tun, um sicherzustellen, dass der Datenbankverkehr nicht gehackt werden kann.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>BCDR

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- **Schützen von Daten.** Contoso sichert die Daten auf der App-VM mithilfe des Azure Backup-Diensts. [Weitere Informationen](https://docs.microsoft.com/azure/backup/backup-overview) Das Unternehmen muss die Sicherung für die Datenbank nicht konfigurieren. Azure Database for MySQL erstellt und speichert Serversicherungen automatisch. Es hat sich für die Georedundanz für die Datenbank entschieden, damit sie robust und einsatzbereit ist.

- **Sicherstellen eines unterbrechungsfreien Betriebs der Apps.** Contoso repliziert die App-VMs in Azure mithilfe von Site Recovery in einer sekundären Region. [Weitere Informationen](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nach der Bereitstellung von Ressourcen, weist Contoso Azure-Tags in Übereinstimmung mit Entscheidungen zu, die während der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md#set-up-tagging) gemacht wurden.
- Es gibt keine Lizenzierungsprobleme für die Contoso Ubuntu-Server.
- Contoso verwendet [Azure Cost Management](https://azure.microsoft.com/services/cost-management), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.
