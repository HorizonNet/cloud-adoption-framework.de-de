---
title: 'Cloudinnovation: Demokratisieren von Daten'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einführung in die Cloudinnovation – Demokratisieren von Daten
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c0ef1165fc416814e0563ec29c4ad5901a83b032
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683271"
---
# <a name="democratize-data"></a>Demokratisieren von Daten

Kohle, Öl und menschliches Potenzial waren in der industriellen Revolution die drei entscheidenden Ressourcen. Diese Ressourcen bildeten das Fundament für Unternehmen und bewirkten schließlich einen grundsätzlichen Wandel von Märkten und Nationen. In der digitalen Wirtschaft gibt es drei gleichermaßen wichtige Ressourcen: Daten, Geräte und menschliches Potenzial. Jede dieser Ressourcen bietet ein hervorragendes Innovationspotenzial. Bei jeder Innovationsinitiative sind die Daten das neue Öl.

Jedes Unternehmen verfügt heute über zahlreiche Daten, die genutzt werden könnten, um die Kundenanforderungen schneller zu erkennen und zu erfüllen. Leider war der Prozess des Minings dieser Daten, um Innovationen voranzutreiben, lange kostspielig und zeitaufwändig. Viele der nützlichsten Lösungen für Kundenanforderungen werden nicht genutzt, da die entscheidenden Personen nicht auf die benötigten Daten zugreifen können.

Die Demokratisierung von Daten ist der Prozess, diese Daten in die richtigen Hände zu legen, um Innovationen voranzutreiben. Dieser Prozess kann verschiedene Formen annehmen, umfasst jedoch im allgemeinen Lösungen für erfasste oder integrierte Rohdaten, die Zentralisierung der Daten, die Freigabe der Daten und das Schützen der Daten. Bei erfolgreicher Ausführung können Experten im Unternehmen die Daten nutzen, um Hypothesen zu testen. In vielen Fällen können Cloudeinführungsteams mit ausschließlicher Verwendung von Daten [Lösungen mit Blick auf die Kundenanforderungen erstellen](./build.md), die sich schnell auf bestehende Kundenanforderungen auswirken.

## <a name="process-of-democratizing-data"></a>Prozess der Demokratisierung von Daten

In den folgenden Phasen werden die Entscheidungen und Ansätze erläutert, die erforderlich sind, um eine Lösung einzuführen, die Daten demokratisiert. Möglicherweise ist nicht jede der Phasen erforderlich, um eine bestimmte Lösung zu erstellen. Jede sollte jedoch beim Erstellen einer Lösung für eine Kundenhypothese ausgewertet werden. Jede stellt einen einzigartigen Ansatz für das Erstellen innovativer Lösungen dar.

![Prozess zur Demokratisierung von Daten](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Freigeben von Daten

Beim [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) hat die Konzentration aller Prozesse auf eine Kundenanforderung Vorrang vor der Konzentration auf eine technische Lösung. Da das Demokratisieren von Daten hier keine Ausnahme bildet, beginnen wir mit der Freigabe von Daten. Um Daten zu demokratisieren, muss eine Lösung zur Freigabe von Daten für einen Datenconsumer enthalten sein. Der Datenconsumer könnte ein direkter Kunde oder ein Stellvertreter sein, der Entscheidungen für Kunden trifft. Zugelassene Datenconsumer haben die Möglichkeit, zentralisierte Daten ohne Unterstützung durch IT-Personal zu analysieren, abzufragen und zu berichten.

Viele erfolgreiche Innovationen wurden als MVPs (Minimum Viable Product, Produkt mit Mindestrentabilität) gestartet, die manuelle, datengesteuerte Prozesse im Auftrag des Kunden bereitstellen. In diesem Concierge-Modell ist ein Mitarbeiter der Datenconsumer. Dieser Mitarbeiter verwendet Daten, um den Kunden zu unterstützen. Jedes Mal, wenn der Kunde die manuelle Unterstützung einbindet, kann eine Hypothese getestet und überprüft werden. Dieser Ansatz ist oft ein kostengünstiges Mittel, eine kundenorientierte Hypothese vor hohen Investitionen in integrierte Lösungen zu testen.

Mit den wichtigsten Tools für die direkte Freigabe von Daten für Datenconsumer wie [Power BI](https://docs.microsoft.com/power-bi) werden u. a. Self-Service-Berichte erstellt oder Daten verarbeitet, die in andere Umgebungen eingebettet sind.

> [!NOTE]
> Vor der Freigabe von Daten müssen Sie die folgenden Abschnitte beachten. Die Freigabe von Daten erfordert möglicherweise die Governance, den Schutz für die freigegebenen Daten zu gewährleisten. Außerdem sind die Daten möglicherweise über mehrere Clouds verteilt, sodass sie zentralisiert werden müssten. Ein Großteil der Daten kann sich sogar innerhalb von Anwendungen befinden, sodass vor der Datenfreigabe eine Erfassung notwendig ist.

### <a name="govern-data"></a>Steuern von Daten

Aus dem Freigeben von Daten kann schnell ein MVP resultieren, das im Dialog mit dem Kunden verwendet werden kann. Daten allein sind jedoch nicht mehr als Daten. Um diese freigegebenen Daten in umsetzbare Informationen umzuwandeln, ist häufig etwas mehr erforderlich. Nachdem eine Hypothese durch die Datenfreigabe überprüft wurde, ist die nächste Entwicklungsphase häufig die Data Governance.

Data Governance ist ein umfassendes Thema, das ein eigenes dediziertes Framework erfordern könnte. Dies liegt nicht im Umfang des [Frameworks für die Cloudeinführung](../../index.md). Einige Aspekte der Datenkontrolle sollten jedoch berücksichtigt werden, sobald die Kundenhypothese überprüft wird. Im Folgenden finden Sie einige Beispiele dieser Fragen:

- **Sind die freigegebenen Daten vertraulich?** Vor jeder öffentlichen Freigabe [sollten Daten klassifiziert werden](../../govern/policy-compliance/data-classification.md), um die Interessen der Kunden und des Unternehmens zu schützen.
- **Wenn die Daten vertraulich sind, wurden sie geschützt?** Der Schutz vertraulicher Daten sollte eine Anforderung für alle demokratisierten Daten sein. Die auf das [Schützen von Datenlösungen](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions.md) konzentrierte Beispielworkload bietet einige Verweise zum Schützen von Daten.
- **Sind die Daten katalogisiert?** Das Erfassen von Details zu den freigegebenen Daten unterstützt die langfristige Datenverwaltung. Tools zum Dokumentieren von Daten wie Azure Data Catalog können diesen Prozess in der Cloud erheblich vereinfachen. Anleitungen zum [Kommentieren von Daten](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) und zum [Dokumentieren von Datenquellen](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) können den Prozess beschleunigen.

Wenn die Demokratisierung von Daten für eine kundenorientierte Hypothese wichtig ist, sollte die Governance von freigegebenen Daten im Freigabeplan enthalten sein, um Kunden, Datenconsumer und das Unternehmen zu schützen.

### <a name="centralize-data"></a>Zentralisieren von Daten

Wenn die Daten in einer IT-Umgebung lückenhaft sind, können die Innovationsmöglichkeiten äußerst eingeschränkt, teuer und zeitaufwändig sein. Die Cloud bietet neue Möglichkeiten, Datensilos übergreifend Daten zu zentralisieren. Wenn eine Zentralisierung mehrerer Datenquellen zum [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) erforderlich ist, kann die Cloud das Testen von Hypothesen beschleunigen.

> [!CAUTION]
> Die Zentralisierung von Daten ist in jedem Innovationsprozess üblicherweise ein riskanter Punkt. Wenn die Datenzentralisierung jedoch statt einer Kundenwertquelle eine [technische Spitze](./build.md#reduce-complexity-and-delay-technical-spikes) ist, sollte die Zentralisierung aufgeschoben werden, bis die Kundenhypothese überprüft wurde.

Wenn die Zentralisierung der Daten erforderlich ist, besteht der erste Schritt darin, den entsprechenden Datenspeicher für die zentralisierten Daten zu definieren. Es ist ratsam, ein Data Warehouse in der Cloud einzurichten. Diese skalierbare Option bietet einen zentralen Speicherort für alle Daten. Diese Art von Lösung ist in den Optionen „Analytische Onlineverarbeitung“ (Online Analytical Processing, OLAP) oder „Big Data“ verfügbar.

Die Referenzarchitekturen für [OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing)- und [Big Data](https://docs.microsoft.com/azure/architecture/data-guide/big-data)-Lösungen können bei der Auswahl der relevantesten Lösung in Azure helfen. Wenn eine Hybridlösung erforderlich ist, kann die Referenzarchitektur für das [Erweitern lokaler Datenlösungen auf die Cloud](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) auch zur Beschleunigung der Lösungsentwicklung beitragen.

> [!IMPORTANT]
> Je nach Kundenanforderung und Lösungsausrichtung ist möglicherweise eine einfachere Lösung ausreichend. Der Cloudarchitekt sollte das Team auffordern, kostengünstigere Lösungen zu berücksichtigen, die insbesondere während der frühen Phase der Entwicklung zu einer schnelleren Validierung der Kundenhypothese führen könnten. Im folgenden Abschnitt zum Sammeln von Daten werden einige Szenarien erläutert, die möglicherweise eine andere Lösung erfordern.

### <a name="collect-data"></a>Sammeln von Daten

Wenn Daten zentralisiert werden müssen, um einer Kundenanforderung gerecht zu werden, müssen die Daten sehr wahrscheinlich auch aus verschiedenen Quellen gesammelt und in den zentralisierten Datenspeicher verschoben werden. Es gibt zwei primäre Formen der Datensammlung: Integration und Erfassung. Jede Methode bietet eine andere Möglichkeit zum Sammeln von Daten.

**Integrieren:** Vorhandene Daten, die sich in einem vorhandenen Datenspeicher befinden, können mithilfe herkömmlicher Datenverschiebungstechniken in den zentralisierten Datenspeicher integriert werden. Dies gilt insbesondere für Szenarien, in denen die Multicloud-Datenspeicherung eine Rolle spielt. Mit diesen Techniken werden die Daten aus dem vorhandenen Datenspeicher extrahiert. Anschließend werden die Daten in den zentralen Datenspeicher geladen. An einem bestimmten Punkt in diesem Prozess werden die Daten oft transformiert, sodass sie im zentralen Speicher besser verwendbar und relevant sind.

Mit cloudbasierten Tools stehen diese Techniken in Form von Tools mit nutzungsabhängiger Bezahlung zur Verfügung und senken so die Hemmschwelle für den Einstieg in Datensammlung und -zentralisierung. Tools wie Datenmigrationsdienst und Data Factory sind zwei gängige Beispiele in Azure. Die Referenzarchitektur für [Data Factory mit einem OLAP-Datenspeicher](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) bietet ein Beispiel einer solchen Lösung.

**Erfassen:** Einige Daten befinden sich nicht in einem vorhandenen Datenspeicher. Wenn diese temporären Daten eine primäre Quelle für Innovation sind, sollten alternative Ansätze berücksichtigt werden. Temporäre Daten finden Sie in einer Vielzahl von vorhandenen Quellen, z. B. Anwendungen, APIs, Datenströme, IoT-Geräte, Blockchain, Anwendungscache, Medieninhalt oder sogar Flatfiles.

Diese unterschiedlichen Datenformen könnten im Rahmen einer OLAP- oder Big Data-Lösung in einen zentralen Datenspeicher integriert werden. Für frühe Iterationen von Erstellen-Messen-Lernen-Zyklen ist eine OLTP-Lösung (Online Transactional Processing) jedoch möglicherweise mehr als ausreichend, um eine Kundenhypothese zu validieren. OLTP-Lösungen sind nicht die qualitativ hochwertigste Lösung für ein Berichterstellungsszenario. Beim [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) hat die Konzentration auf die Kundenanforderungen Vorrang vor technischen Entscheidungen über Tools. Nachdem die Kundenhypothese bedarfsabhängig überprüft wurde, ist möglicherweise eine geeignetere Plattform erforderlich. Die Referenzarchitektur für [OLTP-Datenspeicher](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) kann bei der Ermittlung des für Ihre Lösung am besten geeigneten Datenspeichers helfen.

**Virtualisieren:** Die Integration und Erfassung von Daten kann manchmal die Innovation bremsen. Wenn bereits eine Lösung für die Datenvirtualisierung verfügbar ist, ist dies möglicherweise ein relevanterer Ansatz. Erfassung und Integration können Speicher-/Entwicklungsanforderungen duplizieren, die Datenlatenz steigern, die Angriffsfläche vergrößern, Qualitätsprobleme verursachen und den Governanceaufwand erhöhen. Die Datenvirtualisierung ist eine modernere Alternative, bei der die ursprünglichen Daten an einem einzigen Ort gespeichert werden und Pass-Through- oder zwischengespeicherte Abfragen der Quelldaten erstellt werden.

SQL Server 2017 und Azure SQL Data Warehouse unterstützen [PolyBase](/sql/relational-databases/polybase/polybase-guide). Dies ist der in Azure am häufigsten verwendete Ansatz zur Datenvirtualisierung.

## <a name="next-steps"></a>Nächste Schritte

Wenn die Strategie zur Demokratisierung der Daten feststeht, werden im nächsten Schritt Ansätze zum [Einbinden von Kunden durch Apps](./apps.md) evaluiert.

> [!div class="nextstepaction"]
> [Einbinden von Kunden durch Apps](./apps.md)
