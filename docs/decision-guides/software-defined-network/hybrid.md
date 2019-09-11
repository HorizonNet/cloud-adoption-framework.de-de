---
title: 'Softwaredefiniertes Netzwerk: Hybrides Netzwerk'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erläuterung, wie hybride Netzwerke es Ihren virtuellen Cloudnetzwerken ermöglichen, sich mit lokalen Ressourcen zu verbinden.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 94e285f59442b6632209e1cd6a76c39cfccd337b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837856"
---
# <a name="software-defined-networking-hybrid-network"></a>Softwaredefiniertes Netzwerk: Hybrides Netzwerk

Die hybride Cloud-Netzwerkarchitektur ermöglicht in virtuellen Netzwerken, auf Ihre lokalen Ressourcen und Dienste zuzugreifen und umgekehrt. Dabei wird eine dedizierte WAN-Verbindung wie ExpressRoute oder eine andere Verbindungsmethode zum direkten Verbinden der Netzwerke verwendet.

![Hybrides Netzwerk](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/expressroute.png)

Aufbauend auf der cloudnativen virtuellen Netzwerkarchitektur wird ein hybrides virtuelles Netzwerk bei seiner ersten Erstellung isoliert. Das Hinzufügen von Konnektivität zur lokalen Umgebung gewährt den ein- und ausgehenden Zugriff auf das lokale Netzwerk, obwohl alle anderen eingehenden Datenströme, die auf Ressourcen im virtuellen Netzwerk abzielen, ausdrücklich zugelassen werden müssen. Sie können die Verbindung mithilfe virtueller Firewallgeräte und Routingregeln schützen, um den Zugriff einzuschränken. Sie können auch genau festlegen, auf welche Dienste in den beiden Netzwerken zugegriffen werden kann, indem Sie cloudnative Routingfunktionen verwenden oder virtuelle Netzwerkappliances (NVAs) zur Verwaltung des Datenverkehrs bereitstellen.

Obwohl die hybride Netzwerkarchitektur VPN-Verbindungen unterstützt, werden dedizierte WAN-Verbindungen wie ExpressRoute aufgrund höherer Leistung und erhöhter Sicherheit bevorzugt.

## <a name="hybrid-assumptions"></a>Annahmen für hybride virtuelle Netzwerke

Für die Bereitstellung eines hybriden virtuellen Netzwerks wird Folgendes angenommen:

- Ihre IT-Sicherheitsteams haben die lokalen und cloudbasierten Netzwerksicherheitsrichtlinien abgestimmt, um sicherzustellen, dass cloudbasierte virtuelle Netzwerke vertrauenswürdig sind und direkt mit lokalen Systemen kommunizieren können.
- Ihre cloudbasierten Workloads erfordern Zugriff auf Speicher, Anwendungen und Dienste, die in Ihren lokalen oder Drittanbieternetzwerken gehostet werden, oder Ihre Benutzer oder Anwendungen in Ihren lokalen Umgebungen benötigen Zugriff auf in der Cloud gehostete Ressourcen.
- Sie müssen bestehende Anwendungen und Dienste migrieren, die von lokalen Ressourcen abhängen, möchten aber keine Ressourcen für eine Neuentwicklung aufwenden, um diese Abhängigkeiten zu beseitigen.
- Die Verbindung Ihrer lokalen Netzwerke mit Cloudressourcen über VPN oder dediziertes WAN wird nicht durch Unternehmensrichtlinien, Datenhoheitsanforderungen oder andere regulatorische Complianceprobleme verhindert.
- Ihre Workloads erfordern entweder nicht mehrere Abonnements, um die Beschränkungen für im Rahmen des Abonnements verfügbare Ressourcen zu umgehen, oder Ihre Workloads umfassen mehrere Abonnements, erfordern aber keine zentrale Verwaltung der Konnektivität oder gemeinsamen Dienste, die von auf mehrere Abonnements verteilten Ressourcen genutzt werden.

Ihr für den Umstieg auf die Cloud zuständiges Team muss die folgenden Aspekte berücksichtigen, wenn die Implementierung einer hybriden virtuellen Netzwerkarchitektur erwogen wird:

- Durch die Verbindung von lokalen Netzwerken mit Cloudnetzwerken steigt die Komplexität Ihrer Sicherheitsanforderungen. Beide Netzwerke müssen vor externen Schwachstellen und unbefugtem Zugriff von beiden Seiten der hybriden Umgebung geschützt werden.
- Die Skalierung der Anzahl und Größe der Workloads innerhalb einer hybriden Cloudumgebung kann die Verwaltung des Routings und Datenverkehrs erheblich komplexer machen.
- Sie müssen kompatible Verwaltungs- und Zugriffssteuerungsrichtlinien entwickeln, um unternehmensweit konsistente Governance zu gewährleisten.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zu Hybridnetzwerken in Azure finden Sie hier:

- [Referenzarchitektur für hybride Netzwerke](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute). Hybride virtuelle Azure-Netzwerke verwenden entweder eine ExpressRoute-Leitung oder Azure VPN, um Ihr virtuelles Netzwerk mit den vorhandenen, nicht von Azure gehosteten IT-Ressourcen Ihrer Organisation zu verbinden. In diesem Artikel werden die Optionen für die Erstellung eines hybriden Netzwerks in Azure erörtert.
