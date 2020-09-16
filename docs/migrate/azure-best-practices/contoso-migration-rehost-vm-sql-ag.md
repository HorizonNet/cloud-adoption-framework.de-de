---
title: Zuweisen eines neuen Hosts zu einer Anwendung durch Migration zu Azure-VMs und SQL Server Always On-Verfügbarkeitsgruppen
description: Dieser Artikel enthält Informationen darüber, wie Contoso einer lokalen App einen neuen Host zuweist, indem diese zu Azure-VMs und zur SQL Server Always On-Verfügbarkeitsgruppe migriert wird.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c633fe36e4817ad92501085b8309acf945397bc3
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602559"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc AOAG SQLAOG SQLAOGAVSET contosoadmin contosocloudwitness MSSQLSERVER BEPOOL contosovmsacc SHAOG NSGs inetpub iisreset -->

# <a name="rehost-an-on-premises-application-with-azure-vms-and-sql-server-always-on-availability-groups"></a>Zuweisen eines neuen Hosts zu einer lokale Anwendung mit Azure-VMs und SQL Server Always On-Verfügbarkeitsgruppen

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso einer zweistufigen Windows .NET-Anwendung, die auf virtuellen VMware-Computern (VMs) ausgeführt wird, als Teil einer Migration zu Azure einen neuen Host zuweist. Contoso migriert die Front-End-VM der Anwendung zu einer Azure-VM und die Anwendungsdatenbank zu einer Azure SQL Server-VM, die in einem Windows Server-Failovercluster mit SQL Server Always On-Verfügbarkeitsgruppen ausgeführt werden.

Die in diesem Beispiel verwendete SmartHotel360-Anwendung wird als Open Source bereitgestellt. Wenn Sie diese Anwendung für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte. Sie wünschen Folgendes:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und die Infrastruktur unter Druck.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, um Kundenanforderungen schneller zu bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. IT darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit derselben Geschwindigkeit mitwachsen.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt:

- Nach der Migration soll die Anwendung in Azure die gleichen Leistungsmerkmale aufweisen wie gegenwärtig in der lokalen VMware-Umgebung. Die Anwendung ist in der Cloud ebenso wichtig wie lokal.
- Contoso möchte nicht in diese Anwendung investieren. Die Investition ist wichtig für das Geschäft, aber in ihrer derzeitigen Form soll die Anwendung lediglich sicher in die Cloud verschoben werden.
- Bei der lokalen Anwendungsdatenbank gab es Verfügbarkeitsprobleme. Contoso möchte sie in Azure als Hochverfügbarkeitscluster mit Failoverfunktionen bereitstellen.
- Contoso möchte ein Upgrade von seiner aktuellen SQL Server 2008 R2-Plattform auf SQL Server 2017 durchführen.
- Contoso möchte für diese Anwendung keine Azure SQL-Datenbank verwenden und sucht nach Alternativen.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen des Unternehmens formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess. Die Azure-Dienste, die für die Migration verwendet werden sollen, werden ebenfalls identifiziert.

### <a name="current-architecture"></a>Aktuelle Architektur

- Die Anwendung ist auf zwei VMs aufgeteilt (`WEBVM` und `SQLVM`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird mit der Anwendung vCenter Server 6.5 (`vcenter.contoso.com`) verwaltet, die auf einer VM ausgeführt wird.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Szenario:

- Contoso migriert das Anwendungs-Front-End `WEBVM` zu einer Azure IaaS-VM (Infrastructure-as-a-Service).
  - Die Front-End-VM in Azure wird in der Ressourcengruppe `ContosoRG` bereitgestellt (wird für Produktionsressourcen verwendet).
  - Sie wird sich im Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) befinden.
- Die Anwendungsdatenbank wird zu einer Azure SQL Server-VM migriert.
  - Sie wird sich im Azure-Datenbanknetzwerk von Contoso (`PROD-DB-EUS2`) in der primären Region (`East US 2`) befinden.
  - Sie wird in einem Windows Server-Failovercluster mit zwei Knoten platziert, für den SQL Server Always On-Verfügbarkeitsgruppen verwendet werden.
  - In Azure werden die beiden SQL Server-VM-Knoten im Cluster in der Ressourcengruppe `ContosoRG` bereitgestellt.
  - Die VM-Knoten werden sich im Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) befinden.
  - Auf VMs wird Windows Server 2016 mit der SQL Server 2017 Enterprise Edition ausgeführt. Contoso verfügt über keine Lizenzen für dieses Betriebssystem. Das Unternehmen nutzt ein Image von Azure Marketplace, bei dem die Lizenz über eine Gebühr im Rahmen der Azure Enterprise Agreement-Verpflichtung des Unternehmens bereitgestellt wird.
  - Abgesehen von eindeutigen Namen verwenden beide VMs die gleichen Einstellungen.
- Contoso stellt einen internen Lastenausgleich bereit, der den Cluster hinsichtlich des Datenverkehrs überwacht und diesen an den entsprechenden Clusterknoten weiterleitet.
  - Der interne Lastenausgleich wird in `ContosoNetworkingRG` bereitgestellt (wird für Netzwerkressourcen verwendet).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

    ![Screenshot: Diagramm mit der Szenarioarchitektur](./media/contoso-migration-rehost-vm-sql-ag/architecture.png)

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Server durchgeführt. Hierbei haben die folgenden Überlegungen dem Unternehmen dabei geholfen, sich für eine Azure-IaaS-VM zu entscheiden, auf der SQL Server ausgeführt wird:

- Der Einsatz einer Azure-VM mit SQL Server erscheint als optimale Lösung, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen muss, oder wenn Drittanbieteranwendungen auf derselben VM installiert und ausgeführt werden sollen.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | `WEBVM` wird ohne Änderungen in Azure verlagert. Die Migration ist also sehr einfach. <br><br> Die SQL Server-Schicht wird auf SQL Server 2017 und Windows Server 2016 ausgeführt. Somit wird das aktuelle Betriebssystem Windows Server 2008 R2 außer Betrieb genommen. Mit der Ausführung von SQL Server 2017 werden die technischen Anforderungen und Ziele von Contoso unterstützt. IT bietet 100-prozentige Kompatibilität, während SQL Server 2008 R2 ausgemustert wird. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil nutzen. <br><br> Eine SQL Server-Bereitstellung mit hoher Verfügbarkeit in Azure verfügt über Fehlertoleranz, sodass die Anwendungsdatenschicht kein Single Point of Failover mehr ist. |
| **Nachteile** | Auf `WEBVM` wird Windows Server 2008 R2 ausgeführt. Das Betriebssystem wird für bestimmte Rollen von Azure unterstützt (Juli 2018). Weitere Informationen finden Sie unter [Microsoft-Server-Software-Support für virtuelle Maschinen von Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines). <br><br> Die Webschicht der Anwendung bleibt ein Single Point of Failover. <br><br> Contoso muss die Webschicht weiterhin als Azure-VM unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service umzustellen. <br><br> Mit der gewählten Lösung muss Contoso weiterhin zwei virtuelle SQL Server-Computer verwalten, anstatt auf eine verwaltete Plattform, z. B. Azure SQL Managed Instance, umzustellen. Zudem hat Contoso mit Software Assurance die Möglichkeit, seine vorhandenen Lizenzen gegen reduzierte Tarife von Azure SQL Managed Instance einzutauschen. |

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Azure Database Migration Service](/azure/dms/dms-overview) | Azure Database Migration Service ermöglicht die nahtlose Migration mehrerer Datenbankquellen zu Azure-Datenplattformen mit minimaler Downtime. | Informieren Sie sich über die [unterstützten Regionen](/azure/dms/dms-overview#regional-availability) und die [Preise für Azure Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration). |
| [Azure Migrate](/azure/migrate/migrate-overview) | Contoso verwendet Azure Migrate, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | Azure Migrate ist ohne Aufpreis erhältlich. Je nach den Tools (Originalanbieter oder ISV), die für die Bewertung und Migration verwendet werden, können aber ggf. Gebühren anfallen. Weitere Informationen zu den Preisen von Azure Migrate finden Sie [hier](https://azure.microsoft.com/pricing/details/azure-migrate). |

## <a name="migration-process"></a>Migrationsprozess

Die Contoso-Administratoren migrieren die Anwendungs-VMs zu Azure.

- Sie migrieren die Front-End-VM mithilfe von Azure Migrate zur Azure-VM:
  - Im ersten Schritt bereitet das Unternehmen Azure-Komponenten vor und richtet diese ein, und es bereitet die lokale VMware-Infrastruktur vor.
  - Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der VM beginnen.
  - Nachdem die Replikation aktiviert wurde und funktioniert, migriert das Unternehmen die VM mithilfe von Azure Migrate.
- Nachdem die Datenbank überprüft wurde, wird sie mithilfe von Azure Database Migration Service zu einem SQL Server-Cluster in Azure migriert.
  - Im ersten Schritt müssen SQL Server-VMs in Azure bereitgestellt, der Cluster und ein interner Lastenausgleich eingerichtet und Always On-Verfügbarkeitsgruppen konfiguriert werden.
  - Anschließend kann die Datenbank migriert werden
- Nach der Migration werden Always On-Verfügbarkeitsgruppen für die Datenbank aktiviert.

    ![Screenshot: Diagramm mit dem Migrationsprozess](./media/contoso-migration-rehost-vm-sql-ag/migration-process.png)

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes.

| Anforderungen | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat bereits in einem früheren Artikel dieser Reihe ein Abonnement erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden, aber nicht der Administrator sind, sollten Sie den Administrator bitten, Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuzuweisen. <br><br> |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Contoso – Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) beschrieben. <br><br> Hier erfahren Sie mehr über bestimmte [Voraussetzungen](./contoso-migration-devtest-to-iaas.md#prerequisites) für Azure Migrate: Servermigration. |
| **Lokale Server** | Auf der lokalen vCenter Server-Instanz sollte Version 5.5, 6.0, 6.5 oder 6.7 ausgeführt werden. <br><br> Ein ESXi-Host mit Version 5.5, 6.0, 6.5 oder 6.7. <br><br> Mindestens eine VMware-VM auf dem ESXi-Host. |
| **Lokale VMs** | [Überprüfen Sie Linux-Computer](/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten eines Clusters für SQL Server Always On-Verfügbarkeitsgruppen.** Erstellen Sie einen Cluster für die Bereitstellung von zwei virtuellen SQL Server-Knoten in Azure.
> - **Schritt 2: Bereitstellen und Einrichten des Clusters.** Bereiten Sie einen Azure SQL Server-Cluster vor. Datenbanken werden in diesen vorhandenen Cluster migriert.
> - **Schritt 3: Bereitstellen von Azure Load Balancer.** Stellen Sie einen Lastenausgleich für den Datenverkehr zu den SQL Server-Knoten bereit.
> - **Schritt 4: Vorbereiten von Azure für Azure Migrate.** Erstellen Sie ein Azure Storage-Konto für die Speicherung replizierter Daten.
> - **Schritt 5: Vorbereiten der lokalen VMware-Instanz für Azure Migrate.** Bereiten Sie Konten für die VM-Ermittlung und die Agent-Installation vor. Vorbereiten lokaler virtueller Computer, damit Benutzer nach der Migration eine Verbindung mit virtuellen Azure-Computern herstellen können.
> - **Schritt 6: Replizieren der lokalen VMs in Azure.** Ermöglichen Sie die VM-Replikation in Azure.
> - **Schritt 7: Migrieren der Datenbank mithilfe von Azure Database Migration Service.** Migrieren Sie die Datenbank mithilfe von Azure Database Migration Service zu Azure.
> - **Schritt 8: Schützen der Datenbank mit SQL Server Always On.** Erstellen Sie eine Always On-Verfügbarkeitsgruppe für den Cluster.
> - **Schritt 9: Migrieren der VM mit Azure Migrate.** Führen Sie eine Testmigration aus, um sicherzustellen, dass alles wie erwartet funktioniert. Führen Sie dann eine Migration zu Azure aus.

## <a name="step-1-prepare-a-sql-server-always-on-availability-group-cluster"></a>Schritt 1: Vorbereiten eines Clusters für SQL Server Always On-Verfügbarkeitsgruppen

Die Contoso-Administratoren führen Folgendes durch, um den Cluster einzurichten:

1. Sie erstellen zwei SQL Server-VMs, indem sie im Azure Marketplace das Image „SQL Server 2017 Enterprise Windows Server 2016“ auswählen.

    ![Screenshot: SQL-VM-SKU](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-sku.png)

1. Unter **Assistent zum Erstellen virtueller Maschinen** > **Grundlagen** konfigurieren sie Folgendes:

    - Namen für die VMs: `SQLAOG1` und `SQLAOG2`.
    - Da Computer unternehmenskritisch sind, wird als VM-Datenträgertyp „SSD“ aktiviert.
    - Die Anmeldeinformationen für Computer werden angegeben.
    - Sie stellen die VMs der primären Region (`East US 2`) in der Ressourcengruppe `ContosoRG` bereit.

1. Unter **Größe** beginnt das Unternehmen mit `D2S v3`-Instanzen für beide VMs. Die Skalierung wird später nach Bedarf durchgeführt.
1. Sie führen unter **Einstellungen** die folgenden Aktionen durch:

    - Da es sich bei diesen VMs um wichtige Datenbanken für die Anwendung handelt, werden verwaltete Datenträger verwendet.
    - Das Unternehmen platziert die Computer im Datenbanksubnetz (`PROD-DB-EUS2`) des Produktionsnetzwerks (`VNET-PROD-EUS2`) in der primären Region (`East US 2`).
    - Es erstellt eine neue Verfügbarkeitsgruppe (`SQLAOGAVSET`) mit zwei Fehlerdomänen und fünf Updatedomänen.

      ![Screenshot: Neue Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-settings.png)

1. Contoso begrenzt über die **SQL Server-Einstellungen** die SQL-Konnektivität mit dem virtuellen Netzwerk (privat) am Standardport 1433. Für die Authentifizierung werden die gleichen Anmeldeinformationen wie vor Ort (`contosoadmin`) verwendet.

    ![Screenshot: SQL Server-Einstellungen](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-db.png)

**Benötigen Sie weitere Hilfe?**

- Hilfe zum [Bereitstellen einer SQL Server-VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#1-configure-basic-settings)
- Informationen zum [Konfigurieren von VMs für verschiedene SQL Server-SKUs](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-prereq#create-sql-server-vms)

## <a name="step-2-deploy-and-set-up-the-cluster"></a>Schritt 2: Bereitstellen und Einrichten des Clusters

Die Contoso-Administratoren führen Folgendes durch, um den Cluster einzurichten:

1. Sie richten ein Azure Storage-Konto ein, das als Cloudzeuge fungiert.
1. Sie fügen die SQL Server-VMs der Active Directory-Domäne im lokalen Contoso-Rechenzentrum hinzu.
1. Sie erstellen den Cluster in Azure.
1. Sie konfigurieren den Cloudzeugen.
1. Sie aktivieren die SQL-Always On-Verfügbarkeitsgruppen.

### <a name="set-up-a-storage-account-as-a-cloud-witness"></a>Sie richten ein Speicherkonto als Cloudzeuge ein.

Für die Einrichtung eines Cloudzeugen benötigt Contoso ein Azure-Speicherkonto, das die Blob-Datei für die Clustervermittlung enthält. Dasselbe Speicherkonto kann für die Einrichtung eines Cloudzeugen für mehrere Cluster verwendet werden.

Die Contoso-Administratoren führen Folgendes durch, um ein Speicherkonto zu erstellen:

1. Sie geben einen erkennbaren Namen für das Konto an (`contosocloudwitness`).
1. Sie stellen ein Allzweckkonto mit LRS bereit.
1. Sie platzieren das Konto in einer Drittregion (`South Central US`). Es platziert das Konto außerhalb der primären und sekundären Region, damit es während eines regionalen Ausfalls verfügbar bleibt.
1. Sie platzieren das Konto in der Ressourcengruppe mit den Infrastrukturressourcen (`ContosoInfraRG`).

    ![Screenshot: Kontoname für Cloudzeugen](./media/contoso-migration-rehost-vm-sql-ag/witness-storage.png)

1. Wenn das Unternehmen das Speicherkonto erstellt, werden für dieses Konto primäre und sekundäre Zugriffsschlüssel generiert. Der primäre Zugriffsschlüssel wird für die Erstellung des Cloudzeugen benötigt. Der Schlüssel wird unter dem Namen des Speicherkontos > **Zugriffstasten** angezeigt.

    ![Screenshot: Zugriffsschlüssel](./media/contoso-migration-rehost-vm-sql-ag/access-key.png)

<!-- docsTest:casing "Failover Cluster feature" -->

### <a name="add-sql-server-vms-to-contoso-domain"></a>Hinzufügen von SQL Server-VMs zur Contoso-Domäne

1. Contoso fügt `SQLAOG1` und `SQLAOG2` zur Domäne `contoso.com` hinzu.
1. Auf jeder VM installieren die Administratoren das Feature und die Tools des Windows-Failoverclusters.

### <a name="set-up-the-cluster"></a>Einrichten des Clusters

Vor dem Einrichten des Clusters erstellen die Contoso-Administratoren auf jedem Computer eine Momentaufnahme des Betriebssystemdatenträgers.

![Screenshot: Bereich „Momentaufnahme erstellen“](./media/contoso-migration-rehost-vm-sql-ag/snapshot.png)

1. Sie führen ein Skript aus, um den Windows-Failovercluster zu erstellen.

    ![Screenshot: Skript zum Erstellen des Windows-Failoverclusters](./media/contoso-migration-rehost-vm-sql-ag/create-cluster1.png)

1. Nach der Erstellung des Clusters wird überprüft, ob die VMs als Clusterknoten angezeigt werden.

     ![Screenshot: Anzeige der erstellten Cluster](./media/contoso-migration-rehost-vm-sql-ag/create-cluster2.png)

<!--docsTest:casing "Failover Cluster Manager" -->

### <a name="configure-the-cloud-witness"></a>Konfigurieren des Cloudzeugen

1. Die Contoso-Administratoren konfigurieren den Cloudzeugen mit dem **Assistenten für die Quorumkonfiguration** im Failovercluster-Manager.
1. Im Assistenten erstellt das Unternehmen einen Cloudzeugen mit dem Speicherkonto.
1. Nach der Konfiguration des Cloudzeugen wird dieser im Failovercluster-Manager-Snap-In angezeigt.

    ![Screenshot: Anzeige der Konfiguration des Cloudzeugen](./media/contoso-migration-rehost-vm-sql-ag/cloud-witness.png)

### <a name="enable-sql-server-always-on-availability-groups"></a>Aktivieren von SQL Server Always On-Verfügbarkeitsgruppen

Die Contoso-Administratoren können jetzt Always On-Verfügbarkeitsgruppen aktivieren:

1. Das Unternehmen aktiviert im SQL Server-Konfigurations-Manager die **Always On-Verfügbarkeitsgruppen** für den Dienst **SQL Server (MSSQLSERVER)** .

    ![Screenshot: Kontrollkästchen zum Aktivieren von Always On-Verfügbarkeitsgruppen](./media/contoso-migration-rehost-vm-sql-ag/enable-always-on.png)

1. Das Unternehmen startet den Dienst neu, damit die Änderungen wirksam werden.

Nach der Aktivierung von Always On-Verfügbarkeitsgruppen kann Contoso die Always On-Verfügbarkeitsgruppe für den Schutz der SmartHotel360-Datenbank einrichten.

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über [Cloudzeugen und die Einrichtung eines zugehörigen Speicherkontos](/windows-server/failover-clustering/deploy-cloud-witness).
- Lesen Sie die Anleitung zum [Einrichten eines Clusters und zum Erstellen einer Verfügbarkeitsgruppe](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial).

## <a name="step-3-deploy-azure-load-balancer"></a>Schritt 3: Bereitstellen von Azure Load Balancer

Die Contoso-Administratoren möchten nun ein internes Lastenausgleichsmodul bereitstellen, das sich vor den Clusterknoten befindet. Das Lastenausgleichsmodul ist für Datenverkehr empfangsbereit und leitet diesen an den entsprechenden Knoten weiter.

![Diagramm: Lastenausgleich](./media/contoso-migration-rehost-vm-sql-ag/architecture-lb.png)

Zum Erstellen des Lastenausgleichs führen die Contoso-Administratoren Folgendes durch:

1. Sie navigieren im Azure-Portal zu **Netzwerk** > **Lastenausgleich** und richten einen neuen internen Lastenausgleich ein: `ILB-PROD-DB-EUS2-SQLAOG`.
1. Sie platzieren den Lastenausgleich im Datenbanksubnetz (`PROD-DB-EUS2`) des Produktionsnetzwerks (`VNET-PROD-EUS2`).
1. Sie weisen eine statische IP-Adresse (`10.245.40.100`) zu.
1. Der Lastenausgleich wird als Netzwerkelement in der Netzwerkressourcengruppe `ContosoNetworkingRG` bereitgestellt.

    ![Screenshot: Bereich „Lastenausgleich erstellen“](./media/contoso-migration-rehost-vm-sql-ag/lb-create.png)

Nach der Bereitstellung des internen Lastenausgleichs müssen die Contoso-Administratoren die Einrichtung dafür durchführen. Das Unternehmen erstellt einen Back-End-Adresspool, richtet einen Integritätstest ein und konfiguriert eine Regel für den Lastenausgleich.

### <a name="add-a-back-end-pool"></a>Hinzufügen eines Back-End-Pools

Zum Verteilen von Datenverkehr auf die virtuellen Computer im Cluster richten die Contoso-Administratoren einen Back-End-Adresspool ein, in dem die IP-Adressen der NICs für virtuelle Computer enthalten sind, die den Netzwerkdatenverkehr über den Lastenausgleich empfangen.

1. Contoso fügt im Portal in den Einstellungen für den Lastenausgleich einen Back-End-Pool hinzu: `ILB-PROD-DB-EUS-SQLAOG-BEPOOL`.
1. Die Administratoren ordnen dem Pool die Verfügbarkeitsgruppe `SQLAOGAVSET` zu. Die VMs in der Gruppe (`SQLAOG1` und `SQLAOG2`) werden zum Pool hinzugefügt.

    ![Screenshot: Bildschirm „Back-End-Pool hinzufügen“](./media/contoso-migration-rehost-vm-sql-ag/backend-pool.png)

### <a name="create-a-health-probe"></a>Erstellen eines Integritätstests

Die Contoso-Administratoren erstellen einen Integritätstest, damit der Lastenausgleich den Status der Anwendung überwachen kann. Je nach der Reaktion auf die Integritätsprüfungen fügt der Integritätstest VMs dynamisch der Lastenausgleichsrotation hinzu bzw. entfernt sie daraus.

Die Contoso-Administratoren führen Folgendes durch, um den Test zu erstellen:

1. Sie erstellen im Portal in den Einstellungen für den Lastenausgleich einen Integritätstest: **SQLAlwaysOnEndPointProbe**.
1. Sie legen fest, dass bei dem Test VMs an TCP-Port 59999 überwacht werden sollen.
1. Sie legen ein Intervall von 5 Sekunden zwischen den Tests und einen Schwellenwert von 2 fest. Wenn zwei Tests fehlschlagen, gilt eine VM als fehlerhaft.

    ![Screenshot: Bildschirm „Integritätstest hinzufügen“](./media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

### <a name="configure-the-load-balancer-to-receive-traffic"></a>Konfigurieren des Lastenausgleichs für den Empfang von Datenverkehr

Die Contoso-Administratoren richten nun eine Regel für den Lastenausgleich ein, um zu definieren, wie Datenverkehr auf die virtuellen Computer verteilt wird.

- Die Front-End-IP-Adresse verarbeitet eingehenden Datenverkehr.
- Der Back-End-IP-Pool empfängt den Datenverkehr.

Die Contoso-Administratoren führen Folgendes durch, um die Regel zu erstellen:

1. Im Portal wird in den Einstellungen für den Lastenausgleich eine neue Regel hinzugefügt: `SQLAlwaysOnEndPointListener`.
1. Sie legen für den Empfang von eingehendem Datenverkehr des SQL-Clients an TCP-Port 1433 einen Front-End-Listener fest.
1. Sie geben den Back-End-Pool an, an den Datenverkehr weitergeleitet werden soll, sowie den Port, an dem die VMs für den Datenverkehr empfangsbereit sind.
1. Sie aktivieren das Feature „Floating IP“ (Direct Server Return), das für SQL Server Always On immer erforderlich ist.

    ![Screenshot: Einstellungen für Integritätstests](./media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

**Benötigen Sie weitere Hilfe?**

- Verschaffen Sie sich einen Überblick über [Azure Load Balancer](/azure/load-balancer/load-balancer-overview).
- Informieren Sie sich über das [Erstellen eines Lastenausgleichs](/azure/load-balancer/tutorial-load-balancer-basic-internal-portal).

## <a name="step-4-prepare-azure-for-azure-migrate"></a>Schritt 4: Vorbereiten von Azure für Azure Migrate

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Bereitstellung von Azure Migrate benötigt:

- Ein virtuelles Netzwerk, in dem sich VMs befinden, wenn sie migriert werden.
- Ein Azure Storage-Konto für die Speicherung replizierter Daten.

Die Contoso-Administratoren richten die folgenden Komponenten ein:

1. Contoso hat bereits ein Netzwerk/Subnetz erstellt, das für Azure Migrate verwendet werden kann, wenn das Unternehmen die [Azure-Infrastruktur bereitgestellt](./contoso-migration-rehost-vm-sql-ag.md) hat.

    - Bei der SmartHotel360-Anwendung handelt es sich um eine Produktionsanwendung, und `WEBVM` wird zum Azure-Produktionsnetzwerk (`VNET-PROD-EUS2`) in der primären Region (`East US 2`) migriert.
    - `WEBVM` wird in der Ressourcengruppe `ContosoRG`, die für Produktionsressourcen verwendet wird, und im Produktionssubnetz (`PROD-FE-EUS2`) platziert.

1. Die Contoso-Administratoren erstellen ein Azure Storage-Konto (`contosovmsacc20180528`) in der primären Region.

    - Das Unternehmen verwendet ein universelles Konto mit Standardspeicher und LRS-Replikation.

## <a name="step-5-prepare-on-premises-vmware-for-azure-migrate"></a>Schritt 5: Vorbereiten der lokalen VMware-Instanz für Azure Migrate

Die Contoso-Administratoren bereiten lokal Folgendes vor:

- Ein Konto auf dem vCenter-Server oder dem vSphere ESXi-Host zum Automatisieren der VM-Ermittlung.
- Lokale VM-Einstellungen, damit Contoso nach der Migration eine Verbindung mit der replizierten Azure-VM herstellen kann.

### <a name="prepare-an-account-for-automatic-discovery"></a>Vorbereiten eines Kontos für die automatische Ermittlung

Azure Migrate benötigt Zugriff auf VMware-Server, um folgende Aufgaben durchzuführen:

- Automatisches Ermitteln von VMs.
- Orchestrieren von Replikation und Migration.
- Dafür ist mindestens ein Konto mit Lesezugriff erforderlich. Sie benötigen ein Konto, das berechtigt ist, Vorgänge wie das Erstellen und Entfernen von Datenträgern sowie das Einschalten virtueller Computer durchzuführen.

Zum Einrichten des Kontos müssen die Contoso-Administratoren Folgendes durchführen:

1. Erstellen einer Rolle auf der vCenter-Ebene
1. Zuweisen der erforderlichen Berechtigungen für die Rolle

### <a name="prepare-to-connect-to-azure-vms-after-migration"></a>Vorbereiten der Verbindungsherstellung mit Azure-VMs nach der Migration

Nach der Migration möchte Contoso eine Verbindung mit den Azure VMs herstellen und Azure die Erlaubnis zum Verwalten der VMs geben. Hierzu führen die Contoso-Administratoren vor der Migration die folgenden Aufgaben durch:

1. Für den Zugriff über das Internet:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Sicherstellen, dass TCP- und UDP-Regeln zum **öffentlichen** Profil hinzugefügt wurden.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.

1. Für den Zugriff über Site-to-Site-VPN:

    - Aktivieren Sie vor der Migration RDP oder SSH auf der lokalen VM.
    - Überprüfen Sie, ob RDP oder SSH in der Betriebssystemfirewall zugelassen wird.
    - Legen Sie für Windows die SAN-Richtlinie des Betriebssystems auf der lokalen VM auf **OnlineAll** fest.

1. Installieren Sie den Azure-Agent:

    - [Azure Linux-Agent](/azure/virtual-machines/extensions/agent-linux)
    - [Azure Windows-Agent](/azure/virtual-machines/extensions/agent-windows)

1. Sonstiges

   - Unter Windows sollten auf dem virtuellen Computer keine ausstehenden Windows-Updates vorhanden sein, wenn Sie eine Migration auslösen. Wenn dies doch der Fall ist, können sich die Contoso-Administratoren erst bei der VM anmelden, nachdem das Update abgeschlossen ist.
   - Nach der Migration kann **Startdiagnose** aktiviert werden, um einen Screenshot der VM anzuzeigen. Falls dies nicht funktioniert, sollte überprüft werden, ob die VM ausgeführt wird, und die folgenden [Tipps zur Problembehandlung](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) sollten gelesen werden.

**Benötigen Sie weitere Hilfe?**

Erfahren Sie, wie Sie [VMs auf die Migration vorbereiten](/azure/migrate/prepare-for-migration).

## <a name="step-6-replicate-the-on-premises-vms-to-azure"></a>Schritt 6: Replizieren der lokalen VMs in Azure

Bevor die Contoso-Administratoren eine Migration zu Azure durchführen können, müssen sie die Replikation einrichten und aktivieren.

Nachdem die Ermittlung abgeschlossen ist, können sie mit der Replikation von VMware-VMs in Azure beginnen.

1. Im Azure Migrate-Projekt wechseln sie zu **Server** > **Azure Migrate- Servermigration** und wählen die Option **Replizieren** aus.

    ![Screenshot: Option „Replizieren“](./media/contoso-migration-rehost-vm/select-replicate.png)

1. Unter **Replizieren** > **Quelleinstellungen** > **Sind Ihre Computer virtualisiert?** wählen sie die Option **Ja, mit VMware vSphere** aus.

1. Unter **Lokale Appliance** wählen sie den Namen der Azure Migrate-Appliance, die eingerichtet wurde, und dann **OK** aus.

    ![Screenshot: Registerkarte „Quelleinstellungen“](./media/contoso-migration-rehost-vm/source-settings.png)

1. Unter **Virtuelle Computer** wählen sie die Computer aus, die repliziert werden sollen.
    - Wenn die Contoso-Administratoren eine Bewertung für die VMs ausgeführt haben, können sie die Empfehlungen zur VM-Größenanpassung und zum Datenträgertyp (Premium/Standard) aus den Bewertungsergebnissen anwenden. Unter **Migrationseinstellungen aus einer Azure Migrate-Bewertung importieren?** wählen sie die Option **Ja** aus.
    - Sie wählen **Nein** aus, wenn sie keine Bewertung durchgeführt haben oder die Bewertungseinstellungen nicht verwenden möchten.
    - Falls sie sich für die Verwendung der Bewertung entschieden haben, wählen sie die VM-Gruppe und den Bewertungsnamen aus.

    ![Screenshot: Auswählen von Bewertungen](./media/contoso-migration-rehost-vm/select-assessment.png)

1. Unter **Virtuelle Computer** suchen sie je nach Bedarf nach VMs und aktivieren alle VMs, die migriert werden sollen. Anschließend wählen sie Folgendes aus: **Weiter: Zieleinstellungen**.

1. Unter **Zieleinstellungen** wählen sie das Abonnement und die Zielregion für die Migration aus und geben die Ressourcengruppe an, in der sich die Azure-VMs nach der Migration befinden. Unter **Virtuelles Netzwerk** wählen sie das virtuelle Azure-Netzwerk oder -Subnetz aus, in das die Azure-VMs nach der Migration eingebunden werden.

1. Unter **Azure-Hybridvorteil** führen die Contoso-Administratoren Folgendes durch:

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

## <a name="step-7-migrate-the-database-via-azure-database-migration-service"></a>Schritt 7: Migrieren der Datenbank mithilfe von Azure Database Migration Service

Die Contoso-Administratoren migrieren die Datenbank mit Azure Database Migration Service, indem sie die Schritte im [ausführlichen Migrationstutorial](/azure/dms/tutorial-sql-server-azure-sql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) ausführen.

Zusammenfassend lässt sich festhalten, dass die folgenden Aufgaben durchgeführt werden müssen:

- Verwenden Sie den Tarif „Premium“, um eine Azure Database Migration Service-Instanz zu erstellen, die eine Verbindung mit dem virtuellen Netzwerk herstellt.
- Vergewissern Sie sich, dass die Instanz über das virtuelle Netzwerk auf die SQL Server-Remoteinstanz zugreifen kann. Stellen Sie sicher, dass alle eingehenden Ports von Azure zu SQL Server auf der virtuellen Netzwerkebene, im Netzwerk-VPN und auf dem Computer, auf dem SQL Server gehostet wird, für den Empfang zugelassen sind.
- Konfigurieren der Instanz:
  - Erstellen Sie ein Migrationsprojekt.
  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.
  - Wählen Sie ein Ziel aus.
  - Wählen Sie die zu migrierenden Datenbanken aus.
  - Konfigurieren Sie die erweiterten Einstellungen.
  - Starten Sie die Replikation.
  - Beheben Sie alle Fehler.
  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.

## <a name="step-8-protect-the-database-with-sql-server-always-on"></a>Schritt 8: Schützen der Datenbank mit SQL Server Always On

Wenn die Anwendungsdatenbank auf `SQLAOG1` ausgeführt wird, können die Contoso-Administratoren diese jetzt mit Always On-Verfügbarkeitsgruppen schützen. Sie konfigurieren SQL Server Always On mit SQL Server Management Studio und weisen anschließend über das Windows-Clustering einen Listener zu.

### <a name="create-an-always-on-availability-group"></a>Erstellen einer Always On-Verfügbarkeitsgruppe

1. In SQL Server Management Studio wird die Option **Hochverfügbarkeit mit Always On** gewählt und gehalten (oder mit der rechten Maustaste darauf geklickt), um den **Assistenten für neue Verfügbarkeitsgruppen** zu starten.
1. Unter **Optionen angeben** gibt das Unternehmen der Verfügbarkeitsgruppe den Namen `SHAOG`. Unter **Datenbanken auswählen** wählt es die `SmartHotel360`-Datenbank aus.

    ![Screenshot: Bereich „Datenbanken auswählen“](./media/contoso-migration-rehost-vm-sql-ag/aog-1.png)

1. Unter **Replikate angeben** fügt das Unternehmen die zwei SQL-Knoten als Verfügbarkeitsreplikate hinzu und konfiguriert diese so, dass ein automatisches Failover mit synchronem Commit bereitgestellt wird.

     ![Screenshot: Registerkarte „Replikate“](./media/contoso-migration-rehost-vm-sql-ag/aog-2.png)

1. Contoso konfiguriert einen Listener für die Gruppe (`SHAOG`) und den Port. Die IP-Adresse des internen Lastenausgleichs wird als statische IP-Adresse (`10.245.40.100`) hinzugefügt.

    ![Screenshot: Option „Verfügbarkeitsgruppenlistener erstellen“](./media/contoso-migration-rehost-vm-sql-ag/aog-3.png)

1. Unter **Datensynchronisierung auswählen** aktiviert das Unternehmen das automatische Seeding. Mit dieser Option erstellt SQL Server für jede Datenbank in der Gruppe automatisch sekundäre Replikate, damit Contoso diese nicht manuell sichern und wiederherstellen muss. Nach der Überprüfung wird die Verfügbarkeitsgruppe erstellt.

    ![Screenshot: Erstellte Always On-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/aog-4.png)

1. Bei der Erstellung der Gruppe ist ein Problem aufgetreten. Es wird nicht die in Active Directory integrierte Sicherheit von Windows verwendet. Die Berechtigungen für die SQL-Anmeldung müssen erteilt werden, damit die Rollen für den Windows-Failovercluster erstellt werden können.

    ![Screenshot: Gewähren von Berechtigungen für die SQL-Anmeldung](./media/contoso-migration-rehost-vm-sql-ag/aog-5.png)

1. Nach der Erstellung der Gruppe wird sie in SQL Server Management Studio angezeigt.

### <a name="configure-a-listener-on-the-cluster"></a>Konfigurieren eines Listeners für den Cluster

Im letzten Schritt der Einrichtung der SQL-Bereitstellung konfigurieren die Contoso-Administratoren den internen Lastenausgleich als Listener für den Cluster und versetzen den Listener in den Onlinezustand. Hierfür verwendet das Unternehmen ein Skript.

![Screenshot: Listener für Cluster](./media/contoso-migration-rehost-vm-sql-ag/cluster-listener.png)

### <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Nachdem Contoso die Einrichtung abgeschlossen hat, verfügt das Unternehmen nun über eine funktionale Verfügbarkeitsgruppe in Azure, die die migrierte Datenbank verwendet. Die Administratoren überprüfen die Konfiguration, indem sie in SQL Server Management Studio eine Verbindung mit dem internen Lastenausgleich herstellen.

![Screenshot: Verbindung mit internem Lastenausgleich](./media/contoso-migration-rehost-vm-sql-ag/ilb-connect.png)

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über die Erstellung einer [Verfügbarkeitsgruppe](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#create-the-availability-group) und eines [Listeners](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#configure-listener).
- Sie können den Vorgang [Einrichten des Clusters für die Verwendung der IP-Adresse des Lastenausgleichs](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#configure-the-cluster-to-use-the-load-balancer-ip-address) manuell durchführen.
- Informieren Sie sich über die [SAS-Erstellung und -Nutzung](/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-9-migrate-the-vm-with-azure-migrate"></a>Schritt 9: Migration der virtuellen Computer mit Azure Migrate

Die Contoso-Administratoren führen ein schnelles Testfailover durch und migrieren anschließend den virtuellen Computer.

### <a name="run-a-test-migration"></a>Ausführen einer Testmigration

Das Ausführen einer Testmigration dient zur Sicherstellung, dass vor der Migration alles wie erwartet funktioniert. Die Contoso-Administratoren führen Folgendes durch:

1. Sie führen ein Testfailover bis zum letzten verfügbaren Zeitpunkt aus (`Latest processed`).
1. Sie wählen **Computer vor Starten des Failovers herunterfahren** aus, damit Azure Migrate versucht, die Quell-VM vor dem Auslösen des Failovers herunterzufahren. Das Failover wird auch dann fortgesetzt, wenn das Herunterfahren nicht erfolgreich ist.
1. Ausführung eines Testfailovers:

    - Eine Überprüfung der erforderlichen Komponenten wird ausgeführt, um sicherzustellen, dass alle Bedingungen für eine Migration erfüllt sind.
    - Durch das Failover werden die Daten verarbeitet, sodass eine Azure-VM erstellt werden kann. Wenn der letzte Wiederherstellungspunkt ausgewählt wird, wird ein Wiederherstellungspunkt auf der Grundlage der Daten erstellt.
    - Eine Azure-VM wird anhand der im vorherigen Schritt verarbeiteten Daten erstellt.

1. Nach Abschluss des Failovers wird der virtuelle Azure-Replikatcomputer im Azure-Portal angezeigt. Das Unternehmen überprüft, ob die VM die richtige Größe hat, mit dem richtigen Netzwerk verbunden ist und ausgeführt wird.
1. Nach der Überprüfung bereinigt es das Failover. Darüber hinaus werden Beobachtungen aufgezeichnet und gespeichert.

### <a name="run-a-failover"></a>Ausführen eines Failovers

1. Nachdem sie überprüft haben, ob das Testfailover wie erwartet funktioniert, erstellen sie einen Wiederherstellungsplan für die Migration und fügen `WEBVM` dem Plan hinzu.

     ![Screenshot: Option „Wiederherstellungsplan erstellen“](./media/contoso-migration-rehost-vm-sql-ag/recovery-plan.png)

1. Das Unternehmen führt ein Failover für den Plan aus. Die Administratoren wählen den letzten Wiederherstellungspunkt aus. Sie geben an, dass Azure Migrate versuchen sollte, die lokale VM vor dem Auslösen des Failovers herunterzufahren.

    ![Screenshot: Bereich „Failover“](./media/contoso-migration-rehost-vm-sql-ag/failover1.png)

1. Nach dem Failover überprüft Contoso, ob die Azure-VM wie erwartet im Azure-Portal angezeigt wird.

    ![Screenshot: Übersichtsbereich für den virtuellen Computer](./media/contoso-migration-rehost-vm-sql-ag/failover2.png)

1. Nach dieser Überprüfung führt das Unternehmen die Migration durch, um den Migrationsprozess zu beenden. Darüber hinaus beendet es die Replikation für die VM und die Azure Migrate-Abrechnung für die VM.

    ![Screenshot: Option „Migration abschließen“](./media/contoso-migration-rehost-vm-sql-ag/failover3.png)

### <a name="update-the-connection-string"></a>Aktualisieren der Verbindungszeichenfolge

Der letzte Schritt im Migrationsprozess besteht in der Aktualisierung der Verbindungszeichenfolge der Anwendung, um auf die migrierte Datenbank zu verweisen, die auf dem `SHAOG`-Listener ausgeführt wird. Diese Konfiguration wird auf der `WEBVM` geändert, die jetzt in Azure ausgeführt wird. Diese Konfiguration befindet sich in der Datei `web.config` der ASP.NET-Anwendung.

1. Die Contoso-Administratoren ermitteln die Datei unter `C:\inetpub\SmartHotelWeb\web.config` und ändern den Namen des Servers, um den FQDN der Always On-Verfügbarkeitsgruppe widerzuspiegeln: `shaog.contoso.com`.

    ![Screenshot: FQDN der Always On-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/failover4.png)

1. Nachdem Contoso die Datei aktualisiert und gespeichert hat, startet das Unternehmen IIS auf `WEBVM` neu. Sie verwenden den Befehl `iisreset /restart` an einer Eingabeaufforderung.
1. Nach dem Neustart von IIS nutzt die Anwendung nun die Datenbank, die auf der verwalteten Instanz ausgeführt wird.

**Benötigen Sie weitere Hilfe?**

- Informieren Sie sich über das [Ausführen eines Testfailovers](/azure/site-recovery/tutorial-dr-drill-azure).
- Informieren Sie sich über das [Erstellen eines Wiederherstellungsplans](/azure/site-recovery/site-recovery-create-recovery-plans).
- Informationen zum [Ausführen eines Failovers für Azure](/azure/site-recovery/site-recovery-failover)

### <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration wird die Anwendung SmartHotel360 auf einer Azure-VM ausgeführt. Die SmartHotel360-Datenbank befindet sich im Azure SQL-Cluster.

Contoso muss jetzt die folgenden Bereinigungsschritte abschließen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Entfernen der VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation und Anzeigen der neuen Speicherorte und IP-Adressen für VMs.
- Überprüfen aller Ressourcen, die mit den außer Betrieb genommenen VMs interagieren. Alle relevanten Einstellungen bzw. Dokumentationsinhalte müssen aktualisiert werden, um die neue Konfiguration widerzuspiegeln.
- Hinzufügen der beiden neuen VMs (`SQLAOG1` und `SQLAOG2`) zu Systemen für die Produktionsüberwachung.

### <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die virtuellen Computer `WEBVM`, `SQLAOG1` und `SQLAOG2` auf eventuell vorhandene Sicherheitsprobleme. Folgendes muss durchgeführt werden:

- Die Netzwerksicherheitsgruppen (NSGs) für die VM zur Steuerung des Zugriffs müssen überprüft werden. Mithilfe von NSGs wird sichergestellt, dass nur für die App zulässiger Datenverkehr übergeben werden kann.
- Es muss erwägt werden, ob die Daten auf den VM-Datenträgern mithilfe von Azure Disk Encryption und Azure Key Vault geschützt werden sollten.
- Transparent Data Encryption wird evaluiert. Anschließend erfolgt die Aktivierung in der SmartHotel360-Datenbank, die in der neuen Always On-Verfügbarkeitsgruppe ausgeführt wird. Lesen Sie die weiteren Informationen zu [Transparent Data Encryption](/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017).

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Zur Sicherstellung der Geschäftskontinuität und Notfallwiederherstellung führt Contoso die folgenden Aktionen durch:

- Zum Schutz sichert Contoso die Daten auf den VMs `WEBVM`, `SQLAOG1` und `SQLAOG2` per [Azure VM Backup](/azure/backup/backup-azure-vms-introduction).
- Contoso informiert sich auch darüber, wie Azure Storage zum Sichern von SQL Server direkt im Azure-Blobspeicher verwendet wird. Informieren Sie sich über das [Verwenden von Azure Storage für die Sicherung und Wiederherstellung von SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-use-storage-sql-server-backup-restore).
- Contoso repliziert die Anwendungs-VMs in Azure per Site Recovery in einer sekundären Region, um die Anwendungen betriebsbereit zu halten. Informieren Sie sich über das [Einrichten der Notfallwiederherstellung in einer sekundären Azure-Region für einen virtuellen Azure-Computer](/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Contoso verfügt über eine Lizenzierung für seine WEBVM-Instanz und nutzt den Azure-Hybridvorteil. Contoso wird die vorhandenen virtuellen Azure-Computer konvertieren, um von diesen Preisen zu profitieren.
- Contoso verwendet [Azure Cost Management und Abrechnung](/azure/cost-management-billing/cost-management-billing-overview), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget vom Unternehmen nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso für die SmartHotel360-Anwendung in Azure einen neuen Host zugewiesen hat, indem die Front-End-VM der Anwendung mit Azure Migrate zu Azure migriert wurde. Contoso hat die Anwendungsdatenbank mit Azure Database Migration Service zu einem in Azure bereitgestellten SQL Server-Cluster migriert und in einer SQL Server Always On-Verfügbarkeitsgruppe geschützt.
