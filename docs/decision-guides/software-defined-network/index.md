---
title: Leitfaden zur Entscheidungsfindung für softwaredefinierte Netzwerke
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie mit Software-Defined Networking virtualisierte Netzwerke über Software bereitgestellt werden.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: bab6a87a845074f7a1beac7d24baeea0f043b9f8
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88881511"
---
# <a name="software-defined-networking-decision-guide"></a>Leitfaden zur Entscheidungsfindung für softwaredefinierte Netzwerke

Software-Defined Networking (SDN) ist eine Netzwerkarchitektur, die entwickelt wurde, um virtualisierte Netzwerkfunktionen zu ermöglichen, die mithilfe von Software zentral verwaltet, konfiguriert und modifiziert werden können. SDN ermöglicht die Erstellung von cloudbasierten Netzwerken unter Verwendung der virtualisierten Entsprechungen zu physischen Routern, Firewalls und anderen Netzwerkgeräten, die in lokalen Netzwerken verwendet werden. SDN ist entscheidend für die Erstellung sicherer virtueller Netzwerke auf Public Cloud-Plattformen wie Azure.

## <a name="networking-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Netzwerke

![Abbildung der Netzwerkoptionen mit zunehmender Komplexität entsprechend den nachstehenden weiterführenden Links](../../_images/decision-guides/decision-guide-software-defined-network.png)

Wechseln Sie zu: [Nur PaaS](./paas-only.md) | [Cloudnativ](./cloud-native.md) | [Cloud-DMZ](./cloud-dmz.md) | [Hybrid](./hybrid.md) | [Hub-and-Spoke-Modell](./hub-spoke.md) | [Weitere Informationen](#learn-more)

SDN bietet mehrere Optionen mit unterschiedlicher Preisgestaltung und Komplexität. Dieser Leitfaden zur Entscheidungsfindung bietet eine Referenz, um diese Optionen schnell zu personalisieren und so optimal auf spezifische Geschäfts- und Technologiestrategien abzustimmen.

Der Kernpunkt in diesem Leitfaden hängt von mehreren wichtigen Entscheidungen ab, die Ihr Cloudstrategieteam getroffen hat, bevor Entscheidungen zur Netzwerkarchitektur getroffen werden. Am wichtigsten sind dabei Entscheidungen in Bezug auf die [Definition Ihres digitalen Bestands](../../digital-estate/index.md) und das [Abonnementmodell](../subscriptions/index.md), die auch Rückmeldungen zu Entscheidungen im Zusammenhang mit Ihrer Cloudabrechnung und Ihren globalen Marktstrategien erfordern können.

Kleine Bereitstellungen in einer einzelnen Region mit weniger als 1.000 VMs sind weniger wahrscheinlich von diesem Aspekt betroffen. Im Gegensatz dazu können große Umsetzungsanstrengungen mit mehr als 1.000 VMs, mehreren Geschäftsbereichen oder mehreren geopolitischen Märkten erheblich von Ihrer SDN-Entscheidung und diesem wichtigen Aspekt beeinflusst werden.

## <a name="choose-the-right-virtual-networking-architectures"></a>Wählen der richtigen virtuellen Netzwerkarchitekturen

Dieser Abschnitt in diesem Leitfaden zur Entscheidungsfindung soll Ihnen helfen, die richtigen virtuellen Netzwerkarchitekturen zu wählen.

Es gibt viele Möglichkeiten, SDN-Technologien zur Erstellung cloudbasierter virtueller Netzwerke zu implementieren. Wie Sie die bei der Migration verwendeten virtuellen Netzwerke strukturieren und wie diese mit Ihrer bestehenden IT-Infrastruktur interagieren, hängt von Ihren Anforderungen an Workloads und Governance ab.

Bei der Festlegung der virtuellen Netzwerkarchitektur oder einer Kombination von Architekturen, die bei der Planung Ihrer Cloudmigration zu berücksichtigen sind, sollten Sie die folgenden Fragen prüfen, um festzustellen, was für Ihr Unternehmen das Richtige ist:

| Frage | Reine PaaS-Lösung | Cloudnativ | Cloud-DMZ | Hybrid | Hub-and-Spoke-Modell |
|-----|-----|-----|-----|-----|-----|
| Wird Ihre Workload nur PaaS-Dienste nutzen und keine Netzwerkfunktionen benötigen, die über die von den Diensten selbst bereitgestellten hinausgehen? | Ja | Nein | Nein | Nein | Nein |
| Ist für Ihre Workload eine Integration in lokale Anwendungen erforderlich? | Nein | Nein | Ja | Ja | Ja |
| Verfügen Sie über ausgereifte Sicherheitsrichtlinien und sichere Verbindungen zwischen Ihren lokalen und Cloudnetzwerken? | Nein | Nein | Nein | Ja | Ja |
| Erfordert Ihre Workload Authentifizierungsdienste, die nicht von Cloudidentitätsdiensten unterstützt werden, oder benötigen Sie direkten Zugriff auf lokale Domänencontroller? | Nein | Nein | Nein | Ja | Ja |
| Müssen Sie eine große Anzahl von VMs und Workloads bereitstellen und verwalten? | Nein | Nein | Nein | Nein | Ja |
| Müssen Sie eine zentrale Verwaltung und lokale Konnektivität bereitstellen und gleichzeitig die Kontrolle über die Ressourcen an einzelne für eine Workload zuständige Teams delegieren? | Nein | Nein | Nein | Nein | Ja |

## <a name="virtual-networking-architectures"></a>Virtuelle Netzwerkarchitekturen

Erfahren Sie mehr über die wichtigsten Architekturen für softwaredefinierte Netzwerke:

- **[Reine PaaS-Lösung](./paas-only.md):** Die meisten PaaS-Produkte (Platform as a Service) unterstützen eine begrenzte Anzahl integrierter Netzwerkfunktionen und erfordern möglicherweise kein explizit definiertes softwaredefiniertes Netzwerk zur Unterstützung der Anforderungen der Workload.
- **[Cloudnativ](./cloud-native.md):** Eine cloudnative Architektur unterstützt cloudbasierte Workloads über virtuelle Netzwerke, die auf den Standardfunktionen für softwaredefinierte Netzwerke der Cloudplattform basieren, ohne auf lokale oder andere externe Ressourcen angewiesen zu sein.
- **[Cloud-DMZ](./cloud-dmz.md):** Unterstützt eingeschränkte Konnektivität zwischen Ihrem lokalen und cloudbasierten Netzwerk, die durch die Implementierung eines Umkreisnetzwerks geschützt ist, das den Datenverkehr zwischen den beiden Umgebungen sorgfältig kontrolliert.
- **[Hybrid](./hybrid.md):** Die hybride Cloud-Netzwerkarchitektur ermöglicht es virtuellen Netzwerken in vertrauenswürdigen Cloudumgebungen, auf Ihre lokalen Ressourcen zuzugreifen und umgekehrt.
- **[Hub-and-Spoke-Modell](./hub-spoke.md):** Die Hub-and-Spoke-Architektur ermöglicht Ihnen, externe Konnektivität und gemeinsam genutzte Dienste zentral zu verwalten, einzelne Workloads zu isolieren und mögliche Abonnementgrenzen zu umgehen.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zu softwaredefinierten Netzwerken (SDN) in Azure finden Sie hier:

- [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview). In Azure wird die zentrale SDN-Funktionalität von Azure Virtual Network bereitgestellt, das als Cloud analog zu physischen lokalen Netzwerken fungiert. Virtuelle Netzwerke fungieren auch als Standardisolationsgrenze zwischen Ressourcen auf der Plattform.
- [Bewährte Methoden für die Netzwerksicherheit in Azure](/azure/security/fundamentals/network-best-practices). Empfehlungen des Azure-Sicherheitsteams für das Konfigurieren Ihrer virtuellen Netzwerke, um Sicherheitsrisiken zu minimieren.

## <a name="next-steps"></a>Nächste Schritte

Softwaredefinierte Netzwerke sind nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordern. Besuchen Sie die Übersicht über Leitfäden zur architekturbezogenen Entscheidungsfindung, um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
