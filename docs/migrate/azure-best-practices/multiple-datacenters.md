---
title: Mehrere Rechenzentren
description: Mehrere Rechenzentren
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: cafc53ed064db421c213534ce58f6c9581085dde
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88570571"
---
# <a name="multiple-datacenters"></a>Mehrere Rechenzentren

Häufig umfasst ein Migrationsprojekt mehrere Rechenzentren. Die folgende Anleitung erweitert den [Azure-Migrationsleitfaden](../azure-migration-guide/index.md) um Informationen zur Verwendung mehrerer Rechenzentren.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Die meisten hierfür erforderlichen Arbeiten hängen mit der Vorbereitung, Bewertung und Optimierung einer Migration zusammen.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Vor Beginn der Migration müssen im Projektmanagementtool Epics für jedes zu migrierende Rechenzentrum erstellt werden. Jedes Epic stellt ein Rechenzentrum dar. Es ist wichtig, die geschäftlichen Ergebnisse und Beweggründe für diese Migration zu verstehen. Nutzen Sie diese Beweggründe, um die Liste mit den Epics (Rechenzentren) zu priorisieren. Wenn eine Migration z.B. damit begründet wird, dass Rechenzentren verlassen werden sollen, bevor Leasingzeiträume verlängert werden müssen, müssen die Epics basierend auf den Verlängerungsdaten der Leasingverträge priorisiert werden.

In jedem Epic werden die Workloads, die bewertet und migriert werden sollen, als Features verwaltet. Jedes Asset innerhalb dieser Workload wird als User Story verwaltet. Die Arbeiten, die zum Bewerten, Migrieren, Optimieren, Höherstufen, Schützen und Verwalten der einzelnen Assets erforderlich sind, werden als Aufgaben für das jeweilige Asset dargestellt.

Sprints oder Iterationen setzen sich aus einer Reihe von Aufgaben zusammen, die zum Migrieren der Ressourcen und User Storys erforderlich sind, die sich das Cloudeinführungsteam vorgenommen hat. Releases umfassen die Workloads/Features, die in die Produktion hochgestuft werden sollen.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Bei der Umfangserweiterung auf mehrere Rechenzentren hängt die größte Änderung für den Bewertungsprozess mit der präzisen Erfassung und Priorisierung von Workloads und Abhängigkeiten in verschiedenen Rechenzentren zusammen.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

**Evaluieren von rechenzentrumsübergreifenden Abhängigkeiten**: Die [Tools für die Visualisierung von Abhängigkeiten in Azure Migrate](/azure/migrate/concepts-dependency-visualization) helfen bei der Ermittlung von Abhängigkeiten. Die Verwendung dieses Toolsets vor der Migration ist im Allgemeinen eine bewährte Methode. Wenn es aber um globale Komplexität geht, wird diese Verwendung zu einem notwendigen Schritt im Bewertungsprozess. Die Visualisierung durch die [Gruppierung von Abhängigkeiten](/azure/migrate/how-to-create-group-machine-dependencies) kann dabei helfen, die IP-Adressen und Ports aller Assets zu ermitteln, die zur Unterstützung der Workload erforderlich sind.

> [!IMPORTANT]
>
> - Ein Experte, der über Kenntnisse zu Ressourcenplatzierung und IP-Adressschemas verfügt, muss Ressourcen identifizieren, die sich in einem sekundären Rechenzentrum befinden.
> - Evaluieren Sie sowohl Downstreamabhängigkeiten als auch Clients in der Visualisierung, um bidirektionale Abhängigkeiten zu verstehen.

## <a name="migration-process-changes"></a>Änderungen für den Migrationsprozess

Die Migration mehrerer Rechenzentren ähnelt der Konsolidierung von Rechenzentren. Nach der Migration ist die Cloud die einzige Rechenzentrumslösung für mehrere Assets. Die wahrscheinlichste Umfangserweiterung während des Migrationsprozesses ist die Überprüfung und Ausrichtung von IP-Adressen.

### <a name="suggested-action-during-the-migration-process"></a>Empfohlene Aktion während des Migrationsprozesses

Der Erfolg einer Cloudmigration hängt stark von folgenden Aktivitäten ab:

- **Evaluieren von Netzwerkkonflikten**: Wenn Rechenzentren in einem einzelnen Cloudanbieter konsolidiert werden, kommt es wahrscheinlich zu Konflikten (beispielsweise im Zusammenhang mit dem Netzwerk oder mit DNS). Im Zuge der Migration ist es wichtig, Tests für diese Konflikte durchzuführen, um Unterbrechungen bei Produktionssystemen zu vermeiden, die in der Cloud gehostet werden.
- **Aktualisieren von Routingtabellen**: Häufig sind beim Konsolidieren von Netzwerken oder Rechenzentren Änderungen an Routingtabellen erforderlich.

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Während der Optimierung sind möglicherweise weitere Tests erforderlich.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Empfohlene Aktion während des Prozesses der Optimierung und Höherstufung

Führen Sie vor der Höherstufung im Rahmen dieser Umfangserweiterung zusätzliche Testebenen ein. Hierbei muss auf Routingkonflikte und andere Netzwerkkonflikte getestet werden. Darüber hinaus ist es wichtig, die bereitgestellte Anwendung zu isolieren und erneut zu testen, um sicherzustellen, dass alle Abhängigkeiten zur Cloud migriert wurden. In diesem Fall bedeutet Isolierung, die bereitgestellte Umgebung von Produktionsnetzwerken zu trennen. Auf diese Weise lassen sich Assets ermitteln, die übersehen wurden und noch immer lokal ausgeführt werden.

## <a name="secure-and-manage-process-changes"></a>Änderungen am Sicherungs- und Verwaltungsprozess

Schutz- und Verwaltungsprozesse bleiben trotz dieser Umfangserweiterung voraussichtlich unverändert.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur Checkliste zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für bewährte Migrationsmethoden](./index.md)
