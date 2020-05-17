---
title: Testgesteuerte Entwicklung für Zielzonen
description: Testgesteuerte Entwicklung für Zielzonen
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 055279bccb9c2897b3cc67adf549f5f57c5bf5fc
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222996"
---
# <a name="test-driven-development-tdd-for-landing-zones"></a>Testgesteuerte Entwicklung (TDD) für Zielzonen

Die testgesteuerte Entwicklung ist ein allgemeiner Softwareentwicklungs- und DevOps-Prozess, der die Qualität von neuen Features und Verbesserungen in jeder codebasierten Lösung optimiert. Die cloudbasierte Infrastruktur und der zugrunde liegende Quellcode mit diesem Prozess sicherstellen, dass Zielzonen die zentralen Anforderungen erfüllen und eine hohe Qualität aufweisen. Dieser Prozess ist besonders nützlich, wenn Zielzonen in einem parallelen Entwicklungsaufwand entwickelt und umgestaltet werden.

![Testgesteuerter Entwicklungsprozess für Cloudzielzonen](../../_images/ready/test-driven-development-process.png)

In der Cloud stellt die Infrastruktur die Ausgabe von Code dar. Ein gut strukturierter, getesteter und überprüfter Code erzeugt eine entwicklungsfähige Zielzone. Gemäß der [Definition von Zielzonen](../landing-zone/index.md): „Eine Zielzone eine durch Code vorbereitete Umgebung zum Hosten Ihrer Workloads. Sie umfasst grundlegende Funktionen unter Verwendung eines definierten Satzes von Clouddiensten und bewährten Methoden, sodass Sie **für die erfolgreiche Durchführung eingerichtet** sind.“ In diesem Artikel wird ein Ansatz vorgestellt, bei dem die testgesteuerte Entwicklung verwendet wird, um den letzten Teil dieser Definition zu erfüllen und gleichzeitig die Anforderungen an Qualität, Sicherheit, Betrieb und Governance zu erfüllen.

Dieser Ansatz kann verwendet werden, um einfache Featureanforderungen während der frühen Entwicklung zu erfüllen. Dieser Prozess kann zu einem späteren Zeitpunkt im Lebenszyklus der Cloudeinführung verwendet werden, um Anforderungen an Sicherheit, Betrieb, Governance oder Compliance zu erfüllen.

## <a name="definition-of-done"></a>Definition of Done

„Für die erfolgreiche Durchführung eingerichtet“ ist eine subjektive Aussage. Diese Aussage liefert dem Cloudplattformteam während der Entwicklung der Zielzone oder für den Refactoringaufwand wenig verwertbare Informationen. Diese fehlende Eindeutigkeit kann zu enttäuschten Erwartungen und Sicherheitsrisiken in einer Cloudumgebung führen. Bevor eine Zielzone umgestaltet oder erweitert wird, sollte sich das Cloudplattformteam Klarheit über die „Definition of Done“ für jede Zielzone verschaffen.

Die „Definition of Done“ ist eine einfache Vereinbarung zwischen dem Cloudplattformteam und anderen betroffenen Teams. Diese Vereinbarung skizziert die erwarteten Features mit Mehrwert, die in jeglichem Bereitstellungsaufwand für Zielzonen enthalten sein sollten. Oftmals ist die „Definition of Done“ eine Prüfliste, die mit dem kurzfristigen Cloudeinführungsplan übereinstimmt. In ausgereiften Prozessen werden die erwarteten Features in der Prüfliste jeweils eigene Akzeptanzkriterien aufweisen, um noch mehr Klarheit zu schaffen. Wenn die Features mit Mehrwert jeweils die Akzeptanzkriterien erfüllen, ist die Zielzone ausreichend konfiguriert, um den Erfolg der aktuellen Welle oder die Freisetzung des Einführungsaufwands zu ermöglichen.

Da die Teams zusätzliche Workloads und Cloudfeatures einführen, werden die „Definition of Done“ sowie die Akzeptanzkriterien zunehmend komplexer.

## <a name="test-driven-development-cycle"></a>Testgesteuerter Entwicklungszyklus

Der Zyklus, der für eine effektive testgesteuerte Entwicklung sorgt, wird oft als Rot/Grün-Test bezeichnet. Bei diesem Ansatz beginnt das Cloudplattformteam mit einem fehlgeschlagenen Test (Rot-Test), basierend auf der Definition von Done und der definierten Akzeptanzkriterien. Für jedes Feature oder Akzeptanzkriterium würde das Cloudplattformteam Entwicklungsaufgaben bis zum Bestehen des Tests (Grün-Test) durchführen. Ein testgesteuerter Entwicklungszyklus (oder Rot/Grün-Test) würde die grundlegenden Schritte in der folgenden Abbildung und der Liste unten wiederholen, bis die vollständige Definition of Done erfüllt ist.

![Testgesteuerter Entwicklungsprozess für Cloudzielzonen](../../_images/ready/test-driven-development-process.png)

- **Erstellen eines Tests:** Definieren Sie einen Test, um zu überprüfen, ob die Akzeptanzkriterien für ein bestimmtes Feature mit Mehrwert erfüllt sind. Automatisieren Sie den Test wann immer möglich.
- **Testen der Zielzone:** Führen Sie den neuen Test und alle vorhandenen Tests aus. Wenn das erforderliche Feature nicht bereits durch vorherigen Entwicklungsaufwand erfüllt wurde und nicht im Angebot des Cloudanbieters enthalten ist, sollte der Test fehlschlagen. Die Durchführung vorhandener Tests hilft zu überprüfen, dass Ihr neuer Test die Zuverlässigkeit der Zielzonenfeatures, die von vorhandenem Code bereitgestellt werden, nicht beeinträchtigt.
- **Erweitern und Umgestalten der Zielzone:** Fügen Sie den Quellcode hinzu oder modifizieren Sie ihn, um das gewünschte Feature mit Mehrwert zu erfüllen und die allgemeine Qualität der Codebasis zu verbessern. Das Cloudplattformteam würde nur Code hinzufügen, der dem gewünschten Feature entspricht (und nicht mehr), um vollständig im Sinne der testgesteuerten Entwicklung zu handeln. Gleichzeitig ist die Codequalität und -wartung ein gemeinsamer Aufwand. Bei der Erfüllung von Anforderungen für neue Features sollte das Cloudplattformteam versuchen, den Code zu optimieren, indem es die Duplizierung entfernt und den Code klarer gestaltet. Das Ausführen von Tests zwischen der Erstellung neuen Codes und dem Refactoring des Quellcodes wird dringend empfohlen.
- **Bereitstellen der Zielzone:** Sobald der Quellcode in der Lage ist, die Featureanforderungen zu erfüllen, stellen Sie die modifizierte Zielzone dem Cloudanbieter in einer kontrollierten Test- oder Sandboxumgebung zur Verfügung.
- **Testen der Zielzone:** Beim erneuten Testen der Zielzone muss überprüft werden, ob der neue Code die Akzeptanzkriterien für das angeforderte Feature erfüllt. Nachdem alle Tests bestanden wurden, wird das Feature als abgeschlossen betrachtet, und die Akzeptanzkriterien gelten als erfüllt.

Wenn alle Features mit Mehrwert und die Akzeptanzkriterien die entsprechenden Tests bestanden haben, ist die Zielzone bereit, die nächste Welle des Cloudeinführungsplans zu unterstützen.

## <a name="simple-example-of-a-definition-of-done"></a>Einfaches Beispiel für eine „Definition of Done“

Für einen anfänglichen Migrationsaufwand kann die „Definition of Done“ zu einfach sein. Im Folgenden finden Sie ein Beispiel für eines dieser zu einfachen Beispiele.

- Die anfängliche Zielzone wird zum Hosten von 10 Workloads für erste Lernzwecke genutzt. Diese Workloads sind nicht geschäftskritisch und haben keinen Zugriff auf vertrauliche Daten. Es ist wahrscheinlich, dass diese Arbeitslasten in Zukunft für die Produktion freigegeben werden, aber die Wichtigkeit und Vertraulichkeit wird sich voraussichtlich nicht ändern. Um diese Workloads zu unterstützen, muss das Cloudeinführungsteam die folgenden Kriterien erfüllen:

- Netzwerksegmentierung zur Anpassung an den vorgeschlagenen Netzwerkentwurf.
- Zugriff auf Compute-, Speicher- und Netzwerkressourcen zur Bewältigung der Workloads, die auf die Ermittlung digitaler Ressourcen ausgerichtet sind.
- Benennungs- und Kennzeichnungsschema für die einfache Anwendung.
- Diese Umgebung sollte als _Umkreisnetzwerk (DMZ)_ mit Zugang zum öffentlichen Internet behandelt werden.
- Während des Einführungsaufwands wünscht das Cloudeinführungsteam einen temporären Zugriff auf die Umgebung, um Dienstkonfigurationen zu ändern.
- Nur zur Kenntnisnahme: Vor der Produktionsfreigabe erfordern diese Workloads eine Integration mit dem Unternehmensidentitätsanbieter, um die fortlaufende Identität und den Zugriff für Vorgangsverwaltungzwecke zu regeln. Zu diesem Zeitpunkt sollte der Zugriff des Cloudeinführungsteams widerrufen werden.

Der letzte Punkt oben ist weder ein Feature noch ein Akzeptanzkriterium. Es ist jedoch ein Indikator dafür, dass zusätzliche Erweiterungen erforderlich sein werden, die mit anderen Teams frühzeitig untersucht werden sollten.

## <a name="additional-examples-of-a-definition-of-done"></a>Weitere Beispiele für eine „Definition of Done“

Die Governancemethodik innerhalb des Cloud Adoption Frameworks bietet eine erzählerische Reise durch den natürliche Entwicklungsverlaufs eines Governanceteams. Eingebettet in diese Reise sind mehrere Beispiele für „Definition of Done“ und „Akzeptanzkriterien“ in Form von Richtlinienanweisungen.

- [Anfängliche Richtlinienanweisungen](../../govern/guides/complex/initial-corporate-policy.md#policy-statements): Beispiel für steuernde Unternehmensrichtlinien und die anfängliche „Definition of Done“ auf der Grundlage der Einführungsanforderungen in einer frühen Phase.
- [Identitätserweiterung](../../govern/guides/complex/identity-baseline-improvement.md#incremental-improvement-of-the-policy-statements): Beispiel für steuernde Unternehmensrichtlinien („Definition of Done“), um die Anforderungen zum Erweitern der Identitätsverwaltung für eine Zielzone zu erfüllen.
- [Sicherheitserweiterung](../../govern/guides/complex/security-baseline-improvement.md#incremental-improvement-of-the-policy-statements): Beispiel für steuernde Unternehmensrichtlinien („Definition of Done“), um die Anforderungen an die Sicherheit zu erfüllen, die mit dem Referenzplan für die Cloudeinführung ausgerichtet sind.
- [Vorgangserweiterung](../../govern/guides/complex/resource-consistency-improvement.md#incremental-improvement-of-the-policy-statements): Beispiel für steuernde Unternehmensrichtlinien („Definition of Done“), um grundlegende Anforderungen an die Vorgangsverwaltung zu erfüllen.
- [Kostenexpansion](../../govern/guides/complex/cost-management-improvement.md#changes-to-the-policy-statements): Beispiel für steuernde Unternehmensrichtlinien („Definition of Done“), um Anforderungen an die Kostenverwaltung zu erfüllen.

Die obigen Beispiele sind einfache Beispiele, die Ihnen helfen, eine „Definition of Done“ für Ihre Zielzonen zu entwickeln. Weitere Beispielrichtlinien sind unter den einzelnen [Disziplinen von Cloudgovernance](../../govern/governance-disciplines.md) verfügbar.

## <a name="next-steps"></a>Nächste Schritte

Informationen zum Beschleunigen der testgesteuerten Entwicklung in Azure finden Sie unter [Testgesteuerte Entwicklungsfeatures von Azure](./azure-test-driven-development.md).

> [!div class="nextstepaction"]
> [Testgesteuerte Entwicklung in Azure](./azure-test-driven-development.md)
