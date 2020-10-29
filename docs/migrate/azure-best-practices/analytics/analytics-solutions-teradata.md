---
title: Migrieren von Teradata zu Azure Synapse Analytics
description: Informieren Sie sich über das Cloud Adoption Framework für Azure über Analyselösungen für Teradata und die Migration zu Azure Synapse Analytics.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7df0db259902f3b840c21138e111f06ab492aca4
ms.sourcegitcommit: c1d6c1c777475f92a3f8be6def84f1779648a55c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2020
ms.locfileid: "92334798"
---
<!-- cSpell:ignore DATEADD DATEDIFF Inmon NUSI Informatica Talend BTEQ FASTEXPORT QUALIFY ORC Parquet "Parallel Data Transporter" Attunity "Qlik Replicate" -->

# <a name="azure-synapse-analytics-solutions-and-migration-for-teradata"></a>Azure Synapse Analytics-Lösungen und Migrieren von Teradata

Viele Organisationen sind bereit, kostenintensive Data Warehouse-Aufgaben wie die Infrastrukturwartung und die Plattformentwicklung an einen Cloudanbieter abzugeben. Unternehmen erwägen jetzt, innovative Cloud-, Infrastructure-as-a-Service- und Platform-as-a-Service-Angebote in neueren Umgebungen wie Azure zu nutzen.


Azure Synapse Analytics ist ein unbegrenzter Analysedienst, der Data Warehousing auf Unternehmensniveau mit Big Data-Analysen vereint. Er ermöglicht flexible Datenabfragen nach Ihren Vorstellungen und im großen Stil mithilfe von serverlosen On-Demand-Ressourcen oder bereitgestellten Ressourcen. In diesem Artikel erfahren Sie, wie Sie die Migration von einem Teradata-Legacysystem zu Azure Synapse planen.

Teradata und Azure Synapse ähneln sich insofern, als dass es sich bei beiden Plattformen um SQL-Datenbanken handelt, die für die massive Parallelverarbeitung konzipiert wurden, um eine hohe Abfrageleistung für große Datenmengen zu erzielen. Dennoch weisen Sie einige grundlegende Unterschiede auf:

- Legacysysteme von Teradata werden lokal installiert und verwenden proprietäre Hardware. Azure Synapse ist hingegen cloudbasiert und basiert auf Azure-Computeressourcen und -Speicherressourcen.
- Ein Upgrade einer Teradata-Konfiguration ist eine umfangreiche Aufgabe, die zusätzliche physische Hardware und eine potenziell langwierige Neukonfiguration oder das Sichern und Neuladen der Datenbank erfordert. In Azure Synapse sind Compute- und Speicherressourcen voneinander getrennt, sodass Sie dank der elastischen Skalierbarkeit von Azure problemlos zentral hoch- oder herunterskalieren können.
- Da kein physisches System mehr unterstützt werden muss, kann Azure Synapse nach Bedarf angehalten oder in der Größe angepasst werden, um die Ressourcennutzung und die Kosten zu senken. Mit Azure haben Sie Zugriff auf eine weltweit verfügbare, äußerst sichere und skalierbare Cloudumgebung, die nicht nur Azure Synapse sondern auch ein Ökosystems aus unterstützenden Tools und Funktionen beinhaltet.

Im diesem Artikel finden Sie eine Übersicht über wichtige Migrationsüberlegungen und erfahren, wie Sie in Azure Synapse eine gleichwertige oder bessere Leistung der Data Warehouse-Systeme und Data Marts erzielen, die Sie aus Teradata migriert haben. Zudem werden Probleme besprochen, die speziell bei der Migration einer vorhandenen Teradata-Umgebung auftreten können.

Im Allgemeinen kann der Migrationsprozess in die Schritte untergliedert werden, die in der folgenden Tabelle aufgeführt sind:

| Vorbereitung        | Migration                             | Nach der Migration |
| :----------------- | :----------------------------- | :---------------- |
| <ul><li> Festlegen des Umfangs: Was soll migriert werden?</li><li>Erstellen eines Inventars der zu migrierenden Daten und Prozesse</li><li>Definieren der Änderungen am Datenmodell</li><li>Ermitteln der am besten geeigneten Azure- und Drittanbietertools und -features, die verwendet werden sollen</li><li>Frühzeitige Schulung von Mitarbeitern für die neue Plattform</li><li>Einrichten der Azure-Zielplattform</li></ul> |  <ul><li>Einfaches Beginnen im kleinen Umfang</li><li>Automatisieren, wann immer möglich</li><li>Verwenden von integrierten Azure-Tools und -Features zum Verringern des Migrationsaufwands</li><li>Migrieren von Metadaten für Tabellen und Sichten</li><li>Migrieren relevanter historischer Daten</li><li>Migrieren oder Umgestalten von gespeicherten Prozeduren und Geschäftsprozessen</li><li>Migrieren oder Umgestalten von ETL/ELT-Prozessen für inkrementelles Laden</li></ul> | <ul><li> Überwachen und Dokumentieren aller Migrationsphasen</li><li>Nutzen der gewonnenen Erfahrungen zum Erstellen einer Vorlage für zukünftige Migrationsvorgänge</li><li>Neuerstellen des Datenmodells bei Bedarf unter Verwendung der Leistung und Skalierbarkeit der neuen Plattform</li><li>Testen von Anwendungen und Abfragetools</li><li>Erstellen von Benchmarks für die Abfrageleistung und Optimieren derselben</li></ul> |

Bei der Migration einer Teradata-Legacyumgebung zu Azure Synapse müssen Sie zusätzlich zu den allgemeineren Themen, die in der Teradata-Dokumentation beschrieben werden, weitere konkrete Aspekte berücksichtigen.

## <a name="initial-migration-workload"></a>Erste Migrationsworkload

Teradata-Legacyumgebungen wurden meist im Laufe der Zeit auf mehrere Themenbereiche und gemischte Workloads ausgeweitet. Bei der Entscheidung, wo das erste Migrationsprojekt ansetzen soll, sollten Sie einen Bereich auswählen, der:

- durch eine schnelle Bereitstellung der neuen Umgebung die Machbarkeit einer Migration zu Azure Synapse belegt
- den internen technischen Mitarbeitern die Möglichkeit bietet, sich mit den neuen Prozessen und Tools vertraut zu machen, um später weitere Bereiche mit diesen Prozessen und Tools migrieren zu können
- eine Vorlage auf Grundlage der aktuellen Tools und Prozesse erstellt, die bei weiteren Migrationen aus der Teradata-Quellumgebung zum Einsatz kommt

Üblicherweise handelt es sich bei den Bereichen, die diese Ziele unterstützen und sich daher für die erste Migration einer Teradata-Umgebung eignen, um Fachgebiete, in denen anstelle einer OLTP-Workload eine Power BI-Workload oder Analyseworkload implementiert wird. Das Datenmodell dieser Workload sollte auch ohne größere Änderungen migrierbar sein. Es sollte sich also z. B. um ein Stern- oder Schneeflockenschema handeln.

Zudem muss das bei der ersten Migration verwendete Datenvolumen groß genug sein, um die Funktionen und Vorteile der Azure Synapse-Umgebung innerhalb kurzer Zeit zu veranschaulichen. Die üblicherweise für diese Anforderungen passende Größe liegt bei 1–10 Terabyte (TB).

Eine Vorgehensweise bei der ersten Migration, die die Risiken und die Implementierungszeit minimiert, besteht in der Beschränkung der Migration auf Data Marts. Ein gutes Beispiel für Teradata ist der OLAP-Datenbankteil eines Teradata-Data Warehouse. Dieser Ansatz ist empfehlenswert, da der Migrationsumfang eingegrenzt wird und die Migration häufig in kurzer Zeit durchführbar ist.

Bei einer ersten Migration von Data Marts können jedoch keine umfassenderen Aspekte wie die Migration von ETL- und historischen Daten berücksichtigt werden. Diese Bereiche müssen in späteren Phasen behandelt und die migrierte Data-Mart-Ebene mit den Daten und Prozessen abgeglichen werden, die für ihre Erstellung erforderlich sind.

## <a name="lift-and-shift-approach-vs-phased-approach"></a>Lift-&-Shift-Verfahren im Vergleich zum mehrstufigen Ansatz

Unabhängig von den Treibern und dem ausgewählten Migrationsumfang stehen Ihnen zwei allgemeine Migrationstypen zur Auswahl:

- **Lift-&-Shift-Verfahren:** Bei diesem Vorgehen wird das vorhandene Datenmodell (z. B. ein Sternschema) unverändert zur neuen Azure Synapse-Plattform migriert. Ziel ist es, das Risiko sowie die Migrationsdauer zu reduzieren, indem die Arbeit verringert wird, die für die Umstellung auf die Azure-Cloudumgebung erforderlich ist.

  Dieser Ansatz eignet sich gut für vorhandene Teradata-Umgebungen, in denen ein einzelner Data Mart migriert werden soll, und für Szenarios, in denen die Daten bereits in einem gut durchdachten Stern- oder Schneeflockenschema vorliegen. Dieser Migrationstyp ist ebenfalls gut geeignet, wenn der Wechsel in eine modernere Cloudumgebung unter Zeit- und Kostendruck stattfindet.

- **Mehrstufiger Ansatz unter Einbindung von Änderungen:** Wenn Ihr Legacywarehouse im Laufe der Zeit weiterentwickelt wurde, müssen Sie das Data Warehouse möglicherweise überarbeiten, um die erforderliche Leistung aufrechtzuerhalten oder neue Datenquellen wie IoT-Streams zu unterstützen. Im Rahmen dieser Überarbeitung kann beispielsweise eine Migration zu Azure Synapse durchgeführt werden, um von den bekannten Vorteilen einer skalierbaren Cloudumgebung zu profitieren. Dieser Prozess kann das Ändern des zugrunde liegenden Datenmodells wie das Verschieben eines Inmon-Modells in Azure Data Vault beinhalten.

  Es wird jedoch empfohlen, das bestehende Datenmodell bei der ersten Migration unverändert zu Azure zu verschieben. Anschließend können Sie sich die Leistung und Flexibilität der Azure-Dienste zunutze machen und die Änderungen ohne Auswirkungen auf das Quellsystem umsetzen.

## <a name="virtual-machine-colocation-to-support-migration"></a>Zusammenstellung des virtuellen Computers zur Unterstützung der Migration

Bei einem optionaler Ansatz für die Migration aus einer lokalen Teradata-Umgebung wird kostengünstiger Cloudspeicher und elastische Skalierbarkeit in Azure genutzt. Zuerst erstellen Sie eine Teradata-Instanz auf einem virtuellen Azure-Computer, der mit der Azure Synapse-Zielumgebung zusammengestellt wird. Dann verwenden Sie ein Teradata-Standardhilfsprogramm wie Teradata Parallel Transporter oder ein Datenreplikationstool eines Drittanbieters wie Qlik Replicate (ehemals von Attunity), um die Teilmenge der Teradata-Tabellen, die Sie in die VM-Instanz migrieren, effizient zu verschieben. Alle Migrationsaufgaben erfolgen in der Azure-Umgebung.

Dieser Ansatz hat mehrere Vorteile:

- Nach der ersten Replikation von Daten wird das Quellsystem von weiteren Migrationsaufgaben nicht weiter beeinträchtigt.
- Vertraute Teradata-Schnittstellen, -Tools und -Hilfsprogramme sind in der Azure-Umgebung verfügbar.
- Nach der Migration zur Azure-Umgebung gibt es keine potenziellen Probleme mehr mit der Verfügbarkeit von Netzwerkbandbreite zwischen dem lokalen Quellsystem und dem Cloudzielsystem.
- Tools wie Azure Data Factory können effizient Hilfsprogramme wie Teradata Parallel Transporter aufrufen, um Daten schnell und einfach zu migrieren.
- Der Migrationsprozess wird vollständig in der Azure-Umgebung orchestriert und gesteuert.

## <a name="metadata-migration"></a>Migration von Metadaten

Es ist sinnvoll, die Migration mithilfe der Funktionen der Azure-Umgebung zu automatisieren und zu orchestrieren. Bei dieser Vorgehensweise werden die Auswirkungen auf die vorhandene Teradata-Umgebung, die möglicherweise bereits fast vollständig ausgelastet ist, minimiert.

Azure Data Factory ist ein cloudbasierter Datenintegrationsdienst. Er ermöglicht Ihnen das Erstellen datengesteuerter Workflows in der Cloud, um die Datenverschiebung und -transformation zu orchestrieren und zu automatisieren. Data Factory-Pipelines können Daten aus unterschiedlichen Datenspeichern erfassen. Dann können diese die Daten mithilfe von Compute Services wie Azure HDInsight für Apache Hadoop und Apache Spark, Azure Data Lake Analytics und Azure Machine Learning verarbeiten und transformieren.

Beginnen Sie mit dem Erstellen von Metadaten, die die zu migrierenden Datentabellen zusammen mit ihren Speicherorten auflisten. Verwenden Sie dann Data Factory-Funktionen, um den Migrationsprozess zu verwalten.

## <a name="design-differences-between-teradata-and-azure-synapse"></a>Entwurfsunterschiede zwischen Teradata und Azure Synapse

Bei der Planung einer Migration von einer Teradata-Legacyumgebung zu Azure Synapse ist es wichtig, die Entwurfsunterschiede zwischen beiden Plattformen zu berücksichtigen.

### <a name="multiple-databases-vs-a-single-database-and-schemas"></a>Mehrere Datenbanken im Vergleich zu einem Singleton und Schemas

In einer Teradata-Umgebung werden verschiedene Teile der Gesamtumgebung unter Umständen auf mehreren separaten Datenbanken bereitgestellt. Beispielsweise kann eine separate Datenbank für die Datenerfassung und Stagingtabellen vorhanden sein, eine Datenbank für zentrale Warehouse-Tabellen und eine weitere Datenbank für Data Marts (manchmal auch als _semantische Ebene_ bezeichnet). Die Verarbeitung von separaten Datenbanken als ETL-/ELT-Pipelines in Azure Synapse erfordert möglicherweise die Implementierung von datenbankübergreifenden Verknüpfungen und die Verschiebung von Daten zwischen den separaten Datenbanken.

Die Azure Synapse-Umgebung verfügt über ein Singleton. Tabellen werden mithilfe von Schemas in logisch getrennte Gruppen unterteilt. Es wird empfohlen, die separaten Datenbanken, die Sie von Teradata migrieren, mithilfe von mehreren Schemas in Azure Synapse zu imitieren.

Falls Sie in der Teradata-Umgebung Schemas verwendet haben, müssen Sie möglicherweise die Namenskonvention ändern, um die vorhandenen Teradata-Tabellen und -Sichten in die neue Umgebung verschieben zu können. Sie können beispielsweise die vorhandenen Teradata-Schema- und -Tabellennamen mit dem neuen Azure Synapse-Tabellennamen verketten und mithilfe der Schemanamen die Namen der ursprünglichen separaten Datenbanken in der neuen Umgebung beibehalten.

Eine andere Möglichkeit ist die Verwendung von SQL-Sichten für die zugrunde liegenden Tabellen, um deren logische Strukturen beizubehalten. SQL-Sichten weisen die folgenden potenziellen Nachteile auf:

- Azure Synapse-Sichten sind schreibgeschützt, sodass alle Updates an den Daten in den zugrunde liegenden Basistabellen erfolgen müssen.
- Wenn bereits verschiedene Sichtebenen bestehen, wirken sich weitere Sichtebenen möglicherweise negativ auf die Leistung aus.

### <a name="tables"></a>Tabellen

Beim Migrieren von Tabellen zwischen unterschiedlichen Technologien werden nur die Rohdaten sowie die Metadaten, die diese beschreiben, physisch zwischen den beiden Umgebungen verschoben. Datenbankelemente wie Indizes werden nicht aus dem Quellsystem migriert, da diese möglicherweise nicht benötigt oder in der neuen Umgebung anders implementiert werden.

Das Wissen, wo Leistungsoptimierungen wie Indizes in der Quellumgebung eingesetzt wurden, kann jedoch Hinweise darauf geben, an welcher Stelle in der neuen Umgebung Optimierungspotenzial besteht. Wenn ein nicht eindeutiger Sekundärindex in der Teradata-Quellumgebung erstellt wurde, kann es vorteilhaft sein, in der migrierten Azure Synapse-Umgebung einen nicht gruppierten Index zu erstellen. Alternativ können Zonenzuordnungen ebenfalls darauf hindeuten, dass andere native Techniken zur Leistungsoptimierung, z. B. die Tabellenreplikation, der Erstellung eines Like-for-Like-Indexes vorzuziehen sind.

### <a name="high-availability-database"></a>Hochverfügbarkeitsdatenbank

Teradata unterstützt die knotenübergreifende Datenreplikation über die Option `FALLBACK`. Tabellenzeilen, die sich physisch auf einem Knoten befinden, werden auf einen anderen Knoten im System repliziert. Mit diesem Ansatz wird sichergestellt, dass keine Daten verloren gehen, wenn ein Knotenfehler auftritt. Damit stellt er die Grundlage für Failoverszenarios dar.

Die Architektur für Hochverfügbarkeit in Azure SQL-Datenbank soll garantieren, dass Ihre Datenbank aktiv ist und zu 99,99 % der Zeit ausgeführt wird. Sie müssen daher nicht berücksichtigen, welche Auswirkungen Wartungsarbeiten und Ausfälle auf die Workload haben könnten. Azure verarbeitet automatisch wichtige Wartungsaufgaben, wie Patches, Sicherungen, Windows- und SQL-Upgrades, aber auch ungeplante Ereignisse wie Ausfälle der zugrunde liegenden Hard- und Software oder Netzwerkfehler.

Momentaufnahmen sind ein integriertes Feature des Diensts zum Erstellen von Wiederherstellungspunkten in Azure Synapse. Momentaufnahmen stellen eine automatische Sicherung für die Datenspeicherung in Azure Synapse bereit. Sie müssen das Feature nicht aktivieren. Derzeit können einzelne Benutzer keine automatischen Wiederherstellungspunkte löschen, die der Dienst zum Verwalten von SLAs für die Wiederherstellung verwendet.

Azure Synapse erstellt über den Tag verteilte Momentaufnahmen des Data Warehouse. Die dabei erstellten Wiederherstellungspunkte sind sieben Tage lang verfügbar. Dieser Aufbewahrungszeitraum kann nicht geändert werden. Azure Synapse unterstützt eine Recovery Point Objective von acht Stunden. Sie können das Data Warehouse in der primären Region anhand einer beliebigen Momentaufnahme wiederherstellen, die in den vergangenen sieben Tagen erstellt wurde. Wenn Ihre Organisation differenziertere Sicherungen benötigt, stehen weitere benutzerdefinierte Optionen zur Verfügung.

### <a name="unsupported-teradata-table-types"></a>Nicht unterstützte Teradata-Tabellentypen

Teradata bietet Unterstützung für spezielle Tabellentypen für Zeitreihen und temporale Daten. Die Syntax und einige Funktionen für diese Tabellentypen werden in Azure Synapse nicht direkt unterstützt, aber die Daten können in eine Standardtabelle migriert werden, die die erforderlichen Datentypen und die entsprechende Indizierung oder Partitionierung in der Datums-/Uhrzeitspalte aufweist.

Teradata implementiert die Funktion für temporale Abfragen, indem das Umschreiben von Abfragen dazu verwendet wird, Filter zu einer temporale Abfrage hinzuzufügen, um so den betreffenden Datumsbereich einzuschränken. Wenn Sie in der Teradata-Quellumgebung temporale Abfragen verwenden und diese migrieren möchten, müssen Sie die relevanten temporalen Abfragefilter hinzufügen.

Die Azure-Umgebung umfasst auch Features für komplexe Analysen zu Zeitreihendaten in jeder Größenordnung über Azure Time Series Insights. Time Series Insights ist für IOT-Datenanalyseanwendungen konzipiert und ist für diesen Anwendungsfall möglicherweise besser geeignet. Weitere Informationen finden Sie unter [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/).

### <a name="teradata-data-type-mapping"></a>Teradata-Datentypzuordnung

Einige Teradata-Datentypen werden in Azure Synapse nicht direkt unterstützt. In der folgenden Tabelle sind diese Datentypen und die empfohlene Vorgehensweise zur Behandlung aufgeführt. In der Tabelle ist der Teradata-Spaltentyp der Typ, der im Systemkatalog gespeichert ist (z. B. in `DBC.ColumnsV`).

Verwenden Sie die Metadaten aus den Teradata-Katalogtabellen, um festzulegen, ob diese Datentypen migriert werden sollen, und planen Sie die Unterstützung von Ressourcen im Migrationsplan ein. Beispielsweise können Sie eine SQL-Abfrage wie die im nächsten Abschnitt verwenden, um beliebige Vorkommen nicht unterstützter Datentypen zu finden, die Sie beheben müssen.

Drittanbieter bieten Tools und Dienste an, mit denen die Migration automatisiert werden kann, einschließlich Datentypzuordnungen zwischen Plattformen. Wenn Sie in der Teradata-Umgebung bereits ein ETL-Tool von Drittanbietern wie Informatica oder Talend verwenden, können Sie damit alle erforderlichen Datentransformationen implementieren.

## <a name="sql-data-manipulation-language-dml-syntax-differences"></a>Syntaxunterschiede in der SQL-Datenbearbeitungssprache

Es gibt einige Unterschiede in der Syntax der SQL-Datenbearbeitungssprache (Data Manipulation Language, DML) zwischen Teradata SQL und Azure Synapse:

- `QUALIFY`: Teradata unterstützt den Operator `QUALIFY`.

   Beispiel:

  `SELECT col1 FROM tab1 WHERE col1='XYZ'`

  Tools und Dienste von Drittanbietern können Datenzuordnungsaufgaben automatisieren:

  `QUALIFY ROW_NUMBER() OVER (PARTITION by col1 ORDER BY col1) = 1;`

  In Azure Synapse können Sie das gleiche Ergebnis erzielen, indem Sie die folgende Syntax verwenden:

  `SELECT * FROM (SELECT col1, ROW_NUMBER() OVER (PARTITION by col1 ORDER BY col1) rn FROM tab1 WHERE c1='XYZ' ) WHERE rn = 1;`

- **Datumsarithmetik:** Azure Synapse verfügt über Operatoren wie `DATEADD` und `DATEDIFF`, die Sie für `DATE` oder `DATETIME` verwenden können.

   Teradata unterstützt die direkte Subtraktion für Datumsangaben:

  - `SELECT DATE1 - DATE2 FROM ...`

  - `LIKE ANY`-Syntax

    Beispiel:

    `SELECT * FROM CUSTOMER WHERE POSTCODE LIKE ANY ('CV1%', 'CV2%', CV3%') ;`.

    Die Entsprechung in der Azure Synapse-Syntax lautet:

    `SELECT * FROM CUSTOMER WHERE (POSTCODE LIKE 'CV1%') OR (POSTCODE LIKE 'CV2%') OR (POSTCODE LIKE 'CV3%') ;`

- Abhängig von den Systemeinstellungen wird bei Zeichenvergleichen in Teradata eventuell standardmäßig nicht zwischen Groß- und Kleinschreibung unterschieden. In Azure Synapse wird die Groß- und Kleinschreibung bei diesen Vergleichen immer beachtet.

## <a name="functions-stored-procedures-triggers-and-sequences"></a>Funktionen, gespeicherte Prozeduren, Trigger und Sequenzen

Bei der Migration eines Data Warehouse aus einer ausgereiften Legacyumgebung wie Teradata müssen Sie häufig noch weitere Elemente außer einfachen Tabellen und Sichten in die neue Zielumgebung migrieren. Beispiele für Teradata-Elemente, die keine Tabellen sind und möglicherweise zu Azure Synapse migriert werden müssen, sind Funktionen, gespeicherte Prozeduren, Trigger und Sequenzen. Während der Vorbereitung der Migration sollten Sie ein Inventar der zu migrierenden Objekte erstellen. Definieren Sie im Projektplan die Methode für die Verarbeitung aller Objekte, und weisen Sie die entsprechenden Ressourcen für deren Migration zu.

Möglicherweise gibt es Dienste in der Azure-Umgebung, die die Funktionalität ersetzen, die in Form von Funktionen oder gespeicherten Prozeduren in der Teradata-Umgebung implementiert wurde. In der Regel ist es effizienter, die integrierten Azure-Funktionen zu verwenden, anstatt die Teradata-Funktionen neu zu schreiben.

Nachstehend sind weitere Informationen zur Migration von Funktionen, gespeicherten Prozeduren, Triggern und Sequenzen aufgeführt:

- **Funktionen:** Wie bei den meisten Datenbankprodukten unterstützt Teradata Systemfunktionen und benutzerdefinierte Funktionen in einer SQL-Implementierung. Werden gängige Systemfunktionen zu einer anderen Datenbankplattform wie Azure Synapse migriert, sind diese üblicherweise in der neuen Umgebung verfügbar und können ohne Änderung migriert werden. Wenn Systemfunktionen in der neuen Umgebung eine leicht veränderte Syntax aufweisen, können Sie die erforderlichen Änderungen normalerweise automatisieren.

  Zu diesem Zweck müssen Sie möglicherweise beliebige benutzerdefinierte Funktionen und Systemfunktionen neu schreiben, wenn diese keine Entsprechung in der neuen Umgebung aufweisen. Nutzen Sie dazu die Sprachen, die in der neuen Umgebung verfügbar sind. In Azure Synapse werden benutzerdefinierte Funktionen mithilfe der weit verbreiteten Sprache „Transact-SQL“ implementiert.

- **Gespeicherte Prozeduren:** In den meisten modernen Datenbankprodukten können Sie Prozeduren in der Datenbank speichern. Eine gespeicherte Prozedur enthält üblicherweise SQL-Anweisungen und etwas prozedurale Logik. Möglicherweise gibt die Prozedur auch Daten oder einen Zustand zurück.

  Teradata stellt Sprache für gespeicherte Prozeduren zum Erstellen gespeicherter Prozeduren bereit. Azure Synapse unterstützt gespeicherte Prozeduren mithilfe von T-SQL. Wenn Sie gespeicherte Prozeduren zu Azure Synapse migrieren, müssen Sie diese in T-SQL neu programmieren.

- **Trigger:** Trigger können nicht in Azure Synapse erstellt werden, aber Sie können Trigger in Data Factory implementieren.

- **Sequenzen:** Azure Synapse-Sequenzen werden ähnlich wie in Teradata behandelt. Verwenden Sie `IDENTITY`-Spalten oder SQL-Code, um die nächste Sequenznummer in einer Reihe zu erstellen.

## <a name="metadata-and-data-extraction"></a>Metadaten und Datenextraktion

Berücksichtigen Sie die folgenden Informationen bei der Planung der Metadaten- und Datenextraktion aus der Teradata-Umgebung:

- **Generieren von DDL-Anweisungen (Data Definition Language, Datendefinitionssprache):** Wie bereits beschrieben können vorhandene Teradata-Skripts `CREATE TABLE` und `CREATE VIEW` bearbeitet werden, um die entsprechenden Definitionen (bei Bedarf mit geänderten Datentypen) zu erstellen. In diesem Szenario müssen Sie in der Regel zusätzliche Teradata-spezifische Klauseln entfernen (z. B. `FALLBACK`).

  Die Informationen, die die aktuellen Tabellen- und Sichtdefinitionen angeben, werden in den Systemkatalogtabellen verwaltet. Systemkatalogtabellen sind die beste Quelle für diese Informationen, weil sie mit hoher Wahrscheinlichkeit auf dem neuesten Stand und vollständig sind. Die benutzerseitig verwaltete Dokumentation ist möglicherweise nicht mit den aktuellen Tabellendefinitionen synchron.

  Sie können auf die Informationen über Sichten im Katalog zugreifen, z. B. `DBC.ColumnsV`. Sie können auch Sichten verwenden, um die entsprechenden `CREATE TABLE`-DDL-Anweisungen (Datendefinitionssprache) für die entsprechenden Tabellen in Azure Synapse zu generieren.

  Migrations- und ETL-Tools von Drittanbietern nutzen die Informationen im Katalog auch, um das gleiche Ergebnis zu erzielen.

- **Extrahieren von Daten**

  Migrieren Sie die Rohdaten mit Teradata-Standardhilfsprogrammen wie `BTEQ` und `FASTEXPORT` aus vorhandenen Teradata-Tabellen. Bei einer Migration müssen die Daten stets so effizient wie möglich extrahiert werden. Der für neuere Versionen von Teradata empfohlene Ansatz ist die Verwendung von Teradata Parallel Transporter, einem Hilfsprogramm, das mehrere parallele `FASTEXPORT`-Datenströme verwendet, um den besten Durchsatz zu erzielen.

  Teradata Parallel Transporter kann direkt von Data Factory aufgerufen werden. Diese Vorgehensweise wird für die Verwaltung des Datenmigrationsprozesses empfohlen, unabhängig davon, ob die Teradata-Instanz lokal oder in eine VM in der Azure-Umgebung kopiert wurde, wie zuvor beschrieben.

  Empfohlene Datenformate für die extrahierten Daten sind _durch Trennzeichen getrennte Textdateien_ (auch CSV-Dateien genannt) oder ORC- (Optimized Row Columnar) oder Parquet-Dateien.

Weitere Informationen zum Migrieren von Daten und ETL aus einer Teradata-Umgebung finden Sie in der Teradata-Dokumentation.

## <a name="performance-tuning-recommendations"></a>Empfehlungen für die Leistungsoptimierung

In Bezug auf die Optimierung bestehen gewisse Unterschiede zwischen den Plattformen. In der folgenden Übersicht der Empfehlungen zur Leistungsoptimierung werden spezifische Unterschiede zwischen Teradata und Azure Synapse sowie Migrationsalternativen hervorgehoben:

- **Optionen für die Datenverteilung:** In Azure können Sie die Datenverteilungsmethoden für einzelne Tabellen festlegen. Der Zweck dieser Funktionalität besteht darin, die Datenmenge zu reduzieren, die zwischen den Verarbeitungsknoten ausgetauscht wird, wenn eine Abfrage ausgeführt wird.

  Bei Verknüpfungen großer Tabellen miteinander wird durch die Hashverteilung von einer Tabelle oder (idealerweise beiden) in den Joinspalten sichergestellt, dass die Joinverarbeitung lokal ausgeführt werden kann, da sich die zu verknüpfenden Datenzeilen bereits auf demselben Verarbeitungsknoten befinden.

  Azure Synapse sieht eine zusätzliche Methode vor, um kleine und große Tabellen in einem Sternschemamodell lokal zu verknüpfen (oft als *Verknüpfung zwischen einer Dimensions- und einer Faktentabelle* bezeichnet). Sie replizieren die kleinere Tabelle auf allen Knoten. Dies stellt sicher, dass jeder Wert des Verknüpfungsschlüssels für die größere Tabelle eine übereinstimmende Dimensionszeile enthält, die lokal verfügbar ist. Der Mehraufwand für die Replikation der Dimensionstabelle ist relativ gering, sofern die Tabellen nicht groß sind. Andernfalls wäre die Verwendung einer Hashverteilung (wie zuvor beschrieben) vorzuziehen.

- **Datenindizierung:** Azure Synapse bietet verschiedene Indizierungsoptionen. Diese unterscheiden sich jedoch in der Funktionsweise und der Nutzung von Indizierungsoptionen in Teradata. Weitere Informationen zu den Indizierungsoptionen in Azure Synapse finden Sie unter [Entwurfstabellen in einem Azure Synapse-Pool](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-overview).

  Vorhandene Indizes in der Teradata-Quellumgebung können einen nützlichen Hinweis auf die aktuelle Verwendungsweise von Daten geben. Außerdem können sie darauf hindeuten, welche Spalten in der Azure Synapse-Umgebung indiziert werden sollten.

- **Datenpartitionierung:** Im Data Warehouse eines Unternehmens können Faktentabellen Milliarden von Datenzeilen enthalten. Die Partitionierung ist eine Methode, um die Wartung und das Abfragen dieser Tabellen zu optimieren. Durch Aufteilen der Tabellen in separate Teile wird die Menge der Daten reduziert, die gleichzeitig verarbeitet werden. Die Partitionierung einer Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

  Für die Partitionierung kann nur ein Feld pro Tabelle verwendet werden. Bei dem für die Partitionierung verwendeten Feld handelt es sich häufig um ein Datumsfeld, da viele Abfragen nach Datum oder nach einem Datumsbereich gefiltert werden. Die Partitionierung einer Tabelle kann nach dem ersten Laden geändert werden. Zu diesem Zweck müssen Sie die Tabelle mit einer neuen Verteilung neu erstellen, die die `CREATE TABLE AS SELECT`-Anweisung verwendet. Eine ausführliche Erläuterung der Partitionierung in Azure Synapse finden Sie unter [Partitionieren von Tabellen in einem Synapse-SQL-Pool](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-tables-partition).

- **Datentabellenstatistiken:** Sie können sicherstellen, dass die Statistiken zu Datentabellen auf dem neuesten Stand sind, indem Sie einen `COLLECT STATISTICS`-Schritt in ETL/ELT-Jobs hinzufügen oder indem Sie die automatische Statistiksammlung für die Tabelle aktivieren.

- **PolyBase zum Laden von Daten:** PolyBase ist die effizienteste Methode, um große Datenmengen in ein Warehouse zu laden. Mit PolyBase können Daten auch in parallelen Streams geladen werden.

- **Ressourcenklassen für die Workloadverwaltung:** Azure Synapse verwendet Ressourcenklassen zum Verwalten von Workloads. Im Allgemeinen verbessern große Ressourcenklassen die Leistung einzelner Abfragen. Kleinere Ressourcenklassen hingegen erhöhen das Maß von Parallelität. Sie können die Auslastung über dynamische Verwaltungssichten überwachen, um sicherzustellen, dass die entsprechenden Ressourcen effizient verwendet werden.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Implementieren einer Teradata-Migration erhalten Sie bei Ihrem Microsoft-Kontovertreter, der Sie gerne über lokale Migrationsangebote informiert.
