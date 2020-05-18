---
title: Zuweisen eines neuen Hosts zu einer App durch Migration zu Azure-VMs und Always On-Verfügbarkeitsgruppen für SQL Server
description: Dieser Artikel enthält Informationen darüber, wie Contoso einer lokalen App einen neuen Host zuweist, indem diese zu Azure-VMs und zur SQL Server Always On-Verfügbarkeitsgruppe migriert wird.
author: givenscj
ms.author: abuck
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: ff7c476737bed0f079cbebac736506cb6801bfd8
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223608"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM contosohost vcenter contosodc AOAG SQLAOG SQLAOGAVSET contosoadmin contosocloudwitness MSSQLSERVER BEPOOL contosovmsacc SHAOG NSGs inetpub iisreset -->

# <a name="rehost-an-on-premises-app-with-azure-virtual-machines-and-sql-server-always-on-availability-groups"></a>Zuweisen eines neuen Hosts für eine lokale App mit Azure Virtual Machines und in SQL Server Always On-Verfügbarkeitsgruppen

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso einer zweistufigen Windows.NET-App, die auf virtuellen VMware-Computern (VMs) ausgeführt wird, als Teil einer Migration der App-VMs auf Azure einen neuen Host zuweist. Contoso migriert den virtuellen Front-End-Computer der App zu einem virtuellen Azure-Computer und die App-Datenbank zu einem virtuellen Azure SQL Server-Computer, die in einem Windows Server-Failovercluster mit SQL Server AlwaysOn-Verfügbarkeitsgruppen ausgeführt werden.

Die in diesem Beispiel verwendet SmartHotel360-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten die lokalen Systeme und Infrastrukturen unter Druck.

- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.

- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. IT darf nicht im Weg stehen oder zum Geschäftshindernis werden.

- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt:

- Nach der Migration sollte die App in Azure das gleiche Leistungsvermögen aufweisen wie derzeit in der VMware-Umgebung. Die App bleibt lokal und in der Cloud gleichermaßen wichtig.

- Contoso möchte nicht in diese App investieren. Die Investition ist wichtig für das Geschäft, in ihrer derzeitigen Form soll die App jedoch lediglich sicher in die Cloud verschoben werden.

- Bei der lokalen App-Datenbank gab es Verfügbarkeitsprobleme. Contoso möchte sie in Azure als Hochverfügbarkeitscluster mit Failoverfunktionen bereitstellen.

- Contoso möchte ein Upgrade von der aktuellen SQL Server 2008 R2-Plattform auf SQL Server 2017 durchführen.

- Contoso möchte für diese App keine Azure SQL-Datenbank verwenden und sucht nach Alternativen.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess, einschließlich der für die Migration genutzten Azure-Dienste.

### <a name="current-architecture"></a>Aktuelle Architektur

- Die App ist auf zwei VMs aufgeteilt (WEBVM und SQLVM).
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (contoso-datacenter) mit einem lokalen Domänencontroller (**contosodc1**).

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

Szenario:

- Contoso migriert das App-Front-End „WEBVM“ zu einem virtuellen Azure-IaaS-Computer.
  - Der virtuelle Front-End-Computer in Azure wird in der Ressourcengruppe „ContosoRG“ bereitgestellt (wird für Produktionsressourcen verwendet).
  - Er wird sich im Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten 2“ befinden.
- Die App-Datenbank wird zu einem virtuellen Azure SQL Server-Computer migriert.
  - Sie wird sich im Azure-Datenbanknetzwerk von Contoso (PROD-DB-EUS2) in der primären Region „USA, Osten 2“ befinden.
  - Sie wird in einem Windows Server-Failovercluster mit zwei Knoten platziert, der SQL Server AlwaysOn-Verfügbarkeitsgruppen verwendet.
  - In Azure werden die beiden virtuellen SQL Server-Computerknoten im Cluster in der Ressourcengruppe „ContosoRG“ bereitgestellt.
  - Die virtuellen Computerknoten werden sich im Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten2“ befinden.
  - Auf VMs wird Windows Server 2016 mit der SQL Server 2017 Enterprise Edition ausgeführt. Contoso hat keine Lizenzen für dieses Betriebssystem. Daher verwendet das Unternehmen im Azure Marketplace ein Image, das die Lizenz als Gebühr für die Azure EA-Verpflichtung bereitstellt.
  - Abgesehen von eindeutigen Namen verwenden beide VMs die gleichen Einstellungen.
- Contoso stellt einen internen Lastenausgleich bereit, der den Cluster hinsichtlich des Datenverkehrs überwacht und diesen an den entsprechenden Clusterknoten weiterleitet.
  - Der interne Lastenausgleich wird in der Ressourcengruppe ContosoNetworkingRG bereitgestellt (wird für Netzwerkressourcen verwendet).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

    ![Szenarioarchitektur](./media/contoso-migration-rehost-vm-sql-ag/architecture.png)

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso einen Featurevergleich zwischen Azure SQL-Datenbank und SQL Server durchgeführt. Hierbei haben die folgenden Überlegungen Contoso dabei unterstützt, sich für einen virtuellen Azure-IaaS-Computer zu entscheiden, auf dem SQL Server ausgeführt wird:

- Der Einsatz eines virtuellen Azure-Computers mit SQL Server erscheint als optimale Lösung, wenn Contoso das Betriebssystem oder den Datenbankserver anpassen muss, oder wenn Drittanbieter-Apps auf demselben virtuellen Computer installiert und ausgeführt werden sollen.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | WEBVM wird ohne Änderungen nach Azure verlagert, was die Migration vereinfacht. <br><br> Die SQL Server-Schicht wird auf SQL Server 2017 und Windows Server 2016 ausgeführt. Dadurch wird das derzeitige Betriebssystem Windows Server 2008 R2 außer Betrieb genommen, und die Ausführung von SQL Server 2017 unterstützt die technischen Anforderungen und Ziele von Contoso. IT bietet 100%-ige Kompatibilität, während SQL Server 2008 R2 ausgemustert wird. <br><br> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil nutzen. <br><br> Ein hoch verfügbare SQL Server-Bereitstellung in Azure bietet Fehlertoleranz, sodass die App-Datenschicht kein Single Point of Failover mehr ist.
**Nachteile** | Auf WEBVM wird Windows Server 2008 R2 ausgeführt. Das Betriebssystem wird für bestimmte Rollen von Azure unterstützt (Juli 2018). [Weitere Informationen](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines) <br><br> Die Webschicht der App bleibt ein Single Point of Failover. <br><br> Contoso muss die Webschicht weiterhin als virtuellen Azure-Computer unterstützen, anstatt auf einen verwalteten Dienst wie Azure App Service umzustellen. <br><br> Mit der gewählten Lösung muss Contoso weiterhin zwei virtuelle SQL Server-Computer verwalten, anstatt auf eine verwaltete Plattform wie die verwaltete Azure SQL-Datenbank-Instanz umzustellen. Zudem könnte Contoso mit Software Assurance seine vorhandenen Lizenzen gegen reduzierte Tarife der verwalteten Azure SQL-Datenbank-Instanz eintauschen.

<!-- markdownlint-enable MD033 -->

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Der Azure Database Migration Service ermöglicht die nahtlose Migration von mehreren Datenbankquellen zu Azure-Datenplattformen bei minimaler Ausfallzeit. | Informieren Sie sich über die [unterstützten Regionen](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) und die [Preise für den Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | Contoso nutzt den Azure Migrate-Dienst, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | Ab Mai 2018 ist Azure Migrate ein kostenloser Dienst.

## <a name="migration-process"></a>Migrationsprozess

Contoso-Administratoren migrieren die virtuellen Computer der App zu Azure.

- Es migriert die Front-End-VM mithilfe von Azure Migrate zur Azure-VM:
  - Im ersten Schritt bereitet das Unternehmen Azure-Komponenten vor und richtet diese ein, und es bereitet die lokale VMware-Infrastruktur vor.
  - Wenn alle Vorbereitungen getroffen sind, kann Contoso mit dem Replizieren der VM beginnen.
  - Wenn die Replikation aktiviert wurde und funktioniert, migriert das Unternehmen die VM via Failover zu Azure.
- Nachdem die Datenbank überprüft wurde, wird sie mithilfe des Data Migration Service (DMS) zu einem SQL Server-Cluster in Azure migriert.
  - Im ersten Schritt müssen SQL Server-VMs in Azure bereitgestellt, der Cluster und ein interner Lastenausgleich eingerichtet und Always On-Verfügbarkeitsgruppen konfiguriert werden.
  - Anschließend kann die Datenbank migriert werden
- Nach der Migration wird der Always On-Schutz für die Datenbank aktiviert.

    ![Migrationsprozess](./media/contoso-migration-rehost-vm-sql-ag/migration-process.png)

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes.

<!-- markdownlint-disable MD033 -->

| **Anforderungen** | **Details** |
| --- | --- |
| **Azure-Abonnement** | Contoso hat bereits in einem früheren Artikel dieser Reihe ein Abonnement erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Contoso – Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) beschrieben. <br><br> Hier erfahren Sie mehr über bestimmte [Voraussetzungen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) für Azure Migrate: Servermigration. |
| **Lokale Server** | Auf dem lokalen vCenter-Server sollte Version 5.5, 6.0, 6.5 oder 6.7 ausgeführt werden. <br><br> Ein ESXi-Host mit Version 5.5, 6.0, 6.5 oder 6.7. <br><br> Mindestens eine VMware-VM auf dem ESXi-Host. |
| **Lokale VMs** | [Überprüfen Sie Linux-Computer](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), deren Ausführung unter Azure unterstützt wird. |

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Vorbereiten eines AOAG-Clusters.** Erstellen Sie einen Cluster für die Bereitstellung von zwei virtuellen SQL Server-Knoten in Azure.
> - **Schritt 2: Bereitstellen und Einrichten des Clusters.** Bereiten Sie einen Azure SQL Server-Cluster vor. Datenbanken werden in diesen vorhandenen Cluster migriert.
> - **Schritt 3: Bereitstellen von Azure Load Balancer.** Stellen Sie einen Lastenausgleich für den Datenverkehr zu den SQL Server-Knoten bereit.
> - **Schritt 4: Vorbereiten von Azure für Azure Migrate.** Erstellen Sie ein Azure-Speicherkonto für die Speicherung replizierter Daten.
> - **Schritt 5: Vorbereiten der lokalen VMware-Instanz für Azure Migrate.** Bereiten Sie Konten für die VM-Ermittlung und die Agent-Installation vor. Vorbereiten lokaler virtueller Computer, damit Benutzer nach der Migration eine Verbindung mit virtuellen Azure-Computern herstellen können.
> - **Schritt 6: Replizieren von VMs.** Ermöglichen Sie die VM-Replikation in Azure.
> - **Schritt 7: Migrieren der Datenbank mit Database Migration Service (DMS).** Migrieren Sie die Datenbank mit dem Database Migration Service zu Azure.
> - **Schritt 8: Schützen der Datenbank.** Erstellen Sie eine Always On-Verfügbarkeitsgruppe für den Cluster.
> - **Schritt 9: Migrieren der VMs mithilfe von Azure Migrate** Ausführen eines Testfailovers, um sicherzustellen, dass alles erwartungsgemäß funktioniert. Anschließendes Ausführen eines vollständigen Failovers zu Azure.

## <a name="step-1-prepare-a-sql-server-always-on-availability-group-cluster"></a>Schritt 1: Vorbereiten eines Clusters für SQL Server Always On-Verfügbarkeitsgruppen

Contoso-Administratoren richten den Cluster wie folgt ein:

1. Das Unternehmen erstellt zwei SQL Server-VMs, indem es das Image SQL Server 2017 Enterprise Windows Server 2016 im Azure Marketplace auswählt.

    ![SQL-VM-SKU](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-sku.png)

2. Unter **Assistent für die Erstellung virtueller Computer** > **Grundlagen** konfiguriert das Unternehmen Folgendes:

    - Namen für die virtuellen Computer: **SQLAOG1** und **SQLAOG2**.
    - Da Computer unternehmenskritisch sind, aktiviert Contoso SSD für den VM-Datenträgertyp.
    - Es gibt Anmeldeinformationen für Computer an.
    - Das Unternehmen stellt die VMs in der primären Region „USA, Osten 2“ in der Ressourcengruppe ContosoRG bereit.

3. Unter **Größe** beginnt das Unternehmen bei beiden VMs mit der SKU „D2s_V3“. Nach Bedarf kann die Skalierung zu einem späteren Zeitpunkt durchgeführt werden.
4. Das Unternehmen führt unter **Einstellungen** die folgenden Schritte aus:

    - Da es sich bei diesen VMs um wichtige Datenbanken für die App handelt, verwenden sie verwaltete Datenträger.
    - Das Unternehmen ordnet die Computer im Produktionsnetzwerk der primären Region „USA, Osten 2“ (**VNET-PROD-EUS2**) im Subnetz der Datenbank (**PROD-DB-EUS2**) an.
    - Es wird eine neue Verfügbarkeitsgruppe erstellt: **SQLAOGAVSET** mit zwei Fehlerdomänen und fünf Updatedomänen.

      ![SQL-VM](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-settings.png)

5. Contoso begrenzt über die **SQL Server-Einstellungen** die SQL-Konnektivität mit dem virtuellen Netzwerk (privat) am Standardport 1433. Für die Authentifizierung verwendet es die gleichen Anmeldeinformationen wie vor Ort (**contosoadmin**).

    ![SQL-VM](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-db.png)

**Benötigen Sie weitere Hilfe?**

- [Hilfe](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#1-configure-basic-settings) zur Bereitstellung einer SQL Server-VM.
- [Weitere Informationen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-prereq#create-sql-server-vms) zum Konfigurieren von VMs für verschiedene SQL Server-SKUs.

## <a name="step-2-deploy-and-set-up-the-cluster"></a>Schritt 2: Bereitstellen und Einrichten des Clusters

Contoso-Administratoren gehen bei der Einrichtung des Clusters wie folgt vor:

1. Das Unternehmen richtet ein Azure-Speicherkonto ein, um als Cloudzeuge zu fungieren.
2. Es fügt die SQL Server-VMs zur Active Directory-Domäne im lokalen Contoso-Rechenzentrum hinzu.
3. Es erstellt den Cluster in Azure.
4. Es konfiguriert den Cloudzeugen.
5. Schließlich aktiviert das Unternehmen die Always On-Verfügbarkeitsgruppen von SQL.

### <a name="set-up-a-storage-account-as-cloud-witness"></a>Einrichten eines Speicherkontos als Cloudzeuge

Für die Einrichtung eines Cloudzeugen benötigt Contoso ein Azure-Speicherkonto, das die Blob-Datei für die Clustervermittlung enthält. Dasselbe Speicherkonto kann für die Einrichtung eines Cloudzeugen für mehrere Cluster verwendet werden.

Contoso-Administratoren gehen bei der Erstellung eines Speicherkontos wie folgt vor:

1. Das Unternehmen gibt einen erkennbaren Namen für das Konto an (**contosocloudwitness**).
2. Es stellt ein allgemein einsetzbares Konto mit LRS bereit.
3. Contoso platziert das Konto in einer dritten Region: USA, Süden-Mitte. Es platziert das Konto außerhalb der primären und sekundären Region, damit es während eines regionalen Ausfalls verfügbar bleibt.
4. Das Unternehmen platziert das Konto in seiner Ressourcengruppe mit Infrastrukturressourcen: **ContosoInfraRG**.

    ![Cloudzeuge](./media/contoso-migration-rehost-vm-sql-ag/witness-storage.png)

5. Wenn das Unternehmen das Speicherkonto erstellt, werden für dieses Konto primäre und sekundäre Zugriffsschlüssel generiert. Der primäre Zugriffsschlüssel wird für die Erstellung des Cloudzeugen benötigt. Der Schlüssel wird unter dem Namen des Speicherkontos > **Zugriffstasten** angezeigt.

    ![Zugriffsschüssel](./media/contoso-migration-rehost-vm-sql-ag/access-key.png)

### <a name="add-sql-server-vms-to-contoso-domain"></a>Hinzufügen von SQL Server-VMs zur Contoso-Domäne

1. Contoso fügt die VMs SQLAOG1 und SQLAOG2 zur Domäne contoso.com hinzu.
2. Anschließend werden auf jeder VM das Feature und die Tools des Windows-Failoverclusters installiert.

### <a name="set-up-the-cluster"></a>Einrichten des Clusters

Vor dem Einrichten des Clusters erstellen Contoso-Administratoren auf jedem Computer eine Momentaufnahme des Betriebssystemdatenträgers.

![Erstellen einer Momentaufnahme](./media/contoso-migration-rehost-vm-sql-ag/snapshot.png)

1. Anschließend führt das Unternehmen ein Skript aus, mit dem der Windows-Failovercluster erstellt werden soll.

    ![Cluster erstellen](./media/contoso-migration-rehost-vm-sql-ag/create-cluster1.png)

2. Nach der Erstellung des Clusters überprüft das Unternehmen, ob die VMs als Clusterknoten angezeigt werden.

     ![Cluster erstellen](./media/contoso-migration-rehost-vm-sql-ag/create-cluster2.png)

### <a name="configure-the-cloud-witness"></a>Konfigurieren des Cloudzeugen

1. Contoso-Administratoren konfigurieren den Cloudzeugen mithilfe des **Assistenten für die Quorumkonfiguration** im Failovercluster-Manager.
2. Im Assistenten erstellt das Unternehmen einen Cloudzeugen mit dem Speicherkonto.
3. Nach der Konfiguration des Cloudzeugen wird dieser im Failovercluster-Manager-Snap-In angezeigt.

    ![Cloudzeuge](./media/contoso-migration-rehost-vm-sql-ag/cloud-witness.png)

### <a name="enable-sql-server-always-on-availability-groups"></a>Aktivieren von SQL Server Always On-Verfügbarkeitsgruppen

Contoso-Administratoren können jetzt Always On aktivieren:

1. Das Unternehmen aktiviert im SQL Server-Konfigurations-Manager die **Always On-Verfügbarkeitsgruppen** für den Dienst **SQL Server (MSSQLSERVER)** .

    ![Aktivieren von AlwaysOn](./media/contoso-migration-rehost-vm-sql-ag/enable-always-on.png)

2. Das Unternehmen startet den Dienst neu, damit die Änderungen wirksam werden.

Nach der Aktivierung von Always On kann Contoso die Always On-Verfügbarkeitsgruppe für den Schutz der SmartHotel360-Datenbank einrichten.

**Benötigen Sie weitere Hilfe?**

- [Weitere Informationen](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness) zum Cloudzeugen und zum Einrichten eines Speicherkontos für diesen Cloudzeugen.
- [Anweisungen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial) zum Einrichten eines Clusters und zum Erstellen einer Verfügbarkeitsgruppe.

## <a name="step-3-deploy-the-azure-load-balancer"></a>Schritt 3: Bereitstellen von Azure Load Balancer

Contoso-Administratoren möchten nun ein internes Lastenausgleichsmodul bereitstellen, das sich vor den Clusterknoten befindet. Das Lastenausgleichsmodul ist für Datenverkehr empfangsbereit und leitet diesen an den entsprechenden Knoten weiter.

![Lastenausgleich](./media/contoso-migration-rehost-vm-sql-ag/architecture-lb.png)

Contoso geht bei der Erstellung des Lastenausgleichs wie folgt vor:

1. Das Unternehmen richtet im Azure-Portal unter **Netzwerk** > **Lastenausgleich** einen neuen internen Lastenausgleich ein: **ILB-PROD-DB-EUS2-SQLAOG**.
2. Das Unternehmen ordnet den Lastenausgleich im Produktionsnetzwerk **VNET-PROD-EUS2** im Subnetz der Datenbank **PROD-DB-EUS2** an.
3. Dem Lastenausgleich wird eine statische IP-Adresse zugewiesen: 10.245.40.100.
4. Der Lastenausgleich wird als Netzwerkelement in der Netzwerkressourcengruppe **ContosoNetworkingRG** bereitgestellt.

    ![Lastenausgleich](./media/contoso-migration-rehost-vm-sql-ag/lb-create.png)

Nach der Bereitstellung des internen Lastenausgleichs muss dieser eingerichtet werden. Das Unternehmen erstellt einen Back-End-Adresspool, richtet einen Integritätstest ein und konfiguriert eine Regel für den Lastenausgleich.

### <a name="add-a-back-end-pool"></a>Hinzufügen eines Back-End-Pools

Zum Verteilen von Datenverkehr an die virtuellen Computer im Cluster richten Contoso-Administratoren einen Back-End-Adresspool ein, der die IP-Adressen der NICs für virtuelle Computer enthält, die den Netzwerkdatenverkehr über den Lastenausgleich empfangen.

1. Contoso fügt im Portal in den Einstellungen für den Lastenausgleich einen Back-End-Pool hinzu: **ILB-PROD-DB-EUS-SQLAOG-BEPOOL**.
2. Dem Pool wird die Verfügbarkeitsgruppe SQLAOGAVSET zugeordnet. Die VMs in der Gruppe (**SQLAOG1** und **SQLAOG2**) werden zum Pool hinzugefügt.

    ![Back-End-Pool](./media/contoso-migration-rehost-vm-sql-ag/backend-pool.png)

### <a name="create-a-health-probe"></a>Erstellen eines Integritätstests

Contoso-Administratoren erstellen einen Integritätstest, damit der Lastenausgleich den Status der App überwachen kann. Abhängig von der Reaktion auf Integritätstests werden durch den Integritätstest dynamisch VMs zur Lastenausgleichsrotation hinzugefügt oder daraus entfernt.

Das Unternehmen geht bei der Erstellung des Tests wie folgt vor:

1. Contoso erstellt im Portal in den Einstellungen für den Lastenausgleich einen Integritätstest: **SQLAlwaysOnEndPointProbe**.
2. Das Unternehmen legt fest, dass bei dem Test VMs an TCP-Port 59999 überwacht werden sollen.
3. Es legt ein Intervall von 5 Sekunden zwischen den Tests und einen Schwellenwert von 2 fest. Wenn zwei Tests fehlschlagen, gilt eine VM als fehlerhaft.

    ![Test](./media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

### <a name="configure-the-load-balancer-to-receive-traffic"></a>Konfigurieren des Lastenausgleichs für den Empfang von Datenverkehr

Contoso-Administratoren richten jetzt eine Regel für den Lastenausgleich ein, um zu definieren, wie Datenverkehr auf die virtuellen Computer verteilt wird.

- Die Front-End-IP-Adresse verarbeitet eingehenden Datenverkehr.
- Der Back-End-IP-Pool empfängt den Datenverkehr.

Das Unternehmen geht bei der Erstellung der Regel wie folgt vor:

1. Es fügt im Portal in den Einstellungen für den Lastenausgleich eine neue Regel hinzu: **SQLAlwaysOnEndPointListener**.
2. Es legt für den Empfang von eingehendem Datenverkehr des SQL-Clients an TCP-Port 1433 einen Front-End-Listener fest.
3. Es gibt den Back-End-Pool an, an den Datenverkehr weitergeleitet werden soll, und den Port, an dem die VMs für den Datenverkehr empfangsbereit sind.
4. Es aktiviert Floating IP (Direct Server Return). Dies ist für SQL Always On immer erforderlich.

    ![Test](./media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

**Benötigen Sie weitere Hilfe?**

- [Übersicht](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) über Azure Load Balancer.
- [Weitere Informationen](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal) zum Erstellen eines Lastenausgleichs.

## <a name="step-4-prepare-azure-for-azure-migrate"></a>Schritt 4: Vorbereiten von Azure für Azure Migrate

Im Folgenden werden die Azure-Komponenten aufgeführt, die Contoso für die Bereitstellung von Azure Migrate benötigt:

- Ein VNet, in dem sich VMs befinden, wenn diese während eines Failovers erstellt werden.
- Ein Azure-Speicherkonto für die Speicherung replizierter Daten.

Contoso-Administratoren gehen bei der Einrichtung dieser Komponenten wie folgt vor:

1. Contoso hat bereits ein Netzwerk/Subnetz erstellt, das für Azure Migrate verwendet werden kann, wenn das Unternehmen die [Azure-Infrastruktur bereitgestellt](./contoso-migration-rehost-vm-sql-ag.md) hat.

    - Bei der SmartHotel360-App handelt es sich um eine Produktions-App. WEBVM wird zum Azure-Produktionsnetzwerk (VNET-PROD-EUS2) in der primären Region „USA, Osten 2“ migriert.
    - WEBVM wird in der Ressourcengruppe ContosoRG, die für Produktionsressourcen verwendet wird, und im Produktionssubnetz (PROD-FE EUS2) platziert.

2. Contoso-Administratoren erstellen ein Azure-Speicherkonto (contosovmsacc20180528) in der primären Region.

    - Contoso verwendet ein allgemeines Konto mit Standardspeicher und LRS-Replikation.

## <a name="step-5-prepare-on-premises-vmware-for-azure-migrate"></a>Schritt 5: Vorbereiten der lokalen VMware-Instanz für Azure Migrate

Contoso-Administratoren bereiten lokal Folgendes vor:

- Ein Konto auf dem Server von vCenter Server oder dem vSphere ESXi-Host zum Automatisieren der VM-Ermittlung.
- Lokale VM-Einstellungen, damit Contoso nach einem Failover eine Verbindung mit der replizierten Azure-VM herstellen kann.

### <a name="prepare-an-account-for-automatic-discovery"></a>Vorbereiten eines Kontos für die automatische Ermittlung

Azure Migrate benötigt Zugriff auf VMware-Server, um folgende Aufgaben durchzuführen:

- Automatisches Ermitteln von VMs.
- Orchestrieren von Replikation, Failover und Failback.
- Dafür ist mindestens ein Konto mit Lesezugriff erforderlich. Sie benötigen ein Konto, das berechtigt ist, Vorgänge wie das Erstellen und Entfernen von Datenträgern sowie das Einschalten virtueller Computer durchzuführen.

Contoso-Administratoren richten das Konto wie folgt ein:

1. Es wird eine Rolle auf vCenter-Ebene erstellt.
2. Anschließend werden dieser Rolle die erforderlichen Berechtigungen zugewiesen.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Vorbereiten der Verbindungsherstellung mit Azure-VMs nach dem Failover

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

   - [Informationen](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) zum Vorbereiten von virtuellen Computern für die Migration

## <a name="step-6-replicate-the-on-premises-vms-to-azure"></a>Schritt 6: Replizieren der lokalen VMs in Azure

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

## <a name="step-7-migrate-the-database-with-azure-database-migration-service-dms"></a>Schritt 7: Migrieren der Datenbank mit dem Azure Database Migration Service (DMS)

Die Administratoren von Contoso migrieren sie mithilfe von Azure Database Migration Services (DMS) anhand des [Schritt-für-Schritt-Tutorials für die Migration](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online). Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) ausführen.

Zusammenfassend müssen Sie die folgenden Schritte ausführen:

- Erstellen Sie einen Azure Database Migration Service (DMS) mit einer `Premium`-SKU, der mit dem VNet verbunden ist.
- Vergewissern Sie sich, dass der Azure Database Migration Service (DMS) über das virtuelle Netzwerk auf den SQL-Remoteserver zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu SQL Server auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem SQL Server gehostet ist, zugelassen werden.
- Konfigurieren des Azure Database Migration Service:
  - Erstellen Sie ein Migrationsprojekt.
  - Fügen Sie eine Quelle (lokale Datenbank) hinzu.
  - Wählen Sie ein Ziel aus.
  - Wählen Sie die zu migrierende(n) Datenbank(en) aus.
  - Konfigurieren Sie die erweiterten Einstellungen.
  - Starten Sie die Replikation.
  - Beheben Sie alle Fehler.
  - Führen Sie den abschließenden Cutover (Systemwechsel) durch.

## <a name="step-8-protect-the-database-with-always-on"></a>Schritt 8: Schützen der Datenbank mit Always On

Wenn die App-Datenbank auf **SQLAOG1** ausgeführt wird, können Contoso-Administratoren diese jetzt mithilfe von AlwaysOn-Verfügbarkeitsgruppen schützen. Das Unternehmen konfiguriert Always On mit SQL Server Management Studio und weist anschließend über das Windows-Clustering einen Listener zu.

### <a name="create-an-always-on-availability-group"></a>Erstellen einer Always On-Verfügbarkeitsgruppe

1. Contoso klickt in SQL Server Management Studio mit der rechten Maustaste auf **Hochverfügbarkeit mit Always On**, um den **Assistenten für neue Verfügbarkeitsgruppen** zu starten.
2. Unter **Optionen angeben** gibt das Unternehmen der Verfügbarkeitsgruppe den Namen **SHAOG**. Unter **Datenbanken auswählen** wählt das Unternehmen die SmartHotel360-Datenbank aus.

    ![AlwaysOn-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/aog-1.png)

3. Unter **Specify Replicas** (Replikate angeben) fügt das Unternehmen die zwei SQL-Knoten als Verfügbarkeitsreplikate hinzu und konfiguriert diese so, dass ein automatisches Failover mit synchronem Commit bereitgestellt wird.

     ![AlwaysOn-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/aog-2.png)

4. Contoso konfiguriert einen Listener für die Gruppe (**SHAOG**) und den Port. Die IP-Adresse des internen Lastenausgleichs wird als statische IP-Adresse (10.245.40.100) hinzugefügt.

    ![AlwaysOn-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/aog-3.png)

5. Unter **Datensynchronisierung auswählen** aktiviert das Unternehmen das automatische Seeding. Mit dieser Option erstellt SQL Server für jede Datenbank in der Gruppe automatisch die sekundären Replikate, sodass Contoso diese nicht manuell sichern und wiederherstellen muss. Nach der Überprüfung wird die Verfügbarkeitsgruppe erstellt.

    ![AlwaysOn-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/aog-4.png)

6. Bei der Erstellung der Gruppe ist ein Problem aufgetreten. Contoso verwendet in Active Directory nicht die integrierte Sicherheit von Windows. Folglich müssen Berechtigungen für die SQL-Anmeldung erteilt werden, damit die Rollen für den Windows-Failovercluster erstellt werden können.

    ![AlwaysOn-Verfügbarkeitsgruppe](./media/contoso-migration-rehost-vm-sql-ag/aog-5.png)

7. Nach der Erstellung der Gruppe kann Contoso diese in SQL Server Management Studio anzeigen.

### <a name="configure-a-listener-on-the-cluster"></a>Konfigurieren eines Listeners für den Cluster

Im letzten Schritt der Einrichtung der SQL-Bereitstellung konfigurieren Contoso-Administratoren den internen Lastenausgleich als Listener für den Cluster und schalten den Listener online. Hierzu verwendet das Unternehmen ein Skript.

![Listener für Cluster](./media/contoso-migration-rehost-vm-sql-ag/cluster-listener.png)

### <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Nachdem Contoso die Einrichtung abgeschlossen hat, verfügt das Unternehmen nun über eine funktionale Verfügbarkeitsgruppe in Azure, die die migrierte Datenbank verwendet. Administratoren überprüfen dies, indem sie eine Verbindung in SQL Server Management Studio mit dem internen Lastenausgleich herstellen.

![Verbinden mit dem internen Lastenausgleich](./media/contoso-migration-rehost-vm-sql-ag/ilb-connect.png)

**Benötigen Sie weitere Hilfe?**

- Weitere Informationen zum Erstellen einer [Verfügbarkeitsgruppe](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#create-the-availability-group) und eines [Listeners](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#configure-listener).
- Sie können den Vorgang [Einrichten des Clusters für die Verwendung der IP-Adresse des Lastenausgleichs](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#configure-the-cluster-to-use-the-load-balancer-ip-address) manuell durchführen.
- [Weitere Informationen](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2) zum Erstellen und Verwenden von SAS.

## <a name="step-9-migrate-the-vm-with-azure-migrate"></a>Schritt 9: Migration der virtuellen Computer mit Azure Migrate

Die Contoso-Administratoren führen ein schnelles Testfailover aus und migrieren anschließend die virtuellen Computer.

### <a name="run-a-test-failover"></a>Ausführen eines Testfailovers

Das Ausführen eines Testfailovers dient zur Sicherstellung, dass vor der Migration alles wie erwartet funktioniert.

1. Sie führen ein Testfailover auf den letzten verfügbaren Zeitpunkt aus (**Zuletzt verarbeitet**).
2. **Computer vor Starten des Failovers herunterfahren** wird ausgewählt, damit Azure Migrate versucht, die Quell-VM vor dem Auslösen des Failovers herunterzufahren. Das Failover wird auch dann fortgesetzt, wenn das Herunterfahren nicht erfolgreich ist.
3. Testfailover durchführen:

    - Eine Überprüfung der erforderlichen Komponenten wird ausgeführt, um sicherzustellen, dass alle Bedingungen für eine Migration erfüllt sind.
    - Durch das Failover werden die Daten verarbeitet, sodass eine Azure-VM erstellt werden kann. Wenn der letzte Wiederherstellungspunkt ausgewählt wird, wird ein Wiederherstellungspunkt auf der Grundlage der Daten erstellt.
    - Eine Azure-VM wird anhand der im vorherigen Schritt verarbeiteten Daten erstellt.

4. Nach Abschluss des Failovers wird der virtuelle Azure-Replikatcomputer im Azure-Portal angezeigt. Das Unternehmen überprüft, ob die VM die richtige Größe hat, mit dem richtigen Netzwerk verbunden ist und ausgeführt wird.
5. Nach der Überprüfung bereinigt es das Failover. Darüber hinaus werden Beobachtungen aufgezeichnet und gespeichert.

### <a name="run-a-failover"></a>Ausführen eines Failovers

1. Nachdem Contoso-Administratoren überprüft haben, ob das Testfailover wie erwartet funktioniert, erstellen sie einen Wiederherstellungsplan für die Migration und fügen WEBVM dem Plan hinzu.

     ![Wiederherstellungsplan](./media/contoso-migration-rehost-vm-sql-ag/recovery-plan.png)

2. Das Unternehmen führt ein Failover für den Plan aus. Es entscheidet, ein Failover für den letzten Wiederherstellungspunkt auszuführen. Zudem gibt das Unternehmen an, dass Azure Migrate versuchen sollte, die lokale VM vor dem Auslösen des Failovers herunterzufahren.

    ![Failover](./media/contoso-migration-rehost-vm-sql-ag/failover1.png)

3. Nach dem Failover überprüft Contoso, ob die Azure-VM wie erwartet im Azure-Portal angezeigt wird.

    ![Wiederherstellungsplan](./media/contoso-migration-rehost-vm-sql-ag/failover2.png)

4. Nach dieser Überprüfung führt das Unternehmen die Migration durch, um den Migrationsprozess zu beenden. Darüber hinaus beendet es die Replikation für die VM und die Azure Migrate-Abrechnung für die VM.

    ![Failover](./media/contoso-migration-rehost-vm-sql-ag/failover3.png)

### <a name="update-the-connection-string"></a>Aktualisieren der Verbindungszeichenfolge

Der letzte Schritt im Migrationsprozess besteht in der Aktualisierung der Verbindungszeichenfolge der Anwendung, um auf die migrierte Datenbank zu verweisen, die auf dem SHAOG-Listener ausgeführt wird. Diese Konfiguration wird auf der WEBVM geändert, die jetzt in Azure ausgeführt wird. Diese Konfiguration befindet sich in der Datei „web.config“ der ASP-Anwendung.

1. Suchen Sie die Datei unter `C:\inetpub\SmartHotelWeb\web.config`. Ändern Sie den Namen des Servers, damit der FQDN der Always On-Verfügbarkeitsgruppe widergespiegelt wird: shaog.contoso.com.

    ![Failover](./media/contoso-migration-rehost-vm-sql-ag/failover4.png)

2. Nachdem Contoso die Datei aktualisiert und gespeichert hat, startet das Unternehmen IIS auf WEBVM neu. Dies erfolgt mithilfe von `iisreset /restart` an einer Eingabeaufforderung.
3. Nachdem IIS neu gestartet wurde, verwendet die Anwendung nun die Datenbank, die auf der verwalteten SQL-Instanz ausgeführt wird.

**Benötigen Sie weitere Hilfe?**

- [Informationen](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) zum Ausführen eines Testfailovers.
- [Informationen](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans) zum Erstellen eines Wiederherstellungsplans.
- [Informationen](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) zum Ausführen eines Failovers für Azure.

### <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration wird die SmartHotel360-App auf einem Azure-VM ausgeführt, und die SmartHotel360-Datenbank befindet sich im Azure SQL-Cluster.

Contoso muss jetzt folgende Schritte für die Bereinigung durchführen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Entfernen der VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation und Anzeigen der neuen Speicherorte und IP-Adressen für VMs.
- Überprüfen sämtlicher Ressourcen, die mit den außer Betrieb genommenen VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.
- Hinzufügen der beiden neuen VMs (SQLAOG1 und SQLAOG2) zu Systemen für die Produktionsüberwachung.

### <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs WEBVM, SQLAOG1 und SQLAOG2 auf eventuell vorhandene Sicherheitsprobleme.

- Das Team überprüft die Netzwerksicherheitsgruppen (NSGs) der des virtuellen Computers zur Steuerung des Zugriffs. Mithilfe von NSGs wird sichergestellt, dass nur für die App zulässiger Datenverkehr übergeben werden kann.
- Das Team zieht darüber hinaus in Erwägung, die Daten über Azure Disk Encryption und Key Vault zu sichern.
- Das Team sollte die transparente Datenverschlüsselung (Transparent Data Encryption, TDE) auswerten und dann in der SmartHotel360-Datenbank aktivieren, die auf dem neuen SQL AOG ausgeführt wird. [Weitere Informationen](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017)

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Für die Geschäftskontinuität und Notfallwiederherstellung (Business Continuity & Disaster Recovery, BCDR) führt Contoso die folgenden Aktionen durch:

- Contoso sichert die Daten mithilfe des Azure Backup-Diensts auf den virtuellen Computern WEBVM, SQLAOG1 und SQLAOG2, um Daten zu schützen. [Weitere Informationen](https://docs.microsoft.com/azure/backup/backup-overview)
- Contoso erfährt auch, wie Azure Storage zum Sichern von SQL Server direkt im Blobspeicher verwendet wird. [Weitere Informationen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-use-storage-sql-server-backup-restore)
- Contoso repliziert die App-VMs mithilfe von Site Recovery in eine sekundäre Region, um Apps funktionstüchtig zu halten. [Weitere Informationen](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Contoso verfügt über eine Lizenzierung für WEBVM und nutzt den Azure-Hybridvorteil. Contoso wird die vorhandenen virtuellen Azure-Computer konvertieren, um von diesen Preisen zu profitieren.
- Contoso verwendet [Azure Cost Management](https://azure.microsoft.com/services/cost-management), um sicherzustellen, dass das von den IT-Führungskräften festgelegte Budget nicht überschritten wird.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat Contoso der SmartHotel360-App in Azure einen neuen Host zugewiesen, indem das Unternehmen die Front-End-VM der App mithilfe des Azure Migrate-Diensts zu Azure migrierte. Contoso hat die App-Datenbank mithilfe von Azure Database Migration Service zu einem in Azure bereitgestellten SQL Server-Cluster migriert und diesen in einer SQL Server AlwaysOn-Verfügbarkeitsgruppe geschützt.
