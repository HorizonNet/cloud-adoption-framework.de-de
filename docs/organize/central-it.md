---
title: Grundlegendes zu den Aufgaben eines zentralen IT-Teams
description: Grundlegendes zu den Aufgaben des zentralen IT-Teams, einschließlich Quelle, Umfang, Zielvorgaben und Risiken.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: d83840a99d0a772ae449b5ae345cbdcb077a94a6
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85074749"
---
# <a name="central-it-team-functions"></a>Aufgaben des zentralen IT-Teams

Wenn die Cloudeinführung hochskaliert wird, reichen Cloudgovernancefunktionen allein möglicherweise nicht mehr aus, um das gesamte Einführungsprojekt zu regulieren. Wenn diese Einführung schrittweise erfolgt, entwickeln Teams meist nach und nach die Fähigkeiten und Prozesse, die sie für die Arbeit in der Cloud benötigen.

Wenn aber ein Cloudeinführungsteam die Cloud nutzt, um ein wichtiges und prestigeträchtiges Geschäftsergebnis zu erzielen, ist eine sukzessive Einführung selten der Fall. Erfolg zieht Erfolg nach sich. Dies gilt auch für die Cloudeinführung, dann aber im Maßstab der Cloud. Wenn mehrere Teams diesem einen Team relativ schnell bei der Cloudeinführung folgen, ist zusätzliche Unterstützung durch die vorhandenen IT-Mitarbeiter erforderlich. Diese Mitarbeiter verfügen aber möglicherweise nicht über die Kenntnisse und Erfahrung, um die Cloud mit cloudnativen IT-Tools zu unterstützen. Daher wird häufig ein zentrales IT-Team gebildet, das die Cloudnutzung steuert.

> [!CAUTION]
> Dies ist zwar ein gängiger Schritt im Reifeprozess, kann jedoch ein hohes Risiko für die Einführung bergen und Innovationen und Migrationsaufgaben blockieren, wenn er nicht effektiv ausgeführt wird. Im Abschnitt zu Risiken weiter unten in diesem Artikel erfahren Sie, wie Sie das Risiko minimieren, dass die Zentralisierung ein kulturelles Antimuster wird.

Die für die Bereitstellung zentralisierter IT-Funktionen erforderlichen Qualifikationen können bereitgestellt werden durch:

- Ein vorhandenes zentrales IT-Team
- Unternehmensarchitekten
- IT-Abläufe
- IT-Governance
- IT-Infrastruktur
- Netzwerk
- Identity
- Virtualisierung
- Business Continuity & Disaster Recovery
- Anwendungsbesitzer im IT-Bereich

> [!WARNING]
> Zentralisierte IT-Aufgaben sollten nur dann in der Cloud zum Tragen kommen, wenn die vorhandene lokale Bereitstellung auf einem zentralisierten IT-Teammodell basiert. Wenn das aktuelle lokale Modell auf delegierter Steuerung basiert, ziehen Sie ein Cloudkompetenzzentrum in Betracht, das eine besser für die Cloud geeignete Alternative darstellen kann.

## <a name="key-responsibilities"></a>Wichtige Zuständigkeiten

Passen Sie vorhandene IT-Verfahren an, um sicherzustellen, dass ein Cloudeinführungsprojekt zu sorgfältig regulierten und verwalteten Umgebungen in der Cloud führt.

Die folgenden Aufgaben werden normalerweise regelmäßig ausgeführt:

### <a name="strategic-tasks"></a>Strategische Aufgaben

- Überprüfung:
  - [Geschäftsergebnisse](../strategy/business-outcomes/index.md).
  - [Finanzmodelle](../strategy/financial-models.md).
  - [Gründe für die Cloudeinführung](../strategy/motivations.md).
  - [Geschäftsrisiken](../govern/policy-compliance/risk-tolerance.md).
  - [Rationalisierung der digitalen Ressourcen](../digital-estate/index.md).
- Überwachung von Einführungsplänen und Fortschritten anhand des [priorisierten Migrationsbacklogs](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Identifizieren und priorisieren Sie Plattformänderungen, die zur Unterstützung des Migrationsbacklogs erforderlich sind.
- Agieren Sie als Vermittler zwischen den Anforderungen einer Cloudeinführung und den vorhandenen IT-Teams.
- Nutzen Sie die Fähigkeiten vorhandener IT-Teams, um Plattformfunktionen schneller umzusetzen und die Einführung zu ermöglichen.

### <a name="technical-tasks"></a>Technische Aufgaben

- Erstellen und Warten der Cloudplattform zur Unterstützung von Lösungen.
- Definieren und Implementieren der Plattformarchitektur.
- Betreiben und Verwalten der Cloudplattform.
- Kontinuierliches Verbessern der Plattform.
- Auf dem Laufenden bleiben mit neuen Innovationen in der Cloudplattform.
- Bereitstellen neuer Cloudfunktionen zur Unterstützung der Wertschöpfung im Unternehmen.
- Empfehlen von Self-Service-Lösungen
- Sicherstellen, dass Lösungen die bestehenden Governance- und Complianceanforderungen erfüllen.
- Erstellen und Validieren der Bereitstellung der Plattformarchitektur
- Überprüfen der Releasepläne für Quellen neuer Plattformanforderungen

## <a name="meeting-cadence"></a>Rhythmus von Besprechungen

Das Know-how des zentralen IT-Teams stammt in der Regel aus einem bestehenden Arbeitsteam. Instruieren Sie die Beteiligten, dass sie einen Großteil ihrer täglichen Arbeitszeit der Ausrichtung widmen müssen. Beiträge sind nicht auf Besprechungen und Feedbackzyklen beschränkt.

## <a name="central-it-team-risks"></a>Risiken bei zentralen IT-Teams

Jede Cloudfunktion und alle Phasen der Organisationsreife sind durch das Wort „Cloud“ markiert. Die einzige Ausnahme ist das zentrale IT-Team. Die zentralisierte IT-Verwaltung war die vorherrschende Herangehensweise, als alle IT-Ressourcen an einigen wenigen Standorten untergebracht, von wenigen Teams verwaltet und über eine einzige Plattform zur Betriebsverwaltung gesteuert werden konnten. Durch die Globalisierung und die digitale Wirtschaft wurde die Anzahl von Instanzen solcher zentral verwalteten Umgebungen drastisch reduziert.

Aus moderner Sicht sind IT-Ressourcen global verteilt. Zuständigkeiten werden delegiert. Die Betriebsverwaltung erfolgt durch eine Kombination aus internen Mitarbeitern, Anbietern verwalteter Dienste und Cloudanbietern. In der digitalen Wirtschaft werden IT-Verwaltungsfunktionen langsam durch ein Modell mit self-service-basierten und delegierten Steuerungsfunktionen ersetzt, das klare Leitlinien für die Durchsetzung von Governance aufweist. Ein zentrales IT-Team kann einen wertvollen Beitrag zur Cloudeinführung leisten, indem es zum Cloudbroker und Partner für Innovationen und geschäftliche Agilität wird.

Ein zentrales IT-Team ist gut aufgestellt, um wertvolle Kenntnisse und Vorgehensweisen aus den vorhandenen lokalen Modellen zu extrahieren und auf die Cloudbereitstellung zu übertragen. Aber dieser Prozess erfordert Änderungen. Um die Cloudeinführung in großem Umfang zu unterstützen, sind neue Prozesse, neue Fähigkeiten und neue Tools erforderlich. Wenn sich ein zentrales IT-Team an diese Anforderungen anpassen kann, wird es bei einem Cloudeinführungsprojekt zu einem wichtigen Partner. Wenn das zentrale IT-Team diese Anpassung nicht schafft oder versucht, die Cloud als Katalysator für eine sehr differenzierte Steuerung zu nutzen, wird es schnell zu einem Hindernis für Einführung, Innovation und Migration.

Dieses Risiko lässt sich anhand von Geschwindigkeit und Flexibilität ermessen. Die Cloud vereinfacht die schnelle Einführung neuer Technologien. Wenn neue Cloudfunktionen innerhalb weniger Minuten bereitgestellt werden können, aber das zentrale IT-Team Wochen oder sogar Monate benötigt, um diese zu prüfen, blockieren diese zentralisierten Prozesse den Geschäftserfolg. In diesem Fall sollten Sie alternative Strategien für die IT-Bereitstellung bedenken.

### <a name="exceptions"></a>Ausnahmen

In vielen Branchen ist eine strikte Einhaltung von Complianceanforderungen von dritter Seite erforderlich. Für einige dieser Anforderungen ist weiterhin eine zentralisierte IT-Steuerung notwendig. Die Erfüllung dieser Compliancevorgaben kann den Bereitstellungsprozess verlängern, insbesondere dann, wenn neue Technologien ins Spiel kommen, die noch nicht flächendeckend eingesetzt werden. In solchen Szenarien müssen Sie in den Frühphasen der Einführung mit Verzögerungen der Bereitstellung rechnen. Ähnliche Situationen können bei Unternehmen auftreten, die vertrauliche Kundendaten verarbeiten, aber möglicherweise keine Complianceanforderungen einer dritten Seite erfüllen müssen.

### <a name="operate-within-the-exceptions"></a>Arbeiten innerhalb der Ausnahmen

Wenn zentrale IT-Prozesse erforderlich sind und zu zusätzlichen Prüfpunkten bei der Einführung neuer Technologien führen, können diese Prüfpunkte dennoch schnell umgesetzt werden. Governance- und Complianceanforderungen sind dafür konzipiert, vertrauliche Aspekte zu schützen, sie sollen keinen Rundumschutz für alles und jedes bieten. Die Cloud bietet einfache Mechanismen zum Erwerben und Bereitstellen isolierter Ressourcen bei gleichzeitiger Einhaltung der jeweils geltenden Leitlinien.

Ein ausgereiftes zentrales IT-Team behält die notwendigen Schutzmaßnahmen bei, handelt aber Verfahren aus, die Innovationen ermöglichen. Um einen solchen Reifegrad zu demonstrieren, ist eine ordnungsgemäße Klassifizierung und Isolierung von Ressourcen erforderlich.

### <a name="example-narrative-of-operating-within-exceptions-to-empower-adoption"></a>Beispiel für einen IT-Betrieb in Ausnahmesituationen zur Unterstützung der Cloudeinführung

Dieser Beispielbericht veranschaulicht den Ansatz, den ein erfahrenes zentrales IT-Team beim fiktiven Unternehmen Contoso gewählt hat, um die Einführung zu realisieren.

Contoso hat ein zentrales IT-Teammodell für die Unterstützung der Cloudressourcen des Unternehmens eingeführt. Um dieses Modell bereitzustellen, hat das Unternehmen strikte Kontrollen für verschiedene gemeinsam genutzte Dienste wie eingehende Netzwerkverbindungen implementiert. Dank dieses klugen Schachzugs konnte Contoso, LLC die Risiken für die Cloudumgebung senken und ein einzelnes Gerät bereitstellen, das beim Auftreten einer Sicherheitsverletzung sämtlichen Datenverkehr blockiert. Die Sicherheitsbaseline des Unternehmens gibt vor, dass sämtlicher eingehender Datenverkehr durch ein freigegebenes Gerät fließen muss, das vom zentralen IT-Team verwaltet wird.

Nun benötigt aber eins der Cloudeinführungsteams eine Umgebung mit einer dedizierten und speziell konfigurierten eingehenden Netzwerkverbindung, um eine bestimmte Cloudtechnologie zu nutzen. Ein zentrales IT-Team, das noch nicht den entsprechenden Reifegrad aufweist, würde diese Anforderung einfach ablehnen und die vorhandenen Prozesse über die Einführungsanforderungen stellen. Das zentrale IT-Team von Contoso reagierte anders. Das Team hat schnell eine einfache, vierteilige Lösung für dieses Dilemma gefunden:

  1. **Klassifizierung**: Da das Cloudeinführungsteam sich in der Frühphase der neuen Lösung befand und keine vertraulichen Daten oder unternehmenskritischen Anforderungen vorhanden waren, wurden die Ressourcen in der Umgebung als risikoarm und nicht kritisch eingestuft. Eine effektive Klassifizierung ist ein Zeichen für den Reifegrad eines zentralen IT-Teams. Wenn alle Ressourcen und Umgebungen klassifiziert werden, können klarere Richtlinien eingerichtet werden.
  1. **Verhandlung**: Eine Klassifizierung allein ist nicht ausreichend. Gemeinsam genutzte Dienste wurden implementiert, um vertrauliche und unternehmenskritische Ressourcen konsistent betreiben zu können. Eine Änderung der Regeln würde die Governance- und Compliancerichtlinien gefährden, die für diejenigen Ressourcen eingerichtet wurde, die einen höheren Schutz benötigen. Die Unterstützung einer Cloudeinführung darf nicht auf Kosten der Stabilität, Sicherheit oder Governance erfolgen. Dies führte zu Verhandlungen mit dem Einführungsteam, um bestimmte Fragen zu beantworten. Kann ein unternehmensgeführtes DevOps-Team die betriebliche Verwaltung für diese Umgebung übernehmen? Würde diese Lösung direkten Zugriff auf andere interne Ressourcen erfordern? Wenn das Cloudeinführungsteam mit diesen Kompromissen einverstanden ist, kann eingehender Datenverkehr möglich sein.
  1. **Isolierung**: Da die geschäftliche Seite selbst eine fortlaufende Betriebsverwaltung bereitstellen kann und die Lösung nicht von direktem Datenverkehr zu anderen internen Ressourcen abhängig ist, kann die Lösung in einem neuen, getrennten Abonnement eingerichtet werden. Dieses Abonnement wird auch einem separaten Knoten der neuen Verwaltungsgruppenhierarchie hinzugefügt.
  1. **Automatisierung:** Ein weiteres Zeichen für den Grad der Ausgereiftheit in diesem Team sind die Automatisierungsprinzipien. Das Team nutzt Azure Policy, um die Richtliniendurchsetzung zu automatisieren. Es verwendet auch Azure Blueprints, um die Bereitstellung allgemeiner Plattformkomponenten zu automatisieren und die Einhaltung der definierten Identitätsbaseline zu erzwingen. Für dieses und weitere Abonnements in der neuen Verwaltungsgruppe gelten geringfügig andere Richtlinien und Vorlagen. Richtlinien, die die eingehende Datenverkehrsbandbreite blockieren würden, wurden aufgehoben. Sie wurden durch Anforderungen ersetzt, den Datenverkehr – wie jeden eingehenden Datenverkehr – durch ein Abonnement mit gemeinsam genutzten Diensten zu leiten, um eine Datenverkehrsisolierung zu erzwingen. Da die lokalen Tools für die Betriebsverwaltung nicht auf dieses Abonnement zugreifen können, werden auch keine Agents für diese Tools mehr benötigt. Alle weiteren Governanceleitlinien, die von anderen Abonnements in der Verwaltungsgruppenhierarchie benötigt werden, gelten weiterhin und bieten ausreichenden Schutz.

Der ausgereifte, kreative Ansatz des zentralen IT-Teams von Contoso sorgte für eine Lösung, die weder Governance noch Compliance gefährdete und denn die Einführung förderte. Dieser Ansatz, die zentralisierte IT eher in Form von Brokerdiensten als durch Besitz cloudnativer Funktionen zu gestalten, ist der erste Schritt auf dem Weg zu einem Cloudkompetenzzentrum (CCoE). Auf diese Weise können vorhandene Richtlinien schnell weiterentwickelt werden, sodass je nach Bedarf eine zentralisierte Kontrolle ausgeübt werden kann oder – wenn mehr Flexibilität akzeptabel ist – Governanceleitlinien zur Anwendung kommen. Indem diese beiden Überlegungen sorgfältig gegeneinander abgewogen werden, lassen sich die Risiken minimieren, die mit einer zentralisierten IT-Verwaltung in der Cloud einhergehen.

## <a name="next-steps"></a>Nächste Schritte

- Wenn ein zentrales IT-Team in der Cloud einen gewissen Reifegrad erreicht hat, besteht der nächste Schritt im Prozess typischerweise in einer lockeren Kopplung von Cloudvorgängen. Die Verfügbarkeit von cloudnativen Tools für die Betriebsverwaltung und die geringeren Betriebskosten für PaaS-zentrierte Lösungen führen häufig dazu, dass Geschäftsteams (genauer gesagt DevOps-Teams auf geschäftlicher Seite) die Verantwortung für Cloudvorgänge übernehmen.

Weitere Informationen:

- [Aufbauen eines Cloudbetriebsteams](../get-started/team/cloud-operations.md)
- [Cloudbetriebsfunktionen](./cloud-operations.md)
