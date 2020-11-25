---
title: Was sind KI-Agents?
description: Hier finden Sie Informationen zu KI-Agents und Unterhaltungsschnittstellen. Außerdem erfahren Sie, wie Sie einen Bot planen, erstellen, testen, veröffentlichen, mit verschiedenen Kanälen verbinden und bewerten.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: think-tank
ms.openlocfilehash: f3174a439376cbb23f1446a1bdca30f77e613363
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95446826"
---
<!-- docutune:casing "natural language understanding" -->
<!-- cSpell:ignore Twilio -->

# <a name="what-are-ai-agents"></a>Was sind KI-Agents?

Benutzer interagieren immer mehr mit Konversationsschnittstellen. Diese bieten eine natürlichere Umgebung, in der Benutzer ihre Anforderungen in natürlicher Sprache äußern und Aufgaben schnell erledigen können. Für viele Unternehmen entwickeln sich Anwendungen mit Konversations-KI zu einem Wettbewerbsfaktor. Zahlreiche Organisationen machen Bots strategisch auf den Messagingplattformen verfügbar, die auch von ihren Kunden genutzt werden.

Organisationen auf der ganzen Welt nutzen Konversations-KI, um eine effizientere und natürlichere Interaktion mit Kunden und Mitarbeitern zu ermöglichen. Im Anschluss finden Sie einige gängige Anwendungsfälle:

- Kundendienst
- Assistent für Unternehmen
- Callcenteroptimierung
- Sprachassistent für Fahrzeuge

## <a name="build-a-bot"></a>Erstellen eines Bots

Azure Bot Service und Bot Framework bieten integrierte Tools und Dienste, die diesen Prozess vereinfachen. Verwenden Sie Ihre bevorzugte Entwicklungsumgebung oder bevorzugten Befehlszeilentools, um Ihren Bot zu erstellen. Es sind SDKs für C#, JavaScript, TypeScript und Python verfügbar. Das SDK für Java wird derzeit entwickelt. Wir stellen Tools für unterschiedliche Phasen der Bot-Entwicklung bereit, um Sie beim Entwerfen und Erstellen von Bots zu unterstützen.

![Diagramm mit Tools für die verschiedenen Phasen der Bot-Entwicklung](../../_images/ai-bot-dev-tools.png)

### <a name="plan"></a>Planen

Ein umfassendes Verständnis der Ziele, Prozesse und Benutzeranforderungen ist wichtig für das Erstellen eines erfolgreichen Bots. Machen Sie sich vor dem Programmieren mit dem [Entwurfsleitfaden](/azure/bot-service/bot-service-design-principles?view=azure-bot-service-4.0) für Bots vertraut, um Informationen zu bewährten Methoden und Anforderungen für Ihren Bot zu erhalten. Sie können einen einfachen Bot erstellen oder komplexere Funktionen wie Spracheingabe, Verständnis natürlicher Sprache oder Beantwortung von Fragen hinzufügen.

Berücksichtigen Sie beim Entwerfen Ihres Bots in der Planungsphase die folgenden Aspekte:

- Definieren der Bot-Persona:
  - Wie soll Ihr Bot aussehen?
    - Wie soll er heißen?
    - Was für eine Persönlichkeit soll Ihr Bot haben? Hat er ein Geschlecht?
    - Wie soll Ihr Bot auf schwierige Situationen und Fragen reagieren?
- Entwerfen des Konversationsablaufs:
  - Welche Art von Konversationen ist für Ihre Anwendungsfälle zu erwarten?
- Definieren eines Bewertungsplans:
  - Wie kann der Erfolg gemessen werden?
  - Welche Messungen sollen verwendet werden, um den Dienst zu verbessern?

Weitere Informationen zum Entwerfen Ihres Bots finden Sie in den [Prinzipien des Bot-Entwurfs](/azure/bot-service/bot-service-design-principles?view=azure-bot-service-4.0).

### <a name="build"></a>Entwickeln

Ihr Bot ist ein Webdienst, der eine Konversationsoberfläche implementiert und mit dem Bot Framework-Dienst kommuniziert, um Nachrichten und Ereignisse zu senden und zu empfangen. Bot Framework Service ist eine Komponente von Azure Bot Service und Bot Framework. Sie können Bots in einer beliebigen Anzahl von Umgebungen und Sprachen erstellen. Sie können mit der Bot-Entwicklung im [Azure-Portal](/azure/bot-service/bot-service-quickstart?view=azure-bot-service-4.0) beginnen oder Vorlagen für [C#, JavaScript oder Python](/azure/bot-service/dotnet/bot-builder-dotnet-sdk-quickstart?view=azure-bot-service-4.0) verwenden, um Ihren Bot lokal zu entwickeln. Sie haben auch Zugriff auf eine Vielzahl von [Beispielen](https://github.com/microsoft/botbuilder-samples), die zahlreiche der über das SDK verfügbaren Funktionen veranschaulichen. Diese Beispiele eignen sich hervorragend für Entwickler, die sich einen Ausgangspunkt mit mehr Features wünschen.

Im Rahmen von Azure Bot Service und Bot Framework stehen zusätzliche Komponenten zur Verfügung, mit denen Sie die Funktionalität Ihres Bots erweitern können.

| Funktion | Beschreibung | Link |
| --- | --- | --- |
| Hinzufügen der Verarbeitung natürlicher Sprache | Ermöglichen Sie es Ihrem Bot, natürliche Sprache zu verstehen, Rechtschreibfehler zu erkennen, Sprachfunktionen zu verwenden sowie die Absichten des Benutzers zu erkennen. | Verwenden von [LUIS](/azure/bot-service/bot-builder-howto-v4-luis?view=azure-bot-service-4.0) (Language Understanding Intelligent Service) |
| Beantworten von Fragen | Fügen Sie eine Wissensdatenbank hinzu, um Fragen von Benutzern auf natürlichere, mit einer Unterhaltung vergleichbare Weise zu beantworten. | Verwenden von [QnA Maker](/azure/bot-service/bot-builder-howto-qna?view=azure-bot-service-4.0) |
| Verwalten mehrerer Modelle | Wenn Sie mehrere Modelle nutzen (z. B. für LUIS und QnA Maker), können Sie auf intelligente Weise ermitteln, wann welches Modell für die Konversation des Bots verwendet werden sollte. | [Dispatch](/azure/bot-service/bot-builder-tutorial-dispatch?view=azure-bot-service-4.0)-Tool |
| Hinzufügen von Karten und Schaltflächen | Verbessern Sie die Benutzerfreundlichkeit durch die Verwendung von anderen Medien als Text, z. B. Grafiken, Menüs und Karten. | [Hinzufügen von Karten](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0) |

> [!NOTE]
> Diese Tabelle stellt keine vollständige Liste dar. Weitere Informationen finden Sie in der [Dokumentation zu Azure Bot Service](/azure/bot-service/).

### <a name="test"></a>Testen

Bots sind komplexe Anwendungen mit vielen verschiedenen Komponenten, die zusammenarbeiten. Wie bei jeder komplexen Anwendung kann diese Komplexität zu einigen interessanten Fehlern oder zu einem unerwartetem Verhalten Ihres Bots führen. Testen Sie Ihren Bot, bevor Sie ihn veröffentlichen. Wir bieten mehrere Methoden zum Testen von Bots, bevor sie zur Verwendung freigegeben werden:

- Testen Sie Ihren Bot lokal mit dem [Emulator](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0). Bot Framework Emulator ist eine eigenständige Anwendung, die nicht nur über eine Chatschnittstelle, sondern auch über Debug- und Abfragetools verfügt, mit denen Sie das Verhalten Ihres Bots nachvollziehen können. Der Emulator kann neben Ihrer in der Entwicklung befindlichen Botanwendung lokal ausgeführt werden.
- Testen Sie Ihren Bot im [Web](/azure/bot-service/bot-service-manage-test-webchat?view=azure-bot-service-4.0). Sobald Ihr Bot über das Azure-Portal konfiguriert wurde, ist er auch über eine Webchat-Schnittstelle erreichbar. Die Webchat-Schnittstelle eignet sich sehr gut, um Testern und anderen Personen, die nicht direkt auf den ausgeführten Code zugreifen können, Zugriff auf Ihren Bot zu gewähren.
- Führen Sie mit dem Update des Bot Framework-SDK aus dem Juli einen [Komponententest für Ihren Bot](/azure/bot-service/unit-test-bots) durch.

### <a name="publish"></a>Veröffentlichen

Wenn Sie bereit sind, Ihren Bot im Web verfügbar zu machen, [veröffentlichen Sie ihn in Azure](/azure/bot-service/bot-builder-howto-deploy-azure?view=azure-bot-service-4.0) oder in Ihrem eigenen Webdienst oder Rechenzentrum. Eine Adresse im öffentlichen Internet ist der erste Schritt, um Ihren Bots auf Ihrer Website oder in Chatkanälen verfügbar zu machen.

### <a name="connect"></a>Verbinden

Verbinden Sie Ihren Bot mit Kanälen wie Facebook, Messenger, Kik, Skype, Slack, Microsoft Teams, Telegram, Text/SMS, Twilio, Cortana und Skype. Bot Framework nimmt Ihnen den Großteil der erforderlichen Aufgaben rund um das Senden und Empfangen von Nachrichten über diese verschiedenen Plattformen ab. Ihre Botanwendung empfängt einen einheitlichen, normalisierten Nachrichtenstrom – unabhängig von der Anzahl und Art der Kanäle, mit denen sie verbunden ist. Informationen zum Hinzufügen von Kanälen finden Sie unter [Verbinden eines Bots mit Kanälen](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0).

### <a name="evaluate"></a>Evaluieren

Verwenden Sie die im Azure-Portal erfassten Daten, um Möglichkeiten zur Verbesserung der Funktionen und der Leistung Ihres Bots zu ermitteln. Sie können einen Servicelevel und Instrumentierungsdaten wie Datenverkehr, Latenz und Integrationen abrufen. Analytics bieten außerdem Berichterstellung für Benutzer-, Nachrichten- und Kanaldaten auf Konversationsebene. Weitere Informationen finden Sie unter [Botanalyse](/azure/bot-service/bot-service-manage-analytics?view=azure-bot-service-4.0).

### <a name="patterns-for-common-use-cases"></a>Muster für gängige Anwendungsfälle

In diesem Abschnitt finden Sie Informationen zu allgemeinen Mustern für die Implementierung einer Anwendung mit Konversations-KI:

- **Wissensdatenbank:** Ein Wissensbot kann so entworfen werden, dass er Informationen zu so gut wie jedem Thema bereitstellt. So kann ein Wissensbot beispielsweise Fragen zu Veranstaltungen beantworten, etwa: „Welche Veranstaltungen zu Bots finden auf dieser Konferenz statt?“ Oder „Wann findet das nächste Reggaekonzert statt?“. Ein anderer Bot beantwortet hingegen möglicherweise IT-bezogene Fragen wie „Wie aktualisiere ich mein Betriebssystem?“. Wieder ein anderer Bot beantwortet möglicherweise Fragen zu Kontakten wie „Wer ist John Doe?“. Oder „Wie lautet die E-Mail-Adresse von Jane Doe?“.

   Informationen zu den Entwurfselementen für Wissensbots finden Sie unter [Entwerfen von Wissensbots](/azure/bot-service/bot-service-design-pattern-knowledge-base?view=azure-bot-service-4.0).

- **Übergabe an einen Menschen:** In bestimmten Situationen muss die Unterhaltung möglicherweise immer noch an einen Menschen übergeben werden – ganz gleich, über wie viel künstliche Intelligenz ein Bot verfügt. In solchen Fällen sollte der Bot erkennen, wann eine Übergabe erforderlich ist, und dem Benutzer eine reibungslose Übergabe ermöglichen.

   Informationen zu Mustern für die Übergabe finden Sie unter [Übergeben von Konversationen von einem Bot an einen Menschen](/azure/bot-service/bot-service-design-pattern-handoff-human?view=azure-bot-service-4.0).

- **Einbetten eines Bots in eine Anwendung:** Bots befinden sich zwar in den meisten Fällen außerhalb von Anwendungen, können aber auch mit Anwendungen integriert werden. Beispielsweise können Sie einen [Wissensbot](/azure/bot-service/bot-service-design-pattern-knowledge-base?view=azure-bot-service-4.0) in eine Anwendung einbetten, um Benutzer bei der Suche nach Informationen zu unterstützen. Sie können auch einen Bot in eine Helpdeskanwendung einbetten, der dann als erste Anlaufstelle für eingehende Benutzeranfragen fungiert. Der Bot kann unabhängig einfache Probleme lösen und kompliziertere Fälle an einen menschlichen Mitarbeiter [übergeben](/azure/bot-service/bot-service-design-pattern-handoff-human?view=azure-bot-service-4.0).

   Weitere Informationen dazu, wie Sie einen Bot in eine Anwendung integrieren können, finden Sie unter [Einbetten eines Bots in eine App](/azure/bot-service/bot-service-design-pattern-embed-app?view=azure-bot-service-4.0).

- **Einbetten eines Bots in eine Website:** Bots können nicht nur in Anwendungen, sondern auch in Websites eingebettet werden, um mehrere Kommunikationsmöglichkeiten über verschiedene Kanäle zu bieten.

   Weitere Informationen dazu, wie Sie einen Bot in eine Website integrieren können, finden Sie unter [Einbetten eines Bots in eine Website](/azure/bot-service/bot-service-design-pattern-embed-web-site?view=azure-bot-service-4.0).

## <a name="next-steps"></a>Nächste Schritte

- Lesen Sie Whitepaper über maschinelles Lernen und E-Books zu [Azure Bot Service](https://azure.microsoft.com/resources/whitepapers/search/?service=bot-service).
- Machen Sie sich mit [KI-Architekturen und Architekturen für maschinelles Lernen](/azure/architecture/browse/) vertraut.
- Lesen Sie das E-Book zum [Erstellen intelligenter Anwendungen mit kognitiven APIs](https://azure.microsoft.com/resources/building-intelligent-apps-with-cognitive-apis/).
- Machen Sie sich mit [häufig gestellten Fragen zur Chatbotarchitektur](https://azure.microsoft.com/resources/faq-chatbot-architecture/) vertraut.
