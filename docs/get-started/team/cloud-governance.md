---
title: 'Erste Schritte: Aufstellen eines Cloudgovernanceteams'
description: Legen Sie für ein Governanceteam den Bereich, die Zielvorgaben und die Funktionen fest, um die erfolgreiche Durchführung von Maßnahmen für die Cloudgovernance sicherzustellen.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 04/04/2020
ms.openlocfilehash: ac6696cf71d43fb8cae3ec5d7e8fe455cf18d989
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400181"
---
# <a name="get-started-build-a-cloud-governance-team"></a>Erste Schritte: Aufstellen eines Cloudgovernanceteams

Mit einem Cloudgovernanceteam wird sichergestellt, dass Risiken und die Risikotoleranz richtig ausgewertet und verwaltet werden. Dieses Team sorgt dafür, dass Risiken, die für das Unternehmen nicht tolerierbar sind, richtig identifiziert werden. Die Mitarbeiter dieses Teams steuern Risiken mithilfe von Unternehmensrichtlinien.

![Einstieg in die Aufstellung eines Cloudgovernanceteams](../../_images/get-started/governance-team-map.png)

## <a name="step-1-determine-if-a-cloud-governance-team-is-needed"></a>Schritt 1: Ermitteln, ob ein Cloudgovernanceteam benötigt wird

Die offizielle Empfehlung für das Cloud Adoption Framework lautet, dass immer ein Cloudgovernanceteam aufgestellt werden sollte. Dieses Team ist unter Umständen anfänglich sehr klein. Unabhängig von seiner Größe erfüllt es aber eine wichtige Funktion. Falls kein Team benötigt wird, sollten die Aufgaben, die mit [Cloudgovernancefunktionen](../../organize/cloud-governance.md) verbunden sind, einer Gruppe oder Einzelperson übertragen werden.

**Zielvorgaben:**

- Ermitteln Sie, ob Sie ein Cloudgovernanceteam benötigen.
- Dokumentieren Sie die Entscheidung und die verantwortlichen Personen in der [RACI-Vorlage](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) auf der Registerkarte für die organisatorische Ausrichtung.

**Hinweis zur Erreichung der Zielvorgaben:**

- Die [Cloudgovernancefunktionen](../../organize/cloud-governance.md) sind unter Umständen bereits auf mehrere Einzelpersonen oder Teams verteilt. Es ist nicht entscheidend, dass ein Team mit dem Namen „Cloudgovernanceteam“ vorhanden ist. Die erforderlichen Aufgaben sollten aber einer verantwortlichen Person oder einem Team übertragen werden.
- Falls die langfristige Cloudeinführungsstrategie des Unternehmens über eine Zielzone in einer Cloudumgebung bereitgestellt werden kann, ist der Aufwand für die Governance- und Operations-Maßnahmen ggf. so gering, dass eine Person bzw. ein Team ausreicht. Der Name dieses Teams enthält dann vermutlich nicht die Bezeichnung „Cloudgovernance“, weil es darüber hinaus noch viele weitere Aufgaben erfüllt. Auch für ein Team dieser Art kann mit dem folgenden Leitfaden zum Einstieg aber sichergestellt werden, dass das Team diese wichtige Governanceaufgabe erfüllen kann.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudstrategieteam | <li> Cloudeinführungsteam |

## <a name="step-2-align-with-other-teams"></a>Schritt 2: Ausrichten an anderen Teams

Das Governanceteam sorgt für die Konsistenz und die Einhaltung der allgemeinen Richtlinien. Diese Richtlinien sind das Ergebnis einer fortlaufenden Ausrichtung an anderen Teams. Vor dem Festlegen von Richtlinien oder von automatisierten Maßnahmen für Cloudgovernance sollte sich das Cloudgovernanceteam mit anderen Teams absprechen, die in der RACI-Vorlage angegeben sind, um die gemeinsame Ausrichtung in Bezug auf kritische Themen sicherzustellen, z. B. Sicherheit, Kosten, Leistung, Betrieb und Bereitstellung. Die Schritte 4 und 5 können diese Ausrichtung vereinfachen.

**Ziele:**

- Besprechen Sie den aktuellen Zustand der Implementierung und die Pläne zur laufenden Einführung mit jedem Team.

**Hinweis zur Erreichung der Ziele:**

- Sehen Sie sich gemeinsam mit Mitgliedern des Cloudstrategieteams die [Strategie- und Planungsvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) Ihres Unternehmens an, um sich über Beweggründe und Metriken sowie über die Strategie zu informieren.
- Sehen Sie sich die [Vorlage für den Cloudeinführungsplan](../../plan/template.md) Ihres Unternehmens zusammen mit Mitgliedern des Cloudeinführungsteams an, um sich mit den Zeitachsen und Prioritäten vertraut zu machen.
- Sehen Sie sich die [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) des Operations-Teams an, um sich über die betriebsbezogenen Anforderungen und Verpflichtungen zu informieren, die für das Unternehmen gelten.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-3-establish-a-cadence-with-other-teams"></a>Schritt 3: Festlegen eines gemeinsamen Rhythmus mit anderen Teams

Die Umstellung auf die Cloud erfolgt normalerweise in mehreren Wellen (bzw. Releases). Ein regelmäßiger Rhythmus, der an diesen Releases ausgerichtet ist, ermöglicht dem Cloudgovernanceteam eine Vorausschau und die Erkennung von Risiken, die mit der nächsten Welle verbunden sind. Indem das Governanceteam in der Planungs- und Prüfungsphase mit den Teams für die Bereiche Strategie, Einführung und Operations in Verbindung bleibt, kann es bevorstehende Risiken besser überblicken.

**Zielvorgaben:**

- Etablieren Sie einen gemeinsamen Rhythmus mit den einzelnen unterstützenden Teams. Richten Sie diesen Rhythmus nach Möglichkeit an den Release- und Planungszyklen aus.
- Legen Sie einen separaten Rhythmus direkt mit dem Cloudstrategieteam (bzw. einzelnen Teammitgliedern) fest, nach dem die Risiken der nächsten Welle der Einführung überprüft werden, und ermitteln Sie die Toleranz des Teams in Bezug auf diese Risiken.

**Hinweis zur Erreichung der Zielvorgaben:**

- Unter den [Cloudgovernancefunktionen](../../organize/cloud-governance.md#deliverable) finden Sie weitere Informationen zur Einhaltung von Rhythmen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudbetriebsteam |

## <a name="step-4-review-the-methodology"></a>Schritt 4: Überprüfen der Methodik

Sehen Sie sich die Governance-Methodik des Cloud Adoption Framework an, um die Bestimmung einer Zukunftsvision für Governance und die Auswahl eines funktionierenden Ansatzes zur Erreichung dieser Vision zu vereinfachen.

**Zielvorgaben:**

- Verschaffen Sie sich einen Überblick über die Methodik, den Ansatz und die Implementierung der Governance-Methodik.

**Hinweis zur Erreichung der Zielvorgaben:**

- Informieren Sie sich über die [Cloudgovernance-Methodik](../../govern/methodology.md).

**Verantwortliches Team:**

- Das Cloudgovernanceteam hat die Aufgabe, eine Governancevision und einen entsprechenden Ansatz zur Erreichung festzulegen.

## <a name="step-5-complete-the-governance-benchmark"></a>Schritt 5: Durchführen der Governance-Benchmarkbewertung

Governance ist ein weites Feld. Diese kurze Bewertung kann Ihnen bei der Ermittlung eines Ansatzpunkts helfen.

**Zielvorgaben:**

- Führen Sie die Governance-Benchmarkbewertung basierend auf Gesprächen mit verschiedenen Projektbeteiligten durch (oder bitten Sie andere Teams, die Bewertung selbst durchzuführen).

**Hinweis zur Erreichung der Zielvorgaben:**

- Bewerten Sie Ihre Governanceanforderungen und -prioritäten, indem Sie das [Governance-Benchmarktool](../../govern/benchmark.md) verwenden.

**Verantwortliches Team:**

- Das Cloudgovernanceteam sollte die Lücken erkennen, die mit dem Governance-Benchmarktool ermittelt wurden, und entsprechende Governancelösungen bereitstellen, mit denen diese Lücken geschlossen werden können.

## <a name="step-6-implement-the-initial-governance-best-practice-and-configuration"></a>Schritt 6: Implementieren der anfänglichen bewährten Methoden und der Konfiguration für Governance

Die Governance-Methodik umfasst zwei Ansätze zur Schaffung einer Governancegrundlage als Ausgangsbasis. Sehen Sie sich die beiden Ansätze an, und implementieren Sie den Ansatz, der Ihre Anforderungen am besten erfüllt.

**Zielvorgaben:**

- Stellen Sie die grundlegenden Governancetools und Organisationskonfigurationen bereit, die für die Umgebung während der nächsten Wellen der Einführung erforderlich sind.

**Hinweis zur Erreichung der Zielvorgaben:**

- Lesen Sie den Leitfaden zu den [ersten bewährten Methoden](../../govern/initial-foundation.md) in Bezug auf die Konfiguration und Implementierung.

**Verantwortliches Team:**

- Das Cloudgovernanceteam ist dafür verantwortlich, die bewährten Governancemethoden zu überprüfen und zu implementieren und eine erste Grundlage für Governance zu schaffen.

## <a name="step-7-continuously-improve-the-governance-maturity"></a>Schritt 7: Fortlaufendes Verbessern des Entwicklungsstands in Bezug auf Governance

Die Governanceanforderungen nehmen zu, wenn die Cloudeinführung weiter voranschreitet. Stellen Sie die Ausrichtung am Plan für die laufende Einführung sicher, um dafür zu sorgen, dass beim gewählten Governanceansatz die richtigen Ebenen und Kontrollen eingehalten werden.

**Zielvorgaben:**

- Implementieren Sie Governanceverbesserungen als Schutz vor sich ändernden Risiken und Governanceanforderungen.

**Hinweis zur Erreichung der Zielvorgaben:**

- Implementieren Sie [erweiterte Governanceszenarien](../../govern/foundation-improvements.md), um die anfängliche Governancegrundlage zu verbessern.

**Verantwortliches Team:**

- Das Cloudgovernanceteam ist für die Ausrichtung an den Plänen für die laufende Einführung verantwortlich.

## <a name="step-8-evaluate-landing-zone-changes"></a>Schritt 8: Auswerten von Änderungen der Zielzone

Wenn Zielzonen bereitgestellt und erweitert werden, können sich neue Risiken oder Governanceverletzungen ergeben. Überprüfen Sie die Konfigurationen von Zielzonen regelmäßig, um Abweichungen von der Richtlinie zu ermitteln, die mit den nativen Governancetools in der Cloud nicht erkannt werden. Stellen Sie sicher, dass für jede Zielzonenbereitstellung die Richtlinien für die entsprechenden Governancevorgaben eingehalten werden.

**Zielvorgaben:**

- Unterstützen Sie das Cloudplattformteam bei der Entwicklung von Verbesserungen der Zielzone, bei denen die Governancerichtlinien eingehalten werden.

**Hinweis zur Erreichung der Zielvorgaben:**

- Verbessern der [Governance von Zielzonen](../../ready/considerations/landing-zone-governance.md).

**Verantwortliches Team:**

- Das Cloudgovernanceteam sollte sicherstellen, dass bei jeder Zielzonenbereitstellung die Governancerichtlinien eingehalten werden.

## <a name="step-9-adoption-handoffs"></a>Schritt 9: Übertragung von Aufgaben während der Einführung

Wenn neue Einführungsmaßnahmen abgeschlossen werden, überträgt das Cloudeinführungsteam betriebsbezogene Zuständigkeiten an das Cloudbetriebsteam und an Cloudgovernanceteams. Behalten Sie die Ausrichtung auf Einführungsreleases bei, um eine ordnungsgemäße Dokumentation sowie die Einhaltung von Richtlinien sicherzustellen und die Verantwortung für die Workloads zu übernehmen.

**Ziele:**

- Führen Sie eine regelmäßige Überprüfung der Aufgaben durch, die von Cloudeinführungsteams übertragen werden, und akzeptieren Sie sie.

**Hinweis zur Erreichung der Ziele:**

- Legen Sie einen Prozess für das [Durchführen des Onboardings für neue Workloads und Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/custom-providers/concepts-resource-onboarding) fest.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteams | <li> Cloudgovernanceteam <li> Cloudbetriebsteam |

## <a name="whats-next"></a>Nächste Schritte

Jedes Unternehmen ist einzigartig, und dies gilt auch für die jeweiligen Governanceanforderungen. Wählen Sie die Entwicklungsstufe, die zu Ihrer Organisation passt, und verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) als Anleitung für die Methoden, Prozesse und Tools, um diese Stufe zu erreichen.

Während der Weiterentwicklung der Cloudgovernance werden Teams in die Lage versetzt, die Einführung der Cloud schneller zu betreiben. Wenn weiter kontinuierlich an der Cloudeinführung gearbeitet wird, werden in der Regel auch die anderen IT-Abläufe weiterentwickelt. Stellen Sie entweder ein [Cloudbetriebsteam](./cloud-operations.md) auf, oder sprechen Sie sich mit Ihrem Cloudbetriebsteam ab, um sicherzustellen, dass Governance Teil der Entwicklungsmaßnahmen für den Operations-Bereich ist.
