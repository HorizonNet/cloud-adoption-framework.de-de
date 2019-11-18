---
title: 'Geschäftliche Verpflichtung: Cloudverwaltung und -vorgänge'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Geschäftliche Verpflichtung: Cloudverwaltung und -vorgänge'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f5461ea659ae2363e98ddf45d8623e21f1ce0d90
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565194"
---
# <a name="business-commitment-in-cloud-management"></a>Die geschäftliche Verpflichtung in der Cloudverwaltung

Die Definition einer _geschäftlichen Verpflichtung_ ist eine Übung des Ausbalancierens von Prioritäten. Das richtige Betriebsverwaltungsniveau muss zu akzeptablen Betriebskosten erzielt werden. Hier die Balance zu finden, erfordert einige Datenpunkte und Berechnungen, die wir in diesem Artikel beschrieben haben.

![Ausgleichen von Kosten und Resilienz](../../_images/manage/business-commitment-scale.png)

Verpflichtungen gegenüber der Geschäftsstabilität durch technische Resilienz oder andere Auswirkungen auf die Vereinbarung zum Servicelevel (SLA) basieren auf einer geschäftlichen Begründung. Für die meisten Workloads in einer Umgebung ist eine Basiscloudverwaltung ausreichend. Für andere lassen sich 2- bis 4-fache Kosten aufgrund der möglichen Auswirkungen in Form von Geschäftsunterbrechungen mühelos rechtfertigen.

Die vorherigen Artikel in dieser Serie können Ihnen helfen, die Klassifizierung und Auswirkung von Unterbrechungen bei verschiedenen Workloads zu verstehen. Dieser Artikel hilft Ihnen bei der Berechnung der Ergebnisse. Wie in der vorherigen Abbildung dargestellt, gibt es auf jeder Ebene der Cloudverwaltung Wendepunkte, bei denen die Kosten schneller ansteigen können als die Resilienz. Diese Wendepunkte fordern ausführliche Geschäftsentscheidungen und Geschäftsverpflichtungen.

## <a name="determine-a-proper-commitment-with-the-business"></a>Bestimmen einer angemessenen Verpflichtung gegenüber dem Unternehmen

Für jede Workload im Portfolio sollten sich das Cloudbetriebsteam und das Cloudstrategieteam an der Verwaltungsebene ausrichten, die direkt vom Cloudbetriebsteam bereitgestellt wird.

Im Folgenden sind die wichtigsten Aspekte aufgeführt, die beim Aufstellen einer Verpflichtung gegenüber dem Unternehmen zu berücksichtigen sind:

- IT-Betriebsvoraussetzungen
- Verwaltungsverantwortlichkeit
- Cloudmandant
- Weiche Kostenfaktoren
- ROI bei Verlustvermeidung
- Validierung der Verwaltungsebene

Als Unterstützung für Ihren Entscheidungsprozess wird im weiteren Verlauf dieses Artikels jeder dieser Aspekte eingehender beschrieben.

## <a name="it-operations-prerequisites"></a>IT-Betriebsvoraussetzungen

Im [Azure-Verwaltungsleitfaden](../azure-management-guide/index.md) werden die in Azure verfügbaren Verwaltungstools beschrieben. Bevor eine Verpflichtung gegenüber dem Unternehmen formuliert wird, sollte die IT eine akzeptable Verwaltungsbaseline auf Standardniveau festlegen, die auf alle verwalteten Workloads angewendet werden soll. Anschließend sollte die IT basierend auf der Anzahl von CPU-Kernen, dem Speicherplatz auf dem Datenträger und anderen ressourcenbezogenen Variablen für jede der verwalteten Workloads im IT-Portfolio die Standardverwaltungskosten berechnen. Außerdem sollte für jede Workload basierend auf der Architektur eine zusammengesetzte SLA geschätzt werden.

> [!TIP]
> IT-Betriebsteams setzen häufig eine standardmäßige minimale Betriebszeit von mindestens 99,9 Prozent für die anfängliche zusammengesetzte SLA an. Sie können die Verwaltungskosten auch basierend auf der durchschnittlichen Workload normalisieren, insbesondere bei Lösungen, in denen die Anforderungen an Protokollierung und Speicher minimal sind. Die Ermittlung des Durchschnitts der Kosten für ein paar Workloads von mittlerer Wichtigkeit kann der Ausgangspunkt für erste Konversationen sein.

<!-- -->

> [!TIP]
> Wenn Sie die Cloudverwaltung mit der Arbeitsmappe [Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) planen, sollten die Felder für Operations Management aktualisiert werden, um diese Voraussetzungen zu berücksichtigen. Zu diesen Feldern zählen _Commitment Level_ (Verpflichtungsebene), _Composite SLA_ (Zusammengesetzte SLA) und _Monthly cost_ (Monatliche Kosten). „Monthly Cost“ sollte die Kosten der hinzugefügten Tools zur Betriebsverwaltung pro Monat darstellen.

Die Betriebsverwaltungsbaseline dient als Ausgangspunkt, der in jedem der folgenden Abschnitte überprüft wird.

## <a name="management-responsibility"></a>Verwaltungsverantwortlichkeit

In einer herkömmlichen lokalen Umgebung werden die Kosten für die Verwaltung der Umgebung häufig als versunkene Kosten des IT-Betriebs angesetzt. In der Cloud ist die Verwaltung eine gezielte Entscheidung mit direkten Auswirkungen auf das Budget. Die Kosten der einzelnen Verwaltungsfunktionen können den einzelnen in der Cloud ausgeführten Workloads direkter zugeordnet werden. Dieser Ansatz ermöglicht eine bessere Kontrolle, stellt jedoch an Cloudbetriebsteams und Cloudstrategieteams die Anforderung, zunächst eine Verpflichtung zu einer Vereinbarung über Zuständigkeiten einzugehen.

Organisationen können auch entscheiden, [einige ihrer laufenden Verwaltungsfunktionen an einen Dienstanbieter auszulagern](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Diese Dienstanbieter können Organisationen mit [Azure Lighthouse](https://azure.com/lighthouse) ermöglichen, den Zugriff auf ihre Ressourcen genauer zu steuern sowie einen umfassenderen Einblick in die von den Dienstanbietern ausgeführten Aktionen zu erhalten.

- **Delegierte Verantwortung:** Da es nicht erforderlich ist, zu zentralisieren und einen Mehraufwand für die Betriebsverwaltung vorauszusetzen, erwägen die IT-Abteilungen vieler Organisationen neue Ansätze. Ein gängiger Ansatz wird als _Delegierte Verantwortung_ bezeichnet. In einem Cloudkompetenzzentrum-Modell bieten Plattformvorgänge und Plattformautomatisierung Self-Service-Verwaltungstools, die unabhängig von einem zentralen IT-Betriebsteam von unternehmensgeführten Betriebsteams genutzt werden können. Dieser Ansatz ermöglicht den Beteiligten im Unternehmen eine umfassende Kontrolle verwaltungsrelevanter Budgets. Außerdem kann das Cloudkompetenzzentrum (CCoE) so sicherstellen, dass ein minimaler Satz von Schutzmaßnahmen ordnungsgemäß implementiert wird. In diesem Modell fungiert die IT als Broker und Führer, um dem Unternehmen zu helfen, vernünftige Entscheidungen zu treffen. Geschäftsvorgänge überwachen tägliche Vorgänge abhängiger Workloads.

- **Zentralisierte Verantwortung:** Complianceanforderungen, technische Komplexität und einige freigegebene Dienstmodelle erfordern möglicherweise ein _zentrales IT_-Modell. In diesem Modell nimmt die IT-Abteilung weiterhin ihre Verantwortlichkeiten für die Betriebsverwaltung wahr. Umgebungsentwurf, Verwaltungskontrollen und Governancetools können zentral verwaltet und gesteuert werden, was die Rolle der Beteiligten im Unternehmen einschränkt, wenn Verpflichtungen zur Verwaltung eingegangen werden. Die Transparenz hinsichtlich Kosten und Architektur von Cloudansätzen erleichtern es der zentralisierten IT stark, die Kosten und Verwaltungsebene für die einzelnen Workloads zu kommunizieren.

- **Gemischtes Modell:** Die Klassifizierung ist der Kern eines _gemischten Modells_ für Verantwortlichkeiten für die Betriebsverwaltung. Unternehmen, die sich mitten im Wandel von „lokal“ zur Cloud befinden, benötigen möglicherweise für eine Weile ein „Zuerst lokal“-Betriebsmodell. Unternehmen mit strengen Complianceanforderungen oder die von langfristigen Verträgen mit IT-Outsourcinganbietern abhängen, benötigen möglicherweise ein zentralisiertes Betriebsmodell.

  Unabhängig von ihren Einschränkungen müssen Unternehmen heute innovativ sein. Wenn eine schnelle Innovation mitten in einem Modell einer zentralen IT mit zentralisierter Verantwortung gedeihen muss, könnte ein gemischter Ansatz für ein Gleichgewicht sorgen. Bei diesem Ansatz bietet die zentrale IT ein zentralisiertes Betriebsmodell für alle Workloads, die unternehmenskritisch sind oder vertrauliche Informationen enthalten. Gleichzeitig können alle anderen Klassifizierungen der Workload in einer Cloudumgebung platziert werden, die für delegierte Verantwortlichkeiten entworfen wurde. Der Ansatz der zentralisierten Verantwortlichkeit dient als allgemeines Betriebsmodell. Das Unternehmen besitzt dann die Flexibilität, ein spezialisiertes Betriebsmodell basierend auf dem erforderlichen Niveau von Unterstützung und Vertraulichkeit anzunehmen.

Der erste Schritt besteht in der Verpflichtung zu einem Verantwortlichkeitsansatz, der dann die folgenden Verpflichtungen prägt.

**Welche Organisation ist für diese Workload für die tägliche Betriebsverwaltung verantwortlich?**

## <a name="cloud-tenancy"></a>Cloudmandant

Bei den meisten Unternehmen ist die Verwaltung einfacher, wenn sich alle Ressourcen in einem einzigen Mandanten befinden. Allerdings müssen einige Organisationen möglicherweise mehrere Mandanten verwalten. Informationen dazu, warum ein Unternehmen eine mehrinstanzenfähige Azure-Umgebung benötigt, finden Sie unter [Zentralisieren von Verwaltungsvorgängen mit Azure Lighthouse](../centralize-operations.md).

**Befindet sich diese Workload neben allen anderen Workloads in einem einzelnen Azure-Mandanten?**

## <a name="soft-cost-factors"></a>Weiche Kostenfaktoren

Im nächsten Abschnitt wird ein Ansatz für Vergleichsrenditen erläutert, die Ebenen von Verwaltungsprozessen und Tools zugeordnet sind. Am Ende dieses Abschnitts werden für jede analysierte Workload die Kosten der Verwaltung im Vergleich zu den vorhergesagten Auswirkungen von Geschäftsunterbrechungen gemessen. Dieser Ansatz ist eine relativ einfache Methode, um zu verstehen, ob eine Investition in aufwändigere Verwaltungsansätze gerechtfertigt ist.

Vor dem Ausführen der Zahlen ist es wichtig, die weichen Kostenfaktoren zu betrachten. Weiche Kostenfaktoren erzeugen eine Rendite, aber diese Rendite ist schwierig in direkten Kosteneinsparungen zu messen, die in einer Gewinn-und-Verlust-Rechnung sichtbar wären. Weiche Kostenfaktoren sind wichtig, da sie darauf hindeuten können, dass in eine höhere Verwaltungsebene investiert werden muss, als fiskalisch klug ist.

Einige Beispiele für diese weichen Kostenfaktoren sind:

- Tägliche Verwendung einer Workload durch den Vorstand oder den CEO.
- Nutzung einer Workload durch Top-_x Prozent_ von Kunden, was an anderer Stelle größere Auswirkungen auf den Umsatz bewirkt.
- Auswirkung auf die Zufriedenheit der Mitarbeiter.

Der nächste Datenpunkt, der erforderlich ist, um eine Verpflichtung einzugehen, ist eine Liste der weichen Kostenfaktoren. Diese Faktoren müssen in dieser Phase nicht dokumentiert werden, aber der Geschäftsbeteiligte sollte die Wichtigkeit dieser Faktoren und deren Ausschluss aus den folgenden Berechnungen beachten.

## <a name="calculate-loss-avoidance-roi"></a>Berechnen des ROI bei Verlustvermeidung

Beim Berechnen der relativen Rendite der Betriebsverwaltungskosten sollte das für Cloudvorgänge verantwortliche IT-Team die zuvor genannten Voraussetzungen erfüllen und von einer minimalen Verwaltungsebene für alle Workloads ausgehen.

Die nächste Verpflichtung ist die Akzeptanz der Kosten, die mit dem Baselineverwaltungsangebot verbunden sind, durch das Unternehmen.

**Ist das Unternehmen damit einverstanden, in das Baselineangebot zu investieren, um die Mindestanforderungen der Cloudvorgänge zu erfüllen?**

Wenn das Unternehmen dieser Verwaltungsebene nicht zustimmt, muss eine Lösung entwickelt werden, mit der das Unternehmen fortfahren kann, ohne dass die Cloudvorgänge anderer Workloads wesentlich beeinträchtigt werden.

Wenn das Unternehmen mehr als die Standardverwaltungsebene wünscht, hilft der Rest dieses Abschnitts bei der Überprüfung dieser Investition und der damit verbundenen Rendite (in Form der Verlustvermeidung).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Höhere Verwaltungsebenen: Entwurfsprinzipien und Dienstkatalog

Für verwaltete Lösungen gibt es mehrere Entwurfsprinzipien und Vorlagenlösungen, die zusätzlich zur Verwaltungsbaseline angewendet werden können. Jedes dieser Entwurfsprinzipien für Zuverlässigkeit und Resilienz erhöht die Betriebskosten für die Workload. Damit IT und Unternehmen diesen zusätzlichen Verpflichtungen zustimmen, ist es wichtig, potenzielle Verluste zu verstehen, die mit dieser höheren Investition vermieden werden können.

In den folgenden Berechnungen werden Formeln erläutert, die Ihnen dabei helfen, die Unterschiede zwischen Verlusten und Investitionen für eine intensivere Verwaltung zu verstehen. Anleitungen zum Berechnen der Kosten für eine intensivere Verwaltung finden Sie unter [Workloadautomatisierung](./workload.md) und [Plattformautomatisierung](./platform.md).

> [!TIP]
> Wenn Sie die Cloudverwaltung mit der Arbeitsmappe [Operations Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) planen, aktualisieren Sie die Felder für Operations Management, um jede Konversation zu berücksichtigen. Zu diesen Feldern zählen _Commitment Level_ (Verpflichtungsebene), _Composite SLA_ (Zusammengesetzte SLA) und _Monthly cost_ (Monatliche Kosten). „Monthly Cost“ sollte die monatlichen Kosten der hinzugefügten Tools zur Betriebsverwaltung darstellen. Nach der Aktualisierung aktualisieren diese Felder die ROI-Formeln und jedes der folgenden Felder.

### <a name="estimate-outage-hours-per-year"></a>Geschätzter Ausfall (Stunden pro Jahr)

„Composite SLA“ (zusammengesetzte SLA) ist die Vereinbarung zum Service Level, die auf der Bereitstellung der einzelnen Ressourcen in der Workload basiert. Dieses Feld steuert den _geschätzten Ausfall_ (in der Arbeitsmappe mit _Est. Outage_ beschriftet). Um den geschätzten Ausfall in Stunden pro Jahr zu berechnen, ohne die Arbeitsmappe zu verwenden, wenden Sie die folgende Formel an:

> _Geschätzter Ausfall = (1 - Prozentsatz der zusammengesetzten SLA) &#215; Anzahl von Stunden pro Jahr_

In der Arbeitsmappe wird der Standardwert von _8.760 Stunden pro Jahr_ verwendet.

### <a name="standard-loss-impact"></a>Standardmäßige Auswirkungen von Datenverlust

Die _standardmäßigen Auswirkungen von Datenverlust_ (Titel _Standard impact_ in der Arbeitsmappe) prognostizieren die finanziellen Auswirkungen eines Ausfalls, vorausgesetzt, dass die Vorhersage _geschätzter Ausfall_ korrekt ist. Um diese Vorhersage ohne Verwendung der Arbeitsmappe zu berechnen, wenden Sie die folgende Formel an:

> _Standardmäßige Auswirkung = geschätzter Ausfall bei drei Neunen der Betriebszeit &#215; Zeit-Wert-Auswirkung_

Dies dient als Grundlage für die Kosten, wenn die Geschäftsbeteiligten entscheiden, in eine höhere Verwaltungsebene zu investieren.

### <a name="composite-sla-impact"></a>Auswirkung der zusammengesetzten SLA

Die _Auswirkung der zusammengesetzten SLA_ (Titel _Commitment level impact_ (Auswirkung der Verpflichtungsebene) in der Arbeitsmappe) stellt die aktualisierten fiskalischen Auswirkungen dar, basierend auf den Änderungen der Betriebszeit-SLA. Anhand dieser Berechnung können Sie die projizierten finanziellen Auswirkungen beider Optionen vergleichen. Um diese vorhergesagte Auswirkung ohne die Arbeitsmappe zu berechnen, wenden Sie die folgende Formel an:

> _Auswirkung der zusammengesetzten SLA = geschätzter Ausfall &#215; Zeit-Wert-Auswirkung_

Der Wert stellt die potenziellen Verluste dar, die durch die geänderte Verpflichtungsebene und die neue zusammengesetzte SLA vermieden werden sollen.

### <a name="comparison-basis"></a>Vergleichsbasis

_Comparison basis_ (Vergleichsbasis) wertet „Standard Impact“ und „Composite SLA Impact“ aus, um zu bestimmen, was in der Renditespalte am besten geeignet ist.

### <a name="return-on-loss-avoidance"></a>Rendite bei Verlustvermeidung

Wenn die Kosten für die Verwaltung einer Workload die potenziellen Verluste überschreiten, ist die in der Cloudverwaltung vorgeschlagene Investition möglicherweise nicht rentabel. Beachten Sie zum Vergleichen der _Rendite bei Verlustvermeidung_ die Spalte mit der Bezeichnung _Annual ROI****_ (jährlicher ROI). Um diese Spalte selbst zu berechnen, verwenden Sie die folgende Formel:

> _Rendite bei Verlustvermeidung = (Vergleichsbasis - (monatliche Kosten &#215; 12)) &#247; (monatliche Kosten &#215; 12))_

Wenn keine weiteren weichen Kostenfaktoren berücksichtigt werden müssen, kann dieser Vergleich schnell zeigen, ob eine höhere Investition in Cloudbetrieb, Resilienz, Zuverlässigkeit oder andere Bereiche erfolgen sollte.

## <a name="validate-the-commitment"></a>Überprüfen der Verpflichtung

An diesem Punkt des Prozesses wurden Verpflichtungen eingegangen: zentralisierte oder delegierte Verantwortlichkeit, Azure-Mandant und Verpflichtungsgrad. Jede Verpflichtung sollte überprüft und dokumentiert werden, um sicherzustellen, dass das Cloudbetriebsteam, das Cloudstrategieteam und die Geschäftsbeteiligten sich an diese Verpflichtung zur Verwaltung der Workload halten.

## <a name="next-steps"></a>Nächste Schritte

Sobald Verpflichtungen eingegangen wurden, können die zuständigen Betriebsteams mit der Konfiguration für die betreffende Workload beginnen. Evaluieren Sie zunächst verschiedene Ansätze zu [Bestand und Transparenz bei der Cloudverwaltung](./inventory.md).

> [!div class="nextstepaction"]
> [Bestands- und Transparenzoptionen](./inventory.md)
