---
title: Verschieben einer lokalen VMware-Infrastruktur in Azure
description: Hier erfahren Sie, wie Contoso lokale VMware-VMs zu Azure migriert.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 12d83670b5d2c18a14229c2b14373da70c6b84d9
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199273"
---
<!-- docsTest:ignore "Bulk Migration" "Cold Migration" -->

# <a name="move-on-premises-vmware-infrastructure-to-azure"></a>Verschieben einer lokalen VMware-Infrastruktur in Azure

Für die Migration von VMware-VMs von einem lokalen Rechenzentrum zu Azure stehen Contoso mehrere Optionen zur Auswahl.

| Migrationsoptionen | Ergebnis |
| --- | --- |
| [Azure Migrate](https://azure.microsoft.com/services/azure-migrate/) | [Bewerten](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) und [Migrieren](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware) lokaler VMs <br><br> Ausführen von Workloads mit Azure IaaS <br><br> Verwalten von VMs mit [Azure Resource Manager](https://azure.microsoft.com/features/resource-manager/) |
| [Azure VMware Solution](https://azure.microsoft.com/overview/azure-vmware) | Migrieren lokaler VMs mithilfe von VMware HCX oder vMotion <br><br> Ausführen nativer VMware-Workloads auf Azure-Bare-Metal-Hardware <br><br> Verwalten von VMs mit vSphere |

Azure VMware Solution wird verwendet, um eine private Cloud in Azure zu erstellen, die nativen Zugriff auf VMware vCenter und andere von VMware unterstützte Tools für die Workloadmigration hat. Contoso kann Azure VMware Solution dann in dem sicheren Wissen verwenden, dass die Microsoft-Angebote von VMware unterstützt werden.

> [!NOTE]
> In diesem Artikel wird hauptsächlich die Verwendung von Azure VMware Solution (AVS) zum Migrieren von lokalen VMware-VMs zu Azure behandelt.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Team von Contoso definiert in enger Zusammenarbeit mit Geschäftspartnern die geschäftlichen Faktoren, die für eine VMware-Migration zu Azure sprechen. Dazu können folgende Faktoren zählen:

- **Verlegung oder Schließung von Rechenzentren:** Nahtlose Migration von VMware-basierten Workloads, wenn vorhandene Rechenzentren konsolidiert oder außer Betrieb genommen werden.
- **Notfallwiederherstellung und Business Continuity:** Verwendung eines in Azure bereitgestellten VMware-Stapels als primären oder sekundären Standort für die bedarfsgesteuerte Notfallwiederherstellung für die lokale Rechenzentrumsinfrastruktur.
- **Anwendungsmodernisierung:** Nutzung des Azure-Ökosystems zum Modernisieren der Anwendungen von Contoso, ohne VMware-basierte Umgebungen neu erstellen zu müssen.
- **Implementieren von DevOps:** Nutzung von Azure DevOps-Toolketten in VMware-Umgebungen und Modernisierung von Anwendungen im eigenen Tempo.
- **Sicherstellen der Betriebskontinuität:** Erneute Bereitstellung von vSphere-basierten Anwendungen in Azure ohne Hypervisorkonvertierungen und Refactoring von Anwendungen. Erweiterte Unterstützung für ältere Anwendungen unter Windows und SQL Server.

## <a name="vmware-on-premises-to-vmware-in-the-cloud-goals"></a>Ziele für die Migration lokaler VMware-VMs zu VMware in der Cloud

Contoso hat sich unter Berücksichtigung der geschäftlichen Faktoren die folgenden Ziele für die Migration gesetzt:

- Die vorhandenen Umgebungen sollen weiterhin mit VMware-Tools verwaltet werden, die den Teams vertraut sind, und gleichzeitig sollen die Anwendungen mit nativen Azure-Diensten modernisiert werden.
- Die VMware-basierten Workloads von Contoso sollen nahtlos vom Rechenzentrum zu Azure migriert werden, und die VMware-Umgebung soll in Azure integriert werden.
- Nach der Migration soll die Anwendung in Azure die gleichen Leistungsmerkmale aufweisen wie gegenwärtig in der lokalen VMware-Umgebung. Die Anwendung bleibt lokal und in der Cloud gleichermaßen wichtig.

Diese Ziele bestätigen, dass AVS die beste Migrationsmethode für Contoso ist, und stützen die Entscheidung für die Verwendung des Diensts.

## <a name="benefits-of-running-vmware-workloads-in-azure"></a>Vorteile der Ausführung von VMware-Workloads in Azure

Mit Azure VMware Solution (AVS) kann Contoso Anwendungen jetzt in VMware-Umgebungen und Azure mit einem einheitlichen Betriebsframework nahtlos ausführen, verwalten und sichern.

Contoso kann bereits getätigte Investitionen in VMware sowie vorhandene Qualifikationen und Tools nutzen (darunter VMware vSphere, vSAN und vCenter) und gleichzeitig von den Skalierungsmöglichkeiten, der Leistung und den Innovationen von Azure profitieren. Folgende weitere Vorteile sind möglich:

- Eine VMware-Infrastruktur kann innerhalb weniger Minuten in der Cloud bereitgestellt werden, und Anwendungen können im eigenen Tempo modernisiert werden.
- VMware-Anwendungen können durch die Verwendung einer dedizierten, isolierten leistungsfähigen Infrastruktur sowie spezifischer Azure-Produkte und -Dienste erweitert werden.
- Lokale VMs können ohne Refactoring von Anwendungen zu Azure migriert oder auf Azure erweitert werden.
- Auf der globalen Azure-Infrastruktur können VMware-Workloads skaliert, automatisiert und schnell bereitgestellt werden.
- Azure VMware Solution wird von Microsoft bereitgestellt, von VMware überprüft und auf der Azure-Infrastruktur ausgeführt.

## <a name="solutions-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess.

### <a name="current-architecture"></a>Aktuelle Architektur

- In einem lokalen Rechenzentrum bereitgestellte VMs, die mit [vSphere](https://www.vmware.com/products/vsphere.html) verwaltet werden
- In einem VMware-ESXi-Hostcluster bereitgestellte Workloads, die mit [vCenter](https://www.vmware.com/products/vcenter-server.html), [vSAN](https://www.vmware.com/products/vsan.html) und [NSX](https://www.vmware.com/products/nsx.html) verwaltet werden

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Bereitstellen einer [privaten AVS-Cloud](https://docs.microsoft.com/azure/azure-vmware/concepts-private-clouds-clusters) in der Azure-Region `West US`
- Herstellen einer Verbindung zwischen dem lokalen Rechenzentrum und dem in `West US` ausgeführten AVS-Dienst mithilfe von virtuellen Netzwerken und [ExpressRoute](https://docs.microsoft.com/azure/azure-vmware/concepts-networking) mit Aktivierung von Global Reach
- Migrieren von VMs zu einer dedizierten Azure VMware Solution-Instanz mithilfe von [VMware Hybrid Cloud Extension (HCX)](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-D0CD0CC6-3802-42C9-9718-6DA5FEC246C6.html).

![Vorgeschlagene Architektur](./media/contoso-migration-vmware-to-azure/on-premises-stretched-network-expressroute.png)

## <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Bare-Metal-VMware-Hochleistungsinfrastruktur. Die Infrastruktur ist ausschließlich für Contoso bestimmt und physisch von der Infrastruktur anderer Kunden isoliert. <br><br> Da Contoso einen neuen Host mit VMware zuweist, ist weder eine besondere Konfiguration erforderlich noch ist die Migration besonders komplex. <br><br> Mit dem [Azure-Hybridvorteil](https://azure.microsoft.com/pricing/hybrid-benefit/) und [erweiterten Sicherheitsupdates](https://www.microsoft.com/cloud-platform/windows-server-2008) für ältere Windows- und SQL-Plattformen kann Contoso seine Investition in die Software Assurance nutzen. <br><br> Contoso behält die vollständige Kontrolle über die Anwendungs-VMs in Azure. <br><br> |
| **Nachteile** | Contoso muss die Anwendung weiterhin als VMware-VMs unterstützen, anstatt sie auf einen verwalteten Dienst wie Azure App Service und Azure SQL-Datenbank umzustellen. <br><br> Für die Bereitstellung und Abrechnung von Azure VMware Solution werden keine einzelnen VMs in Azure IaaS, sondern mindestens drei großen Knoten zugrunde gelegt. Contoso muss seine Kapazitätsanforderungen wie in der lokalen Umgebung planen und kann nicht vom On-Demand-Charakter anderer Dienste in Azure profitieren. |

> [!NOTE]
> Informieren Sie sich über die [Preise](https://azure.microsoft.com/pricing/details/azure-vmware/) von Azure VMware Solution.

## <a name="migration-process"></a>Migrationsprozess

Contoso migriert VMs mit dem VMware HCX-Tool zu AVS. Die VMs werden in einer privaten AVS-Cloud ausgeführt.  Zu den [VMware HCX-Migrationstypen](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-8A31731C-AA28-4714-9C23-D9E924DBB666.html) zählen die Massenmigration, die kalte Migration und sogar die Livemigration einer ausgeführten Workload mit vMotion oder Replication Assisted vMotion (RAV).

- Contoso plant sein Netzwerk in Azure und ExpressRoute.
- Contoso erstellt die private AVS-Cloud über das Azure-Portal.
- Anschließend werden das Netzwerk sowie die ExpressRoute-Leitungen konfiguriert.
- Danach konfiguriert Contoso die HCX-Komponenten für die Verbindung zwischen der lokalen vSphere-Umgebung und der privaten AVS-Cloud.
- Die VMs werden dann repliziert und mithilfe von VMware HCX zu Azure migriert.

 ![Migrationsprozess](./media/contoso-migration-vmware-to-azure/on-premises-vmware-hcx-azure.png)

## <a name="scenarios-steps"></a>Schritte für das Szenario

1. Netzwerkplanung
1. Erstellen einer privaten AVS-Cloud
1. Konfigurieren der Netzwerkeinstellungen
1. Migrieren von VMs mithilfe von HCX

### <a name="step-1-network-planning"></a>Schritt 1: Netzwerkplanung

Contoso muss sein Netzwerk planen, einschließlich Microsoft Azure Virtual Network und der Konnektivität zwischen der lokalen Infrastruktur und Azure. Contoso benötigt eine Hochgeschwindigkeitsverbindung zwischen den lokalen und Azure-basierten Umgebungen sowie eine Verbindung mit der privaten AVS-Cloud.

Diese Konnektivität wird über Azure ExpressRoute bereitgestellt und erfordert bestimmte Netzwerkadressbereiche und Firewallports, um die Dienste zu aktivieren. Diese Verbindung mit hoher Bandbreite und geringen Wartezeiten ermöglicht den Benutzern bei Contoso den Zugriff auf Dienste, die in ihrem Azure-Abonnement in der privaten AVS-Cloudumgebung ausgeführt werden.

Contoso muss ein IP-Adressschema mit einem nicht überlappenden Adressraum für die [virtuellen Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) planen. Für das [ExpressRoute-Gateway](https://docs.microsoft.com/azure/expressroute/expressroute-about-virtual-network-gateways) müssen sie ein Gatewaysubnetz hinzufügen.

Die private AVS-Cloud wird über eine weitere Azure ExpressRoute-Verbindung mit der Azure Virtual Network-Instanz von Contoso verbunden. Der Global Reach-Dienst von ExpressRoute wird aktiviert, um eine [direkte Verbindung](https://docs.microsoft.com/azure/azure-vmware/concepts-networking#on-premises-interconnectivity) zwischen der lokalen Umgebung und in der privaten AVS-Cloud ausgeführten VMs zuzulassen. Zum Aktivieren von Global Reach ist die ExpressRoute-Premium-SKU ist erforderlich.

![ExpressRoute Global Reach mit AVS](./media/contoso-migration-vmware-to-azure/adjacency-overview-drawing-double.png)

Private AVS-Clouds erfordern mindestens einen `/22`-CIDR-Netzwerkadressblock für Subnetze. Für die Verbindungsherstellung mit lokalen Umgebungen und virtuellen Netzwerken darf der Netzwerkadressblock keine Überlappung aufweisen.

>[!NOTE]
> In diesem [Tutorial](https://docs.microsoft.com/azure/azure-vmware/tutorial-network-checklist/) erfahren Sie mehr über die Netzwerkplanung für AVS.

### <a name="step-2-create-an-avs-private-cloud"></a>Schritt 2: Erstellen einer privaten AVS-Cloud

Nachdem die Planung des Netzwerks und der IP-Adressen abgeschlossen ist, konzentriert sich Contoso auf die Bereitstellung des AVS-Diensts in der Azure-Region „USA, Westen“. AVS ermöglicht Contoso das Bereitstellen eines vSphere-Clusters in Azure.

Eine private AVS-Cloud ist ein isoliertes softwaredefiniertes VMware-Rechenzentrum, das ESXi-Hosts, vCenter, vSAN und NSX unterstützt. Der Stapel wird auf dedizierten und isolierten Bare-Metal-Hardwareknoten in einer Azure-Region ausgeführt. Die anfängliche Bereitstellung für eine private AVS-Cloud muss mindestens drei Hosts umfassen. Später können nacheinander weitere Host hinzugefügt werden. Pro Cluster sind bis zu 16 Hosts möglich.

>[!NOTE]
> Informieren Sie sich über die [Konzepte der privaten AVS-Cloud](https://docs.microsoft.com/azure/azure-vmware/concepts-private-clouds-clusters).

Private AVS-Clouds werden über das AVS-Portal verwaltet. Sie verfügen über eine eigene vCenter Server-Instanz in einer eigenen Verwaltungsdomäne.

>[!NOTE]
> In diesem [Tutorial](https://docs.microsoft.com/azure/azure-vmware/tutorial-create-private-cloud) erfahren Sie, wie Sie private AVS-Clouds erstellen.

- Zunächst registriert Contoso den AVS-Anbieter mit dem folgenden Befehl in Azure.

```bash
az provider register -n Microsoft.AVS --subscription <your subscription ID>
```

- Im Azure-Portal gibt das Contoso-Team die Netzwerkinformationen aus seinem Plan an, um die private AVS-Cloud zu erstellen.

![Erstellen einer privaten AVS-Cloud](./media/contoso-migration-vmware-to-azure/create-private-cloud.png)

> [!NOTE]
> Dieser Schritt dauert etwa zwei Stunden.

- Das Contoso-Team überprüft, ob die Bereitstellung der privaten AVS-Cloud abgeschlossen wurde, indem es zur Ressourcengruppe navigiert und die private Cloudressource auswählt. Wenn die Bereitstellung abgeschlossen ist, wird der Status **Erfolgreich** angezeigt.

![Überprüfen der Bereitstellung der privaten Cloud](./media/contoso-migration-vmware-to-azure/validate-deployment.png)

### <a name="step-3-configure-networking"></a>Schritt 3: Konfigurieren der Netzwerkeinstellungen

Eine private Azure VMware Solution (AVS)-Cloud erfordert ein virtuelles Netzwerk (VNET). Da AVS Ihr lokales vCenter in der Vorschauversion nicht unterstützt, müssen Sie zusätzliche Schritte für die Integration in Ihre lokale Umgebung durchführen. Durch die Einrichtung einer ExpressRoute-Leitung und eines Gateways für virtuelle Netzwerke werden die virtuellen Netzwerke mit der privaten AVS-Cloud verbunden.

>[!NOTE]
> In diesem [Tutorial](https://docs.microsoft.com/azure/azure-vmware/tutorial-configure-networking) erfahren Sie mehr über die Konfiguration des Netzwerks für AVS.

- Contoso erstellt zunächst ein virtuelles Netzwerk mit einem Gatewaysubnetz.

> [!IMPORTANT]
> Contoso muss einen Adressraum verwenden, der sich **nicht** mit dem beim Erstellen der privaten Cloud verwendeten Adressraum überlappt.

- Als Nächstes erstellt Contoso unter Auswahl der korrekten SKU das ExpressRoute-VPN-Gateway.

![ExpressRoute-VPN-Gateway](./media/contoso-migration-vmware-to-azure/create-virtual-network-gateway.png)

- Contoso benötigt den Autorisierungsschlüssel, um ExpressRoute mit dem virtuellen Netzwerk zu verbinden. Der Schlüssel wird im Azure-Portal auf dem Bildschirm „Konnektivität“ der privaten AVS-Cloudressource angezeigt.

![ER-Authentifizierungsschlüssel](./media/contoso-migration-vmware-to-azure/request-auth-key.png)

- Zum Schluss verbindet Contoso ExpressRoute mit dem VPN-Gateway, das die private AVS-Cloud mit dem virtuellen Netzwerk verbindet. Hierzu wird eine Verbindung in Azure erstellt.

![Verbinden von ExpressRoute mit dem VNET](./media/contoso-migration-vmware-to-azure/add-connection.png)

>[!NOTE]
> In diesem [Tutorial](https://docs.microsoft.com/azure/azure-vmware/tutorial-access-private-cloud) erfahren Sie, wie Sie auf die private Cloud zugreifen und eine Verbindung mit vSphere herstellen.

### <a name="step-4-migrate-using-vmware-hcx"></a>Schritt 4: Migrieren mithilfe von VMware HCX

Um VMware-VMs mithilfe von HCX zu Azure zu migrieren, muss Contoso folgende allgemeine Schritte ausführen:

- Installieren und Konfigurieren von VMware HCX
- Durchführen der Migrationen zu Azure mithilfe von HCX

>[!NOTE]
> In diesem [Tutorial](https://docs.microsoft.com/azure/azure-vmware/hybrid-cloud-extension-installation) erfahren Sie, wie Sie HCX für AVS installieren.

<!-- docsTest:ignore L2 -->

#### <a name="install-and-configure-vmware-hcx-for-public-cloud"></a>Installieren und Konfigurieren von VMware HCX für die öffentliche Cloud

[VMware HCX](https://cloud.vmware.com/vmware-hcx) ist ein VMware-Produkt, das Teil der Standardinstallation von Azure VMware Solution ist. Standardmäßig wird HCX Advanced installiert. Wenn mehr Features benötigt werden, ist jedoch ein Upgrade auf HCX Enterprise möglich. AVS automatisiert die Cloud Manager-Komponente von HCX in AVS und stellt die Aktivierungsschlüssel des Kunden sowie einen Downloadlink zur Connector-HCX-Appliance bereit, die lokal und in der vCenter-Domäne des Kunden konfiguriert werden muss. Nachdem diese dann mit der AVS-Cloudappliance gekoppelt wurden, können Kunden Dienste wie Migration und L2-Stretching nutzen.

- Contoso stellt HCX mit einer von VMware zur Verfügung gestellten OVA-Vorlage bereit.

![HCX-OVA-Vorlage](./media/contoso-migration-vmware-to-azure/configure-template.png)

Informationen zum Konfigurieren von HCX für Ihre private AVS-Cloud finden Sie in diesem Leitfaden.

>[!NOTE]
> In diesem [Tutorial](https://docs.microsoft.com/azure/azure-vmware/hybrid-cloud-extension-installation) erfahren Sie, wie Sie HCX für AVS installieren.

- Während der Konfiguration von HCX hat Contoso verschiedene Optionen aktiviert, darunter die Migration und Notfallwiederherstellung.

![Konfigurieren von HCX](./media/contoso-migration-vmware-to-azure/hcx-manager.png)

> Hinweis: Informieren Sie sich über den [Workflow für die Installation von HCX für öffentliche HCX-Clouds](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-FDE5473E-6B71-4A71-85B6-8C9BA2B73686.html).

#### <a name="perform-migrations-to-azure-using-hcx"></a>Durchführen der Migrationen zu Azure mithilfe von HCX

Nachdem sowohl das lokale Rechenzentrum (Quelle) als auch die private AVS-Cloud (Ziel) mit VMware Cloud und HCX konfiguriert wurden, kann Contoso mit der Migration von VMs beginnen. VMs können mithilfe verschiedener Migrationstechnologien in und aus VMware HCX-fähige(n) Rechenzentren verschoben werden.

- Die HCX-Anwendung von Contoso ist online, und der Status ist grün. Das Contoso-Team kann jetzt AVS-VMs mit HCX migrieren und schützen.

![HCX-Status](./media/contoso-migration-vmware-to-azure/appliance-status.png)

#### <a name="vmware-hcx-bulk-migration"></a>VMware HCX-Massenmigration

Bei dieser Migrationsmethode werden die VMware vSphere-Replikationsprotokolle verwendet, um die VMs an einen Zielstandort zu verschieben.

- Die Massenmigration ist für das parallele Migrieren von VMs vorgesehen.
- Bei diesem Migrationstyp kann ein vordefinierter Zeitplan zum Ausführen der Migration festgelegt werden.
- Die VM wird am Quellstandort ausgeführt, bis das Failover beginnt. Die Dienstunterbrechung bei der Massenmigration entspricht einem Neustart.

#### <a name="vmware-hcx-vmotion-live-migration"></a>VMware HCX vMotion-Livemigration

Bei dieser Methode wird das VMware vMotion-Protokoll verwendet, um eine VM an einen Remotestandort zu verschieben.

- Mit vMotion kann jeweils eine VM migriert werden.
- Der VM-Status wird verschoben. Während der VMware HCX vMotion-Migration gibt es keine Dienstunterbrechung.

#### <a name="vmware-hcx-cold-migration"></a>Kalte VMware HCX-Migration

Bei dieser Migrationsmethode wird das VMware NFC-Protokoll verwendet. Diese Option wird automatisch ausgewählt, wenn die Quell-VM ausgeschaltet ist.

#### <a name="vmware-hcx-replication-assisted-vmotion"></a>VMware HCX Replication Assisted vMotion

VMware HCX Replication Assisted vMotion (RAV) verbindet die Vorteile der VMware HCX-Massenmigration (parallele Vorgänge, Resilienz und Zeitplanung) mit denen von VMware HCX vMotion (Migration des VM-Status ohne Downtime).

> [!IMPORTANT]
> Weitere Informationen finden Sie in der [VMware-Dokumentation zu HCX](https://docs.vmware.com/en/VMware-HCX/index.html) und im Abschnitt zum [Migrieren von VMs mit VMware HCX](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-D0CD0CC6-3802-42C9-9718-6DA5FEC246C6.html?hWord=N4IghgNiBcIBIGEAaACAtgSwOYCcwBcMB7AOxAF8g) in der technischen Dokumentation zu VMware.
