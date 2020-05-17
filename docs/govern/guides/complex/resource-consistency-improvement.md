---
title: 'Governance in komplexen Unternehmen: Verbessern der Disziplin „Ressourcenkonsistenz“'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um die Governancebaseline zu optimieren und Risiken zu mindern, indem Sie sich mit der Wiederherstellung, Dimensionierung und Überwachung vertraut machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b5bb646fd658f3b0c4393b0f68c5d449ee53db08
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219970"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-resource-consistency-discipline"></a>Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Ressourcenkonsistenz“

In diesem Artikel wird die Lösung weiterentwickelt, indem Steuerelemente für Ressourcenkonsistenz zum Governance-MVP hinzugefügt werden, um unternehmenskritische Anwendungen zu unterstützen.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Die Teams zur Cloudeinführung haben alle Anforderungen für die Verschiebung geschützter Daten erfüllt. Diese Anwendungen bringen SLA-Verpflichtungen für das Unternehmen und den Bedarf an Unterstützung durch das IT-Betriebsteam mit sich. Direkt hinter dem Team, das die zwei Rechenzentren migriert, stehen mehrere Anwendungsentwicklungs- und Business Intelligence-Teams bereit, um mit dem Start neuer Lösungen in der Produktion zu beginnen. Für den IT-Betrieb ist der Gedanke von Cloudabläufen neu, und es wird eine Möglichkeit zur schnellen Integration bestehender Betriebsprozesse benötigt.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

- IT verschiebt aktiv Produktionsworkloads mit geschützten Daten nach Azure. Einige Workloads mit niedriger Priorität bedienen den Produktionsdatenverkehr. Weitere können umgestellt werden, sobald das IT-Betriebsteam die Bereitschaft zur Unterstützung der Workloads signalisiert.
- Die Anwendungsentwicklungsteams sind für Produktionsdatenverkehr bereit.
- Das Business Intelligence-Team steht bereit, Prognosen und Erkenntnisse in die Systeme zu integrieren, die den Betrieb für die drei Geschäftseinheiten tragen.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

- Für den IT-Betrieb ist der Gedanke von Cloudabläufen neu, und es wird eine Möglichkeit zur schnellen Integration bestehender Betriebsprozesse benötigt.
- Die Änderungen des aktuellen und zukünftigen Status bergen neue Risiken, die neue Richtlinienanweisungen erfordern.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Unterbrechung des Geschäftsbetriebs:** Jede neue Plattform bringt ein inhärentes Risiko für Unterbrechungen in unternehmenskritischen Geschäftsabläufen mit sich. Das IT-Betriebsteam und die Teams, die verschiedene Cloudeinführungen vornehmen, sind relativ unerfahren in Cloudvorgängen. Dadurch steigt die Gefahr von Unterbrechungen, die entsprechend verringert und kontrolliert werden muss.

Dieses Geschäftsrisiko lässt sich auf eine Reihe von technischen Risiken ausweiten:

1. Falsch ausgerichtete Betriebsprozesse können zu Ausfällen führen, die nicht erkannt oder schnell korrigiert werden können.
2. Ein Eindringen von außerhalb oder Denial-of-Service-Angriffe können zu einer Unterbrechung des Geschäftsbetriebs führen.
3. Unternehmenswichtige Ressourcen werden möglicherweise nicht korrekt identifiziert und daher nicht ordnungsgemäß betrieben.
4. Nicht identifizierte oder falsch bezeichnete Ressourcen werden möglicherweise durch die vorhandenen Prozesse des Betriebsmanagements nicht unterstützt.
5. Die Konfiguration der bereitgestellten Ressourcen erfüllt möglicherweise nicht die Leistungserwartungen.
6. Die Protokollierung wird eventuell nicht ordnungsgemäß aufgezeichnet und ist nicht korrekt zentralisiert, um die Behebung der Leistungsprobleme zu ermöglichen.
7. Bei Wiederherstellungsrichtlinien treten möglicherweise Fehler auf, oder ihre Ausführung dauert länger als erwartet.
8. Inkonsistente Bereitstellungsprozesse können Sicherheitslücken verursachen, die zu Datenverlusten oder Unterbrechungen führen können.
9. Konfigurationsabweichungen oder fehlende Patches können unbeabsichtigte Sicherheitslücken zur Folge haben, die zu Datenverlusten oder Unterbrechungen führen können.
10. Die Konfiguration setzt möglicherweise die Anforderungen der definierten SLAs oder der festgeschriebenen Wiederherstellungsanforderungen nicht durch.
11. Die bereitgestellten Betriebssysteme oder Anwendungen genügen eventuell nicht den Härtungsanforderungen an Betriebssysteme und Anwendungen.
12. Es besteht die Gefahr von Inkonsistenzen aufgrund der verschiedenen Teams, die in der Cloud arbeiten.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung. Die Liste wirkt lang, aber die Einführung dieser Richtlinien ist möglicherweise einfacher, als es den Anschein hat.

1. Alle bereitgestellten Ressourcen müssen nach Wichtigkeit und Datenklassifizierung kategorisiert werden. Vor der Bereitstellung in der Cloud müssen die Klassifizierungen durch das Cloudgovernanceteam und die Besitzer der Anwendung überprüft werden.
2. Subnetze, die unternehmenskritische Anwendungen enthalten, müssen durch eine Firewalllösung geschützt werden, die Eindringversuche erkennen und auf Angriffe reagieren kann.
3. Die Anforderungen an die Netzwerkkonfiguration, die vom Sicherheitsbaselineteam definiert wurden, müssen mit Governancetools überwacht und durchgesetzt werden.
4. Mit den Governancetools muss überprüft werden, ob alle Ressourcen, die in einem Zusammenhang mit unternehmenskritischen Anwendungen oder geschützten Daten stehen, in die Überwachung auf Ressourcenschwund und -optimierung einbezogen sind.
5. Ferner muss mit den Governancetools überprüft werden, ob für alle unternehmenskritischen Anwendungen oder geschützten Daten Protokolldaten mit dem passenden Protokolliergrad erfasst werden.
6. Der Governanceprozess muss überprüfen, ob für unternehmenskritische Anwendungen und geschützte Daten die Sicherung, Wiederherstellung und Einhaltung von SLAs ordnungsgemäß implementiert sind.
7. Mit den Governancetools muss die Bereitstellung virtueller Computer ausschließlich auf genehmigte Images eingeschränkt werden.
8. Die Governancetools müssen erzwingen, dass für alle bereitgestellten Ressourcen, die unternehmenskritische Anwendungen unterstützen, automatische Updates **verhindert** werden. Verstöße müssen von Betriebsmanagementteams überprüft und in Übereinstimmung mit den Betriebsrichtlinien beseitigt werden. Ressourcen, die nicht automatisch aktualisiert werden, müssen in Prozesse des IT-Betriebs einbezogen werden, um eine schnelle und effektive Aktualisierung dieser Server zu gewährleisten.
9. Mit Governancetools muss die Kennzeichnung (Tagging) im Hinblick auf Kosten, Kritikalität, SLA, Anwendung und Datenklassifizierung überprüft werden. Alle Werte müssen sich an vordefinierten Werten ausrichten, die vom Cloudgovernanceteam verwaltet werden.
10. Governanceprozesse müssen Überwachungen zum Bereitstellungszeitpunkt und nachfolgend in regelmäßigen Zyklen umfassen, um für alle Ressourcen Konsistenz zu gewährleisten.
11. Trends und Exploits, die Auswirkungen auf Cloudbereitstellungen haben könnten, müssen vom Sicherheitsteam regelmäßig überprüft werden, damit Updates für in der Cloud verwendete Sicherheitsbaselinetools bereitgestellt werden können.
12. Vor der Veröffentlichung in einer Produktionsumgebung müssen alle unternehmenskritischen Anwendungen und geschützten Daten der designierten Betriebsüberwachungslösung hinzugefügt werden. Ressourcen, die von den gewählten IT Operations-Tools nicht erkannt werden können, können nicht für die Produktion freigegeben werden. Alle Änderungen, die erforderlich sind, um die Ressourcen erkennbar zu machen, müssen an den relevanten Bereitstellungsprozessen vorgenommen werden, um sicherzustellen, dass die Ressourcen in kommenden Bereitstellungen ermitelbar sind.
13. Bei der Ermittlung muss die Ressourcendimensionierung von den Betriebsmanagementteams überprüft werden, um sicherzustellen, dass die Ressourcen den Leistungsanforderungen genügen.
14. Bereitstellungstools müssen vom Cloudgovernanceteam genehmigt werden, um eine kontinuierliche Governance für bereitgestellte Ressourcen sicherzustellen.
15. Bereitstellungsskripts müssen in einem zentralen Repository aufbewahrt werden, das für das Cloudgovernanceteam zur regelmäßigen Überprüfung und Überwachung zugänglich ist.
16. Mithilfe von Governanceprüfprozessen muss bestätigt werden, dass die bereitgestellten Ressourcen im Hinblick auf SLA- und Wiederherstellungsanforderungen ordnungsgemäß konfiguriert sind.

## <a name="incremental-improvement-of-the-best-practices"></a>Inkrementelle Verbesserungen der bewährten Methoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so verbessert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

Nach den Erfahrungen mit diesem fiktiven Beispiel wird davon ausgegangen, dass die Änderungen der geschützten Daten bereits erfolgt sind. Aufbauend auf diesen bewährten Verfahren, werden in der Folge Anforderungen an die Betriebsüberwachung hinzugefügt, mit denen ein Abonnement für geschäftskritische Anwendungen vorbereitet wird.

**Unternehmenseigenes IT-Abonnement:** Fügen Sie dem unternehmenseigenen IT-Abonnement, das als Hub fungiert, Folgendes hinzu.

1. Als externe Abhängigkeit muss das Cloud Operations-Team Tools für die Betriebsüberwachung, BCDR-Tools (Business Continuity/Disaster Recovery) und Tools zur automatisierten Wartung definieren. Damit kann das Cloudgovernanceteam die erforderlichen Ermittlungsvorgänge unterstützen.
    1. In diesem Anwendungsfall hat das Cloud Operations-Team Azure Monitor als primäres Tool für die Überwachung unternehmenskritischer Anwendungen ausgewählt.
    2. Das Team sich ferner für Azure Site Recovery als primäres BCDR-Tool entschieden.
2. Azure Site Recovery-Implementierung:
    1. Definieren Sie einen Azure Site Recovery-Tresor für Sicherungs- und Wiederherstellungsvorgänge, und stellen Sie ihn bereit.
    2. Erstellen Sie eine Azure-Ressourcenverwaltungsvorlage zur Erstellung eines Tresors in jedem Abonnement.
3. Azure Monitor-Implementierung:
    1. Nachdem ein unternehmenskritisches Abonnement ermittelt wurde, kann ein Log Analytics-Arbeitsbereich erstellt werden.

**Individuelles Abonnement zur Cloudeinführung:** Mit den folgenden Maßnahmen stellen Sie sicher, dass jedes Abonnement von der Überwachungslösung ermittelbar und zur Aufnahme in BCDR-Praktiken bereit ist.

1. Azure-Richtlinie für unternehmenskritische Knoten:
    1. Überwachen und erzwingen Sie die ausschließliche Verwendung von Standardrollen.
    2. Überwachen und erzwingen Sie die Anwendung von Verschlüsselung für alle Speicherkonten.
    3. Überwachen und erzwingen Sie die Verwendung eines genehmigten Netzwerksubnetzes und virtuellen Netzwerks pro Netzwerkschnittstelle.
    4. Überwachen und erzwingen Sie die Einschränkung benutzerdefinierter Routingtabellen.
    5. Überwachen und erzwingen Sie die Bereitstellung von Log Analytics-Agents für virtuelle Windows- und Linux-Computer.
2. Azure-Blaupause:
    1. Erstellen Sie eine Blaupause mit dem Namen `mission-critical-workloads-and-protected-data`. Diese Blaupause betrifft Ressourcen, in Ergänzung zur Blaupause der geschützten Daten.
    2. Fügen Sie der Blaupause die neuen Azure-Richtlinien hinzu.
    3. Wenden Sie die Blaupause auf jedes Abonnement an, von dem angenommen wird, dass es eine unternehmenskritische Anwendung hostet.

## <a name="conclusion"></a>Zusammenfassung

Durch das Hinzufügen dieser Prozesse und Änderungen zum Governance-MVP lassen sich viele Risiken im Zusammenhang mit der Ressourcengovernance minimieren. In Kombination fügen Sie die Steuerelemente für Wiederherstellung, Dimensionierung und Überwachung hinzu, die zum Ermöglichen eines cloudfähigen Betriebs erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Mit dem Wachstum der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an Cloud Governance. Für das fiktive Unternehmen in diesem Leitfaden kommt der nächste Trigger, wenn die Größe der Bereitstellung 1.000 Ressourcen in der Cloud oder die monatlichen Ausgaben 10.000 US-Dollar übersteigen. An diesem Punkt fügt das Cloudgovernanceteam Steuerelemente für die Kostenverwaltung hinzu.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Cost Management“](./cost-management-improvement.md)
