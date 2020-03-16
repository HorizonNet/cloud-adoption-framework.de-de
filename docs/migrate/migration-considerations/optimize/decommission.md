---
title: Außerbetriebnahme ausgesonderter Ressourcen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die Außerbetriebnahme ausgesonderter Ressourcen mit minimalen Betriebsunterbrechungen richtig durchführen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a62ef520f948d8bea415e4a65749944b91bb16c8
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092756"
---
# <a name="decommission-retired-assets"></a>Außerbetriebnahme ausgesonderter Ressourcen

Nachdem eine Workload in die Produktionsumgebung hochgestuft wurde, sind die Ressourcen, auf denen die Produktionsworkload zuvor gehostet wurde, nicht mehr zur Unterstützung von Geschäftsvorgängen erforderlich. An diesem Punkt werden die älteren Ressourcen als ausgesondert betrachtet. Ausgesonderte Ressourcen können dann zur Reduzierung der Betriebskosten außer Betrieb genommen werden. Dazu kann einfach die Stromzufuhr zur Ressource abgeschaltet und die Ressource ordnungsgemäß entsorgt werden. Allerdings kann die Außerbetriebnahme von Ressourcen manchmal unerwünschte Folgen haben. Die folgenden Anleitungen können Ihnen helfen, ausgesonderten Ressourcen ordnungsgemäß und mit minimalen Betriebsunterbrechungen außer Betrieb zu nehmen.

## <a name="cost-savings-realization"></a>Realisierung von Kosteneinsparungen

Wenn Kosteneinsparungen die Hauptmotivation für eine Migration sind, ist die Außerbetriebnahme ein wichtiger Schritt. Bis zur Außerbetriebnahme verbraucht eine Ressource weiterhin Strom, erfordert Unterstützung für die Umgebung und benötigt andere Ressourcen, wodurch weitere Kosten verursacht werden. Erst nachdem die Ressource außer Betrieb genommen wurde, können Kosteneinsparungen realisiert werden.

## <a name="continued-monitoring"></a>Fortgesetzte Überwachung

Nachdem eine migrierte Workload hochgestuft wurde, sollten die außer Betrieb zu nehmenden Ressourcen weiterhin überwacht werden, um sicherzustellen, dass kein zusätzlicher Produktionsdatenverkehr an die falschen Ressourcen weitergeleitet wird.

## <a name="testing-windows-and-dependency-validation"></a>Testzeitfenster und Abhängigkeitsüberprüfung

Selbst bei bester Planung können Produktionsworkloads noch Abhängigkeiten von Ressourcen aufweisen, die als ausgesondert gelten. In solchen Fällen kann das Ausschalten einer ausgesonderten Ressource zu unerwarteten Systemfehlern führen. Daher sollte die Beendigung von Ressourcen ebenso konsequent durchgeführt werden wie eine Wartungsaktivität für das System. Es müssen geeignete Test- und Ausfallzeitfenster für die Beendigung der Ressource festgelegt werden.

## <a name="holding-period-and-data-validation"></a>Aufbewahrungszeitraum und Datenüberprüfung

Es ist bei Migrationen nicht ungewöhnlich, dass Daten während des Replikationsprozesses ausgelassen werden. Dies trifft insbesondere auf ältere Daten zu, die nicht regelmäßig verwendet werden. Nachdem eine ausgesonderte Ressource abgeschaltet wurde, ist es ratsam, die Ressource noch eine Weile als temporäre Datensicherung aufzubewahren. Unternehmen sollten mindestens 30 Tage als Aufbewahrungs- und Testzeitraum einplanen, bevor ausgesonderte Ressourcen vernichtet wird.

## <a name="next-steps"></a>Nächste Schritte

Nachdem ausgesonderte Ressourcen außer Betrieb genommen wurden, ist die Migration abgeschlossen. Dies ist eine gute Gelegenheit, den Migrationsprozess zu verbessern, und eine [Retrospektive](./retrospective.md) sorgt dafür, dass das Cloudeinführungsteam das Release noch einmal überprüft, um daraus zu lernen und den Ablauf zu verbessern.

> [!div class="nextstepaction"]
> [Retrospektive](./retrospective.md)
