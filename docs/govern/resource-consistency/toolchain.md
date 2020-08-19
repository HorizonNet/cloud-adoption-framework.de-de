---
title: Ressourcenkonsistenztools in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Disziplin „Ressourcenkonsistenz“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 55ffac53041f961757909ec80b7118d2e2118f2a
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88568990"
---
# <a name="resource-consistency-tools-in-azure"></a>Ressourcenkonsistenztools in Azure

[Ressourcenkonsistenz](./index.md) ist eine der [fünf Disziplinen der Cloud-Governance](../governance-disciplines.md). Dieser Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Richtlinien, die sich auf die Verwaltung des Betriebs einer Umgebung, Anwendung oder Workload beziehen. Innerhalb der fünf Disziplinen der Cloudgovernance umfasst die Disziplin „Ressourcenkonsistenz“ die Überwachung der Anwendungs-, Workload- und Ressourcenleistung. Darüber hinaus umfasst sie die Aufgaben, die zur Erfüllung von Skalierungsanforderungen erforderlich sind, sowie zur Korrektur von Leistungs-SLA-Verstößen und zur proaktiven Vermeidung von Leistungs-SLA-Verstößen durch automatisierte Korrektur.

<!-- docsTest:ignore "conditional access to resources" -->

Im Folgenden ist eine Liste der Azure-Tools aufgeführt, die zur Ausreifung der Richtlinien und Prozesse beitragen können, die diese Disziplin unterstützen.

| Tool | [Azure portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](/azure/azure-resource-manager/management/overview)  | [Azure Blueprint](/azure/governance/blueprints/overview) | [Azure Automation](/azure/automation/automation-intro) | [Azure AD](/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Backup](/azure/backup/backup-overview) | [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Bereitstellen von Ressourcen                             | Ja | Ja | Ja | Ja | Nein  | Nein | Nein |
| Ressourcen verwalten                             | Ja | Ja | Ja | Ja | Nein  | Nein | Nein |
| Bereitstellen von Ressourcen mithilfe von Vorlagen             | Nein  | Ja | Nein  | Ja | Nein  | Nein | Nein |
| Orchestrierte Umgebungsbereitstellung          | Nein  | Nein  | Ja | Nein  | Nein  | Nein | Nein |
| Definieren von Ressourcengruppen                       | Ja | Ja | Ja | Nein  | Nein  | Nein | Nein |
| Verwalten von Workload- und Kontobesitzern           | Ja | Ja | Ja | Nein  | Nein  | Nein | Nein |
| Verwalten des bedingten Zugriffs auf Ressourcen       | Ja | Ja | Ja | Nein  | Nein  | Nein | Nein |
| Konfigurieren von Benutzern mit rollenbasierter Zugriffssteuerung (RBAC)                         | Ja | Nein  | Nein  | Nein  | Ja | Nein | Nein |
| Zuweisen von Rollen und Berechtigungen zu Ressourcen | Ja | Ja | Ja | Nein  | Ja | Nein | Nein |
| Definieren von Abhängigkeiten zwischen Ressourcen        | Nein  | Ja | Ja | Nein  | Nein  | Nein | Nein |
| Anwenden der Zugriffssteuerung                         | Ja | Ja | Ja | Nein  | Ja | Nein | Nein |
| Bewerten der Verfügbarkeit und Skalierbarkeit          | Nein  | Nein  | Nein  | Ja | Nein  | Nein | Nein |
| Anwenden von Tags auf Ressourcen                      | Ja | Ja | Ja | Nein  | Nein  | Nein | Nein |
| Zuweisen von Azure Policy-Regeln                    | Ja | Ja | Ja | Nein  | Nein  | Nein | Nein |
| Anwenden der automatisierten Korrektur                  | Nein  | Nein  | Nein  | Ja | Nein  | Nein | Nein |
| Verwalten der Abrechnung                               | Ja | Nein  | Nein  | Nein  | Nein  | Nein | Nein |
| Planen von Ressourcen für die Notfallwiederherstellung         | Ja | Ja | Ja | Nein  | Nein  | Ja | Ja |
| Datenwiederherstellung bei Ausfall oder SLA-Verletzung     | Nein | Nein  | Nein  | Nein  | Nein  | Ja | Ja |
| Anwendungs- und Datenwiederherstellung bei Ausfall oder SLA-Verletzung     | Nein | Nein  | Nein  | Nein  | Nein  | Ja | Ja |

Zusammen mit diesen Ressourcenkonsistenztools und -funktionen müssen Sie Ihre bereitgestellten Ressourcen auf Leistungs- und Integritätsprobleme überwachen. [Azure Monitor](/azure/azure-monitor/overview) ist die-Standardlösung für Überwachung und Berichterstellung in Azure. Azure Monitor bietet Funktionen für die Überwachung Ihrer Cloudressourcen. Diese Liste zeigt, welche Funktion für allgemeine Überwachungsanforderungen geeignet ist.

| Tool | [Azure portal](https://azure.microsoft.com/features/azure-portal) | [Application Insights](/azure/application-insights/app-insights-overview) | [Log Analytics](/azure/azure-monitor/log-query/log-query-overview) | [Azure Monitor-REST-API](/rest/api/monitor) |
|----------------------------------------------------|--------------|----------------------|---------------|------------------------|
| Protokollieren von Telemetriedaten von VMs                 | Nein           | Nein                   | Ja           | Nein                     |
| Protokollieren von Telemetriedaten von virtuellen Netzwerken              | Nein           | Nein                   | Ja           | Nein                     |
| Protokollieren von Telemetriedaten von PaaS-Diensten                   | Nein           | Nein                   | Ja           | Nein                     |
| Protokoll von Telemetriedaten von Anwendungen                     | Nein           | Ja                  | Nein            | Nein                     |
| Konfigurieren von Berichten und Warnungen                       | Ja          | Nein                   | Nein            | Ja                    |
| Planen regelmäßiger Berichte oder benutzerdefinierter Analysen        | Nein           | Nein                   | Nein            | Nein                     |
| Visualisieren und Analysieren von Protokoll- und Leistungsdaten     | Ja          | Nein                   | Nein            | Nein                     |
| Integrieren in lokale oder Drittanbieterlösung für die Überwachung     | Nein           | Nein                   | Nein            | Ja                    |

Bei der Planung Ihrer Bereitstellung müssen Sie berücksichtigen, wo Protokolldaten gespeichert werden und wie Sie cloudbasierte [Berichts- und Überwachungsdienste](../../decision-guides/logging-and-reporting/index.md) in Ihre bestehenden Prozesse und Tools integrieren.

> [!NOTE]
> Organisationen verwenden auch DevOps-Tools von Drittanbietern, um Workloads und Ressourcen zu überwachen. Weitere Informationen finden Sie unter [Integrationen von DevOps-Tools](https://azure.microsoft.com/products/devops-tool-integrations).

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie [Richtliniendefinitionen](/azure/governance/policy) in Azure erstellen, zuweisen und verwalten.
