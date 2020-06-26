---
title: Vorhersagen und Beeinflussen des Kundenverhaltens
description: Verwenden Sie die Vorhersagemodellierung, um Vorhersagefunktionen auf der Grundlage von Daten, Erkenntnissen, Mustern, Vorhersagen und Interaktionen zu entwickeln.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: f3b3987c016a5fbf76355a27eec720c5620cdc34
ms.sourcegitcommit: 2794cab8eb925103ae22babc704d89f7f7d4f6f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84993762"
---
# <a name="predict-and-influence"></a>Vorhersagen und Beeinflussen

Es gibt in der digitalen Wirtschaft zwei Klassen von Anwendungen: _historisch_ und _prädiktiv_. Viele Kundenbedürfnisse können nur mithilfe historischer Daten erfüllt werden, einschließlich Daten in nahezu Echtzeit. Die meisten Lösungen konzentrieren sich derzeit in erster Linie auf die Aggregation von Daten. Diese Daten werden verarbeitet und an den Kunden in Form einer digitalen oder Umgebungserfahrung zurückgegeben.

Da die prädiktive Modellierung immer wirtschaftlicher und leichter verfügbar wird, verlangen Kunden nach zukunftsweisenden Erfahrungen, die zu besseren Entscheidungen und Maßnahmen führen. Diese Nachfrage muss jedoch nicht zwangsläufig eine prädiktive Lösung vorschlagen. In den meisten Fällen kann eine historische Sicht genügend Daten liefern, um den Kunden in die Lage zu versetzen, selbst eine Entscheidung zu treffen.

Leider haben Kunden eine kurzsichtige Sichtweise, die zu Entscheidungen führt, die auf ihrer unmittelbaren Umgebung und ihrem Einflussbereich basieren. Da Optionen und Entscheidungen in Bezug auf Anzahl und Tragweite zunehmen, dient diese Kurzsichtigkeit möglicherweise nicht den Bedürfnissen des Kunden. Gleichzeitig, da eine Hypothese maßstäblich bestätigt ist, kann das Unternehmen, das die Lösung anbietet, Tausende oder Millionen von Kundenentscheidungen nachvollziehen. Dieser allgemeine Überblick ermöglicht es, weitreichende Muster und die Auswirkungen dieser Muster zu erkennen. Die Fähigkeit zur Vorhersage ist eine kluge Investition, wenn ein Verständnis dieser Muster erforderlich ist, um Entscheidungen zu treffen, die dem Kunden in bestmöglicher Weise dienen.

## <a name="examples-of-predictions-and-influence"></a>Beispiele für Vorhersagen und Einfluss

Eine Vielzahl von Anwendungen und Umgebungserfahrungen nutzen Daten, um Vorhersagen zu treffen:

- **E-Commerce:** Basierend auf dem, was andere ähnliche Verbraucher gekauft haben, schlägt eine E-Commerce-Website Produkte vor, die sich der Kunde ggf. in seinen Warenkorb legen sollte.
- **Angepasste Realität:** Das Internet der Dinge (IoT) bietet fortgeschrittenere Instanzen der prädiktiven Funktionalität. Ein Gerät an einer Montagelinie erkennt z. B. einen Anstieg der Temperatur einer Maschine. Ein cloudbasiertes prädiktives Modell bestimmt, wie reagiert werden soll. Gestützt auf diese Vorhersage verlangsamt ein anderes Gerät die Montagelinie, damit die Maschine abkühlen kann.
- **Konsumgüter:** Mobiltelefone, intelligente Häuser und sogar Ihr Auto verwenden alle prädiktive Fähigkeiten, um das Benutzerverhalten basierend auf Faktoren wie Standort oder Tageszeit vorzuschlagen. Wenn eine Vorhersage und die Ausgangshypothese ausgerichtet sind, führt die Vorhersage zu Maßnahmen. In einem sehr ausgereiften Stadium kann diese Ausrichtung Produkte wie selbstfahrende Autos zur Realität werden lassen.

## <a name="develop-predictive-capabilities"></a>Entwickeln prädiktiver Fähigkeiten

Lösungen, die durchgängig genaue prädiktive Fähigkeiten bieten, weisen in der Regel fünf Kernmerkmale auf:

    - Daten
    - Einblicke
    - Muster
    - Vorhersagen (Predictions)
    - Interaktionen

Alle Aspekte sind erforderlich, um prädiktive Fähigkeiten zu entwickeln. Wie alle großen Innovationen erfordert die Entwicklung prädiktiver Fähigkeiten eine [Verpflichtung zur Iteration](./index.md#commitment-to-iteration). Bei jeder Iteration reifen ein oder mehrere der folgenden Merkmale, um immer komplexere Kundenhypothesen für gültig zu erklären.

![Schritte beim Entwickeln prädiktiver Fähigkeiten](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Wenn die Kundenhypothese, die unter [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) entwickelt wurde, prädiktive Fähigkeiten umfasst, könnten die dort beschriebenen Prinzipien durchaus gelten. Prädiktive Fähigkeiten setzen jedoch einen erheblichen Aufwand an Zeit und Energie voraus. Wenn prädiktive Fähigkeiten jedoch statt eines Ausgangspunkts eines realen Nutzens für den Kunden eine [technische Herausforderung](./build.md#reduce-complexity-and-delay-technical-spikes) darstellen, sollten sie aufgeschoben werden, bis die bedarfsorientierte Kundenhypothese auf Gültigkeit geprüft wurde.

## <a name="data"></a>Daten

Die Daten sind das grundlegendste der zuvor genannten Merkmale. Jede der Fachrichtungen für die Entwicklung digitaler Erfindungen erzeugt Daten. Diese Daten tragen natürlich zur Entwicklung von Vorhersagen bei. Weitere Informationen zu Möglichkeiten, Daten in eine prädiktive Lösung einzubringen, finden Sie unter [Demokratisierung von Daten](./data.md) und [Interaktion mit Geräten](./devices.md).

Zur Bereitstellung prädiktiver Fähigkeiten können eine Reihe von Datenquellen genutzt werden:

## <a name="insights"></a>Einblicke

Fachleute nutzen Daten zu den Bedürfnissen und Verhaltensweisen von Kunden, um grundlegende geschäftliche Erkenntnisse aus einer Analyse von Rohdaten zu gewinnen. Diese Erkenntnisse können das Vorkommen des gewünschten Kundenverhaltens (oder alternativ unerwünschte Ergebnisse) aufdecken. Im Verlauf von Iterationen der Vorhersagen können diese Erkenntnisse helfen, potenzielle Korrelationen aufzuzeigen, die letztlich zu positiven Ergebnissen führen könnten. Eine Anleitung, wie Experten Erkenntnisse erlangen können, finden Sie unter [Demokratisierung von Daten](./data.md).

## <a name="patterns"></a>Muster

Menschen haben immer versucht, Muster in großen Datenmengen zu erkennen. Zu diesem Zweck wurden Computer entwickelt. Das maschinelle Lernen beschleunigt diese Aufgabe, indem es genau solche Muster erkennt, eine Qualifikation, die das Machine Learning-Modell enthält. Diese Muster werden dann mithilfe von Algorithmen für maschinelles Lernen eingesetzt, um Ergebnisse vorherzusagen, wenn ein neuer Satz von Daten in die Algorithmen eingefügt wird.

Ausgehend von Erkenntnissen werden beim maschinellen Lernen prädiktive Modelle entwickelt und angewendet, um die Muster in Daten bestmöglich auszunutzen. Durch mehrere Iterationen von Training, Tests und Anpassung können diese Modelle und Algorithmen künftige Ergebnisse genau vorhersagen.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) ist der cloudbasierte Dienst in Azure zum Entwickeln und Trainieren von Modellen, die auf Ihren Daten basieren. Dieses Tool bietet auch einen [Workflow zur Beschleunigung der Entwicklung von Algorithmen für maschinelles Lernen](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Mit diesem Workflow können Algorithmen über eine grafische Oberfläche oder in Python entwickelt werden.

Für leistungsfähigere Machine Learning-Modelle bieten [ML-Dienste in Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) eine Plattform für maschinelles Lernen, die auf Apache Hadoop-Clustern basiert. Dieser Ansatz ermöglicht eine präzisere Steuerung der zugrunde liegenden Cluster, Speicher und Computeknoten. Azure HDInsight bietet auch eine noch umfassendere Integration durch Tools wie ScaleR und SparkR, um Vorhersagen auf der Grundlage integrierter und erfasster Daten zu erstellen und sogar mit Daten aus einem Stream zu arbeiten. Die [Lösung zur Vorhersage von Flugverspätungen](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) demonstriert jede dieser erweiterten Möglichkeiten, wenn sie zur Vorhersage von Flugverspätungen basierend auf Wetterbedingungen verwendet wird. Die HDInsight-Lösung bietet Unternehmen auch Steuerungsmechanismen für Datensicherheit, Netzwerkzugriff und Leistungsüberwachung, um Muster zu operationalisieren.

## <a name="predictions"></a>Vorhersagen (Predictions)

Nachdem ein Muster erstellt und trainiert wurde, können Sie es über APIs anwenden, die Vorhersagen während der Bereitstellung einer digitalen Erfahrung treffen können. Die meisten dieser APIs basieren auf einem sorgfältig trainierten Modell, das auf einem Muster in Ihren Daten basiert. Da immer mehr Kunden tägliche Workloads in der Cloud bereitstellen, führen die von Cloudanbietern verwendeten Vorhersage-APIs zu einer immer schnelleren Akzeptanz.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) ist ein Beispiel einer prädiktive API, die von einem Cloudanbieter entwickelt wurde. Dieser Dienst umfasst prädiktive APIs zur Inhaltsmoderation, Anomalieerkennung und Vorschläge zur Personalisierung von Inhalten. Diese APIs sind sofort einsatzbereit und basieren auf bekannten Inhaltsmustern, mit denen Microsoft Modelle trainiert hat. Jede dieser APIs trifft Vorhersagen auf Grundlage der Daten, die Sie in die API einpflegen.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning) ermöglicht die Bereitstellung maßgeschneiderter Algorithmen, die Sie ausschließlich auf Grundlage Ihrer eigenen Daten erstellen und trainieren können. Erfahren Sie mehr über die Bereitstellung von Vorhersagen mit [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

Unter [Einrichten von HDInsight-Clustern](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) werden die Prozesse zur Bereitstellung von Vorhersagen erörtert, die für ML Services in Azure HDInsight entwickelt wurden.

## <a name="interactions"></a>Interaktionen

Nachdem eine Vorhersage über eine API zur Verfügung gestellt wurde, können Sie damit das Kundenverhalten beeinflussen. Dieser Einfluss erfolgt in Form von Interaktionen. Eine Interaktion mit einem Algorithmus für maschinelles Lernen findet innerhalb Ihrer anderen digitalen oder Umgebungserfahrungen statt. Die über die Anwendung oder Erfahrung gesammelten Daten durchlaufen die Algorithmen für maschinelles Lernen. Wenn der Algorithmus ein Ergebnis voraussagt, kann diese Vorhersage über die vorhandene Erfahrung an den Kunden zurückgegeben werden.

Erfahren Sie mehr darüber, wie Sie mit einer [Lösung mit angepasster Realität](./devices.md#adjusted-reality) eine Umgebungserfahrung schaffen können.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie sich mit den [Erfindungsdisziplinen](./invention.md) und der [innovativen Methodik](./index.md) vertraut gemacht haben, sind Sie jetzt bereit zu erfahren, wie Sie [Lösungen mit Blick auf die Kundenanforderungen entwickeln](./build.md).

> [!div class="nextstepaction"]
> [Entwickeln von Lösungen mit Blick auf die Kundenanforderungen](./build.md)
