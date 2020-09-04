---
title: 'Erste Schritte: Verwalten von Cloudkosten'
description: Erfahren Sie mehr über die Grundlagen der Kostenverwaltung im Zusammenhang mit der Cloudeinführung.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c6351e1e6de0db3247b584d914ea3b5c5e842e68
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884333"
---
# <a name="get-started-manage-cloud-costs"></a>Erste Schritte: Verwalten von Cloudkosten

Die Disziplin „Cost Management“ von Cloudgovernance konzentriert sich auf die Aufstellung von Budgets, die Überwachung von Kostenzuordnungsmustern und die Implementierung von Kontrollen zur Verbesserung des Cloudausgabenverhaltens im gesamten IT-Portfolio. Die Kostenoptimierung in Unternehmen umfasst noch viele andere Rollen und Funktionen, um die Kosten zu minimieren und die Anforderungen an Größe, Leistung, Sicherheit und Zuverlässigkeit auszugleichen. Dieser Artikel stellt diese verschiedenen unterstützenden Funktionen in einem Leitfaden für erste Schritte dar, um die Abstimmung zwischen den einzelnen beteiligten Teams zu erleichtern.

Die Kostenoptimierung in Unternehmen umfasst jedoch noch viele andere Rollen und Funktionen, um die Kosten zu minimieren und die Anforderungen an Größe, Leistung, Sicherheit und Zuverlässigkeit auszugleichen. In diesem Artikel werden die unterstützenden Funktionen beschrieben, mit denen die beteiligten Teams aufeinander abgestimmt werden können.

Governance ist der Eckpfeiler der Kostenoptimierung innerhalb jedes großen Unternehmens. Im folgenden Abschnitt wird die Kostenoptimierungsanleitung im Kontext von Governance beschrieben. Die nachfolgenden Schritte unterstützen jedes Team bei den Aktionen, die sich auf ihre Rolle bei der Kostenoptimierung beziehen. Zusammen können Sie mit diesen Schritten Ihre gesamte Organisation bei der Umstellung auf eine Kostenoptimierung unterstützen.

![Erste Schritte zur Kostenoptimierung](../_images/get-started/cost-map.png)

## <a name="step-1-optimize-enterprise-costs"></a>Schritt 1: Optimieren der Unternehmenskosten

Das Cloudgovernanceteam ist gut darauf vorbereitet, überhöhte oder ungeplante Ausgaben durch eine Kombination aus Leistungsüberwachung, Reduzierung der Ressourcengröße und sichere Beendigung ungenutzter Ressourcen zu bewerten und dagegen vorzugehen. Kostenoptimierung in Unternehmen beginnt mit einem gemeinsamen Teamverständnis der Tools, Prozesse und Abhängigkeiten, die erforderlich sind, um auf Kostenbelange auf Umgebungsebene klug zu reagieren.

**Zielvorgaben:**

- Implementieren Sie sinnvolle Änderungen an Ihren Cost Management-Richtlinien im gesamten Unternehmen.
- Dokumentieren der Richtlinien, Prozesse und Entwurfsleitfäden für Cost Management in der [Vorlage für Cost Management](../govern/cost-management/template.md).

Diese Zielvorgabe sind das Ergebnis von einigen wiederkehrenden Aufgaben:

- Sicherstellen einer strategischen Ausrichtung mit dem Cloudstrategieteam (das Workloadbeteiligte im gesamten Portfolio umfasst).
- Optimieren der Kosten für die gesamte Umgebung:
  - Manuelles oder automatisches Herunterfahren von nicht verwendeten virtuellen Computern.
  - Löschen oder Aufheben der Zuordnung beendeter VMs.
  - Sicherstellen der richtigen Ressourcengröße.
  - Ausrichten der Ausgaben an den Budgeterwartungen.
- Überprüfen aller architektonischen Änderungen mithilfe von Microsoft Azure Well-Architected Review, um ein Gespräch mit technischen Besitzern der Workloads zu ermöglichen.

**Hinweis zur Erreichung der Ziele:**

- Stellen Sie sicher, dass alle Workloads und Ressourcen die [richtigen Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) befolgen. [Erzwingen Sie Kennzeichnungskonventionen mithilfe von Azure Policy](/azure/governance/policy/tutorials/govern-tags) mit einem speziellen Schwerpunkt auf Tags für „Kostenstelle“ und „technischer Besitzer“.
- Überprüfen und wenden Sie regelmäßig [Best Practices für Cost Management](../govern/cost-management/best-practices.md) an, um Analysen und Verbesserungen im gesamten Unternehmen zu steuern. Zu den wichtigen Governancemethoden gehören:

  - Arbeiten mit [allgemeinen Best Practices für Kosten](../govern/cost-management/best-practices.md), um die Größe und die Kosten zu reduzieren und nicht verwendete Computer zu beenden.
  - Anwenden von [Hybridnutzungsvorteilen](../govern/cost-management/best-practices.md#best-practice-take-advantage-of-azure-hybrid-benefit), um die Lizenzierungskosten zu reduzieren.
  - Ausrichten von [reservierten Instanzen](../govern/cost-management/best-practices.md#best-practice-use-azure-reserved-vm-instances), um Ressourcenkosten zu senken.
  - [Überwachen der Ressourcennutzung](../govern/cost-management/best-practices.md#best-practice-monitor-resource-utilization), um Auswirkungen auf die Ressourcenleistung zu minimieren.
  - [Verringern der Kosten, die sich nicht auf die Produktion beziehen](../govern/cost-management/best-practices.md#best-practice-reduce-nonproduction-costs) durch Richtlinien zum Steuern von Nicht-Produktionsumgebungen.
  - Reagieren auf [Empfehlungen zur Kostenoptimierung](/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).

- Kompromisse auf Workloadebene sind möglicherweise erforderlich, um wirksame Änderungen zur Kostenoptimierung umzusetzen. [Microsoft Azure Well-Architected Framework](/azure/architecture/framework/cost/tradeoffs) und [Microsoft Azure Well-Architected Review](/assessments/?id=azure-architecture-review) können diese Gespräche mit dem technischen Besitzer einer bestimmten Workload unterstützen.
- Sollten Sie noch nicht mit Cloudgovernance vertraut sein, verwenden Sie die Governancemethodik, um [Governancerichtlinien, -prozesse und -disziplinen](../govern/index.md) einzurichten.
- Falls Sie noch keine Erfahrung mit der Disziplin „Cost Management“ haben, befassen Sie sich ggf. mit dem [Artikel zur Verbesserung der Kostenverwaltung](../govern/guides/complex/cost-management-improvement.md) (insbesondere mit dem [Abschnitt zur Implementierung](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

Das Governanceteam kann in den meisten Unternehmen eine beträchtliche Kostenoptimierung erkennen und steuern. Grundlegende, datengesteuerte Ressourcengrößen können eine unmittelbare und messbare Auswirkung auf die Kosten haben.

Wie unter [Schaffen einer kostenbewussten Organisation](../organize/cost-conscious-organization.md) erläutert wird, kann ein unternehmensweiter Schwerpunkt auf Kostenverwaltung und Kostenoptimierung einen erheblich größeren Mehrwert bereitstellen. Die folgenden Schritte veranschaulichen, wie die verschiedenen Teams beim Schaffen einer kostenbewussten Organisation helfen können.

## <a name="step-2-define-a-strategy"></a>Schritt 2: Definieren einer Strategie

Strategische Entscheidungen wirken sich direkt auf die Kostenkontrolle aus, durchlaufen den Einführungslebenszyklus und werden zu langfristigen Vorgängen. Strategische Klarheit verbessert die Kostenoptimierungsanstrengungen, die vom Governanceteam gesteuert werden.

**Ziele:**

- Erfassen Sie Beweggründe, Ergebnisse und geschäftliche Begründungen in der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx).
- Erstellen des ersten Budgets mit Azure Cost Management und Abrechnung.

**Hinweis zur Erreichung der Ziele:**

- [Verstehen der Motivationen](../strategy/motivations.md). Wichtige Geschäftsereignisse und einige Migrationsgründe sind tendenziell kostensensibel, was die Wichtigkeit der Kostenkontrolle für alle nachfolgenden Maßnahmen erhöht. Andere zukunftsgerichtete Motivationen, die mit Innovation oder Wachstum durch Migration zu tun haben, können sich ggf. mehr auf den Umsatz konzentrieren. Das Verstehen der Motivationen wird Ihnen bei der Entscheidung helfen, wie hoch die Prioritäten für Ihre Kostenverwaltung zu setzen sind.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md). Einige fiskalische Ergebnisse neigen dazu, extrem kostenempfindlich zu sein. Wenn sich die gewünschten Ergebnisse den fiskalischen Metriken zuordnen lassen, sollten Sie sehr frühzeitig in die Governancedisziplin „Cost Management“ investieren.
- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md). Die geschäftliche Begründung dient als allgemeine Übersicht über den Finanzplan für die Cloudeinführung. Dies ist eine gute Quelle für die anfängliche Budgetplanung.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudgovernanceteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-develop-a-cloud-adoption-plan"></a>Schritt 3: Entwickeln eines Cloudeinführungsplans

Der Einführungsplan bietet Klarheit bezüglich der Zeitachse der Aktivitäten während der Einführung. Wenn Sie den Plan und die Analyse den digitalen Bestand abgleichen, können Sie Ihr monatliches Wachstum bei Ausgaben vorhersagen. Außerdem hilft dies Ihrem Cloudgovernanceteam dabei, Prozesse auszurichten und Ausgabenmuster zu identifizieren.

**Zielvorgaben:**

- Ausführen der Schritte 1 bis 6, um einen [Cloudeinführungsplan](../plan/plan-intro.md#build-your-cloud-adoption-plan) zu entwickeln.
- Zusammenarbeiten mit Ihrem Cloudgovernanceteam, um Budgets zu verfeinern und realistische Ausgabenprognosen zu erstellen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Erfassen von Bestandsdaten](../digital-estate/inventory.md). Richten Sie eine Datenquelle für die Analyse des digitalen Bestands vor der Einführung ein.
- [Bewährte Methode: Azure Migrate](../plan/contoso-migration-assessment.md). Verwenden Sie Azure Migrate, um den Bestand zu erfassen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization). Während der inkrementellen Rationalisierung kann eine quantitative Analyse für die Zwecke der Budgeterstellung Cloudkandidaten identifizieren.
- [Abstimmen von Kostenmodellen und Vorhersagemodellen](../digital-estate/calculate.md). Verwenden Sie Azure Cost Management und Abrechnung, um Kosten- und Vorhersagemodelle durch [Erstellen von Budgets](/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) abzustimmen.
- [Entwickeln Ihres Cloudeinführungsplans](../plan/plan-intro.md#build-your-cloud-adoption-plan). Erstellen Sie einen Plan mit handlungsrelevanten Details zu Workloads und Ressourcen sowie zum zeitlichen Ablauf. Dieser Plan stellt die Grundlage für Ausgaben im Zeitverlauf (oder Kostenprognose) dar. *Ausgaben im Zeitverlauf* ist die anfängliche Baseline für alle umsetzbaren Optimierungsanalysen innerhalb der Governancedisziplin „Cost Management“.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-4-implement-best-practices-for-landing-zones"></a>Schritt 4: Implementieren bewährter Methoden für Zielzonen

Die Bereitschaftsmethodik des Microsoft Cloud Adoption Framework für Azure konzentriert sich stark auf die Entwicklung von Zielzonen für das Hosten von Workloads in der Cloud. Während der Implementierung von Zielzonen sollte eine Organisation verschiedene Entscheidungen zur Kostenoptimierung in Erwägung ziehen.

**Ziele:**

- Bereitstellen mindestens einer Zielzone, die Workloads im kurzfristigen Einführungsplan hosten kann.
- Sicherstellen, dass alle Zielzonen Kostenoptimierungsentscheidungen und Kostenverwaltungsanforderungen erfüllen.

**Hinweis zur Erreichung der Ziele:**

- [Nachverfolgen von Kosten](../ready/azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access). Einrichten einer gut verwalteten Umgebungshierarchie, Bereitstellen der richtigen Kostenzugriffsebene und Verwenden zusätzlicher Kostenverwaltungsressourcen in jeder Zielzone.
- [Optimieren Ihrer Cloudinvestitionen](/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen bewährter Methoden für die Optimierung von Investitionen.
- [Erstellen und Verwalten von Budgets](/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen bewährter Methoden zum Erstellen und Verwalten von Budgets.
- [Optimieren von Kosten mithilfe von Empfehlungen](/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen bewährter Methoden zum Verwenden von Empfehlungen, die Kosten optimieren.
- [Überwachen von Nutzung und Ausgaben](/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Verstehen von bewährten Methoden zum Überwachen von Nutzung und Ausgaben innerhalb einer Zielzone.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-5-complete-waves-of-migration-effort"></a>Schritt 5: Abschließen von Phasen der Migrationsbemühungen

Migration ist ein wiederholbarer Prozess, der vom Cloudeinführungsteam ausgeführt wird. In diesem Prozess gibt es viele Möglichkeiten, die Kosten im gesamten Portfolio zu optimieren. Viele dieser prozessinternen Entscheidungen werden auf eine kleine Gruppe von Workloads während der einzelnen Migrationswellen oder -iterationen angewendet.

**Zielvorgaben:**

- Messen, Testen, Ändern der Größe und Bereitstellen einer Sammlung vollständig optimierter Workloads.

**Hinweis zur Erreichung der Ziele:**

- [Migrationsorientierte Kostenkontrollmechanismen](../migrate/azure-migration-guide/manage-costs.md) bieten Einblicke in die cloudnativen Kostenoptimierungssteuerungen, die bei der Migration helfen.
- [Bewährte Methoden für die Optimierung der Kosten migrierter Workloads](../migrate/azure-best-practices/migrate-best-practices-costs.md) enthält eine Checkliste mit 14 bewährten Methoden, die vor und nach der Migration befolgt werden müssen, um die Kostenoptimierung für die einzelnen Workloadreleases zu maximieren.

Langfristige Betriebskosten sind ein gängiges Thema in jedem Bereich von Verbesserungen des Migrationsprozesses. Diese Liste der Prozessverbesserungen ist nach der Phase des Migrationsprozesses gegliedert:

- [Voraussetzungen](../migrate/migration-considerations/prerequisites/index.md) enthält Informationen zum Verwalten von Änderungen und Backlog, was sowohl budgetierte als auch tatsächliche Cloudkosten beeinflusst.
- [Bewerten](../migrate/migration-considerations/assess/index.md) bietet sechs spezifische Prozesse (vom Überprüfen von Annahmen bis hin zum Verstehen der Partneroptionen). Jeder Prozess wirkt sich auf die Cloudoptimierungsmöglichkeiten aus.
- [Migration](../migrate/migration-considerations/migrate/index.md) enthält einen Prozessvorschlag zur Optimierung von Ressourcen. Dieser Vorschlag bietet die Möglichkeit, den aktuell konfigurierten Status zu optimieren und durch eine optimierte Lösung zu ersetzen.
- [Höherstufung](../migrate/migration-considerations/optimize/index.md) konzentriert sich stark auf das Testen, Ändern der Größe, Überprüfen und Freigeben migrierter Ressourcen sowie die Außerbetriebnahme von Ressourcen. Dies ist der erste klare Punkt, an dem Prognosen und Budgets anhand der tatsächlichen Leistung und Konfiguration getestet werden können.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

## <a name="step-6-drive-customer-focused-innovation"></a>Schritt 6: Fördern kundenorientierter Innovation

Innovationen und die Entwicklung neuer Produkte erfordern einen weitaus höheren Grad an Architekturüberprüfung. Das Cloud Adoption Framework bietet ausführliche Informationen zum Innovationsprozess und zu Konzepten der Produktverwaltung. Entscheidungen zur Kostenoptimierung in Bezug auf neue Innovationen sprengen größtenteils den Rahmen dieses Leitfadens.

**Ziele:**

- Treffen wichtiger architektonischer Entscheidungen bezüglich neuer Innovationen, um Kosten und andere kritische Entwurfsüberlegungen auszugleichen.

**Hinweis zur Erreichung der Ziele:**

- Verwenden von [Microsoft Azure Well-Architected Review](/assessments/?id=azure-architecture-review), um das Gleichgewicht bei Architekturentscheidungen zu verstehen.
- Überprüfen des [Microsoft Azure Well-Architected Framework](/azure/architecture/framework), um genauere Anleitungen zur Kostenoptimierung während der Innovation zu erhalten.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-7-implement-sound-operations"></a>Schritt 7: Implementieren solider Vorgänge

Das Einrichten einer soliden Verwaltungsbaseline hilft Ihnen, Daten zu erfassen und Betriebswarnungen zu erstellen. Diese Maßnahme kann bei der Erkennung von Möglichkeiten zum Optimieren von Kosten hilfreich sein. Sie führt zu einem Gleichgewicht zwischen Resilienz und Kostenoptimierung.

**Ziele:**

- Überwachen Ihrer Unternehmensumgebung auf fortlaufende Empfehlungen zur Optimierung der Kosten, ausgerichtet an den Wichtigkeits- und die Resilienzklassifizierungen der einzelnen Workloads.

**Leitfaden zur Erreichung der Zielvorgaben:**

- [Erstellen der geschäftlichen Ausrichtung](../manage/considerations/business-alignment.md), um Klarheit in Bezug auf die Wichtigkeit von und die Bereitschaft für Resilienzinvestitionen zu erhalten.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Das Ausführen dieser Schritte kann Sie dabei unterstützen, [eine kostenbewusste Organisation zu erstellen](../organize/cost-conscious-organization.md). Durch die Verwendung geteilter Eigentümerschaft und eines kollaborativen Fokus mit den richtigen Teams zur richtigen Zeit im Unternehmen lässt sich Kostenoptimierung einfacher umsetzen.
