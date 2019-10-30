---
title: 'Cloudinnovation: Vorhersagen und Beeinflussen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Einführung in die Cloudinnovation: Vorhersagen und Beeinflussen'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: e6187bc926aacd9a09e67b8cd2bfe94e5a4a42dd
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682624"
---
# <a name="predict-and-influence"></a>Vorhersagen und Beeinflussen

Es gibt in der digitalen Wirtschaft zwei Klassen von Anwendungen: historisch und prädiktiv. Viele Kundenbedürfnisse können nur mithilfe historischer Daten erfüllt werden, einschließlich Daten in nahezu Echtzeit. Die meisten Lösungen konzentrieren sich derzeit in erster Linie auf die Aggregation von Daten. Diese Daten werden verarbeitet und an den Kunden in Form einer digitalen oder Umgebungserfahrung zurückgegeben.

Da die prädiktive Modellierung immer wirtschaftlicher und leichter verfügbar wird, verlangen Kunden nach zukunftsweisenden Erfahrungen, die zu besseren Entscheidungen und Maßnahmen führen. Diese Nachfrage muss jedoch nicht zwangsläufig zu einer prädiktiven Lösung führen. In den meisten Szenarien kann eine historische Sicht genügend Daten liefern, um den Kunden in die Lage zu versetzen, selbst eine Entscheidung zu treffen.

Leider haben Kunden eine kurzsichtige Sichtweise, die zu Entscheidungen führt, die auf ihrer unmittelbaren Umgebung und ihrem Einflussbereich basieren. Da Optionen und Entscheidungen in Bezug auf Anzahl und Tragweite zunehmen, führt diese Kurzsichtigkeit möglicherweise dazu, dass die Bedürfnisse des Kunden nicht erfüllt werden. Gleichzeitig, da eine Hypothese maßstäblich bestätigt ist, kann das Unternehmen, das die Lösung anbietet, Tausende oder Millionen von Kundenentscheidungen nachvollziehen. Es ist möglich, Muster und deren Auswirkungen zu erkennen. Die Fähigkeit zur Vorhersage ist eine kluge Investition, wenn ein Verständnis dieser Muster erforderlich ist, um Entscheidungen zu treffen, die Kundenbedürfnissen entsprechen.

## <a name="examples-of-predictions-and-influence"></a>Beispiele für Vorhersagen und Einfluss

Die Nutzung von Daten für Vorhersagen kann in verschiedenen Anwendungen und Umgebungserfahrungen beobachtet werden.

- **E-Commerce:** Vorgeschlagene Artikel sind ein Beispiel einer Vorhersage. Basierend auf dem, was andere bereits gekauft haben, kann die Website Produkte vorschlagen, die sich der Kunde ggf. in seinen Warenkorb legen sollte.
- **Angepasste Realität:** Mit IoT sind ausgefeiltere Beispiele möglich. Ein Gerät an einer Montagelinie erkennt einen Anstieg der Temperatur einer Maschine. Ein cloudbasiertes prädiktives Modell bestimmt, wie reagiert werden soll. Gestützt auf diese Vorhersage wird ein anderes Gerät angewiesen, die Montagelinie zu verlangsamen, damit die Maschine abkühlen kann.
- **Konsumgüter:** Mobiltelefone, intelligente Häuser und sogar Ihr Auto enthalten alle ein gewisses Maß an prädiktiven Fähigkeiten, indem Aktivitäten vorgeschlagen werden, die auf Faktoren wie Standort oder Tageszeit basieren. Wenn die Vorhersage und die Ausgangshypothese in Einklang gebracht werden, beeinflussen diese Vorhersagen Ihr Verhalten. Wenn beide sehr ausgereift sind, führt die Vorhersage zum Handeln, wie zum Beispiel bei einem selbstfahrenden Auto.

## <a name="developing-predictive-capabilities"></a>Entwickeln prädiktiver Fähigkeiten

Lösungen, die durchgängig genaue prädiktive Fähigkeiten bieten, weisen in der Regel fünf Kernmerkmale auf: Daten, Erkenntnisse, Muster, Vorhersagen und Interaktionen. Alle sind erforderlich, um prädiktive Fähigkeiten zu entwickeln. Wie alle großen Innovationen erfordert die Entwicklung prädiktiver Fähigkeiten eine [Verpflichtung zur Iteration](./index.md#commitment-to-iteration). Bei jeder Iteration reifen ein oder mehrere der folgenden Merkmale, um immer komplexere Kundenhypothesen für gültig zu erklären.

![Schritte beim Entwickeln prädiktiver Fähigkeiten](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Wenn die Kundenhypothese, die anhand des Artikels [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) entwickelt wurde, prädiktive Fähigkeiten umfasst, ist dieser Artikel möglicherweise von Interesse. Doch prädiktive Fähigkeiten setzen einen erheblichen Aufwand an Zeit und Energie voraus. Wenn prädiktive Fähigkeiten jedoch statt eines Ausgangspunkts eines erreichbaren Nutzens für den Kunden eine [technische Herausforderung](./build.md#reduce-complexity-and-delay-technical-spikes) darstellen, sollten sie aufgeschoben werden, bis die Kundenhypothese nach Maß auf Gültigkeit geprüft wurde.

## <a name="data"></a>Data

Das einfachste der zuvor genannten Merkmale sind Daten. Jede der vorherigen Fachrichtungen für die Entwicklung digitaler Erfindungen erzeugt Daten. Diese Daten können alle zur Entwicklung von Vorhersagen beitragen. Weitere Informationen zu Möglichkeiten, Daten in eine prädiktive Lösung einzubringen, finden Sie in den Artikeln zur [Demokratisierung von Daten](./data.md) oder [Interaktion mit Geräten](./devices.md).

Zur Bereitstellung prädiktiver Fähigkeiten können eine Reihe von Datenquellen genutzt werden:

## <a name="insights"></a>Einblicke

Fachleute nutzen Daten zu den Bedürfnissen und Verhaltensweisen von Kunden, um grundlegende geschäftliche Erkenntnisse aus einer Analyse der Rohdaten zu gewinnen. Diese Erkenntnisse können das Vorkommen des gewünschten Kundenverhaltens (oder alternativ unerwünschte Ergebnisse) aufdecken. Im Verlauf von Iterationen der Vorhersagen können diese Erkenntnisse helfen, potenzielle Korrelationen aufzuzeigen, die eine kausale Wirkung auf positive Ergebnisse haben könnten. Eine Anleitung, wie Experten Erkenntnisse erlangen können, finden Sie im Artikel zur [Demokratisierung von Daten](./data.md).

## <a name="patterns"></a>Muster

Der Mensch hat naturgemäß Schwierigkeiten mit der Erkennung von Mustern in großen Datenmengen. Zu diesem Zweck wurden Computer entwickelt. Maschinelles Lernen beschleunigt diese Aufgabe durch Erkennen von Mustern in einer großen Datenmenge, was als Machine Learning-Modell bezeichnet wird. Diese Muster werden dann mithilfe von Algorithmen für maschinelles Lernen eingesetzt, um vorherzusagen, was passiert, wenn ein neuer Satz von Datenpunkten in die Algorithmen eingefügt wird.

Ausgehend von Erkenntnissen werden beim maschinellen Lernen prädiktive Modelle trainiert und auf die Daten angewendet, um die Muster in den Daten bestmöglich auszunutzen. Durch mehrere Iterationen von Training, Tests und Anpassung können diese Modelle und Algorithmen künftige Ergebnisse genau vorhersagen.

[Azure Machine Learning Service](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) ist das cloudbasierte Tool in Azure zum Entwickeln und Trainieren von Modellen, die auf Ihren Daten basieren. Dieses Tool bietet auch einen [Workflow zur Beschleunigung der Entwicklung von Algorithmen für maschinelles Lernen](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Mit diesem Workflow können Algorithmen auf einer grafischen Oberfläche oder in Python entwickelt werden.

Für leistungsfähigere Machine Learning-Modelle bieten [ML-Dienste in Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) eine Plattform für maschinelles Lernen, die auf Apache Hadoop-Clustern basiert. Dieser Ansatz ermöglicht eine präzisere Steuerung der zugrunde liegenden Cluster, Speicher und Computeknoten. Die Nutzung von Azure HDInsight ermöglicht auch eine noch umfassendere Integration durch Tools wie ScaleR und SparkR, um Vorhersagen auf der Grundlage integrierter und erfasster Daten zu erstellen und sogar mit Daten aus einem Stream zu arbeiten. Die [Lösung zur Vorhersage von Flugverspätungen](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) demonstriert jede dieser erweiterten Möglichkeiten, Verspätungen von Flügen basierend auf Wetterverhältnissen vorherzusagen. Die HDInsight-Lösung bietet Unternehmen auch Steuerungsmechanismen für Datensicherheit, Netzwerkzugriff und Leistungsüberwachung, um Muster zu operationalisieren.

## <a name="predictions"></a>Vorhersagen

Sobald ein Muster gebildet und trainiert wurde, kann es mithilfe von APIs angewendet werden, die Vorhersagen während der Bereitstellung einer digitalen Erfahrung treffen können. Die meisten dieser APIs basieren auf einem sorgfältig trainierten Modell, das auf einem Muster in Ihren Daten basiert. Da jedoch immer mehr Kunden gängige Workloads in der Cloud bereitstellen, sind Cloudanbieter in der Lage, allgemeine Vorhersage-APIs bereitzustellen, um eine schnellere Akzeptanz von Vorhersagen zu ermöglichen.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) ist ein Beispiel einer prädiktive API, die von einem Cloudanbieter entwickelt wurde. Dieser Dienst umfasst prädiktive APIs zur Inhaltsmoderation, Anomalieerkennung oder Vorschläge zur Personalisierung von Inhalten. Diese APIs sind sofort einsatzbereit und basieren auf gängigen Inhaltsmustern, mit denen Microsoft Modelle trainiert hat. Jede dieser APIs trifft Vorhersagen auf Grundlage von Daten, die Sie in die API einpflegen.

[Azure Machine Learning Service](https://docs.microsoft.com/azure/machine-learning) ermöglicht die Bereitstellung maßgeschneiderter Algorithmen, die Sie ausschließlich auf Grundlage Ihrer eigenen Daten erstellen und trainieren können. [Hier](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where) erfahren Sie mehr über die Bereitstellung von Vorhersagen mit Azure Machine Learning.

Im Artikel zum [Einrichten von HDInsight-Clustern](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) werden die Prozesse zur Bereitstellung von Vorhersagen erörtert, die für ML Services in Azure HDInsight entwickelt wurden.

## <a name="interactions"></a>Interaktionen

Sobald eine Vorhersage über eine API zur Verfügung gestellt wird, kann sie genutzt werden, um das Kundenverhalten zu beeinflussen. Dieser Einfluss erfolgt in Form von Interaktionen. Eine Interaktion mit einem Algorithmus für maschinelles Lernen findet innerhalb Ihrer anderen digitalen oder Umgebungserfahrungen statt. Die über die Anwendung oder Erfahrung gesammelten Daten durchlaufen die Algorithmen für maschinelles Lernen. Wenn der Algorithmus ein Ergebnis voraussagt, kann diese Vorhersage über die vorhandene Erfahrung an den Kunden zurückgegeben werden.

Erfahren Sie mehr über die Interaktionen innerhalb einer [Lösung mit angepasster Realität](./devices.md#adjusted-reality), um weitere Details zum Erstellen einer Interaktion innerhalb einer Umgebungserfahrung zu erhalten.

## <a name="next-steps"></a>Nächste Schritte

Basierend auf dem Wissen, das in Bezug auf die [Fachrichtungen von Innovation](./invention.md) innerhalb der [Methodik für Innovation](./index.md) erworben wurde, ist Ihnen bekannt, dass Sie über die technischen Instrumente verfügen, die erforderlich sind, um [Lösungen mit Blick auf die Kundenanforderungen](./build.md) zu entwickeln.

> [!div class="nextstepaction"]
> [Entwickeln von Lösungen mit Blick auf die Kundenanforderungen](./build.md)
