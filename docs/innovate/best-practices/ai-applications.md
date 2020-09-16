---
title: Was sind KI-Anwendungen?
description: Hier erfahren Sie, wie Sie mit Azure Cognitive Services KI-Funktionen und -Innovationen in Ihre Anwendungen integrieren können.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3d799dd4d5d1821a8d914ad5ad4daae631d65df6
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89604615"
---
# <a name="what-are-ai-applications"></a>Was sind KI-Anwendungen?

In Azure können Sie schneller intelligente Anwendungen mithilfe von Tools und Technologien Ihrer Wahl und integrierter KI entwickeln.

- **Unkompliziertes Erstellen und Bereitstellen an jedem Ort:** Nutzen Sie die Fähigkeiten Ihres Teams und bereits bekannte Tools, um intelligente Anwendungen zu entwickeln und ohne Codeänderungen bereitzustellen. Sie können diese Anwendungen ein einziges Mal erstellen und dann in der Cloud, lokal und auf Edgegeräten bereitstellen. Sie können sich auf eine globale Verteilung auf mehr Rechenzentren verlassen als bei jedem anderen Anbieter.
- **Verwenden einer offenen Plattform, um etwas zu bewirken:** Verwenden Sie Ihre bevorzugten Technologien – einschließlich Open Source. Azure unterstützt eine Reihe von Bereitstellungsoptionen, beliebten Stapeln und Sprachen sowie eine umfangreiche Sammlung von Daten-Engines. Machen Sie sich diese Flexibilität sowie die Leistung, Skalierbarkeit und Sicherheit von Microsoft-Technologien zunutze, um Anwendungen für jedes beliebige Szenario zu entwickeln.
- **Entwickeln von Anwendungen mit integrierter Intelligenz:** Mit Azure können Sie problemlos intelligente Anwendungen erstellen, da nur diese Plattform Analysen und native KI für Ihre Daten bietet – unabhängig davon, wo sich diese befinden oder welche Sprache Sie verwenden. Sie können viele verschiedene [kognitive APIs](https://azure.microsoft.com/services/cognitive-services/) nutzen, um ganz einfach neue Komponenten in Ihre Anwendungen zu integrieren, um menschenähnliche Intelligenz zu erzielen.

## <a name="what-is-azure-cognitive-services"></a>Was ist Azure Cognitive Services?

Azure Cognitive Services kann durch ein paar wenige Codezeilen das Integrieren von KI-Funktionen und -Innovationen in Anwendungen vereinfachen. Azure Cognitive Services unterstützt Sie beim Entwickeln von Anwendungen, die im Zusammenhang mit Ihren Geschäftsprozessen sehen, hören, sprechen, verstehen und sogar Schlussfolgerungen ziehen können. Cognitive Services bietet benutzerfreundliche KI, die sich problemlos in Ihre Anwendungen integrieren lässt.

Es handelt sich dabei um APIs, SDKs und Dienste, die Entwicklern beim Erstellen intelligenter Anwendungen helfen, ohne dass direkte Fertigkeiten oder Kenntnisse in den Bereichen KI oder Data Science erforderlich sind. Mit Cognitive Services können Entwickler ganz einfach kognitive Features in ihre Anwendungen integrieren. Die dort verfügbaren Dienste können in fünf Hauptkategorien unterteilt werden: Sehen, Sprechen, Sprache, Websuche und Entscheidungsfindung.

### <a name="vision-apis"></a>Bildanalyse-APIs

| Dienstname | Dienstbeschreibung |
| --- | --- |
| [Maschinelles Sehen](/azure/cognitive-services/computer-vision/) | Über die Maschinelles Sehen-API haben Sie Zugriff auf erweiterte Algorithmen für die Bildverarbeitung und die Rückgabe von Informationen. |
| [Custom Vision](/azure/cognitive-services/custom-vision-service/home) | Mit Custom Vision können Sie benutzerdefinierte Bildklassifizierungen entwickeln. |
| [Gesichtserkennung](/azure/cognitive-services/face/) | Der Gesichtserkennungsdienst ermöglicht den Zugriff auf erweiterte Gesichtserkennungsalgorithmen, die Gesichtsmerkmale erkennen. |
| [Formularerkennung](/azure/cognitive-services/form-recognizer/) (Vorschauversion) | Die Formularerkennung identifiziert und extrahiert Schlüssel-Wert-Paare und Tabellendaten aus Formulardokumenten. Anschließend werden strukturierte Daten ausgegeben, die die Beziehungen in der Originaldatei enthalten. |
| [Freihanderkennung](/azure/cognitive-services/ink-recognizer/) (Vorschauversion) | Die Freihanderkennung ermöglicht das Erkennen und Analysieren von Strichdaten, Formen und handschriftlichen Inhalten aus Freihandeingaben sowie die Ausgabe einer Dokumentstruktur mit allen erkannten Entitäten. |
| [Video Indexer](/azure/cognitive-services/video-indexer/video-indexer-overview) | Video Indexer ermöglicht es Ihnen, Erkenntnisse aus Ihren Videos zu extrahieren. |

### <a name="speech-apis"></a>Spracherkennungs-APIs

| Dienstname | Dienstbeschreibung |
| --- | --- |
| [Spracheingabe](/azure/cognitive-services/speech-service/) | Der Spracherkennungsdienst erweitert Anwendungen um sprachaktivierte Features. |
| [Sprechererkennung](/azure/cognitive-services/speaker-recognition/home "Sprechererkennungs-API") (Vorschauversion) | Die Sprechererkennungs-API stellt Algorithmen zur Sprecheridentifikation und -verifizierung zur Verfügung. |
| [Bing-Spracheingabe](/azure/cognitive-services/speech/home) (wird eingestellt) | Die Bing-Spracheingabe-API bietet Ihnen eine einfache Möglichkeit, sprachaktivierte Features in Ihren Anwendungen zu erstellen. |
| [Sprachübersetzung](/azure/cognitive-services/translator-speech/) (wird eingestellt) | Die Sprachübersetzung ist ein Dienst für maschinelle Übersetzungen. |

### <a name="language-apis"></a>Sprache-APIs

| Dienstname | Dienstbeschreibung |
|--|--|
| [Language Understanding (LUIS)](/azure/cognitive-services/luis/) | Mit dem LUIS-Dienst (Language Understanding) kann Ihre Anwendung frei formulierte Anliegen von Personen verstehen. |
| [QnA Maker](/azure/cognitive-services/qnamaker/index "QnA Maker") | Der QnA Maker ermöglicht es Ihnen, aus Ihren teilstrukturierten Inhalten einen Frage- und Antwortdienst zu erstellen. |
| [Textanalyse](/azure/cognitive-services/text-analytics/) | Die Textanalyse bietet die Verarbeitung von natürlicher Sprache für unformatierten Text für die Standpunktanalyse, die Schlüsselbegriffserkennung und die Sprachenerkennung. |
| [Translator](/azure/cognitive-services/translator/) | Translator ermöglicht eine maschinelle Textübersetzung nahezu in Echtzeit. |

### <a name="decision-apis"></a>Entscheidungs-APIs

| Dienstname | Dienstbeschreibung |
| --- | --- |
| [Anomalieerkennung](/azure/cognitive-services/anomaly-detector/) (Vorschauversion) | Die Anomalieerkennung bietet Ihnen die Möglichkeit, Abweichungen in Ihren Zeitreihendaten zu überwachen und zu erkennen. |
| [Content Moderator](/azure/cognitive-services/content-moderator/overview "Content Moderator") | Der Content Moderator bietet die Überwachung auf möglicherweise anstößige, unerwünschte und risikobehaftete Inhalte. |
| [Personalisierung](/azure/cognitive-services/personalizer/) | Die Personalisierung ermöglicht es Ihnen, Informationen über das Echtzeitverhalten von Benutzern zu erhalten, um die am besten geeignete Darstellung auszuwählen. |

### <a name="supported-cultural-languages"></a>Unterstützte Kultursprachen

Cognitive Services unterstützt eine Vielzahl von Kultursprachen auf Dienstebene. Sie finden die Sprachenverfügbarkeit für jede API in der [Liste unterstützter Sprachen](/azure/cognitive-services/language-support).

### <a name="secure-resources"></a>Sichere Ressourcen

Cognitive Services bietet ein mehrschichtiges Sicherheitsmodell – einschließlich [Authentifizierung](/azure/cognitive-services/authentication) über Azure Active Directory-Anmeldeinformationen, einem gültigem Ressourcenschlüssel und [Azure Virtual Network](/azure/cognitive-services/cognitive-services-virtual-networks).

### <a name="container-support"></a>Containerunterstützung

Cognitive Services stellt Container für die Bereitstellung in der Cloud oder lokal bereit. Weitere Informationen zu Cognitive Services-Containern finden Sie [hier](/azure/cognitive-services/cognitive-services-container-support).

<!-- docutune:casing "HIPAA BAA" "CSA STAR" -->

### <a name="certifications-and-compliance"></a>Zertifizierungen und Compliance

Cognitive Services hat Zertifizierungen wie die CSA STAR-Zertifizierung, FedRAMP Moderate und HIPAA BAA erhalten.

Sie können Zertifizierungen für eigene Überwachungen und Sicherheitsüberprüfungen [herunterladen](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942).

Informationen zum Datenschutz und zur Datenverwaltung finden Sie im [Microsoft Trust Center](https://servicetrust.microsoft.com/).

## <a name="how-are-cognitive-services-and-azure-machine-learning-similar"></a>Inwiefern ähneln sich Cognitive Services und Azure Machine Learning?

Cognitive Services und Azure Machine Learning haben beide das Ziel, KI zur Verbesserung des Geschäftsbetriebs zu nutzen. In den jeweiligen Angeboten wird diese Funktion jedoch unterschiedlich bereitgestellt. Im Grundsatz sind die Zielgruppen unterschiedlich:

- Cognitive Services ist für Entwickler gedacht, die über keine Erfahrung im Bereich maschinelles Lernen verfügen.
- Machine Learning ist auf die Bedürfnisse von Data Scientists zugeschnitten.

## <a name="how-is-a-cognitive-service-different-from-machine-learning"></a>Inwiefern unterscheidet sich ein Cognitive Service von maschinellem Lernen?

Ein Cognitive Service stellt ein trainiertes Modell bereit. Dieses Modell verknüpft die Daten mit einem Algorithmus und ist über eine REST-API oder ein SDK verfügbar. Abhängig von Ihrem Szenario können Sie diesen Dienst innerhalb weniger Minuten implementieren. Ein Cognitive Service liefert Antworten für allgemeine Probleme, etwa Schlüsselwörter in Texten oder Elementerkennung in Bildern.

Machine Learning ist ein Prozess, für dessen erfolgreiche Implementierung üblicherweise ein längerer Zeitraum erforderlich ist. Diese Zeit wird für Datensammlung, Bereinigung, Transformation, Algorithmusauswahl, Modelltraining und Bereitstellung aufgewendet, um die gleiche Funktionalität zu erreichen, die von einem Cognitive Service bereitgestellt wird. Mit maschinellem Lernen ist es möglich, Antworten auf hochspezialisierte oder spezifische Probleme bereitzustellen. Diese mit maschinellem Lernen zu lösenden Probleme erfordern Vertrautheit mit der spezifischen Thematik und den Daten des betreffenden Problems sowie ein entsprechendes Know-how.

## <a name="next-steps"></a>Nächste Schritte

- Informieren Sie sich ausführlicher über [Cognitive Services](/azure/cognitive-services/).
- Machen Sie sich mit [bewährten Methoden für KI-Architekturen](/azure/architecture/solution-ideas/articles/ai-at-the-edge) vertraut.
