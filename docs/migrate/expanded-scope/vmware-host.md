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
ms.openlocfilehash: b09c1dcbb36e5f630ca0ae86c95c5c874e29d60b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558608"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Beschleunigen der Migration mit VMware-Hosts

Durch das Migrieren vollständiger VMware-Hosts können mehrere Workloads und Ressourcen in einer Migration verschoben werden. Die folgende Anleitung erweitert den Umfang des [Azure-Migrationsleitfadens](../azure-migration-guide/index.md) durch die Migration von VMware-Hosts.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Die meisten Aufgaben dieser Umfangserweiterung finden in den Vorgängen zum Erfüllen von Voraussetzungen und in den Migrationsprozessen einer Migration statt.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Bei der Migration Ihres ersten VMware-Hosts zu Azure müssen einige Voraussetzungen erfüllt sein, um die Identitäts-, Netzwerk- und Verwaltungsanforderungen vorzubereiten. Sobald diese Voraussetzungen erfüllt sind, sollte für jeden zusätzlichen Host erheblich weniger Aufwand für die Migration erforderlich sein. Diese Voraussetzungen beziehen sich auf einige wichtige Maßnahmen: Sichern der Azure-Umgebung, Verwaltung der privaten Cloud und private Cloudnetzwerke.

### <a name="secure-your-azure-environment"></a>Sichern der Azure-Umgebung

Implementieren Sie die geeignete Cloudlösung für RBAC und Netzwerkkonnektivität in ihrer Azure-Umgebung. Der [Leitfaden zum Sichern Ihrer Umgebung](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) kann bei dieser Implementierung hilfreich sein.

### <a name="private-cloud-management"></a>Verwaltung von privaten Clouds

Es gibt zwei erforderliche Aufgaben und eine optionale Aufgabe zum Einrichten der Verwaltung der privaten Cloud. Das [Eskalieren von Berechtigungen der privaten Cloud](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) und das [Einrichten von Workload-DNS und -DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) sind beides erforderliche bewährte Methoden.

Wenn das Ziel darin besteht, [Workloads mithilfe von Layer-2-Stretingnetzwerken zu migrieren](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), ist diese dritte bewährte Methode erforderlich.

### <a name="private-cloud-networking"></a>Private Cloudnetzwerke

Sobald die Verwaltungsanforderungen festgelegt wurden, kann das private Cloudnetzwerk unter Verwendung der folgenden bewährten Methoden eingerichtet werden:

- [VPN-Verbindung mit privater Cloud](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Lokale Netzwerkverbindung mit ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Virtual Network-Verbindung mit ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurieren der DNS-Namensauflösung](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integration in den Cloud Adoption-Plan

Nachdem die Voraussetzungen erfüllt sind, muss jeder VMware-Host in den [Cloud Adoption-Plan](../../plan/template.md) eingeschlossen werden. Fügen Sie im Cloud Adoption-Plan jeden zu migrierenden Host als [individuelle Workload](../../plan/workloads.md) hinzu. In jeder Workload können die zu migrierenden VMs als [Ressourcen](../../plan/workloads.md)hinzugefügt werden. Um Workloads und Ressourcen in den Cloud Adoption-Plan durch Massenhinzufügen einzubinden, lesen Sie [Hinzufügen und Bearbeiten von Arbeitselementen mit Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Während jeder Iteration arbeitet das Cloud Adoption-Team das Backlog auf, um die Workloads mit der höchsten Priorität zu migrieren. Der Prozess ändert sich für VMWare-Hosts nicht wirklich. Wenn die nächste Workload im Backlog ein VMware-Host ist, ist die einzige Änderung das verwendete Tool.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

Im Folgenden finden Sie einige Beispiele für die Tools, die im Rahmen der Migrationsmaßnahmen eingesetzt werden können:

- [Native VMware-Tools](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Alternativ können Workloads durch ein Notfallwiederherstellungs-Failover mithilfe der folgenden Tools migriert werden:

- [Sichern von virtuellen Workloadcomputern](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurieren einer privaten Cloud als Standort für die Notfallwiederherstellung mithilfe von Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurieren einer privaten Cloud als Standort für die Notfallwiederherstellung mithilfe von VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur [Checkliste für erweiterten Umfang](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
