---
title: Erzielen eines Konsenses hinsichtlich des Geschäftswerts von Innovationen
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Sie im Hinblick auf den Geschäftswert von Cloudinnovationen einen Konsens bei den Definitionen der Projektbeteiligten erzielen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: f93b0a643a5751f4090a82a0688b1ed1073533e1
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86449471"
---
# <a name="build-consensus-on-the-business-value-of-innovation"></a>Erzielen eines Konsenses zum Geschäftswert der Cloudinnovation

Der erste Schritt bei der Entwicklung einer neuen Innovation besteht darin, herauszufinden, wie diese Innovation für einen geschäftlichen Wert sorgen kann. In dieser Übung beantworten Sie eine Reihe von Fragen, die die Bedeutung der Investition von ausreichend Zeit hervorheben, wenn Ihr Unternehmen den Geschäftswert definiert.

## <a name="qualifying-questions"></a>Fragen zur Einstufung

Bevor Sie eine Lösung entwickeln (in der Cloud oder lokal), überprüfen Sie Ihre Kriterien für den Geschäftswert, indem Sie die folgenden Fragen beantworten:

1. Welche definierte Kundenanforderung soll mit dieser Lösung erfüllt werden?
1. Welche Verkaufschancen schafft diese Lösung für Ihr Unternehmen?
1. Welche Geschäftsergebnisse lassen sich mit dieser Lösung erzielen?
1. Welcher der Beweggründe Ihres Unternehmens wäre mit dieser Lösung erfüllt?

Wenn die Antworten auf alle vier Fragen sorgfältig dokumentiert sind, müssen Sie den Rest dieser Übung wahrscheinlich nicht durcharbeiten. Glücklicherweise können Sie jede Dokumentation problemlos testen. Richten Sie zwei kurze Besprechungen ein, um sowohl die Dokumentation als auch die interne Ausrichtung Ihres Unternehmens zu testen. Laden Sie engagierte Beteiligte im Unternehmen zu einer Besprechung ein, und vereinbaren Sie eine separate Besprechung mit dem beteiligten Entwicklungsteam. Stellen Sie jeder Gruppe die vier oben aufgeführten Fragen, und vergleichen Sie dann die Ergebnisse.

> [!NOTE]
> Die vorhandene Dokumentation sollte vor der jeweiligen Besprechung **nicht** an die Teams weitergegeben werden. Wenn die richtige Ausrichtung vorhanden ist, sollten die grundlegenden Hypothesen von Mitgliedern beider Gruppen beschrieben oder sogar zitiert werden können.

<!-- -->

> [!WARNING]
> Machen Sie die Besprechung nicht einfacher. Dieser Test dient dazu, die Ausrichtung zu bestimmen. Es handelt sich nicht um eine Übung zur Erstellung einer Ausrichtung. Erinnern Sie zu Beginn der Besprechung die Teilnehmer, dass das Ziel das Testen der Ausrichtung an vorhandenen Übereinkünften innerhalb des Teams sein soll. Legen Sie für jede Frage ein Zeitlimit von fünf Minuten fest. Setzten Sie einen Timer, und schließen Sie jede Frage nach fünf Minuten ab, auch wenn sich die Teilnehmer nicht auf eine Antwort geeinigt haben.

Berücksichtigen Sie die verschiedenen Sprachen und Interessen der einzelnen Gruppen. Wenn der Test zu Antworten führt, die auf die richtige Ausrichtung hinweisen, betrachten Sie diese Übung als Erfolg. Sie sind bereit, zur Lösungsentwicklung überzugehen.

Wenn ein oder zwei Antworten auf die richtige Ausrichtung hinweisen, freuen Sie sich, dass sich Ihre harte Arbeit auszahlt. Die Ausrichtung in Ihrem Unternehmen ist besser als in den meisten anderen. Ein zukünftiger Erfolg ist wahrscheinlich, allerdings sind noch geringfügige Investitionen in die Ausrichtung erforderlich. Lesen Sie die folgenden Abschnitte, um Ideen zu entwickeln, die Ihnen bei der weiteren Förderung der Ausrichtung helfen.

Wenn eins der Teams in 30 Minuten keine der vier Fragen beantworten konnte, werden die Ausrichtung und die Überlegungen in den folgenden Abschnitten wahrscheinlich einen erheblichen Einfluss auf diese und andere Bemühungen haben. Lesen Sie die folgenden Abschnitte sorgfältig.

<!-- docsTest:ignore "Strategy, Plan, Ready, and Adopt" -->

## <a name="address-the-big-picture-first"></a>Zuerst das große Ganze

Das Cloud Adoption Framework folgt einem vorgeschriebenen Pfad mit vier Phasen: Strategie, Planung, Bereitschaft und Einführung. Cloudinnovationen sind der Einführungsphase dieses Prozesses zuzuordnen. Die Antworten auf die [qualifizierenden Fragen](#qualifying-questions) drei und vier betreffen Ergebnisse und Beweggründe. Wenn diese Antworten nicht passen, deutet dies darauf hin, dass Ihr Unternehmen in der Strategiephase des Lebenszyklus der Cloudeinführung etwas vergessen hat. Hierbei kommen verschiedene der folgenden Szenarien in Frage.

- **Chance: Ausrichtung**: Wenn geschäftliche Beteiligte sich nicht auf Beweggründe und Geschäftsergebnisse in Bezug auf ein Cloudinnovationsprojekt einigen können, ist dies ein Symptom für eine größere Herausforderung. Die Übungen in der [Strategiemethodik](../strategy/index.md) können hilfreich sein, um eine Ausrichtung der geschäftlichen Beteiligten zu erreichen. Darüber hinaus empfiehlt es sich dringend, dass dieselben Beteiligten ein [Cloudstrategieteam](../organize/cloud-strategy.md) bilden, das sich regelmäßig trifft.

- **Chance: Kommunikation**: Wenn das Entwicklungsteam sich nicht auf Beweggründe und Geschäftsergebnisse einigen kann, kann dies ein Symptom für Lücken in der strategischen Kommunikation sein. Dieses Problem lässt sich durch eine Überprüfung der Cloudstrategie mit dem Cloudeinführungsteam schnell beseitigen. Einige Wochen nach dieser Überprüfung sollte das Team die Einstufungsfragen erneut beantworten.

- **Chance: Priorisierung**: Eine Cloudstrategie ist im Grunde eine Hypothese auf Führungsebene. Die besten Cloudstrategien sind offen für Iterationen und Feedback. Wenn beide Teams die Strategie verstehen, aber dennoch keine übereinstimmenden Antworten auf diese Fragen finden, sind möglicherweise die Prioritäten nicht richtig ausgerichtet. Organisieren Sie eine Sitzung mit dem Cloudeinführungsteam und dem Cloudstrategieteam. Diese Sitzung kann die Bemühungen beider Gruppen erleichtern. Das Cloudeinführungsteam beginnt damit, dass es seine ausgerichteten Antworten auf die qualifizierenden Fragen teilt. Von dort aus kann ein Gespräch zwischen den beiden Teams Chancen für eine bessere Ausrichtung der Prioritäten eröffnen.

Solche Besprechungen zeigen häufig Möglichkeiten auf, die innovative Lösung besser an der Cloudstrategie auszurichten. Diese Übung zeitigt in der Regel zwei Ergebnisse:

- Diese Gespräche können Ihrem Team helfen, die Cloudstrategie Ihres Unternehmens zu verbessern und wichtige Kundenanforderungen besser darzustellen. Eine solche Veränderung kann mehr Unterstützung für Ihr Team durch die Geschäftsleitung bedeuten.
- Umgekehrt können diese Gespräche zeigen, dass Ihr Cloudeinführungsteam in eine andere Lösung investieren sollte. Erwägen Sie in diesem Fall eine Migration dieser Lösung, bevor Sie weiter in Innovationen investieren. Alternativ können diese Gespräche darauf hindeuten, dass ein Ansatz mit Entwicklern ohne Programmiererfahrung (Citizen Developers) erforderlich ist, um zuerst den Geschäftswert zu testen. In beiden Fällen wird Ihr Team davor bewahrt, umfangreiche Investitionen zu tätigen, die nur eine geringfügige geschäftliche Rendite einbringen.

## <a name="address-solution-alignment"></a>Ausrichten von Lösungen

Es ist ziemlich üblich, dass die Antworten auf die Fragen 1 und 2 falsch ausgerichtet sind. In den frühen Phasen der Ideenfindung und Entwicklung sind Kundenanforderungen und geschäftliche Chancen oft nicht aneinander ausgerichtet. Das richtige Gleichgewicht zwischen zu viel und zu wenig Definition zu finden, ist für viele Entwicklungsteams eine Herausforderung. Im Framework für die Cloudeinführung werden Ansätze mit geringem Aufwand wie z. B. Erstellen-Messen-Lernen-Feedbackschleifen als Antworten auf diese Fragen empfohlen. Die folgende Liste zeigt Chancen und Ansätze zum Schaffen der richtigen Ausrichtung.

- **Chance: Hypothese**: Es geschieht häufig, dass verschiedene Beteiligte und Entwicklungsteams von einer Lösung zu viel erwarten. Unrealistische Erwartungen können ein Zeichen dafür sein, dass die Hypothese zu ungenau ist. Sehen Sie sich den Leitfaden [Erstellen mit Blick auf die Kundenanforderungen](./considerations/build.md) an, um eine klarere Hypothese zu formulieren.
- **Chance: Erstellen**: Teams können falsch ausgerichtet sein, weil sie sich auf dem Weg zur Lösung der Kundenanforderungen nicht einig sind. Eine solche Meinungsverschiedenheit deutet typischerweise darauf hin, dass das Team durch eine [vorzeitige technische Herausforderung aufgehalten wird](./considerations/build.md#reduce-complexity-and-delay-technical-spikes). Um die Fokussierung des Teams auf den Kunden sicherzustellen, beginnen Sie mit der ersten Iteration und erstellen ein kleines MVP (Minimum Viable Product), um eine Teil der Hypothese anzugehen. Weitere Informationen dazu, wie Sie das Team unterstützen können, finden Sie unter [Entwickeln digitaler Erfindungen](./considerations/invention.md).
- **Chance: Schulungen**: Beide Teams können falsch ausgerichtet sein, weil sie umfassende technische Anforderungen und funktionale Voraussetzungen benötigen. Diese Notwendigkeit kann zu einer Möglichkeit zum Training in flexiblen Methoden führen. Wenn die Teamkultur noch nicht für flexible Prozesse bereit ist, kann es schwierig werden, Innovationen zu schaffen und mit dem Markt Schritt zu halten. Schulungsressourcen zu DevOps und agilen Methoden finden Sie hier:
  - [Weiterentwickeln Ihrer DevOps-Methoden](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)
  - [Erstellen von Anwendungen mit Azure DevOps](https://docs.microsoft.com/learn/paths/build-applications-with-azure-devops)
  - [Bereitstellen von Anwendungen mit Azure DevOps](https://docs.microsoft.com/learn/paths/deploy-applications-with-azure-devops)

Durch Befolgen dieser Methodik und mithilfe der Tools zur Behandlung von Rückständen in den einzelnen Abschnitten dieses Artikels, lässt sich die richtige Ausrichtung für Lösungen erzielen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie den Geschäftswert ermittelt und kommuniziert haben, sind Sie bereit, mit der Erstellung der Lösung zu beginnen.

> [!div class="nextstepaction"]
> [Zurück zu den Übungen zu Innovationen](./index.md)
