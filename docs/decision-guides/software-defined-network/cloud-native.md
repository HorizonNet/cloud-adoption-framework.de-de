---
title: 'Softwaredefiniertes Netzwerk: Cloudnativ'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über cloudnative virtuelle Netzwerke zu informieren, die erforderlich sind, um virtuelle Computer in der Cloud bereitzustellen.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 250f78bb0287e30615aee4b2cfb1234823197f56
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222672"
---
# <a name="software-defined-networking-cloud-native"></a>Softwaredefiniertes Netzwerk: Cloudnativ

Ein cloudnatives virtuelles Netzwerk ist erforderlich, wenn IaaS-Ressourcen wie virtuelle Computer auf einer Cloudplattform bereitgestellt werden. Der Zugriff auf virtuelle Netzwerke aus mit dem Web vergleichbaren externen Quellen muss explizit bereitgestellt werden. Diese Arten virtueller Netzwerke unterstützen die Erstellung von Subnetzen, Routingregeln sowie von virtuellen Geräten für Firewallfunktionen und Datenverkehrsverwaltung.

Ein cloudnatives virtuelles Netzwerk weist keine Abhängigkeiten von den lokalen oder anderen Nicht-Cloudressourcen Ihrer Organisation auf, um die in der Cloud gehosteten Workloads zu unterstützen. Alle benötigten Ressourcen werden entweder im virtuellen Netzwerk selbst oder über verwaltete PaaS-Angebote bereitgestellt.

## <a name="cloud-native-assumptions"></a>Cloudnative Annahmen

Für die Bereitstellung eines cloudnativen virtuellen Netzwerks wird Folgendes angenommen:

- Die Workloads, die Sie im virtuellen Netzwerk bereitstellen, weisen keine Abhängigkeiten von Anwendungen oder Diensten auf, auf die nur innerhalb Ihres lokalen Netzwerks zugegriffen werden kann. Sofern sie keine Endpunkte bereitstellen, auf die über das öffentliche Internet zugegriffen wird, sind Anwendungen und Dienste, die intern lokal gehostet werden, nicht von Ressourcen nutzbar, die auf einer Cloudplattform gehostet werden.
- Die Identitätsverwaltung und Zugriffssteuerung Ihres Workloads hängt von den Identitätsdiensten der Cloudplattform oder IaaS-Servern ab, die in Ihrer Cloudumgebung gehostet werden. Sie müssen sich nicht direkt mit Identitätsdiensten verbinden, die lokal oder an anderen externen Standorten gehostet werden.
- Ihre Identitätsdienste müssen eimaliges Anmelden (SSO) bei lokalen Verzeichnissen nicht unterstützen.

Cloudnative virtuelle Netzwerke weisen keine externen Abhängigkeiten auf. Dadurch sind sie einfach bereitzustellen und zu konfigurieren, und deshalb ist diese Architektur oft die beste Wahl für Experimente oder andere kleinere, in sich geschlossene oder schnell iterierende Bereitstellungen.

Zusätzliche Aspekte, die Ihr für den Umstieg auf die Cloud zuständiges Team berücksichtigen sollte, wenn es um den Einsatz einer cloudnativen virtuellen Netzwerkarchitektur geht, sind u.a.:

- Bestehende Workloads, die für den Betrieb in einem lokalen Rechenzentrum konzipiert sind, müssen möglicherweise umfassend angepasst werden, um in den Genuss cloudbasierter Funktionen, wie z.B. von Speicher- oder Authentifizierungsdiensten, zu kommen.
- Cloudnative Netzwerke werden ausschließlich mithilfe der von der Cloudplattform bereitgestellten Verwaltungstools verwaltet, weshalb es im Laufe der Zeit zu Abweichungen von Ihren bestehenden IT-Standards in Bezug auf Verwaltung und Richtlinien kommen kann.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu cloudnativen virtuellen Netzwerken in Azure finden Sie hier:

- [Azure Virtual Network: Anleitungen](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm). Neu erstellte Azure Virtual Networks sind standardmäßig cloudnativ. Befolgen Sie diese Anleitungen bei der Planung des Entwurfs und der Bereitstellung Ihrer virtuellen Netzwerke.
- [Grenzwerte für Abonnements: Netzwerk](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=/azure/virtual-network/toc.json#networking-limits) aus. Die einzelnen virtuellen Netzwerke und die verbundenen Ressourcen befinden sich jeweils in einem einzelnen Abonnement. Diese Ressourcen unterliegen Abonnementgrenzen.
