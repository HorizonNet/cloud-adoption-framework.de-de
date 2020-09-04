---
title: 'Erste Schritte: Verbessern der Zuverlässigkeit mit den richtigen Steuerungen'
description: Lernen Sie die Grundlagen der Verbesserung der Zuverlässigkeit durch Governancesteuerungen und eine Verwaltungsbaseline kennen.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 448e98d06a79f9683996a8db946bf52b0c8e8cdd
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884231"
---
# <a name="get-started-improve-reliability-with-the-right-controls"></a>Erste Schritte: Verbessern der Zuverlässigkeit mit den richtigen Steuerungen

Wie werden die richtigen Steuerungen angewendet, um die Zuverlässigkeit zu verbessern? Dieser Artikel hilft Ihnen beim Minimieren von Unterbrechungen im Zusammenhang mit den folgenden Aspekten:

- Inkonsistenzen in der Konfiguration.
- Ressourcenorganisation.
- Sicherheitsbaselines.
- Ressourcenschutz.

Die Schritte in diesem Artikel helfen dem Betriebsteam beim Ausgleichen von Zuverlässigkeit und Kosten im gesamten IT-Portfolio. Dieser Artikel hilft auch dem Governanceteam bei der Sicherstellung, dass das Gleichgewicht konsistent angewendet wird. Zuverlässigkeit hängt auch von anderen Rollen und Funktionen ab. In diesem Artikel werden die unterstützenden Funktionen beschrieben, mit denen Sie die beteiligten Teams aufeinander abstimmen können.

Betriebsverwaltung und Governance sind gleichberechtigte Partner bei der Zuverlässigkeit von Unternehmen. Bei den Entscheidungen bezüglich Betriebspraktiken wird die Baseline für Zuverlässigkeit festgelegt. Die Ansätze, die zur Steuerung der Gesamtumgebung verwendet werden, gewährleisten Konsistenz für alle Ressourcen.

Die ersten beiden Schritte in diesem Leitfaden unterstützen beide Teams beim Einstieg. Sie werden sequenziell aufgelistet, Sie können sie jedoch parallel ausführen. Die folgenden Schritte helfen Ihnen, das gesamte Unternehmen auf einen gemeinsamen Weg zu zuverlässigeren Lösungen im gesamten Unternehmen zu bringen.

![Erste Schritte mit Unternehmenszuverlässigkeit](../_images/get-started/reliability-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Schritt 1: Einrichten von Anforderungen für die Betriebsverwaltung

Nicht alle Workloads werden gleich erstellt. In jeder Umgebung gibt es Workloads, die einen direkten und konstanten Einfluss auf das Geschäft haben. Es gibt auch unterstützende Geschäftsprozesse und Workloads, die einen geringeren Einfluss auf das Gesamtgeschäft haben. In diesem Schritt identifiziert und implementiert das Cloudbetriebsteam anfängliche Anforderungen zur Unterstützung des gesamten IT-Portfolios.

**Ziele:**

- Implementieren einer Verwaltungsbaseline, um die für alle Produktionsworkloads erforderlichen Standardvorgänge zu definieren.
- Aushandeln von Geschäftsverpflichtungen mit dem Cloudstrategieteam, um einen Plan für erweiterte Betriebs- und Resilienzanforderungen zu entwickeln.
- Erweitern der Verwaltungsbaseline, wenn für die Mehrzahl der Workloads zusätzliche Vorgänge erforderlich sind.
- Anwenden erweiterter Betriebsanforderungen auf Zielzonen und Ressourcen, die die wichtigsten Workloads unterstützen.
- Dokumentieren von Betriebsentscheidungen im IT-Portfolio in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Hinweis zur Erreichung der Ziele:**

- [Verwaltungsbaseline](../manage/considerations/discipline.md):

  - [Bestand und Transparenz](../manage/considerations/inventory.md): [Mithilfe von cloudnativen Tools](../manage/azure-management-guide/inventory.md) können Sie [Daten erfassen](../manage/monitor/data-collection.md) und [Warnungen konfigurieren](../manage/monitor/index.md). Mithilfe der Tools können Sie auch die [Überwachungsplattform](../manage/monitor/index.md) implementieren, die für Ihr Betriebsmodell am besten geeignet ist.
  - [Betriebsbezogene Compliance](../manage/considerations/operational-compliance.md): Die höchsten Prozentsätze von Ausfällen sind in der Regel auf Änderungen der Ressourcenkonfiguration oder schlechte Wartungspraktiken zurückzuführen. Befolgen Sie den [Leitfaden zur Azure-Serververwaltung](../manage/azure-server-management/index.md), um cloudnative Tools zur Verwaltung von Patches und Änderungen an der Ressourcenkonfiguration zu implementieren.
  - [Schutz und Wiederherstellung](../manage/considerations/protect.md): Ausfälle sind auf jeder Plattform unvermeidlich. Wenn eine Unterbrechung auftritt, können Sie sich mit [Sicherungs- und Wiederherstellungslösungen](../manage/azure-management-guide/protect-recover.md) vorbereiten, um die Dauer zu minimieren.
- [Erweiterter Betrieb](../manage/design-principles.md): Verwenden Sie die Verwaltungsbaseline als Grundlage für Ihren Austausch über die [Geschäftsausrichtung](../manage/considerations/business-alignment.md). Die hilft Ihnen, [Wichtigkeit](../manage/considerations/criticality.md), [Geschäftsauswirkungen](../manage/considerations/impact.md) und [Betriebsverpflichtungen](../manage/considerations/commitment.md) klar zu benennen. Die Geschäftsausrichtung hilft bei der Quantifizierung und Validierung von Anforderungen für eine [erweiterte Baseline](../manage/azure-management-guide/enhanced-baseline.md), der Verwaltung spezifischer [Technologieplattformen](../manage/azure-management-guide/workload-specialization.md) oder [workloadspezifischer Vorgänge](../manage/azure-management-guide/platform-specialization.md).
- **Durchführen einer Architekturüberprüfung:** Zum Erfüllen von Betriebsanforderungen sind möglicherweise Architekturänderungen auf Workloadebene erforderlich. [Microsoft Azure Well-Architected Framework](/azure/architecture/framework/cost/tradeoffs) und [Microsoft Azure Well-Architected Review](/assessments?id=azure-architecture-review) können diese Gespräche mit dem technischen Besitzer einer bestimmten Workload unterstützen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-2-consistently-apply-the-management-baseline"></a>Schritt 2: Konsistentes Anwenden der Verwaltungsbaseline

Unternehmenszuverlässigkeit erfordert eine konsistente Anwendung der Verwaltungsbaseline. Diese Konsistenz ergibt sich aus den entsprechenden Unternehmensrichtlinien, IT-Prozessen und automatisierten Tools. Diese Ressourcen steuern die Implementierung der Verwaltungsbaseline für alle betroffenen Ressourcen.

**Ziele:**

- Sicherstellen, dass die Verwaltungsbaseline für alle betroffenen Systeme ordnungsgemäß angewendet wird.
- Dokumentieren der Richtlinien zur Ressourcenkonsistenz, Prozesse und Entwurfsanleitungen in der [Vorlage für die Fachrichtung „Ressourcenkonsistenz“](../govern/resource-consistency/template.md).

**Hinweis zur Erreichung der Ziele:**

- Stellen Sie sicher, dass alle Workloads und Ressourcen die [richtigen Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) befolgen. [Erzwingen Sie Kennzeichnungskonventionen mithilfe von Azure Policy](/azure/governance/policy/tutorials/govern-tags) mit einem speziellen Schwerpunkt auf Tags für „Wichtigkeit“.
- Sollten Sie noch nicht mit Cloudgovernance vertraut sein, verwenden Sie die Governancemethodik, um [Governancerichtlinien, -prozesse und -disziplinen](../govern/index.md) einzurichten.
- Wenn Sie mit der Disziplin „Cost Management“ noch nicht vertraut sind, befolgen Sie die Anweisungen im Artikel [Verbesserung der Disziplin „Cost Management“](../govern/guides/complex/cost-management-improvement.md). Konzentrieren Sie sich auf den Abschnitt [Implementierung](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices).

> [!NOTE]
> **Schritte zum Einstieg in eine Zuverlässigkeitspartnerschaft mit anderen Teams:** Verschiedene Entscheidungen im gesamten Lebenszyklus der Cloudeinführung können einen direkten Einfluss auf die Zuverlässigkeit haben. Die folgenden Schritte unterstützen Sie bei der Gliederung der Partnerschaften und der unterstützenden Anstrengungen, die erforderlich sind, um konsistente Zuverlässigkeit im gesamten IT-Portfolio bereitzustellen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-define-your-strategy"></a>Schritt 3: Definieren Ihrer Strategie

Strategische Entscheidungen wirken sich direkt auf die Zuverlässigkeit aus. Sie prägen den Einführungslebenszyklus und den langfristigen Betrieb. Durch strategische Klarheit werden die Zuverlässigkeitsbemühungen verbessert.

**Ziele:**

- Erfassen Sie Beweggründe, Ergebnisse und geschäftliche Begründungen in der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx).
- Stellen Sie sicher, dass die Verwaltungsbaseline eine auf die strategische Richtung der Cloudeinführung abgestimmte betriebliche Unterstützung bietet.

**Hinweis zur Erreichung der Ziele:**

- [Verstehen der Beweggründe](../strategy/motivations.md): Wichtige Geschäftsereignisse und einige Migrationsgründe sind tendenziell kostensensibel. Diese Bereiche können die Wichtigkeit der Kostenkontrolle für alle späteren Anstrengungen erhöhen. Andere zukunftsgerichtete Beweggründe, die mit Innovation oder Wachstum durch Migration zu tun haben, sind möglicherweise eher auf den Umsatz ausgerichtet. Wenn Sie die Motivationen kennen, können Sie die Kostenverwaltung einfacher priorisieren.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Einige fiskalische Ergebnisse neigen dazu, extrem kostensensibel zu sein. Wenn sich die gewünschten Ergebnisse den fiskalischen Metriken zuordnen lassen, sollten Sie frühzeitig in die Governancedisziplin „Cost Management“ investieren.
- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md): Die geschäftliche Begründung dient als allgemeine Übersicht über den Gesamtfinanzplan für die Cloudeinführung. Sie kann eine gute Quelle für die anfängliche Budgetplanung darstellen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-4-develop-a-cloud-adoption-plan"></a>Schritt 4: Entwickeln eines Cloudeinführungsplans

Der digitale Bestand (oder die Analyse des vorhandenen IT-Portfolios) kann Ihnen helfen, die geschäftliche Begründung zu validieren. Er kann eine optimierte Ansicht des gesamten IT-Portfolios bereitstellen. Der Einführungsplan sorgt für Klarheit beim zeitlichen Ablauf der Aktivitäten während der Einführung.

Wenn Sie den Einführungsplan mit der Analyse des digitalen Bestands abstimmen, können Sie zukünftige Abhängigkeiten der Betriebsverwaltung planen. Wenn Sie den Einführungsplan verstehen, können Sie auch das Cloudbetriebsteam in die Entwicklungszyklen integrieren. Es kann dann Änderungen an der Verwaltungsbaseline auswerten und planen, die für die Bereitstellung von Workloadvorgängen erforderlich sind.

**Ziele:**

- Aktualisieren der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx), um die Änderung widerzuspiegeln, die für die Umsetzung der gewünschten Strategie erforderlich ist. Die aufgezeichneten Änderungen können Folgendes umfassen:

  - Eine Bewertung des vorhandenen digitalen Bestands.
  - Einen Cloudeinführungsplan, der die erforderlichen Änderungen und die damit verbundenen Aufgaben widerspiegelt.
  - Die Organisationsänderung, die für die Umsetzung des Plans erforderlich ist.
  - Einen Plan zur Ermittlung der Fähigkeiten, die benötigt werden, damit das vorhandene Team die erforderliche Aufgaben erfolgreich erfüllen kann.
- Arbeiten Sie mit dem Governanceteam zusammen, um Kostenmodelle und Vorhersagemodelle abzustimmen. Dieser Vorgang umfasst Maßnahmen zum Einstieg in die Optimierung der Ausgaben durch quantitative Analysen.

**Hinweis zur Erreichung der Ziele:**

- [Erfassen von Bestandsdaten](../digital-estate/inventory.md): Richten Sie eine Datenquelle für die Analyse des digitalen Bestands vor der Einführung ein.
- [Bewährte Methode: Azure Migrate:](../plan/contoso-migration-assessment.md) Verwenden Sie Azure Migrate, um den Bestand zu erfassen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization): Während der inkrementellen Rationalisierung kann eine quantitative Analyse Cloudkandidaten zu Budgetierungszwecken identifizieren.
- [Abstimmen von Kostenmodellen und Vorhersagemodellen](../digital-estate/calculate.md): Verwenden Sie Azure Cost Management und Abrechnung, um Kosten- und Vorhersagemodelle durch [Erstellen von Budgets](/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) abzustimmen.
- [Entwickeln Ihres Cloudeinführungsplans](../plan/plan-intro.md#build-your-cloud-adoption-plan): Erstellen Sie einen Plan mit handlungsrelevanten Details zu Workloads und Ressourcen sowie zum zeitlichen Ablauf.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-5-implement-landing-zone-best-practices"></a>Schritt 5: Implementieren von bewährten Methoden für Zielzonen

Die Bereitschaftsmethodik des Cloud Adoption Framework für Azure konzentriert sich stark auf die Entwicklung von Zielzonen für das Hosten von Workloads in der Cloud. Bei der Implementierung Zielzone können sich mehrere Entscheidungen auf den Betrieb auswirken. Lassen Sie sich bei der Prüfung der Zielzone auf mögliche Betriebsverbesserungen vom Cloudbetriebsteam unterstützen. Wenden Sie sich auch an das Cloudgovernanceteam, um die Richtlinien für „Ressourcenkonsistenz“ und den Entwurfsleitfaden zu verstehen, die sich möglicherweise auf den Entwurf der Zielzone auswirken.

**Ziele:**

- Bereitstellen mindestens einer Zielzone, die Workloads im kurzfristigen Einführungsplan hosten kann.
- Stellen Sie sicher, dass alle Zielzonen mit Betriebsentscheidungen und Ressourcenkonsistenzanforderungen in Einklang stehen.

**Hinweis zur Erreichung der Ziele:**

- [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-operations.md): Bewährte Methoden zur Verbesserung des Betriebs innerhalb einer bestimmten Zielzone.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudbetriebsteam <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-6-complete-waves-of-adoption-effort-and-change"></a>Schritt 6: Abschließen von Phasen der Einführungsbemühungen und -änderung

Langfristige Vorgänge können von den Entscheidungen beeinflusst werden, die während der Migration und der Innovationsbemühungen getroffen werden. Wenn eine konsistente Ausrichtung frühzeitig in Einführungsprozessen gewährleistet ist, werden Barrieren für ein Produktionsrelease entfernt. Außerdem wird der Aufwand reduziert, der erforderlich ist, um neue Lösungen in Betriebsverwaltungspraktiken einzuführen.

**Ziele:**

- Testen der Betriebsbereitschaft von Produktionsbereitstellungen unter Verwendung von Ressourcenkonsistenzrichtlinien.
- Überprüfen Sie die Einhaltung von Entwurfsrichtlinien und Betriebsanforderungen für die Ressourcenkonsistenz.
- Dokumentieren Sie alle erweiterten Betriebsanforderungen in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Hinweis zur Erreichung der Ziele:**

- [Prüfliste zur Bereitschaft der Umgebung](../migrate/migration-considerations/prerequisites/planning-checklist.md)
- [Prüfliste vor der Höherstufung](../migrate/migration-considerations/optimize/ready.md)
- [Prüfliste für Produktionsreleases](../migrate/migration-considerations/optimize/promote.md)

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudbetriebsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Diese Schritte helfen dabei, die Steuerungen und Prozesse zu implementieren, die erforderlich sind, um die Zuverlässigkeit im Unternehmen und für alle gehosteten Ressourcen sicherzustellen.
