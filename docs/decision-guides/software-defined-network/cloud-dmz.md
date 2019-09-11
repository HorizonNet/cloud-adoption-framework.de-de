---
title: 'Softwaredefiniertes Netzwerk: Cloud-DMZ'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diese Netzwerkarchitektur ermöglicht einen eingeschränkten Zugriff zwischen Ihren lokalen und cloudbasierten Netzwerken.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 6dfee69d20afac27c735f2ff77abbadc2816ca26
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837504"
---
# <a name="software-defined-networking-cloud-dmz"></a>Softwaredefiniertes Netzwerk: Cloud-DMZ

Die Netzwerkarchitektur von Cloud-DMZ ermöglicht einen eingeschränkten Zugriff zwischen Ihren lokalen und cloudbasierten Netzwerken, indem ein virtuelles privates Netzwerk (VPN) zur Verbindung der Netzwerke verwendet wird. Obwohl ein DMZ-Modell häufig verwendet wird, wenn Sie den externen Zugriff auf ein Netzwerk sichern möchten, ist die hier vorgestellte Cloud-DMZ-Architektur speziell für den sicheren Zugriff auf das lokale Netzwerk aus cloudbasierten Ressourcen gedacht und umgekehrt.

![Sichere Hybrid-Netzwerkarchitektur](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/images/dmz-private.png)

Diese Architektur ist so ausgelegt, dass Szenarien unterstützt werden, in denen Ihr Unternehmen mit der Integration von cloudbasierten Workloads in lokale Workloads beginnen möchte, aber möglicherweise noch keine vollständig ausgereiften Sicherheitsrichtlinien für die Cloud hat oder keine sichere dedizierte WAN-Verbindung zwischen den beiden Umgebungen hergestellt wurde. Daher sollten Cloudnetzwerke wie eine DMZ behandelt werden, um zu gewährleisten, dass lokale Dienste sicher sind.

Die DMZ stellt virtuelle Netzwerkappliances (NVAs) bereit, die Sicherheitsfunktionen wie Firewalls und Paketüberprüfung implementieren. Datenverkehr zwischen lokalen und cloudbasierten Anwendungen oder Diensten muss die DMZ passieren, wo er überprüft werden kann. VPN-Verbindungen und die Regeln, die festlegen, welcher Datenverkehr durch das DMZ-Netzwerk geleitet werden darf, werden von IT-Sicherheitsteams streng kontrolliert.

## <a name="cloud-dmz-assumptions"></a>Annahmen für Cloud-DMZ

Das Bereitstellen einer Cloud DMZ-Architektur beinhaltet die folgenden Annahmen:

- Ihre Sicherheitsteams haben die lokalen und cloudbasierten Sicherheitsanforderungen und -richtlinien noch nicht vollständig aufeinander abgestimmt.
- Ihre cloudbasierten Workloads erfordern den Zugriff auf eine eingeschränkte Teilmenge von Diensten, die in Ihren lokalen oder Drittanbieternetzwerken gehostet werden, oder Benutzer oder Anwendungen in Ihren lokalen Umgebungen benötigen eingeschränkten Zugriff auf in der Cloud gehostete Ressourcen.
- Die Implementierung eines VPN zwischen Ihren lokalen Netzwerken und dem Cloudanbieter wird nicht durch unternehmensinterne Richtlinien, regulatorische Anforderungen oder technische Kompatibilitätsprobleme erschwert.
- Ihre Workloads erfordern entweder nicht mehrere Abonnements, um die Ressourcenbeschränkungen für Abonnements zu umgehen, oder sie umfassen mehrere Abonnements, erfordern aber keine zentrale Verwaltung der Konnektivität oder gemeinsamen Dienste, die von auf mehrere Abonnements verteilten Ressourcen genutzt werden.

Ihr für den Umstieg auf die Cloud zuständiges Team muss die folgenden Aspekte berücksichtigen, wenn die Implementierung einer virtuellen Netzwerkarchitektur mit Cloud-DMZ erwogen wird:

- Durch die Verbindung von lokalen Netzwerken mit Cloudnetzwerken steigt die Komplexität Ihrer Sicherheitsanforderungen. Auch wenn Verbindungen zwischen Cloudnetzwerken und der lokalen Umgebung geschützt ist, müssen Sie dennoch dafür sorgen, dass Cloudressourcen geschützt sind. Alle öffentlichen IP-Adressen, die für den Zugriff auf cloudbasierte Workloads erstellt werden, müssen ordnungsgemäß mit einer [öffentlichen DMZ](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz) oder [Azure Firewall](/azure/firewall) gesichert werden.
- Die Cloud-DMZ-Architektur wird häufig als Ausgangspunkt verwendet, während die Konnektivität weiter abgesichert und die Sicherheitsrichtlinien zwischen lokalen und Cloudnetzwerken abgestimmt werden, was eine breitere Einführung einer vollständig hybriden Netzwerkarchitektur ermöglicht. Dies kann jedoch auch für isolierte Bereitstellungen mit spezifischen Sicherheits-, Identitäts- und Konnektivitätsanforderungen gelten, die der Cloud-DMZ-Ansatz erfüllt.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zur Implementierung einer Cloud-DMZ in Azure finden Sie hier:

- [Implementieren einer DMZ zwischen Azure und Ihrem lokalen Rechenzentrum](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid). In diesem Artikel wird das Implementieren einer sicheren hybriden Netzwerkarchitektur in Azure erörtert.
