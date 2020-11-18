---
title: 'Governance für Standardunternehmen: Verbessern der Disziplin „Sicherheitsbaseline“'
description: Verwenden Sie das Azure Cloud Adoption Framework, um zu erfahren, wie Sie Sicherheitskontrollen hinzufügen, die das Verschieben geschützter Daten in die Cloud unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: eb9b071490580123a7358d2215907ab4c106d7a3
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94712807"
---
# <a name="standard-enterprise-governance-guide-improve-the-security-baseline-discipline"></a>Governanceleitfaden für Standardunternehmen: Verbessern der Disziplin „Sicherheitsbaseline“

In diesem Artikel wird die [Geschichte der Governancestrategie](./narrative.md) fortgeführt. Es werden Sicherheitskontrollen hinzugefügt, die das Verschieben geschützter Daten in die Cloud unterstützen.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

IT-Abteilung und Unternehmensführung sind mit den Ergebnissen erster Experimente der IT-, Anwendungsentwicklung- und BI-Teams zufrieden. Um aus diesen Experimenten konkrete Geschäftswerte zu gewinnen, müssen diese Teams in die Lage versetzt werden, geschützte Daten in Lösungen zu integrieren. Diese Integration führt zu Änderungen an der Unternehmensrichtlinie. Sie erfordert aber auch eine Weiterentwicklung der Cloud Governance-Implementierungen, damit geschützte Daten in die Cloud verschoben werden können.

### <a name="changes-to-the-cloud-governance-team"></a>Änderungen des Cloudgovernanceteams

Angesichts der Auswirkungen der sich verändernden Darstellung und der bisher geleisteten Unterstützung wird das Cloudgovernanceteam nun anders beurteilt. Die beiden Systemadministratoren, die das Team gegründet haben, gelten heute als erfahrene Cloudarchitekten. Mit der Zeit werden sie weniger als Cloudverwalter, sondern eher als Cloudwächter wahrgenommen.

Diese Unterscheidung mag spitzfindig erscheinen, ist bei der Entwicklung einer governancebezogenen IT-Kultur aber von großer Bedeutung. Ein Cloudverwalter bereinigt das Chaos, das innovative Cloudarchitekten hinterlassen haben. Es ist ganz natürlich, dass es zwischen diesen beiden Rollen gewisse Spannungen gibt und dass sie gegensätzliche Ziele verfolgen. Auf der anderen Seite trägt ein Cloudwächter zur Sicherheit der Cloud bei, sodass andere Cloudarchitekten schneller und strukturierter arbeiten können. Darüber hinaus arbeiten Cloudwächter an der Erstellung von Vorlagen zur Beschleunigung der Bereitstellung und Einführung. Sie setzen sich also nicht nur für die Bewahrung der fünf Disziplinen der Cloud-Governance ein, sondern treiben auch Innovationen voran.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

Zu Beginn dieser Geschichte arbeiteten die Anwendungsentwicklungsteams noch mit Entwicklungs-/Testkapazität, und das BI-Team befand sich noch in der Experimentierphase. Von der IT-Abteilung wurden zwei gehostete Infrastrukturumgebungen („`Prod`“ und „`DR`“) betrieben.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Das Anwendungsentwicklungsteam hat eine CI/CD-Pipeline implementiert, um eine cloudnative Anwendung mit einer verbesserten Benutzeroberfläche bereitzustellen. Diese Anwendung interagiert noch nicht mit geschützten Daten und ist daher nicht für die Produktion bereit.
- Das Business Intelligence-Team innerhalb der IT-Abteilung stellt aktiv Daten aus Logistik, Inventar und Drittanbieterquellen in der Cloud zusammen. Diese Daten werden verwendet, um neue Vorhersagen zu treffen, die Geschäftsprozesse beeinflussen können. Diese Vorhersagen und Erkenntnisse sind erst dann umsetzbar, wenn Kunden- und Finanzdaten in die Datenplattform integriert werden können.
- Das IT-Team setzt zurzeit die Pläne des CIO und CFO zur Außerbetriebnahme des DR-Rechenzentrums um. Mehr als 1.000 der 2.000 Ressourcen im DR-Datencenter wurden außer Betrieb genommen oder migriert.
- Die lose definierten Richtlinien für personenbezogene Informationen und Finanzdaten wurden modernisiert. Die neuen Unternehmensrichtlinien sind von der Implementierung der entsprechenden Sicherheits- und Governancerichtlinien abhängig. Teams können noch nicht weiterarbeiten.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Frühe Experimente der Teams für Anwendungsentwicklung und Business Intelligence haben potenzielle Verbesserungen für die Kundenumgebung und datengestützte Entscheidungen aufgezeigt. Beide Teams möchten die Einführung der Cloud in den nächsten 18 Monaten erweitern, indem Sie diese Lösungen in der Produktionsumgebung bereitstellen.

In den verbleibenden sechs Monaten wird das Cloudgovernanceteam Sicherheits- und Governanceanforderungen umsetzen, damit die Cloudeinführungsteams die geschützten Daten in diesen Datencentern migrieren können.

Die Änderungen des aktuellen und zukünftigen Status bergen neue Risiken, die neue Richtlinienanweisungen erfordern.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Verletzung des Datenschutzes:** Die Einführung einer neuen Datenplattform geht mit einer inhärenten Zunahme von Pflichten im Zusammenhang mit potenziellen Datenpannen einher. Techniker, die Cloudtechnologien einführen, müssen sich verstärkt um die Implementierung von Lösungen kümmern, die dieses Risiko senken können. Eine robuste Sicherheits- und Governancestrategie muss implementiert werden, um sicherzustellen, dass dieses technische Personal dieser Verantwortung nachkommt.

Dieses Unternehmensrisiko lässt sich auf einige technische Risiken erweitern:

- Unternehmenskritische Anwendungen oder geschützten Daten werden möglicherweise unbeabsichtigt bereitgestellt.
- Geschützte Daten können ggf. aufgrund von falschen Verschlüsselungsentscheidungen im Speicher offengelegt werden.
- Nicht autorisierte Benutzer können möglicherweise auf geschützte Daten zugreifen.
- Ein Eindringen von außerhalb kann den Zugriff auf geschützte Daten ermöglichen.
- Ein Eindringen von außerhalb oder Denial-of-Service-Angriffe können zu einer Unterbrechung des Geschäftsbetriebs führen.
- Organisatorische Änderungen oder Personalwechsel können den unbefugten Zugriff auf geschützte Daten ermöglichen.
- Neue Exploits können neue Angriffs- oder Zugriffsmöglichkeiten schaffen.
- Inkonsistente Bereitstellungsprozesse können Sicherheitslücken herbeiführen, die zu Datenverlusten oder Unterbrechungen führen können.
- Konfigurationsabweichungen oder fehlende Patches können unbeabsichtigte Sicherheitslücken zur Folge haben, die zu Datenverlusten oder Unterbrechungen führen können.

**Datenverlust:** Die neue Plattform birgt auch ein inhärentes Datenverlustrisiko. Bei der Sicherheits- und Governancestrategie müssen die folgenden Szenarien berücksichtigt werden, in denen Daten verloren gehen können:

- Eine unternehmenskritische Ressource geht verloren oder wird gelöscht.
- Eine unternehmenskritische Ressource ist vorhanden, die Daten gehen jedoch durch versehentliches Löschen verloren.
- Eine unternehmenskritische Ressource ist vorhanden, die Daten gehen jedoch durch einen böswilligen Administrator verloren.

## <a name="incremental-improvement-of-policy-statements"></a>Inkrementelle Verbesserung von Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung. Die Liste wirkt lang, aber die Einführung dieser Richtlinien ist möglicherweise einfacher, als es den Anschein hat.

- Alle bereitgestellten Ressourcen müssen nach Wichtigkeit und Datenklassifizierung kategorisiert werden. Diese Klassifizierungen müssen vor der Bereitstellung in der Cloud durch das Cloudgovernanceteam und die Besitzer der Anwendung überprüft werden.
- Anwendungen, die geschützte Daten speichern oder darauf zugreifen, müssen anders verwaltet werden als Anwendungen, auf die das nicht zutrifft. Zumindest müssen sie segmentiert werden, um einen unbeabsichtigten Zugriff auf geschützte Daten zu vermeiden.
- Alle geschützten Daten müssen im Ruhezustand verschlüsselt sein. Diese Verschlüsselung wird standardmäßig für alle Azure Storage-Konten verwendet. Möglicherweise sind jedoch weitere Verschlüsselungsstrategien erforderlich, einschließlich der Verschlüsselung der Daten im Speicherkonto, der Verschlüsselung virtueller Computer und der Verschlüsselung auf Datenbankebene bei Verwendung von SQL auf einem virtuellen Computer (TDE und Spaltenverschlüsselung).
- Unternehmenskritische Daten können versehentlich gelöscht werden. Sie benötigen eine Datensicherungsstrategie, die dieses Risiko abdeckt und die Wiederherstellung der Daten vor dem Löschpunkt ermöglicht. Ein böswilliger Administrator kann die unternehmenskritischen Daten und auch deren Sicherungen löschen. Aus diesem Grund sollte für Sicherungsdaten eine vorläufige Löschung verwendet werden, die wieder rückgängig gemacht werden kann. Azure Backup kann Sie bei diesen beiden Szenarien unterstützen.
- Erhöhte Berechtigungen in einem Segment mit geschützten Daten sollten nur in Ausnahmefällen gewährt werden. Solche Ausnahmen werden vom Cloudgovernanceteam erfasst und regelmäßig überwacht.
- Netzwerksubnetze mit geschützten Daten müssen von anderen Subnetzen isoliert werden. Der Netzwerkdatenverkehr zwischen Subnetzen mit geschützten Daten wird regelmäßig überwacht.
- Subnetze mit geschützten Daten sollten nicht direkt über das öffentliche Internet oder über Rechenzentren hinweg zugänglich sein. Der Zugriff auf diese Subnetze muss über zwischengeschaltete Subnetze geroutet werden. Der gesamte Zugriff auf diese Subnetze muss über eine Firewalllösung erfolgen, die Funktionen zur Paketüberprüfung und Sperrfunktionen durchführen kann.
- Die Anforderungen an die Netzwerkkonfiguration, die vom Sicherheitsverwaltungsteam definiert wurden, müssen mit Governancetools überwacht und durchgesetzt werden.
- Governancetools müssen die VM-Bereitstellung auf genehmigte Images beschränken.
- Der Governanceprozess muss überprüfen, ob für unternehmenskritische Anwendungen und geschützte Daten die Sicherung, Wiederherstellung und Einhaltung von SLAs ordnungsgemäß implementiert sind.
- Nach Möglichkeit muss die Knotenkonfigurationsverwaltung Richtlinienanforderungen auf die Konfiguration aller Gastbetriebssysteme anwenden.
- Governancetools müssen durchsetzen, dass automatische Updates für alle bereitgestellten Ressourcen aktiviert sind. Verstöße müssen von Betriebsmanagementteams überprüft und in Übereinstimmung mit den Betriebsrichtlinien beseitigt werden. Ressourcen, die nicht automatisch aktualisiert werden, müssen in IT-Betriebsprozesse einbezogen werden.
- Für die Erstellung neuer Abonnements oder Verwaltungsgruppen für unternehmenskritische Anwendungen oder geschützte Daten ist eine Überprüfung durch das Cloudgovernanceteam erforderlich, um sicherzustellen, dass die richtige Blaupause zugewiesen wird.
- Das Zugriffsmodell der geringsten Rechte wird auf alle Verwaltungsgruppen oder Abonnements angewendet, die unternehmenskritische Anwendungen oder geschützte Daten enthalten.
- Trends und Exploits, die mögliche Auswirkungen auf Cloudbereitstellungen haben, müssen vom Sicherheitsteam regelmäßig überprüft werden, damit Updates für in der Cloud verwendete Sicherheitsverwaltungstools bereitgestellt werden.
- Bereitstellungstools müssen vom Cloudgovernanceteam genehmigt werden, um eine kontinuierliche Governance für bereitgestellte Ressourcen sicherzustellen.
- Bereitstellungsskripts müssen in einem zentralen Repository aufbewahrt werden, das für das Cloudgovernanceteam zur regelmäßigen Überprüfung und Überwachung zugänglich ist.
- Governanceprozesse müssen Überwachungen zum Bereitstellungszeitpunkt und nachfolgend in regelmäßigen Zyklen umfassen, um für alle Ressourcen Konsistenz zu gewährleisten.
- Die Bereitstellung von Anwendungen, für die eine Kundenauthentifizierung erforderlich ist, erfordert einen genehmigten Identitätsanbieter, der mit dem primären Identitätsanbieter für interne Benutzer kompatibel ist.
- Cloud Governance-Prozesse müssen vierteljährliche Überprüfungen mit den Identitätsverwaltungsteams umfassen. Diese Überprüfungen können helfen, böswillige Akteure oder Nutzungsmuster zu identifizieren, die durch die Konfiguration von Cloudressourcen verhindert werden sollten.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

Der Governance-MVP-Entwurf wird so geändert, dass er neue Azure-Richtlinien und eine Implementierung der Azure-Kostenverwaltung und -Abrechnung umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

- Die Netzwerk- und IT-Sicherheitsteams definieren die Netzwerkanforderungen. Das Cloudgovernanceteam unterstützt die Kommunikation.
- Die Identitäts- und IT-Sicherheitsteams definieren die Identitätsanforderungen und nehmen alle erforderlichen Änderungen an der lokalen Active Directory-Implementierung vor. Das Cloudgovernanceteam überprüft die Änderungen.
- Erstellen Sie in Azure DevOps ein Repository zur Speicherung und Versionsverwaltung für alle relevanten Azure Resource Manager-Vorlagen und Skriptkonfigurationen.
- Azure Recovery Services-Tresorimplementierung:
  - Definieren Sie einen Azure Recovery Services-Tresor für Sicherungs- und Wiederherstellungsvorgänge, und stellen Sie ihn bereit.
  - Erstellen Sie eine Resource Manager-Vorlage zum Erstellen eines Tresors in jedem Abonnement.
- Implementierung von Azure Security Center:
  - Konfigurieren Sie Azure Security Center für jede Verwaltungsgruppe, die Klassifizierungen geschützter Daten enthält.
  - Legen Sie automatische Bereitstellung standardmäßig auf „Aktiviert“ fest, um Patchingkompatibilität zu gewährleisten.
  - Richten Sie Sicherheitskonfigurationen von Betriebssystemen ein. Das IT-Sicherheitsteam definiert die Konfiguration.
  - Unterstützen Sie das IT-Sicherheitsteam bei der anfänglichen Verwendung von Security Center. Übertragen Sie die Nutzung von Security Center an das IT-Sicherheitsteam, behalten Sie jedoch den Zugriff, um die Governance kontinuierlich zu verbessern.
  - Erstellen Sie eine Resource Manager-Vorlage, die die erforderlichen Änderungen für die Security Center-Konfiguration in einem Abonnement widerspiegelt.
- Aktualisieren Sie Azure-Richtlinien für alle Abonnements:
  - Überprüfen und erzwingen Sie die Wichtigkeit von Daten sowie die Datenklassifizierung für alle Verwaltungsgruppen und Abonnements, um Abonnements mit Klassifizierungen geschützter Daten zu identifizieren.
  - Überwachen und erzwingen Sie die ausschließliche Verwendung genehmigter Images.
- Aktualisieren Sie Azure-Richtlinien für alle Abonnements, die Klassifizierungen geschützter Daten enthalten:
  - Überwachen und erzwingen Sie die ausschließliche Verwendung von Azure RBAC-Standardrollen.
  - Überwachen und erzwingen Sie die Verschlüsselung für alle Speicherkonten und Dateien im Ruhezustand auf einzelnen Knoten.
  - Überwachen und erzwingen Sie die Anwendung einer NSG auf alle NICs und Subnetze. Die Netzwerk- und IT-Sicherheitsteams definieren die NSG.
  - Überwachen und erzwingen Sie die Verwendung eines genehmigten Netzwerksubnetzes und virtuellen Netzwerks pro Netzwerkschnittstelle.
  - Überwachen und erzwingen Sie die Einschränkung benutzerdefinierter Routingtabellen.
  - Wenden Sie die integrierten Richtlinien für die Gastkonfiguration wie folgt an:
    - Überwachen Sie die Verwendung sicherer Kommunikationsprotokolle auf Windows-Webservern.
    - Überwachen Sie die korrekte Festlegung der Kennwortsicherheitseinstellungen auf Linux- und Windows-Computern.
  - Überprüfen Sie, ob Azure Recovery Services-Tresore im Abonnement vorhanden sind, und erzwingen Sie deren Bereitstellung.
- Firewallkonfiguration:
  - Identifizieren Sie eine Konfiguration von Azure Firewall, die die erforderlichen Sicherheitsanforderungen erfüllt. Identifizieren Sie alternativ eine kompatible Appliance eines Drittanbieters, die mit Azure kompatibel ist. Der Vergleichstest für die Azure-Sicherheit bietet zusätzliche Informationen zur [Netzwerksicherheitsstrategie](/azure/security/benchmarks/security-controls-v2-governance-strategy#gs-5-define-network-security-strategy) und zu [Firewallkonfigurationen für die Unterstützung Ihrer Sicherheitsstrategie](/azure/security/benchmarks/security-controls-v2-network-security#ns-4-protect-applications-and-services-from-external-network-attacks).
  - Erstellen Sie eine Resource Manager-Vorlage, um die Firewall mit den erforderlichen Konfigurationen bereitzustellen.
- Azure Blueprints:
  - Erstellen Sie eine neue Blaupause mit dem Namen `protected-data`.
  - Fügen Sie der Blaupause die Azure Firewall-Vorlagen, Azure Security Center-Vorlagen und Azure Recovery Services-Tresorvorlagen hinzu.
  - Fügen Sie die neuen Richtlinien für Abonnements geschützter Daten hinzu.
  - Veröffentlichen Sie die Blaupause für jede Verwaltungsgruppe, die aktuell plant, geschützte Daten zu hosten.
  - Wenden Sie die neue Blaupause auf die betroffenen Abonnements sowie auf vorhandene Blaupausen an.

## <a name="conclusion"></a>Zusammenfassung

Durch Hinzufügen der oben genannten Prozesse und Änderungen zum Governance-MVP lassen sich viele der mit der Sicherheitsgovernance verbundenen Risiken beseitigen. Zusammen stellen Sie die Tools zur Überwachung von Netzwerk, Identität und Sicherheit bereit, die zum Schutz von Daten erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Mit der Fortsetzung der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an Cloudgovernance. Für das fiktive Unternehmen in diesem Leitfaden besteht der nächste Schritt darin, unternehmenskritische Workloads zu unterstützen. An dieser Stelle werden Steuerelemente für Ressourcenkonsistenz benötigt.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Ressourcenkonsistenz“](./resource-consistency-improvement.md)
