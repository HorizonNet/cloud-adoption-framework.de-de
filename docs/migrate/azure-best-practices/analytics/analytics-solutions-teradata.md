---
title: Analyselösungen für Teradata
description: Verwenden Sie das Cloud Adoption Framework für Azure, um mehr über Analyselösungen mit Teradata zu erfahren.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 85dc03afc7ea0d8c931c24009beb220d03b108e5
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452587"
---
<!-- cSpell:ignore DATEADD DATEDIFF Attunity Teradata Inmon NUSI Informatica Talend BTEQ FASTEXPORT QUALIFY ORC Parquet "Parallel Data Transporter" "Attunity Replicate" -->

# <a name="analytics-solutions-for-teradata"></a>Analyselösungen für Teradata

Benutzer der Data Warehouse-Systeme von Teradata möchten zunehmend auch die Innovationen in neueren Umgebungen wie Cloud, IaaS oder PaaS nutzen und Aufgaben wie Infrastrukturwartung und Plattformentwicklung an den Cloudanbieter delegieren.

Es gibt Ähnlichkeiten zwischen Teradata und Azure Synapse Analytics, da es sich bei beiden um SQL-Datenbanken handelt, die eine hohe Abfrageleistung für große Datenmengen mithilfe von MPP-Techniken (Massively Parallel Processing) erzielen, aber auch einige grundlegende Unterschiede:

- Ältere Teradata-Systeme werden normalerweise lokal unter Verwendung proprietärer Hardware installiert, während Azure Synapse Analytics cloudbasierte Speicher- und Computeressourcen nutzt.
- Ein Upgrade einer Teradata-Konfiguration stellt eine umfangreiche Aufgabe dar, die zusätzliche physische Hardware und eine potenziell langwierige Neukonfiguration der Datenbank einschließt. Da Speicher- und Computeressourcen in der Azure-Umgebung voneinander getrennt sind, können diese Ressourcen mithilfe der Funktion zur elastischen Skalierung sehr einfach zentral skaliert werden.
- Azure Synapse Analytics kann bei Bedarf angehalten oder in der Größe geändert werden, um die Ressourcennutzung und somit die Kosten zu reduzieren.

Zur Maximierung dieser Vorteile müssen vorhandene (oder neue) Daten und Anwendungen zur Azure Synapse Analytics-Plattform migriert werden. In vielen Organisationen gehört dazu die Migration eines vorhandenen Data Warehouse von lokalen Legacyplattformen wie Teradata. Der grundlegende Prozess umfasst im Allgemeinen die folgenden Schritte:

<!-- markdownlint-disable MD033 -->

| Vorbereitung | Migration | Nach der Migration |
|---|---|---|
| <li> Definieren des Bereichs: Was soll migriert werden? <li> Durchführen einer Inventur von Daten und Prozessen für die Migration <li> Definieren von Datenmodelländerungen (falls erforderlich) <li> Identifizieren der geeigneten Tools und Features von Azure (und Drittanbietern), die verwendet werden sollen <li> Frühzeitige Schulung von Mitarbeitern auf der neuen Plattform <li> Einrichten der Azure-Zielplattform |  <li> Einfaches Beginnen mit einem kleinen Umfang <li> Automatisieren, wann immer möglich <li> Verwenden von integrierten Azure-Tools und -Features zum Verringern des Migrationsaufwands <li> Migrieren von Metadaten für Tabellen und Sichten <li> Migrieren von Verlaufsdaten, die beibehalten werden sollen <li> Migrieren oder Umgestalten von gespeicherten Prozeduren und Geschäftsprozessen <li> Migrieren oder Umgestalten von ETL-/ELT-Prozessen für inkrementelles Laden |  <li> Überwachen und Dokumentieren aller Phasen des Prozesses <li> Nutzen der gewonnenen Erfahrungen zum Erstellen einer Vorlage für zukünftige Migrationsvorgänge <li> Erneutes Erstellen des Datenmodells bei Bedarf anhand der Leistung und Skalierbarkeit der neuen Plattform <li> Testen von Anwendungen und Abfragetools <li> Erstellen von Benchmarks und Optimieren der Abfrageleistung |

## <a name="migration-scope"></a>Migrationsumfang

### <a name="choose-the-workload-for-the-initial-migration"></a>Auswählen der Workload für die erste Migration

Ältere Teradata-Umgebungen wurden meist im Lauf der Zeit auf mehrere Themenbereiche und gemischte Workloads ausgeweitet. Bei der Entscheidung, wo ein erstes Migrationsprojekt ansetzen soll, sollten Sie einen Bereich auswählen, mit dem folgende Ergebnisse erzielt werden können:

- Belegen der Machbarkeit einer Migration zu Azure Synapse Analytics durch schnelles Bereitstellen der Vorteile der neuen Umgebung
- Ermöglichen des Gewinnens relevanter Erfahrungen für die internen technischen Mitarbeiter zu den Prozessen und Tools, die bei Migrationsvorgängen anderer Bereiche genutzt werden können
- Erstellen einer Vorlage für weitere Migrationsübungen speziell für die Teradata-Quellumgebung sowie die bereits vorhanden aktuellen Tools und Prozesse

Ein guter Kandidat für eine erste Migration aus einer Teradata-Umgebung, die die oben genannten Punkte umsetzt, ist normalerweise eine Implementierung einer BI-/Analyseworkload (d. h. keine OLTP-Workload) mit einem Datenmodell, das mit minimalen Änderungen migriert werden kann – im Allgemeinen ein Stern- oder Schneeflockenschema.

Bezüglich der Größe muss das in der ersten Übung migrierte Datenvolume groß genug sein, um die Funktionen und Vorteile der Azure Synapse Analytics-Umgebung zu veranschaulichen, und gleichzeitig die Zeit für die Veranschaulichung kurz halten, in der Regel im Bereich von 1–10 TB.

Ein möglicher Ansatz für das erste Migrationsprojekt mit minimalem Risiko und kurzer Implementierungszeit ist eine Beschränkung des Umfangs der Migration auf die Data Marts (z. B. die OLAP-Datenbank eines Teradata-Warehouse). Bei diesem Ansatz wird per Definition der Umfang der Migration eingeschränkt, sodass er normalerweise in kurzer Zeit erreicht werden kann. Dadurch bildet er einen guten Ausgangspunkt. Dieser Ansatz schließt jedoch nicht die breiter gestreuten Themen wie ETL-Migration und Verlaufsdatenmigration im Rahmen des ersten Migrationsprojekts ein. Diese müssen in späteren Phasen des Projekts behandelt werden, wenn die migrierte Data Mart-Schicht wieder mit den erforderlichen Daten und Prozessen gefüllt wird.

## <a name="lift-and-shift-as-is-versus-a-phased-approach-incorporating-changes"></a>Lift & Shift der vorhandenen Umgebung im Vergleich zu einem phasenorientierten Ansatz mit Änderungen

Unabhängig von den Beweggründen und dem Umfang der vorgesehenen Migration gibt es allgemein ausgedrückt zwei Typen von Migrationsvorgängen:

### <a name="lift-and-shift"></a>Lift & Shift

In diesem Fall wird das vorhandene Datenmodell (z. B. ein Sternschema) unverändert zur neuen Azure Synapse Analytics-Plattform migriert. Der Schwerpunkt liegt hierbei auf der Minimierung des Risikos und der Zeit für die Migration, indem die erforderliche Arbeit zum Erreichen der Vorteile der Umstellung auf die Azure-Cloudumgebung verringert wird.

Dies eignet sich gut für vorhandene Teradata-Umgebungen, in denen ein einzelner Data Mart migriert werden soll oder sich die Daten bereits in einem gut entworfenen Stern- oder Schneeflockenschema befinden. Auch wenn für den Wechsel in eine modernere Umgebung Zeitdruck besteht, ist dieser Migrationstyp gut geeignet.

### <a name="phased-approach-incorporating-modifications"></a>Phasenorientiertes Konzept unter Einbindung von Änderungen

In Fällen, in denen ein Legacywarehouse über einen längeren Zeitraum weiterentwickelt wurde, muss möglicherweise eine Umstrukturierung erfolgen, um die erforderlichen Leistungsstufen beizubehalten oder neue Daten zu unterstützen (z. B. IoT-Streams). Die Migration zu Azure Synapse Analytics zum Erreichen der Vorteile einer skalierbaren Cloudumgebung kann als Teil des Umgestaltungsvorgangs angesehen werden. Dazu kann eine Änderung des zugrunde liegenden Datenmodells gehören (z. B. eine Umstellung von einem Inmon-Modell zu einem Datentresor).

Die empfohlene Vorgehensweise besteht darin, zuerst das vorhandene Datenmodell unverändert in die Azure-Umgebung zu verschieben (optional unter Verwendung einer VM-Teradata-Instanz in Azure wie unten beschrieben) und dann mithilfe der Leistungsfähigkeit und Flexibilität der Azure-Umgebung die Änderungen im Rahmen der Umgestaltung vorzunehmen. Bei Bedarf können dabei Azure-Funktionen verwendet werden, damit die Änderungen keine Auswirkungen auf das vorhandene Quellsystem haben.

## <a name="using-a-vm-teradata-instance-as-part-of-a-migration"></a>Verwenden einer VM-Teradata-Instanz als Teil einer Migration

Ein optionaler Ansatz zum Ausführen einer Migration von einer lokalen Teradata-Umgebung ist die Verwendung der Azure-Umgebung mit ihrem preisgünstigen Cloudspeicher und elastischer Skalierbarkeit, um eine Teradata-Instanz in einer VM in Azure zu erstellen, die sich am selben Standort wie die Azure Synapse Analytics-Zielumgebung befindet.

Bei diesem Ansatz können standardmäßige Teradata-Hilfsprogramme wie Teradata Parallel Data Transporter (oder Datenreplikationstools von Drittanbietern wie Attunity Replicate) verwendet werden, um die Teilmenge der zu migrierenden Teradata-Tabellen effizient auf die VM-Instanz zu verschieben. Anschließend können alle Migrationsaufgaben in der Azure-Umgebung ausgeführt werden. Dieser Ansatz hat mehrere Vorteile:

- Nach der ersten Replikation von Daten wird das Quellsystem von den Migrationsaufgaben nicht weiter beeinträchtigt.
- Die vertrauten Teradata-Schnittstellen, -Tools und -Hilfsprogramme sind in der Azure-Umgebung verfügbar.
- In der Azure-Umgebung gibt es keine potenziellen Probleme mehr mit der Verfügbarkeit von Netzwerkbandbreite zwischen dem lokalen Quellsystem und dem Cloudzielsystem.
- Tools wie Azure Data Factory können effizient Hilfsprogramme wie Teradata Parallel Transporter aufrufen, um Daten schnell und einfach zu migrieren.
- Der Migrationsprozess wird vollständig in der Azure-Umgebung orchestriert und gesteuert.

## <a name="use-azure-data-factory-to-implement-a-metadata-driven-migration"></a>Verwenden von Azure Data Factory zum Implementieren einer metadatengesteuerten Migration

Es ist sinnvoll, den Migrationsprozess mithilfe der Funktionen in der Azure-Umgebung zu automatisieren und zu orchestrieren. Bei dieser Vorgehensweise werden auch die Auswirkungen auf die vorhandene Teradata-Umgebung (die möglicherweise bereits fast vollständig ausgelastet ist) minimiert.

Azure Data Factory ist ein cloudbasierter Datenintegrationsdienst, mit dem Sie datengesteuerte Workflows in der Cloud erstellen können, um Datenverschiebungen und Datentransformationen zu orchestrieren und zu automatisieren. Mit Azure Data Factory können Sie datengesteuerte Workflows (so genannte Pipelines) erstellen und planen, die Daten aus unterschiedlichen Datenspeichern erfassen. Die Anwendung kann diese Daten mithilfe von Compute Services wie Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics und Azure Machine Learning verarbeiten und transformieren.

Wenn Sie Metadaten zum Auflisten der zu migrierenden Datentabellen und deren Speicherort erstellen, können Sie die Funktionen von Azure Data Factory teilweise zum Verwalten und Automatisieren des Migrationsprozesses verwenden.

## <a name="design-differences-between-teradata-and-azure-synapse-analytics"></a>Entwurfsunterschiede zwischen Teradata und Azure Synapse Analytics

### <a name="separate-databases-versus-schemas"></a>Separate Datenbanken im Vergleich zu Schemas

In einer Teradata-Umgebung werden häufig mehrere separate Datenbanken für einzelne Teile der Gesamtumgebung definiert. Beispielsweise kann eine separate Datenbank für Datenerfassung und Stagingtabellen vorhanden sein, eine Datenbank für die Haupttabellen des Warehouses und eine weitere Datenbank für Data Marts (manchmal auch als Semantikschicht bezeichnet). Bei der Verarbeitung von ETL-/ELT-Pipelines werden möglicherweise datenbankübergreifende Joins implementiert und immer Daten zwischen diesen separaten Datenbanken verschoben.

Die Azure Synapse Analytics-Umgebung verfügt über einen Singleton, und mithilfe von Schemas werden die Tabellen in logisch getrennte Gruppen aufgeteilt. Es wird daher empfohlen, eine Reihe von Schemas im Azure Synapse Analytics-Ziel zu verwenden, um die aus der Teradata-Umgebung migrierten einzelnen Datenbanken zu imitieren. Wenn in der Teradata-Umgebung bereits Schemas verwendet werden, muss eventuell eine neue Benennungskonvention verwendet werden, um die vorhandenen Teradata-Tabellen und -Sichten in die neue Umgebung zu verschieben. Beispielsweise können das vorhandene Teradata-Schema und die Tabellennamen mit den neuen Azure Synapse Analytics-Tabellennamen verkettet werden, um über die Schemanamen in der neuen Umgebung die ursprünglichen separaten Datenbanknamen beizubehalten. Eine andere Möglichkeit ist die Verwendung von SQL-Sichten für die zugrunde liegenden Tabellen, um die logischen Strukturen beizubehalten. Dieser Ansatz bringt jedoch einige mögliche Nachteile mit sich:

- Sichten in Azure Synapse Analytics sind schreibgeschützt, sodass alle Updates an den Daten in den zugrunde liegenden Basistabellen erfolgen müssen.
- Möglicherweise gibt es bereits Ebenen von Sichten, und das Hinzufügen einer zusätzlichen Sichtebene wirkt sich auf die Leistung aus.

### <a name="table-considerations"></a>Überlegungen zu Tabellen

Beim Migrieren von Tabellen zwischen unterschiedlichen Technologien werden in der Regel nur die Rohdaten zusammen mit den Metadaten, die sie beschreiben, physisch zwischen den beiden Umgebungen verschoben. Andere Datenbankelemente aus dem Quellsystem (z. B. Indizes) werden nicht migriert, da diese Elemente möglicherweise nicht benötigt werden oder in der neuen Zielumgebung anders implementiert sind.

Es ist jedoch wichtig zu verstehen, wo Leistungsoptimierungen wie z. B. Indizes in der Quellumgebung verwendet wurden, da diese Informationen nützliche Hinweise darauf geben können, wo eine Leistungsoptimierung in der neuen Zielumgebung umgesetzt werden kann. Wenn beispielsweise in der Teradata-Quellumgebung ein NUSI erstellt wurde, kann dies darauf hindeuten, dass in der migrierten Azure Synapse Analytics-Umgebung ein nicht gruppierter Index erstellt werden sollte, jedoch sind andere native Leistungsoptimierungstechniken (z. B. Tabellenreplikation) möglicherweise besser geeignet als eine direkt abgebildete Indexerstellung.

### <a name="high-availability-for-the-database"></a>Hochverfügbarkeit für die Datenbank

Teradata unterstützt die Datenreplikation über Knoten hinweg mit der Option `FALLBACK`. Hierbei werden Tabellenzeilen, die sich physisch auf einem bestimmten Knoten befinden, auf einen anderen Knoten im System repliziert. Mit diesem Ansatz wird sichergestellt, dass keine Daten verloren gehen, wenn ein Knotenfehler auftritt. Damit stellt er die Grundlage für Failoverszenarien dar.

Die Architektur für Hochverfügbarkeit in Azure SQL-Datenbank soll garantieren, dass Ihre Datenbank aktiv ist und zu 99,99 % der Zeit ausgeführt wird, ohne dass Sie sich Gedanken über die Auswirkungen von Wartungsarbeiten und Ausfällen machen müssen. Azure verarbeitet automatisch wichtige Wartungsaufgaben, z. B. Patches, Sicherungen, Windows- und SQL-Upgrades, aber auch ungeplante Ereignisse wie Ausfälle der zugrunde liegenden Hard- und Software oder Netzwerkfehler.

Die Datenspeicherung in Azure Synapse Analytics wird automatisch durch Momentaufnahmen gesichert. Diese Momentaufnahmen sind ein integriertes Feature des Diensts zum Erstellen von Wiederherstellungspunkten. Sie müssen das Feature nicht aktivieren. Automatische Wiederherstellungspunkte können derzeit nicht von Benutzern gelöscht werden, wenn der Dienst mithilfe dieser Wiederherstellungspunkte SLAs für die Wiederherstellung verwaltet.

Azure SQL Data Warehouse erstellt im Lauf des Tages Momentaufnahmen des Data Warehouse und generiert Wiederherstellungspunkte, die sieben Tage lang verfügbar sind. Dieser Aufbewahrungszeitraum kann nicht geändert werden. Azure SQL Data Warehouse unterstützt ein RPO (Recovery Point Objective) von acht Stunden. Sie können das Data Warehouse in der primären Region anhand einer beliebigen Momentaufnahme wiederherstellen, die in den vergangenen sieben Tagen erstellt wurde. Wenn differenziertere Sicherungen erforderlich sind, stehen weitere benutzerdefinierte Optionen zur Verfügung.

### <a name="unsupported-teradata-table-types"></a>Nicht unterstützte Teradata-Tabellentypen

Teradata bietet Unterstützung für spezielle Tabellentypen für Zeitreihen und temporale Daten. Die Syntax und einige Funktionen für diese Tabellentypen werden in Azure Synapse Analytics nicht direkt unterstützt, aber die Daten können mit entsprechenden Datentypen und Indizierung oder Partitionierung für die Datums-/Uhrzeitspalte zu einer Standardtabelle migriert werden.

Teradata implementiert die Funktion für temporale Abfrage über das Umschreiben von Abfragen, um zusätzliche Filter in einer temporalen Abfrage hinzuzufügen und so den betreffenden Datumsbereich einzuschränken. Wenn diese Funktion derzeit in der Teradata-Quellumgebung verwendet wird und migriert werden soll, muss diese zusätzliche Filterung den entsprechenden temporalen Abfragen hinzugefügt werden.

Die Azure-Umgebung umfasst auch bestimmte Features für komplexe Analysen zu Zeitreihendaten in jeder Größenordnung unter dem Namen Time Series Insights. Dies richtet sich an IoT-Datenanalyseanwendungen und eignet sich für diesen Anwendungsfall möglicherweise besser. Weitere Informationen finden Sie unter [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/).

### <a name="teradata-data-type-mapping"></a>Teradata-Datentypzuordnung

Einige Teradata-Datentypen werden in Azure Synapse Analytics nicht direkt unterstützt. In der folgenden Tabelle sind diese Datentypen und die empfohlene Vorgehensweise zur Behandlung aufgeführt. In der Tabelle ist der Teradata-Spaltentyp der Typ, der im Systemkatalog gespeichert ist (z. B. in `DBC.ColumnsV`).

Verwenden Sie die Metadaten aus den Teradata-Katalogtabellen, um festzulegen, ob diese Datentypen migriert werden sollen, und planen Sie dies im Migrationsplan ein. Beispielsweise kann eine SQL-Abfrage wie die folgende verwendet werden, um beliebige Vorkommen nicht unterstützter Datentypen zu finden, die Aufmerksamkeit erfordern.

Bestimmte Drittanbieter bieten Tools und Dienste zum Automatisieren der Migration an, einschließlich der oben beschriebenen Zuordnung von Datentypen. Wenn bereits in der Teradata-Umgebung ein ETL-Tool von Drittanbietern wie Informatica oder Talend verwendet wird, kann dieses außerdem alle erforderlichen Datentransformationen implementieren.

## <a name="sql-dml-syntax-differences"></a>Syntaxunterschiede in SQL DML

Es gibt einige Unterschiede in der SQL DML-Syntax (Data Manipulation Language) zwischen Teradata SQL und Azure Synapse Analytics, die bei der Migration berücksichtigt werden müssen:

- **QUALIFY:** Teradata unterstützt den Operator `QUALIFY`. Beispiel:

  `SELECT col1 FROM tab1 WHERE col1='XYZ'`

  Tools und Dienste von Drittanbietern können Datenzuordnungsaufgaben automatisieren:

  `QUALIFY ROW_NUMBER() OVER (PARTITION by col1 ORDER BY col1) = 1;`

  Dies kann in Azure Synapse mithilfe der nachstehenden Syntax erreicht werden:

  `SELECT * FROM (SELECT col1, ROW_NUMBER() OVER (PARTITION by col1 ORDER BY col1) rn FROM tab1 WHERE c1='XYZ' ) WHERE rn = 1;`

- **Datumsarithmetik:** Azure Synapse verfügt über Operatoren wie

  - `DATEADD` und `DATEDIFF`, die in Feldern der Typen `DATE` oder `DATETIME` verwendet werden können. Teradata unterstützt die direkte Subtraktion für Datumsangaben, z. B.:

    `SELECT DATE1 - DATE2 FROM ...`

  - `LIKE ANY`-Syntax, z. B.:

    `SELECT * FROM CUSTOMER WHERE POSTCODE LIKE ANY ('CV1%', 'CV2%', CV3%') ;`.

    Die Entsprechung in der Azure Synapse-Syntax lautet:

    `SELECT * FROM CUSTOMER WHERE (POSTCODE LIKE 'CV1%') OR (POSTCODE LIKE 'CV2%') OR (POSTCODE LIKE 'CV3%') ;`

- Abhängig von den Systemeinstellungen wird bei Zeichenvergleichen in Teradata eventuell standardmäßig nicht zwischen Groß- und Kleinschreibung unterschieden. In Azure Synapse wird die Groß- und Kleinschreibung bei diesen Vergleichen immer beachtet.

## <a name="functions-stored-procedures-triggers-and-sequences"></a>Funktionen, gespeicherte Prozeduren, Trigger und Sequenzen

Bei der Migration von einer ausgereiften Legacy-Data Warehouse-Umgebung wie Teradata müssen häufig noch weitere Elemente als einfache Tabellen und Sichten zur neuen Zielumgebung migriert werden. Beispiele sind Funktionen, gespeicherte Prozeduren, Trigger und Sequenzen.

In der Vorbereitungsphase sollte eine Inventur dieser zu migrierenden Objekte durchgeführt und die Methode zur Handhabung definiert werden. Dabei sollten die im Projektplan zugewiesenen Ressourcen entsprechenden zugeordnet werden.

Funktionen in der Azure-Umgebung können die als Funktionen oder gespeicherte Prozeduren in der Teradata-Umgebung implementierte Funktionalität ersetzen. In diesem Fall ist es in der Regel effizienter, die integrierten Azure-Funktionen zu verwenden, anstatt den Code der Teradata-Funktionen zu rekonstruieren.

Weitere Informationen zu diesen einzelnen Elementen finden Sie weiter unten.

### <a name="functions"></a>Functions

Bei den meisten Datenbankprodukten unterstützt Teradata Systemfunktionen und auch benutzerdefinierte Funktionen in der SQL-Implementierung. Bei der Migration zu einer anderen Datenbankplattform wie Azure Synapse sind gängige Systemfunktionen allgemein verfügbar und können ohne Änderung migriert werden. Einige Systemfunktionen weisen möglicherweise eine etwas andere Syntax auf, aber die erforderlichen Änderungen können in diesem Fall automatisiert werden.

Systemfunktionen, für die es keine Entsprechung gibt, oder unabhängige benutzerdefinierte Funktionen müssen möglicherweise mithilfe der in der Zielumgebung verfügbaren Sprachen neu programmiert werden. Azure Synapse verwendet die verbreitete Sprache Transact-SQL für die Implementierung von benutzerdefinierten Funktionen.

### <a name="stored-procedures"></a>Gespeicherte Prozeduren

Bei den meisten modernen Datenbankprodukten können Prozeduren in der Datenbank gespeichert werden. Teradata stellt zu diesem Zweck die SPL-Sprache bereit. Eine gespeicherte Prozedur enthält normalerweise SQL-Anweisungen und prozedurale Logik und kann Daten oder einen Status zurückgeben.

SQL Azure Data Warehouse unterstützt auch gespeicherte Prozeduren unter Verwendung von T-SQL. Zum Migrieren gespeicherter Prozeduren müssen diese dementsprechend neu programmiert werden.

### <a name="triggers"></a>Trigger

Das Erstellen von Triggern wird in Azure Synapse nicht unterstützt, kann aber in Azure Data Factory implementiert werden.

### <a name="sequences"></a>Sequenzen

Azure Synapse-Sequenzen werden ähnlich wie bei Teradata behandelt, indem die nächste Sequenznummer in einer Reihe über `IDENTITY`-Spalten oder SQL-Code erstellt wird.

## <a name="extracting-metadata-and-data-from-a-teradata-environment"></a>Extrahieren von Metadaten und Daten aus einer Teradata-Umgebung

### <a name="data-definition-language-ddl-generation"></a>Generierung von DDL-Anweisungen (Data Definition Language, Datendefinitionssprache)

Vorhandene Teradata-Skripts mit `CREATE TABLE` und `CREATE VIEW` können bearbeitet werden, um die entsprechenden Definitionen zu erstellen (bei Bedarf mit geänderten Datentypen, wie oben beschrieben). In der Regel umfasst dies das Entfernen zusätzlicher Teradata-spezifischer Klauseln (z. B. `FALLBACK`).

Alle Informationen, die sich auf die aktuellen Definitionen von Tabellen und Sichten in der vorhandenen Teradata-Umgebung beziehen, werden jedoch in den Systemkatalogtabellen verwaltet. Dies ist die beste Quelle für diese Informationen, da sie garantiert aktuell und vollständig ist. Die benutzerseitig verwaltete Dokumentation ist möglicherweise nicht mit den aktuellen Tabellendefinitionen synchron.

Auf diese Informationen kann über Sichten im Katalog zugegriffen werden, z. B. `DBC.ColumnsV`. Mit ihrer Hilfe können die entsprechenden `CREATE TABLE`-Anweisungen der DDL für die entsprechenden Tabellen in Azure Synapse generiert werden.  

Das gleiche Ergebnis kann auch mit Migrations- und ETL-Tools von Drittanbietern erzielt werden, indem diese auf die Informationen im Katalog zugreifen.

### <a name="data-extraction-from-teradata"></a>Extrahieren von Daten aus Teradata

Migrieren Sie die Rohdaten mit Teradata-Standardhilfsprogrammen wie `BTEQ` und `FASTEXPORT` aus vorhandenen Teradata-Tabellen. Im Allgemeinen ist es bei einer Migrationsübung wichtig, die Daten so effizient wie möglich zu extrahieren. Der empfohlene Ansatz bei den aktuellen Versionen von Teradata ist die Verwendung von Teradata Parallel Transporter, bei dem über mehrere parallele `FASTEXPORT`-Streams ein optimaler Durchsatz erzielt wird.

Teradata Parallel Transporter kann direkt aus Azure Data Factory aufgerufen werden. Dies ist die empfohlene Vorgehensweise für die Verwaltung des Datenmigrationsprozesses. (Dies gilt unabhängig davon, ob die Teradata-Instanz lokal ist oder auf eine VM in der Azure-Umgebung kopiert wurde, wie oben beschrieben.)  
Empfohlene Datenformate für die extrahierten Daten sind durch Trennzeichen getrennte Textdateien (auch als CSV-Dateien o. ä. bezeichnet) oder ORC- (Optimized Row Columnar) oder Parquet-Dateien.

Ausführlichere Informationen zum Migrieren von Daten und ETL aus einer Teradata-Umgebung finden Sie in Abschnitt 2.1 des zugehörigen Dokuments. Datenmigration durch ETL und Laden von Teradata.

## <a name="performance-recommendations-for-teradata-migrations"></a>Leistungsempfehlungen für Teradata-Migrationsvorgänge

Unterschiede in Leistungsoptimierungskonzepten

### <a name="data-distribution-options"></a>Datenverteilungsoptionen

Azure ermöglicht die Angabe von Datenverteilungsmethoden für einzelne Tabellen. Dabei soll die Menge der Daten verringert werden, die beim Ausführen einer Abfrage zwischen Verarbeitungsknoten verschoben werden müssen.  

Bei Verknüpfungen großer Tabellen miteinander wird durch die Hashverteilung von einer Tabelle oder (idealerweise) in den Joinspalten sichergestellt, dass die Joinverarbeitung lokal ausgeführt werden kann, da sich die zu verknüpfenden Datenzeilen bereits auf demselben Verarbeitungsknoten befinden.

Eine andere Möglichkeit, lokale Joins für Verknüpfungen kleiner Tabellen mit großen Tabellen (meist eine Dimensionstabelle mit einer Faktentabelle in einem Sternschemamodell) zu erreichen, besteht im Replizieren der kleineren Dimensionstabelle auf allen Knoten. Dadurch wird sichergestellt, dass für jeden Wert des Joinschlüssels der größeren Tabelle eine zugehörige Dimensionszeile lokal verfügbar ist. Der Aufwand für die Replikation der Dimensionstabellen ist relativ gering, sofern die Tabellen nicht groß sind. In diesem Fall ist der oben beschriebene Hashverteilungsansatz besser geeignet.

### <a name="data-indexing"></a>Datenindizierung

Azure Synapse bietet verschiedene Indizierungsoptionen, aber diese unterscheiden sich in Betrieb und Nutzung von den in Teradata implementierten. Weitere Informationen zu den verschiedenen Indizierungsoptionen finden Sie unter [Entwerfen von Tabellen in einem Synapse SQL-Pool](https://docs.microsoft.com/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-overview).

Vorhandene Indizes in der Teradata-Quellumgebung können jedoch einen nützlichen Hinweis darauf bereitstellen, wie die Daten derzeit verwendet werden und welche Daten in der Azure Synapse-Umgebung indiziert werden sollten.

### <a name="data-partitioning"></a>Datenpartitionierung

Im Data Warehouse eines Unternehmens können Faktentabellen viele Milliarden Zeilen enthalten, und die Partitionierung ist eine Möglichkeit, die Verwaltung und Abfrage dieser Tabellen zu optimieren, indem sie in separate Teile aufgeteilt werden, um die Menge der verarbeiteten Daten zu reduzieren. Die Partitionierungsspezifikation für eine Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

Für die Partitionierung kann nur ein Feld pro Tabelle verwendet werden. Hierbei handelt es sich häufig um ein Datumsfeld, da viele Abfragen nach einem Datum oder Datumsbereich gefiltert werden. Sie können die Partitionierung einer Tabelle nach dem anfänglichen Laden bei Bedarf ändern, indem Sie die Tabelle mit der neuen Verteilung anhand der `CREATE TABLE AS SELECT`-Anweisung neu erstellen. Eine ausführliche Erläuterung der Partitionierung in Azure Synapse finden Sie unter [Partitionieren von Tabellen in einem Synapse SQL-Pool](https://docs.microsoft.com/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition).

### <a name="data-table-statistics"></a>Datentabellenstatistiken

Stellen Sie sicher, dass die Statistiken zu Datentabellen auf dem neuesten Stand sind. Integrieren Sie dazu einen Schritt `COLLECT STATISTICS` für ETL-/ELT-Aufträge, oder aktivieren Sie die automatische Statistiksammlung für die Tabelle.

### <a name="polybase-for-data-loading"></a>PolyBase zum Laden von Daten

PolyBase stellt die effizienteste Methode dar, große Datenmengen in das Warehouse zu laden, da hierbei parallele Ladestreams verwendet werden können.

### <a name="use-resource-classes-for-workload-management"></a>Verwenden von Ressourcenklassen für die Workloadverwaltung

Azure Synapse Analytics verwendet Ressourcenklassen zum Verwalten von Workloads. Im Allgemeinen bieten große Ressourcenklassen eine bessere Leistung bei einzelnen Abfragen, während kleinere Ressourcenklassen ein höheres Maß an Parallelität ermöglichen. Die Auslastung kann über dynamische Verwaltungssichten überwacht werden, um sicherzustellen, dass die entsprechenden Ressourcen effizient verwendet werden.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Implementieren einer Teradata-Migration erhalten Sie bei Ihrem Microsoft-Kontovertreter, der Sie gerne über lokale Migrationsangebote informiert.
