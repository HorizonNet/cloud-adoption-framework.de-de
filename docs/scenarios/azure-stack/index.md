---
title: 'Eine strategische Option zum Ausführen von Azure in Ihrem Rechenzentrum: Azure Stack'
description: Stellen Sie Azure mithilfe von Azure Stack Hub in Ihrem Rechenzentrum bereit.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 9684ad72587b1132632a53d15385e2f396311536
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88575025"
---
# <a name="azure-stack-a-strategic-option-for-running-azure-in-your-datacenter"></a>Azure Stack: Eine strategische Option zum Ausführen von Azure in Ihrem Rechenzentrum

Microsoft verfolgt einen Cloud-First-Ansatz für die Anwendungs- und Datenspeicherung. Die Priorität besteht darin, Anwendungen und Daten in eine oder mehrere der Hyperscale-Clouds zu verschieben, zu denen die globale Azure-Option aber auch gebietsschemaspezifische Sovereign Clouds wie Azure Deutschland oder Azure Government zählen.

Azure Stack Hub fungiert als eine weitere Instanz einer Sovereign Cloud, unabhängig davon, ob sie von Kunden in ihren Rechenzentren betrieben oder über einen Cloud-Dienstanbieter genutzt wird. Azure Stack Hub ist jedoch keine Hyperscale-Cloud, und Microsoft veröffentlicht oder unterstützt keine Vereinbarungen zum Service Level für Azure Stack Hub.

## <a name="understand-your-cloud-journey"></a>Grundlegendes zu Ihrer Cloud Journey

Der Weg in die Cloud unterscheidet sich von Organisation zu Organisation. Er ist abhängig von der Geschichte der Organisation, ihren geschäftlichen Anforderungen, ihrer Kultur und – was vielleicht am wichtigsten ist – von ihrem Ausgangspunkt. Für diesen Weg stehen zahlreiche Optionen, Features und Funktionen zur Verfügung. Außerdem bietet er Möglichkeiten, vorhandene Governancelösungen und Vorgänge zu verbessern, neue zu implementieren und sogar die Anwendungen umzugestalten, um die Cloudarchitekturen nutzen zu können.

Die Journey Ihrer Organisation kann eindeutige Vorteile aufzeigen, die die Verwendung der Cloud als Teil Ihrer IT- und Geschäftsstrategie bietet. Sie kann jedoch ebenso überzeugende Gründe dafür liefern, die Cloud zumindest vorerst auf das vorhandene Rechenzentrum zu beschränken. Wenn bei Ihnen beides der Fall ist, müssen Sie nicht zwischen dem einen und dem anderen entscheiden. Im Grunde genommen ist Azure Stack Hub ein [IaaS-Angebot (Infrastructure-as-a-Service)](https://azure.microsoft.com/blog/azure-stack-iaas-part-one). Es bietet aber zudem Platform-as-a-Service-Dienste (PaaS), die es Ihnen ermöglichen, eine Teilmenge von Azure-Diensten in Ihrem eigenen Rechenzentrum auszuführen.

## <a name="azure-stack-hub-in-your-strategy"></a>Azure Stack Hub in Ihrer Strategie

Azure Stack Hub bietet einen alternativen Ansatz für die Migration vorhandener Anwendungen, die entweder auf physischen Servern oder auf vorhandenen Virtualisierungsplattformen ausgeführt werden. Durch die Verschiebung dieser Workloads in die Azure Stack Hub-IaaS-Umgebung profitieren Teams von reibungsloseren Vorgängen, Self-Service-Bereitstellungen, standardisierten Hardwarekonfigurationen und Azure-Konsistenz. Wenn Sie Azure Stack Hub zur Modernisierung oder zum Unterstützen von Innovationen verwenden, können Ihre Teams Ihre Anwendungen und Workloads zur optimalen Nutzung der Cloud vorbereiten.

Die Verwendung eines einheitlichen Verfahrens für die Cloudeinführung in Azure und Azure Stack Hub bietet Ihnen die Möglichkeit, die gleichen Governance- und Betriebsmodelle auf Ressourcen in der öffentlichen Cloud und Ihrem eigenen Rechenzentrum anzuwenden. Azure Stack Hub verwendet das gleiche Azure Resource Manager-Modell wie Azure, sodass Sie eine zentrale Ansicht für Ihre Lösungen haben.

## <a name="compare-azure-with-azure-stack-hub"></a>Vergleichen von Azure mit Azure Stack Hub

Es gibt einige Unterschiede zwischen Azure und Azure Stack Hub. Während manche offensichtlich sind, machen sich andere erst bemerkbar, wenn der Implementierungszyklus bereits weit fortgeschritten ist. Bedenken Sie dabei folgende Unterschiede:

- Azure bietet nahezu unbegrenzte Kapazität. Azure Stack Hub basiert auf physischer Hardware in Ihrem Rechenzentrum, was zu Kapazitätsbeschränkungen führt.
- API-Versionen und Authentifizierungsmechanismen können sich zwischen Azure und Azure Stack Hub geringfügig unterscheiden.
- Azure Stack Hub unterscheidet sich hinsichtlich des _Betreibers_ der Cloud, was sich auf die Ebene der Workloadvorgänge auswirkt.
- Berücksichtigen Sie, welchen Teil des Azure Stack Hub-Diensts der Azure Stack Hub-Operator ausführt, da dies bestimmt, ob der Kunde ein PaaS- oder SaaS-Angebot (Software-as-a-Service) aufruft.

Andere Unterschiede werden in weiteren Artikeln zu Azure Stack Hub erläutert, die sich mit verschiedenen Punkten im Lebenszyklus der Cloudeinführung befassen.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Planen der Azure Stack Hub-Migration](./plan.md)
- [Bereitschaft der Umgebung](./ready.md)
- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
