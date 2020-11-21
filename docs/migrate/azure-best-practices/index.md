---
title: Prüfliste mit bewährten Methoden für die Azure-Cloudmigration
description: Die Prüfliste für die Azure-Cloudmigration enthält Informationen zur Implementierung der Azure-Tools, die zur Anpassung an die Best Practices für die Cloudmigration verwendet werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: seo-azure-migrate
ms.openlocfilehash: f90c1ef74d63d282270eeb022ca6e4ec54300071
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996076"
---
# <a name="azure-cloud-migration-best-practices-checklist"></a>Prüfliste mit bewährten Methoden für die Azure-Cloudmigration

Beginnen Sie mit dem [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) im Cloud Adoption Framework, wenn Sie an der Migration zu Azure interessiert sind. Dieser Leitfaden führt Sie durch eine Reihe von Tools und grundlegenden Ansätzen für die Migration virtueller Computer in die Cloud.

Die folgenden Prüflisten enthalten Best Practices für die Azure-Cloudmigration, die über die grundlegenden cloudnativen Tools hinausgehen. Diese Prüflisten beschreiben die allgemeinen Komplexitätsbereiche, die eine Erweiterung des Umfangs der Migration über den [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) hinaus erfordern könnten.

## <a name="migration-best-practices-for-business-driven-scope-expansion"></a>Best Practices für die Migration für die geschäftsorientierte Umfangserweiterung

- **[Unterstützung globaler Märkte](./multiple-regions.md):** Das Unternehmen ist in mehreren geografischen Regionen mit unterschiedlichen Anforderungen an die Datenhoheit tätig. Um diesen Anforderungen gerecht zu werden, sollten zusätzliche Überlegungen bei der erforderlichen Überprüfung und Verteilung der Ressourcen während der Migration berücksichtigt werden.

## <a name="migration-best-practices-for-technology-driven-scope-expansion"></a>Best Practices für die Migration für die technologieorientierte Umfangserweiterung

- **[VMware-Migration](./vmware-host.md):** Das Migrieren von VMware-Hosts kann den gesamten Migrationsprozess beschleunigen. Jeder migrierte VMware-Host kann mehrere Workloads in die Cloud verschieben. Nach der Migration können diese VMs und Workloads in VMware verbleiben oder zu modernen Cloudfunktionen migriert werden.
- **[SQL Server-Migration](./sql-migration.md):** Das Migrieren von SQL Server-Instanzen kann den gesamten Migrationsprozess beschleunigen. Jede migrierte Instanz kann mehrere Datenbanken und Dienste verschieben, was zu einer Beschleunigung mehrerer Workloads beitragen kann.
- **[Mehrere Rechenzentren](./multiple-datacenters.md):** Die Migration mehrerer Rechenzentren erhöht die Komplexität erheblich. Während der einzelnen Prozesse zum Verschieben (Bewertung, Migration, Optimierung und Verwaltung) werden zur Vorbereitung auf komplexere Umgebungen zusätzliche Überlegungen erläutert.
- **[Datenanforderungen überschreiten Netzwerkkapazität](./network-capacity-exceeded.md):** Unternehmen entscheiden sich häufig für eine Migration zur Cloud, da die Kapazität, Geschwindigkeit und Stabilität eines bestehenden Rechenzentrums nicht mehr zufriedenstellend ist. Leider erhöhen dieselben Einschränkungen die Komplexität des Migrationsprozesses, was eine zusätzliche Planung während der Bewertungs- und Migrationsprozesse erfordert.
- **[Strategie für Governance bzw. Compliance](./governance-or-compliance.md):** Wenn Governance und Compliance für den Erfolg einer Migration entscheidend sind, ist eine zusätzliche Abstimmung zwischen IT-Governanceteams und dem Cloudeinführungsteam erforderlich.

## <a name="additional-migration-best-practices"></a>Weitere Best Practices für die Azure-Migration

- [Einrichten von Netzwerken für zu Azure migrierte Workloads](./migrate-best-practices-networking.md)
- [Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md)
- [Kostenermittlung und Größenanpassung von zu Azure migrierten Workloads](./migrate-best-practices-costs.md)
- [Skalieren einer Migration zu Azure](./contoso-migration-scale.md)

## <a name="next-steps"></a>Nächste Schritte

Bei der Überprüfung der Best Practices für die Azure-Migration ist folgender Artikel ein guter Ausgangspunkt:

> [!div class="nextstepaction"]
> [Mehrere Rechenzentren](./multiple-datacenters.md)
