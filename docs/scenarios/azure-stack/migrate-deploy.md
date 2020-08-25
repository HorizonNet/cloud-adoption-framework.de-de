---
title: Bereitstellen von Workloads in Azure Stack Hub
description: Hier erfahren Sie, wie Sie Workloads mithilfe von Azure Stack Hub in Ihrem Rechenzentrum bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 86c1d4b7eaea3c7de15dfd4417a6bcc21d956ea8
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88569636"
---
# <a name="deploy-workloads-to-azure-stack-hub"></a>Bereitstellen von Workloads in Azure Stack Hub

Durch die Verwendung von Azure Stack kann Ihre Organisation eine eigene Instanz von Azure in ihrem Rechenzentrum betreiben. Organisationen integrieren Azure Stack in Ihre Cloudstrategie, weil sie damit Situationen bewältigen können, in denen die öffentliche Cloud nicht für sie funktioniert. Die drei häufigsten Gründe für die Verwendung von Azure Stack sind:

- Schlechte Netzwerkkonnektivität mit der öffentlichen Cloud.
- Gesetzliche oder vertragliche Anforderungen.
- Back-End-Systeme, die nicht mit dem Internet verbunden werden können.

## <a name="infrastructure-as-a-service-deployment"></a>Infrastructure-as-a-Service-Bereitstellung

Unabhängig vom Grund für die Infrastructure-as-a-Service-Bereitstellung (IaaS) ist die Bereitstellung in Azure Stack Hub ähnlich wie jede andere IaaS-Bereitstellung. Oft wird IaaS nur mit virtuellen Computern (VMs) in Verbindung gebracht, aber IaaS ist mehr als das. Eine VM, die Sie in Azure oder Azure Stack bereitstellen, verfügt über ein softwaredefiniertes Netzwerk, einschließlich Domain Name System, öffentlicher IP-Adressen und Firewallregeln (auch bezeichnet als Netzwerksicherheitsgruppen), sowie viele weitere Funktionen. Bei der VM-Bereitstellung werden auch Datenträger für Ihre VMs in softwaredefiniertem Speicher mit Azure Blob Storage erstellt.

Eine ausführliche Anleitung zum Bereitstellen von VMs in Azure Stack finden Sie in der [Einführung in Azure Stack Hub-VMs](/azure-stack/user/azure-stack-compute-overview?view=azs-2002).

## <a name="platform-as-a-service-deployment"></a>Platform-as-a-Service-Bereitstellung

In der Cloud werden alle Platform-as-a-Service-Ressourcen (PaaS) in einem Infrastrukturdienst ausgeführt, z. B. auf einer VM. Azure-Dienste „verschleiern“ diese Back-End-Ressourcen jedoch, sodass Sie sie nicht verwalten müssen. Die Obfuskation und Koordination dieser Infrastrukturressourcen wird von Azure Resource Manager verwaltet. Bei der Bereitstellung in Azure mit einer Azure Resource Manager-Vorlage haben Sie vielleicht einen Aspekt von Resource Manager kennen gelernt. Diese Vorlagen weisen Azure an, welche Ressourcenanbieter Sie aufrufen möchten und wie Ihre Ressourcen konfiguriert werden sollen.

Wenn die Cloud in Ihrem Rechenzentrum ausgeführt wird, müssen Ihre Stack Hub-Administratoren zumindest grundlegend mit den Ebenen der Obfuskation vertraut sein. Bevor Ihre Benutzer oder Entwickler eine PaaS-Ressource verwenden können, muss der Azure Stack Hub-Administrator den Ressourcenanbieter über den Marketplace installieren. Diese Ressourcenanbieter ermöglichen es Ihrer Instanz von Azure Stack Hub, die Ressourcenanbieterfunktionalität von Azure in Ihrer Stack-Instanz zu replizieren. Weitere Informationen zum Bereitstellen von Azure Stack Hub-Ressourcenanbietern finden Sie in der [Blogreihe zu Azure Stack IaaS](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/).

## <a name="deploy-workloads"></a>Bereitstellen von Workloads

Nachdem der Azure Stack Hub-Administrator die Stack-Instanz korrekt konfiguriert hat, können Migrationen wie bei den meisten anderen Azure-Migrationsprozessen fortgesetzt werden. Durch die Verwendung von Azure Stack kann Ihr Team eine der folgenden Arten der Migration durchführen:

<!-- cSpell:ignore howto -->

- [Ethereum-Blockchain-Netzwerk](/azure-stack/user/azure-stack-ethereum?view=azs-2002)
- [AKS-Engine](/azure-stack/user/azure-stack-kubernetes-aks-engine-overview?view=azs-2002)
- [Azure Cognitive Services](/azure-stack/user/azure-stack-solution-template-cognitive-services?view=azs-2002)
- [C#-Web-App (ASP.NET)](/azure-stack/user/azure-stack-dev-start-howto-vm-dotnet?view=azs-2002)
- [Linux-VM](/azure-stack/user/azure-stack-dev-start-howto-deploy-linux?view=azs-2002)
- [Java-Web-App](/azure-stack/user/azure-stack-dev-start-howto-vm-java?view=azs-2002)

## <a name="additional-considerations-during-migration"></a>Weitere Überlegungen während der Migration

In den folgenden Artikeln finden Sie Informationen, die Ihrem Team bei der Migration und Modernisierung helfen können:

- [Skalierbarkeits- und Verfügbarkeitsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-six/) wie nutzungsbasierte Bezahlung, VM-Verfügbarkeitsgruppen, VM-Skalierungsgruppen, Netzwerkadapter sowie die Möglichkeit, VMs und Datenträger hinzuzufügen und ihre Größe zu ändern
- [Speicherkapazität](https://azure.microsoft.com/blog/azure-stack-iaas-part-3/), einschließlich der Möglichkeit zum Hoch- und Herunterladen sowie zum Erfassen und Bereitstellen von VM-Images
- GitHub-Repository mit [Schnellstartvorlagen für Azure Stack](https://github.com/Azure/AzureStack-QuickStart-Templates)
- GitHub-Repository mit [Schnellstartvorlagen für Azure](https://github.com/Azure/Azure-QuickStart-Templates)

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
