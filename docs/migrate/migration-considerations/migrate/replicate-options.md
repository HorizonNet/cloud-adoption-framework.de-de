---
title: Replikationsoptionen
description: Ein Prozess innerhalb der Cloudmigration, der sich auf die Aufgaben der Migration von Workloads in die Cloud konzentriert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: bf798a816d799ba856d8ea20b999de1240ac5284
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802139"
---
# <a name="replication-options"></a>Replikationsoptionen

Vor einer Migration müssen Sie sicherstellen, dass primäre Systeme sicher sind und ohne Probleme weiter ausgeführt werden. Ausfallzeiten bedeuten immer Unterbrechungen für Benutzer oder Kunden und kosten Zeit und Geld. Bei einer Migration ist es nicht damit getan, einfach die lokalen virtuellen Computer nach Azure zu kopieren und dann auszuschalten. Migrationstools müssen asynchrone und synchrone Replikationsvorgänge berücksichtigen, um sicherzustellen, dass Livesysteme ohne jede Ausfallzeit nach Azure kopiert werden können. Das Wichtigste ist: Die Systeme müssen auf dem gleichen Stand gehalten werden wie ihre lokalen Pendants. Es empfiehlt sich, migrierte Ressourcen auf Azure in isolierten Partitionen zu testen, um die erwartungsgemäße Funktionsweise der Workloads sicherzustellen.

Im Cloud Adoption Framework wird davon ausgegangen, dass Azure Migrate (oder Azure Site Recovery) das am besten geeignete Tool für die Replikation von Assets in die Cloud ist. Es gibt jedoch auch andere Optionen. Dieser Artikel erläutert diese Optionen, um die Entscheidungsfindung zu erleichtern.

## <a name="azure-site-recovery-also-known-as-azure-migrate"></a>Azure Site Recovery (auch als Azure Migrate bezeichnet)

[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) orchestriert und verwaltet die Notfallwiederherstellung für Azure-VMs, lokale virtuelle Computer und physische Server. Sie können Site Recovery auf verwenden, um die Migration lokaler Computer und anderer Cloudanbieter nach Azure zu verwalten. Replizieren Sie lokale Computer in Azure oder Azure-VMs in eine sekundäre Region. Dann führen Sie für die VM ein Failover vom primären an den sekundären Standort aus und schließen den Migrationsprozess ab. Mit Azure Site Recovery können Sie verschiedene Migrationsszenarien umsetzen:

- **Migrieren vom lokalen Standort nach Azure**: Migrieren Sie lokale VMware-VMs, Hyper-V-VMs und physische Server nach Azure. Hierzu führen Sie fast die gleichen Schritte wie bei einer vollständigen Notfallwiederherstellung durch. Sie führen allerdings kein Failback der Computer von Azure an den lokalen Standort aus.
- **Migrieren zwischen Azure-Regionen**: Migrieren Sie Azure-VMs von einer Azure-Region in eine andere. Nach Abschluss der Migration konfigurieren Sie die Notfallwiederherstellung für die Azure-VMs, die sich jetzt in der sekundären Region befinden, dem Migrationsziel.
- **Migrieren aus einer anderen Cloud nach Azure**: Sie können Ihre Compute-Instanzen, die bei anderen Cloudanbietern bereitgestellt wurden, zu Azure-VMs migrieren. Für Migrationszwecke behandelt Site Recovery diese Instanzen als physische Server.

![Azure Site Recovery](../../../_images/migrate/asr-replication-image.png)
*Verlagern von Assets nach Azure oder in andere Clouds durch Azure Site Recovery*

Nachdem Sie die lokale und Cloudinfrastruktur im Hinblick auf die Migration bewertet haben, trägt Azure Site Recovery durch Replizieren lokaler Computer zu Ihrer Migrationsstrategie bei. Mit den folgenden einfachen Schritten können Sie die Migration von lokalen VMs, physischen Servern und Cloud-VM-Instanzen nach Azure einrichten:

- Vergewissern Sie sich, dass die Voraussetzungen erfüllt sind.
- Bereiten Sie die Azure-Ressourcen vor.
- Bereiten Sie die lokalen VM- oder Cloudinstanzen auf die Migration vor.
- Stellen Sie einen Konfigurationsserver bereit.
- Aktivieren Sie die Replikation für VMs.
- Führen Sie ein Testfailover aus, um sicherzustellen, dass alles richtig funktioniert.
- Führen Sie ein einmaliges Failover nach Azure aus.

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Dieser Dienst verringert die Komplexität Ihrer Cloudmigration, da Sie nur einen einzigen umfassenden Dienst statt verschiedener Tools benötigen. [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) ist als nahtlose End-to-End-Lösung für die Migration von lokalen SQL Server-Datenbanken in die Cloud konzipiert. Es handelt sich um einen vollständig verwalteten Dienst, der die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen mit minimaler Ausfallzeit ermöglicht. Der Dienst integriert einige Funktionen vorhandener Tools und Dienste und bietet Kunden eine umfassende, hochverfügbare Lösung.

Der Dienst verwendet den Datenmigrations-Assistenten, um Bewertungsberichte zu generieren, die Empfehlungen bezüglich der Änderungen enthalten, die vor einer Migration erforderlich sind. Sie müssen ggf. entsprechende Aufgaben durchführen. Wenn Sie bereit sind, den Migrationsprozess zu starten, führt Azure Database Migration Service alle entsprechenden Schritte aus. Sie können den Prozess starten und müssen sich nicht weiter um Ihre Migrationsprojekte kümmern, da Sie sich darauf verlassen können, dass die Migration mit den von Microsoft bestimmten bewährten Methoden erfolgt.

## <a name="next-steps"></a>Nächste Schritte

Nach Abschluss der Replikation können die [Stagingaktivitäten](./stage.md) beginnen.

> [!div class="nextstepaction"]
> [Stagingaktivitäten während einer Migration](./stage.md)
