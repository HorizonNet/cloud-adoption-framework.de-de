---
title: 'Governance für Standardunternehmen: Beschreibung der bewährten Methoden'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um ein Minimum Viable Product (MVP) für die Governance einzurichten, das bewährte Methoden für ein Standardunternehmen widerspiegelt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b7f8b26833a98ac02a867b466e58f5214334a0b5
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219993"
---
# <a name="standard-enterprise-governance-guide-best-practices-explained"></a>Governanceleitfaden für Standardunternehmen: Beschreibung der bewährten Methoden

Der Governanceleitfaden beginnt mit einer Sammlung von anfänglichen [Unternehmensrichtlinien](./initial-corporate-policy.md). Diese Richtlinien werden verwendet, um ein Governance-MVP einzurichten, das [bewährte Methoden](./index.md) berücksichtigt.

In diesem Artikel werden die allgemeinen Strategien behandelt, die zum Erstellen eines Governance-MVP erforderlich sind. Der Kern des Governance-MVP ist die [Disziplin der Beschleunigung der Bereitstellung](../../deployment-acceleration/index.md). Die in dieser Phase angewandten Tools und Muster ermöglichen die inkrementellen Verbesserungen, die für die zukünftige Erweiterung von Governance erforderlich sind.

## <a name="governance-mvp-initial-governance-foundation"></a>Governance-MVP (anfängliche Governancegrundlage)

Die schnelle Einführung von Governance und Unternehmensrichtlinien ist dank einiger einfacher Prinzipien und cloudbasierter Governancetools möglich. Dies sind die ersten drei Disziplinen, die in jedem Governanceprozess enthalten sind. Jede Disziplin wird in diesem Artikel näher beschrieben.

<!--docsTest:ignore "Identity Baseline, Security Baseline, and Deployment Acceleration disciplines" -->

Als Ausgangspunkt werden in diesem Artikel die allgemeinen Strategien hinter den Disziplinen „Identitätsbaseline“, „Sicherheitsbaseline“ und „Beschleunigung der Bereitstellung“ behandelt, die zum Erstellen eines Governance-MVP erforderlich sind, der als Grundlage für jede Umsetzung dient.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Implementierungsprozess

Die Implementierung des Governance-MVP weist Abhängigkeiten von Identität, Sicherheit und Netzwerk auf. Sobald die Abhängigkeiten aufgelöst wurden, entscheidet das Cloudgovernanceteam über einige Aspekte von Governance. Die Entscheidungen des Cloudgovernanceteams und der unterstützenden Teams werden durch ein einziges Paket von Durchsetzungsmaßnahmen umgesetzt.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp-implementation-flow.png)

Diese Implementierung kann auch mithilfe einer einfachen Prüfliste beschrieben werden:

1. Einholen von Entscheidungen über Kernabhängigkeiten: Identität, Netzwerk, Überwachung und Verschlüsselung.
2. Bestimmen des Musters, das bei der Durchsetzung von Unternehmensrichtlinien verwendet werden soll.
3. Bestimmen der geeigneten Governancemuster für die Disziplinen „Ressourcenkonsistenz“, „Ressourcentagging“, „Protokollierung“ und „Berichterstellung“.
4. Implementieren der Governancetools, die auf das gewählte Muster der Richtliniendurchsetzung abgestimmt sind, um die abhängigen Entscheidungen und Governanceentscheidungen anzuwenden.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Anwenden von durch Governance definierten Mustern

Das Cloudgovernanceteam ist für die folgenden Entscheidungen und Implementierungen verantwortlich. Viele Entscheidungen erfordern Informationen von anderen Teams, aber das Cloudgovernanceteam wird wahrscheinlich sowohl für die endgültige Entscheidung als auch für die Implementierung verantwortlich sein. In den folgenden Abschnitten werden die für diesen Anwendungsfall getroffenen Entscheidungen und Details zu jeder Entscheidung beschrieben.

### <a name="subscription-design"></a>Abonnemententwurf

Die Entscheidung über den Abonnemententwurf bestimmt, wie Azure-Abonnements strukturiert werden und wie Azure-Verwaltungsgruppen verwendet werden, um Zugriff, Richtlinien und Compliance für diese Abonnements effizient zu verwalten. In diesem Beispielfall hat das Governanceteam Abonnements für Produktions- und Nichtproduktionsworkloads mit dem Abonnemententwurfsmuster für [Produktion und Nichtproduktion](../../../ready/azure-best-practices/initial-subscriptions.md) eingerichtet.

- Abteilungen werden angesichts des aktuellen Schwerpunkts wahrscheinlich nicht erforderlich sein. Es wird erwartet, dass die Bereitstellungen innerhalb einer einzigen Abrechnungseinheit eingeschränkt sind. In der Einführungsphase gibt es möglicherweise nicht einmal eine Unternehmensvereinbarung (Enterprise Agreement, EA) zur Zentralisierung der Abrechnung. Es ist wahrscheinlich, dass dieser Grad der Einführung von einem einzigen Azure-Abonnement mit nutzungsbasierter Bezahlung verwaltet wird.
- Unabhängig von der Verwendung des EA-Portals oder des Vorhandenseins einer Unternehmensvereinbarung sollte dennoch ein Abonnementmodell definiert und vereinbart werden, um den Verwaltungsmehraufwand über die reine Abrechnung hinaus zu minimieren.
- Im Rahmen des Abonnementdesigns sollte auf der Grundlage der beiden vorangegangenen Punkte eine gemeinsame Namenskonvention vereinbart werden.

### <a name="resource-consistency"></a>Ressourcenkonsistenz

Entscheidungen zur Ressourcenkonsistenz bestimmen die Tools, Prozesse und Aufgaben, die erforderlich sind, um sicherzustellen, dass Azure-Ressourcen innerhalb eines Abonnements konsistent bereitgestellt, konfiguriert und verwaltet werden. Im vorliegenden Beispielfall wurde [Bereitstellungskonsistenz](../../../decision-guides/resource-consistency/index.md#deployment-consistency) als primäres Muster für die Ressourcenkonsistenz ausgewählt.

- Ressourcengruppen werden mit dem Lebenszyklusansatz für Anwendungen erstellt. Alle Elemente, die gemeinsam erstellt, verwaltet und außer Betrieb genommen werden, sollten sich in einer einzigen Ressourcengruppe befinden. Weitere Informationen finden Sie im [Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy sollte auf alle Abonnements aus der zugehörigen Verwaltungsgruppe angewendet werden.
- Im Rahmen des Bereitstellungsprozesses sollten Azure-Ressourcenkonsistenzvorlagen für die Ressourcengruppe in der Quellcodeverwaltung gespeichert werden.
- Jede Ressourcengruppe ist basierend auf dem oben beschriebenen Lebenszyklusansatz einer bestimmten Workload oder Anwendung zugeordnet.
- Azure-Verwaltungsgruppen ermöglichen das Aktualisieren der Governanceentwürfe, wenn sich die Unternehmensrichtlinie weiterentwickelt.
- Eine umfassende Implementierung von Azure Policy könnte den Zeitrahmen für das Team überschreiten und bietet zu diesem Zeitpunkt möglicherweise keinen großen Mehrwert. Allerdings sollte eine einfache Standardrichtlinie erstellt und auf jede Verwaltungsgruppe angewendet werden, um die geringe Anzahl der aktuellen Richtlinienerklärungen zur Cloud-Governance durchzusetzen. In dieser Richtlinie wird die Implementierung spezifischer Governanceanforderungen definiert. Diese Implementierungen können dann auf alle bereitgestellten Ressourcen angewendet werden.

>[!IMPORTANT]
>Wann immer eine Ressource in einer Ressourcengruppe nicht mehr den gleichen Lebenszyklus hat, sollte sie in eine andere Ressourcengruppe verschoben werden. Beispiele hierfür sind allgemeine Datenbanken und Netzwerkkomponenten. Diese unterstützen zwar die Anwendung, die entwickelt wird, dienen aber auch anderen Zwecke und sollten daher in anderen Ressourcengruppen vorhanden sein.

### <a name="resource-tagging"></a>Tags für Ressourcen

Entscheidungen zur Ressourcenkennzeichnung bestimmen, wie Metadaten innerhalb eines Abonnements auf Azure-Ressourcen angewandt werden, um Prozesse, Verwaltung und Buchhaltung zu unterstützen. Im vorliegenden Beispielfall wurde das Muster [Klassifizierung](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns) als Standardmodell für das Ressourcentagging ausgewählt.

- Bereitgestellte Ressourcen sollten mit Folgendem gekennzeichnet werden:
  - Datenklassifizierung
  - Wichtigkeit
  - SLA
  - Environment
- Diese vier Werte sind für Governance-, Vorgangs- und Sicherheitentscheidungen wichtig.
- Wenn dieser Governanceleitfaden für eine Geschäftseinheit oder ein Team innerhalb eines größeren Unternehmens implementiert wird, sollte das Tagging auch Metadaten für die Abrechnungseinheit enthalten.

### <a name="logging-and-reporting"></a>Protokollierung und Berichterstellung

Entscheidungen zu Protokollierung und Berichterstellung bestimmen, wie Ihr Speicher Daten protokolliert und wie die Überwachungs- und Berichterstellungstools strukturiert sind, die IT-Mitarbeiter über die operative Integrität informieren. In dieser Geschichte wird ein [cloudnatives Muster](../../../decision-guides/logging-and-reporting/index.md#cloud-native)** für die Protokollierung und Berichterstellung vorgeschlagen.

## <a name="incremental-improvement-of-governance-processes"></a>Inkrementelle Verbesserung der Governanceprozesse

Im Zuge von Governanceänderungen können oder sollen einige Richtlinienanweisungen nicht durch automatisierte Tools kontrolliert werden. Andere Richtlinien werden im Laufe der Zeit zu einem erhöhten Aufwand für das IT-Sicherheitsteam und das lokale Identity Management-Team führen. Um neu auftretende Risiken einzudämmen, wird das Cloudgovernanceteam die folgenden Prozesse überwachen.

**Schnellere Einführung:** Das Cloudgovernanceteam hat Bereitstellungsskripts in mehreren Teams überprüft. Es verwaltet eine Reihe von Skripts, die als Bereitstellungsvorlagen dienen. Diese Vorlagen werden von den Cloudeinführungs- und DevOps-Teams verwendet, um Bereitstellungen schneller zu definieren. Jedes dieser Skripts enthält die erforderlichen Anforderungen, um eine Reihe von Governancerichtlinien durchzusetzen, und zwar ohne zusätzlichen Aufwand für die Techniker, die für die Cloudeinführung zuständig sind. Als Kurator dieser Skripts kann das Cloudgovernanceteam Richtlinienänderungen schneller umsetzen. Als Ergebnis der Skriptkuratierung wird das Cloudgovernanceteam als Quelle der Beschleunigung der Einführung angesehen. Dies schafft Konsistenz zwischen den Bereitstellungen, ohne die Einhaltung streng zu erzwingen.

**Schulung der Techniker:** Das Cloudgovernanceteam bietet alle zwei Monate Schulungen an und hat zwei Videos für Techniker erstellt. Diese Materialien helfen den Engineers, die Governancekultur und die Vorgehensweise bei der Bereitstellung schnell zu erlernen. Das Team fügt Schulungsressourcen hinzu, die den Unterschied zwischen Produktions- und Nicht-Produktionsbereitstellungen zeigen, sodass die Techniker verstehen, wie sich die neuen Richtlinien auf die Einführung auswirken. Dies schafft Konsistenz zwischen den Bereitstellungen, ohne die Einhaltung streng zu erzwingen.

**Bereitstellungsplanung**: Vor der Bereitstellung von Ressourcen, die geschützte Daten enthalten, überprüft das Cloudgovernanceteam die Bereitstellungsskripts, um die Ausrichtung von Governance zu überprüfen. Vorhandene Teams mit bereits genehmigten Bereitstellungen werden mithilfe von programmgesteuerten Tools überprüft.

**Monatliche Überprüfung und Berichterstellung:** Jeden Monat führt das Cloudgovernanceteam eine Überprüfung aller Cloudbereitstellungen durch, um die kontinuierliche Einhaltung der Richtlinien zu überprüfen. Wenn Abweichungen festgestellt werden, werden sie dokumentiert und an die Cloudeinführungsteams weitergegeben. Wenn die Durchsetzung keine Betriebsunterbrechung oder Datenlecks zur Folge hat, werden die Richtlinien automatisch durchgesetzt. Am Ende der Überprüfung erstellt das Cloudgovernanceteam einen Bericht für das Cloudstrategieteam und jedes Cloudeinführungsteam, um die allgemeine Einhaltung der Richtlinien zu kommunizieren. Der Bericht wird außerdem für prüfungsbezogene und rechtliche Zwecke gespeichert.

**Vierteljährliche Richtlinienüberprüfung:** Jedes Quartal überprüfen das Cloudgovernanceteam und das Cloudstrategieteam die Überwachungsergebnisse und schlagen Änderungen der Unternehmensrichtlinien vor. Viele dieser Vorschläge sind das Ergebnis kontinuierlicher Verbesserungen und der Beobachtung von Nutzungsmustern. Genehmigte Richtlinienänderungen werden während der nachfolgenden Überwachungszyklen in die Governancetools integriert.

## <a name="alternative-patterns"></a>Alternative Muster

Wenn eines der in diesem Governanceleitfaden ausgewählten Muster nicht mit den Anforderungen Ihres Unternehmens übereinstimmt, gibt es Alternativen zu jedem Muster:

- [Verschlüsselungsmuster](../../../decision-guides/encryption/index.md)
- [Identitätsmuster](../../../decision-guides/identity/index.md)
- [Protokollierungs- und Berichterstellungsmuster](../../../decision-guides/logging-and-reporting/index.md)
- [Richtliniendurchsetzungsmuster](../../../decision-guides/policy-enforcement/index.md)
- [Ressourcenkonsistenzmuster](../../../decision-guides/resource-consistency/index.md)
- [Ressourcenmarkierungsmuster](../../../decision-guides/resource-tagging/index.md)
- [Muster für Software-Defined Networking](../../../decision-guides/software-defined-network/index.md)
- [Abonnemententwurfsmuster](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Nächste Schritte

Sobald dieser Leitfaden implementiert wurde, kann jedes Cloudeinführungsteam seine Arbeit mit einer soliden Governancebasis fortsetzen. Gleichzeitig werden die Unternehmensrichtlinien und Governanceverfahren kontinuierlich durch das Cloudgovernanceteam aktualisiert.

Die beiden Teams verwenden die Toleranzindikatoren, um die nächsten Verbesserungen zu identifizieren, die erforderlich sind, um die Einführung der Cloud weiterhin zu unterstützen. Für das fiktive Unternehmen in diesem Leitfaden ist der nächste Schritt die Verbesserung der Sicherheitsbaseline zur Unterstützung des Verschiebens geschützter Daten in die Cloud.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Sicherheitsbaseline“](./security-baseline-improvement.md)
