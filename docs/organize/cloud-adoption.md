---
title: Grundlegendes zu Cloudeinführungsfunktionen
description: Erfahren Sie, wie Cloudeinführungsfunktionen technische Lösungen ermöglichen, sodass Sie Ihre Teams entsprechend besetzen können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: c2f030d594a3bdb3ef195252187ae3c033c06e27
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755812"
---
# <a name="cloud-adoption-functions"></a>Cloudeinführungsfunktionen

Cloudeinführungsfunktionen ermöglichen die Implementierung technischer Lösungen in der Cloud. Wie bei jedem IT-Projekt entscheiden die Personen, die die eigentliche Arbeit leisten, über den Erfolg. Die Teams, die die notwendigen Cloudeinführungsfunktionen bereitstellen, können aus verschiedenen fachlichen Ansprechpartnern oder Implementierungspartnern bestehen.

Cloudeinführungsteams sind das moderne Äquivalent zu technischen Implementierungs- oder Projektteams. Die Charakteristik der Cloud kann aber eine dynamischere Teamstruktur erfordern. Einige Teams konzentrieren sich ausschließlich auf die Cloudmigration, während andere Teams sich schwerpunktmäßig mit Innovationen beschäftigen, die Cloudtechnologien nutzen. Einige Teams verfügen über das umfassende technische Fachwissen, das erforderlich ist, um große Implementierungsbemühungen wie eine vollständige Rechenzentrumsmigration abzuschließen. Andere Teams haben einen engeren technischen Fokus und wechseln möglicherweise zwischen den Projekten, um bestimmte Ziele zu erreichen. Ein Beispiel wäre ein Team von Datenplattformspezialisten, das bei der Konvertierung von SQL-VMs in SQL-PaaS-Instanzen hilft.

Unabhängig von der Art oder Anzahl der Cloudeinführungsteams wird die für die Cloudeinführung erforderliche Funktionalität durch fachliche Ansprechpartner aus den Bereichen IT, Geschäftsanalyse oder Implementierungspartner bereitgestellt.

Je nach den gewünschten Geschäftsergebnissen können die Fähigkeiten, die für umfassende Funktionen für die Cloudeinführung benötigt werden, Folgendes umfassen:

- Infrastrukturimplementierer
- DevOps-Techniker
- Anwendungsentwickler
- Datenanalysten
- Daten- oder Anwendungsplattformexperten

Um eine optimale Zusammenarbeit und Effizienz zu erzielen, wird empfohlen, dass Cloudeinführungsteams über eine durchschnittliche Teamgröße von sechs Personen verfügen. Diese Teams sollten sich hinsichtlich der technischen Ausführung selbst organisieren. Es wird dringend empfohlen, dass diese Teams auch über Projektmanagementexpertise mit umfassender Erfahrung in agilen, Scrum- oder anderen iterativen Modellen verfügen. Dieses Team ist am effektivsten, wenn es über eine flache Struktur verwaltet wird.

## <a name="preparation"></a>Vorbereitung

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

## <a name="deliverable"></a>Ergebnisse

Der primäre Anspruch an eine Cloudeinführungsfunktion ist die rechtzeitige, hochwertige Implementierung der technischen Lösungen, die im Einführungsplan beschrieben sind. Diese Lösungen sollten sich an Governanceanforderungen und Geschäftsergebnisse orientieren und Technologie, Tools und Automatisierungslösungen nutzen, die dem Team zur Verfügung stehen.

**Anfängliche Planungsaufgaben:**

- Ausführen der [Rationalisierung der digitalen Ressourcen](../digital-estate/index.md).
- Überprüfen, Validieren und Verbessern des [priorisierten Migrationsbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Starten der Ausführung der [ersten Workload](../digital-estate/rationalize.md#select-the-first-workload) als Lernmöglichkeit.

**Fortlaufende monatliche Aufgaben:**

- Überwachen der [Change Management-Prozesse](../migrate/migration-considerations/prerequisites/technical-complexity.md).
- Verwalten der [Release- und Sprintbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Erstellen und Verwalten der Einführungslandezone in Verbindung mit den Governanceanforderungen.
- Ausführen der in den [Sprintbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md) beschriebenen technischen Aufgaben.

**Rhythmus von Besprechungen:**

Es wird empfohlen, dass Teams, die Cloudeinführungsfunktionen bereitstellen, sich in Vollzeit auf diese Aufgabe konzentrieren.

Dabei ist es am besten, wenn sich diese Teams täglich selbstständig treffen. Das Ziel täglicher Besprechungen ist es, das Backlog schnell zu aktualisieren, die Ergebnisse und heute zu erledigende Aufgaben sowie blockierte Bereiche zu kommunizieren, die zusätzliche externe Unterstützung erfordern.

Releasezeitpläne und Iterationszeitspannen sind für jedes Unternehmen spezifisch. Allerdings ist ein Zeitraum von einer bis vier Wochen pro Iteration die durchschnittliche Dauer. Unabhängig vom Iterations- oder Releaserhythmus wird empfohlen, dass das Team am Ende jedes Releases alle unterstützenden Teams trifft, um das Releaseergebnis zu kommunizieren und die kommenden Bemühungen neu zu priorisieren. Ebenso ist es wichtig, sich am Ende eines jeden Sprints als Team mit dem Cloudkompetenzzentrums- oder Cloudgovernanceteam zu treffen, um sich auf gemeinsame Bemühungen und jeglichen Unterstützungsbedarf einzustellen.

Einige der technischen Aufgaben, die mit der Einführung der Cloud verbunden sind, können sich wiederholen. Teammitglieder sollten alle drei bis sechs Monate rotieren, um Probleme mit der Mitarbeiterzufriedenheit zu vermeiden und relevante Qualifikationen zu erhalten. Ein wechselnder Platz im Cloudkompetenzzentrums- oder Cloudgovernanceteam kann eine ausgezeichnete Gelegenheit bieten, die Mitarbeiter zu motivieren und Innovationen zu nutzen.

Erfahren Sie mehr über die Funktion eines [Cloudkompetenzzentrums (CCoE, Cloud Center of Excellence)](./cloud-center-of-excellence.md) oder eines [Cloudgovernanceteams](./cloud-governance.md).

## <a name="next-steps"></a>Nächste Schritte

- [Aufbauen eines Cloudeinführungsteams](../get-started/team/cloud-adoption.md)
- Stimmen Sie Cloudeinführungsbemühungen mit [Cloudgovernancefunktionen](./cloud-governance.md) ab, um die Einführung und Implementierung bewährter Methoden zu beschleunigen und gleichzeitig unternehmerische sowie technische Risiken zu verringern.
