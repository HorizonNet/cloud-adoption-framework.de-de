---
title: Skalieren einer Migration zu Azure
description: Erfahren Sie, wie Contoso eine Migration in großem Umfang nach Azure behandelt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: c4d5e151d5ea4badd3c6c5fab25f4a6be9ee60c5
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222828"
---
# <a name="scale-a-migration-to-azure"></a>Skalieren einer Migration zu Azure

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso eine Migration zu Azure durchführt. Das Unternehmen überlegt, wie sich eine Migration von mehr als 3.000 Workloads, 8.000 Datenbanken und über 10.000 VMs nach Azure planen und durchführen lässt.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst und sorgt für eine größere Belastung der lokalen Systeme und Infrastrukturen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Es darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss das Contoso-IT-Team Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Verbessern von Kostenmodellen.** Contoso möchte die Kapitalanforderungen im IT-Budget verringern. Contoso möchte Cloudfunktionen zur Skalierung nutzen und die Notwendigkeit teurer Hardware reduzieren.
- **Senken von Lizenzierungskosten.** Contoso möchte die Kosten für die Cloud minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

**Anforderungen** | **Details**
--- | ---
**Schneller Wechsel nach Azure** | Contoso möchte so schnell wie möglich mit dem Verlagern von Apps und VMs nach Azure beginnen.
**Erstellen einer vollständigen Bestandsaufnahme** | Contoso möchte eine vollständige Bestandsliste aller Apps, Datenbanken und VMs in der Organisation erstellen.
**Bewerten und Klassifizieren von Apps** | Contoso will die Vorteile der Cloud voll ausschöpfen. Standardmäßig geht Contoso davon aus, dass alle Dienste als PaaS ausgeführt werden. Für Bereiche, in denen PaaS ungeeignet ist, wird IaaS eingesetzt.
**Bereitstellen von Schulungen und Wechsel zu DevOps** | Contoso möchte zu einem DevOps-Modell wechseln. Contoso wird Schulungen zu Azure und DevOps bereitstellen und Teams nach Bedarf neu organisieren.

Nach der Bestimmung der Ziele und Anforderungen überprüft Contoso den Platzbedarf der IT und stellt den Migrationsprozess zusammen.

## <a name="current-deployment"></a>Aktuelle Bereitstellung

Nach dem Planen und Einrichten einer [Azure-Infrastruktur](./contoso-migration-infrastructure.md) und dem Testen verschiedener Kombinationen aus POC-Migrationsoptionen (Proof of Concept) – wie der Tabelle oben zu entnehmen – kann Contoso mit der vollständigen Migration nach Azure in großem Umfang beginnen. Folgende Elemente möchte Contoso migrieren.

<!--markdownlint-disable MD033 -->

**Element** | **Umfang** | **Details**
--- | --- | ---
**Workloads** | Mehr als 3.000 Apps | Apps werden auf VMs ausgeführt.<br/><br/>  Apps sind Windows-, SQL- und OSS LAMP-basiert.
**Datenbanken** | Ca. 8.500 | Es handelt sich um SQL Server-, MySQL- und PostgreSQL-Datenbanken.
**VMs** | Über 35.000 | VMs werden auf VMware-Hosts ausgeführt und werden von vCenter-Servern verwaltet.

<!--markdownlint-enable MD033 -->

## <a name="migration-process"></a>Migrationsprozess

Nachdem Contoso die geschäftlichen Faktoren und die Migrationsziele bestimmt hat, legt das Unternehmen eine aus vier Phasen bestehende Vorgehensweise für den Migrationsprozess fest:

- **Phase 1: Bewerten.** Die aktuellen Assets werden ermittelt, und es wird bewertet, ob diese sich für die Migration zu Azure eignen.
- **Phase 2: Migrieren.** Die Assets werden zu Azure verschoben. Auf welche Weise die Apps und Objekte nach Azure verschoben werden, richtet sich nach der App und den Zielen, die erreicht werden sollen.
- **Phase 3: Optimieren.** Nach dem Verschieben der Ressourcen zu Azure muss Contoso sie optimieren, um maximale Leistung und Effizienz zu erzielen.
- **Phase 4: Sichern und Verwalten.** Wenn alles eingerichtet ist, nutzt Contoso die Azure-Ressourcen und -Dienste für Sicherheit und Verwaltung, um Cloud-Apps in Azure zu steuern, zu schützen und zu überwachen.

Diese Phasen finden nicht für alle Organisationsteile zur gleichen Zeit statt. Jeder Teil des Migrationsprojekts von Contoso befindet sich in einer anderen Phase des Bewertungs- und Migrationsprozesses. Optimierung, Sicherheit und Verwaltung finden jederzeit statt.

## <a name="phase-1-assess"></a>Phase 1: Bewerten

Contoso startet den Prozess, indem das Unternehmen die lokalen Apps, Daten und Infrastrukturen ermittelt und bewertet. Contoso geht wie folgt vor:

- Contoso muss Apps ermitteln, Abhängigkeiten zwischen Apps zuordnen und über Reihenfolge und Prioritäten der Migration entscheiden.
- Während der Bewertungsphase erstellt Contoso eine umfassende Bestandsliste seiner Apps und Ressourcen. Contoso erstellt nicht nur eine neue Bestandsliste, sondern verwendet und aktualisiert auch die vorhandene Datenbank für die Konfigurationsverwaltung (Configuration Management Database, CMDB) und den Dienstkatalog.
  - Die CMDB enthält die technischen Konfigurationen der Contoso-Apps.
  - Im Dienstkatalog sind die operativen Informationen für die Apps gespeichert, z.B. zugehörige Geschäftspartner und Vereinbarungen zum Servicelevel (Service Level Agreements, SLAs).

### <a name="discover-apps"></a>Ermitteln der Apps

Contoso führt Tausende von Apps auf verschiedenen Servern aus. Zusätzlich zur CMDB und zum Dienstkatalog benötigt Contoso Tools für die Ermittlung und Bewertung.

- Diese Tools müssen einen Mechanismus bereitstellen, der Bewertungsdaten in den Migrationsprozess einbringen kann.
- Bewertungstools müssen Daten bereitstellen, mit denen sich eine sinnvolle Bestandsliste der physischen und virtuellen Ressourcen von Contoso erstellen lässt. Daten müssen Profilinformationen und Leistungsmetriken enthalten.
- Wenn die Ermittlung abgeschlossen ist, sollte Contoso über eine vollständige Bestandsliste sämtlicher Assets und zugehöriger Metadaten verfügen. Anhand dieser Bestandsliste wird der Migrationsplan definiert.

### <a name="identify-classifications"></a>Identifizieren von Klassifizierungen

Contoso legt einige allgemeine Kategorien fest, um die Assets der Bestandsliste zu klassifizieren. Diese Klassifizierungen sind von großer Bedeutung für die Entscheidungen von Contoso in Bezug auf die Migration. Die Klassifizierung hilft dabei, Prioritäten für die Migration festzulegen und komplexe Probleme zu identifizieren.

**Kategorie** | **Zugewiesener Wert** | **Details**
--- | --- | ---
Unternehmensgruppe | Namen der Unternehmensgruppen | Welche Gruppe ist für das Element der Bestandsliste zuständig?
Proof of Concept-Kandidat | J/N | Kann die App als Proof of Concept oder Early Adopter für die Cloudmigration verwendet werden?
Technische Schulden | Keine/Einige/Schwerwiegende | Wird auf dem Bestandslistenelement ein Produkt, ein Betriebssystem oder eine Plattform ausgeführt oder verwendet, für das bzw. die kein Support mehr besteht?
Auswirkungen auf die Firewall | J/N | Kommuniziert die App mit dem Internet oder benötigt externen Datenverkehr?  Lässt sie sich in eine Firewall integrieren?
Sicherheitsprobleme | J/N | Gibt es bekannte Sicherheitsprobleme mit der App?  Verwendet die App nicht verschlüsselte Daten oder veraltete Plattformen?

### <a name="discover-app-dependencies"></a>Ermitteln von App-Abhängigkeiten

Im Rahmen des Bewertungsprozesses muss Contoso ermitteln, wo Apps ausgeführt werden, und die Abhängigkeiten und Verbindungen zwischen App-Servern identifizieren. Contoso ordnet die Umgebung schrittweise zu.

1. Im ersten Schritt ermittelt Contoso die Zuordnung der einzelnen Apps, Netzwerkadressen und Gruppen zu Servern und Computern.
2. Mit diesen Informationen kann Contoso die Apps ermitteln, bei denen wenige Abhängigkeiten bestehen und die sich für eine schnelle Migration eignen.
3. Mithilfe der Zuordnung kann Contoso komplexere Abhängigkeiten und Kommunikationsprozesse zwischen App-Servern identifizieren. Contoso kann diese Server dann logisch gruppieren, um die Apps zu repräsentieren, und basierend auf diesen Gruppen eine Migrationsstrategie planen.

Wenn die Zuordnung abgeschlossen ist, kann Contoso sicherstellen, dass alle App-Komponenten identifiziert sind und bei der Erstellung des Migrationsplans berücksichtigt werden.

![Zuordnung der Abhängigkeiten](./media/contoso-migration-scale/dependency-map.png)

### <a name="evaluate-apps"></a>Evaluieren von Apps

Im letzten Schritt des Ermittlungs- und Bewertungsprozesses kann Contoso die Bewertungs- und Zuordnungsergebnisse evaluieren, um zu ermitteln, auf welche Weise jede App im Dienstkatalog migriert werden soll.

Um diesen Evaluierungsprozesses zu erfassen, fügt Contoso der Bestandsliste einige zusätzliche Klassifizierungen hinzu.

**Kategorie** | **Zugewiesener Wert** | **Details**
--- | --- | ---
Unternehmensgruppe | Namen der Unternehmensgruppen | Welche Gruppe ist für das Element der Bestandsliste zuständig?
Proof of Concept-Kandidat | J/N | Kann die App als Proof of Concept oder Early Adopter für die Cloudmigration verwendet werden?
Technische Schulden | Keine/Einige/Schwerwiegende | Wird auf dem Bestandslistenelement ein Produkt, ein Betriebssystem oder eine Plattform ausgeführt oder verwendet, für das bzw. die kein Support mehr besteht?
Auswirkungen auf die Firewall | J/N | Kommuniziert die App mit dem Internet oder benötigt externen Datenverkehr?  Lässt sie sich in eine Firewall integrieren?
Sicherheitsprobleme | J/N | Gibt es bekannte Sicherheitsprobleme mit der App?  Verwendet die App nicht verschlüsselte Daten oder veraltete Plattformen?
Migrationsstrategie | Zuweisen eines neuen Hosts/Umgestalten/Umstrukturieren/Neuerstellen | Welche Art von Migration wird für die App benötigt? Wie wird die App in Azure bereitgestellt? [Weitere Informationen](./contoso-migration-overview.md#migration-patterns)
Technische Komplexität | 1–5 | Wie komplex ist die Migration? Dieser Wert muss von Contoso DevOps und den entsprechenden Partnern definiert werden.
Geschäftliche Bedeutung | 1–5 | Wie wichtig ist die App für das Geschäft? Eine App für eine kleine Arbeitsgruppe könnte beispielsweise den Wert 1 erhalten, eine kritische App, die in der ganzen Organisation benötigt wird, dagegen den Wert 5. Diese Bewertung wirkt sich auf die Prioritätsstufe bei der Migration aus.
Priorität bei der Migration | 1/2/3 | Wie wird die Priorität der App bei der Migration eingestuft?
Migrationsrisiko | 1–5 | Wie hoch ist die Risikostufe bei der Migration der App? Dieser Wert muss mit Contoso DevOps und den entsprechenden Partnern abgesprochen werden.

### <a name="figure-out-costs"></a>Ermitteln der Kosten

Um die Kosten und die potenziellen Einsparungen einer Migration nach Azure zu ermitteln, kann Contoso den [TCO-Rechner](https://azure.microsoft.com/pricing/tco/calculator) verwenden. Mit diesem Rechner können die Gesamtbetriebskosten für den Betrieb in Azure und als lokale Bereitstellung berechnet und miteinander verglichen werden.

### <a name="identify-assessment-tools"></a>Ermitteln von Bewertungstools

Contoso entscheidet über das Tool für die Ermittlung, Bewertung und Erstellung der Bestandsliste. Contoso identifiziert eine Mischung aus Azure-Tools und -Diensten, nativen App-Tools und Skripts sowie Partnertools. Contoso interessiert sich insbesondere dafür, wie Azure Migrate für eine Bewertung eingesetzt werden kann.

#### <a name="azure-migrate"></a>Azure Migrate

Zur Vorbereitung auf die Migration nach Azure hilft der Azure Migrate-Dienst dabei, lokale VMware-VMs zu ermitteln und zu bewerten. Azure Migrate bietet Folgendes:

1. Ermitteln: Ermitteln Sie lokale virtuelle VMware-Computer.
    - Azure Migrate unterstützt die Ermittlung mehrerer vCenter Server-Instanzen (seriell) und kann Ermittlungen in separaten Azure Migrate-Projekten ausführen.
    - Die Ermittlung erfolgt über den Migrate-Collector, der auf einer VMware-VM ausgeführt wird. Dieser Collector kann VMs auf verschiedenen vCenter Server-Instanzen ermitteln und Daten an verschiedene Projekte senden.
2. Bewerten der Bereitschaft: Bewerten Sie, ob die lokalen Computer für die Ausführung in Azure geeignet sind. Die Bewertung umfasst Folgendes:
    - Größenempfehlungen: Sie erhalten Größenempfehlungen für virtuelle Azure-Computer, die auf der bisherigen Leistung lokaler virtueller Computer basieren.
    - Geschätzte monatliche Kosten: Sie erhalten Kostenschätzungen zur Ausführung lokaler Computer in Azure.
3. Ermitteln von Abhängigkeiten: Abhängigkeiten lokaler Computer werden visuell dargestellt, sodass optimale Computergruppen für die Bewertung und Migration erstellt werden können.

![Azure Migrate](./media/contoso-migration-scale/azure-migrate.png)

##### <a name="migrate-at-scale"></a>Migration in großem Umfang

Contoso muss Azure Migrate verwenden, um den Umfang dieser Migration richtig zu berechnen.

- Contoso bewertet die Apps einzeln mit Azure Migrate. So wird sichergestellt, dass Azure Migrate zeitgenaue Daten an das Azure-Portal sendet.
- Die Administratoren informieren sich über die [Bereitstellung von Azure Migrate in großem Umfang](https://docs.microsoft.com/azure/migrate/how-to-scale-assessment).
- Contoso beachtet die für Azure Migrate geltenden Grenzwerte, die in der folgenden Tabelle zusammengefasst sind.

**Aktion** | **Begrenzung**
--- | ---
Erstellen des Azure Migrate-Projekts | 10.000 virtuelle Computer
Ermittlung | 10.000 virtuelle Computer
Bewertung | 10.000 virtuelle Computer

Contoso verwendet Azure Migrate folgendermaßen:

- Contoso organisiert VMs in vCenter in Ordner. Dies erleichtert die Fokussierung bei den Bewertungen der VMs in einem bestimmten Ordner.
- Azure Migrate verwendet die Azure-Dienstzuordnung, um Abhängigkeiten zwischen Computern zu bewerten. Zu diesem Zweck müssen auf den VMs, die bewertet werden sollen, Agents installiert werden.
  - Contoso verwendet automatisierte Skripts, um die erforderlichen Windows- oder Linux-Agents zu installieren.
  - Mithilfe dieser Skripts kann Contoso eine Pushinstallation auf VMs innerhalb eines vCenter-Ordners ausführen.

#### <a name="database-tools"></a>Datenbanktools

Zusätzlich zu Azure Migrate verwendet Contoso spezielle Tools für die Datenbankbewertung. Tools wie der [Datenmigrations-Assistent](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) (DMA) helfen dabei, SQL Server-Datenbanken im Hinblick auf eine Migration zu bewerten.

Der Datenmigrations-Assistent unterstützt Contoso dabei, herauszufinden, ob lokale Datenbanken mit verschiedenen Azure-Datenbanklösungen kompatibel sind, wie z.B. Azure SQL-Datenbank, SQL Server auf einer Azure-IaaS-VM und verwaltete Azure SQL-Datenbank-Instanzen.

Zusätzlich verwendet Contoso einige andere Skripts, um die SQL Server-Datenbanken zu ermitteln und zu dokumentieren. Diese befinden sich im GitHub-Repository.

#### <a name="partner-assessment-tools"></a>Partnerbewertungstools

Es gibt einige weitere Partnertools, die Contoso bei der Bewertung der lokalen Umgebung im Hinblick auf die Migration nach Azure unterstützen können. [Erfahren Sie mehr](https://azure.microsoft.com/migration/partners) über Azure-Migrationspartner.

## <a name="phase-2-migrate"></a>Phase 2: Migrieren

Wenn die Bewertungsphase abgeschlossen ist, muss Contoso die Tools identifizieren, mit denen das Unternehmen seine Apps, Daten und Infrastruktur nach Azure verschieben möchten.

### <a name="migration-strategies"></a>Migrationsstrategien

Es gibt vier grundlegende Migrationsstrategien, die Contoso in Erwägung ziehen kann.

<!--markdownlint-disable MD033 -->

**Strategie** | **Details** | **Verwendung**
--- | --- | ---
**Zuweisen eines neuen Hosts** | Wird oft als _Lift & Shift_-Migration bezeichnet – eine Option ohne Codeänderungen, mit der Sie Ihre vorhandenen Apps schnell nach Azure migrieren können.<br/><br/> Eine App wird im vorliegenden Zustand migriert – mit den Vorteilen der Cloud, aber ohne die mit Änderungen des Codes verbundenen Risiken und Kosten. | Contoso kann Hosts für strategisch weniger wichtige Apps neu zuweisen, ohne Code ändern zu müssen.
**Umgestalten** | Diese Strategie, die auch als „Erneutes Packen“ bezeichnet wird, erfordert geringfügige Änderungen des App-Codes oder der App-Konfiguration, um die App mit Azure PaaS zu verknüpfen und besser von den Möglichkeiten der Cloud zu profitieren. | Contoso kann strategische Apps umgestalten, um deren grundlegende Funktionalität zu erhalten, sie aber auf einer Azure-Plattform wie Azure App Service auszuführen.<br/><br/> Dafür sind geringfügige Änderungen am Code erforderlich.<br/><br/> Contoso muss sich allerdings um eine VM-Plattform kümmern, da diese nicht von Microsoft verwaltet wird.
**Überarbeiten** | Diese Strategie ändert oder erweitert die Codebasis einer App, um die App-Architektur im Hinblick auf Cloudfunktionen und Skalierbarkeit zu optimieren.<br/><br/> Bei dieser Strategie wird die App zu einer robusten, hochgradig skalierbaren Architektur modernisiert, die unabhängig bereitgestellt werden kann.<br/><br/> Azure-Dienste können den Prozess beschleunigen, Anwendungen zuverlässig skalieren und Ihre Apps völlig problemlos verwalten.
**Neuerstellen** | Bei dieser Strategie wird eine App mithilfe von cloudnativen Technologien von Grund auf neu erstellt.<br/><br/> Azure Platform-as-a-Service (PaaS) stellt eine vollständige Entwicklungs- und Bereitstellungsumgebung in der Cloud zur Verfügung. Dieser Dienst eliminiert einige Kosten und einen Teil der Komplexität in Zusammenhang mit Softwarelizenzen. Außerdem entfällt hierbei die Notwendigkeit zugrunde liegender Infrastruktur- oder Middlewarekomponenten oder anderer Ressourcen für die App. | Contoso kann kritische Apps von Grund auf neu schreiben und dabei von Cloudtechnologien wie serverlosem Computing oder Microservices profitieren.<br/><br/> Contoso verwaltet die selbst entwickelten Apps und Dienste, und Azure kümmert sich um den Rest.

<!--markdownlint-enable MD033 -->

Daten müssen ebenfalls berücksichtigt werden – insbesondere angesichts der Anzahl von Datenbanken, die Contoso betreibt. Die Standardvorgehensweise von Contoso besteht darin, PaaS-Dienste wie Azure SQL-Datenbank zu nutzen, um vollständig von Cloudfunktionen zu profitieren. Durch den Umstieg auf einen PaaS-Dienst für die Datenbanken muss Contoso sich nur noch um die Daten kümmern und kann die zugrunde liegende Plattform Microsoft überlassen.

### <a name="evaluate-migration-tools"></a>Evaluieren von Migrationstools

Contoso nutzt hauptsächlich folgende Azure-Dienste und -Tools für die Migration:

- [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview): Orchestriert die Notfallwiederherstellung und migriert lokale VMs zu Azure.
- [Azure Database Migration Service:](https://docs.microsoft.com/azure/dms/dms-overview) Migriert lokale Datenbanken wie SQL Server, MySQL und Oracle zu Azure.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery ist der primäre Azure-Dienst für die Orchestrierung der Notfallwiederherstellung und Migration aus Azure und von lokalen Standorten nach Azure.

1. Site Recovery ermöglicht und orchestriert die Replikation aus Ihren lokalen Standorten in Azure.
2. Wenn Sie Replikation eingerichtet ist und ausgeführt wird, kann für die lokalen Computer ein Failover nach Azure ausgeführt und so die Migration abgeschlossen werden.

Contoso hat bereits ein [Proof of Concept durchgeführt](./contoso-migration-rehost-vm.md), um herauszufinden, wie Site Recovery bei der Migration in die Cloud helfen kann.

##### <a name="use-site-recovery-at-scale"></a>Verwenden von Site Recovery in großem Umfang

Contoso plant, eine Reihe von „Lift & Shift“-Migrationen durchzuführen. Um sicherzustellen, dass dies funktioniert, repliziert Site Recovery immer jeweils etwa 100 VMs gleichzeitig. Contoso muss eine Kapazitätsplanung für die vorgeschlagene Site Recovery-Migration ausführen, um herauszufinden, wie dies funktioniert.

- Zu diesem Zweck muss Contoso Informationen zu den Datenverkehrsvolumen sammeln. Dies gilt insbesondere für:
  - Contoso muss die Änderungsrate für die VMs ermitteln, die repliziert werden sollen.
  - Contoso muss auch die Netzwerkkonnektivität zwischen dem lokalen Standort und Azure in Betracht ziehen.
- In Bezug auf die Kapazitäts- und Volumenanforderungen muss Contoso basierend auf der täglichen Datenänderungsrate für die erforderlichen VMs genügend Bandbreite zuordnen, um die RPO (Recovery Point Objective) zu erfüllen.
- Abschließend muss das Unternehmen ermitteln, wie viele Server erforderlich sind, um die Site Recovery-Komponenten auszuführen, die für die Bereitstellung benötigt werden.

###### <a name="gather-on-premises-information"></a>Sammeln von Informationen zu lokalen Assets

Contoso kann den [Site Recovery-Bereitstellungsplaner](https://docs.microsoft.com/azure/site-recovery/site-recovery-deployment-planner) verwenden, um folgende Schritte auszuführen:

- Mit diesem Tool kann Contoso remote Profile für VMs erstellen, ohne dass dies sich auf die Produktionsumgebung auswirkt. So lassen sich die Bandbreiten- und Speicheranforderungen für Replikation und Failover ermitteln.
- Contoso kann das Tool ausführen, ohne Site Recovery-Komponenten lokal installieren zu müssen.
- Das Tool sammelt Informationen über kompatible und inkompatible VMs, Datenträger pro VM und Datenänderungen pro Datenträger. Zudem ermittelt es Anforderungen an Netzwerkbandbreite und die erforderliche Azure-Infrastruktur für eine erfolgreiche Replikation und ein erfolgreiches Failover.
- Contoso muss das Planungstool dann auf einem Windows Server-Computer ausführen, der die Mindestanforderungen für den Site Recovery-Konfigurationsserver erfüllt. Der Konfigurationsserver ist ein Site Recovery-Computer, der zum Replizieren der lokalen VMware-VMs erforderlich ist.

###### <a name="identify-site-recovery-requirements"></a>Ermitteln von Site Recovery-Anforderungen

Zusätzlich zu den zu replizierenden VMs benötigt Site Recovery eine Reihe von Komponenten für die VMware-Migration.

<!--markdownlint-disable MD033 -->

**Komponente** | **Details**
--- | ---
**Konfigurationsserver** | Üblicherweise wird eine VMware-VM mithilfe einer OVF-Vorlage eingerichtet.<br/><br/> Die Konfigurationsserverkomponente koordiniert die Kommunikation zwischen der lokalen Umgebung und Azure und verwaltet die Datenreplikation.
**Prozessserver** | Wird standardmäßig auf dem Konfigurationsserver installiert.<br/><br/> Die Prozessserverkomponente empfängt Replikationsdaten, optimiert sie durch Zwischenspeicherung, Komprimierung und Verschlüsselung und sendet sie an Azure Storage.<br/><br/> Der Prozessserver installiert auch Azure Site Recovery Mobility Service auf VMs, die Sie replizieren möchten, und führt auf lokalen Computern eine automatische Ermittlung durch.<br/><br/> Skalierte Bereitstellungen erfordern zusätzliche, eigenständige Prozessserver, um große Mengen an Replikationsdatenverkehr zu verarbeiten.
**Mobilitätsdienst** | Der Mobilitätsdienst-Agent wird auf jeder VMware-VM installiert, die mit Site Recovery migriert wird.

<!--markdownlint-enable MD033 -->

Contoso muss ermitteln, wie diese Komponenten unter Berücksichtigung von Überlegungen hinsichtlich der Kapazität bereitgestellt werden sollten.

<!--markdownlint-disable MD033 -->

**Komponente** | **Kapazitätsanforderungen**
--- | ---
**Maximale tägliche Änderungsrate** | Ein einzelner Prozessserver kann eine tägliche Änderungsrate von bis zu 2 TB verarbeiten. Da eine VM nur einen Prozessserver verwenden kann, beträgt die maximale tägliche Datenänderungsrate, die für eine replizierte VM unterstützt wird, 2 TB.
**Maximaler Durchsatz** | Ein Azure Storage-Konto kann maximal 20.000 Anforderungen pro Sekunde verarbeiten, und die Anzahl von Eingabe-/Ausgabevorgängen pro Sekunde (IOPS) für eine replizierende VM sollte unter diesem Grenzwert liegen. Wenn Ihre VM z.B. über 5 Datenträger verfügt und jeder Datenträger 120 IOPS (mit einer Größe von 8 K) für die Quelle generiert, wird das Azure-Limit von 500 IOPS pro Datenträger eingehalten.<br/><br/> Beachten Sie, dass die Anzahl von erforderlichen Speicherkonten dem IOPS-Gesamtwert des Quellcomputers geteilt durch 20.000 entspricht. Ein replizierter Computer darf nur zu einem einzigen Speicherkonto in Azure gehören.
**Konfigurationsserver** | Basierend auf der Schätzung von Contoso, dass etwa 100–200 VMs gleichzeitig repliziert werden, und basierend auf den [Größenanforderungen des Konfigurationsservers](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#size-recommendations-for-the-configuration-server-and-inbuilt-process-server) berechnet Contoso den erforderlichen Konfigurationsservercomputer folgendermaßen:<br/><br/> CPU: 16 vCPUs (2 Sockets &#215; 8 Kerne @ 2,5 GHz)<br/><br/> Memory: 32 GB<br/><br/> Cachedatenträger: 1 TB<br/><br/> Datenänderungsrate: 1 TB bis 2 TB<br/><br/> Zusätzlich zur Erfüllung der Größenanforderungen muss Contoso sicherstellen, dass der Konfigurationsserver optimal platziert wird: im gleichen Netzwerk und LAN-Segment wie die VMs, die migriert werden sollen.
**Prozessserver** | Contoso stellt einen eigenständigen dedizierten Prozessserver bereit, der 100–200 VMs replizieren kann:<br/><br/> CPU: 16 vCPUs (2 Sockets &#215; 8 Kerne @ 2,5 GHz)<br/><br/> Memory: 32 GB<br/><br/> Cachedatenträger: 1 TB<br/><br/> Datenänderungsrate: 1 TB bis 2 TB<br/><br/> An den Prozessserver werden hohe Anforderungen gestellt, daher sollte er sich auf einem ESXi-Host befinden, der die Datenträger-E/A-Vorgänge, den Netzwerkdatenverkehr und die CPU-Anforderungen für die Replikation verarbeiten kann. Contoso zieht für diesen Zweck einen dedizierten Host in Betracht.
**Netzwerk** | Contoso hat die aktuelle Site-to-Site-VPN-Infrastruktur überprüft und beschlossen, Azure ExpressRoute zu implementieren. Die Implementierung ist von entscheidender Bedeutung, da sie die Latenz senken und die Bandbreite bei der Verbindung mit „USA, Osten 2“ verbessern wird, der primären Azure-Region von Contoso.<br/><br/> **Überwachung:** Contoso muss die vom Prozessserver übertragenen Daten sorgfältig überwachen. Wenn die Daten die Netzwerkbandbreite überlasten, zieht Contoso eine [Drosselung der Bandbreite für den Prozessserver](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#control-network-bandwidth) in Betracht.
**Azure Storage** | Für die Migration muss Contoso den richtigen Typ und die richtige Anzahl von Azure Storage-Zielkonten ermitteln. Site Recovery repliziert VM-Daten in den Azure-Speicher.<br/><br/> Site Recovery kann eine Replikation in Storage-Konten vom Typ „Standard“ oder „Premium“ (SSD) ausführen.<br/><br/> Um die richtigen Entscheidungen zum Thema Speicher zu treffen, muss Contoso die [Speicherlimits](https://docs.microsoft.com/azure/virtual-machines/windows/disks-types) überprüfen und das erwartete Wachstum und die damit verbundene erhöhte Nutzung im Lauf der Zeit berücksichtigen. Angesichts des Migrationstempos und der Priorität von Migrationsvorgängen hat Contoso beschlossen, SSD Premium-Datenträger zu verwenden.<br/><br/>
Contoso hat die Entscheidung getroffen, Managed Disks für alle in Azure bereitgestellten VMs zu nutzen. Der erforderliche IOPS-Wert bestimmt, ob es sich bei den Datenträgern um HDD Standard-Datenträger, SSD Standard-Datenträger oder Premium-Datenträger (SSD) handelt.<br/><br/>

<!--markdownlint-enable MD033 -->

#### <a name="azure-database-migration-service"></a>Azure Database Migration Service

Der Azure Database Migration Service ist ein vollständig verwalteter Dienst, der die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen mit minimalen Ausfallzeiten ermöglicht.

- DMS integriert die Funktionen vorhandener Tools und Dienste. Der Dienst nutzt den Datenmigrations-Assistenten (DMA), um Bewertungsberichte mit Empfehlungen zu Datenbankkompatibilität und erforderlichen Änderungen zu generieren.
- DMS nutzt einen einfachen, selbstbestimmten Migrationsprozess sowie intelligente Bewertungsfunktionen, sodass potenzielle Probleme bereits vor der Migration behoben werden können.
- DMS kann umfangreiche Migrationen aus mehreren Quellsystemen in die Azure-Zieldatenbank durchführen.
- DMS unterstützt SQL Server 2005 bis SQL Server 2017.

DMS ist nicht das einzige Datenbankmigrationstool von Microsoft. Lesen Sie einen [Vergleich der Tools und Dienste](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services) (in englischer Sprache).

##### <a name="use-dms-at-scale"></a>Verwenden von DMS in großem Umfang

Contoso verwendet DMS bei der Migration von SQL Server.

- Bei der Bereitstellung von DMS muss Contoso den Dienst richtig dimensionieren und zum Optimieren der Leistung bei Datenmigrationen einrichten. Contoso wählt die Option für geschäftskritische Umgebungen mit 4 virtuellen Kernen. Auf diese Weise kann der Dienst zur Parallelisierung und für eine schnellere Datenübertragung mehrere vCPUs nutzen.

    ![DMS-Skalierung](./media/contoso-migration-scale/dms.png)

- Eine andere Skalierungstaktik für Contoso besteht darin, die Azure SQL- oder MySQL-Datenbank-Zielinstanz während der Datenmigration vorübergehend zentral auf die SKU im Premium-Tarif hochzuskalieren. Dadurch wird die Datenbankdrosselung minimiert, die sich auf Aktivitäten der Datenübertragung auswirken kann, wenn SKUs in niedrigeren Tarifen verwendet werden.

##### <a name="use-other-tools"></a>Verwenden weiterer Tools

Neben DMS kann Contoso weitere Tools und Dienste nutzen, um VM-Informationen zu erfassen.

- Diese Tools und Dienste verfügen über Skripts zur Unterstützung manueller Migrationen. Sie stehen im GitHub-Repository zur Verfügung.
- Es kann auch eine Reihe von [Partnertools](https://azure.microsoft.com/migration/partners) für die Migration verwendet werden.

## <a name="phase-3-optimize"></a>Phase 3: Optimieren

Nachdem Contoso Ressourcen nach Azure verschoben hat, muss das Unternehmen diese Ressourcen optimieren, um die Leistung zu verbessern. Zudem muss mithilfe von Kostenmanagementtools der ROI maximiert werden. Angesichts der Tatsache, dass Azure ein Dienst mit nutzungsbasierter Bezahlung ist, muss Contoso unbedingt wissen, welche Leistung die Systeme erbringen, und es muss sichergestellt werden, dass die Systeme richtig dimensioniert sind.

### <a name="azure-cost-management"></a>Azure Cost Management

Um die Cloudinvestitionen optimal auszuschöpfen, nutzt Contoso das kostenlose Azure Cost Management-Tool.

- Dank dieser von Cloudyn – einem Microsoft-Tochterunternehmen – erstellten lizenzierten Lösung kann Contoso die Cloudausgaben transparent und präzise verwalten. Die Lösung stellt Tools zum Überwachen, Zuteilen und Senken von Cloudkosten bereit.
- Azure Cost Management bietet einfache Dashboardberichte, um Kunden bei Kostenzuteilungen, Showbacks und Chargebacks zu unterstützen.
- Cost Management optimiert die Ausgaben für die Cloud, indem nicht ausgelastete Ressourcen ermittelt werden, die Contoso dann verwalten und anpassen kann.
- [Erfahren Sie mehr](https://docs.microsoft.com/azure/cost-management/overview) über die Azure Cost Management.

![Kostenverwaltung](./media/contoso-migration-scale/cost-management.png)

### <a name="native-tools"></a>Native Tools

Contoso verwendet auch Skripts, um nicht genutzte Ressourcen zu lokalisieren.

- Bei umfangreichen Migrationen bleiben häufig Daten wie z.B. virtuelle Festplatten übrig, die Gebühren verursachen, aber keinen Wert für das Unternehmen bieten. Skripts stehen im GitHub-Repository zur Verfügung.
- Contoso möchte von der Vorarbeit der IT-Abteilung von Microsoft profitieren und erwägt eine Implementierung des ARO-Toolkits (Azure Resource Optimization).
- Contoso kann im Contoso-eigenen Abonnement ein Azure Automation-Konto mit vorkonfigurierten Runbooks und Zeitplänen bereitstellen und damit bares Geld sparen. Die Azure-Ressourcenoptimierung erfolgt automatisch in einem Abonnement, nachdem ein Zeitplan erstellt oder aktiviert wurde, und umfasst auch die Optimierung neuer Ressourcen.
- So erhalten Kunden dezentralisierte Automatisierungsfunktionen, um die Kosten zu senken. Folgende Features sind enthalten:
  - Automatische Schlummerfunktion für Azure-VMs bei niedrigem CPU-Wert.
  - Planen Sie die Aktivierung und Deaktivierung der Schlummerfunktion für Azure-VMs.
  - Planen Sie die Aktivierung und Deaktivierung der Schlummerfunktion für Azure-VMs in aufsteigender oder absteigender Reihenfolge mithilfe von Azure-Tags.
  - Ressourcengruppen lassen sich bei Bedarf per Massenvorgang löschen.
- Starten Sie mit dem ARO-Toolkit in diesem [GitHub-Repository](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

### <a name="partner-optimization-tools"></a>Partneroptimierungstools

Partnertools wie [Hanu](https://hanu.com/insight) und [Scalr]( https://www.scalr.com/cost-optimization) können ebenfalls genutzt werden.

## <a name="phase-4-secure-and-manage"></a>Phase 4: Sichern und Verwalten

In dieser Phase verwendet Contoso die Sicherheits- und Verwaltungsressourcen von Azure, um die Cloud-Apps in Azure zu steuern, zu sichern und zu überwachen. Diese Ressourcen helfen beim Ausführen einer sicheren und optimal verwalteten Umgebung mithilfe von Produkten, die im Azure-Portal verfügbar sind. Contoso nutzt diese Dienste zunächst während der Migration. Danach verwendet das Unternehmen viele der Dienste dank Azure-Hybridunterstützung weiterhin, um eine konsistente Umgebung in der gesamten Hybrid Cloud zu gewährleisten.

### <a name="security"></a>Sicherheit

Contoso verlässt sich auf das Azure Security Center, um eine einheitliche Sicherheitsverwaltung und einen erweiterten Schutz vor Bedrohungen über Hybrid Cloud-Workloads hinweg zu erzielen.

- Das Security Center bietet umfassende Einblicke und Steuerungsmöglichkeiten für die Sicherheit von Cloud-Apps in Azure.
- Contoso kann Bedrohungen frühzeitig erkennen und Maßnahmen ergreifen, um gegen sie vorzugehen. Außerdem kann das Unternehmen mithilfe des adaptiven Bedrohungsschutzes Risiken reduzieren.

[Erfahren Sie mehr](https://azure.microsoft.com/services/security-center) über das Security Center.

### <a name="monitoring"></a>Überwachung

Contoso benötigt Einblicke in die Integrität und Leistung der gerade migrierten Apps, Infrastruktur und Daten, die jetzt auf Azure basieren. Contoso nutzt integrierte Azure-Tools für die Cloudüberwachung wie Azure Monitor, Log Analytics-Arbeitsbereich und Application Insights.

- Mit diesen Tools kann Contoso ganz einfach Daten aus verschiedenen Quellen sammeln und umfassende Erkenntnisse erhalten. Contoso kann beispielsweise die CPU-, Datenträger- und Arbeitsspeichernutzung der VMs messen, Anwendungen und Netzwerkabhängigkeiten auf mehreren VMs anzeigen und die Entwicklung der Anwendungsleistung verfolgen.
- Contoso nutzt diese Cloudüberwachungstools, um Maßnahmen zu ergreifen und Integrationen in Dienstlösungen durchzuführen.
- [Erfahren Sie mehr](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) über die Überwachung in Azure.

### <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Contoso benötigt eine BCDR-Strategie (Business Continuity & Disaster Recovery) für seine Azure-Ressourcen.

- Azure bietet [integrierte BCDR-Features](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications), um die Datensicherheit und den unterbrechungsfreien Betrieb von Apps und Diensten zu gewährleisten.
- Zusätzlich zu den integrierten Features möchte Contoso die Wiederherstellbarkeit nach Ausfällen sicherstellen, teure Geschäftsunterbrechungen vermeiden, Complianceziele erfüllen und die Daten vor Ransomware und menschlichen Fehlern schützen. Gehen Sie dazu folgendermaßen vor:
  - Contoso stellt Azure Backup als kostengünstige Lösung für die Sicherung von Azure-Ressourcen bereit. Da dieser Dienst integriert ist, kann Contoso Cloudsicherungen in einigen wenigen einfachen Schritten einrichten.
  - Contoso richtet eine Notfallwiederherstellung für Azure-VMs ein und nutzt dabei Azure Site Recovery für Replikation, Failover und Failback zwischen Azure-Regionen, die das Unternehmen angibt. So wird sichergestellt, dass Apps, die auf Azure-VMs ausgeführt werden, in einer sekundären, von Contoso ausgewählten Region verfügbar bleiben, falls in der primären Region ein Ausfall auftritt. [Weitere Informationen](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel plante Contoso eine Azure-Migration in großem Umfang. Das Unternehmen teilte den Migrationsprozess in vier Phasen auf – von der Bewertung und Migration über die Optimierung bis hin zur Sicherheit und Verwaltung nach Abschluss der Migration. Es ist wichtig, ein Migrationsprojekt als vollständigen Prozess zu planen. Die eigentliche Migration der Systeme in einer Organisation sollte dann aber anhand von Klassifizierungen und in einer Größenordnung durchgeführt werden, die für das Business sinnvoll ist. Durch Bewertung von Daten und Anwendung von Klassifizierungen kann jedes Projekt in eine Reihe kleinerer Migrationen unterteilt werden, die sich sicher und schnell ausführen lassen. Diese kleineren Migrationen summieren sich dann schnell zu einer großen erfolgreichen Migration nach Azure.
