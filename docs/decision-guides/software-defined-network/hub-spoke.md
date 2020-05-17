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
ms.openlocfilehash: f3291bb1a5ef114b2ae790bb1a3c82eaf382c37e
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215125"
---
# <a name="software-defined-networking-hub-and-spoke"></a>Softwaredefiniertes Netzwerk: Hub-and-Spoke-Modell

Im Hub-and-Spoke-Netzwerkmodell wird Ihre auf Azure basierende Cloud-Netzwerkinfrastruktur in mehreren verbundenen virtuellen Netzwerken organisiert. Mithilfe dieses Modells können Sie gängige Kommunikations- oder Sicherheitsanforderungen effizienter bewältigen und mögliche Einschränkungen des Abonnements berücksichtigen.

Im Hub-and-Spoke-Modell ist der _Hub_ ein virtuelles Netzwerk, das als Zentrale für die Verwaltung externer Konnektivitäts- und Hostingdienste dient, die von mehreren Workloads genutzt werden. Die _Spokes_ sind virtuelle Netzwerke, die Workloads hosten und sich über [Peering virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) mit dem zentralen Hub verbinden.

Der gesamte Datenverkehr, der in die oder aus den Spoke-Netzwerken der Workload geleitet wird, wird über das Hub-Netzwerk geleitet, wo er weitergeleitet, inspiziert oder anderweitig von zentral verwalteten IT-Regeln oder -Prozessen verwaltet werden kann.

Dieses Modell zielt darauf ab, die folgenden Probleme zu lösen:

- **Kosteneinsparungen und Effizienz der Verwaltung.** Zentralisierung von Diensten, die von mehreren Workloads, z.B. Network Virtual Appliances (NVAs) und DNS-Servern an einem zentralen Standort gemeinsam genutzt werden können. Auf diese Weise kann die IT-Abteilung redundante Ressourcen und den Verwaltungsaufwand für mehrere Workloads minimieren.
- **Überwinden von Abonnementgrenzen**. Große cloudbasierte Workloads können den Einsatz von mehr Ressourcen erfordern, als in einem einzelnen Azure-Abonnements zulässig ist. Durch ein Peering virtueller Netzwerke für eine Workload aus verschiedenen Abonnements zu einem zentralen Hub können diese Grenzwerte umgangen werden. Weitere Informationen finden Sie unter [Grenzwerte für Azure-Netzwerke](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#networking-limits).
- **Trennung von Zuständigkeiten.** Die Fähigkeit, einzelne Workloads zwischen zentralen IT-Teams und Workloadteams bereitzustellen.

Das folgende Diagramm zeigt eine exemplarische Hub-and-Spoke-Architektur mit zentral verwalteter Hybridkonnektivität.

![Architektur für Hub-and-Spoke-Netzwerk](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

Die Hub-and-Spoke-Architektur wird häufig zusammen mit der hybriden Netzwerkarchitektur verwendet und bietet eine zentral verwaltete Verbindung mit Ihrer lokalen Umgebung, die von mehreren Workloads gemeinsam genutzt wird. In diesem Szenario durchläuft der gesamte Datenverkehr zwischen den Workloads und den lokalen Standorten den Hub, wo er verwaltet und geschützt werden kann.

## <a name="hub-and-spoke-assumptions"></a>Annahmen für das Hub-and-Spoke-Modell

Für die Implementieren einer virtuellen Netzwerkarchitektur gemäß Hub-and-Spoke-Modell wird Folgendes angenommen:

- Ihre Cloudbereitstellungen umfassen Workloads, die in separaten Arbeitsumgebungen wie Entwicklung, Test und Produktion gehostet werden, und die alle auf einer Reihe von gemeinsamen Diensten wie DNS oder Verzeichnisdiensten basieren.
- Ihre Workloads müssen nicht miteinander kommunizieren, sondern haben gemeinsame Anforderungen an die externe Kommunikation und gemeinsam genutzte Dienste.
- Ihre Workloads erfordern mehr Ressourcen, als innerhalb eines einzelnen Azure-Abonnements verfügbar sind.
- Sie müssen für Workloads zuständigen Teams delegierte Verwaltungsrechte für ihre eigenen Ressourcen zur Verfügung stellen und gleichzeitig die zentrale Sicherheitskontrolle über die externe Konnektivität beibehalten.

## <a name="global-hub-and-spoke"></a>Globales Hub-and-Spoke-Modell

Hub-and-Spoke-Architekturen werden häufig mit virtuellen Netzwerken implementiert, die in derselben Azure-Region bereitgestellt werden, um die Wartezeiten zwischen Netzwerken zu minimieren. Große Unternehmen mit globaler Reichweite müssen jedoch möglicherweise Workloads in mehreren Regionen bereitstellen, um Verfügbarkeit, Notfallwiederherstellung oder die Erfüllung gesetzlicher Anforderungen zu gewährleisten. Das Hub-and-Spoke-Modell kann ein [globalen Peerings virtueller Netzwerke](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) in Azure nutzen, um die zentralisierte Verwaltung und die gemeinsamen Dienste regionsübergreifend erweitern, um die über die ganze Welt verteilten Workloads zu unterstützen.

## <a name="learn-more"></a>Weitere Informationen

Beispiele für Referenzarchitekturen, in denen gezeigt wird, wie Hub-and-Spoke-Netzwerke in Azure implementiert werden, finden Sie unter:

- [Implementieren einer Hub-and-Spoke-Netzwerktopologie in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
- [Implementieren einer Hub-and-Spoke-Netzwerktopologie mit gemeinsamen Diensten in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
