---
title: Datendefinitionssprachen für die Schemamigration
description: Hier werden Entwurfsaspekte und Leistungsoptionen für Datendefinitionssprachen erläutert, die für die Schemamigration zu Azure Synapse Analytics relevant sind.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eebd659ad0dc0455c481e0f5b82a84fafa960c9e
ms.sourcegitcommit: c1d6c1c777475f92a3f8be6def84f1779648a55c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2020
ms.locfileid: "92334747"
---
<!-- cSpell:ignore DDLs Attunity "Attunity Replicate" "Attunity Visibility" Inmon Denodo DMVs multinode equi Datometry -->

# <a name="data-definition-languages-for-schema-migration"></a>Datendefinitionssprachen für die Schemamigration

In diesem Artikel werden Entwurfsaspekte und Leistungsoptionen für Datendefinitionssprachen erläutert, die für die Schemamigration zu Azure Synapse Analytics relevant sind.

## <a name="design-considerations"></a>Überlegungen zum Entwurf

### <a name="preparation-for-migration"></a>Vorbereitung für die Migration

Bei der Vorbereitung für die Migration vorhandener Daten zu Azure Synapse Analytics ist es wichtig, den Umfang des Migrationsdurchlaufs eindeutig zu definieren (insbesondere für ein erstes Migrationsprojekt). Wenn Sie sich zuvor mit der Migration von Datenbankobjekten und zugehörigen Prozessen befassen, können der Aufwand und die Risiken für das spätere Projekt verringert werden.

Erfassen Sie den Bestand an zu migrierenden Datenbankobjekten. Je nach Quellplattform umfasst dieser Bestand einige oder alle der folgenden Objekte:

- Tabellen
- Sichten
- Indizes
- Funktionen
- Gespeicherte Prozeduren
- Datenverteilung und -partitionierung

Die grundlegenden Informationen für diese Objekte sollten Metriken wie die Zeilenanzahl, die physische Größe, die Datenkomprimierungsverhältnisse und die Objektabhängigkeiten beinhalten. Diese Informationen sollten über Abfragen von Systemkatalogtabellen im Quellsystem verfügbar sein. Die Systemmetadaten sind die beste Quelle für diese Informationen. Die externe Dokumentation ist möglicherweise veraltet und umfasst nicht die Änderungen, die seit der anfänglichen Implementierung an der Datenstruktur vorgenommen wurden.

Sie können auch die tatsächliche Objektnutzung anhand von Abfrageprotokollen analysieren oder unterstützende Tools von Microsoft-Partnern (z. B. Attunity Visibility) verwenden. Möglicherweise müssen einige Tabellen nicht migriert werden, da sie nicht mehr in Produktionsabfragen verwendet werden.

Die Datengröße und die Arbeitsauslastungsinformationen sind für Azure Synapse Analytics wichtig, da Sie so die geeigneten Konfigurationen bestimmen können. Ein Beispiel hierfür ist der erforderliche Parallelitätsgrad. Das erwarte Wachstum von Daten und Arbeitsauslastungen kann sich auf die empfohlene Zielkonfiguration auswirken. Deshalb sollten Ihnen diese Informationen bekannt sein.

Wenn Sie Datenvolumen verwenden, um den für die neue Zielplattform benötigten Speicher zu schätzen, ist es wichtig, das Datenkomprimierungsverhältnis (sofern vorhanden) in der Quelldatenbank zu kennen. Einfach von der Menge des auf dem Quellsystem verwendeten Speichers auszugehen, ist wahrscheinlich die falsche Grundlage für eine Größenbestimmung. Überwachungs- und Metadateninformationen können nützlich sein, um die Größe der unkomprimierten Rohdaten sowie den Mehraufwand für die Indizierung, Datenreplikation, Protokollierung oder andere Prozesse im aktuellen System zu ermitteln.

Die Größe der unkomprimierten Rohdaten in den zu migrierenden Tabellen ist ein guter Ausgangspunkt für das Schätzen des Speichers, der in der neuen Azure Synapse Analytics-Zielumgebung erforderlich ist.

Die neue Zielplattform enthält zudem einen Komprimierungsfaktor und Indizierungsaufwand. Diese unterscheiden sich jedoch wahrscheinlich vom Quellsystem. Im Preis für Azure Synapse Analytics-Speicher sind auch Momentaufnahmesicherungen für sieben Tage enthalten. Dies kann sich auf die Gesamtkosten für den benötigten Speicher im Vergleich zur vorhandenen Umgebung auswirken.

Sie können die Leistungsoptimierung für das Datenmodell bis zu einem späten Zeitpunkt des Migrationsvorgangs verzögern und so planen, dass sie erst durchgeführt wird, wenn echte Datenvolumes im Data Warehouse vorhanden sind. Es wird jedoch empfohlen, einige Optionen für die Leistungsoptimierung schon vorher zu implementieren.

Beispielsweise ist es in Azure Synapse Analytics sinnvoll, kleine Dimensionstabellen als replizierte Tabellen und große Faktentabellen als gruppierte Columnstore-Indizes zu definieren. Ebenso geben Indizes, die in der Quellumgebung definiert sind, einen guten Hinweis darauf, welche Spalten von der Indizierung in der neuen Umgebung profitieren können. Wenn Sie diese Informationen beim anfänglichen Definieren der Tabellen vor dem Laden verwenden, sparen Sie später im Prozess Zeit.

Es empfiehlt sich, die Komprimierungsrate und den Indizierungsaufwand für Ihre eigenen Daten bei Fortschreiten des Migrationsprozesses in Azure Synapse Analytics zu messen. Diese Messung ermöglicht eine zukünftige Kapazitätsplanung.

Möglicherweise kann auch das vorhandene Data Warehouse vor der Migration vereinfacht werden, indem die Komplexität für eine einfache Migration verringert wird. Dafür sind ggf. folgende Schritte nötig:

- Löschen oder archivieren Sie nicht verwendete Tabellen vor der Migration, um eine Migration nicht verwendeter Daten zu vermeiden. Durch das Archivieren in Azure Blob Storage und das Definieren der Daten als externe Tabelle können die Daten zu geringeren Kosten verfügbar bleiben.
- Konvertieren Sie physische Data Marts mithilfe von Datenvirtualisierungssoftware in virtuelle Data Marts, um den Migrationsumfang zu verringern. Diese Konvertierung verbessert auch die Agilität und senkt die Gesamtbetriebskosten. Sie können diese als Modernisierungsmaßnahme während der Migration betrachten.

Ein Ziel des Migrationsdurchlaufs kann auch die Modernisierung des Warehouse sein, indem das zugrunde liegende Datenmodell geändert wird. Ein Beispiel hierfür ist der Wechsel von einem Inmon-Datenmodell zu einem Datentresoransatz. Sie sollten darüber während der Vorbereitungsphase entscheiden und eine Strategie für den Übergang zum Migrationsplan etablieren.

In diesem Szenario wird empfohlen, zuerst das Datenmodell auf die neue Plattform zu migrieren und dann in Azure Synapse Analytics zum neuen Modell zu wechseln. Verwenden Sie die Skalierbarkeits- und Leistungsfeatures der Plattform, um die Transformation auszuführen, ohne das Quellsystem zu beeinträchtigen.

### <a name="data-model-migration"></a>Datenmodellmigration

Je nach Plattform und Ursprüngen des Quellsystems kann das Datenmodell einiger oder aller Teile möglicherweise bereits die Form eines Stern- oder Schneeflockenschemas aufweisen. In diesem Fall kann es direkt und unverändert zu Azure Synapse Analytics migriert werden. Dieses Szenario ist die einfachste und risikoärmste Migrationsoption. Eine Migration in unverändertem Zustand kann auch die erste Phase einer komplexeren Migration sein, die einen Übergang zu einem neuen Datenmodell umfasst, z. B. wie bereits beschrieben zu einem Datentresor.

Sie können sämtliche relationalen Tabellen und Sichten zu Azure Synapse Analytics migrieren. Wenn Sie Arbeitsauslastungen für Analyseabfragen für große Datasets ausführen, erzielen Sie mit einem Stern- oder Schneeflockendatenmodell im Allgemeinen die beste Gesamtleistung. Wenn das Quelldatenmodell noch nicht in dieser Form vorliegt, kann es sinnvoll sein, den Migrationsprozess zur Umstrukturierung des Modells zu nutzen.

Wenn das Migrationsprojekt Änderungen am Datenmodell einschließt, sollten Sie diese Änderungen in der neuen Zielumgebung ausführen. Sie können also zuerst das vorhandene Modell migrieren und dann die Leistungsfähigkeit und Flexibilität von Azure Synapse Analytics nutzen, um die Daten in das neue Modell umzuwandeln. Durch diesen Ansatz werden die Auswirkungen auf das vorhandene System minimiert und die Leistung und Skalierbarkeit von Azure Synapse Analytics genutzt, um alle Änderungen schnell und kostengünstig vorzunehmen.

Sie können das vorhandene System in mehrere Schichten migrieren (z. B. in eine Datenerfassungs- und Stagingschicht, eine Data-Warehouse-Schicht und eine Berichtserstellungsschicht oder Data-Mart-Schicht). Jede Schicht besteht aus relationalen Tabellen und Sichten. Obwohl diese unverändert zu Azure Synapse Analytics migriert werden können, kann es kostengünstiger und zuverlässiger sein, einige Features und Funktionen des Azure-Ökosystems zu nutzen. Beispiel:

- **Datenerfassung und Staging:** Für einen Teil des ETL-Prozesses (Extrahieren, Transformieren und Laden) oder ELT-Prozesses (Extrahieren, Laden und Transformieren) können Sie Azure Blob Storage in Verbindung mit PolyBase anstelle von relationalen Tabellen verwenden, um Daten schnell und parallel zu laden.
- **Berichtsschicht und Data Marts:** Die Leistungsfeatures von Azure Synapse Analytics machen es möglicherweise überflüssig, aggregierte Tabellen für Berichtszwecke oder Data Marts physisch zu instanziieren. Diese können möglicherweise als Sichten für das zentrale Data Warehouse oder über die Datenvirtualisierungsschicht eines Drittanbieters implementiert werden. Grundsätzlich können der Prozess für die Migration von Verlaufsdaten und ggf. auch inkrementelle Aktualisierungen wie im folgenden Diagramm dargestellt erfolgen:

   ![Diagramm: modernes Data Warehouse](../../../_images/analytics/schema-migration-ddl.png)

Wenn Sie diesen oder einen ähnlichen Ansatz verwenden können, wird die Anzahl der zu migrierenden Tabellen reduziert. Einige Prozesse werden möglicherweise vereinfacht oder überflüssig, wodurch die Arbeitsauslastung für die Migration weiter reduziert wird. Die Anwendbarkeit dieser Ansätze hängt vom jeweiligen Anwendungsfall ab. Das allgemeine Prinzip ist jedoch, nach Möglichkeit die Features und Funktionen des Azure-Ökosystems zu verwenden, um die Arbeitsauslastung für die Migration zu reduzieren und eine kosteneffiziente Zielumgebung zu erstellen. Das gilt auch für andere Features wie Sicherung, Wiederherstellung, Workflowverwaltung und Workflowüberwachung.

Es stehen außerdem Produkte und Dienste von Microsoft-Partnern zur Verfügung, die bei der Data-Warehouse-Migration helfen und in einigen Fällen Teile des Prozesses automatisieren. Wenn das vorhandene System ein ETL-Produkt eines Drittanbieters beinhaltet, unterstützt es Azure Synapse Analytics als Zielumgebung möglicherweise bereits. Die vorhandenen ETL-Workflows können an das neue Data Warehouse-Ziel umgeleitet werden.

### <a name="data-marts-physical-or-virtual"></a>Data Marts: physisch oder virtuell

Organisationen mit älteren Data-Warehouse-Umgebungen erstellen häufig Data Marts, die den Abteilungen oder Geschäftsfunktionen gute Ad-hoc-Self-Service-Abfragen und Berichtsleistung ermöglichen. Ein Data Mart besteht in der Regel aus einer Teilmenge des Data Warehouse und enthält aggregierte Versionen der ursprünglichen Daten. Da es sich meistens um ein dimensionales Datenmodell handelt, sind benutzerfreundliche Tools wie Tableau, MicroStrategy und Microsoft Power BI enthalten, um Daten einfach und schnell abzufragen.

Eine Verwendung von Data Marts besteht darin, die Daten in einer nutzbaren Form verfügbar zu machen, selbst wenn das zugrunde liegende Warehouse-Datenmodell z. B. ein Datentresor ist. Dieser Ansatz wird auch als Modell mit drei Ebenen bezeichnet.

Sie können separate Data Marts für einzelne Geschäftseinheiten innerhalb einer Organisation verwenden, um stabile Datensicherheitssysteme zu implementieren. Beispielsweise können Sie Benutzern den Zugriff auf bestimmte relevante Data Marts gewähren und vertrauliche Daten löschen, verschleiern oder anonymisieren.

Wenn diese Data Marts als physische Tabellen implementiert werden, sind zusätzliche Speicherressourcen nötig, um diese aufzubewahren, und zusätzliche Verarbeitungsschritte, um sie regelmäßig zu erstellen und zu aktualisieren. Physische Tabellen verdeutlichen, dass die Daten im Data Mart nur so aktuell wie der letzte Aktualisierungsvorgang sind. Für hochgradig flüchtige Datendashboards sind sie daher möglicherweise nicht geeignet.

Mit der Einführung relativ kostengünstiger skalierbarer MPP-Architekturen (Massively Parallel Processing) wie Azure Synapse Analytics und deren inhärenten Leistungsfeatures können Sie Data-Mart-Funktionen ggf. bereitstellen, ohne den Mart als physische Tabellen zu instanziieren. Nutzen Sie eine der folgenden Methoden, um die Data Marts im Prinzip zu virtualisieren:

- SQL-Sichten im primären Data Warehouse
- Eine Virtualisierungsschicht, die Features wie Azure Synapse Analytics-Sichten oder Drittanbieterprodukte für die Virtualisierung wie Denodo verwendet

Durch diesen Ansatz wird der Bedarf für zusätzlichen Speicher oder zusätzliche Aggregationsverarbeitungen reduziert oder entfällt. Zudem müssen insgesamt weniger Datenbankobjekte migriert werden.

Ein weiterer Vorteil des Data-Warehouse-Ansatzes besteht in der Möglichkeit, Vorgänge wie Joins und Aggregationen für große Datenvolumes auszuführen. Wenn Sie die Aggregations- und Joinlogik beispielsweise in eine Virtualisierungsschicht implementieren und die externe Berichterstellung in einer virtualisierten Sicht darstellen, wird die stabile Verarbeitung zur Erstellung dieser Sichten in das Data Warehouse verschoben.

Die Hauptgründe für die Implementierung physischer oder virtueller Data Marts sind:

- Mehr Agilität, da ein virtueller Data Mart leichter zu ändern ist als physische Tabellen und die zugehörigen ETL-Prozesse.
- Geringere Gesamtkosten aufgrund weniger Datenspeicher und Datenkopien in einer virtualisierten Implementierung.
- Keine zu migrierenden ETL-Aufträge und vereinfachte Data-Warehouse-Architektur in einer virtualisierten Umgebung
- Leistung. Früher waren physische Data Marts die zuverlässigere Option. Virtualisierungsprodukte implementieren jetzt intelligente Zwischenspeicherungsverfahren, um die Unterschiede auszugleichen.

Sie können die Datenvirtualisierung auch verwenden, damit die Daten den Benutzern während eines Migrationsprojekts konsistent angezeigt werden.

### <a name="data-mapping"></a>Datenzuordnung

#### <a name="key-and-integrity-constraints-in-azure-synapse-analytics"></a>Schlüssel- und Integritätseinschränkungen in Azure Synapse Analytics

Einschränkungen für den Primärschlüssel und den Referenzschlüssel werden derzeit in Azure Synapse Analytics nicht erzwungen. Sie können jedoch die Definition für `PRIMARY KEY` in der `CREATE TABLE`-Anweisung mithilfe der `NOT ENFORCED`-Klausel einschließen. Dies bedeutet, dass Berichtsprodukte von Drittanbietern die Metadaten für die Tabelle verwenden können, um die Schlüssel im Datenmodell zu verstehen und somit die effizientesten Abfragen zu generieren.

#### <a name="data-type-support-in-azure-synapse-analytics"></a>Datentypunterstützung in Azure Synapse Analytics

Einige ältere Datenbanksysteme bieten Unterstützung für Datentypen, die in Azure Synapse Analytics nicht direkt unterstützt werden. Sie können diese Datentypen jedoch verarbeiten, indem Sie einen unterstützten Datentyp zum unveränderten Speichern der Daten verwenden oder die Daten in einen unterstützten Datentyp transformieren.

Es folgt eine alphabetische Liste der unterstützten Datentypen:

<!-- TODO: Review format of this list. Are the arguments necessary for this list? -->

<!-- docutune:disable -->

- `bigint`
- `binary [ (n) ]`
- `bit`
- `char [ (n) ]`
- `date`
- `datetime`
- `datetime2 [ (n) ]`
- `datetimeoffset [ (n) ]`
- `decimal [ (precision [, scale ]) ]`
- `float [ (n) ]`
- `int`
- `money`
- `nchar [ (n) ]`
- `numeric [ (precision [ , scale ]) ]`
- `nvarchar [ (n | MAX) ]`
- `real [ (n) ]`
- `smalldatetime`
- `smallint`
- `smallmoney`
- `time [ (n) ]`
- `tinyint`
- `uniqueidentifier`
- `varbinary [ (n | MAX) ]`
- `varchar [ (n | MAX) ]`

<!-- docutune:enable -->

In der folgenden Tabelle werden gebräuchliche Datentypen, die derzeit nicht unterstützt werden, zusammen mit der empfohlenen Vorgehensweise für die Speicherung dieser Daten in Azure Synapse Analytics aufgeführt. Ausführliche Informationen für bestimmte Umgebungen wie Teradata oder Netezza finden Sie in den entsprechenden Dokumenten.

| Nicht unterstützte Datentypen | Problemumgehung |
|--|--|
| `geometry` | `varbinary` |
| `geography` | `varbinary` |
| `hierarchyid` | `nvarchar(4000)` |
| `image` | `varbinary` |
| `text` | `varchar` |
| `ntext` | `nvarchar` |
| `sql_variant` | Unterteilen der Spalte in mehrere Spalten mit starker Typisierung |
| `table` | Konvertieren in temporäre Tabellen |
| `timestamp` | Anpassen des Codes für die Verwendung von `datetime2` und `CURRENT_TIMESTAMP`-Funktion |
| `xml` | `varchar` |
| Benutzerdefinierter Typ | Rückkonvertieren in nativen Datentyp (wenn möglich) |

#### <a name="potential-data-issues"></a>Mögliche Datenprobleme

Je nach Quellumgebung können bei der Datenmigration einige Probleme auftreten:

- Es können geringfügige Unterschiede bestehen, wie `NULL`-Daten in unterschiedlichen Datenbankprodukten verarbeitet werden. Beispiele hierfür sind die Sortierreihenfolge und die Verarbeitung leerer Zeichenfolgen.
- `DATE`-, `TIME`-, `INTERVAL`- und `TIME ZONE`-Daten und zugehörige Funktionen können von Produkt zu Produkt stark variieren.

Testen Sie gründlich, ob diese zu den gewünschten Ergebnissen in der Zielumgebung führen. Beim Migrationsdurchlauf können Fehler oder falsche Ergebnisse aufgedeckt werden, die derzeit Teil des vorhandenen Quellsystems sind. Der Migrationsprozess bietet eine gute Gelegenheit, Anomalien zu korrigieren.

#### <a name="best-practices-for-defining-columns-in-azure-synapse-analytics"></a>Bewährte Methoden für das Definieren von Spalten in Azure Synapse Analytics

Ältere Systeme enthalten häufig Spalten mit ineffizienten Datentypen. Beispielsweise kann ein Feld als `VARCHAR(20)` definiert sein, obwohl die Datenwerte auch in ein `CHAR(5)`-Feld passen würden. Möglicherweise werden auch `INTEGER`-Felder verwendet, obwohl alle Werte in ein `SMALLINT`-Feld passen würden. Solche Datentypen können insbesondere bei großen Faktentabellen zu Ineffizienzen bei der Speicher- und Abfrageleistung führen.

Ein Migrationsdurchlauf ist ein guter Zeitpunkt, um aktuelle Datendefinitionen zu überprüfen und zu rationalisieren. Sie können diese Aufgaben durch SQL-Abfragen automatisieren, um den maximalen numerischen Wert oder die maximale Zeichenlänge innerhalb eines Datenfelds zu suchen und das Ergebnis mit dem Datentyp zu vergleichen.

Im Allgemeinen empfiehlt es sich, die definierte Gesamtzeilenlänge für eine Tabelle zu minimieren. Die beste Abfrageleistung erzielen Sie, indem Sie wie beschrieben den kleinsten Datentyp für jede Spalte verwenden. Der empfohlene Ansatz zum Laden von Daten aus externen Tabellen in Azure Synapse Analytics besteht in der Verwendung des Hilfsprogramms PolyBase, das eine definierte Zeilenlänge von maximal 1 MB unterstützt. PolyBase lädt nur Tabellen, deren Zeilen kleiner als 1 MB sind, und Sie müssen stattdessen [bcp](/sql/tools/bcp-utility?view=sql-server-ver15) verwenden.

Für eine möglichst effiziente Joinausführung sollten Sie die Spalten auf beiden Seiten des Joins mit denselben Datentyp definieren. Wenn der Schlüssel einer Dimensionstabelle als `SMALLINT` definiert ist, sollten die entsprechenden Verweisspalten in Faktentabellen, die diese Dimension verwenden, ebenfalls als `SMALLINT` definiert werden.

Vermeiden Sie es, für Zeichenfelder eine große Standardgröße zu definieren. Wenn die maximale Größe der Daten in einem Feld 50 Zeichen beträgt, verwenden Sie `VARCHAR(50)`. Ebenso sollten Sie nicht `NVARCHAR` verwenden, wenn `VARCHAR` ausreicht. `NVARCHAR` speichert Unicode-Daten, um unterschiedliche Sprachzeichensätze zuzulassen. `VARCHAR` speichert ASCII-Daten und benötigt weniger Speicherplatz.

## <a name="summary-of-design-recommendations"></a>Zusammenfassung der Entwurfsempfehlungen

Migrieren Sie keine unnötigen Objekte oder Prozesse. Verwenden Sie ggf. integrierte Features und Funktionen in der Azure-Zielumgebung, um die tatsächliche Anzahl der zu migrierenden Objekte und Prozesse zu verringern. Ziehen Sie die Verwendung einer Virtualisierungsschicht in Betracht, damit weniger oder gar keine physischen Data Marts migriert werden müssen und die Verarbeitung an das Data Warehouse übertragen wird.

Automatisieren Sie den Vorgang nach Möglichkeit, und verwenden Sie Metadaten aus Systemkatalogen im Quellsystem, um DDLs für die Zielumgebung zu generieren. Automatisieren Sie nach Möglichkeit auch das Generieren von Dokumenten. Microsoft-Partner wie WhereScape können spezielle Tools und Dienste zur Automatisierungsunterstützung bereitstellen.

Führen Sie alle erforderlichen Änderungen des Datenmodells oder Optimierungen der Datenzuordnung auf der Zielplattform aus. Diese Änderungen können Sie in Azure Synapse Analytics effizienter durchführen. Durch diese Vorgehensweise werden die Auswirkungen auf Quellsysteme verringert, die möglicherweise bereits nahezu voll ausgelastet sind.

## <a name="performance-options"></a>Leistungsoptionen

In diesem Abschnitt werden die Features beschrieben, die in Azure Synapse Analytics zur Verbesserung der Leistung eines Datenmodells verfügbar sind.

### <a name="general-approach"></a>Allgemeiner Ansatz

Die Features der Plattform führen die Leistungsoptimierung für die zu migrierende Datenbank aus. Indizes, die Datenpartitionierung und die Datenverteilung sind Beispiele für eine solche Leistungsoptimierung. Wenn Sie die Migration vorbereiten, können durch das Dokumentieren von Optimierungen auch Optimierungen entdeckt und erfasst werden, die auf die Azure Synapse Analytics-Zielumgebung angewendet werden können.

Beispielsweise kann das Vorhandensein eines nicht eindeutigen Indexes für eine Tabelle darauf hindeuten, dass die im Index verwendeten Felder häufig zum Filtern, Gruppieren oder Verknüpfen verwendet werden. Das ist dann auch in der neuen Umgebung noch der Fall und sollte bei der Auswahl der dort zu indizierenden Felder berücksichtigt werden. Migrationsempfehlungen für bestimmte Quellplattformen wie Teradata und Netezza werden in separaten Dokumenten ausführlich beschrieben.

Dank der Leistungsfähigkeit und Skalierbarkeit der Azure Synapse Analytics-Zielumgebung können Sie mit unterschiedlichen Leistungsoptionen wie der Datenverteilung experimentieren. Wählen Sie die besten alternativen Ansätze aus (z. B. repliziert statt hashverteilt bei großen Tabellen). Dies bedeutet nicht, dass Daten aus externen Quellen neu geladen werden müssen. Alternative Ansätze können in Azure Synapse Analytics relativ schnell und einfach getestet werden, indem Sie Kopien einer beliebigen Tabelle über eine `CREATE TABLE AS SELECT`-Anweisung mit unterschiedlichen Partitionierungs- oder Verteilungsoptionen erstellen.

Verwenden Sie die Überwachungstools der Azure-Umgebung, um zu ermitteln, wie Abfragen ausgeführt werden und wo Engpässe auftreten können. Es sind auch Tools von Microsoft-Partnern als Drittanbieter verfügbar, die Überwachungsdashboards, automatisierte Ressourcenverwaltung und Warnungen enthalten.

Jeder SQL-Vorgang in Azure Synapse Analytics und Ressourcen wie dem Arbeitsspeicher oder der CPU, die von dieser Abfrage verwendet werden, wird in Systemtabellen protokolliert. Es sind einige dynamische Verwaltungssichten verfügbar, die den Zugang zu diesen Informationen vereinfachen.

In den folgenden Abschnitten werden die wichtigsten Azure SQL Data Warehouse-Optionen zum Optimieren der Abfrageleistung erläutert. Vorhandene Umgebungen enthalten Informationen zur möglichen Optimierung in der Zielumgebung.

### <a name="temporary-tables"></a>Temporäre Tabellen

Azure Synapse Analytics unterstützt temporäre Tabellen, die nur in der Sitzung sichtbar sind, in der sie erstellt wurden. Sie bestehen für die Dauer einer Benutzersitzung und werden anschließend automatisch gelöscht.

Zum Erstellen einer temporären Tabelle stellen Sie dem Tabellennamen das Hashzeichen (`#`) voran. Sie können alle üblichen Indizierungs- und Verteilungsoptionen mit temporären Tabellen verwenden. Im nächsten Abschnitt wird dies beschrieben.

Temporäre Tabellen weisen einige Einschränkungen auf:

- Das Umbenennen ist nicht zulässig.
- Das Anzeigen oder Partitionieren ist nicht zulässig.
- Das Ändern von Berechtigungen ist nicht zulässig.

Temporäre Tabellen werden häufig innerhalb der ETL- oder ELT-Verarbeitung verwendet, wo vorübergehende Zwischenergebnisse für Transformationsprozesse verwendet werden.

### <a name="table-distribution-options"></a>Tabellenverteilungsoptionen

Azure Synapse Analytics ist ein MPP-Datenbanksystem (Massively Parallel Processing), das Leistung und Skalierbarkeit durch parallele Ausführung auf mehreren Verarbeitungsknoten erreicht.

Das ideale Verarbeitungsszenario für das Ausführen einer SQL-Abfrage in einer Umgebung mit mehreren Knoten besteht darin, die Arbeitsauslastung auszubalancieren und allen Knoten eine gleich große Menge an zu verarbeitenden Daten zu übergeben. Mit diesem Ansatz können Sie dafür sorgen, dass weniger oder gar keine Daten zwischen Knoten verschoben werden müssen, um die Abfrage zu erfüllen.

Es kann schwierig sein, das ideale Szenario zu finden, da in typischen Analyseabfragen oft Aggregationen und mehrere Joins zwischen Tabellen (z. B. zwischen Fakten- und Dimensionstabellen) vorhanden sind.

Eine Möglichkeit, die Verarbeitung von Abfragen zu beeinflussen, ist die Verwendung der Verteilungsoptionen in Azure Synapse Analytics. Mit diesen können Sie angeben, wo einzelne Datenzeilen der jeweiligen Tabellen gespeichert werden. Nehmen Sie beispielsweise an, dass zwei große Tabellen mit der Datenspalte `CUSTOMER_ID` verknüpft werden. Wenn Sie die beiden Tabellen über die `CUSTOMER_ID`-Spalten verteilen, wenn dieser Join ausgeführt wird, können Sie sicherstellen, dass sich die Daten auf beiden Seiten des Joins bereits auf demselben Verarbeitungsknoten befinden. Dadurch müssen keine Daten zwischen Knoten verschoben werden. Die Verteilungsspezifikation für eine Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

In den folgenden Abschnitten werden die verfügbaren Verteilungsoptionen beschrieben, und Sie finden Empfehlungen für deren Verwendung. Die Verteilung einer Tabelle kann nach dem ersten Laden bei Bedarf geändert werden. Dazu wird die Tabelle mithilfe der `CREATE TABLE AS SELECT`-Anweisung mit der neuen Verteilung neu erstellt.

#### <a name="round-robin"></a>Roundrobin

Die Roundrobin-Tabellenverteilung ist die Standardoption. Hierbei werden die Daten gleichmäßig auf die Knoten im System verteilt. Diese Methode eignet sich gut dafür, relativ geringe Datenmengen ohne offensichtliche Hashkandidaten schnell zu laden. Sie wird häufig für bei ETL- oder ELT-Prozessen für Stagingtabellen verwendet.

#### <a name="hashed"></a>Hash

Das System weist die Zeile einem Hashbucket zu – einem Task, der auf einem Hashalgorithmus basiert, der auf einen benutzerdefinierten Schlüssel (wie `CUSTOMER_ID` im vorherigen Beispiel) angewendet wurde. Der Bucket wird dann einem bestimmten Knoten zugewiesen, und alle Datenzeilen, die auf denselben Wert hashverteilt sind, werden demselben Verarbeitungsknoten zugeordnet.

Diese Methode eignet sich für große Tabellen, die häufig mithilfe eines Schlüssels verknüpft oder aggregiert werden. Bei anderen großen Tabellen, die verknüpft werden sollen, sollte nach Möglichkeit ein Hash für denselben Schlüssel verwendet werden. Wenn mehrere Kandidaten für den Hashschlüssel vorhanden sind, wählen Sie den am häufigsten verknüpften aus.

Die Hashspalte sollte keine NULL-Werte enthalten und ist in der Regel keine Datumsspalte, da bei vielen Abfragen nach Datum gefiltert wird. Das Hashing ist in der Regel effizienter, wenn der zu hashende Schlüssel ein Integerwert statt `CHAR` oder `VARCHAR` ist. Vermeiden Sie außerdem Schlüssel mit einem stark verzerrten Wertebereich, z. B. eine geringe Anzahl von Schlüsselwerten, die einen hohen Prozentsatz der Datenzeilen darstellen.

#### <a name="replicated"></a>Replikation

Wenn Sie die Replikation als Verteilungsoption für eine Tabelle auswählen, wird für die Abfrageverarbeitung eine komplette Kopie dieser Tabelle auf jedem Computeknoten repliziert.

Diese Vorgehensweise ist bei relativ kleinen Tabellen nützlich (üblicherweise weniger als 2 GB in komprimierter Form), die relativ statisch sind und häufig über einen Gleichheitsjoin mit größeren Tabellen verknüpft werden. Bei diesen Tabellen handelt es sich häufig um Dimensionstabellen in einem Sternschema.

### <a name="indexing"></a>Indizierung

Azure Synapse Analytics bietet Optionen zum Indizieren von Daten in großen Tabellen, um die Ressourcen und die Zeit zu reduzieren, die zum Abrufen von Datensätzen benötigt werden:

- Gruppierter Columnstore-Index
- Gruppierter Index
- Nicht gruppierter Index

Eine nicht indizierte Option (`HEAP`) ist für Tabellen vorhanden, die keine der Indexoptionen nutzen können. Die Verwendung von Indizes bedeutet eine Abwägung zwischen verbesserten Abfragezeiten und längeren Ladezeiten sowie mehr Speicherplatznutzung. Indizes beschleunigen oft `SELECT`-, `UPDATE`-, `DELETE`- und `MERGE`-Vorgänge für große Tabellen, die einen kleinen Prozentsatz der Datenzeilen betreffen, und können vollständige Tabellenscans auf ein Minimum reduzieren.

Indizes werden automatisch erstellt, wenn `UNIQUE`- oder `PRIMARY KEY`-Einschränkungen für Spalten definiert werden.

#### <a name="clustered-columnstore-index"></a>Gruppierter Columnstore-Index

Gruppierte Columnstore-Indizes sind die Standardindizierungsoption in Azure Synapse Analytics. Sie bieten die beste Komprimierungs- und Abfrageleistung für große Tabellen. Bei kleineren Tabellen (weniger als 60 Millionen Zeilen) sind diese Indizes nicht effizient. Daher sollten Sie die `HEAP`-Option verwenden. Ein Heap oder eine temporäre Tabelle kann ebenso auch effizienter sein, wenn die Daten in einer Tabelle temporär und Teil eines ETL- oder ELT-Prozesses sind.

#### <a name="clustered-index"></a>Gruppierter Index

Wenn es erforderlich ist, eine einzelne Zeile oder eine kleine Anzahl von Zeilen regelmäßig aus einer großen Tabelle auf Grundlage einer starken Filterbedingung abzurufen, kann ein gruppierter Index effizienter als ein gruppierter Columnstore-Index sein. Pro Tabelle ist nur ein gruppierter Index zulässig.

#### <a name="non-clustered-index"></a>Nicht gruppierter Index

Nicht gruppierte Indizes ähneln gruppierten Indizes insofern, dass Sie den Abruf einzelner Zeilen oder einer kleinen Anzahl von Zeilen basierend auf einer Filterbedingung beschleunigen können. Intern werden nicht gruppierte Indizes getrennt von den Daten gespeichert, und es können mehrere nicht gruppierte Indizes für eine Tabelle definiert werden. Jeder zusätzliche Index benötigt jedoch weiteren Speicherplatz und verringert den Durchsatz beim Einfügen oder Laden von Daten.

#### <a name="heap"></a>Heap

Heaptabellen verursachen keinen Aufwand für die Erstellung und Wartung von Indizes zur Ladezeit der Daten. Sie können das schnelle Laden temporärer Daten bei Prozessen wie ELT-Prozessen ermöglichen. Das Zwischenspeichern ist auch nützlich, wenn die Daten sofort gelesen werden. Da gruppierte Columnstore-Indizes mit unter 60 Millionen Zeilen ineffizient sind, können Heaptabellen auch eingesetzt werden, um Tabellen mit weniger Zeilen zu speichern.

### <a name="data-partitioning"></a>Datenpartitionierung

Im Data Warehouse eines Unternehmens können Faktentabellen Milliarden von Zeilen enthalten. Die Partitionierung ist eine Möglichkeit, die Verwaltung und Abfrage dieser Tabellen zu optimieren, indem sie aufgeteilt werden, um die Menge der beim Ausführen von Abfragen verarbeiteten Daten zu reduzieren. Die Partitionierungsspezifikation für eine Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

Sie können nur ein Feld pro Tabelle für die Partitionierung verwenden. Häufig handelt es sich dabei um ein Datumsfeld, da viele Abfragen nach einem Datum oder Datumsbereich gefiltert werden. Sie können die Partitionierung einer Tabelle nach dem ersten Laden bei Bedarf ändern. Dazu erstellen Sie die Tabelle mit der neuen Verteilung mithilfe der `CREATE TABLE AS SELECT`-Anweisung neu.

#### <a name="partitioning-for-query-optimization"></a>Partitionierung für die Abfrageoptimierung

Wenn Abfragen für eine große Faktentabelle häufig nach einer bestimmten Datenspalte gefiltert werden, kann durch die Partitionierung anhand dieser Spalte die Datenmenge, die zum Ausführen der Abfragen verarbeitet werden muss, erheblich reduziert werden. Ein gängiges Beispiel ist die Verwendung eines Datumsfelds, um die Tabelle in kleinere Gruppen aufzuteilen. Jede Gruppe enthält Daten für einen einzelnen Tag. Wenn eine Abfrage eine `WHERE`-Klausel enthält, die nach dem Datum filtert, muss nur auf die Partitionen zugegriffen werden, die dem Datumsfilter entsprechen.

#### <a name="partitioning-for-optimization-of-table-maintenance"></a>Partitionierung zur Optimierung der Tabellenpflege

In Data-Warehouse-Umgebungen ist es üblich, ein rollierendes Fenster detaillierter Faktendaten zu pflegen. Ein Beispiel hierfür sind Verkaufstransaktionen, die fünf Jahre zurückgehen. Durch eine Partitionierung anhand des Verkaufsdatums wird das Entfernen alter Daten, die über das rollierende Fenster hinausgehen, wesentlich effizienter. Das Löschen der ältesten Partition geht schneller und braucht weniger Ressourcen als das Löschen aller einzelnen Zeilen.

### <a name="statistics"></a>Statistik

Wenn eine Abfrage an Azure Synapse Analytics übermittelt wird, wird sie zuerst vom Abfrageoptimierer verarbeitet. Der Optimierer bestimmt die besten internen Methoden, um die Abfrage effizient auszuführen.

Zudem vergleicht der Optimierer die verschiedenen Abfrageausführungspläne, die auf Grundlage eines kostenbasierten Algorithmus verfügbar sind. Die Genauigkeit der Kostenschätzungen hängt von der verfügbaren Statistik ab. Sie sollten deshalb dafür sorgen, dass die Statistiken auf dem neuesten Stand sind.

Wenn in Azure Synapse Analytics die Option `AUTO_CREATE_STATISTICS` aktiviert ist, wird eine automatische Aktualisierung der Statistiken ausgelöst. Sie können Statistiken auch manuell über den Befehl `CREATE STATISTICS` erstellen oder aktualisieren.

Aktualisieren Sie Statistiken, wenn sich der Inhalt erheblich geändert hat (z. B. bei einem täglichen Update). Diese Aktualisierung kann in einen ETL-Prozess integriert werden.

Für alle Tabellen in der Datenbank sollten Statistiken in mindestens einer Spalte erfasst werden. Dadurch wird sichergestellt, dass grundlegende Informationen wie die Zeilenanzahl und die Tabellengröße für den Optimierer verfügbar sind. Weitere Spalten, für die Statistiken gesammelt werden sollten, sind Spalten, die bei der `JOIN`-, `DISTINCT`-, `ORDER BY`- und `GROUP BY`-Verarbeitung angegeben werden.

### <a name="workload-management"></a>Workloadverwaltung

Azure Synapse Analytics enthält umfassende Features zur Verwaltung der Ressourcennutzung bei gemischten Workloads. Das Erstellen von Ressourcenklassen für verschiedene Arbeitsauslastungen (wie Abfragen und Datenladevorgänge) ist bei der Verwaltung Ihrer Arbeitsauslastung hilfreich. So werden die Anzahl gleichzeitiger Abfragen und die den Abfragen zugewiesenen Computeressourcen begrenzt. Es gibt einen Kompromiss zwischen Arbeitsspeicher und Parallelität:

- Kleinere Ressourcenklassen verringern den maximalen Arbeitsspeicher pro Abfrage, erhöhen jedoch die Parallelität.
- Größere Ressourcenklassen erhöhen den maximalen Arbeitsspeicher pro Abfrage, verringern jedoch die Parallelität.

### <a name="performance-recommendations"></a>Empfehlungen zur Leistung

Verwenden Sie Methoden zur Leistungsverbesserung (z. B. Indizes, Datenverteilung), um Kandidaten für ähnliche Methoden in der neuen Zielumgebung zu erfassen. Führen Sie jedoch einen Vergleichstest durch, um zu bestätigen, dass diese in Azure Synapse Analytics notwendig sind. Fügen Sie `COLLECT STATISTICS`-Schritte in ETL- oder ELT-Prozesse ein, um sicherzustellen, dass die Statistiken aktuell sind, oder aktivieren Sie die automatische Erstellung von Statistiken.

Informieren Sie sich über die in Azure Synapse Analytics verfügbaren Optimierungsoptionen und die Leistungsmerkmale zugehöriger Hilfsprogramme, z. B. PolyBase für schnelles paralleles Laden von Daten. Verwenden Sie diese Optionen, um eine effiziente End-to-End-Implementierung zu erstellen.

Nutzen Sie die Flexibilität, Skalierbarkeit und Leistungsfähigkeit der Azure-Umgebung, um Änderungen des Datenmodells oder Optionen zur Leistungsoptimierung zu implementieren. Dadurch werden die Auswirkungen auf vorhandene Quellsysteme verringert.

Informieren Sie sich über die dynamischen Verwaltungssichten, die in Azure Synapse Analytics verfügbar sind. Diese Sichten bieten sowohl Informationen zur systemweiten Ressourcennutzung als auch zur Ausführung einzelner Abfragen.

Informieren Sie sich über Azure-Ressourcenklassen, und weisen Sie diese entsprechend zu, um eine effiziente Verwaltung gemischter Workloads und Parallelität zu gewährleisten.

Ziehen Sie die Verwendung einer Virtualisierungsschicht für die Azure Synapse Analytics-Umgebung in Erwägung. Sie kann Änderungen an der Warehouse-Implementierung vor Geschäftskunden und Berichterstattungstools abschirmen.

Machen Sie sich mit den von Partnern bereitgestellten Migrationstools und -diensten wie Qlik Replicate für Microsoft-Migrationen, WhereScape und Datometry vertraut. Mit diesen Diensten können Teile des Migrationsprozesses automatisiert und die benötigte Zeit sowie das mit einem Migrationsprojekt verbundene Risiko reduziert werden.
