---
title: Umgestalten einer lokalen Anwendung zu einer Azure App Service-Web-App und einer Instanz von SQL Managed Instance
description: Hier erfahren Sie, wie das Unternehmen Contoso einer lokalen Anwendung einen neuen Host zuweist, indem es sie zu einer Azure App Service-Web-App und einer Instanz von SQL Managed Instance migriert.
author: givenscj
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 2c46ade2fe117898cd1afa9b976c87ae9baf5e6c
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86234853"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM contosohost vcenter contosodc smarthotel SQLMI SHWCF SHWEB -->

# <a name="refactor-an-on-premises-application-to-an-azure-app-service-web-app-and-an-sql-managed-instance"></a>Umgestalten einer lokalen Anwendung zu einer Azure App Service-Web-App und einer Instanz von SQL Managed Instance

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso eine Windows .NET-Anwendung mit zwei Ebenen, die auf VMware-VMs ausgeführt wird, im Rahmen einer Migration zu Azure umgestaltet. Contoso migriert die Front-End-VM der Anwendung zu einer Azure App Service-Web-App. Außerdem wird erläutert, wie Contoso die Anwendungsdatenbank zu Azure SQL Managed Instance migriert.

Die in diesem Beispiel verwendete Anwendung SmartHotel360 wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und damit steigt die Last auf den lokalen Systeme und Infrastrukturen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigerung der Flexibilität.**  Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Es darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Anwendung** | Die Anwendung wird in Azure so wichtig bleiben wie heute. <br><br> Sie sollte die gleichen Leistungsmerkmale wie aktuell in VMware aufweisen. <br><br> Das Team möchte nicht in die Anwendung investieren. Vorerst werden die Administratoren die Anwendung daher lediglich sicher in die Cloud verschieben. <br><br> Das Team möchte die Unterstützung für Windows Server 2008 R2 einstellen, das Betriebssystem, unter dem die Anwendung derzeit ausgeführt wird. <br><br> Das Team möchte SQL Server 2008 R2 generell nicht mehr verwenden und zu einer modernen PaaS-Datenbankplattform wechseln, die den Verwaltungsaufwand minimiert. <br><br> Seine Investitionen in die SQL Server-Lizenzierung und in die Software Assurance möchte Contoso nutzen, wo immer dies möglich ist. <br><br> Darüber hinaus möchte Contoso die Auswirkungen des Single Point of Failure in der Webebene abschwächen. |
| **Einschränkungen** | Die Anwendung besteht aus einer ASP.NET-Anwendung und einem WCF-Dienst, die auf derselben VM ausgeführt werden. Über den Azure App Service soll dies auf zwei Web-Apps aufgeteilt werden. |
| **Azure** | Contoso möchte die Anwendung zu Azure migrieren, jedoch nicht auf VMs ausführen. Sowohl in der Web- als auch in der Datenschicht soll auf Azure-PaaS-Dienste zurückgegriffen werden. |
| **DevOps** | Contoso möchte auf ein DevOps-Modell umsteigen und Azure DevOps für Builds und Releasepipelines verwenden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-application"></a>Aktuelle Anwendung

- Die lokale Anwendung SmartHotel360 ist auf zwei VMs aufgeteilt (`WEBVM` und `SQLVM`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Für die Webebene der Anwendung hat sich Contoso für die Verwendung von Azure App Service entschieden. Über diesen PaaS-Dienst kann die Anwendung mit nur wenigen Konfigurationsänderungen bereitgestellt werden. Contoso führt die Änderung mit Visual Studio durch und stellt zwei Web-Apps bereit. Eine für die Website, und eine für den WCF-Dienst.
- Um die Anforderungen einer DevOps-Pipeline erfüllen zu können, hat Contoso Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys ausgewählt. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service bereitgestellt.

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Managed Instance durchgeführt. Die folgenden Überlegungen haben dabei zu der Entscheidung für SQL Managed Instance geführt.

- SQL Managed Instance bietet eine nahezu uneingeschränkte Kompatibilität mit der aktuellen lokalen SQL Server-Version. Microsoft empfiehlt SQL Managed Instance für Kunden, die SQL Server lokal oder auf einer IaaS-VM ausführen und ihre Anwendungen mit minimalen Entwurfsänderungen zu einem vollständig verwalteten Dienst migrieren möchten.
- Contoso plant die Migration vieler Anwendungen von der lokalen Ausführung zu IaaS. Viele dieser Apps werden durch einen unabhängigen Softwarehersteller (ISV) bereitgestellt. Contoso hat erkannt, dass SQL Managed Instance die Datenbankkompatibilität dieser Anwendungen sicherstellt, während SQL-Datenbank möglicherweise nicht unterstützt wird.
- Contoso kann mit dem vollständig automatisierten Azure Database Migration Service-Tool ganz einfach eine Lift & Shift-Migration zu SQL Managed Instance durchführen. Außerdem kann Contoso diesen Dienst für spätere Datenbankmigrationen erneut einsetzen.
- SQL Managed Instance unterstützt den SQL Server-Agent, eine wichtige Komponente der Anwendung SmartHotel360. Contoso benötigt diese Kompatibilität, weil ansonsten die erforderlichen Wartungspläne für diese Anwendung geändert werden müssen.
- Dank Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen gegen SQL Managed Instance austauschen. Dadurch kann Contoso bei SQL Managed Instance bis zu 30 % der Kosten einsparen.
- Verwaltete SQL-Instanzen sind vollständig in das virtuelle Netzwerk integriert und bieten somit mehr Isolation und Sicherheit für die Daten von Contoso. Contoso kann die Vorteile der öffentlichen Cloud nutzen und gleichzeitig die Umgebung vom öffentlichen Internet isolieren.
- SQL Managed Instance unterstützt zahlreiche Sicherheitsfeatures, darunter Always Encrypted, dynamische Datenmaskierung, Sicherheit auf Zeilenebene und Bedrohungserkennung.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Der Code der Anwendung SmartHotel360 muss für die Migration zu Azure nicht geändert werden. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für SQL Server und Windows Server nutzen. <br><br> Nach der Migration muss Windows Server 2008 R2 nicht unterstützt werden. Weitere Informationen finden Sie in der [Microsoft Lifecycle-Richtlinie](https://aka.ms/lifecycle). <br><br> Contoso kann die Webebene der Anwendung mit mehreren Instanzen konfigurieren, sodass sie kein Single Point of Failure mehr ist. <br><br> Die Datenbank ist nicht mehr auf das veraltete SQL Server 2008 R2 angewiesen. <br><br> Die verwaltete SQL-Instanz unterstützt die technischen Anforderungen und Ziele von Contoso. <br><br> SQL Managed Instance bietet 100 % Kompatibilität mit der aktuellen Bereitstellung und ermöglicht gleichzeitig die Abschaffung von SQL Server 2008 R2. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für sowohl SQL Server als auch Windows Server nutzen. <br><br> Azure Database Migration Service kann für weitere Migrationen in der Zukunft genutzt werden. <br><br> Die verwaltete SQL-Instanz bietet integrierte Fehlertoleranz, die nicht von Contoso konfiguriert werden muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist. |
| **Nachteile** | Azure App Service unterstützt nur eine Anwendungsbereitstellung für jede Web-App. Dies bedeutet, dass zwei Web-Apps bereitgestellt werden müssen (eine für die Website und eine für den WCF-Dienst). <br><br> Für die Datenschicht stellt SQL Managed Instance möglicherweise nicht die beste Lösung dar, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen oder Drittanbieteranwendungen mit SQL Server ausführen möchte. Eine Ausführung von SQL Server auf einer IaaS-VM könnte diese Flexibilität bieten. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Szenarioarchitektur](./media/contoso-migration-refactor-web-app-sql-managed-instance/architecture.png)

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt eine Instanz von Azure SQL Managed Instance bereit und migriert die Datenbank von SmartHotel360 mithilfe von Azure Database Migration Service zu dieser Instanz.
2. Contoso stellt Web-Apps bereit, konfiguriert sie und stellt die Anwendung SmartHotel360 in ihnen bereit.

    ![Migrationsprozess](./media/contoso-migration-refactor-web-app-sql-managed-instance/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration mehrerer Datenbankquellen zu Azure-Datenplattformen mit minimaler Downtime. | Informieren Sie sich über die [unterstützten Regionen](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) und die [Preise für Azure Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Verwaltete Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | SQL Managed Instance ist ein verwalteter Datenbankdienst, der eine vollständig verwaltete SQL Server-Instanz in der Azure-Cloud darstellt. Sie nutzt den gleichen Code wie die neueste Version der Microsoft SQL Server-Datenbank-Engine und verfügt über die neuesten Features, Leistungsverbesserungen und Sicherheitspatches. | Bei der Verwendung einer in Azure ausgeführten Instanz von SQL Managed Instance fallen Gebühren je nach Kapazität an. Informieren Sie sich über die [Preise für SQL Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed). |
| [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Mit Azure App Service können leistungsstarke Cloudanwendungen auf einer vollständig verwalteten Plattform erstellt werden. | Die Kosten basieren auf Größe, Standort und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |
| [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/what-is-azure-pipelines) | Azure Pipelines stellt eine CI/CD-Pipeline (Continuous Integration/Continuous Deployment) für die Anwendungsentwicklung bereit. Die Pipeline beginnt bei einem Git-Repository für die Verwaltung von Anwendungscode, einem Buildsystem zum Erstellen von Paketen und anderen Buildartefakten sowie einem Releaseverwaltungssystem zum Bereitstellen von Änderungen in Entwicklungs-, Test- und Produktionsumgebungen. |

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
> - **Schritt 1: Einrichten einer Instanz von SQL Managed Instance.** Contoso benötigt eine bereits vorhandene verwaltete Instanz, zu der die lokale SQL Server-Datenbank-Instanz migriert wird.
> - **Schritt 2: Migrieren mithilfe von Azure Database Migration Service.** Contoso migriert die Anwendungsdatenbank mithilfe von Azure Database Migration Service.
> - **Schritt 3: Bereitstellen von Web-Apps.** Contoso stellt die beiden Web-Apps bereit.
> - **Schritt 4: Einrichten von Azure DevOps.** Contoso erstellt ein neues Azure DevOps-Projekt und importiert das Git-Repository.
> - **Schritt 5: Konfigurieren von Verbindungszeichenfolgen.** Contoso konfiguriert Verbindungszeichenfolgen, damit die Web-App auf Webebene, die Web-App für den WCF-Dienst und die SQL-Instanz kommunizieren können.
> - **Schritt 6: Einrichten von Build- und Releasepipelines.** Im letzten Schritt richtet Contoso Build- und Releasepipelines zum Erstellen der Anwendung ein und stellt sie in zwei separaten Web-Apps bereit.

## <a name="step-1-set-up-a-sql-managed-instance"></a>Schritt 1: Einrichten einer Instanz von SQL Managed Instance

Contoso benötigt ein Subnetz, das die folgenden Anforderungen erfüllt, um eine Instanz von Azure SQL Managed Instance einzurichten:

- Das Subnetz muss dediziert sein. Es muss leer sein und darf keinen anderen Clouddienst enthalten. Das Subnetz darf kein Gatewaysubnetz sein.
- Nachdem die verwaltete Instanz erstellt wurde, sollte Contoso dem Subnetz keine Ressourcen mehr hinzufügen.
- Dem Subnetz darf keine Netzwerksicherheitsgruppe zugeordnet sein.
- Das Subnetz muss über eine benutzerdefinierte Routingtabelle verfügen. Die einzige zugewiesene Route sollte `0.0.0.0/0` sein (nächster Hop „Internet“).
- Wenn ein optionales benutzerdefiniertes DNS für das virtuelle Netzwerk angegeben wird, muss die virtuelle IP-Adresse `168.63.129.16` für die rekursiven Resolver in Azure zur Liste hinzugefügt werden. Informieren Sie sich über das [Konfigurieren eines benutzerdefinierten DNS für eine Instanz von Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).
- Dem Subnetz darf kein Dienstendpunkt (Speicher oder SQL) zugeordnet sein. Dienstendpunkte sollten im virtuellen Netzwerk deaktiviert sein.
- Das Subnetz muss mindestens 16 IP-Adressen aufweisen. Informieren Sie sich über das [Bestimmen der Größe des Subnetzes für verwaltete Instanzen](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).
- In der Hybridumgebung von Contoso sind benutzerdefinierte DNS-Einstellungen erforderlich. Contoso konfiguriert die DNS-Einstellungen so, dass mindestens ein Azure DNS-Server des Unternehmens genutzt wird. Informieren Sie sich über die [DNS-Anpassung](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Einrichten eines virtuellen Netzwerks für die verwaltete Instanz

Die Contoso-Administratoren richten das virtuelle Netzwerk folgendermaßen ein:

1. Sie erstellen ein neues virtuelles Netzwerk (`VNET-SQLMI-EU2`) in der primären Region (`East US 2`). Sie fügen das virtuelle Netzwerk der Ressourcengruppe `ContosoNetworkingRG` hinzu.
2. Sie weisen den Adressraum `10.235.0.0/24` zu. Es wird sichergestellt, dass der Bereich zu keinerlei Überschneidungen mit anderen Netzwerken im Unternehmen führt.
3. Dem Netzwerk werden zwei Subnetze hinzugefügt:
    - `SQLMI-DS-EUS2` (`10.235.0.0/25`).
    - `SQLMI-SAW-EUS2` (`10.235.0.128/29`). Dieses Subnetz wird verwendet, um ein Verzeichnis an die verwaltete Instanz anzufügen.

      ![Verwaltete Instanz: Erstellen eines virtuellen Netzwerks](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Nach der Bereitstellung des virtuellen Netzwerks und der Subnetze wird das folgende Netzwerkpeering eingerichtet:

    - Peering zwischen `VNET-SQLMI-EUS2` und `VNET-HUB-EUS2` (das virtuelle Hubnetzwerk für `East US 2`)
    - Peering zwischen `VNET-SQLMI-EUS2` und `VNET-PROD-EUS2` (das Produktionsnetzwerk)

      ![Netzwerkpeering](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Es werden benutzerdefinierte DNS-Einstellungen festgelegt. Das DNS verweist zuerst auf den Azure-Domänencontroller von Contoso. Das Azure DNS ist der sekundäre Verweis. Die Azure-Domänencontroller von Contoso befinden sich an den folgenden Orten:

    - Im Subnetz `PROD-DC-EUS2` des Produktionsnetzwerks (`VNET-PROD-EUS2`) in der Region `East US 2`
    - Adresse von `CONTOSODC3`: `10.245.42.4`
    - Adresse von `CONTOSODC4`: `10.245.42.5`
    - Azure DNS-Auflösung: `168.63.129.16`

      ![Netzwerk-DNS-Server](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Benötigen Sie weitere Hilfe?**

- Lesen Sie die [Übersicht zu SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
- Informieren Sie sich über das [Erstellen eines virtuellen Netzwerks für eine Instanz von SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).
- Erfahren Sie, wie Sie das [Peering einrichten](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Erfahren Sie, wie Sie die [DNS-Einstellungen für Azure Active Directory aktualisieren](https://docs.microsoft.com/azure/active-directory-domain-services/tutorial-create-instance).

### <a name="set-up-routing"></a>Einrichten des Routings

Die verwaltete Instanz wird in einem privaten virtuellen Netzwerk angeordnet. Contoso benötigt eine Routingtabelle für das virtuelle Netzwerk, um mit dem Azure-Verwaltungsdienst zu kommunizieren. Wenn das virtuelle Netzwerk nicht mit dem Dienst kommunizieren kann, von dem es verwaltet wird, kann nicht mehr auf das virtuelle Netzwerk zugegriffen werden.

Contoso berücksichtigt die folgenden Faktoren:

- Die Routingtabelle enthält Regeln (Routen), die bestimmen, wie von der verwalteten Instanz gesendete Pakete im virtuellen Netzwerk weitergeleitet werden sollen.
- Die Routingtabelle bezieht sich auf Subnetze, in denen verwaltete Instanzen bereitgestellt werden. Jedes Paket, das ein Subnetz verlässt, wird auf Grundlage der entsprechenden Routingtabelle verarbeitet.
- Ein Subnetz kann nur einer Routingtabelle zugeordnet sein.
- Für die Erstellung von Routingtabellen in Microsoft Azure fallen keine zusätzlichen Gebühren an.

 Die Contoso-Administratoren führen die folgenden Schritte aus, um das Routing einzurichten:

1. Sie erstellen eine benutzerdefinierte Routingtabelle in der Ressourcengruppe `ContosoNetworkingRG`.

    ![Routingtabelle](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Nach dem Bereitstellen der Routingtabelle (`MIRouteTable`) fügen sie eine Route mit dem Adresspräfix `0.0.0.0/0` hinzu, um die Anforderungen von SQL Managed Instance zu erfüllen. Die Option **Typ des nächsten Hops** wird auf **Internet** festgelegt.

    ![Routingtabellenpräfix](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. Sie ordnen die Routingtabelle dem Subnetz `SQLMI-DB-EUS2` (im Netzwerk `VNET-SQLMI-EUS2`) zu.

    ![Routingtabellensubnetz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über das [Einrichten von Routen für eine verwaltete Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

### <a name="create-a-managed-instance"></a>Erstellen einer verwalteten Instanz

Jetzt können die Administratoren von Contoso eine Instanz von SQL Managed Instance bereitstellen:

1. Da die verwaltete Instanz als Geschäftsanwendung dient, stellen sie sie in der primären Region des Unternehmens (`East US 2`) bereit. Sie fügen die verwaltete Instanz der Ressourcengruppe `ContosoRG` hinzu.
2. Für die Instanz wird ein Tarif, eine Computegröße und Speicher ausgewählt. Informieren Sie sich über die [Preise für SQL Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![SQL-Datenbank-Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Nach der Bereitstellung der verwalteten Instanz werden zwei neue Ressourcen in der Ressourcengruppe `ContosoRG` angezeigt:

    - Die neue Instanz von SQL Managed Instance
    - Ein virtueller Cluster, falls Contoso über mehrere verwaltete Instanzen verfügt

      ![SQL-Datenbank-Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über das [Bereitstellen einer verwalteten Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

## <a name="step-2-migrate-via-azure-database-migration-service"></a>Schritt 2: Migrieren mithilfe von Azure Database Migration Service

Die Administratoren von Contoso führen die Migration mithilfe von Azure Database Migration Service durch, indem sie die Schritte im [ausführlichen Migrationstutorial](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) ausführen.

Zusammenfassend müssen Sie die folgenden Schritte ausführen:

- Erstellen Sie eine Azure Database Migration Service-Instanz mit einer `Premium`-SKU, die mit dem VNET verbunden ist.
- Vergewissern Sie sich, dass Azure Database Migration Service über das virtuelle Netzwerk auf den SQL-Remoteserver zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu SQL Server auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem SQL Server gehostet ist, zugelassen werden.
- Konfigurieren Sie Azure Database Migration Service:
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

    ![Web-App](./media/contoso-migration-refactor-web-app-sql-managed-instance/web-app1.png)

2. Die Administratoren geben einen Namen für die Web-App an (`SHWEB-EUS2`), führen sie unter Windows aus und fügen sie der Produktionsressourcengruppe `ContosoRG` hinzu. Es wird eine neue Web-App und ein Azure App Service-Plan erstellt.

    ![Web-App](./media/contoso-migration-refactor-web-app-sql-managed-instance/web-app2.png)

3. Nachdem die Web-App bereitgestellt wurde, wiederholen sie den Prozess, um eine Web-App für den WCF-Dienst (`SHWCF-EUS2`) zu erstellen.

    ![Web-App](./media/contoso-migration-refactor-web-app-sql-managed-instance/web-app3.png)

4. Anschließend navigieren sie zu der Adresse der Anwendungen, um zu überprüfen, ob die Erstellung erfolgreich war.

## <a name="step-4-set-up-azure-devops"></a>Schritt 4: Einrichten von Azure DevOps

Contoso muss die DevOps-Infrastruktur und die Pipelines für die Anwendung erstellen. Hierzu erstellen die Administratoren von Contoso ein neues DevOps-Projekt, importieren ihren Code und richten anschließend die Build- und Releasepipelines ein.

1. Im Azure DevOps-Konto von Contoso erstellen sie ein neues Projekt (`ContosoSmartHotelRefactor`) und wählen **Git** für die Versionskontrolle aus.

    ![Neues Projekt](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts1.png)

2. Sie importieren das Git-Repository, das derzeit ihren Anwendungscode enthält. Der Code befindet sich in einem [öffentlichen GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Registration) und kann heruntergeladen werden.

    ![Herunterladen des App-Codes](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts2.png)

3. Nach dem Importieren des Codes verknüpfen sie Visual Studio mit dem Repository und klonen den Code mithilfe von Team Explorer.

    ![Herstellen einer Verbindung mit dem Projekt](./media/contoso-migration-refactor-web-app-sql-managed-instance/devops1.png)

4. Nachdem das Repository auf dem Entwicklercomputer geklont wurde, öffnen sie die Projektmappendatei für die Anwendung. Die Datei enthält separate Projekte für die Web-App und den WCF-Dienst.

    ![Projektmappendatei](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Schritt 5: Konfigurieren von Verbindungszeichenfolgen

Die Administratoren von Contoso müssen sicherstellen, dass die Web-Apps und die Datenbank kommunizieren können. Zu diesem Zweck konfiguriert das Unternehmen Verbindungszeichenfolgen im Code und in den Web-Apps.

1. In der Web-App für den WCF-Dienst (`SHWCF-EUS2`) fügen sie unter **Einstellungen** > **Anwendungseinstellungen** eine neue Verbindungszeichenfolge mit dem Namen `DefaultConnection` hinzu.
2. Die Verbindungszeichenfolge wird aus der Datenbank `SmartHotel-Registration` gepullt und sollte mit den entsprechenden Anmeldeinformationen aktualisiert werden.

    ![Verbindungszeichenfolge](./media/contoso-migration-refactor-web-app-sql-managed-instance/string1.png)

3. Sie öffnen in Visual Studio das Projekt `SmartHotel.Registration.wcf` in der Projektmappendatei. Der Abschnitt `connectionStrings` der Datei `web.config` für den WCF-Dienst `SmartHotel.Registration.Wcf` sollte mit der Verbindungszeichenfolge aktualisiert werden.

     ![Verbindungszeichenfolge](./media/contoso-migration-refactor-web-app-sql-managed-instance/string2.png)

4. Der Abschnitt `client` der Datei `web.config` für `SmartHotel.Registration.Web` sollte so geändert werden, dass er auf den neuen Speicherort des WCF-Diensts verweist. Dies ist die URL der WCF-Web-App, die den Dienstendpunkt hostet.

    ![Verbindungszeichenfolge](./media/contoso-migration-refactor-web-app-sql-managed-instance/strings3.png)

5. Nachdem die Änderungen im Code vorgenommen wurden, müssen die Administratoren die Änderungen committen. Sie führen Commit und Synchronisierung mithilfe von Team Explorer in Visual Studio durch.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps

Als Nächstes konfigurieren die Contoso-Administratoren Azure DevOps für die Durchführung des Build- und Releasevorgangs.

1. Dazu wählen sie in Azure DevOps **Build und Release** > **Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline1.png)

2. Sie wählen **Azure Repos Git** und das entsprechende Repository aus.

    ![Git und Repository](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline2.png)

3. Unter **Vorlage auswählen** wählen sie die ASP.NET-Vorlage für ihren Build aus.

     ![ASP.NET-Vorlage](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline3.png)

4. Der Name `ContosoSmartHotelRefactor-ASP.NET-CI` wird für den Build verwendet. Wählen Sie **Speichern und in Warteschlange einreihen** aus.

     ![Speichern und in Warteschlange einreihen](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline4.png)

5. Dies startet den ersten Build. Sie wählen die Buildnummer aus, um den Prozess zu überwachen. Nachdem dieser abgeschlossen ist, können sie das Prozessfeedback sehen und auf **Artefakte** klicken, um die Buildergebnisse zu überprüfen.

    ![Überprüfung](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline5.png)

6. Der Ordner **Drop** enthält die Buildergebnisse.

    - Die beiden ZIP-Dateien sind die Pakete, die die Anwendungen enthalten.
    - Diese Dateien werden in der Releasepipeline für die Bereitstellung in Azure App Service verwendet.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline6.png)

7. Sie wählen **Releases** >  **+ Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline7.png)

8. Sie wählen die Bereitstellungsvorlage für Azure App Service aus.

    ![Bereitstellungsvorlage für Azure App Service](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline8.png)

9. Sie geben für die Releasepipeline den Namen `ContosoSmartHotel360Refactor` ein und legen für **Stagename** den Namen der WCF-Web-App (`SHWCF-EUS2`) fest.

    ![Environment](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline9.png)

10. Sie klicken unter den Phasen auf **1 Auftrag, 1 Aufgabe**, um die Bereitstellung des WCF-Diensts zu konfigurieren.

    ![Bereitstellen von WCF](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline10.png)

11. Sie überprüfen, ob das Abonnement ausgewählt und autorisiert ist, und klicken dann auf den **App Service-Namen**.

     ![Auswählen des Namens des App-Diensts](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline11.png)

12. In der Pipeline klicken sie dann unter **Artefakte** auf **+ Artefakt hinzufügen** und wählen für den Buildvorgang die Pipeline `ContosoSmarthotel360Refactor` aus.

     ![Entwickeln](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline12.png)

13. Sie klicken auf das Blitzsymbol des ausgewählten Artefakts, um den Continuous Deployment-Trigger zu aktivieren.

     ![Blitzsymbol](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline13.png)

14. Der Continuous Deployment-Trigger sollte außerdem auf **Aktiviert** festgelegt sein.

    ![Continuous Deployment aktiviert](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline14.png)

15. Jetzt navigieren sie zurück zur Stage **1 Auftrag, 1 Aufgabe** und wählen **Azure App Service bereitstellen** aus.

    ![Bereitstellen von Azure App Service](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline15.png)

16. Sie wählen unter **Datei oder Ordner suchen** die Datei `SmartHotel.Registration.Wcf.zip` aus, die während des Buildvorgangs erstellt wurde, und klicken auf **Speichern**.

    ![Speichern von WCF](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline16.png)

17. Sie wählen **Pipeline** > **Phasen**, **+ Hinzufügen** aus, um eine Umgebung für `SHWEB-EUS2` hinzuzufügen. Sie wählen eine weitere Azure App Service-Bereitstellung aus.

    ![Hinzufügen einer Umgebung](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline17.png)

18. Sie wiederholen den Prozess, um die Datei der Web-App (`SmartHotel.Registration.Web.zip`) in der korrekten Web-App zu veröffentlichen.

    ![Veröffentlichen der Web-App](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline18.png)

19. Nach dem Speichern wird die Releasepipeline wie folgt angezeigt.

     ![Releasepipeline – Zusammenfassung](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline19.png)

20. Sie wechseln zurück zum **Build** und klicken auf **Trigger** > **Continuous Integration aktivieren**. Dies aktiviert die Pipeline. Wenn also Änderungen am Code committet werden, erfolgt ein vollständiger Build mit Release.

    ![Aktivieren von Continuous Integration](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline20.png)

21. Sie klicken auf **Speichern und in Warteschlange einreihen**, um die vollständige Pipeline auszuführen. Es wird ein neuer Build ausgelöst, der wiederum das erste Release der App in Azure App Service erstellt.

    ![Speichern der Pipeline](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline21.png)

22. Die Administratoren von Contoso können die Verarbeitung von Build- und Releasepipeline in Azure DevOps überwachen. Nachdem der Build abgeschlossen wurde, startet die Veröffentlichung.

    ![Erstellen und veröffentlichen der App](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline22.png)

23. Nachdem die Pipeline abgeschlossen wurde, sind beide Websites bereitgestellt, und die Anwendung wird online ausgeführt.

    ![Abschließen der Veröffentlichung](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline23.png)

An dieser Stelle wurde die Anwendung erfolgreich zu Azure migriert.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die folgenden Schritte zur Bereinigung ausführen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Entfernen der VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation mit den neuen Speicherorten für die Anwendung SmartHotel360. Anzeigen, dass die Datenbank in Azure SQL Managed Instance und das Front-End in zwei Web-Apps ausgeführt wird
- Überprüfen sämtlicher Ressourcen, die mit den außer Betrieb genommenen VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neue Datenbank `SmartHotel-Registration` geschützt ist. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Insbesondere sollte Contoso die Web-Apps für die Verwendung von SSL mit Zertifikaten aktualisieren.

### <a name="backups"></a>Backups

- Contoso muss die Sicherungsanforderungen für die SQL Managed Instance-Datenbank überprüfen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Contoso muss sich auch über die Verwaltung von Sicherungen und Wiederherstellungen in SQL-Datenbank informieren. [Erfahren Sie mehr über automatische Sicherungen.](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Contoso sollte die Implementierung von Failovergruppen erwägen, um ein regionales Failover für die Datenbank bereitzustellen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)
- Contoso muss hinsichtlich der Resilienz die Bereitstellung der Web-App in der Hauptregion (`East US 2`) und der sekundären Region (`Central US`) in Erwägung ziehen. Contoso könnte den Traffic Manager konfigurieren, um ein Failover während regionaler Ausfälle sicherzustellen.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über EA verrechnet.
- Contoso verwendet [Azure Cost Management und die Azure-Abrechnung](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von der IT-Leitung festgelegte Budget nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat das Unternehmen Contoso die Anwendung SmartHotel360 in Azure umgestaltet, indem es die Front-End-VM der Anwendung zu zwei Azure App Service-Web-Apps migriert hat. Die Anwendungsdatenbank wurde zu Azure SQL Managed Instance migriert.
