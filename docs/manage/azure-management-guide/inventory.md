---
title: Bestand und Transparenz in Azure
description: Enthält eine Beschreibung der Tools, die sowohl die Bereitstellung eines Bestands als auch Transparenz in Bezug auf den Ausführungszustand des Bestands ermöglichen, um Betriebsdaten sammeln zu können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: e6cae79ab54c4b1389f9f74ab291575e16831b38
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756429"
---
# <a name="inventory-and-visibility-in-azure"></a>Bestand und Transparenz in Azure

_Bestand und Transparenz_ ist die erste von drei Disziplinen in einer Baseline zur Cloudverwaltung.

![Baseline zur Cloudverwaltung](../../_images/manage/management-baseline.png)

Diese Disziplin steht an erster Stelle, da das Sammeln von korrekten Betriebsdaten entscheidend ist, wenn Sie Entscheidungen über den Betrieb treffen. Cloudverwaltungsteams müssen wissen, was verwaltet wird und wie gut diese Ressourcen eingesetzt werden. Dieser Artikel beschreibt die verschiedenen Tools, die sowohl den Bestand erfassen als auch Einblicke in den Ausführungszustand des Bestands geben.

In der folgenden Tabelle wird für jede Umgebung auf Unternehmensniveau der empfohlene Mindestwert für eine Verwaltungsbaseline aufgeführt.

| Prozess | Tool | Zweck |
|---|---|---|
| Überwachen der Integrität von Azure-Diensten | Azure Service Health | Integrität, Leistung und Diagnose für Dienste, die in Azure ausgeführt werden |
| Zentralisierung von Protokollen | Log Analytics | Zentrale Protokollierung für jegliche Transparenzzwecke |
| Zentralisierung der Überwachung | Azure Monitor | Zentrale Überwachung von Betriebsdaten und Trends |
| Nachverfolgen von Bestand und Änderungen für virtuelle Computer | Azure-Änderungsnachverfolgung und Bestand | Bestandsaufnahme von VMs und Überwachen von Änderungen auf Ebene des Gastbetriebssystems |
| Abonnementüberwachung | Azure-Aktivitätsprotokoll | Überwachen von Änderungen auf Abonnementebene |
| Überwachung des Gastbetriebssystems | Azure Monitor für VMs | Überwachen von Änderungen und der Leistung von VMs |
| Netzwerküberwachung | Azure Network Watcher | Überwachen von Netzwerkänderungen und -leistung |
| DNS-Überwachung | DNS-Analyse | Sicherheit, Leistung und Vorgänge von DNS |

::: zone target="docs"

## <a name="azure-service-health"></a>Azure Service Health

::: zone-end
::: zone target="chromeless"

## <a name="azure-service-health"></a>[Azure Service Health](#tab/AzureServiceHealth)

::: zone-end

Azure Service Health bietet eine personalisierte Darstellung der Integrität Ihrer Azure-Dienste und -Regionen. In Azure Service Health werden Informationen zu aktiven Problemen veröffentlicht, um Sie über die Auswirkungen auf Ihre Ressourcen zu informieren. Während der Problembehandlung werden Sie mit regelmäßigen Aktualisierungen stets auf dem Laufenden gehalten.

In Azure Service Health werden auch geplante Wartungsmaßnahmen veröffentlicht, um Sie über Änderungen zu informieren, die Auswirkungen auf die Verfügbarkeit von Ressourcen haben können. Richten Sie Service Health-Warnungen ein, um eine Benachrichtigung zu erhalten, wenn Ihre Azure-Dienste und -Regionen ggf. von Dienstproblemen, geplanten Wartungsmaßnahmen oder anderen Änderungen betroffen sind.

Azure Service Health umfasst Folgendes:

- **Azure-Status:** eine globale Ansicht der Integrität von Azure-Diensten.
- **Dienstintegrität:** eine personalisierte Ansicht zur Integrität Ihrer Azure-Dienste.
- **Ressourcenintegrität:** eine detailliertere Ansicht zur Integrität Ihrer einzelnen Ressourcen.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Gehen Sie wie folgt vor, um eine Service Health-Warnung einzurichten:

1. Wechseln Sie zu **Service Health**.
2. Wählen Sie **Integritätswarnungen**.
3. Erstellen Sie eine Service Health-Warnung.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts), um Service Health-Warnungen einzurichten.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter [Azure Service Health](https://docs.microsoft.com/azure/service-health).

## <a name="log-analytics"></a>Log Analytics

::: zone-end
::: zone target="chromeless"

## <a name="log-analytics"></a>[Log Analytics](#tab/Log-Analytics)

::: zone-end

Ein [Log Analytics-Arbeitsbereich](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) ist eine spezifische Umgebung für das Speichern von Azure Monitor-Protokolldaten. Jeder Arbeitsbereich verfügt über ein eigenes Datenrepository und eine eigene Konfiguration. Datenquellen und Lösungen sind so konfiguriert, dass sie ihre Daten in bestimmten Arbeitsbereichen speichern. Azure-Überwachungslösungen erfordern, dass alle Server mit einem Arbeitsbereich verbunden sind, damit ihre Protokolldaten gespeichert und abgerufen werden können.

::: zone target="chromeless"

### <a name="action"></a>Aktion

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2FWorkspaces]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Dokumentation zum Erstellen eines Log Analytics-Arbeitsbereichs](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace).

## <a name="azure-monitor"></a>Azure Monitor

::: zone-end
::: zone target="chromeless"

## <a name="azure-monitor"></a>[Azure Monitor](#tab/Azure-Monitor)

::: zone-end

Azure Monitor ist ein separater einheitlicher Hub für alle Überwachungs- und Diagnosedaten in Azure und bietet Ihnen eine ressourcenübergreifende Transparenz. Mit Azure Monitor können Sie Probleme ermitteln und beheben und die Leistung optimieren. Sie können auch das Kundenverhalten besser verstehen.

- **Überwachen und Visualisieren von Metriken.** Metriken sind numerische Werte, die über Azure-Ressourcen verfügbar sind. Sie helfen Ihnen, die Integrität Ihrer Systeme zu verstehen. Passen Sie die Diagramme für Ihre Dashboards an, und nutzen Sie Arbeitsmappen für die Berichterstellung.

- **Abfragen und Analysieren von Protokollen.** Zu den Protokollen gehören die Aktivitätsprotokolle und Diagnoseprotokolle aus Azure. Erfassen Sie zusätzliche Protokolle anderer Überwachungs- und Verwaltungslösungen für Ihre Cloudressourcen oder lokalen Ressourcen. Log Analytics bietet ein zentrales Repository für die Aggregierung dieser Daten. Von dort aus können Sie Abfragen ausführen, um Probleme zu beheben oder Daten zu visualisieren.

- **Einrichten von Warnungen und Aktionen.** Mit Warnungen werden Sie über kritische Zustände benachrichtigt. Korrekturmaßnahmen können basierend auf Triggern von Metriken, Protokollen oder Problemen mit der Dienstintegrität ergriffen werden. Sie können unterschiedliche Benachrichtigungen und Aktionen einrichten und auch Daten an Ihre Tools für das IT-Service-Management senden.

::: zone target="chromeless"

### <a name="action"></a>Aktion

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

 Beginnen Sie mit der Überwachung von:

- [Anwendungen](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Container](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Virtuelle Computer](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Netzwerke](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Auf dem Azure Marketplace finden Sie noch weitere Lösungen zur Überwachung anderer Ressourcen.

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview), um Azure Monitor zu erkunden.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

## <a name="onboard-solutions"></a>Onboarding von Lösungen

::: zone-end
::: zone target="chromeless"

## <a name="onboard-solutions"></a>[Onboarding von Lösungen](#tab/Configure-solutions)

::: zone-end

Zur Aktivierung von Lösungen müssen Sie den Log Analytics-Arbeitsbereich konfigurieren. Für Azure-VMs und lokale Server, für die das Onboarding durchgeführt wurde, werden die Lösungen aus den Log Analytics-Arbeitsbereichen abgerufen, mit denen sie verbunden sind.

Es gibt zwei Ansätze für das Onboarding:

- [Einzelne VM](../../manage/azure-server-management/onboard-single-vm.md)
- [Ganzes Abonnement](../../manage/azure-server-management/onboard-at-scale.md)

Jeder Artikel erläutert die Schritte zum Onboarding der folgenden Lösungen:

- Updateverwaltung
- Änderungsnachverfolgung und Bestand
- Azure-Aktivitätsprotokoll
- Azure Log Analytics-Agent-Integritätsdiagnose
- Antischadsoftwarebewertung
- Azure Monitor für VMs
- Azure Security Center

Jede der vorherigen Schritte unterstützt Sie beim Erfassen des Bestands und Schaffen von Transparenz.
