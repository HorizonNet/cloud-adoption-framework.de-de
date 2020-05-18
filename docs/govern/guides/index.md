---
title: Cloudgovernance-Leitfäden
description: Sehen Sie sich die Cloudgovernance-Leitfäden an, in denen Best Practices für einen inkrementellen Ansatz zu jedem Governanceszenario veranschaulicht werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6fceb9665712b4d787689ad2e3e709a5ac14d0d0
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400740"
---
# <a name="cloud-governance-guides"></a>Cloudgovernance-Leitfäden

Die direkt umsetzbaren Governanceleitfäden in diesem Abschnitt veranschaulichen den inkrementellen Ansatz des Cloud Adoption Framework-Governancemodells basierend auf der zuvor beschriebenen [Governancemethodik](../methodology.md). Sie können einen agilen Ansatz für Cloudgovernance entwickeln, der sich anpasst, um den Anforderungen jedes Cloudgovernanceszenarios gerecht zu werden.

## <a name="review-and-adopt-cloud-governance-best-practices"></a>Überprüfen und Einführen bewährter Methoden für Cloud Governance

Wählen Sie einen der folgenden Governanceleitfäden aus, um mit der Cloudeinführung zu beginnen. Jeder Leitfaden beschreibt eine Reihe von bewährten Methoden, die auf einer Reihe fiktiver Kundenerfahrungen basieren. Leser, die noch keine Erfahrung mit dem inkrementellen Ansatz des Governancemodells des Frameworks für die Cloudeinführung haben, sollten sich zunächst weiter unten mit der Einführung in die Theorie der allgemeinen Governance vertraut machen, bevor sie eine der bewährten Methoden anwenden.

<!-- markdownlint-disable MD033 -->

- [Standardgovernanceleitfaden:](./standard/index.md) Ein Leitfaden für die meisten Organisationen, basierend auf dem empfohlenen Modell mit zwei Abonnements, das für Bereitstellungen in mehreren Regionen konzipiert wurde, aber nicht für öffentliche Clouds und Sovereign/Government Clouds gilt.

> [!div class="nextstepaction"]
> [Standardgovernanceleitfaden](./standard/index.md)

- [Governanceleitfaden für komplexe Unternehmen:](./complex/index.md) Ein Leitfaden für Unternehmen, die über mehrere unabhängige IT-Geschäftseinheiten verwaltet werden oder öffentliche Clouds und Sovereign/Government Clouds umfassen.

> [!div class="nextstepaction"]
> [Governanceleitfaden für komplexe Unternehmen](./complex/index.md)

<!-- markdownlint-enable MD033 -->

## <a name="an-incremental-approach-to-cloud-governance"></a>Ein inkrementeller Ansatz für die Cloudgovernance

## <a name="choose-a-governance-guide"></a>Auswählen eines Governanceleitfadens

Die Leitfäden veranschaulichen, wie ein Governance-MVP implementiert wird. Von dort aus zeigt jeder Leitfaden, wie das Cloudgovernanceteam als Partner den Cloudeinführungsteams zuarbeiten kann, um die Einführung zu beschleunigen. Das Governancemodell des Frameworks für die Cloudeinführung steuert die Governanceanwendung von der Grundlage bis hin zu nachfolgenden Verbesserungen und Weiterentwicklungen.

Um mit einer Governancelösung zu beginnen, wählen Sie eine der beiden folgenden Optionen aus. Die Optionen basieren auf synthetisierten Kundenerfahrungen. Die Titel basieren auf der Komplexität des Unternehmens zur Vereinfachung der Navigation. Die Entscheidung des Lesers kann jedoch komplexer sein. Die folgenden Tabellen zeigen die Unterschiede zwischen den beiden Optionen.

<!-- TODO: Refactor VDC content below. -->
<!-- docsTest:ignore "Azure Virtual Datacenter" -->

> [!WARNING]
> Ein robusterer Ausgangspunkt für die Governance kann erforderlich sein. Beachten Sie in solchen Fällen das Modell des [virtuellen Azure-Rechenzentrums](#azure-virtual-datacenter), das [weiter unten](#azure-virtual-datacenter) kurz beschrieben wird. Dieser Ansatz wird häufig bei einer unternehmensweiten Einführung vorgeschlagen, insbesondere bei einem Umfang von über 10.000 Ressourcen. Er ist auch die Standardwahl bei komplexen Governanceszenarien, wenn eine der folgenden Anforderungen erfüllt werden muss: umfangreiche Complianceanforderungen von Drittanbietern, tiefgreifendes Fachwissen oder Parität mit ausgereiften IT-Governancerichtlinien und Complianceanforderungen.

<!-- markdownlint-disable MD028 -->

> [!NOTE]
> Es ist unwahrscheinlich, dass ein Leitfaden vollständig auf Ihre Situation abgestimmt ist. Wählen Sie den Leitfaden aus, der Ihrer Situation am nächsten kommt, und nutzen Sie ihn als Ausgangspunkt. Im gesamten Leitfaden werden zusätzliche Informationen bereitgestellt, die Ihnen helfen, Entscheidungen an bestimmte Kriterien anzupassen.

### <a name="business-characteristics"></a>Geschäftsmerkmale

| Merkmal | Standardorganisation | Komplexes Unternehmen |
|---|---|---|
| Geografie (Land oder geopolitische Region) | Kunden oder Mitarbeiter befinden sich hauptsächlich an einem geografischen Standort | Kunden oder Mitarbeiter befinden sich an mehreren geografischen Standorten oder benötigen Sovereign Clouds |
| Betroffene Geschäftseinheiten | Geschäftseinheiten, die eine gemeinsame IT-Infrastruktur verwenden | Mehrere Geschäftseinheiten, die keine gemeinsame IT-Infrastruktur verwenden |
| IT-Budget | Einzelnes IT-Budget | Budget verteilt auf Geschäftseinheiten und Währungen |
| IT-Investitionen | Kapitalkostengesteuerte Investitionen werden jährlich geplant und decken in der Regel nur die Grundwartung ab. | Kapitalkostengesteuerte Investitionen werden jährlich geplant und beinhalten oft Wartung und einen Aktualisierungszyklus von drei bis fünf Jahren. |

### <a name="current-state-before-adopting-cloud-governance"></a>Aktueller Status vor der Einführung von Cloud Governance

| State | Standardunternehmen | Komplexes Unternehmen |
|---|---|---|
| Datencenter oder Drittanbieter-Hostinganbieter | Weniger als fünf Datencenter | Mehr als fünf Datencenter |
| Netzwerk | Kein WAN oder 1 &ndash; 2 WAN-Anbieter | Komplexes Netzwerk oder globales WAN |
| Identity | Einzelne Gesamtstruktur, einzelne Domäne. | Komplex, mehrere Gesamtstrukturen, mehrere Domänen. |

### <a name="desired-future-state-after-incremental-improvement-of-cloud-governance"></a>Gewünschter zukünftiger Zustand nach inkrementeller Verbesserung der Cloudgovernance

| State | Standardorganisation | Komplexes Unternehmen |
|---|---|---|
| Kostenverwaltung&mdash;Cloudabrechnung | Showbackmodell Abrechnung wird über IT zentralisiert. | Chargebackmodell Die Abrechnung kann durch IT-Beschaffung verteilt werden. |
| Sicherheitsbaseline&mdash;geschützte Daten | Unternehmensfinanzdaten und IP. Eingeschränkte Kundendaten. Keine Complianceanforderungen von Drittanbietern. | Mehrere Sammlungen von Finanzdaten und personenbezogenen Daten von Kunden. Möglicherweise muss Drittanbietercompliance berücksichtigt werden. |

## <a name="azure-virtual-datacenter"></a>Virtuelles Azure-Rechenzentrum

Mit dem virtuelle Azure-Rechenzentrum können Sie die Funktionen der Azure-Cloudplattform optimal nutzen und gleichzeitig den Sicherheits- und Governanceanforderungen eines Unternehmens gerecht werden.

Im Vergleich zu herkömmlichen lokalen Umgebungen ermöglicht Azure es Workload-Entwicklungsteams und ihren Geschäftssponsoren, die Vorteile der erhöhten Bereitstellungsagilität von Cloudplattformen zu nutzen. Da sich Ihre Bemühungen zur Cloudeinführung jedoch auf unternehmenskritische Daten und Workloads ausdehnen, kann diese Agilität im Widerspruch zu den von Ihren IT-Teams festgelegten Anforderungen an Unternehmenssicherheit und Richtlinieneinhaltung stehen. Dies gilt insbesondere für große Unternehmen, in denen bereits ausgereifte Governance- und Regulierungsanforderungen vorhanden sind.

Der Ansatz des virtuellen Azure-Rechenzentrums ist dafür ausgelegt, diese Bedenken im Lebenszyklus der Einführung frühzeitig zu berücksichtigen. Dazu werden Modelle, Referenzarchitekturen, Beispiele für Automatisierungsartefakte und Anleitungen bereitstellt, um während der Enterprise Cloud-Einführung ein Gleichgewicht zwischen Entwickler- und IT-Governanceanforderungen zu erreichen. Im Mittelpunkt dieses Ansatzes steht das Konzept eines virtuellen Rechenzentrums selbst: die Implementierung von Isolationsgrenzen rund um Ihre Cloudinfrastruktur durch den Einsatz von Zugriffs- und Sicherheitskontrollen, Netzwerkrichtlinien und Complianceüberwachung.

Ein virtuelles Rechenzentrum kann als Ihre eigene isolierte Cloud innerhalb der Azure-Plattform betrachtet werden, die Managementprozesse, gesetzliche Anforderungen und Sicherheitsprozesse integriert, die von Ihren Governancerichtlinien gefordert werden. Innerhalb dieser virtuellen Grenze bietet das virtuelle Azure-Rechenzentrum Beispielmodelle für die Bereitstellung von Workloads bei gleichzeitiger Sicherstellung einer konsistenten Compliance sowie grundlegende Hinweise zur Implementierung der Trennung von Rollen und Verantwortlichkeiten einer Organisation in der Cloud.

### <a name="azure-virtual-datacenter-assumptions"></a>Annahmen für virtuelle Azure-Rechenzentren

Obwohl kleinere Teams von den Modellen und Empfehlungen des virtuellen Azure-Rechenzentrums profitieren können, wurde dieser Ansatz entwickelt, um IT-Gruppen von Unternehmen bei der Verwaltung großer Cloudumgebungen zu unterstützen. Für Organisationen, die die folgenden Kriterien erfüllen, wird empfohlen, bei der Gestaltung der Azure-basierten Cloudinfrastruktur den Leitfaden zum virtuellen Azure-Rechenzentrum zu beachten:

- Ihr Unternehmen unterliegt gesetzlichen Bestimmungen, die eine zentrale Überwachung erfordern.
- Sie müssen die Einhaltung allgemeiner Richtlinien und Governancebestimmungen sowie die zentrale IT-Kontrolle über die wichtigsten Dienste sicherstellen.
- Ihre Branche hängt von einer komplexen Plattform ab, die umfassende Steuerungsmechanismen und tiefgehendes Fachwissen erfordert. Dies ist am häufigsten bei großen Unternehmen in den Bereichen Finanzen, Herstellung, und Öl und Gas der Fall.
- Ihre bestehenden IT-Governancerichtlinien erfordern eine engere Parität mit bestehenden Funktionen, auch in frühen Phasen der Einführung.

Weitere Informationen finden Sie im Artikel zum Framework für die Cloudeinführung im Abschnitt zum [virtuellen Azure-Rechenzentrum](../../reference/vdc.md).

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie einen der Leitfäden aus:

> [!div class="nextstepaction"]
> [Governanceleitfaden für Standardunternehmen](./standard/index.md)
>
> [Governanceleitfaden für komplexe Unternehmen](./complex/index.md)
