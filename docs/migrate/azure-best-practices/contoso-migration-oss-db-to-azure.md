---
title: Migration von Open-Source-Datenbanken zu Azure
description: In diesem Artikel erfahren Sie, wie das Unternehmen Contoso seine lokalen Open-Source-Datenbanken zu Azure migriert hat.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: d8b68e25f7cd52fc02037d64b79b282c816e41ec
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199217"
---
# <a name="migrate-open-source-databases-to-azure"></a>Migration von Open-Source-Datenbanken zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso verschiedene lokale Open-Source-Datenbanken bewertet hat und die Migration zu Azure geplant und ausgeführt hat.

Contoso erwägt die Migration zu Azure und muss anhand einer technischen und finanziellen Bewertung ermitteln, ob seine lokalen Workloads gute Kandidaten für die Cloudmigration sind. Das Contoso-Team möchte vor allem die Computer- und Datenbankkompatibilität für die Migration bewerten. Außerdem sollen die Kapazität und die Kosten für die Ausführung der Ressourcen von Contoso in Azure geschätzt werden.

## <a name="business-drivers"></a>Business-Treiber

Bei Contoso treten mehrere Probleme bei der Verwaltung der verschiedenen Versionen der Open-Source-Datenbankworkloads auf, die im Netzwerk vorhanden sind. Nach dem letzten Meeting der Investoren haben der CFO und der CTO entschieden, alle diese Workloads zu Azure zu migrieren. Dies ermöglicht Contoso den Wechsel von einem strukturierten Investitionskostenmodell zu einem fließenden Betriebskostenmodell.

Das IT-Führungsteam arbeitet eng mit Geschäftspartnern zusammen, um die Geschäfts- und technischen Anforderungen genau zu verstehen:

- **Sicherheit erhöhen:** Contoso muss in der Lage sein, alle Datenressourcen zeitgerecht und effizient zu überwachen und zu schützen. Außerdem soll ein zentralisierteres Berichtssystem für Datenbankzugriffsmuster eingerichtet werden.

- **Computeressourcen optimieren:** Contoso hat eine umfassende lokale Serverinfrastruktur bereitgestellt. Sie verfügen über mehrere SQL Server-Instanzen, die die zugrunde liegende CPU, den Arbeitsspeicher und den zugewiesenen Datenträger zwar nutzen, allerdings nicht wirklich effizient.

- **Effizienz erhöhen:** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten. Datenbankverwaltungsaufgaben sollten nach der Migration auf ein Minimum reduziert sein.

- **Flexibilität steigern:** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Die IT-Abteilung darf nicht im Weg stehen oder zum Geschäftshindernis werden.

- **Skalierung**: Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.

- **Kosten:** Geschäftsinhaber und Anwendungsbesitzer möchten sicher sein, dass keine hohen Cloudkosten auf sie zukommen, wenn die Anwendungen lokal ausgeführt werden.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die verschiedenen Migrationen gesetzt. Anhand dieser Ziele werden die besten Migrationsmethoden bestimmt.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Leistung** | Nach der Migration sollten die Apps in Azure die gleichen Leistungsmerkmale aufweisen, über die sie in der lokalen Umgebung von Contoso derzeit verfügen. Die Umstellung auf die Cloud bedeutet nicht, dass die Leistung der Anwendung weniger wichtig ist. |
| **Kompatibilität** | Contoso muss die Kompatibilität seiner Anwendungen und Datenbanken mit Azure verstehen. Außerdem muss Contoso mit den Hostingoptionen in Azure vertraut sein. |
| **Datenquellen** | Alle Datenbanken werden ohne Ausnahme zu Azure verschoben. Basierend auf den Datenbank- und Anwendungsanalysen der verwendeten SQL-Features werden sie zu PaaS- oder IaaS-Modellen migriert. Alle Datenbanken müssen verschoben werden. |
| **Anwendung** | Anwendungen müssen wo möglich in die Cloud verschoben werden. Wenn sie nicht verschoben werden können, ist es möglich, dass sie über das Netzwerk von Azure ausschließlich über private Verbindungen eine Verbindung zur migrierten Datenbank herstellen. |
| **Kosten** | Contoso möchte nicht nur verstehen, welche Migrationsoptionen verfügbar sind, sondern auch über die Infrastrukturkosten nach der Verlagerung in die Cloud Bescheid wissen. |
| **Verwaltung** | Für die verschiedenen Abteilungen müssen Ressourcenverwaltungsgruppen sowie Ressourcengruppen erstellt werden, um die migrierten Datenbanken zu verwalten. Alle Ressourcen müssen aus Gründen der verbrauchsbasierten Kostenzuteilung mit Tags mit Abteilungsinformationen versehen werden. |
| **Einschränkungen** | Zu Beginn verfügen nicht alle Zweigstellen, die Anwendungen ausführen, über einen direkten ExpressRoute-Link zu Azure. Diese Zweigstellen müssen also eine Verbindung über virtuelle Netzwerkgateways herstellen. |

## <a name="solution-design"></a>Lösungsentwurf

Contoso hat bereits eine [Migrationsbewertung](https://docs.microsoft.com/azure/cloud-adoption-framework/plan/contoso-migration-assessment) für seine digitalen Ressourcen mithilfe von [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) und dem [Dienstzuordnungsfeature](https://docs.microsoft.com/azure/azure-monitor/insights/service-map) durchgeführt.

![Migrationsprozess](./media/contoso-migration-oss-db-to-azure/migration-process.png)
_Abbildung 1: Der Migrationsvorgang._

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Azure stellt eine zentralisierte Benutzeroberfläche für die Datenbankworkloads bereit. <br><br> Die Kosten können über Azure Cost Management und das Azure-Abrechnungsportal überwacht werden. <br><br> Dank der Azure-Abrechnungs-APIs ist eine Abrechnung mit verbrauchsbasierter Kostenzuteilung einfach durchzuführen. <br><br> Die Server- und Softwareverwaltung kann auf die IaaS-basierten Umgebungen reduziert werden. |
| **Nachteile** | Aufgrund der Anforderung IaaS-basierter VMs muss die Software auf diesen Computern weiterhin verwaltet werden. |

### <a name="budget-and-management"></a>Budget und Verwaltung

Vor der Migration muss die erforderliche Azure-Struktur vorhanden sein, damit die Verwaltungs- und Abrechnungsaspekte der Lösung unterstützt werden können.

Für die Verwaltungsanforderungen wurden mehrere [Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups/overview) erstellt, um die Organisationsstruktur unterstützen zu können.

Für die Abrechnungsanforderungen werden alle Azure-Ressourcen mit entsprechenden [Abrechnungstags](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources) versehen.

### <a name="migration-process"></a>Migrationsprozess

Datenmigrationen folgen einem Standardmuster, das wiederholt werden kann. Dazu gehören die folgenden Schritte, die den [Best Practices von Microsoft](https://datamigration.microsoft.com/) entsprechen:

- Vor der Migration:
  - **Ermittlung:** Ressourcen der Inventardatenbank und Anwendungsstapel
  - **Bewerten:** Bewerten der Workloads und Erstellen von Empfehlungen
  - **Konvertieren:** Konvertieren des Quellschemas, damit es im Ziel verwendet werden kann
- Migration:
  - **Migration:** Migrieren des Quellschemas, der Quelldaten und der Objekte in das Ziel
  - **Synchronisieren der Daten:** Synchronisieren der Daten, damit die Downtime möglichst gering ist
  - **Umstellung:** Umstellen der Quelle auf das Ziel
- Nach der Migration:
  - **Anpassen der Anwendungen:** Iteratives Vornehmen erforderlicher Änderungen an den Anwendungen
  - **Durchführen von Tests:** Iteratives Durchführen von Funktions- und Leistungstests
  - **Optimieren:** Auf den Tests basierende Behebung von Leistungsproblemen und Durchführen von erneuten Tests zur Bestätigung vorgenommener Leistungsverbesserungen
  - **Außerbetriebnahme von Ressourcen:** Sicherung und Außerbetriebnahme alter VMs und Hostingumgebungen

#### <a name="step-1-discovery"></a>Schritt 1: Ermittlung

Contoso hat Azure Migrate und das Dienstzuordnungsfeature verwendet, um die Abhängigkeiten in der Contoso-Umgebung offen zu legen. Mithilfe von Azure Migrate können Anwendungskomponenten in Windows- und Linux-Systemen automatisch erkannt und die Kommunikation zwischen Diensten zugeordnet werden. Mithilfe des Dienstzuordnungsfeatures von Azure Migrate wurden die Verbindungen zwischen Contoso-Servern, Prozessen, der Latenz zwischen eingehenden und ausgehenden Verbindungen, und Ports in der über TCP verbundenen Architektur offengelegt. Contoso musste einfach nur [Microsoft Monitoring Agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) und den [Microsoft Dependency-Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) installieren.

Bei der Azure-Migration konnte Contoso mehr als 300 Datenbankinstanzen identifizieren, die migriert werden müssen. Von diesen Instanzen können etwa 40 Prozent zu PaaS-basierten Diensten verschoben werden. Die verbleibenden 60 Prozent der Instanzen müssen zu einem IaaS-basierten Ansatz mit einer VM verschoben werden, die die entsprechende Datenbanksoftware ausführt.

#### <a name="step-2-application-assessment"></a>Schritt 2: Anwendungsbewertung

Die Ergebnisse der Bewertung konnten Contoso zeigen, dass hauptsächlich Java-, PHP- und Node.js-Anwendungen verwendet werden. Dabei wurde Folgendes identifiziert:

- 100 Java-Anwendungen
- Etwa 50 Node.js-Anwendungen
- Etwa 25 PHP-Anwendungen

#### <a name="step-3-database-assessment"></a>Schritt 3: Datenbankbewertung

Bei der Inventarisierung der Datenbanken wurden die einzelnen Datenbanken überprüft, um eine Methode zu bestimmen, mit der sie zu Azure migriert werden können. Bei den Datenbankmigrationen wurden die folgenden Richtlinien befolgt.

| Datenbanktyp | Details | Ziel | Migrationsleitfaden |
| --- | --- | --- | --- |
| **MySQL** | Alle unterstützten Versionen werden vor der Migration auf eine unterstützte Version aktualisiert. | Azure Database for MySQL (PaaS) | [Leitfaden](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)
| **PostgreSQL** | Alle unterstützten Versionen werden vor der Migration auf eine unterstützte Version aktualisiert. | Azure Database for PostgreSQL (PaaS) | [Leitfaden](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online) |
| **MariaDB** | Alle unterstützten Versionen werden vor der Migration auf eine unterstützte Version aktualisiert. | Azure Database for MySQL (PaaS) | [Leitfaden](https://datamigration.microsoft.com/scenario/mariadb-to-azuremariadb?step=1) |

#### <a name="step-4-migration-planning"></a>Schritt 4: Migrationsplanung

Aufgrund der großen Anzahl der Datenbanken richtete Contoso ein Projektmanagementbüro ein, das den Überblick über die einzelnen Datenbankmigrationsinstanzen behalten sollte. Jedem Unternehmens- und Anwendungsteam wurden [Zuständigkeiten und Verantwortlichkeiten](https://docs.microsoft.com/azure/cloud-adoption-framework/migrate/migration-considerations/assess/) zugewiesen.

Außerdem führte Contoso eine [Überprüfung der Workloads auf die jeweilige Migrationsbereitschaft](https://docs.microsoft.com/azure/cloud-adoption-framework/migrate/migration-considerations/assess/evaluate) durch. Bei dieser Überprüfung wurden die Infrastruktur, die Datenbank und die Netzwerkkomponenten untersucht.

#### <a name="step-5-test-migrations"></a>Schritt 5: Testmigrationen

Zum ersten Teil der Migrationsvorbereitung gehörte eine Testmigration der einzelnen Datenbanken in die bereits eingerichteten Umgebungen. Aus Zeitersparnisgründen wurden Skripts für alle Migrationsvorgänge erstellt und die jeweilige Dauer aufgezeichnet. Zur Beschleunigung der Migration wurde untersucht, welche Migrationsvorgänge gleichzeitig ausgeführt werden könnten.

Außerdem wurden Rollbackverfahren für die einzelnen Datenbankworkloads herausgearbeitet, sollten unerwartete Fehler auftreten.

Für die IaaS-basierten Workloads wurde vorab sämtliche erforderliche Drittanbietersoftware eingerichtet.

Nach der Testmigration konnte Contoso die verschiedenen [Tools für die Kostenschätzung](https://docs.microsoft.com/azure/cloud-adoption-framework/migrate/migration-considerations/assess/estimate) von Azure verwenden, um ein genaueres Bild der zukünftigen Betriebskosten für die Migration zu erhalten.

#### <a name="step-6-migration"></a>Schritt 6: Migration

Bei der Migration der Produktion arbeitete Contoso Zeitrahmen für alle Datenbankmigrationen heraus und untersuchte, welcher Umfang innerhalb des zeitlichen Rahmens eines Wochenendes (Freitag Mitternacht bis Sonntag Mitternacht) durchgeführt werden könnte, um so die Downtime für das Unternehmen möglichst gering zu halten.

### <a name="cleanup-after-migration"></a>Bereinigung nach der Migration

Contoso hat das Archivierungsfenster für alle Datenbankworkloads identifiziert. Wenn das Fenster abläuft, wird die Zuordnung der Ressourcen zur lokalen Infrastruktur aufgehoben. Dabei würden auch die Produktionsdaten von lokalen Servern entfernt und die Hostingserver würden außer Betrieb genommen werden, wenn das letzte Workloadfenster abgelaufen ist.

### <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

#### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, das die neuen Datenbankworkloads in Azure geschützt sind. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Contoso sollte die Konfiguration der Firewall und des virtuellen Netzwerks überprüfen.
- Contoso sollte Private Link einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte Azure Advanced Threat Protection aktivieren.

#### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Datenbanken in Azure gesichert sind. Dies ermöglicht Sicherungen, die in einer gekoppelten Region im Fall eines regionalen Ausfalls genutzt werden können.

> [!IMPORTANT]
>Sorgen Sie dafür, dass die Azure-Ressource über eine [Ressourcensperre](https://docs.microsoft.com/azure/azure-resource-manager/management/lock-resources) verfügt, damit sie nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

#### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Viele Datenbankworkloads in Azure können nach oben oder unten skaliert werden. Die Überwachung der Server- und Datenbankleistung ist wichtig, um dafür zu sorgen, dass die Anforderung, die Kosten so gering wie möglich zu gestalten, erfüllt werden kann.
- Sowohl für CPU als auch für Speicher können jeweils Kosten auftreten. Sie können zwischen verschiedenen Tarifen auswählen. Stellen Sie sicher, dass ein entsprechender Tarif für die Datenworkloads ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.
- Verwenden Sie reservierte Kapazitäten, um Kosten zu sparen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde gezeigt, wie das fiktive Unternehmen Contoso seine Open-Source-Datenbanken bewertet hat und die Migration zu PaaS- und IaaS-Lösungen in Azure geplant und ausgeführt hat.
