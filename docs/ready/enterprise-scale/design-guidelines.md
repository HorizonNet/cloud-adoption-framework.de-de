---
title: CAF-Entwurfsrichtlinien für die Unternehmensebene
description: Erfahren Sie mehr über die Entwurfsrichtlinien für die Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1764c949d48ee2a68a13e2cff251a6949f9933ef
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194747"
---
# <a name="caf-enterprise-scale-design-guidelines"></a>CAF-Entwurfsrichtlinien für die Unternehmensebene

In diesem Artikel und in der folgenden Artikelserie wird dargelegt, wie die unternehmensweite Architektur eine wertende Position zu jedem der [Entwurfsbereiche von Microsoft Azure-Zielzonen](../landing-zone/design-areas.md) bietet. In diesem Artikel wird schrittweise eine Reihe von Entwurfsrichtlinien bereitgestellt, die befolgt werden können, um die in der unternehmensweiten Lösung verankerten Entwurfsprinzipien umzusetzen.

Der Kern der unternehmensweiten Architektur enthält einen kritischen Entwurfspfad, der aus grundlegenden Entwurfsthemen mit sehr eng zusammenhängenden und abhängigen Entwurfsentscheidungen besteht. Dieses Repository bietet eine Entwurfsanleitung für diese architektonisch bedeutsamen technischen Bereiche, um die kritischen Entwurfsentscheidungen zu unterstützen, die zur Definition der unternehmensweiten Architektur getroffen werden müssen. Für jeden der betrachteten Bereiche sollten Sie die bereitgestellten Überlegungen und Empfehlungen prüfen und nutzen, um die Entwürfe innerhalb jedes Bereichs zu strukturieren und voranzubringen.

Sie könnten z. B. fragen, wie viele Abonnements für Ihre Umgebung erforderlich sind. In diesem Fall sollten Sie [Organisation und Governance von Abonnements](./management-group-and-subscription-organization.md#subscription-organization-and-governance) durchsehen und die dargelegten Empfehlungen befolgen, um Entscheidungen zu Abonnements zu treffen.

## <a name="critical-design-areas"></a>Wichtige Entwurfsbereiche

Die folgenden acht wichtigen Entwurfsbereiche können Ihnen bei der Übersetzung Ihrer Anforderungen in Microsoft Azure-Konstrukte und -Funktionen helfen. Sie kann Ihnen helfen, die Diskrepanz zwischen der lokalen und der Cloudentwurfsinfrastruktur zu beseitigen, die in der Regel zu Dissonanzen und Reibungen zwischen der Definition auf Unternehmensebene und der Azure-Einführung führt.

Die Auswirkungen von Entscheidungen, die in diesen kritischen Bereichen getroffen werden, werden in der gesamten unternehmensweiten Architektur nachhallen und andere Entscheidungen beeinflussen. Sie sollten sich mit den acht nachstehend aufgeführten Bereichen vertraut machen, um die Konsequenzen herbeigeführter Entscheidungen besser zu verstehen, die später zu Kompromissen in verwandten Bereichen führen können.

1. [Enterprise Agreement-Registrierung (EA) und Azure Active Directory-Mandanten](./enterprise-enrollment-and-azure-ad-tenants.md)
2. [Identitäts- und Zugriffsverwaltung](./identity-and-access-management.md)
3. [Organisation von Verwaltungsgruppen und Abonnements](./management-group-and-subscription-organization.md)
4. [Netzwerktopologie und -konnektivität](./network-topology-and-connectivity.md)
5. [Verwaltung und Überwachung](./management-and-monitoring.md)
6. [Business Continuity & Disaster Recovery](./business-continuity-and-disaster-recovery.md)
7. [Sicherheit, Governance und Compliance](./security-governance-and-compliance.md)
8. [Plattformautomatisierung und DevOps](./platform-automation-and-devops.md)
