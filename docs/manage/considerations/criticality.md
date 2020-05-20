---
title: Geschäftliche Wichtigkeit der Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit der kritischen Bedeutung von Workloads vertraut zu machen und negative Auswirkungen auf Umsatz und Rentabilität zu verhindern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2114b212718adb22b190f854de665e0d59fa50a4
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83398458"
---
# <a name="business-criticality-in-cloud-management"></a>Geschäftliche Wichtigkeit der Cloudverwaltung

In jedem Unternehmen gibt es eine kleine Anzahl von Workloads, die so wichtig sind, dass sie nicht ausfallen dürfen. Diese Workloads gelten als unternehmenskritisch. Wenn bei diesen Workloads Ausfälle oder Leistungsbeeinträchtigungen auftreten, sind die negativen Auswirkungen auf Umsatz und Rentabilität im gesamten Unternehmen zu spüren.

Am anderen Ende des Spektrums gibt es einige Workloads, die monatelang nicht verwendet werden. Ausfälle oder Leistungseinbußen solcher Workloads sind zwar nicht wünschenswert, aber die Auswirkungen sind isoliert und begrenzt.

Eine genaue Kenntnis der Wichtigkeit jeder Workload im IT-Portfolio ist der erste Schritt auf dem Weg zu gegenseitigen Zusagen für die Cloudverwaltung.
Das folgende Diagramm veranschaulicht eine allgemeine Ausrichtung zwischen der zu befolgenden Wichtigkeitsskala und den Standardzusagen der geschäftlichen Seite.

![Ausrichtung zwischen Wichtigkeit und Verwaltungsebene](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Wichtigkeitsskala

Der erste Schritt bei jedem Projekt zur Ausrichtung an der geschäftlichen Wichtigkeit ist die Erstellung einer Wichtigkeitsskala. In der folgenden Tabelle finden Sie eine Beispielskala, die als Referenz oder Vorlage für die Erstellung Ihrer eigenen Skala verwendet werden kann.

| Wichtigkeit | Geschäftliche Sicht |
| --------- | --------- |
| Unternehmenskritisch |  Wirkt sich auf das Kerngeschäft des Unternehmens aus und kann auf die Gewinn- und Verlustrechnung des Unternehmens merklich beeinflussen. |
| Einheitenkritisch | Wirkt sich auf das Kerngeschäft einer bestimmten Geschäftseinheit und deren Gewinn- und Verlustrechnung aus. |
| High | Behindert die Kernaufgaben möglicherweise nicht, wirkt sich aber auf Prozesse mit hoher Wichtigkeit aus. Bei Ausfällen können messbare Verluste ermittelt werden. |
| Medium | Auswirkungen auf die Prozesse sind wahrscheinlich. Verluste sind gering oder nicht messbar, aber eine Schädigung der Marke oder Verluste bei vorgelagerten Prozessen sind wahrscheinlich. |
| Niedrig | Die Auswirkungen auf die Geschäftsprozesse sind nicht messbar. Weder eine Schädigung der Marke noch Verluste bei vorgelagerten Prozessen sind wahrscheinlich. Lokal begrenzte Auswirkungen auf ein einzelnes Team sind wahrscheinlich. |
| Nicht unterstützt | Kein geschäftlicher Besitzer, kein Team und kein Prozess im Zusammenhang mit dieser Workload kann eine Investition in die weitere Verwaltung der Workload rechtfertigen. |

Die meisten Unternehmen nutzen zusätzliche Klassifizierungen der Wichtigkeit, die für ihre Branche spezifisch sind, einen vertikalen Markt oder bestimmte Geschäftsprozesse. Hierbei kann es sich beispielsweise um folgende Klassifizierungen handeln:

- **Compliancekritisch**: In stark regulierten Branchen sind einige Workloads möglicherweise kritisch, weil sie zur Erfüllung von Complianceanforderungen erforderlich sind.
- **Kritisch im Hinblick auf die Datensicherheit**: Einige Workloads sind möglicherweise nicht unternehmenskritisch, aber Ausfälle können zu Datenverlusten oder unbeabsichtigtem Zugriffen auf geschützte Informationen führen.
- **Kritisch im Hinblick auf die Betriebssicherheit**: Wenn während eines Ausfalls die physische Sicherheit oder sogar das Leben von Mitarbeitern und Kunden gefährdet ist, sollten entsprechende Workloads als kritisch im Hinblick auf die Betriebssicherheit klassifiziert werden.

## <a name="importance-of-accurate-criticality"></a>Die richtige Einstufung der Wichtigkeit

Später in diesem Cloudeinführungsprozess wird das Cloudverwaltungsteam diese Klassifizierung verwenden, um den Aufwand zu ermitteln, der erforderlich ist, um die Anforderungen der verschiedenen Wichtigkeitsstufen zu erfüllen. In lokalen Umgebungen wird die operative Verwaltung häufig zentral eingekauft und als notwendige geschäftliche Belastung ohne oder mit nur wenig zusätzlichen Betriebskosten behandelt. In der Cloud wird die operative Verwaltung (wie alle Komponenten in der Cloud) pro Ressource als monatliche Betriebskosten erworben.

Da es in der Cloud eine klare und direkte Beziehung zwischen Kosten und operativem Betrieb gibt, ist es wichtig, die Kosten und die gewünschten Wichtigkeitsskalen richtig auszurichten.

## <a name="select-a-default-criticality"></a>Auswählen der standardmäßigen Wichtigkeit

Eine anfängliche Überprüfung jeder Workload im Portfolio kann sehr zeitaufwendig sein. Um sicherzustellen, dass diese Aufgabe nicht ihre gesamte Cloudstrategie blockiert, empfiehlt es sich, dass ihre Teams eine standardmäßige Wichtigkeit vereinbaren, die auf alle Workloads anzuwenden ist.

Basierend auf der vorhergehenden Tabelle der Wichtigkeitsskala empfehlen wir Ihnen, die _mittlere_ Wichtigkeit als Standard zu übernehmen. So kann Ihr Cloudstrategieteam schnell Workloads ermitteln, die eine höhere Wichtigkeitsstufe erfordern.

## <a name="use-the-template"></a>Verwenden der Vorlage

Die folgenden Schritte gelten, wenn Sie die Arbeitsmappe [Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) verwenden, um die Cloudverwaltung zu planen.

1. Erfassen Sie die Wichtigkeitsskala auf der Registerkarte **Scale** der Arbeitsmappe.
2. Aktualisieren Sie jede Workload auf den Blättern _Example_ oder _Clean Template_, um die standardmäßige Wichtigkeit in der Spalte _Criticality_ wiederzugeben.
3. Das Unternehmen sollte die richtigen Werte eingeben, um Abweichungen von der standardmäßigen Wichtigkeit widerzuspiegeln.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Ihr Team die geschäftliche Bedeutung definiert hat, können Sie die [geschäftlichen Auswirkungen berechnen und aufzeichnen](./impact.md).

> [!div class="nextstepaction"]
> [Berechnen und Aufzeichnen von geschäftlichen Auswirkungen](./impact.md)
