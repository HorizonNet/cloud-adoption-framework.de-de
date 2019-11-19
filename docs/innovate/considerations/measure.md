---
title: 'Cloudinnovation: "Measure"'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Einführung in die Cloudinnovation: Measures für Inhalte'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c050e34feecfe26431c7105eef46d000fbb32cf8
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565601"
---
# <a name="measure-for-customer-impact"></a>Messen der Auswirkungen für Kunden

Es gibt mehrere Möglichkeiten, um die Auswirkungen auf Kunden zu messen. Dieser Artikel unterstützt Sie bei der Definition von Metriken zur Validierung von Hypothesen, die sich aus dem Bestreben ergeben, die [Erstellung mit Blick auf die Kundenanforderungen](./build.md) durchzuführen.

## <a name="strategic-metrics"></a>Strategische Metriken

Während der [Strategiephase](../../strategy/index.md) des Lebenszyklus der Cloudeinführung untersuchen wir [Beweggründe](../../strategy/motivations.md) und [Geschäftsergebnisse](../../strategy/business-outcomes/index.md). Diese Methoden bieten eine Reihe von Metriken, mit denen die Auswirkungen für Kunden getestet werden können. Wenn die Innovation erfolgreich ist, werden in der Regel Ergebnisse erzielt, die auf Ihre strategischen Ziele ausgerichtet sind.

Bevor Sie Lernmetriken einrichten, sollten Sie eine kleine Anzahl von strategischen Metriken definieren, die von dieser Innovation beeinflusst werden sollen. Im Allgemeinen stimmen diese strategischen Metriken mit einem oder mehreren der folgenden Ergebnisbereiche überein: [Unternehmensflexibilität](../../strategy/business-outcomes/agility-outcomes.md), [Kundenbindung](../../strategy/business-outcomes/engagement-outcomes.md), [Kundenreichweite](../../strategy/business-outcomes/reach-outcomes.md), [finanzielle Auswirkungen](../../strategy/business-outcomes/fiscal-outcomes.md) oder im Falle von betrieblichen Innovationen: [Lösungsleistung](../../strategy/business-outcomes/fiscal-outcomes.md).

Dokumentieren Sie die vereinbarten Metriken, und verfolgen Sie deren Auswirkung regelmäßig nach. Erwarten Sie jedoch nicht, dass Ergebnisse in einer dieser Metriken bereits bei mehreren Iterationen entstehen. Weitere Informationen zum Festlegen und Ausrichten der Erwartungen zwischen den Beteiligten finden Sie unter [Verpflichtung zu Iterationen](./index.md#commitment-to-iteration).

Abgesehen von der Motivation und den Geschäftsergebnismetriken konzentriert sich der Rest dieses Artikels auf Lernmetriken, die für transparente Ermittlung und kundenorientierte Iterationen konzipiert sind. Weitere Informationen zu diesen Aspekten finden Sie unter [Verpflichtung zur Transparenz](./index.md#commitment-to-transparency).

## <a name="learning-metrics"></a>Lernmetriken

Wenn die erste Version eines Minimum Viable Product (MVP) dem Kunden vorgestellt wird (vorzugsweise am Ende der ersten Entwicklungsiteration), gibt es noch keine Auswirkungen auf die strategischen Metriken. Mehrere Iterationen später kann es für das Team immer noch schwierig sein, die Verhaltensweisen so weit zu ändern, dass sich die strategischen Metriken entscheidend auswirken. Bei Lernprozessen (z. B. bei Zyklen aus Erstellen, Messen und Lernen) empfehlen wir dem Team, Lernmetriken einzuführen. Diese Metriken bieten Gelegenheiten zur Nachverfolgung und zum Lernen.

### <a name="customer-flow-and-learning-metrics"></a>Customer Flow und Lernmetriken

Wenn eine MVP-Lösung eine kundenorientierte Hypothese validiert, führt die Lösung zu Änderungen im Kundenverhalten. Diese Verhaltensänderungen in allen Kundengruppen sollten die Geschäftsergebnisse verbessern. Beachten Sie, dass die Änderung des Kundenverhaltens in der Regel ein mehrstufiger Prozess ist. Da jeder Schritt die Möglichkeit bietet, die Auswirkungen zu messen, kann das Cloudeinführungsteam auf dem Weg dorthin weiterhin lernen und eine bessere Lösung entwickeln.

Die Erkenntnisse über Änderungen im Kundenverhalten beginnen mit der Zuordnung des Flows, den Sie von einer MVP-Lösung erwarten.

![Zum Ermitteln der Lernmetriken verwendeter Customer Flow](../../_images/innovate/customer-flow-learning-metrics.png)

In den meisten Fällen verfügt ein Customer Flow über einen einfach zu definierenden Ausgangspunkt und über höchstens zwei Endpunkte. Zwischen dem Ausgangs- und den Endpunkten stehen eine Vielzahl von Lernmetriken zur Verwendung als Measures in der Feedbackschleife zur Auswahl:

1. **Ausgangspunkt – Anfänglicher Trigger:** Der Ausgangspunkt ist das Szenario, das die Notwendigkeit dieser Lösung auslöst. Wenn die Lösung mit Kundenempathie erstellt wird, sollte dieser anfängliche Trigger einen Kunden zum Ausprobieren der MVP-Lösung bewegen.
2. **Kundenanforderung erfüllt:** Die Hypothese wurde validiert, wenn eine Kundenanforderung mithilfe der Lösung erfüllt wurde.
3. **Lösungsschritte:** Dieser Begriff bezieht sich auf die Schritte, die erforderlich sind, um den Kunden vom anfänglichen Trigger zu einem erfolgreichen Ergebnis zu führen. Jeder Schritt erzeugt eine Lernmetrik, die auf einer Kundenentscheidung basiert, um mit dem nächsten Schritt fortzufahren.
4. **Individuelle Cloud Adoption erreicht:** Bei der nächsten Ausführung des Triggers wird die individuelle Cloud Adoption erreicht, wenn der Kunde zur Lösung zurückkehrt, damit seine Anforderung erfüllt wird.
5. **Indikator für Geschäftsergebnis:** Wenn sich ein Kunde auf eine Weise verhält, die zum definierten Geschäftsergebnis beiträgt, kann ein Indikator für das Geschäftsergebnis beobachtet werden.
6. **Echte Innovation:** Wenn sowohl *Geschäftsergebnisindikatoren* als auch *individuelle Akzeptanz* im gewünschten Maßstab auftreten, haben Sie echte Innovationen realisiert.

Jeder Schritt im Customer Flow generiert Lernmetriken. Nach jeder Iterationen (oder jedem Release) wird eine neue Version der Hypothese getestet. Gleichzeitig werden Optimierungen der Lösung getestet, um Anpassungen der Hypothese widerzuspiegeln. Wenn Kunden den vorgegebenen Pfad mit jedem einzelnen Schritt befolgen, wird eine positive Metrik erfasst. Wenn Kunden vom vorgegebenen Pfad abweichen, wird eine negative Metrik aufgezeichnet.

Diese Ausrichtungs- und Abgrenzungsindikatoren führen zu Lernmetriken. Jede Metrik sollte aufgezeichnet und nachverfolgt werden, wenn das Cloudeinführungsteam Fortschritte in Bezug auf Geschäftsergebnisse und echte Innovationen erzielt. In [Lernen von Kunden](./learn.md) werden die Möglichkeiten zur Anwendung dieser Metriken diskutiert, um bessere Lösungen kennenzulernen und zu entwickeln.

### <a name="grouping-and-observing-customer-partners"></a>Gruppieren und Beobachten von Kundenpartnern

Die erste Messung beim Definieren von Lernmetriken ist die Definition der Kundenpartner. Alle Kunden, die an Innovationszyklen teilnehmen, qualifizieren sich als Kundenpartner. Um das Verhalten genau zu messen, sollten Sie ein Kohortenmodell verwenden, um Kundenpartner zu definieren. In diesem Modell werden die Kunden gruppiert, um Ihr Verständnis für ihre Reaktionen auf Veränderungen im MVP zu verbessern. Diese Gruppen ähneln in der Regel den folgenden:

- **Experiment- oder Fokusgruppe:** Gruppierung von Kunden basierend auf ihrer Teilnahme an einem bestimmten Experiment, das dazu dient, Änderungen im Laufe der Zeit zu testen.
- **Segment:** Gruppieren von Kunden nach der Größe des Unternehmens.
- **Schlüsselindustrie:** Gruppieren von Kunden nach der *Schlüsselindustrie*, die Sie repräsentieren.
- **Individuelle demografische Informationen:** Gruppierung basierend auf persönlichen demografischen Angaben wie Alter und physischer Standort.

Diese Arten der Gruppierung helfen Ihnen beim Validieren von Lernmetriken über verschiedene Querschnitte der Kunden, die sich für eine Partnerschaft mit Ihnen während Ihrer Innovationsbemühungen entscheiden. Alle nachfolgenden Metriken sollten von einer definierbaren Kundengruppierung abgeleitet werden.

## <a name="next-steps"></a>Nächste Schritte

Wenn Lernmetriken akkumuliert werden, kann das Team damit beginnen, [von Kunden zu lernen](./learn.md).

> [!div class="nextstepaction"]
> [Lernen von Kunden](./learn.md)

Einige der Konzepte in diesem Artikel bauen auf Themen auf, die zuerst in [The Lean Startup](http://theleanstartup.com/book) von Eric Ries beschrieben wurden.
