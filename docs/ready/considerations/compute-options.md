---
title: Überprüfen Ihrer Computeoptionen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um die Computeanforderungen für das Hosten Ihrer Workloads zu ermitteln.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e2f0eaf711cb52c400f63ae33131f295a66c9e84
ms.sourcegitcommit: 71a4f33546443d8c875265ac8fbaf3ab24ae8ab4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86479737"
---
# <a name="review-your-compute-options"></a>Überprüfen Ihrer Computeoptionen

Die Ermittlung der Computeanforderungen für das Hosting Ihrer Workloads ist ein wichtiger Aspekt, wenn Sie sich auf die Cloudeinführung vorbereiten. Azure-Computeprodukte und -dienste unterstützen viele verschiedene Szenarien und Funktionen für das Workloadcomputing. Die Konfiguration Ihrer Landezonenumgebung zur Unterstützung der Computeanforderungen richtet sich nach den governancebezogenen, technischen und betriebswirtschaftlichen Anforderungen Ihrer Workload.

## <a name="identify-compute-services-requirements"></a>Bestimmen von Anforderungen der Computedienste

Im Rahmen der Evaluierung und Vorbereitung Ihrer Landezone müssen Sie alle Computeressourcen bestimmen, die von Ihrer Landezone unterstützt werden müssen. Dieser Prozess umfasst die Bewertung der einzelnen Anwendungen und Dienste, aus denen Ihre Workloads bestehen, um die Compute- und Hostinganforderungen zu bestimmen. Nachdem Sie Ihre Anforderungen identifiziert und dokumentiert haben, können Sie Richtlinien für Ihre Landezone erstellen und steuern, welche Ressourcentypen basierend auf Ihren Workloadanforderungen zulässig sind.

Verwenden Sie für alle Anwendungen oder Dienste, die Sie in Ihrer Landezonenumgebung bereitstellen, die folgende Entscheidungsstruktur als Ausgangspunkt für die Ermittlung der Anforderungen der Computedienste:

![Entscheidungsstruktur: Azure-Computedienste](../../_images/ready/compute-decision-tree.png)
_Abbildung 1: Entscheidungsstruktur für Azure-Computedienste._

> [!NOTE]
> Weitere Informationen zum Bewerten von Computeoptionen für die einzelnen Anwendungen oder Dienste finden Sie im [Leitfaden zur Azure-Anwendungsarchitektur](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-decision-tree).

### <a name="key-questions"></a>Kernfragen

Die Beantwortung der folgenden Fragen zu Ihren Workloads ist hilfreich, um basierend auf der Entscheidungsstruktur für Azure-Computedienste Entscheidungen treffen zu können:

- **Erstellen Sie neue Anwendungen und Dienste, oder migrieren Sie von bestehenden lokalen Workloads?** Die Entwicklung neuer Anwendungen im Rahmen Ihrer Cloudeinführungsmaßnahmen ermöglicht es Ihnen, die Vorteile moderner cloudbasierter Hostingtechnologien bereits ab der Entwurfsphase voll auszuschöpfen.
- **Wenn Sie bestehende Workloads migrieren, können diese dann die Vorteile moderner Cloudtechnologien nutzen?** Zum Migrieren von lokalen Workloads ist eine Analyse erforderlich. Können Sie vorhandene Anwendungen und Dienste auf einfache Weise optimieren, um moderne Cloudtechnologien zu nutzen, oder funktioniert für Ihre Workloads ein Ansatz per Lift & Shift besser?
- **Können Ihre Anwendungen oder Dienste Container nutzen?** Wenn sich Ihre Anwendungen gut für ein containerisiertes Hosting eignen, können Sie die Vorteile der Ressourceneffizienz, Skalierbarkeit und Orchestrierung nutzen, die von [Containerdiensten in Azure](https://azure.microsoft.com/product-categories/containers) bereitgestellt werden. Sowohl [verwaltete Azure-Datenträger](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) als auch [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) können für die permanente Speicherung in containerisierten Anwendungen verwendet werden.
- **Sind Ihre Anwendungen web- oder API-basiert, und verwenden sie PHP, ASP.NET, Node.js oder ähnliche Technologien?** Web-Apps können für verwaltete [App Service](https://docs.microsoft.com/azure/app-service/overview)-Instanzen bereitgestellt werden, sodass keine virtuelle Computer für Hostingzwecke verwaltet werden müssen.
- **Benötigen Sie die volle Kontrolle über das Betriebssystem und die Hostingumgebung Ihrer Workload?** Wenn Sie die Hostingumgebung, einschließlich Betriebssystem, Datenträger, lokal ausgeführte Software und andere Konfigurationen, steuern müssen, können Sie für das Hosting Ihrer Anwendungen und Dienste [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines) verwenden. Zusätzlich zur Auswahl der Größen und Leistungsstufen Ihres virtuellen Computers wirken sich Ihre Entscheidungen hinsichtlich des Speichers virtueller Datenträger auf die Leistung und SLAs aus, die mit ihren IaaS-Workloads (Infrastructure-as-a-Service) in Zusammenhang stehen. Weitere Informationen finden Sie in der Dokumentation zu [Azure Disk Storage](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).
- **Umfasst ihre Workload HPC-Funktionen (High Performance Computing)?** [Azure Batch](https://docs.microsoft.com/azure/batch/batch-technical-overview) ermöglicht eine Auftragsplanung und automatische Skalierung von Computeressourcen, sodass Sie problemlos umfangreiche parallele und HPC-Anwendungen in der Cloud ausführen können.
- **Werden Ihre Anwendungen eine Microservicesarchitektur verwenden?** Anwendungen, die eine Microservicearchitektur verwenden, können die Vorteile mehrerer optimierter Computetechnologien nutzen. Unabhängige, ereignisgesteuerte Workloads können mit [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview) skalierbare, serverlose Anwendungen erstellen, die keine Infrastruktur benötigen. Für Anwendungen, die mehr Kontrolle über die Umgebung erfordern, in der Microservices ausgeführt werden, können Sie Containerdienste wie [Azure Container Instances](https://docs.microsoft.com/azure/container-instances/container-instances-overview), [Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/intro-kubernetes) und [Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) verwenden.

> [!NOTE]
> Die meisten Azure-Computedienste werden in Verbindung mit Azure Storage verwendet. Lesen Sie zu den damit verbundenen Speicherentscheidungen die [Anleitungen zu Speicherentscheidungen](./storage-options.md).

## <a name="common-compute-scenarios"></a>Gängige Computeszenarien

In der folgenden Tabelle sind einige häufige Nutzungsszenarien und die empfohlenen Computedienste für die Verarbeitung aufgeführt:

| Szenario  | Computedienst |
| --- | --- |
| Ich muss virtuelle Linux- und Windows-Computer innerhalb weniger Sekunden mit den gewünschten Konfigurationen bereitstellen. | [Dokumentation zu virtuellen Computern](https://azure.microsoft.com/services/virtual-machines) |
| Ich muss Hochverfügbarkeit durch automatische Skalierung von Tausenden von VMs in wenigen Minuten erzielen. | [Skalierungsgruppen für virtuelle Computer](https://azure.microsoft.com/services/virtual-machine-scale-sets) |
| Ich möchte die Bereitstellung, die Verwaltung und den Betrieb von Kubernetes vereinfachen. | [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service) |
| Ich muss die App-Entwicklung durch eine ereignisgesteuerte, serverlose Architektur beschleunigen. | [Azure-Funktionen](https://azure.microsoft.com/services/functions) |
| Ich muss Microservices entwickeln und Container unter Windows oder Linux orchestrieren. | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) |
| Ich möchte schnell Cloud-Apps für Web- und mobile Anwendungen mit einer vollständig verwalteten Plattform erstellen. | [Azure App Service](https://azure.microsoft.com/services/app-service) |
| Ich möchte App-Containern erstellen und diese Container auf einfache Weise mit einem einzigen Befehl ausführen. | [Azure Container Instances](https://azure.microsoft.com/services/container-instances) |
| Ich benötige eine cloudbasierte Auftragsplanung und Computeverwaltung mit der Möglichkeit, eine Skalierung auf Dutzende, Hunderte oder Tausende von virtuellen Computern auszuführen. | [Azure Batch](https://azure.microsoft.com/services/batch) |
| Ich muss hochverfügbare, skalierbare Cloudanwendungen und APIs erstellen, mit denen ich mich auf Apps anstatt auf die Hardware konzentrieren kann. | [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services) |

## <a name="regional-availability"></a>Regionale Verfügbarkeit

Mit Azure können Sie Dienste in der Größenordnung bereitstellen, die Sie benötigen, um Ihre Kunden und Partner zu erreichen, **wo auch immer diese sich befinden**. Ein wichtiger Faktor bei der Planung Ihrer Cloudbereitstellung ist die Ermittlung, in welcher Azure-Region Ihre Workloadressourcen gehostet werden.

Einige Computeoptionen wie z. B. Azure App Service sind in den meisten Azure-Regionen allgemein verfügbar, während andere Computedienste nur in bestimmten Regionen unterstützt werden. Einige Typen von virtuellen Computern und die zugehörigen Speichertypen haben eine begrenzte regionale Verfügbarkeit. Bevor Sie die Entscheidung treffen, in welchen Regionen Sie Ihre Computeressourcen bereitstellen, empfehlen wir Ihnen die [Seite zu den Regionen](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=azure-vmware-cloudsimple,cloud-services,batch,container-instances,app-service,service-fabric,functions,kubernetes-service,virtual-machine-scale-sets,virtual-machines), um den aktuellen Status der regionalen Verfügbarkeit zu überprüfen.

Sie können die [Seite „Azure-Regionen“](https://azure.microsoft.com/global-infrastructure/regions) besuchen, um weitere Informationen zur globalen Azure-Infrastruktur zu erhalten. Sie können auch die Seite mit den [verfügbaren Produkten nach Region](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) verwenden, um spezifische Informationen dazu zu erhalten, welche Dienste in den einzelnen Azure-Regionen verfügbar sind.

## <a name="data-residency-and-compliance-requirements"></a>Anforderungen an Datenresidenz und -konformität

Häufig gelten für Ihre Workloads rechtliche und vertragliche Anforderungen in Bezug auf die Datenspeicherung. Diese Anforderungen können je nach Standort Ihrer Organisation, dem Gerichtsstand, in dem Dateien und Daten gespeichert und verarbeitet werden, und Ihrer jeweiligen Branche variieren. Für das Berücksichtigen von Datenverpflichtungen sind die Datenklassifizierung, der Datenstandort und die entsprechenden Zuständigkeiten für den Schutz der Daten im Rahmen des Modells für die gemeinsame Verantwortung wichtig. Viele Computelösungen sind von verknüpften Speicherressourcen abhängig. Diese Anforderung kann sich auch auf Ihre Computeentscheidungen auswirken. Hilfe zum Verständnis dieser Anforderungen finden Sie im Whitepaper [Sicherheit und Compliance bei der Speicherung von Benutzerdaten mit Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Ein Teil ihrer Compliancemaßnahmen kann die Steuerung des physischen Speicherorts ihrer Computeressourcen umfassen. Azure-Regionen sind in Gruppen organisiert, die als „Geografien“ bezeichnet werden. Eine [Azure-Geografie](https://azure.microsoft.com/global-infrastructure/geographies) sorgt dafür, dass Anforderungen an Datenresidenz, Datenhoheit, Compliance und Ausfallsicherheit innerhalb geografischer Grenzen erfüllt werden. Wenn für Ihre Workloads Anforderungen an die Datenhoheit oder andere Complianceanforderungen bestehen, müssen die Speicherressourcen in den Regionen in einer konformen Azure-Geografie bereitgestellt werden.

## <a name="establish-controls-for-compute-services"></a>Einrichten von Kontrollelementen für Computedienste

Wenn Sie Ihre Landezonenumgebung vorbereiten, können Sie Kontrollelemente einrichten, die einschränken, welche Ressourcen von den einzelnen Benutzern bereitgestellt werden können. Diese Kontrollelemente können Ihnen als Hilfe beim Verwalten von Kosten und Eindämmen von Sicherheitsrisiken dienen, während Entwickler und IT-Teams weiterhin Ressourcen bereitstellen und konfigurieren können, die zum Unterstützen Ihrer Workloads benötigt werden.

Nachdem Sie die Anforderungen Ihrer Landezone identifiziert und dokumentiert haben, können Sie [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) nutzen, um zu steuern, welche Computeressourcen von Benutzern erstellt werden dürfen. Kontrollelemente können [die Erstellung von Computeressourcentypen zulassen oder verweigern](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types). Beispielsweise können Sie festlegen, dass Benutzer nur Azure App Service- oder Azure Functions-Ressourcen erstellen können. Mit Policy können auch die zulässigen Optionen beim Erstellen einer Ressource gesteuert werden, z.B. das [Einschränken der Bereitstellung von SKUs für virtuelle Computer](https://docs.microsoft.com/azure/governance/policy/samples/built-in-policies#compute) oder das [Zulassen nur von bestimmten VM-Images](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

Der Bereich von Richtlinien kann auf Ressourcen, Ressourcengruppen, Abonnements oder Verwaltungsgruppen festgelegt werden. Darüber hinaus können diese Richtlinien auch in [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview)-Definitionen eingebunden und in der gesamten Cloudumgebung wiederholt angewendet werden.
