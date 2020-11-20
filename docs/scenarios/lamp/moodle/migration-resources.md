---
title: Moodle-Migrationsressourcen
description: Erfahren Sie mehr über Ressourcen für eine Moodle-Migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: a4b57c31e1b8d3fd489498eb36cf36f259c8e560
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714875"
---
# <a name="moodle-migration-resources"></a>Moodle-Migrationsressourcen

Wenn die Azure Resource Manager-Vorlage verwendet wird, werden in Azure die folgenden Ressourcen erstellt:

- **Netzwerkvorlage:** Die Netzwerkvorlage erstellt ein virtuelles Netzwerk, eine Netzwerksicherheitsgruppe, eine Netzwerkschnittstelle, ein Subnetz, eine öffentliche IP-Adresse, Azure Load Balancer/Application Gateway, Redis Cache und mehr.

Die Netzwerkvorlage erstellt außerdem ein virtuelles Netzwerk mit einer Zeichenfolge als Name, apiVersion, location und DNS-Servername. Der `AddressSpace` enthält einen Bereich von IP-Adressen, der von Subnetzen verwendet werden kann.

- **Virtuelles Netzwerk:** Azure Virtual Network ist eine Darstellung Ihres eigenen Netzwerks in der Cloud. Es handelt sich um eine logische Isolation der speziell für Ihr Abonnement dedizierten Azure-Cloud. Wenn Sie ein virtuelles Netzwerk erstellen, können Ihre darin vorhandenen Dienste und virtuellen Computer direkt und sicher miteinander in der Cloud kommunizieren. Weitere Informationen finden Sie unter [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview).

- **Netzwerksicherheitsgruppe:** Eine Netzwerksicherheitsgruppe (NSG) ist ein Netzwerkfilter, der eine Liste von Sicherheitsregeln enthält, die den Netzwerkdatenverkehr zu Ressourcen, die mit einem Azure Virtual Network verbunden sind, zulassen oder verweigern. Weitere Informationen finden Sie unter [Netzwerksicherheitsgruppe](/azure/virtual-network/network-security-groups-overview).

- **Netzwerkschnittstelle:** Eine Netzwerkschnittstelle ermöglicht einem virtuellen Azure-Computer die Kommunikation mit Internet, Azure und lokalen Ressourcen. Weitere Informationen finden Sie unter [Netzwerkschnittstelle](/azure/virtual-network/virtual-network-network-interface).

- **Subnetz:** Ein Subnetz oder Subnetzwerk ist ein kleineres Netzwerk innerhalb eines großen Netzwerks. Standardmäßig kann eine IP-Adresse in einem Subnetz mit allen anderen IP-Adressen innerhalb des virtuellen Netzwerks kommunizieren. Weitere Informationen finden Sie unter [Subnetz](/azure/virtual-network/virtual-network-manage-subnet).

- **Öffentliche IP:** Öffentliche IP-Adressen werden für die Kommunikation von Azure-Ressourcen mit dem Internet verwendet. Die Adresse ist dediziert für die Azure-Ressource. Weitere Informationen finden Sie unter [Öffentliche IP-Adresse](/azure/virtual-network/public-ip-addresses#:~:text=Public%20IP%20addresses%20enable%20Azure,IP%20assigned%20can%20communicate%20outbound).

- **Azure Load Balancer:** Eine effiziente Verteilung von Netzwerk- oder Anwendungsdatenverkehr auf mehrere Server in einer Serverfarm. Gewährleistet Hochverfügbarkeit und Zuverlässigkeit dadurch, dass Anforderungen nur an Server gesendet werden, die online sind. Weitere Informationen finden Sie unter [Azure Load Balancer](/azure/virtual-machines/windows/tutorial-load-balancer#:~:text=An%20Azure%20load%20balancer%20is,traffic%20to%20an%20operational%20VM).

Jede der vier vordefinierten Vorlagen stellt einen Azure Load Balancer bereit. In einer vollständig konfigurierbaren Bereitstellung kann der Benutzer Azure Application Gateway anstelle von Load Balancer auswählen.

- **Azure Application Gateway:** Ein Azure Load Balancer für Webdatenverkehr, mit dem Sie Datenverkehr an Ihre Webanwendungen verwalten können. Application Gateway kann Routingentscheidungen auf der Grundlage zusätzlicher Attribute einer HTTP-Anforderung treffen. Beispiele für solche Attribute wären etwa der URI-Pfad oder Hostheader. Weitere Informationen finden Sie unter [Was ist Azure Application Gateway?](/azure/application-gateway/overview).

- **Redis Cache:** Azure Cache for Redis bietet einen auf der Open-Source-Software Redis basierenden In-Memory-Datenspeicher. Redis verbessert die Leistung und Skalierbarkeit einer Anwendung, die in hohem Maß Back-End-Daten speichert. Redis kann große Mengen von Anwendungsanforderungen verarbeiten, indem häufig verwendete Daten im Arbeitsspeicher des Servers behalten werden, die dann schnell geschrieben und gelesen werden können. Weitere Informationen finden Sie unter [Redis Cache](/azure/azure-cache-for-redis/cache-overview).

- **Speichervorlage:** Eine Speicherkontovorlage erstellt ein Speicherkonto mit FileStorage-Variante und lokal redundanter Premium-Speicherreplikation (LRS) in einem Umfang von 1 TB. Gemäß der vordefinierten Vorlage erstellt ein Speicherkonto mit Azure Files Dateifreigaben.

Ein Azure-Speicherkonto enthält Blobs, Dateien, Warteschlangen, Tabellen und Datenträger, die alle Azure Storage-Datenobjekte sind. Das Speicherkonto stellt einen eindeutigen Namespace für Ihre Azure Storage-Daten bereit, auf den von jedem Ort der Welt aus über HTTP oder HTTPS zugegriffen werden kann. Typen von Azure-Speicherkonten sind Universell V1, Universell V2, BlockBlobStorage, FileStorage und BlobStorage. Replikationsarten sind LRS und zonenredundanter oder georedundanter Speicher. Die Leistungstypen lauten „Standard“ und „Premium“, und ein einzelnes Speicherkonto kann bis zu 500 TB Daten speichern, wie jeder andere Azure-Dienst.

Die folgenden Speicherkontotypen verfügen über Unterstützung für Azure Resource Manager-Vorlagen:

- NFS: Ein Netzwerkdateisystem (Network File System, NFS) gestattet Remotehosts das Einbinden von Dateisystemen über ein Netzwerk und die Interaktion mit diesen Dateisystemen, als ob sie lokal eingebunden wären. Dies ermöglicht es Systemadministratoren, Ressourcen auf zentralisierten Servern im Netzwerk zu konsolidieren. Weitere Informationen finden Sie unter [NFS](/windows-server/storage/nfs/nfs-overview).

- GlusterFS: Ein verteiltes Open-Source-Dateisystem, das in Bausteinweise zentral hochskaliert werden kann, um mehrere Petabytes von Daten zu speichern. Weitere Informationen finden Sie unter [Gluster FS](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-glusterfs).

- Azure Files: Der einzige öffentliche Clouddateispeicher, der sichere, SMB-basierte und vollständig verwaltete Clouddateifreigaben bereitstellt, die aus Leistungs- und Kompatibilitätsgründen auch lokal zwischengespeichert werden können. Weitere Informationen finden Sie unter [Azure Files](/azure/storage/files/storage-files-introduction). Bei NFS und glusterFS ist die Replikation Standard-LRS, und der Speichertyp ist „Universell V1“. Bei Azure Files handelt es sich bei der Replikation um lokal redundanten Premium-Speicher, LRS, und der Typ ist „FileStorage“.

Diese Speichermechanismen unterscheiden sich gemäß der ausgewählten Bereitstellung. NFS und glusterFS erstellen einen Container, und Azure Files erstellt eine Dateifreigabe. Für „Minimal“ und „short2mid“ unterstützt die Vorlage NFS, und für „Groß“ und „Maximal“ unterstützt die Vorlage Azure Files. Um auf die Container und die Dateifreigabe zuzugreifen, navigieren Sie zum Portal, und wählen Sie das Speicherkonto in der Ressourcengruppe aus.

![Ein Speicherkonto.](images/storage-account.png)

Weitere Informationen zu Speicherkonten finden Sie unter [Speicherkonto](/azure/storage/common/storage-account-overview).

- **Datenbankvorlage:** Eine Datenbankvorlage erstellt einen [Azure Database for MySQL-Server](/azure/mysql/). Ein Azure Database for MySQL-Server lässt sich einfach einrichten, verwalten und skalieren. Er automatisiert die Verwaltung und Wartung Ihrer Infrastruktur und des Datenbankservers, einschließlich Routineupdates, Sicherungen und Sicherheit. Erstellen Sie Builds mit der neuesten Communityversion von MySQL, einschließlich der Versionen 5.6, 5.7 und 8.0. Um auf den erstellten Datenbankserver zuzugreifen, navigieren Sie zu der **Ressourcengruppe**, die während der Bereitstellung bereitgestellt wird, und wechseln Sie zu **Azure Database for MySQL-Server**. Der Datenbankserver verfügt über einen Servernamen, eine Anmeldenamen des Serveradministrators, die MySQL-Version und eine Leistungskonfiguration.

- **Vorlage für virtuelle Computer:** Diese Vorlage unterscheidet einen virtuellen Computer von einem virtuellen Controllercomputer. Das Betriebssystem für einen virtuellen Controllercomputer ist Ubuntu 18.04.

- **VM-Erweiterung:** VM-Erweiterungen können kleine Anwendungen sein, die Konfigurations- und Automatisierungsaufgaben nach der Bereitstellung auf [virtuellen Azure-Computern](/azure/virtual-machines/extensions/overview) bereitstellen. Eine VM-Erweiterung führt eine Shellskriptdatei aus, die Moodle auf dem virtuellen Controllercomputer installiert und Protokolldateien erfasst. Die Protokolldateien `stderr` und `stdout` werden unter `/var/lib/waagent/custom-script/download/0/` erstellt, und der Benutzer kann Sie als root-Benutzer anzeigen.

- **Skalierungsgruppenvorlage:** Diese Vorlage erstellt eine [VM-Skalierungsgruppe](/azure/virtual-machine-scale-sets/overview). Mit einer VM-Skalierungsgruppe können Sie eine Gruppe automatisch skalierender virtueller Computer bereitstellen und verwalten. Sie können die Anzahl virtueller Computer in der Skalierungsgruppe manuell skalieren oder basierend auf der Ressourcennutzung, z. B. CPU-Auslastung, Speicherbedarf oder Netzwerkdatenverkehr, Regeln für die automatische Skalierung definieren. Die automatische Skalierung von VM-Instanzen hängt von der [CPU-Auslastung](/visualstudio/profiling/average-cpu-utilization) ab. Beim zentralen Hochskalieren einer Instanz wird ein virtueller Computer bereitgestellt, und es wird ein Shellskript ausgeführt, um Moodle-Voraussetzungen zu installieren und cron-Aufträge einzurichten. Virtuelle Computerinstanzen haben eine private IP-Adresse. Befolgen Sie die Schritte unter [Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse](./vpn-gateway.md), um eine Verbindung mit virtuellen Computern in einer Skalierungsgruppe mit einer privaten IP-Adresse herzustellen.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit [Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse](./vpn-gateway.md) fort, um weitere Informationen zum Moodle-Migrationsprozess zu erhalten.
