---
title: Einrichten einer Überprüfung der Einsatztauglichkeit
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Leitfaden zu betrieblichen Grundlagen
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/20/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 04afedc133d001405c5042b309a45c9b41f3268e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031856"
---
# <a name="establish-an-operational-fitness-review"></a>Einrichten einer Überprüfung der Einsatztauglichkeit

Wenn Ihr Unternehmen damit beginnt, Workloads in Azure auszuführen, besteht der nächste Schritt darin, einen Prozess zur *Überprüfung der Einsatztauglichkeit* einzurichten. In diesem Prozess werden die *nicht funktionalen* Anforderungen für diese Workloads aufgelistet, implementiert und iterativ überprüft. Nicht funktionale Anforderungen beziehen sich auf das erwartete betriebliche Verhalten des Diensts.

Es gibt fünf wesentliche Kategorien nicht funktionaler Anforderungen, die als [Säulen der Softwarequalität](https://docs.microsoft.com/azure/architecture/guide/pillars) bezeichnet werden:

- Skalierbarkeit
- Verfügbarkeit
- Resilienz, einschließlich Business Continuity und Disaster Recovery (BCDR)
- Verwaltung
- Sicherheit

Mit einem Prozess zur Überprüfung der Einsatztauglichkeit lässt sich sicherstellen, dass Ihre unternehmenskritischen Workloads den Erwartungen Ihres Unternehmens in Bezug auf die Qualitätssäulen entsprechen.

Ihr Unternehmen sollte diese Überprüfung auf Einsatztauglichkeit durchführen, um die Probleme, die sich aus der Ausführung des Workloads in einer Produktionsumgebung ergeben, vollständig zu verstehen, festzustellen, wie die Probleme behoben werden können, und sie dann lösen. Dieser Artikel beschreibt eine allgemeine Überprüfung der Einsatztauglichkeit, die Ihr Unternehmen nutzen kann, um dieses Ziel zu erreichen.

## <a name="operational-fitness-at-microsoft"></a>Einsatztauglichkeit bei Microsoft

Von Anfang an war die Entwicklung der Azure-Plattform ein kontinuierliches Projekt, das von vielen Teams bei Microsoft durchgeführt wurde. Es ist schwierig, die Qualität und Konsistenz für ein Projekt mit derartiger Größe und Komplexität sicherzustellen. Ein robuster Prozess ist erforderlich, um grundlegende nicht funktionale Anforderungen in regelmäßigen Abständen aufzuzählen und zu implementieren.

Die von Microsoft verfolgten Prozesse bilden die Grundlage für die in diesem Artikel beschriebenen Prozesse.

## <a name="understand-the-problem"></a>Verstehen des Problems

Wie Sie in [Erste Schritte](../getting-started/migrate.md) gesehen haben, besteht der erste Schritt bei der digitalen Transformation eines Unternehmens darin, die zu lösenden Geschäftsprobleme durch die Einführung von Azure zu identifizieren. Der nächste Schritt besteht darin, eine allgemeine Lösung für das Problem zu finden, z.B. die Migration eines Workloads in die Cloud oder die Anpassung eines vorhandenen lokalen Dienstes mit Cloudfunktionalität. Schließlich wird die Lösung entworfen und implementiert.

Während dieses Vorgangs liegt der Schwerpunkt häufig auf den Features des Dienstanbieters: dem Satz der _funktionalen_ Anforderungen, die vom Dienst ausgeführt werden sollen. Ein Produktlieferdienst benötigt beispielsweise Funktionen zum Bestimmen des Quell- und Zielortes des Produkts, zur Verfolgung des Produkts während der Lieferung, zur Benachrichtigung von Kunden und dergleichen.

Im Gegensatz dazu beziehen sich die _nicht funktionalen_ Anforderungen auf Eigenschaften wie die [Verfügbarkeit](https://docs.microsoft.com/azure/architecture/checklist/availability), [Resilienz](https://docs.microsoft.com/azure/architecture/resiliency) und [Skalierbarkeit](https://docs.microsoft.com/azure/architecture/checklist/scalability) des Diensts. Diese Eigenschaften unterscheiden sich von den funktionalen Anforderungen, da sie die endgültige Funktion eines bestimmten Features im Dienst nicht direkt beeinflussen. Diese nicht funktionalen Anforderungen beziehen sich jedoch auf die Leistung und Kontinuität des Diensts.

Einige nicht funktionale Anforderungen können in Form einer Vereinbarung zum Servicelevel (SLA) festgelegt werden. Im Hinblick auf die Dienstkontinuität kann beispielsweise eine Verfügbarkeitsanforderung für den Dienst als Prozentsatz ausgedrückt werden: „99,99 % der Zeit verfügbar“. Andere nicht funktionale Anforderungen können schwieriger zu definieren sein und sich mit zunehmendem Produktionsbedarf ändern. So könnte beispielsweise ein verbraucherorientierter Dienst nach einem Popularitätsschub mit unerwarteten Durchsatzanforderungen konfrontiert werden.

> [!NOTE]
> Die Anforderungen für Resilienz werden unter [Entwerfen zuverlässiger Azure-Anwendungen](https://docs.microsoft.com/azure/architecture/reliability#define-requirements) ausführlicher erläutert. Dieser Artikel enthält Erläuterungen zu Konzepten wie RPO (Recovery Point Objective), RTO (Recovery Time Objective), SLA und anderen.

## <a name="process-for-operational-fitness-review"></a>Prozess zur Überprüfung der Einsatztauglichkeit

Der Schlüssel zur Aufrechterhaltung der Leistung und Kontinuität der Dienste eines Unternehmens liegt in der Implementierung eines Prozesses für die Überprüfung der Einsatztauglichkeit.

![Übersicht über den Prozess zur Überprüfung der Einsatztauglichkeit](../_images/manage/ofr-flow.png)

Der Prozess besteht allgemein aus zwei Phasen. In der *Phase der Voraussetzungen* werden die Anforderungen ermittelt und unterstützenden Diensten zugeordnet. Diese Phase tritt selten auf, vielleicht jährlich oder bei der Einführung neuer Vorgänge. Die Ausgabe der Phase der Voraussetzungen wird in der *Flussphase* verwendet. Die Flussphase tritt häufiger auf. Wir empfehlen, sie monatlich durchzuführen.

### <a name="prerequisites-phase"></a>Phase der Voraussetzungen

Die Schritte in dieser Phase schaffen die Voraussetzungen für eine regelmäßige Überprüfung der wichtigen Dienste.

1. **Identifizieren unternehmenskritischer Geschäftsvorgänge**. Bestimmen Sie Ihre unternehmenskritischen Geschäftsvorgänge. Die Geschäftsvorgänge sind unabhängig von allen unterstützenden Dienstfunktionen. Mit anderen Worten: Geschäftsvorgänge stellen die tatsächlichen Aktivitäten dar, die das Unternehmen ausführen muss, und werden durch eine Reihe von IT-Diensten unterstützt.

    Der Begriff *unternehmenskritisch* (oder *geschäftskritisch*) gibt an, dass es zu schwerwiegenden Auswirkung für das Unternehmen kommen kann, wenn der Vorgang behindert wird. So kann beispielsweise ein Onlinehändler einen Geschäftsvorgang wie „einem Kunden ermöglichen, einen Artikel in einen Warenkorb zu legen“ oder „eine Kreditkartenzahlung abwickeln“ haben. Wenn bei einem dieser beiden Vorgänge ein Fehler auftritt, kann ein Kunde die Transaktion nicht abschließen, und das Unternehmen kann keinen Umsatz erzielen.

1. **Zuordnen der Vorgänge zu Diensten**. Ordnen Sie diese wichtigen Geschäftsvorgänge den Diensten zu, die sie unterstützen. Im Beispiel des Warenkorbs können mehrere Dienste beteiligt sein: ein Bestandsverwaltungsdienst, ein Einkaufswagendienst usw. Um eine Kreditkartenzahlung zu verarbeiten, kann ein lokaler Zahlungsdienst mit einem externen Zahlungsabwicklungsdienst interagieren.

1. **Analysieren der Dienstabhängigkeiten**. Die meisten Geschäftsvorgänge erfordern eine Orchestrierung zwischen mehreren unterstützenden Diensten. Es ist wichtig, die Abhängigkeiten zwischen den Diensten und dem Fluss unternehmenskritischer Transaktionen durch diese Dienste zu verstehen.

    Berücksichtigen Sie auch die Abhängigkeiten zwischen lokalen Diensten und Azure-Diensten. Im Beispiel des Warenkorbs kann der Inventarbestands Verwaltungsdienst lokal gehostet werden und Daten erfassen, die von Mitarbeitern in einem physischen Lager eingegeben werden. Es kann jedoch vorkommen, dass Daten nicht lokal in einem Azure-Dienst ([z.B. Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction)) oder in einer Datenbank ([z.B. Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)) gespeichert werden.

Eine Ausgabe aus diesen Aktivitäten ist ein Satz von *Scorecardmetriken* für Dienstvorgänge. Die Metriken werden nach nicht funktionalen Kriterien wie Verfügbarkeit, Skalierbarkeit und Notfallwiederherstellung kategorisiert. Scorecardmetriken drücken die operativen Kriterien aus, die der Dienst voraussichtlich erfüllen wird. Diese Metriken können auf jeder Granularitätsstufe ausgedrückt werden, die für den Dienstvorgang geeignet ist.

Die Scorecard sollte in einfachen Worten ausgedrückt werden, um eine sinnvolle Diskussion zwischen den Business Owners und dem Engineering zu erleichtern. So könnte beispielsweise eine Scorecardmetrik für die Skalierbarkeit wie folgt ausgedrückt werden: Grün für die Erfüllung der definierten Kriterien, Gelb für die Nichterfüllung der definierten Kriterien, aber geplante Korrekturen werden aktiv implementiert, und Rot für die Nichterfüllung der definierten Kriterien ohne Plan oder Maßnahme.

Es ist wichtig zu betonen, dass diese Metriken die Geschäftsanforderungen direkt widerspiegeln sollten.

### <a name="service-review-phase"></a>Phase der Dienstüberprüfung

Die Phase der Dienstüberprüfung ist der Kern des Prozesses der Überprüfung der Einsatztauglichkeit. Sie umfasst die folgenden Schritte:

1. **Messen der Dienstmetriken**. Verwenden Sie die Scorecardmetriken, um die Dienste zu überwachen, und so sicherzustellen, dass die Dienste die geschäftlichen Erwartungen erfüllen. Mit anderen Worten, die Dienstüberwachung spielt eine wesentliche Rolle. Wenn Sie eine Reihe von Diensten in Bezug auf die nicht funktionalen Anforderungen nicht überwachen können, sollten die entsprechenden Scorecardmetriken als rot betrachtet werden. In diesem Fall ist der erste Schritt zur Korrektur die Implementierung einer entsprechenden Dienstüberwachung. Wenn das Unternehmen beispielsweise erwartet, dass ein Dienst mit einer Verfügbarkeit von 99,99 % arbeitet, aber keine Produktionstelemetrie zur Messung der Verfügbarkeit vorhanden ist, gehen Sie davon aus, dass die Anforderung nicht erfüllt werden.

2. **Planen der Korrekturmaßnahmen**. Bestimmen Sie für jeden Dienstvorgang mit Metriken, die unter einen akzeptablen Schwellenwert fallen, die Kosten für die Korrektur des Diensts, um damit eine akzeptable Ebene zu erreichen. Wenn die Kosten für die Korrektur des Dienstes höher sind als die erwarteten Einnahmen aus dem Dienst, sollten Sie die immateriellen Kosten (etwa die Kundenzufriedenheit) berücksichtigen. Wenn Kunden beispielsweise Schwierigkeiten haben, über den Dienst erfolgreich zu bestellen, könnten sie stattdessen einen Konkurrenten wählen.

3. **Implementieren der Korrekturmaßnahmen**. Nachdem die Geschäftsinhaber und das Engineering sich auf einen Plan geeinigt haben, implementieren Sie diesen. Melden Sie den Status der-Implementierung immer, wenn Sie Ihre Scorecardmetriken überprüfen.

Dieser Prozess ist iterativ, und idealerweise verfügt Ihr Unternehmen über ein Team, das für ihn zuständig ist. Dieses Team sollte sich regelmäßig treffen, um bestehende Korrekturprojekte zu überprüfen, die grundlegende Überprüfung neuer Workloads einzuleiten und die gesamte Scorecard des Unternehmens nachzuverfolgen. Das Team sollte befugt sein, die Verantwortlichkeit für Korrekturteams sicherzustellen, die in Verzug sind oder Metriken nicht einhalten.

## <a name="structure-of-the-review-team"></a>Struktur des Überprüfungsteams

Das Team, das für die Überprüfung der Einsatztauglichkeit verantwortlich ist, besteht aus den folgenden Rollen:

- **Geschäftsinhaber**: Diese Rolle stellt Informationen zum Unternehmen bereit, um jeden „unternehmenskritischen“ Geschäftsvorgang zu identifizieren und zu priorisieren. Diese Rolle vergleicht auch die Minderungskosten mit den Auswirkungen auf das Unternehmen und trifft die endgültige Entscheidung zur Korrektur.

- **Business Advocate**: Unterteilt den Geschäftsbetrieb in diskrete Teile und ordnet diese Teile Diensten und Infrastruktur zu, sei es lokal oder in der Cloud. Die Rolle erfordert fundierte Kenntnisse zur Technologie, die mit jedem Geschäftsvorgang verbunden ist.

- **Engineering Owner**: Implementiert die dem Geschäftsvorgang zugeordneten Dienste. Diese Personen können zur Konzeption, Implementierung und Bereitstellung von Lösungen zum Beheben von Problemen mit nicht funktionalen Anforderungen beitragen, die vom Überprüfungsteam festgestellt wurden.

- **Service Owner**. Betreibt die Anwendungen und Dienste des Unternehmens. Diese Personen sammeln Protokollierungs- und Nutzungsdaten für diese Anwendungen und Dienste. Diese Daten werden verwendet, um Probleme zu identifizieren und Fehlerbehebungen nach ihrer Bereitstellung zu überprüfen.

## <a name="review-meeting"></a>Überprüfungsbesprechung

Wir empfehlen, dass sich Ihr Überprüfungsteam regelmäßig trifft. Beispielsweise könnte sich das Team ein Mal pro Monat treffen und den Status und die Metriken dann vierteljährlich an die Führungskräfte berichten.

Passen Sie die Details des Prozesses und der Besprechung so an, dass sie Ihre spezifischen Bedürfnisse berücksichtigen. Wir empfehlen die folgenden Aufgaben als Ausgangspunkt:

1. Der Business Owner und der Business Advocate bestimmen mit Unterstützung der Engineering und Service Owners die nicht funktionalen Anforderungen für jeden Geschäftsvorgang. Für zuvor identifizierte Geschäftsvorgänge wird die Priorität überprüft und verifiziert. Für neue Geschäftsvorgänge wird eine Priorität in der vorhandenen Liste zugewiesen.

2. Die Engineering und Service Owner ordnen den aktuellen Zustand der Geschäftsvorgänge den entsprechenden lokalen und Clouddiensten zu. Die Zuordnung besteht aus einer Liste der Komponenten in jedem Dienst, die als Abhängigkeitsstruktur dargestellt sind. Nachdem die Listen und die Abhängigkeitsstruktur erstellt wurden, werden die kritischen Pfade anhand der Struktur bestimmt.

3. Die Engineering und Service Owners überprüfen den aktuellen Status der betrieblichen Protokollierung und Überwachung für die im vorherigen Schritt aufgeführten Dienste. Eine zuverlässige Protokollierung und Überwachung ist von entscheidender Bedeutung, um Dienstkomponenten zu identifizieren, die dazu beitragen, dass nicht funktionale Anforderungen nicht erfüllt werden. Wenn es keine ausreichende Protokollierung und Überwachung gibt, muss ein Plan erstellt und implementiert werden, um sie umzusetzen.

4. Für neue Geschäftsvorgänge werden Scorecardmetriken erstellt. Die Scorecard besteht aus der Liste der beteiligten Komponenten für jeden in Schritt 2 erkannten Dienst. Sie wird mit den nicht funktionalen Anforderungen in Einklang gebracht und stellt ein Maß dafür dar, wie gut die jeweilige Komponente die Anforderung erfüllt.

5. Für beteiligte Komponenten, die die nicht funktionalen Anforderungen nicht erfüllen, wird eine allgemeine Lösung konzipiert und ein Engineering Owner zugewiesen. An dieser Stelle stellen der Business Owner und der Business Advocate ein Budget für die Korrekturmaßnahmen auf, das auf den erwarteten Einnahmen des Geschäftsvorgangs basiert.

6. Schließlich erfolgt eine Überprüfung der laufenden Korrekturmaßnahmen. Jede der Scorecardmetriken für laufende Arbeiten wird mit den erwarteten Kriterien verglichen. Für Komponenten, die Metrikkriterien erfüllen, legt der Service Owner Protokollierungs- und Überwachungsdaten vor, um zu bestätigen, dass die Kriterien erfüllt werden. Für die Komponenten, die nicht den Metrikkriterien entsprechen, erläutert jeder Engineering Owner die Probleme, die das Erreichen von Kriterien verhindern, und stellt alle neuen Entwürfe für die Korrektur vor.

## <a name="recommended-resources"></a>Empfohlene Ressourcen

- [Säulen der Softwarequalität](https://docs.microsoft.com/azure/architecture/guide/pillars).
    Dieser Abschnitt des Architekturleitfadens für Azure-Anwendungen beschreibt die fünf Säulen der Softwarequalität: Skalierbarkeit, Verfügbarkeit, Resilienz, Verwaltung und Sicherheit.
- [Zehn Entwurfsprinzipien für Azure-Anwendungen](https://docs.microsoft.com/azure/architecture/guide/design-principles).
    Dieser Abschnitt des Architekturleitfadens für Azure-Anwendungen beschreibt eine Reihe von Entwurfsprinzipien, um Ihre Anwendung skalierbarer, belastbarer und verwaltbarer zu machen.
- [Entwerfen robuster Anwendungen für Azure](https://docs.microsoft.com/azure/architecture/resiliency).
    In diesem Leitfaden werden der Begriff _Resilienz_ und die dazugehörigen Konzepte definiert. Anschließend wird der Prozess zur Erreichung von Resilienz beschrieben. Hierzu wird ein strukturierter Ansatz für die Lebensdauer einer Anwendung verwendet – vom Entwurf und der Implementierung über die Bereitstellung bis zum Betrieb.
- [Cloudentwurfsmuster](https://docs.microsoft.com/azure/architecture/patterns).
    Diese Entwurfsmuster unterstützen Engineeringteams, wenn sie Anwendungen basierend auf den Säulen der Softwarequalität erstellen.
