---
title: Validierung von Bewertungsannahmen vor der Migration
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Bewertungsannahmen vor Beginn der Migration in die Cloud überprüft werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: cc095a1751e945ca18763757582a6cd27b65d72a
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81119765"
---
# <a name="assess-workloads-and-validate-assumptions-before-migration"></a>Bewerten von Workloads und Validieren von Annahmen vor der Migration

Viele Ihrer vorhandenen Workloads sind ideale Kandidaten für eine Cloudmigration, aber nicht alle Ressourcen sind mit Cloudplattformen kompatibel. Ebenso können nicht alle Workloads vom Hosting in der Cloud profitieren. Die [Planung digitaler Bestände](../../../digital-estate/index.md) ermöglicht es Ihnen, einen allgemeinen [Migrationsbacklog](../prerequisites/technical-complexity.md#migration-backlog-aligning-business-priorities-and-timing) potenzieller Workloads für die Migration zu erstellen. Dieser Planungsaufwand erfolgt jedoch auf hoher Ebene. Es stützt sich auf Annahmen des Cloudstrategieteams und beschäftigt sich nicht ausführlicher mit technischen Überlegungen.

Daher ist es wichtig, vor der Migration einer Workload in die Cloud die einzelnen mit dieser Workload verbundenen Ressourcen auf ihre Eignung für die Migration zu überprüfen. Während dieser Bewertung sollte Ihr Cloudeinführungsteam die technische Kompatibilität, die erforderliche Architektur, die Leistungs-/Skalierungserwartungen und Abhängigkeiten bewerten, um sicherzustellen, dass die migrierte Workload effektiv in der Cloud bereitgestellt werden kann.

Der Prozess *Bewerten* ist die erste von vier inkrementellen Aktivitäten, die innerhalb einer Iteration auftreten. Wie im Artikel zur [technischen Komplexität und zum Change Management](../prerequisites/technical-complexity.md) erläutert, sollte im Voraus eine Entscheidung getroffen werden, wie diese Phase durchgeführt wird. Insbesondere sollte die Frage beantwortet werden, ob die Bewertungen des Cloudeinführungsteams während des gleichen Durchgangs abgeschlossen werden wie der eigentliche Migrationsaufwand. Wird alternativ ein Wellen- oder Factorymodell verwendet, um die Bewertungen in einer separaten Iteration abzuschließen? Wenn die Antwort auf diese grundlegende Prozessfrage nicht von jedem Mitglied des Teams beantwortet werden kann, ist es möglicherweise empfehlenswert, den Abschnitt [Voraussetzungen](../prerequisites/index.md) erneut zu besuchen.

## <a name="objective"></a>Ziel

Bewerten eines Migrationskandidaten und Bewerten der Workload, der zugehörigen Ressourcen und der Abhängigkeiten vor der Migration.

## <a name="definition-of-done"></a>Definition von *Fertig*.

Dieser Prozess ist abgeschlossen, wenn die folgenden Punkte über einen einzelnen Migrationskandidaten bekannt sind:

- Der Weg von einem lokalen Ansatz zur Cloud, einschließlich der Entscheidung über den Ansatz der Höherstufung zur Produktion, wurde definiert.
- Alle erforderlichen Genehmigungen, Änderungen, Kostenschätzungen oder Validierungsprozesse wurden abgeschlossen, damit das Cloudeinführungsteam die Migration durchführen kann.

## <a name="accountability-during-assessment"></a>Verantwortlichkeit während der Bewertungsphase

Das Cloudeinführungsteam ist für den gesamten Bewertungsprozess verantwortlich. Die Mitglieder des Cloudstrategieteams haben jedoch auch einige Aufgaben, wie im folgenden Abschnitt beschrieben.

## <a name="responsibilities-during-assessment"></a>Zuständigkeiten während der Bewertungsphase

Zusätzlich zur Verantwortlichkeit auf hoher Ebene gibt es Maßnahmen, für die eine Person oder Gruppe direkt verantwortlich sein muss. Im Folgenden sind einige Aktivitäten aufgeführt, die eine Zuordnung zu verantwortlichen Personen erfordern:

- **Geschäftliche Priorität** Das Team versteht den Zweck der Migration dieser Workload, einschließlich aller geplanten Auswirkungen auf das Geschäft.
  - Ein Mitglied des Cloudstrategieteams sollte die Letztverantwortung für diese Aktivität tragen (unter der Leitung des Cloudeinführungsteams).
- **Ausrichtung der Projektbeteiligten** Das Team stimmt die Erwartungen und Prioritäten mit den internen Projektbeteiligten ab und identifiziert Erfolgskriterien für die Migration. Wie sieht der Erfolg nach der Migration aus?
- **Optimierte Rationalisierung:** Werten Sie die anfänglichen Annahmen bezüglich der Rationalisierung aus. Sollte ein anderer [Rationalisierungsansatz](../../../digital-estate/rationalize.md) zum Migrieren dieser bestimmten Workload verwendet werden?
- **Modernisierungsentscheidungen:** Sollten unabhängig von der Rationalisierungsentscheidung verschiedene Ressourcen in der Workload optimiert werden, um auf PaaS basierende Lösungen zu nutzen?
- **Kosten:** Die Kosten der Zielarchitektur wurden geschätzt und das Gesamtbudget wurde angepasst.
- **Migrationsunterstützung:** Das Team hat entschieden, wie die technischen Aufgaben der Migration abgeschlossen werden, einschließlich der Entscheidungen über den Partner- oder Microsoft-Support.
- **Auswertung:** Die Workload wird hinsichtlich Kompatibilität und Abhängigkeiten bewertet.
  - Diese Aktivität sollte einem Fachexperten zugewiesen werden, der mit der Architektur und den Abläufen der Workload des Kandidaten vertraut ist.
- **Entwerfen:** Das Team hat sich auf die endgültige Zustandsarchitektur für die migrierte Workload geeinigt.
- **Migrationstools:** Abhängig von den Modernisierungs- und Architekturansätzen können verschiedene Migrationstools verwendet werden, um die Migration zu automatisieren. Werden bei dieser Migration die besten [Migrationstools](../../../decision-guides/migrate-decision-guide/index.md) basierend auf der vorgeschlagenen Architektur verwendet?
- **Backlogausrichtung:** Das Cloudeinführungsteam überprüft die Anforderungen und kümmert sich um die Migration der Kandidatenworkload. Nach der Zusage sind Releasebacklog und Iterationsbacklog entsprechend zu aktualisieren.
- **Projektstrukturplan oder Nachbearbeitungsplan:** Das Team erstellt einen Zeitplan mit wichtigen Meilensteinen, in dem die Ziele für den Abschluss von Planungs-, Implementierungs- und Überprüfungsprozessen festgelegt werden.
- **Abschließende Genehmigung:** Alle erforderlichen genehmigenden Personen haben den Plan überprüft und den Ansatz für die Migration der Ressource genehmigt.
  - Um spätere Überraschungen zu vermeiden, sollte mindestens ein Vertreter des Unternehmens in den Genehmigungsprozess einbezogen werden.

> [!CAUTION]
> Diese vollständige Liste von Verantwortlichkeiten und Aktionen kann große und komplexe Migrationen mit mehreren Rollen und unterschiedlichen Zuständigkeitsebenen unterstützen, die einen detaillierten Genehmigungsprozess erfordern. Kleinere und einfachere Migrationsaufgaben erfordern möglicherweise nicht alle hier beschriebenen Rollen und Aktionen. Um zu bestimmen, welche dieser Aktivitäten den Nutzen erhöhen und welche nicht erforderlich sind, sollte das Cloudeinführungs- und das Cloudstrategieteam im Rahmen Ihrer ersten Workloadmigration diesen vollständigen Prozess durchführen. Nachdem die Workload überprüft und getestet wurde, kann das Team diesen Prozess bewerten und entscheiden, welche Aktionen verwendet werden sollen.

## <a name="next-steps"></a>Nächste Schritte

Mit einem allgemeinen Überblick über den Bewertungsprozess sind Sie bereit, den Prozess durch das [Klassifizieren von Workloads](./classify.md) zu starten.

> [!div class="nextstepaction"]
> [Klassifizieren von Workloads](./classify.md)
