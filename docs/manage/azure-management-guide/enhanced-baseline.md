---
title: Optimierte Verwaltungsbaseline in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Allgemeine Verbesserungen an der Verwaltungsbaseline
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 85e289867ac69f3403d964078a7c3f3b2a6c96a7
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683696"
---
# <a name="enhanced-management-baseline-in-azure"></a>Optimierte Verwaltungsbaseline in Azure

In den ersten drei Disziplinen der Cloudverwaltung wird eine Verwaltungsbaseline beschrieben. In den vorangehenden Artikeln dieses Leitfadens wurde ein MVP (Minimum Viable Product) für Cloudverwaltungsdienste erläutert, das als Verwaltungsbaseline bezeichnet wird. Dieser Artikel beschreibt einige allgemeine Verbesserungen der Baseline.

Der Zweck einer Verwaltungsbaseline besteht darin, ein stimmiges Angebot zu schaffen, das für **alle** unterstützten Workloads ein Mindestmaß an geschäftlicher Verpflichtung vorsieht. Diese Baseline für allgemeine, wiederholbare Verwaltungsangebote ermöglicht es dem Team, eine äußerst optimierte Betriebsführung mit nur minimalen Abweichungen zu gewährleisten. Möglicherweise ist jedoch eine größere Verpflichtung für das Unternehmen erforderlich, die über das Standardangebot hinausgeht. Die folgende Abbildung und die Aufzählungszeichen skizzieren drei Möglichkeiten, um über die Verwaltungsbaseline hinauszugehen.

![Über die Cloudverwaltungsbaseline hinaus](../../_images/manage/beyond-the-baseline.png)

- **Workloadbetrieb:**
  - Größte Investition pro Workloadvorgang.
  - Höchster Resilienzgrad.
  - Empfohlen für etwa 20 % der Workloads, die den Geschäftswert erzeugen.
  - In der Regel für Workloads von hoher Wichtigkeit oder unternehmenskritische Workloads reserviert.
- **Plattformbetrieb:**
  - Die Betriebsinvestition ist auf viele Workloads verteilt.
  - Verbesserungen der Resilienz betreffen alle Workloads, die die definierte Plattform nutzen.
  - Empfohlen für etwa 20 % der Plattformen von höchster Wichtigkeit.
  - In der Regel für Workloads von mittlerer bis hoher Wichtigkeit reserviert.
- **Optimierte Verwaltungsbaseline:**
  - Niedrigste relative Betriebsinvestition.
  - Leicht verbesserte Erfüllung der Geschäftsverpflichtungen mit zusätzlichen cloudnativen Betriebstools und Prozessen.

Workload- und Plattformbetrieb erfordern Änderungen von Entwurfs- und Architekturprinzipien. Diese Änderungen können Zeit in Anspruch nehmen und zu erhöhten Betriebskosten führen. Um die Anzahl der Workloads zu reduzieren, die solche Investitionen erfordern, kann eine optimierte Verwaltungsbaseline eine ausreichende Verbesserung zur Erfüllung geschäftlicher Verpflichtungen bewirken.

In der folgenden Tabelle werden einige gängige Prozesse, Tools und potenzielle Auswirkungen beschrieben, die in den optimierten Verwaltungsbaselines der Kunden üblich sind.

|Disziplin  |Prozess  |Tool  |Potenzielle Auswirkung| Weitere Informationen |
|---------|---------|---------|---------|---------|
|Bestand und Transparenz|Änderungsnachverfolgung für Dienste|Azure Resource Graph|Ein umfassenderer Einblick in Änderungen an Azure-Diensten kann helfen, negative Auswirkungen früher zu erkennen oder schneller zu beheben.|[Übersicht über Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview)|
|Bestand und Transparenz|ITSM-Integration (IT-Service-Management)|IT Service Management Connector|Eine automatisierte ITSM-Verbindung führt zu früheren Erkenntnissen.|[Azure-ITSM-Connector](https://docs.microsoft.com/azure/azure-monitor/platform/itsmc-overview)|
|Betriebsbezogene Compliance|Betriebsautomatisierung|Azure-Automatisierung|Durch automatisierte betriebsbezogene Compliance können Sie auf Änderungen schneller und präziser reagieren.|Siehe unten|
|Betriebsbezogene Compliance|Multicloudvorgänge|Azure Automation – Hybrid Runbook Worker|Automatisieren Sie Vorgänge in mehreren Clouds.|[Übersicht über Hybrid Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)|
|Betriebsbezogene Compliance|Gastautomatisierung|Desired State Configuration (DSC)|Durch die codebasierte Konfiguration von Gastbetriebssystemen können Fehler und Konfigurationsabweichungen behoben werden.|[Übersicht über DSC](/powershell/scripting/dsc/overview/overview)|
|Schutz und Wiederherstellung|Benachrichtigung bei Sicherheitsverletzungen|Azure Security Center|Durch Erweitern des Schutzes können Wiederherstellungstrigger bei Sicherheitsverletzungen einbezogen werden.|Siehe unten|

::: zone target="docs"

## <a name="azure-automation"></a>Azure-Automatisierung

::: zone-end
::: zone target="chromeless"

## <a name="azure-automationtabazureautomation"></a>[Azure Automation](#tab/AzureAutomation)

::: zone-end

Azure Automation stellt ein zentralisiertes System zur Verwaltung automatisierter Steuerelemente bereit. In Azure Automation können einfache Wiederherstellungs-, Skalierungs- und Optimierungsprozesse als Reaktion auf Umgebungsmetriken ausgeführt werden, um den Aufwand zu reduzieren, der mit der manuellen Verarbeitung von Incidents verknüpft ist. Am wichtigsten ist, dass die automatisierte Wiederherstellung nahezu in Echtzeit erfolgen kann, wodurch Unterbrechungen von Geschäftsprozessen erheblich verringert werden. Durch eine Studie der gängigsten Geschäftsunterbrechungen lassen sich Aktivitäten in Ihrer Umgebung identifizieren, die automatisiert werden können.

### <a name="runbooks"></a>Runbooks

Die grundlegende Codeeinheit zur Bereitstellung der automatisierten Wiederherstellung ist ein Runbook. Runbooks enthalten die Anweisungen zum Beheben eines Vorfalls oder zur anschließenden Wiederherstellung.

So erstellen oder verwalten Sie Runbooks:

1. Wechseln Sie zu [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Wählen Sie eines der aufgelisteten **Automation-Konten** aus.
3. Suchen Sie in der Portalnavigation den Abschnitt **Prozessautomatisierung**.
4. Mit den Optionen in diesem Abschnitt können Sie Runbooks, Zeitpläne und andere Funktionen zur automatisierten Wiederherstellung erstellen oder verwalten.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
::: zone target="docs"

## <a name="azure-security-center"></a>Azure Security Center

::: zone-end
::: zone target="chromeless"

## <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

::: zone-end

Azure Security Center spielt auch bei Ihrer Schutz- und Wiederherstellungsstrategie eine wichtige Rolle. Hiermit können Sie die Sicherheit Ihrer Computer und Netzwerke, Ihres Speichers, Ihrer Datendienste und Ihrer Anwendungen überwachen. Azure Security Center ermöglicht eine erweiterte Bedrohungserkennung basierend auf maschinellem Lernen und Verhaltensanalysen, um für Ihre Azure-Ressourcen aktive Bedrohungen zu identifizieren. Darüber hinaus ist ein Schutz vor Bedrohungen vorhanden, bei dem Schadsoftware oder anderer unerwünschter Code blockiert wird und die Fläche für Brute-Force- und andere Netzwerkangriffe verkleinert wird.

Wenn Azure Security Center eine Bedrohung erkennt, wird eine Sicherheitswarnung mit Schritten ausgelöst, die Sie ausführen müssen, um auf einen Angriff zu reagieren. Darüber hinaus wird ein Bericht mit Informationen zur erkannten Bedrohung bereitgestellt.

Azure Security Center wird in zwei Tarifen angeboten: Free und Standard. Features wie die Sicherheitsempfehlungen stehen im Free-Tarif zur Verfügung. Der Standard-Tarif bietet zusätzlichen Schutz, etwa eine erweiterte Bedrohungserkennung sowie Schutz vor Bedrohungen für Hybrid Cloud-Workloads.

::: zone target="chromeless"

### <a name="action"></a>Aktion

**Testen Sie den Standard-Tarif in den ersten 30 Tagen kostenlos.**

Nachdem Sie die Sicherheitsrichtlinien für die Ressourcen eines Abonnements aktiviert und konfiguriert haben, können Sie den Sicherheitsstatus Ihrer Ressourcen und alle Probleme im Abschnitt **Prävention** anzeigen. Eine Liste mit diesen Problemen steht auch auf der Kachel **Empfehlungen** zur Verfügung.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0), um Azure Security Center zu erkunden.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Azure Security Center-Dokumentation](https://docs.microsoft.com/azure/security-center).

::: zone-end
