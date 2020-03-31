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
ms.openlocfilehash: 3dc3071fbba6d8b33ccf7fd75a0f451160481fc5
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433115"
---
# <a name="software-defined-networking-decision-guide"></a>Leitfaden zur Entscheidungsfindung für softwaredefinierte Netzwerke

Software-Defined Networking (SDN) ist eine Netzwerkarchitektur, die entwickelt wurde, um virtualisierte Netzwerkfunktionen zu ermöglichen, die mithilfe von Software zentral verwaltet, konfiguriert und modifiziert werden können. SDN ermöglicht die Erstellung von cloudbasierten Netzwerken unter Verwendung der virtualisierten Entsprechungen zu physischen Routern, Firewalls und anderen Netzwerkgeräten, die in lokalen Netzwerken verwendet werden. SDN ist entscheidend für die Erstellung sicherer virtueller Netzwerke auf Public Cloud-Plattformen wie Azure.

## <a name="networking-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Netzwerke

![Abbildung der Netzwerkoptionen mit zunehmender Komplexität entsprechend den nachstehenden weiterführenden Links](../../_images/decision-guides/decision-guide-software-defined-network.png)

Wechseln Sie zu: [Nur PaaS](./paas-only.md) | [Cloudnativ](./cloud-native.md) | [Cloud-DMZ](./cloud-dmz.md) [Hybrid](./hybrid.md) | [Hub-and-Spoke-Modell](./hub-spoke.md) | [Weitere Informationen](#learn-more)

SDN bietet mehrere Optionen mit unterschiedlicher Preisgestaltung und Komplexität. Dieser Leitfaden zur Entscheidungsfindung bietet eine Referenz, um diese Optionen schnell zu personalisieren und so optimal auf spezifische Geschäfts- und Technologiestrategien abzustimmen.

Der Kernpunkt in diesem Leitfaden hängt von mehreren wichtigen Entscheidungen ab, die Ihr Cloudstrategieteam getroffen hat, bevor Entscheidungen zur Netzwerkarchitektur getroffen werden. Am wichtigsten sind dabei Entscheidungen, die die [Definition Ihres digitalen Bestands](../../digital-estate/index.md) und das [Abonnementmodell](../subscriptions/index.md) betreffen (was auch Rückmeldungen zu Entscheidungen im Zusammenhang mit Ihrer Cloudabrechnung und Ihren globalen Marktstrategien erfordern kann).

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

Erfahren Sie mehr über die wichtigsten Software-Defined Networking-Architekturen:

- **[Reine PaaS-Lösung](./paas-only.md):** Die meisten PaaS-Produkte (Platform as a Service) unterstützen eine begrenzte Anzahl integrierter Netzwerkfunktionen und erfordern möglicherweise kein explizit definiertes softwaredefiniertes Netzwerk zur Unterstützung der Anforderungen der Workload.
- **[Cloudnativ](./cloud-native.md):** Eine cloudnative Architektur unterstützt cloudbasierte Workloads über virtuelle Netzwerke, die auf den von der Cloudplattform standardmäßig definierten Netzwerkfunktionen basieren, ohne auf lokale oder andere externe Ressourcen angewiesen zu sein.
- **[Cloud-DMZ](./cloud-dmz.md):** Unterstützt eingeschränkte Konnektivität zwischen Ihrem lokalen und Cloudnetzwerk, die durch die Implementierung einer DMZ geschützt ist, die den Datenverkehr zwischen den beiden Umgebungen sorgfältig kontrolliert.
- **[Hybrid](./hybrid.md):** Die hybride Cloud-Netzwerkarchitektur ermöglicht es virtuellen Netzwerken in vertrauenswürdigen Cloudumgebungen, auf Ihre lokalen Ressourcen zuzugreifen und umgekehrt.
- **[Hub-and-Spoke-Modell](./hub-spoke.md):** Die Hub-and-Spoke-Architektur ermöglicht Ihnen, externe Konnektivität und gemeinsam genutzte Dienste zentral zu verwalten, einzelne Workloads zu isolieren und mögliche Abonnementgrenzen zu umgehen.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zu softwaredefinierten Netzwerken (SDN) in Azure finden Sie hier:

- [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). In Azure wird die zentrale SDN-Funktionalität von Azure Virtual Network bereitgestellt, das als Cloud analog zu physischen lokalen Netzwerken fungiert. Virtuelle Netzwerke fungieren auch als Standardisolationsgrenze zwischen Ressourcen auf der Plattform.
- [Bewährte Methoden für die Netzwerksicherheit in Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices). Empfehlungen des Azure Security-Teams zum Konfigurieren Ihrer virtuellen Netzwerke, um Sicherheitsrisiken zu minimieren.

## <a name="next-steps"></a>Nächste Schritte

„Softwaredefinierte Netzwerke“ sind nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die [Übersicht über Leitfäden zur Entscheidungsfindung](../index.md), um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
