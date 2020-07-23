---
title: Überprüfen der Netzwerkoptionen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die Netzwerkfunktionen ermitteln, die von Ihrer Zielzone zur Unterstützung der Azure-Workloads benötigt werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8314433ae406bbc97ddc8ef998cfeb5d8cf49d20
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86195036"
---
<!-- cSpell:ignore paas NVAs VPNs -->

# <a name="review-your-network-options"></a>Überprüfen der Netzwerkoptionen

Das Entwerfen und Implementieren von Azure-Netzwerkfunktionen ist ein wichtiger Bestandteil Ihrer Anstrengungen zur Cloudbereitstellung. Sie müssen Entscheidungen hinsichtlich des Netzwerkentwurfs treffen, um die Arbeitsauslastungen und Dienste, die in der Cloud gehostet werden, ordnungsgemäß zu unterstützen. Die Netzwerkprodukte und -dienste von Azure unterstützen eine Vielzahl von Netzwerkfunktionen. Die Art und Weise, in der Sie diese Dienste und die ausgewählten Netzwerkarchitekturen strukturieren, hängt von den Anforderungen Ihrer Organisation in Bezug auf Workload, Governance und Konnektivität ab.

## <a name="identify-workload-networking-requirements"></a>Ermitteln der Netzwerkanforderungen von Workloads

Im Rahmen der Evaluierung und Vorbereitung Ihrer Landezone müssen Sie die Netzwerkfunktionen identifizieren, die von Ihrer Landezone unterstützt werden müssen. Dieser Prozess umfasst die Bewertung der einzelnen Anwendungen und Dienste, aus denen Ihre Workloads bestehen, um die Konnektivitäts- und Netzwerksteuerungsanforderungen zu ermitteln. Nachdem Sie diese Anforderungen identifiziert und dokumentiert haben, können Sie Richtlinien für Ihre Landezone erstellen, mit denen gesteuert wird, welche Netzwerkressourcen und -konfigurationen basierend auf Ihren Workloadanforderungen zulässig sind.

Verwenden Sie für alle Anwendungen oder Dienste, die Sie in Ihrer Landezonenumgebung bereitstellen, die folgende Entscheidungsstruktur als Ausgangspunkt für die Ermittlung der geeigneten Netzwerktools oder -dienste, die verwendet werden sollen:

![Entscheidungsstruktur: Azure-Netzwerkdienste](../../_images/ready/network-decision-tree.png)

### <a name="key-questions"></a>Kernfragen

Die Beantwortung der folgenden Fragen zu Ihren Workloads ist hilfreich, um basierend auf der Entscheidungsstruktur für Azure-Netzwerkdienste Entscheidungen treffen zu können:

- **Ist für Ihre Workloads ein virtuelles Netzwerk erforderlich?** Verwaltete PaaS-Ressourcentypen (Platform-as-a-Service) nutzen zugrunde liegende Netzwerkfunktionen, die nicht immer ein virtuelles Netzwerk erfordern. Wenn Ihre Workloads keine komplexeren Netzwerkfeatures erfordern und Sie keine IaaS-Ressourcen (Infrastructure-as-a-Service) bereitstellen müssen, erfüllen möglicherweise die [nativen Netzwerkfunktionen von PaaS-Ressourcen](../../decision-guides/software-defined-network/paas-only.md) die Anforderungen Ihrer Workloads hinsichtlich Konnektivität und Datenverkehrsverwaltung.
- **Erfordern Ihre Workloads Konnektivität zwischen virtuellen Netzwerken und Ihrem lokalen Datencenter?** Azure bietet zwei Lösungen für die Einrichtung von hybriden Netzwerkfunktionen: Azure VPN Gateway und Azure ExpressRoute. [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) verbindet Ihre lokalen Netzwerke über Site-to-Site-VPNs auf ähnliche Weise mit Azure wie bei der Einrichtung eines Remotefilialstandorts und dem Herstellen einer Verbindung mit diesem. VPN Gateway weist eine maximale Bandbreite von 10 GBit/s auf. [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) bietet mehr Zuverlässigkeit und eine niedrigere Latenz über eine private Verbindung zwischen Azure und Ihrer lokalen Infrastruktur. Die Bandbreitenoptionen reichen von 50 MBit/s bis hin zu 100 GBit/s.
- **Müssen Sie ausgehenden Datenverkehr mithilfe von lokalen Netzwerkgeräten untersuchen und überwachen?** Bei cloudnativen Workloads können Sie [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview) oder in der Cloud gehostete [virtuelle Netzwerkgeräte (Network Virtual Appliances, NVAs)](https://azure.microsoft.com/solutions/network-appliances) von Drittanbietern verwenden, um Datenverkehr zu untersuchen und zu überwachen, der aus dem öffentlichen Internet empfangen oder an das öffentliche Internet gesendet wird. Viele unternehmensweite IT-Sicherheitsrichtlinien erfordern jedoch, dass ausgehender Datenverkehr an das Internet über zentral verwaltete Geräte in der lokalen Umgebung der Organisation geleitet wird. [Tunnelerzwingung](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) unterstützt diese Szenarien. Nicht alle verwalteten Dienste unterstützen die Tunnelerzwingung. Dienste und Funktionen wie die [App Service-Umgebung in Azure App Service](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-key-concepts), [Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/intro-kubernetes), [verwaltete Azure SQL-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index), [Azure Databricks](https://docs.microsoft.com/azure/azure-databricks/what-is-azure-databricks) und [Azure HDInsight](https://docs.microsoft.com/azure/hdinsight) unterstützen diese Konfiguration, wenn der Dienst oder die Funktion in einem virtuellen Netzwerk bereitgestellt wird.
- **Müssen Sie mehrere virtuelle Netzwerke verbinden?** Sie können das [Peering virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) verwenden, um mehrere Instanzen von [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) zu verbinden. Das Peering kann Verbindungen abonnement- und regionsübergreifend unterstützen. In Szenarien, in denen Sie Dienste bereitstellen, die für mehrere Abonnements freigegeben sind oder eine große Anzahl von Netzwerkpeerings verwalten müssen, sollten Sie eine [Hub-and-Spoke-Netzwerkarchitektur](../../decision-guides/software-defined-network/hub-spoke.md) oder die Verwendung von [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) in Betracht ziehen. Das Peering virtueller Netzwerke bietet nur Verbindungen zwischen zwei Netzwerken mit Peering. Standardmäßig wird keine transitive Konnektivität über mehrere Peerings hinweg bereitgestellt.
- **Kann über das Internet auf Ihre Workloads zugegriffen werden?** Azure bietet Dienste, die Sie beim Verwalten und Sichern des externen Zugriffs auf Ihre Anwendungen und Dienste unterstützen:
  - [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview)
  - [Network Appliances](https://azure.microsoft.com/solutions/network-appliances)
  - [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
  - [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway)
  - [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)
- **Müssen Sie eine benutzerdefinierte DNS-Verwaltung unterstützen?** [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) ist ein Hostingdienst für DNS-Domänen. Azure DNS bietet eine Namensauflösung mithilfe der Azure-Infrastruktur. Wenn Ihre Workloads eine Namensauflösung erfordern, die von den Azure DNS-Features nicht durchgeführt werden kann, müssen Sie möglicherweise Zusatzlösungen bereitstellen. Wenn Ihre Workloads außerdem Active Directory-Dienste erfordern, sollten Sie die Verwendung von [Azure Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/overview) in Betracht ziehen, um die Azure DNS-Funktionen zu ergänzen. Um weitere Funktionen für Ihre Anforderungen zu nutzen, können Sie auch [benutzerdefinierte virtuelle IaaS-Computer bereitstellen](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

## <a name="common-networking-scenarios"></a>Gängige Netzwerkszenarien

Ein Azure-Netzwerk bietet mehrere Produkte und Dienste, die verschiedene Netzwerkfunktionen bereitstellen. Im Rahmen der Entwicklung Ihres Netzwerkentwurfs können Sie Ihre Workloadanforderungen mit den Netzwerkszenarien in der folgenden Tabelle vergleichen, um die Azure-Tools oder -Dienste zu ermitteln, die Sie zum Bereitstellen dieser Netzwerkfunktionen nutzen können:

<!-- markdownlint-disable MD033 -->

| Szenario | Netzwerkprodukt oder -dienst |
| --- | --- |
| Ich benötige die Netzwerkinfrastruktur zum Verbinden sämtlicher Komponenten – von virtuellen Computern bis hin zu eingehenden VPN-Verbindungen. | [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network) |
| Ich muss Lastenausgleich für ein- und ausgehenden Verbindungen und Anforderungen an meine Anwendungen oder Dienste ausführen. | [Azure-Lastenausgleich](https://docs.microsoft.com/azure/load-balancer) |
| Ich möchte die Bereitstellung von Anwendungsserverfarmen optimieren und gleichzeitig die Anwendungssicherheit durch eine Web Application Firewall erhöhen. | [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway) <br> [Azure Front Door](https://docs.microsoft.com/azure/frontdoor) |
| Ich muss für sichere Nutzung des Internets für den Zugriff auf Azure Virtual Networks mit leistungsstarken VPN-Gateways sorgen. | [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway) |
| Ich möchte superschnelle DNS-Antworten und extrem hohe Verfügbarkeit für alle meine Domänenanforderungen sicherstellen. | [Azure DNS](https://docs.microsoft.com/azure/dns) |
| Ich muss die Bereitstellung von Inhalten mit hoher Bandbreite für Kunden auf der ganzen Welt beschleunigen – von Anwendungen und gespeicherten Inhalten bis hin zum Streamen von Videos. | [Azure Content Delivery Network (CDN)](https://docs.microsoft.com/azure/cdn) |
| Ich muss meine Azure-Anwendungen vor DDoS-Angriffen schützen. | [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) |
| Ich muss den Datenverkehr optimal auf Dienste in Azure-Regionen auf der ganzen Welt verteilen und gleichzeitig für Hochverfügbarkeit und Reaktionsfähigkeit sorgen. | [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager) <br><br> [Azure Front Door](https://docs.microsoft.com/azure/frontdoor) |
| Ich muss für Konnektivität in einem privaten Netzwerk sorgen, sodass aus meinem Unternehmensnetzwerken so auf Microsoft-Clouddienste zugreifen kann, als befänden diese sich in meinem eigenen Datencenter. | [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute) |
| Ich möchte Überwachung und Diagnose von Bedingungen auf der Ebene des Netzwerkszenarios bereitstellen. | [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher) |
| Ich benötige native Firewallfunktionen mit integrierter Hochverfügbarkeit, uneingeschränkter Cloudskalierbarkeit und ganz ohne Wartungsaufwand. | [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview) |
| Ich muss Geschäftsniederlassungen, Einzelhandelsstandorte und Standorte sicher verbinden. | [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan) |
| Ich benötige einen skalierbaren Bereitstellungspunkt mit erweiterter Sicherheit für globale Webanwendungen, die auf Microservices basieren. | [Azure Front Door](https://docs.microsoft.com/azure/frontdoor) |

<!-- markdownlint-enable MD033 -->

## <a name="choose-a-networking-architecture"></a>Auswählen einer Netzwerkarchitektur

Nachdem Sie die Azure-Netzwerkdienste ermittelt haben, die Sie zur Unterstützung Ihrer Workloads benötigen, müssen Sie die Architektur entwerfen, die diese Dienste kombiniert, um die Cloud-Netzwerkinfrastruktur Ihrer Landezone bereitzustellen. Der [Leitfaden zur Entscheidungsfindung für softwaredefinierte Netzwerke](../../decision-guides/software-defined-network/index.md) des Frameworks für die Cloudeinführung bietet Informationen zu den gängigsten Mustern für die Netzwerkarchitektur, die in Azure verwendet werden.

Die folgende Tabelle bietet einen Überblick über die wichtigsten Szenarien, die von diesen Mustern unterstützt werden:

| Szenario  | Vorgeschlagene Netzwerkarchitektur                                                  |
| --- | --- |
| Alle in Azure gehosteten Workloads, die in Ihrer Zielzone bereitgestellt werden, sind vollständig PaaS-basiert, erfordern kein virtuelles Netzwerk und gehören nicht zu einem größeren Cloudeinführungsprojekt mit IaaS-Ressourcen.                                                                                                                                                          | [Reine PaaS-Lösung](../../decision-guides/software-defined-network/paas-only.md)            |
| Ihre in Azure gehosteten Workloads stellen IaaS-basierte Ressourcen wie z.B. virtuelle Computer bereit oder benötigen aus einem anderen Grund ein virtuelles Netzwerk, erfordern aber keine Konnektivität zu Ihrer lokalen Umgebung.                                                                                                                                                                            | [Cloudnativ](../../decision-guides/software-defined-network/cloud-native.md)      |
| Ihre in Azure gehosteten Workloads erfordern begrenzten Zugriff auf lokale Ressourcen, Sie müssen Cloudverbindungen aber als nicht vertrauenswürdig behandeln.                                                                                                                                                                                                                             | [Cloud-DMZ](../../decision-guides/software-defined-network/cloud-dmz.md)            |
| Ihre in Azure gehosteten Workloads erfordern begrenzten Zugriff auf lokale Ressourcen, und Sie planen die Implementierung von ausgereiften Sicherheitsrichtlinien und einer sicheren Konnektivität zwischen der Cloud und Ihrer lokalen Umgebung.                                                                                                                                                           | [Hybrid](../../decision-guides/software-defined-network/hybrid.md)                  |
| Sie müssen eine große Anzahl von virtuellen Computern und Workloads bereitstellen und verwalten, wodurch möglicherweise [Grenzwerte für Azure-Abonnements](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits) überschritten werden, Sie müssen Dienste über mehrere Abonnements hinweg gemeinsam nutzen, oder Sie benötigen eine besser aufgeteilte Struktur zur Trennung von Rollen, Anwendungen oder Berechtigungen. | [Hub-and-Spoke-Architektur](../../decision-guides/software-defined-network/hub-spoke.md)        |
| Sie verfügen über eine Vielzahl von Filialstellen, die miteinander und mit Azure verbunden werden müssen.                                                                                                                                                                                                                                                                                         | [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) |

<!-- TODO: Refactor VDC content below. -->
<!-- docsTest:ignore "Azure Virtual Datacenter" -->

### <a name="azure-virtual-datacenter"></a>Virtuelles Azure-Rechenzentrum

Zusätzlich zur Verwendung dieser Architekturmuster sollte Ihre IT-Unternehmensgruppen, die umfangreiche Cloudumgebungen verwalten, sich die [CAF-Zielzone auf Unternehmensebene](../../ready/enterprise-scale/index.md) ansehen. Wenn Sie Ihre Azure-basierte Cloudinfrastruktur entwerfen, bietet die CAF-Zielzone auf Unternehmensebene einen kombinierten Ansatz für Netzwerk, Sicherheit, Verwaltung und Infrastruktur, wenn Sie mittelfristig (innerhalb von 24 Monaten) das Ziel haben, **mehr als 1.000 Ressourcen (Apps, Infrastruktur oder Datenbestände) in der Cloud zu hosten**.

Bei Organisationen, die die folgenden Kriterien erfüllen, können Sie ebenfalls mit der [CAF-Zielzone auf Unternehmensebene](../../ready/enterprise-scale/index.md) beginnen:

- Ihr Unternehmen unterliegt gesetzlichen Bestimmungen, die eine zentrale Überwachung erfordern.
- Sie müssen die Einhaltung allgemeiner Richtlinien und Governancebestimmungen sowie die zentralisierte IT-Kontrolle über die wichtigsten Dienste sicherstellen.
- Ihre Branche hängt von einer komplexen Plattform ab, die umfassende Steuerungsmechanismen und tiefgehendes Fachwissen erfordert. Dies ist am häufigsten bei großen Unternehmen im Bereich Finanzen, Öl und Gas oder Herstellung der Fall.
- Ihre bestehenden IT-Governancerichtlinien erfordern eine engere Parität mit bestehenden Funktionen, auch in frühen Phasen der Einführung.

## <a name="follow-azure-networking-best-practices"></a>Nutzen von bewährten Methoden für Netzwerke von Azure

Sehen Sie sich im Rahmen der Entwicklung Ihres Netzwerkentwurfs die folgenden Artikel an:

- [Planen virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Erfahren Sie, wie Sie virtuelle Netzwerke basierend auf Ihren Anforderungen in Bezug auf Isolierung, Verbindung und Standort planen.
- [Bewährte Methoden für die Netzwerksicherheit in Azure](https://docs.microsoft.com/azure/security/fundamentals/network-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Erfahren Sie mehr über bewährte Azure-Methoden, mit denen Sie Ihre Netzwerksicherheit verbessern können.
- [Bewährte Methoden für Netzwerke bei der Migration von Workloads zu Azure](https://docs.microsoft.com/azure/migrate/migrate-best-practices-networking?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Rufen Sie zusätzliche Informationen zum Implementieren von Azure-Netzwerkfunktionen zur Unterstützung von IaaS- und PaaS-basierten Workloads ab.
