---
title: Einführung in das Betriebsmodell
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hier finden Sie grundlegende Informationen zum Betriebsmodell des Frameworks für die Cloudeinführung.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: operating-model
ms.openlocfilehash: 85123239ad6dd4a389a2b32692638a3debe98951
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556631"
---
# <a name="establish-an-operating-model-for-the-cloud"></a>Einrichten eines Betriebsmodells für die Cloud

Die Cloudeinführung besteht aus iterativen Maßnahmen, die darauf ausgerichtet sind, welche Aktionen Sie in der Cloud ausführen. Die Cloudstrategie skizziert die digitale Transformation, um Unternehmensprogramme zu unterstützen, wie etwa die Ausführung von Einführungsprojekten verschiedener Teams. Durch Planung und Bereitschaft wird der Erfolg all dieser wichtigen Elemente sichergestellt. Alle Schritte der Cloudeinführung entsprechen konkreten Projekten mit verwaltbaren Zielen, Zeitplänen und Budgets.

Die Maßnahmen zur Einführung können relativ einfach nachverfolgt und gemessen werden, auch wenn mehrere Iterationen und Freigaben geplant sind. Jede Phase des Einführungslebenszyklus ist wichtig. In jeder Phase gibt es unter Umständen potenzielle Hindernisse aufgrund geschäftlicher, kultureller und technologischer Einschränkungen. Allerdings ist jede Phase stark vom zugrunde liegenden Betriebsmodell abhängig.

**In der Einführung ist beschrieben, was Sie tun, während das Betriebsmodell definiert, wer die Einführung wie ermöglicht.**

Satya Nadella sagte dazu einmal **„Die Kultur isst die Strategie zum Frühstück.“** Das Betriebsmodell verkörpert die IT-Kultur, die in einer Reihe messbarer Prozesse erfasst wird. Wenn die Cloud von einem starken Betriebsmodell unterstützt wird, wird auch die Strategie besser übernommen, was wiederum die Akzeptanz und das Erreichen von Geschäftswerten beschleunigt. Wenn die Einführung hingegen erfolgreich ist, aber kein Betriebsmodell vorhanden ist, ist das Ergebnis unter Umständen zwar beeindruckend, aber sehr kurzlebig. Für den langfristigen Erfolg ist es von entscheidender Bedeutung, dass die Einführung und die Betriebsmodelle parallel weiterentwickelt werden.

## <a name="establish-your-operating-model"></a>Einrichten Ihres Betriebsmodells

Aktuelle Betriebsmodelle können skaliert werden, um die Einführung der Cloud zu unterstützen. Ein modernes Betriebsmodell trägt zur Beseitigung nicht technischer Hindernisse bei der Cloudeinführung bei.

Dieser Abschnitt des Frameworks für die Cloudeinführung stellt ein umsetzbares Betriebsmodell bereit, um Sie bei nicht technischen Entscheidungen zu unterstützen. Dieses Betriebsmodell umfasst drei hilfreiche Methodiken für die Erstellung eines eigenen Cloudbetriebsmodells:

- [Steuern](../govern/index.md): Sorgen Sie für Konsistenz während der gesamten Einführung. Orientieren Sie sich an Governance- oder Complianceanforderungen, um eine optimale Verwaltung Ihrer cloudübergreifenden Umgebung zu gewährleisten.
- [Verwalten](../manage/index.md): Gestalten Sie laufende Prozesse für die Verwaltung des Technologiebetriebs so, dass sie zur Nutzenmaximierung und zur Vermeidung von Störungen beitragen.
- [Organisieren](../organize/index.md): Bei der Entwicklung des Betriebsmodells entwickelt sich auch die Organisation der unterschiedlichen Teams und Funktionen weiter, die das Betriebsmodell unterstützen.

## <a name="aligning-operating-models"></a>Ausrichten von Betriebsmodellen

Die Cloud und die digitale Wirtschaft haben aufgezeigt, dass mehrere Betriebsmodelle erforderlich sind. Manchmal geht dieser Bedarf von der Anforderung aus, mehrere Public Clouds zu unterstützen. Meistens entsteht dieser Bedarf jedoch beim Wechsel von einer lokalen Umgebung in die Cloud. In beiden Szenarien ist es wichtig, Betriebsmodelle auszurichten, um maximale Leistung bei minimaler Redundanz zu erreichen.

Analysten prognostizieren eine Einführung von Multi-Cloud-Umgebungen bei hohen Volumen. Die Entwicklung geht bei vielen Kunden in diese Richtung. Leider berichten Kunden jedoch von großen Herausforderungen beim Betrieb mehrerer Clouds. Duplizierte Ressourcen, Prozesse, Fertigkeiten und Technologien führen zu höheren Kosten und nicht zu den angekündigten Einsparungen. Um dies zu vermeiden, wird den Kunden empfohlen, ein spezielles Betriebsmodell einzuführen. Beim Ausrichten von Betriebsmodellen sollte immer ein **allgemeines Betriebsmodell** vorhanden sein. Zusätzliche **spezialisierte Betriebsmodelle** kommen für bestimmte Szenarien zum Einsatz, um Abweichungen vom Standardmodell zu unterstützen.

- **Allgemeines Betriebsmodell:** Das allgemeine Betriebsmodell ist für eine einzelne Public oder Private Cloud-Plattform geeignet. Vorgänge dieser Plattform definieren betriebliche Standards, Richtlinien und Prozesse. Dieses Betriebsmodell sollte das primäre Mittel für die weitere Cloudstrategie darstellen. Bei diesem Modell besteht das Ziel darin, den primären Cloudanbieter für den Großteil der Cloudeinführung zu nutzen.

- **Spezialisiertes Cloudbetriebsmodell:** Bestimmte Geschäftsergebnisse sind für einen alternativen Cloudanbieter unter Umständen besser geeignet. Bei einem überzeugenden Geschäftsszenario werden die Standards, Richtlinien und Prozesse vom allgemeinen Betriebsmodell auf den neuen Cloudanbieter angewendet und anschließend an den speziellen Anwendungsfall angepasst.

Wenn Azure die primäre Plattform der Wahl ist, sind die Leitfäden und bewährten Methoden in jedem der oben aufgeführten Abschnitte zu Betriebsmodellen beim Erstellen Ihres Betriebsmodells sehr hilfreich. Dieses Framework berücksichtigt jedoch, dass nicht alle unserer Leser in Azure als primäre Plattform verwenden. Um dieser breiteren Zielgruppe Rechnung zu tragen, kann der theoretische Inhalt in den einzelnen Abschnitten auf Public oder Private Cloud-Betriebsmodelle mit ähnlichen Ergebnissen angewendet werden.

## <a name="next-steps"></a>Nächste Schritte

Governance ist ein gängiger erster Schritt zur Einrichtung eines Betriebsmodells für die Cloud.

> [!div class="nextstepaction"]
> [Informationen zur Cloudgovernance](../govern/index.md)
