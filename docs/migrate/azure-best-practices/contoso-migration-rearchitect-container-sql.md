---
title: Umstrukturieren einer App in einem Azure-Container und einer Azure SQL-Datenbank-Instanz
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie eine lokale Anwendung in einem Azure-Container und einer Azure SQL-Datenbank-Instanz umstrukturieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 37bf2a4d96cc1f60b351f40f6a2c51c2ea1dcf95
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311641"
---
<!-- cSpell:ignore reqs contosohost contosodc contosoacreus contososmarthotel smarthotel vcenter WEBVM SQLVM -->

# <a name="rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a>Umstrukturieren einer lokalen App zu einem Azure-Container und einer Azure SQL-Datenbank-Instanz

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso eine zweistufige Windows.NET-App, die auf VMware-VMs ausgeführt wird, als Teil einer Migration der App-VMs auf Azure umstrukturiert. Contoso migriert die Front-End-VM der App zu einem Azure-Windows-Container und die App-Datenbank zu einer Azure SQL-Datenbank-Instanz.

Die in diesem Beispiel verwendet SmartHotel360-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam von Contoso hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was sie mit dieser Migration erreichen möchten:

- **Unternehmenswachstum.** Contoso wächst, und daher geraten seine lokalen Systeme und Infrastrukturen unter Druck.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. Es darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

<!-- markdownlint-disable MD033 -->

**Ziele** | **Details**
--- | ---
**App-Anforderungen** | Die App wird in Azure so wichtig bleiben wie heute.<br/><br/> Sie sollte die gleichen Leistungsmerkmale wie aktuell in VMware aufweisen.<br/><br/> Contoso möchte Windows Server 2008 R2, unter dem die App derzeit gehostet wird, nicht mehr unterstützen und ist bereit, in die App zu investieren.<br/><br/> Contoso möchte weg von SQL Server 2008 R2 und hin zu einer modernen verwalteten Datenbankplattform, die den Verwaltungsaufwand minimiert.<br/><br/> Seine Investitionen in die SQL Server-Lizenzierung und in die Software Assurance möchte Contoso nutzen, wo immer dies möglich ist.<br/><br/> Contoso möchte in der Lage sein, die Webebene der App bei Bedarf zu skalieren.
**Einschränkungen** | Die App besteht aus einer ASP.NET-App und einem WCF-Dienst, die auf derselben VM ausgeführt werden. Contoso möchte diese über Azure App Service auf zwei Web-Apps aufteilen.
**Azure-Anforderungen** | Contoso möchte die App in Azure umziehen und in einem Container ausführen, um die Lebensdauer der App zu verlängern. Das Unternehmen möchte nicht bei Null beginnen, um die App in Azure zu implementieren.
**DevOps** | Contoso möchte den Betrieb auf ein DevOps-Modell mit Azure DevOps Services für Builds und die Releasepipeline umstellen.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-app"></a>Aktuelle App

- Die lokale App SmartHotel360 ist auf zwei VMs aufgeteilt (WEBVM und SQLVM).
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5)
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (contoso-datacenter) mit einem lokalen Domänencontroller (**contosodc1**).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Für die Datenbankebene der App verglich Contoso mithilfe [dieses Artikels](https://docs.microsoft.com/azure/sql-database/sql-database-features) Azure SQL-Datenbank mit SQL Server. Die Entscheidung für Azure SQL-Datenbank hat verschiedene Gründe:
  - Azure SQL-Datenbank ist ein verwalteter Dienst für relationale Datenbanken. Er bietet eine vorhersagbare Leistung auf mehreren Serviceleveln bei nahezu keinem Administrationsaufwand. Zu den Vorteilen gehören dynamische Skalierbarkeit ohne Ausfallzeiten, integrierte intelligente Optimierung sowie globale Skalierbarkeit und Verfügbarkeit.
  - Contoso nutzt den einfachen Datenmigrations-Assistenten (DMA), um die lokale Datenbank zu bewerten und zu Azure SQL-Datenbank zu migrieren.
  - Mit der Software Assurance kann Contoso seine vorhandenen Lizenzen mit dem Azure-Hybridvorteil für SQL Server zu ermäßigten Preisen für eine SQL-Datenbank-Instanz austauschen. So sind Einsparungen von bis zu 30 % möglich.
  - SQL-Datenbank bietet verschiedene Sicherheitsfeatures, darunter Always Encrypted, dynamische Datenmaskierung und Sicherheit bzw. Bedrohungserkennung auf Zeilenebene.
- Zudem hat Contoso entschieden, die App-Webebene mit Azure DevOps Services in den Windows-Container zu konvertieren.
  - Die App wird mit Azure Service Fabric bereitgestellt und das Windows-Containerimage aus der Azure Container Registry (ACR) gepullt.
  - Ein Prototyp für die Erweiterung der App um die Standpunktanalyse wird als weiterer Dienst in Service Fabric, verbunden mit Cosmos DB, implementiert. Dieser liest Informationen aus Tweets und zeigt sie in der App an.
- Zur Implementierung einer DevOps-Pipeline verwendet Contoso Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys. Automatisierte Builds und Releases werden verwendet, um Code zu erstellen und in Azure Container Registry sowie in Azure Service Fabric bereitzustellen.

    ![Szenarioarchitektur](./media/contoso-migration-rearchitect-container-sql/architecture.png)

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | Der Code der SmartHotel360-App muss für die Migration zu Azure Service Fabric geändert werden. Der Aufwand ist jedoch minimal, da die Service Fabric-SDK Tools für die Änderungen verwendet werden.<br/><br/> Durch den Umstieg auf Service Fabric kann Contoso mit der Entwicklung von Microservices beginnen, um die App im Laufe der Zeit schnell und ohne Gefahr für die ursprüngliche Codebasis zu erweitern.<br/><br/> Windows-Container bieten die gleichen Vorteile wie Container im Allgemeinen. Sie verbessern die Flexibilität, die Portabilität und die Steuerungsmöglichkeiten.<br/><br/> Contoso kann seine Investition in die Software Assurance mit dem Azure-Hybridvorteil für SQL Server und Windows Server nutzen.<br/><br/> Nach der Migration ist die Unterstützung von Windows Server 2008 R2 nicht mehr erforderlich. [Weitere Informationen](https://support.microsoft.com/lifecycle)<br/><br/> Contoso kann die Webebene der App mit mehreren Instanzen konfigurieren, sodass sie kein Single Point of Failure mehr ist.<br/><br/> Sie ist nicht mehr auf das veraltete SQL Server 2008 R2 angewiesen.<br/><br/> SQL-Datenbank unterstützt die technischen Anforderungen von Contoso. Die Administratoren von Contoso haben die lokale Datenbank mithilfe des Datenmigrations-Assistenten bewertet und festgestellt, dass sie kompatibel ist.<br/><br/> SQL-Datenbank verfügt über eine integrierte Fehlertoleranz, die Contoso nicht einrichten muss. Dadurch wird sichergestellt, dass die Datenschicht kein Single Point of Failover mehr ist.
**Nachteile** | Container sind komplexer als andere Migrationsoptionen. Die Lernkurve bei Containern könnte für Contoso ein Problem darstellen. Der Grad der Komplexität steigt und bietet trotz der Kurve einen hohen Nutzen.<br/><br/> Das Betriebsteam von Contoso muss eingearbeitet werden, um Azure, Container und Microservices für die App verstehen und unterstützen zu können.<br/><br/> Wenn Contoso anstelle des Azure Database Migration Service den Datenmigrations-Assistenten zur Migration der Datenbank verwendet, verfügt das Unternehmen nicht über die entsprechende Infrastruktur für die Migration umfangreicher Datenbanken.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt den Azure Service Fabric-Cluster für Windows bereit.

1. Das Unternehmen stellt eine Azure SQL-Instanz bereit und migriert die SmartHotel360-Datenbank zu dieser Instanz.

1. Contoso konvertiert die VM auf Webebene mithilfe der Service Fabric SDK-Tools in einen Docker-Container.

1. Anschließend verknüpft das Unternehmen den Service Fabric-Cluster mit der ACR-Instanz und stellt die App über Azure Service Fabric bereit.

    ![Migrationsprozess](./media/contoso-migration-rearchitect-container-sql/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[Datenmigrations-Assistent (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Bewertet und erkennt Kompatibilitätsprobleme, die sich auf die Funktion der Datenbank in Azure auswirken können. Der DMA bewertet die Featureparität zwischen SQL-Quellen und -Zielen, und empfiehlt Verbesserungen der Leistung und Zuverlässigkeit. | Sie können das Tool kostenlos herunterladen.
[Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database) | Bietet einen intelligenten, vollständig verwalteten Dienst für relationale Clouddatenbanken. | Die Kosten ergeben sich durch Features, Durchsatz und Größe. [Weitere Informationen](https://azure.microsoft.com/pricing/details/sql-database/managed)
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Speichert Images für alle Arten von Containerbereitstellungen. | Die Kosten ergeben sich aus Features, Speicher und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/container-registry)
[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) | Dient zum Erstellen und Betreiben skalierbarer, verteilter Always On-Apps. | Die Kosten ergeben sich aus Größe, Standort und Dauer der Computeknoten. [Weitere Informationen](https://azure.microsoft.com/pricing/details/service-fabric)
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Stellt die Pipeline für Continuous Integration und Continuous Deployment (CI/CD) für die App-Entwicklung bereit. Die Pipeline beginnt bei einem Git-Repository für die Verwaltung von App-Code, einem Buildsystem zum Erstellen von Paketen und anderen Buildartefakten sowie einem Releaseverwaltungssystem zum Bereitstellen von Änderungen in Entwicklungs-, Test- und Produktionsumgebungen.

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenarios benötigt Contoso Folgendes:

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Abonnements wurden in einem früheren Artikel dieser Reihe erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.
**Azure-Infrastruktur** | Contoso hat bereits eine Azure-Infrastruktur eingerichtet. Weitere Informationen finden Sie [hier](./contoso-migration-infrastructure.md).
**Voraussetzungen für Entwickler** | Contoso benötigt die folgenden Tools auf einer Entwicklerarbeitsstation:<br/><br/> - [Visual Studio 2017 Community Edition: Version 15.5](https://www.visualstudio.com)<br/><br/> – .NET-Workload aktiviert.<br/><br/> - [Git](https://git-scm.com)<br/><br/> - [Service Fabric-SDK-Version 3.0 oder höher](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)<br/><br/> - [Docker CE (Windows 10) oder Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) festgelegt für die Verwendung von Windows-Containern.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

So führt Contoso die Migration durch:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen einer SQL-Datenbankinstanz in Azure.** Contoso stellt eine SQL-Instanz in Azure bereit. Nach der Migration der Web-Front-End-VM zu einem Azure-Container wird die Containerinstanz mit dem Web-Front-End der App auf diese Datenbank zeigen.
> - **Schritt 2: Erstellen einer ACR-Instanz (Azure Container Registry).** Contoso stellt eine professionelle Containerregistrierung für die Docker-Containerimages bereit.
> - **Schritt 3: Bereitstellen von Azure Service Fabric.** ES wird ein Service Fabric-Cluster bereitgestellt.
> - **Schritt 4: Verwalten von Service Fabric-Zertifikaten.** Contoso richtet Zertifikate für den Azure DevOps Services-Zugriff auf den Cluster ein.
> - **Schritt 5: Migrieren der Datenbank mit dem DMA.** Es migriert die App-Datenbank mit dem Datenmigrations-Assistenten.
> - **Schritt 6: Einrichten von Azure DevOps Services.** Contoso richtet ein neues Projekt in Azure DevOps Services ein und importiert den Code in das Git-Repository.
> - **Schritt 7: Konvertieren der App.** Contoso konvertiert die App mithilfe von Azure DevOps und SDK-Tools in einen Container.
> - **Schritt 8: Einrichten von Build und Release.** Contoso richtet die Build- und Releasepipelines ein, um die App zu erstellen und in ACR sowie im Service Fabric-Cluster zu veröffentlichen.
> - **Schritt 9: Erweitern der App.** Die veröffentlichte App wird von Contoso erweitert, um die Vorteile von Azure-Funktionen zu nutzen, und anschließend mithilfe der Pipeline erneut in Azure veröffentlicht.

## <a name="step-1-provision-an-azure-sql-database"></a>Schritt 1: Bereitstellen einer Azure SQL-Datenbank-Instanz

Die Contoso-Administratoren stellen eine Azure SQL-Datenbank bereit.

1. Sie entscheiden sich dafür, eine **SQL-Datenbank**-Instanz in Azure zu erstellen.

    ![Bereitstellen von SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

1. Das Unternehmen gibt einen Datenbanknamen an, der mit der Datenbank übereinstimmt, die auf der lokalen VM (**SmartHotel.Registration**) ausgeführt wird. Die Datenbank wird dann in der ContosoRG-Ressourcengruppe platziert. Dies ist die Ressourcengruppe, die das Unternehmen für die Produktionsressourcen in Azure verwendet.

    ![Bereitstellen von SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

1. Das fiktive Unternehmen richtet eine neue SQL Server-Instanz (**sql-smarthotel-eus2**) in der primären Region ein.

    ![Bereitstellen von SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

1. Den Tarif legt das Unternehmen gemäß seiner Server- und Datenbankanforderungen fest. Zudem entscheidet es sich, Geld mit dem Azure-Hybridvorteil zu sparen, da es bereits über eine SQL Server-Lizenz verfügen.

1. Zur Größenanpassung nutzt es das auf virtuellen Kernen basierende Kaufmodell und legt die Grenzwerte für die erwarteten Anforderungen fest.

    ![Bereitstellen von SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

1. Dann erstellt Contoso die Datenbankinstanz.

    ![Bereitstellen von SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

1. Nach dem Erstellen der Instanz öffnet das Unternehmen die Datenbank und notiert sich Details, die es für die Migration mit dem Datenmigrations-Assistenten benötigt.

    ![Bereitstellen von SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)

**Benötigen Sie weitere Hilfe?**

- [Erhalten Sie Hilfe](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) bei der Bereitstellung einer SQL-Datenbank-Instanz.
- [Erfahren Sie mehr](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) zu Ressourcengrenzwerten des auf virtuellen Kernen basierenden Kaufmodells.

## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a>Schritt 2: Erstellen einer ACR und Bereitstellen eines Azure-Containers

Der Azure-Container wird mithilfe der exportierten Dateien aus der Web-VM erstellt. Der Container wird in der Azure Container Registry (ACR) gespeichert.

1. Die Administratoren von Contoso erstellen im Azure-Portal eine Container Registry-Instanz.

     ![Containerregistrierung](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

1. Das Unternehmen gibt einen Namen für die Registrierung (**contosoacreus2**) an und platziert sie in der primären Region, in der für seine Infrastrukturressourcen verwendeten Ressourcengruppe. Dann aktiviert es den Zugriff für Administratorbenutzer, und es legt sie als Premium-SKU fest, um die Georeplikation nutzen zu können.

    ![Containerregistrierung](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)

## <a name="step-3-provision-azure-service-fabric"></a>Schritt 3: Bereitstellen von Azure Service Fabric

Der SmartHotel360-Container wird im Azure Service Fabric-Cluster ausgeführt. Die Administratoren von Contoso gehen wie folgt vor, um den Service Fabric-Cluster zu erstellen:

1. Erstellen einer Service Fabric-Ressource aus dem Azure Marketplace.

     ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

1. Unter **Grundlagen** gibt Contoso einen eindeutigen DS-Namen für den Cluster sowie Anmeldeinformationen für den Zugriff auf die lokale VM an. Es platziert die Ressource in der Produktionsressourcengruppe (**ContosoRG**) in der primären Region „USA, Osten 2“.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png)

1. In **Knotentypkonfiguration** gibt das Unternehmen einen Knotentypnamen, Einstellungen zur Dauerhaftigkeit, VM-Größe und App-Endpunkte ein.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png)

1. In **Schlüsseltresor erstellen** wird ein neuer Schlüsseltresor in der Infrastrukturressourcengruppe erstellt, in der das Zertifikat gespeichert wird.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png)

1. In **Zugriffsrichtlinien** aktiviert das Unternehmen den Zugriff auf virtuelle Computer für die Bereitstellung des Schlüsseltresors.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png)

1. Es gibt einen Namen für das Zertifikat an.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png)

1. Auf der Seite mit der Zusammenfassung wird der Link kopiert, der zum Herunterladen des Zertifikats benötigt wird. Dies ist erforderlich, um eine Verbindung mit dem Service Fabric-Cluster herzustellen.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png)

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png)

1. Nach erfolgreicher Validierung stellt Contoso den Cluster bereit.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png)

1. Mit dem Assistenten zum Importieren von Zertifikaten importiert das fiktive Unternehmen das heruntergeladene Zertifikat in die Entwicklercomputer. Das Zertifikat wird zum Authentifizieren beim Cluster verwendet.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png)

1. Nachdem der Cluster bereitgestellt ist, wird eine Verbindung mit dem Service Fabric-Cluster-Explorer hergestellt.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png)

1. Contoso muss das richtige Zertifikat auswählen.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png)

1. Der Service Fabric Explorer wird geladen, und der Contoso-Administrator kann den Cluster verwalten.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png)

## <a name="step-4-manage-service-fabric-certificates"></a>Schritt 4: Verwalten von Service Fabric-Zertifikaten

Contoso benötigt Clusterzertifikate, um Azure DevOps Services den Zugriff auf den Cluster zu ermöglichen. Diese werden von den Contoso-Administratoren eingerichtet.

1. Dazu navigieren sie im Azure-Portal zum Schlüsseltresor.

1. Sie öffnen die Zertifikate und kopieren den Fingerabdruck des Zertifikats, das im Rahmen des Bereitstellungsprozesses erstellt wurde.

    ![Kopieren des Fingerabdrucks](./media/contoso-migration-rearchitect-container-sql/cert1.png)

1. Der Fingerabdruck wird für später in eine Textdatei kopiert.

1. Anschließend fügen sie ein Clientzertifikat hinzu, das als Administratorclientzertifikat für den Cluster konfiguriert wird. Dadurch kann Azure DevOps Services eine Verbindung mit dem Cluster für die App-Bereitstellung in der Releasepipeline herstellen. Hierzu öffnen Sie den Schlüsseltresor im Portal und wählen **Zertifikate** > **Generieren/Importieren** aus.

    ![Generieren des Clientzertifikats](./media/contoso-migration-rearchitect-container-sql/cert2.png)

1. Sie geben den Namen des Zertifikats ein und geben unter **Antragsteller** einen Distinguished Name (X.509) an.

     ![Zertifikatname](./media/contoso-migration-rearchitect-container-sql/cert3.png)

1. Das erstellte Zertifikat laden sie lokal im PFX-Format herunter.

     ![Herunterladen des Zertifikats](./media/contoso-migration-rearchitect-container-sql/cert4.png)

1. Danach navigieren Sie wieder zur Zertifikatliste im Schlüsseltresor und kopieren den Fingerabdruck des soeben erstellen Clientzertifikats. Diesen speichern Sie in der Textdatei.

     ![Fingerabdruck des Clientzertifikats](./media/contoso-migration-rearchitect-container-sql/cert5.png)

1. Für die Azure DevOps Services-Bereitstellung muss der Base64-Wert des Zertifikats ermittelt werden. Diesen Schritt führen sie mithilfe von PowerShell auf der lokalen Entwicklerarbeitsstation aus. Die Ausgabe fügen sie für später in eine Textdatei ein.

    ```powershell
    [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx"))
    ```

     ![Base64-Wert](./media/contoso-migration-rearchitect-container-sql/cert6.png)

1. Abschließend fügen sie das neue Zertifikat dem Service Fabric-Cluster hinzu. Hierzu öffnen sie den Cluster im Portal und wählen **Sicherheit** aus.

     ![Hinzufügen des Clientzertifikats](./media/contoso-migration-rearchitect-container-sql/cert7.png)

1. Sie wählen **Hinzufügen** > **Administratorclient** aus und fügen den Fingerabdruck des neuen Clientzertifikats ein. Anschließend wählen sie **Hinzufügen** aus. Der Vorgang kann bis zu 15 Minuten dauern.

     ![Hinzufügen des Clientzertifikats](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a>Schritt 5: Migrieren der Datenbank mit dem DMA

Jetzt können die Administratoren von Contoso die SmartHotel360-Datenbank mit dem DMA migrieren.

### <a name="install-dma"></a>Installieren des DMA

1. Es lädt das Tool aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) auf die lokale SQL Server-VM (**SQLVM**) herunter.

1. Es führt das Setup (DownloadMigrationAssistant.msi) auf der VM aus.

1. Auf der Seite **Fertigstellen** wählen sie **Launch Microsoft Data Migration Assistant** (Microsoft-Datenmigrations-Assistenten starten) aus, bevor sie den Assistenten beenden.

### <a name="configure-the-firewall"></a>Konfigurieren der Firewall

Für die Verbindungsherstellung mit Azure SQL-Datenbank richten die Administratoren von Contoso eine Firewallregel ein, um den Zugriff zuzulassen.

1. In den Eigenschaften für **Firewall und virtuelle Netzwerke** für die Datenbank gewährt Contoso Zugriff auf Azure-Dienste, und es fügt eine Regel für die Client-IP-Adresse der lokalen SQL Server-VM hinzu.

1. Es wird eine Firewallregel auf Serverebene erstellt.

    ![Firewall](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

**Benötigen Sie weitere Hilfe?**

[Erfahren Sie mehr](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) über das Erstellen und Verwalten von Firewallregeln für Azure SQL-Datenbank.

### <a name="migrate"></a>Migrieren

Als Nächstes migrieren die Administratoren von Contoso die Datenbank.

1. Im DMA erstellt das Unternehmen ein neues Projekt (**SmartHotelDB**) und wählt anschließend **Migration** aus.

1. Als Quellservertyp wird **SQL Server** und als Ziel **Azure SQL-Datenbank** ausgewählt.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

1. In den Migrationsdetails fügt das Unternehmen **SQLVM** als Quellserver und die **SmartHotel.Registration**-Datenbank als Ziel hinzu.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

1. Ein Fehler wird angezeigt, der anscheinend mit der Authentifizierung zusammenhängt. Beim Ermitteln der Ursache wird jedoch festgestellt, dass das Problem durch den Punkt (.) im Datenbanknamen verursacht wird. Daher wurde beschlossen, eine neue SQL-Datenbank-Instanz mit dem Namen **SmartHotel-Registration** bereitzustellen, um das Problem zu beheben. Beim erneuten Ausführen des DMA können sie **SmartHotel-Registration** auswählen, und der Assistent kann fortgesetzt werden.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

1. Unter **Objekte auswählen** wählt das Unternehmen die Datenbanktabellen aus und generiert ein SQL-Skript.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

1. Nachdem das Skript durch den DMA erstellt wurde, wählen Sie **Schema bereitstellen** aus.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

1. Der DMA bestätigt, dass die Bereitstellung erfolgreich war.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

1. Jetzt kann mit der Migration begonnen werden.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

1. Nach Abschluss der Migration kann Contoso überprüfen, ob die Datenbank auf der Azure SQL-Datenbank-Instanz ausgeführt wird.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

1. Die zusätzliche SQL-Datenbank-Instanz **SmartHotel.Registration** wird von Contoso im Azure-Portal gelöscht.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)

## <a name="step-6-set-up-azure-devops-services"></a>Schritt 6: Einrichten von Azure DevOps Services

Contoso muss die DevOps-Infrastruktur und die Pipelines für die Anwendung erstellen. Hierzu erstellen die Administratoren von Contoso ein neues Azure DevOps-Projekt, importieren ihren Code und erstellen anschließend die Build- und Releasepipelines.

1. Im Azure DevOps-Konto von Contoso erstellen sie ein neues Projekt (**ContosoSmartHotelRearchitect**) und verwenden anschließend **Git** für die Versionskontrolle.
![Neues Projekt](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

1. Sie importieren das Git-Repository, das derzeit ihren App-Code enthält. Der Code befindet sich in einem [öffentlichen Repository](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) und kann heruntergeladen werden.

    ![Herunterladen des App-Codes](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

1. Nach dem Importieren des Codes verknüpfen sie Visual Studio mit dem Repository und klonen den Code mithilfe von Team Explorer.

1. Nachdem das Repository auf dem Entwicklercomputer geklont wurde, öffnen sie die Projektmappendatei für die App. Die Datei enthält jeweils ein eigenes Projekt für die Web-App und den WCF-Dienst.

    ![Projektmappendatei](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a>Schritt 7: Konvertieren der App in einen Container

Bei der lokalen App handelt es sich um eine herkömmliche dreischichtige App:

- Sie enthält WebForms und einen WCF-Dienst zur Verbindung mit SQL Server.
- Sie verwendet Entity Framework zur Integration mit den Daten in der SQL-Datenbank-Instanz, die über einen WCF-Dienst verfügbar gemacht wird.
- Die WebForms-Anwendung interagiert mit dem WCF-Dienst.

Die Administratoren von Contoso konvertieren die App mit Visual Studio und den SDK-Tools wie folgt in einen Container:

1. Sie prüfen unter Verwendung von Visual Studio die geöffnete Projektmappendatei (SmartHotel.Registration.sln) im Verzeichnis **SmartHotel360-interne-Buchung-Apps\src\Registration** des lokalen Repositorys. Es werden zwei Apps angezeigt. „SmartHotel.Registration.Web“ (Web-Front-End) und „SmartHotel.Registration.WCF“ (WCF-Dienst).

    ![Container](./media/contoso-migration-rearchitect-container-sql/container2.png)

1. Contoso klickt mit der rechten Maustaste auf die Web-App > **Hinzufügen** > **Unterstützung für Containerorchestrator**.

1. In **Unterstützung für Containerorchestrator hinzufügen** wird **Service Fabric** ausgewählt.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container3.png)

1. Sie wiederholen den Vorgang für die App „SmartHotel.Registration.WCF“.

1. Als Nächstes überprüfen sie, wie sich die Lösung geändert hat.

    - Die neue App heißt nun **SmartHotel.RegistrationApplication/** .
    - Sie umfasst zwei Dienste: **SmartHotel.Registration.WCF** und **SmartHotel.Registration.Web**.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container4.png)

1. Die Docker-Datei wurde von Visual Studio erstellt, und die erforderlichen Bilder wurden lokal auf den Entwicklercomputer gezogen.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container5.png)

1. Es wird eine Manifestdatei (**ServiceManifest.xml**) von Visual Studio erstellt und geöffnet. Diese Datei informiert Service Fabric darüber, wie der Container bei der Bereitstellung in Azure konfiguriert werden soll.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container6.png)

1. Eine weitere Manifestdatei (**ApplicationManifest.xml) enthält die Konfigurationsanwendungen für die Container.

    ![Container](./media/contoso-migration-rearchitect-container-sql/container7.png)

1. Sie öffnen die Datei **ApplicationParameters/Cloud.xml** und aktualisieren die Verbindungszeichenfolge, um die App mit der Azure SQL-Datenbank zu verknüpfen. Die Verbindungszeichenfolge kann in der Datenbank über das Azure-Portal ermittelt werden.

    ![Verbindungszeichenfolge](./media/contoso-migration-rearchitect-container-sql/container8.png)

1. Sie committen den aktualisierten Code und pushen ihn an Azure DevOps Services.

    ![Commit](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a>Schritt 8: Build- und Releasepipelines in Azure DevOps Services

Als Nächstes konfigurieren die Contoso-Administratoren Azure DevOps Services für die Durchführung des Build- und Releasevorgangs, um die DevOps-Praktiken umzusetzen.

1. Dazu wählen sie in Azure DevOps Services **Build und Release** > **Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

1. Sie wählen **Azure DevOps Services Git** und das entsprechende Repository aus.

    ![Git und Repository](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

1. Unter **Vorlage auswählen** wählen sie Fabric mit Docker-Unterstützung aus.

     ![Fabric und Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)

1. Sie ändern das Aktionstag von Images in **Build an image** (Imageerstellung) und konfigurieren die Aufgabe für die Verwendung der bereitgestellten ACR-Instanz.

     ![Registrierung](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

1. In der Aufgabe zum **Pushen von Images** konfigurieren sie das Image, das an die ACR-Instanz gepusht werden soll, und wählen aus, dass das neueste Tag eingeschlossen werden soll.

1. Unter **Trigger** aktivieren sie Continuous Integration und fügen den Masterbranch hinzu.

    ![Trigger](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

1. Sie wählen **Speichern und in Warteschlange einreihen** aus, um einen Buildvorgang zu starten.

1. Nach erfolgreicher Ausführung des Buildvorgangs wenden sie sich der Releasepipeline zu. Dazu wählen sie in Azure DevOps Services **Releases** > **Neue Pipeline** aus.

    ![Releasepipeline](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)

1. Sie wählen die Vorlage **Azure Service Fabric-Bereitstellung** aus und benennen die Phase (**SmartHotelSF**).

    ![Environment](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

1. Sie geben einen Pipelinenamen (**ContosoSmartHotel360Rearchitect**) an. Für die Phase wählen sie **1 Auftrag, 1 Aufgabe** aus, um die Service Fabric-Bereitstellung zu konfigurieren.

    ![Phase und Aufgabe](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

1. Als Nächstes wählen sie **Neu** aus, um eine neue Clusterverbindung hinzuzufügen.

    ![Neue Verbindung](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

1. Unter **Add Service Fabric service connection** (Service Fabric-Dienstverbindung hinzufügen) konfigurieren sie die Verbindung und die Authentifizierungseinstellungen, die von Azure DevOps Services zum Bereitstellen der App verwendet werden. Der Clusterendpunkt kann im Azure-Portal ermittelt werden, und sie fügen **tcp://** als Präfix hinzu.

1. Die gesammelten Zertifikatinformationen werden unter **Fingerabdruck des Serverzertifikats** und **Clientzertifikat** eingegeben.

    ![Zertifikat](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

1. Sie wählen sie die Pipeline und anschließend die Option zum **Hinzufügen eines Artefakts** aus.

     ![Artefakt](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

1. Sie wählen das Projekt und die Buildpipeline (neueste Version) aus.

     ![Entwickeln](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

1. Beachten Sie das Blitzsymbol des Artefakts.

     ![Artefaktstatus](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

1. Beachten Sie außerdem, dass der Continuous Deployment-Trigger aktiviert ist.
   ![Continuous Deployment aktiviert](./media/contoso-migration-rearchitect-container-sql/pipeline14.png)

1. Sie wählen **Speichern** > **Release erstellen** aus.

    ![Release](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

1. Nach Abschluss der Bereitstellung wird SmartHotel360 in Service Fabric ausgeführt.

    ![Veröffentlichen](./media/contoso-migration-rearchitect-container-sql/publish4.png)

1. Um eine Verbindung mit der App herzustellen, leiten sie den Datenverkehr an die öffentliche IP-Adresse des Azure-Lastenausgleichs weiter, der den Service Fabric-Knoten vorgelagert ist.

    ![Veröffentlichen](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a>Schritt 9: Erweitern der App und erneutes Veröffentlichen

Nachdem die SmartHotel360-App und die SmartHotel360-Datenbank in Azure ausgeführt werden, möchte Contoso die App erweitern.

- Die Contoso-Entwickler erstellen gerade den Prototyp einer neuen .NET Core-Anwendung, die im Service Fabric-Cluster ausgeführt werden soll.
- Die App wird dann zum Pullen von Stimmungsdaten aus Cosmos DB verwendet.
- Diese Daten werden in Form von Tweets vorliegen, die mit einer serverlosen Azure-Funktion und der Azure Cognitive Services-Textanalyse-API verarbeitet werden.

### <a name="provision-azure-cosmos-db"></a>Bereitstellen von Azure Cosmos DB

Im ersten Schritt erstellen die Administratoren von Contoso eine Azure-Cosmos-Datenbank.

1. Dabei wird eine Azure Cosmos DB-Ressource aus dem Azure Marketplace erstellt.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend1.png)

1. Contoso gibt einen Datenbanknamen (**contosmarthotel**) an, wählt die SQL-API aus und platziert die Ressource in der Produktionsressourcengruppe in der primären Region „USA, Osten 2“.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend2.png)

1. In **Erste Schritte** wählt das Unternehmen **Daten-Explorer** aus und fügt eine neue Sammlung hinzu.

1. In **Sammlung hinzufügen** gibt esIDs an und legt die Speicherkapazität und den Durchsatz fest.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend3.png)

1. Im Portal öffnet Contoso die neue Datenbank > **Sammlung** > **Dokumente** und wählt **Neues Dokument** aus.

1. Der folgende JSON-Code wird in das Dokumentfenster eingefügt. Dies sind Beispieldaten in Form eines einzelnen Tweets.

    ```json
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500,
            "hashtags": [
                ""
            ]
    }
    ```

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend4.png)

1. Contoso lokalisiert den Cosmos DB-Endpunkt und den Authentifizierungsschlüssel. Diese werden in der App verwendet, um sich mit der Sammlung zu verbinden. In der Datenbank wählt Contoso **Schlüssel** aus und kopiert die URI und den Primärschlüssel nach Notepad.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a>Aktualisieren der Standpunkt-App

Nach der Bereitstellung der Cosmos DB-Instanz können die Administratoren von Contoso die App konfigurieren, um eine Verbindung damit herzustellen.

1. In Visual Studio öffnet das Unternehmen im Projektmappen-Explorer die Datei ApplicationModern\ApplicationParameters\cloud.xml.

    ![Standpunkt-App](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

1. Die folgenden beiden Parameter werden angegeben:

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Standpunkt-App](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a>Erneutes Veröffentlichen der App

Nach dem Erweitern der App veröffentlichen die Administratoren von Contoso die App mithilfe der Pipeline erneut in Azure.

1. Sie committen ihren Code und pushen ihn an Azure DevOps Services. Dadurch werden die Build- und Releasepipelines initiiert.

1. Nach Abschluss der Erstellung und Bereitstellung wird SmartHotel360 in Service Fabric ausgeführt. Die drei Dienste werden nun in der Service Fabric-Verwaltungskonsole angezeigt.

    ![Erneut veröffentlichen](./media/contoso-migration-rearchitect-container-sql/republish3.png)

1. Sie können sich nun durch die Dienste klicken und sich vergewissern, dass die SentimentIntegration-App aktiv ist und ausgeführt wird.

    ![Erneut veröffentlichen](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die folgenden Schritte zur Bereinigung ausführen:

- Entfernen der lokalen VMs aus dem vCenter-Bestand.
- Entfernen der VMs aus lokalen Sicherungsaufträgen.
- Aktualisieren der internen Dokumentation zur Anzeige der neuen Speicherorte für die App SmartHotel360 Anzeigen, dass die Datenbank in Azure SQL-Datenbank und das Front-End in Service Fabric ausgeführt wird.
- Überprüfen sämtlicher Ressourcen, die mit den außer Betrieb genommenen VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Die Administratoren von Contoso müssen die Sicherheit der neuen Datenbank **SmartHotel-Registration** gewährleisten. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Insbesondere sollte es den Container aktualisieren, sodass dieser SSL mit Zertifikaten verwendet.
- Zum Schutz von Geheimnissen für die Service Fabric-Apps sollte die Verwendung des Schlüsseltresors in Erwägung gezogen werden. [Weitere Informationen](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management)

### <a name="backups"></a>Backups

- Contoso muss die Sicherungsanforderungen für Azure SQL-Datenbank überprüfen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)
- Die Administratoren von Contoso sollten die Implementierung von Failovergruppen in Betracht ziehen, um ein regionales Failover für die Datenbank bereitzustellen. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)
- Die geografische Replikation für die Premium-SKU von ACR kann genutzt werden. [Weitere Informationen](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication)
- Contoso muss den Einsatz der Web-App in der Hauptregion „USA, Osten 2“ und „USA, Mitte“ in Erwägung ziehen, wenn die Web-App für Container verfügbar wird. Die Administratoren von Contoso können Traffic Manager konfigurieren, um ein Failover bei regionalen Ausfällen sicherzustellen.
- Cosmos DB führt automatisch Sicherungen durch. Weitere Informationen zu diesem Prozess finden Sie [hier](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf der [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über EA verrechnet.
- Contoso aktiviert Azure Cost Management. Es ist durch Cloudyn lizenziert, ein Tochterunternehmen von Microsoft. Dabei handelt es sich um eine Kostenverwaltungslösung mit mehreren Clouds, die Ihnen das Verwenden und Verwalten von Azure und anderen Cloudressourcen erleichtert. [Erfahren Sie mehr](https://docs.microsoft.com/azure/cost-management/overview) über die Azure Cost Management.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat Contoso die SmartHotel360-App in Azure umgestaltet, indem der Front-End-VM der App zu Service Fabric migriert wurde. Die App-Datenbank wurde zu einer Azure SQL-Datenbank-Instanz migriert.
