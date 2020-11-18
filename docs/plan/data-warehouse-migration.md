---
title: Planen einer Data Warehouse-Migration
description: In diesem Artikel erhalten Sie Informationen zu Best Practices für die Data-Warehouse-Migration, zu den wichtigsten Schritte für den Prozess der Data-Warehouse-Migration und zu den in den einzelnen Schritten enthaltenen Aufgaben.
author: v-hanki
ms.author: janet
ms.date: 06/24/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 4a0d6d857481b3c3bbd73d44a81ff5fe72e4a3fd
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94712084"
---
<!-- cSpell:ignore Informatica gzipped Attunity -->

# <a name="plan-a-data-warehouse-migration"></a>Planen einer Data Warehouse-Migration

Eine Data-Warehouse-Migration ist eine Herausforderung für ein Unternehmen. Damit eine solche Migration erfolgreich umgesetzt werden kann und dabei nicht willkommene Überraschungen und unerwartete Kosten vermieden werden können, müssen Sie für diese Herausforderung gründliche Recherche betreiben, Risiken ausschließen und die Migration so planen, dass Sie bestmöglich darauf vorbereitet sind. Allgemein gesprochen sollte Ihr Plan die wichtigsten Schritte für den Data-Warehouse-Migrationsprozess beinhalten sowie die darin eingeschlossenen Aufgaben. Die Schritte des Hauptprozesses sind die folgenden:

- Vorbereitungen vor der Migration
- Strategie für die Migration und Ausführung
- Nach der Migration

Zur Vorbereitung gehören beispielsweise Aufgaben wie das Vorbereiten des Teams für die Data-Warehouse-Migration, z. B. durch Trainingsangebote für die erforderlichen Fähigkeiten und der Möglichkeit, sich näher mit der Thematik auseinanderzusetzen. Außerdem gehört das Einrichten eines Proof-of-Concept-Labs, ein Verständnis für die Verwaltung der Test- und Produktionsumgebungen, das Schaffen der Möglichkeiten, um Ihre Daten und ein Produktionssystem außerhalb der Firewall Ihres Unternehmens migrieren zu können, und das Einrichten der Software für die Migration in Ihrem Rechenzentrum dazu, um die Migration vorantreiben zu können.

Damit die Data-Warehouse-Migration problemlos fortgesetzt werden kann, sollte in Ihrem Plan ein klares Verständnis folgender Punkte enthalten sein:

- Ihr Geschäftsszenario einschließlich der Motivation, Geschäftsvorteile und Risiken
- Rollen und Zuständigkeiten im Migrationsteam
- Die erforderlichen Fähigkeiten und dazugehöriges Training für eine erfolgreiche Migration
- Zugewiesenes Budget für die vollständige Migration
- Ihre Migrationsstrategie
- Vermeidung von Risiken im Migrationsprojekt zur Vermeidung von Verzögerungen und Nacharbeiten
- Ihr vorhandenes Data-Warehouse-System, seine Architektur, sein Schema, die Datenvolumes, Datenflüsse und betrieblichen Abhängigkeiten
- Unterschiede zwischen Datenbank-Managementsystemen für Ihr vorhandenes Data Warehouse und Azure Synapse, z. B. Datentypen, SQL-Funktionen, Logik und weitere Überlegungen
- Inhalte der Migration und Prioritäten
- Migrationsaufgaben, Ansätze, Reihenfolge und Fristen
- Steuerung der Migration
- Vermeiden von Unterbrechungen für Benutzer während der Migrationsausführung
- Lokale Aufgaben zur Vermeidung von Verzögerungen und für das Ermöglichen der Migration
- Tools für eine sichere Migration der Schemas, Daten und ETL-Verarbeitung zu Azure
- Während und nach der Migration erforderliche Änderungen am Entwurf des Datenmodells
- Technologieänderungen vor oder nach der Migration und Minimieren der Nacharbeiten
- Veralten der Technologie nach der Migration
- Implementieren von Tests und Qualitätssicherungsmaßnahmen als Nachweis für einen Erfolg
- Prüfpunkte zur Bewertung des Fortschritts und Ermöglichen von Entscheidungsfindungen
- Notfallplan und Rollbackpunkte im Fall von Fehlern

Bestimmte Aktivitäten müssen vorbereitet und eingeleitet werden, noch bevor die Migration beginnt, um ein Verständnis für die erwähnten Punkte zu erlangen. Sehen Sie sich im Folgenden noch genauer an, was dies beinhaltet.

## <a name="pre-migration-preparation"></a>Vorbereitungen vor der Migration

Es gibt mehrere Dinge, die geklärt werden müssen, noch bevor Sie mit der Data-Warehouse-Migration beginnen.

### <a name="key-roles-in-a-data-warehouse-migration-team"></a>Wichtige Rollen im Team für eine Data-Warehouse-Migration

Zu den wichtigsten Rollen eines Migrationsprojekts gehören die folgenden:

- Geschäftsinhaber
- Projektmanager (mit agilen Methodologieerfahrungen, z. B. Scrum)
- Projektkoordinator
- Cloud Engineer
- Datenbankadministrator (vorhandenes Datenbank-Managementsystem für ein Data Warehouse und Azure Synapse)
- Entwickler von Datenmodellen
- ETL-Entwickler
- Experten für Datenvirtualisierungen (z. B. Datenbankadministrator)
- Entwickler für Tests
- Business Analysts (für Tests von Abfragen, Berichten und Analysen von Business Intelligence-Tools)

Außerdem benötigt Ihr Team die Unterstützung des Teams für die lokale Infrastruktur.

### <a name="skills-and-training-to-ready-the-team-for-migration"></a>Fähigkeiten und dazugehöriges Training als Vorbereitung des Teams für die Migration

In Bezug auf erforderliche Fähigkeiten spielt Fachwissen bei der Data-Warehouse-Migration eine große Rolle. Sorgen Sie deshalb dafür, dass die entsprechenden Mitglieder Ihres Migrationsteams Erfahrungen mit den Grundlagen zur Cloud in Azure, mit Azure Blob Storage, Azure Data Lake Storage, Azure Data Box, ExpressRoute, der Identitätsverwaltung mithilfe von Azure, Azure Data Factory und Azure Synapse sammeln können. Die Ersteller von Datenmodellen müssen höchstwahrscheinlich Ihre Datenmodelle in Microsoft Azure Synapse optimieren, sobald die Migration Ihres vorhandenen Data Warehouse durchgeführt wurde.

### <a name="assessing-your-existing-data-warehouse"></a>Bewerten Ihres vorhandenen Data Warehouse

Ein weiterer Bestandteil der Vorbereitungen für eine Migration ist es, Ihr vorhandenes Data Warehouse vollständig zu bewerten, um ein umfassendes Verständnis für die Architektur, die Datenspeicher, Schemas, Geschäftslogik, Datenflüsse und die verwendeten Funktionen eines Datenbank-Managementsystems, die Vorgänge im Data Warehouse und die Abhängigkeiten zu erlangen. Je mehr Verständnis hier erlangt werden kann, desto besser. Ein detailliertes Verständnis der Funktionsweise des Systems erleichtert die Kommunikation und Information aller Beteiligten.

Der Zweck einer Bewertung besteht nicht nur in einem detaillierten Verständnis dafür, wie das Migrationsteam gegenwärtig aufgestellt ist, sondern auch dafür, Stärken und Schwächen in dieser Aufstellung zu erkennen. Das Ergebnis einer Bewertung Ihres aktuellen Data Warehouse kann sich deshalb auf Ihre Migrationsstrategie auswirken, im Sinne einer Verschiebung zu einer größer angelegten Migration. Wenn als Ergebnis einer Bewertung beispielsweise festgehalten wird, dass die Lebensdauer Ihres Data Warehouse beinahe abgelaufen ist, sollte die Strategie eindeutig so ausgerichtet werden, dass die Datenmigration in ein neu entworfenes Data Warehouse bei Azure Synapse erfolgt, anstatt nur kleinere Verschiebungen vorzunehmen.

### <a name="on-premises-preparation-for-data-migration"></a>Lokale Vorbereitung für die Datenmigration

Zusätzlich zur Vorbereitung Ihres Migrationsteams für die Zielumgebung und einer Einschätzung Ihrer aktuellen Aufstellung ist es genauso wichtig, wichtige Aufgaben auch lokal anzustoßen, da Data Warehouses in der Produktion tendenziell stark von IT-Prozeduren und Genehmigungsprozessen abhängig sind. Zur Vermeidung von Verzögerungen sollten Sie dafür sorgen, dass Ihre Teams für die Rechenzentrumsinfrastruktur und den normalen Betrieb für die Migration der Daten, Schemas, ETL-Aufträge etc. zur Cloud in Azure bereit sind. Datenmigrationen können folgendermaßen ausgeführt werden:

- AzCopy zu Azure Blob Storage
- Microsoft Azure ExpressRoute zur direkten Übertragung komprimierter Daten zu Azure
- Dateiexport zu Azure Data Box

Die Hauptfaktoren, die beeinflussen, welche dieser Optionen ausgewählt wird, sind die Größe des Datenvolumes (in Terabyte) und die Netzwerkgeschwindigkeit (in MBit/s). Es muss berechnet werden, wie lange die Migration von Daten über das Netzwerk dauern würde. Dabei muss bedacht werden, dass die Daten in Ihrem Data Warehouse möglicherweise komprimiert sind und für den Export dekomprimiert werden müssen. Eine solche Situation kann die Datenübertragung verlangsamen. Wenn Daten über eine der oben erwähnten Methoden verschoben werden, können sie danach über Gzip wieder komprimiert werden. PolyBase kann über Gzip komprimierte Daten direkt verarbeiten. Große Datenvolumes werden wahrscheinlicher über Azure Data Box migriert, wenn es zu lange dauern würde, die Daten zu verschieben.

Außerdem muss eine selbstgehostete Integration-Runtime-Software in Ihrem Rechenzentrum installiert werden, damit die Migration fortgesetzt werden kann und Azure Data Factory die Ausführung der Datenexporte aus Ihrem vorhandenen Data Warehouse in Azure steuern kann. Angesichts dieser Anforderungen sollten Sie erforderliche Genehmigungsprozesse frühzeitig anstoßen, um Verzögerungen insgesamt auszuschließen, wenn formelle Genehmigungen für die Umsetzung der Migration erforderlich sind.

### <a name="azure-preparation-for-schema-and-data-migration"></a>Vorbereitung für die Schema- und Datenmigration in Azure

In Bezug auf eine Azure-seitige Vorbereitung muss der Datenimport entweder über Microsoft Azure ExpressRoute oder Microsoft Azure Data Box verwaltet werden. Azure Data Factory-Pipelines sind eine ideale Möglichkeit, Ihre Daten in Azure Blob Storage zu laden und sie dann von dort mithilfe von PolyBase in Azure Synapse zu laden. Deshalb ist auch eine Azure-seitige Vorbereitung erforderlich, um eine solche Pipeline zu entwickeln.

Die Alternative ist die Verwendung Ihres vorhandenen ETL-Tools in Azure, wenn dieses Azure Synapse unterstützt, d. h. das Einrichten des Tools in Azure über den Azure Marketplace und das Vorbereiten einer Pipeline für das Importieren und Laden Ihrer Daten in Azure Blob Storage.

## <a name="defining-a-migration-strategy"></a>Definieren einer Migrationsstrategie

### <a name="migration-goals"></a>Migrationsziele

Für jede Strategie sollten mehrere Ziele definiert werden, die auf einen Erfolg eines Projekts hinweisen können. Entsprechend dieser Ziele können dann kleinere Ziele abgesteckt werden, und einzelnen Personen kann dann die Verantwortung der Erreichung eines konkreten Ziels übertragen werden. Beispiele für Migrationsziele und entsprechende Metriken, für die kleinere Ziele in einem Data-Warehouse-Migrationsprojekt in die Cloud abgesteckt werden können, finden Sie in der folgenden Tabelle:

Beispiele für Typen von Zielen und Metriken:

#### <a name="improve-overall-performance"></a>Verbessern der Gesamtleistung

- Datenmigrationsleistung
- ETL-Leistung
- Leistung beim Laden von Daten
- Leistung komplexer Abfragen
- Anzahl gleichzeitiger Benutzer

#### <a name="run-at-lower-cost"></a>Ausführung bei niedrigeren Kosten

- Computekosten pro Workload, z. B. die Anzahl Computestunden × Kosten pro Stunde für Folgendes:
  - Standardberichterstellung
  - Ad-hoc-Abfragen
  - ETL-Batchverarbeitung
- Speicherkosten (Staging, Produktionstabellen, Indizes, temporärer Speicherplatz)

#### <a name="operate-with-better-availability-and-service-levels"></a>Betrieb mit höherer Verfügbarkeit und bessere Servicelevel

- Vereinbarungen zum Servicelevel (SLAs)
- Hochverfügbarkeit

#### <a name="improve-productively"></a>Gesteigerte Produktivität

- Automatisierte Aufgaben, reduzierte Mitarbeiterzahl

Eine erfolgreiche Data-Warehouse-Migration kann deshalb als ein Data Warehouse interpretiert werden, dass so schnell wie oder sogar schneller und zu niedrigeren Kosten als das alte System ausgeführt werden kann, aus dem Sie migrieren. Wenn Zielen Besitzer zugewiesen werden, können damit Zuständigkeiten für das Erreichen der entsprechenden Ziele geschaffen werden. So wird auch sichergestellt, dass Tests im Rahmen eines Proof-of-Concept-Labs (wie es im Bereich zur Risikominimierung in diesem Artikel definiert wird) als erfolgreich gelten können, wenn über die Tests Möglichkeiten ermittelt werden können, wie die Ziele erreicht werden können.

### <a name="migration-approach"></a>Migrationsansatz

Für das Migrieren Ihres vorhandenen Data Warehouse zu Azure Synapse stehen Ihnen mehrere strategische Optionen zur Verfügung:

- Führen Sie ein Lift & Shift für Ihr vorhandenes Data Warehouse aus, ohne Änderungen vorzunehmen.
- Vereinfachen Sie Ihr vorhandenes Data Warehouse, und migrieren Sie es dann.
- Entwerfen Sie Ihr Data Warehouse in Azure Synapse vollständig neu, und migrieren Sie Ihre Daten.

Die Ergebnisse der Bewertung Ihres vorhandenen Data Warehouse sollten Ihre Strategie maßgeblich beeinflussen. Bei einem positiven Bewertungsergebnis würde sich gegebenenfalls eine Lift & Shift-Strategie eignen. Ein mittelmäßiges Ergebnis aufgrund einer schlechteren Bewertung der Agilität könnte darauf hinweisen, dass vor der Migration Vereinfachungen durchgeführt werden sollten. Ein schlechtes Ergebnis weist am ehesten darauf hin, dass ein vollständiger neuer Entwurf erforderlich ist.

Bei einem Lift & Shift-Ansatz wird Ihre Architektur unverändert übernommen, während versucht wird, die Arbeit durch Verschieben Ihres vorhandenen Systems zu minimieren. Wenn Ihr vorhandenes ETL-Tool Azure Synapse bereits unterstützt, können Sie das Ziel möglicherweise mit minimalem Einsatz ändern. Nichtsdestotrotz bestehen Unterschiede, z. B. bei den Tabellentypen, Datentypen, SQL-Funktionen, Ansichten und der Geschäftslogik für gespeicherte Prozeduren. Diese Unterschiede und Umgehungsmöglichkeiten dafür finden Sie in anderen Artikeln dieser Reihe zur Migration.

Eine Vereinfachung Ihres vorhandenen Data Warehouse vor der Migration kann die Komplexität einer Migration verringern. Dies kann Folgendes umfassen:

- Entfernen oder Archivieren nicht verwendeter Tabellen vor der Migration, um eine Migration nicht verwendeter Daten zu vermeiden.
- Konvertieren physischer Data Marts in virtuelle Data Marts mithilfe von Datenvirtualisierungssoftware, um den Migrationsumfang zu verringern. Diese Konvertierung verbessert auch die Agilität und senkt die Gesamtkosten und kann als Modernisierung während der Migration angesehen werden.

Sie können auch zuerst Vereinfachungen vornehmen und das Data Warehouse dann im vereinfachten Zustand per Lift & Shift verschieben.

### <a name="migration-scope"></a>Migrationsumfang

Unabhängig davon, welche Strategie Sie auswählen, sollten Sie eindeutig den Migrationsumfang definieren, und herausarbeiten, was genau migriert wird und ob inkrementell oder gleich vollständig migriert werden soll. Ein Beispiel für eine inkrementelle Migration ist, dass Sie zunächst Ihre Data Marts migrieren und dann Ihr Data Warehouse. Mithilfe dieses Ansatzes können Sie den Fokus auf die Geschäftsbereiche mit hoher Priorität legen und es Ihrem Team dabei ermöglichen, inkrementell Erfahrung zu sammeln, da die einzelnen Marts einzeln migriert werden, bevor dann das Data Warehouse selbst migriert wird.

### <a name="defining-what-has-to-be-migrated"></a>Definition des zu migrierenden Inhalts

Erstellen Sie ein Inventar aller Inhalte, die migriert werden sollen. Dazu gehören Schemas, Daten, ETL-Prozesse (Pipelines), Autorisierungsberechtigungen, Benutzer, semantische Zugriffsebenen des BI-Tools und analytische Anwendungen. Detaillierte Informationen dazu, wie ein Inventar migriert wird, finden Sie in den Artikeln zur Migration unten in dieser Reihe. Entsprechende Links finden Sie unten.

- Überlegungen zur Schemamigration, zum Design und zur Leistung
- Datenmigration, ETL-Verarbeitung und Ladevorgänge
- Zugriffssicherheit und Data-Warehouse-Vorgänge
- Migration von Visualisierungen und Berichten
- Minimieren der Auswirkungen von SQL-Problemen
- Tools von Drittanbietern als Unterstützung für die Data-Warehouse-Migration

Wenn Sie unsicher sind, welcher Ansatz am besten für Sie geeignet ist, führen Sie Tests in einem Proof-of-Concept-Lab durch, um die für Sie am besten geeigneten Methoden zu identifizieren. Weitere Informationen finden Sie im Abschnitt zur Risikominimierung für Ihr Data-Warehouse-Migrationsprojekt.

### <a name="migration-control"></a>Migrationssteuerung

Zur Data-Warehouse-Migration zu Azure Synapse gehören Aufgaben, die durchgeführt werden müssen:

- Lokale Aufgaben, z. B. Datenexport
- Aufgaben im Netzwerk, z. B. Datenübertragungen
- Aufgaben in der Azure-Cloud, z. B. Transformation, Integration und Laden von Daten

Das Problem dabei ist, dass die Verwaltung dieser Aufgaben kompliziert werden kann, wenn Skripts und Hilfsprogramme entwickelt, getestet und unabhängig voneinander sowohl lokal als auch in Azure-Umgebungen ausgeführt werden. Dies führt insbesondere dann zu zusätzlicher Komplexität, wenn Versionskontrolle, Testverwaltung und Migrationsausführung nicht koordiniert werden.

Sie sollten diese Komplexität vermeiden und sie über eine zentrale Stelle steuern, z. B. über ein Quellcodeverwaltungsrepository, um Änderungen von der Entwicklung bis hin zu Tests und in der Produktion zu verwalten. Zur Migrationsausführung gehören Aufgaben, die lokal, im Netzwerk und in Azure ausgeführt werden müssen. Da Azure Synapse die Zielumgebung ist, vereinfacht das Steuern der Migrationsausführung in Azure die Verwaltung. Verwenden Sie Azure Data Factory (ADF), um eine Pipeline für die Migrationssteuerung zu erstellen, mit der Sie die Ausführung sowohl lokal als auch in Azure steuern können. Dies führt zu Automatisierung und senkt die Fehleranfälligkeit. ADF kann als Tool für die Migrationsorchestrierung verwendet werden, nicht nur als Tool für die Datenintegration auf Unternehmensebene.

Weitere Möglichkeiten, die von Microsoft-Partnern über Azure angeboten werden, mit denen die Migration gesteuert werden kann, sind Tools für die Data-Warehouse-Automatisierung, mit denen die Migration automatisiert werden kann. Anbieter wie WhereScape und Attunity sind Beispiele hierfür. Die meisten dieser Automatisierungstools basieren auf einem Lift & Shift-Migrationsansatz. Auch dann kann es aber Szenarios geben, die von solchen Tools nicht unterstützt werden, z. B. gespeicherte Prozeduren. Diese Produkte sowie einige andere finden Sie in einem eigenen Leitfaden, in dem der Fokus auf Tools von Drittanbietern liegt, die Sie bei der Migration zu Azure Synapse unterstützen.

### <a name="migration-testing"></a>Migrationstests

Als ersten Schritt für Tests müssen Sie mehrere Tests definieren sowie mehrere erforderliche Ergebnisse für die einzelnen Tests, die ausgeführt werden müssen, um das Projekt auf seinen Erfolg hin zu überprüfen bzw. diesen zu bestätigen. Es ist wichtig, dafür zu sorgen, dass alle Aspekte Ihrer vorhanden und migrierten Systeme getestet und miteinander verglichen werden. Dazu gehört auch Folgendes:

- Schema
- Wurden Datentypen konvertiert, wo dies erforderlich war?
- Verwenden Sie ein benutzerdefiniertes Schema in Azure Synapse, um zwischen Data-Warehouse- und Data-Mart-Tabellen zu unterscheiden.
- Benutzer
- Rollen und Benutzerzuweisungen zu diesen Rollen
- Sicherheitsberechtigungen für den Datenzugriff
- Datenschutz und Compliance
- Berechtigungen, die Verwaltungsfunktionen steuern
- Datenqualität und -integrität
- ETL-Verarbeitung, die Azure Synapse sowohl im Data Warehouse als auch aus dem Data Warehouse bis zu jeglichen Data Marts auffüllt, einschließlich Tests
- Alle Datensätze in allen Tabellen sind einschließlich ihres Verlaufs korrekt
- Verarbeitung sich langsam verändernder Dimensionen
- Change Data Capture-Verarbeitung
- Berechnungen und Aggregationen, die Funktionen verwenden, die sich von System zu System unterscheiden könnten
- Ergebnisse aller bekannten Abfragen, Berichte und Dashboards
- Leistung und Skalierbarkeit
- Analysefunktionen
- Kosten in der neuen Umgebung mit nutzungsbasierter Bezahlung

Weitestgehende Automatisierung der Tests; jeder Test sollte wiederholbar sein und einen konsistenten Ansatz für das Auswerten der Testergebnisse ermöglichen Wenn Berichte und Dashboards nicht konsistent sind, ist es sinnvoll, eine Möglichkeit zu haben, die Herkunft der Metadaten für alle ursprünglichen und migrierten Systeme während Migrationstests vergleichen zu können, da so Unterschiede hervorgehoben und gezeigt werden kann, wo genau diese bestehen, wenn sie beispielsweise nur schwierig zu erkennen sind.

Die beste sichere Möglichkeit dafür ist es, Rollen zu erstellen, Rollen Zugriffsrechte zuzuweisen und Benutzern dann Rollen zuzuweisen. Für den Zugriff auf Ihr neu migriertes Data Warehouse richten Sie einen automatisierten Prozess ein, um neue Benutzer zu erstellen und Rollen zuzuweisen. Das gleiche Vorgehen können Sie anwenden, um Benutzer aus Rollen zu entfernen.

Kommunizieren Sie eine solche Umstellung für alle Benutzer, damit sie darüber Bescheid wissen, was sich ändert und was zu erwarten ist.

## <a name="de-risking-your-data-warehouse-migration-project"></a>Risikominimierung für Ihr Data-Warehouse-Migrationsprojekt

Ein weiterer entscheidender Faktor für eine Data-Warehouse-Migration ist es, mögliche Risiken für das Projekt zu minimieren, um die Wahrscheinlichkeit eines Erfolgs zu maximieren. Zu diesem Zweck können verschiedene Schritte durchgeführt werden. Dazu gehören:

- Implementieren Sie ein Proof-of-Concept-Lab, damit Ihr Team Dinge testen kann, Tests durchführen kann, Probleme besser verstehen und mögliche Lösungen und Optimierungen finden kann, die dabei helfen, Migrationsansätze zu überprüfen, die Leistung zu verbessern und die Kosten zu senken. So können außerdem Möglichkeiten geschaffen werden, um Aufgaben zu automatisieren, integrierte Tools zu verwenden und Vorlagen zu erstellen, mit denen von Best Practices profitiert werden kann. Außerdem erhalten Sie so den Überblick über Ihre Erfahrungen und daraus abgeleitete Erkenntnisse. Dabei handelt es sich um eine besonders hilfreiche Methode, Risiken zu minimieren und die Erfolgschancen zu erhöhen. Außerdem können Sie Tests Benutzern zuweisen, die dann dafür verantwortlich sind, Migrationsziele zu erreichen, die in Ihrer Migrationsstrategie festgehalten sind.
- Führen Sie Optionen für die Datenvirtualisierung zwischen BI-Tools, Ihrem Data Warehouse und Data Marts ein. Sorgen Sie mithilfe von Datenvirtualisierung für Transparenz für Benutzer, um Risiken bei der Migration eines Data Warehouse zu minimieren, und blenden Sie die Migration selbst für Benutzer mithilfe von BI-Tools für die Datenvirtualisierung aus, wie es auf der folgenden Abbildung dargestellt ist.

![Abbildung einer Data-Warehouse-Migration](../_images/data-warehouse-migration.png)

Der Zweck hiervon besteht darin, die Abhängigkeit zwischen Benutzern im Unternehmen, die Self-Service-BI-Tools nutzen, und dem physischen Schema des zugrunde liegenden Data Warehouse und der zugrunde liegenden Data Marts aufzuheben, die migriert werden sollen. Durch Einführung der Datenvirtualisierung können sämtliche Änderungen an Schemas, die während der Data-Warehouse- und Data-Mart-Migration zu Azure Synapse vorgenommen wurden (z. B. Leistungsverbesserungen), für Benutzer im Unternehmen ausgeblendet werden, da diese nur auf virtuelle Tabellen auf der Virtualisierungsebene der Daten zugreifen. Wenn strukturelle Änderungen erforderlich sind, müssen so nur die Zuordnungen zwischen dem Data Warehouse oder Data Marts und entsprechenden virtuellen Tabellen geändert werden, sodass diese Änderungen und die Migration selbst für Benutzer gar nicht auffällt.

- Vorhandene Tabellen, die nie genutzt wurden, sollten Sie vor der Data-Warehouse-Migration archivieren, da es wenig Sinn ergibt, nicht verwendete Tabellen zu migrieren. Eine Möglichkeit dafür ist es, die ungenutzten Daten in Azure Blob Storage oder Azure Data Lake zu archivieren und externe Tabellen in Azure Synapse zu erstellen, damit die Daten weiterhin online sind.
- Ziehen Sie die Möglichkeit in Betracht, eine VM in Azure mit einer Entwicklungsversion (die in der Regel kostenfrei ist) des vorhandenen Legacy-Datenbank-Managementsystems für das Data Warehouse einzuführen, das auf dieser VM ausgeführt wird. So können Sie vorhandene Data-Warehouse-Schemas schnell auf die VM verschieben. Von dort können sie dann zu Azure Synapse verschoben werden. Dies lässt sich vollständig in der Azure-Cloud umsetzen.
- Definieren Sie eine Reihenfolge und Abhängigkeiten für die Migration.
- Sorgen Sie dafür, dass Ihr Infrastruktur- und Betriebsteam auf die Migration Ihrer Daten in das Migrationsprojekt so frühzeitig wie möglich vorbereitet ist.
- Identifizieren Sie Unterschiede bei der Funktionalität des Datenbank-Managementsystems sowie Stellen, an denen die proprietäre Geschäftslogik zu einem Problem werden könnte. Es ist beispielsweise unwahrscheinlich, dass die Verwendung gespeicherter Prozeduren für die ETL-Verarbeitung einfach migriert werden kann. Dabei wird auch keine Metadatenherkunft enthalten sein, da Transformationen im Code eingebunden sind.
- Ziehen Sie eine Strategie in Betracht, bei der Data Marts zuerst und dann das Data Warehouse migriert wird, das die Quelle der Data Marts darstellt. Der Grund dafür liegt darin, dass so eine inkrementelle Migration ermöglicht werden kann. Die Migration kann so besser verwaltet werden, und es ist möglich, die Migration basierend auf Geschäftsanforderungen zu priorisieren.
- Ziehen Sie die Möglichkeit der Verwendung der Datenvirtualisierung in Betracht, um Ihre aktuelle Data-Warehouse-Architektur vor der Migration zu vereinfachen, z. B. indem Sie Data Marts durch virtuelle Data Marts ersetzen, damit Sie physische Datenspeicher und ETL-Aufträge für Data Marts entfernen können, ohne Funktionalität vor der Migration zu verlieren. Dadurch könnten Sie die Anzahl der Datenspeicher reduzieren, die migriert werden sollen, die Anzahl der Datenkopien reduzieren, die Gesamtkosten minimieren und die Agilität erhöhen. Dafür müssen Sie vor der Migration Ihres Data Warehouse von physischen zu virtuellen Data Marts wechseln. In gewisser Weise könnten Sie dies als einen Schritt zur Modernisierung des Data Warehouse vor der Migration sehen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Data-Warehouse-Migrationen erhalten Sie in einem virtuellen [Workshop zur Cloud-Data-Warehouse-Modernisierung in Azure](https://now.informatica.com/Microsoft_CDW_Workshops.html) von Informatica.
