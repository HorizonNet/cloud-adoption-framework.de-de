---
title: Ausgewogenheit konkurrierender Prioritäten
description: Entdecken Sie Strategien zum Abwägen konkurrierender Prioritäten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 768007ea6b745eab76f6ae6e255287490da93ec1
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81119668"
---
# <a name="balance-competing-priorities"></a>Ausgewogenheit konkurrierender Prioritäten

Der Einstieg in die digitale Transformation ist für alle Beteiligten in den Geschäfts- und Technologieteams ein zeitkritisches Unterfangen. Der Erfolg ist stark von der Fähigkeit des Unternehmens abhängig, eine Ausgewogenheit zwischen konkurrierenden Prioritäten herzustellen.

Ähnlich wie bei anderen digitalen Transformationen werden auch bei der Einführung der Cloud im Laufe der Zeit konkurrierende Prioritäten deutlich. Wie auch bei anderen Transformationsarten hat die Fähigkeit, eine Ausgewogenheit zwischen diesen Prioritäten zu finden, einen erheblichen Einfluss auf die Umsetzung des Geschäftswerts. Erforderlich sind offene (und manchmal schwierige) Gespräche zwischen den Beteiligten (und teilweise auch mit einzelnen Mitwirkenden), um diese Ausgewogenheit zu erreichen.

In diesem Artikel werden einige der konkurrierenden Prioritäten beschrieben, die während der Ausführung der einzelnen Methoden häufig erläutert werden. Wir hoffen, dass dieses erweiterte Wissen Sie bei den Gesprächen über die Strategien zur Einführung der Cloud unterstützt.

![Übersicht über den Lebenszyklus der Cloudeinführung](../_images/caf-overview.png)

Die folgenden Abschnitte orientieren sich an dem oben dargestellten Ablauf des Lebenszyklus der Cloudeinführung. Beachten Sie, dass die Einführung der Cloud iterativ (und nicht sequenziell) erfolgt. Die konkurrierenden Prioritäten werden an verschiedenen Punkten während der Cloudeinführung ersichtlich (und kommen teilweise an anderer Stelle erneut auf).

## <a name="general-theme-of-the-cloud-adoption-framework-approach"></a>Allgemeines Thema des Ansatzes für das Framework für die Cloudeinführung

Monolithische Lösungen und die erweiterte Planung basieren beide auf einer Reihe von Annahmen, die sich im Laufe der Zeit als korrekt erweisen können (oder eben nicht). Die Einführung der Cloud ist häufig eine neue Erfahrung für das Unternehmen und die technischen Teams. Wie bei den meisten neuen Erfahrungen oder Lernmöglichkeiten besteht eine hohe Wahrscheinlichkeit, dass sich diese Annahmen als falsch erweisen.

Das Befolgen bewährter agiler Prinzipien verzögerter technischer Entscheidungen ist der bevorzugte Ansatz für die meisten Leitlinien in diesem Framework. Dieser Ansatz befolgt ein konsistentes Muster: Legen Sie einen allgemeinen Endzustand fest, gehen Sie schnell zur ersten Implementierung über, testen und validieren Sie die Annahmen, und gestalten Sie frühzeitig um, damit Sie Annahmen berücksichtigen können. Diese auf Wachstum ausgerichtete Denkweise maximiert den Lerneffekt und minimiert gleichzeitig das Risiko im Hinblick auf den Geschäftswert. Bei dieser Denkweise müssen Sie jedoch mit einem gewissen Maß an Unklarheit zurechtkommen.

Zuweilen kann Unklarheit beängstigender (oder gefährlicher) sein als falsche Annahmen. Zwar ist dieses Framework auf das Bekanntwerden und Ansprechen von Unklarheiten während der Ausführung ausgerichtet, jedoch sind viele Situationen denkbar, in denen sich das Team auf analyse- oder annahmebasierte Ansätze stützen muss. Im Folgenden möchten wir pro Abschnitt nach Möglichkeit mindestens ein „Beispiel mit erweitertem Umfang“ illustrieren, um Situationen zu veranschaulichen, in denen eine zweite umfassendere Iteration hilfreich wäre.

## <a name="balance-during-strategy"></a>Ausgewogenheit während der Strategie

Das Hauptziel der Strategiemethodik ist das Erreichen eines Konsens zwischen den Beteiligten. Einmal definiert, bestimmt diese ausgerichtete strategische Position das Verhalten hinsichtlich jeder Methodik. So wird sichergestellt, dass technische Entscheidungen den gewünschten Geschäftsergebnissen entsprechen. Durch die Abstimmung zwischen den Beteiligten werden für alle dieselben konkurrierenden Prioritäten geschaffen: **Geschäftliche Rechtfertigung** und **Zeit bis zur geschäftlichen Auswirkung**.

**Konkurrierende Prioritäten:**

- **Geschäftliche Rechtfertigung:** Beteiligte wünschen sich oft eine umfassende Finanzanalyse und eine vollständige geschäftliche Rechtfertigung, um sich ruhigen Gewissens auf eine strategische Richtung festlegen zu können. Leider nimmt eine so gründliche Analyse oft mehr Zeit in Anspruch, weil Daten zunächst erfasst und dann analysiert werden müssen.
- **Zeit bis zur geschäftlichen Auswirkung:** Umgekehrt sind Beteiligte häufig dafür verantwortlich, Geschäftsergebnisse innerhalb eines bestimmten Zeitrahmens zu liefern. Mit der zeitaufwendigen Analyse und Bewertung können diese Ergebnisse gefährdet werden, noch bevor die technische Arbeit beginnt.

**Mindestumfang:** Um hier ein Gleichgewicht zu finden, müssen alle Beteiligten schon zu Beginn des Prozesses miteinander kommunizieren. Laut der Strategiemethodik empfiehlt es sich, den Umfang der Ausrichtung zu Beginn des Prozesses einzugrenzen. Bei dem vorgeschlagenen Ansatz konzentrieren sich die Beteiligten auf die Ausrichtung auf eine Reihe von Kernmotivationen, messbare Ergebnisse und eine allgemeine geschäftliche Rechtfertigung. Die Beteiligten sollten sich dann schnell auf eine kleine Anzahl erster Projekte oder Pilotprojekte einigen, um erforderliche Lernmöglichkeiten zu fördern.

**Beispiel zum erweiterten Umfang:** Wenn die anfängliche Geschäftsanalyse auf ein hohes Risiko negativer Auswirkungen auf das Unternehmen hinweist, müssen die Beteiligten möglicherweise innehalten und im Rahmen der geschäftlichen Begründung eine vorsichtigere Bewertung einer umfassenderen Analyse vornehmen.

## <a name="balance-during-plan"></a>Ausgewogenheit während der Planung

Ähnlich wie bei den Prioritäten der Strategie muss auch bei der Planung ein Gleichgewicht bestehen: Umfang der anfänglichen Planung und verzögerte technische Entscheidungen.

**Konkurrierende Prioritäten:**

- Im **Umfang der anfänglichen Planung** hinsichtlich der technischen Implementierung in der Cloud sind häufig viele Annahmen vorhanden. Dies ist besonders dann der Fall, wenn das Team Kompetenzlücken oder die Umgebung Ermittlungslücken aufweist und bezüglich der Workloads keine architektonischen Endzustände vorhanden sind. Alle diese Annahmen sind in detaillierten Plänen zur Cloudeinführung üblich. Experimente, Pilotprojekte und eine qualitative Analyse sind erforderlich, um diese Annahmen zu beseitigen.
- Bei **verzögerten technischen Entscheidungen** wird davon ausgegangen, dass eine Entscheidung genauer ist, je später sie getroffen wird. Die folgenden Prinzipien der agilen Produktplanung unterstützen das Verzögern technischer Entscheidungen, damit sie zum richtigen Zeitpunkt mit genügend Informationen getroffen werden können. Dieser Ansatz führt jedoch zu mehr Unklarheit im ursprünglichen Plan.

**Mindestumfang:** Agile Ansätze zur Produktentwicklung werden empfohlen, um ein schnelles Handeln innerhalb umsetzbarer Pläne voranzutreiben. Laut der Planungsmethodik sind die folgenden Schritte zum Erreichen dieser Ausgewogenheit empfehlenswert. Inventarisieren Sie mit automatisierten Ermittlungstools alle digitalen Ressourcen, aber planen Sie die nächsten ein bis drei Monate in inkrementellen Schritten. Die richtige Ausrichtung des Unternehmens sollte schnell voranschreiten. Erstellen Sie einen Bereitschaftsplan für die Fähigkeiten des zugeteilten Teams. Nutzen Sie die Vorlage für den Cloudeinführungsplan, um schnell einen anfänglichen Backlog bereitzustellen.

**Beispiel zum erweiterten Umfang:** Manchmal ist die Bereitstellung eines Cloudeinführungsplans eine Reaktion auf ein zeitkritisches oder äußerst wichtiges Geschäftsereignis. Wenn für den Erfolg viele Ressourcen innerhalb eines bestimmten Zeitraums verschoben werden müssen, werden die oben beschriebenen Schritte häufig im Rahmen eines umfassenderen Planungsaufwands befolgt. Der Schlüssel zum Erfolg ist in solchen Szenarien, zunächst den Anfang zu planen und dann den gesamten Prozess. Mit diesem Ansatz wird die Wahrscheinlichkeit blockierter Geschäftsergebnisse bei der Planung reduziert.

## <a name="balance-during-ready"></a>Ausgewogenheit bei der Bereitschaft

Wenn die Einführungsteams die ersten Schritte zur Cloud vorbereiten, bestehen oft konkurrierende Prioritäten zwischen der Zeit bis zur Einführung und den langfristigen Vorgängen. Das Team hat möglicherweise Bedenken im Hinblick auf die für die Erfüllung der Aufgaben erforderlichen Kompetenzen und die Verwaltung der Prozesse. Diese Überlegungen sind in herkömmlichen IT-Umgebungen erforderlich, in denen das Entwickeln einer Plattform physische Ressourcen und Erwerbszyklen erfordert. Wenn jedoch die gesamte IT-Plattform durch Code definiert ist, verringern traditionelle Entwicklungsmethoden (wie das Refactoring) die Notwendigkeit einer von Beginn an geeigneten Verwaltung.

**Konkurrierende Prioritäten:**

- **Langfristige Vorgänge:** Kunden werden oft durch den Wunsch nach einer Cloudumgebung gehemmt, die den Anforderungen der aktuellen Vorgangsverwaltungs-, Governance- und Sicherheitssystemen gerecht wird. Einer aktuellen Kundenstudie zufolge müssen mehr als 90 Prozent der Kunden bei der Überwindung einer solchen Denkweise unterstützt werden. Diese Blockade verlangsamt den Prozess um Monate und kann auch geschäftliche Auswirkungen verhindern.
- **Einführungszeit:** Cloudbasierte Tools wie Azure Policy, Azure Blueprints und Verwaltungsgruppen ermöglichen ein einfaches Refactoring der IT-Plattform. Darüber hinaus bieten vordefinierte Zielzonen meinungsbildende Positionen, um die Bereitstellung in einer Umgebung zu beschleunigen, die bereits viele der Anforderungen an die Featureparität erfüllt. Es besteht die Möglichkeit, die Markteinführungszeit mit minimalen Auswirkungen auf langfristige Vorgänge zu verkürzen.

**Mindestumfang:** Die Bereitschaftsmethodik beschreibt einen direkten Pfad von der schnellen Einführung zu langfristigen Vorgängen. Diese Vorgehensweise beginnt mit einer grundlegenden Einführung in die Tools, die das Refactoring der Umgebung ermöglichen. Basierend auf diesen Tools und Umgebungsanforderungen werden Kunden zu einer Auswahl vordefinierter Zielzonen geleitet (diese werden jeweils über die Infrastruktur als Codemodelle bereitgestellt). Dieser Code kann dann im Laufe der Cloudeinführung umgestaltet werden, um die Vorgänge, die Sicherheit und die Verwaltungsfunktionen zu verbessern.

**Beispiel zum erweiterten Umfang:** Für Teams, deren Einführungsplan das mittelfristige Ziel (innerhalb von 24 Monaten) vorsieht, **mehr als 1.000 Ressourcen (Apps, Infrastrukturen oder Datenressourcen) in der Cloud zu hosten,** wird eine stabilere Ansicht der Zielzonen empfohlen. In diesen Fällen sollten die Steuerungs- und Verwaltungsmethodiken während der ersten Konversationen über die Zielzone berücksichtigt werden. Dies führt im Rahmen des Cloudeinführungsplans jedoch oft zu Verzögerungen von Wochen oder Monaten. Um die Auswirkungen auf die Geschäftsergebnisse zu minimieren, sollte das Einführungsteam tatsächliche Workloads in der Cloud parallel zur Erstellung einer ausgereiften Zielzone sowie einer zentralen Architekturlösung erstellen.

## <a name="balance-during-migrate"></a>Ausgewogenheit während der Migration

Während der Migration ist es üblich, dass die Einführungsteams davon ausgehen, dass die Workloads in ihrer aktuellen Ist-Konfiguration wieder in der Cloud untergebracht werden. Dies steht in direkter Konkurrenz mit der vorausschauenden Sichtweise, jede Workload neu zu strukturieren, um aus den Cloudfähigkeiten einen größeren Nutzen zu ziehen. Leider schließen sich die beiden Denkweisen nicht gegenseitig aus und können sich sogar gegenseitig ergänzen, wenn sie in einem gemeinsamen Prozess gehandhabt werden.

**Konkurrierende Prioritäten:**

- **Zuweisen eines neuen Hosts:** Kunden gehen bei der Migration häufig von einem _Lift & Shift-Prozess_ aus, bei dem alle Ressourcen in der Cloud in ihrer aktuellen Zustandskonfiguration replizieren werden. Dies führt zu geringfügigen Abweichungen im IT-Portfolio. Diese Vorgehensweise ist auch die schnellste Möglichkeit, Ressourcen in einem vorhandenen Rechenzentrum außer Betrieb zu nehmen.
- **Überarbeiten:** Die Modernisierung der Architektur jeder Workload maximiert den Cloudwert hinsichtlich der Kosten, Leistung und Vorgänge. Dieser Ansatz ist jedoch weitaus langsamer und erfordert häufig Zugriff auf den Quellcode der einzelnen Anwendungen.

**Mindestumfang:** Verwenden Sie während der Planung in der Frühphase die Option für das erneute Hosten, und seien Sie sich dabei bewusst, dass diese Option eine anfängliche Geschäftsannahme und keine technische Entscheidung ist. Bei der Migrationsmethodik stellt das Einführungsteam dann diese Annahme für jede migrierte Workload in Frage. Diese Methodik folgt den Schritten der Bewertungs-, Migrations- und Förderungsmethodik für jede Workload oder Workloadgruppe, die eine Migrationsfactory bildet. Während der Bewertungsphase wertet das Einführungsteam die technische Eignung sowie die Architektur der einzelnen Workloads aus. Diese Bewertungsmaßnahmen führen selten zu einem reinen Lift & Shift-Ansatz, da viele der Architekturkomponenten zum Zwecke von Refactoring und Modernisierung ausgewählt werden.

**Beispiel zum erweiterten Umfang:** Bei unternehmenskritischen oder äußerst wichtigen Workloads, etwa bei einem Mainframe oder einer Microserviceanwendung mit mehreren Ebenen, kann in der Beurteilungsphase eine umfassendere Einschätzung der Workload erforderlich sein. In solchen Situationen, in denen die Architektur neu überdacht wird, sollten Kunden die Azure-Architekturüberprüfung und Azure Architecture Framework nutzen, um die Anforderungen an die Workload während der Bewertung zu einzuschränken.

## <a name="balance-during-innovate"></a>Ausgewogenheit bei Innovationen

Bei echten kundenorientierten Innovationen kommt es immer wieder zu Konflikten bei den Prioritäten. Auf der einen Seite steht die Notwendigkeit, geplante Features umzusetzen, auf der anderen Seite der Entwicklungsprozess mit Blick auf die Kundenanforderungen.

**Konkurrierende Prioritäten:**

- Funktionsfokus: Anfängliche Innovationspläne bauen auf den vorhandenen digitalen Ressourcen und Cloudfähigkeiten auf, um eine Reihe von Funktionen bereitzustellen, die den Kundenbedürfnissen entsprechen. Es ist einfach, die technische Implementierung mithilfe der Planung zu fördern, was zu einer funktionsorientierten Entwicklung führt. Dieser Ansatz führt oft zu einer vorübergehenden Zufriedenheit der Beteiligten, verringert aber die Wahrscheinlichkeit, dass Innovationen vorangetrieben werden, die sich auf das Kundenverhalten auswirken.
- Blick auf die Kundenanforderungen: Anfängliche Pläne sind ein wichtiger Bestandteil der geschäftlichen Seite der Entwicklung und sollten in die regelmäßigen Berichte aufgenommen werden. Das Lernen, Messen und Entwickeln mit Blick auf die Kundenanforderungen stellen bei Innovationsbemühungen jedoch genauere Maßnahmen dar. Die Priorisierung des Kunden statt der Funktionen führt sowohl kurz- als auch langfristig zu Kundenzufriedenheit und geschäftlichen Auswirkungen.

**Mindestumfang:** Die Innovationsmethodik veranschaulicht, wie sich Strategie und Pläne durch einen Konsens über den Geschäftswert integrieren lassen. Anschließend werden im Leitfaden cloudnative Tools vorgestellt, mit denen die einzelnen Innovationsmöglichkeiten beschleunigt werden. Außerdem finden Sie darin bewährte Methoden zur Implementierung. Der Abschnitt zu Prozessverbesserungen beschreibt unter Berücksichtigung von Plänen und Strategien bei der Cloudeinführung Ansätze für die Entwicklung eines Blicks auf Kundenanforderungen. Dieser Ansatz konzentriert sich darauf, Innovationen mit so wenig Technologie wie möglich zu erreichen.

**Beispiel zum erweiterten Umfang:** Manchmal ist eine Innovation abhängig von unternehmenskritischen oder hochsensiblen Workloads. Wenn es sich bei dem „Kunden“ um einen internen Benutzer handelt, kann der Entwicklungsaufwand während der frühesten Iterationen sowohl unternehmenskritisch als auch hochsensibel sein. Für diese Szenarien sollten die Einführungsteams die Azure-Architekturüberprüfung und Azure Architecture Framework verwenden, um das fortgeschrittene Architekturdesign frühzeitig zu bewerten.

## <a name="balance-during-govern"></a>Ausgewogenheit bei der Governance

Die Praxis der Cloudgovernance ist ein ständiges Gleichgewicht zwischen zwei konkurrierenden Prioritäten: Geschwindigkeit/Agilität und eine angemessen gesteuerte Umgebung. Durch eine einheitliche Steuerung und minimale Änderungen konzentriert sich das Cloudgovernanceteam auf das Auswerten und Minimieren von Risiken für das Unternehmen. Das Einführungsteam konzentriert sich auf die Förderung von Geschäftsergebnissen, die neue Risiken erfordern und von Natur aus Veränderungen bewirken.

**Konkurrierende Prioritäten:**

- Angemessene Governance: Jede auf Risikominimierung ausgerichtete Kontrolle blockiert einen Änderungsaspekt oder schränkt die Gestaltungsmöglichkeiten ein. Kontrolle ist für eine angemessen gesteuerte Umgebung unverzichtbar. Wenn Kontrollen jedoch isoliert entwickelt und bereitgestellt werden, können Sie so schädlich sein wie die Risiken, die durch sie verhindert werden sollen.
- Geschwindigkeit/Agilität: Geschwindigkeit und Agilität sind in der digitalen Wirtschaft grundlegende Geschäftsanforderungen. Beide erfordern die Fähigkeit, Veränderungen mit minimalen Blockaden für die Innovationen oder die Einführung voranzutreiben. Wenn Änderungen von der Governance isoliert vorangetrieben werden, führt dies zu neuen Risiken, die dem Unternehmen auf unbeabsichtigte Weise schaden können.

**Mindestumfang:** Die Governancemethodik deutet darauf hin, dass weder Governance noch Einführung isoliert erfolgen sollten. Diese Methode beginnt mit einem Verständnis der Governancedisziplinen und einem Gespräch über Geschäftsrisiken, Richtlinien und Prozesse. Als aktives Mitglied der gesamten Cloudeinführung kann das Governanceteam ein Minimum an Schutzmaßnahmen implementieren, um die greifbaren Risiken innerhalb des Cloudeinführungsplans anzugehen. Im Laufe der Zeit kann das Governanceteam diese Schutzmaßnahmen umgestalten und erweitern, um neue Risiken anzusprechen. Dieser Ansatz maximiert den Lerneffekt und mögliche Innovationen und minimiert gleichzeitig das Risiko.

**Beispiel zum erweiterten Umfang:** Wenn das Geschäftsrisiko hoch ist, insbesondere zu Beginn der Einführung, ist möglicherweise die Beschleunigung der Ausweitung der Governanceimplementierungen durch das Cloudgovernanceteam erforderlich. Die gleichen Anleitungen und Übungen können auch für diese höhere Governanceebene verwendet werden, dabei muss jedoch die zeitliche Steuerung möglicherweise beschleunigt werden. In einigen Szenarien kann sogar während der Bereitstellung der ersten Zielzonen eine fortgeschrittene Governance erforderlich sein.

## <a name="balance-during-manage"></a>Ausgewogenheit während der Verwaltung

Das IT-Geschäftsmodell hinsichtlich der Verwaltung von Vorgängen hat sich im letzten Jahrzehnt kontinuierlich weiterentwickelt. In dem Maße, in dem sich die Hardwarewartung immer weiter vom zentralen Wertversprechen der IT entfernt, hat sich auch der Blick auf die Betriebsverwaltung geändert. Da sich die IT zunehmend auf die Erzielung des geschäftlichen Nutzens konzentriert, werden die Betriebsführungsteams mit der Abwägung zwischen Investitionen für keine bzw. wenig Vorgänge (No Ops/Low Ops) und umfangreichen Investitionen belastet.

**Konkurrierende Prioritäten:**

- **Umfassende Investitionen:** Beim traditionellen Ansatz der Betriebsverwaltung wird gleichermaßen in die Vermeidung von Ausfällen, die schnelle Wiederherstellung und die Überwachung der gesamten Umgebung investiert. Dieser Ansatz kann kostspielig sein und zuweilen zu einer Duplizierung der vom Cloudanbieter zur Verfügung gestellten unterstützenden Produkte führen.
- **Keine bzw. wenig Vorgänge (No Ops/Low Ops):** Nutzen Sie cloudnative Vorgangstools, um sich wiederholende und wiederkehrende Aufgaben zu minimieren, die zuvor von Vollzeitmitarbeitern durchgeführt wurden. Durch die Reduzierung dieser vorgangsbasierten Abhängigkeiten im Vorgangsverwaltungsmodell können diese Mitarbeiter verstärkt zum Mehrwert beitragen. Für sich genommen kann dieser Ansatz zu einer suboptimalen Unterstützung von Vorgängen führen.

**Mindestumfang:** Laut der Verwaltungsmethodik ist es ratsam, eine cloudnative No Ops-Verwaltungsbaseline einzurichten. Mit dem Wissen, dass die Low Ops-Baseline nicht alle Geschäftsanforderungen erfüllt, müssen Sie mit dem Unternehmen zusammenarbeiten, um Verpflichtungen zu definieren und Investitionen besser abzustimmen. Erweitern Sie die Baseline, um allgemeine Anforderungen für alle Workloads zu erfüllen. Anschließend ermöglichen Sie es Plattformteams oder Teams mit spezifischen Workloads, gut verwaltete Lösungen in einer gut verwalteten Umgebung aufrechtzuerhalten.

**Beispiel zum erweiterten Umfang:** In den meisten Umgebungen ist es ein kleiner Prozentsatz der Workloads, deren Geschäftswert umfassende Investitionen in den IT-Betrieb rechtfertigt. In diesen Szenarien kann das IT-Team die Azure-Architekturüberprüfung und Azure Architecture Framework nutzen, um umfassendere Abläufe zu leiten.

## <a name="balance-during-organize"></a>Ausgewogenheit während der Organisation

Die konkurrierenden Prioritäten in diesem Artikel reflektieren das Bestreben der IT, die Geschäftsanforderungen hinsichtlich Geschwindigkeit und Agilität zu erfüllen. Dieselbe Verschiebung zeigt sich auch bei Änderungen an Organigrammen (oder V-Team-Strukturen), um eine größere Unterstützung für Geschäftsergebnisse zu ermöglichen. Wenn IT-Leiter über Teamstrukturen nachdenken, werden häufig zwei konkurrierende Prioritäten angesprochen: Zentralisierte Steuerung und delegierte Steuerung

**Konkurrierende Prioritäten:**

- Zentralisierte Steuerung: Vorgangsmodelle mit zentralisierter Steuerung konzentrieren sich auf die Zentralisierung aller Steuerungselemente, die zur Durchsetzung starrer Richtlinien erforderlich sind. In diesem Modell stellt die IT ein Hindernis für Innovationen, Geschwindigkeit und Agilität dar. Die IT ist jedoch in der Lage, ein höheres Maß an Stabilität, Compliance und Sicherheit zu gewährleisten.
- Delegierte Steuerung: In diesem verteilten Vorgangsmodell wird davon ausgegangen, dass jedes Entwicklerteam oder Geschäftsanwendungsteam eigene Steuerungselemente bereitstellt, die auf den Lösungen basieren, die zur Erreichung der Geschäftsziele erforderlich sind. In diesem Modell stellt die IT Schutzmaßnahmen zur Verfügung, damit Teams auf ihrem Kurs bleiben, minimiert aber wann immer möglich die Anzahl erzwungener technischer Einschränkungen.

**Mindestumfang:** Die meisten Organisationen durchlaufen im Laufe der Zeit mehrere Entwicklungen. Die Organisationsmethodik beschreibt die gängigsten Entwicklungen. Der empfohlene Leitfaden ist für Teams, die sich auf eine Cloud Center of Excellence-Struktur konzentrieren möchten, um delegierte Steuerungsansätze bereitzustellen.

**Beispiel zum erweiterten Umfang:** In vielen Situationen ist eine zentralisierte Steuerung erforderlich. Complianceanforderungen von Drittanbietern und vorübergehende Sicherheitsrisiken sind zwei Beispiele für die Auslöser einer zentralisierten Steuerung. In solchen Situationen besteht häufig die Notwendigkeit, eine einschränkende Richtlinie und starre, feste Steuerungselemente einzuführen. Um weiterhin Innovationen sowie die Einführung zu ermöglichen, sollten zentrale IT-Teams diese Steuerungselemente auf der Grundlage der Wichtigkeit der einzelnen Workloads bereitstellen. Die Bereitstellung von Umgebungen mit weniger Steuerungselementen und einem reduzierten Umfang oder Risikoprofil ermöglicht Flexibilität, selbst wenn Steuerungen erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie [Migration, Innovation und Experimentieren in Einklang bringen](./balance-the-portfolio.md), um Ihre Cloudmigration optimal zu nutzen.

> [!div class="nextstepaction"]
> [Ausgewogenheit des Portfolios](./balance-the-portfolio.md)
