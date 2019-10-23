---
title: Gastkonfigurationsrichtlinie
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Gastkonfigurationsrichtlinie
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 16d67f628ff99f971d2d79127b25698987cc8977
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547269"
---
# <a name="guest-configuration-policy"></a>Gastkonfigurationsrichtlinie

Die Erweiterung für die [Gastkonfiguration](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) von Azure Policy ermöglicht es Ihnen, Konfigurationseinstellungen in einem virtuellen Computer zu überprüfen. Die Gastkonfiguration wird derzeit nur auf virtuellen Azure-Computern unterstützt.

Sie können die Liste der Gastkonfigurationsrichtlinien finden, indem Sie nach der Kategorie „Gastkonfiguration“ auf der Portalseite von Azure Policy suchen. Sie können auch das folgende Cmdlet in einem PowerShell-Fenster ausführen, um die Liste zu finden:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Die Funktionalität der Gastkonfiguration wird regelmäßig aktualisiert, um zusätzliche Richtliniensätze zu unterstützen. Überprüfen Sie regelmäßig auf neue unterstützte Richtlinien und bewerten Sie, ob diese für Ihre Anforderungen nützlich sind.

<!-- TODO: Update these links when available. 

By default, we recommend enabling the following policies:

- [Preview]: Audit to verify password security settings are set correctly inside Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Bereitstellung

Sie können das folgende PowerShell-Beispielskript verwenden, um diese Richtlinien bereitzustellen:

- Überprüfen Sie, ob die Einstellungen für die Kennwortsicherheit auf Windows- und Linux-Computern ordnungsgemäß eingestellt sind.
- Stellen Sie sicher, dass Zertifikate auf virtuellen Windows-Computern nicht in Kürze ablaufen.

 Bevor Sie dieses Skript ausführen, müssen Sie sich mit dem Cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) anmelden. Wenn Sie das Skript ausführen, müssen Sie den Namen des Abonnements angeben, auf das Sie die Richtlinien anwenden möchten.

```powershell

    #Assign Guest Configuration policy.
    param (
        [Parameter(Mandatory=$true)]
        [string]$SubscriptionName
    )

    $Subscription = Get-AzSubscription -SubscriptionName $SubscriptionName
    $scope = "/subscriptions/" + $Subscription.Id

    $PasswordPolicy = Get-AzPolicySetDefinition -Name "3fa7cbf5-c0a4-4a59-85a5-cca4d996d5a6"
    $CertExpirePolicy = Get-AzPolicySetDefinition -Name "b6f5e05c-0aaa-4337-8dd4-357c399d12ae"

    New-AzPolicyAssignment -Name "PasswordPolicy" -DisplayName "[Preview]: Audit that password security settings are set correctly inside Linux and Windows machines" -Scope $scope -PolicySetDefinition $PasswordPolicy -AssignIdentity -Location eastus

    New-AzPolicyAssignment -Name "CertExpirePolicy" -DisplayName "[Preview]: Audit that certificates are not expiring on Windows VMs" -Scope $scope -PolicySetDefinition $CertExpirePolicy -AssignIdentity -Location eastus

```

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie die [Änderungsnachverfolgung und Warnungen](./enable-tracking-alerting.md) bei kritischen Änderungen an Dateien, Diensten, der Software und der Registrierung aktivieren können.

> [!div class="nextstepaction"]
> [Aktivieren von Nachverfolgung und Warnungen für kritische Änderungen](./enable-tracking-alerting.md)
