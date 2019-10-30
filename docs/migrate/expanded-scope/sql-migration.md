---
title: Beschleunigen der Migration durch eine SQL-Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beschleunigen der Migration durch eine SQL-Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4af94af91874ac666f45a917eed003b3cf881c51
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558612"
---
# <a name="accelerate-migration-with-a-sql-migration"></a>Beschleunigen der Migration durch eine SQL-Migration

Die Migration vollständiger SQL Server-Instanzen kann die Migration von Workloads beschleunigen. Der folgende Leitfaden erweitert den [Azure-Migrationsleitfaden](../azure-migration-guide/index.md) durch die Migration einer SQL Server-Instanz außerhalb eines workloadorientierten Migrationsansatzes. Dieser Ansatz kann die Migration mehrerer Workloads mit einer einzigen Datenplattformmigration einleiten.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Der größte Teil des in diesem Bereich erforderlichen Aufwands entfällt auf die Voraussetzungen, Bewertungs-, Migrations- und Optimierungsprozesse einer Migration.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Ist dieser erweiterte Bereich für Sie geeignet?

Der empfohlene Ansatz, der im [Azure-Migrationsleitfaden](../azure-migration-guide/index.md) beschrieben wird, besteht darin, jede Datenstruktur zusammen mit den zugehörigen Workloads im Rahmen einer einzelnen Migrationsanstrengung zu migrieren. Der iterative Ansatz zur Migration reduziert das Erkennen, Bewerten und andere Aufgaben, die Blockaden verursachen und die Wertschöpfung im Unternehmen verlangsamen können.

Allerdings können einige Datenstrukturen durch eine separate Datenplattformmigration effektiver migriert werden. Im Folgenden finden Sie einige Beispiele, die zur Verwendung dieses erweiterten Bereichsleitfadens führen können:

- **Ende des Diensts:** Wenn Sie eine SQL-Server-Instanz schnell verschieben möchten, um Herausforderungen am Ende des Diensts zu vermeiden, kann es gerechtfertigt sein, diesen Leitfaden außerhalb der üblichen Migrationsbemühungen zu verwenden.
- **SQL Server-Dienste:** Die Datenstruktur ist Teil einer umfassenderen Lösung, die erfordert, dass SQL Server auf einem virtuellen Computer ausgeführt wird. Dies ist für Lösungen üblich, die SQL Server-Dienste wie SQL Server Reporting Services, SQL Server Integration Services oder SQL Server Analysis Services nutzen.
- **Datenbanken mit hoher Dichte und geringer Auslastung:** Die SQL Server-Instanz verfügt über eine hohe Datenbankdichte. Jede dieser Datenbanken verfügt über niedrige Transaktionsvolumen und erfordert wenig Computeressourcen. Weitere moderne Lösungen sollten berücksichtigt werden, aber ein IaaS-Ansatz kann zu erheblich geringeren Betriebskosten führen.
- **Gesamtbetriebskosten:** Wenn zutreffend, können [Azure-Hybridvorteile](https://azure.microsoft.com/pricing/hybrid-benefit) auf den Listenpreis angewendet werden, wodurch die niedrigsten Betriebskosten für SQL Server erzielt werden. Dies gilt insbesondere für Kunden, die SQL Server in Szenarien mit mehreren Cloudumgebungen hosten.
- **Migrationsbeschleunigung:** Die Migration durch Verlagerung einer SQL Server-Instanz kann mehrere Datenbanken in einer Iterationen verschieben. Dieser Ansatz ermöglicht es manchmal, dass sich zukünftige Iterationen spezifischer auf Anwendungen und VMs konzentrieren und mehr Workloads in einer einzigen Iteration migriert werden.
- **VMware-Migration:** Eine gängige lokale Architektur umfasst Anwendungen und VMs auf einem virtuellen Host und Datenbanken auf Bare-Metal-Computern. Wenn Sie diese gängige Architektur migrieren, kann die Migration des VMware-Hosts zu Azure VMware Service (AVS) durch diesen Leitfaden ergänzt werden, um vollständige SQL Server-Instanzen zur Unterstützung dieser virtuellen Hosts zu migrieren. Einen ergänzenden Leitfaden finden Sie unter [VMware-Hostmigration](./vmware-host.md).

Wenn keines der oben genannten Kriterien für diese Migration gilt, empfiehlt es sich, mit dem [Standardmigrationsprozess](../index.md) fortzufahren. Im Standardprozess werden Datenstrukturen parallel zu jeder Workload iterativ migriert.

Wenn dieses Handbuch auf Ihre Kriterien zutrifft, fahren Sie mit diesem erweiterten Bereichsleitfaden als Maßnahme innerhalb des [Standardmigrationsprozesses](../index.md) fort. Während der Voraussetzungsphase kann der Aufwand in den allgemeinen Cloud Adoption-Plan integriert werden.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Bevor Sie eine SQL Server-Migration durchführen, beginnen Sie mit einer Erweiterung der **digitalen Ressourcen**, indem Sie eine Datenressource einbeziehen. Die Datenressource zeichnet den Bestand der Datenobjekte auf, die für die Migration berücksichtigt werden können. In den folgenden Tabellen wird ein Ansatz zum Aufzeichnen der Datenressource erläutert.

### <a name="server-inventory"></a>Serverbestand

Im Folgenden finden Sie ein Beispiel für einen Serverbestand für SQL Server-Instanzen:

|SQL Server|Zweck|Version|[Wichtigkeit](../../manage/considerations/criticality.md)|[Vertraulichkeit](../../govern/policy-compliance/data-classification.md)|Anzahl von Datenbanken|SSIS|SSRS|SSAS|Cluster|Anzahl von Knoten|
|---------|---------|---------|---------|---------|---------|---------|---------|
|sql-01|Kern-Apps|2016|Unternehmenskritisch|Streng vertraulich|40|–|–|–|Ja|3|
|sql-02|Kern-Apps|2016|Unternehmenskritisch|Streng vertraulich|40|–|–|–|Ja|3|
|sql-03|Kern-Apps|2016|Unternehmenskritisch|Streng vertraulich|40|–|–|–|Ja|3|
|sql-04|BI|2012|Hoch|XX|6|–|Vertraulich|Ja, mehrdimensionaler Cube|Nein|1|
|sql-05|Integration|2008 R2|Niedrig|Allgemein|20|Ja|–|–|Nein|1|

### <a name="database-inventory"></a>Datenbankbestand

Im Folgenden finden Sie ein Beispiel für einen Datenbankbestand für eine der oben aufgeführten SQL Server-Instanzen:

|Server|Datenbank|[Wichtigkeit](../../manage/considerations/criticality.md)|[Vertraulichkeit](../../govern/policy-compliance/data-classification.md)|DMA-Ergebnisse|DMA-Wartung|Zielplattform|
|---------|---------|---------|---------|---------|---------|---------|
|sql-01|DB-1|Unternehmenskritisch|Streng vertraulich|Kompatibel|–|Azure SQL-Datenbank|
|sql-01|DB-2|Hoch|Vertraulich|Schemaänderung erforderlich|Implementierte Änderungen|Azure SQL-Datenbank|
|sql-01|DB-1|Hoch|Allgemein|Kompatibel|–|Verwaltete Azure SQL-Instanz|
|sql-01|DB-1|Niedrig|Streng vertraulich|Schemaänderung erforderlich|Geplante Änderungen|Verwaltete Azure SQL-Instanz|
|sql-01|DB-1|Unternehmenskritisch|Allgemein|Kompatibel|–|Verwaltete Azure SQL-Instanz|
|sql-01|DB-2|Hoch|Vertraulich|Kompatibel|–|Azure SQL-Datenbank|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integration in den Cloud Adoption-Plan

Nach Abschluss der Ermittlung kann der Plan in den [Cloud Adoption-Plan](../../plan/template.md) eingeschlossen werden. Fügen Sie innerhalb des Cloud Adoption-Plans jede zu migrierende SQL Server-Instanz als [individuelle Workload](../../plan/workloads.md) hinzu. In jeder Workload können die einzelnen Datenbanken und Dienste (SSIS, SSAS, SSRS) als [Ressourcen](../../plan/workloads.md) hinzugefügt werden. Um Workloads und Ressourcen in den Cloud Adoption-Plan durch Massenhinzufügen einzubinden, lesen Sie [Hinzufügen und Bearbeiten von Arbeitselementen mit Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Sobald die Workloads und Ressourcen im Plan enthalten sind, kann das Team mit einem Standardmigrationsprozess fortfahren, indem der Cloud Adoption-Plan verwendet wird, um die Anstrengungen zu steuern. Wenn das Cloud Adoption-Team zu den Bewertungs-, Migrations- und Optimierungsprozessen übergeht, sollten die folgenden Änderungen in die Maßnahmen einbezogen werden.

## <a name="assessment-process-changes"></a>Änderungen am Bewertungsprozess

Wenn eine Datenbank im Plan zu einer PaaS-Datenplattform (Platform-as-a-Service) migriert werden kann, verwenden Sie den Datenmigrations-Assistenten, um die Kompatibilität der ausgewählten Datenbank auszuwerten. Wenn die Datenbank Schemakonvertierungen erfordert, wird empfohlen, diese im Rahmen des Bewertungsprozesses abzuschließen, um Unterbrechungen der Migrationspipeline zu vermeiden.

### <a name="suggested-action-during-the-assessment-process"></a>Empfohlene Aktion während des Bewertungsprozesses

Für Datenbanken, die zu einer PaaS-Lösung migriert werden können, werden während des Bewertungsprozesses die folgenden Aktionen durchgeführt.

- **Bewerten mit dem Datenmigrations-Assistenten:** Verwenden Sie den Datenmigrations-Assistenten, um Kompatibilitätsprobleme zu erkennen, die sich auf die Datenbankfunktionalität in der verwalteten Instanz Ihrer Azure SQL-Zieldatenbank auswirken können, um Leistungs- und Zuverlässigkeitsverbesserungen zu empfehlen und um das Schema, die Daten und die abhängigen Objekte von Ihrem Quellserver auf Ihren Zielserver zu verschieben. Weitere Informationen finden Sie unter [Datenmigrations-Assistent](/sql/dma/dma-overview).
- **Korrektur und Konvertierung:** Konvertieren Sie basierend auf der Ausgabe des Datenmigrations-Assistenten das Quelldatenschema, um Kompatibilitätsprobleme zu korrigieren. Testen Sie das konvertierte Datenschema mit den abhängigen Anwendungen.

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Während der Migration gibt es mehrere Optionen für die verwendeten Tools und Ansätze. Aber jeder Ansatz folgt einem einfachen Prozess: Migrieren von Schema, Daten und Objekten. Synchronisieren Sie Daten mit der Zieldatenquelle.

Durch das Ziel und die Quelle der Datenstruktur und der Dienste können diese beiden Schritte recht kompliziert werden. In den folgenden Abschnitten finden Sie Informationen zur optimalen Auswahl von Tools basierend auf Ihren Migrationsentscheidungen.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

Der empfohlene Pfad für Migration und Synchronisierung verwendet eine Kombination der folgenden drei Tools. In den folgenden Abschnitten werden komplexere Migrations- und Synchronisierungsoptionen erläutert, die eine breitere Palette von Ziel- und Quelllösungen ermöglichen.

|Migrationsoption|Zweck|
|---------|---------|
|[Azure Database Migration Service](/sql/dma/dma-overview)|Azure DMS unterstützt Online- (minimale Ausfallzeiten) und Offlinemigrationen (einmalige Migration) im entsprechenden Maßstab zu einer verwalteten Azure SQL-Datenbank-Instanz von SQL Server 2005, SQL Server 2008 und SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 und SQL Server 2017.|
|[Transaktionsreplikation](/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Transaktionsreplikation in eine verwaltete Azure SQL-Datenbank-Instanz wird unterstützt für Migrationen von: SQL Server 2012 (SP2 CU8, SP3 oder höher), SQL Server 2014 (RTM CU10 oder höher oder SP1 CU3 oder höher), SQL Server 2016, SQL Server 2017|
|[Massenladen](/sql/t-sql/statements/bulk-insert-transact-sql)|Verwenden Sie das Massenladen in eine verwaltete Azure SQL-Datenbank-Instanz für Daten, die in SQL Server 2005, SQL Server 2008 und SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 und SQL Server 2017 gespeichert sind.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Anleitungen und Tutorials für den empfohlenen Migrationsprozess

Die Entscheidung für die beste Anleitung zur Migration mit DMS hängt von der Quell- und Zielplattform Ihrer Wahl ab. In der folgenden Tabelle werden die Tutorials für die einzelnen Standardansätze zum Migrieren einer SQL-Datenbank mithilfe von DMS beschrieben.

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL-Datenbank|DMS|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL-Datenbank|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Verwaltete Azure SQL-Datenbank-Instanz|DMS|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Verwaltete Azure SQL-Datenbank-Instanz|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS SQL Server|Azure SQL-Datenbank (oder verwaltete Instanz)|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Anleitungen und Tutorials für verschiedene Dienste für äquivalente PaaS-Lösungen

Nach dem Verschieben von Datenbanken aus einer SQL Server-Datenbank in DMS können das Schema und die Daten in einer Reihe von PaaS-Lösungen erneut gehostet werden. Andere erforderliche Dienste werden jedoch möglicherweise weiterhin auf diesem Server ausgeführt. Die folgenden drei Tutorials unterstützen Sie beim Verschieben von SSIS, SSAS und SSRS in entsprechende PaaS-Dienste in Azure.

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|SQL Server Integration Services|Data Factory Integration Runtime|Azure Data Factory|Offline|[Tutorial](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Services: Tabellenmodell|Azure Analysis Services|SSDT|Offline|[Tutorial](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|SQL Server Reporting Services|Power BI-Berichtsserver|Power BI|Offline|[Tutorial](/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Anleitungen und Tutorials für die Migration von SQL Server zu einer IaaS-Instanz von SQL Server

Nach dem Migrieren von Datenbanken und Diensten zu PaaS-Instanzen können noch Datenstrukturen und -Dienste vorhanden sein, die nicht mit PaaS kompatibel sind. Wenn vorhandene Einschränkungen die Migration von Datenstrukturen oder-Diensten verhindern, kann Sie das folgende Tutorial bei der Migration verschiedener Ressourcen im Datenportfolio zu Azure-IaaS-Lösungen unterstützen.

Dieser Ansatz kann verwendet werden, um Datenbanken auf dem SQL Server-Computer oder andere Dienste zu migrieren, die auf dem SQL Server-Quellcomputer ausgeführt werden.

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|Einzelne Instanz von SQL Server|SQL Server unter IaaS|Verschiedene|Offline|[Tutorial](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Änderungen im Optimierungsprozess

Während der Optimierung kann jede Datenstruktur, jeder Dienst oder jede SQL Server-Instanz getestet, optimiert und in die Produktion höhergestuft werden. Dies ist die größte Auswirkung der Abweichung von einem Migrationsmodell pro Workload.

Im Idealfall werden abhängige Workloads, Anwendungen und VMs innerhalb derselben Iterationen wie die SQL Server-Instanz migriert. Wenn dieses ideale Szenario auftritt, kann die Workload zusammen mit der Datenquelle getestet werden. Nachdem die Datenstruktur getestet wurde, kann sie in die Produktionsumgebung höhergestuft werden, und der Synchronisierungsprozess kann beendet werden.

Bedauerlicherweise tritt die größte Änderung des Optimierungsprozesses während einer nicht workloadgesteuerten Migration ein, wenn es eine signifikante zeitliche Lücke zwischen der Datenbankmigration und der Workloadmigration gibt. Wenn mehrere Datenbanken im Rahmen einer SQL Server-Migration migriert werden, können diese Datenbanken für mehrere Iterationen sowohl in der Cloud als auch lokal parallel vorhanden sein. Während dieses Zeitraums ist es erforderlich, die Datensynchronisierung beizubehalten, bis die abhängigen Ressourcen migriert, getestet und höhergestuft wurden.

Bis alle abhängigen Workloads höhergestuft wurden, ist das Team für die Unterstützung der Synchronisierung von Daten zwischen Quellsystem und Zielsystem verantwortlich. Diese Synchronisierung verbraucht Netzwerkbandbreite und vor allem Zeit der Benutzer und verursacht Cloudkosten. Die ordnungsgemäße Abstimmung des Cloud Adoption-Plans für die SQL Server-Migration „Workload“ und alle abhängigen Workloads/Anwendungen kann diesen kostenintensiven Mehraufwand verringern.

### <a name="suggested-action-during-the-optimization-process"></a>Empfohlene Aktion während des Optimierungsprozesses

Während der Optimierungsprozesse sollten die folgenden Aufgaben bei allen Iterationen abgeschlossen werden, bis alle Datenstrukturen und Dienste in die Produktionsumgebung höhergestuft wurden.

1. Überprüfen Sie die Synchronisierung von Daten.
2. Testen Sie alle migrierten Anwendungen.
3. Optimieren Sie die Anwendungs- und Datenstruktur, um Kosten zu optimieren.
4. Stufen Sie die Anwendungen höher in die Produktion.
5. Testen Sie auf fortgesetzten lokalen Datenverkehr für die lokale Datenbank.
6. Beenden Sie die Synchronisierung von Daten, die in die Produktion höhergestuft werden.
7. Beenden Sie die ursprüngliche Quelldatenbank.

Bis Schritt 5 abgeschlossen ist, können Datenbanken und die Synchronisierung nicht beendet werden. Bis alle Datenbanken in einer SQL Server-Instanz die Schritte 1 bis 7 durchlaufen haben, sollte die lokale SQL Server-Instanz als Produktionsumgebung behandelt werden, und die gesamte Synchronisierung sollte beibehalten werden.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur [Checkliste für erweiterten Umfang](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
