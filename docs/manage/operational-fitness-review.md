---
title: Einrichten einer Überprüfung der Einsatztauglichkeit
description: Richten Sie einen Prozess zur Überprüfung der Einsatztauglichkeit ein, um sich eingehend mit den Problemen vertraut zu machen, die sich aus der Ausführung von Workloads in einer Produktionsumgebung ergeben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 70bc3bfe59756d78364e7f6b24306d3969907935
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879240"
---
# <a name="establish-an-operational-fitness-review"></a>Einrichten einer Überprüfung der Einsatztauglichkeit

Wenn Ihr Unternehmen damit beginnt, Workloads in Azure auszuführen, besteht der nächste Schritt darin, einen Prozess zur _Überprüfung der Einsatztauglichkeit_ einzurichten. In diesem Prozess werden die _nicht funktionalen_ Anforderungen für diese Workloads aufgelistet, implementiert und iterativ überprüft. Nicht funktionale Anforderungen beziehen sich auf das erwartete betriebliche Verhalten des Diensts.

Es gibt fünf wesentliche Kategorien nicht funktionaler Anforderungen, die als die [Säulen der Architekturexzellenz](/azure/architecture/framework) bezeichnet werden:

- Kostenoptimierung
- Optimaler Betrieb
- Effiziente Leistung
- Zuverlässigkeit
- Sicherheit

Mit einem Prozess zur Überprüfung der Einsatztauglichkeit lässt sich sicherstellen, dass Ihre unternehmenskritischen Workloads den Erwartungen Ihres Unternehmens in Bezug auf die Säulen entsprechen.

Erstellen Sie einen Prozess zur Überprüfung auf Einsatztauglichkeit, um vollständig zu verstehen, welche Probleme sich aus der Ausführung von Workloads in einer Produktionsumgebung ergeben, und wie diese Probleme behoben und gelöst werden können. Dieser Artikel beschreibt eine allgemeine Überprüfung der Einsatztauglichkeit, die Ihr Unternehmen nutzen kann, um dieses Ziel zu erreichen.

## <a name="operational-fitness-at-microsoft"></a>Einsatztauglichkeit bei Microsoft

Seit Beginn sind viele Teams von Microsoft an der Entwicklung der Azure-Plattform beteiligt gewesen. Es ist schwierig, die Qualität und Konsistenz für ein Projekt mit derartiger Größe und Komplexität sicherzustellen. Sie benötigen einen robusten Prozess, um grundlegende nicht funktionale Anforderungen in regelmäßigen Abständen aufzuzählen und zu implementieren.

Die von Microsoft verfolgten Prozesse bilden die Grundlage für die in diesem Artikel beschriebenen Prozesse.

## <a name="understand-the-problem"></a>Verstehen des Problems

Wie in [Erste Schritte: Beschleunigen der Migration](../get-started/migrate.md) erläutert, besteht der erste Schritt bei der digitalen Transformation eines Unternehmens darin, die zu lösenden Geschäftsprobleme durch die Einführung von Azure zu identifizieren. Der nächste Schritt besteht darin, eine allgemeine Lösung für das Problem zu finden, z.B. die Migration eines Workloads in die Cloud oder die Anpassung eines vorhandenen lokalen Dienstes mit Cloudfunktionalität. Schließlich entwerfen und implementieren Sie die Lösung.

Während dieses Vorgangs liegt der Schwerpunkt häufig auf den Features des Dienstanbieters: dem Satz der _funktionalen_ Anforderungen, die vom Dienst ausgeführt werden sollen. Ein Produktlieferdienst benötigt beispielsweise Funktionen zum Bestimmen des Quell- und Zielortes des Produkts, zur Verfolgung des Produkts während der Lieferung und zum Senden von Benachrichtigungen an Kunden.

Im Gegensatz dazu beziehen sich die _nicht funktionalen_ Anforderungen auf Eigenschaften wie die [Verfügbarkeit](/azure/architecture/checklist/availability), [Resilienz](/azure/architecture/resiliency) und [Skalierbarkeit](/azure/architecture/framework/scalability/performance-efficiency) des Diensts. Diese Eigenschaften unterscheiden sich von den funktionalen Anforderungen, da sie die endgültige Funktion eines bestimmten Features im Dienst nicht direkt beeinflussen. Diese nicht funktionalen Anforderungen beziehen sich jedoch auf die Leistung und Kontinuität des Diensts.

Sie können einige nicht funktionale Anforderungen in Form einer Vereinbarung zum Servicelevel (SLA) festlegen. Sie können die Dienstkontinuität beispielsweise als Verfügbarkeit in Prozent ausdrücken: „99,99 % der Zeit verfügbar“. Andere nicht funktionale Anforderungen können schwieriger zu definieren sein und sich mit zunehmendem Produktionsbedarf ändern. So könnte beispielsweise ein verbraucherorientierter Dienst nach einem Popularitätsschub mit unerwarteten Durchsatzanforderungen konfrontiert werden.

> [!NOTE]
> Weitere Informationen zu den Anforderungen an die Resilienz finden Sie unter [Entwerfen zuverlässiger Azure-Anwendungen](/azure/architecture/reliability#define-requirements). Dieser Artikel enthält Erläuterungen zu Konzepten wie RPO (Recovery Point Objective), RTO (Recovery Time Objective) und SLA.

## <a name="process-for-operational-fitness-review"></a>Prozess zur Überprüfung der Einsatztauglichkeit

Der Schlüssel zur Aufrechterhaltung der Leistung und Kontinuität der Dienste eines Unternehmens liegt in der Implementierung eines Prozesses für die Überprüfung der Einsatztauglichkeit.

![Übersicht über den Prozess zur Überprüfung der Einsatztauglichkeit](../_images/manage/ofr-flow.png)

Der Prozess besteht allgemein aus zwei Phasen. In der _Phase der Voraussetzungen_ werden die Anforderungen ermittelt und unterstützenden Diensten zugeordnet. Diese Phase tritt selten auf, vielleicht jährlich oder bei der Einführung neuer Vorgänge. Die Ausgabe der Phase der Voraussetzungen wird in der _Flussphase_ verwendet. Die Flussphase tritt häufiger auf, z. B. monatlich.

### <a name="prerequisites-phase"></a>Phase der Voraussetzungen

Die Schritte in dieser Phase schaffen die Voraussetzungen für eine regelmäßige Überprüfung der wichtigen Dienste.

1. **Identifizieren unternehmenskritischer Geschäftsvorgänge**. Bestimmen Sie Ihre unternehmenskritischen Geschäftsvorgänge. Die Geschäftsvorgänge sind unabhängig von allen unterstützenden Dienstfunktionen. Mit anderen Worten: Geschäftsvorgänge stellen die tatsächlichen Aktivitäten dar, die das Unternehmen ausführen muss, und werden durch eine Reihe von IT-Diensten unterstützt.

    Der Begriff _unternehmenskritisch_ (oder _geschäftskritisch_) gibt an, dass es zu schwerwiegenden Auswirkung für das Unternehmen kommen kann, wenn der Vorgang behindert wird. So kann beispielsweise ein Onlinehändler einen Geschäftsvorgang wie „einem Kunden ermöglichen, einen Artikel in einen Warenkorb zu legen“ oder „eine Kreditkartenzahlung abwickeln“ haben. Wenn bei einem dieser beiden Vorgänge ein Fehler auftritt, kann ein Kunde die Transaktion nicht abschließen, und das Unternehmen kann keinen Umsatz erzielen.

1. **Zuordnen der Vorgänge zu Diensten**. Ordnen Sie diese wichtigen Geschäftsvorgänge den Diensten zu, die sie unterstützen. Im Beispiel des Warenkorbs können mehrere Dienste inklusive eines Bestandsverwaltungs- und Einkaufswagendiensts beteiligt sein. Um eine Kreditkartenzahlung zu verarbeiten, kann ein lokaler Zahlungsdienst mit einem externen Zahlungsabwicklungsdienst interagieren.

1. **Analysieren der Dienstabhängigkeiten**. Die meisten Geschäftsvorgänge erfordern eine Orchestrierung zwischen mehreren unterstützenden Diensten. Es ist wichtig, die Abhängigkeiten zwischen den Diensten und dem Fluss unternehmenskritischer Transaktionen durch diese Dienste zu verstehen.

    Berücksichtigen Sie auch die Abhängigkeiten zwischen lokalen Diensten und Azure-Diensten. Im Beispiel des Warenkorbs kann der Inventarbestands Verwaltungsdienst lokal gehostet werden und Daten erfassen, die von Mitarbeitern in einem physischen Lager eingegeben werden. Es kann jedoch vorkommen, dass Daten nicht lokal in einem Azure-Dienst ([z.B. Azure Storage](/azure/storage/common/storage-introduction)) oder in einer Datenbank ([z.B. Azure Cosmos DB](/azure/cosmos-db/introduction)) gespeichert werden.

Eine Ausgabe aus diesen Aktivitäten ist ein Satz von _Scorecardmetriken_ für Dienstvorgänge. Die Scorecard misst Kriterien wie Verfügbarkeit, Skalierbarkeit und Notfallwiederherstellung. Scorecardmetriken drücken die operativen Kriterien aus, deren Erfüllung Sie vom Dienst erwarten. Diese Metriken können auf jeder Granularitätsstufe ausgedrückt werden, die für den Dienstvorgang geeignet ist.

Die Scorecard sollte in einfachen Worten ausgedrückt werden, um eine sinnvolle Diskussion zwischen den Business Owners und dem Engineering zu erleichtern. Beispielsweise könnte eine Scorecardmetrik für die Skalierbarkeit auf einfache Weise farbcodiert sein. Grün bedeutet die Erfüllung der definierten Kriterien, Gelb die Nichterfüllung der definierten Kriterien, aber aktive Implementierung einer geplanten Korrektur, und Rot die Nichterfüllung der definierten Kriterien ohne Plan oder Maßnahme.

Es ist wichtig zu betonen, dass diese Metriken die Geschäftsanforderungen direkt widerspiegeln sollten.

### <a name="service-review-phase"></a>Phase der Dienstüberprüfung

Die Phase der Dienstüberprüfung ist der Kern des Prozesses der Überprüfung der Einsatztauglichkeit. Sie umfasst die folgenden Schritte:

1. **Messen der Dienstmetriken**. Verwenden Sie die Scorecardmetriken, um die Dienste zu überwachen, und so sicherzustellen, dass die Dienste die geschäftlichen Erwartungen erfüllen. Dienstüberwachung spielt eine wesentliche Rolle. Wenn Sie eine Reihe von Diensten in Bezug auf die nicht funktionalen Anforderungen nicht überwachen können, sollten die entsprechenden Scorecardmetriken als rot betrachtet werden. In diesem Fall ist der erste Schritt zur Korrektur die Implementierung einer entsprechenden Dienstüberwachung. Wenn das Unternehmen beispielsweise erwartet, dass ein Dienst mit einer Verfügbarkeit von 99,99 Prozent arbeitet, aber keine Produktionstelemetrie zur Messung der Verfügbarkeit vorhanden ist, gehen Sie davon aus, dass die Anforderung nicht erfüllt wird.

2. **Planen der Korrekturmaßnahmen**. Bestimmen Sie für jeden Dienstvorgang mit Metriken, die unter einen akzeptablen Schwellenwert fallen, die Kosten für die Korrektur des Diensts, um damit eine akzeptable Ebene zu erreichen. Wenn die Kosten für die Korrektur des Dienstes höher sind als die erwarteten Einnahmen aus dem Dienst, sollten Sie die immateriellen Kosten (etwa die Kundenzufriedenheit) berücksichtigen. Wenn Kunden beispielsweise Schwierigkeiten haben, über den Dienst erfolgreich zu bestellen, könnten sie stattdessen einen Konkurrenten wählen.

3. **Implementieren der Korrekturmaßnahmen**. Nachdem die Geschäftsinhaber und das Engineeringteam sich auf einen Plan geeinigt haben, implementieren Sie ihn. Melden Sie den Status der Implementierung immer, wenn Sie Ihre Scorecardmetriken überprüfen.

Dieser Prozess ist iterativ, und idealerweise verfügt Ihr Unternehmen über ein Team, das für ihn zuständig ist. Dieses Team sollte sich regelmäßig treffen, um bestehende Korrekturprojekte zu überprüfen, die grundlegende Überprüfung neuer Workloads einzuleiten und die gesamte Scorecard des Unternehmens nachzuverfolgen. Das Team sollte befugt sein, die Verantwortlichkeit für Korrekturteams sicherzustellen, die in Verzug sind oder Metriken nicht einhalten.

## <a name="structure-of-the-review-team"></a>Struktur des Überprüfungsteams

Das Team, das für die Überprüfung der Einsatztauglichkeit verantwortlich ist, besteht aus den folgenden Rollen:

- **Geschäftsinhaber**: Diese Rolle stellt Informationen zum Unternehmen bereit, um jeden „unternehmenskritischen“ Geschäftsvorgang zu identifizieren und zu priorisieren. Diese Rolle vergleicht auch die Minderungskosten mit den Auswirkungen auf das Unternehmen und trifft die endgültige Entscheidung zur Korrektur.

- **Business Advocate**: Unterteilt den Geschäftsbetrieb in diskrete Teile und ordnet diese Teile Diensten und Infrastruktur zu, lokal oder in der Cloud. Die Rolle erfordert fundierte Kenntnisse zur Technologie, die mit jedem Geschäftsvorgang verbunden ist.

- **Engineering Owner**: Implementiert die dem Geschäftsvorgang zugeordneten Dienste. Diese Personen können zur Konzeption, Implementierung und Bereitstellung von Lösungen zum Beheben von Problemen mit nicht funktionalen Anforderungen beitragen, die vom Überprüfungsteam festgestellt wurden.

- **Dienstbesitzer**: Betreibt die Anwendungen und Dienste des Unternehmens. Diese Personen sammeln Protokollierungs- und Nutzungsdaten für diese Anwendungen und Dienste. Diese Daten werden verwendet, um Probleme zu identifizieren und Fehlerbehebungen nach ihrer Bereitstellung zu überprüfen.

## <a name="review-meeting"></a>Überprüfungsbesprechung

Wir empfehlen, dass sich Ihr Überprüfungsteam regelmäßig trifft. Beispielsweise könnte sich das Team ein Mal pro Monat treffen und den Status und die Metriken dann vierteljährlich an die Führungskräfte berichten.

Passen Sie die Details des Prozesses und der Besprechung so an, dass sie Ihre spezifischen Bedürfnisse berücksichtigen. Wir empfehlen die folgenden Aufgaben als Ausgangspunkt:

1. Der Business Owner und der Business Advocate bestimmen mit Unterstützung der Engineering und Service Owners die nicht funktionalen Anforderungen für jeden Geschäftsvorgang. Überprüfen und verifizieren Sie die Priorität für zuvor identifizierte Geschäftsvorgänge. Vergeben Sie für neue Geschäftsvorgänge eine Priorität in der bestehenden Liste.

2. Die Engineering und Service Owner ordnen den aktuellen Zustand der Geschäftsvorgänge den entsprechenden lokalen und Clouddiensten zu. Die Zuordnung besteht aus einer Liste der Komponenten in jedem Dienst, die als Abhängigkeitsstruktur dargestellt sind. Engineering- und Dienstbesitzer bestimmen dann die kritischen Pfade durch die Struktur.

3. Die Engineering und Service Owners überprüfen den aktuellen Status der betrieblichen Protokollierung und Überwachung für die im vorherigen Schritt aufgeführten Dienste. Eine zuverlässige Protokollierung und Überwachung ist von entscheidender Bedeutung, um Dienstkomponenten zu identifizieren, die dazu beitragen, dass nicht funktionale Anforderungen nicht erfüllt werden. Wenn es keine ausreichende Protokollierung und Überwachung gibt, muss das Team einen Plan erstellen und implementieren, um sie umzusetzen.

4. Das Team erstellt Scorecardmetriken für neue Geschäftsvorgänge. Die Scorecard besteht aus der Liste der beteiligten Komponenten für jeden in Schritt 2 erkannten Dienst. Sie wird mit den nicht funktionalen Anforderungen in Einklang gebracht und stellt ein Maß dafür dar, wie gut die jeweilige Komponente die Anforderung erfüllt.

5. Für beteiligte Komponenten, die nicht funktionale Anforderungen nicht erfüllen, konzipiert das Team eine allgemeine Lösung und weist sie einem Engineeringbesitzer zu. An dieser Stelle stellen der Business Owner und der Business Advocate ein Budget für die Korrekturmaßnahmen auf, das auf den erwarteten Einnahmen des Geschäftsvorgangs basiert.

6. Schließlich führt das Team eine Überprüfung der laufenden Korrekturmaßnahmen durch. Jede der Scorecardmetriken für laufende Arbeiten wird mit den erwarteten Kriterien verglichen. Für Komponenten, die Metrikkriterien erfüllen, legt der Service Owner Protokollierungs- und Überwachungsdaten vor, um zu bestätigen, dass die Kriterien erfüllt werden. Für beteiligte Komponenten, die nicht den Metrikkriterien entsprechen, erläutert jeder Engineeringbesitzer die Probleme, die die Erfüllung von Kriterien verhindern, und stellt alle neuen Entwürfe für die Korrektur vor.

## <a name="recommended-resources"></a>Empfohlene Ressourcen

- [Microsoft Azure Well-Architected Framework](/azure/architecture/framework): Erfahren Sie mehr über die Grundsätze zum Verbessern der Qualität einer Workload. Das Framework besteht aus fünf Säulen der Architekturexzellenz:
  - Kostenoptimierung
  - Optimaler Betrieb
  - Effiziente Leistung
  - Zuverlässigkeit
  - Sicherheit
- [Zehn Entwurfsprinzipien für Azure-Anwendungen](/azure/architecture/guide/design-principles). Befolgen Sie die folgenden Entwurfsprinzipien, um die Skalierbarkeit, Resilienz und Verwaltbarkeit Ihrer Anwendung zu optimieren.
- [Entwerfen robuster Anwendungen für Azure](/azure/architecture/resiliency). Erstellen und pflegen Sie zuverlässige Systeme mit einem strukturierten Ansatz für die Lebensdauer einer Anwendung – vom Entwurf und der Implementierung über die Bereitstellung bis zum Betrieb.
- [Cloudentwurfsmuster](/azure/architecture/patterns). Verwenden Sie Entwurfsmuster, um Anwendungen anhand der Säulen der Architekturexzellenz zu erstellen.
- [Azure Advisor:](/azure/advisor) Azure Advisor bietet basierend auf Ihrer Nutzung und Ihren Konfigurationen personalisierte Empfehlungen zum Optimieren Ihrer Ressourcen im Hinblick auf Hochverfügbarkeit, Sicherheit, Leistung und Kosten.
