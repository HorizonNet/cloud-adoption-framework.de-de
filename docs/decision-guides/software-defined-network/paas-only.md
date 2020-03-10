---
title: 'Softwaredefiniertes Netzwerk: Reine PaaS-Lösung'
description: Hier finden Sie Informationen zu den Vorteilen und Einschränkungen eines reinen PaaS-Architekturmodells in softwaredefinierten Netzwerken in der Cloud.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 14b1a068f4f1011fe10a61dd8f9a7738f7b35f07
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707967"
---
# <a name="software-defined-networking-paas-only"></a>Softwaredefiniertes Netzwerk: Reine PaaS-Lösung

Wenn Sie eine PaaS-Ressource (Platform as a Service) implementieren, wird im Bereitstellungsprozess automatisch ein angenommenes zugrunde liegendes Netzwerk mit einer begrenzten Anzahl von Steuerungsmöglichkeiten über dieses Netzwerk erstellt, einschließlich Lastenausgleich, Portblockierung und Verbindungen mit anderen PaaS-Diensten.

In Azure können mehrere PaaS-Ressourcentypen in einem virtuellen Netzwerk [bereitgestellt](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services) oder damit [verbunden](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) werden, sodass diese Ressourcen in Ihre bestehende virtuelle Netzwerkinfrastruktur integriert werden können. Andere Dienste wie [App Service-Umgebungen](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure Kubernetes Services (AKS)](https://docs.microsoft.com/azure/aks/intro-kubernetes) und [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) müssen innerhalb eines virtuellen Netzwerks bereitgestellt werden. In vielen Fällen reicht jedoch eine reine PaaS-Netzwerkarchitektur, die sich ausschließlich auf die standardmäßigen native Netzwerkfunktionen stützt, die von PaaS-Ressourcen nativ bereitgestellt werden, aus, um die Anforderungen an die Konnektivität und Datenverkehrsverwaltung von Workloads zu erfüllen.

Wenn Sie eine reine PaaS-Netzwerkarchitektur in Betracht ziehen, sollten Sie sicherstellen, dass Ihre Annahmen mit Ihren Anforderungen übereinstimmen.

## <a name="paas-only-assumptions"></a>Annahmen für eine reine Paas-Lösung

Für die Bereitstellung einer reinen PaaS-Netzwerkarchitektur wird Folgendes angenommen:

- Die bereitzustellende Anwendung ist eine eigenständige Anwendung oder ist nur von anderen PaaS-Ressourcen abhängig, für die kein virtuelles Netzwerk erforderlich ist.
- Ihre IT-Betriebsteams können ihre Tools, Trainings und Prozesse aktualisieren, um die Verwaltung, Konfiguration und Bereitstellung eigenständiger PaaS-Anwendungen zu unterstützen.
- Die PaaS-Anwendung ist nicht Teil einer umfassenderen Cloudmigration, die IaaS-Ressourcen einbezieht.

Diese Annahmen sind Mindestkriterien, die auf die Bereitstellung eines reinen PaaS-Netzwerks ausgelegt sind. Wenngleich dieser Ansatz die Anforderungen einer einzelnen Anwendungsbereitstellung erfüllen kann, sollte jedes, für die Cloudeinführung zuständiges Team diese längerfristigen Fragen prüfen:

- Wird diese Bereitstellung in Bezug auf Umfang oder Skalierung erweitert, um den Zugriff auf andere Nicht-PaaS-Ressourcen zu ermöglichen?
- Sind weitere PaaS-Bereitstellungen über die aktuelle Lösung hinaus geplant?
- Hat die Organisation Pläne für weitere künftige Cloudmigrationen?

Die Antworten auf diese Fragen werden ein Team nicht davon abhalten, sich für eine reine PaaS-Lösung zu entscheiden, sollten aber vor einer endgültigen Entscheidung berücksichtigt werden.
