---
title: 'Erste Schritte: Sicherstellen konsistenter Leistung in einem Portfolio'
description: Lernen Sie die Grundlagen der Leistungsverwaltung über ein Portfolio hinweg kennen, einschließlich der Aufrechterhaltung der Leistung, des Festlegens von Erwartungen und der Schaffung einer organisatorischen Ausrichtung.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 5fc14f4ae460e3f2543754c2f99b5e278ea87815
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86450474"
---
# <a name="get-started-ensure-consistent-performance-across-a-portfolio"></a>Erste Schritte: Sicherstellen konsistenter Leistung in einem Portfolio

Wie lässt sich eine angemessene Leistung für ein gesamtes Workloadportfolio gewährleisten? Die Schritte in diesem Leitfaden unterstützen Sie dabei, Prozesse zur Aufrechterhaltung dieses Leistungsniveaus einzurichten.

Leistung hängt auch von anderen Rollen und Funktionen ab. In diesem Artikel werden die unterstützenden Funktionen beschrieben, mit denen Sie die beteiligten Teams aufeinander abstimmen können.

Die gängigste Methode zur Gewährleistung einer portfolioweit konsistenten Leistung ist die zentralisierte Betriebsverwaltung. Die im Zusammenhang mit betrieblichen Verfahren getroffenen Entscheidungen bestimmen die Betriebsbaseline sowie ganzheitliche Optimierungen (sofern vorhanden).

Der erste Schritt in dieser Anleitung unterstützt das Betriebsteam beim Einstieg. Die weiteren Schritte dienen dazu, dem gesamten Unternehmen zu einer angemessenen Leistung beim gesamten Workloadportfolio zu verhelfen.

![Erste Schritte zur Leistungsverwaltung im Unternehmen](../_images/get-started/performance-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Schritt 1: Einrichten von Anforderungen für die Betriebsverwaltung

Die im Microsoft Cloud Adoption Framework für Azure beschriebene Betriebsverwaltungsbaseline bietet eine Reihe von Kontrollen und cloudnativen Betriebstools zur Gewährleistung eines konsistenten Betriebs. Diese Baseline kann mit Automatisierungstools erweitert werden, um Leistungsüberwachung und Automatisierung bereitzustellen und so konsistente Leistungsanforderungen im gesamten Portfolio zu erfüllen.

**Ziele:**

- Optimieren Sie die Verwaltungsbaseline mit automatisierten Wartungsaufgaben im Zusammenhang mit Abweichungen von Leistungserwartungen.
- Wenn zur Erfüllung von Leistungsanforderungen workloadspezifische Datenmuster oder Architekturänderungen erforderlich sind, verwenden Sie workloadspezifische Vorgänge, um bessere Leistungsteuerung zu ermöglichen.
- Dokumentieren von Betriebsentscheidungen im IT-Portfolio in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx). Im Abschnitt **Betriebscompliance** der Registerkarte **Baseline** sollten Sie sich auf Entscheidungen zur Automatisierung der Leistung konzentrieren.

**Hinweis zur Erreichung der Ziele:**

- Der Artikel [Optimierte Verwaltungsbaseline in Azure](../manage/azure-management-guide/enhanced-baseline.md) enthält Beispiele für das Hinzufügen leistungsbezogener Erweiterungen mithilfe von Tools wie Azure Automation. Dieser Ansatz kann zur Gewährleistung einer konsistenten Leistung durch einfache Änderungen an der Größe und Skalierung der unterstützenden Ressourcen beitragen.
- Bei [workloadspezifischen Vorgängen](../manage/azure-management-guide/platform-specialization.md) wird Microsoft Azure Well-Architected Review verwendet, um Informationen zur Automatisierung für eine bestimmte Workload bereitzustellen. Dieser Leistungsverwaltungsansatz ist besonders hilfreich, wenn workloadspezifische Daten operative Aktionen steuern sollen.
- In der Anleitung oben wird davon ausgegangen, dass bereits eine Implementierung einer [Verwaltungsbaseline](../manage/considerations/discipline.md) zur Unterstützung des gesamten Workloadportfolios vorhanden ist.

> [!NOTE]
> Verschiedene Entscheidungen im gesamten Lebenszyklus der Cloudeinführung können sich unmittelbar auf die Leistung auswirken. Die folgenden Schritte unterstützen Sie bei der Gliederung der Partnerschaften und der unterstützenden Bestrebungen, die zur Leistungserbringung im gesamten IT-Portfolio erforderlich sind.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-2-consistent-application-of-the-management-baseline"></a>Schritt 2: Konsistentes Anwenden der Verwaltungsbaseline

Im Zuge der Optimierung der Verwaltungsbaseline ist es wichtig, dass die entsprechenden Verbesserungen in die Governancedisziplin „Ressourcenkonsistenz“ integriert werden. Dadurch wird sichergestellt, dass die optimierte Baseline in allen verwalteten Umgebungen angewendet wird.

**Ziele:**

- Stellen Sie die ordnungsgemäße Anwendung der Verwaltungsbaseline für alle betroffenen Systeme sicher.
- Dokumentieren Sie Ihre Richtlinien, Prozesse und Entwurfsinformationen für Ressourcenkonsistenz in der [Vorlage für die Disziplin „Ressourcenkonsistenz“](../govern/resource-consistency/template.md).

**Hinweis zur Erreichung der Ziele:**

- Stellen Sie sicher, dass alle Workloads und Ressourcen die [richtigen Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) befolgen. [Erzwingen Sie Kennzeichnungskonventionen mithilfe von Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) mit einem speziellen Schwerpunkt auf Tags für „Wichtigkeit“.
- Sollten Sie noch nicht mit Cloudgovernance vertraut sein, verwenden Sie die Governancemethodik, um [Governancerichtlinien, -prozesse und -disziplinen](../govern/index.md) einzurichten.
- Falls Sie noch keine Erfahrung mit der Governancedisziplin „Cost Management“ haben, befassen Sie sich ggf. mit dem folgenden [Artikel zur Verbesserung der Kostenverwaltung](../govern/guides/complex/cost-management-improvement.md) (insbesondere mit dem [Abschnitt zur Implementierung](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

## <a name="step-3-define-strategy"></a>Schritt 3: Definieren der Strategie

Strategische Entscheidungen wirken sich unmittelbar auf die Leistung sowie indirekt auf den Einführungslebenszyklus und letztendlich auf langfristige Vorgänge aus. Eine klare Strategie trägt zur Verbesserung der Leistungsbestrebungen im gesamten Portfolio bei. Darüber hinaus kann das Betriebsteam dank dieser Klarheit besser nachvollziehen, für welche Workloads ein gewisses Maß an Spezialisierung und erweiterte Vorgänge erforderlich sind.

**Zielvorgaben:**

- Erfassen Sie Beweggründe, Ergebnisse und geschäftliche Begründungen in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Stellen Sie sicher, dass die Verwaltungsbaseline eine auf die strategische Richtung der Cloudeinführung abgestimmte betriebliche Unterstützung bietet.

**Hinweis zur Erreichung der Ziele:**

- [Verstehen der Beweggründe](../strategy/motivations.md): Wichtige Geschäftsereignisse und einige Migrationsgründe sind tendenziell kostensensibel, was die Wichtigkeit der Kostenkontrolle für alle späteren Maßnahmen erhöht. Andere zukunftsgerichtete Beweggründe, die mit Innovation oder Wachstum durch Migration zu tun haben, sind möglicherweise eher auf den Umsatz ausgerichtet. Wenn Sie die Beweggründe kennen, können Sie besser entscheiden, welche Priorität der Kostenverwaltung eingeräumt werden sollte.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Einige fiskalische Ergebnisse neigen dazu, extrem kostensensibel zu sein. Wenn sich die gewünschten Ergebnisse den fiskalischen Metriken zuordnen lassen, sollten Sie frühzeitig in die Governancedisziplin „Cost Management“ investieren.
- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md): Die geschäftliche Begründung dient als allgemeine Übersicht über den Finanzplan für die Cloudeinführung. Sie kann eine gute Quelle für die anfängliche Budgetplanung darstellen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

## <a name="step-4-assess-and-plan-for-workload-adoption"></a>Schritt 4: Bewerten und Planen der Workloadeinführung

Der digitale Bestand (oder die Analyse des vorhandenen IT-Portfolios) kann bei der Validierung der geschäftlichen Begründung helfen und einen präziseren Einblick in das IT-Portfolio bieten. Der Einführungsplan sorgt für Klarheit beim zeitlichen Ablauf der Aktivitäten während der Einführung. Die Abstimmung dieses Plans und der Analyse des digitalen Bestands ermöglichen die Planung zukünftiger Abhängigkeiten für die Betriebsverwaltung.

Wenn Sie den Plan verstehen, können Sie auch das Cloudbetriebsteam in den Entwicklungszyklus integrieren. Das Team kann dann Änderungen an der Verwaltungsbaseline auswerten und planen, die für die Bereitstellung von Workloadvorgängen erforderlich sind.

**Ziele:**

- Aktualisieren Sie die [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) mit Änderungen, die durch die Analyse des digitalen Bestands ausgelöst wurden.
- Arbeiten Sie mit dem Cloudbetriebsteam zusammen, um die Wichtigkeit und die geschäftlichen Auswirkungen der einzelnen Workloads im kurz- und langfristigen Einführungsplan eindeutig zu definieren.
- Erarbeiten Sie zusammen mit dem Cloudbetriebsteam einen Zeitplan für die Betriebsbereitschaft.

**Hinweis zur Erreichung der Ziele:**

- [Erfassen von Bestandsdaten](../digital-estate/inventory.md): Richten Sie eine Datenquelle für die Analyse des digitalen Bestands vor der Einführung ein.
- [Bewährte Methode: Azure Migrate:](../plan/contoso-migration-assessment.md) Verwenden Sie Azure Migrate, um den Bestand zu erfassen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization): Verwenden Sie während der inkrementellen Rationalisierung eine quantitative Analyse, um Cloudkandidaten für Budgetierungszwecke zu identifizieren.
- [Abstimmen von Kostenmodellen und Vorhersagemodellen](../digital-estate/calculate.md): Verwenden Sie Azure Cost Management, um Kosten- und Vorhersagemodelle durch [Erstellen von Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) abzustimmen.
- [Entwickeln Ihres Cloudeinführungsplans](../plan/plan-intro.md#build-your-cloud-adoption-plan): Erstellen Sie einen Plan mit handlungsrelevanten Details zu Workloads und Ressourcen sowie zum zeitlichen Ablauf.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-5-expand-the-landing-zones"></a>Schritt 5: Erweitern der Zielzonen

Die Bereitschaftsmethodik des Cloud Adoption Framework konzentriert sich stark auf die Entwicklung von Zielzonen für das Hosten von Workloads in der Cloud. Bei der Implementierung von Zielzonen können sich verschiedene Entscheidungen auf den Betrieb auswirken.

Lassen Sie sich bei der Prüfung der Zielzone auf mögliche Betriebsverbesserungen vom Cloudbetriebsteam unterstützen. Wenden Sie sich außerdem an das Cloudgovernanceteam, um die Richtlinien für „Ressourcenkonsistenz“ und den Entwurfsleitfaden zu verstehen, da sich diese auf die Gestaltung der Zielzone auswirken können.

**Ziele:**

- Bereitstellen mindestens einer Zielzone, die Workloads im kurzfristigen Einführungsplan hosten kann.
- Stellen Sie sicher, dass alle Zielzonen mit Betriebsentscheidungen und Ressourcenkonsistenzanforderungen in Einklang stehen.

**Hinweis zur Erreichung der Ziele:**

- [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-operations.md): Bewährte Methoden zur Verbesserung des Betriebs innerhalb einer Zielzone.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudbetriebsteam <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-6-adoption"></a>Schritt 6: Einführung

Der langfristige Betrieb kann durch die Entscheidungen beeinflusst werden, die Sie im Zuge der Migrations- und Innovationsbestrebungen treffen. Wenn eine konsistente Ausrichtung frühzeitig in Einführungsprozessen gewährleistet ist, werden Barrieren für ein Produktionsrelease entfernt. Außerdem wird der Aufwand reduziert, der erforderlich ist, um ein Onboarding neuer Lösungen in Betriebsverwaltungspraktiken durchzuführen.

**Ziele:**

- Testen der Betriebsbereitschaft von Produktionsbereitstellungen unter Verwendung von Ressourcenkonsistenzrichtlinien.
- Überprüfen Sie die Einhaltung von Entwurfsrichtlinien und Betriebsanforderungen für Ressourcenkonsistenz.
- Dokumentieren Sie alle erweiterten Betriebsanforderungen in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Hinweis zur Erreichung der Zielvorgaben:**

- [Prüfliste zur Bereitschaft der Umgebung](../migrate/migration-considerations/prerequisites/planning-checklist.md)
- [Prüfliste vor der Höherstufung](../migrate/migration-considerations/optimize/ready.md)
- [Prüfliste für Produktionsreleases](../migrate/migration-considerations/optimize/promote.md)

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudbetriebsteam <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Die oben beschriebenen Schritte helfen dabei, Steuerungen und Prozesse zu implementieren, um die Leistung im Unternehmen und für alle gehosteten Ressourcen sicherzustellen.
