---
title: Einrichten von Iterationen und Freigabeplänen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einrichten von Iterationen und Freigabeplänen
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 0dbef36d3909f11c1616d2e44c63227959c4ff56
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839176"
---
# <a name="establish-iterations-and-release-plans"></a>Einrichten von Iterationen und Freigabeplänen

Flexible und andere iterative Methodiken basieren auf den Konzepten von Iterationen und Freigaben. Dieser Artikel beschreibt die Zuordnung von Iterationen und Freigaben während der Planung. Diese Zuweisungen steuern die Sichtbarkeit der Zeitachse, um Gespräche zwischen Mitgliedern des Cloudtstrategieteams zu erleichtern. Darüber hinaus werden technische Aufgaben so ausgerichtet, dass das Cloudeinführungsteam die laufende Implementierung verwalten kann.

## <a name="establish-iterations"></a>Einrichten von Iterationen

In einem iterativen Ansatz zur technischen Implementierung planen Sie technische Aktivitäten rund um wiederkehrende Zeitblöcke. Iterationen werden tendenziell in Blöcken von ein bis sechs Wochen Dauer durchgeführt. Der Konsens legt nahe, dass die durchschnittliche Iterationsdauer für die meisten Cloudeinführungsteams zwei Wochen beträgt. Die Wahl der Iterationsdauer hängt jedoch von der Art der technischen Aktivität, dem administrativen Aufwand und der Präferenz des Teams ab.

Um die Aktivitäten an einer Zeitachse auszurichten, sollte eine Reihe von Iterationen für die nächsten 6 bis 12 Monate definiert werden.

## <a name="understand-velocity"></a>Grundlegendes zur Geschwindigkeit

Die Ausrichtung der Aktivitäten an Iterationen und Freigaben erfordert grundlegende Kenntnisse über die Geschwindigkeit. Die Geschwindigkeit ist die Menge an Arbeit, die in einer bestimmten Iteration abgeschlossen werden kann. In der frühen Planungsphase wird die Geschwindigkeit geschätzt. Nach mehreren Iterationen wird die Geschwindigkeit ein äußerst nützlicher Indikator für die Festlegungen, die das Team zuverlässig treffen kann.

Sie können die Geschwindigkeit in abstrakten Begriffen wie Story Points messen. Sie können sie auch in handfesteren Begriffen wie Stunden messen. Für die meisten iterativen Frameworks empfiehlt sich die Verwendung abstrakter Messungen, um Präzisions- und Wahrnehmungsprobleme zu vermeiden. Die Beispiele in diesem Artikel stellen die Geschwindigkeit in Stunden pro Sprint dar. Durch diese Darstellung lässt sich das Thema universeller verstehen.

**Beispiel:** Ein fünf Personen starkes Cloudeinführungsteam hat sich für Zwei-Wochen-Sprints entschieden. Aufgrund aktueller Verpflichtungen wie Besprechungen und die Unterstützung anderer Prozesse kann jedes der Teammitglieder konsistent 20 Stunden pro Woche zur Einführung beitragen. Für dieses Team beträgt die Schätzung der anfänglichen Geschwindigkeit 100 Stunden pro Sprint.

## <a name="iteration-planning"></a>Planung der Iteration

Zunächst planen Sie Iterationen, indem die technischen Aufgaben auf der Grundlage des priorisierten Rückstands bewertet werden. Cloudeinführungsteams schätzen den Aufwand zum Ausführen verschiedener Aufgaben. Diese Aufgaben werden dann der ersten verfügbaren Iteration zugewiesen.

Während der Iterationsplanung validieren und verfeinern die Cloudeinführungsteams die Schätzungen. Dies erfolgt so lange, bis alle verfügbaren Geschwindigkeiten auf bestimmte Aufgaben abgestimmt sind. Dieser Prozess wird für die einzelnen priorisierten Workloads fortgesetzt, bis der gesamte Aufwand an einer prognostizierten Iteration ausgerichtet ist.

In diesem Prozess überprüft das Team die Aufgaben, die dem nächsten Sprint zugewiesen werden. Das Team aktualisiert seine Schätzungen aufgrund der Gespräche des Teams über die einzelnen Aufgaben. Dann fügt das Team jede geschätzte Aufgabe dem nächsten Sprint hinzu, bis die verfügbare Geschwindigkeit erreicht ist. Schließlich schätzt das Team zusätzliche Aufgaben ab und fügt Sie der nächsten Iteration hinzu. Das Team führt diese Schritte aus, bis die Geschwindigkeit dieser Iteration ebenfalls erschöpft ist.

Der vorherige Prozess wird fortgesetzt, bis alle Aufgaben einer Iteration zugewiesen sind.

**Beispiel:** Wir bauen nun auf dem vorherigen Beispiel auf. Angenommen, jede Workloadmigration erfordert 40 Aufgaben. Nehmen wir ferner an, dass Sie für die Dauer jeder Aufgabe einen Mittelwert von einer Stunde abschätzen. Die kombinierte Schätzung entspricht etwa 40 Stunden pro Workloadmigration. Wenn diese Schätzungen über alle 10 der priorisierten Workloads hinweg konsistent bleiben, erfordern diese Workloads 400 Stunden Aufwand.

Die im vorherigen Beispiel definierte Geschwindigkeit legt nahe, dass die Migration der ersten 10 Workloads vier Iterationen dauern wird, was zwei Monaten Kalenderzeit entspricht. Die erste Iteration besteht aus 100 Aufgaben, die zur Migration von zwei Workloads führen. In der nächsten Iteration resultiert eine ähnliche Sammlung von 100 Aufgaben zur Migration von drei Workloads.

> [!WARNING]
> Die vorherige Anzahl von Aufgaben und Schätzungen wird ausschließlich als reine Beispiele verwendet. Technische Aufgaben sind selten derart konsistent. Sie sollten dieses Beispiel nicht als repräsentativ für die Zeit verstehen, die für die Migration eines Workloads benötigt wird.

## <a name="release-planning"></a>Releaseplanung

Im Rahmen einer Cloudeinführung ist eine Freigabe definiert als eine Sammlung von Ergebnissen, die genügend Geschäftswert erzeugen, um das Risiko einer Störung der Geschäftsprozesse zu rechtfertigen.

Die Freigabe von workloadbezogenen Änderungen in einer Produktionsumgebung führt zu einer Änderung der Geschäftsprozesse. Im Idealfall sind diese Änderungen nahtlos und der Wert der Änderung kommt dem Unternehmen ohne wesentliche Störungen des Betriebs zugute. Das Risiko von Unterbrechungen des Geschäftsbetriebs ist jedoch bei jeder Änderung gegeben und sollte nicht auf die leichte Schulter genommen werden.

Um sicherzustellen, dass eine Änderung durch ihre potenzielle Rendite gerechtfertigt ist, sollte das Cloudstrategieteam an der Freigabeplanung teilnehmen. Sobald die Aufgaben an Sprints ausgerichtet sind, kann das Team grob festlegen, wann jeder Workload für die Produktionsfreigabe bereit sein wird. Das Cloudstrategieteam würde das Timing jeder Freigabe überprüfen. Das Team würde dann den Wendepunkt zwischen Risiko und Geschäftswert identifizieren.

**Beispiel:** In Fortsetzung des vorherigen Beispiels hat das Cloudstrategieteam den Iterationsplan überprüft. Die Überprüfung hat zwei Freigabepunkte identifiziert. Während der zweiten Iteration sind insgesamt fünf Workloads zur Migration bereit. Diese fünf Workloads bieten einen erheblichen Geschäftswert und lösen die erste Freigabe aus. Die nächste Freigabe steht zwei Iterationen später an, wenn die nächsten fünf Workloads zur Freigabe bereit sind.

## <a name="assign-iteration-paths-and-tags"></a>Zuweisen von Iterationspfaden und Tags

Für Kunden, die Cloudeinführungspläne in Azure DevOps verwalten, werden die vorherigen Prozesse durch die Zuweisung eines Iterationspfads zu jeder Aufgabe und User Story widergespiegelt. Wir empfehlen außerdem, jeden Workload mit einer bestimmten Freigabe zu markieren. Diese Markierung und Zuweisung bilden die Eingabe für das automatische Füllen von Zeitachsenberichten.

## <a name="next-steps"></a>Nächste Schritte

[Schätzen Sie Zeitachsen](./timelines.md), um Erwartungen ordnungsgemäß zu kommunizieren.

> [!div class="nextstepaction"]
> [Schätzen von Zeitachsen](./timelines.md)
