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
ms.openlocfilehash: fc3e2aa9ea201e203c961275f26305cbfd5d45ed
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86450168"
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

Um mit einer Governancelösung zu beginnen, wählen Sie eine der beiden folgenden Optionen aus. Die Optionen basieren auf synthetisierten Kundenerfahrungen. Die Titel basieren auf der Komplexität des Unternehmens zur Vereinfachung der Navigation. Ihre Entscheidung kann komplexer sein. Die folgenden Tabellen zeigen die Unterschiede zwischen den beiden Optionen.

<!-- TODO: Refactor VDC content below. -->
<!-- docsTest:ignore "Azure Virtual Datacenter" -->

> [!WARNING]
> Ein robusterer Ausgangspunkt für die Governance kann erforderlich sein. In solchen Fällen sollten Sie die [CAF-Zielzone auf Unternehmensebene](../../ready/enterprise-scale/index.md) in Betracht ziehen. Beim Ansatz der CAF-Zielzone auf Unternehmensebene stehen Einführungsteams im Fokus, die mittelfristig (innerhalb von 24 Monaten) das Ziel haben, mehr als 1.000 Assets (Infrastruktur, Apps oder Datenassets) in der Cloud zu hosten. Die CAF-Zielzone auf Unternehmensebene ist die erste Wahl für komplexe Governanceszenarien für diese umfangreicheren Cloudeinführungsmaßnahmen.

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
| Kostenverwaltung: Cloudabrechnung | Showbackmodell Abrechnung wird über IT zentralisiert. | Chargebackmodell Die Abrechnung kann durch IT-Beschaffung verteilt werden. |
| Sicherheitsbaseline: Geschützte Daten | Unternehmensfinanzdaten und IP. Eingeschränkte Kundendaten. Keine Complianceanforderungen von Drittanbietern. | Mehrere Sammlungen von Finanzdaten und personenbezogenen Daten von Kunden. Möglicherweise muss Drittanbietercompliance berücksichtigt werden. |

## <a name="caf-enterprise-scale-landing-zone"></a>CAF-Zielzone auf Unternehmensebene

Mit der [CAF-Zielzone auf Unternehmensebene](../../ready/enterprise-scale/index.md) können Sie die Funktionen der Azure-Cloudplattform optimal nutzen und gleichzeitig den Sicherheits- und Governanceanforderungen eines Unternehmens gerecht werden.

Im Vergleich zu herkömmlichen lokalen Umgebungen ermöglicht Azure es Workload-Entwicklungsteams und ihren Geschäftssponsoren, die Vorteile der erhöhten Bereitstellungsagilität von Cloudplattformen zu nutzen. Da sich Ihre Bemühungen zur Cloudeinführung auf unternehmenskritische Daten und Workloads ausdehnen, kann diese Agilität im Widerspruch zu den von Ihren IT-Teams festgelegten Anforderungen an Unternehmenssicherheit und Richtlinieneinhaltung stehen. Dies gilt insbesondere für große Unternehmen, in denen bereits ausgereifte Governance- und Regulierungsanforderungen vorhanden sind.

Die Architektur einer CAF-Zielzone auf Unternehmensebene ist darauf ausgelegt, diese Aspekte im Lebenszyklus der Einführung frühzeitig zu berücksichtigen. Dazu werden Architekturen, Implementierungen und Anleitungen bereitgestellt, um während der Enterprise Cloud-Einführung ein Gleichgewicht zwischen den Anforderungen der Cloudeinführungsteams und des zentralen IT-Teams zu erzielen. Im Mittelpunkt dieses Ansatzes steht das Konzept einer Shared Services-Architektur und gut verwalteter Zielzonen.

Eine CAF-Zielzone auf Unternehmensebene stellt Ihre eigene isolierte Cloud innerhalb der Azure-Plattform bereit, die Managementprozesse, gesetzliche Anforderungen und Sicherheitsprozesse integriert, die von Ihren Governancerichtlinien gefordert werden. Innerhalb dieser virtuellen Grenze bietet die CAF-Zielzone auf Unternehmensebene Beispielmodelle für die Bereitstellung von Workloads bei gleichzeitiger Sicherstellung einer konsistenten Compliance sowie grundlegende Hinweise zur Implementierung der Trennung von Rollen und Verantwortlichkeiten einer Organisation in der Cloud.

### <a name="caf-enterprise-scale-landing-zone-qualifications"></a>Voraussetzungen für die CAF-Zielzone auf Unternehmensebene

Kleinere Teams können von der Architektur und den Empfehlungen der CAF-Zielzone auf Unternehmensebene profitieren. Unser Ziel ist es, die Implementierungen der CAF-Zielzone auf Unternehmensebene weiter zu optimieren, um sie benutzerfreundlicher für kleinere Teams zu gestalten. Derzeit ist dieser Ansatz darauf ausgerichtet, zentrale IT-Teams bei der Verwaltung umfangreicher Cloudumgebungen zu unterstützen.

Beim Ansatz der [CAF-Zielzone auf Unternehmensebene](../../ready/enterprise-scale/index.md) stehen Einführungsteams im Fokus, die mittelfristig (innerhalb von 24 Monaten) das Ziel haben, **mehr als 1.000 Assets (Apps, Infrastruktur- oder Datenassets) in der Cloud zu hosten**.

Bei Organisationen, die die folgenden Kriterien erfüllen, können Sie ebenfalls mit der [CAF-Zielzone auf Unternehmensebene](../../ready/enterprise-scale/index.md) beginnen:

- Ihr Unternehmen unterliegt gesetzlichen Bestimmungen, die eine zentrale Überwachung erfordern.
- Sie müssen die Einhaltung allgemeiner Richtlinien und Governancebestimmungen sowie die zentralisierte IT-Kontrolle über die wichtigsten Dienste sicherstellen.
- Ihre Branche hängt von einer komplexen Plattform ab, die umfassende Steuerungsmechanismen und tiefgehendes Fachwissen erfordert. Dies ist am häufigsten bei großen Unternehmen in den Bereichen Finanzen, Herstellung, und Öl und Gas der Fall.
- Ihre bestehenden IT-Governancerichtlinien erfordern eine engere Parität mit bestehenden Funktionen, auch in frühen Phasen der Einführung.

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie einen der Leitfäden aus:

> [!div class="nextstepaction"]
> [Governanceleitfaden für Standardunternehmen](./standard/index.md)
>
> [Governanceleitfaden für komplexe Unternehmen](./complex/index.md)
