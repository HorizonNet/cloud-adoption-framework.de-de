---
title: 'Governance für Standardunternehmen: Verbessern der Disziplin „Ressourcenkonsistenz“'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über die Optimierung der Governancebaseline zu informieren und zu erfahren, wie Sie Risiken mindern, indem Sie Steuerelemente für die Wiederherstellung, Dimensionierung und Überwachung hinzufügen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2284bfc4b2b31142e1356955a0a8941799bf997a
ms.sourcegitcommit: c2249056464d748a6ce15c82cb35a9f164d8f661
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91107994"
---
# <a name="standard-enterprise-governance-guide-improve-the-resource-consistency-discipline"></a>Governanceleitfaden für Standardunternehmen: Verbessern der Disziplin „Ressourcenkonsistenz“

In diesem Artikel wird die Lösung weiterentwickelt, indem Steuerelemente für Ressourcenkonsistenz hinzugefügt werden, um unternehmenskritische Anwendungen zu unterstützen.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Neue Kundenerfahrungen, neue Vorhersagetools und migrierte Infrastruktur entwickeln sich weiter. Das Unternehmen kann jetzt damit beginnen, diese Ressourcen mit einer Produktionskapazität zu verwenden.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Lösung waren die Anwendungsentwicklungs- und BI-Teams nahezu bereit, Kunden- und Finanzdaten in die Produktionsworkloads zu integrieren. Das IT-Team war dabei, das DR-Datencenter außer Betrieb zu nehmen.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Die IT-Abteilung hat 100 % des DR-Datencenters vorzeitig außer Betrieb genommen. Während des Prozesses wurden mehrere Ressourcen im Produktionsrechenzentrum als Cloudmigrationskandidaten identifiziert.
- Die Anwendungsentwicklungsteams sind nun für Produktionsdatenverkehr bereit.
- Das BI-Team ist bereit, Vorhersagen und Erkenntnisse wieder an die Betriebssysteme im Produktionsrechenzentrum zu übermitteln.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Bevor Azure-Bereitstellungen in Produktionsgeschäftsprozessen eingesetzt werden können, muss der Cloudbetrieb ausgereift sein. In Verbindung damit sind zusätzliche Änderungen der Governance erforderlich, um sicherzustellen, dass Ressourcen ordnungsgemäß betrieben werden können.

Die Änderungen des aktuellen und zukünftigen Status bergen neue Risiken, die neue Richtlinienanweisungen erfordern.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Unterbrechung des Geschäftsbetriebs:** Jede neue Plattform bringt ein inhärentes Risiko für Unterbrechungen in unternehmenskritischen Geschäftsabläufen mit sich. Das IT-Betriebsteam und die Teams, die verschiedene Cloudeinführungen vornehmen, sind relativ unerfahren in Cloudvorgängen. Dadurch steigt die Gefahr von Unterbrechungen, die entsprechend verringert und kontrolliert werden muss.

Dieses Geschäftsrisiko lässt sich auf eine Reihe von technischen Risiken ausweiten:

1. Ein Eindringen von außerhalb oder Denial-of-Service-Angriffe können zu einer Unterbrechung des Geschäftsbetriebs führen.
1. Unternehmenswichtige Ressourcen werden möglicherweise nicht richtig identifiziert und daher nicht ordnungsgemäß betrieben.
1. Nicht identifizierte oder falsch bezeichnete Ressourcen werden möglicherweise durch die vorhandenen Prozesse des Betriebsmanagements nicht unterstützt.
1. Die Konfiguration der bereitgestellten Ressourcen erfüllt möglicherweise nicht die Leistungserwartungen.
1. Die Protokollierung wird eventuell nicht ordnungsgemäß aufgezeichnet und ist nicht korrekt zentralisiert, um die Behebung der Leistungsprobleme zu ermöglichen.
1. Bei Wiederherstellungsrichtlinien treten möglicherweise Fehler auf, oder ihre Ausführung dauert länger als erwartet.
1. Inkonsistente Bereitstellungsprozesse können Sicherheitslücken verursachen, die zu Datenverlusten oder Unterbrechungen führen können.
1. Konfigurationsabweichungen oder fehlende Patches können unbeabsichtigte Sicherheitslücken zur Folge haben, die zu Datenverlusten oder Unterbrechungen führen können.
1. Die Konfiguration setzt möglicherweise die Anforderungen der definierten SLAs oder der festgeschriebenen Wiederherstellungsanforderungen nicht durch.
1. Die bereitgestellten Betriebssysteme oder Anwendungen genügen möglicherweise nicht den Härtungsanforderungen.
1. Aufgrund der zahlreichen Teams, die in der Cloud arbeiten, besteht die Gefahr von Inkonsistenzen.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung. Die Liste wirkt lang, aber die Einführung dieser Richtlinien ist möglicherweise einfacher, als es den Anschein hat.

1. Alle bereitgestellten Ressourcen müssen nach Wichtigkeit und Datenklassifizierung kategorisiert werden. Vor der Bereitstellung in der Cloud müssen die Klassifizierungen durch das Cloudgovernanceteam und die Besitzer der Anwendung überprüft werden.
1. Subnetze, die unternehmenskritische Anwendungen enthalten, müssen durch eine Firewalllösung geschützt werden, die Eindringversuche erkennen und auf Angriffe reagieren kann.
1. Die Anforderungen an die Netzwerkkonfiguration, die vom Sicherheitsverwaltungsteam definiert wurden, müssen mit Governancetools überwacht und durchgesetzt werden.
1. Mit den Governancetools muss überprüft werden, ob alle Ressourcen, die in einem Zusammenhang mit unternehmenskritischen Anwendungen oder geschützten Daten stehen, in die Überwachung auf Ressourcenschwund und -optimierung einbezogen sind.
1. Ferner muss mit den Governancetools überprüft werden, ob für alle unternehmenskritischen Anwendungen oder geschützten Daten Protokolldaten mit dem passenden Protokolliergrad erfasst werden.
1. Der Governanceprozess muss überprüfen, ob für unternehmenskritische Anwendungen und geschützte Daten die Sicherung, Wiederherstellung und Einhaltung von SLAs ordnungsgemäß implementiert sind.
1. Mit den Governancetools müssen die Bereitstellungen virtueller Computer ausschließlich auf genehmigte Images eingeschränkt werden.
1. Die Governancetools müssen erzwingen, dass für alle bereitgestellten Ressourcen, die unternehmenskritische Anwendungen unterstützen, automatische Updates verhindert werden. Verstöße müssen von Betriebsmanagementteams überprüft und in Übereinstimmung mit den Betriebsrichtlinien beseitigt werden. Ressourcen, die nicht automatisch aktualisiert werden, müssen in Prozesse einbezogen werden, die IT Operations unterstehen.
1. Mit Governancetools muss die Kennzeichnung (Tagging) im Hinblick auf Kosten, Kritikalität, SLA, Anwendung und Datenklassifizierung überprüft werden. Alle Werte müssen sich an vordefinierten Werten ausrichten, die vom Governance-Team verwaltet werden.
1. Governanceprozesse müssen Überwachungen zum Bereitstellungszeitpunkt und nachfolgend in regelmäßigen Zyklen umfassen, um für alle Ressourcen Konsistenz zu gewährleisten.
1. Trends und Exploits, die mögliche Auswirkungen auf Cloudbereitstellungen haben, müssen vom Sicherheitsteam regelmäßig überprüft werden, damit Updates für in der Cloud verwendete Sicherheitsverwaltungstools bereitgestellt werden.
1. Vor der Veröffentlichung in einer Produktionsumgebung müssen alle unternehmenskritischen Anwendungen und geschützten Daten der designierten Betriebsüberwachungslösung hinzugefügt werden. Ressourcen, die von den gewählten IT Operations-Tools nicht erkannt werden können, können nicht für die Produktion freigegeben werden. Alle Änderungen, die erforderlich sind, um die Ressourcen erkennbar zu machen, müssen an den relevanten Bereitstellungsprozessen vorgenommen werden, um sicherzustellen, dass die Ressourcen in kommenden Bereitstellungen ermitelbar sind.
1. Bei der Ermittlung dimensionieren die operativen Managementteams die Ressourcen, um sicherzustellen, dass die Ressourcen den Leistungsanforderungen entsprechen.
1. Bereitstellungstools müssen vom Cloudgovernanceteam genehmigt werden, um eine kontinuierliche Governance für bereitgestellte Ressourcen sicherzustellen.
1. Bereitstellungsskripts müssen in einem zentralen Repository aufbewahrt werden, das für das Cloudgovernanceteam zur regelmäßigen Überprüfung und Überwachung zugänglich ist.
1. Mithilfe von Governanceprüfprozessen muss bestätigt werden, dass die bereitgestellten Ressourcen im Hinblick auf SLA- und Wiederherstellungsanforderungen ordnungsgemäß konfiguriert sind.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so geändert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management + Billing umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

1. Das Cloud Operations-Team definiert operative Überwachungstools und automatisierte Korrekturtools. Das Cloudgovernanceteam unterstützt diese Ermittlungsprozesse. In diesem Anwendungsfall hat das Cloud Operations-Team Azure Monitor als primäres Tool für die Überwachung unternehmenskritischer Anwendungen ausgewählt.
2. Erstellen Sie in Azure DevOps ein Repository zur Speicherung und Versionsverwaltung für alle relevanten Resource Manager-Vorlagen und Skriptkonfigurationen.
3. Azure Recovery Services-Tresorimplementierung:
    1. Definieren Sie einen Azure Recovery Services-Tresor für Sicherungs- und Wiederherstellungsvorgänge, und stellen Sie ihn bereit.
    2. Erstellen Sie eine Resource Manager-Vorlage zum Erstellen eines Tresors in jedem Abonnement.
4. Aktualisieren Sie Azure Policy für alle Abonnements:
    1. Überprüfen und erzwingen Sie die Wichtigkeits- und Datenklassifizierung für alle Abonnements, um Abonnements mit unternehmenskritischen Ressourcen zu identifizieren.
    2. Überwachen und erzwingen Sie die ausschließliche Verwendung genehmigter Images.
5. Azure Monitor-Implementierung:
    1. Nachdem eine unternehmenskritische Workload identifiziert wurde, erstellen Sie einen Azure Monitor Log Analytics-Arbeitsbereich.
    2. Während der Bereitstellungstests stellt das Cloud Operations-Team die erforderlichen Agents bereit und testet die Ermittlung.
6. Aktualisieren Sie Azure Policy für alle Abonnements, die unternehmenskritische Anwendungen enthalten.
    1. Überwachen und erzwingen Sie die Anwendung einer NSG auf alle NICs und Subnetze. Die Netzwerk- und die IT-Sicherheit definieren die NSG.
    2. Überwachen und erzwingen Sie die Verwendung von genehmigten Netzwerksubnetzen und virtuellen Netzwerken für jede Netzwerkschnittstelle.
    3. Überwachen und erzwingen Sie die Einschränkung benutzerdefinierter Routingtabellen.
    4. Überwachen und erzwingen Sie die Bereitstellung von Azure Monitor-Agents für alle virtuellen Computer.
    5. Überprüfen Sie, ob Azure Recovery Services-Tresore im Abonnement vorhanden sind, und erzwingen Sie deren Bereitstellung.
7. Firewallkonfiguration:
    1. Identifizieren Sie eine Konfiguration von Azure Firewall, die die Sicherheitsanforderungen erfüllt. Identifizieren Sie alternativ eine Appliance eines Drittanbieters, die mit Azure kompatibel ist.
    1. Erstellen Sie eine Resource Manager-Vorlage, um die Firewall mit den erforderlichen Konfigurationen bereitzustellen.
8. Azure-Blaupause:
    1. Erstellen Sie eine neue Azure-Blaupause namens `protected-data`.
    2. Fügen Sie der Blaupause die Firewall und die Azure Recovery Services-Tresorvorlagen hinzu.
    3. Fügen Sie die neuen Richtlinien für Abonnements geschützter Daten hinzu.
    4. Veröffentlichen Sie die Blaupause für alle Verwaltungsgruppen, die zum Hosten unternehmenskritischer Anwendungen verwendet werden.
    5. Wenden Sie die neue Blaupause zusammen mit vorhandenen Blaupausen auf die betroffenen Abonnements an.

## <a name="conclusion"></a>Zusammenfassung

Durch diese zusätzlichen Prozesse und Änderungen am Governance-MVP lassen sich viele Risiken im Zusammenhang mit der Ressourcengovernance umgehen. In Kombination fügen sie die Steuerelemente für Wiederherstellung, Dimensionierung und Überwachung hinzu, die einen cloudfähigen Betrieb ermöglichen.

## <a name="next-steps"></a>Nächste Schritte

Mit der Fortsetzung der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an die Cloudgovernance. Für das fiktive Unternehmen in diesem Leitfaden wird der nächste Trigger ausgelöst, wenn die Größe der Bereitstellung 100 Ressourcen in der Cloud oder monatliche Ausgaben von 1.000 US-Dollar übersteigt. An diesem Punkt fügt das Cloudgovernanceteam Steuerelemente für die Kostenverwaltung hinzu.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Cost Management“](./cost-management-improvement.md)
