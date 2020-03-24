---
title: Vorbereiten auf die Komplexität beim flexiblen Change Management
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um Cloudarchitekten auf den Austausch mit dem Projektmanagement vorzubereiten, bei dem es um Change Management geht.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3e2b9139fa4774549f68ccf3762234bc755fd458
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311828"
---
<!-- cSpell:ignore ITSM TOGAF -->

# <a name="prepare-for-technical-complexity-agile-change-management"></a>Vorbereiten der technischen Komplexität: Agile Change Management

Wenn mit nur einer Codezeile die Bereitstellung eines kompletten Rechenzentrums aufgehoben und neu erstellt werden kann, können herkömmliche Verfahren nicht mehr mithalten. Die Anleitungen im Cloud Adoption Framework basieren u. a. auf Methoden wie dem IT-Service-Management (ITSM) oder dem Open Group Architecture Framework (TOGAF). Um allerdings auch bei geschäftlichen Änderungen flexibel und reaktionsfähig zu bleiben, werden diese Methoden in diesem Framework an Agile-Verfahren und DevOps-Ansätze angepasst.

Beim Umstieg auf ein Agile-Modell mit Schwerpunkt auf Flexibilität und Iterationen werden die technische Komplexität und das Change Management anders behandelt als beim herkömmlichen Wasserfallmodell mit einer linearen Folge von Migrationsschritten. In diesem Artikel wird ein allgemeiner Ansatz für das Change Management in einem Agile-basierten Migrationsablauf beschrieben. Am Ende dieses Artikels verfügen Sie über allgemeine Kenntnisse über die Ebenen des Change Managements und die Dokumentation bei einem inkrementellen Migrationsansatz. Um basierend auf diesen Kenntnissen Agile-Methoden umzusetzen, sind weitere Schulungen und Entscheidungen erforderlich. Mit diesem Artikel sollen Cloudarchitekten auf Gespräche mit dem Projektmanagement vorbereitet werden, um diesen das allgemeine Konzept des Change Managements bei dieser Vorgehensweise zu erläutern.

## <a name="address-technical-complexity"></a>Erläutern der technischen Komplexität

Wenn technische Systeme geändert werden, können Komplexität und gegenseitige Abhängigkeiten Risiken für die Projektpläne darstellen. Cloudmigrationsvorgänge sind da keine Ausnahme. Beim Verschieben von Tausenden – oder Zehntausenden – von Ressourcen in die Cloud steigern sich diese Risiken noch einmal. Die Erkennung und Zuordnung aller Abhängigkeiten bei großen digitalen Umgebungen könnte Jahre dauern. Nur wenige Unternehmen können sich einen derartig langen Zyklus erlauben. Um die Notwendigkeiten für Architekturanalyse und Geschäftsbeschleunigung abzugleichen, liegt der Fokus beim Framework für die Cloudeinführung bei der Verwaltung des Product Backlogs auf einem „INVEST-Modell“. In den folgenden Abschnitten wird dieser Modelltyp zusammengefasst.

## <a name="invest-in-workloads"></a>INVEST-Modell bei Workloads

Der Begriff _Workload_ taucht im Cloud Adoption Framework immer wieder auf. Eine Workload ist eine Einheit von Anwendungsfunktionalität, die zur Cloud migriert werden kann. Dabei kann es sich um eine einzelne Anwendung, eine Anwendungsebene oder eine Sammlung einer Anwendung handeln. Die Definition ist flexibel und kann während der verschiedenen Phasen der Migration variieren. Im Cloud Adoption Framework wird zur Definition einer Workload der Begriff _INVEST_ verwendet.

INVEST ist ein allgemeines Akronym bei vielen Agile-Verfahren, um User Storys oder Product Backlog Items zu schreiben, bei denen es sich jeweils um Ausgabeeinheiten von Agile-Projektverwaltungstools handelt. Die messbare Einheit der Ausgabe einer Migration ist eine migrierte Workload. Im Cloud Adoption Framework wird das Akronym INVEST etwas anders verwendet, um Workloads zu definieren:

- **Independent** (Unabhängig): Eine Workload sollte keine Abhängigkeiten enthalten, auf die nicht zugegriffen werden kann. Damit eine Workload als migriert bezeichnet werden kann, muss auf alle Abhängigkeiten, die in der Migration enthalten sind, zugegriffen werden können.
- **Negotiable** (Verhandelbar): Wenn eine zusätzliche Ermittlung erfolgt, ändert sich die Definition einer Workload. Die Architekten, die die Migration planen, können einzelne Faktoren in Bezug auf Abhängigkeiten verhandeln. Beispiele für die Verhandlungspunkte sind etwa das Vorabveröffentlichen von Funktionen, das Verfügbarmachen einzelner Funktionen über ein Hybridnetzwerk oder das Packen aller Abhängigkeiten in einem einzigen Release.
- **Valuable** (Hilfreich): Der Wert wird in einer Workload durch die Möglichkeit gemessen, Benutzern den Zugriff auf eine Produktionsworkload bereitzustellen.
- **Estimable** (Schätzbar): Abhängigkeiten, Ressourcen, Migrationsdauer, Leistung und Cloudkosten sollten abschätzbar sein und vor der Migration geschätzt werden.
- **Small** (Klein): Ziel ist es, Workloads in einem einzigen Sprint zu packen. Allerdings ist dies unter Umständen nicht immer möglich. Stattdessen sollten die Teams Sprints und Releases planen, um die erforderliche Zeit zum Verschieben einer Workload in die Produktion zu minimieren.
- **Testable** (Testbar): Es sollten stets Verfahren zum Testen oder Validieren des Abschlusses der Migration einer Workload definiert werden.

Dieses Akronym dient nicht als Grundlage für strikte Einhaltung, sondern als Richtlinie für die Definition des Begriffs _Workload_.

## <a name="migration-backlog-aligning-business-priorities-and-timing"></a>Migrationsbacklog: Anpassen von Geschäftsprioritäten und zeitlichem Ablauf

Mit dem Migrationsbacklog können Sie das Portfolio der wichtigsten Workloads für die Migration nachverfolgen. Vor der Migration sollten die Teams für die Cloudstrategie und die Cloudeinführung den aktuellen [digitalen Status](../../../digital-estate/index.md) bewerten und sich auf eine priorisierte Liste mit Workloads für die Migration einigen. Diese Liste bildet die Grundlage für das anfängliche Migrationsbacklog.

Anfangs entsprechen die Workloads im Migrationsbacklog den im vorherigen Abschnitt beschriebenen INVEST-Kriterien sicherlich noch nicht. Sie dienen stattdessen als eine logische Gruppierung von Ressourcen aus einem anfänglichen Bestand als Platzhalter für die künftige Arbeit. Diese Platzhalter sind technisch möglicherweise noch nicht präzise, können aber als Grundlage für die Koordination mit dem Unternehmen dienen.

![Beziehungen zwischen Migrations-, Release- und Iterationsbacklogs während der Migration](../../../_images/migrate/backlog-relationships.png)

*Migration-, Release- und Iterationsbacklogs verfolgen verschiedene Ebenen von Aktivitäten während der Migrationsprozesse.*

Das Change Management-Team sollte mit jedem Migrationsbacklog die folgenden Informationen für alle Workloads im Plan erhalten. Diese Daten sollten mindestens für alle Workloads, die für die Migration in den nächsten zwei oder drei Releases priorisiert wurden, verfügbar sein.

### <a name="migration-backlog-data-points"></a>Datenpunkte in Migrationsbacklogs

- **Geschäftliche Auswirkungen:** Verständnis der Auswirkungen auf das Geschäft, wenn der Zeitrahmen nicht eingehalten oder die Funktionalität während Unterbrechungen eingeschränkt wird.
- **Relative geschäftliche Priorität:** Eine sortierte Liste von Workloads basierend auf geschäftlichen Prioritäten.
- **Besitzer dieses Geschäfts:** Die Person, die für Geschäftsentscheidungen in Zusammenhang mit dieser Workload verantwortlich ist.
- **Technischer Besitzer:** Die Person, die für technische Entscheidungen in Zusammenhang mit dieser Workload verantwortlich ist.
- **Erwartete Zeitrahmen:** Geplanter Termin für den Abschluss der Migration.
- **Workloadsperrungen:** Zeiträume, in denen die Workload nicht geändert werden darf.
- **Workloadname**
- **Anfangsbestand:** Alle Ressourcen, die zum Bereitstellen der Funktionen dieser Workload erforderlich sind, einschließlich VMs, IT-Geräten, Daten, Anwendungen, Bereitstellungspipelines usw. Diese Informationen sind wahrscheinlich ungenau.

## <a name="release-backlog-aligning-business-change-and-technical-coordination"></a>Releasebacklog: Abgleichen von geschäftlichen Änderungen mit der technischen Koordinierung

Im Kontext einer Migration ist ein _Release_ eine Aktivität, mit der Workloads in der Produktion bereitgestellt werden. Ein Release umfasst im Allgemeinen mehrere Iterationen oder technische Arbeiten. Es stellt jedoch eine einzelne Iteration einer geschäftlichen Änderung dar. Nachdem Workloads für die Höherstufung in die Produktion vorbereitet wurden, erfolgt ein Release. Die Entscheidung für den Inhalt eines Releasepakets erfolgt, wenn die migrierten Workloads einen ausreichenden Geschäftswert darstellen, um eine Änderung an einer Geschäftsumgebung zu rechtfertigen. Releases werden in Verbindung mit einem [geschäftsbezogenen Änderungsplan](../optimize/business-change-plan.md) ausgeführt, nachdem die [geschäftsbezogenen Tests](../optimize/business-test.md) abgeschlossen wurden. Das Team für die Cloudstrategie ist für das Planen und Überwachen der Ausführung eines Releases verantwortlich. Es muss sicherstellen, dass die gewünschten geschäftsbezogenen Änderungen umgesetzt werden.

Ein *Releasebacklog* ist der Plan für den zukünftigen Status für ein anstehendes Release. Das Releasebacklog ist der Schnittpunkt zwischen dem geschäftsbezogenen Change Management (*Migrationsbacklog*) und dem technische Change Management (*Sprintbacklog*). Ein Releasebacklog umfasst eine Liste von Workloads aus dem Migrationsbacklog, die bestimmten Aspekten der zu erzielenden Geschäftsergebnisse entsprechen. Die Festlegung und Übermittlung eines Releasebacklogs an das Cloudeinführungsteam stellt gleichzeitig den Auslöser für eine tiefer gehende Analyse und Planung der Migration dar. Nachdem das Cloudeinführungsteam die technischen Details zum Release überprüft hat, kann es ein Commit für das Release beschließen und basierend auf den derzeitigen Kenntnissen einen Zeitplan für das Release festlegen.

Aufgrund des Umfangs der erforderlichen Analyse für die Validierung eines Releases sollte das Cloudstrategieteam eine fortlaufend aktualisierte Liste der nächsten zwei bis vier Releases verwalten. Das Team sollte außerdem versuchen, möglichst viele der folgenden Informationen zu überprüfen, bevor es ein Release definiert und übermittelt. Ein sorgfältiges Cloudstrategieteam, das in der Lage ist, die nächsten vier Releases zu verwalten, kann zu einer erheblich gesteigerten Konsistenz und Genauigkeit bei Schätzungen des Releasezeitrahmens beitragen.

### <a name="release-backlog-data-points"></a>Datenpunkte in Releasebacklogs

In enger Zusammenarbeit zwischen dem Cloudstrategieteam und dem Cloudeinführungsteam können dem Releasebacklog die folgenden Datenpunkte für alle Workloads hinzugefügt werden:

- **Präzisierter Bestand:** Überprüfung der erforderlichen Ressourcen für die Migration. Die Validierung erfolgt oftmals über Protokoll- oder Überwachungsdaten auf Host-, Netzwerk- oder Betriebssystemebene, um eine genaue Kenntnis von Netzwerk- und Hardwareabhängigkeiten für jede Ressource einer Standardlast sicherzustellen.
- **Verwendungsmuster:** Verständnis von Mustern der Nutzung durch Endbenutzer. Zu diesen Mustern gehört häufig eine Analyse von der geografischen Verteilung der Endbenutzer, Netzwerkrouten, saisonalen Nutzungsspitzen, täglichen/stündlichen Nutzungsspitzen und der Zusammensetzung der Endbenutzer (intern/extern).
- **Erwartung an die Leistung:** Analyse der verfügbaren Protokolldaten für Durchsatz, Seitenaufrufe, Netzwerkrouten und andere Leistungsdaten, die für die Replikation der Benutzererfahrung erforderlich sind.
- **Abhängigkeiten:** Analyse von Mustern bei Netzwerkdatenverkehr und Anwendungsnutzung zur Ermittlung möglicher zusätzlicher Abhängigkeiten, die bei der Planung der Reihenfolge und der Vorbereitung der Umgebung berücksichtigt werden sollten. Fügen Sie eine Workload erst dann einem Release hinzu, wenn eines der folgenden Kriterien erfüllt wird:
  - Alle abhängigen Workloads wurden migriert.
  - Netzwerk- und Sicherheitskonfigurationen wurden implementiert, sodass die Workload unter Einhaltung der erwarteten Leistung Zugriff auf alle Abhängigkeiten hat.
- **Gewünschter Migrationsansatz:** Für das Migrationsbacklog stellt der angenommene Migrationsaufwand den einzigen Aspekt für die Analyse dar. Wenn beispielsweise das Geschäftsergebnis ein Auszug aus einem vorhandenen Rechenzentrum ist, gelten im Migrationsbacklog alle Migrationsvorgänge als Rehostingszenarien. Im Releasebacklog sollten das Cloudstrategieteam und das Cloudeinführungsteam den Langzeitwert durch zusätzliche Funktionen, Modernisierungen und kontinuierliche Investitionen in die Entwicklung bewerten, um zu ermitteln, ob ein moderner Ansatz in Betracht gezogen werden sollte.
- **Kriterien für geschäftsbezogene Tests:** Nach dem Hinzufügen einer Workload zum Migrationsbacklog sollten gemeinsam Testkriterien vereinbart werden. In einigen Fällen können die Testkriterien auf einen Leistungstest mit einer feststehenden Gruppe von Powerusern beschränkt werden. Allerdings ist für die statistische Überprüfung ein automatisierter Leistungstest wünschenswert und sollte deshalb einbezogen werden. Die vorhandene Anwendungsinstanz verfügt häufig nicht über Funktionen für automatisierte Tests. In diesem Fall ist es nicht ungewöhnlich, wenn die Cloudarchitekten mit den Powerusern zusammenarbeiten, um einen Basisauslastungstest für die vorhandene Lösung zu entwickeln, der dann während der Migration als Richtwert verwendet werden kann.

### <a name="release-backlog-cadence"></a>Intervalle im Releasebacklog

Bei umfassend geplanten Migrationsvorgängen erfolgen Releases in regelmäßigen Abständen. Die Geschwindigkeit wird vom Cloudeinführungsteam häufig angepasst, um alle zwei bis vier Iterationen ein Release zu erstellen (etwa alle ein bis zwei Monate). Dies sollte jedoch ohne Zwang erfolgen. Das künstliche Erzwingen von Releaserhythmen kann verhindern, dass das Cloudeinführungsteam einen konsistenten Durchsatz erzielt.

Um die Auswirkungen auf den Geschäftsbetrieb zu minimieren, sollte das Cloudstrategieteam einen monatlichen Releaseprozess für das Unternehmen einrichten und so einen regelmäßigen Austausch aufrechterhalten. Gleichzeitig sollte es aber auch die Erwartung fördern, dass es mehrere Monate dauern kann, bis ein regelmäßiges Releaseintervall vorhergesagt werden kann.

## <a name="sprint-or-iteration-backlog-aligning-technical-change-and-effort"></a>Sprint- oder Iterationsbacklog: Abgleichen von technischen Änderungen und Aufwand

Ein *Sprint* oder eine *Iteration* ist eine konsistente, zeitgebundene Arbeitseinheit. Bei der Migration wird diese oft in Intervallen von zwei Wochen gemessen. Jedoch sind auch Iterationen von einer oder vier Wochen nicht unüblich. Das Erstellen von zeitgebundenen Iterationen erzwingt konsistente Intervalle für Arbeitsabschlüsse und erlaubt häufigere Anpassungen der Pläne basierend auf neuen Erkenntnissen. Während eines Sprints gibt es in der Regel Aufgaben für die Bewertung, Migration und Optimierung der Workloads, die im Migrationsbacklog definiert wurden. Diese Arbeitseinheiten sollten mit demselben Projektverwaltungstool nachverfolgt und verwaltet werden, das auch für das Migrations- und Releasebacklog verwendet wird, damit alle Ebenen des Change Managements konsistent bleiben.

Ein *Sprint-* oder *Iterationsbacklog* enthält die technischen Aufgaben für einen einzelnen Sprint oder eine Iteration im Zusammenhang mit der Migration einzelner Ressourcen. Diese Aufgabe sollte aus der Liste der zu migrierenden Workloads abgeleitet werden. Bei der Verwendung von Tools wie Azure DevOps (zuvor Visual Studio Online) für die Projektverwaltung sind die Arbeitselemente in einem Sprint untergeordnete Elemente der Elemente des Produktbacklogs in einem Releasebacklog und damit die Kernelemente in einem Migrationsbacklog. Eine solche Anordnung in über- und untergeordnete Elemente bietet mehr Übersichtlichkeit auf allen Ebenen des Change Managements.

Das Cloudeinführungsteam stellt in einem einzelnen Sprint oder einer Iteration die zugesicherten technischen Arbeiten sicher, um die Migration einer definierten Workload zu gewährleisten. Dies ist das Endergebnis der Change Management-Strategie. Wenn diese Aufgaben abgeschlossen wurden, können sie getestet werden, indem die Produktionsbereitschaft einer in der Cloud bereitgestellten Workload getestet wird.

### <a name="large-or-complex-sprint-structures"></a>Strukturen für große oder komplexe Sprints

Bei einer kleinen Migration mit einem eigenständigen Migrationsteam kann ein einzelner Sprint alle vier Phasen der Migration für eine einzelne Workload umfassen (*Bewerten*, *Migrieren*, *Optimieren* sowie *Schützen und Verwalten*). Häufiger wird jedoch jeder dieser Prozesse von mehreren Teams mit unterschiedlichen Arbeitselementen für zahlreiche Sprints ausgeführt. Je nach Art der Aufgabe, Aufwand und Rollen können diese Sprints unterschiedliche Formen annehmen.

- **Migrationsfactory:** Umfangreiche Migrationsvorgänge erfordern in einigen Fällen einen Ansatz, der einer Factory im Ausführungsmodell ähnelt. Bei diesem Modell wird den verschiedenen Teams die Ausführung eines spezifischen Migrationsprozesses (oder einer Teilmenge des Prozesses) zugeordnet. Nach Abschluss des Vorgangs wird das Ergebnis des Sprints eines Teams in das Backlog des nächsten Teams übernommen. Dies ist ein effizienter Ansatz für umfangreiche Migrationsvorgänge für das Rehosting vieler großer Workloads mit Tausenden virtuellen Computern, die die Phasen Bewertung, Architektur, Korrektur und Migration durchlaufen. Damit dieser Ansatz funktioniert, ist jedoch unbedingt eine neue homogene Umgebung mit optimierten Change Management- und Genehmigungsprozessen erforderlich.
- **Migrationswellen:** Eine weitere Möglichkeit, die auch bei großen Migrationsvorgängen funktioniert, ist ein Wellenmodell. Bei diesem Modell ist die Arbeitsaufteilung nicht annähernd so klar. Die Teams übernehmen selbst die Ausführung von Migrationsprozessen für einzelne Workloads. Damit ändert sich jedoch die Art jedes Sprints. In einem Sprint kann das Team die Aufgaben für die Bewertung und Architektur abschließen. In einem weiteren Sprint könnte es den Migrationsvorgang beenden. Der Schwerpunkt eines weiteren Sprints könnte auf der Optimierung und dem Produktionsrelease liegen. Bei diesem Ansatz kann ein Kernteam die Übersicht über alle Workloads und die erforderlichen Prozesse behalten. Wenn Sie diesen Ansatz verfolgen, könnten die Vielfalt der Fähigkeiten und die unterschiedlichen Kontexte möglicherweise die Geschwindigkeit des Teams und damit den gesamten Migrationsprozess verlangsamen. Darüber hinaus können Hürden bei Genehmigungszyklen zu beträchtlichen Verzögerungen führen. Es ist bei diesem Modell wichtig, die Optionen im Releasebacklog im Blick zu behalten, damit das Team auch in Sperrzeiten weiterarbeitet. Außerdem ist es wichtig, die Teammitglieder untereinander zu schulen und sicherzustellen, dass die Fähigkeiten auch für den jeweiligen Sprint angemessen sind.

### <a name="sprint-backlog-data-points"></a>Datenpunkte in Sprintbacklogs

Das Ergebnis eines Sprints erfasst und dokumentiert die Änderungen an einer Workload und beendet daher den Change Management-Zyklus. Nach Abschluss sollte zumindest Folgendes dokumentiert werden. Während der Ausführung eines Sprints sollte diese Dokumentation zeitgleich zu den technischen Arbeitselementen abgeschlossen werden.

- **Bereitgestellte Ressourcen:** Alle Ressourcen, die in der Cloud zum Hosten der Workload bereitgestellt wurden.
- **Korrektur:** Alle Änderungen an Ressourcen zur Vorbereitung der Cloudmigration.
- **Konfiguration:** Ausgewählte Konfiguration für alle bereitgestellten Ressourcen, einschließlich Verweisen auf Konfigurationsskripts.
- **Bereitstellungsmodell:** Verwendeter Ansatz für die Bereitstellung der Ressource in der Cloud, einschließlich Verweisen auf mögliche Bereitstellungsskripts oder -tools.
- **Architektur:** Dokumentation der Architektur, die in der Cloud bereitgestellt wurde.
- **Leistungsmetriken:** Ausgabe automatisierter Tests oder geschäftsbezogener Tests, die durchgeführt wurden, um die Leistung zum Zeitpunkt der Bereitstellung zu überprüfen.
- **Besondere Anforderungen oder Konfigurationen:** Besondere Aspekte von Bereitstellung, Konfiguration oder technischen Anforderungen, die für die Ausführung der Workload erforderlich sind.
- **Betriebliche Genehmigung:** Bestätigung der Betriebsbereitschaft vom Anwendungsbesitzer und den IT-Mitarbeitern, die für die Verwaltung der Workload nach der Bereitstellung verantwortlich sind.
- **Genehmigung der Architektur:** Bestätigung vom Workloadbesitzer und dem Cloudeinführungsteam für sämtliche Architekturänderungen, die zum Hosten der einzelnen Ressourcen erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die Phasen beim Change Management festgelegt wurden, sollte die letzte Voraussetzung erfüllt werden: die [Überprüfung des Migrationsbacklogs](./migration-backlog-review.md).

> [!div class="nextstepaction"]
> [Überprüfen des Migrationsbacklogs](./migration-backlog-review.md)
