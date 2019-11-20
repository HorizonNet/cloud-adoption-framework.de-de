---
title: Beschleunigen der Migration durch Migrieren einer Instanz von SQL Server
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Die Migration vollständiger SQL Server-Instanzen kann die Migration von Workloads beschleunigen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 71632e8f3f995922f4021f216f2090b742141169
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753523"
---
# <a name="accelerate-migration-by-migrating-an-instance-of-sql-server"></a>Beschleunigen der Migration durch Migrieren einer Instanz von SQL Server

Die Migration vollständiger SQL Server-Instanzen kann die Migration von Workloads beschleunigen. Die folgende Anleitung erweitert den [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) durch die Migration einer SQL Server-Instanz außerhalb eines workloadorientierten Migrationsansatzes. Dieser Ansatz kann die Migration mehrerer Workloads mit einer einzigen Datenplattformmigration einleiten. Der größte Teil des in diesem Bereich erforderlichen Aufwands entfällt auf die Voraussetzungen und die Bewertungs-, Migrations- und Optimierungsvorgänge einer Migration.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Ist dieser erweiterte Bereich für Sie geeignet?

Der im [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) empfohlene Ansatz besteht darin, jede Datenstruktur zusammen mit den zugehörigen Workloads im Rahmen einer einzelnen Migrationsbemühung zu migrieren. Der iterative Ansatz zur Migration reduziert das Erkennen, Bewerten und andere Aufgaben, die Blockaden verursachen und die Wertschöpfung im Unternehmen verlangsamen können.

Allerdings können einige Datenstrukturen durch eine separate Datenplattformmigration effektiver migriert werden. Im Folgenden finden Sie einige Beispiele:

- **Ende des Diensts:** Wenn Sie eine SQL-Server-Instanz schnell verschieben möchten, um Herausforderungen am Ende des Diensts zu vermeiden, können Sie diese Anleitung auch außerhalb der üblichen Migrationsbemühungen verwenden.
- **SQL Server-Dienste:** Die Datenstruktur ist Teil einer umfassenderen Lösung, die erfordert, dass SQL Server auf einem virtuellen Computer ausgeführt wird. Dies ist für Lösungen üblich, die SQL Server-Dienste wie SQL Server Reporting Services, SQL Server Integration Services oder SQL Server Analysis Services nutzen.
- **Datenbanken mit hoher Dichte und geringer Auslastung:** Die SQL Server-Instanz weist eine hohe Datenbankdichte auf. Jede dieser Datenbanken verfügt über niedrige Transaktionsvolumen und erfordert wenig Aufwand an Computeressourcen. Sie sollten andere, modernere Lösungen in Betracht ziehen, aber ein IaaS-Ansatz (Infrastructure-as-a-Service) kann zu erheblich geringeren Betriebskosten führen.
- **Gesamtbetriebskosten:** Gegebenenfalls können [Azure-Hybridvorteile](https://azure.microsoft.com/pricing/hybrid-benefit) auf den Listenpreis angewandt werden, sodass die niedrigsten Betriebskosten für SQL Server erzielt werden. Dies gilt insbesondere für Kunden, die SQL Server in Szenarien mit mehreren Cloudumgebungen hosten.
- **Migrationsbeschleunigung:** Bei der Migration einer SQL Server-Instanz per Lift & Shift können mehrere Datenbanken in einer Iteration verschoben werden. Dieser Ansatz ermöglicht es manchmal, sich bei zukünftigen Iterationen spezifischer auf Anwendungen und VMs zu konzentrieren, sodass Sie mehr Workloads in einer einzigen Iteration migrieren können.
- **VMware-Migration:** Eine gängige lokale Architektur umfasst Anwendungen und VMs auf einem virtuellen Host und Datenbanken auf Hardwarecomputern. In diesem Szenario können Sie ganze SQL Server-Instanzen migrieren, um Ihre Migration des VMware-Hosts zu Azure VMware Service zu unterstützen. Weitere Informationen finden Sie unter [VMware-Hostmigration](./vmware-host.md).

Wenn keines der oben genannten Kriterien für diese Migration gilt, empfiehlt es sich, mit dem [Standardmigrationsvorgang](../index.md) fortzufahren. Beim Standardvorgang werden Datenstrukturen parallel zu jeder Workload iterativ migriert.

Wenn dieses Handbuch auf Ihre Kriterien zutrifft, fahren Sie mit diesem erweiterten Bereichsleitfaden als Maßnahme innerhalb des [Standardmigrationsprozesses](../index.md) fort. Während der Voraussetzungsphase kann der Aufwand in den allgemeinen Cloudeinführungsplan integriert werden.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Bevor Sie eine SQL Server-Migration durchführen, beginnen Sie mit einer Erweiterung der digitalen Ressourcen, indem Sie eine Datenressource einbeziehen. Die Datenressource zeichnet den Bestand der Datenobjekte auf, die Sie für die Migration in Erwägung ziehen. In den folgenden Tabellen wird ein Ansatz zum Aufzeichnen der Datenressource erläutert.

### <a name="server-inventory"></a>Serverbestand

Im Folgenden finden Sie ein Beispiel für einen Serverbestand:

|SQL Server|Zweck|Version|[Wichtigkeit](../../manage/considerations/criticality.md)|[Vertraulichkeit](../../govern/policy-compliance/data-classification.md)|Anzahl von Datenbanken|SSIS|SSRS|SSAS|Cluster|Anzahl von Knoten|
|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|sql-01|Kern-Apps|2016|Unternehmenskritisch|Streng vertraulich|40|–|–|–|Ja|3|
|sql-02|Kern-Apps|2016|Unternehmenskritisch|Streng vertraulich|40|–|–|–|Ja|3|
|sql-03|Kern-Apps|2016|Unternehmenskritisch|Streng vertraulich|40|–|–|–|Ja|3|
|sql-04|BI|2012|Hoch|XX|6|–|Vertraulich|Ja, mehrdimensionaler Cube|Nein|1|
|sql-05|Integration|2008 R2|Niedrig|Allgemein|20|Ja|–|–|Nein|1|

### <a name="database-inventory"></a>Datenbankbestand

Im Folgenden finden Sie ein Beispiel für einen Datenbankbestand für einen der oben aufgeführten Server:

|Server|Datenbank|[Wichtigkeit](../../manage/considerations/criticality.md)|[Vertraulichkeit](../../govern/policy-compliance/data-classification.md)|DMA-Ergebnisse (Datenmigrations-Assistent)|DMA-Wartung|Zielplattform|
|---------|---------|---------|---------|---------|---------|---------|
|sql-01|DB-1|Unternehmenskritisch|Streng vertraulich|Kompatibel|–|Azure SQL-Datenbank|
|sql-01|DB-2|Hoch|Vertraulich|Schemaänderung erforderlich|Implementierte Änderungen|Azure SQL-Datenbank|
|sql-01|DB-1|Hoch|Allgemein|Kompatibel|–|Verwaltete Azure SQL-Instanz|
|sql-01|DB-1|Niedrig|Streng vertraulich|Schemaänderung erforderlich|Geplante Änderungen|Verwaltete Azure SQL-Instanz|
|sql-01|DB-1|Unternehmenskritisch|Allgemein|Kompatibel|–|Verwaltete Azure SQL-Instanz|
|sql-01|DB-2|Hoch|Vertraulich|Kompatibel|–|Azure SQL-Datenbank|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integration in den Cloud Adoption-Plan

Nach Abschluss dieses Erkennungsvorgangs können Sie ihn in den [Cloudeinführungsplan](../../plan/template.md) einschließen. Fügen Sie innerhalb des Cloud Adoption-Plans jede zu migrierende SQL Server-Instanz als [individuelle Workload](../../plan/workloads.md) hinzu. In jeder Workload können die einzelnen Datenbanken und Dienste (SSIS, SSAS, SSRS) als [Ressourcen](../../plan/workloads.md) hinzugefügt werden. Um Workloads und Ressourcen in den Cloud Adoption-Plan durch Massenhinzufügen einzubinden, lesen Sie [Hinzufügen und Bearbeiten von Arbeitselementen mit Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Nachdem die Workloads und Ressourcen in den Plan aufgenommen wurden, können Sie und Ihr Team mit einem Standardmigrationsvorgang gemäß dem Einführungsplan fortfahren. Wenn das Cloudeinführungsteam zu den Bewertungs-, Migrations- und Optimierungsvorgängen übergeht, berücksichtigen Sie die Änderungen, die in den folgenden Abschnitten erläutert werden.

## <a name="assessment-process-changes"></a>Änderungen am Bewertungsprozess

Wenn eine Datenbank im Plan zu einer PaaS-Datenplattform (Platform as a Service) migriert werden kann, bewerten Sie die Kompatibilität der ausgewählten Datenbank mit dem DMA. Wenn die Datenbank Schemakonvertierungen erfordert, sollten Sie diese im Rahmen des Bewertungsvorgangs abschließen, um Unterbrechungen der Migrationspipeline zu vermeiden.

### <a name="suggested-action-during-the-assessment-process"></a>Empfohlene Aktion während des Bewertungsprozesses

Für Datenbanken, die zu einer PaaS-Lösung migriert werden können, werden während des Bewertungsvorgangs die folgenden Aktionen durchgeführt.

- **Bewertung durch den DMA:** Der Datenmigrations-Assistent erkennt Kompatibilitätsprobleme, die die Datenbankfunktion in der verwalteten Azure SQL-Datenbank-Zielinstanz beeinträchtigen können. Verwenden Sie den DMA für Empfehlungen zu Leistungs- und Zuverlässigkeitsverbesserungen und zum Verschieben des Schemas, der Daten und abhängiger Objekte vom Quellserver auf den Zielserver. Weitere Informationen finden Sie unter [Datenmigrations-Assistent](https://docs.microsoft.com/sql/dma/dma-overview).
- **Korrektur und Konvertierung:** Konvertieren Sie basierend auf der Ausgabe des DMA das Quelldatenschema, um Kompatibilitätsprobleme zu korrigieren. Testen Sie das konvertierte Datenschema mit den abhängigen Anwendungen.

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Bei der Migration können Sie zwischen vielen verschiedenen Tools und Ansätzen auswählen. Aber jeder Ansatz folgt einem einfachen Prozess: Migrieren von Schema, Daten und Objekten. Synchronisieren Sie dann Daten mit der Zieldatenquelle.

Durch das Ziel und die Quelle der Datenstruktur und der Dienste können diese beiden Schritte recht kompliziert werden. In den folgenden Abschnitten finden Sie Informationen zur optimalen Auswahl von Tools basierend auf Ihren Migrationsentscheidungen.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

Der empfohlene Pfad für Migration und Synchronisierung verwendet eine Kombination der folgenden drei Tools. In den folgenden Abschnitten werden komplexere Migrations- und Synchronisierungsoptionen erläutert, die eine breitere Palette von Ziel- und Quelllösungen ermöglichen.

|Migrationsoption|Zweck|
|---------|---------|
|[Azure Database Migration Service](https://docs.microsoft.com/sql/dma/dma-overview)|Unterstützt Migrationsvorgänge in jeder Größenordnung online (minimale Ausfallzeit) und offline (einmalig) zu einer verwalteten Azure SQL-Datenbank-Instanz. Unterstützt Migrationsvorgänge von: SQL Server 2005, SQL Server 2008 und SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 und SQL Server 2017.|
|[Transaktionsreplikation](https://docs.microsoft.com/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Transaktionsreplikation in eine verwaltete Azure SQL-Datenbank-Instanz wird unterstützt für Migrationen von: SQL Server 2012 (SP2 CU8, SP3 oder höher), SQL Server 2014 (RTM CU10 oder höher oder SP1 CU3 oder höher), SQL Server 2016, SQL Server 2017.|
|[Massenladen](https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql)|Verwenden Sie das Massenladen in eine verwaltete Azure SQL-Datenbank-Instanz für Daten, die in folgenden Umgebungen gespeichert sind: SQL Server 2005, SQL Server 2008 und SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 und SQL Server 2017.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Anleitungen und Tutorials für den empfohlenen Migrationsprozess

Die Entscheidung für die beste Anleitung zur Migration mit Azure Database Migration Service ist von Ihrer ausgewählten Quell- und Zielplattform abhängig. Die folgende Tabelle enthält Links zu Tutorials für die einzelnen Standardansätze zum Migrieren einer SQL-Datenbank mithilfe von Azure Database Migration Service:

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL-Datenbank|Database Migration Service|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL-Datenbank|Database Migration Service|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Azure SQL-Datenbank – Verwaltete Instanz|Database Migration Service|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Azure SQL-Datenbank – Verwaltete Instanz|Database Migration Service|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS SQL Server|Azure SQL-Datenbank (oder verwaltete Instanz)|Database Migration Service|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Anleitungen und Tutorials für verschiedene Dienste für äquivalente PaaS-Lösungen

Nach dem Verschieben von Datenbanken von einer SQL Server-Instanz in Azure Database Migration Service können das Schema und die Daten in verschiedenen PaaS-Lösungen erneut gehostet werden. Andere erforderliche Dienste werden jedoch möglicherweise weiterhin auf diesem Server ausgeführt. Die folgenden drei Tutorials unterstützen Sie beim Verschieben von SSIS, SSAS und SSRS in entsprechende PaaS-Dienste in Azure.

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|SQL Server Integration Services|Azure Data Factory-Integration Runtime|Azure Data Factory|Offline|[Tutorial](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Services – Tabellenmodell|Azure Analysis Services|SQL Server Data Tools|Offline|[Tutorial](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|SQL Server Reporting Services|Power BI-Berichtsserver|Power BI|Offline|[Tutorial](https://docs.microsoft.com/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Anleitungen und Tutorials für die Migration von SQL Server zu einer IaaS-Instanz von SQL Server

Nach dem Migrieren von Datenbanken und Diensten zu PaaS-Instanzen können noch Datenstrukturen und -dienste vorhanden sein, die nicht PaaS-kompatibel sind. Wenn vorhandene Einschränkungen die Migration von Datenstrukturen oder-Diensten verhindern, kann Sie das folgende Tutorial bei der Migration verschiedener Ressourcen im Datenportfolio zu Azure-IaaS-Lösungen unterstützen.

Verwenden Sie diesen Ansatz zum Migrieren von Datenbanken oder anderen Diensten auf der SQL Server-Instanz.

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|Einzelne Instanz von SQL Server|SQL Server unter IaaS|Verschiedene|Offline|[Tutorial](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Änderungen im Optimierungsprozess

Während der Optimierung können Sie jede Datenstruktur, jeden Dienst und jede SQL Server-Instanz testen, optimieren und in die Produktion hochstufen. Dies ist die größte Auswirkung im Gegensatz zu einem Migrationsmodell pro Workload.

Im Idealfall migrieren Sie die abhängigen Workloads, Anwendungen und VMs innerhalb derselben Iteration wie die SQL Server-Instanz. Wenn dieses Idealszenario eintritt, kann die Workload zusammen mit der Datenquelle getestet werden. Nach dem Testen können Sie die Datenstruktur in die Produktion höherstufen und den Synchronisierungsprozess beenden.

Betrachten wir nun das Szenario, in dem zwischen der Datenbankmigration und der Workloadmigration ein erheblicher Zeitabstand besteht. Dies kann leider die größte Änderung am Optimierungsvorgang während einer nicht workloadgesteuerten Migration darstellen. Wenn Sie mehrere Datenbanken im Rahmen einer SQL Server-Migration migrieren, können diese Datenbanken für mehrere Iterationen sowohl in der Cloud als auch lokal parallel vorhanden sein. Während dieses Zeitraums müssen Sie die Datensynchronisierung beibehalten, bis diese abhängigen Ressourcen migriert, getestet und höhergestuft wurden.

Bis alle abhängigen Workloads höhergestuft wurden, sind Sie und Ihr Team für die Unterstützung der Synchronisierung von Daten zwischen Quellsystem und Zielsystem verantwortlich. Diese Synchronisierung beansprucht Netzwerkbandbreite und vor allem Zeit der Benutzer und verursacht Cloudkosten. Durch die ordnungsgemäße Abstimmung des Cloudeinführungsplans für die SQL Server-Migrationsworkload und alle abhängigen Workloads und Anwendungen kann dieser kostenintensive Mehraufwand verringert werden.

### <a name="suggested-action-during-the-optimization-process"></a>Empfohlene Aktion während des Optimierungsvorgangs

Schließen Sie während der Optimierungsvorgänge die folgenden Aufgaben in allen Iterationen ab, bis alle Datenstrukturen und Dienste in die Produktionsumgebung hochgestuft wurden.

1. Überprüfen Sie die Synchronisierung von Daten.
2. Testen Sie alle migrierten Anwendungen.
3. Optimieren Sie die Anwendungs- und Datenstruktur, um Kosten zu optimieren.
4. Stufen Sie die Anwendungen höher in die Produktion.
5. Testen Sie auf fortgesetzten lokalen Datenverkehr für die lokale Datenbank.
6. Beenden Sie die Synchronisierung von Daten, die in die Produktion höhergestuft werden.
7. Beenden Sie die ursprüngliche Quelldatenbank.

Bevor Schritt 5 nicht abgeschlossen ist, können Sie Datenbanken und die Synchronisierung nicht beenden. Bis alle Datenbanken in einer SQL Server-Instanz alle sieben Schritte durchlaufen haben, sollten Sie die lokale Instanz von SQL Server als Produktionsumgebung behandeln. Alle Synchronisierungsvorgänge sollten beibehalten werden.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur [Checkliste für erweiterten Umfang](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
