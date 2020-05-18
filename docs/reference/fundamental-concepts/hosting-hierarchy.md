---
title: Grundlegendes zur Portfoliohierarchie und deren Ausrichtung
description: Grundlegendes zur Portfoliohierarchie und deren Ausrichtung
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8b7b81c6d931eb5a5518bedfff665c580c7e9053
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230646"
---
<!-- cSpell:ignore matrixed ISVs -->

<!-- markdownlint-disable MD026 -->

# <a name="understand-and-align-the-portfolio-hierarchy"></a>Grundlegendes zur Portfoliohierarchie und deren Ausrichtung

Die Geschäftsanforderungen werden oft durch Informationstechnologie unterstützt, verbessert oder beschleunigt. Eine Sammlung von Technologien, die einen definierten Geschäftswert liefert, wird als _Workload_ bezeichnet. Diese Sammlung kann Anwendungen, Server oder virtuelle Computer, Daten, Geräte und andere ähnlich gruppierte Ressourcen umfassen.

In der Regel teilen sich ein Projektbeteiligter und ein technischer Leiter die Verantwortung für die fortlaufende Unterstützung der einzelnen Workloads. In einigen Phasen des Lebenszyklus der Workload sind diese Rollen klar festgelegt. In operativeren Phasen des Lebenszyklus einer Workload können diese Rollen in ein gemeinsames Operations Management-Team oder Cloudbetriebsteam überführt werden. Mit der Zunahme der Workloads werden die (angegebenen oder impliziten) Rollen komplexer und vielfältiger.

Die meisten Unternehmen verlassen sich auf mehrere Workloads, um wichtige Geschäftsfunktionen bereitzustellen. Die Sammlung von Workloads, Ressourcen und den unterstützenden Projekten, Personen, Prozessen und Investitionen wird als _Portfolio_ bezeichnet. Die Matrix aus Geschäfts-, Entwicklungs- und Betriebsmitarbeitern erfordert eine Portfoliohierarchie, um zu verstehen, wie die Workloads und unterstützenden Dienste zusammenpassen.

In diesem Artikel finden Sie klare Definitionen für die Ebenen der Portfoliohierarchie. In dem Artikel werden verschiedene Teams mit der entsprechenden Verantwortung auf den einzelnen Ebenen zusammen mit der Quelle für die beste Anleitung für dieses Team ausgerichtet, um die Erwartungen für diese Ebene zu erfüllen. In diesem Artikel wird jede Ebene der Hierarchie auch als _Bereich_ bezeichnet.

## <a name="portfolio-hierarchy"></a>Portfoliohierarchie

Workloads und deren unterstützende Ressourcen sind der Kern eines jeden Portfolios. Die zusätzlichen folgenden Bereiche oder Ebenen legen fest, wie diese Workloads angezeigt werden und inwieweit sie von der Matrix potenzieller unterstützender Teams betroffen sind.

Wenn Sie Ihre erste Workload bereitstellen, kann es sein, dass die Workload und ihre Ressourcen der einzige definierte Bereich sind. Die anderen Ebenen werden möglicherweise explizit definiert, wenn weitere Workloads bereitgestellt werden.

![Eine Hierarchie eines Cloudportfolios aus Portfolio, Plattform, Zielzonen/Plattformhilfsprogrammen, Workloads/Lösungen und Objekte. Die Liste wird in einer geschachtelten Beziehung von über- und untergeordneten Elementen von der höchsten bis zur niedrigsten Ebene aufgeführt.](../../_images/ready/hierarchy.png)

Obwohl die Bedingungen variieren können, umfassen alle IT-Lösungen Objekte und Workloads:

- **Objekt:** Objekte sind die kleinste Einheit technischer Funktionen, die eine Workload oder Lösung unterstützen.
- **Workload:** Workloads sind die kleinste Einheit des IT-Supports für das Unternehmen. Eine Workload ist eine Sammlung von Objekten (Infrastrukturen, Anwendungen und Daten), die zusammen ein gemeinsames Geschäftsziel oder die Ausführung eines allgemeinen Geschäftsprozesses unterstützen.

Wenn Unternehmen Workloads mithilfe von Matrix- oder zentralisierten Ansätzen unterstützen, besteht wahrscheinlich eine umfassendere Hierarchie zur Unterstützung dieser Workloads:

- **Zielzone:** Zielzonen bieten den Workloads Zugriff auf alle _grundlegenden Hilfsprogramme_ (oder gemeinsam genutzten Installationen), die von einer _Plattformumgebung_ bereitgestellt werden, die zur Unterstützung einer oder mehrerer Workloads erforderlich ist.
- **Grundlegende Hilfsprogramme:** Gemeinsame IT-Dienste, die für den Betrieb der Workloads innerhalb des Technologie- und Geschäftsportfolios erforderlich sind.
- **Plattformumgebung:** Das organisatorische Konstrukt, um grundlegende Lösungen zu zentralisieren und sicherzustellen, dass diese Kontrollen für alle Zielzonen erzwungen werden.
- **Cloudplattformen:** In Abhängigkeit von der Gesamtstrategie zur Unterstützung des gesamten _Portfolios_ benötigen Kunden möglicherweise mehrere Cloudplattformen mit unterschiedlichen Bereitstellungen der Plattformumgebung, um mehrere Regionen, Hybridlösungen oder sogar Multicloudlösungen zu verwalten.
- **Portfolio:** Aus Sicht der Technologie ist das Portfolio die Sammlung der Workloads, Objekte und unterstützenden Ressourcen, die sich über alle Cloudplattformen erstreckt. Aus geschäftlicher Sicht besteht das Portfolio aus einer Sammlung von Projekten, Personen, Prozessen und Investitionen, die das Technologieportfolio unterstützen und verwalten, um die Geschäftsergebnisse zu fördern. Zusammen erfassen diese beiden Sichten das _Portfolio_.

## <a name="hierarchy-accountability-and-guidance"></a>Hierarchieverantwortlichkeit und Leitung

Jede Ebene der Portfoliohierarchie wird von einer verantwortlichen Instanz verwaltet. Das folgende Diagramm zeigt die Zuordnung zwischen dem verantwortlichen Team und der Leitung zur Unterstützung ihrer geschäftlichen und technischen Entscheidungen und der anschließenden technischen Implementierung.

> [!NOTE]
> Die im folgenden Abschnitt erwähnten Teams sind möglicherweise virtuelle Teams (v-Teams) oder Einzelpersonen. Bei einigen Varianten dieser Hierarchie können einige der verantwortlichen Teams reduziert werden, wie in den nachstehenden Varianten der Verantwortlichkeit beschrieben.

![An der Hierarchie ausgerichtete Verantwortlichkeit](../../_images/ready/hierarchy-with-roles.png)

- **Portfolio:** Das Cloudstrategieteam und das Cloudkompetenzzentrum (CCoE) nutzen die Strategie- und Planungsmethodiken, um Entscheidungen zu steuern, die das Gesamtportfolio betreffen. Das Cloudstrategieteam ist für die Unternehmensebene der gesamten Cloudportfoliohierarchie verantwortlich. Sie sollten auch über Entscheidungen in Bezug auf die Umgebung, Zielzonen und Workloads mit hoher Priorität informiert werden.
- **Cloudplattform:** Das Cloudgovernanceteam ist für die Disziplinen verantwortlich, die in Übereinstimmung mit der Governancemethodik die Konsistenz in den einzelnen Umgebungen sicherstellen. Das Cloudgovernanceteam ist für die Governance aller Ressourcen in allen Umgebungen verantwortlich. Das Cloudgovernanceteam sollte bei Änderungen, die möglicherweise eine Ausnahme erfordern, oder beim Ändern der geltenden Richtlinien konsultiert werden. Das Cloudgovernanceteam sollte auch über den Fortschritt in Bezug auf die Workload- und Objekteinführung informiert werden.
- **Zielzone und Plattformumgebungen:** Das Cloudplattformteam ist für die Entwicklung der Zielzonen und Plattformumgebungen verantwortlich, die die Einführung unterstützen. Das Cloudautomatisierungsteam ist für die Automatisierung der Entwicklung und laufenden Unterstützung dieser Zielzonen und Plattformhilfsprogrammen verantwortlich. Beide Teams verwenden die Bereitschaftsmethodik als Leitfaden für die Implementierung. Beide Teams sollten über den Fortschritt bei der Workloadeinführung und über alle Änderungen im Unternehmen oder in der Umgebung informiert werden.
- **Workload:** Die Einführung erfolgt auf der Workloadebene. Cloudeinführungsteams verwenden die Migrations- und Innovationsmethodiken, um skalierbare Prozesse zur Beschleunigung der Einführung einzurichten. Sobald die Einführung abgeschlossen ist, wird der Besitz der Workloads wahrscheinlich an ein Cloudbetriebsteam übertragen, das die Verwaltungsmethodik zur Steuerung des Operations Managements verwendet. Beide Teams sollten mit der Verwendung des Azure Architecture Framework vertraut sein, um detaillierte architekturbezogene Entscheidungen zu treffen, die sich auf die von ihnen unterstützten Workloads auswirken. Beide Teams sollten über Änderungen an Zielzonen und Umgebungen informiert werden. Beide Teams können gelegentlich zu Features der Zielzone beitragen.
- **Objekt:** Für die Objekte ist in der Regel das Cloudbetriebsteam zuständig. Dieses Team verwendet die Verwaltungsbaseline in der Verwaltungsmethodik, um Entscheidungen des Operations Managements zu leiten. Sie sollten auch den Azure Advisor und das Azure Architecture Framework nutzen, um detaillierte Änderungen an den Ressourcen und der Architektur vorzunehmen, die für die Anforderungen der erweiterten Vorgänge erforderlich sind.

### <a name="accountability-variants"></a>Verantwortlichkeitsvarianten:

- **Einzelne Umgebung:** Wenn ein Unternehmen nur eine Umgebung benötigt, ist in der Regel kein Cloudkompetenzzentrum (CCoE) erforderlich.
- **Einzelne Zielzone:** Wenn eine Umgebung nur eine einzelne Zielzone enthält, können die Governance- und Plattformfunktionen wahrscheinlich in einem Team zusammengefasst werden.
- **Einzelne Workload:** Einige Unternehmen benötigen nur eine oder wenige Workloads in einer einzelnen Zielzone und einer einzelnen Umgebung. In diesen Fällen müssen die Aufgaben nicht zwischen Governance-, Plattform-und Betriebsteams aufgeteilt werden.

## <a name="common-workload-and-accountability-examples"></a>Allgemeine Beispiele für Workload und Verantwortlichkeit

Die folgenden Beispiele veranschaulichen die Portfoliohierarchie.

### <a name="commercial-off-the-shelf-cots-workloads"></a>COTS-Workloads (commercial off-the-shelf)

Traditionell bevorzugen Unternehmen COTS-Softwarelösungen zur Unterstützung von Geschäftsprozessen. Diese Lösungen werden installiert, konfiguriert und dann betrieben. Nach der Konfiguration gibt es kaum Änderungen an der Lösungsarchitektur. In diesen Szenarien endet jede Cloudeinführung von COTS-Lösungen mit dem Übergang zu einem Cloudbetriebsteam. Das Cloudbetriebsteam wird dann zum technischen Besitzer dieser Software und übernimmt die Verantwortung für die Verwaltung von Konfiguration, Kosten, Patchzyklen und anderen betrieblichen Anforderungen.

Zu diesen Workloads gehören Buchhaltungspakete, Logistiksoftware oder branchenspezifische Lösungen. In der Microsoft-Terminologie werden die Anbieter dieser Pakete als unabhängige Softwareanbieter bezeichnet. Viele unabhängige Softwareanbieter bieten einen Dienst zur Bereitstellung und Wartung einer Instanz ihres Softwarepakets in Ihren Abonnements an. Sie können auch eine Version des Softwarepakets anbieten, die in ihrer eigenen in der Cloud gehosteten Umgebung läuft und eine PaaS-Alternative (Platform-as-a-Service) zur Workload bietet. Mit Ausnahme von PaaS-Angeboten tragen die Cloudbetriebsteams die Last der Sicherstellung grundlegender betrieblicher Complianceanforderungen für diese Workloads und sollten mit dem Cloudgovernanceteam zusammenarbeiten, um Kosten, Leistung und andere Pfeiler der Architektur aufeinander abzustimmen.

### <a name="in-development-with-active-revisions"></a>In Entwicklung mit aktiven Revisionen

Wenn eine COTS-Lösung oder ein PaaS-Angebot nicht auf die Geschäftsanforderungen abgestimmt ist oder keine Lösung existiert, erstellen Unternehmen individuell entwickelte Workloads. Normalerweise verwendet nur ein kleiner Prozentsatz des gesamten IT-Portfolios diesen Workloadansatz. Diese Workloads führen jedoch tendenziell zu einem unverhältnismäßig hohen Prozentsatz des Beitrags der IT zu den Geschäftsergebnissen, insbesondere zu Ergebnissen im Zusammenhang mit neuen Umsatzquellen. Diese Workloads lassen sich tendenziell gut zu neuen Innovationsideen zuordnen.

Angesichts verschiedener Bewegungen, die in agilen Methoden und DevOps-Praktiken verwurzelt sind, begünstigen diese Workloads eine Geschäfts-/DevOps-Ausrichtung gegenüber der traditionellen IT-Verwaltung. Bei diesen Workloads wird es möglicherweise mehrere Jahre lang keine Übergabe an das Cloudbetriebsteam geben. In diesen Fällen fungiert das Entwicklungsteam als technischer Besitzer der Workload.

Aufgrund umfangreicher Zeit- und damit verbundener Kapitalbeschränkungen sind benutzerdefinierte Entwicklungsoptionen oft auf hochwertige Gelegenheiten beschränkt. Typische Beispiele sind Anwendungsinnovationen, eingehende Datenanalysen oder unternehmenskritische Geschäftsfunktionen.

### <a name="breakfix-or-sunset-development"></a>Problemlösungs- oder Ablaufentwicklung

Sobald eine kundenspezifisch entwickelte Workload ihre maximale Reife erreicht hat, kann das Entwicklungsteam anderen Projekten zugewiesen werden. In diesen Fällen geht der technische Besitz normalerweise an ein Cloudbetriebsteam über. Wenn kleine Korrekturen erforderlich sind, trägt das Betriebsteam entsprechende Entwickler ein, um den Fehler zu beheben.

In einigen Fällen wechselt das Entwicklungsteam zu einem Projekt, das letztendlich die aktuelle Workload ersetzt. Alternativ könnten sie fortfahren, da die durch die Workload unterstützte Geschäftsmöglichkeit mit der Zeit eingestellt wird. Dies sind Beispiele für Ablaufszenarien, bei denen das Cloudbetriebsteam als technischer Besitzer fungiert, bis die Workload nicht mehr benötigt wird.

In beiden Szenarien fungiert das Cloudbetriebsteam in der Regel als langfristiger technischer Besitzer und Entscheidungsträger. Sie werden wahrscheinlich Anwendungsentwickler hinzuziehen, wenn betriebliche Änderungen erhebliche Änderungen der Architektur erfordern.

### <a name="mission-critical-workloads"></a>Unternehmenskritische Workloads

In jedem Unternehmen sind einige wenige Workloads zu wichtig für das Geschäft, als dass sie scheitern dürften. Bei diesen unternehmenskritischen Workloads gibt es in der Regel Betriebs- und Entwicklungsbesitzer mit verschiedenen Verantwortungsebenen. Diese Teams sollten betriebliche und architekturbezogene Änderungen aufeinander abstimmen, um Störungen der Produktionslösung zu minimieren. Diese Szenarien erfordern einen starken Schwerpunkt auf die Trennung von Aufgaben. Um eine Aufgabentrennung zu erreichen, wird das Betriebsteam im Allgemeinen die Verantwortung für alltägliche betriebliche Änderungen in der Produktionsumgebung übernehmen. Wenn diese betrieblichen Änderungen eine architekturbezogene Änderung erfordern, werden sie vom Entwicklungs- oder Einführungsteam in einer Nicht-Produktionsumgebung durchgeführt, bevor das Betriebsteam die Änderungen in der Produktionsumgebung anwendet.

Beispiele für unternehmenskritische Workloads mit einer erforderlichen Trennung von Aufgaben sind Workloads wie SAP, Oracle oder andere ERP-Lösungen (Enterprise Resource Planning), die sich über mehrere Geschäftseinheiten im Unternehmen erstrecken.

## <a name="strategy-portfolio-alignment"></a>Ausrichtung des Strategieportfolios

Wie im Artikel über das Gleichgewicht des Portfolios erörtert, ist es wichtig, die strategischen Ziele der Bemühungen zur Cloudeinführung zu verstehen und das Portfolio so auszurichten, dass es diese Transformation unterstützt. Einige gängige Arten der strategischen Portfolioausrichtung helfen bei der Gestaltung der Struktur der Portfoliohierarchie. Die folgenden Abschnitte enthalten Beispiele für die Ausrichtung des Portfolios und die Auswirkungen auf die Portfoliohierarchie.

### <a name="innovation-or-development-led-portfolio"></a>Innovations- oder entwicklungsorientiertes Portfolio

Einige Unternehmen, insbesondere schnell wachsende etablierte Startups, haben einen überdurchschnittlich hohen Anteil an benutzerdefinierten Entwicklungsprojekten. In entwicklungsintensiven Portfolios werden Umgebung, Zielzone und Workloads oft komprimiert und es kann bestimmte Umgebungen (Produktions- oder Nicht-Produktionsumgebungen) für bestimmte Workloads geben. Daraus ergibt sich ein Verhältnis von 1:1 zwischen Umgebung, Zielzone und Workload. Da die Umgebung benutzerdefinierte Lösungen hostet, könnte außerdem die DevOps-Pipeline und Berichterstellung auf Anwendungsebene den Bedarf an Betriebs- und Verwaltungsfunktionen ersetzen. Für diese Kunden ist ein reduzierter Fokus auf Betrieb, Governance oder andere unterstützende Rollen wahrscheinlich. Typisch ist auch eine stärkere Betonung der Verantwortlichkeiten der Teams für die Cloudeinführung und die Cloudautomatisierung.

**Portfolioausrichtung:** Das IT-Portfolio wird sich wahrscheinlich auf Workloads und Workloadbesitzer konzentrieren, um kritische Entscheidungen zur Architektur zu fördern. Diese Teams werden wahrscheinlich mehr Wert in der Azure Architecture Framework-Anleitung während der Einführungs- und Betriebsaktivitäten finden.
**Definitionen der Grenzen:** Die logischen Grenzen, selbst auf Unternehmensebene, werden sich wahrscheinlich auf die Segmentierung von Produktions- und Nicht-Produktionsumgebungen konzentrieren. Es kann auch eine klare Segmentierung zwischen den Produkten im Softwareportfolio des Unternehmens geben. Gelegentlich kann es auch eine Segmentierung zwischen Entwicklung und gehosteten Kundeninstanzen geben.

### <a name="operations-led-portfolio"></a>Betriebsorientiertes Portfolio

Multinationale Unternehmensorganisationen mit größeren IT-Betriebsteams haben in der Regel einen stärkeren Fokus auf Governance und Betrieb als auf die Entwicklung. In diesen Organisationen richtet sich ein höherer Prozentsatz der Workloads üblicherweise nach den COTS- oder Problemlösungskategorien, die von den technischen Besitzern innerhalb des Cloudbetriebsteams verwaltet werden.

**Portfolioausrichtung:** Das IT-Portfolio wird an der Workload ausgerichtet, aber diese Workloads werden dann an die Betriebseinheiten oder Geschäftsbereiche angepasst. Möglicherweise erfolgt auch die Anordnung nach Finanzierungsmodellen, Branchen- oder anderen Anforderungen der Geschäftssegmentierung.
**Definitionen der Grenzen:** Zielzonen werden Anwendungen wahrscheinlich in Anwendungsarchetypen gruppieren, um ähnliche Vorgänge in einer ähnlichen Segmentierung zu belassen. Umgebungen werden sich wahrscheinlich auf physische Konstrukte wie Rechenzentren, Nationen, Cloudanbieterregionen oder andere betriebliche Organisationsstandards beziehen.

### <a name="migration-led-portfolio"></a>Migrationsorientiertes Portfolio

Ähnlich wie betriebsorientierte Portfolios wird ein Portfolio, das weitgehend durch Migration erstellt wird, auf bestimmten Geschäftsfaktoren basieren, die zur Migration bestehender Objekte geführt haben. Normalerweise ist das Rechenzentrum der größte Faktor für diese Treiber.

**Portfolioausrichtung:** Das IT-Portfolio ist möglicherweise an der Workload ausgerichtet, aber wahrscheinlicher an den Objekten. Wenn in der Geschichte des Unternehmens Übergänge zum IT-Betrieb stattgefunden haben, lassen sich viele aktiv genutzte Objekte möglicherweise nicht ohne weiteres einer geförderten Workload zuordnen. In diesen Fällen verfügen viele Objekte möglicherweise erst in einem späten Stadium des Migrationsprozesses über eine definierte Workload oder einen eindeutigen Besitzer der Workload.
**Definitionen der Grenzen:** Die Zielzonen werden die Anwendungen wahrscheinlich in solchen Begrenzungen gruppieren, die die lokale Segmentierung widerspiegeln. Obwohl es sich dabei nicht um eine bewährte Methode handelt, entsprechen die Umgebungen oft dem Namen des lokalen Rechenzentrums und den Zielzonen, die die Praktiken der Netzwerksegmentierung darstellen. Es ist eine bessere Methode, sich an eine Segmentierung zu halten, die sich enger an ein betriebsorientiertes Portfolio anlehnt.

### <a name="governance-led-portfolio"></a>Governanceorientiertes Portfolio

Die Ausrichtung auf Governanceteams sollte so früh wie möglich erfolgen. Durch die Verwendung von Governancemethoden und Cloudgovernancetools können Portfolios und umgebungsbezogenen Grenzen die Anforderungen von Innovation, Betrieb und Migration am besten ausgleichen.

- **Portfolioausrichtung:** Governanceorientierte Portfolios tendieren dazu, Datenpunkte zu enthalten, die Innovations- und Betriebsdetails erfassen, z. B. Workload, Betriebsbesitzer, Datenklassifizierung und betriebliche Wichtigkeit. Diese Datenpunkte schaffen eine abgerundete Sicht auf das Portfolio.
- **Definitionen der Grenzen:** Grenzen in einem governanceorientierten Portfolio tendieren dazu, Innovationen dem Betrieb vorzuziehen, während eine von der Verwaltungsgruppe gesteuerte Hierarchie verwendet wird, die sich an den Kriterien der Geschäftseinheit und der Entwicklungsumgebung orientiert. Auf jeder Ebene der Hierarchie kann eine Cloudgovernancegrenze unterschiedliche Grade der Richtlinienerzwingung erhalten, um Entwicklung und kreative Flexibilität zu gestatten. Gleichzeitig können Anforderungen an die Produktionsqualität auf Produktionsabonnements angewandt werden, um eine Trennung der Aufgaben und einen konsistenten Betrieb zu gewährleisten.
