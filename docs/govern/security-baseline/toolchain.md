---
title: Tools für Sicherheitsbaseline in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erläuterung der Tools zur Vereinfachung einer verbesserten Sicherheitsbaseline in Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3bf3eea5486fbd349094663dc5f37527f5042bb5
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221685"
---
# <a name="security-baseline-tools-in-azure"></a>Tools für Sicherheitsbaseline in Azure

[Sicherheitsbaseline](./index.md) ist eine der [fünf Disziplinen von Cloud Governance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Festlegen von Richtlinien, die das Netzwerk, Ressourcen und vor allem die Daten schützen, die sich in der Lösung eines Cloudanbieters befinden werden. Innerhalb der fünf Disziplinen von Cloud Governance umfasst die Disziplin „Sicherheitsbaseline“ die Klassifizierung des digitalen Bestands und der Daten. Darüber hinaus sind die Dokumentation zu Risiken, Geschäftstoleranz und Lösungsstrategien in Zusammenhang mit der Sicherheit von Daten, Ressourcen und Netzwerke enthalten. Aus technischer Sicht umfasst diese Disziplin auch die Beteiligung an Entscheidungen in Bezug auf [Verschlüsselung](../../decision-guides/encryption/index.md), [Netzwerkanforderungen](../../decision-guides/software-defined-network/index.md), [Hybrididentitätsstrategien](../../decision-guides/identity/index.md) und Tools für [automatisiertes Erzwingen](../../decision-guides/policy-enforcement/index.md) von Sicherheitsrichtlinien für alle [Ressourcengruppen](../../decision-guides/resource-consistency/index.md).

Die folgende Liste von Azure-Tools kann beim Ausreifen der Richtlinien und Prozesse helfen, die „Sicherheitsbaseline“ unterstützen.

| Tool | [Azure-Portal](https://azure.microsoft.com/features/azure-portal) / [Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
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

Eine vollständige Liste der Azure-Sicherheitstools und -dienste finden Sie unter [Bei Azure verfügbare Sicherheitsdienste und -technologien](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Es kommt auch häufig vor, dass Kunden Drittanbietertools zur Vereinfachung von Aktivitäten für Sicherheitsbaseline verwenden. Weitere Informationen finden Sie im Artikel [Integrieren von Sicherheitslösungen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Außer den Sicherheitstools enthält das [Microsoft Trust Center](https://www.microsoft.com/trustcenter/guidance/risk-assessment) umfassende Anweisungen, Berichte und zugehörige Dokumentation, mit denen Sie die Risikobewertungen im Rahmen Ihres Migrationsplanungsprozesses ausführen können.
