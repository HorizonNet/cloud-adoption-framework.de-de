---
title: Bereitstellen einer grundlegenden Workload
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hier erfahren Sie, wie Sie eine grundlegende Workload in Azure bereitstellen.
author: alexbuckgit
ms.author: abuck
ms.date: 12/31/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5c3fcb72fc58f4b33735a95a7fcf1623fe081795
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548103"
---
# <a name="deploy-a-basic-workload-in-azure"></a>Bereitstellen einer grundlegenden Workload in Azure

Der Begriff *Workload* bezeichnet in der Regel eine beliebige Funktionseinheit – etwa eine Anwendung oder einen Dienst. Unter einer Workload kann man sich die auf einem Server bereitgestellten Codeartefakte, aber auch andere für eine Anwendung erforderliche Dienste vorstellen. Dies ist möglicherweise eine hilfreiche Definition für eine lokale Anwendung oder einen lokalen Dienst, sie muss für Cloudanwendungen jedoch erweitert werden.

In der Cloud umfasst eine Workload nicht nur sämtliche Artefakte, sondern auch die Cloudressourcen. Cloudressourcen werden aufgrund eines Konzepts namens „Infrastructure-as-Code“ in die Definition einbezogen. Wie Sie in [Wie funktioniert Azure?](../../getting-started/what-is-azure.md) erfahren haben, werden Ressourcen in Azure durch einen Orchestratordienst bereitgestellt. Dieser Orchestratordienst macht Funktionen über eine Web-API verfügbar, und Sie können die Web-API über verschiedene Tools aufrufen. Hierzu zählen etwa PowerShell, die Azure CLI und das Azure-Portal. Folglich können Sie Azure-Ressourcen in einer maschinenlesbaren Datei angeben, die zusammen mit den Codeartefakten für die Anwendung gespeichert werden kann.

Dadurch können Sie eine Workload als Codeartefakte und die erforderlichen Cloudressourcen definieren und somit die Workloads isolieren. Die Isolierung von Workloads kann auf der Art der Ressourcenstrukturierung, auf der Netzwerktopologie oder auf anderen Attributen basieren. Die Workloadisolierung dient dazu, die spezifischen Ressourcen einer Workload einem Team zuzuordnen, damit das Team alle Aspekte dieser Ressourcen unabhängig verwalten kann. Dies ermöglicht die gemeinsame Nutzung von Ressourcenverwaltungsdiensten in Azure durch mehrere Teams und verhindert gleichzeitig die versehentliche Löschung oder Änderung fremder Ressourcen.

Darüber hinaus ermöglicht diese Isolierung ein weiteres Konzept namens DevOps. DevOps umfasst die Softwareentwicklungsverfahren, die neben der Softwareentwicklung und den IT-Vorgängen von weiter oben auch eine möglichst weitreichende Automatisierung beinhaltet. Zu den Prinzipien von DevOps zählen unter anderem Continuous Integration und Continuous Delivery (CI/CD). Continuous Integration bezieht sich auf die automatisierten Buildprozesse, die jedes Mal ausgeführt werden, wenn ein Entwickler eine Codeänderung committet. Continuous Delivery bezieht sich auf die automatisierten Prozesse, die diesen Code in verschiedenen Umgebungen bereitstellen (beispielsweise zu Testzwecken in einer Entwicklungsumgebung oder zur endgültigen Bereitstellung in einer Produktionsumgebung).

## <a name="basic-workload"></a>Grundlegende Workload

Eine *grundlegende Workload* wird üblicherweise als einzelne Webanwendung oder als virtuelles Netzwerk (VNET) mit virtuellem Computer (Virtual Machine, VM) definiert.

> [!NOTE]
> Die Anwendungsentwicklung wird in diesem Leitfaden nicht behandelt. Weitere Informationen zur Entwicklung von Anwendungen in Azure finden Sie im [Azure-Anwendungsarchitekturleitfaden](https://docs.microsoft.com/azure/architecture/guide).

Jede dieser Bereitstellungen erfordert eine *Ressourcengruppe* – ganz gleich, ob es sich bei der Workload um eine Webanwendung oder um einen virtuellen Computer handelt. Daher muss ein Benutzer mit entsprechender Berechtigung eine Ressourcengruppe erstellen, bevor Sie mit den folgenden Schritten fortfahren.

## <a name="basic-web-application-paas"></a>Einfache Webanwendung (PaaS)

Wählen Sie für eine einfache Webanwendung eine der 5-Minuten-Schnellstartanleitungen der [Dokumentation zu Web-Apps](https://docs.microsoft.com/azure/app-service?toc=/azure/architecture/cloud-adoption-guide/toc.json) aus, und führen Sie die jeweiligen Schritte aus.

> [!NOTE]
> In einigen Schnellstartanleitungen wird standardmäßig eine Ressourcengruppe bereitgestellt. In diesem Fall muss nicht explizit eine Ressourcengruppe erstellt werden. Stellen Sie die Webanwendung andernfalls in der oben erstellten Ressourcengruppe bereit.

Nachdem Sie eine einfache Workload bereitgestellt haben, können Sie sich weiter über die Best Practices zur Bereitstellung einer [einfachen Webanwendung](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/basic-web-app?toc=/azure/architecture/cloud-adoption-guide/toc.json) in Azure informieren.

## <a name="single-windows-or-linux-vm-iaas"></a>Einzelne Windows- oder Linux-VM (IaaS)

Für eine einfache Workload, die auf einer VM ausgeführt wird, ist der erste Schritt das Bereitstellen eines virtuellen Netzwerks. Für alle IaaS-Ressourcen (Infrastructure-as-a-Service) in Azure, z.B. virtuelle Computer, Lastenausgleiche und Gateways, ist ein virtuelles Netzwerk erforderlich. Erfahren Sie mehr zu [virtuellen Azure-Netzwerken](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview?toc=/azure/architecture/cloud-adoption-guide/toc.json), und führen Sie die Schritte zum [Bereitstellen eines virtuellen Netzwerks in Azure mit dem Portal](https://docs.microsoft.com/azure/virtual-network/quick-create-portal?toc=/azure/architecture/cloud-adoption-guide/toc.json) aus. Geben Sie unbedingt den Namen der oben erstellten Ressourcengruppe an, wenn Sie die Einstellungen für das virtuelle Netzwerk im Azure-Portal festlegen.

Der nächste Schritt ist die Entscheidung, ob eine einzelne Windows- oder Linux-VM bereitgestellt werden soll. Führen Sie für eine Windows-VM die Schritte zum [Bereitstellen eines virtuellen Windows-Computers in Azure mit dem Portal](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal?toc=/azure/architecture/cloud-adoption-guide/toc.json) aus. Geben Sie wieder den Namen der oben erstellten Ressourcengruppe an, wenn Sie die Einstellungen für den virtuellen Computer im Azure-Portal festlegen.

Nachdem Sie die Schritte ausgeführt und die VM bereitgestellt haben, können Sie sich über die [Best Practices für das Ausführen eines virtuellen Windows-Computers in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/single-vm?toc=/azure/architecture/cloud-adoption-guide/toc.json) informieren. Führen Sie für eine Linux-VM die Schritte zum [Bereitstellen eines virtuellen Linux-Computers in Azure mit dem Portal](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal?toc=/azure/architecture/cloud-adoption-guide/toc.json) aus. Außerdem können Sie sich über die [Best Practices für das Ausführen eines virtuellen Linux-Computers in Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-linux/single-vm?toc=/azure/architecture/cloud-adoption-guide/toc.json) informieren.

## <a name="next-steps"></a>Nächste Schritte

Hinweise zur Verwendung wichtiger Infrastrukturkomponenten in der Azure-Cloud finden Sie im [Leitfaden zur architekturbezogenen Entscheidungsfindung](../../decision-guides/index.md).
