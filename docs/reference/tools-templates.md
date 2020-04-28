---
title: Tools und Vorlagen
description: Finden Sie die Tools und Vorlagen, die im Cloud Adoption Framework zur Verfügung stehen, um Ihre Cloudeinführung zu beschleunigen.
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.topic: article
author: JanetCThomas
ms.author: janet
ms.date: 04/14/2020
ms.openlocfilehash: e37019a571d5868b98083e9f7fba0198da2b1ff0
ms.sourcegitcommit: 825f9ae5b6cdd2fa6cb18c14a9733ba9106194f2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81646722"
---
<!-- cSpell:ignore CAF Terraform's -->

# <a name="tools-and-templates"></a>Tools und Vorlagen

Das Cloud Adoption Framework umfasst Tools, mit denen Sie technische Änderungen schnell implementieren können. Verwenden Sie diese Tools, Vorlagen und Bewertungen, um die Cloudeinführung zu beschleunigen. Die folgenden Ressourcen können Ihnen in den einzelnen Einführungsphasen helfen. Einige der Tools und Vorlagen können in mehreren Phasen verwendet werden.

## <a name="strategy"></a>Strategie

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Cloud Journey Tracker](https://docs.microsoft.com/assessments/?mode=pre-assessment&id=cloud-journey-tracker) | Identifizieren Sie Ihren Cloudeinführungspfad basierend auf den Anforderungen Ihres Unternehmens. |
| [Strategie-&nbsp;und&nbsp;Planvorlage&nbsp;](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) | Dokumentieren Sie Entscheidungen, während Sie Ihre Strategie und den Plan für die Cloudeinführung umsetzen. |

## <a name="plan"></a>Planen

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Cloud Journey Tracker](https://docs.microsoft.com/assessments/?mode=pre-assessment&id=cloud-journey-tracker) | Identifizieren Sie Ihren Cloudeinführungspfad basierend auf den Anforderungen Ihres Unternehmens. |
| [Strategie-&nbsp;und&nbsp;Planvorlage&nbsp;](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) | Dokumentieren Sie Entscheidungen, während Sie Ihre Strategie und den Plan für die Cloudeinführung umsetzen. |
| [Generator für den Cloudeinführungsplan](../plan/template.md) | Standardisieren Sie Prozesse, indem Sie ein Backlog für [Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/what-is-azure-boards) unter Verwendung der Vorlage für den Cloudeinführungsplan bereitstellen. |

## <a name="ready"></a>Bereit

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Bereitschaftsprüfliste](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/ready/readiness-checklist.docx) | Verwenden Sie diese Prüfliste, um Ihre Umgebung auf die Einführung vorzubereiten, einschließlich der Vorbereitung Ihrer ersten Migrationszielzone, der Personalisierung der Blaupause und ihrer Erweiterung. |
| [Vorlage für die Nachverfolgung der Benennung und Markierung](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) | Dokumentieren Sie Entscheidungen über Benennungs- und Markierungsstandards, um Einheitlichkeit zu gewährleisten und die Zeit für das Onboarding zu verkürzen. |
| [&nbsp;CAF-Basisblaupause&nbsp;](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Verwenden Sie eine einfache Implementierung einer anfänglichen Governancegrundlage, um praktische Erfahrungen mit Governancetools in Azure bereitzustellen. |
| [Blaupause für die CAF-Migrationszielzone](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone) | Bereitstellung und Vorbereitung auf das Hosten von Workloads, die aus einer lokalen Umgebung zu Azure migriert werden. Weitere Informationen zu dieser Blaupause finden Sie unter [Entwickeln einer Migrationszielzone](https://docs.microsoft.com/azure/architecture/cloud-adoption/ready/azure-readiness-guide/migration-landing-zone). |
| [Blaupause der Terraform-Zielzone](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready/terraform-landing-zones/landingzone_caf_foundations) | Open-Source-Codebasis für die Terraform-Version der CAF-Blaupausen. |
| [Terraform-Registrierung](https://registry.terraform.io/search?q=aztfmod) | Die gefilterte Website der Terraform-Registrierung, um alle Module des Cloud Adoption Framework aufzulisten, die zum Erstellen einer Terraform-Zielzone erforderlich sind. |

## <a name="govern"></a>Steuern

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Bewertung des Vergleichstests für Governance](https://cafbaseline.com) | Identifizieren Sie die Lücken zwischen Ihrem derzeitigen Zustand und den geschäftlichen Prioritäten, und holen Sie sich die richtigen Ressourcen, um diese Lücken zu schließen. |
| [&nbsp;CAF-Basisblaupause&nbsp;](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Dies ist eine einfache Implementierung einer anfänglichen Governancegrundlage, um praktische Erfahrungen mit Governancetools in Azure bereitzustellen. |
| [Governanceprozessvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Governance%20Discipline%20Template.docx) | Definieren Sie den grundlegenden Satz von Governanceprozessen, die zur Durchsetzung der einzelnen Governancedisziplinen verwendet werden. |
| [Prozessvorlage für Cost Management](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Cost%20Management%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf das Cost Management voranschreitet. |
| [Prozessvorlage für die Bereitstellungsbeschleunigung](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Deployment%20Acceleration%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Bereitstellungsbeschleunigung voranschreitet. |
| [Identitätsprozessvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Identity%20Baseline%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Identitätsanforderungen voranschreitet. |
| [Prozessvorlage für die Ressourcenkonsistenz](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Resource%20Consistency%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Ressourcenkonsistenz voranschreitet. |
| [Prozessvorlage für die Sicherheitsbaseline](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Security%20Baseline%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Sicherheitsbaseline voranschreitet. |

## <a name="manage"></a>Verwalten

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Azure-Architekturüberprüfung](https://docs.microsoft.com/assessments/?id=azure-architecture-review) | Diese Onlinebewertung wird dazu beitragen, Workload-spezifische Architekturen und Betriebsoptionen zu definieren. |
| [Bewährte&nbsp;Methoden&nbsp;für&nbsp;Quellcode](https://github.com/microsoft/CloudAdoptionFramework/tree/master/manage/Automation-Best-Practices) | Dieser bereitstellbare Quellcode ergänzt und beschleunigt die Einführung des Leitfadens, der in der bewährten Methode für die Azure-Serververwaltung zu finden ist. Verwenden Sie diesen Quellcode, um das Operations Management schnell zu ermöglichen und eine betriebliche Baseline zu erstellen. |
| [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) | Dokumentieren Sie Entscheidungen zum Operations Management in der Cloud und erleichtern Sie Unterhaltungen mit dem Unternehmen, um eine Abstimmung in Bezug auf SLAs, Investitionen in die Resilienz und die Budgetzuweisung im Zusammenhang mit dem Betrieb zu gewährleisten. |

## <a name="organize"></a>Organisieren

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Teamübergreifendes RACI-Diagramm](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) | Laden Sie die RACI-Tabellenvorlage herunter, und ändern Sie sie, um Entscheidungen bezüglich der Organisationstruktur im Lauf der Zeit nachzuverfolgen. |
