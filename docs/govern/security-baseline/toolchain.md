---
title: Tools für Sicherheitsbaseline in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Governancedisziplin „Sicherheitsbaseline“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 53321f274480094d5ff9db91f282a825594536fc
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997229"
---
# <a name="security-baseline-tools-in-azure"></a>Tools für Sicherheitsbaseline in Azure

[Sicherheitsbaseline](./index.md) ist eine der [fünf Disziplinen von Cloud Governance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Festlegen von Richtlinien, die das Netzwerk, Ressourcen und vor allem die Daten schützen, die sich in der Lösung eines Cloudanbieters befinden werden. Innerhalb der fünf Disziplinen von Cloud Governance umfasst die Disziplin „Sicherheitsbaseline“ die Klassifizierung des digitalen Bestands und der Daten. Darüber hinaus sind die Dokumentation zu Risiken, Geschäftstoleranz und Lösungsstrategien in Zusammenhang mit der Sicherheit von Daten, Ressourcen und Netzwerke enthalten. Aus technischer Sicht umfasst diese Disziplin auch die Beteiligung an Entscheidungen in Bezug auf [Verschlüsselung](../../decision-guides/encryption/index.md), [Netzwerkanforderungen](../../decision-guides/software-defined-network/index.md), [Hybrididentitätsstrategien](../../decision-guides/identity/index.md) und Tools für [automatisiertes Erzwingen](../../decision-guides/policy-enforcement/index.md) von Sicherheitsrichtlinien für alle [Ressourcengruppen](../../decision-guides/resource-consistency/index.md).

Die folgende Liste von Azure-Tools kann beim Ausreifen der Richtlinien und Prozesse helfen, die „Sicherheitsbaseline“ unterstützen.

| Tool | [Azure-Portal](https://azure.microsoft.com/features/azure-portal) und [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview)  | [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Anwenden von Zugriffssteuerungen auf Ressourcen und Ressourcenerstellung   | Ja                             | Nein              | Ja      | Nein           | Nein                    | Nein            |
| Sichere virtuelle Netzwerke                                    | Ja                             | Nein              | Nein       | Ja          | Nein                    | Nein            |
| Verschlüsseln virtueller Laufwerke                                     | Nein                              | Ja             | Nein       | Nein           | Nein                    | Nein            |
| Verschlüsseln von PaaS-Speicher und -Datenbanken                         | Nein                              | Ja             | Nein       | Nein           | Nein                    | Nein            |
| Verwalten von Hybrididentitätsdiensten                            | Nein                              | Nein              | Ja      | Nein           | Nein                    | Nein            |
| Beschränken zulässiger Ressourcentypen                         | Nein                              | Nein              | Nein       | Ja          | Nein                    | Nein            |
| Erzwingen georegionaler Einschränkungen                          | Nein                              | Nein              | Nein       | Ja          | Nein                    | Nein            |
| Überwachen der Sicherheitsintegrität von Netzwerken und Ressourcen          | Nein                              | Nein              | Nein       | Nein           | Ja                   | Ja           |
| Erkennen schädlicher Aktivität                                  | Nein                              | Nein              | Nein       | Nein           | Ja                   | Ja           |
| Präventives Erkennen von Sicherheitsrisiken                        | Nein                              | Nein              | Nein       | Nein           | Ja                   | Nein            |
| Konfigurieren von Sicherung und Notfallwiederherstellung                     | Ja                             | Nein              | Nein       | Nein           | Nein                    | Nein            |

Eine vollständige Liste der Azure-Sicherheitstools und -dienste finden Sie unter [Bei Azure verfügbare Sicherheitsdienste und -technologien](https://docs.microsoft.com/azure/security/fundamentals/services-technologies).

Es kommt auch häufig vor, dass Kunden Drittanbietertools zur Vereinfachung von Aktivitäten für Sicherheitsbaseline verwenden. Weitere Informationen finden Sie im Artikel [Integrieren von Sicherheitslösungen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Außer den Sicherheitstools enthält das [Microsoft Trust Center](https://www.microsoft.com/microsoft-365/business/compliance-solutions#office-KeyMessages-k3j63yo) umfassende Anweisungen, Berichte und zugehörige Dokumentation, mit denen Sie die Risikobewertungen im Rahmen Ihres Migrationsplanungsprozesses ausführen können.
