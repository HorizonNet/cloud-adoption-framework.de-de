---
title: 'Erste Schritte: Aufstellen eines Cloudgovernanceteams'
description: Legen Sie für ein Governanceteam den Bereich, die Zielvorgaben und die Funktionen fest, um die erfolgreiche Durchführung von Maßnahmen für die Cloudgovernance sicherzustellen.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 346b4feabfbb7fefd8632ac4b3f5f81473815843
ms.sourcegitcommit: 12fa4597633ca8e04efbae7d0bd7526d3581618e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88661995"
---
# <a name="get-started-build-a-cloud-governance-team"></a>Erste Schritte: Aufstellen eines Cloudgovernanceteams

Mit einem Cloudgovernanceteam wird sichergestellt, dass Risiken bei der Cloudeinführung und die Risikotoleranz richtig ausgewertet und verwaltet werden. Das Team identifiziert Risiken, die vom Unternehmen nicht toleriert werden können, und wandelt sie in geltende Unternehmensrichtlinien um.

![Einstieg in die Aufstellung eines Cloudgovernanceteams](../../_images/get-started/governance-team-map.png)

## <a name="step-1-determine-whether-a-cloud-governance-team-is-needed"></a>Schritt 1: Ermitteln, ob ein Cloudgovernanceteam benötigt wird

Die offizielle Empfehlung für das Cloud Adoption Framework für Azure lautet, dass immer ein Cloudgovernanceteam aufgestellt werden sollte. Dieses Team ist unter Umständen anfänglich sehr klein. Unabhängig von seiner Größe erfüllt es eine wichtige Funktion. Falls kein Team benötigt wird, sollten die Aufgaben, die mit [Cloudgovernancefunktionen](../../organize/cloud-governance.md) verbunden sind, einer Gruppe oder Einzelperson in einem vorhandenen Einführungsteam übertragen werden.

**Ziele:**

- Ermitteln, ob ein Cloudgovernanceteam benötigt wird.
- Zuordnen übergreifender Zuständigkeiten für Teams, indem eine sogenannte RACI-Matrix entwickelt und damit bestimmt wird, welche Teams *verantwortlich sind (responsible), rechenschaftspflichtig sind (accountable), konsultiert werden (consulted) und zu informieren sind (informed)* . Dokumentieren der Entscheidung und der verantwortlichen Personen mithilfe der [RACI-Vorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx) im Arbeitsblatt `Org Alignment`.

**Hinweis zur Erreichung der Ziele:**

- Die [Cloudgovernancefunktionen](../../organize/cloud-governance.md) sind unter Umständen bereits auf mehrere Einzelpersonen oder Teams verteilt. Ein Team mit dem Titel „Cloudgovernanceteam“ ist nicht wichtig, aber die erforderlichen Funktionen sollten einer verantwortlichen Partei oder einem Team übertragen werden.
- Falls die langfristige Cloudeinführungsstrategie des Unternehmens über eine Zielzone in einer Cloudumgebung bereitgestellt werden kann, ist der Aufwand für die Governance- und Operationsmaßnahmen ggf. so gering, dass eine Person bzw. ein Team ausreicht. Es ist unwahrscheinlich, dass dieses Team als „Cloudgovernanceteam“ bezeichnet wird, da es zahlreiche Funktionen jenseits von Cloudgovernance erfüllt. Selbst bei diesem Team kann dieser Leitfaden zu den ersten Schritten beim Sicherstellen helfen, dass es diese wichtige Funktion der Governance bereitstellen kann.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam |

## <a name="step-2-align-with-other-teams"></a>Schritt 2: Ausrichten an anderen Teams

Das Governanceteam sorgt für die Konsistenz und die Einhaltung der allgemeinen Richtlinien. Diese Richtlinien sind das Ergebnis einer fortlaufenden Ausrichtung an anderen Teams.

Bevor es Richtlinien oder automatisierte Cloudgovernance festlegt, sollte das Cloudgovernanceteam mit anderen Teams zusammenarbeiten, die in der RACI-Vorlage identifiziert werden. Dadurch wird die Konzentration auf wichtige Themen (z. B. Sicherheit, Kosten, Leistung, Betrieb und Bereitstellung) sichergestellt. Die Schritte 4 und 5 können diese Abstimmung vereinfachen.

**Ziele:**

- Besprechen des aktuellen Zustands der Implementierung und der Pläne zur laufenden Einführung mit jedem Team.

**Hinweis zur Erreichung der Ziele:**

- Sehen Sie sich gemeinsam mit Mitgliedern des Cloudstrategieteams die [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) Ihres Unternehmens an, um sich über Beweggründe und Metriken sowie über die Strategie zu informieren.
- Sehen Sie sich gemeinsam mit Mitgliedern des Cloudeinführungsteams den [Cloudeinführungsplan](../../plan/template.md) Ihres Unternehmens an, um sich mit dem Zeitplan und den Prioritäten vertraut zu machen.
- Sehen Sie sich die [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) des Operations-Teams an, um sich über die betriebsbezogenen Anforderungen und Verpflichtungen zu informieren, die für das Unternehmen gelten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-establish-a-cadence-with-other-teams"></a>Schritt 3: Festlegen eines gemeinsamen Rhythmus mit anderen Teams

Die Cloudeinführung erfolgt normalerweise in mehreren Wellen bzw. Releases. Ein regelmäßiger Rhythmus, der an diesen Releases ausgerichtet ist, ermöglicht dem Cloudgovernanceteam eine Vorausschau und die Erkennung von Risiken, die mit der nächsten Welle verbunden sind. Indem das Governanceteam in der Planungs- und Prüfungsphase mit den Teams für die Bereiche Strategie, Einführung und Operations in Verbindung bleibt, kann es bevorstehende Risiken besser überblicken.

**Ziele:**

- Etablieren eines gemeinsamen Rhythmus mit den unterstützenden Teams. Stimmen Sie diesen Rhythmus nach Möglichkeit auf die Release- und Planungszyklen ab.
- Legen Sie einen separaten Rhythmus direkt mit dem Cloudstrategieteam (bzw. einzelnen Teammitgliedern) fest, nach dem die Risiken der nächsten Welle der Einführung überprüft werden, und ermitteln Sie die Toleranz des Teams in Bezug auf diese Risiken.

**Hinweis zur Erreichung der Ziele:**

- Weitere Informationen zur Besprechungshäufigkeit finden Sie unter [Cloudgovernancefunktionen](../../organize/cloud-governance.md#deliverable).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudbetriebsteam |

## <a name="step-4-review-the-methodology"></a>Schritt 4: Überprüfen der Methodik

Sehen Sie sich die Governancemethodik des Cloud Adoption Framework an, um die Bestimmung einer Zukunftsvision für Governance und die Auswahl eines funktionierenden Ansatzes zur Erreichung dieser Vision zu vereinfachen.

**Ziele:**

- Verschaffen Sie sich einen Überblick über die Methodik, den Ansatz und die Implementierung der Governance-Methodik.

**Hinweis zur Erreichung der Zielvorgaben:**

- Informieren Sie sich über die [Cloudgovernance-Methodik](../../govern/methodology.md).

**Verantwortliches Team:**

- Das Cloudgovernanceteam hat die Aufgabe, eine Governancevision und einen entsprechenden Ansatz zur Erreichung festzulegen.

## <a name="step-5-complete-the-governance-benchmark"></a>Schritt 5: Durchführen der Governance-Benchmarkbewertung

Governance ist ein weites Feld. Eine kurze Bewertung kann dem Team bei der Ermittlung eines Ausgangspunkts helfen.

**Ziele:**

- Führen Sie die Governance-Benchmarkbewertung basierend auf Gesprächen mit verschiedenen Projektbeteiligten durch. Oder bitten Sie andere Teams, die Bewertung eigenständig abzuschließen.

**Hinweis zur Erreichung der Ziele:**

- Verwenden Sie den [Governancebenchmark](../../govern/benchmark.md), um Ihre Governanceanforderungen und -prioritäten zu bewerten.

**Verantwortliches Team:**

- Das Cloudgovernanceteam sollte die Lücken erkennen, die mit dem Governance-Benchmarktool ermittelt wurden, und dann entsprechende Governancelösungen bereitstellen, mit denen diese Lücken geschlossen werden können.

## <a name="step-6-implement-the-initial-governance-best-practice-and-configuration"></a>Schritt 6: Implementieren der anfänglichen bewährten Methoden und der Konfiguration für Governance

Die Governance-Methodik umfasst zwei Ansätze zur Schaffung einer Governancegrundlage als Ausgangsbasis. Sehen Sie sich die beiden Ansätze an, und implementieren Sie den Ansatz, der Ihre Anforderungen am besten erfüllt.

**Ziele:**

- Stellen Sie die grundlegenden Governancetools und Organisationskonfigurationen bereit, die für die Umgebung während der nächsten Wellen der Einführung erforderlich sind.

**Hinweis zur Erreichung der Ziele:**

- Eine Anleitung zur Konfiguration und Implementierung finden Sie unter [Einrichten einer ersten Grundlage für Cloudgovernance](../../govern/initial-foundation.md).

**Verantwortliches Team:**

- Das Cloudgovernanceteam ist dafür verantwortlich, die bewährten Governancemethoden zu überprüfen und zu implementieren und eine erste Grundlage für Governance zu schaffen.

## <a name="step-7-continuously-improve-governance-maturity"></a>Schritt 7: Fortlaufendes Verbessern des Entwicklungsstands in Bezug auf Governance

Die Governanceanforderungen nehmen zu, wenn weitere Cloudeinführungsmaßnahmen abgeschlossen werden. Stellen Sie die Ausrichtung am Plan für die laufende Einführung sicher, um dafür zu sorgen, dass beim gewählten Governanceansatz die richtigen Ebenen und Kontrollen eingehalten werden.

**Ziele:**

- Implementieren Sie Governanceverbesserungen als Schutz vor sich ändernden Risiken und Governanceanforderungen.

**Hinweis zur Erreichung der Ziele:**

- Implementieren Sie [erweiterte Governanceszenarien](../../govern/foundation-improvements.md), um die anfängliche Governancegrundlage zu verbessern.

**Verantwortliches Team:**

- Das Cloudgovernanceteam ist für die Ausrichtung an den Plänen für die laufende Einführung verantwortlich.

## <a name="step-8-evaluate-landing-zone-changes"></a>Schritt 8: Auswerten von Änderungen der Zielzone

Wenn Zielzonen bereitgestellt und erweitert werden, können sich neue Risiken oder Governanceverletzungen ergeben. Überprüfen Sie die Konfigurationen von Zielzonen regelmäßig, um alle Abweichungen von der Richtlinie zu ermitteln, die mit den nativen Governancetools in der Cloud nicht erkannt werden. Stellen Sie sicher, dass für jede Zielzonenbereitstellung die Richtlinien für die entsprechenden Governancevorgaben eingehalten werden.

**Ziele:**

- Unterstützen Sie das Cloudplattformteam bei der Entwicklung von Verbesserungen der Zielzone, bei denen die Governancerichtlinien eingehalten werden müssen.

**Hinweis zur Erreichung der Ziele:**

- Verbessern der [Governance von Zielzonen](../../ready/considerations/landing-zone-governance.md).

**Verantwortliches Team:**

- Das Cloudgovernanceteam sollte sicherstellen, dass bei jeder Zielzonenbereitstellung die Governancerichtlinien eingehalten werden.

## <a name="step-9-adoption-handoffs"></a>Schritt 9: Übertragung von Aufgaben während der Einführung

Wenn neue Einführungsmaßnahmen abgeschlossen werden, überträgt das Cloudeinführungsteam betriebsbezogene Zuständigkeiten an das Cloudbetriebsteam und an Cloudgovernanceteams. Behalten Sie die Ausrichtung auf die Häufigkeit von Einführungsreleases bei, um eine ordnungsgemäße Dokumentation sowie die Einhaltung von Richtlinien sicherzustellen und dem Team dabei zu helfen, die Verantwortung für die Workloads zu übernehmen.

**Ziele:**

- Führen Sie eine regelmäßige Überprüfung der Aufgaben durch, die von anderen Cloudeinführungsteams übertragen werden, und akzeptieren Sie sie.

**Hinweis zur Erreichung der Ziele:**

- Legen Sie einen Prozess für das [Durchführen des Onboardings für neue Workloads und Ressourcen](/azure/azure-resource-manager/custom-providers/concepts-resource-onboarding) fest.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteams | <li> Cloudgovernanceteam <li> Cloudbetriebsteam |

## <a name="whats-next"></a>Nächste Schritte

Jedes Unternehmen ist einzigartig, und dies gilt auch für die jeweiligen Governanceanforderungen. Wählen Sie die Entwicklungsstufe, die zu Ihrer Organisation passt, und verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) als Anleitung für die Methoden, Prozesse und Tools, um diese Stufe zu erreichen.

Während der Weiterentwicklung der Cloudgovernance werden Teams in die Lage versetzt, die Einführung der Cloud schneller zu betreiben. Wenn weiter kontinuierlich an der Cloudeinführung gearbeitet wird, werden in der Regel auch die anderen IT-Abläufe weiterentwickelt. Stellen Sie entweder ein [Cloudbetriebsteam](./cloud-operations.md) auf, oder sprechen Sie sich mit Ihrem Cloudbetriebsteam ab, um sicherzustellen, dass Governance Teil der Entwicklungsmaßnahmen für den Operationsbereich ist.
