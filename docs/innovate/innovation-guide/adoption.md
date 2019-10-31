---
title: 'Azure-Innovationsleitfaden: Vorbereiten für Kundenfeedback'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vorbereiten für Kundenfeedback
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: ec17c66fa92abc292a19a8e74c215111d8638a05
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769368"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Azure-Innovationsleitfaden: Vorbereiten für Kundenfeedback

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Vorbereiten für Kundenfeedback

::: zone-end

Einführung, Interaktion und Bindung von Benutzern sind der Schlüssel für erfolgreiche Innovation. Warum?

Beim Erstellen einer innovativen neuen Lösung geht es nicht darum, dem Benutzer das zu geben, was er will oder glaubt zu wollen. Es geht um die Formulierung einer Hypothese, die getestet und als Basis für Verbesserungen verwendet werden kann. Diese Tests gibt es in zwei Formen: Quantitativ (Testfeedback), d.h. die Aktionen, die wir uns erhoffen. Qualitativ (Kundenfeedback), d.h. wir erfahren, was diese Metriken aus Sicht des Kunden bedeuten. Gemeinsam ergeben sie die nächste Hypothese und die nächste Verbesserung der Lösung. Diese Feedbackschleifen bilden die Grundlage für den [Erstellen-Messen-Lernen-Prozess](../considerations/adoption.md), dem zentralen Punkt dieser Methodik.

Ein gemeinsam genutztes Repository für Ihre Lösung ist eine unerlässliche Voraussetzung, bevor Feedbackschleifen eingebunden werden. Ein zentralisiertes Repository bietet die Möglichkeit, das gesamte Feedback zu Ihrem Projekt aufzuzeichnen und darauf zu reagieren.  [GitHub](https://github.com/) ist der zentrale Aufbewahrungsort für Open Source-Software. Es ist auch eine der am häufigsten verwendeten Plattformen für das Hosting des Quellcoderepositorys für kommerziell entwickelte Anwendungen. Der Artikel zum [Erstellen von GitHub-Repositorys](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) kann Ihnen bei den ersten Schritten mit Ihrem Repository helfen.

Jedes der folgenden Tools in Azure kann in GitHub gehostete Projekte integriert werden (oder ist mit ihnen kompatibel):

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Quantitatives Feedback für Web-Apps](#tab/Quantitative-Apps)

Application Insights ist ein Überwachungstool, das quantitatives Feedback zur Nutzung Ihrer Anwendung nahezu in Echtzeit ermöglicht. Anhand dieses Feedbacks können Sie Ihre aktuelle Hypothese testen und überprüfen, um das nächste Feature oder die nächste User Story in Ihrem Backlog zu gestalten.

### <a name="action"></a>Aktion

Zum Anzeigen quantitativer Daten für Ihre Anwendungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **App-Erkenntnisse**.
2. Wenn Ihre Anwendung nicht in der Liste angezeigt wird, klicken Sie auf den Link **Hinzufügen +** , und folgen Sie den Anweisungen, um mit der Konfiguration von App-Erkenntnissen zu beginnen.
3. Wenn die gewünschte App in der Liste enthalten ist, wählen Sie die Anwendung aus.
4. Der Bereich **Übersicht** enthält einige Statistiken für die Anwendung. Über den Link **Anwendungsdashboard** können Sie ein benutzerdefiniertes Dashboard erstellen, um Daten anzuzeigen, die für ihre Hypothese von größerer Relevanz sind.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to App Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Um die Daten zu Ihren Apps anzuzeigen, wechseln Sie zum [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

- [Einrichten von Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Erste Schritte mit Azure Monitor App Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Erstellen eines Telemetriedashboards](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Quantitatives Feedback für APIs](#tab/Quantitative-APIs)

Die vernetzte Wirtschaft verändert die Art und Weise, in der Unternehmen Innovationen entwickeln.  Märkte und Branchen werden schneller als je zuvor gestört. Störungen treten in vielen Formen auf, und Unternehmen müssen sich mit dem **Dilemma des Innovators** auseinandersetzen: Wie kann man das Tempo der Änderung festlegen, ohne die laufende Geschäftsaktivität zu beeinträchtigen.

Unternehmen verwenden extern APIs, um die Interaktion mit Kunden und ihren Partnern zu ändern. Intern verwenden Sie APIs, um verschiedene Teile des Unternehmens nahtlos miteinander zu verbinden. Die API-Struktur basiert auf vier Bausteinen: soziale Netzwerke, mobile Apps, Analysen und Cloud. Apps und Dienste können schnell und kostengünstig verknüpft werden, um ein erweitertes Wertversprechen zu schaffen.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Zum Aufzeichnen quantitativer Daten für Ihre APIs gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **API Management-Dienst**.
2. Wählen Sie die gewünschte API aus der Liste aus.
3. Wählen Sie im Abschnitt **Überwachung** die Option **Diagnoseeinstellungen** aus.

Zum Anzeigen quantitativer Daten für Ihre APIs gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **API Management-Dienst**.
2. Wählen Sie die gewünschte API aus der Liste aus.
3. Wählen Sie im Abschnitt **Überwachung** die Option **Anwendung** aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Um den API Management-Dienst zu öffnen, wechseln Sie zum [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

Dieser Artikel hilft Ihnen bei der Verwendung von [Azure Monitor zum Abrufen von Feedback zu APIs](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor).

## <a name="qualitative-feedbacktabqualitative"></a>[Qualitatives Feedback](#tab/Qualitative)

Feedback wird in Form von User Storys im Backlog (oder Board) aufgezeichnet. Dort werden auch die zugehörigen Arbeiten als ausführbare Aufgaben nachverfolgt. Azure Boards können direkt in GitHub integriert werden, was ein nahtloses Zusammenwirken von Feedback/Arbeitsverwaltung und beliebigem Quellcode ermöglicht.

::: zone target="docs"

### <a name="action"></a>Aktion

Azure Boards und Azure Pipelines erfordern ein separates Portal von GitHub und Azure.
Informationen zu den ersten Schritten mit beiden Tools finden Sie unter [Azure DevOps](https://dev.azure.com/).

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Aktion

Zum Erstellen eines DevOps-Projekts gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Azure DevOps-Projekt**.
2. Klicken Sie auf **DevOps-Projekt erstellen**.
3. Wählen Sie **Runtime, Framework und Dienst** aus.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Project" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

Die folgenden Links helfen beim Zentralisieren und Verwalten von Feedback mithilfe von Azure Boards in Verbindung mit GitHub:

- [Erste Schritte mit Azure Boards](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)
- [Azure Boards und GitHub](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Schließen der Schleife mit Pipelines](#tab/pipelines)

Das Reagieren auf Feedback führt möglicherweise nicht immer zu dem vom Kunden geforderten Feature. Jeder Datenpunkt sollte aber eine Änderung in irgendeiner Form bewirken. Diese Änderung kann auch in einer anderen Denkweise in Bezug auf bestimmte Dinge bestehen. Es kann sich ebenso um eine ganz andere technische Änderung handeln, als angefordert wurde. In jedem Fall bieten Ihnen Bereitstellungspipelines und Tools wie Azure Pipelines die Möglichkeit, diese Änderungen schnell zu veröffentlichen, sodass sie regelmäßig für den Kunden freigegeben werden können.

Zum Anzeigen aktiver Bereitstellungen in Bezug auf Ihre in Azure gehosteten Anwendungen gehen Sie folgendermaßen vor:

### <a name="action"></a>Aktion

Zum Anzeigen aktueller Bereitstellungen in ihrer Pipeline gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **App Service**.
2. Wählen Sie die gewünschte Anwendung aus der Liste aus.
3. Wählen Sie im Bereich „App Services“ im Abschnitt **Bereitstellung** die Option **Bereitstellungscenter** aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Um Ihre Anwendungen in App Service anzuzeigen, wechseln Sie zum [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

Es folgen einige zusätzliche Links für den Einstieg in das Erstellen Ihrer Bereitstellungspipelines:

- [Erstellen Ihrer ersten Pipeline](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [GitHub-Releaseaufgaben](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
