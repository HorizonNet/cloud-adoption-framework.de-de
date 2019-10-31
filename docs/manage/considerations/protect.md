---
title: 'Schutz und Wiederherstellung: Cloudverwaltung und -betrieb'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Schutz und Wiederherstellung: Cloudverwaltung und -betrieb'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2e055cb6105b9424259d2b8e86bdde7d64798479
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682449"
---
# <a name="protect-and-recover-in-cloud-management"></a>Schutz und Wiederherstellung in der Cloudverwaltung

Sobald die Anforderungen an [Bestand und Transparenz](./inventory.md) und [Betriebskonformität](./operational-compliance.md) erfüllt sind, können die Cloudverwaltungsteams für die Zukunft planen und sich auf potenzielle Ausfälle einer Workload vorbereiten. Beim Planen der Cloudverwaltung muss das Team mit der Annahme beginnen, dass etwas ausfällt.

Keine technische Lösung kann konsistent eine SLA mit 100 % Betriebszeit bieten. Lösungen mit Architekturen mit einem Höchstmaß an Redundanz nehmen für sich in Anspruch, Betriebszeiten mit „sechs Neunen“, also 99,9999 % zu bieten. Aber selbst eine Lösung mit „sechs Neunen“ fällt jedes Jahr durchschnittlich 31,6 Sekunden lang aus. Und leider rechtfertigen Lösungen selten die umfangreichen, kontinuierlichen Investitionen, die vonnöten sind, um eine Betriebszeit mit „sechs Neunen“ zu erzielen.

Wenn Teams sich auf Ausfälle vorbereiten, können sie Fehler schneller erkennen und den Betrieb in kürzerer Zeit wiederherstellen. In der vorliegenden Disziplin geht es um die Schritte, die nach einem Systemausfall ausgeführt werden müssen. Wie schützen Sie Workloads, sodass sie nach einem Ausfall schnell wiederhergestellt werden können?

## <a name="translating-protection-and-recovery-conversations"></a>Übersetzen von Gesprächen zum Thema Schutz und Wiederherstellung

Die Workloads, auf denen der Geschäftsbetrieb basiert, bestehen aus Anwendungen, Daten, virtuellen Computern und anderen Ressourcen. Möglicherweise erfordert jede dieser Ressource einen anderen Ansatz in Bezug auf Schutz und Wiederherstellung. Der wichtigste Aspekt dieser Disziplin ist es, konsistente Zusagen in Bezug auf die Verwaltungsbaseline zu treffen, um eine Ausgangsbasis für geschäftsbezogene Gespräche zu schaffen.

Als Mindestanforderung sollte für jede Ressource, die eine bestimmte Workload unterstützt, eine Baseline mit eindeutigen Zusagen in Bezug auf die Geschwindigkeit einer Wiederherstellung (Recovery Time Objective, RTO) oder das Risiko von Datenverlusten (Recovery Point Objective, RPO) festgelegt werden.

### <a name="recovery-time-objectives-rto"></a>Recovery Time Objective (RTO)

Wenn der Ernstfall eintritt, ist die RTO die Zeitspanne, die benötigt wird, um ein bestimmtes System auf seinen Zustand vor dem Ausfall wiederherzustellen. Dies umfasst für jede Workload die Zeit, die notwendig ist, um eine Mindestfunktionalität für die VMs und Apps wiederherzustellen. Dazu gehört auch die Zeit, die notwendig ist, um die von den Anwendungen benötigten Daten wiederherzustellen.

Aus geschäftlicher Sicht stellt die RTO den Zeitraum dar, in dem der Geschäftsprozess außer Betrieb ist. Bei unternehmenskritischen Workloads sollte diese Variable relativ niedrig sein, damit die Geschäftsprozesse schnell fortgesetzt werden können. Bei Workloads mit geringerer Priorität hat eine Standard-RTO möglicherweise keine nennenswerten Auswirkungen auf die Gesamtleistung des Unternehmens.

Die Verwaltungsbaseline sollte eine Standard-RTO für nicht unternehmenskritische Workloads festlegen. Aus geschäftlicher Sicht kann diese Baseline dann dazu dienen, zusätzliche Investitionen in Wiederherstellungszeiten zu rechtfertigen.

### <a name="recovery-point-objectives-rpo"></a>Recovery Point Objective (RPO)

In den meisten Cloudverwaltungssystemen werden Daten durch irgendeine Form des Datenschutzes in regelmäßigen Abständen erfasst und gespeichert. Der letzte Zeitpunkt, zu dem Daten erfasst wurden, wird als Wiederherstellungspunkt bezeichnet. Wenn ein System ausfällt, kann es nur auf den jüngsten Wiederherstellungspunkt wiederhergestellt werden.

Wenn für ein System eine RPO von mehreren Stunden oder sogar Tagen festgelegt wurde, würde ein Systemausfall dazu führen, dass alle Daten zwischen dem letzten Wiederherstellungspunkt und dem Ausfall verloren sind. Eine RPO von einem Tag würde theoretisch zum Verlust sämtlicher Transaktionen an diesem Tag bis zum Ausfall führen.

Bei unternehmenskritischen Systemen ist daher eine RPO in einer Größenordnung von einigen Minuten oder Sekunden wahrscheinlich besser geeignet, um Umsatzverluste zu vermeiden. Eine kürzere RPO führt im Allgemeinen aber auch zu einer Erhöhung der Verwaltungskosten insgesamt.

Eine Verwaltungsbaseline sollte sich nach der längsten akzeptablen RPO richten, um die Kosten zu minimieren. Das Cloudverwaltungsteam kann die RPO dann für bestimmte Plattformen oder Workloads erhöhen, wofür weitere Investitionen gerechtfertigt wären.

## <a name="protect-and-recover-workloads"></a>Workloads für Schutz und Wiederherstellung

Die meisten Workloads in einer IT-Umgebung unterstützen nur einen kleinen geschäftlichen oder technischen Prozess. Systeme, die keine systemrelevanten Auswirkungen auf den Geschäftsbetrieb haben, rechtfertigen häufig nicht die höheren Investitionen, die erforderlich wären, um die Systeme schnell wiederherzustellen oder Datenverluste zu minimieren. Durch Einrichtung einer Baseline lässt sich dem Geschäftsteam klar vermitteln, welches Maß an Wiederherstellungsunterstützung zu einem konsistenten, überschaubaren Preispunkt geboten werden kann. So können die Beteiligten auf geschäftlicher Seite den Wert einer höheren Investition in die Wiederherstellung bemessen.

Für die meisten Cloudverwaltungsteams bietet eine erweiterte Baseline mit spezifischen Zusagen in Bezug auf RPO und RTO für verschiedene Ressourcen den günstigsten Weg zu gegenseitigen Geschäftszusagen. In den folgenden Abschnitten werden einige gängige erweiterte Baselines erläutert, die es den Geschäftsteams ermöglichen, Schutz- und Wiederherstellungsfunktionen problemlos über einen wiederholbaren Prozess hinzuzufügen.

### <a name="protect-and-recover-data"></a>Schutz und Wiederherstellung von Daten

Daten sind die wohl wertvollste Ressource in der digitalen Wirtschaft. Die Fähigkeit, Daten effektiver zu schützen und wiederherzustellen, ist die häufigste erweiterte Baseline. Bei Daten, die für Produktionsworkloads unabdingbar sind, können Datenverluste mit Umsatz- oder Einnahmeverlusten gleichgesetzt werden. Im Allgemeinen wird empfohlen, dass Cloudverwaltungsteams eine erweiterte Verwaltungsbaseline anbieten, die gängige Datenplattformen unterstützt.

Bevor Cloudverwaltungsteams Plattformvorgänge implementieren, unterstützen sie häufig verbesserte Vorgänge für PaaS-Datenplattformen (Platform-as-a-Service). Es ist zum Beispiel für ein Cloudverwaltungsteam problemlos möglich, häufigere Sicherungs- oder regionsübergreifende Replikationsvorgänge für Azure SQL- oder Cosmo DB-Lösungen durchzusetzen. So kann das Entwicklungsteam die RPO ganz einfach durch Modernisierung seiner Datenplattformen verbessern.

Dieser Denkprozess wird in der [Disziplin „Plattformbetrieb“](./platform.md) detaillierter erläutert.

### <a name="protect-and-recover-vms"></a>Schutz und Wiederherstellung von VMs

Die meisten Workloads sind in irgendeiner Form von virtuellen Computern abhängig. Diese virtuellen Computer sind für verschiedene Aspekte der Lösung zuständig. Damit eine Workload einen Geschäftsprozess nach einem Systemausfall wieder unterstützen kann, muss eine bestimmte Anzahl dieser virtuellen Computer schnell wiederhergestellt werden.

Jede Minute Ausfallzeit dieser virtuellen Computer kann Umsatzverlust oder eine geringere Rentabilität bedeuten. Wenn sich Ausfallzeiten von VMs direkt auf das finanzielle Ergebnis des Geschäfts auswirken, ist die RTO sehr wichtig. Durch Replikation zu einem sekundären Standort und automatisierte Wiederherstellungsprozesse lassen sich virtuelle Computer schneller wiederherstellen. Dieses Modell wird als „Hot/Warm-Wiederherstellungsmodell“ bezeichnet. Virtuelle Computer mit dem höchsten Wiederherstellungsstatus können zu einem voll funktionsfähigen sekundären Standort repliziert werden. Dieser kostenintensivere Ansatz wird als Wiederherstellungsmodell mit hoher Verfügbarkeit oder „Hot/Hot-Wiederherstellungsmodell“ bezeichnet.

Jedes der oben genannten Modelle reduziert die RTO und sorgt dafür, dass Geschäftsprozessfunktionen schneller wiederhergestellt werden. Allerdings zieht jedes Modell auch deutlich höhere Cloudverwaltungskosten nach sich.

Dieser Denkprozess wird in der [Disziplin „Workloadbetrieb“](./workload.md) detaillierter erläutert.

## <a name="next-steps"></a>Nächste Schritte

Sobald diese Komponente der Verwaltungsbaseline umgesetzt ist, kann sich das Team um die Vermeidung von Ausfällen beim [Plattformbetrieb](./platform.md) und beim [Workloadbetrieb](./workload.md) kümmern.

> [!div class="nextstepaction"]
> [Plattformbetrieb](./platform.md)
> [Workloadbetrieb](./workload.md)
