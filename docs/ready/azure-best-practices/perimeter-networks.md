---
title: Umkreisnetzwerke
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Azure für Ihre Organisation effizient einrichten.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
ms.custom: virtual-network
ms.openlocfilehash: 4e97a1140d80a201489e86b5652a15b11b508e60
ms.sourcegitcommit: 71a4f33546443d8c875265ac8fbaf3ab24ae8ab4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86479873"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs WAFs -->

# <a name="perimeter-networks"></a>Umkreisnetzwerke

[Umkreisnetzwerke][perimeter-network] sorgen für sichere Konnektivität zwischen Ihren Cloudnetzwerken und Ihren lokalen oder physischen Datencenternetzwerken (sowie für Internetkonnektivität). Ein Umkreisnetzwerk wird manchmal als „demilitarisierte Zone“ oder „DMZ“ bezeichnet.

Damit Umkreisnetzwerke effektiv sind, müssen eingehende Pakete über Sicherheitsgeräte geleitet werden, die in sicheren Subnetzen gehostet werden, bevor sie zu Back-End-Servern gelangen. Beispiele hierfür sind die Firewall, Intrusion-Detection-Systeme und Intrusion-Prevention-Systeme. Von Workloads an das Internet gesendete Pakete sollten ebenfalls über die Sicherheitsgeräte im Umkreisnetzwerk geleitet werden, bevor sie das Netzwerk verlassen. Dieser Fluss dient der Richtlinienerzwingung, Überprüfung und Überwachung.

Umkreisnetzwerken nutzen die folgenden Azure-Funktionen und -Dienste:

- [Virtuelle Netzwerke][virtual-networks], [benutzerdefinierte Routen][user-defined-routes] und [Netzwerksicherheitsgruppen][network-security-groups]
- [Virtuelle Netzwerkgeräte (NVAs)][network-virtual-appliances]
- [Azure-Lastenausgleich][alb]
- [Azure Application Gateway][appgw] und [Web Application Firewall (WAF)][appgwwaf]
- [Öffentliche IP-Adressen][PIP]
- [Azure Front Door][afd] mit [Web Application Firewall][afdwaf]
- [Azure Firewall][Azure-firewall]

> [!NOTE]
> Azure-Referenzarchitekturen bieten Beispielvorlagen, die Sie für die Implementierung Ihrer eigenen Umkreisnetzwerke verwenden können:
>
> - [Implementieren eines Umkreisnetzwerks zwischen Azure und Ihrem lokalen Rechenzentrum](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)
> - [Implementieren eines Umkreisnetzwerks zwischen Azure und dem Internet](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)

Normalerweise sind Ihr zentrales IT-Team und die und Sicherheitsteams für die Anforderungendefinition und den Betrieb Ihrer Umkreisnetzwerke verantwortlich.

![Beispiel für eine Hub-and-Spoke-Netzwerktopologie](../../_images/azure-best-practices/network-high-level-perimeter-networks.png)
_Abbildung 1: Beispiel für eine Hub-and-Spoke-Netzwerktopologie_

Das obige Diagramm enthält ein Beispiel für eine [Hub-and-Spoke-Netzwerktopologie](./hub-spoke-network-topology.md), in dem die Durchsetzung von zwei Umkreisnetzwerken mit Zugriff auf das Internet und ein lokales Netzwerk implementiert wird. Beide Perimeter befinden sich im DMZ-Hub. Im DMZ-Hub kann das Umkreisnetzwerk für das Internet hochskaliert werden und so viele Branchenanwendungen über mehrere Farmen von WAFs und Azure Firewall-Instanzen unterstützen, die zum Schutz der virtuellen Spoke-Netzwerke beitragen. Der Hub ermöglicht je nach Bedarf außerdem Konnektivität über VPN oder Azure ExpressRoute.

## <a name="virtual-networks"></a>Virtuelle Netzwerke

Umkreisnetzwerke werden normalerweise mithilfe eines [virtuellen Netzwerks][virtual-networks] mit mehreren Subnetzen erstellt, um verschiedene Arten von Diensten zu hosten, die den Internetdatenverkehr über virtuelle Netzwerkgeräte, WAFs und Azure Application Gateway-Instanzen filtern und überprüfen.

## <a name="user-defined-routes"></a>Benutzerdefinierte Routen

Mithilfe von [benutzerdefinierten Routen][user-defined-routes] können Kunden Firewalls, Eindringschutzsysteme, Angriffserkennungssysteme und andere virtuelle Geräte bereitstellen. Kunden können den Netzwerkdatenverkehr zum Erzwingen von Sicherheitsrichtlinien, zur Überwachung und zur Überprüfung über diese Sicherheitsgeräte routen. Benutzerdefinierte Routen können erstellt werden, um sicherzustellen, dass Datenverkehr durch die spezifischen benutzerdefinierten VMs, NVAs und Lastenausgleichsmodule geleitet wird.

In einem Hub-and-Spoke-Netzwerkbeispiel erfordert die Gewährleistung, dass Datenverkehr, der von VMs erzeugt wird, die sich in der Spoke befinden, durch die richtigen virtuellen Geräte im Hub geleitet wird, eine benutzerdefinierte Route, die in den Subnetzen der Spoke definiert ist. Diese Route legt die Front-End-IP-Adresse des internen Lastenausgleichs als nächsten Hop fest. Der interne Load Balancer verteilt den internen Datenverkehr auf die virtuellen Geräte (Back-End-Pool des Load Balancers).

## <a name="azure-firewall"></a>Azure Firewall

[Azure Firewall][Azure-firewall] ist ein verwalteter, cloudbasierter Dienst zum Schutz Ihrer Azure Virtual Network-Ressourcen. Es handelt sich dabei um eine vollständig zustandsbehaftete verwaltete Firewall mit integrierter Hochverfügbarkeit und uneingeschränkter Cloudskalierbarkeit. Sie können Richtlinien zur Anwendungs- und Netzwerkkonnektivität übergreifend für Abonnements und virtuelle Netzwerke zentral erstellen, erzwingen und protokollieren.

Azure Firewall verwendet eine statische öffentliche IP-Adresse für Ihre virtuellen Netzwerkressourcen. Dadurch können externe Firewalls Datenverkehr aus Ihrem virtuellen Netzwerk identifizieren. Der Dienst arbeitet für Protokollierung und Analyse mit Azure Monitor zusammen.

## <a name="network-virtual-appliances"></a>Virtuelle Netzwerkgeräte

Umkreisnetzwerke mit Zugriff auf das Internet werden in der Regel über eine Azure Firewall-Instanz oder eine Farm von Firewalls oder [Webanwendungsfirewalls][afdwaf] verwaltet.

Verschiedene Geschäftsbereiche verwenden häufig viele Webanwendungen. Diese Anwendungen weisen häufig unterschiedliche Sicherheitsrisiken und Exploits auf. Eine Web Application Firewall erkennt Angriffe auf Webanwendungen (HTTP/S) genauer als eine generische Firewall. Verglichen mit herkömmlichen Firewalls stellen Web Application Firewalls einen Satz von bestimmten Features bereit, um den internen Webserver vor Bedrohungen zu schützen.

Eine Azure Firewall-Instanz und eine Firewall eines virtuellen Netzwerkgeräts (NVA) werden jeweils über eine gemeinsame Verwaltungsebene mit einem Satz von Sicherheitsregeln ausgeführt, die die in den Spokes gehosteten Workloads schützen und den Zugriff auf lokale Netzwerke steuern. Azure Firewall verfügt über integrierte Skalierbarkeit, während NVA-Firewalls hinter einem Lastenausgleich manuell skaliert werden können.

Eine Firewallfarm verfügt im Allgemeinen im Vergleich zu einer Web Application Firewall über weniger spezialisierte Software. Sie hat jedoch einen umfassenderen Anwendungsbereich, sodass sie alle Arten von ein- und ausgehendem Datenverkehr filtern und überprüfen kann. Wenn Sie einen NVA-Ansatz verwenden, können Sie Software in Azure Marketplace ermitteln und bereitstellen.

Verwenden Sie eine Gruppe von Azure Firewall-Instanzen (oder virtuelle Netzwerkgeräte) für Datenverkehr aus dem Internet und eine andere Gruppe für Datenverkehr mit lokalem Ursprung. Die Verwendung einer einzigen Gruppe von Firewalls für den gesamten Datenverkehr stellt ein Sicherheitsrisiko dar, da sie keinen wirksamen Sicherheitsbereich zwischen den beiden Arten von Netzwerkdatenverkehr bietet. Separate Firewallebenen vereinfachen die Überprüfung von Sicherheitsregeln und ermöglichen eine eindeutige Zuordnung von Regeln zu eingehenden Netzwerkanforderungen.

## <a name="azure-load-balancer"></a>Azure Load Balancer

[Azure Load Balancer][alb] stellt einen Dienst mit hoher Verfügbarkeit der Ebene 4 (TCP, UDP) bereit, mit dem eingehender Datenverkehr zwischen Dienstinstanzen verteilt werden kann, die in einer Gruppe mit Lastenausgleich definiert sind. Der Datenverkehr, der von den Front-End-Endpunkten (öffentliche IP-Endpunkte oder private IP-Endpunkte) an den Load Balancer gesendet wird, kann mit oder ohne Adressübersetzung auf einen Pool von Back-End-IP-Adressen weiterverteilt werden (z.B. NVAs oder VMs).

Azure Load Balancer kann auch die Integrität der verschiedenen Serverinstanzen testen. Wenn eine Instanz nicht auf einen Test reagiert, sendet der Lastenausgleich keinen weiteren Datenverkehr an die fehlerhafte Instanz.

Als Beispiel für die Verwendung einer Hub-and-Spoke-Netzwerktopologie kann ein externer Lastausgleich sowohl für den Hub als auch für die Spokes bereitgestellt werden. Im Hub leitet der Lastenausgleich Datenverkehr effizient an Dienste in den Spokes weiter. In den Spokes verwalten Lastenausgleichsmodule Anwendungsdatenverkehr.

## <a name="azure-front-door"></a>Azure Front Door

[Azure Front Door][afd] von Microsoft stellt eine hochverfügbare und hochgradig skalierbare Plattform für die Beschleunigung von Webanwendungen und einen globalen HTTPS-Lastenausgleich bereit. Sie können Azure Front Door verwenden, Ihre dynamischen Webanwendungen und statischen Inhalte zu erstellen, auszuführen und aufzuskalieren. Azure Front Door Service wird an mehr als 100 Standorten im Edgebereich des globalen Netzwerks von Microsoft ausgeführt.

Azure Front Door stellt für Ihre Anwendung einheitliche Automatisierung der Regions-/Stempelwartung, BCDR-Automatisierung, einheitliche Client-/Benutzerinformationen, Zwischenspeicherung und Erkenntnisse zu Ihren Diensten bereit. Die Plattform bietet Leistung, Zuverlässigkeit, Support-SLAs. Außerdem bietet sie Konformitätszertifizierungen und überwachbare Sicherheitsverfahren, die von Azure entwickelt, betrieben und nativ unterstützt werden.

## <a name="azure-application-gateway"></a>Azure Application Gateway

[Azure Application Gateway][appgw] ist ein dediziertes virtuelles Gerät, mit dem ein verwalteter Controller zur Anwendungsbereitstellung (Application Delivery Controller, ADC) bereitgestellt wird. Es bietet verschiedene Lastenausgleichsfunktionen der Ebene 7 für Ihre Anwendung.

<!-- docsTest:ignore "application gateway" TODO -->

Mit Azure Application Gateway können Sie die Produktivität von Webfarmen optimieren, indem Sie die CPU-intensive SSL-Beendigung an das Anwendungsgateway auslagern. Darüber hinaus werden weitere Routingfunktionen der Ebene 7 bereitgestellt. Hierzu gehören beispielsweise die Roundrobin-Verteilung des eingehenden Datenverkehrs, cookiebasierte Sitzungsaffinität, Routing auf URL-Pfadbasis und die Möglichkeit zum Hosten mehrerer Websites hinter einem einzelnen Anwendungsgateway.

Die Azure Application Gateway WAF-SKU enthält eine Web Application Firewall. Dieser SKU bietet Schutz für Webanwendungen vor allgemeinen Onlinesicherheitsrisiken und Exploits. Sie können Azure Application Gateway als Gateway mit Internetzugriff, ein nur internes Gateway oder als Kombination dieser beiden Optionen konfigurieren.

## <a name="public-ips"></a>Öffentliche IP-Adressen

Einige Azure-Features ermöglichen Ihnen, einer [öffentlichen IP-Adresse][PIP] Dienstendpunkte zuzuordnen, sodass über das Internet auf die Ressource zugegriffen werden kann. Dieser Endpunkt verwendet die Netzwerkadressenübersetzung (Network Address Translation, NAT), um Datenverkehr zur internen Adresse und zum Port im Azure Virtual Network zu leiten. Dieser Pfad ist der primäre Weg, auf dem externer Datenverkehr in das virtuelle Netzwerk gelangt. Sie können die öffentlichen IP-Adressen konfigurieren, um festzulegen, welcher Datenverkehr zugelassen wird bzw. wie und wo eine Übersetzung in das virtuelle Netzwerk stattfindet.

## <a name="azure-ddos-protection-standard"></a>Azure DDoS Protection Standard

[Azure DDoS Protection Standard][DDoS] stellt über den Diensttarif [Basic][DDoS] hinaus zusätzliche Funktionen zur Bedrohungsabwehr bereit, die speziell für Azure Virtual Network-Ressourcen optimiert sind. DDoS Protection Standard kann auf einfache Weise aktiviert werden und erfordert keine Änderungen der Anwendung.

Sie können Schutzrichtlinien über dedizierte Datenverkehrsüberwachung und Machine Learning-Algorithmen optimieren. Richtlinien werden auf öffentliche IP-Adressen angewendet, die in virtuellen Netzwerken bereitgestellten Ressourcen zugeordnet sind. Beispiele hierfür sind Instanzen von Azure Load Balancer, Application Gateway und Service Fabric.

Über Azure Monitor-Ansichten steht Echtzeittelemetrie sowohl während eines Angriffs als auch für den Verlauf zur Verfügung. Mit der Web Application Firewall in Azure Application Gateway können Sie Schutz auf Anwendungsebene hinzufügen. Der Schutz wird für öffentliche Azure-IPv4-Adressen bereitgestellt.

<!-- links -->

[Virtual-networks]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[Network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[User-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[Network-virtual-appliances]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[Azure-firewall]: https://docs.microsoft.com/azure/firewall/overview
[Perimeter-network]: https://docs.microsoft.com/azure/best-practices-network-security
[Alb]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[Afd]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[Afdwaf]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[Appgw]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[Appgwwaf]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
