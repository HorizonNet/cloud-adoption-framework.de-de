---
title: Risikotoleranzmetriken und -indikatoren in der Disziplin „Kostenverwaltung“
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um Risikotoleranzmetriken und -indikatoren für Kostenverwaltung (Cost Management) in der Cloudgovernance zu quantifizieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a50a03096aad4dd492fc86e574aa7e335c5b178f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220514"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-cost-management-discipline"></a>Risikotoleranzmetriken und -indikatoren in der Disziplin „Kostenverwaltung“

Hier erfahren Sie, wie die Risikotoleranz von Unternehmen im Zusammenhang mit der Disziplin „Kostenverwaltung“ (Cost Management) quantifiziert wird. Durch das Definieren von Metriken und Indikatoren können Sie ein Geschäftsszenario erstellen, um in die Ausgereiftheit dieser Disziplin zu investieren.

## <a name="metrics"></a>Metriken

Die Kostenverwaltung befasst sich normalerweise mit Metriken im Zusammenhang mit Kosten. Im Rahmen der Risikoanalyse sollten Sie Daten zu Ihren aktuellen und geplanten Ausgaben für cloudbasierte Workloads sammeln, um zu ermitteln, wie hoch das Risiko ist und wie wichtig Investitionen in Ihre Disziplin „Kostenverwaltung“ für Ihre geplanten Cloudbereitstellungen sind.

Es folgen Beispiele für nützliche Metriken, die Sie sammeln sollten, um die Risikotoleranz innerhalb der Kostenverwaltungsdisziplin zu bewerten:

- **Jährliche Ausgaben:** Die jährlichen Gesamtkosten für Dienste, die von einem Cloudanbieter bereitgestellt werden.
- **Monatliche Ausgaben:** Die monatlichen Gesamtkosten für Dienste, die von einem Cloudanbieter bereitgestellt werden.
- **Verhältnis zwischen Prognose und tatsächlichen Ausgaben:** Das Verhältnis zwischen den prognostizierten und den tatsächlichen Ausgaben (monatlich oder jährlich).
- **Verhältnis der Einführungsgeschwindigkeit (zwischen zwei Monaten):** Der Prozentsatz des Deltas zwischen den monatlichen Cloudkosten.
- **Akkumulierte Kosten:** Akkumulierte Ausgaben auf Tagesbasis ab Monatsbeginn.
- **Ausgabentrends:** Ausgabentrend in Relation zum Budget.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

In frühen kleineren Bereitstellungen, z. B. Dev/Test oder experimentellen ersten Workloads, ist die Kostenverwaltung wahrscheinlich mit vergleichsweise geringem Risiko verbunden. Wenn weitere Ressourcen bereitgestellt werden, steigt das Risiko, und die Risikotoleranz des Unternehmens nimmt wahrscheinlich ab. Darüber hinaus steigt das Risiko, und nimmt die Toleranz ab, wenn weitere Cloudeinführungsteams die Möglichkeit erhalten, Ressourcen in der Cloud zu konfigurieren oder bereitzustellen. Im Gegensatz dazu sind für die Entwicklung einer Disziplin vom Typ „Kostenverwaltung“ Personen aus der Cloudeinführungsphase erforderlich, um innovativere Technologien bereitzustellen.

In den frühen Phasen der Cloudeinführung erarbeiten Sie zusammen mit Ihrem Unternehmen eine Baseline für Risikotoleranz. Nachdem Sie eine Basislinie haben, müssen Sie die Kriterien festlegen, die eine Investition in die Disziplin der Kostenverwaltung auslösen würden. Diese Kriterien sind wahrscheinlich für jede Organisation unterschiedlich.

Nachdem Sie [Geschäftsrisiken](./business-risks.md) ermittelt haben, identifizieren Sie gemeinsam mit dem Unternehmen Benchmarks, anhand derer Sie Auslöser identifizieren können, die diese Risiken potenziell erhöhen können. Es folgen einige Beispiele für den Vergleich von Metriken wie den oben genannten mit Ihrer Risikotoleranz-Baseline als Indikator, dass das Unternehmen weiter in die Kostenverwaltung investieren muss.

- **Engagementgesteuert (am häufigsten):** Ein Unternehmen, das sich vorgenommen hat, in diesem Jahr _x Mio. USD_ für einen Cloudanbieter auszugeben. Es erfordert eine Kostenverwaltungsdisziplin, um sicherzustellen, dass das Unternehmen seine Ausgabenziele nicht um mehr als 20 Prozent überschreitet und mindestens 90 Prozent dieser Vorgabe verwendet.
- **Prozentsatztrigger:** Ein Unternehmen mit Cloudausgaben, die für die Produktionssysteme stabil sind. Wenn sich dieser Wert um mehr als _x %_ ändert, ist eine Kostenverwaltungsdisziplin eine sinnvolle Investition.
- **Trigger bei Überdimensionierung:** Ein Unternehmen, das glaubt, dass die bereitgestellten Lösungen überdimensioniert sind. Kostenverwaltung ist so lange eine Investition mit hoher Priorität, bis ein vernünftiger Abgleich zwischen Bereitstellung und Ressourcennutzung nachgewiesen wird.
- **Trigger bei monatlichen Ausgaben:** Ein Unternehmen, das monatlich mehr als _x Tausend USD_ ausgibt und dies als Kostenobergrenze ansieht. Wenn die Ausgaben diesen Betrag in einem bestimmten Monat übersteigen, muss eine Investition in die Kostenverwaltung erfolgen.
- **Trigger bei jährlichen Ausgaben:** Ein Unternehmen mit einem Budget für IT-Forschung und -Entwicklung, das Ausgaben von _x Tausend USD_ pro Jahr für Cloudexperimente zulässt. Möglicherweise werden Produktionsworkloads in der Cloud ausgeführt, diese werden aber weiter als experimentelle Lösungen angesehen, wenn das Budget diesen Betrag nicht überschreitet. Wird das Budget überschritten, muss es als Produktionsinvestition behandelt werden, und Ausgaben müssen strikt überwacht werden.
- **Betriebskostenumkehrung (ungewöhnlich):** Das Unternehmen steht Betriebskosten sehr negativ gegenüber, und es müssen Kostenverwaltungskontrollen eingerichtet werden, bevor eine Dev/Test-Workload bereitgestellt werden kann.

## <a name="next-steps"></a>Nächste Schritte

Dokumentieren Sie mit der [Richtlinienvorlage „Kostenverwaltung“](./template.md) die Metriken und Toleranzindikatoren, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Beispielrichtlinien für Kostenverwaltung als Ausgangspunkt für die Entwicklung Ihrer eigenen Richtlinien, um bestimmte Geschäftsrisiken zu behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
