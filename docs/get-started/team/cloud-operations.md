---
title: 'Erste Schritte: Aufbauen eines Cloudbetriebsteams'
description: Anhand dieses Leitfadens kann ein Cloudbetriebsteam den Projektumfang sowie die Ziele und Funktionen nachvollziehen, für die das Team verantwortlich ist.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 4d1ecbe31f7469cb992ab7e983a9ff4a34ef437f
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884061"
---
# <a name="get-started-build-a-cloud-operations-team"></a>Erste Schritte: Aufbauen eines Cloudbetriebsteams

Ein Betriebsteam konzentriert sich auf die Überwachung, Reparatur und Problembehandlung im Zusammenhang mit herkömmlichen IT-Vorgängen und -Ressourcen. In der Cloud werden viele dieser Investitionskosten und Betriebsaktivitäten auf den Cloudanbieter übertragen, was es der IT-Abteilung ermöglicht, sich weiterzuentwickeln und einen erheblichen Mehrwert zu schaffen.

![Erste Schritte für den Aufbau eines Cloudbetriebsteams](../../_images/get-started/operations-team-map.png)

## <a name="step-1-determine-whether-a-cloud-operations-team-is-needed"></a>Schritt 1: Ermitteln, ob ein Cloudbetriebsteam benötigt wird

Vor der Veröffentlichung von Workloads muss zunächst eine Einigung hinsichtlich der Zuständigkeit für die Bereitstellung von [Cloudbetriebsfunktionen](../../organize/cloud-operations.md) erzielt werden. Bei manchen Portfolios sind möglicherweise weiterhin das DevOps- und das Cloudeinführungsteam für operative Aufgaben zuständig. In anderen Fällen werden laufende operative Aufgaben unter Umständen von einem verwalteten Dienstanbieter mit Cloudbetriebserfahrung übernommen.

Sollten keine DevOps- oder Dienstanbietervereinbarungen für den Betrieb vorliegen, ist davon auszugehen, dass sich jemand aus der IT-Abteilung um laufende operative Aufgaben im Zusammenhang mit der Verwaltung von Produktionsworkloads kümmern muss.

**Ziele:**

- Ermitteln, ob ein Cloudbetriebsteam benötigt wird.
- Zuordnen übergreifender Zuständigkeiten für Teams, indem eine sogenannte RACI-Matrix entwickelt und damit bestimmt wird, welche Teams *verantwortlich sind (responsible), rechenschaftspflichtig sind (accountable), konsultiert werden (consulted) und zu informieren sind (informed)* . Dokumentieren der Entscheidung und der verantwortlichen Personen in der [RACI-Vorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx) im Arbeitsblatt `Org Alignment`.

**Hinweis zur Erreichung der Ziele:**

- [Cloudbetriebsfunktionen](../../organize/cloud-operations.md) sind unter Umständen bereits auf mehrere Einzelpersonen oder Teams verteilt. Entscheiden Sie, ob ein Cloudbetriebsteam erforderlich ist. Produktionsworkloads sind immer mit einem gewissen Betriebsaufwand verbunden.
- Falls die langfristige Cloudeinführungsstrategie des Unternehmens über eine Zielzone in einer Cloudumgebung bereitgestellt werden kann, ist der Governance- und Betriebsaufwand ggf. so gering, dass eine einzelne Person bzw. ein einzelnes Team ausreicht. Dieses Team wird dann wahrscheinlich nicht als Cloudbetriebsteam bezeichnet, da es verschiedene Aufgaben erfüllt. Für diese Einzelperson oder dieses Team können Sie mithilfe der folgenden Anleitungen sicherstellen, dass diese wichtige Betriebsfunktion bereitgestellt werden kann.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam <li> Cloudgovernanceteam |

## <a name="step-2-align-with-other-teams"></a>Schritt 2: Abstimmen mit anderen Teams

Operative Zuständigkeiten für alle Workloads im Produktionsportfolio gehen auf das Cloudbetriebsteam über. Diese Zuständigkeiten können sich abhängig von den Erwartungen und den Verpflichtungen, die vom Team gegenüber den Unternehmensbeteiligten eingegangen wurden, von Workload zu Workload unterscheiden. Die Architekturentscheidungen migrations- und innovationsorientierter Cloudeinführungsteams besitzen auch Einfluss auf betriebsbezogene Zusagen des Teams.

Bevor das Cloudbetriebsteam laufende Betriebspraktiken implementiert, ist es wichtig, dass es sich mit anderen Teams abstimmt. Das Team sollte sich mit anderen in der RACI-Vorlage angegebenen Teams absprechen, um für Einigkeit bei wichtigen Themen wie Sicherheit, Kosten, Leistung, Governance und Bereitstellung zu sorgen. Die Schritte 4 und 5 können diese Abstimmung vereinfachen.

**Ziele:**

- Besprechen des aktuellen Zustands der Implementierung und der Pläne zur laufenden Einführung mit jedem Team.

**Hinweis zur Erreichung der Ziele:**

- Sehen Sie sich gemeinsam mit Mitgliedern des Cloudstrategieteams die [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) Ihres Unternehmens an, um sich über Beweggründe des Teams und Metriken sowie über die Strategie zu informieren.
- Sehen Sie sich gemeinsam mit Mitgliedern des Cloudeinführungsteams den [Cloudeinführungsplan](../../plan/template.md) Ihres Unternehmens an, um sich mit dem Zeitplan und den Prioritäten vertraut zu machen.
- Beginnen Sie mit der Ausarbeitung der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx), um die betriebsbezogenen Anforderungen und Verpflichtungen des Teams für das Unternehmen nachzuvollziehen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-establish-a-cadence-with-other-teams"></a>Schritt 3: Festlegen eines gemeinsamen Rhythmus mit anderen Teams

Die Cloudeinführung erfolgt normalerweise in mehreren Wellen bzw. Releases. Ein regelmäßiger, auf diese Releases abgestimmter Rhythmus ermöglicht es dem Cloudbetriebsteam, sich auf Übergaben vorzubereiten, die jeweils am Ende der nächsten Welle anstehen. Durch die Abstimmung mit den Strategie-, Einführungs- und Governanceteams während der Planungs- und Prüfungsphase kann das Betriebsteam zukünftigen betrieblichen Anforderungen stets einen Schritt voraus sein.

**Ziele:**

- Etablieren eines gemeinsamen Rhythmus mit den unterstützenden Teams. Stimmen Sie diesen Rhythmus nach Möglichkeit auf die Release- und Planungszyklen ab.
- Etablieren Sie direkt mit dem Cloudstrategieteam (oder mit einzelnen Teammitgliedern) einen separaten Rhythmus für die Überprüfung betrieblicher Anforderungen im Zusammenhang mit der nächsten Welle der Einführung.

**Hinweis zur Erreichung der Ziele:**

- Weitere Anleitungen zur Häufigkeit von Besprechungen finden Sie im Abschnitt „Zielvorgaben“ unter [Cloudbetriebsfunktionen](../../organize/cloud-operations.md#deliverables).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudbetriebsteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudgovernanceteam |

## <a name="step-4-review-the-methodology"></a>Schritt 4: Überprüfen der Methodik

Um eine Zukunftsvision für die Betriebsverwaltung und einen Arbeitsansatz zur Verwirklichung dieser Vision zu entwickeln, sollten Sie sich die Verwaltungsmethodik des Cloud Adoption Framework ansehen.

**Ziele:**

- Verschaffen Sie sich einen Überblick über die Methodik, den Ansatz und die Implementierung für die Verwaltungsmethodik.

**Hinweis zur Erreichung der Ziele:**

- Sehen Sie sich die [Verwaltungsmethodik des Cloud Adoption Framework ](../../manage/index.md) an.

**Verantwortliches Team:**

- Das Cloudbetriebsteam ist für die Vision und den Ansatz im Zusammenhang mit der Betriebsverwaltung verantwortlich.

## <a name="step-5-implement-the-operations-baseline"></a>Schritt 5: Implementieren der Betriebsbaseline

Falls in Ihren Cloudumgebungen noch keine Verfahren für den Betrieb bereitgestellt wurden, beginnen Sie mit der Betriebsbaseline. Diese Baseline dient zur Implementierung cloudnativer No-Ops-/Low-Ops-Verfahren, um einen grundlegenden Schutz für den Betrieb zu gewährleisten.

**Ziele:**

- Stellen Sie die grundlegenden Azure-Serververwaltungskonfigurationen bereit, die für den Betrieb der Umgebung während der nächsten Einführungswellen benötigt werden.

**Hinweis zur Erreichung der Ziele:**

- Implementieren Sie die Konfiguration der [Betriebsbaseline](../../manage/azure-server-management/index.md).

**Verantwortliches Team:**

- Das Cloudbetriebsteam ist für die Implementierung der Betriebsbaseline verantwortlich.

## <a name="step-6-align-business-commitments"></a>Schritt 6: Ausrichten geschäftlicher Zusagen

Überprüfen Sie Zusagen der Betriebsbaseline des Teams für Unternehmensbeteiligte. Auf der Grundlage dieser Baseline lassen sich die allgemeinen Anforderungen für die Mehrzahl der Workloads bewerten. Darüber hinaus ermöglicht der Prozess Ihnen die Identifizierung von Beteiligten für verschiedene Workloads sowie die Dokumentation ihrer aktuellen betrieblichen Erwartungen.

**Ziele:**

- Dokumentieren der Erwartungen von Unternehmensbeteiligten.
- Ermitteln Sie, ob für bestimmte Workloads oder Plattformen erweiterte Vorgänge erforderlich sind.

**Hinweis zur Erreichung der Ziele:**

- Sorgen Sie für eine [geschäftliche Ausrichtung](../../manage/considerations/business-alignment.md) in der Cloud.
- Dokumentieren Sie die Portfolio- und Betriebserwartungen in der [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Verantwortliches Team:**

- Das Cloudbetriebsteam muss mit den geschäftlichen Erwartungen vertraut sein und ist für die kontinuierliche Ausrichtung auf diese Erwartungen verantwortlich.

## <a name="step-7-operations-maturity"></a>Schritt 7: Betriebsreife

Das Team kann durch kontinuierliche Betriebsoptimierungen die folgenden Ziele erreichen:

- Optimieren der Betriebsbaseline
- Verbessern des Plattformbetriebs
- Implementieren workloadspezifischer Vorgänge.

Mit der zunehmenden Umstellung von Workloads auf den Cloudbetrieb wird auch der Bedarf für operative Verbesserungen deutlicher.

**Ziele:**

- Verbessern der Betriebsreife, um die Erfüllung von Zusagen für Geschäftsbeteiligte zu unterstützen.

**Hinweis zur Erreichung der Ziele:**

- Ermitteln Sie die beste Option für die [Verwaltung erweiterter Vorgänge](../../manage/design-principles.md).

**Verantwortliches Team:**

- Das Cloudbetriebsteam ist für operative Verbesserungen und die Betriebsreife im Zeitverlauf verantwortlich.

## <a name="step-8-scale-operations-consistency-through-governance"></a>Schritt 8: Skalieren der Betriebskonsistenz mittels Governance

Mit zunehmender Reife der Betriebsplanung sollte sich das Team regelmäßig mit dem Cloudgovernanceteam abstimmen, um die Betriebsanforderungen auf das gesamte Portfolio anzuwenden.

**Ziele:**

- Unterstützen Sie das Cloudgovernanceteam bei der Implementierung neuer Anforderungen an die Ressourcenkonsistenz.

**Hinweis zur Erreichung der Ziele:**

- Weitere Informationen finden Sie im [Leitfaden zur Verbesserung der Ressourcenkonsistenz](../../govern/guides/complex/resource-consistency-improvement.md).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudbetriebsteam |

## <a name="step-9-adoption-handoffs"></a>Schritt 9: Übertragung von Aufgaben während der Einführung

Wenn neue Einführungsmaßnahmen abgeschlossen werden, überträgt das Cloudeinführungsteam betriebsbezogene Zuständigkeiten an das Cloudbetriebs- und das Cloudgovernanceteam. Das Team sollte die Ausrichtung auf Einführungsreleases beibehalten, um eine ordnungsgemäße Dokumentation sowie die Einhaltung von Richtlinien sicherzustellen und die Verantwortung für die Workloads zu übernehmen.

**Ziele:**

- Führen Sie eine regelmäßige Überprüfung der Aufgaben durch, die von Cloudeinführungsteams übertragen werden, und akzeptieren Sie sie.

**Hinweis zur Erreichung der Ziele:**

- Legen Sie einen Prozess für das [Durchführen des Onboardings für neue Workloads und Ressourcen](/azure/azure-resource-manager/custom-providers/concepts-resource-onboarding) fest.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteams | <li> Cloudgovernanceteam <li> Cloudbetriebsteam |

## <a name="whats-next"></a>Nächste Schritte

Da Einführung und Abläufe einer Skalierung unterliegen, ist es wichtig, bewährte Methoden für die Governance zu definieren und zu automatisieren, die vorhandene IT-Anforderungen erweitern. Der Aufbau eines CCoE-Teams (Cloud Center of Excellence, Cloudkompetenzzentrum) ist ein wichtiger Schritt hin zur Skalierung von Cloudeinführung, Cloudbetrieb und Cloudgovernance.

Weitere Informationen:

- [CCoE-Funktionen (Cloud Center of Excellence, Cloudkompetenzzentrum)](../../organize/cloud-center-of-excellence.md)
- [Antimuster in Unternehmen: Silos und Machtbereiche](../../organize/fiefdoms-silos.md)

Abstimmen von Verantwortlichkeiten in den Teams, indem eine teamübergreifende Matrix entwickelt wird, die die RACI-Parteien identifiziert. Herunterladen und Ändern der [RACI-Vorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx).
