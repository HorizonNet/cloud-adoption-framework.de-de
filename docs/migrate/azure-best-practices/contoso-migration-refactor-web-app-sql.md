---
title: Migrieren einer App zu Azure App Service und SQL-Datenbank
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie eine App umgestalten, indem Sie sie zu Azure App Service und Azure SQL-Datenbank migrieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: d56c39085124c821f7989389cda9aea7e4673141
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86234768"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc smarthotel SHWEB SHWCF -->

# <a name="migrate-an-application-to-azure-app-service-and-sql-database"></a>Migrieren einer App zu Azure App Service und SQL-Datenbank

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso eine Windows .NET-App mit zwei Ebenen, die auf VMware-VMs ausgeführt wird, als Teil einer Migration zu Azure umgestaltet. Das Unternehmen migriert die App-Front-End-VM zu einer Azure App Service-Web-App und die App-Datenbank zu einer Azure SQL-Datenbank-Instanz.

Die in diesem Beispiel verwendete SmartHotel360-Anwendung wird quelloffen bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und damit steigt die Last auf den lokalen Systeme und Infrastrukturen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigerung der Flexibilität.**  Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Es darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Anwendung** | Die App wird in Azure so wichtig bleiben wie heute. <br><br> Sie sollte die gleichen Leistungsmerkmale wie aktuell in VMware aufweisen. <br><br> Das Team möchte nicht in die App investieren. Im Moment möchten die Administratoren die App sicher in die Cloud verschieben. <br><br> Die Unterstützung für Windows Server 2008 R2, die Version, unter der die App derzeit ausgeführt wird, möchte das Team einstellen. <br><br> Das Team möchte SQL Server 2008 R2 generell nicht mehr verwenden und zu einer modernen PaaS-Datenbankplattform wechseln, die den Verwaltungsaufwand minimiert. <br><br> Seine Investitionen in die SQL Server-Lizenzierung und in die Software Assurance möchte Contoso nutzen, wo immer dies möglich ist. <br><br> Darüber hinaus möchte Contoso die Auswirkungen des Single Point of Failure in der Webebene abschwächen. |
| **Einschränkungen** | Die App besteht aus einer ASP.NET-App und einem WCF-Dienst, die auf derselben VM ausgeführt werden. Sie möchten diese Komponenten mithilfe von Azure App Service auf zwei Web-Apps verteilen. |
| **Azure** | Contoso möchte die App zu Azure migrieren, jedoch nicht auf VMs ausführen. Sowohl in der Web- als auch in der Datenschicht soll auf Azure-PaaS-Dienste zurückgegriffen werden. |
| **DevOps** | Contoso möchte auf ein DevOps-Modell umsteigen und Azure DevOps für Builds und Releasepipelines verwenden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-application"></a>Aktuelle Anwendung

- Die lokale App SmartHotel360 ist auf zwei VMs aufgeteilt (`WEBVM` und `SQLVM`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Für die Datenbankebene der App verglich Contoso mithilfe [dieses Artikels](https://docs.microsoft.com/azure/sql-database/sql-database-features) Azure SQL-Datenbank mit SQL Server. Die Entscheidung für Azure SQL-Datenbank hat für Contoso verschiedene Gründe:
  - Azure SQL-Datenbank ist ein verwalteter relationaler Datenbankdienst. Er bietet eine vorhersagbare Leistung auf mehreren Serviceleveln bei nahezu keinem Administrationsaufwand. Zu den Vorteilen gehören dynamische Skalierbarkeit ohne Ausfallzeiten, integrierte intelligente Optimierung sowie globale Skalierbarkeit und Verfügbarkeit.
  - Contoso kann den einfachen Datenmigrations-Assistenten (DMA) nutzen, um die Migration der lokalen Datenbank zu Azure SQL-Datenbank zu bewerten.
  - Contoso kann Azure Database Migration Service verwenden, um lokale Datenbanken zu Azure SQL zu migrieren.
  - Mit der Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen für eine SQL-Datenbank-Instanz austauschen. So sind Einsparungen von bis zu 30 Prozent möglich.
  - SQL-Datenbank bietet verschiedene Sicherheitsfeatures, darunter Always Encrypted, dynamische Datenmaskierung und Sicherheit bzw. SQL-Bedrohungserkennung auf Zeilenebene.
- Für die Webebene der App hat sich Contoso dazu entschieden, Azure App Service zu verwenden. Über diesen PaaS-Dienst kann die App mit nur wenigen Konfigurationsänderungen bereitgestellt werden. Contoso führt die Änderung mit Visual Studio durch und stellt zwei Web-Apps bereit. Eine für die Website, und eine für den WCF-Dienst.
- Contoso hat sich dazu entschieden, Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys zu verwenden, um die Anforderungen einer DevOps-Pipeline zu erfüllen. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service bereitgestellt.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Der Code der SmartHotel360-App erfordert für die Migration zu Azure keine Änderungen. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für SQL Server und Windows Server nutzen. <br><br> Nach der Migration muss Windows Server 2008 R2 nicht unterstützt werden. Weitere Informationen finden Sie in der [Microsoft Lifecycle-Richtlinie](https://aka.ms/lifecycle). <br><br> Contoso kann die Webebene der App mit mehreren Instanzen konfigurieren, sodass sie kein Single Point of Failure mehr ist. <br><br> Die Datenbank ist nicht mehr auf das veraltete SQL Server 2008 R2 angewiesen. <br><br> SQL-Datenbank unterstützt die technischen Anforderungen. Contoso bewertete die lokale Datenbank mithilfe des Datenmigrations-Assistenten und stellte fest, dass sie kompatibel ist. <br><br> Azure SQL-Datenbank verfügt über eine integrierte Fehlertoleranz, die Contoso nicht einrichten muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist. <br><br> Wenn Contoso Azure Database Migration Service für die Migration der Datenbank verwendet, verfügt das Unternehmen über die entsprechende Infrastruktur für die Migration umfangreicher Datenbanken. |
| **Nachteile** | Azure App Service unterstützt nur eine App-Bereitstellung für jede Web-App. Dies bedeutet, dass zwei Web-Apps bereitgestellt werden müssen (eine für die Website und eine für den WCF-Dienst). |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Szenarioarchitektur](./media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt eine Azure SQL-Instanz bereit und migriert mithilfe von Azure Database Migration Service die Datenbank von SmartHotel360 dorthin.
2. Nach der Bereitstellung und Konfiguration von Web-Apps stellt Contoso die App SmartHotel360 in diesen bereit.

    ![Migrationsprozess](./media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Datenmigrations-Assistent (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso verwendet den DMA zum Bewerten und Erkennen von Kompatibilitätsproblemen, die sich auf die Funktionalität ihrer Datenbank in Azure auswirken könnten. Der DMA bewertet die Featureparität zwischen SQL-Quellen und -Zielen, und empfiehlt Verbesserungen der Leistung und Zuverlässigkeit. | Sie können das Tool kostenlos herunterladen. |
| [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen bei minimaler Ausfallzeit. | Informieren Sie sich über die [unterstützten Regionen](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Azure SQL-Datenbank](https://docs.microsoft.com/azure/azure-sql/database/sql-database-paas-overview) | Ein intelligenter, vollständig verwalteter Dienst für relationale Clouddatenbanken. | Die Kosten ergeben sich durch Features, Durchsatz und Größe. [Weitere Informationen](https://azure.microsoft.com/pricing/details/sql-database/managed) |
| [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Es wird gezeigt, wie leistungsstarke Cloud-Apps auf einer vollständig verwalteten Plattform erstellt werden können. | Die Kosten basieren auf Größe, Standort und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |
| [Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Stellt die Pipeline für Continuous Integration und Continuous Deployment (CI/CD) für die App-Entwicklung bereit. Die Pipeline beginnt bei einem Git-Repository für die Verwaltung von App-Code, einem Buildsystem zum Erstellen von Paketen und anderen Buildartefakten sowie einem Releaseverwaltungssystem zum Bereitstellen von Änderungen in Entwicklungs-, Test- und Produktionsumgebungen. |

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | [Weitere Informationen](./contoso-migration-infrastructure.md) zur Vorgehensweise von Contoso beim Einrichten einer Azure-Infrastruktur. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen einer SQL-Datenbankinstanz in Azure.** Contoso stellt eine SQL-Instanz in Azure bereit. Nachdem die App-Website zu Azure migriert wurde, verweist die Web-App für den WCF-Dienst auf diese Instanz.
> - **Schritt 2: Bewerten der Datenbank mit dem Datenmigrations-Assistenten (DMA) von Azure und Migration mit Azure Database Migration Service** Contoso bewertet die Datenbank für die Migration und migriert dann die Anwendungsdatenbank mit Azure Database Migration Service.
> - **Schritt 3: Bereitstellen von Web-Apps.** Contoso stellt die beiden Web-Apps bereit.
> - **Schritt 4: Einrichten von Azure DevOps.** Contoso erstellt ein neues Azure DevOps-Projekt und importiert das Git-Repository.
> - **Schritt 5: Konfigurieren von Verbindungszeichenfolgen.** Contoso konfiguriert Verbindungszeichenfolgen, damit die Web-App auf Webebene, die Web-App für den WCF-Dienst und die SQL-Instanz kommunizieren können.
> - **Schritt 6: Einrichten von Build- und Releasepipelines.** Als letzten Schritt richtet Contoso Build- und Releasepipelines zum Erstellen der App ein und stellt sie in zwei separaten Web-Apps bereit.

## <a name="step-1-provision-azure-sql-database"></a>Schritt 1: Bereitstellen einer Azure SQL-Datenbank

1. Die Administratoren von Contoso entscheiden sich dafür, eine Azure SQL-Datenbank-Instanz zu erstellen.

    ![Bereitstellen von SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. Das Unternehmen gibt einen Datenbanknamen an, der mit der Datenbank übereinstimmt, die auf der lokalen VM (`SmartHotel.Registration`) ausgeführt wird. Die Datenbank wird dann in der `ContosoRG`-Ressourcengruppe platziert. Dies ist die Ressourcengruppe, die das Unternehmen für die Produktionsressourcen in Azure verwendet.

    ![Bereitstellen einer Azure SQL-Datenbank-Instanz](./media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. Das Unternehmen richtet eine neue SQL Server-Instanz (`sql-smarthotel-eus2`) in der primären Region ein.

    ![Bereitstellen von SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. Den Tarif legt das Unternehmen entsprechend seiner Server- und Datenbankanforderungen fest. Zudem entscheidet es sich, Geld mit dem Azure-Hybridvorteil zu sparen, da es bereits über eine SQL Server-Lizenz verfügen.
5. Zur Größenanpassung nutzt es das auf virtuellen Kernen basierende Kaufmodell und legt die Grenzwerte für seine erwarteten Anforderungen fest.

    ![Bereitstellen von SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. Dann erstellt Contoso die Datenbankinstanz.

    ![Bereitstellen von SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. Nach dem Erstellen der Instanz öffnet ein Unternehmensmitarbeiter die Datenbank und notiert sich Details, die für die Migration mit dem Datenmigrations-Assistenten benötigt werden.

    ![Bereitstellen von SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Benötigen Sie weitere Hilfe?**

- [Erhalten Sie Hilfe](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) bei der Bereitstellung einer SQL-Datenbank-Instanz.
- Erfahren Sie mehr zu den [Ressourcenlimits für virtuelle Kerne](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools).

## <a name="step-2-assess-the-database-using-data-migration-assistant-dma-and-migrate-it-using-azure-database-migration-service"></a>Schritt 2: Bewerten der Datenbank mit dem Datenmigrations-Assistenten (DMA) und Migration mit Azure Database Migration Service

Contoso-Administratoren bewerten die Datenbank mithilfe des Datenbankmigrations-Assistenten (DMA) und migrieren sie anschließend anhand des [Tutorials: Onlinemigration von SQL Server zu einer Einzel- oder Pooldatenbank in Azure SQL-Datenbank mit DMS](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online) mithilfe von Azure Database Migration Service. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) ausführen.

Zusammenfassend müssen Sie die folgenden Schritte ausführen:

- Nutzen Sie den Datenmigrations-Assistenten (DMA) zum Ermitteln und Beheben aller Probleme bei der Datenbankmigration.
- Erstellen Sie eine Azure Database Migration Service-Instanz mit einer `Premium`-SKU, die mit dem VNet verbunden ist.
- Vergewissern Sie sich, dass die Instanz über das virtuelle Netzwerk auf die SQL Server-Remoteinstanz zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu SQL Server auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem SQL Server gehostet ist, zugelassen werden.
- Konfigurieren der Instanz:
  - Erstellen Sie ein Migrationsprojekt.
  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.
  - Wählen Sie ein Ziel aus.
  - Wählen Sie die zu migrierenden Datenbanken aus.
  - Konfigurieren Sie die erweiterten Einstellungen.
  - Starten Sie die Replikation.
  - Beheben Sie alle Fehler.
  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.

## <a name="step-3-provision-web-apps"></a>Schritt 3: Bereitstellen von Web-Apps

Nachdem die Datenbank migriert wurde, können die Administratoren von Contoso die beiden Web-Apps bereitstellen.

1. Das Unternehmen wählt **Web-App** im Portal aus.

    ![Web-App](./media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. Das Unternehmen gibt einen Namen für die Web-App an (`SHWEB-EUS2`), führt die App unter Windows aus und platziert sie in der Produktionsressourcengruppe `ContosoRG`. Es wird eine neue Web-App und ein Azure App Service-Plan erstellt.

    ![Web-App](./media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. Nachdem die Web-App bereitgestellt wurde, wird der Prozess zum Erstellen einer Web-App für den WCF-Dienst (`SHWCF-EUS2`) wiederholt.

    ![Web-App](./media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. Anschließend navigiert Contoso zu der Adresse der Apps, um zu überprüfen, ob diese erfolgreich erstellt wurden.

## <a name="step-4-set-up-azure-devops"></a>Schritt 4: Einrichten von Azure DevOps

Contoso muss die DevOps-Infrastruktur und die Pipelines für die Anwendung erstellen. Hierzu erstellen die Administratoren von Contoso ein neues DevOps-Projekt, importieren ihren Code und richten anschließend die Build- und Releasepipelines ein.

1. In der Azure DevOps-Organisation von Contoso erstellen sie ein neues Projekt (`ContosoSmartHotelRefactor`) und wählen anschließend **Git** für die Versionskontrolle aus.

    ![Neues Projekt](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. Sie importieren das Git-Repository, das derzeit ihren App-Code enthält. Der Code befindet sich in einem [öffentlichen GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Registration) und kann heruntergeladen werden.

    ![Herunterladen des App-Codes](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. Nach dem Importieren des Codes verknüpfen sie Visual Studio mit dem Repository und klonen den Code mithilfe von Team Explorer.

    ![Herstellen einer Verbindung mit dem Projekt](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. Nachdem das Repository auf dem Entwicklercomputer geklont wurde, öffnen sie die Projektmappendatei für die App. Die Datei enthält jeweils ein eigenes Projekt für die Web-App und den WCF-Dienst.

    ![Projektmappendatei](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Schritt 5: Konfigurieren von Verbindungszeichenfolgen

Die Administratoren von Contoso müssen sicherstellen, dass die Web-Apps und die Datenbank kommunizieren können. Zu diesem Zweck konfiguriert das Unternehmen Verbindungszeichenfolgen im Code und in den Web-Apps.

1. In der Web-App für den WCF-Dienst (`SHWCF-EUS2`) fügt Contoso unter **Einstellungen** > **Anwendungseinstellungen** eine neue Verbindungszeichenfolge mit dem Namen `DefaultConnection` hinzu.
2. Die Verbindungszeichenfolge wird von der Datenbank `SmartHotel-Registration` abgerufen und sollte mit den entsprechenden Anmeldeinformationen aktualisiert werden.

    ![Verbindungszeichenfolge](./media/contoso-migration-refactor-web-app-sql/string1.png)

3. Sie öffnen in Visual Studio das Projekt `SmartHotel.Registration.wcf` in der Projektmappendatei. Der `connectionStrings`-Bereich der `web.config`-Datei für den WCF-Dienst `SmartHotel.Registration.wcf` sollte mit der Verbindungszeichenfolge aktualisiert werden.

     ![Verbindungszeichenfolge](./media/contoso-migration-refactor-web-app-sql/string2.png)

4. Der Abschnitt `client` der Datei `web.config` für `SmartHotel.registration.web` sollte dahingehend geändert werden, dass er auf den neuen Speicherort des WCF-Diensts verweist. Dies ist die URL der WCF-Web-App, die den Dienstendpunkt hostet.

    ![Verbindungszeichenfolge](./media/contoso-migration-refactor-web-app-sql/strings3.png)

5. Nachdem die Änderungen im Code vorgenommen wurden, müssen die Administratoren die Änderungen committen. Sie führen Commit und Synchronisierung mithilfe von Team Explorer in Visual Studio durch.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps

Als Nächstes konfigurieren die Contoso-Administratoren Azure DevOps für die Durchführung des Build- und Releasevorgangs.

1. Dazu wählen sie in Azure DevOps **Build und Release** > **Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. Sie wählen **Azure Repos Git** und das entsprechende Repository aus.

    ![Git und Repository](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. Unter **Vorlage auswählen** wählen sie die ASP.NET-Vorlage für ihren Build aus.

     ![ASP.NET-Vorlage](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Der Name `ContosoSmartHotelRefactor-ASP.NET-CI` wird für den Build verwendet. Wählen Sie **Speichern und in Warteschlange einreihen** aus.

     ![Speichern und in Warteschlange einreihen](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Dies startet den ersten Build. Sie wählen die Buildnummer aus, um den Prozess zu überwachen. Nachdem dieser abgeschlossen ist, können sie das Prozessfeedback sehen und **Artefakte** auswählen, um die Buildergebnisse zu überprüfen.

    ![Überprüfung](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. Der Ordner **Drop** enthält die Buildergebnisse.

    - Die beiden ZIP-Dateien sind die Pakete, die die Apps enthalten.
    - Diese Dateien werden in der Releasepipeline für die Bereitstellung in Azure App Service verwendet.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. Ein Mitarbeiter klickt auf **Releases** >  **+ Neue Pipeline**.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. Sie wählen die Bereitstellungsvorlage für Azure App Service aus.

    ![Bereitstellungsvorlage für Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. Er benennt die Releasepipeline mit `ContosoSmartHotel360Refactor` und gibt den Namen der WCF-Web-App (`SHWCF-EUS2`) für den **Phasennamen** ein.

    ![Environment](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. Sie klicken unter den Phasen auf **1 Auftrag, 1 Aufgabe**, um die Bereitstellung des WCF-Diensts zu konfigurieren.

    ![Bereitstellen von WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. Er überprüft, ob das Abonnement ausgewählt und autorisiert ist, und klickt dann auf den **App Service-Namen**.

     ![Auswählen des Namens des App-Diensts](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. In der Pipeline klickt er dann unter **Artefakte** auf **Artefakt hinzufügen** und wählt für den Build die Pipeline `ContosoSmarthotel360Refactor` aus.

     ![Entwickeln](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. Sie überprüfen, ob das Blitzsymbol des ausgewählten Artefakts aktiviert ist, um den Continuous Deployment-Trigger zu aktivieren.

     ![Blitzsymbol](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. Der Continuous Deployment-Trigger sollte außerdem auf **Aktiviert** festgelegt sein.

    ![Continuous Deployment aktiviert](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Jetzt navigiert er zurück zur Phase **1 Auftrag, 1 Aufgabe** und klickt anschließend auf **Azure App Service bereitstellen**.

    ![Bereitstellen von Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. Er sucht unter **Datei oder Ordner suchen** die Datei `SmartHotel.Registration.Wcf.zip`, die während der Erstellung erstellt wurde, und klickt anschließend auf **Speichern**.

    ![Speichern von WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. Er klickt auf **Pipeline** > **Phasen**, **+ Hinzufügen**, um eine Umgebung für `SHWEB-EUS2` hinzuzufügen. Sie wählen eine weitere Azure App Service-Bereitstellung aus.

    ![Hinzufügen einer Umgebung](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. Der Prozess wird wiederholt, um die Datei der Web-App (`SmartHotel.Registration.Web.zip`) in der korrekten Web-App zu veröffentlichen.

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

An dieser Stelle wurde die Anwendung erfolgreich zu Azure migriert.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die folgenden Schritte zur Bereinigung ausführen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Entfernen der VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation zur Anzeige der neuen Speicherorte für die App SmartHotel360. Anzeigen, dass die Datenbank in Azure SQL-Datenbank und das Front-End in zwei Web-Apps ausgeführt wird.
- Überprüfen sämtlicher Ressourcen, die mit den außer Betrieb genommenen VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass seine neue `SmartHotel-Registration`-Datenbank geschützt ist. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Insbesondere sollte Contoso die Web-Apps für die Verwendung von SSL mit Zertifikaten aktualisieren.

### <a name="backups"></a>Backups

- Contoso muss die Sicherungsanforderungen für Azure SQL-Datenbank überprüfen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Contoso muss sich auch über die Verwaltung von Sicherungen und Wiederherstellungen in SQL-Datenbank informieren. [Erfahren Sie mehr über automatische Sicherungen.](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Contoso sollte die Implementierung von Failovergruppen erwägen, um ein regionales Failover für die Datenbank bereitzustellen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)
- Contoso muss hinsichtlich der Resilienz die Bereitstellung der Web-App in der Hauptregion (`East US 2`) und der sekundären Region (`Central US`) in Erwägung ziehen. Contoso könnte den Traffic Manager konfigurieren, um ein Failover während regionaler Ausfälle sicherzustellen.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über EA verrechnet.
- Contoso verwendet [Azure Cost Management und das Azure-Abrechnungsportal](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

Im vorliegenden Artikel hat Contoso die App SmartHotel360 in Azure umgestaltet, indem das Unternehmen die Front-End-VM der App mithilfe zweier Azure App Service-Web-Apps migriert hat. Die Anwendungsdatenbank wurde zu einer Azure SQL-Datenbank-Instanz migriert.
