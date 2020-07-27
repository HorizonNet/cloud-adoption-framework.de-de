---
title: Was ist maschinelles Lernen?
description: Was ist maschinelles Lernen?
author: v-hanki
ms.author: janet
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: df003da24bc539dceb4ee31ebb4137dc83174de4
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452600"
---
<!-- cSpell:ignore scikit RLlib Jupyter MLflow Kubeflow -->

# <a name="what-is-machine-learning"></a>Was ist Machine Learning?

Machine Learning ist ein Data Science-Verfahren, mit dem Computer aus vorhandenen Daten lernen können, um zukünftiges Verhalten, Ergebnisse und Trends vorherzusagen. Durch den Einsatz von maschinellem Lernen können Computer lernen, ohne konkret programmiert worden zu sein.

Dank solcher Vorhersagen oder Prognosen durch maschinelles Lernen können Anwendungen und Geräte intelligenter werden. Wenn Sie beispielsweise online einkaufen, trägt maschinelles Lernen dazu bei, dass Ihnen anhand der gekauften Produkte weitere Produkte empfohlen werden, die Ihnen gefallen könnten. Ein weiteres Beispiel ist die Nutzung Ihrer Kreditkarte. Dabei wird mithilfe von maschinellem Lernen die Transaktion mit einer Transaktionsdatenbank verglichen, wodurch Betrugsfälle erkannt werden können. Auch wenn ein automatischer Staubsauger ein Zimmer saugt, wird mit maschinellem Lernen entschieden, ob die Arbeit erledigt ist.

## <a name="machine-learning-tools-to-fit-each-task"></a>Passende Machine Learning-Tools für alle Aufgaben

Azure Machine Learning verfügt über alle Tools, die Entwickler und Data Scientists für ihre Machine Learning-Workflows benötigen, z. B.:

- [Azure Machine Learning-Designer (Vorschauversion):](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score) Fügen Sie Module per Drag & Drop ein, um Ihre Experimente zu erstellen, und stellen Sie anschließend Pipelines bereit.
- Jupyter Notebooks: Verwenden Sie unsere [Beispielnotebooks](https://github.com/Azure/MachineLearningNotebooks), oder erstellen Sie eigene Notebooks, um unsere SDK-Beispiele für Python zu nutzen.
- R-Skripts oder Notebooks, in denen Sie das [SDK für R](https://azure.github.io/azureml-sdk-for-r/reference/index.html) zum Schreiben Ihres eigenen Codes verwenden (oder die R-Module im Designer).
- Der [Solution Accelerator für viele Modelle](https://github.com/microsoft/solution-accelerator-many-models) (Vorschauversion) baut auf Azure Machine Learning auf und ermöglicht Ihnen Training, Betrieb und Verwaltung von Hunderten oder sogar Tausenden Machine Learning-Modellen.
- [Visual Studio Code-Erweiterung](https://docs.microsoft.com/azure/machine-learning/tutorial-setup-vscode-extension)
- [Machine Learning-CLI](https://docs.microsoft.com/azure/machine-learning/reference-azure-machine-learning-cli)
- Open-Source-Frameworks, z. B. PyTorch, TensorFlow, scikit-learn und viele mehr
- [Vertiefendes Lernen](https://docs.microsoft.com/azure/machine-learning/how-to-use-reinforcement-learning) mit Ray RLlib

Sie können sogar [MLflow zum Nachverfolgen von Metriken und Bereitstellen von Modellen](https://docs.microsoft.com/azure/machine-learning/how-to-use-mlflow) oder [Kubeflow zum Erstellen von End-to-End-Workflowpipelines](https://www.kubeflow.org/docs/azure/) verwenden.

## <a name="build-machine-learning-models-in-python-or-r"></a>Erstellen von Machine Learning-Modellen in Python oder R

Beginnen Sie auf Ihrem lokalen Computer mit dem Azure Machine Learning [Python SDK](https://docs.microsoft.com/python/api/overview/azure/ml/?view=azure-ml-py) oder dem [R SDK](https://azure.github.io/azureml-sdk-for-r/reference/index.html) mit dem Training. Anschließend können Sie in die Cloud aufskalieren. Dank zahlreicher verfügbarer [Computeziele](https://docs.microsoft.com/azure/machine-learning/how-to-set-up-training-targets) wie Azure Machine Learning-Compute und [Azure Databricks](https://docs.microsoft.com/azure/databricks/scenarios/what-is-azure-databricks) sowie [Diensten für die erweiterte Hyperparameteroptimierung](https://docs.microsoft.com/azure/machine-learning/how-to-tune-hyperparameters) können Sie mithilfe der Cloud schneller bessere Modelle erstellen. Mit dem SDK können Sie auch [Modelltraining und -optimierung](https://docs.microsoft.com/azure/machine-learning/tutorial-auto-train-models) automatisieren.

## <a name="build-machine-learning-models-with-no-code-tools"></a>Erstellen von Machine Learning-Modellen mit Tools ohne Code

Optionen für Training und Bereitstellung ohne oder mit nur wenig Code:

- Azure Machine Learning-Designer (Vorschauversion)

  Verwenden Sie den Designer zum Aufbereiten von Daten, Trainieren, Testen, Bereitstellen, Verwalten und Nachverfolgen von Machine Learning-Modellen, ohne Code schreiben zu müssen. Für das Erstellen Ihres Modells ist keine Programmierung erforderlich, sondern einfach nur das visuelle Verbinden von Datasets und Modulen. Probieren Sie das [Tutorial zum Designer](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score) aus.

  Weitere Informationen finden Sie im [Übersichtsartikel über den Azure Machine Learning-Designer](https://docs.microsoft.com/azure/machine-learning/concept-designer).
- Benutzeroberfläche für automatisiertes maschinelles Lernen (AutoML)

  Erfahren Sie, wie Sie auf der benutzerfreundlichen Oberfläche [AutoML-Experimente](https://docs.microsoft.com/azure/machine-learning/tutorial-first-experiment-automated-ml) erstellen.

## <a name="mlops-deploy-and-lifecycle-management"></a>MLOps: Bereitstellung und Lebenszyklusverwaltung

Vorgänge des maschinellen Lernens (MLOps) basieren auf [DevOps](https://azure.microsoft.com/overview/what-is-devops/)-Prinzipien und -Methoden, die die Effizienz von Workflows erhöhen. Beispiele sind Continuous Integration, Continuous Delivery und Continuous Deployment. MLOps wendet diese Prinzipien auf den Machine Learning-Prozess mit folgendem Ziel an:

- Schnelleres Experimentieren und Entwickeln von Modellen
- Schnellere Bereitstellung von Modellen in der Produktionsumgebung
- Qualitätssicherung

Wenn Sie das richtige Modell haben, können Sie es ganz einfach in einem Webdienst, auf einem IoT-Gerät oder in Power BI verwenden. Weitere Informationen finden Sie im Artikel [Bereitstellen: wie und wo](https://docs.microsoft.com/azure/machine-learning/how-to-deploy-and-where).

Anschließend können Sie Ihre bereitgestellten Modelle verwalten, indem Sie das [Azure Machine Learning SDK für Python](https://docs.microsoft.com/python/api/overview/azure/ml/?view=azure-ml-py), [Azure Machine Learning Studio](https://ml.azure.com/) oder die [Machine Learning-CLI](https://docs.microsoft.com/azure/machine-learning/reference-azure-machine-learning-cli) verwenden.

Diese Modelle können genutzt werden, um Prognosen [in Echtzeit](https://docs.microsoft.com/azure/machine-learning/how-to-consume-web-service) oder [asynchron](https://docs.microsoft.com/azure/machine-learning/how-to-use-parallel-run-step) für große Datenmengen zurückzugeben.

Und dank fortschrittlicher[Machine Learning-Pipelines](https://docs.microsoft.com/azure/machine-learning/concept-ml-pipelines) können Sie bei jedem einzelnen Schritt – von der Datenaufbereitung über Training und Bewertung von Modellen bis hin zur Bereitstellung – zusammenarbeiten. Pipelines ermöglichen Folgendes:

- Automatisieren des End-to-End-Prozesses für maschinelles Lernen in der Cloud
- Wiederverwenden von Komponenten und Wiederholen von Schritten nur bei Bedarf
- Verwenden verschiedener Computeressourcen in jedem Schritt
- Ausführen von Batchbewertungsaufgaben

Falls Sie Skripts zum Automatisieren Ihres Machine Learning-Workflows nutzen möchten, helfen Ihnen die Befehlszeilentools der [Machine Learning-CLI](https://docs.microsoft.com/azure/machine-learning/reference-azure-machine-learning-cli) weiter. Hiermit können häufige Aufgaben erledigt werden, z. B. das Übermitteln einer Trainingsausführung oder das Bereitstellen eines Modells.

Informationen zu den ersten Schritten mit Azure Machine Learning finden Sie [hier](https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml#next-steps).

## <a name="automated-machine-learning"></a>Automatisiertes maschinelles Lernen

Data Scientists verbringen einen Großteil ihrer Zeit mit dem Durchlaufen von Modellen während der Experimentierphase. Der gesamte Prozess des Ausprobierens verschiedener Kombinationen aus Algorithmen und Hyperparametern, bis ein akzeptables Modell erstellt wurde, ist aufgrund der monotonen und nicht sehr anspruchsvollen Arbeit äußerst anstrengend für Data Scientists. Durch diese Übung können zwar im Hinblick auf die Modellwirksamkeit riesige Gewinne erzielt werden, sie ist jedoch manchmal zu zeit- und ressourcenaufwendig und kann dadurch eine negative Rendite (ROI) nach sich ziehen.

Hier kommt automatisiertes maschinelles Lernen (AutoML) ins Spiel. Dabei werden die Konzepte aus dem Forschungsergebnis zur probabilistischen Matrixfaktorisierung genutzt und eine automatisierte Pipeline implementiert, mit der intelligent ausgewählte Algorithmen und Hyperparametereinstellungen basierend auf der Heuristik der vorgelegten Daten und unter Berücksichtigung des jeweiligen Problems oder Szenarios ausprobiert werden. Das Ergebnis dieser Pipeline ist ein Satz von Modellen, die für das jeweilige Problem und Dataset am besten geeignet sind.

Weitere Informationen zu AutoML finden Sie unter [AutoML und MLOps mit Azure Machine Learning](https://azure.microsoft.com/blog/automated-machine-learning-and-mlops-with-azure-machine-learning/).

## <a name="responsible-ml"></a>Verantwortungsvolles maschinelles Lernen

Während der gesamten Entwicklung und Nutzung von KI-Systemen muss Vertrauen im Mittelpunkt stehen. Vertrauen in die Plattform, den Prozess und die Modelle. Da KI und autonome Systeme immer stärker in unsere Gesellschaft integriert werden, ist es wichtig, proaktiv Maßnahmen zu ergreifen, um den unbeabsichtigten Folgen dieser Technologien vorzugreifen und sie zu beheben.

- Verstehen Sie Ihre Modelle, und bauen Sie auf Fairness: Erläutern Sie das Modellverhalten, und legen Sie Features frei, die die größten Auswirkungen auf Vorhersagen haben. Verwenden Sie die integrierten Erläuterungen für transparente und intransparente Modelle beim Modelltraining und dem Ziehen von Rückschlüssen. Verwenden Sie interaktive Visualisierungen zum Vergleichen von Modellen, und führen Sie Was-wäre-wenn-Analysen durch, um die Modellgenauigkeit zu verbessern. Testen Sie Ihre Modelle mit hochmodernen Algorithmen auf Fairness. Verringern Sie Unfairness im gesamten Lebenszyklus des maschinellen Lernens, vergleichen Sie die angepassten Modelle, und gehen Sie bewusst Kompromisse zwischen Fairness und Genauigkeit ein.
- Schützen Sie die Privatsphäre und Vertraulichkeit: Erstellen Sie Modelle, die dies mit den neuesten Innovationen im differenziellen Datenschutz gewährleisten, bei dem in Daten genau abgestimmtes statistisches Datenrauschen eingefügt wird, um die Offenlegung vertraulicher Informationen einzuschränken. Erkennen Sie Datenverluste, und begrenzen Sie auf intelligente Weise wiederholte Abfragen, um das Risiko der Offenlegung gering zu halten. Verwenden Sie Verschlüsselung und Techniken für vertrauliches maschinelles Lernen (demnächst verfügbar), die speziell entwickelt wurden, um Modelle mit vertraulichen Daten mithilfe von maschinellem Lernen sicher zu erstellen.
- Steuern Sie jeden Schritt des maschinellen Lernens: Greifen Sie auf integrierte Funktionen zu, um automatisch die Herkunft nachverfolgen und einen Audit-Trail für den gesamten Lebenszyklus des maschinellen Lernens zu schaffen. Verschaffen Sie sich durch Nachverfolgung von Datasets, Modellen, Experimenten, Code u. v. m. umfassende Einblicke in das Verfahren des maschinellen Lernens. Verwenden Sie benutzerdefinierte Tags, um Modelldatenblätter zu implementieren, Metadaten für wichtige Modelle zu dokumentieren, die Verantwortlichkeit zu erhöhen und einen verantwortungsbewussten Ablauf zu gewährleisten.

Erfahren Sie mehr über die Implementierung von [verantwortlichem ML](https://docs.microsoft.com/azure/machine-learning/concept-responsible-ml).

## <a name="integration-with-other-services"></a>Integration in andere Dienste

Azure Machine Learning funktioniert mit anderen Diensten der Azure-Plattform und lässt sich auch in Open-Source-Tools wie Git und MLFlow integrieren.

- Computeziele wie Azure Kubernetes Service, Azure Container Instances, Azure Databricks, Azure Data Lake Analytics und Azure HDInsight. Weitere Informationen zu Computezielen finden Sie unter [Was sind Computeziele in Azure Machine Learning?](https://docs.microsoft.com/azure/machine-learning/concept-compute-target).
- Azure Event Grid: Weitere Informationen finden Sie unter [Nutzen von Azure Machine Learning-Ereignissen (Vorschauversion)](https://docs.microsoft.com/azure/machine-learning/how-to-use-event-grid).
- Azure Monitor. Weitere Informationen finden Sie unter [Überwachen von Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/monitor-azure-machine-learning).
- Datenspeicher wie Azure Storage-Konten, Azure Data Lake Storage, Azure SQL-Datenbank, Azure Database for PostgreSQL und Azure Open Datasets. Weitere Informationen finden Sie unter [Zugreifen auf Daten in Azure Storage-Diensten](https://docs.microsoft.com/azure/machine-learning/how-to-access-data) und [Erstellen von Datasets mit Azure Open Datasets](https://docs.microsoft.com/azure/machine-learning/how-to-create-register-datasets#create-datasets-with-azure-open-datasets).
- Azure Virtual Network. Weitere Informationen finden Sie unter [Sichern von Azure ML-Experiment- und Rückschlussaufträgen in einem virtuellen Azure-Netzwerk](https://docs.microsoft.com/azure/machine-learning/how-to-enable-virtual-network).
- Azure Pipelines. Weitere Informationen finden Sie unter [Trainieren und Bereitstellen von Machine Learning-Modellen](https://docs.microsoft.com/azure/devops/pipelines/targets/azure-machine-learning?view=azure-devops&tabs=yaml).
- Git-Repositoryprotokolle. Weitere Informationen finden Sie unter [Git-Integration für Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/concept-train-model-git-integration).
- MLflow. Weitere Informationen finden Sie unter [Nachverfolgen von Modellmetriken und Bereitstellen von ML-Modellen mit MLflow und Azure Machine Learning (Vorschauversion)](https://docs.microsoft.com/azure/machine-learning/how-to-use-mlflow).
- Kubeflow. Weitere Informationen finden Sie unter [Erstellen von End-to-End-Workflowpipelines](https://www.kubeflow.org/docs/azure/).
- Sichere Kommunikation. Das Azure Storage-Konto, die Computeziele und andere Ressourcen können innerhalb eines virtuellen Netzwerks gefahrlos zum Trainieren von Modellen sowie für Rückschlüsse verwendet werden. Weitere Informationen finden Sie unter [Sichern von Azure ML-Experiment- und Rückschlussaufträgen in einem virtuellen Azure-Netzwerk](https://docs.microsoft.com/azure/machine-learning/how-to-enable-virtual-network).

## <a name="next-steps"></a>Nächste Schritte

- Lesen Sie Whitepapers und E-Books zu maschinellem Lernen für [Machine Learning Studio](https://azure.microsoft.com/resources/whitepapers/search/?service=machine-learning-studio) und [Machine Learning-Dienste](https://azure.microsoft.com/resources/whitepapers/search/?service=machine-learning-service).
- Machen Sie sich mit [KI-Architekturen und Architekturen für maschinelles Lernen](https://docs.microsoft.com/azure/architecture/browse/) vertraut.
