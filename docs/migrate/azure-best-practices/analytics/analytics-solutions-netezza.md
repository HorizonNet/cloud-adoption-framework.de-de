---
title: Analyselösungen für Netezza
description: Verwenden Sie das Cloud Adoption Framework für Azure, um mehr über Analyselösungen mit Netezza zu erfahren.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4de63bd39c9b5e22d5848532aef956374fa32414
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452586"
---
<!-- cSpell:ignore Netezza Informatica Talend InMon zonemap CBTs Attunity Wherescape nzlua CBT NZPLSQL DELIM TABLENAME ORC Parquet nzsql nzunload mpp -->

# <a name="analytics-solutions-for-netezza"></a>Analyselösungen für Netezza

Angesichts des Endes des Supports von IBM möchten viele Benutzer der Data Warehouse-Systeme von Netezza zunehmend auch die Innovationen in neueren Umgebungen wie Cloud, IaaS oder PaaS nutzen und Aufgaben wie Infrastrukturwartung und Plattformentwicklung an den Cloudanbieter delegieren.

Es gibt Ähnlichkeiten zwischen Netezza und Azure Synapse Analytics, da es sich bei beiden um SQL-Datenbanken handelt, die eine hohe Abfrageleistung für sehr große Datenmengen mithilfe von MPP-Techniken (Massively Parallel Processing) erzielen, aber auch einige grundlegende Unterschiede:

- Ältere Netezza-Systeme werden normalerweise lokal unter Verwendung proprietärer Hardware installiert, während Azure Synapse Analytics cloudbasierte Azure Storage- und Computeressourcen nutzt.
- Ein Upgrade einer Netezza-Konfiguration stellt eine umfangreiche Aufgabe dar, die zusätzliche physische Hardware und eine potenziell langwierige Neukonfiguration der Datenbank oder eine Abbildsicherung und erneutes Laden einschließt. Da Speicher- und Computeressourcen in der Azure-Umgebung voneinander getrennt sind, können sie mithilfe der Funktion zur elastischen Skalierung sehr einfach zentral skaliert werden.
- Bei Bedarf kann Azure Synapse Analytics angehalten oder seine Größe geändert werden, um die Ressourcennutzung und somit die Kosten zu reduzieren. Microsoft Azure ist eine weltweit verfügbare, äußerst sichere und skalierbare Cloudumgebung, die Azure Synapse innerhalb eines Ökosystems aus unterstützenden Tools und Funktionen umfasst.

Im folgenden finden Sie eine Übersicht über die Schemamigration und erfahren, wie Sie eine entsprechende oder bessere Leistung Ihrer migrierten Netezza-Data Warehouse und -Data Marts in Azure Synapse erzielen. Die Themen dieses Dokuments gelten speziell für Migrationen aus einer vorhandenen Netezza-Umgebung.

## <a name="design-considerations"></a>Überlegungen zum Entwurf

### <a name="migration-scope"></a>Migrationsumfang

### <a name="preparation-for-migration"></a>Vorbereitung für die Migration

Bei der Migration aus einer Netezza-Umgebung müssen neben den allgemeineren Themen, die im Dokument „Abschnitt 1: Entwurf und Leistung“ beschrieben werden, einige spezifische Themen berücksichtigt werden.

### <a name="choosing-the-workload-for-the-initial-migration"></a>Auswählen der Workload für die erste Migration

Ältere Netezza-Umgebungen wurden meist im Lauf der Zeit auf mehrere Themenbereiche und gemischte Workloads ausgeweitet. Bei der Entscheidung, wo ein erstes Migrationsprojekt ansetzen soll, sollten Sie einen Bereich auswählen, mit dem folgende Ergebnisse erzielt werden können:

- Belegen der Machbarkeit einer Migration zu Azure Synapse durch schnelles Bereitstellen der Vorteile der neuen Umgebung.
- Ermöglichen des Gewinnens relevanter Erfahrungen für die internen technischen Mitarbeiter zu den Prozessen und Tools, die bei Migrationsvorgängen anderer Bereiche genutzt werden können.
- Erstellen einer Vorlage für weitere Migrationsübungen speziell für die Netezza-Quellumgebung sowie die bereits vorhanden aktuellen Tools und Prozesse.

Ein guter Kandidat für eine erste Migration aus einer Netezza-Umgebung, die die oben genannten Punkte umsetzt, ist normalerweise eine Implementierung einer BI-/Analyseworkload statt einer OLTP-Workload mit einem Datenmodell, das mit minimalen Änderungen migriert werden kann – im Allgemeinen ein Stern- oder Schneeflockenschema.

Bezüglich der Größe muss das in der ersten Übung migrierte Datenvolume groß genug sein, um die Funktionen und Vorteile der Azure Synapse-Umgebung zu veranschaulichen, und gleichzeitig die Zeit für die Veranschaulichung kurz halten, in der Regel im Bereich von 1–10 TB.

Ein möglicher Ansatz für das erste Migrationsprojekt mit minimalem Risiko und kurzer Implementierungszeit ist eine Beschränkung des Umfangs der Migration auf die Data Marts. Bei diesem Ansatz wird per Definition der Umfang der Migration eingeschränkt, sodass er normalerweise in kurzer Zeit erreicht werden kann. Dadurch bildet er einen guten Ausgangspunkt. Dies schließt jedoch nicht die breiter gestreuten Themen wie ETL-Migration und Verlaufsdatenmigration im Rahmen des ersten Migrationsprojekts ein. Diese Themen müssen in späteren Phasen des Projekts behandelt werden, wenn die migrierte Data Mart-Schicht wieder mit den erforderlichen Daten und Prozessen gefüllt wird.

### <a name="lift-and-shift-as-is-versus-a-phased-approach-incorporating-changes"></a>Lift und Shift der vorhandenen Umgebung im Vergleich zu einem phasenorientierten Ansatz mit Änderungen

Unabhängig von den Beweggründen und dem Umfang der vorgesehenen Migration gibt es im Allgemeinen zwei Typen von Migrationsvorgängen:

- **Lift und Shift:** In diesem Fall wird das vorhandene Datenmodell (z. B. ein Sternschema) unverändert zur neuen Azure Synapse-Plattform migriert. Der Schwerpunkt liegt hierbei auf der Minimierung des Risikos und der Zeit für die Migration, indem die erforderliche Arbeit zum Erreichen der Vorteile der Umstellung auf die Azure-Cloudumgebung verringert wird.

  Dieser Ansatz eignet sich gut für vorhandene Netezza-Umgebungen, in denen ein einzelner Data Mart migriert werden soll oder sich die Daten bereits in einem gut entworfenen Stern- oder Schneeflockenschema befinden. Auch bei Zeit- und Kostendruck für den Wechsel in eine modernere Cloudumgebung ist dieser Migrationstyp gut geeignet.

- **Phasenorientiertes Konzept unter Einbindung von Änderungen:** Wenn sich ein Legacy-Warehouse im Laufe der Zeit weiterentwickelt hat, müssen Sie es möglicherweise erneut entwickeln, um die erforderliche Leistung aufrechtzuerhalten oder neue Datenquellen wie IoT-Streams zu unterstützen. Die Migration zu Azure Synapse wegen der gut bekannten Vorteile einer skalierbaren Cloudumgebung kann als Teil des Umgestaltungsvorgangs angesehen werden. Dieser Prozess kann das Ändern des zugrunde liegenden Datenmodells wie das Verschieben eines Inmon-Modells in Azure Data Vault beinhalten.

  Zunächst sollte das vorhandene Datenmodell unverändert in Azure verschoben und dann die Leistung und Flexibilität von Azure genutzt werden, um erforderliche Überarbeitungen mithilfe von Azure-Funktionen zu übernehmen, ohne dass sich dies auf das vorhandene Quellsystem auswirkt.

### <a name="use-azure-data-factory-to-implement-a-metadata-driven-migration"></a>Verwenden von Azure Data Factory zum Implementieren einer metadatengesteuerten Migration

Es ist sinnvoll, den Migrationsprozess mithilfe der Funktionen in der Azure-Umgebung zu automatisieren und zu orchestrieren. Bei dieser Vorgehensweise werden auch die Auswirkungen auf die vorhandene Netezza-Umgebung (die möglicherweise bereits fast vollständig ausgelastet ist) minimiert.

Azure Data Factory ist ein cloudbasierter Datenintegrationsdienst, mit dem Sie datengesteuerte Workflows in der Cloud erstellen können, um Datenverschiebungen und Datentransformationen zu orchestrieren und zu automatisieren. Mit Azure Data Factory können Sie datengesteuerte Workflows (so genannte Pipelines) erstellen und planen, die Daten aus unterschiedlichen Datenspeichern erfassen. Die Anwendung kann diese Daten mithilfe von Compute Services wie Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics und Azure Machine Learning verarbeiten und transformieren.

Wenn Sie Metadaten zum Auflisten der zu migrierenden Datentabellen und deren Speicherort erstellen, können Sie die Funktionen von Azure Data Factory zum Verwalten des Migrationsprozesses verwenden.

### <a name="design-differences-between-netezza-and-azure-synapse"></a>Entwurfsunterschiede zwischen Netezza und Azure Synapse

**Mehrere Datenbanken im Vergleich zu einzelnen Datenbanken und Schemas:**

In einer Netezza-Umgebung sind manchmal mehrere separate Datenbanken für einzelne Teile der Gesamtumgebung vorhanden. Beispielsweise kann eine separate Datenbank für Datenerfassung und Stagingtabellen vorhanden sein, eine Datenbank für die zentralen Warehouse-Tabellen und eine andere Datenbank für Data Marts (manchmal auch als semantische Ebene bezeichnet). Bei der Verarbeitung von ETL/ELT-Pipelines werden möglicherweise datenbankübergreifende Joins implementiert und immer Daten zwischen diesen separaten Datenbanken verschoben.

Die Azure Synapse-Umgebung verfügt über eine einzelne Datenbank, und mithilfe von Schemas werden die Tabellen in logisch getrennte Gruppen aufgeteilt. Es wird daher empfohlen, eine Reihe von Schemas im Azure Synapse-Ziel zu verwenden, um die aus der Netezza-Umgebung migrierten einzelnen Datenbanken zu imitieren. Wenn in der Netezza-Umgebung Schemas verwendet werden, müssen Sie eventuell eine neue Benennungskonvention verwenden, um die vorhandenen Netezza-Tabellen und -Sichten in die neue Umgebung zu verschieben. Beispielsweise können das vorhandene Netezza-Schema und die Tabellennamen mit den neuen Azure Synapse-Tabellennamen verkettet werden, um über die Schemanamen in der neuen Umgebung die ursprünglichen separaten Datenbanknamen beizubehalten. Eine andere Möglichkeit ist die Verwendung von SQL-Sichten für die zugrunde liegenden Tabellen, um die logischen Strukturen beizubehalten. Dieser Ansatz bringt jedoch einige mögliche Nachteile mit sich:

- Sichten in Azure Synapse sind schreibgeschützt, sodass alle Updates an den Daten in den zugrunde liegenden Basistabellen erfolgen müssen.
- Möglicherweise gibt es bereits Ebenen von Sichten, und das Hinzufügen einer zusätzlichen Sichtebene wirkt sich auf die Leistung aus.

**Überlegungen zu Tabellen:**

Beim Migrieren von Tabellen zwischen unterschiedlichen Technologien werden in der Regel nur die Rohdaten (und die Metadaten, die sie beschreiben) physisch zwischen den beiden Umgebungen verschoben. Andere Datenbankelemente aus dem Quellsystem wie Indizes werden nicht migriert, da sie möglicherweise nicht benötigt werden oder in der neuen Zielumgebung anders implementiert sind.

Es ist jedoch wichtig zu verstehen, wo Leistungsoptimierungen wie z. B. Indizes in der Quellumgebung verwendet wurden, da diese Informationen nützliche Hinweise darauf geben können, wo eine Leistungsoptimierung in der neuen Zielumgebung umgesetzt werden kann. Wenn beispielsweise in der Netezza-Quellumgebung häufig Zonenzuordnungen von Abfragen verwendet werden, kann dies darauf hindeuten, dass in der migrierten Azure Synapse-Umgebung ein nicht gruppierter Index erstellt werden sollte, jedoch sind andere native Leistungsoptimierungstechniken wie Tabellenreplikation möglicherweise besser geeignet als eine direkt abgebildete Indexerstellung.

<!-- docsTest:ignore "NZ Toolkit" -->

**Nicht unterstützte Netezza-Datenbankobjekttypen:**

Netezza implementiert einige Datenbankobjekte, die in Azure Synapse nicht direkt unterstützt werden. Es gibt jedoch allgemeine Methoden, um die gleiche Funktionalität innerhalb der neuen Umgebung zu erreichen:

- **Zonenzuordnungen:** In Netezza werden Zonenzuordnungen für einige Spaltentypen automatisch erstellt und verwaltet. Sie werden zur Abfragezeit verwendet, um die zu scannende Datenmenge einzuschränken. Sie werden für die folgenden Spaltentypen erstellt:

  - `INTEGER` Spalten mit einer Länge von 8 Bytes oder weniger.
  - Temporale Spalten (z. B. `DATE`, `TIME` und `TIMESTAMP`).
  - `CHAR` Spalten, wenn diese Teil einer materialisierten Sicht sind und in der `ORDER BY`-Klausel erwähnt werden. Mit dem Hilfsprogramm nz_zonemap (Teil des NZ-Toolkits) können Sie herausfinden, welche Spalten Zonenzuordnungen aufweisen.

  Azure Synapse umfasst keine Zonenzuordnungen, aber ähnliche Ergebnisse können mit anderen (benutzerdefinierten) Indextypen oder Partitionierungen erzielt werden.

- **Gruppierte Basistabellen (Clustered Base Tables, CBT):** In Netezza werden CBTs am häufigsten für die Faktentabelle verwendet, die Milliarden von Datensätzen enthält. Das Scannen einer sehr großen Tabelle erfordert viel Verarbeitungszeit, da ein vollständiger Tabellenscan erforderlich sein könnte, um relevante Datensätze zu erhalten. Durch das Organisieren von Datensätzen in einer einschränkenden CBT kann Netezza Datensätze in denselben oder in der Nähe befindlichen Blöcken gruppieren, und mit diesem Prozess werden auch Zonenzuordnungen erstellt, die die Leistung verbessern, indem die zu scannende Datenmenge reduziert wird.

  In Azure Synapse kann ein ähnlicher Effekt durch die Verwendung der Partitionierung oder anderer Indizes erzielt werden.

- **Materialisierte Sichten:** Netezza unterstützt materialisierte Sichten und empfiehlt, dass eine oder mehrere davon über große Tabellen erstellt werden, die über viele Spalten verfügen, in denen nur einige dieser Spalten regelmäßig in Abfragen verwendet werden. Materialisierte Sichten werden automatisch vom System verwaltet, wenn Daten in der Basistabelle aktualisiert werden. Microsoft hat angekündigt, dass Azure Synapse ab Mai 2019 materialisierte Sichten mit der gleichen Funktionalität wie Netezza unterstützt. Dieses Feature ist nun als Vorschau verfügbar.

- **Netezza-Datentypzuordnung:** In Azure Synapse gibt es eine direkte Entsprechung für die meisten Netezza-Datentypen. In der folgenden Tabelle sind diese Datentypen und die empfohlene Vorgehensweise für ihre Zuordnung aufgeführt.

  Bestimmte Drittanbieter bieten Tools und Dienste zum Automatisieren der Migration an, einschließlich der oben beschriebenen Zuordnung von Datentypen. Wenn bereits in der Netezza-Umgebung ein ETL-Tool von Drittanbietern wie Informatica oder Talend verwendet wird, kann dieses außerdem alle erforderlichen Datentransformationen implementieren.

- **Syntaxunterschiede in SQL DML:** Es gibt einige Unterschiede in der SQL DML-Syntax (Data Manipulation Language) zwischen Netezza SQL und Azure Synapse, die bei der Migration berücksichtigt werden müssen:

  <!-- TODO: This query should probably be a code snippet that the user can copy and use. -->

  ![SQL-Abfrage (SQL query)](../../../_images/analytics/sql-query-netezza.png)

### <a name="functions-stored-procedures-and-sequences"></a>Funktionen, gespeicherte Prozeduren und Sequenzen

Bei der Migration von einer ausgereiften Legacy-Data Warehouse-Umgebung wie Netezza müssen häufig noch weitere Elemente als einfache Tabellen und Sichten zur neuen Zielumgebung migriert werden. Beispiele hierfür in Netezza sind Funktionen, gespeicherte Prozeduren und Sequenzen. In der Vorbereitungsphase sollte eine Inventur dieser zu migrierenden Objekte durchgeführt und die Methode zur Handhabung definiert werden. Dabei sollten die im Projektplan zugewiesenen Ressourcen entsprechenden zugeordnet werden.

Möglicherweise gibt es Funktionen in der Azure-Umgebung, die die als Funktionen oder gespeicherte Prozeduren in der Netezza-Umgebung implementierte Funktionalität ersetzen. In diesem Fall ist es in der Regel effizienter, die integrierten Azure-Funktionen zu verwenden, anstatt den Code der Netezza-Funktionen neu zu programmieren.

Drittanbieter bieten Tools und Dienste, die die Migration dieser Anwendungen automatisieren können (Beispiele finden Sie bei Attunity- oder Wherescape-Migrationsprodukten).

- **Funktionen:** Bei den meisten Datenbankprodukten unterstützt Netezza Systemfunktionen und auch benutzerdefinierte Funktionen in der SQL-Implementierung. Bei der Migration zu einer anderen Datenbankplattform wie Azure Synapse sind gängige Systemfunktionen allgemein verfügbar und können ohne Änderung migriert werden. Einige Systemfunktionen weisen möglicherweise eine etwas andere Syntax auf, aber die erforderlichen Änderungen können in diesem Fall automatisiert werden.

  Systemfunktionen, für die es keine Entsprechung gibt, oder unabhängige benutzerdefinierte Funktionen müssen möglicherweise mithilfe der in der Zielumgebung verfügbaren Sprachen neu programmiert werden. Benutzerdefinierte Netezza-Funktionen sind in nzlua oder C++ codiert, wohingegen Azure Synapse die beliebte Transact-SQL-Sprache für die Implementierung von benutzerdefinierten Funktionen verwendet.

- **Gespeicherte Prozeduren:** Bei den meisten modernen Datenbankprodukten können Prozeduren in der Datenbank gespeichert werden. Netezza stellt zu diesem Zweck die NZPLSQL-Sprache bereit. NZPLSQL basiert auf PostgreSQL PL/pgSQL. Eine gespeicherte Prozedur enthält normalerweise SQL-Anweisungen und prozedurale Logik und kann Daten oder einen Status zurückgeben.

  Azure SQL Data Warehouse unterstützt auch gespeicherte Prozeduren unter Verwendung von T-SQL. Zum Migrieren gespeicherter Prozeduren müssen sie dementsprechend neu programmiert werden.

- **Sequenzen:** In Netezza ist eine Sequenz ein mit CREATE SEQUENCE erstelltes benanntes Datenbankobjekt, das den eindeutigen Wert über die NEXT VALUE FOR-Methode bereitstellen kann. Mit Sequenzen können eindeutige Zahlen generiert werden, die als Ersatzschlüsselwerte für Primärschlüsselwerte verwendet werden können.

  In Azure Synapse gibt es `CREATE SEQUENCE` nicht, sodass Sequenzen mithilfe von Identitätsspalten oder SQL-Code verarbeitet werden, um die nächste Sequenznummer in einer Reihe zu erstellen.

### <a name="extracting-metadata-and-data-from-a-netezza-environment"></a>Extrahieren von Metadaten und Daten aus einer Netezza-Umgebung

- **DDL-Generierung:** Vorhandene CREATE TABLE- und CREATE VIEW-Netezza-Skripts können bearbeitet werden, um die entsprechenden Definitionen zu erstellen (bei Bedarf mit geänderten Datentypen, wie oben beschrieben). In der Regel umfasst dies das Entfernen oder Ändern zusätzlicher Netezza-spezifischer Klauseln (z. B. `ORGANIZE ON`).

  Alle Informationen, die sich auf die aktuellen Definitionen von Tabellen und Sichten in der vorhandenen Netezza-Umgebung beziehen, werden jedoch in den Systemkatalogtabellen verwaltet. Dies ist die beste Quelle für diese Informationen, da sie garantiert aktuell und vollständig ist. Die benutzerseitig verwaltete Dokumentation ist möglicherweise nicht mit den aktuellen Tabellendefinitionen synchron.

  Auf diese Informationen kann über Hilfsprogramme wie nz_ddl_table zugegriffen werden, und mit ihrer Hilfe können die CREATE TABLE-DDL-Anweisungen generiert werden, die dann für die entsprechenden Tabellen in Azure Synapse bearbeitet werden können.

  Migrations- und ETL-Tools von Drittanbietern nutzen die Informationen im Katalog auch, um das gleiche Ergebnis zu erzielen.

- **Extrahieren von Daten aus Netezza:** Die Rohdaten, die aus vorhandenen Netezza-Tabellen migriert werden sollen, können mithilfe der standardmäßigen Netezza-Hilfsprogramme wie nzsql, nzunload und über externe Tabellen in durch Trennzeichen getrennte Dateien extrahiert werden. Diese Dateien können mit gzip komprimiert und mit AzCopy in Azure Blob Storage oder mit Azure-Datentransporteinrichtungen wie Azure Data Box hochgeladen werden.

  Während einer Migration müssen die Daten so effizient wie möglich extrahiert werden. Bei Netezza sollten externe Tabellen verwendet werden, weil dies die schnellste Methode ist. Mehrere Extrahierungen können parallel ausgeführt werden, um den Durchsatz der Datenextraktion zu maximieren. Im Folgenden finden Sie ein einfaches Beispiel für die Extraktion einer externen Tabelle:

  `CREATE EXTERNAL TABLE '/tmp/export_tab1.CSV' USING (DELIM ',') AS SELECT * from <TABLENAME>;`

Wenn die Netzwerkbandbreite ausreicht, können Daten mit Azure Data Factory-Prozessen oder einer Datenmigration von Drittanbietern oder ETL-Produkten direkt aus einem lokalen Netezza-System in Azure Synapse-Tabellen oder Azure-Datenspeicher extrahiert werden.

Empfohlene Datenformate für die extrahierten Daten sind durch Trennzeichen getrennte Textdateien (auch als CSV-Dateien o. ä. bezeichnet) oder ORC- oder Parquet-Dateien (Optimized Row Columnar).

Ausführlichere Informationen zum Migrieren von Daten und ETL aus einer Netezza-Umgebung finden Sie im zugehörigen Dokument von Netezza, „Abschnitt 2.1: Datenmigration ETL und Laden.

### <a name="performance-recommendations-for-netezza-migrations"></a>Leistungsempfehlungen für Netezza-Migrationsvorgänge

- **Ähnlichkeiten in Leistungsoptimierungskonzepten:** Beim Umstieg aus einer Netezza-Umgebung sind viele der Leistungsoptimierungskonzepte für Azure SQL Data Warehouse vertraut. Beispiel:

  - Verwenden der Datenverteilung zum Zusammenstellen von Daten, die auf demselben Verarbeitungsknoten verknüpft werden sollen.
  - Wenn Sie den kleinsten Datentyp für eine bestimmte Spalte verwenden, wird Speicherplatz gespart und die Abfrageverarbeitung beschleunigt.
  - Wenn Sie sicherstellen, dass Datentypen von Spalten, die verknüpft werden sollen, identisch sind, wird die Verknüpfungsverarbeitung optimiert, da die Notwendigkeit, Daten zu transformieren, so geringer ist.
  - Wenn Sie sicherstellen, dass die Statistiken auf dem neuesten Stand sind, kann der Optimierer den besten Ausführungsplan erstellen.

- **Unterschiede in Leistungsoptimierungskonzepten:** In diesem Abschnitt werden Implementierungsunterschiede auf niedrigerer Ebene zwischen Netezza und Azure Synapse für die Leistungsoptimierung hervorgehoben.

- **Optionen für die Datenverteilung:** `CREATE TABLE`-Anweisungen in Netezza und Azure Synapse ermöglichen die Angabe einer Verteilungsdefinition über `DISTRIBUTE ON` für Netezza und `DISTRIBUTION =` in Azure Synapse.

  Eine weitere Möglichkeit im Vergleich zu Netezza, lokale Joins für Verknüpfungen kleiner Tabellen mit großen Tabellen (meist eine Dimensionstabelle mit einer Faktentabelle in einem Sternschemamodell) zu erreichen, bietet Azure Synapse mit dem Replizieren der kleineren Dimensionstabelle auf allen Knoten. Dadurch wird sichergestellt, dass für jeden Wert des Joinschlüssels der größeren Tabelle eine zugehörige Dimensionszeile lokal verfügbar ist. Der Aufwand für die Replikation der Dimensionstabellen ist relativ gering, sofern die Tabellen nicht groß sind. In diesem Fall ist der oben beschriebene Hashverteilungsansatz besser geeignet.

- **Datenindizierung:** Azure Synapse bietet verschiedene benutzerdefinierbare Indizierungsoptionen, aber diese unterscheiden sich in Betrieb und Nutzung von den systemverwalteten Zonenzuordnungen in Netezza. Lernen Sie die verschiedenen Indizierungsoptionen kennen, wie beschrieben in <!-- TODO verify link: https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-datawarehouse-tables-index -->

  Vorhandene systemverwaltete Zonenzuordnungen in der Netezza-Quellumgebung können jedoch ein nützlicher Hinweis auf die Art und Weise sein, wie die Daten derzeit verwendet werden und welche Datenspalten in der Azure Synapse-Umgebung indiziert werden sollten.

- **Datenpartitionierung:** Im Data Warehouse eines Unternehmens können Faktentabellen viele Milliarden Zeilen enthalten, und die Partitionierung ist eine Möglichkeit, die Verwaltung und Abfrage dieser Tabellen zu optimieren, indem sie in separate Teile aufgeteilt werden, um die Menge der verarbeiteten Daten zu reduzieren. Die Partitionierungsspezifikation für eine Tabelle wird in der CREATE TABLE-Anweisung definiert.

  Für die Partitionierung kann nur ein Feld pro Tabelle verwendet werden. Hierbei handelt es sich häufig um ein Datumsfeld, da viele Abfragen nach einem Datum oder Datumsbereich gefiltert werden. Sie können die Partitionierung einer Tabelle nach dem anfänglichen Laden bei Bedarf ändern. Dazu erstellen Sie die Tabelle mit der neuen Verteilung anhand der `CREATE TABLE AS SELECT`-Anweisung neu. Finden Sie unter <!-- TODO verify link https://docs.microsoft.com/en-us/azure/sql-datawarehouse/sql-data-warehouse-tables-partition --> Ausführliche Informationen zur Partitionierung in Azure Synapse.

- **PolyBase zum Laden von Daten:** PolyBase stellt die effizienteste Methode dar, große Datenmengen in das Warehouse zu laden, da hierbei parallele Ladestreams verwendet werden können.

- **Verwenden von Ressourcenklassen für die Workloadverwaltung:** Azure Synapse verwendet Ressourcenklassen zum Verwalten von Workloads. Im Allgemeinen bieten große Ressourcenklassen eine bessere Leistung bei einzelnen Abfragen, während kleinere Ressourcenklassen ein höheres Maß an Parallelität ermöglichen. Die Auslastung kann über dynamische Verwaltungssichten überwacht werden, um sicherzustellen, dass die entsprechenden Ressourcen effizient verwendet werden.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Implementieren einer Netezza-Migration erhalten Sie bei Ihrem Microsoft-Kontovertreter, der Sie gerne über lokale Migrationsangebote informiert.
