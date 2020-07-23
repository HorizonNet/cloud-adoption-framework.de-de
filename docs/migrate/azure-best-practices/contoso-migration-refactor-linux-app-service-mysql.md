---
title: Umgestalten einer Linux-Anwendung zu Azure App Service, Traffic Manager und Azure Database for MySQL
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie eine Linux-Service Desk-App in Azure App Service und Azure Database for MySQL umgestalten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 18512a360213ab979ace853492d553149432c464
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86234904"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc OSTICKETWEB OSTICKETMYSQL osTicket contosoosticket trafficmanager InnoDB binlog DBHOST DBUSER CNAME -->

# <a name="refactor-a-linux-application-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Umgestalten einer Linux-Anwendung für mehrere Regionen mit Azure App Service, Traffic Manager und Azure Database for MySQL

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso eine [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung mit zwei Ebenen umgestaltet und sie mithilfe von Azure App Service mit GitHub-Integration und Azure Database for MySQL aus einer lokalen Umgebung zu Azure migriert.

Die in diesem Beispiel verwendete Service Desk-Anwendung osTicket wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie aus dem [osTicket-Repository in GitHub](https://github.com/osTicket/osTicket) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam hat in enger Zusammenarbeit mit Geschäftspartnern seine Ziele festgelegt:

- **Unternehmenswachstum.** Contoso wächst und erschließt neue Märkte. Das Unternehmen benötigt zusätzliche Kundendienstmitarbeiter.
- **Skalierung.** Die Lösung soll erstellt werden, damit Contoso beim Ausbau der Geschäftsbereiche weitere Kundendienstmitarbeiter einstellen kann.
- **Verbesserte Resilienz:** In der Vergangenheit waren nur interne Benutzer von Problemen mit dem System betroffen. Beim neuen Geschäftsmodell wirken sich diese auch auf externe Benutzer aus, und Contoso muss sicherstellen, dass die Anwendung jederzeit verfügbar ist.

## <a name="migration-goals"></a>Migrationsziele

Für die Bestimmung der besten Migrationsmethode hat das Contoso-Cloudteam Ziele für diese Migration festgelegt:

- Eine Skalierung der Anwendung sollte über die aktuelle lokale Kapazität und Leistung hinaus möglich sein. Contoso verschiebt die Anwendung, um die Vorteile der bedarfsgesteuerten Skalierung von Azure zu nutzen.
- Contoso möchte die Codebasis der Anwendung in eine Continuous Delivery-Pipeline verschieben. Da Anwendungsänderungen nach GitHub gepusht werden, möchte Contoso diese Änderungen bereitstellen, ohne dass zusätzliche Aufgaben für das Betriebspersonal anfallen.
- Die Anwendung muss widerstandsfähig sein und über Wachstums- und Failovermöglichkeiten verfügen. Die Anwendung soll in zwei verschiedenen Azure-Regionen bereitgestellt und automatisch skaliert werden.
- Contoso möchte die Administratoraufgaben für die Datenbank minimieren, nachdem die Anwendung in die Cloud verschoben wird.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

## <a name="current-architecture"></a>Aktuelle Architektur

- Die Anwendung ist auf zwei VMs aufgeteilt (`OSTICKETWEB` und `OSTICKETMYSQL`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).

![Aktuelle Architektur](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Die vorgeschlagene Architektur sieht wie folgt aus:

- Die Anwendung auf Webebene auf `OSTICKETWEB` wird durch Erstellen einer Azure App Service-Instanz in zwei Azure-Regionen migriert. Azure App Service für Linux wird mit dem PHP 7.0-Docker-Container implementiert.
- Der Anwendungscode wird nach GitHub verschoben, und die Azure App Service-Web-App wird für Continuous Delivery mit GitHub konfiguriert.
- Azure App Service wird sowohl in der primären Region (`East US 2`) als auch der sekundären Region (`Central US`) bereitgestellt.
- Traffic Manager wird vor den beiden Web-Apps in beiden Regionen eingerichtet.
- Traffic Manager wird im Prioritätsmodus konfiguriert, um den Datenverkehr über `East US 2` zu erzwingen.
- Wenn der Azure-App-Server in `East US 2` offline geht, können Benutzer in `Central US` auf die Anwendung zugreifen, für die ein Failover ausgeführt wurde.
- Die Anwendungsdatenbank wird mit Azure Database Migration Service zum Azure Database for MySQL-Dienst migriert. Die lokale Datenbank wird lokal gesichert und direkt in Azure Database for MySQL wiederhergestellt.
- Die Datenbank wird in der primären Region (`East US 2`) im Datenbanksubnetz (`PROD-DB-EUS2`) des Produktionsnetzwerks (`VNET-PROD-EUS2`) platziert:
- Da es sich um die Migration einer Produktionsworkload handelt, befinden sich die Azure-Ressourcen für die Anwendung in der Produktionsressourcengruppe `ContosoRG`.
- Die Traffic Manager-Ressource wird in der Infrastrukturressourcengruppe `ContosoInfraRG` von Contoso bereitgestellt.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Szenarioarchitektur](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

1. Im ersten Schritt richten die Administratoren von Contoso die Azure-Infrastruktur ein – einschließlich der Bereitstellung von Azure App Service-Instanzen, der Einrichtung von Traffic Manager und der Bereitstellung einer Azure Database for MySQL-Instanz.
2. Nachdem sie die Azure-Infrastruktur vorbereitet haben, migrieren sie die Datenbank mithilfe von Azure Database Migration Service.
3. Sobald die Datenbank in Azure ausgeführt wird, richtet Contoso ein privates GitHub-Repository für Azure App Service mit Continuous Delivery ein und lädt es mit der Anwendung osTicket.
4. Im Azure-Portal laden sie die Anwendung von GitHub in den Docker-Container mit Azure App Service.
5. Sie optimieren die DNS-Einstellungen und konfigurieren die automatische Skalierung für die Anwendung.

![Migrationsprozess](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure App Service](https://azure.microsoft.com/services/app-service) | Der Dienst wird ausgeführt und skaliert Anwendungen mit dem Azure-PaaS-Dienst für Websites. | Der Preis richtet sich nach der Größe der Instanzen und den benötigten Features. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |
| [Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | Ein Lastenausgleichsmodul, das DNS verwendet, um Benutzer zu Azure oder externen Websites und Diensten zu leiten. | Der Preis richtet sich nach der Anzahl der empfangenen DNS-Abfragen und der Anzahl der überwachten Endpunkte. | [Weitere Informationen](https://azure.microsoft.com/pricing/details/traffic-manager) |
| [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration mehrerer Datenbankquellen zu Azure-Datenplattformen mit minimaler Downtime. | Informieren Sie sich über die [unterstützten Regionen](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Die Datenbank basiert auf der Open-Source-MySQL-Datenbank-Engine. Sie stellt eine vollständig verwaltete, für Unternehmen geeignete MySQL Community-Datenbank für die Entwicklung und Bereitstellung von Anwendungen bereit. | Der Preis richtet sich nach den Compute-, Speicher- und Sicherungsanforderungen. [Weitere Informationen](https://azure.microsoft.com/pricing/details/mysql) |

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Abonnements wurden in einem früheren Artikel dieser Reihe erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen von Azure App Service:** Die Administratoren von Contoso stellen Web-Apps in der primären und sekundären Region bereit.
> - **Schritt 2: Einrichten von Traffic Manager:** Das Unternehmen richtet Traffic Manager vorgelagert vor den Web-Apps ein, um den Datenverkehr zu routen und einen Lastenausgleich auszuführen.
> - **Schritt 3: Bereitstellen von MySQL:** Die Administratoren stellen in Azure eine Instanz von Azure Database for MySQL bereit.
> - **Schritt 4: Migrieren der Datenbank:** Sie migrieren die Datenbank mit Azure Database Migration Service.
> - **Schritt 5: Einrichten von GitHub:** Sie richten ein lokales GitHub-Repository für die Anwendungswebsites bzw. den Anwendungscode ein.
> - **Schritt 6: Bereitstellen der Web-Apps:** Die Web-Apps werden über GitHub bereitgestellt.

## <a name="step-1-provision-azure-app-service"></a>Schritt 1: Bereitstellen von Azure App Service

Die Administratoren von Contoso stellen mithilfe von Azure App Service zwei Web-Apps (jeweils eine pro Region) bereit.

1. Sie erstellen über den Azure Marketplace eine Web-App-Ressource (`osticket-eus2`) in der primären Region (`East US 2`).
2. Sie fügen die Ressource der Produktionsressourcengruppe `ContosoRG` hinzu.

    ![Erstellen einer Web-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. Sie erstellen in der primären Region unter Verwendung der Standardgröße einen App Service-Plan (`APP-SVP-EUS2`).

     ![Wie erstelle ich einen Plan?](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Sie entscheiden sich für ein Linux-Betriebssystem mit PHP 7.0-Laufzeitstapel. Dabei handelt es sich um einen Docker-Container.

    ![Erstellen einer Web-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Sie erstellen eine zweite Web-App (`osticket-cus`) und einen Azure App Service-Plan für `Central US`.

    ![Azure-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Benötigen Sie weitere Hilfe?**

- Erfahren Sie mehr über [Azure App Service-Web-Apps](https://docs.microsoft.com/azure/app-service/overview).
- Erfahren Sie mehr über [Azure App Service unter Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Schritt 2: Einrichten von Traffic Manager

Die Administratoren von Contoso richten Traffic Manager ein, um eingehende Webanforderungen an die Web-Apps weiterzuleiten, die auf der osTicket-Webebene ausgeführt werden.

1. Sie erstellen über den Azure Marketplace eine Traffic Manager-Ressource (`osticket.trafficmanager.net`). Sie verwenden das prioritätsbasierte Routing, sodass `East US 2` der primäre Standort ist. Sie platzieren die Ressource in ihrer Infrastrukturressourcengruppe (`ContosoInfraRG`). Beachten Sie, dass Traffic Manager global und nicht an einen bestimmten Standort gebunden ist.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Als Nächstes konfigurieren sie Traffic Manager mit Endpunkten. Sie fügen die Web-App in `East US 2` als primären Standort (`osticket-eus2`) und die Web-App in `Central US` als sekundären Standort (`osticket-cus`) hinzu.

    ![Hinzufügen von Endpunkten in Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. Nach dem Hinzufügen der Endpunkte können diese überwacht werden.

    ![Überwachen von Endpunkten in Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Benötigen Sie weitere Hilfe?**

- Erfahren Sie mehr über [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Erfahren Sie mehr über das [Routing von Datenverkehr zu einem prioritätsbasierten Endpunkt](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Schritt 3: Bereitstellen von Azure Database for MySQL

Die Administratoren von Contoso stellen eine MySQL-Datenbankinstanz in der primären Region (`East US 2`) bereit.

1. Im Azure-Portal erstellen die Verantwortlichen von Contoso eine Azure Database for MySQL-Ressource.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Sie fügen den Namen `contosoosticket` für die Azure-Datenbank hinzu. Sie fügen die Datenbank der Produktionsressourcengruppe `ContosoRG` hinzu und geben Anmeldeinformationen für sie an.
3. Die lokale MySQL-Datenbank ist in Version 5.7 vorhanden. Deshalb wählen sie diese Version für Kompatibilitätszwecke. Sie verwenden die Standardgrößen, die ihren Datenbankanforderungen entsprechen.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. Bei den **Optionen für Sicherungsredundanz** entscheiden sie sich für die Verwendung von **Georedundanz**. Diese Option ermöglicht es ihnen, die Datenbank bei einem Ausfall in der sekundären Region (`Central US`) wiederherzustellen. Sie können diese Option nur konfigurieren, wenn sie die Datenbank zur Verfügung stellen.

    ![Redundanz](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Sie richten die Verbindungssicherheit ein. Unter „Datenbank > **Verbindungssicherheit**“ richten sie Firewallregeln ein, um der Datenbank den Zugriff auf Azure-Dienste zu ermöglichen.

6. Sie fügen die Client-IP-Adresse der lokalen Arbeitsstation zu den Start- und End-IP-Adressen hinzu. Dadurch können die Web-Apps zusammen mit dem Datenbankclient, der die Migration durchführt, auf die MySQL-Datenbank zugreifen.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Schritt 4: Migrieren der Datenbank

Es gibt mehrere Möglichkeiten, die MySQL-Datenbank zu verschieben. Bei jeder der Optionen müssen Sie für das Ziel eine Azure Database for MySQL-Instanz erstellen. Nach der Erstellung können Sie die Migration auf zweierlei Weise durchführen:

- Schritt 4a: Azure Database Migration Service
- Schritt 4b: Sicherung und Wiederherstellung von MySQL Workbench

### <a name="step-4a-migrate-the-database-via-azure-database-migration-service"></a>Schritt 4a: Migrieren der Datenbank mithilfe von Azure Database Migration Service

Die Administratoren von Contoso migrieren die Datenbank mithilfe von Azure Database Migration Service, indem sie die Schritte im [ausführlichen Migrationstutorial](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) von MySQL 5.6 oder 5.7 ausführen.

> [!NOTE]
> MySQL 8.0 wird in Azure Database for MySQL unterstützt, das Database Migration Service-Tool unterstützt diese Version jedoch noch nicht.

Zusammenfassend müssen Sie die folgenden Schritte ausführen:

- Sicherstellen, dass alle Voraussetzungen für die Migration erfüllt sind:
  - Die Version der MySQL-Datenbankserverquelle muss der von Azure Database for MySQL unterstützten Version entsprechen. Azure Database for MySQL unterstützt die MySQL Community Edition, die InnoDB-Speicher-Engine sowie die Migration zwischen Quellen und Zielen mit derselben Version.
  - Aktivieren Sie die binäre Protokollierung in `my.ini` (Windows) oder `my.cnf` (Unix). Andernfalls tritt im Migrations-Assistenten der folgende Fehler auf: `Error in binary logging. Variable binlog_row_image has value 'minimal'. Please change it to 'full'. For more information, see https://go.microsoft.com/fwlink/?linkid=873009`.
  - Der Benutzer muss über die `ReplicationAdmin`-Rolle verfügen.
  - Migrieren Sie die Datenbankschemas ohne Fremdschlüssel und Trigger.
- Erstellen Sie ein virtuelles Netzwerk, das über ExpressRoute oder VPN mit Ihrem lokalen Netzwerk verbunden ist.
- Erstellen Sie einen Azure Database Migration Service mit einer `Premium`-SKU, der mit dem VNet verbunden ist.
- Vergewissern Sie sich, dass Azure Database Migration Service über das virtuelle Netzwerk auf die MySQL-Datenbank zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu MySQL auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem MySQL gehostet ist, zugelassen werden.
- Ausführen des Database Migration Service-Tools:
  - Erstellen Sie auf der Grundlage der **Premium-SKU** ein Migrationsprojekt.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-new-project.png)

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-new-project-02.png)

  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-source.png)

  - Wählen Sie ein Ziel aus.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-target.png)

  - Wählen Sie die zu migrierenden Datenbanken aus.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-databases.png)

  - Konfigurieren Sie die erweiterten Einstellungen.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-settings.png)

  - Starten Sie die Replikation, und beheben Sie alle Fehler.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-monitor.png)

  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover.png)

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-complete.png)

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-complete-02.png)

  - Setzen Sie alle Fremdschlüssel und Trigger wieder ein.

  - Ändern Sie die Anwendungen so, dass sie die neue Datenbank verwenden.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-apps.png)

### <a name="step-4b-migrate-the-database-mysql-workbench"></a>Schritt 4b: Migrieren der Datenbank (MySQL Workbench)

1. Sie überprüfen die [Voraussetzungen und laden MySQL Workbench herunter](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Die Verantwortlichen bei Contoso installieren MySQL Workbench for Windows entsprechend den [Installationsanweisungen](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Der Computer, auf dem sie die Anwendung installieren, muss für die VM `OSTICKETMYSQL` und Azure über das Internet zugänglich sein.
3. In MySQL Workbench erstellen sie eine MySQL-Verbindung mit `OSTICKETMYSQL`.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. Sie exportieren die Datenbank als `osticket` in eine lokale eigenständige Datei.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. Nachdem die Datenbank lokal gesichert wurde, erstellen sie eine Verbindung mit der Azure Database for MySQL-Instanz.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Nun können sie die Datenbank aus der eigenständigen Datei in die Azure Database for MySQL-Instanz importieren (wiederherstellen). Ein neues Schema (`osticket`) wird für die Instanz erstellt.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. Nach dem Wiederherstellen der Daten können diese mit MySQL Workbench abgefragt und im Azure-Portal angezeigt werden.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Abschließend müssen sie die Datenbankinformationen in den Web-Apps aktualisieren. In der MySQL-Instanz wird **Verbindungszeichenfolge** geöffnet.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. In der Liste der Zeichenfolgen sucht Contoso die Web-App-Einstellungen und wählt diese aus, um sie zu kopieren.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. Contoso öffnet ein Editor-Fenster und fügt die Zeichenfolge in eine neue Datei ein. Dann aktualisiert es diese, damit sie mit der osticket-Datenbank, MySQL-Instanz und Anmeldeinformationseinstellungen übereinstimmt.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. Im Azure-Portal können sie in der **Übersicht** der MySQL-Instanz den Servernamen und die dazugehörigen Anmeldeinformationen überprüfen.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Schritt 5: Einrichten von GitHub

Die Administratoren von Contoso erstellen ein neues privates GitHub-Repository und stellen eine Verbindung mit der osTicket-Datenbank in Azure Database for MySQL her. Anschließend laden sie die Web-App in Azure App Service.

1. Das Unternehmen durchsucht das öffentliche GitHub-Repository der osTicket-Software und forkt es an das GitHub-Konto von Contoso.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. Nach dem Forken navigieren sie zum Ordner `include` und suchen nach der Datei `ost-config.php`.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Die Datei wird im Browser geöffnet und bearbeitet.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. Im Editor aktualisieren sie die Datenbankdetails (insbesondere für `DBHOST` und `DBUSER`).

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Dann führt Contoso für die Änderungen einen Commit aus.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Sie ändern für jede Web-App (`osticket-eus2` und `osticket-cus`) die **Anwendungseinstellungen** im Azure-Portal.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Sie geben die Verbindungszeichenfolge mit dem Namen `osticket` ein und kopieren die Zeichenfolge aus Editor in den **Wertebereich**. Contoso wählt in der Dropdownliste neben der Zeichenfolge **MySQL** aus und speichert die Einstellungen.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Schritt 6: Konfigurieren der Web-Apps:

Im letzten Schritt des Migrationsprozesses konfigurieren die Administratoren von Contoso die Web-Apps mit den osTicket-Websites.

1. In der primären Web-App (`osticket-eus2`) öffnen sie **Bereitstellungsoption** und legen die Quelle auf **GitHub** fest.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Contoso wählt die Bereitstellungsoptionen aus.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. Nach dem Festlegen der Optionen wird die Konfiguration im Azure-Portal als „Ausstehend“ angezeigt.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. Nachdem die Konfiguration aktualisiert wurde und die osTicket-Web-App von GitHub in den Docker-Container mit Azure App Service geladen wurde, wird die Website als „Aktiv“ angezeigt.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Sie wiederholen die obigen Schritte für die sekundäre Web-App (`osticket-cus`).
6. Nachdem die Site konfiguriert wurde, ist sie über das Traffic Manager-Profil erreichbar. Der DNS-Name ist der neue Speicherort der Anwendung osTicket. [Weitere Informationen](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record)

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Contoso wünscht einen DNS-Namen, der leicht zu merken ist. Das Unternehmen erstellt einen Aliasdatensatz (CNAME) `osticket.contoso.com`, der auf den Traffic Manager-Namen im DNS seiner Domänencontroller verweist.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. Die Administratoren konfigurieren die Web-Apps `osticket-eus2` und `osticket-cus`, um die benutzerdefinierten Hostnamen zuzulassen.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Einrichten der automatischen Skalierung

Zum Schluss richten die Administratoren von Contoso die automatische Skalierung für die Anwendung ein. Dadurch wird sichergestellt, dass die Anwendungsinstanzen bei der Verwendung durch Agents entsprechend den geschäftlichen Anforderungen erweitert oder verkleinert werden.

1. In der App Service-Instanz `APP-SVP-EUS2` öffnen sie **Skalierungseinheit**.
2. Sie konfigurieren eine neue Einstellung für die automatische Skalierung mit einer einzigen Regel, die die Anzahl von Instanzen um eins erhöht, wenn der CPU-Prozentsatz für die aktuelle Instanz zehn Minuten lang über 70 Prozent liegt.

    ![Autoscale](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Sie konfigurieren die gleiche Einstellung für `APP-SVP-CUS`, um sicherzustellen, dass bei einem Failover der Anwendung zur sekundären Region das gleiche Verhalten gilt. Der einzige Unterschied ist, dass die Standardinstanz auf 1 gesetzt wird, da dies nur für Failover gilt.

   ![Autoscale](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration wird die Anwendung osTicket in eine Azure App Service-Web-App mit Continuous Delivery mit einem privaten GitHub-Repository umgestaltet. Zur Verbesserung der Resilienz wird die Anwendung in zwei Regionen ausgeführt. Nach der Migration zur PaaS-Plattform wird die osTicket-Datenbank in Azure Database for MySQL ausgeführt.

Zur Bereinigung muss Contoso folgende Schritte ausführen:

- Das Unternehmen entfernt die VMware-VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation und zeigt neue Speicherorte und IP-Adressen an.
- Das Unternehmen überprüft sämtliche Ressourcen, die mit den lokalen VMs interagieren, und aktualisiert sämtliche relevanten Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.
- Es konfiguriert die Überwachung neu, sodass sie auf die URL von `osticket-trafficmanager.net` zeigt, um nachzuverfolgen, ob die Anwendung ausgeführt wird.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die Anwendung jetzt ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso hat die Anwendung auf Sicherheitsprobleme überprüft. Dabei hat es festgestellt, dass die Kommunikation zwischen der Anwendung osTicket und der MySQL-Datenbankinstanz nicht für SSL konfiguriert ist. Das Team muss dies tun, um sicherzustellen, dass der Datenbankverkehr nicht gehackt werden kann. [Weitere Informationen](https://docs.microsoft.com/azure/mysql/howto-configure-ssl)

### <a name="backups"></a>Backups

- Die osTicket-Web-Apps enthalten keine Zustandsdaten und müssen daher auch nicht gesichert werden.
- Das Unternehmen muss die Sicherung für die Datenbank nicht konfigurieren. Azure Database for MySQL erstellt automatisch Serversicherungen und -speicher. Es hat sich für die Georedundanz für die Datenbank entschieden, damit sie robust und einsatzbereit ist. Sicherungen können verwendet werden, um für Ihren Server den Stand zu einem bestimmten Zeitpunkt wiederherzustellen. [Weitere Informationen](https://docs.microsoft.com/azure/mysql/concepts-backup)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Es gibt keine Lizenzierungsprobleme für die PaaS-Bereitstellung.
- Contoso verwendet [Azure Cost Management und die Azure-Abrechnung](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von der IT-Leitung festgelegte Budget nicht überschritten wird.
