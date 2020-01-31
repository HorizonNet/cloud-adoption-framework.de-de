---
title: Umkreisnetzwerke
description: Umkreisnetzwerke
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 6125a428d67130d891623a30ca75a11527fbbe23
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76799776"
---
# <a name="perimeter-networks"></a>Umkreisnetzwerke

[Umkreisnetzwerke][perimeter-network] sorgen für sichere Konnektivität zwischen Ihren Cloudnetzwerken und Ihren lokalen oder physischen Datencenternetzwerken (sowie für Internetkonnektivität). Sie werden auch als „entmilitarisierte Zonen“ (DMZ) bezeichnet.

Damit Umkreisnetzwerke effektiv sind, müssen eingehende Pakete über Sicherheitsgeräte geleitet werden, die in sicheren Subnetzen gehostet werden, bevor sie zu Back-End-Servern gelangen. Beispiele hierfür sind Firewall, Angriffserkennungssysteme (IDS) und Eindringschutzsysteme (IPS). Von Workloads an das Internet gesendete Pakete sollten ebenfalls über die Sicherheitsgeräte im Umkreisnetzwerk geleitet werden, bevor sie das Netzwerk verlassen. Dieser Fluss dient der Richtlinienerzwingung, Überprüfung und Überwachung.

Umkreisnetzwerken nutzen die folgenden Azure-Funktionen und -Dienste:

- [Virtuelle Netzwerke][virtual-networks], [benutzerdefinierte Routen][user-defined-routes] und [Netzwerksicherheitsgruppen][network-security-groups]
- [Virtuelle Netzwerkgeräte (NVAs)][NVA]
- [Azure-Lastenausgleich][ALB]
- [Azure Application Gateway][AppGW] und [Web Application Firewall (WAF)][AppGWWAF]
- [Öffentliche IP-Adressen][PIP]
- [Azure Front Door][AFD] mit [Web Application Firewall][AFDWAF]
- [Azure Firewall][AzFW]

> [!NOTE]
> Azure-Referenzarchitekturen bieten Beispielvorlagen, die Sie für die Implementierung Ihrer eigenen Umkreisnetzwerke verwenden können:
>
> - [Implementieren einer DMZ zwischen Azure und Ihrem lokalen Rechenzentrum](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid)
> - [Implementieren einer DMZ zwischen Azure und dem Internet](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

In der Regel sind Ihre zentralen IT- und Sicherheitsteams für die Anforderungendefinition und den Betrieb Ihrer Umkreisnetzwerke verantwortlich.

![Beispiel zur Hub-and-Spoke-Netzwerktopologie][7]

Die obige Abbildung zeigt ein Beispiel einer [Hub-and-Spoke-Netzwerktopologie](./hub-spoke-network-topology.md), das die Durchsetzung von zwei Perimetern mit Zugriff auf das Internet und ein lokales Netzwerk implementiert. Beide Perimeter befinden sich im DMZ-Hub. Im DMZ-Hub kann das Umkreisnetzwerk für das Internet zentral hochskaliert werden, um viele Branchenanwendungen (LOBs) zu unterstützen, indem mehrere Farmen von WAFS und Azure-Firewallinstanzen verwendet werden, die zum Schutz der virtuellen Spokenetzwerks beitragen. Der Hub ermöglicht je nach Bedarf außerdem Konnektivität über VPN oder Azure ExpressRoute.

## <a name="virtual-networks"></a>Virtuelle Netzwerke

Umkreisnetzwerke werden normalerweise mithilfe eines [virtuellen Netzwerks][virtual-networks] mit mehreren Subnetzen erstellt, um verschiedene Arten von Diensten zu hosten, die den Internetdatenverkehr über virtuelle Netzwerkgeräte, WAFs und Azure Application Gateway-Instanzen filtern und überprüfen.

## <a name="user-defined-routes"></a>Benutzerdefinierte Routen

Mit [benutzerdefinierten Routen][user-defined-routes] können Kunden Firewalls, IDS- oder IPS-Geräte und andere virtuelle Geräte bereitstellen. Kunden können den Netzwerkdatenverkehr zum Erzwingen von Sicherheitsrichtlinien, zur Überwachung und zur Überprüfung über diese Sicherheitsgeräte routen. Benutzerdefinierte Routen können erstellt werden, um sicherzustellen, dass Datenverkehr durch die spezifischen benutzerdefinierten VMs, NVAs und Lastenausgleichsmodule geleitet wird.

In einem Hub-and-Spoke-Netzwerkbeispiel erfordert die Gewährleistung, dass Datenverkehr, der von VMs erzeugt wird, die sich in der Spoke befinden, durch die richtigen virtuellen Geräte im Hub geleitet wird, eine benutzerdefinierte Route, die in den Subnetzen der Spoke definiert ist. Diese Route legt die Front-End-IP-Adresse des internen Lastenausgleichs als nächsten Hop fest. Der interne Load Balancer verteilt den internen Datenverkehr auf die virtuellen Geräte (Back-End-Pool des Load Balancers).

## <a name="azure-firewall"></a>Azure Firewall

[Azure Firewall][AzFW] ist ein verwalteter, cloudbasierter Netzwerksicherheitsdienst zum Schutz Ihrer Azure Virtual Network-Ressourcen. Es handelt sich dabei um eine vollständig zustandsbehaftete verwaltete Firewall mit integrierter Hochverfügbarkeit und uneingeschränkter Cloudskalierbarkeit. Sie können Richtlinien zur Anwendungs- und Netzwerkkonnektivität übergreifend für Abonnements und virtuelle Netzwerke zentral erstellen, erzwingen und protokollieren.

Azure Firewall verwendet eine statische öffentliche IP-Adresse für Ihre virtuellen Netzwerkressourcen. Dadurch können externe Firewalls Datenverkehr aus Ihrem virtuellen Netzwerk identifizieren. Der Dienst arbeitet für Protokollierung und Analyse mit Azure Monitor zusammen.

## <a name="network-virtual-appliances"></a>Virtuelle Netzwerkgeräte

Umkreisnetzwerke mit Zugriff auf das Internet werden in der Regel über eine Azure Firewall-Instanz oder eine Farm von Firewalls oder [Webanwendungsfirewalls][AFDWAF] verwaltet.

In verschiedenen Branchen werden häufig viele Webanwendungen verwendet. Diese Anwendungen weisen häufig unterschiedliche Sicherheitsrisiken und Exploits auf. Eine Web Application Firewall erkennt Angriffe auf Webanwendungen (HTTP/HTTPS) genauer als eine generische Firewall. Verglichen mit herkömmlichen Firewalls stellen Web Application Firewalls einen Satz von bestimmten Features bereit, um den internen Webserver vor Bedrohungen zu schützen.

Eine Azure Firewall-Instanz und eine Firewall eines [virtuellen Netzwerkgeräts][NVA] werden jeweils über eine gemeinsame Verwaltungsebene mit einem Satz von Sicherheitsregeln ausgeführt, die die in den Spokes gehosteten Workloads schützen und den Zugriff auf lokale Netzwerke steuern. Azure Firewall verfügt über integrierte Skalierbarkeit, während NVA-Firewalls hinter einem Lastenausgleich manuell skaliert werden können.

Eine Firewallfarm verfügt im Allgemeinen im Vergleich zu einer Web Application Firewall über weniger spezialisierte Software. Sie hat jedoch einen umfassenderen Anwendungsbereich, sodass sie alle Arten von ein- und ausgehendem Datenverkehr filtern und überprüfen kann. Wenn Sie einen NVA-Ansatz verwenden, können Sie Software in Azure Marketplace ermitteln und bereitstellen.

Verwenden Sie eine Gruppe von Azure Firewall-Instanzen (oder virtuelle Netzwerkgeräte) für Datenverkehr aus dem Internet und eine andere Gruppe für Datenverkehr mit lokalem Ursprung. Die Verwendung einer einzigen Gruppe von Firewalls für den gesamten Datenverkehr stellt ein Sicherheitsrisiko dar, da sie keinen wirksamen Sicherheitsbereich zwischen den beiden Arten von Netzwerkdatenverkehr bietet. Separate Firewallebenen vereinfachen die Überprüfung von Sicherheitsregeln und ermöglichen eine eindeutige Zuordnung von Regeln zu eingehenden Netzwerkanforderungen.

## <a name="azure-load-balancer"></a>Azure Load Balancer

[Azure Load Balancer][ALB] stellt einen Dienst mit hoher Verfügbarkeit der Ebene 4 (TCP, UDP) bereit, mit dem eingehender Datenverkehr zwischen Dienstinstanzen verteilt werden kann, die in einer Gruppe mit Lastenausgleich definiert sind. Der Datenverkehr, der von den Front-End-Endpunkten (öffentliche IP-Endpunkte oder private IP-Endpunkte) an den Load Balancer gesendet wird, kann mit oder ohne Adressübersetzung auf einen Pool von Back-End-IP-Adressen weiterverteilt werden (z.B. NVAs oder VMs).

Azure Load Balancer kann auch die Integrität der verschiedenen Serverinstanzen testen. Wenn eine Instanz nicht auf einen Test reagiert, sendet der Lastenausgleich keinen weiteren Datenverkehr an die fehlerhafte Instanz.

Als Beispiel für die Verwendung einer Hub-and-Spoke-Netzwerktopologie kann ein externer Lastausgleich sowohl für den Hub als auch für die Spokes bereitgestellt werden. Im Hub leitet der Lastenausgleich Datenverkehr effizient an Dienste in den Spokes weiter. In den Spokes verwalten Lastenausgleichsmodule Anwendungsdatenverkehr.

## <a name="azure-front-door-service"></a>Azure Front Door Service

[Azure Front Door Service][AFD] von Microsoft stellt eine hochverfügbare und hochgradig skalierbare Plattform für die Beschleunigung von Webanwendungen und einen globalen HTTPS-Lastenausgleich bereit. Sie können Azure Front Door Service verwenden, Ihre dynamischen Webanwendungen und statischen Inhalte zu erstellen, auszuführen und horizontal zu skalieren. Azure Front Door Service wird an mehr als 100 Standorten im Edgebereich des globalen Netzwerks von Microsoft ausgeführt.

Azure Front Door Service stellt für Ihre Anwendung einheitliche Automatisierung der Regions-/Stempelwartung, BCDR-Automatisierung, einheitliche Client-/Benutzerinformationen, Zwischenspeicherung und Erkenntnisse zu Ihren Diensten bereit. Die Plattform bietet Leistung, Zuverlässigkeit, Support-SLAs. Außerdem bietet sie Konformitätszertifizierungen und überwachbare Sicherheitsverfahren, die von Azure entwickelt, betrieben und nativ unterstützt werden.

## <a name="application-gateway"></a>Application Gateway

[Azure Application Gateway][AppGW] ist eine dedizierte virtuelle Appliance, mit der ein verwalteter Application Delivery Controller (ADC) als Dienst bereitgestellt wird. Es bietet verschiedene Lastenausgleichsfunktionen der Ebene 7 für Ihre Anwendung.

Application Gateway erlaubt Ihnen das Optimieren der Produktivität von Webfarmen, indem Sie die CPU-intensive SSL-Beendigung an das Anwendungsgateway auslagern. Darüber hinaus werden noch weitere Routingfunktionen der Ebene 7 bereitgestellt. Hierzu zählen etwa die Roundrobin-Verteilung des eingehenden Datenverkehrs, cookiebasierte Sitzungsaffinität, Routing auf URL-Pfadbasis und die Möglichkeit zum Hosten mehrerer Websites hinter einer einzelnen Application Gateway-Instanz.

Die Azure Application Gateway WAF-SKU enthält eine Webanwendungsfirewall. Dieser SKU bietet Schutz für Webanwendungen vor allgemeinen Onlinesicherheitsrisiken und Exploits. Application Gateway kann als Gateway mit Internetzugriff, rein internes Gateway oder als Kombination dieser beiden Optionen konfiguriert werden.

## <a name="public-ips"></a>Öffentliche IP-Adressen

Einige Azure-Features ermöglichen Ihnen, einer [öffentlichen IP-Adresse][PIP] Dienstendpunkte zuzuordnen, sodass über das Internet auf die Ressource zugegriffen werden kann. Der Endpunkt verwendet die Netzwerkadressenübersetzung, um Datenverkehr zur internen Adresse und zum Port im virtuellen Azure-Netzwerk zu leiten. Dieser Pfad ist der primäre Weg, auf dem externer Datenverkehr in das virtuelle Netzwerk gelangt. Sie können die öffentlichen IP-Adressen konfigurieren, um festzulegen, welcher Datenverkehr zugelassen wird bzw. wie und wo eine Übersetzung in das virtuelle Netzwerk stattfindet.

## <a name="azure-ddos-protection-standard"></a>Azure DDoS Protection Standard

[Azure DDoS Protection Standard][DDoS] stellt über den Diensttarif [Basic][DDoS] zusätzliche Funktionen zur Bedrohungsabwehr bereit, die speziell für Azure Virtual Network-Ressourcen optimiert sind. DDoS Protection Standard kann leicht aktiviert werden und erfordert keine Änderung der Anwendung.

Sie können Schutzrichtlinien über dedizierte Datenverkehrsüberwachung und Machine Learning-Algorithmen optimieren. Richtlinien werden auf öffentliche IP-Adressen angewendet, die in virtuellen Netzwerken bereitgestellten Ressourcen zugeordnet sind. Beispiele hierfür sind Instanzen von Azure Load Balancer, Azure Application Gateway und Azure Service Fabric.

Über Azure Monitor-Ansichten steht Echtzeittelemetrie sowohl während eines Angriffs als auch für den Verlauf zur Verfügung. Mit der Webanwendungsfirewall in Azure Application Gateway können Sie Schutz auf Anwendungsebene hinzufügen. Der Schutz wird für öffentliche Azure-IPv4-Adressen bereitgestellt.

<!-- images -->

[0]: ../../_images/azure-best-practices/network-redundant-equipment.png "Beispiele für Komponentenüberlappung"
[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Allgemeines Beispiel für Hub-and-Spoke"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Cluster mit Hub und Spokes"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Spoke-zu-Spoke"
[4]: ../../_images/azure-best-practices/network-hub-spoke-block-level-diagram.png "Blockebenenabbildung von Hub-Spoke"
[5]: ../../_images/azure-best-practices/network-users-groups-subscriptions.png "Benutzer, Gruppen, Abonnements und Projekte"
[6]: ../../_images/azure-best-practices/network-infrastructure-high-level.png "Abbildung der allgemeinen Infrastruktur"
[7]: ../../_images/azure-best-practices/network-high-level-perimeter-networks.png "Abbildung der allgemeinen Infrastruktur"
[8]: ../../_images/azure-best-practices/network-vnet-peering-perimeter-networks.png "VNET-Peering und Umkreisnetzwerke"
[9]: ../../_images/azure-best-practices/network-high-level-diagram-monitoring.png "Übersichtsabbildung der Überwachung"
[10]: ../../_images/azure-best-practices/network-high-level-workloads.png "Übersichtsabbildung über Workloads"

<!-- links -->

[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[virtual-networks]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[azure-ad]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[vWAN]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[SubMgmt]: https://docs.microsoft.com/azure/architecture/cloud-adoption/reference/azure-scaffold
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[perimeter-network]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[AppGWWAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[NPM]: https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
