---
title: Strategische Option zum Ausführen von Azure in Ihrem Rechenzentrum
description: Stellen Sie Azure mithilfe Azure Stack Hub in Ihrem Rechenzentrum bereit.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 5b0f1e25f542a2e13403707ea5604ecc29159d66
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451526"
---
# <a name="strategic-option-to-run-azure-in-your-datacenter"></a>Strategische Option zum Ausführen von Azure in Ihrem Rechenzentrum

Microsoft verfolgt einen Cloud-First-Ansatz. Die Priorität besteht darin, Anwendungen und Daten in eine oder mehrere der Hyperscale-Clouds zu verschieben, zu denen die globale Azure-Option aber auch gebietsschemaspezifische Sovereign Clouds wie Azure Deutschland oder Azure Government zählen. Azure Stack Hub fungiert als eine weitere Instanz einer Sovereign Cloud, die von Kunden in ihren Rechenzentren betrieben oder über einen Cloud-Dienstanbieter genutzt wird. Azure Stack Hub ist jedoch keine Hyperscale-Cloud, und Microsoft veröffentlicht oder unterstützt keine Vereinbarungen zum Service Level (SLAs) für Azure Stack Hub.

## <a name="understand-your-cloud-journey"></a>Grundlegendes zu Ihrer Cloud Journey

Der Weg in die Cloud unterscheidet sich von Organisation zu Organisation. Er ist abhängig von der Geschichte der Organisation, ihren geschäftlichen Anforderungen, ihrer Kultur und – was vielleicht am wichtigsten ist – von ihrem Ausgangspunkt. Die Umstellung auf die Cloud bietet zahlreiche Optionen, Features und Funktionen sowie Möglichkeiten zum Verbessern vorhandener Governance- und Betriebsprozesse, zum Implementieren neuer Prozesse und sogar zum Umgestalten der Anwendungen, um die Cloudarchitekturen zu nutzen.

Ihre Journey kann eindeutige Vorteile aufzeigen, die die Verwendung der Cloud als Teil Ihrer IT- und Geschäftsstrategie bietet. Sie kann jedoch ebenso überzeugende Gründe dafür liefern, die Cloud _zumindest vorerst_ auf Ihr Rechenzentrum zu beschränken. Wenn bei Ihnen beides der Fall ist, müssen Sie nicht zwischen dem einen und dem anderen entscheiden. Azure Stack Hub ist im Kern ein [IaaS-Angebot (Infrastructure-as-a-Service)](https://azure.microsoft.com/blog/azure-stack-iaas-part-one), bietet aber zudem Platform-as-a-Service-Dienste (PaaS), die es Ihnen ermöglichen, eine Teilmenge von Azure-Diensten in Ihrem eigenen Rechenzentrum auszuführen.

## <a name="azure-stack-hub-in-your-strategy"></a>Azure Stack Hub in Ihrer Strategie

Die Azure Stack Hub-Migration bietet einen alternativen Ansatz für die Migration vorhandener Anwendungen, die entweder auf physischen Servern oder auf vorhandenen Virtualisierungsplattformen ausgeführt werden. Durch die Verschiebung dieser Workloads in die Azure Stack Hub-IaaS-Umgebung profitieren Teams von reibungsloseren Vorgängen, Self-Service-Bereitstellungen, standardisierten Hardwarekonfigurationen und Azure-Konsistenz. Wenn Sie Azure Stack Hub zur Modernisierung oder zum Unterstützen von Innovationen verwenden, können Ihre Teams Ihre Anwendungen und Workloads zur optimalen Nutzung der Cloud vorbereiten.

Die Verwendung eines einheitlichen Verfahrens für die Cloudeinführung in Azure und Azure Stack Hub bietet Ihnen die Möglichkeit, die gleichen Governance- und Betriebsmodelle auf Ressourcen in der öffentlichen Cloud und Ihrem eigenen Rechenzentrum anzuwenden. Azure Stack Hub verwendet das gleiche Azure Resource Manager-Modell wie Azure, sodass Sie eine zentrale Ansicht für Ihre Lösungen haben.

## <a name="understand-the-differences"></a>Verständnis der Unterschiede

Es gibt einige Unterschiede zwischen Azure und Azure Stack Hub. Während manche offensichtlich sind, machen sich andere erst bemerkbar, wenn die Implementierungszyklen bereits weit fortgeschritten sind. Folgende Unterschiede sollten Sie beachten:

- Azure bietet nahezu unbegrenzte Kapazität. Azure Stack Hub basiert auf physischer Hardware in Ihrem Rechenzentrum, was zu Kapazitätsbeschränkungen führt.
- API-Versionen und Authentifizierungsmechanismen können sich zwischen Azure und Azure Stack Hub geringfügig unterscheiden.
- Azure Stack Hub unterscheidet sich hinsichtlich des _Betreibers_ der Cloud, was sich auf die Ebene der Workloadvorgänge auswirkt.
- Sie müssen berücksichtigen, welchen Teil des Azure Stack Hub-Diensts der Azure Stack Hub-Operator ausführt, da dies bestimmt, ob der Endkunde einen Dienst PaaS oder SaaS aufruft.

Andere Unterschiede werden in weiteren Artikeln zu Azure Stack Hub erläutert, die sich mit verschiedenen Punkten im Lebenszyklus der Cloudeinführung befassen.

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Nächster Schritt: Integrieren dieser Strategie in Ihre Cloudeinführungsjourney

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney.

- [Planen von Azure Stack Hub-Migrationen](./plan.md)
- [Bereitschaft der Umgebung](./ready.md)
- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
