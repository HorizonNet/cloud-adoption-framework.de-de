---
title: Schutz und Wiederherstellung in Azure
description: Es wird beschrieben, wie Sie für einen stabilen Geschäftsbetrieb sorgen, indem Sie die Wiederherstellungsdauer verkürzen und die Wahrscheinlichkeit für Unterbrechungen des Geschäftsbetriebs verringern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 67145b6c5da9c7da740771acfea38ba97e6f8a9c
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83217454"
---
<!-- cSpell:ignore siterecovery -->

# <a name="protect-and-recover-in-azure"></a>Schutz und Wiederherstellung in Azure

_Schutz und Wiederherstellung_ repräsentieren die dritte und letzte Disziplin in einer Baseline zur Cloudverwaltung.

![Baseline zur Cloudverwaltung](../../_images/manage/management-baseline.png)

In [Betriebsbezogene Compliance in Azure](./operational-compliance.md) bestand das Ziel darin, die Wahrscheinlichkeit einer Unterbrechung des Geschäftsbetriebs zu verringern. Der aktuelle Artikel zielt darauf ab, die Dauer und Auswirkung von Ausfällen zu verringern, die nicht vermeidbar sind.

In dieser Tabelle wird für jede Umgebung auf Unternehmensniveau der empfohlene Mindestwert für die einzelnen Verwaltungsbaselines aufgeführt:

| Prozess                 | Tool                  | Zweck                                                                                  |
| ----------------------- | --------------------- | ---------------------------------------------------------------------------------------- |
| Schützen von Daten            | Azure Backup          | Sichern Sie Daten und virtuelle Computer in der Cloud.                                          |
| Schutz der Umgebung | Azure Security Center | Erhöhen Sie die Sicherheit und bieten Sie erweiterten Schutz vor Bedrohungen für Ihre Hybrid-Workloads. |

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backup"></a>[Azure Backup](#tab/AzureBackup)

::: zone-end

Mit Azure Backup können Sie Ihre Daten in der Microsoft-Cloud sichern, schützen und wiederherstellen. Azure Backup ersetzt Ihre vorhandene lokale bzw. standortexterne Sicherungslösung durch eine cloudbasierte Lösung. Diese neue Lösung ist zuverlässig, sicher und kostengünstig. Azure Backup kann auch dazu beitragen, lokale Ressourcen durch eine einheitliche Lösung zu schützen und wiederherzustellen.

### <a name="enable-backup-for-an-azure-vm"></a>Aktivieren der Sicherung für eine Azure-VM

1. Wählen Sie im Azure-Portal die Option **Virtuelle Computer** und anschließend den virtuellen Computer aus, den Sie replizieren möchten.
1. Wählen Sie im Bereich **Vorgänge** die Option **Sicherung** aus.
1. Erstellen Sie einen Azure Recovery Services-Tresor, oder wählen Sie einen vorhandenen Tresor aus.
1. Wählen Sie **Neue Richtlinie erstellen (oder bearbeiten)** aus.
1. Konfigurieren Sie den Zeitplan und die Aufbewahrungsdauer.
1. Klicken Sie auf **OK**.
1. Wählen Sie **Sicherung aktivieren** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Übersicht](https://docs.microsoft.com/azure/backup/backup-overview)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery ist eine wesentliche Komponente in Ihrer Strategie für die Notfallwiederherstellung.

Site Recovery repliziert virtuelle Computer und Workloads, die in einer primären Azure-Region gehostet werden. Es repliziert sie in eine Kopie, die in einer sekundären Region gehostet wird. Wenn ein Ausfall in Ihrer primären Region auftritt, führen Sie ein Failover auf die in der sekundären Region aktiven Kopie aus. Von dort aus können Sie dann weiter auf Ihre Anwendungen und Dienste zugreifen. Dieser proaktive Ansatz für die Wiederherstellung kann die Wiederherstellungszeiten erheblich verringern. Wenn die Wiederherstellungsumgebung nicht mehr benötigt wird, kann für den Produktionsdatenverkehr ein Fallback auf die ursprüngliche Umgebung durchgeführt werden.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery"></a>Replizieren einer Azure-VM in einer anderen Region mit Site Recovery

Die folgenden Schritte beschreiben das Verfahren zur Verwendung von Site Recovery für die Azure-zu-Azure-Replikation, d. h. zum Replizieren einer Azure-VM in eine andere Region.
>
> [!TIP]
> Abhängig von Ihrem Szenario können sich die genauen Schritte leicht unterscheiden.
>

### <a name="enable-replication-for-the-azure-vm"></a>Aktivieren der Replikation für die Azure-VM

1. Wählen Sie im Azure-Portal die Option **Virtuelle Computer** und anschließend den virtuellen Computer aus, den Sie replizieren möchten.
1. Wählen Sie im Bereich **Vorgänge** die Option **Notfallwiederherstellung** aus.
1. Wählen Sie unter **Notfallwiederherstellung konfigurieren** > **Zielregion** die Zielregion für die Replikation aus.
1. Übernehmen Sie für diesen Schnellstart die Standardwerte für alle anderen Optionen.
1. Wählen Sie **Replikation aktivieren** aus, um einen Auftrag zum Aktivieren der Replikation für die VM zu starten.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Überprüfen der Einstellungen

Nach Abschluss des Replikationsauftrags können Sie den Replikationsstatus und die Replikationsintegrität überprüfen und die Bereitstellung testen.

1. Wählen Sie im VM-Menü die Option **Notfallwiederherstellung** aus.
1. Überprüfen Sie die Replikationsintegrität, die erstellten Wiederherstellungspunkte sowie die Quell- und Zielregionen auf der Karte.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

- [Azure Site Recovery – Übersicht](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replizieren eines virtuellen Azure-Computers in einer anderen Region](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
