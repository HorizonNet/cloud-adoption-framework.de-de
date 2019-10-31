---
title: 'Azure-Innovationsleitfaden: Vorhersagen und Beeinflussen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Ihnen Azure das Vorhersagen und Beeinflussen ermöglicht.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b2ed1b072d5226649e5248e350edfa3578978c4c
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769256"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Azure-Innovationsleitfaden: Vorhersagen und Beeinflussen

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Vorhersagen und Beeinflussen

::: zone-end

Als Innovator hat Ihr Unternehmen Einblicke in die Daten, das Verhalten und die Anforderungen Ihrer Kundenbasis. Diese Erkenntnisse können dabei helfen, die Anforderungen Ihrer Kunden vorherzusagen, bevor sie sich dieser Anforderungen überhaupt bewusst sind. In diesem Artikel werden einige Ansätze zur Bereitstellung von Vorhersagelösungen vorgestellt. Im darauf folgenden Abschnitt werden Methoden zum Integrieren dieser Vorhersagen in Ihre Lösung erläutert, um das Kundenverhalten zu beeinflussen.

Die folgende Tabelle soll Ihnen helfen, die beste Lösung für Ihre Implementierungsanforderungen zu finden.

|Dienst  |Vordefinierte Modelle  |Erstellen und Experimentieren  |Trainieren und Erstellen mit Python|Erforderliche Kenntnisse|
|---------|---------|---------|---------|---------|
|Cognitive Services|Ja|Nein|Nein|API- und Entwicklerkenntnisse|
|Azure Machine Learning Studio|Ja|Ja|Nein|Allgemeine Kenntnisse der Vorhersagealgorithmen|
|Azure Machine Learning-Dienst|Ja|Ja|Ja|Data Scientist|

## <a name="azure-cognitive-servicestabcognitiveservices"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Der schnellste und einfachste Weg zu Vorhersagen ist Azure Cognitive Services. Cognitive Services ermöglicht Vorhersagen auf Grundlage vorhandener Modelle, die keinen zusätzlichen Trainingsaufwand erfordern. Diese Dienste sind optimal geeignet, wenn kein Data Scientist unter den Mitarbeitern vorhanden ist, der das Vorhersagemodell trainieren kann. Bei einigen Diensten ist kein Training erforderlich. Andere erfordern nur minimales Training.

Eine Liste der verfügbaren Dienste und des erforderlichen Trainingsaufwands finden Sie unter [Cognitive Services und maschinelles Lernen](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Aktion

Zum Verwenden einer Cognitive Service-API gehen Sie folgendermaßen vor:

1. Navigieren Sie zu **Cognitive Services**.
2. Klicken Sie auf **Hinzufügen+** , um im Marketplace nach einem Cognitive Service zu suchen.
3. Wenn Sie den Namen des zu verwendenden Diensts kennen, können Sie den Dienstnamen im Textfeld **Marketplace durchsuchen** eingeben.
4. Sie können auch eine Liste von Cognitive Services anzeigen, indem Sie neben dem Cognitive Services-Header auf den Link **Mehr anzeigen** klicken.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Cognitive Services im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts).

::: zone-end

## <a name="azure-machine-learning-studiotabmachinelearningstudio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Wenn die vorhandenen Modelle in Cognitive Services nicht der gewünschten Vorhersage entsprechen, bietet Azure Machine Learning Studio die Möglichkeit, die gewünschten Vorhersagen zu erstellen, ohne dass umfassende Kenntnisse eines Data Scientists erforderlich sind.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Mit Azure Machine Learning Studio können Sie ein Modell erstellen und mit diesem Modell experimentieren:

1. Navigieren Sie zu **Azure Machine Learning Studio**.
2. Klicken Sie auf **Machine Learning Studio-Arbeitsbereich erstellen**, und folgen Sie den Anweisungen zum Erstellen eines Arbeitsbereichs.
3. Der neue Arbeitsbereich bietet eine Drag & Drop-Schnittstelle zum Erstellen eines Modells und zum Experimentieren mit dem Modell als Alternative zu einem tief gehenden Training.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Machine Learning Studio im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces).

::: zone-end

## <a name="azure-machine-learning-servicetabmachinelearningservice"></a>[Azure Machine Learning Service](#tab/MachineLearningService)

Azure Machine Learning Service bietet den tiefer gehenden codebasierten Ansatz, der für ein tiefer gehendes Training von Kundendatasets erforderlich ist. Mithilfe von Sprachen wie Python können Data Scientists einen Algorithmus trainieren und anschließend erstellen, um Kundenanforderungen vorherzusagen.

### <a name="action"></a>Aktion

Ein Data Scientist kann mithilfe eines Azure Machine Learning Service ein Modell anhand erweiterter Sprachen wie Python trainieren und erstellen:

1. Navigieren Sie zu **Azure Machine Learning Service**.
2. Klicken Sie auf **Machine Learning Service-Arbeitsbereiche erstellen**, und folgen Sie den Anweisungen zum Erstellen eines Arbeitsbereichs.
3. Der neue Arbeitsbereich bietet einen codebasierten Ansatz für Data Scientists zum Trainieren und Erstellen von Modellen, die erweiterte Analysen zur genauen Vorhersage von Kundenanforderungen benötigen.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces]" submitText="Go to Azure Machine Learning Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Machine Learning Studio im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces).

::: zone-end

## <a name="influence"></a>Einfluss

Alle oben genannten Ansätze ergeben eine API, die das Vorhersagemodell für Anwendungen verfügbar macht. Verwenden Sie innerhalb Ihrer Lösung einen dieser Ansätze, um von Ihren Kunden gesammelte Daten einer Vorhersage-API zuzuführen. Die Ergebnisse können dann als empfohlener nächster Schritt in die Kundenoberfläche integriert werden.

In diesen nächsten Schritten wird versucht, die Verhaltensmuster der Kunden zu formen und deren Reaktionen zu beeinflussen. Da die empfohlenen nächsten Schritte auf Vorhersagealgorithmen basieren, werden die vorherigen Kunden und verfügbaren Daten verwendet, um die Kundenanforderung vorherzusagen und diese Anforderung zu erfüllen, häufig bevor sich der Kunde dieser Anforderung überhaupt bewusst ist.
