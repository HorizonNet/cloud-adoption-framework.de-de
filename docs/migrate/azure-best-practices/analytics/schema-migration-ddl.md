---
title: Datendefinitionssprachen (DDLs) für die Schemamigration
description: Verwenden Sie Azure Synapse-Features, um Anforderungen hinsichtlich Hochverfügbarkeit und Notfallwiederherstellung zu erfüllen.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 50c4233325ffd1663331d0bf36d5fcb4b32cda7b
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452589"
---
<!-- cSpell:ignore DDLs Attunity "Attunity Replicate" "Attunity Visibility" Inmon Denodo Teradata Netezza Wherescape DMVs multinode equi Datometry -->

# <a name="schema-migration-data-definition-languages-ddls"></a>Datendefinitionssprachen (DDLs) für die Schemamigration

## <a name="design-considerations"></a>Überlegungen zum Entwurf

### <a name="preparation-for-migration"></a>Vorbereitung für die Migration

Bei der Vorbereitung für die Migration vorhandener Daten zu Azure Synapse Analytics ist es wichtig, den Umfang des Migrationsdurchlaufs eindeutig zu definieren (insbesondere für ein erstes Migrationsprojekt). Die Zeit, die im Vorfeld für das Verstehen der zu migrierenden Datenbankobjekte und zugehörigen Prozesse aufgewendet wird, macht sich später im Projekt durch weniger Aufwand und ein geringeres Risiko bezahlt.

Erfassen Sie den Bestand an zu migrierenden Datenbankobjekten. Je nach Quellplattform umfasst dieser Bestand einige oder alle der folgenden Objekte:

- Tabellen
- Sichten
- Indizes
- Funktionen
- Gespeicherte Prozeduren
- Datenverteilung und -partitionierung

Die grundlegenden Informationen für diese Objekte (einschließlich Metriken wie Zeilenanzahl, physische Größe, Datenkomprimierungsraten und Objektabhängigkeiten) sollten über Abfragen von Systemkatalogtabellen im Quellsystem verfügbar sein. Die Systemmetadaten sind die beste Quelle für diese Informationen. Die externe Dokumentation ist möglicherweise veraltet und umfasst nicht die Änderungen, die seit der anfänglichen Implementierung an der Datenstruktur vorgenommen wurden.

Es kann auch möglich sein, die tatsächliche Objektnutzung anhand von Abfrageprotokollen zu analysieren oder Tools von Microsoft-Partnern zu verwenden, z. B. Attunity Visibility. Möglicherweise müssen einige Tabellen nicht migriert werden, da sie nicht mehr in Produktionsabfragen verwendet werden.

Informationen zu Datengröße und Workload (z. B. der erforderliche Grad an Parallelität ) sind wichtig, da sie zum Definieren einer geeignete Konfiguration für Azure Synapse Analytics verwendet werden. Außerdem empfiehlt es sich, das erwartete zukünftige Wachstum von Daten und Workload zu kennen, da sich dies auch auf die empfohlene Zielkonfiguration auswirken kann.

Wenn Sie Datenvolumen verwenden, um den für die neue Zielplattform benötigten Speicher zu schätzen, ist es wichtig, Kenntnisse über die Datenkomprimierungsrate (sofern vorhanden) in der Quelldatenbank zu haben. Einfach von der Menge des auf dem Quellsystem verwendeten Speichers auszugehen, ist wahrscheinlich die falsche Grundlage für eine Größenbestimmung. Es sollte möglich sein, aus Überwachungs- und Metadateninformationen die Größe der unkomprimierten Rohdaten sowie den Mehraufwand für Indizierung, Datenreplikation, Protokollierung oder andere Prozesse im aktuellen System zu ermitteln.

Die Größe der unkomprimierten Rohdaten in den zu migrierenden Tabellen ist ein guter Ausgangspunkt für das Schätzen des Speichers, der in der neuen Azure Synapse Analytics-Zielumgebung erforderlich ist.

Es gibt auch auf der neuen Zielplattform einen Komprimierungsfaktor und Indizierungsaufwand, doch unterscheiden sich diese wahrscheinlich vom Quellsystem. Im Preis für Azure Synapse Analytics-Speicher sind auch Momentaufnahmesicherungen für sieben Tage enthalten. Dies kann sich auf die Gesamtkosten für den benötigten Speicher im Vergleich zur vorhandenen Umgebung auswirken.

Der Prozess zur Leistungsoptimierung für Datenmodelle kann auf einen späten Zeitpunkt im Migrationsprozess verschoben werden, sodass er dann stattfindet, wenn im Data Warehouse echte Datenvolumen vorhanden sind. Es wird jedoch empfohlen, dass einige Optionen zur Leistungsoptimierung bereits früher in diesem Prozess implementiert werden können. Beispielsweise ist es in Azure Synapse Analytics im Allgemeinen sinnvoll, kleine Dimensionstabellen als replizierte Tabellen und große Faktentabellen als gruppierte Columnstore-Indizes zu definieren. Ebenso geben Indizes, die in der Quellumgebung definiert sind, einen guten Hinweis darauf, welche Spalten von der Indizierung in der neuen Umgebung profitieren können. Wenn Sie diese Informationen beim anfänglichen Definieren der Tabellen vor dem Laden verwenden, sparen Sie später im Prozess Zeit.

Es empfiehlt sich, die Komprimierungsrate und den Indizierungsaufwand für Ihre eigenen Daten bei Fortschreiten des Migrationsprozesses in Azure Synapse Analytics zu messen. Diese Messung ermöglicht eine zukünftige Kapazitätsplanung.

Möglicherweise kann auch das vorhandene Data Warehouse vor der Migration vereinfacht werden, indem die Komplexität für eine einfache Migration verringert wird. Dies kann Folgendes umfassen:

- Entfernen oder Archivieren nicht verwendeter Tabellen vor der Migration, um eine Migration nicht verwendeter Daten zu vermeiden. Durch Archivieren in Azure Blob Storage und Definieren der Daten als externe Tabelle können die Daten zwar verfügbar bleiben, aber zu geringeren Kosten.
- Konvertieren physischer Data Marts in virtuelle Data Marts mithilfe von Datenvirtualisierungssoftware, um den Migrationsumfang zu verringern. Diese Konvertierung verbessert auch die Agilität und senkt die Gesamtkosten und kann als Modernisierung während der Migration angesehen werden.

Ein Ziel des Migrationsdurchlaufs kann auch die Modernisierung des Warehouse durch Änderung des zugrunde liegende Datenmodells sein, z. B. der Wechsel von einem Inmon-Datenmodell zu einem Ansatz mit Datentresor. Dies sollte im Rahmen der Vorbereitungsphase entschieden und eine Strategie für den Übergang in den Migrationsplan integriert werden. In diesem Szenario wird empfohlen, zuerst das Datenmodell unverändert auf die neue Plattform zu migrieren und dann den Übergang zum neuen Modell in Azure Synapse Analytics vorzunehmen, wobei die Skalierbarkeit und die Leistungsmerkmale der Plattform genutzt werden, um die Transformation ohne Auswirkung auf das Quellsystem auszuführen.

### <a name="data-model-migration"></a>Datenmodellmigration

Je nach Plattform und Ursprüngen des Quellsystems kann das Datenmodell einiger oder aller Teile möglicherweise bereits die Form eines Stern- oder Schneeflockenschemas aufweisen. In diesem Fall kann es direkt in unveränderter Form zu Azure Synapse Analytics migriert werden. Dieses Szenario stellt die einfachste und risikoärmste Migration dar, die erreicht werden kann. Eine Migration in unverändertem Zustand kann auch die erste Phase einer komplexeren Migration sein, die einen Übergang zu einem neuen zugrunde liegenden Datenmodell umfasst, z. B. zu einem Datentresor, wie es oben beschrieben ist.

Zwar kann eine beliebige Gruppe relationaler Tabellen und Sichten zu Azure Synapse Analytics migriert werden, doch bietet bei Workloads mit Analyseabfragen eines großen Datasets ein Stern- oder Schneeflocken-Datenmodell in der Regel die beste Gesamtleistung. Wenn das Quelldatenmodell noch nicht in dieser Form vorliegt, kann es sinnvoll sein, den Migrationsprozess zur Umstrukturierung des Modells zu nutzen.

Wenn im Rahmen des Migrationsprojekts Änderungen am Datenmodell vorgenommen werden, empfiehlt es sich, diese Änderungen in der neuen Zielumgebung auszuführen. Das bedeutet, dass Sie zuerst das vorhandene Modell migrieren und dann die Leistungsfähigkeit und Flexibilität von Azure Synapse Analytics nutzen, um die Daten dort in das neue Modell umzuwandeln. Durch diesen Ansatz werden die Auswirkungen auf das vorhandene System minimiert und die Leistung und Skalierbarkeit von Azure Synapse Analytics genutzt, um alle Änderungen schnell und kostengünstig vorzunehmen.

Das vorhandene System, das migriert werden soll, kann in Form mehrerer Schichten implementiert sein (z. B. Datenerfassungs-/Stagingschicht, Data Warehouse-Schicht und Berichts- oder Data Marts-Schicht), die jeweils aus einer Reihe von relationalen Tabellen und Sichten bestehen. Obwohl diese alle unverändert zu Azure Synapse Analytics migriert werden können, kann es kostengünstiger und leistungsfähiger sein, einige Features und Funktionen des Azure-Ökosystems zu nutzen, anstatt alles direkt zu migrieren. Beispiel:

- **Datenerfassung und Staging:** Für einen Teil des ETL/ELT-Prozesses kann Azure Blob Storage in Verbindung mit PolyBase für schnelles paralleles Laden von Daten anstelle von relationalen Tabellen verwendet werden.
- **Berichtsschicht und Data Marts:** Die Leistungsmerkmale von Azure Synapse Analytics machen es möglicherweise überflüssig, aggregierte Tabellen für Berichtszwecke oder Data Marts physisch zu instanziieren. Diese können möglicherweise als Sichten auf das zentrale Data Warehouse oder über eine Datenvirtualisierungsschicht eines Drittanbieters implementiert werden. Auf der Basisebene können der Prozess für die Migration von Verlaufsdaten und möglicherweise auch inkrementelle Aktualisierungen wie nachfolgend dargestellt erreicht werden:

![Modernes Data Warehouse](../../../_images/analytics/schema-migration-ddl.png)

Wenn diese oder ähnliche Ansätze verwendet werden können, wird die Anzahl der zu migrierenden Tabellen reduziert und einige Prozesse können vereinfacht oder ausgelassen werden, wodurch sich die Migrationsworkload ebenfalls verringert. Die Anwendbarkeit dieser Ansätze hängt vom jeweiligen Anwendungsfall ab. Das allgemeine Prinzip ist jedoch, nach Möglichkeit die Features und Funktionen des Azure-Ökosystems zu verwenden, um die Migrationsworkload zu reduzieren und eine kostengünstige Zielumgebung zu erstellen. Dies gilt auch für andere Funktionen wie Sicherung/Wiederherstellung und Workflowverwaltung und -überwachung.

Es stehen außerdem Produkte und Dienste von Microsoft-Partnern zur Verfügung, die bei der Data Warehouse-Migration helfen und in einigen Fällen Teile des Prozesses automatisieren. Wenn das vorhandene System ein ETL-Produkt eines Drittanbieters enthält, ist es möglich, dass dieses bereits Azure Synapse Analytics als Zielumgebung unterstützt und die vorhandenen ETL-Workflows an das neue Azure SQL Data Warehouse als Ziel umgeleitet werden können.

### <a name="data-marts-physical-or-virtual"></a>Data Marts: physisch oder virtuell

In älteren Data Warehouse-Umgebungen ist es üblich, eine Reihe von Data Marts zu erstellen, die so strukturiert sind, dass sie eine gute Leistung für Ad-hoc-Self-Service-Abfragen und Berichte für eine bestimmte Abteilung oder Geschäftsfunktion innerhalb einer Organisation bieten. Daher besteht ein Data Mart in der Regel aus einer Teilmenge des Data Warehouse, die aggregierte Versionen der Daten in einer Form enthält, die Benutzern das einfache Abfragen dieser Daten mit schnellen Reaktionszeiten über benutzerfreundliche Abfragetools wie Tableau, MicroStrategy oder Microsoft Power BI ermöglicht. Bei dieser Form handelt es sich im Allgemeinen um ein dimensionales Datenmodell, und eine Verwendung von Data Marts besteht darin, die Daten in einer nutzbaren Form verfügbar zu machen, selbst wenn das zugrunde liegende Warehouse-Datenmodell etwas anderes ist (z. B. ein Datentresor). Dieser Ansatz wird auch als Modell mit drei Ebenen bezeichnet.

Es können auch separate Data Marts für einzelne Geschäftseinheiten innerhalb einer Organisation verwendet werden, um robuste Datensicherheitsregelungen zu implementieren, indem nur der Benutzerzugriff auf bestimmte, relevante Data Marts gewährt und sensible Daten entfernt, verborgen oder anonymisiert werden.

Wenn diese Data Marts als physische Tabellen implementiert werden, benötigen sie zusätzliche Speicherressourcen, um sie zu speichern, und zusätzliche Verarbeitungsschritte, um sie in regelmäßigen Abständen zu erstellen und zu aktualisieren. Dies bedeutet auch, dass die Aktualität der Daten im Data Mart nur dem letzten Aktualisierungsvorgang entspricht und sie daher möglicherweise nicht für stark veränderliche Datendashboards geeignet sind.

Mit der Einführung relativ kostengünstiger skalierbarer MPP-Architekturen (Massively Parallel Processing) wie Azure Synapse Analytics und deren inhärenten Leistungsmerkmalen kann es sein, dass Data Mart-Funktionalität bereitgestellt werden kann, ohne das Data Mart als eine Gruppe physischer Tabellen instanziieren zu müssen. Dies wird durch eine effektive Virtualisierung der Data Marts über SQL-Sichten auf das zentrale Data Warehouse oder über eine Virtualisierungsschicht mithilfe von Features wie Sichten in Azure Synapse Analytics oder Virtualisierungsprodukte von Drittanbietern (z. B. Denodo) erreicht. Durch diesen Ansatz wird die Notwendigkeit von zusätzlichem Speicher und Aggregationsverarbeitung vereinfacht oder entfällt ganz, und die Gesamtzahl der zu migrierenden Datenbankobjekte wird reduziert.

Dieser Ansatz bietet auch einen weiteren potenziellen Nutzen. Durch Implementierung der Aggregations- und Joinlogik innerhalb einer Virtualisierungsschicht und die Darstellung externer Berichtstools über eine virtualisierte Sicht wird die zum Erstellen dieser Sichten erforderliche Verarbeitung per Push an das Data Warehouse übertragen. Dies ist in der Regel der beste Ort zum Ausführen von Vorgängen wie Joins und Aggregationen für große Datenvolumen.

Die Hauptgründe für die Implementierung physischer oder virtueller Data Marts sind:

- Mehr Agilität, da ein virtuelles Data Mart leichter zu ändern ist als physische Tabellen und die zugehörigen ETL-Prozesse.
- Geringere Gesamtkosten aufgrund weniger Datenspeicher und Datenkopien in einer virtualisierten Implementierung.
- Aufhebung zu migrierender ETL-Aufträge und vereinfachte DW-Architektur in einer virtualisierten Umgebung.
- Leistung: Zwar waren in der Vergangenheit physische Data Marts leistungsfähiger, doch werden nun durch Virtualisierungsprodukte intelligente Cachingverfahren implementiert, um dies auszugleichen.

Datenvirtualisierung kann auch verwendet werden, um Endbenutzern während eines Migrationsprojekts eine konsistente Sicht auf die Daten zu bieten.

### <a name="data-mapping"></a>Datenzuordnung

**Schlüssel- und Integritätseinschränkungen in Azure Synapse Analytics:**

Primärschlüssel- und Fremdschlüsseleinschränkungen werden derzeit innerhalb von Azure Synapse Analytics nicht erzwungen, doch kann die Definition für `PRIMARY KEY` mit der `NOT ENFORCED`-Klausel in die `CREATE TABLE`-Anweisung aufgenommen werden. Dies bedeutet, dass Berichtsprodukte von Drittanbietern die Metadaten für die Tabelle verwenden können, um die Schlüssel im Datenmodell zu verstehen und somit die effizientesten Abfragen zu generieren.

**Datentypunterstützung in Azure Synapse Analytics:**

Einige Legacydatenbanksysteme bieten Unterstützung für Datentypen, die derzeit in Azure Synapse-Analysen nicht direkt unterstützt werden. Diese Datentypen können jedoch im Allgemeinen entweder mithilfe eines unterstützten Datentyps zum Speichern der Daten in unveränderter Form oder durch Transformieren der Daten in einen unterstützten Datentyp verarbeitet werden.

Es folgt eine alphabetische Liste der unterstützten Datentypen:

<!-- TODO: Review format of this list. Are the arguments necessary for this list? -->

<!-- docsTest:disable -->

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

<!-- docsTest:enable -->

In der folgenden Tabelle sind einige gebräuchliche Datentypen, die derzeit nicht unterstützt werden, zusammen mit der empfohlenen Vorgehensweise für die Speicherung dieser Daten in Azure Synapse Analytics aufgeführt. (Ausführliche Informationen für bestimmte Umgebungen wie Teradata oder Netezza finden Sie in den zugehörigen Dokumenten.)

| **Nicht unterstützter Datentyp** | **Problemumgehung**                                                      |
|-----------------------|-----------------------------------------------------------------|
| `geometry`              | `varbinary`                                                       |
| `geography`             | `varbinary`                                                       |
| `hierarchyid`           | `nvarchar(4000)`                                                  |
| `image`                 | `varbinary`                                                       |
| `text`                  | `varchar`                                                         |
| `ntext`                 | `nvarchar`                                                        |
| `sql_variant`           | Unterteilen der Spalte in mehrere Spalten mit starker Typisierung                |
| `table`                 | Konvertieren in temporäre Tabellen                                     |
| `timestamp`             | Anpassen des Codes für die Verwendung von `datetime2` und `CURRENT_TIMESTAMP`-Funktion |
| `xml`                   | `varchar`                                                         |
| Benutzerdefinierter Typ     | Rückkonvertieren in nativen Datentyp (wenn möglich)              |

**Mögliche Datenprobleme:**

Je nach Quellumgebung gibt es einige Punkte, die beim Migrieren von Daten Probleme verursachen können:

- Es kann geringfügige Unterschiede bei der Verarbeitung von `NULL`-Daten in verschiedenen Datenbankprodukten geben. Dies betrifft z. B. die Sortierreihenfolge und die Handhabung leerer Zeichenfolgen.
- `DATE`-, `TIME`-, `INTERVAL`-, `TIME ZONE`-Daten und zugehörige Funktionen können von Produkt zu Produkt stark variieren.

Testen Sie diese gründlich, um sicherzustellen, dass die gewünschten Ergebnisse in der Zielumgebung erreicht werden. Beim Migrationsdurchlauf können auch Fehler oder falsche Ergebnisse aufgedeckt werden, die derzeit Teil des vorhandenen Quellsystems sind. Der Migrationsprozess ist eine gute Gelegenheit, eventuelle Anomalien zu beheben. Bewährte Methoden zum Definieren von Spalten in Azure Synapse Analytics: Es kommt häufig vor, dass in Legacysystemen Spalten gefunden werden, die mit ineffizienten Datentypen angegeben sind, z. B. ein als `VARCHAR(20)` definiertes Feld, wenn die tatsächlichen Datenwerte in ein `CHAR(5)`-Feld passen, oder `INTEGER`-Felder, wenn alle Werte in ein `SMALLINT`-Feld passen. Dies kann zu Ineffizienzen sowohl bei der Speicher- als auch der Abfrageleistung führen, insbesondere bei großen Faktentabellen.

Ein Migrationsdurchlauf kann ein guter Zeitpunkt sein, bestehende Datendefinitionen zu überprüfen und zu rationalisieren. Dies kann mithilfe von SQL-Abfragen automatisiert werden, um den maximalen numerischen Wert oder die maximale Zeichenlänge innerhalb eines Datenfelds zu suchen und mit dem Datentyp zu vergleichen. Dieses Feature wird auch von einigen Tools zum Durchsuchen von Daten oder Migrationstools von Drittanbietern genutzt.

Im Allgemeinen empfiehlt es sich, die gesamte definierte Zeilenlänge für eine Tabelle zu minimieren (z. B. durch Verwendung des kleinsten Datentyps für jede Spalte wie oben beschrieben), da dadurch die beste Abfrageleistung erzielt wird. Das Hilfsprogramm PolyBase, das die empfohlene Methode zum Laden von Daten aus externen Tabellen für Azure Synapse Analytics darstellt, unterstützt eine definierte Zeilenlänge von maximal 1 MB. Bei Zeilen mit einer Länge von mehr als 1 MB kann PolyBase nicht zum Laden der Tabelle verwendet werden. Stattdessen muss bcp verwendet werden.

Für eine möglichst effiziente Joinausführung definieren Sie die auf beiden Seiten des Joins verwendeten Spalten als denselben Datentyp. Wenn der Schlüssel einer Dimensionstabelle als `SMALLINT` definiert ist, sollten die entsprechenden Verweisspalten in Faktentabellen, die diese Dimension verwenden, ebenfalls als `SMALLINT` definiert werden.

Vermeiden Sie es, für Zeichenfelder eine große Standardgröße zu definieren. Wenn die maximale Größe der Daten in einem Feld 50 Zeichen beträgt, verwenden Sie `VARCHAR(50)`. Ebenso sollten Sie nicht `NVARCHAR` verwenden, wenn `VARCHAR` ausreicht. `NVARCHAR` speichert Unicode-Daten, um unterschiedliche Sprachzeichensätze zuzulassen, während `VARCHAR` ASCII-Daten speichert und weniger Speicherplatz benötigt.

## <a name="design-recommendations-summary"></a>Zusammenfassung der Entwurfsempfehlungen

Migrieren Sie keine unnötigen Objekte oder Prozesse. Verwenden Sie ggf. integrierte Features und Funktionen in der Azure-Zielumgebung, um die tatsächliche Anzahl der zu migrierenden Objekte und Prozesse zu verringern. Ziehen Sie die Verwendung einer Virtualisierungsschicht in Betracht, um die Anzahl der zu migrierenden physischen Data Marts zu reduzieren oder ganz auszuschließen und die Verarbeitung per Push an das Data Warehouse zu übertragen.

Nehmen Sie wann immer möglich eine Automatisierung vor. Verwenden Sie Metadaten aus Systemkatalogen im Quellsystem, um DDL für die Zielumgebung zu generieren. Automatisieren Sie nach Möglichkeit auch das Generieren der Dokumentation. Microsoft-Partner wie Wherescape können spezielle Tools und Dienste zur Unterstützung bereitstellen.

Führen Sie alle erforderlichen Änderungen des Datenmodells oder Optimierungen der Datenzuordnung auf der Zielplattform aus. Diese Änderungen können in Azure Synapse Analytics effizienter durchgeführt werden. Durch diese Vorgehensweise werden die Auswirkungen auf Quellsysteme verringert, die möglicherweise bereits nahezu voll ausgelastet sind.

## <a name="performance-options"></a>Leistungsoptionen

In diesem Abschnitt werden die Features beschrieben, die in Azure Synapse Analytics zur Verbesserung der Leistung für ein bestimmtes Datenmodell verfügbar sind.

### <a name="general-approach"></a>Allgemeiner Ansatz

Für die zu migrierende Datenbank wurde bereits eine Leistungsoptimierung anhand der auf dieser Plattform verfügbaren Features angewendet, z. B. Indizes, Datenpartitionierung und möglicherweise Datenverteilung. Im Rahmen der Vorbereitung für die Migration sollten diese dokumentiert werden, da dies ein guter Hinweis auf Optimierungen sein kann, die in der Azure Synapse Analytics-Zielumgebung angewendet werden können.

Beispielsweise kann das Vorhandensein eines nicht eindeutigen Index für eine Tabelle darauf hindeuten, dass die im Index verwendeten Felder häufig zum Filtern, Gruppieren oder Verknüpfen verwendet werden. Dies ist dann auch in der neuen Umgebung noch der Fall und sollte bei der Auswahl der dort zu indizierenden Felder berücksichtigt werden. Migrationsempfehlungen für bestimmte Quellplattformen wie Teradata und Netezza werden in separaten Dokumenten ausführlich beschrieben.

Nutzen Sie die Leistung und Skalierbarkeit der Azure Synapse Analytics-Zielumgebung, um mit verschiedenen Leistungsoptionen, wie beispielsweise der Datenverteilung, zu experimentieren und so die beste Auswahl alternativer Ansätze zu ermitteln (z. B. Replikation gegenüber Hashverteilung für eine große Dimensionstabelle). Dies bedeutet nicht, dass Daten aus externen Quellen neu geladen werden müssen. Alternative Ansätze können in Azure Synapse Analytics relativ schnell und einfach getestet werden, indem Sie Kopien einer beliebigen Tabelle über eine `CREATE TABLE AS SELECT`-Anweisung mit unterschiedlichen Partitionierungs- oder Verteilungsoptionen erstellen.

Verwenden Sie die Überwachungstools der Azure-Umgebung, um zu ermitteln, wie Abfragen ausgeführt werden und wo Engpässe auftreten können. Es stehen auch Tools von Microsoft-Partnern als Drittanbieter bereit, die Überwachungsdashboards sowie automatisierte Ressourcenverwaltung und Warnungen bieten.

Jeder SQL-Vorgang in Azure Synapse Analytics sowie die von dieser Abfrage verwendeten Ressourcen (z. B. Arbeitsspeicher oder CPU) werden in Systemtabellen protokolliert, und eine Reihe dynamischer Verwaltungssichten (DMVs) wird bereitgestellt, um den Zugriff auf diese Informationen zu vereinfachen.

In den folgenden Abschnitten werden die wichtigsten Optionen in Azure Data Warehouse zum Optimieren der Abfrageleistung erläutert. Vorhandene Umgebungen enthalten Informationen zur möglichen Optimierung in der Zielumgebung.

### <a name="temporary-tables"></a>Temporäre Tabellen

Azure Synapse Analytics unterstützt temporäre Tabellen, die nur für die Sitzung sichtbar sind, in der sie erstellt wurden, für die Dauer einer Benutzersitzung bestehen und am Ende der Sitzung automatisch gelöscht werden.

Zum Erstellen einer temporären Tabelle stellen Sie dem Tabellennamen das Hashzeichen (`#`) voran. Für temporäre Tabellen können alle üblichen Indizierungs- und Verteilungsoptionen verwendet werden (siehe unten).

Temporäre Tabellen weisen einige Einschränkungen auf:

- Das Umbenennen der Tabelle ist nicht zulässig.
- Sichten und Partitionen sind für temporäre Tabellen nicht zulässig.
- Berechtigungen für temporäre Tabellen können nicht geändert werden.

Temporäre Tabellen werden häufig innerhalb der ETL/ELT-Verarbeitung verwendet, wo vorübergehende Zwischenergebnisse als Teil eines Transformationsprozesses verwendet werden.

### <a name="table-distribution-options"></a>Tabellenverteilungsoptionen

Azure Synapse Analytics ist ein MPP-Datenbanksystem (Massively Parallel Processing), das Leistung und Skalierbarkeit durch parallele Ausführung über mehrere Verarbeitungsknoten erreicht.

Das ideale Verarbeitungsszenario beim Ausführen einer SQL-Abfrage in einer Umgebung mit mehreren Knoten besteht darin, die Workload so auszugleichen, dass alle Knoten eine gleich große Datenmenge zu verarbeiten haben, während gleichzeitig die Datenmenge, die zum Erfüllen der Abfrage zwischen Knoten verschoben werden muss, minimiert (oder vollständig aufgehoben) wird.

Bei typischen Analyseabfragen gibt es häufig mehrere Joins zwischen verschiedenen Tabellen (z. B. zwischen Faktentabellen und Dimensionstabellen) sowie Aggregationen. Daher kann es schwierig sein, das ideale Szenario zu erreichen.

Eine Möglichkeit, die Verarbeitung von Abfragen zu beeinflussen, ist die Verwendung der Verteilungsoptionen in Azure Synapse Analytics, um anzugeben, wo einzelne Datenzeilen der jeweiligen Tabellen gespeichert werden. Wenn z. B. in einer bestimmten Datenspalte wie `CUSTOMER_ID` häufig zwei große Tabellen verknüpft werden, werden durch die Verteilung der beiden Tabellen anhand der `CUSTOMER_ID`-Spalten bei jeder Ausführung dieses Joins die Daten auf beiden Seiten des Joins bereits auf demselben Verarbeitungsknoten zusammengestellt, sodass keine Daten mehr zwischen Knoten verschoben werden müssen. Die Verteilungsspezifikation für eine Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

Die verfügbaren Verteilungsoptionen und Empfehlungen zu deren Verwendung werden nachfolgend beschrieben. Die Verteilung einer Tabelle kann nach dem anfänglichen Laden bei Bedarf geändert werden. Dazu wird die Tabelle mit der neuen Verteilung anhand der `CREATE TABLE AS SELECT`-Anweisung neu erstellt.

#### <a name="round-robin"></a>Roundrobin

Diese Tabellenverteilung ist die Standardoption. Hierbei werden die Daten gleichmäßig auf die Knoten im System verteilt. Diese Methode eignet sich für das schnelle Laden von Daten und für Daten, die ein relativ geringes Volumen haben und nicht über einen offensichtlichen Kandidaten für Hashs verfügen. Sie wird daher häufig für Stagingtabellen im Rahmen eines ETL- oder ELT-Prozesses verwendet.

#### <a name="hashed"></a>Hash

Basierend auf einem Hashalgorithmus, der auf einen benutzerdefinierten Schlüssel angewendet wird (wie `CUSTOMER_ID` im Beispiel oben), weist das System die Zeile einem Hashbucket zu, der dann einem bestimmten Knoten zugewiesen wird. Alle Datenzeilen mit einer Hashverteilung für denselben Wert enden daher auf demselben Verarbeitungsknoten.

Diese Methode eignet sich für große Tabellen, die häufig für einen bestimmten Schlüssel verknüpft oder aggregiert werden. Bei anderen großen Tabellen, die verknüpft werden sollen, sollte nach Möglichkeit ein Hash für denselben Schlüssel verwendet werden. Wenn mehrere Kandidaten für den Hashschlüssel vorhanden sind, wählen Sie den am häufigsten verknüpften aus. Die Hashspalte sollte keine NULL-Werte enthalten und ist in der Regel kein Datum, da bei vielen Abfragen nach Datum gefiltert wird. Das Hashing ist in der Regel effizienter, wenn der Schlüssel für den Hash ein ganzzahliger Wert und nicht `CHAR` oder `VARCHAR` ist. Vermeiden Sie außerdem die Auswahl von Schlüsseln, die einen stark verzerrten Wertebereich aufweisen, wie z. B. eine kleine Anzahl von Schlüsselwerten, die einen hohen Prozentsatz der Datenzeilen darstellen.

#### <a name="replicated"></a>Replikation

Wenn Sie die Replikation als Verteilungsoption für eine Tabelle auswählen, wird für die Abfrageverarbeitung eine komplette Kopie dieser Tabelle auf jedem Computeknoten repliziert.

Diese Vorgehensweise ist bei relativ kleinen Tabellen nützlich (üblicherweise weniger als 2 GB in komprimierter Form), die relativ statisch sind und häufig über einen Gleichheitsjoin mit größeren Tabellen verknüpft werden. Bei diesen Tabellen handelt es sich häufig um Dimensionstabellen in einem Sternschema.

### <a name="indexing"></a>Indizierung

Azure Synapse Analytics bietet verschiedene Optionen zum Indizieren von Daten in großen Tabellen, um die Ressourcen und die Zeit, die zum Abrufen von Datensätzen benötigt werden, zu reduzieren:

- Gruppierter Columnstore-Index
- Gruppierter Index
- Nicht gruppierter Index

Es gibt auch eine nicht indizierte Option namens `HEAP` für Tabellen, die von keiner der Indexoptionen profitieren würden. Die Verwendung von Indizes bedeutet eine Abwägung zwischen verbesserten Abfragezeiten und längeren Ladezeiten sowie größerer Speicherplatznutzung. Indizes beschleunigen oft `SELECT`-, `UPDATE`-, `DELETE`- und `MERGE`-Vorgänge für große Tabellen, die einen kleinen Prozentsatz der Datenzeilen betreffen. Die Indizes können auch helfen, vollständige Tabellenscans zu vermeiden.

Indizes werden automatisch erstellt, wenn `UNIQUE`- oder `PRIMARY KEY`-Einschränkungen für Spalten definiert werden.

#### <a name="clustered-columnstore-index"></a>Gruppierter Columnstore-Index

Dies ist die Standardoption für die Indizierung in Azure Synapse Analytics und bietet die beste Komprimierung und Abfrageleistung für große Tabellen. Bei kleineren Tabellen (weniger als 60 Millionen Zeilen) sind diese Indizes nicht effizient, und es sollte daher die Heapoption verwendet werden. Ein Heap oder eine temporäre Tabelle kann auch effizienter sein, wenn die Daten in einer Tabelle vorübergehend sind (möglicherweise Teil eines ETL/ELT-Prozesses).

#### <a name="clustered-index"></a>Gruppierter Index

Wenn es erforderlich ist, eine einzelne Zeile oder eine kleine Anzahl von Zeilen regelmäßig aus einer großen Tabelle basierend auf einer starken Filterbedingung abzurufen, kann ein gruppierter Index effizienter als ein gruppierter Columnstore-Index sein. Pro Tabelle ist nur ein gruppierter Index zulässig. Replikation

#### <a name="non-clustered-index"></a>Nicht gruppierter Index

Nicht gruppierte Indizes ähneln gruppierten Indizes insofern, dass Sie den Abruf einzelner Zeilen oder einer kleinen Anzahl von Zeilen basierend auf einer Filterbedingung beschleunigen können. Intern werden nicht gruppierte Indizes getrennt von den Daten gespeichert, und es können mehrere nicht gruppierte Indizes für eine Tabelle definiert werden. Jeder zusätzliche Index benötigt jedoch weiteren Speicherplatz und verringert den Durchsatz beim Einfügen oder Laden von Daten.

#### <a name="heap"></a>Heap

Heaptabellen bedeuten keinen Aufwand im Zusammenhang mit der Erstellung und Verwaltung von Indizes zur Ladezeit der Daten und können daher zum schnellen Laden vorübergehender Daten (z. B. im Rahmen eines ETL-Prozesses) nützlich sein. Lesevorgänge der Daten, die unmittelbar folgen, können in diesem Fall auch vom Caching profitieren. Heaptabellen können auch nützlich sein, um Tabellen mit weniger als 60 Millionen Zeilen zu speichern, da gruppierte Columnstore-Indizes unterhalb dieser Größe ineffizient sind.

### <a name="data-partitioning"></a>Datenpartitionierung

Im Data Warehouse eines Unternehmens können Faktentabellen viele Milliarden von Zeilen enthalten, und die Partitionierung ist eine Möglichkeit, die Verwaltung und Abfrage dieser Tabellen zu optimieren, indem sie in separate Teile aufgeteilt werden, um die Menge der beim Ausführen von Abfragen verarbeiteten Daten zu reduzieren. Die Partitionierungsspezifikation für eine Tabelle wird in der `CREATE TABLE`-Anweisung definiert.

Für die Partitionierung kann nur ein Feld pro Tabelle verwendet werden. Hierbei handelt es sich häufig um ein Datumsfeld, da viele Abfragen nach einem Datum oder Datumsbereich gefiltert werden. Sie können die Partitionierung einer Tabelle nach dem anfänglichen Laden bei Bedarf ändern. Dazu erstellen Sie die Tabelle mit der neuen Verteilung anhand der `CREATE TABLE AS SELECT`-Anweisung neu.

#### <a name="partitioning-for-query-optimization"></a>Partitionierung für die Abfrageoptimierung

Wenn Abfragen für eine große Faktentabelle häufig nach einer bestimmten Datenspalte gefiltert werden, kann durch die Partitionierung anhand dieser Spalte die Datenmenge, die zum Ausführen der Abfragen verarbeitet werden muss, erheblich reduziert werden. Ein gängiges Beispiel ist die Verwendung eines Datumsfelds, um die Tabelle in kleinere Gruppen aufzuteilen, die jeweils Daten für einen einzelnen Tag enthalten. Wenn eine Abfrage eine `WHERE`-Klausel enthält, die nach dem Datum filtert, muss nur auf die Partitionen zugegriffen werden, die dem Datumsfilter entsprechen.

#### <a name="partitioning-for-table-maintenance-optimization"></a>Partitionierung für die Optimierung der Tabellenverwaltung

In Data Warehouse-Umgebungen ist es üblich, ein rollierendes Fenster mit detaillierten Faktendaten zu verwalten, z. B. Verkaufstransaktionen der letzten fünf Jahre. Durch eine Partitionierung anhand des Verkaufsdatums wird das Entfernen alter Daten, die über das rollierende Fenster hinausgehen, wesentlich effizienter. Das Löschen der ältesten Partition geht schneller und braucht weniger Ressourcen als das Löschen aller einzelnen Zeilen.

### <a name="statistics"></a>Statistik

Wenn eine Abfrage an Azure Synapse Analytics übermittelt wird, wird sie zuerst vom Abfrageoptimierer verarbeitet, der die besten internen Methoden zur effizienten Ausführung der Abfrage bestimmt. Der Optimierer vergleicht die verschiedenen Ausführungspläne für die Abfrage, die basierend auf einem kostenbasierten Algorithmus verfügbar sind. Die Genauigkeit der Kostenschätzungen hängt von der verfügbaren Statistik ab. Es empfiehlt sich deshalb, dafür zu sorgen, dass die Statistiken auf dem neuesten Stand sind.

Wenn in Azure Synapse Analytics die Option `AUTO_CREATE_STATISTICS` aktiviert ist, wird eine automatische Aktualisierung der Statistiken ausgelöst. Statistiken können auch manuell über den Befehl `CREATE STATISTICS` erstellt oder aktualisiert werden.

Aktualisieren Sie Statistiken, wenn sich der Inhalt erheblich geändert hat (z. B. bei einem täglichen Update). Diese Aktualisierung kann in den ETL-Prozess integriert werden.

Für alle Tabellen in der Datenbank sollten Statistiken zu mindestens einer Spalte gesammelt werden (um sicherzustellen, dass dem Optimierer grundlegende Informationen wie Zeilenanzahl und Tabellengröße zur Verfügung stehen). Weitere Spalten, für die Statistiken gesammelt werden sollten, sind Spalten, die bei der `JOIN`-, `DISTINCT`-, `ORDER BY`- und `GROUP BY`-Verarbeitung angegeben werden.

### <a name="workload-management"></a>Workloadverwaltung

Azure Synapse Analytics enthält umfassende Features zur Verwaltung der Ressourcennutzung bei gemischten Workloads. Das Erstellen von Ressourcenklassen für verschiedene Workloadtypen (z. B. Abfragen gegenüber Laden von Daten) hilft Ihnen bei der Verwaltung Ihrer Workload, indem Grenzwerte für die Anzahl der gleichzeitig ausgeführten Abfragen und für die Computeressourcen, die den einzelnen Abfragen zugewiesen sind, festgelegt werden. Dabei erfolgt ein Ausgleich zwischen Speicher und Parallelität.

- Kleinere Ressourcenklassen verringern den maximalen Speicher pro Abfrage, erhöhen jedoch die Parallelität.
- Größere Ressourcenklassen erhöhen den maximalen Speicher pro Abfrage, verringern jedoch die Parallelität.

### <a name="performance-recommendations"></a>Empfehlungen zur Leistung

Verwenden Sie beliebige Methoden zur Leistungsverbesserung (z. B. Indizes, Datenverteilung) als Hinweis auf Kandidaten für ähnliche Maßnahmen in der neuen Zielumgebung, doch erstellen Sie Benchmarks, um zu bestätigen, dass sie in Azure Synapse Analytics erforderlich sind. Fügen Sie `COLLECT STATISTICS`-Schritte in ETL/ELT-Prozesse ein, um sicherzustellen, dass die Statistiken aktuell sind, oder aktivieren Sie die automatische Erstellung von Statistiken.

Informieren Sie sich über die in Azure Synapse Analytics verfügbaren Optimierungsoptionen und die Leistungsmerkmale zugehöriger Hilfsprogramme, z. B. PolyBase für schnelles paralleles Laden von Daten. Verwenden Sie diese Optionen, um eine effiziente End-to-End-Implementierung zu erstellen.

Nutzen Sie die Flexibilität, Skalierbarkeit und Leistung der Azure-Umgebung, um Änderungen des Datenmodells oder Optionen zur Leistungsoptimierung dort zu implementieren und so die Auswirkungen auf vorhandene Quellsysteme zu verringern.

Informieren Sie sich über die dynamischen Verwaltungssichten, die in Azure Synapse Analytics verfügbar sind, um sowohl Informationen zur systemweiten Ressourcennutzung als auch detaillierte Ausführungsinformationen für einzelne Abfragen bereitzustellen.

Informieren Sie sich über Azure-Ressourcenklassen, und weisen Sie diese entsprechend zu, um eine effiziente Verwaltung gemischter Workloads und Parallelität zu gewährleisten.

Verwenden Sie ggf. eine Virtualisierungsschicht als Teil der Azure Synapse Analytics-Umgebung, um Änderungen an der Warehouse-Implementierung vor Geschäftsbenutzern und Berichtstools zu schützen.

Erkunden Sie Migrationstools und Dienste, die von Drittanbietern bereitgestellt werden, z. B. Attunity Replicate für Microsoft-Migrationen, Wherescape und Datometry. Mit diesen Tools können Teile des Migrationsprozesses automatisiert und die benötigte Zeit sowie das mit einem Migrationsprojekt verbundene Risiko reduziert werden.
