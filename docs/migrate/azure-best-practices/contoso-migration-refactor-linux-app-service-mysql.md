---
title: Umgestalten einer Linux-Anwendung zu Azure App Service, Traffic Manager und Azure Database for MySQL
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie eine Linux-Service Desk-App in Azure App Service und Azure Database for MySQL umgestalten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: df3ca412e1cf405a0927e13e5c030da66f4a0e53
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94713631"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc OSTICKETWEB OSTICKETMYSQL osTicket contosoosticket trafficmanager InnoDB binlog DBHOST DBUSER CNAME -->

# <a name="refactor-a-linux-application-by-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Umgestalten einer Linux-Anwendung mithilfe von Azure App Service, Traffic Manager und Azure Database for MySQL

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso eine [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung mit zwei Ebenen umgestaltet und sie mithilfe von Azure App Service mit GitHub-Integration und Azure Database for MySQL aus einer lokalen Umgebung zu Azure migriert.

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
- Die Anwendung muss resilient sein und über Wachstums- und Failovermöglichkeiten verfügen. Die Anwendung soll in zwei verschiedenen Azure-Regionen bereitgestellt und automatisch skaliert werden.
- Contoso möchte die Administratoraufgaben für die Datenbank minimieren, nachdem die Anwendung in die Cloud verschoben wird.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

## <a name="current-architecture"></a>Aktuelle Architektur

- Die Anwendung ist auf zwei virtuelle Computer (VMs) aufgeteilt (`OSTICKETWEB` und `OSTICKETMYSQL`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).

![Diagramm der aktuellen Architektur](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Die vorgeschlagene Architektur sieht wie folgt aus:

- Die Anwendung auf Webebene auf `OSTICKETWEB` wird durch Erstellen einer Azure App Service-Web-App in zwei Azure-Regionen migriert. Das Contoso-Team implementiert Azure App Service für Linux mithilfe des PHP 7.0-Docker-Containers.
- Der Anwendungscode wird nach GitHub verschoben, und die Azure App Service-Web-App wird für Continuous Delivery mit GitHub konfiguriert.
- Azure App Service wird sowohl in der primären Region (`East US 2`) als auch der sekundären Region (`Central US`) bereitgestellt.
- Azure Traffic Manager wird vor den beiden Web-Apps in beiden Regionen eingerichtet.
- Traffic Manager wird im Prioritätsmodus konfiguriert, um den Datenverkehr über `East US 2` zu erzwingen.
- Wenn der Azure-App-Server in `East US 2` offline geht, können Benutzer in `Central US` auf die Anwendung zugreifen, für die ein Failover ausgeführt wurde.
- Die Anwendungsdatenbank wird mit Azure Database Migration Service zum Azure Database for MySQL-Dienst migriert. Die lokale Datenbank wird lokal gesichert und direkt in Azure Database for MySQL wiederhergestellt.
- Die Datenbank wird in der primären Region (`East US 2`) im Datenbanksubnetz (`PROD-DB-EUS2`) des Produktionsnetzwerks (`VNET-PROD-EUS2`) platziert.
- Da es sich um die Migration einer Produktionsworkload handelt, befinden sich die Azure-Ressourcen für die Anwendung in der Produktionsressourcengruppe `ContosoRG`.
- Die Traffic Manager-Ressource wird in der Infrastrukturressourcengruppe `ContosoInfraRG` von Contoso bereitgestellt.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Diagramm der Szenarioarchitektur.](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso schließt den Migrationsprozess wie folgt ab:

1. Im ersten Schritt richten die Administratoren von Contoso die Azure-Infrastruktur ein – einschließlich der Bereitstellung von Azure App Service-Instanzen, der Einrichtung von Traffic Manager und der Bereitstellung einer Azure Database for MySQL-Instanz.
2. Nachdem sie die Azure-Infrastruktur vorbereitet haben, migrieren sie die Datenbank mithilfe von Azure Database Migration Service.
3. Sobald die Datenbank in Azure ausgeführt wird, lädt Contoso ein privates GitHub-Repository für Azure App Service mit Continuous Delivery hoch und lädt es mit der Anwendung osTicket.
4. Im Azure-Portal lädt das Unternehmen die Anwendung von GitHub in den Docker-Container mit Azure App Service.
5. Es optimiert die DNS-Einstellungen und konfiguriert die automatische Skalierung für die Anwendung.

![Diagramm des Contoso-Migrationsprozesses](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure App Service](https://azure.microsoft.com/services/app-service) | Der Dienst wird für die Ausführung und Skalierung von Anwendungen mit dem Azure-Platform-as-a-Service-Dienst (PaaS) für Websites genutzt. | Der Preis richtet sich nach der Größe der Instanzen und den benötigten Features. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |
| [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | Ein Lastenausgleichsmodul, das Domain Name System (DNS) verwendet, um Benutzer zu Azure oder externen Websites und Diensten zu leiten | Der Preis richtet sich nach der Anzahl der empfangenen DNS-Abfragen und der Anzahl der überwachten Endpunkte. | [Weitere Informationen](https://azure.microsoft.com/pricing/details/traffic-manager) |
| [Azure Database Migration Service](/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen bei minimaler Ausfallzeit. | Informieren Sie sich über die [unterstützten Regionen](/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Azure Database for MySQL](/azure/mysql) | Die Datenbank basiert auf der Open-Source-MySQL-Datenbank-Engine. Sie stellt eine vollständig verwaltete, für Unternehmen geeignete MySQL Community-Datenbank für die Entwicklung und Bereitstellung von Anwendungen bereit. | Der Preis richtet sich nach den Compute-, Speicher- und Sicherungsanforderungen. [Weitere Informationen](https://azure.microsoft.com/pricing/details/mysql) |

## <a name="prerequisites"></a>Voraussetzungen

Zum Ausführen dieses Szenarios muss Contoso die folgenden Voraussetzungen erfüllen:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Abonnements wurden in einem früheren Artikel dieser Reihe erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben. |

## <a name="scenario-steps"></a>Szenarioschritte

Im Folgenden sehen Sie den Plan von Contoso zum Abschließen der Migration:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen von Azure App Service**. Die Administratoren von Contoso stellen Web-Apps in der primären und sekundären Region bereit.
> - **Schritt 2: Einrichten von Traffic Manager**. Das Unternehmen richtet Traffic Manager vorgelagert vor den Web-Apps ein, um den Datenverkehr zu routen und einen Lastenausgleich auszuführen.
> - **Schritt 3: Bereitstellen von Azure Database for MySQL**. Die Administratoren stellen in Azure eine Instanz von Azure Database for MySQL bereit.
> - **Schritt 4: Migrieren der Datenbank**. Sie migrieren die Datenbank mithilfe von Azure Database Migration Service.
> - **Schritt 5: Einrichten von GitHub**. Sie richten ein lokales GitHub-Repository für die Anwendungswebsites und den Anwendungscode ein.
> - **Schritt 6: Konfigurieren der Web-Apps**. Sie konfigurieren die Web-Apps mit den osTicket-Websites.

## <a name="step-1-provision-azure-app-service"></a>Schritt 1: Bereitstellen von Azure App Service

Die Administratoren von Contoso stellen mithilfe von Azure App Service zwei Web-Apps (jeweils eine pro Region) bereit.

1. Sie erstellen über den Azure Marketplace eine Web-App-Ressource (`osticket-eus2`) in der primären Region (`East US 2`).
2. Sie fügen die Ressource der Produktionsressourcengruppe `ContosoRG` hinzu.

    ![Screenshot des Bereichs „Web-App“ zum Erstellen einer Web-App in Linux](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. Sie erstellen einen App Service-Plan, **APP-SVP-EUS2**, in der primären Region und verwenden die Standardgröße.

     ![Screenshot des Bereichs „Neuer App Service-Plan“ zum Erstellen eines App Service-Plans](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Sie entscheiden sich für ein Linux-Betriebssystem mit PHP 7.0-Laufzeitstapel. Dabei handelt es sich um einen Docker-Container.

    ![Screenshot des Bereichs „Web-App“ mit dem Linux-Betriebssystem, dem Standort „USA, Osten 2“ und der Auswahl PHP 7.0](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Sie erstellen eine zweite Web-App (**osticket-cus**) und einen Azure App Service-Plan für die Region **USA, Mitte**.

    ![Screenshot des Bereichs „Web-App“ mit dem Linux-Betriebssystem, dem Standort „USA, Mitte“ und der Auswahl PHP 7.0](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Benötigen Sie weitere Hilfe?**

- Erfahren Sie mehr über [Azure App Service-Web-Apps](/azure/app-service/overview).
- Erfahren Sie mehr über [Azure App Service unter Linux](/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Schritt 2: Einrichten von Traffic Manager

Die Administratoren von Contoso richten Traffic Manager ein, um eingehende Webanforderungen an die Web-Apps weiterzuleiten, die auf der osTicket-Webebene ausgeführt werden.

1. Sie erstellen in Azure Marketplace eine Traffic Manager-Ressource (**osticket.trafficmanager.net**). Sie nutzen das prioritätsbasierte Routing, sodass **USA, Osten 2** der primäre Standort ist. Sie platzieren die Ressource in ihrer vorhandenen Infrastrukturressourcengruppe (**ContosoInfraRG**). Beachten Sie, dass Traffic Manager global und nicht an einen bestimmten Standort gebunden ist.

    ![Screenshot des Bereichs „Traffic Manager-Profil erstellen“](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Als Nächstes konfigurieren sie Traffic Manager mit Endpunkten. Die Web-App wird in „USA, Osten 2“ als primärer Standort (**osticket-eus2**) und die Web-App in „USA, Mitte“ als sekundärer Standort (**osticket-cus**) hinzugefügt.

    ![Screenshot des Bereichs „Endpunkt hinzufügen“ in Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. Nachdem die Administratoren die Endpunkte hinzugefügt haben, können sie sie überwachen.

    ![Screenshot des Bereichs „Endpunkte“ zum Überwachen von Endpunkten in Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Benötigen Sie weitere Hilfe?**

- Erfahren Sie mehr über [Traffic Manager](/azure/traffic-manager/traffic-manager-overview).
- Erfahren Sie mehr über das [Routing von Datenverkehr zu einem prioritätsbasierten Endpunkt](/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Schritt 3: Bereitstellen von Azure Database for MySQL

Die Administratoren von Contoso stellen eine MySQL-Datenbankinstanz in der primären Region (USA, Osten 2) bereit.

1. Im Azure-Portal erstellen die Verantwortlichen von Contoso eine Azure Database for MySQL-Ressource.

    ![Screenshot des Links „Azure Database for MySQL“ im Azure-Portal](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Sie fügen den Namen **contosoosticket** für die Azure-Datenbank hinzu. Sie fügen die Datenbank zur Produktionsressourcengruppe **ContosoRG** hinzu, und geben Anmeldeinformationen für sie an.
3. Die lokale MySQL-Datenbank ist in Version 5.7 vorhanden. Deshalb wählen sie diese Version für Kompatibilitätszwecke. Sie verwenden die Standardgrößen, die ihren Datenbankanforderungen entsprechen.

    ![Screenshot des Bereichs „MySQL-Server“ mit Version 5.7](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. Bei den **Optionen für Sicherungsredundanz** entscheiden sie sich für die **Georedundanz**. Mit dieser Option können sie ihre Datenbank in der sekundären Region (USA, Mitte) wiederherstellen, wenn ein Ausfall auftritt. Sie können diese Option nur konfigurieren, wenn sie die Datenbank zur Verfügung stellen.

    ![Screenshot des Bereichs „Optionen für Sicherungsredundanz“ mit der ausgewählten Option „Georedundant“](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Sie richten die Verbindungssicherheit ein. In der Datenbank wählen sie **Verbindungssicherheit** aus und richten Firewallregeln ein, um der Datenbank den Zugriff auf Azure-Dienste zu ermöglichen.

6. Sie fügen die Client-IP-Adresse der lokalen Arbeitsstation zu den Start- und End-IP-Adressen hinzu. Dadurch können die Web-Apps zusammen mit dem Datenbankclient, der die Migration durchführt, auf die MySQL-Datenbank zugreifen.

    ![Screenshot des Bereichs „Verbindungssicherheit“, in dem der Zugriff auf die aktivierten Azure-Dienste und die ausgewählte Client-IP-Adresse angezeigt wird](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Schritt 4: Migrieren der Datenbank

Es gibt mehrere Möglichkeiten, die MySQL-Datenbank zu verschieben. Bei jeder Option müssen die Contoso-Administratoren eine Azure Database for MySQL-Instanz für das Ziel erstellen. Nachdem die Instanz erstellt wurde, können sie die Datenbank mit einem von zwei Pfaden migrieren:

- Schritt 4a: Azure Database Migration Service
- Schritt 4b: Sicherung und Wiederherstellung von MySQL Workbench

### <a name="step-4a-migrate-the-database-via-azure-database-migration-service"></a>Schritt 4a: Migrieren der Datenbank mithilfe von Azure Database Migration Service

Die Administratoren von Contoso migrieren die Datenbank mithilfe von Azure Database Migration Service, indem sie die Schritte im [ausführlichen Migrationstutorial](/azure/dms/tutorial-mysql-azure-mysql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) von MySQL 5.6 oder 5.7 ausführen.

> [!NOTE]
> MySQL 8.0 wird in Azure Database for MySQL unterstützt, das Database Migration Service-Tool unterstützt diese Version jedoch noch nicht.

Contoso geht im Wesentlichen wie folgt vor:

- Das Unternehmen stellt sicher, dass alle Voraussetzungen für die Migration erfüllt sind:
  - Die Version der MySQL-Datenbankserverquelle muss der von Azure Database for MySQL unterstützten Version entsprechen. Azure Database for MySQL unterstützt die MySQL Community Edition, die InnoDB-Speicher-Engine sowie die Migration zwischen Quellen und Zielen mit derselben Version.

  - Es aktiviert die binäre Protokollierung in `my.ini` (Windows) oder `my.cnf` (Unix). Andernfalls tritt im Migrations-Assistenten der folgende Fehler auf:

    „Fehler bei der binären Protokollierung. Die Variable "binlog_row_image" weist den Wert "minimal" auf. Ändern Sie diesen in "full". Weitere Informationen finden Sie unter `https://go.microsoft.com/fwlink/?linkid=873009`.“

  - Der Benutzer muss über die Rolle `ReplicationAdmin` verfügen.

  - Migrieren Sie die Datenbankschemas ohne Fremdschlüssel und Trigger.

- Sie erstellen ein virtuelles privates Netzwerk (VPN), das über ExpressRoute oder VPN mit dem lokalen Netzwerk verbunden ist.

- Sie erstellen eine Azure Database Migration Service-Instanz mit einer Premium-SKU, die mit dem virtuellen Netzwerk verbunden ist.

- Sie vergewissern sich, dass Azure Database Migration Service über das virtuelle Netzwerk auf die MySQL-Datenbank zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu MySQL auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem MySQL gehostet ist, zugelassen werden.

- Sie führen das Database Migration Service-Tool aus und führen anschließend die folgenden Schritte durch:

  a. Sie erstellen auf der Grundlage der Premium-SKU ein Migrationsprojekt.

    ![Screenshot des MySQL-Bereichs „Übersicht“ mit einer Meldung, die angibt, dass der Migrationsdienst erfolgreich erstellt wurde](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-new-project.png)

    ![Screenshot des MySQL-Bereichs „Neues Migrationsprojekt“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-new-project-02.png)

  b. Fügen Sie eine Quelle (lokale Datenbank) hinzu.

    ![Screenshot des Migrations-Assistenten-Bereichs „Quelldetails hinzufügen“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-source.png)

  c. Wählen Sie ein Ziel aus.

    ![Screenshot des Migrations-Assistenten-Bereichs „Zieldetails“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-target.png)

  d. Wählen Sie die zu migrierenden Datenbanken aus.

    ![Screenshot des Migrations-Assistenten-Bereichs „Den Zieldatenbanken zuordnen“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-databases.png)

  e. Konfigurieren Sie die erweiterten Einstellungen.

    ![Screenshot des Migrations-Assistenten-Bereichs „Migrationseinstellungen“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-settings.png)

  f. Starten Sie die Replikation, und beheben Sie alle Fehler.

    ![Screenshot des Bereichs „Serverdetails“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-monitor.png)

  g. Führen Sie den abschließenden Cutover (Systemwechsel) durch.

    ![Screenshot des Bereichs mit osTicket-Details](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover.png)

    ![Screenshot des Bereichs „Umstellung abschließen“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-complete.png)

    ![Screenshot der Statustabelle für Migrationsaktivitäten](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-complete-02.png)

  h. Setzen Sie alle Fremdschlüssel und Trigger wieder ein.

  i. Ändern Sie die Anwendungen so, dass sie die neue Datenbank verwenden.

    ![Screenshot der Statustabelle „Migrationsaktivitäten“](./media/contoso-migration-refactor-linux-app-service-mysql/migration-dms-cutover-apps.png)

### <a name="step-4b-migrate-the-database-mysql-workbench"></a>Schritt 4b: Migrieren der Datenbank (MySQL Workbench)

1. Die Contoso-Administratoren überprüfen die [Voraussetzungen und laden MySQL Workbench herunter](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Die Verantwortlichen bei Contoso installieren MySQL Workbench for Windows entsprechend den [Installationsanweisungen](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Der für die Installation von MySQL Workbench verwendete Computer muss für die OSTICKETMYSQL-VM und Azure über das Internet zugänglich sein.
3. In MySQL Workbench erstellen sie eine MySQL-Verbindung mit OSTICKETMYSQL.

    ![Screenshot des Detailbereichs für die MySQL Workbench-Verbindung](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. Sie exportieren die Datenbank als `osticket` in eine lokale, eigenständige Datei.

    ![Screenshot des MySQL Workbench-Detailbereichs „Daten exportieren“](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. Nachdem die Datenbank lokal gesichert wurde, erstellen die Administratoren eine Verbindung mit der Azure Database for MySQL-Instanz.

    ![Der MySQL Workbench-Bereich „Setup New Connection“ (Neue Verbindung einrichten)](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Nun können sie die Datenbank aus der eigenständigen Datei in die Azure Database for MySQL-Instanz importieren (wiederherstellen). Ein neues Schema (`osticket`) wird für die Instanz erstellt.

    ![Screenshot des MySQL Workbench-Detailbereichs „Daten importieren“](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. Nachdem die Daten wiederhergestellt wurden, können sie von den Administratoren mithilfe von MySQL Workbench abgefragt werden. Die Daten werden im Azure-Portal angezeigt.

    ![Screenshot des Azure-Portals, in dem wiederhergestellte Daten angezeigt werden](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![Screenshot des Blatts „Meine SQL-Datenbanken“ mit einem Pfeil, der auf die osticket-Datenbank zeigt.](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Die Administratoren aktualisieren die Datenbankinformationen in den Web-Apps. In der MySQL-Instanz wird **Verbindungszeichenfolge** geöffnet.

    ![Screenshot des Links „Verbindungszeichenfolgen“ in der MySQL-Instanz.](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. In der Liste mit Verbindungszeichenfolgen wählen sie die Web-App-Einstellungen aus und kopieren sie, indem sie **Klicken Sie zum Kopieren.** auswählen.

    ![Screenshot der Web-App-Einstellungen in der MySQL-Instanz](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. Sie öffnen eine neue Datei in Editor und fügen die Zeichenfolge in die Datei ein. Anschließend aktualisieren sie die Zeichenfolge, damit sie mit der osTicket-Datenbank, der MySQL-Instanz und den Anmeldeinformationseinstellungen übereinstimmt.

    ![Screenshot der in eine Editor-Datei eingefügten Verbindungszeichenfolge](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. Im Azure-Portal können sie im Bereich **Übersicht** der MySQL-Instanz den Servernamen und die dazugehörigen Anmeldeinformationen überprüfen.

    ![Screenshot des Bereichs „Ressourcengruppe“, der den Servernamen und den Anmeldenamen des Serveradministrators anzeigt](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Schritt 5: Einrichten von GitHub

Die Administratoren von Contoso erstellen ein neues privates GitHub-Repository und stellen eine Verbindung mit der osTicket-Datenbank in Azure Database for MySQL her. Anschließend laden sie die Web-App in Azure App Service.

1. Sie durchsuchen das öffentliche GitHub-Repository der osTicket-Software und forken es an das GitHub-Konto von Contoso.

    ![Screenshot der GitHub-Repositoryseite mit der hervorgehobenen Schaltfläche „Fork“](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. Nach dem Forken des Repositorys navigieren sie zum Ordner *include* und suchen anschließend die Datei *ost-config.php* und wählen diese aus.

    ![Screenshot der PHP-Datei in GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Die Datei wird im Browser geöffnet und bearbeitet.

    ![Screenshot des Symbols für die Dateibearbeitung (Stift) in GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. Im Editor aktualisieren die Administratoren die Datenbankdetails (insbesondere für `DBHOST` und `DBUSER`).

    ![Screenshot des Bereichs für die Dateibearbeitung in GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Dann führen sie für die Änderungen einen Commit aus.

    ![Screenshot mit der hervorgehobenen Schaltfläche „Commit für Änderungen ausführen“ im Bearbeitungsbereich](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Sie wählen für jede Web-App (osticket-eus2 und osticket-cus) im Azure-Portal die **Anwendungseinstellungen** im linken Bereich aus und ändern anschließend die Einstellungen.

    ![Screenshot mit dem hervorgehobenen Link „Anwendungseinstellungen“ im Azure-Portal](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Sie geben die Verbindungszeichenfolge mit dem Namen `osticket` ein und kopieren die Zeichenfolge aus Editor in den **Wertebereich**. Contoso wählt in der Dropdownliste neben der Zeichenfolge **MySQL** aus und speichert die Einstellungen.

    ![Screenshot des Bereichs „Verbindungszeichenfolgen“ mit der hervorgehobener osTicket-Verbindungszeichenfolge](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Schritt 6: Konfigurieren der Web-Apps:

Im letzten Schritt des Migrationsprozesses konfigurieren die Administratoren von Contoso die Web-Apps mit den osTicket-Websites.

1. In der primären Web-App (osticket-eus2) öffnen sie **Bereitstellungsoption** und legen die Quelle auf **GitHub** fest.

    ![Screenshot des Bereichs „Bereitstellungsoption“, bei dem GitHub als Quelle ausgewählt ist](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Contoso wählt die Bereitstellungsoptionen aus.

    ![Screenshot der Optionsdetails im Bereich „Bereitstellungsoption“](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. Nach dem Festlegen der Optionen wird die Konfiguration im Azure-Portal als *Ausstehend* angezeigt.

    ![Screenshot des Bereichs „Bereitstellungsoptionen“ mit dem Sitestatus „Ausstehend“](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. Nachdem die Konfiguration aktualisiert wurde und die osTicket-Web-App von GitHub in den Docker-Container mit Azure App Service geladen wurde, wird die Website als *Aktiv* angezeigt.

    ![Screenshot des Bereichs „Bereitstellungsoptionen“](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Sie wiederholen die obigen Schritte für die sekundäre Web-App osticket-cus.
6. Nachdem die Site konfiguriert wurde, ist sie über das Traffic Manager-Profil erreichbar. Der DNS-Name ist der neue Speicherort der Anwendung osTicket. [Weitere Informationen](/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record)

    ![Screenshot des Traffic Manager-Profilbereichs mit dem DNS-Namen](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Contoso möchte einen DNS-Namen, der leicht zu merken ist. Im Bereich **Neuer Ressourceneintrag** erstellen sie einen Alias, **CNAME**, und einen voll qualifizierten Domänennamen, **osticket.contoso.com**, der auf den Traffic Manager-Namen im DNS ihrer Domänencontroller verweist.

    ![Screenshot des Bereichs „Neuer Ressourceneintrag“, der den Aliasnamen und einen Zeiger auf Traffic Manager anzeigt](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. Sie konfigurieren die Web-Apps osticket-eus2 und osticket-cus, um die benutzerdefinierten Hostnamen zuzulassen.

    ![Screenshot des Bereichs „Hostnamen hinzufügen“ mit hervorgehobener Schaltfläche „Überprüfen“](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Einrichten der automatischen Skalierung

Zum Schluss richten die Administratoren von Contoso die automatische Skalierung für die Anwendung ein. Mit der automatischen Skalierung wird sichergestellt, dass die Anwendungsinstanzen bei der Verwendung durch Agents den geschäftlichen Anforderungen entsprechend erweitert oder verkleinert werden.

1. In App Service **APP-SVP-EUS2** öffnen sie **Skalierungseinheit**.
2. Sie konfigurieren eine neue Einstellung für die automatische Skalierung mit einer einzigen Regel, die die Anzahl von Instanzen um eins erhöht, wenn die CPU-Auslastung für die aktuelle Instanz zehn Minuten lang über 70 Prozent liegt.

    ![Screenshot der Seite mit den Einstellungen für die automatische Skalierung für die erste Region](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Sie konfigurieren die gleiche Einstellung für **APP-SVP-CUS**, um sicherzustellen, dass bei einem Failover der Anwendung zur sekundären Region das gleiche Verhalten gilt. Der einzige Unterschied besteht darin, dass die Standardinstanz auf 1 gesetzt wird, da dies nur für Failover gilt.

   ![Screenshot der Seite mit den Einstellungen für die automatische Skalierung für die zweite Region](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration wird die Anwendung osTicket in eine Azure App Service-Web-App mit Continuous Delivery mit einem privaten GitHub-Repository umgestaltet. Zur Verbesserung der Resilienz wird die Anwendung in zwei Regionen ausgeführt. Nach der Migration zur PaaS-Plattform wird die osTicket-Datenbank in Azure Database for MySQL ausgeführt.

Zum Bereinigen nach der Migration führt Contoso folgende Schritte aus:

- Das Unternehmen entfernt die VMware-VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation und zeigt neue Speicherorte und IP-Adressen an.
- Das Unternehmen überprüft sämtliche Ressourcen, die mit den lokalen VMs interagieren, und aktualisiert alle relevanten Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.
- Es konfiguriert die Überwachung neu, sodass sie auf die URL von `osticket-trafficmanager.net` zeigt, um nachzuverfolgen, ob die Anwendung ausgeführt wird.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die Anwendung jetzt ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso hat die Anwendung auf Sicherheitsprobleme überprüft. Dabei hat es festgestellt, dass die Kommunikation zwischen der Anwendung osTicket und der MySQL-Datenbankinstanz nicht für SSL konfiguriert ist. Das Team muss dies tun, um sicherzustellen, dass der Datenbankverkehr nicht gehackt werden kann. [Weitere Informationen](/azure/mysql/howto-configure-ssl)

### <a name="backups"></a>Backups

- Die osTicket-Web-Apps enthalten keine Zustandsdaten und müssen daher auch nicht gesichert werden.
- Das Team von Contoso muss die Sicherung für die Datenbank nicht konfigurieren. Azure Database for MySQL erstellt automatisch Serversicherungen und -speicher. Das Team hat sich für die Georedundanz für die Datenbank entschieden, damit sie robust und einsatzbereit ist. Sicherungen können verwendet werden, um für ihren Server den Stand zu einem bestimmten Zeitpunkt wiederherzustellen. [Weitere Informationen](/azure/mysql/concepts-backup)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Es gibt keine Lizenzierungsprobleme für die PaaS-Bereitstellung.
- Contoso verwendet die [Azure-Kostenverwaltung und -Abrechnung](/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.
