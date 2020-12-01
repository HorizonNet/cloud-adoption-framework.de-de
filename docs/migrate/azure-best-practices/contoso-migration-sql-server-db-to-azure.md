---
title: Migrieren von SQL Server-Datenbanken zu Azure
description: In diesem Artikel erfahren Sie, wie Contoso seine lokalen SQL-Datenbanken zu Azure migriert hat.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 733216e9e8a4bca165c1bc73a1fd1870ecba8d3a
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879224"
---
<!-- cSpell:ignore BACPAC FILESTREAM -->

# <a name="migrate-sql-server-databases-to-azure"></a>Migrieren von SQL Server-Datenbanken zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso verschiedene lokale SQL Server-Datenbanken bewertet hat und die Migration zu Azure geplant und ausgeführt hat.

Contoso erwägt die Migration zu Azure und muss anhand einer technischen und finanziellen Bewertung ermitteln, ob seine lokalen Workloads gute Kandidaten für die Cloudmigration sind. Das Contoso-Team möchte vor allem die Computer- und Datenbankkompatibilität für die Migration bewerten. Außerdem sollen die Kapazität und die Kosten für die Ausführung der Ressourcen von Contoso in Azure geschätzt werden.

## <a name="business-drivers"></a>Business-Treiber

Bei Contoso treten mehrere Probleme bei der Verwaltung der verschiedenen Versionen von SQL Server-Workloads auf, die im Netzwerk vorhanden sind. Nach dem letzten Meeting der Investoren haben der CFO und der CTO entschieden, alle diese Workloads zu Azure zu migrieren. Dies ermöglicht Contoso den Wechsel von einem strukturierten Investitionskostenmodell zu einem fließenden Betriebskostenmodell.

Das IT-Führungsteam arbeitet eng mit Geschäftspartnern zusammen, um die Geschäfts- und technischen Anforderungen genau zu verstehen:

- **Sicherheit erhöhen:** Contoso muss in der Lage sein, alle Datenressourcen zeitgerecht und effizient zu überwachen und zu schützen. Außerdem soll ein zentralisierteres Berichtssystem für Datenbankzugriffsmuster eingerichtet werden.

- **Computeressourcen optimieren:** Contoso hat eine umfassende lokale Serverinfrastruktur bereitgestellt. Sie verfügen über mehrere SQL Server-Instanzen, die die zugrunde liegende CPU, den Arbeitsspeicher und den zugewiesenen Datenträger zwar nutzen, allerdings nicht wirklich effizient.

- **Effizienz steigern:** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten. Datenbankverwaltungsaufgaben sollten nach der Migration auf ein Minimum reduziert sein.

- **Flexibilität steigern:** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Es darf nicht im Weg stehen oder zum Geschäftshindernis werden.

- **Skalierung**: Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können. Es gibt mehrere ältere Hardwareumgebungen, für die kein Upgrade mehr durchgeführt werden kann und deren Support abgelaufen ist oder kurz vor dem Ende steht.

- **Kosten:** Geschäftsinhaber und Anwendungsbesitzer möchten sicher sein, dass im Vergleich zur lokalen Ausführung der Anwendungen keine hohen Cloudkosten auf sie zukommen.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die verschiedenen Migrationen gesetzt. Anhand dieser Ziele werden die besten Migrationsmethoden bestimmt.

| Anforderungen | Details |
| --- | --- |
| **Leistung** | Nach der Migration sollten die Anwendungen in Azure die gleichen Leistungsmerkmale aufweisen, über die sie in der lokalen Umgebung von Contoso derzeit verfügen. Die Umstellung auf die Cloud bedeutet nicht, dass die Leistung der Anwendung weniger wichtig ist. |
| **Kompatibilität** | Contoso muss die Kompatibilität seiner Anwendungen und Datenbanken mit Azure verstehen. Außerdem muss Contoso mit den Hostingoptionen in Azure vertraut sein. |
| **Datenquellen** | Alle Datenbanken werden ohne Ausnahme zu Azure verschoben. Basierend auf den Datenbank- und Anwendungsanalysen der verwendeten SQL-Features werden sie zu PaaS, IaaS oder verwalteten Instanzen migriert. Alle Datenbanken müssen verschoben werden. |
| **Anwendung** | Anwendungen müssen wo möglich in die Cloud verschoben werden. Wenn sie nicht verschoben werden können, ist es möglich, dass sie über das Netzwerk von Azure ausschließlich über private Verbindungen eine Verbindung zur migrierten Datenbank herstellen. |
| **Kosten** | Contoso möchte nicht nur verstehen, welche Migrationsoptionen verfügbar sind, sondern auch über die Infrastrukturkosten nach der Verlagerung in die Cloud Bescheid wissen. |
| **Verwaltung** | Für die verschiedenen Abteilungen müssen Ressourcenverwaltungsgruppen sowie Ressourcengruppen erstellt werden, um alle migrierten SQL-Datenbanken zu verwalten. Alle Ressourcen müssen aus Gründen der verbrauchsbasierten Kostenzuteilung mit Tags mit Abteilungsinformationen versehen werden. |
| **Einschränkungen** | Zu Beginn verfügen nicht alle Zweigstellen, die Anwendungen ausführen, über einen direkten ExpressRoute-Link zu Azure. Diese Zweigstellen müssen also eine Verbindung über virtuelle Netzwerkgateways herstellen. |

## <a name="solution-design"></a>Lösungsentwurf

Contoso hat bereits eine [Migrationsbewertung](../..//plan/contoso-migration-assessment.md) für seine digitalen Ressourcen mithilfe von [Azure Migrate](/azure/migrate/migrate-services-overview) durchgeführt.

Die Bewertung ergibt mehrere Workloads, die auf mehrere Abteilungen verteilt sind. Die Gesamtgröße des Migrationsprojekts erfordert ein gesamtes Projektmanagementbüro, das die Besonderheiten der Kommunikation, der Ressourcen und der Zeitplanung verwaltet.

![Migrationsprozess](./media/contoso-migration-sql-server-db-to-azure/migration-process.png)

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Azure stellt eine zentralisierte Benutzeroberfläche für die Datenbankworkloads bereit. <br><br> Die Kosten können über Azure Cost Management und Abrechnung überwacht werden. <br><br> Dank der Azure-Abrechnungs-APIs ist eine Abrechnung mit verbrauchsbasierter Kostenzuteilung einfach durchzuführen. <br><br> Die Server- und Softwarewartung kann auf die IaaS-basierten Umgebungen reduziert werden. |
| **Nachteile** | Aufgrund der Anforderung IaaS-basierter virtueller Computer muss die Software auf diesen Computern weiterhin verwaltet werden. |

### <a name="budget-and-management"></a>Budget und Verwaltung

Vor der Migration muss die erforderliche Azure-Struktur vorhanden sein, damit die Verwaltungs- und Abrechnungsaspekte der Lösung unterstützt werden können.

Für die Verwaltungsanforderungen wurden mehrere [Verwaltungsgruppen](/azure/governance/management-groups/overview) erstellt, um die Organisationsstruktur unterstützen zu können.

Für die Abrechnungsanforderungen werden alle Azure-Ressourcen mit entsprechenden [Abrechnungstags](/azure/azure-resource-manager/management/tag-resources) versehen.

### <a name="migration-process"></a>Migrationsprozess

Datenmigrationen folgen einem wiederholbaren Standardmuster. Dazu gehören die folgenden Schritte, die den [bewährten Methoden von Microsoft](https://datamigration.microsoft.com/) entsprechen:

- Vor der Migration:
  - **Ermittlung:** Ressourcen der Inventardatenbank und Anwendungsstapel
  - **Bewerten:** Bewerten der Workloads und Erstellen von Empfehlungen
  - **Konvertieren:** Konvertieren des Quellschemas, damit es im Ziel verwendet werden kann
- Migration:
  - **Migrieren:** Migrieren des Quellschemas, der Quelldaten und der Objekte in das Ziel
  - **Synchronisieren der Daten:** Synchronisieren der Daten, damit die Downtime möglichst gering ist
  - **Umstellung:** Umstellen der Quelle auf das Ziel
- Nach der Migration:
  - **Anpassen der Anwendungen:** Iteratives Vornehmen erforderlicher Änderungen an den Anwendungen
  - **Durchführen von Tests:** Iteratives Durchführen von Funktions- und Leistungstests
  - **Optimieren:** Auf den Tests basierende Behebung von Leistungsproblemen und Durchführen von erneuten Tests zur Bestätigung vorgenommener Leistungsverbesserungen
  - **Außerbetriebnahme von Ressourcen:** Sicherung und Außerbetriebnahme alter VMs und Hostingumgebungen

#### <a name="step-1-discovery"></a>Schritt 1: Ermittlung

Contoso hat Azure Migrate verwendet, um die Abhängigkeiten in der Contoso-Umgebung offenzulegen. Mithilfe von Azure Migrate können Anwendungskomponenten in Windows- und Linux-Systemen automatisch erkannt und die Kommunikation zwischen Diensten zugeordnet werden. Mithilfe von Azure Migrate wurden auch die Verbindungen zwischen Contoso-Servern, Prozessen, der Latenz zwischen eingehenden und ausgehenden Verbindungen und Ports in der über TCP verbundenen Architektur offengelegt.

Außerdem fügte Contoso seinem Azure Migrate-Projekt den Datenmigrations-Assistenten hinzu. Durch Auswahl dieses Tools können die Datenbanken für die Migration zu Azure bewertet werden.

![Datenmigrations-Assistent](./media/contoso-migration-sql-server-db-to-azure/add-dma.png)

#### <a name="step-2-application-assessment"></a>Schritt 2: Anwendungsbewertung

<!-- docutune:casing "mainly .NET-based" "non-.NET-based" -->

Durch die Ergebnisse der Bewertung erfuhr Contoso, dass das Unternehmen hauptsächlich NET-basierte Anwendungen nutzt. Im Laufe der Jahre wurden bei verschiedenen Projekten jedoch auch andere Technologien wie PHP und Node.js verwendet. Durch von einem Anbieter erworbene Systeme wurden auch Nicht-.NET-basierte Anwendungen eingeführt. Es wurde Folgendes ermittelt:

- ~800 Windows .NET-Anwendungen
- ~50 PHP-Anwendungen
- 25 Node.js-Anwendungen
- 10 Java-Anwendungen

#### <a name="step-3-database-assessment"></a>Schritt 3: Datenbankbewertung

Bei der Ermittlung der einzelnen Datenbankworkloads wurde der Datenmigrations-Assistent (DMA-Tool) ausgeführt, um zu bestimmen, welche Features verwendet wurden. Das DMA-Tool hilft Contoso bei der Bewertung seiner Datenmigrationen zu Azure, indem Kompatibilitätsprobleme erkannt werden, die die Datenbankfunktionalität in einer neuen Version von SQL Server oder Azure SQL-Datenbank beeinträchtigen können.

Contoso führte die folgenden Schritte aus, um die Datenbanken zu bewerten und anschließend Ergebnisdaten in Azure Migrate hochzuladen:

1. DMA herunterladen
1. Bewertungsprojekt erstellen
1. In DMA beim Azure Migrate-Projekt anmelden und Bewertungszusammenfassung synchronisieren

![Azure Migrate und DMA](./media/contoso-migration-sql-server-db-to-azure/azure-migrate-dma.png)

DMA empfiehlt Leistungs- und Zuverlässigkeitsverbesserungen für die Zielumgebung und ermöglicht es, Schema, Daten und abhängige Objekte von einem Quellserver auf einen Zielserver zu verschieben.

Erfahren Sie mehr über den [Datenmigrations-Assistenten](/sql/dma/dma-assesssqlonprem?view=sql-server-2017).

Contoso hat den Assistenten zum Ausführen der Bewertung verwendet und dann die Daten direkt in Azure Migrate hochgeladen.

![Hochladen von DMA in Azure Migrate](./media/contoso-migration-sql-server-db-to-azure/upload-db-data.png)

Anhand der jetzt in Azure Migrate hochgeladenen Informationen konnte Contoso mehr als 1.000 Datenbankinstanzen identifizieren, die migriert werden müssen. Von diesen Instanzen können etwa 40 Prozent in eine SQL-Datenbank für Azure verschoben werden. Die verbleibenden 60 Prozent müssen entweder in SQL Server auf Azure Virtual Machines oder in Azure SQL Managed Instance verschoben werden. Von diesen 60 Prozent erfordern ungefähr 10 Prozent einen VM-basierten Ansatz. Die verbleibenden Instanzen werden in Azure SQL Managed Instance verschoben.

Wenn DMA für eine Datenquelle nicht ausgeführt werden konnte, wurden die folgenden Richtlinien für die Datenbankmigrationen befolgt.

> [!NOTE]
> Im Rahmen der Bewertungsphase wurden von Contoso verschiedene Open-Source-Datenbanken ermittelt. Für deren Migrationsplanung wurde separat [Migration von Open-Source-Datenbanken zu Azure](./contoso-migration-oss-db-to-azure.md) gefolgt.

<!-- docutune:casing "custom .NET" -->

#### <a name="step-4-migration-planning"></a>Schritt 4: Migrationsplanung

Contoso bestimmt auf Grundlage der vorliegenden Informationen und anhand der folgenden Richtlinien, welche Migrationsmethode für die einzelnen Datenbanken zu verwenden ist.

| Ziel | Datenbanknutzung | Details | Onlinemigration | Offlinemigration | Max. Größe | Migrationsleitfaden |
| --- | --- | --- | --- | ---| --- | --- |
| Azure SQL-Datenbank (PaaS) | SQL Server (nur Daten) | Diese Datenbanken verwenden lediglich einfache Tabellen, Spalten, gespeicherte Prozeduren und Funktionen. | [Datenmigrations-Assistent](/sql/dma/dma-overview), [Transaktionsreplikation](/azure/sql-database/sql-database-managed-instance-transactional-replication) | [BACPAC](/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database), [bcp](/sql/tools/bcp-utility?view=sql-server-ver15) | 1 TiB | [Link](/azure/dms/tutorial-sql-server-to-azure-sql) |
| Verwaltete Azure SQL-Instanz | SQL Server (erweiterte Features) | Diese Datenbanken verwenden Trigger und andere [erweiterte Konzepte](/azure/sql-database/sql-database-managed-instance-transact-sql-information#service-broker), z. B. benutzerdefinierte .NET-Typen, Service Broker usw. | [Datenmigrations-Assistent](/sql/dma/dma-overview), [Transaktionsreplikation](/azure/sql-database/sql-database-managed-instance-transactional-replication) | [BACPAC](/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database), [bcp](/sql/tools/bcp-utility?view=sql-server-ver15), [native Sicherung/Wiederherstellung](/azure/sql-database/sql-database-managed-instance-get-started-restore) | 2 TiB – 8 TiB | [Link](/azure/dms/tutorial-sql-server-managed-instance-online) |
| SQL Server auf Azure Virtual Machines (IaaS) | SQL Server (Drittanbieterintegrationen) | Der SQL Server muss über [nicht unterstützte SQL Managed Instance-Features](/azure/sql-database/sql-database-managed-instance-transact-sql-information#service-broker) (instanzübergreifende Service Broker, Kryptografieanbieter, Pufferpool, Kompatibilitätsgrade unter 100, Datenbankspiegelung, FILESTREAM, PolyBase, alles, was Zugriff auf Dateifreigaben erfordert, externe Skripts, erweiterte gespeicherte Prozeduren usw.) verfügen, oder es muss Drittanbietersoftware zur Unterstützung der Aktivitäten der Datenbank installiert sein. | [Transaktionsreplikation](/azure/sql-database/sql-database-managed-instance-transactional-replication) | [BACPAC](/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database), [bcp](/sql/tools/bcp-utility?view=sql-server-ver15), [Momentaufnahmereplikation](/azure/sql-database/sql-database-managed-instance-transactional-replication), [native Sicherung/Wiederherstellung](/azure/sql-database/sql-database-managed-instance-get-started-restore), Konvertieren des physischen Computers in eine VM | 4 GiB – 64 TiB | [Link](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql) |

Aufgrund der großen Anzahl der Datenbanken richtete Contoso ein Projektmanagementbüro ein, das den Überblick über die einzelnen Datenbankmigrationsinstanzen behalten sollte. Jedem Unternehmens- und Anwendungsteam wurden [Zuständigkeiten und Verantwortlichkeiten](../..//migrate/migration-considerations/assess/index.md) zugewiesen.

Außerdem führte Contoso eine [Überprüfung der Workloads auf die jeweilige Migrationsbereitschaft](../..//migrate/migration-considerations/assess/evaluate.md) durch. Bei dieser Überprüfung wurden die Infrastruktur, die Datenbank und die Netzwerkkomponenten untersucht.

#### <a name="step-5-test-migrations"></a>Schritt 5: Testmigrationen

Zum ersten Teil der Migrationsvorbereitung gehörte eine Testmigration der einzelnen Datenbanken in die bereits eingerichteten Umgebungen. Aus Zeitersparnisgründen wurden Skripts für alle Migrationsvorgänge erstellt und die jeweilige Dauer aufgezeichnet. Zur Beschleunigung der Migration wurde untersucht, welche Migrationsvorgänge gleichzeitig ausgeführt werden könnten.

Außerdem wurden Rollbackverfahren für die einzelnen Datenbankworkloads herausgearbeitet, sollten unerwartete Fehler auftreten.

Für die IaaS-basierten Workloads wurde vorab sämtliche erforderliche Drittanbietersoftware eingerichtet.

Nach der Testmigration konnte Contoso die verschiedenen [Tools für die Kostenschätzung](../..//migrate/migration-considerations/assess/estimate.md) von Azure verwenden, um ein genaueres Bild der zukünftigen Betriebskosten für die Migration zu erhalten.

#### <a name="step-6-migration"></a>Schritt 6: Migration

Für die Produktionsmigration arbeitete Contoso Zeitrahmen für alle Datenbankmigrationen heraus und untersuchte, welcher Umfang innerhalb des zeitlichen Rahmens eines Wochenendes (Freitag Mitternacht bis Sonntag Mitternacht) mit minimaler Ausfallzeit für das Unternehmen durchgeführt werden könnte.

Basierend auf den dokumentierten Testverfahren wird jede Migration so weit wie möglich über Skripts ausgeführt, wobei manuelle Aufgaben zur Minimierung von Fehlern eingeschränkt werden.

Wenn Migrationen während des Zeitfensters fehlschlagen, wird ein Rollback ausgeführt und die Migrationen werden im nächsten Migrationsfenster neu geplant.

### <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Contoso hat das Archivierungsfenster für alle Datenbankworkloads identifiziert. Wenn das Fenster abläuft, werden die Ressourcen aus der lokalen Infrastruktur genommen.

Dies schließt Folgendes ein:

- Entfernen der Produktionsdaten von lokalen Servern
- Außerbetriebnahme des Hostservers nach Ablauf des letzten Workloadfensters

### <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

#### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neuen Datenbankworkloads in Azure geschützt sind. [Weitere Informationen](/azure/sql-database/sql-database-security-overview)
- Insbesondere sollte Contoso die Konfiguration der Firewall und des virtuellen Netzwerks überprüfen.
- Contoso sollte [Private Link](/azure/azure-sql/database/private-endpoint-overview) einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte [Azure Advanced Threat Protection](/azure/azure-sql/database/threat-detection-overview) für Azure SQL-Datenbank aktivieren.

#### <a name="backups"></a>Backups

- Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Datenbanken in Azure gesichert sind. Mit dieser Funktion können Sicherungen erstellt werden, die im Fall eines regionalen Ausfalls in einer gekoppelten Region verfügbar sind.
- **Wichtig:** Stellen Sie sicher, dass die Azure-Ressource über eine [Ressourcensperre](/azure/azure-resource-manager/management/lock-resources) verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

#### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Viele Azure-Datenbankworkloads können zentral hoch- oder herunterskaliert werden. Daher ist die Leistungsüberwachung von Server und Datenbanken wichtig, um sicherzustellen, dass die Anforderungen erfüllt und gleichzeitig die Kosten möglichst gering gehalten werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Sie können zwischen verschiedenen Tarifen wählen. Achten Sie darauf, dass ein passender Tarif für die Datenworkloads ausgewählt ist.
- [Pools für elastische Datenbanken](/azure/sql-database/sql-database-service-tiers-dtu) müssen für Datenbanken implementiert werden, die über kompatible Ressourcenauslastungsmuster verfügen.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.
- Verwenden Sie reservierte Kapazitäten, um Kosten zu sparen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde gezeigt, wie Contoso seine Microsoft SQL Server-Workloads bewertet hat und die Migration zu Azure geplant und ausgeführt hat.  
Außerdem wurde ein Azure DevOps-Projekt für Ihre SQL-Migration entwickelt. Das Projekt wurde am Cloud Adoption Framework ausgerichtet. Es führt Sie Schritt für Schritt durch die wichtigsten erforderlichen Entscheidungen. [Klicken Sie hier](https://azuredevopsdemogenerator.azurewebsites.net/?name=sqlmigration), um zum Azure DevOps-Projekt zu gelangen. 