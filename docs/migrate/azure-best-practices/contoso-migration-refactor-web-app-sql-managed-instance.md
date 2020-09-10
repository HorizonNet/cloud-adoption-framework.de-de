---
title: Umgestalten einer lokalen Anwendung zu einer Azure App Service-Web-App und einer verwalteten SQL-Instanz
description: Hier erfahren Sie, wie Contoso einer lokalen Anwendung einen neuen Host zuweist, indem es sie zu einer Azure App Service-Web-App und einer verwalteten SQL-Instanz migriert.
author: givenscj
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 3d95604d9b12a5452853550a655a6c42034d8f23
ms.sourcegitcommit: 78fa714f964225cd5fc7a762e83fafe9b3f9dea1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89427857"
---
<!-- cSpell:ignore contosohost vcenter contosodc smarthotel SQLMI SHWCF SHWEB -->

# <a name="refactor-an-on-premises-application-to-an-azure-app-service-web-app-and-a-sql-managed-instance"></a>Umgestalten einer lokalen Anwendung zu einer Azure App Service-Web-App und einer verwalteten SQL-Instanz

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso als Teil der Migration zu Azure eine zweistufige Windows .NET-Anwendung umgestaltet, die auf virtuellen VMware-Computern (VMs) ausgeführt wird. Das Team von Contoso migriert die Front-End-VM der Anwendung zu einer Azure App Service-Web-App. Außerdem wird in diesem Artikel erläutert, wie Contoso die Anwendungsdatenbank zu einer verwalteten Azure SQL-Instanz migriert.

Die in diesem Beispiel verwendete Anwendung „SmartHotel360“ wird als Open-Source-Anwendung bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam von Contoso hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was sie mit dieser Migration erreichen möchten:

- **Unternehmenswachstum**. Contoso wächst, und damit steigt die Last auf seinen lokalen Systeme und Infrastrukturen.
- **Steigern der Effizienz**. Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigern der Flexibilität**. Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Sie muss schneller reagieren können, als sich die Gegebenheiten des Markts ändern, damit das Unternehmen auf dem globalen Markt Erfolg hat. Ihre Reaktionszeit darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung:** Bei einer Anwendung für Hunderttausende oder Millionen von Mandanten sind Ansätze mit gemeinsamer Datenbanknutzung vorteilhaft, z.B. Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Senken der Kosten:** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat die folgenden Ziele festgelegt, um die beste Migrationsmethode bestimmen zu können:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Anwendung** | Die Anwendung wird in Azure die gleiche zentrale Bedeutung haben wie heute lokal. <br><br> Sie sollte die gleichen Leistungsmerkmale wie aktuell in VMware aufweisen. <br><br> Das Team möchte nicht in die Anwendung investieren. Vorerst werden die Administratoren die Anwendung daher lediglich sicher in die Cloud verschieben. <br><br> Das Team möchte die Unterstützung für Windows Server 2008 R2 einstellen, das Betriebssystem, unter dem die Anwendung derzeit ausgeführt wird. <br><br> Das Team möchte SQL Server 2008 R2 generell nicht mehr verwenden und zu einer modernen Platform-as-a-Service-Datenbankplattform (PaaS) wechseln, die den Verwaltungsaufwand minimiert. <br><br> Seine Investitionen in die SQL Server-Lizenzierung und in die Software Assurance möchte Contoso nutzen, wo immer dies möglich ist. <br><br> Darüber hinaus möchte Contoso die Auswirkungen des Single Point of Failure in der Webebene abschwächen. |
| **Einschränkungen** | Die Anwendung besteht aus einer ASP.NET-Anwendung und einem Windows Communication Foundation-Dienst (WCF), die auf demselben virtuellen Computer ausgeführt werden. Sie möchten diese Komponenten mithilfe von Azure App Service auf zwei Web-Apps verteilen. |
| **Azure** | Contoso möchte die Anwendung zu Azure migrieren, sie soll jedoch nicht auf virtuellen Computern ausgeführt werden. Sowohl in der Web- als auch in der Datenschicht soll auf Azure-PaaS-Dienste zurückgegriffen werden. |
| **DevOps** | Contoso möchte auf ein DevOps-Modell umsteigen und Azure DevOps für Builds und Releasepipelines verwenden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung. Das Unternehmen ermittelt den Migrationsprozess, einschließlich der Azure-Dienste, die für die Migration verwendet werden.

### <a name="current-application"></a>Aktuelle Anwendung

- Die lokale Anwendung „SmartHotel360“ ist auf zwei virtuelle Computer aufgeteilt: `WEBVM` und `SQLVM`.
- Die VMs befinden sich auf dem VMware ESXi-Host „contosohost1.contoso.com“ (Version 6.5).
- Die VMware-Umgebung wird von vCenter Server 6.5 („vcenter.contoso.com“) auf einem virtuellen Computer verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum („contoso-datacenter“) mit einem lokalen Domänencontroller („contosodc1“).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Für die Webebene der Anwendung hat sich Contoso für die Verwendung von Azure App Service entschieden. Über diesen PaaS-Dienst kann die Anwendung mit nur wenigen Konfigurationsänderungen bereitgestellt werden. Contoso verwendet Visual Studio, um die Änderung vorzunehmen, und stellt zwei Web-Apps bereit, eine für die Website und eine für den WCF-Dienst.
- Um die Anforderungen einer DevOps-Pipeline zu erfüllen, verwendet Contoso Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service bereitgestellt.

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Managed Instance durchgeführt. Die folgenden Überlegungen haben dabei zu der Entscheidung für SQL Managed Instance geführt:

- SQL Managed Instance bietet eine Kompatibilität von nahezu 100 % mit der aktuellen lokalen SQL Server-Version. Microsoft empfiehlt SQL Managed Instance für Kunden, die SQL Server lokal oder auf einer Infrastructure-as-a-Service-VM (IaaS) ausführen und ihre Anwendungen mit minimalen Entwurfsänderungen zu einem vollständig verwalteten Dienst migrieren möchten.
- Contoso plant die Migration vieler Anwendungen von der lokalen Ausführung zu IaaS-VMs. Viele dieser virtuellen Computer werden von unabhängigen Softwareanbietern bereitgestellt. Contoso hat erkannt, dass SQL Managed Instance die Datenbankkompatibilität dieser Anwendungen sicherstellt. Daher verwendet das Unternehmen SQL Managed Instance anstelle von SQL-Datenbank, was unter Umständen nicht unterstützt wird.
- Contoso kann mit dem vollständig automatisierten Azure Database Migration Service-Tool ganz einfach eine Lift & Shift-Migration zu SQL Managed Instance durchführen. Außerdem kann Contoso diesen Dienst für spätere Datenbankmigrationen erneut einsetzen.
- SQL Managed Instance unterstützt den SQL Server-Agent, eine wichtige Komponente der Anwendung SmartHotel360. Contoso benötigt diese Kompatibilität, da ansonsten die erforderlichen Wartungspläne für diese Anwendung geändert werden müssen.
- Mit der Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen gegen SQL Managed Instance austauschen. Dadurch kann Contoso bei SQL Managed Instance bis zu 30 Prozent der Kosten einsparen.
- Die verwaltete SQL-Instanz des Unternehmens ist vollständig in das virtuelle Netzwerk integriert und bieten somit mehr Isolation und Sicherheit für die Daten von Contoso. Contoso kann die Vorteile der öffentlichen Cloud nutzen und gleichzeitig die Umgebung vom öffentlichen Internet isolieren.
- SQL Managed Instance unterstützt zahlreiche Sicherheitsfeatures, darunter Always Encrypted, die dynamische Datenmaskierung, die Sicherheit auf Zeilenebene und die Bedrohungserkennung.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet seinen vorgeschlagenen Entwurf aus, indem das Unternehmen eine Liste mit den Vor- und Nachteilen erstellt. Dies ist in der folgenden Tabelle dargestellt:

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Der Code der SmartHotel360-App erfordert für die Migration zu Azure keine Änderungen. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für SQL Server und Windows Server nutzen. <br><br> Nach der Migration muss Windows Server 2008 R2 nicht unterstützt werden. Weitere Informationen finden Sie in der [Microsoft Lifecycle-Richtlinie](https://aka.ms/lifecycle). <br><br> Contoso kann die Webebene der Anwendung mit mehreren Instanzen konfigurieren, sodass sie kein Single Point of Failure mehr ist. <br><br> Die Datenbank ist nicht mehr auf das veraltete SQL Server 2008 R2 angewiesen. <br><br> Die verwaltete SQL-Instanz unterstützt die technischen Anforderungen und Ziele von Contoso. <br><br> SQL Managed Instance bietet eine 100-prozentige Kompatibilität mit der aktuellen Bereitstellung und ermöglicht gleichzeitig die Abschaffung von SQL Server 2008 R2. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für sowohl SQL Server als auch Windows Server nutzen. <br><br> Azure Database Migration Service kann für weitere Migrationen in der Zukunft genutzt werden. <br><br> Die verwaltete Instanz bietet integrierte Fehlertoleranz, die nicht von Contoso konfiguriert werden muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist. |
| **Nachteile** | Azure App Service unterstützt nur eine Anwendungsbereitstellung für jede Web-App. Das bedeutet, dass zwei Web-Apps bereitgestellt werden müssen, eine für die Website und eine für den WCF-Dienst. <br><br> Für die Datenschicht stellt SQL Managed Instance möglicherweise nicht die beste Lösung dar, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen oder Drittanbieteranwendungen mit SQL Server ausführen möchte. Eine Ausführung von SQL Server auf einer IaaS-VM könnte diese Flexibilität bieten. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Diagramm der vorgeschlagenen Architektur](./media/contoso-migration-refactor-web-app-sql-managed-instance/architecture.png)

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt eine verwaltete Azure SQL-Instanz bereit und migriert die Datenbank von „SmartHotel360“ mithilfe von Azure Database Migration Service zu dieser Instanz.
1. Contoso stellt Web-Apps bereit, konfiguriert sie und stellt die Anwendung „SmartHotel360“ für sie bereit.

    ![Diagramm zum Migrationsprozess.](./media/contoso-migration-refactor-web-app-sql-managed-instance/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure App Service-Migrations-Assistent](/learn/paths/migrate-dotnet-apps-azure/) | Eine kostenlose und einfache Möglichkeit, um .NET-Webanwendungen aus der lokalen Umgebung nahtlos und mit minimalen oder sogar ganz ohne Codeänderungen zur Cloud zu migrieren. | Sie können das Tool kostenlos herunterladen. |
| [Azure Database Migration Service](/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration mehrerer Datenbankquellen zu Azure-Datenplattformen mit minimaler Downtime. | Informieren Sie sich über die [unterstützten Regionen](/azure/dms/dms-overview#regional-availability) und die [Preise für Azure Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Verwaltete Azure SQL-Datenbank-Instanz](/azure/sql-database/sql-database-managed-instance) | SQL Managed Instance ist ein verwalteter Datenbankdienst, der eine vollständig verwaltete SQL Server-Instanz in Azure darstellt. Sie nutzt den gleichen Code wie die neueste Version der Microsoft SQL Server-Datenbank-Engine und verfügt über die neuesten Features, Leistungsverbesserungen und Sicherheitspatches. | Bei der Verwendung einer in Azure ausgeführten verwalteten SQL-Instanz fallen Gebühren je nach Kapazität an. Informieren Sie sich über die [Preise für SQL Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed). |
| [Azure App Service](/azure/app-service/overview) | Hilft beim Erstellen leistungsstarker Cloudanwendungen auf einer vollständig verwalteten Plattform. | Die Kosten basieren auf Größe, Standort und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |
| [Azure Pipelines](/azure/devops/pipelines/get-started/what-is-azure-pipelines) | Azure Pipelines stellt eine CI/CD-Pipeline (Continuous Integration/Continuous Deployment) für die Anwendungsentwicklung bereit. Die Pipeline beginnt bei einem Git-Repository für die Verwaltung von Anwendungscode, einem Buildsystem zum Erstellen von Paketen und anderen Buildartefakten sowie einem Releaseverwaltungssystem zum Bereitstellen von Änderungen in Entwicklungs-, Test- und Produktionsumgebungen. |

## <a name="prerequisites"></a>Voraussetzungen

Zum Ausführen dieses Szenarios muss Contoso die folgenden Voraussetzungen erfüllen:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Abonnements wurden in einem früheren Artikel dieser Reihe erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bewerten und Migrieren der Web-Apps**. Contoso verwendet den [Azure App Service-Migrations-Assistenten](https://azure.microsoft.com/migration/web-applications/), um die Kompatibilität vor der Migration zu überprüfen und die Web-Apps zu Azure App Service zu migrieren.
> - **Schritt 2: Einrichten einer verwalteten SQL-Instanz**. Contoso benötigt eine bereits vorhandene verwaltete Instanz, zu der die lokale SQL Server-Datenbank-Instanz migriert wird.
> - **Schritt 3: Migrieren mithilfe von Azure Database Migration Service**. Contoso migriert die Anwendungsdatenbank mithilfe von Azure Database Migration Service.
> - **Schritt 4: Einrichten von Azure DevOps**. Contoso erstellt ein neues Azure DevOps-Projekt und importiert das Git-Repository.
> - **Schritt 5: Konfigurieren von Verbindungszeichenfolgen**. Contoso konfiguriert Verbindungszeichenfolgen, damit die Web-App auf Webebene, die Web-App für den WCF-Dienst und die verwaltete SQL-Instanz kommunizieren können.
> - **Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps**. Im letzten Schritt richtet Contoso Build- und Releasepipelines in Azure DevOps zum Erstellen der Anwendung ein. Das Team stellt die Pipelines anschließend in zwei separaten Web-Apps bereit.

## <a name="step-1-assess-and-migrate-the-web-apps"></a>Schritt 1: Bewerten und Migrieren der Web-Apps

Contoso-Administratoren bewerten und migrieren ihre Web-App mithilfe des [Azure App Service-Migrations-Assistenten](https://azure.microsoft.com/migration/web-applications/). Bei dem Prozess orientieren sie sich am [Microsoft-Lernpfad](/learn/paths/migrate-dotnet-apps-azure/). Die Administratoren führen im Wesentlichen folgende Aktionen aus:

- Sie verwenden die [Azure App Service-Migrationsbewertung](https://appmigration.microsoft.com/assessment/), um alle ggf. vorhandenen Abhängigkeiten zwischen Ihren Web-Apps auszuwerten und um mögliche Inkompatibilitäten zwischen ihren lokalen Web-Apps und der Unterstützung durch Azure App Service zu ermitteln.

- Sie laden den Azure App Service-Migrations-Assistenten herunter und melden sich bei ihrem Azure-Konto an.

- Sie wählen ein Abonnement, eine Ressourcengruppe und den Domänennamen der Website aus.

## <a name="step-2-set-up-a-sql-managed-instance"></a>Schritt 2: Einrichten einer verwalteten SQL-Instanz

Contoso benötigt ein Subnetz, das die folgenden Anforderungen erfüllt, um eine verwaltete Azure SQL-Instanz einzurichten:

- Das Subnetz muss dediziert sein. Es muss leer sein und darf keinen anderen Clouddienst enthalten. Das Subnetz darf kein Gatewaysubnetz sein.
- Nachdem die verwaltete Instanz erstellt wurde, sollte Contoso dem Subnetz keine Ressourcen mehr hinzufügen.
- Dem Subnetz darf keine Netzwerksicherheitsgruppe zugeordnet sein.
- Das Subnetz muss über eine benutzerdefinierte Routingtabelle verfügen. Die einzige zugewiesene Route sollte `0.0.0.0/0` sein (nächster Hop „Internet“).
- Wenn ein optionales benutzerdefiniertes DNS für das virtuelle Netzwerk angegeben wird, muss die virtuelle IP-Adresse `168.63.129.16` für die rekursiven Resolver in Azure zur Liste hinzugefügt werden. Informieren Sie sich über das [Konfigurieren eines benutzerdefinierten DNS für Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-custom-dns).
- Dem Subnetz darf kein Dienstendpunkt (Speicher oder SQL) zugeordnet sein. Dienstendpunkte sollten im virtuellen Netzwerk deaktiviert sein.
- Das Subnetz muss mindestens 16 IP-Adressen aufweisen. Informieren Sie sich über das [Bestimmen der Größe des Subnetzes für verwaltete Instanzen](/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).
- In der Hybridumgebung von Contoso sind benutzerdefinierte DNS-Einstellungen erforderlich. Contoso konfiguriert die DNS-Einstellungen so, dass mindestens ein Azure DNS-Server des Unternehmens genutzt wird. Informieren Sie sich über die [DNS-Anpassung](/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Einrichten eines virtuellen Netzwerks für die verwaltete Instanz

Die Contoso-Administratoren richten das virtuelle Netzwerk folgendermaßen ein:

1. Sie erstellen ein neues virtuelles Netzwerk (VNET-SQLMI-EU2) in der primären Region (USA, Osten 2). Das virtuelle Netzwerk wird der Ressourcengruppe „ContosoNetworkingRG“ hinzugefügt.
1. Sie weisen den Adressraum **10.235.0.0/24** zu. Es wird sichergestellt, dass der Bereich zu keinerlei Überschneidungen mit anderen Netzwerken im Unternehmen führt.
1. Dem Netzwerk werden zwei Subnetze hinzugefügt:
    - `SQLMI-DS-EUS2` (`10.235.0.0/25`).
    - `SQLMI-SAW-EUS2` (`10.235.0.128/29`). Dieses Subnetz wird verwendet, um ein Verzeichnis an die verwaltete Instanz anzufügen.

      ![Screenshot des Bereichs „Virtuelles Netzwerk erstellen“ für die verwaltete Instanz](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

1. Nach der Bereitstellung des virtuellen Netzwerks und der Subnetze wird das folgende Netzwerkpeering eingerichtet:

    - Peering zwischen `VNET-SQLMI-EUS2` und `VNET-HUB-EUS2` (das virtuelle Hubnetzwerk für `East US 2`)  
    - Peering zwischen `VNET-SQLMI-EUS2` und `VNET-PROD-EUS2` (das Produktionsnetzwerk)

      ![Screenshot der Peernetzwerke](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

1. Es werden benutzerdefinierte DNS-Einstellungen festgelegt. Die DNS-Einstellungen verweisen zuerst auf den Azure-Domänencontroller von Contoso. Das Azure DNS ist der sekundäre Verweis. Die Azure-Domänencontroller von Contoso befinden sich an den folgenden Orten:

    - Im Subnetz „PROD-DC-EUS2“ des Produktionsnetzwerks (VNET-PROD-EUS2) in der Region „USA, Osten 2“.  
    - Adresse von `CONTOSODC3`: `10.245.42.4`  
    - Adresse von `CONTOSODC4`: `10.245.42.5`  
    - Azure DNS-Auflösung: `168.63.129.16`

    ![Screenshot der Liste der Netzwerk-DNS-Server](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Benötigen Sie weitere Hilfe?**

- Lesen Sie die [Übersicht zu SQL Managed Instance](/azure/sql-database/sql-database-managed-instance).
- Informieren Sie sich über das [Konfigurieren eines vorhandenen virtuellen Netzwerks für Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).
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

1. Sie erstellen eine benutzerdefinierte Routingtabelle in der Ressourcengruppe „ContosoNetworkingRG“.

    ![Screenshot des Bereichs „Routingtabelle erstellen“](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

1. Um die Anforderungen für SQL Managed Instance zu erfüllen, wird nach dem Bereitstellen der Routingtabelle (MIRouteTable) eine Route mit dem Adresspräfix **0.0.0.0/0** hinzugefügt. Die Option **Typ des nächsten Hops** wird auf **Internet** festgelegt.

    ![Screenshot des Bereichs „Route hinzufügen“ zum Hinzufügen eines Adresspräfixes](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

1. Die Routingtabelle wird dem Subnetz „SQLMI-DB-EUS2“ (im Netzwerk VNET-SQLMI-EUS2) zugeordnet.

    ![Screenshot des Bereichs „Subnetz zuordnen“ für das Routing des Tabellensubnetzes](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über das [Einrichten von Routen für eine verwaltete Instanz](/azure/sql-database/sql-database-managed-instance-get-started).

### <a name="create-a-managed-instance"></a>Erstellen einer verwalteten Instanz

Jetzt können die Administratoren von Contoso eine verwaltete SQL-Instanz bereitstellen:

1. Da die verwaltete Instanz als Geschäftsanwendung dient, stellen die Administratoren sie in der primären Region des Unternehmens (USA, Osten 2) bereit. Die verwaltete Instanz wird zur Ressourcengruppe „ContosoRG“ hinzugefügt.
1. Für die Instanz wird ein Tarif, eine Computegröße und Speicher ausgewählt. Informieren Sie sich über die [Preise für SQL Managed Instance](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Screenshot des Bereichs „Verwaltete SQL-Instanz“](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

    Nach der Bereitstellung der verwalteten Instanz werden zwei neue Ressourcen in der Ressourcengruppe „ContosoRG“ angezeigt:
    - Die neue verwaltete SQL-Instanz  
    - Ein virtueller Cluster, falls Contoso über mehrere verwaltete Instanzen verfügt

      ![Screenshot der neuen Ressource in der Ressourcengruppe „ContosoRG“](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Benötigen Sie weitere Hilfe?**

Informieren Sie sich über das [Bereitstellen einer verwalteten Instanz](/azure/sql-database/sql-database-managed-instance-get-started).

## <a name="step-3-migrate-via-azure-database-migration-service"></a>Schritt 3: Migrieren mithilfe von Azure Database Migration Service

Die Administratoren von Contoso migrieren die verwaltete Instanz mithilfe von Azure Database Migration Service, indem sie die Anweisungen im [ausführlichen Migrationstutorial](/azure/dms/tutorial-sql-server-azure-sql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) ausführen.

Contoso-Administratoren gehen im Wesentlichen wie folgt vor:

- Sie erstellen eine Azure Database Migration Service-Instanz mit einer Premium-SKU, die mit dem virtuellen Netzwerk verbunden ist.
- Sie vergewissern sich, dass Azure Database Migration Service über das virtuelle Netzwerk auf den SQL-Remoteserver zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu SQL Server auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem SQL Server gehostet ist, zugelassen werden.
- Sie konfigurieren Azure Database Migration Service:
  - Erstellen Sie ein Migrationsprojekt.
  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.
  - Wählen Sie ein Ziel aus.
  - Wählen Sie die zu migrierenden Datenbanken aus.
  - Konfigurieren Sie die erweiterten Einstellungen.
  - Starten Sie die Replikation.
  - Beheben Sie alle Fehler.
  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.

## <a name="step-4-set-up-azure-devops"></a>Schritt 4: Einrichten von Azure DevOps

Contoso muss die DevOps-Infrastruktur und die Pipelines für die Anwendung erstellen. Hierzu erstellen die Administratoren von Contoso ein neues DevOps-Projekt, importieren den Code und richten anschließend die Build- und Releasepipelines ein.

1. Im Azure DevOps-Konto von Contoso erstellen sie ein neues Projekt namens „ContosoSmartHotelRefactor“ und wählen anschließend **Git** für die Versionskontrolle aus.

    ![Screenshot des Bereichs „Neues Projekt“](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts1.png)

1. Sie importieren das Git-Repository, das derzeit ihren Anwendungscode enthält. Sie laden es aus dem [öffentlichen GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Registration) herunter.

    ![Screenshot des Bereichs „Git-Repository importieren“ zum Festlegen des Quelltyps und der Klon-URL](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts2.png)

1. Sie stellen eine Verbindung von Visual Studio mit dem Repository her und klonen den Code mithilfe von Team Explorer zum Entwicklercomputer.

    ![Screenshot des Bereichs „Verbindung mit einem Projekt herstellen“](./media/contoso-migration-refactor-web-app-sql-managed-instance/devops1.png)

1. Sie öffnen die Projektmappendatei für die Anwendung. Die Datei enthält separate Projekte für die Web-App und den WCF-Dienst.

    ![Screenshot des Projektmappen-Explorers mit der Auflistung der Web-App- und WCF-Dienstprojekte](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Schritt 5: Konfigurieren von Verbindungszeichenfolgen

Die Administratoren von Contoso müssen sicherstellen, dass die Web-Apps und die Datenbank miteinander kommunizieren können. Zu diesem Zweck konfiguriert das Unternehmen Verbindungszeichenfolgen im Code und in den Web-Apps.

1. In der Web-App für den WCF-Dienst (SHWCF-EUS2) fügt Contoso unter **Einstellungen** > **Anwendungseinstellungen** eine neue Verbindungszeichenfolge mit dem Namen **DefaultConnection** hinzu.
1. Die Verbindungszeichenfolge wird von der Datenbank „SmartHotel-Registration“ abgerufen und mit den entsprechenden Anmeldeinformationen aktualisiert.

    ![Screenshot des Bereichs „Einstellungen für Verbindungszeichenfolgen“](./media/contoso-migration-refactor-web-app-sql-managed-instance/string1.png)

1. Die Administratoren öffnen in Visual Studio das Projekt `SmartHotel.Registration.wcf` in der Projektmappendatei. Im Projekt aktualisieren sie den Abschnitt `connectionStrings` der Datei *web.config* mit der Verbindungszeichenfolge.

     ![Screenshot des Abschnitts „connectionStrings“ der Datei „web.config“ im Projekt „SmartHotel.Registration.wcf“](./media/contoso-migration-refactor-web-app-sql-managed-instance/string2.png)

1. Sie ändern den Abschnitt `client` der Datei `web.config` für „SmartHotel.Registration.Web“ so, dass er auf den neuen Speicherort des WCF-Diensts verweist. Dies ist die URL der WCF-Web-App, die den Dienstendpunkt hostet.

    ![Screenshot des Abschnitts „Client“ der Datei „web.config“ im Projekt „SmartHotel.Registration.wcf“](./media/contoso-migration-refactor-web-app-sql-managed-instance/strings3.png)

1. Wenn die Codeänderungen abgeschlossen sind, committen und synchronisieren die Administratoren sie mithilfe von Team Explorer in Visual Studio.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Schritt 6: Einrichten von Build- und Releasepipelines in Azure DevOps

Als Nächstes konfigurieren die Contoso-Administratoren Azure DevOps für die Durchführung des Build- und Releasevorgangs.

1. Dazu wählen sie in Azure DevOps **Build und Release** > **Neue Pipeline** aus.

    ![Screenshot des Links „Neue Pipeline“ in Azure DevOps](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline1.png)

1. Sie wählen **Azure Repos Git** und das entsprechende Repository aus.

    ![Screenshot der Schaltfläche „Azure Repos Git“ und des ausgewählten Repositorys](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline2.png)

1. Unter **Vorlage auswählen** wählen sie die ASP.NET-Vorlage für ihren Build aus.

     ![Screenshot des Bereichs „Vorlage auswählen“ zum Auswählen der ASP.NET-Vorlage](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline3.png)

1. Sie verwenden den Namen **ContosoSmartHotelRefactor-ASP.NET-CI** für den Build und wählen anschließend **Save & Queue** (Speichern und in die Warteschlange stellen) aus, wodurch der erste Build gestartet wird.

     ![Screenshot der Schaltfläche „Save & Queue“ (Speichern und in die Warteschlange stellen) für den Build](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline4.png)

1. Sie wählen die Buildnummer aus, um den Prozess zu überwachen. Nachdem dieser abgeschlossen ist, können die Administratoren das Prozessfeedback sehen und **Artefakte** auswählen, um die Buildergebnisse zu überprüfen.

    ![Screenshot der Buildseite und des Links „Artefakte“ zum Überprüfen der Buildergebnisse](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline5.png)

    Der Bereich **Artefakte-Explorer** wird geöffnet, und im **Ablageordner** werden die Buildergebnisse angezeigt.

    - Die beiden ZIP-Dateien sind die Pakete, die die Anwendungen enthalten.
    - Diese ZIP-Dateien werden in der Releasepipeline für die Bereitstellung in Azure App Service verwendet.

     ![Screenshot des Bereichs „Artefakte-Explorer“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline6.png)

1. Sie wählen **Releases** >  **+ Neue Pipeline** aus.

    ![Screenshot: Link „Neue Pipeline“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline7.png)

1. Sie wählen die Bereitstellungsvorlage für Azure App Service aus.

    ![Screenshot der Azure App Service-Bereitstellungsvorlage](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline8.png)

1. Sie nennen die Releasepipeline **ContosoSmartHotel360Refactor** und geben im Feld **Phasenname** den Namen **SHWCF-EUS2** als Namen der WCF-Web-App ein.

    ![Screenshot des Phasennamens der WCF-Web-App](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline9.png)

1. Sie klicken unter den Phasen auf **1 Auftrag, 1 Aufgabe**, um die Bereitstellung des WCF-Diensts zu konfigurieren.

    ![Screenshot der Option „1 Auftrag, 1 Aufgabe“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline10.png)

1. Sie überprüfen, ob das Abonnement ausgewählt und autorisiert ist, und wählen anschließend den **App Service-Namen** aus.

     ![Screenshot: Auswählen des App-Dienstnamens](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline11.png)

1. In der Pipeline wählen sie **Artefakte**, anschließend **+ Artefakt hinzufügen** und dann **Build** als Quelltyp aus und erstellen anschließend mit der Pipeline `ContosoSmarthotel360Refactor`.

     ![Screenshot der Schaltfläche „Build“ im Bereich „Artefakt hinzufügen“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline12.png)

1. Die Administratoren wählen das Blitzsymbol des ausgewählten Artefakts aus, um den Continuous Deployment-Trigger zu aktivieren.

     ![Screenshot des Blitzsymbols für das Artefakt](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline13.png)

1. Sie legen den Continuous Deployment-Trigger auf **Aktiviert** fest.

    ![Screenshot des aktivierten Continuous Deployment-Triggers](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline14.png)

1. Die Administratoren navigieren zurück zur Phase **1 Auftrag, 1 Aufgabe** und wählen anschließend **Azure App Service bereitstellen** aus.

    ![Screenshot der Option zum Auswählen von „Azure App Service bereitstellen“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline15.png)

1. Unter **Datei oder Ordner suchen** erweitern sie den **Ablageordner**, wählen die Datei `SmartHotel.Registration.Wcf.zip` aus, die während der Erstellung erstellt wurde, und klicken anschließend auf **Speichern**.

    ![Screenshot des Bereichs „Datei oder Ordner suchen“ zum Auswählen der WCF-Datei](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline16.png)

1. Sie wählen **Pipeline** > **Phasen** und anschließend **+ Hinzufügen** aus, um eine Umgebung für `SHWEB-EUS2` hinzuzufügen. Sie wählen eine weitere Azure App Service-Bereitstellung aus.

    ![Screenshot des Links „1 Auftrag, 1 Aufgabe“ zum Hinzufügen einer Umgebung](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline17.png)

1. Anschließend wiederholen sie den Prozess zum Veröffentlichen der Web-App-Datei (*SmartHotel.Registration.Web.zip*), um die Web-App zu korrigieren, und wählen anschließend **Speichern** aus.

    ![Screenshot des Bereichs „Datei oder Ordner suchen“ zum Auswählen der WEB-Datei](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline18.png)

    Die Releasepipeline wird wie folgt angezeigt:

     ![Screenshot der Zusammenfassung der Releasepipeline](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline19.png)

1. Sie navigieren zurück zu **Build**, wählen **Trigger**aus und aktivieren anschließend das Kontrollkästchen **Continuous Integration aktivieren**. Diese Aktion aktiviert die Pipeline. Wenn also Änderungen am Code committet werden, erfolgt ein vollständiger Build mit Release.

    ![Screenshot mit dem hervorgehobenen Kontrollkästchen „Continuous Integration aktivieren“](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline20.png)

1. Sie klicken auf **Speichern und in Warteschlange einreihen**, um die vollständige Pipeline auszuführen. Ein neuer Build wird ausgelöst, der wiederum das erste Release der App in Azure App Service erstellt.

    ![Screenshot der Schaltfläche „Save & Queue“ (Speichern und in Warteschlange stellen)](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline21.png)

1. Die Administratoren von Contoso können die Verarbeitung von Build- und Releasepipeline in Azure DevOps überwachen. Wenn der Build abgeschlossen wurde, wird das Release gestartet.

    ![Screenshot der Build- und Release-App](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline22.png)

1. Nachdem die Pipeline abgeschlossen wurde, sind beide Websites bereitgestellt, und die Anwendung wird online ausgeführt.

    ![Screenshot: Anwendung wird ausgeführt](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline23.png)

    Die Anwendung wurde erfolgreich zu Azure migriert.

## <a name="clean-up-after-the-migration"></a>Bereinigung nach der Migration

Nach der Migration führt das Contoso-Team die folgenden Bereinigungsschritte durch:

- Das Unternehmen entfernt die lokalen VMs aus dem vCenter-Bestand.
- Es entfernt die virtuellen Computer aus den lokalen Sicherungsaufträgen.
- Es aktualisiert die interne Dokumentation, um die neuen Speicherorte für die Anwendung „SmartHotel360“ anzuzeigen. Die Dokumentation zeigt an, dass die Datenbank in der verwalteten SQL-Instanz und das Front-End in zwei Web-Apps ausgeführt wird.
- Es überprüft sämtliche Ressourcen, die mit den außer Betrieb genommenen virtuellen Computern interagieren, und aktualisiert alle relevanten Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Nachdem die Ressourcen nun zu Azure migriert wurden, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neue Datenbank `SmartHotel-Registration` geschützt ist. [Weitere Informationen](/azure/sql-database/sql-database-security-overview)
- Insbesondere muss Contoso die Web-Apps für die Verwendung von SSL mit Zertifikaten aktualisieren.

### <a name="backups"></a>Backups

- Das Contoso-Team muss die Sicherungsanforderungen für die Datenbank in Azure SQL Managed Instance überprüfen. [Weitere Informationen](/azure/sql-database/sql-database-automated-backups)
- Es muss sich auch über die Verwaltung von Sicherungen und Wiederherstellungen in SQL-Datenbank informieren. [Erfahren Sie mehr über automatische Sicherungen.](/azure/sql-database/sql-database-automated-backups)
- Das Unternehmen muss die Implementierung von Failovergruppen berücksichtigen, um ein regionales Failover für die Datenbank bereitzustellen. [Weitere Informationen](/azure/sql-database/sql-database-geo-replication-overview)
- Es muss hinsichtlich der Resilienz die Bereitstellung der Web-App in der Hauptregion (`East US 2`) und der sekundären Region (`Central US`) in Erwägung ziehen. Das Team könnte den Traffic Manager konfigurieren, um ein Failover während regionaler Ausfälle sicherzustellen.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, weist Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zu.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Diese Kosten werden über das Enterprise Agreement verrechnet.
- Contoso verwendet die [Azure-Kostenverwaltung und -Abrechnung](/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat das Unternehmen Contoso die Anwendung SmartHotel360 in Azure umgestaltet, indem es die Front-End-VM der Anwendung zu zwei Azure App Service-Web-Apps migriert hat. Die Anwendungsdatenbank wurde zu einer verwalteten Azure SQL-Instanz migriert.
