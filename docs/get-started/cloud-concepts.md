---
title: 'Erste Schritte: Dokumentieren grundlegender Ausrichtungsentscheidungen'
description: Verstehen und Dokumentieren anfänglicher Entscheidungen, die für die Umstellung auf die Cloud erforderlich sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 0c59a383f47629dd16cd81bc6865812fcaca4679
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230586"
---
<!-- docsTest:ignore CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template -->

# <a name="get-started-understand-and-document-foundational-alignment-decisions"></a>Erste Schritte: Verstehen und Dokumentieren grundlegender Ausrichtungsentscheidungen

Die Umstellung auf die Cloud kann eine Vielzahl von geschäftlichen, technischen und organisatorischen Vorteilen durch verschiedene Wege der Umsetzung ermöglichen. Unabhängig davon, was Sie erreichen möchten, gibt es bei Ihrem Umstieg auf die Cloud einige anfängliche Entscheidungen, die von jedem beteiligten Team verstanden werden sollten. Wenn Sie diesen Leitfaden durcharbeiten, zeichnen Sie diese Entscheidungen mithilfe der [Vorlage für anfängliche Entscheidungen](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx) auf, um schnell ein Onboarding von Teammitgliedern durchführen zu können, die am gesamten Cloudeinführungs-Lebenszyklus teilnehmen.

> [!NOTE]
> Wenn Sie auf einen der unten aufgeführten Schritte klicken, springen Sie durch das Inhaltsverzeichnis von Cloud Adoption Framework, um grundlegende Konzepte abzudecken, die später verwendet werden, um das Team beim Implementieren der zugehörigen Maßnahmen zu unterstützen. Versehen Sie diese Seite mit einem Lesezeichen, um häufig zu dieser Checkliste zurückzukehren.

## <a name="step-1-understand-how-azure-works"></a>Schritt 1: Wie funktioniert Azure?

Wenn Sie Azure als Cloudanbieter ausgewählt haben, um Ihre Umstellung auf die Cloud zu unterstützen, ist es wichtig, zu verstehen, [wie Azure funktioniert](./what-is-azure.md).

**Beteiligte Teams, Zielvorgaben und unterstützende Anleitungen:**

Alle Personen, die am Cloudeinführungs-Lebenszyklus beteiligt sind, sollten ein grundlegendes Verständnis der Funktionsweise von Azure haben.

## <a name="step-2-understand-initial-azure-concepts"></a>Schritt 2: Verstehen der ersten Azure-Konzepte

Azure baut auf einer Reihe von [grundlegenden Konzepten](../ready/considerations/fundamental-concepts.md) auf, für die tief greifende Ausführungen zur technischen Strategie erforderlich sind, da sie sich speziell auf Azure-Implementierungen bezieht.

**Beteiligte Teams, Zielvorgaben und unterstützende Anleitungen:**

Alle Personen, die an der Azure-Implementierung der Technologiestrategie beteiligt sind, müssen die Begriffe und Definitionen in den grundlegenden Konzepten verstehen.

## <a name="step-3-review-the-portfolio"></a>Schritt 3: Überprüfen des Portfolios

Unabhängig vom ausgewählten Cloudanbieter beginnen alle Cloudhosting- und Umgebungsentscheidungen mit dem Verständnis des gesamten Portfolios der Workloads. Das Cloud Adoption Framework umfasst einige Tools zum Verstehen und Auswerten des Portfolios.

**Zielvorgaben:**

- Aufzeichnen des Standorts, des Status und der zuständigen Person für die Portfoliodokumentation in der [Vorlage für anfängliche Entscheidung](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Grundlegende Konzepte](../ready/considerations/fundamental-concepts.md) helfen Ihnen, wichtige Azure-Themen zu verstehen, bevor Sie mit der Cloudeinführung beginnen.
- Mithilfe der [Arbeitsmappe für die Betriebsverwaltung](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/manage/opsmanagementworkbook.xlsx) und des Geschäftsausrichtungsansatzes können Sie die Workloads und Ressourcen verstehen, die an ein Cloudbetriebsteam übergeben wurden.
- Der [Cloudeinführungsplan](../plan/plan-intro.md) bietet ein Backlog der Workloads und Ressourcen, die für die Übernahme in die Cloud vorgesehen sind.
- Bei der [Analyse des digitalen Bestands](../digital-estate/approach.md) handelt es sich um einen Ansatz zum Dokumentieren vorhandener Workloads und Ressourcen, die für die Übernahme in die Cloud vorgesehen sind. In Azure wird der digitale Bestand am besten in einem Tool namens [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-support-matrix) dargestellt.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudstrategieteam ist dafür verantwortlich, eine Möglichkeit zum Anzeigen des Portfolios zu definieren. | <li> Mehrere Teams verwenden die folgenden Anleitungen, um diese Ansichten zu erstellen. Alle Personen, die an der Cloudeinführung beteiligt sind, sollten wissen, wo Sie die Portfolioansicht finden, um Entscheidungen später in diesem Prozess zu unterstützen. |

## <a name="step-4-define-portfolio-hierarchy-depth-to-align-the-portfolio"></a>Schritt 4: Definieren der Tiefe der Portfoliohierarchie, um das Portfolio auszurichten

Das Hosten von Ressourcen und Workload in der Cloud kann einfach sein und aus einer einzelnen Workload und unterstützenden Ressourcen bestehen. Für andere Kunden kann die Cloudeinführungsstrategie Tausende von Workloads und viele weitere unterstützende Ressourcen beinhalten. In der Portfoliohierarchie werden allgemeine Bezeichnungen für jede der geschichteten Hierarchieebenen erläutert, um eine gemeinsame Sprache für die Organisation unabhängig vom Cloudanbieter zu erstellen.

**Zielvorgaben:**

- Aufzeichnen der relevanten Hierarchieanforderungen in der [Vorlage für anfängliche Entscheidungen](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Leitfaden zur Erreichung der Zielvorgaben:**

- Verstehen der Ebenen der [Portfoliohierarchie](../reference/fundamental-concepts/hosting-hierarchy.md), um grundlegende Begriffe abzugleichen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudgovernanceteam ist für das Definieren, Erzwingen und Automatisieren der Portfoliohierarchie verantwortlich, um die Unternehmensrichtlinien in der Cloud zu formen. | <li> Alle Personen, die an der technischen Strategie für die Cloudeinführung beteiligt sind, sollten mit der Portfoliohierarchie und den Hierarchieebenen vertraut sein, die aktuell verwendet werden. |

## <a name="step-5-establish-a-naming-and-tagging-standard-across-the-portfolio"></a>Schritt 5: Einrichten eines Benennungs- und Markierungsstandards im gesamten Portfolio

Alle vorhandenen Workloads und Ressourcen müssen ordnungsgemäß benannt und in Übereinstimmung mit einem Benennungs- und Markierungsstandard gekennzeichnet werden. Diese Standards sollten dokumentiert und als Referenz für alle Teammitglieder verfügbar sein. Wenn möglich, sollten die Standards auch automatisch erzwungen werden, um die Mindestanforderungen an die Markierung sicherzustellen.

**Zielvorgaben:**

- Aufzeichnen des Speicherorts, des Status und der verantwortlichen Partei für die Arbeitsmappe für Benennungs- und Markierungsstandards in der [Vorlage für anfängliche Entscheidungen](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Leitfaden zur Erreichung der Zielvorgaben:**

- Erstellen eines [Standards für Benennung und Markierung](../ready/azure-best-practices/naming-and-tagging.md).
- Füllen Sie die [Arbeitsmappe für die Nachverfolgung von Benennungs- und Markierungskonventionen](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) mit Daten auf, um Entscheidungen nachzuverfolgen.
- [Überprüfen und aktualisieren Sie vorhandene Tags in Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).
- [Erzwingen von Markierungsrichtlinien in Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-policies).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudgovernanceteam ist für das Definieren, Erzwingen und Automatisieren der Benennungs- und Markierungsstandards verantwortlich, um Konsistenz im gesamten Portfolio sicherzustellen. | <li> Alle Personen, die an der technischen Strategie für die Cloudeinführung beteiligt sind, sollten mit den Benennungs- und Markierungsstandards vertraut sein, bevor die Bereitstellung in der Cloud stattfindet. |

## <a name="step-6-create-a-resource-organization-design-to-implement-the-portfolio-hierarchy"></a>Schritt 6: Erstellen eines Ressourcenorganisationsentwurfs zum Implementieren der Portfoliohierarchie

Um eine konsistente Ausrichtung mit den Entscheidungen hinsichtlich der Portfoliohierarchie zu gewährleisten, ist es wichtig, einen Entwurf für die Ressourcenorganisation zu erstellen. Ein solcher Entwurf würde die Organisationstools des Cloudanbieters an der Portfoliohierarchie ausrichten, die zur Unterstützung Ihres Cloudeinführungsplans erforderlich ist. Dieser Entwurf steuert die Implementierung, indem er klarstellt, welche Ressourcen in bestimmten Grenzen innerhalb der Cloudumgebungen eingesetzt werden können.

**Zielvorgaben:**

- Zuordnen von Azure-Produkten zur ausgerichteten Ebene der Portfoliohierarchie in der [Vorlage für anfängliche Entscheidungen](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Leitfaden zur Erreichung der Zielvorgaben:**

- Verstehen, wie [Azure-Produkte die Portfoliohierarchie unterstützen](../reference/fundamental-concepts/hierarchy-azure-tools.md).
- Überprüfen Sie vorhandene Abonnements für die Ausrichtung an der ausgewählten Portfoliohierarchie.

Erstellen einer Abonnementstrategie:

- Beginnen Sie [entwurfsbedingt mit zwei Abonnements](../ready/azure-best-practices/initial-subscriptions.md).
  - Fügen Sie grundlegende Abonnemententwürfe hinzu, um allgemeine Unternehmensanforderungen zu berücksichtigen, etwa gemeinsame Dienste oder Sandboxabonnements.
- [Verwalten Sie mehrere Abonnements](../ready/azure-best-practices/organize-subscriptions.md), wenn zusätzliche Abonnements erforderlich sind, um den Cloudeinführungsplan zu unterstützen.
- Richten Sie [klare Grenzen basierend auf der Portfoliohierarchie](../reference/fundamental-concepts/hierarchy-azure-tools.md#organizing-the-hierarchy-in-azure) ein.
- [Verschieben Sie bei Bedarf Ressourcengruppen und Ressourcen zwischen Abonnements](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription), um die Organisationsstrategie einzuhalten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudgovernanceteam ist für das Definieren, Implementieren und Automatisieren des Ressourcenorganisationsentwurfs im gesamten Portfolio verantwortlich. | <li> Alle Personen, die an der technischen Strategie für die Cloudeinführung beteiligt sind, sollten mit dem Ressourcenorganisationsentwurf vertraut sein, bevor die Bereitstellung in der Cloud stattfindet. |

## <a name="step-7-map-capabilities-teams-and-raci-to-fundamental-concepts"></a>Schritt 7: Zuordnen von Funktionen, Teams und RACI zu grundlegenden Konzepten

Die Komplexität der Portfoliohierarchie hilft Ihnen, Organisationsstrukturen und -methoden zu definieren, um die alltäglichen Aktivitäten verschiedener Teams zu leiten.

**Zielvorgaben:**

- Befolgen der Leitfäden für erste Schritte für die Organisationsausrichtung basierend auf diesen grundlegenden Konzepten.

<!-- docsTest:ignore Get Align -->

**Leitfaden zur Erreichung der Zielvorgaben:**

- Verwenden der vorherigen Schritte als Leitfaden, um den [Leitfaden zur Verantwortlichkeit der Portfoliohierarchie](../reference/fundamental-concepts/hosting-hierarchy.md#hierarchy-accountability-and-guidance) zu evaluieren, um zu bestimmen, welche Funktionen von dedizierten Organisationen oder virtuellen Teams bereitgestellt werden müssen.
- Verwenden Sie [Erste Schritte: Ausrichten Ihrer Organisation](./org-alignment.md), um die Anleitungen zur Verantwortlichkeit der Portfoliohierarchie auf das RACI-Diagramm anzuwenden.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudstrategieteam ist für die Ausrichtung virtueller oder dedizierter Organisationsstrukturen verantwortlich, um den Erfolg des gesamten Cloud einführungs-Lebenszyklus zu gewährleisten. | <li> Alle Personen, die am Cloudeinführungs-Lebenszyklus beteiligt sind, sollten mit der Ausrichtung von Personen und Ebenen der Verantwortlichkeit vertraut sein. |

## <a name="whats-next"></a>Nächste Schritte

Aufbauen auf diesen grundlegenden Konzepten mithilfe der Leitfäden für erste Schritte in diesem Abschnitt des Cloud Adoption Framework.

> [!div class="nextstepaction"]
> [Anwenden grundlegender Konzepte auf andere Leitfäden mit ersten Schritten](./index.md)
