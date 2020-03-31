---
title: Bewährte Methoden für die Azure-Migration
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die Tools implementieren, die für die Ausrichtung auf bewährte Methoden für die Cloudmigration erforderlich sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 22f2718775b194196f65672f0cbc1712d0a3a4ac
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433547"
---
# <a name="best-practices-for-cloud-migration"></a>Bewährte Methoden für die Cloudmigration

Die [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) im Framework für die Cloudeinführung ist der empfohlene Ausgangspunkt, wenn Sie an der Migration zu Azure interessiert sind. Dieser Leitfaden führt Sie durch eine Reihe von Tools und grundlegenden Ansätzen für die Migration virtueller Computer in die Cloud. In diesem Abschnitt des Frameworks für die Cloudeinführung werden viele bewährte Methoden behandelt, die über die grundlegenden cloudbasierten Tools hinausgehen.

## <a name="cloud-migration-best-practice-checklist"></a>Bewährte Methoden für die Cloudmigration

Die folgende Checkliste beschreibt die allgemeinen Komplexitätsbereiche, die eine Erweiterung des Umfangs der Migration über den [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) hinaus erfordern könnten.

### <a name="business-driven-scope-expansion"></a>Geschäftsorientierte Umfangserweiterung

- **[Unterstützung globaler Märkte](./multiple-regions.md):** Das Unternehmen ist in mehreren geografischen Regionen mit unterschiedlichen Anforderungen an die Datenhoheit tätig. Um diesen Anforderungen gerecht zu werden, sollten zusätzliche Überlegungen bei der erforderlichen Überprüfung und Verteilung der Ressourcen während der Migration berücksichtigt werden.

### <a name="technology-driven-scope-expansion"></a>Technologieorientierte Umfangserweiterung

- **[VMware-Migration](./vmware-host.md):** Das Migrieren von VMware-Hosts kann den gesamten Migrationsprozess beschleunigen. Jeder migrierte VMware-Host kann mithilfe eines Lift-and-Shift-Ansatzes mehrere Workloads in die Cloud verschieben. Nach der Migration können diese VMs und Workloads in VMware verbleiben oder zu modernen Cloudfunktionen migriert werden.
- **[SQL Server-Migration](./sql-migration.md):** Das Migrieren von SQL Server-Instanzen kann den gesamten Migrationsprozess beschleunigen. Jede migrierte SQL Server-Instanz kann mehrere Datenbanken und Dienste verschieben, was zu einer Beschleunigung mehrerer Workloads beitragen kann.
- **[Mehrere Rechenzentren](./multiple-datacenters.md):** Die Migration mehrerer Rechenzentren erhöht die Komplexität erheblich. Während der Prozesse zur Bewertung, Migration, Optimierung und Verwaltung werden zur Vorbereitung auf komplexere Umgebungen zusätzliche Überlegungen erläutert.
- **[Datenanforderungen überschreiten Netzwerkkapazität](./network-capacity-exceeded.md):** Unternehmen entscheiden sich häufig für eine Migration zur Cloud, da die Kapazität, Geschwindigkeit und Stabilität eines bestehenden Rechenzentrums nicht mehr zufriedenstellend ist. Leider erhöhen dieselben Einschränkungen die Komplexität des Migrationsprozesses, was eine zusätzliche Planung während der Bewertungs- und Migrationsprozesse erfordert.
- **[Strategie für Governance bzw. Compliance](./governance-or-compliance.md):** Wenn Governance und Compliance für den Erfolg einer Migration entscheidend sind, ist eine zusätzliche Abstimmung zwischen IT-Governanceteams und dem Cloudeinführungsteam erforderlich.

Wenn eine dieser Komplexitäten in Ihrem Szenario vorhanden ist, dann bietet dieser Abschnitt des Cloud Adoption Framework wahrscheinlich die erforderliche Art von Anleitung, um den Umfang der Migrationsprozesse ordnungsgemäß abzustimmen.

Jedes dieser Szenarien wird in den verschiedenen Artikeln in diesem Abschnitt des Cloud Adoption Frameworks behandelt.

## <a name="next-steps"></a>Nächste Schritte

Durchsuchen Sie das Inhaltsverzeichnis auf der linken Seite, um bestimmte Anforderungen oder Änderungen des Umfangs zu berücksichtigen. Alternativ ist die erste Umfangserweiterung in der Liste [Unterstützung globaler Märkte](./multiple-regions.md) ein guter Ausgangspunkt für die Überprüfung dieser Szenarien.

> [!div class="nextstepaction"]
> [Unterstützung globaler Märkte](./multiple-regions.md)
