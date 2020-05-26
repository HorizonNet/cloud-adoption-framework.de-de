---
title: Grundlegendes zu Cloudmigrationsfunktionen
description: Grundlegendes zu Cloudmigrationsfunktionen.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 04/04/2020
ms.openlocfilehash: 876705322aad42ac2dac0eb29d7291d6d6df71ec
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401004"
---
# <a name="cloud-migration-functions"></a>Cloudmigrationsfunktionen

Cloudmigrationsteams sind das moderne Äquivalent zu technischen Implementierungs- oder Projektteams. Die Charakteristik der Cloud kann jedoch eine dynamischere Teamstruktur erfordern. Einige Migrationsteams konzentrieren sich ausschließlich auf die Cloudmigration, während andere Teams sich schwerpunktmäßig mit Innovationen beschäftigen, die Cloudtechnologien nutzen. Einige Teams verfügen über das breite technische Fachwissen, das erforderlich ist, um große Einführungsbemühungen wie eine vollständige Rechenzentrumsmigration abzuschließen, während andere einen engeren technischen Fokus haben und zwischen Projekten wechseln können, um bestimmte Ziele zu erreichen, z. B. ein Team von Datenplattformspezialisten, das bei der Konvertierung von SQL-VMs in SQL-PaaS-Instanzen mitwirkt.

Unabhängig von der Art oder Anzahl der Cloudmigrationsteams bieten diese Teams in der Regel fachliche Expertise für IT, Geschäftsanalysen oder Implementierungspartner.

## <a name="prerequisites"></a>Voraussetzungen

- [Erstellen eines Azure-Kontos](https://docs.microsoft.com/learn/modules/create-an-azure-account): Der erste Schritt beim Verwenden von Azure ist, ein Konto zu erstellen.
- [Azure-Portal](https://docs.microsoft.com/learn/modules/tour-azure-portal): Führen Sie die Tour durch die Features und Dienste im Azure-Portal durch, und passen Sie das Portal an.
- [Einführung in Azure](https://docs.microsoft.com/learn/modules/welcome-to-azure): Erste Schritte mit Azure. Erstellen und konfigurieren Sie Ihren ersten virtuellen Computer in der Cloud.
- [Azure-Grundlagen](https://docs.microsoft.com/learn/paths/azure-for-the-data-engineer): Erfahren Sie mehr über Cloudkonzepte, deren Vorteile, vergleichen und kontrastieren Sie grundlegende Strategien, und entdecken Sie das breite Angebot der in Azure verfügbaren Dienste.
- Sehen Sie sich die [Migrationsmethodik](../migrate/index.md) an.

## <a name="minimum-scope"></a>Mindestumfang

Das Herzstück aller Cloudeinführungsmaßnahmen ist das Cloudmigrationsteam. Dieses Team stößt die technischen Änderungen an, die eine Einführung ermöglichen. Abhängig von den Zielen des Einführungsprojekts kann dieses Team aus vielen Mitgliedern unterschiedlichster Fachrichtungen bestehen, die eine umfassende Palette technischer und geschäftlicher Aufgaben übernehmen.

Der Teamumfang umfasst mindestens:

- [Rationalisierung der digitalen Ressourcen](../digital-estate/index.md)
- Überprüfen, Validieren und Verbessern des [priorisierten Migrationsbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md)
- Die Ausführung der [ersten Workload](../digital-estate/rationalize.md#select-the-first-workload) als Lernmöglichkeit.

## <a name="deliverable"></a>Zielvorgaben

Die primäre Zielvorgabe für jedes Cloudmigrationsteam ist die rechtzeitige und qualitativ hochwertige Implementierung der im Einführungsplan skizzierten technischen Lösungen in Übereinstimmung mit den Governanceanforderungen und Geschäftsergebnissen unter Verwendung von verfügbaren Technologien, Tools und Automatisierungslösungen.

### <a name="ongoing-monthly-tasks"></a>Fortlaufende monatliche Aufgaben

- Überwachen der [Change Management-Prozesse](../migrate/migration-considerations/prerequisites/technical-complexity.md).
- Verwalten der [Release- und Sprintbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md)
- Erstellen und Verwalten der Einführungszielzone in Verbindung mit den Governanceanforderungen.
- Abschließen der in den [Sprintbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md) beschriebenen technischen Aufgaben.

### <a name="team-cadence"></a>Teamrhythmus

Es wird empfohlen, dass Teams, die Cloudeinführungsfunktionen bereitstellen, sich in Vollzeit auf diese Aufgabe konzentrieren.

Dabei ist es am besten, wenn sich diese Teams täglich selbstständig treffen. Das Ziel täglicher Besprechungen ist es, das Backlog schnell zu aktualisieren, die Ergebnisse und heute zu erledigende Aufgaben sowie blockierte Bereiche zu kommunizieren, die zusätzliche externe Unterstützung erfordern.

Releasezeitpläne und Iterationszeitspannen sind für jedes Unternehmen spezifisch. Allerdings ist ein Zeitraum von einer bis vier Wochen pro Iteration die durchschnittliche Dauer. Unabhängig vom Iterations- oder Releaserhythmus wird empfohlen, dass das Team am Ende jedes Releases alle unterstützenden Teams trifft, um das Releaseergebnis zu kommunizieren und die kommenden Bemühungen neu zu priorisieren. Es ist auch wichtig, sich am Ende eines jeden Sprints als Team mit dem [Cloudkompetenzzentrums](../organize/cloud-center-of-excellence.md)- oder [Cloudgovernanceteam](./cloud-governance.md) zu treffen, um sich auf gemeinsame Bemühungen und jeglichen Unterstützungsbedarf einzustellen.

Einige der technischen Aufgaben, die mit der Einführung der Cloud verbunden sind, können sich wiederholen. Teammitglieder sollten alle drei bis sechs Monate rotieren, um Probleme mit der Mitarbeiterzufriedenheit zu vermeiden und relevante Qualifikationen zu erhalten. Ein wechselnder Platz im [Cloudkompetenzzentrums](../organize/cloud-center-of-excellence.md)- oder [Cloudgovernanceteam](./cloud-governance.md) kann eine ausgezeichnete Gelegenheit bieten, die Mitarbeiter zu motivieren und Innovationen zu nutzen.

## <a name="baseline-capability"></a>Baselinefunktionalität

Je nach den gewünschten Geschäftsergebnissen können die Fähigkeiten, die für umfassende Funktionen für die Cloudeinführung benötigt werden, Folgendes umfassen:

- Infrastrukturimplementierer
- DevOps-Techniker
- Anwendungsentwickler
- Datenanalysten
- Daten- oder Anwendungsplattformexperten

Um eine optimale Zusammenarbeit und Effizienz zu erzielen, wird empfohlen, dass Cloudeinführungsteams über eine durchschnittliche Teamgröße von sechs Personen verfügen. Diese Teams sollten sich hinsichtlich der technischen Ausführung selbst organisieren. Es wird dringend empfohlen, dass diese Teams auch über Projektmanagementexpertise mit umfassender Erfahrung in agilen, Scrum- oder anderen iterativen Modellen verfügen. Dieses Team ist am effektivsten, wenn es über eine flache Struktur verwaltet wird.

## <a name="out-of-scope"></a>Nicht betreffende Organisationen

Weitere Unterstützung durch vorhandene IT-Mitarbeiter ist möglicherweise erforderlich. Die IT kann einen wertvollen Beitrag zur Cloudeinführung leisten, indem sie zum Cloudbroker und Partner für Innovationen und geschäftliche Agilität wird.

- [Zuständigkeiten der zentralen IT](../organize/central-it.md)

## <a name="whats-next"></a>Nächste Schritte

Die Einführung ist großartig, aber eine unkontrollierte Einführung kann zu unerwarteten Ergebnissen führen. Die Abstimmung mit dem [Cloudgovernanceteam](./cloud-governance.md) beschleunigt die Einführung und bewährte Methoden und reduziert gleichzeitig unternehmerische sowie technische Risiken.

Diese beiden Teams sorgen für ein ausgewogenes Verhältnis von Cloudeinführungsbemühungen, werden jedoch als MVP angesehen, da das Ergebnis möglicherweise nicht nachhaltig ist. Jedes Team hat viele Aufgaben, wie in den [RACI-Diagrammen (*Responsible, Accountable, Consulted, Informed*)](../organize/raci-alignment.md) erläutert wird.

Weitere Informationen zu [Antimustern in Organisationen: Silos und Machtbereiche](../organize/fiefdoms-silos.md).
