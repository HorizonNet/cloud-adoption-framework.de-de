---
title: KI-Anwendungen
description: Integrieren von KI in eine Anwendung mit Microsoft Azure Cognitive Services
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 9e331bc698467926e496b6a1e8c29e7fb0caf097
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88882633"
---
# <a name="ai-applications-and-agents"></a>KI-Anwendungen und -Agents

Das Integrieren von künstlicher Intelligenz (KI) in eine Anwendung kann schwierig und zeitaufwendig sein. Bis vor Kurzem waren fundiertes Wissen über maschinelles Lernen und eine monatelange Entwicklung notwendig, um Daten abzurufen, Modelle zu trainieren und diese im großen Stil bereitzustellen. Auch dann war jedoch der Erfolg keinesfalls garantiert. Der Pfad war mit Hindernissen, Problemen und Rückschlägen verbunden, sodass einige Teams den tatsächlichen Nutzen aus ihrer KI-Investitionen nicht richtig einschätzen konnten.

## <a name="ai-applications"></a>KI-Anwendungen

Microsoft Azure Cognitive Services beseitigt diese Schwierigkeiten und ist auf Produktivität, Unternehmensbereitschaft und Vertrauen ausgelegt. Die Dienste ermöglichen es Ihnen, die neuesten Errungenschaften bei künstlicher Intelligenz zu nutzen, ohne eigene Modelle erstellen und bereitstellen zu müssen. Stattdessen können Sie mit nur wenigen einfachen Codezeilen KI-Modelle bereitstellen, sodass Sie auch ohne großes Data Science-Team zügig Anwendungen erstellen können, die sehen, hören, sprechen und sogar bereits Verständnis entwickeln können.

Häufige Szenarien für KI-Anwendungen:

- Stimmungsanalyse
- Objekterkennung
- Sprachübersetzung
- Personalisierung
- Robotergesteuerte Prozessautomatisierung

Die unten angegebene Checkliste und die Ressourcen dienen Ihnen beim Einstieg als Hilfe bei der Anwendungsentwicklung und -bereitstellung.

- Kennen Sie die vielen Funktionen und Dienste, die Azure Cognitive Services bietet, und wissen Sie schon, welche Sie verwenden werden?
- Ermitteln Sie, ob Sie benutzerdefinierte Daten nutzen, mit denen Sie diese Modelle trainieren und anpassen möchten. Einige Cognitive Services sind anpassbar.
- Es gibt mehrere Möglichkeiten, Azure Cognitive Services zu verwenden. Erkunden Sie die Schnellstarttutorials zum Einrichten und Ausführen von SDK und REST-APIs. Hinweis: Es stehen Cognitive Services-SDKs für viele beliebte Programmiersprachen zur Verfügung, einschließlich C#, Python, Java, JavaScript und Go.
- Legen Sie fest, ob diese Cognitive Services in Containern bereitgestellt werden müssen.

## <a name="ai-applications-checklist"></a>Prüfliste für KI-Anwendungen

Machen Sie sich zunächst mit den verschiedenen Kategorien und Diensten in Azure Cognitive Services vertraut. Besuchen Sie die Produktseiten, um mehr zu erfahren und Demos zu testen, über die Sie mehr über die verfügbaren Funktionen erfahren, z. B. Sehen, Sprechen, Spracherkennung und Entscheidungsfindung. Es gibt auch ein E-Book, in dem gängige Szenarien und das Erstellen Ihrer ersten Anwendung mit Cognitive Services erläutert werden.

- [Cognitive Services](/azure/cognitive-services/welcome)
- [Interaktive Demos auf den Produkt-/Dienstseiten](https://azure.microsoft.com/services/cognitive-services/)
- Lesen Sie das E-Book [Erstellen intelligenter Apps mit kognitiven APIs](https://azure.microsoft.com/resources/building-intelligent-apps-with-cognitive-apis/).

Wählen Sie den Dienst aus, den Sie für das maschinelle Sehen oder Sprechen, die Spracherkennung, die Entscheidungsfindung oder die Websuche verwenden möchten. Jede Kategorie auf der Seite bietet eine Reihe von Schnellstarts, Tutorials und Schrittanleitungen für die REST-APIs oder SDKs.

<!-- docsTest:casing "Intelligent Kiosk" -->

Sie können auch den intelligenten Kiosk herunterladen, um diese Dienste zu erleben und an Demos zu testen.

- [Dokumentation zu Cognitive Services](/azure/cognitive-services/)
- Lesen Sie das E-Book [Erstellen intelligenter Apps mit kognitiven APIs](https://azure.microsoft.com/resources/building-intelligent-apps-with-cognitive-apis/).
- [Installieren Sie den intelligenten Kiosk, um sich mit den Funktionen von Cognitive Services vertraut zu machen.](https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk)

Erfahren Sie mehr über die Containerunterstützung für Azure Cognitive Services.

- [Containerunterstützung in Azure Cognitive Services](/azure/cognitive-services/cognitive-services-container-support?tabs=luis)

Sehen Sie sich die Referenzarchitekturen für KI-Lösungen an.

- [KI und Machine Learning](/azure/architecture/browse/#ai--machine-learning)

## <a name="ai-agents"></a>KI-Agents

Die Azure KI-Plattform von Microsoft zielt darauf ab, Entwicklern mehr Innovationen zu bieten und eine Beschleunigung ihrer Projekte zu ermöglichen. Speziell für die Konversations-KI bietet Azure den Azure Bot Service und das Bot Framework SDK sowie Tools, mit denen Entwickler umfassende Unterhaltungsfunktionen erstellen können. Darüber hinaus können Entwickler Azure Cognitive Services (domänenspezifische KI-Dienste, die als APIs verfügbar sind) wie Language Understanding (LUIS), QnA Maker und den Speech-Dienst verwenden, um den eigenen Chatbot um Funktionen für die Kommunikation mit ihren Endbenutzern zu erweitern.

Häufige Szenarien für Lösungen mit Konversations-KI oder Chatbot:

- Chatbot für Informationen (Q&A)
- Chatbot für Kundendienst oder Support
- Chatbot für IT-Helpdesk oder Personalabteilung
- Chatbot für E-Commerce oder Verkauf
- Sprachfähige Geräte

> [!NOTE]
> Wir bieten für Entwickler, die einen Chatbot mit wenig oder gar keinem Code erstellen möchten, Power Virtual Agents, die auf dem Bot Framework basieren. Außerdem müssen Entwickler, die Cognitive Services nutzen, weder den Bot selbst hosten noch die natürliche Sprache oder andere KI-Modelle selbst steuern.

## <a name="ai-agents-checklist"></a>Prüfliste für KI-Agents

Machen Sie sich mit Azure Bot Service und Microsoft Bot Framework vertraut.

- Bot Framework stellt als Open-Source-Angebot ein SDK (verfügbar in C#, JavaScript, Python und Java) bereit, das Sie beim Entwerfen, Erstellen und Testen Ihres Bots unterstützt. Außerdem bietet es mit dem Bot Framework Composer einen kostenlosen visuellen Zeichenbereich und mit dem Bot Framework Emulator ein Testtool.
- Azure Bot Service ist ein dedizierter Dienst in Azure, der es Ihnen ermöglicht, Ihren Bot in Azure zu hosten oder zu veröffentlichen und mit beliebten Kanälen zu verbinden.

- [Erfahren Sie mehr über Azure Bot Service und Bot Framework.](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
- [Prinzipien des Bot-Entwurfs](/azure/bot-service/bot-service-design-principles?view=azure-bot-service-4.0)
- [Finden Sie die neuesten Versionen des Bot Framework SDK und der Tools.](/azure/bot-service/what-is-new?view=azure-bot-service-4.0)

Eine der einfachsten Möglichkeiten für den Einstieg stellt QnA Maker dar. Dieser Dienst ist Teil von Azure Cognitive Services und kann ein Dokument mit häufig gestellten Fragen oder eine Website innerhalb von Minuten in eine Frage-Antwort-Umgebung verwandeln.

- [Erfahren Sie, wie Sie mit QnA Maker schnell einen Bot mit Frage-Antwort-Funktion erstellen.](/azure/bot-service/bot-builder-tutorial-add-qna?tabs=csharp&view=azure-bot-service-4.0)
- [Direktes Testen des QnA Maker-Diensts](https://www.qnamaker.ai/)

Herunterladen und Verwenden des Bot Framework SDK und der Tools für die Bot-Entwicklung

- [5-Minuten-Schnellstart mit Bot Framework Composer](/composer/)
- [Erstellen und Testen von Bots mit dem Bot Framework SDK (C#, JavaScript, Python)](/azure/bot-service/dotnet/bot-builder-dotnet-sdk-quickstart?view=azure-bot-service-4.0)

Erfahren Sie, wie Sie Cognitive Services hinzufügen, um Ihren Bot noch intelligenter zu gestalten.

- [Entwicklerhandbuch zum Erstellen von KI-Anwendungen](https://www.oreilly.com/library/view/a-developers-guide/9781492080619/) (E-Book)
- Informieren Sie sich ausführlicher über [Cognitive Services](/azure/cognitive-services/).

Erfahren Sie, wie Sie einen eigenen virtuellen Assistenten mit Bot Framework-Solution Accelerators erstellen, und wählen Sie einen allgemeinen Satz von Skills aus, z. B. Kalender, E-Mail, Point of Interest oder Aufgaben.

- [Bot Framework-Lösung für einen virtuellen Assistenten](https://microsoft.github.io/botframework-solutions/index)

## <a name="next-steps"></a>Nächste Schritte

Erkunden Sie andere Kategorien für KI-Lösungen:

- [Maschinelles Lernen](./machine-learning.md)
- [Knowledge Mining](./knowledge-mining.md)
