---
title: Checkliste für die Cloudmigration mit erweitertem Umfang
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Checkliste für die Cloudmigration mit erweitertem Umfang
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 181777e08e82cf7e58c73c7c8b66544d0960656d
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564633"
---
# <a name="expanded-scope-for-cloud-migration"></a>Erweiterter Umfang für die Cloudmigration

Der [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) im Cloud Adoption Framework ist der empfohlene Ausgangspunkt für Leser, die an einer Migration mit erneutem Hosten zu Azure interessiert sind, die auch als „Lift & Shift“-Migration bezeichnet wird. Dieser Leitfaden führt Sie durch eine Reihe von Voraussetzungen, Tools und Ansätzen für die Migration virtueller Computer in die Cloud.

Dieser Leitfaden ist zwar eine effektive Baseline, um Sie mit dieser Art von Migration vertraut zu machen, er geht aber von verschiedenen Annahmen aus. Diese Annahmen richten den Leitfaden auf viele Leser des Cloud Adoption Framework aus, indem sie einen vereinfachten Ansatz für Migrationen bieten. Dieser Abschnitt des Cloud Adoption Frameworks befasst sich mit einigen erweiterten Migrationsszenarien, die als Orientierungshilfe dienen, wenn diese Annahmen nicht zutreffen.

## <a name="cloud-migration-expanded-scope-checklist"></a>Checkliste für die Cloudmigration mit erweitertem Umfang

Die folgende Checkliste beschreibt die allgemeinen Komplexitätsbereiche, die eine Erweiterung des Umfangs der Migration über den [Leitfaden zur Azure-Migration](../azure-migration-guide/index.md) hinaus erfordern könnten.

### <a name="business-driven-scope-expansion"></a>Geschäftsorientierte Umfangserweiterung

- **[Ausgewogenheit des Portfolios](./balance-the-portfolio.md):** Das Cloudstrategieteam ist daran interessiert, verstärkt in die Migration (erneutes Hosting bestehender Workloads und Anwendungen mit minimalen Änderungen) oder in Innovationen (Refactoring oder erneutes Erstellen dieser Workloads und Anwendungen unter Verwendung moderner Cloudtechnologie) zu investieren. Häufig ist ein Gleichgewicht zwischen den beiden Prioritäten der Schlüssel zum Erfolg. In diesem Leitfaden ist das Thema zum Ausgleichen des Portfolios zur Cloudeinführung ein allgemeines Thema, das in jedem der Migrationsprozesse behandelt wird.
- **[Unterstützung globaler Märkte](../../decision-guides/regions/index.md):** Das Unternehmen ist in mehreren geografischen Regionen mit unterschiedlichen Anforderungen an die Datenhoheit tätig. Um diesen Anforderungen gerecht zu werden, sollten zusätzliche Überlegungen bei der erforderlichen Überprüfung und Verteilung der Ressourcen während der Migration berücksichtigt werden.

### <a name="technology-driven-scope-expansion"></a>Technologieorientierte Umfangserweiterung

- **[VMware-Migration](./vmware-host.md):** Das Migrieren von VMware-Hosts kann den gesamten Migrationsprozess beschleunigen. Jeder migrierte VMware-Host kann mithilfe eines Lift-and-Shift-Ansatzes mehrere Workloads in die Cloud verschieben. Nach der Migration können diese VMs und Workloads in VMware verbleiben oder zu modernen Cloudfunktionen migriert werden.
- **[SQL Server-Migration](./sql-migration.md):** Das Migrieren von SQL Server-Instanzen kann den gesamten Migrationsprozess beschleunigen. Jede migrierte SQL Server-Instanz kann mehrere Datenbanken und Dienste verschieben, was zu einer Beschleunigung mehrerer Workloads beitragen kann.
- **[Mehrere Rechenzentren](./multiple-datacenters.md):** Die Migration mehrerer Rechenzentren erhöht die Komplexität erheblich. Während der Prozesse zur Bewertung, Migration, Optimierung und Verwaltung werden zur Vorbereitung auf komplexere Umgebungen zusätzliche Überlegungen erläutert.
- **[Datenanforderungen überschreiten Netzwerkkapazität](./network-capacity-exceeded.md):** Unternehmen entscheiden sich häufig für eine Migration zur Cloud, da die Kapazität, Geschwindigkeit und Stabilität eines bestehenden Rechenzentrums nicht mehr zufriedenstellend ist. Leider erhöhen dieselben Einschränkungen die Komplexität des Migrationsprozesses, was eine zusätzliche Planung während der Bewertungs- und Migrationsprozesse erfordert.
- **[Strategie für Governance bzw. Compliance](./governance-or-compliance.md):** Wenn Governance und Compliance für den Erfolg einer Migration entscheidend sind, ist eine zusätzliche Abstimmung zwischen IT-Governanceteams und dem Cloudeinführungsteam erforderlich.

Wenn eine dieser Komplexitäten in Ihrem Szenario vorhanden ist, dann bietet dieser Abschnitt des Cloud Adoption Framework wahrscheinlich die erforderliche Art von Anleitung, um den Umfang der Migrationsprozesse ordnungsgemäß abzustimmen.

Jedes dieser Szenarien wird in den verschiedenen Artikeln in diesem Abschnitt des Cloud Adoption Frameworks behandelt.

## <a name="next-steps"></a>Nächste Schritte

Durchsuchen Sie das Inhaltsverzeichnis auf der linken Seite, um bestimmte Anforderungen oder Änderungen des Umfangs zu berücksichtigen. Alternativ ist die erste Umfangserweiterung in der Liste [Ausgewogenheit des Portfolios](./balance-the-portfolio.md) ein guter Ausgangspunkt für die Überprüfung dieser Szenarien.

> [!div class="nextstepaction"]
> [Ausgewogenheit des Portfolios](./balance-the-portfolio.md)
