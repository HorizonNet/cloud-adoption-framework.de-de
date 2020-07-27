---
title: Mehrere Rechenzentren
description: Mehrere Rechenzentren
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7a2a2684eb0b23c4a2f0c9b93665de1c52442050
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86450933"
---
# <a name="multiple-datacenters"></a>Mehrere Rechenzentren

Häufig umfasst ein Migrationsprojekt mehrere Rechenzentren. Die folgende Anleitung erweitert den Umfang des [Azure-Migrationsleitfadens](../azure-migration-guide/index.md), um Verfahren für mehrere Rechenzentren zu beschreiben.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Die meisten Aufgaben dieser Umfangserweiterung finden in den Prozessen für die Erfüllung von Voraussetzungen, die Bewertung und die Optimierung einer Migration statt.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Vor Beginn der Migration sollten Sie im Projektmanagementtool Epics für jedes Rechenzentrum erstellen, das migriert werden soll. Danach ist es wichtig, die geschäftlichen Ergebnisse und Beweggründe zu verstehen, die diese Migration rechtfertigen. Diese Beweggründe können zum Priorisieren der Liste der Epics (bzw. Rechenzentren) verwendet werden. Wenn eine Migration z.B. damit begründet wird, dass Rechenzentren verlassen werden sollen, bevor Leasingzeiträume verlängert werden müssen, müssen die Epics basierend auf den Verlängerungsdaten der Leasingverträge priorisiert werden.

In jedem Epic werden die Workloads, die bewertet und migriert werden sollen, als Features verwaltet. Jedes Asset innerhalb dieser Workload wird als User Story verwaltet. Die Arbeit, die zum Bewerten, Migrieren, Optimieren, Höherstufen, Sichern und Verwalten der Assets erforderlich ist, wird als Aufgabe für jedes Asset verwaltet.

Sprints oder Iterationen bestehen dann aus einer Reihe von Aufgaben, die zum Migrieren der Ressourcen bzw. User Storys erforderlich sind, die vom Cloudeinführungsteam festgelegt wurden. Releases umfassen diejenigen Workloads/Features, die in die Produktion hochgestuft werden sollen.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Bei einer Umfangserweiterung auf mehrere Rechenzentren steht die größte Änderung am Bewertungsprozess in Zusammenhang mit der präzisen Erfassung und Priorisierung von Workloads und Abhängigkeiten über Rechenzentren hinweg.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

**Evaluieren von rechenzentrumsübergreifenden Abhängigkeiten**: Die [Tools für die Visualisierung von Abhängigkeiten in Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) helfen bei der Ermittlung von Abhängigkeiten. Die Verwendung dieses Toolsets vor der Migration ist im Allgemeinen eine bewährte Methode. Wenn es aber um globale Komplexität geht, wird diese Verwendung zu einem notwendigen Schritt im Bewertungsprozess. Die Visualisierung durch die [Gruppierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) kann dabei helfen, die IP-Adressen und Ports aller Assets zu ermitteln, die zur Unterstützung der Workload erforderlich sind.

> [!IMPORTANT]
>
> - Ein Experte, der über Kenntnisse zu Ressourcenplatzierung und IP-Adressschemas verfügt, muss Ressourcen identifizieren, die sich in einem sekundären Rechenzentrum befinden.
> - Werten Sie sowohl Downstreamabhängigkeiten als auch Clients im visuellen Element aus, um bidirektionale Abhängigkeiten zu verstehen.


## <a name="migration-process-changes"></a>Änderungen für den Migrationsprozess

Die Migration mehrerer Rechenzentren ähnelt der Konsolidierung von Rechenzentren. Nach der Migration ist die Cloud die einzige Rechenzentrumslösung für mehrere Assets. Die wahrscheinlichste Umfangserweiterung während des Migrationsprozesses ist die Überprüfung und Ausrichtung von IP-Adressen.

### <a name="suggested-action-during-the-migration-process"></a>Empfohlene Aktion während des Migrationsprozesses

Folgende Aktivitäten tragen in hohem Maß zum Erfolg einer Cloudmigration bei:

- **Evaluieren von Netzwerkkonflikten**: Beim Konsolidieren von Rechenzentren zu einem einzelnen Cloudanbieter entstehen wahrscheinlich Konflikte hinsichtlich Netzwerk, DNS oder anderer Aspekte. Während der Migration ist es wichtig, Tests im Hinblick auf diese Konflikte durchzuführen, um Unterbrechungen in Produktionssystemen zu vermeiden, die in der Cloud gehostet werden.
- **Aktualisieren von Routingtabellen**: Häufig sind beim Konsolidieren von Netzwerken oder Rechenzentren Änderungen an Routingtabellen erforderlich.

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Während der Optimierung sind möglicherweise weitere Tests erforderlich.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Empfohlene Aktion während des Prozesses der Optimierung und Höherstufung

Bei dieser Umfangserweiterung müssen vor der Höherstufung zusätzliche Testebenen eingeführt werden. Hierbei müssen unbedingt Tests im Hinblick auf Routingkonflikte oder andere Netzwerkkonflikte ausgeführt werden. Darüber hinaus ist es wichtig, die bereitgestellte Anwendung zu isolieren und erneut zu testen, um zu überprüfen, ob alle Abhängigkeiten in die Cloud migriert wurden. In diesem Fall bedeutet Isolierung, die bereitgestellte Umgebung von Produktionsnetzwerken zu trennen. Auf diese Weise lassen sich Assets ermitteln, die übersehen wurden und noch immer lokal ausgeführt werden.

## <a name="secure-and-manage-process-changes"></a>Änderungen am Sicherungs- und Verwaltungsprozess

Prozesse für Sicherung und Verwaltung sollten durch diese Umfangserweiterung nicht verändert werden.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur [Checkliste für bewährte Migrationsmethoden](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für bewährte Migrationsmethoden](./index.md)
