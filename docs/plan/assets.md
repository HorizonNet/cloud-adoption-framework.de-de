---
title: Ausrichten von Ressourcen auf priorisierte Workloads
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Ressourcen auf Ihre priorisierten Workloads ausrichten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 65d1ac327bc5a36e1dca12ab121825751be3b53f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214241"
---
# <a name="align-assets-to-prioritized-workloads"></a>Ausrichten von Ressourcen auf priorisierte Workloads

Workload ist eine konzeptionelle Beschreibung einer Sammlung von Ressourcen: Virtuelle Computer, Anwendungen und Datenquellen. Im vorherigen Artikel zum [Definieren und Priorisieren](./workloads.md) wurde ein Leitfaden zum Erfassen der Daten bereitgestellt, die die Workload definieren. Vor der Migration müssen einige der technischen Eingaben in dieser Liste zusätzlich überprüft werden. Dieser Artikel hilft bei der Validierung der folgenden Eingaben:

- **Anwendungen:** Auflisten aller Anwendungen, die in dieser Workload enthalten sind.
- **VMs und Server:** Auflisten aller virtuellen Computer oder Server, die in der Workload enthalten sind
- **Datenquellen:** Auflisten aller Datenquellen, die in der Workload enthalten sind
- **Abhängigkeiten**: Listen Sie alle Ressourcenabhängigkeiten auf, die nicht in der Workload enthalten sind.

Es gibt eine Reihe von Optionen, um diese Daten zusammenzustellen. Im Folgenden sind einige der gebräuchlichsten Ansätze aufgeführt.

## <a name="alternative-inputs-migrate-modernize-innovate"></a>Alternative Eingaben: Migration, Modernisierung, Innovation

Das Ziel dieser vorhergehenden Datenpunkte ist es, den relativen technischen Aufwand und die Abhängigkeiten als Hilfe für die Priorisierung zu erfassen. Je nach gewünschtem Übergang müssen Sie möglicherweise alternative Datenpunkte sammeln, um eine ordnungsgemäße Priorisierung zu ermöglichen.

**Migration:** Für den reinen Migrationsaufwand dienen die bestehenden Bestands- und Ressourcenabhängigkeiten als angemessenes Maß für die relative Komplexität.

**Modernisierung:** Wenn das Ziel einer Workload darin besteht, Anwendungen oder andere Ressourcen zu modernisieren, sind diese Datenpunkte weiterhin solide Maßstäbe der Komplexität. Es könnte jedoch sinnvoll sein, der Workloaddokumentation eine Eingabe für Modernisierungsmöglichkeiten hinzuzufügen.

**Innovation:** Wenn sich die Daten oder die Geschäftslogik während einer Cloudeinführung erheblich ändern, gilt dies als _innovative_ Art der Transformation. Dasselbe gilt, wenn Sie neue Daten oder eine neue Geschäftslogik erstellen. Für alle Innovationsszenarien wird die Migration von Ressourcen wahrscheinlich den geringsten Aufwand erfordern. Für diese Szenarien sollte das Team eine Reihe von technischen Dateneingaben entwickeln, um die relative Komplexität zu messen.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate bietet eine Reihe von Gruppierungsfunktionen, die die Aggregation von Anwendungen, VMs, Datenquellen und Abhängigkeiten beschleunigen können. Nachdem die Workloads konzeptionell definiert wurden, können sie als Grundlage für die Gruppierung von Ressourcen auf Basis der Abhängigkeitszuordnung verwendet werden.

Die Azure Migrate-Dokumentation bietet eine Anleitung zum [Gruppieren von Computern auf Basis von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies).

## <a name="configuration-management-database"></a>Datenbank für Konfigurationsverwaltung

Einige Organisationen verfügen im Rahmen ihrer bestehenden Tools zur Vorgangsverwaltung über eine gut gepflegte CMDB (Datenbank für die Konfigurationsverwaltung). Sie könnten die CMDB alternativ verwenden, um die zuvor diskutierten Eingabedatenpunkte bereitzustellen.

## <a name="next-steps"></a>Nächste Schritte

[Überprüfen der Rationalisierungsentscheidungen](./review-rationalization.md), die auf Ressourcenausrichtung und Workloaddefinitionen basieren

> [!div class="nextstepaction"]
> [Überprüfen der Rationalisierungsentscheidungen](./review-rationalization.md)
