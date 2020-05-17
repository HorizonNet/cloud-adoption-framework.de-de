---
title: Umgestalten von Zielzonen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Prozess zum Refactoring von Zielzonen
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bc5263b1f9dfcbdb0d5c14e79e5de976fdd59818
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83221806"
---
# <a name="refactor-landing-zones"></a>Umgestalten von Zielzonen

Eine Zielzone ist eine **mittels Code vorab bereitgestellte** Umgebung zum Hosten Ihrer Workloads. Da die Infrastruktur der Zielzone im Code definiert ist, kann sie ähnlich wie jede andere Codebasis umgestaltet werden. Refactoring ist der Prozess der Änderung oder Umstrukturierung des Quellcodes, um die Ausgabe dieses Codes zu optimieren, ohne seinen Zweck oder seine zentrale Funktion zu ändern.

Die Ready-Methode verwendet das Konzept des Refactoring, um die Migration zu beschleunigen und häufige Hindernisse zu beseitigen. Die Schritte in der Ready-Übersicht beschreiben einen Prozess, der mit einer vordefinierten Zielzonenvorlage beginnt, die am besten auf Ihre Hostingfunktion abgestimmt ist. Dann wird der Quellcode umgestaltet oder ergänzt, um die Funktionen der Landezonen so zu erweitern, dass sie diese Funktion durch verbesserte Sicherheit, Abläufe oder Governance bereitstellen können. Die folgende Abbildung veranschaulicht das Konzept des Refactorings.

![Abbildung zum Refactoring der Zielzone – Beschrieben in einem späteren Abschnitt dieses Artikels](../../_images/ready/refactor.png)

## <a name="common-blockers"></a>Allgemeine Hindernisse

Wenn Kunden die Cloud einführen, sind Überlegungen zur Zielzone das häufigste Hindernis für die Einführung und die cloudbezogenen Geschäftsergebnisse. Kunden neigen dazu, sich einem der beiden folgenden Hindernisse zuzuwenden. Oftmals tendieren verschiedene Teams jeweils zu einem dieser beiden Hindernisse, was zu kulturellen Deadlocks führt, die eine Einführung erschweren.

Die beiden primären Hindernisse sind in einer Überzeugung verwurzelt: Die Cloudumgebung und die vorhandenen Rechenzentren sollten in Bezug auf Betrieb, Governance und Sicherheit (nahezu) eine Featureparität aufweisen. Dies ist ein vernünftiges langfristiges Ziel. Aber das Problem ist das schwierige Gleichgewicht zwischen dem Timing zur Erreichung dieses Ziels und der Geschwindigkeit, die zur Erzielung von Geschäftsergebnissen erforderlich ist.

### <a name="blocker-acting-too-soon"></a>Hindernis: Zu frühes Handeln

Es bedurfte Jahre und erheblicher Anstrengungen, um den aktuellen Stand hinsichtlich Sicherheit, Governance und Betrieb im derzeitigen Rechenzentrum zu erreichen. Außerdem waren Beobachtungen, Lernprozesse und Anpassungen erforderlich, um den eindeutigen Einschränkungen dieser Umgebung zu entsprechen. Das Replizieren derselben Verfahren und Konfigurationen wird einige Zeit in Anspruch nehmen. Das Erreichen einer 100%igen Featureparität kann auch zu einer Umgebung führen, die in der Cloud unterdurchschnittlich leistungsfähig ist. Dieser Paritätsansatz führt außerdem häufig zu erheblichen ungeplanten Ausgabenüberschreitungen in der Cloudumgebung. Versuchen Sie nicht, die aktuellen Zustandsanforderungen auf eine zukünftige Zustandsumgebung als eine Art „Tor zu einer frühen Phase“ anzuwenden. Ein solcher Ansatz erweist sich selten als profitabel.

![Allgemeines Hindernis: Zu frühes Handeln](../../_images/ready/blocker-act-too-soon.png)

In der obigen Abbildung hat der Kunde ein Ziel von 100 Workloads, die in der Cloud existieren. Um dies zu erreichen, wird der Kunde wahrscheinlich seine erste Workload bereitstellen. Dann ihre ersten 10 oder so Workloads, bevor sie bereit sind, eines dieser Workloads für die Produktion freizugeben. Schließlich werden sie das Ziel des Einführungsplans erreichen und über ein robustes Portfolio in der Cloud verfügen. Das rote X in der Abbildung zeigt jedoch, wo Kunden häufig hängen bleiben. Das Warten auf eine 100%ige Ausrichtung kann die erste Workload um Wochen, Monate oder sogar Jahre verzögern.

### <a name="blocker-acting-too-late"></a>Hindernis: Zu spätes Handeln

Andererseits kann ein zu spätes Handeln erhebliche langfristige Folgen für den Erfolg der Bemühungen um die Einführung der Cloud haben. Wenn das Team mit dem Erreichen der Featureparität wartet, bis der Einführungsaufwand abgeschlossen ist, wird es auf unnötige Hindernisse stoßen und mehrere Eskalationen benötigen, um den Aufwand auf Kurs zu halten.

![Allgemeines Hindernis: Zu spätes Handeln](../../_images/ready/blocker-act-too-late.png)

Ähnlich wie bei zu frühem Handeln wartet der Kunde in dieser Abbildung zu lange, um über Zielzonen hinweg die Unternehmensbereitschaft zu erreichen. Durch zu langes Warten wird der Kunde hinsichtlich des Umfangs beim Refactoring und der Erweiterung eingeschränkt, die er in der Umgebung durchführen kann. Diese Einschränkungen werden ihre Möglichkeiten für einen anhaltenden Erfolg begrenzen.

### <a name="finding-balance"></a>Finden des Gleichgewichts

Um diese allgemeinen Hindernisse zu vermeiden, schlagen wir einen iterativen Ansatz vor, der auf einem gut strukturierten Plan zur Einführung der Cloud basiert, der die Lernmöglichkeiten maximiert und die Zeit bis zum Geschäftserfolg minimiert. Refactoring und parallele Anstrengungen sind für diesen Ansatz von entscheidender Bedeutung.

> [!WARNING]
> Einführungsteams, die mittelfristig (innerhalb von 24 Monaten) das Ziel haben, **mehr als 1.000 Assets (Apps, Infrastruktur oder Datenassets) in der Cloud zu hosten**, werden mit einem Refactoringansatz höchstwahrscheinlich nicht erfolgreich sein. Die Lernkurve ist zu steil und der Zeitrahmen zu knapp bemessen, um einen organischen Ansatz für die Erlangung von Qualifikationen zu ermöglichen. Ein vollständigerer Ausgangspunkt, der weniger Anpassungen erfordert, ist ein besserer Weg, um Ihre Ziele zu erreichen. Ihre Implementierungspartner werden Sie wahrscheinlich durch einen besseren Ansatz führen können.

Der Rest dieses Artikels konzentriert sich auf einige wesentliche Einschränkungen, die einen Refactoringansatz bei gleichzeitiger Risikominimierung ermöglichen können.

## <a name="theory"></a>Theorie

Das Konzept des Refactoring einer Zielzone ist in der Theorie einfach, erfordert jedoch geeignete Schutzmaßnahmen. Das oben dargestellte Konzept skizziert den grundlegenden Flow wie folgt. Wenn Sie bereit sind, Ihre erste Zielzone zu erstellen, beginnen Sie mit einer anfänglichen Zielzone, die über eine Vorlage definiert wird. Nachdem diese Zielzone bereitgestellt ist, verwenden Sie die Entscheidungsstrukturen in den nachfolgenden Artikeln unter dem Abschnitt „Erweitern Ihrer Zielzone“ dieser Artikelserie (siehe Inhaltsverzeichnis), um Ihre ursprüngliche Zielzone umzugestalten und zu ergänzen. Wiederholen Sie Entscheidungsstrukturen und Refactoring, bis Sie über eine für den Unternehmenseinsatz bereite Umgebung verfügen, die den erhöhten Anforderungen Ihrer Sicherheits-, Betriebs- und Governanceteams entspricht.

## <a name="development-approach"></a>Entwicklungsansatz

Der Vorteil eines auf Refactoring basierenden Ansatzes ist die Möglichkeit, parallele Iterationspfade für die Entwicklung zu erzeugen. Die folgende Abbildung zeigt ein Beispiel für zwei parallele Iterationspfade: Cloudeinführung und Cloudplattform. Beide schreiten in ihrem eigenen Tempo voran, wobei ein minimales Risiko besteht, zum Hindernis für den täglichen Aufwand beider Teams zu werden. Die Anpassung an den Einführungsplan und die Schutzmaßnahmen für das Refactoring schaffen eine Reihe von Vereinbarungen hinsichtlich der Meilensteine, die klare zukünftige Zustandsabhängigkeiten bereitstellen.

![Parallele Iteration der Zielzone](../../_images/ready/iterations.png)

In den obigen Beispieliterationspfaden migriert das Cloudeinführungsteam sein Portfolio von 100 Workloads in die Cloud. Parallel dazu konzentriert sich das Cloudplattformteam darauf, dem Cloudeinführungsplan voraus zu sein, um sicherzustellen, dass die Umgebung auf diese Workloads vorbereitet ist.

In diesem Beispiel werden die geplanten Iterationen wie folgt ausgeführt:

- Das Cloudplattformteam beginnt die Entwicklungsmaßnahmen mit der Bereitstellung einer ersten Zielzone. Diese Zielzone ermöglicht es dem Cloudeinführungsteam, die erste Workload bereitzustellen und zu testen.
- Um die nächste Bereitstellung von 10 Workloads durch das Cloudeinführungsteam vorzubereiten, arbeitet das Cloudplattformteam im Voraus an der Umgestaltung und Ergänzung einer verbundenen Umgebung und behandelt die Cloud als ein Umkreisnetzwerk (DMZ).
- Bevor das Einführungsteam seine erste Produktionsworkload freigeben kann, verlangt das Sicherheitsteam eine Sicherheitsüberprüfung. Während das Einführungsteam seine ersten 10 Workloads bereitstellt, schreitet das Plattformteam bei der Definition und Implementierung der Sicherheitsanforderungen voran.
- Wenn die erste Workload für die Produktion freigegeben wird, sollten beide Teams über ausreichende Erfahrungen verfügen, um sich auf ein längerfristiges Modell mit freigegebenen Diensten vorzubereiten. Die Zentralisierung der zentralen Dienstarchitekturen wird dazu beitragen, Governance- und Betriebsteam aufeinander abzustimmen. Die Zentralisierung der zentralen Dienste wird dazu beitragen, das Einführungsteam auf die Skalierung und Freigabe der nächsten Wellen von Produktionsworkloads vorzubereiten.
- Wenn sich das Team seinem Ziel nähert, 100 Workloads zu migrieren, wird das Team natürlich beginnen, sich mehr in Richtung eines Kollaborationsmodells und einer Teamstruktur für ein Cloudkompetenzzentrum zu bewegen.

Die Konfiguration einer für Unternehmen geeigneten Umgebung wird einige Zeit in Anspruch nehmen. Dieser Ansatz wird diese Anforderung nicht aufheben. Stattdessen ist dieser Ansatz darauf ausgerichtet, frühe Hindernisse aus dem Weg zu räumen und Möglichkeiten für die Plattform- und Einführungsteams zu schaffen, gemeinsam zu lernen.

## <a name="landing-zone-refactoring-guardrails"></a>Schutzmaßnahmen für das Refactoring von Zielzonen

Alle anfänglichen Zielzonenvorlagen weisen Einschränkungen auf. Schutzmaßnahmen oder Richtlinien während des Refactorings sollten diese Einschränkungen widerspiegeln. Vor Beginn eines Refactoringprozesses für die Zielzone ist es wichtig, die langfristigen Anforderungen des Cloudeinführungsplans und die Klassifizierung der betroffenen Workloads im Vergleich zu den anfänglichen Einschränkungen der Vorlage zu verstehen.

Als Beispiel für die Einrichtung von Schutzmaßnahmen für das Refactoring lassen Sie uns den Entwicklungsansatz im vorherigen Beispiel und die Blaupause für die CAF-Migrationszielzone vergleichen.

- Gemäß den [Annahmedetails der Blaupause für die CAF-Migrationszielzone](./migrate-landing-zone.md#assumptions) ist diese anfängliche Zielzone nicht für vertrauliche Daten oder unternehmenskritische Workloads ausgelegt. Diese Features müssen durch Refactoring hinzugefügt werden.
- In diesem Beispiel nehmen wir an, dass das Portfolio von 100 Workloads Hostingfunktionen für sowohl unternehmenskritische als auch vertrauliche Daten erfordern wird.

Um diese beiden konkurrierenden Anforderungen ausgewogen zu gestalten, werden das Einführungsteam und das Plattformteam unter den folgenden vereinbarten Bedingungen arbeiten:

- Das Cloudeinführungsteam wird Produktionsworkloads, die keinen Zugriff auf vertrauliche Daten haben und nicht als unternehmenskritisch eingestuft werden, priorisieren.
- Vor der Produktionsfreigabe wird das Sicherheits- und Betriebsteam die Anpassung an die vorherige Richtlinie überprüfen.
- Das Cloudplattformteam wird mit den Sicherheits- und Governanceteams zusammenarbeiten, um eine Sicherheitsbaseline zu implementieren. Sobald die Sicherheit die Implementierung genehmigt hat, wird das Einführungsteam für die Migration von Workloads, die Zugriff auf einige vertrauliche Daten haben, zugelassen.
- Das Cloudplattformteam wird mit dem Betriebsteam zusammenarbeiten, um eine Verwaltungsbaseline zu implementieren. Sobald das Betriebsteam die Implementierung genehmigt hat, wird das Einführungsteam für die Migration von Workloads mit höherer Wichtigkeit zugelassen.

In diesem Beispiel ermöglichen die oben genannten vereinbarten Bedingungen dem Einführungsteam, mit dem Migrationsaufwand zu beginnen. Es hilft dem Plattformteam auch dabei, seine Interaktionen mit anderen Teams zu gestalten, während sie auf eine längerfristige, für den Unternehmenseinsatz bereite Umgebung hinarbeiten.

## <a name="meeting-long-term-requirements-while-refactoring"></a>Erfüllen langfristiger Anforderungen beim Refactoring

Der Abschnitt der Ready-Methode über die Erweiterung Ihrer Zielzone wird Ihnen helfen, sich auf die längerfristigen Anforderungen einzustellen. Während das Cloudeinführungsteam gemäß seinem Einführungsplan voranschreitet, bietet der Abschnitt über die Erweiterung Ihrer Zielzone eine Orientierungshilfe bei der Entscheidungsfindung und beim Refactoring in Übereinstimmung mit den sich entwickelnden Anforderungen der verschiedenen Teams.

![Parallele Iteration der Zielzone](../../_images/ready/refactor-methodologies.png)

Jeder Unterabschnitt von „Erweitern Ihrer Zielzone“ weist auf eine der in der obigen Abbildung dargestellten Ergänzungen hin. Über diese grundlegenden Ergänzungen hinaus werden die tiefer gehenden Methoden (z. B. „Govern“ oder „Manage“) dieses Frameworks dazu beitragen, über grundlegende Änderungen der Zielzone hinauszugehen und langfristige Regelungen umzusetzen.

## <a name="next-steps"></a>Nächste Schritte

[Wählen Sie Ihre erste Zielzone aus](./first-landing-zone.md), um mit den ersten Schritten des Refactoringprozesses zu beginnen.

> [!div class="nextstepaction"]
> [Wählen Ihrer ersten Zielzone](./first-landing-zone.md)
