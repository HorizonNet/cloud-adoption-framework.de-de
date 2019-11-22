---
title: Migrieren von Objekten
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrieren von Objekten
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7e464b93dd9cc46526ab5f72bd8cf4fbf15f31f3
ms.sourcegitcommit: 3655aa7f3e80249e0b2b562cd40dd750afc82043
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2019
ms.locfileid: "74251817"
---
# <a name="migrate-assets-infrastructure-apps-and-data"></a>Migrieren von Objekten (Infrastruktur, Apps und Daten)

In dieser Phase verwenden Sie die Ausgabe der Bewertungsphase, um die Migration der Umgebung einzuleiten. Dieser Leitfaden hilft Ihnen, die geeigneten Tools zu identifizieren, um den Zustand "Fertig" zu erreichen, einschließlich nativer Tools, Tools von Drittanbietern und Projektmanagementtools.

<!-- markdownlint-disable MD025 -->

# <a name="native-migration-toolstabtools"></a>[Native Migrationstools](#tab/Tools)

In den folgenden Abschnitten werden die nativen Azure-Tools beschrieben, die zur Durchführung oder Unterstützung der Migration zur Verfügung stehen. Informationen zur Auswahl der richtigen Tools zur Unterstützung Ihrer Migrationsbemühungen finden Sie im [Leitfaden zur Entscheidungsfindung für Migrationstools des Frameworks für die Cloudeinführung (Cloud Adoption Framework)](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Mit Azure Migrate wird eine vereinheitlichte und erweiterbare Migrationsumgebung bereitgestellt. Azure Migrate bietet eine zentrale dedizierte Umgebung, mit der Sie Ihre Migration über die Phasen der Bewertung und Migration nach Azure verfolgen können. Azure Migrate ermöglicht Ihnen, die Tools Ihrer Wahl zu verwenden und den Fortschritt der Migration über diese Tools hinweg zu verfolgen.

Azure Migrate bietet die folgenden Funktionen:

1. Erweiterte Bewertungs- und Migrationsfunktionen:
    - Hyper-V-Bewertungen.
    - Verbesserte VMware-Bewertung.
    - Migration ohne Agents Ihrer virtuellen VMware-Computer zu Azure.
1. Einheitliche Bewertung, Migration und Fortschrittsverfolgung.
1. Erweiterbarer Ansatz mit ISV-Integration (z. B. Cloudamize).

Führen Sie die folgenden Schritte aus, um eine Migration mit Azure Migrate durchzuführen:

1. Suchen Sie unter **Alle Dienste** nach Azure Migrate. Wählen Sie **Azure Migrate** aus, um den Vorgang fortzusetzen.
1. Wählen Sie **Tool hinzufügen**, um Ihr Migrationsprojekt zu starten.
1. Wählen Sie das Abonnement, die Ressourcengruppe und die Geografie aus, für die die Migration durchgeführt werden soll.
1. Wählen Sie **Bewertungstool auswählen** > **Azure Migrate: Serverbewertung** >  **Weiter** aus.
1. Wählen Sie **Überprüfen + Tools hinzufügen** aus, und überprüfen Sie die Konfiguration. Klicken Sie auf **Tools hinzufügen**, um den Auftrag zur Erstellung des Migrationsprojekts und zur Registrierung der ausgewählten Lösungen zu initiieren.

<!-- TODO: TBA -->

### <a name="learn-more"></a>Weitere Informationen

- [Azure Migrate-Tutorial: Migrieren von physischen oder virtualisierten Servern zu Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)

## <a name="azure-site-recovery"></a>Azure Site Recovery

Mit dem Azure Site Recovery-Dienst können Sie die Migration lokaler Ressourcen nach Azure verwalten. Außerdem können Sie mit Azure Site Recovery die Notfallwiederherstellung von lokalen Computern und Azure-VMs zwecks Business Continuity und Disaster Recovery (BCDR) verwalten und orchestrieren.

Die folgenden Schritte beschreiben, wie Sie Site Recovery zur Migration verwenden:

> [!TIP]
> Abhängig von Ihrem Szenario können sich diese Schritte leicht unterscheiden. Weitere Informationen finden Sie im Artikel [Migrieren von lokalen Computern zu Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure).

### <a name="prepare-azure-site-recovery-service"></a>Vorbereiten des Azure Site Recovery-Diensts

1. Wählen Sie im Azure-Portal **+ Ressource erstellen > Verwaltungstools > Backup und Site Recovery** aus.
1. Wenn Sie noch keinen Wiederherstellungstresor erstellt haben, schließen Sie den Assistenten ab, um eine Ressource **Recovery Services-Tresor** zu erstellen.
1. Wählen Sie im Menü **Ressource** **Site Recovery > Infrastruktur vorbereiten > Schutzziel** aus.
1. Wählen Sie in **Schutzziel** aus, was Sie migrieren möchten.
    1. **VMware:** Wählen Sie die Option **Zu Azure > Ja, mit VMware vSphere-Hypervisor** aus.
    1. **Physischer Computer:** Wählen Sie **Zu Azure > Nicht virtualisiert/Andere** aus.
    1. **Hyper-V:** Wählen Sie **Zu Azure > Ja, mit Hyper-V** aus. Wenn Hyper-V-VMs von VMM verwaltet werden, wählen Sie **Ja** aus.

### <a name="configure-migration-settings"></a>Konfigurieren von Migrationseinstellungen

1. Richten Sie bei Bedarf die Quellumgebung ein.
1. Richten Sie die Zielumgebung ein.
    1. Klicken Sie auf **Infrastruktur vorbereiten > Ziel**, und wählen Sie das gewünschte Azure-Abonnement aus.
    1. Geben Sie das Ressourcen-Manager-Bereitstellungsmodell an.
    1. Site Recovery prüft, ob Sie über ein oder mehrere kompatible Azure-Speicherkonten und -Netzwerke verfügen.
1. Richten Sie eine Replikationsrichtlinie ein.
1. Aktivieren Sie die Replikation.
1. Führen Sie eine Testmigration (Testfailover) aus.

### <a name="migrate-to-azure-using-failover"></a>Migrieren zu Azure mit Failover

1. Wählen Sie in **Einstellungen > Replizierte Elemente** den Computer und dann auf **Failover** aus.
1. Wählen Sie in **Failover** einen **Wiederherstellungspunkt** für das Failover aus. Wählen Sie den letzten Wiederherstellungspunkt aus.
1. Konfigurieren Sie alle Einstellungen für Verschlüsselungsschlüssel nach Bedarf.
1. Wählen Sie **Computer vor Beginn des Failovers herunterfahren** aus. Site Recovery versucht, virtuelle Computer herunterzufahren, bevor das Failover ausgelöst wird. Das Failover wird auch dann fortgesetzt, wenn das Herunterfahren nicht erfolgreich ist. Der Fortschritt des Failovers wird auf der Seite „Aufträge“ angezeigt.
1. Überprüfen Sie, ob die Azure-VM wie erwartet in Azure angezeigt wird.
1. Klicken Sie unter **Replizierte Elemente** mit der rechten Maustaste auf die VM, und wählen Sie dann **Migration abschließen** aus.
1. Führen Sie alle Schritte nach der Migration nach Bedarf aus (relevante Informationen finden Sie in diesem Handbuch).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.RecoveryServices]" submitText="Create a Recovery Services vault" :::

::: zone-end

::: zone target="docs"

Weitere Informationen finden Sie unter

- [Migrieren von lokalen Computern zu Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure)

::: zone-end

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service ist ein vollständig verwalteter Dienst, der die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen mit minimaler Ausfallzeit ermöglicht (Onlinemigrationen). Azure Database Migration Service führt alle erforderlichen Schritte durch. Sie können Ihre Migrationsprojekte mit der Gewissheit initiieren, dass die Migration unter Verwendung der von Microsoft empfohlenen bewährten Methoden erfolgt.

### <a name="create-an-azure-database-migration-service-instance"></a>Erstellen einer Instanz von Azure Database Migration Service

Wenn Sie Azure Database Migration Service zum ersten Mal verwenden, müssen Sie den Ressourcenanbieter für Ihr Azure-Abonnement registrieren:

1. Wählen Sie **Alle Dienste**, anschließend **Abonnements** und dann das Zielabonnement aus.
1. Wählen Sie **Ressourcenanbieter** aus.
1. Suchen Sie nach `migration`, und wählen Sie rechts neben **Microsoft.DataMigration** die Option **Registrieren** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

Nach der Registrierung des Ressourcenanbieters können Sie eine Azure Database Migration Service-Instanz erstellen.

1. Wählen Sie **+ Ressource erstellen** aus, und suchen Sie im Marketplace nach **Azure Database Migration Service**.
1. Schließen Sie den Assistenten **Migrationsdienst erstellen** ab, und wählen Sie **Erstellen** aus.

Der Dienst ist nun bereit, die unterstützten Quelldatenbanken (z.B. SQL Server, MySQL, PostgreSQL oder MongoDb) zu migrieren.

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Weitere Informationen finden Sie unter

- [Übersicht über Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview)
- [Erstellen einer Instanz von Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal)
- [Azure Migrate im Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade)
- [Azure-Portal: Erstellen eines Migrationsprojekts](https://portal.azure.com/#create/Microsoft.AzureMigrate)

::: zone-end

## <a name="data-migration-assistant"></a>Datenmigrations-Assistent

Der Datenmigrations-Assistent (DMA) hilft Ihnen beim Upgrade auf eine moderne Datenplattform, indem er Kompatibilitätsprobleme erkennt, die die Datenbankfunktionalität in Ihrer neuen Version von SQL Server oder Microsoft Azure SQL-Datenbank beeinträchtigen können. DMA empfiehlt Leistungs- und Zuverlässigkeitsverbesserungen für Ihre Zielumgebung und ermöglicht es Ihnen, Ihr Schema, Ihre Daten und abhängige Objekte vom Quellserver auf Ihren Zielserver zu verschieben.

> [!NOTE]
> Für große Migrationen (in Bezug auf Anzahl und Größe der Datenbanken) empfehlen wir Ihnen, Azure Database Migration Service zu verwenden, mit dem Datenbanken im großen Maßstab migriert werden können.
>

Um den Datenmigrations-Assistenten zu verwenden, führen Sie zunächst folgende Schritte aus.

1. Laden Sie den Datenmigrations-Assistenten aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595), herunter und installieren Sie ihn.
1. Erstellen Sie eine Bewertung, indem Sie auf das Symbol **Neu (+)** klicken und den Projekttyp **Bewertung** auswählen.
1. Legen Sie den Typ von Quell- und Zielserver fest. Klicken Sie auf **Create**.
1. Konfigurieren Sie die Bewertungsoptionen nach Bedarf (empfohlen werden die Standardwerte).
1. Fügen Sie die Datenbanken zur Bewertung hinzu.
1. Klicken Sie auf **Weiter**, um die Bewertung zu starten.
1. Zeigen Sie die Ergebnisse im Data Migration Assistant-Toolset an.

Unternehmen empfehlen wir, dem unter [Bewerten eines Unternehmens und Konsolidieren der Bewertungsberichte mit DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports) beschriebenen Ansatz zu folgen, um mehrere Server zu bewerten, die Berichte zu kombinieren und dann die bereitgestellten Power BI-Berichte zur Analyse der Ergebnisse zu verwenden.

Weitere Informationen und ausführliche Verwendungsschritte finden Sie unter:

- [Übersicht über den Datenmigrations-Assistenten](https://docs.microsoft.com/sql/dma/dma-overview)
- [Bewerten eines Unternehmens und Konsolidieren der Bewertungsberichte mit DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports)
- [Analysieren der vom Datenmigrations-Assistenten erstellten konsolidierten Bewertungsberichte mit Power BI](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport)

## <a name="sql-server-migration-assistant"></a>SQL Server Migration Assistant

Microsoft SQL Server Migration Assistant (SSMA) ist ein Tool zur Automatisierung der Datenbankmigration von Microsoft Access, DB2, MySQL, Oracle und SAP ASE zu SQL Server. Das allgemeine Konzept besteht in der Erfassung, Bewertung und Überprüfung mit diesen Tools. Aufgrund der unterschiedlichen Prozesse für die einzelnen Quellsysteme empfehlen wir Ihnen, die detaillierte [Dokumentation zu SQL Server Migration Assistant](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant) zu lesen.

Weitere Informationen finden Sie unter

- [Übersicht über SQL Server Migration Assistant](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant)

## <a name="database-experimentation-assistant"></a>Assistent für Datenbankexperimente

Der Assistent für Datenbankexperimente (DEA) ist eine neue A/B-Testlösung für SQL Server-Upgrades. Er hilft bei der Evaluierung einer Zielversion von SQL für eine bestimmte Workload. Kunden, die ein Upgrade von einer früheren SQL Server-Version (SQL Server 2005 und höher) auf eine neue Version von SQL Server ausführen, können diese Analysemetriken verwenden.

Der Assistent für Datenbankexperimente enthält die folgenden Workflowaktivitäten:

- **Erfassen**: Der erste Schritt des SQL Server-A/B-Tests ist die Erfassung einer Ablaufverfolgung auf Ihrem Quellserver. Der Quellserver ist normalerweise der Produktionsserver.
- **Wiedergeben**: Im zweiten Schritt des SQL Server-A/B-Tests wird die erfasste Ablaufverfolgungsdatei auf Ihren Zielservern wiedergegeben. Anschließend werden umfangreiche Ablaufverfolgungen aus den Wiedergaben zur Analyse gesammelt.
- **Analyse**: Der letzte Schritt besteht darin, einen Analysebericht unter Verwendung der Wiedergabeablaufverfolgungen zu generieren. Anhand des Analyseberichts erhalten Sie wertvolle Einblicke in die Auswirkungen der vorgeschlagenen Änderung auf die Leistung.

Weitere Informationen finden Sie unter

- [Übersicht über den Assistenten für Datenbankexperimente](https://docs.microsoft.com/sql/dea/database-experimentation-assistant-overview)

## <a name="cosmos-db-data-migration-tool"></a>Datenmigrationstool von Cosmos DB

Das Datenmigrationstool von Azure Cosmos DB kann Daten aus verschiedenen Quellen in Azure Cosmos DB-Sammlungen und -Tabellen importieren. Sie können Daten aus JSON-Dateien, CSV-Dateien, SQL-, MongoDB-, Azure Table Storage-, Amazon DynamoDB- und sogar Azure Cosmos DB-SQL-API-Sammlungen importieren. Das Datenmigrationstool kann auch für die Migration von einer Sammlung mit einer einzelnen Partition zu einer Sammlung mit mehreren Partitionen für die SQL-API verwendet werden.

Weitere Informationen finden Sie unter

- [Migrieren Ihrer Daten zu Azure Cosmos DB mithilfe des Datenmigrationstools](https://docs.microsoft.com/azure/cosmos-db/import-data)

<!-- markdownlint-disable MD025 -->

# <a name="third-party-migration-toolstabthird-party-tools"></a>[Migrationstool von einem Drittanbieter](#tab/third-party-tools)

Verschiedene Migrationstools von Drittanbietern und ISV-Dienste können während der Migration hilfreich sein. Alle bieten unterschiedliche Vorteile und Stärken. Zu diesen Tools zählen:

## <a name="cloudamize"></a>Cloudamize

Cloudamize ist ein ISV-Dienst, der alle Phasen der Migrationsstrategie abdeckt.

[Weitere Informationen](https://www.cloudamize.com)

## <a name="zerto"></a>Zerto

Zerto stellt virtuelle Replikationsverarbeitung in Microsoft Hyper-V- und VMware vSphere-Umgebungen bereit.

[Weitere Informationen](https://www.zerto.com/solutions/use-cases/data-center-migration-software)

## <a name="carbonite"></a>Carbonite

Carbonite bietet Server- und Datenmigrationslösungen zur Migration von Workloads zu, von oder zwischen physischen, virtuellen oder cloudbasierten Umgebungen.

[Weitere Informationen](https://www.carbonite.com/data-protection/data-migration-software)

## <a name="movere"></a>Movere

Movere ist eine Ermittlungslösung, die die notwendigen Daten und Erkenntnisse liefert, um Cloudmigrationen zu planen und IT-Umgebungen kontinuierlich und zuverlässig zu optimieren, zu überwachen und zu analysieren.

[Weitere Informationen](https://www.movere.io)

## <a name="cosmos-db-partners"></a>Cosmos DB-Partner

Sie können aus einer Vielzahl erfahrener Systemintegratorpartner und Tools wählen, die Sie bei Ihren Azure Cosmos DB-Migrationen für Ihre NoSQL-Datenbankanforderungen unterstützen.

[Weitere Informationen](https://docs.microsoft.com/azure/cosmos-db/partners-migration-cosmosdb#migration-tools)

Besuchen Sie das [Azure Migration Center](https://azure.microsoft.com/migration/support), um Organisationen zu ermitteln, die verwendungsbereite Partnertechnologielösungen anbieten, die zu Ihren Migrationsszenarien passen, und erfahren Sie mehr über zusätzliche Migrationstools und Supportdienste von Drittanbietern.

Im [Leitfaden zur Azure-Datenbankmigration](https://datamigration.microsoft.com) finden Sie Informationen zu verschiedenen Datenbankmigrationsoptionen sowie Schritt-für-Schritt-Anleitungen für native Tools und Partner.

# <a name="project-management-toolstabproject-management-tools"></a>[Projektmanagementtools](#tab/project-management-tools)

Bei Projekten, die nicht nachverfolgt und verwaltet werden, treten eher Probleme auf. Um ein erfolgreiches Ergebnis zu gewährleisten, empfehlen wir dringend, ein Projektmanagementtool zu verwenden. Es gibt viele verschiedene Tools, und Projektmanager in Ihrer Organisation haben möglicherweise bereits einen Favoriten.

Als Tool für die Projektverwaltung während einer Cloudmigration wird Azure DevOps empfohlen. Das Framework für die Cloudeinführung enthält ein Tool zur automatischen Bereitstellung einer Projektvorlage, um die Verwendung von Azure DevOps zu beschleunigen. Diese Vorlage umfasst die Aufgaben, die bei einer Migration üblicherweise ausgeführt werden. Stellen Sie die Vorlage wie [hier](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/template) beschrieben bereit. Anschließend können Sie die Vorlage ändern, um sie auf die zu migrierenden [Workloads](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/workloads) und [Ressourcen](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/assets) abzustimmen.

Microsoft bietet außerdem folgende Projektverwaltungstools zur Erweiterung des Funktionsspektrums an:

- [Microsoft Planner](https://tasks.office.com): Eine einfache, visuelle Möglichkeit zum Organisieren von Teamwork.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): Projekt- und Portfolioverwaltung, Ressourcenkapazitätsverwaltung, Finanzmanagement, Timesheet- und Zeitplanverwaltung.
- [Microsoft Teams](https://products.office.com/microsoft-teams): Tool für Zusammenarbeit und Kommunikation im Team. Teams integriert auch Planner und andere Tools, um die Zusammenarbeit zu verbessern.
- [Azure DevOps](https://dev.azure.com): Die Planungsvorlage des Frameworks für die Cloudeinführung ist zur Verwendung von Azure DevOps nicht erforderlich. Sie können den Dienst ohne die Vorlage verwenden, um Ihre Infrastruktur als Code zu verwalten, oder die Projektverwaltung mithilfe der Arbeitselemente und Boards durchführen. Mit steigender Erfahrung können Sie die CI/CD-Funktionen nutzen.

Dies sind nicht die einzigen verfügbaren Tools. Viele weitere Tools von Drittanbietern sind in der Projektmanagementcommunity weit verbreitet.

## <a name="set-up-for-devops"></a>Setup für DevOps

Die Migration in Cloudtechnologien bietet eine großartige Gelegenheit, Ihre Organisation für DevOps und CI/CD einzurichten. Selbst wenn Ihre Organisation nur Infrastruktur verwaltet, können Sie, wenn Sie beginnen, Ihre Infrastruktur als Code zu verwalten und die Branchenmuster und -praktiken für DevOps zu verwenden, Ihre Agilität durch CI/CD-Pipelines erhöhen und sich so schneller an Änderungs-, Wachstums-, Release- und sogar Wiederherstellungszenarien anpassen.

Azure DevOps bietet alle erforderlichen Funktionen und die Integration mit Azure, lokalen Umgebungen und sogar anderen Clouds. Weitere Informationen finden Sie unter [Azure DevOps](https://azure.microsoft.com/services/devops). Ein angeleitetes Training finden Sie unter [CI- und CD mit Azure DevOps – Schnellstart](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html).

# <a name="cost-managementtabmanagecost"></a>[Kostenmanagement](#tab/ManageCost)

Bei der Migration von Ressourcen in Ihre Cloudumgebung ist es wichtig, eine regelmäßige Kostenanalyse durchzuführen. Dadurch können Sie unerwartete Nutzungsgebühren vermeiden, denn der Migrationsprozess stellt möglicherweise zusätzliche Nutzungsanforderungen an Ihre Dienste. Sie können zudem die Größe der Ressourcen nach Bedarf anpassen, um Kosten und Workload auszugleichen (weitere Details finden Sie im Abschnitt **[Optimierung und Transformation](./optimize-and-transform.md)** ).
