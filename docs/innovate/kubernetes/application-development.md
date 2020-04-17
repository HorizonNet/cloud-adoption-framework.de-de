---
title: Anwendungsentwicklung und Bereitstellung
description: Es wird beschrieben, wie Kubernetes im Framework für die Cloudeinführung (Cloud Adoption Framework) für die Anwendungsentwicklung und -architektur verwendet wird.
author: sabbour
ms.author: asabbour
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5381580fc947c71ba651c96e73874c047246991c
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997688"
---
<!-- cSpell:ignore asabbour sabbour autoscaler Istio Linkerd -->

# <a name="application-development-and-deployment"></a>Anwendungsentwicklung und Bereitstellung

Untersuchen Sie Muster und Vorgehensweisen für die Anwendungsentwicklung, konfigurieren Sie DevOps-Pipelines, und implementieren Sie bewährte Methoden für Websitezuverlässigkeits-Engineering (Site Reliability Engineering, SRE).

## <a name="plan-train-and-proof"></a>Planen, Trainieren und Prüfen

Die unten angegebene Checkliste und die Ressourcen dienen Ihnen beim Einstieg als Hilfe bei der Anwendungsentwicklung und -bereitstellung. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Haben Sie Ihre Entwicklungsumgebung und den Setupworkflow vorbereitet?
> - Wie strukturieren Sie den Projektordner, um die Kubernetes-Anwendungsentwicklung zu unterstützen?
> - Haben Sie für Ihre Anwendung den Status, die Konfiguration und die Speicheranforderungen ermittelt?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste | Ressourcen |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Vorbereiten Ihrer Entwicklungsumgebung:** Konfigurieren Sie Ihre Umgebung mit den Tools, die Sie zum Erstellen von Containern und zum Einrichten des Entwicklungsworkflows benötigen. | [Arbeiten mit Docker in Visual Studio Code](https://code.visualstudio.com/docs/azure/docker) <br/>[Arbeiten&nbsp;mit&nbsp;Kubernetes&nbsp;in&nbsp;Visual&nbsp;Studio Code](https://code.visualstudio.com/docs/azure/kubernetes) <br/> [Einführung in Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/about) |
> | **Containerisieren Ihrer Anwendung:** Machen Sie sich mit der umfassenden Kubernetes-Entwicklungsumgebung vertraut, z. B. Anwendungsgerüst, Inner Loop-Workflows, Frameworks für die Anwendungsverwaltung, CI/CD-Pipelines, Protokollaggregation, Überwachung und Anwendungsmetriken. | [Containerisieren Sie Ihre Apps mit Docker und Kubernetes (E-Book)](https://azure.microsoft.com/resources/containerize-your-apps-with-docker-and-kubernetes) <br/> [Umfassende Kubernetes-Entwicklungsumgebung in Azure (Webinar)](https://info.microsoft.com/AU-AzureApp-WBNR-FY20-11Nov-12-ContainerizeYourApplicationswithKubernetesonAzure-SRDEM10557_LP02OnDemandRegistration-ForminBody.html) |
> | **Gängige Kubernetes-Szenarien:** Kubernetes wird häufig als Plattform für die Bereitstellung von Microservices betrachtet, aber die Entwicklung geht in Richtung einer deutlich umfassenderen Plattform. Sehen Sie sich dieses Video an, um mehr über gängige Kubernetes-Szenarien zu erfahren, z. B. Batchanalysen und Workflows.    | [Häufige&nbsp;Szenarien&nbsp;zur&nbsp;Verwendung von&nbsp;Kubernetes&nbsp;(Video)](https://www.youtube.com/watch?v=zd8vYhrFXp4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=7) |
> | **Vorbereiten Ihrer Anwendung für Kubernetes:** Bereiten Sie Ihr Anwendungsdateisystem-Layout für Kubernetes vor, und organisieren Sie wöchentliche oder tägliche Releases. Informieren Sie sich, wie durch den Kubernetes-Bereitstellungsprozess zuverlässige Upgrades ohne Ausfallzeit ermöglicht werden. | [Projektentwurf und -layout für erfolgreiche Kubernetes-Apps (Webinar)](https://info.microsoft.com/ww-OnDemandRegistration-successful-kubernetes-applications-webinar.html) <br/> [Funktionsweise von Kubernetes-Bereitstellungen (Video)](https://www.youtube.com/watch?v=mNK14yXIZF4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=3) </br> [Azure Kubernetes Service Workshop](https://aka.ms/learn/aksworkshop) |
> | **Verwalten des Anwendungsspeichers:** Machen Sie sich mit den Leistungsanforderungen und Zugriffsmethoden für Pods vertraut, damit Sie die entsprechenden Speicheroptionen zur Verfügung stellen können. Sie sollten auch Möglichkeiten zur Sicherung und zum Testen des Wiederherstellungsprozesses für angefügte Speicher planen. | [Grundlagen von zustandsbehafteten Anwendungen in Kubernetes (Video)](https://www.youtube.com/watch?v=GieXzb91I40&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=9) <br/> [Zustand und Daten in Docker-Anwendungen](https://docs.microsoft.com/dotnet/architecture/microservices/architect-microservice-container-applications/docker-application-state-data) <br/>[Best Practices für Speicherung und Sicherungen in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/operator-best-practices-storage) |
> | **Verwalten von Anwendungsgeheimnissen:** Speichern Sie Anmeldeinformationen nicht in Ihrem Anwendungscode. Es sollte ein Schlüsseltresor verwendet werden, um Schlüssel und Anmeldeinformationen zu speichern und abzurufen.  | [Funktionsweise von Kubernetes und der Konfigurationsverwaltung (Video)](https://www.youtube.com/watch?v=vRcQOZLnKUk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=11) <br/> [Grundlagen der Verwaltung von Geheimnissen in Kubernetes (Video)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) <br/>[Verwenden von Azure Key Vault mit Kubernetes](https://github.com/Azure/kubernetes-keyvault-flexvol) <br/>[Verwenden der Podidentität für die Authentifizierung und den Zugriff auf Azure-Ressourcen](https://github.com/Azure/aad-pod-identity) |

## <a name="deploy-to-production-and-apply-best-practices"></a>Bereitstellen für die Produktion und Anwendungen von bewährten Methoden

Beim Vorbereiten der Anwendung für die Produktion sollten Sie einen Mindestsatz an bewährten Methoden implementieren. Verwenden Sie an diesem Punkt die unten angegebene Checkliste. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Können Sie alle Aspekte Ihrer Anwendung überwachen?
> - Haben Sie Ressourcenanforderungen für Ihre Anwendung definiert? Welche Skalierungsanforderungen bestehen?
> - Können Sie neue Versionen der Anwendung bereitstellen, ohne dass sich Auswirkungen auf Produktionssysteme ergeben?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Konfigurieren von Integritätsprüfungen in Bezug auf die Bereitschaft und den Livezustand:** In Kubernetes werden Bereitschafts- und Livetests durchgeführt, damit Sie wissen, wann Ihre Anwendung für den Empfang von Datenverkehr bereit ist und wann sie neu gestartet werden muss. Bei fehlender Definition dieser Überprüfungen kann von Kubernetes nicht ermittelt werden, ob Ihre Anwendung aktiv ist und ausgeführt wird.   | [Überprüfung des Livezustands und der Bereitschaft](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes) |
> | **Konfigurieren von Protokollierung, Anwendungsüberwachung und Warnungen:** Die Überwachung Ihrer Container ist vor allem dann entscheidend, wenn Sie einen umfangreichen Produktionscluster mit mehreren Anwendungen ausführen. Das empfohlene Protokollierungsverfahren für containerisierte Anwendungen ist das Schreiben in die Standardausgabe- (stdout) und Standardfehlerstreams (stderr).   | [Protokollierung in Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging) <br/> [Erste Schritte mit Überwachung und Warnungen für Kubernetes (Video)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Azure Monitor für Container](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Aktivieren und Überprüfen der Kubernetes-Masterknotenprotokolle in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/view-master-logs)  <br/> [Anzeigen von Kubernetes-Protokollen, -Ereignissen und -Podmetriken in Echtzeit](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-livedata-overview) |
> | **Definieren der Ressourcenanforderungen für die Anwendung:** Eine primäre Methode zum Verwalten der Computeressourcen in einem Kubernetes-Cluster ist die Verwendung von Podanforderungen und -grenzwerten. Anhand dieser Anforderungen und Grenzwerte kann der Kubernetes-Planer sehen, welche Computeressourcen einem Pod zugewiesen werden sollten.     | [Definieren&nbsp;von&nbsp;Podressourcenanforderungen&nbsp;und&nbsp;-grenzwerten&nbsp;](https://docs.microsoft.com/azure/aks/developer-best-practices-resource-management) |
> | **Konfigurieren der Skalierungsanforderungen für Anwendungen:** Kubernetes unterstützt die automatische horizontale Skalierung von Pods, um die Anzahl von Pods in einer Bereitstellung je nach CPU-Nutzung und anderen ausgewählten Metriken anzupassen. Um die automatische Skalierungsfunktion zu verwenden, müssen für alle Container in Ihren Pods CPU-Anforderungen und -Grenzwerte definiert sein.    | [Automatisches Skalieren von Pods](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale#autoscale-pods) |
> | **Bereitstellen von Anwendungen per automatisierter Pipeline und DevOps:**  Die vollständige Automatisierung aller Schritte vom Codecommit bis zur Bereitstellung für die Produktion ermöglicht Teams die Konzentration auf die Codeerstellung und beseitigt den Mehraufwand und die potenzielle Anfälligkeit für menschliche Fehler bei lästigen manuellen Schritten. Die Bereitstellung von neuem Code ist schneller und weniger risikoreich, sodass Teams Code flexibler, produktiver und vertrauensvoller ausführen können.    | [Weiterentwickeln Ihrer DevOps-Methoden](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices) <br/> [Einrichten einer Kubernetes-Buildpipeline (Video)](https://www.youtube.com/watch?v=5irsAdKoEBU&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=6) <br/> [Bereitstellungscenter für Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/deployment-center-launcher) <br/> [GitHub Actions für die Bereitstellung im Kubernetes Service](https://docs.microsoft.com/azure/aks/kubernetes-action) <br/>  [Tutorial: Bereitstellen über GitHub in Azure Kubernetes Service (AKS) mit Continuous Integration und Continuous Deployment von Jenkins](https://docs.microsoft.com/azure/aks/jenkins-continuous-deployment) |

## <a name="optimize-and-scale"></a>Optimieren und Skalieren

Nachdem sich die Anwendung nun in der Produktion befindet, stellt sich die folgende Frage: Wie können Sie Ihren Workflow optimieren und Ihre Anwendung und das Team auf die Skalierung vorbereiten? Nutzen Sie für die Vorbereitung die Checkliste für die Optimierung und Skalierung. Sie sollten diese Fragen beantworten können:

> [!div class="checklist"]
>
> - Werden von Ihrer Anwendung übergreifende Anwendungsaspekte abstrahiert?
> - Können Sie die System- und Anwendungszuverlässigkeit aufrechterhalten, während neue Features und Versionen durchlaufen werden?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Checkliste  | Ressourcen                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Bereitstellen eines API-Gateways:** Ein API-Gateway dient als Front Door für die Microservices, entkoppelt Clients von Ihren Microservices, fügt eine zusätzliche Sicherheitsebene hinzu und verringert die Komplexität Ihrer Microservices, da die Behandlung von bereichsübergreifenden Problemen entfällt.     | [Verwenden von API Management mit in Azure Kubernetes Service bereitgestellten Microservices](https://docs.microsoft.com/azure/api-management/api-management-kubernetes) |
> | **Bereitstellen eines Dienstnetzes:** Ein Dienstnetz verfügt für Ihre Workloads über Funktionen für die Bereiche Datenverkehrsverwaltung, Resilienz, Richtlinie, Sicherheit, sichere Identität und Einblick. Ihre Anwendung ist von diesen betriebsbezogenen Funktionen abgekoppelt, und sie werden vom Dienstnetz von der Anwendungsschicht herunter auf die Infrastrukturebene verschoben.     | [Funktionsweise&nbsp;von&nbsp;Dienstnetzen&nbsp;in&nbsp;Kubernetes&nbsp;(Video)&nbsp;](https://www.youtube.com/watch?v=izVWk7rYqWI&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=15&t=0s) <br/> [Informationen zu Dienstnetzen](https://docs.microsoft.com/azure/aks/servicemesh-about) <br/> [Istio](https://docs.microsoft.com/azure/aks/servicemesh-istio-about) <br/> [Linkerd](https://docs.microsoft.com/azure/aks/servicemesh-linkerd-about) <br/> [Consul](https://docs.microsoft.com/azure/aks/servicemesh-consul-about) |
> | **Implementieren von Methoden für Websitezuverlässigkeits-Engineering (Site Reliability Engineering):**  Websitezuverlässigkeits-Engineering (Site Reliability Engineering, SRE) ist ein bewährter Ansatz zur Aufrechterhaltung der entscheidenden Zuverlässigkeit von Systemen und Anwendungen, während gleichzeitig mit der vom Marketplace geforderten Geschwindigkeit Schritt gehalten wird.   | [Einführung in Site Reliability Engineering (SRE)](https://docs.microsoft.com/learn/modules/intro-to-site-reliability-engineering) <br/> [DevOps bei Microsoft: SRE für Game-Streaming](https://azure.microsoft.com/resources/devops-at-microsoft-game-streaming-sre) |
