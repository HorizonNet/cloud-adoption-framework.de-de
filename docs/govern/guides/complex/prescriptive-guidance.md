---
title: 'Governanceleitfaden für komplexe Unternehmen: Beschreibung der bewährten Methoden'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: In diesem Artikel werden die bewährten Methoden für Governance in komplexen Unternehmen erläutert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 543f4e59645fb389b00508fbd9d6426ded6f41f9
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547648"
---
# <a name="governance-guide-for-complex-enterprises-best-practices-explained"></a>Governanceleitfaden für komplexe Unternehmen: Beschreibung der bewährten Methoden

Der Governanceleitfaden beginnt mit einer Sammlung von anfänglichen [Unternehmensrichtlinien](./initial-corporate-policy.md). Diese Richtlinien werden verwendet, um ein Miminum Viable-Product (MVP, minimal brauchbares Produkt) für die Governance einzurichten, das [bewährte Methoden](./index.md) berücksichtigt.

In diesem Artikel werden die allgemeinen Strategien behandelt, die zum Erstellen eines Governance-MVP erforderlich sind. Der Kern des Governance-MVP ist das Verfahren zur [Beschleunigung der Bereitstellung](../../deployment-acceleration/index.md). Die in dieser Phase angewandten Tools und Muster ermöglichen die inkrementellen Verbesserungen, die für die zukünftige Erweiterung von Governance erforderlich sind.

## <a name="governance-mvp-initial-governance-foundation"></a>Governance-MVP (anfängliche Governancegrundlage)

Die schnelle Einführung von Governance und Unternehmensrichtlinien ist dank einiger einfacher Prinzipien und cloudbasierter Governancetools möglich. Dies sind die ersten der drei Governance-Verfahren, die in jedem Governanceprozess zur Anwendung kommen. Sämtliche Disziplinen werden weiter unten in diesem Artikel erläutert.

Als Ausgangspunkt werden in diesem Artikel die High-Level-Strategien hinter Identitätsbaseline, Sicherheitsbaseline und Beschleunigung der Bereitstellung behandelt, die für die Erstellung eines Governance-MVP erforderlich sind, das als Grundlage für jede Umsetzung dient.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Implementierungsprozess

Die Implementierung des Governance-MVP weist Abhängigkeiten von Identität, Sicherheit und Netzwerk auf. Sobald die Abhängigkeiten aufgelöst wurden, entscheidet das Cloudgovernanceteam über einige Aspekte von Governance. Die Entscheidungen des Cloudgovernanceteams und der unterstützenden Teams werden durch ein einziges Paket von Durchsetzungsmaßnahmen umgesetzt.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp-implementation-flow.png)

Diese Implementierung kann auch mithilfe einer einfachen Prüfliste beschrieben werden:

1. Einholen von Entscheidungen über Kernabhängigkeiten: Identität, Netzwerk und Verschlüsselung.
1. Bestimmen des Musters, das bei der Durchsetzung von Unternehmensrichtlinien verwendet werden soll.
1. Bestimmen der geeigneten Governancemuster für die Disziplinen Ressourcenkonsistenz, Ressourcentagging, Protokollierung und Berichterstellung.
1. Implementieren der Governancetools, die auf das gewählte Muster der Richtliniendurchsetzung abgestimmt sind, um die abhängigen Entscheidungen und Governanceentscheidungen anzuwenden.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Anwenden von durch Governance definierten Mustern

Das Cloudgovernanceteam ist für die folgenden Entscheidungen und Implementierungen verantwortlich. Viele Entscheidungen erfordern Informationen von anderen Teams, aber das Cloudgovernanceteam wird wahrscheinlich sowohl für die endgültige Entscheidung als auch für die Implementierung verantwortlich sein. In den folgenden Abschnitten werden die für diesen Anwendungsfall getroffenen Entscheidungen und Details zu jeder Entscheidung beschrieben.

### <a name="subscription-design"></a>Abonnemententwurf

Die Entscheidung über den Abonnemententwurf bestimmt, wie Azure-Abonnements strukturiert werden und wie Azure-Verwaltungsgruppen verwendet werden, um Zugriff, Richtlinien und Compliance für diese Abonnements effizient zu verwalten. Im vorliegenden Beispielfall hat das Governanceteam das Abonnemententwurfsmuster **[Gemischt](../../../decision-guides/subscriptions/index.md#mixed-patterns)** ausgewählt.

- Wenn neue Anforderungen für Azure-Ressourcen auftreten, sollte für jede größere Geschäftseinheit in jeder geografischen Betriebsregion eine „Abteilung“ eingerichtet werden. Innerhalb jeder der Abteilungen sollten „Abonnements“ für jeden Anwendungsarchetyp erstellt werden.
- Ein Anwendungsarchetyp ist eine Möglichkeit, Anwendungen mit ähnlichen Anwendungen zu gruppieren. Häufige Beispiele sind: Anwendungen mit geschützten Daten, verwaltete Anwendungen (wie HIPAA oder FedRAMP), risikoarme Anwendungen, Anwendungen mit lokalen Abhängigkeiten, SAP-Anwendungen oder Anwendungen anderer Mainframes in Azure oder Anwendungen, die lokale SAP- oder lokale Mainframeanwendungen erweitern. Jedes Unternehmen hat individuelle Anforderungen, die auf Datenklassifikationen und den Arten von Anwendungen basieren, die das Geschäft unterstützen. Die Abhängigkeitszuordnung der digitalen Infrastruktur kann bei der Definition der Anwendungsarchitekturen in einem Unternehmen helfen.
- Im Rahmen des Abonnementdesigns sollte auf der Grundlage der beiden vorangegangenen Aufzählungspunkte eine gemeinsame Namenskonvention vereinbart werden.

### <a name="resource-consistency"></a>Ressourcenkonsistenz

Entscheidungen zur Ressourcenkonsistenz bestimmen die Tools, Prozesse und Aufgaben, die erforderlich sind, um sicherzustellen, dass Azure-Ressourcen innerhalb eines Abonnements konsistent bereitgestellt, konfiguriert und verwaltet werden. Im vorliegenden Beispielfall wurde **[Bereitstellungskonsistenz](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** als primäres Muster für die Ressourcenkonsistenz ausgewählt.

- Ressourcengruppen werden mit dem Lebenszyklusansatz für Anwendungen erstellt. Alle Elemente, die gemeinsam erstellt, verwaltet und außer Betrieb genommen werden, sollten sich in einer einzigen Ressourcengruppe befinden. Weitere Informationen zu Ressourcengruppen finden Sie [hier](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy sollte auf alle Abonnements aus der zugehörigen Verwaltungsgruppe angewendet werden.
- Im Rahmen des Bereitstellungsprozesses sollten Azure Resource Consistency-Vorlagen für die Ressourcengruppe in der Quellcodeverwaltung gespeichert werden.
- Jede Ressourcengruppe ist basierend auf dem oben beschriebenen Lebenszyklusansatz einer bestimmten Workload oder Anwendung zugeordnet.
- Azure-Verwaltungsgruppen ermöglichen das Aktualisieren der Governanceentwürfe, wenn sich die Unternehmensrichtlinie weiterentwickelt.
- Eine umfassende Implementierung von Azure Policy könnte den Zeitrahmen für das Team überschreiten und bietet zu diesem Zeitpunkt möglicherweise keinen großen Mehrwert. Allerdings sollte eine einfache Standardrichtlinie erstellt und auf jede Verwaltungsgruppe angewendet werden, um die geringe Anzahl der aktuellen Richtlinienerklärungen zur Cloud-Governance durchzusetzen. In dieser Richtlinie wird die Implementierung spezifischer Governanceanforderungen definiert. Diese Implementierungen können dann auf alle bereitgestellten Ressourcen angewendet werden.

>[!IMPORTANT]
>Wann immer eine Ressource in einer Ressourcengruppe nicht mehr den gleichen Lebenszyklus hat, sollte sie in eine andere Ressourcengruppe verschoben werden. Beispiele hierfür sind allgemeine Datenbanken und Netzwerkkomponenten. Diese unterstützen zwar die Anwendung, die entwickelt wird, dienen aber auch anderen Zwecke und sollten daher in anderen Ressourcengruppen vorhanden sein.

### <a name="resource-tagging"></a>Tags für Ressourcen

Entscheidungen zur Ressourcenkennzeichnung bestimmen, wie Metadaten innerhalb eines Abonnements auf Azure-Ressourcen angewandt werden, um Prozesse, Verwaltung und Buchhaltung zu unterstützen. Im vorliegenden Beispielfall wurde das Muster **[Buchhaltung](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** als Standardmodell für die Ressourcenkennzeichnung ausgewählt.

- Bereitgestellte Ressourcen sollten mit Werten für Folgendes gekennzeichnet werden:
  - Abteilung/Abrechnungseinheit
  - Gebiet
  - Datenklassifizierung
  - Wichtigkeit
  - SLA
  - Environment
  - Anwendungsprototyp
  - Anwendung
  - Anwendungsbesitzer
- Diese Werte beeinflussen in Kombination mit der Azure-Verwaltungsgruppe und dem einer bereitgestellten Ressource zugeordneten Abonnement die Entscheidungen in den Bereichen Governance, Betrieb und Sicherheit.

### <a name="logging-and-reporting"></a>Protokollierung und Berichterstellung

Entscheidungen zu Protokollierung und Berichterstellung bestimmen, wie Ihr Speicher Daten protokolliert und wie die Überwachungs- und Berichterstellungstools strukturiert sind, die IT-Mitarbeiter über die operative Integrität informieren. Im vorliegenden Beispielfall wird ein **[Hybridüberwachungsmuster](../../../decision-guides/logging-and-reporting/index.md)** für Protokollierung und Berichterstellung vorgeschlagen, zum aktuellen Zeitpunkt aber noch von keinem Entwicklungsteam verlangt.

- Es sind aktuell keine Governanceanforderungen in Bezug auf die für die Protokollierung oder Berichterstellung zu erfassenden spezifischen Datenpunkte festgelegt. Dies ist für diese fiktive Erzählung spezifisch und sollte als Antimuster betrachtet werden. Protokollierungsstandards sollten so früh wie möglich festgelegt und durchgesetzt werden.
- Vor der Freigabe geschützter Daten oder unternehmenskritischer Workloads sind zusätzliche Analysen erforderlich.
- Vor der Unterstützung geschützter Daten oder unternehmenskritischer Workloads muss der bestehenden lokalen Betriebsüberwachungslösung Zugang zu dem für die Protokollierung verwendeten Arbeitsbereich gewährt werden. Anwendungen müssen die mit der Nutzung des betreffenden Mandanten einhergehenden Sicherheits- und Protokollierungsanforderungen erfüllen, wenn die Anwendung mit einem definierten SLA unterstützt werden soll.

## <a name="incremental-of-governance-processes"></a>Inkrementelle Governanceprozesse

Einige der Richtlinienanweisungen können oder sollten nicht durch automatisierte Tools gesteuert werden. Andere Richtlinien erfordern regelmäßigen Aufwand seitens der IT-Sicherheits- und Identitätsbaselineteams. Das Cloudgovernanceteam muss die folgenden Prozesse beaufsichtigen, um die letzten acht Richtlinienanweisungen zu implementieren:

**Änderungen der Unternehmensrichtlinie:** Das Cloudgovernanceteam nimmt Änderungen am Entwurf des Governance-MVP vor, um die neuen Richtlinien zu übernehmen. Der Wert des Governance-MVP besteht darin, dass es die automatische Durchsetzung der neuen Richtlinien ermöglicht.

**Schnellere Einführung:** Das Cloudgovernanceteam hat Bereitstellungsskripts in mehreren Teams überprüft. Es verwaltet eine Reihe von Skripts, die als Bereitstellungsvorlagen dienen. Diese Vorlagen können von den Cloudeinführungs- und DevOps-Teams verwendet werden, um Bereitstellungen schneller zu definieren. Jedes Skript enthält die Anforderungen für die Durchsetzung von Governance-Richtlinien, und zusätzliche Anstrengungen von Technikern für die Cloudeinführung sind nicht erforderlich. Als Kurator dieser Skripts kann das Cloud Governance-Team Richtlinienänderungen schneller umsetzen. Darüber hinaus werden sie als Beschleuniger der Einführung angesehen. Dadurch sind konsistente Bereitstellungen sichergestellt, ohne dass die Einhaltung streng durchgesetzt werden müsste.

**Schulung der Techniker:** Das Cloudgovernanceteam bietet alle zwei Monate Schulungen an und hat zwei Videos für Techniker erstellt. Beide Ressourcen helfen Technikern, schnell mit der Governance-Kultur und der Durchführung von Bereitstellungen vertraut zu werden. Das Team fügt Schulungsressourcen hinzu, die den Unterschied zwischen Produktions- und Nicht-Produktionsbereitstellungen zeigen, was Technikern das Verständnis erleichtert, wie sich die neuen Richtlinien auf die Einführung auswirken. Dadurch sind konsistente Bereitstellungen sichergestellt, ohne dass die Einhaltung streng durchgesetzt werden müsste.

**Bereitstellungsplanung**: Vor der Bereitstellung von Ressourcen, die geschützte Daten enthalten, muss das Cloudgovernanceteam anhand der Bereitstellungsskripts die Governanceausrichtung überprüfen. Vorhandene Teams mit bereits genehmigten Bereitstellungen werden mithilfe von programmgesteuerten Tools überprüft.

**Monatliche Überprüfung und Berichterstellung:** Jeden Monat führt das Cloudgovernanceteam eine Überprüfung aller Cloudbereitstellungen durch, um die kontinuierliche Einhaltung der Richtlinien zu überprüfen. Wenn Abweichungen festgestellt werden, werden sie dokumentiert und an die Cloudeinführungsteams weitergegeben. Wenn die Durchsetzung keine Betriebsunterbrechung oder Datenlecks zur Folge hat, werden die Richtlinien automatisch durchgesetzt. Am Ende der Überprüfung erstellt das Cloudgovernanceteam einen Bericht für das Cloudstrategieteam und jedes Cloudeinführungsteam, um die allgemeine Einhaltung der Richtlinien zu kommunizieren. Der Bericht wird außerdem für prüfungsbezogene und rechtliche Zwecke gespeichert.

**Vierteljährliche Richtlinienüberprüfung:** Jedes Quartal überprüfen das Cloudgovernanceteam und das Cloudstrategieteam die Überwachungsergebnisse und schlagen Änderungen der Unternehmensrichtlinien vor. Viele dieser Vorschläge sind das Ergebnis kontinuierlicher Verbesserungen und der Beobachtung von Nutzungsmustern. Genehmigte Richtlinienänderungen werden während der nachfolgenden Überwachungszyklen in die Governancetools integriert.

## <a name="alternative-patterns"></a>Alternative Muster

Wenn eines der in diesem Governanceleitfaden ausgewählten Muster nicht mit den Anforderungen Ihres Unternehmens übereinstimmt, gibt es Alternativen zu jedem Muster:

- [Verschlüsselungsmuster](../../../decision-guides/encryption/index.md)
- [Identitätsmuster](../../../decision-guides/identity/index.md)
- [Protokollierungs- und Berichterstellungsmuster](../../../decision-guides/logging-and-reporting/index.md)
- [Richtliniendurchsetzungsmuster](../../../decision-guides/policy-enforcement/index.md)
- [Ressourcenkonsistenzmuster](../../../decision-guides/resource-consistency/index.md)
- [Ressourcenkennzeichnungsmuster](../../../decision-guides/resource-tagging/index.md)
- [Muster für Software-Defined Networking](../../../decision-guides/software-defined-network/index.md)
- [Abonnemententwurfsmuster](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Nächste Schritte

Sobald dieser Leitfaden implementiert wurde, kann jedes Cloudeinführungsteam seine Arbeit mit einer soliden Governancebasis fortsetzen. Gleichzeitig werden die Unternehmensrichtlinien und Governanceverfahren kontinuierlich durch das Cloudgovernanceteam aktualisiert.

Beide Teams verwenden die Toleranzindikatoren, um die nächsten Verbesserungen zu identifizieren, die erforderlich sind, um die Einführung der Cloud weiterhin zu unterstützen. Der nächste Schritt für dieses Unternehmen ist die inkrementelle Verbesserung seiner Governancebaseline zur Unterstützung von Anwendungen mit Legacy- oder Drittanbieterlösungen für die mehrstufige Authentifizierung.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Identitätsbaseline“](./identity-baseline-improvement.md)
