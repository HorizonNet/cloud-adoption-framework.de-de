---
title: Iterations- und Releasebacklog
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie ein Iterations- und Releasebacklog zum Organisieren Ihrer Aufgaben erstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4cbf0c7760ed2c471e1b462ae2712c544e9d0e8c
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355493"
---
# <a name="manage-change-in-an-incremental-migration-effort"></a>Verwalten von Änderungen bei einer inkrementellen Migration

In diesem Artikel wird davon ausgegangen, dass Migrationsprozesse inkrementell sind und parallel zum [Governanceprozess](../../../govern/index.md) ausgeführt werden. Dieselben Anleitungen können aber auch verwendet werden, um erste Aufgaben in einem Projektstrukturplan für herkömmliche Change Management-Ansätze des Wasserfalltyps auszufüllen.

## <a name="release-backlog"></a>Releasebacklog

Ein *Releasebacklog* besteht aus einer Reihe von Ressourcen (virtuelle Computer, Datenbanken, Dateien, Anwendungen usw.), die migriert werden müssen, bevor eine Workload für den Produktionseinsatz in der Cloud freigegeben werden kann. Während jeder Iteration dokumentiert und schätzt das Cloudeinführungsteam den erforderlichen Aufwand für das Verschieben der einzelnen Ressourcen in die Cloud. Informationen dazu finden Sie im folgenden Abschnitt „Iterationsbacklog“.

## <a name="iteration-backlog"></a>Iterationsbacklog

Ein *Iterationsbacklog* ist eine Liste der detaillierten Arbeitsschritte, die erforderlich sind, um eine bestimmte Anzahl von Ressourcen aus dem vorhandenen digitalen Bestand in die Cloud zu migrieren. Die Einträge in dieser Liste werden häufig als Arbeitselemente in einem agilen Verwaltungstool wie Azure DevOps gespeichert.

Vor Beginn der ersten Iteration legt das Cloudeinführungsteam eine Iterationsdauer fest. Dies sind in der Regel zwei bis vier Wochen. Dieses Zeitfenster ist wichtig, um einen Start- und Abschlusszeitraum für jede Gruppe zugesicherter Aktivitäten zu erstellen. Die Aufrechterhaltung konsistenter Ausführungsfenster erleichtert das Messen der Geschwindigkeit (Tempo der Migration) und das Anpassen an die sich ändernden Geschäftsanforderungen.

Vor jeder Iteration überprüft das Team das Releasebacklog und schätzt den Aufwand und Prioritäten der zu migrierenden Ressourcen. Anschließend verpflichtet es sich, eine bestimmte Anzahl vereinbarter Migrationen durchzuführen. Nachdem das Cloudeinführungsteam dem zugestimmt hat, wird die Liste mit den Aktivitäten zum *aktuellen Iterationsbacklog*.

Während jeder Iteration arbeiten Teammitglieder als selbstorganisierendes Team, um die Verpflichtungen im aktuellen Iterationsbacklog zu erfüllen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem ein Iterationsbacklog definiert und vom Cloudeinführungsteam akzeptiert wurde, können [Change Management-Genehmigungen](./approve.md) endgültig festgelegt werden.

> [!div class="nextstepaction"]
> [Genehmigen von Änderungen an der Architektur vor der Migration](./approve.md)
