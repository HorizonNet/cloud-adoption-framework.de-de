---
title: Bewerten von Ressourcen vor der Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Bewerten von Ressourcen vor der Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7aac08981375a3fcbbd658d6e14564a07e06795e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816294"
---
# <a name="assess-assets-prior-to-migration"></a>Bewerten von Ressourcen vor der Migration

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
- **Kosten:** Die Kosten der Zielarchitektur wurden geschätzt und das Gesamtbudget wurde angepasst.
- **Migrationsunterstützung:** Das Team hat entschieden, wie die technischen Aufgaben der Migration abgeschlossen werden, einschließlich der Entscheidungen über den Partner- oder Microsoft-Support.
- **Auswertung:** Die Workload wird hinsichtlich Kompatibilität und Abhängigkeiten bewertet.
  - Diese Aktivität sollte einem Fachexperten zugewiesen werden, der mit der Architektur und den Abläufen der Workload des Kandidaten vertraut ist.
- **Entwerfen:** Das Team hat sich auf die endgültige Zustandsarchitektur für die migrierte Workload geeinigt.
- **Backlogausrichtung:** Das Cloudeinführungsteam überprüft die Anforderungen und kümmert sich um die Migration der Kandidatenworkload. Nach der Zusage sind Releasebacklog und Iterationsbacklog entsprechend zu aktualisieren.
- **Projektstrukturplan oder Nachbearbeitungsplan:** Das Team erstellt einen Zeitplan mit wichtigen Meilensteinen, in dem die Ziele für den Abschluss von Planungs-, Implementierungs- und Überprüfungsprozessen festgelegt werden.
- **Abschließende Genehmigung:** Alle erforderlichen genehmigenden Personen haben den Plan überprüft und den Ansatz für die Migration der Ressource genehmigt.
  - Um spätere Überraschungen zu vermeiden, sollte mindestens ein Vertreter des Unternehmens in den Genehmigungsprozess einbezogen werden.

> [!CAUTION]
> Diese vollständige Liste von Verantwortlichkeiten und Aktionen kann große und komplexe Migrationen mit mehreren Rollen und unterschiedlichen Zuständigkeitsebenen unterstützen, die einen detaillierten Genehmigungsprozess erfordern. Kleinere und einfachere Migrationsaufgaben erfordern möglicherweise nicht alle hier beschriebenen Rollen und Aktionen. Um zu bestimmen, welche dieser Aktivitäten den Nutzen erhöhen und welche nicht erforderlich sind, empfiehlt sich für das Cloudeinführungs- und das Cloudstrategieteam die Verwendung dieses vollständigen Prozesses im Rahmen Ihrer ersten Workloadmigration. Nachdem die Workload überprüft und getestet wurde, kann das Team diesen Prozess bewerten und entscheiden, welche Aktionen verwendet werden sollen.

## <a name="next-steps"></a>Nächste Schritte

Mit einem allgemeinen Überblick über den Bewertungsprozess sind Sie bereit, den Prozess durch [Ausrichtung von geschäftlichen Prioritäten](./business-priorities.md) zu starten.

> [!div class="nextstepaction"]
> [Ausrichten von geschäftlichen Prioritäten](./business-priorities.md)
