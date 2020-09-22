---
title: Arten von Höherstufungsmodellen
description: Es werden drei gängige Höherstufungsmodelle für die Cloudmigration beschrieben, und Sie erfahren, wie sich Ihre Modellwahl auf die Aktivitäten der Migrations- und Optimierungsprozesse auswirkt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 81e19ba4fd92aa6e3510593ef48aaa0b113a3a69
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602255"
---
# <a name="promotion-models-single-step-staged-or-flight"></a>Höherstufungsmodelle: „in einem Schritt“, „gestaffelt“ oder „Flight“

Die Workloadmigration wird oft als eine einzelne Aktivität erläutert. In der Praxis handelt es sich dabei um eine Sammlung kleinerer Aktivitäten, die die Verschiebung einer digitalen Ressource in die Cloud unterstützen. Eine der letzten Aktivitäten bei einer Migration ist die Höherstufung einer Ressource in die Produktion. Höherstufung ist der Punkt, an dem sich das Produktionssystem für Endbenutzer ändert. Dazu kann oft einfach das Netzwerkrouting geändert werden, wodurch Endbenutzer an die neue Produktionsressource weitergeleitet werden. Höherstufung ist auch der Punkt, an dem IT- oder Cloudvorgänge den Schwerpunkt betrieblicher Verwaltungsprozesse vom vorherigen Produktionssystem auf die neuen Produktionssysteme verlagern.

Es gibt mehrere Höherstufungsmodelle. In diesem Artikel werden drei der Modelle beschrieben, die bei Cloudmigrationen am häufigsten verwendet werden. Die Wahl eines Höherstufungsmodells ändert die Aktivitäten in den Migrations- und Optimierungsprozessen. Deshalb sollte die Entscheidung über das Höherstufungsmodell zu einem frühen Zeitpunkt in einem Release getroffen werden.

## <a name="impact-of-promotion-model-on-migrate-and-optimize-activities"></a>Auswirkungen des Höherstufungsmodells auf Migrations- und Optimierungsaktivitäten

In jedem der folgenden Höherstufungsmodelle repliziert und staffelt das ausgewählte Migrationstool die Ressourcen, aus denen eine Workload besteht. Nach dem Stagingprozess behandelt jedes Modell die Ressource etwas anders.

- **Höherstufung in einem Schritt.** Bei einem Höherstufungsmodell des Typs _in einem Schritt_ wird der Stagingprozess als Höherstufungsprozess verdoppelt. Nachdem alle Ressourcen gestaffelt wurden, wird der Datenverkehr für Endbenutzer umgeleitet, und aus Staging wird Produktion. In solch einem Fall ist Höherstufung ein Teil des Migrationsprozesses. Dies ist das schnellste Migrationsmodell. Allerdings erschwert dieser Ansatz die Integration stabiler Test- oder Optimierungsaktivitäten. Darüber hinaus wird bei diesem Modelltyp vorausgesetzt, dass das Migrationsteam Zugriff auf die Staging- und Produktionsumgebung hat, wodurch die Trennung von Aufgaben in einigen Umgebungen gefährdet ist.
  > [!NOTE]
  > Im Inhaltsverzeichnis für diese Website ist die Höherstufungsaktivität als Teil des Optimierungsprozesses aufgeführt. In einem Modell des Typs „ein Schritt“ erfolgt die Höherstufung während der Migrationsphase. Bei Verwendung dieses Modells sollten Rollen und Zuständigkeiten aktualisiert werden, um dies zu berücksichtigen.
- **Gestaffelt.** In einem _gestaffelten_ Höherstufungsmodell wird die Workload nach ihrer Staffelung als migriert betrachtet, aber noch nicht höhergestuft. Vor der Höherstufung durchläuft die migrierte Workload eine Reihe von Leistungstests, geschäftsbezogenen Tests und Optimierungsänderungen. Zu einem späteren Zeitpunkt wird sie dann in Verbindung mit einem Plan für geschäftsbezogene Tests höhergestuft. Dieser Ansatz verbessert das Kosten-/Leistungsverhältnis, während eine Geschäftsvalidierung einfacher zu erhalten ist.
- **Flight.** Im Höherstufungsmodell des Typs _Flight_ sind die Modelle des Typs „in einem Schritt“ und „gestaffelt“ kombiniert. In einem „Flight“-Modell werden die Ressourcen im Workload wie „Produktion nach dem Ziel im Stagingprozess“ behandelt. Nach einem verkürzten Zeitraum von automatisierten Tests wird der Produktionsdatenverkehr an die Workload weitergeleitet. Allerdings handelt es sich dabei um eine Teilmenge des Datenverkehrs. Dieser Datenverkehr dient als der erste Flight von Produktion und Tests. Vorausgesetzt, dass die Workload im Hinblick auf Feature und Leistung ausgeführt wird, wird zusätzlicher Datenverkehr migriert. Nachdem der gesamte Produktionsdatenverkehr auf die neuen Ressourcen verschoben wurde, wird die Workload als vollständig höhergestuft betrachtet.

Das ausgewählte Höherstufungsmodell wirkt sich auf die Abfolge der auszuführenden Aktivitäten aus. Außerdem wirkt es sich auf die Rollen und Zuständigkeiten des Cloudeinführungsteams aus. Es kann sich sogar auf die Zusammensetzung von einem oder mehreren Sprints auswirken.

## <a name="single-step-promotion"></a>Höherstufung „in einem Schritt“

Dieses Modell verwendet Migrationsautomatisierungstools zum Replizieren, Staffeln und Höherstufen von Ressourcen. Die Ressourcen werden in eine eigenständige Stagingumgebung repliziert, die durch das Migrationstool gesteuert wird. Nachdem alle Ressourcen repliziert wurden, kann das Tool einen automatisierten Prozess zum Höherstufen der Ressourcen in das ausgewählte Abonnement in einem einzigen Schritt ausführen. Während des Stagings repliziert das Tool die Ressource weiterhin und minimiert so einen Datenverlust zwischen den beiden Umgebungen. Nachdem eine Ressource höhergestuft wurde, wird die Verknüpfung zwischen dem Quellsystem und dem replizierten System unterbrochen. Wenn bei diesem Ansatz zusätzliche Änderungen in den ursprünglichen Quellsystemen vorgenommen werden, gehen diese Änderungen verloren.

**Vorteile.** Bei diesem Ansatz gibt es folgende Vorteile:

- Durch dieses Modell werden weniger Änderungen in die Zielsysteme eingeführt.
- Eine fortlaufende Replikation minimiert den Datenverlust.
- Wenn ein Stagingprozess fehlschlägt, kann er schnell gelöscht und wiederholt werden.
- Replikation und wiederholte Stagingtests ermöglichen einen inkrementellen Prozess von Skripterstellung und Tests.

**Nachteile.** Bei diesem Ansatz gibt es folgende negative Aspekte:

- Ressourcen, die innerhalb der toolsisolierten Sandbox gestaffelt wurden, lassen keine komplexen Tests von Modellen zu.
- Das Migrationstool verbraucht während der Replikation Bandbreite im lokalen Rechenzentrum. Das Staging einer großen Anzahl von Ressourcen über einen längeren Zeitraum wirkt sich exponentiell auf die verfügbare Bandbreite aus, wodurch der Migrationsprozess und möglicherweise auch die Leistung von Produktionsworkloads in der lokalen Umgebung beeinträchtigt wird.

## <a name="staged-promotion"></a>Höherstufung „gestaffelt“

In diesem Modell wird die vom Migrationstool verwaltete Staging-Sandbox für eingeschränkte Testzwecke verwendet. Die replizierten Ressourcen werden dann in der Cloudumgebung bereitgestellt, die als eine erweiterte Stagingumgebung dient. Die migrierten Ressourcen werden in der Cloud ausgeführt, während zusätzliche Ressourcen repliziert, gestaffelt und migriert werden. Wenn vollständige Workloads zur Verfügung stehen, werden umfangreichere Tests eingeleitet. Nachdem alle einem Abonnement zugeordneten Ressourcen migriert wurden, werden das Abonnement und alle gehosteten Workloads in die Produktion höhergestuft. In diesem Szenario gibt es während des Höherstufungsprozesses keine Änderung an den Workloads. Stattdessen erfolgen die Änderungen häufig an der Vermittlungs- und Identitätsschicht, wodurch Benutzer in die neue Umgebung weitergeleitet und der Zugriff auf das Cloudeinführungsteam widerrufen wird.

**Vorteile.** Bei diesem Ansatz gibt es folgende Vorteile:

- Dieses Modell bietet präzisere Möglichkeiten für geschäftsbezogene Tests.
- Die Workload kann genauer untersucht werden, um die Leistung und Kosten der Ressourcen noch mehr zu optimieren.
- Eine größere Anzahl von Ressourcen kann innerhalb ähnlicher Zeit- und Bandbreiteneinschränkungen repliziert werden.

**Nachteile.** Bei diesem Ansatz gibt es folgende negative Aspekte:

- Das ausgewählte Migrationstool kann die laufende Replikation nach der Migration nicht unterstützen.
- Es ist eine zweite Methode der Datenreplikation erforderlich, um Datenplattformen während des gestaffelten Zeitrahmens zu synchronisieren.

## <a name="flight-promotion"></a>Höherstufung „Flight“

Dieses Modell ist ähnlich wie das Höherstufungsmodell „gestaffelt“. Es gibt jedoch einen grundlegenden Unterschied. Wenn das Abonnement bereit für die Höherstufung ist, erfolgt das Routing von Endbenutzern in Stufen oder Flights. Bei jedem Flight werden zusätzliche Benutzer an die Produktionssysteme umgeleitet.

**Vorteile.** Bei diesem Ansatz gibt es folgende Vorteile:

- Dieses Modell mindert die Risiken, die mit der Aktivität einer großen Migration oder Höherstufung verbunden sind. Fehler in der migrierten Lösung können mit einer geringeren Auswirkung auf Geschäftsprozesse identifiziert werden.
- Es ermöglicht die Überwachung von Anforderungen an die Workloadleistung in der Cloudumgebung über einen längeren Zeitraum. Dadurch lassen sich Entscheidungen zur Ressourcengröße mit höherer Genauigkeit treffen.
- Es können mehr Ressourcen innerhalb ähnlicher Zeit- und Bandbreiteneinschränkungen repliziert werden.

**Nachteile.** Bei diesem Ansatz gibt es folgende negative Aspekte:

- Das ausgewählte Migrationstool kann die laufende Replikation nach der Migration nicht unterstützen.
- Es ist eine zweite Methode der Datenreplikation erforderlich, um Datenplattformen während des gestaffelten Zeitrahmens zu synchronisieren.

## <a name="next-steps"></a>Nächste Schritte

Nachdem ein Höherstufungsmodell definiert und vom Cloudeinführungsteam akzeptiert wurde, kann die [Korrektur von Ressourcen](./remediate.md) beginnen.

> [!div class="nextstepaction"]
> [Korrigieren von Ressourcen vor der Migration](./remediate.md)
