---
title: Optimieren und Höherstufen
description: Dieser Teil des Azure-Migrationsleitfadens behandelt Optimierungsbereiche, einschließlich der Überprüfung des Lösungsentwurfs, der richtigen Dimensionierung der Dienste und der Analyse der Kosten.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 3b7d6437e9e066497f55f8ce0bd601e7c53854f0
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892462"
---
<!-- cSpell:ignore Fservers Fdatabases -->

<!-- markdownlint-disable MD025 DOCSMD001 -->

# <a name="test-optimize-and-promote"></a>Testen, Optimieren und Höherstufen

Nachdem Sie Ihre Dienste zu Azure migriert haben, beinhaltet die nächste Phase die Überprüfung der Lösung auf mögliche Optimierungsbereiche. Dies kann die Überprüfung des Lösungsentwurfs, die richtige Größenbestimmung der Dienste und die Analyse der Kosten umfassen.

In dieser Phase bietet sich auch die Möglichkeit, die Umgebung zu optimieren und mögliche Transformationen der Umgebung durchzuführen. Angenommen, Sie haben z. B. eine „Rehosting“-Migration durchgeführt. Da Ihre Dienste nun in Azure ausgeführt werden, können Sie die Konfiguration oder genutzten Dienste der Lösung überprüfen und möglicherweise einige Refactoringvorgänge durchführen, um die Funktionen der Lösung zu modernisieren und zu erweitern.

Im weiteren Verlauf dieses Artikels werden die Tools zum Optimieren der migrierten Workload behandelt. Wenn die beste Leistungsverteilung und Kosteneffizienz erreicht wurde, kann eine Workload in die Produktion hochgestuft werden. Anleitungen zu den Optionen zum Höherstufen finden Sie in den Artikeln zur Prozessverbesserung zum [Optimieren und Höherstufen](../migration-considerations/optimize/index.md).

# <a name="right-size-assets"></a>[Größenbestimmung der Ressourcen](#tab/optimize)

Die Größe aller Azure-Dienste mit einem nutzungsbasierten Kostenmodell kann über das Azure-Portal, die Befehlszeilenschnittstelle oder PowerShell geändert werden. Der erste Schritt bei der Bestimmung der richtigen Größe eines Diensts ist die Überprüfung der zugehörigen Nutzungsmetriken. Der Azure Monitor-Dienst ermöglicht den Zugriff auf diese Metriken. Möglicherweise müssen Sie die Erfassung der Metriken für den zu analysierenden Dienst konfigurieren und eine angemessene Zeit einplanen, damit aussagekräftige Daten basierend auf Ihren Workloadmustern gesammelt werden.

1. Navigieren Sie zu **Monitor**.
1. Wählen Sie **Metriken** aus, und konfigurieren Sie das Diagramm so, dass Metriken für den zu analysierenden Dienst angezeigt werden.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/metrics]" submitText="Go to Monitor" :::

::: zone-end

Es folgen einige allgemeine Dienste, deren Größe Sie ändern können.

## <a name="resize-a-virtual-machine"></a>Ändern der Größe eines virtuellen Computers

In Azure Migrate wird als Teil der Bewertungsphase vor der Migration eine Analyse zur richtigen Größenanpassung durchgeführt, sodass die Größe virtueller Computer, die mit diesem Tool migriert werden, wahrscheinlich bereits entsprechend Ihren Anforderungen vor der Migration angepasst ist.

Bei virtuellen Computern, die mit anderen Methoden erstellt oder migriert wurden, oder in Fällen, bei denen eine Anpassung Ihrer Anforderungen für virtuelle Computer nach der Migration erforderlich ist, müssen Sie die Größenanpassung der virtuellen Computer möglicherweise optimieren.

1. Navigieren Sie zu **Virtuelle Computer**.
1. Wählen Sie den gewünschten virtuellen Computer in der Liste aus.
1. Wählen Sie **Größe** und die gewünschte neue Größe in der Liste aus. Möglicherweise müssen Sie die Filter anpassen, um die gewünschte Größe zu suchen.
1. Wählen Sie **Größe ändern** aus.

Ein Ändern der Größe von virtuellen Produktionscomputern kann zu Dienstunterbrechungen führen. Versuchen Sie, die Größenanpassung der virtuellen Computer vorzunehmen, bevor diese in der Produktionsumgebung verwendet werden.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

- [Verwalten von Reservierungen für Azure-Ressourcen](https://docs.microsoft.com/azure/billing/billing-manage-reserved-vm-instance)
- [Ändern der Größe eines virtuellen Windows-Computers](https://docs.microsoft.com/azure/virtual-machines/windows/resize-vm)
- [Ändern der Größe eines virtuellen Linux-Computers über die Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/azure/virtual-machines/linux/change-vm-size)

Partner können die Nutzung über das Partner Center überprüfen.

- [Microsoft Azure-VM-Größe für die maximale Reservierungsnutzung](https://docs.microsoft.com/partner-center/azure-usage)

::: zone-end

## <a name="resize-a-storage-account"></a>Ändern der Größe eines Speicherkontos

1. Navigieren Sie zu **Speicherkonten**.
1. Wählen Sie das gewünschte Speicherkonto aus.
1. Wählen Sie **Konfigurieren** aus, und passen Sie die Eigenschaften des Speicherkontos entsprechend Ihren Anforderungen an.
1. Wählen Sie **Speichern** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2FStorageAccounts]" submitText="Go to Storage Accounts" :::

::: zone-end

## <a name="resize-a-sql-database"></a>Ändern der Größe einer SQL-Datenbank

1. Navigieren Sie zu **SQL-Datenbanken** oder **SQL Server-Instanzen**, und wählen Sie dann den Server aus.
1. Wählen Sie die gewünschte Datenbank aus.
1. Wählen Sie **Konfigurieren** und die gewünschte neue Größe der Dienstebene aus.
1. Wählen Sie **Übernehmen**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Sql%2Fservers%2Fdatabases]" submitText="Go to SQL Databases" :::

::: zone-end

# <a name="cost-management"></a>[Cost Management](#tab/ManageCost)

Es ist wichtig, eine kontinuierliche Kostenanalyse und -überprüfung durchzuführen. Dadurch können Sie die Größe von Ressourcen nach Bedarf anpassen, um Kosten und Workload auszugleichen.

Azure Cost Management unterbreitet Ihnen mithilfe von Azure Advisor Empfehlungen zur Kostenoptimierung. Azure Advisor zeigt Ihnen Möglichkeiten der Optimierung und Steigerung der Effizienz auf, indem ungenutzte oder nicht ausreichend genutzte Ressourcen ermittelt werden.

1. Wählen Sie **Kostenverwaltung + Abrechnung** aus.
1. Wählen Sie **Ratgeberempfehlungen** und die Registerkarte **Kosten** aus.
1. Unter **Auswirkung** und **Mögliche Einsparung pro Jahr** können Sie die potenziellen Vorteile überprüfen.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" :::

::: zone-end

Sie können auch **Advisor** verwenden und die Registerkarte **Kosten** auswählen, um Empfehlungen für potenzielle Kosteneinsparungen anzuzeigen.

> [!TIP]
> Bei Diensten, für die keine kontinuierliche Verfügbarkeit erforderlich ist, kann die Implementierung einer Lösung zum Starten, Beenden oder Anhalten des entsprechenden Diensts nach Bedarf zur Senkung der Kosten beitragen (z. B. Azure Virtual Machines oder Azure SQL Data Warehouse).
>

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

- [Tutorial: Optimieren von Kosten mithilfe von Empfehlungen](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations)
- [Vermeiden unerwarteter Gebühren bei der Azure-Abrechnung und -Kostenverwaltung](https://docs.microsoft.com/azure/billing/billing-getting-started)
- [Ermitteln und Analysieren von Kosten mit der Kostenanalyse](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis)

::: zone-end
