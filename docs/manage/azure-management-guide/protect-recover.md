---
title: Schutz und Wiederherstellung in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Sicherstellen eines stabilen Geschäftsbetriebs durch Verkürzung der Wiederherstellungszeit
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: a79164435772f571849d0a836f43b53ce3bca087
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557005"
---
# <a name="protect-and-recover-in-azure"></a>Schutz und Wiederherstellung in Azure

Schutz und Wiederherstellung repräsentieren die dritte und letzte Disziplin in einer Baseline zur Cloudverwaltung.

![Baseline zur Cloudverwaltung](../../_images/manage/management-baseline.png)

Im vorangegangenen Artikel „Betriebsbezogene Compliance“ bestand das Ziel darin, die Wahrscheinlichkeit einer Unterbrechung des Geschäftsbetriebs zu verringern. Der vorliegende Artikel „Schutz und Wiederherstellung“ zielt darauf ab, die Dauer und Auswirkung von Ausfällen zu verringern, die nicht vermeidbar sind.

In der folgenden Tabelle wird für jede Umgebung auf Unternehmensniveau der empfohlene Mindestwert für die einzelnen Verwaltungsbaselines aufgeführt.

|Prozess  |Tool  |Zweck  |
|---------|---------|---------|
|Schützen von Daten|Azure Backup|Sicherung von Daten und VMs in der Cloud|
|Schutz der Umgebung|Azure Security Center|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Azure Backup ist der Azure-basierte Dienst, den Sie zum Sichern (bzw. Schützen) und Wiederherstellen Ihrer Daten in der Microsoft-Cloud verwenden können. Azure Backup ersetzt Ihre vorhandene lokale bzw. standortexterne Lösung durch eine zuverlässige, sichere und wirtschaftliche Cloudlösung. Mithilfe von Azure Backup ist es außerdem möglich, lokale Ressourcen mithilfe einer konsistenten Lösung zu schützen und wiederherzustellen.

### <a name="enable-backup-for-an-azure-vm"></a>Aktivieren der Sicherung für eine Azure-VM

1. Wählen Sie im Azure-Portal **Virtuelle Computer** und dann die VM aus, die Sie replizieren möchten.
1. Wählen Sie unter **Vorgänge** die Option **Sicherung** aus.
1. Erstellen Sie einen Recovery Services-Tresor, oder wählen Sie einen vorhandenen Tresor aus.
1. Wählen Sie **Neue Richtlinie erstellen (oder bearbeiten)** aus.
1. Konfigurieren Sie den Zeitplan und die Aufbewahrungsdauer.
1. Klicken Sie auf **OK**.
1. Wählen Sie **Sicherung aktivieren** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Übersicht](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery ist eine wesentliche Komponente in Ihrer Strategie für die Notfallwiederherstellung.

Der Azure Site Recovery-Dienst ermöglicht es Ihnen, virtuelle Computer und Workloads, die in einer primären Azure-Region gehostet werden, in einer Kopie in einer sekundären Region zu replizieren. Wenn es in Ihrer primären Region zu einem Ausfall kommt, können Sie ein Failover zur Kopie in der sekundären Region ausführen und von dort aus weiter auf Ihre Anwendungen und Dienste zugreifen. Dieser proaktive Ansatz für die Wiederherstellung kann die Wiederherstellungszeiten erheblich verringern. Wenn die Wiederherstellungsumgebung nicht mehr benötigt wird, kann für den Produktionsdatenverkehr ein Fallback auf die ursprüngliche Umgebung durchgeführt werden.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replizieren einer Azure-VM in einer anderen Region mit dem Site Recovery-Dienst

Die folgenden Schritte beschreiben das Verfahren zur Verwendung des Site Recovery-Diensts zum Replizieren einer Azure-VM in einer anderen Region (Azure-to-Azure):

>
> [!TIP]
> Abhängig von Ihrem Szenario können sich die genauen Schritte leicht unterscheiden.
>

### <a name="enable-replication-for-the-azure-vm"></a>Aktivieren der Replikation für die Azure-VM

1. Wählen Sie im Azure-Portal **Virtuelle Computer** und dann die VM aus, die Sie replizieren möchten.
1. Wählen Sie unter **Vorgänge** die Option **Notfallwiederherstellung** aus.
1. Wählen Sie unter **Notfallwiederherstellung konfigurieren** > **Zielregion** die Zielregion für die Replikation aus.
1. Akzeptieren Sie für diesen Schnellstart die anderen Standardeinstellungen.
1. Wählen Sie **Replikation aktivieren** aus, um einen Auftrag zum Aktivieren der Replikation für die VM zu starten.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Überprüfen der Einstellungen

Nach Abschluss des Replikationsauftrags können Sie den Replikationsstatus und die Replikationsintegrität überprüfen und die Bereitstellung testen.

1. Wählen Sie im VM-Menü die Option **Notfallwiederherstellung** aus.
2. Überprüfen Sie die Replikationsintegrität, die erstellten Wiederherstellungspunkte sowie die Quell- und Zielregionen auf der Karte.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

- [Azure Site Recovery – Übersicht](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replizieren eines virtuellen Azure-Computers in einer anderen Region](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
