---
title: Ausführen einer Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ausführen einer Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 21520edecc7ba874713561672cd0bd38aa96c0a2
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818232"
---
# <a name="execute-a-migration"></a>Ausführen einer Migration

Nachdem eine Workload bewertet wurde, kann sie in die Cloud migriert werden. In dieser Artikelreihe werden die verschiedenen Aktivitäten erläutert, die möglicherweise beim Ausführen einer Migration involviert sind.

## <a name="objective"></a>Ziel

Das Ziel einer Migration ist es, eine einzelne Workload in die Cloud zu migrieren.

## <a name="definition-of-done"></a>Definition von *Fertig*.

Die Migrationsphase ist abgeschlossen, wenn eine Workload in der Cloud bereitgestellt und testbereit ist, einschließlich aller abhängigen Ressourcen, die für die Funktion der Workload erforderlich sind. Während des Optimierungsprozesses wird die Workload für den Einsatz in der Produktionsumgebung vorbereitet.

Diese Definition von *Fertig* kann je nach Ihren Test- und Freigabeprozessen variieren. Der nächste Artikel in dieser Reihe behandelt die [Entscheidung für ein Höherstufungsmodell](./promotion-models.md) und kann Ihnen helfen zu verstehen, wann der beste Zeitpunkt ist, eine migrierte Workload in die Produktion hochzustufen.

## <a name="accountability-during-migration"></a>Verantwortlichkeit während der Migrationsphase

Das Cloudeinführungsteam ist für den gesamten Migrationsprozess verantwortlich. Die Mitglieder des Cloudstrategieteams haben jedoch ebenfalls einige Aufgaben, wie im folgenden Abschnitt erläutert.

## <a name="responsibilities-during-migration"></a>Zuständigkeiten während der Migrationsphase

Zusätzlich zur Verantwortlichkeit auf hoher Ebene gibt es Maßnahmen, für die eine Person oder Gruppe direkt verantwortlich sein muss. Im Folgenden sind einige Aktivitäten aufgeführt, die eine Zuordnung zu verantwortlichen Personen erfordern:

- **Problembehandlung** Beheben aller Kompatibilitätsprobleme, die eine Migration der Workload in die Cloud verhindern.
  - Wie im Artikel zur [technischen Komplexität und zum Change Management](../prerequisites/technical-complexity.md) erläutert, sollte im Voraus eine Entscheidung getroffen werden, wie diese Aktivität ausgeführt wird. Insbesondere sollte die Frage beantwortet werden, ob die Problembehandlung des Cloudeinführungsteams während des gleichen Durchgangs abgeschlossen wird wie der eigentliche Migrationsaufwand. Wird alternativ ein Wellen- oder Factorymodell verwendet, um die Problembehandlung in einer separaten Iteration abzuschließen? Wenn die Antwort auf diese grundlegende Prozessfrage nicht von jedem Mitglied des Teams beantwortet werden kann, ist es möglicherweise empfehlenswert, den Abschnitt [Voraussetzungen](../prerequisites/index.md) erneut zu besuchen.
- **Replikation** Erstellen einer Kopie der einzelnen Ressourcen in der Cloud, um virtuelle Computer, Daten und Anwendungen mit Ressourcen in der Cloud zu synchronisieren.
  - Abhängig vom Höherstufungsmodell können verschiedene Tools erforderlich sein, um diese Aktivität abzuschließen.
- **Staging** Nachdem alle Ressourcen für eine Workload repliziert und überprüft wurden, kann die Workload für geschäftsbezogene Tests und die Ausführung eines geschäftsbezogenen Änderungsplans bereitgestellt werden.

## <a name="next-steps"></a>Nächste Schritte

Mit einem allgemeinen Überblick über den Migrationsprozess sind Sie bereit, [sich für ein Höherstufungsmodell zu entscheiden](./promotion-models.md).

> [!div class="nextstepaction"]
> [Entscheiden für ein Höherstufungsmodell](./promotion-models.md)
