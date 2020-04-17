---
title: 'Azure-Innovation: Vorhersagen und Beeinflussen'
description: Hier finden Sie Informationen zu Azure-Lösungen, mit denen Sie Kundenanforderungen vorhersagen und diese Vorhersagen in Ihre Lösung integrieren können, um das Kundenverhalten zu beeinflussen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 166c938b510959427a30cecea1c97de35032d20e
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80427000"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Azure-Innovationsleitfaden: Vorhersagen und Beeinflussen

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Vorhersagen und Beeinflussen

::: zone-end

Als Innovator hat Ihr Unternehmen Einblicke in die Daten, das Verhalten und die Anforderungen seiner Kunden. Die Untersuchung dieser Erkenntnisse kann helfen, die Anforderungen Ihrer Kunden vorherzusagen, möglicherweise bevor Ihre Kunden selbst diese Anforderungen kennen. In diesem Artikel werden einige Ansätze zur Bereitstellung von Vorhersagelösungen vorgestellt. In den abschließenden Abschnitten werden Methoden zum Integrieren der Vorhersagen in Ihre Lösung erläutert, um das Kundenverhalten zu beeinflussen.

Die folgende Tabelle kann Sie dabei unterstützen, die beste Lösung für Ihre Implementierungsanforderungen zu finden.

|Dienst  |Vordefinierte Modelle  |Erstellen und Experimentieren  |Trainieren und Erstellen von Lösungen mit Python|Erforderliche Kenntnisse|
|---------|---------|---------|---------|---------|
|Azure Cognitive Services|Ja|Nein|Nein|API- und Entwicklerkenntnisse|
|Azure Machine Learning Studio|Ja|Ja|Nein|Allgemeine Kenntnisse der Vorhersagealgorithmen|
|Azure Machine Learning-Dienst|Ja|Ja|Ja|Data Scientist|

## <a name="azure-cognitive-services"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Der schnellste und einfachste Weg zu Vorhersagen von Kundenanforderungen ist Azure Cognitive Services. Cognitive Services ermöglicht Vorhersagen auf Grundlage vorhandener Modelle, die keinen zusätzlichen Trainingsaufwand erfordern. Diese Dienste sind optimal und effektiv, wenn Sie keinen Data Scientist im Team haben, der das Vorhersagemodell trainiert. Bei einigen Diensten ist kein Training erforderlich. Andere Dienste erfordern nur minimales Training.

Eine Liste der verfügbaren Dienste und des ggf. erforderlichen Trainingsaufwands finden Sie unter [Cognitive Services und maschinelles Lernen](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Aktion

Zum Verwenden einer Cognitive Service-API gehen Sie folgendermaßen vor:

1. Navigieren Sie im [Azure-Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.CognitiveServices%2FAccounts) zu **Cognitive Services**.
2. Wählen Sie **Hinzufügen** aus, um eine Cognitive Services-API in Azure Marketplace zu finden.
3. Führen Sie einen der folgenden Schritte aus:
   - Wenn Sie den Namen des Diensts kennen, den Sie verwenden möchten, geben Sie den Namen im Feld **Marketplace durchsuchen** ein.
   - Eine Liste der Cognitive Services-APIs finden Sie unter dem Link **Mehr anzeigen** neben der Überschrift „Cognitive Services“.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Cognitive Services im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

## <a name="azure-machine-learning-studio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Wenn die vorhandenen Modelle in Cognitive Services nicht Ihrer gewünschten Vorhersage entsprechen, bietet Azure Machine Learning Studio die Möglichkeit, die gewünschten Vorhersagen zu erstellen, ohne dass umfassende Kenntnisse eines Data Scientists erforderlich sind.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Sie können Azure Machine Learning Studio verwenden, um ein Modell zu erstellen und mit ihm zu experimentieren, indem Sie wie folgt vorgehen:

1. Navigieren Sie im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces) zu **Azure Machine Learning Studio**.
2. Wählen Sie **Machine Learning Studio-Arbeitsbereich erstellen** aus, und befolgen Sie die Anweisungen zum Erstellen eines Arbeitsbereichs.

   Der neue Arbeitsbereich bietet eine Drag & Drop-Schnittstelle zum Erstellen eines Modells und zum Experimentieren mit dem Modell als Alternative zu einem Deep Training-Ansatz.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Machine Learning Studio im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces).

::: zone-end

## <a name="azure-machine-learning-service"></a>[Azure Machine Learning-Dienst](#tab/MachineLearningService)

Azure Machine Learning Service bietet den tiefer gehenden codebasierten Ansatz, der für Deep Training von Kundendatasets erforderlich ist. Mithilfe von Sprachen wie Python können Data Scientists ein Modell trainieren und anschließend einen Algorithmus erstellen, um Kundenanforderungen vorherzusagen.

### <a name="action"></a>Aktion

Ein Data Scientist kann mithilfe eines Azure Machine Learning Service ein Modell anhand erweiterter Sprachen wie Python trainieren und erstellen:

1. Navigieren Sie zu **Azure Machine Learning Service**.
2. Wählen Sie **Machine Learning Service-Arbeitsbereiche erstellen** aus, und befolgen Sie die Anweisungen zum Erstellen eines Arbeitsbereichs.
3. Der neue Arbeitsbereich bietet einen codebasierten Ansatz für Data Scientists zum Trainieren und Erstellen von Modellen, die erweiterte Analysen zur genauen Vorhersage von Kundenanforderungen benötigen.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Machine Learning Studio im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="influence"></a>Einfluss

Alle oben genannten Ansätze ergeben eine API, die das Vorhersagemodell für Anwendungen verfügbar macht. Verwenden Sie innerhalb Ihrer Lösung einen dieser Ansätze, um von Ihren Kunden gesammelte Daten einer Vorhersage-API zuzuführen. Die Ergebnisse können dann als empfohlener nächster Schritt in die Kundenoberfläche integriert werden.

Die vorgeschlagenen nächsten Schritte können dazu beitragen, das Kundenverhalten zu gestalten und die Reaktion von Kunden zu beeinflussen. Da die vorgeschlagenen nächsten Schritte auf Vorhersagealgorithmen basieren, nutzen sie frühere Kundenanforderungen und verfügbare Daten, um zukünftige Kundenanforderungen vorherzusagen und zu erfüllen, oftmals bevor die Kunden selbst überhaupt wissen, dass diese Anforderungen bestehen.
