---
title: Governanceleitfaden für Standardunternehmen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Governanceleitfaden für Standardunternehmen
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 82467948ae3141ef1f961ab07a503be485a1bc6f
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908454"
---
# <a name="standard-enterprise-governance-guide"></a>Governanceleitfaden für Standardunternehmen

## <a name="overview-of-best-practices"></a>Übersicht über bewährte Methoden

Dieser Governanceleitfaden folgt den Erfahrungen eines fiktiven Unternehmens in verschiedenen Phasen der Governancereife. Er basiert auf echten Kundenerfahrungen. Die empfohlenen Methoden basieren auf den Einschränkungen und Anforderungen des fiktiven Unternehmens.

Als Schnellstartpunkt definiert diese Übersicht ein auf einem ausführlichen Leitfaden basierendes Minimum Viable Product (MVP) für Governance. Sie enthält außerdem Links zu einigen Governanceverbesserungen, die weitere empfohlene Methoden hinzufügen, wenn neue Geschäftsrisiken oder technische Risiken entstehen.

> [!WARNING]
> Dieses MVP ist ein Baselineausgangspunkt, der auf einer Reihe von Annahmen basiert. Auch dieser minimale Satz bewährter Methoden basiert auf Unternehmensrichtlinien, die von beispiellosen geschäftlichen Risiken und Risikotoleranzen bestimmt werden. Um festzustellen, ob diese Annahmen auf Sie zutreffen, lesen Sie die [längere Schilderung](./narrative.md), die diesem Artikel folgt.

### <a name="governance-best-practices"></a>Bewährte Governancemethoden

Auf der Grundlage dieser bewährten Methoden kann eine Organisation schnell und konsistent Governanceleitlinien für Ihre Azure-Abonnements hinzufügen.

### <a name="resource-organization"></a>Ressourcenorganisation

Die folgende Abbildung zeigt die Governance-MVP-Hierarchie zum Organisieren von Ressourcen.

![Diagramm der Ressourcenorganisation](../../../_images/governance/resource-organization.png)

Jede Anwendung sollte im richtigen Bereich der Verwaltungsgruppen-, Abonnement- und Ressourcengruppenhierarchie bereitgestellt werden. Während der Bereitstellungsplanung erstellt das Cloudgovernanceteam die erforderlichen Knoten in der Hierarchie, um die für die Cloudeinführung zuständigen Teams zu unterstützen.

1. Eine Verwaltungsgruppe für jeden Typ von Umgebung (z. B. Produktion, Entwicklung und Test)
2. Zwei Abonnements, eine für die Produktion und eine für die Nichtproduktion
3. Geeignete Ressourcengruppen mit RBAC in diesen Abonnements
4. [Konsistente Benennung](../../../ready/considerations/name-and-tag.md) sollte auf jeder Ebene dieser Gruppierungshierarchie angewendet werden.

Dies ist ein Beispiel für die Anwendung dieses Musters:

![Ressourcenorganisationsbeispiel für ein mittelgroßes Unternehmen](../../../_images/governance/mid-market-resource-organization.png)

Diese Muster bieten Raum für Wachstum, ohne die Hierarchie unnötig zu verkomplizieren.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Iterative Governanceverbesserungen

Sobald dieses MVP bereitgestellt ist, können zusätzliche Ebenen der Governance schnell in die Umgebung integriert werden. Einige Möglichkeiten zur Verbesserung des MVP, um bestimmte Geschäftsanforderungen zu erfüllen:

- [Sicherheitsbaseline für geschützte Daten](./security-baseline-evolution.md)
- [Ressourcenkonfigurationen für unternehmenskritische Anwendungen](./resource-consistency-evolution.md)
- [Steuerelemente für das Kostenmanagement](./cost-management-evolution.md)
- [Steuerelemente für die Multi-Cloud-Entwicklung](./multicloud-evolution.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Was bietet dieser Leitfaden?

Im MVP sind Methoden und Tools für die Disziplin der [Beschleunigung der Bereitstellung](../../deployment-acceleration/index.md) festgelegt, um schnell Unternehmensrichtlinien anzuwenden. Insbesondere verwendet das MVP Azure Blueprints, Azure Policy und Azure-Verwaltungsgruppen, um einige grundlegende Unternehmensrichtlinien anzuwenden, wie in der Lösung für das fiktive Unternehmen definiert. Diese Unternehmensrichtlinien werden mithilfe von Resource Manager-Vorlagen und Azure-Richtlinien angewandt, um eine kleine Baseline für Identität und Sicherheit festzulegen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/governance/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

Im Lauf der Zeit wird dieses Governance-MVP verwendet, um die Governancemethoden zu verbessern. Mit fortschreitender Einführung wächst das geschäftliche Risiko. Verschiedene Disziplinen im CAF-Governancemodell (Cloud Adoption Framework) werden zur Bewältigung dieser Risiken angepasst. Spätere Artikel dieser Reihe erläutern die schrittweise Verbesserung der Unternehmensrichtlinie, die sich auf das fiktive Unternehmen auswirkt. Diese Verbesserungen betreffen drei Disziplinen:

- Kostenmanagement, wenn die Einführung skaliert wird.
- Sicherheitsbaseline, indem geschützte Daten bereitgestellt werden.
- Ressourcenkonsistenz, indem die IT-Abteilung beginnt, unternehmenskritische Workloads zu unterstützen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/governance/governance-evolution.png)

## <a name="next-steps"></a>Nächste Schritte

Da Sie jetzt mit dem Governance-MVP vertraut sind und eine Vorstellung von zukünftigen Verbesserungen der Governance haben, lesen Sie die unterstützende Lösung, um zusätzliche Kontextinformationen zu erhalten.

> [!div class="nextstepaction"]
> [Lesen Sie die unterstützende Lösung](./narrative.md)
