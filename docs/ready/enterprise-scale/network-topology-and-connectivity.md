---
title: Netzwerktopologie und -konnektivität
description: Untersuchen Sie wichtige Entwurfsüberlegungen und -empfehlungen im Zusammenhang mit Netzwerken und Konnektivität zu, aus und innerhalb von Microsoft Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 08597bc09225c5444ee7ba2ac5cb867d9678cb64
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194026"
---
<!-- cSpell:ignore autoregistration BGPs MACsec MPLS MSEE onprem privatelink VPNs -->

# <a name="network-topology-and-connectivity"></a>Netzwerktopologie und -konnektivität

In diesem Abschnitt werden wichtige Entwurfsüberlegungen und -empfehlungen im Zusammenhang mit Netzwerken und Konnektivität zu, aus und innerhalb von Microsoft Azure erläutert.

## <a name="planning-for-ip-addressing"></a>Planen der IP-Adressierung

Es ist wichtig, dass Ihre Organisation die IP-Adressierung in Azure plant, um sicherzustellen, dass in lokalen Standorten und Azure-Regionen kein überlappender IP-Adressraum vorhanden ist.

**Überlegungen zum Entwurf:**

- Überlappende IP-Adressräume in der lokalen Umgebung und in Azure-Regionen bewirken gravierende Konflikte.

- Der Adressraum für virtuelle Netzwerke (VNet) kann nach der Erstellung hinzugefügt werden. Dieser Vorgang erfordert jedoch eine Betriebsunterbrechung, wenn das VNet bereits über das Peering virtueller Netzwerke mit einem anderen VNet verbunden ist, da das Peering gelöscht und neu erstellt werden muss.

- Azure reserviert in jedem Subnetz fünf IP-Adressen, die bei der Größenanpassung von VNets und der enthaltenen Subnetze berücksichtigt werden müssen.

- Einige Azure-Dienste erfordern [dedizierte Subnetze](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services#services-that-can-be-deployed-into-a-virtual-network), z. B. Azure Firewall oder VNet Gateway.

- Subnetze können an bestimmte Dienste delegiert werden, um Instanzen des betreffenden Diensts im Subnetz zu erstellen.

**Entwurfsempfehlungen:**

- Planen Sie nicht überlappende IP-Adressräume für Azure-Regionen und lokale Standorte bereits im Voraus.

- Verwenden Sie IP-Adressen aus der Adresszuordnung für private Internetadressen (RFC 1918).

- In Umgebungen mit eingeschränkter Verfügbarkeit von privaten IP-Adressen (RFC 1918) sollten Sie IPv6 verwenden.

- Erstellen Sie keine unnötig großen VNets (z. B. `/16`), um sicherzustellen, dass der IP-Adressraum nicht vergeudet wird.

- Erstellen Sie keine VNets, ohne den erforderlichen Adressraum im Voraus zu planen, da das Hinzufügen eines Adressraums zu einem Ausfall führt, sobald ein VNet über das Peering virtueller Netzwerke verbunden wird.

- Verwenden Sie keine öffentlichen IP-Adressen für VNets, insbesondere, wenn die öffentlichen IP-Adressen nicht Ihrer Organisation gehören.

## <a name="configure-the-domain-name-system-dns-and-name-resolution-for-on-premises-and-azure-resources"></a>Konfigurieren von DNS (Domain Name System) und der Namensauflösung für lokale Ressourcen und Azure-Ressourcen

Bei DNS handelt es sich um ein kritisches Entwurfsthema in der gesamten unternehmensweiten Architektur, und während einige Organisationen ihre vorhandenen Investitionen in DNS nutzen möchten, möchten andere möglicherweise ihre interne DNS-Infrastruktur modernisieren und native Azure-Funktionen nutzen.

**Überlegungen zum Entwurf:**

- Ein DNS-Konfliktlöser kann in Verbindung mit privatem Azure-DNS für die standortübergreifende Namensauflösung verwendet werden.

- Sie müssen möglicherweise vorhandene DNS-Lösungen lokal und in Azure nutzen.

- Die maximale Anzahl von privaten DNS-Zonen, mit denen ein VNet mit automatischer Registrierung verknüpft werden kann, beträgt 1.

- Die maximale Anzahl von privaten DNS-Zonen, mit denen ein VNet ohne automatische Registrierung verknüpft werden kann, beträgt 1.000.

**Entwurfsempfehlungen:**

- Für Umgebungen, in denen lediglich die Namensauflösung in Azure erforderlich ist, verwenden Sie privates Azure-DNS für die Auflösung, indem Sie eine delegierte Zone für die Namensauflösung erstellen (z. B. `azure.contoso.com`).

- Für Umgebungen, in denen die Namensauflösung in Azure und in der lokalen Umgebung erforderlich ist, verwenden Sie die vorhandene DNS-Infrastruktur (z. B. in Active Directory integriertes DNS). Diese muss auf mindestens zwei Azure-VMs bereitgestellt sein, und Sie müssen DNS-Einstellungen in VNets für die Verwendung dieser DNS-Server konfigurieren.

  - Privates Azure DNS kann weiterhin verwendet werden, wenn die Azure-Zone mit privatem DNS mit den VNets verknüpft ist und DNS-Server als Hybrid-Konfliktlöser mit bedingter Weiterleitung an lokale DNS-Namen (z. B. `onprem.contoso.com`) mit lokalen DNS-Servern verwendet werden. Lokale Server können mit bedingten Weiterleitungen an Konfliktlöser-VMs in Azure für die Zone mit privatem Azure-DNS (z. B. `azure.contoso.com`) konfiguriert werden.

- Für besondere Workloads, die ihr eigenes DNS erfordern und dieses bereitstellen (z. B. Red Hat OpenShift), sollte die jeweils bevorzugte DNS-Lösung verwendet werden.

- Die automatische Registrierung sollte für Azure DNS aktiviert werden, sodass der Lebenszyklus der DNS-Einträge für die in einem VNet bereitgestellten VMs automatisch verwaltet wird.

- Verwenden Sie einen virtuellen Computer als Konfliktlöser für die standortübergreifende DNS-Auflösung mit privatem Azure-DNS.

- Erstellen Sie die Zone mit privatem Azure-DNS in einem globalen Konnektivitätsabonnement. Es können zusätzliche Zonen mit privatem Azure-DNS erstellt werden (z. B. `privatelink.database.windows.net` oder `privatelink.blob.core.windows.net` für Azure Private Link).

## <a name="define-an-azure-network-topology"></a>Definieren einer Azure-Netzwerktopologie

Die Netzwerktopologie ist ein wichtiges grundlegendes Element der unternehmensweiten Architektur, da sie letztendlich bestimmt, wie Anwendungen miteinander kommunizieren können. In diesem Abschnitt werden relevante Technologien und Topologieansätze für Azure-Unternehmensbereitstellungen erläutert, die sich auf zwei Kernansätze konzentrieren: auf Azure Virtual WAN basierende Topologien und herkömmliche Topologien.

Eine Netzwerktopologie, die auf Azure Virtual WAN basiert, ist der bevorzugte Ansatz auf Unternehmensebene für umfangreiche Bereitstellungen in mehreren Regionen, bei denen Ihre Organisation ihre globalen Standorte sowohl mit Azure als auch lokal verbinden muss. Eine Virtual WAN-Netzwerktopologie sollte auch dann verwendet werden, wenn Ihre Organisation softwaredefinierte WAN-Bereitstellungen (SD-WAN) komplett in Azure integriert verwenden möchte. Virtual WAN wird Interkonnektivitätsanforderungen in großem Stil gerecht. Da es sich um einen von Microsoft verwalteten Dienst handelt, verringert er außerdem die generelle Komplexität des Netzwerks und kann zur Modernisierung des Netzwerks in Ihrer Organisation beitragen.

Wenn Ihre Organisation plant, Ressourcen nur in wenigen Azure-Regionen bereitzustellen, sollte eine herkömmliche Azure-Netzwerktopologie verwendet werden. Sie benötigen kein globales Netzwerk mit Interkonnektivität, haben eine geringe Anzahl von Remotestandorten oder Zweigstellen pro Region (weniger als 30 IPsec-Tunnel erforderlich), oder Sie benötigen vollständige Kontrolle und Granularität für das manuelle Konfigurieren Ihres Azure-Netzwerks. Diese herkömmliche Topologie hilft Ihnen, ein sicheres Netzwerkfundament in Azure zu erstellen.

## <a name="virtual-wan-network-topology-microsoft-managed"></a>Virtual WAN-Netzwerktopologie (von Microsoft verwaltet)

![Netzwerktopologie und -konnektivität](./media/virtual-wan-topology.png)
_Abbildung 1: Virtual WAN-Netzwerktopologie._

**Überlegungen zum Entwurf:**

- [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) ist eine von Microsoft verwaltete Lösung, bei der standardmäßig End-to-End-Konnektivität für globale Übertragungen geboten wird. Mit Virtual WAN-Hubs muss die Netzwerkkonnektivität nicht mehr manuell konfiguriert werden. Beispielsweise müssen Sie keine benutzerdefinierte Weiterleitung (User-Defined Routing, UDR) oder virtuelle Netzwerkgeräte (Network Virtual Appliances, NVAs) einrichten, um die Konnektivität für globale Übertragungen zu ermöglichen.

- Virtual WAN vereinfacht die End-to-End-Netzwerkkonnektivität in Azure und standortübergreifend erheblich, indem eine [Hub-Spoke-Netzwerkarchitektur](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-global-transit-network-architecture) erstellt wird, die mehrere Azure-Regionen und lokale Standorte (Any-to-Any-Konnektivität) umfasst. Dies wird in der folgenden Abbildung veranschaulicht:

![Netzwerktopologie und -konnektivität](./media/global-transit.png)
_Abbildung 2: Globales Transitnetzwerk mit Virtual WAN._

- Transitive Virtual WAN-Any-to-Any-Konnektivität unterstützt die folgenden Pfade (innerhalb derselben Region und zwischen Regionen):

  - Virtuelles Netzwerk zu virtuellem Netzwerk
  - Virtuelles Netzwerk zu Zweigstelle
  - Zweigstelle zu virtuellem Netzwerk
  - Zweigstelle zu Zweigstelle

- Virtual WAN-Hubs sind gesperrt, und die einzigen Ressourcen, die Sie darin bereitstellen können, sind virtuelle Netzwerkgateways (Point-to-Site-VPN, Site-to-Site-VPN und ExpressRoute), Azure Firewall über Firewall Manager und Routingtabellen.

- Virtual WAN erhöht das Limit von bis zu 200 Präfixen, die von Azure zu lokalen Umgebungen angeboten werden, über privates ExpressRoute-Peering auf 10.000 Präfixe pro Virtual WAN-Hub. Das Limit von 10.000 Präfixen schließt auch Site-to-Site-VPN-und Point-to-Site-VPN ein.

- Transitive VNet-zu-VNet-Konnektivität (innerhalb einer Region und zwischen Regionen) liegt jetzt in der allgemeinen Verfügbarkeit (GA) vor.

- Hub-zu-Hub-Verbindungen von Virtual WAN liegen jetzt in der allgemeinen Verfügbarkeit (GA) vor.

- Die Transitkonnektivität zwischen den VNETs unter Virtual WAN Standard wird ermöglicht, weil auf jedem virtuellen Hub ein Router vorhanden ist. Für jeden Router eines virtuellen Hubs wird ein aggregierter Durchsatz von bis zu 50 GBit/s unterstützt.

- Virtual WAN ist mit einer Vielzahl von [SD-WAN-Anbietern](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-locations-partners) integriert.

- Viele Anbieter verwalteter Dienste bieten [verwaltete Dienste](https://docs.microsoft.com/azure/networking/networking-partners-msp) für Virtual WAN.

- VPN-Gateways in Virtual WAN können auf bis zu 20 Gbit/s und 20.000 Verbindungen pro virtuellen Hub aufskaliert werden.

- ExpressRoute-Leitungen mit dem Premium-Add-On sind erforderlich, und sie müssen von einem ExpressRoute-Global Reach-Standort ausgehen.

- Azure Firewall Manager, der jetzt in der allgemeinen Verfügbarkeit (GA) vorliegt, ermöglicht das Bereitstellen der Azure Firewall im Virtual WAN-Hub.

- Virtual WAN-Hub-to-Hub-Datenverkehr über Azure Firewall wird derzeit nicht unterstützt. Verwenden Sie alternativ eine native Hub-to-Hub-Transitweiterleitung in Virtual WAN, und verwenden Sie NSGs, um VNet-Datenverkehr zwischen Hubs zuzulassen bzw. zu sperren.

**Entwurfsempfehlungen:**

- Virtual WAN wird dringend für neue große/globale Netzwerkbereitstellungen in Azure empfohlen, bei denen Sie eine globale Transitkonnektivität zwischen Azure-Regionen und lokalen Standorten benötigen, ohne dass Sie das transitive Routing von Azure-Netzwerken selbst manuell einrichten müssen.

  In der folgenden Abbildung wird ein Beispiel für eine globale Unternehmensbereitstellung mit Rechenzentren in Europa und den USA und einer großen Anzahl von Zweigstellen in beiden Regionen veranschaulicht. Die Umgebung ist global über Virtual WAN und ExpressRoute Global Reach verbunden.

![Beispiel-Netzwerktopologie](./media/global-reach-topology.png)
_Abbildung 3: Beispiel-Netzwerktopologie._

- Verwenden Sie Virtual WAN als globale Konnektivitätsressource mit einem Virtual WAN-Hub pro Azure-Region, um mehrere Zielzonen in Azure-Regionen über den lokalen Virtual WAN-Hub miteinander zu verbinden.

- Verbinden Sie Virtual WAN-Hubs mit lokalen Rechenzentren mithilfe von ExpressRoute.

- Verbinden Sie Zweigstellen und Remotestandorte über ein Site-to-Site-VPN mit dem nächstgelegenen Virtual WAN-Hub, oder aktivieren Sie die Zweigstellenkonnektivität mit Virtual WAN über eine SD-WAN-Partnerlösung.

- Verbinden Sie Endbenutzer mit dem Virtual WAN-Hub über ein Point-to-Site-VPN.

- Befolgen Sie das Prinzip „Datenverkehr in Azure verbleibt in Azure“, sodass die Kommunikation über Ressourcen in Azure über das Microsoft-Backbone-Netzwerk erfolgt, auch wenn sich die Ressourcen in unterschiedlichen Regionen befinden.

- Stellen Sie Azure Firewall in Virtual WAN-Hubs zum Schützen/Filtern von Ost-West- und Süd-Nord-Datenverkehr in einer Azure-Region bereit.

- Wenn Drittanbieter-NVAs zum Schützen/Filtern von Ost-West- und/oder Süd-Nord-Datenverkehr erforderlich sind, stellen Sie die NVAs in einem separaten VNet bereit (z. B. einem NVA-VNet), und verbinden Sie dieses mit dem regionalen Virtual WAN-Hub und den Zielzonen, die Zugriff auf NVAs benötigen. Weitere Informationen finden Sie unter [Erstellen einer Routingtabelle für den Virtual WAN-Hub für virtuelle Netzwerkgeräte](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-route-table-portal).

- Wenn Sie Netzwerktechnologien und NVAs von Drittanbietern bereitstellen, befolgen Sie die Anweisungen des Drittanbieters, um sicherzustellen, dass keine Konflikte mit Azure-Netzwerken auftreten.

- Erstellen Sie kein Transitnetzwerk über dem Azure Virtual WAN, da Virtual WAN alle Anforderungen an eine transitive Netzwerktopologie erfüllt, einschließlich der Fähigkeit, NVAs von Drittanbietern zu verwenden.

- Verwenden Sie keine vorhandenen lokalen Netzwerke wie MPLS (Multiprotocol Label Switching), um Azure-Ressourcen über Azure-Regionen hinweg zu verbinden, da Azure-Netzwerktechnologien die Verbindung von Azure-Ressourcen regionsübergreifend über den Microsoft-Backbone unterstützen.

- Informationen zu Brownfield-Szenarien, in denen Sie aus einer Hub-Spoke-Netzwerktopologie migrieren, die nicht auf Virtual WAN basiert, finden Sie unter [Migrieren zu Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/migrate-from-hub-spoke-topology).

- Azure Virtual WAN- und Azure Firewall-Ressourcen müssen innerhalb des Konnektivitätsabonnements erstellt werden.

- Erstellen Sie nicht mehr als 500 VNet-Verbindungen pro virtuellen Virtual WAN-Hub.

## <a name="traditional-azure-networking-topology"></a>Herkömmliche Azure-Netzwerktopologie

Virtual WAN bietet zwar eine große Bandbreite an leistungsstarken Funktionen, gelegentlich kann jedoch ein herkömmlicher Azure-Netzwerkansatz optimal sein.

- Wenn ein globales transitives Netzwerk über mehrere Azure-Regionen oder mehrere lokale Standorte nicht erforderlich ist, z. B. wenn eine Zweigstelle in den USA Konnektivität mit einem virtuellen Netzwerk in Europa benötigt.

- Wenn keine Notwendigkeit besteht, eine Verbindung mit einer großen Anzahl von Remotestandorten über VPN oder die Integration mit einer SD-WAN-Lösung herzustellen.

- Wenn Ihre Organisation granulare Kontrolle und Konfiguration beim Einrichten einer Netzwerktopologie Azure wünscht.

![Netzwerktopologie und -konnektivität](./media/customer-managed-topology.png)
_Abbildung 4: Eine herkömmliche Azure-Netzwerktopologie._

**Überlegungen zum Entwurf:**

- Es gibt verschiedene Netzwerktopologien zum Verbinden von VNets in mehreren Zielzonen: ein großes flaches VNet, mehrere VNets, die über mehrere ExpressRoute-Leitungen oder -Verbindungen verbunden sind, Hub-and-Spoke, Full Mesh und Hybrid.

- VNets überschreiten keine Abonnementgrenzen, aber die Konnektivität zwischen VNets in verschiedenen Abonnements kann entweder über das Peering virtueller Netzwerke, über eine ExpressRoute-Leitung oder mithilfe von VPN-Gateways erreicht werden.

- Das Peering virtueller Netzwerke kann zum Verbinden von VNets in derselben Region, in verschiedenen Azure-Regionen und in verschiedenen Azure AD-Mandanten verwendet werden.

- Das Peering virtueller Netzwerke und das globale VNet-Peering sind nicht transitiv. Daher sind UDRs und NVAs erforderlich, um ein Transitnetzwerk zu aktivieren. Weitere Informationen finden Sie unter [Hub-Spoke-Netzwerktopologie in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke).

- Über Expressroute-Leitungen können Verbindungen zwischen VNets innerhalb derselben geopolitischen Region hergestellt werden; auch das Premium-Add-On kann für die Konnektivität zwischen geopolitischen Regionen verwendet werden.

  - VNet-zu-VNet-Datenverkehr kann eine zusätzliche Wartezeit zur Folge haben, da Datenverkehr die MSEE-Router (Microsoft Enterprise Edge) mühsam durchlaufen muss.

  - Die Bandbreite ist auf die ExpressRoute-Gateway-SKU beschränkt.

  - Sie müssen weiterhin UDRs bereitstellen und verwalten, wenn Sie VNet-überschreitenden Datenverkehr untersuchen und protokollieren müssen.

- VPN-Gateways mit BGP (Border Gateway Protocol) sind innerhalb von Azure und lokal transitiv, werden jedoch nicht über ExpressRoute-Gateways übertragen.

- Wenn mehrere ExpressRoute-Leitungen mit demselben VNet verbunden sind, muss mit Verbindungsgewichtungen und BGP-Techniken ein optimaler Pfad für den Datenverkehr zwischen lokalen Standorten und Azure sichergestellt werden. Weitere Informationen finden Sie unter [Optimieren von ExpressRoute-Routing](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing).

- Die Verwendung von BGP-Techniken zum Beeinflussen des ExpressRoute-Routings ist eine Konfiguration außerhalb der Azure-Cloud. Daher müssen Ihre Organisation oder Ihr Konnektivitätsanbieter die lokalen Router entsprechend konfigurieren.

- Expressroute-Leitungen mit Premium-Add-Ons bieten globale Konnektivität. Die maximale Anzahl von ExpressRoute-Verbindungen pro ExpressRoute-Gateway beträgt jedoch 4.

- Während die maximale Anzahl von Peeringverbindungen zwischen virtuellen Netzwerken pro VNet 500 beträgt, beläuft sich die maximale Anzahl von Routen, die von Azure zu lokalen Standorten über privates ExpressRoute-Peering angekündigt werden können, auf 200.

- Der maximale aggregierte Durchsatz eines VPN-Gateways beträgt 10 GBit/s, und es werden bis zu 30 Site-to-Site- oder VNet-zu-VNet-Tunnel unterstützt.

**Entwurfsempfehlungen:**

- Ein Netzwerkentwurf, der auf der Hub-and-Spoke-Netzwerktopologie mit Nicht-Virtual WAN-Technologien basiert, sollte für die folgenden Szenarien erwogen werden:

  - Azure-Bereitstellungen, bei denen die Datenverkehrsgrenze innerhalb einer Azure-Region liegt.

  - Eine Netzwerkarchitektur mit bis zu zwei Azure-Regionen, in denen die Transitkonnektivität zwischen Zielzonen-VNets in verschiedenen Regionen erforderlich ist.

  - Eine Netzwerkarchitektur, die mehrere Azure-Regionen umfasst, wobei keine Transitkonnektivität zwischen Zielzonen-VNets in verschiedenen Regionen benötigt wird.

  - Transitkonnektivität zwischen VPN- und ExpressRoute-Verbindungen ist nicht erforderlich.

  - Der Hauptkanal für die Konnektivität zwischen lokalen Standorten ist ExpressRoute, und die Anzahl der VPN-Verbindungen pro VPN-Gateway ist kleiner als 30.

  - Es besteht eine starke Abhängigkeit von zentralisierten NVAs und einem komplexen/präzisen Routing.

- Verwenden Sie für regionale Bereitstellungen hauptsächlich die Hub-Spoke-Topologie, wobei Zielzonen-VNets über das Peering virtueller Netzwerke mit einem zentralen Hub-VNet für die Konnektivität zwischen lokalen Standorten über ExpressRoute verbunden sind. VPN wird für die Zweigstellenkonnektivität verwendet, Spoke-to-Spoke-Konnektivität über NVAs und UDRs sichergestellt und der Schutz für ausgehenden Datenverkehr in das Internet über NVA erfolgt, wie in der Abbildung unten veranschaulicht.

![Netzwerktopologie und -konnektivität](./media/hub-and-spoke-topology.png)

_Abbildung 5: Hub-Spoke-Netzwerktopologie._

- Wenn ein hohes Maß an Isolation erforderlich ist, für bestimmte Geschäftseinheiten eine dedizierte ExpressRoute-Bandbreite benötigt wird oder die maximale Anzahl von Verbindungen pro ExpressRoute-Gateway (bis zu vier) erreicht wird, verwenden Sie die verschiedenen VNets, die mit einer Topologie mit mehreren ExpressRoute-Leitungen verbunden sind. Dies wird in der folgenden Abbildung dargestellt:

![Netzwerktopologie und -konnektivität](./media/vnet-multiple-circuits.png)
_Abbildung 6: Mehrere virtuelle Netzwerke sind mit mehreren ExpressRoute-Leitungen verbunden._

- Stellen Sie im zentralen Hub-VNet eine minimale Gruppe von gemeinsamen Diensten bereit, einschließlich ExpressRoute-Gateways, VPN-Gateways (sofern erforderlich) und Azure Firewall oder Drittanbieter-NVAs (falls erforderlich). Falls erforderlich, auch Active Directory-Domänencontroller und DNS-Server.

- Stellen Sie Azure Firewall oder Drittanbieter-NVAs zum Schützen/Filtern des Ost-West- und/oder Süd-Nord-Datenverkehrs im zentralen Hub-VNet bereit.

- Wenn Sie Netzwerktechnologien/NVAs von Drittanbietern bereitstellen, befolgen Sie die Anweisungen des Drittanbieters, um sicherzustellen, dass die Bereitstellung vom Hersteller unterstützt wird, für Hochverfügbarkeit und maximale Leistung konzipiert ist und dass es keine Konfigurationen gibt, welche Konflikte mit Azure-Netzwerken bewirken.

- L7-Eingangs-NVAs (wie Azure Application Gateway) sollten nicht als gemeinsamer Dienst im zentralen Hub-VNet bereitgestellt werden. Stattdessen sollten sie in der jeweiligen Zielzone zusammen mit der App bereitgestellt werden.

- Verwenden Sie Ihr vorhandenes Netzwerk (MPLS und SD-WAN), um Zweigstellen mit dem Hauptsitz des Unternehmens zu verbinden. Transit in Azure zwischen ExpressRoute- und VPN-Gateways wird nicht unterstützt.

- Verwenden Sie für Netzwerkarchitekturen mit mehreren Hub-Spoke-Topologien in Azure-Regionen das globale VNet-Peering, um Zielzonen-VNets zu verbinden, wenn eine kleine Anzahl von Zielzonen regionsübergreifend miteinander kommunizieren muss. Diese Vorgehensweise bietet Vorteile, wie z. B. eine hohe Netzwerkbandbreite mit globalem VNet-Peering (sofern durch die VM-SKU zugelassen), aber die zentrale NVA wird umgangen (wenn die Prüfung/Filterung des Datenverkehrs erforderlich ist). Außerdem gelten [Einschränkungen durch das globale VNet-Peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview#constraints-for-peered-virtual-networks).

- Wenn Sie eine Hub-Spoke-Netzwerktechnologie in zwei Azure-Regionen bereitstellen und Transitkonnektivität regionsüberschreitend zwischen allen Zielzonen erforderlich ist, verwenden Sie ExpressRoute mit dualen Leitungen, um Transitkonnektivität für Zielzonen-VNets in den Azure-Regionen sicherzustellen. In diesem Szenario ist der Transit für Zielzonen innerhalb einer Region über NVA im lokalen Hub-VNet und zwischen Regionen über eine ExpressRoute-Leitung möglich, und der Datenverkehr muss mühsam die MSEE-Router (Microsoft Enterprise Edge) durchlaufen. Dieser Entwurf wird in der folgenden Abbildung veranschaulicht:

![Netzwerktopologie und -konnektivität](./media/vnet-dual-circuits.png)
_Abbildung 7: Zielzonen-Konnektivitätsentwurf._

- Wenn Ihr Unternehmen Hub-and-Spoke-Netzwerkarchitekturen über mehr als zwei Azure-Regionen und globale Transitkonnektivität zwischen Zielzonen benötigt, sind VNets erforderlich, die über Azure-Regionen hinweg arbeiten. Diese Architektur könnte zwar durch die Verbindung von VNets des zentralen Hubs mit globalen VNet-Peerings und die Verwendung von UDRs und NVAs zur Ermöglichung eines globalen Transitrouting implementiert werden, aber die Komplexität und der Verwaltungsaufwand sind hoch. Stattdessen empfehlen wir die Bereitstellung einer Architektur mit globalem Transitnetzwerk mit Virtual WAN.

- Verwenden Sie [Azure Monitor Network Insights](https://docs.microsoft.com/azure/azure-monitor/insights/network-insights-overview) (derzeit in der Vorschauversion), um den End-to-End-Status von Ihren Netzwerken in Azure zu überwachen.

- Erstellen Sie nicht mehr als 200 Peeringverbindungen pro zentralem Hub-VNet. VNets unterstützen zwar bis zu 500 Peeringverbindungen, ExpressRoute mit privatem Peering unterstützt jedoch nur die Ankündigung von bis zu 200 Präfixen von Azure zur lokalen Umgebung.

## <a name="connectivity-to-azure"></a>Konnektivität mit Azure

In diesem Abschnitt wird die Netzwerktopologie erweitert, um empfohlene Modelle für die Verbindung von lokalen Standorten mit Azure zu betrachten.

**Überlegungen zum Entwurf:**

- Azure ExpressRoute bietet dedizierte private Konnektivität zu Microsoft Azure IaaS- (Infrastructure-as-a-Service ) und PaaS-Funktionen (Platform-as-a-Service) von lokalen Standorten.

- Mit Private Link kann die Konnektivität mit PaaS-Diensten über ExpressRoute mit privatem Peering eingerichtet werden.

- Wenn mehrere VNets mit derselben ExpressRoute-Leitung verbunden sind, werden sie Teil derselben Routingdomäne, und die Bandbreite wird von allen VNets gemeinsam genutzt.

- ExpressRoute Global Reach (falls verfügbar) ermöglicht es Ihnen, lokale Standorte mithilfe von ExpressRoute-Leitungen zu verbinden, um den Datenverkehr über das Microsoft-Backbone-Netzwerk zu übertragen.

- Expressroute-Global Reach ist in vielen [ExpressRoute-Peeringstandorten](https://docs.microsoft.com/azure/expressroute/expressroute-global-reach#availability) vorhanden.

- ExpressRoute Direct ermöglicht das Erstellen von mehreren ExpressRoute-Leitungen ohne anfallende Zusatzkosten bis zur Kapazität des ExpressRoute Direct-Ports (10 GBit/s oder 100 GBit/s) und lässt das Herstellen von direkten Verbindungen mit den ExpressRoute-Routern von Microsoft zu. Bei der 100-GBit/s-SKU beträgt die Mindestbandbreite der Leitung 5 GBit/s. Bei der 10-GBit/s-SKU beträgt die Mindestbandbreite der Leitung 1 GBit/s.

<!-- cSpell:ignore prepending -->
<!-- docsTest:ignore "AS PATH prepending -->

**Entwurfsempfehlungen:**

- Verwenden Sie ExpressRoute als hauptsächlichen Konnektivitätskanal für Verbindungen zwischen dem lokalen Netzwerk und Microsoft Azure. VPNs können als Quelle für die Sicherungskonnektivität verwendet werden, um die Resilienz der Konnektivität zu verbessern.

- Verwenden Sie duale ExpressRoute-Leitungen von verschiedenen Peeringstandorten, wenn Sie eine Verbindung eines lokalen Standorts mit VNets in Azure herstellen. Durch dieses Setup werden redundante Pfade zu Azure sichergestellt, da Single Points of Failure zwischen dem lokalen Standort und Azure beseitigt werden.

- Wenn mehrere ExpressRoute-Leitungen verwendet werden, [optimieren Sie das ExpressRoute-Routing über die lokale BGP-Einstellung und Voranstellen von AS PATH](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing#solution-use-as-path-prepending).

- Stellen Sie sicher, dass die richtige SKU für ExpressRoute-/VPN-Gateways verwendet wird, entsprechend den Anforderungen in Bezug auf Bandbreite und Leistung.

- Stellen Sie ein zonenredundantes ExpressRoute-Gateway in den unterstützten Azure-Regionen bereit.

- Verwenden Sie ExpressRoute Direct für Szenarien, in denen eine Bandbreite von mehr als 10 GBit/s oder dedizierte 10/100 GBit/s-Ports benötigt werden.

- Wird eine geringe Latenzzeit benötigt oder muss der Durchsatz zwischen einem lokalen Standort und Azure mehr als 10 GBit/s betragen, aktivieren Sie FastPath, um das ExpressRoute-Gateway vom Datenpfad zu umgehen.

- Verwenden Sie VPN-Gateways, um Zweigstellen oder Remotestandorte mit Azure zu verbinden. Stellen Sie für eine höhere Resilienz zonenredundante Gateways bereit (soweit verfügbar).

- Verwenden Sie ExpressRoute Global Reach, um große Niederlassungen/regionale Zentralen/Rechenzentren zu verbinden, die über ExpressRoute mit Azure verbunden sind.

- Wenn die Isolation von Datenverkehr oder dedizierte Bandbreite benötigt wird (z. B. zum Trennen von Produktions- und Nicht-Produktionsumgebungen), sollten verschiedene ExpressRoute-Leitungen verwendet werden, um isolierte Routingdomänen sicherzustellen und das Risiko der Beeinträchtigung durch andere Dienste („Noisy Neighbors“) zu mindern.

- Überwachen Sie ExpressRoute-Leitungen proaktiv mit dem Netzwerkleistungsmonitor.

- Verwenden Sie ExpressRoute-Leitungen nicht explizit von einem einzigen Peeringstandort aus, da dadurch ein Single Point of Failure entsteht und Ihre Organisation anfällig für den Ausfall von Peeringstandorten ist.

- Verwenden Sie nicht dieselbe ExpressRoute-Leitung zum Verbinden mehrerer Umgebungen, die Isolation oder dedizierte Bandbreite benötigen, um das Noisy-Neighbor-Risiko zu mindern.

## <a name="connectivity-to-azure-paas-services"></a>Konnektivität mit Azure PaaS-Diensten

Aufbauen auf den vorigen Abschnitten zur Konnektivität werden in diesem Abschnitt empfohlene Ansätze hinsichtlich der Konnektivität bei der Verwendung von Azure PaaS-Diensten erläutert.

**Überlegungen zum Entwurf:**

- Der Zugriff auf Azure PaaS-Dienste erfolgt im Allgemeinen über öffentliche Endpunkte. Die Azure-Plattform bietet jedoch Funktionen, mit denen solche Endpunkte gesichert oder sogar vollständig eingerichtet werden können.

  - Die Einschleusung von VNet ermöglicht dedizierte private Bereitstellungen für unterstützte Dienste. Der Datenverkehr auf der Verwaltungsebene fließt jedoch über öffentliche IP-Adressen.

  - [Private Link](https://docs.microsoft.com/azure/private-link/private-endpoint-overview#private-link-resource) bietet dedizierten Zugriff mit privaten IP-Adressen auf Azure PaaS-Instanzen, ebenso benutzerdefinierte Dienste hinter einem Azure Load Balancer-Standard.

  - VNet-Dienstendpunkte bieten aus ausgewählten Subnetzen Zugriff auf der Dienstebene auf ausgewählte PaaS-Dienste.

- Unternehmen haben häufig Bedenken in Bezug auf öffentliche Endpunkte für PaaS-Dienste, die entsprechend adressiert werden müssen.

- Für [unterstützte Dienste](https://docs.microsoft.com/azure/private-link/private-link-overview#availability) adressiert Private Link die Datenexfiltrationsprobleme an Dienstendpunkten. Alternativ können über Filterung ausgehenden Datenverkehrs über NVAs Schritte ergriffen werden, um das Risiko der Datenexfiltration zu mindern.

**Entwurfsempfehlungen:**

- Verwenden Sie die Einschleusung von VNet für unterstützte Azure-Dienste, um diese aus Ihrem VNet verfügbar zu machen.

- Azure PaaS-Dienste, die in ein VNet eingeschleust wurden, führen immer noch Vorgänge auf der Verwaltungsebene mit öffentlichen IP-Adressen durch. Stellen Sie mit benutzerdefinierten Routen und Netzwerksicherheitsgruppen sicher, dass diese Kommunikation im VNet gesperrt wird.

- Verwenden Sie Private Link (sofern verfügbar) für die freigegebenen Azure PaaS-Dienste. Private Link ist für einige Dienste allgemein verfügbar und liegt für eine Vielzahl von Diensten in der öffentlichen Vorschauversion vor. Die Private Link-Verfügbarkeit wird [hier](https://docs.microsoft.com/azure/private-link/private-link-overview#availability) ausführlich erläutert.

- Greifen Sie auf Azure PaaS-Dienste von lokalen Standorten über privates ExpressRoute-Peering zu, und verwenden Sie dabei VNet-Einschleusung für dedizierte Azure-Dienste oder Azure Private Link für verfügbare gemeinsame Azure-Dienste. Verwenden Sie ExpressRoute mit Microsoft-Peering, um von einem lokalen Standort aus auf Azure-PaaS-Dienste zuzugreifen, wenn VNet-Einschleusung und Private Link nicht verfügbar sind. Dadurch wird der Transit über das öffentliche Internet vermieden.

- Verwenden Sie VNet-Dienstendpunkte, um den Zugriff auf Azure PaaS-Dienste aus Ihrem VNet zu schützen. Dies gilt jedoch nur, wenn Private Link nicht verfügbar ist, und keine Risiken der Datenexfiltration bestehen. Verwenden Sie zum Adressieren von Risiken der Datenexfiltration bei Dienstendpunkten NVA-Filterung oder Richtlinien zu VNet-Dienstendpunkten für Azure Storage.

- Aktivieren Sie VNet-Dienstendpunkte nicht standardmäßig in allen Subnetzen.

- Verwenden Sie keine VNet-Dienstendpunkte, wenn Risiken hinsichtlich der Datenexfiltration vorliegen, es sei denn, die NVA-Filterung ist eingerichtet.

- Es wird nicht empfohlen, die Tunnelerzwingung zu implementieren, um die Kommunikation zwischen Azure und Azure-Ressourcen zu ermöglichen.

## <a name="planning-for-inbound-and-outbound-internet-connectivity"></a>Planen der eingehenden und ausgehenden Internetkonnektivität

In diesem Abschnitt werden empfohlene Konnektivitätsmodelle für die eingehende und ausgehende Konnektivität zum und aus dem öffentlichen Internet beschrieben.

**Überlegungen zum Entwurf:**

- Native Azure-Netzwerksicherheitsdienste wie Azure Firewall, Azure Web Application Firewall (WAF) in Azure Application Gateway und Azure Front Door sind vollständig verwaltete Dienste, sodass für Sie nicht der operative und verwaltungsbezogene Aufwand anfällt, der mit Infrastrukturbereitstellungen verbunden ist und in großem Maßstab sehr komplex werden kann.

- Die Architektur auf Unternehmensebene ist vollständig kompatibel mit Drittanbieter-NVAs, sollte Ihre Organisation die Verwendung von NVAs bevorzugen oder wenn native Dienste den konkreten Anforderungen Ihrer Organisation nicht gerecht werden.

**Entwurfsempfehlungen:**

- Verwenden Sie Azure Firewall, um Folgendes zu steuern:

  - Ausgehender Azure-Datenverkehr zum Internet

  - Eingehende Nicht-HTTP/S-Verbindungen

  - Filtern von Ost-West-Datenverkehr (falls von Ihrer Organisation gefordert)

- Verwenden Sie Firewall Manager mit Virtual WAN, um Azure-Firewalls für Virtual WAN-Hubs oder in Hub-VNets bereitzustellen und zu verwalten. Firewall Manager liegt jetzt sowohl für Virtual WAN als auch für normale VNets in der allgemeinen Verfügbarkeit (GA) vor.

- Erstellen Sie eine globale Azure Firewall-Richtlinie, um den Sicherheitsstatus in der globalen Netzwerkumgebung zu steuern, und weisen Sie sie allen Azure Firewall-Instanzen zu. Erfüllen Sie anhand präziser Richtlinien die Anforderungen bestimmter Regionen zu, indem Sie inkrementelle Firewall-Richtlinien über RBAC an lokale Sicherheitsteams delegieren.

- Konfigurieren Sie unterstützte Drittanbieter von Saas-Sicherheitslösungen in Firewall Manager, wenn Ihre Organisation derartige Lösungen zum Schutz ausgehender Verbindungen verwenden möchte.

- Verwenden Sie WAF in einem Zielzonen-VNet zum Schützen eingehenden HTTP/S-Datenverkehrs aus dem Internet.

- Verwenden Sie Azure Front Door- und WAF-Richtlinien, um über Azure-Regionen hinweg globalen Schutz für eingehende HTTP/S-Verbindungen mit einer Zielzone bereitzustellen.

- Wenn Sie HTTP/S-Apps mit Azure Front Door und Azure Application Gateway schützen, verwenden Sie WAF-Richtlinien in Azure Front Door, und sperren Sie Azure Application Gateway für den Empfang von Datenverkehr ausschließlich von Azure Front Door.

- Wenn Drittanbieter-NVAs zum Schützen/Filtern von Ost-West- und/oder Süd-Nord-Datenverkehr benötigt werden:

- Stellen Sie für Virtual WAN-Netzwerktopologien die NVAs in einem separaten VNet bereit (z. B. einem NVA-VNet), und verbinden Sie es mit dem regionalen Virtual WAN-Hub und den Zielzonen, die Zugriff auf NVAs benötigen (siehe Beschreibung in diesem [Artikel](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-route-table-portal)). Stellen Sie für Nicht-Virtual WAN-Netzwerktopologien die Drittanbieter-NVAs im VNet des zentralen Hubs bereit.

- Wenn NVAs von Drittanbietern für eingehende HTTP/S-Verbindungen erforderlich sind, sollten Sie in einem Zielzonen-VNet und zusammen mit den Apps bereitgestellt werden, die sie schützen und für das Internet verfügbar machen.

- Schützen Sie mit [Azure DDoS Protection Standard-Schutzplänen](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) alle öffentlichen Endpunkte, die in Ihren VNets gehostet werden.

- Replizieren Sie keine lokalen DMZ-Konzepte und -Architekturen in Azure, da Sie vergleichbare Sicherheitsfunktionen in Azure wie in Ihrer lokalen Umgebung erhalten können, die Implementierung und Architektur jedoch an die Cloud angepasst werden müssen.

## <a name="planning-for-app-delivery"></a>Planen der Bereitstellung von Apps

Dieser Abschnitt enthält wichtige Empfehlungen zum Bereitstellen von internen und öffentlichen Apps, wobei höchste Sicherheit, hohe Skalierbarkeit und Hochverfügbarkeit gewährleistet werden.

**Überlegungen zum Entwurf:**

- Azure Load Balancer (intern und öffentlich) bietet Hochverfügbarkeit für die Bereitstellung von Apps auf regionaler Ebene.

- Azure Application Gateway ermöglicht die sichere Bereitstellung von HTTP/S-Apps auf regionaler Ebene.

- Azure Front Door ermöglicht die sichere Bereitstellung von hochverfügbaren HTTP/S-Apps über Azure-Regionen hinweg.

- Azure Traffic Manager ermöglicht die Bereitstellung von globalen Apps.

**Entwurfsempfehlungen:**

- Die App-Bereitstellung sowohl für interne als auch öffentliche Apps sollte innerhalb von Zielzonen ausgeführt werden.

- Verwenden Sie für die sichere Bereitstellung von HTTP/S-Apps App Gateway v2, und stellen Sie sicher, dass WAF-Schutz/-Richtlinien aktiviert sind.

- Verwenden Sie ein Drittanbieter-NVA, wenn Application Gateway v2 nicht für die Sicherheit von HTTP/S-Apps verwendet werden kann.

- Azure Application Gateway v2 oder für eingehende HTTP/S-Verbindungen verwendete Drittanbieter-NVAs müssen im Zielzonen-VNet und mit den Apps bereitgestellt werden, die sie sichern.

- Alle öffentlichen IP-Adressen in einer Zielzone sollten mit einem DDoS Protection-Standardplan geschützt werden.

- Globale HTTP/S-Apps, die sich über Azure-Regionen erstrecken, sollten mit Azure Front Door mit WAF-Richtlinien bereitgestellt und geschützt werden.

- Wenn Sie HTTP/S-Apps mit Front Door und Application Gateway schützen, verwenden Sie WAF-Richtlinien in Azure Front Door, und sperren Sie Application Gateway für den Empfang von Datenverkehr ausschließlich von Front Door.

- Globale Apps, die andere Protokolle als HTTP/S umfassen, sollten mithilfe von Traffic Manager bereitgestellt werden.

## <a name="planning-for-landing-zone-network-segmentation"></a>Planen der Zielzonen-Netzwerksegmentierung

In diesem Abschnitt werden wichtige Empfehlungen für die Bereitstellung höchst sicherer interner Netzwerksegmentierung innerhalb einer Zielzone erläutert, mit denen eine Netzwerk-Zero-Trust-Implementierung gefördert wird.

**Überlegungen zum Entwurf:**

- Das Zero-Trust-Modell geht davon aus, dass ein Verstoß vorliegt, und jede Anforderung wird so verifiziert, als ob sie aus einem nicht kontrollierten Netzwerk stammen würde.

- Eine erweiterte Implementierung eines Zero-Trust-Netzwerks umfasst vollständig verteilte Mikroparameter für eingehenden/ausgehenden Clouddatenverkehr und tiefere Mikrosegmentierung.

- Netzwerksicherheitsgruppen können Azure-Diensttags verwenden, um die Konnektivität mit Azure PaaS-Diensten zu ermöglichen.

- App-Sicherheitsgruppen bieten keinen Schutz zwischen VNets.

- NSG-Datenflussprotokolle werden nun durch Azure Resource Manager-Vorlagen unterstützt.

**Entwurfsempfehlungen:**

- Delegieren Sie die Subnetzerstellung an den Zielzonenbesitzer. Dadurch kann dieser festlegen, wie Workloads über Subnetze segmentiert werden (z. B. ein einziges großes Subnetz, mehrschichtige App oder in das VNet integrierte App). Das Plattformteam kann mithilfe von Azure Policy sicherstellen, dass Subnetzen mit Richtlinien vom Typ „Immer verweigern“ immer ein NSG mit bestimmten Regeln (z. B. eingehenden SSH oder RDP aus dem Internet verweigern oder Datenverkehr zwischen Zielzonen zulassen/blockieren) zugeordnet ist.

- Mit NSGs muss der Datenverkehr über mehrere Subnetze geschützt werden, ebenso Ost-West-Datenverkehr über die Plattform (Datenverkehr zwischen Zielzonen).

- Das App-Team muss mit App-Sicherheitsgruppen auf Subnetzebenen-NSGs mehrschichtige VMs in der Zielzone schützen.

- Verwenden Sie NSGs und App-Sicherheitsgruppen zum Mikrosegmentieren von Datenverkehr in der Zielzone, filtern Sie Datenverkehrsströme nach Möglichkeit nicht mit einer zentralen NVA.

- Aktivieren Sie NSG-Datenflussprotokolle und speisen Sie diese in Traffic Analytics ein, um Erkenntnisse zu internen und externen Datenverkehrsflüssen zu gewinnen.

- Verwenden Sie NSGs, um die Konnektivität zwischen Zielzonen selektiv zuzulassen.

- Leiten Sie bei Virtual WAN-Topologien Datenverkehr über Zielzonen hinweg per Azure Firewall weiter, wenn Ihre Organisation Filter- und Protokollierungsfunktionen für Datenverkehr benötigt, der zwischen Zielzonen fließt.

## <a name="define-network-encryption-requirements"></a>Definieren von Netzwerkverschlüsselungsanforderungen

In diesem Abschnitt werden wichtige Empfehlungen zum Einrichten der Netzwerkverschlüsselung zwischen der lokalen Umgebung und Azure sowie über Azure-Regionen hinweg behandelt.

**Überlegungen zum Entwurf:**

- Kosten und verfügbare Bandbreite sind umgekehrt proportional zur Länge des Verschlüsselungstunnels zwischen Endpunkten.

- Wenn Sie mit VPN eine Verbindung mit Azure herstellen, wird der Datenverkehr über das Internet über IPSec-Tunnel (IP Security) verschlüsselt.

- Bei Verwendung von ExpressRoute mit privatem Peering wird Datenverkehr derzeit nicht verschlüsselt.

- MACsec-Verschlüsselung kann auf ExpressRoute Direct angewendet werden, um eine Netzwerkverschlüsselung zu erreichen.

- Azure bietet derzeit keine native Verschlüsselung über globales VNet-Peering. Wenn Sie heute Verschlüsselung zwischen Azure-Regionen benötigen, können Sie VNets mithilfe von VPN-Gateways anstatt über globales VNet-Peering verbinden.

**Entwurfsempfehlungen:** ![Verschlüsselungsabläufe](./media/enc-flows.png)
_Abbildung 8: Verschlüsselungsabläufe._

- Beim Einrichten von VPN-Verbindungen von einer lokalen Umgebung über VPN-Gateways mit Azure wird Datenverkehr auf einer Protokollebene mit IPsec-Tunneln verschlüsselt. Dies wird im obigen Diagramm in `Flow A` veranschaulicht.

- Konfigurieren Sie bei Verwendung von ExpressRoute Direct [Media Access Control-Sicherheit (MACsec)](https://docs.microsoft.com/azure/expressroute/expressroute-howto-MACsec), um Datenverkehr auf Ebene 2 zwischen den Routern Ihrer Organisation und MSEE zu verschlüsseln. Dies wird im obigen Diagramm in `Flow B` veranschaulicht.

- Für Virtual WAN-Szenarien, bei denen MACsec keine Option ist (z. B. keine Verwendung von ExpressRoute Direct), verwenden Sie ein Virtual WAN-Gateway, um IPsec-Tunnel über privates ExpressRoute-Peering einzurichten. Dies wird im obigen Diagramm in `Flow C` veranschaulicht.

- Für Nicht-Virtual WAN-Szenarien, bei denen MACsec keine Option ist (z. B. keine Verwendung von ExpressRoute Direct), gibt es derzeit nur die Möglichkeiten, mit Drittanbieter-NVAs IPsec-Tunnel über privates ExpressRoute-Peering einzurichten oder einen VPN-Tunnel über ExpressRoute mit Microsoft-Peering einzurichten.

- Wenn Datenverkehr zwischen Azure-Regionen verschlüsselt werden muss, verbinden Sie VNets mit VPN-Gateways regionsübergreifend.

- Verwenden Sie Drittanbieter-NVAs in Azure, um Datenverkehr über privates ExpressRoute-Peering zu verschlüsseln, falls in Azure angebotene native Lösungen (wie in den obigen Abläufen B und C dargestellt) Ihre Anforderungen nicht erfüllen.

## <a name="planning-for-traffic-inspection"></a>Planen der Datenverkehrsüberprüfung

In vielen Branchen muss für Organisationen Datenverkehr in Azure (insbesondere eingehender und ausgehender Internetdatenverkehr) in einem Netzwerkpaketcollector zur eingehenden Überprüfung und Analyse gespiegelt werden. In diesem Abschnitt finden Sie wichtige Überlegungen und empfohlene Ansätze für Spiegelung oder Tapping von Datenverkehr in Azure Virtual Network.

**Überlegungen zum Entwurf:**

<!-- docsTest:ignore TAP -->

- [TAP für virtuelle Azure-Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-tap-overview) liegt in der Vorschauversion vor, Einzelheiten zur Verfügbarkeit müssen Sie jedoch bei `azurevnettap@microsoft.com` erfragen.

- Die Paketerfassung in Network Watcher ist generell verfügbar, Erfassungen sind jedoch auf einen maximalen Zeitraum von fünf Stunden beschränkt.

**Entwurfsempfehlungen:**

Ziehen Sie als Alternative zum TAP für virtuelle Azure-Netzwerke die folgenden Optionen in Betracht:

- Verwenden Sie das Network Watcher-Paket trotz des beschränkten Erfassungszeitraums.

- Untersuchen Sie, ob NSG-Flussprotokolle v2 die benötigte Detailstufe liefern.

- Nutzen Sie Lösungen von Drittanbietern für Szenarien, in denen eine nachhaltige eingehende Paketüberprüfung erforderlich ist.

- Entwickeln Sie keine benutzerdefinierte Lösung zum Spiegeln von Datenverkehr. Dies mag zwar für Szenarien in kleinem Maßstab akzeptabel sein, bei Szenarien im großen Stil wird jedoch aufgrund der möglicherweise auftretenden Komplexitäts- und Unterstützungsprobleme von diesem Ansatz abgeraten.
