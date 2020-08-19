---
title: Erstellen von Zeitplänen für Updates
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Zeitpläne für Updates mit dem Azure-Portal oder den neuen PowerShell-Cmdlet-Modulen verwalten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c418233559d93b59a468caa24fe43984184898ec
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88574940"
---
# <a name="create-update-schedules"></a>Erstellen von Zeitplänen für Updates

Sie können Zeitpläne für Updates über das Azure-Portal oder die neuen PowerShell-Cmdlet-Module verwalten.

Informationen zum Erstellen eines Zeitplans für Updates über das Azure-Portal finden Sie unter [Planen einer Updatebereitstellung](/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

Das Modul `Az.Automation` unterstützt jetzt die Konfiguration der Updateverwaltung mit Azure PowerShell. Die [Version 1.7.0](https://www.powershellgallery.com/packages/Az/1.7.0) des Moduls bietet Unterstützung für das Cmdlet [New-AzAutomationUpdateManagementAzureQuery](/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0). Mit diesem Cmdlet können Sie Tags, Speicherort und gespeicherte Suchen verwenden, um Zeitpläne für Updates für eine flexible Gruppe von Computern zu konfigurieren.

## <a name="example-script"></a>Beispielskript

Das Beispielskript in diesem Abschnitt veranschaulicht die Verwendung von Tagging und Abfragen zum Erstellen dynamischer Gruppen von Computern, auf die Sie Zeitpläne für Updates anwenden können. Es führt die folgenden Aktionen aus. Sie können bei der Erstellung eigener Skripte auf die Implementierungen der einzelnen Aktionen verweisen.

- Erstellt einen Azure Automation-Updatezeitplan, der jeden Samstag um 8:00 Uhr ausgeführt wird.
- Erstellt eine Abfrage für alle Computer, die den folgenden Kriterien entsprechen:
  - Am Azure-Standort `westus`, `eastus` oder `eastus2` bereitgestellt.
  - Verfügt über ein `Owner`-Tag mit einem auf `JaneSmith` festgelegten Wert.
  - Verfügt über ein `Production`-Tag mit einem auf `true` festgelegten Wert.
- Wendet den Updatezeitplan auf die abgefragten Computer an und legt ein zweistündiges Updatefenster fest.

Bevor Sie das Beispielskript ausführen, müssen Sie sich mit dem Cmdlet [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) anmelden. Stellen Sie beim Starten des Skripts die folgenden Informationen zur Verfügung:

- Zielabonnement-ID
- Zielressourcengruppe
- Name des Log Analytics-Arbeitsbereichs
- Azure Automation-Kontoname

```powershell

    <#
        .SYNOPSIS
            This script orchestrates the deployment of the solutions and the agents.
        .Parameter SubscriptionName
        .Parameter WorkspaceName
        .Parameter AutomationAccountName
        .Parameter ResourceGroupName

    #>

    param (
        [Parameter(Mandatory=$true)]
        [string] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [string] $ResourceGroupName,

        [Parameter(Mandatory=$true)]
        [string] $WorkspaceName,

        [Parameter(Mandatory=$true)]
        [string] $AutomationAccountName,

        [Parameter(Mandatory=$false)]
        [string] $scheduleName = "SaturdayCriticalSecurity"
    )

    Import-Module Az.Automation

    $startTime = ([DateTime]::Now).AddMinutes(10)
    $schedule = New-AzAutomationSchedule -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -StartTime $startTime `
        -Name $scheduleName `
        -Description "Saturday patches" `
        -DaysOfWeek Saturday `
        -WeekInterval 1 `
        -ForUpdateConfiguration

    # Using AzAutomationUpdateManagementAzureQuery to create dynamic groups.

    $queryScope = @("/subscriptions/$SubscriptionID/resourceGroups/")

    $query1Location =@("westus", "eastus", "eastus2")
    $query1FilterOperator = "Any"
    $ownerTag = @{ "Owner"= @("JaneSmith") }
    $ownerTag.Add("Production", "true")

    $DGQuery = New-AzAutomationUpdateManagementAzureQuery -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Scope $queryScope `
        -Tag $ownerTag

    $AzureQueries = @($DGQuery)

    $UpdateConfig = New-AzAutomationSoftwareUpdateConfiguration -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Schedule $schedule `
        -Windows `
        -Duration (New-TimeSpan -Hours 2) `
        -AzureQuery $AzureQueries `
        -IncludedUpdateClassification Security,Critical
```

## <a name="next-steps"></a>Nächste Schritte

Hier finden Sie Beispiele für die Implementierung von [allgemeinen Richtlinien in Azure](./common-policies.md), die Ihnen bei der Verwaltung Ihrer Server helfen können.

> [!div class="nextstepaction"]
> [Allgemeine Richtlinien in Azure](./common-policies.md)
