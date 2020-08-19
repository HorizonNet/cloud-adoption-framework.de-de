---
title: Machine Learning
description: Diese Checklisten und Ressourcen dienen Ihnen als Hilfe bei der Anwendungsentwicklung und -bereitstellung.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3fb28e0f68a5eddaff094a3f16640689cad48769
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88568548"
---
<!-- cSpell:ignore scikit RLlib ONNX Jupyter -->

# <a name="machine-learning"></a>Machine Learning

Azure bietet Ihnen die fortschrittlichsten Machine-Learning-Funktionen Sie können Machine Learning-Modelle schnell und einfach mit Azure Machine Learning erstellen, trainieren und bereitstellen. Machine Learning kann für alle Arten von maschinellem Lernen verwendet werden. Der Anwendungsbereich reicht von klassischem Machine Learning bis zu Deep Learning, überwachtem und nicht überwachtem Lernen. Unabhängig davon, ob Sie das Schreiben von Python- oder R-Code oder die Nutzung von Optionen ohne bzw. mit nur wenig Code (z. B. per [Designer](/azure/machine-learning/tutorial-designer-automobile-price-train-score)) bevorzugen, können Sie in einem Machine Learning-Arbeitsbereich hochpräzise Machine Learning- und Deep Learning-Modelle erstellen, trainieren und nachverfolgen.

Sie können auch auf Ihrem lokalen Computer mit dem Training beginnen und dann eine Aufskalierung auf die Cloud durchführen. Der Dienst kann auch zusammen mit beliebten Open-Source-Tools für Deep Learning und vertiefendes Lernen (etwa PyTorch, TensorFlow, scikit-learn, Ray und RLlib) genutzt werden.

Erste Schritte mit [Azure Machine Learning](/azure/machine-learning/): Ein Tutorial zum Einstieg finden Sie unter [Tutorial: Erste Schritte beim Erstellen Ihres ersten ML-Experiments mit dem Python SDK](/azure/machine-learning/tutorial-1st-experiment-sdk-setup). Weitere Informationen zum Open-Source-Modellformat und zur Runtime für Machine Learning finden Sie unter [ONNX Runtime](http://onnxruntime.ai).

Gängige Szenarios für Machine-Learning-Lösungen sind:

- Predictive Maintenance
- Bestandsverwaltung
- Betrugserkennung
- Bedarfsvorhersage
- Intelligente Empfehlungen
- Verkaufsvorhersage

## <a name="checklist"></a>Checkliste

- **Machen Sie sich zunächst mit Machine Learning vertraut**, und wählen Sie dann aus, mit welchem Prozess Sie beginnen möchten. Sie können die Schritte zum Verwenden eines Jupyter-Notebooks mit Python, der visuellen Drag & Drop-Funktion oder der Funktion zum automatisierten Machine Learning (AutoML) befolgen.

  - [Was ist Azure Machine Learning?](/azure/machine-learning/overview-what-is-azure-ml)
  - [Erstellen Ihres ersten Machine-Learning-Experiments mit einem Jupyter-Notebook mit Python](/azure/machine-learning/tutorial-1st-experiment-sdk-setup)
  - [Visuelle Drag & Drop-Experimente](/azure/machine-learning/tutorial-designer-automobile-price-train-score)
  - [Verwenden der AutoML-Benutzeroberfläche](/azure/machine-learning/tutorial-first-experiment-automated-ml)
  - [Konfigurieren einer Entwicklungsumgebung für Azure Machine Learning](/azure/machine-learning/how-to-configure-environment)

- **Experimentieren Sie mit erweiterten Tutorials**, um Taxigebühren vorherzusagen, Bilder zu klassifizieren und eine Pipeline für die Batchbewertung zu erstellen.

  - [Tutorial: Vorhersagen von Preisen für Taxifahrten mit automatisiertem maschinellem Lernen](/azure/machine-learning/tutorial-auto-train-models)
  - [Klassifizieren von Bildern mit scikit-learn](/azure/machine-learning/tutorial-train-models-with-aml)
  - [Tutorial: Erstellen einer Azure Machine Learning-Pipeline für die Batchbewertung](/azure/machine-learning/tutorial-pipeline-batch-scoring-classification)

- **Sehen Sie sich die Videotutorials an**, um mehr über die Vorteile von Machine Learning wie die Modellerstellung ohne Code, MLOps, ONNX Runtime, Modellinterpretierbarkeit und -transparenz und mehr zu erfahren.

  - [Neuerungen in Machine Learning](https://channel9.msdn.com/Shows/AI-Show/Allup-Azure-ML)
  - [Verwenden von AutoML zur Modellerstellung](https://aka.ms/automlvideo)
  - [Erstellen von Modellen ohne Code mit dem Machine Learning-Designer](https://aka.ms/studioanddesigner)
  - [MLOps zum Verwalten des End-to-End-Lebenszyklus](https://aka.ms/mlopsvideo)
  - [Einbinden der ONNX Runtime in Ihre Modelle](https://www.youtube.com/watch?v=qy7X2JGLUC4)
  - [Modellinterpretierbarkeit und -transparenz](https://aka.ms/azuremlinterpret)
  - [Erstellen von Modellen mi R](https://aka.ms/Rmodels)

- [Überprüfen der Referenzarchitekturen für KI-Lösungen](/azure/architecture/browse/#ai--machine-learning)

## <a name="next-steps"></a>Nächste Schritte

Erkunden Sie andere Kategorien für KI-Lösungen:

- [KI-Anwendungen und -Agents](./ai-applications.md)
- [Knowledge Mining](./knowledge-mining.md)
