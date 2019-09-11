---
title: Verstehen der Stagingaktivitäten während einer Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verstehen der Stagingaktivitäten während einer Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a23a1e0f42382311a67e39238db8762c27c14480
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836644"
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
