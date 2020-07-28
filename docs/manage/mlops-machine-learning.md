---
title: MLOps mit Azure Machine Learning
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit den verschiedenen Übergängen vertraut zu machen, die erfolgen müssen, um die cloudbasierte Betriebsverwaltung zu ermöglichen.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e5320b72d89e89c4034480614272c526e61e97b1
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452588"
---
# <a name="mlops-with-azure-machine-learning"></a>MLOps mit Azure Machine Learning

Machine Learning-Vorgänge (MLOps) basieren auf DevOps-Prinzipien und -Methoden, die die Effizienz von Workflows erhöhen. Beispiele sind Continuous Integration, Continuous Delivery und Continuous Deployment. MLOps wendet diese Prinzipien auf den Machine Learning-Prozess mit folgendem Ziel an:

- Schnelleres Experimentieren und Entwickeln von Modellen
- Schnellere Bereitstellung von Modellen in der Produktionsumgebung
- Qualitätssicherung

Azure Machine Learning bietet die folgenden MLOps-Features:

- **Erstellen reproduzierbarer ML-Pipelines**. Mit Machine Learning-Pipelines können Sie wiederholbare und wiederverwendbare Schritte für Ihre Datenaufbereitungs-, Trainings- und Bewertungsprozesse definieren.
- **Erstellen Sie wiederverwendbare Softwareumgebungen**  für das Training und die Bereitstellung von Modellen.
- **Registrieren, Verpacken und Bereitstellen von Modellen von überall aus**. Sie können auch zugehörige Metadaten nachverfolgen, die für die Verwendung des Modells erforderlich sind.
- **Erfassung der Governancedaten für den End-to-End-ML-Lebenszyklus**. Die protokollierten Informationen können umfassen, wer die Modelle veröffentlicht, warum Änderungen vorgenommen wurden und wann die Modelle bereitgestellt oder in der Produktionsumgebung verwendet wurden.
- **Benachrichtigen und Warnen bei Ereignissen im ML-Lebenszyklus**. Beispielsweise die Durchführung von Experimenten, die Registrierung und Bereitstellung von Modellen sowie die Erkennung von Datendrift.
- **Überwachen von ML-Anwendungen auf betriebs- und ML-bezogene Probleme**. Vergleichen Sie Modelleingaben zwischen Trainings- und Inferenzphase, untersuchen Sie modellspezifische Metriken, und stellen Sie Überwachungsfunktionen und Warnungen für Ihre ML-Infrastruktur bereit.
- **Automatisieren des End-to-End-ML-Lebenszyklus mit Azure Machine Learning und Azure Pipelines**. Mithilfe von Pipelines können Sie Modelle regelmäßig aktualisieren, neue Modelle testen und fortlaufende Rollouts von neuen ML-Modellen zusätzlich zu Ihren anderen Anwendungen und Diensten durchführen.

## <a name="best-practices-for-mlops-with-azure-machine-learning"></a>Bewährte Methoden für MLOps mit Azure Machine Learning

Modelle unterscheiden sich von Code, da sie eine natürliche Lebensdauer haben und sich ihre Funktion verschlechtert, wenn sie nicht gewartet werden. Nach ihrer Bereitstellung können sie einen echten Geschäftswert bieten, insbesondere wenn Datenanalysten über die Tools zur Einführung von standardmäßigen Entwicklungsverfahren verfügen.

„Indem wir unseren Technologiestapel vereinheitlicht und unsere Techniker bei Big Data- und Onlinesoftwareprojekten mit Datenanalysten zusammengebracht haben, konnten wir die Entwicklungszeit von Monaten auf wenige Wochen reduzieren.“ *Naeem Khedarun, Principal Software Engineer, ASOS*

Mit MLOps in Azure können Sie Ihre Modelle schnell gewinnbringend nutzen und diesen Wert langfristig erhalten.

- Erstellen Sie reproduzierbare Modelle und wiederverwendbare Trainingspipelines.
- Vereinfachen Sie die Paketerstellung, Validierung und Bereitstellung von Modellen für die Qualitätslenkung, A/B-Tests und vieles mehr.
- Erklären und beobachten Sie das Modellverhalten, und automatisieren Sie den Prozess für das erneute Trainieren.

MLOps verbessert die Qualität und Konsistenz ihrer Machine Learning-Lösungen. Informationen zur Verwendung von Azure Machine Learning zum Verwalten des Lebenszyklus Ihrer Modelle finden Sie unter [MLOps: Verwaltung, Bereitstellung und Überwachung von Modellen mit Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/concept-model-management-and-deployment).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden Ressourcen:

- [MLOps: Verwaltung, Bereitstellung und Überwachung von Modellen mit Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/concept-model-management-and-deployment)
- [Bereitstellen von Modellen mit Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/how-to-deploy-and-where)
- Tutorial: [Bereitstellen eines Bildklassifizierungsmodells in Azure Container Instances](https://docs.microsoft.com/azure/machine-learning/tutorial-deploy-models-with-aml)
- [Repository mit End-to-End-Beispielen für MLOps](https://github.com/microsoft/MLOps)
- [CI/CD von ML-Modellen mit Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/targets/azure-machine-learning?view=azure-devops&tabs=yaml)
- Erstellen von Clients, die ein  [bereitgestelltes Modell nutzen](https://docs.microsoft.com/azure/machine-learning/how-to-consume-web-service)
- [Bedarfsorientiertes Machine Learning](https://docs.microsoft.com/azure/architecture/data-guide/big-data/machine-learning-at-scale)
- [Repository mit bewährten Methoden und Referenzarchitekturen für Azure KI](https://github.com/microsoft/AI)
