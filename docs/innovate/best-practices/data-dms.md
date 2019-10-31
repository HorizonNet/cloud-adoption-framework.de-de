---
title: 'Cloudinnovation: Data Migration Service'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Cloudinnovation: Data Migration Service'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 538cbc89fb592ecc19a5c25c42cf21231bfe05fe
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "73047755"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Sammeln von Daten durch Migration und Modernisierung vorhandener Datenquellen

In Unternehmen ist häufig eine Vielzahl unterschiedlicher Daten vorhanden, die [demokratisiert](../considerations/data.md) werden können. Wenn die Kundenhypothese zum Erstellen moderner Lösungen die Verwendung vorhandener Daten erfordert, ist der erste Schritt möglicherweise die Migration und Modernisierung dieser Daten, um diese auf Erfindungen und Innovationen vorzubereiten. Um eine Ausrichtung an den vorhandenen Migrationsbemühungen in einem Cloudeinführungsplan zu erzielen, können diese Migrations- und Modernisierungsaufgaben einfacher innerhalb der [Migrationsmethodik](../../migrate/index.md) ausgeführt werden.

## <a name="use-of-this-article"></a>Verwendung dieses Artikels

Dieser Artikel erläutert eine Reihe von Ansätzen, die am Migrationsprozess ausgerichtet sind, aber am besten in die standardmäßige Migrationstoolkette passen. Während des Bewertungsprozesses in der Migrationsmethodik bewertet das Cloudeinführungsteam den aktuellen und den gewünschten zukünftigen Status der zu migrierenden Ressource. Wenn dieser Prozess zu einem Innovationsprojekt gehört, hilft dieser Artikel beiden Cloudeinführungsteams bei solchen Entscheidungen.

## <a name="primary-toolset"></a>Das primäre Toolset

Beim Migrieren und Modernisieren von lokal gespeicherten Daten ist das Azure-Tool der Wahl meist der [Data Migration Service (DMS)](https://docs.microsoft.com/azure/dms), der zur umfassenderen [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)-Toolkette gehört. Bei vorhandenen SQL Server-Datenquellen kann auch der [Datenmigrations-Assistent (DMA)](https://docs.microsoft.com/sql/dma/dma-overview) bei der Bewertung und Migration einer kleineren Anzahl von Datenstrukturen helfen.

Zur Unterstützung von Oracle- oder NoSQL-Migrationen kann der [Data Migration Service](https://docs.microsoft.com/azure/dms) auch zur Migration zwischen bestimmten Quell- und Zieldatenbanken verwendet werden, z. B. von Oracle zu PostgreSQL oder von MongoDB zu Cosmos DB. Einführungsteams nutzen häufiger Drittanbietertools oder benutzerdefinierte Migrationsskripts für die Migration zu Cosmos DB, HDInsight oder IaaS-basierten VM-Optionen.

## <a name="considerations-and-guidance"></a>Überlegungen und Anleitungen

Wenn Sie DMS für die Migration und Modernisierung von Daten einsetzen möchten, müssen Sie die aktuelle Plattform zum Hosten der Daten (Quelle) einschließlich der Version sowie die zukünftige Plattform einschließlich Version (Ziel) kennen, die die Kundenhypothese am besten unterstützt. Im Folgenden finden Sie eine Liste mit Quell- und Zielpaaren, die zusammen mit dem Migrationsteam geprüft werden sollten. Für jedes Paar sind eine Toolauswahl und ein Link zu einem Leitfaden gemäß diesen Überlegungen vorhanden.

**Migrationstyp**: Bei einer Offlinemigration beginnt der Ausfall der Anwendung, wenn die Migration gestartet wird. Bei einer Onlinemigration ist der Ausfall auf die Dauer der Umstellung am Ende der Migration beschränkt. Sie müssen wissen, welche Ausfallzeiten für das Geschäft akzeptabel sind, und eine Offlinemigration testen, um zu ermitteln, ob die Wiederherstellungszeit diese Vorgaben erfüllt. Wenn dies nicht der Fall ist, muss die Migration online erfolgen.

|`Source`  |Ziel  |Tool  |Migrationstyp  |Anleitungen  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL-Datenbank|DMS|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL-Datenbank|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Verwaltete Azure SQL-Datenbank-Instanz|DMS|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Verwaltete Azure SQL-Datenbank-Instanz|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|RDS SQL Server|Azure SQL-Datenbank (oder verwaltete Instanz)|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure Database for MySQL|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure Database for PostgreSQL|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|MongoDB|Mongo-API von Azure Cosmos DB|DMS|Offline|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Mongo-API von Azure Cosmos DB|DMS|Online|[Tutorial](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|Verschiedene PaaS- und IaaS-Optionen|Drittanbieter oder Azure Migrate|Verschiedene|[Entscheidungsstruktur](../../migrate/expanded-scope/data-oracle-migration.md)|
|Verschiedene NoSQL-Datenbanken|Cosmo DB oder IaaS-Optionen|Prozedurbasierte Migrationen oder Azure Migrate|Verschiedene|[Entscheidungsstruktur](../../migrate/expanded-scope/data-no-sql-migration.md)|
