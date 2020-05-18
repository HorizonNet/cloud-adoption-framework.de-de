---
title: Tools für die Beschleunigung der Bereitstellung in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Disziplin „Beschleunigung der Bereitstellung“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 356373e71bc12c7927debdb64f036f8774809860
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220225"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Tools für die Beschleunigung der Bereitstellung in Azure

[Beschleunigung der Bereitstellung](./index.md) ist eine der [fünf Disziplinen der Cloud Governance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf das Festlegen von Richtlinien, mit denen die Ressourcenkonfiguration bzw. -bereitstellung gesteuert wird. Innerhalb der fünf Disziplinen der Cloudgovernance schließt die Beschleunigung der Bereitstellung die Disziplin der Anpassung von Bereitstellung und Konfiguration ein. Zu diesem Zweck können manuelle Aktivitäten oder vollständig automatisierte DevOps-Aktivitäten zum Einsatz kommen. In beiden Fällen bleiben die angewandten Richtlinien größtenteils gleich.

Cloudverwalter, -überwacher und -architekten mit Interesse an der Governance werden wahrscheinlich viel Zeit in die Disziplin „Beschleunigung der Bereitstellung“ investieren, da mit dieser Disziplin Richtlinien und Anforderungen für mehrere Cloudanpassungsaktivitäten festgeschrieben werden. Die Tools in dieser Toolkette sind wichtig für das Cloudgovernanceteam und sollten im Lernpfad des Teams eine hohe Priorität einnehmen.

Im Folgenden ist eine Liste der Azure-Tools aufgeführt, die zur Ausreifung der Richtlinien und Prozesse beitragen können, die diese Disziplin unterstützen.

|  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) | [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
| Unternehmensrichtlinien implementieren     | Ja | Nein  | Nein  | Nein | Nein | Nein |
| Richtlinien zwischen Abonnements anwenden     | Erforderlich | Ja  | Nein  | Nein | Nein | Nein |
| Definierte Ressourcen bereitstellen     | Nein | Nein  | Ja  | Nein | Nein | Nein |
| Vollständig konforme Umgebungen erstellen      | Erforderlich | Erforderlich  | Erforderlich  | Ja | Nein | Nein |
| Richtlinien überprüfen      | Ja | Nein  | Nein  | Nein | Nein | Nein |
| Azure-Ressourcen abfragen      | Nein | Nein  | Nein  | Nein | Ja | Nein |
| Kosten von Ressourcen berichten      | Nein | Nein  | Nein  | Nein | Nein | Ja |

Im Folgenden finden Sie zusätzliche Tools, die für die Umsetzung spezieller Ziele im Zusammenhang mit der Beschleunigung der Bereitstellung möglicherweise erforderlich sind. Oft kommen diese Tools außerhalb des Governance-Teams zum Einsatz, werden aber immer noch als Aspekt der Disziplin „Beschleunigung der Bereitstellung“ betrachtet.

|  | [Azure portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure DevOps](https://docs.microsoft.com/azure/devops) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
| Manuelle Bereitstellung (einzelne Ressource)     | Ja | Ja  | Nein  | Nicht effizient | Nein | Ja |
| Manuelle Bereitstellung (vollständige Umgebung)     | Nicht effizient | Ja | Nein  | Nicht effizient | Nein | Ja |
| Automatische Bereitstellung (vollständige Umgebung)     | Nein  | Ja  | Nein  | Ja  | Nein | Ja |
| Konfiguration einzelner Ressource aktualisieren     | Ja | Ja | Nicht effizient | Nicht effizient | Nein | Ja – während der Replikation |
| Konfiguration vollständiger Umgebung aktualisieren     | Nicht effizient | Ja | Ja | Ja  | Nein | Ja – während der Replikation |
| Konfigurationsabweichung verwalten     | Nicht effizient | Nicht effizient | Ja  | Ja  | Nein | Ja – während der Replikation |
| Automatische Pipeline zum Bereitstellen von Code und Konfigurieren von Ressourcen (DevOps) erstellen     | Nein | Nein | Nein | Ja | Nein | Nein |

Abgesehen von den oben erwähnten nativen Azure-Tools verwenden Kunden häufig Tools von Drittanbietern, um die Beschleunigung der Bereitstellung und DevOps-Bereitstellungen zu vereinfachen.
