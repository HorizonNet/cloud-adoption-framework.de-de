---
title: 'Erste Schritte: Verbessern der Zuverlässigkeit mit den richtigen Steuerungen'
description: Lernen Sie die Grundlagen der Verbesserung der Zuverlässigkeit durch Governancesteuerungen und eine Verwaltungsbaseline kennen.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c75b7a17c8c2676688f5221ec0e4d0f2ed0641a5
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400213"
---
# <a name="get-started-improve-reliability-with-the-right-controls"></a>Erste Schritte: Verbessern der Zuverlässigkeit mit den richtigen Steuerungen

Wie werden die richtigen Steuerungen angewendet, um die Zuverlässigkeit zu verbessern? Dieser Leitfaden hilft dabei, Unterbrechungen im Zusammenhang mit Inkonsistenzen bezüglich Konfiguration, Ressourcenorganisation, Sicherheitsbaselines oder Ressourcenschutz zu minimieren. Die Schritte in diesem Leitfaden helfen dem Betriebsteam, Zuverlässigkeit und Kosten über das gesamte IT-Portfolio hinweg auszugleichen, und unterstützen das Governanceteam bei der Sicherstellung einer konsistenten Anwendung dieses Gleichgewichts. Zuverlässigkeit hängt auch von anderen Rollen und Funktionen ab. In diesem Artikel werden die verschiedenen unterstützenden Funktionen beschrieben, mit denen Sie die Ausrichtung zwischen den beteiligten Teams gestalten können.

Betriebsverwaltung und Governance sind gleichberechtigte Partner bei der Zuverlässigkeit von Unternehmen. Bei den Entscheidungen bezüglich Betriebspraktiken wird die Baseline für Zuverlässigkeit festgelegt. Die Ansätze, die zur Steuerung der Gesamtumgebung verwendet werden, gewährleisten Konsistenz für alle Ressourcen. Die ersten beiden Schritte in diesem Leitfaden unterstützen beide Teams beim Einstieg. Obwohl Sie nacheinander genannt werden, können die folgenden Schritte parallel ausgeführt werden. Die folgenden Schritte helfen, das gesamte Unternehmen auf einen gemeinsamen Weg zu zuverlässigeren Lösungen im gesamten Unternehmen zu bringen.

![Erste Schritte mit Unternehmenszuverlässigkeit](../_images/get-started/reliability-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Schritt 1: Einrichten von Anforderungen für Betriebsverwaltung

Alle Workloads werden nicht gleich erstellt. In jeder Umgebung gibt es Workloads, die einen direkten und konstanten Einfluss auf das Geschäft haben. Es gibt auch unterstützende Geschäftsprozesse und Workloads, die einen geringeren Einfluss auf das Gesamtgeschäft haben. In diesem Schritt identifiziert und implementiert das Cloudbetriebsteam anfängliche Anforderungen zur Unterstützung des gesamten IT-Portfolios.

**Zielvorgaben:**

- Implementieren einer Verwaltungsbaseline, um die für alle Produktionsworkloads erforderlichen Standardvorgänge zu definieren.
- Aushandeln von Geschäftsverpflichtungen mit dem Cloudstrategieteam, um einen Plan für erweiterte Betriebs- und Resilienzanforderungen zu entwickeln.
- Erweitern der Verwaltungsbaseline, wenn für die Mehrzahl der Workloads zusätzliche Vorgänge erforderlich sind.
- Anwenden erweiterter Betriebsanforderungen auf Zielzonen und Ressourcen an, die höhere kritische Workloads unterstützen.
- Dokumentieren von Betriebsentscheidungen im IT-Portfolio in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Hinweis zur Erreichung der Zielvorgaben:**

- **[Verwaltungsbaseline](../manage/considerations/discipline.md):**

  - [Bestand und Transparenz](../manage/considerations/inventory.md): [Mit cloudnativen Tools](../manage/azure-management-guide/inventory.md) können Sie [Daten erfassen](../manage/monitor/data-collection.md), [Warnungen konfigurieren](../manage/monitor/index.md) und die [Überwachungsplattform implementieren](../manage/monitor/index.md), die am besten zu Ihrem Betriebsmodell passt.
  - [Betriebsbezogene Compliance](../manage/considerations/operational-compliance.md): Die höchsten Prozentsätze von Ausfällen sind in der Regel auf Änderungen der Ressourcenkonfiguration oder schlechte Wartungspraktiken zurückzuführen. Befolgen Sie den [Leitfaden zur Azure-Serververwaltung](../manage/azure-server-management/index.md), um cloudnative Tools zur Verwaltung von Patches und Änderungen an der Ressourcenkonfiguration zu implementieren.
  - [Schutz und Wiederherstellung](../manage/considerations/protect.md): Ausfälle sind auf jeder Plattform unvermeidlich. Wenn eine Unterbrechung auftritt, können Sie sich mit [Sicherungs- und Wiederherstellungslösungen](../manage/azure-management-guide/protect-recover.md) vorbereiten, um die Dauer solcher Unterbrechungen zu minimieren.

- **[Erweiterter Betrieb](../manage/design-principles.md):** Nutzen Sie die Verwaltungsbaseline als Grundlage für Gespräche zur [Geschäftsausrichtung](../manage/considerations/business-alignment.md), um Klarheit bezüglich der [Wichtigkeit](../manage/considerations/criticality.md), der [geschäftlichen Auswirkungen](../manage/considerations/impact.md) und der [betrieblichen Verpflichtungen](../manage/considerations/commitment.md) zu schaffen. Die Geschäftsausrichtung hilft bei der Quantifizierung und Validierung von Anforderungen für eine [erweiterte Baseline](../manage/azure-management-guide/enhanced-baseline.md), der Verwaltung spezifischer [Technologieplattformen](../manage/azure-management-guide/workload-specialization.md) oder [workloadspezifischer Vorgänge](../manage/azure-management-guide/platform-specialization.md).

- **Durchführen einer Architekturüberprüfung:** Zum Erfüllen von Betriebsanforderungen sind möglicherweise Architekturänderungen auf Workloadebene erforderlich. [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework/cost/tradeoffs) und [Azure Architecture Review](https://docs.microsoft.com/assessments?id=azure-architecture-review) können diese Gespräche mit dem technischen Besitzer einer bestimmten Workload unterstützen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-2-consistently-apply-the-management-baseline"></a>Schritt 2: Konsistentes Anwenden der Verwaltungsbaseline

Unternehmenszuverlässigkeit erfordert eine konsistente Anwendung der Verwaltungsbaseline. Diese Konsistenz ergibt sich aus den entsprechenden Unternehmensrichtlinien, IT-Prozessen und automatisierten Tools, um die Implementierung der Verwaltungsbaseline für alle betroffenen Ressourcen zu steuern.

**Zielvorgaben:**

- Sicherstellen, dass die Verwaltungsbaseline für alle betroffenen Systeme ordnungsgemäß angewendet wird.
- Dokumentieren der Richtlinien zur Ressourcenkonsistenz, Prozesse und Entwurfsanleitungen in der [Vorlage für die Fachrichtung „Ressourcenkonsistenz“](../govern/resource-consistency/template.md).

**Hinweis zur Erreichung der Zielvorgaben:**

- Achten Sie darauf, dass bei allen Workloads und Ressourcen ordnungsgemäße [Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) eingehalten werden, und setzen Sie [Kennzeichnungskonventionen mithilfe von Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) mit einem spezifischen Schwerpunkt auf Tags für „Wichtigkeit“ durch.
- Wenn Sie mit Cloudgovernance noch nicht vertraut sind, richten Sie [Governancerichtlinien, -prozesse und -fachrichtungen](../govern/index.md) mithilfe der Governancemethodik ein.
- Wenn Sie mit der Fachrichtung „Kostenverwaltung“ noch nicht vertraut sind, sollten Sie sich mit dem Artikel [Verbesserungen der Kostenverwaltung](../govern/guides/complex/cost-management-improvement.md) befassen und sich dabei auf den Abschnitt [Implementierung](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices) konzentrieren.

> [!NOTE]
> **Schritte zum Einstieg in eine Zuverlässigkeitspartnerschaft mit anderen Teams:** Verschiedene Entscheidungen im gesamten Lebenszyklus der Cloudeinführung können einen direkten Einfluss auf die Zuverlässigkeit haben. Die folgenden Schritte unterstützen Sie bei der Gliederung der Partnerschaften und der unterstützenden Anstrengungen, die erforderlich sind, um konsistente Zuverlässigkeit im gesamten IT-Portfolio bereitzustellen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-3-define-your-strategy"></a>Schritt 3: Definieren Ihrer Strategie

**Zielvorgaben:**

- Aufzeichnen von Motivationen, Ergebnissen und geschäftlichen Begründungen in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Sicherstellen, dass die Verwaltungsbaseline betriebliche Unterstützung bereitstellt, die der strategischen Richtung der Cloudeinführung entspricht.

**Hinweis zur Erreichung der Zielvorgaben:**

- [Verstehen der Motivationen](../strategy/motivations.md): Wichtige Geschäftsereignisse und einige Migrationsgründe sind tendenziell kostensensibel, was die Wichtigkeit der Kostenkontrolle für alle nachfolgenden Bemühungen erhöht. Andere zukunftsgerichtete Motivationen, die mit Innovation oder Wachstum durch Migration zu tun haben, können sich ggf. mehr auf den Umsatz konzentrieren. Das Verstehen von Motivationen hilft Ihnen zu verstehen, wie hoch die Priorität der Kostenverwaltung sein sollte.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Einige fiskalische Ergebnisse neigen dazu, extrem kostenempfindlich zu sein. Wenn sich die gewünschten Ergebnisse den fiskalischen Metriken zuordnen lassen, sollten Sie frühzeitig in die Fachrichtung „Kostenverwaltung“ investieren.
- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md): Die geschäftliche Begründung dient als allgemeine Übersicht über den Gesamtfinanzplan für die Cloudeinführung. Dies kann eine gute Quelle für die anfängliche Budgetplanung sein.

Strategische Entscheidungen wirken sich direkt auf die Zuverlässigkeit aus, durchlaufen den Einführungslebenszyklus und werden zu langfristigen Vorgängen. Durch strategische Klarheit werden die Zuverlässigkeitsbemühungen verbessert.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-4-develop-a-cloud-adoption-plan"></a>Schritt 4: Entwickeln eines Cloudeinführungsplans

Der digitale Bestand (oder die Analyse des vorhandenen IT-Portfolios) kann bei der Validierung der geschäftlichen Begründung helfen und einen verfeinerten Überblick über das gesamte IT-Portfolio bieten. Der Einführungsplan bietet Klarheit bezüglich der Zeitachse der Aktivitäten während der Einführung. Das Ausrichten des Plans und der Analyse des digitalen Bestands ermöglicht die Planung zukünftiger Abhängigkeiten der Betriebsverwaltung. Wenn Sie den Plan verstehen, wird das Cloud-Betriebsteam auch in die Entwicklungszyklen integriert, um Änderungen an der Verwaltungs Basislinie zu evaluieren und zu planen.

**Zielvorgaben:**

- Aktualisieren der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um die Änderung widerzuspiegeln, die für die Umsetzung der gewünschten Strategie erforderlich ist. Die aufgezeichneten Änderungen können Folgendes umfassen:
  - Eine Bewertung des vorhandenen digitalen Bestands.
  - Einen Cloudeinführungsplan, der die erforderlichen Änderungen und die damit verbundenen Aufgaben widerspiegelt.
  - Die Organisationsänderung, die für die Umsetzung des Plans erforderlich ist.
  - Einen Plan zur Ermittlung der Fähigkeiten, die benötigt werden, damit das vorhandene Team die erforderliche Aufgaben erfolgreich erfüllen kann.
- Arbeiten Sie mit dem Governanceteam zusammen, um Kostenmodelle und Vorhersagemodelle auszurichten, einschließlich Bemühungen, Ausgaben durch quantitative Analysen zu optimieren.

**Hinweis zur Erreichung der Zielvorgaben:**

- [Erfassen von Bestandsdaten](../digital-estate/inventory.md). Einrichten einer Datenquelle für die Analyse des digitalen Bestands vor der Einführung.
- [Bewährte Methode: Azure Migrate](../plan/contoso-migration-assessment.md). Verwenden Sie Azure Migrate, um den Bestand zu erfassen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization). Während der inkrementellen Rationalisierung kann eine quantitative Analyse für die Zwecke der Budgeterstellung Cloudkandidaten identifizieren.
- [Abstimmen von Kostenmodellen und Vorhersagemodellen](../digital-estate/calculate.md). Verwenden Sie Azure Cost Management, um Kosten- und Vorhersagemodelle durch [Erstellen von Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)abzustimmen.
- [Entwickeln Ihres Cloudeinführungsplans](../plan/plan-intro.md#build-your-cloud-adoption-plan). Erstellen Sie einen Plan mit ausführbaren Workloads, Ressourcen- und Zeitachsendetails.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-5-implement-landing-zone-best-practices"></a>Schritt 5: Implementieren von bewährten Methoden für Zielzonen

Die Bereitschaftsmethodik des Cloud Adoption Framework konzentriert sich stark auf die Entwicklung von Zielzonen zum Hosten von Workloads in der Cloud. Bei der Implementierung Zielzone können sich mehrere Entscheidungen auf den Betrieb auswirken. Wenden Sie sich an das Cloudbetriebsteam, um sich bei der Überprüfung der Zielzone in Bezug auf Betriebsverbesserungen unterstützen zu lassen. Wenden Sie sich auch an das Cloudgovernanceteam, um die Richtlinien für „Ressourcenkonsistenz“ und den Entwurfsleitfaden zu verstehen, die sich möglicherweise auf den Entwurf der Zielzone auswirken.

**Zielvorgaben:**

- Bereitstellen mindestens einer Zielzone, die Workloads im kurzfristigen Einführungsplan hosten kann.
- Sicherstellen, dass alle Zielzonen Betriebsentscheidungen und Ressourcenkonsistenzanforderungen erfüllen.

**Hinweis zur Erreichung der Zielvorgaben:**

- [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-operations.md): Bewährte Methoden zur Verbesserung des Betriebs innerhalb einer bestimmten Zielzone.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudbetriebsteam <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-6-complete-waves-of-adoption-effort-and-change"></a>Schritt 6: Abschließen von Phasen der Einführungsbemühungen und -änderung

Langfristige Vorgänge können von den Entscheidungen beeinflusst werden, die während der Migration und der Innovationsbemühungen getroffen werden. Die Beibehaltung einer konsistenten Ausrichtung zu einem frühen Zeitpunkt in den Einführungsprozessen trägt dazu bei, Hindernisse für Produktionsreleases zu beseitigen und den Aufwand zu verringern, der für das Onboarding von neuen Lösungen in Betriebsverwaltungsverfahren erforderlich ist.

**Zielvorgaben:**

- Testen der Betriebsbereitschaft von Produktionsbereitstellungen mithilfe von Ressourcenkonsistenzrichtlinien.
- Überprüfen der Einhaltung von Entwurfsrichtlinien und Betriebsanforderungen für Ressourcenkonsistenz.
- Dokumentieren aller erweiterten Betriebsanforderungen in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Hinweis zur Erreichung der Zielvorgaben:**

- [Checkliste zur Bereitschaft der Umgebung](../migrate/migration-considerations/prerequisites/planning-checklist.md)
- [Prüfliste vor der Höherstufung](../migrate/migration-considerations/optimize/ready.md)
- [Checkliste für Produktionsreleases](../migrate/migration-considerations/optimize/promote.md)

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudbetriebsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="value-statement"></a>Wertaussage

Die oben beschriebenen Schritte helfen dabei, die richtigen Steuerungen und Prozesse zu implementieren, die erforderlich sind, um die Zuverlässigkeit im Unternehmen und für alle gehosteten Ressourcen sicherzustellen.
