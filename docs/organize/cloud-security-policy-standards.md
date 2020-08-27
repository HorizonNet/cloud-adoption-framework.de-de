---
title: Funktion von Cloudsicherheitsrichtlinie und -standards
description: Grundlegendes zur Funktion von Cloudsicherheitsrichtlinie und -standards.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: c9a141575b8978eb5f16b51b7c5139801bb0fb66
ms.sourcegitcommit: 8b5fdb68127c24133429b4288f6bf9004a1d1253
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88848294"
---
# <a name="function-of-cloud-security-policy-and-standards"></a>Funktion von Cloudsicherheitsrichtlinie und -standards

Sicherheitsrichtlinien- und standardsteams erstellen, genehmigen und veröffentlichen Sicherheitsrichtlinien und -standards, um Sicherheitsentscheidungen innerhalb der Organisation zu steuern.

Die Richtlinien und Standards sollten:

- Die Sicherheitsstrategie der Organisation detailliert genug wiedergeben, um Entscheidungen in der Organisation durch verschiedene Teams zu steuern.
- Produktivität im gesamten Unternehmen ermöglichen und gleichzeitig das Risiko für das Geschäft und die Mission der Organisation verringern.

**Sicherheitsrichtlinien** sollten langfristige nachhaltige Ziele widerspiegeln, die an der Sicherheitsstrategie und Risikotoleranz der Organisation ausgerichtet sind. Richtlinien sollten immer Folgendes behandeln:

- Einhaltung gesetzlicher Bestimmungen und aktueller Compliancestatus (Anforderungen erfüllt, Risiken akzeptiert usw.)
- Bewertung des aktuellen Zustands unter Architekturaspekten sowie was sich technisch möglich entwickeln, implementieren und durchsetzen lässt
- Organisationskultur und -einstellungen
- Bewährte Branchenmethoden
- Verantwortlichkeit von Sicherheitsrisiken, die entsprechenden Geschäftsbeteiligten zugewiesen sind, die für weitere Risiken und Geschäftsergebnisse verantwortlich sind.

**Sicherheitsstandards** definieren die Prozesse und Regeln, um die Ausführung der Sicherheitsrichtlinie zu unterstützen.

## <a name="modernization"></a>Modernisierung

Obwohl Richtlinien statisch bleiben sollten, sollten Standards dynamisch sein und fortlaufend neu bewertet werden, um mit den Änderungen in der Cloudtechnologie, Bedrohungsumgebung und geschäftlichen Wettbewerbslandschaft Schritt zu halten.

Aufgrund dieser hohen Änderungsrate sollten Sie genau beobachten, wie viele Ausnahmen gemacht werden, da dies darauf hindeuten kann, dass Standards (oder Richtlinien) angepasst werden müssen.

Sicherheitsstandards sollten Anleitungen enthalten, die für die Einführung der Cloud spezifisch sind, z. B.:

- Sichere Verwendung von Cloudplattformen zum Hosten von Workloads
- Sichere Verwendung von DevOps-Modellen und Einbindung von Cloudanwendungen, APIs und Diensten in die Entwicklung
- Verwendung von Kontrollen des Identitätsumkreises, um Kontrollen des Netzwerkumkreises zu ergänzen oder zu ersetzen
- Definieren Ihrer Segmentierungsstrategie vor dem Verlagern Ihrer Workloads auf die IaaS-Plattform
- Markieren und Klassifizieren der Vertraulichkeit von Ressourcen
- Definieren eines Prozesses zur Bewertung und Sicherstellung, dass Ihre Assets ordnungsgemäß konfiguriert und geschützt sind

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Cloudsicherheitsrichtlinie und -standards werden üblicherweise von den folgenden Arten von Rollen bereitgestellt. Die Organisationsrichtlinie sollte Folgende informieren (und von diesen informiert werden):

- Sicherheitsarchitekturen
- Compliance- und Risikomanagementteams
- Führungskräfte und Vertreter von Geschäftseinheiten
- Informationstechnologie
- Auditing- und juristische Teams

Die Richtlinie sollte auf Grundlage vieler Eingaben/Anforderungen aus dem gesamten Unternehmen optimiert werden, einschließlich, aber nicht beschränkt auf jene, die [Diagramm der Sicherheitsübersicht](./cloud-security.md) dargestellt sind.

## <a name="next-steps"></a>Nächste Schritte

Sehen Sie sich die Funktion eines [Cloud Security Operations Centers](./cloud-security-operations-center.md) (SOC) an.
