---
title: 'Governance für Standardunternehmen: Verbessern der Ressourcenkonsistenz'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über die Optimierung der Governancebaseline zu informieren und zu erfahren, wie Sie Risiken mindern, indem Sie Steuerelemente für die Wiederherstellung, Dimensionierung und Überwachung hinzufügen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 57358a9933c6f18d72678c3c4ba82bef90e713a0
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170816"
---
# <a name="standard-enterprise-governance-guide-improving-resource-consistency"></a>Governanceleitfaden für Standardunternehmen: Verbessern der Ressourcenkonsistenz

Dieser Artikel führt die Geschichte fort, indem Steuerelemente für Ressourcenkonsistenz hinzugefügt werden, um unternehmenskritische Apps zu unterstützen.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Neue Kundenerfahrungen, neue Vorhersagetools und migrierte Infrastruktur entwickeln sich weiter. Das Unternehmen kann jetzt damit beginnen, diese Ressourcen mit einer Produktionskapazität zu verwenden.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Lösung waren die Anwendungsentwicklungs- und BI-Teams nahezu bereit, Kunden- und Finanzdaten in die Produktionsworkloads zu integrieren. Das IT-Team war dabei, das DR-Datencenter außer Betrieb zu nehmen.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Die IT-Abteilung hat 100 % des DR-Datencenters vorzeitig außer Betrieb genommen. Dabei wurde ein Satz von Ressourcen im Produktionsrechenzentrum als Cloudmigrationskandidaten identifiziert.
- Die Anwendungsentwicklungsteams sind nun für Produktionsdatenverkehr bereit.
- Das BI-Team ist bereit, Vorhersagen und Erkenntnisse in die Betriebssysteme im Produktionsdatencenter zurückzuliefern.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Bevor Azure-Bereitstellungen in Produktionsgeschäftsprozessen eingesetzt werden können, muss der Cloudbetrieb ausgereift sein. In Verbindung damit sind zusätzliche Änderungen der Governance erforderlich, um sicherzustellen, dass Ressourcen ordnungsgemäß betrieben werden können.

Die Änderungen des aktuellen und zukünftigen Status bergen neue Risiken, die neue Richtlinienanweisungen erfordern.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Unterbrechung des Geschäftsbetriebs:** Jede neue Plattform bringt ein inhärentes Risiko für Unterbrechungen in unternehmenskritischen Geschäftsabläufen mit sich. Das IT Operations-Team und die Teams, die in verschiedenen Cloud-Einsatztypen agieren, sind relativ unerfahren in Cloud Operations. Dadurch steigt die Gefahr von Unterbrechungen, die entsprechend verringert und kontrolliert werden muss.

Dieses Geschäftsrisiko lässt sich auf eine Reihe von technischen Risiken ausweiten:

1. Ein Eindringen von außerhalb oder Denial-of-Service-Angriffe können zu einer Unterbrechung des Geschäftsbetriebs führen.
2. Unternehmenswichtige Ressourcen werden möglicherweise nicht richtig identifiziert und daher nicht ordnungsgemäß betrieben.
3. Nicht identifizierte oder falsch bezeichnete Ressourcen werden möglicherweise durch die vorhandenen Prozesse des Betriebsmanagements nicht unterstützt.
4. Die Konfiguration der bereitgestellten Ressourcen erfüllt möglicherweise nicht die Leistungserwartungen.
5. Die Protokollierung wird eventuell nicht ordnungsgemäß aufgezeichnet und ist nicht korrekt zentralisiert, um die Behebung der Leistungsprobleme zu ermöglichen.
6. Bei Wiederherstellungsrichtlinien treten möglicherweise Fehler auf, oder ihre Ausführung dauert länger als erwartet.
7. Inkonsistente Bereitstellungsprozesse können Sicherheitslücken verursachen, die zu Datenverlusten oder Unterbrechungen führen können.
8. Konfigurationsabweichungen oder fehlende Patches können unbeabsichtigte Sicherheitslücken zur Folge haben, die zu Datenverlusten oder Unterbrechungen führen können.
9. Die Konfiguration setzt möglicherweise die Anforderungen der definierten SLAs oder der festgeschriebenen Wiederherstellungsanforderungen nicht durch.
10. Die bereitgestellten Betriebssysteme oder Anwendungen genügen möglicherweise nicht den Härtungsanforderungen.
11. Aufgrund der zahlreichen Teams, die in der Cloud arbeiten, besteht die Gefahr von Inkonsistenzen.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung. Die Liste wirkt lang, aber die Einführung dieser Richtlinien ist möglicherweise einfacher, als es den Anschein hat.

1. Alle bereitgestellten Ressourcen müssen nach Wichtigkeit und Datenklassifizierung kategorisiert werden. Vor der Bereitstellung in der Cloud müssen die Klassifizierungen durch das Cloudgovernanceteam und die Besitzer der Anwendung überprüft werden.
2. Subnetze, die unternehmenskritische Anwendungen enthalten, müssen durch eine Firewalllösung geschützt werden, die Eindringversuche erkennen und auf Angriffe reagieren kann.
3. Die Anforderungen an die Netzwerkkonfiguration, die vom Sicherheitsmanagementteam definiert wurden, müssen mit Governancetools überwacht und durchgesetzt werden.
4. Mit den Governancetools muss überprüft werden, ob alle Ressourcen, die in einem Zusammenhang mit unternehmenskritischen Apps oder geschützten Daten stehen, in die Überwachung auf Ressourcenschwund und -optimierung einbezogen sind.
5. Ferner muss mit den Governancetools überprüft werden, ob für alle unternehmenskritischen Anwendungen oder geschützten Daten Protokolldaten mit dem passenden Protokolliergrad erfasst werden.
6. Der Governanceprozess muss überprüfen, ob für unternehmenskritische Anwendungen und geschützte Daten die Sicherung, Wiederherstellung und Einhaltung von SLAs ordnungsgemäß implementiert sind.
7. Mit den Governancetools müssen die Bereitstellungen virtueller Computer ausschließlich auf genehmigte Images eingeschränkt werden.
8. Die Governancetools müssen erzwingen, dass für alle bereitgestellten Ressourcen, die unternehmenskritische Anwendungen unterstützen, automatische Updates verhindert werden. Verstöße müssen von Betriebsmanagementteams überprüft und in Übereinstimmung mit den Betriebsrichtlinien beseitigt werden. Ressourcen, die nicht automatisch aktualisiert werden, müssen in Prozesse des IT-Betriebs einbezogen werden.
9. Mit Governancetools muss die Kennzeichnung (Tagging) im Hinblick auf Kosten, Kritikalität, SLA, Anwendung und Datenklassifizierung überprüft werden. Alle Werte müssen sich an vordefinierten Werten ausrichten, die vom Governance-Team verwaltet werden.
10. Governanceprozesse müssen Überwachungen zum Bereitstellungszeitpunkt und nachfolgend in regelmäßigen Zyklen umfassen, um für alle Ressourcen Konsistenz zu gewährleisten.
11. Trends und Exploits, die mögliche Auswirkungen auf Cloudbereitstellungen haben, müssen vom Sicherheitsteam regelmäßig überprüft werden, damit Updates für in der Cloud verwendete Sicherheitsverwaltungstools bereitgestellt werden.
12. Vor der Veröffentlichung in einer Produktionsumgebung müssen alle unternehmenskritischen Apps und geschützten Daten der designierten Betriebsüberwachungslösung hinzugefügt werden. Ressourcen, die von den gewählten IT Operations-Tools nicht erkannt werden können, können nicht für die Produktion freigegeben werden. Alle Änderungen, die erforderlich sind, um die Ressourcen erkennbar zu machen, müssen an den relevanten Bereitstellungsprozessen vorgenommen werden, um sicherzustellen, dass die Ressourcen in kommenden Bereitstellungen ermitelbar sind.
13. Bei der Ermittlung dimensionieren die operativen Managementteams die Ressourcen, um sicherzustellen, dass die Ressourcen den Leistungsanforderungen entsprechen.
14. Bereitstellungstools müssen vom Cloudgovernanceteam genehmigt werden, um eine kontinuierliche Governance für bereitgestellte Ressourcen sicherzustellen.
15. Bereitstellungsskripts müssen in einem zentralen Repository aufbewahrt werden, das für das Cloudgovernanceteam zur regelmäßigen Überprüfung und Überwachung zugänglich ist.
16. Mithilfe von Governanceprüfprozessen muss bestätigt werden, dass die bereitgestellten Ressourcen im Hinblick auf SLA- und Wiederherstellungsanforderungen ordnungsgemäß konfiguriert sind.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so geändert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

1. Das Cloud Operations-Team definiert operative Überwachungstools und automatisierte Korrekturtools. Das Cloudgovernanceteam unterstützt diese Ermittlungsprozesse. In diesem Anwendungsfall hat das Cloud Operations-Team Azure Monitor als primäres Tool für die Überwachung unternehmenskritischer Anwendungen ausgewählt.
2. Erstellen Sie in Azure DevOps ein Repository zur Speicherung und Versionsverwaltung für alle relevanten Resource Manager-Vorlagen und Skriptkonfigurationen.
3. Azure Recovery Services-Tresorimplementierung:
    1. Definieren Sie einen Azure Recovery Services-Tresor für Sicherungs- und Wiederherstellungsvorgänge, und stellen Sie ihn bereit.
    2. Erstellen Sie eine Resource Manager-Vorlage zum Erstellen eines Tresors in jedem Abonnement.
4. Aktualisieren Sie Azure Policy für alle Abonnements:
    1. Überprüfen und erzwingen Sie die Wichtigkeits- und Datenklassifizierung für alle Abonnements, um Abonnements mit unternehmenskritischen Ressourcen zu identifizieren.
    2. Überwachen und erzwingen Sie die ausschließliche Verwendung genehmigter Images.
5. Azure Monitor-Implementierung:
    1. Nachdem eine unternehmenskritische Workload identifiziert wurde, erstellen Sie einen Azure Monitor-Arbeitsbereich.
    2. Während der Bereitstellungstests stellt das Cloud Operations-Team die erforderlichen Agents bereit und testet die Ermittlung.
6. Aktualisieren Sie Azure Policy für alle Abonnements, die unternehmenskritische Anwendungen enthalten.
    1. Überwachen und erzwingen Sie die Anwendung einer NSG auf alle NICs und Subnetze. Netzwerke und IT-Sicherheit definieren die NSG.
    2. Überwachen und erzwingen Sie die Verwendung genehmigter Netzwerksubnetze und VNETs für jede Netzwerkschnittstelle.
    3. Überwachen und erzwingen Sie die Einschränkung benutzerdefinierter Routingtabellen.
    4. Überwachen und erzwingen Sie die Bereitstellung von Azure Monitor-Agents für alle virtuellen Computer.
    5. Überprüfen Sie, ob Azure Recovery Services-Tresore im Abonnement vorhanden sind, und erzwingen Sie deren Bereitstellung.
7. Firewallkonfiguration:
    1. Identifizieren Sie eine Konfiguration von Azure Firewall, die die Sicherheitsanforderungen erfüllt. Identifizieren Sie alternativ eine Appliance eines Drittanbieters, die mit Azure kompatibel ist.
    1. Erstellen Sie eine Resource Manager-Vorlage, um die Firewall mit den erforderlichen Konfigurationen bereitzustellen.
8. Azure-Blaupause:
    1. Erstellen Sie eine neue Azure-Blaupause namens `protected-data`.
    2. Fügen Sie der Blaupause die Firewall und die Azure-Tresorvorlagen hinzu.
    3. Fügen Sie die neuen Richtlinien für Abonnements geschützter Daten hinzu.
    4. Veröffentlichen Sie die Blaupause für alle Verwaltungsgruppen, die zum Hosten unternehmenskritischer Anwendungen verwendet werden.
    5. Wenden Sie die neue Blaupause zusammen mit vorhandenen Blaupausen auf die betroffenen Abonnements an.

## <a name="conclusion"></a>Zusammenfassung

Durch diese zusätzlichen Prozesse und Änderungen am Governance-MVP lassen sich viele Risiken im Zusammenhang mit der Ressourcengovernance umgehen. In Kombination fügen sie die Steuerelemente für Wiederherstellung, Dimensionierung und Überwachung hinzu, die einen cloudfähigen Betrieb ermöglichen.

## <a name="next-steps"></a>Nächste Schritte

Mit der Fortsetzung der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an die Cloudgovernance. Für das fiktive Unternehmen in diesem Leitfaden wird der nächste Trigger ausgelöst, wenn die Größe der Bereitstellung 100 Ressourcen in der Cloud oder monatliche Ausgaben von 1.000 US-Dollar übersteigt. An diesem Punkt fügt das Cloudgovernanceteam Cost Management-Steuerelemente hinzu.

> [!div class="nextstepaction"]
> [Verbessern des Kostenmanagements](./cost-management-improvement.md)
