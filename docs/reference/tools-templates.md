---
title: Tools und Vorlagen
description: Finden Sie die Tools und Vorlagen, die im Cloud Adoption Framework zur Verfügung stehen, um Ihre Cloudeinführung zu beschleunigen.
author: JanetCThomas
ms.author: janet
ms.date: 04/14/2020
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.topic: article
ms.openlocfilehash: 975a848cbc2afe9ded2d0dea56b69717f796c5d3
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879173"
---
# <a name="tools-and-templates"></a>Tools und Vorlagen

Das Cloud Adoption Framework umfasst Tools, mit denen Sie technische Änderungen schnell implementieren können. Verwenden Sie diese Tools, Vorlagen und Bewertungen, um die Cloudeinführung zu beschleunigen. Die folgenden Ressourcen können Ihnen in den einzelnen Einführungsphasen helfen. Einige der Tools und Vorlagen können in mehreren Phasen verwendet werden.

## <a name="strategy"></a>Strategie

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Cloud Journey Tracker](/assessments/?id=cloud-journey-tracker&mode=pre-assessment) | Identifizieren Sie Ihren Cloudeinführungspfad basierend auf den Anforderungen Ihres Unternehmens. |
| [Strategie-&nbsp;und&nbsp;Planvorlage&nbsp;](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) | Dokumentieren Sie Entscheidungen, während Sie Ihre Strategie und den Plan für die Cloudeinführung umsetzen. |

## <a name="plan"></a>Planen

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Cloud Journey Tracker](/assessments/?id=cloud-journey-tracker&mode=pre-assessment) | Identifizieren Sie Ihren Cloudeinführungspfad basierend auf den Anforderungen Ihres Unternehmens. |
| [Strategie-&nbsp;und&nbsp;Planvorlage&nbsp;](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) | Dokumentieren Sie Entscheidungen, während Sie Ihre Strategie und den Plan für die Cloudeinführung umsetzen. |
| [Generator für den Cloudeinführungsplan](../plan/template.md) | Standardisieren Sie Prozesse, indem Sie ein Backlog für [Azure Boards](/azure/devops/boards/get-started/what-is-azure-boards) unter Verwendung einer Vorlage bereitstellen. |
| [Verwenden der ADO-Vorlage für die Strategiedefinition, Planung, Bereitmachung und Steuerung (Strategy-Plan-Ready-Govern)](https://azuredevopsdemogenerator.azurewebsites.net/?name=strategyplan) | Standardisieren Sie Prozesse, indem Sie ein Backlog für [Azure Boards](/azure/devops/boards/get-started/what-is-azure-boards) unter Verwendung einer Vorlage bereitstellen. |  


## <a name="ready"></a>Bereit

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Bereitschaftscheckliste](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/ready/readiness-checklist.docx) | Verwenden Sie diese Prüfliste, um Ihre Umgebung auf die Einführung vorzubereiten, einschließlich der Vorbereitung Ihrer ersten Migrationszielzone, der Personalisierung der Blaupause und ihrer Erweiterung. |
| [Vorlage für die Nachverfolgung der Konventionen zur Benennung und Markierung](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/ready/naming-and-tagging-conventions-tracking-template.xlsx) | Dokumentieren Sie Entscheidungen über Benennungs- und Markierungsstandards, um Einheitlichkeit zu gewährleisten und die Zeit für das Onboarding zu verkürzen. |
| [CAF-Basisblaupause](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Verwenden Sie eine einfache Implementierung einer anfänglichen Governancegrundlage, um praktische Erfahrungen mit Governancetools in Azure bereitzustellen. |
| [Blaupause für die CAF-Migrationszielzone](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone) | Bereitstellung und Vorbereitung auf das Hosten von Workloads, die aus einer lokalen Umgebung zu Azure migriert werden. Weitere Informationen zu dieser Blaupause finden Sie unter [Entwickeln einer Migrationszielzone](../ready/landing-zone/migrate-landing-zone.md). |
| [Terraform-Module](../ready/landing-zone/terraform-landing-zone.md) | Open-Source-Codebasis für die Terraform-Version der CAF-Zielzonen. |
| [Terraform-Registrierung](https://registry.terraform.io/search?q=aztfmod) | Die gefilterte Website der Terraform-Registrierung, um alle Module des Cloud Adoption Framework aufzulisten, die zum Erstellen einer Zielzone über Terraform erforderlich sind. |

## <a name="govern"></a>Steuern

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Bewertung des Vergleichstests für Governance](https://cafbaseline.com) | Identifizieren Sie die Lücken zwischen Ihrem derzeitigen Zustand und den geschäftlichen Prioritäten, und holen Sie sich die richtigen Ressourcen, um diese Lücken zu schließen. |
| [CAF-Basisblaupause](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Dies ist eine einfache Implementierung einer anfänglichen Governancegrundlage, um praktische Erfahrungen mit Governancetools in Azure bereitzustellen. |
| [Vorlage zur Governancedisziplin](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/govern/governance-discipline-template.docx) | Definieren Sie den grundlegenden Satz von Governanceprozessen, die zur Durchsetzung der einzelnen Governancedisziplinen verwendet werden. |
| [Vorlage zur Disziplin „Kostenverwaltung“](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/govern/cost-management-discipline-template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf das Cost Management voranschreitet. |
| [Vorlage zur Disziplin „Beschleunigung der Bereitstellung“](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/govern/deployment-acceleration-discipline-template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Bereitstellungsbeschleunigung voranschreitet. |
| [Vorlage für die Disziplin „Identitätsbaseline“](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/govern/identity-baseline-discipline-template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Identitätsanforderungen voranschreitet. |
| [Vorlage für die Disziplin „Ressourcenkonsistenz“](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/govern/resource-consistency-discipline-template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Ressourcenkonsistenz voranschreitet. |
| [Vorlage für die Disziplin „Sicherheitsbaseline“](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/govern/security-baseline-discipline-template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Sicherheitsbaseline voranschreitet. |
| [Azure Governance-Schnellansicht](https://github.com/JulianHayward/Azure-MG-Sub-Governance-Reporting) | Die Azure Governance-Schnellansicht ist ein PowerShell-Skript, das die Hierarchie der Azure-Mandantenverwaltungsgruppe bis hinunter zur Abonnementebene durchläuft. Sie erfasst Daten aus den relevantesten Azure Governance-Funktionen, z. B. Azure Policy, rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) und Azure Blueprints. Auf Basis der gesammelten Daten zeigt die Schnellansicht Ihre Hierarchiezuordnung, erstellt eine Mandantenübersicht und bietet differenzierte Erkenntnisse zum Umfang von Verwaltungsgruppen und Abonnements. |

## <a name="migrate"></a>Migrieren

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Prüfliste für die Rechenzentrumsmigration](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/migrate/datacenter-migration-discovery-checklist.docx) | In dieser Prüfliste finden Sie Informationen, die Ihnen helfen, Workloads, Server und andere Ressourcen in Ihrem Rechenzentrum zu identifizieren. Verwenden Sie diese Informationen, um Ihre Migration zu planen.
| [Migrationsvorlagen](https://aka.ms/adopt/plan/generator) | Im Azure DevOps-Generator wurden eine Reihe von Vorlagen erstellt, mit denen Sie Ihre Projekte optimieren können. Es wurden Vorlagen für [WVD](https://azuredevopsdemogenerator.azurewebsites.net/?name=wvdmigration), die [Servermigration](https://azuredevopsdemogenerator.azurewebsites.net/?name=servermigration), die [SQL-Migration](https://azuredevopsdemogenerator.azurewebsites.net/?name=sqlmigration) und [AKS-Bereitstellungen](https://azuredevopsdemogenerator.azurewebsites.net/?name=cafaks) erstellt.

## <a name="manage"></a>Verwalten

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Microsoft Azure Well-Architected Review](/assessments/?id=azure-architecture-review) | Diese Onlinebewertung wird dazu beitragen, Workload-spezifische Architekturen und Betriebsoptionen zu definieren. |
| [Bewährte&nbsp;Methoden&nbsp;für&nbsp;Quellcode](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/manage/Automation-Best-Practices) | Dieser bereitstellbare Quellcode ergänzt und beschleunigt die Einführung bewährter Methoden für Azure-Serververwaltungsdienste. Verwenden Sie diesen Quellcode, um das Operations Management schnell zu ermöglichen und eine betriebliche Baseline zu erstellen. |
| [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) | Dokumentieren Sie Entscheidungen zum Operations Management in der Cloud und erleichtern Sie Unterhaltungen mit dem Unternehmen, um eine Abstimmung in Bezug auf SLAs, Investitionen in die Resilienz und die Budgetzuweisung im Zusammenhang mit dem Betrieb zu gewährleisten. |

## <a name="organize"></a>Organisieren

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Teamübergreifendes RACI-Diagramm](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx) | Laden Sie die RACI-Tabellenvorlage herunter, und ändern Sie sie, um Entscheidungen bezüglich der Organisationstruktur im Lauf der Zeit nachzuverfolgen. |
