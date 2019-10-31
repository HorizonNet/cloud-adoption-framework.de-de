---
title: 'Workloadvorgänge: Cloudverwaltung und -betrieb'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Workloadvorgänge: Cloudverwaltung und -betrieb'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5f250362e93a81c6bb38ef11e8659484ef023182
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683733"
---
# <a name="workload-operations-in-cloud-management"></a>Workloadvorgänge in der Cloudverwaltung

Einige Workloads sind für den Erfolg des Unternehmens wichtig. Für diese Workloads reicht eine Verwaltungsbaseline nicht aus, um die erforderlichen Geschäftsverpflichtungen für die Cloudverwaltung zu erfüllen. Möglicherweise reicht der Plattformbetrieb nicht einmal aus, um Geschäftsverpflichtungen zu erfüllen. Diese äußerst wichtige Teilmenge von Workloads erfordert eine spezielle Konzentration auf die Workloadfunktionen und ihre Unterstützung.

Im Gegenzug kann die Investition in Workloadvorgänge zu einer verbesserten Leistung, geringeren Risiken bei Unterbrechung des Geschäftsbetriebs und einer schnelleren Wiederherstellung führen, wenn Systemfehler auftreten. In diesem Artikel wird erläutert, wie Sie in den fortlaufenden Betrieb dieser Workloads mit hoher Priorität investieren, um bessere Geschäftsverpflichtungen zu erzielen.

## <a name="when-to-invest-in-workload-operations"></a>Wann sollten Sie in Workloadvorgänge investieren?

Nach dem Pareto-Prinzip (auch bekannt als 80/20-Regel) sind 80 % der Wirkungen auf 20 % der Gründe zurückzuführen. Wenn IT-Portfolios im Lauf der Zeit immer mehr organisch wachsen dürfen, ist diese Regel häufig in einer Bewertung des IT-Portfolios zu finden. Abhängig von dem Effekt, der eine Investition erfordert, kann die Ursache variieren, aber das allgemeine Prinzip gilt weiterhin:

- 80 % der Systemfehler sind tendenziell das Ergebnis von 20 % der häufigen Fehler oder Bugs
- 80 % des Geschäftswerts stammen tendenziell von 20 % der Workloads in einem Portfolio
- 80 % des Aufwands für die Migration zur Cloud stammen aus 20 % der zu migrierenden Workloads
- 80 % des Cloudverwaltungsaufwands unterstützen 20 % der Servicevorfälle oder Tickets zur Problembehandlung
- 80 % der geschäftlichen Auswirkungen von Ausfällen ergeben sich aus 20 % der Systeme, die von einem Ausfall betroffen sind

Workloadvorgänge sollten nur bei einem fundierten Verständnis von Cloudeinführungsstrategie, Geschäftsergebnissen und betrieblichen Metriken angewendet werden. Dies ist ein Paradigmenwechsel weg von der klassischen Sichtweise der IT. Herkömmlicherweise setzte die IT voraus, dass alle Workloads in gleichem Maße unterstützt wurden und gleiche Prioritätsstufen erforderten.

Vor der Investition in tiefgreifende Workloadvorgänge sollten sowohl die IT als auch die übrigen Unternehmensangehörigen die geschäftlichen Begründungen und die Erwartungen an eine größere Investition in die Cloudverwaltung verstehen.

## <a name="start-with-the-data"></a>Der Anfang mit den Daten

Workloadvorgänge beginnen mit einem umfassenden Verständnis der Workloadleistung und der Supportanforderungen. Vor der Investition in Workloadvorgänge muss das Team über umfangreiche Daten zu Workloadabhängigkeiten, Anwendungsleistung, Datenbankdiagnose, Telemetriedaten virtueller Computer und Vorfallsverlauf verfügen.

Aus diesen Daten resultieren die Erkenntnisse, die Entscheidungen zu Workloadvorgängen ermöglichen.

## <a name="continued-observation"></a>Fortgesetzte Beobachtung

Ausgangsdaten und fortlaufende Telemetriedaten können dabei helfen, Theorien zur Leistung einer Workload zu formulieren und zu testen. Laufende Workloadvorgänge sind jedoch von einer kontinuierlichen und ausgedehnten Überwachung der Workloadleistung abhängig, wobei der Schwerpunkt auf Anwendungs- und Datenleistung liegt.

### <a name="testing-automation"></a>Testen der Automatisierung

Auf Anwendungsebene ist die erste Anforderung von Workloadvorgängen eine Investition in umfassende Tests. Für alle Anwendungen, die durch Workloadvorgänge unterstützt werden, sollte ein Testplan eingerichtet und regelmäßig ausgeführt werden, um für alle Anwendungen umfassende Funktions- und Skalierungstests durchzuführen.

Reguläre Testtelemetriedaten ermöglichen eine sofortige Überprüfung verschiedener Hypothesen in Bezug auf den Betrieb der Workload. Das Verbessern von Betriebs- und Architekturmustern kann ausgeführt und getestet werden. Das Delta dieser Ergebnisse liefert eine deutliche Auswirkungsanalyse als Grundlage für fortlaufende Investitionen.

### <a name="understand-releases"></a>Verständnis von Releases

Das klare Verständnis von Releasezyklen und Releasepipelines ist ein wichtiges Element von Workloadvorgängen.

Ein Verständnis der Zyklen kann auf potenzielle Unterbrechungen vorbereiten und dem Team ermöglichen, proaktiv alle Releases zu behandeln, die negative Auswirkungen auf Vorgänge haben könnten. Dieses Verständnis ermöglicht dem Cloudverwaltungsteam auch die Partnerschaft mit Einführungsteams, um die Qualität des Produkts kontinuierlich zu verbessern und Fehler zu beheben, die sich auf die Stabilität auswirken könnten.

Noch wichtiger ist, dass das Verständnis der Releasepipelines die RTO einer Workload erheblich verbessern kann. In vielen Szenarios ist der schnellste und präziseste Pfad zur Wiederherstellung einer Anwendung eine Releasepipeline. Bei Anwendungsebenen, die sich nur ändern, wenn ein neues Release herauskommt, kann die höhere Investition in die Pipelineoptimierung sinnvoller sein als die Wiederherstellung der Anwendung mittels herkömmlicher Sicherungsprozesse.

Eine Bereitstellungspipeline kann nicht nur der schnellste Weg zur Wiederherstellung sein, sie kann auch der schnellste Weg zur Bereinigung sein. Wenn eine Anwendung über eine schnelle, effiziente und zuverlässige Releasepipeline verfügt, hat das Cloudverwaltungsteam eine Option, die Bereitstellung auf einem neuen Host als Form einer automatisierten Bereinigung zu automatisieren.

Möglicherweise gibt es noch viele weitere schnellere, effektivere Mechanismen zur Bereinigung und Wiederherstellung. Wenn jedoch die Verwendung einer vorhandenen Pipeline Geschäftsverpflichtungen erfüllen kann und vorhandene DevOps-Investitionen sich so auszahlen, kann es sich um eine sinnvolle Alternative handeln.

### <a name="clearly-communicate-changes-to-the-workload"></a>Klares Kommunizieren von Änderungen der Workload

Änderungen an Workloads zählen zu den größten Risiken für Workloadvorgänge. Für alle Workloads auf Workloadvorgangsebene der Cloudverwaltung sollte das Cloudverwaltungsteam eng mit den Cloudeinführungsteams zusammenarbeiten, um die mit den einzelnen Releases verbundenen Änderungen zu verstehen. Diese Investition in das proaktive Verständnis hat eine direkte Auswirkung auf die Betriebsstabilität.

## <a name="improve-outcomes"></a>Verbessern von Ergebnissen

Laufende Vorgänge werden in der Regel auf eine von zwei Arten verbessert. Aus den Daten- und Kommunikationsinvestitionen in eine Workload resultieren Verbesserungsvorschläge, bei denen zwei Pfade zur Auswahl stehen: Automatisierte Bereinigung oder verbessertes Systemdesign

### <a name="technical-debt-resolution"></a>Auflösung technischer Schulden

Die besten Pläne für Workloadvorgänge erfordern weiterhin eine Bereinigung. Da das Cloudverwaltungsteam in Verbindung bleiben möchte, um Maßnahmen und Releases zur Einführung zu verstehen, sollte das Team ebenso regelmäßig Bereinigungsanforderungen teilen, um sicherzustellen, dass technische Schulden und Fehler für Entwicklungsteams weiterhin Priorität haben.

### <a name="automate-remediation"></a>Automatisieren der Bereinigung

Bei Anwendung des Pareto-Prinzips resultieren 80 % negativer Geschäftsauswirkungen wahrscheinlich aus 20 % der Servicevorfälle. Wenn diese Vorfälle nicht in normalen Entwicklungszyklen behandelt werden können, können Investitionen in die Automatisierung der Bereinigung die Geschäftsunterbrechungen erheblich verringern.

### <a name="improved-system-design"></a>Verbessertes Systemdesign

In beiden Fällen (Auflösung technischer Schulden oder automatisierte Bereinigung) sind Systemfehler die häufigste Ursache für die meisten Systemausfälle. Die Einhaltung einiger Entwurfsprinzipien kann die größten Auswirkungen auf die gesamten Workloadvorgänge haben.

1. Skalierbarkeit: Die Fähigkeit eines Systems, eine höhere Last zu verarbeiten.
2. Verfügbarkeit: Der Zeitanteil, in dem ein System funktioniert und erreichbar ist.
3. Resilienz: Die Fähigkeit eines Systems, nach Ausfällen eine Wiederherstellung durchzuführen und die Betriebsbereitschaft sicherzustellen.
4. Verwaltung: Operative Prozesse, die für die Ausführung eines Systems in der Produktion sorgen.
5. Sicherheit: Schützen von Anwendungen und Daten vor Bedrohungen.

Das [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) bietet einen Ansatz zur Bewertung spezifischer Workloads hinsichtlich der Einhaltung dieser Vorgaben, um so den Gesamtbetrieb zu verbessern. Diese Eckpfeiler können sowohl für den Plattform- als auch den Workloadbetrieb gelten.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie die Verwaltungsmethodik innerhalb des Cloud Adoption Frameworks vollständig verstanden haben, sind Sie bestens gerüstet, die Cloudverwaltungsprinzipien zu implementieren. Eine Anleitung zur Umsetzung dieser Methodik in Ihrer Betriebsumgebung finden Sie auf der [Landing Page für die Verwaltungsphase](../index.md) des Einführungslebenszyklus.

> [!div class="nextstepaction"]
> [Anwenden dieser Methodik](../index.md)
