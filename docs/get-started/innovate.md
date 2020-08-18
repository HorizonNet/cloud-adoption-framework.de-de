---
title: 'Erste Schritte: Erstellen neuer Produkte und Dienste in der Cloud'
description: Hier finden Sie Informationen zur Innovationsmethodik – einem Ansatz, an dem Sie sich bei der Entwicklung neuer Cloudprodukte und -dienste orientieren können.
author: JanetCThomas
ms.author: janet
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 94c66af70be7c3683e459719eb6e2a73e74e66d9
ms.sourcegitcommit: 264382fcb31ad0c6387c15a74127f288f8920995
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87805448"
---
# <a name="get-started-accelerate-new-product-and-service-innovation-in-the-cloud"></a>Erste Schritte: Beschleunigen neuer Produkt- und Dienstinnovationen in der Cloud

Die Entwicklung neuer Produkte und Dienste in der Cloud erfordert eine andere Herangehensweise als die Migration. Die Innovationsmethodik im Cloud Adoption Framework für Azure etabliert einen Ansatz, der als Leitfaden für die Entwicklung neuer Produkte und Dienste dienen kann.

Dieser Leitfaden basiert auf den Abschnitten des Cloud Adoption Framework, die in der folgenden Abbildung hervorgehoben sind. Innovationen sind zwar weniger vorhersehbar als eine Standardmigration, passen aber dennoch in den Kontext des weiter gefassten Cloudeinführungsplans. Dieser Leitfaden kann Ihrem Unternehmen dabei helfen, die für Innovationen erforderliche Unterstützung zu bieten und eine Struktur für den Aufbau eines ausgewogenen Portfolios im Rahmen der Cloudeinführung bereitzustellen.

![Diagramm des Cloud Adoption Framework einschließlich der Innovationsmethodik](../_images/get-started/innovation-map.png)

## <a name="step-1-document-the-business-strategy"></a>Schritt 1: Dokumentieren der Geschäftsstrategie

Erstellen Sie zur Vermeidung gängiger Hindernisse eine klare und prägnante Geschäftsstrategie für Innovationen. Die Einigkeit der Projektbeteiligten im Hinblick auf Beweggründe und erwartete Geschäftsergebnisse beeinflusst die Entscheidungen, die das Cloudeinführungsteam trifft.

**Ziele:**

- Verwenden Sie die [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um Beweggründe und gewünschte Geschäftsergebnisse zu erfassen.

<!-- docsTest:ignore "Get started: Accelerate migration" -->

**Hinweis zur Erreichung der Ziele:**

- [Beweggründe](../strategy/motivations.md): Der erste Schritt bei der strategischen Ausrichtung besteht darin, einen Konsens über die Beweggründe für die Innovationsbestrebungen zu erzielen. Beginnen Sie mit dem Verstehen und Kategorisieren von Beweggründen und gemeinsamen Themen der Beteiligten aus dem Geschäftsbereich und dem IT-Bereich.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Nachdem die Beweggründe ausgerichtet wurden, können die gewünschten Geschäftsergebnisse erfasst werden. Diesen Informationen können Sie klare Metriken entnehmen, mit denen Sie die Gesamttransformation messen können.
- [Ausgewogene Gestaltung des Portfolios:](../strategy/balance-the-portfolio.md) Innovation ist nicht der richtige Einführungspfad für alle Workloads. Dieser Einführungsansatz eignet sich eher für neue, benutzerdefinierte Anwendungen oder Workloads, für die eine Umstrukturierung oder vollständige Neuerstellung *erforderlich* ist. Wenn die Beweggründe stark zu Innovationen für alle Workloads tendieren, ist es wichtig, das Portfolio zu überprüfen, um sicherzustellen, dass sich mit diesen Investitionen die gewünschte Rendite erzielen lässt. Die Modernisierung bestimmter Ressourcen sowie kleinere Neuerstellungen können zwar innovativ sein, hierfür sind jedoch ggf. folgende Informationen besser geeignet: [Erste Schritte: Beschleunigen der Migration](./migrate.md).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-2-evaluate-the-business-justification"></a>Schritt 2: Bewerten der geschäftlichen Begründung

Bewerten Sie in diesem ersten Durchgang für die Erstellung des Geschäftsszenarios die anfängliche Wertschöpfung einer potenziellen Cloudeinführung. In diesem Schritt soll anhand einer einfachen Frage eine gemeinsame Linie für alle Beteiligten erzielt werden: Ist die Einführung der Cloud allgemein angesichts der verfügbaren Daten eine kluge Geschäftsentscheidung? Auf der Grundlage dieser Fragestellung kann das Team besser gemeinsam ermitteln, wie dieses Innovationsprojekt dazu beiträgt, die prognostizierten Anforderungen der Benutzer im Rahmen des Ziels der Cloudeinführung zu erfüllen.

**Ziele:**

- Verwenden Sie die [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um die geschäftliche Begründung festzuhalten.

**Hinweis zur Erreichung der Ziele:**

- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md): Vor der Bewertung der einzelnen Innovationsmöglichkeiten in der Cloud sollten Sie eine allgemeine geschäftliche Begründung erstellen, an der sich die Beteiligten im Zusammenhang mit dem allgemeinen Einführungsplan orientieren können.
- [Konsens über den geschäftlichen Nutzen](../innovate/business-value.md): In der Anfangsphase des Prozesses lässt sich der Nutzen einer Innovation unter Umständen nicht so leicht quantifizieren. Die Übung in diesem Artikel kann dabei helfen, die Ausrichtung im Hinblick auf den geschäftlichen Nutzen einer bestimmten Innovationsbestrebung zu bewerten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>Schritt 3: Erfassen von Daten und Analysieren von Ressourcen und Workloads

In den meisten Unternehmen können Innovationen durch die Nutzung bereits vorhandener Ressourcen wie Anwendungen, virtuellen Computern (VMs) und Daten beschleunigt werden. Bei der Innovationsplanung ist es wichtig zu verstehen, wie und wann diese Ressourcen in die Cloud migriert werden.

**Ziele:**

- Erfassen Sie Rohdaten zum vorhandenen Bestand (z. B. Anwendungen, VMs und Daten).
- Wenn die vorgeschlagene Innovation von vorhandenem Bestand abhängt, erstellen Sie Folgendes:
  - Quantitative Analyse des unterstützenden Bestands, der zur Unterstützung der geplanten Innovation erforderlich ist
  - Qualitative Analyse aller unterstützenden Workloads, die für die Bereitstellung der Innovation erforderlich sind
- Berechnen Sie die Kosten des neuen Bestands, der für die Innovationsbestrebungen erforderlich ist.
- Aktualisieren Sie die geschäftliche Begründung in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) mit präziseren Berechnungen.

**Leitfaden zur Erreichung der Zielvorgaben:**

Ermittlung und Bewertung bieten eine präzisere Anpassung auf technischer Ebene. Anschließend können Sie einen Aktionsplan für die Migration aller abhängigen Workloads erstellen, die für die geplante Innovation erforderlich sind. Dieses Szenario ist eine weit verbreitete Vorgehensweise bei Unternehmen mit bereits vorhandenen Datenquellen, zentralisierten Anwendungen oder Dienstebenen, die für die Bereitstellung von Innovationen im Kontext des restlichen Unternehmens erforderlich sind. 

Sollten abhängige Systeme vorhanden sein, können Sie sich bei der Ermittlung und Bewertung an den folgenden Artikeln orientieren:

- [Vorhandener Systembestand](../digital-estate/inventory.md): Der erste Schritt besteht darin, sich auf der Grundlage eines programm- und datengesteuerten Ansatzes mit dem Ist-Zustand vertraut zu machen. Ermitteln und sammeln Sie Daten, um alle Bewertungsaktivitäten zu ermöglichen.
- [Inkrementelle Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization): Optimieren der Bewertungsbemühungen, um sich möglicherweise sogar zur Unterstützung des Geschäftsszenarios auf eine qualitative Analyse aller Ressourcen zu konzentrieren. Fügen Sie dann eine umfassende qualitative Analyse für die ersten zehn Workloads hinzu.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-4-plan-for-migration-of-dependent-assets"></a>Schritt 4: Planen der Migration abhängiger Ressourcen

Wenn neue Innovationen von vorhandenen Workloads oder Ressourcen abhängig sind, bietet die Vorlage für den Cloudeinführungsplan einen beschleunigten Ansatz für die Entwicklung eines Projektbacklogs. Das Backlog kann dann geändert werden, um Ermittlungsergebnisse, Rationalisierung, erforderliche Fertigkeiten und Partnerverträge widerzuspiegeln.

**Ziele:**

- Bereitstellen der Backlogvorlage.
- Aktualisieren der Vorlage mit den ersten 10 zu migrierenden Workloads.
- Aktualisieren der Personen und der Geschwindigkeit (Zeitaufwand der Personen), um das Releasetiming zu schätzen.
- Zeitachsenrisiken:
  - Mangelnde Vertrautheit mit Azure DevOps kann den Bereitstellungsvorgang verlangsamen.
  - Komplexität und Daten, die für die einzelnen Workloads verfügbar sind, können sich ebenfalls auf die Zeitplanung auswirken.

**Hinweis zur Erreichung der Ziele:**

- [Vorlage für den Cloudeinführungsplan](../plan/template.md): Bereitstellen der Basisvorlage.
- [Workloadausrichtung](../plan/workloads.md): Definieren von Workloads im Backlog.
- [Aufwandsausrichtung](../plan/assets.md): Passen Sie Ressourcen und Workloads im Rückstand an, um den Aufwand für priorisierte Workloads eindeutig zu definieren.
- [Ausrichtung von Personen und Zeit](../plan/iteration-paths.md): Legen Sie Iteration, Geschwindigkeit und Releases für die Workloads fest.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-5-align-governance-requirements-to-your-adoption-plan"></a>Schritt 5: Ausrichten der Governanceanforderungen an Ihrem Einführungsplan

Zahlreiche Hindernisse lassen sich bereits im Vorfeld vermeiden, indem die geplanten Innovationen mit dem Governanceteam besprochen werden. Manchmal sind für innovative neue Lösungen möglicherweise Vorgehensweisen erforderlich, die nicht als solide Governancemethoden betrachtet werden. Einige dieser erforderlichen Features werden möglicherweise sogar durch automatisierte Tools für die Durchsetzung der Governance blockiert.

**Ziele:**

- Sorgen Sie für Transparenz und Verständnis im Hinblick auf Innovationsbedarf und Governanceeinschränkungen.
- Aktualisieren Sie bei Bedarf Richtlinien und Prozesse, um Änderungen oder Ausnahmen für bereits vorhandene Governanceeinschränkungen zu implementieren.

**Hinweis zur Erreichung der Ziele:**

Diese Links helfen dem Einführungsteam dabei, den vom Cloudgovernanceteam verfolgten Ansatz besser zu verstehen:

- [Governanceansatz](../govern/index.md): Diese Methodik beschreibt einen Prozess für Überlegungen zu Unternehmensrichtlinien und -prozessen. Dann können Sie die Fachrichtungen aufbauen, die erforderlich sind, um Governance in Ihrem gesamten Cloudunternehmen zu gewährleisten.
- [Definieren der Unternehmensrichtlinie:](../govern/corporate-policy.md) Identifizieren und mindern Sie Geschäftsrisiken.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-6-define-operational-needs-and-business-commitments"></a>Schritt 6: Definieren betrieblicher Anforderungen und geschäftlicher Verpflichtungen

Definieren Sie den Plan für langfristige operative Zuständigkeiten für die geplante Innovation. Entspricht die festgelegte Verwaltungsbaseline Ihren betrieblichen Anforderungen? Falls nicht, prüfen Sie spezifische Finanzierungsoptionen im Zusammenhang mit der Technologie, die diese Innovation unterstützt.

**Ziele:**

- Führen Sie die [Microsoft Azure-Architekturüberprüfung](https://docs.microsoft.com/assessments/?id=azure-architecture-review) durch, um verschiedene Architektur- und Betriebsentscheidungen zu bewerten.
- Passen Sie die [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) an, um ggf. erforderliche erweiterte Vorgänge zu berücksichtigen.

**Hinweis zur Erreichung der Ziele:**

- [Erweitern der Verwaltungsbaseline](../manage/best-practices.md): Dieser Abschnitt von Cloud Adoption Framework führt den Leser durch verschiedene Übergänge in die cloudbasierte Betriebsverwaltung.
- [Spezifische Angaben zu erweiterten Vorgängen](../manage/design-principles.md): Entdecken Sie Möglichkeiten, Ihre Verwaltungsbaseline zu übertreffen.
- Sollten erweiterte Vorgänge zur Unterstützung Ihrer betrieblichen Anforderungen erforderlich sein, bewerten Sie die [geschäftlichen Verpflichtungen](../manage/considerations/business-alignment.md), um betriebliche Zuständigkeiten für beide Teams zu bestimmen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-7-deploy-an-aligned-landing-zone"></a>Schritt 7: Bereitstellen einer ausgerichteten Zielzone

Alle in der Cloud gehosteten Ressourcen befinden sich in einer Zielzone. Für diese Zielzone gelten ggf. explizite Governance-, Sicherheits- und Betriebsanforderungen. Es kann sich dabei aber auch um ein neues Abonnement ohne Unterstützung durch andere Teams handeln. In allen Szenarios ist es wichtig, mit einer Zielzone zu beginnen, die von Anfang an auf die Governance- und Betriebsanforderungen abgestimmt ist. 

Die Verwendung einer freigegebenen Zielzone bereits bei Beginn hilft Ihrem Team dabei, Richtlinienverstöße frühzeitig bei der Entwicklung zu erkennen und nicht erst, wenn die Lösung für die Produktion freigegeben wird. Bei einer frühen Erkennung kann Ihr Team Hindernisse beseitigen, und das Einführungs- und das Governanceteam haben genug Zeit, Änderungen vorzunehmen.

**Ziele:**

- Stellen Sie in der Anfangsphase einer Innovation eine erste Zielzone für erste Experimente mit geringem Risiko bereit.
- Entwickeln Sie zusammen mit dem Cloudkompetenzzentrum oder dem zentralen IT-Team einen Plan für das Refactoring, um sicherzustellen, dass dieser mit Governance-, Sicherheits- und Betriebsaspekten in Einklang steht.
- Zeitachsenrisiken:
  - Governance-, Betriebs- und Sicherheitsanforderungen für die ersten zehn Workloads können diesen Prozess verlangsamen. Das Refactoring der ersten Zielzone und der nachfolgenden Zielzonen dauert länger, sollte aber parallel zu den Migrationsmaßnahmen erfolgen.

**Hinweis zur Erreichung der Ziele:**

- [Auswählen einer Zielzone](../ready/landing-zone/index.md): Ermitteln Sie anhand dieses Abschnitts den richtigen Ansatz für die Bereitstellung einer Zielzone basierend auf Ihrem Einführungsmuster. Stellen Sie dann diese standardisierte Codebasis bereit.
- [Erweitern der Zielzone](../ready/considerations/index.md): Identifizieren Sie unabhängig vom Ausgangspunkt Lücken in der bereitgestellten Zielzone, um erforderliche Komponenten für Ressourcenorganisation, Sicherheit, Governance, Compliance und Betrieb hinzuzufügen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudplattformteam <li> Cloudeinführungsteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-8-innovate-in-the-cloud"></a>Schritt 8: Entwickeln innovativer Cloudlösungen

Die Innovationsmethodik bietet Informationen zu gängigen Tools und Produktverwaltungsmethoden für Innovationen in der Cloud. Diese Schritte helfen Ihnen beim Einstieg in diesen Ansatz.

**Ziele:**

- Technologiebasierte Lösungen, die das Leben Ihrer Kunden bereichern und zur Wertschöpfung für das Unternehmen beitragen.
- Prozesse und Tools zur Beschleunigung der Iteration für diese Lösungen sowie zur Steigerung des Nutzens mithilfe der Cloud:
  - Iterative Entwicklungsansätze
  - Benutzerdefinierte Anwendungen
  - Technologiebasierte Lösungen
  - Integration physischer Produkte und Technologien mithilfe von IoT.
  - Umgebungsintelligenz: Integration nicht intrusiver Technologien in eine Umgebung
  - Azure Cognitive Services: Big Data-, KI-, Machine Learning- und Vorhersagelösungen.

**Hinweis zur Erreichung der Ziele:**

- [Konsens über den geschäftlichen Nutzen](../innovate/business-value.md): Beginnen Sie hiermit, falls der letzte Konsens über den geschäftlichen Nutzen mehr als drei Monate zurückliegt oder noch kein solcher Konsens erarbeitet wurde.
- [Azure-Innovationsleitfaden](../innovate/innovation-guide/index.md): Verwenden Sie den Azure-Innovationsleitfaden, um die Bereitstellung innovativer Lösungen zu beschleunigen. Machen Sie sich hierzu mit den Tools und Prozessen vertraut, die Ihnen dabei helfen, ein Minimum Viable Product (MVP) zu erstellen.
- [Bewährte Methoden für Innovationen](../innovate/best-practices/index.md): Kombinieren von Azure-Diensten, um eine Toolkette für digitale Innovationen zu erstellen.
- [Feedbackschleifen](../innovate/considerations/adoption.md): Entwickeln Sie verbesserte Feedbackschleifen, um Ihre Kunden schnell mit beeindruckenden Innovationen zu versorgen.

## <a name="step-9-assess-the-innovation-maturity-of-your-organization"></a>Schritt 9: Bewerten der Innovationsreife Ihrer Organisation

Das KI-Reifegradmodell unterstützt Sie bei der Entwicklung Ihrer Innovationsstrategie. Hierbei handelt es sich um ein kostenloses Tool, das Organisationen dabei hilft, zu bewerten, ob sie für die Erstellung und den Betrieb KI-basierter Systeme bereit sind. Es gibt vier Reifegrade: grundlegend, annähernd, ambitioniert und ausgereift. Jeder dieser Reifegrade umfasst gewisse Kriterien, auf deren Grundlage sich ermitteln lässt, ob Ihre Organisation in der Lage ist, bestimmte Arten von KI-Lösungen einzuführen, die damit verbundenen Risiken zu mindern und Strategien zu implementieren. 

Die Bewertung dauert zwischen fünf und zehn Minuten und ermittelt die Bereitschaft Ihrer Organisation in vier Kategorien: Strategie, Kultur, Organisationsmerkmale und Fähigkeiten. Durch die Bewertung in diesen Kategorien kann das KI-Reifegradmodell ein Ergebnis für Ihre Organisation berechnen und eine Schätzung bezüglich der KI-Innovationsreife in Form einer Kurve abgeben.

**Ziele:**

- Verwenden Sie das [KI-Reifegradmodell](https://aiready.microsoft.com), um die KI-Reife Ihrer Organisation für die Erstellung KI-basierter Systeme zu bewerten.

**Hinweis zur Erreichung der Ziele:**

- Nach Abschluss der Bewertung gibt das Tool ein Ergebnis für Ihre geschätzte KI-Innovationsreife aus.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudkompetenzzentrum <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Die in diesem Leitfaden beschriebenen Schritte helfen Ihnen und Ihren Teams dabei, innovative Lösungen in der Cloud zu erstellen, die zur Wertschöpfung für das Unternehmen beitragen und sich durch eine angemessene Governance sowie durch eine durchdachte Architektur auszeichnen.

## <a name="next-steps"></a>Nächste Schritte

Das Cloud Adoption Framework ist eine Lebenszykluslösung. Es kann Ihnen dabei helfen, eine Innovationsjourney zu beginnen. Es kann Ihrer Organisation nicht nur dabei helfen, mit der Entwicklung von Innovationen zu beginnen, sondern auch dazu beitragen, den Innovationsreifegrad der Teams zu erhöhen, die die Innovationsbestrebungen unterstützen. 

Die folgenden Teams können die nächsten Schritte ausführen, um ihre Anstrengungen noch weiter zu optimieren. Diese parallelen Prozesse sind nicht linear und sollten nicht als Hindernisse betrachtet werden. Stattdessen handelt es sich jeweils um einen parallelen Wertstrom, der dazu beiträgt, die allgemeine Bereitschaft Ihres Unternehmens für die Cloud zu verbessern.

| Team | Nächste Iteration |
|---|---|
| Cloudeinführungsteam&nbsp;&nbsp; | [Prozessverbesserungen](../innovate/considerations/index.md) bieten Einblicke in die Ansätze zur Bereitstellung von Innovationen, die für Kunden relevant sind und die Einführung attraktiv machen. |
| Cloudstrategieteam&nbsp;&nbsp; | Die [Strategiemethodik](../strategy/index.md) und die [Planungsmethodik](../plan/index.md) sind iterative Prozesse, die sich mit dem Einführungsplan weiterentwickeln. Kehren Sie zu diesen Übersichtsseiten zurück, und führen Sie Ihre geschäftlichen und technischen Strategien weiter aus. |
| Cloudplattformteam&nbsp;&nbsp; | Kehren Sie zur [Bereitschaftsmethodik](../ready/index.md) zurück, um die gesamte Cloudplattform, die die Migration oder andere Einführungsmaßnahmen unterstützt, weiter voranzutreiben. |
| Cloudgovernanceteam&nbsp;&nbsp; | Verwenden Sie die [Governancemethodik](../govern/index.md), um Governanceprozesse, -richtlinien und -disziplinen weiter zu verbessern. |
| Cloudbetriebsteam&nbsp;&nbsp; | Verwenden Sie die [Verwaltungsmethodik](../manage/index.md), um umfassendere Vorgänge in Azure bereitzustellen. |
