---
title: Konversations-KI
description: Für Konversations-KI bietet Azure den Azure Bot Service und das Bot Framework-SDK sowie Tools, mit denen Entwickler umfassende Unterhaltungsfunktionen erstellen können.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a908cdaa72ff857f0e1743100710e83434bcda55
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94712577"
---
# <a name="conversational-ai"></a>Konversations-KI

Die Azure KI-Plattform von Microsoft zielt darauf ab, Entwicklern mehr Innovationen zu bieten und eine Beschleunigung ihrer Projekte zu ermöglichen. Speziell für die Konversations-KI bietet Azure den Azure Bot Service und das Bot Framework SDK sowie Tools, mit denen Entwickler umfassende Unterhaltungsfunktionen erstellen können. Darüber hinaus können Entwickler Azure Cognitive Services (domänenspezifische KI-Dienste, die als APIs verfügbar sind) wie Language Understanding (LUIS), QnA Maker und den Speech-Dienst verwenden, um den eigenen Chatbot um Funktionen für die Kommunikation mit ihren Endbenutzern zu erweitern.

Häufige Szenarien für Lösungen mit Konversations-KI oder Chatbot:

- Chatbot für Informationen (Q&A)
- Chatbot für Kundendienst oder Support
- Chatbot für IT-Helpdesk oder Personalabteilung
- Chatbot für E-Commerce oder Verkauf
- Sprachfähige Geräte

> [!NOTE]
> Für Entwickler, die einen Chatbot primär codelos oder mit wenig Code entwickeln möchten, bietet Microsoft Power Virtual Agents, einen auf Bot Framework basierenden Dienst. Außerdem müssen Entwickler, die Cognitive Services nutzen, weder den Bot selbst hosten noch die natürliche Sprache oder andere KI-Modelle selbst steuern.

## <a name="checklist"></a>Checkliste

Machen Sie sich mit Azure Bot Service und Microsoft Bot Framework vertraut.

- Bot Framework ist ein Open-Source-Angebot, das ein SDK (verfügbar in C#, JavaScript, Python und Java) bereitstellt, das Sie beim Entwerfen, Entwickeln und Testen Ihres Bots unterstützt. Außerdem bietet es mit dem Bot Framework Composer einen kostenlosen visuellen Zeichenbereich und mit dem Bot Framework Emulator ein Testtool.
- Azure Bot Service ist ein dedizierter Dienst in Azure, der es Ihnen ermöglicht, Ihren Bot in Azure zu hosten oder zu veröffentlichen und mit beliebten Kanälen zu verbinden.

- Lesen Sie die [Übersicht zu Azure Bot Service und Bot Framework](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).
- Erfahren Sie mehr über [Prinzipien des Bot-Entwurfs](/azure/bot-service/bot-service-design-principles?view=azure-bot-service-4.0).
- Holen Sie sich die [neuesten Versionen des Bot Framework SDK und der Tools](/azure/bot-service/what-is-new?view=azure-bot-service-4.0).

Eine der einfachsten Möglichkeiten für den Einstieg stellt QnA Maker dar. Dieser Dienst ist Teil von Azure Cognitive Services und kann ein Dokument mit häufig gestellten Fragen oder eine Website innerhalb von Minuten in eine Frage-Antwort-Umgebung verwandeln.

- [Schnelles Erstellen eines Bots mit Frage-Antwort-Funktion mit QnA Maker](/azure/bot-service/bot-builder-tutorial-add-qna?tabs=csharp&view=azure-bot-service-4.0)
- Testen des [QnA Maker-Diensts](https://www.qnamaker.ai/)

Herunterladen und Verwenden des Bot Framework SDK und der Tools für die Bot-Entwicklung.

- [5-Minuten-Schnellstartanleitungen für Bot Framework Composer](/composer/)
- [Erstellen und Testen von Bots mit dem Bot Framework SDK (C#, JavaScript, Python)](/azure/bot-service/dotnet/bot-builder-dotnet-sdk-quickstart?view=azure-bot-service-4.0)

Erfahren Sie, wie Sie Cognitive Services hinzufügen, um Ihren Bot noch intelligenter zu gestalten.

- [Entwicklerhandbuch zum Erstellen von KI-Anwendungen](https://www.oreilly.com/library/view/a-developers-guide/9781492080619/) (E-Book)
- Informieren Sie sich ausführlicher über [Cognitive Services](/azure/cognitive-services/).

Erfahren Sie, wie Sie einen eigenen virtuellen Assistenten mit Bot Framework-Solution Accelerators erstellen, und wählen Sie einen allgemeinen Satz von Skills aus, z. B. Kalender, E-Mail, Point of Interest oder Aufgaben.

- [Bot Framework-Lösung für einen virtuellen Assistenten](https://microsoft.github.io/botframework-solutions/index)

## <a name="next-steps"></a>Nächste Schritte

[Knowledge Mining](./knowledge-mining.md)
