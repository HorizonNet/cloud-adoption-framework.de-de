---
title: 'Erste Schritte: Aufbauen eines Cloudeinführungsteams'
description: Legen Sie zur Vorbereitung einer erfolgreichen Cloudeinführung den Aufgabenbereich, die Ziele und die Funktionen eines Cloudeinführungsteams fest.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 7a3e3eb6feec8fde3749e3204519f1859f19b280
ms.sourcegitcommit: c2249056464d748a6ce15c82cb35a9f164d8f661
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108197"
---
# <a name="get-started-build-a-cloud-adoption-team"></a>Erste Schritte: Aufbauen eines Cloudeinführungsteams

Cloudeinführungsteams sind das moderne Äquivalent zu technischen Implementierungs- oder Projektteams. Die Natur der Cloud kann dynamischere Teamstrukturen erfordern.

Einige Cloudeinführungsteams konzentrieren sich ausschließlich auf die Cloudmigration, andere Teams beschäftigen sich schwerpunktmäßig mit Innovationen, die Cloudtechnologien nutzen. Einige Teams verfügen über das umfassende technische Fachwissen, das erforderlich ist, um große Implementierungsbemühungen wie eine vollständige Rechenzentrumsmigration abzuschließen, andere Teams haben einen engeren technischen Schwerpunkt.

Ein kleineres Team kann zwischen Projekten wechseln, um bestimmte Ziele zu erreichen. Beispielsweise könnte sich ein Team von Datenplattformspezialisten darauf konzentrieren, bei der Konvertierung von virtuellen Computern (VMs) von SQL-Datenbank in SQL-PaaS-Instanzen zu helfen.

Beim Erweitern der Cloud profitieren Kunden von einem dedizierten Team für die [Cloudplattformfunktion](../../organize/cloud-platform.md). Dieses Team beschleunigt die erfolgreiche Einführung mit automatisierter Bereitstellung und Wiederverwendung von Code. Auf eine Cloudplattformfunktion konzentrierte Personen können Infrastruktur, Anwendungsmuster, Governance und andere unterstützende Ressourcen implementieren, um Effizienz und Konsistenz zu steigern und Cloudprinzipien in Ihrer Organisation zu etablieren. Kleine Organisationen und Einführungsteams können sich kein dediziertes Cloudplattformteam leisten. Sie sollten in Ihrem Einführungsteam eine Automatisierungsfunktion einrichten, um mit dem Aufbau dieses wichtigen „Cloudmuskels“ zu beginnen.

![Erste Schritte beim Aufbau eines Cloudeinführungsteams](../../_images/get-started/adoption-team-map.png)

## <a name="step-1-determine-the-type-of-adoption-team-you-need"></a>Schritt 1: Bestimmen der Art des benötigten Einführungsteams

Von Cloudeinführungsteams wird in der Regel mindestens eine der folgenden Arten von Einführungen durchgeführt:

- Migration vorhandener Workloads
- Modernisierung vorhandener Workloads und Ressourcen
- Architekturänderungen für vorhandene Workloads und Ressourcen
- Entwicklung neuer Workloads

Für die Einführung eines beliebigen IT-Portfolios wird üblicherweise eine Kombination dieser Maßnahmen benötigt. Leider sind für jeden Typ andere Fertigkeiten und Denkrichtungen erforderlich. Je höher die Spezialisierung eines Einführungsteams ist, desto effektiver und effizienter kann das Team die jeweilige Aufgabe bewältigen. Andererseits kann sich die Beherrschung aller Implementierungsoptionen des gesamten Cloudeinführungsspektrums als kaum lösbare Aufgabe für diese spezialisierteren Teams erweisen.

Orientieren Sie sich daher beim Aufbau eines Cloudeinführungsteams zunächst an einer der Einführungsmethoden, um die Entwicklung der Fähigkeiten des gesamten Teams zu beschleunigen.

**Ziele:**

- Ermitteln Sie, ob die Migrationsmethodik oder die Innovationsmethodik besser zum Team passt.
- Jede Methodik verfügt über ein vierstufiges Onboardingverfahren, das dem Team hilft, die Tools und Prozesse zu verstehen, die erforderlich sind, um diese Bestrebung optimal umzusetzen. Nehmen Sie sich als Team etwas Zeit, um anhand der ersten Schritte zu ermitteln, welche Tools und Szenarien Sie voraussichtlich in den ersten Iterationen benötigen.
- Zuordnen übergreifender Zuständigkeiten für Teams, indem eine sogenannte RACI-Matrix entwickelt und damit bestimmt wird, welche Teams *verantwortlich sind (responsible), rechenschaftspflichtig sind (accountable), konsultiert werden (consulted) und zu informieren sind (informed)* . Aktualisieren Sie die [RACI-Vorlage](../../organize/raci-alignment.md) Ihres Unternehmens, damit andere besser nachvollziehen können, wer dem Team angehört und auf welche Methodik sich das Team konzentriert.

**Hinweis zur Erreichung der Ziele:**

- In der [Übersicht über die Migrationsmethodik](../../migrate/index.md) werden der Prozess, die Tools und die Ansätze für die Migration und Modernisierung eines Portfolios von Workloads beschrieben.
- In der [Übersicht über die Innovationsmethodik](../../innovate/index.md) werden der Prozess, die Tools und die Ansätze zum Hinzufügen cloudnativer Workloads zum Portfolio beschrieben.
- Machen Sie sich mit den [Beweggründen](../../strategy/motivations.md) für diese Bestrebung vertraut, um zu ermitteln, ob sie eher zu Migrationsbestrebungen oder eher zu Innovationsbestrebungen passen.

## <a name="step-2-align-your-team-with-other-supporting-teams"></a>Schritt 2: Ausrichten Ihres Teams mit anderen unterstützenden Teams

Wenn die Cloudeinführungsbestrebung Ihres Unternehmens weit genug vorangeschritten ist, um über unterstützende Teams zu verfügen, finden Sie in der [RACI-Vorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx) Ihres Unternehmens ggf. eine Liste der Teams und Experten für Bereiche wie Cloudgovernance, Cloudbetrieb und Cloudkompetenzzentrum sowie andere ähnliche Teams.

**Ziele:**

- Machen Sie sich anhand des Entwurfsleitfadens sowie der operativen Baselines, Richtlinien und Prozesse der verschiedenen unterstützenden Teams mit den Leitlinien vertraut, die als Orientierungshilfe für die Cloudeinführung ausgearbeitet wurden.
- Sehen Sie sich die Orientierungshilfe mit anderen Cloudanführungsteams an, um Informationen zu möglichen Einschränkungen zu erhalten, die sich ggf. durch diese Leitlinien ergeben.

**Hinweis zur Erreichung der Ziele:**

- Unter [Auswerten der Unternehmensrichtlinie](../../govern/corporate-policy.md) werden die Schritte zum Definieren der Unternehmensrichtlinie beschrieben, durch die möglicherweise Entscheidungen eingeschränkt werden, die das Team gefahrlos in der Cloudumgebung des Unternehmens treffen kann.
- In den [Governancedisziplinen](../../govern/corporate-policy.md) werden die Arten von Kontrollen oder disziplinierten Prozessen beschrieben, die das Governanceteam wahrscheinlich implementiert hat, um eine sichere und konforme Cloudeinführung zu ermöglichen.
- In der [Verwaltungsmethodik](../../manage/index.md) werden die Überlegungen erläutert, die in eine Cloudbetriebsbaseline einfließen, um eine grundlegende Betriebsverwaltung bereitzustellen.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudstrategieteam ist über den gesamten Lebenszyklus der Cloudeinführung hinweg für eine klare RACI-Struktur zuständig. | Machen Sie sich mit den Angaben und Anforderungen folgender Teams/Stellen vertraut: <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung <li> Andere in der RACI-Vorlage aufgeführte Cloudeinführungsteams oder Personen |

## <a name="step-3-begin-your-adoption-journey"></a>Schritt 3: Starten des Einführungsprozesses

Abhängig von der Art des Einführungsteams, dem Sie angehören, beginnen Sie mit einem dieser Leitfäden:

- [Erste Schritte: Migrieren von Workloads zur Cloud](../migrate.md)
- [Erste Schritte: Erstellen neuer Produkte oder Dienste](../innovate.md)

Diese Leitfäden bieten Anleitungen für verschiedene Teams, die zusammen mit den unterschiedlichen Verantwortlichkeiten und Zuständigkeiten aufgeführt werden. Orientieren Sie sich an diesen Leitfäden, um die Rolle Ihres Teams in Relation zum restlichen Prozess zu verstehen. Sie geben auch Aufschluss über den Grad der Unterstützung, die Sie innerhalb des Unternehmens erwarten können.

Letztendlich ist das Cloudeinführungsteam für die Umsetzung zugewiesener Migrationsbestrebungen bzw. die Entwicklung neuer Produkte verantwortlich. Unterstützende Teams müssen zwar die Durchführung der einzelnen Schritte sicherstellen, es liegt jedoch in der Verantwortung des jeweiligen Cloudeinführungsteams, dafür zu sorgen, dass das unterstützende Team die Unterstützung erhält, die es benötigt, um erfolgreich zu sein. Wenn das verantwortliche Team noch nicht vorhanden ist oder mehr Unterstützung benötigt, um seine verantwortlichen Schritte zu erfüllen, wird das Einführungsteam ermutigt, sich mit anderen Teams zusammenzuschließen, um seine Ziele zu erreichen.

**Ziele:**

- Optimieren Sie die Umsetzung der zugehörigen Methodik für Ihren Einführungsansatz.
- Unterstützen Sie andere Teams bei der Durchführung ihrer verantwortlichen Schritte selbst dann, wenn diese Schritte Ihren Einführungsmaßnahmen im Wege stehen.

**Hinweis zur Erreichung der Ziele:**

- Im Leitfaden zu den ersten Schritten für die Migration ist das Einführungsteam für die Umsetzung von [Schritt 10: Migrieren Ihrer ersten Workload](../migrate.md#step-8-migrate-your-first-10-workloads) zuständig.
- Im Leitfaden zu den ersten Schritten für neue Produkte ist das Einführungsteam für die Umsetzung von [Schritt 8: Entwickeln innovativer Cloudlösungen](../innovate.md#step-8-innovate-in-the-cloud) zuständig.

Alle anderen Schritte in diesen Prüflisten dienen dazu, die Verwaltbarkeit der Bestrebung zu erleichtern.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team <li> Cloudstrategieteam |

## <a name="step-4-expand-your-skills-with-scenarios-and-best-practices"></a>Schritt 4: Erweitern Ihrer Kenntnisse mit Szenarien und bewährten Methoden

Nach ein oder zwei Iterationen ist das Cloudeinführungsteam mit den Grundlagen der primären Methodik vertraut. Nun ist das Team wahrscheinlich bereit für weitere Szenarien und für die Implementierung einiger zusätzlicher bewährter Methoden.

**Ziele:**

- Verbessern Sie die Kenntnisse und die Erfahrung, um sich komplexeren Einführungsszenarien widmen zu können.

**Hinweis zur Erreichung der Ziele:**

Das Team kann seine Fähigkeiten überprüfen und erweitern, indem es die folgenden Anleitungen durcharbeitet:

- Migrieren Sie neue Arten von Workloads, oder bewältigen Sie komplexere Migrationsherausforderungen durch [Szenarien](../../migrate/azure-best-practices/contoso-migration-overview.md) und [bewährte Methoden](../../migrate/azure-best-practices/index.md).
- Entwickeln Sie Innovationen mithilfe cloudnativer Lösungen, oder bewältigen Sie komplexere Innovationsherausforderungen durch [Szenarien](../../innovate/kubernetes/index.md) und [bewährte Methoden](../../innovate/best-practices/index.md).

**Verantwortliches Team:**

- Das Cloudeinführungsteam ist für die Erweiterung seiner Kenntnisse verantwortlich.

## <a name="step-5-build-a-cloud-adoption-factory"></a>Schritt 5: Aufbauen einer Cloudeinführungsfactory

Da das Team nach und nach immer besser in die verschiedenen Einführungsszenarien eingearbeitet ist, können Sie in kürzerer Zeit mehr erreichen. Dieser Abschnitt des Leitfadens hebt die Einführungsmöglichkeiten des Teams auf die nächste Stufe.

Der Ansatz der Cloudeinführungsfactory betrachtet die Prozesse hinter den Einführungsbestrebungen. Den Großteil des Zeitaufwands für die Migration und die Entwicklung von Innovationen machen die vielen Besprechungen aus, die auf mangelndes Verständnis oder mangelnde klare Kommunikation zurückzuführen sind. Eindeutig definierte Prozesse und Interaktionen für diverse Phasen der Cloudeinführung tragen dazu bei, kulturelle und politische Hindernisse zu beseitigen.

**Ziele:**

- Verbessern Sie die Umsetzungsprozesse, um eine stark optimierte Einführungsfactory aufzubauen.

**Hinweis zur Erreichung der Ziele:**

- Der Prozessleitfaden zur Unterstützung von [Migrationsbestrebungen](../../migrate/migration-considerations/index.md) befindet sich in der Migrationsmethodik im Abschnitt zu Prozessverbesserungen.
- In der Innovationsmethodik stehen [Innovationsprozesse](../../innovate/considerations/index.md) im Vordergrund, die zu weniger Technologie und zu einer effektiveren Produktentwicklung führen.

**Verantwortliches Team:**

- Das Cloudeinführungsteam ist für den Aufbau der Prozesse verantwortlich, die die Einführung noch weiter voranbringen.

## <a name="whats-next"></a>Nächste Schritte

Die Cloudeinführung ist ein erstrebenswertes Ziel, aber eine unkontrollierte Einführung kann zu unerwarteten Ergebnissen führen. Um die Einführung und die Anwendung bewährter Methoden zu beschleunigen und gleichzeitig unternehmerische sowie technische Risiken zu verringern, koordinieren Sie die Cloudeinführung mit [Cloudgovernancefunktionen](../../organize/cloud-governance.md).

Die Ausrichtung mit dem Cloudgovernanceteam sorgt für ein Gleichgewicht in Bezug auf die Cloudbereitstellungsmaßnahmen, aber dies gilt als MVP (Minimal Viable Product), da es möglicherweise nicht nachhaltig ist. Jedes Team hat mehrere Aufgaben, wie in den [RACI-Diagrammen](../../organize/raci-alignment.md) unten gezeigt wird.

Weitere Informationen zum Überwinden von [Antimustern in Organisationen: Silos und Machtbereiche](../../organize/fiefdoms-silos.md).
