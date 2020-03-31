---
title: Cloud Adoption Framework-Migrationsmodell
description: Cloud Adoption Framework-Migrationsmodell
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d238918580c2db808a82c52d67d837a055c033e9
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432577"
---
# <a name="cloud-adoption-framework-migration-model"></a>Cloud Adoption Framework-Migrationsmodell

In diesem Abschnitt des Cloud Adoption Frameworks werden die Prinzipien des Migrationsmodells erläutert. Wo immer dies möglich ist, versuchen diese Inhalte, eine anbieterneutrale Position einzunehmen und Sie durch die Prozesse und Aktivitäten zu führen, die bei jeder Cloudmigration angewendet werden können, unabhängig von Ihrem gewählten Cloudanbieter.

## <a name="understand-migration-motivations"></a>Grundlegendes zu den Beweggründen für die Migration

Die Cloudmigration ist ein Portfolioverwaltungsaufwand, der sich raffiniert als technische Implementierung tarnt. Während des Migrationsprozesses entscheiden Sie sich dafür, einige Ressourcen zu verschieben, in andere zu investieren und veraltete oder ungenutzte Ressourcen außer Betrieb zu nehmen. Einige Ressourcen werden im Rahmen dieses Prozesses optimiert, umgestaltet oder komplett ersetzt. Jede dieser Entscheidungen sollte mit den Beweggründen für Ihre Cloudmigration ausgerichtet sein. Die erfolgreichsten Migrationen gehen auch einen Schritt weiter und richten diese Entscheidungen an den gewünschten Geschäftsergebnissen aus.

Das Migrationsmodell des Cloud Adoption Frameworks hängt davon ab, ob Ihr Unternehmen einen Prozess der Geschäftsbereitschaft für die Cloudeinführung abgeschlossen hat. Stellen Sie sicher, dass Sie die Anleitungen [Plan](../../strategy/index.md) (Planen) und [Ready](../../ready/index.md) (Bereit) im Cloud Adoption Framework gelesen haben, um die geschäftlichen Gründe oder eine andere Rechtfertigung für eine Cloudmigration sowie alle erforderlichen organisatorischen Planungen oder Schulungen zu ermitteln, die erforderlich sind, bevor Sie einen Migrationsprozess in großem Umfang durchführen.

> [!NOTE]
> Obwohl die Geschäftsplanung wichtig ist, ist eine wachstumsorientierte Haltung ebenso wichtig. Parallel zur breit angelegten Geschäftsplanung des Cloudstrategieteams wird empfohlen, dass das Cloudeinführungsteam mit der Migration einer ersten Workload als Vorstufe für breit angelegte Migrationsarbeiten beginnt. Diese anfängliche Migration ermöglicht es dem Team, praktische Erfahrungen mit den geschäftlichen und technischen Problemen einer Migration zu sammeln.

## <a name="envision-an-end-state"></a>Planen des Endzustands

Es ist wichtig, eine grobe Vorstellung von Ihrem Endzustand zu erhalten, bevor Sie mit der Migration beginnen. Das folgende Diagramm zeigt einen lokalen Ausgangspunkt für Infrastruktur, Anwendungen und Daten, der Ihren *digitalen Bestand* definiert. Während des Migrationsprozesses werden diese Ressourcen mit einer der fünf in [Die fünf Phasen der Rationalisierung](../../digital-estate/5-rs-of-rationalization.md) beschriebenen Migrationsstrategien überführt.

![Infografik zu den Migrationsoptionen](../../_images/migrate/migration-options.png)

Die Migration und Modernisierung von Workloads reichen von einfachen Migrationen vom Typ _Zuweisen eines neuen Hosts_ (auch als _Lift & Shift_ bezeichnet) mithilfe von IaaS-Funktionen (Infrastruktur-as-a-Service), die keine Code- und App-Änderungen erfordern, über _Refactoring_-Migrationen mit minimalen Änderungen bis hin zu _Überarbeiten_-Migrationen zum Ändern und Erweitern von Code- und App-Funktionen, um die Vorteile von Cloudtechnologien zu nutzen.

Cloudnative Strategien und PaaS-Strategien (Platform-as-a-Service) *erstellen* lokale Workloads mithilfe von Azure-Plattformangeboten und verwalteten Diensten neu. Workloads, die über gleichwertige, vollständig verwaltete cloudbasierte SaaS-Angebote (Software-as-a-Service) verfügen, können oft vollständig durch diese Dienste im Rahmen des Migrationsprozesses *ersetzt* werden.

> [!NOTE]
> Während der öffentlichen Vorschauversion des Cloud Adoption Frameworks hebt dieser Abschnitt des Frameworks eine „Zuweisen eines neuen Hosts“-Migrationsstrategie hervor. Obwohl PaaS- und SaaS-Lösungen bei Bedarf als Alternativen diskutiert werden, steht die Migration von virtuellen computerbasierten Workloads mit IaaS-Funktionen im Vordergrund.
>
> Andere Abschnitte und zukünftige Iterationen dieser Inhalte werden auf andere Ansätze ausgedehnt. Eine Diskussion auf hoher Ebene über die Erweiterung des Umfangs Ihrer Migration um komplexere Migrationsstrategien finden Sie im Artikel zur Ausgewogenheit des Portfolios.

## <a name="incremental-migration"></a>Inkrementelle Migration

Die Cloud Adoption Framework-Migrationsmodell basiert auf einem inkrementellen Cloudtransformationsprozess. Es wird davon ausgegangen, dass Ihr Unternehmen mit einem anfänglichen Cloudmigrationsaufwand mit begrenztem Umfang beginnt, den wir allgemein als die erste Workload bezeichnen. Diese Bemühungen werden sich iterativ auf weitere Workloads ausweiten, wenn Ihre Betriebsteams die Migrationsprozesse optimieren und verbessern.

Tools für Cloudmigrationen wie [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) können ganze Rechenzentren mit Zehntausenden virtuellen Computern migrieren. Selten können jedoch das Unternehmen und die bestehenden IT-Abteilungen ein so hohes Änderungstempo bewältigen. Daher unterteilen viele Unternehmen einen Migrationsaufwand in mehrere Iterationen, indem sie eine Workload (oder eine Sammlung von Workloads) pro Iteration verschieben.

Die Prinzipien dieses inkrementellen Modells basieren auf der Ausführung von Prozessen und Voraussetzungen, auf die in der folgenden Infografik verwiesen wird.

![Cloud Adoption Framework-Migrationsmodell](../../_images/migrate/methodology.png)

Die konsequente Anwendung dieser Prinzipien stellt ein Endziel für Ihre Cloudmigrationsprozesse dar und sollte nicht als erforderlicher Ausgangspunkt betrachtet werden. Während Ihre Migrationsbemühungen fortschreiten, lesen Sie die Hinweise in diesem Abschnitt, um den besten Prozess zur Unterstützung Ihrer organisatorischen Anforderungen zu definieren.

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der [Untersuchung der Voraussetzungen für die Migration](./prerequisites/index.md), um mehr über dieses Modell zu erfahren.

> [!div class="nextstepaction"]
> [Voraussetzungen für die Migration](./prerequisites/index.md)
