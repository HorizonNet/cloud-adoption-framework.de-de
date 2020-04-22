---
title: Zuweisen eines neuen Hosts für eine lokale App durch Migration zu Azure-VMs und zu einer verwalteten Azure-SQL-Datenbank-Instanz
description: Es wird beschrieben, wie Contoso für eine lokale App auf Azure-VMs einen neuen Host zuweist und eine verwaltete Azure SQL-Datenbank-Instanz verwendet.
author: givenscj
ms.author: abuck
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 089a772bdc41bc96f327f9d9ce34d2107fd48934
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80996796"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc NSGs agentless SQLMI iisreset -->

# <a name="rehost-an-on-premises-app-on-an-azure-vm-and-sql-database-managed-instance"></a>Zuweisen eines neuen Hosts für eine lokale App auf einer Azure-VM und einer verwalteten Azure SQL-Datenbank-Instanz

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso eine zweistufige Windows .NET-Front-End-App, die auf VMware-VMs ausgeführt wird, mit dem Azure Migrate-Dienst zu einer Azure-VM migriert. Er zeigt außerdem, wie Contoso die App-Datenbank zu einer verwalteten Azure-SQL-Datenbank-Instanz migriert.

Die in diesem Beispiel verwendet SmartHotel360-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team von Contoso hat eng mit den Geschäftspartnern des Unternehmens zusammengearbeitet, um zu verstehen, was mit dieser Migration erreicht werden soll:

- **Unternehmenswachstum.** Contoso wächst. Aus diesem Grund hat der Druck auf die lokalen Systeme und die Infrastruktur des Unternehmens zugenommen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und die Prozesse für seine Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, damit die Kundenanforderungen in kürzerer Zeit erfüllt werden können.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Sie muss schneller reagieren können, als sich die Gegebenheiten des Markts ändern, damit das Unternehmen auf dem globalen Markt Erfolg hat. Die IT-Abteilung von Contoso darf keine Hindernisse in den Weg stellen und keine Geschäftsabläufe blockieren.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich Ziele für die Migration gesetzt. Das Unternehmen nutzt die Migrationsziele, um die beste Migrationsmethode zu ermitteln.

- Nach der Migration sollte die App in Azure die gleichen Leistungsmerkmale aufweisen, über die sie derzeit in der lokalen VMware-Umgebung von Contoso verfügt. Die Umstellung auf die Cloud bedeutet nicht, dass die Leistung der App weniger wichtig ist.
- Contoso möchte nicht in die App investieren. Die App hat eine entscheidende Bedeutung und ist wichtig für das Geschäft, aber Contoso möchte die App einfach in ihrer jetzigen Form in die Cloud verlagern.
- Datenbankverwaltungsaufgaben sollten nach der Migration der App auf ein Minimum reduziert sein.
- Contoso möchte für diese App keine Azure SQL-Datenbank-Instanz verwenden. Das Unternehmen ist auf der Suche nach Alternativen.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess, einschließlich der für die Migration genutzten Azure-Dienste.

### <a name="current-architecture"></a>Aktuelle Architektur

- Contoso verfügt über ein zentrales Rechenzentrum (**contoso-datacenter**). Das Rechenzentrum befindet sich in New York City, im Osten der USA.
- Contoso verfügt in den USA über drei weitere Niederlassungen.
- Das zentrale Rechenzentrum ist über eine auf Glasfaser basierende Metro-Ethernet-Verbindung (500 MBit/s) mit dem Internet verbunden.
- Jede Niederlassung ist lokal über Business-Class-Verbindungen mit dem Internet verbunden, und IPsec-VPN-Tunnel führen zurück zum zentralen Rechenzentrum. Aufgrund dieser Anordnung ist das gesamte Netzwerk von Contoso dauerhaft verbunden, und die Internetverbindung wird optimiert.
- Das Hauptrechenzentrum ist vollständig mit VMware virtualisiert. Contoso verfügt über zwei ESXi 6.5-Virtualisierungshosts, die mit vCenter Server 6.5 verwaltet werden.
- Contoso nutzt Active Directory für die Identitätsverwaltung. Contoso verwendet im internen Netzwerk DNS-Server.
- Contoso verfügt über einen lokalen Domänencontroller (**contosodc1**).
- Die Domänencontroller werden auf VMware-VMs ausgeführt. Die Domänencontroller in lokalen Niederlassungen werden auf physischen Servern ausgeführt.
- Die SmartHotel360-App ist auf zwei VMs (**WEBVM** und **SQLVM**) verteilt, die sich auf einem VMware ESXi-Host der Version 6.5 (**contosohost1.contoso.com**) befinden.
- Die VMware-Umgebung wird per vCenter Server 6.5-Software (**vcenter.contoso.com**) verwaltet, die auf einer VM ausgeführt wird.

![Aktuelle Contoso-Architektur](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

In diesem Szenario möchte Contoso seine lokale zweischichtige Reise-App folgendermaßen migrieren:

- Migration der App-Datenbank (**SmartHotelDB**) zu einer verwalteten Azure SQL-Datenbank-Instanz.
- Migration der Front-End-**WebVM** zu einer Azure-VM.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Szenarioarchitektur](./media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und einer verwalteten SQL Server-Instanz durchgeführt. Hierbei haben die folgenden Überlegungen Contoso dabei unterstützt, sich für eine verwaltete Instanz zu entscheiden.

- Eine verwaltete Instanz bietet nahezu 100% Kompatibilität mit der aktuellen SQL Server-Version. Microsoft empfiehlt verwaltete Instanzen für Kunden, die SQL Server lokal oder auf einer IaaS-VM ausführen und ihre Apps mit minimalen Entwurfsänderungen zu einem vollständig verwalteten Dienst migrieren möchten.
- Contoso plant die Migration einer großen Anzahl von Apps von der lokalen Ausführung zu IaaS. Viele dieser Apps werden durch einen unabhängigen Softwarehersteller (ISV) bereitgestellt. Contoso hat erkannt, dass eine verwaltete Instanz für Datenbankkompatibilität für diese Apps sorgt, während eine SQL-Datenbank möglicherweise nicht unterstützt wird.
- Contoso kann mit dem vollständig automatisierten Azure Database Migration Service eine Lift & Shift-Migration zu einer verwalteten Instanz ausführen. Außerdem kann Contoso diesen Dienst für spätere Datenbankmigrationen erneut einsetzen.
- Eine verwaltete SQL-Instanz unterstützt SQL Server-Agent, eine wichtige Komponente der SmartHotel360-App. Contoso benötigt diese Kompatibilität, weil ansonsten die für diese App benötigten Wartungspläne umgestaltet werden müssen.
- Dank Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen gegen eine verwaltete SQL-Datenbank-Instanz austauschen. Auf diese Weise kann Contoso bei der verwalteten Instanz bis zu 30% an Kosten einsparen.
- Verwaltete SQL-Instanzen sind vollständig in das virtuelle Netzwerk integriert und bieten somit mehr Isolation und Sicherheit für die Daten von Contoso. Contoso kann die Vorteile der öffentlichen Cloud nutzen und gleichzeitig die Umgebung vom öffentlichen Internet isolieren.
- Verwaltete Instanzen unterstützen zahlreiche Sicherheitsfeatures, darunter Always Encrypted, dynamische Datenmaskierung, Sicherheit auf Zeilenebene und Bedrohungserkennung.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | WEBVM wird ohne Änderungen nach Azure verlagert, was die Migration vereinfacht.<br/><br/> Die verwaltete SQL-Instanz unterstützt die technischen Anforderungen und Ziele von Contoso.<br/><br/> Eine verwaltete Instanz bietet 100% Kompatibilität mit der aktuellen Bereitstellung und ermöglicht gleichzeitig den Ausstieg aus SQL Server 2008 R2.<br/><br/> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für sowohl SQL Server als auch Windows Server nutzen.<br/><br/> Der Azure Database Migration Service kann für zusätzliche Migrationen in der Zukunft genutzt werden.<br/><br/> Die verwaltete SQL-Instanz bietet integrierte Fehlertoleranz, die nicht von Contoso konfiguriert werden muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist.
**Nachteile** | Auf der WEBVM wird Windows Server 2008 R2 ausgeführt. Obwohl dieses Betriebssystem von Azure unterstützt wird, ist es kein weiterhin unterstütztes Betriebssystem. [Weitere Informationen](https://support.microsoft.com/help/956893)<br/><br/> Die Webschicht bleibt ein Single Point of Failure, weil nur die WEBVM Dienste bereitstellt.<br/><br/> Contoso muss die App-Webschicht weiterhin als virtuellen Computer unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service umzustellen.<br/><br/> Für die Datenschicht stellt die verwaltete Instanz möglicherweise nicht die beste Lösung dar, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen oder Drittanbieter-Apps mit SQL Server ausführen möchte. Eine Ausführung von SQL Server auf einer IaaS-VM könnte diese Flexibilität bieten.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migrationsprozess

Contoso migriert die Web- und Datenschichten seiner SmartHotel360-App mit den folgenden Schritten zu Azure:

1. Contoso hat bereits eine Azure-Infrastruktur eingerichtet, sodass für dieses Szenario nur noch einige bestimmte Azure-Komponenten hinzugefügt werden müssen.
2. Die Datenschicht wird per Azure Database Migration Service migriert. Der Dienst stellt über eine Site-to-Site-VPN-Verbindung zwischen dem Contoso-Rechenzentrum und Azure eine Verbindung mit der lokalen SQL Server-VM her. Der Dienst migriert dann die Datenbank.
3. Die Webschicht wird per „Lift & Shift“-Migration mit Azure Migrate migriert. Dieser Prozess umfasst das Vorbereiten der lokalen VMware-Umgebung, das Einrichten und Aktivieren der Replikation und das Migrieren der VMs per Failover zu Azure.

     ![Migrationsarchitektur](./media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Azure-Dienste

Dienst | BESCHREIBUNG | Kosten
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Der Azure Database Migration Service ermöglicht die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen bei minimaler Ausfallzeit. | Informieren Sie sich über die [unterstützten Regionen](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Verwaltete Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Die verwaltete Azure SQL-Datenbank-Instanz ist ein verwalteter Datenbankdienst, der eine vollständig verwaltete SQL Server-Instanz in der Azure-Cloud darstellt. Sie nutzt den gleichen Code wie die neueste Version der Microsoft SQL Server-Datenbank-Engine und verfügt über die neuesten Features, Leistungsverbesserungen und Sicherheitspatches. | Bei Verwendung einer verwalteten Azure SQL-Datenbank-Instanz, die in Azure ausgeführt wird, fallen Gebühren je nach Kapazität an. Erfahren Sie mehr zu den [Preisen für verwaltete SQL-Datenbank-Instanzen](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) | Contoso nutzt den Azure Migrate-Dienst, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | Ab Mai 2018 ist Azure Migrate ein kostenloser Dienst.

## <a name="prerequisites"></a>Voraussetzungen

Contoso und andere Benutzer müssen für dieses Szenario die folgenden Voraussetzungen erfüllen:

<!-- markdownlint-disable MD033 -->

Requirements (Anforderungen) | Details
--- | ---
**Azure-Abonnement** | Sie müssten bereits ein Abonnement erstellt haben, als Sie die Bewertung im ersten Artikel dieser Reihe durchgeführt haben. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator des Abonnements zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ für die erforderlichen Ressourcengruppen und Ressourcen zuweist.
**Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben.
**Lokale Server** | Der lokale vCenter-Server muss mit Version 5.5, 6.0 oder 6.5 ausgeführt werden.<br/><br/> Einen ESXi-Host mit Version 5.5, 6.0 oder 6.5.<br/><br/> Mindestens eine VMware-VM auf dem ESXi-Host.
**Lokale VMs** | [Überprüfen Sie Linux-Computer](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird.
**Database Migration Service** | Für den Azure Database Migration Service benötigen Sie ein [kompatibles lokales VPN-Gerät](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).<br/><br/> Sie müssen das lokale VPN-Gerät konfigurieren können. Es muss über eine externe öffentliche IPv4-Adresse verfügen. Diese Adresse darf sich nicht hinter einem NAT-Gerät befinden.<br/><br/> Stellen Sie sicher, dass Sie Zugriff auf Ihre lokale SQL Server-Datenbank haben.<br/><br/> Windows-Firewall sollte auf die Quelldatenbank-Engine zugreifen können. Informieren Sie sich, wie Sie [Windows-Firewall für den Datenbank-Engine-Zugriff konfigurieren](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).<br/><br/> Wenn sich eine Firewall vor dem Datenbankcomputer befindet, sollten Sie Regeln hinzufügen, um den Zugriff auf die Datenbank und auf Dateien über SMB-Port 445 zuzulassen.<br/><br/> Für die zum Herstellen einer Verbindung zwischen der SQL Server-Quellinstanz und der jeweiligen verwalteten Zielinstanz verwendeten Anmeldeinformationen muss sichergestellt sein, dass es sich jeweils um Mitglieder der Serverrolle „sysadmin“ handelt.<br/><br/> Sie benötigen eine Netzwerkfreigabe in der lokalen Datenbank, die vom Azure Database Migration Service zum Sichern der Quelldatenbank verwendet werden kann.<br/><br/> Vergewissern Sie sich, dass das Dienstkonto, mit dem die SQL Server-Quellinstanz ausgeführt wird, über Schreibberechtigungen für die Netzwerkfreigabe verfügt.<br/><br/> Notieren Sie sich einen Windows-Benutzernamen, der über eine Berechtigung für Vollzugriff auf die Netzwerkfreigabe verfügt, und das zugehörige Kennwort. Azure Database Migration Service verwendet diese Benutzeranmeldeinformationen, um Sicherungsdateien in den Azure-Speichercontainer hochzuladen.<br/><br/> Bei der SQL Server Express-Installation wird das TCP/IP-Protokoll standardmäßig auf **Deaktiviert** gesetzt. Stellen Sie sicher, dass es aktiviert ist.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso plant die Einrichtung der Bereitstellung wie folgt:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten einer verwalteten SQL-Datenbank-Instanz** Contoso benötigt eine bereits vorhandene verwaltete Instanz, zu der die lokale SQL Server-Datenbank-Instanz migriert wird.
> - **Schritt 2: Vorbereiten des Azure Database Migration Service.** Contoso muss den Datenbankmigrationsanbieter registrieren, eine Instanz erstellen und dann ein Azure Database Migration Service-Projekt erstellen. Außerdem muss Contoso einen SAS-URI (Shared Access Signature Uniform Resource Identifier) für den Azure Database Migration Service einrichten. Ein SAS-URI ermöglicht den delegierten Zugriff auf Ressourcen im Speicherkonto von Contoso, damit Contoso eingeschränkte Berechtigungen für Speicherobjekte gewähren kann. Contoso richtet einen SAS-URI ein, damit der Azure Database Migration Service auf den Speicherkontocontainer zugreifen kann, in den der Dienst die SQL Server-Sicherungsdateien hochlädt.
> - **Schritt 3: Vorbereiten von Azure für die Azure Migrate-Servermigration.** Sie fügen das Tool für die Servermigration ihrem Azure Migrate-Projekt hinzu.
> - **Schritt 4: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate-Servermigration.** Sie bereiten Konten für die VM-Ermittlung sowie das Herstellen einer Verbindung mit Azure-VMs nach der Migration vor.
> - **Schritt 5: Replizieren von VMs.** Das Unternehmen richtet die Replikation ein und startet das Replizieren von VMs in Azure-Storage.
> - **Schritt 6: Migrieren der Datenbank mit dem Azure Database Migration Service.** Contoso migriert die Datenbank.
> - **Schritt 7: Migration der virtuellen Computer mit der Azure Migrate-Servermigration.** Es wird eine Testmigration durchgeführt, um sicherzustellen, dass alles funktioniert, und anschließend wird eine vollständige Migration ausgeführt, um die VMs in Azure zu verlagern.

## <a name="step-1-prepare-a-sql-database-managed-instance"></a>Schritt 1: Vorbereiten einer verwalteten SQL-Datenbank-Instanz

Contoso benötigt ein Subnetz, das die folgenden Anforderungen erfüllt, um eine verwaltete Azure SQL-Datenbank-Instanz einzurichten:

- Das Subnetz muss dediziert sein. Es muss leer sein und darf keinen anderen Clouddienst enthalten. Das Subnetz darf kein Gatewaysubnetz sein.
- Nachdem die verwaltete Instanz erstellt wurde, sollte Contoso dem Subnetz keine Ressourcen hinzufügen.
- Dem Subnetz darf keine Netzwerksicherheitsgruppe zugeordnet sein.
- Das Subnetz muss über eine benutzerdefinierte Routingtabelle verfügen. Die folgende Route sollte die einzige zugewiesene Route sein: 0.0.0.0/0, nächster Hop „Internet“.
- Optionales benutzerdefiniertes DNS: Wenn ein benutzerdefiniertes DNS für das virtuelle Azure-Netzwerk angegeben ist, muss die IP-Adresse des rekursiven Azure-Konfliktlösers (z.B. 168.63.129.16) der Liste hinzugefügt werden. Informieren Sie sich, wie Sie [ein benutzerdefiniertes DNS für eine verwaltete Azure SQL-Datenbank-Instanz konfigurieren](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).
- Dem Subnetz darf kein Dienstendpunkt (Speicher oder SQL) zugeordnet sein. Dienstendpunkte sollten im virtuellen Netzwerk deaktiviert sein.
- Das Subnetz muss mindestens 16 IP-Adressen aufweisen. Informieren Sie sich, wie Sie [die Größe des Subnetzes für verwaltete Instanzen ermitteln](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- In der Hybridumgebung von Contoso sind benutzerdefinierte DNS-Einstellungen erforderlich. Contoso konfiguriert die DNS-Einstellungen so, dass mindestens ein Azure DNS-Server des Unternehmens genutzt wird. Informieren Sie sich über die [DNS-Anpassung](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Einrichten eines virtuellen Netzwerks für die verwaltete Instanz

Die Contoso-Administratoren richten das virtuelle Netzwerk folgendermaßen ein:

1. Es wird ein neues virtuelles Netzwerk (**VNET-SQLMI-EU2**) in der primären Region „USA, Osten 2“ eingerichtet. Das virtuelle Netzwerk wird der Ressourcengruppe **ContosoNetworkingRG** hinzugefügt.
2. Contoso weist den Adressraum 10.235.0.0/24 zu. Es wird sichergestellt, dass der Bereich zu keinerlei Überschneidungen mit anderen Netzwerken im Unternehmen führt.
3. Dem Netzwerk werden zwei Subnetze hinzugefügt:
    - **SQLMI-DS-EUS2** (10.235.0.0.25).
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Dieses Subnetz wird verwendet, um ein Verzeichnis an die verwaltete Instanz anzufügen.

      ![Verwaltete Instanz – Erstellen eines virtuellen Netzwerks](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Nach der Bereitstellung des virtuellen Netzwerks und der Subnetze wird das folgende Netzwerkpeering eingerichtet:

    - Peering von **VNET-SQLMI-EUS2** mit **VNET-HUB-EUS2** (dem virtuellen Hubnetzwerk für „USA, Osten 2“).
    - Peering von **VNET-SQLMI-EUS2** mit **VNET-PROD-EUS2** (Produktionsnetzwerk).

      ![Netzwerkpeering](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Es werden benutzerdefinierte DNS-Einstellungen festgelegt. Das DNS verweist zuerst auf den Azure-Domänencontroller von Contoso. Das Azure DNS ist der sekundäre Verweis. Die Azure-Domänencontroller von Contoso befinden sich an den folgenden Orten:

    - Im Subnetz **PROD-DC-EUS2** im Produktionsnetzwerk „USA, Osten 2“ (**VNET-PROD-EUS2**).
    - **CONTOSODC3**-Adresse: 10.245.42.4
    - **CONTOSODC4**-Adresse: 10.245.42.5
    - Azure DNS-Konfliktlöser: 168.63.129.16

      ![Netzwerk-DNS-Server](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Benötigen Sie weitere Hilfe?**

- Sehen Sie sich eine Übersicht über die [verwaltete Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) an.
- Informieren Sie sich über das [Erstellen eines virtuellen Netzwerks für eine verwaltete Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- Erfahren Sie, wie Sie das [Peering einrichten](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Erfahren Sie, wie Sie die [DNS-Einstellungen für Azure Active Directory aktualisieren](https://docs.microsoft.com/azure/active-directory-domain-services/tutorial-create-instance).

### <a name="set-up-routing"></a>Einrichten des Routings

Die verwaltete Instanz wird in einem privaten virtuellen Netzwerk angeordnet. Contoso benötigt eine Routingtabelle für das virtuelle Netzwerk, um mit dem Azure-Verwaltungsdienst zu kommunizieren. Wenn das virtuelle Netzwerk nicht mit dem Dienst kommunizieren kann, von dem es verwaltet wird, kann nicht mehr auf das virtuelle Netzwerk zugegriffen werden.

Contoso berücksichtigt die folgenden Faktoren:

- Die Routingtabelle enthält einen Satz mit Regeln (Routen), mit denen angegeben wird, wie von der verwalteten Instanz gesendete Pakete im virtuellen Netzwerk weitergeleitet werden sollen.
- Die Routingtabelle bezieht sich auf Subnetze, in denen verwalteten Instanzen bereitgestellt werden. Jedes Paket, das ein Subnetz verlässt, wird auf Grundlage der entsprechenden Routingtabelle verarbeitet.
- Ein Subnetz kann nur einer Routingtabelle zugeordnet sein.
- Für die Erstellung von Routingtabellen in Microsoft Azure fallen keine zusätzlichen Gebühren an.

 Die Contoso-Administratoren führen die folgenden Schritte aus, um das Routing einzurichten:

1. Es wird eine benutzerdefinierte Routingtabelle in der Ressourcengruppe **ContosoNetworkingRG** erstellt.

    ![Routingtabelle](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Um die Anforderungen für verwaltete Instanzen zu erfüllen, wird nach dem Bereitstellen der Routingtabelle (**MIRouteTable**) eine Route mit dem Adresspräfix 0.0.0.0/0 hinzugefügt. Die Option **Typ des nächsten Hops** wird auf **Internet** festgelegt.

    ![Routingtabellenpräfix](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. Die Routingtabelle wird dem Subnetz **SQLMI-DB-EUS2** (im Netzwerk **VNET-SQLMI-EUS2**) zugeordnet.

    ![Routingtabellensubnetz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich, wie Sie [Routen für eine verwaltete Instanz einrichten](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

### <a name="create-a-managed-instance"></a>Erstellen einer verwalteten Instanz

Jetzt können die Contoso-Administratoren eine verwaltete SQL-Datenbank-Instanz bereitstellen:

1. Da die verwaltete Instanz als Geschäfts-App dient, wird sie in der primären Region „USA, Osten 2“ des Unternehmens bereitgestellt. Die verwaltete Instanz wird zur Ressourcengruppe **ContosoRG** hinzugefügt.
2. Für die Instanz wird ein Tarif, eine Computegröße und Speicher ausgewählt. Erfahren Sie mehr zu den [Preisen für verwaltete SQL-Datenbank-Instanzen](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![SQL-Datenbank-Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Nach der Bereitstellung der verwalteten Instanz werden zwei neue Ressourcen in der Ressourcengruppe **ContosoRG** angezeigt:

    - Ein virtueller Cluster, falls Contoso über mehrere verwaltete Instanzen verfügt.
    - Die verwaltete SQL-Datenbank-Instanz.

      ![SQL-Datenbank-Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich, wie Sie [eine verwaltete Instanz bereitstellen](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

## <a name="step-2-prepare-the-azure-database-migration-service"></a>Schritt 2: Vorbereiten des Azure Database Migration Service

Um den Azure Database Migration Service vorzubereiten, müssen die Contoso-Administratoren folgende Aufgaben ausführen:

- Registrieren Sie den Azure Database Migration Service-Anbieter in Azure.
- Stellen Sie den Azure Database Migration Service mit Zugriff auf Azure Storage zum Hochladen der Sicherungsdateien bereit, die zum Migrieren einer Datenbank verwendet werden. Um Zugriff auf Azure Storage bereitzustellen, wird ein Azure Blob Storage-Container erstellt. Außerdem wird ein SAS-URI für den Blob Storage-Container generiert.
- Erstellen eines Azure Database Migration Service-Projekts.

Anschließend werden die folgenden Schritte ausgeführt:

1. Die Administratoren registrieren den Anbieter für die Datenbankmigration unter dem Abonnement.
    ![Database Migration Service – Registrieren](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

2. Sie erstellen einen Blob Storage-Container. Contoso generiert einen SAS-URI, damit der Azure Database Migration Service darauf zugreifen kann.

    ![Database Migration Service – Generieren eines SAS-URI](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

3. Sie erstellen eine Instanz von Azure Database Migration Service.

    ![Database Migration Service – Erstellen einer Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

4. Sie platzieren die Azure Database Migration Service-Instanz im Subnetz **PROD-DC-EUS2** des virtuellen Netzwerks **VNET-PROD-DC-EUS2**.
    - Die Azure Database Migration Service-Instanz wird hier platziert, weil der Dienst sich in einem virtuellen Netzwerk befinden muss, das über ein VPN-Gateway auf die lokale SQL Server-VM zugreifen kann.
    - Für **VNET-FA-EUS2** wird ein Peering mit **VNET-HUB-EUS2** durchgeführt und die Verwendung von Remotegateways zugelassen. Mit der Option **Use remote gateways** (Remotegateways verwenden) wird sichergestellt, dass der Azure Database Migration Service so kommunizieren kann, wie dies erforderlich ist.

        ![Database Migration Service – Konfigurieren des Netzwerks](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich, wie Sie [den Azure Database Migration Service einrichten](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal).
- Erfahren Sie, wie Sie [eine SAS erstellen und verwenden](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-3-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 3: Vorbereiten von Azure für das Tool für die Azure Migrate-Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein VNET, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Das bereitgestellte Tool für die Azure Migrate-Servermigration.

Das Unternehmen geht bei der Einrichtung dieser Komponenten wie folgt vor:

1. **Einrichten eines Netzwerks:** Im Rahmen der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) hat Contoso bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann.

    - Bei der SmartHotel360-App handelt es sich um eine Produktions-App. Die VMs werden zum Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten 2“ migriert.
    - Beide VMs werden in der Ressourcengruppe ContosoRG bereitgestellt, die für Produktionsressourcen verwendet wird.
    - Die App-Front-End-VM (WEBVM) wird zum Front-End-Subnetz (PROD-FE-EUS2) im Produktionsnetzwerk migriert.
    - Die App-Datenbank-VM (SQLVM) wird zum Datenbanksubnetz (PROD-DB-EUS2) im Produktionsnetzwerk migriert.

## <a name="step-4-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Schritt 4: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate-Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein VNET, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Das bereitgestellte und konfigurierte Tool für die Azure Migrate-Servermigration (OVA).

Das Unternehmen geht bei der Einrichtung dieser Komponenten wie folgt vor:

1. Einrichten eines Netzwerks: Im Rahmen der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) hat Contoso bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann.

    - Bei der SmartHotel360-App handelt es sich um eine Produktions-App. Die VMs werden zum Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten 2“ migriert.
    - Beide VMs werden in der Ressourcengruppe ContosoRG bereitgestellt, die für Produktionsressourcen verwendet wird.
    - Die App-Front-End-VM (WEBVM) wird zum Front-End-Subnetz (PROD-FE-EUS2) im Produktionsnetzwerk migriert.
    - Die App-Datenbank-VM (SQLVM) wird zum Datenbanksubnetz (PROD-DB-EUS2) im Produktionsnetzwerk migriert.

2. Bereitstellen des Azure Migrate-Servermigrationstools.

    - Laden Sie das OVA-Image von Azure Migrate herunter, und importieren Sie es in VMware.

        ![Herunterladen der OVA-Datei](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    - Starten Sie das importierte Image, und konfigurieren Sie das Tool, einschließlich der folgenden Schritte:

      - Einrichten der erforderlichen Komponenten

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

      - Verweisen des Tools auf das Azure-Abonnement

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-register-azure.png)

      - Legen Sie die VMWare vCenter-Anmeldeinformatioen fest.

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

      - Fügen Sie alle Linux-basierten oder Windows-basierten Anmeldeinformationen für die Ermittlung hinzu.

        ![Konfigurieren des Tools](./media/contoso-migration-rehost-vm/migration-credentials.png)

3. Nach der Konfiguration dauert es einige Zeit, bis das Tool alle virtuellen Computer auflistet. Nach Abschluss des Vorgangs sehen Sie, dass sie im Azure Migrate-Tool in Azure aufgefüllt werden.

**Benötigen Sie weitere Hilfe?**

[Hier finden Sie Informationen](https://docs.microsoft.com/azure/migrate) zur Einrichtung des Tools für die Azure Migrate-Servermigration.

### <a name="prepare-on-premises-vms"></a>Vorbereiten von lokalen VMs

Nach der Migration möchte Contoso eine Verbindung mit den Azure VMs herstellen und Azure die Erlaubnis zum Verwalten der VMs geben. Dazu führen Contoso-Administratoren vor der Migration folgende Schritte aus:

1. Für den Zugriff über das Internet:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Sicherstellen, dass TCP- und UDP-Regeln zum **öffentlichen** Profil hinzugefügt wurden.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.

2. Für den Zugriff über Site-to-Site-VPN:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.
    - Legen Sie für Windows die SAN-Richtlinie des Betriebssystems auf der lokalen VM auf **OnlineAll** fest.

3. Installieren Sie den Azure-Agent:

    - [Azure Linux-Agents](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux)
    - [Azure Windows-Agent](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-windows)

4. Sonstiges

   - Unter Windows sollten auf dem virtuellen Computer keine ausstehenden Windows-Updates vorhanden sein, wenn Sie eine Migration auslösen. Andernfalls ist nach Abschluss des Updates die Anmeldung bei der VM nicht mehr möglich.
   - Nach der Migration kann **Startdiagnose** aktiviert werden, um einen Screenshot der VM anzuzeigen. Falls dies nicht funktioniert, sollte überprüft werden, ob die VM ausgeführt wird, und die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) gelesen werden.

5. Benötigen Sie weitere Hilfe?

   - [Informationen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) zum Vorbereiten von virtuellen Computern für die Migration.

## <a name="step-5-replicate-the-on-premises-vms"></a>Schritt 5: Replizieren der lokalen VMs

Bevor Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können Sie mit der Replikation von VMware-VMs in Azure beginnen.

1. Klicken Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** auf **Replizieren**.

    ![Replizieren von VMs](./media/contoso-migration-rehost-vm/select-replicate.png)

2. Wählen Sie unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere-Hypervisor** aus.

3. Wählen Sie unter **Lokale Appliance** den Namen der Azure Migrate-Appliance aus, die Sie eingerichtet haben, und dann **OK**.

    ![Quelleinstellungen](./media/contoso-migration-rehost-vm/source-settings.png)

4. Wählen Sie unter **Virtuelle Computer** die Computer aus, die Sie replizieren möchten.
    - Wenn Sie eine Bewertung für die VMs ausgeführt haben, können Sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Wählen Sie hierzu unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** die Option **Ja** aus.
    - Wählen Sie **Nein** aus, wenn Sie keine Bewertung ausgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls Sie sich für die Verwendung der Bewertung entschieden haben, wählen Sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Auswählen der Bewertung](./media/contoso-migration-rehost-vm/select-assessment.png)

5. Suchen Sie unter **Virtuelle Computer** je nach Bedarf nach VMs, und aktivieren Sie alle VMs, die Sie migrieren möchten. Klicken Sie anschließend auf **Next: Zieleinstellungen**.

6. Wählen Sie unter **Zieleinstellungen** das Abonnement und die Zielregion für die Migration aus, und geben Sie die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden. Wählen Sie unter **Virtuelles Netzwerk** das Azure-VNET/-Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

7. Wählen Sie unter **Azure-Hybridvorteil** Folgendes aus:

    - die Option **Nein** aus, falls Sie den Azure-Hybridvorteil nicht anwenden möchten. Klicken Sie dann auf **Weiter**.
    - Wählen Sie **Ja** aus, wenn Sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Klicken Sie dann auf **Weiter**.

8. Überprüfen Sie unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste für die VM-Größe die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der höchsten Übereinstimmung im Azure-Abonnement aus. Alternativ können Sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Geben Sie den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben Sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die Sie für die Migration angeben.

9. Geben Sie unter **Datenträger** an, ob die VM-Datenträger in Azure repliziert werden sollen, und wählen Sie in Azure den Datenträgertyp aus (SSD Standard/HDD Standard oder Managed Disks Premium). Klicken Sie dann auf **Weiter**.
    - Sie können Datenträger von der Replikation ausschließen.
    - Wenn Sie Datenträger ausschließen, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

10. Überprüfen Sie unter **Replikation prüfen und starten** die Einstellungen, und klicken Sie auf **Replizieren**, um die erste Replikation für die Server zu starten.

> [!NOTE]
> Sie können die Replikationseinstellungen vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisieren. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-6-migrate-the-database-using-the-azure-database-migration-service"></a>Schritt 6: Migrieren der Datenbank mit dem Azure Database Migration Service

Die Contoso-Administratoren müssen ein Azure Database Migration Service-Projekt erstellen und anschließend die Datenbank migrieren.

### <a name="create-an-azure-database-migration-service-project"></a>Erstellen eines Azure Database Migration Service-Projekts

1. Sie erstellen ein Azure Database Migration Service-Projekt. Als Quellservertyp wählen sie **SQL Server** und als Ziel **Verwaltete Azure SQL-Datenbank-Instanz** aus.

     ![Database Migration Service – Neues Migrationsprojekt](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

2. Der Migrations-Assistent wird geöffnet.

### <a name="migrate-the-database"></a>Migrieren der Datenbank

1. Im Migrations-Assistenten geben die Administratoren die Quell-VM an, auf der sich die lokale Datenbank befindet. Sie geben die Anmeldeinformationen für den Zugriff auf die Datenbank ein.

    ![Database Migration Service – Quelldetails](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

2. Sie wählen die Datenbank (**SmartHotel.Registration**) für die Migration aus:

    ![Database Migration Service – Auswählen der Quelldatenbanken](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source-db.png)

3. Als Ziel geben sie den Namen der verwalteten Instanz in Azure und die Zugangsdaten ein.

    ![Database Migration Service – Zieldetails](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

4. Unter **Neue Aktivität** > **Migration ausführen** geben sie die Einstellungen für die Ausführung der Migration an:
    - Quell- und Zielanmeldeinformationen
    - Zu migrierende Datenbank
    - Die Netzwerkfreigabe, die auf der lokalen VM erstellt wurde. Der Azure Database Migration Service ordnet Quellsicherungen auf dieser Freigabe an.
        - Das Dienstkonto, mit dem die SQL Server-Quellinstanz ausgeführt wird, muss über Schreibberechtigungen für diese Freigabe verfügen.
        - Der FQDN-Pfad zur Freigabe muss verwendet werden.
    - Der SAS-URI, mit dem für den Azure Database Migration Service der Zugriff auf den Speicherkontocontainer gewährt wird, in den der Dienst die Sicherungsdateien für die Migration hochlädt.

        ![Database Migration Service – Konfigurieren der Migrationseinstellungen](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-migration-settings.png)

5. Sie speichern die Migrationseinstellungen und führen anschließend die Migration aus.
6. Der Migrationsstatus wird unter **Übersicht** überwacht.

    ![Database Migration Service – Überwachen](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor1.png)

7. Nach Abschluss der Migration überprüfen die Administratoren, ob die Zieldatenbanken auf der verwalteten Instanz vorhanden sind.

    ![Database Migration Service – Überprüfen der Datenbankmigration](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor2.png)

## <a name="step-7-migrate-the-vms-with-azure-migrate-server-migration"></a>Schritt 7: Migration der virtuellen Computer mit der Azure Migrate-Servermigration

Die Contoso-Administratoren führen eine schnelle Testmigration aus, überprüfen, ob die VM ordnungsgemäß funktioniert, und migrieren dann die VM.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** auf **Migrierte Server testen**.

     ![Testen der migrierten Server](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Klicken Sie mit der rechten Maustaste auf die zu testende VM, und klicken Sie anschließend auf **Testmigration**.

    ![Testmigration](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. Wählen Sie unter **Testmigration** das Azure VNET aus, in dem sich die Azure-VM nach der Migration befindet. Es empfiehlt sich, ein nicht für die Produktion bestimmtes VNET zu verwenden.
4. Der Auftrag **Testmigration** wird gestartet. Überwachen Sie den Auftrag anhand der Portalbenachrichtigungen.
5. Zeigen Sie die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
6. Klicken Sie nach Abschluss des Tests mit der rechten Maustaste unter **Aktuell replizierte Computer** auf die Azure-VM, und klicken Sie anschließend auf **Testmigration bereinigen**.

    ![Bereinigen der Migration](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrieren der VMs

Die Contoso-Administratoren führen jetzt eine vollständige Migration aus, um die Verlagerung abzuschließen.

1. Klicken Sie im Azure Migrate-Projekt unter **Server** > **Azure Migrate: Servermigration** auf **Server werden repliziert**.

    ![Replizieren der Server](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. Klicken Sie unter **Aktuell replizierte Computer** mit der rechten Maustaste auf die VM und dann auf **Migrieren**.
3. Wählen Sie unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. So wird sichergestellt, dass keine Daten verloren gehen.
    - Falls Sie die VM nicht herunterfahren möchten, wählen Sie **Nein** aus.
4. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Verfolgen Sie den Auftrag anhand der Azure-Benachrichtigungen nach.
5. Nach Abschluss des Auftrags können Sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.
6. Schließlich aktualisiert Contoso die DNS-Datensätze für **WEBVM** auf einem der Contoso-Domänencontroller.

### <a name="update-the-connection-string"></a>Aktualisieren der Verbindungszeichenfolge

Der letzte Schritt im Migrationsprozess besteht darin, dass die Contoso-Administratoren die Verbindungszeichenfolge der Anwendung aktualisieren, um auf die migrierte Datenbank zu verweisen, die auf der verwalteten Instanz von Contoso ausgeführt wird.

1. Um im Azure-Portal nach der neuen Verbindungszeichenfolge im Azure-Portal zu suchen, klicken sie auf **Einstellungen** > **Verbindungszeichenfolgen**.

    ![Verbindungszeichenfolgen](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

2. Sie aktualisieren die Zeichenfolge mit dem Benutzernamen und Kennwort der verwalteten SQL-Datenbank-Instanz.
3. Nachdem die Zeichenfolge konfiguriert wurde, ersetzen sie die aktuelle Verbindungszeichenfolge in der Datei „web.config“ der Anwendung.
4. Nach dem Aktualisieren und Speichern der Datei starten sie IIS auf WEBVM neu, indem sie in einem Eingabeaufforderungsfenster `iisreset /restart` ausführen.
5. Nach dem Neustart von IIS nutzt die App die Datenbank, die auf der verwalteten Azure SQL-Datenbank-Instanz ausgeführt wird.
6. An diesem Punkt können die Administratoren den SQLVM-Computer lokal herunterfahren. Die Migration wurde abgeschlossen.

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über die [Durchführung eines Testfailovers](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure).
- Informieren Sie sich über das [Erstellen eines Wiederherstellungsplans](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).
- Erfahren Sie, wie Sie [das Failover in Azure ausführen](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration wird die SmartHotel360-App auf einem Azure-VM ausgeführt, und die SmartHotel360-Datenbank befindet sich in der verwalteten Azure SQL-Datenbank-Instanz.

Contoso muss nun die folgenden Bereinigungsschritte ausführen:

- Entfernen des WEBVM-Computers aus dem vCenter Server-Bestand
- Entfernen des SQLVM-Computers aus dem vCenter Server-Bestand
- Entfernen von WEBVM und SQLVM aus lokalen Sicherungsaufträgen
- Aktualisieren der internen Dokumentation zum Anzeigen des neuen Speicherorts und der IP-Adresse für WEBVM
- Entfernen von SQLVM aus der internen Dokumentation. Alternativ hierzu kann Contoso die Dokumentation auch überarbeiten, um anzugeben, dass SQLVM gelöscht wurde und nicht mehr im VM-Bestand enthalten ist.
- Überprüfen aller Ressourcen, die mit den außer Betrieb genommenen VMs interagieren. Alle relevanten Einstellungen bzw. Dokumentationsinhalte müssen aktualisiert werden, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Das Contoso-Sicherheitsteam überprüft die Azure-VMs und die verwaltete SQL-Datenbank-Instanz, um eine Überprüfung auf eventuelle Sicherheitsprobleme bei der Implementierung durchzuführen:

- Das Team überprüft die Netzwerksicherheitsgruppen, die zum Steuern des Zugriffs für den virtuellen Computer verwendet werden. Mit Netzwerksicherheitsgruppen kann sichergestellt werden, dass nur Datenverkehr, der für die App zulässig ist, passieren kann.
- Das Sicherheitsteam von Contoso erwägt auch, die Daten auf dem Datenträger per Azure Disk Encryption und Azure Key Vault zu schützen.
- Das Team aktiviert die Bedrohungserkennung auf der verwalteten Instanz. Bei der Bedrohungserkennung wird eine Benachrichtigung mit dem Hinweis, dass ein Ticket erstellt werden soll, an das Sicherheitsteam von Contoso bzw. das Service Desk-System gesendet. Erfahren Sie mehr zur [Bedrohungserkennung für verwaltete Instanzen](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-threat-detection).

     ![Sicherheit der verwalteten Instanz – Bedrohungserkennung](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-security.png)

Weitere Informationen zu den Sicherheitsmethoden für VMs finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>BCDR

Für die Geschäftskontinuität und Notfallwiederherstellung (Business Continuity & Disaster Recovery, BCDR) führt Contoso die folgenden Aktionen durch:

- Schützen von Daten: Contoso sichert die Daten auf den VMs mithilfe des Azure Backup-Diensts. [Weitere Informationen](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=/azure/virtual-machines/linux/toc.json)
- Sicherstellen eines unterbrechungsfreien Betriebs der Apps: Contoso repliziert die App-VMs in Azure mithilfe von Site Recovery in einer sekundären Region. [Weitere Informationen](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
- Contoso ruft weitere Informationen zum Verwalten der verwalteten SQL-Instanz ab, einschließlich von [Datenbanksicherungen](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Contoso verfügt über eine vorhandene Lizenzierung für WEBVM. Contoso konvertiert die vorhandene Azure-VM, um die günstigeren Preise über den Azure-Hybridvorteil zu nutzen.
- Contoso verwendet [Azure Cost Management](https://azure.microsoft.com/services/cost-management), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel weist Contoso der SmartHotel360-App in Azure einen neuen Host zu, indem das Unternehmen die Front-End-VM der App mithilfe des Azure Migrate-Diensts zu Azure migriert. Contoso migriert die lokale Datenbank zu einer verwalteten Azure SQL-Datenbank-Instanz, indem der Database Migration Service von Azure verwendet wird.
