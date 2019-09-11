---
title: Silos und Machtbereiche
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Grundlegendes zu den Antimustern von Silos und Machtbereichen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 4f9c1f13c6d6c0fe6cbb272d93f6cad2570e9a83
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2019
ms.locfileid: "70906340"
---
# <a name="organizational-antipatterns-silos-and-fiefdoms"></a>Antimuster in Unternehmen: Silos und Machtbereiche

Für den Erfolg bei allen größeren Veränderungen von Geschäftsmethoden, Unternehmenskulturen oder Technologieabläufen ist ein „dynamisches Selbstbild“ (Growth Mindset) unabdingbar. Kernkomponenten des dynamisches Selbstbilds sind die Akzeptanz von Veränderungen und die Fähigkeit, trotz eventuell bestehender Ungewissheiten Führungsstärke zu beweisen.

Das dynamische Selbstbild in Organisationen, deren Ziele die Weiterentwicklung und Transformation sind, kann durch bestimmte Antimuster blockiert werden. Hierzu gehören Mikromanagement, Vorurteile und Ablehnungsverhalten. Bei vielen dieser blockierenden Elemente geht es um persönliche Herausforderungen, aus denen sich Weiterentwicklungschancen für alle Mitarbeiter ergeben. Zwei gängige Antimuster in der IT erfordern jedoch mehr als individuelles Wachstum oder Reife: Silos und Machtbereiche.

![Vergleich von intakten Teams und Antimustern in Organisationen](../_images/ready/fiefdom-and-silo.png)

Diese Antimuster das Ergebnis von natürlichen Veränderungen in verschiedenen Teams, die zu fehlerhaftem Verhalten in Organisationen führen. Damit Sie dem auf den einzelnen Antimustern basierenden Widerstand begegnen können, ist es wichtig, dass Sie die Grundursache verstehen.

## <a name="healthy-organic-it-teams"></a>Intakte natürliche IT-Teams

Es ist ganz natürlich, im IT-Bereich eine Arbeitsteilung vorzunehmen. Es ist in Ordnung, Teams einzurichten, die über ähnliche Kenntnisse, gemeinsame Prozesse, ein gemeinsames Ziel und eine gemeinsame Vision verfügen. Es ist auch kein Problem, wenn diese Teams über eine eigene Mikrokultur und gemeinsame Normen und Sichtweisen verfügen.

Bei intakten IT-Teams steht die Partnerschaft mit anderen Teams im Vordergrund, um die erfolgreiche Erledigung ihrer Aufgaben zu fördern. In intakten IT-Teams wird versucht, die geschäftlichen Ziele zu verstehen, die durch den geleisteten technologischen Beitrag unterstützt werden sollen. Die Details und finanziellen Auswirkungen sind ggf. nicht ganz eindeutig, aber der Wertbeitrag des Teams ist innerhalb des Teams meist klar.

Intakte IT-Teams stehen zwar leidenschaftlich zur von ihnen unterstützten Technologie, aber sie sind auch offen für Veränderungen und bereit, neue Dinge auszuprobieren. Teams dieser Art tragen häufig am frühesten und stärksten zur Arbeit des [Cloudkompetenzzentrums (CCoE)](./cloud-center-excellence.md) bei. Ihr Beitrag sollte ausgiebig gefördert werden.

### <a name="natural-resistance-to-change"></a>Natürlicher Widerstand gegen Veränderungen

Es kann vorkommen, dass Mikrokulturen innerhalb von intakten IT-Teams unangemessen auf Entscheidungen der Führungsebene reagieren, die mit Veränderungen verbunden sind. Diese Reaktion ist normal, da Gruppen von Menschen mit gemeinsamen Normen häufig zusammenarbeiten, um Bedrohungen von außen abzuwehren.

Veränderungen, die Auswirkungen auf die tägliche Arbeit, das Gefühl der Sicherheit oder die Autonomie von Teams haben, können von der Gruppe als Risiko angesehen werden. Anzeichen für Widerstand sind häufig ein früher Hinweis darauf, dass die Teammitglieder der Meinung sind, nicht in den Entscheidungsfindungsprozess eingebunden zu sein.

Wenn Cloudarchitekten und andere Führungskräfte Arbeit in die Beseitigung von persönlichen Vorurteilen und die Einbindung der vorhandenen IT-Teams investieren, ist die Wahrscheinlichkeit hoch, dass der Widerstand schnell abnimmt und im Laufe der Zeit nicht mehr erkennbar ist. Ein Werkzeug für Cloudarchitekten und Führungskräfte, mit dem die Einbindung in die Entscheidungsfindung sichergestellt werden kann, ist die Schaffung eines CCoE (Cloudkompetenzzentrum).

### <a name="healthy-friction"></a>Normale Spannungen

Widerstand kann leicht mit Spannungen verwechselt werden. Es kann durchaus sein, dass sich vorhandene IT-Teams der in der Vergangenheit gemachten Fehler, der konkreten Risiken, des Gruppenwissens zu Lösungen und der nicht dokumentierten technischen Schulden bewusst sind. Leider machen auch die intaktesten IT-Teams ggf. den Fehler, diese wichtigen Datenpunkte als Teil einer bestimmten technischen Lösung zu beschreiben, die nicht geändert werden sollte. Dieser Kommunikationsansatz verschleiert das Wissen des Teams und erweckt den Eindruck von Widerstand.

Indem für diese Teams ein Mechanismus für die Kommunikation mit auf die Zukunft ausgerichteter Terminologie bereitgestellt wird, werden Datenpunkte hinzugefügt und Lücken identifiziert, und es wird eine gesunde Spannung rund um die vorgeschlagenen Lösungen erzeugt. Durch diese zusätzlichen Spannungen werden die Ecken und Kanten der Lösung beseitigt, und der langfristige Nutzen wird gefördert. Durch eine einfache Veränderung der Kommunikation kann Klarheit bei komplexen Themen geschaffen und Energie freigesetzt werden, um erfolgreichere Lösungen zu erhalten.

Im Leitfaden zum [Definieren einer Unternehmensrichtlinie](../governance/corporate-policy.md) geht es um eine risikobasierte Kommunikation mit den Projektbeteiligten im Unternehmen. Dasselbe Modell kann aber auch für die Kommunikation mit Teams verwendet werden, die der Cloud eher ablehnend gegenüberstehen. Wenn die Ablehnung weit verbreitet ist, kann es ratsam sein, in die Beauftragung eines [Cloudgovernanceteams](./cloud-governance.md) Lösungsmethoden zur Beseitigung von Widerstand zu integrieren.

## <a name="antipatterns"></a>Antimuster

Die natürliche und aktive Weiterentwicklung im IT-Bereich, aus der intakte IT-Teams entstehen, kann auch zu Antimustern führen, mit denen die Transformation und Cloudeinführung blockiert wird. IT-Silos und -Machtbereiche unterscheiden sich von den natürlichen Mikrokulturen intakter IT-Teams. Bei beiden Mustern ist für das Team meist die Verteidigung ihres Bereichs am wichtigsten. Wenn Teammitglieder mit einer Gelegenheit für Veränderungen und eine Verbesserung des Betriebs konfrontiert wird, investieren sie mehr Zeit und Energie in die Blockade der Veränderung als mit der Suche nach einer positiven Lösung.

Wie bereits erwähnt, kann es bei intakten IT-Teams zu natürlichem Widerstand und positiven Spannungen kommen. Silos und Machtbereiche stellen dagegen eine andere Herausforderung dar. Für beide Antimuster gibt es keinen dokumentierten Hauptindikator. Diese Antimuster werden häufig erst identifiziert, nachdem vom [Cloudkompetenzzentrum](./cloud-center-excellence.md) und vom [Cloudgovernanceteam](./cloud-governance.md) bereits monatelange Arbeit geleistet wurde. Sie werden aufgrund von ständig geleistetem Widerstand erkannt.

Auch in toxischen Unternehmenskulturen sollte es durch die Arbeit des CCoE und des Cloudgovernanceteams möglich sein, für kulturelle Weiterentwicklung und technischen Fortschritt zu sorgen. Auch nach monatelanger Arbeit gibt es unter Umständen noch einige Teams, die sich nicht beteiligen und auf ihrem Widerstand gegen Veränderungen beharren. Diese Teams gehen wahrscheinlich nach einem der folgenden Antimustermodelle vor: Silos und Machtbereiche. Auch wenn diese Modelle ähnliche Symptome aufweisen, unterscheiden sich jedoch die Grundursache und die Ansätze für den Umgang mit Widerstand für sie stark.

## <a name="it-silos"></a>IT-Silos

Teammitglieder in einem IT-Silos definieren sich häufig über ihre Verbindung mit einer kleinen Zahl von IT-Anbietern oder einen bestimmten Bereich technischer Spezialisierung. Sie sollten IT-Silos aber nicht mit IT-Machtbereichen verwechseln. Bei IT-Silos stehen Benutzerfreundlichkeit und Leidenschaft im Vordergrund, und Vorbehalte lassen sich normalerweise leichter ausräumen, als es bei den angstgetriebenen Motiven von Machtbereichen der Fall ist.

Dieses Antimuster entsteht oft aus einer gemeinsamen Leidenschaft für eine bestimmte Lösung. Die IT-Silos werden dann durch die besonderen Fähigkeiten des Teams gestärkt, nachdem in diese bestimmte Lösung investiert wurde. Durch diese besonderen Fähigkeiten kann die Arbeit zur Einführung der Cloud beschleunigt werden, sofern der Widerstand gegen die Veränderung beseitigt werden kann. Es kann auch zu größeren Blockaden kommen, wenn die Silos aufgelöst werden oder die Teammitglieder die Optionen nicht richtig evaluieren können. Glücklicherweise kann für IT-Silos häufig eine Lösung gefunden werden, ohne dass das Organigramm erheblich geändert werden muss.

### <a name="addressing-resistance-from-it-silos"></a>Reagieren auf Widerstand aus IT-Silos

Für den Umgang mit IT-Silos können die folgenden Ansätze verwendet werden. Der beste Ansatz richtet sich jeweils nach der Grundursache des Widerstands.

**Erstellen virtueller Teams:** Im Abschnitt zur [Bereitschaft der Organisation](./index.md) des Frameworks für die Cloudeinführung (Cloud Adoption Framework) wird eine mehrschichtige Struktur zur Integration und Definition von vier virtuellen Teams (V-Teams) beschrieben. Ein Vorteil dieser Struktur ist die organisationsweite Transparenz und Inklusion. Durch die Einführung eines [Cloudkompetenzzentrums](./cloud-center-excellence.md) wird ein bedeutendes ehrgeiziges Team geschaffen, an dessen Arbeit die besten Techniker beteiligt sein möchten. Auf diese Weise können neue lösungsübergreifende Zusammenhänge entstehen, die nicht durch Vorgaben des Organigramms eingeschränkt werden, und die Beteiligung der besten Techniker, die bisher Teil von IT-Silos waren, wird gefördert.

Durch die Einführung eines [Cloudstrategieteams](./cloud-strategy.md) wird sofort Transparenz in Bezug auf IT-Beiträge geschaffen, die die Arbeit zur Einführung der Cloud betreffen. Wenn sich IT-Silos für eine Trennung einsetzen, kann diese Transparenz hilfreich dabei sein, Führungskräfte aus dem IT-Bereich und dem betriebswirtschaftlichen Bereich dazu zu motivieren, diese Widerstand leistenden Teammitglieder richtig zu unterstützen. Dieser Prozess ist eine schnelle Möglichkeit, um Projektbeteiligte einzubinden und zu unterstützen.

**Experimentieren und Offenlegen als Chance:** Teammitglieder in einem IT-Silo waren meist eine Zeit lang darauf beschränkt, in eine bestimmte Richtung zu denken. Das Aufbrechen dieser engen Sichtweise ist der erste Schritt zur Beseitigung des Widerstands.

Experimente und Offenlegungen sind leistungsfähige Werkzeuge, wenn es um die Beseitigung von Hindernissen in Silos geht. Da konkurrierende Lösungen von Teammitgliedern unter Umständen abgelehnt werden, ist es nicht ratsam, dem Team die Leitung eines Experiments zu überlassen, bei der ein konkurrierendes Produkt getestet wird. Im Rahmen eines ersten Workloadtests der Cloud sollte die Organisation jedoch konkurrierende Lösungen implementieren. Die Teams aus den Silos sollten beteiligt werden, um Beiträge leisten und Überprüfungen durchführen zu können, aber nicht als Entscheidungsträger. Dies sollte eindeutig an das Team kommuniziert werden, und außerdem sollte zugesichert werden, dass das Team stärker in die Entscheidungsfindung eingebunden wird, bevor die Umstellung auf Lösungen für die Produktion erfolgt.

Halten Sie sich bei der Überprüfung der konkurrierenden Lösung an die bewährten Methoden unter [Definieren der Unternehmensrichtlinie](../governance/corporate-policy.md). So können Sie konkrete Risiken des Experiments dokumentieren und Richtlinien festlegen, die dazu beitragen, dass das Team aus dem Silo sich eher mit dem zukünftigen Zustand anfreunden kann. Für das Team werden hierdurch neue Lösungen verfügbar gemacht, und die Akzeptanz der zukünftigen Lösung wird erhöht.

**„Grenzenlosigkeit“:** Teams, die sich mit der Cloudeinführung beschäftigen, fällt die Verschiebung von Grenzen leicht, indem sie aufregende, neue cloudnative Lösungen erkunden. Dies ist eine Seite des Ansatzes zur Beseitigung von Hindernissen. Diese Herangehensweise kann aber auch dazu führen, dass IT-Silos gestärkt werden. Wenn Veränderungen zu schnell vorangetrieben und vorhandene Kulturen nicht respektiert werden, kann dies zu negativen Spannungen und natürlichem Widerstand führen.

Wenn IT-Silos Widerstand leisten, ist es wichtig, dass Sie bei Ihren eigenen Lösungen „grenzenlos“ vorgehen. Beachten Sie die folgende einfache Wahrheit: die cloudnative Lösung ist nicht immer die beste Lösung. Erwägen Sie den Einsatz von Hybridlösungen, die es ermöglichen, die Nutzung der vorhandenen Investitionen des IT-Silos zu verlängern.

Erwägen Sie auch die Verwendung von cloudbasierten Versionen der Lösung, die das Team des IT-Silos bereits nutzt. Experimentieren Sie mit diesen Lösungen, und versetzen Sie sich in die Position der Mitarbeiter im IT-Silo. Hierbei lernen Sie mindestens eine neue Sichtweise kennen. Oftmals verdienen Sie sich genug Respekt vom IT-Silo, um den Widerstand zu verringern.

**Investition in Weiterbildung:** Viele Mitarbeiter in einem IT-Silo haben ihre Leidenschaft für die derzeitige Lösung entwickelt, weil sie sich dafür weitergebildet haben. Eine Investition in die Weiterbildung dieser Teams ist selten fehl am Platze. Ermöglichen Sie es, dass diese Personen Zeit für die Weiterbildung per Selbststudium oder die Teilnahme an Schulungen oder sogar an Konferenzen haben, um die tagtägliche Ausrichtung auf die derzeitige Lösung aufzubrechen.

Damit Bildung eine Investition ist, muss sich ein gewisser Gewinn aus den Kosten ergeben. Als Gegenleistung für die Investition kann das Team die vorgeschlagene Lösung beispielsweise für die restlichen Teams demonstrieren, die an der Cloudeinführung beteiligt sind. Darüber hinaus kann es auch die konkreten Risiken, Ansätze für das Risikomanagement und die gewünschten Richtlinien dokumentieren, die für die Einführung der vorgeschlagenen Lösung gelten. Hierbei werden die Teams in die Lösung eingebunden, und ihr kollektives Wissens wird genutzt.

**Transformieren von Straßensperren in Temposchwellen:** IT-Silos können bewirken, dass die Transformation verlangsamt oder gestoppt wird. Es finden sich immer Möglichkeiten, mit den Experimenten und Iterationen fortzufahren, aber dies gilt nur, wenn für das Projekt Fortschritte erzielt werden. Konzentrieren Sie sich darauf, Straßensperren in Temposchwellen zu verwandeln. Definieren Sie Richtlinien, die von allen Beteiligten vorübergehend akzeptiert werden können, um sicherzustellen, dass das Projekt Fortschritte macht.

Wenn beispielsweise die IT-Sicherheit die Straßensperre darstellt, weil geschützte Daten in der Cloud mit der verwendeten Sicherheitslösung nicht auf Kompromittierungen überwachten werden können, sollten Sie Richtlinien für die Datenklassifizierung aufstellen. Verhindern Sie die Bereitstellung von klassifizierten Daten in der Cloud, bis eine akzeptable Lösung gefunden wird. Laden Sie die IT-Sicherheit dazu ein, mit hybriden oder cloudnativen Lösungen zu experimentieren, um geschützte Daten zu überwachen.

Wenn das Netzwerkteam als Silo betrieben wird, sollten Sie Workloads identifizieren, die eigenständig sind und nicht über Netzwerkabhängigkeiten verfügen. Führen Sie parallel dazu Experimente und Offenlegungen durch, und sorgen Sie für die Weiterbildung des Netzwerkteams, während Sie an hybriden oder alternativen Lösungen arbeiten.

**Geduld und Einbindung:** Es ist verlockend, ohne die Unterstützung eines IT-Silos weiterzuarbeiten. Diese Entscheidung führt aber später zu Störungen und „Straßensperren“. Eine Einstellungsänderung bei den Mitgliedern des IT-Silos braucht wahrscheinlich Zeit. Haben Sie Geduld mit natürlichem Widerstand – und verwandeln Sie ihn in Nutzen. Gehen Sie inklusiv vor, und fördern Sie gesunde Spannungen, um die zukünftige Lösung zu verbessern.

**Vermeidung einer Wettbewerbssituation:** Es hat einen Grund, warum das IT-Silo existiert. Es hat einen Grund, warum es immer noch vorhanden ist. In die Pflege der Lösung, die vom Team mit Leidenschaft verteidigt wird, wurde auch aus einem bestimmten Grund investiert. Ein direkter Wettbewerb mit der Lösung oder dem IT-Silo lenkt nur vom wirklichen Ziel ab: der Erreichung der Geschäftsergebnisse. In diese Falle sind schon viele Transformationsprojekte geraten und wurden so blockiert.

Behalten Sie weiterhin das Ziel im Auge, nicht nur eine einzelne Komponente dieses Ziels. Tragen Sie dazu bei, die positiven Aspekte der Lösung des IT-Silos hervorzuheben, und leisten Sie dem Team Hilfe beim Treffen der richtigen Entscheidungen über die bestmöglichen Lösungen für die Zukunft. Schmälern oder werten Sie die aktuelle Lösung nicht ab, denn das wäre kontraproduktiv.

**Partnerschaftliche Zusammenarbeit mit dem Unternehmen:** Wenn das IT-Silo die Geschäftsergebnisse nicht blockiert, warum interessiert es Sie dann? Es gibt keine perfekte Lösung und auch keinen perfekten IT-Anbieter. Es hat einen Grund, warum es zu einem Wettbewerb kommt. Hieraus ergeben sich jeweils bestimmte Vorteile.

Fördern Sie Vielfalt, und binden Sie das Unternehmen ein, indem Sie Unterstützung leisten und die Ausrichtung auf ein starkes [Cloudstrategieteam](./cloud-strategy.md) durchführen. Wenn von einem IT-Silo eine Lösung unterstützt wird, mit der Geschäftsergebnisse blockiert werden, ist es einfacher, diese Straßensperre zum Thema zu machen – ohne die unnötige Ablenkung durch technische Streitereien. Die Unterstützung von nicht blockierenden IT-Silos verdeutlicht, dass eine Zusammenarbeit möglich ist, um die gewünschten Geschäftsergebnisse zu erreichen. Diese Bemühungen führen zu mehr Respekt und einer größeren Unterstützung durch das Unternehmen, wenn ein IT-Silo einen legitimen Blockadegrund nennt.

## <a name="it-fiefdoms"></a>IT-Machtbereiche

Teammitglieder in einem IT-Machtbereich definieren sich häufig über ihre Ausrichtung auf einen bestimmten Prozess oder Zuständigkeitsbereich. Das Team unterliegt der Annahme, dass eine externe Einflussnahme auf ihren Zuständigkeitsbereich zu Problemen führt. Bei Machtbereichen handelt es sich um angstgetriebene Antimuster, für deren Überwindung erhebliche Unterstützung durch die Führungsebene erforderlich ist.

Machtbereiche treten besonders häufig in Organisationen auf, in denen es zu einer Verkleinerung des IT-Bereichs, häufigen Turbulenzen in Bezug auf die IT-Mitarbeiter oder schlechter IT-Führungsleistung gekommen ist. Wenn der IT-Bereich vom Unternehmen lediglich als Kostenstelle angesehen wird, ist die Wahrscheinlichkeit für die Entstehung von Machtbereichen deutlich höher.

Im Allgemeinen sind Machtbereiche das Ergebnis einer Situation, in der eine Leitungsperson den Verlust des Teams und der zugehörigen Machtbasis fürchtet. Diese Leitungspersonen fühlen sich ihrem Team häufig verpflichtet und möchten die Untergebenen vor negativen Konsequenzen schützen. Sätze wie „Das Team muss vor Veränderungen geschützt werden“ und „Das Team muss vor Prozessstörungen geschützt werden“ können Indikatoren für einen übervorsichtigen Manager sein, der möglicherweise mehr Unterstützung durch die Führung benötigt.

### <a name="addressing-resistance-from-it-fiefdoms"></a>Reagieren auf Widerstand aus IT-Machtbereichen

Für IT-Machtbereiche lassen sich einige Fortschritte erzielen, indem die Ansätze verfolgt werden, die Sie unter [Reagieren auf Widerstand aus IT-Silos](#addressing-resistance-from-it-silos) finden. Bevor Sie versuchen, auf den Widerstand eines IT-Machtbereichs zu reagieren, wird empfohlen, das Team zunächst wie ein IT-Silo zu behandeln. Wenn diese Ansätze nicht zu signifikanten Veränderungen führen, kann es sein, dass das Widerstand leistende Team in das Antimuster eines IT-Machtbereichs verfallen ist. Die Grundursache von IT-Machtbereichen ist etwas komplexer, da diese Art von Widerstand meist vom direkten Bereichsleiter kommt (oder einer Führungsperson auf einer höheren Ebene des Organigramms). Herausforderungen, die durch IT-Silos gesteuert werden, sind in der Regel einfacher zu bewältigen.

Wenn die Arbeit zur Cloudeinführung durch den fortdauernden Widerstand von IT-Machtbereichen blockiert wird, kann es ratsam sein, die Situation gemeinsam mit den vorhandenen IT-Führungskräften zu bewerten. Erkenntnisse des [Cloudstrategieteams](./cloud-strategy.md), [Cloudkompetenzzentrums](./cloud-center-excellence.md) und [Cloudgovernanceteams](./cloud-governance.md) sollten von der IT-Führungsebene sorgfältig geprüft werden, bevor Entscheidungen getroffen werden.

> [!NOTE]
> IT-Verantwortliche sollten Änderungen am Organigramm niemals auf die leichte Schulter nehmen. Sie sollten auch das Feedback der einzelnen unterstützenden Teams überprüfen und analysieren. Durch Transformationsmaßnahmen wie die Cloudeinführung kommen jedoch häufig grundlegende Probleme ans Tageslicht, die bisher nicht wahrgenommen oder zu einem Zeitpunkt lange vor diesen Maßnahmen nicht gelöst wurden. Wenn Machtbereiche den Erfolg des Unternehmens verhindern, sind wahrscheinlich Veränderungen auf der Führungsebene erforderlich.
>
> Glücklicherweise führt die Entfernung des Leiters eines Machtbereichs häufig nicht zu seiner Kündigung. Nach einer kurzen Besinnungsphase können diese starken, leidenschaftlichen Führungspersönlichkeiten häufig eine Managementrolle übernehmen. Mit der richtigen Unterstützung kann diese Änderung für die Leitungsperson des Machtbereichs und das derzeitige Team durchaus positiv sein.

> [!CAUTION]
> Das Schützen des Teams vor Risiken ist für Manager in IT-Machtbereichen eindeutig eine positive Fähigkeit von Führungspersonen. Es sollte aber zwischen Schutz und Isolation unterschieden werden. Wenn das Team daran gehindert wird, sich an der Förderung von Veränderungen zu beteiligen, kann dies psychologische und berufliche Konsequenzen für die Teammitglieder haben. Der Drang, Widerstand zu leisten, ist ggf. stark. Dies gilt besonders in Zeiten, in denen viele Veränderungen passieren.
>
> Der Manager eines isolierten Teams kann ein dynamisches Selbstbild am besten demonstrieren, indem er mit den Tipps zu intakten IT-Teams experimentiert, die bisher beschrieben wurden. Eine aktive und optimistische Teilnahme an Governance- und CCoE-Aktivitäten kann zu einem persönlichen Wachstum führen. Manager von IT-Machtbereichen sind am besten positioniert, um lähmende Denkansätze zu ändern und das Team beim Entwickeln neuer Ideen zu unterstützen.

IT-Machtbereiche können ein Anzeichen für systemische Probleme auf der Führungsebene sein. Zur Überwindung eines IT-Machtbereichs müssen IT-Führungskräfte dazu in der Lage sein, Änderungen an Abläufen, Zuständigkeiten und ggf. auch an den Personen vorzunehmen, die als Manager für bestimmte Teams tätig sind. Wenn Änderungen dieser Art erforderlich sind, ist es ratsam, mit eindeutigen und vertretbaren Datenpunkten an die Änderungen heranzugehen.

Unter Umständen ist eine Abstimmung mit Projektbeteiligten aus dem Unternehmen und in Bezug auf die geschäftliche Motivation und Geschäftsergebnisse erforderlich, um die notwendige Veränderung voranzubringen. Die partnerschaftliche Zusammenarbeit mit dem [Cloudstrategieteam](./cloud-strategy.md), [Cloudkompetenzzentrum](./cloud-center-excellence.md) und [Cloudgovernanceteam](./cloud-governance.md) kann die Datenpunkte liefern, die für eine gut vertretbare Position benötigt werden. Bei Bedarf sollten diese Teams in eine Gruppeneskalation einbezogen werden, um Schwierigkeiten zu überwinden, die mit der IT-Führungsebene allein nicht ausgeräumt werden können.

## <a name="next-steps"></a>Nächste Schritte

Die Beseitigung von Antimustern in Organisationen ist eine gemeinschaftliche Aufgabe. Sie können basierend auf diesem Leitfaden aktiv werden, indem Sie die „Einführung in die Bereitschaft von Organisationen“ lesen. Darin erhalten Sie Hilfe beim Identifizieren der richtigen Teamstrukturen und -mitglieder:

> [!div class="nextstepaction"]
> [Identifizieren der richtigen Teamstrukturen und Teilnehmer](./index.md)
