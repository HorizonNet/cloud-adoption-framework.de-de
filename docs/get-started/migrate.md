---
title: 'Erste Schritte: Beschleunigen der Migration'
description: Empfohlene Schritte für die Ausrichtung von Beteiligten, die Migrationsplanung, das Bereitstellen einer Zielzone und das Migrieren Ihrer ersten 10 Workloads.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 65a201886f9cbc67a58aa5bd14f53e928d4495b8
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076505"
---
# <a name="get-started-accelerate-migration"></a>Erste Schritte: Beschleunigen der Migration

Die richtige Ausrichtung von Geschäfts- und IT-Beteiligten kann Ihrem Unternehmen helfen, Migrationsblockaden zu überwinden und die Migrationsbemühungen zu beschleunigen. In diesem Artikel werden die empfohlenen Schritte für die folgenden Aufgaben beschrieben:

- Ausrichtung der Projektbeteiligten.
- Migrationsplanung.
- Bereitstellen einer Zielzone.
- Migrieren der ersten 10 Workloads.

Er kann Ihnen auch zu langfristigem Erfolg verhelfen, der durch eine ordnungsgemäße Governance und Verwaltung gewährleistet wird.

Verwenden Sie diesen Leitfaden, um die Anzahl an Materialien und die Prozesse zu reduzieren, die für die Abstimmung einer Gesamtmigration erforderlich sind. Bei diesem Vorgang werden die Abschnitte des Cloud Adoption Framework für Azure verwendet, die in der folgenden Abbildung hervorgehoben sind.

![Erste Schritte bei der Migration in Azure](../_images/get-started/migration-map.png)

Wenn Ihr Migrationsszenario atypisch ist, können Sie eine personalisierte Bewertung der Migrationsbereitschaft Ihrer Organisation erhalten, indem Sie die [SMART-Bewertung (Strategic Migration and Readiness Tool)](https://docs.microsoft.com/assessments/?id=strategic-migration-assessment) verwenden. Verwenden Sie diese, um den Leitfaden zu identifizieren, der Ihren aktuellen Anforderungen am besten entspricht.

## <a name="get-started"></a>Erste Schritte

Der für die Migration von Workloads erforderliche technische Aufwand und Vorgang ist relativ unkompliziert. Es ist wichtig, den Migrationsprozess effizient abzuschließen. Die strategische Bereitschaft zur Migration besitzt einen noch größeren Einfluss auf den Zeitplan und den erfolgreichen Abschluss der gesamten Migration.

Um die Einführung zu beschleunigen, müssen Sie Maßnahmen ergreifen, um das Cloudeinführungsteam während der Migration zu unterstützen. Dieser Leitfaden umreißt diese iterativen Aufgaben, um Kunden auf dem richtigen Weg zu einer Cloudmigration zu unterstützen. Um die Wichtigkeit der unterstützenden Schritte zu zeigen, wird die Migration in diesem Artikel als Schritt 10 aufgeführt. In Wirklichkeit wird das Cloudeinführungsteam wahrscheinlich parallel zu den Schritten 4 oder 5 mit seiner ersten Pilotmigration beginnen.

## <a name="step-1-align-stakeholders"></a>Schritt 1: Ausrichten von Beteiligten

Um häufige Migrationshindernisse zu vermeiden, erstellen Sie eine klare und prägnante Geschäftsstrategie für die Migration. Die Ausrichtung von Projektbeteiligten im Hinblick auf Beweggründe und erwartete Geschäftsergebnisse beeinflusst die Entscheidungen, die vom Cloudeinführungsteam getroffen werden.

- [Beweggründe](../strategy/motivations.md): Der erste Schritt bei der strategischen Ausrichtung besteht darin, einen Konsens über die Beweggründe für die Migrationsbemühungen zu erzielen. Beginnen Sie mit dem Verstehen und Kategorisieren von Beweggründen und gemeinsamen Themen verschiedener Beteiligter aus dem Geschäfts- und IT-Bereich.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Nachdem die Beweggründe ausgerichtet wurden, können die gewünschten Geschäftsergebnisse erfasst werden. Diese Informationen stellt klare Metriken bereit, mit denen Sie die Gesamttransformation messen können.

**Ziele:**

- Verwenden der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um Beweggründe und gewünschte Geschäftsergebnisse aufzuzeichnen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-2-align-partner-support"></a>Schritt 2: Ausrichten des Partnersupports

Partner, Microsoft-Dienste oder verschiedene Microsoft-Programme sind verfügbar, um Sie während des gesamten Migrationsvorgangs zu unterstützen.

- [Informieren Sie sich über die Partneroptionen](../migrate/migration-considerations/assess/partnership-options.md), um die richtige Ebene für Partnerschaft und Support zu finden.

**Ziele:**

- Einrichten der Geschäftsbedingungen oder andere vertraglichen Vereinbarungen, bevor Sie unterstützende Partner einbinden.
- Identifizieren genehmigter Partner in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>Schritt 3: Erfassen von Daten und Analysieren von Ressourcen und Workloads

Ermittlung und Bewertung bieten eine tiefere Ebene der technischen Ausrichtung und unterstützen Sie beim Erstellen eines umsetzbaren Plans zur Verwirklichung der Strategie. In diesem Schritt überprüfen Sie den Geschäftsfall mithilfe von Daten zur aktuellen Zustandsumgebung. Anschließend führen Sie eine quantitative Analyse dieser Daten und eine tiefgreifende qualitative Bewertung der Workloads mit der höchsten Priorität durch.

- [Vorhandener Systembestand](../digital-estate/inventory.md): Der erste Schritt besteht darin, sich auf der Grundlage eines programm- und datengesteuerten Ansatzes mit dem Ist-Zustand vertraut zu machen. Ermitteln und sammeln Sie Daten, um alle Bewertungsaktivitäten zu ermöglichen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization): Optimieren der Bewertungsbemühungen, um sich möglicherweise sogar zur Unterstützung des Geschäftsszenarios auf eine qualitative Analyse aller Ressourcen zu konzentrieren. Fügen Sie dann eine umfassende, qualitativ hochwertige Analyse für die ersten 10 zu migrierenden Workloads hinzu.

**Zielvorgaben:**

- Rohdaten für vorhandenen Bestand.
- Quantitative Analyse für vorhandenen Bestand, um die geschäftliche Begründung zu verfeinern.
- Qualitative Analyse der ersten 10 Workloads.
- Aktualisieren der geschäftlichen Begründung in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-4-make-a-business-case"></a>Schritt 4: Erstellen eines Geschäftsszenarios

Das Erstellen des Geschäftsszenarios für die Migration ist wahrscheinlich eine iterative Konversation zwischen Beteiligten. Bewerten Sie in diesem ersten Durchgang bei der Erstellung des Geschäftsszenarios die anfängliche Wertschöpfung aus einer potenziellen Cloudmigration. Ziel dieses Schritts ist es, sicherzustellen, dass sich alle Beteiligten eine einfache Frage stellen: Ist die allgemeine Einführung der Cloud angesichts der verfügbaren Daten eine kluge Geschäftsentscheidung?

- Der [Aufbau eines Geschäftsfalls für die Cloudmigration](../strategy/cloud-migration-business-case.md) ist ein guter Ausgangspunkt für die Entwicklung eines Geschäftsfalls für die Migration. Die Klarheit von Formeln und Tools kann die geschäftliche Begründung unterstützen.

**Ziele:**

- Verwenden der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um die geschäftliche Begründung festzuhalten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam |

## <a name="step-5-create-a-migration-plan"></a>Schritt 5: Erstellen eines Migrationsplans

Die Vorlage für den Cloudeinführungsplan bietet einen beschleunigten Ansatz für die Entwicklung eines Projektbacklogs. Das Backlog kann dann geändert werden, um Ermittlungsergebnisse, Rationalisierung, erforderliche Fertigkeiten und Partnerverträge widerzuspiegeln.

- [Vorlage für den Cloudeinführungsplan](../plan/template.md): Bereitstellen der Basisvorlage.
- [Workloadausrichtung](../plan/workloads.md): Definieren von Workloads im Backlog.
- [Aufwandsausrichtung](../plan/assets.md): Richten Sie Ressourcen und Workloads im Backlog aus, um den Aufwand für priorisierte Workloads eindeutig zu definieren.
- [Ausrichtung von Personen und Zeit](../plan/iteration-paths.md): Einrichten von Iterationen, Geschwindigkeit (Zeitaufwand der Personen) und Releases für die migrierten Workloads.

**Zielvorgaben:**

- Bereitstellen der Backlogvorlage.
- Aktualisieren der Vorlage mit den ersten 10 zu migrierenden Workloads.
- Aktualisieren der Personen und der Geschwindigkeit, um das Releasetiming zu schätzen.
- Zeitachsenrisiken:
  - Mangelnde Vertrautheit mit Azure DevOps kann den Bereitstellungsvorgang verlangsamen.
  - Komplexität und Daten, die für die einzelnen Workloads verfügbar sind, können sich ebenfalls auf die Zeitplanung auswirken.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-6-build-a-skills-readiness-plan"></a>Schritt 6: Erstellen eines Bereitschaftsplans für Qualifikationen

Vorhandene Mitarbeiter können eine praktische Rolle bei der Migration spielen, aber möglicherweise sind auch zusätzliche Fertigkeiten erforderlich. In diesem Schritt führt das Team eine Selbstbewertung durch, um Möglichkeiten zur Entwicklung dieser Fähigkeiten zu ermitteln oder Partner zu nutzen, um diese Fähigkeiten zu verbessern.

- [Erstellen eines Bereitschaftsplans für Fertigkeiten](../plan/adapt-roles-skills-processes.md). Evaluieren Sie schnell erforderliche und vorhandene Kenntnisse, um besser zu verstehen, welche Anforderungen für die Qualifizierung zu berücksichtigen sind.

**Ziele:**

- Hinzufügen eines Bereitschaftsplans für Qualifikationen zur [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-7-deploy-and-align-a-landing-zone"></a>Schritt 7: Bereitstellen und Ausrichten einer Zielzone

Alle migrierten Ressourcen werden innerhalb einer Zielzone bereitgestellt. Anfänglich ist die Zielzone einfach, um kleinere Workloads zu unterstützen. Im Laufe der Zeit wird sie skaliert, um komplexere Workloads zu ermöglichen.

- [Auswählen einer Zielzone](../ready/landing-zone/index.md): Ermitteln Sie anhand dieses Abschnitts den richtigen Ansatz für die Bereitstellung einer Zielzone basierend auf Ihrem Einführungsmuster. Stellen Sie dann diese standardisierte Codebasis bereit.
- [Erweitern der Zielzone](../ready/considerations/index.md): Identifizieren Sie unabhängig vom Ausgangspunkt Lücken in der bereitgestellten Zielzone, um erforderliche Komponenten für Ressourcenorganisation, Sicherheit, Governance, Compliance und Betrieb hinzuzufügen.

**Ziele:**

- Bereitstellen einer ersten Zielzone für anfängliche Migrationen mit geringem Risiko.
- Entwickeln eines Plans für die Umgestaltung mit dem Cloudkompetenzzentrum oder der zentralen IT-Abteilung.
- Zeitachsenrisiken:
  - Governance-, Betriebs- und Sicherheitsanforderungen für die ersten zehn Workloads können diesen Prozess verlangsamen.
  - Die eigentliche Umgestaltung der ersten Zielzone und der nachfolgenden Zielzonen dauert länger, sollte aber parallel zu den Migrationsmaßnahmen erfolgen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudplattformteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-8-migrate-your-first-10-workloads"></a>Schritt 8: Migrieren der ersten 10 Workloads

Der für die Migration der ersten 10 Workloads erforderliche technische Aufwand ist relativ unkompliziert. Außerdem handelt es sich um einen iterativen Prozess, den Sie beim Migrieren von weiteren Ressourcen wiederholen. In diesem Prozess bewerten Sie Ihre Workloads (siehe Schritt 4), stellen die Workloads bereit und geben sie anschließend für die Produktionsumgebung frei.

![Phasen der iterativen Migrationsbemühungen: Bewertung, Bereitstellung, Freigabe](../_images/migrate/methodology-effort-only.png)

Cloudmigrationstools ermöglichen es, alle VMs in einem Rechenzentrum in einem Durchgang oder einer Iteration zu migrieren. Es ist eher üblich, bei jeder Iterationen eine geringere Anzahl von Workloads zu migrieren. Das Aufteilen der Migration in kleinere Einheiten oder Releases erfordert mehr Planung, kleinere Workloadmengen verringern jedoch die technischen Risiken und die Auswirkungen des Change Management der Organisation.

Mit jeder Iteration wird das Cloudeinführungsteam beim Migrieren von Workloads besser. Mit diesen Schritten startet das technische Team in diese Reifekurve:

1. Migrieren Sie Ihre ersten Workloads in einem reinen IaaS-Ansatz (Infrastructure-as-a-Service) mithilfe der Tools, die im [Azure-Migrationsleitfaden](../migrate/azure-migration-guide/index.md) beschrieben werden.
2. Erweitern Sie die Tooloptionen auf die Verwendung von Migration und Modernisierung mithilfe der [Migrationsszenarien](../migrate/azure-best-practices/contoso-migration-overview.md).
3. Entwickeln Sie Ihre technische Strategie mithilfe von umfassenderen Ansätzen, die in den [bewährten Methoden für Migrationen](../migrate/azure-best-practices/index.md) beschrieben werden.
4. Verbessern Sie Konsistenz, Zuverlässigkeit und Leistung durch einen effizienten Migrationsfactoryansatz, wie unter [Optimierungen des Migrationsvorgangs](../migrate/migration-considerations/index.md) beschrieben.

**Ziele:**

Fortlaufende Verbesserung der Fähigkeit des Einführungsteams, Workloads zu migrieren.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-9-hand-off-production-workloads-to-cloud-governance"></a>Schritt 9: Übergeben von Produktionsworkloads an Cloudgovernance

Governance ist ein wichtiger Faktor für den langfristigen Erfolg einer beliebigen Migrationsbemühung. Geschwindigkeit der Migration und geschäftlichen Auswirkungen ist wichtig. Geschwindigkeit ohne Governance kann jedoch gefährlich sein. Ihre Organisation muss Entscheidungen hinsichtlich der Governance treffen, die Ihren Einführungsmustern und Ihren Governance- und Complianceanforderungen entsprechen.

- [Governanceansatz](../govern/index.md): Diese Methodik beschreibt einen Prozess für Überlegungen zu Unternehmensrichtlinien und -prozessen. Dann können Sie die Fachrichtungen aufbauen, die erforderlich sind, um Governance in Ihrem gesamten Cloudunternehmen zu gewährleisten.
- [Anfängliche Governancegrundlage](../govern/guides/complex/prescriptive-guidance.md): Verstehen der Fachrichtungen Identitätsbaseline, Sicherheitsbaseline und Bereitstellungsbeschleunigung, die erforderlich sind, um ein Governance-MVP (Minimum Viable Product) zu schaffen, das als Grundlage für jede Einführung dient.

**Ziele:**

- Bereitstellen einer ersten Grundlage für Governance.
- Abschließen eines Governancebenchmarks, um zukünftige Verbesserungen zu planen.
- Zeitplanrisiko: Die Verbesserung der Richtlinien- und Governanceimplementierung kann eine Woche bis vier weitere Wochen pro Fachrichtung hinzufügen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-10-hand-off-production-workloads-to-cloud-operations"></a>Schritt 10: Übergeben von Produktionsworkloads an den Cloudbetrieb

Vorgangsverwaltung ist eine weitere Voraussetzung für eine erfolgreiche Migration. Das Migrieren einzelner Workloads in die Cloud ohne Verständnis der laufenden Unternehmensabläufe ist eine riskante Entscheidung. Parallel zur Migration sollten Sie mit der Planung für längerfristige Vorgänge beginnen.

- [Einrichten einer Verwaltungsbaselinie](../manage/index.md)
- [Definieren von geschäftlichen Verpflichtungen](../manage/considerations/business-alignment.md)
- [Erweitern der Verwaltungsbaseline](../manage/best-practices.md)
- [Spezifische Angaben zu erweiterten Vorgängen](../manage/design-principles.md)

**Zielvorgaben:**

- Bereitstellen einer Verwaltungsbaseline.
- Vervollständigen der Arbeitsmappe zum Operations Management.
- Identifizieren von Workloads, die eine Microsoft Azure Well-Architected Review-Bewertung erfordern.
- Zeitachsenrisiken:
  - Überprüfen der Arbeitsmappe: Planen Sie eine Stunde pro Anwendungsbesitzer ein.
  - Schließen Sie die Microsoft Azure Well-Architected Review-Bewertung ab: Planen Sie eine Stunde pro Anwendung ein.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Mithilfe der in diesem Leitfaden beschriebenen Schritte können Ihre Teams ihre Migrationsaktivitäten durch besseres Change Management und die Ausrichtung von Beteiligten beschleunigen. Das Ausführen dieser Schritte kann den Prozess verlangsamen. Mit diesen Schritten werden auch gängige Hindernisse entfernt und die Umsetzung des Geschäftswerts beschleunigt.

## <a name="next-steps"></a>Nächste Schritte

Das Cloud Adoption Framework ist eine Lebenszykluslösung. Es kann Ihnen dabei helfen, eine Migration zu beginnen. Es kann Ihnen aber auch helfen, die Reife der Teams, die die Migrationsbemühungen unterstützen, zu fördern. Die folgenden Teams können die nächsten Schritte ausführen, um ihre Anstrengungen noch weiter zu optimieren. Diese parallelen Prozesse sind nicht linear und sollten nicht als Hindernisse betrachtet werden. Stattdessen handelt es sich jeweils um einen parallelen Wertstrom, der dazu beiträgt, die allgemeine Bereitschaft Ihres Unternehmens für die Cloud zu verbessern.

| Team  | Nächste Iteration |
|---|---|
| Cloudeinführungsteam&nbsp;&nbsp; | [Prozessverbesserungen](../migrate/migration-considerations/index.md) bieten Einblicke auf dem Weg zu einer Migrationsfactory mit effizienten fortlaufenden Migrationsfunktionen. |
| Cloudstrategieteam&nbsp;&nbsp; | Die [Strategiemethodik](../strategy/index.md) und die [Planungsmethodik](../plan/index.md) sind iterative Prozesse, die sich mit dem Einführungsplan weiterentwickeln. Kehren Sie zu diesen Übersichtsseiten zurück, und führen Sie Ihre geschäftlichen und technischen Strategien weiter aus. |
| Cloudplattformteam&nbsp;&nbsp; | Kehren Sie zur [Bereitschaftsmethodik](../ready/index.md) zurück, um die gesamte Cloudplattform, die die Migration oder andere Einführungsmaßnahmen unterstützt, weiter voranzutreiben. |
| Cloudgovernanceteam&nbsp;&nbsp; | Verwenden Sie die [Governancemethodik](../govern/index.md), um Governanceprozesse, -richtlinien und -disziplinen weiter zu verbessern. |
| Cloudbetriebsteam&nbsp;&nbsp; | Verwenden Sie die [Verwaltungsmethodik](../manage/index.md), um umfassendere Vorgänge in Azure bereitzustellen. |

Wenn Ihr Migrationsszenario atypisch ist, können Sie eine personalisierte Bewertung der Migrationsbereitschaft Ihrer Organisation erhalten, indem Sie die [SMART-Bewertung (Strategic Migration and Readiness Tool)](https://docs.microsoft.com/assessments/?id=strategic-migration-assessment) verwenden. Basierend auf den Antworten, die Sie während der Bewertung geben, können wir Ihnen helfen, die Anleitungen zu identifizieren, die Ihren aktuellen Anforderungen am besten entsprechen.
