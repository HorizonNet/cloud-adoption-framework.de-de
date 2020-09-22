---
title: 'Erste Schritte: Beschleunigen der Migration'
description: Empfohlene Schritte für die Ausrichtung von Beteiligten, die Migrationsplanung, das Bereitstellen einer Zielzone und das Migrieren Ihrer ersten 10 Workloads.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c806816f8d85e71f1b310dab0e89013e9946bc03
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89603311"
---
# <a name="get-started-accelerate-migration"></a>Erste Schritte: Beschleunigen der Migration

Eine ordnungsgemäße Ausrichtung von Geschäfts- und IT-Beteiligten trägt dazu bei, Migrationsblockaden zu überwinden und die Migration zu beschleunigen. In diesem Artikel werden die empfohlenen Schritte für die folgenden Aufgaben beschrieben:

- Ausrichtung der Projektbeteiligten
- Migrationsplanung
- Bereitstellen einer Zielzone
- Migrieren der ersten zehn Workloads

Außerdem finden Sie hier hilfreiche Informationen zur Implementierung geeigneter Governance- und Verwaltungsprozesse.

Nutzen Sie diesen Leitfaden, um die Prozesse und Materialien zu optimieren, die für die allgemeine Ausrichtung der Migrationsmaßnahmen erforderlich sind. Dieser Leitfaden basiert auf den Methodiken des Cloud Adoption Framework, die in der folgenden Abbildung hervorgehoben sind:

![Erste Schritte bei der Migration in Azure](../_images/get-started/migration-map.png)

Wenn Ihr Migrationsszenario atypisch ist, können Sie eine personalisierte Bewertung der Migrationsbereitschaft Ihrer Organisation erhalten, indem Sie die [SMART-Bewertung (Strategic Migration and Readiness Tool)](/assessments/?id=strategic-migration-assessment) verwenden. Verwenden Sie diese, um den Leitfaden zu identifizieren, der Ihren aktuellen Anforderungen am besten entspricht.

## <a name="get-started"></a>Erste Schritte

Der für die Migration von Workloads erforderliche technische Aufwand und Vorgang ist relativ unkompliziert. Es ist wichtig, den Migrationsprozess effizient abzuschließen. Die strategische Bereitschaft zur Migration besitzt einen noch größeren Einfluss auf den Zeitplan und den erfolgreichen Abschluss der gesamten Migration.

Um die Einführung zu beschleunigen, müssen Sie Maßnahmen ergreifen, um das Cloudeinführungsteam während der Migration zu unterstützen. Dieser Leitfaden umreißt diese iterativen Aufgaben, um Kunden auf dem richtigen Weg zu einer Cloudmigration zu unterstützen. Um die Wichtigkeit der unterstützenden Schritte zu zeigen, wird die Migration in diesem Artikel als Schritt 10 aufgeführt. In der Praxis beginnt das Cloudeinführungsteam wahrscheinlich parallel zu den Schritten 4 oder 5 mit einer ersten Pilotmigration.

## <a name="step-1-align-stakeholders"></a>Schritt 1: Ausrichten von Beteiligten

Um häufige Migrationshindernisse zu vermeiden, erstellen Sie eine klare und prägnante Geschäftsstrategie für die Migration. Die Ausrichtung von Projektbeteiligten im Hinblick auf Beweggründe und erwartete Geschäftsergebnisse beeinflusst die Entscheidungen, die vom Cloudeinführungsteam getroffen werden.

- [Beweggründe](../strategy/motivations.md): Der erste Schritt bei der strategischen Ausrichtung besteht darin, einen Konsens über die Beweggründe für die Migrationsbemühungen zu erzielen. Beginnen Sie mit dem Verstehen und Kategorisieren von Beweggründen und gemeinsamen Themen verschiedener Beteiligter aus dem Geschäfts- und IT-Bereich.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Nachdem die Beweggründe ausgerichtet wurden, können die gewünschten Geschäftsergebnisse erfasst werden. Diese Informationen stellt klare Metriken bereit, mit denen Sie die Gesamttransformation messen können.

**Ziele:**

- Verwenden der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx), um Beweggründe und gewünschte Geschäftsergebnisse aufzuzeichnen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-2-align-partner-support"></a>Schritt 2: Ausrichten des Partnersupports

Partner, Microsoft-Dienste oder verschiedene Microsoft-Programme sind verfügbar, um Sie während des gesamten Migrationsvorgangs zu unterstützen.

- [Informieren Sie sich über die Partneroptionen](../migrate/migration-considerations/assess/partnership-options.md), um die richtige Ebene für Partnerschaft und Support zu finden.

**Ziele:**

- Einrichten der Geschäftsbedingungen oder andere vertraglichen Vereinbarungen, bevor Sie unterstützende Partner einbinden.
- Identifizieren genehmigter Partner in der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>Schritt 3: Erfassen von Daten und Analysieren von Ressourcen und Workloads

Nutzen Sie die Ermittlung und Bewertung, um die technische Ausrichtung zu verbessern und einen Aktionsplan für Ihre Strategie zu erstellen. Überprüfen Sie im Rahmen dieses Schritts den Geschäftsfall mithilfe von Daten zur aktuellen Umgebung. Führen Sie anschließend eine quantitative Analyse und eine tiefgreifende qualitative Bewertung der Workloads mit der höchsten Priorität durch.

- [Vorhandener Systembestand](../digital-estate/inventory.md): Machen Sie sich unter Verwendung eines programm- und datengesteuerten Ansatzes mit dem Ist-Zustand vertraut. Ermitteln und sammeln Sie Daten, um alle Bewertungsaktivitäten zu ermöglichen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization): Optimieren der Bewertungsbemühungen, um sich möglicherweise sogar zur Unterstützung des Geschäftsszenarios auf eine qualitative Analyse aller Ressourcen zu konzentrieren. Fügen Sie dann eine umfassende, qualitativ hochwertige Analyse für die ersten 10 zu migrierenden Workloads hinzu.

**Zielvorgaben:**

- Rohdaten für vorhandenen Bestand.
- Quantitative Analyse für vorhandenen Bestand, um die geschäftliche Begründung zu verfeinern.
- Qualitative Analyse der ersten 10 Workloads.
- Geschäftliche Begründung (dokumentiert in der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx)).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-4-make-a-business-case"></a>Schritt 4: Erstellen eines Geschäftsszenarios

Das Erstellen des Geschäftsszenarios für die Migration ist wahrscheinlich eine iterative Konversation zwischen Beteiligten. Bewerten Sie in diesem ersten Durchgang bei der Erstellung des Geschäftsszenarios die anfängliche Wertschöpfung aus einer potenziellen Cloudmigration. Ziel dieses Schritts ist es, sicherzustellen, dass sich alle Beteiligten eine einfache Frage stellen: Ist die allgemeine Einführung der Cloud angesichts der verfügbaren Daten eine kluge Geschäftsentscheidung?

- Der [Aufbau eines Geschäftsfalls für die Cloudmigration](../strategy/cloud-migration-business-case.md) ist ein guter Ausgangspunkt für die Entwicklung eines Geschäftsfalls für die Migration. Die Klarheit von Formeln und Tools kann die geschäftliche Begründung unterstützen.

**Ziele:**

- Verwenden der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx), um die geschäftliche Begründung festzuhalten.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam |

## <a name="step-5-create-a-migration-plan"></a>Schritt 5: Erstellen eines Migrationsplans

Ein Cloudeinführungsplan bietet einen beschleunigten Ansatz für die Entwicklung eines Projektbacklogs. Das Backlog kann dann geändert werden, um Ermittlungsergebnisse, Rationalisierung, erforderliche Fertigkeiten und Partnerverträge widerzuspiegeln.

- [Cloudeinführungsplan](../plan/template.md): Definieren Sie Ihren Cloudeinführungsplan mithilfe der Basisvorlage.
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

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-6-build-a-skills-readiness-plan"></a>Schritt 6: Erstellen eines Bereitschaftsplans für Qualifikationen

Vorhandene Mitarbeiter können eine praktische Rolle bei der Migration spielen, aber möglicherweise sind auch zusätzliche Fertigkeiten erforderlich. Suchen Sie in diesem Schritt nach Wegen, um diese Qualifikationen zu entwickeln, oder nutzen Sie Partner, um diese Qualifikationen zu erweitern.

- [Erstellen eines Bereitschaftsplans für Fertigkeiten](../plan/adapt-roles-skills-processes.md). Werten Sie schnell Ihre vorhandenen Qualifikationen aus, um zu ermitteln, welche anderen Qualifikationen das Team entwickeln sollte.

**Ziele:**

- Hinzufügen eines Bereitschaftsplans für Qualifikationen zur [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-7-deploy-and-align-a-landing-zone"></a>Schritt 7: Bereitstellen und Ausrichten einer Zielzone

Alle migrierten Ressourcen werden in einer Zielzone bereitgestellt. Die Zielzone unterstützt zunächst kleinere Workloads und wird im Laufe der Zeit skaliert, um komplexere Workloads bewältigen zu können.

- [Auswählen einer Zielzone](../ready/landing-zone/index.md): Ermitteln Sie den richtigen Ansatz für die Bereitstellung einer Zielzone basierend auf Ihrem Einführungsmuster. Stellen Sie dann diese standardisierte Codebasis bereit.
- [Erweitern der Zielzone](../ready/considerations/index.md): Identifizieren Sie unabhängig von Ihrem Ausgangspunkt Lücken in der bereitgestellten Zielzone, und fügen Sie erforderliche Komponenten für Ressourcenorganisation, Sicherheit, Governance, Compliance und Betrieb hinzu.

**Ziele:**

- Stellen Sie Ihre erste Zielzone für anfängliche Migrationen mit geringem Risiko bereit.
- Entwickeln Sie einen Refactoringplan mit dem Cloudkompetenzzentrum oder dem zentralen IT-Team.
- Zeitachsenrisiken:
  - Governance-, Betriebs- und Sicherheitsanforderungen für die ersten zehn Workloads können diesen Prozess verlangsamen.
  - Das Refactoring der ersten Zielzone und der nachfolgenden Zielzonen dauert zwar länger, sollte aber parallel zu den Migrationsmaßnahmen erfolgen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudplattformteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-8-migrate-your-first-10-workloads"></a>Schritt 8: Migrieren der ersten 10 Workloads

Der für die Migration der ersten 10 Workloads erforderliche technische Aufwand ist relativ unkompliziert. Außerdem handelt es sich um einen iterativen Prozess, den Sie beim Migrieren von weiteren Ressourcen wiederholen. In diesem Prozess werden Ihre Workloads bewertet, bereitgestellt und anschließend für die Produktionsumgebung freigegeben.

![Phasen der iterativen Migrationsbemühungen: Bewertung, Bereitstellung, Freigabe](../_images/migrate/methodology-effort-only.png)

Mithilfe von Cloudmigrationstools können alle virtuellen Computer eines Rechenzentrums in einem einzelnen Durchlauf oder in einer einzelnen Iteration migriert werden. Es ist eher üblich, bei jeder Iterationen eine geringere Anzahl von Workloads zu migrieren. Die Aufteilung der Migration in kleinere Einheiten ist zwar mit einem höheren Planungsaufwand verbunden, verringert jedoch die technischen Risiken und die Auswirkungen des Change Management der Organisation.

Mit jeder Iteration wird das Cloudeinführungsteam beim Migrieren von Workloads besser. Die folgenden Schritte helfen dem technischen Team dabei, seine Fähigkeiten zu verbessern:

1. Migrieren Sie Ihre ersten Workloads in einem reinen IaaS-Ansatz (Infrastructure-as-a-Service) mithilfe der Tools, die im [Azure-Migrationsleitfaden](../migrate/azure-migration-guide/index.md) beschrieben werden.
2. Erweitern Sie die Tooloptionen auf die Verwendung von Migration und Modernisierung mithilfe der [Migrationsbeispiele](../migrate/azure-best-practices/contoso-migration-overview.md).
3. Entwickeln Sie Ihre technische Strategie mithilfe von umfassenderen Ansätzen, die in den [bewährten Methoden für die Azure-Cloudmigration](../migrate/azure-best-practices/index.md) beschrieben werden.
4. Verbessern Sie Konsistenz, Zuverlässigkeit und Leistung durch einen effizienten Migrationsfactoryansatz, wie unter [Optimierungen des Migrationsvorgangs](../migrate/migration-considerations/index.md) beschrieben.

**Ziele:**

Fortlaufende Verbesserung der Fähigkeit des Einführungsteams, Workloads zu migrieren.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-9-hand-off-production-workloads-to-cloud-governance"></a>Schritt 9: Übergeben von Produktionsworkloads an Cloudgovernance

Governance ist ein wichtiger Faktor für den langfristigen Erfolg einer beliebigen Migrationsbemühung. Geschwindigkeit der Migration und geschäftlichen Auswirkungen ist wichtig. Geschwindigkeit ohne Governance kann jedoch gefährlich sein. Ihre Organisation muss Entscheidungen hinsichtlich der Governance treffen, die Ihren Einführungsmustern und Ihren Governance- und Complianceanforderungen entsprechen.

- [Governanceansatz](../govern/index.md): Diese Methodik beschreibt einen Prozess für Überlegungen zu Ihren Unternehmensrichtlinien und -prozessen. Nach der Bestimmung Ihres Ansatzes können Sie die Disziplinen aufbauen, die erforderlich sind, um Governance für Ihre gesamte Enterprise Cloud-Einführung zu ermöglichen.
- [Anfängliche Governancegrundlage](../govern/guides/complex/prescriptive-guidance.md): Machen Sie sich mit den Disziplinen vertraut, die für die Erstellung eines Governance-MVP (Minimum Viable Product) erforderlich sind, das die Grundlage für jede Einführung bildet.
- [Governancebenchmark](https://aka.ms/adopt/assess/govern): Identifizieren Sie Lücken im aktuellen Zustand der Governance Ihrer Organisation. Erhalten Sie einen personalisierten Benchmarkbericht und einen zusammengestellten Leitfaden für die ersten Schritte.

**Ziele:**

- Bereitstellen einer ersten Grundlage für Governance.
- Abschließen eines Governancebenchmarks, um zukünftige Verbesserungen zu planen.
- Zeitplanrisiko: Die Verbesserung der Richtlinien- und Governanceimplementierung kann eine Woche bis vier weitere Wochen pro Fachrichtung hinzufügen.

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

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Mithilfe dieser Schritte können Teams ihre Migrationsmaßnahmen durch besseres Change Management und eine bessere Ausrichtung von Beteiligten beschleunigen. Diese Schritte können den Prozess verlangsamen. Darüber hinaus tragen diese Schritte zur Beseitigung gängiger Hindernisse sowie zur schnelleren Generierung eines Geschäftswerts bei.

## <a name="next-steps"></a>Nächste Schritte

Das Cloud Adoption Framework ist eine Lebenszykluslösung, die Sie beim Einstieg in eine Migration unterstützt. Darüber hinaus trägt sie zur Weiterentwicklung der Teams bei, die die Migration unterstützen. Die folgenden Teams können die nächsten Schritte ausführen, um ihre Fähigkeiten weiter zu optimieren. Diese parallelen Prozesse sind nicht linear und sollten nicht als Hindernisse betrachtet werden. Stattdessen handelt es sich jeweils um einen parallelen Wertstrom, der dazu beiträgt, die allgemeine Cloudbereitschaft Ihrer Organisation zu verbessern.

| Team | Nächste Iteration |
|--|--|
| Cloudeinführungsteam | Informieren Sie sich anhand des [Migrationsmodells](../migrate/migration-considerations/index.md) über den Weg zu einer Migrationsfactory mit effizienten fortlaufenden Migrationsfunktionen. |
| Cloudstrategieteam | Verbessern Sie nach und nach die [Strategiemethodik](../strategy/index.md) und die [Planungsmethodik](../plan/index.md) sowie den Einführungsplan. Sehen Sie sich diese Übersichten an, und verfolgen Sie Ihre geschäftlichen und technischen Strategien weiter. |
| Cloudplattformteam | Kehren Sie zur [Bereitschaftsmethodik](../ready/index.md) zurück, um die gesamte Cloudplattform, die die Migration oder andere Einführungsmaßnahmen unterstützt, weiter voranzutreiben. |
| Cloudgovernanceteam&nbsp;&nbsp; | Verwenden Sie die [Governancemethodik](../govern/index.md), um Governanceprozesse, -richtlinien und -disziplinen weiter zu verbessern. |
| Cloudbetriebsteam | Verwenden Sie die [Verwaltungsmethodik](../manage/index.md), um umfassendere Vorgänge in Azure bereitzustellen. |

Wenn Ihr Migrationsszenario atypisch ist, können Sie eine personalisierte Bewertung der Migrationsbereitschaft Ihrer Organisation erhalten, indem Sie die [SMART-Bewertung (Strategic Migration and Readiness Tool)](/assessments/?id=strategic-migration-assessment) verwenden. Ihre Antworten tragen dazu bei, den Leitfaden zu ermitteln, der am besten zu Ihren aktuellen Anforderungen passt.
