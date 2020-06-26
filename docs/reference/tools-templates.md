---
title: Tools und Vorlagen
description: Finden Sie die Tools und Vorlagen, die im Cloud Adoption Framework zur Verfügung stehen, um Ihre Cloudeinführung zu beschleunigen.
author: JanetCThomas
ms.author: janet
ms.date: 04/14/2020
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.topic: article
ms.openlocfilehash: c098fbf86771b9520d7530354ab993f956683050
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85077183"
---
<!-- cSpell:ignore Terraform's -->

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
| [Bereitschaftsprüfliste](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/ready/readiness-checklist.docx) | Verwenden Sie diese Prüfliste, um Ihre Umgebung auf die Einführung vorzubereiten, einschließlich der Vorbereitung Ihrer ersten Migrationszielzone, der Personalisierung der Blaupause und ihrer Erweiterung. |
| [Vorlage für die Nachverfolgung der Benennung und Markierung](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) | Dokumentieren Sie Entscheidungen über Benennungs- und Markierungsstandards, um Einheitlichkeit zu gewährleisten und die Zeit für das Onboarding zu verkürzen. |
| [&nbsp;CAF-Basisblaupause&nbsp;](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Verwenden Sie eine einfache Implementierung einer anfänglichen Governancegrundlage, um praktische Erfahrungen mit Governancetools in Azure bereitzustellen. |
| [Blaupause für die CAF-Migrationszielzone](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone) | Bereitstellung und Vorbereitung auf das Hosten von Workloads, die aus einer lokalen Umgebung zu Azure migriert werden. Weitere Informationen zu dieser Blaupause finden Sie unter [Entwickeln einer Migrationszielzone](../ready/landing-zone/migrate-landing-zone.md). |
| [Terraform-Module](../ready/landing-zone/terraform-landing-zone.md) | Open-Source-Codebasis für die Terraform-Version der CAF-Zielzonen. |
| [Terraform-Registrierung](https://registry.terraform.io/search?q=aztfmod) | Die gefilterte Website der Terraform-Registrierung, um alle Module des Cloud Adoption Framework aufzulisten, die zum Erstellen einer Zielzone über Terraform erforderlich sind. |

## <a name="govern"></a>Steuern

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Bewertung des Vergleichstests für Governance](https://cafbaseline.com) | Identifizieren Sie die Lücken zwischen Ihrem derzeitigen Zustand und den geschäftlichen Prioritäten, und holen Sie sich die richtigen Ressourcen, um diese Lücken zu schließen. |
| [&nbsp;CAF-Basisblaupause&nbsp;](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Dies ist eine einfache Implementierung einer anfänglichen Governancegrundlage, um praktische Erfahrungen mit Governancetools in Azure bereitzustellen. |
| [Governanceprozessvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Governance%20Discipline%20Template.docx) | Definieren Sie den grundlegenden Satz von Governanceprozessen, die zur Durchsetzung der einzelnen Governancedisziplinen verwendet werden. |
| [Prozessvorlage für Cost Management](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Cost%20Management%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf das Cost Management voranschreitet. |
| [Prozessvorlage für die Bereitstellungsbeschleunigung](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Deployment%20Acceleration%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Bereitstellungsbeschleunigung voranschreitet. |
| [Identitätsprozessvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Identity%20Baseline%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Identitätsanforderungen voranschreitet. |
| [Prozessvorlage für die Ressourcenkonsistenz](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Resource%20Consistency%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Ressourcenkonsistenz voranschreitet. |
| [Prozessvorlage für die Sicherheitsbaseline](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Security%20Baseline%20Discipline%20Template.docx) | Definieren Sie die Richtlinienanweisungen und Entwurfsleitfäden, die es Ihnen ermöglichen, dass die Cloudgovernance innerhalb Ihres Unternehmens mit Schwerpunkt auf die Sicherheitsbaseline voranschreitet. |

## <a name="manage"></a>Verwalten

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Microsoft Azure Well-Architected Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review) | Diese Onlinebewertung wird dazu beitragen, Workload-spezifische Architekturen und Betriebsoptionen zu definieren. |
| [Bewährte&nbsp;Methoden&nbsp;für&nbsp;Quellcode](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/manage/Automation-Best-Practices) | Dieser bereitstellbare Quellcode ergänzt und beschleunigt die Einführung bewährter Methoden für Azure-Serververwaltungsdienste. Verwenden Sie diesen Quellcode, um das Operations Management schnell zu ermöglichen und eine betriebliche Baseline zu erstellen. |
| [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) | Dokumentieren Sie Entscheidungen zum Operations Management in der Cloud und erleichtern Sie Unterhaltungen mit dem Unternehmen, um eine Abstimmung in Bezug auf SLAs, Investitionen in die Resilienz und die Budgetzuweisung im Zusammenhang mit dem Betrieb zu gewährleisten. |

## <a name="organize"></a>Organisieren

| Resource | BESCHREIBUNG |
|----------|-------------|
| [Teamübergreifendes RACI-Diagramm](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) | Laden Sie die RACI-Tabellenvorlage herunter, und ändern Sie sie, um Entscheidungen bezüglich der Organisationstruktur im Lauf der Zeit nachzuverfolgen. |
