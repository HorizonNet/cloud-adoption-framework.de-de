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
ms.openlocfilehash: be5cc97c7b42eb79f0ec9721376524dc2710e2c4
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683633"
---
# <a name="business-impact-in-cloud-management"></a>Die geschäftlichen Auswirkungen in der Cloudverwaltung

Gehen Sie vom Optimalzustand aus, aber bereiten Sie sich auf das Schlimmste vor. In der IT-Verwaltung müssen Sie davon ausgehen, dass die Workloads, die für die Unterstützung des Geschäftsbetriebs erforderlich sind, verfügbar sein und innerhalb der für die jeweilige Wichtigkeit vereinbarten Bedingungen funktionieren müssen. Um jedoch Investitionen vernünftig zu verwalten, müssen Sie genau wissen, welche Auswirkungen ein Ausfall oder eine verminderte Leistung auf die geschäftliche Seite haben. Diese Wichtigkeit wird in der folgenden Abbildung veranschaulicht, die potenzielle Geschäftsunterbrechungen bestimmter Workloads den geschäftlichen Auswirkungen von Ausfällen in einer relativen Werteskala zuordnet.

![Auswirkungen von Geschäftsunterbrechungen](../../_images/manage/time-value-impact.png)

Um eine solide Vergleichsbasis für die Auswirkungen auf verschiedene Workloads in einem Portfolio zu erhalten, empfiehlt sich die Verwendung einer Zeit-Wert-Metrik. Die Zeit-Wert-Metrik erfasst die negativen Auswirkungen eines Workloadausfalls. Im Allgemeinen werden diese Auswirkungen als direkter Umsatz- oder Betriebsertragsverlust während eines typischen Ausfallzeitraums erfasst. Genauer gesagt wird der Umsatzverlust für eine bestimmte Zeiteinheit berechnet. Die gängigste Zeit-Wert-Metrik ist „Auswirkung pro Stunde“, die Betriebsertragsverluste pro Ausfallstunde misst.

Es gibt verschiedene Verfahren zum Berechnen der Auswirkungen. Alle Optionen in den folgenden Abschnitten können mit ähnlichen Ergebnissen verwendet werden. Wichtig ist, dass beim Berechnen möglicher Verluste in einem Portfolio für jede Workload derselbe Ansatz verwendet wird.

## <a name="start-with-estimates"></a>Starten mit Schätzungen

Bei aktuellen Betriebsmodellen kann es schwierig sein, die genauen Auswirkungen zu bestimmen. Glücklicherweise ist nur für wenige Systeme eine sehr genaue Verlustberechnung notwendig. Im vorherigen Schritt: „Klassifizieren der Wichtigkeit“ wurde empfohlen, für alle Workloads zu Beginn einen Standardwert von „Mittlere Wichtigkeit“ festzulegen. Für Workloads mit mittlerer Wichtigkeit wird im Allgemeinen eine Standardstufe an Verwaltungsunterstützung mit relativ geringen Auswirkungen auf die Betriebskosten festgelegt. Nur wenn eine Workload zusätzliche Ressourcen für die operative Verwaltung erfordert, müssen die genauen finanziellen Auswirkungen ermittelt werden.

Bei allen standardisierten Workloads dienen die geschäftlichen Auswirkungen als Priorisierungsvariable bei der Wiederherstellung von Systemen nach einem Ausfall. Mit Ausnahme dieser Situationen erfordern die geschäftlichen Auswirkungen keine oder nur wenige Änderungen an der operativen Verwaltung. 

## <a name="calculating-time"></a>Berechnen der Zeit

Je nach Art der Workload können die Verluste unterschiedlich berechnet werden. Bei Hochleistungs-Transaktionssystemen wie z. B. Plattformen für den Echtzeithandel können Verluste im Millisekundenbereich bereits von Bedeutung sein. Andere Systeme – beispielsweise für Gehaltsabrechnungen – müssen nicht stündlich genutzt werden. Unabhängig davon, ob die Nutzungsfrequenz hoch oder niedrig ist, muss beim Berechnen der finanziellen Auswirkungen die Zeitvariable normalisiert werden.

## <a name="calculating-total-impact"></a>Berechnen der Auswirkungen insgesamt

Wenn zusätzliche Investitionen in die Verwaltung gewünscht sind, ist es wichtiger, die geschäftlichen Auswirkungen genau zu ermitteln. Die folgende Aufzählung beschreibt Ansätze für die Berechnung von Verlusten (von der genauesten zu der am wenigsten genauen):

- **Bereinigte Verluste**: Wenn im Unternehmen in der Vergangenheit bereits einmal ein Ereignis eingetreten ist, das zu massiven Verlusten führte – z. B. ein Wirbelsturm oder eine andere Naturkatastrophe –, wurden die tatsächlichen Verluste während des Ausfalls möglicherweise bereits berechnet. Diese Berechnungen basieren auf Normen der Versicherungsbranche für die Verlustberechnung und das Risikomanagement. Die Verwendung von bereinigten Verlusten als Gesamtverlustmenge in einem bestimmten Zeitrahmen kann zu sehr exakten Prognosen führen.

- **Verluste der Vergangenheit**: Wenn in der lokalen Umgebung früher aufgrund einer Instabilität der Infrastruktur Ausfälle aufgetreten sind, können Verluste etwas schwieriger zu berechnen sein. Die Bereinigungsformeln können intern jedoch weiterhin verwendet werden. Um Verluste der Vergangenheit zu berechnen, vergleichen Sie die Differenzen zwischen Umsatz, Bruttoeinnahmen und Betriebskosten für die Zeiträume vor, während und nach dem Ausfall. Durch Untersuchung dieser Deltawerte können genaue Verlustzahlen ermittelt werden, wenn keine anderen Daten verfügbar sind.

- **Berechnung des Gesamtverlustes**: Wenn keine früheren Daten verfügbar sind, kann ein Vergleichswert für Verluste abgeleitet werden. In diesem Modell ermitteln Sie die durchschnittlichen Bruttoeinnahmen pro Stunde für die Geschäftseinheit. Die Annahme, dass ein vollständiger Systemausfall einem 100 %igen Umsatzverlust entspricht, ist bei der Prognose von Investitionen zur Verlustvermeidung unzureichend. Diese Annahme kann jedoch als ungefähre Basis zum Vergleich der Auswirkungen von Verlusten und zur Priorisierung von Investitionen herangezogen werden.

Bevor Sie Vermutungen in Bezug auf Verlustberechnungen anstellen, arbeiten Sie mit der Finanzabteilung zusammen, um den besten Ansatz für die Berechnungen potenzieller Verluste in Zusammenhang mit einem Workloadausfall zu ermitteln.

## <a name="calculating-workload-impact"></a>Berechnen der Auswirkungen der Workloads

Wenn Sie zur Berechnung von Verlusten Daten der Vergangenheit heranziehen, sind möglicherweise genügend Informationen vorhanden, um die Auswirkungen jeder einzelnen Workload auf diese Verluste zu bestimmen. Diese Evaluierung ist ein Punkt, an dem eine enge Zusammenarbeit mit der geschäftlichen Seite absolut kritisch ist. Sobald die Auswirkungen insgesamt berechnet wurden, müssen diese den einzelnen Workloads zugeordnet werden. Diese Verteilung der Auswirkungen muss durch die geschäftlichen Beteiligten erfolgen, die sich auf die relativen und kumulierten Auswirkungen jeder Workload verständigen müssen. Darüber hinaus muss das Team die Geschäftsleitung um Feedback bitten, um die Ausrichtung zu überprüfen. Leider besteht das Endergebnis zumeist zu gleichen Teilen aus Emotionen und Fachkenntnissen. Diese Übung ist deswegen so wichtig, weil sie die Logik und die Überzeugungen der geschäftlichen Beteiligten repräsentiert, die bei der Budgetzuweisung ein Mitspracherecht haben sollten.

## <a name="using-the-template"></a>Verwenden der Vorlage

Die folgenden Schritte gelten für Leser, die die Arbeitsmappe [Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) verwenden, um die Cloudverwaltung zu planen.

1. Jede Workload auf den Blättern „Example“ oder „Clean Template“ sollte von geschäftlicher Seite mit dem „Time/Value Impact“ jeder Workload aktualisiert werden. Standardmäßig repräsentiert der Wert „Time/Value Impact“ die prognostizierten Verluste pro Stunde in Zusammenhang mit einem Ausfall der Workload.

## <a name="next-steps"></a>Nächste Schritte

Sobald die Auswirkungen definiert wurden, [können Zusagen ausgerichtet werden](./commitment.md).

> [!div class="nextstepaction"]
> [Ausrichten von Verwaltungszusagen am Geschäft](./commitment.md)
