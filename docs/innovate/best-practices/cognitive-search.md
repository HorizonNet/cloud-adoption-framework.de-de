---
title: Was ist Azure Cognitive Search?
description: Azure Cognitive Search (früher „Azure Search“) ermöglicht Ihnen das Anwenden von KI-Prozessen während der Indizierung.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a5221713e9e6125aa134e958b2baca2e99dcadec
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884537"
---
<!-- cSpell:ignore Lucene -->

<!-- docsTest:casing "JFK Files" -->
<!-- docsTest:ignore "Azure Search" -->

# <a name="what-is-azure-cognitive-search"></a>Was ist Azure Cognitive Search?

Azure Cognitive Search (früher „Azure Search“) ist eine verwaltete Cloudlösung, die Entwicklern APIs und Tools zum Hinzufügen von umfangreichen Suchfunktionen für private, heterogene Inhalte in Web- und Unternehmensanwendungen sowie in mobilen Anwendungen bietet. Ihr Code oder ein Tool ruft die Datenerfassung (Indizierung) auf, um einen Index zu erstellen und zu laden. Optional können Sie kognitive Qualifikationen zum Anwenden von KI-Prozessen während der Indizierung hinzufügen. Dadurch können neue Informationen und Strukturen hinzugefügt werden, die nützlich für die Suche und andere Szenarios sind.

Auf der anderen Seite des Diensts gibt Ihr Anwendungscode Abfrageanforderungen aus und verarbeitet Antworten. Das Suchverhalten ist mit Funktionen aus Azure Cognitive Search in Ihrem Client definiert, und Abfragen werden in einem permanenten Index ausgeführt, den Sie erstellen, besitzen und in Ihrem Dienst speichern.

![Abbildung von Azure Cognitive Search](../../_images/ai-cognitive-search.png)

Die Funktionalität wird über eine einfache [REST-API](/rest/api/searchservice/) oder ein [.NET SDK](/azure/search/search-howto-dotnet-sdk) bereitgestellt, sodass die inhärente Komplexität des Informationsabrufs verborgen bleibt. Zusätzlich zu den APIs bietet das Azure-Portal mit Tools für die Prototyperstellung und Indexabfrage Unterstützung für Administration und Inhaltsverwaltung. Da der Dienst in der Cloud ausgeführt wird, werden die Infrastruktur und Verfügbarkeit von Microsoft verwaltet.

## <a name="when-to-use-azure-cognitive-search"></a>Einsatzgebiete von Azure Cognitive Search

Azure Cognitive Search eignet sich sehr gut für die folgenden Anwendungsszenarien:

- Konsolidierung von heterogenen Inhaltstypen in einem einzelnen privaten, durchsuchbaren Index. Abfragen werden immer für einen Index ausgeführt, den Sie erstellen und zusammen mit Dokumenten laden. Der Index befindet sich immer in der Cloud in Ihrer Azure Cognitive Search-Instanz. Sie können einen Index mit Streams aus JSON-Dokumenten aus jeder beliebigen Quelle und von jeder beliebigen Plattform auffüllen. Bei Inhalten, die aus Azure stammen, können Sie alternativ dazu einen Indexer verwenden, um Daten per Pull in einen Index abzurufen. Die Definition sowie die Verwaltung bzw. der Besitz eines Index sind die Hauptgründe für die Verwendung von Azure Cognitive Search.
- Bei unformatiertem Inhalt handelt es sich um große Mengen von undifferenziertem Text oder um Bild- und Anwendungsdateien, etwa Microsoft Office-Inhaltstypen in einer Azure-Datenquelle wie Azure Blob Storage oder Azure Cosmos DB. Sie können während der Indizierung kognitive Qualifikationen anwenden, um Struktur hinzuzufügen oder aussagekräftige Informationen aus Image- und Anwendungsdateien zu gewinnen.
- Einfache Implementierung von Features in Zusammenhang mit der Suche. Azure Cognitive Search-APIs vereinfachen Abfrageerstellung, Facettennavigation, Filter (einschließlich geografisch-räumlicher Suche), Synonymzuordnung, Abfragen mit automatischer Vervollständigung sowie die Optimierung der Relevanz. Mithilfe von integrierten Features können Sie die Erwartungen von Endbenutzern an einen Suchdienst erfüllen, der der Funktionalität von kommerziellen Suchmaschinen in nichts nachsteht.
- Indizieren unstrukturierter Texte oder Extrahieren von Text und anderen Informationen aus Bilddateien. Das Feature für die [KI-Anreicherung](/azure/search/cognitive-search-concept-intro) von Azure Cognitive Search ergänzt die Indizierungspipeline um die Verarbeitung von KI-Funktionen. Einige häufige Anwendungsfälle: OCR in gescannten Dokumenten, Erkennen von Entitäten und Extrahieren von Schlüsselbegriffen in großen Dokumenten, Spracherkennung und Textübersetzung sowie Stimmungsanalyse.
- Erfüllen von linguistischen Anforderungen dank der benutzerdefinierten Sprachanalysefunktionen von Azure Cognitive Search. Bei nicht englischsprachigen Inhalten unterstützt Azure Cognitive Search sowohl Lucene-Analysetools als auch die Microsoft-Prozessoren für die Verarbeitung natürlicher Sprache. Sie können Analysetools auch so konfigurieren, dass Rohdaten einer speziellen Verarbeitung unterzogen werden, um z.B. diakritische Zeichen herauszufiltern.

## <a name="use-azure-cognitive-search"></a>Verwenden von Azure Cognitive Search

### <a name="step-1-provision-the-service"></a>Schritt 1: Bereitstellen des Diensts

Eine Azure Cognitive Search-Instanz können Sie entweder über das [Azure-Portal](https://portal.azure.com/) oder die [Azure Resource Manager-REST-API](/rest/api/searchmanagement/) bereitstellen. Sie können entweder den gemeinsam mit anderen Abonnenten genutzten kostenlosen Dienst auswählen oder eine kostenpflichtige Ebene, die Ressourcen zur ausschließlichen Nutzung für Ihren Dienst reserviert. Für kostenpflichtige Ebenen können Sie einen Dienst in zwei Dimensionen skalieren:

- Fügen Sie Replikate hinzu, um Ihre Kapazität für ein hohes Abfrageaufkommen zu erhöhen.
- Fügen Sie Partitionen hinzu, um den Speicher für weitere Dokumente zu vergrößern.

Durch getrenntes Verarbeiten von Dokumentspeicherung und Abfragedurchsatz können Sie Ressourcen auf Produktionsanforderungen basierend kalibrieren.

### <a name="step-2-create-an-index"></a>Schritt 2: Erstellen eines Index

Bevor Sie durchsuchbaren Inhalt hochladen können, müssen Sie einen Azure Cognitive Search-Index definieren. Einen Index können Sie sich wie eine Datenbanktabelle vorstellen, die Ihre Daten enthält und Suchabfragen entgegennimmt. Sie definieren das zuzuordnende Indexschema, um die Struktur der Dokumente widerzuspiegeln, die Sie durchsuchen möchten (ähnlich wie bei Feldern in einer Datenbank).

Ein Schema kann im Azure-Portal oder programmgesteuert mithilfe des [.NET SDK](/azure/search/search-howto-dotnet-sdk) oder der [REST-API](/rest/api/searchservice/) erstellt werden.

### <a name="step-3-load-data"></a>Schritt 3: Laden der Daten

Nachdem Sie einen Index definiert haben, können Sie Inhalte hochladen. Sie können entweder ein Push- oder Pullmodell verwenden.

Das Pullmodell ruft Daten aus externen Datenquellen ab. Es wird durch Indexer unterstützt, die Aspekte der Datenerfassung optimieren und automatisieren, z. B. das Herstellen einer Verbindung mit Daten, Lesen und Serialisieren von Daten. [Indexer](/rest/api/searchservice/Indexer-operations) stehen für Azure Cosmos DB, Azure SQL-Datenbank, Azure Blob Storage und in einer auf einer Microsoft Azure Virtual Machines-Instanz gehosteten SQL Server-Instanz zur Verfügung. Sie können einen Indexer für bedarfsgesteuerte oder geplante Datenaktualisierung konfigurieren.

Das Pushmodell wird über das SDK oder die REST-APIs bereitgestellt, die zum Senden von aktualisierten Dokumenten an einen Index verwendet werden. Sie können Daten aus praktisch jedem Dataset im JSON-Format übertragen. Weitere Informationen zum Laden von Daten finden Sie unter [Hinzufügen, Aktualisieren oder Löschen von Dokumenten](/rest/api/searchservice/addupdate-or-delete-documents) und [Verwenden des .NET SDK](/azure/search/search-howto-dotnet-sdk).

### <a name="step-4-search"></a>Schritt 4: Suchen,

Nach dem Füllen eines Indexes können Sie über einfache HTTP-Anforderungen mit [REST-APIs](/rest/api/searchservice/search-documents) oder dem [.NET-SDK](/dotnet/api/microsoft.azure.search.idocumentsoperations?view=azure-dotnet) [Suchabfragen](/azure/search/search-query-overview) an Ihren Dienstendpunkt richten. Führen Sie die Schritte zum [Erstellen Ihrer ersten Suchanwendung](/azure/search/tutorial-csharp-create-first-app) aus, um eine Webseite zu erstellen und anschließend zu erweitern, die Benutzereingaben sammelt und Ergebnisse verarbeitet. Sie können auch [Postman für interaktive REST-Aufrufe](/azure/search/search-get-started-postman) oder den integrierten [Suchexplorer](/azure/search/search-explorer) im Azure-Portal verwenden, um einen vorhandenen Index abzufragen.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zu [Azure Cognitive Search](/azure/search/)
- Weitere [KI-Architekturen](/azure/architecture/browse/)
- Im Artikel [KI-Anreicherung mit Azure Cognitive Search](/azure/architecture/solution-ideas/articles/cognitive-search-with-skillsets) finden Sie ein Beispiel für eine Knowledge-Mining-Lösung.
