---
title: 'Cloudinnovation: Demokratisieren von Daten'
description: Einführung in die Cloudinnovation – Demokratisieren von Daten
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 158c3e25bac2124312a8ceaf3ac5500a58246f48
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808497"
---
# <a name="democratize-data"></a>Demokratisieren von Daten

Kohle, Öl und menschliches Potenzial waren während der industriellen Revolution die drei entscheidenden Ressourcen. Diese Ressourcen bildeten das Fundament für Unternehmen und bewirkten schließlich einen grundsätzlichen Wandel von Märkten und Nationen. In der digitalen Wirtschaft gibt es drei gleichermaßen wichtige Ressourcen: Daten, Geräte und menschliches Potenzial. Jede dieser Ressourcen weist ein hervorragendes Innovationspotenzial auf. In der heutigen Zeit sind bei jeder Innovationsinitiative die Daten das neue Öl.

Jedes Unternehmen verfügt heute über zahlreiche Daten, die genutzt werden könnten, um die Kundenanforderungen effektiver zu erkennen und zu erfüllen. Leider war der Prozess des Minings dieser Daten, um Innovationen voranzutreiben, lange kostspielig und zeitaufwändig. Viele der nützlichsten Lösungen für Kundenanforderungen werden nicht genutzt, da die entscheidenden Personen nicht auf die benötigten Daten zugreifen können.

Die Demokratisierung von Daten ist der Prozess, diese Daten in die richtigen Hände zu legen, um Innovationen voranzutreiben. Dieser Prozess kann verschiedene Formen annehmen, umfasst jedoch im Allgemeinen Lösungen für erfasste oder integrierte Rohdaten, die Zentralisierung der Daten, die Freigabe der Daten und das Schützen der Daten. Bei erfolgreicher Anwendung dieser Methoden können Experten im Unternehmen die Daten nutzen, um Hypothesen zu testen. In vielen Fällen können Cloudeinführungsteams mit ausschließlicher Verwendung von Daten [Lösungen mit Blick auf die Kundenanforderungen erstellen](./build.md) und damit schnell auf bestehende Kundenanforderungen reagieren.

## <a name="process-of-democratizing-data"></a>Prozess der Demokratisierung von Daten

In den folgenden Phasen werden die Entscheidungen und Ansätze erläutert, die für die Einführung einer Lösung zur Datendemokratisierung erforderlich sind. Nicht jede Phase ist notwendigerweise erforderlich, um eine bestimmte Lösung zu erstellen. Sie sollten jedoch jede Phase auswerten, wenn Sie eine Lösung für eine Kundenhypothese entwickeln. Jede stellt einen einzigartigen Ansatz für das Erstellen innovativer Lösungen dar.

![Prozess zur Demokratisierung von Daten](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Freigeben von Daten

Beim [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) stellen alle Prozesse die Kundenanforderung über eine technische Lösung. Da das Demokratisieren von Daten hier keine Ausnahme bildet, beginnen wir mit der Freigabe von Daten. Um Daten zu demokratisieren, muss eine Lösung zur Freigabe von Daten für einen Datenconsumer enthalten sein. Der Datenconsumer könnte ein direkter Kunde oder ein Stellvertreter sein, der Entscheidungen für Kunden trifft. Zugelassene Datenconsumer können zentralisierte Daten ohne Unterstützung durch IT-Personal analysieren und abfragen und daraus Berichte erstellen.

Viele erfolgreiche Innovationen wurden als MVPs (Minimum Viable Product, Produkt mit Mindestrentabilität) gestartet, die manuelle, datengesteuerte Prozesse im Auftrag des Kunden bereitstellen. In diesem Concierge-Modell ist ein Mitarbeiter der Datenconsumer. Dieser Mitarbeiter verwendet Daten, um den Kunden zu unterstützen. Jedes Mal, wenn der Kunde die manuelle Unterstützung einbindet, kann eine Hypothese getestet und überprüft werden. Dieser Ansatz ist oft ein kostengünstiges Mittel, um eine kundenorientierte Hypothese vor hohen Investitionen in integrierte Lösungen zu testen.

Mit den wichtigsten Tools für die direkte Freigabe von Daten für Datenconsumer wie [Power BI](https://docs.microsoft.com/power-bi) werden u. a. Self-Service-Berichte erstellt oder Daten verarbeitet, die in andere Umgebungen eingebettet sind.

> [!NOTE]
> Bevor Sie Daten freigeben, sollten Sie unbedingt die folgenden Abschnitte gelesen haben. Die Freigabe von Daten erfordert möglicherweise Governance, um den Schutz für die freigegebenen Daten zu gewährleisten. Außerdem sind die Daten möglicherweise über mehrere Clouds verteilt, sodass sie zentralisiert werden müssten. Ein Großteil der Daten kann sich sogar in Anwendungen befinden, sodass vor der Freigabe eine Datensammlung notwendig ist.

### <a name="govern-data"></a>Steuern von Daten

Aus dem Freigeben von Daten kann schnell ein MVP resultieren, das für den Dialog mit dem Kunden verwendet werden kann. Um diese freigegebenen Daten jedoch in umsetzbare Informationen umzuwandeln, ist im Allgemeinen etwas mehr erforderlich. Nachdem eine Hypothese durch die Datenfreigabe überprüft wurde, ist die nächste Entwicklungsphase meist die Data Governance.

Data Governance ist ein umfassendes Thema, das ein eigenes dediziertes Framework erfordern könnte. Der Grad an Granularität liegt nicht im Umfang des [Frameworks für die Cloudeinführung](../../index.md). Mehrere Aspekte der Datenkontrolle sollten jedoch berücksichtigt werden, wenn die Kundenhypothese überprüft wird. Beispiel:

- **Sind die freigegebenen Daten vertraulich?** Vor jeder öffentlichen Freigabe [sollten Daten klassifiziert werden](../../govern/policy-compliance/data-classification.md), um die Interessen der Kunden und des Unternehmens zu schützen.
- **Wenn die Daten vertraulich sind, wurden sie geschützt?** Der Schutz vertraulicher Daten sollte eine Anforderung für alle demokratisierten Daten sein. Die auf das [Schützen von Datenlösungen](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions) konzentrierte Beispielworkload bietet einige Verweise zum Schützen von Daten.
- **Sind die Daten katalogisiert?** Das Erfassen von Details zu den freigegebenen Daten unterstützt die langfristige Datenverwaltung. Tools zum Dokumentieren von Daten wie Azure Data Catalog können diesen Prozess in der Cloud erheblich vereinfachen. Anleitungen zum [Kommentieren von Daten](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) und zum [Dokumentieren von Datenquellen](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) können den Prozess beschleunigen.

Wenn die Demokratisierung von Daten für eine kundenorientierte Hypothese wichtig ist, sollte die Governance von gemeinsam genutzten Daten im Freigabeplan enthalten sein. Dadurch werden Kunden, Datenconsumer und das Unternehmen geschützt.

### <a name="centralize-data"></a>Zentralisieren von Daten

Wenn die Daten in einer IT-Umgebung lückenhaft sind, können die Innovationsmöglichkeiten äußerst eingeschränkt, teuer und zeitaufwendig sein. Die Cloud bietet neue Möglichkeiten, Daten über Datensilos hinweg zu zentralisieren. Wenn zum [Erstellen von Lösungen mit Blick auf die Kundenanforderungen](./build.md) eine Zentralisierung mehrerer Datenquellen erforderlich ist, kann die Cloud das Testen von Hypothesen beschleunigen.

> [!CAUTION]
> Die Zentralisierung von Daten stellt bei jedem Innovationsprozess ein Risiko dar. Wenn die Datenzentralisierung jedoch statt einer Kundenwertquelle eine [technische Spitze](./build.md#reduce-complexity-and-delay-technical-spikes) ist, sollte die Zentralisierung aufgeschoben werden, bis die Kundenhypothese überprüft wurde.

Wenn die Zentralisierung der Daten erforderlich ist, sollten Sie zunächst den entsprechenden Datenspeicher für die zentralisierten Daten definieren. Es ist ratsam, ein Data Warehouse in der Cloud einzurichten. Diese skalierbare Option bietet einen zentralen Speicherort für Ihre sämtlichen Daten. Diese Art von Lösung ist in den Optionen „Analytische Onlineverarbeitung“ (Online Analytical Processing, OLAP) oder „Big Data“ verfügbar.

Die Referenzarchitekturen für [OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing)- und [Big Data](https://docs.microsoft.com/azure/architecture/data-guide/big-data)-Lösungen können bei der Auswahl der geeignetsten Lösung in Azure helfen. Wenn eine Hybridlösung erforderlich ist, kann die Referenzarchitektur für das [Erweitern lokaler Datenlösungen auf die Cloud](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) auch zur Beschleunigung der Lösungsentwicklung beitragen.

> [!IMPORTANT]
> Je nach Kundenanforderung und Lösungsausrichtung ist möglicherweise ein einfacherer Ansatz ausreichend. Der Cloudarchitekt sollte das Team auffordern, kostengünstigere Lösungen zu berücksichtigen, die insbesondere während der frühen Phase der Entwicklung zu einer schnelleren Validierung der Kundenhypothese führen könnten. Im folgenden Abschnitt zum Sammeln von Daten werden einige Szenarien behandelt, die möglicherweise eine andere Lösung für Ihre Situation empfehlen.

### <a name="collect-data"></a>Sammeln von Daten

Wenn Daten zentralisiert werden müssen, um einer Kundenanforderung gerecht zu werden, müssen die Daten sehr wahrscheinlich auch aus verschiedenen Quellen gesammelt und in den zentralisierten Datenspeicher verschoben werden. Es gibt zwei primäre Formen der Datensammlung: *Integration* und *Erfassung*.

**Integration:** Daten, die sich in einem vorhandenen Datenspeicher befinden, können mithilfe herkömmlicher Datenverschiebungstechniken in den zentralisierten Datenspeicher integriert werden. Dies gilt insbesondere für Szenarien, in denen die Multicloud-Datenspeicherung eine Rolle spielt. Zu diesen Techniken gehört das Extrahieren der Daten aus dem vorhandenen Datenspeicher und das anschließende Laden in den zentralen Datenspeicher. An einem bestimmten Punkt in diesem Prozess werden die Daten typischerweise transformiert, sodass sie im zentralen Speicher besser verwendbar und relevant sind.

Mit cloudbasierten Tools stehen diese Techniken in Form von Tools mit nutzungsabhängiger Bezahlung zur Verfügung und senken so die Hemmschwelle für den Einstieg in Datensammlung und -zentralisierung. Tools wie Azure Database Migration Service und Azure Data Factory sind zwei Beispiele. Die Referenzarchitektur für [Data Factory mit einem OLAP-Datenspeicher](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) ist ein Beispiel einer solchen Lösung.

**Erfassung:** Einige Daten befinden sich nicht in einem vorhandenen Datenspeicher. Wenn diese temporären Daten eine primäre Quelle für die Innovation sind, sollten alternative Ansätze in Erwägung gezogen werden. Temporäre Daten finden Sie in einer Vielzahl von vorhandenen Quellen, z. B. Anwendungen, APIs, Datenströme, IoT-Geräte, Blockchain, Anwendungscache, Medieninhalt oder sogar Flatfiles.

Diese unterschiedlichen Datenformen können Sie im Rahmen einer OLAP- oder Big Data-Lösung in einen zentralen Datenspeicher integrieren. Für frühe Iterationen von Erstellen-Messen-Lernen-Zyklen ist eine OLTP-Lösung (Online Transactional Processing) jedoch möglicherweise mehr als ausreichend, um eine Kundenhypothese zu validieren. OLTP-Lösungen sind nicht für alle Berichterstellungsszenarien die qualitativ hochwertigste Lösung. Wenn Sie jedoch [Beim Erstellen einen Blick auf die Kundenanforderungen behalten](./build.md), sollten Sie sich mehr auf die Kundenanforderungen als auf die Entscheidungen zu den technischen Tools konzentrieren. Nachdem die Kundenhypothese bedarfsabhängig überprüft wurde, ist möglicherweise eine geeignetere Plattform erforderlich. Die Referenzarchitektur für [OLTP-Datenspeicher](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) kann bei der Ermittlung des für Ihre Lösung am besten geeigneten Datenspeichers helfen.

**Virtualisieren:** Die Integration und Erfassung von Daten kann manchmal die Innovation bremsen. Wenn bereits eine Lösung für die Datenvirtualisierung verfügbar ist, stellt dies möglicherweise ein geeigneteren Ansatz dar. Erfassung und Integration können sowohl Speicher- als auch Entwicklungsanforderungen duplizieren, die Datenlatenz steigern, die Angriffsfläche vergrößern, Qualitätsprobleme verursachen und den Governanceaufwand erhöhen. Die Datenvirtualisierung ist eine zeitgemäße Alternative, bei der die ursprünglichen Daten an einem einzigen Ort gespeichert werden und Pass-Through- oder zwischengespeicherte Abfragen der Quelldaten erstellt werden.

SQL Server 2017 und Azure SQL Data Warehouse unterstützen [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide). Dies ist der in Azure am häufigsten verwendete Ansatz zur Datenvirtualisierung.

## <a name="next-steps"></a>Nächste Schritte

Wenn die Strategie zur Demokratisierung der Daten feststeht, evaluieren Sie im nächsten Schritt Ansätze zum [Einbinden von Kunden durch Apps](./apps.md).

> [!div class="nextstepaction"]
> [Einbinden von Kunden durch Apps](./apps.md)
