---
title: Zuweisen eines neuen Hosts für eine lokale Dev/Test-Umgebung auf virtuellen Azure-Computern über Azure Migrate
description: Hier erfahren Sie, wie Contoso einer lokalen Dev/Test-Umgebung mithilfe des Azure Migrate-Diensts mit einer Lift & Shift-Migration von lokalen Computern zu Azure einen neuen Host zuweist.
author: deltadan
ms.author: abuck
ms.date: 07/1/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: d0b92f1c27fdb2ac4e2867ad21b382ee89915a4a
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86234173"
---
<!-- docsTest:ignore SmartHotel360 -->
<!-- cSpell:ignore vcenter contosohost contosodc NSGs agentless osTicket WEBVMDEV SQLVMDEV OSTICKETWEBDEV OSTICKETMYSQLDEV -->

# <a name="rehost-an-on-premises-devtest-environment-on-azure-virtual-machines-via-azure-migrate"></a>Zuweisen eines neuen Hosts für eine lokale Dev/Test-Umgebung auf virtuellen Azure-Computern über Azure Migrate

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso seiner Dev/Test-Umgebung für zwei Anwendungen, die auf virtuellen VMware-Computern (VMs) ausgeführt werden, durch die Migration zu virtuellen Azure-Computern einen neuen Host zuweist.

Die in diesem Beispiel genutzten Anwendungen [SmartHotel360](https://github.com/Microsoft/SmartHotel360) und [osTicket](https://github.com/osTicket/osTicket) sind Open Source. Sie können sie für eigene Testzwecke herunterladen.

## <a name="migration-options"></a>Migrationsoptionen

Bei der Verlagerung von Entwicklungs-/Testumgebungen in Azure stehen Contoso mehrere Optionen zur Verfügung.

| Migrationsoptionen | Ergebnis |
| --- | --- |
| [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | [Bewerten](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) und [Migrieren](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware) lokaler VMs <br><br> Ausführen von Dev/Test-Servern mithilfe von Azure IaaS <br><br> Verwalten von VMs mit [Azure Resource Manager](https://azure.microsoft.com/features/resource-manager) |
| [Azure DevTest Labs](https://docs.microsoft.com/azure/devtest-labs/devtest-lab-overview) | Schnelles Bereitstellen von Entwicklungs- und Testumgebungen <br><br> Minimieren von Verlusten durch Kontingente und Richtlinien <br><br> Festlegen von automatisiertem Herunterfahren zum Minimieren von Kosten <br><br> Erstellen von Windows- und Linux-Umgebungen |

> [!NOTE]
> Erfahren Sie, wie Contoso seine [Dev/Test-Umgebung mithilfe von DevTest Labs in Azure](./contoso-migration-devtest-to-labs.md) verlagert hat.

## <a name="business-drivers"></a>Business-Treiber

Das Führungsteam für die Entwicklung hat festgelegt, was mit dieser Migration erreicht werden soll. Das Ziel ist es, Dev/Test-Funktionen schnell aus dem lokalen Rechenzentrum auszulagern und keine Hardware für die Entwicklung von Software mehr zu kaufen. Außerdem sollen Entwickler in der Lage sein, ihre Umgebungen ohne Beteiligung der IT-Abteilung zu erstellen und auszuführen.

> [!NOTE]
> Contoso nutzt dabei das [Abonnementangebot „Dev/Test Pay-As-You-Go“](https://azure.microsoft.com/offers/ms-azr-0023p) für seine Umgebungen. Jeder aktive Visual Studio-Abonnent im Team kann die Microsoft-Software, die im Abonnement der virtuellen Computer enthalten ist, ohne zusätzliche Kosten für Dev/Test verwenden. Contoso zahlt lediglich die Linux-Rate für ausgeführte VMs. Dies gilt auch für VMs mit SQL Server, SharePoint Server oder anderer Software, die normalerweise zu einem höheren Preis in Rechnung gestellt wird.

## <a name="migration-goals"></a>Migrationsziele

Das Entwicklungsteam von Contoso hat sich Ziele für diese Migration gesetzt. Diese Ziele werden verwendet, um die beste Migrationsmethode zu bestimmen:

- Contoso möchte seine lokalen Dev/Test-Umgebungen schnell auslagern.
- Nach der Migration sollte Contosos Dev/Test-Umgebung in Azure über erweiterte Funktionen gegenüber dem aktuellen System in VMware verfügen.
- Das Betriebsmodell wechselt von der Bereitstellung durch die IT-Abteilung zu DevOps und Self-Service-Bereitstellung.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-application"></a>Aktuelle Anwendung

- Die Dev/Test-VMs für die beiden Anwendungen werden auf VMs ausgeführt (`WEBVMDEV`, `SQLVMDEV`, `OSTICKETWEBDEV`, `OSTICKETMYSQLDEV`). Diese VMs werden für die Entwicklung verwendet, bevor Code auf die Produktions-VMs hochgestuft wird.
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Da die VMs für Dev/Test verwendet werden, befinden sie sich in der Ressourcengruppe `ContosoDevRG` in Azure.
- Die VMs werden in die primäre Azure-Region (`East US 2`) migriert und im virtuellen Entwicklungsnetzwerk (`VNET-DEV-EUS2`) platziert.
- Die Web-Front-End-VMs werden im Front-End-Subnetz (`DEV-FE-EUS2`) im Entwicklungsnetzwerk platziert.
- Die Datenbank-VM wird im Datenbanksubnetz (`DEV-DB-EUS2`) im Entwicklungsnetzwerk platziert.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

  ![Szenarioarchitektur](./media/contoso-migration-devtest-to-iaas/architecture.png)
  _Abbildung 1: Vorgeschlagene Architektur_

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Zur Unterstützung der laufenden Entwicklung hat sich Contoso für die fortgesetzte Verwendung vorhandener VMs und deren Migration zu Azure entschieden. Zukünftig hat Contoso die Verwendung von PaaS-Diensten wie [Azure SQL-Datenbank](https://docs.microsoft.com/azure/azure-sql/azure-sql-iaas-vs-paas-what-is-overview) und [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) zum Ziel.

- Datenbank-VMs werden im aktuellen Zustand ohne Änderungen migriert.
- Durch die Verwendung des Azure Dev/Test-Abonnementangebots fallen für die Windows- und SQL-Server keine Lizenzgebühren an, sodass die Computekosten minimal bleiben.
- Zukünftig möchte Contoso die Entwicklung in PaaS-Dienste integrieren.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Alle Entwicklungs-VMs werden ohne Änderungen nach Azure verlagert, was die Migration vereinfacht. <br><br> Da Contoso beide Gruppen von VMs mithilfe eines Lift & Shift-Ansatzes migriert, sind für die Anwendungsdatenbank keine besonderen Konfigurations- oder Migrationstools erforderlich. <br><br> Contoso kann seine Investition in das Azure Dev/Test-Abonnement nutzen, um Lizenzgebühren zu sparen. <br><br> Contoso behält die vollständige Kontrolle über die Anwendungs-VMs in Azure. <br><br> Entwickler erhalten Berechtigungen für das Abonnement, wodurch sie neue Ressourcen erstellen können, ohne darauf warten zu müssen, dass die IT-Abteilung auf ihre Anforderungen reagiert. |
| **Nachteile** | Bei der Migration werden nur die VMs verschoben, und es erfolgt noch kein Wechsel zu PaaS-Dienste für die Entwicklung. Das bedeutet, dass Contoso den Betrieb seiner VMs selbst unterstützen muss, einschließlich Sicherheitspatches. Dies wurde bisher von der IT-Abteilung erledigt, sodass eine Lösung für diese neue operative Aufgabe gefunden werden muss. <br><br> Die cloudbasierte Lösung bietet den Entwicklern mehr Möglichkeiten und umfasst keine Sicherheitsvorkehrungen für eine Überbereitstellung von Systemen. Entwickler können ihre Systeme sofort bereitstellen, dabei jedoch Ressourcen erstellen, die Geld kosten, aber nicht im Budget enthalten sind. |

> [!NOTE]
> Contoso kann die Nachteile in der Liste mithilfe von [DevTest Labs](https://docs.microsoft.com/azure/devtest-labs/devtest-lab-overview) beheben.

### <a name="migration-process"></a>Migrationsprozess

Contoso migriert das Entwicklungs-Front-End und die Datenbank zu Azure-VMs und verwendet dazu die  Methode ohne Agent des Tools für die Azure Migrate-Servermigration.

- Als ersten Schritt bereitet Contoso die Azure-Komponenten für die Azure Migrate- Servermigration vor und richtet sie ein. Anschließend bereitet es die lokale VMware-Infrastruktur vor.
- Contoso verfügt bereits über die [Azure-Infrastruktur](./contoso-migration-infrastructure.md), sodass es nur noch die Replikation der virtuellen Computer über das Tool für die Azure Migrate- Servermigration konfigurieren muss.
- Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der virtuellen Computer beginnen.
- Wenn die Replikation aktiviert wurde und funktioniert, migriert Contoso die virtuellen Computer durch Testen der Migration und im Erfolgsfall anschließendes Failover zu Azure.
- Sobald die Entwicklungs-VMs in Azure ausgeführt werden, folgt eine Neukonfiguration der Entwicklungsarbeitsstationen, damit sie auf die VMs verweisen, die jetzt in Azure ausgeführt werden.

  ![Migrationsprozess](./media/contoso-migration-devtest-to-iaas/migration-process-az-migrate.png)
  _Abbildung 2: Übersicht über den Migrationsprozess_

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Migrate: Servermigration](https://docs.microsoft.com/azure/migrate) | Der Dienst orchestriert und verwaltet die Migration lokaler Anwendungen und Workloads sowie von AWS- oder GCP-VM-Instanzen. | Während der Replikation in Azure fallen Gebühren für Azure Storage an. Azure-VMs werden erstellt und verursachen Gebühren, wenn die Migration erfolgt und die VMs in Azure ausgeführt werden. [Weitere Informationen](https://azure.microsoft.com/pricing/details/azure-migrate) zu Gebühren und Preisen. |

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes:

| Anforderungen | Details |
| --- | --- |
| **Azure Dev/Test-Abonnement** | Contoso erstellt ein [Azure Dev/Test-Abonnement](https://azure.microsoft.com/offers/ms-azr-0023p), um von den Vorteilen einer Kostenreduzierung von bis zu 80 Prozent zu profitieren. <br><br> Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden, aber nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. <br><br> Falls Sie präzisere Berechtigungen benötigen, helfen Ihnen die Informationen unter [Verwalten des Site Recovery-Zugriffs mit rollenbasierter Zugriffssteuerung (Role-Based Access Control, RBAC)](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control) weiter. |
| **Azure-Infrastruktur** | Informieren Sie sich, wie Contoso eine [Azure-Infrastruktur einrichtet](./contoso-migration-infrastructure.md). <br><br> Erfahren Sie mehr über bestimmte [Voraussetzungen](#prerequisites) für Azure Migrate: Servermigration. |
| **Lokale Server** | Auf lokalen vCenter-Servern sollte Version 5.5, 6.0, 6.5 oder 6.7 ausgeführt werden. <br><br> ESXi-Hosts sollten Version 5.5, 6.0, 6.5 oder 6.7 ausführen. <br><br> Mindestens eine VMware-VM sollte auf dem ESXi-Host ausgeführt werden. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso-Administratoren gehen bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten von Azure für die Azure Migrate- Servermigration.** Sie fügen das Tool für die Servermigration ihrem Azure Migrate-Projekt hinzu.
> - **Schritt 2: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration.** Sie bereiten Konten für die VM-Ermittlung sowie das Herstellen einer Verbindung mit Azure-VMs nach der Migration vor.
> - **Schritt 3: Replizieren von VMs.** Das Unternehmen richtet die Replikation ein und startet das Replizieren von VMs in Azure Storage.
> - **Schritt 4: Migrieren der VMs mit der Azure Migrate- Servermigration.** Es wird eine Testmigration durchgeführt, um sicherzustellen, dass alles funktioniert, und anschließend wird eine vollständige Migration ausgeführt, um die VMs in Azure zu verlagern.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 1: Vorbereiten von Azure für das Azure Migrate- Tool für die Servermigration

Contoso muss die VMs zu einem virtuellen Netzwerk (VNET) migrieren, in dem sich die Azure-VMs befinden, wenn sie während der Migration mit dem Tool für die Azure Migrate- Servermigration erstellt, bereitgestellt und konfiguriert werden.

Das Unternehmen geht bei der Einrichtung wie folgt vor:

1. Einrichten eines Netzwerks: Contoso hat bereits ein Netzwerk eingerichtet, das verwendet werden kann für die Azure Migrate- Servermigration bei der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md).

    - Die zu migrierenden VMs werden für die Entwicklung verwendet. Sie werden zum virtuellen Azure-Entwicklungsnetzwerk (`VNET-DEV-EUS2`) in der primären Region „USA, Osten 2“ migriert.
    - Beide VMs werden in der Ressourcengruppe `ContosoDevRG` bereitgestellt, die für Entwicklungsressourcen verwendet wird.
    - Die Front-End-VMs der Anwendung (`WEBVMDEV` und `OSTICKETWEBDEV`) werden zum Front-End-Subnetz (`DEV-FE-EUS2`) im virtuellen Entwicklungsnetzwerk migriert.
    - Die Anwendungsdatenbank-VM (`SQLVMDEV` und `OSTICKETMYSQLDEV`) wird zum Datenbanksubnetz (`DEV-DB-EUS2`) im virtuellen Entwicklungsnetzwerk migriert.

2. Bereitstellen des Tools für die Azure Migrate- Servermigration.

    - Laden Sie das OVA-Image von Azure Migrate herunter, und importieren Sie es in VMware.

      ![Herunterladen der OVA-Datei](./media/contoso-migration-devtest-to-iaas/migration-download-ova.png)
      _Abbildung 3: Herunterladen der OVA-Datei_

    - Starten Sie das importierte Image, und konfigurieren Sie das Tool, einschließlich der folgenden Schritte:

      - Einrichten der erforderlichen Komponenten

        ![Konfigurieren des Tools](./media/contoso-migration-devtest-to-iaas/migration-setup-prerequisites.png)
        _Abbildung 4: Einrichten der erforderlichen Komponenten_

      - Verweisen des Tools auf das Azure-Abonnement

        ![Konfigurieren des Tools](./media/contoso-migration-devtest-to-iaas/migration-register-azure.png)
        _Abbildung 5: Das Azure-Abonnement_

      - Festlegen der VMware vCenter-Anmeldeinformationen

        ![Konfigurieren des Tools](./media/contoso-migration-devtest-to-iaas/migration-vcenter-server.png)
        _Abbildung 6: Festlegen der VMware vCenter-Anmeldeinformationen_

      - Hinzufügen aller Windows-basierten Anmeldeinformationen für die Ermittlung

        ![Konfigurieren des Tools](./media/contoso-migration-devtest-to-iaas/migration-credentials.png)
        _Abbildung 7: Hinzufügen der Windows-basierten Anmeldeinformationen für die Ermittlung_

3. Nach der Konfiguration dauert es einige Zeit, bis das Tool alle VMs auflistet. Nach Abschluss dieses Vorgangs sehen Sie, dass sie im Azure Migrate-Tool in Azure aufgefüllt werden.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie das [Tool für die Azure Migrate- Servermigration einrichten](https://docs.microsoft.com/azure/migrate).

### <a name="prepare-on-premises-vms"></a>Vorbereiten von lokalen VMs

Nach der Migration möchte Contoso eine Verbindung mit den Azure VMs herstellen und Azure die Erlaubnis zum Verwalten der VMs geben. Dazu führen Contoso-Administratoren vor der Migration folgende Schritte aus:

1. Für den Zugriff über das Internet:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Stellen Sie sicher, dass TCP- und UDP-Regeln zum `Public`-Profil hinzugefügt wurden.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.
    - Installieren Sie SSH mit dem folgenden Befehl: `sudo apt-get ssh install -y`.

2. Für den Zugriff über Site-to-Site-VPN:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.
    - Legen Sie für Windows die SAN-Richtlinie des Betriebssystems auf der lokalen VM auf `OnlineAll` fest.

3. Installieren Sie den [Azure Windows-Agent](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-windows) und den [Azure Linux-Agent](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux).

4. Sonstiges

   Unter Windows sollten auf der VM keine ausstehenden Windows-Updates vorhanden sein, wenn Sie eine Migration auslösen. Andernfalls ist nach Abschluss des Updates die Anmeldung bei der VM nicht mehr möglich. Nach der Migration kann **Startdiagnose** aktiviert werden, um einen Screenshot der VM anzuzeigen. Falls dies nicht funktioniert, sollte überprüft werden, ob die VM ausgeführt wird, und die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) gelesen werden.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie [VMs auf die Migration vorbereiten](https://docs.microsoft.com/azure/migrate/prepare-for-migration).

## <a name="step-3-replicate-the-on-premises-vms"></a>Schritt 3: Replizieren der lokalen VMs

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren. Nachdem die Ermittlung abgeschlossen ist, können sie mit dem Replizieren von VMware-VMs in Azure beginnen.

1. Klicken Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** die Option **Replizieren** aus.

    ![Replizieren von VMs](./media/contoso-migration-devtest-to-iaas/select-replicate.png) _Abbildung 8: Replizieren von VMs_

2. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere** aus.

3. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance, die Sie eingerichtet haben, und dann **OK** aus.

    ![Quelleinstellungen](./media/contoso-migration-devtest-to-iaas/source-settings.png) _Abbildung 9: Quelleinstellungen_

4. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten.
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie hierzu unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung ausgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

      ![Auswählen der Bewertung](./media/contoso-migration-devtest-to-iaas/select-assessment.png)
      _Abbildung 10: Einrichten der erforderlichen Komponenten_

5. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und aktivieren Sie alle VMs, die Sie migrieren möchten. Wählen Sie anschließend **Weiter: Zieleinstellungen**.

6. Wählen Sie unter **Zieleinstellungen** das Abonnement und die Zielregion für die Migration aus, und geben Sie die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden. Wählen Sie unter **Virtuelles Netzwerk** das Azure-VNET/-Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

7. Wählen Sie unter **Azure-Hybridvorteil** die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Wählen Sie **Weiter** aus. Wählen Sie **Ja** aus, wenn Sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Wählen Sie **Weiter** aus.

      > [!NOTE]
      > Im Fall von Contoso wird **Nein** für den Azure-Hybridvorteil ausgewählt, da es sich hierbei um ein Azure Dev/Test-Abonnement handelt. Das bedeutet, dass nur für die Computekapazität bezahlt wird. Der [Azure-Hybridvorteil](https://azure.microsoft.com/pricing/hybrid-benefit) sollte nur für Produktionssysteme mit Software Assurance-Vorteilen verwendet werden.

8. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste für die VM-Größe die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der höchsten Übereinstimmung im Azure-Abonnement aus. Sie können stattdessen unter **Azure-VM-Größe** eine manuelle Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

9. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen, und wählen Sie in Azure den Datenträgertyp aus (SSD Standard/HDD Standard oder Managed Disks Premium). Wählen Sie **Weiter** aus. Sie können Datenträger von der Replikation ausschließen. In diesem Fall sind die Datenträger nach der Migration nicht auf der Azure-VM vorhanden.

10. Überprüfen Sie unter **Replikation prüfen und starten** die Einstellungen, und klicken Sie dann auf **Replizieren**, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-4-migrate-the-vms"></a>Schritt 4: Migrieren der VMs

Die Contoso-Administratoren führen eine schnelle Testmigration und dann eine vollständige Migration aus, um die VMs zu migrieren.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** die Option **Migrierte Server testen** aus.

    ![Testen der migrierten Server](./media/contoso-migration-devtest-to-iaas/test-migrated-servers.png) _Abbildung 11: Testen der migrierten Server_

2. Wählen und halten Sie (oder klicken Sie mit der rechten Maustaste auf) die zu testende VM, und klicken Sie anschließend auf **Testmigration**.

    ![Testmigration](./media/contoso-migration-devtest-to-iaas/test-migrate.png) _Abbildung 12: Testen der Migration_

3. Wählen Sie unter **Testmigration** das Azure VNET aus, in dem sich die Azure-VM nach der Migration befindet. Es empfiehlt sich, ein nicht für die Produktion bestimmtes VNET zu verwenden.
4. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
5. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
6. Wählen und halten Sie nach Abschluss des Tests unter **Aktuell replizierte Computer** die Azure-VM (oder klicken mit der rechten Maustaste darauf), und klicken Sie anschließend auf **Testmigration bereinigen**.

    ![Bereinigen der Testmigration](./media/contoso-migration-devtest-to-iaas/clean-up.png) _Abbildung 13: Bereinigen der Testmigration_

### <a name="migrate-the-vms"></a>Migrieren der VMs

Die Contoso-Administratoren führen jetzt eine vollständige Migration aus.

1. Wählen Sie im Azure Migrate-Projekt die Optionen **Server**, **Azure Migrate: Servermigration** und **Server werden repliziert** aus.

    ![Replizieren der Server](./media/contoso-migration-devtest-to-iaas/replicating-servers.png) _Abbildung 14: Replizieren der Server_

2. Wählen und halten Sie unter **Aktuell replizierte Computer** die VM (oder klicken Sie mit der rechten Maustaste darauf), und klicken Sie dann auf **Migrieren**.
3. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus. Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. So wird sichergestellt, dass keine Daten verloren gehen. Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
4. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
5. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie eine [Testmigration ausführen](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) und [VMs zu Azure migrieren](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Die Entwicklungs-VMs für die Anwendungen SmartHotel360 und osTicket werden nach Abschluss der Migration auf Azure-VMs ausgeführt.

Contoso muss jetzt folgende Schritte für die Bereinigung durchführen:

- Beenden der Replikation nach Abschluss der Migration.
- Entfernen der VMs `WEBVMDEV`, `SQLVMDEV`, `OSTICKETWEBDEV` und `OSTICKETMYSQLDEV` aus dem vCenter-Bestand.
- Entfernen aller VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation zum Anzeigen des neuen Speicherorts und der IP-Adressen für die VMs.
- Überprüfen sämtlicher Ressourcen, die mit den VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die Anwendung jetzt ausgeführt wird, muss Contoso sie nun vollständig in Azure operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs auf eventuell vorhandene Sicherheitsprobleme. Zur Steuerung des Zugriffs überprüft das Team die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer. Mithilfe von NSGs wird sichergestellt, dass nur für die Anwendung zulässiger Datenverkehr diese erreichen kann. Das Team zieht darüber hinaus in Betracht, die Daten über Azure Disk Encryption und Azure Key Vault auf dem Datenträger zu sichern.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgende Aktion durch: Schützen von Daten. Contoso sichert die Daten auf den VMs mithilfe des Azure Backup-Diensts. Weitere Informationen finden Sie unter [Ein Überblick über die Sicherung von Azure-VMs](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

Contoso stellt sicher, dass alle Azure-Entwicklungsressourcen mithilfe dieses Dev/Test-Abonnements erstellt werden, um 80 Prozent zu sparen. Das Unternehmen aktiviert [Azure Cost Management und Abrechnung](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso den Entwicklungs-VMs, die für die Anwendungen SmartHotel360 und osTicket in Azure verwendet werden, einen neuen Host zugewiesen hat, indem die Anwendungs-VMs mithilfe des Tools für die Azure Migrate- Servermigration zu Azure migriert wurden.
