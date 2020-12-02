---
title: Moodle-Migrationsressourcen
description: Hier erfahren Sie mehr über die Ressourcen, die bei einer Moodle-Migration in Azure erstellt werden. Dies sind z. B. eine Azure Virtual Network-Instanz, eine Netzwerksicherheitsgruppe und ein Subnetz.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: b42253b69dfaca4ca411e2de20b2527d58cb81ff
ms.sourcegitcommit: 18f3ee8fcd8838f649cb25de1387b516aa23a5a0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2020
ms.locfileid: "96327830"
---
# <a name="moodle-migration-resources"></a>Moodle-Migrationsressourcen

Wenn Sie eine Azure Resource Manager-Vorlage (ARM) zum Migrieren von Moodle verwenden, werden bei der Bereitstellung Ressourcen in Azure erstellt. Im Rahmen dieses Bereitstellungsprozesses werden zusätzliche Bereitstellungen automatisch mit untergeordneten Vorlagen ausgeführt. In den folgenden Abschnitten werden diese Bereitstellungen und die dabei erstellten Ressourcen beschrieben.

## <a name="network-template"></a>Netzwerkvorlage

Bei der Bereitstellung der Netzwerkvorlage werden die folgenden Ressourcen erstellt:

- [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview): Hierbei handelt es sich um eine Darstellung Ihres eigenen Netzwerks in der Cloud. Virtual Network ist eine logische Isolation der dedizierten Azure-Cloud für Ihr Abonnement. Wenn Sie ein virtuelles Netzwerk erstellen, können Ihre darin vorhandenen Dienste und virtuellen Computer direkt und sicher miteinander in der Cloud kommunizieren. Das von der Netzwerkvorlage erstellte virtuelle Netzwerk enthält den Namen des virtuellen Netzwerks, die API-Version, den Ort, den DNS-Servernamen und den Adressraum (AddressSpace). „AddressSpace“ enthält einen Bereich von IP-Adressen, die von Subnetzen verwendet werden können.

- [Netzwerksicherheitsgruppe (NSG)](/azure/virtual-network/network-security-groups-overview): Hierbei handelt es sich um einen Netzwerkfilter oder eine Firewall mit einer Liste von Sicherheitsregeln. Diese Regeln lassen den Netzwerkdatenverkehr zu Ressourcen, die mit einem virtuellen Netzwerk verbunden sind, zu oder verweigern ihn.

- [Netzwerkschnittstelle:](/azure/virtual-network/virtual-network-network-interface) Hierbei handelt es sich um eine Schnittstelle, die einem virtuellen Azure-Computer die Kommunikation mit dem Internet, Azure und lokalen Ressourcen ermöglicht.

- [Subnetz](/azure/virtual-network/virtual-network-manage-subnet): Hierbei handelt es sich um ein kleineres Netzwerk innerhalb eines großen Netzwerks. Subnetze werden auch Subnetzwerke genannt. Standardmäßig kann eine IP-Adresse in einem Subnetz mit allen anderen IP-Adressen innerhalb des virtuellen Netzwerks kommunizieren.

- [Öffentliche IP-Adresse:](/azure/virtual-network/public-ip-addresses#:~:text=Public%20IP%20addresses%20enable%20Azure,IP%20assigned%20can%20communicate%20outbound) Hierbei handelt es sich um eine IP-Adresse, die von einer Azure-Ressource für die Kommunikation mit dem Internet verwendet wird. Die Adresse ist dediziert für die Azure-Ressource.

- [Azure Load Balancer](/azure/virtual-machines/windows/tutorial-load-balancer#:~:text=An%20Azure%20load%20balancer%20is,traffic%20to%20an%20operational%20VM): Hierbei handelt es sich um einen Lastenausgleich, der Netzwerk- oder Anwendungsdatenverkehr effizient auf mehrere Server in einer Serverfarm verteilt. Load Balancer stellt Hochverfügbarkeit und Zuverlässigkeit dadurch sicher, dass Anforderungen nur an Server gesendet werden, die online sind.

- [Azure Application Gateway](/azure/application-gateway/overview): Azure Application Gateway ist eine Alternative zu Load Balancer. Alle vier vordefinierten ARM-Vorlagen stellen Load Balancer bereit. Wenn Sie statt einer ARM-Vorlage eine vollständig konfigurierbare Bereitstellung verwenden, können Sie Application Gateway anstelle von Load Balancer auswählen. Application Gateway ist ein Lastenausgleich für Webdatenverkehr, mit dem Sie den eingehenden Datenverkehr für Ihre Webanwendungen verwalten können. Application Gateway kann Routingentscheidungen auf Grundlage der zusätzlichen Attribute einer HTTP-Anforderung treffen. Beispiele für solche Attribute wären etwa der URI-Pfad oder der Hostheader.

- [Azure Cache for Redis:](/azure/azure-cache-for-redis/cache-overview) Hierbei handelt es sich um einen auf der Open-Source-Software Redis basierenden In-Memory-Datenspeicher. Redis verbessert die Leistung und Skalierbarkeit einer Anwendung, die in großem Umfang Back-End-Daten speichert. Diese Software kann große Mengen von Anwendungsanforderungen verarbeiten, indem häufig verwendete Daten im Arbeitsspeicher des Servers verbleiben. Dies ermöglicht ein schnelles Schreiben in diese und Lesen aus diesen Daten.

## <a name="storage-template"></a>Speichervorlage

Bei der Bereitstellung der Speicherkontovorlage wird ein Azure-Speicherkonto vom Typ FileStorage erstellt. Dieses Konto verfügt über Premium-Leistung, LRS-Replikation (lokal redundanter Speicher) und 1 Terabyte (TB) Speicher. Die vordefinierte Vorlage ist so konfiguriert, dass ein Speicherkonto mit Azure Files Dateifreigaben erstellt.

Ein [Azure-Speicherkonto](/azure/storage/common/storage-account-overview) enthält Azure Storage-Datenobjekte wie Blobs, Dateien, Warteschlangen, Tabellen und Datenträger. Das Speicherkonto stellt einen eindeutigen Namespace für Ihre Azure Storage-Daten bereit, auf den von jedem Ort der Welt aus über HTTP oder HTTPS zugegriffen werden kann. Folgende Typen von Azure-Speicherkonten sind verfügbar: Universell V1, Universell V2, BlockBlobStorage, FileStorage und BlobStorage. Mögliche Replikationstypen sind georedundanter Speicher oder LRS und zonenredundanter Speicher. Die Leistungstypen sind „Standard“ und „Premium“, und ein einzelnes Speicherkonto kann bis zu 500 TB Daten speichern, wie bei jedem anderen Azure-Dienst.

ARM-Vorlagen unterstützen die folgenden Speicherkontotypen:

- [Network File System (NFS)](/windows-server/storage/nfs/nfs-overview): Hierbei handelt es sich um einen Kontotyp, der von einem Remotehost zum Einbinden von Dateisystemen über ein Netzwerk verwendet werden kann. Der Remotehost kann mit diesen Dateisystemen interagieren, als wären sie lokal eingebunden. Diese Gestaltung ermöglicht es Systemadministratoren, Ressourcen auf zentralisierten Servern im Netzwerk zu konsolidieren.

- [GlusterFS](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-glusterfs): Ein verteiltes Open-Source-Dateisystem, das in Bausteinweise zentral hochskaliert werden kann, um mehrere Petabytes von Daten zu speichern.

- [Azure Files](/azure/storage/files/storage-files-introduction): Der einzige öffentliche Clouddateispeicher, der sichere, SMB-basierte und vollständig verwaltete Clouddateifreigaben bereitstellt, die aus Leistungs- und Kompatibilitätsgründen auch lokal zwischengespeichert werden können. Beim NFS und GlusterFS werden Standard-LRS für die Replikation und der Speichertyp „Universell V1“ verwendet. Bei Azure Files werden Premium-LRS für die Replikation und der Typ FileStorage verwendet.

Diese Speichermechanismen unterscheiden sich abhängig von der von Ihnen gewählten Bereitstellung. Das NFS und GlusterFS erstellen einen Container, und Azure Files erstellt eine Dateifreigabe. Bei einer minimalen oder kleinen bis mittleren Moodle-Größe unterstützt die Vorlage das NFS. Bei einer großen oder maximalen Größe unterstützt die Vorlage Azure Files. Navigieren Sie zum Azure-Portal, und wählen Sie das Speicherkonto in der Ressourcengruppe aus, um auf die Container und Dateifreigaben zuzugreifen.

![Screenshot: Azure-Portal. Es wird eine Seite für das Speicherkonto mit Schaltflächen für den Zugriff auf Container und Dateifreigaben angezeigt.](./images/storage-account.png)

## <a name="database-template"></a> Datenbankvorlage

Bei der Bereitstellung der Datenbankvorlage wird ein [Azure Database for MySQL-Server](/azure/mysql/) erstellt. Azure Database for MySQL lässt sich leicht einrichten, verwalten und skalieren. Er automatisiert die Verwaltung und Wartung Ihrer Infrastruktur und des Datenbankservers, einschließlich Routineupdates, Sicherungen und Sicherheit. Azure Database for MySQL basiert auf der neuesten Community Edition von MySQL, einschließlich der Versionen 5.6, 5.7 und 8.0. Navigieren Sie zum Azure-Portal, und öffnen Sie die Ressourcengruppe, die beim Bereitstellungsprozess bereitgestellt wurde, um auf den von der Vorlage erstellten Datenbankserver zuzugreifen. Navigieren Sie anschließend zu **Azure Database for MySQL-Server**. Die Vorlage legt für den Datenbankserver einen Servernamen, einen Anmeldenamen für den Serveradministrator, eine MySQL-Version und eine Leistungskonfiguration fest.

## <a name="virtual-machine-template"></a>Vorlage für virtuelle Maschinen

Bei der Bereitstellung der Vorlage für virtuelle Computer wird eine VM als Controller-VM festgelegt. Das Betriebssystem der Controller-VM ist Ubuntu 18.04.

VM-Erweiterungen sind kleine Anwendungen, die nach der Bereitstellung Konfigurations- und Automatisierungstasks auf [virtuellen Azure-Computern](/azure/virtual-machines/extensions/overview) bereitstellen. Eine VM-Erweiterung führt ein Shellskript aus, das Moodle auf der Controller-VM installiert und Protokolldateien erfasst. Sie erstellt die Protokolldateien `stderr` und `stdout` im Ordner `/var/lib/waagent/custom-script/download/0/`. Diese Dateien können Sie als Root-Benutzer anzeigen.

## <a name="scale-set-template"></a>Skalierungsgruppenvorlage

Bei der Bereitstellung der Skalierungsgruppenvorlage wird eine [VM-Skalierungsgruppe](/azure/virtual-machine-scale-sets/overview) erstellt. Mit einer VM-Skalierungsgruppe können Sie eine Gruppe automatisch skalierender virtueller Computer bereitstellen und verwalten. Sie können die Anzahl virtueller Computer in der Skalierungsgruppe manuell skalieren oder Regeln für die Autoskalierung basierend auf der Ressourcennutzung definieren, z. B. basierend auf der [CPU-Auslastung](/visualstudio/profiling/average-cpu-utilization), dem Speicherbedarf oder dem Netzwerkdatenverkehr. Wenn eine Instanz hochskaliert wird, wird ein virtueller Computer bereitgestellt. Anschließend wird ein Shellskript ausgeführt, das Moodle-Voraussetzungen installiert und Cronjobs einrichtet. Ein virtueller Computer in einer Skalierungsgruppe verfügt über eine private IP-Adresse. Führen Sie die Schritte unter [Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse](./vpn-gateway.md) aus, um eine Verbindung mit virtuellen Computern in einer Skalierungsgruppe mit einer privaten IP-Adresse herzustellen.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie fort mit [Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse](./vpn-gateway.md).
