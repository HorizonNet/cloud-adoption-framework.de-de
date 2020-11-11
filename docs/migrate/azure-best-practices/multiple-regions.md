---
title: Leitfaden zur Entscheidungsfindung für Azure-Regionen
description: Erfahren Sie mehr über Cloudplattformregionen sowie die Faktoren und Merkmale, die sich auf die Auswahl ihrer Azure-Region auswirken können.
author: doodlemania2
ms.author: dermar
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: f24f29b9d910c97da2dc1109db8b186c0dfef0bd
ms.sourcegitcommit: 2c949c44008161e50b91ffd3f01f6bf32da2d4d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2020
ms.locfileid: "94432634"
---
# <a name="azure-regions-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Azure-Regionen

Azure besteht aus vielen Regionen überall auf der Welt. Jede [Azure-Region](https://azure.microsoft.com/global-infrastructure/regions) hat bestimmte Merkmale, weshalb die Wahl der zu verwendenden Region überaus wichtig ist. Dazu gehören verfügbare Dienste, Kapazität, Einschränkungen und Datenhoheit.

- **Verfügbare Dienste:** Welche Dienste in den jeweiligen Regionen bereitgestellt werden, hängt von zahlreichen Faktoren ab. Wählen Sie eine Region für Ihre Workload aus, die den gewünschten Dienst enthält. Weitere Informationen finden Sie unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services).
- **Kapazität:** Jede Region hat eine maximale Kapazität. Diese wirkt sich darauf aus, welche Arten von Abonnements welche Diensttypen unter welchen Bedingungen bereitstellen können. Kapazität ist nicht das Gleiche wie Abonnementkontingente. Falls Sie eine umfangreiche Rechenzentrumsmigration zu Azure planen, informieren Sie sich ggf. bei Ihrem Azure-Vertreterteam oder -Kundenbetreuer vor Ort, ob eine Bereitstellung im gewünschten Umfang möglich ist.
- **Einschränkungen:** In bestimmten Regionen unterliegt die Bereitstellung von Diensten gewissen Einschränkungen. Einige Regionen stehen beispielsweise nur als Sicherungs- oder Failoverziel zur Verfügung. Weitere wichtige Einschränkungen sind [Datenhoheitsanforderungen](https://azure.microsoft.com/global-infrastructure/geographies).
- **Datenhoheit:** Bestimmte Regionen sind für spezifische unabhängige Entitäten dediziert. Zwar sind alle Regionen Azure-Regionen, diese unabhängigen Regionen sind jedoch vollständig von Azure isoliert. Sie werden nicht zwangsläufig von Microsoft verwaltet und sind möglicherweise auf bestimmte Kundentypen beschränkt. Diese unabhängigen Regionen sind:
  - [Azure China](https://azure.microsoft.com/global-infrastructure/china)
  - [Azure Deutschland](https://azure.microsoft.com/global-infrastructure/germany): Azure Deutschland wird zugunsten von nicht unabhängigen Azure-Standardregionen in Deutschland eingestellt.
  - [Azure US Government](https://azure.microsoft.com/global-infrastructure/government)
  - Zwei Regionen in [Australien](https://azure.microsoft.com/global-infrastructure/australia) werden zwar von Microsoft verwaltet, werden aber für die australische Regierung und ihre Kunden und Auftragnehmer bereitgestellt. Für diese beiden Regionen gelten daher ähnliche Clienteinschränkungen wie für die anderen Sovereign Clouds.

## <a name="operate-in-multiple-geographic-regions"></a>Agieren in mehreren geografischen Regionen

Wenn Unternehmen in mehreren geografischen Regionen agieren, ist das zwar grundlegend für die Resilienz, kann aber die Komplexität erhöhen:

- Ressourcenverteilung
- Benutzerzugriffsprofile
- Complianceanforderungen
- Regionale Resilienz

Die Regionsauswahl spielt eine große Rolle für Ihre Cloudeinführungsstrategie insgesamt. Beginnen wir mit Überlegungen zum Netzwerk.

## <a name="network-considerations"></a>Überlegungen zu Netzwerken

Jede robuste Cloudbereitstellung ist auf ein sorgfältig durchdachtes Netzwerk angewiesen, wobei auch Azure-Regionen eine Rolle spielen. Sie sollten Folgendes berücksichtigen:

- Azure-Regionen werden paarweise bereitgestellt. Für den Fall eines schwerwiegenden Ausfalls einer Region wird eine andere Region innerhalb derselben geopolitischen Grenze als gekoppelte Region festgelegt. Die Bereitstellung in Regionspaaren sollte als primäre und sekundäre Resilienzstrategie in Erwägung gezogen werden. Eine Ausnahme für diese Strategie ist `Brazil South`. Diese Region ist mit `South Central US` gekoppelt. Weitere Informationen finden Sie unter [Azure-Regionspaare](/azure/best-practices-availability-paired-regions).

  - Azure Storage unterstützt [georedundanten Speicher (GRS)](/azure/storage/common/storage-redundancy-grs). Das bedeutet, dass drei Kopien Ihrer Daten in Ihrer primären Region und drei zusätzliche Kopien in der gekoppelten Region gespeichert werden. Die Speicherkopplung für GRS kann nicht geändert werden.
  - Dienste, die auf Azure Storage-GRS basieren, können von dieser Regionskopplung profitieren. Ihre Anwendungen und das Netzwerk müssen dazu entsprechend ausgerichtet sein.
  - Falls Sie GRS nicht für Ihre regionalen Resilienzanforderungen nutzen möchten, sollten Sie die gekoppelte Region nicht als sekundäre Region verwenden. Ein regionaler Ausfall hat aufgrund der Ressourcenmigration eine hohe Auslastung der Ressourcen in der gekoppelten Region zur Folge. Sie können diesen Druck vermeiden, indem die Wiederherstellung an einen alternativen Standort durchgeführt und zusätzlich beschleunigt wird.
  > [!WARNING]
  > Verwenden Sie Azure-GRS nicht für VM-Sicherungen oder -Wiederherstellungen. Nutzen Sie stattdessen [Azure Backup](https://azure.microsoft.com/services/backup) und [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery) in Kombination mit [verwalteten Azure-Datenträgern](/azure/virtual-machines/windows/managed-disks-overview), um die Resilienz Ihrer IaaS-Workloads (Infrastructure as a Service) zu unterstützen.

- Azure Backup und Azure Site Recovery arbeiten mit Ihrem Netzwerkentwurf zusammen, um regionale Resilienz für Ihre IaaS- und Datensicherungsanforderungen bereitzustellen. Stellen Sie sicher, dass das Netzwerk optimiert ist, damit Datenübertragungen ausschließlich über den Microsoft-Backbone abgewickelt werden, und verwenden Sie nach Möglichkeit [Peering virtueller Netzwerke](/azure/virtual-network/virtual-network-peering-overview). Größere Organisationen mit globalen Bereitstellungen können für regionsübergreifendes Routing stattdessen [ExpressRoute Premium](/azure/expressroute/expressroute-introduction) nutzen, um regionale Gebühren für ausgehenden Datenverkehr zu sparen.

- Azure-Ressourcengruppen sind regionsspezifisch. Es ist jedoch normal, dass sich Ressourcen in einer Ressourcengruppe über mehrere Regionen erstrecken. Berücksichtigen Sie in diesem Fall, dass bei einem regionalen Ausfall Vorgänge der Steuerungsebene für eine Ressourcengruppe in der betroffenen Region nicht erfolgreich sind, auch wenn die Ressourcen in anderen Regionen (innerhalb dieser Ressourcengruppe) weiterhin aktiv sind. Dies kann sich sowohl auf Ihre Netzwerk- als auch auf Ihre Ressourcengruppengestaltung auswirken.

- Viele PaaS-Dienste (Plattform as a Service) in Azure unterstützen [Dienstendpunkte](/azure/virtual-network/virtual-network-service-endpoints-overview) oder [Azure Private Link](/azure/private-link/private-link-overview). Beide Lösungen haben erhebliche Auswirkungen auf Ihre Netzwerküberlegungen im Zusammenhang mit regionaler Resilienz, Migration und Governance.

- Viele PaaS-Dienste basieren auf eigenen Lösungen für regionale Resilienz. So ermöglichen beispielsweise Azure SQL-Datenbank und Azure Cosmos DB eine problemlose Replikation in zusätzlichen Regionen. Dienste wie Azure DNS weisen keine regionalen Abhängigkeiten auf. Für Ihre Überlegungen hinsichtlich der Dienste, die Sie im Rahmen Ihres Einführungsprozesses nutzen möchten, ist es wichtig, die genauen Failoverfunktionen und Wiederherstellungsschritte zu kennen, die ggf. für die jeweiligen Azure-Dienste erforderlich sind.

- Neben der Bereitstellung in mehreren Regionen für die Notfallwiederherstellung entscheiden sich viele Organisationen für eine Bereitstellung mit Aktiv/Aktiv-Muster, sodass kein Failover erforderlich ist. Diese Methode hat außerdem die zusätzlichen Vorteile eines globalen Lastenausgleichs, einer höheren Fehlertoleranz und einer höheren Netzwerkleistung. Wenn Sie dieses Muster nutzen möchten, müssen Ihre Anwendungen die Aktiv/Aktiv-Ausführung in mehreren Regionen unterstützen.

> [!WARNING]
> Azure-Regionen sind hochverfügbare Konstrukte mit SLAs für die darin ausgeführten Dienste. Geschäftskritische Anwendungen sollten aber niemals von einer einzelnen Region abhängig sein. Planen Sie stets für regionale Ausfälle, und üben Sie Wiederherstellungs- und Problembehebungsschritte.

Unter Berücksichtigung der Netzwerktopologie sollten Sie als nächsten Schritt zusätzliche Dokumentationen lesen und sich eine Prozessausrichtung ansehen, die möglicherweise erforderlich ist. Anhand der folgenden Punkte können Sie die potenziellen Herausforderungen bewerten und eine allgemeine Vorgehensweise festlegen:

- Ziehen Sie eine stabilere Implementierung von Bereitschaft und Governance in Betracht.
- Erstellen Sie ein Inventar der betroffenen Geografien. Stellen Sie eine Liste der betroffenen Regionen und Länder zusammen.
- Dokumentieren Sie Anforderungen an die Datenhoheit. Liegen in den ermittelten Ländern Complianceanforderungen vor, die die Datenhoheit regulieren?
- Dokumentieren Sie die Benutzerbasis. Wird sich die Cloudmigration auf Mitarbeiter, Partner oder Kunden im ermittelten Land/der ermittelten Region auswirken?
- Dokumentieren Sie Rechenzentren und Assets. Sind im ermittelten Land/der Region Assets vorhanden, die in das Migrationsprojekt aufgenommen werden sollten?
- Dokumentieren Sie die regionale SKU-Verfügbarkeit sowie Failoveranforderungen.

Stimmen Sie Änderungen im gesamten Migrationsprozess ab, um das anfängliche Inventar zu aktualisieren.

## <a name="document-complexity"></a>Dokumentkomplexität

Die folgende Tabelle kann beim Dokumentieren der Ergebnisse aus den oben genannten Schritten helfen:

| Region        | Country     | Lokale Mitarbeiter | Lokale externe Benutzer   | Lokale Rechenzentren oder Assets | Anforderungen an die Datenhoheit |
|---------------|-------------|-----------------|------------------------|-----------------------------|-------------------------------|
| Nordamerika | USA         | Ja             | Partner und Kunden | Ja                         | Nein                            |
| Nordamerika | Canada      | Nein              | Kunden              | Ja                         | Ja                           |
| Europa        | Deutschland     | Ja             | Partner und Kunden | Nein – nur Netzwerk           | Ja                           |
| Asien-Pazifik  | Südkorea | Ja             | Partner               | Ja                         | Nein                            |

## <a name="relevance-of-data-sovereignty"></a>Relevanz der Datenhoheit

Auf der ganzen Welt haben Organisationen damit begonnen, Anforderungen an die Datenhoheit zu etablieren, beispielsweise durch die Datenschutz-Grundverordnung (DSGVO). Complianceanforderungen dieser Art erfordern häufig einen Speicherort innerhalb einer bestimmten Region oder sogar innerhalb eines bestimmten Lands, um die Bürger dieses Lands zu schützen. In einige Fällen müssen Daten zu Kunden, Mitarbeitern oder Partnern auf einer Cloudplattform gespeichert werden, die sich in derselben Region befindet wie die Endbenutzer.

Diese Herausforderung ist ein wichtiger Beweggrund für Cloudmigrationen in Unternehmen, die auf globaler Ebene tätig sind. Um Complianceanforderungen zu erfüllen, haben einige Unternehmen sich dafür entschieden, duplizierte IT-Assets bei Cloudanbietern innerhalb einer Region bereitzustellen. In der Tabelle oben ist Deutschland ein gutes Beispiel für dieses Szenario. Dieses Beispiel umfasst Kunden, Partner und Mitarbeiter in Deutschland, aber keine IT-Assets. Hier kann sich das Unternehmen dafür entscheiden, einige Assets in einem Rechenzentrum innerhalb des DSGVO-Gebiets bereitzustellen, möglicherweise sogar in einem der deutschen Azure-Rechenzentren. Kenntnisse der Daten, für die die DSGVO gilt, würden dem Cloudeinführungsteam dabei helfen, den besten Migrationsansatz für diesen Fall zu ermitteln.

### <a name="why-is-the-location-of-end-users-relevant"></a>Warum ist der Standort von Endbenutzern relevant?

Unternehmen, die Endbenutzer in mehreren Ländern unterstützen, haben technische Lösungen zur Verarbeitung des Datenverkehrs von Endbenutzern entwickelt. In einigen Fällen umfasst dies die Speicherung von Assets innerhalb einer bestimmten Region oder eines bestimmten Lands. In anderen Szenarios entscheiden sich Unternehmen möglicherweise dazu, globale WAN-Lösungen zu implementieren, um die Anforderungen disparater Benutzergruppen über netzwerkzentrierte Lösungen zu erfüllen. In beiden Fällen können sich die Nutzungsprofile dieser disparaten Endbenutzergruppen auf die Migrationsstrategie auswirken.

Da das Unternehmen Mitarbeiter, Partner und Kunden in Deutschland unterstützt, ohne dass sich aktuell Rechenzentren dort befinden, hat es vermutlich eine Mietleitungslösung implementiert. Diese Art von Lösung leitet Datenverkehr an Rechenzentren in anderen Ländern weiter. Diese vorhandene Weiterleitung stellt ein erhebliches Risiko für die wahrgenommene Leistung der migrierten Anwendungen dar. Durch Hinzufügen zusätzlicher Hops zu einem etablierten und optimierten globalen WAN kann die Wahrnehmung entstehen, dass die Leistung von Anwendungen nach der Migration gesunken sei. Das Auffinden und Beheben solcher Probleme kann beträchtliche Verzögerungen für ein Projekt bedeuten.

Jeder der unten genannten Prozesse umfasst Hinweise dazu, wie sich diese Komplexität bewältigen lässt – über Voraussetzungen sowie Bewertungs-, Migrations- und Optimierungsprozesse hinweg. Die Kenntnis der Benutzerprofile in den einzelnen Ländern ist sehr wichtig, um diese Komplexität zu bewältigen.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Warum ist der Standort von Rechenzentren relevant?

Der Standort vorhandener Rechenzentren kann eine Migrationsstrategie beeinflussen. Beispiel:

**Architekturentscheidungen** : Das Festlegen der Zielregion ist einer der ersten Schritte beim Entwerfen einer Migrationsstrategie. Der Standort der vorhandenen Assets spielt dabei häufig eine Rolle. Darüber hinaus können die Verfügbarkeit von Clouddiensten und die Kosten pro Einheit für diese Dienste zwischen Regionen variieren. Das Wissen darüber, wo sich aktuelle und zukünftige Ressourcen befinden, beeinflusst Entwurfsentscheidungen und kann sich auf Budgetschätzungen auswirken.

**Abhängigkeiten zwischen Rechenzentren** : Die Daten in der vorherigen Tabelle zeigen, dass Abhängigkeiten zwischen verschiedenen globalen Rechenzentren wahrscheinlich sind. Diese Abhängigkeiten sind in vielen Unternehmen möglicherweise nicht sorgfältig dokumentiert oder werden nicht richtig verstanden. Der Ansatz Ihres Unternehmens für die Bewertung von Benutzerprofilen kann beim Identifizieren einiger dieser Abhängigkeiten in Ihrer Organisation unterstützen. Außerdem sollte Ihr Team zusätzliche Bewertungsschritte in Erwägung ziehen, die die Risiken und Komplexitäten abmildern, die aus Abhängigkeiten entstehen.

## <a name="implement-the-general-approach"></a>Implementieren der allgemeinen Vorgehensweise

Für den folgenden Ansatz wird ein datengesteuertes Modell verwendet, um die Komplexität einer globalen Migration zu bewältigen. Wenn der Umfang einer Migration mehrere Regionen umfasst, sollte das Cloudeinführungsteam folgende Überlegungen zur Bereitschaft berücksichtigen:

- Zur Sicherstellung der Datenhoheit müssen einige Assets möglicherweise an bestimmten Standorten bereitgestellt werden, für viele Assets gelten diese Complianceeinschränkungen jedoch unter Umständen nicht. Aspekte wie Protokollierung, Berichterstellung, Netzwerkrouting, Identität und weitere zentrale IT-Dienste können möglicherweise als freigegebene Dienste über mehrere Abonnements oder sogar Regionen hinweg gehostet werden. Das Cloudeinführungsteam sollte für diese Dienste ein Freigabemodell evaluieren, wie in der [Referenzarchitektur für eine Hub-and-Spoke-Topologie mit freigegebenen Diensten](/azure/architecture/reference-architectures/hybrid-networking/#hub-spoke-network-topology) beschrieben.
- Wenn mehrere Instanzen ähnlicher Umgebungen bereitgestellt werden müssen, könnte eine Umgebungsfactory für Konsistenz sorgen, die Governance verbessern und die Bereitstellung beschleunigen. Der [Governanceleitfaden für komplexe Unternehmen](../../govern/guides/complex/index.md) etabliert eine Vorgehensweise, bei der eine Umgebung erstellt wird, die sich über mehrere Regionen hinweg skalieren lässt.

Wenn das Team mit dem grundlegenden Ansatz zufrieden und die Bereitschaft entsprechend vorhanden ist, müssen einige Voraussetzungen in Bezug auf die Daten berücksichtigt werden:

- **Allgemeine Ermittlung** : Füllen Sie die oben stehende Tabelle zum [Dokumentieren der Komplexität](#document-complexity) aus.
- **Durchführen einer Analyse der Benutzerprofile in jedem betroffenen Land** : Sie müssen die allgemeine Weiterleitung des Datenverkehrs von Endbenutzern bereits frühzeitig im Migrationsprozess kennen. Das Ändern globaler geleaster Leitungen und das Hinzufügen von Verbindungen wie ExpressRoute zu einem Cloudrechenzentrum kann die Netzwerkeinrichtung um Monate verzögern. Gehen Sie diesen Aspekt so früh wie möglich im Prozess an.
- **Anfängliche Bewertung des digitalen Eigentums** : Jedes Mal, wenn der Komplexitätsgrad einer Migrationsstrategie erhöht wird, sollte eine Bewertung des digitalen Eigentums durchgeführt werden. Unterstützung hierbei finden Sie in den Anleitungen zur [Bewertung des digitalen Eigentums](../../digital-estate/index.md).
  - **Weitere Anforderungen in Bezug auf das digitale Eigentum** : Richten Sie Kennzeichnungsrichtlinien ein, um alle Workloads zu ermitteln, die von Anforderungen an die Datenhoheit betroffen sind. Die Kennzeichnungspflicht sollte bei der Bewertung des digitalen Eigentums beginnen und bis zu den migrierten Assets beibehalten werden.
- **Evaluieren eines Hub-and-Spoke-Modells:** In verteilten Systemen existieren häufig allgemeine Abhängigkeiten. Diese Abhängigkeiten können häufig durch Implementierung eines Hub-and-Spoke-Modells verarbeitet werden. Ein solches Modell gehört nicht zum Umfang des Migrationsprozesses, sollte aber bei weiteren Iterationen der [Bereitschaftsprozesse](../../ready/index.md) Berücksichtigung finden.
- **Priorisierung des Migrationsbacklogs** : Wenn Netzwerkänderungen erforderlich sind, um die Produktionsbereitstellung einer Workload zu unterstützen, die mehrere Regionen unterstützt, muss das Cloudstrategieteam Eskalationen in Bezug auf diese Netzwerkänderungen nachverfolgen und verwalten. Die Unterstützung durch die Geschäftsleitung ermöglicht es, die Änderungen zu beschleunigen, indem das Strategieteam freigestellt wird, um den Rückstand wieder zu priorisieren und um sicherzustellen, dass globale Workloads nicht von Netzwerkänderungen blockiert werden. Solche Workloads sollten erst priorisiert werden, nachdem die Netzwerkänderungen abgeschlossen sind.

Anhand dieser Voraussetzungen lassen sich Prozesse einrichten, mit denen diese Komplexität während der Umsetzung der Migrationsstrategie bewältigt werden kann.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

In Bezug auf globale Ressourcen und Komplexitäten der Benutzerbasis in Migrationsszenarios sollten Sie einige wichtige Aktivitäten hinzufügen, um Ihre Migrationskandidaten zu bewerten. Diese Aktivitäten erzeugen Daten, mit denen Hindernisse und Ergebnisse für globale Benutzer und Ressourcen deutlich gemacht werden können.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

**Evaluieren von rechenzentrumsübergreifenden Abhängigkeiten** : Die [Tools für die Visualisierung von Abhängigkeiten in Azure Migrate](/azure/migrate/concepts-dependency-visualization) helfen bei der Ermittlung von Abhängigkeiten. Die Verwendung dieser Tools vor der Migration ist eine bewährte Vorgehensweise. Wenn es um globale Komplexität geht, wird diese Verwendung zu einem notwendigen Schritt im Bewertungsprozess. Die Visualisierung durch die [Gruppierung von Abhängigkeiten](/azure/migrate/how-to-create-group-machine-dependencies) kann dabei helfen, die IP-Adressen und Ports aller Assets zu ermitteln, die zur Unterstützung der Workload erforderlich sind.

> [!IMPORTANT]
>
> - Ein Experte, der über Kenntnisse zu Ressourcenplatzierung und IP-Adressschemas verfügt, muss Ressourcen identifizieren, die sich in einem sekundären Rechenzentrum befinden.
> - Evaluieren Sie sowohl Downstreamabhängigkeiten als auch Clients in der Visualisierung, um bidirektionale Abhängigkeiten zu verstehen.

**Erkennen der globalen Auswirkungen auf Benutzer** : Die Ergebnisse der Benutzerprofilanalyse sollten alle Workloads bezeichnen, die durch globale Benutzerprofile beeinflusst werden. Wenn sich ein Migrationskandidat auf der Liste der betroffenen Workloads befindet, sollte sich der Architekt, der die Migration vorbereitet, mit den Experten für Netzwerkfunktionen und Betrieb beraten. Diese helfen dabei, Netzwerkrouting und Leistungserwartungen zu überprüfen. Eine Mindestanforderung ist, dass die Architektur eine ExpressRoute-Verbindung zwischen dem nächstgelegenen Netzwerkbetriebszentrum und Azure umfasst. Die [Referenzarchitektur für ExpressRoute-Verbindungen](/azure/architecture/reference-architectures/hybrid-networking/expressroute) kann bei der Konfiguration der notwendigen Verbindung helfen.

**Entwurf im Hinblick auf die Compliance** : Die Ergebnisse der Benutzerprofilanalyse sollten alle Workloads bezeichnen, die durch Anforderungen hinsichtlich der Datenhoheit beeinflusst werden. Während der architekturbezogenen Aktivitäten des Bewertungsprozesses sollte der zuständige Architekt Complianceexperten konsultieren. So können alle Anforderungen für die Migration bzw. Bereitstellung über mehrere Regionen hinweg verstanden werden. Diese Anforderungen haben erhebliche Auswirkungen auf Entwurfsstrategien. Die Referenzarchitekturen für [Webanwendungen in mehreren Regionen](/azure/architecture/reference-architectures/app-service-web-app/multi-region) und [n-schichtige Anwendungen in mehreren Regionen](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) können beim Entwurf hilfreich sein.

> [!WARNING]
> Bei Verwendung einer der gerade genannten Referenzarchitekturen müssen möglicherweise bestimmte Datenelemente von Replikationsprozessen ausgeschlossen werden, um Datenhoheitsanforderungen zu erfüllen. Dadurch wird ein weiterer Schritt zum Prozess der Höherstufung hinzugefügt.

## <a name="migration-process-changes"></a>Änderungen für den Migrationsprozess

Beim Migrieren einer Anwendung, die in mehreren Regionen bereitgestellt werden muss, muss das Cloudeinführungsteam einige Überlegungen berücksichtigen. Hierzu gehören der Entwurf des Azure Site Recovery-Tresors, des Konfigurations-/Prozessservers, der Netzwerkbandbreite sowie die Datensynchronisierung.

### <a name="suggested-action-during-the-migration-process"></a>Empfohlene Aktion während des Migrationsprozesses

**Entwurf des Azure Site Recovery-Tresors** : Azure Site Recovery ist das empfohlene Tool für die cloudnative Replikation und Synchronisierung von digitalen Assets in Azure. Site Recovery repliziert Daten zum Asset in einen Site Recovery-Tresor, der an ein bestimmtes Abonnement in einer bestimmten Region und einem bestimmten Azure-Rechenzentrum gebunden ist. Wenn Sie Ressourcen in eine sekundäre Region replizieren, benötigen Sie möglicherweise auch einen zweiten Site Recovery-Tresor.

**Entwurf des Konfigurations- und Prozessservers:** Site Recovery arbeitet mit einer lokalen Instanz eines Konfigurations- und Prozessservers, die an einen einzelnen Site Recovery-Tresor gebunden ist. Das bedeutet, dass möglicherweise eine zweite Instanz dieser Server im Quellrechenzentrum installiert werden muss, um die Replikation zu ermöglichen.

**Entwurf der Netzwerkbandbreite** : Während der Replikation und der fortlaufenden Synchronisierung werden binäre Daten über das Netzwerk vom Quellrechenzentrum zum Site Recovery-Tresor im Azure-Zielrechenzentrum verschoben. Dieser Prozess verbraucht Bandbreite. Die Duplizierung der Workload in eine zweite Region verdoppelt die verbrauchte Bandbreitenmenge. Wenn die Bandbreite begrenzt ist oder eine Workload ein hohes Maß an Konfiguration oder Datenabweichung beinhaltet, kann dies zu Konflikten hinsichtlich des Zeitraums führen, der für den Abschluss der Migration erforderlich ist. Wichtiger noch: Es könnte sich auf die Servicequalität oder die Anwendungsleistung auswirken, wenn Benutzer bzw. Anwendungen noch auf die Bandbreite des Quellrechenzentrums angewiesen sind.

**Datensynchronisierung** : Häufig wird die Bandbreite bei der Synchronisierung der Datenplattform am meisten beansprucht. Wie in den Referenzarchitekturen für [Webanwendungen in mehreren Regionen](/azure/architecture/reference-architectures/app-service-web-app/multi-region) und [n-schichtige Anwendungen in mehreren Regionen](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) definiert, ist eine Synchronisierung der Daten häufig erforderlich, um die Anwendungen auf dem gleichen Stand zu halten. Wenn dies der gewünschte Betriebszustand der Anwendung ist, kann es klug sein, eine vollständige Synchronisierung zwischen der Quelldatenplattform und den einzelnen Cloudplattformen durchzuführen. Dies sollte geschehen, bevor die Anwendung und die Assets der mittleren Schicht migriert werden.

**Azure-zu-Azure-Notfallwiederherstellung:** Eine alternative Option kann die Komplexität weiter verringern. Wenn Zeitpläne und Datensynchronisierung eine zweistufige Bereitstellung vorsehen, könnte die [Azure-zu-Azure-Notfallwiederherstellung](/azure/site-recovery/azure-to-azure-architecture) eine akzeptable Lösung sein. In diesem Szenario wird die Workload mithilfe eines Entwurfs mit einem einzelnen Site Recovery-Tresor und Konfigurations- oder Prozessserver zum ersten Azure-Rechenzentrum migriert. Nachdem die Workload getestet wurde, kann sie aus den migrierten Assets in einem zweiten Azure-Rechenzentrum wiederhergestellt werden. Diese Vorgehensweise reduziert die Auswirkungen auf Ressourcen im Quellrechenzentrum und profitiert von den höheren Übertragungsgeschwindigkeiten und den hohen Bandbreitenkapazitäten zwischen Azure-Rechenzentren.

> [!NOTE]
> Dieser Ansatz kann die kurzfristigen Migrationskosten durch zusätzliche Gebühren für Bandbreite für ausgehenden Datenverkehr erhöhen.

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Der Umgang mit der globalen Komplexität während der Optimierung und Höherstufung könnte in jeder der zusätzlichen Regionen doppelte Arbeit erfordern. Auch wenn eine einzelne Bereitstellung akzeptabel ist, müssen geschäftsbezogene Tests und Änderungspläne möglicherweise dennoch dupliziert werden.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Empfohlene Aktion während des Prozesses der Optimierung und Höherstufung

**Vorabtests der Optimierung** : Ein anfänglicher Test der Automatisierung kann potenzielle Optimierungschancen identifizieren – wie bei jedem Migrationsprojekt. Im Fall globaler Workloads testen Sie die Workload unabhängig in jeder Region. Kleine Konfigurationsänderungen im Netzwerk oder im Azure-Zielrechenzentrum können die Leistung beeinträchtigen.

**Geschäftsbezogene Änderungspläne** : Für komplexe Migrationsszenarios können Sie einen geschäftsbezogenen Änderungsplan erstellen. Dieser sorgt für eine klare Kommunikation jeglicher Änderungen an Geschäftsprozessen, der Servicequalität für Benutzer und des Zeitaufwands für die Integration der Änderungen. Im Fall von globalen Migrationsprojekten sollte der Änderungsplan Endbenutzer in jeder betroffenen Geografie berücksichtigen.

**Geschäftsbezogene Tests** : Zusammen mit dem geschäftsbezogenen Änderungsplan sind geschäftsbezogene Tests möglicherweise für jede Region erforderlich. So kann eine angemessene Leistung und eine Anpassung an die geänderten Netzwerkroutingmuster gewährleistet werden.

**Höherstufung in Gruppen** : Häufig erfolgt die Höherstufung als Einzelaktivität, und der Produktionsdatenverkehr wird an die migrierten Workloads umgeleitet. Im Fall von globalen Releases empfiehlt es sich, die Höherstufung in Flights (vordefinierte Benutzergruppen) durchzuführen. So können das Cloudstrategieteam und das Cloudeinführungsteam die Leistung besser beobachten und die Unterstützung für die Benutzer in den einzelnen Regionen verbessern. Höher gestufte Gruppen werden häufig auf Netzwerkebene gesteuert, indem die Weiterleitung bestimmter IP-Adressbereiche von den Quell-Workloadassets zu den neu migrierten Assets geändert wird. Nachdem eine bestimmte Gruppe von Endbenutzern migriert wurde, ist die nächste an der Reihe.

**Optimierung der Gruppen** : Einer der Vorteile der Höherstufung in Gruppen besteht darin, dass detailliertere Beobachtungen und eine weitere Optimierung der bereitgestellten Assets möglich sind. Nach einer kurzen Zeit der Produktionsnutzung durch die erste Gruppe wird eine weitere Optimierung der migrierten Assets empfohlen, sofern die IT-Betriebsverfahren dies zulassen.
