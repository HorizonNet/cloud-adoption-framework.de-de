---
title: Beschleunigen der Migration mit VMware-Hosts
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beschleunigen der Migration mit VMware-Hosts
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 724a227407f431e08b5344dfd1280397bfca9b65
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566882"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Beschleunigen der Migration mit VMware-Hosts

Durch das Migrieren vollständiger VMware-Hosts können mehrere Workloads und Ressourcen in einer Migration verschoben werden. Die folgende Anleitung erweitert den Umfang des [Azure-Migrationsleitfadens](../azure-migration-guide/index.md) durch die Migration von VMware-Hosts. Die meisten Aufgaben dieser Umfangserweiterung finden in den Vorgängen zum Erfüllen von Voraussetzungen und in den Migrationsprozessen einer Migration statt.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Bei der Migration Ihres ersten VMware-Hosts zu Azure müssen Sie einige Voraussetzungen erfüllen, um die Identitäts-, Netzwerk- und Verwaltungsanforderungen vorzubereiten. Sobald diese Voraussetzungen erfüllt sind, sollte für jeden zusätzlichen Host erheblich weniger Aufwand für die Migration erforderlich sein. Ausführlichere Informationen zu diesen Voraussetzungen finden Sie in den folgenden Abschnitten.

### <a name="secure-your-azure-environment"></a>Sichern der Azure-Umgebung

Implementieren Sie die geeignete Cloudlösung für rollenbasierte Zugriffssteuerung und Netzwerkkonnektivität in ihrer Azure-Umgebung. Der [Leitfaden zum Sichern Ihrer Umgebung](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) kann bei dieser Implementierung hilfreich sein.

### <a name="private-cloud-management"></a>Verwaltung von privaten Clouds

Es gibt zwei erforderliche Aufgaben und eine optionale Aufgabe zum Einrichten der Verwaltung der privaten Cloud. Das [Eskalieren von Berechtigungen der privaten Cloud](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) und das [Einrichten von Workload-DNS und -DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) sind beides erforderliche bewährte Methoden.

Wenn das Ziel darin besteht, [Workloads mithilfe von Layer-2-Stretchingnetzwerken zu migrieren](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), ist diese dritte bewährte Methode auch erforderlich.

### <a name="private-cloud-networking"></a>Private Cloudnetzwerke

Sobald die Verwaltungsanforderungen festgelegt sind, können Sie das private Cloudnetzwerk unter Verwendung der folgenden bewährten Methoden einrichten:

- [VPN-Verbindung mit privater Cloud](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Lokale Netzwerkverbindung mit ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Virtual Network-Verbindung mit ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurieren der DNS-Namensauflösung](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integration in den Cloud Adoption-Plan

Nachdem Sie die sonstigen Voraussetzungen erfüllt haben, sollten Sie jeden VMware-Host in den [Cloudeinführungsplan](../../plan/template.md) einschließen. Fügen Sie im Cloud Adoption-Plan jeden zu migrierenden Host als [individuelle Workload](../../plan/workloads.md) hinzu. Fügen Sie in jeder Workload die zu migrierenden VMs als [Ressourcen](../../plan/workloads.md) hinzu. Um Workloads und Ressourcen durch Massenhinzufügen in den Einführungsplan einzubinden, lesen Sie [Hinzufügen und Bearbeiten von Arbeitselementen mit Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Während jeder Iteration arbeitet das Cloud Adoption-Team das Backlog auf, um die Workloads mit der höchsten Priorität zu migrieren. Der Prozess ändert sich für VMware-Hosts nicht wirklich. Wenn die nächste Workload im Backlog ein VMware-Host ist, ist die einzige Änderung das verwendete Tool.

Zur Migration können Sie die folgenden Tools verwenden:

- [Native VMware-Tools](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Alternativ können Sie Workloads durch ein Notfallwiederherstellungs-Failover mithilfe der folgenden Tools migrieren:

- [Sichern von virtuellen Workloadcomputern](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurieren einer privaten Cloud als Standort für die Notfallwiederherstellung mithilfe von Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurieren einer privaten Cloud als Standort für die Notfallwiederherstellung mithilfe von VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur Checkliste für erweiterten Umfang zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
