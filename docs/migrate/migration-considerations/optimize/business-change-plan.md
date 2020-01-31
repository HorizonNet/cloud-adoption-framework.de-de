---
title: Anleitungen zum Erstellen eines geschäftsbezogenen Änderungsplans
description: Ein Prozess innerhalb der Cloudmigration, der sich auf die Aufgaben der Migration von Workloads in die Cloud konzentriert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 48e670028e26be5a28abf55c7a0565769e17dacf
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801969"
---
# <a name="business-change-plan"></a>Geschäftsbezogener Änderungsplan

In der Vergangenheit lag die Veröffentlichung neuer Workloads im Verantwortungsbereich der IT. Auch die Leitung einer tief greifenden Veränderung wie der Migration eines Rechenzentrums oder einer Cloudmigration könnte der IT-Abteilung übertragen werden. Beim herkömmlichen Ansatz könnten aber Möglichkeiten für zusätzliche Unternehmenswerte verpasst werden. Aus diesem Grund wird vor der Umstellung einer migrierten Workload auf die Produktion ein umfassenderer Ansatz für die Benutzereinführung empfohlen. In diesem Artikel werden mögliche Vorteile durch die Umsetzung eines geschäftsbezogenen Änderungsplans für den Standardplan zur Benutzereinführung beschrieben.

## <a name="traditional-user-adoption-approach"></a>Herkömmlicher Ansatz für die Benutzereinführung

Pläne für die Benutzereinführung konzentrieren sich meist darauf, wie Benutzer eine neue Technologie annehmen oder auf eine bestimmte Technologie umsteigen. Dieser Ansatz hat sich lange für die Einführung neuer Tools bei Benutzern bewährt. Bei einem typischen Plan zur Benutzereinführung konzentriert sich die IT auf die Installation, Konfiguration, Wartung und Schulung im Zusammenhang mit den technischen Änderungen durch die neue Geschäftsumgebung.

Obwohl Ansätze variieren können, sind allgemeine Schemas in den meisten Plänen zur Benutzereinführung enthalten. Diese Schemas basieren in der Regel auf einer Risikokontrolle und einem Ansatz zur Vereinfachung der Übernahme von inkrementeller Verbesserung. Die Eason-Matrix in der folgenden Abbildung stellt die Ideen hinter diesen Schemas für verschiedene Einführungsarten dar.

![Eason-Matrix mit Fragen zur Benutzereinführung](../../../_images/migrate/eason-matrix.jpg)

*Eason-Matrix der Arten von Benutzereinführungen*

Diese Schemas basieren häufig auf der Annahme, dass sich Benutzer bei der Einführung neuer Lösungen hauptsächlich auf die Risikokontrolle und die Vereinfachung der Veränderung konzentrieren sollten. Darüber hinaus konzentriert sich die IT vor allem auf die Risiken aus der technologischen Änderung sowie deren Umsetzung.

## <a name="create-business-change-plans"></a>Erstellen geschäftsbezogener Änderungspläne

Bei einem geschäftsbezogenen Änderungsplan wird über die technischen Änderung hinausgeschaut, und dabei wird davon ausgegangen, dass jedes Release bei einer Migration gewisse Änderungen an Geschäftsprozessen nach sich zieht. Dabei wird von den technischen Veränderungen aus in der Kette nach vorne (downstream) und zurückgeblickt (upstream). Die folgenden Fragen helfen Ihnen dabei, die Einführung für die Benutzer aus dem Blickwinkel von geschäftsbezogenen Änderungen zu betrachten, um die Auswirkungen auf Ihre Geschäfte zu maximieren:

**Upstreamfragen:** Upstreamfragen beschäftigen sich mit den Auswirkungen oder Änderungen vor der Benutzereinführung:

- Wurde ein erwartetes [Geschäftsergebnis](../../../strategy/business-outcomes/index.md) quantifiziert?
- Entsprechen die geschäftlichen Auswirkungen den definierten [Lernmetriken](../../../strategy/learning-metrics.md)?
- Welche Geschäftsprozesse und Teams profitieren von dieser technischen Lösung?
- Welche Personen im Unternehmen eignen sich am ehesten als Poweruser und für Feedback?
- Wurden die betroffenen Führungskräfte in die Priorisierung und Planung der Migration einbezogen?
- Gibt es kritische Ereignisse oder Daten für das Unternehmen, die von dieser Änderung betroffen sein könnten?
- Führt der geschäftsbezogene Änderungsplan zu einer Maximierung der Auswirkungen, aber einer Minimierung von Unterbrechungen beim Geschäftsbetrieb?
- Sind Ausfallzeiten zu erwarten? Wurden die Ausfallzeiten den Endbenutzern mitgeteilt?

**Downstreamfragen:** Nach Abschluss der Einführung können die geschäftlichen Änderungen beginnen. Leider ist dies auch der Zeitpunkt, an dem viele Pläne zur Benutzereinführung enden. Downstreamfragen unterstützen das Team für die Cloudstrategie dabei, sich nach der Umsetzung der technischen Änderungen auf die Transformation zu konzentrieren:

- Reagieren geschäftliche Benutzer gut auf die Änderungen?
- Wurde die zu erwartende Leistungsanpassung erreicht, nachdem die technische Änderung umgesetzt wurde?
- Haben sich die Geschäftsprozesse oder Kundenerfahrungen wie erwartet geändert?
- Sind weitere Änderungen erforderlich, um Lernmetriken zu erreichen?
- Entsprechen die Änderungen den gewünschten Geschäftsergebnissen? Wenn nicht: warum?
- Sind zusätzliche Änderungen erforderlich, um die Geschäftsergebnisse zu erreichen?
- Wurden nachteilige Auswirkungen infolge dieser Änderung beobachtet?

Der geschäftsbezogene Änderungsplan variiert von Unternehmen zu Unternehmen. Mithilfe dieser Fragen können die Geschäftsabläufe besser an die Änderung jedes Releases angepasst werden. Wenn jedes neue Release nicht nur als eine technologische Änderung angesehen wird, sondern stattdessen als ein geschäftsbezogener Änderungsplan, können die Geschäftsergebnisse besser beurteilt werden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die Änderungen für das Geschäft dokumentiert und geplant wurden, können die [geschäftsbezogenen Tests](./business-test.md) beginnen.

> [!div class="nextstepaction"]
> [Leitfaden für Tests von Geschäftsabläufen (UAT) während der Migration](./business-test.md)

## <a name="references"></a>References

- Eason, K. (1988) _Information technology and organizational change_, New York: Taylor und Francis (Änderungen bei Unternehmenstechnologien und -abläufen).
