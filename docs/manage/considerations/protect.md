---
title: Schutz und Wiederherstellung in der Cloudverwaltung
description: Enthält eine Beschreibung dazu, wie wichtig es ist, sich auf einen potenziellen Workloadausfall vorzubereiten. Dank dieser Vorbereitung kann Ihr Team Fehler schneller erkennen und den Betrieb in kürzerer Zeit wiederherstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f46fb65572d319e2dc9a4a779cd205bbe476908b
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340994"
---
# <a name="protect-and-recover-in-cloud-management"></a>Schutz und Wiederherstellung in der Cloudverwaltung

Nachdem sie die Anforderungen an [Bestand und Transparenz](./inventory.md) und [betriebsbezogene Compliance](./operational-compliance.md) erfüllt haben, können die Cloudverwaltungsteams einen potenziellen Workloadausfall vorhersehen und sich darauf vorbereiten. Beim Planen der Cloudverwaltung muss das Team mit der Annahme beginnen, dass etwas ausfällt.

Keine technische Lösung kann konsistent eine SLA mit 100 Prozent Betriebszeit bieten. Lösungen mit Architekturen mit einem Höchstmaß an Redundanz nehmen für sich in Anspruch, Betriebszeiten mit „sechs Neunen“, also 99,9999 Prozent zu bieten. Aber selbst eine Lösung mit „sechs Neunen“ fällt jedes Jahr durchschnittlich 31,6 Sekunden lang aus. Leider rechtfertigen Lösungen selten die umfangreichen, kontinuierlichen Investitionen, die vonnöten sind, um eine Betriebszeit mit „sechs Neunen“ zu erzielen.

Wenn Teams sich auf Ausfälle vorbereiten, können sie Fehler schneller erkennen und den Betrieb in kürzerer Zeit wiederherstellen. In der vorliegenden Disziplin geht es um die Schritte, die sofort nach einem Systemausfall ausgeführt werden müssen. Wie schützen Sie Workloads, sodass sie nach einem Ausfall schnell wiederhergestellt werden können?

## <a name="translate-protection-and-recovery-conversations"></a>Übersetzen von Gesprächen zum Thema Schutz und Wiederherstellung

Die Workloads, auf denen der Geschäftsbetrieb basiert, bestehen aus Anwendungen, Daten, virtuellen Computern (VMs) und anderen Ressourcen. Möglicherweise erfordert jede dieser Ressource einen anderen Ansatz in Bezug auf Schutz und Wiederherstellung. Der wichtigste Aspekt dieser Disziplin ist es, konsistente Zusagen in Bezug auf die Verwaltungsbaseline zu treffen, um eine Ausgangsbasis für geschäftsbezogene Gespräche zu schaffen.

Als Mindestanforderung sollte für jede Ressource, die eine bestimmte Workload unterstützt, eine Baseline mit eindeutigen Zusagen in Bezug auf die Geschwindigkeit einer Wiederherstellung (Recovery Time Objective, RTO) oder das Risiko von Datenverlusten (Recovery Point Objective, RPO) festgelegt werden.

### <a name="recovery-time-objectives-rto"></a>Recovery Time Objective (RTO)

Wenn der Ernstfall eintritt, ist die RTO (Recovery Time Objective) die Zeitspanne, die benötigt wird, um ein beliebiges System auf seinen Zustand vor dem Ausfall wiederherzustellen. Dies umfasst für jede Workload die Zeit, die notwendig ist, um eine Mindestfunktionalität für die VMs und Apps wiederherzustellen. Dazu gehört auch die Zeit, die notwendig ist, um die von den Anwendungen benötigten Daten wiederherzustellen.

Aus geschäftlicher Sicht stellt die RTO den Zeitraum dar, in dem der Geschäftsprozess außer Betrieb ist. Bei unternehmenskritischen Workloads sollte diese Variable relativ niedrig sein, damit die Geschäftsprozesse schnell fortgesetzt werden können. Bei Workloads mit geringerer Priorität hat eine Standard-RTO möglicherweise keine nennenswerten Auswirkungen auf die Gesamtleistung des Unternehmens.

Die Verwaltungsbaseline sollte eine Standard-RTO für nicht unternehmenskritische Workloads festlegen. Aus geschäftlicher Sicht kann diese Baseline dann dazu dienen, zusätzliche Investitionen in Wiederherstellungszeiten zu rechtfertigen.

### <a name="recovery-point-objectives-rpo"></a>Recovery Point Objective (RPO)

In den meisten Cloudverwaltungssystemen werden Daten durch irgendeine Form des Datenschutzes in regelmäßigen Abständen erfasst und gespeichert. Der letzte Zeitpunkt, zu dem Daten erfasst wurden, wird als Wiederherstellungspunkt bezeichnet. Wenn ein System ausfällt, kann es nur auf den jüngsten Wiederherstellungspunkt wiederhergestellt werden.

Wenn für ein System eine RPO von mehreren Stunden oder sogar Tagen festgelegt wurde, würde ein Systemausfall dazu führen, dass alle Daten zwischen dem letzten Wiederherstellungspunkt und dem Ausfall verloren sind. Eine RPO von einem Tag würde theoretisch zum Verlust sämtlicher Transaktionen an diesem Tag bis zum Ausfall führen.

Bei unternehmenskritischen Systemen ist daher eine RPO in einer Größenordnung von einigen Minuten oder Sekunden wahrscheinlich besser geeignet, um Umsatzverluste zu vermeiden. Eine kürzere RPO führt im Allgemeinen aber auch zu einer Erhöhung der Verwaltungskosten insgesamt.

Eine Verwaltungsbaseline sollte sich nach der längsten akzeptablen RPO richten, um dabei zu helfen, die Kosten zu minimieren. Das Cloudverwaltungsteam kann die RPO dann für bestimmte Plattformen oder Workloads erhöhen, wofür weitere Investitionen gerechtfertigt wären.

## <a name="protect-and-recover-workloads"></a>Workloads für Schutz und Wiederherstellung

Die meisten Workloads in einer IT-Umgebung unterstützen nur einen bestimmten geschäftlichen oder technischen Prozess. Systeme, die keine systemrelevanten Auswirkungen auf den Geschäftsbetrieb haben, rechtfertigen häufig nicht die höheren Investitionen, die erforderlich wären, um die Systeme schnell wiederherzustellen oder Datenverluste zu minimieren. Durch Einrichtung einer Baseline lässt sich dem Geschäftsteam klar vermitteln, welches Maß an Wiederherstellungsunterstützung zu einem konsistenten, überschaubaren Preispunkt geboten werden kann. Dieses Verständnis hilft den Beteiligten auf geschäftlicher Seite den Wert einer höheren Investition in die Wiederherstellung zu bemessen.

Für die meisten Cloudverwaltungsteams bietet eine erweiterte Baseline mit spezifischen Zusagen in Bezug auf RPO und RTO für verschiedene Ressourcen den günstigsten Weg zu gegenseitigen Geschäftszusagen. In den folgenden Abschnitten werden einige gängige erweiterte Baselines erläutert, die es den Geschäftsteams ermöglichen, Schutz- und Wiederherstellungsfunktionen problemlos über einen wiederholbaren Prozess hinzuzufügen.

### <a name="protect-and-recover-data"></a>Schutz und Wiederherstellung von Daten

Daten sind die wohl wertvollste Ressource in der digitalen Wirtschaft. Die Fähigkeit, Daten effektiver zu schützen und wiederherzustellen, ist die häufigste erweiterte Baseline. Bei Daten, die für Produktionsworkloads unabdingbar sind, können Datenverluste mit Umsatz- oder Einnahmeverlusten gleichgesetzt werden. Im Allgemeinen empfehlen wir Cloudverwaltungsteams, dass sie eine erweiterte Verwaltungsbaseline anbieten, die gängige Datenplattformen unterstützt.

Bevor Cloudverwaltungsteams Plattformvorgänge implementieren, unterstützen sie häufig verbesserte Vorgänge für PaaS-Datenplattformen (Platform-as-a-Service). Es ist zum Beispiel für ein Cloudverwaltungsteam problemlos möglich, häufigere Sicherungsvorgänge oder regionsübergreifende Replikationsvorgänge für Azure SQL-Datenbank- oder Azure Cosmos DB-Lösungen durchzusetzen. So kann das Entwicklungsteam die RPO einfach durch Modernisierung seiner Datenplattformen verbessern.

Weitere Informationen zu diesem Denkprozess finden Sie unter [Disziplin „Plattformbetrieb“](./platform.md).

### <a name="protect-and-recover-vms"></a>Schutz und Wiederherstellung von VMs

Die meisten Workloads sind teilweise von virtuellen Computern abhängig, die verschiedene Aspekte der Lösung hosten. Damit eine Workload einen Geschäftsprozess nach einem Systemausfall wieder unterstützen kann, muss eine bestimmte Anzahl virtueller Computer schnell wiederhergestellt werden.

Jede Minute Ausfallzeit dieser virtuellen Computer kann Umsatzverlust oder eine geringere Rentabilität nach sich ziehen. Wenn sich Ausfallzeiten von virtuellen Computern direkt auf das finanzielle Ergebnis des Geschäfts auswirken, ist die RTO sehr wichtig. Durch Replikation zu einem sekundären Standort und automatisierte Wiederherstellungsprozesse lassen sich virtuelle Computer schneller wiederherstellen. Dieses Modell wird als „Hot/Warm-Wiederherstellungsmodell“ bezeichnet. Virtuelle Computer mit dem höchsten Wiederherstellungsstatus können zu einem voll funktionsfähigen sekundären Standort repliziert werden. Dieser kostenintensivere Ansatz wird als Wiederherstellungsmodell mit hoher Verfügbarkeit oder „Hot/Hot-Wiederherstellungsmodell“ bezeichnet.

Jedes der eben genannten Modelle reduziert die RTO und sorgt dafür, dass Geschäftsprozessfunktionen schneller wiederhergestellt werden. Allerdings zieht jedes Modell auch deutlich höhere Cloudverwaltungskosten nach sich.

Weitere Informationen zu diesem Denkprozess finden Sie unter [Disziplin „Plattformbetrieb“](./workload.md).

## <a name="next-steps"></a>Nächste Schritte

Sobald diese Komponente der Verwaltungsbaseline umgesetzt ist, kann sich das Team um die Vermeidung von Ausfällen beim [Plattformbetrieb](./platform.md) und beim [Workloadbetrieb](./workload.md) kümmern.

> [!div class="nextstepaction"]
> [Plattformbetrieb](./platform.md)
> [Workloadbetrieb](./workload.md)
