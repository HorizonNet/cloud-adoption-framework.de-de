---
title: 'Geschäftliche Wichtigkeit: Cloudverwaltung und -betrieb'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Geschäftliche Wichtigkeit: Cloudverwaltung und -betrieb'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 290fcf7093f128c1415bbf960d65074d12490ae1
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683647"
---
# <a name="business-criticality-in-cloud-management"></a>Geschäftliche Wichtigkeit der Cloudverwaltung

In jedem Unternehmen gibt es eine kleine Anzahl von Workloads, die so wichtig sind, dass sie nicht ausfallen dürfen. Wenn bei diesen Workloads Ausfälle oder Leistungsbeeinträchtigungen auftreten, sind die negativen Auswirkungen auf Umsatz und Rentabilität im gesamten Unternehmen zu spüren. Diese Workloads werden als unternehmenskritisch betrachtet.

Am anderen Ende des Spektrums gibt es einige Workloads, die monatelang nicht verwendet werden. Ausfälle oder Leistungseinbußen solcher Workloads sind zwar nicht wünschenswert, aber die Auswirkungen sind isoliert und begrenzt.

Eine genaue Kenntnis der Wichtigkeit jeder Workload im IT-Portfolio ist der erste Schritt auf dem Weg zu gegenseitigen Zusagen für die Cloudverwaltung.
Die Abbildung unten veranschaulicht eine allgemeine Ausrichtung zwischen der zu befolgenden Wichtigkeitsskala und den Standardzusagen der geschäftlichen Seite.

![Ausrichtung zwischen Wichtigkeit und Verwaltungsebene](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Wichtigkeitsskala

Der erste Schritt bei jedem Projekt zur Ausrichtung an der geschäftlichen Wichtigkeit ist die Erstellung einer Wichtigkeitsskala. Im Folgenden finden Sie eine Beispielskala, die Sie als Referenz oder Vorlage für Ihre eigene Skala verwenden können.

|Wichtigkeit  |Geschäftliche Sicht  |
|---------|---------|
|Unternehmenskritisch|Wirkt sich auf das Kerngeschäft des Unternehmens aus und kann auf die Gewinn- und Verlustrechnung des Unternehmens merklich beeinträchtigen.|
|Kritisch für Geschäftseinheit|Wirkt sich auf den Kern einer bestimmten Geschäftseinheit und deren Gewinn- und Verlustrechnung aus.|
|Hoch|Behindert die Kernaufgaben möglicherweise nicht, wirkt sich aber auf Prozesse mit hoher Wichtigkeit aus. Bei Ausfällen können messbare Verluste ermittelt werden.|
|Mittel|Auswirkungen auf Prozess sind wahrscheinlich. Verluste sind gering oder nicht messbar, aber eine Schädigung der Marke oder Verluste bei vorgelagerten Prozessen sind wahrscheinlich.|
|Niedrig|Die Auswirkungen auf Geschäftsprozesse sind nicht messbar. Weder eine Schädigung der Marke noch Verluste bei vorgelagerten Prozessen sind wahrscheinlich. Lokal begrenzte Auswirkungen auf ein einzelnes Team sind wahrscheinlich.|
|Nicht unterstützt|Kein geschäftlicher Besitzer, kein Team und kein Prozess im Zusammenhang mit dieser Workload kann eine Investition in die weitere Verwaltung der Workload rechtfertigen.|

Die meisten Unternehmen nutzen zusätzliche Klassifizierungen der Wichtigkeit speziell für eine Branche, einen vertikalen Markt oder bestimmte Geschäftsprozesse. Hierbei kann es sich beispielsweise um folgende Klassifizierungen handeln:

- **Compliancekritisch**: In stark regulierten Branchen sind einige Workloads möglicherweise kritisch, weil sie zur Erfüllung von Complianceanforderungen erforderlich sind.
- **Kritisch im Hinblick auf die Datensicherheit**: Einige Workloads sind möglicherweise nicht unternehmenskritisch, aber Ausfälle können zu Datenverlusten oder unbeabsichtigtem Zugriffen auf geschützte Informationen führen.
- **Kritisch im Hinblick auf die Betriebssicherheit**: Wenn während eines Ausfalls die physische Sicherheit oder sogar das Leben von Mitarbeitern und Kunden gefährdet ist, sollten entsprechende Workloads als kritisch im Hinblick auf die Betriebssicherheit klassifiziert werden.

## <a name="importance-of-accurate-criticality"></a>Die richtige Einstufung der Wichtigkeit

Später in diesem Prozess wird das Cloudverwaltungsteam diese Klassifizierung verwenden, um den Aufwand zu ermitteln, der erforderlich ist, um die Anforderungen der verschiedenen Wichtigkeitsstufen zu erfüllen. In lokalen Umgebungen wird die operative Verwaltung häufig zentral eingekauft und als notwendige geschäftliche Belastung ohne oder mit nur wenig zusätzlichen Betriebskosten behandelt. In der Cloud wird die operative Verwaltung (wie alle Komponenten in der Cloud) pro Ressource als monatliche Betriebskosten erworben.

Da es in der Cloud eine klare und direkte Beziehung zwischen Kosten und operativem Betrieb gibt, ist es wichtig, die Kosten und die gewünschten Wichtigkeitsskalen richtig auszurichten.

## <a name="select-a-default-criticality"></a>Auswählen der standardmäßigen Wichtigkeit

Eine anfängliche Überprüfung jeder Workload im Portfolio kann sehr zeitaufwendig sein. Um sicherzustellen, dass diese Aufgabe nicht die gesamte Cloudstrategie blockiert, empfiehlt es sich, eine standardmäßige Wichtigkeit zu vereinbaren, die auf alle Workload anzuwenden ist.

Basierend auf der oben gezeigten Wichtigkeitsskala wird die Wichtigkeit „Mittel“ als Standardwert empfohlen. So kann das Cloudstrategieteam schnell Workloads ermitteln, die eine höhere Wichtigkeitsstufe erfordern.

## <a name="using-the-template"></a>Verwenden der Vorlage

Die folgenden Schritte gelten für Leser, die die Arbeitsmappe [Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) verwenden, um die Cloudverwaltung zu planen.

1. Die Wichtigkeitsskala kann auf dem Blatt „Scale“ der Arbeitsmappe erfasst werden.
2. Jede Workload auf den Blättern „Example“ oder „Clean Template“ sollte aktualisiert werden, um die standardmäßige Wichtigkeit in der Spalte „Criticality“ wiederzugeben.
3. Die richtigen Werte müssen von geschäftlicher Seite eingegeben werden, damit Abweichungen von der standardmäßigen Wichtigkeit aufgenommen werden.

## <a name="next-steps"></a>Nächste Schritte

Sobald die Wichtigkeit definiert wurde, müssen [geschäftliche Auswirkungen berechnet und aufgezeichnet](./impact.md) werden.

> [!div class="nextstepaction"]
> [Berechnen und Aufzeichnen von geschäftlichen Auswirkungen](./impact.md)
