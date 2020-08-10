---
title: Verschieben einer lokalen VMware-Infrastruktur in Azure
description: Es wird beschrieben, wie das fiktive Unternehmen Contoso für lokale VMware-VMs die Umstellung auf Azure durchführt.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 237757b19f8289a6659d3a9c5a6275bbb4d4d7d4
ms.sourcegitcommit: 9662234674e663bc7d4bc134d303520cb146bd95
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87560473"
---
<!-- docsTest:ignore "Bulk Migration" "Cold Migration" -->

# <a name="move-on-premises-vmware-infrastructure-to-azure"></a>Verschieben einer lokalen VMware-Infrastruktur in Azure

Wenn das fiktive Unternehmen Contoso seine virtuellen VMware-Computer (VMs) aus einem lokalen Rechenzentrum zu Azure migrieren möchte, hat das zuständige Team zwei Optionen. In diesem Artikel geht es um den Dienst „Azure VMware Solution“, der von Contoso als die bessere Migrationsoption ermittelt wurde.

| Migrationsoptionen | Ergebnis |
| --- | --- |
| [Azure Migrate](https://azure.microsoft.com/services/azure-migrate/) | <li>[Bewerten](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) und [Migrieren](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware) lokaler VMs <li>Ausführen von Workloads per Azure IaaS (Infrastructure-as-a-Service) <li>Verwalten von VMs mit [Azure Resource Manager](https://azure.microsoft.com/features/resource-manager/) |
| [Azure VMware Solution](https://azure.microsoft.com/overview/azure-vmware) | <li>Verwenden der VMware HCX-Lösung (Hybrid Cloud Extension) oder von vMotion zum Verschieben von lokalen VMs <li>Ausführen nativer VMware-Workloads auf Azure-Bare-Metal-Hardware <li>Verwalten von VMs mit vSphere |

In diesem Artikel wird Azure VMware Solution von Contoso verwendet, um eine private Cloud in Azure zu erstellen, die nativen Zugriff auf VMware vCenter sowie andere von VMware unterstützte Tools für die Workloadmigration hat. Contoso kann Azure VMware Solution in dem sicheren Wissen verwenden, dass es sich um ein Erstanbieterangebot von Microsoft handelt, das auf VMware basiert.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Team von Contoso definiert in enger Zusammenarbeit mit Geschäftspartnern die geschäftlichen Faktoren, die für eine VMware-Migration zu Azure sprechen. Diese Treiber können Folgendes umfassen:

- **Verlegung oder Schließung von Rechenzentren**: Nahtlose Migration von VMware-basierten Workloads, wenn vorhandene Rechenzentren konsolidiert oder außer Betrieb genommen werden.
- **Notfallwiederherstellung und Geschäftskontinuität**: Verwendung eines in Azure bereitgestellten VMware-Stapels als primären oder sekundären Standort für die bedarfsgesteuerte Notfallwiederherstellung für die lokale Rechenzentrumsinfrastruktur.
- **Anwendungsmodernisierung**: Nutzung des Azure-Ökosystems zum Modernisieren der Anwendungen von Contoso, ohne VMware-basierte Umgebungen neu erstellen zu müssen.
- **Implementieren von DevOps**: Nutzung von Azure DevOps-Toolketten in VMware-Umgebungen und Modernisierung von Anwendungen mit der selbst gewählten Geschwindigkeit.
- **Sicherstellen der Betriebskontinuität**: Erneute Bereitstellung von vSphere-basierten Anwendungen in Azure ohne Hypervisorkonvertierungen und Refactoring von Anwendungen. Erweiterte Unterstützung für ältere Anwendungen, die unter Windows und SQL Server ausgeführt werden.

## <a name="goals-for-migrating-vmware-on-premises-to-vmware-in-the-cloud"></a>Ziele für die Migration von VMware aus der lokalen Umgebung zu VMware in der Cloud

Contoso hat sich unter Berücksichtigung der geschäftlichen Faktoren einige Ziele für die Migration gesetzt:

- Die vorhandenen Umgebungen sollen weiterhin mit VMware-Tools verwaltet werden, die den Teams des Unternehmens vertraut sind, und gleichzeitig sollen die Anwendungen mit nativen Azure-Diensten modernisiert werden.
- Die VMware-basierten Workloads von Contoso sollen nahtlos aus dem eigenen Rechenzentrum zu Azure migriert werden, und die VMware-Umgebung soll in Azure integriert werden.
- Nach der Migration soll die Anwendung in Azure die gleichen Leistungsmerkmale aufweisen wie gegenwärtig in der lokalen VMware-Umgebung. Die Anwendung bleibt lokal und in der Cloud gleichermaßen wichtig.

Diese Ziele unterstützen die Entscheidung von Contoso, Azure VMware Solution zu verwenden und als die beste Methode für die Migration zu ermitteln.

## <a name="benefits-of-running-vmware-workloads-in-azure"></a>Vorteile der Ausführung von VMware-Workloads in Azure

Mit Azure VMware Solution kann Contoso Anwendungen jetzt in VMware-Umgebungen und in Azure mit einem einheitlichen Betriebsframework nahtlos ausführen, verwalten und schützen.

Contoso profitiert von vorhandenen VMware-Investitionen, Fähigkeiten und Tools, z. B. VMware vSphere, vSAN und vCenter. Gleichzeitig kommt Contoso in den Genuss der Skalierungsmöglichkeiten, hohen Leistung und Innovationen von Azure. Darüber hinaus hat das Unternehmen folgende Möglichkeiten:

- Einrichtung der VMware-Infrastruktur in der Cloud in wenigen Minuten.
- Modernisierung von Anwendungen mit selbst gewählter Geschwindigkeit.
- VMware-Anwendungen können durch die Verwendung einer dedizierten, isolierten leistungsfähigen Infrastruktur sowie spezifischer Azure-Produkte und -Dienste erweitert werden.
- Lokale VMs können ohne Umgestaltung der Anwendungen zu Azure migriert oder auf Azure erweitert werden.
- Auf der globalen Azure-Infrastruktur können VMware-Workloads skaliert, automatisiert und schnell bereitgestellt werden.
- Nutzung der Vorteile einer Lösung, die von Microsoft bereitgestellt, von VMware überprüft und auf der Azure-Infrastruktur ausgeführt wird.

## <a name="the-solutions-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen von Contoso festgelegt wurden, entwirft und prüft das Unternehmen eine Bereitstellungslösung und bestimmt den Migrationsprozess.

### <a name="current-architecture"></a>Aktuelle Architektur

Aktuelle Features der Architektur von Contoso:

- Bereitgestellte VMs in einem lokalen Rechenzentrum, das mit [vSphere](https://www.vmware.com/products/vsphere.html) verwaltet wird
- Bereitgestellte Workloads in einem VMware-ESXi-Hostcluster, der mit [vCenter](https://www.vmware.com/products/vcenter-server.html), [vSAN](https://www.vmware.com/products/vsan.html) und [NSX](https://www.vmware.com/products/nsx.html) verwaltet wird

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Für die vorgeschlagene Architektur führt Contoso die folgende Schritte aus:

- Bereitstellen einer [privaten Azure VMware Solution-Cloud](https://docs.microsoft.com/azure/azure-vmware/concepts-private-clouds-clusters) in der Azure-Region „USA, Westen“
- Herstellen einer Verbindung zwischen dem lokalen Rechenzentrum und dem in „USA, Westen“ ausgeführten Azure VMware Solution-Dienst mithilfe von virtuellen Netzwerken und [ExpressRoute](https://docs.microsoft.com/azure/azure-vmware/concepts-networking) mit Aktivierung von Global Reach
- Migrieren von VMs zu einer dedizierten Azure VMware Solution-Instanz mithilfe von [VMware Hybrid Cloud Extension (HCX)](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-D0CD0CC6-3802-42C9-9718-6DA5FEC246C6.html)

![Diagramm: Vorgeschlagene Architektur](./media/contoso-migration-vmware-to-azure/on-premises-stretched-network-expressroute.png)

## <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet seinen vorgeschlagenen Entwurf aus, indem das Unternehmen eine Liste mit den Vor- und Nachteilen erstellt. Dies ist in der folgenden Tabelle dargestellt:

| Aspekt | Details |
| --- | --- |
| **Vorteile** | <li>Bare-Metal-VMware-Hochleistungsinfrastruktur. <li>Die Infrastruktur ist ausschließlich für Contoso bestimmt und physisch von der Infrastruktur anderer Kunden isoliert. <li>Da Contoso einen neuen Host zuweist, für den VMware verwendet wird, ist weder eine besondere Konfiguration erforderlich, noch ist die Migration besonders komplex. <li>Mit dem [Azure-Hybridvorteil](https://azure.microsoft.com/pricing/hybrid-benefit/) und den [erweiterten Sicherheitsupdates](https://www.microsoft.com/cloud-platform/windows-server-2008) für ältere Windows- und SQL-Plattformen kann Contoso seine Investition in die Software Assurance nutzen. <li>Contoso behält die vollständige Kontrolle über die Anwendungs-VMs in Azure. <br><br> |
| **Nachteile** | <li>Contoso muss die Anwendung weiterhin basierend auf VMware-VMs unterstützen, anstatt sie auf einen verwalteten Dienst wie Azure App Service und Azure SQL-Datenbank umzustellen. <li>Für die Einrichtung und Abrechnung von Azure VMware Solution werden keine einzelnen VMs in Azure IaaS, sondern mindestens drei großen Knoten zugrunde gelegt. Contoso muss seine Kapazitätsanforderungen planen, weil das Unternehmen derzeit eine lokale Umgebung nutzt, die eine Einschränkung gegenüber dem On-Demand-Ansatz der anderen Dienste in Azure darstellt. |

> [!NOTE]
> Informationen zu Preisen finden Sie unter [VMware-Lösung in Azure – Preise](https://azure.microsoft.com/pricing/details/azure-vmware/).

## <a name="migration-process"></a>Migrationsprozess

Contoso verwendet das VMware HCX-Tool, um seine VMs auf Azure VMware Solution umzustellen. Die virtuellen Computer werden in einer privaten Cloud von Azure VMware Solution ausgeführt. Die [Migrationsmethoden von VMware HCX](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-8A31731C-AA28-4714-9C23-D9E924DBB666.html) umfassen auch eine Massenmigration bzw. „kalte“ Migration. vMotion (mit oder ohne Replikationsunterstützung, Replication-assisted vMotion (RAV)) ist eine Methode, die für Workloads mit Ausführung über eine Livemigration reserviert ist.

Das Contoso-Team führt Folgendes durch, um den Prozess abzuschließen:

- Planen des Netzwerks in Azure und ExpressRoute
- Erstellen der privaten Cloud von Azure VMware Solution über das Azure-Portal
- Konfigurieren des Netzwerks, um die ExpressRoute-Leitungen einzubinden
- Konfigurieren der HCX-Komponenten für die Verbindung zwischen der lokalen vSphere-Umgebung und der privaten Cloud von Azure VMware Solution
- Replizieren der VMs und anschließendes Verschieben in Azure per VMware HCX

 ![Diagramm zum Migrationsprozess.](./media/contoso-migration-vmware-to-azure/on-premises-vmware-hcx-azure.png)

## <a name="scenarios-steps"></a>Schritte für das Szenario

> [!div class="checklist"]
>
> - **Schritt 1: Netzwerkplanung**
> - **Schritt 2: Erstellen einer privaten Cloud von Azure VMware Solution**
> - **Schritt 3: Konfigurieren des Netzwerks**
> - **Schritt 4: Migrieren von VMs mit HCX**

### <a name="step-1-network-planning"></a>Schritt 1: Netzwerkplanung

Contoso muss sein Netzwerk planen, um Azure Virtual Network und die Konnektivität zwischen der lokalen Umgebung und Azure abzudecken. Das Unternehmen muss eine Hochgeschwindigkeitsverbindung zwischen seiner lokalen und der Azure-basierten Umgebung sowie eine Verbindung mit der privaten Cloud von Azure VMware Solution bereitstellen.

Diese Konnektivität wird über Azure ExpressRoute bereitgestellt und erfordert bestimmte Netzwerkadressbereiche und Firewallports, um die Dienste zu aktivieren. Diese Verbindung mit hoher Bandbreite und geringer Latenz ermöglicht Contoso den Zugriff auf Dienste, die unter seinem Azure-Abonnement aus der privaten Cloud von Azure VMware Solution ausgeführt werden.

Contoso muss ein IP-Adressschema mit einem nicht überlappenden Adressraum für seine [virtuellen Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) planen. Für das [ExpressRoute-Gateway](https://docs.microsoft.com/azure/expressroute/expressroute-about-virtual-network-gateways) muss das Unternehmen ein Gatewaysubnetz hinzufügen.

Die private Cloud von Azure VMware Solution wird über eine weitere Azure ExpressRoute-Verbindung mit dem virtuellen Azure-Netzwerk von Contoso verbunden. Der Global Reach-Dienst von ExpressRoute wird aktiviert, um eine [direkte Verbindung](https://docs.microsoft.com/azure/azure-vmware/concepts-networking#on-premises-interconnectivity) zwischen den lokalen VMs und den in der privaten Cloud von Azure VMware Solution ausgeführten VMs zuzulassen. Zum Aktivieren von Global Reach ist die ExpressRoute-Premium-SKU ist erforderlich.

![Diagramm: ExpressRoute Global Reach mit Azure VMware Solution](./media/contoso-migration-vmware-to-azure/adjacency-overview-drawing-double.png)

Für private Clouds von Azure VMware Solution ist mindestens ein CIDR-Netzwerkadressblock vom Typ `/22` für Subnetze erforderlich. Für die Verbindungsherstellung mit lokalen Umgebungen und virtuellen Netzwerken darf der Netzwerkadressblock keine Überlappung aufweisen.

>[!NOTE]
> Weitere Informationen zur Netzwerkplanung für Azure VMware Solution finden Sie unter [Netzwerkprüfliste für die Azure-VMware-Lösung (Azure VMware Solution, AVS)](https://docs.microsoft.com/azure/azure-vmware/tutorial-network-checklist/).

### <a name="step-2-create-an-azure-vmware-solution-private-cloud"></a>Schritt 2: Erstellen einer privaten Cloud von Azure VMware Solution

Nachdem die Planung für das Netzwerk und die IP-Adressen abgeschlossen ist, führt Contoso als Nächstes die Einrichtung des Diensts „Azure VMware Solution“ in der Azure-Region „USA, Westen“ durch. Mit Azure VMware Solution kann Contoso einen vSphere-Cluster in Azure bereitstellen.

Eine private Cloud von Azure VMware Solution ist ein isoliertes softwaredefiniertes VMware-Rechenzentrum, das ESXi-Hosts, vCenter, vSAN und NSX unterstützt. Der Stapel wird auf dedizierten und isolierten Bare-Metal-Hardwareknoten in einer Azure-Region ausgeführt. Die anfängliche Bereitstellung für eine private Cloud von Azure VMware Solution muss mindestens drei Hosts umfassen. Später können nacheinander weitere Host hinzugefügt werden. Pro Cluster sind bis zu 16 Hosts möglich.

Weitere Informationen finden Sie unter [Azure VMware Solution (Vorschau): Konzepte – Private Clouds und Cluster](https://docs.microsoft.com/azure/azure-vmware/concepts-private-clouds-clusters).

Private Clouds von Azure VMware Solution werden über das Azure VMware Solution-Portal verwaltet. Contoso verfügt über eine eigene vCenter Server-Instanz in einer eigenen Verwaltungsdomäne.

Informationen zur Erstellung einer privaten Cloud von Azure VMware Solution finden Sie unter [Tutorial: Bereitstellen einer privaten AVS-Cloud in Azure](https://docs.microsoft.com/azure/azure-vmware/tutorial-create-private-cloud).

1. Zunächst registriert das Contoso-Team den Azure VMware Solution-Anbieter bei Azure, indem es den folgenden Befehl ausführt:

    ```bash
    az provider register -n Microsoft.AVS --subscription <your subscription ID>
    ```

1. Im Azure-Portal erstellt das Team die private Cloud von Azure VMware Solution, indem die Netzwerkinformationen aus dem Plan bereitgestellt werden. Anschließend wählt das Team die Option **Bewerten + erstellen** aus. Dieser Schritt dauert ungefähr zwei Stunden.

    ![Screenshot: Bereich im Azure-Portal zum Erstellen einer privaten Cloud von Azure VMware Solution](./media/contoso-migration-vmware-to-azure/create-private-cloud.png)

1. Das Team vergewissert sich, dass die Bereitstellung der privaten Cloud von Azure VMware Solution abgeschlossen ist, indem es in der Ressourcengruppe die Ressource für die private Cloud auswählt. Als Status wird *Erfolgreich* angezeigt.

    ![Screenshot: Seite mit privater Cloud von Azure VMware Solution und Anzeige der erfolgreichen Bereitstellung](./media/contoso-migration-vmware-to-azure/validate-deployment.png)

### <a name="step-3-configure-networking"></a>Schritt 3: Konfigurieren der Netzwerkeinstellungen

Für eine private Cloud von Azure VMware Solution ist ein virtuelles Netzwerk erforderlich. Da Azure VMware Solution eine lokale vCenter-Instanz während der Vorschauphase nicht unterstützt, muss Contoso für die Integration in seine lokale Umgebung weitere Schritte ausführen. Indem eine ExpressRoute-Leitung und ein Gateway für virtuelle Netzwerke eingerichtet wird, stellt das Team für seine virtuellen Netzwerke eine Verbindung mit der privaten Cloud von Azure VMware Solution her.

Weitere Informationen finden Sie unter [Tutorial: Konfigurieren des Netzwerks für Ihre private VMware-Cloud in Azure](https://docs.microsoft.com/azure/azure-vmware/tutorial-configure-networking).

1. Das Contoso-Team erstellt zunächst ein virtuelles Netzwerk mit einem Gatewaysubnetz.

    > [!IMPORTANT]
    > Das Team muss einen Adressraum verwenden, der sich *nicht* mit dem beim Erstellen der privaten Cloud verwendeten Adressraum überlappt.

1. Das Team erstellt das ExpressRoute-VPN-Gateway und achtet dabei auf die Auswahl der richtigen SKU und wählt anschließend die Option **Bewerten + erstellen** aus.

    ![Screenshot: Bereich „Gateway für virtuelle Netzwerke erstellen“](./media/contoso-migration-vmware-to-azure/create-virtual-network-gateway.png)

1. Das Team ruft den Autorisierungsschlüssel ab, um ExpressRoute mit dem virtuellen Netzwerk zu verbinden. Der Schlüssel wird im Azure-Portal auf dem Bildschirm „Konnektivität“ der Ressource für die private Cloud von Azure VMware Solution angezeigt.

    ![Screenshot: Registerkarte „ExpressRoute“ im Bereich „Konnektivität“ der Ressource für die private Cloud von Azure VMware Solution für Contoso](./media/contoso-migration-vmware-to-azure/request-auth-key.png)

1. Das Team verbindet ExpressRoute mit dem VPN-Gateway, mit dem die private Cloud von Azure VMware Solution mit dem virtuellen Netzwerk von Contoso verbunden ist. Hierfür erstellt es eine Verbindung in Azure.

    ![Screenshot: Bereich „Verbindung hinzufügen“ zum Verbinden von ExpressRoute mit dem virtuellen Netzwerk](./media/contoso-migration-vmware-to-azure/add-connection.png)

Weitere Informationen finden Sie unter [Tutorial: Hier erfahren Sie, wie Sie auf eine private AVS-Cloud (Azure VMware Solution, Azure-VMware-Lösung) zugreifen](https://docs.microsoft.com/azure/azure-vmware/tutorial-access-private-cloud).

### <a name="step-4-migrate-by-using-vmware-hcx"></a>Schritt 4: Migrieren mit VMware HCX

Um VMware-VMs mithilfe von HCX zu Azure zu migrieren, muss das Contoso-Team die folgenden allgemeinen Schritte ausführen:

- Installieren und Konfigurieren von VMware HCX
- Durchführen der Migrationen zu Azure mit HCX

Weitere Informationen finden Sie unter [Installieren von HCX für eine Azure-VMware-Lösung](https://docs.microsoft.com/azure/azure-vmware/hybrid-cloud-extension-installation).

<!-- docsTest:ignore L2 -->

#### <a name="install-and-configure-vmware-hcx-for-the-public-cloud"></a>Installieren und Konfigurieren von VMware HCX für die öffentliche Cloud

[VMware HCX](https://cloud.vmware.com/vmware-hcx) ist ein VMware-Produkt, das Teil der Standardinstallation von Azure VMware Solution ist. Standardmäßig wird HCX Advanced installiert, kann aber auf HCX Enterprise aktualisiert werden, da zusätzliche Features und Funktionen erforderlich sind. 

Azure VMware Solution automatisiert die Cloud Manager-Komponente von HCX in Azure VMware Solution. Der Dienst stellt die Aktivierungsschlüssel des Kunden sowie einen Downloadlink zur Connector-HCX-Appliance bereit, die lokal und in der vCenter-Domäne eines Kunden konfiguriert werden muss. Diese Elemente werden dann mit dem Cloudgerät von Azure VMware Solution gekoppelt, damit Kunden Dienste wie Migration und L2-Stretching nutzen können.

- Das Contoso-Team entwickelt HCX mit einem OVF-Paket, das von VMware bereitgestellt wird.

   ![Screenshot: Fenster „OVF-Vorlage bereitstellen“](./media/contoso-migration-vmware-to-azure/configure-template.png)

   Informationen zur Installation und Konfiguration von HCX für Ihre private Cloud von Azure VMware Solution finden Sie unter [Installieren von HCX für eine Azure-VMware-Lösung](https://docs.microsoft.com/azure/azure-vmware/hybrid-cloud-extension-installation).

- Beim Konfigurieren von HCX hat das Team die Aktivierung der Migration und andere Optionen ausgewählt, z. B. Notfallwiederherstellung.

   ![Screenshot: Fenster „Create Service Mesh“ (Dienstnetz erstellen) für die Konfiguration von HCX](./media/contoso-migration-vmware-to-azure/hcx-manager.png)

   Weitere Informationen finden Sie unter [HCX-Installationsworkflow für öffentliche HCX-Clouds](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-FDE5473E-6B71-4A71-85B6-8C9BA2B73686.html).

#### <a name="migrate-vms-to-azure-by-using-hcx"></a>Migrieren von VMs zu Azure mit HCX

Nachdem sowohl das lokale Rechenzentrum (Quelle) als auch die private Cloud von Azure VMware Solution (Ziel) mit der VMware-Cloud und HCX konfiguriert wurden, kann Contoso mit der Migration seiner VMs beginnen. Das Team kann verschiedenste Migrationstechnologien nutzen, um VMs in und aus Rechenzentren zu verschieben, die für VMware HCX geeignet sind.

- Die HCX-Anwendung von Contoso ist online, und der Status lautet „Grün“. Das Team ist jetzt bereit, um Azure VMware Solution-VMs mit HCX zu migrieren und zu schützen.

  ![Screenshot: Seite mit dem vSphere-Webclient von VMware](./media/contoso-migration-vmware-to-azure/appliance-status.png)

#### <a name="vmware-hcx-bulk-migration"></a>VMware HCX-Massenmigration

Bei dieser Migrationsmethode werden die VMware vSphere-Replikationsprotokolle verwendet, um mehrere VMs gleichzeitig an einen Zielstandort zu verschieben. Dies hat unter anderem folgende Vorteile:

- Diese Methode ist so konzipiert, dass mehrere VMs parallel verschoben werden.
- Die Migration kann so festgelegt werden, dass sie nach einem vordefinierten Zeitplan beendet wird.
- Die VMs werden am Quellstandort ausgeführt, bis das Failover beginnt. Die Dienstunterbrechung entspricht einem Neustart.

#### <a name="vmware-hcx-vmotion-live-migration"></a>VMware HCX vMotion-Livemigration

Bei dieser Migrationsmethode wird das VMware vMotion-Protokoll verwendet, um eine einzelne VM an einen Remotestandort zu verschieben. Dies hat unter anderem folgende Vorteile:

- Diese Methode ist so konzipiert, dass jeweils nur eine VM verschoben wird.
- Es kommt nicht zu einer Dienstunterbrechung, wenn der VM-Status migriert wird.

#### <a name="vmware-hcx-cold-migration"></a>Kalte VMware HCX-Migration

Bei dieser Migrationsmethode wird das VMware-NFC-Protokoll (Near-Field Communication) genutzt. Diese Option wird automatisch ausgewählt, wenn die Quell-VM ausgeschaltet wird.

#### <a name="vmware-hcx-replication-assisted-vmotion"></a>VMware HCX Replication Assisted vMotion

Bei VMware HCX mit vMotion mit Replikationsunterstützung (Replication Assisted vMotion, RAV) sind die Vorteile der VMware HCX-Massenmigration, z. B. parallele Vorgänge, Resilienz und Zeitplanung, mit den Vorteilen der VMware HCX vMotion-Migration, z. B. keine Ausfallzeit bei der Migration des VM-Status, vereint.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
Weitere technische Informationen zu VMware finden Sie in der Dokumentation unter:
- [VMware HCX-Dokumentation](https://docs.vmware.com/en/VMware-HCX/index.html)
- [Migrieren von virtuellen Computern per VMware HCX](https://docs.vmware.com/en/VMware-HCX/services/user-guide/GUID-D0CD0CC6-3802-42C9-9718-6DA5FEC246C6.html?hWord=N4IghgNiBcIBIGEAaACAtgSwOYCcwBcMB7AOxAF8g)
