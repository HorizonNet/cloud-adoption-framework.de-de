---
title: Ansatz der Einzelmigration für die Einführung von Azure
description: Azure Migrate bietet einen Migrationsansatz, mit dem Sie Ihr gesamtes IT-Portfolio migrieren und modernisieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1fcc9914a2ba517598972c52dc9e286933d122d2
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572628"
---
<!-- docsTest:ignore "One Migration" -->
<!-- cSpell:ignore HANA -->

# <a name="the-one-migration-approach-to-migrating-the-it-portfolio"></a>Ansatz der Einzelmigration für die Migration des IT-Portfolios

Sowohl Azure als auch Azure Migrate sind für das Hosting von Microsoft-Technologien bekannt. Vielleicht wissen Sie aber nicht, dass Azure auch Migrationen unterstützt, die über Windows und SQL Server hinausgehen. Die in der Migrationsmethodik dokumentierten Szenarien für die *Einzelmigration* beruhen sowohl für die Migration von Microsoft- als auch von Drittanbietertechnologien auf den gleichen einheitlichen Richtlinien und Prozessen.

## <a name="migration-scenarios"></a>Migrationsszenarios

Das folgende Diagramm und die folgende Tabelle zeigen eine Reihe von Szenarien, die auf der gleichen iterativen Methodik für die Migration und Modernisierung beruhen.

![Diagramm: Cloud Adoption Framework-Migrationsmodell](../_images/migrate/one-migrate.png)

| | | | |
|---------|---------|---------|---------|
| **Virtuelle Computer** | [Virtuelle Computer](../migrate/azure-best-practices/contoso-migration-rehost-vm.md) | [Linux-Server](../migrate/azure-best-practices/contoso-migration-rehost-linux-vm.md) | [Virtuelle Desktops](./wvd/index.md) |
| **Anwendungen** | [ASP.NET](../migrate/azure-best-practices/contoso-migration-refactor-web-app-sql.md) | [Java](/azure/java/migration-overview?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json) | [PHP](../migrate/azure-best-practices/contoso-migration-refactor-linux-app-service-mysql.md) |
| **Daten** | [SQL Server](../migrate/azure-best-practices/contoso-migration-rehost-vm-sql-managed-instance.md) | [Open Source-Datenbanken](../migrate/azure-best-practices/sql-migration.md) | Analytics |
| **Hybrid** | [Azure Stack](./azure-stack/index.md) | [VMware](../migrate/azure-best-practices/vmware-host.md) | |
| **Weitere Szenarien** | [Sichere Workloads](../migrate/azure-best-practices/migrate-best-practices-security-management.md) | [Mainframes](../infrastructure/mainframe-migration/index.md) | NetApp und SAP HANA |

## <a name="migration-methodology"></a>Migrationsmethodik

In jedem der vorhergehenden Migrationsszenarien werden Sie durch den gleichen grundlegenden Prozess geleitet, wenn Sie Ihre bestehenden Workloads in die Cloud verlagern, wie hier gezeigt:

![Diagramm: Cloud Adoption Framework-Migrationsmodell](../_images/migrate/methodology.png)

In jedem Szenario strukturieren Sie Migrationswellen, um die Releases mehrerer Workloads zu steuern. Das Erstellen eines Cloudeinführungsplans und Einrichten von Azure-Zielzonen im Rahmen der Planungs- und Bereitschaftsmethodik erleichtert Ihnen die Strukturierung Ihrer Migrationswellen.

Befolgen Sie während jeder Iteration die Migrationsmethodik, um Workloads zu bewerten, bereitzustellen und freizugeben. Wenn Sie diese Prozesse an die speziellen Szenarien Ihrer Organisation anpassen möchten, klicken Sie auf eines der in der Tabelle aufgeführten Migrationsszenarien, um weiterführende Informationen anzuzeigen.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie kein bestimmtes Szenario migrieren, beginnen Sie mit dem [Cloud Adoption Framework-Migrationsprozess in vier Schritten](../migrate/index.md).
