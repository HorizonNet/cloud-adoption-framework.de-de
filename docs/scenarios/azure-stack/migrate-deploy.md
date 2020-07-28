---
title: Bereitstellen von Workloads in Azure Stack Hub
description: Hier erfahren Sie, wie Sie Workloads mithilfe von Azure Stack Hub in Ihrem Rechenzentrum bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2e29dcf36d0da76d72187fb895f6108e7a9dd2b5
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452748"
---
# <a name="deploy-workloads-to-azure-stack-hub"></a>Bereitstellen von Workloads in Azure Stack Hub

Azure Stack bietet Kunden die Möglichkeit, eine eigene Instanz von Azure in Ihrem Rechenzentrum auszuführen. Organisationen integrieren Azure Stack in Ihre Cloudstrategie, weil sie damit Situationen bewältigen können, in denen die öffentliche Cloud nicht für sie funktioniert. Die drei häufigsten Gründe für die Verwendung von Azure Stack sind eine schlechte Netzwerkverbindung mit der öffentlichen Cloud, gesetzliche oder vertragliche Anforderungen und Back-End-Systeme, die nicht im Internet verfügbar gemacht werden können.

## <a name="infrastructure-as-a-service-iaas-deployment"></a>Infrastructure-as-a-Service-Bereitstellung (IaaS)

Die Bereitstellung in Azure Stack Hub ähnelt jeder anderen IaaS-Bereitstellung – ganz gleich, aus welchem Grund Sie sich dafür entscheiden. Viele denken bei IaaS nur an VMs, doch dies ist deutlich zu kurz gegriffen. Eine VM, die Sie in Azure oder Azure Stack bereitstellen, verfügt über ein softwaredefiniertes Netzwerk, einschließlich DNS, öffentlicher IP-Adressen und Firewallregeln (auch bezeichnet als Netzwerksicherheitsgruppen), sowie viele weitere Funktionen. Bei der VM-Bereitstellung werden auch Datenträger für Ihre VMs in softwaredefiniertem Speicher mit Azure Blob Storage erstellt.

Eine ausführliche Anleitung zum Bereitstellen von VMs in Azure Stack finden Sie in der [Einführung in Azure Stack Hub-VMs](https://docs.microsoft.com/azure-stack/user/azure-stack-compute-overview?view=azs-2002).

## <a name="platform-as-a-service-paas-deployment"></a>Platform-as-a-Service-Bereitstellung (PaaS)

In der Cloud werden alle PaaS-Ressourcen in einem Infrastrukturdienst ausgeführt, z. B. auf einer VM. Azure-Dienste „verschleiern“ diese Back-End-Ressourcen jedoch, sodass Sie sie nicht verwalten müssen. Die Obfuskation und Koordination dieser Infrastrukturressourcen wird von Azure Resource Manager verwaltet. Bei der Bereitstellung in Azure mit einer Azure Resource Manager-Vorlage haben Sie vielleicht einen Aspekt von Resource Manager kennen gelernt. Diese Vorlagen weisen Azure an, welche Ressourcenanbieter Sie aufrufen möchten und wie Ihre Ressourcen konfiguriert werden sollen.

Wenn die Cloud in Ihrem Rechenzentrum ausgeführt wird, müssen Ihre Stack Hub-Administratoren zumindest grundlegend mit den Ebenen der Obfuskation vertraut sein. Bevor Ihre Benutzer oder Entwickler eine PaaS-Ressource verwenden können, muss der Azure Stack Hub-Administrator den Ressourcenanbieter über den Marketplace installieren. Diese Ressourcenanbieter ermöglichen es Ihrer Instanz von Azure Stack Hub, die Ressourcenanbieterfunktionalität von Azure in Ihrer Stack-Instanz zu replizieren. Weitere Informationen zum Bereitstellen von Azure Stack Hub-Ressourcenanbietern finden Sie in der [Blogreihe zu Azure Stack IaaS](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/).

## <a name="deploy-workloads"></a>Bereitstellen von Workloads

Nachdem der Azure Stack Hub-Administrator die Stack-Instanz korrekt konfiguriert hat, können Migrationen wie bei den meisten anderen Azure-Migrationsprozessen fortgesetzt werden. Im Folgenden finden Sie Links zu einigen spezifischen Migrationstypen, die Kunden häufig in Azure Stack ausführen:

- [Ethereum-Blockchain-Netzwerk](https://docs.microsoft.com/azure-stack/user/azure-stack-ethereum?view=azs-2002)
- [AKS-Engine](https://docs.microsoft.com/azure-stack/user/azure-stack-kubernetes-aks-engine-overview?view=azs-2002)
- [Azure Cognitive Services](https://docs.microsoft.com/azure-stack/user/azure-stack-solution-template-cognitive-services?view=azs-2002)
- [C#-Web-App (ASP.NET)](https://docs.microsoft.com/azure-stack/user/azure-stack-dev-start-howto-vm-dotnet?view=azs-2002)
- [Linux-VM](https://docs.microsoft.com/azure-stack/user/azure-stack-dev-start-howto-deploy-linux?view=azs-2002)
- [Java-Web-App](https://docs.microsoft.com/azure-stack/user/azure-stack-dev-start-howto-vm-java?view=azs-2002)

## <a name="additional-considerations-during-migration"></a>Weitere Überlegungen während der Migration

In den folgenden Artikeln finden Sie Informationen, die Ihrem Team bei der Migration und Modernisierung helfen können:

- [Skalierbarkeits- und Verfügbarkeitsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-six/) wie nutzungsbasierte Bezahlung, VM-Verfügbarkeitsgruppen, VM-Skalierungsgruppen, Netzwerkadapter sowie die Möglichkeit, VMs und Datenträger hinzuzufügen und ihre Größe zu ändern
- [Speicherkapazität](https://azure.microsoft.com/blog/azure-stack-iaas-part-3/), einschließlich der Möglichkeit zum Hoch- und Herunterladen sowie zum Erfassen und Bereitstellen von VM-Images
- GitHub-Repository mit [Schnellstartvorlagen für Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates)
- GitHub-Repository mit [Schnellstartvorlagen für Azure](https://github.com/Azure/Azure-QuickStart-Templates)

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Nächster Schritt: Integrieren dieser Strategie in Ihre Cloudeinführungsjourney

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney.

- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
