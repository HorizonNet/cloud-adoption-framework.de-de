---
title: Beginnen mit Zielzonen auf Unternehmensebene
description: Beginnen mit Zielzonen auf Unternehmensebene
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1e34cf58fd3f9827a3cf8dd1ffd866fdcfcca1f7
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215227"
---
# <a name="start-with-enterprise-scale-landing-zones"></a>Beginnen mit Zielzonen auf Unternehmensebene

Mitunter ist es für ein Cloudplattformteam nicht ratsam, klein anzufangen und dann zu skalieren. Die Teams arbeiteten jahrelang unter den Einschränkungen der bestehenden lokalen Umgebung des Unternehmens, um den aktuellen Entwicklungsstand in den Bereichen Sicherheit, Betrieb und Governance zu erreichen. Es wird einige Zeit dauern, bis die gewünschten Prozesse, Tools und Architekturen auf der Grundlage der neuen Einschränkungen einer jeden Cloudumgebung repliziert werden können. Um diesen Lernprozess zu beschleunigen, ist ein etwas anderer Startpunkt erforderlich. Beim Vergleich der folgenden Abbildung mit der [frühen Refactoring-Anleitung innerhalb dieser Methodik](../landing-zone/refactor.md) ist die grundlegende Änderung der Startpunkt, der jetzt komplexer ist und zu dem später in diesem Artikel weitere Informationen folgen werden.

![Abbildung zum Refactoring der Zielzone – Beschrieben in einem späteren Abschnitt dieses Artikels](../../_images/ready/refactor-enterprise-scale.png)

<!-- markdownlint-disable MD026 -->

## <a name="qualifiers-should-i-start-with-enterprise-scale"></a>Qualifizierer: Sollte ich auf Unternehmensniveau beginnen?

Bei den meisten Einführungsmustern ist der Ansatz „im kleinen Rahmen starten und erweitern“ vorzuziehen, da er es dem Team ermöglicht, aus realen Erfahrungen zu lernen. Für Unternehmen, die zu den Referenzen in diesem Artikel passen, ist ein stabilerer Ansatz erforderlich.

### <a name="scale-and-speed"></a>Skalierung und Geschwindigkeit

Wenn das Einführungsteam ein mittelfristiges Ziel (innerhalb von 24 Monaten) hat, mehr als 1.000 Assets (Apps, Infrastruktur oder Datenassets) in der Cloud zu hosten, bleibt nicht genug Zeit, um nur durch praktische Ansätze zu lernen. Es müssen mehrere Kriterien voreingestellt werden, um die für ein Großunternehmen erforderliche Geschwindigkeit und Skalierung zu erreichen.

### <a name="security-compliance-and-culture"></a>Sicherheit, Compliance und Kultur

Mehrere Geschäftsmotivationen könnten eine unternehmensweite Zielzone und eine Architektur für gemeinsam genutzte Dienste erfordern, bevor mit der Einführung begonnen werden kann. Der Bedarf an einer Zielzonenlösung auf Unternehmensebene kann für Unternehmen, deren Geschäfte auf vertraulichen Daten und komplexen, voneinander abhängigen Architekturen basieren, offensichtlich sein. Es kann ebenso offensichtlich sein, wenn Unternehmen Cloudumgebungen benötigen, die strenge Anforderungen Dritter erfüllen, bevor sie die Cloud nutzen. Kulturen mit tief verwurzelten Steuerungsmodellen der zentralen IT-Abteilung benötigen möglicherweise auch eine Architektur, die mit einer zentralisierten Steuerung beginnt, um die Anforderungen an die Änderungssteuerung zu erfüllen.

### <a name="all-in-on-the-cloud"></a>Alles in der Cloud

Der häufigste Auslöser für eine Zielzone auf Unternehmensebene kommt von Unternehmen, die sich dafür entscheiden, alles auf die Cloud zu setzen. Dies kann eine Folge der Auflösung eines Rechenzentrums oder einer Massenbewegung sein, um als Unternehmen agiler zu sein. Unabhängig vom Motiv erfordert diese Geschäftsentscheidung in der Regel sowohl die Skalierung als auch die Geschwindigkeit der Einführung. Diese Kombination von Anforderungen gestaltet es schwierig, sich die Zeit zu nehmen, die zum Erlernen und Vorbereiten von vertraulichen Daten und unternehmenskritischem Hosting in der Cloud erforderlich ist.

### <a name="skill-requirements"></a>Qualifikationsanforderungen

Beim Starten auf Unternehmensniveau wird davon ausgegangen, dass das Cloudplattformteam über ein Budget verfügt, das dem Unternehmensniveau entspricht. Dieser Qualifizierer geht davon aus, dass das Team über fundiertere Qualifikationen bezüglich der Cloud verfügt als die meisten anderen Unternehmen. Diese Qualifikationen können aus vergangenen Cloudeinführungen in kleinerem Umfang innerhalb des Unternehmens stammen. Die Qualifikationen können auch durch die Verpflichtung erfahrener Mitarbeiter oder die Zusammenarbeit mit sehr erfahrenen Partnern erweitert werden. Für beide Ausrichtungen sind die folgenden Qualifikationen erforderlich, um auf Unternehmensniveau zu beginnen.

Empfohlene Qualifikationen:

- Umfassende Kenntnisse zur Architektur des gewählten Cloudanbieters.
- Umfassende praktische Erfahrung mit cloudbasierten Infrastructure-as-Code-Ansätzen.
- Angemessene Vertrautheit mit GitHub oder anderen Quellcoderepositorys, einschließlich Branching- und Pull Request-Strategien.
- Umsetzbare Erfahrungen mit automatisierten Bereitstellungen vom Quellcode bis zum Cloudanbieter.

Wenn diese Qualifikationen innerhalb des Cloudplattformteams nicht verfügbar sind (durch Mitarbeiter, Partner oder andere Supportmechanismen), wird der Ansatz „im kleinen Rahmen starten und erweitern“ wahrscheinlich schneller die Unternehmensbereitschaft mit einer qualitativ hochwertigeren Ausgabe erreichen. Ein solcher Ansatz würde einen weniger kostenintensiven Kompetenzerwerb innerhalb des bestehenden Teams ermöglichen.

## <a name="start-with-an-enterprise-scale-landing-zones"></a>Beginnen mit Zielzonen auf Unternehmensebene

Microsoft investiert seit langem in Tools und Ansätze, um Kunden die Entwicklung und Verwaltung von Zielzonen auf Unternehmensniveau zu erleichtern. In den letzten Jahren hat diese Investition zu Leitfäden und Tools in ganz Azure geführt. Dieser Investitionsansatz wird fortgesetzt und kann zu regelmäßigen Aktualisierungen dieses Abschnitts dieses bestimmten Artikels führen.

![Abbildung zum Refactoring der Zielzone](../../_images/ready/refactor-enterprise-scale.png)

Jede der folgenden Vorlagen bietet den Kunden eine anfängliche Zielzone auf Unternehmensniveau mit Infrastrukturmustern:

- [ISO 27001: Gemeinsame Dienste](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared)
- [ISO 27001: App Service-Umgebungs-/SQL-Datenbank-Workload](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload)
- [UK Official und UK NHS: Governance](https://docs.microsoft.com/azure/governance/blueprints/samples/ukofficial)

Die zusätzlichen Beispiele im Artikel [Azure-Blaupausenbeispiele](https://docs.microsoft.com/azure/governance/blueprints/samples) können als „Rot/Grün“-Test für Zielzonen auf Unternehmensebene verwendet werden. Die Anwendung dieser Blaupausen würde sicherstellen, dass eine Umgebung vor der Einführung die Konformitätsstandard erfüllt. Dieser spätere Ansatz ist besonders nützlich, um Zielzonen von Drittanbietern oder Partnern zu überprüfen, bevor die Cloud eingeführt wird:

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie eine der Zielzonenblaupausen auf Unternehmensebene aus.
Von dort aus kann derselbe Leitfaden in [im kleinem Rahmen starten und erweitern](./index.md) verwendet werden, um Ihre unternehmensweiten Zielzonen so zu erweitern, dass sie Ihren unterschiedlichen Anforderungen entsprechen.

> [!div class="nextstepaction"]
> [Setzen Sie den Leitfaden „im kleinen Rahmen starten und erweitern“ fort, indem Sie Ihre Zielzone auf Unternehmensebene als anfängliche Quelle nutzen.](./index.md)
