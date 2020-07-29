---
title: Machine Learning
description: Diese Checklisten und Ressourcen dienen Ihnen als Hilfe bei der Anwendungsentwicklung und -bereitstellung.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3cbc697e979f741342c3a75f38de8f4086cb4871
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452606"
---
<!-- cSpell:ignore scikit RLlib ONNX Jupyter -->

# <a name="machine-learning"></a>Machine Learning

Azure bietet Ihnen die fortschrittlichsten Machine-Learning-Funktionen Sie können das Machine Learning-Modell schnell und einfach mit Azure Machine Learning erstellen, trainieren und bereitstellen. Azure Machine Learning kann für alle Arten von Machine Learning verwendet werden – von klassischem Machine Learning bis zu Deep Learning und für überwachtes und nicht überwachtes Lernen. Unabhängig davon, ob Sie das Schreiben von Python- oder R-Code oder die Nutzung von Optionen ohne bzw. mit nur wenig Code (z. B. per [Designer](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score)) bevorzugen, können Sie in einem Azure Machine Learning-Arbeitsbereich hochpräzise Machine Learning- und Deep Learning-Modelle erstellen, trainieren und nachverfolgen.

Sie können auch auf Ihrem lokalen Computer mit dem Training beginnen und dann eine Aufskalierung auf die Cloud durchführen. Der Dienst kann auch zusammen mit beliebten Open-Source-Tools für Deep Learning und vertiefendes Lernen (etwa PyTorch, TensorFlow, scikit-learn, Ray und RLlib) genutzt werden.

Erste Schritte mit [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/). Ein Tutorial zum Einstieg finden Sie unter [Tutorial: Erste Schritte beim Erstellen Ihres ersten ML-Experiments mit dem Python SDK](https://docs.microsoft.com/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Weitere Informationen zum Open-Source-Modellformat und zur Laufzeit für Machine Learning finden Sie im [ONNX Runtime](http://onnxruntime.ai).

Gängige Szenarios für Machine-Learning-Lösungen sind:

- Predictive Maintenance
- Bestandsverwaltung
- Betrugserkennung
- Bedarfsvorhersage
- Intelligente Empfehlungen
- Verkaufsvorhersage

## <a name="checklist"></a>Checkliste

- **Machen Sie sich zunächst mit Azure Machine Learning vertraut**, und wählen Sie dann aus, mit welchem Prozess Sie beginnen möchten. Sie können die Schritte zum Verwenden eines Jupyter-Notebooks mit Python, der visuellen Drag & Drop-Funktion oder der Funktion zum automatisierten Machine Learning (AutoML) befolgen.

  - [Azure Machine Learning – Übersicht](https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml)
  - [Erstellen Ihres ersten Machine-Learning-Experiments mit einem Jupyter-Notebook mit Python](https://docs.microsoft.com/azure/machine-learning/tutorial-1st-experiment-sdk-setup)
  - [Visuelle Drag & Drop-Experimente](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score)
  - [Verwenden der AutoML-Benutzeroberfläche](https://docs.microsoft.com/azure/machine-learning/tutorial-first-experiment-automated-ml)
  - [Konfigurieren einer Entwicklungsumgebung für Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/how-to-configure-environment)

- **Experimentieren Sie mit erweiterten Tutorials**, um Taxigebühren vorherzusagen, Bilder zu klassifizieren und eine Pipeline für die Batchbewertung zu erstellen.

  - [Tutorial: Vorhersagen von Preisen für Taxifahrten mit automatisiertem maschinellem Lernen](https://docs.microsoft.com/azure/machine-learning/tutorial-auto-train-models)
  - [Klassifizieren von Bildern mit scikit-learn](https://docs.microsoft.com/azure/machine-learning/tutorial-train-models-with-aml)
  - [Tutorial: Erstellen einer Azure Machine Learning-Pipeline für die Batchbewertung](https://docs.microsoft.com/azure/machine-learning/tutorial-pipeline-batch-scoring-classification)

- **Sehen Sie sich die Videotutorials an**, um mehr über die Vorteile von Azure Machine Learning zu erfahren, einschließlich der Modellerstellung ohne Code, MLOps, ONNX Runtime, Modellinterpretierbarkeit und -transparenz und mehr.

  - [Neuerungen in Azure Machine Learning](https://channel9.msdn.com/Shows/AI-Show/Allup-Azure-ML)
  - [Verwenden von AutoML zur Modellerstellung](https://aka.ms/automlvideo)
  - [Erstellen von Modellen ohne Code mit Azure Machine Learning-Designer](https://aka.ms/studioanddesigner)
  - [MLOps zum Verwalten des End-to-End-Lebenszyklus](https://aka.ms/mlopsvideo)
  - [Einbinden der ONNX Runtime in Ihre Modelle](https://www.youtube.com/watch?v=qy7X2JGLUC4)
  - [Modellinterpretierbarkeit und -transparenz](https://aka.ms/azuremlinterpret)
  - [Erstellen von Modellen mi R](https://aka.ms/Rmodels)

- [Überprüfen der Referenzarchitekturen für KI-Lösungen](https://docs.microsoft.com/azure/architecture/browse/#ai--machine-learning)

## <a name="next-steps"></a>Nächste Schritte

Erkunden Sie andere Kategorien für KI-Lösungen:

- [KI-Anwendungen und -Agents](./ai-applications.md)
- [Knowledge Mining](./knowledge-mining.md)
