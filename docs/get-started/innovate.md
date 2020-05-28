---
title: 'Erste Schritte: Erstellen neuer Produkte und Dienste in der Cloud'
description: Hier finden Sie Informationen zur Innovationsmethodik – einem Ansatz, an dem Sie sich bei der Entwicklung neuer Cloudprodukte und -dienste orientieren können.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 79c428da9d0be27c209fcc30686225217832dbe1
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862499"
---
# <a name="get-started-accelerate-new-product-and-service-innovation-in-the-cloud"></a>Erste Schritte: Beschleunigen neuer Produkt- und Dienstinnovationen in der Cloud

Die Erstellung neuer Produkte und Dienste in der Cloud erfordert eine andere Herangehensweise als die Migration. Die Innovationsmethodik im Cloud Adoption Framework für Azure etabliert einen Ansatz, der als Leitfaden für die Entwicklung neuer Produkte und Dienste dienen kann.

Dieser Leitfaden basiert auf den Abschnitten des Cloud Adoption Framework, die in der folgenden Abbildung hervorgehoben sind. Innovationen sind zwar weniger berechenbar als eine Standardmigration, passen aber immer noch in den Kontext des weiter gefassten Cloudeinführungsplans. Dieser Leitfaden kann Ihrem Unternehmen dabei helfen, die für Innovationsbestrebungen nötige Unterstützung zu bieten und die Struktur bereitzustellen, die zum Aufbau eines ausgeglichenen Portfolios im Rahmen der Cloudeinführung erforderlich ist.

![Erste Schritte zum Beschleunigen von Innovationen in der Cloud](../_images/get-started/innovation-map.png)

## <a name="step-1-document-the-business-strategy"></a>Schritt 1: Dokumentieren der Geschäftsstrategie

Erstellen Sie zur Vermeidung gängiger Hindernisse eine klare und prägnante Geschäftsstrategie für Innovationen. Die Ausrichtung von Projektbeteiligten im Hinblick auf Beweggründe und erwartete Geschäftsergebnisse beeinflusst die Entscheidungen, die vom Cloudeinführungsteam getroffen werden.

**Ziele:**

- Verwenden Sie die [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um Beweggründe und gewünschte Geschäftsergebnisse zu erfassen.

<!-- docsTest:ignore "Get started: Accelerate migration" -->

**Hinweis zur Erreichung der Ziele:**

- [Beweggründe](../strategy/motivations.md): Der erste Schritt bei der strategischen Ausrichtung besteht darin, einen Konsens über die Beweggründe für die Innovationsbestrebungen zu erzielen. Beginnen Sie mit dem Verstehen und Kategorisieren von Beweggründen und gemeinsamen Themen verschiedener Beteiligter aus dem Geschäfts- und IT-Bereich.
- [Geschäftsergebnisse](../strategy/business-outcomes/index.md): Nachdem die Beweggründe ausgerichtet wurden, können die gewünschten Geschäftsergebnisse erfasst werden. Diese Informationen stellt klare Metriken bereit, mit denen Sie die Gesamttransformation messen können.
- [Ausgewogenheit des Portfolios](../strategy/balance-the-portfolio.md): Innovation ist nicht der richtige Einführungspfad für alle Workloads. Dieser Einführungsansatz eignet sich eher für neue, benutzerdefinierte Anwendungen oder Workloads, für die eine Umstrukturierung oder vollständige Neuerstellung _erforderlich_ ist. Wenn die Beweggründe stark zu Innovationen für alle Workloads tendieren, ist es wichtig, das Portfolio zu untersuchen, um sicherzustellen, dass sich mit den entsprechenden Investitionen die gewünschte Rendite (Return On Investment, ROI) erzielen lässt. Die Modernisierung bestimmter Ressourcen sowie kleinere Neuerstellungen können zwar innovativ sein, hierfür sind jedoch ggf. folgende Informationen besser geeignet: [Erste Schritte: Beschleunigen der Migration](./migrate.md).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-2-evaluate-the-business-justification"></a>Schritt 2: Bewerten der geschäftlichen Begründung

Bewerten Sie in diesem ersten Durchgang für die Erstellung des Geschäftsszenarios die anfängliche Wertschöpfung einer potenziellen Cloudeinführung. Ziel dieses Schritts ist es, sicherzustellen, dass sich alle Beteiligten eine einfache Frage stellen: Ist die allgemeine Einführung der Cloud angesichts der verfügbaren Daten eine kluge Geschäftsentscheidung? Auf der Grundlage dieser Fragestellung kann das Team besser ermitteln, wie dieses Innovationsprojekt dazu beiträgt, die prognostizierten Anforderungen der Endbenutzer im Rahmen des Ziels der Cloudeinführung zu erfüllen.

**Ziele:**

- Verwenden Sie die [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), um die geschäftliche Begründung zu erfassen.

**Hinweis zur Erreichung der Ziele:**

- [Geschäftliche Begründung](../strategy/cloud-migration-business-case.md): Vor der Bewertung der einzelnen Innovationsmöglichkeiten in der Cloud sollten Sie eine allgemeine geschäftliche Begründung erstellen, an der sich die Beteiligten im Zusammenhang mit dem allgemeinen Einführungsplan orientieren können.
- [Konsens über den geschäftlichen Nutzen](../innovate/business-value.md): In der Anfangsphase des Prozesses lässt sich der Nutzen einer Innovation unter Umständen nicht so leicht quantifizieren. Die Übung in diesem Artikel kann dabei helfen, die Ausrichtung im Hinblick auf den geschäftlichen Nutzen einer bestimmten Innovationsbestrebung zu bewerten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>Schritt 3: Erfassen von Daten und Analysieren von Ressourcen und Workloads

In den meisten Unternehmen können Innovationen durch die Nutzung bereits vorhandener Ressourcen wie Anwendungen, virtuellen Computern und Daten beschleunigt werden. Bei der Innovationsplanung ist es wichtig zu verstehen, wie und wann diese Ressourcen in die Cloud migriert werden.

**Ziele:**

- Rohdaten zum vorhandenen Bestand (etwa Anwendungen, virtuelle Computer und Daten).
- Wenn die vorgeschlagene Innovation von vorhandenem Bestand abhängt, erstellen Sie Folgendes:
  - Quantitative Analyse des unterstützenden Bestands, der zur Unterstützung der geplanten Innovation erforderlich ist
  - Qualitative Analyse aller unterstützenden Workloads, die für die Bereitstellung der Innovation erforderlich sind
- Berechnen Sie die Kosten des neuen Bestands, der zur Unterstützung der Innovationsbestrebungen erforderlich ist.
- Aktualisieren Sie die geschäftliche Begründung in der [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) mit präziseren Berechnungen.

**Hinweis zur Erreichung der Ziele:**

Ermittlung und Bewertung ermöglichen eine fundiertere technische Ausrichtung, um einen Aktionsplan für die Migration aller abhängigen Workloads auszuarbeiten, die für die geplante Innovation erforderlich sind. Dieses Szenario ist eine weit verbreitete Vorgehensweise bei Unternehmen mit bereits vorhandenen Datenquellen, zentralisierten Anwendungen oder erforderlichen Dienstebenen, die für die Bereitstellung der Innovation im Kontext des restlichen Unternehmens erforderlich sind. Sollten abhängige Systeme vorhanden sein, können Sie sich bei der Ermittlung und Bewertung an den folgenden Artikeln orientieren.

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
- [Aufwandsausrichtung](../plan/assets.md): Richten Sie Ressourcen und Workloads im Backlog aus, um den Aufwand für priorisierte Workloads eindeutig zu definieren.
- [Ausrichtung von Personen und Zeit](../plan/iteration-paths.md): Legen Sie Iteration, Geschwindigkeit und Releases für die Workloads fest.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudstrategieteam |

## <a name="step-5-align-governance-requirements-to-your-adoption-plan"></a>Schritt 5: Ausrichten der Governanceanforderungen an Ihrem Einführungsplan

Zahlreiche Hindernisse lassen sich bereits im Vorfeld vermeiden, indem die geplanten Innovationen mit dem Governanceteam besprochen werden. Manchmal sind für innovative neue Lösungen möglicherweise Vorgehensweisen erforderlich, die nicht als solide Governancemethoden betrachtet werden. Einige dieser erforderlichen Features werden unter Umständen sogar durch Tools für die automatisierte Governanceerzwingung blockiert.

**Ziele:**

- Sorgen Sie für Transparenz und Verständnis im Hinblick auf Innovationsbedarf und Governanceeinschränkungen.
- Aktualisieren Sie bei Bedarf Richtlinien und Prozesse, um Änderungen oder Ausnahmen für bereits vorhandene Governanceeinschränkungen zu implementieren.

**Hinweis zur Erreichung der Ziele:**

Diese Links helfen dem Einführungsteam dabei, den vom Cloudgovernanceteam verfolgten Ansatz besser zu verstehen.

- [Governanceansatz](../govern/index.md): Diese Methodik beschreibt einen Prozess für Überlegungen zu Unternehmensrichtlinien und -prozessen. Dann können Sie die Fachrichtungen aufbauen, die erforderlich sind, um Governance in Ihrem gesamten Cloudunternehmen zu gewährleisten.
- [Definieren der Unternehmensrichtlinie](../govern/corporate-policy.md): Identifizieren und mindern Sie Geschäftsrisiken.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam <li> Cloudeinführungsteam | <li> Cloudstrategieteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-6-define-operational-needs-and-business-commitments"></a>Schritt 6: Definieren betrieblicher Anforderungen und geschäftlicher Verpflichtungen

Definieren Sie den Plan für langfristige operative Zuständigkeiten für die geplante Innovation. Ist die festgelegte Verwaltungsbaseline für Ihre betrieblichen Anforderungen ausreichend? Falls nicht, prüfen Sie spezifische Finanzierungsoptionen im Zusammenhang mit der Technologie, die diese Innovation unterstützt.

**Ziele:**

- Führen Sie [Microsoft Azure Well-Architected Review](https://docs.microsoft.com/assessments/?id=azure-architecture-review) durch, um verschiedene Architektur- und Betriebsentscheidungen zu bewerten.
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

Alle in der Cloud gehosteten Ressourcen befinden sich in einer Zielzone. Für diese Zielzone gelten ggf. explizite Governance-, Sicherheits- und Betriebsanforderungen. Es kann sich dabei aber auch um ein ganz neues Abonnement ohne Unterstützung durch andere Teams handeln. In beiden Szenarien ist es wichtig, mit einer Zielzone zu beginnen, die von Anfang an auf die Governance- und Betriebsanforderungen ausgerichtet ist. Die Verwendung einer freigegebenen Zielzone hilft Ihrem Team dabei, Richtlinienverstöße bei der Entwicklung frühzeitig zu erkennen (und nicht erst, wenn die Lösung in der Produktionsumgebung veröffentlicht wird). Eine frühzeitige Erkennung trägt dazu bei, Hindernisse zu beseitigen, und gibt dem Einführungs- und dem Governanceteam genügend Zeit für die Implementierung von Änderungen.

**Ziele:**

- Stellen Sie in der Anfangsphase einer Innovation eine erste Zielzone für erste Experimente mit geringem Risiko bereit.
- Entwickeln Sie einen Plan für die Umgestaltung mit dem Cloudkompetenzzentrum oder der zentralen IT-Abteilung, um sicherzustellen, dass er mit Governance-, Sicherheits- und Betriebsaspekten in Einklang steht.
- Zeitachsenrisiken:
  - Governance-, Betriebs- und Sicherheitsanforderungen für die ersten zehn Workloads können diesen Prozess verlangsamen. Die eigentliche Umgestaltung der ersten Zielzone und der nachfolgenden Zielzonen dauert länger, sollte aber parallel zu den Migrationsmaßnahmen erfolgen.

**Hinweis zur Erreichung der Ziele:**

- [Auswählen einer Zielzone](../ready/landing-zone/first-landing-zone.md): Verwenden Sie diesen Artikel, um den richtigen Ansatz für die Bereitstellung einer Zielzone basierend auf Ihrem Einführungsmuster zu ermitteln. Stellen Sie dann diese standardisierte Codebasis bereit.
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

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudkompetenzzentrum <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="value-statement"></a>Wertaussage

Die in diesem Leitfaden beschriebenen Schritte helfen Ihnen und Ihren Teams dabei, innovative Lösungen in der Cloud zu erstellen, die zur Wertschöpfung für das Unternehmen beitragen und sich durch eine angemessene Governance sowie durch eine durchdachte Architektur auszeichnen.

## <a name="next-steps"></a>Nächste Schritte

Das Cloud Adoption Framework ist eine Lebenszykluslösung. Es kann Ihnen dabei helfen, eine Innovationsjourney zu beginnen. Es kann Ihnen aber auch helfen, die Reife der Teams, die die Innovationsbemühungen unterstützen, zu fördern. Die folgenden Teams können die nächsten Schritte ausführen, um ihre Anstrengungen noch weiter zu optimieren. Diese parallelen Prozesse sind nicht linear und sollten nicht als Hindernisse betrachtet werden. Stattdessen handelt es sich jeweils um einen parallelen Wertstrom, der dazu beiträgt, die allgemeine Bereitschaft Ihres Unternehmens für die Cloud zu verbessern.

| Team | Nächste Iteration |
|---|---|
| Cloudeinführungsteam&nbsp;&nbsp; | [Prozessverbesserungen](../innovate/considerations/index.md) bieten Einblicke in die Ansätze zur Bereitstellung von Innovationen, die für Kunden relevant sind und die Einführung attraktiv machen. |
| Cloudstrategieteam&nbsp;&nbsp; | Die [Strategiemethodik](../strategy/index.md) und die [Planungsmethodik](../plan/index.md) sind iterative Prozesse, die sich mit dem Einführungsplan weiterentwickeln. Kehren Sie zu diesen Übersichtsseiten zurück, und führen Sie Ihre geschäftlichen und technischen Strategien weiter aus. |
| Cloudplattformteam&nbsp;&nbsp; | Kehren Sie zur [Bereitschaftsmethodik](../ready/index.md) zurück, um die gesamte Cloudplattform, die die Migration oder andere Einführungsmaßnahmen unterstützt, weiter voranzutreiben. |
| Cloudgovernanceteam&nbsp;&nbsp; | Verwenden Sie die [Governancemethodik](../govern/index.md), um Governanceprozesse, -richtlinien und -disziplinen weiter zu verbessern. |
| Cloudbetriebsteam&nbsp;&nbsp; | Verwenden Sie die [Verwaltungsmethodik](../manage/index.md), um umfassendere Vorgänge in Azure bereitzustellen. |
