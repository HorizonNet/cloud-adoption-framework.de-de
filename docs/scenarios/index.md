---
title: Ein Migrationsansatz für die Einführung von Azure
description: Azure Migrate bietet einen Migrationsansatz, mit dem Sie Ihr gesamtes IT-Portfolio migrieren und modernisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: f8135b59ed583a2c790b1f78a6b1f940fe4a0acd
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451492"
---
<!-- docsTest:ignore "One Migration" -->
<!-- cSpell:ignore HANA -->

# <a name="one-migration-approach-to-migrating-the-it-portfolio"></a>Ein Migrationsansatz für die Migration des gesamten IT-Portfolios

Sowohl Azure als auch Azure Migrate sind für das Hosting von Microsoft-Technologien bekannt. Vielleicht wissen Sie aber nicht, dass Azure auch Migrationen unterstützt, die über Windows und SQL Server hinausgehen. Die in der Migrationsmethodik dokumentierten Migrationsszenarien beruhen sowohl für die Migration von Microsoft- als auch von Drittanbietertechnologien auf den gleichen einheitlichen Richtlinien und Prozessen.

## <a name="migration-scenarios"></a>Migrationsszenarios

Die folgende Abbildung zeigt eine Reihe von Migrationsszenarien, die auf der gleichen iterativen Methodik für die Migration und Modernisierung beruhen.

![Cloud Adoption Framework-Migrationsmodell](../_images/migrate/one-migrate.png)

### <a name="links-to-migration-scenarios"></a>Links zu Migrationsszenarien

| | | | |
|---------|---------|---------|---------|
| **Virtuelle Computer** | [Virtuelle Computer](../migrate/azure-best-practices/contoso-migration-rehost-vm.md) | [Linux-Server](../migrate/azure-best-practices/contoso-migration-rehost-linux-vm.md) | [Virtuelle Desktops](./wvd/index.md) |
| **Anwendungen** | [ASP.NET](../migrate/azure-best-practices/contoso-migration-refactor-web-app-sql.md) | [Java](https://docs.microsoft.com/azure/java/migration-overview?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) | [PHP](../migrate/azure-best-practices/contoso-migration-refactor-linux-app-service-mysql.md) |
| **Daten** | [SQL Server](../migrate/azure-best-practices/contoso-migration-rehost-vm-sql-managed-instance.md) | [Open Source-Datenbanken](../migrate/azure-best-practices/sql-migration.md) | Analytics |
| **Hybrid** | [Azure Stack](./azure-stack/index.md) | [VMware](../migrate/azure-best-practices/vmware-host.md) | |
| **Weitere Szenarien** | [Sichere Workloads](../migrate/azure-best-practices/migrate-best-practices-security-management.md) | [Mainframes](../infrastructure/mainframe-migration/index.md) | NetApp und SAP HANA |

## <a name="migrate-methodology"></a>Migrationsmethodik

Bei jedem der Migrationsszenarien beruht die Migration vorhandener Workloads zur Cloud auf den gleichen einheitlichen Prozessen.

![Cloud Adoption Framework-Migrationsmodell](../_images/migrate/methodology.png)

Strukturieren Sie Migrationswellen, um die Releases mehrerer Workloads zu steuern. Das Erstellen eines Cloudeinführungsplans und Einrichten von Azure-Zielzonen im Rahmen der Planungs- und Bereitschaftsmethodik erleichtert Ihnen die Strukturierung Ihrer Migrationswellen.

Befolgen Sie während jeder Iteration die Migrationsmethodik, um Workloads zu bewerten, bereitzustellen und freizugeben. Wenn Sie diese Prozesse an Ihre speziellen Szenarien anpassen möchten, klicken Sie auf eines der oben aufgeführten Migrationsszenarien, um weiterführende Informationen anzuzeigen.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie kein bestimmtes Szenario migrieren, beginnen Sie mit dem [Cloud Adoption Framework-Migrationsprozess in vier Schritten](../migrate/index.md).
