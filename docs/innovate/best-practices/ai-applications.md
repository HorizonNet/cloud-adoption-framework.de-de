---
title: Was sind KI-Anwendungen?
description: Was ist Cognitive Search?
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: e632b5e460c4a5a100b63a45032b75fcebd971e6
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452603"
---
<!-- cSpell:ignore Personalizer -->

# <a name="what-are-ai-applications"></a>Was sind KI-Anwendungen?

In Azure können Sie schneller intelligente Anwendungen mit bereits integrierter KI erstellen und dabei die Tools und Technologien Ihrer Wahl verwenden.

- **Unkompliziertes Erstellen und Bereitstellen an jedem Ort:** Nutzen Sie die vorhandenen Fähigkeiten Ihres Teams sowie Ihre vertrauten und bevorzugten Tools, um intelligente Anwendungen zu erstellen und ohne Codeänderungen bereitzustellen. Einmal erstellte Anwendungen können anschließend überall bereitgestellt werden – sei es in der Cloud, lokal oder auf Edgegeräten. Dabei können Sie darauf vertrauen, dass sie weltweit in auf mehr Rechenzentren verteilt werden als bei jedem anderen Anbieter.

- **Verwenden einer offenen Plattform, um etwas zu bewirken:** Wählen Sie Ihre bevorzugten Technologien – einschließlich Open Source. Azure unterstützt eine Reihe von Bereitstellungsoptionen, beliebten Stapeln und Sprachen sowie eine umfangreiche Sammlung von Daten-Engines. Machen Sie sich diese Flexibilität sowie die Leistung, Skalierbarkeit und Sicherheit von Microsoft-Technologien zunutze, um Anwendungen für jedes beliebige Szenario zu entwickeln.

- **Entwickeln von Anwendungen mit integrierter Intelligenz:** Mit Azure können Sie problemlos intelligente Anwendungen erstellen, da nur diese Plattform Analysen und native KI für Ihre Daten bietet – unabhängig davon, wo sich diese befinden oder welche Sprache Sie verwenden. Nutzen Sie verschiedenste [kognitive APIs](https://azure.microsoft.com/services/cognitive-services/), um ganz einfach neue Erfahrungen in Ihre Anwendungen zu integrieren und menschenähnliche Intelligenz zu erzielen.

## <a name="what-are-azure-cognitive-services"></a>Was ist Azure Cognitive Services?

Azure Cognitive Services kann die Integration von KI in Ihre Anwendungen vereinfachen und die neuesten Durchbrüche in der KI nutzbar machen – alles mit ein paar einfachen Codezeilen. Die Lösung ermöglicht die Erstellung von Anwendungen, die sehen, hören, sprechen, verstehen und sogar zu vernünftigen Geschäftsprozessen beitragen können. Azure Cognitive Services bietet benutzerfreundliche KI, die sich problemlos in Ihre Anwendung integrieren lässt.

Azure Cognitive Services sind APIs, SDKs und Dienste, die Entwicklern beim Erstellen intelligenter Anwendungen helfen, ohne direkte KI- oder Data Science-Fähigkeiten oder -Kenntnisse zu haben. Mit Azure Cognitive Services können Entwickler ganz einfach kognitive Funktionen in ihre Anwendungen integrieren. Das Ziel von Azure Cognitive Services ist es, Entwicklern zu helfen, Anwendungen zu entwickeln, die sehen, hören, sprechen, verstehen und sogar schlussfolgern können. Der Katalog der Dienste innerhalb von Azure Cognitive Services kann in fünf Hauptkategorien unterteilt werden: Bildanalyse, Spracheingabe, Sprache, Websuche und Entscheidungen.

### <a name="vision-apis"></a>Bildanalyse-APIs

| Dienstname | Dienstbeschreibung |
| --- | --- |
| [Maschinelles Sehen](https://docs.microsoft.com/azure/cognitive-services/computer-vision/) | Über den Dienst für maschinelles Sehen haben Sie Zugriff auf erweiterte Algorithmen für die Bildverarbeitung und die Rückgabe von Informationen. |
| [Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home) | Mit dem Custom Vision-Dienst können Sie benutzerdefinierte Bildklassifizierungen erstellen. |
| [Gesichtserkennung](https://docs.microsoft.com/azure/cognitive-services/face/) | Der Gesichtserkennungsdienst ermöglicht den Zugriff auf erweiterte Algorithmen zur Gesichtserkennung, wodurch die Ermittlung von Gesichtsmerkmalen sowie die Gesichtserkennung ermöglicht wird. |
| [Formularerkennung](https://docs.microsoft.com/azure/cognitive-services/form-recognizer/) (Vorschauversion) | Die Formularerkennung identifiziert und extrahiert Schlüssel-Wert-Paare und Tabellendaten aus Formulardokumenten und gibt dann strukturierte Daten aus, die auch die Beziehungen in der ursprünglichen Datei umfassen. |
| [Freihanderkennung](https://docs.microsoft.com/azure/cognitive-services/ink-recognizer/) (Vorschauversion) | Die Freihanderkennung ermöglicht das Erkennen und Analysieren von Daten, Formen und handschriftlichen Inhalten aus Freihandeingaben sowie die Ausgabe einer Dokumentstruktur mit allen erkannten Entitäten. |
| [Video Indexer](https://docs.microsoft.com/azure/cognitive-services/video-indexer/video-indexer-overview) | Video Indexer ermöglicht es Ihnen, Erkenntnisse aus Ihren Videos zu extrahieren. |

### <a name="speech-apis"></a>Spracherkennungs-APIs

| Dienstname | Dienstbeschreibung |
| --- | --- |
| [Spracheingabe](https://docs.microsoft.com/azure/cognitive-services/speech-service/) | Der Spracherkennungsdienst erweitert Anwendungen um sprachaktivierte Features. |
| [Sprechererkennung](https://docs.microsoft.com/azure/cognitive-services/speaker-recognition/home "Sprechererkennungs-API") (Vorschauversion) | Die Sprechererkennungs-API stellt Algorithmen zur Sprecheridentifikation und -verifizierung zur Verfügung. |
| [Bing-Spracheingabe](https://docs.microsoft.com/azure/cognitive-services/speech/home) (wird eingestellt) | Die Bing-Spracheingabe-API bietet Ihnen eine einfache Möglichkeit, sprachaktivierte Features in Ihren Anwendungen zu erstellen. |
| [Sprachübersetzung](https://docs.microsoft.com/azure/cognitive-services/translator-speech/) (wird eingestellt) | Die Sprachübersetzung ist ein Dienst für maschinelle Übersetzungen. |

### <a name="language-apis"></a>Sprache-APIs

| Dienstname | Dienstbeschreibung |
| --- | -- |
| [Language Understanding (LUIS)](https://docs.microsoft.com/azure/cognitive-services/luis/) | Mit dem LUIS-Dienst (Language Understanding) kann Ihre Anwendung frei formulierte Anliegen von Personen verstehen. |
| [QnA Maker](https://docs.microsoft.com/azure/cognitive-services/qnamaker/index "QnA Maker") | QnA Maker ermöglicht es Ihnen, aus Ihren teilstrukturierten Inhalten einen Frage- und Antwortdienst zu erstellen. |
| [Textanalyse](https://docs.microsoft.com/azure/cognitive-services/text-analytics/) | Die Textanalyse bietet die Verarbeitung natürlicher Sprache für unformatierten Text für die Stimmungsanalyse, die Schlüsselbegriffserkennung und die Sprachenerkennung. |
| [Translator](https://docs.microsoft.com/azure/cognitive-services/translator/) | Translator ermöglicht eine maschinenbasierte Textübersetzung in Quasi-Echtzeit. |

### <a name="decision-apis"></a>Entscheidungs-APIs

| Dienstname | Dienstbeschreibung |
| --- | --- |
| [Anomalieerkennung](https://docs.microsoft.com/azure/cognitive-services/anomaly-detector/) (Vorschauversion) | Die Anomalieerkennung bietet Ihnen die Möglichkeit, Abweichungen in Ihren Zeitreihendaten zu überwachen und zu erkennen. |
| [Content Moderator](https://docs.microsoft.com/azure/cognitive-services/content-moderator/overview "Content Moderator") | Der Content Moderator bietet die Überwachung auf möglicherweise anstößige, unerwünschte und risikobehaftete Inhalte. |
| [Personalisierung](https://docs.microsoft.com/azure/cognitive-services/personalizer/) | Mit der Personalisierung können Sie die beste Benutzeroberfläche für Ihre Benutzer auswählen und dabei in Echtzeit von deren Verhalten lernen. |

### <a name="supported-cultural-languages"></a>Unterstützte Kultursprachen

Cognitive Services unterstützt eine Vielzahl von Kultursprachen auf Dienstebene. Sie finden die Sprachenverfügbarkeit für jede API in der [Liste unterstützter Sprachen](https://docs.microsoft.com/azure/cognitive-services/language-support).

### <a name="securing-resources"></a>Sichern von Ressourcen

Azure Cognitive Services bietet ein mehrschichtiges Sicherheitsmodell – einschließlich [Authentifizierung](https://docs.microsoft.com/azure/cognitive-services/authentication) per Azure Active Directory-Anmeldeinformationen, gültigem Ressourcenschlüssel und [Azure Virtual Network](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-virtual-networks).

### <a name="container-support"></a>Containerunterstützung

Cognitive Services stellt Container für die Bereitstellung in der Azure-Cloud oder lokal bereit. Weitere Informationen zu Cognitive Services-Containern finden Sie [hier](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-container-support).

<!-- docsTest:ignore "HIPAA BAA" "CSA STAR" -->

### <a name="certifications-and-compliance"></a>Zertifizierungen und Compliance

Cognitive Services hat Zertifizierungen wie die CSA STAR-Zertifizierung, FedRAMP Moderate und HIPAA BAA erhalten.

Sie können Zertifizierungen für eigene Überwachungen und Sicherheitsüberprüfungen [herunterladen](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942).

Informationen zum Datenschutz und zur Datenverwaltung finden Sie im [Microsoft Trust Center](https://servicetrust.microsoft.com/).

## <a name="how-are-cognitive-services-and-azure-machine-learning-similar"></a>Inwiefern ähneln sich Cognitive Services und Azure Machine Learning?

Beide haben zwar die Verbesserung des Geschäftsbetriebs durch den Einsatz von KI zum Ziel, unterscheiden sich jedoch bei der Bereitstellung in den jeweiligen Angeboten. Im Grundsatz sind die Zielgruppen unterschiedlich:

- Cognitive Services sind für Entwickler vorgesehen, die keine Machine Learning-Erfahrung haben.
- Azure Machine Learning ist auf Data Scientists zugeschnitten.

## <a name="how-is-a-cognitive-service-different-from-machine-learning"></a>Inwiefern unterscheidet sich ein Cognitive Service von maschinellem Lernen?

Ein Cognitive Service stellt ein trainiertes Modell bereit. Dabei werden Daten und ein Algorithmus miteinander verknüpft und über eine REST-API oder ein SDK verfügbar gemacht. Abhängig von Ihrem Szenario können Sie diesen Dienst innerhalb von Minuten implementieren. Ein Cognitive Service liefert Antworten für allgemeine Probleme, etwa Schlüsselwörter in Texten oder Elementerkennung in Bildern.

Machine Learning ist ein Prozess, für dessen erfolgreiche Implementierung üblicherweise ein längerer Zeitraum erforderlich ist. Diese Zeit wird für Datensammlung, Bereinigung, Transformation, Algorithmusauswahl, Modelltraining und Bereitstellung aufgewendet, um die gleiche Funktionalität zu erreichen, die von einem Cognitive Service bereitgestellt wird. Mit maschinellem Lernen ist es möglich, Antworten auf hochspezialisierte und/oder spezifische Probleme bereitzustellen. Diese mit maschinellem Lernen zu lösenden Probleme erfordern Vertrautheit mit der spezifischen Thematik und den Daten des betreffenden Problems sowie entsprechendes Know-how.

## <a name="next-steps"></a>Nächste Schritte

- Informieren Sie sich ausführlicher über [Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/).
- Machen Sie sich mit [bewährten Methoden für KI-Architekturen](https://docs.microsoft.com/azure/architecture/solution-ideas/articles/ai-at-the-edge) vertraut.
