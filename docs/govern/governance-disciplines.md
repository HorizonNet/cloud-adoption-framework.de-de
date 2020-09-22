---
title: Die fünf Disziplinen der Cloud-Governance
description: Verwenden Sie das Cloud Adoption Framework für Azure, um sich über die Disziplinen „Kostenverwaltung“, „Sicherheitsbaseline“, „Identitätsbaseline“, „Ressourcenkonsistenz“ und „Bereitstellungsbeschleunigung“ zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: daf25b3027d0eb5becff23c96fa9bd2f6f30476d
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89605011"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Die fünf Disziplinen der Cloud-Governance

<!-- docutune:casing "Disciplines of Cloud Governance" "Cost Management" "Security Baseline" "Identity Baseline" "Resource Consistency" "Deployment Acceleration" -->

:::row:::
    :::column:::
        Jede Änderung von Geschäftsprozessen oder Technologieplattformen birgt Risiken. Cloudgovernanceteams, deren Mitglieder manchmal auch als Cloudverwalter bezeichnet werden, haben die Aufgabe, diese Risiken mit minimaler Unterbrechung der Einführungs- oder Innovationsanstrengungen zu minimieren. <br><br> Das Governancemodell des Cloud Adoption Frameworks steuert diese Entscheidungen (unabhängig von der ausgewählten Cloudplattform), indem es sich auf die [Entwicklung der Unternehmensrichtlinien](./corporate-policy.md) und die [fünf Disziplinen der Cloudgovernance](#disciplines-of-cloud-governance) konzentriert. [Umsetzbare Entwurfsleitfäden](./guides/index.md) zeigen dieses Modell mithilfe von Azure-Diensten. Im Folgenden werden die Disziplinen des Governancemodells im Framework für die Cloudeinführung erläutert.
    :::column-end:::
    :::column:::
        [![Abbildung des Governancemodells des Cloud Adoption Frameworks: Unternehmensrichtlinien und Governancedusziplinen](../_images/operational-transformation-govern-thumbnail.png)](../_images/operational-transformation-govern-large.png#lightbox) <br> *Abbildung 1: Visuelle Darstellung der Unternehmensrichtlinie und der fünf Disziplinen von Cloud Governance.*
    :::column-end:::
:::row-end:::

## <a name="disciplines-of-cloud-governance"></a>Disziplinen von Cloud Governance

Für jede Cloudplattform gibt es allgemeine Governancedisziplinen, die als Leitfaden dienen können, um Richtlinien zu formulieren und Toolketten anzupassen. Diese Disziplinen sind ausschlaggebend für Entscheidungen über den richtigen Automatisierungsgrad und die Durchsetzung von Unternehmensrichtlinien auf Cloudplattformen.

| <span title="Symbol">&nbsp;</span> | <span title="Beschreibung">&nbsp;</span> |
|--|--|
| <br> ![Cost Management](../_images/govern/cost-management.png) | <br> [Cost Management](./cost-management/index.md): Die Kosten sind für Cloudbenutzer ein Hauptanliegen. Entwickeln Sie Richtlinien zur Kostenkontrolle für alle Cloudplattformen. |
| <br> ![Sicherheitsbaseline](../_images/govern/security-baseline.png) | <br> [Sicherheitsbaseline](./security-baseline/index.md): Sicherheit ist ein komplexes Thema, das für jedes Unternehmen einzigartig ist. Sobald die Sicherheitsanforderungen festgelegt sind, wenden Cloudgovernancerichtlinien und -durchsetzung diese Anforderungen auf Netzwerk-, Daten- und Ressourcenkonfigurationen an.|
| <br> ![Identitätsbaseline](../_images/govern/identity-baseline.png) | <br> [Identitätsbaseline](./identity-baseline/index.md): Inkonsistenzen bei der Anwendung von Identitätsanforderungen können das Risiko von Sicherheitsverletzungen erhöhen. Die Identitätsbaseline-Disziplin stellt hauptsächlich sicher, dass die Identität bei der Cloudeinführung konsistent angewendet wird. |
| <br> ![Ressourcenkonsistenz](../_images/govern/resource-consistency.png) | <br> [Ressourcenkonsistenz](./resource-consistency/index.md): Cloudvorgänge hängen von einer konsistenten Ressourcenkonfiguration ab. Durch Governancetools können Ressourcen konsistent konfiguriert werden, um Risiken im Zusammenhang mit Onboarding, Abweichung, Erkennbarkeit und Wiederherstellung zu umgehen. |
| <br> ![Beschleunigung der Bereitstellung](../_images/govern/deployment-acceleration.png) | <br> [Beschleunigung der Bereitstellung](./deployment-acceleration/index.md): Zentralisierung, Standardisierung und Konsistenz bei Bereitstellungs- und Konfigurationsansätzen verbessern die Governancepraktiken. Wenn diese Aspekte über cloudbasierte Governancetools bereitgestellt werden, schaffen sie einen Cloudfaktor, der die Bereitstellungsaktivitäten beschleunigen kann. |
