---
title: Migrieren von Objekten
description: Initiieren Sie die Migration zu Azure, indem Sie die geeigneten Tools ermitteln, z. B. native Tools, Drittanbietertools und Projektmanagementtools.
author: matticusau
ms.author: mlavery
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 1a52864576b7965a10a2fb7a4f3ea773cd4979c9
ms.sourcegitcommit: fbfd66dab002b549d3e9cbf1b7efa0099d0b7700
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282929"
---
# <a name="deploy-workloads-and-assets-infrastructure-apps-and-data"></a>Bereitstellen von Workloads und Assets (Infrastruktur, Apps und Daten)

In dieser Phase verwenden Sie die Ausgabe der Bewertungsphase, um die Migration der Umgebung einzuleiten. Dieser Leitfaden hilft Ihnen, die geeigneten Tools zu identifizieren, um den Zustand „Abgeschlossen“ zu erreichen. Hierbei lernen Sie native Tools, Tools von Drittanbietern und Projektmanagementtools. kennen.

## <a name="native-migration-tools"></a>[Native Migrationstools](#tab/Tools)

In den folgenden Abschnitten werden die nativen Azure-Tools beschrieben, die zur Durchführung oder Unterstützung der Migration zur Verfügung stehen. Informationen zur Auswahl der richtigen Tools zur Unterstützung Ihrer Migrationsbemühungen finden Sie im [Leitfaden zur Entscheidungsfindung für Migrationstools des Frameworks für die Cloudeinführung (Cloud Adoption Framework)](../../decision-guides/migrate-decision-guide/index.md).

### <a name="azure-migrate"></a>Azure Migrate

Mit Azure Migrate wird eine vereinheitlichte und erweiterbare Migrationsumgebung bereitgestellt. Azure Migrate bietet eine zentrale dedizierte Umgebung, mit der Sie Ihre Migration über die Phasen der Bewertung und Migration nach Azure verfolgen können. Azure Migrate ermöglicht Ihnen, die Tools Ihrer Wahl zu verwenden und den Fortschritt der Migration über diese Tools hinweg zu verfolgen.

Azure Migrate ist ein zentralisierter Hub für die Bewertung und die Migration von lokaler Infrastruktur, Anwendungen und Daten zu Azure. Er bietet die folgenden Funktionen:

- Einheitliche Plattform mit Bewertung, Migration und Fortschrittsverfolgung.
- Erweiterte Bewertungs- und Migrationsfunktionen:
    - Lokale Server, einschließlich Hyper-V und VMware.
    - Migration ohne Agents Ihrer virtuellen VMware-Computer zu Azure.
    - Datenbankmigration zu Azure SQL-Datenbank oder einer SQL Managed Instance
    - Webanwendungen
    - Virtual Desktop Infrastructure (VDI) zu Windows Virtual Desktop in Azure
    - Große Datensammlungen, die Azure Data Box-Produkte verwenden
- Erweiterbarer Ansatz mit ISV-Integration (z. B. Cloudamize).

Führen Sie die folgenden Schritte aus, um eine Migration mit Azure Migrate durchzuführen:

1. Suchen Sie unter **Alle Dienste** nach Azure Migrate. Wählen Sie **Azure Migrate** aus, um den Vorgang fortzusetzen.
1. Wählen Sie **Tool hinzufügen** , um Ihr Migrationsprojekt zu starten.
1. Wählen Sie das Abonnement, die Ressourcengruppe und die Geografie aus, für die die Migration durchgeführt werden soll.
1. Wählen Sie **Bewertungstool auswählen** > **Azure Migrate: Serverbewertung** > **Weiter** aus.
1. Wählen Sie **Überprüfen + Tools hinzufügen** aus, und überprüfen Sie die Konfiguration. Wählen Sie **Tools hinzufügen** aus, um den Auftrag zur Erstellung des Migrationsprojekts und zur Registrierung der ausgewählten Lösungen zu initiieren.

> [!NOTE]
> Eine für Ihr Szenario spezifische Anleitung finden Sie in den Tutorials und der [Dokumentation](/azure/migrate/migrate-services-overview) zu Azure Migrate.
>

#### <a name="learn-more"></a>Weitere Informationen

- [Informationen zu Azure Migrate](/azure/migrate/migrate-services-overview)
- [Azure Migrate-Tutorial: Migrieren von physischen oder virtualisierten Servern zu Azure](/azure/migrate/tutorial-migrate-physical-virtual-machines)

### <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service ist ein vollständig verwalteter Dienst, der die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen mit minimaler Ausfallzeit ermöglicht (Onlinemigrationen). Azure Database Migration Service führt alle erforderlichen Schritte durch. Sie können Ihre Migrationsprojekte mit der Gewissheit starten, dass die Migration unter Verwendung der von Microsoft empfohlenen bewährten Methoden erfolgt.

#### <a name="create-an-azure-database-migration-service-instance"></a>Erstellen einer Instanz von Azure Database Migration Service

Wenn Sie Azure Database Migration Service zum ersten Mal verwenden, müssen Sie den Ressourcenanbieter für Ihr Azure-Abonnement registrieren:

1. Wählen Sie **Alle Dienste** > **Abonnements** und dann das Zielabonnement aus.
1. Wählen Sie **Ressourcenanbieter** aus.
1. Suchen Sie nach `migration`, und wählen Sie rechts neben **Microsoft.DataMigration** die Option **Registrieren** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

Nach der Registrierung des Ressourcenanbieters können Sie eine Azure Database Migration Service-Instanz erstellen.

1. Wählen Sie **+ Ressource erstellen** aus, und suchen Sie im Marketplace nach **Azure Database Migration Service**.
1. Schließen Sie den Assistenten „Migrationsdienst erstellen“ ab, und wählen Sie anschließend **Erstellen** aus.

Der Dienst ist jetzt bereit, die unterstützten Quelldatenbanken auf Zielplattformen wie SQL Server, MySQL, PostgreSQL oder MongoDB zu migrieren.

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Weitere Informationen finden Sie unter

- [Übersicht über Azure Database Migration Service](/azure/dms/dms-overview)
- [Erstellen einer Instanz von Azure Database Migration Service](/azure/dms/quickstart-create-data-migration-service-portal)
- [Azure Migrate im Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade)
- [Azure-Portal: Erstellen eines Migrationsprojekts](https://portal.azure.com/#create/Microsoft.AzureMigrate)

::: zone-end

### <a name="azure-app-service-migration-assistant"></a>Azure App Service-Migrations-Assistent

Der Azure App Service-Migrations-Assistent ist Teil einer [größeren Anwendungssuite](https://azure.microsoft.com/services/azure-migrate/), die Organisationen bei der Migration zur Cloud unterstützt. Der Migrations-Assistent führt Benutzer auf seiner Benutzeroberfläche durch zwei Aufgaben:

1. Er bewertet eine bestimmte, unter Windows Server installierte Web-App, indem er die Kompatibilität vor der Migration überprüft, um zu ermitteln, ob die Web-App unverändert zu Azure App Service migriert werden kann.
1. Wenn die Bewertung ergibt, dass die Web-App migriert werden kann, führt der Migration Assistant die Migration durch. Sie müssen dem Migration Assistant Zugriff auf Ihr Azure-Konto gewähren sowie die zu verwendenden Ressourcengruppe, einen Namen für die Web-App und weitere Details auswählen.
Alternativ generiert der Migrations-Assistent eine Azure Resource Manager-Vorlage, mit der Sie die Webanwendung mit mehr Automatisierung und Wiederholbarkeit migrieren können.

#### <a name="migrate-a-web-app-to-azure-app-service"></a>Migrieren einer Web-App zu Azure App Service

Zu Beginn des Migrationsprozesses benötigt der Migration Assistant wichtige Informationen zu Ihrem Azure-Konto.

Melden Sie sich zunächst bei Ihrem Azure-Konto an, und verknüpfen Sie die Migration Assistant-Sitzung über einen eindeutigen Code mit Ihrem Konto. Wählen Sie anschließend das Abonnement, die Ressourcengruppe und den Domänennamen der Website aus. Sie können einen neuen Azure App Service-Plan zum Hosten der App erstellen oder einen vorhandenen Plan auswählen. Die Auswahl wirkt sich auf die geografische Region aus, in der Ihre App gehostet wird. Sie haben zudem die Möglichkeit, diesen Migrationsvorgang einem vorhandenen Azure Migration-Projekt zuzuordnen. Abschließend können Sie die Datenbankeinrichtung entweder überspringen oder eine Hybridverbindung einrichten, um eine Datenbankverbindung zu ermöglichen.

Nachdem der Migrations-Assistent Ihre Angaben erfasst und überprüft hat, werden die benötigten Azure App Service-Ressourcen in der ausgewählten Region und Ressourcengruppe erstellt. Er komprimiert die Quelldateien der Web-App und verwendet die Azure App Service-Bereitstellungs-API, um sie bereitzustellen. Zuletzt werden Sie bei optionalen Schritten unterstützt, wie etwa dem Einrichten einer Hybridverbindung.

Nachdem die App erfolgreich migriert wurde, können weitere Aufgaben erforderlich sein. Dazu kann Folgendes gehören:

- Manuelles Verschieben von Anwendungseinstellungen und Verbindungszeichenfolgen in der Datei „web.config“ zu Azure App Service
- Migrieren von Daten von einer lokalen SQL Server-Instanz zu einer Azure SQL-Datenbank
- Einrichten eines SSL-Zertifikats
- Einrichten von benutzerdefinierten Domänennamen
- Einrichten von Berechtigungen in Azure Active Directory

Sie können auch den Azure App Service-Hostingplan und andere Einstellungen wie automatische Skalierung und Bereitstellungsslots ändern.

Weitere Informationen finden Sie unter: 

[Migrieren von ASP.NET-Apps zu Azure](/learn/paths/migrate-dotnet-apps-azure)

### <a name="data-migration-assistant"></a>Datenmigrations-Assistent

Der Datenmigrations-Assistent (DMA) hilft Ihnen beim Upgrade auf eine moderne Datenplattform, indem er Kompatibilitätsprobleme erkennt, die die Datenbankfunktionalität in Ihrer neuen Version von SQL Server oder Microsoft Azure SQL-Datenbank beeinträchtigen können. DMA empfiehlt Leistungs- und Zuverlässigkeitsverbesserungen für Ihre Zielumgebung und ermöglicht es Ihnen, Ihr Schema, Ihre Daten und abhängige Objekte vom Quellserver auf Ihren Zielserver zu verschieben.

Der Datenmigrations-Assistent ist in Azure Migrate integriert, sodass Sie den gesamten Bewertungsfortschritt im Azure Migrate-Dashboard verfolgen können. Starten Sie DMA aus Azure Migrate, indem Sie das Azure Migrate: Datenbank-Bewertungstool hinzufügen, und fügen Sie Ihre Datenbankbewertung zu Azure Migrate hinzu, indem Sie die Schaltfläche „In Azure Migrate hochladen“ in DMA auswählen.

> [!NOTE]
> Für große Migrationen (in Bezug auf Anzahl und Größe der Datenbanken) empfehlen wir Ihnen, Azure Database Migration Service zu verwenden, mit dem Datenbanken im großen Maßstab migriert werden können.
>

Führen Sie die folgenden Schritte aus, um mit der Nutzung des Datenmigrations-Assistenten zu beginnen:

1. Laden Sie den Datenmigrations-Assistenten aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) herunter, und installieren Sie ihn.
1. Erstellen Sie eine Bewertung, indem Sie das Symbol **Neu (+)** und anschließend den Projekttyp **Bewertung** auswählen.
1. Legen Sie den Quell- und Zielservertyp fest, und wählen Sie anschließend **Erstellen** aus.
1. Konfigurieren Sie die Bewertungsoptionen nach Bedarf (empfohlen werden die Standardwerte).
1. Fügen Sie die Datenbanken zur Bewertung hinzu.
1. Wählen Sie **Weiter** aus, um die Bewertung zu starten.
1. Zeigen Sie die Ergebnisse im Datenmigrations-Assistenten an.

Unternehmen empfehlen wir, dem unter [Bewerten eines Unternehmens und Konsolidieren der Bewertungsberichte mit DMA](/sql/dma/dma-consolidatereports) beschriebenen Ansatz zu folgen, um mehrere Server zu bewerten, die Berichte zu kombinieren und dann die bereitgestellten Power BI-Berichte zur Analyse der Ergebnisse zu verwenden.

Weitere Informationen und ausführliche Verwendungsschritte finden Sie unter:

- [Übersicht über den Datenmigrations-Assistenten](/sql/dma/dma-overview)
- [Bewerten eines Unternehmens und Konsolidieren der Bewertungsberichte mit DMA](/sql/dma/dma-consolidatereports)
- [Analysieren der vom Datenmigrations-Assistenten erstellten konsolidierten Bewertungsberichte mit Power BI](/sql/dma/dma-powerbiassesreport)

### <a name="sql-server-migration-assistant"></a>SQL Server Migration Assistant

Microsoft SQL Server Migration Assistant (SSMA) ist ein Tool zur Automatisierung der Datenbankmigration von Microsoft Access, DB2, MySQL, Oracle und SAP ASE zu SQL Server. Das allgemeine Konzept besteht in der Erfassung, Bewertung und Überprüfung mit diesen Tools. Aufgrund der unterschiedlichen Prozesse für die einzelnen Quellsysteme empfehlen wir Ihnen, die detaillierte [Dokumentation zu SQL Server Migration Assistant](/sql/ssma/sql-server-migration-assistant) zu lesen.

Weitere Informationen finden Sie unter

- [Übersicht über SQL Server Migration Assistant](/sql/ssma/sql-server-migration-assistant)

### <a name="database-experimentation-assistant"></a>Assistent für Datenbankexperimente

Der Assistent für Datenbankexperimente (DEA) ist eine neue A/B-Testlösung für SQL Server-Upgrades. Er hilft bei der Evaluierung einer Zielversion von SQL für eine bestimmte Workload. Kunden, die ein Upgrade von einer früheren SQL Server-Version (SQL Server 2005 und höher) auf eine neue Version von SQL Server ausführen, können diese Analysemetriken verwenden.

Der Assistent für Datenbankexperimente enthält die folgenden Workflowaktivitäten:

- **Erfassen** : Der erste Schritt des SQL Server-A/B-Tests ist die Erfassung einer Ablaufverfolgung auf Ihrem Quellserver. Der Quellserver ist normalerweise der Produktionsserver.
- **Wiedergeben** : Im zweiten Schritt des SQL Server-A/B-Tests wird die erfasste Ablaufverfolgungsdatei auf Ihren Zielservern wiedergegeben. Anschließend werden umfangreiche Ablaufverfolgungen aus den Wiedergaben zur Analyse gesammelt.
- **Analyse** : Der letzte Schritt besteht darin, einen Analysebericht unter Verwendung der Wiedergabeablaufverfolgungen zu generieren. Anhand des Analyseberichts erhalten Sie wertvolle Einblicke in die Auswirkungen der vorgeschlagenen Änderung auf die Leistung.

Weitere Informationen finden Sie unter

- [Übersicht über den Assistenten für Datenbankexperimente](/sql/dea/database-experimentation-assistant-overview)

### <a name="azure-cosmos-db-data-migration-tool"></a>Azure Cosmos DB: Datenmigrationstool

Das Datenmigrationstool von Azure Cosmos DB kann Daten aus verschiedenen Quellen in Azure Cosmos DB-Sammlungen und -Tabellen importieren. Sie können Daten aus JSON-Dateien, CSV-Dateien, SQL-, MongoDB-, Azure Table Storage-, Amazon DynamoDB- und sogar Azure Cosmos DB-SQL-API-Sammlungen importieren. Das Datenmigrationstool kann auch für die Migration von einer Sammlung mit einer einzelnen Partition zu einer Sammlung mit mehreren Partitionen für die SQL-API verwendet werden.

Weitere Informationen finden Sie unter

- [Azure Cosmos DB: Datenmigrationstool](/azure/cosmos-db/import-data)

## <a name="third-party-migration-tools"></a>[Migrationstool von einem Drittanbieter](#tab/third-party-tools)

Verschiedene Migrationstools von Drittanbietern und ISV-Dienste können während der Migration hilfreich sein. Alle bieten unterschiedliche Vorteile und Stärken. Zu diesen Tools zählen:

### <a name="unifycloud"></a>UnifyCloud

UnifyCloud ist ein ISV-Dienst mit Automatisierungstools für die Bewertung, Migration und Modernisierung.

[Weitere Informationen](https://www.unifycloud.com)

### <a name="cloudamize"></a>Cloudamize

Cloudamize ist ein ISV-Dienst, der alle Phasen der Migrationsstrategie abdeckt.

[Weitere Informationen](https://www.cloudamize.com)

### <a name="zerto"></a>Zerto

Zerto stellt virtuelle Replikationsverarbeitung in Microsoft Hyper-V- und VMware vSphere-Umgebungen bereit.

[Weitere Informationen](https://www.zerto.com/modernize)

### <a name="carbonite"></a>Carbonite

Carbonite bietet Server- und Datenmigrationslösungen zur Migration von Workloads zu, von oder zwischen physischen, virtuellen oder cloudbasierten Umgebungen.

[Weitere Informationen](https://www.carbonite.com/data-protection/data-migration-software)

### <a name="movere"></a>Movere

Movere ist eine Ermittlungslösung, die die notwendigen Daten und Erkenntnisse liefert, um Cloudmigrationen zu planen und IT-Umgebungen kontinuierlich und zuverlässig zu optimieren, zu überwachen und zu analysieren.

[Weitere Informationen](https://www.movere.io)

### <a name="azure-cosmos-db-partners"></a>Azure Cosmos DB-Partner

Sie können aus einer Vielzahl erfahrener Systemintegratorpartner und Tools wählen, die Sie bei Ihren Azure Cosmos DB-Migrationen für Ihre NoSQL-Datenbankanforderungen unterstützen.

[Weitere Informationen](/azure/cosmos-db/partners-migration-cosmosdb#migration-tools)

Besuchen Sie das [Azure-Migrationscenter](https://azure.microsoft.com/migration/support), um Organisationen zu ermitteln, die verwendungsbereite Partnertechnologielösungen anbieten, die zu Ihren Migrationsszenarien passen, und erfahren Sie mehr über zusätzliche Migrationstools und Supportdienste von Drittanbietern.

Im [Leitfaden zur Azure-Datenbankmigration](https://datamigration.microsoft.com) finden Sie Informationen zu verschiedenen Datenbankmigrationsoptionen sowie Schritt-für-Schritt-Anleitungen für native Tools und Partner.

## <a name="project-management-tools"></a>[Projektmanagementtools](#tab/project-management-tools)

Bei Projekten, die nicht nachverfolgt und verwaltet werden, treten eher Probleme auf. Um ein erfolgreiches Ergebnis zu gewährleisten, empfehlen wir dringend, ein Projektmanagementtool zu verwenden. Es gibt viele verschiedene Tools, und Projektmanager in Ihrer Organisation haben möglicherweise bereits einen Favoriten.

Als Tool für die Projektverwaltung während einer Cloudmigration wird Azure DevOps empfohlen. Das Framework für die Cloudeinführung enthält ein Tool zur automatischen Bereitstellung einer Projektvorlage, um die Verwendung von Azure DevOps zu beschleunigen. Diese Vorlage umfasst die Aufgaben, die bei einer Migration üblicherweise ausgeführt werden. Stellen Sie die Vorlage mithilfe der Anweisungen unter [Cloudeinführungsplan und Azure DevOps](/azure/architecture/cloud-adoption/plan/template) bereit. Anschließend können Sie die Vorlage ändern, um sie auf die zu migrierenden [Workloads](/azure/architecture/cloud-adoption/plan/workloads) und [Ressourcen](/azure/architecture/cloud-adoption/plan/assets) abzustimmen.

Microsoft bietet außerdem folgende Projektverwaltungstools zur Erweiterung des Funktionsspektrums an:

- [Microsoft Planner](https://tasks.office.com): Eine einfache, visuelle Möglichkeit zum Organisieren von Teamwork.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): Projekt- und Portfolioverwaltung, Ressourcenkapazitätsverwaltung, Finanzmanagement, Timesheet- und Zeitplanverwaltung.
- [Microsoft Teams](https://products.office.com/microsoft-teams): Tool für Zusammenarbeit und Kommunikation im Team. Teams integriert auch Planner und andere Tools, um die Zusammenarbeit zu verbessern.
- [Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops?view=azure-devops): Die Planungsvorlage des Frameworks für die Cloudeinführung ist zur Verwendung von Azure DevOps nicht erforderlich. Sie können den Dienst ohne die Vorlage verwenden, um Ihre Infrastruktur als Code zu verwalten, oder die Projektverwaltung mithilfe der Arbeitselemente und Boards durchführen. Mit steigender Erfahrung können Sie die CI/CD-Funktionen nutzen.

Diese Projektmanagementtools sind nicht die einzigen verfügbaren Tools. Viele weitere Tools von Drittanbietern sind in der Projektmanagementcommunity weit verbreitet.

### <a name="set-up-for-devops"></a>Setup für DevOps

Die Migration zu Cloudtechnologien bietet eine großartige Gelegenheit, Ihre Organisation für DevOps und CI/CD einzurichten. Selbst wenn Ihre Organisation nur Infrastruktur verwaltet, können Sie, wenn Sie beginnen, Ihre Infrastruktur als Code zu verwalten und die Branchenmuster und -praktiken für DevOps zu verwenden, Ihre Agilität durch CI/CD-Pipelines erhöhen und sich so schneller an Änderungs-, Wachstums-, Release- und sogar Wiederherstellungszenarien anpassen.

Azure DevOps bietet die erforderlichen Funktionen und die Integration mit Azure, lokalen Umgebungen und sogar anderen Clouds. Weitere Informationen finden Sie unter [Azure DevOps](https://azure.microsoft.com/services/devops). Ein angeleitetes Training finden Sie unter [Schnellstart: CI/CD mit Azure DevOps](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html).

### <a name="suggested-skills"></a>Empfohlene Qualifikationen

Microsoft Learn ist ein neuer Lernansatz. Die Bereitschaft zu den neuen Qualifikationen und Aufgaben, die mit der Cloudeinführung verbunden sind, entwickeln sich nicht einfach so. Microsoft Learn bietet einen lohnenderen Ansatz für praktisches Lernen, der Ihnen hilft, Ihre Ziele schneller zu erreichen. Punkte sammeln, zu höheren Stufen aufsteigen und mehr erreichen.

Hier sehen Sie ein Beispiel für einen maßgeschneiderten Lernpfad auf Microsoft Learn, der das Setup für den DevOps-Leitfaden im Cloud Adoption Framework ergänzt.

[Erstellen von Anwendungen mit Azure DevOps:](/learn/paths/build-applications-with-azure-devops) Arbeiten Sie mit anderen zusammen, um Ihre Anwendungen mit Azure Pipelines und GitHub zu erstellen. Führen Sie in Ihrer Pipeline automatisierte Tests zum Überprüfen der Codequalität aus. Überprüfen Sie den Quellcode und die Komponenten von Drittanbietern auf potenzielle Sicherheitsrisiken. Definieren Sie mehrere Pipelines, die zusammenwirken, um Ihre Anwendung zu erstellen. Erstellen Sie Anwendungen mit von Microsoft gehosteten Agents und mit eigenen Build-Agents.

## <a name="cost-management"></a>[Kostenmanagement](#tab/ManageCost)

Bei der Migration von Ressourcen in Ihre Cloudumgebung ist es wichtig, eine regelmäßige Kostenanalyse durchzuführen. Da der Migrationsprozess zusätzliche Nutzungsanforderungen an Ihre Dienste stellen kann, können Ihnen regelmäßige Kostenanalysen dabei helfen, unerwartete Nutzungsgebühren zu vermeiden. Sie können zudem die Größe der Ressourcen nach Bedarf anpassen, um Kosten und Workload auszugleichen (weitere Details finden Sie im Abschnitt [Optimierung und Transformation](./optimize-and-transform.md)).
