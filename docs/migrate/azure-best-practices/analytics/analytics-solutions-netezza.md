---
title: Migrieren von Netezza zu Azure Synapse Analytics
description: Informieren Sie sich über das Cloud Adoption Framework für Azure über Analyselösungen für Netezza und die Migration zu Azure Synapse Analytics.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 792f71c94d9ed16d134d444da8b467983ae9b5a8
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996331"
---
<!-- docutune:casing Informatica Talend Inmon Attunity Qlik nzLua CBT CBTs NZPLSQL DELIM TABLENAME ORC Parquet nzsql nzunload mpp -->

<!-- cSpell:ignore Informatica Talend Qlik CBTs NZPLSQL CHARINDEX DATEDIFF DELIM STRPOS TABLENAME nzsql nzunload zonemap -->

# <a name="azure-synapse-analytics-solutions-and-migration-for-netezza"></a>Azure Synapse Analytics-Lösungen und Migrieren von Netezza

Da IBM die Unterstützung für Netezza einstellt, erwägen viele Unternehmen, die derzeit auf Data-Warehouse-Systeme von Netezza setzen, die Vorteile der innovativen Cloud-, Infrastructure-as-a-Service- und Platform-as-a-Service-Angebote von neueren Umgebungen wie Azure zu nutzen. Viele Organisationen sind bereit, kostenintensive Aufgaben wie die Infrastrukturwartung und die Plattformentwicklung an einen Cloudanbieter abzugeben.

Azure Synapse Analytics ist ein unbegrenzter Analysedienst, der Data Warehousing auf Unternehmensniveau mit Big Data-Analysen vereint. Er ermöglicht flexible Datenabfragen nach Ihren Vorstellungen und im großen Stil mithilfe von serverlosen On-Demand-Ressourcen oder bereitgestellten Ressourcen. In diesem Artikel erfahren Sie, wie Sie die Migration von einem Netezza-Legacysystem zu Azure Synapse planen.

Netezza und Azure Synapse ähneln sich insofern, als dass es sich bei beiden Plattformen um SQL-Datenbanken handelt, die für die massive Parallelverarbeitung konzipiert wurden, um eine hohe Abfrageleistung für große Datenmengen zu erzielen. Dennoch unterscheiden sie sich in zentralen Aspekten:

- Legacysysteme von Netezza werden lokal installiert und verwenden proprietäre Hardware. Azure Synapse ist hingegen cloudbasiert und basiert auf Azure-Computeressourcen und -Speicherressourcen.
- Ein Upgrade einer Netezza-Konfiguration ist eine umfangreiche Aufgabe, die zusätzliche physische Hardware und eine potenziell langwierige Neukonfiguration oder das Sichern und Neuladen der Datenbank erfordert. In Azure Synapse sind die Speicher- und Computeressourcen getrennt. Dank der elastischen Skalierbarkeit von Azure können Sie flexibel hoch- und herunterskalieren.
- Da kein physisches System mehr unterstützt werden muss, kann Azure Synapse nach Bedarf angehalten oder in der Größe angepasst werden, um die Ressourcennutzung und die Kosten zu senken. Mit Azure haben Sie Zugriff auf eine weltweit verfügbare, äußerst sichere und skalierbare Cloudumgebung, die nicht nur Azure Synapse sondern auch ein Ökosystems aus unterstützenden Tools und Funktionen beinhaltet.

Im diesem Artikel finden Sie eine Übersicht über wichtige Migrationsüberlegungen und erfahren, wie Sie in Azure Synapse eine gleichwertige oder bessere Leistung der Data Warehouse-Systeme und Data Marts erzielen, die Sie aus Netezza migriert haben. Zudem werden Probleme besprochen, die speziell bei der Migration einer vorhandenen Netezza-Umgebung auftreten können.

Im Allgemeinen kann der Migrationsprozess in die Schritte untergliedert werden, die in der folgenden Tabelle aufgeführt sind:

| Vorbereitung        | Migration                             | Nach der Migration |
| :----------------- | :----------------------------- | :---------------- |
| <ul><li> Festlegen des Umfangs: Was soll migriert werden?</li><li>Erstellen eines Inventars der zu migrierenden Daten und Prozesse</li><li>Definieren der Änderungen am Datenmodell</li><li>Ermitteln der am besten geeigneten Azure- und Drittanbietertools und -features, die verwendet werden sollen</li><li>Frühzeitige Schulung von Mitarbeitern für die neue Plattform</li><li>Einrichten der Azure-Zielplattform</li></ul> |  <ul><li> Einfaches Beginnen im kleinen Umfang</li><li>Automatisieren, wann immer möglich</li><li>Verwenden von integrierten Azure-Tools und -Features zum Verringern des Migrationsaufwands</li><li>Migrieren von Metadaten für Tabellen und Sichten</li><li>Migrieren relevanter historischer Daten</li><li>Migrieren oder Umgestalten von gespeicherten Prozeduren und Geschäftsprozessen</li><li>Migrieren oder Umgestalten der inkrementelle Ladevorgänge im Rahmen von ETL/ELT</li></ul> | <ul><li> Überwachen und Dokumentieren aller Migrationsphasen</li><li>Nutzen der gewonnenen Erfahrungen zum Erstellen einer Vorlage für zukünftige Migrationsvorgänge</li><li>Neuerstellen des Datenmodells bei Bedarf unter Verwendung der Leistung und Skalierbarkeit der neuen Plattform</li><li>Testen von Anwendungen und Abfragetools</li><li>Erstellen von Benchmarks für die Abfrageleistung und Optimieren derselben</li></ul> |

Bei der Migration einer Netezza-Legacyumgebung zu Azure Synapse müssen Sie zusätzlich zu den allgemeineren Themen, die in der Netezza-Dokumentation beschrieben werden, weitere konkrete Aspekte berücksichtigen.

## <a name="initial-migration-workload"></a>Erste Migrationsworkload

Netezza-Legacyumgebungen wurden meist im Laufe der Zeit auf mehrere Themenbereiche und gemischte Workloads ausgeweitet. Bei der Entscheidung, wo das erste Migrationsprojekt ansetzen soll, sollten Sie einen Bereich auswählen, der:

- durch eine schnelle Bereitstellung der neuen Umgebung die Machbarkeit einer Migration zu Azure Synapse belegt
- den internen technischen Mitarbeitern die Möglichkeit bietet, sich mit den neuen Prozessen und Tools vertraut zu machen, um später weitere Bereiche mit diesen Prozessen und Tools migrieren zu können
- die Erstellung einer Vorlage auf Grundlage der aktuellen Tools und Prozesse, die bei weiteren Migrationen aus der Netezza-Quellumgebung zum Einsatz kommt

Üblicherweise handelt es sich bei den Bereichen, die diese Ziele unterstützen und sich daher für die erste Migration einer Netezza-Umgebung eignen, um Fachgebiete, in denen anstelle einer OLTP-Workload eine Power BI-Workload oder Analyseworkload implementiert wird. Das Datenmodell dieser Workload sollte auch ohne größere Änderungen migrierbar sein. Es sollte sich also z. B. um ein Stern- oder Schneeflockenschema handeln.

Zudem muss das bei der ersten Migration verwendete Datenvolumen groß genug sein, um die Funktionen und Vorteile der Azure Synapse-Umgebung innerhalb kurzer Zeit zu veranschaulichen. Die üblicherweise für diese Anforderungen passende Größe liegt bei 1–10 Terabyte (TB).

Eine Vorgehensweise bei der ersten Migration, die die Risiken und die Implementierungszeit minimiert, besteht in der Beschränkung der Migration auf Data Marts. Dieser Ansatz ist empfehlenswert, da der Migrationsumfang eingegrenzt wird und die Migration in kurzer Zeit durchführbar ist. Bei einer ersten Migration von Data Marts können jedoch keine umfassenderen Aspekte wie die Migration von ETL- und historischen Daten berücksichtigt werden. Diese Bereiche müssen in späteren Phasen behandelt und die migrierte Data-Mart-Ebene mit den Daten und Prozessen abgeglichen werden, die für ihre Erstellung erforderlich sind.

## <a name="lift-and-shift-approach-vs-phased-approach"></a>Lift-&-Shift-Verfahren im Vergleich zum mehrstufigen Ansatz

Unabhängig von den Treibern und dem ausgewählten Migrationsumfang stehen Ihnen zwei allgemeine Migrationstypen zur Auswahl:

- **Lift-&-Shift-Verfahren:** Bei diesem Vorgehen wird das vorhandene Datenmodell (z. B. ein Sternschema) unverändert zur neuen Azure Synapse-Plattform migriert. Ziel dieses Szenarios ist es, das Risiko sowie die Migrationsdauer zu reduzieren, indem die Arbeit verringert wird, die für die Umstellung auf die Azure-Cloudumgebung erforderlich ist.

  Dieser Ansatz eignet sich gut für vorhandene Teradata-Umgebungen, in denen ein einzelner Data Mart migriert werden soll, und für Szenarios, in denen die Daten bereits in einem gut durchdachten Stern- oder Schneeflockenschema vorliegen. Dieser Migrationstyp ist ebenfalls gut geeignet, wenn der Wechsel in eine modernere Cloudumgebung unter Zeit- und Kostendruck stattfindet.

- **Mehrstufiger Ansatz unter Einbindung von Änderungen:** Wenn ein Legacywarehouse im Laufe der Zeit weiterentwickelt wurde, müssen Sie das Data Warehouse möglicherweise überarbeiten, um die erforderliche Leistung aufrechtzuerhalten oder neue Datenquellen wie IoT-Streams zu unterstützen. Im Rahmen dieser Überarbeitung kann beispielsweise eine Migration zu Azure Synapse durchgeführt werden, um von den bekannten Vorteilen einer skalierbaren Cloudumgebung zu profitieren. Dieser Prozess kann das Ändern des zugrunde liegenden Datenmodells wie das Verschieben eines Inmon-Modells in Azure Data Vault beinhalten.

  Es wird jedoch empfohlen, das bestehende Datenmodell bei der ersten Migration unverändert zu Azure zu verschieben. Anschließend können Sie sich die Leistung und Flexibilität der Azure-Dienste zunutze machen und die Änderungen ohne Auswirkungen auf das Quellsystem umsetzen.

## <a name="metadata-migration"></a>Migration von Metadaten

Es ist sinnvoll, die Migration mithilfe der Funktionen der Azure-Umgebung zu automatisieren und zu orchestrieren. Bei dieser Vorgehensweise werden die Auswirkungen auf die vorhandene Netezza-Umgebung minimiert, die möglicherweise bereits fast vollständig ausgelastet ist.

Azure Data Factory ist ein cloudbasierter Datenintegrationsdienst. Er ermöglicht Ihnen das Erstellen datengesteuerter Workflows in der Cloud, um die Datenverschiebung und -transformation zu orchestrieren und zu automatisieren. Data Factory-Pipelines können Daten aus unterschiedlichen Datenspeichern erfassen und diese dann mithilfe von Computediensten wie Azure HDInsight für Apache Hadoop und Apache Spark, Azure Data Lake Analytics sowie Azure Machine Learning verarbeiten und transformieren. Dazu erstellen Sie zunächst Metadaten, um die zu migrierenden Datentabellen und deren Speicherort aufzulisten. Anschließend verwalten Sie den Migrationsprozess mithilfe der Funktionen von Azure Data Factory.

## <a name="design-differences-between-netezza-and-azure-synapse"></a>Entwurfsunterschiede zwischen Netezza und Azure Synapse

Bei der Planung einer Migration von einer Netezza-Legacyumgebung zu Azure Synapse ist es wichtig, die Entwurfsunterschiede zwischen beiden Plattformen zu berücksichtigen.

### <a name="multiple-databases-vs-a-single-database-and-schemas"></a>Mehrere Datenbanken im Vergleich zu einem Singleton und Schemas

In einer Netezza-Umgebung werden verschiedene Teile der Gesamtumgebung unter Umständen auf mehreren separaten Datenbanken bereitgestellt. Zum Beispiel verfügen Sie möglicherweise über eine separate Datenbank für die Datenerfassung und Stagingtabellen, eine Datenbank für zentrale Warehouse-Tabellen und eine weitere Datenbank für Data Marts, die manchmal auch als _semantische Ebene_ bezeichnet wird. Die Verarbeitung von separaten Datenbanken als ETL-/ELT-Pipelines in Azure Synapse erfordert möglicherweise die Implementierung von datenbankübergreifenden Verknüpfungen und die Verschiebung von Daten zwischen den separaten Datenbanken.

Die Azure Synapse-Umgebung verfügt über ein Singleton. Tabellen werden mithilfe von Schemas in logisch getrennte Gruppen unterteilt. Es wird empfohlen, die separaten Datenbanken, die Sie von Netezza migrieren, mithilfe von mehreren Schemas in der Azure Synapse-Zielumgebung zu imitieren. Falls Sie in der Netezza-Umgebung Schemas verwendet haben, müssen Sie möglicherweise die Namenskonvention ändern, um die vorhandenen Netezza-Tabellen und -Sichten in die neue Umgebung verschieben zu können. Sie können beispielsweise die vorhandenen Netezza-Schema- und -Tabellennamen mit dem neuen Azure Synapse-Tabellennamen verketten und mithilfe der Schemanamen die Namen der ursprünglichen separaten Datenbanken in der neuen Umgebung beibehalten.

Eine andere Möglichkeit ist die Verwendung von SQL-Sichten für die zugrunde liegenden Tabellen, um die logischen Strukturen beizubehalten. SQL-Sichten weisen die folgenden potenziellen Nachteile auf:

- Azure Synapse-Sichten sind schreibgeschützt, sodass alle Updates an den Daten in den zugrunde liegenden Basistabellen erfolgen müssen.
- Wenn bereits verschiedene Sichtebenen bestehen, wirken sich weitere Sichtebenen möglicherweise negativ auf die Leistung aus.

### <a name="tables"></a>Tabellen

Beim Migrieren von Tabellen zwischen unterschiedlichen Technologien werden nur die Rohdaten sowie die Metadaten, die diese beschreiben, physisch zwischen den beiden Umgebungen verschoben. Datenbankelemente wie Indizes werden nicht aus dem Quellsystem migriert, da diese möglicherweise nicht benötigt oder in der neuen Umgebung anders implementiert werden.

Das Wissen, wo Leistungsoptimierungen wie Indizes in der Quellumgebung eingesetzt wurden, kann jedoch Hinweise darauf geben, an welcher Stelle in der neuen Umgebung Optimierungspotenzial besteht. Wenn bei Abfragen in der Netezza-Quellumgebung z. B. häufig Zonenzuordnungen verwendet wurden, kann es vorteilhaft sein, in der migrierten Azure Synapse-Umgebung einen nicht gruppierten Index zu erstellen. Alternativ können Zonenzuordnungen ebenfalls darauf hindeuten, dass andere native Techniken zur Leistungsoptimierung, z. B. die Tabellenreplikation, der Erstellung eines Like-for-Like-Indexes vorzuziehen sind.

<!-- docutune:casing "NZ Toolkit" -->

### <a name="unsupported-netezza-database-object-types"></a>Nicht unterstützte Typen von Netezza-Datenbankobjekten

In Netezza werden einige Datenbankobjekte implementiert, die in Azure Synapse nicht direkt unterstützt werden. Azure Synapse bietet jedoch Methoden, mit denen Sie dieselbe Funktionalität in der neuen Umgebung erzielen können. Dies wird in der folgenden Liste beschrieben:

- **Zonenzuordnungen:** In Netezza werden Zonenzuordnungen für einige Spaltentypen automatisch erstellt und verwaltet. Zonenzuordnungen werden zur Abfragezeit für die folgenden Spaltentypen verwendet, um die zu scannende Datenmenge einzuschränken:

  - `INTEGER`-Spalten mit einer Länge von höchstens 8 Byte
  - Temporale Spalten, einschließlich `DATE`, `TIME` und `TIMESTAMP`
  - `CHAR`-Spalten, wenn diese Teil einer materialisierten Sicht und der `ORDER BY`-Klausel sind

  Mit dem Hilfsprogramm „nz_zonemap“ können Sie herausfinden, welche Spalten über Zonenzuordnungen verfügen. Das Hilfsprogramm ist Teil des NZ-Toolkits.

  In Azure Synapse werden keine Zonenzuordnungen verwendet. Es ist jedoch möglich, ähnliche Ergebnisse mit benutzerdefinierten Indextypen oder Partitionierungen zu erzielen.

- **Gruppierte Basistabellen (Clustered Base Tables, CBT):** Die häufigste gruppierte Basistabelle in Netezza ist die Faktentabelle, die Milliarden von Datensätzen enthält. Das Scannen einer sehr großen Tabelle erfordert eine hohe Verarbeitungszeit, da ein vollständiger Tabellenscan erforderlich sein könnte, um relevante Datensätze zu erhalten. Durch das Organisieren von Datensätzen in restriktiven gruppierten Basistabellen können Datensätze in Netezza in derselben oder nahe gelegenen Erweiterungen gruppiert werden. Bei diesem Vorgang werden auch Zonenzuordnungen erstellt, die die Leistung durch eine Verkleinerung der zu scannenden Datenmenge verbessern.

  In Azure Synapse können Sie ein ähnliches Ergebnis durch Partitionierungen oder durch die Verwendung anderer Indextypen erzielen.

- **Materialisierte Sichten:** Für Netezza wird empfohlen, dass Benutzer mindestens eine materialisierte Sicht für große Tabellen erstellen, die über viele Spalten verfügen und in denen nur einige dieser Spalten regelmäßig abgefragt werden. Materialisierte Sichten werden automatisch vom System verwaltet, wenn Daten in der Basistabelle aktualisiert werden.

  Microsoft bietet in Azure Synapse aktuell Vorschausupport für materialisierte Sichten mit der gleichen Funktionalität wie Netezza an.

- **Datentypzuordnung:** In Azure Synapse gibt es eine direkte Entsprechung für die meisten Netezza-Datentypen. In der folgenden Tabelle sind die Datentypen und die empfohlenen Vorgehensweisen für die Zuordnung der Datentypen aufgeführt.

  Einige Drittanbieter bieten Tools und Dienste an, mit denen Migrationstasks automatisiert werden können, einschließlich der Datentypzuordnung. Wenn in der Netezza-Umgebung bereits ein ETL-Tool von Drittanbietern wie Informatica oder Talend verwendet wird, können Sie damit alle erforderlichen Datentransformationen implementieren.

- **Syntax der SQL-Datenbearbeitungssprache (DML):** Zwischen der Syntax der SQL-Datenbearbeitungssprache von Netezza SQL und Azure Synapse bestehen einige Unterschiede, die Sie beachten sollten.

  Nachstehend finden Sie eine Übersicht über die wichtigsten Funktionen und die Unterschiede:

  - `STRPOS`: In Netezza gibt die Funktion `STRPOS` die Position einer Teilzeichenfolge innerhalb einer Zeichenfolge zurück. Die entsprechende Funktion in Azure Synapse ist `CHARINDEX`, die Reihenfolge der Argumente ist jedoch umgekehrt.

    In Netezza:

    `SELECT STRPOS('abcdef', 'def') ...`

    Wird in Azure Synapse durch den folgenden Code ersetzt:

    `SELECT CHARINDEX('def', 'abcdef') ...`

  - `AGE`: Netezza unterstützt den `AGE`-Operator, um das Intervall zwischen zwei temporalen Werten zu ermitteln, z. B. zwischen Zeitstempeln und Datumsangaben. Beispiel:

    `SELECT AGE ('23-03-1956', '01-01-2019') FROM ...`

    Sie können dasselbe Ergebnis in Azure Synapse mithilfe von `DATEDIFF` erzielen. Beachten Sie dabei die Sequenz mit der Datumsdarstellung:

    `SELECT DATEDIFF(day, '1956-03-23', '2019-01-01') FROM ...`

  - `NOW()`: Netezza verwendet `NOW()`, um `CURRENT_TIMESTAMP` in Azure Synapse darzustellen.

## <a name="functions-stored-procedures-and-sequences"></a>Funktionen, gespeicherte Prozeduren und Sequenzen

Bei der Migration eines Data Warehouse aus einer ausgereiften Legacyumgebung wie Netezza müssen häufig noch weitere Elemente außer einfachen Tabellen und Sichten in die neue Zielumgebung migriert werden. Beispiele für Netezza-Elemente, die keine Tabellen sind und möglicherweise zu Azure Synapse migriert werden müssen, sind Funktionen, gespeicherte Prozeduren und Sequenzen. Während der Vorbereitung der Migration sollten Sie ein Inventar der zu migrierenden Objekte erstellen. Definieren Sie im Projektplan die Methode für die Verarbeitung aller Objekte, und weisen Sie die entsprechenden Ressourcen für die Migration zu.

Möglicherweise gibt es Dienste in der Azure-Umgebung, die die Funktionalität ersetzen, die in Form von Funktionen oder gespeicherten Prozeduren in der Netezza-Umgebung implementiert wurde. In der Regel ist es effizienter, die integrierten Azure-Funktionen zu verwenden, anstatt die Netezza-Funktionen neu zu schreiben.

Es gibt zudem viele Drittanbietertools und -dienste, mit denen die Migration von Funktionen, gespeicherten Prozeduren und Sequenzen aus Netezza automatisiert werden kann. Beispiele sind Qlik (ehemals Attunity) und WhereScape.

Nachstehend sind einige zusätzliche Informationen zur Migration von Funktionen, gespeicherten Prozeduren und Sequenzen aufgeführt:

- **Funktionen:** Wie bei den meisten Datenbankprodukten unterstützt Netezza Systemfunktionen und benutzerdefinierte Funktionen in einer SQL-Implementierung. Werden gängige Systemfunktionen zu einer anderen Datenbankplattform wie Azure Synapse migriert, sind diese allgemein in der neuen Umgebung verfügbar und können ohne Änderung migriert werden. Wenn Systemfunktionen in der neuen Umgebung eine leicht veränderte Syntax aufweisen, können Sie die erforderlichen Änderungen normalerweise automatisieren.

  Zu diesem Zweck müssen Sie möglicherweise beliebige benutzerdefinierte Funktionen und Systemfunktionen neu schreiben, wenn diese keine Entsprechung in der neuen Umgebung aufweisen. Nutzen Sie dazu die Sprachen, die in der neuen Umgebung verfügbar sind. Benutzerdefinierte Netezza-Funktionen werden in nzLua oder C++ programmiert. In Azure Synapse werden benutzerdefinierte Funktionen mithilfe der weit verbreiteten Sprache „Transact-SQL“ implementiert.

- **Gespeicherte Prozeduren:** In den meisten modernen Datenbankprodukten können Sie Prozeduren in der Datenbank speichern. Eine gespeicherte Prozedur enthält üblicherweise SQL-Anweisungen und etwas prozedurale Logik. Möglicherweise gibt die Prozedur auch Daten oder einen Zustand zurück.

  Netezza stellt die auf PL/pgSQL basierende Sprache NZPLSQL für gespeicherte Prozeduren bereit. Azure Synapse unterstützt gespeicherte Prozeduren mithilfe von T-SQL. Wenn Sie gespeicherte Prozeduren zu Azure Synapse migrieren, müssen Sie diese in T-SQL neu programmieren.

- **Sequenzen:** Bei einer Sequenz handelt es sich in Netezza um ein benanntes Datenbankobjekt, das mit einer `CREATE SEQUENCE`-Anweisung erstellt wird. Objekte können den eindeutigen Wert über die Methode `NEXT()` bereitstellen. Mit Werten können eindeutige Zahlen als Ersatzschlüsselwerte für Primärschlüsselwerte generiert werden.

  `CREATE SEQUENCE` wird in Azure Synapse nicht unterstützt. In Azure Synapse werden Sequenzen mithilfe von Identitätsspalten oder SQL-Code verarbeitet, um die nächste Sequenzzahl in einer Reihe zu erstellen.

## <a name="metadata-and-data-extraction"></a>Metadaten und Datenextraktion

Berücksichtigen Sie die folgenden Informationen bei der Planung der Metadaten- und Datenextraktion aus der Netezza-Umgebung:

- **Generieren von DDL-Anweisungen (Data Definition Language, Datendefinitionssprache):** Vorhandene `CREATE TABLE`- und `CREATE VIEW`-Skripts in Netezza können bearbeitet werden, um die entsprechenden Definitionen zu erstellen (bei Bedarf mit geänderten Datentypen, wie zuvor beschrieben). Diese Aufgabe umfasst in der Regel das Entfernen oder Ändern von Netezza-spezifischen Klauseln, z. B. `ORGANIZE ON`.

  In Netezza werden die Informationen, die die aktuellen Tabellen- und Sichtdefinitionen angeben, in den Systemkatalogtabellen verwaltet. Systemkatalogtabellen sind die beste Quelle für diese Informationen, weil sie mit hoher Wahrscheinlichkeit auf dem neuesten Stand und vollständig sind. Die benutzerseitig verwaltete Dokumentation ist möglicherweise nicht mit den aktuellen Tabellendefinitionen synchron.

Sie können mithilfe eines Hilfsprogramms wie „nz_ddl_table“ in Netezza auf Systemkatalogtabellen zugreifen. Mithilfe dieser Tabellen können Sie `CREATE TABLE`-DDL-Anweisungen generieren, die Sie dann für die entsprechenden Tabellen in Azure Synapse bearbeiten können. Migrations- und ETL-Tools von Drittanbietern verwenden dieselben Kataloginformationen, um dasselbe Ergebnis zu erzielen.

- **Datenextraktion:** Mithilfe von standardmäßig verfügbaren Netezza-Hilfsprogrammen wie „nzsql“ und „nzunload“ sowie mithilfe von externen Tabellen können Sie Rohdaten extrahieren, um diese aus einer vorhandenen Netezza-Tabelle in eine durch Trennzeichen getrennte Flatfile zu migrieren. Komprimieren Sie die Dateien mithilfe von gzip, und nutzen Sie anschließend AzCopy oder einen Azure-Datentransportdienst wie Azure Data Box, um die Dateien in Azure Blob Storage hochzuladen.

  Während einer Migration müssen Daten so effizient wie möglich extrahiert werden. In Bezug auf Netezza wird empfohlen, externe Tabellen zu verwenden, weil dies die schnellste Methode ist. Sie können mehrere Extraktionen parallel ausführen, um den Durchsatz der Datenextraktion zu maximieren.

Im Folgenden finden Sie ein einfaches Beispiel für die Extraktion einer externen Tabelle:

  `CREATE EXTERNAL TABLE '/tmp/export_tab1.CSV' USING (DELIM ',') AS SELECT * from <TABLE-NAME>;`

   Wenn Ihre Netzwerkbandbreite ausreichend hoch ist, können Sie Daten mit Azure Data Factory-Prozessen, mit einer Datenmigration über einen Drittanbieter oder mit ETL-Produkten direkt aus einem lokalen Netezza-System in Azure Synapse-Tabellen oder einen Azure-Datenspeicher extrahieren.

   Empfohlene Datenformate für die extrahierten Daten sind _durch Trennzeichen getrennte Textdateien_ (auch CSV-Dateien genannt) oder ORC- oder Parquet-Dateien (Optimized Row Columnar).

Ausführlichere Informationen zum Migrieren von Daten und ETL-Prozessen aus einer Netezza-Umgebung finden Sie in der Netezza-Dokumentation über ETL-Prozesse und das Laden bei der Datenmigration.

## <a name="performance-tuning-recommendations"></a>Empfehlungen für die Leistungsoptimierung

Wenn Sie von einer Netezza-Umgebung auf Azure Synapse umsteigen, sind Sie bereits mit vielen der für die Leistungsoptimierung eingesetzten Techniken vertraut.

Im Folgenden finden Sie ein Beispiele für die Techniken, die in beiden Umgebungen identisch sind:

- Mithilfe der Datenverteilung werden Daten zusammengestellt, die auf demselben Verarbeitungsknoten verknüpft werden sollen.
- Durch die Verwendung des kleinsten Datentyps für eine bestimmte Spalte wird Speicherplatz gespart und die Abfrageverarbeitung beschleunigt.
- Wenn Sie sicherstellen, dass die Datentypen von Spalten, die verknüpft werden sollen, identisch sind, wird die Verknüpfungsverarbeitung optimiert, da die Notwendigkeit einer Datentransformation verringert wird.
- Indem Sie sicherstellen, dass die Statistiken auf dem neuesten Stand sind, kann der Optimierer den besten Ausführungsplan erstellen.

In Bezug auf die Optimierung bestehen gewisse Unterschiede zwischen den Plattformen. In der folgenden Übersicht der Empfehlungen zur Leistungsoptimierung werden spezifische Unterschiede zwischen Netezza und Azure Synapse sowie Migrationsalternativen hervorgehoben:

- **Optionen für die Datenverteilung:** Sie können sowohl in Netezza als auch in Azure Synapse mit einer `CREATE TABLE`-Anweisung eine Verteilungsdefinition angeben. Verwenden Sie `DISTRIBUTE ON` für Netezza und `DISTRIBUTION =` für Azure Synapse.

   Azure Synapse sieht eine zusätzliche Methode vor, um kleine und große Tabellen in einem Sternschemamodell lokal zu verknüpfen. Dies wird oft als _Verknüpfung zwischen einer Dimensions- und einer Faktentabelle_ bezeichnet. Bei diesem Vorgang wird die kleinere Dimensionstabelle auf allen Knoten repliziert. Dies stellt sicher, dass jeder Wert des Verknüpfungsschlüssels für die größere Tabelle eine übereinstimmende Dimensionszeile enthält, die lokal verfügbar ist. Der Mehraufwand für die Replikation der Dimensionstabelle ist relativ gering, sofern die Tabellen nicht groß sind. Andernfalls wäre die Verwendung einer Hashverteilung (wie zuvor beschrieben) vorzuziehen.

- **Datenindizierung:** Azure Synapse bietet verschiedene benutzerdefinierbare Indizierungsoptionen. Diese unterscheiden sich jedoch in der Funktionsweise und der Nutzung von den systemseitig verwalteten Zonenzuordnungen in Netezza. Weitere Informationen zu den Indizierungsoptionen in Azure Synapse finden Sie unter [Indextabellen in einem Azure Synapse-SQL-Pool](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-index).

   Vorhandene systemseitig verwaltete Zonenzuordnungen in der Netezza-Quellumgebung können einen nützlichen Hinweis auf die aktuelle Verwendungsweise von Daten geben. Außerdem können sie darauf hindeuten, welche Spalten in der Azure Synapse-Umgebung indiziert werden sollten.

- **Datenpartitionierung:** Im Data Warehouse eines Unternehmens können Faktentabellen Milliarden von Datenzeilen enthalten. Die Partitionierung ist eine Methode, um die Wartung und das Abfragen dieser Tabellen zu optimieren. Durch Aufteilen der Tabellen in separate Teile wird die Menge der Daten reduziert, die gleichzeitig verarbeitet werden. Die Partitionierung einer Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

  Für die Partitionierung kann nur ein Feld pro Tabelle verwendet werden. Bei dem für die Partitionierung verwendeten Feld handelt es sich häufig um ein Datumsfeld, da viele Abfragen nach Datum oder nach einem Datumsbereich gefiltert werden. Die Partitionierung einer Tabelle kann nach dem ersten Laden geändert werden. Zu diesem Zweck müssen Sie die Tabelle mit einer neuen Verteilung neu erstellen, die die `CREATE TABLE AS SELECT`-Anweisung verwendet. Eine ausführliche Erläuterung der Partitionierung in Azure Synapse finden Sie unter [Partitionieren von Tabellen in einem Synapse-SQL-Pool](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition).

- **PolyBase zum Laden von Daten:** PolyBase ist die effizienteste Methode, um große Datenmengen in ein Warehouse zu laden. Mit PolyBase können Daten auch in parallelen Streams geladen werden.

- **Ressourcenklassen für die Workloadverwaltung:** Azure Synapse verwendet Ressourcenklassen zum Verwalten von Workloads. Im Allgemeinen verbessern große Ressourcenklassen die Leistung einzelner Abfragen. Kleinere Ressourcenklassen hingegen erhöhen das Maß von Parallelität. Sie können die Auslastung über dynamische Verwaltungssichten überwachen, um sicherzustellen, dass die entsprechenden Ressourcen effizient verwendet werden.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Implementieren einer Netezza-Migration erhalten Sie bei Ihrem Microsoft-Ansprechpartner, der Sie gern über Angebote für lokale Migrationen informiert.
