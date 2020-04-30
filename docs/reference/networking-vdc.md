---
title: 'Das virtuelle Rechenzentrum: Eine Netzwerkperspektive'
description: Erfahren Sie anhand des Cloud Adoption Framework für Azure, wie Sie Ihre Infrastruktur mit Azure nahtlos in die Cloud erweitern und Architekturen mit mehreren Ebenen erstellen können.
author: tracsman
ms.author: jonor
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: ba2933a90c67d1c7c0cd33057ab0b2476dfd584c
ms.sourcegitcommit: 825f9ae5b6cdd2fa6cb18c14a9733ba9106194f2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81646982"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs iptables WAFs DDOS ITSM LLAP anycast vwan -->

# <a name="the-virtual-datacenter-a-network-perspective"></a>Das virtuelle Rechenzentrum: Eine Netzwerkperspektive

Anwendungen, die aus einer lokalen Umgebung migriert werden, profitieren von der sicheren, kostengünstigen Infrastruktur von Azure, selbst bei minimalen Anwendungsänderungen. Auch dann sollten Unternehmen ihre Architekturen anpassen, um ihre Flexibilität zu steigern und von den Funktionen von Azure zu profitieren.

Microsoft Azure stellt Dienste mit Hyperskalierung und Infrastruktur mit Funktionen und Zuverlässigkeit auf Unternehmensniveau bereit. Mit diesen Diensten und der Infrastruktur haben Sie viele Möglichkeiten in Bezug auf die Hybridkonnektivität, sodass Kunden die Wahl haben, ob sie über das Internet oder über eine private Netzwerkverbindung darauf zugreifen möchten. Außerdem können Microsoft-Partner erweiterte Funktionen in Form von Sicherheitsdiensten und virtuellen Geräten anbieten, die für die Verwendung in Azure optimiert sind.

Mit Azure können Kunden ihre Infrastruktur nahtlos auf die Cloud ausdehnen und Architekturen mit mehreren Ebenen erstellen.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-virtual-datacenter"></a>Was ist ein virtuelles Rechenzentrum?

Die Cloud war in ihrer Anfangszeit lediglich eine Plattform für das Hosting von öffentlich Anwendungen. Unternehmen erkannten den Wert der Cloud und begannen, interne Branchenanwendungen in die Cloud zu verlagern. Diese Anwendungen waren mit zusätzlicher Sicherheit, Zuverlässigkeit und Leistung sowie mit Kostenaspekten verbunden, die eine weitere Flexibilisierung hinsichtlich der Bereitstellung von Clouddiensten nötig machten. Es wurden neue Infrastruktur- und Netzwerkdienste geschaffen, mit denen für diese Flexibilität gesorgt wurde, sowie neue Features für flexible Skalierung, Notfallwiederherstellung und mehr.

Cloudlösungen waren anfänglich darauf ausgelegt, einzelne, relativ isolierte Anwendungen im öffentlichen Spektrum zu hosten. Dieser Ansatz hat sich für einige Jahre bewährt. Dann wurden jedoch die Vorteile von Cloudlösungen ersichtlich, und es wurden mehrere umfangreiche Workloads in der Cloud gehostet. Die Erfüllung der Anforderungen hinsichtlich der Sicherheit, Zuverlässigkeit, Leistung und Kosten von Bereitstellungen in mindestens einer Region entwickelte sich dadurch zu einem entscheidenden Faktor im Lebenszyklus des Clouddiensts.

Im Beispiel eines Cloud-Bereitstellungsdiagramms unten markiert das rote Kästchen eine Sicherheitslücke. Das gelbe Kästchen hingegen stellt Möglichkeiten zum Optimieren von virtuellen Netzwerkgeräten in verschiedenen Workloads dar.

![0][0]

Mit virtuellen Rechenzentren kann die Skalierung für Unternehmensworkloads erzielt werden. Diese Skalierung muss den Herausforderungen gerecht werden, die mit dem Ausführen umfassender Anwendungen in der öffentlichen Cloud verbunden sind.

Die Implementierung eines virtuellen Rechenzentrums (Virtual Datacenter, VDC) umfasst mehr als die Anwendungsworkloads in der Cloud. Sie stellt auch Netzwerk, Sicherheit, Verwaltung und sonstige Infrastruktur wie DNS und Active Directory-Dienste bereit. Wenn Unternehmen zusätzliche Workloads in Azure migrieren, sind die Infrastruktur und die Objekte zu bedenken, welche diese Workloads unterstützen. Durch eine sorgfältige Strukturierung Ihrer Ressourcen können Sie verhindern, dass Hunderte von getrennt verwalteten „Workloadinseln“ mit jeweils eigenen Datenflüssen, Sicherheitsmodellen und Konformitätsaspekten entstehen.

Das Konzept des virtuellen Rechenzentrums umfasst Empfehlungen und allgemeine Designs zum Implementieren einer Sammlung separater, jedoch zusammengehörender Entitäten. Diese Entitäten weisen häufig gemeinsame unterstützende Funktionen, Features und Infrastrukturen auf. Wenn Sie Ihre Workloads als virtuelles Rechenzentrum begreifen, können Sie aufgrund von Skaleneffekten, optimierter Sicherheit durch die Zentralisierung von Komponenten und Datenflüssen sowie der Vereinfachung von Vorgängen, der Verwaltung und Konformitätsprüfungen Kosten sparen.

> [!NOTE]
> Ein virtuelles Rechenzentrum ist **kein** spezieller Azure-Dienst. Stattdessen wurden verschiedene Azure-Features und -Funktionen miteinander kombiniert, um Ihre Anforderungen zu erfüllen. Ein virtuelles Rechenzentrum stellt ein bestimmtes Verständnis Ihrer Workloads und Azure-Nutzung dar, dessen Ziel es ist, Ihre Ressourcen und Möglichkeiten in der Cloud zu optimieren. Es handelt sich um einen modularen Ansatz zum Erstellen von IT-Diensten in Azure, bei dem die organisatorischen Rollen und Zuständigkeiten des Unternehmens respektiert werden.

Ein virtuelles Rechenzentrum kann Unternehmen dabei helfen, Workloads und Anwendungen für die folgenden Szenarien in Azure bereitzustellen:

- Hosten mehrerer verwandter Workloads
- Migrieren von Workloads aus einer lokalen Umgebung zu Azure
- Implementieren von gemeinsam genutzten oder zentralisierten Sicherheits- und Zugriffsanforderungen für verschiedene Workloads
- Ordnungsgemäßes Zusammenlegen von DevOps und der zentralen IT für große Unternehmen

## <a name="who-should-implement-a-virtual-datacenter"></a>Wer sollte ein virtuelles Rechenzentrum implementieren?

Alle Kunden, die sich für die Einführung von Azure entschieden haben, können von der effizienten Konfiguration eines Ressourcensatzes profitieren, der von allen Anwendungen gemeinsam genutzt wird. Je nach Größe können auch einzelne Anwendungen Vorteile aus den Mustern und den Komponenten ziehen, die zum Erstellen der Implementierung eines virtuellen Rechenzentrums verwendet werden.

In einigen Organisationen gibt es zentrale Teams oder Abteilungen für IT, Netzwerke, Sicherheit oder Compliance. Das Implementieren eines virtuellen Rechenzentrums kann dabei helfen, Aspekte von Richtlinien zu erzwingen, Zuständigkeiten voneinander abzugrenzen und die Konsistenz der zugrunde liegenden gemeinsamen Komponenten sicherzustellen. Anwendungsteams behalten die jeweils benötigte Freiheit und Kontrolle.

Organisationen mit DevOps-Ansatz können auch auf VDC-Konzepte setzen, um autorisierte Segmente von Azure-Ressourcen bereitzustellen. Mit dieser Methode kann sichergestellt werden, dass die DevOps-Gruppen über vollständige Kontrolle innerhalb dieser Gruppenstruktur verfügen, entweder auf der Abonnementebene oder innerhalb von Ressourcengruppen in einem gemeinsamen Abonnement haben. Gleichzeitig bleiben die Netzwerk- und Sicherheitsbegrenzungen entsprechend den definierten Vorgaben einer zentralen Richtlinie im Hub-Netzwerk und einer zentral verwalteten Ressourcengruppe konform.

## <a name="considerations-for-implementing-a-virtual-datacenter"></a>Überlegungen zur Implementierung eines virtuellen Rechenzentrums

Beim Entwerfen eines virtuellen Rechenzentrums sind diese zentralen Aspekte zu beachten:

### <a name="identity-and-directory-service"></a>Identitäts- und Verzeichnisdienst

Identitäts- und Verzeichnisdienste sind wichtige Aspekte jedes Rechenzentrums, ganz gleich, ob lokal oder in der Cloud gehostet. Identität bezieht sich auf alle Aspekte des Zugriffs und der Autorisierung für Dienste innerhalb der Implementierung eines virtuellen Rechenzentrums. Um sicherzustellen, dass nur autorisierte Benutzer und Prozesse auf Ihre Azure-Ressourcen zugreifen, verwendet Azure mehrere Typen von Anmeldeinformationen für die Authentifizierung. Hierzu zählen Kontokennwörter, Kryptografieschlüssel, digitale Signaturen und Zertifikate. Die [Azure Multi-Factor Authentication][multi-factor-authentication] bietet eine zusätzliche Sicherheitsebene für den Zugriff auf Azure-Dienste. Hierbei kommt die sichere Authentifizierung mit einer Reihe einfacher Überprüfungsoptionen (Telefonanruf, SMS oder Benachrichtigung in einer mobilen App) zur Anwendung, und Kunden können die von ihnen bevorzugte Methode auswählen.

Alle großen Unternehmen müssen einen Identitätsverwaltungsprozess definieren, der die Verwaltung der einzelnen Identitäten, deren Authentifizierung, Autorisierung, Rollen und Berechtigungen innerhalb eines oder in mehreren virtuellen Rechenzentren beschreibt. Mit diesem Prozess sollten Sicherheit und Produktivität gesteigert und gleichzeitig Kosten, Ausfallzeiten und sich wiederholende manuelle Aufgaben verringert werden.

Unternehmensorganisationen können eine anspruchsvolle Kombination aus Diensten für verschiedene Branchen erfordern, und Mitarbeiter nehmen häufig unterschiedliche Rollen ein, wenn sie an unterschiedlichen Projekten arbeiten. Das virtuelle Rechenzentrum erfordert eine gute Zusammenarbeit zwischen verschiedenen Teams mit bestimmten Rollendefinitionen, um Systeme verantwortungsbewusst mit geeigneter Governance aufzusetzen. Die Matrix der Zuständigkeiten, Zugriffsrechte und Berechtigungen kann komplex sein. Die Identitätsverwaltung im virtuellen Rechenzentrum wird über [Azure Active Directory][azure-ad] (Azure AD) und die rollenbasierte Zugriffssteuerung implementiert.

Ein Verzeichnisdienst ist eine freigegebene Informationsstruktur für die Suche, Verwaltung und Organisation von täglich verwendeten Elementen und Netzwerkressourcen. Diese Ressourcen können Volumes, Ordner, Dateien, Drucker, Benutzer, Gruppen, Geräte und andere Objekte enthalten. Jede Ressource im Netzwerk wird vom Verzeichnisserver als Objekt angesehen. Informationen zu einer Ressource werden als eine Auflistung von dieser Ressource oder diesem Objekt zugeordneten Attributen gespeichert.

Alle Microsoft-Onlinedienste für Unternehmen nutzen für Anmelde- und andere Identitätsanforderungen Azure Active Directory (Azure AD). Azure Active Directory ist eine umfassende, hochverfügbare Cloudlösung für die Identitäts- und Zugriffsverwaltung, die grundlegende Verzeichnisdienste, erweiterte Identitätsgovernance und Zugriffsverwaltung für Anwendungen kombiniert. Azure AD kann in eine lokale Active Directory-Instanz integriert werden, um einmaliges Anmelden für alle cloudbasierten und lokal gehosteten Anwendungen zu ermöglichen. Die Benutzerattribute der lokalen Active Directory-Instanz können automatisch mit Azure AD synchronisiert werden.

In einer Implementierung des virtuellen Rechenzentrums muss nicht ein einzelner globaler Administrator alle Berechtigungen zuweisen. Stattdessen können jeder spezifischen Abteilung, Gruppe von Benutzern oder Diensten im Verzeichnisdienst die erforderlichen Berechtigungen zum Verwalten ihrer eigenen Ressourcen innerhalb der Implementierung eines virtuellen Rechenzentrums zugewiesen werden. Das Strukturieren von Berechtigungen muss gut durchdacht sein. Zu viele Berechtigungen können die Leistungseffizienz beeinträchtigen, und zu wenige oder ungenau definierte Berechtigungen können Sicherheitsrisiken erhöhen. Die rollenbasierte Zugriffssteuerung in Azure löst dieses Problem, indem sie eine differenzierte Zugriffsverwaltung für die Ressourcen in einer VDC-Implementierung ermöglicht.

### <a name="security-infrastructure"></a>Sicherheitsinfrastruktur

Die Sicherheitsinfrastruktur bezieht sich auf die Trennung des Datenverkehrs im spezifischen VNET-Segment der Implementierung des virtuellen Netzwerks. Mit dieser Infrastruktur wird angegeben, wie der Ein- und Ausgang bei der Implementierung eines virtuellen Rechenzentrums gesteuert wird. Azure basiert auf einer mehrinstanzenfähigen Architektur. Nicht autorisierter oder unbeabsichtigter Datenverkehr zwischen Bereitstellungen wird durch Isolierung virtueller Netzwerke, Zugriffssteuerungslisten, Lastenausgleichsmodule, IP-Filter und Richtlinien zum Datenverkehrsfluss verhindert. Die Netzwerkadressenübersetzung (Network Address Translation, NAT) trennt den internen vom externen Netzwerkdatenverkehr.

Das Azure-Fabric ordnet Infrastrukturressourcen Mandantenworkloads zu und verwaltet die ein- und ausgehende Kommunikation von virtuellen Computern (Virtual Machines, VMs). Der Azure-Hypervisor erzwingt eine Speicher- und Prozesstrennung zwischen virtuellen Computern und routet den Netzwerkdatenverkehr sicher zu den Gastbetriebssystem-Mandanten.

### <a name="connectivity-to-the-cloud"></a>Verbindung mit der Cloud

Ein virtuelles Rechenzentrum erfordert Konnektivität mit externen Netzwerken, um Dienste für Kunden, Partner oder interne Benutzer bereitzustellen. Es ist nicht nur Konnektivität mit dem Internet, sondern auch mit lokalen Netzwerken und Rechenzentren erforderlich.

Kunden steuern, welche Dienste auf das öffentliche Internet zugreifen können und auf welche Dienste aus dem öffentlichen Internet zugegriffen werden kann. Dieser Zugriff wird mit [Azure Firewall][AzFW] oder anderen virtuellen Netzwerkgeräten, angepassten Routingrichtlinien mit [benutzerdefinierten Routen][UDR] und der Netzwerkfilterung mit [Netzwerksicherheitsgruppen][NSG] gesteuert. Wir empfehlen, alle Ressourcen mit Internetzugriff zusätzlich durch [Azure DDoS Protection Standard][DDoS] zu schützen.

Unternehmen müssen ihr virtuelles Rechenzentrum unter Umständen mit lokalen Rechenzentren oder anderen Ressourcen verbinden. Diese Konnektivität zwischen Azure und lokalen Netzwerken ist ein entscheidender Aspekt beim Entwerfen einer effektiven Architektur. Unternehmen haben zwei Möglichkeiten, diese Verknüpfung einzurichten: Übertragung über das Internet oder über private Direktverbindungen.

Ein [Azure-Site-to-Site-VPN][VPN] verbindet lokale Netzwerke mit Ihrem virtuellen Rechenzentrum in Azure. Der Link wird über sichere verschlüsselte Verbindungen (IPSec-Tunnel) hergestellt. Azure-Site-to-Site-VPN-Verbindungen sind flexibel, sie können schnell erstellt werden, und es muss in der Regel keine zusätzliche Hardware beschafft werden. Basierend auf Protokollen nach Branchenstandard können die meisten aktuellen Netzwerkgeräte VPN-Verbindungen mit Azure über das Internet oder vorhandene Konnektivitätspfade herstellen.

[**ExpressRoute**][ExR] ermöglicht private Verbindungen zwischen Ihrem virtuellen Rechenzentrum und lokalen Netzwerken. ExpressRoute-Verbindungen erfolgen nicht über das öffentliche Internet und bieten eine höhere Sicherheit, größere Zuverlässigkeit und schnellere Geschwindigkeit (bis zu 100 Gbit/s) bei konstanter Latenz. ExpressRoute bietet die Vorteile von Konformitätsregeln, die privaten Verbindungen zugeordnet sind. Mit [ExpressRoute Direct][ExRD] können Sie eine direkte 10-Gbit/s- oder 100-Gbit/s-Verbindung mit Microsoft-Routern herstellen.

Für die Bereitstellung von ExpressRoute-Verbindungen ist in der Regel ein ExpressRoute-Dienstanbieter erforderlich (eine Ausnahme stellt ExpressRoute Direct dar). Kunden, die schnell die Arbeit aufnehmen müssen, verwenden anfangs üblicherweise Site-to-Site-VPN-Verbindungen, um die Konnektivität zwischen dem virtuellen Rechenzentrum und lokalen Ressourcen herzustellen. Sobald die physische Verbindung mit dem Dienstanbieter eingerichtet wurde, migrieren sie die Konnektivität zu einer ExpressRoute-Verbindung.

Der Netzwerkdienst [**Azure Virtual WAN**][virtual-wan] bietet für eine große Anzahl von VPN- oder ExpressRoute-Verbindungen optimierte und automatisierte Konnektivität zwischen Branches über Azure. Per Virtual WAN können Sie Branchgeräte für die Kommunikation mit Azure verbinden und konfigurieren. Die Verbindungsherstellung und Konfiguration kann entweder manuell oder mit Geräten eines bevorzugten Anbieters über einen Virtual WAN-Partner durchgeführt werden. Die Nutzung von Geräten eines bevorzugten Anbieters ermöglicht eine einfache Verwendung, die Vereinfachung der Verbindungsherstellung und die Konfigurationsverwaltung. Über das integrierte Azure WAN-Dashboard können Sie anhand der Problembehandlung sofort Erkenntnisse gewinnen, um Zeit zu sparen, und auf einfache Weise umfangreiche Site-to-Site-Verbindungen anzeigen. Virtual WAN bietet außerdem Sicherheitsdienste mit einer optionalen Azure Firewall und Firewall Manager in Ihrem Virtual WAN-Hub.

### <a name="connectivity-within-the-cloud"></a>Konnektivität in der Cloud

[Virtuelle Azure-Netzwerke][virtual-network] und [Peering in virtuellen Netzwerken][virtual-network-peering] sind die grundlegenden Netzwerkkomponenten in einem virtuellen Rechenzentrum. Ein virtuelles Netzwerk garantiert eine Isolationsgrenze für Ressourcen virtueller Rechenzentren. Das Peering ermöglicht die Kommunikation zwischen verschiedenen virtuellen Netzwerken in derselben Azure-Regionen, zwischen verschiedenen Regionen und sogar zwischen Netzwerken in verschiedenen Abonnements. Innerhalb von und zwischen virtuellen Netzwerken können Datenverkehrsflüsse durch Sicherheitsregeln gesteuert werden, die in [Netzwerksicherheitsgruppen][NSG], Firewallrichtlinien ([Azure Firewall][AzFW] oder [virtuelle Netzwerkgeräte][NVA]) und [benutzerdefinierten Routen][UDR] angegeben sind.

Virtuelle Netzwerke sind zudem Ankerpunkte für die Integration von PaaS-Produkten (Platform-as-a-Service) von Azure wie [Azure Storage][Storage], [Azure SQL][SQL] und anderen integrierten öffentlichen Diensten mit öffentlichen Endpunkten. Mit [Dienstendpunkten][ServiceEndpoints] und [Azure Private Link][PrivateLink] können Sie Ihre öffentlichen Dienste mit Ihrem privaten Netzwerk integrieren. Sie können sogar ihre öffentlichen Dienste für privat erklären, aber dennoch die Vorteile der von Azure verwalteten PaaS-Dienste nutzen.

## <a name="virtual-datacenter-overview"></a>Übersicht über das virtuelle Rechenzentrum

### <a name="topologies"></a>Topologien

Ein virtuelles Rechenzentrum kann mit einer dieser allgemeinen Topologien entsprechend den jeweiligen Vorgaben und Skalierungsanforderungen erstellt werden:

In einer *flachen* Topologie werden sämtliche Ressourcen in einem einzigen virtuellen Netzwerk bereitgestellt. Subnetze ermöglichen die Steuerung und Trennung von Datenflüssen.

![11][11]

In einer *Mesh*-Topologie sind alle virtuellen Netzwerke über das Peering virtueller Netzwerke direkt miteinander verbunden.

![12][12]

Eine *Hub-and-Spoke-Peering*-Topologie eignet sich für verteilte Anwendungen und Teams mit delegierten Verantwortlichkeiten.

![13][13]

Eine *Azure Virtual WAN*-Topologie kann Szenarien mit umfassenden Branches und globale WAN-Dienste unterstützen.

![14][14]

Sowohl der Hub-and-Spoke-Peering-Topologie als auch der Azure Virtual WAN-Topologie liegt ein Hub-and-Spoke-Design zugrunde, das sich optimal für Kommunikation, gemeinsame Ressourcen und zentralisierte Sicherheitsrichtlinien eignet. Hubs werden mit einem Peering-Hub für virtuelle Netzwerke (in der Abbildung als `Hub Virtual Network` bezeichnet) oder einem Virtual WAN-Hub (in der Abbildung als `Azure Virtual WAN` bezeichnet) erstellt. Azure Virtual WAN ist auf Kommunikation zwischen umfassenden Branches und die Kommunikation zwischen Branches und Azure ausgelegt. Außerdem wird die Komplexität reduziert, da in einem Peering-Hub für virtuelle Netzwerke nicht alle Komponenten einzeln erstellt werden müssen. In einigen Fällen sprechen Ihre Anforderungen möglicherweise für ein Design mit einem Peering-Hub für virtuelle Netzwerke, z. B. wenn virtuelle Netzwerkgeräte im Hub vorhanden sein müssen.

In beiden Hub-Spoke-Topologien ist ein Hub die zentrale Netzwerkzone, die den gesamten Datenverkehr zwischen den verschiedenen Zonen steuert und überprüft: im Internet, lokal und in den Spokes. Mit der Hub-and-Spoke-Topologie kann die IT-Abteilung Sicherheitsrichtlinien zentral erzwingen. Außerdem verringert sie das Risiko von Fehlkonfigurationen und Offenlegungen.

Der Hub enthält oft die allgemeinen Dienstkomponenten, die von den Spokes genutzt werden. Im Folgenden finden Sie einige Beispiele für allgemeine zentrale Dienste:

- Die Windows Active Directory-Infrastruktur, die für die Benutzerauthentifizierung von Drittanbietern, die über nicht vertrauenswürdige Netzwerke zugreifen, erforderlich ist, bevor sie Zugriff auf die Workloads im Spoke erhalten. Dies beinhaltet die zugehörigen Active Directory-Verbunddienste (Active Directory Federation Services, AD FS).
- Ein DNS-Dienst (Distributed Name System), mit dem die Namen der Workloads in den Spokes aufgelöst werden, um lokal und über das Internet auf Ressourcen zuzugreifen, wenn [Azure DNS][DNS] nicht verwendet wird.
- Eine Public Key-Infrastruktur (PKI), mit der das einmalige Anmelden in Workloads implementiert wird.
- Flusssteuerung des TCP- und UDP-Datenverkehrs zwischen den Spoke-Netzwerkzonen und dem Internet.
- Flusssteuerung zwischen den Spokes und dem lokalen Netzwerk.
- Flusssteuerung zwischen zwei Spokes (sofern erforderlich).

Ein virtuelles Rechenzentrum reduziert die Gesamtkosten mithilfe der gemeinsamen Hubinfrastruktur, die mehrere Spokes umfasst.

Die Rolle eines jeden Spokes kann über verschiedene Arten von Workloads gehostet werden. Die Spokes können auch einen modularen Ansatz für wiederholbare Bereitstellungen der gleichen Workloads bieten. Beispiele hierfür sind Entwicklung und Tests, Benutzerakzeptanztests (User Acceptance Testing, UAT), Präproduktion und Produktion. Mit den Spokes können auch verschiedene Gruppen in Ihrer Organisation getrennt und aktiviert werden. Ein Beispiel hierfür sind DevOps-Gruppen. Innerhalb eines Spokes ist es möglich, eine einfache Workload oder komplexe Workloads mit mehreren Ebenen mit einer Datenverkehrssteuerung zwischen den Ebenen bereitzustellen.

### <a name="subscription-limits-and-multiple-hubs"></a>Abonnementlimit und mehrere Hubs

> [!IMPORTANT]
> Je Größe Ihrer Azure-Bereitstellungen müssen Sie möglicherweise eine Strategie mit mehreren Hubs verfolgen. Stellen Sie sich beim Entwerfen Ihrer Hub-and-Spoke-Strategie die Fragen „Kann dieses Design für die Verwendung eines weiteren virtuellen Hub-Netzwerks in dieser Region skaliert werden?“ und „Kann dieses Design so skaliert werden, dass mehrere Regionen abgedeckt werden?“. Es ist weitaus besser, einen Entwurf zu planen, der eine solche Skalierung zulässt, die dann nicht erforderlich ist, als wenn keine derartige Planung erfolgt und Sie diese benötigen.
>
> Ob auf einen sekundären Hub (oder weitere Hubs) skaliert werden muss, hängt von einer Vielzahl von Faktoren ab. Im Allgemeinen sind die inhärenten Beschränkungen für die Skalierung zu beachten. Beim Entwerfen der Skalierung müssen Sie das Abonnement, das virtuelle Netzwerk und die [Grenzen][limits] für virtuelle Computer überprüfen.

In Azure wird jede Komponente, unabhängig vom Typ, in einem Azure-Abonnement bereitgestellt. Die Isolation von Azure-Komponenten in verschiedenen Azure-Abonnements kann die Anforderungen verschiedener Branchenanwendungen erfüllen, z.B. das Einrichten unterschiedlicher Zugriffs- und Autorisierungsebenen.

Ein einzelne Implementierung eines virtuellen Rechenzentrums kann auf eine große Anzahl von Spokes hochskaliert werden, wobei aber wie bei jedem IT-System gewisse Plattformbeschränkungen gelten. Die Hub-Bereitstellung ist an ein bestimmtes Azure-Abonnement gebunden. Für dieses gelten Einschränkungen, wie z. B. eine maximale Anzahl von Peerings virtueller Netzwerke. Weitere Informationen finden Sie unter [Grenzwerte für Azure-Abonnements und Dienste, Kontingente und Einschränkungen][limits].) In Fällen, in denen diese Beschränkungen ein Problem darstellen, kann die Architektur weiter hochskaliert werden, indem das Modell von einem einzelnen Hub und Spoke auf ein Cluster von Hub und Spokes erweitert wird. Mehrere Hubs in einer oder mehreren Azure-Regionen können mithilfe von Peering virtueller Netzwerke, ExpressRoute, Virtual WAN oder einem Site-to-Site-VPN miteinander verbunden werden.

![2][2]

Die Einführung von mehreren Hubs erhöht die Kosten und den Verwaltungsaufwand für das System. Dies lässt sich nur durch Skalierbarkeit, Systemeinschränkungen oder Redundanz und die regionale Replikation zum Erzielen von Leistung für Endbenutzer oder Notfallwiederherstellung rechtfertigen. In Szenarios, die mehrere Hubs erfordern, sollten alle Hubs die gleichen Dienste anbieten, um die Vorgänge nicht zu erschweren.

### <a name="interconnection-between-spokes"></a>Verbindung zwischen Spokes

Innerhalb eines einzelnen Spokes oder in einem flachen Netzwerkdesign ist es möglich, komplexe Workloads mit mehreren Ebenen zu implementieren. Konfigurationen mit mehreren Ebenen können mit Subnetzen (eines für jede Ebene oder jede Anwendung) im gleichen virtuellen Netzwerk implementiert werden. Datenverkehr wird mithilfe von Netzwerksicherheitsgruppen und benutzerdefinierten Routen gesteuert und gefiltert.

Ein Architekt möchte vielleicht eine Workload mit mehreren Ebenen in mehreren virtuellen Netzwerken bereitstellen. Mittels Peering in virtuellen Netzwerken können Spokes Verbindungen mit anderen Spokes im gleichen Hub oder in anderen Hubs herstellen. Ein typisches Beispiel für dieses Szenario ist die Platzierung von Anwendungsverarbeitungsservern in einem Spoke oder virtuellen Netzwerk, während die Datenbank in einem anderen Spoke oder virtuellen Netzwerk bereitgestellt wird. In diesem Fall ist es einfach, die Spokes mittels Peering virtueller Netzwerke zu verbinden und dadurch das Durchlaufen des Hubs zu vermeiden. Die Architektur und Sicherheit sollten sorgfältig überprüft werden, um sicherzustellen, dass bei der Umgehung des Hubs keine wichtigen Sicherheits- oder Überwachungspunkte umgangen werden, die nur im Hub vorhanden sind.

![3][3]

Spokes können auch mit einem Spoke verbunden werden, der als Hub fungiert. Bei diesem Ansatz wird eine Hierarchie mit zwei Ebenen erstellt: Der Spoke auf der höheren Ebene (Ebene 0) wird der Hub der unteren Spokes (Stufe 1) in der Hierarchie. Die Spokes der Implementierung eines virtuellen Rechenzentrums sind zum Weiterleiten des Datenverkehrs an den zentralen Hub erforderlich, damit der Datenverkehr an sein Ziel im lokalen Netzwerk oder im öffentlichen Internet geleitet werden kann. Eine Architektur mit zwei Hub-Ebenen führt komplexes Routing ein, das die Vorteile einer einfachen Hub-Spoke-Beziehung aufhebt.

Obwohl Azure komplexe Topologien zulässt, ist eines der wesentlichen Prinzipien virtueller Rechenzentren die Wiederholbarkeit und Einfachheit. Um den Verwaltungsaufwand zu minimieren, empfehlen wir den einfachen Hub-Spoke-Entwurf als Referenzarchitektur für virtuelle Rechenzentren.

### <a name="components"></a>Komponenten

Das virtuelle Rechenzentrum besteht aus vier grundlegenden Komponententypen: **Infrastruktur**, **Umkreisnetzwerke**, **Workloads** und **Überwachung**.

Jeder Komponententyp besteht aus verschiedenen Azure-Funktionen und -Ressourcen. Ihre Implementierung des virtuellen Rechenzentrums besteht aus Instanzen verschiedener Komponententypen und mehreren Varianten des gleichen Komponententyps. Angenommen, Sie haben viele verschiedene, logisch getrennte Workload-Instanzen, die verschiedene Anwendungen darstellen. Aus diesen verschiedenen Komponententypen und Instanzen erstellen Sie letztendlich das virtuelle Rechenzentrum.

![4][4]

Die obige allgemeine konzeptionelle Architektur des virtuellen Rechenzentrums zeigt verschiedene Komponententypen, die in unterschiedlichen Zonen der Hub-and-Spoke-Topologie verwendet werden. Die Abbildung zeigt die Infrastrukturkomponenten in verschiedenen Teilen der Architektur.

Es ist im Allgemeinen eine bewährte Methode, gruppenbasierte Zugriffsrechte und Berechtigungen zu verwenden. Die Nutzung von Gruppen anstelle von einzelnen Benutzern vereinfacht die Wartung von Zugriffsrichtlinien, indem eine einheitliche teamübergreifende Verwaltung der Wartung erreicht und die Minimierung von Konfigurationsfehlern unterstützt wird. Das Zuweisen und Entfernen von Benutzern zu und aus den entsprechenden Gruppen erleichtert die Aktualisierung der Berechtigungen von bestimmten Benutzern.

Der Name jeder Rollengruppe sollte ein eindeutiges Präfix aufweisen. Anhand dieses Präfixes kann einfach ermittelt werden, welcher Gruppe eine Workload zugeordnet ist. Einer Workload, die einen Authentifizierungsdienst hostet, könnten beispielsweise Gruppen namens **AuthServiceNetOps**, **AuthServiceSecOps**, **AuthServiceDevOps** und **AuthServiceInfraOps** zugewiesen sein. Für zentrale Rollen oder Rollen, die in keinem Zusammenhang mit einem bestimmten Dienst stehen, könnte das Präfix **Corp** verwendet werden. Ein Beispiel hierfür ist **CorpNetOps**.

Viele Organisationen verwenden in etwa die folgenden Gruppen, um Rollen bereitzustellen:

- Die zentrale IT-Gruppe **Corp** verfügt über die Besitzrechte zum Steuern von Infrastrukturkomponenten. Beispiele hierfür sind Netzwerke und die Sicherheit. Der Gruppe muss über die Rolle „Mitwirkender“ für das Abonnement, die Kontrolle über den Hub und die Rechte eines Mitwirkenden des virtuellen Netzwerks in den Spokes verfügen. Große Unternehmen teilen diese Verwaltungsaufgaben häufig zwischen mehreren Teams auf, beispielsweise zwischen einer Gruppe für Netzwerkvorgänge **CorpNetOps**, die sich ausschließlich um den Netzwerkbetrieb kümmert, und einer Gruppe für Sicherheitsvorgänge **CorpSecOps**, die für die Firewall- und Sicherheitsrichtlinien verantwortlich ist. In diesem speziellen Fall müssen zwei unterschiedliche Gruppen für die Zuweisung dieser benutzerdefinierten Rollen erstellt werden.
- Die für die Entwicklung und Tests zuständige Gruppe **AppDevOps** ist für die Bereitstellung von App- oder Dienstworkloads verantwortlich. Diese Gruppe übernimmt die Rolle des VM-Mitwirkenden für IaaS-Bereitstellungen oder eine oder mehrere Rollen von PaaS-Mitwirkenden. Informationen dazu finden Sie unter [Integrierte Rollen für die rollenbasierte Zugriffssteuerung in Azure][Roles]. Optional benötigt das Entwicklungs- und Testteam möglicherweise Einblick in Sicherheitsrichtlinien (Netzwerksicherheitsgruppen) und Routingrichtlinien (benutzerdefinierte Routen) im Hub oder einem bestimmte Spoke. Zusätzlich zur Rolle des Mitwirkenden für Workloads benötigt diese Gruppe auch die Rolle des Netzwerklesers.
- Die Betriebs- und Wartungsgruppe **CorpInfraOps** oder **AppInfraOps** ist für die Verwaltung von Workloads in der Produktion zuständig. Diese Gruppe muss ein Mitwirkender des Abonnements von Workloads in jedem Produktionsabonnement sein. Manche Organisationen sollten zudem prüfen, ob sie ein zusätzliches Team für den Eskalationssupport mit der Rolle des Mitwirkenden des Abonnements in der Produktion und im zentralen Hub-Abonnement benötigen. Diese zusätzliche Gruppe behebt potenzielle Konfigurationsprobleme in der Produktionsumgebung.

Das virtuelle Rechenzentrum ist so ausgelegt, dass es für Gruppen, die für zentrale IT-Gruppen zur Verwaltung des Hubs erstellt wurden, entsprechende Gruppen auf Workloadebene gibt. Zusätzlich zur Verwaltung der Hub-Ressourcen können nur die zentralen IT-Gruppen den externen Zugriff und die Berechtigungen auf oberster Ebene für das Abonnement steuern. Workloadgruppen sind ebenfalls in der Lage, Ressourcen und Berechtigungen ihres eigenen virtuellen Netzwerks unabhängig von der zentralen IT zu steuern.

Das virtuelle Rechenzentrum ist partitioniert, damit mehrere Projekte in unterschiedlichen Branchenanwendungen sicher gehostet werden können. Alle Projekte erfordern unterschiedliche isolierte Umgebungen (Dev, UAT und Produktion). Einzelne Azure-Abonnements für jede dieser Umgebungen können natürliche Isolationsstufen darstellen.

![5][5]

Das obige Diagramm veranschaulicht die Beziehung zwischen den Projekten, Benutzern und Gruppen einer Organisation und den Umgebungen, in denen die Azure-Komponenten bereitgestellt werden.

In der Regel ist eine Umgebung (oder Ebene) in der IT ein System, in dem mehrere Anwendungen bereitgestellt und ausgeführt werden. Große Unternehmen verwenden eine Entwicklungsumgebung (in der Änderungen vorgenommen und getestet werden) und eine Produktionsumgebung (die die Endbenutzer verwenden). Diese Umgebungen werden häufig durch mehrere Stagingumgebungen getrennt, um die Bereitstellung (Rollout), Tests und den Rollback in Phasen zu ermöglichen, falls Probleme auftreten. Bereitstellungsarchitekturen unterscheiden sich erheblich. In der Regel wird aber dem Grundmuster (Entwicklung (DEV) = Beginn, Produktion (PROD) = Ende) gefolgt.

Eine übliche Architektur für diese Arten von Umgebungen mit mehreren Ebenen besteht aus einer DevOps-Umgebung für Entwicklung und Tests, einer UAT-Umgebung für das Staging und einer Produktionsumgebung. Organisationen können einzelne oder mehrere Azure AD-Mandanten nutzen, um Zugriff auf und Rechte für diese Umgebungen zu definieren. Die vorherige Abbildung veranschaulicht die Verwendung von zwei verschiedenen Azure AD-Mandanten: einen für DevOps und UAT und der andere ausschließlich für die Produktion.

Wenn mehrere Azure AD-Mandanten vorhanden sind, müssen die Umgebungen getrennt werden. Für den Zugriff auf einen anderen Azure AD-Mandanten muss sich dieselbe Benutzergruppe (z. B. die zentrale IT) mit einem anderen URI authentifizieren, um die Rollen oder Berechtigungen der DevOps-Umgebung oder der Produktionsumgebung eines Projekts zu ändern. Die Verwendung unterschiedlicher Benutzerauthentifizierungen für den Zugriff auf verschiedene Umgebungen reduziert das Risiko möglicher Ausfälle und anderer Probleme durch menschliches Versagen.

#### <a name="component-type-infrastructure"></a>Komponententyp: Infrastruktur

In diesem Komponententyp befindet sich der Großteil der unterstützenden Infrastruktur. Diese Komponente beansprucht auch die meiste Zeit Ihrer Teams für die zentrale IT, Sicherheit und Konformität.

![6][6]

Infrastrukturkomponenten stellen eine Verbindung für die unterschiedlichen Komponenten der Implementierung eines virtuellen Rechenzentrums bereit und sind sowohl auf dem Hub als auch auf den Spokes vorhanden. Die Verantwortung für die Verwaltung und Wartung der Infrastrukturkomponenten wird in der Regel der zentralen IT und/oder dem Sicherheitsteam zugewiesen.

Eine der wichtigsten Aufgaben des IT-Infrastrukturteams ist die Gewährleistung der Konsistenz von IP-Adressenschemata im gesamten Unternehmen. Der private IP-Adressraum, der einer Implementierung eines virtuellen Rechenzentrums zugewiesen ist, muss konsistent sein und darf sich NICHT mit privaten IP-Adressen in Ihren lokalen Netzwerken überlappen.

Obwohl die Netzwerkadressenübersetzung (Network Address Translation, NAT) in den lokalen Edgeroutern oder in Azure-Umgebungen IP-Adressenkonflikte vermeiden kann, bedeutet sie Komplikationen für Ihre Infrastrukturkomponenten. Die Vereinfachung der Verwaltung ist eines der wichtigsten Ziele des virtuellen Rechenzentrums. Aus diesem Grund ist es nicht empfehlenswert, die Netzwerkadressenübersetzung zur Behandlung von IP-Problemen zu verwenden, auch wenn sie eine zulässige Lösung darstellt.

Infrastrukturkomponenten bieten die folgenden Funktionen:

- [**Identitäts- und Verzeichnisdienste**][azure-ad]. Der Zugriff auf jeden Ressourcentyp in Azure wird durch eine in einem Verzeichnisdienst gespeicherte Identität gesteuert. Der Verzeichnisdienst speichert nicht nur die Liste der Benutzer, sondern auch die Zugriffsrechte für Ressourcen in einem bestimmten Azure-Abonnement. Diese Dienste können rein cloudbasiert sein, oder sie können mit einer lokalen Identität in Active Directory synchronisiert werden.
- [**Virtuelles Netzwerk**][virtual-network]. Virtuelle Netzwerke sind eine der Hauptkomponenten des virtuellen Rechenzentrums und ermöglichen es Ihnen, eine Isolationsgrenze für den Datenverkehr auf der Azure-Plattform zu erstellen. Ein virtuelles Netzwerk besteht aus einem einzelnen oder mehreren virtuellen Netzwerksegmenten, die jeweils ein bestimmtes Präfix für IP-Netzwerke (ein Subnetz, entweder IPv4 oder Dual Stack IPv4/IPv6) haben. Das virtuelle Netzwerk definiert einen internen Umkreisbereich, in dem IaaS-VMs und PaaS-Dienste eine private Kommunikation herstellen können. Virtuelle Computer (und PaaS-Dienste) in einem virtuellen Netzwerk können nicht direkt mit virtuellen Computern (und PaaS-Diensten) in anderen virtuellen Netzwerken kommunizieren, selbst wenn beide virtuelle Netzwerke vom gleichen Kunden im selben Abonnement erstellt wurden. Isolation ist eine wichtige Eigenschaft, mit der sichergestellt wird, dass VMs und die Kommunikation von Kunden innerhalb eines virtuellen Netzwerks privat bleiben. Wenn netzwerkübergreifende Verbindungen gewünscht werden, kann dies mit den im Folgenden beschriebenen Features erreicht werden.
- [**Peering virtueller Netzwerke**][virtual-network-peering]. Die grundlegende Funktion für das Erstellen der Infrastruktur eines virtuellen Rechenzentrums ist das Peering virtueller Netzwerke. Dabei werden zwei virtuelle Netzwerke in der gleichen Region über das Netzwerk des Azure-Rechenzentrums oder regionsübergreifend über den weltweiten Azure-Backbone verbunden.
- [**VNET-Dienstendpunkte**][ServiceEndpoints]. Dienstendpunkte erweitern den privaten Adressraum Ihres virtuellen Netzwerks, sodass er den PaaS-Raum einschließt. Die Endpunkte erweitern auch die Identität Ihres virtuellen Netzwerks über eine direkte Verbindung auf die Azure-Dienste. Endpunkte ermöglichen es Ihnen, Ihre kritischen Ressourcen von Azure-Diensten auf Ihre virtuellen Netzwerke zu beschränken und so zu schützen.
- [**Private Link**][PrivateLink]. Mit Azure Private Link können Sie über einen privaten Endpunkt in Ihrem virtuellen Netzwerk auf Azure-PaaS-Dienste (beispielsweise [Azure Storage][Storage], [Azure Cosmos DB][Cosmos] und [Azure SQL Database][SQL]) sowie auf in Azure gehostete Kunden-/Partnerdienste zugreifen. Der Datenverkehr zwischen Ihrem virtuellen Netzwerk und dem Dienst wird über das Microsoft-Backbone-Netzwerk übertragen und dadurch vom öffentlichen Internet isoliert. Sie können auch Ihren eigenen [Private Link-Dienst][PrivateLinkSvc] in Ihrem virtuellen Netzwerk erstellen und Ihren Kunden privat zur Verfügung stellen. Die Einrichtung und Nutzung von Azure Private Link ist in Azure-PaaS-, Kunden- und gemeinsamen Partnerdiensten konsistent.
- [**Benutzerdefinierte Routen**][UDR]. Datenverkehr in einem virtuellen Netzwerk wird standardmäßig basierend auf der Systemroutingtabelle weitergeleitet. Eine benutzerdefinierte Route ist eine vom Benutzer definierte Routingtabelle, die von Netzwerkadministratoren einem oder mehreren Subnetzen zugeordnet werden kann, um das Verhalten der Systemroutingtabelle außer Kraft zu setzen und einen Kommunikationspfad innerhalb eines virtuellen Netzwerks zu definieren. Benutzerdefinierte Routen gewährleisten, dass ausgehender Datenverkehr aus dem Spoke durch einen bestimmten benutzerdefinierten virtuellen Computer oder virtuelle Netzwerkgeräte und Lastenausgleichsmodule geleitet wird, die sowohl im Hub als auch in den Spokes vorhanden sind.
- [**Netzwerksicherheitsgruppen**][NSG]. Eine Netzwerksicherheitsgruppe ist eine Liste von Sicherheitsregeln, die als Datenverkehrsfilter für IP-Quellen, IP-Ziele, Protokolle, IP-Quellports und IP-Zielports fungieren (auch als Fünf-Tupel der Ebene 4 bezeichnet). Die Netzwerksicherheitsgruppe kann auf ein Subnetz, auf eine virtuelle Netzwerkkarte (NIC), die mit einer Azure-VM verknüpft ist, oder beides angewendet werden. Netzwerksicherheitsgruppen sind entscheidend für die Implementierung einer korrekten Flusssteuerung im Hub und in den Spokes. Das Maß an Sicherheit, das die Netzwerksicherheitsgruppen bieten, hängt davon ab, welche Ports Sie öffnen und zu welchem Zweck. Kunden sollten zusätzliche Filter für jede VM mit hostbasierten Firewalls anwenden, z. B. iptables oder die Windows-Firewall.
- [**DNS**][DNS]. DNS ermöglicht die Namensauflösung für Ressourcen in einem virtuellen Rechenzentrum. Azure bietet DNS-Dienste für [öffentliche][DNS] und [private][PrivateDNS] Namensauflösung. Private Zonen bieten Namensauflösung in einem virtuellen Netzwerk sowie zwischen virtuellen Netzwerken. Sie können private Zonen einrichten, die sich nicht nur über virtuelle Netzwerke in derselben Region erstrecken, sondern auch zwischen Regionen und Abonnements. Für die öffentliche Auflösung bietet Azure DNS einen Hostingdienst für DNS-Domänen, der die Namensauflösung mithilfe von Microsoft Azure-Infrastruktur durchführt. Durch das Hosten Ihrer Domänen in Azure können Sie Ihre DNS-Einträge mithilfe der gleichen Anmeldeinformationen, APIs, Tools und Abrechnung wie für die anderen Azure-Dienste verwalten.
- [**Managementgruppen**][MgmtGrp]-, [**Abonnement**][subscription-management]- und [**Ressourcengruppen**][RGMgmt]-Verwaltung. Ein Abonnement definiert eine natürliche Grenze, um mehrere Ressourcengruppen in Azure zu erstellen. Diese Abgrenzung kann sich auf Funktionen, die Trennung von Rollen oder die Abrechnung beziehen. Ressourcen in einem Abonnement werden in logischen Containern zusammengefasst, die als Ressourcengruppen bezeichnet werden. Die Ressourcengruppe stellt eine logische Gruppe dar, in der die Ressourcen eines virtuellen Rechenzentrums organisiert werden. Wenn Ihre Organisation über viele Abonnements verfügt, benötigen Sie möglicherweise eine Möglichkeit zur effizienten Verwaltung von Zugriff, Richtlinien und Konformität für diese Abonnements. Azure-Verwaltungsgruppen stellen einen abonnementübergreifenden Bereich dar. Sie organisieren Abonnements in Containern, die als Verwaltungsgruppen bezeichnet werden, und wenden Ihre Governancebedingungen auf die Verwaltungsgruppen an. Alle Abonnements in einer Verwaltungsgruppe erben automatisch die auf die Verwaltungsgruppe angewendeten Bedingungen. Informationen zu diesen drei Features in einer hierarchischen Ansicht finden Sie unter [Organisieren Ihrer Azure-Ressourcen][Organize] im Cloud Adoption Framework.
- [**Rollenbasierte Zugriffssteuerung (RBAC)** ][RBAC]. Mit RBAC ist es möglich, die Organisationsrollen und Zugriffsberechtigungen für bestimmte Azure-Ressourcen zuzuordnen und gleichzeitig Benutzer auf eine bestimmte Teilmenge von Aktionen zu beschränken. Wenn Sie Azure Active Directory mit einem lokalen Active Directory synchronisieren, können Sie in Azure die gleichen Active Directory-Gruppen verwenden, die Sie lokal verwenden. Mit RBAC können Sie Zugriff gewähren, indem Sie Benutzern, Gruppen und Anwendungen innerhalb des relevanten Bereichs die entsprechende Rolle zuweisen. Der Bereich einer Rollenzuweisung kann ein Azure-Abonnement, eine Ressourcengruppe oder eine einzelne Ressource sein. RBAC ermöglicht die Vererbung von Berechtigungen. Mit einer Rolle, die einem übergeordneten Bereich zugewiesen ist, wird außerdem der Zugriff auf die darin enthaltenen untergeordneten Elemente gewährt. Mit RBAC können Sie Aufgaben verteilen und Benutzern nur den Zugriff gewähren, den sie zur Ausführung ihrer Aufgaben benötigen. Ein Mitarbeiter kann beispielsweise virtuelle Computer in einem Abonnement verwalten, während ein anderer im gleichen Abonnement SQL Server-Datenbanken verwalten kann.

#### <a name="component-type-perimeter-networks"></a>Komponententyp: Umkreisnetzwerke

Mit den Komponenten eines Umkreisnetzwerks (das gelegentlich auch als DMZ-Netzwerk bezeichnet wird) können Sie Verbindungen zwischen Ihren lokalen oder physischen Rechenzentrumsnetzwerken und darüber hinaus Konnektivität mit dem Internet herstellen. Ihre Netzwerk- und Sicherheitsteams verwenden in der Regel viel Zeit auf den Umkreis.

Eingehende Pakete sollten durch die Sicherheitsgeräte im Hub geleitet werden, bevor sie die Back-End-Server und -Dienste in den Spokes erreichen. Beispiele für diese Sicherheitsgeräte sind die Firewall, IDS und IPS. Von den Workloads an das Internet gesendete Pakete sollten ebenfalls über die Sicherheitsgeräte im Umkreisnetzwerk geleitet werden, bevor sie das Netzwerk verlassen. Mit diesem Fluss können Richtlinien erzwungen, überprüft und überwacht werden.

Komponenten des Umkreisnetzwerks:

- [Virtuelle Netzwerke][virtual-network], [benutzerdefinierte Routen][UDR] und [Netzwerksicherheitsgruppen][NSG]
- [Virtuelle Netzwerkgeräte][NVA]
- [Azure-Lastenausgleich][ALB]
- [Azure Application Gateway][AppGW] mit [Web Application Firewall (WAF)][AppGWWAF]
- [Öffentliche IP-Adressen][PIP]
- [Azure Front Door][azure-front-door] mit [Web Application Firewall (WAF)][AFDWAF]
- [Azure Firewall][AzFW] und [Azure Firewall Manager][AzFWMgr]
- [DDoS Protection Standard][DDoS]

In der Regel sind die zentralen IT- und Sicherheitsteams für die Anforderungsdefinition und die Vorgänge in den Umkreisnetzwerken verantwortlich.

![7][7]

Die obige Abbildung veranschaulicht die Durchsetzung von zwei Perimetern mit Zugriff auf das Internet und einem lokalen Netzwerk, beide im DMZ-Hub. Im DMZ-Hub kann das Umkreisnetzwerk zum Internet zur Unterstützung vieler Branchenanwendungen mit mehreren Farmen von Web Application Firewalls (WAFs) oder Azure Firewalls hochskaliert werden. Der Hub ermöglicht je nach Bedarf außerdem lokale Konnektivität über VPN oder ExpressRoute.

> [!NOTE]
> Im obigen Diagramm können Sie im „DMZ Hub“ viele der folgenden Features zusammen in einem Azure Virtual WAN-Hub bündeln (z. B. virtuelle Netzwerke, benutzerdefinierte Routen, Netzwerksicherheitsgruppen, VPN-Gateways, ExpressRoute-Gateways, Azure Load Balancer-Instanzen, Azure Firewall-Instanzen, Firewall Manager und DDOS). Das Verwenden von Azure Virtual WAN-Hubs kann die Erstellung des virtuellen Hub-Netzwerks und damit des virtuellen Rechenzentrums sehr erleichtern, da die meisten technisch komplexen Vorgänge beim Erstellen eines Azure Virtual WAN-Hubs von Azure ausgeführt werden.

[**Virtuelle Netzwerke**][virtual-network]. Der Hub basiert normalerweise auf einem virtuellen Netzwerk mit mehreren Subnetzen, um verschiedene Arten von Diensten zu hosten, die den Internetdatenverkehr über Azure Firewall, virtuelle Netzwerkgeräte, WAFs und Azure Application Gateway-Instanzen filtern und überprüfen.

[**Benutzerdefinierte Routen**][UDR]: Mit benutzerdefinierten Routen können Kunden Firewalls, IDS/IPS und andere virtuelle Geräte bereitstellen und den Netzwerkdatenverkehr über diese Sicherheitsgeräte leiten, um Sicherheitsrichtlinien zu erzwingen und die Überprüfung und Überwachung durchzuführen. Benutzerdefinierte Routen können sowohl im Hub als auch in den Spokes erstellt werden, um sicherzustellen, dass Datenverkehr durch die spezifischen benutzerdefinierten VMs, virtuellen Netzwerkgeräte und Lastenausgleichsmodule geleitet wird, die von einer VDC-Implementierung verwendet werden. Um zu gewährleisten, dass der von virtuellen Computern generierte Datenverkehr im Spoke zu den richtigen virtuellen Geräten geleitet wird, muss in den Subnetzen des Spokes eine benutzerdefinierte Route festgelegt werden, indem die Front-End-IP-Adresse des internen Lastenausgleichsmoduls als nächster Hop festgelegt wird. Der interne Load Balancer verteilt den internen Datenverkehr auf die virtuellen Geräte (Back-End-Pool des Load Balancers).

[**Azure Firewall**][AzFW] ist ein verwalteter Netzwerksicherheitsdienst zum Schutz Ihrer Azure Virtual Network-Ressourcen. Es handelt sich dabei um eine zustandsbehaftete verwaltete Firewall mit Hochverfügbarkeit und Cloudskalierbarkeit. Sie können Richtlinien zur Anwendungs- und Netzwerkkonnektivität übergreifend für Abonnements und virtuelle Netzwerke zentral erstellen, erzwingen und protokollieren. Azure Firewall verwendet eine statische öffentliche IP-Adresse für Ihre virtuellen Netzwerkressourcen. Dadurch können externe Firewalls Datenverkehr aus Ihrem virtuellen Netzwerk identifizieren. Der Dienst ist für Protokollierung und Analyse vollständig in Azure Monitor integriert.

Wenn Sie die Azure Virtual WAN-Topologie verwenden, verfügen Sie mit [**Azure Firewall Manager**][AzFWMgr] über einen Sicherheitsverwaltungsdienst, der eine zentrale Sicherheitsrichtlinien- und Routenverwaltung für cloudbasierte Sicherheitsperimeter bereitstellt. Der Dienst arbeitet mit Azure Virtual WAN Hub zusammen, einer von Microsoft verwalteten Ressource, mit der Sie ganz einfach Hub-and-Spoke-Architekturen erstellen können. Wenn einem solchen Hub Sicherheits- und Routingrichtlinien zugeordnet werden, wird dieser als geschützter virtueller Hub bezeichnet.

[**Virtuelle Netzwerkgeräte**][NVA]. Im Hub wird das Umkreisnetzwerk mit Zugriff auf das Internet normalerweise über eine Azure Firewall-Instanz oder eine Farm von Firewalls oder Web Application Firewall (WAF) verwaltet.

In verschiedenen Branchen werden häufig viele Webanwendungen verwendet. Diese Anwendungen weisen häufig diverse Sicherheitsrisiken und potenzielle Exploits auf. Eine Web Application Firewall ist ein spezielles Produkt, das Angriffe auf Webanwendungen (HTTP/HTTPS) genauer erkennt als eine generische Firewall. Verglichen mit herkömmlichen Firewalls besitzen WAFs einen Satz von bestimmten Features, um den internen Webserver vor Bedrohungen zu schützen.

Azure Firewall oder eine NVA-Firewall wird jeweils über eine gemeinsame Verwaltungsebene mit einem Satz von Sicherheitsregeln ausgeführt, die die in den Spokes gehosteten Workloads schützen und den Zugriff auf lokale Netzwerke steuern. Azure Firewall verfügt über integrierte Skalierbarkeit, während NVA-Firewalls hinter einem Lastenausgleich manuell skaliert werden können. Im Allgemeinen verfügt eine Firewallfarm im Vergleich zu einer Web Application Firewall über weniger spezialisierte Software. Sie hat jedoch einen umfassenderen Anwendungsbereich, sodass sie alle Arten von ein- und ausgehendem Datenverkehr filtern und überprüfen kann. Virtuelle Netzwerkgeräte für den NVA-Ansatz sind auf dem Azure Marketplace verfügbar und können von dort bereitgestellt werden.

Wir empfehlen, eine Gruppe von Azure Firewall-Instanzen oder virtuellen Netzwerkgeräten für Datenverkehr aus dem Internet zu verwenden. Verwenden Sie für Datenverkehr mit lokalem Ursprung eine andere Gruppe. Die Verwendung einer einzigen Gruppe von Firewalls für den gesamten Datenverkehr stellt ein Sicherheitsrisiko dar, da sie keinen wirksamen Sicherheitsbereich zwischen den beiden Arten von Netzwerkdatenverkehr bietet. Separate Firewallebenen vereinfachen die Überprüfung von Sicherheitsregeln und ermöglichen eine eindeutige Zuordnung von Regeln zu eingehenden Netzwerkanforderungen.

[**Azure Load Balancer**][ALB] stellt einen Dienst mit hoher Verfügbarkeit der Ebene 4 (TCP, UDP) bereit, mit dem eingehender Datenverkehr zwischen Dienstinstanzen verteilt werden kann, die in einem Satz mit Lastenausgleich definiert sind. Der Datenverkehr, der von den Front-End-Endpunkten (öffentliche IP-Endpunkte oder private IP-Endpunkte) an den Load Balancer gesendet wird, kann mit oder ohne Adressübersetzung auf einen Satz von Back-End-IP-Adresspools weiterverteilt werden (z. B. virtuelle Netzwerkgeräte oder virtuelle Computer).

Der Azure Load Balancer kann die Integrität der verschiedenen Serverinstanzen überprüfen, und wenn bei einer Instanz die Antwort auf einen Test ausbleibt, beendet der Load Balancer das Senden von Datenverkehr an die fehlerhafte Instanz. Im virtuellen Rechenzentrum wird ein externer Load Balancer für den Hub und die Spokes bereitgestellt. Auf dem Hub wird der Load Balancer zum effizienten Weiterleiten von Datenverkehr über Firewall-Instanzen verwendet. Auf den Spokes dienen Load Balancers zum Verwalten des Datenverkehrs von Anwendungen.

Der Microsoft-Dienst [**Azure Front Door Service**][azure-front-door] (AFDS) stellt eine hoch verfügbare und hochgradig skalierbare Plattform für die Beschleunigung von Webanwendungen mit globalem HTTP-Lastenausgleich, Anwendungsschutz und Content Delivery Network bereit. AFDS wird an mehr als 100 Standorten im Edgebereich des globalen Netzwerks von Microsoft ausgeführt und ermöglicht Ihnen das Erstellen, Ausführen und Aufskalieren Ihrer dynamischen Webanwendung und statischen Inhalte. AFDS stellt für Ihre Anwendung erstklassige Endbenutzerleistung, einheitliche Automatisierung der Regions-/Stempelwartung, BCDR-Automatisierung, einheitliche Client-/Benutzerinformationen, Zwischenspeicherung und Erkenntnisse zu Ihren Diensten bereit. Die Plattform bietet Folgendes:
    - Leistung, Zuverlässigkeit und Vereinbarungen zum Service Level (SLAs) für den Support
    - Compliancezertifizierungen
    - Überprüfbare Sicherheitspraktiken, die von Azure entwickelt, betrieben und nativ unterstützt werden.
Azure Front Door bietet außerdem eine Web Application Firewall (WAF), mit der Webanwendungen vor häufigen Sicherheitsrisiken und Exploits geschützt werden.

[**Azure Application Gateway**][AppGW] ist ein dediziertes virtuelle Gerät, mit dem ein verwalteter ADC (Controller zur Anwendungsbereitstellung) bereitgestellt wird. Es bietet verschiedene Lastenausgleichsfunktionen der Ebene 7 für Ihre Anwendung. Sie können damit die Leistung von Webfarmen steigern, indem sie die CPU-intensive SSL-Beendigung an das Anwendungsgateway auslagern. Darüber hinaus werden noch weitere Routingfunktionen der Ebene 7 bereitgestellt. Hierzu zählen etwa die Roundrobin-Verteilung des eingehenden Datenverkehrs, cookiebasierte Sitzungsaffinität, Routing auf URL-Pfadbasis und die Möglichkeit zum Hosten mehrerer Websites hinter einer einzelnen Application Gateway-Instanz. Eine Web Application Firewall (WAF) wird auch als Teil des WAF SKU des Anwendungsgateways bereitgestellt. Dieser SKU bietet Schutz für Webanwendungen vor allgemeinen Onlinesicherheitsrisiken und Exploits. Application Gateway kann als Gateway mit Internetanbindung, rein internes Gateway oder als Kombination dieser beiden Optionen konfiguriert werden.

[**Öffentliche IP-Adressen**][PIP]. Einige Azure-Features ermöglichen Ihnen, einer öffentlichen IP-Adresse Dienstendpunkte zuzuordnen, sodass über das Internet auf die Ressource zugegriffen werden kann. Der Endpunkt verwendet die Netzwerkadressenübersetzung (NAT), um Datenverkehr zur internen Adresse und zum Port im virtuellen Azure-Netzwerk zu leiten. Dieser Pfad ist der primäre Weg, auf dem externer Datenverkehr in das virtuelle Netzwerk gelangt. Sie können die öffentlichen IP-Adressen konfigurieren, um festzulegen, welcher Datenverkehr zugelassen wird bzw. wie und wo eine Übersetzung in das virtuelle Netzwerk stattfindet.

[**Azure DDoS Protection Standard**][DDoS] stellt über den Diensttarif [Basic][DDoS] zusätzliche Funktionen zur Bedrohungsabwehr bereit, die speziell für Azure Virtual Network-Ressourcen optimiert sind. DDoS Protection Standard kann leicht aktiviert werden und erfordert keine Änderung der Anwendung. Schutzrichtlinien werden über dedizierte Datenverkehrsüberwachung und Machine Learning-Algorithmen optimiert. Richtlinien werden auf öffentliche IP-Adressen angewendet, die in virtuellen Netzwerken bereitgestellten Ressourcen zugeordnet sind. Beispiele hierfür sind Instanzen von Azure Load Balancer, Azure Application Gateway und Azure Service Fabric. Über Azure Monitor-Ansichten stehen systemgenerierte Protokolle (nahezu in Echtzeit) während eines Angriffs und für den Verlauf zur Verfügung. Mit der Web Application Firewall für Azure Application Gateway können Sie Schutz auf der Anwendungsebene hinzufügen. Schutz wird für öffentliche Azure-IP-Adressen mit IPv4 und IPv6 bereitgestellt.

Die Hub-Spoke-Topologie nutzt zum ordnungsgemäßen Weiterleiten von Datenverkehr das Peering virtueller Netzwerke und benutzerdefinierte Routen.

![8][8]

Im Diagramm stellt die benutzerdefinierte Route sicher, dass der Datenverkehr von der Spoke zur Firewall fließt, bevor er über das ExpressRoute-Gateway an den lokalen Standort weitergegeben wird (sofern die Firewallrichtlinie diesen Datenfluss zulässt).

#### <a name="component-type-monitoringmonitoroverview"></a>Komponententyp: [Überwachung][MonitorOverview]

Überwachungskomponenten bieten Sichtbarkeit und Warnungen aus allen anderen Komponententypen. Alle Teams sollten die Komponenten und Dienste, auf die sie Zugriff haben, überwachen können. Wenn Sie über einen zentralen Helpdesk oder Betriebsteams verfügen, benötigen diese integrierten Zugriff auf die von diesen Komponenten bereitgestellten Daten.

Azure bietet verschiedene Protokollierungs- und Überwachungsdienste zum Nachverfolgen des Verhaltens von in Azure gehosteten Ressourcen. Die Governance und Steuerung von Workloads in Azure basiert nicht nur auf dem Sammeln von Protokolldaten, sondern auch auf der Möglichkeit, Aktionen auf der Grundlage von bestimmten gemeldeten Ereignissen auszulösen.

[**Azure Monitor**][AzureMonitor]. Azure umfasst mehrere Dienste, die eine bestimmte Rolle oder Aufgabe im Überwachungsbereich ausführen. Zusammen bieten diese Dienste eine umfassende Lösung für das Sammeln, Analysieren und Verarbeiten von systemgenerierten Protokollen aus Ihren Anwendungen und den zugrunde liegenden Azure-Ressourcen, die sie unterstützen. Sie können auch kritische lokale Ressourcen überwachen und so eine hybride Überwachungsumgebung bilden. Voraussetzung der Entwicklung einer vollständigen Überwachungsstrategie für Ihre Anwendungen ist die Kenntnis der verfügbaren Tools und Daten.

In Azure Monitor gibt es zwei grundlegende Typen von Protokollen:

- [Metriken][Metrics] sind numerische Werte, die einen Aspekt eines Systems zu einem bestimmten Zeitpunkt beschreiben. Sie sind einfach strukturiert und in der Lage, Szenarien nahezu in Echtzeit zu unterstützen. Für viele Azure-Ressourcen können die von Azure Monitor gesammelten Daten direkt auf ihrer Übersichtsseite im Azure-Portal angezeigt werden. Werfen Sie beispielsweise einen Blick auf einen beliebigen virtuellen Computer, und Sie sehen eine Reihe von Diagrammen mit Leistungsmetriken. Wählen Sie eines dieser Diagramme aus, um die Daten im Azure-Portal im Metrik-Explorer anzuzeigen. Hier können Sie die Werte mehrerer Metriken im zeitlichen Verlauf als Diagramm darstellen. Sie können die Diagramme interaktiv nutzen oder an ein Dashboard anheften, um sie mit anderen Visualisierungstools anzuzeigen.

- [Protokolle][Logs] enthalten verschiedene Arten von Daten, die in Datensätzen mit unterschiedlichen Eigenschaften für jeden Typ organisiert sind. Ereignisse und Ablaufverfolgungen werden als Protokolle zusammen mit Leistungsdaten gespeichert; ihre Kombination zu Analysezwecken ist möglich. Die in Azure Monitor gesammelten Protokolldaten können mit Abfragen analysiert werden, die die gesammelten Daten schnell abrufen, konsolidieren und analysieren. Protokolle werden in [Log Analytics][LogAnalytics] gespeichert und abgefragt. Sie können Abfragen mit Log Analytics im Azure-Portal erstellen und testen und die Daten dann entweder mit diesen Tools direkt analysieren oder Abfragen zur Verwendung mit Visualisierungen oder Warnungsregeln speichern.

![9][9]

Azure Monitor kann Daten aus vielen verschiedenen Quellen sammeln. Sie können sich das Überwachen von Daten für Ihre Anwendungen in Ebenen vorstellen, die von Ihrer Anwendung über ein Betriebssystem und die Dienste, auf denen sie aufbaut, bis zur Azure-Plattform selbst hinunterreichen. Azure Monitor sammelt Daten aus jeder der folgenden Schichten:

- **Überwachungsdaten zu Anwendungen:** Daten zur Leistung und Funktionalität des von Ihnen geschriebenen Codes, unabhängig von seiner Plattform.
- Überwachungsdaten zum Gast-BS: Daten zum Betriebssystem, unter dem die Anwendung ausgeführt wird. Dieses Betriebssystem kann in Azure, einer anderen Cloud oder lokal ausgeführt werden.
- **Überwachungsdaten zur Azure-Ressource:** Daten zum Betrieb einer Azure-Ressource.
- **Überwachungsdaten zum Azure-Abonnement:** Daten zum Betrieb und zur Verwaltung eines Azure-Abonnements sowie Daten zur Integrität und zum Betrieb von Azure selbst.
- **Überwachungsdaten zu Azure-Mandanten:** Daten zum Betrieb von Azure-Diensten auf Mandantenebene, z. B. Azure Active Directory.
- **Benutzerdefinierte Quellen:** Von lokalen Quellen gesendete Protokolle können ebenfalls eingeschlossen werden. Beispiele hierfür sind lokale Serverereignisse oder die Syslog-Ausgabe von Netzwerkgeräten.

Das Überwachen von Daten ist nur nützlich, wenn dadurch Ihre Einsicht in den Betrieb Ihrer Computerumgebung ausgeweitet wird. Azure Monitor enthält eine Reihe von Features und Tools, die wertvolle Einblicke in Ihre Anwendungen und weitere Ressourcen bieten, von denen sie abhängen. Überwachungslösungen und -features wie Application Insights und Azure Monitor für Container ermöglichen umfassende Einblicke in verschiedene Aspekte Ihrer Anwendung und bestimmter Azure-Dienste.

Überwachungslösungen in Azure Monitor sind Programmpakete, die Einblicke für eine bestimmte Anwendung oder einen bestimmten Dienst liefern. Dazu gehören die Logik zum Sammeln von Überwachungsdaten für die Anwendung oder den Dienst, Abfragen zur Analyse dieser Daten und Ansichten zur Visualisierung. Überwachungslösungen sind bei Microsoft und den Partnern von Microsoft verfügbar und bieten Überwachung für verschiedene Azure-Dienste und andere Anwendungen.

Angesichts dieser vielfältigen erfassten Daten ist es unerlässlich, proaktive Maßnahmen in Bezug auf Ereignisse in Ihrer Umgebung zu ergreifen, bei denen manuelle Abfragen allein nicht ausreichend sind. Warnungen in Azure Monitor informieren Sie proaktiv über kritische Zustände und versuchen potenziell, Korrekturmaßnahmen einzuleiten. Warnungsregeln, die auf Metriken basieren, ermöglichen das Veröffentlichen von Warnungen nahezu in Echtzeit auf der Grundlage von numerischen Werten, während mit auf Protokollen basierenden Regeln komplexe Logik über Daten aus mehreren Quellen hinweg möglich ist. Warnungsregeln in Azure Monitor verwenden Aktionsgruppen, die eindeutige Sätze von Empfängern und Aktionen enthalten, die gemeinsam von mehreren Regeln übergreifend verwendet werden können. Je nach Ihren Anforderungen können Aktionsgruppen Aktionen wie das Verwenden von Webhooks ausführen, die das Auslösen externer Aktionen durch Warnungen bewirken oder die Integration in Ihre ITSM-Tools ermöglichen.

Mit Azure Monitor können außerdem benutzerdefinierte Dashboards erstellt werden. Mit Azure Dashboards können Sie verschiedene Arten von Daten, einschließlich von Metriken und Protokollen, in einem einzelnen Bereich im Azure-Portal kombinieren. Sie können das Dashboard optional gemeinsam mit anderen Azure-Benutzern nutzen. Über die Ausgabe beliebiger Protokollabfragen oder Metrikdiagramme hinaus können Elemente im gesamten Azure Monitor einem Azure-Dashboard hinzugefügt werden. Beispielsweise können Sie ein Dashboard erstellen, das Kacheln kombiniert, die ein Diagramm der Metriken, eine Tabelle mit Aktivitätsprotokollen, ein Nutzungsdiagramm von Application Insights und die Ausgabe einer Protokollabfrage zeigen.

Schließlich stellen Azure Monitor-Daten eine native Quelle für Power BI dar. Power BI ist ein Business Analytics-Dienst, der interaktive Visualisierungen für eine Vielzahl von Datenquellen bereitstellt und eine effektive Möglichkeit darstellt, Daten für andere Personen innerhalb und außerhalb Ihrer Organisation verfügbar zu machen. Sie können Power BI für den automatischen Import von Protokolldaten aus Azure Monitor konfigurieren, um diese zusätzlichen Visualisierungen zu nutzen.

[Azure Network Watcher][NetWatch] bietet Tools für die Überwachung, Diagnose und Anzeige von Metriken sowie die Aktivierung oder Deaktivierung von Protokollen für Ressourcen in einem virtuellen Azure-Netzwerk. Es ist ein breit gefächerter Dienst, der unter anderem die folgenden Funktionen bietet:

- Überwachen der Kommunikation zwischen einer VM und einem Endpunkt
- Anzeigen von Ressourcen in einem virtuellen Netzwerk mit den dazugehörigen Beziehungen
- Diagnostizieren von Problemen bei der Filterung des ein- und ausgehenden Netzwerkdatenverkehrs einer VM
- Diagnostizieren von Problemen beim Netzwerkrouting über eine VM
- Diagnostizieren ausgehender Verbindungen einer VM
- Erfassen von ein- und ausgehenden Paketen einer VM
- Diagnostizieren von Problemen mit einem Gateway eines virtuellen Azure-Netzwerks und Verbindungen
- Bestimmen von relativen Wartezeiten zwischen Azure-Regionen und Internetdienstanbietern
- Anzeigen der Sicherheitsregeln für eine Netzwerkschnittstelle
- Anzeigen von Netzwerkmetriken
- Analysieren des ein- und ausgehenden Datenverkehrs einer Netzwerksicherheitsgruppe
- Anzeigen von Diagnoseprotokollen für Netzwerkressourcen

#### <a name="component-type-workloads"></a>Komponententyp: Arbeitsauslastungen

Workload-Komponenten befinden sich dort, wo auch Ihre tatsächlichen Anwendungen und Dienste sind. Dort verbringen Ihre Anwendungsentwicklungsteams die meiste Zeit.

Die Möglichkeiten für Workloads sind endlos. Im Folgenden finden Sie einige der möglichen Workload-Typen:

**Interne Anwendungen:** Branchenanwendungen sind für Unternehmensaktivitäten von entscheidender Bedeutung. Diese Anwendungen haben einige gemeinsame Merkmale:

- **Interaktiv:** Daten werden eingegeben, und Ergebnisse oder Berichte werden zurückgegeben.
- **Datengesteuert:** Branchenanwendungen sind datenintensiv und greifen häufig auf Datenbanken oder einen anderen Speicher zu.
- **Integriert:** Branchenanwendungen ermöglichen die Integration in andere Systeme innerhalb oder außerhalb der Organisation.

**Websites für Kunden (im Internet oder intern):** Die meisten Internetanwendungen sind Websites. Azure kann eine Website entweder über einen virtuellen IaaS-Computer oder über eine [Azure-Web-Apps][WebApps]-Website (PaaS) ausführen. Azure-Web-Apps können in virtuelle Netzwerke integriert werden, um Web-Apps in einer Spoke-Netzwerkzone bereitzustellen. Für interne Websites muss kein öffentlicher Internetendpunkt verfügbar gemacht werden, weil auf die Ressourcen aus dem privaten virtuellen Netzwerk über Adressen zugegriffen werden kann, die nicht über das Internet geroutet werden können.

**Big Data-Analyse:** Wenn Daten auf größere Volumen hochskaliert werden müssen, ist die Leistung relationaler Datenbanken angesichts der extremen Auslastung oder aufgrund der unstrukturierten Daten möglicherweise schlecht. [Azure HDInsight][HDInsight] ist ein umfassender, verwalteter Open-Source-Analysedienst in der Cloud für Unternehmen. Sie können Open-Source-Frameworks wie Hadoop, Apache Spark, Apache Hive, LLAP, Apache Kafka, Apache Storm und R verwenden. HDInsight unterstützt die Bereitstellung in einem standortbasierten Netzwerk, und die Bereitstellung in einem Cluster in einer Spoke des virtuellen Rechenzentrums ist möglich.

**Ereignisse und Messaging:** Bei [Azure Event Hubs][EventHubs] handelt es sich um eine Big Data-Streamingplattform und einen Ereigniserfassungsdienst. Mit diesem Dienst können Millionen von Ereignissen pro Sekunde empfangen und verarbeitet werden. Er bietet niedrige Latenz und konfigurierbare Aufbewahrungszeiten, wodurch Sie riesige Datenmengen in Azure einspeisen und diese in verschiedenen Anwendungen lesen können. Ein einziger Datenstrom kann sowohl Echtzeit als auch batchbasierte Pipelines unterstützen.

Über [Azure Service Bus][ServiceBus] können Sie einen zuverlässigen Cloudmessagingdienst zwischen Anwendungen und Diensten implementieren. Der Dienst bietet asynchrones Brokermessaging zwischen Client und Server, strukturiertes FIFO-Messaging (First In, First Out) sowie Funktionen zum Veröffentlichen und Abonnieren.

![10][10]

Diese Beispiele beschreiben nicht einmal andeutungsweise die vielfältigen Typen von Workloads, die Sie in Azure erstellen können: Möglich ist alles von einer einfachen Web- und SQL-App bis hin zu aktuellen Entwicklungen in IoT, Big Data, ML, KI und vielem mehr.

### <a name="highly-availability-multiple-virtual-datacenters"></a>Hochverfügbarkeit: mehrere virtuelle Rechenzentren

Bisher ging es in diesem Artikel in erster Linie um den Entwurf eines einzelnen virtuellen Rechenzentrums sowie die grundlegenden Komponenten und Architekturen, die zur Resilienz beitragen. Azure-Funktionen wie der Azure Load Balancer, NVAs, Verfügbarkeitszonen, Verfügbarkeitsgruppen, Skalierungsgruppen und weitere Funktionen ermöglichen es Ihnen, solide SLA-Ebenen in Ihre Produktionsdienste zu integrieren.

Da ein virtuelles Rechenzentrum normalerweise in einer einzelnen Region implementiert wird, kann es anfällig für Ausfälle sein, welche die gesamte Region betreffen. Kunden, die Hochverfügbarkeit benötigen, müssen die Dienste schützen, indem sie dasselbe Projekt in zwei (oder mehr) Implementierungen des virtuellen Rechenzentrums in unterschiedlichen Regionen bereitstellen.

Neben den Vorteilen in Bezug auf SLAs ist der Betrieb mehrerer virtueller Rechenzentren günstig in vielen gängigen Szenarien:

- Regionale oder globale Präsenz Ihrer Endbenutzer oder Partner
- Anforderungen hinsichtlich der Notfallwiederherstellung
- Mechanismus zum Umleiten von Datenverkehr zwischen Rechenzentren aus Auslastungs- oder Leistungsgründen

#### <a name="regionalglobal-presence"></a>Regionale/globale Präsenz

Azure-Rechenzentren befinden sich in vielen Regionen auf der ganzen Welt. Bei der Auswahl mehrerer Azure-Rechenzentren sind zwei zusammenhängende Faktoren zu berücksichtigen: die geografische Entfernung und die Latenz. Bewerten Sie zum Optimieren der Benutzererfahrung die Entfernung zwischen den einzelnen virtuellen Rechenzentren sowie die Entfernung jedes virtuellen Rechenzentrums zu den Endbenutzern.

Eine Azure-Region, in der Ihr virtuelles Rechenzentrum gehostet wird, muss die gesetzlichen Anforderungen des Rechtsraums erfüllen, in dem Ihre Organisation tätig ist.

#### <a name="disaster-recovery"></a>Notfallwiederherstellung

Der Entwurf eines Plans für die Notfallwiederherstellung richtet sich nach den Arten von Workloads und der Möglichkeit, den Zustand dieser Workloads zwischen unterschiedlichen Implementierungen des virtuellen Rechenzentrums zu synchronisieren. Die meisten Kunden wünschen sich im Idealfall einen schnellen Failovermechanismus. Hierfür ist ggf. eine Synchronisierung der Anwendungsdaten zwischen den Bereitstellungen erforderlich, die in mehreren Implementierungen des virtuellen Rechenzentrums ausgeführt werden. Beim Entwerfen von Plänen für die Notfallwiederherstellung sollte aber unbedingt berücksichtigt werden, dass die meisten Anwendungen empfindlich auf die Latenz reagieren, die durch diese Datensynchronisierung verursacht werden kann.

Für die Synchronisierung und Heartbeatüberwachung von Anwendungen in verschiedenen Implementierungen des virtuellen Rechenzentrums ist eine Kommunikation über das Netzwerk erforderlich. Mehrere Implementierungen des virtuellen Rechenzentrums in unterschiedlichen Regionen können wie folgt Weise verbunden werden:

- Hub-zu-Hub Kommunikation, die in Azure Virtual WAN-Hubs in Regionen im selben Virtual WAN integriert ist.
- Über Peering virtueller Netzwerke können Hubs regionsübergreifend verbunden werden.
- Privates ExpressRoute-Peering, wenn die Hubs jeder Implementierung des virtuellen Rechenzentrums mit derselben ExpressRoute-Leitung verbunden sind.
- Mehrere ExpressRoute-Verbindungen, die über Ihren firmeneigenen Backbone und Ihre Implementierungen der virtuellen Rechenzentren mit den ExpressRoute-Leitungen verbunden sind.
- Site-to-Site-VPN-Verbindungen zwischen der Hubzone Ihrer Implementierungen virtueller Rechenzentren in jeder Azure-Region.

Normalerweise stellen Virtual WAN-Hubs, das Peering virtueller Netzwerke oder ExpressRoute-Verbindungen aufgrund ihrer höheren Bandbreite und konsistenten Latenzebenen bei der Übertragung über den Microsoft-Backbone die bevorzugte Art von Netzwerkkonnektivität dar.

Führen Sie Netzwerkqualifizierungstests durch, um die Latenz und Bandbreite dieser Verbindungen zu überprüfen, und entscheiden Sie dann anhand des Ergebnisses, ob eine synchrone oder asynchrone Datenreplikation geeignet ist. Es ist auch wichtig, diese Ergebnisse hinsichtlich des optimalen RTO-Werts (Recovery Time Objective) zu bewerten.

#### <a name="disaster-recovery-diverting-traffic-from-one-region-to-another"></a>Notfallwiederherstellung: Umleiten von Datenverkehr aus einer Region in eine andere

Sowohl [Azure Traffic Manager][azure-traffic-manager] als auch [Azure Front Door][azure-front-door] überprüfen regelmäßig die Dienstintegrität von überwachenden Endpunkten in verschiedenen Implementierungen virtueller Rechenzentren. Wenn für diese Endpunkte ein Fehler auftritt, werden die Daten automatisch an das nächstgelegene virtuelle Rechenzentrum umgeleitet. Traffic Manager leitet Benutzer anhand von Echtzeit-Benutzermessungen und DNS an das nächste (oder während eines Ausfalls an das nächstgelegene) Rechenzentrum weiter. Azure Front Door ist ein Reverseproxy auf mehr als 100 Microsoft-Backbone-Edge-Sites und leitet Benutzer mit Anycast an den nächstgelegenen überwachenden Endpunkt weiter.

### <a name="summary"></a>Zusammenfassung

Ein virtuelles Rechenzentrum ist ein Ansatz, mit dem beim Migrieren von Rechenzentren eine skalierbare Architektur geschaffen wird, welche die Nutzung von Azure-Ressourcen optimiert, die Kosten senkt und die Steuerung des Systems vereinfacht. Das virtuelle Rechenzentrum basiert im Allgemeinen auf Hub-and-Spoke-Netzwerktopologien (wobei entweder das Peering virtueller Netzwerke oder Virtual WAN-Hubs verwendet werden). Gemeinsame Dienste werden im Hub bereitgestellt, während spezifische Anwendungen und Workloads in den Spokes bereitgestellt werden. Darüber hinaus wird im virtuellen Rechenzentrum auch die Struktur von Unternehmensrollen berücksichtigt, indem unterschiedliche Abteilungen, z. B. zentrale IT-Abteilung, DevOps sowie Betrieb und Wartung zusammenarbeiten, während sie ihre jeweiligen Rollen ausfüllen. Das virtuelle Rechenzentrum unterstützt das Migrieren vorhandener lokaler Workloads in Azure, es bietet jedoch auch viele Vorteile für cloudnative Bereitstellungen.

## <a name="references"></a>References

Erfahren Sie mehr über die in diesem Dokument erläuterten Azure-Funktionen.

<!-- markdownlint-disable MD033 -->

|Netzwerkfunktionen | Lastenausgleich | Konnektivität |
| --- | --- | --- |
|[Virtuelle Azure-Netzwerke][virtual-network]</br>[Netzwerksicherheitsgruppen][NSG]</br>[Dienstendpunkte][ServiceEndpoints]</br>[Private Link][PrivateLink]</br>[Benutzerdefinierte Routen][UDR]</br>[Virtuelle Netzwerkgeräte][NVA]:</br>[Öffentliche IP-Adressen][PIP]</br>[Azure DNS][DNS]|[Azure Front Door][azure-front-door]</br>[Azure Load Balancer (L4)][ALB]</br>[Application Gateway (L7)][AppGW]</br>[Azure Traffic Manager][azure-traffic-manager]</br></br></br></br></br> |[Peering virtueller Netzwerke][virtual-network-peering]</br>[Virtuelles privates Netzwerk][VPN]</br>[Virtual WAN][virtual-wan]</br>[ExpressRoute][ExR]</br>[ExpressRoute Direct][ExRD]</br></br></br></br></br>

|Identity | Überwachung | Bewährte Methoden |
| --- | --- | --- |
|[Azure Active Directory][azure-ad]</br>[Multi-Factor Authentication][multi-factor-authentication]</br>[Rollenbasierte Zugriffssteuerung][RBAC]</br>[Azure AD-Standardrollen][Roles]</br></br></br> |[Network Watcher][NetWatch]</br>[Azure Monitor][MonitorOverview]</br>[Log Analytics][LogAnalytics]</br> |[Verwaltungsgruppe][MgmtGrp]</br>[Abonnementverwaltung][subscription-management]</br>[Verwaltung von Ressourcengruppen][RGMgmt]</br>[Einschränkungen für Azure-Abonnements][limits] </br></br></br>|

Sicherheit |Weitere Azure-Dienste | |
|-|-|-|
|[Azure Firewall][AzFW]</br>[Firewall Manager][AzFWMgr]</br>[Application Gateway – WAF][AppGWWAF]</br>[Front Door – WAF][AFDWAF]</br>[Azure DDoS][DDoS]</br>|[Azure Storage (in englischer Sprache)][Storage]</br>[Azure SQL][SQL]</br>[Azure-Web-Apps][WebApps]</br>[Cosmos DB][Cosmos]</br>[HDInsight][HDInsight]|[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]</br>[Azure IoT][IoT]</br>[Azure Machine Learning][machine-learning]|

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie mehr über das [Peering virtueller Netzwerke][virtual-network-peering], die Kerntechnologie von Hub-and-Spoke-Topologien.
- Implementieren Sie [Azure Active Directory][azure-ad], um die [rollenbasierte Zugriffssteuerung][RBAC] zu verwenden.
- Entwickeln Sie ein Modell für die Abonnement- und Ressourcenverwaltung mit rollenbasierter Zugriffssteuerung, welches der Struktur, den Anforderungen und Richtlinien Ihrer Organisation gerecht wird. Die wichtigste Aktivität ist die Planung. Analysieren Sie, wie sich Umstrukturierungen, Fusionen, neue Produktlinien und andere Aspekte auf Ihre ursprünglichen Modelle auswirken, um deren Skalierbarkeit hinsichtlich künftiger Anforderung und des Wachstums sicherzustellen.

<!-- images -->

[0]: ../_images/vdc/networking-vdc-redundant.png "Beispiele für Komponentenüberlappung"
<!-- _1_ >: ../_images/vdc/networking-vdc-high-level.png "Example of hub and spoke VDC" -->
[2]: ../_images/vdc/networking-vdc-cluster.png "Cluster mit Hub und Spokes"
[3]: ../_images/vdc/networking-vdc-spoke-to-spoke.png "Spoke-zu-Spoke"
[4]: ../_images/vdc/networking-vdc-block-level-diagram.png "Blockebenenabbildung des virtuellen Rechenzentrums"
[5]: ../_images/vdc/networking-vdc-users-groups-subscriptions.png "Benutzer, Gruppen, Abonnements und Projekte"
[6]: ../_images/vdc/networking-vdc-infrastructure.png "Abbildung der Infrastruktur"
[7]: ../_images/vdc/networking-vdc-perimeter.png "Abbildung der Infrastruktur"
[8]: ../_images/vdc/networking-vdc-perimeter-peering.png "Peering virtueller Netzwerke und Umkreisnetzwerke"
[9]: ../_images/vdc/networking-vdc-monitoring.png "Diagramm zu Azure Monitor"
[10]: ../_images/vdc/networking-vdc-workloads.png "Diagramm zu Workloads"
[11]: ../_images/vdc/networking-vdc-brief-flat.png "Beispiel für ein flaches Netzwerk"
[12]: ../_images/vdc/networking-vdc-brief-mesh.png "Beispiel für ein vermaschtes Netzwerk"
[13]: ../_images/vdc/networking-vdc-brief-hub.png "Beispiel für ein Hub-and-Spoke-VDC"
[14]: ../_images/vdc/networking-vdc-brief-vwan.png "Beispiel für ein Virtual WAN-VDC"

<!-- links -->

[limits]: https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[virtual-network]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/security-overview
[PrivateLink]: https://docs.microsoft.com/azure/private-link/private-link-overview
[PrivateLinkSvc]: https://docs.microsoft.com/azure/private-link/private-link-service-overview
[ServiceEndpoints]: https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[virtual-network-peering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[multi-factor-authentication]: https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks
[azure-ad]: https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[virtual-wan]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[AzFWMgr]: https://docs.microsoft.com/azure/firewall-manager/overview
[Organize]: ../ready/azure-setup-guide/organize-resources.md
[MgmtGrp]: https://docs.microsoft.com/azure/governance/management-groups/overview
[subscription-management]: ../ready/azure-best-practices/scale-subscriptions.md
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal#what-is-a-resource-group
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[azure-front-door]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/web-application-firewall/afds/afds-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/overview
[AppGWWAF]: https://docs.microsoft.com/azure/web-application-firewall/ag/ag-overview
[MonitorOverview]: https://docs.microsoft.com/azure/networking/networking-overview#monitor
[AzureMonitor]: https://docs.microsoft.com/azure/azure-monitor/overview
[Metrics]: https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-metrics
[Logs]: https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-logs
[LogAnalytics]: https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-portal
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDInsight]: https://docs.microsoft.com/azure/hdinsight/hdinsight-overview
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-about
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[azure-traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
[Storage]: https://docs.microsoft.com/azure/storage/common/storage-introduction
[SQL]: https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview
[Cosmos]: https://docs.microsoft.com/azure/cosmos-db/introduction
[IoT]: https://docs.microsoft.com/azure/iot-fundamentals/iot-introduction
[machine-learning]: https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml
