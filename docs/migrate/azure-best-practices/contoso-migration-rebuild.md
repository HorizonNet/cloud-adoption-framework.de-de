---
title: Neuerstellen einer lokalen App in Azure
description: In diesem Artikel erfahren Sie, wie Contoso eine App in Azure mithilfe von Azure App Service, Azure Kubernetes Service, Cosmos DB, Azure Functions und Azure Cognitive Services neu erstellt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 92ca2b6a59654824e4d4dcb23f29917491f64ffb
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81120785"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM contosohost vcenter contosodc smarthotel contososmarthotel smarthotelcontoso smarthotelpetchecker petchecker smarthotelakseus smarthotelacreus smarthotelpets kubectl contosodevops visualstudio azuredeploy cloudapp smarthotelsettingsurl appsettings -->

# <a name="rebuild-an-on-premises-app-on-azure"></a>Neuerstellen einer lokalen App in Azure

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso einer zweistufigen Windows-.NET-App, die auf VMware-VMs ausgeführt wird, als Teil einer Migration der App-VMs zu Azure neu erstellt. Contoso migriert die Front-End-VM der App zu einer Azure App Services-Web-App. Das Back-End der App wird mithilfe von Microservices erstellt, die für Container bereitgestellt werden, die von Azure Kubernetes Service (AKS) verwaltet werden. Die Website interagiert mit Azure Functions zum Bereitstellen der Funktionalität für Fotos von Haustieren.

Die in diesem Beispiel verwendet SmartHotel360-App wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst und möchte für seine Kunden differenzierte Funktionen auf seinen Websites bereitstellen.
- **Mehr Flexibilität.** Contoso muss schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss das Contoso-IT-Team Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat folgende App-Anforderungen für diese Migration gestellt. Anhand dieser Anforderungen wird die beste Migrationsmethode bestimmt:

- Die App wird in Azure so wichtig bleiben wie bisher. Sie sollte reibungslos laufen und sich mühelos skalieren lassen.
- Die App darf nicht auf IaaS-Komponenten basieren. Sie sollte für die Verwendung von PaaS- oder serverlosen Diensten ausgelegt sein.
- Die App-Builds sollten in Clouddiensten ausgeführt werden und Container sollten sich in einer privaten unternehmensweiten Containerregistrierung in der Cloud befinden.
- Die API-Dienst für Fotos von Haustieren sollte in der Praxis präzise und zuverlässig sein, da die von der App getroffenen Entscheidungen in den Hotels berücksichtigt werden müssen. Haustiere, denen der Zutritt erlaubt ist, dürfen in den Hotels bleiben.
- Um die Anforderungen einer DevOps-Pipeline zu erfüllen, verwendet Contoso Azure DevOps für die Quellcodeverwaltung mit Git-Repositorys. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service, Azure Functions und AKS bereitgestellt.
- Für Microservices im Back-End und für die Website im Front-End sind unterschiedliche CI/CD-Pipelines erforderlich.
- Für die Back-End-Dienste gelten andere Releasezyklen als für die Front-End-Web-App. Zur Erfüllung dieser Anforderung werden zwei verschiedene Pipelines bereitgestellt.
- Contoso benötigt eine Verwaltungsgenehmigung für die gesamte Front-End-Websitebereitstellung, die von der CI/CD-Pipeline bereitgestellt werden muss.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Azure-Dienste.

### <a name="current-app"></a>Aktuelle App

- Die lokale App SmartHotel360 ist auf zwei VMs aufgeteilt (WEBVM und SQLVM).
- Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com** (Version 6.5).
- Die VMware-Umgebung wird von der vCenter Server 6.5-Software (**vcenter.contoso.com**) auf einer VM verwaltet.
- Contoso verfügt über ein lokales Rechenzentrum (contoso-datacenter) mit einem lokalen Domänencontroller (**contosodc1**).
- Die lokalen VMs im Rechenzentrum von Contoso werden nach Abschluss der Migration außer Betrieb gesetzt.

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Das Front-End der App wird als Azure App Service-Web-App in der primären Azure-Region bereitgestellt.
- Eine Azure-Funktion bietet Uploads von Fotos von Haustieren, und die Website interagiert mit dieser Funktionalität.
- Die Haustierfotofunktion nutzt die maschinelles Sehen-API von Azure Cognitive Services und Cosmos DB.
- Das Back-End der Website wird mithilfe von Microservices erstellt. Diese werden in Containern bereitgestellt, die in Azure Kubernetes Service (AKS) verwaltet werden.
- Container werden mithilfe von Azure DevOps erstellt und mithilfe von Push an Azure Container Registry (ACR) übertragen.
- Vorerst stellt Contoso die Web-App und den Funktionscode mithilfe von Visual Studio manuell bereit.
- Microservices werden mithilfe eines PowerShell-Skripts bereitgestellt, das Kubernetes-Befehlszeilentools aufruft.

    ![Szenarioarchitektur](./media/contoso-migration-rebuild/architecture.png)

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

<!-- markdownlint-disable MD033 -->

**Aspekt** | **Details**
--- | ---
**Vorteile** | Durch den Einsatz von PaaS- und serverlosen Lösungen für die End-to-End-Bereitstellung verkürzt sich die Verwaltungszeit, die Contoso aufwenden muss, um ein Vielfaches.<br/><br/> Die Migration zu einer auf Microservices basierenden Architektur bietet Contoso die Möglichkeit, die Lösung ganz einfach im Lauf der Zeit zu erweitern.<br/><br/> Neue Funktionalität kann online geschaltet werden, ohne dass vorhandene Codebasen von Lösungen beeinträchtigt werden.<br/><br/> Die Web-App wird mit mehreren Instanzen ohne Single Point of Failure konfiguriert.<br/><br/> Die automatische Skalierung wird aktiviert, damit die App unterschiedliche hohe Datenverkehrsvolumen verarbeiten kann.<br/><br/> Mit dem Wechsel zu PaaS-Diensten kann Contoso veraltete Lösungen, die unter dem Betriebssystem Windows Server 2008 R2 ausgeführt werden, außer Betrieb nehmen.<br/><br/> Cosmos DB weist eine integrierte Fehlertoleranz auf, die keinen Konfigurationsaufwand seitens Contoso erfordert. Dies bedeutet, dass die Datenschicht kein Single Point of Failover mehr ist.
**Nachteile** | Container sind komplexer als andere Migrationsoptionen. Die Lernkurve könnte für Contoso ein Problem darstellen. Der Grad der Komplexität steigt und bietet trotz der Kurve einen hohen Nutzen.<br/><br/> Das Betriebsteam von Contoso muss eingearbeitet werden, um Azure, Container und Microservices für die App verstehen und unterstützen zu können.<br/><br/> Contoso hat noch nicht vollständig DevOps für die gesamte Lösung implementiert. Dies muss Contoso bei der Bereitstellung von Diensten für AKS, Azure Functions und Azure App Service berücksichtigen.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt ACR, AKS und Cosmos DB bereit.
2. Es stellt die Infrastruktur für die Bereitstellung bereit, wie etwa Azure App Service-Web-App, Speicherkonto, Funktionen und APIs.
3. Sobald die Infrastruktur eingerichtet ist, erstellt Contoso Microservicecontainerimages mithilfe der Azure DevOps-Lösung, die diese mithilfe von Push an ACR überträgt.
4. Contoso stellt diese Microservices mithilfe eines PowerShell-Skripts in AKS bereit.
5. Abschließend stellt Contoso die Funktion und die Web-App bereit.

    ![Migrationsprozess](./media/contoso-migration-rebuild/migration-process.png)

### <a name="azure-services"></a>Azure-Dienste

**Service** | **Beschreibung** | **Kosten**
--- | --- | ---
[AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Vereinfacht die Verwaltung, die Bereitstellung und den Betrieb von Kubernetes. Nutzt einen vollständig verwalteten Orchestrierungsdienst für Kubernetes-Container. | AKS ist ein kostenloser Dienst. Nur die virtuellen Computer sowie die entsprechenden verbrauchten Speicher- und Netzwerkressourcen müssen bezahlt werden. [Weitere Informationen](https://azure.microsoft.com/pricing/details/kubernetes-service)
[Azure-Funktionen](https://azure.microsoft.com/services/functions) | Beschleunigt die Entwicklung mit einer ereignisbasierten, serverlosen Computeumgebung. Die Skalierung erfolgt bedarfsabhängig. | Nur verbrauchte Ressourcen müssen bezahlt werden. Der Plan wird basierend auf dem Ressourcenverbrauch und den Ausführungen pro Sekunde berechnet. [Weitere Informationen](https://azure.microsoft.com/pricing/details/functions)
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Speichert Images für alle Arten von Containerbereitstellungen. | Die Kosten ergeben sich aus Features, Speicher und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/container-registry)
[Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Es können schnell Web-Apps, mobile Apps und API-Apps der Unternehmensklasse auf jeder Plattform erstellt, bereitgestellt und skaliert werden. | App Service-Pläne werden sekundengenau abgerechnet. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows)

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes:

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.
**Azure-Infrastruktur** | [Weitere Informationen](./contoso-migration-infrastructure.md) zur Vorgehensweise von Contoso beim Einrichten einer Azure-Infrastruktur.
**Voraussetzungen für Entwickler** | Contoso benötigt die folgenden Tools auf einer Entwicklerarbeitsstation:<br/><br/> - [Visual Studio 2017 Community Edition: Version 15.5](https://visualstudio.microsoft.com)<br/><br/> .NET-Workload aktiviert<br/><br/> [Git-Client](https://git-scm.com)<br/><br/> [Azure PowerShell](https://azure.microsoft.com/downloads)<br/><br/> [Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)<br/><br/> [Docker CE (Windows 10) oder Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) für die Verwendung von Windows-Containern festgelegt

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen von AKS und ACR:** Contoso stellt mithilfe von PowerShell den verwalteten AKS-Cluster und Azure Container Registry bereit.
> - **Schritt 2: Erstellen von Docker-Containern:** Das Unternehmen richtet CI für Docker-Container mithilfe von Azure DevOps ein und überträgt diese mithilfe von Push an ACR.
> - **Schritt 3: Bereitstellen von Back-End-Microservices:** Es stellt die restliche Infrastruktur bereit, die von Back-End-Microservices genutzt wird.
> - **Schritt 4: Bereitstellen der Front-End-Infrastruktur:** Es stellt die Front-End-Infrastruktur bereit, einschließlich Blob Storage für Fotos von Haustieren, Cosmos DB und der Maschinelles Sehen-API.
> - **Schritt 5: Migrieren des Back-Ends:** Es stellt Microservices bereit und führt diese in AKS aus, um das Back-End zu migrieren.
> - **Schritt 6: Veröffentlichen des Front-Ends:** Es veröffentlicht die App SmartHotel360 in App Service und die Funktions-App, die vom Haustierdienst aufgerufen wird.

## <a name="step-1-provision-back-end-resources"></a>Schritt 1: Bereitstellen von Back-End-Ressourcen

Contoso-Administratoren führen ein Bereitstellungsskript zum Erstellen des Managed Kubernetes-Clusters mit AKS und Azure Container Registry (ACR) aus.

- In den Anweisungen für diesen Abschnitt wird das Repository **SmartHotel360-Backend** verwendet.
- Das GitHub-Repository **SmartHotel360-Backend** enthält die gesamte Software für diesen Teil der Bereitstellung.

### <a name="ensure-prerequisites"></a>Erfüllen der Voraussetzungen

1. Vor Beginn stellen Contoso-Administratoren sicher, dass auf dem Entwicklungscomputer, den sie für die Bereitstellung verwenden, die erforderliche Software installiert ist.
2. Sie klonen das Repository mithilfe von Git lokal auf dem Entwicklungscomputer:

    `git clone https://github.com/Microsoft/SmartHotel360-Backend.git`

### <a name="provision-aks-and-acr"></a>Bereitstellen von AKS und ACR

Die Contoso-Administratoren führen die Bereitstellung wie folgt durch:

1. Sie öffnen den Ordner mit Visual Studio Code und wechseln zum Verzeichnis **/deploy/k8s**, das das Skript **gen-aks-env.ps1** enthält.

2. Sie führen das Skript zum Erstellen des Managed Kubernetes-Clusters mit AKS und ACR aus.

   ![AKS](./media/contoso-migration-rebuild/aks1.png)

3. Bei geöffneter Datei aktualisiert Contoso den $location-Parameter in **eastus2** und speichert die Datei.

   ![AKS](./media/contoso-migration-rebuild/aks2.png)

4. Sie wählen die Optionen **Ansicht** > **Integriertes Terminal** aus, um das integrierte Terminal in Visual Studio Code zu öffnen.

   ![AKS](./media/contoso-migration-rebuild/aks3.png)

5. In dem in PowerShell integrierten Terminal meldet Contoso sich bei Azure mit dem Befehl „Connect-AzureRmAccount“ an. Weitere Informationen zu den ersten Schritten mit PowerShell finden Sie [hier](https://docs.microsoft.com/powershell/azure/get-started-azureps).

   ![AKS](./media/contoso-migration-rebuild/aks4.png)

6. Contoso authentifiziert die Azure CLI, indem der Befehl `az login` ausgeführt wird und die Anweisungen für die Authentifizierung mithilfe eines Webbrowsers befolgt werden. Weitere Informationen zur Anmeldung bei der Azure CLI finden Sie [hier](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).

   ![AKS](./media/contoso-migration-rebuild/aks5.png)

7. Contoso führt den folgenden Befehl aus, übergibt den Ressourcengruppennamen von ContosoRG, den Namen des AKS-Clusters „smarthotel-aks-eus2“ und den Namen der neuen Registrierung.

   ```PowerShell
   .\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2
   ```

   ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. Azure erstellt eine andere Ressourcengruppe, die die Ressourcen für den AKS-Cluster enthält.

   ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. Nachdem die Bereitstellung abgeschlossen ist, installieren sie das Befehlszeilentool `kubectl`. Das Tool ist bereits in Azure Cloud Shell installiert.

   ```azurecli
   az aks install-cli
   ```

10. Contoso überprüft die Verbindung mit dem Cluster, indem es den Befehl `kubectl get nodes` ausführt. Der Knoten weist den gleichen Namen wie die VM in der automatisch erstellten Ressourcengruppe auf.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. Contoso führt den folgenden Befehl zum Starten des Kubernetes-Dashboards aus:

    ```azurecli
    az aks browse --resource-group ContosoRG --name smarthotelakseus2
    ```

12. Eine Browserregisterkarte wird auf dem Dashboard geöffnet. Hierbei handelt es sich um eine getunnelte Verbindung, die auf die Azure CLI zurückgreift.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)

## <a name="step-2-configure-the-back-end-pipeline"></a>Schritt 2: Konfigurieren der Back-End-Pipeline

### <a name="create-an-azure-devops-project-and-build"></a>Erstellen eines Azure DevOps-Projekts und -Builds

Contoso-Administratoren erstellen ein Azure DevOps-Projekt und konfigurieren einen CI-Build zum Erstellen des Containers und übertragen es dann mithilfe von Push an ACR. In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.

1. Unter „visualstudio.com“ erstellen sie eine neue Organisation (**contosodevops360.visualstudio.com**) und konfigurieren sie für die Verwendung von Git.

2. Sie erstellen ein neues Projekt (**SmartHotelBackend**) mithilfe von Git für die Versionskontrolle und Agile für den Workflow.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png)

3. Sie importieren das [GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png)

4. Sie wählen unter **Pipelines** die Option **Build** aus und erstellen mit Azure Repos Git als Quelle aus dem Repository eine neue Pipeline.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png)

5. Sie legen fest, dass mit einem leeren Auftrag begonnen wird.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)

6. Sie klicken auf **Gehostete Linux-Vorschau** für die Buildpipeline.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png)

7. Unter **Phase 1** fügt Contoso einen **Docker Compose**-Task hinzu. Dieser Task erstellt Docker Compose.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png)

8. Contoso wiederholt den **Docker Compose**-Task und fügt einen weiteren Task hinzu. Dieser überträgt die Container mithilfe von Push an ACR.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)

9. Contoso wählt den ersten Task (für die Erstellung) aus und konfiguriert den Build mit dem Azure-Abonnement, der Autorisierung und ACR.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

10. Sie geben den Pfad der Datei **docker-compose.yaml** im Ordner **src** des Repositorys an. Sie legen fest, dass Dienstimages erstellt werden und dass das aktuelle Tag eingebunden wird. Wenn die Aktion zu **Dienstimages erstellen** wechselt, ändert sich der Name des Azure DevOps-Tasks in **Dienste automatisch erstellen**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

11. Nun konfigurieren sie den zweiten Docker-Task (für die Übertragung mithilfe von Push). Das Unternehmen wählt das Abonnement und die ACR-Instanz **smarthotelacreus2** aus.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

12. Es gibt erneut die Datei für die Datei „docker-compose.yaml“ ein, klickt anschließend auf **Dienstimages mithilfe von Push übertragen** und schließt das aktuelle Tag ein. Wenn die Aktion zu **Dienstimages mithilfe von Push übertragen** wechselt, ändert sich der Name des Azure DevOps-Tasks in **Dienste automatisch mithilfe von Push übertragen**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

13. Nachdem die Azure DevOps-Tasks konfiguriert wurden, speichern Contoso-Administratoren die Buildpipeline und beginnt mit dem Buildprozess.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

14. Sie wählen den Buildauftrag aus, um den Status zu überprüfen.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

15. Wenn der Build fertiggestellt ist, zeigt ACR die neuen Repositorys an, die mit den von den Microservices verwendeten Containern aufgefüllt werden.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)

### <a name="deploy-the-back-end-infrastructure"></a>Bereitstellen der Back-End-Infrastruktur

Mithilfe des erstellten AKS-Clusters und der Docker-Imagebuilds stellen Contoso-Administratoren nun die restliche Infrastruktur bereit, die von Back-End-Microservices genutzt wird.

- In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.
- Im Ordner **/deploy/k8s/arm** gibt es ein einziges Skript zum Erstellen aller Elemente.

Die Bereitstellung erfolgt wie folgt:

1. Sie öffnen eine Developer-Eingabeaufforderung und verwenden den Befehl `az login` als Anmeldung für das Azure-Abonnement.

2. Sie verwenden die Datei „deploy.cmd“, um die Azure-Ressourcen in der Ressourcengruppe „ContosoRG“ und in der Region „USA, Osten 2“ (EUS2) bereitzustellen, indem sie den folgenden Befehl eingeben:

    ```azurecli
    .\deploy.cmd azuredeploy ContosoRG -c eastus2
    ```

    ![Bereitstellen des Back-Ends](./media/contoso-migration-rebuild/backend1.png)

3. Im Azure-Portal erfassen sie die Verbindungszeichenfolge für die einzelnen Datenbanken, die später verwendet werden.

    ![Bereitstellen des Back-Ends](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a>Erstellen der Back-End-Releasepipeline

Contoso-Administratoren gehen nun wie folgt vor:

- Sie stellen den NGINX-Eingangscontroller bereit, um eingehenden Datenverkehr für die Dienste zuzulassen.
- Sie stellen die Microservices für den AKS-Cluster bereit.
- In einem ersten Schritt aktualisieren sie die Verbindungszeichenfolgen zu den Microservices mithilfe von Azure DevOps. Sie konfigurieren eine neue Azure DevOps-Releasepipeline, um die Microservices bereitzustellen.
- In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.
- Einige der Konfigurationseinstellungen (z.B. Active Directory B2C) werden nicht in diesem Artikel behandelt. Weitere Informationen zu diesen Einstellungen finden Sie im Repository weiter oben.

Sie erstellen die Pipeline:

1. Mithilfe von Visual Studio aktualisieren sie die Datei **/deploy/k8s/config_local.yml** anhand der zuvor notierten Informationen zur Datenverbindung.

    ![Datenbankverbindungen](./media/contoso-migration-rebuild/back-pipe1.png)

2. Sie öffnen Azure DevOps und wählen im Projekt „SmartHotel360“ in **Releases** die Option **+Neue Pipeline** aus.

    ![Neue Pipeline](./media/contoso-migration-rebuild/back-pipe2.png)

3. Sie wählen **Leere Stufe** aus, um die Pipeline ohne Vorlage zu starten.
4. Sie geben den Phasen- und Pipelinenamen an.

      ![Phasenname](./media/contoso-migration-rebuild/back-pipe4.png)

      ![Pipelinename](./media/contoso-migration-rebuild/back-pipe5.png)

5. Sie fügen ein Artefakt hinzu.

     ![Hinzufügen des Artefakts](./media/contoso-migration-rebuild/back-pipe6.png)

6. Sie wählen **Git** als Quelltyp aus und geben Projekt, Quelle und Masterbranch für die App SmartHotel360 an.

    ![Artefakteinstellungen](./media/contoso-migration-rebuild/back-pipe7.png)

7. Sie wählen den Tasklink aus.

    ![Aufgabenlink](./media/contoso-migration-rebuild/back-pipe8.png)

8. Sie fügen eine neue Azure PowerShell-Aufgabe hinzu, sodass sie ein PowerShell-Skript in einer Azure-Umgebung ausführen können.

    ![PowerShell in Azure](./media/contoso-migration-rebuild/back-pipe9.png)

9. Sie wählen zunächst das Azure-Abonnement für die Aufgabe und anschließend das Skript **deploy.ps1** im Git-Repository aus.

    ![Ausführen des Skripts](./media/contoso-migration-rebuild/back-pipe10.png)

10. Sie fügen dem Skript Argumente hinzu. Das Skript löscht den gesamten Clusterinhalt (außer den **eingehenden Daten** und dem **Eingangscontroller**) und stellt die Microservices bereit.

    ![Skriptargumente](./media/contoso-migration-rebuild/back-pipe11.png)

11. Sie legen die bevorzugte Azure PowerShell-Version als neueste fest und speichern die Pipeline.

12. Sie kehren zur Seite **Release** zurück, und erstellen manuell ein neues Release.

    ![Neues Release](./media/contoso-migration-rebuild/back-pipe12.png)

13. Nach dem Erstellen wählen sie das Release und anschließend in **Aktionen** die Option **Bereitstellen** aus.

      ![Release bereitstellen](./media/contoso-migration-rebuild/back-pipe13.png)

14. Nach Abschluss der Bereitstellung führen sie mithilfe der Azure Cloud Shell folgenden Befehl aus, um den Status von Diensten zu überprüfen: `kubectl get services`.

## <a name="step-3-provision-front-end-services"></a>Schritt 3: Bereitstellen von Front-End-Diensten

Contoso-Administratoren müssen die Infrastruktur bereitstellen, die von den Front-End-Apps verwendet wird. Sie erstellen einen Blobspeichercontainer zum Speichern der Bilder der Haustiere, die Cosmos DB-Datenbank zum Speichern von Dokumenten mit den Informationen zu den Haustieren und die Maschinelles Sehen-API für die Website.

In den Anweisungen für diesen Abschnitt wird das Repository [SmartHotel360-Website](https://github.com/Microsoft/SmartHotel360-Website) verwendet.

### <a name="create-blob-storage-containers"></a>Erstellen von Blob Storage-Containern

1. Sie öffnen im Azure-Portal das erstellte Speicherkonto und wählen anschließend **Blobs** aus.
2. Es erstellt einen neuen Container (**Haustiere**), bei dem die öffentliche Zugriffsebene auf Container festgelegt ist. Benutzer laden ihre Fotos von Haustieren in diesen Container hoch.

    ![Speicherblob](./media/contoso-migration-rebuild/blob1.png)

3. Es erstellt einen zweiten neuen Container namens **Einstellungen**. Eine Datei mit allen Front-End-App-Einstellungen wird in diesen Container platziert.

    ![Speicherblob](./media/contoso-migration-rebuild/blob2.png)

4. Es speichert die Zugriffsdetails für das Speicherkonto in einer Textdatei zur späteren Verwendung.

    ![Speicherblob](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-a-cosmos-database"></a>Bereitstellen einer Cosmos DB-Datenbank

Contoso-Administratoren stellen eine Cosmos DB-Datenbank bereit, die für Informationen zu Haustieren verwendet wird.

1. Contoso erstellt eine **Azure Cosmos DB**-Instanz im Azure Marketplace.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. Contoso gibt einen Namen (**contososmarthotel**) an, wählt die SQL-API aus und fügt sie in die Produktionsressourcengruppe „ContosoRG“ in der Hauptregion „USA, Osten 2“ ein.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. Contoso fügt eine neue Sammlung zur Datenbank mit Standardkapazität und -durchsatz hinzu.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)

4. Contoso nimmt die Verbindungsinformationen für die Datenbank für die zukünftige Verwendung zur Kenntnis.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)

### <a name="provision-computer-vision"></a>Bereitstellen der Maschinelles Sehen-API

Contoso-Administratoren stellen die Maschinelles Sehen-API bereit. Die API wird von der Funktion zum Auswerten der Bilder aufgerufen, die von den Benutzern hochgeladen wurden.

1. Contoso erstellt im Azure Marketplace eine **Maschinelles Sehen**-Instanz.

     ![Maschinelles Sehen](./media/contoso-migration-rebuild/vision1.png)

2. Contoso stellt die API (**smarthotelpets**) in der Produktionsressourcengruppe „ContosoRG“ in der Hauptregion „USA, Osten 2“ bereit.

    ![Maschinelles Sehen](./media/contoso-migration-rebuild/vision2.png)

3. Contoso speichert die Verbindungseinstellungen für die API in einer Textdatei zur späteren Verwendung.

     ![Maschinelles Sehen](./media/contoso-migration-rebuild/vision3.png)

### <a name="provision-the-azure-web-app"></a>Bereitstellen der Azure-Web-App

Contoso-Administratoren stellen die Web-App mithilfe des Azure-Portals bereit.

1. Das Unternehmen wählt **Web-App** im Portal aus.

    ![Web-App](./media/contoso-migration-rebuild/web-app1.png)

2. Sie geben einen App-Namen an (**smarthotelcontoso**), führen die App unter Windows aus und platzieren sie in der Produktionsressourcengruppe **ContosoRG**. Sie erstellen eine neue Application Insights-Instanz zur App-Überwachung.

    ![Web-App-Name](./media/contoso-migration-rebuild/web-app2.png)

3. Anschließend navigieren sie zur Adresse der Apps, um zu überprüfen, ob diese erfolgreich erstellt wurden.

4. Im Azure-Portal erstellen sie nun einen Stagingslot für den Code. Die Pipeline wird für diesen Slot bereitgestellt. Dadurch wird sichergestellt, dass Code erst in die Produktionsumgebung gelangt, wenn Administratoren ein Release ausführen.

    ![Web-App-Stagingslot](./media/contoso-migration-rebuild/web-app3.png)

### <a name="provision-the-azure-function-app"></a>Bereitstellen der Azure-Funktionen-App

Contoso-Administratoren stellen im Azure-Portal die Funktionen-App bereit.

1. Sie wählen **Funktionen-App** aus.

   ![Erstellen einer Funktionen-App](./media/contoso-migration-rebuild/function-app1.png)

2. Sie geben einen App-Namen an (**smarthotelpetchecker**). Es platziert die Ressource in der Produktionsressourcengruppe **ContosoRG**. Es legt den Hostingort auf **Verbrauchstarif** fest und platziert die App in der Region USA, Osten 2. Daraufhin wird neben einem neuen Speicherkonto auch eine Application Insights-Instanz für die Überwachung erstellt.

   ![Einstellungen für Funktions-Apps](./media/contoso-migration-rebuild/function-app2.png)

3. Nach der Bereitstellung der App navigieren sie zur Adresse der App, um zu überprüfen, ob diese erfolgreich erstellt wurde.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Schritt 4: Einrichten der Front-End-Pipeline

Contoso-Administratoren erstellen zwei verschiedene Projekte für die Front-End-Website.

1. In Azure DevOps erstellen sie ein **SmartHotelFrontend**-Projekt.

   ![Front-End-Projekt](./media/contoso-migration-rebuild/function-app1.png)

2. Sie importieren das Git-Repository [SmartHotel360 front end](https://github.com/Microsoft/SmartHotel360-Website) in das neue Projekt.

3. Für die Funktions-App erstellen sie ein weiteres Azure DevOps-Projekt (**SmartHotelPetChecker**) und importieren das Git-Repository [PetChecker](https://github.com/sonahander/SmartHotel360-PetCheckerFunction) in dieses Projekt.

### <a name="configure-the-web-app"></a>Konfigurieren der Web-App

Contoso-Administratoren konfigurieren nun die Web-App zur Verwendung von Contoso-Ressourcen.

1. Sie stellen eine Verbindung mit dem Azure DevOps-Projekt her und klonen das Repository lokal auf dem Entwicklungscomputer.
2. In Visual Studio öffnet Contoso den Ordner, um alle Dateien im Repository anzuzeigen.

    ![Repositorydateien](./media/contoso-migration-rebuild/configure-webapp1.png)

3. Sie aktualisieren ggf. die Konfigurationsänderungen.

    - Wenn die Web-App gestartet wird, sucht es nach der App-Einstellung **SettingsUrl**.
    - Diese Variable muss eine URL enthalten, die auf eine Konfigurationsdatei zeigt.
    - Standardmäßig wird die Einstellung als öffentlicher Endpunkt verwendet.

4. Sie aktualisieren die Datei „/config-sample.json/sample.json“.

    - Dies ist die Konfigurationsdatei für das Web, wenn der öffentliche Endpunkt verwendet wird.
    - Sie bearbeiten die Abschnitte **urls** und **pets_config** mit den Werten für die AKS-API-Endpunkte, die Speicherkonten und die Cosmos DB-Datenbank.
    - Die URLs sollten dem DNS-Namen der neuen Web-App entsprechen, die von Contoso erstellt wird.
    - Bei Contoso lautet dieser **smarthotelcontoso.eastus2.cloudapp.azure.com**.

    ![JSON-Einstellungen](./media/contoso-migration-rebuild/configure-webapp2.png)

5. Nachdem die Datei aktualisiert wurde, benennen sie diese in **smarthotelsettingsurl** um und laden sie in den Blobspeicher hoch, den sie zuvor erstellt haben.

    ![Umbenennen und hochladen](./media/contoso-migration-rebuild/configure-webapp3.png)

6. Sie wählen die Datei aus, um die URL abzurufen. Diese URL wird von der App beim Abrufen der Konfigurationsdatei verwendet.

    ![URL der App](./media/contoso-migration-rebuild/configure-webapp4.png)

7. Sie aktualisieren **SettingsUrl** in der Datei **appsettings.Production.json** in die URL der neuen Datei.

    ![URL für das Update](./media/contoso-migration-rebuild/configure-webapp5.png)

### <a name="deploy-the-website-to-azure-app-service"></a>Bereitstellen der Website in Azure App Service

Contoso-Administratoren können die Website jetzt veröffentlichen.

1. Sie öffnen Azure DevOps und wählen im Projekt **SmartHotelFrontend** in **Builds and Releases** (Builds und Releases) die Option **+Neue Pipeline** aus.
2. Sie wählen **Azure DevOps-Git** als Quelle aus.
3. Sie wählen die Vorlage **ASP.NET Core** aus.
4. Sie überprüfen in der Pipeline, ob die Optionen **Webprojekte veröffentlichen** und **Veröffentlichte Projekte komprimieren** ausgewählt wurden.

    ![Pipelineeinstellungen](./media/contoso-migration-rebuild/vsts-publish-front2.png)

5. Unter **Trigger** aktivieren sie Continuous Integration und fügen den Masterbranch hinzu. Dadurch wird sichergestellt, dass die Buildpipeline jedes Mal startet, wenn die Lösung neuen Code für den Masterbranch committet.

    ![Continuous Integration](./media/contoso-migration-rebuild/vsts-publish-front3.png)

6. Sie wählen **Speichern und in Warteschlange einreihen** aus, um einen Buildvorgang zu starten.
7. Nach Abschluss des Buildvorgangs konfigurieren sie eine Releasepipeline mithilfe der **Azure App Service-Bereitstellung**.
8. Sie geben den Phasennamen **Staging** an.

    ![Umgebungsname](./media/contoso-migration-rebuild/vsts-publish-front4.png)

9. Sie fügen ein Artefakt hinzu und wählen Build aus, den sie konfiguriert haben.

     ![Hinzufügen des Artefakts](./media/contoso-migration-rebuild/vsts-publish-front5.png)

10. Sie wählen das Blitzsymbol des Artefakts aus, um Continuous Deployment zu aktivieren.

    ![Kontinuierliche Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front6.png)
11. Sie wählen in **Umgebung** unter **Staging** die Option **1 job, 1 task** (1 Auftrag, 1 Aufgabe) aus.
12. Nachdem sie das Abonnement und den App-Namen ausgewählt haben, öffnen sie die Aufgabe **Deploy Azure App Service** (Azure App Service bereitstellen). Die Bereitstellung wurde für die Verwendung des Bereitstellungsslots **Staging** konfiguriert. Dadurch wird automatisch Code zur Überprüfung und Genehmigung in diesem Slot erstellt.

     ![Slot](./media/contoso-migration-rebuild/vsts-publish-front7.png)

13. In der **Pipeline** fügen sie eine neue Phase hinzu.

    ![Neue Umgebung](./media/contoso-migration-rebuild/vsts-publish-front8.png)

14. Sie wählen **Azure App Service-Bereitstellung mit Slot** aus und geben der Umgebung den Namen **Prod**.
15. Sie wählen **1 job, 2 tasks** (1 Auftrag, 2 Aufgaben) und dann das Abonnement, den App Service-Namen und den Slot **Staging** aus.

    ![Umgebungsname](./media/contoso-migration-rebuild/vsts-publish-front10.png)

16. Sie entfernen **Deploy Azure App Service to Slot** (Azure App Service in Slot bereitstellen) aus der Pipeline. Diese Aufgabe wurde in den vorherigen Schritten dort eingefügt.

    ![Aus Pipeline entfernen](./media/contoso-migration-rebuild/vsts-publish-front11.png)

17. Sie speichern die Pipeline. Sie wählen in der Pipeline **Bedingungen nach der Bereitstellung** aus.

    ![Nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front12.png)

18. Sie aktivieren **Genehmigungen nach der Bereitstellung** und fügen eine Entwicklungsleitung als genehmigende Person hinzu.

    ![Genehmigung nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front13.png)

19. Sie starten in der Buildpipeline einen Build. Dadurch wird die neue Releasepipeline ausgelöst, wodurch wiederum die Website im Stagingslot bereitgestellt wird. Bei Contoso lautet die URL für den Slot `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Nach Abschluss des Buildvorgangs und nachdem das Release im Slot bereitgestellt wurde, sendet Azure DevOps für die Genehmigung eine E-Mail an die Entwicklungsleitung.

21. Die Entwicklungsleitung wählt **Genehmigung anzeigen** aus und kann dann die Anforderung im Azure DevOps-Portal genehmigen oder ablehnen.

    ![Genehmigungs-E-Mail](./media/contoso-migration-rebuild/vsts-publish-front14.png)

22. Die Leitung erstellt einen Kommentar und genehmigt die Anforderung. Dadurch beginnt der Austausch der Slots **Staging** und **Prod**. Zudem wird der Build in die Produktionsumgebung verschoben.

    ![Genehmigen und austauschen](./media/contoso-migration-rebuild/vsts-publish-front15.png)

23. Der Austausch wird durch die Pipeline abgeschlossen.

    ![Vollständiger Austausch](./media/contoso-migration-rebuild/vsts-publish-front16.png)

24. Das Team überprüft den Slot **prod**, um sicherzustellen, dass sich die Web-App in der Produktionsumgebung unter `https://smarthotelcontoso.azurewebsites.net/` befindet.

### <a name="deploy-the-petchecker-function-app"></a>Bereitstellen der Funktions-App PetChecker

Contoso-Administratoren stellen die App wie folgt bereit.

1. Sie klonen das Repository lokal auf dem Entwicklungscomputer, indem sie eine Verbindung mit dem Azure DevOps-Projekt herstellen.
2. In Visual Studio öffnet Contoso den Ordner, um alle Dateien im Repository anzuzeigen.
3. Sie öffnen die Datei **src/PetCheckerFunction/local.settings.json** und fügen die App-Einstellungen für Speicher, Cosmos-Datenbank und Maschinelles Sehen-API hinzu.

    ![Bereitstellen der Funktion](./media/contoso-migration-rebuild/function5.png)

4. Sie führen für den Code einen Commit aus, synchronisieren ihn mit Azure DevOps und übertragen so ihre Änderungen mithilfe von Push.
5. Sie fügen eine neue Buildpipeline hinzu und wählen anschließend **Azure DevOps-Git** für die Quelle aus.
6. Sie wählen die Vorlage **ASP.NET Core (.NET Framework)** aus.
7. Sie übernehmen die Standardwerte für die Vorlage.
8. In **Trigger** wählen sie **Continuous Integration aktivieren** und anschließend **Speichern und in Warteschlange einreihen** aus, um einen Buildvorgang zu starten.
9. Nach dem erfolgreichen Ausführen des Buildvorgangs erstellen sie eine Releasepipeline, indem sie **Azure App Service-Bereitstellung mit Slot** hinzufügen.
10. Sie geben der Umgebung den Namen **Prod** und wählen anschließend das Abonnement aus. Sie legen den **App-Typ** auf **Funktionen-App** und den App Service-Namen auf **smarthotelpetchecker** fest.

    ![Funktionen-App](./media/contoso-migration-rebuild/petchecker2.png)

11. Sie fügen einen Artefakt-**Build** hinzu.

    ![Artefakt](./media/contoso-migration-rebuild/petchecker3.png)

12. Sie aktivieren **Continuous Deployment-Trigger** und wählen anschließend **Speichern** aus.
13. Sie wählen **Neuen Build in Warteschlange** aus, um die ganze CI/CD-Pipeline auszuführen.
14. Nachdem die Funktion bereitgestellt wurde, wird sie im Azure-Portal mit dem Status **Wird ausgeführt** angezeigt.

    ![Bereitstellen der Funktion](./media/contoso-migration-rebuild/function6.png)

15. Contoso navigiert zur App unter [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets), um zu testen, ob die Pet Checker-App wie erwartet funktioniert.

16. Sie wählen den Avatar aus, um ein Bild hochzuladen.

    ![Bereitstellen der Funktion](./media/contoso-migration-rebuild/function7.png)

17. Das erste Foto, das überprüft werden soll, ist das eines kleinen Hundes.

    ![Bereitstellen der Funktion](./media/contoso-migration-rebuild/function8.png)

18. Die App gibt eine Meldung zur Bestätigung zurück.

    ![Bereitstellen der Funktion](./media/contoso-migration-rebuild/function9.png)

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso nun die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neuen Datenbanken geschützt sind. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Die App muss für die Verwendung von SSL mit Zertifikaten aktualisiert werden. Die Containerinstanz sollte erneut bereitgestellt werden, um auf 443 zu antworten.
- Zum Schutz von Geheimnissen für die Service Fabric-Apps sollte Contoso die Verwendung von Key Vault in Erwägung ziehen. [Weitere Informationen](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management)

### <a name="backups-and-disaster-recovery"></a>Sicherungen und Notfallwiederherstellung

- Contoso muss die [Sicherungsanforderungen für Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) überprüfen.
- Contoso sollte die Implementierung von [SQL-Failovergruppen berücksichtigen, um ein regionales Failover für die Datenbank bereitzustellen](https://docs.microsoft.com/azure/sql-database/sql-database-auto-failover-group).
- Contoso kann die [Georeplikation für die Premium-SKU von ACR](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication) nutzen.
- Cosmos DB führt automatisch Sicherungen durch. Contoso kann sich über diesen Prozess [informieren](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über EA verrechnet.
- Contoso aktiviert das [Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde die App SmartHotel360 in Azure von Contoso neu erstellt. Die lokale VM für das App-Front-End wurde in Azure App Service-Web-Apps neu erstellt. Das Back-End der Anwendung wird mithilfe von Microservices erstellt, die für Container bereitgestellt werden, die von Azure Kubernetes Service (AKS) verwaltet werden. Die App-Funktionalität hat Contoso durch eine App für Fotos von Haustieren verbessert.

## <a name="suggested-skills"></a>Empfohlene Qualifikationen

Microsoft Learn ist ein neuer Lernansatz. Die Bereitschaft zu den neuen Qualifikationen und Aufgaben, die mit der Cloudeinführung verbunden sind, entsteht nicht problemlos. Microsoft Learn bietet einen lohnenderen Ansatz für praktisches Lernen, der Ihnen hilft, Ihre Ziele schneller zu erreichen. Punkte sammeln, zu höheren Stufen aufsteigen und mehr erreichen.

Hier finden Sie einige Beispiele für maßgeschneiderte Lernpfade auf Microsoft Learn, die auf die App Contoso SmartHotel360 in Azure abgestimmt sind.

[Bereitstellen einer Website in Azure mithilfe von Azure App Service:](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service) Mit Web-Apps in Azure können Sie Ihre Website leicht veröffentlichen und verwalten, ohne dass Sie mit den zugrunde liegenden Servern, Speicher oder Netzwerkressourcen arbeiten müssen. Stattdessen können Sie sich auf Ihre Websitefeatures konzentrieren und die stabile Azure-Plattform verwenden, um sicheren Zugriff auf Ihre Site bereitzustellen.

[Verarbeiten und Klassifizieren von Images mit der Bildanalyse von Azure Cognitive Services:](https://docs.microsoft.com/learn/paths/classify-images-with-vision-services) Azure Cognitive Services bietet vorgefertigte Funktionen, um die Funktionalität für maschinelles Sehen in Ihren Anwendungen zu aktivieren. Erfahren Sie, wie Sie die Bildanalyse von Cognitive Services verwenden, um Gesichter zu erkennen, Bilder mit Tags zu versehen und zu klassifizieren und Objekte zu identifizieren.
