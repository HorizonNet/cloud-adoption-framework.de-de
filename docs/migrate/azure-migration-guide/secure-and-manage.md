---
title: Sichern und Verwalten
description: Hier erfahren Sie mehr über Sicherheits- und Verwaltungsmethoden, mit denen Sie Ihre Umgebung nach der Migration zu Azure verwalten können.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: afde995e27d37114727fafa540f0f1232c49e8b3
ms.sourcegitcommit: 8b5fdb68127c24133429b4288f6bf9004a1d1253
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88848124"
---
<!-- markdownlint-disable MD024 MD025 DOCSMD001 -->

# <a name="secure-and-manage"></a>Sichern und Verwalten

Nach der Migration Ihrer Umgebung zu Azure ist es wichtig, sich Gedanken über die Sicherheit und die Methoden zur Verwaltung der Umgebung zu machen. Azure bietet viele Features und Funktionen, um diese Anforderungen in Ihrer Lösung zu erfüllen.

## <a name="azure-monitor"></a>[Azure Monitor](#tab/monitor)

Azure Monitor maximiert die Verfügbarkeit und Leistung Ihrer Anwendungen durch die Bereitstellung einer umfassenden Lösung für das Sammeln, Analysieren und Reagieren auf Telemetriedaten aus Ihren cloudbasierten und lokalen Umgebungen. Diese Lösung hilft Ihnen, die Leistung Ihrer Anwendungen zu verstehen, und erkennt proaktiv Probleme, die sich auf sie auswirken, und Ressourcen, von denen sie abhängen.

### <a name="use-and-configure-azure-monitor"></a>Verwenden und Konfigurieren von Azure Monitor

1. Wechseln Sie im Azure-Portal zu **Monitor**.
2. Wählen Sie **Metriken**, **Protokolle** oder **Service Health** aus, um Übersichten anzuzeigen.
3. Wählen Sie beliebige relevante Erkenntnisse aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Go to Azure Monitor" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure Monitor – Übersicht](/azure/azure-monitor/overview).

::: zone-end

## <a name="azure-service-health"></a>[Azure Service Health](#tab/serviceHealth)

Azure Service Health bietet personalisierte Anleitungen und Unterstützung, wenn Sie von Problemen bei den Azure-Diensten betroffen sind. Dieser Dienst kann Sie benachrichtigen, die Auswirkungen von Problemen verdeutlichen und Sie über die Lösung eines Problem auf dem Laufenden halten. Er kann Sie auch bei der Vorbereitung auf geplante Wartungsmaßnahmen und Änderungen unterstützen, die sich u.U. auf die Verfügbarkeit Ihrer Ressourcen auswirken.

Azure Service Health umfasst Folgendes:

- **Azure-Status:** eine globale Ansicht der Integrität von Azure-Diensten.
- **Dienstintegrität:** eine personalisierte Ansicht zur Integrität Ihrer Azure-Dienste.
- **Ressourcenintegrität:** eine tiefergehende Ansicht der Integrität der einzelnen Ressourcen, die Ihnen von Ihren Azure-Diensten bereitgestellt werden.

Kombiniert bieten diese Oberflächen einen umfassenden Überblick über die Azure-Integrität auf der für Sie relevanten Detailebene.

### <a name="access-service-health"></a>Zugreifen auf Service Health

1. Wechseln Sie im Azure-Portal zu **Monitor**.
2. Wählen Sie **Service Health**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter [Azure Service Health](/azure/service-health).

::: zone-end

## <a name="azure-advisor"></a>[Azure Advisor](#tab/advisor)

Bei Azure Advisor handelt es sich um einen personalisierten Cloudberater, der Sie mit bewährten Methoden zum Optimieren von Azure-Bereitstellungen unterstützt. Er analysiert Ihre Ressourcenkonfiguration und Nutzungstelemetrie. Anschließend schlägt er Lösungen vor, um die Leistung, Sicherheit und Hochverfügbarkeit Ihrer Ressourcen zu verbessern, und sucht gleichzeitig nach Möglichkeiten, Ihre Azure-Gesamtausgaben zu reduzieren.

### <a name="access-azure-advisor"></a>Zugreifen auf Azure Advisor

1. Wechseln Sie im Azure-Portal zu **Advisor**, oder suchen Sie nach der Ressource.
2. Wählen Sie **Hochverfügbarkeit**, **Sicherheit**, **Leistung**, **Kosten** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorMenuBlade/overview]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

[Übersicht](/azure/advisor/advisor-overview).

::: zone-end

## <a name="azure-security-center"></a>[Azure Security Center](#tab/security)

Azure Security Center ist ein vereinheitlichtes Sicherheitsverwaltungssystem für Infrastrukturen, mit dem der Sicherheitsstatus Ihrer Rechenzentren gestärkt und Azure Advanced Threat Protection für Ihre Hybridworkloads in der Cloud (&mdash;in Azure oder anderswo&mdash;) und in der lokalen Umgebung bereitgestellt wird.

### <a name="access-azure-security-center"></a>Zugriff auf Azure Security Center

1. Wechseln Sie im Azure-Portal zu **Security Center**, oder suchen Sie nach der Ressource.
2. Wählen Sie **Empfehlungen** aus.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/0]" submitText="Go to Security Center" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

[Übersicht](/azure/security-center/security-center-intro)

::: zone-end

## <a name="azure-backup"></a>[Azure Backup](#tab/backup)

Azure Backup ist der Azure-basierte Dienst, den Sie zum Sichern (bzw. Schützen) und Wiederherstellen Ihrer Daten in der Microsoft Cloud verwenden können. Azure Backup ersetzt Ihre vorhandene lokale bzw. standortexterne Lösung durch eine zuverlässige, sichere und wirtschaftliche Cloudlösung.

### <a name="enable-backup-for-an-azure-vm"></a>Aktivieren der Sicherung für eine Azure-VM

1. Wählen Sie im Azure-Portal die Option **Virtuelle Computer** und anschließend den virtuellen Computer aus, den Sie replizieren möchten.
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

[Übersicht](/azure/backup/backup-overview)

::: zone-end

## <a name="azure-site-recovery"></a>[Azure Site Recovery](#tab/siteRecovery)

Azure Site Recovery stellt jedoch auch nach Abschluss der Migration eine wichtige Komponente in Ihrer Notfallwiederherstellungsstrategie dar.

Der Azure Site Recovery-Dienst ermöglicht es Ihnen, virtuelle Computer und Workloads, die in einer primären Azure-Region gehostet werden, in einer Kopie in einer sekundären Region zu replizieren. Wenn es in Ihrer primären Region zu einem Ausfall kommt, können Sie ein Failover zur Kopie in der sekundären Region ausführen und von dort aus weiter auf Ihre Anwendungen und Dienste zugreifen. Sobald die primäre Kopie Ihres virtuellen Computers nach dem Ausfall wieder läuft, können Sie ein Failback ausführen.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replizieren einer Azure-VM in einer anderen Region mit dem Site Recovery-Dienst

Die folgenden Schritte beschreiben das Verfahren zur Verwendung des Site Recovery-Diensts zum Replizieren einer Azure-VM in einer anderen Region (Azure-to-Azure):

>
> [!TIP]
> Abhängig von Ihrem Szenario können sich die genauen Schritte leicht unterscheiden.
>

### <a name="enable-replication-for-the-azure-vm"></a>Aktivieren der Replikation für die Azure-VM

1. Wählen Sie im Azure-Portal die Option **Virtuelle Computer** und anschließend den virtuellen Computer aus, den Sie replizieren möchten.
1. Wählen Sie unter **Vorgänge** die Option **Notfallwiederherstellung** aus.
1. Wählen Sie unter **Notfallwiederherstellung konfigurieren** > **Zielregion** die Zielregion für die Replikation aus.
1. Akzeptieren Sie für diesen Schnellstart die anderen Standardeinstellungen.
1. Wählen Sie **Replikation aktivieren** aus. Dadurch wird ein Auftrag gestartet, um die Replikation der VM zu aktivieren.

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

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

- [Azure Site Recovery – Übersicht](/azure/site-recovery/site-recovery-overview)
- [Replizieren eines virtuellen Azure-Computers in einer anderen Region](/azure/site-recovery/azure-to-azure-quickstart)

::: zone-end
