---
title: Übersicht über Beispiele für eine Anwendungsmigration für Azure
description: Bietet eine Übersicht über die Beispiele für die Anwendungsmigration, die als Teil der Migrationsmethodik im Cloud Adoption Framework enthalten sind.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7f6789a390d38b902ec8b7d64ac20b51557f86ca
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86233561"
---
# <a name="overview-of-application-migration-examples-for-azure"></a>Übersicht über Beispiele für eine Anwendungsmigration für Azure

Dieser Abschnitt des Cloud Adoption Framework enthält Beispiele für mehrere gängige Migrationsszenarien und zeigt, wie Sie lokale Infrastrukturen in [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure) migrieren können.

## <a name="introduction"></a>Einführung

Azure bietet Zugriff auf einen umfassenden Satz von Clouddiensten. Als Entwickler und IT-Spezialisten können Sie diese Dienste zum Erstellen, Bereitstellen und Verwalten von Anwendungen für verschiedene Tools und Frameworks über ein globales Netzwerk von Rechenzentren verwenden. Im Rahmen der Herausforderungen, die Ihr Unternehmen in Bezug auf die digitalen Veränderungen bewältigen muss, können Sie mithilfe der Azure-Cloud ermitteln, wie Sie Ressourcen und Vorgänge optimieren, sich mit Ihren Kunden und Mitarbeitern vernetzen und Ihre Produkte transformieren.

Es ist aber klar, dass viele Organisationen trotz aller Vorteile, die sich mit der Cloud in Bezug auf Geschwindigkeit und Flexibilität, Kostensenkung, Leistung und Zuverlässigkeit ergeben, noch längere Zeit lokale Rechenzentren betreiben müssen. Als Antwort auf die Hürden, die bei der Umstellung auf die Cloud überwunden werden müssen, verfügt Azure über eine Hybrid Cloud-Strategie, bei der Brücken zwischen Ihren lokalen Rechenzentren und der öffentlichen Azure-Cloud geschlagen werden (z. B durch Verwendung von Azure-Cloudressourcen wie Azure Backup zum Schützen von lokalen Ressourcen oder Azure-Analysen, um Erkenntnisse zu lokalen Workloads zu erhalten).

Im Rahmen der Hybrid Cloud-Strategie werden für Azure kontinuierlich erweiterte Lösungen zum Migrieren von lokalen Anwendungen und Workloads in die Cloud bereitgestellt. Sie können Ihre lokalen Ressourcen mit einfachen Schritten umfassend bewerten, um zu ermitteln, wie sie in der Azure-Cloud ausgeführt werden. Nachdem Sie über eine ausführliche Bewertung verfügen, können Sie die Migration der Ressourcen zu Azure beruhigt angehen. Wenn die Ressourcen in Azure aktiv sind und ausgeführt werden, können Sie sie optimieren, um Zugriff, Flexibilität, Sicherheit und Zuverlässigkeit sicherzustellen und zu verbessern.

## <a name="migration-patterns"></a>Migrationsmuster

Die Strategien für die Migration zur Cloud lassen sich grob in vier Muster unterteilen: Zuweisen eines neuen Hosts, Umgestalten, Umstrukturieren oder Neu erstellen. Welche Strategie Sie übernehmen, richtet sich nach Ihrer Business-Treibern und Migrationszielen. Sie könnten mehrere Muster übernehmen. Beispielsweise können Sie nicht kritischen Anwendungen einen neuen Host zuweisen, während Sie Anwendungen, die komplexer und unternehmenskritisch sind, umstrukturieren. Sehen wir uns diese Muster einmal an:

| Muster | Definition | Verwendung |
| --- | --- | --- |
| **Zuweisen eines neuen Hosts** | Häufig als Lift & Shift-Migration bezeichnet. Diese Option erfordert keine Änderungen des Codes und ermöglicht Ihnen die schnelle Migration Ihrer vorhandenen Anwendungen zu Azure. Um die Vorteile der Cloud ohne die mit Änderungen des Codes verbundenen Risiken und Kosten zu nutzen, wird jede Anwendung im vorliegenden Zustand migriert. | Wenn Sie Anwendungen schnell in die Cloud verschieben müssen. <br><br> Wenn Sie eine Anwendung verschieben möchten, ohne sie zu ändern. <br><br> Wenn Ihre Anwendungen so konzipiert sind, dass sie nach der Migration die [Azure-IaaS](https://azure.microsoft.com/overview/what-is-iaas)-Skalierbarkeit nutzen können. <br><br> Wenn Anwendungen für Ihr Unternehmen wichtig sind, aber Anwendungsfunktionen nicht sofort geändert werden müssen. |
| **Umgestalten** | Die häufig als „Umpacken“ bezeichnete Umgestaltung erfordert nur minimale Änderungen der Anwendungen, sodass sie eine Verbindung mit [Azure-PaaS](https://azure.microsoft.com/overview/what-is-paas) herstellen und Cloudangebote verwenden können. <br><br> Sie könnten Ihre vorhandenen Anwendungen beispielsweise zu Azure App Service oder Azure Kubernetes Service (AKS) migrieren. <br><br> Alternativ könnten Sie relationale und nicht relationale Datenbanken für Azure SQL Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL und Azure Cosmos DB umgestalten. | Wenn Ihre Anwendung einfach zum Arbeiten in Azure umgepackt werden kann. <br><br> Wenn Sie innovative, von Azure bereitgestellte DevOps-Methoden anwenden möchten oder erwägen, DevOps mit einer Containerstrategie für Workloads zu verwenden. <br><br> Für die Umgestaltung müssen Sie die Portabilität Ihrer vorhandenen Codebasis und verfügbare Entwicklungsfertigkeiten berücksichtigen. |
| **Überarbeiten** | Beim Überarbeiten für die Migration liegt der Fokus auf dem Ändern und Erweitern von Anwendungsfunktionalität und Codebasis, um die Anwendungsarchitektur für die Cloudskalierbarkeit zu optimieren. <br><br> Sie könnten z.B. eine monolithische Anwendung in eine Gruppe von Microservices unterteilen, die zusammenarbeiten und einfach zu skalieren sind. <br><br> Sie könnten auch relationale und nicht relationale Datenbanken zu einer vollständig verwalteten Datenbanklösung umstrukturieren, z. B. Azure SQL Managed Instance, Azure Database for MySQL, Azure Database for PostgreSQL und Azure Cosmos DB. | Wenn Ihre Anwendungen eine größere Überarbeitung benötigen, um neue Funktionen zu integrieren oder effektiv auf einer Cloudplattform zu funktionieren. <br><br> Wenn Sie vorhandene Anwendungsinvestitionen nutzen, Skalierbarkeitsanforderungen erfüllen, innovative DevOps-Methoden anwenden und die Verwendung virtueller Computer minimieren möchten. |
| **Neuerstellen** | Das Neuerstellen geht einen Schritt weiter, da eine Anwendung in diesem Fall unter Verwendung von Azure-Cloudtechnologien von Grund auf neu erstellt wird. <br><br> Sie könnten beispielsweise Greenfield-Anwendungen mit [nativen Cloudtechnologien](https://azure.microsoft.com/overview/cloudnative) wie Azure Functions, Azure KI, SQL Managed Instance und Azure Cosmos DB erstellen. | Wenn Sie schnelle Entwicklung wünschen und Funktionalität sowie Lebensdauer vorhandener Anwendungen eingeschränkt sind. <br><br> Wenn Sie bereit sind, Business-Innovation (einschließlich von Azure bereitgestellter DevOps-Methoden) voran zu treiben, neue Anwendungen mit nativen Cloudtechnologien zu erstellen und die Weiterentwicklungen in KI, Blockchain und IoT zu nutzen. |

## <a name="migration-example-articles"></a>Artikel mit Migrationsbeispielen

Dieser Abschnitt enthält Beispiele für mehrere gängige Migrationsszenarien. Jedes Beispiel enthält Hintergrundinformationen und detailreiche Bereitstellungsszenarien, in denen die Einrichtung einer Migrationsinfrastruktur veranschaulicht und die Eignung der lokalen Ressourcen für die Migration bewertet wird. Diesem Abschnitt werden im Laufe der Zeit weitere Artikel hinzugefügt.

![Kategorien der Migrations-/Modernisierungsprojekte](./media/migration-patterns.png)
_Abbildung  1: Kategorien der gängigen Migrations-/Modernisierungsprojekte_

Bei dieser Reihe liegt der Schwerpunkt auf den einzelnen Migrationsszenarien, die auf geringfügig variierten Geschäftszielen basieren, die die Migrationsstrategie bestimmen. Für die einzelnen Bereitstellungsszenarien erhalten Sie Informationen zu Business-Treibern und Zielen, einer vorgeschlagenen Architektur, Schritten zum Ausführen der Migration sowie Empfehlungen zur Bereinigung und den nächsten Schritten nach Abschluss der Migration.

### <a name="assessment"></a>Bewertung

| Artikel | Details |
| --- | --- |
| [Bewerten der lokalen Ressourcen für die Migration zu Azure](../../plan/contoso-migration-assessment.md) | In diesem Artikel zu bewährten Methoden der Planmethodik wird erläutert, wie Sie eine Bewertung einer lokalen Anwendung ausführen, die unter VMware ausgeführt wird. In diesem Artikel bewertet eine Beispielorganisation Anwendungs-VMs mit dem Azure Migrate-Dienst und die SQL Server-Datenbank der Anwendung mit dem Datenmigrations-Assistenten. |

### <a name="infrastructure"></a>Infrastruktur

| Artikel | Details |
| --- | --- |
| [Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) | Der Artikel zeigt, wie eine Organisation seine lokale Infrastruktur und die Azure-Infrastruktur für die Migration vorbereitet. Auf das in diesem Artikel festgelegte Infrastrukturbeispiel wird in den anderen in diesem Abschnitt bereitgestellten Beispielen verwiesen. |

### <a name="windows-server-workloads"></a>Windows Server-Workloads

| Artikel | Details |
| --- | --- |
| [Zuweisen eines neuen Hosts für eine Anwendung auf Azure-VMs](./contoso-migration-rehost-vm.md) | Dieser Artikel enthält ein Beispiel für die Migration von lokalen Anwendungs-VMs zu Azure-VMs mit dem Azure Migrate-Dienst. |

### <a name="sql-server-workloads"></a>SQL Server-Workloads

| Artikel | Details |
| --- | --- |
| [Migrieren von SQL Server-Datenbanken zu Azure](./contoso-migration-sql-server-db-to-azure.md) | In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso verschiedene lokale SQL Server-Datenbanken bewertet hat und die Migration zu Azure geplant und ausgeführt hat. |
| [Zuweisen eines neuen Hosts für eine Anwendung auf einer Azure-VM und in einer verwalteten SQL-Instanz](./contoso-migration-rehost-vm-sql-managed-instance.md) | Dieser Artikel enthält ein Beispiel für eine Lift & Shift-Migration zu Azure für eine lokale Anwendung. Dazu gehört die Migration der Front-End-VM der Anwendung mithilfe von Azure Migrate und der Anwendungsdatenbank zu einer verwalteten Azure SQL-Instanz mithilfe von [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview). |
| [Zuweisen eines neuen Hosts für eine Anwendung auf Azure-VMs mithilfe von SQL Server Always On-Verfügbarkeitsgruppen](./contoso-migration-rehost-vm-sql-ag.md) | Dieses Beispiel zeigt, wie Sie eine Anwendung und Daten mit von Azure gehosteten SQL Server-VMs migrieren können. Dabei wird Azure Migrate verwendet, um die Anwendungs-VMs zu migrieren, und Azure Database Migration Service, um die Anwendungsdatenbank zu einem SQL Server-Cluster zu migrieren, der durch eine Always On-Verfügbarkeitsgruppe geschützt wird. |

### <a name="linux-and-open-source-databases"></a>Linux- und Open-Source-Datenbanken

| Artikel | Details |
| --- | --- |
| [Migrieren von Open-Source-Datenbanken zu Azure](./contoso-migration-oss-db-to-azure.md) | In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso verschiedene lokale Open-Source-Datenbanken bewertet hat und die Migration zu Azure geplant und ausgeführt hat. |
| [Migrieren von MySQL zu Azure](./contoso-migration-mysql-to-azure.md) | In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-MySQL-Datenbankplattform zu Azure geplant und durchgeführt hat. |
| [Migrieren von PostgreSQL zu Azure](./contoso-migration-postgresql-to-azure.md) | In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-PostgreSQL-Datenbankplattform zu Azure geplant und durchgeführt hat. |
| [Migrieren von MariaDB zu Azure](./contoso-migration-mariadb-to-azure.md) | In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-MariaDB-Datenbankplattform zu Azure geplant und durchgeführt hat. |
| [Zuweisen eines neuen Hosts für eine Linux-Anwendung auf Azure-VMs und Azure Database for MySQL](./contoso-migration-rehost-linux-vm-mysql.md) | Dieser Artikel enthält ein Beispiel für die Migration einer von Linux gehosteten Anwendung zu Azure-VMs mithilfe von Azure Migrate. Es migriert die Anwendungsdatenbank mit [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) zu Azure Database for MySQL. |
| [Zuweisen eines neuen Hosts für eine Linux-Anwendung auf Azure-VMs](./contoso-migration-rehost-linux-vm.md) | Dieses Beispiel zeigt, wie Sie eine Lift & Shift-Migration einer Linux-basierten App zu Azure-VMs mit dem Azure Migrate-Dienst durchführen können. |

### <a name="devtest-workloads"></a>Dev/Test-Workloads

| Artikel | Details |
| --- | --- |
| [Migrieren von Dev/Test-Umgebungen zu Azure IaaS](./contoso-migration-devtest-to-iaas.md) | Dieser Artikel zeigt, wie Contoso seiner Dev/Test-Umgebung für zwei Anwendungen, die auf VMware-VMs ausgeführt werden, durch die Migration zu Azure-VMs einen neuen Host zuweist. |
| [Migrieren zu Azure DevTest Labs](./contoso-migration-devtest-to-labs.md) | In diesem Artikel wird erläutert, wie Contoso seine Dev/Test-Workloads mithilfe von DevTest Labs in Azure verschiebt. |

### <a name="aspnet-and-php-web-apps"></a>ASP.NET- und PHP-Web-Apps

| Artikel | Details |
| --- | --- |
| [Umgestalten einer Windows-Anwendung mithilfe von Azure App Service und SQL-Datenbank](./contoso-migration-refactor-web-app-sql.md) | Dieses Beispiel zeigt, wie Sie eine lokale Windows-basierte Anwendung in eine Azure-Web-App migrieren und die Anwendungsdatenbank mit [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) in eine Azure SQL Server-Instanz migrieren. |
| [Umgestalten einer Windows-Anwendung mithilfe von Azure App Service und einer verwalteten SQL-Instanz](./contoso-migration-refactor-web-app-sql-managed-instance.md) | Dieses Beispiel zeigt, wie Sie eine lokale Windows-basierte Anwendung in eine Azure-Web-App migrieren und die Anwendungsdatenbank mit [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) in eine verwaltete Azure SQL-Instanz migrieren. |
| [Umgestalten einer Linux-Anwendung für mehrere Regionen mit Azure App Service, Traffic Manager und Azure Database for MySQL](./contoso-migration-refactor-linux-app-service-mysql.md) | Dieses Beispiel zeigt, wie Sie eine lokale Linux-basierte Anwendung mit dem Azure Traffic Manager, der in GitHub für Continuous Delivery integriert ist, in mehreren Azure-Regionen in eine Azure-Web-App migrieren. Die Anwendungsdatenbank wird zu einer Azure Database for MySQL-Instanz migriert. |
| [Neuerstellen einer Anwendung in Azure](./contoso-migration-rebuild.md) | Dieser Artikel enthält ein Beispiel für das Neuerstellen einer lokalen Anwendung mit einer Reihe von Azure-Funktionen und verwalteten Diensten, einschließlich Azure App Service, AKS, Azure Functions, Cognitive Services und Azure Cosmos DB. |
| [Umgestalten von Team Foundation Server in Azure DevOps Services](./contoso-migration-tfs-vsts.md) | Dieser Artikel zeigt eine Beispielmigration einer lokalen Team Foundation Server-Bereitstellung zu Azure DevOps Services in Azure. |

### <a name="sap"></a>SAP

| Artikel | Details |
| --- | --- |
| [SAP-Migrationshandbuch](https://azure.microsoft.com/resources/sap-on-azure-implementation-guide) | Hier finden Sie praktische Anleitungen zum Verschieben Ihrer lokalen SAP-Workloads in die Cloud. |
| [Migrieren von SAP-Anwendungen zu Azure](https://azure.microsoft.com/resources/migrating-sap-applications-to-azure) | Whitepaper und Roadmap für Ihren SAP-Übergang in die Cloud. |
| [Migrationsmethoden für SAP in Azure](https://azure.microsoft.com/resources/migration-methodologies-for-sap-on-azure) | Übersicht über verschiedene Migrationsoptionen zum Verschieben von SAP-Anwendungen in Azure. |

### <a name="specialized-workloads"></a>Spezialisierte Workloads

| Artikel | Details |
| --- | --- |
| [Verschieben einer lokalen VMware-Infrastruktur in Azure](./contoso-migration-vmware-to-azure.md) | Dieser Artikel enthält ein Beispiel für das Verschieben lokaler VMware-VMs in Azure mithilfe von Azure VMware Solution. |
| [Azure NetApp Files](https://azure.microsoft.com/services/netapp) | Unternehmensdateispeicher unterstützt von NetApp. Ausführen von Linux- und Windows-Dateiworkloads in Azure. |
| [Oracle in Azure](https://azure.microsoft.com/solutions/oracle) | Ausführen Ihrer Oracle-Datenbank und Unternehmensanwendungen in Azure und Oracle Cloud. |
| [Cray in Azure](https://azure.microsoft.com/solutions/high-performance-computing/cray) | High Performance Computing mit Cray in Azure. Ein dedizierter Supercomputer in Ihrem virtuellen Netzwerk. |

### <a name="vdi"></a>VDI

| Artikel | Details |
| --- | --- |
| [Verschieben lokaler Remotedesktopdienste zu Azure mit Windows Virtual Desktop](./contoso-migration-rds-to-wvd.md) | In diesem Artikel wird gezeigt, wie Sie lokale Remotedesktopdienste zu Windows Virtual Desktop in Azure migrieren. |

### <a name="migration-scaling"></a>Migrationskalierung

| Artikel | Details |
| --- | --- |
| [Skalieren einer Migration zu Azure](./contoso-migration-scale.md) | Dieser Artikel zeigt, wie eine Beispielorganisation die Skalierung auf eine vollständige Migration zu Azure vorbereitet. |

### <a name="demo-applications"></a>Demoanwendungen

<!-- docsTest:ignore SmartHotel360 osTicket -->

Die in diesem Abschnitt aufgeführten Beispielartikel verwenden zwei Demoanwendungen: SmartHotel360 und osTicket.

**SmartHotel360:** Diese Anwendung wurde von Microsoft als Testanwendung entwickelt, die Sie beim Arbeiten mit Azure verwenden können. Sie wird als Open-Source-App bereitgestellt und kann von [GitHub](https://github.com/Microsoft/SmartHotel360) heruntergeladen werden. Es ist eine ASP.NET-Anwendung, die mit einer SQL Server-Datenbank verbunden ist. In den in diesen Artikeln beschriebenen Szenarien wird die aktuelle Version dieser Anwendung auf zwei VMware-VMs mit Windows Server 2008 R2 und SQL Server 2008 R2 bereitgestellt. Diese Anwendungs-VMs werden lokal gehostet und von vCenter Server verwaltet.

**osTicket:** Dies ist eine unter Linux ausgeführte Open-Source-Anwendung für Service Desk-Tickets. Sie können es von [GitHub](https://github.com/osTicket/osTicket) herunterladen. In den in diesen Artikeln beschriebenen Szenarien wird die aktuelle Version dieser Anwendung lokal auf zwei VMware-VMs mit Ubuntu 16.04 LTS unter Verwendung von Apache 2, PHP 7.0 und MySQL 5.7 bereitgestellt.
