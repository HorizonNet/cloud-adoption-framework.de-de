---
title: Zeitpläne in einem Cloudeinführungsplan
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie basierend auf Ihrem Cloudeinführungsplan Zeitplanschätzungen durchführen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 04cfd35b56fb345474d3d4dd5f554f5bb3eb6f5c
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884707"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Zeitpläne in einem Cloudeinführungsplan

Im vorherigen Artikel dieser Reihe wurden Workloads und Aufgaben zu [Releases und Iterationen](./iteration-paths.md) zugeordnet. Diese Zuweisungen versorgen die Zeitplanschätzungen in diesem Artikel.

In sequenziellen Projektverwaltungstools werden häufig Projektstrukturpläne verwendet. Diese stellen dar, wie abhängige Aufgaben im Lauf der Zeit erledigt werden. Derartige Strukturen sind gut für sequenzielle Aufgaben geeignet. Die Abhängigkeiten in den Aufgaben zur Cloudeinführung erschweren die Verwaltung solcher Strukturen. Um diese Lücke zu schließen, können Sie Zeitpläne basierend auf Iterationspfadzuweisungen abschätzen, indem die Komplexität ausgeblendet wird.

## <a name="estimate-timelines"></a>Schätzen von Zeitplänen

Beginnen Sie bei der Entwicklung eines Zeitplans mit Releases. Diese Releaseziele erstellen ein Zieldatum für alle Auswirkungen auf das Unternehmen. Iterationen helfen bei der Ausrichtung dieser Releases auf bestimmte Zeitspannen.

Wenn im Zeitplan detailliertere Meilensteine erforderlich sind, nutzen Sie die Iterationszuweisung, um Meilensteine anzuzeigen. Um diese Zuweisung vorzunehmen, gehen Sie davon aus, dass die letzte Instanz einer Workload-bezogenen Aufgabe als letzter Meilenstein dienen kann. Teams markieren die letzte Aufgabe auch häufig als Meilenstein.

Für jeden Grad der Granularität verwenden Sie den letzten Tag der Iteration als Datum für die einzelnen Meilensteine. Dadurch wird die Erledigung der Workloadeinführung mit einem bestimmten Datum verknüpft. Sie können das Datum in einer Kalkulationstabelle oder in einem sequenziellen Projektverwaltungstool wie Microsoft Project nachverfolgen.

## <a name="delivery-plans-in-azure-devops"></a>Lieferpläne in Azure DevOps

<!-- docsTest:casing "Microsoft Delivery Plans" -->

Wenn Sie Ihren Cloudeinführungsplan mit Azure DevOps verwalten, sollten Sie die [Microsoft-Erweiterung für Lieferpläne (Delivery Plans)](https://marketplace.visualstudio.com/items?itemname=ms.vss-plans) verwenden. Diese Erweiterung kann schnell eine visuelle Darstellung des Zeitplans erstellen, die auf Iterations- und Releasezuweisungen beruht.
