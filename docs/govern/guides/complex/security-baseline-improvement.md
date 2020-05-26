---
title: 'Governance in komplexen Unternehmen: Verbessern der Disziplin „Sicherheitsbaseline“'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Sie Sicherheitskontrollen hinzufügen, die das Verschieben geschützter Daten in die Cloud unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 07b9eb1ebcb464abda6f2c2cf276cb91596cea1a
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400497"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-security-baseline-discipline"></a>Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Sicherheitsbaseline“

In diesem Artikel wird die Geschichte fortgeführt. Es werden Sicherheitskontrollen hinzugefügt, die das Verschieben geschützter Daten in die Cloud unterstützen.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Der CIO hat mehrere Monate lang mit Kollegen und der Rechtsabteilung des Unternehmens zusammengearbeitet. Ein Unternehmensberater mit Fachkenntnissen im Bereich Cybersicherheit wurde engagiert, um die bestehenden Teams für IT-Sicherheit und IT-Governance beim Entwurf einer neuen Richtlinie für geschützte Daten zu unterstützen. Die Gruppe konnte die Unterstützung des Vorstands dafür gewinnen, die vorhandene Richtlinie zu ersetzen, sodass vertrauliche personenbezogene Informationen und Finanzdaten von genehmigten Cloudanbietern gehostet werden dürfen. Dafür mussten eine Reihe von Sicherheitsanforderungen und ein Governanceprozess installiert werden, um die Einhaltung dieser Richtlinien zu verifizieren und zu dokumentieren.

In den letzten zwölf Monaten haben die Cloudeinführungsteams die meisten der 5.000 Ressourcen aus den beiden Rechenzentren außer Betrieb gesetzt. Die 350 inkompatiblen Ressourcen wurden in ein anderes Rechenzentrum verschoben. Es verbleiben nur die 1.250 virtuellen Computer, die geschützte Daten enthalten.

### <a name="changes-in-the-cloud-governance-team"></a>Änderungen des Cloudgovernanceteams

Das Cloudgovernanceteam ändert sich im Laufe der Geschichte weiter. Die beiden Gründungsmitglieder des Teams gehören jetzt zu den angesehensten Cloudarchitekten im Unternehmen. Die Sammlung von Konfigurationsskripts wächst, während neue Teams innovative neue Bereitstellungen in Angriff nehmen. Auch das Cloudgovernanceteam ist gewachsen. Bis vor Kurzem haben die Mitglieder des IT-Betriebsteams an den Aktivitäten des Cloudgovernanceteams teilgenommen, um sich auf Cloudvorgänge vorzubereiten. Die Cloudarchitekten, die diese Community gefördert haben, werden sowohl als Cloudwächter als auch als Cloudbeschleuniger betrachtet.

Der Unterschied ist zwar subtil, aber beim Erstellen einer governancebezogenen IT-Kultur von entscheidender Bedeutung. Ein Cloudverwaltungsberechtigter räumt das Chaos auf, das von innovativen Cloudarchitekten hinterlassen wird, und zwischen den beiden Rollen gibt es natürliche Reibung und gegensätzliche Ziele. Ein Cloudwächter hält die Cloud sicher, damit andere Cloudarchitekten mit weniger Chaos schneller vorankommen. Ein Cloudbeschleuniger erfüllt beide Funktionen, ist jedoch auch an der Erstellung von Vorlagen zur Beschleunigung von Bereitstellung und Einführung beteiligt. Damit ist er sowohl Innovationsbeschleuniger als auch Verteidiger der fünf Disziplinen der Cloud-Governance.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Geschichte hatte das Unternehmen damit begonnen, zwei Rechenzentren außer Betrieb zu nehmen. Zu diesem laufenden Prozess gehört die Migration einiger Anwendungen mit Legacyauthentifizierungsanforderungen. Dazu waren inkrementelle Verbesserungen der Identitätsbaseline erforderlich, die im [vorherigen Artikel](./identity-baseline-improvement.md) beschrieben sind.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Tausende von IT- und Unternehmensressourcen werden in der Cloud bereitgestellt.
- Das Team für die Anwendungsentwicklung hat eine CI/CD-Pipeline (Continuous Integration/Continuous Deployment) implementiert, um eine native Cloudanwendung mit einer verbesserten Benutzeroberfläche bereitzustellen. Diese Anwendung interagiert noch nicht mit geschützten Daten und ist daher nicht für die Produktion bereit.
- Das Business Intelligence-Team innerhalb der IT-Abteilung stellt aktiv Daten aus Logistik, Inventur und Drittanbieterdaten in der Cloud zusammen. Diese Daten werden verwendet, um neue Vorhersagen zu treffen, die Geschäftsprozesse beeinflussen könnten. Diese Vorhersagen und Erkenntnisse sind jedoch erst dann umsetzbar, wenn Kunden- und Finanzdaten in die Datenplattform integriert werden können.
- Das IT-Team setzt zurzeit die Pläne des CIO und CFO zur Außerbetriebnahme zweier Rechenzentren um. Fast 3.500 Ressourcen in den beiden Rechenzentren wurden außer Betrieb genommen oder migriert.
- Die Richtlinien im Hinblick auf vertrauliche personenbezogene Informationen und Finanzdaten wurden modernisiert. Allerdings sind die neuen Unternehmensrichtlinien abhängig von der Implementierung der entsprechenden Sicherheits- und Governancerichtlinien. Teams können noch nicht weiterarbeiten.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

- Frühe Experimente der Teams für Anwendungsentwicklung und Business Intelligence haben potenzielle Verbesserungen für die Kundenumgebung und datengestützte Entscheidungen aufgezeigt. Beide Teams möchten die Einführung der Cloud in den nächsten 18 Monaten erweitern, indem Sie diese Lösungen in der Produktionsumgebung bereitstellen.
- Die IT-Abteilung hat eine geschäftliche Rechtfertigung für die Migration von fünf weiteren Rechenzentren zu Azure entwickelt. Dadurch werden die IT-Kosten weiter gesenkt, und eine höhere geschäftliche Flexibilität wird ermöglicht. Auch wenn diese Rechenzentren kleiner sind, sollen sich die Kosteneinsparungen durch die Außerbetriebnahme dieser Rechenzentren insgesamt verdoppeln.
- Von den Budgets für Kapital- und Betriebsaufwand wurde die Implementierung der erforderlichen Richtlinien, Tools und Prozesse für Sicherheit und Governance genehmigt. Die erwarteten Kosteneinsparungen durch die Außerbetriebnahme von Rechenzentren reichen zur Finanzierung dieser neuen Initiative deutlich aus. Die IT-Abteilung und die Unternehmensführung sind zuversichtlich, dass diese Investition die Rendite in anderen Bereichen beschleunigen wird. Das Cloudgovernance-Basisteam ist mittlerweile ein anerkanntes Team mit engagierten Führungskräften und Mitarbeitern.
- Die Cloudeinführungsteams, das Cloudgovernanceteam,das Team für IT-Sicherheit und das IT-Governanceteam implementieren zusammen Sicherheits- und Governanceanforderungen, um den Cloudeinführungsteams die Migration geschützter Daten in die Cloud zu ermöglichen.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Verletzung des Datenschutzes:** Bei Einführung einer neuen Datenplattform gibt es eine inhärente Zunahme der Haftung im Zusammenhang mit Datenpannen. Das technische Personal zur Einführung von Cloudtechnologien ist zunehmend dafür verantwortlich, dass Lösungen implementiert werden, die dieses Risiko senken können. Eine robuste Sicherheits- und Governancestrategie muss implementiert werden, um sicherzustellen, dass dieses technische Personal dieser Verantwortung nachkommt.

Dieses Geschäftsrisiko lässt sich auf eine Reihe von technischen Risiken ausweiten:

1. Unternehmenskritische Apps oder geschützten Daten werden möglicherweise unbeabsichtigt bereitgestellt.
2. Geschützte Daten könnten aufgrund falscher Verschlüsselungsentscheidungen im Speicher verfügbar gemacht werden.
3. Nicht autorisierte Benutzer können möglicherweise auf geschützte Daten zugreifen.
4. Ein Eindringen von außerhalb kann den Zugriff auf geschützte Daten ermöglichen.
5. Ein Eindringen von außerhalb oder Denial-of-Service-Angriffe können zu einer Unterbrechung des Geschäftsbetriebs führen.
6. Organisatorische Änderungen oder Personalwechsel können den unbefugten Zugriff auf geschützte Daten ermöglichen.
7. Neue Exploits schaffen Möglichkeiten für Eindringlinge oder für unbefugten Zugriff.
8. Inkonsistente Bereitstellungsprozesse können Sicherheitslücken verursachen, die zu Datenverlusten oder Unterbrechungen führen können.
9. Konfigurationsabweichungen oder fehlende Patches können unbeabsichtigte Sicherheitslücken zur Folge haben, die zu Datenverlusten oder Unterbrechungen führen können.
10. Verschiedenartige Edge-Geräte können die Kosten für den Netzwerkbetrieb erhöhen.
11. Verschiedenartige Gerätekonfigurationen können zu Fehlern in der Konfiguration und zur Gefährdung der Sicherheit führen.
12. Das Team für Cybersicherheit besteht darauf, dass durch das Generieren von Verschlüsselungsschlüsseln auf der Plattform eines einzigen Cloudanbieters das Risiko einer Anbieterabhängigkeit besteht. Auch wenn diese Sorge unbegründet ist, wurde dies vom Team vorerst akzeptiert.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung. Die Liste wirkt lang, aber die Einführung dieser Richtlinien ist möglicherweise einfacher, als es den Anschein hat.

1. Alle bereitgestellten Ressourcen müssen nach Wichtigkeit und Datenklassifizierung kategorisiert werden. Vor der Bereitstellung in der Cloud müssen die Klassifizierungen durch das Cloudgovernanceteam und die Anwendung überprüft werden.
2. Anwendungen, die geschützte Daten speichern oder darauf zugreifen, müssen anders verwaltet werden als Anwendungen, auf die das nicht zutrifft. Zumindest müssen sie segmentiert werden, um einen unbeabsichtigten Zugriff auf geschützte Daten zu vermeiden.
3. Alle geschützten Daten müssen im Ruhezustand verschlüsselt sein.
4. Erhöhte Berechtigungen in einem Segment mit geschützten Daten müssen eine Ausnahme bleiben. Solche Ausnahmen werden vom Cloudgovernanceteam erfasst und regelmäßig überwacht.
5. Netzwerksubnetze mit geschützten Daten müssen von allen anderen Subnetzen isoliert werden. Der Netzwerkdatenverkehr zwischen Subnetzen mit geschützten Daten wird regelmäßig überwacht.
6. Kein Subnetz mit geschützten Daten ist direkt über das öffentliche Internet oder datencenterübergreifend zugänglich. Der Zugriff auf diese Subnetze muss über zwischengeschaltete Subnetze geroutet werden. Der gesamte Zugriff auf diese Subnetze muss über eine Firewalllösung erfolgen, die Funktionen zur Paketüberprüfung und Sperrfunktionen durchführen kann.
7. Die Anforderungen an die Netzwerkkonfiguration, die vom Sicherheitsverwaltungsteam definiert wurden, müssen mit Governancetools überwacht und durchgesetzt werden.
8. Governancetools müssen die VM-Bereitstellung auf genehmigte Images begrenzen.
9. Nach Möglichkeit muss die Knotenkonfigurationsverwaltung Richtlinienanforderungen auf die Konfiguration aller Gastbetriebssysteme anwenden. Die Knotenkonfigurationsverwaltung muss die vorhandene Investition in das Gruppenrichtlinienobjekt (Group Policy Object, GPO) für die Ressourcenkonfiguration berücksichtigen.
10. Governancetools überwachen die Aktivierung automatischer Updates für alle bereitgestellten Assets. Nach Möglichkeit werden automatische Updates durchgesetzt. Wenn sie nicht durch Tools erzwungen werden, müssen Verstöße auf Knotenebene von Betriebsmanagementteams überprüft und in Übereinstimmung mit den Betriebsrichtlinien beseitigt werden. Ressourcen, die nicht automatisch aktualisiert werden, müssen in Prozesse einbezogen werden, die IT Operations unterstehen.
11. Für die Erstellung neuer Abonnements oder Verwaltungsgruppen für unternehmenskritische Anwendungen oder geschützte Daten ist eine Überprüfung durch das Cloudgovernanceteam erforderlich, um eine angemessene Blaupausenzuweisung sicherzustellen.
12. Das Zugriffsmodell der geringsten Rechte wird auf alle Abonnements angewendet, die unternehmenskritische Anwendungen oder geschützte Daten enthalten.
13. Der Cloudanbieter muss Verschlüsselungsschlüssel integrieren können, die von der vorhandenen lokalen Lösung verwaltet werden.
14. Der Cloudanbieter muss die vorhandene Lösung für Edge-Geräte und alle erforderlichen Konfigurationen zum Schutz öffentlich zugänglicher Netzwerkgrenzen unterstützen können.
15. Der Cloudanbieter muss eine freigegebene Verbindung mit dem globalen WAN unterstützen können, bei der die Datenübertragung über die vorhandene Edge-Gerätelösung geroutet wird.
16. Trends und Exploits, die Auswirkungen auf Cloudbereitstellungen haben könnten, müssen vom Sicherheitsteam regelmäßig überprüft werden, damit Updates für in der Cloud verwendete Sicherheitsbaselinetools bereitgestellt werden können.
17. Bereitstellungstools müssen vom Cloudgovernanceteam genehmigt werden, um eine kontinuierliche Governance für bereitgestellte Ressourcen sicherzustellen.
18. Bereitstellungsskripts müssen in einem zentralen Repository aufbewahrt werden, das für das Cloudgovernanceteam zur regelmäßigen Überprüfung und Überwachung zugänglich ist.
19. Governanceprozesse müssen Überwachungen zum Bereitstellungszeitpunkt und nachfolgend in regelmäßigen Zyklen umfassen, um für alle Ressourcen Konsistenz zu gewährleisten.
20. Die Bereitstellung von Anwendungen, für die eine Kundenauthentifizierung erforderlich ist, erfordert einen genehmigten Identitätsanbieter, der mit dem primären Identitätsanbieter für interne Benutzer kompatibel ist.
21. Cloudgovernanceprozesse müssen vierteljährliche Überprüfungen durch Identitätsbaselineteams umfassen, um böswillige Akteure oder Nutzungsmuster identifizieren zu können, die durch die Cloudressourcenkonfiguration verhindert werden sollten.

## <a name="incremental-improvement-of-the-best-practices"></a>Inkrementelle Verbesserungen der bewährten Methoden

In diesem Abschnitt wird der Governance-MVP-Entwurf so geändert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

Die neuen bewährten Methoden lassen sich in zwei Kategorien unterteilen: Unternehmens-IT (Hub) und Cloudeinführung (Spoke).

**Einrichten eines Hub-and-Spoke-Abonnements für die Unternehmens-IT zum Zentralisieren der Sicherheitsbaseline:** In dieser bewährten Methode wird die vorhandene Governancekapazität von einer [Hub-and-Spoke-Topologie mit Shared Services](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) umschlossen, mit einigen wichtigen Ergänzungen des Cloudgovernanceteams.

1. Azure DevOps-Repository. Erstellen Sie in Azure DevOps ein Repository zur Speicherung und Versionsverwaltung für alle relevanten Azure Resource Manager-Vorlagen und Skriptkonfigurationen.
2. Hub-and-Spoke-Vorlage:
    1. Die Anleitung in der [Hub-and-Spoke-Topologie mit Shared Services](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) kann zum Generieren von Resource Manager-Vorlagen für die Ressourcen verwendet werden, die in einem Unternehmens-IT-Hub erforderlich sind.
    2. Mit diesen Vorlagen kann diese Struktur im Rahmen einer zentralen Governancestrategie wiederholbar gemacht werden.
    3. Zusätzlich zur aktuellen Referenzarchitektur wird empfohlen, eine NSG-Vorlage zu erstellen, die alle Anforderungen zu Portsperren oder Whitelists für das virtuelle Netzwerk erfasst, das die Firewall hosten soll. Diese Netzwerksicherheitsgruppe unterscheidet sich von früheren Gruppen, da sie die erste Netzwerksicherheitsgruppe ist, die öffentlichen Datenverkehr in ein virtuelles Netzwerk zulässt.
3. Erstellen von Azure-Richtlinien. Erstellen Sie eine Richtlinie namens `hub NSG enforcement`, um die Konfiguration der Netzwerksicherheitsgruppe zu erzwingen, die einem in diesem Abonnement erstellten virtuellen Netzwerk zugewiesen ist. Wenden Sie die integrierten Richtlinien für die Gastkonfiguration wie folgt an:
    1. Überwachen Sie die Verwendung sicherer Kommunikationsprotokolle auf Windows-Webservern.
    2. Überwachen Sie die korrekte Festlegung der Kennwortsicherheitseinstellungen auf Linux- und Windows-Computern.
4. Erstellen Sie die Unternehmens-IT-Blaupause.
    1. Erstellen Sie eine Azure-Blaupause namens `corporate-it-subscription`.
    2. Fügen Sie die Hub-and-Spoke-Vorlagen und die `hub NSG enforcement`-Richtlinie hinzu.
5. Erweitern der anfänglichen Verwaltungsgruppenhierarchie.
    1. Für jede Verwaltungsgruppe, die Unterstützung für geschützte Daten angefordert hat, bietet die Blaupause `corporate-it-subscription-blueprint` eine beschleunigte Hublösung.
    2. Da Verwaltungsgruppen in diesem fiktiven Beispiel neben einer Geschäftseinheitshierarchie auch eine regionale Hierarchie umfassen, wird diese Blaupause in jeder Region bereitgestellt.
    3. Erstellen Sie für jede Region in der Verwaltungsgruppenhierarchie ein Abonnement namens `corporate IT subscription`.
    4. Wenden Sie die Blaupause `corporate-it-subscription-blueprint` auf die einzelnen regionalen Instanzen an.
    5. Dadurch wird für jede Geschäftseinheit in jeder Region ein Hub eingerichtet. Hinweis: Weitere Kosteneinsparungen könnten durch die gemeinsame Nutzung von Hubs durch die Geschäftseinheiten in jeder Region erzielt werden.
6. Integrieren von Gruppenrichtlinienobjekten (GPO) über DSC (Desired State Configuration):
    1. Konvertieren eines GPO in DSC: Das [Projekt zur Microsoft-Baselineverwaltung](https://github.com/microsoft/baselinemanagement) auf GitHub kann diese Aufgabe beschleunigen. Stellen Sie sicher, dass DSC im Repository parallel zu den Resource Manager-Vorlagen gespeichert wird.
    2. Stellen Sie Azure Automation State Configuration für alle Instanzen des Unternehmens-IT-Abonnements bereit. Mit Azure Automation kann DSC auf virtuelle Computer angewendet werden, die in unterstützten Abonnements innerhalb der Verwaltungsgruppe bereitgestellt werden.
    3. In der aktuellen Roadmap ist die Aktivierung benutzerdefinierter Gastkonfigurationsrichtlinien als Ziel festgelegt. Wenn dieses Feature veröffentlicht wird, ist die Verwendung von Azure Automation in dieser bewährten Methode nicht mehr erforderlich.

**Anwenden zusätzlicher Governance auf ein Cloudeinführungsabonnement (Spoke):** Aufbauend auf dem `corporate IT subscription` können geringfügige Änderungen am Governance-MVP, die auf die einzelnen Abonnements zur Unterstützung von Anwendungsarchetypen angewendet werden, für eine schnelle Verbesserung sorgen.

In früheren iterativen Änderungen der bewährten Methoden haben wir Netzwerksicherheitsgruppen so definiert, dass sie den öffentlichen Verkehr blockiert und den internen Verkehr auf einer Whitelist vermerkt haben. Darüber hinaus wurden durch die Azure-Blaupause vorübergehend DMZ- und Active Directory-Funktionen erstellt. Im Rahmen dieser Iteration werden wir diese Ressourcen ein wenig anpassen und so eine neue Version der Azure-Blaupause erstellen.

1. Vorlage zum Netzwerkpeering. Mit dieser Vorlage wird das virtuelle Netzwerk in den einzelnen Abonnements mit dem virtuellen Hub-Netzwerk im Unternehmens-IT-Abonnement gekoppelt.
    1. Die Referenzarchitektur aus dem vorherigen Abschnitt ([Hub-and-Spoke-Topologie mit Shared Services](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)) generierte eine Resource Manager-Vorlage für das Aktivieren des Peerings virtueller Netzwerke.
    2. Diese Vorlage kann als Anleitung zum Ändern der DMZ-Vorlage aus der vorherigen Governanceiteration verwendet werden.
    3. Jetzt fügen wir dem virtuellen DMZ-Netzwerk, das zuvor per VPN mit dem lokalen Edge-Gerät verbunden war, das Peering virtueller Netzwerke hinzu.
    4. Sie sollten das VPN außerdem aus dieser Vorlage entfernen und sicherstellen, dass kein Datenverkehr direkt an das lokale Rechenzentrum weitergeleitet wird, ohne das Unternehmens-IT-Abonnement und die Firewalllösung zu durchlaufen. Dieses VPN kann auch als Failoververbindung im Fall eines ExpressRoute-Verbindungsausfalls festgelegt werden.
    5. Azure Automation erfordert zusätzliche [Netzwerkkonfiguration](https://docs.microsoft.com/azure/automation/automation-dsc-overview#network-planning), damit DSC auf gehostete VMs angewendet werden kann.
2. Ändern Sie die Netzwerksicherheitsgruppe. Blockieren Sie den gesamten öffentlichen **und** den direkten lokalen Datenverkehr in der Netzwerksicherheitsgruppe. Der einzige eingehende Datenverkehr sollte über den virtuellen Netzwerkpeer im Unternehmens-IT-Abonnement erfolgen.
    1. In der vorherigen Iteration wurde eine Netzwerksicherheitsgruppe erstellt, die den gesamten öffentlichen Datenverkehr blockiert und den gesamten internen Datenverkehr über eine Whitelist zulässt. Jetzt möchten wir diese Netzwerksicherheitsgruppe etwas verschieben.
    2. In der neuen Konfiguration der Netzwerksicherheitsgruppe wird der gesamte öffentliche Datenverkehr sowie der gesamte Datenverkehr aus dem lokalen Datencenter blockiert.
    3. Der einzige in dieses virtuelle Netzwerk eingehende Datenverkehr darf nur von dem virtuellen Netzwerk auf der anderen Seite des virtuellen Netzwerkpeers stammen.
3. Implementierung von Azure Security Center:
    1. Konfigurieren Sie Azure Security Center für jede Verwaltungsgruppe, die Klassifizierungen geschützter Daten enthält.
    2. Legen Sie automatische Bereitstellung standardmäßig auf „Aktiviert“ fest, um Patchingkompatibilität zu gewährleisten.
    3. Richten Sie Sicherheitskonfigurationen von Betriebssystemen ein. Das IT-Sicherheitsteam definiert die Konfiguration.
    4. Unterstützen Sie das IT-Sicherheitsteam bei der anfänglichen Verwendung von Azure Security Center. Übertragen Sie die Verwendung von Security Center an das IT-Sicherheitsteam, aber behalten Sie den Zugriff, um die Governance stetig zu verbessern.
    5. Erstellen Sie eine Resource Manager-Vorlage, die die erforderlichen Änderungen für die Azure Security Center-Konfiguration in einem Abonnement widerspiegelt.
4. Aktualisieren Sie Azure Policy für alle Abonnements.
    1. Überprüfen und erzwingen Sie die Wichtigkeits- und Datenklassifizierung für alle Verwaltungsgruppen und Abonnements, um Abonnements mit Klassifizierungen geschützter Daten zu identifizieren.
    2. Überwachen und erzwingen Sie die ausschließliche Verwendung genehmigter Betriebssystemimages.
    3. Überwachen und erzwingen Sie Gastkonfigurationen basierend auf den Sicherheitsanforderungen für die einzelnen Knoten.
5. Aktualisieren Sie Azure Policy für alle Abonnements, die Klassifizierungen geschützter Daten enthalten.
    1. Überwachen und erzwingen Sie die ausschließliche Verwendung von Standardrollen.
    2. Überwachen und erzwingen Sie die Anwendung der Verschlüsselung für alle Speicherkonten und Dateien, die sich auf den einzelnen Knoten im Ruhezustand befinden.
    3. Überwachen und erzwingen Sie die Anwendung der neuen Version der DMZ-Netzwerksicherheitsgruppe.
    4. Überwachen und erzwingen Sie die Verwendung eines genehmigten Netzwerksubnetzes und virtuellen Netzwerks pro Netzwerkschnittstelle.
    5. Überwachen und erzwingen Sie die Einschränkung benutzerdefinierter Routingtabellen.
6. Azure-Blaupause:
    1. Erstellen Sie eine Azure-Blaupause namens `protected-data`.
    2. Fügen Sie der Blaupause die Vorlagen für den virtuellen Netzwerkpeer, für die Netzwerksicherheitsgruppe und die Azure Security Center-Vorlagen hinzu.
    3. Stellen Sie sicher, dass die Vorlage für Active Directory aus der vorherigen Iteration **nicht** in der Blaupause enthalten ist. Alle Abhängigkeiten von Active Directory werden vom Unternehmens-IT-Abonnement bereitgestellt.
    4. Beenden Sie alle vorhandenen Active Directory-VMs, die in der vorherigen Iteration bereitgestellt wurden.
    5. Fügen Sie die neuen Richtlinien für Abonnements geschützter Daten hinzu.
    6. Veröffentlichen Sie die Blaupause für alle Verwaltungsgruppen, die zum Hosten geschützter Daten verwendet werden.
    7. Wenden Sie die neue Blaupause zusammen mit vorhandenen Blaupausen auf die betroffenen Abonnements an.

## <a name="conclusion"></a>Zusammenfassung

Durch das Hinzufügen dieser Prozesse und Änderungen zum Governance-MVP lassen sich viele Risiken im Zusammenhang mit der Sicherheitsgovernance verringern. Zusammen stellen Sie die Tools zur Überwachung von Netzwerk, Identität und Sicherheit bereit, die zum Schutz von Daten erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Mit der Fortsetzung der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an Cloudgovernance. Für das fiktive Unternehmen in diesem Leitfaden besteht der nächste Schritt darin, unternehmenskritische Workloads zu unterstützen. An dieser Stelle werden Steuerelemente für die Ressourcenkonsistenz benötigt.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Ressourcenkonsistenz“](./resource-consistency-improvement.md)
