---
title: Allgemeine Azure Policy-Beispiele
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Allgemeine Azure Policy-Beispiele
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9eee6f81922c88304c0ca5bf7edd6572daf493d8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031439"
---
# <a name="common-azure-policy-examples"></a>Allgemeine Azure Policy-Beispiele

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) kann Ihnen helfen, Governance auf Ihre Cloudressourcen anzuwenden. Dieser Dienst kann Ihnen beim Erstellen von Leitlinien helfen, die die unternehmensweite Compliance mit den Anforderungen der Governancerichtlinien sicherstellen. Verwenden Sie zum Erstellen von Richtlinien entweder das Azure-Portal oder PowerShell-Cmdlets. Dieser Artikel enthält Beispiele für PowerShell-Cmdlets.

> [!NOTE]
> Mit Azure Policy werden Erzwingungsrichtlinien (**deployIfNotExists**) nicht automatisch auf vorhandenen virtuellen Computern bereitgestellt. Um die Compliance dieser virtuellen Computer sicherzustellen, ist eine Bereinigung erforderlich. Weitere Informationen finden Sie unter [Korrigieren nicht konformer Ressourcen mit Azure Policy](https://docs.microsoft.com/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Allgemeine Beispiele für Richtlinien

In den folgenden Abschnitten werden einige häufig verwendeten Richtlinien beschrieben.

### <a name="restrict-resource-regions"></a>Einschränken von Ressourcenbereichen

Die Vorschriften- und Richtliniencompliance hängt oft von der Kontrolle des physischen Standorts ab, an dem die Ressourcen bereitgestellt werden. Sie können eine integrierte Richtlinie verwenden, die es Benutzern gestattet, Ressourcen nur in den Azure-Regionen zu erstellen, die in einer Whitelist enthalten sind. Sie können diese Richtlinie im Portal finden, indem Sie auf der Richtliniendefinitionsseite nach „Standort“ suchen.

Alternativ können Sie dieses Cmdlet ausführen, um die Richtlinie zu finden:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*location*") }
```

Das folgende Skript zeigt, wie Sie die Richtlinie zuweisen. Um das Skript zu verwenden, ändern Sie den Wert `$SubscriptionID` so, dass er auf das Abonnement verweist, dem Sie die Richtlinie zuweisen möchten. Bevor Sie dieses Skript ausführen, müssen Sie sich mit dem Cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) anmelden.

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{"listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyparam
```

Sie können dasselbe Skript verwenden, um die anderen in diesem Artikel beschriebenen Richtlinien anzuwenden. Ersetzen Sie einfach die GUID in der Zeile, die `$AllowedLocationPolicy` festlegt, durch die GUID der Richtlinie, die Sie anwenden möchten.

### <a name="block-certain-resource-types"></a>Blockieren bestimmter Ressourcentypen

Eine weitere allgemeine integrierte Richtlinie zur Kostenkontrolle gestattet Ihnen das Blockieren bestimmter Ressourcentypen. Sie können diese Richtlinie im Portal finden, indem Sie auf der Richtliniendefinitionsseite nach „zulässigen Ressourcentypen“ suchen.

Alternativ können Sie dieses Cmdlet ausführen, um die Richtlinie zu finden:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

Nachdem Sie die zu verwendende Richtlinie identifiziert haben, können Sie das PowerShell-Beispiel im Abschnitt [Ressourcenregionen einschränken](#restrict-resource-regions) ändern, um diese Richtlinie zuzuweisen.

### <a name="restrict-vm-size"></a>Einschränken der Größe des virtuellen Computers

Azure bietet eine große Auswahl an VM-Größen, um die verschiedene Arten von Workloads zu unterstützen. Um Ihr Budget zu kontrollieren, können Sie eine Richtlinie erstellen, die nur eine Teilmenge der VM-Größen in Ihren Abonnements zulässt.

### <a name="deploy-antimalware"></a>Bereitstellen von Antischadsoftware

Mit dieser Richtlinie können Sie eine Microsoft IaaS-Antischadsoftwareerweiterung mit einer Standardkonfiguration auf virtuellen Computern bereitstellen, die nicht durch Antischadsoftware geschützt sind.

Die GUID der Richtlinie lautet `2835b622-407b-4114-9198-6f7064cbe0dc`.

Das folgende Skript zeigt, wie Sie die Richtlinie zuweisen. Um das Skript zu verwenden, ändern Sie den Wert `$SubscriptionID` so, dass er auf das Abonnement verweist, dem Sie die Richtlinie zuweisen möchten. Bevor Sie dieses Skript ausführen, müssen Sie sich mit dem Cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) anmelden.

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location “eastus” with the value you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Nächste Schritte

Erhalten Sie Informationen zu anderen verfügbaren Tools und Diensten für die Serververwaltung.

> [!div class="nextstepaction"]
> [Azure-Serververwaltungstools und -dienste](./tools-services.md)
