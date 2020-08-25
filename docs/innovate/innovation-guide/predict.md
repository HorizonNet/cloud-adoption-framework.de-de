---
title: 'Azure-Innovation: Innovationen mit KI'
description: Erfahren Sie mehr über Azure-Lösungen zum Vorhersagen von Kundenanforderungen, Automatisieren von Geschäftsprozessen, Entdecken verborgener Informationen in unstrukturierten Daten und neue Wege der Interaktion mit Kunden, um bessere Erfahrungen zu bieten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/26/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 2e8a4b21fa23eef21d0330c1f89e56fd7d56814a
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88567834"
---
<!-- cSpell:ignore ONNX -->

# <a name="innovate-with-ai"></a>Innovationen mit KI

Als Innovator verfügt Ihr Unternehmen über umfassende Informationen zum Geschäft und seinen Kunden. Mithilfe von KI hat Ihr Unternehmen folgende Möglichkeiten:

- Treffen von Vorhersagen zu Kundenanforderungen
- Automatisieren von Geschäftsprozessen
- Entdecken von Informationen, die in unstrukturierten Daten verborgen sind
- Zusammenarbeit mit Kunden auf neue Weise, um bessere Erfahrungen zu bieten

 In diesem Artikel werden einige Ansätze für Innovationen mit KI vorgestellt. Die folgende Tabelle kann Sie dabei unterstützen, die beste Lösung für Ihre Implementierungsanforderungen zu finden.

| Lösungskategorie | BESCHREIBUNG                                                                                                                              | Erforderliche Kenntnisse              |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| Machine Learning            | **Azure Machine Learning** <br> Erstellen, Bereitstellen und Verwalten eigener Machine Learning-Modelle                                                       | Data Scientist und Entwickler |
| KI-Anwendungen und -Agents             | **Azure Cognitive Services** <br> Verwenden domänenspezifischer KI-Modelle für maschinelles Sehen, Sprach- und Texterkennung sowie Entscheidungsfindung, die mit Ihren Daten angepasst werden können <br><br> **Azure Bot Service** <br> Verbessern der Interaktion mit Kunden durch Hinzufügen von Bots zu Ihren Anwendungen und Websites | Entwickler                    |
| Knowledge Mining            | **Azure Cognitive Search** <br> Entdecken von Erkenntnissen, die in Inhalten wie Dokumenten, Verträgen, Bildern und anderen Datentypen verborgen sind      | Entwickler                    |

## <a name="machine-learning"></a>Machine Learning

Azure bietet erweiterte Machine Learning-Funktionen. Mit Azure Machine Learning können Sie Ihre Machine Learning-Modelle in der Cloud und Edge-übergreifend erstellen, trainieren und bereitstellen. Entwickeln Sie Modelle schneller mit automatisiertem maschinellen Lernen. Verwenden Sie Tools und Frameworks Ihrer Wahl, ohne darauf begrenzt zu sein.

Weitere Informationen finden Sie in der [Übersicht über Azure Machine Learning](/azure/machine-learning/overview-what-is-azure-ml) und im Tutorial zu den [ersten Schritten mit dem ersten Machine Learning-Experiment](/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Weitere Informationen zum Open-Source-Modellformat und zur Runtime für Machine Learning finden Sie unter [ONNX Runtime](http://onnxruntime.ai).

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Ein Data Scientist kann mithilfe von Azure Machine Learning ein Modell anhand erweiterter Sprachen wie Python und R trainieren und erstellen sowie eine visuelle Drag-&-Drop-Oberfläche verwenden. Erste Schritte mit Azure Machine Learning:

1. Suchen Sie im Azure-Portal nach **Machine Learning**, und wählen Sie den Eintrag aus.

1. Wählen Sie **Hinzufügen** aus, und folgen Sie dann den Schritten im Portal zum Erstellen eines Arbeitsbereichs.

1. Der neue Arbeitsbereich bietet Data Scientists codebasierte Ansätze mit wenig Code zum Trainieren, Erstellen, Bereitstellen und Verwalten von Modellen.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning resources" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Machine Learning-Ressourcen im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="ai-applications-and-agents"></a>KI-Anwendungen und -Agents

Azure bietet eine Reihe von vorgefertigten KI-Diensten mit Namen Cognitive Services zum Erstellen von KI-Anwendungen. Außerdem stellt Azure einen Botdienst bereit, der Entwicklern das Erstellen von interaktiven KI-Agents ermöglicht, die die Interaktion zwischen Kunden und Mitarbeitern verbessern.

### <a name="ai-applications"></a>KI-Anwendungen

Cognitive Services ermöglicht es Ihnen, die KI-Funktionen für maschinelles Sehen, Sprach- und Texterkennung sowie Entscheidungsfindung in Ihre Anwendungen zu integrieren. Bei den meisten Vorhersagemodellen ist kein zusätzliches Training erforderlich. Diese Dienste sind nützlich, wenn keine Data Scientists für das Training des Vorhersagemodells verfügbar sind. Andere Dienste erfordern minimales Training.

Weitere Informationen über das möglicherweise erforderliche Training und eine Liste der verfügbaren Dienste für maschinelles Sehen, Sprach- und Texterkennung sowie Entscheidungsfindung finden Sie in der Dokumentation zu [Cognitive Services](/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

#### <a name="action"></a>Aktion

Erste Schritte mit einer Cognitive Services-API:

1. Suchen Sie im Azure-Portal nach **Cognitive Services**, und wählen Sie den Eintrag aus.

1. Wählen Sie **Hinzufügen** aus, um eine Cognitive Services-API in Azure Marketplace zu finden.

1. Suchen Sie nach einem Dienst, und wählen Sie ihn aus:

    - Wenn Sie den Namen des Diensts kennen, den Sie verwenden möchten, geben Sie den Namen in **Marketplace durchsuchen** ein. Wählen Sie dann den Dienst aus.

    - Um eine Liste der Cognitive Services-APIs anzuzeigen, klicken Sie neben der Überschrift **Cognitive Services** auf **Mehr anzeigen**. Wählen Sie dann den Dienst aus.

1. Wählen Sie **Erstellen** aus, und führen Sie dann die Schritte im Portal zum Bereitstellen des Diensts aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Cognitive Services im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

### <a name="ai-agents"></a>KI-Agents

Interagieren Sie mit Ihren Kunden auf natürlichere Weise und verbessern Sie die Kommunikation durch Konversationsumgebungen unterstützt von Bot Framework und Azure Bot Service. Verwenden Sie darüber hinaus Cognitive Services-APIs wie Language Understanding (LUIS), QnA Maker und den Speech-Dienst. Diese helfen Ihren Kunden bei allgemeinen Aufgaben und lassen Ihren Callcenter-Agents Zeit, sich auf differenziertere, anspruchsvollere Fälle zu konzentrieren.

Weitere Informationen zum Erstellen von Bots finden Sie unter [Azure Bot Service](/learn/paths/create-bots-with-the-azure-bot-service/).

#### <a name="action"></a>Aktion

Erste Schritte mit Azure Bot Service:

1. Suchen Sie im Azure-Portal nach **Bot Services**, und wählen Sie den Eintrag aus.

1. Wählen Sie **Hinzufügen** und dann **Web-App-Bot** oder **Registrierung von Botkanälen** aus.

1. Klicken Sie auf **Erstellen**. Führen Sie dann die Schritte im Portal zum Bereitstellen des Diensts aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices]" submitText="Go to Azure Bot Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Bot Service im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices).

::: zone-end

## <a name="knowledge-mining"></a>Knowledge Mining

Verwenden Sie Azure Cognitive Search, um mögliche Erkenntnisse aus den Inhalten wie Dokumenten, Verträgen, Bildern und Medien zu ziehen. Sie können Muster und Beziehungen in Ihren Inhalten entdecken, Stimmungen verstehen und Schlüsselbegriffe extrahieren.

<!-- docsTest:ignore "Azure Search" -->

Azure Cognitive Search verwendet denselben natürlichen Sprachstapel, den auch Bing und Microsoft Office verwenden. Verbringen Sie mehr Zeit mit Innovationen und weniger Zeit mit der Verwaltung einer komplexen Cloudsuchlösung.

Weitere Informationen finden Sie unter [Was ist Azure Cognitive Search?](/azure/search/search-what-is-azure-search)

### <a name="action"></a>Aktion

Erste Schritte:

1. Suchen Sie im Azure-Portal nach **Azure Cognitive Search**, und wählen Sie den Eintrag aus.

1. Führen Sie die Schritte im Portal zum Bereitstellen des Diensts aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FSearchServices]" submitText="Go to Azure Cognitive Search" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Cognitive Search im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FSearchServices).

::: zone-end

---
