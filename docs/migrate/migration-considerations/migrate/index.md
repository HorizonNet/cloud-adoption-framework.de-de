---
title: Ausführen einer Migration
description: Verschaffen Sie sich einen Überblick über die Artikel, in denen die verschiedenen Aktivitäten erläutert werden, die unter Umständen bei der Migration einer Workload in Azure ausgeführt werden müssen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 115b79d41c4f7d0c2c9b27db0d42b61e1ee45dee
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81119689"
---
# <a name="deploy-workloads"></a>Bereitstellen von Workloads

Nachdem Workloads bewertet wurden, können sie in der Cloud bereitgestellt oder für die Freigabe gestaget werden. In dieser Artikelreihe werden die verschiedenen Aktivitäten erläutert, die in dieser Phase des Migrationsablaufs erforderlich sein können.

## <a name="objective"></a>Ziel

Das Ziel einer Migration ist es, eine einzelne Workload in die Cloud zu migrieren.

## <a name="definition-of-done"></a>Definition von *Fertig*.

Die Migrationsphase ist abgeschlossen, wenn eine Workload in der Cloud bereitgestellt und testbereit ist, einschließlich aller abhängigen Ressourcen, die für die Funktion der Workload erforderlich sind. Während des Optimierungsprozesses wird die Workload für den Einsatz in der Produktionsumgebung vorbereitet.

Diese Definition von *Fertig* kann je nach Ihren Test- und Freigabeprozessen variieren. Der nächste Artikel in dieser Reihe behandelt die [Entscheidung für ein Höherstufungsmodell](./promotion-models.md) und kann Ihnen helfen zu verstehen, wann der beste Zeitpunkt ist, eine migrierte Workload in die Produktion hochzustufen.

## <a name="accountability-during-migration"></a>Verantwortlichkeit während der Migrationsphase

Das Cloudeinführungsteam ist für den gesamten Migrationsprozess verantwortlich. Die Mitglieder des Cloudstrategieteams haben jedoch ebenfalls einige Aufgaben, wie im folgenden Abschnitt erläutert.

## <a name="responsibilities-during-migration"></a>Zuständigkeiten während der Migrationsphase

Zusätzlich zur Verantwortlichkeit auf hoher Ebene gibt es Maßnahmen, für die eine Person oder Gruppe direkt verantwortlich sein muss. Im Folgenden sind einige Aktivitäten aufgeführt, die eine Zuordnung zu verantwortlichen Personen erfordern:

- **Korrektur:** Beheben aller Kompatibilitätsprobleme, die eine Migration der Workload in die Cloud verhindern.
  - Wie im Artikel zur [technischen Komplexität und zum Change Management](../prerequisites/technical-complexity.md) erläutert, sollte im Voraus eine Entscheidung getroffen werden, wie diese Aktivität ausgeführt wird. Insbesondere sollte die Frage beantwortet werden, ob die Problembehandlung des Cloudeinführungsteams während des gleichen Durchgangs abgeschlossen wird wie der eigentliche Migrationsaufwand. Wird alternativ ein Wellen- oder Factorymodell verwendet, um die Problembehandlung in einer separaten Iteration abzuschließen? Wenn die Antwort auf diese grundlegende Prozessfrage nicht von jedem Mitglied des Teams beantwortet werden kann, ist es möglicherweise empfehlenswert, den Abschnitt [Voraussetzungen](../prerequisites/index.md) erneut zu besuchen.
- **Replikation** Erstellen einer Kopie der einzelnen Ressourcen in der Cloud, um virtuelle Computer, Daten und Anwendungen mit Ressourcen in der Cloud zu synchronisieren.
  - Abhängig vom Höherstufungsmodell können verschiedene Tools erforderlich sein, um diese Aktivität abzuschließen.
- **Staging** Nachdem alle Ressourcen für eine Workload repliziert und überprüft wurden, kann die Workload für geschäftsbezogene Tests und die Ausführung eines geschäftsbezogenen Änderungsplans bereitgestellt werden.

## <a name="next-steps"></a>Nächste Schritte

Mit einem allgemeinen Überblick über den Migrationsprozess sind Sie bereit, [sich für ein Höherstufungsmodell zu entscheiden](./promotion-models.md).

> [!div class="nextstepaction"]
> [Entscheiden für ein Höherstufungsmodell](./promotion-models.md)
