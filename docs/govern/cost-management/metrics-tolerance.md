---
title: 'Cost Management: Risikotoleranzmetriken und -indikatoren'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um Cost Management-Risikotoleranzmetriken und -indikatoren im Zusammenhang mit der Cloudgovernance zu quantifizieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c44fc6974be69ff684089c65aa23da5eefbfd814
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708817"
---
# <a name="cost-management-metrics-indicators-and-risk-tolerance"></a>Metriken, Indikatoren und Risikotoleranz in der Kostenverwaltung

Dieser Artikel unterstützt Sie bei der Quantifizierung der Geschäftsrisikotoleranz im Zusammenhang mit der Kostenverwaltung. Das Definieren von Metriken und Indikatoren ermöglicht das Erstellen eines Geschäftsszenarios, mit dem Sie verstärkt auf die Ausgereiftheit der Disziplin der Kostenverwaltung setzen können.

## <a name="metrics"></a>Metriken

Die Kostenverwaltung befasst sich in der Regel mit Metriken im Zusammenhang mit Kosten. Im Rahmen der Risikoanalyse sollten Sie Daten zu Ihren aktuellen und geplanten Ausgaben für cloudbasierte Workloads sammeln, um zu ermitteln, wie hoch das Risiko ist und wie wichtig Investitionen in die Kostengovernance für Ihre Cloudeinführungsstrategie sind.

Es folgen Beispiele für nützliche Metriken, die Sie sammeln sollten, um die Risikotoleranz innerhalb der Kostenverwaltungsdisziplin zu bewerten:

- **Jährliche Ausgaben:** Die jährlichen Gesamtkosten für Dienste, die von einem Cloudanbieter bereitgestellt werden.
- **Monatliche Ausgaben:** Die monatlichen Gesamtkosten für Dienste, die von einem Cloudanbieter bereitgestellt werden.
- **Verhältnis zwischen Prognose und tatsächlichen Ausgaben:** Das Verhältnis zwischen den prognostizierten und den tatsächlichen Ausgaben (monatlich oder jährlich).
- **Verhältnis der Einführungsgeschwindigkeit (MOM):** Der Prozentsatz des Deltas zwischen den monatlichen Cloudkosten.
- **Akkumulierte Kosten:** Akkumulierte Ausgaben auf Tagesbasis ab Monatsbeginn.
- **Ausgabentrends:** Ausgabentrend in Relation zum Budget.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

In frühen kleineren Bereitstellungen, z.B. Dev/Test oder experimentellen ersten Workloads, ist die Kostenverwaltung wahrscheinlich mit vergleichsweise geringem Risiko verbunden. Wenn weitere Ressourcen bereitgestellt werden, steigt das Risiko, und die Toleranz im Unternehmens für Risiken nimmt wahrscheinlich ab. Darüber hinaus steigt das Risiko, und nimmt die Toleranz ab, wenn weitere Cloudeinführungsteams die Möglichkeit erhalten, Ressourcen in der Cloud zu konfigurieren oder bereitzustellen. Im Gegensatz dazu sind zum Erweitern einer Disziplin der Kostenverwaltung Personen aus der Cloudeinführungsphase erforderlich, die innovativere neue Technologien bereitstellen.

In den frühen Phasen der Cloudeinführung erarbeiten Sie zusammen mit Ihrem Unternehmen eine Baseline für Risikotoleranz. Nachdem Sie eine Basislinie haben, müssen Sie die Kriterien festlegen, die eine Investition in die Disziplin der Kostenverwaltung auslösen würden. Diese Kriterien sind wahrscheinlich für jede Organisation unterschiedlich.

Nachdem Sie [Geschäftsrisiken](./business-risks.md) ermittelt haben, identifizieren Sie gemeinsam mit dem Unternehmen Benchmarks, anhand derer Sie Auslöser identifizieren können, die diese Risiken potenziell erhöhen können. Es folgen einige Beispiele für den Vergleich von Metriken wie den oben genannten mit Ihrer Risikotoleranz-Baseline als Indikator, dass das Unternehmen weiter in die Kostenverwaltung investieren muss.

- **Engagementgesteuert (am häufigsten):** Ein Unternehmen, das sich vorgenommen hat, in diesem Jahr _x Mio. USD_ für einen Cloudanbieter auszugeben. Es erfordert eine Kostenverwaltungsdisziplin, um sicherzustellen, dass das Unternehmen seine Ausgabenziele nicht um mehr als 20 Prozent überschreitet und mindestens 90 Prozent dieser Vorgabe verwendet.
- **Prozentsatztrigger:** Ein Unternehmen mit Cloudausgaben, die für die Produktionssysteme stabil sind. Wenn sich dieser Wert um mehr als _x %_ ändert, ist eine Kostenverwaltungsdisziplin eine sinnvolle Investition.
- **Trigger bei Überdimensionierung:** Ein Unternehmen, das glaubt, dass die bereitgestellten Lösungen überdimensioniert sind. Kostenverwaltung ist eine Investition mit hoher Priorität, bis ein vernünftiger Abgleich zwischen Bereitstellung und Ressourcennutzung nachgewiesen wird.
- **Trigger bei monatlichen Ausgaben:** Ein Unternehmen, das monatlich mehr als _x Tausend USD_ ausgibt und dies als Kostenobergrenze ansieht. Wenn die Ausgaben diesen Betrag in einem bestimmten Monat übersteigen, muss eine Investition in Kostenverwaltung stattfinden.
- **Trigger bei jährlichen Ausgaben:** Ein Unternehmen mit einem Budget für IT-Forschung und -Entwicklung, das Ausgaben von _x Tausend USD_ pro Jahr für Cloudexperimente zulässt. Möglicherweise werden Produktionsworkloads in der Cloud ausgeführt, diese werden aber weiter als experimentelle Lösungen angesehen, wenn das Budget diesen Betrag nicht überschreitet. Wird das Budget überschritten, muss es als Produktionsinvestition behandelt werden, und Ausgaben müssen strikt überwacht werden.
- **Betriebskostenumkehrung (ungewöhnlich):** Das Unternehmen steht Betriebskosten sehr negativ gegenüber, und es müssen Kostenverwaltungskontrollen eingerichtet werden, bevor eine Dev/Test-Workload bereitgestellt werden kann.

## <a name="next-steps"></a>Nächste Schritte

Dokumentieren Sie mit der Vorlage [Cloudverwaltung](./template.md) die Metriken und Toleranzindikatoren, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Cost Management-Beispielrichtlinien als Ausgangspunkt für die Entwicklung von Richtlinien, die bestimmte Geschäftsrisiken behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
