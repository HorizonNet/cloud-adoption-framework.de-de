---
title: Netzwerktopologie und -konnektivität
description: Untersuchen Sie wichtige Entwurfsüberlegungen und -empfehlungen im Zusammenhang mit Netzwerken und Konnektivität zu, aus und innerhalb von Microsoft Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 49af307d23c997692def763772eb87d37f5b5c70
ms.sourcegitcommit: fbfd66dab002b549d3e9cbf1b7efa0099d0b7700
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93283392"
---
<!-- cSpell:ignore autoregistration BGPs MACsec MPLS MSEE onprem privatelink VPNs -->

# <a name="network-topology-and-connectivity"></a>Netzwerktopologie und -konnektivität

In diesem Artikel werden wichtige Entwurfsüberlegungen und -empfehlungen im Zusammenhang mit Netzwerken und Konnektivität, aus und innerhalb von Microsoft Azure, erläutert.

## <a name="plan-for-ip-addressing"></a>Planen der IP-Adressierung

Es ist wichtig, dass Ihre Organisation die IP-Adressierung in Azure plant, um sicherzustellen, dass an lokalen Standorten und in Azure-Regionen kein überlappender IP-Adressraum vorhanden ist.

**Überlegungen zum Entwurf:**

- Überlappende IP-Adressräume in der lokalen Umgebung und in Azure-Regionen bewirken gravierende Konflikte.

- Nach dem Erstellen Ihres virtuellen Netzwerks können Sie weitere Adressräume hinzufügen. Dieser Vorgang erfordert jedoch eine Betriebsunterbrechung, wenn das virtuelle Netzwerk bereits über das Peering virtueller Netzwerke mit einem anderen virtuellen Netzwerk verbunden ist, da das Peering gelöscht und neu erstellt werden muss.

- Fünf IP-Adressen innerhalb jedes Subnetzes sind in Azure reserviert. Berücksichtigen Sie diese Adressen, wenn Sie die Größe virtueller Netzwerke und Subnetze anpassen.

- Einige Azure-Dienste erfordern [dedizierte Subnetze](/azure/virtual-network/virtual-network-for-azure-services#services-that-can-be-deployed-into-a-virtual-network). Zu diesen Diensten gehören Azure Firewall und Azure VPN Gateway.

- Sie können Subnetze an bestimmte Dienste delegieren, um Instanzen eines Diensts im Subnetz zu erstellen.

**Entwurfsempfehlungen:**

- Planen Sie nicht überlappende IP-Adressräume für Azure-Regionen und lokale Standorte bereits im Voraus.

- Verwenden Sie IP-Adressen aus der Adresszuordnung für private Internetadressen (RFC 1918).

- In Umgebungen mit eingeschränkter Verfügbarkeit von privaten IP-Adressen (RFC 1918) sollten Sie IPv6 verwenden.

- Erstellen Sie keine unnötig großen virtuellen Netzwerke (z. B. `/16`), damit der IP-Adressraum nicht vergeudet wird.

- Erstellen Sie keine virtuellen Netzwerke, ohne den erforderlichen Adressraum im Voraus zu planen. Das Hinzufügen von Adressräumen führt zu einem Ausfall, nachdem ein virtuelles Netzwerk über das Peering virtueller Netzwerke verbunden ist.

- Verwenden Sie keine öffentlichen IP-Adressen für virtuelle Netzwerke, insbesondere, wenn die öffentlichen IP-Adressen nicht Ihrer Organisation gehören.

## <a name="configure-dns-and-name-resolution-for-on-premises-and-azure-resources"></a>Konfigurieren von DNS und der Namensauflösung für lokale Ressourcen und Azure-Ressourcen

Domain Name System (DNS) ist ein kritisches Entwurfsthema in der allgemeinen Architektur des Unternehmens. Einige Unternehmen möchten möglicherweise Ihre vorhandenen Investitionen in DNS nutzen. Andere sehen möchten vielleicht die Gelegenheit nutzen, eine Cloudlösung einzuführen, um Ihre interne DNS-Infrastruktur zu modernisieren und native Azure-Funktionen zu verwenden.

**Überlegungen zum Entwurf:**

- Sie können einen DNS-Konfliktlöser in Verbindung mit privatem Azure-DNS für die standortübergreifende Namensauflösung verwenden.

- Sie müssen möglicherweise vorhandene DNS-Lösungen lokal und in Azure nutzen.

- Ein virtuelles Netzwerk kann mit automatischer Registrierung maximal mit einer privaten DNS-Zone verknüpft werden.

- Die maximale Anzahl von privaten DNS-Zonen, mit denen ein virtuelles Netzwerk ohne aktivierte automatische Registrierung verknüpft werden kann, beträgt 1.000.

**Entwurfsempfehlungen:**

- Für Umgebungen, in denen lediglich die Namensauflösung in Azure erforderlich ist, verwenden Sie privates Azure-DNS für die Auflösung. Erstellen Sie eine delegierte Zone für die Namensauflösung (z. B. `azure.contoso.com`).

- Für Umgebungen, in denen die Namensauflösung in Azure und in der lokalen Umgebung erforderlich ist, verwenden Sie die vorhandene DNS-Infrastruktur (z. B. in Active Directory integriertes DNS). Diese muss auf mindestens zwei Azure-VMs bereitgestellt sein. Konfigurieren Sie DNS-Einstellungen in virtuellen Netzwerken, um diese DNS-Server dann zu verwenden.

- Sie können weiterhin eine Azure-Zone mit privatem DNS mit den virtuellen Netzwerken verknüpfen und DNS-Server als Hybrid-Konfliktlöser mit bedingter Weiterleitung an lokale DNS-Namen (z. B. `onprem.contoso.com`) mit lokalen DNS-Servern verwenden. Sie haben die Möglichkeit, lokale Server mit bedingten Weiterleitungen an Konfliktlöser-VMs in Azure für die Zone mit privatem Azure-DNS (z. B. `azure.contoso.com`) zu konfigurieren.

- Für besondere Workloads, die ihr eigenes DNS erfordern und dieses bereitstellen (z. B. Red Hat OpenShift), sollte die jeweils bevorzugte DNS-Lösung verwendet werden.

- Aktivieren Sie die automatische Registrierung für Azure DNS, sodass der Lebenszyklus der DNS-Einträge für die in einem virtuellen Netzwerk bereitgestellten VMs automatisch verwaltet wird.

- Verwenden Sie einen virtuellen Computer als Konfliktlöser für die standortübergreifende DNS-Auflösung mit privatem Azure-DNS.

- Erstellen Sie die Zone mit privatem Azure-DNS in einem globalen Konnektivitätsabonnement. Sie können auch zusätzliche Zonen mit privatem Azure-DNS erstellen (z. B. `privatelink.database.windows.net` oder `privatelink.blob.core.windows.net` für Azure Private Link).

## <a name="define-an-azure-network-topology"></a>Definieren einer Azure-Netzwerktopologie

Die Netzwerktopologie ist ein wichtiges Element der unternehmensweiten Architektur, da sie bestimmt, wie Anwendungen miteinander kommunizieren können. In diesem Abschnitt werden Technologien und Topologieansätze für Azure-Unternehmensbereitstellungen behandelt. Der Schwerpunkt liegt auf zwei Hauptansätzen: Topologien basierend auf Azure Virtual WAN und herkömmlichen Topologien.

Verwenden Sie eine auf Azure Virtual WAN basierende Netzwerktopologie, wenn einer der folgenden Punkte zutrifft:

- Ihre Organisation möchte Ressourcen in mehreren Azure-Regionen bereitstellen und muss Ihre globalen Standorte sowohl mit Azure als auch mit der lokalen Umgebung verbinden.
- Ihre Organisation möchte softwaredefinierte WAN-Bereitstellungen (SD-WAN) mit vollständiger Azure-Integration verwenden.
- Sie möchten bis zu 2.000 VM-Workloads aus allen VNETs bereitstellen, die mit einem einzelnen Azure Virtual WAN-Hub verbunden sind.

Virtual WAN wird Interkonnektivitätsanforderungen in großem Stil gerecht. Da es sich um einen von Microsoft verwalteten Dienst handelt, verringert er außerdem die generelle Komplexität des Netzwerks und kann zur Modernisierung des Netzwerks in Ihrer Organisation beitragen.

Verwenden Sie eine traditionelle Azure-Netzwerktopologie, wenn einer der folgenden Punkte zutrifft:

- Ihre Organisation beabsichtigt, Ressourcen über verschiedene Azure-Regionen bereitzustellen.
- Sie können globales VNet-Peering verwenden, um virtuelle Netzwerke über Azure-Regionen hinweg zu verbinden.
- Sie verfügen über eine geringe Anzahl von Remote- oder Zweigstellenstandorten pro Region. Das heißt, Sie benötigen weniger als 30 IP-Sicherheitstunnel (IPsec).
- Sie benötigen vollständige Kontrolle und Granularität für die manuelle Konfiguration Ihres Azure-Netzwerks.

Eine traditionelle Netzwerktopologie hilft Ihnen beim Aufbau Erstellen eines sicheren, groß angelegten Netzwerks in Azure.

## <a name="virtual-wan-network-topology-microsoft-managed"></a>Virtual WAN-Netzwerktopologie (von Microsoft verwaltet)

![Diagramm zur Virtual WAN-Netzwerktopologie](./media/virtual-wan-topology.png)

_Abbildung 1: Virtual WAN-Netzwerktopologie._

**Überlegungen zum Entwurf:**

- [Azure Virtual WAN](/azure/virtual-wan/virtual-wan-about) ist eine von Microsoft verwaltete Lösung, die standardmäßig End-to-End-Konnektivität für globale Übertragungen bietet. Mit Virtual WAN-Hubs muss die Netzwerkkonnektivität nicht mehr manuell konfiguriert werden. Beispielsweise müssen Sie keine benutzerdefinierte Weiterleitung (User-Defined Routing, UDR) oder virtuelle Netzwerkgeräte (Network Virtual Appliances, NVAs) einrichten, um die Konnektivität für globale Übertragungen zu ermöglichen.

- Virtual WAN vereinfacht die End-to-End-Netzwerkkonnektivität in Azure und auch standortübergreifend, indem eine [Hub-and-Spoke-Netzwerkarchitektur](/azure/virtual-wan/virtual-wan-global-transit-network-architecture) erstellt wird. Die Architektur erstreckt sich über mehrere Azure-Regionen und lokalen Standorte (Any-to-Any-Konnektivität), wie in dieser Abbildung dargestellt:

  ![Diagramm zum globalen Übertragungsnetzwerk mit Virtual WAN](./media/global-transit.png)
  
  _Abbildung 2: Globales Transitnetzwerk mit Virtual WAN._

- Transitive Virtual WAN-Any-to-Any-Konnektivität unterstützt die folgenden Pfade (innerhalb derselben Region und zwischen Regionen):

  - Virtuelles Netzwerk zu virtuellem Netzwerk
  - Virtuelles Netzwerk zu Zweigstelle
  - Zweigstelle zu virtuellem Netzwerk
  - Zweigstelle zu Zweigstelle

- Virtuelle WAN-Hubs sind gesperrt. Die einzigen Ressourcen, die Sie darin bereitstellen können, sind virtuelle Netzwerkgateways (Point-to-Site-VPN, Site-to-Site-VPN und Azure ExpressRoute), Azure Firewall über Firewall Manager und Routingtabellen.

- Virtual WAN erhöht das Limit von bis zu 200 Präfixen, die von Azure zu lokalen Umgebungen angeboten werden, über privates ExpressRoute-Peering auf 10.000 Präfixe pro Virtual WAN-Hub. Das Limit von 10.000 Präfixen schließt auch Site-to-Site-VPN-und Point-to-Site-VPN ein.

- Transitive Konnektivität zwischen Netzwerken (innerhalb einer Region und zwischen Regionen) liegt jetzt in der allgemeinen Verfügbarkeit (GA) vor.

- Hub-zu-Hub-Verbindungen von Virtual WAN liegen jetzt in der GA vor.

- Die Transitkonnektivität zwischen den virtuellen Netzwerken unter Virtual WAN Standard wird ermöglicht, weil auf jedem virtuellen Hub ein Router vorhanden ist. Für jeden Router eines virtuellen Hubs wird ein aggregierter Durchsatz von bis zu 50 GBit/s unterstützt.

- Mit einem einzelnen Virtual WAN-Hub können bis zu 2.000 VM-Workloads aus allen VNETs verbunden werden.

- Virtual WAN ist mit einer Vielzahl von [SD-WAN-Anbietern](/azure/virtual-wan/virtual-wan-locations-partners) integriert.

- Viele Anbieter verwalteter Dienste bieten [verwaltete Dienste](/azure/networking/networking-partners-msp) für Virtual WAN.

- VPN-Gateways in Virtual WAN können auf bis zu 20 Gbit/s und 20.000 Verbindungen pro virtuellen Hub aufskaliert werden.

- ExpressRoute-Leitungen mit dem Premium-Add-On sind erforderlich. Sie sollten von einem ExpressRoute Global Reach-Standort stammen.

- Azure Firewall Manager, der jetzt in der GA vorliegt, ermöglicht das Bereitstellen von Azure Firewall im Virtual WAN-Hub.

- Virtual WAN-Hub-to-Hub-Datenverkehr über Azure Firewall wird derzeit nicht unterstützt. Verwenden Sie als Alternative die nativen Routingfunktionen für die Hub-zu-Hub-Übertragung in Virtual WAN. Verwenden Sie Netzwerksicherheitsgruppen (NSGs), um den Datenverkehr von virtuellen Netzwerken zwischen Hubs zuzulassen oder zu blockieren.

**Entwurfsempfehlungen:**

- Es empfiehlt sich, Virtual WAN für neue große oder globale Netzwerkbereitstellungen in Azure zu verwenden, bei denen eine globale Transitkonnektivität zwischen Azure-Regionen und lokalen Standorten benötigt wird. Auf diese Weise müssen Sie das transitiv Routing für Azure-Netzwerke nicht manuell einrichten.

  In der folgenden Abbildung wird ein Beispiel für eine globale Unternehmensbereitstellung mit Rechenzentren in Europa und den USA veranschaulicht. Zudem gibt es in der Bereitstellung eine große Anzahl von Zweigstellen in beiden Regionen. Die Umgebung ist global über Virtual WAN und ExpressRoute Global Reach verbunden.

  ![Diagramm einer Beispiel-Netzwerktopologie](./media/global-reach-topology.png)
  
  _Abbildung 3: Beispiel-Netzwerktopologie._

- Verwenden Sie Virtual WAN als Ressource für globale Konnektivität. Nutzen Sie einen Virtual WAN-Hub pro Azure-Region, um mehrere Zielzonen in Azure-Regionen über den lokalen Virtual WAN-Hub miteinander zu verbinden.

- Verbinden Sie Virtual WAN-Hubs mit lokalen Rechenzentren mithilfe von ExpressRoute.

- Stellen Sie erforderliche freigegebene Dienste, wie DNS-Server, in einer dedizierten Zielzone bereit. Erforderliche freigegebene Ressourcen können nicht auf einem Azure Virtual WAN-Hub bereitgestellt werden.

- Verbinden Sie Zweigstellen und Remotestandorte über ein Site-to-Site-VPN mit dem nächstgelegenen Virtual WAN-Hub, oder aktivieren Sie die Zweigstellenkonnektivität mit Virtual WAN über eine SD-WAN-Partnerlösung.

- Verbinden Sie Benutzer mit dem Virtual WAN-Hub über ein Point-to-Site-VPN.

- Befolgen Sie das Prinzip „Datenverkehr in Azure verbleibt in Azure“, sodass die Kommunikation über Ressourcen in Azure über das Microsoft-Backbone-Netzwerk erfolgt, auch wenn sich die Ressourcen in unterschiedlichen Regionen befinden.

- Stellen Sie Azure Firewall in Virtual WAN-Hubs zum Schützen und Filtern von Ost-West- und Süd-Nord-Datenverkehr in einer Azure-Region bereit.

- Wenn Partner-NVAs zum Schützen und Filtern des Ost/West- oder Süd/Nord-Datenverkehrs erforderlich sind, stellen Sie die NVAs in einem separaten virtuellen Netzwerk, z. B. einem virtuellen Netzwerk der NVAs, bereit. Stellen Sie eine Verbindung mit dem regionalen Virtual WAN-Hub und den Zielzonen her, die Zugriff auf NVAs benötigen. Weitere Informationen finden Sie unter [Erstellen einer Routingtabelle für den Virtual WAN-Hub für virtuelle Netzwerkgeräte](/azure/virtual-wan/virtual-wan-route-table-portal).

- Wenn Sie Netzwerktechnologien und NVAs von Partnern bereitstellen, befolgen Sie die Anweisungen des Partners, um sicherzustellen, dass keine Konflikte mit Azure-Netzwerken auftreten.

- Setzen Sie kein Transitnetzwerk auf Azure Virtual WAN auf. Virtual WAN erfüllt Anforderungen an die transitive Netzwerktopologie, wie z. B. die Möglichkeit zur Verwendung von Drittanbieter-NVAs. Das Aufbauen eines Transitnetzwerks auf Azure Virtual WAN wäre redundant und würde die Komplexität erhöhen.

- Verwenden Sie keine vorhandenen lokalen Netzwerke wie MPLS (Multiprotocol Label Switching), um Azure-Ressourcen über Azure-Regionen hinweg zu verbinden, da Azure-Netzwerktechnologien die Verbindung von Azure-Ressourcen regionsübergreifend über den Microsoft-Backbone unterstützen. Dies liegt an den Leistungs- und Betriebszeitmerkmalen des Microsoft-Backbones sowie der Vereinfachung des Routings. Dieser Vorschlag zielt auf die Leistungs- und Betriebszeitmerkmale des Microsoft-Backbones. Er unterstützt außerdem die Vereinfachung des Routings.

- Informationen zu Brownfield-Szenarien, in denen Sie aus einer Hub-Spoke-Netzwerktopologie migrieren, die nicht auf Virtual WAN basiert, finden Sie unter [Migrieren zu Azure Virtual WAN](/azure/virtual-wan/migrate-from-hub-spoke-topology).

- Erstellen Sie Azure Virtual WAN- und Azure Firewall-Ressourcen innerhalb des Konnektivitätsabonnements.

- Erstellen Sie nicht mehr als 500 virtuelle Netzwerkverbindungen pro virtuellem Virtual WAN-Hub.

- Planen Sie Ihre Bereitstellung sorgfältig, und achten Sie darauf, dass sich Ihre Netzwerkarchitektur innerhalb der [Azure Virtual WAN-Grenzwerte](/azure/azure-resource-manager/management/azure-subscription-service-limits#virtual-wan-limits) bewegt.

## <a name="traditional-azure-networking-topology"></a>Herkömmliche Azure-Netzwerktopologie

Virtual WAN bietet zwar eine große Bandbreite an leistungsstarken Funktionen, in manchen Fällen kann jedoch ein herkömmlicher Azure-Netzwerkansatz optimal sein:

- Wenn kein globales transitives Netzwerk über mehrere Azure-Regionen oder Standorte hinweg erforderlich ist. Ein Beispiel hierfür ist eine Zweigstelle in der USA, die mit einem virtuellen Netzwerk in Europa verbunden werden muss.

- Wenn Sie ein globales Netzwerk über mehrere Azure-Regionen hinweg bereitstellen müssen und globales VNet-Peering verwenden können, um virtuelle Netzwerke über Regionen hinweg zu verbinden.

- Wenn keine Notwendigkeit besteht, eine Verbindung mit einer großen Anzahl von Remotestandorten über VPN oder die Integration mit einer SD-WAN-Lösung herzustellen.

- Wenn Ihre Organisation granulare Kontrolle und Konfiguration beim Einrichten einer Netzwerktopologie Azure wünscht.

![Diagramm zur herkömmlichen Azure-Netzwerktopologie](./media/customer-managed-topology.png)

_Abbildung 4: Eine herkömmliche Azure-Netzwerktopologie._

**Überlegungen zum Entwurf:**

- Verschiedene Netzwerktopologien können mehrere virtuelle Netzwerke für die Zielzone verbinden. Beispiele hierfür sind ein großes, flaches virtuelles Netzwerk, mehrere virtuelle Netzwerke, die an mehreren ExpressRoute-Leitungen oder -Verbindungen angeschlossen sind, Hub-and-Spoke, vollständiges Mesh und Hybrid.

- Die Abonnementgrenzen werden von virtuellen Netzwerken nicht durchlaufen. Allerdings können Sie Verbindungen zwischen virtuellen Netzwerken in unterschiedlichen Abonnements herstellen, indem Sie das Peering virtueller Netzwerke, eine ExpressRoute-Leitung oder VPN-Gateways verwenden.

- Mit dem Peering virtueller Netzwerke können Sie virtuelle Netzwerke in derselben Region, über verschiedene Azure-Regionen hinweg und über verschiedene Azure Active Directory-Mandanten (Azure AD) verbinden.

- Das Peering virtueller Netzwerke und das globale Peering virtueller Netzwerke sind nicht transitiv. UDRs und NVAs sind erforderlich, um ein Transitnetzwerk zu aktivieren. Weitere Informationen finden Sie unter [Hub-Spoke-Netzwerktopologie in Azure](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke).

- Über ExpressRoute-Leitungen können Verbindungen zwischen virtuellen Netzwerken innerhalb derselben geopolitischen Region hergestellt werden; auch das Premium-Add-On kann für die Konnektivität zwischen geopolitischen Regionen verwendet werden. Beachten Sie Folgendes:

  - Datenverkehr zwischen Netzwerken kann eine längere Wartezeit zur Folge haben, da Datenverkehr die MSEE-Router (Microsoft Enterprise Edge) mühsam durchlaufen muss.

  - Die Bandbreite ist auf die ExpressRoute-Gateway-SKU beschränkt.

  - Sie müssen weiterhin UDRs bereitstellen und verwalten, wenn Sie Datenverkehr zwischen virtuellen Netzwerken untersuchen und protokollieren müssen.

- VPN-Gateways mit BGP (Border Gateway Protocol) sind innerhalb von Azure und lokal transitiv, werden jedoch nicht über ExpressRoute-Gateways übertragen.

- Wenn mehrere ExpressRoute-Leitungen mit demselben virtuellen Netzwerk verbunden sind, muss mit Verbindungsgewichtungen und BGP-Techniken ein optimaler Pfad für den Datenverkehr zwischen lokalen Standorten und Azure sichergestellt werden. Weitere Informationen finden Sie unter [Optimieren von ExpressRoute-Routing](/azure/expressroute/expressroute-optimize-routing).

- Die Verwendung von BGP-Techniken zum Beeinflussen des ExpressRoute-Routings ist eine Konfiguration außerhalb der Azure-Plattform. Ihre Organisation oder Ihr Konnektivitätsanbieter müssen die lokalen Router entsprechend konfigurieren.

- ExpressRoute-Verbindungen mit Premium-Add-Ons bieten globale Konnektivität. Die maximale Anzahl von ExpressRoute-Verbindungen pro ExpressRoute-Gateway beträgt jedoch vier.

- Während die maximale Anzahl von Peeringverbindungen zwischen virtuellen Netzwerken pro virtuellem Netzwerk 500 beträgt, beläuft sich die maximale Anzahl von Routen, die von Azure zu lokalen Standorten über privates ExpressRoute-Peering angekündigt werden können, auf 200.

- Der maximale aggregierte Durchsatz eines VPN-Gateways beträgt 10 GBit/s. Es werden bis zu 30 Standort-zu-Standort- oder Netzwerk-zu-Netzwerk-Tunnel unterstützt.

**Entwurfsempfehlungen:**

- Ziehen Sie einen Netzwerkentwurf, der auf der Hub-and-Spoke-Netzwerktopologie mit Nicht-Virtual WAN-Technologien basiert, für die folgenden Szenarios in Betracht:

  - Die Grenze für den Datenverkehr in einer Azure-Bereitstellung liegt innerhalb einer Azure-Region.

  - Eine Netzwerkarchitektur, die mehrere Azure-Regionen umfasst, wobei keine Transitkonnektivität zwischen virtuellen Netzwerken für Zielzonen in verschiedenen Regionen benötigt wird.

  - Eine Netzwerkarchitektur erstreckt sich über mehrere Azure-Regionen, und globales VNet-Peering verwendet werden, um virtuelle Netzwerke über Azure-Regionen hinweg zu verbinden.

  - Transitkonnektivität zwischen VPN- und ExpressRoute-Verbindungen ist nicht erforderlich.

  - Der Hauptkanal für die Konnektivität zwischen lokalen Standorten ist ExpressRoute, und die Anzahl der VPN-Verbindungen pro VPN-Gateway ist kleiner als 30.

  - Es besteht eine Abhängigkeit von zentralisierten NVAs und einem differenzierten Routing.

- Verwenden Sie für regionale Bereitstellungen hauptsächlich die Hub-and-Spoke-Topologie. Nutzen Sie Zielzonen für virtuelle Netzwerke, die über das Peering virtueller Netzwerke mit einem zentralen virtuellen Hub-Netzwerk für die Konnektivität zwischen lokalen Standorten über ExpressRoute verbunden sind. VPN wird für die Zweigstellenkonnektivität verwendet, Spoke-to-Spoke-Konnektivität über NVAs und UDRs sichergestellt und der Schutz für ausgehenden Datenverkehr in das Internet über NVA erfolgt. Die folgende Abbildung zeigt diese Topologie.  Dies ermöglicht der entsprechenden Datenverkehrskontrolle, die meisten Anforderungen an Segmentierung und Überprüfung zu erfüllen.

  ![Diagramm zur Hub-and-Spoke-Netzwerktopologie](./media/hub-and-spoke-topology.png)

  _Abbildung 5: Hub-Spoke-Netzwerktopologie._

- Verwenden Sie die Topologie mehrerer virtueller Netzwerke, die an mehrere ExpressRoute-Leitungen angeschlossen sind, wenn eine der folgenden Bedingungen zutrifft:

  - Sie benötigen eine hohe Isolationsebene.

  - Sie benötigen eine dedizierte ExpressRoute-Bandbreite für bestimmte Geschäftseinheiten.

  - Die maximale Anzahl von Verbindungen pro ExpressRoute-Gateway (bis zu vier) wurde erreicht.
  
  Die folgende Abbildung zeigt diese Topologie.

  ![Diagramm mit mehreren virtuellen Netzwerken, die an mehrere ExpressRoute-Leitungen angeschlossen sind.](./media/vnet-multiple-circuits.png)
  
  _Abbildung 6: Mehrere virtuelle Netzwerke sind mit mehreren ExpressRoute-Leitungen verbunden._

- Stellen Sie im virtuellen Netzwerk für den zentralen Hub eine minimale Gruppe von gemeinsamen Diensten bereit, einschließlich ExpressRoute-Gateways, VPN-Gateways (sofern erforderlich) und Azure Firewall oder Partner-NVAs (falls erforderlich). Bei Bedarf stellen Sie auch Active Directory-Domänencontroller und DNS-Server bereit.

- Stellen Sie Azure Firewall oder Partner-NVAs zum Schützen und Filtern des Ost-West- und/oder Süd-Nord-Datenverkehrs im virtuellen Netzwerk für den zentralen Hub bereit.

- Wenn Sie Partnernetzwerktechnologien oder NVAs bereitstellen, befolgen Sie die Anweisungen des Partneranbieters, um Folgendes sicherzustellen:

  - Der Anbieter unterstützt die Bereitstellung.

  - Die Anweisungen beziehen sich auf Hochverfügbarkeit und maximale Leistung.

  - Es gibt keine in Konflikt stehenden Konfigurationen mit Azure-Netzwerken vorhanden.

- Stellen Sie keine L7-Eingangs-NVAs (wie Azure Application Gateway) als gemeinsamer Dienst im virtuellen Netzwerk für den zentralen Hub bereit. Stattdessen stellen Sie diese in der jeweiligen Zielzone zusammen mit der App bereit.

- Verwenden Sie Ihr vorhandenes Netzwerk, MPLS und SD-WAN, um Zweigstellen mit dem Hauptsitz des Unternehmens zu verbinden. Transit in Azure zwischen ExpressRoute- und VPN-Gateways wird nicht unterstützt.

- Verwenden Sie für Netzwerkarchitekturen mit mehreren Hub-and-Spoke-Topologien in Azure-Regionen das globale Peering virtueller Netzwerke, um Zielzonen für virtuelle Netzwerke zu verbinden, wenn eine kleine Anzahl von Zielzonen regionsübergreifend miteinander kommunizieren muss. Dieser Ansatz bietet viele Vorteile, wie z. B. eine hohe Netzwerkbandbreite mit globalem Peering virtueller Netzwerke, die die VM-SKU zulässt. Die zentrale NVA wird jedoch umgangen, wenn eine Überprüfung oder Filterung des Datenverkehrs erforderlich ist. Dies unterliegt auch [Einschränkungen für das globale Peering virtueller Netzwerke](/azure/virtual-network/virtual-network-peering-overview#constraints-for-peered-virtual-networks).

- Wenn Sie eine Hub-and-Spoke-Netzwerkarchitektur in zwei Azure-Regionen bereitstellen und Transitkonnektivität regionsüberschreitend zwischen allen Zielzonen erforderlich ist, verwenden Sie ExpressRoute mit dualen Leitungen, um Transitkonnektivität für Zielzonen für virtuelle Netzwerke in den Azure-Regionen sicherzustellen. In diesem Szenario ist der Transit für Zielzonen innerhalb einer Region über NVA im virtuellen Netzwerk für den lokalen Hub und zwischen Regionen über eine ExpressRoute-Leitung möglich. Der Datenverkehr muss mühsam die MSEE-Router durchlaufen. Die folgende Abbildung zeigt diesen Entwurf.

  ![Diagramm zum Konnektivitätsentwurf für Zielzonen](./media/vnet-dual-circuits.png)
  
  _Abbildung 7: Zielzonen-Konnektivitätsentwurf._

- Wenn Ihr Unternehmen Hub-and-Spoke-Netzwerkarchitekturen über mehr als zwei Azure-Regionen und globale Transitkonnektivität zwischen Zielzonen benötigt, sind virtuelle Netzwerke erforderlich, die über Azure-Regionen hinweg arbeiten. Sie können diese Architektur implementieren, indem Sie eine Verbindung zwischen virtuellen Netzwerken im zentralen Hub mit globalem Peering virtueller Netzwerke herstellen und die Verwendung von UDRs und NVAs für das globale Transitrouting ermöglichen. Aufgrund der hohen Komplexität und des großen Verwaltungsaufwands wird die Überprüfung einer globalen Transitnetzwerkarchitektur mit Virtual WAN empfohlen.

- Verwenden Sie [Azure Monitor für Netzwerke (Vorschau)](/azure/azure-monitor/insights/network-insights-overview), um den End-to-End-Status Ihrer Netzwerke in Azure zu überwachen.

- Erstellen Sie nicht mehr als 200 Peeringverbindungen pro virtuellem Netzwerk im zentralen Hub. Virtuelle Netzwerke unterstützen zwar bis zu 500 Peeringverbindungen, ExpressRoute mit privatem Peering unterstützt jedoch nur die Ankündigung von bis zu 200 Präfixen von Azure zur lokalen Umgebung.

## <a name="connectivity-to-azure"></a>Konnektivität mit Azure

In diesem Abschnitt wird die Netzwerktopologie erweitert, um empfohlene Modelle für die Verbindung von lokalen Standorten mit Azure zu betrachten.

**Überlegungen zum Entwurf:**

- Azure ExpressRoute bietet dedizierte private Konnektivität für Azure-IaaS- und -PaaS-Funktionen (Infrastructure-as-a-Service und Platform-as-a-Service) von lokalen Standorten.

- Mit Private Link können Sie die Konnektivität mit PaaS-Diensten über ExpressRoute mit privatem Peering einrichten.

- Wenn mehrere virtuelle Netzwerke mit derselben ExpressRoute-Leitung verbunden sind, werden sie Teil derselben Routingdomäne, und die Bandbreite wird von allen virtuellen Netzwerken gemeinsam genutzt.

- Mit ExpressRoute Global Reach (falls verfügbar) können Sie lokale Standorte über ExpressRoute-Leitungen verbinden, um den Datenverkehr über das Microsoft-Backbone-Netzwerk zu übertragen.

- Expressroute-Global Reach ist in vielen [ExpressRoute-Peeringstandorten](/azure/expressroute/expressroute-global-reach#availability) vorhanden.

- ExpressRoute Direct ermöglicht das Erstellen von mehreren ExpressRoute-Leitungen ohne anfallende Zusatzkosten bis zur Kapazität des ExpressRoute Direct-Ports (10 GBit/s oder 100 GBit/s). Zudem lassen sich direkte Verbindungen mit den ExpressRoute-Routern von Microsoft herstellen. Bei der 100-GBit/s-SKU beträgt die Mindestbandbreite der Leitung 5 GBit/s. Bei der 10-GBit/s-SKU beträgt die Mindestbandbreite der Leitung 1 GBit/s.

**Entwurfsempfehlungen:**

- Verwenden Sie ExpressRoute als primären Konnektivitätskanal für Verbindungen zwischen einem lokalen Netzwerk und Azure. Sie können VPNs als Quelle für die Sicherungskonnektivität verwenden, um die Resilienz der Konnektivität zu verbessern.

- Verwenden Sie duale ExpressRoute-Leitungen von verschiedenen Peeringstandorten, wenn Sie eine Verbindung eines lokalen Standorts mit virtuellen Netzwerken in Azure herstellen. Durch dieses Setup werden redundante Pfade zu Azure sichergestellt, da Single Points of Failure zwischen dem lokalen Standort und Azure beseitigt werden.

- Wenn Sie mehrere ExpressRoute-Leitungen verwenden, [optimieren Sie das ExpressRoute-Routing über die lokale BGP-Einstellung und Voranstellen von AS PATH](/azure/expressroute/expressroute-optimize-routing#solution-use-as-path-prepending).

- Stellen Sie sicher, dass Sie die richtige SKU für ExpressRoute-/VPN-Gateways nutzen, entsprechend den Anforderungen in Bezug auf Bandbreite und Leistung.

- Stellen Sie ein zonenredundantes ExpressRoute-Gateway in den unterstützten Azure-Regionen bereit.

- Verwenden Sie ExpressRoute Direct für Szenarien, in denen eine Bandbreite von mehr als 10 GBit/s oder dedizierte 10/100 GBit/s-Ports benötigt werden.

- Wird eine geringe Latenzzeit benötigt oder muss der Durchsatz zwischen einem lokalen Standort und Azure mehr als 10 GBit/s betragen, aktivieren Sie FastPath, um das ExpressRoute-Gateway vom Datenpfad zu umgehen.

- Verwenden Sie VPN-Gateways, um Zweigstellen oder Remotestandorte mit Azure zu verbinden. Stellen Sie für eine höhere Resilienz zonenredundante Gateways bereit (soweit verfügbar).

- Verwenden Sie ExpressRoute Global Reach, um große Niederlassungen, regionale Zentralen oder Rechenzentren zu verbinden, die über ExpressRoute mit Azure verbunden sind.

- Wenn die Isolation von Datenverkehr oder dedizierte Bandbreite benötigt wird, z. B. zum Trennen von Produktions- und Nicht-Produktionsumgebungen, sollten verschiedene ExpressRoute-Leitungen verwendet werden. So können Sie isolierte Routingdomänen sicherstellen und das Risiko der Beeinträchtigung durch andere Dienste („Noisy Neighbors“) mindern.

- Überwachen Sie ExpressRoute-Leitungen proaktiv mit dem Netzwerkleistungsmonitor.

- Verwenden Sie ExpressRoute-Leitungen nicht explizit von einem einzelnen Peeringstandort aus. Dadurch wird ein Single Point of Failure erstellt und Ihre Organisation anfällig für Peeringstandortausfälle.

- Verwenden Sie nicht dieselbe ExpressRoute-Leitung zum Verbinden mehrerer Umgebungen, die Isolation oder dedizierte Bandbreite benötigen, um das Noisy-Neighbor-Risiko zu mindern.

## <a name="connectivity-to-azure-paas-services"></a>Konnektivität mit Azure PaaS-Diensten

Aufbauen auf den vorigen Abschnitten zur Konnektivität werden in diesem Abschnitt empfohlene Ansätze hinsichtlich der Konnektivität bei der Verwendung von Azure PaaS-Diensten erläutert.

**Überlegungen zum Entwurf:**

- Der Zugriff auf Azure PaaS-Dienste erfolgt in der Regel über öffentliche Endpunkte. Die Azure-Plattform bietet jedoch Funktionen, mit denen solche Endpunkte gesichert oder sogar vollständig eingerichtet werden können:

  - Die Einschleusung von virtuellen Netzwerken ermöglicht dedizierte private Bereitstellungen für unterstützte Dienste. Der Datenverkehr auf der Verwaltungsebene fließt jedoch über öffentliche IP-Adressen.

  - [Private Link](/azure/private-link/private-endpoint-overview#private-link-resource) bietet über private IP-Adressen dedizierten Zugriff auf Azure PaaS-Instanzen bzw. benutzerdefinierte Dienste hinter einem Azure Load Balancer-Standard.

  - VNET-Dienstendpunkte bieten aus ausgewählten Subnetzen Zugriff auf der Dienstebene auf ausgewählte PaaS-Dienste.

- Unternehmen haben häufig Bedenken in Bezug auf öffentliche Endpunkte für PaaS-Dienste, die entsprechend adressiert werden müssen.

- Für [unterstützte Dienste](/azure/private-link/private-link-overview#availability) adressiert Private Link die Datenexfiltrationsprobleme an Dienstendpunkten. Alternativ können Sie über Filterung ausgehenden Datenverkehrs über NVAs Schritte ergreifen, um das Risiko der Datenexfiltration zu mindern.

**Entwurfsempfehlungen:**

- Verwenden Sie die Einschleusung von virtuellen Netzwerken für unterstützte Azure-Dienste, um diese aus Ihrem virtuellen Netzwerk verfügbar zu machen.

- Azure PaaS-Dienste, die in ein virtuelles Netzwerk eingeschleust wurden, führen immer noch Vorgänge auf der Verwaltungsebene mit öffentlichen IP-Adressen durch. Stellen Sie mit benutzerdefinierten Routen und Netzwerksicherheitsgruppen sicher, dass diese Kommunikation im virtuellen Netzwerk gesperrt wird.

- Verwenden Sie Private Link, [sofern verfügbar](/azure/private-link/private-link-overview#availability), für die freigegebenen Azure PaaS-Dienste. Private Link ist für einige Dienste allgemein verfügbar und liegt für eine Vielzahl von Diensten in der öffentlichen Vorschauversion vor.

- Greifen Sie vom lokalen Standort aus über das private ExpressRoute-Peering auf Azure PaaS-Dienste zu. Verwenden Sie entweder die Einschleusung virtueller Netzwerke für dedizierte Azure-Dienste oder Azure Private Link für verfügbare freigegebene Azure-Dienste. Verwenden Sie ExpressRoute mit Microsoft-Peering, um von einem lokalen Standort aus auf Azure PaaS-Dienste zuzugreifen, wenn die Einschleusung virtueller Netzwerke und Private Link nicht verfügbar sind. Dadurch wird der Transit über das öffentliche Internet vermieden.

- Verwenden Sie VNET-Dienstendpunkte, um den Zugriff auf Azure PaaS-Dienste aus Ihrem virtuellen Netzwerk zu schützen. Dies gilt jedoch nur, wenn Private Link nicht verfügbar ist, und keine Risiken der Datenexfiltration bestehen. Verwenden Sie zum Adressieren von Risiken der Datenexfiltration bei Dienstendpunkten NVA-Filterung oder Richtlinien zu VNET-Dienstendpunkten für Azure Storage.

- Aktivieren Sie VNET-Dienstendpunkte nicht standardmäßig in allen Subnetzen.

- Verwenden Sie keine VNET-Dienstendpunkte, wenn Risiken hinsichtlich der Datenexfiltration vorliegen, es sei denn, Sie verwenden die NVA-Filterung.

- Es wird nicht empfohlen, die Tunnelerzwingung zu implementieren, um die Kommunikation zwischen Azure und Azure-Ressourcen zu ermöglichen.

## <a name="plan-for-inbound-and-outbound-internet-connectivity"></a>Planen der eingehenden und ausgehenden Internetkonnektivität

In diesem Abschnitt werden empfohlene Konnektivitätsmodelle für die eingehende und ausgehende Konnektivität zum und aus dem öffentlichen Internet beschrieben.

**Überlegungen zum Entwurf:**

- Native Azure-Netzwerksicherheitsdienste wie Azure Firewall, Azure Web Application Firewall (WAF) auf Azure Application Gateway und Azure Front Door Service sind vollständig verwaltete Dienste. Sie verursachen also keine Betriebs- und Verwaltungskosten im Zusammenhang mit Infrastrukturbereitstellungen, die bei der Skalierung komplex werden können.

- Die Architektur auf Unternehmensebene ist vollständig kompatibel mit Partner-NVAs, wenn Ihre Organisation die Verwendung von NVAs bevorzugt oder native Dienste den konkreten Anforderungen Ihrer Organisation nicht gerecht werden.

**Entwurfsempfehlungen:**

- Verwenden Sie Azure Firewall, um Folgendes zu steuern:

  - Ausgehender Azure-Datenverkehr zum Internet

  - Eingehende Nicht-HTTP/S-Verbindungen

  - Filtern von Ost-West-Datenverkehr (falls von Ihrer Organisation gefordert)

- Verwenden Sie Firewall Manager mit Virtual WAN, um Azure-Firewalls für Virtual WAN-Hubs oder in virtuellen Netzwerken im Hub bereitzustellen und zu verwalten. Firewall Manager liegt jetzt sowohl für Virtual WAN als auch für normale virtuelle Netzwerke in der GA vor.

- Erstellen Sie eine globale Azure Firewall-Richtlinie, um den Sicherheitsstatus in der globalen Netzwerkumgebung zu steuern, und weisen Sie sie allen Azure Firewall-Instanzen zu. Erfüllen Sie anhand präziser Richtlinien die Anforderungen bestimmter Regionen, indem Sie inkrementelle Firewall-Richtlinien über die rollenbasierte Zugriffssteuerung an lokale Sicherheitsteams delegieren.

- Konfigurieren Sie unterstützte Partner von Saas-Sicherheitslösungen in Firewall Manager, wenn Ihre Organisation derartige Lösungen zum Schutz ausgehender Verbindungen verwenden möchte.

- Verwenden Sie WAF in einem virtuellen Netzwerk in einer Zielzonen zum Schützen eingehenden HTTP/S-Datenverkehrs aus dem Internet.

- Verwenden Sie Azure Front Door Service- und WAF-Richtlinien, um über Azure-Regionen hinweg globalen Schutz für eingehende HTTP/S-Verbindungen mit einer Zielzone bereitzustellen.

- Wenn Sie Azure Front Door Service und Azure Application Gateway zum Schutz von HTTP/S-Apps nutzen, verwenden Sie WAF-Richtlinien in Azure Front Door Service. Sperren Sie Azure Application Gateway, um nur Datenverkehr von Azure Front Door Service zu empfangen.

- Wenn Partner-NVAs zum Schützen und Filtern von Ost-West- oder Süd-Nord-Datenverkehr benötigt werden:

  - Stellen Sie die NVAs bei Virtual WAN-Netzwerktopologien in einem separaten virtuellen Netzwerk bereit (z. B. virtuelles Netzwerk in NVA). Stellen Sie dann eine Verbindung mit dem regionalen Virtual WAN-Hub und den Zielzonen her, die Zugriff auf NVAs benötigen. Der Prozess wird in [diesem Artikel](/azure/virtual-wan/virtual-wan-route-table-portal) beschrieben.
  - Stellen Sie für Nicht-Virtual WAN-Netzwerktopologien die Partner-NVAs im virtuellen Netzwerk des zentralen Hubs bereit.

- Wenn Partner-NVAs für eingehende HTTP/S-Verbindungen erforderlich sind, stellen Sie sie in einem virtuellen Netzwerk in einer Zielzone und zusammen mit den Apps bereit, die sie schützen und für das Internet verfügbar machen.

- Schützen Sie mit [Azure DDoS Protection Standard-Schutzplänen](/azure/virtual-network/ddos-protection-overview) alle öffentlichen Endpunkte, die in Ihren virtuellen Netzwerken gehostet werden.

- Replizieren Sie keine lokalen Umkreisnetzwerkkonzepte und -architekturen in Azure. Ähnliche Sicherheitsfunktionen sind in Azure verfügbar, aber die Implementierung und die Architektur müssen an die Cloud angepasst werden.

## <a name="plan-for-app-delivery"></a>Planen der Bereitstellung von Apps

Dieser Abschnitt enthält wichtige Empfehlungen zum Bereitstellen von internen und öffentlichen Apps, wobei höchste Sicherheit, hohe Skalierbarkeit und Hochverfügbarkeit gewährleistet werden.

**Überlegungen zum Entwurf:**

- Azure Load Balancer (intern und öffentlich) bietet Hochverfügbarkeit für die Bereitstellung von Apps auf regionaler Ebene.

- Azure Application Gateway ermöglicht die sichere Bereitstellung von HTTP/S-Apps auf regionaler Ebene.

- Azure Front Door Service ermöglicht die sichere Bereitstellung von hochverfügbaren HTTP/S-Apps über Azure-Regionen hinweg.

- Azure Traffic Manager ermöglicht die Bereitstellung von globalen Apps.

**Entwurfsempfehlungen:**

- Führen Sie die App-Bereitstellung innerhalb von Zielzonen sowohl für interne als auch für öffentliche Apps durch.

- Verwenden Sie für die sichere Bereitstellung von HTTP/S-Apps Application Gateway v2, und stellen Sie sicher, dass WAF-Schutz und -Richtlinien aktiviert sind.

- Verwenden Sie ein Partner-NVA, wenn Sie Application Gateway v2 nicht für die Sicherheit von HTTP/S-Apps verwenden können.

- Stellen Sie Azure Application Gateway v2 oder für eingehende HTTP/S-Verbindungen verwendete Partner-NVAs in virtuellen Netzwerk der Zielzone und mit den sichernden Apps bereit.

- Verwenden Sie für alle öffentlichen IP-Adressen in einer Zielzone einen DDoS-Standardschutzplan.

- Verwenden Sie Azure Front Door Service mit WAF-Richtlinien, um globale HTTP/S-Apps, die sich über Azure-Regionen erstrecken, bereitzustellen und zu schützen.

- Wenn Sie Azure Front Door Service und Application Gateway zum Schutz von HTTP/S-Apps nutzen, verwenden Sie WAF-Richtlinien in Azure Front Door Service. Sperren Sie Application Gateway, um nur Datenverkehr von Azure Front Door Service zu empfangen.

- Mithilfe von Traffic Manager können Sie globale Apps bereitstellen, die andere Protokolle als HTTP/S umfassen.

## <a name="plan-for-landing-zone-network-segmentation"></a>Planen der Zielzonen-Netzwerksegmentierung

In diesem Abschnitt werden wichtige Empfehlungen für die Bereitstellung höchst sicherer interner Netzwerksegmentierung innerhalb einer Zielzone erläutert, mit denen eine Netzwerk-Zero-Trust-Implementierung gefördert wird.

**Überlegungen zum Entwurf:**

- Das Zero-Trust-Modell geht davon aus, dass ein Verstoß vorliegt, und jede Anforderung wird so verifiziert, als ob sie aus einem nicht kontrollierten Netzwerk stammen würde.

- Eine erweiterte Implementierung eines Zero-Trust-Netzwerks umfasst vollständig verteilte Mikroparameter für eingehenden/ausgehenden Clouddatenverkehr und tiefere Mikrosegmentierung.

- Netzwerksicherheitsgruppen können Azure-Diensttags verwenden, um die Konnektivität mit Azure PaaS-Diensten zu ermöglichen.

- App-Sicherheitsgruppen bieten keinen Schutz zwischen virtuellen Netzwerken.

- NSG-Datenflussprotokolle werden nun durch Azure Resource Manager-Vorlagen unterstützt.

**Entwurfsempfehlungen:**

- Delegieren Sie die Subnetzerstellung an den Zielzonenbesitzer. Dadurch kann dieser festlegen, wie Workloads über Subnetze segmentiert werden (z. B. ein einziges großes Subnetz, mehrschichtige App oder in das Netzwerk integrierte App). Das Plattformteam kann mithilfe von Azure Policy sicherstellen, dass Subnetzen mit Richtlinien vom Typ „Immer verweigern“ immer ein NSG mit bestimmten Regeln (z. B. eingehenden SSH oder RDP aus dem Internet verweigern oder Datenverkehr zwischen Zielzonen zulassen/blockieren) zugeordnet ist.

- Verwenden Sie NSGs, um den subnetzübergreifenden Datenverkehr sowie den plattformübergreifenden Ost-West-Datenverkehr (Datenverkehr zwischen Zielzonen) zu schützen.

- Das App-Team muss mit App-Sicherheitsgruppen auf Subnetzebenen-NSGs mehrschichtige VMs in der Zielzone schützen.

- Verwenden Sie NSGs und App-Sicherheitsgruppen zum Mikrosegmentieren von Datenverkehr in der Zielzone, filtern Sie Datenverkehrsströme nach Möglichkeit nicht mit einer zentralen NVA.

- Aktivieren Sie NSG-Datenflussprotokolle und speisen Sie diese in Traffic Analytics ein, um Erkenntnisse zu internen und externen Datenverkehrsflüssen zu gewinnen.

- Verwenden Sie NSGs, um die Konnektivität zwischen Zielzonen selektiv zuzulassen.

- Leiten Sie bei Virtual WAN-Topologien Datenverkehr über Zielzonen hinweg per Azure Firewall weiter, wenn Ihre Organisation Filter- und Protokollierungsfunktionen für Datenverkehr benötigt, der zwischen Zielzonen fließt.

## <a name="define-network-encryption-requirements"></a>Definieren von Netzwerkverschlüsselungsanforderungen

In diesem Abschnitt werden wichtige Empfehlungen zum Einrichten der Netzwerkverschlüsselung zwischen der lokalen Umgebung und Azure sowie über Azure-Regionen hinweg behandelt.

**Überlegungen zum Entwurf:**

- Kosten und verfügbare Bandbreite sind umgekehrt proportional zur Länge des Verschlüsselungstunnels zwischen Endpunkten.

- Wenn Sie mit VPN eine Verbindung mit Azure herstellen, wird der Datenverkehr über das Internet über IPsec-Tunnel (IP Security) verschlüsselt.

- Bei Verwendung von ExpressRoute mit privatem Peering wird Datenverkehr derzeit nicht verschlüsselt.

- Konfigurieren einer Site-to-Site-VPN-Verbindung über privates ExpressRoute-Peering befindet sich jetzt in der [Vorschauphase](https://docs.microsoft.com/azure/vpn-gateway/site-to-site-vpn-private-peering).

- Sie können die Verschlüsselung [Media Access Control Security (MACsec)](/azure/expressroute/expressroute-howto-MACsec) auf ExpressRoute Direct anwenden, um eine Netzwerkverschlüsselung zu erreichen.

- Wenn Azure-Datenverkehr zwischen Rechenzentren (außerhalb physischer Grenzen, die nicht von Microsoft oder im Auftrag von Microsoft kontrolliert werden) bewegt wird, wird auf der zugrunde liegenden Netzwerkhardware eine [MACsec-Verschlüsselung der Sicherungsschicht](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview#encryption-of-data-in-transit) verwendet. Dies gilt für VNET-Peeringdatenverkehr.

**Entwurfsempfehlungen:**

![Diagramm mit den Datenflüssen bei der Verschlüsselung](./media/enc-flows.png)

_Abbildung 8: Verschlüsselungsabläufe._

- Beim Einrichten von VPN-Verbindungen von einer lokalen Umgebung über VPN-Gateways mit Azure wird Datenverkehr auf einer Protokollebene durch IPsec-Tunnel verschlüsselt. Dies wird im obigen Diagramm in Datenfluss `A` veranschaulicht.

- Konfigurieren Sie bei Verwendung von ExpressRoute Direct [MACsec](/azure/expressroute/expressroute-howto-MACsec), um Datenverkehr auf Ebene 2 zwischen den Routern Ihrer Organisation und MSEE zu verschlüsseln. Dies wird im Diagramm in Datenfluss `B` veranschaulicht.

- Für Virtual WAN-Szenarios, bei denen MACsec keine Option darstellt (z. B. keine Verwendung von ExpressRoute Direct), verwenden Sie ein Virtual WAN-VPN-Gateway, um [IPsec-Tunnel über privates ExpressRoute-Peering](https://docs.microsoft.com/azure/virtual-wan/vpn-over-expressroute) einzurichten. Dies wird im Diagramm in Datenfluss `C` veranschaulicht.

- Bei Szenarios ohne Virtual WAN, in denen MACsec keine Option ist (z. B. keine Verwendung von ExpressRoute Direct), gibt es nur die folgenden Optionen:
  
  - Verwenden Sie Partner-NVAs, um IPsec-Tunnel über das private ExpressRoute-Peering einzurichten.
  - Richten Sie mit Microsoft-Peering einen VPN-Tunnel über ExpressRoute ein.
  - Evaluieren Sie die Funktion zum Konfigurieren einer Site-to-Site-VPN-Verbindung über privates ExpressRoute-Peering ([in Vorschauphase](https://docs.microsoft.com/azure/vpn-gateway/site-to-site-vpn-private-peering)).

- Wenn Datenverkehr zwischen Azure-Regionen verschlüsselt werden muss, nutzen Sie globales VNet-Peering, um virtuelle Netzwerke regionsübergreifend zu verbinden.

- Wenn native Azure-Lösungen (wie in den Datenflüssen `B` und `C` im Diagramm dargestellt) Ihren Anforderungen nicht entsprechen, verwenden Sie Partner-NVAs in Azure, um den Datenverkehr über das private ExpressRoute-Peering zu verschlüsseln.

## <a name="plan-for-traffic-inspection"></a>Planen der Datenverkehrsüberprüfung

In vielen Branchen muss für Organisationen Datenverkehr in Azure in einem Netzwerkpaketcollector zur eingehenden Überprüfung und Analyse gespiegelt werden. Diese Anforderung bezieht sich in der Regel auf eingehenden und ausgehenden Internetdatenverkehr. In diesem Abschnitt finden Sie wichtige Überlegungen und empfohlene Ansätze für Spiegelung oder Tapping von Datenverkehr in Azure Virtual Network.

**Überlegungen zum Entwurf:**

<!-- docutune:ignore TAP -->

- [Terminalzugangspunkt (Terminal Access Point, TAP) für virtuelle Netzwerke in Azure](/azure/virtual-network/virtual-network-tap-overview) ist als Vorschauversion verfügbar. Weitere Informationen zur Verfügbarkeit erhalten Sie bei `azurevnettap@microsoft.com`.

- Die Paketerfassung in Azure Network Watcher ist generell verfügbar, Erfassungen sind jedoch auf einen maximalen Zeitraum von fünf Stunden beschränkt.

**Entwurfsempfehlungen:**

Ziehen Sie als Alternative zum TAP für virtuelle Azure-Netzwerke die folgenden Optionen in Betracht:

- Verwenden Sie das Network Watcher-Paket trotz des beschränkten Erfassungszeitraums.

- Evaluieren Sie, ob die neueste Version der NSG-Datenflussprotokolle die von Ihnen benötigte Detailtiefe bietet.

- Verwenden Sie Partnerlösungen für Szenarios, die eine umfassende Paketuntersuchung erfordern.

- Entwickeln Sie keine benutzerdefinierte Lösung zum Spiegeln von Datenverkehr. Dies mag zwar für Szenarios in kleinem Maßstab akzeptabel sein, bei Szenarios im großen Stil wird jedoch aufgrund der möglicherweise auftretenden Komplexitäts- und Unterstützungsprobleme von diesem Ansatz abgeraten.
