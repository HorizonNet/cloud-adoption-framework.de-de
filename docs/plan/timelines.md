---
title: Zeitpläne in einem Cloudeinführungsplan
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie basierend auf Ihrem Cloudeinführungsplan Zeitplanschätzungen durchführen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 885d5c46099c0e161449aeae3f9c1203a2949728
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092635"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Zeitpläne in einem Cloudeinführungsplan

Im vorherigen Artikel dieser Reihe wurden Workloads und Aufgaben zu [Releases und Iterationen](./iteration-paths.md) zugeordnet. Diese Zuweisungen versorgen die Zeitplanschätzungen in diesem Artikel.

In sequenziellen Projektverwaltungstools werden häufig Projektstrukturpläne (PSP) verwendet. Diese stellen dar, wie abhängige Aufgaben im Lauf der Zeit erledigt werden. Derartige Strukturen sind gut für sequenzielle Aufgaben geeignet. Die Abhängigkeiten in den Aufgaben zur Cloudeinführung erschweren die Verwaltung solcher Strukturen. Um diese Lücke zu schließen, können Sie Zeitpläne basierend auf Iterationspfadzuweisungen abschätzen, indem die Komplexität ausgeblendet wird.

## <a name="estimate-timelines"></a>Schätzen von Zeitplänen

Beginnen Sie bei der Entwicklung eines Zeitplans mit Releases. Diese Releaseziele erstellen ein Zieldatum für alle Auswirkungen auf das Unternehmen. Iterationen helfen bei der Ausrichtung dieser Releases auf bestimmte Zeitspannen.

Wenn im Zeitplan detailliertere Meilensteine erforderlich sind, nutzen Sie die Iterationszuweisung, um Meilensteine anzuzeigen. Um diese Zuweisung vorzunehmen, gehen Sie davon aus, dass die letzte Instanz einer Workload-bezogenen Aufgabe als letzter Meilenstein dienen kann. Teams markieren die letzte Aufgabe auch häufig als Meilenstein.

Für jeden Grad der Granularität verwenden Sie den letzten Tag der Iteration als Datum für die einzelnen Meilensteine. Dadurch wird die Erledigung der Workloadeinführung mit einem bestimmten Datum verknüpft. Sie können das Datum in einer Kalkulationstabelle oder in einem sequenziellen Projektverwaltungstool wie Microsoft Project nachverfolgen.

## <a name="delivery-plans-in-azure-devops"></a>Lieferpläne in Azure DevOps

Wenn Sie Azure DevOps zum Verwalten Ihres Einführungsplans für die Cloud verwenden, sollten Sie die Erweiterung [Microsoft-Lieferpläne](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans) verwenden. Diese Erweiterung kann schnell eine visuelle Darstellung des Zeitplans erstellen, die auf Iterations- und Releasezuweisungen beruht.
