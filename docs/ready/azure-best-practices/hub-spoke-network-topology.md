---
title: Hub-and-Spoke-Netzwerktopologie
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hub-and-Spoke-Netzwerktopologie
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: fcbcda63ff080de234075f0a8784731e591ca0f3
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549012"
---
# <a name="hub-and-spoke-network-topology"></a>Hub-and-Spoke-Netzwerktopologie

*Hub-and-Spoke* ist ein Netzwerkmodell für eine effizientere Verwaltung gemeinsamer Kommunikations- oder Sicherheitsanforderungen. Es hilft auch dabei, Azure-Abonnementeinschränkungen zu vermeiden. Dieses Modell berücksichtigt die folgenden Punkte:

- **Kosteneinsparungen und Effizienz der Verwaltung** Zentralisierung von Diensten, die von mehreren Workloads, z.B. Network Virtual Appliances (NVAs) und DNS-Servern an einem zentralen Standort gemeinsam genutzt werden können. Auf diese Weise kann die IT-Abteilung redundante Ressourcen und den Verwaltungsaufwand minimieren.
- **Umgehen von Abonnementgrenzen** Große cloudbasierte Workloads können den Einsatz von mehr Ressourcen erfordern, als in einem einzelnen Azure-Abonnements zulässig ist. Durch ein Peering virtueller Netzwerke für eine Workload aus verschiedenen Abonnements zu einem zentralen Hub können diese Grenzwerte umgangen werden. Weitere Informationen finden Sie unter [Grenzwerte für Abonnements](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Trennung von Zuständigkeiten**: Sie können einzelne Workloads zwischen zentralen IT-Teams und für Workloads zuständige Teams bereitstellen.

Kleinere Cloudumgebungen profitieren möglicherweise nicht von der zusätzlichen Struktur und den Funktionen, die dieses Modell bietet. Für größere Cloudeinführungsaktivitäten sollte jedoch die Implementierung einer Hub-and-Spoke-Architektur in Erwägung gezogen werden, wenn für sie bereits die oben aufgeführten Bedenken gelten.

> [!NOTE]
> Die Website für Azure-Referenzarchitekturen enthält Beispielvorlagen, die Sie als Grundlage für die Implementierung Ihrer eigenen Hub-and-Spoke-Netzwerke verwenden können:
>
> - [Implementieren einer Hub-and-Spoke-Netzwerktopologie in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementieren einer Hub-and-Spoke-Netzwerktopologie mit gemeinsamen Diensten in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Übersicht

![Beispiele für eine Hub-and-Spoke-Netzwerktopologie][1]

Wie in der Abbildung gezeigt, unterstützt Azure zwei Arten von Hub-and-Spoke-Entwürfen. Kommunikation, gemeinsame Ressourcen und zentralisierte Sicherheitsrichtlinien („VNet Hub“ in der Abbildung) oder ein Virtual WAN-Typ („Virtual WAN“ in der Abbildung) für umfassende Kommunikation zwischen Branches oder zwischen einem Branch und Azure werden unterstützt.

Ein Hub ist eine zentrale Netzwerkzone, die den ein- oder ausgehenden Datenverkehr zwischen Zonen steuert und überprüft: im Internet, lokal und in den Spokes. Die Hub-and-Spoke-Topologie stellt für Ihre IT-Abteilung eine effektive Möglichkeit zum Erzwingen von Sicherheitsrichtlinien an einem zentralen Ort dar. Außerdem verringert sie das Risiko von Fehlkonfigurationen und Offenlegungen.

Der Hub enthält oft die allgemeinen Dienstkomponenten, die von den Spokes genutzt werden. Im Folgenden finden Sie einige Beispiele für allgemeine zentrale Dienste:

- Die Windows Server Active Directory-Infrastruktur, die für die Benutzerauthentifizierung von Drittanbietern, die über nicht vertrauenswürdige Netzwerke zugreifen, erforderlich ist, bevor sie Zugriff auf die Workloads im Spoke erhalten. Dies beinhaltet die zugehörigen Active Directory-Verbunddienste (Active Directory Federation Services, AD FS).
- Ein DNS-Dienst, mit dem die Namen der Workloads in den Spokes aufgelöst werden, um lokal und über das Internet auf Ressourcen zuzugreifen, wenn [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) nicht verwendet wird.
- Eine Public Key-Infrastruktur (PKI), mit der das einmalige Anmelden in Workloads implementiert wird.
- Flusssteuerung des TCP- und UDP-Datenverkehrs zwischen den Spoke-Netzwerkzonen und dem Internet.
- Flusssteuerung zwischen den Spokes und dem lokalen Netzwerk.
- Flusssteuerung zwischen zwei Spokes (sofern erforderlich).

Sie können Redundanzen minimieren, die Verwaltung vereinfachen und die Gesamtkosten senken, indem Sie die gemeinsame Hubinfrastruktur zur Unterstützung mehrerer Spokes nutzen.

Die Rolle eines jeden Spokes kann über verschiedene Arten von Workloads gehostet werden. Die Spokes können auch einen modularen Ansatz für wiederholbare Bereitstellungen der gleichen Workloads bieten. Beispiele hierfür sind Entwicklung und Testing, Benutzerakzeptanztests, Staging und Produktion.

Mit den Spokes können auch verschiedene Gruppen in Ihrer Organisation getrennt und aktiviert werden. Ein Beispiel hierfür sind Azure DevOps-Gruppen. Innerhalb eines Spokes ist es möglich, eine einfache Workload oder komplexe Workloads mit mehreren Ebenen mit einer Datenverkehrssteuerung zwischen den Ebenen bereitzustellen.

## <a name="subscription-limits-and-multiple-hubs"></a>Abonnementlimit und mehrere Hubs

In Azure wird jede Komponente, unabhängig vom Typ, in einem Azure-Abonnement bereitgestellt. Die Isolation von Azure-Komponenten in verschiedenen Azure-Abonnements kann die Anforderungen verschiedener Branchenanwendungen erfüllen, z.B. das Einrichten unterschiedlicher Zugriffs- und Autorisierungsebenen.

Eine einzelne Hub-ans-Spoke-Implementierung kann auf eine große Anzahl von Spokes zentral hochskaliert werden. Dabei gelten jedoch wie bei jedem IT-System gewisse Plattformbeschränkungen. Die Hub-Bereitstellung ist an ein bestimmtes Azure-Abonnement gebunden. (Beispielsweise kann eine maximale Anzahl von Peerings in virtuellen Netzwerken gelten. Details finden Sie unter [Grenzwerte für Azure-Abonnements und Dienste, Kontingente und Einschränkungen][Grenzwerte].)

In Fällen, in denen diese Beschränkungen ggf. ein Problem darstellen, kann die Architektur weiter zentral hochskaliert werden, indem das Modell von einem einzelnen Hub und Spoke auf ein Cluster von Hubs und Spokes erweitert wird. Mehrere Hubs in mindestens einer Azure-Region können mithilfe von Peering in virtuellen Netzwerken, ExpressRoute, Virtual WAN oder einem Site-to-Site-VPN miteinander verbunden werden.

![Cluster mit Hubs und Spokes][2]

Die Einführung von mehreren Hubs erhöht die Kosten und den Verwaltungsaufwand für das System. Dies lässt sich nur durch Skalierbarkeit, Systemeinschränkungen oder Redundanz und die regionale Replikation zum Erzielen von Leistung für Benutzer oder Notfallwiederherstellung rechtfertigen. In Szenarien, die mehrere Hubs erfordern, sollten alle Hubs die gleichen Dienste anbieten, um die Vorgänge nicht zu erschweren.

## <a name="interconnection-between-spokes"></a>Verbindung zwischen Spokes

Innerhalb eines einzelnen Spokes ist es möglich, komplexe Workloads mit mehreren Ebenen zu implementieren. Sie können Konfigurationen mit mehreren Ebenen implementieren, indem Sie Subnetze (eines für jede Ebene) im selben virtuellen Netzwerk verwenden und Netzwerksicherheitsgruppen einsetzen, um die Datenflüsse zu filtern.

Ein Architekt möchte vielleicht eine Workload mit mehreren Ebenen in mehreren virtuellen Netzwerken bereitstellen. Mittels Peering in virtuellen Netzwerken können Spokes Verbindungen mit anderen Spokes im gleichen Hub oder in anderen Hubs herstellen.

Ein typisches Beispiel für dieses Szenario ist die Platzierung von Anwendungsverarbeitungsservern in einem Spoke oder virtuellen Netzwerk. Die Datenbank wird dann in einem anderen Spoke oder virtuellen Netzwerk bereitgestellt. In diesem Fall ist es einfach, die Spokes mittels Peering in virtuellen Netzwerken zu verbinden und das Durchlaufen des Hubs dabei zu vermeiden. Die Lösung besteht darin, Architektur und Sicherheit sorgfältig zu überprüfen, um sicherzustellen, dass durch die Umgehung des Hubs keine wichtigen Sicherheits- oder Überwachungspunkte umgangen werden, die nur im Hub vorhanden sind.

![Spokes, die eine Verbindung untereinander und mit einem Hub herstellen][3]

Spokes können auch mit einem Spoke verbunden werden, der als Hub fungiert. Bei diesem Ansatz wird eine Hierarchie mit zwei Ebenen erstellt: Der Spoke auf der höheren Ebene (Ebene 0) wird der Hub der unteren Spokes (Stufe 1) in der Hierarchie. Die Spokes einer Hub-and-Spoke-Implementierung eines virtuellen Datencenters sind zum Weiterleiten des Datenverkehrs an den zentralen Hub erforderlich, damit der Datenverkehr an sein Ziel im lokalen Netzwerk oder im öffentlichen Internet geleitet werden kann. Eine Architektur mit zwei Hubebenen führt komplexes Routing ein, das die Vorteile einer einfachen Hub-and-Spoke-Beziehung aufhebt.

<!-- images -->

[0]: ../../_images/azure-best-practices/network-redundant-equipment.png "Beispiele für Komponentenüberlappung"
[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Allgemeines Beispiel für Hub-and-Spoke"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Cluster mit Hub und Spokes"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Spoke-zu-Spoke"
[4]: ../../_images/azure-best-practices/network-hub-spoke-block-level-diagram.png "Blockebenenabbildung für Hub-and-Spoke"
[5]: ../../_images/azure-best-practices/network-users-groups-subscriptions.png "Benutzer, Gruppen, Abonnements und Projekte"
[6]: ../../_images/azure-best-practices/network-infrastructure-high-level.png "Abbildung der allgemeinen Infrastruktur"
[7]: ../../_images/azure-best-practices/network-high-level-perimeter-networks.png "Abbildung der allgemeinen Infrastruktur"
[8]: ../../_images/azure-best-practices/network-vnet-peering-perimeter-networks.png "Peering virtueller Netzwerke und Umkreisnetzwerke"
[9]: ../../_images/azure-best-practices/network-high-level-diagram-monitoring.png "Übersichtsabbildung der Überwachung"
[10]: ../../_images/azure-best-practices/network-high-level-workloads.png "Übersichtsabbildung zu Workloads"

<!-- links -->

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
[SubMgmt]: ../../reference/azure-scaffold.md
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
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
