---
title: Schätzen der Cloudkosten vor der Migration
description: Erläuterung des Prozesses zum Schätzen der Cloudkosten vor der Migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0618676a995971951a27a5bdba66b7e9b126d7d6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802581"
---
# <a name="estimate-cloud-costs"></a>Schätzen der Cloudkosten

Während der Migration gibt es mehrere Faktoren, die sich auf Entscheidungen und Ausführungsaktivitäten auswirken können. Um zu verstehen, welche dieser Optionen in verschiedene Situationen am besten geeignet sind, werden in diesem Artikel verschiedene Möglichkeiten für das Schätzen der Cloudkosten erläutert.

## <a name="digital-estate-size"></a>Größe der digitalen Ressourcen

Die Größe Ihrer digitalen Ressourcen wirkt sich direkt auf Migrationsentscheidungen aus. Migrationen, die weniger als 250 virtuelle Computer umfassen, können sehr viel leichter geschätzt werden als eine Migration mit 10.000 oder mehr virtuellen Computern. Es wird dringend empfohlen, eine kleinere Workload für die erste Migration auszuwählen. Dies gibt Ihrem Team die Gelegenheit zu lernen, wie die Kosten für eine einfache Migration geschätzt werden, bevor versucht wird, die Kosten größerer und komplexerer Workloadmigrationen zu schätzen.

Beachten Sie jedoch, dass kleinere Migrationen mit nur einer Workload eine sehr unterschiedliche Menge an unterstützenden Ressourcen umfassen können. Wenn die Migration weniger als 1.000 virtuelle Computer betrifft, ist ein Tool wie [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) wahrscheinlich ausreichend, um Daten zum Bestand zu sammeln und die Kosten zu prognostizieren. Weitere Tooloptionen für die Kostenschätzung sind im Artikel zu [Kostenberechnungen für digitale Ressourcen](../../../digital-estate/calculate.md) beschrieben.

Bei digitalen Ressourcen mit 1.000 Einheiten und mehr ist es möglich, eine Schätzung in vier oder fünf umsetzbare Iterationen aufzuteilen, um den Schätzungsprozess überschaubar zu machen. Bei größeren Ressourcenumgebungen oder wenn ein höheres Maß an Prognosegenauigkeit erforderlich ist, wird wahrscheinlich ein umfassenderer Ansatz erforderlich sein, wie er im Abschnitt [Digitale Ressourcen](../../../digital-estate/index.md) des Framework für die Cloudeinführung beschrieben ist.

## <a name="accounting-models"></a>Kostenrechnungsmodelle

Kostenrechnungsmodelle

Wenn Sie mit herkömmlichen IT-Beschaffungsprozessen vertraut sind, kann Ihnen die Kostenschätzung in der Cloud fremd erscheinen. Bei der Einführung von Cloudtechnologien wechselt der Erwerb von einem festen, strukturierten Investitionskostenmodell zu einem fließenden Betriebskostenmodell. Beim herkömmlichen Investitionskostenmodell versucht das IT-Team, die Kaufkraft für mehrere Workloads über verschiedene Programme zu konsolidieren, um einen Pool gemeinsam genutzter IT-Ressourcen zu zentralisieren, der jede dieser Lösungen unterstützen kann. Beim Betriebskosten-Cloudmodell können Kosten direkt den Unterstützungsanforderungen einzelner Workloads, Teams oder Unternehmenseinheiten zugeordnet werden. Diese Methode ermöglicht eine direktere Zuordnung von Kosten zum unterstützten internen Kunden. Bei der Kostenschätzung muss zunächst klar sein, inwieweit diese neue Kostenrechnungsfunktion vom IT-Team verwendet wird.

Diejenigen, die den traditionellen Investitionskostenansatz für die Kostenrechnung replizieren möchten, verwenden die Ergebnisse einer der beiden Methoden, die im Abschnitt [Größe digitaler Ressourcen](#digital-estate-size) weiter oben vorgeschlagen werden, um eine Jahreskostenbasis zu erhalten. Anschließend werden diese Jahreskosten mit dem üblichen Hardwareaktualisierungszyklus des Unternehmens multipliziert. Der Hardwareaktualisierungszyklus bezeichnet die Rate, mit der ein Unternehmen alternde Hardware ersetzt, und wird in der Regel in Jahren gemessen. Die jährliche Ausführungsrate multipliziert mit dem Hardwareaktualisierungszyklus ergibt eine Kostenstruktur, die einem Investitionskostenmuster ähnelt.

## <a name="next-steps"></a>Nächste Schritte

Nach dem Schätzen der Kosten kann die Migration beginnen. Es ist allerdings ratsam, vor Beginn der Migration die [Partnerschafts- und Supportoptionen](./partnership-options.md) zu überprüfen.

> [!div class="nextstepaction"]
> [Grundlegendes zu Partnerschaftsoptionen](./partnership-options.md)
