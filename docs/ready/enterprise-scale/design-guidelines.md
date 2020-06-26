---
title: Entwurfsrichtlinien
description: Entwurfsrichtlinien.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c1f23841cbde493b2c8279a1870ebbe7b061c721
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076939"
---
# <a name="design-guidelines"></a>Entwurfsrichtlinien

In diesem Artikel und in der folgenden Artikelserie wird dargelegt, wie die unternehmensweite Architektur eine wertende Position zu jedem der [Entwurfsbereiche von Microsoft Azure-Zielzonen](../landing-zone/design-areas.md) bietet. In dieser Artikelreihe wird schrittweise eine Reihe von Entwurfsrichtlinien definiert, die befolgt werden können, um die in der unternehmensweiten Lösung verankerten Entwurfsprinzipien umzusetzen.

Der Kern der unternehmensweiten Architektur enthält einen kritischen Entwurfspfad, der aus grundlegenden Entwurfsthemen mit sehr eng zusammenhängenden und abhängigen Entwurfsentscheidungen besteht. Dieses Repository bietet eine Entwurfsanleitung für diese architektonisch bedeutsamen technischen Bereiche, um die kritischen Entwurfsentscheidungen zu unterstützen, die zur Definition der unternehmensweiten Architektur getroffen werden müssen. Für jeden der betrachteten Bereiche sollten Leser die bereitgestellten Überlegungen und Empfehlungen prüfen und nutzen, um die Entwürfe innerhalb jedes Bereichs zu strukturieren und voranzubringen.

Beispielsweise kann ein Kunde fragen, wie viele Abonnements er für seine Umgebung benötigt. In diesem Fall sollte der Leser [ Organisation und Governance von Abonnements](./management-group-and-subscription-organization.md#subscription-organization-and-governance) durchsehen und die dargelegten Empfehlungen befolgen, um Entscheidungen zu Abonnements zu treffen.

## <a name="critical-design-areas"></a>Wichtige Entwurfsbereiche

Die folgenden acht kritischen Entwurfsbereiche helfen dabei, Kundenanforderungen in Microsoft Azure-Konstrukte und -Funktionen zu übersetzen und die Diskrepanz zwischen der lokalen und der Cloudentwurfsinfrastruktur zu beseitigen, die in der Regel zu Dissonanzen und Reibungen zwischen der Definition auf Unternehmensebene und der Azure-Einführung führt.

Die Auswirkungen von Entscheidungen, die in diesen kritischen Bereichen getroffen werden, werden in der gesamten unternehmensweiten Architektur nachhallen und andere Entscheidungen beeinflussen. Leser sollten sich mit den acht nachstehend aufgeführten Bereichen vertraut machen, um die Konsequenzen herbeigeführter Entscheidungen besser zu verstehen, die später zu Kompromissen in verwandten Bereichen führen können.

1. [Unternehmensregistrierung und Azure Active Directory-Mandanten](./enterprise-enrollment-and-azure-ad-tenants.md)
2. [Identitäts- und Zugriffsverwaltung](./identity-and-access-management.md)
3. [Organisation von Verwaltungsgruppen und Abonnements](./management-group-and-subscription-organization.md)
4. [Netzwerktopologie und -konnektivität](./network-topology-and-connectivity.md)
5. [Verwaltung und Überwachung](./management-and-monitoring.md)
6. [Business Continuity & Disaster Recovery](./business-continuity-and-disaster-recovery.md)
7. [Sicherheit, Governance und Compliance](./security-governance-and-compliance.md)
8. [Plattformautomatisierung und DevOps](./platform-automation-and-devops.md)
