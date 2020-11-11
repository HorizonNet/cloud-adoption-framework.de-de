---
title: 'Softwaredefiniertes Netzwerk: Hub-and-Spoke-Modell'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Ihre Netzwerkinfrastruktur beim Hub-and-Spoke-Netzwerkmodell in mehreren verbundenen virtuellen Netzwerken organisiert wird.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9b564c5e73afe2968b928c78a3cc1dd4b9ea3028
ms.sourcegitcommit: 2c949c44008161e50b91ffd3f01f6bf32da2d4d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2020
ms.locfileid: "94432583"
---
# <a name="software-defined-networking-hub-and-spoke"></a>Softwaredefiniertes Netzwerk: Hub-and-Spoke-Modell

Im Hub-and-Spoke-Netzwerkmodell wird Ihre auf Azure basierende Cloud-Netzwerkinfrastruktur in mehreren verbundenen virtuellen Netzwerken organisiert. Mithilfe dieses Modells können Sie gängige Kommunikations- oder Sicherheitsanforderungen effizienter bewältigen und mögliche Einschränkungen des Abonnements berücksichtigen.

Im Hub-and-Spoke-Modell ist der *Hub* ein virtuelles Netzwerk, das als Zentrale für die Verwaltung externer Konnektivitäts- und Hostingdienste dient, die von mehreren Workloads genutzt werden. Die *Spokes* sind virtuelle Netzwerke, die Workloads hosten und sich über [Peering virtueller Netzwerke](/azure/virtual-network/virtual-network-peering-overview) mit dem zentralen Hub verbinden.

Der gesamte Datenverkehr, der in die oder aus den Spoke-Netzwerken der Workload geleitet wird, wird über das Hub-Netzwerk geleitet, wo er weitergeleitet, inspiziert oder anderweitig von zentral verwalteten IT-Regeln oder -Prozessen verwaltet werden kann.

Mit diesem Modell sollen die folgenden Bedenken ausgeräumt werden:

- **Kosteneinsparungen und Effizienz der Verwaltung.** Zentralisierung von Diensten, die von mehreren Workloads, z.B. Network Virtual Appliances (NVAs) und DNS-Servern an einem zentralen Standort gemeinsam genutzt werden können. Auf diese Weise kann die IT-Abteilung redundante Ressourcen und den Verwaltungsaufwand für mehrere Workloads minimieren.
- **Überwinden von Abonnementgrenzen**. Große cloudbasierte Workloads können den Einsatz von mehr Ressourcen erfordern, als in einem einzelnen Azure-Abonnements zulässig ist. Durch ein Peering virtueller Netzwerke für eine Workload aus verschiedenen Abonnements zu einem zentralen Hub können diese Grenzwerte umgangen werden. Weitere Informationen finden Sie unter [Grenzwerte für Azure-Netzwerke](/azure/azure-resource-manager/management/azure-subscription-service-limits#networking-limits).
- **Trennung von Zuständigkeiten.** Die Fähigkeit, einzelne Workloads zwischen zentralen IT-Teams und Workloadteams bereitzustellen.

Das folgende Diagramm zeigt eine exemplarische Hub-and-Spoke-Architektur mit zentral verwalteter Hybridkonnektivität.

![Architektur für Hub-and-Spoke-Netzwerk](/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

Die Hub-and-Spoke-Architektur wird häufig zusammen mit der hybriden Netzwerkarchitektur verwendet und bietet eine zentral verwaltete Verbindung mit Ihrer lokalen Umgebung, die von mehreren Workloads gemeinsam genutzt wird. In diesem Szenario durchläuft der gesamte Datenverkehr zwischen den Workloads und den lokalen Standorten den Hub, wo er verwaltet und geschützt werden kann.

## <a name="hub-and-spoke-assumptions"></a>Annahmen für das Hub-and-Spoke-Modell

Für die Implementieren einer virtuellen Netzwerkarchitektur gemäß Hub-and-Spoke-Modell wird Folgendes angenommen:

- Ihre Cloudbereitstellungen umfassen Workloads, die in separaten Arbeitsumgebungen wie Entwicklung, Test und Produktion gehostet werden, und die alle auf einer Reihe von gemeinsamen Diensten wie DNS oder Verzeichnisdiensten basieren.
- Ihre Workloads müssen nicht miteinander kommunizieren, sondern haben gemeinsame Anforderungen an die externe Kommunikation und gemeinsam genutzte Dienste.
- Ihre Workloads erfordern mehr Ressourcen, als innerhalb eines einzelnen Azure-Abonnements verfügbar sind.
- Sie müssen für Workloads zuständigen Teams delegierte Verwaltungsrechte für ihre eigenen Ressourcen zur Verfügung stellen und gleichzeitig die zentrale Sicherheitskontrolle über die externe Konnektivität beibehalten.

## <a name="global-hub-and-spoke"></a>Globales Hub-and-Spoke-Modell

Hub-and-Spoke-Architekturen werden häufig mit virtuellen Netzwerken implementiert, die in derselben Azure-Region bereitgestellt werden, um die Wartezeiten zwischen Netzwerken zu minimieren. Große Organisationen mit globaler Reichweite müssen möglicherweise Workloads in mehreren Regionen bereitstellen, um Verfügbarkeit, Notfallwiederherstellung oder die Erfüllung gesetzlicher Anforderungen zu gewährleisten. Das Hub-and-Spoke-Modell kann ein [globalen Peerings virtueller Netzwerke](/azure/virtual-network/virtual-network-peering-overview) in Azure nutzen, um die zentralisierte Verwaltung und die gemeinsamen Dienste regionsübergreifend erweitern, um die über die ganze Welt verteilten Workloads zu unterstützen.

## <a name="learn-more"></a>Weitere Informationen

Beispiele für Referenzarchitekturen, in denen gezeigt wird, wie Hub-and-Spoke-Netzwerke in Azure implementiert werden, finden Sie unter:

- [Implementieren einer Hub-and-Spoke-Netzwerktopologie in Azure](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
- [Implementieren einer Hub-and-Spoke-Netzwerktopologie mit gemeinsamen Diensten in Azure](/azure/architecture/reference-architectures/hybrid-networking/#hub-spoke-network-topology)
