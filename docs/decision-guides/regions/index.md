---
title: Leitfaden zur Entscheidungsfindung für Regionen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hier finden Sie Informationen zu Regionsoptionen für die Cloudplattform.
author: doodlemania2
ms.author: dermar
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 041e1ccaf6ec0e928b6868f4e8c90849c8d4dea8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224591"
---
# <a name="azure-regions"></a>Azure-Regionen

Azure besteht aus zahlreichen Regionen auf der ganzen Welt. Jede der [Azure-Regionen](https://azure.microsoft.com/global-infrastructure/regions) hat bestimmte Merkmale, weshalb die Wahl der zu verwendenden Region überaus wichtig ist.

1. **Verfügbare Dienste:** Welche Dienste in den jeweiligen Regionen bereitgestellt werden, hängt von zahlreichen Faktoren ab. Als Zielregion für die Workloadbereitstellung muss eine Region gewählt werden, die den gewünschten Dienst enthält. Unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services) erfahren Sie, welche Dienste in welcher Region verfügbar sind.
1. **Kapazität:** Jede Region hat eine maximale Kapazität. Für den Endbenutzer wird dies zwar in der Regel abstrahiert, es kann sich aber darauf auswirken, von welchen Abonnementarten unter welchen Umständen welche Arten von Diensten bereitgestellt werden können. Diese Kapazität ist nicht das Gleiche wie Abonnementkontingente. Falls Sie eine umfangreiche Datencentermigration zu Azure planen, informieren Sie sich ggf. bei Ihrem Azure-Vertreterteam oder -Kundenbetreuer vor Ort, ob eine Bereitstellung im gewünschten Umfang möglich ist.
1. **Einschränkungen:** In bestimmten Regionen unterliegt die Bereitstellung von Diensten gewissen Einschränkungen. Einige Regionen stehen beispielsweise nur als Sicherungs- oder Failoverziel zur Verfügung. Weitere wichtige Einschränkungen sind [Datenhoheitsanforderungen](https://azure.microsoft.com/global-infrastructure/geographies).
1. **Datenhoheit:** Es gibt spezifische dedizierte Regionen für spezifische unabhängige Entitäten. Zwar handelt es sich bei allen Regionen um Azure-Regionen, diese unabhängigen Regionen sind jedoch vollständig vom Rest von Azure isoliert, werden nicht notwendigerweise von Microsoft verwaltet und können Einschränkungen hinsichtlich des Kundentyps unterliegen. Diese unabhängigen Regionen sind:
    1. [Azure China](https://azure.microsoft.com/global-infrastructure/china)
    1. [Azure Deutschland](https://azure.microsoft.com/global-infrastructure/germany) (Einstellung zugunsten deutscher Azure-Standardregionen (nicht unabhängig))
    1. [Azure US Government](https://azure.microsoft.com/global-infrastructure/government)
    1. Hinweis: Es gibt zwei Regionen in [Australien](https://azure.microsoft.com/global-infrastructure/australia), die zwar von Microsoft verwaltet, aber für die australische Regierung und ihre Kunden und Auftragnehmer bereitgestellt werden. Für diese beiden Regionen gelten daher ähnliche Clienteinschränkungen wie für die anderen Sovereign Clouds.

## <a name="operating-in-multiple-geographic-regions"></a>Agieren in mehreren geografischen Regionen

Wenn Unternehmen in mehreren geografischen Regionen agieren, ist das zwar grundlegend für die Resilienz, kann aber die Komplexität erhöhen. Diese Komplexität betrifft hauptsächlich vier Bereiche:

- Ressourcenverteilung
- Benutzerzugriffsprofile
- Complianceanforderungen
- Regionale Resilienz

Bei näherer Betrachtung der obigen Komplexitäten wird deutlich, wie wichtig die Regionsauswahl für Ihre Cloudeinführungsstrategie ist. Beginnen wir mit Überlegungen zum Netzwerk.

## <a name="networking-considerations"></a>Überlegungen zum Netzwerkbetrieb

Jede robuste Cloudbereitstellung ist auf ein sorgfältig durchdachtes Netzwerk angewiesen, wobei auch Azure-Regionen eine Rolle spielen. Nach Berücksichtigung der obigen Kriterien für die Wahl der Bereitstellungsregionen muss das Netzwerk bereitgestellt werden. Eine umfassende Besprechung des Netzwerks würde den Rahmen dieses Artikels sprengen, es sind jedoch unter anderem folgende Punkte zu beachten:

1. Azure-Regionen werden paarweise bereitgestellt. Für den Fall eines schwerwiegenden Ausfalls einer Region wird eine andere Region innerhalb der gleichen geopolitischen Grenze* als gekoppelte Region festgelegt. Die Bereitstellung in Regionspaaren sollte als primäre und sekundäre Resilienzstrategie in Erwägung gezogen werden. *Azure Brasilien ist eine erwähnenswerte Ausnahme, da die gekoppelte Region in diesem Fall „USA, Süden-Mitte“ ist. Weitere Informationen finden Sie [hier](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions).
    1. Azure Storage unterstützt [georedundanten Speicher (GRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs). Das bedeutet, dass drei Kopien Ihrer Daten in Ihrer primären Region und drei zusätzliche Kopien in der gekoppelten Region gespeichert werden. Die Speicherkopplung für GRS kann nicht geändert werden.
    1. Dienste, die auf Azure Storage-GRS basieren, können von dieser Regionskopplung profitieren. Ihre Anwendungen und das Netzwerk müssen dazu entsprechend ausgerichtet sein.
    1. Falls Sie GRS nicht für Ihre regionalen Resilienzanforderungen nutzen möchten, wird davon _abgeraten_, die gekoppelte Region als sekundäre Region zu verwenden. Ein regionaler Ausfall hat aufgrund der Ressourcenmigration eine hohe Auslastung der Ressourcen in der gekoppelten Region zur Folge. Die Umgehung dieser hohen Auslastung kann Ihnen einen Geschwindigkeitsvorteil bei der Wiederherstellung verschaffen, wenn Sie für die Wiederherstellung einen alternativen Standort nutzen.
    > [!WARNING]
    > Verwenden Sie Azure-GRS nicht für VM-Sicherungen oder -Wiederherstellungen. Nutzen Sie stattdessen [Azure Backup](https://azure.microsoft.com/services/backup) und [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery) in Kombination mit [Managed Disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview), um die Resilienz Ihrer IaaS-Workloads zu unterstützen.
2. Azure Backup und Azure Site Recovery arbeiten mit Ihrem Netzwerkentwurf zusammen, um regionale Resilienz für Ihre IaaS- und Datensicherungsanforderungen bereitzustellen. Stellen Sie sicher, dass das Netzwerk optimiert ist, damit Datenübertragungen ausschließlich über den Microsoft-Backbone abgewickelt werden, und verwenden Sie nach Möglichkeit [VNET-Peering](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview). Größere Organisationen mit globalen Bereitstellungen können für regionsübergreifendes Routing stattdessen [ExpressRoute Premium](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) nutzen, um regionale Gebühren für ausgehenden Datenverkehr zu sparen.
3. Azure-Ressourcengruppen sind regionsspezifische Konstrukte. Es ist jedoch normal, dass sich Ressourcen in einer Ressourcengruppe über mehrere Regionen erstrecken. Berücksichtigen Sie in diesem Fall, dass bei einem regionalen Ausfall Vorgänge der Steuerungsebene für eine Ressourcengruppe in der betroffenen Region nicht erfolgreich sind, auch wenn die Ressourcen in anderen Regionen (innerhalb dieser Ressourcengruppe) weiterhin aktiv sind. Dies kann sich sowohl auf Ihre Netzwerk- als auch auf Ihre Ressourcengruppengestaltung auswirken.
4. Viele PaaS-Dienste in Azure unterstützen [Dienstendpunkte](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) und/oder [Private Link](https://docs.microsoft.com/azure/private-link/private-link-overview). Beide Lösungen haben erhebliche Auswirkungen auf Ihre Netzwerküberlegungen im Zusammenhang mit regionaler Resilienz, Migration und Governance.
5. Viele PaaS-Dienste basieren auf eigenen Lösungen für regionale Resilienz. So ermöglicht beispielsweise Azure SQL-Datenbank eine problemlose Migration zu N zusätzlichen Regionen – ebenso wie CosmosDB. Einige Dienste, etwa Azure DNS, sind regionsunabhängig. Für Ihre Überlegungen hinsichtlich der Dienste, die Sie im Rahmen Ihres Einführungsprozess nutzen möchten, ist es wichtig, die genauen Failoverfunktionen und Wiederherstellungsschritte zu kennen, die ggf. für die jeweiligen Azure-Dienste erforderlich sind.
6. Neben der Bereitstellung in mehreren Regionen für die Notfallwiederherstellung entscheiden sich viele Organisationen für eine Bereitstellung mit Aktiv/Aktiv-Muster, sodass kein Failover erforderlich ist. Dies hat außerdem den Vorteil eines globalen Lastenausgleichs, einer höheren Fehlertoleranz und einer höheren Netzwerkleistung. Wenn Sie dieses Muster nutzen möchten, müssen Ihre Anwendungen die Aktiv/Aktiv-Ausführung in mehreren Regionen unterstützen.

> [!WARNING]
> Azure-Regionen sind hochverfügbare Konstrukte mit SLAs für die darin ausgeführten Dienste. Geschäftskritische Anwendungen sollten jedoch niemals von einer einzelnen Region abhängig sein. Planen Sie stets für regionale Ausfälle, und üben Sie Wiederherstellungs- und Problembehebungsschritte.

Nachdem Sie sich mit der Netzwerktopologie auseinandergesetzt haben, die zur Gewährleistung der Betriebsbereitschaft benötigt wird, sind zusätzliche Dokumentations- und Prozessabstimmungsschritte erforderlich. Anhand der folgenden Punkte können Sie die potenziellen Herausforderungen bewerten und eine allgemeine Vorgehensweise festlegen:

- Ziehen Sie eine stabilere Implementierung von Bereitschaft und Governance in Betracht.
- Erstellen Sie ein Inventar der betroffenen Geografien. Stellen Sie eine Liste der betroffenen Regionen und Länder zusammen.
- Dokumentieren Sie Anforderungen an die Datenhoheit: Liegen in den ermittelten Ländern Complianceanforderungen vor, die die Datenhoheit regulieren?
- Dokumentieren Sie die Benutzerbasis: Wird sich die Cloudmigration auf Mitarbeiter, Partner oder Kunden im ermittelten Land auswirken?
- Dokumentieren Sie Rechenzentren und Assets: Sind im ermittelten Land Assets vorhanden, die in das Migrationsprojekt aufgenommen werden sollten?
- Dokumentieren Sie die regionale SKU-Verfügbarkeit sowie Failoveranforderungen.

Stimmen Sie Änderungen im gesamten Migrationsprozess ab, um das anfängliche Inventar zu aktualisieren.

## <a name="documenting-complexity"></a>Dokumentieren der Komplexität

Die folgende Tabelle kann beim Dokumentieren der Ergebnisse aus den oben genannten Schritten helfen:

|Region  |Country  |Lokale Mitarbeiter  |Lokale externe Benutzer  |Lokale Rechenzentren oder Assets |Anforderungen an die Datenhoheit  |
|---------|---------|---------|---------|---------|---------|
|Nordamerika     |USA         |Ja         |Partner und Kunden         |Ja         |Nein         |
|Nordamerika     |Kanada         |Nein         |Kunden         |Ja         |Ja         |
|Europa     |Deutschland         |Ja         |Partner und Kunden         |Nein – nur Netzwerk         |Ja         |
|Asien-Pazifik     |Südkorea         |Ja         |Partner         |Ja         |Nein         |

<!-- markdownlint-disable MD026 -->

## <a name="data-sovereignty-relevancy"></a>Relevanz der Datenhoheit

Auf der ganzen Welt haben Organisationen damit begonnen, Anforderungen an die Datenhoheit zu etablieren, beispielsweise durch die Datenschutz-Grundverordnung (DSGVO). Complianceanforderungen dieser Art erfordern häufig einen Speicherort innerhalb einer bestimmten Region oder sogar innerhalb eines bestimmten Lands, um die Bürger dieses Lands zu schützen. In einige Fällen müssen Daten zu Kunden, Mitarbeitern oder Partnern auf einer Cloudplattform gespeichert werden, die sich in derselben Region befindet wie die Endbenutzer.

Diese Herausforderung ist ein wichtiger Beweggrund für Cloudmigrationen in Unternehmen, die auf globaler Ebene tätig sind. Um Complianceanforderungen zu erfüllen, haben einige Unternehmen sich dafür entschieden, duplizierte IT-Assets bei Cloudanbietern innerhalb einer Region bereitzustellen. In der Beispieltabelle oben ist Deutschland ein gutes Beispiel für dieses Szenario. In diesem Beispiel sind in Deutschland Kunden, Partner und Mitarbeiter vorhanden, aber keine IT-Assets. Hier kann sich das Unternehmen dafür entscheiden, einige Assets in einem Rechenzentrum innerhalb des DSGVO-Gebiets bereitzustellen, möglicherweise sogar in einem der deutschen Azure-Rechenzentren. Kenntnisse der Daten, für die die DSGVO gilt, würden dem Cloudeinführungsteam dabei helfen, den besten Migrationsansatz für diesen Fall zu ermitteln.

### <a name="why-is-the-location-of-end-users-relevant"></a>Warum ist der Standort von Endbenutzern relevant?

Unternehmen, die Endbenutzer in mehreren Ländern unterstützen, haben technische Lösungen zur Verarbeitung des Datenverkehrs von Endbenutzern entwickelt. In einigen Fällen umfasst dies die Speicherung von Assets innerhalb einer bestimmten Region oder eines bestimmten Lands. In anderen Szenarien entscheiden sich Unternehmen möglicherweise dazu, globale WAN-Lösungen zu implementieren, um die Anforderungen disparater Benutzergruppen über netzwerkzentrierte Lösungen zu erfüllen. In beiden Fällen können sich die Nutzungsprofile dieser disparaten Endbenutzergruppen auf die Migrationsstrategie auswirken.

Da das Unternehmen Mitarbeiter, Partner und Kunden in Deutschland unterstützt, dort derzeit aber nicht über Rechenzentren verfügt, ist es wahrscheinlich, dass dieses Unternehmen eine wie auch immer geartete Lösung mit geleasten Leitungen implementiert hat, um den Datenverkehr in andere Länder zu weiterzuleiten. Diese vorhandene Weiterleitung stellt ein erhebliches Risiko für die wahrgenommene Leistung der migrierten Anwendungen dar. Durch Hinzufügen zusätzlicher Hops zu einem etablierten und optimierten globalen WAN kann die Wahrnehmung entstehen, dass die Leistung von Anwendungen nach der Migration gesunken sei. Das Auffinden und Beheben solcher Probleme kann beträchtliche Verzögerungen für ein Projekt bedeuten. Jeder der unten genannten Prozesse umfasst Hinweise dazu, wie sich diese Komplexität bewältigen lässt – über Voraussetzungen sowie Bewertungs-, Migrations- und Optimierungsprozesse hinweg. Die Kenntnis der Benutzerprofile in den einzelnen Ländern ist sehr wichtig, um diese Komplexität zu bewältigen.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Warum ist der Standort von Rechenzentren relevant?

Der Standort vorhandener Rechenzentren kann eine Migrationsstrategie beeinflussen. Im Folgenden sind einige der häufigsten Auswirkungen aufgeführt:

**Architekturentscheidungen**: Das Festlegen von Zielregion bzw. Zielstandort ist einer der ersten Schritte beim Entwerfen einer Migrationsstrategie. Der Standort der vorhandenen Assets spielt dabei häufig eine Rolle. Darüber hinaus können die Verfügbarkeit von Clouddiensten und die Kosten pro Einheit für diese Dienste zwischen Regionen variieren. Daher spielt die Kenntnis des aktuellen und des zukünftigen Standorts von Assets eine Rolle bei Architekturentscheidungen und Budgetschätzungen.

**Abhängigkeiten zwischen Rechenzentren**: Basierend auf der oben stehenden Tabelle ist es wahrscheinlich, dass zwischen den verschiedenen Rechenzentren auf der ganzen Welt Abhängigkeiten bestehen. In vielen Unternehmen dieser Größenordnung sind diese Abhängigkeiten möglicherweise nicht sorgfältig dokumentiert oder werden nicht richtig verstanden. Die Vorgehensweisen, die zum Evaluieren von Benutzerprofilen verwendet werden, helfen dabei, einige dieser Abhängigkeiten zu identifizieren. Während des Bewertungsprozesses werden jedoch weitere Schritte vorgeschlagen, um die Risiken zu minimieren, die mit dieser Komplexität einhergehen.

## <a name="implementing-the-general-approach"></a>Implementieren der allgemeinen Vorgehensweise

Diese Vorgehensweise wird durch quantifizierbare Informationen gesteuert. Daher wird ein datengesteuertes Modell verwendet, um die Komplexität einer globalen Migration zu bewältigen.

Wenn der Umfang einer Migration mehrere Regionen umfasst, sollte das Cloudeinführungsteam folgende Überlegungen zur Bereitschaft berücksichtigen:

- Zur Sicherstellung der Datenhoheit müssen einige Assets möglicherweise an bestimmten Standorten bereitgestellt werden, es gibt aber viele Assets, für die diese Complianceeinschränkungen nicht gelten. Aspekte wie Protokollierung, Berichterstellung, Netzwerkrouting, Identität und weitere zentrale IT-Dienste können möglicherweise als freigegebene Dienste über mehrere Abonnements oder sogar Regionen hinweg gehostet werden. Es empfiehlt sich, dass das Cloudeinführungsteam für diese Dienste ein Freigabemodell evaluiert, wie in der [Referenzarchitektur für eine Hub-and-Spoke-Topologie mit freigegebenen Diensten](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) beschrieben.
- Wenn mehrere Instanzen ähnlicher Umgebungen bereitgestellt werden müssen, könnte eine Umgebungsfactory für Konsistenz sorgen, die Governance verbessern und die Bereitstellung beschleunigen. Die [Governance Journey für große Unternehmen](../../govern/guides/complex/index.md) etabliert eine Vorgehensweise, bei der eine Umgebung erstellt wird, die sich über mehrere Regionen hinweg skalieren lässt.

Sobald das Team mit dem grundlegenden Ansatz zufrieden und die Bereitschaft entsprechend vorhanden ist, müssen einige Voraussetzungen in Bezug auf die Daten berücksichtigt werden:

- **Allgemeine Ermittlung**: Füllen Sie die oben stehende Tabelle zum [Dokumentieren der Komplexität](#documenting-complexity) aus.
- **Durchführen einer Analyse der Benutzerprofile in jedem betroffenen Land**: Sie müssen die allgemeine Weiterleitung des Datenverkehrs von Endbenutzern bereits frühzeitig im Migrationsprozess kennen. Das Ändern globaler geleaster Leitungen und das Hinzufügen von Verbindungen wie ExpressRoute zu einem Cloudrechenzentrum kann die Netzwerkeinrichtung um Monate verzögern. Gehen Sie diesen Aspekt so früh wie möglich im Prozess an.
- **Anfängliche Bewertung des digitalen Eigentums**: Jedes Mal, wenn der Komplexitätsgrad einer Migrationsstrategie erhöht wird, sollte eine Bewertung des digitalen Eigentums durchgeführt werden. Unterstützung hierbei finden Sie in den Anleitungen zur [Bewertung des digitalen Eigentums](../../digital-estate/index.md).
  - **Weitere Anforderungen in Bezug auf das digitale Eigentum**: Richten Sie Kennzeichnungsrichtlinien ein, um alle Workloads zu ermitteln, die von Anforderungen an die Datenhoheit betroffen sind. Die Kennzeichnungspflicht sollte bei der Bewertung des digitalen Eigentums beginnen und bis zu den migrierten Assets beibehalten werden.
- **Evaluieren eines Hub-and-Spoke-Modells**: In verteilten Systemen existieren häufig allgemeine Abhängigkeiten. Diese Abhängigkeiten können häufig durch Implementierung eines Hub-and-Spoke-Modells verarbeitet werden. Ein solches Modell gehört nicht zum Umfang des Migrationsprozesses, sollte aber bei weiteren Iterationen der [Bereitschaftsprozesse](../../ready/index.md) Berücksichtigung finden.
- **Priorisierung des Migrationsbacklogs**: Wenn Netzwerkänderungen erforderlich sind, um die Produktionsbereitstellung einer Workload zu unterstützen, die mehrere Regionen unterstützt, muss das Cloudstrategieteam Eskalationen in Bezug auf diese Netzwerkänderungen nachverfolgen und verwalten. Die Unterstützung auf höherer Ebene der Unternehmenshierarchie hilft beim Beschleunigen der Änderung. Wichtiger ist jedoch, dass das Strategieteam die Möglichkeit erhält, das Backlog neu zu priorisieren, um sicherzustellen, dass globale Workloads nicht durch Netzwerkänderungen ausgebremst werden. Solche Workloads sollten erst priorisiert werden, nachdem die Netzwerkänderungen abgeschlossen sind.

Anhand dieser Voraussetzungen lassen sich Prozesse einrichten, mit denen diese Komplexität während der Umsetzung der Migrationsstrategie bewältigt werden kann.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Beim Umgang mit Komplexitäten in Zusammenhang mit globalen Assets und der globalen Benutzerbasis gibt es einige wichtige Aktivitäten, die bei der Bewertung von Migrationskandidaten ebenfalls ausgeführt werden sollten. Jede dieser Änderungen bringt durch eine datengesteuerte Vorgehensweise Klarheit hinsichtlich der Auswirkungen auf globale Benutzer und Assets.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

**Evaluieren von rechenzentrumsübergreifenden Abhängigkeiten**: Die [Tools für die Visualisierung von Abhängigkeiten in Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) helfen bei der Ermittlung von Abhängigkeiten. Die Verwendung dieser Tools vor der Migration ist eine allgemeine bewährte Methode. Wenn es aber um globale Komplexität geht, wird diese Verwendung zu einem notwendigen Schritt im Bewertungsprozess. Die Visualisierung durch die [Gruppierung von Abhängigkeiten](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) kann dabei helfen, die IP-Adressen und Ports aller Assets zu ermitteln, die zur Unterstützung der Workload erforderlich sind.

> [!IMPORTANT]
> Zwei wichtige Hinweise: Erstens muss ein Experte, der über Kenntnisse zu Assetplatzierung und IP-Adressschemas verfügt, Assets identifizieren, die sich in einem sekundären Rechenzentrum befinden. Zweitens müssen sowohl Downstreamabhängigkeiten als auch Clients in der Visualisierung evaluiert werden, um bidirektionale Abhängigkeiten zu verstehen.

**Erkennen der globalen Auswirkungen auf Benutzer**: Die Ergebnisse der Benutzerprofilanalyse sollten alle Workloads bezeichnen, die durch globale Benutzerprofile beeinflusst werden. Wenn sich ein Migrationskandidat auf der Liste der betroffenen Workloads befindet, sollte sich der Architekt, der die Migration vorbereitet, mit den Experten für Netzwerkfunktionen und Betrieb beraten, um Netzwerkrouting und Leistungserwartungen zu überprüfen. Eine Mindestanforderung ist, dass die Architektur eine ExpressRoute-Verbindung zwischen dem nächstgelegenen Netzwerkbetriebszentrum und Azure umfasst. Die [Referenzarchitektur für ExpressRoute-Verbindungen](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute) kann bei der Konfiguration der notwendigen Verbindung helfen.

**Entwurf im Hinblick auf die Compliance**: Die Ergebnisse der Benutzerprofilanalyse sollten alle Workloads bezeichnen, die durch Anforderungen hinsichtlich der Datenhoheit beeinflusst werden. Während der architekturbezogenen Aktivitäten des Bewertungsprozesses sollte der zuständige Architekt Complianceexperten konsultieren, um alle Anforderungen für die Migration bzw. Bereitstellung über mehrere Regionen hinweg zu verstehen. Diese Anforderungen haben erhebliche Auswirkungen auf Entwurfsstrategien. Die Referenzarchitekturen für [Webanwendungen in mehreren Regionen](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) und [n-schichtige Anwendungen in mehreren Regionen](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) können beim Entwurf hilfreich sein.

> [!WARNING]
> Bei Verwendung einer der gerade genannten Referenzarchitekturen müssen möglicherweise bestimmte Datenelemente von Replikationsprozessen ausgeschlossen werden, um Datenhoheitsanforderungen zu erfüllen. Dadurch wird ein weiterer Schritt zum Prozess der Höherstufung hinzugefügt.

## <a name="migrate-process-changes"></a>Änderungen am Migrationsprozess

Beim Migrieren einer Anwendung, die in mehreren Regionen bereitgestellt werden muss, muss das Cloudeinführungsteam einige Überlegungen berücksichtigen. Hierzu gehören der Entwurf des Azure Site Recovery-Tresors, des Konfigurations-/Prozessservers, der Netzwerkbandbreite sowie die Datensynchronisierung.

### <a name="suggested-action-during-the-migrate-process"></a>Empfohlene Aktion während des Migrationsprozesses

**Entwurf des Azure Site Recovery-Tresors**: Azure Site Recovery ist das empfohlene Tool für die cloudnative Replikation und Synchronisierung von digitalen Assets in Azure. Site Recovery repliziert Daten zum Asset in einen Site Recovery-Tresor, der an ein bestimmtes Abonnement in einer bestimmten Region und einem bestimmten Azure-Rechenzentrum gebunden ist. Beim Replizieren von Assets in eine zweite Region ist möglicherweise ein zweiter Site Recovery-Tresor erforderlich.

**Entwurf des Konfigurations-/Prozessservers**: Site Recovery arbeitet mit einer lokalen Instanz eines Konfigurations- und Prozessservers, die an einen einzelnen Site Recovery-Tresor gebunden ist. Das bedeutet, dass möglicherweise eine zweite Instanz dieser Server im Quellrechenzentrum installiert werden muss, um die Replikation zu ermöglichen.

**Entwurf der Netzwerkbandbreite**: Während der Replikation und der fortlaufenden Synchronisierung werden binäre Daten über das Netzwerk vom Quellrechenzentrum zum Site Recovery-Tresor im Azure-Zielrechenzentrum verschoben. Dieser Prozess verbraucht Bandbreite. Die Duplizierung der Workload in eine zweite Region verdoppelt die verbrauchte Bandbreitenmenge. Wenn die Bandbreite begrenzt ist oder eine Workload ein hohes Maß an Konfiguration oder Datenabweichung beinhaltet, kann dies zu Konflikten hinsichtlich des Zeitraums führen, der für den Abschluss der Migration erforderlich ist. Wichtiger noch: Es könnte sich auf das Benutzererlebnis oder die Anwendungsleistung auswirken, wenn Benutzer bzw. Anwendungen noch auf die Bandbreite des Quellrechenzentrums angewiesen sind.

**Datensynchronisierung**: Häufig wird die Bandbreite bei der Synchronisierung der Datenplattform am meisten beansprucht. Wie in den Referenzarchitekturen für [Webanwendungen in mehreren Regionen](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) und [n-schichtige Anwendungen in mehreren Regionen](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) definiert, ist eine Synchronisierung der Daten häufig erforderlich, um die Anwendungen auf dem gleichen Stand zu halten. Wenn dies der gewünschte Betriebszustand der Anwendung ist, kann es klug sein, eine vollständige Synchronisierung zwischen der Quelldatenplattform und den einzelnen Cloudplattformen durchzuführen, bevor die Anwendung und die Assets der mittleren Schicht migriert werden.
**Datensynchronisierung**: Häufig wird die Bandbreite bei der Synchronisierung der Datenplattform am meisten beansprucht. Wie in den Referenzarchitekturen für [Webanwendungen in mehreren Regionen](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) und [n-schichtige Anwendungen in mehreren Regionen](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) definiert, ist eine Synchronisierung der Daten häufig erforderlich, um die Anwendungen auf dem gleichen Stand zu halten. Wenn dies der gewünschte Betriebszustand der Anwendung ist, kann es klug sein, eine vollständige Synchronisierung zwischen der Quelldatenplattform und den einzelnen Cloudplattformen durchzuführen, bevor die Anwendung und die Assets der mittleren Schicht migriert werden.

**Azure-zu-Azure-Notfallwiederherstellung**: Es gibt eine alternative Option, die die Komplexität weiter verringern kann. Wenn Zeitpläne und Datensynchronisierung eine zweistufige Bereitstellung vorsehen, könnte die [Azure-zu-Azure-Notfallwiederherstellung](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-architecture) eine akzeptable Lösung sein. In diesem Szenario wird die Workload mithilfe eines Entwurfs mit einem einzelnen Site Recovery-Tresor und Konfigurations- oder Prozessserver zum ersten Azure-Rechenzentrum migriert. Sobald die Workload getestet wurde, kann sie aus den migrierten Assets in einem zweiten Azure-Rechenzentrum wiederhergestellt werden. Diese Vorgehensweise reduziert die Auswirkungen auf Ressourcen im Quellrechenzentrum und profitiert von den höheren Übertragungsgeschwindigkeiten und den hohen Bandbreitenkapazitäten zwischen Azure-Rechenzentren.

> [!NOTE]
> Dadurch können die kurzfristigen Migrationskosten steigen, da dieses Verfahren zusätzliche Kosten für ausgehende Bandbreite verursachen kann.

## <a name="optimize-and-promote-process-changes"></a>Änderungen an Prozessen zum Optimieren und Höherstufen

Der Umgang mit der globalen Komplexität während der Optimierung und Höherstufung könnte in jeder der zusätzlichen Regionen doppelte Arbeit erfordern. Auch wenn eine einzelne Bereitstellung akzeptabel ist, müssen geschäftsbezogene Tests und Änderungspläne möglicherweise dennoch dupliziert werden.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Empfohlene Aktion während des Prozesses der Optimierung und Höherstufung

**Vorabtests der Optimierung**: Ein anfänglicher Test der Automatisierung kann potenzielle Optimierungschancen identifizieren – wie bei jedem Migrationsprojekt. Im Fall von globalen Workloads ist es wichtig, diese unabhängig in jeder Region zu testen, da sich kleine Konfigurationsänderungen im Netzwerk oder dem Azure-Zielrechenzentrum auf die Leistung auswirken können.

**Geschäftsbezogene Änderungspläne**: Bei allen komplexen Migrationsszenarien empfiehlt es sich, einen geschäftsbezogenen Änderungsplan zu erstellen, um eine eindeutige Kommunikation zu Änderungen an Geschäftsprozessen, Benutzeroberflächen und zur zeitlichen Planung der Integration der Änderungen sicherzustellen. Im Fall von globalen Migrationsprojekten sollte der Änderungsplan Endbenutzer in jeder betroffenen Geografie berücksichtigen.

**Geschäftsbezogene Tests**: Zusammen mit dem Plan der geschäftsbezogenen Änderungen müssen möglicherweise in jeder Region geschäftsbezogene Tests durchgeführt werden, um eine angemessene Leistung sowie die Einhaltung der geänderten Weiterleitungsmuster im Netzwerk sicherzustellen.

**Höherstufung in Gruppen**: Häufig erfolgt die Höherstufung als Einzelaktivität, und der Produktionsdatenverkehr wird an die migrierten Workloads umgeleitet. Im Fall von globalen Releases empfiehlt es sich, die Höherstufung in Gruppen (vordefinierte Benutzergruppen) durchzuführen. So können das Cloudstrategieteam und das Cloudeinführungsteam die Leistung besser beobachten und die Unterstützung für die Benutzer in den einzelnen Regionen verbessern. Höher gestufte Gruppen werden häufig auf Netzwerkebene gesteuert, indem die Weiterleitung bestimmter IP-Adressbereiche von den Quell-Workloadassets zu den neu migrierten Assets geändert wird. Nachdem eine bestimmte Gruppe von Endbenutzern migriert wurde, ist die nächste an der Reihe.

**Optimierung der Gruppen**: Einer der Vorteile der Höherstufung in Gruppen besteht darin, dass detailliertere Beobachtungen und eine weitere Optimierung der bereitgestellten Assets möglich sind. Nach einer kurzen Zeit der Produktionsnutzung durch die erste Gruppe wird eine weitere Optimierung der migrierten Assets empfohlen, sofern die IT-Betriebsverfahren dies zulassen.
