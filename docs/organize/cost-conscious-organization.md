---
title: Schaffen einer kostenbewussten Organisation
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie etwas über bewährte Methoden zum Schaffen einer kostenbewussten Organisation.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.openlocfilehash: 6c01ec344d6c02fa9c576e5e674b8fddf59849fe
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566817"
---
# <a name="build-a-cost-conscious-organization"></a>Schaffen einer kostenbewussten Organisation

Wie unter [Beweggründe: Warum steigen wir auf die Cloud um?](../strategy/motivations.md) beschrieben, gibt es für ein Unternehmen viele gute Gründe für den Einsatz der Cloud. Wenn die Kostenreduzierung eine wichtige Rolle spielt, ist es wichtig, eine kostenbewusste Organisation zu schaffen.

Die Sicherstellung von Kostenbewusstsein ist keine einmalige Aktion. Wie auch bei allen anderen Bereichen der Cloudeinführung handelt es sich um einen iterativen Prozess. Im folgenden Diagramm ist dieser Prozess anhand von drei Aktivitäten dargestellt, die voneinander abhängig sind: *Transparenz*, *Zurechenbarkeit* und *Optimierung*. Diese Prozesse spielen sich auf Makro- und Mikroebenen ab. Dies wird in diesem Artikel ausführlich beschrieben.

![Prozess für Kostenbewusstsein](../_images/ready/cost-optimization-process.png)
*Abbildung 1 – Organisation des kostenbewussten Unternehmens.*

## <a name="general-cost-conscious-processes"></a>Allgemeine Prozesse für Kostenbewusstsein

- **Transparenz:** Um für eine Organisation Kostenbewusstsein zu erzielen, muss ein transparenter Einblick in die Kosten möglich sein. Zum Erzielen von Transparenz in einer kostenbewussten Organisation ist eine konsistente Berichterstellung für die Teams, die an der Cloudeinführung arbeiten, die Finanzteams, die die Budgets verwalten, und die Managementteams, die für die Kosten verantwortlich sind, erforderlich. Diese Transparenz wird erreicht, indem Folgendes festgelegt wird:
  - Der richtige Berichtsbereich
  - Ordnungsgemäße Ressourcenorganisation (Verwaltungsgruppen, Ressourcengruppen, Abonnements)
  - Klare Kennzeichnungsstrategien
  - Geeignete Zugriffssteuerung (RBAC)

- **Zurechenbarkeit:** Die Zurechenbarkeit ist genau so wichtig wie die Transparenz. Die Zurechenbarkeit beginnt mit eindeutigen Budgets für alle Maßnahmen der Cloudeinführung. Budgets sollten klar festgelegt und eindeutig kommuniziert werden und auf realistischen Erwartungen basieren. Für Zurechenbarkeit sind ein iterativer Prozess und ein „dynamisches Selbstbild“ (Growth Mindset) erforderlich, um das richtige Maß an Zurechenbarkeit zu erreichen.

- **Optimierung:** Bei der Optimierung werden Kosteneinsparungen erzielt. Während der Optimierung werden die Ressourcenzuordnungen geändert, um die Kosten von verschiedenen unterstützenden Workloads zu senken. Für diesen Prozess sind Iterationen und Experimentiervorgänge erforderlich. Mit jeder Reduzierung der Kosten verringert sich die Leistung. Für die Ermittlung der richtigen Balance zwischen der Kostenkontrolle und der gewünschten Endbenutzerleistung werden unter Umständen Beiträge mehrerer Parteien benötigt.

In den folgenden Abschnitten werden die Rollen beschrieben, die das *Cloudstrategieteam*, *Cloudeinführungsteam*, *Cloudgovernanceteam* und *Cloudkompetenzzentrum* (CCoE) jeweils bei der Entwicklung einer kostenbewussten Organisation spielen.

## <a name="cloud-strategy-team"></a>Cloudstrategieteam

Die Integration von Kostenbewusstsein in die Maßnahmen zur Cloudeinführung beginnt auf der Führungsebene. Zum Erzielen von langfristiger Effektivität sollte das [Cloudstrategieteam](./cloud-strategy.md) ein Mitglied des Finanzteams enthalten. Wenn laut Finanzstruktur Manager aus dem betriebswirtschaftlichen Bereich für die Lösungskosten verantwortlich sind, sollten sie auch zur Teilnahme im Team eingeladen werden. Zusätzlich zu den Kernaktivitäten, die dem Cloudstrategieteam normalerweise zugewiesen werden, sollten alle Mitglieder des Cloudstrategieteams auch für die folgenden Aktivitäten verantwortlich sein:

- **Transparenz:** Das Cloudstrategieteam und das [Cloudgovernanceteam](./cloud-governance.md) müssen die tatsächlichen Kosten des Umstiegs auf die Cloud kennen. Da dieses Team auf der Führungsebene angesiedelt ist, sollte es über Zugriff auf mehrere Kostenbereiche für die Analyse der Ausgabenentscheidungen verfügen. Normalerweise benötigt eine Führungskraft transparenten Einblick in die Gesamtkosten, die sich als Summe aller Cloudausgaben ergeben. Als aktives Mitglied des Cloudstrategieteams sollten aber auch die Kosten pro Geschäfts- oder Abrechnungseinheit einsehbar sein, damit Showback, Chargeback oder andere [Modelle für die Cloudabrechnung](../strategy/cloud-accounting.md) überprüft werden können.

- **Zurechenbarkeit:** Die Budgets sollten zusammen vom Cloudstrategie-, [Cloudgovernance-](./cloud-governance.md) und [Cloudeinführungsteam](./cloud-adoption.md) basierend auf den erwarteten Einführungsaktivitäten aufgestellt werden. Wenn es zu Budgetabweichungen kommt, müssen das Cloudstrategieteam und das Cloudgovernanceteam gemeinsam daran arbeiten, schnell die beste Vorgehensweise zu ermitteln, um diese Abweichungen zu beseitigen.

- **Optimierung:** Während der Optimierungsmaßnahmen kann das Cloudstrategieteam den Investitions- und Renditewert von bestimmten Workloads darstellen. Falls eine Workload für das Unternehmen einen strategischen Nutzen oder finanzielle Auswirkungen hat, sollten die Maßnahmen für die Kostenoptimierung sorgfältig überwacht werden. Wenn es keine strategischen Auswirkungen auf die Organisation und keine inhärenten Kosten für eine schlechte Leistung einer Workload gibt, kann das Cloudstrategieteam die Überoptimierung genehmigen. Um diese Entscheidungen zu treffen, muss das Team in der Lage sein, die Kosten pro Projektbereich anzuzeigen.

## <a name="cloud-adoption-team"></a>Cloudeinführungsteam

Das [Cloudeinführungsteam](./cloud-adoption.md) steht im Mittelpunkt aller Einführungsaktivitäten. Es fungiert daher als erste Kontrollstelle in Bezug auf Mehrkosten. Dieses Team spielt in allen drei Phasen des Bereichs „Kostenbewusstsein“ eine aktive Rolle.

- **Transparenz:**

  - **Bewusstsein:** Es ist wichtig, dass das Cloudeinführungsteam über transparenten Einblick in die jeweils angestrebten Kosteneinsparungsziele verfügt. Wenn einfach nur verkündet wird, dass die Cloudeinführung eine Reduzierung der Kosten bewirkt, ist der Prozess zum Scheitern verurteilt. Es ist wichtig, dass eine *spezifische* Transparenz sichergestellt ist. Wenn das Ziel beispielsweise darin besteht, die Gesamtkosten des Datencenters um 3 Prozent zu reduzieren oder die jährlichen Betriebskosten um 7 Prozent zu senken, sollten Sie diese Ziele rechtzeitig und deutlich kommunizieren.
  - **Telemetrie:** Dieses Team benötigt Einblicke in die Auswirkungen ihrer Entscheidungen. Während der Migrations- oder Innovationsaktivitäten haben von diesem Team getroffene Entscheidungen direkten Einfluss auf Kosten und Leistung. Das Team muss für diese beiden konkurrierenden Faktoren eine Balance erzielen. Eine angemessene Leistungsüberwachung und Kostenüberwachung in Bezug auf die aktiven Projekte des Teams ist wichtig, um die erforderliche Transparenz zu schaffen.

- **Zurechenbarkeit:** Das Cloudeinführungsteam muss über alle vorab festgelegten Budgets informiert sein, die für die Einführungsmaßnahmen gelten. Wenn die tatsächlichen Kosten nicht am Budget ausgerichtet sind, besteht die Möglichkeit, für Zurechenbarkeit zu sorgen. Bei Zurechenbarkeit geht es nicht darum, das Einführungsteam für die Überschreitung des Budgets zu bestrafen, da diese Überschreitung auch das Ergebnis notwendiger Entscheidungen im Hinblick auf die Leistung sein kann. Vielmehr bedeutet Zurechenbarkeit, das Team über die Ziele zu informieren und aufzuzeigen, wie sich seine Entscheidungen auf diese Ziele auswirken. Darüber hinaus wird durch die Zurechenbarkeit ein Dialog mit dem Team ermöglicht, damit es die Entscheidungen erläutern kann, die zu den Mehrkosten geführt haben. Falls diese Entscheidungen nicht am Ziel des Projekts ausgerichtet sind, ist dies eine gute Gelegenheit, mit dem Cloudstrategieteam zusammenzuarbeiten, um bessere Entscheidungen zu treffen.

- **Optimierung:** Diese Aufgabe kann zu einem Balanceakt werden, da durch die Optimierung der Ressourcen gleichzeitig die Leistung der von ihnen unterstützten Workloads reduziert wird. Manchmal können antizipierte oder budgetierte Einsparungen für eine Workload nicht realisiert werden, weil die Workload mit den budgetierten Ressourcen keine adäquate Leistung aufweist. In diesen Fällen muss das Cloudeinführungsteam die richtigen Entscheidungen treffen und diese Änderungen dem Cloudstrategieteam und dem Cloudgovernanceteam melden, damit die Budgets oder die Optimierungsentscheidungen korrigiert werden können.

## <a name="cloud-governance-team"></a>Cloudgovernanceteam

Im Allgemeinen ist das [Cloudgovernanceteam](./cloud-governance.md) für die Kostenverwaltung aller Maßnahmen für die Cloudeinführung verantwortlich. Wie im Thema zur [Disziplin „Kostenverwaltung“](../govern/cost-management/index.md) in der Governance-Methodik des Frameworks für die Cloudeinführung (Cloud Adoption Framework) beschrieben, ist die Kostenverwaltung die erste der fünf Disziplinen der Cloudgovernance. In diesen Artikeln werden einige tiefer gehende Zuständigkeiten für das Cloudgovernanceteam beschrieben.

Diese Bestrebungen konzentrieren sich auf die folgenden Aktivitäten im Zusammenhang mit der Entwicklung einer kostenbewussten Organisation:

- **Transparenz:** Das Cloudgovernanceteam arbeitet bei der Planung der Budgets für die Cloudeinführung gleichberechtigt mit dem Cloudstrategieteam zusammen. Außerdem arbeiten diese beiden Teams zusammen an der regelmäßigen Überprüfung der tatsächlichen Ausgaben. Es ist die Aufgabe des Cloudgovernanceteams Teams sicherzustellen, dass eine einheitliche, zuverlässige Kostenberichterstattung durchgeführt wird und Telemetriedaten zur Leistung erhoben werden.

- **Zurechenbarkeit:** Wenn es zu Budgetabweichungen kommt, müssen das Cloudstrategieteam und das Cloudgovernanceteam gemeinsam daran arbeiten, schnell die beste Vorgehensweise zu ermitteln, um diese Abweichungen zu beseitigen. Normalerweise werden diese Entscheidungen vom Cloudgovernanceteam umgesetzt. Manchmal reicht ggf. eine einfache erneute Schulung des betroffenen [Cloudeinführungsteams](./cloud-adoption.md) aus. Das Cloudgovernanceteam kann sich auch an der Optimierung der bereitgestellten Ressourcen, der Änderung von Rabattoptionen oder auch der Implementierung von automatisierten Optionen für die Kostenkontrolle beteiligen, z.B. einer Blockade der Bereitstellung von ungeplanten Ressourcen.

- **Optimierung:** Nachdem Ressourcen in die Cloud migriert oder in dieser erstellt wurden, können Sie Überwachungstools nutzen, um die Leistung und Nutzung dieser Ressourcen zu bewerten. Durch geeignete Überwachungsmaßnahmen und Leistungsdaten können Ressourcen identifiziert werden, die optimiert werden sollten. Das Cloudgovernanceteam muss sicherstellen, dass die Tools für Überwachung und Kostenberichterstattung konsistent bereitgestellt werden. Die Mitglieder des Teams können auch die Einführungsteams dabei unterstützen, Möglichkeiten zu ermitteln, wie basierend auf Telemetriedaten zur Leistung und zu den Kosten eine Optimierung erzielt werden kann.

## <a name="cloud-center-of-excellence"></a>Cloudkompetenzzentrum

Das CCoE ist zwar normalerweise nicht für die Kostenverwaltung verantwortlich, aber es kann erheblichen Einfluss auf kostenbewusste Organisationen haben. Viele grundlegende IT-Entscheidungen wirken sich in größerem Maße auf die Kosten. Wenn das CCoE seine Aufgaben erfüllt, können diese Kosten für die Maßnahmen zur Cloudeinführung reduziert werden.

- **Transparenz:** Jede Verwaltungs- oder Ressourcengruppe, die über wichtige IT-Ressourcen verfügt, sollte für das CCoE-Team sichtbar sein. Das Team kann diese Daten nutzen, um Möglichkeiten zur Optimierung zusammenzufassen.

- **Zurechenbarkeit:** Das Cloudkompetenzzentrum ist zwar normalerweise nicht für die Kosten zuständig, aber es kann sich selbst die Aufgabe stellen, wiederholbare Lösungen zu schaffen, mit denen die Kosten reduziert werden und die Leistung gesteigert wird.

- **Optimierung:** Da das Cloudkompetenzzentrum über Einblick in mehrere Bereitstellungen verfügt, befindet sich das Team in einer optimalen Position, Tipps für die Optimierung vorzuschlagen und Einführungsteams bei der besseren Optimierung von Ressourcen zu unterstützen.

## <a name="next-steps"></a>Nächste Schritte

Wenn diese Aufgaben auf den einzelnen Unternehmensebenen erledigt werden, wird die Schaffung einer kostenbewussten Organisation gefördert. Sie können basierend auf diesem Leitfaden aktiv werden, indem Sie die [Einführung in die Bereitschaft von Organisationen](./index.md) lesen. Darin erhalten Sie Hilfe beim Identifizieren der richtigen Teamstrukturen.

> [!div class="nextstepaction"]
> [Identifizieren der richtigen Teamstrukturen](./index.md)
