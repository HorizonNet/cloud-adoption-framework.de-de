---
title: Zuweisen eines neuen Hosts für eine Anwendung auf virtuellen Computern mit Azure Migrate
description: Es wird beschrieben, wie Contoso den Azure Migrate-Dienst zum Durchführen einer Lift & Shift-Migration für lokale Computer zu Azure verwendet und für eine lokale App einen neuen Host zuweist.
author: givenscj
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1275997c3ca3e2da4947dff20e063e18cd907e9f
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879445"
---
<!-- cSpell:ignore WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc NSGs agentless -->

# <a name="rehost-an-on-premises-application-on-azure-vms-by-using-azure-migrate"></a>Zuweisen eines neuen Hosts für eine lokale Anwendung auf virtuellen Azure-Computern mit Azure Migrate

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso einer zweistufigen Windows .NET-Front-End-Anwendung, die auf virtuellen VMware-Computern (VMs) ausgeführt wird, einen neuen Host zuweist, indem es die virtuellen Anwendungscomputer zu virtuellen Azure-Computern migriert.

Die in diesem Beispiel verwendete Anwendung „SmartHotel360“ wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte. Sie wünschen Folgendes:

- **Unternehmenswachstum.** Da Contoso wächst, geraten die lokalen Systeme und die Infrastruktur des Unternehmens unter Druck.
- **Risikobegrenzung.** Die Anwendung „SmartHotel360“ ist für das Geschäft von Contoso äußerst wichtig. Das Unternehmen möchte die Anwendung ohne jedes Risiko nach Azure verschieben.
- **Erweitern.** Contoso möchte die Anwendung nicht ändern, aber es soll sichergestellt sein, dass sie stabil ist.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Diese Ziele werden verwendet, um die beste Migrationsmethode zu bestimmen:

- Nach der Migration soll die Anwendung in Azure die gleichen Leistungsmerkmale aufweisen wie gegenwärtig in der lokalen VMware-Umgebung. Die Anwendung ist in der Cloud ebenso wichtig wie lokal.
- Diese Anwendung ist zwar wichtig für Contoso, aber das Unternehmen möchte noch nicht in die Anwendung investieren. Contoso möchte die Anwendung in ihrer derzeitigen Form sicher in die Cloud verschieben.
- Contoso möchte das Betriebsmodell für diese Anwendung nicht ändern. Contoso möchte in der Cloud damit so interagieren, wie dies derzeit auch der Fall ist.
- Contoso möchte keine Anwendungsfunktionen ändern. Nur der Speicherort der Anwendung ändert sich.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen festgelegt wurden, entwirft und prüft Contoso eine Bereitstellungslösung. Contoso ermittelt den Migrationsprozess, und zwar einschließlich der Azure-Dienste, die für die Migration verwendet werden.

### <a name="current-application"></a>Aktuelle Anwendung

- Die Anwendung ist auf zwei virtuelle Computer aufgeteilt (`WEBVM` und `SQLVM`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von vCenter Server 6.5 (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Da es sich bei der Anwendung um eine Produktionsworkload handelt, befinden sich die virtuellen Anwendungscomputer in Azure in der Produktionsressourcengruppe `ContosoRG`.
- Die virtuellen Anwendungscomputer werden zur primären Azure-Region (USA, Osten 2) migriert und im Produktionsnetzwerk (`VNET-PROD-EUS2`) platziert.
- Der virtuelle Front-End-Computer wird im Front-End-Subnetz (`PROD-FE-EUS2`) des Produktionsnetzwerks platziert.
- Der virtuelle Datenbankcomputer wird im Datenbanksubnetz (`PROD-DB-EUS2`) des Produktionsnetzwerks platziert.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Diagramm: Szenarioarchitektur](./media/contoso-migration-rehost-vm/architecture.png)

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Server durchgeführt. Hierbei haben die folgenden Überlegungen dem Unternehmen dabei geholfen, sich für einen virtuellen Azure-IaaS-Computer zu entscheiden, auf dem SQL Server ausgeführt wird:

- Die Verwendung eines virtuellen Azure-Computers mit SQL Server erscheint als optimale Lösung, wenn Contoso das Betriebssystem und die Datenbank anpassen muss oder Partneranwendungen auf demselben virtuellen Computer installiert und ausgeführt werden sollen.
- Dank Software Assurance kann Contoso vorhandene Lizenzen später über den Azure-Hybridvorteil für SQL Server gegen Azure SQL Managed Instance zu ermäßigten Preisen austauschen. Dadurch kann das Unternehmen bei SQL Managed Instance bis zu 30 Prozent sparen.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Beide virtuellen Anwendungscomputer werden unverändert in Azure verschoben, was die Migration vereinfacht. <br><br> Da Contoso beide virtuellen Anwendungscomputer per Lift & Shift-Vorgang migriert, sind für die Anwendungsdatenbank keine besonderen Konfigurations- oder Migrationstools erforderlich. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil nutzen. <br><br> Contoso behält die vollständige Kontrolle über die Anwendungs-VMs in Azure. |
| **Nachteile** | Auf `WEBVM` und `SQLVM` wird Windows Server 2008 R2 ausgeführt. Azure unterstützt das Betriebssystem für bestimmte Rollen. [Weitere Informationen](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines) <br><br> Die Web- und die Datenschicht der Anwendung bleiben Single Points of Failure. <br><br> `SQLVM` wird unter SQL Server 2008 R2 ausgeführt. Für SQL Server 2008 R2 wird kein Mainstream-Support mehr geleistet, aber die Unterstützung für Azure-VMs ist vorhanden. [Weitere Informationen](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support) <br><br> Contoso muss die Anwendung weiterhin auf virtuellen Azure-Computern unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service oder Azure SQL-Datenbank umzustellen. |

### <a name="migration-process"></a>Migrationsprozess

Contoso migriert das Anwendungs-Front-End und die Datenbank-VMs zu virtuellen Azure-Computern, indem das Unternehmen in Azure Migrate die Methode ohne Agent verwendet: Servermigration“ kommunizieren kann.

- Als ersten Schritt bereitet Contoso die Azure-Komponenten für die Azure Migrate- Servermigration vor und richtet sie ein. Anschließend bereitet es die lokale VMware-Infrastruktur vor.
- Die [Azure-Infrastruktur](./contoso-migration-infrastructure.md) ist bereits vorhanden, sodass es nur noch die Replikation der virtuellen Computer über das „Tool für die Azure Migrate- Servermigration“ kommunizieren kann.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der virtuellen Computer beginnen.
- Wenn die Replikation aktiviert wurde und funktioniert, migriert Contoso den virtuellen Computer, indem die Migration getestet und im Erfolgsfall ein Failover zu Azure durchgeführt wird.

![Diagramm: Schritte des Migrationsprozesses](./media/contoso-migration-rehost-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Migrate: Servermigration](/azure/migrate/contoso-migration-rehost-vm) | Der Dienst orchestriert und verwaltet die Migration von lokalen Anwendungen und Workloads sowie von VM-Instanzen für Amazon Web Services (AWS) und Google Cloud Platform (GCP). | Während der Replikation in Azure fallen Gebühren für Azure Storage an. Azure-VMs werden erstellt und verursachen Gebühren, wenn die Migration erfolgt und die VMs in Azure ausgeführt werden. Informieren Sie sich über die [Gebühren und Preise](https://azure.microsoft.com/pricing/details/azure-migrate).  |

## <a name="prerequisites"></a>Voraussetzungen

Contoso und andere Benutzer müssen für dieses Szenario die unten angegebenen Voraussetzungen erfüllen.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat in einem früheren Artikel dieser Reihe Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden, aber nicht der Administrator sind, sollten Sie den Administrator bitten, Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuzuweisen. <br><br> Falls Sie präzisere Berechtigungen benötigen, helfen Ihnen die Informationen unter [Verwalten des Site Recovery-Zugriffs mit rollenbasierter Zugriffssteuerung von Azure](/azure/site-recovery/site-recovery-role-based-linked-access-control) weiter. |
| **Azure-Infrastruktur** | Informieren Sie sich, wie Contoso eine [Azure-Infrastruktur einrichtet](./contoso-migration-infrastructure.md). <br><br> Erfahren Sie mehr über bestimmte [Voraussetzungen](./contoso-migration-devtest-to-iaas.md#prerequisites) für Azure Migrate: Servermigration. |
| **Lokale Server** | Auf lokalen vCenter-Servern sollte Version 5.5, 6.0, 6.5 oder 6.7 ausgeführt werden. <br><br> ESXi-Hosts sollten Version 5.5, 6.0, 6.5 oder 6.7 ausführen. <br><br> Mindestens eine VMware-VM sollte auf dem ESXi-Host ausgeführt werden. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso-Administratoren gehen bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten von Azure für die Azure Migrate- Servermigration.** Sie fügen das Tool für die Servermigration ihrem Azure Migrate-Projekt hinzu.
> - **Schritt 2: Replizieren von lokalen VMs.** Das Unternehmen richtet die Replikation ein und startet das Replizieren von VMs in Azure Storage.
> - **Schritt 3: Migrieren der VMs mit der Azure Migrate- Servermigration.** Es wird eine Testmigration durchgeführt, um sicherzustellen, dass alles funktioniert, und anschließend wird eine vollständige Migration ausgeführt, um die VMs in Azure zu verlagern.

## <a name="step-1-prepare-azure-for-azure-migrate-server-migration"></a>Schritt 1: Vorbereiten von Azure für die Azure Migrate- Servermigration

Zum Migrieren der VMs zu Azure benötigt Contoso ein virtuelles Netzwerk, in dem Azure-VMs angeordnet werden, wenn sie während der Migration erstellt werden. Darüber hinaus muss das Tool für die Azure Migrate-Servermigration (OVA-Datei) bereitgestellt und konfiguriert werden.

1. Einrichten eines Netzwerks. Contoso hat bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann, als die [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) durchgeführt wurde.

    - Bei der Anwendung „SmartHotel360“ handelt es sich um eine Produktionsanwendung, und die virtuellen Computer werden zum Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) migriert.
    - Beide virtuellen Computer werden in der für Produktionsressourcen verwendeten Ressourcengruppe `ContosoRG` bereitgestellt.
    - Der virtuelle Computer für das Anwendungs-Front-End (`WEBVM`) wird zum Front-End-Subnetz (`PROD-FE-EUS2`) im Produktionsnetzwerk migriert.
    - Der virtuelle Computer für die Anwendungsdatenbank (`SQLVM`) wird zum Datenbanksubnetz (`PROD-DB-EUS2`) im Produktionsnetzwerk migriert.

1. Bereitstellen des Tools für die Azure Migrate- Servermigration“ kommunizieren kann.

    1. Laden Sie das OVA-Image von Azure Migrate herunter, und importieren Sie es in VMware.

       ![Screenshot: Schaltfläche „Herunterladen“ für die OVA-Datei](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    1. Starten Sie das importierte Image, und konfigurieren Sie das Tool, einschließlich der folgenden Schritte:

       - Einrichten der erforderlichen Komponenten

         ![Screenshot: Bereich für die Einrichtung von erforderlichen Lizenzbedingungen](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

       - Stellen Sie die Verweise des Tools auf das Azure-Abonnement ein.

         ![Screenshot: Auswahl für die Registrierung bei Azure Migrate](./media/contoso-migration-rehost-vm/migration-register-azure.png)

       - Legen Sie die VMware vCenter-Anmeldeinformationen fest.

         ![Screenshot: Auswahl zum Angeben einer vCenter Server-Instanz](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

       - Fügen Sie alle Windows-basierten Anmeldeinformationen für die Ermittlung hinzu.

         ![Screenshot: Bereich für die Ermittlung von Anwendungen und Abhängigkeiten auf virtuellen Computern](./media/contoso-migration-rehost-vm/migration-credentials.png)

Wenn Sie die Konfiguration abgeschlossen haben, wird das Tool einige Zeit benötigen, um eine Enumeration aller VMs durchzuführen. Nach Abschluss dieses Vorgangs sehen Sie, dass sie im Azure Migrate-Tool in Azure aufgefüllt werden.

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über die Einrichtung der [Azure Migrate: Servermigration](/azure/migrate/migrate-services-overview#azure-migrate-server-migration-tool).

### <a name="prepare-on-premises-vms"></a>Vorbereiten von lokalen VMs

Nach der Migration möchte Contoso eine Verbindung mit den Azure VMs herstellen und Azure die Erlaubnis zum Verwalten der VMs geben. Die Contoso-Administratoren müssen vor der Migration die folgenden Schritte ausführen:

1. Für Zugriff über das Internet:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Sicherstellen, dass TCP- und UDP-Regeln zum **öffentlichen** Profil hinzugefügt wurden.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.

2. Für Zugriff per Site-to-Site-VPN:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.
    - Legen Sie für Windows die SAN-Richtlinie des Betriebssystems auf dem lokalen virtuellen Computer auf **OnlineAll** fest.

3. Installieren Sie den [Azure Windows-Agent](/azure/virtual-machines/extensions/agent-windows).

Weitere Überlegungen:

- Unter Windows sollten auf dem virtuellen Computer keine ausstehenden Windows-Updates vorhanden sein, wenn Sie eine Migration auslösen. Wenn welche vorhanden sind, können sich die Administratoren nicht bei der VM anmelden, bis die Updates abgeschlossen sind.
- Nach der Migration können die Administratoren **Startdiagnose** aktivieren, um einen Screenshot der VM anzuzeigen. Falls dies nicht funktioniert, sollte überprüft werden, ob die VM ausgeführt wird, und die [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) gelesen werden.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie [VMs auf die Migration vorbereiten](/azure/migrate/prepare-for-migration).

## <a name="step-2-replicate-the-on-premises-vms"></a>Schritt 2: Replizieren der lokalen VMs

Bevor die Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können sie mit der Replikation von VMware-VMs in Azure beginnen.

1. Wechseln Sie im Azure Migrate-Projekt zu **Server** > **Azure Migrate- Servermigration**). Wählen Sie dann **Replizieren** aus.

    ![Screenshot: Auswahlmöglichkeiten für die Replikation virtueller Computer](./media/contoso-migration-rehost-vm/select-replicate.png)

2. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere** aus.

3. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance, die Sie eingerichtet haben, und dann **OK** aus.

    ![Screenshot: „Quelleinstellungen“](./media/contoso-migration-rehost-vm/source-settings.png)

4. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten.
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium oder Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie hierzu unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung durchgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Screenshot: Feld für die Auswahl von virtuellen Computern für die Migration](./media/contoso-migration-rehost-vm/select-assessment.png)

5. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und aktivieren Sie alle VMs, die Sie migrieren möchten. Wählen Sie anschließend **Next: Zieleinstellungen**.

6. Wählen Sie in **Zieleinstellungen** das Abonnement und die Zielregion aus, zu der Sie migrieren. Geben Sie dann die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden werden. Wählen Sie unter **Virtuelles Netzwerk** das virtuelle Azure-Netzwerk oder -Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

7. Wählen Sie unter **Azure-Hybridvorteil**

    - die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Wählen Sie **Weiter** aus.
    - Wählen Sie **Ja** aus, wenn Sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Wählen Sie **Weiter** aus.

8. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste für die VM-Größe die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der größten Übereinstimmung im Azure-Abonnement aus. Alternativ können Sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

9. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen, und wählen Sie in Azure den Datenträgertyp aus (SSD Standard/HDD Standard oder Managed Disks Premium). Wählen Sie **Weiter** aus.

   Sie können Datenträger von der Replikation ausschließen. Wenn Sie Datenträger ausschließen, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

10. Überprüfen Sie unter **Replikation prüfen und starten** die Einstellungen, und wählen Sie anschließend **Replizieren** aus, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-3-migrate-the-vms-with-azure-migrate-server-migration"></a>Schritt 3: Migrieren der VMs mit der Azure Migrate- Servermigration

Die Contoso-Administratoren führen eine schnelle Testmigration und dann eine vollständige Migration durch, um die VMs zu migrieren.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** die Option **Migrierte Server testen** aus.

    ![Screenshot: Schaltfläche zum Starten eines Tests von migrierten Servern](./media/contoso-migration-rehost-vm/test-migrated-servers.png)

2. Wählen und halten Sie (oder klicken Sie mit der rechten Maustaste auf) die zu testende VM, und wählen Sie anschließend **Testmigration** aus.

    ![Screenshot: Ausgewählter virtueller Computer und Schaltfläche zum Starten des Migrationstests](./media/contoso-migration-rehost-vm/test-migrate.png)

3. Wählen Sie unter **Testmigration** das virtuelle Azure-Netzwerk aus, in dem sich der virtuelle Azure-Computer nach der Migration befindet. Es empfiehlt sich, ein nicht für die Produktion bestimmtes virtuelles Netzwerk zu verwenden.
4. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
5. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
6. Wählen und halten Sie nach Abschluss des Tests unter **Aktuell replizierte Computer** die Azure-VM (oder klicken mit der rechten Maustaste darauf), und wählen Sie anschließend **Testmigration bereinigen** aus.

    ![Screenshot: Auswahl für die Bereinigung der Migration](./media/contoso-migration-rehost-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrieren der VMs

Die Contoso-Administratoren führen jetzt eine vollständige Migration durch.

1. Wählen Sie im Azure Migrate-Projekt die Optionen **Server** > **Azure Migrate- Servermigration** > **Server werden repliziert** aus.

    ![Screenshot: Auswahl für die Replikation von Servern](./media/contoso-migration-rehost-vm/replicating-servers.png)

2. Wählen und halten Sie unter **Aktuell replizierte Computer** die VM (oder klicken Sie mit der rechten Maustaste darauf), und wählen Sie dann **Migrieren** aus.
3. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.

    Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. So wird sichergestellt, dass keine Daten verloren gehen. Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
4. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
5. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über das [Ausführen einer Testmigration](/azure/migrate/tutorial-migrate-vmware#run-a-test-migration).
- Informieren Sie sich über das [Migrieren von virtuellen Computern zu Azure](/azure/migrate/tutorial-migrate-vmware#migrate-vms).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration werden die Logikschichten von „SmartHotel360“ auf virtuellen Azure-Computern ausgeführt.

Contoso muss jetzt die folgenden Bereinigungsschritte ausführen:

- Beenden der Replikation nach Abschluss der Migration
- Entfernen des Computers `WEBVM` aus dem vCenter-Bestand
- Entfernen des Computers `SQLVM` aus dem vCenter-Bestand
- Entfernen von `WEBVM` und `SQLVM` aus lokalen Sicherungsaufträgen
- Aktualisieren der internen Dokumentation zum Anzeigen des neuen Speicherorts und der IP-Adressen für die VMs
- Überprüfen sämtlicher Ressourcen, die mit den VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die Anwendung nun ausgeführt wird, muss Contoso sie in Azure vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs auf eventuell vorhandene Sicherheitsprobleme. Zur Steuerung des Zugriffs überprüft das Team die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer. Mithilfe von Netzwerksicherheitsgruppen wird sichergestellt, dass nur für die Anwendung zulässiger Datenverkehr diese erreichen kann. Das Team zieht darüber hinaus in Betracht, die Daten per Azure Disk Encryption und Key Vault auf dem Datenträger zu schützen.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- Schützen von Daten: Contoso [sichert die Daten auf den VMs mithilfe von Azure Backup](/azure/backup/backup-overview).
- Aufrechterhalten des Anwendungsbetriebs: Contoso [repliziert die virtuellen Anwendungscomputer in Azure mit Azure Site Recovery in einer sekundären Region](/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

Contoso verfügt über eine vorhandene Lizenzierung für seine VMs und nutzt den Azure-Hybridvorteil. Contoso wird die vorhandenen virtuellen Azure-Computer konvertieren, um von diesen Preisen zu profitieren.

Contoso aktiviert [Azure Cost Management und das Azure-Abrechnungsportal](/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung von Azure-Ressourcen zu unterstützen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde von Contoso für die Anwendung SmartHotel360 ein neuer Host in Azure zugewiesen. Die Administratoren migrierten die Anwendungs-VMs mithilfe des „Tools zur Azure- Servermigration“ kommunizieren kann.
Eine Anleitung zum Abschließen eines ähnlichen Projekts in Ihrer Umgebung finden Sie in der Azure DevOps-Projektvorlage für ein [Servermigrationsprojekt](https://azuredevopsdemogenerator.azurewebsites.net/?name=servermigration). 
