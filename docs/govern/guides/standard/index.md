---
title: Governanceleitfaden für Standardunternehmen
description: Verfolgen Sie ein fiktives Standardunternehmen in den verschiedenen Phasen der Governancereife, das ein MVP (Minimum Viable Product) basierend auf Best Practices definiert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 67412e36a4048d1441679458bbff5a90bbceaa84
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214775"
---
# <a name="standard-enterprise-governance-guide"></a>Governanceleitfaden für Standardunternehmen

## <a name="overview-of-best-practices"></a>Übersicht über bewährte Methoden

Dieser Governanceleitfaden folgt den Erfahrungen eines fiktiven Unternehmens in verschiedenen Phasen der Governancereife. Er basiert auf echten Kundenerfahrungen. Die bewährten Methoden basieren auf den Einschränkungen und Anforderungen des fiktiven Unternehmens.

Als Schnellstartpunkt definiert diese Übersicht ein auf bewährten Methoden basierendes Minimum Viable Product (MVP) für die Governance. Sie enthält außerdem Links zu einigen Governanceverbesserungen, die weitere bewährte Methoden hinzufügen, wenn neue Geschäftsrisiken oder technische Risiken entstehen.

> [!WARNING]
> Dieses MVP ist ein Baselineausgangspunkt, der auf einer Reihe von Annahmen basiert. Auch dieser minimale Satz bewährter Methoden basiert auf Unternehmensrichtlinien, die von beispiellosen geschäftlichen Risiken und Risikotoleranzen bestimmt werden. Um festzustellen, ob diese Annahmen auf Sie zutreffen, lesen Sie die [längere Schilderung](./narrative.md), die diesem Artikel folgt.

### <a name="governance-best-practices"></a>Bewährte Governancemethoden

Auf der Grundlage dieser bewährten Methoden kann eine Organisation schnell und konsistent Governanceleitlinien für Ihre Azure-Abonnements hinzufügen.

### <a name="resource-organization"></a>Ressourcenorganisation

Die folgende Abbildung zeigt die Governance-MVP-Hierarchie zum Organisieren von Ressourcen.

![Diagramm der Ressourcenorganisation](../../../_images/govern/resource-organization.png)

Jede Anwendung sollte im richtigen Bereich der Verwaltungsgruppen-, Abonnement- und Ressourcengruppenhierarchie bereitgestellt werden. Während der Bereitstellungsplanung erstellt das Cloudgovernanceteam die erforderlichen Knoten in der Hierarchie, um die für die Cloudeinführung zuständigen Teams zu unterstützen.

1. Eine Verwaltungsgruppe für jeden Typ von Umgebung (z. B. Produktion, Entwicklung und Test)
2. Zwei Abonnements, eins für die Produktionsworkloads und eins für Nichtproduktionsworkloads
3. [Konsistente Benennung](../../../ready/azure-best-practices/naming-and-tagging.md) sollte auf jeder Ebene dieser Gruppierungshierarchie angewendet werden.
4. Bei der Ressourcengruppenbereitstellung muss der Lebenszyklus der Inhalte berücksichtigt werden: Alle Inhalte, die gemeinsam entwickelt, verwaltet und ausgemustert werden, gehören zusammen. Weitere Informationen zu bewährten Methoden für Ressourcengruppen finden Sie [hier](../../../decision-guides/resource-consistency/index.md).
5. Die [Regionswahl](../../../migrate/azure-best-practices/multiple-regions.md) ist äußerst wichtig und muss berücksichtigt werden, damit sowohl Netzwerk- und Überwachungsfunktionen für Failover-/Failbackvorgänge als auch die [erforderlichen SKUs in den bevorzugten Regionen](https://azure.microsoft.com/global-infrastructure/services) zur Verfügung stehen.

Dies ist ein Beispiel für die Anwendung dieses Musters:

![Ressourcenorganisationsbeispiel für ein mittelgroßes Unternehmen](../../../_images/govern/mid-market-resource-organization.png)

Diese Muster bieten Raum für Wachstum, ohne die Hierarchie unnötig zu verkomplizieren.

[!INCLUDE [governance-of-resources](../../../../includes/governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Iterative Governanceverbesserungen

Sobald dieses MVP bereitgestellt ist, können zusätzliche Ebenen der Governance schnell in die Umgebung integriert werden. Einige Möglichkeiten zur Verbesserung des MVP, um bestimmte Geschäftsanforderungen zu erfüllen:

- [Sicherheitsbaseline für geschützte Daten](./security-baseline-improvement.md)
- [Ressourcenkonfigurationen für unternehmenskritische Anwendungen](./resource-consistency-improvement.md)
- [Steuerelemente für die Kostenverwaltung](./cost-management-improvement.md)
- [Steuerelemente für die Multi-Cloud-Entwicklung](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Was bietet dieser Leitfaden?

Im MVP sind Methoden und Tools für die [Disziplin der Beschleunigung der Bereitstellung](../../deployment-acceleration/index.md) festgelegt, um Unternehmensrichtlinien schnell anwenden zu können. Insbesondere verwendet das MVP Azure Blueprints, Azure Policy und Azure-Verwaltungsgruppen, um einige grundlegende Unternehmensrichtlinien anzuwenden, wie in der Lösung für das fiktive Unternehmen definiert. Diese Unternehmensrichtlinien werden mithilfe von Resource Manager-Vorlagen und Azure-Richtlinien angewandt, um eine kleine Baseline für Identität und Sicherheit festzulegen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

Im Lauf der Zeit wird dieses Governance-MVP verwendet, um die Governancemethoden zu verbessern. Mit fortschreitender Einführung wächst das geschäftliche Risiko. Verschiedene Disziplinen im CAF-Governancemodell (Cloud Adoption Framework) werden zur Bewältigung dieser Risiken angepasst. Spätere Artikel dieser Reihe erläutern die schrittweise Verbesserung der Unternehmensrichtlinie, die sich auf das fiktive Unternehmen auswirkt. Diese Verbesserungen betreffen drei Disziplinen:

- Kostenverwaltung, wenn die Einführung skaliert wird.
- Sicherheitsbaseline, wenn geschützte Daten bereitgestellt werden.
- Ressourcenkonsistenz, wenn das IT-Betriebsteam beginnt, unternehmenskritische Workloads zu unterstützen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-improvement.png)

## <a name="next-steps"></a>Nächste Schritte

Da Sie jetzt mit dem Governance-MVP vertraut sind und eine Vorstellung von zukünftigen Verbesserungen der Governance haben, lesen Sie die unterstützende Lösung, um zusätzliche Kontextinformationen zu erhalten.

> [!div class="nextstepaction"]
> [Lesen Sie die unterstützende Lösung](./narrative.md)
