---
title: Innovationstools für die Datenmigration
description: Hier finden Sie Informationen zu Azure Database Migration Service sowie zu anderen Tools für die Migration und Modernisierung von Daten, um für Cloudentwicklungen und -innovationen gerüstet zu sein.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 87376016c2d775d9aa546036504dfdf8c3ec9ba2
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83398731"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Sammeln von Daten durch Migration und Modernisierung vorhandener Datenquellen

Unternehmen verfügen häufig über verschiedene Arten von vorhandenen Daten, die sie [demokratisieren können](../considerations/data.md). Wenn eine Kundenhypothese zum Erstellen moderner Lösungen die Verwendung vorhandener Daten erfordert, ist der erste Schritt möglicherweise die Migration und Modernisierung dieser Daten, um diese auf Erfindungen und Innovationen vorzubereiten. Um eine Ausrichtung an den vorhandenen Migrationsbemühungen in einem Cloudeinführungsplan zu erzielen, können diese Migrations- und Modernisierungsaufgaben einfacher innerhalb der [Migrationsmethodik](../../migrate/index.md) ausgeführt werden.

## <a name="use-of-this-article"></a>Verwendung dieses Artikels

In diesem Artikel werden eine Reihe von Ansätzen beschrieben, die am Migrationsprozess ausgerichtet sind. Sie können diese Ansätze am besten an der standardmäßigen Migrationstoolkette ausrichten.

Während des Bewertungsprozesses in der Migrationsmethodik bewertet ein Cloudeinführungsteam den aktuellen und den gewünschten zukünftigen Status der migrierten Ressource. Wenn dieser Prozess zu einem Innovationsprojekt gehört, können beide Cloudeinführungsteams diesen Artikel verwenden, um bei solchen Entscheidungen zu helfen.

## <a name="primary-toolset"></a>Das primäre Toolset

Wenn Sie lokale Daten migrieren und modernisieren, ist die häufigste Wahl des Azure-Tools [Azure Database Migration Service](https://docs.microsoft.com/azure/dms). Dieser Dienst ist Teil der umfassenderen [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview)-Toolkette. Für bestehende SQL Server-Datenquellen kann der [Datenmigrations-Assistent](https://docs.microsoft.com/sql/dma/dma-overview) Ihnen helfen, eine kleine Anzahl von Datenstrukturen zu bewerten und zu migrieren.

Um Oracle- und NoSQL-Migrationen zu unterstützen, können Sie auch den [Database Migration Service](https://docs.microsoft.com/azure/dms) für bestimmte Arten von Quelle-zu-Ziel-Datenbanken verwenden. Beispiele hierfür sind Oracle zu PostgreSQL und MongoDB zu Azure Cosmos DB. Häufiger verwenden Einführungsteams Partnertools oder benutzerdefinierte Skripts, um zu Azure Cosmos DB, Azure HDInsight oder Optionen virtueller Computer auf Basis von IaaS (Infrastructure-as-a-Service) zu migrieren.

## <a name="considerations-and-guidance"></a>Überlegungen und Anleitungen

Wenn Sie Azure Database Migration Service für die Migration und Modernisierung von Daten verwenden, ist es wichtig, Folgendes zu verstehen:

- Die aktuelle Plattform für das Hosting der Datenquelle.
- Die aktuelle Version.
- Die zukünftige Plattform und Version, die die Kundenhypothese oder das Ziel am besten unterstützt.

In der folgenden Tabelle sind die Quell- und Zielpaare aufgeführt, die zusammen mit dem Migrationsteam geprüft werden sollten. Jedes Paar enthält eine Toolauswahl und einen Link zu einer entsprechenden Anleitung.

### <a name="migration-type"></a>Migrationstyp

Bei einer Offlinemigration beginnt der Ausfall der Anwendung, wenn die Migration gestartet wird. Bei einer Onlinemigration ist der Ausfall auf die Dauer der Umstellung am Ende der Migration beschränkt.

Es wird empfohlen, dass Sie Ihre akzeptablen Ausfallzeiten für das Geschäft festlegen und eine Offlinemigration testen. Auf diese Weise können Sie überprüfen, ob die Wiederherstellungsdauer mit der akzeptablen Ausfallzeit übereinstimmt. Wenn die Wiederherstellungsdauer inakzeptabel ist, führen Sie eine Onlinemigration durch.

| `Source`  | Ziel  | Tool  | Migrationstyp | Anleitungen |
|---|---|---|---|---|
| SQL Server | Azure SQL-Datenbank | Database Migration Service | Offline | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql) |
| SQL Server | Azure SQL-Datenbank | Database Migration Service | Online | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online) |
| SQL Server | Azure SQL-Datenbank – Verwaltete Instanz | Database Migration Service | Offline | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) |
| SQL Server | Azure SQL-Datenbank – Verwaltete Instanz | Database Migration Service | Online | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) |
| RDS SQL Server | Azure SQL-Datenbank oder verwaltete Azure SQL-Datenbank-Instanz | Database Migration Service | Online | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online) |
| MySQL | Azure Database for MySQL | Database Migration Service | Online | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online) |
| PostgreSQL | Azure Database for PostgreSQL | Database Migration Service | Online | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online) |
| MongoDB | Mongo-API von Azure Cosmos DB | Database Migration Service | Offline | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db) |
| MongoDB | Mongo-API von Azure Cosmos DB | Database Migration Service | Online | [Tutorial](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online) |
