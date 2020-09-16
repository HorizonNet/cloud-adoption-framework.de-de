---
title: Migrieren einer App zu Azure App Service und SQL-Datenbank
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie eine App umgestalten, indem Sie sie zu Azure App Service und Azure SQL-Datenbank migrieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 399f6e4d6506539c59d17670ba6f55f2df82a0c5
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602876"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc smarthotel SHWEB SHWCF -->

# <a name="migrate-an-application-to-azure-app-service-and-sql-database"></a>Migrieren einer App zu Azure App Service und SQL-Datenbank

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso eine auf VMware-VMs ausgeführte Windows .NET-Anwendung mit zwei Ebenen im Rahmen einer Migration zu Azure umgestaltet. Das Team von Contoso migriert die Front-End-VM der Anwendung zu einer Azure App Service-Web-App und die Anwendungsdatenbank zu einer Azure SQL-Datenbank-Instanz.

Die in diesem Beispiel verwendete Anwendung „SmartHotel360“ wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam von Contoso hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was sie mit dieser Migration erreichen möchten:

- **Unternehmenswachstum**. Contoso wächst, und damit steigt die Last auf seinen lokalen Systeme und Infrastrukturen.
- **Steigern der Effizienz**. Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigern der Flexibilität**. Die IT-Abteilung von Contoso muss schneller auf geschäftliche Anforderungen reagieren, um in einer globalen Wirtschaft erfolgreich zu sein. Sie muss in der Lage sein, schneller auf Änderungen auf dem Markt zu reagieren. Die IT darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung:** Bei einer Anwendung für Hunderttausende oder Millionen von Mandanten sind Ansätze mit gemeinsamer Datenbanknutzung vorteilhaft, z.B. Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Senken der Kosten:** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat die folgenden Ziele festgelegt, um die beste Migrationsmethode bestimmen zu können:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Anwendung** | Die Anwendung wird in Azure die gleiche zentrale Bedeutung haben wie heute lokal. <br><br> Sie sollte die gleichen Leistungsmerkmale wie aktuell in VMware aufweisen. <br><br> Das Team möchte nicht in die Anwendung investieren. Vorerst werden die Administratoren die Anwendung daher lediglich sicher in die Cloud verschieben. <br><br> Das Team möchte die Unterstützung für Windows Server 2008 R2 einstellen, das Betriebssystem, unter dem die Anwendung derzeit ausgeführt wird. <br><br> Das Team möchte SQL Server 2008 R2 generell nicht mehr verwenden und zu einer modernen Platform-as-a-Service-Datenbankplattform (PaaS) wechseln, die den Verwaltungsaufwand minimiert. <br><br> Seine Investitionen in die SQL Server-Lizenzierung und in die Software Assurance möchte Contoso nutzen, wo immer dies möglich ist. <br><br> Darüber hinaus möchte Contoso die Auswirkungen des Single Point of Failure in der Webebene abschwächen. |
| **Einschränkungen** | Die Anwendung besteht aus einer ASP.NET-Anwendung und einem Windows Communication Foundation-Dienst (WCF), die auf demselben virtuellen Computer ausgeführt werden. Sie möchten diese Komponenten mithilfe von Azure App Service auf zwei Web-Apps verteilen. |
| **Azure** | Contoso möchte die Anwendung zu Azure migrieren, sie soll jedoch nicht auf virtuellen Computern ausgeführt werden. Sowohl in der Web- als auch in der Datenschicht soll auf Azure-PaaS-Dienste zurückgegriffen werden. |
| **DevOps** | Contoso möchte auf ein DevOps-Modell umsteigen und Azure DevOps für Builds und Releasepipelines verwenden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung. Das Unternehmen ermittelt den Migrationsprozess, einschließlich der Azure-Dienste, die für die Migration verwendet werden.

### <a name="current-application"></a>Aktuelle Anwendung

- Die lokale Anwendung „SmartHotel360“ ist auf zwei virtuelle Computer aufgeteilt: `WEBVM` und `SQLVM`.
- Die VMs befinden sich auf dem VMware ESXi-Host „contosohost1.contoso.com“ (Version 6.5).
- Die VMware-Umgebung wird von vCenter Server 6.5 („vcenter.contoso.com“) auf einem virtuellen Computer verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum („contoso-datacenter“) mit einem lokalen Domänencontroller („contosodc1“).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Für die Datenbankebene der Anwendung hat Contoso Azure SQL-Datenbank mit SQL Server verglichen. Grundlage dafür war der Artikel [Featurevergleich: Azure SQL-Datenbank und Azure SQL Managed Instance](/azure/sql-database/sql-database-features). Die Entscheidung für Azure SQL-Datenbank hat für Contoso verschiedene Gründe:
  - Azure SQL-Datenbank ist ein verwalteter relationaler Datenbankdienst. Er bietet eine vorhersagbare Leistung auf mehreren Serviceleveln bei nahezu keinem Administrationsaufwand. Zu den Vorteilen gehören dynamische Skalierbarkeit ohne Ausfallzeiten, integrierte intelligente Optimierung sowie globale Skalierbarkeit und Verfügbarkeit.
  - Contoso kann den einfachen Datenmigrations-Assistenten nutzen, um die Migration der lokalen Datenbank zu Azure SQL-Datenbank zu bewerten.
  - Contoso kann Azure Database Migration Service verwenden, um lokale Datenbanken zu Azure SQL zu migrieren.
  - Mit der Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen für eine Datenbank in SQL-Datenbank austauschen. Diese Vorgehensweise kann zu Kosteneinsparungen von bis zu 30 Prozent führen.
  - SQL-Datenbank bietet verschiedene Sicherheitsfeatures, darunter Always Encrypted, dynamische Datenmaskierung und Sicherheit bzw. SQL-Bedrohungserkennung auf Zeilenebene.
- Für die Webebene der App hat sich Contoso dazu entschieden, Azure App Service zu verwenden. Über diesen PaaS-Dienst kann die Anwendung mit nur wenigen Konfigurationsänderungen bereitgestellt werden. Contoso verwendet Visual Studio, um die Änderung vorzunehmen, und stellt zwei Web-Apps bereit, eine für die Website und eine für den WCF-Dienst.
- Um die Anforderungen einer DevOps-Pipeline zu erfüllen, verwendet Contoso Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service bereitgestellt.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet seinen vorgeschlagenen Entwurf aus, indem das Unternehmen eine Liste mit den Vor- und Nachteilen erstellt. Dies ist in der folgenden Tabelle dargestellt:

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Der Code der SmartHotel360-App erfordert für die Migration zu Azure keine Änderungen. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für SQL Server und Windows Server nutzen. <br><br> Nach der Migration muss Windows Server 2008 R2 nicht unterstützt werden. Weitere Informationen finden Sie in der [Microsoft Lifecycle-Richtlinie](https://aka.ms/lifecycle). <br><br> Contoso kann die Webebene der Anwendung mit mehreren Instanzen konfigurieren, sodass sie kein Single Point of Failure mehr ist. <br><br> Die Datenbank ist nicht mehr auf das veraltete SQL Server 2008 R2 angewiesen. <br><br> SQL-Datenbank unterstützt die technischen Anforderungen. Contoso hat die lokale Datenbank mithilfe des Datenmigrations-Assistenten bewertet und festgestellt, dass sie kompatibel ist. <br><br> Azure SQL-Datenbank verfügt über eine integrierte Fehlertoleranz, die Contoso nicht einrichten muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist. <br><br> Wenn Contoso Azure Database Migration Service für die Migration der Datenbank verwendet, verfügt das Unternehmen über die entsprechende Infrastruktur für die Migration umfangreicher Datenbanken. |
| **Nachteile** | Azure App Service unterstützt nur eine Anwendungsbereitstellung für jede Web-App. Dies bedeutet, dass zwei Web-Apps bereitgestellt werden müssen, eine für die Website und eine für den WCF-Dienst. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Diagramm der vorgeschlagenen Architektur](./media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt eine verwaltete Azure SQL-Instanz bereit und migriert die Datenbank von „SmartHotel360“ mithilfe von Azure Database Migration Service zu dieser Instanz.
1. Contoso stellt Web-Apps bereit, konfiguriert sie und stellt die Anwendung SmartHotel360 in ihnen bereit.

    ![Diagramm zum Migrationsprozess.](./media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure App Service-Migrations-Assistent](/learn/paths/migrate-dotnet-apps-azure/) | Eine kostenlose und einfache Möglichkeit, um .NET-Webanwendungen aus der lokalen Umgebung nahtlos und mit minimalen oder sogar ganz ohne Codeänderungen zur Cloud zu migrieren. | Sie können das Tool kostenlos herunterladen. |
| [Data Migration Assistant](/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso nutzt den Datenmigrations-Assistenten, um Kompatibilitätsprobleme zu bewerten und zu erkennen, die sich unter Umständen auf die Datenbankfunktionen in Azure auswirken. Der Datenmigrations-Assistent bewertet die Featureparität zwischen SQL-Quellen und -Zielen und empfiehlt Verbesserungen der Leistung und Zuverlässigkeit. | Sie können das Tool kostenlos herunterladen. |
| [Azure Database Migration Service](/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration mehrerer Datenbankquellen zu Azure-Datenplattformen mit minimaler Downtime. | Informieren Sie sich über die [unterstützten Regionen](/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Azure SQL-Datenbank](/azure/azure-sql/database/sql-database-paas-overview) | Ein intelligenter, vollständig verwalteter Dienst für relationale Clouddatenbanken. | Die Kosten basieren auf Features, Durchsatz und Größe. [Weitere Informationen](https://azure.microsoft.com/pricing/details/sql-database/managed) |
| [Azure App Service](/azure/app-service/overview) | Hilft beim Erstellen leistungsstarker Cloudanwendungen auf einer vollständig verwalteten Plattform. | Die Kosten basieren auf Größe, Standort und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |
| [Azure DevOps](/azure/azure-portal/tutorial-azureportal-devops) | Stellt die Pipeline für Continuous Integration und Continuous Deployment (CI/CD) für die App-Entwicklung bereit. Die Pipeline beginnt bei einem Git-Repository für die Verwaltung von Anwendungscode, einem Buildsystem zum Erstellen von Paketen und anderen Buildartefakten sowie einem Releaseverwaltungssystem zum Bereitstellen von Änderungen in Entwicklungs-, Test- und Produktionsumgebungen. |

## <a name="prerequisites"></a>Voraussetzungen

Zum Ausführen dieses Szenarios muss Contoso die folgenden Voraussetzungen erfüllen:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Abonnements wurden in einem früheren Artikel dieser Reihe erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bewerten und Migrieren der Web-Apps**. Contoso verwendet den [Azure App Service-Migrations-Assistenten](https://azure.microsoft.com/migration/web-applications/), um die Kompatibilität vor der Migration zu überprüfen und die Web-Apps zu Azure App Service zu migrieren.
> - **Schritt 2: Bereitstellen einer Datenbank in Azure SQL-Datenbank**. Contoso stellt eine Azure SQL-Datenbank-Instanz bereit. Nachdem die App-Website zu Azure migriert wurde, verweist die Web-App für den WCF-Dienst auf diese Instanz.
> - **Schritt 3: Bewerten der Datenbank**. Contoso bewertet die Datenbank für die Migration mithilfe des Datenmigrations-Assistenten und migriert sie anschließend mit Azure Database Migration Service.
> - **Schritt 4: Einrichten von Azure DevOps**. Contoso erstellt ein neues Azure DevOps-Projekt und importiert das Git-Repository.
> - **Schritt 5: Konfigurieren von Verbindungszeichenfolgen**. Contoso konfiguriert Verbindungszeichenfolgen, damit die Web-App auf Webebene, die Web-App für den WCF-Dienst und die SQL-Instanz kommunizieren können.
> - **Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps**. Im letzten Schritt richtet Contoso Build- und Releasepipelines in Azure DevOps zum Erstellen der Anwendung ein und stellt sie in zwei separaten Web-Apps bereit.

## <a name="step-1-assess-and-migrate-the-web-apps"></a>Schritt 1: Bewerten und Migrieren der Web-Apps

Contoso-Administratoren bewerten und migrieren ihre Web-App mithilfe des [Azure App Service-Migrations-Assistenten](https://azure.microsoft.com/migration/web-applications/). Bei dem Prozess orientieren sie sich am [Microsoft-Lernpfad](/learn/paths/migrate-dotnet-apps-azure/). Die Administratoren führen im Wesentlichen folgende Aktionen aus:

- Sie verwenden die [Azure App Service-Migrationsbewertung](https://appmigration.microsoft.com/assessment/), um alle ggf. vorhandenen Abhängigkeiten zwischen Ihren Web-Apps auszuwerten und um mögliche Inkompatibilitäten zwischen ihren lokalen Web-Apps und der Unterstützung durch Azure App Service zu ermitteln.

- Sie laden den Azure App Service-Migrations-Assistenten herunter und melden sich bei ihrem Azure-Konto an.

- Sie wählen ein Abonnement, eine Ressourcengruppe und den Domänennamen der Website aus.

## <a name="step-2-provision-a-database-in-azure-sql-database"></a>Schritt 2: Bereitstellen einer Datenbank in Azure SQL-Datenbank

1. Die Administratoren von Contoso entscheiden sich dafür, eine Azure SQL-Datenbank-Instanz zu erstellen.

    ![Screenshot des Links „SQL-Datenbank“](./media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

1. Sie geben einen Datenbanknamen an, der mit der Datenbank `SmartHotel.Registration` übereinstimmt, die auf dem lokalen virtuellen Computer ausgeführt wird. Die Datenbank wird dann in der ContosoRG-Ressourcengruppe platziert. Dies ist die Ressourcengruppe, die das Unternehmen für die Produktionsressourcen in Azure verwendet.

    ![Screenshot der Details der SQL-Datenbankinstanz](./media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

1. Das Unternehmen richtet eine neue SQL Server-Instanz, **sql-smarthotel-eus2**, in der primären Region ein.

    ![Screenshot der neuen SQL Server-Instanz](./media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

1. Den Tarif legt das Unternehmen entsprechend seiner Server- und Datenbankanforderungen fest. Zudem entscheidet es sich, Geld mit dem Azure-Hybridvorteil zu sparen, da es bereits über eine SQL Server-Lizenz verfügen.
1. Zur Größenanpassung nutzt es das auf virtuellen Kernen basierende Kaufmodell und legt die Grenzwerte für seine erwarteten Anforderungen fest.

    ![Screenshot der Größenanforderungen für den virtuellen Kern](./media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

1. Dann erstellt das Unternehmen die Datenbankinstanz.

    ![Screenshot: Erstellen einer SQL-Datenbankinstanz](./media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

1. Anschließend öffnet das Team die Datenbank und notiert sich Details, die für die Migration mit dem Datenmigrations-Assistenten benötigt werden.

    ![Screenshot der Textdatei der Datenbankinstanz](./media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Benötigen Sie weitere Hilfe?**

- [Erhalten Sie Hilfe](/azure/sql-database/sql-database-get-started-portal) bei der Bereitstellung einer SQL-Datenbank-Instanz.
- Erfahren Sie mehr zu den [Ressourcenlimits für virtuelle Kerne](/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools).

## <a name="step-3-assess-the-database"></a>Schritt 3: Bewerten der Datenbank

Die Contoso-Administratoren bewerten die Datenbank mithilfe des Datenbankmigrations-Assistenten und migrieren sie anschließend anhand des [Tutorials: Onlinemigration von SQL Server zu einer Einzel- oder Pooldatenbank in Azure SQL-Datenbank mit DMS](/azure/dms/tutorial-sql-server-azure-sql-online) mithilfe von Azure Database Migration Service. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) ausführen.

Die Administratoren gehen im Wesentlichen wie folgt vor:

- Sie nutzen den Datenmigrations-Assistenten zum Ermitteln und Beheben aller Probleme bei der Datenbankmigration.
- Sie erstellen eine Azure Database Migration Service-Instanz mit einer Premium-SKU, die mit dem virtuellen Netzwerk verbunden ist.
- Sie vergewissern sich, dass die Instanz über das virtuelle Netzwerk auf die SQL Server-Remoteinstanz zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu SQL Server auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem SQL Server gehostet ist, zugelassen werden.
- Sie konfigurieren die Instanz:
  - Erstellen Sie ein Migrationsprojekt.
  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.
  - Wählen Sie ein Ziel aus.
  - Wählen Sie die zu migrierenden Datenbanken aus.
  - Konfigurieren Sie die erweiterten Einstellungen.
  - Starten Sie die Replikation.
  - Beheben Sie alle Fehler.
  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.

## <a name="step-4-set-up-azure-devops"></a>Schritt 4: Einrichten von Azure DevOps

Contoso muss die DevOps-Infrastruktur und die Pipelines für die Anwendung erstellen. Hierzu erstellen die Administratoren von Contoso ein neues DevOps-Projekt, importieren ihren Code und richten anschließend die Build- und Releasepipelines ein.

1. Im Azure DevOps-Konto von Contoso erstellen sie ein neues Projekt namens **ContosoSmartHotelRefactor** und wählen anschließend **Git** für die Versionskontrolle aus.

    ![Screenshot: Erstellen eines neuen Projekts in Azure DevOps](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

1. Sie importieren das Git-Repository, das derzeit ihren Anwendungscode enthält. Sie laden es aus dem [öffentlichen GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Registration) herunter.

    ![Screenshot des Bereichs „Git-Repository importieren“](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

1. Sie stellen eine Verbindung von Visual Studio mit dem Repository her und klonen den Code mithilfe von Team Explorer zum Entwicklercomputer.

    ![Screenshot des Bereichs „Verbindung mit einem Projekt herstellen“](./media/contoso-migration-refactor-web-app-sql/devops1.png)

1. Sie öffnen die Projektmappendatei für die Anwendung. Die Datei enthält separate Projekte für die Web-App und den WCF-Dienst.

    ![Screenshot des Projektmappen-Explorers mit der Auflistung der Web-App- und WCF-Dienstprojekte](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Schritt 5: Konfigurieren von Verbindungszeichenfolgen

Die Administratoren von Contoso müssen sicherstellen, dass die Web-Apps und die Datenbank miteinander kommunizieren können. Zu diesem Zweck konfiguriert das Unternehmen Verbindungszeichenfolgen im Code und in den Web-Apps.

1. In der Web-App für den WCF-Dienst (`SHWCF-EUS2`) fügt Contoso unter **Einstellungen** > **Anwendungseinstellungen** eine neue Verbindungszeichenfolge mit dem Namen **DefaultConnection** hinzu.
1. Die Verbindungszeichenfolge wird von der Datenbank „SmartHotel-Registration“ abgerufen und mit den entsprechenden Anmeldeinformationen aktualisiert.

    ![Screenshot des Bereichs „Einstellungen für Verbindungszeichenfolgen“](./media/contoso-migration-refactor-web-app-sql/string1.png)

1. Die Administratoren öffnen in Visual Studio das Projekt `SmartHotel.Registration.wcf` in der Projektmappendatei. Im Projekt aktualisieren sie den Abschnitt `connectionStrings` der Datei `web.config` mit der Verbindungszeichenfolge.

     ![Screenshot des Abschnitts „connectionStrings“ der Datei „web.config“ im Projekt „SmartHotel.Registration.wcf“](./media/contoso-migration-refactor-web-app-sql/string2.png)

1. Sie ändern den Abschnitt `client` der Datei `web.config` für `SmartHotel.Registration.Web` so, dass er auf den neuen Speicherort des WCF-Diensts verweist. Dies ist die URL der WCF-Web-App, die den Dienstendpunkt hostet.

    ![Screenshot des Abschnitts „Client“ der Datei „web.config“ im Projekt „SmartHotel.Registration.wcf“](./media/contoso-migration-refactor-web-app-sql/strings3.png)

1. Wenn die Codeänderungen abgeschlossen sind, committen und synchronisieren die Administratoren sie mithilfe von Team Explorer in Visual Studio.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps

Als Nächstes konfigurieren die Contoso-Administratoren Azure DevOps für die Durchführung des Build- und Releasevorgangs.

1. Dazu wählen sie in Azure DevOps **Build und Release** > **Neue Pipeline** aus.

    ![Screenshot des Links „Neue Pipeline“ in Azure DevOps](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

1. Sie wählen **Azure Repos Git** aus, und in der Dropdownliste **Repository** wählen sie das relevante Repository aus.

    ![Screenshot der Schaltfläche „Azure Repos Git“ und des ausgewählten Repositorys](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

1. Unter **Vorlage auswählen** wählen sie die Vorlage **ASP.NET** für ihren Build aus.

     ![Screenshot des Bereichs „Vorlage auswählen“ zum Auswählen der ASP.NET-Vorlage](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

1. Sie verwenden den Namen **ContosoSmartHotelRefactor-ASP.NET-CI** für den Build und wählen anschließend **Save & queue** (Speichern und in die Warteschlange stellen) aus, wodurch der erste Build gestartet wird.

     ![Screenshot der Schaltfläche „Save & queue“ (Speichern und in die Warteschlange stellen) für den Build](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

1. Sie wählen die Buildnummer aus, um den Prozess zu überwachen. Nachdem dieser abgeschlossen ist, können die Administratoren das Prozessfeedback sehen und **Artefakte** auswählen, um die Buildergebnisse zu überprüfen.

    ![Screenshot der Buildseite und des Links „Artefakte“ zum Überprüfen der Buildergebnisse](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

    Der Bereich **Artefakte-Explorer** wird geöffnet, und im **Ablageordner** werden die Buildergebnisse angezeigt.

    - Die beiden ZIP-Dateien sind die Pakete, die die Anwendungen enthalten.
    - Diese ZIP-Dateien werden in der Releasepipeline für die Bereitstellung in Azure App Service verwendet.

     ![Screenshot des Bereichs „Artefakte-Explorer“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline6.png)

1. Sie wählen **Releases** >  **+ Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

1. Sie wählen die Bereitstellungsvorlage für Azure App Service aus.

    ![Screenshot der Azure App Service-Bereitstellungsvorlage](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

1. Sie nennen die Releasepipeline **ContosoSmartHotel360Refactor** und geben im Feld **Phasenname** den Namen **SHWCF-EUS2** als Namen der WCF-Web-App ein.

    ![Screenshot des Phasennamens der WCF-Web-App](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

1. Sie klicken unter den Phasen auf **1 Auftrag, 1 Aufgabe**, um die Bereitstellung des WCF-Diensts zu konfigurieren.

    ![Screenshot der Option „1 Auftrag, 1 Aufgabe“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline10.png)

1. Sie überprüfen, ob das Abonnement ausgewählt und autorisiert ist, und wählen anschließend den **App Service-Namen** aus.

     ![Screenshot: Auswählen des App-Dienstnamens](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

1. In der Pipeline klicken sie dann unter **Artefakte** auf **+ Artefakt hinzufügen** und wählen für den Build die Pipeline **ContosoSmarthotel360Refactor** aus.

     ![Screenshot der Schaltfläche „Build“ im Bereich „Artefakt hinzufügen“](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

1. Die Administratoren wählen das Blitzsymbol des ausgewählten Artefakts aus, um den Continuous Deployment-Trigger zu aktivieren.

     ![Screenshot des Blitzsymbols für das Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

1. Sie legen den Continuous Deployment-Trigger auf **Aktiviert** fest.

    ![Screenshot des aktivierten Continuous Deployment-Triggers](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

1. Die Administratoren navigieren zurück zur Phase **1 Auftrag, 1 Aufgabe** und wählen anschließend **Azure App Service bereitstellen** aus.

    ![Screenshot der Option zum Auswählen von „Azure App Service bereitstellen“](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

1. Unter **Datei oder Ordner suchen** erweitern sie den **Ablageordner**, wählen die Datei *SmartHotel.Registration.Wcf.zip* aus, die während der Erstellung erstellt wurde, und klicken anschließend auf **Speichern**.

    ![Screenshot des Bereichs „Datei oder Ordner suchen“ zum Auswählen der WCF-Datei](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

1. Sie wählen **Pipeline** > **Phasen** und anschließend **+ Hinzufügen** aus, um eine Umgebung für `SHWEB-EUS2` hinzuzufügen. Sie wählen eine weitere Azure App Service-Bereitstellung aus.

    ![Screenshot des Links „1 Auftrag, 1 Aufgabe“ zum Hinzufügen einer Umgebung](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

1. Sie wiederholen den Prozess, um die Datei `SmartHotel.Registration.Web.zip` in der korrekten Web-App zu veröffentlichen, und wählen anschließend **Speichern** aus.

    ![Screenshot des Bereichs „Datei oder Ordner suchen“ zum Auswählen der WEB-Datei](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

    Die Releasepipeline wird wie folgt angezeigt:

     ![Screenshot der Zusammenfassung der Releasepipeline](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

1. Sie navigieren zurück zu **Build**, wählen **Trigger**aus und aktivieren anschließend das Kontrollkästchen **Continuous Integration aktivieren**. Diese Aktion aktiviert die Pipeline. Wenn also Änderungen am Code committet werden, erfolgt ein vollständiger Build mit Release.

    ![Screenshot mit dem hervorgehobenen Kontrollkästchen „Continuous Integration aktivieren“](./media/contoso-migration-refactor-web-app-sql/pipeline20.png)

1. Sie klicken auf **Save & queue** (Speichern und in Warteschlange stellen), um die vollständige Pipeline auszuführen. Ein neuer Build wird ausgelöst, der wiederum das erste Release der App in Azure App Service erstellt.

    ![Screenshot der Schaltfläche „Save & Queue“ (Speichern und in Warteschlange stellen)](./media/contoso-migration-refactor-web-app-sql/pipeline21.png)

1. Die Administratoren von Contoso können die Verarbeitung von Build- und Releasepipeline in Azure DevOps überwachen. Wenn der Build abgeschlossen wurde, wird das Release gestartet.

    ![Screenshot des Fortschritts der Build- und Release-App](./media/contoso-migration-refactor-web-app-sql/pipeline22.png)

1. Nachdem die Pipeline abgeschlossen wurde, sind beide Websites bereitgestellt, und die Anwendung wird online ausgeführt.

    ![Screenshot: Anwendung wird ausgeführt](./media/contoso-migration-refactor-web-app-sql/pipeline23.png)

    Die Anwendung wurde erfolgreich zu Azure migriert.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration führt Contoso die folgenden Schritte zur Bereinigung aus:

- Das Unternehmen entfernt die lokalen VMs aus dem vCenter-Bestand.
- Es entfernt die virtuellen Computer aus den lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation, um die neuen Speicherorte für die Anwendung „SmartHotel360“ anzuzeigen. Die Dokumentation zeigt an, dass die Datenbank in Azure SQL-Datenbank und das Front-End in zwei Web-Apps ausgeführt wird.
- Das Unternehmen überprüft sämtliche Ressourcen, die mit den außer Betrieb genommenen virtuellen Computern interagieren, und aktualisiert alle relevanten Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Nachdem die Ressourcen nun zu Azure migriert wurden, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neue Datenbank `SmartHotel-Registration` geschützt ist. [Weitere Informationen](/azure/sql-database/sql-database-security-overview)
- Insbesondere muss Contoso die Web-Apps für die Verwendung von SSL mit Zertifikaten aktualisieren.

### <a name="backups"></a>Backups

- Das Team von Contoso überprüft die Sicherungsanforderungen für Azure SQL-Datenbank. [Weitere Informationen](/azure/sql-database/sql-database-automated-backups)
- Es muss sich auch über die Verwaltung von Sicherungen und Wiederherstellungen in SQL-Datenbank informieren. [Erfahren Sie mehr über automatische Sicherungen.](/azure/sql-database/sql-database-automated-backups)
- Das Unternehmen muss die Implementierung von Failovergruppen berücksichtigen, um ein regionales Failover für die Datenbank bereitzustellen. [Weitere Informationen](/azure/sql-database/sql-database-geo-replication-overview)
- Es muss hinsichtlich der Resilienz die Bereitstellung der Web-App in der Hauptregion (`East US 2`) und der sekundären Region (`Central US`) in Erwägung ziehen. Das Team könnte den Traffic Manager konfigurieren, um ein Failover während regionaler Ausfälle sicherzustellen.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, weist Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zu.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Diese Kosten werden über das Enterprise Agreement verrechnet.
- Contoso verwendet die [Azure-Kostenverwaltung und -Abrechnung](/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

Im vorliegenden Artikel hat Contoso die App SmartHotel360 in Azure umgestaltet, indem das Unternehmen die Front-End-VM der App mithilfe zweier Azure App Service-Web-Apps migriert hat. Die Anwendungsdatenbank wurde zu einer Azure SQL-Datenbank-Instanz migriert.
