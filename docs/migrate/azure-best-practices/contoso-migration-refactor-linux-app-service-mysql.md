---
title: Umgestalten einer Linux-Service Desk-App für Azure App Service und Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Contoso eine lokale Linux-App umgestaltet, indem sie zu Azure App Service mit GitHub für die Webebene und Azure SQL-Datenbank migriert wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e504d4032fc019af43ec7cb1e8513504196559a2
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024213"
---
# <a name="refactor-a-linux-app-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Umgestalten einer Linux-App für mehrere Regionen mit Azure App Service, Azure Traffic Manager und Azure Database for MySQL

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso eine LAMP-App (Linux-basiertes Apache/MySQL/PHP) mit zwei Ebenen umgestaltet und sie mithilfe von Azure App Service mit GitHub-Integration und Azure Database for MySQL aus einer lokalen Umgebung zu Azure migriert.

osTicket, die in diesem Beispiel verwendete Service Desk-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/osTicket/osTicket) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team arbeitet eng mit Geschäftspartnern zusammen, um genau zu verstehen, was sie erreichen möchten:

- **Unternehmenswachstum.** Contoso wächst und erschließt neue Märkte. Das Unternehmen benötigt zusätzliche Kundendienstmitarbeiter.
- **Skalierung.** Die Lösung soll erstellt werden, damit Contoso beim Ausbau der Geschäftsbereiche weitere Kundendienstmitarbeiter einstellen kann.
- **Verbesserte Resilienz:**  In der Vergangenheit waren nur interne Benutzer von Problemen mit dem System betroffen. Beim neuen Geschäftsmodell wirken sich diese auch auf externe Benutzer aus, aber die App muss jederzeit verfügbar sein.

## <a name="migration-goals"></a>Migrationsziele

Für die Bestimmung der besten Migrationsmethode hat das Contoso-Cloudteam Ziele für diese Migration festgelegt:

- Eine Skalierung der Anwendung sollte über die aktuelle lokale Kapazität und Leistung hinaus möglich sein. Contoso verschiebt die Anwendung, um die Vorteile der bedarfsgesteuerten Skalierung von Azure zu nutzen.
- Contoso möchte die Codebasis der App in eine Continuous Delivery-Pipeline verschieben. Da App-Änderungen an GitHub gepusht werden, möchte Contoso diese Änderungen bereitstellen, ohne dass zusätzliche Aufgaben für das Betriebspersonal anfallen.
- Die Anwendung muss widerstandsfähig sein und über Wachstums- und Failovermöglichkeiten verfügen. Die App soll in zwei verschiedenen Azure-Regionen bereitgestellt und automatisch skaliert werden.
- Nachdem die App in die Cloud verschoben wurde, soll der Aufwand für die Datenbankadministration auf ein Minimum reduziert werden.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

## <a name="current-architecture"></a>Aktuelle Architektur

- Die App wird über zwei VM-Schichten (OSTICKETWEB und OSTICKETMYSQL) zur Verfügung gestellt.
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (contoso-datacenter) mit einem lokalen Domänencontroller (**contosodc1**).

![Aktuelle Architektur](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Die vorgeschlagene Architektur sieht wie folgt aus:

- Die App auf Webebene auf OSTICKETWEB wird durch die Einrichtung von Azure App Service in zwei Azure Regionen migriert. Azure App Service für Linux wird mit dem PHP 7.0-Docker-Container implementiert.
- Der App-Code wird nach GitHub verschoben, und die Azure App Service-App wird für Continuous Delivery mit GitHub konfiguriert.
- Azure-App-Server werden sowohl in der primären (USA, Osten 2) als auch in der sekundären (USA, Mitte) Region eingesetzt.
- Traffic Manager wird vor den beiden Web-Apps in beiden Regionen eingerichtet.
- Traffic Manager wird im Prioritätsmodus konfiguriert, um den Datenverkehr über „USA, Osten 2“ zu erzwingen.
- Wenn der Azure-App-Server in „USA, Osten 2“ offline geht, können Benutzer auf die App, für die ein Failover ausgeführt wurde, in „USA, Mitte“ zugreifen.
- Die App-Datenbank wird mit den MySQL-Workbench-Tools zum Azure Database for MySQL-Dienst migriert. Die lokale Datenbank wird lokal gesichert und direkt in Azure Database for MySQL wiederhergestellt.
- Die Datenbank befindet sich in der primären Region „USA, Osten 2“, im Datenbanksubnetz (PROD-DB-EUS2) im Produktionsnetzwerk (VNET-PROD-EUS2):
- Da es sich um die Migration einer Produktionsworkload handelt, befinden sich die Azure-Ressourcen für die App in der Ressourcengruppe für die Produktion **ContosoRG**.
- Die Traffic Manager-Ressource wird von Contoso in der Infrastrukturressourcengruppe **ContosoInfraRG** bereitgestellt.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Szenarioarchitektur](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

1. In einem ersten Schritt richten die Administratoren von Contoso die Azure-Infrastruktur ein – einschließlich der Bereitstellung von Azure App Service-Instanzen, der Einrichtung von Traffic Manager und der Bereitstellung einer Azure Database for MySQL-Instanz.
2. Nach der Vorbereitung von Azure migriert das Unternehmen die Datenbank mithilfe von MySQL Workbench.
3. Sobald die Datenbank in Azure ausgeführt wird, richtet Contoso ein privates GitHub-Repository für Azure App Service mit Continuous Delivery ein und lädt es mit der osTicket-App.
4. Im Azure-Portal wird die App von GitHub mit Azure App Service in den Docker-Container geladen.
5. Contoso optimiert die DNS-Einstellungen und konfiguriert die automatische Skalierung für die App.

![Migrationsprozess](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Azure App Service](https://azure.microsoft.com/services/app-service) | Der Dienst wird ausgeführt und skaliert Anwendungen mit dem Azure-PaaS-Dienst für Websites. | Der Preis richtet sich nach der Größe der Instanzen und den benötigten Features. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows)
[Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | Ein Lastenausgleichsmodul, das DNS verwendet, um Benutzer zu Azure oder externen Websites und Diensten zu leiten. | Der Preis richtet sich nach der Anzahl der empfangenen DNS-Abfragen und der Anzahl der überwachten Endpunkte. | [Weitere Informationen](https://azure.microsoft.com/pricing/details/traffic-manager)
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Die Datenbank basiert auf der Open Source-MySQL-Server-Engine. Sie stellt eine vollständig verwaltete, unternehmensgerechte MySQL Community-Edition als Database-as-a-Service für die Entwicklung und Bereitstellung von Apps bereit. | Der Preis richtet sich nach den Compute-, Speicher- und Sicherungsanforderungen. [Weitere Informationen](https://azure.microsoft.com/pricing/details/mysql)

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes.

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Abonnements wurden in einem früheren Artikel dieser Reihe erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.
**Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen von Azure App Service:** Die Administratoren von Contoso stellen Web-Apps in der primären und sekundären Region bereit.
> - **Schritt 2: Einrichten von Traffic Manager:** Das Unternehmen richtet Traffic Manager vorgelagert vor den Web-Apps ein, um den Datenverkehr zu routen und einen Lastenausgleich auszuführen.
> - **Schritt 3: Bereitstellen von MySQL:** Die Administratoren stellen in Azure eine Instanz von Azure Database for MySQL bereit.
> - **Schritt 4: Migrieren der Datenbank:** Die Datenbank wird mit MySQL Workbench migriert.
> - **Schritt 5: Einrichten von GitHub:** Sie richten ein lokales GitHub-Repository für die App-Websites bzw. den App-Code ein.
> - **Schritt 6: Bereitstellen der Web-Apps:** Die Web-Apps werden über GitHub bereitgestellt.

## <a name="step-1-provision-azure-app-service"></a>Schritt 1: Bereitstellen von Azure App Service

Die Administratoren von Contoso stellen mithilfe von Azure App Service zwei Web-Apps (jeweils eine pro Region) bereit.

1. Das Unternehmen erstellt eine Web-App-Ressource in der primären Region „USA, Osten 2“ (**osticket-eus2**) aus dem Azure Marketplace.
2. Es platziert die Ressource in die Produktionsressourcengruppe **ContosoRG**.

    ![Azure-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. In der primären Region (**APP-SVP-EUS2**) erstellt es einen neuen App Service-Plan unter Verwendung der Standardgröße.

     ![Azure-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Sie entscheiden sich für ein Linux-Betriebssystem mit PHP 7.0-Laufzeitstapel. Dabei handelt es sich um einen Docker-Container.

    ![Azure-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Sie erstellen eine zweite Web-App (**osticket-cus**) und einen Azure App Service-Plan für die Region „USA, Mitte“.

    ![Azure-App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Benötigen Sie weitere Hilfe?**

- Erfahren Sie mehr über [Azure App Service-Web-Apps](https://docs.microsoft.com/azure/app-service/overview).
- Erfahren Sie mehr über [Azure App Service unter Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Schritt 2: Einrichten von Traffic Manager

Die Administratoren von Contoso richten Traffic Manager ein, um eingehende Webanforderungen an die Web-Apps weiterzuleiten, die auf der osTicket-Webebene ausgeführt werden.

1. Sie erstellen eine Traffic Manager-Ressource (**osticket.trafficmanager.net**) aus dem Azure Marketplace. Es nutzt das prioritätsbasierte Routing, sodass „USA, Osten 2“ der primäre Standort ist. Es platziert die Ressource in seiner Infrastrukturressourcengruppe (**ContosoInfraRG**). Beachten Sie, dass Traffic Manager global und nicht an einen bestimmten Standort gebunden ist.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Als Nächstes konfigurieren sie Traffic Manager mit Endpunkten. Die Web-App „USA, Osten 2“ wird als primärer Standort (**osticket-eus2**) und die App „USA, Mitte“ als sekundärer Standort (**osticket-cus**) hinzugefügt.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. Nach dem Hinzufügen der Endpunkte können diese überwacht werden.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Benötigen Sie weitere Hilfe?**

- Erfahren Sie mehr über [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Erfahren Sie mehr über das [Routing von Datenverkehr zu einem prioritätsbasierten Endpunkt](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Schritt 3: Bereitstellen von Azure Database for MySQL

Die Administratoren von Contoso stellen eine MySQL-Datenbankinstanz in „USA, Osten 2“ bereit, der primären Region.

1. Im Azure-Portal erstellen die Verantwortlichen von Contoso eine Azure Database for MySQL-Ressource.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Sie fügen den Namen **contosoosticket** für die Azure-Datenbank hinzu. Sie fügen die Datenbank zur Ressourcengruppe für die Produktion **ContosoRG** hinzu, und geben Anmeldeinformationen für sie an.
3. Die lokale MySQL-Datenbank ist in Version 5.7 vorhanden. Deshalb wählen sie diese Version für Kompatibilitätszwecke. Sie verwenden die Standardgrößen, die ihren Datenbankanforderungen entsprechen.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. Bei den **Optionen für Sicherungsredundanz** entscheiden sie sich für die Verwendung von **Georedundanz**. Mit dieser Option können sie ihre Datenbank in der sekundären Region „USA Mitte“ wiederherstellen, wenn ein Ausfall auftritt. Sie können diese Option nur konfigurieren, wenn sie die Datenbank zur Verfügung stellen.

    ![Redundanz](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Sie richten die Verbindungssicherheit ein. In der Datenbank > **Verbindungssicherheit** richtet das Unternehmen Firewallregeln ein, um der Datenbank den Zugriff auf Azure-Dienste zu ermöglichen.

6. Sie fügen die Client-IP-Adresse der lokalen Arbeitsstation zu den Start- und End-IP-Adressen hinzu. Dadurch können die Web-Apps zusammen mit dem Datenbankclient, der die Migration durchführt, auf die MySQL-Datenbank zugreifen.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Schritt 4: Migrieren der Datenbank

Die Contoso-Administratoren migrieren die Datenbank mittels Sicherung und Wiederherstellung mit MySQL-Tools. Das Unternehmen installiert MySQL Workbench, speichert die Datenbank aus OSTICKETMYSQL und stellt sie dann wieder in der Azure Database for MySQL Server her.

### <a name="install-mysql-workbench"></a>Installieren von MySQL Workbench

1. Sie überprüfen die [Voraussetzungen und laden MySQL Workbench herunter](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Die Verantwortlichen bei Contoso installieren MySQL Workbench for Windows entsprechend den [Installationsanweisungen](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Der für die Installation verwendete Computer muss für die OSTICKETMYSQL-VM und Azure über das Internet zugänglich sein.
3. In MySQL Workbench erstellen sie eine MySQL-Verbindung mit OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. Sie exportieren die Datenbank als **Osticket** in eine lokale, eigenständige Datei.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. Nachdem die Datenbank lokal gesichert wurde, erstellen sie eine Verbindung mit der Azure Database for MySQL-Instanz.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Nun können sie die Datenbank aus der eigenständigen Datei in die Azure Database for MySQL-Instanz importieren (wiederherstellen). Ein neues Schema (Osticket) wird für die Instanz erstellt.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. Nach dem Wiederherstellen der Daten können diese mit Workbench abgefragt und im Azure-Portal angezeigt werden.

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

2. Nach dem Forken navigiert es zum **include**-Ordner und findet die Datei **ost-config.php**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Die Datei wird im Browser geöffnet und bearbeitet.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. Im Editor aktualisieren sie die Datenbankdetails (insbesondere **DBHOST** und **DBUSER**).

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Dann führt Contoso für die Änderungen einen Commit aus.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Sie ändern für jede Web-App (**osticket-eus2** und **osticket-cus**) die **Anwendungseinstellungen** im Azure-Portal.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Contoso gibt die Verbindungszeichenfolge mit dem Namen **osticket** ein und kopiert die Zeichenfolge vom Editor in den **Wertebereich**. Contoso wählt in der Dropdownliste neben der Zeichenfolge **MySQL** aus und speichert die Einstellungen.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Schritt 6: Konfigurieren der Web-Apps:

Im letzten Schritt des Migrationsprozesses konfigurieren die Administratoren von Contoso die Web-Apps mit den osTicket-Websites.

1. In der primären Web-App (**osticket-eus2**) öffnen sie **Bereitstellungsoption** und legen die Quelle auf **GitHub** fest.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Contoso wählt die Bereitstellungsoptionen aus.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. Nach dem Festlegen der Optionen wird die Konfiguration im Azure-Portal als „Ausstehend“ angezeigt.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. Nachdem die Konfiguration aktualisiert wurde und die osTicket-Web-App von GitHub in den Docker-Container mit Azure App Service geladen wurde, erscheint die Website als „Aktiv“.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Sie wiederholen die obigen Schritte für die sekundäre Web-App (**osticket-cus**).
6. Nachdem die Site konfiguriert wurde, ist sie über das Traffic Manager-Profil erreichbar. Der DNS-Name ist der neue Speicherort der osTicket-App. [Weitere Informationen](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record)

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Contoso wünscht einen DNS-Namen, der leicht zu merken ist. Das Unternehmen erstellt einen Aliasdatensatz (CNAME) **osticket.contoso.com**, der auf den Traffic Manager-Namen im DNS seiner Domänencontroller zeigt.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. Es konfiguriert sowohl die Web-App **osticket-eus2** als auch **osticket-cus**, um die benutzerdefinierten Hostnamen zuzulassen.

    ![Konfigurieren der App](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Einrichten der automatischen Skalierung

Schließlich richtet Contoso eine automatische Skalierung für die App ein. Dies stellt sicher, dass bei der Verwendung der Apps durch Agents die App-Instanzen entsprechend den Geschäftsanforderungen erweitert oder verkleinert werden.

1. In App Service **APP-SRV-EUS2** öffnen sie **Skalierungseinheit**.
2. Das Unternehmen konfiguriert eine neue Einstellung für die automatische Skalierung mit einer einzigen Regel, die die Anzahl der Instanzen um eins erhöht, wenn der CPU-Prozentsatz für die aktuelle Instanz zehn Minuten lang über 70% liegt.

    ![Autoscale](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Contoso konfiguriert die gleiche Einstellung für **APP-SRV-CUS**, um sicherzustellen, dass das gleiche Verhalten gilt, wenn ein Failover der App auf die sekundäre Region ausgeführt wird. Der einzige Unterschied ist, dass die Standardinstanz auf 1 gesetzt wird, da dies nur für Failover gilt.

   ![Autoscale](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nachdem die Migration abgeschlossen ist, wird die osTicket-App in eine Azure App Service-Web-App mit Continuous Delivery mit einem privaten GitHub-Repository umgestaltet. Zur Verbesserung der Resilienz wird die App in zwei Regionen ausgeführt. Die osTicket-Datenbank wird nach der Migration zur PaaS-Plattform in der Azure-Datenbank für MySQL ausgeführt.

Zur Bereinigung muss Contoso folgende Schritte ausführen:

- Das Unternehmen entfernt die VMware-VMs aus dem vCenter-Bestand.
- Es entfernt die lokalen VMs aus lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation und zeigt neue Speicherorte und IP-Adressen an.
- Das Unternehmen überprüft sämtliche Ressourcen, die mit den lokalen VMs interagieren, und aktualisiert sämtliche relevanten Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.
- Es konfiguriert die Überwachung so, dass sie auf die URL von osticket-trafficmanager.net zeigt, um nachzuverfolgen, ob die App ausgeführt wird.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die App jetzt ausgeführt wird, muss Contoso seine neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüfte die App auf eventuell vorhandene Sicherheitsprobleme. Es wurde festgestellt, dass die Kommunikation zwischen der osTicket-App und der MySQL-Datenbank-Instanz nicht für SSL konfiguriert ist. Das Team muss dies tun, um sicherzustellen, dass der Datenbankverkehr nicht gehackt werden kann. [Weitere Informationen](https://docs.microsoft.com/azure/mysql/howto-configure-ssl)

### <a name="backups"></a>Backups

- Die osTicket-App enthält keine Zustandsdaten und muss daher auch nicht gesichert werden.
- Das Unternehmen muss die Sicherung für die Datenbank nicht konfigurieren. Azure Database for MySQL erstellt automatisch Serversicherungen und -speicher. Es hat sich für die Georedundanz für die Datenbank entschieden, damit sie robust und einsatzbereit ist. Sicherungen können verwendet werden, um für Ihren Server den Stand zu einem bestimmten Zeitpunkt wiederherzustellen. [Weitere Informationen](https://docs.microsoft.com/azure/mysql/concepts-backup)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Es gibt keine Lizenzierungsprobleme für die PaaS-Bereitstellung.
- Contoso aktiviert Azure Cost Management. Es ist durch Cloudyn lizenziert, ein Tochterunternehmen von Microsoft. Dabei handelt es sich um eine Cost Management-Lösung mit mehreren Clouds, die Ihnen das Verwenden und Verwalten von Azure und anderen Cloudressourcen erleichtert. [Erfahren Sie mehr](https://docs.microsoft.com/azure/cost-management/overview) über die Azure Cost Management.
