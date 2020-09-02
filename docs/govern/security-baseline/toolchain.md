---
title: Tools für Sicherheitsbaseline in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Disziplin „Sicherheitsbaseline“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 024078aa9257c450e377ba7b0a766c381800fc58
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88878807"
---
# <a name="security-baseline-tools-in-azure"></a>Tools für Sicherheitsbaseline in Azure

Die [Disziplin „Sicherheitsbaseline“](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Festlegen von Richtlinien, die das Netzwerk, Ressourcen und vor allem die Daten schützen, die sich in der Lösung eines Cloudanbieters befinden werden. Innerhalb der fünf Disziplinen von Cloud Governance umfasst die Disziplin „Sicherheitsbaseline“ die Klassifizierung des digitalen Bestands und der Daten. Darüber hinaus sind die Dokumentation zu Risiken, Geschäftstoleranz und Lösungsstrategien in Zusammenhang mit der Sicherheit von Daten, Ressourcen und Netzwerke enthalten. Aus technischer Sicht umfasst diese Disziplin auch die Beteiligung an Entscheidungen in Bezug auf [Verschlüsselung](../../decision-guides/encryption/index.md), [Netzwerkanforderungen](../../decision-guides/software-defined-network/index.md), [Hybrididentitätsstrategien](../../decision-guides/identity/index.md) und Tools für [automatisiertes Erzwingen](../../decision-guides/policy-enforcement/index.md) von Sicherheitsrichtlinien für alle [Ressourcengruppen](../../decision-guides/resource-consistency/index.md).

Die folgende Liste von Azure-Tools kann beim Ausreifen der Richtlinien und Prozesse helfen, diese Disziplin unterstützen.

| Tool | [Azure-Portal](https://azure.microsoft.com/features/azure-portal) und [Azure Resource Manager](/azure/azure-resource-manager/management/overview)  | [Azure Key Vault](/azure/key-vault)  | [Azure AD](/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](/azure/governance/policy/overview) | [Azure Security Center](/azure/security-center/security-center-intro) | [Azure Monitor](/azure/azure-monitor/overview) |
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

Eine vollständige Liste der Azure-Sicherheitstools und -dienste finden Sie unter [Bei Azure verfügbare Sicherheitsdienste und -technologien](/azure/security/fundamentals/services-technologies).

Kunden verwenden häufig Tools von Drittanbietern, um Aktivitäten der Disziplin „Sicherheitsbaseline“ zu ermöglichen. Weitere Informationen finden Sie im Artikel [Integrieren von Sicherheitslösungen in Azure Security Center](/azure/security-center/security-center-partner-integration).

Außer den Sicherheitstools enthält das [Microsoft Trust Center](https://www.microsoft.com/microsoft-365/business/compliance-solutions#office-KeyMessages-k3j63yo) umfassende Anweisungen, Berichte und zugehörige Dokumentation, mit denen Sie die Risikobewertungen im Rahmen Ihres Migrationsplanungsprozesses ausführen können.
