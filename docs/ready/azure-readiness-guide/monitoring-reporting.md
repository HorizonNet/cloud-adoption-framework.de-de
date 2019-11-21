---
title: Überwachung und Berichterstellung in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Es wird beschrieben, wie Sie die Überwachung, die Berichterstellung und Warnungen für Ihre Azure-Verwaltungsumgebung einrichten.
author: timleyden
ms.author: tileyden
ms.date: 04/09/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: f2ce0c108152f4dcd6d94a095a96a2a0a1b6a361
ms.sourcegitcommit: 3655aa7f3e80249e0b2b562cd40dd750afc82043
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2019
ms.locfileid: "74251760"
---
# <a name="monitoring-and-reporting-in-azure"></a>Überwachung und Berichterstellung in Azure

Azure bietet verschiedene Dienste, die zusammen eine umfassende Lösung zum Erfassen, Analysieren und Nutzen von Telemetriedaten aus Ihren Anwendungen und den unterstützenden Azure-Ressourcen bilden. Diese Dienste lassen sich zudem erweitern, um kritische lokale Ressourcen zu überwachen und eine hybride Überwachungsumgebung zu erhalten.

# <a name="azure-monitortabazuremonitor"></a>[Azure Monitor](#tab/AzureMonitor)

Azure Monitor ist ein separater einheitlicher Hub für alle Überwachungs- und Diagnosedaten in Azure. Sie können Azure Monitor verwenden, um Einblicke in ihre Ressourcen zu erhalten. Mit Azure Monitor können Sie Probleme ermitteln und beheben und die Leistung optimieren. Sie können auch das Kundenverhalten besser verstehen.

- **Überwachen und Visualisieren von Metriken.** Metriken sind numerische Werte von Azure-Ressourcen, die es Ihnen ermöglichen, die Integrität Ihrer Systeme zu verstehen. Passen Sie die Diagramme für Ihre Dashboards an, und nutzen Sie Arbeitsmappen für die Berichterstellung.

- **Abfragen und Analysieren von Protokollen.** Zu den Protokollen gehören die Aktivitätsprotokolle und Diagnoseprotokolle aus Azure. Erfassen Sie zusätzliche Protokolle anderer Überwachungs- und Verwaltungslösungen für Ihre Cloudressourcen oder lokalen Ressourcen. Log Analytics bietet ein zentrales Repository für die Aggregierung dieser Daten. Von dort aus können Sie Abfragen ausführen, um Probleme zu beheben oder Daten zu visualisieren.

- **Einrichten von Warnungen und Aktionen.** Mit Warnungen werden Sie proaktiv über kritische Zustände benachrichtigt. Korrekturmaßnahmen können basierend auf Triggern von Metriken, Protokollen oder Problemen mit der Dienstintegrität ergriffen werden. Sie können unterschiedliche Benachrichtigungen und Aktionen einrichten und Daten an Ihre Tools für das IT-Service-Management senden.

::: zone target="docs"

 Beginnen Sie mit der Überwachung von:

- [Anwendungen](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Container](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Virtuelle Computer](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Netzwerke](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Auf dem Azure Marketplace finden Sie noch weitere Lösungen zur Überwachung anderer Ressourcen.

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview), um Azure Monitor zu erkunden.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Aktion

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

::: zone-end

# <a name="azure-service-healthtabazureservicehealth"></a>[Azure Service Health](#tab/AzureServiceHealth)

Azure Service Health bietet eine personalisierte Darstellung der Integrität der von Ihnen verwendeten Azure-Dienste und -Regionen. In Service Health werden Informationen zu aktiven Problemen veröffentlicht, um Sie über die Auswirkungen auf Ihre Ressourcen zu informieren. Während der Problembehandlung werden Sie mit regelmäßigen Aktualisierungen stets auf dem Laufenden gehalten.

In Service Health werden auch geplante Wartungsmaßnahmen veröffentlicht, um Sie über Änderungen zu informieren, die ggf. Auswirkungen auf die Verfügbarkeit Ihrer Ressourcen haben. Richten Sie Service Health-Warnungen ein, um eine Benachrichtigung zu erhalten, wenn die von Ihnen verwendeten Azure-Dienste und -Regionen ggf. von Dienstproblemen, geplanten Wartungsmaßnahmen oder anderen Änderungen betroffen sind.

Azure Service Health umfasst Folgendes:

- **Azure-Status:** eine globale Ansicht der Integrität von Azure-Diensten.
- **Dienstintegrität:** eine personalisierte Ansicht zur Integrität Ihrer Azure-Dienste.
- **Ressourcenintegrität:** eine detailliertere Ansicht zur Integrität Ihrer einzelnen Ressourcen.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

## <a name="action"></a>Aktion

Gehen Sie wie folgt vor, um eine Service Health-Warnung einzurichten:

1. Wechseln Sie zu **Service Health**.
2. Wählen Sie **Integritätswarnungen**.
3. Erstellen Sie eine Service Health-Warnung.

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts), um eine Service Health-Warnung einzurichten.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Azure Service Health-Dokumentation](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisortabazureadvisor"></a>[Azure Advisor](#tab/AzureAdvisor)

Azure Advisor ist ein kostenloser, personalisierter Cloudberater, der Sie bei der Einhaltung und Umsetzung bewährter Methoden für Azure-Bereitstellungen unterstützt. Azure Advisor analysiert Ihre Ressourcenkonfiguration sowie Ihre Nutzungstelemetriedaten und empfiehlt Lösungen für die Umgebungsoptimierung. Die Empfehlungen sind in vier Kategorien unterteilt:

- **Hochverfügbarkeit:** Der Ratgeber hilft, die ununterbrochene Verfügbarkeit Ihrer unternehmenskritischen Anwendungen zu verbessern. Die Empfehlungen können ggf. auch das Hinzufügen von virtuellen Computern zu einer Verfügbarkeitsgruppe oder das Hinzufügen von georedundanten Endpunkten umfassen.
- **Sicherheit**: Der Ratgeber hilft beim Erkennen von Bedrohungen und Sicherheitsrisiken, die zu Sicherheitslücken führen können. Die Empfehlungen können ggf. das Anwenden einer Datenträgerverschlüsselung oder das Aktivieren von Netzwerksicherheitsgruppen umfassen.
- **Leistung:** Der Ratgeber hilft, die Geschwindigkeit Ihrer Anwendungen zu verbessern. Die Empfehlungen können ggf. die Erhöhung der SQL-Abfrageleistung durch die Erstellung von Indizes oder eine Neukonfiguration Ihrer Traffic Manager-Einstellungen umfassen.
- **Kosten:** Mit dem Ratgeber können Sie Ihre Gesamtausgaben für Azure senken und optimieren. Die Empfehlungen können beispielsweise das Ändern der Größe oder das Herunterfahren von virtuellen Computern mit zu geringer Auslastung oder den Umstieg auf Azure-Reservierungen beinhalten, um die Gesamtkosten zu senken.

Empfehlungen in Advisor basieren auf den von Ihnen bereitgestellten Ressourcen und den Aktionen, die Sie in Azure durchführen. Sie können Advisor regelmäßig auf die neuesten Empfehlungen überprüfen.

::: zone target="chromeless"

## <a name="action"></a>Aktion

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Explore Azure Advisor" :::

::: zone-end

::: zone target="docs"

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Expert/AdvisorBlade), um Azure Advisor zu erkunden.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Azure Advisor-Dokumentation](https://docs.microsoft.com/azure/advisor).

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center spielt auch bei Ihrer Überwachungsstrategie eine wichtige Rolle. Hiermit können Sie die Sicherheit Ihrer Computer und Netzwerke, Ihres Speichers, Ihrer Datendienste und Ihrer Anwendungen überwachen. Security Center ermöglicht eine erweiterte Bedrohungserkennung basierend auf maschinellem Lernen und Verhaltensanalysen, um für Ihre Azure-Ressourcen aktive Bedrohungen zu identifizieren. Darüber hinaus ist ein Schutz vor Bedrohungen vorhanden, bei dem Schadsoftware oder anderer unerwünschter Code blockiert wird und die Fläche für Brute-Force- und andere Netzwerkangriffe verkleinert wird.

Wenn Security Center eine Bedrohung erkennt, wird eine Sicherheitswarnung mit Schritten ausgelöst, die Sie ausführen müssen, um auf einen Angriff zu reagieren. Darüber hinaus wird ein Bericht mit Informationen zur erkannten Bedrohung bereitgestellt.

Azure Security Center wird in zwei Tarifen angeboten: Free und Standard. Features wie die Sicherheitsempfehlungen stehen kostenlos zur Verfügung. Der Standard-Tarif bietet zusätzlichen Schutz, etwa eine erweiterte Bedrohungserkennung sowie Schutz vor Bedrohungen für Hybrid Cloud-Workloads.

::: zone target="chromeless"

## <a name="action"></a>Aktion

**Testen Sie den Standard-Tarif in den ersten 30 Tagen kostenlos.**

Nachdem Sie Sicherheitsrichtlinien für die Ressourcen eines Abonnements aktiviert und eingerichtet haben, können Sie den Sicherheitsstatus Ihrer Ressourcen sowie eventuelle Probleme im Abschnitt **Prävention** anzeigen. Eine Liste mit diesen Problemen steht auch auf der Kachel **Empfehlungen** zur Verfügung.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0), um Azure Security Center zu erkunden.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie in der [Azure Security Center-Dokumentation](https://docs.microsoft.com/azure/security-center).

::: zone-end
