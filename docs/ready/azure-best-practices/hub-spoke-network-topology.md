---
title: Hub-and-Spoke-Netzwerktopologie
description: Enthält eine Beschreibung der Hub-and-Spoke-Netzwerktopologie zur effizienteren Verwaltung gemeinsamer Kommunikations- oder Sicherheitsanforderungen.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
ms.custom: virtual-network
ms.openlocfilehash: 7e5512cba033adca5c3e88be265d45b5f8bc8f3c
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621421"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs -->

# <a name="hub-and-spoke-network-topology"></a>Hub-and-Spoke-Netzwerktopologie

_Hub-and-Spoke_ ist ein Netzwerkmodell für eine effizientere Verwaltung gemeinsamer Kommunikations- oder Sicherheitsanforderungen. Es hilft auch dabei, Azure-Abonnementeinschränkungen zu vermeiden. Dieses Modell berücksichtigt die folgenden Punkte:

- **Kosteneinsparungen und Effizienz der Verwaltung.** Zentralisierung von Diensten, die von mehreren Workloads, z.B. Network Virtual Appliances (NVAs) und DNS-Servern an einem zentralen Standort gemeinsam genutzt werden können. Auf diese Weise kann die IT-Abteilung redundante Ressourcen und den Verwaltungsaufwand minimieren.
- **Umgehen von Abonnementgrenzen.** Große cloudbasierte Workloads können den Einsatz von mehr Ressourcen erfordern, als in einem einzelnen Azure-Abonnements zulässig ist. Durch ein Peering virtueller Netzwerke für eine Workload aus verschiedenen Abonnements zu einem zentralen Hub können diese Grenzwerte umgangen werden. Weitere Informationen finden Sie unter [Grenzwerte für Azure-Abonnements](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits).
- **Trennung von Zuständigkeiten.** Sie können einzelne Workloads zwischen zentralen IT-Teams und für Workloads zuständige Teams bereitstellen.

Kleinere Cloudumgebungen profitieren möglicherweise nicht von der zusätzlichen Struktur und den Funktionen, die dieses Modell bietet. Für größere Cloudeinführungsaktivitäten sollte jedoch die Implementierung einer Hub-and-Spoke-Architektur in Erwägung gezogen werden, wenn für sie bereits die oben aufgeführten Bedenken gelten.

> [!NOTE]
> Die Website für Azure-Referenzarchitekturen enthält Beispielvorlagen, die Sie als Grundlage für die Implementierung Ihrer eigenen Hub-and-Spoke-Netzwerke verwenden können:
>
> - [Implementieren einer Hub-and-Spoke-Netzwerktopologie in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementieren einer Hub-and-Spoke-Netzwerktopologie mit gemeinsamen Diensten in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Übersicht

![Beispiele zur Hub-and-Spoke-Netzwerktopologie][1]

Wie in der Abbildung gezeigt, unterstützt Azure zwei Arten von Hub-and-Spoke-Entwürfen. Kommunikation, freigegebene Ressourcen und zentralisierte Sicherheitsrichtlinien („virtueller Netzwerkhub“ im Diagramm) oder ein virtueller WAN-Typ („Virtual WAN“ im Diagramm) für umfassende Kommunikation zwischen Branches oder zwischen einem Branch und Azure werden unterstützt.

Ein Hub ist eine zentrale Netzwerkzone, die den ein- oder ausgehenden Datenverkehr zwischen Zonen steuert und überprüft: im Internet, lokal und in den Spokes. Die Hub-Spoke-Topologie stellt für Ihre IT-Abteilung eine effektive Möglichkeit zum Erzwingen von Sicherheitsrichtlinien an einem zentralen Ort dar. Außerdem verringert sie das Risiko von Fehlkonfigurationen und Offenlegungen.

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

Eine einzelne Hub-and-Spoke-Implementierung kann auf eine große Anzahl von Spokes hochskaliert werden. Dabei gelten jedoch wie bei jedem IT-System gewisse Plattformbeschränkungen. Die Hub-Bereitstellung ist an ein bestimmtes Azure-Abonnement gebunden. Beispielsweise kann eine maximale Anzahl von Peerings in virtuellen Netzwerken gelten. Weitere Informationen finden Sie unter [Einschränkungen für Azure-Abonnements und Dienste, Kontingente und Einschränkungen](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits).

In Fällen, in denen diese Beschränkungen ggf. ein Problem darstellen, kann die Architektur weiter hochskaliert werden, indem das Modell von einem einzelnen Hub und Spoke auf ein Cluster von Hubs und Spokes erweitert wird. Mehrere Hubs in mindestens einer Azure-Region können mithilfe von Peering in virtuellen Netzwerken, ExpressRoute, Virtual WAN oder einem Site-to-Site-VPN miteinander verbunden werden.

![Cluster mit Hubs und Spokes][2]

Die Einführung von mehreren Hubs erhöht die Kosten und den Verwaltungsaufwand für das System. Dies lässt sich nur durch Skalierbarkeit, Systemeinschränkungen oder Redundanz und die regionale Replikation zum Erzielen von Leistung für Benutzer oder Notfallwiederherstellung rechtfertigen. In Szenarien, die mehrere Hubs erfordern, sollten alle Hubs die gleichen Dienste anbieten, um die Vorgänge nicht zu erschweren.

## <a name="interconnection-between-spokes"></a>Verbindung zwischen Spokes

Innerhalb eines einzelnen Spokes ist es möglich, komplexe Workloads mit mehreren Ebenen zu implementieren. Sie können Konfigurationen mit mehreren Ebenen implementieren, indem Sie Subnetze (eines für jede Ebene) im selben virtuellen Netzwerk verwenden und Netzwerksicherheitsgruppen einsetzen, um die Datenflüsse zu filtern.

Ein Architekt möchte vielleicht eine Workload mit mehreren Ebenen in mehreren virtuellen Netzwerken bereitstellen. Mittels Peering in virtuellen Netzwerken können Spokes Verbindungen mit anderen Spokes im gleichen Hub oder in anderen Hubs herstellen.

Ein typisches Beispiel für dieses Szenario ist die Platzierung von Anwendungsverarbeitungsservern in einem Spoke oder virtuellen Netzwerk. Die Datenbank wird dann in einem anderen Spoke oder virtuellen Netzwerk bereitgestellt. In diesem Fall ist es einfach, die Spokes mittels Peering in virtuellen Netzwerken zu verbinden und das Durchlaufen des Hubs dabei zu vermeiden. Die Lösung besteht darin, Architektur und Sicherheit sorgfältig zu überprüfen, um sicherzustellen, dass durch die Umgehung des Hubs keine wichtigen Sicherheits- oder Überwachungspunkte umgangen werden, die nur im Hub vorhanden sind.

![Spokes, die eine Verbindung untereinander und mit einem Hub herstellen][3]

Spokes können auch mit einem Spoke verbunden werden, der als Hub fungiert. Bei diesem Ansatz wird eine Hierarchie mit zwei Ebenen erstellt: Der Spoke auf der höheren Ebene (Ebene 0) wird der Hub der unteren Spokes (Stufe 1) in der Hierarchie. Die Spokes einer Hub-and-Spoke-Implementierung eines virtuellen Rechenzentrums sind zum Weiterleiten des Datenverkehrs an den zentralen Hub erforderlich, damit der Datenverkehr an sein Ziel im lokalen Netzwerk oder im öffentlichen Internet geleitet werden kann. Eine Architektur mit zwei Hubebenen führt komplexes Routing ein, das die Vorteile einer einfachen Hub-and-Spoke-Beziehung aufhebt.

<!-- images -->

[1]: ../../_Images/azure-best-practices/network-hub-spoke-high-level.png "Allgemeines Beispiel für Hub-and-Spoke"
[2]: ../../_Images/azure-best-practices/network-hub-spokes-cluster.png "Cluster mit Hubs und Spokes"
[3]: ../../_Images/azure-best-practices/network-spoke-to-spoke.png "Spoke-zu-Spoke"
