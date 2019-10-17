---
title: Erste Schritte auf Ihrem Weg zur Cloudmigration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erste Schritte auf Ihrem Weg zur Cloudmigration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: fb521115d0a59af123bd78fdc2f4cc7c72939fb6
ms.sourcegitcommit: b30952f08155513480c6b2c47a40271c2b2357cf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2019
ms.locfileid: "72378005"
---
# <a name="getting-started-with-a-cloud-migration-journey"></a>Erste Schritte auf Ihrem Weg zur Cloudmigration

Erfahren Sie mehr über die Verwendung des Microsoft Cloud Adoption Framework für Azure zum Starten einer Cloudmigration. Dieses Framework bietet umfassende Leitlinien für die Umstellung älterer Anwendungsworkloads mit innovativen cloudbasierten Technologien.

## <a name="executive-summary"></a>Kurzfassung

Das Cloud Adoption Framework unterstützt Kunden bei der Umsetzung einer vereinfachten Cloudeinführung. Dieses Framework enthält detaillierte Informationen über eine End-to-End-Cloudeinführung, beginnend mit den anvisierten Geschäftsergebnissen und der Ausrichtung der Cloudbereitschaft und der entsprechenden Bewertungen auf klar definierte Geschäftsziele. Diese Ergebnisse werden über einen definierten Pfad für die Cloudeinführung erreicht. Bei der migrationsbasierten Einführung konzentriert sich der definierte Pfad weitgehend auf die Durchführung einer Migration von lokalen Workloads in die Cloud. Manchmal schließt dieser Weg auch die Modernisierung von Workloads ein, um die Rendite aus dem Migrationsaufwand zu erhöhen.

Dieses Framework ist in erster Linie für Cloudarchitekten und die Cloudstrategieteams konzipiert, die die Aktivitäten der Cloudeinführung leiten. Viele Themen in diesem Framework sind jedoch auch für andere Rollen im Unternehmen und in der IT relevant. Cloudarchitekten fungieren häufig als Moderatoren, um die einzelnen relevanten Rollen einzubinden. Diese Kurzfassung dient der Vorbereitung der verschiedenen Rollen vor der Durchführung von Gesprächen.

> [!NOTE]
> Bei diesem Leitfaden handelt es sich aktuell um eine öffentliche Vorschauversion. Terminologie, Ansätze und Leitlinien werden umfassend mit Kunden, Partnern und Microsoft-Teams in dieser Vorschauphase getestet. Das Inhaltsverzeichnis und die Leitlinien können sich daher im Laufe der Zeit geringfügig ändern.

## <a name="motivations"></a>Beweggründe

Cloudmigrationen können Unternehmen dabei unterstützen, ihre gewünschten Geschäftsergebnissen zu erzielen. Eine klare Kommunikation der Beweggründe, Geschäftsfaktoren und Erfolgsmessungen ist eine wichtige Grundlage für kluge Entscheidungen während des gesamten Cloudmigrationsprozesses. In der folgenden Tabelle werden die Beweggründe klassifiziert, um diese Kommunikation zu erleichtern. Es wird davon ausgegangen, dass die meisten Unternehmen Beweggründe für jede Klassifizierung haben. In dieser Tabelle geht es nicht darum, die Ergebnisse zu begrenzen, sondern die Priorisierung der allgemeinen Ziele und Beweggründe zu erleichtern:

<!-- markdownlint-disable MD033 -->

|Wichtige Unternehmensereignisse | Beweggründe für Migration | Beweggründe für Innovation |
|---------|---------|---------|
| Ausstieg aus Rechenzentrum<br/><br/>Fusionen, Übernahme oder Veräußerung<br/><br/>Reduzierung der Kapitalkosten<br/><br/>Ende des Supports für unternehmenskritische Technologien<br/><br/>Reaktion auf Änderungen bezüglich der Einhaltung gesetzlicher Bestimmungen<br/><br/>Erfüllen neuer Anforderungen an die Datenhoheit<br/><br/>Verringern von Unterbrechungen und Verbessern der IT-Stabilität|Kostenersparnis<br/><br/>Verringerung der Anbieter- oder technischen Komplexität<br/><br/>Optimierung interner Vorgänge<br/><br/>Erhöhen der Unternehmensflexibilität<br/><br/>Vorbereiten auf neue technische Funktionen und Möglichkeiten<br/><br/>Skalieren, um die Marktanforderungen zu erfüllen<br/><br/>Skalieren, um die geografischen Anforderungen zu erfüllen|Vorbereiten auf neue technische Funktionen und Möglichkeiten<br/><br/>Entwickeln neuer technischer Funktionen und Möglichkeiten<br/><br/>Skalieren, um die Marktanforderungen zu erfüllen<br/><br/>Skalieren, um die geografischen Anforderungen zu erfüllen<br/><br/>Erhöhen der Kundenzufriedenheit/Kundenbindung<br/><br/>Transformieren von Produkten oder Diensten<br/><br/>Revolutionieren des Markts mit neuen Produkten oder Diensten|

<!-- markdownlint-enable MD033 -->

Wenn eine Reaktion auf wichtige Unternehmensereignisse höchste Priorität hat, ist es wichtig, sich frühzeitig mit der [Cloudimplementierung](#cloud-implementation) zu befassen, oft parallel zu Strategie- und Planungsaktivitäten. Ein solcher Ansatz erfordert eine wachstumsorientierte Denkweise und die Bereitschaft, Prozesse basierend auf den direkten Erfahrungen iterativ zu verbessern.

Wenn Beweggründe für die Migration Priorität haben, spielen [Strategie und Planung](#cloud-strategy-and-planning) frühzeitig im Prozess eine wichtige Rolle. Es wird jedoch dringend empfohlen, die [Implementierung](#cloud-implementation) der ersten Workload parallel zur Planung durchzuführen, damit das Team alle Lernkurven in Verbindung mit der Cloud besser verstehen und planen kann.

Wenn Beweggründe für Innovation höchste Priorität haben, sind für die Strategie und Planung zusätzliche Investitionen frühzeitig im Prozess erforderlich, um ein ausgewogenes Portfolio und eine sinnvolle Ausrichtung der Investitionen während der Cloudmigration sicherzustellen. Weitere Informationen zur Umsetzung der Beweggründe für Innovation finden Sie unter [Grundlegendes zur Vorgehensweise bei Innovationen](./innovate.md).

Durch die Vorbereitung aller Teilnehmer auf den Migrationsaufwand unter Berücksichtigung der Beweggründe können klügere Entscheidungen getroffen werden. In der folgenden Migrationsmethodik wird dargelegt, wie Microsoft den Kunden vorschlägt, diese Entscheidungen in einer einheitlichen Methodik zu steuern.

## <a name="migration-approach"></a>Migrationsansatz

Das Cloud Adoption Framework schafft ein allgemeines Konstrukt aus den Komponenten Planen, Bereitmachen und Übernehmen, um die Arten von Aufwand zu gruppieren, die bei jeder Cloudeinführung erforderlich sind. Diese Kurzfassung basiert auf diesem allgemeinen Flow, um iterative Prozesse einzurichten, die Lift & Shift- und Optimierungsmaßnahmen **sowie** Modernisierungsmaßnahmen in einem einzigen Ansatz über alle Cloudmigrationsaktivitäten hinweg vereinfachen können.

Dieser Ansatz besteht aus zwei Methoden oder Schwerpunktbereichen: Cloudstrategie und -planung und Cloudimplementierung. Die [Beweggründe](#motivations) oder die gewünschten Geschäftsergebnisse für eine Cloudmigration bestimmen oft, wie viel ein Team in die [Strategie und Planung](#cloud-strategy-and-planning) und in die [Implementierung](#cloud-implementation) investieren sollte. Diese Beweggründe können auch die Entscheidungen über die sequentielle oder parallele Ausführung beeinflussen.

## <a name="cloud-implementation"></a>Cloudimplementierung

Die Cloudimplementierung ist ein iterativer Prozess für das Migrieren und Modernisieren der digitalen Ressourcen in Einklang mit den anvisierten Geschäftsergebnissen und Change Management-Mechanismen. Bei jeder Iteration werden Workloads entsprechend der Strategie und Planung migriert oder modernisiert. Entscheidungen in Bezug auf IaaS, PaaS oder eine hybride Infrastruktur werden während der Bewertungsphase getroffen, um die Kontrolle und Ausführung zu optimieren. Diese Entscheidungen bestimmen die Tools, die in der Migrationsphase verwendet werden. Dieses Modell kann mit minimalem Strategie- und Planungsaufwand verwendet werden. Um jedoch die größten Unternehmenserträge zu erzielen, sollten sowohl die IT als auch das Unternehmen unbedingt auf eine klare Strategie und Planung zur Durchführung der Implementierungsaktivitäten ausgerichtet sein.

![Cloudimplementierungsmethodik des Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

Der Fokus liegt hierbei auf der Migration oder Modernisierung von Workloads. Eine Workload ist eine Sammlung von Infrastrukturen, Anwendungen und Daten, die zusammen ein gemeinsames Geschäftsziel oder die Ausführung eines allgemeinen Geschäftsprozesses unterstützen. Beispiele für Workloads sind unter anderem eine Branchenanwendung, eine Lohn- und Gehaltsabrechnungslösung, eine CRM-Lösung, ein Workflow zur Genehmigung von Finanzdokumenten oder eine Business Intelligence-Lösung. Workloads können auch gemeinsam genutzte technische Ressourcen wie ein Data Warehouse umfassen, das mehrere andere Lösungen unterstützt. In einigen Fällen kann eine Workload auch durch eine einzelne Ressource wie einen eigenständigen Server, eine Anwendung oder eine Datenplattform repräsentiert werden.

Cloudmigrationen werden oft als ein einzelnes Projekt innerhalb eines umfassenderen, Programms angesehen, um den IT-Betrieb zu optimieren und die Kosten oder die Komplexität zu reduzieren. Die Cloudimplementierungsmethodik hilft dabei, die technischen Aktivitäten in einer Reihe von Workloadmigrationen auf übergeordnete Unternehmenswerte abzustimmen, die in der Cloudstrategie und dem Cloudplan beschrieben sind.

**Erste Schritte:** Informationen zu den ersten Schritten bei einer Cloudimplementierung finden Sie im [Azure-Migrationsleitfaden](../migrate/azure-migration-guide/index.md) und im [Leitfaden für die Azure-Einrichtung](../ready/azure-setup-guide/index.md). Darin werden die Tools und allgemeinen Prozesse beschrieben, die für eine erfolgreiche Ausführung einer Cloudimplementierung erforderlich sind. Wenn Sie Ihre erste Workload anhand dieser Leitfäden migrieren, hilft dies dem Team, erste Lernkurven bereits frühzeitig im Planungsprozess zu überwinden. Anschließend sollten Sie zusätzlich die [Checkliste für den erweiterten Umfang](../migrate/expanded-scope/index.md), die [bewährten Methoden für die Migration](../migrate/azure-best-practices/index.md) und [Überlegungen zur Migration](../migrate/migration-considerations/index.md) berücksichtigen, um die Basisleitlinien an die individuellen Einschränkungen, Prozesse, Teamstrukturen und Ziele Ihrer Bemühungen anzupassen.

## <a name="cloud-strategy-and-planning"></a>Cloudstrategie und -planung

Die Cloudstrategie und -planung ist eine Methodik, die sich auf die Abstimmung von Geschäftsergebnissen, Prioritäten und Einschränkungen konzentriert, um eine eindeutige Migrationsstrategie und einen klaren Migrationsplan zu entwickeln. Der daraus resultierende Plan (oder Migrationsbacklog) beschreibt den Ansatz für die Migration und Modernisierung des gesamten IT-Portfolios, das ganze Rechenzentren, mehrere Workloads oder verschiedene Sammlungen von Infrastrukturen, Anwendungen und Daten umfassen kann. Die richtige Verwaltung des IT-Portfolios während des gesamten Cloudimplementierungsprozesses trägt dazu bei, die gewünschten Geschäftsergebnisse zu erzielen.

![Übersicht über das Framework für die Cloudeinführung](../_images/caf-overview.png)

**Erste Schritte:** Im weiteren Verlauf dieses Artikels wird der Leser auf die richtige Anwendung der Cloudstrategie- und -planungsmethodik des Cloud Adoption Framework vorbereitet. Außerdem werden zusätzliche Ressourcen und Links aufgeführt, die den Leser beim Verfolgen dieses Ansatzes zur Durchführung der Cloudimplementierungsaktivitäten unterstützen können.

### <a name="methodology-explained"></a>Erläuterung der Methodik

Die Cloudstrategie- und -planungsmethodik des Cloud Adoption Framework basiert auf einem inkrementellen Ansatz für die Cloudimplementierung, der auf flexible Technologiestrategien, kulturelle Reife auf der Grundlage von wachstumsorientierten Denkansätzen und durch Geschäftsergebnisse gesteuerte Strategien ausgerichtet ist. Diese Methodik besteht aus den folgenden allgemeinen Komponenten, mit denen die Implementierung der einzelnen Strategien gesteuert wird.

Wie in der obigen Abbildung dargestellt, richtet dieses Framework strategische Entscheidungen auf eine kleine Anzahl von enthaltenen Prozessen aus, die innerhalb eines iterativen Modells ausgeführt werden. Die Beschreibung erfolgt zwar in einem linearen Dokument, aber es wird erwartet, dass jeder der folgenden Prozesse parallel zu den Iterationen der Cloudimplementierung reift. Mithilfe der Links für jeden Prozess können Sie den Endzustand und die Mittel zur Reifung zum gewünschten Endzustand definieren:

- **[Planen](../strategy/index.md):** Wenn die technische Implementierung auf klare Geschäftsziele ausgerichtet ist, kann der Erfolg über mehrere Cloudimplementierungsaktivitäten hinweg viel einfacher gemessen und ausgerichtet werden, unabhängig von technischen Entscheidungen.
- **[Bereitmachen](../ready/index.md):** Die Vorbereitung von Unternehmen, Kultur, Mitarbeitern und Umgebung auf anstehende Änderungen führt bei allen Aktivitäten zum Erfolg und beschleunigt Implementierungs- und Änderungsprojekte.
- **Übernehmen:** Sicherstellen der ordnungsgemäßen Implementierung der gewünschten Änderungen über alle IT- und Geschäftsprozesse hinweg, um die gewünschten Geschäftsergebnisse zu erzielen.
  - **[Migrieren](../migrate/index.md):** Iterative Ausführung der [Cloudimplementierungsmethodik](#cloud-implementation) unter Einhaltung des getesteten Prozesses zum Bewerten, Migrieren, Optimieren, Sichern und Verwalten, um einen wiederholbaren Prozess zum Migrieren von Workloads zu erstellen.
- **[Ausführen](../operate/index.md):** Definieren Sie ein verwaltbares Betriebsmodell, um die Aktivitäten während und lange nach der Einführung zu steuern.
  - **[Organisation](../organize/index.md):** Richten Sie Mitarbeiter und Teams so aus, dass sie einen reibungslosen Cloudbetrieb und eine problemlose Einführung sicherstellen.
  - **[Steuern](../govern/index.md):** Ausrichten der Unternehmensrichtlinie auf konkrete Risiken, die durch richtlinien-, prozess- und cloudbasierte Governancetools gemindert werden können.
  - **[Verwaltung](../manage/index.md):** Erweitern des IT-Betriebs, um sicherzustellen, dass cloudbasierte Lösungen über sichere und kostengünstige Prozesse mit modernen, primär für die Cloud konzipierten Tools ausgeführt werden können.

Während dieses gesamten Migrationsvorgangs wird dieses Framework verwendet, um Unklarheiten zu beseitigen, Änderungen zu meistern und funktionsübergreifende Teams durch die Realisierung von Geschäftsergebnissen zu führen.

### <a name="common-cultural-changes-resulting-from-adherence-to-this-methodology"></a>Häufige kulturelle Veränderungen, die sich aus der Einhaltung dieser Methodik ergeben

Der Versuch, die gewünschten Geschäftsergebnisse zu erzielen, kann geringfügige Änderungen an der IT-Kultur und bis zu einem gewissen Grad auch an der Unternehmenskultur auslösen. Im Folgenden werden einige häufige kulturelle Veränderungen aufgeführt, die bei diesem Prozess zu beobachten sind:

- Das IT-Team wird sich wahrscheinlich neue Fähigkeiten zur Unterstützung von Workloads in der Cloud aneignen.
- Die Ausführung einer Cloudmigration fördert iterative oder flexible Ansätze.
- Die Einbeziehung von Cloudgovernance inspiriert in der Regel auch DevOps-Ansätze.
- Die Gründung eines Cloudstrategieteams kann zu einer engeren Integration zwischen den Leitern der Geschäftsbereiche und IT-Managern führen.
- Zusammen führen diese Änderungen in der Regel zu einer höheren geschäftlichen und IT-Flexibilität.

Kulturelle Veränderung ist kein Ziel der Cloudmigration oder des Cloud Adoption Framework, aber ein häufiges Ergebnis.
Kulturelle Veränderungen werden nicht direkt geleitet. Stattdessen werden geringfügige Änderungen an der Kultur in die vorgeschlagenen Prozessverbesserungen und Ansätze während der gesamten Leitung eingebettet.

### <a name="common-technical-efforts-associated-with-this-methodology"></a>Häufige technische Aufgaben, die mit dieser Methodik verbunden sind

Bei der Implementierung der Cloudstrategie und des Cloudplans konzentriert sich das IT-Team einen großen Teil seiner Zeit auf die Migration von vorhandenen digitalen Ressourcen in die Cloud. Während dieser Bemühungen werden wie erwartet minimale Codeänderungen vorgenommen, diese können aber oft auf Konfigurationsänderungen beschränkt werden. In vielen Fällen kann eine starke geschäftliche Begründung für die Modernisierung im Rahmen der Cloudmigration erfolgen.

### <a name="common-workload-examples"></a>Beispiele für häufige Workloads

Cloudstrategie und -planung zielen oft auf eine umfassende Sammlung von Workloads und Anwendungen ab. Innerhalb des Portfolios werden allgemeine Anwendungs- oder Workloadtypen in der Regel migriert. Im Folgenden finden Sie einige Beispiele:

- Branchenanwendungen
- Kundenorientierte Anwendungen
- Drittanbieteranwendungen
- Datenanalyseplattformen
- Global verteilte Lösungen
- Hochgradig skalierbare Lösungen

### <a name="common-technologies-migrated"></a>Häufige in die Cloud migrierte Technologien

Die in die Cloud migrierten Technologien werden ständig erweitert, da Clouddienstanbieter neue Funktionen hinzufügen. Im Folgenden finden Sie einige Beispiele für Technologien, die häufig bei Migrationen zum Einsatz kommen:

- Windows und SQL Server
- Linux- und Open-Source-Datenbanken (OSS)
- Unstructure/NoSQL-Datenbanken
- SAP in Azure
- Datenanalyse (Data Warehouse, Data Lake)

## <a name="next-steps-lifecycle-solution"></a>Nächste Schritte: Lebenszykluslösung

Das Cloud Adoption Framework ist eine Lebenszykluslösung. Es soll sowohl Leser unterstützen, die gerade erst mit der Migration begonnen haben, als auch als Leser, die bereits im Migrationsprozess weit fortgeschritten sind. Daher ist der Inhalt sehr kontext- und zielgruppenspezifisch. Die nächsten Schritte sind optimal auf den allgemeinen Prozess ausgerichtet, den der Leser als Nächstes verbessern möchte.

> [!div class="nextstepaction"]
> [Planen](../plan/index.md)
>
> [Bereit](../ready/index.md).
>
> [Migrieren](../migrate/index.md)
>
> [Verwalten](../manage/index.md)
>
> [Steuern](../govern/index.md)
