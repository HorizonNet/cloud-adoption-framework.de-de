---
title: Entwurfsrichtlinien für das Cloud Adoption Framework auf Unternehmensebene
description: Erfahren Sie mehr über die Entwurfsrichtlinien für die Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c3a093d92777f41783cd47478f2a72dc3fa0c2ad
ms.sourcegitcommit: d31a9043d1ae9283ed126bf118ca26d1d18d6948
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88040880"
---
# <a name="cloud-adoption-framework-enterprise-scale-design-guidelines"></a>Entwurfsrichtlinien für das Cloud Adoption Framework auf Unternehmensebene

In diesem Artikel und in der folgenden Artikelserie wird dargelegt, wie die unternehmensweite Architektur eine wertende Position zu jedem der [Entwurfsbereiche von Azure-Zielzonen](../landing-zone/design-areas.md) bietet. In dieser Reihe werden einige ausführliche Entwurfsrichtlinien bereitgestellt, die befolgt werden können, um die in der unternehmensweiten Lösung verankerten Entwurfsprinzipien umzusetzen.

Der Kern der unternehmensweiten Architektur enthält einen kritischen Entwurfspfad, der aus grundlegenden Entwurfsthemen mit sehr eng zusammenhängenden und abhängigen Entwurfsentscheidungen besteht. Dieses Repository bietet eine Entwurfsanleitung für diese architektonisch bedeutsamen technischen Bereiche, um die kritischen Entwurfsentscheidungen zu unterstützen, die zur Definition der unternehmensweiten Architektur getroffen werden müssen. Für jeden der betrachteten Bereiche überprüfen Sie die bereitgestellten Überlegungen und Empfehlungen und verwenden diese, um die Entwürfe innerhalb jedes Bereichs zu strukturieren und voranzubringen.

Sie könnten z. B. fragen, wie viele Abonnements für Ihre Umgebung erforderlich sind. Sie können die [Organisation und Governance von Abonnements](./management-group-and-subscription-organization.md#subscription-organization-and-governance) durchsehen und die dargelegten Empfehlungen befolgen, um Entscheidungen zu Abonnements zu treffen.

## <a name="critical-design-areas"></a>Wichtige Entwurfsbereiche

Die folgenden acht wichtigen Entwurfsbereiche können Ihnen bei der Übersetzung Ihrer Anforderungen in Azure-Konstrukte und -Funktionen helfen. Dieser Entwurf kann Ihnen helfen, die Diskrepanz zwischen der lokalen und der Cloudentwurfsinfrastruktur zu beseitigen, die in der Regel zu Dissonanzen und Reibungen zwischen der Definition auf Unternehmensebene und der Azure-Einführung führt.

Die Auswirkungen von Entscheidungen, die in diesen kritischen Bereichen getroffen werden, werden in der gesamten unternehmensweiten Architektur nachhallen und andere Entscheidungen beeinflussen. Machen Sie sich mit diesen acht Bereichen vertraut, um die Konsequenzen herbeigeführter Entscheidungen besser zu verstehen, die später zu Kompromissen in verwandten Bereichen führen können.

- [Enterprise Agreement-Registrierung und Azure Active Directory-Mandanten](./enterprise-enrollment-and-azure-ad-tenants.md)
- [Identitäts- und Zugriffsverwaltung](./identity-and-access-management.md)
- [Organisation von Verwaltungsgruppen und Abonnements](./management-group-and-subscription-organization.md)
- [Netzwerktopologie und -konnektivität](./network-topology-and-connectivity.md)
- [Verwaltung und Überwachung](./management-and-monitoring.md)
- [Business Continuity & Disaster Recovery](./business-continuity-and-disaster-recovery.md)
- [Sicherheit, Governance und Compliance](./security-governance-and-compliance.md)
- [Plattformautomatisierung und DevOps](./platform-automation-and-devops.md)
