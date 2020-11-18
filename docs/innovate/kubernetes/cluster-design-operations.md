---
title: Clusterentwurf und Vorgänge
description: Enthält eine Beschreibung von Kubernetes im Framework für die Cloudeinführung (Cloud Adoption Framework) in Bezug auf den Clusterentwurf und die zugehörigen Vorgänge.
author: sabbour
ms.author: asabbour
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 39fd5d6de4428ae30fa5acb2835a82e49946dca6
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94713597"
---
<!-- cSpell:ignore autoscaler PDBs -->

# <a name="cluster-design-and-operations"></a>Clusterentwurf und Vorgänge

Identifizieren Sie Clusterkonfiguration und Netzwerkdesign. Gewährleisten Sie zukunftssichere Skalierbarkeit durch die Automatisierung der Infrastrukturbereitstellung. Stellen Sie Hochverfügbarkeit sicher, indem Sie Business Continuity & Disaster Recovery planen.

## <a name="plan-train-and-proof"></a>Planen, Trainieren und Prüfen

Die unten angegebene Checkliste und die Ressourcen dienen Ihnen beim Einstieg als Hilfe zur Planung des Clusterentwurfs. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Haben Sie die Anforderungen an den Netzwerkentwurf für Ihren Cluster ermittelt?
> - Verfügen Sie über Workloads mit unterschiedlichen Anforderungen? Wie viele Knotenpools sollen verwendet werden?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Ermitteln der wichtigen Aspekte in Bezug auf den Netzwerkentwurf:** Machen Sie sich mit den Aspekten des Clusternetzwerkentwurfs vertraut, vergleichen Sie Netzwerkmodelle, und wählen Sie das Kubernetes-Netzwerk-Plug-In aus, das Ihre Anforderungen erfüllt. Beachten Sie für das Azure Container Networking Interface (CNI) die Anzahl der IP-Adressen, die als Vielfaches der maximalen Pods pro Knoten (Standardwert 30) und Anzahl der Knoten erforderlich sind. Fügen Sie einen Knoten hinzu, der beim Upgrade erforderlich ist. Bei der Auswahl der Load Balancer-Dienste sollten Sie einen Eingangsdatencontroller verwenden, wenn zu viele Dienste vorhanden sind, um die Anzahl der verfügbar gemachten Endpunkte zu verringern. Für Azure CNI muss die Dienst-CIDR im virtuellen Netzwerk und allen verbundenen virtuellen Netzwerken eindeutig sein, um ein entsprechendes Routing sicherzustellen. | <li> [Kubenet-Netzwerkschnittstelle&nbsp;und&nbsp;Azure&nbsp;Container&nbsp;Networking&nbsp;Interface&nbsp;(CNI)](/azure/aks/concepts-network#azure-virtual-networks) <li> [Verwenden von kubenet-Netzwerken mit Ihren eigenen IP-Adressbereichen in Azure Kubernetes Service (AKS)](/azure/aks/configure-kubenet) <li> [Konfigurieren von Azure CNI-Netzwerken in Azure Kubernetes Service (AKS)](/azure/aks/configure-azure-cni) <li> [Sicherer Netzwerkentwurf für einen AKS-Cluster](https://github.com/Azure/sg-aks-workshop/blob/master/cluster-design/NetworkDesign.md)|
> | **Erstellen mehrerer Knotenpools:** Zur Unterstützung von Anwendungen, die über unterschiedliche Compute- oder Speicheranforderungen verfügen, können Sie Ihren Cluster optional mit mehreren Knotenpools konfigurieren. Verwenden Sie zusätzliche Knotenpools beispielsweise zum Bereitstellen von GPUs für rechenintensive Anwendungen oder für den Zugriff auf leistungsstarken SSD-Speicher.   | <li> [Erstellen&nbsp;und&nbsp;Verwalten&nbsp;mehrerer&nbsp;Knotenpools&nbsp;&nbsp;für einen Cluster in Azure Kubernetes Service](/azure/aks/use-multiple-node-pools) |
> | **Treffen einer Entscheidung zu Verfügbarkeitsanforderungen:** Mindestens zwei Pods hinter Azure Kubernetes Service sorgen im Fall von Podfehlern oder -neustarts für eine hohe Verfügbarkeit Ihrer Anwendung. Verwenden Sie drei oder mehr Pods, um die Last bei Podfehlern und -neustarts zu verarbeiten. Für die Clusterkonfiguration sind mindestens zwei Knoten in einer Verfügbarkeitsgruppe oder VM-Skalierungsgruppe erforderlich, um die Vereinbarung zum Service Level von 99,95 % einzuhalten. Verwenden Sie mindestens drei Pods, um die Podplanung bei Knotenfehlern und -neustarts sicherzustellen. Um eine höhere Verfügbarkeit Ihrer Anwendungen zu gewährleisten, können Cluster über Verfügbarkeitszonen verteilt werden. Diese Zonen sind physisch getrennte Rechenzentren innerhalb einer bestimmten Region. Wenn die Clusterkomponenten auf mehrere Zonen verteilt sind, kann Ihr Cluster einen Fehler in einer dieser Zonen tolerieren. Ihre Anwendungen und Verwaltungsabläufe bleiben auch beim Ausfall eines gesamten Rechenzentrums weiterhin verfügbar. | <li> [Erstellen eines Azure Kubernetes Service-Clusters (AKS), der Verfügbarkeitszonen verwendet](/azure/aks/availability-zones) |

## <a name="go-to-production-and-apply-best-practices"></a>Vorbereiten der Umstellung auf die Produktion und Anwenden von bewährten Methoden

Beim Vorbereiten der Anwendung für die Produktion sollten Sie einen Mindestsatz an bewährten Methoden implementieren. Verwenden Sie an diesem Punkt die unten angegebene Checkliste. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Sind Sie sicher, dass Sie die erneute Bereitstellung der Clusterinfrastruktur durchführen können?
> - Haben Sie Ressourcenkontingente angewendet?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automatisieren der Clusterbereitstellung:** Mit Infrastructure-as-Code können Sie die Infrastrukturbereitstellung automatisieren, um eine bessere Resilienz bei Notfällen zu erzielen und die Flexibilität zu erhöhen, damit Sie die Infrastruktur je nach Bedarf schnell neu bereitstellen können.  | <li> [Erstellen eines Kubernetes-Clusters mit Azure Kubernetes Service unter Verwendung von Terraform](/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks)|
> | **Planen der Verfügbarkeit mit Budgets für die Unterbrechung von Pods:** Zur Aufrechterhaltung der Verfügbarkeit von Anwendungen definieren Sie Budgets für die Unterbrechung von Pods (Pod Disruption Budgets, PDBs), um sicherzustellen, dass bei Hardwarefehlern oder Clusterupgrades eine Mindestanzahl von Pods im Cluster verfügbar ist. | <li> [Verfügbarkeitsplanung&nbsp;mithilfe&nbsp;von&nbsp;Budgets&nbsp;für&nbsp;die&nbsp;Unterbrechung von Pods](/azure/aks/operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)  |
> | **Erzwingen von Ressourcenkontingenten in Namespaces.** Planen Sie Ressourcenkontingente auf Namespaceebene, und wenden Sie sie an. Kontingente können für Computeressourcen, Speicherressourcen und die Objektanzahl festgelegt werden.| <li> [Durchsetzen von Ressourcenkontingenten](/azure/aks/operator-best-practices-scheduler#enforce-resource-quotas)  |

## <a name="optimize-and-scale"></a>Optimieren und Skalieren

Nachdem sich die Anwendung nun in der Produktion befindet, stellt sich die folgende Frage: Wie können Sie Ihren Workflow optimieren und Ihre Anwendung und das Team auf die Skalierung vorbereiten? Nutzen Sie für die Vorbereitung die Checkliste für die Optimierung und Skalierung. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Verfügen Sie über einen Plan für die Geschäftskontinuität und Notfallwiederherstellung (Business Continuity & Disaster Recovery, BCDR)?
> - Kann Ihr Cluster skaliert werden, um Anwendungsanforderungen zu erfüllen?
> - Können Sie Ihre Cluster- und Anwendungsintegrität überwachen und Warnungen empfangen?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste | Ressourcen |
> |--|--|
> | **Automatisches Skalieren eines Clusters zur Erfüllung von Anwendungsanforderungen.** Zur Erfüllung der Anwendungsanforderungen müssen Sie unter Umständen die Anzahl von Knoten, auf denen Ihre Workloads ausgeführt werden, mit der automatischen Clusterskalierung anpassen. | <li> [Automatisches Skalieren eines Clusters zur Erfüllung von Anwendungsanforderungen in Azure Kubernetes Service (AKS)](/azure/aks/cluster-autoscaler) |
> | **Planen für Geschäftskontinuität und Notfallwiederherstellung.** Planen Sie die Bereitstellung in mehreren Regionen, erstellen Sie einen Migrationsplan, und aktivieren Sie die Georeplikation für Containerimages. | <li> [Best Practices für die Bereitstellung in Regionen](/azure/aks/operator-best-practices-multi-region) <li> [Georeplikation in Azure Container Registry](/azure/container-registry/container-registry-geo-replication) |
> | **Konfigurieren der bedarfsgesteuerten Überwachung und Problembehandlung.** Richten Sie Warnungen und die Überwachung für Anwendungen in Kubernetes ein. Informieren Sie sich über die Standardkonfiguration, die Integration erweiterter Metriken und die Hinzufügung Ihrer eigenen benutzerdefinierten Überwachungs- und Warnungsfunktionen, um einen zuverlässigen Betrieb Ihrer Anwendung zu ermöglichen. | <li> [Erste Schritte mit Überwachung und Warnungen für Kubernetes (Video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <li> [Azure Monitor für Container – Übersicht](/azure/azure-monitor/insights/container-insights-overview) <li> [Überprüfen&nbsp;von&nbsp;Diagnoseprotokollen&nbsp;für&nbsp;Masterkomponenten&nbsp;](/azure/aks/view-master-logs) <li> [Übersicht über die Azure Kubernetes Service-Diagnose (Vorschau)](/azure/aks/concepts-diagnostics) |
