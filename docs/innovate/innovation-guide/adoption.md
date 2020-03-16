---
title: 'Azure-Innovation: Vorbereiten für Feedback'
description: Hier erfahren Sie, wie Sie mithilfe von Azure-Tools quantitatives und qualitatives Feedback zu in GitHub gehosteten Web-Apps und APIs erfassen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 95087aeda19eb87759bc09f605c42c706d79aac2
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78891952"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Azure-Innovationsleitfaden: Vorbereiten für Kundenfeedback

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Vorbereiten für Kundenfeedback

::: zone-end

Einführung, Interaktion und Bindung von Benutzern sind der Schlüssel für erfolgreiche Innovation. Warum?

Beim Erstellen einer innovativen neuen Lösung geht es nicht darum, dem Benutzer das zu geben, was er will oder glaubt zu wollen. Es geht um die Formulierung einer Hypothese, die getestet und als Basis für Verbesserungen verwendet werden kann. Diese Tests gibt es in zwei Formen:

- **Quantitative Tests (Testen von Feedback):** Dieses Feedback misst die Aktionen, die wir erwarten.
- **Qualitative Tests (Kundenfeedback):** Dieses Feedback informiert uns, was diese Metriken aus Sicht des Kunden bedeuten.

Bevor Sie Feedbackschleifen integrieren, benötigen Sie ein freigegebenes Repository für Ihre Lösung. Ein zentralisiertes Repository bietet die Möglichkeit, das gesamte Feedback zu Ihrem Projekt aufzuzeichnen und darauf zu reagieren. [GitHub](https://github.com) ist der zentrale Aufbewahrungsort für Open Source-Software. Dies ist auch eine der am häufigsten verwendeten Plattformen für das Hosting des Quellcoderepositorys für kommerziell entwickelte Apps. Der Artikel zum [Erstellen von GitHub-Repositorys](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) kann Ihnen bei den ersten Schritten mit Ihrem Repository helfen.

Jedes der folgenden Tools in Azure kann in Projekte integriert werden, die in GitHub gehostet werden (oder ist mit ihnen kompatibel):

## <a name="quantitative-feedback-for-web-apps"></a>[Quantitatives Feedback für Web-Apps](#tab/Quantitative-Apps)

Application Insights ist ein Überwachungstool, das quantitatives Feedback zur Nutzung Ihrer Anwendung nahezu in Echtzeit bereitstellt. Anhand dieses Feedbacks können Sie Ihre aktuelle Hypothese testen und überprüfen, um das nächste Feature oder die nächste User Story in Ihrem Backlog zu gestalten.

### <a name="action"></a>Aktion

Zum Anzeigen quantitativer Daten für Ihre Anwendungen gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Application Insights**.
   - Wenn Ihre Anwendung nicht in der Liste angezeigt wird, wählen Sie **Hinzufügen** aus, und befolgen Sie die Anweisungen, um mit der Konfiguration von Application Insights zu beginnen.
   - Wenn die gewünschte App in der Liste enthalten ist, wählen Sie die Anwendung aus.
1. Der Bereich **Übersicht** enthält einige Statistiken für die Anwendung. Wählen Sie **Anwendungsdashboard** aus, um ein benutzerdefiniertes Dashboard für Daten zu erstellen, die für ihre Hypothese von größerer Relevanz sind.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to Application Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Um die Daten zu Ihren Apps anzuzeigen, navigieren Sie zum [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

- [Einrichten von Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Erste Schritte mit Azure Monitor Application Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Erstellen eines Telemetriedashboards](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apis"></a>[Quantitatives Feedback für APIs](#tab/Quantitative-APIs)

Die vernetzte Wirtschaft verändert die Art und Weise, in der Unternehmen Innovationen entwickeln. Märkte und Branchen werden schneller als je zuvor gestört. Störungen treten in vielen Formen auf, und Unternehmen müssen sich mit dem _Dilemma des Innovators_ auseinandersetzen: Wie kann das Tempo des Wandels festgelegt werden, ohne die laufende Geschäftsaktivität zu beeinträchtigen?

Unternehmen verwenden extern APIs, um die Interaktion mit ihren Kunden und Partnern zu ändern. Intern verwenden sie APIs, um verschiedene Teile des Unternehmens nahtlos miteinander zu verbinden. Die API-Struktur basiert auf vier Bausteinen: soziale Netzwerke, mobile Apps, Analysen und Cloud. Apps und Dienste können schnell und kostengünstig verknüpft werden, um ein erweitertes Wertversprechen zu schaffen.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Zum Aufzeichnen quantitativer Daten für Ihre APIs gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **API Management-Dienste**.
2. Wählen Sie die gewünschte API aus der Liste aus.
3. Klicken Sie im Abschnitt **Überwachung** auf **Diagnoseeinstellungen**.

Zum Anzeigen quantitativer Daten für Ihre APIs gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **API Management-Dienste**.
2. Wählen Sie die gewünschte API aus der Liste aus.
3. Klicken Sie im Abschnitt **Überwachung** auf **Anwendung**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Um den API Management-Dienst zu öffnen, navigieren Sie zum [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

- [Verwenden von Azure Monitor zum Abrufen von Feedback zu APIs](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor)

## <a name="qualitative-feedback"></a>[Qualitatives Feedback](#tab/Qualitative)

Feedback wird in Form von User Storys im Backlog (oder Board) aufgezeichnet. Dort werden auch die zugehörigen Arbeiten als ausführbare Aufgaben nachverfolgt. Azure Boards können direkt in GitHub integriert werden, was ein nahtloses Zusammenwirken von Feedback und Arbeitsverwaltung sowie beliebigem Quellcode ermöglicht.

::: zone target="docs"

### <a name="action"></a>Aktion

Azure Boards und Azure Pipelines erfordern ein Portal, das von GitHub und Azure getrennt ist. Steigen Sie in [Azure DevOps](https://dev.azure.com) ein.

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Aktion

Zum Erstellen eines DevOps-Projekts gehen Sie folgendermaßen vor:

1. Navigieren zu **Azure DevOps Projects**.
2. Wählen Sie **DevOps-Projekt erstellen** aus.
3. Wählen Sie **Runtime, Framework und Dienst** aus.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Projects" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

Diese Artikel helfen Ihnen, Feedback zu zentralisieren und zu verwalten, indem Sie Azure Boards zusammen mit GitHub verwenden:

- [Erste Schritte mit Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/?view=azure-devops)
- [Azure Boards und GitHub](https://docs.microsoft.com/azure/devops/boards/github?view=azure-devops)

## <a name="close-the-loop-with-pipelines"></a>[Schließen der Schleife mit Pipelines](#tab/pipelines)

Das Reagieren auf Feedback bedeutet möglicherweise nicht immer, dass die vom Kunden gewünschte Funktion hinzugefügt wird. Aber jeder Datenpunkt sollte zu einer gewissen Änderung führen. Diese Änderung kann auch in einer anderen Denkweise in Bezug auf bestimmte Dinge bestehen. Es kann sich ebenso um eine ganz andere technische Änderung handeln, als angefordert wurde. In jedem Fall bieten Ihnen Bereitstellungspipelines und Tools wie Azure Pipelines die Möglichkeit, diese Änderungen schnell zu veröffentlichen, sodass sie regelmäßig mit dem Kunden geteilt werden können.

### <a name="action"></a>Aktion

Zum Anzeigen aktueller Bereitstellungen in ihrer Pipeline gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **App Services**.
2. Wählen Sie die gewünschte Anwendung aus der Liste aus.
3. Wählen Sie im Bereich „App Services“ im Abschnitt **Bereitstellung** die Option **Bereitstellungscenter** aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Um Ihre Anwendungen in App Service anzuzeigen, wechseln Sie zum [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Weitere Informationen

Beginnen Sie mit dem Erstellen Ihrer Bereitstellungspipelines:

- [Erstellen Ihrer ersten Pipeline](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [GitHub-Releaseaufgaben](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
