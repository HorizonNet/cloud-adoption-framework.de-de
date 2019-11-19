---
title: Überprüfen Ihrer Datenoptionen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Überprüfen Sie Ihre Datenoptionen für Azure-Workloads.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 950465788053fa0977a158a5363cb6271e65b3e6
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73243325"
---
# <a name="review-your-data-options"></a>Überprüfen Ihrer Datenoptionen

Wenn Sie Ihre Landezonenumgebung für die Cloudeinführung vorbereiten, müssen Sie die Datenanforderungen für das Hosten Ihrer Workloads ermitteln. Azure-Datenbankprodukte und -dienste unterstützen viele verschiedene Szenarien und Funktionen für die Datenspeicherung. Die Konfiguration Ihrer Landezonenumgebung zur Unterstützung der Datenanforderungen richtet sich nach den governancebezogenen, technischen und betriebswirtschaftlichen Anforderungen Ihrer Workload.

## <a name="identify-data-services-requirements"></a>Identifizieren von Anforderungen der Datendienste

Im Rahmen der Evaluierung und Vorbereitung Ihrer Landezone müssen Sie die Datenspeicher identifizieren, die von Ihrer Landezone unterstützt werden müssen. Dieser Prozess umfasst die Bewertung der einzelnen Anwendungen und Dienste, aus denen Ihre Workloads bestehen, um die Datenspeicher- und Zugriffsanforderungen zu ermitteln. Nachdem Sie diese Anforderungen identifiziert und dokumentiert haben, können Sie Richtlinien für Ihre Landezone erstellen und die zulässigen Ressourcentypen basierend auf Ihren Workloadanforderungen steuern.

Verwenden Sie für alle Anwendungen oder Dienste, die Sie in Ihrer Landezonenumgebung bereitstellen, die folgende Entscheidungsstruktur als Ausgangspunkt für die Ermittlung der geeigneten Datenspeicherdienste, die verwendet werden sollen:

![Entscheidungsstruktur für Azure-Datenbankdienste](../../_images/ready/data-decision-tree.png)

### <a name="key-questions"></a>Kernfragen

Die Beantwortung der folgenden Fragen zu Ihren Workloads ist hilfreich, um basierend auf der Entscheidungsstruktur für Azure-Datenbankdienste Entscheidungen treffen zu können:

- **Benötigen Sie die vollständige Kontrolle über Ihre Datenbanksoftware oder das Hostbetriebssystem, oder müssen Sie der Besitzer sein?** Für einige Szenarien ist ein hohes Maß an Kontrolle bzw. auch der Besitz der Softwarekonfiguration und des Hostservers Ihrer Datenbankworkloads erforderlich. In diesen Szenarien können Sie benutzerdefinierte virtuelle IaaS-Computer (Infrastructure-as-a-Service) bereitstellen, die Ihnen die vollständige Kontrolle der Bereitstellung und Konfiguration von Datendiensten ermöglichen. Falls diese Anforderungen bei Ihnen nicht bestehen, können Ihre Verwaltungs- und Betriebskosten mit verwalteten PaaS-Datenbankdiensten (Platform-as-a-Service) ggf. reduziert werden.
- **Sollen Ihre Workloads relationale Datenbanken verwenden?** Wenn ja: Welche Technologie soll genutzt werden? Azure verfügt über verwaltete PaaS-Datenbankfunktionen für [Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), [MySQL](https://docs.microsoft.com/azure/mysql/overview), [PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) und [MariaDB](https://docs.microsoft.com/azure/mariadb/overview).
- **Verwenden Ihre Workloads SQL Server?** In Azure können Sie Ihre Workloads auf IaaS-basierten [virtuellen Azure-Computern mit SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server) oder unter dem [von Azure SQL-Datenbank gehosteten Dienst](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) auf PaaS-Basis ausführen. Bei der Wahl der Option muss vor allem die Frage beantwortet werden, ob Sie Ihre Datenbank verwalten, Patches anwenden und Sicherungen erstellen oder diese Vorgänge an Azure delegieren möchten. In einigen Szenarien kann es aufgrund von Kompatibilitätsproblemen auch erforderlich sein, dass ein IaaS-gehosteter Computer mit SQL Server verwendet wird. Weitere Informationen zur Auswahl der richtigen Option für Ihre Workloads finden Sie unter [Auswählen der richtigen SQL Server-Option in Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).
- **Wird für Ihre Workloads Schlüssel-Wert-Datenbankspeicher verwendet?** [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) verfügt über eine Hochleistungs-Datenspeicherlösung mit Zwischenspeicherung von Schlüsseln und Werten, die für schnelle, skalierbare Anwendungen genutzt werden kann. [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) verfügt ebenfalls über allgemeine Schlüssel-Wert-Speicherfunktionen.
- **Verwenden Ihre Workloads Dokument- oder Graphdaten?** [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) ist ein Datenbankdienst mit mehreren Modellen, der eine Vielzahl von Datentypen und APIs unterstützt. Azure Cosmos DB bietet auch Funktionen für Dokument- und Graphdatenbanken.
- **Verwenden Ihre Workloads Spaltenfamiliendaten?** [Apache HBase in Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview) basiert auf Apache Hadoop. Apache HBase unterstützt große Mengen von unstrukturierten und halbstrukturierten Daten in einer schemalosen Datenbank, die nach Spaltenfamilien organisiert ist.
- **Werden für Ihre Workloads Datenanalysefunktionen mit hoher Kapazität benötigt?** Sie können [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) zum effektiven Speichern und Abfragen von strukturierten Daten im Petabytebereich verwenden. Für unstrukturierte Big Data-Workloads können Sie [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) zum Speichern und Analysieren von Dateien im Petabytebereich und von Billionen von Objekten verwenden.
- **Werden für Ihre Workloads Suchmaschinenfunktionen benötigt?** Sie können [Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) zum Erstellen cloudbasierter Suchindizes mit KI-Erweiterung verwenden, die in Ihre Anwendungen integriert werden können.
- **Verwenden Ihre Workloads Zeitreihendaten?** [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-overview) ist zum Speichern, Visualisieren und Abfragen großer Mengen von Zeitreihendaten ausgelegt, z.B. der von IoT-Geräten generierten Daten.

> [!NOTE]
> Weitere Informationen zum Bewerten von Datenbankoptionen für die einzelnen Anwendungen oder Dienste finden Sie im [Leitfaden zur Azure-Anwendungsarchitektur](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-comparison).

## <a name="common-database-scenarios"></a>Häufige Datenbankszenarien

In der folgenden Tabelle sind einige häufige Anforderungen für Nutzungsszenarien und die empfohlenen Datenbankdienste für die Verarbeitung aufgeführt:

| **Szenario** | **Datendienst** |
|-----|-----|
| Ich benötige eine global verteilte Datenbank mit mehreren Modellen mit Unterstützung für die NoSQL-Auswahl. | [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) |
| Ich benötige eine vollständig verwaltete relationale Datenbank, die sich schnell einrichten und im laufenden Betrieb skalieren lässt und integrierte Funktionen für Intelligence und Sicherheit umfasst. | [Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) |
| Ich benötige eine vollständig verwaltete, skalierbare relationale MySQL-Datenbank mit integrierter Hochverfügbarkeit und Sicherheit ohne Zusatzkosten. | [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) |
| Ich benötige eine vollständig verwaltete, skalierbare relationale PostgreSQL-Datenbank mit integrierter Hochverfügbarkeit und Sicherheit ohne Zusatzkosten. | [Azure-Datenbank für PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) |
| Ich plane das Hosten von SQL Server-Unternehmens-Apps in der Cloud mit vollständiger Kontrolle des Serverbetriebssystems. | [SQL Server auf virtuellen Computern](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview) |
| Ich benötige ein vollständig verwaltetes, elastisches Data Warehouse mit Sicherheit auf allen Ebenen ohne Zusatzkosten. | [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) |
| Ich benötige Data Lake Storage-Ressourcen, die Hadoop-Cluster oder HDFS-Daten unterstützen können. | [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) |
| Ich benötige hohen Durchsatz und konsistenten Zugriff mit niedriger Latenz für meine Daten, um schnelle und skalierbare Anwendungen zu unterstützen. | [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) |
| Ich benötige eine vollständig verwaltete, skalierbare relationale MariaDB-Datenbank mit integrierter Hochverfügbarkeit und Sicherheit ohne Zusatzkosten. | [Azure Database for MariaDB](https://docs.microsoft.com/azure/mariadb/overview) |

## <a name="regional-availability"></a>Regionale Verfügbarkeit

Mit Azure können Sie Dienste in der Größenordnung bereitstellen, die Sie benötigen, um Ihre Kunden und Partner zu erreichen, _wo auch immer diese sich befinden_. Ein wichtiger Faktor bei der Planung Ihrer Cloudbereitstellung ist die Ermittlung, in welcher Azure-Region Ihre Workloadressourcen gehostet werden.

Die meisten Datenbankdienste sind in den meisten Azure-Regionen allgemein verfügbar. Es gibt aber einige Regionen (vor allem für Behörden), in denen nur ein Teil dieser Produkte unterstützt wird. Bevor Sie die Entscheidung treffen, in welchen Regionen Sie Ihre Datenbankressourcen bereitstellen, empfehlen wir Ihnen die [Seite zu den Regionen](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=data-factory,sql-server-stretch-database,redis-cache,database-migration,sql-data-warehouse,postgresql,mariadb,cosmos-db,mysql,sql-database) , um den aktuellen Status der regionalen Verfügbarkeit zu überprüfen.

Sie können die [Seite „Azure-Regionen“](https://azure.microsoft.com/global-infrastructure/regions) besuchen, um weitere Informationen zur globalen Azure-Infrastruktur zu erhalten. Sie können auch die Seite mit den  [verfügbaren Produkten nach Region](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) verwenden, um spezifische Informationen dazu zu erhalten, welche Dienste in den einzelnen Azure-Regionen verfügbar sind.

## <a name="data-residency-and-compliance-requirements"></a>Anforderungen an Datenresidenz und -konformität

Häufig gelten für Ihre Workloads rechtliche und vertragliche Anforderungen in Bezug auf die Datenspeicherung. Diese Anforderungen können je nach Standort Ihrer Organisation, dem Gerichtsstand der physischen Ressourcen, auf denen Ihre Datenspeicher gehostet werden, und der für Sie geltenden Branche ggf. variieren. Für das Berücksichtigen von Datenverpflichtungen sind die Datenklassifizierung, der Datenstandort und die entsprechenden Zuständigkeiten für den Schutz der Daten im Rahmen des Modells für die gemeinsame Verantwortung wichtig. Hilfe zum Verständnis dieser Anforderungen finden Sie im Whitepaper [Sicherheit und Compliance bei der Speicherung von Benutzerdaten mit Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Ein Teil Ihrer Compliancemaßnahmen kann die Steuerung des physischen Speicherorts Ihrer Datenbankressourcen umfassen. Azure-Regionen sind in Gruppen organisiert, die als „Geografien“ bezeichnet werden. Eine [Azure-Geografie](https://azure.microsoft.com/global-infrastructure/geographies) sorgt dafür, dass Anforderungen an Datenresidenz, Datenhoheit, Konformität und Ausfallsicherheit innerhalb geografischer und politischer Grenzen erfüllt werden. Wenn für Ihre Workloads Anforderungen an die Datenhoheit oder andere Complianceanforderungen bestehen, müssen die Speicherressourcen in den Regionen in einer konformen Azure-Geografie bereitgestellt werden.

## <a name="establish-controls-for-database-services"></a>Einrichten von Kontrollelementen für Datenbankdienste

Wenn Sie Ihre Landezonenumgebung vorbereiten, können Sie Kontrollelemente einrichten, die einschränken, welche Datenspeicher von Benutzern bereitgestellt werden können. Kontrollelemente können Ihnen als Hilfe beim Verwalten von Kosten und Eindämmen von Sicherheitsrisiken dienen, während Entwickler und IT-Teams weiterhin Ressourcen bereitstellen und konfigurieren können, die zum Unterstützen Ihrer Workloads benötigt werden.

Nachdem Sie die Anforderungen Ihrer Landezone identifiziert und dokumentiert haben, können Sie [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) nutzen, um zu steuern, welche Datenbankressourcen von Benutzern erstellt werden dürfen. Kontrollelemente können [die Erstellung von Datenbankressourcentypen zulassen oder verweigern](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types). Beispielsweise können Sie festlegen, dass Benutzer nur Azure SQL-Datenbank-Ressourcen erstellen können. Sie können die zulässigen Optionen bei der Erstellung einer Ressource auch über eine Richtlinie steuern, z.B. das [Einschränken der Bereitstellung von SQL-Datenbank-SKUs](https://docs.microsoft.com/azure/governance/policy/samples/allowed-sql-db-skus) oder das [Zulassen nur von bestimmten Versionen von SQL Server](https://docs.microsoft.com/azure/governance/policy/samples/require-sql-12), die auf einem virtuellen IaaS-Computer installiert werden können.

Der Bereich von Richtlinien kann auf Ressourcen, Ressourcengruppen, Abonnements oder Verwaltungsgruppen festgelegt werden. Darüber hinaus können diese Richtlinien auch in [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview)-Definitionen eingebunden und in der gesamten Cloudumgebung wiederholt angewendet werden.
