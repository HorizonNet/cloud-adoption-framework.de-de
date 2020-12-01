---
title: MLOps mit Azure Machine Learning
description: In diesem Artikel erfahren Sie mehr über die Prinzipien und Methoden von Machine-Learning-Vorgängen (MLOps), die die Effizienz von Workflows wie Continuous Integration, der Zustellung und der Bereitstellung steigern.
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: aa4a7983868af3250ac85cb700ce828cec3fe008
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879479"
---
# <a name="machine-learning-operations-with-azure-machine-learning"></a>Machine-Learning-Vorgänge mit Azure Machine Learning

Machine-Learning-Vorgänge (Machine Learning Operations, MLOps) basieren auf den DevOps-Prinzipien und -Methoden, die die Effizienz von Workflows wie Continuous Integration, der Zustellung und der Bereitstellung steigern. MLOps wendet diese Prinzipien auf den Machine Learning-Prozess mit folgendem Ziel an:

- Schneller experimentieren und Modelle entwickeln.
- Schnellere Bereitstellung von Modellen für die Produktion.
- Ausüben und Optimieren der Qualitätssicherung.

Azure Machine Learning bietet die folgenden MLOps-Features:

- **Erstellen reproduzierbarer Pipelines.** Mit Machine Learning-Pipelines können Sie wiederholbare und wiederverwendbare Schritte für Ihre Datenaufbereitungs-, Trainings- und Bewertungsprozesse definieren.
- **Erstellen Sie wiederverwendbare Softwareumgebungen** für das Training und die Bereitstellung von Modellen.
- **Registrieren, Verpacken und Bereitstellen von Modellen von überall aus.** Sie können die zugehörigen Metadaten nachverfolgen, die für die Verwendung des Modells erforderlich sind.
- **Erfassung der Governancedaten für den End-to-End-Lebenszyklus.** Die protokollierten Informationen können umfassen, wer die Modelle veröffentlicht, warum Änderungen vorgenommen wurden und wann die Modelle bereitgestellt oder in der Produktionsumgebung verwendet wurden.
- **Benachrichtigen und Warnen bei Ereignissen im Lebenszyklus.** Beispielsweise können Sie Warnungen für die Durchführung von Experimenten, die Registrierung und Implementierung von Modellen sowie die Erkennung von Datendrift abrufen.
- **Überwachen von Anwendungen auf betriebliche und Machine Learning-Probleme.** Vergleichen Sie Modelleingaben zwischen Trainings- und Rückschlussphase, untersuchen Sie modellspezifische Metriken, und stellen Sie Überwachungsfunktionen und Warnungen für Ihre Machine Learning-Infrastruktur bereit.
- **Automatisieren des End-to-End-Machine Learning-Lebenszyklus mit Azure Machine Learning und Azure Pipelines.** Mithilfe von Pipelines können Sie Modelle regelmäßig aktualisieren, neue Modelle testen und fortlaufende Rollouts von neuen Machine Learning-Modellen zusätzlich zu Ihren anderen Anwendungen und Diensten durchführen.

## <a name="best-practices-for-mlops-with-azure-machine-learning"></a>Bewährte Methoden für MLOps mit Azure Machine Learning

Modelle unterscheiden sich von Code, da sie eine natürliche Lebensdauer haben und sich ihre Funktion verschlechtert, wenn sie nicht gewartet werden. Nach ihrer Bereitstellung können sie einen echten Geschäftswert bieten, insbesondere wenn Datenanalysten über die Tools zur Einführung von standardmäßigen Entwicklungsverfahren verfügen.

MLOps mit Azure unterstützt Sie bei folgenden Vorgängen:

- Erstellen Sie reproduzierbare Modelle und wiederverwendbare Trainingspipelines.
- Vereinfachen der Paketerstellung, Überprüfung und Bereitstellung von Modellen für die Qualitätslenkung und A/B-Tests
- Erklären und beobachten Sie das Modellverhalten, und automatisieren Sie den Prozess für das erneute Trainieren.

MLOps verbessert die Qualität und Konsistenz ihrer Machine Learning-Lösungen. Weitere Informationen zur Verwaltung des Lebenszyklus Ihrer Modelle mit Azure Machine Learning finden Sie unter [MLOps: Modellverwaltung, -bereitstellung und -überwachung mit Azure Machine Learning](/azure/machine-learning/concept-model-management-and-deployment).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen finden Sie in den folgenden Ressourcen:

- [MLOps: Verwaltung, Bereitstellung und Überwachung von Modellen mit Azure Machine Learning](/azure/machine-learning/concept-model-management-and-deployment)
- [Bereitstellen von Modellen mit Azure Machine Learning](/azure/machine-learning/how-to-deploy-and-where)
- Tutorial: [Bereitstellen eines Imageklassifizierungsmodells in Azure Container Instances](/azure/machine-learning/tutorial-deploy-models-with-aml)
- [Repository mit End-to-End-Beispielen für MLOps](https://github.com/microsoft/MLOps)
- [CI/CD von Machine Learning-Modellen mit Azure Pipelines](/azure/devops/pipelines/targets/azure-machine-learning?tabs=yaml&view=azure-devops)
- Erstellen von Clients, die ein [bereitgestelltes Modell nutzen](/azure/machine-learning/how-to-consume-web-service)
- [Bedarfsorientiertes Machine Learning](/azure/architecture/data-guide/big-data/machine-learning-at-scale)
- [Repository mit bewährten Methoden und Referenzarchitekturen für Azure KI](https://github.com/microsoft/AI)
