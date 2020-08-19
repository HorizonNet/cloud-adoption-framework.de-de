---
title: Clusterentwurf und Vorgänge
description: Enthält eine Beschreibung von Kubernetes im Framework für die Cloudeinführung (Cloud Adoption Framework) in Bezug auf den Clusterentwurf und die zugehörigen Vorgänge.
author: sabbour
ms.author: asabbour
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: d7351fc55f91645c79dd50e803ef8ca940beaa7c
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572237"
---
<!-- cSpell:ignore asabbour sabbour autoscaler PDBs -->

# <a name="cluster-design-and-operations"></a>Clusterentwurf und Vorgänge

Identifizieren Sie Clusterkonfiguration und Netzwerkdesign. Gewährleisten Sie zukunftssichere Skalierbarkeit durch die Automatisierung der Infrastrukturbereitstellung. Stellen Sie Hochverfügbarkeit sicher, indem Sie Business Continuity & Disaster Recovery planen.

## <a name="plan-train-and-proof"></a>Planen, Trainieren und Prüfen

Die unten angegebene Checkliste und die Ressourcen dienen Ihnen beim Einstieg als Hilfe zur Planung des Clusterentwurfs. Sie sollten diese Fragen beantworten können:

<!-- markdownlint-disable MD033 -->

> [!div class="checklist"]
>
> - Haben Sie die Anforderungen an den Netzwerkentwurf für Ihren Cluster ermittelt?
> - Verfügen Sie über Workloads mit unterschiedlichen Anforderungen? Wie viele Knotenpools sollen verwendet werden?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Ermitteln der wichtigen Aspekte in Bezug auf den Netzwerkentwurf:** Machen Sie sich mit den Aspekten des Clusternetzwerkentwurfs vertraut, vergleichen Sie Netzwerkmodelle, und wählen Sie das Kubernetes-Netzwerk-Plug-In aus, das Ihre Anforderungen erfüllt.    | [Kubenet-Netzwerkschnittstelle und Azure Container Networking Interface (CNI)](/azure/aks/concepts-network#azure-virtual-networks) <br> [Verwenden von kubenet-Netzwerken mit Ihren eigenen IP-Adressbereichen in Azure Kubernetes Service (AKS)](/azure/aks/configure-kubenet) <br> [Konfigurieren von Azure CNI-Netzwerken in Azure Kubernetes Service (AKS)](/azure/aks/configure-azure-cni) <br> [Sicherer Netzwerkentwurf für einen AKS-Cluster](https://github.com/azure/sg-aks-workshop/blob/master/cluster-design/NetworkDesign.md) |
> | **Erstellen mehrerer Knotenpools:** Zur Unterstützung von Anwendungen, die über unterschiedliche Compute- oder Speicheranforderungen verfügen, können Sie Ihren Cluster optional mit mehreren Knotenpools konfigurieren. Verwenden Sie zusätzliche Knotenpools beispielsweise zum Bereitstellen von GPUs für rechenintensive Anwendungen oder für den Zugriff auf leistungsstarken SSD-Speicher.   | [Erstellen und Verwalten mehrerer Knotenpools für einen Cluster in Azure Kubernetes Service (AKS)](/azure/aks/use-multiple-node-pools) |
> | **Treffen einer Entscheidung zu Verfügbarkeitsanforderungen:** Um eine höhere Verfügbarkeit Ihrer Anwendungen zu gewährleisten, können Cluster über Verfügbarkeitszonen verteilt werden. Diese Zonen sind physisch getrennte Rechenzentren innerhalb einer bestimmten Region. Wenn die Clusterkomponenten auf mehrere Zonen verteilt sind, kann Ihr Cluster einen Fehler in einer dieser Zonen tolerieren. Ihre Anwendungen und Verwaltungsabläufe sind auch bei Problemen in einem gesamten Rechenzentrum weiterhin verfügbar.   | [Erstellen eines Azure Kubernetes Service-Clusters (AKS), der Verfügbarkeitszonen verwendet](/azure/aks/availability-zones) |

## <a name="go-to-production-and-apply-best-practices"></a>Vorbereiten der Umstellung auf die Produktion und Anwenden von bewährten Methoden

Beim Vorbereiten der Anwendung für die Produktion sollten Sie einen Mindestsatz an bewährten Methoden implementieren. Verwenden Sie an diesem Punkt die unten angegebene Checkliste. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Sind Sie sicher, dass Sie die erneute Bereitstellung der Clusterinfrastruktur durchführen können?
> - Haben Sie Ressourcenkontingente angewendet?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen |
> |---|---|
> | **Automatisieren der Clusterbereitstellung:** Mit Infrastructure-as-Code können Sie die Infrastrukturbereitstellung automatisieren, um eine bessere Resilienz bei Notfällen zu erzielen und die Flexibilität zu erhöhen, damit Sie die Infrastruktur je nach Bedarf schnell neu bereitstellen können. | [Erstellen eines Kubernetes-Clusters mit Azure Kubernetes Service unter Verwendung von Terraform](/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks) |
> | **Planen der Verfügbarkeit mit Budgets für die Unterbrechung von Pods:** Zur Aufrechterhaltung der Verfügbarkeit von Anwendungen definieren Sie Budgets für die Unterbrechung von Pods (Pod Disruption Budgets, PDBs), um sicherzustellen, dass bei Hardwarefehlern oder Clusterupgrades eine Mindestanzahl von Pods im Cluster verfügbar ist. | [Planen der Verfügbarkeit mit Budgets für die Unterbrechung von Pods](/azure/aks/operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets) |
> | **Erzwingen von Ressourcenkontingenten in Namespaces.** Planen Sie Ressourcenkontingente auf Namespaceebene, und wenden Sie sie an. Kontingente können für Computeressourcen, Speicherressourcen und die Objektanzahl festgelegt werden. | [Durchsetzen von Ressourcenkontingenten](/azure/aks/operator-best-practices-scheduler#enforce-resource-quotas) |

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
> | Checkliste  | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automatisches Skalieren eines Clusters zur Erfüllung von Anwendungsanforderungen.** Zur Erfüllung der Anwendungsanforderungen müssen Sie unter Umständen die Anzahl von Knoten, auf denen Ihre Workloads ausgeführt werden, mit der automatischen Clusterskalierung anpassen. | [Automatisches Skalieren eines Clusters zur Erfüllung von Anwendungsanforderungen in Azure Kubernetes Service (AKS)](/azure/aks/cluster-autoscaler)    |
> | **Planen für Geschäftskontinuität und Notfallwiederherstellung.** Planen Sie die Bereitstellung in mehreren Regionen, erstellen Sie einen Migrationsplan, und aktivieren Sie die Georeplikation für Containerimages. | [Best Practices für die Bereitstellung in Regionen](/azure/aks/operator-best-practices-multi-region) <br> [Georeplikation in Azure Container Registry](/azure/container-registry/container-registry-geo-replication)  |
> | **Konfigurieren der bedarfsgesteuerten Überwachung und Problembehandlung.** Richten Sie Warnungen und die Überwachung für Anwendungen in Kubernetes ein. Informieren Sie sich über die Standardkonfiguration, die Integration erweiterter Metriken und die Hinzufügung Ihrer eigenen benutzerdefinierten Überwachungs- und Warnungsfunktionen, um einen zuverlässigen Betrieb Ihrer Anwendung zu ermöglichen. | [Erste Schritte mit Überwachung und Warnungen für Kubernetes (Video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br> [Azure Monitor für Container – Übersicht](/azure/azure-monitor/insights/container-insights-overview) <br> [Aktivieren und Überprüfen der Kubernetes-Masterknotenprotokolle in Azure Kubernetes Service (AKS)](/azure/aks/view-master-logs) <br> [Übersicht über die Azure Kubernetes Service-Diagnose (Vorschau)](/azure/aks/concepts-diagnostics)    |
