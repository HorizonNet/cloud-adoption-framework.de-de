---
title: Evaluieren der Risikotoleranz
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erläuterung der geschäftlichen Risiken bei einer Cloudtransformation
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 2b8bc595377b2748bd00f306659a46196115e91d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223539"
---
# <a name="evaluate-risk-tolerance"></a>Evaluieren der Risikotoleranz

Jede Geschäftsentscheidung führt zu neuen Risiken. Jede Investition in beliebigen Bereichen bringt ein Verlustrisiko mit sich. Neue Produkte oder Dienste bergen das Risiko eines Marktversagens. Durch Änderungen an aktuellen Produkten oder Diensten kann sich der Marktanteil verringern. Die Cloudtransformation ist keine Wunderlösung für die alltäglichen Geschäftsrisiken. Im Gegenteil – durch verbundene Lösungen (Cloud oder lokal) werden neue Risiken eingeführt. Die Bereitstellung von Ressourcen für mit dem Netzwerk verbundene Einrichtungen erweitert zudem das Profil potenzieller Bedrohungen, indem Sicherheitslücken einer viel größeren, globalen Community zugänglich gemacht werden. Glücklicherweise sind Cloudanbieter mit den geänderten, erhöhten und zusätzlichen Risiken vertraut. Sie investieren in hohem Maße in die Minderung und Bewältigung dieser Risiken im Interesse ihrer Kunden.

Dieser Artikel beschäftigt sich nicht vorrangig mit Cloudrisiken. Er befasst sich vielmehr mit den geschäftlichen Risiken, die mit den verschiedenen Formen der Cloudtransformation in Zusammenhang stehen. Im weiteren Verlauf dieses Artikels verlagert sich der Fokus auf die Diskussion von Möglichkeiten zum Verstehen der Risikotoleranz des Unternehmens.

<!-- markdownlint-disable MD026 -->

## <a name="what-business-risks-are-associated-with-a-cloud-transformation"></a>Welche geschäftlichen Risiken sind mit einer Cloudtransformation verbunden?

Echte Geschäftsrisiken basieren auf den Details spezifischer Transformationen. Mehrere gängige Risiken bieten einen Einstieg in das Gespräch, um unternehmensspezifische Risiken zu verstehen.

> [!IMPORTANT]
> Bevor Sie weiterlesen, sollten Sie wissen, dass jedes dieser Risiken entschärft werden kann. Ziel dieses Artikels ist es, die Leser zu informieren und auf produktivere Diskussionen zum Risikomanagement vorzubereiten.

- **Verletzung des Schutzes personenbezogener Daten:** Das Risiko Nummer 1 im Zusammenhang mit jeder Transformation ist der Schutz von Daten. Datenlecks in Ihrem Unternehmen können erhebliche Schäden verursachen, die zum Verlust von Kunden, zu Geschäftseinbrüchen oder sogar zur gesetzlichen Haftung führen. Alle Änderungen an der Speicherung, Verarbeitung oder Verwendung der Daten stellen ein Risiko dar. Cloudtransformationen sorgen für umfangreiche Änderungen im Bereich der Datenverwaltung, daher sollte das Risiko nicht auf die leichte Schulter genommen werden. [Sicherheitbaseline](../security-baseline/index.md), [Datenklassifizierung](./data-classification.md) und [inkrementelle Rationalisierung](../../digital-estate/rationalize.md#incremental-rationalization) können bei der Bewältigung dieses Risikos hilfreich sein.

- **Dienstunterbrechung:** Geschäftsvorgänge und Kundenerlebnis hängen stark von technischen Vorgängen ab. Cloudtransformationen führen zu Änderungen in IT-Vorgängen. In einigen Organisationen ist die Veränderung gering und leicht anzupassen. In anderen Organisationen sind für diese Änderungen möglicherweise neue Tools, neues Fachwissen oder neue Ansätze für die Unterstützung von Cloudvorgängen erforderlich. Je umfangreicher die Änderung, desto größer die potenziellen Auswirkungen auf Geschäftsvorgänge und das Kundenerlebnis. Zur Bewältigung dieses Risikos müssen die Fachbereiche in die Transformationsplanung einbezogen werden. Die Abschnitte „Releaseplanung“ und „Auswählen der ersten Workload“ im Artikel [Inkrementelle Rationalisierung](../../digital-estate/rationalize.md#incremental-rationalization) erörtern Möglichkeiten zur Auswahl von Workloads für Transformationsprojekte. Das Unternehmen muss bei dieser Aktivität das Risiko für Geschäftsvorgänge kommunizieren, das von der Änderung priorisierter Workloads ausgeht. Wird die IT bei der Auswahl von Workloads unterstützt, die geringere Auswirkungen auf Vorgänge haben, verringert sich das Gesamtrisiko.

- **Budgetkontrolle:** In der Cloud verändern sich die Kostenmodelle. Diese Änderung kann zu Risiken im Zusammenhang mit Kostenüberschreitungen oder erhöhten Kosten für verkaufte Waren führen, insbesondere bei direkt damit verbundenen Betriebsausgaben. Wenn das Unternehmen eng mit der IT zusammenarbeitet, ist es möglich, in Bezug auf die Kosten und die von verschiedenen Geschäftseinheiten, Programmen oder Projekten genutzten Dienste für Transparenz zu sorgen. Unter [Cost Management](../cost-management/index.md) finden Sie Beispiele für eine mögliche Zusammenarbeit zwischen Unternehmen und IT in diesem Bereich.

Oben sind einige der gängigsten von Kunden genannten Risiken aufgeführt. Das Cloudgovernanceteam und die Cloudeinführungsteams können mit der Entwicklung eines Risikoprofils beginnen, während Workloads migriert und für den Einsatz in der Produktion vorbereitet werden. Richten Sie sich auf Gespräche ein, um Risiken basierend auf dem gewünschten Geschäftsergebnis und Transformationsaufwand zu definieren, zu präzisieren und in den Griff zu bekommen.

## <a name="understanding-risk-tolerance"></a>Verstehen der Risikotoleranz

Die Identifikation von Risiken ist ein relativ direkter Prozess. IT-bezogene Risiken sind in der Regel branchenübergreifend identisch. Die Toleranz für diese Risiken ist jedoch spezifisch für jede Organisation. An diesem Punkt laufen Gespräche zwischen Unternehmen und IT tendenziell auseinander. Die beiden Gesprächspartner sprechen im Wesentlichen eine andere Sprache. Die folgenden Vergleiche und Fragen sollen als Einstieg für Diskussionen dienen, die es beiden Parteien ermöglichen, die Risikobereitschaft besser zu verstehen und einzuschätzen.

## <a name="simple-use-case-for-comparison"></a>Einfacher Anwendungsfall zum Vergleich

Um die Risikotoleranz zu verstehen, untersuchen wir die Kundendaten. Wenn ein Unternehmen in einer beliebigen Branche Kundendaten auf einem ungesicherten Server ablegt, bleibt das technische Risiko, ob diese Daten kompromittiert oder gestohlen werden, mehr oder weniger gleich. Wie ein Unternehmen dieses Risiko jedoch toleriert, hängt stark von Art und potenziellem Wert der Daten ab.

- Unternehmen im Gesundheits- und Finanzwesen in den Vereinigten Staaten unterliegen strikten Konformitätsanforderungen von Drittanbietern. Es wird vorausgesetzt, dass personenbezogene Daten sowie gesundheitsbezogene Daten extrem vertraulich zu behandeln sind. Für diese Arten von Unternehmen gibt es schwerwiegende Konsequenzen, wenn sie an dem oben beschriebenen Risikoszenario beteiligt sind. Ihre Toleranz wird dementsprechend extrem gering sein. Alle innerhalb oder außerhalb des Netzwerks veröffentlichten Kundendaten müssen durch diese Drittanbieter-Konformitätsrichtlinien verwaltet werden.
- Ein Spieleunternehmen, dessen Kundendaten sich auf Benutzernamen, Spielzeiten und Bestenlisten beschränken, muss abgesehen von einem Imageschaden wahrscheinlich keine schwerwiegenden Folgen befürchten, wenn es das oben beschriebene riskante Verhalten an den Tag legt. Ungeschützte Daten sind zwar gefährdet, die Auswirkungen sind jedoch gering. Daher ist die Risikotoleranz in diesem Fall hoch.
- Ein mittelständisches Unternehmen, das Tausenden von Kunden einen Teppichreinigungsdienst anbietet, fällt zwischen diese beiden Toleranzextreme. Kundendaten sind möglicherweise ausführlicher und enthalten Details wie Adresse oder Telefonnummer. Beide können als personenbezogene Informationen betrachtet werden, die zu schützen sind. Allerdings gibt es möglicherweise keine spezifische Governanceanforderung, die vorschreibt, dass die Daten abgesichert werden müssen. Aus der IT-Perspektive ist die Antwort einfach: Die Daten müssen geschützt werden. Aus geschäftlicher Sicht ist die Sache möglicherweise nicht so einfach. Das Unternehmen benötigt weitere Details, bevor es ein Maß an Toleranz für dieses Risiko ermitteln kann.

Der nächste Abschnitt enthält einige Beispielfragen, anhand derer das Unternehmen ein Maß an Risikotoleranz für den obigen und andere Anwendungsfälle festlegen kann.

## <a name="risk-tolerance-questions"></a>Fragen zur Risikotoleranz

In diesem Abschnitt werden Fragen mit Gesprächsbedarf in drei Kategorien aufgelistet: Wahrscheinlichkeit von Datenverlust, Auswirkung von Datenverlust und Kosten für die Wiederherstellung. Wenn Fachbereiche und IT sich gemeinsam mit diesen Bereichen befassen, kann die Entscheidung, den Aufwand für das Risikomanagement und die allgemeine Toleranz gegenüber einem bestimmten Risiko zu erhöhen, mühelos getroffen werden.

**Auswirkungen von Datenverlust:** Fragen zum Ermitteln der Auswirkungen eines Risikos. Diese Fragen können schwer zu beantworten sein. Ideal ist es, die Auswirkungen in Zahlen auszudrücken, aber oft reicht die Diskussion allein bereits aus, um die Risikotoleranz zu verstehen. Auch Spannen sind zulässig, insbesondere dann, wenn sie mit den Annahmen präsentiert werden, anhand derer sie ermittelt wurden.

- Verstößt dieses Risiko möglicherweise gegen Drittanbieter-Konformitätsanforderungen?
- Verstößt dieses Risiko möglicherweise gegen interne Unternehmensrichtlinien?
- Kann dieses Risiko eine Gefahr für Leib und Leben darstellen oder zu Sachschäden führen?
- Kann dieses Risiko Kunden oder Marktanteile kosten? Falls ja, sind diese Kosten quantifizierbar?
- Kann dieses Risiko zu negativen Kundenerlebnissen führen? Beeinträchtigen diese Erlebnisse ggf. den Absatz oder Umsatz?
- Kann dieses Risiko eine gesetzliche Haftung herbeiführen? Falls ja, gibt es hierfür einen Präzendenzfall für zu leistenden Schadenersatz?
- Können die Geschäftsvorgänge durch dieses Risiko zum Erliegen kommen? Falls ja, wie lang wäre der Betriebsausfall?
- Kann dieses Risiko die Geschäftsvorgänge verlangsamen? Falls ja, inwieweit und für wie lange?
- Ist dieses Risiko zu diesem Zeitpunkt in der Transformation einmalig, oder kann es sich wiederholen?
- Nimmt die Häufigkeit des Risikos im Verlauf der Transformation zu oder ab?
- Nimmt die Wahrscheinlichkeit des Risikos im Laufe der Zeit zu oder ab?
- Ist das Risiko von der Natur her zeitkritisch? Geht das Risiko vorüber, oder wird es schlimmer, wenn es nicht behandelt wird?

Diese grundlegenden Fragen führen zu vielen weiteren Fragen. Nachdem Sie einen konstruktiven Dialog geführt haben, wird empfohlen, die relevanten Risiken aufzuzeichnen und nach Möglichkeit zu beziffern.

**Kosten für die Wiederherstellung:** Fragen zum Ermitteln der Kosten zur Beseitigung oder sonstigen Minimierung des Risikos. Diese Fragen können sehr direkt sein, insbesondere, wenn sie geballt präsentiert werden.

- Gibt es eine klare Lösung, und was kostet sie?
- Gibt es Möglichkeiten, dieses Risiko zu vermeiden oder zu minimieren? In welchem Bereich liegen die Kosten für diese Lösungen?
- Was wird vom Unternehmen benötigt, um eine optimale, klare Lösung auswählen zu können?
- Was wird vom Unternehmen benötigt, um die Kosten zu überprüfen?
- Welche weiteren Vorteile können sich aus der Lösung ergeben, die dieses Risiko beseitigt?

Diese Fragen vereinfachen die technischen Lösungen zu sehr, die für das Management oder die Beseitigung von Risiken erforderlich sind. Die Fragen kommunizieren diese Lösungen jedoch in einer Weise, die dem Unternehmen einen schnellen Einstieg in den Entscheidungsprozess ermöglicht.

**Wahrscheinlichkeit von Datenverlusten:** Fragen zum Ermitteln der Wahrscheinlichkeit, dass der Risikofall eintritt. Dieser Bereich ist am schwierigsten zu beziffern. Stattdessen wird empfohlen, das Cloudgovernanceteam basierend auf den zugrunde liegenden Daten Kategorien festlegen zu lassen, mit deren Hilfe die Wahrscheinlichkeit vermittelt werden kann. Die folgenden Fragen können beim Erstellen von für das Team sinnvollen Kategorien hilfreich sein.

- Wurden in Bezug auf die Wahrscheinlichkeit, dass dieses Risiko eintritt, Recherchen betrieben?
- Kann der Anbieter Referenzen oder Statistiken zur Wahrscheinlichkeit der Auswirkungen vorlegen?
- Gibt es andere Unternehmen im relevanten Sektor oder in der entsprechenden Branche, die von diesem Risiko betroffen waren?
- Gibt es allgemein andere Unternehmen, die von diesem Risiko betroffen waren?
- Ist dieses Risiko einzigartig und bezieht sich nur auf etwas, das in diesem Unternehmen mangelhaft gehandhabt wurde?

Nach Beantwortung dieser und weiterer Fragen nach Ermessen des Cloudgovernanceteams werden sich voraussichtlich Wahrscheinlichkeitsgruppen herauskristallisieren. Im Folgenden werden einige Gruppierungsbeispiele für den Einstieg aufgeführt:

- **Keine Anhaltspunkte:** Es gab noch nicht genügend Untersuchungen, um die Wahrscheinlichkeit zu ermitteln.
- **Geringes Risiko:** Aktuelle Untersuchungen deuten darauf hin, dass es unwahrscheinlich ist, dass das Risiko eintritt.
- **Zukünftiges Risiko:** Die aktuelle Wahrscheinlichkeit ist gering. Bei fortgesetzter Einführung wäre jedoch eine neue Analyse erforderlich.
- **Mittleres Risiko:** Es ist wahrscheinlich, dass sich das Risiko auf das Unternehmen auswirkt.
- **Hohes Risiko:** Im Lauf der Zeit wird es zunehmend wahrscheinlicher, dass das Unternehmen dieses Risiko eingeht.
- **Abnehmendes Risiko:** Das Risiko ist mittel bis hoch. Die Wahrscheinlichkeit von Auswirkungen lässt sich jedoch durch Maßnahmen in der IT oder im Unternehmen reduzieren.

**Ermitteln der Toleranz:**

Die drei oben aufgeführten Fragengruppen sollten genügend Stoff zum Ermitteln der anfänglichen Toleranzen bieten. Wenn Risiko und Wahrscheinlichkeit niedrig und die Kosten zur Risikominderung hoch sind, wird das Unternehmen kaum in die Risikominderung investieren. Sind Risiko und Wahrscheinlichkeit hoch, wird das Unternehmen sicherlich eine Investition erwägen, solange die Kosten nicht die potenziellen Risiken überschreiten.

## <a name="next-steps"></a>Nächste Schritte

Diese Art des Gesprächs kann Unternehmen und IT dabei unterstützen, die Toleranz effektiver auszuwerten. Dialoge dieser Art können während der Erstellung von MVP-Richtlinien und bei inkrementellen Richtlinienüberprüfungen geführt werden.

> [!div class="nextstepaction"]
> [Unternehmensrichtlinie definieren](./policy-definition.md)
