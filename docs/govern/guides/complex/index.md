---
title: Governanceleitfaden für komplexe Unternehmen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Governanceleitfaden für komplexe Unternehmen
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 63b66858c023ff85e1ff6f8adc811540f3034e2d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026396"
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

1. Legen Sie eine Verwaltungsgruppe für die einzelnen Geschäftseinheiten mit einer detaillierten Hierarchie fest, die die Geografie und dann den Umgebungstyp (z. B. Produktion oder Nichtproduktion) wiedergibt.
1. Erstellen Sie ein Abonnement für jede eindeutige Kombination von Geschäftseinheit, Geografie, Umgebung und „Kategorisierung der Anwendung“.
1. Erstellen Sie eine separate Ressourcengruppe für jede Anwendung.
1. Wenden Sie [konsistente Benennung](../../../ready/considerations/naming-and-tagging.md) jeder Ebene dieser Gruppierungshierarchie an.

![Diagramm der Ressourcenorganisation für große Unternehmen](../../../_images/govern/large-enterprise-resource-organization.png)

Diese Muster bieten Raum für Wachstum, ohne die Hierarchie unnötig zu verkomplizieren.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

<!-- See comments for suggestion to possibly add here -->

## <a name="incremental-governance-improvements"></a>Inkrementelle Governanceverbesserungen

Sobald dieses MVP bereitgestellt ist, können zusätzliche Ebenen der Governance schnell in die Umgebung integriert werden. Einige Möglichkeiten zur Verbesserung des MVP, um bestimmte Geschäftsanforderungen zu erfüllen:

- [Sicherheitsbaseline für geschützte Daten](./security-baseline-improvement.md)
- [Ressourcenkonfigurationen für unternehmenskritische Anwendungen](./resource-consistency-improvement.md)
- [Steuerelemente für das Kostenmanagement](./cost-management-improvement.md)
- [Große Unternehmen: Multi-Cloud-Entwicklung](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Was bietet dieser Leitfaden?

Im MVP sind Methoden und Tools für die Disziplin der [Beschleunigung der Bereitstellung](../../deployment-acceleration/index.md) festgelegt, um schnell Unternehmensrichtlinien anzuwenden. Insbesondere verwendet das MVP Azure Blueprints, Azure Policy und Azure-Verwaltungsgruppen, um einige grundlegende Unternehmensrichtlinien anzuwenden, wie in der Lösung für das fiktive Unternehmen definiert. Diese Unternehmensrichtlinien werden mithilfe von Azure Resource Manager-Vorlagen und Azure-Richtlinien angewandt, um eine kleine Baseline für Identität und Sicherheit festzulegen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvements-to-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

Im Lauf der Zeit wird dieses Governance-MVP verwendet, um Governancemethoden schrittweise zu verbessern. Mit fortschreitender Einführung wächst das geschäftliche Risiko. Verschiedene Disziplinen im CAF-Governancemodell (Cloud Adoption Framework) werden zur Bewältigung dieser Risiken angepasst. Spätere Artikel dieser Reihe erläutern die Änderungen der Unternehmensrichtlinie, die sich auf das fiktive Unternehmen auswirkt. Diese Änderungen betreffen vier Disziplinen:

- Identitätsbaseline, indem Migrationsabhängigkeiten in der Schilderung weiterentwickelt werden
- Kostenmanagement, wenn die Einführung skaliert wird.
- Sicherheitsbaseline, indem geschützte Daten bereitgestellt werden.
- Ressourcenkonsistenz, indem die IT-Abteilung beginnt, unternehmenskritische Workloads zu unterstützen.

![Beispiel für ein inkrementelles Governance-MVP](../../../_images/govern/governance-improvement-large.png)

## <a name="next-steps"></a>Nächste Schritte

Da Sie jetzt mit dem Governance-MVP und den zukünftigen Änderungen der Governance vertraut sind, lesen Sie die unterstützende Lösung, um zusätzliche Kontextinformationen zu erhalten.

> [!div class="nextstepaction"]
> [Lesen Sie die unterstützende Lösung](./narrative.md)
