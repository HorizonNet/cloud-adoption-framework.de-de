---
title: Bewährte Methoden zum Einrichten von Netzwerken für zu Azure migrierte Workloads
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über bewährte Methoden (Best Practices) zum Einrichten von Netzwerken für Ihre migrierten Workloads zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ceb8fcff6417754f27d9d1c9f32469f58f88f4aa
ms.sourcegitcommit: fbfd66dab002b549d3e9cbf1b7efa0099d0b7700
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93283342"
---
<!-- cSpell:ignore NSGs CIDR FQDNs BGP's ACLs WAFs -->

# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Bewährte Methoden zum Einrichten von Netzwerken für zu Azure migrierte Workloads

Bei der Planung und dem Entwurf für die Migration besteht einer der wichtigsten Schritte neben der Migration selbst im Entwurf und in der Implementierung von Azure-Netzwerken. Dieser Artikel enthält Informationen zu bewährten Methoden für das Netzwerk bei der Migration zu IaaS-Implementierungen (Infrastructure-as-a-Service) und PaaS-Implementierungen (Platform-as-a-Service) in Azure.

> [!IMPORTANT]
> Die in diesem Artikel beschriebenen Best Practices und Meinungen basieren auf Azure-Plattform- und -Dienstfeatures, die zu dem Zeitpunkt verfügbar waren, zu dem dieser Artikel verfasst wurde. Features und Funktionen ändern sich im Laufe der Zeit. Nicht alle Empfehlungen sind notwendigerweise auf Ihre Bereitstellung anwendbar. Wählen Sie also diejenigen aus, die für Sie relevant sind.

## <a name="design-virtual-networks"></a>Entwerfen virtueller Netzwerke

Azure bietet virtuelle Netzwerke mit folgenden Funktionen:

- Über virtuelle Netzwerke können Azure-Ressourcen privat, direkt und sicher miteinander kommunizieren.
- Für virtuelle Computer und Dienste, die mit dem Internet kommunizieren müssen, können Endpunktverbindungen in virtuellen Netzwerken konfiguriert werden.
- Ein virtuelles Netzwerk ist eine logische Isolierung der dedizierten Azure-Cloud für Ihr Abonnement.
- In Azure-Abonnements und -Region können jeweils mehrere virtuelle Netzwerke implementiert werden.
- Jedes virtuelle Netzwerk wird von den anderen virtuellen Netzwerken isoliert.
- Virtuelle Netzwerke können private und öffentliche IP-Adressen enthalten, die in [RFC 1918](https://tools.ietf.org/html/rfc1918) definiert sind und in der CIDR-Notation ausgedrückt werden. Auf öffentliche IP-Adressen, die im Adressraum eines virtuellen Netzwerks angegeben wurden, kann nicht direkt über das Internet zugegriffen werden.
- Verbindungen zwischen virtuellen Netzwerken können mittels Peering virtueller Netzwerke hergestellt werden. Verbundene virtuelle Netzwerke können sich in der gleichen Region oder in unterschiedlichen Regionen befinden. Somit kann von Ressourcen in einem virtuellen Netzwerk eine Verbindung mit Ressourcen in anderen virtuellen Netzwerken hergestellt werden.
- Azure leitet Datenverkehr standardmäßig zwischen Subnetzen innerhalb eines virtuellen Netzwerks, verbundenen virtuellen Netzwerken, lokalen Netzwerken und dem Internet weiter.

Überlegen Sie sich bei der Planung Ihrer VNET-Topologie, wie Sie die IP-Adressräume anordnen, ein Hub-and-Spoke-Netzwerk implementieren, virtuelle Netzwerke in Subnetze segmentieren, DNS einrichten und Azure-Verfügbarkeitszonen implementieren möchten.

## <a name="best-practice-plan-ip-addressing"></a>Bewährte Methode: Planen der IP-Adressierung

Wenn Sie virtuelle Netzwerke im Rahmen Ihrer Migration erstellen, ist es wichtig, den IP-Adressraum der virtuellen Netzwerke zu planen.

Der für die einzelnen virtuellen Netzwerke zugewiesene Adressraum darf nicht größer sein als der CIDR-Bereich `/16`. In virtuellen Netzwerken können 65.536 IP-Adressen verwendet werden. Die Zuweisung eines kleineren Präfixes als `/16` (z. B. `/15` mit 131.072 Adressen) führt dazu, dass die überzähligen IP-Adressen nicht für andere Bereiche genutzt werden können. IP-Adressen dürfen keinesfalls verschwendet werden, selbst wenn sie sich in den durch RFC 1918 definierten privaten Bereichen befinden.

Weitere Tipps für die Planung:

- Der Adressraum virtueller Netzwerke darf sich nicht mit lokalen Netzwerkbereichen überschneiden.
- Verwenden Sie nicht die Netzwerkadressenübersetzung (Network Address Translation, NAT).
- Adressüberschneidungen können dazu führen, dass mit Netzwerken keine Verbindung hergestellt werden kann und dass das Routing nicht ordnungsgemäß funktioniert. Wenn sich Netzwerke überschneiden, muss das Netzwerk neu gestaltet oder die NAT verwendet werden.

**Weitere Informationen** :

- Lesen Sie die [Übersicht über Azure Virtual Network](/azure/virtual-network/virtual-networks-overview).
- Sehen Sie sich die [häufig gestellten Fragen zu Azure Virtual Network](/azure/virtual-network/virtual-networks-faq) an.
- Erfahren Sie mehr über [Grenzwerte für Azure-Netzwerke](/azure/azure-resource-manager/management/azure-subscription-service-limits).

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Bewährte Methode: Implementieren einer Hub-and-Spoke-Netzwerktopologie

Eine Hub-and-Spoke-Netzwerktopologie dient zur Isolation von Workloads, während Dienste wie Identität und Sicherheit gemeinsam verwendet werden. Der Hub ist ein virtuelles Azure-Netzwerk, das als zentraler Konnektivitätspunkt fungiert.
Die Spokes sind virtuelle Netzwerke, die mit dem virtuellen Hubnetzwerk unter Verwendung von Peering eine Verbindung herstellen. Gemeinsame Dienste werden im Hub bereitgestellt, während einzelne Workloads als Spokes bereitgestellt werden.

Beachten Sie Folgendes:

- Durch die Implementierung einer Hub-and-Spoke-Topologie in Azure werden allgemeine Dienste wie etwa Verbindungen mit lokalen Netzwerken, Firewalls und die Isolation zwischen virtuellen Netzwerken zentralisiert. Das virtuelle Hubnetzwerk stellt einen zentralen Konnektivitätspunkt für lokale Netzwerke und einen Ort zum Hosten von Diensten bereit, die von in virtuellen Spoke-Netzwerken gehosteten Workloads genutzt werden.
- Hub-and-Spoke-Konfigurationen kommen in der Regel in größeren Unternehmen zum Einsatz. Für kleinere Netzwerke sollte ein einfacherer Entwurf in Betracht gezogen werden, um Kosten zu sparen und die Komplexität zu verringern.
- Virtuelle Spoke-Netzwerke können zur Isolation von Workloads verwendet werden, wobei die einzelnen Spokes jeweils separat verwaltet werden. Jede Workload kann mehrere Ebenen und mehrere Subnetze umfassen, die mit Azure-Lastenausgleichsmodulen verbunden sind.
- Virtuelle Hub-and-Spoke-Netzwerke können in verschiedenen Ressourcengruppen und sogar in verschiedenen Abonnements implementiert werden. Wenn Sie eine Peerverbindung zwischen virtuellen Netzwerken in verschiedenen Abonnements herstellen, können die Abonnements demselben oder einem anderen Azure AD-Mandanten (Azure Active Directory) zugeordnet sein. Dies ermöglicht nicht nur eine dezentralisierte Verwaltung der einzelnen Workloads, sondern auch die gemeinsame Nutzung von Diensten im Hub-VNET.

![Diagramm einer Hub-and-Spoke-Topologie](./media/migrate-best-practices-networking/hub-spoke.png)
_Abbildung 1: Hub-and-Spoke-Topologie_

**Weitere Informationen** :

- Machen Sie sich mit einer [Hub-and-Spoke-Topologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) vertraut.
- Erhalten Sie Netzwerkempfehlungen für die Ausführung von [Windows-VMs](/azure/architecture/reference-architectures/n-tier/windows-vm) und [Linux-VMs](/azure/architecture/reference-architectures/n-tier/linux-vm).
- Erfahren Sie mehr zum [Peering virtueller Netzwerke](/azure/virtual-network/virtual-network-peering-overview).

## <a name="best-practice-design-subnets"></a>Bewährte Methode: Entwerfen von Subnetzen

Um innerhalb eines virtuellen Netzwerks für Isolation zu sorgen, wird es in mindestens ein Subnetz segmentiert, und jedem Subnetz wird ein Teil des Adressraums des virtuellen Netzwerks zugeordnet.

- Sie können in jedem virtuellen Netzwerk mehrere Subnetze erstellen.
- Standardmäßig leitet Azure Netzwerkdatenverkehr zwischen allen Subnetzen in einem virtuellen Netzwerk weiter.
- Ihre Subnetzentscheidungen basieren auf Ihren technischen und organisatorischen Anforderungen.
- Subnetze werden mithilfe der CIDR-Notation erstellt.

Achten Sie bei der Wahl des Netzwerkbereichs für Subnetze darauf, dass Azure aus jedem Subnetz fünf IP-Adressen zurückbehält, die nicht verwendet werden können. Wenn Sie also beispielsweise das kleinste verfügbare Subnetz `/29` (mit acht IP-Adressen) erstellen, behält Azure fünf Adressen zurück. In diesem Fall stehen somit nur drei verwendbare Adressen zur Verfügung, die Hosts im Subnetz zugewiesen werden können. In den meisten Fällen verwenden Sie `/28` als das kleinste Subnetz.

**Beispiel:**

Die Tabelle enthält ein Beispiel für ein virtuelles Netzwerk mit einem (in Subnetze segmentierten) Adressbereich von `10.245.16.0/20` für eine geplante Migration.

| Subnet | CIDR | Adressen | Verwendung |
| --- | --- | --- | --- |
| `DEV-FE-EUS2` | `10.245.16.0/22` | 1019 | Front-End- oder Webschicht-VMs |
| `DEV-APP-EUS2` | `10.245.20.0/22` | 1019 | App-Schicht-VMs |
| `DEV-DB-EUS2` | `10.245.24.0/23` | 507 | Datenbank-VMs |

**Weitere Informationen** :

- Erfahren Sie mehr über das [Entwerfen von Subnetzen](/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation).
- Erfahren Sie, wie ein fiktives Unternehmen (Contoso) [seine Netzwerkinfrastruktur für die Migration vorbereitet hat](/azure/migrate/contoso-migration-infrastructure).

## <a name="best-practice-set-up-a-dns-server"></a>Bewährte Methode: Einrichten eines DNS-Servers

Von Azure wird standardmäßig ein DNS-Server hinzugefügt, wenn Sie ein virtuelles Netzwerk bereitstellen. So können Sie schnell virtuelle Netzwerke erstellen und Ressourcen bereitstellen. Dieser DNS-Server stellt jedoch nur Dienste für die Ressourcen im jeweiligen virtuellen Netzwerk bereit. Wenn Sie mehrere virtuelle Netzwerke miteinander verbinden oder von virtuellen Netzwerken aus eine Verbindung mit einem lokalen Server herstellen möchten, benötigen Sie zusätzliche Funktionen zur Namensauflösung. Beispielsweise muss Active Directory möglicherweise DNS-Namen zwischen virtuellen Netzwerken auflösen. Zu diesem Zweck stellen Sie Ihren eigenen benutzerdefinierten DNS-Server in Azure bereit.

- DNS-Server in einem virtuellen Netzwerk können DNS-Abfragen an die rekursiven Resolver in Azure weiterleiten. Dadurch können Sie Hostnamen innerhalb dieses virtuellen Netzwerks auflösen. Beispielsweise kann ein in Azure ausgeführter Domänencontroller auf DNS-Abfragen für die eigenen Domänen antworten und alle anderen Abfragen an Azure weiterleiten.
- Durch die DNS-Weiterleitung sind sowohl Ihre lokalen Ressourcen (über den Domänencontroller) als auch die von Azure bereitgestellten Hostnamen (über die Weiterleitung) für die virtuellen Computer sichtbar. Auf die rekursiven Resolver in Azure kann über die virtuelle IP-Adresse `168.63.129.16` zugegriffen werden.
- Durch die DNS-Weiterleitung wird außerdem eine DNS-Auflösung zwischen virtuellen Netzwerken ermöglicht, sodass lokale Computer von Azure bereitgestellte Hostnamen auflösen können.
  - Um den Hostnamen eines virtuellen Computers auflösen zu können, muss sich der virtuelle DNS-Server im gleichen virtuellen Netzwerk befinden und zur Weiterleitung von Abfragen für Hostnamen an Azure konfiguriert sein.
  - Da jedes virtuelle Netzwerk ein eigenes DNS-Suffix verwendet, können Sie mithilfe von Regeln für die bedingte Weiterleitung DNS-Abfragen zur Auflösung an das richtige virtuelle Netzwerk senden.
- Wenn Sie eigene DNS-Server verwenden, können Sie für jedes virtuelle Netzwerk mehrere DNS-Server angeben. Sie können auch mehrere DNS-Server pro Netzwerkschnittstelle (für Azure Resource Manager) oder pro Clouddienst (für das klassische Bereitstellungsmodell) angeben.
- Für einen Clouddienst oder eine Netzwerkschnittstelle angegebene DNS-Server haben Vorrang vor DNS-Servern, die für das virtuelle Netzwerk angegeben wurden.
- In Azure Resource Manager können Sie DNS-Server für ein virtuelles Netzwerk und eine Netzwerkschnittstelle angeben. Es empfiehlt sich jedoch, die Einstellung nur für virtuelle Netzwerke zu verwenden.

    ![Screenshot: Hinzufügen von DNS-Servern für ein virtuelles Netzwerk](./media/migrate-best-practices-networking/dns2.png)
    _Abbildung 2: DNS-Server für ein virtuelles Netzwerk_

**Weitere Informationen** :

- Erfahren Sie mehr über die [Namensauflösung, wenn Sie einen eigenen DNS-Server verwenden](/azure/migrate/contoso-migration-infrastructure).
- Erfahren Sie mehr über [DNS-Benennungsregeln und -Einschränkungen](../../ready/azure-best-practices/naming-and-tagging.md).

## <a name="best-practice-set-up-availability-zones"></a>Bewährte Methode: Einrichten von Verfügbarkeitszonen

Verfügbarkeitszonen sorgen für höhere Verfügbarkeit, um Ihre Anwendungen und Daten vor Rechenzentrumsausfällen zu schützen. Verfügbarkeitszonen sind eindeutige physische Standorte in einer Azure-Region. Jede Zone besteht aus mindestens einem Rechenzentrum, dessen Stromversorgung, Kühlung und Netzwerkbetrieb unabhängig funktionieren. Zur Gewährleistung der Resilienz sind in allen aktivierten Regionen mindestens drei separate Zonen vorhanden. Die physische Trennung von Verfügbarkeitszonen innerhalb einer Region schützt Anwendungen und Daten vor Ausfällen von Rechenzentren.

Im Anschluss folgen einige weitere Punkte, die bei der Einrichtung von Verfügbarkeitszonen zur berücksichtigen sind:

- Zonenredundante Dienste replizieren Ihre Anwendungen und Daten in mehreren Verfügbarkeitszonen, um sie vor Single Points of Failure zu schützen.

- Mit Verfügbarkeitszonen bietet Azure eine Betriebszeit-SLA von 99,99 Prozent für virtuelle Computer.

    ![Diagramm: Verfügbarkeitszonen innerhalb einer Azure-Region](./media/migrate-best-practices-networking/availability-zone.png)

    _Abbildung 3: Verfügbarkeitszonen_

- Planen und integrieren Sie Hochverfügbarkeit in Ihre Migrationsarchitektur, indem Sie Ihre Compute-, Speicher-, Netzwerk- und Datenressourcen in eine Zone aufnehmen und in anderen Zonen replizieren. Azure-Dienste, die Verfügbarkeitszonen unterstützen, können in zwei Kategorien unterteilt werden:
  - **Zonendienste:** Sie ordnen eine Ressource einer bestimmten Zone – z B. VMs, verwalteten Datenträgern oder IP-Adressen – zu.
  - **Zonenredundante Dienste:** Die Ressource wird zonenübergreifend automatisch repliziert, z. B. zonenredundanter Speicher oder Azure SQL-Datenbank.
- Sie können eine Azure Load Balancer Standard-Instanz mit Internetworkloads oder Logikschichten bereitstellen, um für zonale Fehlertoleranz zu sorgen.

    ![Diagramm: Azure Load Balancer Standard](./media/migrate-best-practices-networking/load-balancer.png) _Abbildung 4: Lastenausgleich_

**Weitere Informationen** :

- Lesen Sie die [Übersicht über Verfügbarkeitszonen](/azure/availability-zones/az-overview).

## <a name="design-hybrid-cloud-networking"></a>Entwerfen von Hybridcloudnetzwerken

Für eine erfolgreiche Migration ist es wichtig, eine Verbindung zwischen lokalen Unternehmensnetzwerke mit Azure herzustellen. Dadurch entsteht eine Always On-Verbindung, die als Hybridcloudnetzwerk bezeichnet wird. In diesem Netzwerk werden den Unternehmensbenutzern Dienste aus der Azure-Cloud bereitgestellt. Es gibt zwei Optionen zum Erstellen dieser Art von Netzwerk:

- **Site-to-Site-VPN** : Sie erstellen eine Site-to-Site-Verbindung zwischen Ihrem kompatiblen lokalen VPN-Gerät und einem Azure-VPN-Gateway, das in einem virtuellen Netzwerk bereitgestellt wird. Jede autorisierte lokale Ressource kann auf virtuelle Netzwerke zugreifen. Die Site-to-Site-Kommunikation wird durch einen verschlüsselten Tunnel über das Internet gesendet.
- **Azure ExpressRoute:** Sie stellen eine Azure ExpressRoute-Verbindung zwischen Ihrem lokalen Netzwerk und Azure über einen ExpressRoute-Partner her. Diese Verbindung ist privat, und der Datenverkehr wird nicht über das Internet geleitet.

**Weitere Informationen** :

- Erfahren Sie mehr über [Hybridcloudnetzwerke](/azure/architecture/reference-architectures/hybrid-networking/vpn).

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Bewährte Methode: Implementieren eines hochverfügbaren Site-to-Site-VPN

Zum Implementieren eines Site-to-Site-VPN richten Sie ein VPN-Gateway in Azure ein.

- Ein VPN-Gateway ist eine spezifische Art eines Gateways für ein virtuelles Netzwerk. Es sendet verschlüsselten Datenverkehr zwischen einem virtuellen Azure-Netzwerk und einem lokalen Standort über das öffentliche Internet.
- Ein VPN-Gateway kann aber auch verschlüsselten Datenverkehr zwischen virtuellen Azure-Netzwerken über das Microsoft-Netzwerk senden.
- Ein virtuelles Netzwerk kann jeweils nur über ein einzelnes VPN-Gateway verfügen.
- Sie können mehrere Verbindungen mit dem gleichen VPN-Gateway herstellen. Wenn Sie mehrere Verbindungen herstellen, wird die für das Gateway zur Verfügung stehende Bandbreite auf alle VPN-Tunnel aufgeteilt.

Jedes Azure-VPN-Gateway umfasst zwei Instanzen in einer Aktiv-Standby-Konfiguration:

- Bei geplanten Wartungsarbeiten oder ungeplanten Störungen für die aktive Instanz findet ein Failover statt, und es wird automatisch die Standbyinstanz verwendet. Diese Instanz nimmt die Site-to-Site- oder Netzwerk-zu-Netzwerk-Verbindung wieder auf.
- Der Wechsel verursacht eine kurze Unterbrechung.
- Bei der geplanten Wartung sollte die Konnektivität innerhalb von 10 bis 15 Sekunden wiederhergestellt werden.
- Bei ungeplanten Problemen dauert die Verbindungswiederherstellung länger – schlimmstenfalls bis zu anderthalb Minuten.
- Point-to-Site-VPN-Clientverbindungen mit dem Gateway werden getrennt, und Benutzer müssen von Clientcomputern aus erneut eine Verbindung herstellen.

Beim Einrichten eines Site-to-Site-VPN gilt Folgendes:

- Sie benötigen ein virtuelles Netzwerk, dessen Adressraum sich nicht mit dem lokalen Netzwerk überschneidet, mit dem das VPN eine Verbindung herstellen soll.
- Sie erstellen ein Gatewaysubnetz im Netzwerk.
- Sie erstellen ein VPN-Gateway, geben den Gatewaytyp (VPN) an und legen fest, ob es sich um ein richtlinienbasiertes oder um ein routenbasiertes Gateway handelt. Ein routenbasiertes VPN wird als leistungsstärker und zukunftssicherer angesehen.
- Sie erstellen ein lokales Netzwerkgateway und konfigurieren Ihr lokales VPN-Gerät.
- Sie erstellen eine Site-to-Site-VPN-Failoververbindung zwischen dem Gateway für virtuelle Netzwerke und dem lokalen Gerät. Die Verwendung eines routenbasierten VPN ermöglicht Aktiv/Passiv- oder Aktiv/Aktiv-Verbindungen mit Azure. Bei der routenbasierten Option werden parallel sowohl Site-to-Site-Verbindungen (von einem beliebigen Computer aus) als auch Point-to-Site-Verbindungen (von einem einzelnen Computer aus) unterstützt.
- Sie geben die gewünschte Gateway-SKU aus. Diese hängt von Ihren Workloadanforderungen, von Ihrem Durchsatz, von Ihren Features und von Ihren SLAs ab.
- Das Border Gateway Protocol (BGP) ist ein optionales Feature. Es kann mit Azure ExpressRoute und routenbasierten VPN-Gateways verwendet werden, um Ihre lokalen BGP-Routen auf Ihre virtuellen Netzwerke zu verteilen.

![Diagramm: Site-to-Site-VPN](./media/migrate-best-practices-networking/vpn.png)
_Abbildung 5: Site-to-Site-VPN_

**Weitere Informationen** :

- Informieren Sie sich über [kompatible lokale VPN-Geräte](/azure/vpn-gateway/vpn-gateway-about-vpn-devices).
- Lesen Sie die [Übersicht über Azure-VPN-Gateways](/azure/vpn-gateway/vpn-gateway-about-vpngateways).
- Erhalten Sie Informationen zu [hochverfügbaren VPN-Verbindungen](/azure/vpn-gateway/vpn-gateway-highlyavailable).
- Erfahren Sie mehr über das [Planen und Entwerfen eines VPN-Gateways](/azure/vpn-gateway/vpn-gateway-plan-design).
- Informieren Sie sich über [VPN-Gatewayeinstellungen](/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku).
- Informieren Sie sich über [Gateway-SKUs](/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku).
- Informieren Sie sich über das [Einrichten des BGP mit Azure-VPN-Gateways](/azure/vpn-gateway/vpn-gateway-bgp-overview).

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Bewährte Methode: Konfigurieren eines Gateways für VPN-Gateways

Wenn Sie ein VPN-Gateway in Azure erstellen, müssen Sie ein spezielles Subnetz namens `GatewaySubnet` verwenden. Berücksichtigen Sie beim Erstellen dieses Subnetzes die folgenden bewährten Methoden:

- `GatewaySubnet` kann eine maximale Präfixlänge von 29 aufweisen (z. B. `10.119.255.248/29`). Aktuell wird empfohlen, eine Präfixlänge von 27 zu verwenden (z. B. `10.119.255.224/27`).
- Wenn Sie den Adressraum des Gatewaysubnetzes definieren, verwenden Sie den letzten Teil des Adressraums des virtuellen Netzwerks.
- Stellen Sie bei Verwendung des Azure-Gatewaysubnetzes keine virtuellen Computer oder anderen Geräte (beispielsweise Azure Application Gateway) im Gatewaysubnetz bereit.
- Weisen Sie diesem Subnetz keine Netzwerksicherheitsgruppe (NSG) zu. Dadurch würde die Funktion des Gateways beendet.

**Weitere Informationen** :

- [Verwenden Sie dieses Tool](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed), um Ihren IP-Adressraum zu ermitteln.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Bewährte Methode: Implementieren von Azure Virtual WAN für Filialen

Bei Verwendung mehrerer VPN-Verbindungen bietet der Azure Virtual WAN-Netzwerkdienst optimierte und automatisierte Konnektivität zwischen Filialen über Azure.

- Per Virtual WAN können Sie Filialgeräte für die Kommunikation mit Azure verbinden und konfigurieren. Dies ist manuell oder durch die Nutzung von Geräten eines bevorzugten Anbieters über einen Azure Virtual WAN-Partner möglich.
- Die Nutzung von Geräten eines bevorzugten Anbieters ermöglicht eine einfache Verwendung, Konnektivität und Konfigurationsverwaltung.
- Im integrierten Azure Virtual WAN-Dashboard können Sie umgehend Erkenntnisse zur Problembehandlung gewinnen, um Zeit zu sparen. Zudem können Sie auf einfache Weise umfangreiche Site-to-Site-Verbindungen überwachen.

**Weitere Informationen** : Erfahren Sie mehr über [Azure Virtual WAN](/azure/virtual-wan/virtual-wan-about).

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Bewährte Methode: Implementieren von ExpressRoute für unternehmenskritische Verbindungen

Mit dem Azure ExpressRoute-Dienst erweitern Sie Ihre lokale Infrastruktur in die Microsoft-Cloud, indem Sie private Verbindungen zwischen dem virtuellen Azure-Rechenzentrum und lokalen Netzwerken erstellen. Im Anschluss folgen einige Implementierungsdetails:

- ExpressRoute-Verbindungen können über ein IP-VPN-Netzwerk (Any-to-Any), ein Point-to-Point-Ethernet-Netzwerk oder über einen Konnektivitätsanbieter hergestellt werden. Sie verlaufen nicht über das öffentliche Internet.
- ExpressRoute-Verbindungen bieten bei gleichbleibenden Wartezeiten mehr Sicherheit und Zuverlässigkeit sowie höhere Geschwindigkeiten (bis zu 10 GBit/s).
- ExpressRoute ist nützlich für virtuelle Rechenzentren, weil Kunden von den Konformitätsregeln privater Verbindungen profitieren.
- Mit ExpressRoute Direct können Sie bei höherem Bandbreitenbedarf eine direkte 100 GBit/s-Verbindung mit Microsoft-Routern herstellen.
- ExpressRoute verwendet BGP zum Austauschen von Routen zwischen lokalen Netzwerken, Azure-Instanzen und öffentlichen Microsoft-Adressen.

Für die Bereitstellung von ExpressRoute-Verbindungen ist in der Regel ein ExpressRoute-Dienstanbieter erforderlich. Zum schnellen Einstieg wird zunächst üblicherweise eine Site-to-Site-VPN-Verbindung verwendet, um eine Verbindung zwischen dem virtuellen Rechenzentrum und lokalen Ressourcen herzustellen. Danach wird dann eine Migration zu einer ExpressRoute-Verbindung durchgeführt, wenn eine physische Verbindung mit Ihrem Dienstanbieter eingerichtet wurde.

**Weitere Informationen** :

- Sehen Sie sich eine [Übersicht](/azure/expressroute/expressroute-introduction) über ExpressRoute an.
- Informieren Sie sich über [ExpressRoute Direct](/azure/expressroute/expressroute-erdirect-about).

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Bewährte Methode: Optimieren von ExpressRoute-Routing mit BGP-Communitys

Wenn Sie mehrere ExpressRoute-Verbindungen nutzen, verfügen Sie über mehr als einen Weg zur Herstellung einer Verbindung mit Microsoft. Dies kann ein suboptimales Routing zur Folge haben, und Ihr Datenverkehr verwendet möglicherweise einen längeren Pfad zu Microsoft bzw. von Microsoft zu Ihrem Netzwerk. Je länger der Netzwerkpfad, desto höher die Latenz. Wartezeit wirkt sich direkt auf die Anwendungsleistung und die Benutzerfreundlichkeit aus.

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
  - Ihr WAN geht möglicherweise davon aus, dass beide Präfixe näher bei `East US` als bei `West US` liegen, und leitet daher Benutzer aus beiden Niederlassungen an die ExpressRoute-Leitung in `East US` weiter. Dadurch wird für Benutzer in der Niederlassung in Los Angeles eine schlechtere Leistung erzielt.

![Diagramm: VPN mit Routenpfad über die falsche Leitung](./media/migrate-best-practices-networking/bgp1.png)
_Abbildung 6: Nicht optimierte Verbindung über BGP-Communitys_

**Lösung:**

Um das Routing für beide Niederlassungen optimieren zu können, müssen Sie wissen, welches Präfix für die Azure-Region `West US` und welches Präfix für die Azure-Region `East US` gilt. Sie können diese Informationen mithilfe von BGP-Communitywerten codieren.

- Sie weisen jeder Azure-Region einen eindeutigen BGP-Communitywert zu. Beispiel: 12076:51004 für `East US` und 12076:51006 für `West US`.
- Damit ist klar, welches Präfix zu welcher Azure-Region gehört, sodass Sie eine bevorzugte ExpressRoute-Leitung konfigurieren können.
- Da Sie BGP zum Austauschen von Routinginformationen verwenden, können Sie über die lokale Einstellung von BGP das Routing beeinflussen.
- Im vorliegenden Beispiel weisen Sie `13.100.0.0/16` in `West US` einen höheren Wert für die lokale Einstellung zu als für `East US`. Analog dazu weisen Sie `23.100.0.0/16` in `East US` einen höheren Wert für die lokale Einstellung zu als für `West US`.
- Diese Konfiguration stellt bei Verfügbarkeit beider Pfade zu Microsoft sicher, dass Benutzer in Los Angeles über die westliche Leitung eine Verbindung mit der Region `West US` herstellen und Benutzer in New York über die östliche Leitung eine Verbindung mit der Region `East US`.

![Diagramm: VPN mit Routenpfad über die korrekte Leitung](./media/migrate-best-practices-networking/bgp2.png)
_Abbildung 7: Optimierte Verbindung über BGP-Communitys_

**Weitere Informationen** :

- Erfahren Sie mehr über das [Optimieren des Routings](/azure/expressroute/expressroute-optimize-routing).

## <a name="secure-virtual-networks"></a>Sichere virtuelle Netzwerke

Die Verantwortung für den Schutz virtueller Netzwerke liegt zu gleichen Teilen bei Microsoft und bei Ihnen. Microsoft bietet viele Netzwerkfeatures und Dienste, die zum Schutz der Ressourcen dienen. Bei der Gestaltung der Sicherheit für virtuelle Netzwerke empfiehlt es sich, ein Umkreisnetzwerk zu implementieren, Filter und Sicherheitsgruppen zu verwenden, den Zugriff auf Ressourcen und IP-Adressen zu schützen sowie einen Angriffsschutz zu implementieren.

**Weitere Informationen** :

- Lesen Sie eine [Übersicht über bewährte Methoden für die Netzwerksicherheit](/azure/security/fundamentals/network-best-practices).
- Erfahren Sie mehr über das [Entwerfen sicherer Netzwerke](/azure/virtual-network/virtual-network-vnet-plan-design-arm#security).

<!-- docutune:casing "IDS/IPS" -->

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Bewährte Methode: Implementieren eines Azure-Umkreisnetzwerks

Wenngleich Microsoft hohe Investitionen in den Schutz der Cloudinfrastruktur tätigt, müssen Sie ebenfalls für den Schutz Ihrer Clouddienste und Ressourcengruppen sorgen. Ein mehrstufiger Sicherheitsansatz bietet die beste Absicherung. Die Einrichtung eines Umkreisnetzwerks ist ein wichtiger Bestandteil dieser Schutzstrategie.

- Ein Umkreisnetzwerk schützt die internen Netzwerkressourcen vor einem nicht vertrauenswürdigen Netzwerk.
- Dabei handelt es sich um die äußerste Schicht, die mit dem Internet verbunden ist. Sie befindet sich normalerweise zwischen dem Internet und der Infrastruktur des Unternehmens, in der Regel mit irgendeiner Art des Schutzes auf beiden Seiten.
- In einer typischen Unternehmensnetzwerktopologie wird der Kern der Infrastruktur im Umkreisnetzwerk durch mehrere Stufen von Sicherheitsgeräten stark geschützt. An den Grenzen der einzelnen Stufen befinden sich Sicherheitsgeräte und Stellen zur Durchsetzung von Richtlinien.
- Die einzelnen Stufen können jeweils eine Kombination der Netzwerksicherheitslösungen enthalten. Hierzu zählen beispielsweise Firewalls, DoS-Schutz (Denial of Service), IDS/IPS (Intrusion Detection System/Intrusion Protection System) und VPN-Geräte.
- Die Durchsetzung von Richtlinien im Umkreisnetzwerk kann über Firewallrichtlinien, Zugriffssteuerungslisten (Access Control Lists, ACLs) oder ein spezifisches Routing erfolgen.
- Eingehender Internetdatenverkehr wird abgefangen und durchläuft eine Kombination von Abwehrlösungen. Durch die Lösungen werden Angriffe und schädlicher Datenverkehr blockiert und legitime Netzwerkanforderungen zugelassen.
- Der eingehende Datenverkehr kann direkt an Ressourcen im Umkreisnetzwerk weitergeleitet werden. Die Umkreisnetzwerkressource kann dann mit anderen, tiefer im Netzwerk befindlichen Ressourcen kommunizieren und den Datenverkehr nach der Überprüfung an das Netzwerk weiterleiten.

Hier sehen Sie ein Beispiel für ein Umkreisnetzwerk mit einem einzelnen Subnetz in einem Unternehmensnetzwerk und mit zwei Sicherheitsgrenzen:

![Diagramm: Bereitstellung eines Azure Virtual Network-Umkreisnetzwerks](./media/migrate-best-practices-networking/perimeter.png)
_Abbildung 8: Bereitstellung eines Umkreisnetzwerks_

**Weitere Informationen** :

- Erfahren Sie mehr über die [Bereitstellung eines Umkreisnetzwerks zwischen Azure und Ihrem lokalen Rechenzentrum](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz).

## <a name="best-practice-filter-virtual-network-traffic-with-nsgs"></a>Bewährte Methode: Filtern des Datenverkehrs virtueller Netzwerke mit NSGs

Netzwerksicherheitsgruppen (NSG) enthalten mehrere Ein- und Ausgangssicherheitsregeln zum Filtern des Datenverkehrs, der bei Ressourcen ein- bzw. von ihnen ausgeht. Das Filtern kann nach Quell- und Ziel-IP-Adresse, Port und Protokoll erfolgen.

- NSGs enthalten Sicherheitsregeln, die eingehenden Netzwerkdatenverkehr an verschiedene Typen von Azure-Ressourcen (bzw. von ihnen ausgehenden Netzwerkdatenverkehr) zulassen oder verweigern. Für jede Regel können Sie die Quelle, das Ziel, den Port und das Protokoll angeben.
- NSG-Regeln werden nach Priorität anhand der 5-Tupel-Informationen (Quelle, Quellport, Ziel, Zielport und Protokoll) ausgewertet, um den Datenverkehr zuzulassen oder zu verweigern.
- Für vorhandene Verbindungen wird ein Flussdatensatz erstellt. Die Kommunikation wird basierend auf dem Verbindungszustand der Flussdatensätze zugelassen oder verweigert.
- Durch einen Datenflussdatensatz kann eine NSG zustandsbehaftet sein. Wenn Sie beispielsweise eine Sicherheitsregel für ausgehenden Datenverkehr an eine beliebige Adresse über Port 80 angeben, ist es nicht erforderlich, für die Antwort auf den ausgehenden Datenverkehr eine Sicherheitsregel für eingehenden Datenverkehr anzugeben. Sie müssen nur dann eine Sicherheitsregel für Datenverkehr in eingehender Richtung angeben, wenn die Kommunikation extern initiiert wird.
- Dies gilt auch für den umgekehrten Fall. Wenn eingehender Datenverkehr über einen Port zugelassen wird, ist es nicht erforderlich, für die Beantwortung des Datenverkehrs über den Port eine Sicherheitsregel für ausgehenden Datenverkehr anzugeben.
- Vorhandene Verbindungen werden nicht unterbrochen, wenn Sie eine Sicherheitsregel entfernen, die den Datenfluss ermöglicht hat. Datenverkehrsflüsse werden unterbrochen, wenn Verbindungen beendet werden und in beide Richtungen mindestens einige Minuten lang kein Datenverkehr besteht.
- Erstellen Sie immer so wenige NSGs wie möglich, aber so viele wie nötig.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Bewährte Methode: Schützen von Datenverkehr in Nord-Süd- und Ost-West-Richtung

Beim Schutz virtueller Netzwerke müssen Angriffsvektoren berücksichtigt werden. Beachten Sie folgende Punkte:

- Durch die ausschließliche Verwendung von Subnetz-NSGs wird Ihre Umgebung vereinfacht, aber nur der Datenverkehr in Ihr Subnetz abgesichert. Dies wird als Nord-Süd-Datenverkehr bezeichnet.
- Der Datenverkehr zwischen virtuellen Computern im selben Subnetz wird Ost-West-Datenverkehr genannt.
- Sie sollten unbedingt beide Schutzformen nutzen, sodass ein Hacker, der von außen Zugriff erlangt, gestoppt wird, wenn er versucht, auf Computer im gleichen Subnetz zuzugreifen.

### <a name="use-service-tags-on-nsgs"></a>Verwenden von Diensttags für NSGs

Ein Diensttag steht für eine Gruppe von IP-Adresspräfixen. Durch Verwendung eines Diensttags ist die Erstellung von NSG-Regeln weniger komplex.

- Bei der Erstellung von Regeln können Sie Diensttags anstelle spezifischer IP-Adressen nutzen.
- Microsoft verwaltet die Adresspräfixe, die einem Diensttag zugeordnet sind, und aktualisiert das Diensttag automatisch, wenn sich die Adressen ändern.
- Sie können kein eigenes Diensttag erstellen und auch nicht angeben, welche IP-Adressen in einem Tag enthalten sind.

Diensttags ersparen Ihnen die manuelle Arbeit beim Zuweisen einer Regel zu Gruppen von Azure-Diensten. Wenn Sie beispielsweise einem Subnetz mit Webservern den Zugriff auf Azure SQL-Datenbank ermöglichen möchten, können Sie eine Ausgangsregel für Port 1433 erstellen und das Diensttag **Sql** verwenden.

- Dieses **Sql** -Tag gibt die Adresspräfixe der Azure SQL-Datenbank- und Azure SQL Data Warehouse-Dienste an.
- Wenn Sie **Sql** als Wert angeben, wird der Datenverkehr für SQL zugelassen oder verweigert.
- Falls Sie den Zugriff auf **Sql** nur für eine bestimmte Region zulassen möchten, können Sie die betreffende Region angeben. Wenn Sie den Zugriff auf Azure SQL-Datenbank beispielsweise nur für die Region „USA, Osten“ zulassen möchten, können Sie **Sql.EastUS** für das Diensttag angeben.
- Das Tag steht für den Dienst, aber nicht für bestimmte Instanzen des Diensts. Beispielsweise steht das Tag für den Azure SQL-Datenbank-Dienst, aber nicht für eine bestimmte SQL-Datenbank oder einen bestimmten SQL-Server.
- Alle Adresspräfixe, für die dieses Tag steht, werden auch durch das **Internet** -Tag repräsentiert.

**Weitere Informationen** :

- Lesen Sie Informationen zu [Netzwerksicherheitsgruppen (NSGs)](/azure/virtual-network/security-overview).
- Informieren Sie sich über [die für NSGs verfügbaren Diensttags](/azure/virtual-network/security-overview#service-tags).

## <a name="best-practice-use-application-security-groups"></a>Bewährte Methode: Verwenden von Anwendungssicherheitsgruppen

Mit Anwendungssicherheitsgruppen können Sie die Netzwerksicherheit als natürliche Erweiterung einer Anwendungsstruktur konfigurieren.

- Anhand von Anwendungssicherheitsgruppen können Sie virtuelle Computer gruppieren und Netzwerksicherheitsrichtlinien definieren.
- Anwendungssicherheitsgruppen ermöglichen die bedarfsabhängige Wiederverwendung Ihrer Sicherheitsrichtlinie, ohne explizite IP-Adressen manuell warten zu müssen.
- Anwendungssicherheitsgruppen übernehmen die komplexe Verarbeitung expliziter IP-Adressen und mehrerer Regelsätze, damit Sie sich auf Ihre Geschäftslogik konzentrieren können.

**Beispiel:**

![Diagramm: Anwendungssicherheitsgruppe](./media/migrate-best-practices-networking/asg.png)
_Abbildung 9: Beispiel für eine Anwendungssicherheitsgruppe_

| Netzwerkschnittstelle | Anwendungssicherheitsgruppe |
| --- | --- |
| `NIC1` | `AsgWeb` |
| `NIC2` | `AsgWeb` |
| `NIC3` | `AsgLogic` |
| `NIC4` | `AsgDb` |

In unserem Beispiel gehört jede Netzwerkschnittstelle nur einer Anwendungssicherheitsgruppe an, aber tatsächlich kann eine Schnittstelle mehreren Gruppen angehören (in Übereinstimmung mit der Azure-Grenzwerten). Keiner der Netzwerkschnittstellen ist eine NSG zugeordnet. `NSG1` ist beiden Subnetzen zugeordnet und enthält die folgenden Regeln:

| Regelname | Zweck | Details |
| --- | --- | --- |
| `Allow-HTTP-Inbound-Internet` | Hiermit wird Datenverkehr aus dem Internet an die Webserver zugelassen. Eingehender Datenverkehr aus dem Internet wird durch die Standardsicherheitsregel `DenyAllInbound` verweigert, daher ist keine zusätzliche Regel für die Anwendungssicherheitsgruppen `AsgLogic` oder `AsgDb` erforderlich. | Priorität: `100`<br><br> Quelle: `internet` <br><br> Quellport: `*` <br><br> Ziel: `AsgWeb` <br><br> Zielport: `80` <br><br> Protokoll: `TCP` <br><br> Zugriff: `Allow` |
| `Deny-Database-All` | Die Standardsicherheitsregel `AllowVNetInBound` erlaubt die gesamte Kommunikation zwischen Ressourcen im gleichen virtuellen Netzwerk. Diese Regel wird benötigt, um den Datenverkehr von allen Ressourcen zu verweigern. | Priorität: `120` <br><br> Quelle: `*` <br><br> Quellport: `*` <br><br> Ziel: `AsgDb` <br><br> Zielport: `1433` <br><br> Protokoll: `All` <br><br> Zugriff: `Deny` |
| `Allow-Database-BusinessLogic` | Diese Regel lässt Datenverkehr von der Anwendungssicherheitsgruppe `AsgLogic` an die Anwendungssicherheitsgruppe `AsgDb` zu. Da die Priorität für diese Regel höher ist als die Priorität der Regel `Deny-Database-All`, wird diese Regel zuerst verarbeitet. Dies führt dazu, dass Datenverkehr von der Anwendungssicherheitsgruppe `AsgLogic` zugelassen und jeglicher andere Datenverkehr blockiert wird. | Priorität: `110` <br><br> Quelle: `AsgLogic` <br><br> Quellport: `*` <br><br> Ziel: `AsgDb` <br><br> Zielport: `1433` <br><br> Protokoll: `TCP` <br><br> Zugriff: `Allow` |

Regeln, in denen eine Anwendungssicherheitsgruppe als Quelle oder Ziel angegeben ist, werden nur auf Netzwerkschnittstellen angewendet, bei denen es sich um Mitglieder der Anwendungssicherheitsgruppe handelt. Wenn die Netzwerkschnittstelle keiner Anwendungssicherheitsgruppe angehört, wird die Regel nicht auf die Netzwerkschnittstelle angewendet, auch wenn die Netzwerksicherheitsgruppe dem Subnetz zugeordnet ist.

**Weitere Informationen** :

- Informieren Sie sich über [Anwendungssicherheitsgruppen](/azure/virtual-network/security-overview#application-security-groups).

### <a name="best-practice-secure-access-to-paas-by-using-virtual-network-service-endpoints"></a>Bewährte Methode: Sicheres Zugreifen auf PaaS unter Verwendung von VNET-Dienstendpunkten

Durch VNET-Dienstendpunkte werden Ihr privater VNET-Adressraum und die Identität über eine direkte Verbindung auf Azure-Dienste erweitert.

- Endpunkte ermöglichen es Ihnen, kritische Ressourcen von Azure-Diensten auf Ihre virtuellen Netzwerke zu beschränken und so zu schützen. Der Datenverkehr aus Ihrem virtuellen Netzwerk an den Azure-Dienst wird vollständig über das Backbone-Netzwerk von Azure abgewickelt.
- Der private VNET-Adressraum kann sich überschneiden und daher nicht zur eindeutigen Identifizierung von Datenverkehr aus einem virtuellen Netzwerk verwendet werden.
- Nach der Aktivierung von Dienstendpunkten in Ihrem virtuellen Netzwerk können Sie Azure-Dienstressourcen schützen, indem Sie ihnen eine VNET-Regel hinzufügen. Dadurch erhöht sich die Sicherheit, da der Ressourcenzugriff über das öffentliche Internet vollständig verhindert und nur Datenverkehr aus Ihrem virtuellen Netzwerk zugelassen wird.

![Diagramm: Dienstendpunkte](./media/migrate-best-practices-networking/endpoint.png)
_Abbildung 10: Dienstendpunkte_

**Weitere Informationen** :

- Informieren Sie sich über [VNET-Dienstendpunkte](/azure/virtual-network/virtual-network-service-endpoints-overview).

## <a name="best-practice-control-public-ip-addresses"></a>Bewährte Methode: Steuern öffentlicher IP-Adressen

Öffentliche IP-Adressen in Azure können virtuellen Computern, Lastenausgleichsmodulen, Application Gateways und VPN-Gateways zugeordnet werden.

- Anhand öffentlicher IP-Adressen können Internetressourcen in eingehender Richtung mit Azure-Ressourcen und Azure-Ressourcen in ausgehender Richtung mit dem Internet kommunizieren.
- Öffentliche IP-Adressen werden mit einer „Basic“- oder „Standard“-SKU erstellt, bei denen es mehrere Unterschiede gibt. Standard-SKUs können jedem Dienst zugewiesen werden, werden jedoch meistens für virtuelle Computer, Lastenausgleichsmodule und Application Gateways konfiguriert.
- Es ist wichtig zu beachten, dass für eine öffentliche IP-Adresse der SKU „Basic“ nicht automatisch eine NSG konfiguriert wird. Sie müssen eine eigene NSG konfigurieren und Regeln zum Steuern des Zugriffs zuweisen. IP-Adressen der SKU „Standard“ umfassen eine Netzwerksicherheitsgruppe und standardmäßig zugewiesene Regeln.
- Als bewährte Methode dürfen VMs nicht mit einer öffentlichen IP-Adresse konfiguriert werden.
  - Wenn Sie einen geöffneten Port benötigen, sollte dieser nur für Webdienste geöffnet werden (beispielsweise Port 80 oder 443).
  - Standard-Remoteverwaltungsports wie SSH (22) und RDP (3389) sollten wie alle übrigen Ports mithilfe von NSGs auf „Verweigern“ festgelegt werden.
- Eine bessere Methode besteht darin, virtuelle Computer hinter Azure Load Balancer oder Azure Application Gateway zu platzieren. Wenn anschließend Zugriff auf Remoteverwaltungsports benötigt wird, können Sie Just-In-Time-VM-Zugriff im Azure Security Center verwenden.

**Weitere Informationen** :

- [Öffentliche IP-Adressen in Azure](/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses)
- [Verwalten des Zugriffs auf virtuelle Computer mithilfe des Just-In-Time-Features](/azure/security-center/security-center-just-in-time)

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Nutzen von Azure-Sicherheitsfeatures für Netzwerke

Azure verfügt über Sicherheitsfeatures auf Plattformebene wie Azure Firewall, Web Application Firewall und Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Bewährte Methode: Bereitstellen von Azure Firewall

Azure Firewall ist ein verwalteter, cloudbasierter Netzwerksicherheitsdienst, der zum Schutz Ihrer VNET-Ressourcen beiträgt. Es handelt sich hierbei um eine vollständig zustandsbehaftete verwaltete Firewall mit integrierter Hochverfügbarkeit und uneingeschränkter Cloudskalierbarkeit.

![Diagramm: Azure Firewall](./media/migrate-best-practices-networking/firewall.png)
_Abbildung 11: Azure Firewall_

Im Anschluss folgen einige Punkte, die beachtet werden müssen, wenn Sie den Dienst bereitstellen:

- Von Azure Firewall können Richtlinien zur Anwendungs- und Netzwerkkonnektivität für Abonnements und virtuelle Netzwerke zentral erstellt, erzwungen und protokolliert werden.
- Azure Firewall verwendet eine statische öffentliche IP-Adresse für Ihre virtuellen Netzwerkressourcen. Dadurch können externe Firewalls Datenverkehr aus Ihrem virtuellen Netzwerk identifizieren.
- Azure Firewall ist für Protokollierung und Analyse vollständig in Azure Monitor integriert.
- Beim Erstellen von Azure Firewall-Regeln empfiehlt sich die Verwendung der FQDN-Tags.
  - Ein FQDN-Tag stellt eine Gruppe von FQDNs dar, die bekannten Microsoft-Diensten zugeordnet sind.
  - Sie können ein FQDN-Tag verwenden, um den erforderlichen ausgehenden Netzwerkdatenverkehr über die Firewall zuzulassen.
- Um beispielsweise den Netzwerkdatenverkehr von Windows Update manuell über Ihre Firewall zuzulassen, müssen Sie mehrere Anwendungsregeln erstellen. Mit FQDN-Tags erstellen Sie eine Anwendungsregel und schließen das Windows Update-Tag ein. Wenn diese Regel festgelegt wurde, kann der Netzwerkdatenverkehr an Microsoft Windows Update-Endpunkte über Ihre Firewall verlaufen.

**Weitere Informationen** :

- Lesen Sie die [Übersicht über Azure Firewall](/azure/firewall/overview).
- Erfahren Sie mehr über [FQDN-Tags in Azure Firewall](/azure/firewall/fqdn-tags).

## <a name="best-practice-deploy-web-application-firewall"></a>Bewährte Methode: Bereitstellen der Web Application Firewall

Webanwendungen sind zunehmend Ziele böswilliger Angriffe, die allgemein bekannte Sicherheitslücken ausnutzen. Zu den Exploits gehören üblicherweise Angriffe durch Einschleusung von SQL-Befehlen oder Angriffe durch websiteübergreifende Skripts. Die Verhinderung solcher Angriffe im Anwendungscode ist oft schwierig und erfordert strikte Wartungs-, Patching- und Überwachungsmaßnahmen auf verschiedenen Ebenen der Anwendungstopologie.

Die Web Application Firewall (WAF) ist ein Feature von Azure Application Gateway, das die Sicherheitsverwaltung erheblich vereinfacht und Anwendungsadministratoren bei Maßnahmen zum Schutz vor Bedrohungen und Angriffen unterstützt. Sie können schneller auf Sicherheitsrisiken reagieren, da bekannte Schwachstellen an einem zentralen Ort gepatcht werden, anstatt einzelne Webanwendungen separat zu schützen. Bereits vorhandene Anwendungsgateways lassen sich problemlos in eine Web Application Firewall-fähige Application Gateway-Instanz konvertieren.

Im Anschluss folgen einige zusätzliche Hinweise zur WAF:

- Die WAF bietet zentralisierten Schutz Ihrer Webanwendungen vor allgemeinen Exploits und Sicherheitsrisiken.
- Sie müssen keine Codeänderungen vornehmen, um die WAF verwenden zu können.
- Sie kann gleichzeitig mehrere Web-Apps schützen (hinter Application Gateway).
- WAF ist in Azure Security Center integriert.
- Sie können WAF-Regeln und Regelgruppen an Ihre Anwendungsanforderungen anpassen.
- Es empfiehlt sich, eine WAF vor jeder Anwendung zu verwenden, auf die über das Web zugegriffen werden kann. Dies gilt auch für Anwendungen auf virtuellen Azure-Computern oder in Azure App Service.

**Weitere Informationen** :

- Erfahren Sie mehr über die [WAF](/azure/application-gateway/waf-overview).
- Informieren Sie sich über [WAF-Einschränkungen und -Ausschlüsse](/azure/application-gateway/application-gateway-waf-configuration).

## <a name="best-practice-implement-azure-network-watcher"></a>Bewährte Methode: Implementieren von Azure Network Watcher

Azure Network Watcher bietet Tools zur Überwachung von Ressourcen und der Kommunikation in einem virtuellen Azure-Netzwerk. So können Sie beispielsweise die Kommunikation zwischen einem virtuellen Computer und einem Endpunkt (beispielsweise einem anderen virtuellen Computer oder FQDN) überwachen. Darüber hinaus können Sie Ressourcen und Ressourcenbeziehungen in einem virtuellen Netzwerk anzeigen oder Probleme mit Netzwerkdatenverkehr diagnostizieren.

![Screenshot: Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
_Abbildung 12: Network Watcher_

Im Anschluss finden Sie einige weitere Details:

- Mithilfe von Network Watcher können Sie Netzwerkprobleme überwachen und diagnostizieren, ohne sich bei virtuellen Computern anzumelden.
- Sie können mithilfe von Warnungen die Paketerfassung auslösen und in Echtzeit Zugriff auf Leistungsinformationen auf Paketebene erhalten. Wenn Sie ein Problem feststellen, können Sie dieses detailliert untersuchen.
- Als eine bewährte Methode sollten Sie Network Watcher zum Überprüfen von NSG-Datenflussprotokollen verwenden.
  - Mit NSG-Datenflussprotokollen in Network Watcher können Sie Informationen zu ein- und ausgehendem IP-Datenverkehr über eine NSG anzeigen.
  - Datenflussprotokolle werden im JSON-Format geschrieben.
  - Datenflussprotokolle geben Aufschluss über regelspezifische aus- und eingehende Datenflüsse sowie über die Netzwerkschnittstelle (NIC) für den Datenfluss. Des Weiteren enthalten sie 5-Tupel-Informationen zum Datenfluss (Quell-/Ziel-IP-Adresse, Quell-/Zielport, Protokoll) sowie Informationen dazu, ob der Datenverkehr zugelassen oder verweigert wurde.

**Weitere Informationen** :

- Lesen Sie die [Übersicht über Network Watcher](/azure/network-watcher).
- Erfahren Sie mehr über [NSG-Datenflussprotokolle](/azure/network-watcher/network-watcher-nsg-flow-logging-overview).

## <a name="use-partner-tools-in-azure-marketplace"></a>Verwenden von Partnertools im Azure Marketplace

Für komplexere Netzwerktopologien können Sie Sicherheitsprodukte von Microsoft-Partnern in bestimmten virtuellen Netzwerkappliances verwenden.

- Eine virtuelle Netzwerkappliance ist ein virtueller Computer, der eine Netzwerkfunktion (Firewall, WAN-Optimierung oder Ähnliches) übernimmt.
- Durch virtuelle Netzwerkappliances werden VNET-Sicherheits- und Netzwerkfunktionen gestärkt. Sie können für hoch verfügbare Firewalls, Eindringschutz, Angriffserkennung, WAFs, WAN-Optimierung, Routing, Lastenausgleich, VPN, Zertifikatverwaltung, Active Directory und mehrstufige Authentifizierung bereitgestellt werden.
- NVAs verschiedenster Anbieter stehen im [Azure Marketplace](https://azuremarketplace.microsoft.com) zur Verfügung.

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Bewährte Methode: Implementieren von Firewalls und NVAs im Hubnetzwerken

Im Hub wird das Umkreisnetzwerk (mit Zugriff auf das Internet) für gewöhnlich per Azure Firewall, über eine Firewallfarm oder über eine WAF verwaltet. Die folgende Tabelle enthält eine Gegenüberstellung:

| Firewalltyp | Details |
| --- | --- |
| WAFs | Web-Anwendungen sind üblich und weisen häufig Sicherheitsrisiken und Exploits auf. WAFs sind für die Erkennung von Angriffen auf Webanwendungen (HTTP/HTTPS) konzipiert. Verglichen mit herkömmlichen Firewalls weisen WAFs einen Satz von bestimmten Features auf, um den internen Webserver vor Bedrohungen zu schützen. |
| Azure Firewall | Azure Firewall verwendet genau wie NVA-Firewallfarmen einen allgemeinen Verwaltungsmechanismus und eine Gruppe von Sicherheitsregeln, um in Spoke-Netzwerken gehostete Workloads zu schützen. Darüber hinaus hilft Azure Firewall dabei, den Zugriff auf lokale Netzwerke zu steuern. Azure Firewall verfügt über integrierte Skalierbarkeit. |
| Firewalls mit virtuellen Netzwerkappliances | NVA-Firewallfarmen verfügen genau wie Azure Firewall über einen allgemeinen Verwaltungsmechanismus und eine Gruppe von Sicherheitsregeln, um in Spoke-Netzwerken gehostete Workloads zu schützen. Darüber hinaus helfen NVA-Firewalls dabei, den Zugriff auf lokale Netzwerke zu steuern. Firewalls mit virtuellen Netzwerkappliances können manuell hinter einem Lastenausgleich skaliert werden. <br><br> Eine Firewallfarm mit virtuellen Netzwerkappliances verfügt über weniger spezialisierte Software als ein WAF, muss aber einen umfassenderen Anwendungsbereich filtern und alle Arten von ein- oder ausgehendem Datenverkehr überprüfen. |

Es wird empfohlen, eine Gruppe von Azure-Firewalls (oder virtuellen Netzwerkappliances) für Datenverkehr aus dem Internet zu verwenden und eine andere für Datenverkehr mit lokalem Ursprung. Die Verwendung einer einzigen Gruppe von Firewalls für den gesamten Datenverkehr stellt ein Sicherheitsrisiko dar, da sie keinen wirksamen Sicherheitsbereich zwischen den beiden Arten von Netzwerkdatenverkehr bietet. Separate Firewallebenen vereinfachen die Überprüfung von Sicherheitsregeln und ermöglichen eine eindeutige Zuordnung von Regeln zu eingehenden Netzwerkanforderungen.

**Weitere Informationen** :

- Informieren Sie sich über die [Verwendung virtueller Netzwerkappliances in einem virtuellen Azure-Netzwerk](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz).

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über weitere Best Practices:

- [Bewährte Methoden](./migrate-best-practices-security-management.md) für Sicherheit und Verwaltung nach der Migration.
- [Best Practices](./migrate-best-practices-costs.md) für die Kostenverwaltung nach der Migration.
