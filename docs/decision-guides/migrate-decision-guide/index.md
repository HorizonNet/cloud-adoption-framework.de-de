---
title: Entscheidungsleitfaden zur Wahl des Migrationstools
description: Nutzen Sie diese Entscheidungsstruktur als Leitfaden für die Auswahl der besten Tools, die auf der Grundlage von Migrationsentscheidungen verwendet werden können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.openlocfilehash: 806f8791575b65cb80a9c17bc2bd57b79f121021
ms.sourcegitcommit: 88fbc36cd634c3069e1a841a763a5327c737aa84
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2020
ms.locfileid: "80636462"
---
# <a name="migration-tools-decision-guide"></a>Entscheidungsleitfaden zur Wahl des Migrationstools

Die für die Migration einer Anwendung zu Azure verwendeten Strategie und Tools hängen weitgehend von Ihren Geschäftsmotivationen, Technologiestrategien und Zeitplänen sowie einem tiefen Verständnis der tatsächlichen Workloads und der zu migrierenden Ressourcen (Infrastruktur, Apps und Daten) ab. Die folgende Entscheidungsstruktur dient als Leitfaden für die Auswahl der besten Tools, die auf der Grundlage von Migrationsentscheidungen verwendet werden können. Behandeln Sie diese Entscheidungsstruktur als Ausgangspunkt.

Die Entscheidung für die Migration über PaaS- (Platform as a Service) oder IaaS-Technologien (Infrastructure as a Service) wird durch das Gleichgewicht zwischen Kosten, Zeit, vorhandener technischer Schulden und langfristigen Renditen bestimmt. IaaS ist oft der schnellste Weg in die Cloud mit der geringsten erforderlichen Änderung des Workloads. PaaS könnte Änderungen an Datenstrukturen oder Quellcode erfordern, bringt aber langfristig erhebliche Renditen in Form von reduzierten Betriebskosten und höherer technischer Flexibilität. Im folgenden Diagramm steht der Begriff _Modernisierung_ für die Entscheidung, eine Ressource im Rahmen der Migration zu modernisieren und die modernisierte Ressource zu einer PaaS-Plattform zu migrieren.

![Beispielentscheidungsstruktur zu Migrationstools.](../../_images/migrate/migration-tools-decision-tree.png)

## <a name="key-questions"></a>Kernfragen

Die Beantwortung der folgenden Fragen ermöglicht es Ihnen, Entscheidungen auf der Grundlage der obigen Struktur zu treffen.

- **Wäre eine Modernisierung der Anwendungsplattform während der Migration eine sinnvolle Investition in Zeit, Energie und Budget?** ? PaaS-Technologien wie Azure App Service oder Azure Functions können die Flexibilität bei der Bereitstellung erhöhen und die Komplexität der Verwaltung virtueller Computer für Hostanwendungen reduzieren. Allerdings können Anwendungen ein Refactoring erfordern, bevor sie die Vorteile dieser cloudnativen Funktionen nutzen können, was zu einem erheblichen Zeit- und Kostenaufwand für die Migration führen kann. Wenn Ihre Anwendung mit einem Minimum an Änderungen zu PaaS-Technologien migrieren kann, ist sie wahrscheinlich für eine Modernisierung geeignet. Wenn ein umfangreiches Refactoring erforderlich wäre, könnte eine Migration mit IaaS-basierten virtuellen Computern die bessere Wahl sein.
- **Wäre eine Modernisierung der Datenplattform während der Migration eine sinnvolle Investition in Zeit, Energie und Budget?** ? Wie bei der Anwendungsmigration bieten auch die von Azure-PaaS verwalteten Speicheroptionen wie Azure SQL-Datenbank, Cosmos DB und Azure Storage erhebliche Vorteile in Bezug auf Verwaltung und Flexibilität, aber die Migration zu diesen Diensten kann eine Überarbeitung bestehender Daten und der Anwendungen erfordern, die diese Daten verwenden. Datenplattformen benötigen oft deutlich weniger Refactoring als die Anwendungsplattform. Daher ist es üblich, dass die Datenplattform modernisiert wird, obwohl die Anwendungsplattform unverändert bleibt. Wenn Ihre Daten mit einem Minimum an Änderungen zu einem verwalteten Datendienst migriert werden können, sind sie für eine Modernisierung gut geeignet. Daten, die für die Nutzung dieser PaaS-Dienste einen erheblichen Zeit- oder Kostenaufwand für das Refactoring erfordern würden, sollten ggf. mithilfe IaaS-basierter virtuellen Computer migriert werden, um bestehende Hostingfunktionen besser zu nutzen.
- **Wird Ihre Anwendung derzeit auf dedizierten virtuellen Computern ausgeführt oder wird das Hosting mit anderen Anwendungen geteilt?** Auf dedizierten virtuellen Computern ausgeführte Anwendungen können leichter in PaaS-Hostingoptionen migriert werden als Anwendungen, die auf gemeinsamen Servern ausgeführt werden.
- **Wird die Datenmigration die Netzwerkbandbreite überschreiten?** Die Netzwerkkapazität zwischen Ihren lokalen Datenquellen und Azure kann einen Engpass bei der Datenmigration darstellen. Wenn die zu übertragenden Daten auf Bandbreitenbeschränkungen treffen, die eine effiziente oder zeitnahe Migration verhindern, müssen Sie sich möglicherweise mit alternativen oder Offlineübertragungsmechanismen befassen. Im [Artikel zur Migrationsreplikation](../../migrate/migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) für das Cloud Adoption Framework wird erläutert, wie sich Replikationsgrenzwerte auf die Migration auswirken können. Konsultieren Sie im Rahmen Ihrer Migrationsbewertung Ihre IT-Teams, um sicherzustellen, dass Ihre lokale und WAN-Bandbreite für Ihre Migrationsanforderungen geeignet ist. Beachten Sie auch das [Migrationsszenario als Beispiel, wenn die Speicheranforderungen die Netzwerkkapazität während einer Migration überschreiten](../../migrate/azure-best-practices/network-capacity-exceeded.md#suggested-prerequisites).
- **Nutzt Ihre Anwendung eine bestehende DevOps-Pipeline?** In vielen Fällen können Azure Pipelines leicht umgestaltet werden, um Anwendungen in cloudbasierten Hostingumgebungen bereitzustellen.
- **Stellen Ihre Daten komplexe Anforderungen an die Datenspeicherung?** Produktionsanwendungen erfordern in der Regel eine hochverfügbare Datenspeicherung, bieten Always On-Funktionalität und ähnliche Features zur Dienstbetriebszeit und Kontinuität. Azure PaaS-basierte verwaltete Datenbankoptionen wie Azure SQL-Datenbank, Azure Database for MySQL und Azure Cosmos DB bieten eine Betriebszeit von 99,99 % gemäß Vereinbarung zum Servicelevel (SLA). Im Gegensatz dazu bietet die IaaS-basierte SQL Server-Instanz auf virtuellen Azure-Computern gemäß Vereinbarung zum Servicelevel (SLA) eine Betriebszeit von 99,95 Prozent für Einzelinstanzen. Wenn Ihre Daten nicht für die Verwendung von PaaS-Speicheroptionen modernisiert werden können, erfordert die Gewährleistung einer höheren IaaS-Betriebszeit komplexere Datenspeicherungsszenarien wie die Ausführung von Always On-Clustern von SQL Server und die kontinuierliche Synchronisierung von Daten zwischen Instanzen. Dies kann erhebliche Hosting- und Wartungskosten verursachen, sodass der Ausgleich von Verfügbarkeitsanforderungen, Modernisierungsaufwand und Gesamtbudgetauswirkungen wichtig ist, wenn Sie Ihre Datenmigrationsoptionen berücksichtigen.

## <a name="innovation-and-migration"></a>Innovation und Migration

Im Einklang mit der Schwerpunktsetzung des Cloud Adoption Frameworks auf die [inkrementelle Migration](../../migrate/index.md#migration-implementation) schließt eine erste Entscheidung zu Migrationsstrategie und -tools zukünftige Innovationsbemühungen zur Aktualisierung einer Anwendung nicht aus, um die Möglichkeiten der Azure-Plattform zu nutzen. Während sich eine anfängliche Migration vor allem auf das erneute Hosten mit einem IaaS-Ansatz konzentrieren kann, sollten Sie planen, Ihr cloudbasiertes Anwendungsportfolio regelmäßig zu überprüfen, um Optimierungsmöglichkeiten zu untersuchen.

## <a name="learn-more"></a>Weitere Informationen

- **[Cloudgrundlagen: Übersicht über Azure-Computeoptionen](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview):** Bietet Informationen über die Möglichkeiten der Azure IaaS- und PaaS-Computeoptionen.
- **[Cloudgrundlagen: Auswählen des richtigen Datenspeichers](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview):** Erläutert die auf der Azure-Plattform verfügbaren PaaS-Speicheroptionen.
- **[Bewährte Methoden für die Migration: Datenanforderungen überschreiten Netzwerkkapazität während einer Migration](../../migrate/azure-best-practices/network-capacity-exceeded.md):** Erläutert alternative Datenmigrationsmechanismen für Szenarien, in denen die Datenmigration durch die verfügbare Netzwerkbandbreite beeinträchtigt wird.
- **[SQL-Datenbank: Auswählen der richtigen SQL Server-Option in Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#business-motivations-for-choosing-databases-managed-instances-or-sql-virtual-machines):** Erläuterung der Optionen und geschäftlichen Gründe für die Entscheidung, Ihre SQL Server-Workloads in einer gehosteten Infrastruktur- (IaaS) oder einer gehosteten Dienstumgebung (PaaS) bereitzustellen.
