---
title: Cluster- und Anwendungssicherheit
description: Enthält eine Beschreibung von Kubernetes im Framework für die Cloudeinführung (Cloud Adoption Framework) in Bezug auf die Cluster- und Anwendungssicherheit.
author: sabbour
ms.author: asabbour
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 919291ade8c760429eb5df4d848f745014912eb6
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/26/2020
ms.locfileid: "83861989"
---
<!-- cSpell:ignore asabbour sabbour kured -->

# <a name="cluster-and-application-security"></a>Cluster- und Anwendungssicherheit

Machen Sie sich mit den Grundlagen der Kubernetes-Sicherheit vertraut, und sehen Sie sich die Anleitung zur sicheren Einrichtung der Cluster- und Anwendungssicherheit an.

## <a name="plan-train-and-proof"></a>Planen, Trainieren und Prüfen

Die unten angegebene Checkliste und die Ressourcen dienen Ihnen beim Einstieg als Hilfe für die Planung des Betriebs und der Sicherheit Ihres Clusters. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Haben Sie das Sicherheits- und Bedrohungsmodell von Kubernetes-Clustern überprüft?
> - Ist für Ihren Cluster die rollenbasierte Zugriffssteuerung aktiviert?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Vertrautmachen mit dem Whitepaper zu den Sicherheitsgrundlagen:** Bei den Hauptzielen einer sicheren Kubernetes-Umgebung geht es um die Sicherstellung, dass die ausgeführten Anwendungen geschützt sind, dass die Sicherheitsprobleme schnell ermittelt und behoben werden können und dass ähnliche Probleme in Zukunft verhindert werden. | [Ultimative Anleitung zum Schützen von Kubernetes (Whitepaper)](https://clouddamcdnprodep.azureedge.net/gdc/gdc8LXmoZ/original)     |
> | **Informieren über die Einrichtung von gehärteten Clusterknoten aus Sicherheitsgründen:** Mit einem aus Sicherheitsgründen gehärteten Hostbetriebssystem wird die Angriffsfläche reduziert und die sichere Bereitstellung von Containern ermöglicht. | [Sicherheitshärtung bei AKS-Hosts für virtuelle Computer](https://docs.microsoft.com/azure/aks/security-hardened-vm-host-image)     |
> | **Einrichten der rollenbasierten Zugriffssteuerung (RBAC) für Cluster:** Mit diesem Steuerungsmechanismus können Sie Benutzern oder Benutzergruppen die Berechtigung für bestimmte Aktionen (z. B. Ressourcen erstellen bzw. ändern oder Protokolle zur Workload ausgeführter Anwendungen anzeigen) zuweisen. | [Grundlegendes zur rollenbasierten Zugriffssteuerung (RBAC) in Kubernetes (Video)](https://www.youtube.com/watch?v=G3R24JSlGjY&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=12) <br> [Integrieren von Azure Active Directory in Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/azure-ad-integration) <br> [Definieren des Zugriffs auf die Kubernetes-Konfigurationsdatei in Azure Kubernetes Service (AKS) mithilfe der rollenbasierten Zugriffssteuerung von Azure](https://docs.microsoft.com/azure/aks/control-kubeconfig-access)   |

## <a name="deploy-to-production-and-apply-best-practices"></a>Bereitstellen für die Produktion und Anwendungen von bewährten Methoden

Beim Vorbereiten der Anwendung für die Produktion sollten Sie einen Mindestsatz an bewährten Methoden implementieren. Verwenden Sie an diesem Punkt die unten angegebene Checkliste. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Haben Sie Netzwerksicherheitsregeln für die eingehende, ausgehende und Pod-interne Kommunikation konfiguriert?
> - Ist Ihr Cluster für die automatische Anwendung von Sicherheitsupdates für Knoten konfiguriert?
> - Führen Sie für Ihre Cluster- und Containerworkloads eine Lösung für Sicherheitsüberprüfungen aus?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Steuern des Zugriffs auf Cluster per Gruppenmitgliedschaft:** Konfigurieren Sie die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) von Kubernetes, um den Zugriff auf Clusterressourcen anhand der Benutzeridentität oder Gruppenmitgliedschaft zu beschränken. | [Steuern des Zugriffs auf Clusterressourcen per rollenbasierter Zugriffssteuerung und mit Azure Active Directory-Identitäten in Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/azure-ad-rbac)    |
> | **Erstellen einer Richtlinie für die Geheimnisverwaltung:** Verwenden Sie die Geheimnisverwaltung von Kubernetes, um sensible Informationen, z. B. Kennwörter und Zertifikate, sicher bereitzustellen und zu verwalten. | [Grundlagen der Verwaltung von Geheimnissen in Kubernetes (Video)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) |
> | **Schützen des Netzwerkdatenverkehrs zwischen Pods mit Netzwerkrichtlinien:** Wenden Sie das Prinzip der geringsten Rechte an, um den Netzwerkdatenverkehr zwischen den Pods im Cluster zu steuern. | [Sicherer Datenverkehr zwischen Pods durch Netzwerkrichtlinien in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/use-network-policies) |
> | **Einschränken des Zugriffs auf den API-Server mit autorisierten IP-Adressen:** Erhöhen Sie die Clustersicherheit, und reduzieren Sie die Angriffsfläche, indem Sie den Zugriff auf den API-Server auf eine begrenzte Zahl von IP-Adressbereichen beschränken. | [Sicherer Zugriff auf den API-Server mit autorisierten IP-Adressbereichen in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/api-server-authorized-ip-ranges) |
> | **Beschränken des ausgehenden Datenverkehrs eines Clusters:** Hier wird beschrieben, welche Ports und Adressen zugelassen werden müssen, wenn Sie den ausgehenden Datenverkehr für den Cluster einschränken. Sie können Azure Firewall oder eine Firewallappliance eines Drittanbieters verwenden, um den ausgehenden Datenverkehr zu schützen und diese erforderlichen Ports und Adressen zu definieren. | [Steuern des ausgehenden Datenverkehrs für Clusterknoten in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/limit-egress-traffic) |
> | **Schützen des Datenverkehrs mit einer Web Application Firewall (WAF):** Verwenden Sie Azure Application Gateway als Controller für den eingehenden Datenverkehr von Kubernetes-Clustern.  | [Was ist der Application Gateway-Eingangscontroller?](https://docs.microsoft.com/azure/application-gateway/ingress-controller-overview)    |
> | **Anwenden von Sicherheits- und Kernelupdates auf Workerknoten:** Grundlegendes zur Umgebung für AKS-Knotenupdates Sicherheitsupdates werden automatisch auf Linux-Knoten in AKS angewendet, um Ihre Cluster zu schützen. Diese Updates enthalten Sicherheitsfixes für das Betriebssystem oder Kernelupdates. Einige dieser Updates erfordern den Neustart eines Knotens, um den Vorgang abzuschließen. | [Anwenden von Sicherheits- und Kernelupdates auf Linux-Knoten in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/node-updates-kured) |
> | **Konfigurieren einer Lösung für die Container- und Clusterüberprüfung:** Überprüfen Sie die in Azure Container Registry angeordneten Container, und verschaffen Sie sich tieferen Einblick in Ihre Clusterknoten, den Clouddatenverkehr und Sicherheitskontrollen. | [Integration von Security Center in Azure Container Registry](https://docs.microsoft.com/azure/security-center/azure-container-registry-integration) <br> [Integration von Security Center in Azure Kubernetes Service](https://docs.microsoft.com/azure/security-center/azure-kubernetes-service-integration)  |

## <a name="optimize-and-scale"></a>Optimieren und Skalieren

Nachdem sich die Anwendung nun in der Produktion befindet, stellt sich die folgende Frage: Wie können Sie Ihren Workflow optimieren und Ihre Anwendung und das Team auf die Skalierung vorbereiten? Nutzen Sie für die Vorbereitung die Checkliste für die Optimierung und Skalierung. Sie sollten die folgenden Fragen beantworten können:

> [!div class="checklist"]
>
> - Können Sie Governance- und Clusterrichtlinien bedarfsgesteuert erzwingen?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Erzwingen von Governancerichtlinien für Cluster:** Wenden Sie zentral und einheitlich bedarfsgesteuerte Erzwingungs- und Schutzmaßnahmen auf Ihre Cluster an. | [Grundlegendes zu Azure Policy für Azure Kubernetes Service](https://docs.microsoft.com/azure/governance/policy/concepts/rego-for-aks)    |
> | **Regelmäßiges Rotieren von Clusterzertifikaten:** In Kubernetes werden für viele Komponenten Zertifikate für die Authentifizierung genutzt. Es ist ratsam, diese Zertifikate aus Sicherheits- bzw. Richtliniengründen in regelmäßigen Abständen zu rotieren. | [Rotieren von Zertifikaten in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/certificate-rotation)    |
