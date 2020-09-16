---
title: Neuhosten einer lokalen Anwendung durch Migration zu Azure-VMs und Azure SQL Managed Instance
description: Es wird beschrieben, wie Contoso für eine lokale Anwendung mit Azure SQL Managed Instance auf Azure-VMs einen neuen Host zuweist.
author: givenscj
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: da6c543bf16434bf0228df3a1bcac163ef1fe4ab
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602598"
---
<!-- cSpell:ignore WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc NSGs agentless SQLMI iisreset -->

# <a name="rehost-an-on-premises-application-by-migrating-to-azure-vms-and-azure-sql-managed-instance"></a>Neuhosten einer lokalen Anwendung durch Migration zu Azure-VMs und Azure SQL Managed Instance

In diesem Artikel wird veranschaulicht, wie das fiktive Unternehmen Contoso eine zweistufige .NET-Front-End-Anwendung für Windows, die auf virtuellen VMware-Computern (VMs) ausgeführt wird, mit Azure Migrate zu einer Azure-VM migriert. Außerdem wird erläutert, wie Contoso die Anwendungsdatenbank zu Azure SQL Managed Instance migriert.

Die in diesem Beispiel verwendete SmartHotel360-Anwendung wird quelloffen bereitgestellt. Wenn Sie diese Anwendung für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team von Contoso hat eng mit den Geschäftspartnern des Unternehmens zusammengearbeitet, um zu verstehen, was mit dieser Migration erreicht werden soll. Sie möchten Folgendes erreichen:

- **Unternehmenswachstum.** Contoso wächst. Aus diesem Grund hat der Druck auf die lokalen Systeme und die Infrastruktur des Unternehmens zugenommen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und die Prozesse für seine Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit für das Unternehmen verschwenden, um Kundenanforderungen schneller zu bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Sie muss schneller reagieren, als sich die Gegebenheiten des Markts ändern, damit das Unternehmen auf dem globalen Markt Erfolg hat. Die IT-Abteilung von Contoso darf keine Hindernisse in den Weg stellen und keine Geschäftsabläufe blockieren.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich Ziele für die Migration gesetzt. Das Unternehmen nutzt die Migrationsziele, um die beste Migrationsmethode zu ermitteln.

- Nach der Migration sollte die Anwendung in Azure die gleichen Leistungsmerkmale aufweisen, über die sie derzeit in der lokalen VMware-Umgebung von Contoso verfügt. Die Umstellung auf die Cloud bedeutet nicht, dass die Leistung der Anwendung weniger wichtig ist.
- Contoso möchte nicht in die Anwendung investieren. Die Anwendung ist unternehmenskritisch, aber Contoso möchte sie einfach in ihrer jetzigen Form in die Cloud verlagern.
- Datenbankverwaltungsaufgaben sollten nach der Migration der Anwendung auf ein Minimum reduziert sein.
- Contoso möchte für diese Anwendung nicht Azure SQL-Datenbank einsetzen. Das Unternehmen ist auf der Suche nach Alternativen.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen des Unternehmens formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess. Die Azure-Dienste, die für die Migration verwendet werden sollen, werden ebenfalls identifiziert.

### <a name="current-architecture"></a>Aktuelle Architektur

- Contoso verfügt über ein zentrales Rechenzentrum (`contoso-datacenter`). Das Rechenzentrum befindet sich im Osten der USA in New York City.
- Contoso verfügt in den USA über drei weitere Niederlassungen.
- Das Hauptrechenzentrum ist über eine Metro-Ethernet-Glasfaserverbindung mit einer Kapazität von 500 MBit/s mit dem Internet verbunden.
- Jede Niederlassung ist lokal über Business-Class-Verbindungen mit dem Internet verbunden, und IPsec-VPN-Tunnel führen zurück zum zentralen Rechenzentrum. Aufgrund dieser Anordnung ist das gesamte Netzwerk von Contoso dauerhaft verbunden, und die Internetverbindung wird optimiert.
- Das Hauptrechenzentrum ist vollständig mit VMware virtualisiert. Contoso verfügt über zwei ESXi 6.5-Virtualisierungshosts, die mit vCenter Server 6.5 verwaltet werden.
- Contoso nutzt Active Directory für die Identitätsverwaltung. Contoso verwendet im internen Netzwerk DNS-Server.
- Contoso verfügt über einen lokalen Domänencontroller (`contosodc1`).
- Die Domänencontroller werden auf VMware-VMs ausgeführt. Die Domänencontroller in lokalen Niederlassungen werden auf physischen Servern ausgeführt.
- Die SmartHotel360-Anwendung ist auf zwei VMs (`WEBVM` und `SQLVM`) verteilt, die sich auf einem VMware ESXi-Host der Version 6.5 (`contosohost1.contoso.com`) befinden.
- Die VMware-Umgebung wird von vCenter Server 6.5 (`vcenter.contoso.com`) auf einer VM verwaltet.

![Diagramm: Aktuelle Architektur von Contoso](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

In diesem Szenario möchte Contoso seine lokale zweischichtige Anwendung für Reisen folgendermaßen migrieren:

- Die Anwendungsdatenbank (`SmartHotelDB`) soll zu einer SQL Managed Instance migriert werden.
- Die Front-End-`WEBVM` soll zu einer Azure-VM migriert werden.
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

![Diagramm der Szenarioarchitektur.](./media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Managed Instance durchgeführt. Die folgenden Überlegungen haben dem Unternehmen dabei geholfen, sich für SQL Managed Instance zu entscheiden.

- SQL Managed Instance bietet eine nahezu uneingeschränkte Kompatibilität mit der aktuellen lokalen SQL Server-Version. Wir empfehlen die Nutzung von SQL Managed Instance für Kunden, die SQL Server lokal oder auf einer IaaS-VM (Infrastructure-as-a-Service) ausführen und ihre Anwendungen mit minimalen Entwurfsänderungen zu einem vollständig verwalteten Dienst migrieren möchten.
- Contoso plant die Migration vieler Anwendungen von der lokalen Ausführung zu IaaS. Viele dieser Anwendungen werden vom ISV bereitgestellt. Contoso hat erkannt, dass SQL Managed Instance für die Datenbankkompatibilität dieser Anwendungen sorgt, während SQL-Datenbank möglicherweise nicht unterstützt wird.
- Contoso kann mit dem vollständig automatisierten Azure Database Migration Service-Dienst eine Lift & Shift-Migration zu SQL Managed Instance ausführen. Außerdem kann Contoso diesen Dienst für spätere Datenbankmigrationen erneut einsetzen.
- SQL Managed Instance unterstützt den SQL Server-Agent, eine wichtige Komponente der Anwendung SmartHotel360. Contoso benötigt diese Kompatibilität. Andernfalls müssen die erforderlichen Wartungspläne für diese Anwendung geändert werden.
- Dank Software Assurance kann Contoso seine vorhandenen Lizenzen über den Azure-Hybridvorteil für SQL Server gegen SQL Managed Instance zu ermäßigten Preisen austauschen. Aus diesem Grund kann Contoso für SQL Managed Instance bis zu 30 Prozent Kosten sparen.
- Verwaltete SQL-Instanzen sind vollständig in das virtuelle Netzwerk integriert und bieten somit mehr Isolation und Sicherheit für die Daten von Contoso. Contoso kann die Vorteile der öffentlichen Cloud nutzen und gleichzeitig die Umgebung vom öffentlichen Internet isolieren.
- SQL Managed Instance unterstützt viele Sicherheitsfunktionen. Hierzu zählen Always Encrypted, dynamische Datenmaskierung, Sicherheit auf Zeilenebene und Bedrohungserkennung.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | `WEBVM` wird ohne Änderungen in Azure verlagert. Die Migration ist also sehr einfach. <br><br> Die verwaltete SQL-Instanz unterstützt die technischen Anforderungen und Ziele von Contoso. <br><br> SQL Managed Instance ermöglicht eine 100-prozentige Kompatibilität mit der aktuellen Bereitstellung von Contoso und gleichzeitig die Aussonderung von SQL Server 2008 R2 für das Unternehmen. <br><br> Contoso kann seine Investition in die Software Assurance und den Azure-Hybridvorteil für SQL Server und Windows Server nutzen. <br><br> Contoso kann Azure Database Migration Service für weitere zukünftige Migrationen nutzen. <br><br> Die verwaltete SQL-Instanz verfügt über eine integrierte Fehlertoleranz, die nicht von Contoso konfiguriert werden muss. Mit diesem Feature wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist. |
| **Nachteile** | Auf `WEBVM` wird Windows Server 2008 R2 ausgeführt. Obwohl dieses Betriebssystem von Azure unterstützt wird, handelt es sich nicht mehr um eine unterstützte Plattform. Weitere Informationen finden Sie unter [Supportrichtlinie für Microsoft SQL Server-Produkte](https://support.microsoft.com/help/956893). <br><br> Die Webschicht bleibt ein Single Point of Failure, weil nur `WEBVM` Dienste bereitstellt. <br><br> Contoso muss die Webschicht der Anwendung weiterhin als virtuellen Computer unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service umzustellen. <br><br> Für die Datenschicht stellt SQL Managed Instance unter Umständen nicht die beste Lösung dar, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen oder Drittanbieteranwendungen mit SQL Server ausführen möchte. Eine Ausführung von SQL Server auf einer IaaS-VM könnte diese Flexibilität bieten. |

### <a name="migration-process"></a>Migrationsprozess

Contoso migriert die Web- und Datenschichten seiner SmartHotel360-Anwendung mit den folgenden Schritten zu Azure:

1. Contoso hat bereits eine Azure-Infrastruktur eingerichtet, sodass für dieses Szenario nur noch einige bestimmte Azure-Komponenten hinzugefügt werden müssen.
1. Die Datenschicht wird mithilfe von Azure Database Migration Service migriert. Der Dienst stellt über eine Site-to-Site-VPN-Verbindung zwischen dem Contoso-Rechenzentrum und Azure eine Verbindung mit der lokalen SQL Server-VM her. Der Dienst migriert dann die Datenbank.
1. Die Webschicht wird per „Lift & Shift“-Migration mit Azure Migrate migriert. Dieser Prozess umfasst das Vorbereiten der lokalen VMware-Umgebung, das Einrichten und Aktivieren der Replikation und das Migrieren der VMs per Failover zu Azure.

     ![Diagramm: Migrationsarchitektur](./media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Database Migration Service](/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration mehrerer Datenbankquellen zu Azure-Datenplattformen mit minimaler Downtime. | Informieren Sie sich über die [unterstützten Regionen](/azure/dms/dms-overview#regional-availability) und die [Preise für Azure Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Verwaltete Azure SQL-Datenbank-Instanz](/azure/sql-database/sql-database-managed-instance) | SQL Managed Instance ist ein verwalteter Datenbankdienst, der eine vollständig verwaltete SQL Server-Instanz in der Azure-Cloud darstellt. Bei diesem Dienst wird der gleiche Code wie bei der neuesten Version der Microsoft SQL Server-Datenbank-Engine genutzt, und er verfügt über die neuesten Features, Leistungsverbesserungen und Sicherheitspatches. | Bei Verwendung einer in Azure ausgeführten Instanz von SQL Managed Instance fallen Gebühren je nach Kapazität an. Lesen Sie mehr zu den [Preisen für SQL Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed). |
| [Azure Migrate](/azure/migrate/migrate-services-overview) | Contoso verwendet Azure Migrate, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | Azure Migrate ist ohne Aufpreis erhältlich. Je nach den Tools (Originalanbieter oder ISV), die für die Bewertung und Migration verwendet werden, können aber ggf. Gebühren anfallen. Weitere Informationen zu den Preisen von Azure Migrate finden Sie [hier](https://azure.microsoft.com/pricing/details/azure-migrate). |

## <a name="prerequisites"></a>Voraussetzungen

Contoso und andere Benutzer müssen für dieses Szenario die unten angegebenen Voraussetzungen erfüllen.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat bereits im ersten Artikel dieser Reihe ein Abonnement erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, sollten Sie mit dem Administrator des Abonnements zusammenarbeiten, damit er Ihnen für die erforderlichen Ressourcengruppen und Ressourcen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie unter [Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) beschrieben. |
| **Lokale Server** | Auf dem lokalen vCenter-Server sollte Version 5.5, 6.0 oder 6.5 ausgeführt werden. <br><br> Auf einem ESXi-Host sollte die Version 5.5, 6.0 oder 6.5 ausgeführt werden. <br><br> Mindestens eine VMware-VM sollte auf dem ESXi-Host ausgeführt werden. |
| **Lokale VMs** | [Überprüfen Sie Linux-Computer](/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird. |
| **Database Migration Service** | Für Azure Database Migration Service benötigen Sie ein [kompatibles lokales VPN-Gerät](/azure/vpn-gateway/vpn-gateway-about-vpn-devices). <br><br> Sie müssen das lokale VPN-Gerät konfigurieren können. Es muss über eine externe öffentliche IPv4-Adresse verfügen. Diese Adresse darf sich nicht hinter einem NAT-Gerät befinden. <br><br> Stellen Sie sicher, dass Sie Zugriff auf Ihre lokale SQL Server-Datenbank haben. <br><br> Windows-Firewall sollte auf die Quelldatenbank-Engine zugreifen können. Informieren Sie sich, wie Sie [Windows Defender Firewall für den Datenbank-Engine-Zugriff konfigurieren](/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access). <br><br> Wenn sich eine Firewall vor dem Datenbankcomputer befindet, sollten Sie Regeln hinzufügen, um den Zugriff auf die Datenbank und auf Dateien über SMB-Port 445 zuzulassen. <br><br> Für die zum Herstellen einer Verbindung zwischen der SQL Server-Quellinstanz und der jeweiligen SQL Managed Instance-Zielinstanz verwendeten Anmeldeinformationen muss sichergestellt sein, dass es sich jeweils um Mitglieder der Serverrolle „sysadmin“ handelt. <br><br> Sie benötigen eine Netzwerkfreigabe in der lokalen Datenbank, die von Azure Database Migration Service zum Sichern der Quelldatenbank verwendet werden kann. <br><br> Vergewissern Sie sich, dass das Dienstkonto, mit dem die SQL Server-Quellinstanz ausgeführt wird, über Schreibberechtigungen für die Netzwerkfreigabe verfügt. <br><br> Notieren Sie sich einen Windows-Benutzernamen, der über eine Berechtigung für Vollzugriff auf die Netzwerkfreigabe verfügt, und das zugehörige Kennwort. Azure Database Migration Service verwendet diese Benutzeranmeldeinformationen, um Sicherungsdateien in den Azure Storage-Container hochzuladen. <br><br> Bei der SQL Server Express-Installation wird das TCP/IP-Protokoll standardmäßig auf **Deaktiviert** gesetzt. Stellen Sie sicher, dass es aktiviert ist. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso plant die Einrichtung der Bereitstellung wie folgt:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten einer Instanz von SQL Managed Instance.** Contoso benötigt eine bereits vorhandene verwaltete Instanz, zu der die lokale SQL Server-Datenbank-Instanz migriert wird.
> - **Schritt 2: Vorbereiten von Azure Database Migration Service** Contoso muss den Datenbankmigrationsanbieter registrieren, eine Instanz erstellen und dann ein Database Migration Service-Projekt erstellen. Außerdem muss Contoso einen SAS-URI (Shared Access Signature Uniform Resource Identifier) für die Database Migration Service-Instanz einrichten. Ein SAS-URI ermöglicht den delegierten Zugriff auf Ressourcen im Speicherkonto von Contoso, damit Contoso eingeschränkte Berechtigungen für Speicherobjekte gewähren kann. Contoso richtet einen SAS-URI ein, damit Azure Database Migration Service auf den Speicherkontocontainer zugreifen kann, in den der Dienst die SQL Server-Sicherungsdateien hochlädt.
> - **Schritt 3: Vorbereiten von Azure für das Azure Migrate- Servermigrationstool.** Contoso fügt das Tool für die Servermigration dem Azure Migrate-Projekt hinzu.
> - **Schritt 4: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration.** Contoso bereitet Konten für die VM-Ermittlung sowie das Herstellen einer Verbindung mit Azure-VMs nach der Migration vor.
> - **Schritt 5: Replizieren der lokalen VMs.** Contoso richtet die Replikation ein und beginnt mit der VM-Replikation in Azure Storage.
> - **Schritt 6: Migrieren der Datenbank mithilfe von Azure Database Migration Service** Contoso migriert die Datenbank.
> - **Schritt 7: Migrieren der VMs mit der Azure Migrate- Servermigration.** Contoso führt eine Testmigration durch, um sicherzustellen, dass alles funktioniert. Anschließend wird eine vollständige Migration durchgeführt, um die VMs nach Azure zu verlagern.

## <a name="step-1-prepare-a-sql-managed-instance"></a>Schritt 1: Vorbereiten einer Instanz von SQL Managed Instance

Contoso benötigt ein Subnetz, das die folgenden Anforderungen erfüllt, um eine Instanz von SQL Managed Instance einzurichten:

- Das Subnetz muss dediziert sein. Es muss leer sein. Es kann keinen anderen Clouddienst enthalten. Das Subnetz darf kein Gatewaysubnetz sein.
- Nachdem die verwaltete Instanz erstellt wurde, sollte Contoso dem Subnetz keine Ressourcen mehr hinzufügen.
- Dem Subnetz darf keine Netzwerksicherheitsgruppe zugeordnet sein.
- Das Subnetz muss über eine benutzerdefinierte Routingtabelle verfügen. Die einzige zugewiesene Route sollte `0.0.0.0/0` sein (nächster Hop „Internet“).
- Wenn ein optionales benutzerdefiniertes DNS für das virtuelle Netzwerk angegeben wird, muss die virtuelle IP-Adresse `168.63.129.16` für die rekursiven Resolver in Azure zur Liste hinzugefügt werden. Informieren Sie sich, wie Sie [ein benutzerdefiniertes DNS für SQL Managed Instance konfigurieren](/azure/sql-database/sql-database-managed-instance-custom-dns).
- Dem Subnetz darf kein Dienstendpunkt (Speicher oder SQL) zugeordnet sein. Dienstendpunkte sollten im virtuellen Netzwerk deaktiviert sein.
- Das Subnetz muss mindestens 16 IP-Adressen aufweisen. Informieren Sie sich über das [Bestimmen der Größe des Subnetzes für verwaltete Instanzen](/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- In der Hybridumgebung von Contoso sind benutzerdefinierte DNS-Einstellungen erforderlich. Contoso konfiguriert die DNS-Einstellungen so, dass mindestens ein Azure DNS-Server des Unternehmens genutzt wird. Informieren Sie sich über die [DNS-Anpassung](/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Einrichten eines virtuellen Netzwerks für die verwaltete Instanz

Die Contoso-Administratoren führen Folgendes durch, um das virtuelle Netzwerk einzurichten:

1. Sie erstellen ein neues virtuelles Netzwerk (`VNET-SQLMI-EU2`) in der primären Region (`East US 2`). Sie fügen das virtuelle Netzwerk der Ressourcengruppe `ContosoNetworkingRG` hinzu.
1. Sie weisen den Adressraum `10.235.0.0/24` zu. Es wird sichergestellt, dass der Bereich zu keinerlei Überschneidungen mit anderen Netzwerken im Unternehmen führt.
1. Dem Netzwerk werden zwei Subnetze hinzugefügt:
    - `SQLMI-DS-EUS2` (`10.235.0.0/25`).
    - `SQLMI-SAW-EUS2` (`10.235.0.128/29`). Dieses Subnetz wird verwendet, um ein Verzeichnis an die verwaltete Instanz anzufügen.

      ![Screenshot zu SQL Managed Instance: Bereich „Virtuelles Netzwerk erstellen“](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

1. Nach der Bereitstellung des virtuellen Netzwerks und der Subnetze wird das folgende Netzwerkpeering eingerichtet:

    - Peering zwischen `VNET-SQLMI-EUS2` und `VNET-HUB-EUS2` (das virtuelle Hubnetzwerk in `East US 2`)
    - Peering zwischen `VNET-SQLMI-EUS2` und `VNET-PROD-EUS2` (das Produktionsnetzwerk)

      ![Screenshot: Netzwerkpeering](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

1. Es werden benutzerdefinierte DNS-Einstellungen festgelegt. Das DNS verweist zuerst auf den Azure-Domänencontroller von Contoso. Das Azure DNS ist der sekundäre Verweis. Die Azure-Domänencontroller von Contoso befinden sich an den folgenden Orten:

    - Im Subnetz `PROD-DC-EUS2` im Produktionsnetzwerk `East US 2` (`VNET-PROD-EUS2`)
    - Adresse von `CONTOSODC3`: `10.245.42.4`
    - Adresse von `CONTOSODC4`: `10.245.42.5`
    - Azure DNS-Auflösung: `168.63.129.16`

      ![Screenshot: Netzwerk-DNS-Server](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Benötigen Sie weitere Hilfe?**

- Lesen Sie die [Übersicht zu SQL Managed Instance](/azure/sql-database/sql-database-managed-instance).
- Informieren Sie sich über das [Konfigurieren eines vorhandenen virtuellen Netzwerks für Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- Erfahren Sie, wie Sie das [Peering einrichten](/azure/virtual-network/virtual-network-manage-peering).
- Erfahren Sie, wie Sie die [DNS-Einstellungen für Azure Active Directory aktualisieren](/azure/active-directory-domain-services/tutorial-create-instance).

### <a name="set-up-routing"></a>Einrichten des Routings

Die verwaltete Instanz wird in einem privaten virtuellen Netzwerk angeordnet. Contoso benötigt eine Routingtabelle für das virtuelle Netzwerk, um mit dem Azure-Verwaltungsdienst zu kommunizieren. Wenn das virtuelle Netzwerk nicht mit dem Dienst kommunizieren kann, von dem es verwaltet wird, kann nicht mehr auf das virtuelle Netzwerk zugegriffen werden.

Contoso berücksichtigt die folgenden Faktoren:

- Die Routingtabelle enthält Regeln (Routen), die bestimmen, wie von der verwalteten Instanz gesendete Pakete im virtuellen Netzwerk weitergeleitet werden sollen.
- Die Routingtabelle bezieht sich auf Subnetze, in denen verwaltete Instanzen bereitgestellt werden. Jedes Paket, das ein Subnetz verlässt, wird auf Grundlage der entsprechenden Routingtabelle verarbeitet.
- Ein Subnetz kann nur einer Routingtabelle zugeordnet sein.
- Für die Erstellung von Routingtabellen in Microsoft Azure fallen keine zusätzlichen Gebühren an.

 Die Contoso-Administratoren führen die folgenden Schritte aus, um das Routing einzurichten:

1. Sie erstellen eine benutzerdefinierte Routingtabelle in der Ressourcengruppe `ContosoNetworkingRG`.

    ![Screenshot: Routingtabelle](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

1. Nach dem Bereitstellen der Routingtabelle (`MIRouteTable`) fügen sie eine Route mit dem Adresspräfix `0.0.0.0/0` hinzu, um die Anforderungen von SQL Managed Instance zu erfüllen. Die Option **Typ des nächsten Hops** wird auf **Internet** festgelegt.

    ![Screenshot: Routingtabellenpräfix](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

1. Sie ordnen die Routingtabelle dem Subnetz `SQLMI-DB-EUS2` (im Netzwerk `VNET-SQLMI-EUS2`) zu.

    ![Screenshot: Routingtabellensubnetz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über das [Einrichten von Routen für eine verwaltete Instanz](/azure/sql-database/sql-database-managed-instance-get-started).

### <a name="create-a-managed-instance"></a>Erstellen einer verwalteten Instanz

Nun können die Contoso-Administratoren eine Instanz von SQL Managed Instance bereitstellen:

1. Da die verwaltete Instanz als Geschäftsanwendung dient, stellen sie sie in der primären Region des Unternehmens (`East US 2`) bereit. Sie fügen die verwaltete Instanz der Ressourcengruppe `ContosoRG` hinzu.
1. Für die Instanz wird ein Tarif, eine Computegröße und Speicher ausgewählt. Informieren Sie sich über die [Preise für SQL Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Screenshot: Bereich „SQL Managed Instance“](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

1. Nach der Bereitstellung der verwalteten Instanz werden zwei neue Ressourcen in der Ressourcengruppe `ContosoRG` angezeigt:

    - Neue Instanz von SQL Managed Instance
    - ein virtueller Cluster, falls Contoso über mehrere verwaltete Instanzen verfügt

      ![Screenshot: Zwei neue Ressourcen](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich, wie Sie [eine verwaltete Instanz bereitstellen](/azure/sql-database/sql-database-managed-instance-get-started).

## <a name="step-2-prepare-azure-database-migration-service"></a>Schritt 2: Vorbereiten von Azure Database Migration Service

Die Contoso-Administratoren müssen folgende Aufgaben erledigen, um Azure Database Migration Service vorzubereiten:

- Registrieren Sie den Database Migration Service-Anbieter in Azure.
- Sie müssen Database Migration Service die Berechtigung für den Zugriff auf Azure Storage erteilen, damit die Sicherungsdateien für die Migration einer Datenbank hochgeladen werden können. Um den Zugriff auf Azure Storage zu ermöglichen, wird ein Azure Blob Storage-Container erstellt. Außerdem wird ein SAS-URI für den Blob Storage-Container generiert.
- Erstellen eines Azure Database Migration Service-Projekts.

Anschließend werden die folgenden Schritte ausgeführt:

1. Sie registrieren den Anbieter für die Datenbankmigration unter dem Abonnement. ![Screenshot: Database Migration Service-Registrierung](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

1. Sie erstellen einen Azure Blob Storage-Container. Contoso generiert einen SAS-URI, damit Azure Database Migration Service darauf zugreifen kann.

    ![Screenshot: Generieren eines SAS-URI](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

1. Erstellen einer Instanz von Azure Database Migration Service

    ![Screenshot: Erstellen einer Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

1. Die Database Migration Service-Instanz wird im Subnetz `PROD-DC-EUS2` des virtuellen Netzwerks `VNET-PROD-DC-EUS2` platziert.
    - Die Instanz wird dort zugeordnet, weil der Dienst sich in einem virtuellen Netzwerk befinden muss, das über ein VPN-Gateway auf die lokale SQL Server-VM zugreifen kann.
    - Für `VNET-PROD-EUS2` erfolgt ein Peering mit `VNET-HUB-EUS2`, und die Verwendung von Remotegateways ist zulässig. Mit der Option **Remotegateways verwenden** wird sichergestellt, dass die Instanz nach Bedarf kommunizieren kann.

        ![Screenshot: Konfigurieren eines Netzwerks](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich, wie Sie [Azure Database Migration Service einrichten](/azure/dms/quickstart-create-data-migration-service-portal).
- Erfahren Sie, wie Sie [eine SAS erstellen und verwenden](/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-3-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Schritt 3: Vorbereiten von Azure für das Azure Migrate- Tool für die Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein virtuelles Netzwerk, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Azure Migrate: Das Tool für die Azure Migrate-Servermigration wurde bereitgestellt.

Die Contoso-Administratoren richten die folgenden Komponenten ein:

1. Einrichten eines Netzwerks. Contoso hat bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann, als die [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) durchgeführt wurde.

    - Bei der Anwendung „SmartHotel360“ handelt es sich um eine Produktionsanwendung, und die virtuellen Computer werden zum Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) migriert.
    - Beide VMs werden in der Ressourcengruppe `ContosoRG` bereitgestellt, die für Produktionsressourcen verwendet wird.
    - Die Front-End-VM der Anwendung (`WEBVM`) wird zum Front-End-Subnetz (`PROD-FE-EUS2`) des Produktionsnetzwerks migriert.
    - Die Anwendungsdatenbank-VM (`SQLVM`) wird zum Datenbanksubnetz (`PROD-DB-EUS2`) des Produktionsnetzwerks migriert.

## <a name="step-4-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Schritt 4: Vorbereiten der lokalen VMware-Instanz für die Azure Migrate- Servermigration

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Migration der VMs zu Azure benötigt:

- Ein virtuelles Netzwerk, in dem sich Azure-VMs befinden, wenn diese während einer Migration erstellt werden.
- Die bereitgestellte und konfigurierte Azure Migrate-Appliance

Die Contoso-Administratoren richten diese Komponenten ein, indem sie die folgenden Schritte ausführen:

1. Einrichten eines Netzwerks. Contoso hat bereits ein Netzwerk eingerichtet, das für die Azure Migrate-Servermigration verwendet werden kann, als die [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) durchgeführt wurde.

    - Bei der Anwendung „SmartHotel360“ handelt es sich um eine Produktionsanwendung, und die virtuellen Computer werden zum Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) migriert.
    - Beide virtuellen Computer werden in der für Produktionsressourcen verwendeten Ressourcengruppe `ContosoRG` bereitgestellt.
    - Der virtuelle Computer für das Anwendungs-Front-End (`WEBVM`) wird zum Front-End-Subnetz (`PROD-FE-EUS2`) im Produktionsnetzwerk migriert.
    - Der virtuelle Computer für die Anwendungsdatenbank (`SQLVM`) wird zum Datenbanksubnetz (`PROD-DB-EUS2`) im Produktionsnetzwerk migriert.

1. Bereitstellen der Azure Migrate-Appliance:

    1. Laden Sie das OVA-Image von Azure Migrate herunter, und importieren Sie es in VMware.

        ![Screenshot: Herunterladen der OVA-Datei](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    1. Starten Sie das importierte Image, und konfigurieren Sie das Tool, indem Sie die folgenden Schritte ausführen:

       1. Richten Sie die erforderlichen Komponenten ein.

          ![Screenshot: Einrichten der erforderlichen Komponenten](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

       1. Stellen Sie die Verweise des Tools auf das Azure-Abonnement ein.

          ![Screenshot: Auswahl des Abonnements](./media/contoso-migration-rehost-vm/migration-register-azure.png)

       1. Legen Sie die VMware vCenter-Anmeldeinformationen fest.

          ![Screenshot: Festlegen der VMware vCenter-Anmeldeinformationen](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

       1. Fügen Sie alle Linux-basierten oder Windows-basierten Anmeldeinformationen für die Ermittlung hinzu.

          ![Screenshot: Festlegen von Linux- und Windows-Anmeldeinformationen](./media/contoso-migration-rehost-vm/migration-credentials.png)

1. Nach der Konfiguration dauert es einige Zeit, bis das Tool alle virtuellen Computer aufgelistet hat. Nach Abschluss des Vorgangs können die Contoso-Administratoren sehen, dass die VMs in Azure in das Azure Migrate-Tool eingefügt wurden.

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über die [Azure Migrate-Appliance](/azure/migrate/migrate-services-overview#azure-migrate-server-migration-tool).

### <a name="prepare-on-premises-vms"></a>Vorbereiten von lokalen VMs

Nach der Migration möchte Contoso eine Verbindung mit den Azure VMs herstellen und Azure die Erlaubnis zum Verwalten der VMs geben. Die Contoso-Administratoren müssen vor der Migration die folgenden Schritte ausführen:

1. Für den Zugriff über das Internet:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Sicherstellen, dass TCP- und UDP-Regeln zum **öffentlichen** Profil hinzugefügt wurden.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.

1. Für den Zugriff über Site-to-Site-VPN:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.
    - Legen Sie für Windows die SAN-Richtlinie des Betriebssystems auf dem lokalen virtuellen Computer auf **OnlineAll** fest.

1. Sie installieren den Azure-Agent:

    - [Azure Linux-Agent](/azure/virtual-machines/extensions/agent-linux)
    - [Azure Windows-Agent](/azure/virtual-machines/extensions/agent-windows)

1. Weitere Überlegungen:

   - Unter Windows sollten auf dem virtuellen Computer keine ausstehenden Windows-Updates vorhanden sein, wenn Sie eine Migration auslösen. Andernfalls ist nach Abschluss des Updates die Anmeldung bei der VM nicht mehr möglich.
   - Nach der Migration kann **Startdiagnose** aktiviert werden, um einen Screenshot der VM anzuzeigen. Falls dies nicht funktioniert, sollte überprüft werden, ob die VM ausgeführt wird, und die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) gelesen werden.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie [VMs auf die Migration vorbereiten](/azure/migrate/prepare-for-migration).

## <a name="step-5-replicate-the-on-premises-vms"></a>Schritt 5: Replizieren der lokalen VMs

Bevor die Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können sie mit der Replikation von VMware-VMs in Azure beginnen.

1. Im Azure Migrate-Projekt wechseln sie zu **Server** > **Azure Migrate- Servermigration**). Anschließend wählen sie die Option **Replizieren** aus.

    ![Screenshot: Option „Replizieren“](./media/contoso-migration-rehost-vm/select-replicate.png)

1. Unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** wählen sie die Option **Ja, mit VMware vSphere** aus.

1. Unter **Lokale Appliance** wählen sie den Namen der Azure Migrate-Appliance, die eingerichtet wurde, und dann **OK** aus.

    ![Screenshot: Registerkarte „Quelleinstellungen“](./media/contoso-migration-rehost-vm/source-settings.png)

1. Unter **Virtuelle Computer** wählen sie die Computer aus, die repliziert werden sollen:
    - Wenn sie den Bewertungsvorgang für die VMs ausgeführt haben, können sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** wählen sie die Option **Ja** aus.
    - Sie wählen **Nein** aus, wenn sie keine Bewertung durchgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls sie sich für die Verwendung der Bewertung entschieden haben, wählen sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Screenshot: Auswählen von Bewertungen](./media/contoso-migration-rehost-vm/select-assessment.png)

1. Unter **Virtuelle Computer** suchen sie je nach Bedarf nach VMs und aktivieren alle VMs, die migriert werden sollen. Anschließend wählen sie Folgendes aus: **Weiter: Zieleinstellungen**.

1. Unter **Zieleinstellungen** wählen sie das Abonnement und die Zielregion aus, zu der migriert werden soll. Sie geben auch die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden. Unter **Virtuelles Netzwerk** wählen sie das virtuelle Azure-Netzwerk oder -Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

1. Unter **Azure-Hybridvorteil** gehen sie wie folgt vor:

    - Sie wählen die Option **Nein** aus, falls sie den Azure-Hybridvorteil nicht anwenden möchten. Anschließend wählen sie **Weiter** aus.
    - Sie wählen **Ja** aus, wenn sie über Windows Server-Computer verfügen, die durch aktive Software Assurance- oder Windows Server-Abonnements abgedeckt sind, und den Vorteil auf die zu migrierenden Computer anwenden möchten. Anschließend wählen sie **Weiter** aus.

1. Sie überprüfen unter **Compute** den VM-Namen, die Größe, den Typ des Betriebssystemdatenträgers und die Verfügbarkeitsgruppe. Die VMs müssen die [Azure-Anforderungen](/azure/migrate/migrate-support-matrix-vmware#vmware-requirements) erfüllen.

    - **Größe des virtuellen Computers:** Bei Verwendung von Bewertungsempfehlungen enthält die Dropdownliste „VM-Größe“ die empfohlene Größe. Andernfalls wählt Azure Migrate eine Größe basierend auf der größten Übereinstimmung im Azure-Abonnement aus. Alternativ können sie unter **Azure-VM-Größe** manuell eine Größe auswählen.
    - **Betriebssystemdatenträger:** Sie geben den Betriebssystemdatenträger (Startdatenträger) für die VM an. Der Betriebssystemdatenträger enthält den Bootloader und das Installationsprogramm des Betriebssystems.
    - **Verfügbarkeitsgruppe:** Wenn die VM nach der Migration in einer Azure-Verfügbarkeitsgruppe enthalten sein soll, geben sie die Gruppe an. Die Gruppe muss Teil der Zielressourcengruppe sein, die für die Migration angegeben wurde.

1. Unter **Datenträger** geben sie an, ob die VM-Datenträger in Azure repliziert werden sollen. Anschließend wählen sie den Datenträgertyp (SSD/HDD Standard oder verwaltete Premium-Datenträger) in Azure und dann **Weiter** aus.
    - Sie können Datenträger von der Replikation ausschließen.
    - Wenn Datenträger ausgeschlossen werden, sind diese nach der Migration nicht auf der Azure-VM vorhanden.

1. Sie überprüfen die Einstellungen unter **Replikation überprüfen und starten**. Anschließend wählen sie **Replizieren** aus, um die anfängliche Replikation für die Server zu starten.

> [!NOTE]
> Replikationseinstellungen können vor Beginn der Replikation jederzeit unter **Verwalten** > **Aktuell replizierte Computer** aktualisiert werden. Die Einstellungen können nach dem Beginn der Replikation nicht mehr geändert werden.

## <a name="step-6-migrate-the-database-via-azure-database-migration-service"></a>Schritt 6: Migrieren der Datenbank mithilfe von Azure Database Migration Service

Die Contoso-Administratoren müssen ein Database Migration Service-Projekt erstellen und anschließend die Datenbank migrieren.

### <a name="create-an-azure-database-migration-service-project"></a>Erstellen eines Azure Database Migration Service-Projekts

1. Die Administratoren erstellen ein Database Migration Service-Projekt. Als Quellservertyp wählen sie **SQL Server** und als Ziel **Azure SQL Managed Instance** aus.

     ![Screenshot: Bereich „Neues Migrationsprojekt“](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

1. Der Migrations-Assistent wird geöffnet.

### <a name="migrate-the-database"></a>Migrieren der Datenbank

1. Im Migrations-Assistenten geben die Administratoren die Quell-VM an, auf der sich die lokale Datenbank befindet. Sie geben die Anmeldeinformationen für den Zugriff auf die Datenbank ein.

    ![Screenshot: Bereich „Quelldetails“](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

1. Sie wählen die zu migrierende Datenbank (`SmartHotel.Registration`) aus.

    ![Screenshot: Bereich „Quelldatenbanken auswählen“](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source-db.png)

1. Als Ziel geben sie den Namen der verwalteten Instanz in Azure und die Zugangsdaten ein.

    ![Screenshot: Bereich „Zieldetails“](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

1. Unter **Neue Aktivität** > **Migration ausführen** geben sie die Einstellungen für die Ausführung der Migration an:
    - Quell- und Zielanmeldeinformationen
    - Zu migrierende Datenbank
    - Die Netzwerkfreigabe, die auf der lokalen VM erstellt wurde. Azure Database Migration Service veranlasst Quellsicherungen auf dieser Freigabe.
        - Das Dienstkonto, mit dem die SQL Server-Quellinstanz ausgeführt wird, muss über Schreibberechtigungen für diese Freigabe verfügen.
        - Der FQDN-Pfad zur Freigabe muss verwendet werden.
    - Der SAS-URI, mit dem für Azure Database Migration Service der Zugriff auf den Speicherkontocontainer gewährt wird, in den der Dienst die Sicherungsdateien für die Migration hochlädt

        ![Screenshot: Bildschirm „Migrationseinstellungen konfigurieren“](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-migration-settings.png)

1. Sie speichern die Migrationseinstellungen und führen anschließend die Migration aus.
1. Der Migrationsstatus wird unter **Übersicht** überwacht.

    ![Screenshot: Status](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor1.png)

1. Nach Abschluss der Migration überprüfen sie, ob die Zieldatenbanken auf der verwalteten Instanz vorhanden sind.

    ![Screenshot: Überprüfung der Datenbankmigration](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor2.png)

## <a name="step-7-migrate-the-vms-with-azure-migrate-server-migration"></a>Schritt 7: Migrieren der VMs mit der Azure Migrate- Servermigration

Die Contoso-Administratoren führen eine schnelle Testmigration aus und überprüfen, ob die VM richtig funktioniert. Anschließend migrieren sie den virtuellen Computer.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

1. Unter **Migrationsziele** > **Server** > **Azure Migrate: Servermigration** wählen sie die Option **Migrierte Server testen** aus.

     ![Screenshot: Option „Migrierte Server testen“](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

1. Sie wählen und halten die zu testende VM (oder klicken mit der rechten Maustaste darauf) und wählen anschließend **Testmigration** aus.

    ![Screenshot: Option „Testmigration“](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

1. Unter **Testmigration** wählen sie das virtuelle Azure-Netzwerk aus, in dem sich der virtuelle Azure-Computer nach der Migration befindet. Wir empfehlen Ihnen, ein nicht für die Produktion bestimmtes virtuelles Netzwerk zu verwenden.
1. Der Auftrag **Testmigration** wird gestartet. Sie überwachen den Auftrag anhand der Portalbenachrichtigungen.
1. Sie zeigen die migrierte Azure-VM nach Abschluss der Migration im Azure-Portal unter **Virtuelle Computer** an. Der Computername enthält das Suffix **-Test**.
1. Sie wählen und halten nach Abschluss des Tests unter **Aktuell replizierte Computer** die Azure-VM (oder klicken mit der rechten Maustaste darauf) und wählen anschließend **Testmigration bereinigen** aus.

    ![Screenshot: Option „Testmigration bereinigen“](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vm"></a>Migrieren der VM

Die Contoso-Administratoren führen nun eine vollständige Migration aus, um die Verlagerung abzuschließen.

1. Im Azure Migrate-Projekt wechseln sie zu **Server** > **Azure Migrate- Servermigration** und wählen die Option **Server werden repliziert** aus.

    ![Screenshot: Option „Server werden repliziert“](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

1. Sie wählen und halten unter **Aktuell replizierte Computer** die VM (oder klicken mit der rechten Maustaste darauf) und wählen dann **Migrieren** aus.
1. Sie wählen unter **Migrieren** > **Virtuelle Computer herunterfahren und eine geplante Migration ohne Datenverlust durchführen?** die Option **Ja** >  und anschließend **OK** aus.
    - Azure Migrate fährt die lokale VM standardmäßig herunter und führt eine bedarfsabhängige Replikation aus, um alle VM-Änderungen zu synchronisieren, die seit der letzten Replikation vorgenommen wurden. Mit dieser Aktion wird sichergestellt, dass es nicht zu Datenverlusten kommt.
    - Sie wählen **Nein** aus, wenn sie die VM nicht herunterfahren möchten.
1. Für den virtuellen Computer wird ein Migrationsauftrag gestartet. Sie verfolgen den Auftrag anhand der Azure-Benachrichtigungen nach.
1. Nach Abschluss des Auftrags können sie die VM auf der Seite **Virtuelle Computer** anzeigen und verwalten.
1. Schließlich aktualisiert Contoso die DNS-Datensätze für `WEBVM` auf einem der Contoso-Domänencontroller.

### <a name="update-the-connection-string"></a>Aktualisieren der Verbindungszeichenfolge

Der letzte Schritt im Migrationsprozess besteht darin, dass die Contoso-Administratoren die Verbindungszeichenfolge der Anwendung aktualisieren, um auf die migrierte Datenbank zu verweisen, die auf der SQL Managed Instance-Instanz von Contoso ausgeführt wird.

1. Klicken sie auf **Einstellungen** > **Verbindungszeichenfolgen**, um im Azure-Portal nach der neuen Verbindungszeichenfolge zu suchen.

    ![Screenshot: Option „Verbindungszeichenfolgen“](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

1. Sie aktualisieren die Zeichenfolge mit dem Benutzernamen und Kennwort der Instanz von SQL Managed Instance.
1. Nachdem die Zeichenfolge konfiguriert wurde, ersetzen sie die aktuelle Verbindungszeichenfolge in der Datei `web.config` der Anwendung.
1. Nach dem Aktualisieren und Speichern der Datei starten sie IIS auf `WEBVM` neu, indem sie in einem Eingabeaufforderungsfenster `iisreset /restart` ausführen.
1. Nach dem Neustart von IIS nutzt die Anwendung die Datenbank, die auf der SQL Managed Instance-Instanz ausgeführt wird.
1. An diesem Punkt können die Administratoren den lokalen SQLVM-Computer herunterfahren. Die Migration ist abgeschlossen.

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über die [Durchführung eines Testfailovers](/azure/site-recovery/tutorial-dr-drill-azure).
- Informieren Sie sich über das [Erstellen eines Wiederherstellungsplans](/azure/site-recovery/site-recovery-create-recovery-plans).
- Erfahren Sie, wie Sie [das Failover in Azure ausführen](/azure/site-recovery/site-recovery-failover).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration wird die SmartHotel360-Anwendung auf einer Azure-VM ausgeführt, und die SmartHotel360-Datenbank ist auf der Instanz von Azure SQL Managed Instance verfügbar.

Von Contoso müssen nun die folgenden Bereinigungsaufgaben durchgeführt werden:

- Der `WEBVM`-Computer muss aus dem vCenter Server-Bestand entfernt werden.
- Der `SQLVM`-Computer muss aus dem vCenter Server-Bestand entfernt werden.
- `WEBVM` und `SQLVM` müssen aus den lokalen Sicherungsaufträgen entfernt werden.
- Die interne Dokumentation muss mit dem neuen Speicherorts und der IP-Adresse für `WEBVM` aktualisiert werden.
- `SQLVM` muss aus der internen Dokumentation entfernt werden. Alternativ kann Contoso die Dokumentation auch überarbeiten, um anzugeben, dass `SQLVM` gelöscht wurde und nicht mehr im VM-Bestand enthalten ist.
- Überprüfen aller Ressourcen, die mit den außer Betrieb genommenen VMs interagieren. Alle relevanten Einstellungen bzw. Dokumentationsinhalte müssen aktualisiert werden, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Das Contoso-Sicherheitsteam überprüft die Azure-VMs und die Instanz von SQL Managed Instance auf eventuelle Sicherheitsprobleme bei der Implementierung:

- Das Team überprüft die Netzwerksicherheitsgruppen, die zum Steuern des Zugriffs für den virtuellen Computer verwendet werden. Mit Netzwerksicherheitsgruppen kann sichergestellt werden, dass nur Datenverkehr fließt, der für die Anwendung zulässig ist.
- Das Sicherheitsteam von Contoso erwägt auch, die Daten auf dem Datenträger per Azure Disk Encryption und Azure Key Vault zu schützen.
- Das Team aktiviert die Bedrohungserkennung auf der verwalteten Instanz. Bei der Bedrohungserkennung wird eine Benachrichtigung mit dem Hinweis, dass ein Ticket erstellt werden soll, an das Sicherheitsteam von Contoso bzw. das Service Desk-System gesendet. Lesen Sie mehr zur [Bedrohungserkennung für SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-threat-detection).

     ![Screenshot mit dem Bereich für die Sicherheit in SQL Managed Instance: Bildschirm „Bedrohungserkennung“](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-security.png)

Weitere Informationen zu den Sicherheitsmethoden für VMs finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](/azure/security/fundamentals/iaas).

### <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- **Schützen von Daten.** Contoso sichert die Daten auf den VMs mithilfe des Azure Backup-Diensts. Weitere Informationen finden Sie unter [Ein Überblick über die Sicherung von Azure-VMs](/azure/backup/backup-azure-vms-introduction).
- **Aufrechterhalten des Anwendungsbetriebs.** Contoso repliziert die Anwendungs-VMs in Azure mithilfe von Site Recovery in einer sekundären Region. Informieren Sie sich über das [Einrichten der Notfallwiederherstellung in einer sekundären Azure-Region für einen virtuellen Azure-Computer](/azure/site-recovery/azure-to-azure-quickstart).
- **Weitere Informationen.** Contoso ruft weitere Informationen zum Verwalten der Instanz von SQL Managed Instance ab, z. B. [Datenbanksicherungen](/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Contoso verfügt über eine vorhandene Lizenzierung für WEBVM. Contoso konvertiert die vorhandene Azure-VM, um die günstigeren Preise über den Azure-Hybridvorteil zu nutzen.
- Contoso verwendet [Azure Cost Management und Abrechnung](/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget vom Unternehmen nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso für die SmartHotel360-Anwendung in Azure einen neuen Host zuweist, indem die Front-End-VM der Anwendung mit Azure Migrate zu Azure migriert wird. Contoso migriert die lokale Datenbank zu einer Instanz von Azure SQL Managed Instance, indem Database Migration Service von Azure verwendet wird.
