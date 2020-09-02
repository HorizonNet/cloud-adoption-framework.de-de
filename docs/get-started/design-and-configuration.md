---
title: 'Erste Schritte: Entsperren des Umgebungsentwurfs und der Konfiguration'
description: Erste Schritte beim Entwerfen und Konfigurieren Ihrer Cloudumgebung.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 526fe646f41f76985c7a4d3ba47cd2df474949c1
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88881256"
---
# <a name="get-started-design-and-configuration"></a>Erste Schritte: Entwurf und Konfiguration

Der Umgebungsentwurf und die -konfiguration sind die häufigsten Hemmnisse bei Migrations- oder innovationsorientierten Einführungsmaßnahmen. Die schnelle Implementierung eines Entwurfs, der Ihren langfristigen Einführungsplan unterstützt, kann schwierig sein. Dieser Artikel stellt einen Ansatz und eine Reihe von Schritten vor, die helfen sollen, häufige Hindernisse zu überwinden und Ihre Einführungsbemühungen zu beschleunigen.

![Erste Schritte bei Entwurf und Konfiguration](../_images/get-started/environment-map.png)

Der technische Aufwand, der erforderlich ist, um eine effektive Umgebung und Konfiguration zu entwerfen, kann komplex sein. Sie können den Umfang der Maßnahmen verwalten, um die Erfolgschancen für das Cloudplattformteam zu verbessern. Die größte Herausforderung besteht in der Abstimmung zwischen mehreren Projektbeteiligten. Einige dieser Projektbeteiligten sind berechtigt, die Einführungsmaßnahmen zu verhindern oder zu verlangsamen. Mit diesen Schritten können Sie schnell kurzfristige Ziele erreichen und langfristigen Erfolg erzielen.

## <a name="step-1-document-the-business-strategy"></a>Schritt 1: Dokumentieren der Geschäftsstrategie

Um häufige Migrationshindernisse zu vermeiden, stellen Sie sicher, dass Sie über eine klare und prägnante Geschäftsstrategie für die Migration verfügen. Die Ausrichtung von Beteiligten an Motivationen, erwarteten Geschäftsergebnissen und der geschäftlichen Begründung sind während der Einführung und der Umgebungskonfiguration wichtig.

Eine klare und präzise Geschäftsstrategie unterstützt das Cloudplattformteam dabei, zu verstehen, was wichtig ist und was bei Entscheidungen über die Umgebungskonfiguration priorisiert werden sollte. Insbesondere hilft es den Teams, Entscheidungen zu treffen, wenn sie gezwungen sind, sich zwischen Innovationsgeschwindigkeit oder Einhaltung von Kontrollen zu entscheiden.

**Ziele:**

- Verwenden der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx), um Beweggründe, gewünschte Geschäftsergebnisse und die geschäftliche Begründung auf hoher Ebene zu erfassen.

**Hinweis zur Erreichung der Zielvorgaben:**

- [Beweggründe](../strategy/motivations.md): Der erste Schritt bei der strategischen Ausrichtung besteht darin, einen Konsens über die Beweggründe für die Migrationsbemühungen zu erzielen. Beginnen Sie mit dem Verstehen und Kategorisieren von Beweggründen und gemeinsamen Themen verschiedener Beteiligter aus dem Geschäfts- und IT-Bereich.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Nachdem die Beweggründe ausgerichtet wurden, können die gewünschten Geschäftsergebnisse erfasst werden. Diese Informationen stellt klare Metriken bereit, mit denen Sie die Gesamttransformation messen können.
- [Erstellen eines Geschäftsszenarios für die Cloudmigration](../strategy/cloud-migration-business-case.md): Nun können Sie mit der Entwicklung eines Geschäftsszenarios für die Migration mit klaren Formeln und Tools beginnen, die bei der geschäftlichen Rechtfertigung helfen können.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams | Informierte Teams |
| --- | --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung | <li> Cloudplattformteam |

## <a name="step-2-assess-the-digital-estate"></a>Schritt 2: Bewerten der digitalen Ressourcen

Ermittlung und Bewertung bieten eine tiefere Ebene der technischen Ausrichtung und unterstützen Sie beim Erstellen eines umsetzbaren Plans zur Verwirklichung der Strategie. In diesem Schritt überprüfen Sie den Geschäftsfall mithilfe von Daten zum aktuellen Zustand der Umgebung. Anschließend führen Sie eine quantitative Analyse dieser Daten und eine tiefgreifende qualitative Bewertung der Workloads mit der höchsten Priorität durch.

Die Ausgabe der Bewertung des digitalen Bestands ermöglicht dem Cloudplattformteam einen klaren Überblick über den Endzustand der Umgebung und die Anforderungen, die zur Unterstützung des Einführungsplans erforderlich sind.

**Ziele:**

- Rohdaten für den vorhandenen Bestand.
- Quantitative Analyse des vorhandenen Bestands, um die geschäftliche Begründung zu verfeinern.
- Qualitative Analyse der ersten 10 Workloads.
- Aktualisierte geschäftliche Begründung in der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx).

**Hinweis zur Erreichung der Zielvorgaben:**

- [Vorhandener Systembestand](../digital-estate/inventory.md): Der erste Schritt besteht darin, sich auf der Grundlage eines programm- und datengesteuerten Ansatzes mit dem Ist-Zustand vertraut zu machen. Ermitteln und sammeln Sie Daten, um alle Bewertungsaktivitäten zu ermöglichen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization): Optimieren der Bewertungsbemühungen, um sich möglicherweise sogar zur Unterstützung des Geschäftsszenarios auf eine qualitative Analyse aller Ressourcen zu konzentrieren. Fügen Sie dann eine umfassende, qualitativ hochwertige Analyse für die ersten 10 zu migrierenden Workloads hinzu.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams | Informierte Teams |
| --- | --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam | <li> Cloudplattformteam |

## <a name="step-3-create-a-cloud-adoption-plan"></a>Schritt 3: Erstellen eines Cloudeinführungsplans

Ihr Cloudeinführungsplan bietet einen beschleunigten Ansatz für die Entwicklung eines Projektbacklogs. Das Backlog kann dann geändert werden, um Bewertungsergebnisse, Rationalisierung, erforderliche Fertigkeiten und Partnerverträge widerzuspiegeln.

Eine Überprüfung des kurzfristigen Cloudeinführungsplans und das Backlog unterstützen das Cloudplattformteam dabei, die Anforderungen der Umgebung in den nächsten Monaten zu verstehen. Dieser Hintergrund ermöglicht es dem Team, die „Definition der Fertigstellung“ für die ersten Zielzonen enger zu fassen.

**Ziele:**

- Bereitstellen der Backlogvorlage.
- Aktualisieren der Vorlage mit den ersten 10 zu migrierenden Workloads.
- Aktualisieren der Personen und der Geschwindigkeit (Zeitaufwand der Personen), um das Releasetiming zu schätzen.
- Zeitachsenrisiken:
  - Mangelnde Vertrautheit mit Azure DevOps kann den Bereitstellungsvorgang verlangsamen.
  - Komplexität und Daten, die für die einzelnen Workloads verfügbar sind, können sich ebenfalls auf die Zeitplanung auswirken.

**Hinweis zur Erreichung der Ziele:**

- [Cloudeinführungsplan](../plan/template.md): Definieren Sie Ihren Plan anhand der Basisvorlage.
- [Workloadausrichtung](../plan/workloads.md): Definieren von Workloads im Backlog.
- [Aufwandsausrichtung](../plan/assets.md): Richten Sie Ressourcen und Workloads im Backlog aus, um den Aufwand für priorisierte Workloads eindeutig zu definieren.
- [Ausrichtung von Personen und Zeit](../plan/iteration-paths.md): Legen Sie Iteration, Geschwindigkeit und Releases für die migrierten Workloads fest.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams | Informierte Teams |
| --- | --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudplattformteam | <li> Cloudplattformteam |

## <a name="step-4-deploy-the-first-landing-zone"></a>Schritt 4: Bereitstellen Ihrer ersten Zielzone

Anfänglich benötigt das Cloudeinführungsteam eine Zielzone, die die Anforderungen der ersten Workloads unterstützen kann. Im Laufe der Zeit wird die Zielzone skaliert, um komplexere Workloads zu ermöglichen. Beginnen Sie zunächst mit einer Zielzone, um dem Cloudplattformteam und dem Cloudeinführungsteam frühzeitiges Lernen zu ermöglichen.

**Ziele:**

- Bereitstellen einer ersten Zielzone für anfängliche Migrationen mit geringem Risiko.
- Entwickeln eines Plans für die Umgestaltung mit dem Cloudkompetenzzentrum oder der zentralen IT-Abteilung.
- Zeitachsenrisiken:
  - Governance-, Betriebs- und Sicherheitsanforderungen für die ersten zehn Workloads können diesen Prozess verlangsamen. Die eigentliche Umgestaltung der ersten Zielzone und der nachfolgenden Zielzonen dauert länger, sollte aber parallel zu den Migrationsmaßnahmen erfolgen.

**Hinweis zur Erreichung der Ziele:**

- [Auswählen einer Zielzone](../ready/landing-zone/index.md): Verwenden Sie diesen Abschnitt, um den richtigen Ansatz für die Bereitstellung einer Zielzone basierend auf Ihrem kurzfristigen Einführungsplan zu ermitteln. Stellen Sie dann diese standardisierte Codebasis bereit.
- [Erweitern der Zielzone](../ready/considerations/index.md): Versuchen Sie noch nicht, langfristige Governance-, Sicherheits- oder Vorgangseinschränkungen zu erfüllen, es sei denn, Sie müssen den kurzfristigen Einführungsplan unterstützen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudplattformteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-5-deploy-an-initial-governance-foundation"></a>Schritt 5: Bereitstellen einer ersten Grundlage für Governance

Governance ist ein wichtiger Faktor für den langfristigen Erfolg einer beliebigen Migrationsbemühung. Geschwindigkeit der Migration und geschäftlichen Auswirkungen ist wichtig. Geschwindigkeit ohne Governance kann jedoch gefährlich sein. Ihre Organisation muss Entscheidungen hinsichtlich der Governance treffen, die Ihren Einführungsmustern und Ihren Governance- und Complianceanforderungen entsprechen.

Wenn diese Entscheidungen getroffen werden, fließen sie wieder in die parallel stattfindenden Anstrengungen des Cloudplattformteams ein.

**Ziele:**

- Bereitstellen einer ersten Grundlage für Governance.
- Abschließen eines Governancebenchmarks, um zukünftige Verbesserungen zu planen.
- Zeitachsenrisiken:
  - Verbesserung der Richtlinien- und Governanceimplementierung kann eine Woche bis vier weitere Wochen pro Fachrichtung hinzufügen.

**Hinweis zur Erreichung der Ziele:**

- [Governanceansatz](../govern/index.md): Diese Methodik beschreibt einen Prozess für Überlegungen zu Unternehmensrichtlinien und -prozessen. Dann bauen Sie die Fachrichtungen auf, die erforderlich sind, um Governance in Ihrem gesamten Cloudunternehmen zu gewährleisten.
- [Governance-Benchmarktool](../govern/benchmark.md): Erkennen Sie Lücken in Ihrem aktuellen Zustand, damit Sie für die Zukunft planen können.
- [Anfängliche Governancegrundlage](../govern/guides/complex/prescriptive-guidance.md): Verstehen der Fachrichtungen Identitätsbaseline, Sicherheitsbaseline und Bereitstellungsbeschleunigung, die erforderlich sind, um ein Governance-MVP (Minimum Viable Product) zu schaffen, das als Grundlage für jede Einführung dient.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams | Zu Rate gezogene Teams |
| --- | --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung | <li> Cloudplattformteam |

## <a name="step-6-implement-an-operations-baseline"></a>Schritt 6: Implementieren einer Betriebsbaseline

Vorgangsverwaltung ist eine weitere Voraussetzung für eine erfolgreiche Migration. Eine Migration in die Cloud ohne Verständnis der laufenden Abläufe ist eine riskante Entscheidung. Parallel zur Migration sollten Sie mit der Planung für längerfristige Vorgänge beginnen.

Wenn diese Pläne erstellt werden, fließen sie wieder in die parallel stattfindenden Anstrengungen des Cloudplattformteams ein.

**Zielvorgaben:**

- Bereitstellen einer Verwaltungsbaseline.
- Vervollständigen der Arbeitsmappe zum Operations Management.
- Identifizieren von Workloads, die eine Microsoft Azure Well-Architected Review-Bewertung erfordern.
- Zeitachsenrisiken:
  - Überprüfen der Arbeitsmappe: Planen Sie eine Stunde pro Anwendungsbesitzer ein.
  - Schließen Sie die Microsoft Azure Well-Architected Review-Bewertung ab: Planen Sie eine Stunde pro Anwendung ein.

**Hinweis zur Erreichung der Ziele:**

- [Einrichten einer Verwaltungsbaselinie](../manage/index.md)
- [Definieren von geschäftlichen Verpflichtungen](../manage/considerations/business-alignment.md)
- [Erweitern der Verwaltungsbaseline](../manage/best-practices.md)
- [Spezifische Angaben zu erweiterten Vorgängen](../manage/design-principles.md)

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams | Zu Rate gezogene Teams |
| --- | --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung | <li> Cloudplattformteam |

## <a name="step-7-expand-the-landing-zone"></a>Schritt 7: Erweitern der Zielzone

Wenn das Cloudeinführungsteam mit den ersten Migrationen beginnt, kann das Cloudplattformteam mit Unterstützung durch das Cloudgovernance- und Cloudbetriebsteam mit der Entwicklung der Konfiguration des Endzustands der Umgebung beginnen. Abhängig von der Geschwindigkeit des Cloudeinführungsplans muss dieser Vorgang möglicherweise in iterativen Releases erfolgen. Funktionalität kann vor den Anforderungen des Einführungsplans hinzugefügt werden.

**Ziele:**

- Einführen eines testgesteuerten Entwicklungsansatzes zum Umgestalten von Zielzonen.
- Verbessern der Governance von Zielzonen.
- Erweitern des Betriebs von Zielzonen.
- Implementieren von Sicherheit für Zielzonen.

**Hinweis zur Erreichung der Ziele:**

- [Umgestalten von Zielzonen](../ready/landing-zone/refactor.md)
- [Testgesteuerte Entwicklung von Zielzonen](../ready/considerations/test-driven-development.md)
- [Erweitern der Governance von Zielzonen](../ready/considerations/landing-zone-governance.md)
- [Erweitern des Betriebs von Zielzonen](../ready/considerations/landing-zone-operations.md)
- [Erweitern der Sicherheit von Zielzonen](../ready/considerations/landing-zone-security.md)

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudplattformteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Die in diesem Leitfaden beschriebenen Schritte können Ihnen und Ihren Teams dabei helfen, den Weg zu einer unternehmenstauglichen Cloudumgebung zu beschleunigen, die ordnungsgemäß konfiguriert ist.

## <a name="next-steps"></a>Nächste Schritte

Erwägen Sie diese nächsten Schritte in einer zukünftigen Iteration, um auf Ihren anfänglichen Bemühungen aufzubauen:

- [Lernpfade für die technische Bereitschaft der Umgebung](../ready/suggested-skills.md)
- [Checkliste für die Planung der Migrationsumgebung](../migrate/migration-considerations/prerequisites/planning-checklist.md)
