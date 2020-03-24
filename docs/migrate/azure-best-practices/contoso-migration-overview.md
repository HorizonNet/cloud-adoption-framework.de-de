---
title: Beispiele für die Anwendungsmigration für Azure
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die lokale Infrastruktur zur Microsoft Azure-Cloud migrieren können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ecb6cfc10b88490269b50a5fe6bec7d2c3277d7b
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312769"
---
# <a name="application-migration-patterns-and-examples"></a>Anwendungsmuster für die Migration und Beispiele

Dieser Abschnitt des Cloud Adoption Framework enthält Beispiele für mehrere gängige Migrationsszenarien und zeigt, wie Sie lokale Infrastrukturen in die [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure) Cloud migrieren können.

## <a name="introduction"></a>Einführung

Azure bietet Zugriff auf einen umfassenden Satz von Clouddiensten. Als Entwickler und IT-Spezialisten können Sie diese Dienste zum Erstellen, Bereitstellen und Verwalten von Anwendungen für verschiedene Tools und Frameworks über ein globales Netzwerk von Rechenzentren verwenden. Im Rahmen der Herausforderungen, die Ihr Unternehmen in Bezug auf die digitalen Veränderungen bewältigen muss, können Sie mithilfe der Azure-Cloud ermitteln, wie Sie Ressourcen und Vorgänge optimieren, sich mit Ihren Kunden und Mitarbeitern vernetzen und Ihre Produkte transformieren.

Es ist aber auch klar, dass viele Organisationen trotz aller Vorteile, die sich mit der Cloud in Bezug auf Geschwindigkeit und Flexibilität, Kostensenkung, Leistung und Zuverlässigkeit ergeben, noch längere Zeit lokale Rechenzentren betreiben müssen. Als Antwort auf die Hürden, die bei der Umstellung auf die Cloud überwunden werden müssen, verfügt Azure über eine Hybrid Cloud-Strategie, bei der Brücken zwischen Ihren lokalen Rechenzentren und der öffentlichen Azure-Cloud gebildet werden. Beispiele hierfür sind die Verwendung von Azure-Cloudressourcen, z.B. Azure Backup zum Schützen von lokalen Ressourcen, oder der Einsatz von Azure-Analysen, um Erkenntnisse zu lokalen Workloads zu erhalten.

Im Rahmen der Hybrid Cloud-Strategie werden für Azure kontinuierlich erweiterte Lösungen zum Migrieren von lokalen Apps und Workloads in die Cloud bereitgestellt. Sie können Ihre lokalen Ressourcen mit einfachen Schritten umfassend bewerten, um zu ermitteln, wie sie in der Azure-Cloud ausgeführt werden. Nachdem Sie über eine ausführliche Bewertung verfügen, können Sie die Migration der Ressourcen zu Azure beruhigt angehen. Wenn die Ressourcen in Azure aktiv sind und ausgeführt werden, können Sie sie optimieren, um Zugriff, Flexibilität, Sicherheit und Zuverlässigkeit sicherzustellen und zu verbessern.

## <a name="migration-patterns"></a>Migrationsmuster

Die Strategien für die Migration zur Cloud lassen sich grob in vier Muster unterteilen: Zuweisen eines neuen Hosts, Umgestalten, Umstrukturieren oder Neu erstellen. Welche Strategie Sie übernehmen, richtet sich nach Ihrer Business-Treibern und Migrationszielen. Sie könnten mehrere Muster übernehmen. Zum Beispiel könnten Sie entscheiden, einfachen Apps bzw. Apps, die nicht unternehmenskritisch sind, einen neuen Host zuzuweisen und die Apps umzustrukturieren, die komplexer und unternehmenskritisch sind. Sehen wir uns diese Muster an.

<!-- markdownlint-disable MD033 -->

**Muster** | **Definition** | **Einsatzgebiete**
--- | --- | ---
**Zuweisen eines neuen Hosts** | Häufig als _Lift & Shift_-Migration bezeichnet. Diese Option erfordert keine Änderungen des Codes und ermöglicht Ihnen die schnelle Migration Ihrer vorhandenen Apps zu Azure. Um die Vorteile der Cloud ohne die mit Änderungen des Codes verbundenen Risiken und Kosten zu nutzen, wird jede App im vorliegenden Zustand migriert. | Wenn Sie Apps schnell in die Cloud verschieben müssen.<br/><br/> Wenn Sie eine App verschieben möchten, ohne sie zu ändern.<br/><br/> Wenn Ihre Apps so überarbeitet sind, dass sie nach der Migration die [Azure-IaaS](https://azure.microsoft.com/overview/what-is-iaas)-Skalierbarkeit nutzen können.<br/><br/> Wenn Apps für Ihr Unternehmen wichtig sind, aber keine unmittelbaren Änderungen der App-Funktionen erforderlich sind.
**Umgestalten** | Die häufig als „Umpacken“ bezeichnete Umgestaltung erfordert nur minimale Änderungen der Apps, sodass sie eine Verbindung mit [Azure-PaaS](https://azure.microsoft.com/overview/what-is-paas) herstellen und Cloudangebote verwenden können.<br/><br/> Sie könnten Ihre vorhandenen Apps beispielsweise zu Azure App Service oder Azure Kubernetes Service (AKS) migrieren.<br/><br/> Alternativ könnten Sie relationale und nicht relationale Datenbanken für die verwaltete Azure SQL-Datenbank-Instanz, Azure Database for MySQL, Azure Database for PostgreSQL und Azure Cosmos DB umgestalten. | Wenn Ihre App einfach zum Arbeiten in Azure umgepackt werden kann.<br/><br/> Wenn Sie innovative, von Azure bereitgestellte DevOps-Methoden anwenden möchten oder erwägen, DevOps mit einer Containerstrategie für Workloads zu verwenden.<br/><br/> Für die Umgestaltung müssen Sie die Portabilität Ihrer vorhandenen Codebasis und verfügbare Entwicklungsfertigkeiten berücksichtigen.
**Überarbeiten** | Beim Überarbeiten für die Migration liegt der Fokus auf dem Ändern und Erweitern von App-Funktionalität und Codebasis, um die App-Architektur für die Cloudskalierbarkeit zu optimieren.<br/><br/> Sie könnten z.B. eine monolithische Anwendung in eine Gruppe von Microservices unterteilen, die zusammenarbeiten und einfach zu skalieren sind.<br/><br/> Alternativ könnten Sie auch Ihre relationalen und nicht relationalen Datenbanken zu einer vollständig verwalteten Datenbanklösung umstrukturieren, z.B. die verwaltete Azure SQL-Datenbank-Instanz, Azure Database for MySQL, Azure Database for PostgreSQL und Azure Cosmos DB. | Wenn Ihre Apps eine größere Überarbeitung benötigen, um neue Funktionen zu integrieren oder effektiv auf einer Cloudplattform zu funktionieren.<br/><br/> Wenn Sie vorhandene Anwendungsinvestitionen nutzen, Skalierbarkeitsanforderungen erfüllen, innovative DevOps-Methoden anwenden und die Verwendung virtueller Computer minimieren möchten.
**Neuerstellen** | Das Neuerstellen geht einen Schritt weiter, da eine App in diesem Fall unter Verwendung von Azure-Cloudtechnologien von Grund auf neu erstellt wird.<br/><br/> Sie könnten beispielsweise Greenfield-Apps mit [nativen Cloudtechnologien](https://azure.com/cloudnative) wie Azure Functions, Azure KI, verwalteten Azure SQL-Datenbank-Instanzen und Azure Cosmos DB erstellen. | Wenn Sie schnelle Entwicklung wünschen und Funktionalität sowie Lebensdauer vorhandener Apps eingeschränkt sind.<br/><br/> Wenn Sie bereit sind, Business-Innovation (einschließlich von Azure bereitgestellter DevOps-Methoden) voranzutreiben, neue Anwendungen mit nativen Cloudtechnologien zu erstellen und die Weiterentwicklungen in KI, Blockchain und IoT zu nutzen.

<!-- markdownlint-enable MD033 -->

## <a name="migration-example-articles"></a>Artikel mit Migrationsbeispielen

Dieser Abschnitt enthält Beispiele für mehrere gängige Migrationsszenarien. Jedes Beispiel enthält Hintergrundinformationen und detailreiche Bereitstellungsszenarien, in denen die Einrichtung einer Migrationsinfrastruktur veranschaulicht und die Eignung der lokalen Ressourcen für die Migration bewertet wird. Diesem Abschnitt werden im Laufe der Zeit weitere Artikel hinzugefügt.

![Gängige Migrations-/Modernisierungsprojekte](./media/migration-patterns.png)

*Kategorien der gängigen Migrations-/Modernisierungsprojekte.*

Die Artikel der Reihe werden unten zusammengefasst.

- Die einzelnen Migrationsszenarien basieren auf geringfügig variierten Geschäftszielen, die die Migrationsstrategie bestimmen.
- Für die einzelnen Bereitstellungsszenarien erhalten Sie Informationen zu Business-Treibern und Zielen, einer vorgeschlagenen Architektur, Schritten zum Ausführen der Migration sowie Empfehlungen zur Bereinigung und den nächsten Schritten nach Abschluss der Migration.

### <a name="assessment"></a>Bewertung

**Artikel** | **Details**
--- | ---
[Bewerten der lokalen Ressourcen für die Migration zu Azure](../../plan/contoso-migration-assessment.md) | In diesem Artikel zu bewährten Methoden der Planmethodik wird erläutert, wie Sie eine Bewertung einer lokalen App ausführen, die unter VMware ausgeführt wird. In diesem Artikel bewertet eine Beispielorganisation virtuelle Computer der App mit dem Azure Migrate-Dienst und die SQL Server-Datenbank der App mit dem Datenmigrations-Assistenten.

### <a name="infrastructure"></a>Infrastruktur

**Artikel** | **Details**
--- | ---
[Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) | Der Artikel zeigt, wie eine Organisation seine lokale Infrastruktur und die Azure-Infrastruktur für die Migration vorbereitet. Auf das in diesem Artikel festgelegte Infrastrukturbeispiel wird in den anderen in diesem Abschnitt bereitgestellten Beispielen verwiesen.

### <a name="windows-server-workloads"></a>Windows Server-Workloads

**Artikel** | **Details**
--- | ---
[Zuweisen eines neuen Hosts für ein App auf Azure-VMs](./contoso-migration-rehost-vm.md) | Dieser Artikel enthält ein Beispiel für die Migration von lokalen App-VMs auf Azure-VMs mit dem Site Recovery-Dienst.
[Umstrukturieren einer App in einen Azure-Container und Azure SQL-Datenbank](./contoso-migration-rearchitect-container-sql.md) | Dieser Artikel enthält ein Beispiel für die Migration einer App beim Umstrukturieren der App-Webschicht zu einem Windows-Container, der in Azure Service Fabric ausgeführt wird, und der Datenbank zu einer Azure SQL-Datenbank.

### <a name="linux-workloads"></a>Linux-Workloads

**Artikel** | **Details**
--- | ---
[Zuweisen eines neuen Hosts für eine Linux-App auf virtuellen Azure-Computern und Azure Database for MySQL](./contoso-migration-rehost-linux-vm-mysql.md) | Dieser Artikel enthält ein Beispiel für die Migration einer von Linux gehosteten Anwendung auf Azure-VMs mithilfe von Site Recovery. Die App-Datenbank wird zu Azure Database for MySQL migriert, indem MySQL Workbench verwendet wird.
[Zuweisen eines neuen Hosts für eine Linux-App auf Azure-VMs](./contoso-migration-rehost-linux-vm.md) | Dieses Beispiel zeigt, wie Sie eine „Lift and Shift“-Migration einer Linux-basierten App auf Azure-VMs mit dem Site Recovery-Dienst durchführen können.

### <a name="sql-server-workloads"></a>SQL Server-Workloads

**Artikel** | **Details**
--- | ---
[Zuweisen eines neuen Hosts für eine App auf einer Azure-VM und einer verwalteten Azure SQL-Datenbank-Instanz](./contoso-migration-rehost-vm-sql-managed-instance.md) | Dieser Artikel enthält ein Beispiel für eine „Lift and Shift“-Migration zu Azure für eine lokale App. Dazu gehört die Migration der Front-End-VM der App mithilfe von [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) und der App-Datenbank mithilfe von [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) zu einer verwalteten Azure-SQL-Datenbank-Instanz.
[Zuweisen eines neuen Hosts für eine App auf Azure-VMs und in einer SQL Server Always On-Verfügbarkeitsgruppe](./contoso-migration-rehost-vm-sql-ag.md) | Dieses Beispiel zeigt, wie Sie eine App und Daten mit von Azure gehosteten SQL Server-VMs migrieren können. Dabei wird Site Recovery verwendet, um die App-VMs zu migrieren, und der Azure Database Migration Service, um die App-Datenbank zu einem SQL Servercluster zu migrieren, das durch eine Always On-Verfügbarkeitsgruppe geschützt wird.

### <a name="aspnet-php-and-java-apps"></a>ASP.NET-, PHP- und Java-Apps

**Artikel** | **Details**
--- | ---
[Umgestalten einer App in eine Azure-Web-App und in Azure SQL-Datenbank](./contoso-migration-refactor-web-app-sql.md) | Dieses Beispiel zeigt, wie Sie eine lokale Windows-basierte App in eine Azure-Web-App migrieren und die App-Datenbank mit dem Datenmigrations-Assistenten in eine Azure SQL Server-Instanz migrieren.
[Umgestalten einer Linux-App für mehrere Regionen mit Azure App Service, Traffic Manager und Azure Database for MySQL](./contoso-migration-refactor-linux-app-service-mysql.md) | Dieses Beispiel zeigt, wie Sie eine lokale Linux-basierte App mit dem Azure Traffic Manager, der in GitHub für Continuous Delivery integriert ist, in mehreren Azure-Regionen auf eine Azure-Web-App migrieren können. Die App-Datenbank wird zu einer Azure Database for MySQL-Instanz migriert.
[Neuerstellen einer lokalen App in Azure](./contoso-migration-rebuild.md) | Dieser Artikel enthält ein Beispiel für das Neuerstellen einer lokalen App mit einer Reihe von Azure-Funktionen und verwalteten Diensten, einschließlich Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services und Azure Cosmos DB.
[Umgestalten von Team Foundation Server in Azure DevOps Services](./contoso-migration-tfs-vsts.md) | Dieser Artikel zeigt eine Beispielmigration einer lokalen Team Foundation Server-Bereitstellung zu Azure DevOps Services in Azure.

### <a name="migration-scaling"></a>Migrationskalierung

**Artikel** | **Details**
--- | ---
[Skalieren einer Migration zu Azure](./contoso-migration-scale.md) | Dieser Artikel zeigt, wie eine Beispielorganisation die Skalierung auf eine vollständige Migration zu Azure vorbereitet.

### <a name="demo-apps"></a>Demo-Apps

Die in diesem Abschnitt aufgeführten Beispielartikel verwenden zwei Demo-Apps: SmartHotel360 und osTicket.

- **SmartHotel360:** Diese App wurde von Microsoft als Test-App entwickelt, die Sie beim Arbeiten mit Azure verwenden können. Sie wird als Open-Source-App bereitgestellt und kann von [GitHub](https://github.com/Microsoft/SmartHotel360) heruntergeladen werden. Es ist eine ASP.NET-App, die mit einer SQL Server-Datenbank verbunden ist. In den in diesen Artikeln beschriebenen Szenarien wird die aktuelle Version dieser App auf zwei VMware-VMs mit Windows Server 2008 R2 und SQL Server 2008 R2 bereitgestellt. Diese App-VMs werden lokal gehostet und von vCenter Server verwaltet.
- **osTicket:** Dies ist eine unter Linux ausgeführte Open-Source-App für Service Desk-Tickets. Sie können es von [GitHub](https://github.com/osTicket/osTicket) herunterladen. In den in diesen Artikeln beschriebenen Szenarien wird die aktuelle Version dieser App lokal auf zwei VMware-VMs mit Ubuntu 16.04 LTS unter Verwendung von Apache 2, PHP 7.0 und MySQL 5.7 bereitgestellt.
