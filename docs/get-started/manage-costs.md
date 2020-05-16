---
title: 'Erste Schritte: Verwalten von Cloudkosten'
description: Erfahren Sie mehr über die Grundlagen der Kostenverwaltung im Zusammenhang mit der Cloudeinführung.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 22956507d801163b2ee75f074f48bbd955546c11
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230526"
---
<!-- docsTest:ignore Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template -->

# <a name="get-started-manage-cloud-costs"></a>Erste Schritte: Verwalten von Cloudkosten

Eine der Kerndisziplinen von Cloudgovernance ist die Kostenverwaltung. Die Disziplin der Kostenverwaltung konzentriert sich auf die Aufstellung von Budgets, die Überwachung von Kostenzuordnungsmustern und die Implementierung von Kontrollen zur Verbesserung des Cloudausgabenverhaltens im gesamten IT-Portfolio. Die Kostenoptimierung in Unternehmen umfasst jedoch noch viele andere Rollen und Funktionen, um die Kosten zu minimieren und die Anforderungen an Größe, Leistung, Sicherheit und Zuverlässigkeit auszugleichen. Dieser Artikel stellt diese verschiedenen unterstützenden Funktionen in einem Leitfaden für erste Schritte dar, um die Abstimmung zwischen den einzelnen beteiligten Teams zu erleichtern.

## <a name="get-started"></a>Erste Schritte

Governance ist der Eckpfeiler der Kostenoptimierung innerhalb jedes großen Unternehmens. Im folgenden Abschnitt wird die Kostenoptimierungsanleitung im Kontext von Governance beschrieben. Die nachfolgenden Schritte unterstützen jedes Team bei den ersten Schritten mit Aktionen, die sich auf ihre Rolle bei der Kostenoptimierung beziehen. Zusammen können Sie mit diesen Schritten Ihre gesamte Organisation bei der Umstellung auf eine zusammenhängende Kostenoptimierung unterstützen.

![Erste Schritte mit Kostenverwaltung im Unternehmen](../_images/get-started/cost-map.png)

## <a name="step-1-enterprise-cost-optimization"></a>Schritt 1: Optimierung der Unternehmenskosten

Das Cloudgovernanceteam ist gut darauf vorbereitet, überhöhte oder ungeplante Ausgaben durch eine Kombination aus Ausgaben-/Leistungsüberwachung, Reduzierung der Ressourcengröße/-ausgaben und sichere Beendigung ungenutzter Ressourcen zu bewerten und dagegen vorzugehen. Kostenoptimierung in Unternehmen beginnt mit einem gemeinsamen Teamverständnis der Tools, Prozesse und Abhängigkeiten, die erforderlich sind, um auf Kostenbelange auf Umgebungsebene klug zu reagieren.

**Zielvorgaben:**

- Implementieren sinnvoller Änderungen in der Kostenverwaltung im gesamten Unternehmen.
- Dokumentieren der Richtlinien, Prozesse und Entwurfsleitfäden für Kostenverwaltung in der [Richtlinienvorlage für Cost Management](../govern/cost-management/template.md).

Diese Zielvorgabe in diesem Schritt ist das Ergebnis von einigen wiederkehrenden Aufgaben:

- Sicherstellen einer strategischen Ausrichtung mit dem Cloudstrategieteam (das Workloadbeteiligte im gesamten Portfolio umfasst).
- Optimieren der Kosten für die gesamte Umgebung.
  - Herunterfahren oder automatisches Herunterfahren nicht verwendeter VMs.
  - Löschen oder Aufheben der Zuordnung beendeter VMs.
  - Sicherstellen der richtigen Ressourcengröße.
  - Ausrichten der tatsächlichen Ausgaben an den Budgeterwartungen.
- Überprüfen aller architektonischen Änderungen mithilfe von Azure Architecture Review, um ein Gespräch mit technischen Besitzern der Workloads zu ermöglichen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- Achten Sie darauf, dass bei allen Workloads und Ressourcen ordnungsgemäße [Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) eingehalten werden, und setzen Sie [Kennzeichnungskonventionen mithilfe von Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) mit einem spezifischen Schwerpunkt auf Tags für „Kostenstelle“ und „technischer Besitzer“ durch.
- Überprüfen und wenden Sie regelmäßig [bewährte Methoden](../govern/cost-management/best-practices.md) an, um Analysen und Verbesserungen im gesamten Unternehmen zu steuern. Im Folgenden finden Sie einige der wirksamsten Governancepraktiken aus diesem Artikel:

  - Arbeiten mit [allgemeinen bewährten Methoden für Kosten](../govern/cost-management/best-practices.md), um die Größe und die Kosten zu reduzieren und nicht verwendete Computer zu beenden.
  - Anwenden von [Hybridnutzungsvorteilen](../govern/cost-management/best-practices.md#best-practice-take-advantage-of-azure-hybrid-benefit), um die Lizenzierungskosten zu reduzieren.
  - Ausrichten von [reservierten Instanzen](../govern/cost-management/best-practices.md#best-practice-use-reserved-vm-instances), um Ressourcenkosten zu senken.
  - [Überwachen der Ressourcennutzung](../govern/cost-management/best-practices.md#best-practice-monitor-resource-utilization), um die Auswirkungen auf die Ressourcenleistung zu minimieren.
  - [Verringern der Kosten, die sich nicht auf die Produktion beziehen](../govern/cost-management/best-practices.md#best-practice-reduce-nonproduction-costs) durch Richtlinien zum Steuern von Nicht-Produktionsumgebungen.
  - Reagieren auf [Empfehlungen zur Kostenoptimierung](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- Kompromisse auf Workloadebene sind möglicherweise erforderlich, um wirksame Änderungen zur Kostenoptimierung umzusetzen. [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework/cost/tradeoffs) und [Azure Architecture Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review) können diese Gespräche mit dem technischen Besitzer einer bestimmten Workload unterstützen.
- Wenn Sie mit Cloudgovernance noch nicht vertraut sind, richten Sie [Governancerichtlinien, -prozesse und -fachrichtungen](../govern/index.md) mithilfe der Governancemethodik ein.
- Wenn Sie mit der Fachrichtung „Kostenverwaltung“ noch nicht vertraut sind, sollten Sie sich mit dem Artikel [Verbesserungen der Kostenverwaltung](../govern/guides/complex/cost-management-improvement.md) befassen und sich dabei auf den Abschnitt [Implementierung](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices) konzentrieren.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="steps-to-scale-cost-optimization"></a>Schritte zum Skalieren der Kostenoptimierung

Das Governanceteam kann in den meisten Unternehmen eine beträchtliche Kostenoptimierung erkennen und steuern. Grundlegende, datengesteuerte Ressourcengrößen können eine unmittelbare und messbare Auswirkung auf die Kosten haben.

Wie unter [Schaffen einer kostenbewussten Organisation](../organize/cost-conscious-organization.md) erläutert wird, kann ein unternehmensweiter Schwerpunkt auf Kostenverwaltung und Kostenoptimierung einen erheblich größeren Mehrwert bereitstellen. Die folgenden Schritte veranschaulichen, wie die verschiedenen Teams beim Schaffen einer kostenbewussten Organisation helfen können.

## <a name="step-2-define-strategy"></a>Schritt 2: Definieren der Strategie

Strategische Entscheidungen wirken sich direkt auf die Kostenkontrolle aus, durchlaufen den Einführungslebenszyklus und werden zu langfristigen Vorgängen. Strategische Klarheit verbessert die Kostenoptimierungsanstrengungen, die vom Governanceteam gesteuert werden.

**Zielvorgaben:**

- Aufzeichnen von Motivationen, Ergebnissen und geschäftlichen Begründungen in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Erstellen des ersten Budgets mit Azure Cost Management.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Verstehen der Motivationen](../strategy/motivations.md). Wichtige Geschäftsereignisse und einige Migrationsgründe sind tendenziell kostensensibel, was die Wichtigkeit der Kostenkontrolle für alle nachfolgenden Bemühungen erhöht. Andere zukunftsgerichtete Motivationen, die mit Innovation oder Wachstum durch Migration zu tun haben, können sich ggf. mehr auf den Umsatz konzentrieren. Das Verstehen von Motivationen hilft Ihnen zu verstehen, wie hoch die Priorität der Kostenverwaltung sein sollte.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md). Einige fiskalische Ergebnisse neigen dazu, extrem kostenempfindlich zu sein. Wenn sich die gewünschten Ergebnisse den fiskalischen Metriken zuordnen lassen, sollten Sie sehr frühzeitig in die Fachrichtung „Kostenverwaltung“ investieren.
- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md). Die geschäftliche Begründung dient als allgemeine Übersicht über den Gesamtfinanzplan für die Cloudeinführung. Dies ist eine gute Quelle für die anfängliche Budgetplanung.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudgovernanceteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-3-develop-a-cloud-adoption-plan"></a>Schritt 3: Entwickeln eines Cloudeinführungsplans

Der Einführungsplan bietet Klarheit bezüglich der Zeitachse der Aktivitäten während der Einführung. Wenn Sie den Plan und die Analyse den digitalen Bestand abgleichen, können Sie Ihr monatliches Wachstum bei Ausgaben vorhersagen. Außerdem hilft dies Ihrem Cloudgovernanceteam dabei, Prozesse auszurichten und Ausgabenmuster zu identifizieren.

**Zielvorgaben:**

- Ausführen der Schritte 1 bis 6, um einen [Cloudeinführungsplan](../plan/plan-intro.md#build-your-cloud-adoption-plan) zu entwickeln.
- Zusammenarbeiten mit Ihrem Cloudgovernanceteam, um Budgets zu verfeinern und realistische Ausgabenprognosen zu erstellen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Erfassen von Bestandsdaten](../digital-estate/inventory.md). Einrichten einer Datenquelle für die Analyse des digitalen Bestands vor der Einführung.
- [Bewährte Methode: Azure Migrate](../plan/contoso-migration-assessment.md). Verwenden Sie Azure Migrate, um den Bestand zu erfassen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization). Während der inkrementellen Rationalisierung kann eine quantitative Analyse für die Zwecke der Budgeterstellung Cloudkandidaten identifizieren.
- [Abstimmen von Kostenmodellen und Vorhersagemodellen](../digital-estate/calculate.md). Verwenden von Azure Cost Management, um Kosten- und Vorhersagemodelle durch [Erstellen von Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) abzustimmen.
- [Entwickeln Ihres Cloudeinführungsplans](../plan/plan-intro.md#build-your-cloud-adoption-plan). Erstellen Sie einen Plan mit ausführbaren Workloads, Ressourcen- und Zeitachsendetails. Dieser Plan stellt die Grundlage für Ausgaben im Zeitverlauf (oder Kostenprognose) dar. _Ausgaben im Zeitverlauf_ ist die anfängliche Baseline für alle umsetzbaren Optimierungsanalysen innerhalb der Fachrichtung „Kostenverwaltung“ von Governance.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-4-implement-landing-zone-best-practices"></a>Schritt 4: Implementieren von bewährten Methoden für Zielzonen

Die Bereitschaftsmethodik des Cloud Adoption Framework konzentriert sich stark auf die Entwicklung von Zielzonen zum Hosten von Workloads in der Cloud. Bei der Implementierung der Zielzonen sollten verschiedene Entscheidungen hinsichtlich der Kostenoptimierung berücksichtigt werden.

**Zielvorgaben:**

- Bereitstellen mindestens einer Zielzone, die Workloads im kurzfristigen Einführungsplan hosten kann.
- Sicherstellen, dass alle Zielzonen Kostenoptimierungsentscheidungen und Kostenverwaltungsanforderungen erfüllen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Nachverfolgen von Kosten](../ready/azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access). Einrichten einer gut verwalteten Umgebungshierarchie, Bereitstellen der richtigen Kostenzugriffsebene und Verwenden zusätzlicher Kostenverwaltungsressourcen in jeder Zielzone.
- [Optimieren Ihrer Cloudinvestitionen](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen bewährter Methoden für die Optimierung von Investitionen.
- [Erstellen und Verwalten von Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen bewährter Methoden zum Erstellen und Verwalten von Budgets.
- [Optimieren von Kosten mithilfe von Empfehlungen](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen bewährter Methoden zum Verwenden von Empfehlungen, die Kosten optimieren.
- [Überwachen von Nutzung und Ausgaben](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen von bewährten Methoden zum Überwachen von Nutzung und Ausgaben innerhalb einer Zielzone.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-5-complete-waves-of-migration-effort"></a>Schritt 5: Abschließen von Phasen der Migrationsbemühungen

Migration ist ein wiederholbarer Prozess, der vom Cloudeinführungsteam ausgeführt wird. In diesem Prozess gibt es viele Möglichkeiten, die Kosten im gesamten Portfolio zu optimieren. Viele dieser prozessinternen Entscheidungen werden auf eine kleine Gruppe von Workloads während der einzelnen Migrationswellen oder -iterationen angewendet.

**Zielvorgaben:**

- Messen, Testen, Ändern der Größe und Bereitstellen einer Sammlung vollständig optimierter Workloads.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Migrationsorientierte Kostenkontrollmechanismen](../migrate/azure-migration-guide/manage-costs.md) bieten Einblicke in die cloudnativen Kostenoptimierungssteuerungen, die bei der Migration helfen.
- [Bewährte Methoden für die Optimierung der Kosten migrierter Workloads](../migrate/azure-best-practices/migrate-best-practices-costs.md) enthält eine Checkliste mit 14 bewährten Methoden, die vor und nach der Migration befolgt werden müssen, um die Kostenoptimierung für die einzelnen Workloadreleases zu maximieren.

Langfristige Betriebskosten sind ein gängiges Thema in jedem Bereich von Verbesserungen des Migrationsprozesses. Diese Liste der Prozessverbesserungen ist nach der Phase des Migrationsprozesses gegliedert.

- [Voraussetzungen](../migrate/migration-considerations/prerequisites/index.md) enthält Informationen zum Verwalten von Änderungen und Backlog, was sowohl budgetierte als auch tatsächliche Cloudkosten beeinflusst.
- [Bewerten](../migrate/migration-considerations/assess/index.md) bietet sechs spezifische Prozesse (vom Überprüfen von Annahmen bis hin zum Verstehen der Partneroptionen), die die Cloudoptimierungsmöglichkeiten beeinflussen.
- [Migrieren](../migrate/migration-considerations/migrate/index.md) enthält einen Prozessvorschlag zur Wiederherstellung von Ressourcen, die die Möglichkeit bieten, den konfigurierten Status zu optimieren und eine optimierte Lösung bereitzustellen.
- [Höherstufung](../migrate/migration-considerations/optimize/index.md): Vom Testen bis hin zur Außerbetriebnahme von Ressourcen konzentriert sich die Höherstufung stark auf das Testen, Ändern der Größe, Überprüfen und Freigeben migrierter Ressourcen. Dies ist der erste klare Punkt, an dem Prognosen und Budgets anhand der tatsächlichen Leistung und Konfiguration getestet werden können.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-6-drive-customer-focused-innovation"></a>Schritt 6: Fördern kundenorientierter Innovation

Innovationen und die Entwicklung neuer Produkte erfordern einen weitaus höheren Grad an Architekturüberprüfung. Das Cloud Adoption Framework bietet ausführliche Informationen zum Innovationsprozess und zu Konzepten der Produktverwaltung. Entscheidungen zur Kostenoptimierung in Bezug auf neue Innovationen sprengen jedoch größtenteils den Rahmen dieses Leitfadens.

**Zielvorgaben:**

- Treffen wichtiger architektonischer Entscheidungen bezüglich neuer Innovationen, um Kosten und andere kritische Entwurfsüberlegungen auszugleichen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- Verwenden von [Azure Architecture Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review), um das Gleichgewicht bei Architekturentscheidungen zu verstehen.
- Überprüfen des [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework), um genauere Anleitungen zur Kostenoptimierung während der Innovation zu erhalten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-7-implement-sound-operations"></a>Schritt 7: Implementieren solider Vorgänge

Durch das Einrichten einer soliden Verwaltungsbaseline werden Daten erfasst und Betriebswarnungen erstellt. Dies kann Ihnen bei der Ermittlung von Kostenoptimierungsmöglichkeiten helfen. Der Schwerpunkt dieses Ansatzes besteht darin, ein Gleichgewicht zwischen Resilienz und Kostenoptimierung zu erzielen.

**Zielvorgaben:**

- Überwachen Ihrer Unternehmensumgebung auf fortlaufende Empfehlungen zur Optimierung der Kosten, ausgerichtet an den Wichtigkeits- und die Resilienzklassifizierungen der einzelnen Workloads.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Erstellen der geschäftlichen Ausrichtung](../manage/considerations/business-alignment.md), um Klarheit in Bezug auf die Wichtigkeit von und die Bereitschaft für Resilienzinvestitionen zu erhalten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="value-statement"></a>Wertaussage

Das Ausführen dieser Schritte kann Sie dabei unterstützen, [eine kostenbewusste Organisation zu erstellen](../organize/cost-conscious-organization.md). Durch geteilte Eigentümerschaft und einen kollaborativen Fokus mit den richtigen Teams zur richtigen Zeit lässt sich Kostenoptimierung einfacher umsetzen.
