---
title: Governanceleitfaden für komplexe Unternehmen
description: Verfolgen Sie ein fiktives komplexes Unternehmen in den verschiedenen Phasen der Governancereife, das ein MVP (Minimum Viable Product) basierend auf Best Practices definiert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c3c22c3ad69b7c08a2b2c3da2fbec22957e44915
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86191398"
---
# <a name="governance-guide-for-complex-enterprises"></a>Governanceleitfaden für komplexe Unternehmen

## <a name="overview-of-best-practices"></a>Übersicht über bewährte Methoden

Dieser Governanceleitfaden folgt den Erfahrungen eines fiktiven Unternehmens in verschiedenen Phasen der Governancereife. Er basiert auf echten Kundenerfahrungen. Die empfohlenen bewährten Methoden basieren auf den Einschränkungen und Anforderungen des fiktiven Unternehmens.

Als Schnellstartpunkt definiert diese Übersicht ein auf bewährten Methoden basierendes Minimum Viable Product (MVP) für die Governance. Sie enthält außerdem Links zu einigen Governanceverbesserungen, die weitere bewährte Methoden hinzufügen, wenn neue Geschäftsrisiken oder technische Risiken entstehen.

> [!WARNING]
> Dieses MVP ist ein Baselineausgangspunkt, der auf einer Reihe von Annahmen basiert. Auch dieser minimale Satz bewährter Methoden basiert auf Unternehmensrichtlinien, die von beispiellosen geschäftlichen Risiken und Risikotoleranzen bestimmt werden. Um festzustellen, ob diese Annahmen auf Sie zutreffen, lesen Sie die [längere Schilderung](./narrative.md), die diesem Artikel folgt.

### <a name="governance-best-practices"></a>Bewährte Governancemethoden

Auf der Grundlage dieser bewährten Methoden kann eine Organisation schnell und konsistent Governanceleitlinien für mehrere Azure-Abonnements hinzufügen.

### <a name="resource-organization"></a>Ressourcenorganisation

Die folgende Abbildung zeigt die Governance-MVP-Hierarchie zum Organisieren von Ressourcen.

![Diagramm der Ressourcenorganisation](../../../_images/govern/resource-organization.png)

Jede Anwendung sollte im richtigen Bereich der Verwaltungsgruppen-, Abonnement- und Ressourcengruppenhierarchie bereitgestellt werden. Während der Bereitstellungsplanung erstellt das Cloudgovernanceteam die erforderlichen Knoten in der Hierarchie, um die für die Cloudeinführung zuständigen Teams zu unterstützen.

1. Legen Sie eine Verwaltungsgruppe für die einzelnen Geschäftseinheiten mit einer detaillierten Hierarchie fest, in der zuerst die Geografie und dann der Umgebungstyp (z. B. Produktions- oder andere Umgebungen) widergespiegelt wird.

1. Erstellen Sie für jede individuelle Kombination aus separater Geschäftseinheit oder Geografie ein produktionsbezogenes und ein produktionsfremdes Abonnement. Beim Erstellen mehrerer Abonnements sollte mit Bedacht vorgegangen werden. Weitere Informationen finden Sie im [Leitfaden zur Entscheidungsfindung für Abonnements](../../../decision-guides/subscriptions/index.md).

1. Wenden Sie [konsistente Benennung](../../../ready/azure-best-practices/naming-and-tagging.md) jeder Ebene dieser Gruppierungshierarchie an.

1. Bei der Bereitstellung von Ressourcengruppen sollte der Inhaltslebenszyklus berücksichtigt werden. Ressourcen, die zusammen entwickelt, verwaltet und ausgesondert werden, sollten in derselben Ressourcengruppe angeordnet sein. Weitere Informationen zu den bewährten Methoden zur Verwendung von Ressourcengruppen finden Sie [hier](../../../decision-guides/resource-consistency/index.md).

1. Die [Regionswahl](../../../migrate/azure-best-practices/multiple-regions.md) ist äußerst wichtig und muss berücksichtigt werden, damit sowohl Netzwerk- und Überwachungsfunktionen für Failover-/Failbackvorgänge als auch die [erforderlichen SKUs in den bevorzugten Regionen](https://azure.microsoft.com/global-infrastructure/services) zur Verfügung stehen.

![Diagramm der Ressourcenorganisation für große Unternehmen](../../../_images/govern/large-enterprise-resource-organization.png)

Diese Muster bieten Raum für Wachstum, ohne die Hierarchie unnötig zu verkomplizieren.

[!INCLUDE [governance-of-resources](../../../../includes/governance-of-resources.md)]

<!-- TODO: See comments for suggestion to possibly add here -->

## <a name="incremental-governance-improvements"></a>Inkrementelle Governanceverbesserungen

Sobald dieses MVP bereitgestellt ist, können zusätzliche Ebenen der Governance schnell in die Umgebung integriert werden. Einige Möglichkeiten zur Verbesserung des MVP, um bestimmte Geschäftsanforderungen zu erfüllen:

- [Sicherheitsbaseline für geschützte Daten](./security-baseline-improvement.md)
- [Ressourcenkonfigurationen für unternehmenskritische Anwendungen](./resource-consistency-improvement.md)
- [Steuerelemente für die Kostenverwaltung](./cost-management-improvement.md)
- [Große Unternehmen: Multi-Cloud-Entwicklung](./multicloud-improvement.md)

## <a name="what-does-this-guidance-provide"></a>Was bietet dieser Leitfaden?

Im MVP sind Methoden und Tools für die [Disziplin der Beschleunigung der Bereitstellung](../../deployment-acceleration/index.md) festgelegt, um Unternehmensrichtlinien schnell anwenden zu können. Insbesondere verwendet das MVP Azure Blueprints, Azure Policy und Azure-Verwaltungsgruppen, um einige grundlegende Unternehmensrichtlinien anzuwenden, wie in der Lösung für das fiktive Unternehmen definiert. Diese Unternehmensrichtlinien werden mithilfe von Azure Resource Manager-Vorlagen und Azure-Richtlinien angewandt, um eine kleine Baseline für Identität und Sicherheit festzulegen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvements-to-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

Im Lauf der Zeit wird dieses Governance-MVP verwendet, um Governancemethoden schrittweise zu verbessern. Mit fortschreitender Einführung wächst das geschäftliche Risiko. Verschiedene Disziplinen im CAF-Governancemodell (Cloud Adoption Framework) werden zur Bewältigung dieser Risiken angepasst. Spätere Artikel dieser Reihe erläutern die Änderungen der Unternehmensrichtlinie, die sich auf das fiktive Unternehmen auswirkt. Diese Änderungen betreffen vier Disziplinen:

- Identitätsbaseline, wenn Migrationsabhängigkeiten in der Lösung weiterentwickelt werden.
- Kostenverwaltung, wenn die Einführung skaliert wird.
- Sicherheitsbaseline, wenn geschützte Daten bereitgestellt werden.
- Ressourcenkonsistenz, wenn das IT-Betriebsteam beginnt, unternehmenskritische Workloads zu unterstützen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-improvement-large.png)

## <a name="next-steps"></a>Nächste Schritte

Da Sie jetzt mit dem Governance-MVP und den zukünftigen Änderungen der Governance vertraut sind, lesen Sie die unterstützende Lösung, um zusätzliche Kontextinformationen zu erhalten.

> [!div class="nextstepaction"]
> [Lesen Sie die unterstützende Lösung](./narrative.md)
