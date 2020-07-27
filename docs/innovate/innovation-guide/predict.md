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
ms.openlocfilehash: 74db213a6d03eaf3df75f8eed88260bb1e457cee
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86448859"
---
<!-- cSpell:ignore ONNX -->

::: zone target="docs"

# <a name="azure-innovation-guide-innovate-with-ai"></a>Azure-Innovationsleitfaden: Innovationen mit KI

::: zone-end

::: zone target="chromeless"

# <a name="innovate-with-ai"></a>Innovationen mit KI

::: zone-end

Als Innovator verfügt Ihr Unternehmen über umfassende Informationen zum Geschäft und seinen Kunden. Mithilfe von KI kann Ihr Unternehmen Vorhersagen zu Kundenanforderungen machen, Geschäftsprozesse automatisieren, verborgene Informationen in unstrukturierten Daten entdecken und neue Wege der Interaktion mit Kunden schaffen, um bessere Erfahrungen zu bieten. In diesem Artikel werden einige Ansätze für Innovationen mit KI vorgestellt. Die folgende Tabelle kann Sie dabei unterstützen, die beste Lösung für Ihre Implementierungsanforderungen zu finden.

| Lösungskategorie | BESCHREIBUNG                                                                                                                              | Erforderliche Kenntnisse              |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| Machine Learning            | **Azure Machine Learning** <br> Erstellen, Bereitstellen und Verwalten eigener Machine Learning-Modelle                                                       | Data Scientist und Entwickler |
| KI-Anwendungen und -Agents             | **Azure Cognitive Services** <br> Verwenden domänenspezifischer KI-Modelle für maschinelles Sehen, Sprach- und Texterkennung sowie Entscheidungsfindung, die mit Ihren Daten angepasst werden können <br><br> **Azure Bot Service** <br> Verbessern der Interaktion mit Kunden durch Hinzufügen von Bots zu Ihren Anwendungen und Websites | Entwickler                    |
| Knowledge Mining            | **Azure Cognitive Search** <br> Entdecken von Erkenntnissen, die in Inhalten wie Dokumenten, Verträgen, Bildern und anderen Datentypen verborgen sind      | Entwickler                    |

## <a name="machine-learning"></a>[Machine Learning](#tab/MachineLearning)

Azure bietet erweiterte Machine Learning-Funktionen. Mit Azure Machine Learning können Sie Ihre Machine Learning-Modelle schnell und einfach in der Cloud und Edge-übergreifend erstellen, trainieren und bereitstellen. Entwickeln Sie Modelle schneller mit automatisiertem Machine Learning. Verwenden Sie Tools und Frameworks Ihrer Wahl, ohne darauf begrenzt zu sein.

Weitere Informationen zu den ersten Schritten mit Azure Machine Learning finden Sie in der [Übersicht über Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml) und im Tutorial zu den [ersten Schritten mit dem ersten Machine Learning-Experiment](https://docs.microsoft.com/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Weitere Informationen zum Open-Source-Modellformat und zur Runtime für Machine Learning finden Sie in der Dokumentation zu [ONNX Runtime](http://onnxruntime.ai).

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Aktion

Ein Data Scientist kann mithilfe von Azure Machine Learning ein Modell anhand erweiterter Sprachen wie Python und R trainieren und erstellen sowie eine visuelle Drag-&-Drop-Oberfläche verwenden. Erste Schritte mit Azure Machine Learning:

1. Suchen Sie im Azure-Portal nach **Machine Learning**, und wählen Sie den Eintrag aus.

1. Wählen Sie **Hinzufügen** aus, und folgen Sie dann den Schritten im Portal zum Erstellen eines Arbeitsbereichs.

1. Der neue Arbeitsbereich bietet Data Scientists einen codebasierten Ansatz mit wenig Code zum Trainieren, Erstellen, Bereitstellen und Verwalten von Modellen.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning resources" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Machine Learning-Ressourcen im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="ai-applications-and-agents"></a>[KI-Anwendungen und -Agents](#tab/AIAppsAndAgents)

Azure bietet eine Reihe von vorgefertigten KI-Diensten mit Namen Cognitive Services zum problemlosen Erstellen von KI-Anwendungen. Außerdem stellt Azure einen Botdienst bereit, der Entwicklern das Erstellen von interaktiven KI-Agents ermöglicht, die die Interaktion zwischen Kunden und Mitarbeitern verbessern.

### <a name="ai-applications"></a>KI-Anwendungen

Cognitive Services ermöglicht es Ihnen, die KI-Funktionen für maschinelles Sehen, Sprach- und Texterkennung sowie Entscheidungsfindung in Ihre Anwendungen zu integrieren, ohne dass ein zusätzliches Training für Vorhersagemodelle erforderlich ist. Diese Dienste sind optimal und effektiv, wenn Sie keinen Data Scientist im Team haben, der das Vorhersagemodell trainiert. Für einige Dienste ist kein Training erforderlich. Andere Dienste erfordern nur ein minimales Training.

Eine Liste der verfügbaren Dienste für maschinelles Sehen, Sprach- und Texterkennung sowie Entscheidungsfindung, einschließlich des möglicherweise erforderlichen Trainingsaufwands, finden Sie in der Dokumentation zu [Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

#### <a name="action"></a>Aktion

Erste Schritte mit einer Cognitive Services-API:

1. Suchen Sie im Azure-Portal nach **Cognitive Services**, und wählen Sie den Eintrag aus.

1. Wählen Sie **Hinzufügen** aus, um eine Cognitive Services-API in Azure Marketplace zu finden.

1. Suchen Sie nach einem Dienst, und wählen Sie ihn aus:

    - Wenn Sie den Namen des Diensts kennen, den Sie verwenden möchten, geben Sie den Namen in das Feld **Marketplace durchsuchen** ein, und wählen Sie dann den Dienst aus.

    - Um eine Liste der Cognitive Services-APIs anzuzeigen, klicken Sie neben der Überschrift **Cognitive Services** auf **Mehr anzeigen**, und wählen Sie dann den Dienst aus.

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

Interagieren Sie mit Ihren Kunden auf natürlichere Weise und verbessern Sie die Kommunikation durch Konversationsumgebungen unterstützt von Bot Framework und Azure Bot Service. Verwenden Sie außerdem Cognitive Services-APIs wie Language Understanding (LUIS), QnA Maker und den Speech-Dienst, damit Ihre Kunden allgemeine Aufgaben selbstständig ausführen können und sich die Mitarbeiter im Callcenter auf differenziertere, hochwertigere Fälle konzentrieren können.

Weitere Informationen zum Erstellen von Bots finden Sie im Lernpfad für [Azure Bot Service](https://docs.microsoft.com/learn/paths/create-bots-with-the-azure-bot-service/).

#### <a name="action"></a>Aktion

Erste Schritte mit Azure Bot Service:

1. Suchen Sie im Azure-Portal nach **Bot Services**, und wählen Sie den Eintrag aus.

1. Wählen Sie **Hinzufügen** und dann **Web-App-Bot** oder **Registrierung von Botkanälen** aus.

1. Wählen Sie **Erstellen** aus, und führen Sie dann die Schritte im Portal zum Bereitstellen des Diensts aus.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices]" submitText="Go to Azure Bot Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Navigieren Sie direkt zu Azure Bot Service im [Azure-Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices).

::: zone-end

## <a name="knowledge-mining"></a>[Knowledge Mining](#tab/KnowledgeMining)

Verwenden Sie Azure Cognitive Search, um mögliche Erkenntnisse aus den Inhalten wie Dokumenten, Verträgen, Bildern und Medien zu ziehen. Verwenden Sie den einzigen Cloudsuchdienst mit integrierten KI-Funktionen, entdecken Sie Muster und Beziehungen in Ihren Inhalten, erkennen Sie die Stimmung, extrahieren Sie Schlüsselwörter und vieles mehr.

<!-- docsTest:ignore "Azure Search" -->

Azure Cognitive Search (früher „Azure Search“) verwendet den gleichen integrierten Microsoft-Stapel für natürliche Sprache, der von Bing und Microsoft Office schon seit mehr als einem Jahrzehnt eingesetzt wird, sowie KI-Dienste für maschinelles Sehen, Sprach- und Texterkennung. Verbringen Sie mehr Zeit mit Innovationen und weniger Zeit mit der Verwaltung einer komplexen Cloudsuchlösung.

Weitere Informationen finden Sie unter [Was ist Azure Cognitive Search?](https://docs.microsoft.com/azure/search/search-what-is-azure-search)

### <a name="action"></a>Aktion

Erste Schritte mit Azure Cognitive Search:

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
