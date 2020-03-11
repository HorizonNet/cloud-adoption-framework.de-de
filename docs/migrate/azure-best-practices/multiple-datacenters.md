---
title: Mehrere Rechenzentren
description: Mehrere Rechenzentren
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9156df0b76f6edf1d249d5d724e0a5d0f4fd8e15
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78898132"
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

**Evaluieren von rechenzentrumsübergreifenden Abhängigkeiten**: Die [Tools für die Visualisierung von Abhängigkeiten in Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) helfen bei der Ermittlung von Abhängigkeiten. Die Verwendung dieser Tools vor der Migration ist eine allgemeine bewährte Methode. Wenn es aber um globale Komplexität geht, wird diese Verwendung zu einem notwendigen Schritt im Bewertungsprozess. Die Visualisierung durch die [Gruppierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) kann dabei helfen, die IP-Adressen und Ports aller Assets zu ermitteln, die zur Unterstützung der Workload erforderlich sind.

> [!IMPORTANT]
> Zwei wichtige Hinweise: Erstens muss ein Experte, der über Kenntnisse zu Assetplatzierung und IP-Adressschemas verfügt, Assets identifizieren, die sich in einem sekundären Rechenzentrum befinden. Zweitens müssen sowohl Downstreamabhängigkeiten als auch Clients in der Visualisierung evaluiert werden, um bidirektionale Abhängigkeiten zu verstehen.

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Die Migration mehrerer Rechenzentren ähnelt der Konsolidierung von Rechenzentren. Nach der Migration ist die Cloud die einzige Rechenzentrumslösung für mehrere Assets. Die wahrscheinlichste Umfangserweiterung während des Migrationsprozesses ist die Überprüfung und Ausrichtung von IP-Adressen.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

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

Kehren Sie zur [Checkliste für erweiterten Umfang](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
