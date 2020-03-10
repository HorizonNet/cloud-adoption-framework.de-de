---
title: Ausgewogenheit des Portfolios
description: Entdecken Sie Strategien dazu, wie Sie Migration, Innovation und Experimentieren so in Einklang bringen, dass die Cloudmigration optimal genutzt wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b41a550583628c1246a0663c99509498f0786d70
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228593"
---
<!-- cSpell:ignore CSAT -->

# <a name="balance-the-portfolio"></a>Ausgewogenheit des Portfolios

Die Cloudeinführung ist ein Portfolioverwaltungsaufwand, der sich raffiniert als technische Implementierung tarnt. Wie bei jeder Form der Portfolioverwaltung ist die Ausgewogenheit des Portfolios von entscheidender Bedeutung. Auf strategischer Ebene bedeutet dies, Migration, Innovation und Experimentieren so in Einklang zu bringen, dass die Cloud optimal genutzt wird. Wenn der Aufwand zur Cloudeinführung zu weit in die eine oder andere Richtung tendiert, schleicht sich die Komplexität in die Migrationsaktivitäten ein. Dieser Artikel führt den Leser durch Methoden, mit denen die Ausgewogenheit des Portfolios erzielt wird.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Die Ausgewogenheit des Portfolios ist ein strategischer Aspekt. Daher ist der in diesem Artikel vorgestellte Ansatz gleichermaßen strategisch. Um die Strategie auf datengesteuerte Entscheidungen zu gründen, wird in diesem Artikel vorausgesetzt, dass der Leser die vorhandenen [digitalen Ressourcen](../digital-estate/index.md) ausgewertet hat (oder die Auswertung gerade durchführt). Das Ziel dieses Ansatzes ist, die Evaluierung der Workloads zu unterstützen, um die Ausgewogenheit des Portfolios durch qualitative Fragen und Portfoliooptimierung sicherzustellen.

### <a name="document-business-outcomes"></a>Dokumentieren von Geschäftsergebnissen

Bevor die Ausgewogenheit des Portfolios hergestellt wird, müssen die Geschäftsergebnisse, die den Cloudmigrationsaufwand bestimmen, dokumentiert und freigegeben werden. Einige Beispiele für allgemeine Geschäftsergebnisse im Zusammenhang mit Cloudmigrationen finden Sie unter [Erste Schritte auf dem Weg zur Cloudmigration](../getting-started/migrate.md).

Die folgende Tabelle soll das Dokumentieren und Freigeben von Geschäftsergebnissen unterstützen. Es ist wichtig zu beachten, dass die meisten Unternehmen mehrere Ergebnisse gleichzeitig verfolgen. Ziel dieser Übung ist, die Ergebnisse zu verdeutlichen, die unmittelbar mit dem Cloudmigrationsaufwand in Zusammenhang stehen:

|Ergebnis  |Gemessen an  |Zielsetzung  |Zeitrahmen  |Priorität für diesen Aufwand  |
|---------|---------|---------|---------|---------|
|Reduzieren der IT-Kosten     |Rechenzentrumsbudget         |Reduzieren um 2 M USD         |12 Monate         |1         |
|Ausstieg aus Rechenzentrum     |Ausstieg aus Rechenzentren         |2 Rechenzentren         |6 Monate         |2         |
|Erhöhen der Unternehmensflexibilität     |Verbessern der Markteinführungszeit  |Reduzieren der Bereitstellungszeit um sechs Monate         |2 Jahre         |3        |
|Verbessern der Benutzerfreundlichkeit     |Kundenzufriedenheit (CSAT)         |Verbesserung um 10%         |12 Monate         |4         |

> [!IMPORTANT]
> Die oben stehende Tabelle ist ein fiktives Beispiel und sollte nicht verwendet werden, um Prioritäten festlegen. In vielen Fällen könnte diese Tabelle als Antimuster betrachtet werden, da Kosteneinsparungen Priorität vor Kundenfreundlichkeit haben.

Die obige Tabelle könnte genau die Prioritäten des Cloudstrategieteams und des Cloudeinführungsteams darstellen, die eine Migration zur Cloud überwachen. Aufgrund kurzfristiger Einschränkungen legen diese Teams mehr Wert auf Reduzierung der IT-Kosten und Priorisieren eines Rechenzentrumsausstiegs als Mittel zum Erzielen der gewünschten Reduzierung der IT-Kosten. Allerdings versetzt das Dokumentieren der konkurrierenden Prioritäten in dieser Tabelle das Cloudeinführungsteam in die Lage, dem Cloudstrategieteam beim Identifizieren von Möglichkeiten zur besseren Ausrichtung der Implementierung der allumfassenden Portfoliostrategie zu helfen.

### <a name="move-fast-while-maintaining-balance"></a>Schnelles Voranschreiten bei Wahrung der Ausgewogenheit

Die Anleitung in Bezug auf [inkrementelle Rationalisierung der digitalen Ressourcen](../digital-estate/index.md) enthält einen Ansatz, in dem die Rationalisierung mit einer unausgeglichenen Position beginnt. Das Cloudstrategieteam sollte jede Workload auf die Kompatibilität mit einem Ansatz zum Zuweisen eines neuen Hosts hin auswerten. Dieser Ansatz wird empfohlen, da er die schnelle Auswertung einer komplexen digitalen Ressource auf Basis quantitativer Daten ermöglicht. Eine solche anfängliche Annahme ermöglicht dem Cloudeinführungsteam, schnell zu handeln und so die Zeit bis zum Erzielen der Geschäftsergebnisse zu reduzieren. Jedoch sorgen qualitative Fragen, wie in diesem Artikel erwähnt, für die notwendige Ausgewogenheit des Portfolios. Dieser Artikel beschreibt den Prozess zum Schaffen der versprochenen Ausgewogenheit.

### <a name="importance-of-sunset-and-retire-decisions"></a>Wichtigkeit von Entscheidungen zum Außerkraftsetzen

In der Tabelle im obigen Abschnitt [Dokumentieren von Geschäftsergebnissen](#document-business-outcomes) fehlt ein entscheidendes Ergebnis, das das höchste Ziel der IT-Kostenreduzierung unterstützen würde. Wenn die IT-Kostenreduzierung an einer beliebigen Stelle in der Liste der Geschäftsergebnisse rangiert, ist es wichtig, das Potenzial der Außerkraftsetzung oder Deaktivierung von Workloads zu berücksichtigen. In einigen Szenarien können Kosteneinsparungen erzielt werden, indem Workloads, die keine kurzfristige Rendite garantieren, NICHT migriert werden. Einige Kunden berichteten von Kosteneinsparungen, die mehr als 20% der Kostenreduzierungen insgesamt ausmachen, durch Außerkraftsetzung von nicht ausgelasteten Workloads.

Im Interesse eines ausgewogenen Portfolios und um Entscheidungen zur Außerkraftsetzung und Deaktivierung besser widerzuspiegeln, werden das Cloudstrategieteam und das Cloudeinführungsteam aufgefordert, zu jeder Workload im Bewertungs- und Migrationsprozess folgende Fragen zu stellen:

- Wurde die Workload in den letzten sechs Monaten von Endbenutzern verwendet?
- Ist der Endbenutzer-Datenverkehr konsistent, oder wächst er?
- Wird diese Workload von jetzt an 12 Monate vom Unternehmen benötigt?

Wenn die Antwort auf eine dieser Fragen „Nein“ ist, kann die Workload ein Kandidat für die Deaktivierung werden. Wenn das Deaktivierungspotenzial vom App-Besitzer bestätigt wird, ist es wohl nicht sinnvoll, die Workload zu migrieren. Hier kommen ein paar Qualifizierungsfragen auf:

- Kann ein Deaktivierungs- oder Außerkraftsetzungsplan für diese Workload eingerichtet werden?
- Kann diese Workload vor dem Rechenzentrumsausstieg außer Betrieb gesetzt werden?

Wenn die Antwort auf beide Fragen „Ja“ lautet, wäre es klug zu erwägen, diese Workload _nicht_ zu migrieren. Dieser Ansatz wäre hilfreich, die Ziele der Kostenreduzierung und des Rechenzentrumsausstiegs zu erfüllen.

Wenn die Antwort auf eine dieser Fragen „Nein“ ist, kann es ratsam sein, einen Plan zu erstellen, wie die Workload gehostet werden kann, bis sie außer Kraft gesetzt werden kann. Dieser Plan könnte das Verschieben der Ressourcen in ein kostengünstigeres oder alternatives Rechenzentrum beinhalten, was auch den Zielen der Kostenreduzierung und des Ausstiegs aus einem Rechenzentrum entsprechen würde.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Die im Baselineleitfaden angegebenen Voraussetzungen sollten immer noch für die Behandlung dieses komplexen Themas ausreichen. Allerdings sollten Ressourcenbestand und digitale Ressourcen unter diesen Voraussetzungen hervorgehoben werden, da diese Daten die folgenden Aktivitäten bestimmen.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Die Ausgewogenheit des Portfolios erfordert eine zusätzliche qualitative Analyse während des Bewertungsprozesses, was die einfache Portfoliorationalisierung unterstützt.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

Anhand der Daten aus der Tabelle im obigen Abschnitt [Dokumentieren von Geschäftsergebnissen](#document-business-outcomes) besteht ein gewisses Risiko, dass das Portfolio zu weit zu einem migrationsfokussierten Ausführungsmodell tendiert. Wenn Benutzerfreundlichkeit oberste Priorität ist, wäre ein innovationslastiges Portfolio wahrscheinlicher. Keines von beiden ist falsch oder richtig, aber eine zu ausgeprägte Tendenz in eine Richtung führt in der Regel zu einer abnehmenden Rendite, unnötiger Steigerung der Komplexität und verlängert die Ausführungszeit relativ zum Cloudeinführungsaufwand.

Um die Komplexität zu reduzieren, sollten Sie einen herkömmlichen Ansatz zur Portfoliorationalisierung verfolgen, aber in einem iterativen Modell. Die folgenden Schritte skizzieren ein qualitatives Modell für einen solchen Ansatz:

- Das Cloudstrategieteam behält ein priorisiertes Backlog zu migrierender Workloads bei.
- Das Cloudstrategieteam und das Cloudeinführungsteam halten vor dem Abschluss jeder Freigabe eine Freigabeplanungsbesprechung ab.
- In der Freigabeplanungsbesprechung einigen sich die Teams auf die obersten 5 bis 10 Workloads im priorisierten Backlog.
- Außerhalb der Freigabeplanungsbesprechung stellt das Cloudeinführungsteam Anwendungsbesitzern und fachlichen Ansprechpartnern die folgenden Fragen:
  - Könnte diese Anwendung mit einem Platform-as-a-Service-Äquivalent (PaaS) ersetzt werden?
  - Ist diese Anwendung eine Drittanbieteranwendung?
  - Wurde das Budget genehmigt, um in den nächsten 12 Monaten in die fortlaufende Entwicklung der Anwendung zu investieren?
  - Würde eine weitere Entwicklung dieser Anwendung die Benutzerfreundlichkeit verbessern? Stellt sie ein Differenzierungsmerkmal im Wettbewerb dar? Bringt sie dem Unternehmen zusätzlichen Umsatz?
  - Tragen die Daten innerhalb dieser Workload zu einer Downstreaminnovation im Zusammenhang mit BI, Machine Learning, IoT oder verwandten Technologien bei?
  - Ist die Workload mit modernen Anwendungsplattformen wie Azure App Service kompatibel?
- Die Antworten auf die oben genannten Fragen und beliebige andere erforderliche qualitativen Analysen würden sich dann auf Anpassungen des priorisierten Backlogs auswirken. Diese Anpassungen können Folgendes umfassen:
  - Wenn eine Workload mit einer PaaS-Lösung ersetzt werden könnte, könnte sie vollständig aus dem Migrationsbacklog entfernt werden. Mindestens würde eine zusätzliche Sorgfaltspflicht, zwischen Zuweisen eines neuen Hosts und Ersetzen zu entscheiden, als Aufgabe hinzugefügt, die vorübergehend die Priorität der Workload im Migrationsbacklog verringern würde.
  - Wenn eine Workload einer Entwicklungsverbesserung unterzogen wird (oder werden sollte), passt sie am besten in ein Umgestaltungs-/Überarbeitungs-/Neuerstellungsmodell. Da Innovation und Migration unterschiedliche technische Fähigkeiten erfordern, sollten Anwendungen, die einem Umgestaltungs-/Überarbeitungs-/Neuerstellungsansatz entsprechen, über ein Innovationsbacklog statt über ein Migrationsbacklog verwaltet werden.
  - Wenn eine Workload Teil einer Downstreaminnovation ist, kann es sinnvoll sein, die Datenplattform umzugestalten, aber die Anwendungsschichten als Kandidaten für das Zuweisen eines neuen Hosts zu belassen. Eine geringfügige Umgestaltung der Datenplattform einer Workload kann oft in einem Migrations- oder Innovationsbacklog behandelt werden. Dieses Rationalisierungsergebnis kann zu detaillierteren Arbeitselementen im Backlog führen, aber ansonsten keine Prioritäten ändern.
  - Wenn eine Workload nicht strategisch, aber mit modernen, cloudbasierten Anwendungshostingplattformen kompatibel ist, kann es möglicherweise besser sein, eine geringfügige Umgestaltung der Anwendung durchzuführen, um sie als moderne App bereitzustellen. Dies kann durch Verringern der gesamten IaaS- und BS-Lizenzierungsanforderungen der Migration zur Cloud zu den gesamten Einsparungen beitragen.
  - Wenn eine Workload eine Drittanbieteranwendung ist und die Daten dieser Workload nicht für die Verwendung in einer Downstreaminnovation eingeplant sind, kann es das Beste sein, sie als Option zum Zuweisen eines neuen Hosts im Backlog zu belassen.

Die für die einzelnen Workloads durchgeführten qualitativen Analysen sollten sich nicht auf diese Fragen beschränken, sind jedoch wegweisend für eine Konversation, die das Behandeln der Komplexität eines nicht ausgewogenen Portfolios betrifft.

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Während der Migration können Aktivitäten zum Herstellen der Ausgewogenheit des Portfolios sich negativ auf die Geschwindigkeit der Migration auswirken (die Geschwindigkeit, mit der Ressourcen migriert werden). Die folgende Anleitung behandelt, warum Aktivitäten in einer bestimmten Weise ausgerichtet werden sollten, um Unterbrechungen der Migrationsaktivitäten zu vermeiden.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

Portfoliorationalisierung erfordert vielfältigen technischen Aufwand. Es ist verlockend für Cloudeinführungsteams, dieser Portfoliovielfalt in Migrationsaktivitäten zu entsprechen. Unternehmensteilhaber fordern oft, dass ein einzelnes Cloudeinführungsteam das gesamte Migrationsbacklog behandelt. Das ist nur selten ein empfehlenswerter Ansatz, in vielen Fällen kann dies sogar kontraproduktiv sein.

Diese unterschiedlichen Aktivitäten sollten auf zwei oder mehr Cloudeinführungsteams aufgeteilt werden. In einem Modell mit zwei Teams als Ausführungsbeispiel ist Team 1 das Migrationsteam und Team 2 das Innovationsteam. Für größere Aktivitäten könnten diese Teams weiter segmentiert werden, um andere Ansätze wie Ersetzungs-/PaaS-Aktivitäten oder geringfügige Umgestaltung zu behandeln. Im Folgenden werden die erforderlichen Fähigkeiten und Rollen zum Zuweisen eines neuen Hosts, zur Umgestaltung oder geringfügigen Umgestaltung skizziert:

**Zuweisen eines neuen Hosts:** Zum Zuweisen eines neuen Hosts müssen Teammitglieder infrastrukturkonzentrierte Änderungen implementieren. In der Regel werden mithilfe eines Tools wie Azure Site Recovery VMs oder andere Ressourcen zu Azure migriert. Für diese Arbeit sind Rechenzentrumsadministratoren oder IT-Implementierer gut geeignet. Das Cloudmigrationsteam ist so gut strukturiert, dass es diese Aufgabe auf hohem Niveau ausführt. Dies ist in den meisten Szenarien der schnellste Ansatz zum Migrieren vorhandener Ressourcen.

**Refactoring:** Beim Umgestalten müssen Teammitglieder Quellcode ändern, die Architektur einer Anwendung ändern oder neue Clouddienste einführen. In der Regel würden für diese Aktivitäten Entwicklungstools wie Visual Studio und Bereitstellungspipelinetools wie Azure DevOps verwendet, um modernisierte Anwendungen erneut in Azure bereitzustellen. Für diese Arbeit sind Anwendungsentwicklungsrollen oder DevOps-Pipelineentwicklungsrollen gut geeignet. Cloudinnovationsteams sind für diese Aufgabe am besten strukturiert. Es kann länger dauern, bei diesem Ansatz vorhandene Ressourcen mit Cloudressourcen zu ersetzen, aber die Apps können cloudnative Funktionen nutzen.

**Geringfügige Umgestaltung:** Einige Anwendungen können mit geringfügiger Umgestaltung auf Daten- oder Anwendungsebene aktualisiert werden. Dabei müssen Teammitglieder Daten für cloudbasierte Datenplattformen bereitstellen oder geringfügige Konfigurationsänderungen an der Anwendung vornehmen. Dies erfordert möglicherweise gewisse Unterstützung von fachlichen Ansprechpartnern für Daten- oder Anwendungsentwicklung. Allerdings ähnelt diese Arbeit der, die IT-Implementierer durchführen, wenn sie Drittanbieter-Apps bereitstellen. Diese Arbeit kann problemlos vom Cloudmigrationsteam oder Cloudstrategieteam ausgeführt werden. Diese Aktivität ist zwar nicht annähernd so schnell wie eine Migration mit Zuweisen eines neuen Hosts, benötigt jedoch weniger Zeit als Umgestaltungsaktivitäten.

Während der Migration sollten Aktivitäten wie oben beschrieben in drei Methoden aufgeteilt werden, und diese Aktivitäten werden vom entsprechenden Team in entsprechender Iteration ausgeführt. Obwohl Sie das Portfolio diversifizieren sollten, müssen Sie auch sicherstellen, dass der Aufwand sehr fokussiert und getrennt bleibt.

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Während der Prozesse zum Optimieren und Höherstufen im Rahmen der Migrationsaktivitäten sind keine zusätzlichen Änderungen erforderlich.

## <a name="secure-and-manage-process-changes"></a>Änderungen am Sicherungs- und Verwaltungsprozess

Während der Prozesse zum Sichern und Verwalten im Rahmen der Migrationsaktivitäten sind keine zusätzlichen Änderungen erforderlich.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur [Checkliste für erweiterten Umfang](./index.md) zurück, um sicherzustellen, dass Ihre Migrationsmethode vollständig ausgerichtet ist.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
