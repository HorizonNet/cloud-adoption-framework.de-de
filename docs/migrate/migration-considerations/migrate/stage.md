---
title: Stagingaktivitäten während einer Migration
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit Stagingaktivitäten und den zugehörigen Ergebnissen vertraut zu machen, die während einer Migration benötigt werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: f6d45943ac8545083ce8d31215488b433a3ad00b
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80432464"
---
# <a name="understand-staging-activities-during-a-migration"></a>Verstehen der Stagingaktivitäten während einer Migration

Wie im Artikel zu Höherstufungsmodellen beschrieben, ist das *Staging* der Punkt, an dem Assets in die Cloud migriert werden. Sie sind allerdings noch nicht bereit, in die Produktion hochgestuft zu werden. Dies ist häufig der letzte Schritt im Migrationsprozess. Nach dem Staging wird die Workload von einem IT-Betriebs- oder Cloudbetriebsteam verwaltet, um sie auf die Nutzung in der Produktion vorzubereiten.

## <a name="deliverables"></a>Ergebnisse

In der Stagingphase sind Assets möglicherweise noch nicht für die Nutzung in der Produktion bereit. Es gibt verschiedene Prüfungen, die durchgeführt werden sollten, bevor diese Phase als abgeschlossen betrachtet werden kann. Im Folgenden finden Sie eine Liste der Ergebnisse, die häufig mit dem Abschluss des Stagingprozesses von Assets in Verbindung gebracht werden.

- **Automatisierte Tests**: Alle automatisierten Tests, die zur Überprüfung der Workloadleistung verfügbar sind, sollten vor Abschluss des Stagingprozesses ausgeführt werden. Wenn das Asset die Stagingphase verlässt, ist die Synchronisierung mit dem ursprünglichen Quellsystem beendet. Daher ist es schwieriger, die replizierten Assets erneut bereitzustellen, nachdem diese zur Optimierung in die Stagingphase versetzt wurden.
- **Dokumentation zur Migration**: Die meisten Migrationstools können einen automatisierten Bericht zu den Assets generieren, die migriert werden. Bevor die Stagingaktivität abgeschlossen wird, sollten alle migrierten Assets aus Gründen der Klarheit dokumentiert werden.
- **Dokumentation zur Konfiguration**: Änderungen, die an einem Asset vorgenommen wurden (während eines Problembehebungs-, Replikations- oder Stagingprozesses), sollten zum Zweck der Betriebsbereitschaft dokumentiert werden.
- **Dokumentation zum Backlog**: Das Migrationsbacklog sollte aktualisiert werden, um widerzuspiegeln, welche Workloads und Assets sich in der Stagingphase befinden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Assets in der Stagingphase getestet und dokumentiert wurden, können Sie mit [Aktivitäten zur Optimierung](../optimize/index.md) fortfahren.

> [!div class="nextstepaction"]
> [Optimieren von migrierten Workloads](../optimize/index.md)
