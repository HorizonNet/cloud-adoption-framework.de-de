---
title: 'Erste Schritte: Aufbauen eines Cloudeinführungsteams'
description: Legen Sie zur Vorbereitung einer erfolgreichen Cloudeinführung den Aufgabenbereich, die Ziele und die Funktionen eines Cloudeinführungsteams fest.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 04/04/2020
ms.openlocfilehash: cb831deaf758d26d15df0d8797f6fda7d0e8dfbf
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230414"
---
# <a name="get-started-build-a-cloud-adoption-team"></a>Erste Schritte: Aufbauen eines Cloudeinführungsteams

Cloudeinführungsteams sind das moderne Äquivalent zu technischen Implementierungs- oder Projektteams. Die Charakteristik der Cloud kann jedoch eine dynamischere Teamstruktur erfordern. Einige Cloudeinführungsteams konzentrieren sich ausschließlich auf die Cloudmigration, während andere Teams sich schwerpunktmäßig mit Innovationen beschäftigen, die Cloudtechnologien nutzen. Einige Teams verfügen über das breite technische Fachwissen, das erforderlich ist, um umfangreiche Einführungsbestrebungen wie eine vollständige Rechenzentrumsmigration durchzuführen, während andere einen engeren technischen Fokus haben und mitunter zwischen Projekten wechseln, um bestimmte Ziele zu erreichen. Ein Beispiel wäre etwa ein Team von Datenplattformspezialisten, das bei der Konvertierung virtueller SQL-Computer in SQL-PaaS-Instanzen mitwirkt.

![Erste Schritte beim Aufbau eines Cloudeinführungsteams](../../_images/get-started/adoption-team-map.png)

## <a name="step-1-determine-the-type-of-adoption-team-you-need"></a>Schritt 1: Bestimmen der Art des benötigten Einführungsteams

Von Cloudeinführungsteams wird in der Regel mindestens eine der folgenden Arten von Einführungen durchgeführt:

    - Migration vorhandener Workloads
    - Modernisierung vorhandener Workloads und Ressourcen
    - Architekturänderungen für vorhandene Workloads und Ressourcen
    - Entwicklung neuer Workloads

Für die Einführung eines beliebigen IT-Portfolios wird üblicherweise eine Kombination dieser Fähigkeiten benötigt. Unglücklicherweise erfordern diese unterschiedlichen Bestrebungen jeweils unterschiedliche Fähigkeiten und Ansätze. Je höher die Spezialisierung eines Einführungsteams im Zusammenhang mit diesen Bestrebungen, desto effektiver und effizienter kann das Team die jeweilige Aufgabe bewältigen. Andererseits kann sich die Beherrschung aller Implementierungsoptionen des gesamten Cloudeinführungsspektrums als kaum lösbare Aufgabe erweisen.

Orientieren Sie sich daher beim Aufbau eines Cloudeinführungsteams zunächst an einer der Einführungsmethoden, um die Entwicklung der Fähigkeiten des gesamten Teams zu beschleunigen.

**Ziele:**

- Ermitteln Sie, welche Methodik am besten zum Team passt: die Migrationsmethodik oder die Innovationsmethodik.
- Jede Methodik verfügt über ein vierstufiges Onboardingverfahren zur Vermittlung grundlegender Kenntnisse für die Tools und Prozesse, die erforderlich sind, um diese Bestrebung optimal umzusetzen. Nehmen Sie sich als Team etwas Zeit, um anhand der ersten Schritte zu ermitteln, welche Tools und Szenarien Sie voraussichtlich in den ersten Iterationen benötigen.
- Aktualisieren Sie die [RACI-Vorlage](../../organize/raci-alignment.md) Ihres Unternehmens, damit andere besser nachvollziehen können, wer dem Team angehört und auf welche Methodik sich das Team konzentriert.

**Hinweis zur Erreichung der Ziele:**

- In der [Übersicht über die Migrationsmethodik](../../migrate/index.md) werden der Prozess, die Tools und die Ansätze für die Migration und Modernisierung eines Portfolios von Workloads beschrieben.
- In der [Übersicht über die Innovationsmethodik](../../innovate/index.md) werden der Prozess, die Tools und die Ansätze zum Hinzufügen cloudnativer Workloads zum Portfolio beschrieben.
- Machen Sie sich mit den [Beweggründen](../../strategy/motivations.md) für diese Bestrebung vertraut, um zu ermitteln, ob sie eher zu Migrationsbestrebungen oder eher zu Innovationsbestrebungen passen.

## <a name="step-2-align-your-team-to-other-supporting-teams"></a>Schritt 2: Ausrichten Ihres Teams an anderen unterstützenden Teams

Wenn die Cloudeinführungsbestrebung Ihres Unternehmens weit genug vorangeschritten ist, um über unterstützende Teams zu verfügen, finden Sie in der [RACI-Vorlage](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) Ihres Unternehmens ggf. eine Liste der Teams und Experten für Bereiche wie Cloudgovernance, Cloudbetrieb und Cloudkompetenzzentrum sowie andere ähnliche Teams.

**Ziele:**

- Machen Sie sich anhand des Entwurfsleitfadens sowie der operativen Baselines, Richtlinien und Prozesse der verschiedenen unterstützenden Teams mit den Leitlinien vertraut, die als Orientierungshilfe für die Cloudeinführung ausgearbeitet wurden.
- Sehen Sie sich die Orientierungshilfe mit anderen Cloudanführungsteams an, um Informationen zu möglichen Einschränkungen zu erhalten, die sich ggf. durch diese Leitlinien ergeben.

**Hinweis zur Erreichung der Ziele:**

- Unter [Auswerten der Unternehmensrichtlinie](../../govern/corporate-policy.md) werden die Schritte zum Definieren der Unternehmensrichtlinie beschrieben, durch die möglicherweise Entscheidungen eingeschränkt werden, die gefahrlos in der Cloudumgebung des Unternehmens getroffen werden können.
- In den [Governancedisziplinen](../../govern/corporate-policy.md) werden die Arten von Kontrollen oder disziplinierten Prozessen beschrieben, die das Governanceteam wahrscheinlich implementiert hat, um eine sichere und konforme Cloudeinführung zu ermöglichen.
- In der [Verwaltungsmethodik](../../manage/index.md) werden die Überlegungen erläutert, die in eine Cloudbetriebsbaseline einfließen, um eine grundlegende Betriebsverwaltung bereitzustellen.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Das Cloudstrategieteam ist über den gesamten Lebenszyklus der Cloudeinführung hinweg für eine klare RACI-Struktur zuständig. | Machen Sie sich mit den Angaben und Anforderungen folgender Teams/Stellen vertraut: <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung <li> Andere in der RACI-Vorlage aufgeführte Cloudeinführungsteams oder Personen |

## <a name="step-3-begin-your-adoption-journey"></a>Schritt 3: Starten des Einführungsprozesses

Abhängig von der Art des Einführungsteams, dem Sie angehören, beginnen Sie mit einem von zwei Prozessen:

- Erste Schritte: Migrieren von Workloads zur Cloud
- Erste Schritte: Erstellen neuer Produkte oder Dienste

In diesen Leitfäden sind jeweils Informationen für verschiedene Teams mit variierendem Zuständigkeits- und Verantwortlichkeitsgrad angegeben. Orientieren Sie sich an diesen Angaben, um die Rolle Ihres Teams in Relation zum restlichen Prozess zu verstehen. Darüber hinaus geben diese Referenzen Aufschluss über den Grad der Unterstützung, die Sie innerhalb des Unternehmens erhalten.

Letztendlich ist das Cloudeinführungsteam für die Umsetzung zugewiesener Migrationsbestrebungen bzw. die Entwicklung neuer Produkte verantwortlich. Unterstützende Teams müssen zwar die Durchführung von Schritten sicherstellen, es liegt jedoch in der Verantwortung des jeweiligen Cloudeinführungsteams, dafür zu sorgen, dass sie die Unterstützung erhalten, die sie benötigen, um erfolgreich zu sein. Das Einführungsteam sollte bei der Durchführung dieser Schritte möglichst mit anderen Teams zusammenarbeiten, falls das verantwortliche Team nicht vorhanden ist oder mehr Unterstützung bei der Bewältigung der Schritte benötigt, für die es zuständig ist.

**Ziele:**

- Optimieren Sie die Umsetzung der zugehörigen Methodik für Ihren Einführungsansatz.
- Unterstützen Sie andere Teams bei der Durchführung ihrer Schritte, wenn diese Schritte Ihrer Einführung im Wege stehen.

**Hinweis zur Erreichung der Ziele:**

- Im Leitfaden zu den ersten Schritten für die Migration ist das Einführungsteam für die Umsetzung von [Schritt 10: Migrieren Ihrer ersten Workload](../migrate.md#step-8-migrate-your-first-10-workloads) zuständig.
- Im Leitfaden zu den ersten Schritten für neue Produkte ist das Einführungsteam für die Umsetzung von [Schritt 8: Entwickeln innovativer Cloudlösungen](../innovate.md#step-8-innovate-in-the-cloud) zuständig.

Alle anderen Schritte in diesen Prüflisten dienen dazu, die Verwaltbarkeit der Bestrebung zu erleichtern.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Letztendlich ist das Cloudeinführungsteam für den Erfolg verantwortlich. | <li> Cloudgovernanceteam <li> Cloudbetriebsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung <li> Cloudstrategieteam |

## <a name="step-4-expand-your-skills-with-scenarios-and-best-practices"></a>Schritt 4: Erweitern Ihrer Kenntnisse mit Szenarien und bewährten Methoden

Nach ein, zwei Einführungsiterationen ist das Team mit den Grundlagen der primären Einführungsmethodik vertraut. Nun ist das Team wahrscheinlich bereit für weitere Szenarien und für die Implementierung einiger zusätzlicher bewährter Methoden. Die folgenden Links führen jeweils zu einer Seite für einen Abschnitt des Inhaltsverzeichnisses. Anhand der dort bereitgestellten Listen kann sich das Team mit beiden Arten von Informationen vertraut machen und seine Kenntnisse erweitern.

**Ziele:**

- Verbessern Sie die Kenntnisse und die Erfahrung, um sich komplexeren Einführungsszenarien widmen zu können.

**Hinweis zur Erreichung der Ziele:**

- Migrieren Sie neue Arten von Workloads, oder bewältigen Sie komplexere Migrationsherausforderungen durch [Szenarien](../../migrate/azure-best-practices/contoso-migration-overview.md) und [bewährte Methoden](../../migrate/azure-best-practices/index.md).
- Entwickeln Sie innovative cloudnative Lösungen, oder bewältigen Sie komplexere Innovationsherausforderungen durch [Szenarien](../../innovate/kubernetes/index.md) und [bewährte Methoden](../../innovate/best-practices/index.md).

**Verantwortliches Team:**

Das Cloudeinführungsteam ist für die Erweiterung der Kenntnisse verantwortlich.

## <a name="step-5-build-a-cloud-adoption-factory"></a>Schritt 5: Aufbauen einer Cloudeinführungsfactory

Da das Team nach und nach immer besser in die verschiedenen Einführungsszenarien eingearbeitet ist, können Sie in kürzerer Zeit mehr erreichen. Dieser Abschnitt hebt Ihre Einführungsmöglichkeiten auf die nächste Stufe. Der Ansatz der Cloudeinführungsfactory betrachtet die Prozesse hinter den Einführungsbestrebungen. Den Großteil des Zeitaufwands für die Migration und die Entwicklung von Innovationen machen die vielen Besprechungen aus, die auf mangelndes Verständnis oder mangelnde Transparenz zurückzuführen sind. Eindeutig definierte Prozesse und Interaktionen für diverse Phasen der Cloudeinführung tragen dazu bei, kulturelle und politische Hindernisse zu beseitigen.

**Ziele:**

- Verbessern Sie die Umsetzungsprozesse, um eine stark optimierte Einführungsfactory aufzubauen.

**Hinweis zur Erreichung der Ziele:**

- Der Prozessleitfaden zur Unterstützung von [Migrationsbestrebungen](../../migrate/migration-considerations/index.md) befindet sich in der Migrationsmethodik im Abschnitt zu Prozessverbesserungen.
- In der Innovationsmethodik stehen [Innovationsprozesse](../../innovate/considerations/index.md) im Vordergrund, die zu weniger Technologie und zu einer effektiveren Produktentwicklung führen.

**Verantwortliches Team:**

Das Cloudeinführungsteam ist für den Aufbau der Prozesse verantwortlich, die die Einführung noch weiter voranbringen.

## <a name="whats-next"></a>Nächste Schritte

Die Einführung ist großartig, aber eine unkontrollierte Einführung kann zu unerwarteten Ergebnissen führen. Koordinieren Sie die Cloudeinführung mit [Cloudgovernancefunktionen](../../organize/cloud-governance.md), um die Einführung und die Anwendung bewährter Methoden zu beschleunigen und gleichzeitig unternehmerische sowie technische Risiken zu verringern.

Diese beiden Teams sorgen zwar für ein ausgewogenes Verhältnis von Cloudeinführungsbestrebungen, dies wird jedoch als MVP betrachtet, da das Ergebnis möglicherweise nicht nachhaltig ist. Jedes Team hat viele Aufgaben, wie in den [RACI-Diagrammen (_Responsible, Accountable, Consulted, Informed_)](../../organize/raci-alignment.md) erläutert wird.

Weitere Informationen finden Sie unter [Antimuster in Unternehmen: Silos und Machtbereiche](../../organize/fiefdoms-silos.md).
