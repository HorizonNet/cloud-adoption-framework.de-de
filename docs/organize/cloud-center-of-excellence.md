---
title: Cloudkompetenzzentrum
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beschreibt die Schaffung eines Cloudkompetenzzentrums (Cloud Center of Excellence, CCoE).
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 1f25b3debed6110f7a45933fa3d4f724ff8390a5
ms.sourcegitcommit: 7df593a67a2e77b5f61c815814af9f0c36ea5ebd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2020
ms.locfileid: "75781826"
---
# <a name="cloud-center-of-excellence"></a>Cloudkompetenzzentrum

Die Erzielung von geschäftlicher und technischer Flexibilität ist ein wichtiges Ziel der meisten IT-Organisationen. Ein Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) ist eine Funktion, mit der eine möglichst gute Balance zwischen Geschwindigkeit und Stabilität erreicht werden soll.

## <a name="function-structure"></a>Funktionsstruktur

Bei einem CCoE-Modell müssen die folgenden Funktionsbereiche zusammenarbeiten:

- Cloudeinführung (insbesondere Lösungsarchitekten)
- Cloudstrategie (insbesondere Programm- und Projektmanager)
- Cloudgovernance
- Cloudplattform
- Cloudautomatisierung

## <a name="impact-and-cultural-change"></a>Auswirkungen und kulturelle Veränderungen

Wenn diese Funktion richtig strukturiert ist und unterstützt wird, können die Teilnehmer ihre Innovations- und Migrationsaufgaben schneller erledigen, während gleichzeitig die Gesamtkosten für Veränderungen reduziert werden und die geschäftliche Flexibilität gesteigert wird. Bei einer erfolgreichen Implementierung kann die Zeit bis zur Markteinführung mit dieser Funktion merklich verkürzt werden. Wenn Teams besser mit den Abläufen vertraut sind, verbessern sich auch die Qualitätsindikatoren. Hierzu zählen beispielsweise Zuverlässigkeit, Leistungseffizienz, Sicherheit, Verwaltbarkeit und Kundenzufriedenheit. Dieser Zugewinn an Effizienz, Flexibilität und Qualität ist besonders wichtig, wenn das Unternehmen die Implementierung einer Cloudmigration in größerem Umfang plant oder Innovationen in Bezug auf die Marktspezialisierung vorantreiben möchte.

Bei erfolgreicher Umsetzung kommt es mit einem CCoE-Modell zu einer signifikanten kulturellen Veränderung im IT-Bereich. Grundvoraussetzung eines CCoE-Ansatzes ist, dass der IT-Bereich für das Unternehmen als Broker, Partner oder Repräsentant fungiert. Dieses Modell stellt einen Paradigmenwechsel gegenüber der herkömmlichen Funktion des IT-Bereichs als Betriebseinheit oder Abstraktionsschicht zwischen dem Unternehmen und den IT-Ressourcen dar.

Die folgende Abbildung enthält einen Vergleich zu dieser kulturellen Veränderung. Ohne CCoE-Ansatz liegt das Hauptaugenmerk des IT-Bereichs meist auf der Steuerung und zentralen Zuständigkeit. Dies ist mit einer Ampel an einer Kreuzung vergleichbar. Wenn die Arbeit des Cloudkompetenzzentrums erfolgreich ist, liegt der Schwerpunkt auf Freiheit und delegierten Zuständigkeiten, und dies entspricht dann eher einem Kreisverkehr als einer Kreuzung.

![Vergleich zum Paradigmenwechsel bei Verwendung eines Cloudkompetenzzentrums](../_images/ready/ccoe-paradigm-shift.png)

Keiner der Ansätze in der obigen Abbildung mit dem Vergleich kann als richtig oder falsch bezeichnet werden, sondern es handelt sich lediglich um Alternativen in Bezug auf die Zuständigkeit und Verwaltung. Falls ein Self-Service-Modell eingerichtet werden soll, mit dem Geschäftseinheiten unter Einhaltung bestimmter Richtlinien und anerkannter wiederholbarer Kontrollmaßnahmen eigene Entscheidungen treffen können, ist für die Technologiestrategie ggf. ein CCoE-Modell geeignet.

## <a name="key-responsibilities"></a>Wichtige Zuständigkeiten

Hauptaufgabe des CCoE-Teams ist die Beschleunigung der Cloudeinführung mit cloudnativen oder hybriden Lösungen.

Mit dem Cloudkompetenzzentrum werden folgende Ziele verfolgt:

- Unterstützen der Schaffung einer modernen IT-Organisation mit flexiblen Ansätzen zur Erfassung und Implementierung von Geschäftsanforderungen
- Verwenden von wiederverwendbaren Bereitstellungspaketen gemäß den Richtlinien für Sicherheit, Konformität und Dienstverwaltung
- Bereitstellen einer funktionsfähigen Azure-Plattform gemäß den geltenden Betriebsverfahren
- Überprüfen und Genehmigen der Nutzung von cloudnativen Tools
- Standardisieren und Automatisieren von häufig benötigten Plattformkomponenten und -lösungen im Lauf der Zeit.

## <a name="meeting-cadence"></a>Rhythmus von Besprechungen

An der Arbeit des Cloudkompetenzzentrums sind vier stark ausgelastete Teams beteiligt. Es ist wichtig, die natürliche Zusammenarbeit zu fördern und den Fortschritt anhand eines gemeinsamen Repositorys bzw. Lösungskatalogs nachzuverfolgen. Erhöhen Sie die Anzahl natürlicher Interaktionen, aber halten Sie die Zahl der Besprechungen möglichst gering. Nachdem mehr Erfahrung mit dem CCoE-Ansatz gesammelt wurde, sollten die Teams versuchen, dedizierte Besprechungen nach Möglichkeit zu reduzieren. Die Teilnahme an wiederkehrenden Besprechungen, z. B. Releasebesprechungen unter Vorsitz des Teams für die Cloudeinführung, ermöglicht die Beisteuerung von Daten. Eine Besprechung nach jeder erneuten Bereitstellung des Releaseplans ist für dieses Team dagegen nur von geringer Bedeutung.

## <a name="solutions-and-controls"></a>Lösungen und Kontrollen

Jedes Mitglied des Cloudkompetenzzentrums hat die Aufgabe, sich mit den erforderlichen Einschränkungen, Risiken und Schutzmaßnahmen vertraut zu machen, die zu den derzeitigen IT-Kontrollelementen geführt haben. Durch die gemeinsame Arbeit der Teilnehmer des Cloudkompetenzzentrums sollte dieses Wissen zur Implementierung von cloudnativen (oder hybriden) Lösungen oder Kontrollelementen führen, um die gewünschten Self-Service-Ergebnisse für das Unternehmen zu erzielen. Wenn Lösungen erstellt werden, werden sie für verschiedene Teams in Form von Kontrollelementen oder Automatisierungen bereitgestellt, die als Richtlinien für unterschiedliche Maßnahmen dienen. Diese Richtlinien ermöglichen die Steuerung der freien Aktivitäten der einzelnen Teams, während die Zuständigkeiten für unterschiedliche Migrations- und Innovationsmaßnahmen an die Teilnehmer delegiert werden.

Beispiele für diese Umstellung:

| Szenario | Lösung vor CCoE | Lösung nach CCoE |
|---------|---------|---------|
| Bereitstellen einer SQL Server-Instanz für die Produktion | Teams für die Bereiche Netzwerk, IT und Datenplattform stellen im Laufe von Tagen oder auch Wochen verschiedene Komponenten bereit. | Das Team, das den Server benötigt, stellt eine PaaS-Instanz von Azure SQL-Datenbank bereit. Alternativ kann auch eine vorab genehmigte Vorlage verwendet werden, um alle IaaS-Ressourcen binnen weniger Stunden in der Cloud bereitzustellen. |
| Bereitstellen einer Entwicklungsumgebung | Die Teams für die Bereiche Netzwerk, IT, Entwicklung und DevOps einigen sich auf Spezifikationen und stellen eine Umgebung bereit. | Das Entwicklungsteam definiert eigene Spezifikationen und stellt basierend auf dem zugeteilten Budget eine Umgebung bereit. |
| Aktualisieren von Sicherheitsanforderungen zur Verbesserung des Schutzes von Daten | Die Teams für die Bereiche Netzwerk, IT und Sicherheit aktualisieren verschiedene Netzwerkgeräte und VMs für mehrere Umgebungen, um Schutzmaßnahmen zu treffen. | Tools für Cloudgovernance werden zum Aktualisieren von Richtlinien verwendet, die sofort auf alle Ressourcen in allen Cloudumgebungen angewendet werden können. |

## <a name="negotiations"></a>Verhandlungen

Kern aller CCoE-Maßnahmen ist ein fortlaufender Verhandlungsprozess. Das CCoE-Team führt Verhandlungen mit vorhandenen IT-Funktionsbereichen durch, um die zentrale Steuerung zu reduzieren. Die Nachteile für das Unternehmen liegen bei diesen Verhandlungen in den Bereichen Freiheit, Flexibilität und Geschwindigkeit. Die Vorteile ergeben sich für vorhandene IT-Teams in Form von neuen Lösungen. Diese neuen Lösungen können für vorhandene IT-Teams beispielsweise die folgenden positiven Auswirkungen haben:

- Möglichkeit zur Automatisierung häufig auftretender Probleme
- Verbesserungen bei der Einheitlichkeit (weniger frustrierende Situationen im Tagesgeschäft)
- Möglichkeit zum Erlernen und Bereitstellen neuer technischer Lösungen
- Verringerung von Incidents mit hohem Schweregrad (weniger Kurz- oder Bereitschaftseinsätze, z. B. nachts per Pager)
- Möglichkeit zur Erweiterung des technischen Umfangs und Abdeckung eines breiteren Themenbereichs
- Beteiligung an höher angesiedelten Geschäftslösungen zur Behandlung der Auswirkungen von Technologiekomponenten
- Verringerung von niederen Wartungsaufgaben
- Steigerung in Bezug auf Technologiestrategie und Automatisierung

Diesen Vorteilen stehen für vorhandene IT-Funktionsbereiche Einbußen in den folgenden Bereichen gegenüber (tatsächlich oder nur empfunden):

- Gefühlte Kontrolle über manuelle Genehmigungsprozesse
- Gefühlte Stabilität aufgrund der Änderungssteuerung
- Gefühlte Arbeitsplatzsicherheit aufgrund der Durchführung von erforderlichen wiederkehrenden Aufgaben
- Gefühlte Beständigkeit aufgrund der Nutzung vorhandener IT-Lösungsanbieter

In intakten cloudaffinen Unternehmen erfolgt dieser Verhandlungsprozess als dynamischer Austausch zwischen Mitarbeitern und IT-Teams als Partnern. Die technischen Details sind ggf. komplex, aber sie können bewältigt werden, wenn der IT-Abteilung die Zielsetzung klar ist und die CCoE-Maßnahmen von ihr unterstützt werden. Falls die IT-Abteilung weniger Unterstützung leistet, können Sie die Informationen im folgenden Abschnitt zur erfolgreichen Einführung eines Cloudkompetenzzentrums nutzen, um kulturelle Blockadehaltungen zu überwinden.

## <a name="enable-ccoe-success"></a>Ermöglichen einer erfolgreichen Arbeit des Cloudkompetenzzentrums

Bevor Sie mit diesem Modell starten, sollten Sie unbedingt prüfen, ob im Unternehmen Toleranz für das „dynamische Selbstbild“ (Growth Mindset) besteht und ob die IT-Abteilung bereit ist, zentrale Zuständigkeiten abzugeben. Wie oben bereits erwähnt, besteht der Zweck eines Cloudkompetenzzentrums darin, Kontrolle durch Flexibilität und Geschwindigkeit zu ersetzen.

Diese Art von Veränderung erfordert Zeit, Experimentieraufwand und Verhandlungen. Während dieses Entwicklungsprozesses kommt es unweigerlich auch zu Schwierigkeiten und Rückschlägen. Wenn das Team aber fokussiert bleibt und sich vom erforderlichen Experimentieraufwand nicht entmutigen lässt, ist die Wahrscheinlichkeit hoch, dass in den Bereichen Flexibilität, Geschwindigkeit und Zuverlässigkeit Verbesserungen erzielt werden können. Einer der wichtigsten Faktoren für den Erfolg oder Misserfolg eines Cloudkompetenzzentrums ist die Unterstützung durch die Führungsebene und durch die wichtigsten Projektbeteiligten.

### <a name="key-stakeholders"></a>Wichtige Projektbeteiligte

Die Führungsebene der IT-Abteilung ist der erste und offensichtlichste Projektbeteiligte. IT-Manager spielen eine wichtige Rolle. Während dieses Prozesses wird aber auch die Unterstützung des CIO und anderer leitender IT-Mitarbeiter benötigt.

Weniger offensichtlich ist die Beteiligung der zuständigen Personen aus dem betriebswirtschaftlichen Bereich. Geschäftliche Flexibilität und eine Verkürzung der Zeit bis zur Markteinführung sind wichtige Motivationsfaktoren bei der Schaffung eines Cloudkompetenzzentrums. Aus diesem Grund sollten die entsprechenden Projektbeteiligten ein besonderes Interesse an diesen Bereichen haben. Beispiele für Projektbeteiligte aus der Betriebswirtschaft sind Branchenleiter, Finanzführungskräfte, Führungskräfte aus dem operativen Bereich und Verantwortliche für Geschäftsprodukte.

### <a name="business-stakeholder-support"></a>Unterstützung durch Projektbeteiligte aus dem betriebswirtschaftlichen Bereich

Der Fortschritt bei der Schaffung des Cloudkompetenzzentrums kann durch die Unterstützung der Projektbeteiligten aus dem betriebswirtschaftlichen Bereich beschleunigt werden. Der Schwerpunkt liegt bei den CCoE-Vorgängen größtenteils darauf, langfristige Verbesserungen in Bezug auf die geschäftliche Flexibilität und die Geschwindigkeit zu erzielen. Die Definition der Auswirkungen von aktuellen Betriebsmodellen und des Nutzens von Verbesserungen ist als Anhaltspunkt und Verhandlungswerkzeug für das Cloudkompetenzzentrum sehr hilfreich. Für die CCoE-Unterstützung wird empfohlen, die folgenden Punkte zu dokumentieren:

- Festlegung von geschäftlichen Zielen und Ergebnissen, die aufgrund der geschäftlichen Flexibilität und Geschwindigkeit zu erwarten sind
- Klar definierte Problempunkte, die durch die aktuellen IT-Prozesse entstehen (z.B. Schwierigkeiten bei Geschwindigkeit, Flexibilität, Stabilität und Kosten).
- Klar definierte in der Vergangenheit entstandene Auswirkungen dieser Problempunkte (z.B. verlorene Marktanteile, Feature- und Funktionsvorteile bei Wettbewerbern, unzureichende Benutzerfreundlichkeit und Budgeterhöhungen).
- Definition von Möglichkeiten für geschäftliche Verbesserungen, die durch die derzeitigen Problempunkte und Betriebsmodelle blockiert werden
- Festlegung von Zeitachsen und Metriken für diese Verbesserungsmöglichkeiten

Diese Datenpunkte stellen keinen Angriff auf die IT-Abteilung dar. Stattdessen ermöglichen sie es, dass für das Cloudkompetenzzentrum aus der Vergangenheit gelernt wird, indem auf realistische Weise der Rückstand dokumentiert und ein Plan für Verbesserungen aufgestellt wird.

**Fortlaufende Unterstützung und Einbindung:** CCoE-Teams können in einigen Bereichen schnelle Erfolge erzielen. Die übergeordneten Ziele, z.B. geschäftliche Flexibilität und eine Verkürzung der Zeit bis zur Markteinführung, können aber deutlich mehr Zeit benötigen. Während des Entwicklungsprozesses besteht ein hohes Risiko, dass es im Cloudkompetenzzentrum zu einer Entmutigung kommt oder dass das Personal für die Arbeit an anderen IT-Projekten herangezogen wird.

Für die ersten sechs bis neun Monate der Arbeit des Cloudkompetenzzentrums empfehlen wir Ihnen, dass sich Projektbeteiligte aus dem betriebswirtschaftlichen Bereich Zeit für monatliche Besprechungen mit der IT-Führungsebene und den Verantwortlichen des Cloudkompetenzzentrums freihalten. Für diese Besprechungen müssen keine besonderen Formalitäten eingehalten werden. Es ist in Bezug auf den Erfolg des Cloudkompetenzzentrums schon viel wert, wenn die Mitglieder des Cloudkompetenzzentrums und deren Führungskräfte an die Bedeutung dieses Programms erinnert werden.

Außerdem wird empfohlen, dass die Projektbeteiligten aus dem betriebswirtschaftlichen Bereich über den Fortschritt und die Schwierigkeiten des CCoE-Teams auf dem Laufenden gehalten werden. Bei einem Großteil der Arbeit scheint es sich nur um technische Einzelheiten zu handeln. Es ist aber wichtig, dass die Projektbeteiligten aus dem betriebswirtschaftlichen Bereich über den Fortschritt des Plans informiert sind, damit sie eingreifen können, wenn das Team schwächelt oder durch andere Prioritäten abgelenkt wird.

### <a name="it-stakeholder-support"></a>Unterstützung von Projektbeteiligten aus dem IT-Bereich

**Vision unterstützen:** Für ein erfolgreiches CCoE-Projekt sind viele Verhandlungen mit Mitgliedern des bestehenden IT-Teams erforderlich. Wenn diese sorgfältig und gut durchgeführt werden, besteht das Ergebnis darin, dass die gesamte IT-Abteilung zur Lösung beiträgt und kein Problem mit der Veränderung hat. Wenn dies nicht der Fall ist, möchten einige Mitglieder des bestehenden IT-Teams bestimmte Kontrollmechanismen aus unterschiedlichen Gründen ggf. in der Hand behalten. Wenn dies der Fall ist, ist die Unterstützung von Projektbeteiligten aus dem IT-Bereich für den Erfolg des Cloudkompetenzzentrums von entscheidender Bedeutung. Eine allgemeine Ermutigung und die Stärkung der übergeordneten Ziele des Cloudkompetenzzentrums ist wichtig, um zu verhindern, dass die Verhandlungen durch Blockierer gestört werden. In seltenen Fällen müssen Projektbeteiligte aus dem IT-Bereich unter Umständen sogar eingreifen und einen Konflikt lösen oder eine Pattsituation beseitigen, damit die Arbeit des Cloudkompetenzzentrums fortgesetzt werden kann.

**Fokussiert bleiben:** Ein Cloudkompetenzzentrum kann für alle IT-Teams mit begrenzten Ressourcen eine erhebliche Verpflichtung darstellen. Wenn kompetente Architekten von kurzfristigen Projekten abgezogen werden, damit sie sich auf langfristige Ziele konzentrieren können, kann dies zu Schwierigkeiten für Teammitglieder führen, die nicht Teil des Cloudkompetenzzentrums sind. Es ist wichtig, dass die IT-Führungskräfte und die Projektbeteiligten aus dem IT-Bereich im Hinblick auf das Ziel des Cloudkompetenzzentrums fokussiert bleiben. Die Unterstützung der IT-Führungskräfte und Projektbeteiligten aus dem IT-Bereich wird benötigt, um zu verdeutlichen, dass die CCoE-Aufgaben Vorrang vor dem normalen Tagesgeschäft haben und dadurch nicht gestört werden sollten.

**Puffer einbauen:** Das CCoE-Team experimentiert mit neuen Ansätzen. Einige dieser Ansätze passen nicht gut zu vorhandenen Vorgängen oder technischen Einschränkungen. Es besteht ein reelles Risiko, dass das Cloudkompetenzzentrum durch andere Teams unter Druck gerät oder quasi in Regress genommen wird, wenn Experimente nicht erfolgreich sind. Es ist wichtig, das Team zu ermutigen und vor den Konsequenzen von Fail-Fast-Lerneffekten zu schützen. Es ist genauso wichtig, dem Team dessen Zuständigkeit für das Erzielen von Fortschritten zu verdeutlichen und sicherzustellen, dass aus diesen Experimenten gelernt wird und bessere Lösungen gefunden werden.

## <a name="next-steps"></a>Nächste Schritte

Für ein CCoE-Modell sind sowohl [Funktionen für die Cloudplattform](./cloud-platform.md) als auch [Funktionen für die Cloudautomatisierung](./cloud-automation.md) erforderlich. Der nächste Schritt ist die Ausrichtung der [Funktionen für die Cloudplattform](./cloud-platform.md).

> [!div class="nextstepaction"]
> [Funktionen der Cloudplattform](./cloud-platform.md)
