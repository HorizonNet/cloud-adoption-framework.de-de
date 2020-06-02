---
title: Verbessern des Betriebs von Zielzonen
description: Verbessern des Betriebs von Zielzonen
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1e338974e3720609640b23e7123fc003801cb371
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756514"
---
# <a name="improve-landing-zone-operations"></a>Verbessern des Betriebs von Zielzonen

Zielzonenvorgänge bilden die anfängliche Grundlage für das Operations Management. Mit der Skalierung der Vorgänge werden diese Verbesserungen die Zielzonen so umgestalten, dass sie den wachsenden Anforderungen an erstklassige Betriebsprozesse, Zuverlässigkeit und Leistung gerecht werden.

## <a name="landing-zone-operations-best-practices"></a>Bewährte Methoden für den Betrieb von Zielzonen

Die folgenden Links bieten bewährte Methoden zur Verbesserung des Betriebs von Zielzonen.

- [Azure-Serververwaltung](../../manage/azure-server-management/index.md): Ein Onboardingleitfaden für die Integration der cloudbasierten Tools und Dienste, die zur Verwaltung des Betriebs erforderlich sind.
- [Hybridüberwachung](../../manage/monitor/index.md): Viele Kunden haben bereits eine beträchtliche Investition in System Center Operations Manager getätigt. Diesen Kunden kann dieser Leitfaden zur Hybridüberwachung helfen, die cloudnativen Berichtstools mit den Operations Manager-Tools zu vergleichen und gegenüberzustellen. Dieser Vergleich erleichtert die Entscheidung, welche Tools für die Betriebsverwaltung eingesetzt werden sollen.
- [Zentralisieren von Verwaltungsvorgängen](../../manage/centralize-operations.md): Verwenden Sie Azure Lighthouse, um das Operations Management für mehrere Azure-Mandanten zu zentralisieren.
- [Einrichten einer Überprüfung der Einsatztauglichkeit](../../manage/operational-fitness-review.md): Überprüfen Sie eine Umgebung auf Einsatztauglichkeit.
- Bewährte Methoden für Workload-spezifische Vorgänge:
  - [Checkliste für Resilienz](https://docs.microsoft.com/azure/architecture/checklist/resiliency-per-service?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Fehlermodusanalyse](https://docs.microsoft.com/azure/architecture/resiliency/failure-mode-analysis?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Wiederherstellung nach einer regionsweiten Dienstunterbrechung](https://docs.microsoft.com/azure/architecture/resiliency/recovery-loss-azure-region?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Wiederherstellung nach Datenbeschädigung oder unbeabsichtigtem Löschen](https://docs.microsoft.com/azure/architecture/framework/resiliency/data-management?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="four-steps-to-improve-operations-beyond-a-single-landing-zone"></a>Vier Schritte zum Verbessern der Vorgänge über eine einzelne Zielzone hinaus

Die [Manage-Methodik](../../manage/index.md) bietet eine allgemeine Anleitung für den Ausbau von Operations Management-Kapazitäten (siehe [Manage-Methodik](../../manage/index.md)). Wir werden die grundlegende Struktur dieser Methodik und die folgenden Schritte aus dieser Methodik verwenden, um den Zielzonenbetrieb und den Betrieb in allen Zielzonen zu verbessern.

<!-- cSpell:ignore caf -->

![Manage-Methodik](../../_images/manage/caf-manage.png)

1. [Einrichten einer Verwaltungsbasislinie](../../manage/azure-server-management/index.md): Eine Verwaltungsbasislinie bildet die Grundlage für das Operations Management. Der Leitfaden in diesem ersten Schritt kann auf jede beliebige Zielzone angewandt werden, um die ersten Vorgänge zu verbessern.
2. [Definieren von geschäftlichen Verpflichtungen](../../manage/considerations/business-alignment.md): Das Verständnis der Wichtigkeit und der Auswirkungen jeder Workload innerhalb einer Zielzone wird eine „Definition of Done“ für alle laufenden Verwaltungsverbesserungen für jede Zielzone festlegen. Im Rahmen dieses Prozesses werden auch die Anforderungen an die Zuverlässigkeit, Leistung und den Betrieb der einzelnen Workloads ermittelt.
3. [Erweitern der Verwaltungsbaseline](../../manage/best-practices.md): Dieser Satz bewährter Methoden kann angewandt werden, um den Betrieb der Zielzone über die ursprüngliche Baseline hinaus zu verbessern.
4. [Erweiterte Vorgänge und Entwurfsprinzipien](../../manage/design-principles.md): Überprüfen Sie den Entwurf und den Betrieb bestimmter Workloads, Plattformen oder kompletter Zielzonen, um eingehendere Anforderungen zu erfüllen.

## <a name="test-driven-development-cycle"></a>Testgesteuerter Entwicklungszyklus

Bevor irgendwelche Sicherheitsverbesserungen in Angriff genommen werden, ist es wichtig, die „Definition of Done“ und alle „Akzeptanzkriterien“ zu verstehen. Weitere Informationen finden Sie in den Artikeln [Testgesteuerte Entwicklung von Zielzonen](./test-driven-development.md) und [Testgesteuerte Entwicklung in Azure](./azure-test-driven-development.md).

![Testgesteuerter Entwicklungsprozess für Cloudzielzonen](../../_images/ready/test-driven-development-process.png)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie die [Verwaltung der Zielzone verbessern können](./landing-zone-governance.md), um die Einführung in großem Stil zu unterstützen.

> [!div class="nextstepaction"]
> [Verbessern der Governance von Zielzonen](./landing-zone-governance.md)
