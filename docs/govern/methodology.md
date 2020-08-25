---
title: Governancemethodik für die Cloud
description: Verwenden Sie einen inkrementellen, auf einem Minimum Viable Product (MVP) basierenden Governanceansatz, um Unternehmensrichtlinien zu unterstützen und eine schnelle Cloudeinführung zu ermöglichen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 8fee6b827beec0311054f1cdf5514f8c4910f3a7
ms.sourcegitcommit: 949b87bad28d32df84df190160089f01826f3a31
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88195521"
---
# <a name="govern-methodology-for-the-cloud"></a>Governancemethodik für die Cloud

Die Einführung der Cloud ist eine Reise und nicht ein Ziel. Auf dem Weg dorthin gibt es klare Meilensteine und konkrete Geschäftsvorteile. Der endgültige Zustand der Cloudeinführung ist hingegen unbekannt, wenn ein Unternehmen diese Reise beginnt. Cloud Governance schafft Absicherungen, die das Unternehmen während der gesamten Reise auf einem sicheren Weg halten.

Das Framework für die Cloudeinführung (Cloud Adoption Framework) bietet Governanceleitfäden, in denen Erfahrungen fiktiver Unternehmen beschrieben werden, denen Erfahrungen realer Kunden zugrunde liegen. Jeder Leitfaden begleitet den Kunden bei den Governanceaspekten seiner Cloudeinführung.

## <a name="envision-an-end-state"></a>Planen des Endzustands

Eine Reise ohne Zielort ist nur eine Wanderung. Es ist wichtig, eine ungefähre Vorstellung vom Endzustand zu erhalten, bevor der erste Schritt unternommen wird. Die folgende Infografik stellt einen Bezugsrahmen für den Endzustand dar. Dies ist nicht Ihr Ausgangspunkt, sondern zeigt Ihr potenzielles Ziel.

![Infografik des Cloud Adoption Framework-Governancemodells](../_images/operational-transformation-govern-large.png)

Das Cloud Adoption Framework-Governancemodell identifiziert wichtige Bereiche von Bedeutung während der Reise. Jeder Bereich bezieht sich auf verschiedene Arten von Risiken, denen sich das Unternehmen bei der Einführung weiterer Clouddienste stellen muss. Im Rahmen dieses Frameworks identifiziert der Governanceleitfaden erforderliche Aktionen für das Cloudgovernanceteam. Dabei wird jedes Prinzip des Cloud Adoption Framework-Governancemodells näher beschrieben. Dazu gehören im Allgemeinen:

**Unternehmensrichtlinien**: Unternehmensrichtlinien steuern die Cloud Governance. Der Governanceleitfaden konzentriert sich auf bestimmte Aspekte der Unternehmensrichtlinie:

- **Geschäftsrisiken**: Identifizieren und Verstehen von Unternehmensrisiken.
- **Richtlinie und Compliance**: Konvertieren von Risiken in Richtlinienanweisungen, die beliebige Compliancevorgaben unterstützen.
- **Prozesse**: Sicherstellen der Befolgung der angegebenen Richtlinien.

**Fünf Disziplinen der Cloud Governance**: Diese Disziplinen unterstützen die Unternehmensrichtlinien. Jede Disziplin schützt das Unternehmen vor potenziellen Fallstricken:

- Disziplin „Kostenverwaltung“
- Disziplin „Sicherheitsbaseline“
- Disziplin „Ressourcenkonsistenz“
- Disziplin „Identitätsbaseline“
- Disziplin „Beschleunigung der Bereitstellung“

Unternehmensrichtlinien dienen im Wesentlichen als Frühwarnsystem zur Erkennung potenzieller Probleme. Die Disziplinen helfen dem Unternehmen, Risiken zu kontrollieren und Absicherungen zu erstellen.

## <a name="grow-to-the-end-state"></a>Wachsen bis zum Endzustand

Da sich die Governanceanforderungen im Lauf der Cloudeinführung ändern, ist ein anderer Ansatz für Governance erforderlich. Unternehmen können nicht länger warten, bis ein kleines Team bildlich gesprochen auf jeder Autobahn Leitplanken anbringt und Landkarten erstellt, **bevor sie den ersten Schritt machen**. Geschäftsergebnisse werden schneller und reibungsloser erwartet. Die IT-Governance muss sich zudem schnell weiterentwickeln und mit den Geschäftsanforderungen Schritt halten, um bei der Einführung der Cloud relevant zu bleiben und „Schatten-IT“ zu vermeiden.

Ein _inkrementeller Governance_ansatz stärkt diese Eigenschaften. Inkrementelle Governance basiert auf einer kleinen Sammlung von Unternehmensrichtlinien, -prozessen und -tools, um eine Grundlage für die Einführung und Governance zu schaffen. Diese Grundlage wird als _Minimum Viable Product (MVP)_ bezeichnet. Ein MVP ermöglicht es dem Governance-Team, Governance schnell in Implementierungen während des gesamten Einführungszyklus zu integrieren. Ein MVP kann zu jedem Zeitpunkt während des Cloudeinführungsprozesses eingerichtet werden. Es hat sich bewährt, ein MVP so früh wie möglich einzuführen.

Die Fähigkeit, schnell auf Risikoveränderungen zu reagieren, eröffnet dem Cloudgovernanceteam neue Möglichkeiten. Das Cloudgovernanceteam kann sich dem Cloudstrategieteam als Scouts anschließen und den Cloudeinführungsteams vorauseilen, Routen planen und schnell Absicherungen einrichten, um Risiken im Zusammenhang mit den Einführungsplänen zu managen. Diese Just-in-time-Governanceebenen werden als _Governanceiterationen_ bezeichnet. Mit diesem Ansatz ist die Governancestrategie den Cloudeinführungsteams einen Schritt voraus.

Die folgende Abbildung zeigt ein einfaches Governance-MVP und drei Governanceiterationen. Im Lauf der Iterationen werden zusätzliche Unternehmensrichtlinien definiert, um neue Risiken zu mindern. Die Bereitstellungsbeschleunigungsdisziplin wendet diese Änderungen dann bei jeder Bereitstellung an.

![Beispiel für inkrementelle Governanceverbesserungen](../_images/govern/incremental-governance-example.png)

> [!NOTE]
> Governance ist kein Ersatz für Schlüsselfunktionen wie Sicherheit, Netzwerk, Identität, Finanzen, DevOps oder Betrieb. Auf dem Weg dorthin wird es Interaktionen mit und Abhängigkeiten von Mitgliedern aus jeder Funktion geben. Diese Mitglieder sollten in das Cloudgovernanceteam eingebunden werden, um Entscheidungen und Maßnahmen zu beschleunigen.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das Governance-Benchmarktool im Cloud Adoption Framework verwenden, um Ihre Transformationsjourney zu bewerten und Schwachstellen in Ihrer Organisation in sechs Schlüsselbereichen zu ermitteln, die im Framework definiert sind.

> [!div class="nextstepaction"]
> [Bewerten der Transformationsjourney](./benchmark.md)
