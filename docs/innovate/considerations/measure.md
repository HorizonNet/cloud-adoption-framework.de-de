---
title: 'Cloudinnovation: Measures'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Einführung in die Cloudinnovation: Measures für Inhalte'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 00928171c3bfba1638a7e8e43ea08df4745754d2
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558436"
---
# <a name="measure-for-customer-impact"></a>Messen der Auswirkungen für Kunden

Es gibt mehrere Möglichkeiten, um die Auswirkungen auf Kunden zu messen. Dieser Artikel unterstützt Sie beim Definieren von Measures, die bei der Validierung von Hypothesen helfen können, die während des Versuchs erstellt werden, [Lösungen mit Kundenempathie zu erstellen](./build.md).

## <a name="strategic-metrics"></a>Strategische Metriken

Während der [Strategiephase](../../strategy/index.md) des Lebenszyklus von Cloud Adoption werden die Leser durch die Erstellung und Dokumentation von [Motivationen](../../strategy/motivations.md) und [Geschäftsergebnissen](../../strategy/business-outcomes/index.md) geleitet. Diese Übungen bieten einen Satz von Metriken, die als Test der Kundenauswirkung verwendet werden. Wenn die Innovation erfolgreich ist, führt sie zu Ergebnissen, die an den Strategiezielen ausgerichtet sind.

Bevor Sie Lernmetriken einrichten, sollten Sie eine kleine Anzahl von strategischen Metriken definieren, auf die sich diese Innovation auswirkt. Im Allgemeinen beziehen sich diese strategischen Metriken auf mindestens einen der folgenden Ergebnisbereiche: [Business Agility](../../strategy/business-outcomes/agility-outcomes.md), [Customer Engagement](../../strategy/business-outcomes/engagement-outcomes.md), [Kundenreichweite](../../strategy/business-outcomes/reach-outcomes.md), [finanzielle Auswirkungen](../../strategy/business-outcomes/fiscal-outcomes.md) oder im Fall von betrieblichen Innovationen: [Lösungsleistung](../../strategy/business-outcomes/fiscal-outcomes.md).

Dokumentieren Sie die vereinbarten Metriken, und verfolgen Sie die Auswirkung regelmäßig nach. Erwarten Sie jedoch nicht, dass Ergebnisse in einer dieser Metriken bereits bei mehreren Iterationen entstehen. Lesen Sie [Verpflichtung zu Iterationen](./index.md#commitment-to-iteration), um die Erwartungen einschätzen zu können.

Abgesehen von der Motivation und den Geschäftsergebnismetriken konzentriert sich der Rest dieses Artikels auf Lernmetriken, die für transparente Ermittlung und kundenorientierte Iterationen konzipiert sind. Lesen Sie [Verpflichtung zur Transparenz](./index.md#commitment-to-transparency), um die Erwartungen einschätzen zu können.

## <a name="learning-metrics"></a>Lernmetriken

Wenn die erste Version eines Minimum Viable Product (MVP) dem Kunden vorgestellt wird (vorzugsweise am Ende der ersten Entwicklungsiteration), gibt es noch keine Auswirkungen auf die strategischen Metriken. Mehrere Iterationen später kann es für das Team immer noch schwierig sein, die Verhaltensweisen so weit zu ändern, dass sich die strategischen Metriken entscheidend auswirken. Bei Lernprozessen (z.B. bei Zyklen aus Erstellen, Messen und Lernen) wird empfohlen, dass das Team Lernmetriken einsetzt. Diese Metriken können leichter nachverfolgt und für Lernmöglichkeiten genutzt werden.

### <a name="customer-flow-and-learning-metrics"></a>Customer Flow und Lernmetriken

Wenn eine MVP-Lösung eine kundenorientierte Hypothese validiert, führt die Lösung zu Änderungen im Kundenverhalten. Diese Verhaltensweisen für verschiedene Kundenkohorten sind für die Geschäftsergebnisse entscheidend. Glücklicherweise ist das Ändern von Kundenverhalten häufig ein Prozess, der aus mehreren Schritten besteht. Jeder Schritt bietet die Möglichkeit, die Auswirkungen zu messen, sodass das Cloud Adoption-Team lernen und eine bessere Lösung entwickeln kann.

Die Erkenntnisse über Änderungen im Kundenverhalten beginnen mit der Zuordnung des gewünschten Flows, der durch eine MVP-Lösung generiert wird.

![Zum Ermitteln der Lernmetriken verwendeter Customer Flow](../../_images/innovate/customer-flow-learning-metrics.png)

In den meisten Fällen verfügt ein Customer Flow über einen einfach zu definierenden Ausgangspunkt und über höchstens zwei Endpunkte. Zwischen dem Ausgangs- und den Endpunkten stehen eine Vielzahl von Lernmetriken zur Verwendung als Measures in der Feedbackschleife zur Auswahl:

1. **Ausgangspunkt – Anfänglicher Trigger:** Der Ausgangspunkt ist das Szenario, das die Notwendigkeit dieser Lösung auslöst. Wenn die Lösung mit Kundenempathie erstellt wird, sollte dieser anfängliche Trigger einen Kunden zum Ausprobieren der MVP-Lösung bewegen.
2. **Kundenanforderung erfüllt:** Die Hypothese wurde validiert, wenn eine Kundenanforderung mithilfe der Lösung erfüllt wurde.
3. **Lösungsschritte:** Jeder Schritt, der erforderlich ist, um den Kunden vom anfänglichen Trigger zu einem erfolgreichen Ergebnis zu verhelfen, ist ein Lösungsschritt. Jeder Schritt erzeugt eine Lernmetrik, die auf Kundenentscheidungen basiert, um mit dem nächsten Schritt fortzufahren.
4. **Individuelle Cloud Adoption erreicht:** Bei der nächsten Ausführung des Triggers wird die individuelle Cloud Adoption erreicht, wenn der Kunde zur Lösung zurückkehrt, damit die Anforderung erneut erfüllt wird.
5. **Indikator für Geschäftsergebnis:** Wenn sich ein Kunde auf eine Weise verhält, die positiv zum definierten Geschäftsergebnis beiträgt, kann ein Indikator für das Geschäftsergebnis beobachtet werden.
6. **Echte Innovation:** Wenn sowohl „Geschäftsergebnisindikatoren“ als auch „individuelle Akzeptanz“ im gewünschten Maßstab auftreten, hat echte Innovation stattgefunden.

Jeder Schritt im Customer Flow generiert Lernmetriken. Nach jeder Iterationen (oder jedem Release) wird eine neue Version der Hypothese getestet. Gleichzeitig werden Optimierungen der Lösung getestet, um Anpassungen der Hypothese widerzuspiegeln. Wenn Kunden den vorgegebenen Pfad mit jedem einzelnen Schritt befolgen, wird eine positive Metrik erfasst. Wenn Kunden vom vorgegebenen Pfad abweichen, um Ihre Anforderungen zu erfüllen, wird eine negative Metrik aufgezeichnet.

Diese Ausrichtungs- und Abgrenzungsindikatoren führen zu Lernmetriken. Jede Metrik sollte aufgezeichnet und nachverfolgt werden, wenn das Cloud Adoption-Team Fortschritte in Bezug auf die Realisierung von Geschäftsergebnissen und echter Innovation erzielt. Im nächsten Artikel [Lernen mit Kundenpartnern](./learn.md) wird erläutert, wie Sie diese Metriken nutzen können, um zu lernen und bessere Lösungen zu erstellen.

### <a name="grouping-and-observing-customer-partners"></a>Gruppieren und Beobachten von Kundenpartnern

Die erste Messung zum Definieren von Lernmetriken ist die Kundenpartnerdefinition. Alle Kunden, die an Innovationszyklen teilnehmen, qualifizieren sich als Kundenpartner. Um das Verhalten genau zu messen, ist es wichtig, Kundenpartner in einem Kohortenmodell zu definieren. In diesem Modell werden Kunden gruppiert, um bestmöglich zu verstehen, wie sie auf Änderungen im MVP reagieren. Kundenpartner werden häufig auf der Grundlage von Datenpunkten wie den folgenden gruppiert:

- **Experiment- oder Fokusgruppe:** Gruppierung basierend auf der Teilnahme eines Kunden an einem bestimmten Experiment, um Änderungen im Laufe der Zeit zu testen.
- **Segment:** Gruppieren von Kunden nach der Größe des Unternehmens.
- **Schlüsselindustrie:** Gruppieren von Kunden nach der Schlüsselindustrie, die Sie repräsentieren.
- **Individuelle demografische Informationen:** Gruppierung basierend auf persönlichen demografischen Angaben wie Alter oder physischer Standort.

Diese Art der Gruppierung ermöglicht die Validierung von Lernmetriken über verschiedene Querschnitte der Kunden, die sich für eine Partnerschaft mit Ihnen während der Innovationsbemühungen entscheiden. Alle nachfolgenden Metriken sollten auf der Grundlage einer definierbaren Kundengruppierung beobachtet werden.

## <a name="next-steps"></a>Nächste Schritte

Wenn Lernmetriken akkumuliert werden, kann das Team damit beginnen, [von Kunden zu lernen](./learn.md).

> [!div class="nextstepaction"]
> [Lernen von Kunden](./learn.md)

Einige der Konzepte in diesem Artikel bauen auf Themen auf, die zuerst in [The Lean Startup](http://theleanstartup.com/book) von Eric Ries beschrieben wurden.
