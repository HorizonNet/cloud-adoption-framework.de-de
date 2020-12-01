---
title: Die geschäftlichen Auswirkungen in der Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die Auswirkungen ermitteln, die Ausfälle oder Leistungsbeeinträchtigungen auf Ihr Unternehmen haben können, und wie Sie sich damit vertraut machen können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e97f09727cb383f0092b1a23a170d963c7a16305
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879870"
---
# <a name="business-impact-in-cloud-management"></a>Die geschäftlichen Auswirkungen in der Cloudverwaltung

Gehen Sie vom Optimalzustand aus, aber bereiten Sie sich auf das Schlimmste vor. In der IT-Verwaltung müssen Sie davon ausgehen, dass die Workloads, die für die Unterstützung des Geschäftsbetriebs erforderlich sind, verfügbar sein und innerhalb der für die jeweilige Wichtigkeit vereinbarten Bedingungen funktionieren müssen. Um jedoch Investitionen vernünftig zu verwalten, müssen Sie genau wissen, welche Auswirkungen ein Ausfall oder eine verminderte Leistung auf die geschäftliche Seite haben. Diese Wichtigkeit wird in der folgenden Abbildung veranschaulicht, die potenzielle Geschäftsunterbrechungen bestimmter Workloads den geschäftlichen Auswirkungen von Ausfällen in einer relativen Werteskala zuordnet.

![Auswirkungen von Geschäftsunterbrechungen](../../_images/manage/time-value-impact.png)

Um eine solide Vergleichsbasis für die Auswirkungen auf verschiedene Workloads in einem Portfolio zu erhalten, empfiehlt sich die Verwendung einer Zeit-Wert-Metrik. Die Zeit-Wert-Metrik erfasst die negativen Auswirkungen eines Workloadausfalls. Im Allgemeinen werden diese Auswirkungen als direkter Umsatz- oder Betriebsertragsverlust während eines typischen Ausfallzeitraums erfasst. Genauer gesagt wird der Umsatzverlust für eine bestimmte Zeiteinheit berechnet. Die gängigste Zeit-Wert-Metrik ist _Auswirkung pro Stunde_, die Betriebsertragsverluste pro Ausfallstunde misst.

Es können einige Ansätze zur Berechnung der Auswirkungen verwendet werden. Sie können jede der Optionen in den folgenden Abschnitten anwenden, um ähnliche Ergebnisse zu erzielen. Es ist wichtig, für jeden Workload denselben Ansatz zu verwenden, wenn Sie mögliche Verluste in einem Portfolio berechnen.

## <a name="start-with-estimates"></a>Starten mit Schätzungen

Bei aktuellen Betriebsmodellen kann es schwierig sein, die genauen Auswirkungen zu bestimmen. Glücklicherweise ist nur für wenige Systeme eine sehr genaue Verlustberechnung notwendig. Im vorherigen Schritt _Klassifizieren der Wichtigkeit_ haben wir vorgeschlagen, dass Sie alle Workloads mit einer Voreinstellung von _Mittlere Wichtigkeit_ starten. Für Workloads mit mittlerer Wichtigkeit wird im Allgemeinen eine Standardstufe an Verwaltungsunterstützung mit relativ geringen Auswirkungen auf die Betriebskosten festgelegt. Nur wenn eine Workload zusätzliche Ressourcen für die operative Verwaltung erfordert, müssen die genauen finanziellen Auswirkungen ermittelt werden.

Bei allen standardisierten Workloads dienen die geschäftlichen Auswirkungen als Priorisierungsvariable bei der Wiederherstellung von Systemen nach einem Ausfall. Mit Ausnahme dieser Situationen erfordern die geschäftlichen Auswirkungen keine oder nur wenige Änderungen an der operativen Verwaltung.

## <a name="calculate-time"></a>Berechnen der Zeit

Je nach Art der Workload können Sie Verluste unterschiedlich berechnen. Bei Hochleistungs-Transaktionssystemen wie z. B. Plattformen für den Echtzeithandel können Verluste im Millisekundenbereich bereits von Bedeutung sein. Weniger häufig genutzte Systeme – z. B. für Gehaltsabrechnungen – müssen nicht stündlich genutzt werden. Unabhängig davon, ob die Nutzungsfrequenz hoch oder niedrig ist, muss beim Berechnen der finanziellen Auswirkungen die Zeitvariable normalisiert werden.

## <a name="calculate-total-impact"></a>Berechnen der Auswirkungen insgesamt

Wenn zusätzliche Investitionen in die Verwaltung berücksichtigt werden sollen, ist es wichtiger, die geschäftlichen Auswirkungen genau zu ermitteln. Bei den folgenden drei Ansätze zur Berechnung von Verlusten erfolgt die Sortierung vom genauesten zum am wenigsten genauen Ansatz:

- **Bereinigte Verluste**: Wenn in Ihrem Unternehmen in der Vergangenheit bereits einmal ein Ereignis eingetreten ist, das zu massiven Verlusten führte – z. B. ein Wirbelsturm oder eine andere Naturkatastrophe –, wurden die tatsächlichen Verluste während des Ausfalls möglicherweise bereits berechnet. Diese Berechnungen basieren auf Normen der Versicherungsbranche für die Verlustberechnung und das Risikomanagement. Die Verwendung von bereinigten Verlusten als Gesamtverlustmenge in einem bestimmten Zeitrahmen kann zu sehr exakten Prognosen führen.

- **Verluste der Vergangenheit**: Wenn in Ihrer lokalen Umgebung früher aufgrund einer Instabilität der Infrastruktur Ausfälle aufgetreten sind, können Verluste etwas schwieriger zu berechnen sein. Die Bereinigungsformeln können intern jedoch weiterhin angewendet werden. Um Verluste der Vergangenheit zu berechnen, vergleichen Sie die Differenzen zwischen Umsatz, Bruttoeinnahmen und Betriebskosten für die Zeiträume vor, während und nach dem Ausfall. Durch Untersuchung dieser Deltawerte können genaue Verlustzahlen ermittelt werden, wenn keine anderen Daten verfügbar sind.

- **Berechnung des Gesamtverlustes**: Wenn keine früheren Daten verfügbar sind, kann ein Vergleichswert für Verluste abgeleitet werden. In diesem Modell ermitteln Sie die durchschnittlichen Bruttoeinnahmen pro Stunde für die Geschäftseinheit. Wenn Sie Investitionen zur Verlustvermeidung planen, ist es nicht angemessen anzunehmen, dass ein kompletter Systemausfall einem 100-prozentigen Umsatzverlust entspricht. Sie können diese Annahme jedoch als ungefähre Basis zum Vergleich der Auswirkungen von Verlusten und zur Priorisierung von Investitionen heranziehen.

Bevor Sie bestimmte Annahmen über potenzielle Verluste im Zusammenhang mit Workloadausfällen treffen, ist es ratsam, mit Ihrer Finanzabteilung zusammenzuarbeiten, um den besten Ansatz für solche Berechnungen zu ermitteln.

## <a name="calculate-workload-impact"></a>Berechnen der Workloadauswirkungen

Wenn Sie Verluste durch die Anwendung historischer Daten berechnen, verfügen Sie möglicherweise über ausreichend Informationen, um den Beitrag jeder Workload zu diesen Verlusten eindeutig zu bestimmen. Bei der Durchführung dieser Bewertung sind Partnerschaften innerhalb des Unternehmens absolut entscheidend. Sobald die Auswirkungen insgesamt berechnet wurden, müssen diese den einzelnen Workloads zugeordnet werden. Diese Verteilung der Auswirkungen muss durch die geschäftlichen Beteiligten erfolgen, die sich auf die relativen und kumulierten Auswirkungen jeder Workload verständigen müssen. Zu diesem Zweck sollte Ihr Team Feedback von der Geschäftsleitung einholen, um die Ausrichtung zu überprüfen. Ein derartiges Feedback besteht zumeist zu gleichen Teilen aus Emotionen und Fachkenntnissen. Es ist wichtig, dass diese Übung die Logik und Überzeugungen der geschäftlichen Beteiligten widerspiegelt, die bei der Budgetzuweisung ein Mitspracherecht haben sollten.

## <a name="use-the-template"></a>Verwenden der Vorlage

Wenn Sie die Cloudverwaltung mithilfe der Vorlage [operationsmanagementworkbook](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) planen, sollten Sie Folgendes in Betracht ziehen:

- Jede Workload im Arbeitsblatt `Example` oder im Arbeitsblatt`Clean Template` sollte von geschäftlicher Seite mit dem Wert `Time/Value Impact` jeder Workload aktualisiert werden. Standardmäßig repräsentiert der Wert `Time/Value Impact` die prognostizierten Verluste pro Stunde in Zusammenhang mit einem Ausfall der Workload.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die geschäftliche Seite die Auswirkungen definiert hat, können Sie [Verpflichtungen ausrichten](./commitment.md).

> [!div class="nextstepaction"]
> [Ausrichten von Verwaltungszusagen am Geschäft](./commitment.md)
