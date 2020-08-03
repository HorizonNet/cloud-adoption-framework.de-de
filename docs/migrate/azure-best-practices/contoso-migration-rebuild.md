---
title: Erneutes Erstellen einer lokalen Anwendung in Azure
description: In diesem Artikel erfahren Sie, wie Contoso mithilfe von Azure App Service, Azure Kubernetes Service, Azure Cosmos DB, Azure Functions und Azure Cognitive Services eine Anwendung in Azure neu erstellt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 7/1/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 373d4216eb9259bd49a85c4d1dd6466c4f33388d
ms.sourcegitcommit: 65e8d2fc3ef31f2bb11a50f7c7a2d1eb116a6632
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87255096"
---
<!-- docsTest:ignore "Enable .NET" SmartHotel360 SmartHotel360-Backend Pet.Checker contoso-datacenter git aks PetCheckerFunction -->

<!-- cSpell:ignore givenscj SQLVM WEBVM contosohost vcenter contosodc smarthotel contososmarthotel smarthotelcontoso smarthotelpetchecker petchecker smarthotelakseus smarthotelacreus smarthotelpets kubectl contosodevops visualstudio azuredeploy cloudapp smarthotelsettingsurl appsettings -->

# <a name="rebuild-an-on-premises-application-in-azure"></a>Erneutes Erstellen einer lokalen Anwendung in Azure

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso als Teil der Migration zu Azure eine zweistufige Windows .NET-Anwendung neu erstellt, die auf virtuellen VMware-Computern (VMs) ausgeführt wird. Contoso migriert die Front-End-VM zu einer Azure App Service-Web-App. Contoso erstellt das Back-End der Anwendung mithilfe von Microservices, die für Container bereitgestellt werden, die von Azure Kubernetes Service (AKS) verwaltet werden. Die Website interagiert mit Azure Functions zum Bereitstellen der Funktionalität für Fotos von Haustieren.

Die in diesem Beispiel verwendete SmartHotel360-Anwendung wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam von Contoso hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was sie mit dieser Migration erreichen möchten:

- **Unternehmenswachstum.** Contoso wächst und möchte für seine Kunden differenzierte Funktionen auf seinen Websites bereitstellen.
- **Mehr Flexibilität.** Contoso muss schneller reagieren können als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss das Contoso-IT-Team Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat folgende Anwendungsanforderungen für diese Migration gestellt. Anhand dieser Anforderungen wird die beste Migrationsmethode bestimmt:

- Die Anwendung muss in Azure so wichtig bleiben, wie sie es heute bereits lokal ist. Sie sollte reibungslos laufen und sich mühelos skalieren lassen.
- Die Anwendung sollte keine IaaS-Komponenten (Infrastructure-as-a-Service) verwenden. Sie sollte für die Verwendung von PaaS-Diensten (Platform as a Service) oder serverlosen Diensten ausgelegt sein.
- Die Builds der Anwendung sollten in Clouddiensten ausgeführt werden, und Container sollten sich in einer privaten, unternehmensweiten Registrierung in der Cloud befinden.
- Der API-Dienst, der für Fotos von Haustieren verwendet wird, sollte in der Praxis präzise und zuverlässig sein, da die von der Anwendung getroffenen Entscheidungen in den Hotels berücksichtigt werden müssen. Haustiere, denen der Zutritt erlaubt ist, dürfen in den Hotels bleiben.
- Um die Anforderungen für eine DevOps-Pipeline zu erfüllen, verwendet Contoso für die Quellcodeverwaltung ein Git-Repository in Azure Repos. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service, Azure Functions und AKS bereitgestellt.
- Für Microservices im Back-End und für die Website im Front-End sind separate CI/CD-Pipelines (Continuous Integration/Continuous Development) erforderlich.
- Die Back-End-Dienste und die Front-End-App haben unterschiedliche Releasezyklen. Contoso stellt zwei verschiedene Pipelines bereit, um diese Anforderung zu erfüllen.
- Contoso benötigt eine Verwaltungsgenehmigung für die gesamte Front-End-Websitebereitstellung, die von der CI/CD-Pipeline bereitgestellt werden muss.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-application"></a>Aktuelle Anwendung

- Die lokale Anwendung SmartHotel360 ist auf zwei VMs aufgeteilt (`WEBVM` und `SQLVM`).
- Die VMs befinden sich auf dem VMware ESXi-Host `contosohost1.contoso.com` (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (`vcenter.contoso.com`) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (`contoso-datacenter`) mit einem lokalen Domänencontroller (`contosodc1`).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Das Front-End der Anwendung wird als Azure App Service-Web-App in der primären Azure-Region bereitgestellt.
- Eine Azure-Funktion bietet Uploads von Fotos von Haustieren, und die Website interagiert mit dieser Funktionalität.
- Die Funktion für Fotos von Haustieren verwendet die Maschinelles Sehen-API von Azure Cognitive Services zusammen mit Azure Cosmos DB.
- Das Back-End der Website wird mithilfe von Microservices erstellt. Diese Microservices werden in Containern bereitgestellt, die in AKS verwaltet werden.
- Container werden mithilfe von Azure DevOps erstellt und dann mithilfe von Push an Azure Container Registry übertragen.
- Vorerst stellt Contoso die Web-App und den Funktionscode mithilfe von Visual Studio manuell bereit.
- Contoso stellt Microservices mithilfe eines PowerShell-Skripts bereit, das Kubernetes-Befehlszeilentools aufruft.

    ![Abbildung der Szenarioarchitektur für die Migration zu Azure](./media/contoso-migration-rebuild/architecture.png)  
    _Abbildung 1: Szenarioarchitektur_

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Durch den Einsatz von PaaS- und serverlosen Lösungen für die End-to-End-Bereitstellung verkürzt sich die Verwaltungszeit, die Contoso aufwenden muss, um ein Vielfaches. <br><br> Die Migration zu einer auf Microservices basierenden Architektur bietet Contoso die Möglichkeit, die Lösung ganz einfach im Lauf der Zeit zu erweitern. <br><br> Neue Funktionalität kann online geschaltet werden, ohne dass vorhandene Codebasen von Lösungen beeinträchtigt werden. <br><br> Die Web-App wird mit mehreren Instanzen ohne Single Point of Failure konfiguriert. <br><br> Die automatische Skalierung wird aktiviert, damit die Anwendung unterschiedlich hohe Datenverkehrsvolumen verarbeiten kann. <br><br> Mit dem Wechsel zu PaaS-Diensten kann Contoso veraltete Lösungen, die unter dem Betriebssystem Windows Server 2008 R2 ausgeführt werden, außer Betrieb nehmen. <br><br> Azure Cosmos DB weist eine integrierte Fehlertoleranz auf, die keinen Konfigurationsaufwand seitens Contoso erfordert. Dies bedeutet, dass die Datenschicht kein Single Point of Failover mehr ist. |
| **Nachteile** | Container sind komplexer als andere Migrationsoptionen. Die Lernkurve könnte für Contoso ein Problem darstellen. Der Grad der Komplexität steigt und bietet trotz der Kurve einen hohen Nutzen. <br><br> Das Betriebsteam von Contoso muss eingearbeitet werden, um Azure, Container und Microservices für die Anwendung verstehen und unterstützen zu können. <br><br> Contoso hat noch nicht vollständig DevOps für die gesamte Lösung implementiert. Dies muss Contoso bei der Bereitstellung von Diensten für AKS, Azure Functions und Azure App Service berücksichtigen. |

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt Azure Container Registry, AKS und Azure Cosmos DB bereit.
2. Contoso stellt die Infrastruktur für die Bereitstellung einschließlich der Azure App Service-Web-App, eines Speicherkontos, Funktionen und einer API bereit.
3. Sobald die Infrastruktur eingerichtet ist, erstellt Contoso Microservicescontainerimages mithilfe von Azure DevOps, das diese Images mithilfe von Push an die Containerregistrierung überträgt.
4. Contoso stellt diese Microservices mithilfe eines PowerShell-Skripts in AKS bereit.
5. Abschließend stellt Contoso die Funktion und die Web-App bereit.

    ![Abbildung des Migrationsprozesses von der Vorbereitung bis zur Bereitstellung in der Cloud](./media/contoso-migration-rebuild/migration-process.png)  
    _Abbildung 2: Der Migrationsvorgang._

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
|---|---|---|
| [AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Vereinfacht die Verwaltung, die Bereitstellung und den Betrieb von Kubernetes. Nutzt einen vollständig verwalteten Orchestrierungsdienst für Kubernetes-Container. | AKS ist ein kostenloser Dienst. Sie zahlen nur für die VMs und die verbrauchten zugeordneten Speicher- und Netzwerkressourcen. [Weitere Informationen](https://azure.microsoft.com/pricing/details/kubernetes-service) |
| [Azure-Funktionen](https://azure.microsoft.com/services/functions) | Beschleunigt die Entwicklung mit einer ereignisbasierten, serverlosen Computeumgebung. Die Skalierung erfolgt bedarfsabhängig. | Nur verbrauchte Ressourcen müssen bezahlt werden. Der Plan wird basierend auf dem Ressourcenverbrauch und den Ausführungen pro Sekunde berechnet. [Weitere Informationen](https://azure.microsoft.com/pricing/details/functions) |
| [Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Speichert Images für alle Arten von Containerbereitstellungen. | Die Kosten basieren auf den Features, dem Speicher und der Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/container-registry) |
| [Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Es können schnell Web-Apps, mobile Apps und API-Apps auf Unternehmensniveau auf jeder Plattform erstellt, bereitgestellt und skaliert werden. | App Service-Pläne werden sekundengenau abgerechnet. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes:

| Requirements (Anforderungen) | Details |
| --- | --- |
| Azure-Abonnement | <li> Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <li> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <li> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| Azure-Infrastruktur | <li> Informieren Sie sich, [wie Contoso eine Azure-Infrastruktur einrichtet](./contoso-migration-infrastructure.md). |
| Voraussetzungen für Entwickler | Contoso benötigt die folgenden Tools auf einer Entwicklerarbeitsstation: <li>  [Visual Studio Community 2017, Version 15.5](https://visualstudio.microsoft.com) <li> .NET-Workload (aktiviert) <li> [Git-Client](https://git-scm.com) <li> [Azure PowerShell](https://azure.microsoft.com/downloads) <li> [Die Azure-CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) <li> [Docker Community Edition (Windows 10) oder Docker Enterprise Edition (Windows Server)](https://docs.docker.com/docker-for-windows/install) für die Verwendung von Windows-Containern festgelegt |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen von AKS und Azure Container Registry.** Contoso stellt mithilfe von PowerShell den verwalteten AKS-Cluster und die Containerregistrierung bereit.
> - **Schritt 2: Erstellen von Docker-Containern:** Contoso richtet CI (Continuous Integration) mithilfe von Azure DevOps für Docker-Container ein und überträgt die Container mithilfe von Push an die Containerregistrierung.
> - **Schritt 3: Bereitstellen von Back-End-Microservices:** Contoso stellt die restliche Infrastruktur bereit, die von Back-End-Microservices genutzt wird.
> - **Schritt 4: Bereitstellen der Front-End-Infrastruktur:** Contoso stellt die Front-End-Infrastruktur einschließlich Blob Storage für die Fotos von Haustieren, Azure Cosmos DB und der Maschinelles Sehen-API bereit.
> - **Schritt 5: Migrieren des Back-Ends:** Contoso stellt Microservices bereit und führt diese in AKS aus, um das Back-End zu migrieren.
> - **Schritt 6: Veröffentlichen des Front-Ends:** Contoso veröffentlicht die SmartHotel360-Anwendung in Azure App Service und die vom Haustierdienst aufzurufende Funktions-App.

## <a name="provision-back-end-resources"></a>Bereitstellen von Back-End-Ressourcen

Contoso-Administratoren führen ein Bereitstellungsskript zum Erstellen des Managed Kubernetes-Clusters mithilfe von AKS und Azure Container Registry aus. In den Anweisungen für diesen Abschnitt wird das GitHub-Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet. Das Repository enthält die gesamte Software für diesen Teil der Bereitstellung.

### <a name="ensure-that-prerequisites-are-met"></a>Sicherstellen der Erfüllung von Voraussetzungen

Vor Beginn stellen Contoso-Administratoren sicher, dass auf dem Entwicklungscomputer, den sie für die Bereitstellung verwenden, die erforderliche Software installiert ist. Sie klonen das Repository mithilfe von Git lokal auf dem Entwicklungscomputer:

`git clone https://github.com/Microsoft/SmartHotel360-Backend.git`

### <a name="provision-aks-and-azure-container-registry"></a>Bereitstellen von AKS und Azure Container Registry

Die Contoso-Administratoren stellen AKS und Azure Container Registry wie folgt bereit:

1. Sie öffnen den Ordner in Visual Studio Code und wechseln zum Verzeichnis `/deploy/k8s`, das das Skript `gen-aks-env.ps1` enthält.

2. Sie führen das Skript zum Erstellen des Managed Kubernetes-Clusters mithilfe von AKS und Azure Container Registry aus.

    ![Screenshot: AKS-Skript in Visual Studio Code](./media/contoso-migration-rebuild/aks1.png)  
    _Abbildung 3: Erstellen des verwalteten Kubernetes-Cluster._

3. Bei geöffneter Datei aktualisieren sie den $location-Parameter in `eastus2` und speichern die Datei.

    ![Screenshot: Aktualisieren des AKS-Parameters „$location“ auf „eastus2“](./media/contoso-migration-rebuild/aks2.png)  
    _Abbildung 4: Speichern der Datei._

4. Sie wählen die Optionen **Ansicht** > **Integriertes Terminal** aus, um das integrierte Terminal in Visual Studio Code zu öffnen.

    ![Screenshot: Option „Integriertes Terminal“](./media/contoso-migration-rebuild/aks3.png)  
    _Abbildung 5: Das Terminal in Visual Studio Code._

5. In dem in PowerShell integrierten Terminal melden sie sich bei Azure mit dem Befehl `Connect-AzureRmAccount` an. Weitere Informationen finden Sie unter [Erste Schritte mit Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

    ![Screenshot: Anmeldefenster für das integrierte PowerShell-Terminal](./media/contoso-migration-rebuild/aks4.png)  
    _Abbildung 6: Das integrierte PowerShell-Terminal._

6. Sie authentifizieren die Azure CLI, indem der Befehl `az login` ausgeführt wird und die Anweisungen für die Authentifizierung mithilfe eines Webbrowsers befolgt werden. Weitere Informationen zur Anmeldung mit der Azure CLI finden Sie [hier](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).

    ![Screenshot: Authentifizierungsfenster für die Azure CLI](./media/contoso-migration-rebuild/aks5.png)  
    _Abbildung 7: Authentifizieren der Azure CLI_

7. Sie führen den folgenden Befehl aus, mit dem der Ressourcengruppenname `ContosoRG`, der Name des AKS-Clusters `smarthotel-aks-eus2` und der neue Registrierungsname übergeben wird.

    `.\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2`

    ![Screenshot: „smarthotel“-Befehle im Bereich „Ressourcengruppe“](./media/contoso-migration-rebuild/aks6.png)  
    _Abbildung 8: Ausführung des Befehls._

8. Azure erstellt eine andere Ressourcengruppe, die die Ressourcen für den AKS-Cluster enthält.

    ![Screenshot: Ressourcengruppenerstellung](./media/contoso-migration-rebuild/aks7.png)  
    _Abbildung 9: Azure erstellt eine Ressourcengruppe._

9. Nachdem die Bereitstellung abgeschlossen ist, installieren sie das Befehlszeilentool `kubectl`. Das Tool ist bereits in Azure Cloud Shell installiert.

    `az aks install-cli`

10. Contoso überprüft die Verbindung mit dem Cluster, indem es den Befehl `kubectl get nodes` ausführt. Der Knoten weist den gleichen Namen wie die VM in der automatisch erstellten Ressourcengruppe auf.

    ![Screenshot: Überprüfung der Verbindung mit dem Cluster](./media/contoso-migration-rebuild/aks8.png)  
    _Abbildung 10: Die Verbindung mit dem Cluster wird überprüft._

11. Sie führen den folgenden Befehl zum Starten des Kubernetes-Dashboards aus:

    `az aks browse --resource-group ContosoRG --name smarthotelakseus2`

12. Eine Browserregisterkarte wird auf dem Dashboard geöffnet. Hierbei handelt es sich um eine getunnelte Verbindung, die auf die Azure CLI zurückgreift.

    ![Screenshot: Getunnelte Verbindung](./media/contoso-migration-rebuild/aks9.png)  
    _Abbildung 11: Eine getunnelte Verbindung._

## <a name="step-2-configure-the-back-end-pipeline"></a>Schritt 2: Konfigurieren der Back-End-Pipeline

### <a name="create-an-azure-devops-project-and-build"></a>Erstellen eines Azure DevOps-Projekts und -Builds

Contoso erstellt ein Azure DevOps-Projekt, konfiguriert einen CI-Build zum Erstellen des Containers und überträgt ihn dann mithilfe von Push an die Containerregistrierung. In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.

1. Unter `visualstudio.com` erstellen sie eine neue Organisation (`contosodevops360.visualstudio.com`) und konfigurieren sie für die Verwendung von Git.

2. Sie erstellen ein neues Projekt (`SmartHotelBackend`), wobei **Git** für die Versionskontrolle und **Agile** für den Workflow ausgewählt wird.

    ![Screenshot: Azure DevOps-Bereich „Neues Projekt erstellen“](./media/contoso-migration-rebuild/vsts1.png)  
    _Abbildung 12: Erstellen eines neuen Projekts._

3. Sie importieren das [GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Screenshot: Azure DevOps-Bereich „Git-Repository importieren“](./media/contoso-migration-rebuild/vsts2.png)  
    _Abbildung 13: Importieren des GitHub-Repositorys._

4. Sie klicken unter **Pipelines** auf **Build** und erstellen eine neue Pipeline, indem sie Azure Repos Git als Quelle aus dem Repository verwenden.

    ![Screenshot: DevOps-Bereich zum Erstellen einer neuen Pipeline](./media/contoso-migration-rebuild/vsts3.png)  
    _Abbildung 14: Eine neue Pipeline wird erstellt._

5. Sie klicken auf **Leere Stufe**.

    ![Screenshot: Option „Leere Stufe“ in Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)  
    _Abbildung 15: Starten mit einem leeren Auftrag._

6. Sie klicken auf **Gehostete Linux-Vorschau** für die Buildpipeline.

    ![Screenshot: Einrichten der Buildpipeline in Azure DevOps](./media/contoso-migration-rebuild/vsts5.png)  
    _Abbildung 16: Einrichten der Buildpipeline._

7. Unter **Phase 1** fügt Contoso einen **Docker Compose**-Task hinzu. Dieser Task erstellt Docker Compose.

    ![Screenshot: Erstellen eines Docker Compose-Tasks in Azure DevOps](./media/contoso-migration-rebuild/vsts6.png)  
    _Abbildung 17: Docker Compose wird erstellt._

8. Contoso wiederholt den **Docker Compose**-Task und fügt einen weiteren Task hinzu. Hierdurch werden die Container mithilfe von Push an die Containerregistrierung übertragen.

     ![Screenshot: Hinzufügen eines weiteren Docker Compose-Tasks in Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)  
    _Abbildung 18: Ein weiterer Docker Compose-Task wird hinzugefügt._

9. Die Contoso-Mitarbeiter wählen den ersten Task für die Erstellung aus und konfigurieren den Build mit dem Azure-Abonnement, der Autorisierung und der Containerregistrierung.

    ![Screenshot: Erstellen und Konfigurieren des Builds in Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)  
    _Abbildung 19: Erstellen und Konfigurieren des Builds._

10. Sie geben den Pfad der Datei `docker-compose.yaml` im *src*-Ordner des Repositorys an. Sie entscheiden sich dazu, Dienstimages zu erstellen und das aktuelle Tag einzubinden. Wenn die Aktion zu **Dienstimages erstellen** wechselt, ändert sich der Name des Azure DevOps-Tasks in **Dienste automatisch erstellen**.

    ![Screenshot: Verschiedene Angaben zum Erstellen von Tasks in Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)  
    _Abbildung 20: Die Besonderheiten des Tasks._

11. Nun konfigurieren sie den zweiten Docker-Task (für die Übertragung mithilfe von Push). Sie wählen das Abonnement und die Containerregistrierung (`smarthotelacreus2`) aus.

    ![Screenshot: Konfigurieren des zweiten Docker-Tasks in Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)  
    _Abbildung 21: Konfigurieren des zweiten Docker-Tasks._

12. Sie geben den Dateinamen *docker-compose.yaml* einschließlich des neuesten Tags ein und klicken dann auf **Push service images** (Dienstimages mithilfe von Push übertragen). Wenn die Aktion zu **Dienstimages mithilfe von Push übertragen** wechselt, ändert sich der Name des Azure DevOps-Tasks in **Dienste automatisch mithilfe von Push übertragen**.

    ![Screenshot: Ändern des Azure DevOps-Tasknamens](./media/contoso-migration-rebuild/vsts11.png)  
    _Abbildung 22: Ändern des Azure DevOps-Tasknamens._

13. Nachdem die Azure DevOps-Tasks konfiguriert wurden, speichern Contoso-Administratoren die Buildpipeline und beginnen mit dem Buildprozess.

    ![Screenshot: Starten des Buildprozesses in Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)  
    _Abbildung 23: Starten des Buildprozesses._

14. Sie wählen den Buildauftrag aus, um den Status zu überprüfen.

    ![Screenshot: Überprüfen des Buildprozesses in Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)  
    _Abbildung 24: Überprüfen des Fortschritts._

15. Wenn der Build fertiggestellt ist, zeigt die Containerregistrierung die neuen Repositorys an, die mit den von den Microservices verwendeten Containern aufgefüllt werden.

    ![Screenshot: Anzeigen neuer Repositorys nach Abschluss des Builds in Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)  
    _Abbildung 25: Anzeigen neuer Repositorys nach Abschluss des Builds._

### <a name="deploy-the-back-end-infrastructure"></a>Bereitstellen der Back-End-Infrastruktur

Mithilfe des erstellten AKS-Clusters und der Docker-Imagebuilds stellen Contoso-Administratoren nun die restliche Infrastruktur bereit, die von Back-End-Microservices genutzt wird. 
- In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet. 
- Der Ordner `/deploy/k8s/arm` enthält ein einziges Skript zum Erstellen aller Elemente.

Die Administratoren stellen die Infrastruktur wie folgt bereit:

1. Sie öffnen eine Developer-Eingabeaufforderung und verwenden dann den Befehl `az login` als Anmeldung für das Azure-Abonnement.

2. Sie verwenden die Datei `deploy.cmd` zur Bereitstellung der Azure-Ressourcen in der Ressourcengruppe „ContosoRG“ und der Region „USA, Osten 2“, indem sie den folgenden Befehl eingeben:

    `.\deploy.cmd azuredeploy ContosoRG -c eastus2`

    ![Screenshot: Bereitstellen des Back-Ends](./media/contoso-migration-rebuild/backend1.png)  
    _Abbildung 26: Bereitstellen des Back-Ends._

3. Im Azure-Portal erfassen sie die Verbindungszeichenfolgen für die einzelnen Datenbanken zur späteren Verwendung.

    ![Screenshot: Verbindungszeichenfolgen für die einzelnen Datenbanken](./media/contoso-migration-rebuild/backend2.png)  
    _Abbildung 27: Erfassen der Verbindungszeichenfolgen der einzelnen Datenbanken._

### <a name="create-the-back-end-release-pipeline"></a>Erstellen der Back-End-Releasepipeline

Contoso-Administratoren gehen nun wie folgt vor:

- Sie stellen den NGINX-Eingangscontroller bereit, um eingehenden Datenverkehr für die Dienste zuzulassen.
- Sie stellen die Microservices für den AKS-Cluster bereit.
- In einem ersten Schritt aktualisieren die Administratoren die Verbindungszeichenfolgen zu den Microservices mithilfe von Azure DevOps. Sie konfigurieren eine neue Azure DevOps-Releasepipeline, um die Microservices bereitzustellen.
- In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.
- Einige der Konfigurationseinstellungen (z. B. Active Directory B2C) werden nicht in diesem Artikel behandelt. Weitere Informationen zu diesen Einstellungen finden Sie im zuvor erwähnten „SmartHotel360“-Back-End-Repository.

Die Administratoren erstellen die Pipeline:

1. In Visual Studio aktualisieren sie die Datei */deploy/k8s/config_local.yml* anhand der zuvor notierten Informationen zur Datenverbindung.

    ![Screenshot: Schaltfläche „Neue Pipeline“ in Visual Studio](./media/contoso-migration-rebuild/back-pipe1.png)  
    _Abbildung 28: Datenbankverbindungen._

2. Sie öffnen Azure DevOps und klicken im Projekt „SmartHotel360“ im Bereich **Releases** auf **+ Neue Pipeline**.

    ![Screenshot: Schaltfläche „Neue Pipeline“ in Azure DevOps](./media/contoso-migration-rebuild/back-pipe2.png)  
    _Abbildung 29: Eine neue Pipeline wird erstellt._

3. Sie wählen **Leere Stufe** aus, um die Pipeline ohne Vorlage zu starten.
4. Sie geben den Phasen- und Pipelinenamen an.

      ![Screenshot: Erstellen eines Stufennamens in Azure DevOps](./media/contoso-migration-rebuild/back-pipe4.png)  
        _Abbildung 30: Der Phasenname._

      ![Screenshot: Erstellen eines Pipelinenamens in Azure DevOps](./media/contoso-migration-rebuild/back-pipe5.png)  
        _Abbildung 31: Der Pipelinename._

5. Sie fügen ein Artefakt hinzu.

     ![Screenshot: Hinzufügen eines Artefakts in Azure DevOps](./media/contoso-migration-rebuild/back-pipe6.png)  
    _Abbildung 32: Hinzufügen eines Artefakts._

6. Sie wählen **Git** als Quelltyp aus und geben Projekt, Quelle und Masterbranch für die Anwendung SmartHotel360 an.

    ![Screenshot: Bereich „Artefakt hinzufügen“ mit Git als Quelltyp](./media/contoso-migration-rebuild/back-pipe7.png)  
    _Abbildung 33: Bereich für Artefakteinstellungen_

7. Sie wählen den Tasklink aus.

    ![Screenshot: Hervorgehobener Link für Tasks in Azure DevOps](./media/contoso-migration-rebuild/back-pipe8.png)  
    _Abbildung 34: Der Tasklink._

8. Sie fügen eine neue Azure PowerShell-Aufgabe hinzu, sodass sie ein PowerShell-Skript in einer Azure-Umgebung ausführen können.

    ![Screenshot: Hinzufügen eines neuen PowerShell-Tasks in Azure](./media/contoso-migration-rebuild/back-pipe9.png)  
    _Abbildung 35: Hinzufügen eines neuen PowerShell-Tasks._

9. Sie wählen zunächst das Azure-Abonnement für den Task und anschließend das Skript `deploy.ps1` im Git-Repository aus.

    ![Screenshot: Auswählen eines Skripts für die Ausführung aus dem Git-Repository](./media/contoso-migration-rebuild/back-pipe10.png)  
    _Abbildung 36: Ausführen des Skripts._

10. Sie fügen dem Skript Argumente hinzu. Das Skript löscht den gesamten Clusterinhalt (außer den **eingehenden Daten** und dem **Eingangscontroller**) und stellt die Microservices bereit.

    ![Screenshot: Argumente, die dem Skript hinzugefügt werden sollen](./media/contoso-migration-rebuild/back-pipe11.png)  
    _Abbildung 37: Hinzufügen von Argumenten zum Skript._

11. Sie legen die bevorzugte Azure PowerShell-Version als neueste Version fest und speichern die Pipeline.

12. Sie gehen zurück zum Bereich **Neues Release erstellen** und erstellen manuell ein neues Release.

    ![Screenshot: Bereich „Neues Release erstellen“](./media/contoso-migration-rebuild/back-pipe12.png)  
    _Abbildung 38: Manuelles Erstellen eines neuen Releases._

13. Nachdem sie das Release erstellt haben, können sie es auswählen und unter **Aktionen** auf **Bereitstellen** klicken.

      ![Screenshot: Hervorgehobene Schaltfläche „Bereitstellen“ zum Bereitstellen eines Releases](./media/contoso-migration-rebuild/back-pipe13.png)  
    _Abbildung 39: Bereitstellen eines Releases._

14. Nach Abschluss der Bereitstellung führen sie mithilfe der Azure Cloud Shell folgenden Befehl aus, um den Status von Diensten zu überprüfen: `kubectl get services`.

## <a name="step-3-provision-front-end-services"></a>Schritt 3: Bereitstellen von Front-End-Diensten

Contoso-Administratoren müssen die von den Front-End-Anwendungen verwendete Infrastruktur bereitstellen. Dazu erstellen sie Folgendes:

- einen Blobspeichercontainer zum Speichern der Fotos von Haustieren
- eine Azure Cosmos DB-Datenbank zum Speichern von Dokumenten mit Informationen zu Haustieren
- Die Maschinelles Sehen-API für die Website.

In den Anweisungen für diesen Abschnitt wird das Repository [SmartHotel360-website](https://github.com/microsoft/smartHotel360-website) verwendet.

### <a name="create-blob-storage-containers"></a>Erstellen von Blob Storage-Containern

1. Die Administratoren öffnen im Azure-Portal das erstellte Speicherkonto und klicken anschließend auf **Blobs**.
2. Sie erstellen einen neuen Container `Pets`, bei dem die öffentliche Zugriffsebene für den Container festgelegt ist. Benutzer laden ihre Fotos von Haustieren in diesen Container hoch.

    ![Screenshot: Erstellen eines neuen Containers im Azure-Portal](./media/contoso-migration-rebuild/blob1.png)  
    _Abbildung 40: Erstellen eines neuen Containers._

3. Sie erstellen einen zweiten neuen Container namens `settings`. Eine Datei mit allen Front-End-App-Einstellungen wird in diesen Container platziert.

    ![Screenshot: Erstellen eines zweiten neuen Containers im Azure-Portal](./media/contoso-migration-rebuild/blob2.png)  
    _Abbildung 41: Erstellen eines zweiten Containers._

4. Sie speichern die Zugriffsdetails für das Speicherkonto zur späteren Verwendung in einer Textdatei.

    ![Screenshot: Textdatei zum Speichern von Zugriffsdetails](./media/contoso-migration-rebuild/blob2.png)  
    _Abbildung 42: Eine Textdatei, in der Zugriffsdetails gespeichert werden._

### <a name="provision-an-azure-cosmos-db-database"></a>Bereitstellen einer Azure Cosmos DB-Datenbank

Contoso-Administratoren stellen eine Azure Cosmos DB-Datenbank bereit, die für Informationen zu Haustieren verwendet werden soll.

1. Sie erstellen eine **Azure Cosmos DB**-Datenbank im Azure Marketplace.

    ![Screenshot: Erstellen einer Azure Cosmos DB-Datenbank im Azure Marketplace](./media/contoso-migration-rebuild/cosmos1.png)  
    _Abbildung 43: Erstellen einer Azure Cosmos DB-Datenbank._

2. Sie geben den Namen `contososmarthotel` an, wählen die SQL-API aus und fügen sie in die Produktionsressourcengruppe `ContosoRG` in der Hauptregion `East US 2` ein.

    ![Screenshot: Azure Cosmos DB-Datenbankname und andere Einstellungen](./media/contoso-migration-rebuild/cosmos2.png)  
    _Abbildung 44: Benennen einer Azure Cosmos DB-Datenbank._

3. Contoso fügt eine neue Sammlung zur Datenbank mit Standardkapazität und -durchsatz hinzu.

    ![Screenshot: Bereich „Sammlung hinzufügen“ für Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)  
    _Abbildung 45: Hinzufügen einer neuen Sammlung zur Datenbank._

4. Sie notieren die Verbindungsinformationen für die Datenbank zur zukünftigen Verwendung.

    ![Screenshot: Verbindungsinformationen für die Azure Cosmos DB-Datenbank](./media/contoso-migration-rebuild/cosmos4.png)  
    _Abbildung 46: Die Verbindungsinformationen für die Datenbank._

### <a name="provision-the-computer-vision-api"></a>Bereitstellen der Maschinelles Sehen-API

Contoso-Administratoren stellen die Maschinelles Sehen-API bereit. Die API wird von der Funktion zum Auswerten der Bilder aufgerufen, die von den Benutzern hochgeladen wurden.

1. Die Administratoren erstellen im Azure Marketplace eine **Maschinelles Sehen**-Instanz.

     ![Screenshot: Erstellen einer neuen „Maschinelles Sehen“-Instanz im Azure Marketplace](./media/contoso-migration-rebuild/vision1.png)  
    _Abbildung 47: Neue Instanz im Azure Marketplace_

2. Sie stellen die API (`smarthotelpets`) in der Produktionsressourcengruppe `ContosoRG` in der Hauptregion (`East US 2`) bereit.

    ![Screenshot: Einrichten einer API in einer Produktionsressourcengruppe](./media/contoso-migration-rebuild/vision2.png)  
    _Abbildung 48: Bereitstellen einer API in einer Produktionsressourcengruppe._

3. Contoso speichert die Verbindungseinstellungen für die API in einer Textdatei zur späteren Verwendung.

     ![Screenshot: Speichern der Verbindungseinstellungen der API in einer Textdatei](./media/contoso-migration-rebuild/vision3.png)  
    _Abbildung 49: Speichern der Verbindungseinstellungen der API_

### <a name="provision-the-azure-web-app"></a>Bereitstellen der Azure-Web-App

Contoso-Administratoren stellen die Web-App mithilfe des Azure-Portals bereit.

1. Das Unternehmen wählt **Web-App** im Portal aus.

    ![Screenshot: Auswählen einer Web-App im Azure-Portal](./media/contoso-migration-rebuild/web-app1.png)  
    _Abbildung 50: Auswählen der Web-App._

2. Sie geben einen Namen für die Web-App an (`smarthotelcontoso`), führen die App unter Windows aus und platzieren sie in der Produktionsressourcengruppe `ContosoRG`. Sie erstellen eine neue Application Insights-Instanz zur Anwendungsüberwachung.

    ![Screenshot: Angeben eines Web-App-Namens und anderer Details](./media/contoso-migration-rebuild/web-app2.png)  
    _Abbildung 51: Der Name der Web-App._

3. Anschließend navigieren die Administratoren zur Adresse der Anwendung, um zu überprüfen, ob sie erfolgreich erstellt wurde.

4. Im Azure-Portal erstellen sie einen Stagingslot für den Code. Die Pipeline wird in diesem Slot bereitgestellt. Durch diesen Ansatz wird sichergestellt, dass Code erst in die Produktionsumgebung gelangt, wenn Administratoren ein Release ausführen.

    ![Screenshot: Hinzufügen eines Web-App-Stagingslots](./media/contoso-migration-rebuild/web-app3.png)  
    _Abbildung 52: Hinzufügen eines Web-App-Stagingslots_

### <a name="provision-the-function-app"></a>Bereitstellen der Funktions-App

Contoso-Administratoren stellen im Azure-Portal die Funktions-App bereit.

1. Sie wählen **Funktionen-App** aus.

    ![Screenshot: Erstellen einer Funktions-App](./media/contoso-migration-rebuild/function-app1.png)  
    _Abbildung 53: Auswählen der Funktions-App._

2. Sie geben einen Namen für die Funktions-App an (`smarthotelpetchecker`). Sie platzieren die Funktions-App in der Produktionsressourcengruppe (`ContosoRG`). Sie legen den Hostingort auf **Consumption Plan** (Verbrauchstarif) fest und platzieren die Funktions-App in der Region `East US 2`. Daraufhin wird neben einem neuen Speicherkonto auch eine Application Insights-Instanz für die Überwachung erstellt.

    ![Screenshot: Einstellungen der Funktions-App](./media/contoso-migration-rebuild/function-app2.png)  
    _Abbildung 54: Funktions-App-Einstellungen._

3. Nachdem sie die Funktions-App bereitgestellt haben, navigieren die Administratoren zur Adresse der App, um zu überprüfen, ob sie erfolgreich erstellt wurde.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Schritt 4: Einrichten der Front-End-Pipeline

Contoso-Administratoren erstellen zwei verschiedene Projekte für die Front-End-Website.

1. In Azure DevOps erstellen sie ein Projekt `SmartHotelFrontend`.

    ![Screenshot: Erstellen eines Front-End-Projekts](./media/contoso-migration-rebuild/function-app1.png)  
    _Abbildung 55: Erstellen eines Front-End-Projekts_

2. Sie importieren das Git-Repository [SmartHotel360 front end](https://github.com/Microsoft/SmartHotel360-Website) in das neue Projekt.

3. Für die Funktions-App erstellen sie ein weiteres Azure DevOps-Projekt (`SmartHotelPetChecker`) und importieren das Git-Repository [PetChecker](https://github.com/sonahander/SmartHotel360-PetCheckerFunction) in dieses Projekt.

### <a name="configure-the-web-app"></a>Konfigurieren der Web-App

Contoso-Administratoren konfigurieren nun die Web-App zur Verwendung von Contoso-Ressourcen.

1. Die Administratoren stellen eine Verbindung mit dem Azure DevOps-Projekt her und klonen das Repository lokal auf dem Entwicklungscomputer.
2. In Visual Studio öffnet Contoso den Ordner, um alle Dateien im Repository anzuzeigen.

    ![Screenshot: Visual Studio-Ordner mit allen Dateien im Repository](./media/contoso-migration-rebuild/configure-webapp1.png)  
    _Abbildung 56: Anzeigen aller Dateien im Repository._

3. Sie aktualisieren ggf. die Konfigurationsänderungen.

    - Wenn die Web-App gestartet wird, sucht sie nach der App-Einstellung `SettingsUrl`.
    - Diese Variable muss eine URL enthalten, die auf eine Konfigurationsdatei zeigt.
    - Die Einstellung wird standardmäßig als öffentlicher Endpunkt verwendet.

4. Sie aktualisieren die `/config-sample.json/sample.json`-Datei.

    - Dies ist die Konfigurationsdatei für das Web, wenn der öffentliche Endpunkt verwendet wird.
    - Sie bearbeiten die Abschnitte `urls` und `pets_config` mit den Werten für die AKS-API-Endpunkte, die Speicherkonten und die Azure Cosmos DB-Datenbank.
    - Die URLs sollten dem DNS-Namen der neuen Web-App entsprechen, die von Contoso erstellt wird.
    - Für Contoso ist dies `smarthotelcontoso.eastus2.cloudapp.azure.com`.

    ![Screenshot: JSON-Einstellungen in Visual Studio](./media/contoso-migration-rebuild/configure-webapp2.png)  
    _Abbildung 57: JSON-Einstellungen_

5. Nachdem die Administratoren die Datei aktualisiert haben, benennen sie diese in `smarthotelsettingsurl` um und laden sie in den zuvor erstellten Blobspeicher hoch.

    ![Screenshot: Umbenennen und Hochladen der JSON-Datei](./media/contoso-migration-rebuild/configure-webapp3.png)  
    _Abbildung 58: Umbenennen und Hochladen der Datei._

6. Sie wählen die Datei aus, um die URL abzurufen. Diese URL wird von der Anwendung beim Abrufen der Konfigurationsdatei verwendet.

    ![Screenshot: URL der von der Anwendung verwendeten Datei](./media/contoso-migration-rebuild/configure-webapp4.png)  
    _Abbildung 59: Die Anwendungs-URL._

7. In der Datei *appsettings.Production.json* aktualisieren sie `SettingsURL` auf die URL der neuen Datei.

    ![Screenshot: Aktualisieren der URL zur neuen Datei](./media/contoso-migration-rebuild/configure-webapp5.png)  
    _Abbildung 60: Aktualisieren der URL mit der neuen Datei._

### <a name="deploy-the-website-to-azure-app-service"></a>Bereitstellen der Website in Azure App Service

Contoso-Administratoren können die Website jetzt veröffentlichen.

1. Sie öffnen Azure DevOps und klicken im Projekt `SmartHotelFrontend` unter **Builds and Releases** (Builds und Releases) auf **+ Neue Pipeline**.
2. Sie wählen **Azure DevOps-Git** als Quelle aus.
3. Sie wählen die Vorlage **ASP.NET Core** aus.
4. Sie überprüfen die Pipeline und stellen sicher, dass die Optionen **Webprojekte veröffentlichen** und **Veröffentlichte Projekte komprimieren** ausgewählt wurden.

    ![Screenshot: Pipelineeinstellungen des Webprojekts](./media/contoso-migration-rebuild/vsts-publish-front2.png)  
    _Abbildung 61: Pipelineeinstellungen._

5. Unter **Trigger** aktivieren sie „Continuous Integration“ und fügen den Masterbranch hinzu. Dadurch wird sichergestellt, dass die Buildpipeline jedes Mal startet, wenn die Lösung neuen Code für den Masterbranch committet.

    ![Screenshot: Aktivieren von Continuous Integration und Hinzufügen des Masterbranchs](./media/contoso-migration-rebuild/vsts-publish-front3.png)  
    _Abbildung 62: Aktivieren von Continuous Integration_

6. Sie wählen **Speichern und in Warteschlange einreihen** aus, um einen Buildvorgang zu starten.
7. Nachdem der Build abgeschlossen wurde, konfigurieren sie mithilfe von **Azure App Service-Bereitstellung** eine Releasepipeline.
8. Sie geben den Stufennahmen **Staging** an.

    ![Screenshot: Angeben eines Stufennamens für die Umgebung](./media/contoso-migration-rebuild/vsts-publish-front4.png)  
    _Abbildung 63: Benennen der Umgebung._

9. Sie fügen ein Artefakt hinzu und wählen den konfigurierten Build aus.

    ![Screenshot: Hinzufügen eines Artefakts mit „Build“ als Quelltyp](./media/contoso-migration-rebuild/vsts-publish-front5.png)  
    _Abbildung 64: Hinzufügen eines Artefakts._

10. Sie klicken auf das Blitzsymbol des Artefakts und legen für Continuous Deployment dann **Aktiviert** fest.

    ![Screenshot: Aktivieren von Continuous Deployment](./media/contoso-migration-rebuild/vsts-publish-front6.png)  
    _Abbildung 65: Aktivieren von „Continuous Deployment“._

11. Sie wählen in **Umgebung** unter **Staging** die Option **1 job, 1 task** (1 Auftrag, 1 Aufgabe) aus.
12. Nachdem sie das Abonnement und den Web-App-Namen ausgewählt haben, öffnen die Administratoren den Task **Deploy Azure App Service** (Azure App Service bereitstellen). Die Bereitstellung wurde für die Verwendung des Bereitstellungsslots **Staging** konfiguriert. Dadurch wird automatisch Code zur Überprüfung und Genehmigung in diesem Slot erstellt.

     ![Screenshot: Bereitstellen der Web-App in einem Slot](./media/contoso-migration-rebuild/vsts-publish-front7.png)  
    _Abbildung 66: Bereitstellen in einem Slot_

13. In der **Pipeline** fügen sie eine neue Phase hinzu.

    ![Screenshot: Registerkarte „Pipeline“ und Hinzufügen einer neuen Stufe](./media/contoso-migration-rebuild/vsts-publish-front8.png)  
    _Abbildung 67: Hinzufügen einer neuen Phase._

14. Sie klicken auf **Azure App Service-Bereitstellung mit Slot** und geben der Umgebung dann den Namen **Prod**.
15. Sie klicken auf **1 job, 2 tasks** (1 Auftrag, 2 Tasks) und wählen dann das Abonnement, den App Service-Namen und den Slot **Staging** aus.

    ![Screenshot: Benennen der Umgebung](./media/contoso-migration-rebuild/vsts-publish-front10.png)  
    _Abbildung 68: Benennen der Umgebung._

16. Sie entfernen **Deploy Azure App Service to Slot** (Azure App Service in Slot bereitstellen) aus der Pipeline. Diese Aufgabe wurde in den vorherigen Schritten dort eingefügt.

    ![Screenshot: Entfernen eines Slots aus der Pipeline](./media/contoso-migration-rebuild/vsts-publish-front11.png)  
    _Abbildung 69: Entfernen eines Slots aus der Pipeline._

17. Sie speichern die Pipeline. Sie wählen in der Pipeline **Bedingungen nach der Bereitstellung** aus.

    ![Screenshot: Schaltfläche „Bedingungen nach der Bereitstellung“](./media/contoso-migration-rebuild/vsts-publish-front12.png)  
    _Abbildung 70: Bedingungen nach der Bereitstellung._

18. Sie aktivieren **Genehmigungen nach der Bereitstellung** und fügen dann eine Entwicklungsleitung als genehmigende Person hinzu.

    ![Screenshot: Liste der aktivierten genehmigenden Personen nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front13.png)  
    _Abbildung 71: Hinzufügen eines Genehmigers._

19. Die Administratoren starten in der Buildpipeline manuell einen Build. Dadurch wird die neue Releasepipeline ausgelöst, wodurch wiederum die Website im Stagingslot bereitgestellt wird. Bei Contoso lautet die URL für den Slot `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Nach Abschluss des Buildvorgangs und nachdem das Release im Slot bereitgestellt wurde, sendet Azure DevOps für die Genehmigung eine E-Mail an die Entwicklungsleitung.

21. Die Entwicklungsleitung wählt **Genehmigung anzeigen** aus und kann dann die Anforderung im Azure DevOps-Portal genehmigen oder ablehnen.

    ![Screenshot: Link „Genehmigen oder ablehnen“ für Genehmigung nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front14.png)  
    _Abbildung 72: Ausstehende Anforderung für Releasegenehmigung_

22. Die Entwicklungsleitung erstellt einen Kommentar und genehmigt die Anforderung. Dadurch beginnt der Austausch der Slots **Staging** und **Prod**. Zudem wird der Build in die Produktionsumgebung verschoben.

    ![Screenshot: Genehmigung und Kommentar nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front15.png)  
    _Abbildung 73: Verschieben des Builds in die Produktion._

23. Der Austausch wird durch die Pipeline abgeschlossen.

    ![Screenshot: Status der Buildbereitstellung](./media/contoso-migration-rebuild/vsts-publish-front16.png)  
    _Abbildung 74: Abschließen des Austausches._

24. Das Team überprüft den Slot **prod**, um sicherzustellen, dass sich die Web-App in der Produktionsumgebung unter `https://smarthotelcontoso.azurewebsites.net/` befindet.

### <a name="deploy-the-petchecker-function-app"></a>Bereitstellen der Funktions-App PetChecker

Die Contoso-Administratoren stellen die Anwendung wie folgt bereit:

1. Sie klonen das Repository lokal auf dem Entwicklungscomputer, indem sie eine Verbindung mit dem Azure DevOps-Projekt herstellen.
2. In Visual Studio öffnet Contoso den Ordner, um alle Dateien im Repository anzuzeigen.
3. Sie öffnen die Datei *src/PetCheckerFunction/local.settings.json* und fügen die App-Einstellungen für Speicher, die Azure Cosmos DB-Datenbank und die Maschinelles Sehen-API hinzu.

    ![Screenshot: App-Einstellungen in der JSON-Datei in Visual Studio](./media/contoso-migration-rebuild/function5.png)  
    _Abbildung 75: Bereitstellen der Funktion._

4. Sie committen den Code, synchronisieren ihn mit Azure DevOps und pushen so ihre Änderungen.
5. Sie fügen eine neue Buildpipeline hinzu und wählen anschließend **Azure DevOps Git** für die Quelle aus.
6. Sie wählen die Vorlage **ASP.NET Core (.NET Framework)** aus.
7. Sie übernehmen die Standardwerte für die Vorlage.
8. Unter **Trigger** klicken sie auf **Continuous Integration aktivieren** und dann auf **Save & Queue** (Speichern und in Warteschlange einreihen), um einen Buildvorgang zu starten.
9. Nach erfolgreichem Buildvorgang erstellen sie eine Releasepipeline, indem sie **Azure App Service-Bereitstellung mit Slot** hinzufügen.
10. Sie geben der Umgebung den Namen **Prod** und wählen anschließend das Abonnement aus. Sie legen den **App-Typ** auf **Funktions-App** und den App Service-Namen auf `smarthotelpetchecker` fest.

    ![Screenshot: Name des App-Typs und des App-Diensts](./media/contoso-migration-rebuild/petchecker2.png)  
    _Abbildung 76: Die Funktions-App._

11. Sie fügen den Artefakt **Build** hinzu.

    ![Screenshot: Hinzufügen eines Artefakts mit dem Buildquellentyp](./media/contoso-migration-rebuild/petchecker3.png)  
    _Abbildung 77: Hinzufügen eines Artefakts._

12. Sie aktivieren **Continuous Deployment-Trigger** und klicken anschließend auf **Speichern**.
13. Sie wählen **Neuen Build in Warteschlange** aus, um die ganze CI/CD-Pipeline auszuführen.
14. Nachdem die Funktion bereitgestellt wurde, wird sie im Azure-Portal mit dem Status **Wird ausgeführt** angezeigt.

    ![Screenshot: Funktions-App mit dem Status „Wird ausgeführt“](./media/contoso-migration-rebuild/function6.png)  
    _Abbildung 78: Aktualisieren des Funktionsstatus_

15. Sie navigieren zur PetChecker-Anwendung unter `http://smarthotel360public.azurewebsites.net/pets`, um zu überprüfen, ob sie ordnungsgemäß funktioniert.

16. Sie wählen den Avatar aus, um ein Bild hochzuladen.

    ![Screenshot: Bereich zum Zuweisen eines Bilds zu einem Avatar](./media/contoso-migration-rebuild/function7.png)  
    _Abbildung 79: Zuweisen eines Bilds zu einem Avatar_

17. Das erste Foto, das überprüft werden soll, ist das eines kleinen Hundes.

    ![Screenshot: Foto von einem Hund](./media/contoso-migration-rebuild/function8.png)  
    _Abbildung 80: Überprüfen des Fotos_

18. Die Anwendung gibt eine Bestätigungsmeldung zurück.

    ![Screenshot: Bestätigungsmeldung](./media/contoso-migration-rebuild/function9.png)  
    _Abbildung 81: Eine Bestätigungsmeldung._

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso nun die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neuen Datenbanken geschützt sind. Weitere Informationen finden Sie in der [Übersicht über die Sicherheitsfunktionen von Azure SQL-Datenbank und SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Die Anwendung muss für die Verwendung von SSL mit Zertifikaten aktualisiert werden. Die Containerinstanz sollte erneut bereitgestellt werden, um auf 443 zu antworten.
- Zum Schutz von Geheimnissen für die Service Fabric-Anwendungen sollte Contoso die Verwendung von Azure Key Vault in Erwägung ziehen. Weitere Informationen finden Sie unter [Verwalten von verschlüsselten Geheimnissen in Service Fabric-Anwendungen](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups-and-disaster-recovery"></a>Sicherungen und Notfallwiederherstellung

- Contoso muss die [Sicherungsanforderungen für Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) überprüfen.
- Contoso sollte die Implementierung von [SQL-Failovergruppen berücksichtigen, um ein regionales Failover für die Datenbank bereitzustellen](https://docs.microsoft.com/azure/sql-database/sql-database-auto-failover-group).
- Contoso kann die [Georeplikation für die Premium-SKU von Azure Container Registry](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication) nutzen.
- Azure Cosmos DB führt automatisch Sicherungen durch. Weitere Informationen finden Sie unter [Onlinesicherung und bedarfsgesteuerte Wiederherstellung in Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über das Enterprise Agreement verrechnet.
- Contoso aktiviert [Azure Cost Management und das Azure-Abrechnungsportal](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde die Anwendung SmartHotel360 in Azure von Contoso neu erstellt. Die lokale VM für das Anwendungs-Front-End wurde für Azure App Service-Web-Apps neu erstellt. Das Back-End der Anwendung wird mithilfe von Microservices erstellt, die für Container bereitgestellt werden, die von AKS verwaltet werden. Die Funktionalität hat Contoso durch eine Anwendung für Fotos von Haustieren verbessert.

## <a name="suggested-skills"></a>Empfohlene Qualifikationen

Microsoft Learn ist ein neuer Lernansatz. Die Bereitschaft zu den neuen Qualifikationen und Aufgaben, die mit der Cloudeinführung verbunden sind, entsteht nicht problemlos. Microsoft Learn bietet einen lohnenderen Ansatz für praktisches Lernen, der Ihnen hilft, Ihre Ziele schneller zu erreichen. In Microsoft Learn können Sie Module abschließen, für die Sie Punkte erhalten. Außerdem können Sie verschiedene Levels durcharbeiten und viele weitere Optionen nutzen.

Hier finden Sie zwei Beispiele für maßgeschneiderte Lernpfade in Microsoft Learn, die auf die Contoso-Anwendung „SmartHotel360“ in Azure abgestimmt sind.

<!--docsTest:ignore "Azure Cognitive Vision Services" -->

- **[Bereitstellen einer Website in Azure mithilfe von Azure App Service:](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service)** Durch das Erstellen von Web-Apps in Azure können Sie Ihre Website leicht veröffentlichen und verwalten, ohne dass Sie mit den zugrunde liegenden Servern, Speicher oder Netzwerkressourcen arbeiten müssen. Stattdessen können Sie sich auf Ihre Websitefeatures konzentrieren und die stabile Azure-Plattform verwenden, um sicheren Zugriff auf Ihre Website zu ermöglichen.

- **[Verarbeiten und Klassifizieren von Bildern mit der Bildanalyse von Azure Cognitive Services:](https://docs.microsoft.com/learn/paths/classify-images-with-vision-services)** Azure Cognitive Services bietet vorgefertigte Funktionen, um die Funktionalität für maschinelles Sehen in Ihren Anwendungen zu aktivieren. Erfahren Sie, wie Sie die Bildanalyse von Cognitive Services verwenden, um Gesichter zu erkennen, Bilder mit Tags zu versehen und zu klassifizieren und Objekte zu identifizieren.
