---
title: Checkliste für die Cloudmigration mit erweitertem Umfang
description: Checkliste für die Cloudmigration mit erweitertem Umfang
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 730da49f910c34bf2bd94b8766cb292520201e50
ms.sourcegitcommit: 58ea417a7df3318e3d1a76d3807cc4e7e3976f52
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/07/2020
ms.locfileid: "78892632"
---
# <a name="expanded-scope-for-cloud-migration"></a>Erweiterter Umfang für die Cloudmigration

Der [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) im Cloud Adoption Framework ist der empfohlene Ausgangspunkt für Leser, die an einer Migration mit erneutem Hosten zu Azure interessiert sind, die auch als „Lift & Shift“-Migration bezeichnet wird. Dieser Leitfaden führt Sie durch eine Reihe von Voraussetzungen, Tools und Ansätzen für die Migration virtueller Computer in die Cloud.

Dieser Leitfaden ist zwar eine effektive Baseline, um Sie mit dieser Art von Migration vertraut zu machen, er geht aber von verschiedenen Annahmen aus. Diese Annahmen richten den Leitfaden auf viele Leser des Cloud Adoption Framework aus, indem sie einen vereinfachten Ansatz für Migrationen bieten. Dieser Abschnitt des Cloud Adoption Frameworks befasst sich mit einigen erweiterten Migrationsszenarien, die als Orientierungshilfe dienen, wenn diese Annahmen nicht zutreffen.

## <a name="cloud-migration-expanded-scope-checklist"></a>Checkliste für die Cloudmigration mit erweitertem Umfang

Die folgende Checkliste beschreibt die allgemeinen Komplexitätsbereiche, die eine Erweiterung des Umfangs der Migration über den [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) hinaus erfordern könnten.

### <a name="business-driven-scope-expansion"></a>Geschäftsorientierte Umfangserweiterung

- **[Unterstützung globaler Märkte](../azure-best-practices/multiple-regions.md):** Das Unternehmen ist in mehreren geografischen Regionen mit unterschiedlichen Anforderungen an die Datenhoheit tätig. Um diesen Anforderungen gerecht zu werden, sollten zusätzliche Überlegungen bei der erforderlichen Überprüfung und Verteilung der Ressourcen während der Migration berücksichtigt werden.

### <a name="technology-driven-scope-expansion"></a>Technologieorientierte Umfangserweiterung

- **[VMware-Migration](../azure-best-practices/vmware-host.md):** Das Migrieren von VMware-Hosts kann den gesamten Migrationsprozess beschleunigen. Jeder migrierte VMware-Host kann mithilfe eines Lift-and-Shift-Ansatzes mehrere Workloads in die Cloud verschieben. Nach der Migration können diese VMs und Workloads in VMware verbleiben oder zu modernen Cloudfunktionen migriert werden.
- **[SQL Server-Migration](../azure-best-practices/sql-migration.md):** Das Migrieren von SQL Server-Instanzen kann den gesamten Migrationsprozess beschleunigen. Jede migrierte SQL Server-Instanz kann mehrere Datenbanken und Dienste verschieben, was zu einer Beschleunigung mehrerer Workloads beitragen kann.
- **[Mehrere Rechenzentren](../azure-best-practices/multiple-datacenters.md):** Die Migration mehrerer Rechenzentren erhöht die Komplexität erheblich. Während der Prozesse zur Bewertung, Migration, Optimierung und Verwaltung werden zur Vorbereitung auf komplexere Umgebungen zusätzliche Überlegungen erläutert.
- **[Datenanforderungen überschreiten Netzwerkkapazität](../azure-best-practices/network-capacity-exceeded.md):** Unternehmen entscheiden sich häufig für eine Migration zur Cloud, da die Kapazität, Geschwindigkeit und Stabilität eines bestehenden Rechenzentrums nicht mehr zufriedenstellend ist. Leider erhöhen dieselben Einschränkungen die Komplexität des Migrationsprozesses, was eine zusätzliche Planung während der Bewertungs- und Migrationsprozesse erfordert.
- **[Strategie für Governance bzw. Compliance](../azure-best-practices/governance-or-compliance.md):** Wenn Governance und Compliance für den Erfolg einer Migration entscheidend sind, ist eine zusätzliche Abstimmung zwischen IT-Governanceteams und dem Cloudeinführungsteam erforderlich.

Wenn eine dieser Komplexitäten in Ihrem Szenario vorhanden ist, dann bietet dieser Abschnitt des Cloud Adoption Framework wahrscheinlich die erforderliche Art von Anleitung, um den Umfang der Migrationsprozesse ordnungsgemäß abzustimmen.

Jedes dieser Szenarien wird in den verschiedenen Artikeln in diesem Abschnitt des Cloud Adoption Frameworks behandelt.

## <a name="next-steps"></a>Nächste Schritte

Durchsuchen Sie das Inhaltsverzeichnis auf der linken Seite, um bestimmte Anforderungen oder Änderungen des Umfangs zu berücksichtigen. Alternativ ist die erste Umfangserweiterung in der Liste [Unterstützung globaler Märkte](../azure-best-practices/multiple-regions.md) ein guter Ausgangspunkt für die Überprüfung dieser Szenarien.

> [!div class="nextstepaction"]
> [Unterstützung globaler Märkte](../azure-best-practices/multiple-regions.md)
