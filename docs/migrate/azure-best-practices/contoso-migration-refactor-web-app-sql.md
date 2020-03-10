---
title: Umgestalten einer App durch die Migration zu Azure App Service und Azure SQL-Datenbank
description: Dieser Artikel enthält Informationen darüber, wie Contoso einer lokalen App einen neuen Host zuweist, indem diese zu einer Azure App Service-Web-App und einer Azure SQL Server-Datenbank migriert wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 3667207de8cc31a85e12666c425ffdf0469c1be5
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223069"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost contosodc vcenter smarthotel SHWEB SHWCF -->

# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-database"></a>Umgestalten einer lokalen App zu einer Azure App Service-Web-App und einer Azure SQL-Datenbank-Instanz

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso eine zweistufigen Windows.NET-App, die auf VMware-VMs ausgeführt wird, als Teil einer Migration der App-VMs auf Azure umgestaltet. Das Unternehmen migriert die App-Front-End-VM zu einer Azure App Service-Web-App und die App-Datenbank zu einer Azure SQL-Datenbank-Instanz.

Die in diesem Beispiel verwendet SmartHotel360-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und damit steigt die Last auf den lokalen Systeme und Infrastrukturen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigerung der Flexibilität.**  Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Es darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**App** | Die App wird in Azure so wichtig bleiben wie heute.<br/><br/> Sie sollte die gleichen Leistungsmerkmale wie aktuell in VMware aufweisen.<br/><br/> Das Team möchte nicht in die App investieren. Im Moment möchten die Administratoren die App lediglich sicher in die Cloud verschieben.<br/><br/> Die Unterstützung für Windows Server 2008 R2, unter dem die App derzeit läuft, möchte das Team einstellen.<br/><br/> Das Team möchte weg von SQL Server 2008 R2 und hin zu einer modernen PaaS-Datenbankplattform, die den Verwaltungsaufwand minimiert.<br/><br/> Seine Investitionen in die SQL Server-Lizenzierung und in die Software Assurance möchte Contoso nutzen, wo immer dies möglich ist.<br/><br/> Darüber hinaus möchte Contoso die Auswirkungen des Single Point of Failure in der Webebene abschwächen.
**Einschränkungen** | Die App besteht aus einer ASP.NET-App und einem WCF-Dienst, die auf derselben VM ausgeführt werden. Über den Azure App Service soll dies auf zwei Web-Apps aufgeteilt werden.
**Azure** | Contoso möchte die App zu Azure migrieren, jedoch nicht auf VMs ausführen. Sowohl in der Web- als auch in der Datenschicht soll auf Azure-PaaS-Dienste zurückgegriffen werden.
**DevOps** | Contoso möchte auf ein DevOps-Modell umsteigen und Azure DevOps für Builds und Releasepipelines verwenden.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-app"></a>Aktuelle App

- Die lokale App SmartHotel360 ist auf zwei VMs aufgeteilt (WEBVM und SQLVM).
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5)
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (contoso-datacenter) mit einem lokalen Domänencontroller (**contosodc1**).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Für die Datenbankebene der App verglich Contoso mithilfe [dieses Artikels](https://docs.microsoft.com/azure/sql-database/sql-database-features) Azure SQL-Datenbank mit SQL Server. Die Entscheidung für Azure SQL-Datenbank hat für Contoso verschiedene Gründe:
  - Azure SQL-Datenbank ist ein verwalteter Dienst für relationale Datenbanken. Er bietet eine vorhersagbare Leistung auf mehreren Serviceleveln bei nahezu keinem Administrationsaufwand. Zu den Vorteilen gehören dynamische Skalierbarkeit ohne Ausfallzeiten, integrierte intelligente Optimierung sowie globale Skalierbarkeit und Verfügbarkeit.
  - Contoso kann den einfachen Datenmigrations-Assistenten (DMA) nutzen, um die lokale Datenbank zu bewerten und zu Azure SQL-Datenbank zu migrieren.
  - Mit der Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen für eine SQL-Datenbank-Instanz austauschen. So sind Einsparungen von bis zu 30 % möglich.
  - SQL-Datenbank bietet verschiedene Sicherheitsfeatures, darunter Always Encrypted, dynamische Datenmaskierung und Sicherheit bzw. Bedrohungserkennung auf Zeilenebene.
- Für die Webebene der App hat sich Contoso dazu entschieden, Azure App Service zu verwenden. Über diesen PaaS-Dienst kann die App mit nur wenigen Konfigurationsänderungen bereitgestellt werden. Contoso führt die Änderung mit Visual Studio durch und stellt zwei Web-Apps bereit. Eine für die Website, und eine für den WCF-Dienst.
- Um die Anforderungen einer DevOps-Pipeline zu erfüllen, hat Contoso sich dazu entschieden, Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys zu verwenden. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service bereitgestellt.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | Der Code der App SmartHotel360 muss für die Migration zu Azure nicht geändert werden.<br/><br/> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für SQL Server und Windows Server nutzen.<br/><br/> Nach der Migration muss Windows Server 2008 R2 nicht unterstützt werden. [Weitere Informationen](https://support.microsoft.com/lifecycle)<br/><br/> Contoso kann die Webebene der App mit mehreren Instanzen konfigurieren, sodass sie kein Single Point of Failure mehr ist.<br/><br/> Die Datenbank ist nicht mehr auf das veraltete SQL Server 2008 R2 angewiesen.<br/><br/> SQL-Datenbank unterstützt die technischen Anforderungen. Contoso bewertete die lokale Datenbank mithilfe des Datenmigrations-Assistenten und stellte fest, dass sie kompatibel ist.<br/><br/> Azure SQL-Datenbank verfügt über eine integrierte Fehlertoleranz, die Contoso nicht einrichten muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist.
**Nachteile** | Azure App Service unterstützt nur eine App-Bereitstellung für jede Web-App. Dies bedeutet, dass zwei Web-Apps bereitgestellt werden müssen (eine für die Website und eine für den WCF-Dienst).<br/><br/> Wenn Contoso anstelle des Azure Database Migration Service den Datenmigrations-Assistenten zur Migration der Datenbank verwendet, verfügt das Unternehmen nicht über die entsprechende Infrastruktur für die Migration umfangreicher Datenbanken. Contoso muss eine andere Region erstellen, um ein Failover zu gewährleisten, wenn die primäre Region nicht verfügbar ist.

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Szenarioarchitektur](media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt eine Azure SQL-Instanz bereit und migriert die Datenbank von SmartHotel360 dorthin.
2. Nach der Bereitstellung und Konfiguration von Web-Apps stellt Contoso die App SmartHotel360 in diesen bereit.

    ![Migrationsprozess](media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Datenmigrations-Assistent (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso verwendet den DMA zum Bewerten und Erkennen von Kompatibilitätsproblemen, die sich auf die Funktionalität ihrer Datenbank in Azure auswirken könnten. Der DMA bewertet die Featureparität zwischen SQL-Quellen und -Zielen, und empfiehlt Verbesserungen der Leistung und Zuverlässigkeit. | Sie können das Tool kostenlos herunterladen.
[Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database) | Ein intelligenter, vollständig verwalteter Dienst für relationale Clouddatenbanken. | Die Kosten ergeben sich durch Features, Durchsatz und Größe. [Weitere Informationen](https://azure.microsoft.com/pricing/details/sql-database/managed)
[Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Es wird gezeigt, wie leistungsstarke Cloud-Apps auf einer vollständig verwalteten Plattform erstellt werden können. | Die Kosten basieren auf Größe, Standort und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows)
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Stellt die Pipeline für Continuous Integration und Continuous Deployment (CI/CD) für die App-Entwicklung bereit. Die Pipeline beginnt bei einem Git-Repository für die Verwaltung von App-Code, einem Buildsystem zum Erstellen von Paketen und anderen Buildartefakten sowie einem Releaseverwaltungssystem zum Bereitstellen von Änderungen in Entwicklungs-, Test- und Produktionsumgebungen.

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes:

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.
**Azure-Infrastruktur** | [Weitere Informationen](./contoso-migration-infrastructure.md) zur Vorgehensweise von Contoso beim Einrichten einer Azure-Infrastruktur.

<!--markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen einer SQL-Datenbankinstanz in Azure.** Contoso stellt eine SQL-Instanz in Azure bereit. Nachdem die App-Website zu Azure migriert wurde, verweist die Web-App für den WCF-Dienst auf diese Instanz.
> - **Schritt 2: Migrieren der Datenbank mit dem DMA.** Contoso migriert die App-Datenbank mit dem Datenmigrations-Assistenten.
> - **Schritt 3: Bereitstellen von Web-Apps.** Contoso stellt die beiden Web-Apps bereit.
> - **Schritt 4: Einrichten von Azure DevOps.** Contoso erstellt ein neues Azure DevOps-Projekt und importiert das Git-Repository.
> - **Schritt 5: Konfigurieren von Verbindungszeichenfolgen.** Contoso konfiguriert Verbindungszeichenfolgen, damit die Web-App auf Webebene, die Web-App für den WCF-Dienst und die SQL-Instanz kommunizieren können.
> - **Schritt 6: Einrichten von Build- und Releasepipelines.** Als letzten Schritt richtet Contoso Build- und Releasepipelines zum Erstellen der App ein und stellt sie in zwei separaten Web-Apps bereit.

## <a name="step-1-provision-an-azure-sql-database"></a>Schritt 1: Bereitstellen einer Azure SQL-Datenbank-Instanz

1. Die Administratoren von Contoso entscheiden sich dafür, eine SQL-Datenbank-Instanz in Azure zu erstellen.

    ![Bereitstellen von SQL](media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. Das Unternehmen gibt einen Datenbanknamen an, der mit der Datenbank übereinstimmt, die auf der lokalen VM (**SmartHotel.Registration**) ausgeführt wird. Die Datenbank wird dann in der ContosoRG-Ressourcengruppe platziert. Dies ist die Ressourcengruppe, die das Unternehmen für die Produktionsressourcen in Azure verwendet.

    ![Bereitstellen von SQL](media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. Das fiktive Unternehmen richtet eine neue SQL Server-Instanz (**sql-smarthotel-eus2**) in der primären Region ein.

    ![Bereitstellen von SQL](media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. Den Tarif legt das Unternehmen entsprechend seiner Server- und Datenbankanforderungen fest. Zudem entscheidet es sich, Geld mit dem Azure-Hybridvorteil zu sparen, da es bereits über eine SQL Server-Lizenz verfügen.
5. Zur Größenanpassung nutzt es das auf virtuellen Kernen basierende Kaufmodell und legt die Grenzwerte für seine erwarteten Anforderungen fest.

    ![Bereitstellen von SQL](media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. Dann erstellt Contoso die Datenbankinstanz.

    ![Bereitstellen von SQL](media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. Nach dem Erstellen der Instanz öffnet das Unternehmen die Datenbank und notiert sich Details, die es für die Migration mit dem Datenmigrations-Assistenten benötigt.

    ![Bereitstellen von SQL](media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Benötigen Sie weitere Hilfe?**

- [Erhalten Sie Hilfe](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) bei der Bereitstellung einer SQL-Datenbank-Instanz.
- [Erfahren Sie mehr](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) zu Ressourcengrenzwerten des auf virtuellen Kernen basierenden Kaufmodells.

## <a name="step-2-migrate-the-database-with-dma"></a>Schritt 2: Migrieren der Datenbank mit dem DMA

Die Administratoren von Contoso migrieren die Datenbank von SmartHotel360 mit dem DMA.

### <a name="install-dma"></a>Installieren des DMA

1. Es lädt das Tool aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) auf die lokale SQL Server-VM (**SQLVM**) herunter.
2. Es führt das Setup (DownloadMigrationAssistant.msi) auf der VM aus.
3. Auf der Seite **Fertigstellen** wählen sie **Launch Microsoft Data Migration Assistant** (Microsoft-Datenmigrations-Assistenten starten) aus, bevor sie den Assistenten beenden.

### <a name="migrate-the-database-with-dma"></a>Migrieren der Datenbank mit dem DMA

1. Sie erstellen im DMA ein neues Projekt (**SmartHotelDB**) und wählen anschließend **Migration** aus.
2. Als Quellservertyp wird **SQL Server** und als Ziel **Azure SQL-Datenbank** ausgewählt.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-1.png)

3. In den Migrationsdetails fügt das Unternehmen **SQLVM** als Quellserver und die **SmartHotel.Registration**-Datenbank als Ziel hinzu.

     ![DMA](media/contoso-migration-refactor-web-app-sql/dma-2.png)

4. Ein Fehler wird angezeigt, der anscheinend mit der Authentifizierung zusammenhängt. Beim Ermitteln der Ursache wird jedoch festgestellt, dass das Problem durch den Punkt (.) im Datenbanknamen verursacht wird. Daher wurde beschlossen, eine neue SQL-Datenbank-Instanz mit dem Namen **SmartHotel-Registration** bereitzustellen, um das Problem zu beheben. Beim erneuten Ausführen des DMA können sie **SmartHotel-Registration** auswählen, und der Assistent kann fortgesetzt werden.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-3.png)

5. Unter **Objekte auswählen** wählt das Unternehmen die Datenbanktabellen aus und generiert ein SQL-Skript.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-4.png)

6. Nachdem das Skript durch den DMA erstellt wurde, wählen Sie **Schema bereitstellen** aus.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-5.png)

7. Der DMA bestätigt, dass die Bereitstellung erfolgreich war.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-6.png)

8. Jetzt kann mit der Migration begonnen werden.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-7.png)

9. Nach Abschluss der Migration können die Administratoren von Contoso überprüfen, ob die Datenbank auf der Azure SQL-Datenbank-Instanz ausgeführt wird.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-8.png)

10. Die zusätzliche SQL-Datenbank-Instanz **SmartHotel.Registration** wird von Contoso im Azure-Portal gelöscht.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-9.png)

## <a name="step-3-provision-web-apps"></a>Schritt 3: Bereitstellen von Web-Apps

Nachdem die Datenbank migriert wurde, können die Administratoren von Contoso die beiden Web-Apps bereitstellen.

1. Das Unternehmen wählt **Web-App** im Portal aus.

    ![Web-App](media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. Es gibt einen App-Namen an (**SHWEB-EUS2**), führt die App unter Windows aus und platziert sie in der Produktionsressourcengruppe **ContosoRG**. Es wird eine neue Web-App und ein Azure App Service-Plan erstellt.

    ![Web-App](media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. Nachdem die Web-App bereitgestellt wurde, wird der Prozess zum Erstellen einer Web-App für den WCF-Dienst (**SHWCF-EUS2**) wiederholt.

    ![Web-App](media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. Anschließend navigiert Contoso zu der Adresse der Apps, um zu überprüfen, ob diese erfolgreich erstellt wurden.

## <a name="step-4-set-up-azure-devops"></a>Schritt 4: Einrichten von Azure DevOps

Contoso muss die DevOps-Infrastruktur und die Pipelines für die Anwendung erstellen. Hierzu erstellen die Administratoren von Contoso ein neues DevOps-Projekt, importieren ihren Code und richten anschließend die Build- und Releasepipelines ein.

1. Im Azure DevOps-Konto von Contoso erstellen sie ein neues Projekt (**ContosoSmartHotelRefactor**) und wählen anschließend **Git** für die Versionskontrolle aus.

    ![Neues Projekt](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. Sie importieren das Git-Repository, das derzeit ihren App-Code enthält. Der Code befindet sich in einem [öffentlichen Repository](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) und kann heruntergeladen werden.

    ![Herunterladen des App-Codes](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. Nach dem Importieren des Codes verknüpfen sie Visual Studio mit dem Repository und klonen den Code mithilfe von Team Explorer.

    ![Herstellen einer Verbindung mit dem Projekt](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. Nachdem das Repository auf dem Entwicklercomputer geklont wurde, öffnen sie die Projektmappendatei für die App. Die Datei enthält jeweils ein eigenes Projekt für die Web-App und den WCF-Dienst.

    ![Projektmappendatei](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Schritt 5: Konfigurieren von Verbindungszeichenfolgen

Die Administratoren von Contoso müssen sicherstellen, dass die Web-Apps und die Datenbank kommunizieren können. Zu diesem Zweck konfiguriert das Unternehmen Verbindungszeichenfolgen im Code und in den Web-Apps.

1. In der Web-App für den WCF-Dienst (**SHWCF-EUS2**) fügt Contoso unter **Einstellungen** > **Anwendungseinstellungen** eine neue Verbindungszeichenfolge mit dem Namen  **DefaultConnection** hinzu.
2. Die Verbindungszeichenfolge wird von der Datenbank **SmartHotel Registrierung** abgerufen und sollte mit den entsprechenden Anmeldeinformationen aktualisiert werden.

    ![Verbindungszeichenfolge](media/contoso-migration-refactor-web-app-sql/string1.png)

3. Sie öffnen in Visual Studio das Projekt **SmartHotel.Registration.wcf** in der Projektmappendatei. Der Abschnitt **connectionStrings** der Datei „web.config“ für den WCF-Dienst „SmartHotel.Registration.Wcf“ sollte mit der Verbindungszeichenfolge aktualisiert werden.

     ![Verbindungszeichenfolge](media/contoso-migration-refactor-web-app-sql/string2.png)

4. Der Abschnitt **client** der Datei „web.config“ für SmartHotel.Registration.Web sollte dahingehend geändert werden, dass es auf den neuen Speicherort des WCF-Diensts verweist. Dies ist die URL der WCF-Web-App, die den Dienstendpunkt hostet.

    ![Verbindungszeichenfolge](media/contoso-migration-refactor-web-app-sql/strings3.png)

5. Nachdem die Änderungen im Code vorgenommen wurden, müssen die Administratoren die Änderungen committen. Sie führen Commit und Synchronisierung mithilfe von Team Explorer in Visual Studio durch.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps

Als Nächstes konfigurieren die Contoso-Administratoren Azure DevOps für die Durchführung des Build- und Releasevorgangs.

1. Dazu wählen sie in Azure DevOps **Build und Release** > **Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. Sie wählen **Azure Repos Git** und das entsprechende Repository aus.

    ![Git und Repository](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. Unter **Vorlage auswählen** wählen sie die ASP.NET-Vorlage für ihren Build aus.

     ![ASP.NET-Vorlage](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Für den Build wird der Name **ContosoSmartHotelRefactor-ASP.NET-CI** verwendet. Wählen Sie **Speichern und in Warteschlange einreihen** aus.

     ![Speichern und in Warteschlange einreihen](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Dies startet den ersten Build. Sie wählen die Buildnummer aus, um den Prozess zu überwachen. Nachdem dieser abgeschlossen ist, können sie das Prozessfeedback sehen und **Artefakte** auswählen, um die Buildergebnisse zu überprüfen.

    ![Überprüfung](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. Der Ordner **Drop** enthält die Buildergebnisse.

    - Die beiden ZIP-Dateien sind die Pakete, die die Apps enthalten.
    - Diese Dateien werden in der Releasepipeline für die Bereitstellung in Azure App Service verwendet.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. Sie wählen **Releases** >  **+ Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. Sie wählen die Bereitstellungsvorlage für Azure App Service aus.

    ![Bereitstellungsvorlage für Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. Sie benennen die Releasepipeline mit **ContosoSmartHotel360Refactor** und geben den Namen der WCF-Web-App („SHWCF-EUS2“) für den **Phasennamen** ein.

    ![Environment](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. Sie klicken unter den Phasen auf **1 Auftrag, 1 Aufgabe**, um die Bereitstellung des WCF-Diensts zu konfigurieren.

    ![Bereitstellen von WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. Sie überprüfen, ob das Abonnement ausgewählt und autorisiert ist, und wählen **App Service-Name** aus.

     ![Auswählen des Namens des App-Diensts](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. In der Pipeline klicken sie dann unter **Artefakte** auf **+ Add an artifact** (+ Artefakt hinzufügen) und wählen für den Build die Pipeline **ContosoSmarthotel360Refactor** aus.

     ![Entwickeln](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. Sie klicken auf das Blitzsymbol des ausgewählten Artefakts, um den Continuous Deployment-Trigger zu aktivieren.

     ![Blitzsymbol](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. Der Continuous Deployment-Trigger sollte außerdem auf **Aktiviert** festgelegt sein.

    ![Continuous Deployment aktiviert](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Jetzt navigieren sie zurück zur Phase „1 Auftrag, 1 Aufgabe“ und wählen anschließend **Azure App Service bereitstellen** aus.

    ![Bereitstellen von Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. Sie suchen unter **Datei oder Ordner auswählen** die Datei **SmartHotel.Registration.Wcf.zip**, die während der Erstellung erstellt wurde, und wählen anschließend **Speichern** aus.

    ![Speichern von WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. Sie wählen **Pipeline** > **Phasen** > **+ Hinzufügen** aus, um eine Umgebung für **SHWEB-EUS2** hinzuzufügen. Sie wählen eine weitere Azure App Service-Bereitstellung aus.

    ![Hinzufügen einer Umgebung](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. Anschließend wiederholen sie den Prozess zum Veröffentlichen der Web-App-Datei (**SmartHotel.Registration.Web.zip**), um die Web-App zu korrigieren.

    ![Veröffentlichen der Web-App](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

19. Nach dem Speichern wird die Releasepipeline wie folgt angezeigt.

     ![Releasepipeline – Zusammenfassung](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

20. Sie wechseln zurück zum **Build** und klicken auf **Trigger** > **Continuous Integration aktivieren**. Dies aktiviert die Pipeline. Wenn also Änderungen am Code committet werden, erfolgt ein vollständiger Build mit Release.

    ![Aktivieren von Continuous Integration](./media/contoso-migration-refactor-web-app-sql/pipeline20.png)

21. Sie klicken auf **Speichern und in Warteschlange einreihen**, um die vollständige Pipeline auszuführen. Es wird ein neuer Build ausgelöst, der wiederum das erste Release der App in Azure App Service erstellt.

    ![Speichern der Pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline21.png)

22. Die Administratoren von Contoso können die Verarbeitung von Build- und Releasepipeline in Azure DevOps überwachen. Nachdem der Build abgeschlossen wurde, startet die Veröffentlichung.

    ![Erstellen und veröffentlichen der App](./media/contoso-migration-refactor-web-app-sql/pipeline22.png)

23. Nachdem die Pipeline abgeschlossen wurde, sind beide Websites bereitgestellt, und die App wird online ausgeführt.

    ![Abschließen der Veröffentlichung](./media/contoso-migration-refactor-web-app-sql/pipeline23.png)

An dieser Stelle wurde die App erfolgreich zu Azure migriert.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die folgenden Schritte zur Bereinigung ausführen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Entfernen der VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation zur Anzeige der neuen Speicherorte für die App SmartHotel360 Anzeigen, dass die Datenbank in Azure SQL-Datenbank und das Front-End in zwei Web-Apps ausgeführt wird.
- Überprüfen sämtlicher Ressourcen, die mit den außer Betrieb genommenen VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss gewährleisten, dass seine neue Datenbank **SmartHotel-Registration** sicher ist. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Insbesondere sollte Contoso die Web-Apps für die Verwendung von SSL mit Zertifikaten aktualisieren.

### <a name="backups"></a>Backups

- Contoso muss die Sicherungsanforderungen für Azure SQL-Datenbank überprüfen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Contoso muss sich auch über die Verwaltung von Sicherungen und Wiederherstellungen in SQL-Datenbank informieren. [Erfahren Sie mehr über automatische Sicherungen.](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Contoso sollte die Implementierung von Failovergruppen erwägen, um ein regionales Failover für die Datenbank bereitzustellen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)
- Contoso muss hinsichtlich der Resilienz die Bereitstellung der Web-App in der Hauptregion „USA, Osten 2“ und „USA, Mitte“ in Erwägung ziehen. Contoso könnte den Traffic Manager konfigurieren, um ein Failover bei regionalen Ausfällen sicherzustellen.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über EA verrechnet.
- Contoso aktiviert Azure Cost Management. Es ist durch Cloudyn lizenziert, ein Tochterunternehmen von Microsoft. Dabei handelt es sich um eine Kostenverwaltungslösung mit mehreren Clouds, die Ihnen das Verwenden und Verwalten von Azure und anderen Cloudressourcen erleichtert. [Erfahren Sie mehr](https://docs.microsoft.com/azure/cost-management/overview) über die Azure Cost Management.

## <a name="conclusion"></a>Zusammenfassung

Im vorliegenden Artikel hat Contoso die App SmartHotel360 in Azure umgestaltet, indem das Unternehmen die Front-End-VM der App mithilfe zweier Azure App Service-Web-Apps migriert hat. Die App-Datenbank wurde zu einer Azure SQL-Datenbank-Instanz migriert.
