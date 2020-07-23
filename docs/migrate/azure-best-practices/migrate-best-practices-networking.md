---
title: Bewährte Methoden zum Einrichten von Netzwerken für zu Azure migrierte Workloads
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über bewährte Methoden (Best Practices) zum Einrichten von Netzwerken für Ihre migrierten Workloads zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c3ca563579ea8879d944fb59372e213faa942f18
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194526"
---
<!-- cSpell:ignore NSGs CIDR FQDNs BGP's ACLs WAFs -->

# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Bewährte Methoden zum Einrichten von Netzwerken für zu Azure migrierte Workloads

Bei der Planung und dem Entwurf für die Migration besteht einer der wichtigsten Schritte neben der Migration selbst im Entwurf und in der Implementierung von Azure-Netzwerken. Dieser Artikel beschreibt bewährte Methoden für den Netzwerkbetrieb bei der Migration zu IaaS- und PaaS-Implementierungen in Azure.

> [!IMPORTANT]
> Die in diesem Artikel beschriebenen Best Practices und Meinungen basieren auf Azure-Plattform- und -Dienstfeatures, die zu dem Zeitpunkt verfügbar waren, zu dem dieser Artikel verfasst wurde. Features und Funktionen ändern sich im Laufe der Zeit. Nicht alle Empfehlungen sind notwendigerweise auf Ihre Bereitstellung anwendbar. Wählen Sie also diejenigen aus, die für Sie relevant sind.

## <a name="design-virtual-networks"></a>Entwerfen virtueller Netzwerke

Azure bietet virtuelle Netzwerke mit folgenden Funktionen:

- Über VNETs können Azure-Ressourcen privat, direkt und sicher miteinander kommunizieren.
- Sie können in VNETs Endpunktverbindungen für die virtuellen Computer und Dienste konfigurieren, die eine Internetkommunikation erfordern.
- Bei einem VNET handelt es sich um eine logische Isolation der dedizierten Azure-Cloud für Ihr Abonnement.
- Sie können in jedem Azure-Abonnement und jeder Azure-Region mehrere VNets implementieren.
- Jedes VNet ist von anderen VNets isoliert.
- VNETs können private und öffentliche IP-Adressen enthalten, die in [RFC 1918](https://tools.ietf.org/html/rfc1918) definiert sind und in der CIDR-Notation dargestellt werden. Auf öffentliche IP-Adressen, die im Adressraum eines VNETs angegeben wurden, kann über das Internet nicht direkt zugegriffen werden.
- VNETs können sich mittels Peering virtueller Netzwerke miteinander verbinden. Verbundene VNETs können sich in derselben oder in verschiedenen Regionen befinden. Daher können Ressourcen in einem VNET eine Verbindung mit Ressourcen in anderen VNETs herstellen.
- Azure leitet Datenverkehr standardmäßig zwischen Subnetzen innerhalb eines VNET, verbundenen VNETs, lokalen Netzwerken und dem Internet weiter.

Bei der Planung Ihrer VNET-Topologie sollten Sie überlegen, wie Sie die IP-Adressräume anordnen, ein Hub-Spoke-Netzwerk implementieren, VNETs in Subnetze segmentieren, DNS einrichten und Azure-Verfügbarkeitszonen implementieren möchten.

## <a name="best-practice-plan-ip-addressing"></a>Bewährte Methode: Planen der IP-Adressierung

Wenn Sie im Rahmen der Migration VNETs erstellen, ist es wichtig, Ihren VNET-IP-Adressraum zu planen.

- Sie müssen einen Adressraum zuweisen, der für jedes VNET nicht größer als der CIDR-Bereich `/16` ist. VNETs ermöglichen die Nutzung von 65.536 IP-Adressen. Die Zuweisung eines kleineren Präfixes als `/16` (z. B. `/15` mit 131.072 Adressen) führt dazu, dass die überzähligen IP-Adressen nicht für andere Bereiche genutzt werden können. IP-Adressen dürfen keinesfalls verschwendet werden, selbst wenn sie sich in den durch RFC 1918 definierten privaten Bereichen befinden.
- Der VNET-Adressraum darf sich nicht mit lokalen Netzwerkbereichen überschneiden.
- Verwenden Sie nicht die Netzwerkadressenübersetzung (Network Address Translation, NAT).
- Überlappende Adressen können zu Netzwerken führen, mit denen keine Verbindung hergestellt werden kann, und zu einem Routing, das nicht ordnungsgemäß funktioniert. Wenn Netzwerke überlappen, müssen Sie das Netzwerk neu entwerfen oder die Netzwerkadressenübersetzung (NAT) verwenden.

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).
- Sehen Sie sich die [häufig gestellten Fragen zu Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) an.
- Erfahren Sie mehr über [Grenzwerte für Azure-Netzwerke](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits).

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Bewährte Methode: Implementieren einer Hub-Spoke-Netzwerktopologie

Eine Hub-Spoke-Netzwerktopologie dient zur Isolation von Workloads, während Dienste wie Identität und Sicherheit gemeinsam verwendet werden.

- Der Hub ist ein Azure-VNET, das als zentraler Konnektivitätspunkt fungiert.
- Die Spokes sind VNETs, die mit dem Hub-VNET eine Verbindung über VNET-Peering herstellen.
- Gemeinsame Dienste werden im Hub bereitgestellt, während einzelne Workloads als Spokes bereitgestellt werden.

Beachten Sie Folgendes:

- Durch die Implementierung einer Hub-Spoke-Topologie in Azure werden allgemeine Dienste wie z.B. Verbindungen mit lokalen Netzwerken, Firewalls und die Isolation zwischen VNETs zentralisiert. Das Hub-VNET stellt einen zentralen Konnektivitätspunkt für lokale Netzwerke und einen Ort zum Hosten der Dienstnutzung durch Workloads bereit, die in Spoke-VNETs gehostet werden.
- Eine Hub-Spoke-Konfiguration wird in der Regel von größeren Unternehmen eingesetzt. Für kleinere Netzwerke sollte ein einfacherer Entwurf in Betracht gezogen werden, um Kosten zu sparen und die Komplexität zu verringern.
- Spoke-VNETs können zur Isolation von Workloads verwendet werden, wobei die einzelnen Spokes separat verwaltet werden. Jede Workload kann mehrere Ebenen und mehrere Subnetze umfassen, die mit Azure-Lastenausgleichsmodulen verbunden sind.
- Hub-Spoke-VNETs können in verschiedenen Ressourcengruppen und sogar in verschiedenen Abonnements implementiert werden. Wenn Sie eine Peerverbindung zwischen virtuellen Netzwerken in verschiedenen Abonnements herstellen, können die Abonnements demselben oder einem anderen Azure AD-Mandanten (Azure Active Directory) zugeordnet sein. Dies ermöglicht nicht nur eine dezentralisierte Verwaltung der einzelnen Workloads, sondern auch die gemeinsame Nutzung von Diensten im Hub-VNET.

![Change Management](./media/migrate-best-practices-networking/hub-spoke.png)
_Hub-Spoke-Topologie_

**Weitere Informationen**:

- Erfahren Sie mehr über eine [Hub-Spoke-Topologie](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke).
- Erhalten Sie Netzwerkempfehlungen für die Ausführung von [Windows-VMs](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) und [Linux-VMs](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm).
- Erfahren Sie mehr zum [Peering virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

## <a name="best-practice-design-subnets"></a>Bewährte Methode: Entwerfen von Subnetzen

Um Isolation innerhalb eines VNET bereitzustellen, segmentieren Sie es in mindestens ein Subnetz, und ordnen Sie jedem Subnetz einen Teil des VNET-Adressraums zu.

- Sie können in jedem VNET mehrere Subnetze erstellen.
- Standardmäßig leitet Azure Netzwerkdatenverkehr zwischen allen Subnetzen in einem VNET weiter.
- Ihre Subnetzentscheidungen basieren auf Ihren technischen und organisatorischen Anforderungen.
- Sie erstellen Subnetze mithilfe der CIDR-Notation.
- Beim Treffen der Entscheidung zum Netzwerkbereich für Subnetze ist unbedingt zu beachten, dass Azure aus jedem Subnetz fünf IP-Adressen zurückbehält, die nicht verwendet werden können. Wenn Sie beispielsweise das kleinste verfügbare Subnetz von `/29` (mit acht IP-Adressen) erstellen, behält Azure fünf Adressen zurück, sodass Sie nur über drei verwendbare Adressen verfügen, die den Hosts im Subnetz zugewiesen werden können.
- In den meisten Fällen verwenden Sie `/28` als das kleinste Subnetz.

**Beispiel:**

Die Tabelle zeigt ein Beispiel für ein VNET mit einem Adressbereich von `10.245.16.0/20` (segmentiert in Subnetze) für eine geplante Migration.

| Subnet | CIDR | Adressen | Verwendung |
| --- | --- | --- | --- |
| `DEV-FE-EUS2` | `10.245.16.0/22` | 1019 | Front-End/Webschicht-VMs |
| `DEV-APP-EUS2` | `10.245.20.0/22` | 1019 | App-Schicht-VMs |
| `DEV-DB-EUS2` | `10.245.24.0/23` | 507 | Datenbank-VMs |

**Weitere Informationen**:

- Erfahren Sie mehr über das [Entwerfen von Subnetzen](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation).
- [Erfahren Sie](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure), wie ein fiktives Unternehmen (Contoso) seine Netzwerkinfrastruktur für die Migration vorbereitet hat.

## <a name="best-practice-set-up-a-dns-server"></a>Bewährte Methode: Einrichten eines DNS-Servers

Azure fügt standardmäßig einen DNS-Server hinzu, wenn Sie ein VNET bereitstellen. So können Sie schnell VNETs erstellen und Ressourcen bereitstellen. Dieser DNS-Server bietet aber nur Dienste für die Ressourcen im jeweiligen VNET an. Wenn Sie mehrere VNETs miteinander verbinden oder von den VNETs aus eine Verbindung mit einem lokalen Server herstellen möchten, benötigen Sie zusätzliche Funktionen zur Namensauflösung. Beispielsweise muss Active Directory möglicherweise DNS-Namen zwischen virtuellen Netzwerken auflösen. Zu diesem Zweck stellen Sie Ihren eigenen benutzerdefinierten DNS-Server in Azure bereit.

- DNS-Server in einem virtuellen Netzwerk können DNS-Abfragen an die rekursiven Resolver in Azure weiterleiten. Dadurch können Sie Hostnamen innerhalb dieses virtuellen Netzwerks auflösen. Beispielsweise kann ein in Azure ausgeführter Domänencontroller auf DNS-Abfragen für die eigenen Domänen antworten und alle anderen Abfragen an Azure weiterleiten.
- Durch die DNS-Weiterleitung sind sowohl Ihre lokalen Ressourcen (über den Domänencontroller) als auch die von Azure bereitgestellten Hostnamen (über die Weiterleitung) für die virtuellen Computer sichtbar. Der Zugriff auf die rekursiven Resolver in Azure wird über die virtuelle IP-Adresse `168.63.129.16` bereitgestellt.
- Durch die DNS-Weiterleitung wird außerdem eine DNS-Auflösung zwischen VNETs ermöglicht, sodass die lokalen Computer von Azure bereitgestellte Hostnamen auflösen können.
  - Um den Hostnamen eines virtuellen Computers aufzulösen, muss sich die DNS-Server-VM im selben VNET befinden und zur Weiterleitung von Abfragen für Hostnamen an Azure konfiguriert sein.
  - Da jedes VNET ein eigenes DNS-Suffix verwendet, können Sie mithilfe von Regeln für die bedingte Weiterleitung DNS-Abfragen zur Auflösung an das richtige VNET senden.
- Wenn Sie eigene DNS-Server verwenden, können Sie für jedes VNET mehrere DNS-Server angeben. Sie können auch mehrere DNS-Server pro Netzwerkschnittstelle (für Azure Resource Manager) oder pro Clouddienst (für das klassische Bereitstellungsmodell) angeben.
- Die für eine Netzwerkschnittstelle oder einen Clouddienst angegebenen DNS-Server besitzen Vorrang vor den für das VNET angegebenen DNS-Servern.
- Im Azure Resource Manager-Bereitstellungsmodell können Sie DNS-Server für ein VNET und eine Netzwerkschnittstelle angeben. Es wird jedoch als bewährte Methode empfohlen, die Einstellung nur für VNETs zu verwenden.

    ![DNS-Server](./media/migrate-best-practices-networking/dns2.png) _DNS-Server für ein VNET_

**Weitere Informationen**:

- Erfahren Sie mehr über die [Namensauflösung, wenn Sie einen eigenen DNS-Server verwenden](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure).
- Erfahren Sie mehr über [DNS-Benennungsregeln und -Einschränkungen](../../ready/azure-best-practices/naming-and-tagging.md).

## <a name="best-practice-set-up-availability-zones"></a>Bewährte Methode: Einrichten von Verfügbarkeitszonen

Verfügbarkeitszonen sorgen für höhere Verfügbarkeit, um Ihre Anwendungen und Daten vor Rechenzentrumsausfällen zu schützen.

- Verfügbarkeitszonen sind eindeutige physische Standorte in einer Azure-Region.
- Jede Zone besteht aus mindestens einem Rechenzentrum, dessen Stromversorgung, Kühlung und Netzwerkbetrieb unabhängig funktionieren.
- Zur Gewährleistung der Resilienz sind in allen aktivierten Regionen mindestens drei separate Zonen vorhanden.
- Die physische Trennung von Verfügbarkeitszonen innerhalb einer Region schützt Anwendungen und Daten vor Ausfällen von Rechenzentren.
- Zonenredundante Dienste replizieren Ihre Anwendungen und Daten in mehreren Verfügbarkeitszonen, um sie vor Single Points of Failure zu schützen. Mit Verfügbarkeitszonen bietet Azure eine Betriebszeit-SLA von 99,99 Prozent für VMs.

    ![Verfügbarkeitszone](./media/migrate-best-practices-networking/availability-zone.png) _Verfügbarkeitszone_

- Planen und integrieren Sie Hochverfügbarkeit in Ihre Migrationsarchitektur, indem Sie Ihre Compute-, Speicher-, Netzwerk- und Datenressourcen in eine Zone aufnehmen und in anderen Zonen replizieren. Azure-Dienste, die Verfügbarkeitszonen unterstützen, können in zwei Kategorien unterteilt werden:
  - **Zonendienste:** Sie ordnen eine Ressource einer bestimmten Zone – z B. VMs, verwalteten Datenträgern oder IP-Adressen – zu.
  - **Zonenredundante Dienste:** Die Ressource wird zonenübergreifend automatisch repliziert, z. B. zonenredundanter Speicher oder Azure SQL-Datenbank.
- Sie können eine Standard-Azure-Last bereitstellen, die mit dem Internet zugewandten Workloads oder Logikschichten ausgeglichen wird, um zonengebundene Fehlertoleranz bereitzustellen.

    ![Lastenausgleich](./media/migrate-best-practices-networking/load-balancer.png) _Lastenausgleich_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Verfügbarkeitszonen](https://docs.microsoft.com/azure/availability-zones/az-overview).

## <a name="design-hybrid-cloud-networking"></a>Entwerfen von Hybridcloudnetzwerken

Für eine erfolgreiche Migration ist es wichtig, eine Verbindung zwischen lokalen Unternehmensnetzwerke mit Azure herzustellen. Dadurch entsteht eine Always On-Verbindung, die als Hybridcloudnetzwerk bezeichnet wird. In diesem Netzwerk werden den Unternehmensbenutzern Dienste aus der Azure-Cloud bereitgestellt. Es gibt zwei Optionen zum Erstellen dieser Art von Netzwerk:

- **Site-to-Site-VPN:** Sie erstellen eine Site-to-Site-Verbindung zwischen Ihrem kompatiblen lokalen VPN-Gerät und einem Azure-VPN-Gateway, das in einem VNET bereitgestellt wird. Jede autorisierte lokale Ressource kann auf VNETs zugreifen. Die Site-to-Site-Kommunikation wird durch einen verschlüsselten Tunnel über das Internet gesendet.
- **Azure ExpressRoute:** Sie stellen eine Azure ExpressRoute-Verbindung zwischen Ihrem lokalen Netzwerk und Azure über einen ExpressRoute-Partner her. Diese Verbindung ist privat, und der Datenverkehr wird nicht über das Internet geleitet.

**Weitere Informationen**:

- Erfahren Sie mehr über [Hybridcloudnetzwerke](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn).

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Bewährte Methode: Implementieren eines hochverfügbaren Site-to-Site-VPN

Zum Implementieren eines Site-to-Site-VPN richten Sie ein VPN-Gateway in Azure ein.

- Ein VPN-Gateway ist eine spezielle Art von VNET-Gateway, das verschlüsselten Datenverkehr zwischen einem Azure-VNET und einem lokalen Standort über das öffentliche Internet sendet.
- Ein VPN-Gateway kann aber auch verschlüsselten Datenverkehr zwischen Azure-VNETs über das Microsoft-Netzwerk senden.
- Jedes VNET kann nur ein einzelnes VPN-Gateway besitzen.
- Sie können mehrere Verbindungen mit dem gleichen VPN-Gateway herstellen. Wenn Sie mehrere Verbindungen herstellen, wird die für das Gateway zur Verfügung stehende Bandbreite auf alle VPN-Tunnel aufgeteilt.
- Jede Azure-VPN-Gateway-Instanz umfasst zwei VM-Instanzen in einer Konfiguration mit aktivem Standbymodus.
  - Bei geplanten Wartungsarbeiten oder ungeplanten Störungen für die aktive Instanz findet automatisch ein Failover statt. Die Standbyinstanz übernimmt automatisch und stellt die Site-to-Site- oder VNET-to-VNET-Verbindung wieder her.
  - Der Wechsel verursacht eine kurze Unterbrechung.
  - Bei der geplanten Wartung sollte die Konnektivität innerhalb von 10 bis 15 Sekunden wiederhergestellt werden.
  - Bei ungeplanten Problemen dauert die Verbindungswiederherstellung länger – schlimmstenfalls zwischen einer und anderthalb Minuten.
  - Point-to-Site-VPN-Clientverbindungen mit dem Gateway werden getrennt, und die Benutzer müssen die Verbindungen von den Clientcomputern aus neu herstellen.

Beim Einrichten eines Site-to-Site-VPN gehen Sie folgendermaßen vor:

- Sie benötigen ein VNET, dessen Adressraum sich mit dem lokalen Netzwerk, mit dem das VPN eine Verbindung herstellen soll, nicht überschneidet.
- Sie erstellen ein Gatewaysubnetz im Netzwerk.
- Sie erstellen ein VPN-Gateway, geben den Gatewaytyp (VPN) an und legen fest, ob es sich um ein richtlinienbasiertes oder um ein routenbasiertes Gateway handelt. Ein routenbasiertes VPN wird als leistungsstärker und zukunftssicherer angesehen.
- Sie erstellen ein lokales Netzwerkgateway und konfigurieren Ihr lokales VPN-Gerät.
- Sie erstellen eine Site-to-Site-VPN-Failoververbindung zwischen dem VNET-Gateway und dem lokalen Gerät. Die Verwendung eines routenbasierten VPN ermöglicht Aktiv/Passiv- oder Aktiv/Aktiv-Verbindungen mit Azure. Ein routenbasiertes VPN unterstützt parallel sowohl Site-to-Site- (von einem beliebigen Computer aus) als auch Point-to-Site-Verbindungen (von einem einzigen Computer aus).
- Sie geben die gewünschte Gateway-SKU aus. Diese richtet sich nach Ihren Workloadanforderungen, Durchsätzen, Features und SLAs.
- BGP (Border Gateway Protocol) ist ein optionales Feature, das Sie mit Azure ExpressRoute und routenbasierten VPN-Gateways verwenden können, um Ihre lokalen BGP-Routen auf Ihre VNETs zu verteilen.

![VPN](./media/migrate-best-practices-networking/vpn.png)
_Site-to-Site-VPN_

**Weitere Informationen**:

- Informieren Sie sich über [kompatible lokale VPN-Geräte](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).
- Lesen Sie die [Übersicht über Azure-VPN-Gateways](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).
- Erhalten Sie Informationen zu [hochverfügbaren VPN-Verbindungen](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable).
- Erfahren Sie mehr über das [Planen und Entwerfen eines VPN-Gateways](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).
- Informieren Sie sich über [VPN-Gatewayeinstellungen](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku).
- Informieren Sie sich über [Gateway-SKUs](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku).
- [Erfahren Sie mehr](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) über das Einrichten von BGP mit Azure-VPN-Gateways.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Bewährte Methode: Konfigurieren eines Gateways für VPN-Gateways

Wenn Sie ein VPN-Gateway in Azure erstellen, müssen Sie ein spezielles Subnetz namens `GatewaySubnet` verwenden. Beachten Sie bei der Erstellung dieses Subnetzes folgende bewährte Methoden:

- `GatewaySubnet` kann eine maximale Präfixlänge von 29 aufweisen (z. B. `10.119.255.248/29`). Aktuell wird empfohlen, eine Präfixlänge von 27 zu verwenden (z. B. `10.119.255.224/27`).
- Wenn Sie den Adressraum des Gatewaysubnetzes definieren, verwenden Sie den allerletzten Teil des VNET-Adressraums.
- Wenn Sie das Subnetz Ihres Azure-Gateways verwenden, stellen Sie dem Gatewaysubnetz keine VMs oder andere Geräte wie z. B. Application Gateway bereit.
- Weisen Sie diesem Subnetz keine Netzwerksicherheitsgruppe (NSG) zu. Dadurch würde die Funktion des Gateways beendet.

**Weitere Informationen**:

- [Verwenden Sie dieses Tool](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed), um Ihren IP-Adressraum zu ermitteln.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Bewährte Methode: Implementieren von Azure Virtual WAN für Filialen

Der Netzwerkdienst Azure Virtual WAN bietet für eine mehrere VPN-Verbindungen optimierte und automatisierte Konnektivität zwischen Filialen über Azure.

- Per Virtual WAN können Sie Filialgeräte für die Kommunikation mit Azure verbinden und konfigurieren. Dies ist manuell oder durch die Nutzung von Geräten eines bevorzugten Anbieters über einen Azure Virtual WAN-Partner möglich.
- Die Nutzung von Geräten eines bevorzugten Anbieters ermöglicht eine einfache Verwendung, Konnektivität und Konfigurationsverwaltung.
- Über das integrierte Azure WAN-Dashboard können Sie anhand der Problembehandlung sofort Erkenntnisse gewinnen, um Zeit zu sparen. Zudem können Sie auf einfache Weise umfangreiche Site-to-Site-Verbindungen überwachen.

**Weitere Informationen**: Erfahren Sie mehr über [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about).

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Bewährte Methode: Implementieren von ExpressRoute für unternehmenskritische Verbindungen

Mit dem Azure ExpressRoute-Dienst erweitern Sie Ihre lokale Infrastruktur in die Microsoft-Cloud, indem Sie private Verbindungen zwischen dem virtuellen Azure-Rechenzentrum und lokalen Netzwerken erstellen.

- ExpressRoute-Verbindungen können über ein IP-VPN-Netzwerk (Any-to-Any), ein Point-to-Point-Ethernet-Netzwerk oder über einen Konnektivitätsanbieter hergestellt werden. Sie verlaufen nicht über das öffentliche Internet.
- ExpressRoute-Verbindungen bieten bei gleichbleibenden Wartezeiten mehr Sicherheit und Zuverlässigkeit sowie höhere Geschwindigkeiten (bis zu 10 GBit/s).
- ExpressRoute ist nützlich für virtuelle Rechenzentren, weil Kunden von den Konformitätsregeln privater Verbindungen profitieren.
- Mit ExpressRoute Direct können Sie bei höherem Bandbreitenbedarf eine direkte 100 GBit/s-Verbindung mit Microsoft-Routern herstellen.
- ExpressRoute verwendet BGP zum Austauschen von Routen zwischen lokalen Netzwerken, Azure-Instanzen und öffentlichen Microsoft-Adressen.

Für die Bereitstellung von ExpressRoute-Verbindungen ist in der Regel ein ExpressRoute-Dienstanbieter erforderlich. Für einen schnellen Einstieg werden anfangs üblicherweise Site-to-Site-VPN-Verbindungen für die Konnektivität zwischen dem virtuellen Rechenzentrum und lokalen Ressourcen verwendet. Anschließend erfolgt die Migration zu einer ExpressRoute-Verbindung, wenn eine physische Verbindung mit Ihrem Dienstanbieter eingerichtet wurde.

**Weitere Informationen**:

- [Lesen Sie eine Übersicht](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) über ExpressRoute.
- Informieren Sie sich über [ExpressRoute Direct](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about).

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Bewährte Methode: Optimieren von ExpressRoute-Routing mit BGP-Communitys

Wenn Sie mehrere ExpressRoute-Verbindungen nutzen, verfügen Sie über mehr als einen Weg zur Herstellung einer Verbindung mit Microsoft. Dies kann ein suboptimales Routing zur Folge haben, und Ihr Datenverkehr verwendet möglicherweise einen längeren Pfad zu Microsoft bzw. von Microsoft zu Ihrem Netzwerk. Je länger der Netzwerkpfad, desto höher die Latenz. Die Latenz wirkt sich direkt auf die Anwendungsleistung und die Benutzerfreundlichkeit aus.

**Beispiel:**

Schauen wir uns ein Beispiel an:

- Sie verfügen über zwei Niederlassungen in den USA: eine in Los Angeles und eine in New York City.
- Die Niederlassungen sind über ein WAN verbunden, wobei es sich entweder um Ihr eigenes Backbonenetzwerk oder die IP-VPN-Verbindung Ihres Dienstanbieters handeln kann.
- Sie verfügen über zwei ExpressRoute-Verbindungen – eine in der Region `West US` und eine in der Region `East US` –, die ebenfalls per WAN verbunden sind. Es sind also zwei Wege zum Herstellen der Verbindung mit dem Microsoft-Netzwerk vorhanden.

**Problem:**

Nehmen Sie weiter an, dass Sie über jeweils eine Azure-Bereitstellung (z. B. Azure App Service) in `West US` und `East US` verfügen.

- Die Benutzer in beiden Niederlassungen sollen auf die nächstgelegenen Azure-Dienste zugreifen, um eine optimale Leistung zu erzielen.
- Daher sollen Benutzer in Los Angeles eine Verbindung mit der Azure-Region `West US` und Benutzer in New York eine Verbindung mit der Azure-Region `East US` herstellen.
- Dies funktioniert für Benutzer an der Ostküste, aber nicht für Benutzer an der Westküste. Das Problem ist Folgendes:
  - Für jede ExpressRoute-Leitung kündigen wir sowohl das Präfix in der Azure-Region `East US` (`23.100.0.0/16`) als auch das Präfix in der Azure-Region `West US` (`13.100.0.0/16`) an.
  - Wenn nicht bekannt ist, welches Präfix aus welcher Region stammt, werden die Präfixe nicht unterschiedlich behandelt.
  - Ihr WAN geht möglicherweise davon aus, dass beide Präfixe näher bei `East US` als bei `West US` liegen, und leitet daher Benutzer aus beiden Niederlassungen an die ExpressRoute-Leitung in `East US` weiter, sodass für Benutzer in der Niederlassung in Los Angeles eine suboptimale Leistung erzielt wird.

![VPN](./media/migrate-best-practices-networking/bgp1.png)
_Nicht optimierte Verbindung über BGP-Communitys_

**Lösung:**

Zum Optimieren des Routings für die Benutzer beider Niederlassungen müssen Sie wissen, welches Präfix für die Azure-Region `West US` und welches Präfix für die Region `East US` gilt. Sie können diese Informationen mithilfe von BGP-Communitywerten codieren.

- Sie weisen jeder Azure-Region einen eindeutigen BGP-Communitywert zu. Beispiel: 12076:51004 für `East US` und 12076:51006 für `West US`.
- Damit ist klar, welches Präfix zu welcher Azure-Region gehört, sodass Sie eine bevorzugte ExpressRoute-Leitung konfigurieren können.
- Da Sie BGP zum Austauschen von Routinginformationen verwenden, können Sie über die lokale Einstellung von BGP das Routing beeinflussen.
- In unserem Beispiel weisen Sie `13.100.0.0/16` in `West US` einen höheren Wert für die lokale Einstellung als für `East US` zu (bzw. einen höheren Wert für die lokale Einstellung für `23.100.0.0/16` in `East US` als in `West US`).
- Diese Konfiguration stellt bei Verfügbarkeit beider Pfade zu Microsoft sicher, dass Benutzer in Los Angeles über die westliche Leitung eine Verbindung mit der Region `West US` herstellen und Benutzer in New York über die östliche Leitung eine Verbindung mit der Region `East US`. Das Routing ist somit auf beiden Seiten optimiert.

![VPN](./media/migrate-best-practices-networking/bgp2.png)
_Optimierte Verbindung über BGP-Communitys_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Optimieren des Routings](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing).

## <a name="secure-vnets"></a>Schützen von VNETs

Die Verantwortung für das Schützen von VNETs liegt zu gleichen Teilen bei Microsoft und bei Ihnen. Microsoft bietet viele Netzwerkfeatures und Dienste, die zum Schutz der Ressourcen dienen. Beim Planen der Sicherheit für VNETs sind bewährte Methoden, die Sie befolgen sollten, unter anderem die Implementierung eines Umkreisnetzwerks, die Verwendung von Filtern und Sicherheitsgruppen, das Absichern des Zugriffs auf Ressourcen und IP-Adressen sowie die Implementierung einer Schutzfunktion vor Angriffen.

**Weitere Informationen**:

- Lesen Sie eine [Übersicht über bewährte Methoden für die Netzwerksicherheit](https://docs.microsoft.com/azure/security/fundamentals/network-best-practices).
- Erfahren Sie mehr über das [Entwerfen sicherer Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security).

<!-- docsTest:ignore "IDS/IPS" -->

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Bewährte Methode: Implementieren eines Azure-Umkreisnetzwerks

Wenngleich Microsoft hohe Investitionen in den Schutz der Cloudinfrastruktur tätigt, müssen Sie ebenfalls für den Schutz Ihrer Clouddienste und Ressourcengruppen sorgen. Ein mehrstufiger Sicherheitsansatz bietet die beste Absicherung. Die Einrichtung eines Umkreisnetzwerks ist ein wichtiger Bestandteil dieser Schutzstrategie.

- Ein Umkreisnetzwerk schützt die internen Netzwerkressourcen vor einem nicht vertrauenswürdigen Netzwerk.
- Dabei handelt es sich um die äußerste Schicht, die mit dem Internet verbunden ist. Sie befindet sich normalerweise zwischen dem Internet und der Infrastruktur des Unternehmens, in der Regel mit irgendeiner Art des Schutzes auf beiden Seiten.
- In einer typischen Unternehmensnetzwerktopologie wird der Kern der Infrastruktur im Umkreisnetzwerk durch mehrere Stufen von Sicherheitsgeräten stark geschützt. An den Grenzen der einzelnen Stufen befinden sich Sicherheitsgeräte und Stellen zur Durchsetzung von Richtlinien.
- Jede Stufe kann eine Kombination der Netzwerksicherheitslösungen enthalten, darunter Firewalls, DoS-Schutz (Denial of Service), IDS/IPS (Intrusion Detection/Protection Systems) und VPN-Geräte.
- Die Durchsetzung von Richtlinien im Umkreisnetzwerk kann über Firewallrichtlinien, Zugriffssteuerungslisten (Access Control Lists, ACLs) oder ein spezifisches Routing erfolgen.
- Wenn Datenverkehr über das Internet eingeht, wird er abgefangen und durch eine Kombination von Verteidigungslösungen verarbeitet, um Angriffe und schädlichen Datenverkehr zu blockieren, aber legitime Anforderungen an das Netzwerk zuzulassen.
- Der eingehende Datenverkehr kann direkt an Ressourcen im Umkreisnetzwerk weitergeleitet werden. Die Umkreisnetzwerkressource kann dann mit anderen, tiefer im Netzwerk befindlichen Ressourcen kommunizieren und den Datenverkehr nach der Überprüfung an das Netzwerk weiterleiten.

Die nachfolgende Abbildung zeigt ein Beispiel für ein Umkreisnetzwerk mit einem einzigen Subnetz in einem Unternehmensnetzwerk. Es umfasst zwei Sicherheitsgrenzen.

![VPN](./media/migrate-best-practices-networking/perimeter.png)
_Bereitstellung eines Umkreisnetzwerks_

**Weitere Informationen**:

- Erfahren Sie mehr über die [Bereitstellung eines Umkreisnetzwerks zwischen Azure und Ihrem lokalen Rechenzentrum](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz).

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Bewährte Methode: Filtern von VNET-Datenverkehr mit Netzwerksicherheitsgruppen

Netzwerksicherheitsgruppen (NSG) enthalten mehrere Sicherheitsregeln zum Filtern des bei Ressourcen eingehenden bzw. von ihnen ausgehenden Datenverkehrs. Das Filtern kann nach Quell- und Ziel-IP-Adresse, Port und Protokoll erfolgen.

- NSGs enthalten Sicherheitsregeln, die eingehenden Netzwerkdatenverkehr an verschiedene Typen von Azure-Ressourcen (bzw. von ihnen ausgehenden Netzwerkdatenverkehr) zulassen oder verweigern. Für jede Regel können Sie die Quelle, das Ziel, den Port und das Protokoll angeben.
- NSG-Regeln werden nach Priorität anhand der 5-Tupel-Informationen (Quelle, Quellport, Ziel, Zielport und Protokoll) ausgewertet, um den Datenverkehr zuzulassen oder zu verweigern.
- Für vorhandene Verbindungen wird ein Flussdatensatz erstellt. Die Kommunikation wird basierend auf dem Verbindungszustand der Flussdatensätze zugelassen oder verweigert.
- Durch einen Datenflussdatensatz kann eine NSG zustandsbehaftet sein. Wenn Sie beispielsweise eine Sicherheitsregel für ausgehenden Datenverkehr an eine beliebige Adresse über Port 80 angeben, ist es nicht erforderlich, für die Antwort auf den ausgehenden Datenverkehr eine Sicherheitsregel für eingehenden Datenverkehr anzugeben. Sie müssen nur dann eine Sicherheitsregel für Datenverkehr in eingehender Richtung angeben, wenn die Kommunikation extern initiiert wird.
- Dies gilt auch für den umgekehrten Fall. Wenn eingehender Datenverkehr über einen Port zugelassen wird, ist es nicht erforderlich, für die Beantwortung des Datenverkehrs über den Port eine Sicherheitsregel für ausgehenden Datenverkehr anzugeben.
- Vorhandene Verbindungen werden nicht unterbrochen, wenn Sie eine Sicherheitsregel entfernen, die den Datenfluss ermöglicht hat. Datenverkehrsflüsse werden unterbrochen, wenn Verbindungen beendet werden und in beide Richtungen mindestens einige Minuten lang kein Datenverkehr besteht.
- Erstellen Sie immer so wenige NSGs wie möglich, aber so viele wie nötig.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Bewährte Methode: Schützen von Datenverkehr in Nord-Süd- und Ost-West-Richtung

Beim Schützen von VNETs müssen Angriffsvektoren unbedingt berücksichtigt werden.

- Durch die ausschließliche Verwendung von Subnetz-NSGs wird Ihre Umgebung vereinfacht, aber nur der Datenverkehr in Ihr Subnetz abgesichert. Dies wird als Nord-Süd-Datenverkehr bezeichnet.
- Der Datenverkehr zwischen virtuellen Computern im selben Subnetz wird Ost-West-Datenverkehr genannt.
- Sie sollten unbedingt beide Schutzformen einsetzen, sodass ein Hacker, der von außen Zugriff erlangt, gestoppt wird, wenn er auf Computer in demselben Subnetz zuzugreifen versucht.

### <a name="use-service-tags-on-nsgs"></a>Verwenden von Diensttags für NSGs

Ein Diensttag steht für eine Gruppe von IP-Adresspräfixen. Durch Verwendung eines Diensttags ist die Erstellung von NSG-Regeln weniger komplex.

- Bei der Erstellung von Regeln können Sie Diensttags anstelle spezifischer IP-Adressen nutzen.
- Microsoft verwaltet die Adresspräfixe, die einem Diensttag zugeordnet sind, und aktualisiert das Diensttag automatisch, wenn sich die Adressen ändern.
- Sie können kein eigenes Diensttag erstellen und auch nicht angeben, welche IP-Adressen in einem Tag enthalten sind.

Diensttags ersparen Ihnen die manuelle Arbeit beim Zuweisen einer Regel zu Gruppen von Azure-Diensten. Wenn Sie beispielsweise einem Subnetz mit Webservern den Zugriff auf Azure SQL-Datenbank ermöglichen möchten, können Sie eine Ausgangsregel für Port 1433 erstellen und das Diensttag **Sql** verwenden.

- Dieses **Sql**-Tag gibt die Adresspräfixe der Azure SQL-Datenbank- und Azure SQL Data Warehouse-Dienste an.
- Wenn Sie **Sql** als Wert angeben, wird der Datenverkehr für SQL zugelassen oder verweigert.
- Falls Sie den Zugriff auf **Sql** nur für eine bestimmte Region zulassen möchten, können Sie die betreffende Region angeben. Wenn Sie den Zugriff auf Azure SQL-Datenbank beispielsweise nur für die Region „USA, Osten“ zulassen möchten, können Sie **Sql.EastUS** für das Diensttag angeben.
- Das Tag steht für den Dienst, aber nicht für bestimmte Instanzen des Diensts. Beispielsweise steht das Tag für den Azure SQL-Datenbank-Dienst, aber nicht für eine bestimmte SQL-Datenbank oder einen bestimmten SQL-Server.
- Alle Adresspräfixe, für die dieses Tag steht, werden auch durch das **Internet**-Tag repräsentiert.

**Weitere Informationen**:

- Lesen Sie Informationen zu [Netzwerksicherheitsgruppen (NSGs)](https://docs.microsoft.com/azure/virtual-network/security-overview).
- Informieren Sie sich über [die für NSGs verfügbaren Diensttags](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags).

## <a name="best-practice-use-application-security-groups"></a>Bewährte Methode: Verwenden von Anwendungssicherheitsgruppen

Mit Anwendungssicherheitsgruppen können Sie die Netzwerksicherheit als natürliche Erweiterung einer Anwendungsstruktur konfigurieren.

- Anhand von Anwendungssicherheitsgruppen können Sie virtuelle Computer gruppieren und Netzwerksicherheitsrichtlinien definieren.
- Anwendungssicherheitsgruppen ermöglichen Ihnen die bedarfsabhängige Wiederverwendung Ihrer Sicherheitsrichtlinie, ohne dass Sie explizite IP-Adressen manuell warten müssen.
- Anwendungssicherheitsgruppen übernehmen die komplexe Verarbeitung expliziter IP-Adressen und mehrerer Regelsätze, damit Sie sich auf Ihre Geschäftslogik konzentrieren können.

**Beispiel:**

![Anwendungssicherheitsgruppe](./media/migrate-best-practices-networking/asg.png)
_Beispiel für eine Anwendungssicherheitsgruppe_

| Netzwerkschnittstelle | Anwendungssicherheitsgruppe |
| --- | --- |
| `NIC1` | `AsgWeb` |
| `NIC2` | `AsgWeb` |
| `NIC3` | `AsgLogic` |
| `NIC4` | `AsgDb` |

- In unserem Beispiel gehört jede Netzwerkschnittstelle nur einer Anwendungssicherheitsgruppe an, aber tatsächlich kann eine Schnittstelle mehreren Gruppen angehören (in Übereinstimmung mit der Azure-Grenzwerten).
- Keiner der Netzwerkschnittstellen ist eine NSG zugeordnet. `NSG1` ist beiden Subnetzen zugeordnet und enthält die folgenden Regeln.

| Regelname | Zweck | Details |
| --- | --- | --- |
| `Allow-HTTP-Inbound-Internet` | Hiermit wird Datenverkehr aus dem Internet an die Webserver zugelassen. Eingehender Datenverkehr aus dem Internet wird durch die Standardsicherheitsregel `DenyAllInbound` verweigert, daher ist keine zusätzliche Regel für die Anwendungssicherheitsgruppen `AsgLogic` oder `AsgDb` erforderlich. | Priorität: `100`<br><br> Quelle: `internet` <br><br> Quellport: `*` <br><br> Ziel: `AsgWeb` <br><br> Zielport: `80` <br><br> Protokoll: `TCP` <br><br> Zugriff: `Allow` |
| `Deny-Database-All` | Die Standardsicherheitsregel `AllowVNetInBound` erlaubt die gesamte Kommunikation zwischen Ressourcen im gleichen VNET, daher ist diese Regel erforderlich, um den Datenverkehr von allen Ressourcen zu verweigern. | Priorität: `120` <br><br> Quelle: `*` <br><br> Quellport: `*` <br><br> Ziel: `AsgDb` <br><br> Zielport: `1433` <br><br> Protokoll: `All` <br><br> Zugriff: `Deny` |
| `Allow-Database-BusinessLogic` | Diese Regel lässt Datenverkehr von der Anwendungssicherheitsgruppe `AsgLogic` an die Anwendungssicherheitsgruppe `AsgDb` zu. Da die Priorität für diese Regel höher ist als die Priorität der Regel `Deny-Database-All`, wird diese Regel zuerst verarbeitet. Dies führt dazu, dass Datenverkehr von der Anwendungssicherheitsgruppe `AsgLogic` zugelassen und jeglicher andere Datenverkehr blockiert wird. | Priorität: `110` <br><br> Quelle: `AsgLogic` <br><br> Quellport: `*` <br><br> Ziel: `AsgDb` <br><br> Zielport: `1433` <br><br> Protokoll: `TCP` <br><br> Zugriff: `Allow` |

- Regeln, in denen eine Anwendungssicherheitsgruppe als Quelle oder Ziel angegeben ist, werden nur auf Netzwerkschnittstellen angewendet, bei denen es sich um Mitglieder der Anwendungssicherheitsgruppe handelt. Wenn die Netzwerkschnittstelle nicht Mitglied einer Anwendungssicherheitsgruppe ist, wird die Regel nicht auf die Netzwerkschnittstelle angewendet, auch wenn die Netzwerksicherheitsgruppe dem Subnetz zugeordnet ist.

**Weitere Informationen**:

- Informieren Sie sich über [Anwendungssicherheitsgruppen](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups).

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Bewährte Methode: Schützen des Zugriffs auf PaaS mithilfe von VNET-Dienstendpunkten

Durch VNET-Dienstendpunkte wird Ihr privater VNET-Adressraum und die Identität Ihres VNET über eine direkte Verbindung auf Azure-Dienste erweitert.

- Mit Endpunkten können Sie Ihre kritischen Azure-Dienstressourcen auf Ihre virtuellen Netzwerke beschränken und somit schützen. Der Datenverkehr aus Ihrem VNET an den Azure-Dienst verbleibt immer im Backbone-Netzwerk von Azure.
- Der private VNET-Adressraum kann sich überschneiden und daher nicht zur eindeutigen Identifizierung von Datenverkehr aus einem VNET verwendet werden.
- Nachdem Dienstendpunkte in Ihrem VNET aktiviert wurden, können Sie Ressourcen von Azure-Diensten schützen, indem Sie den Dienstressourcen eine VNET-Regel hinzufügen. Auf diese Weise erhöhen Sie die Sicherheit, da der Ressourcenzugriff über das öffentliche Internet vollständig verhindert und nur Datenverkehr aus Ihrem VNET zugelassen wird.

![Dienstendpunkte](./media/migrate-best-practices-networking/endpoint.png)
_Dienstendpunkte_

**Weitere Informationen**:

- Informieren Sie sich über [VNET-Dienstendpunkte](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview).

## <a name="best-practice-control-public-ip-addresses"></a>Bewährte Methode: Steuern öffentlicher IP-Adressen

Öffentliche IP-Adressen in Azure können virtuellen Computern, Lastenausgleichsmodulen, Application Gateways und VPN-Gateways zugeordnet werden.

- Anhand öffentlicher IP-Adressen können Internetressourcen in eingehender Richtung mit Azure-Ressourcen und Azure-Ressourcen in ausgehender Richtung mit dem Internet kommunizieren.
- Öffentliche IP-Adressen werden mit einer „Basic“- oder „Standard“-SKU erstellt, bei denen es mehrere Unterschiede gibt. Standard-SKUs können jedem Dienst zugewiesen werden, werden jedoch meistens für virtuelle Computer, Lastenausgleichsmodule und Application Gateways konfiguriert.
- Es ist wichtig zu beachten, dass für eine öffentliche IP-Adresse der SKU „Basic“ nicht automatisch eine NSG konfiguriert wird. Sie müssen eine eigene NSG konfigurieren und Regeln zum Steuern des Zugriffs zuweisen. IP-Adressen der SKU „Standard“ umfassen eine Netzwerksicherheitsgruppe und standardmäßig zugewiesene Regeln.
- Als bewährte Methode dürfen VMs nicht mit einer öffentlichen IP-Adresse konfiguriert werden.
  - Wenn Sie einen geöffneten Port benötigen, sollte dies nur für Webdienste erfolgen (z.B. Port 80 oder 443).
  - Standard-Remoteverwaltungsports wie SSH (22) und RDP (3389) sollten wie alle übrigen Ports anhand von NSGs auf „Verweigern“ festgelegt werden.
- Eine bessere Methode besteht darin, VMs hinter einem Azure Load Balancer oder Application Gateway zu platzieren. Wenn anschließend ein Zugriff auf Remoteverwaltungsports erforderlich ist, können Sie Just-In-Time-VM-Zugriff im Azure Security Center verwenden.

**Weitere Informationen**:

- [Öffentliche IP-Adressen in Azure](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses)
- [Verwalten des Zugriffs auf virtuelle Computer mithilfe des Just-In-Time-Features](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Nutzen von Azure-Sicherheitsfeatures für Netzwerke

Azure bietet Features für die Plattformsicherheit, die benutzerfreundlich sind und umfassende Gegenmaßnahmen für allgemeine Netzwerkangriffe bereitstellen. Dazu gehören Azure Firewall, Web Application Firewall und Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Bewährte Methode: Bereitstellen von Azure Firewall

Azure Firewall ist ein verwalteter, cloudbasierter Netzwerksicherheitsdienst zum Schutz Ihrer VNET-Ressourcen. Es handelt sich dabei um eine vollständig zustandsbehaftete verwaltete Firewall mit integrierter Hochverfügbarkeit und uneingeschränkter Cloudskalierbarkeit.

![Dienstendpunkte](./media/migrate-best-practices-networking/firewall.png)
_Azure Firewall_

- Azure Firewall kann Richtlinien zur Anwendungs- und Netzwerkkonnektivität übergreifend für Abonnements und VNETs zentral erstellen, erzwingen und protokollieren.
- Azure Firewall verwendet eine statische öffentliche IP-Adresse für Ihre VNET-Ressourcen, die es außenstehenden Firewalls ermöglicht, Datenverkehr aus Ihrem VNET zu identifizieren.
- Azure Firewall ist für Protokollierung und Analyse vollständig in Azure Monitor integriert.
- Als bewährte Methode bei der Erstellung von Azure Firewall-Regeln empfiehlt sich die Verwendung der FQDN-Tags, um Regeln zu erstellen.
  - Ein FQDN-Tag stellt eine Gruppe von FQDNs dar, die bekannten Microsoft-Diensten zugeordnet sind.
  - Sie können ein FQDN-Tag verwenden, um den erforderlichen ausgehenden Netzwerkdatenverkehr über die Firewall zuzulassen.
- Um beispielsweise den Netzwerkdatenverkehr von Windows Update manuell über Ihre Firewall zuzulassen, müssen Sie mehrere Anwendungsregeln erstellen. Mit FQDN-Tags erstellen Sie eine Anwendungsregel und schließen das Windows Updates-Tag ein. Wenn diese Regel festgelegt wurde, kann der Netzwerkdatenverkehr an Microsoft Windows Update-Endpunkte über Ihre Firewall verlaufen.

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure Firewall](https://docs.microsoft.com/azure/firewall/overview).
- Erfahren Sie mehr über [FQDN-Tags in Azure Firewall](https://docs.microsoft.com/azure/firewall/fqdn-tags).

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Bewährte Methode: Bereitstellen einer Web Application Firewall (WAF)

Webanwendungen sind zunehmend Ziele böswilliger Angriffe, die allgemein bekannte Sicherheitslücken ausnutzen. Zu den Exploits gehören üblicherweise Angriffe durch Einschleusung von SQL-Befehlen oder Angriffe durch websiteübergreifende Skripts. Das Verhindern solcher Angriffe im Anwendungscode ist oft schwierig und erfordert strenge Wartung, Patching und Überwachung auf verschiedenen Ebenen der Anwendungstopologie. Eine zentrale Web Application Firewall vereinfacht die Sicherheitsverwaltung erheblich und ermöglicht Anwendungsadministratoren einen Schutz vor Bedrohungen und Angriffen. Mit einer Web Application Firewall können Sie schneller auf Sicherheitsrisiken reagieren, weil bekannte Schwachstellen an einem zentralen Ort gepatcht werden, statt einzelne Webanwendungen separat zu sichern. Vorhandene Anwendungsgateways lassen sich problemlos in ein Anwendungsgateway mit Web Application Firewall konvertieren.

Die Web Application Firewall (WAF) ist ein Feature von Azure Application Gateway.

- Die WAF bietet einen zentralisierten Schutz Ihrer Webanwendungen vor allgemeinen Exploits und Sicherheitsrisiken.
- Dieser Schutz wird ohne Änderung des Back-End-Codes bereitgestellt.
- Hinter einem Application Gateway können Sie mehrere Web-Apps gleichzeitig schützen.
- WAF ist in Azure Security Center integriert.
- Sie können WAF-Regeln und Regelgruppen an Ihre Anwendungsanforderungen anpassen.
- Als bewährte Methode sollten Sie eine WAF vor jeder aus dem Web zugänglichen Anwendung verwenden, einschließlich Anwendungen auf virtuellen Azure-Computern oder Azure App Service.

**Weitere Informationen**:

- Erfahren Sie mehr über die [WAF](https://docs.microsoft.com/azure/application-gateway/waf-overview).
- Informieren Sie sich über [WAF-Einschränkungen und -Ausschlüsse](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration).

## <a name="best-practice-implement-azure-network-watcher"></a>Bewährte Methode: Implementieren von Azure Network Watcher

Azure Network Watcher bietet Tools zum Überwachen von Ressourcen und Kommunikation in einem Azure-VNET. Beispielsweise können Sie die Kommunikation zwischen einem virtuellen Computer und einem Endpunkt wie z.B. einem anderen virtuellen Computer oder FQDN überwachen, Ressourcen und Ressourcenbeziehungen in einem VNET anzeigen oder Probleme mit Netzwerkdatenverkehr diagnostizieren.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
_Network Watcher_

- Mithilfe von Network Watcher können Sie Netzwerkprobleme überwachen und diagnostizieren, ohne sich bei Ihren VMs anmelden zu müssen.
- Sie können mithilfe von Warnungen die Paketerfassung auslösen und in Echtzeit Zugriff auf Leistungsinformationen auf Paketebene erhalten. Wenn Sie ein Problem feststellen, können Sie dieses detailliert untersuchen.
- Als eine bewährte Methode sollten Sie Network Watcher zum Überprüfen von NSG-Datenflussprotokollen verwenden.
  - Mit NSG-Datenflussprotokollen in Network Watcher können Sie Informationen zu ein- und ausgehendem IP-Datenverkehr über eine NSG anzeigen.
  - Datenflussprotokolle werden im JSON-Format geschrieben.
  - Die Datenflussprotokolle zeigen aus- und eingehende Datenflüsse pro Regel, die Netzwerkschnittstelle, auf die sich der Datenfluss bezieht, 5-Tupel-Informationen über den Datenfluss (Quell-/Ziel-IP-Adresse, Quell-/Zielport, Protokoll) und Informationen zu zugelassenem oder verweigertem Datenverkehr an.

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Network Watcher](https://docs.microsoft.com/azure/network-watcher).
- Erfahren Sie mehr über [NSG-Datenflussprotokolle](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview).

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Verwenden von Partnertools im Azure Marketplace

Für komplexere Netzwerktopologien können Sie Sicherheitsprodukte von Microsoft-Partnern in bestimmten virtuellen Netzwerkappliances verwenden.

- Eine virtuelle Netzwerkappliance ist ein virtueller Computer, der eine Netzwerkfunktion (Firewall, WAN-Optimierung oder Ähnliches) übernimmt.
- Durch virtuelle Netzwerkappliances werden VNET-Sicherheits- und Netzwerkfunktionen gestärkt. Sie können für hoch verfügbare Firewalls, Eindringschutz, Angriffserkennung, Web Application Firewalls (WAFs), WAN-Optimierung, Routing, Lastenausgleich, VPN, Zertifikatverwaltung, Active Directory und mehrstufige Authentifizierung bereitgestellt werden.
- Virtuelle Netzwerkappliances von zahlreichen Anbietern stehen im [Azure Marketplace](https://azuremarketplace.microsoft.com) zur Verfügung.

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Bewährte Methode: Implementieren von Firewalls und NVAs im Hubnetzwerken

Im Hub wird das Umkreisnetzwerk (mit Zugriff auf das Internet) normalerweise über eine Azure Firewall, eine Firewallfarm oder eine Web Application Firewall (WAF) verwaltet. Betrachten Sie die folgenden Vergleiche.

| Firewalltyp | Details |
| --- | --- |
| WAFs | Web-Anwendungen sind üblich und weisen häufig Sicherheitsrisiken und Exploits auf. <br><br> WAFs sind spezifischer als eine generische Firewall und auf das Erkennen von Angriffen auf Webanwendungen (HTTP/HTTPS) ausgelegt. <br><br> Verglichen mit herkömmlichen Firewalls weisen WAFs einen Satz von bestimmten Features auf, um den internen Webserver vor Bedrohungen zu schützen. |
| Azure Firewall | Wie eine Farm von Firewalls mit virtuellen Netzwerkappliances verwendet Azure Firewall einen allgemeinen Verwaltungsmechanismus und einen Satz von Sicherheitsregeln zum Schutz der in den Spoke-Netzwerken gehosteten Workloads und zum Steuern des Zugriffs auf lokale Netzwerke. <br><br> In Azure Firewall ist die Skalierbarkeit integriert. |
| Firewalls mit virtuellen Netzwerkappliances | Wie Azure Firewall verwenden Farms von Firewalls mit virtuellen Netzwerkappliances einen allgemeinen Verwaltungsmechanismus und einen Satz von Sicherheitsregeln zum Schutz der in den Spokes gehosteten Workloads und zum Steuern des Zugriffs auf lokale Netzwerke. <br><br> Firewalls mit virtuellen Netzwerkappliances können manuell hinter einem Lastenausgleich skaliert werden. <br><br> Eine Firewallfarm mit virtuellen Netzwerkappliances verfügt über weniger spezialisierte Software als ein WAF, muss aber einen umfassenderen Anwendungsbereich filtern und alle Arten von ein- oder ausgehendem Datenverkehr überprüfen. <br><br> Wenn Sie virtuelle Netzwerkappliances verwenden möchten, finden Sie diese im Azure Marketplace. |

Es wird empfohlen, eine Gruppe von Azure-Firewalls (oder virtuellen Netzwerkappliances) für Datenverkehr aus dem Internet zu verwenden und eine andere für Datenverkehr mit lokalem Ursprung.

- Die Verwendung einer einzigen Gruppe von Firewalls für den gesamten Datenverkehr stellt ein Sicherheitsrisiko dar, da sie keinen wirksamen Sicherheitsbereich zwischen den beiden Arten von Netzwerkdatenverkehr bietet.
- Separate Firewallebenen vereinfachen die Überprüfung von Sicherheitsregeln und ermöglichen eine eindeutige Zuordnung von Regeln zu eingehenden Netzwerkanforderungen.

**Weitere Informationen**:

- Erfahren Sie mehr über die [Verwendung virtueller Netzwerkappliances in einem Azure-VNET](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz).

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über weitere Best Practices:

- [Bewährte Methoden](./migrate-best-practices-security-management.md) für Sicherheit und Verwaltung nach der Migration.
- [Best Practices](./migrate-best-practices-costs.md) für die Kostenverwaltung nach der Migration.
