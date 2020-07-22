---
title: Erneutes Erstellen einer lokalen Anwendung in Azure
description: In diesem Artikel erfahren Sie, wie Contoso eine Anwendung in Azure mithilfe von Azure App Service, Kubernetes Services, Cosmos DB, Functions und Cognitive Services neu erstellt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 7/1/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 280c2712528f0dd5b46bc17af6fde416ba499661
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86235091"
---
<!-- docsTest:ignore "Enable .NET" SmartHotel360 SmartHotel360-Backend Pet.Checker contoso-datacenter git aks PetCheckerFunction -->

<!-- cSpell:ignore givenscj SQLVM WEBVM contosohost vcenter contosodc smarthotel contososmarthotel smarthotelcontoso smarthotelpetchecker petchecker smarthotelakseus smarthotelacreus smarthotelpets kubectl contosodevops visualstudio azuredeploy cloudapp smarthotelsettingsurl appsettings -->

# <a name="rebuild-an-on-premises-application-in-azure"></a>Erneutes Erstellen einer lokalen Anwendung in Azure

Dieser Artikel zeigt, wie das fiktive Unternehmen Contoso eine zweistufige Windows .NET-Anwendung, die auf VMware-VMs ausgeführt wird, als Teil einer Migration zu Azure neu erstellt. Contoso migriert die Front-End-VM zu einer Azure App Service-Web-App. Das Back-End der Anwendung wird mithilfe von Microservices erstellt, die für Container bereitgestellt werden, die von Azure Kubernetes Service (AKS) verwaltet werden. Die Website interagiert mit Azure Functions zum Bereitstellen der Funktionalität für Fotos von Haustieren.

Die in diesem Beispiel verwendete SmartHotel360-Anwendung wird als Open Source bereitgestellt. Wenn Sie diese App für Ihre eigenen Tests verwenden möchten, können Sie sie von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Unternehmenswachstum.** Contoso wächst und möchte für seine Kunden differenzierte Funktionen auf seinen Websites bereitstellen.
- **Mehr Flexibilität.** Contoso muss schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss das Contoso-IT-Team Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Senken Sie Kosten.** Contoso möchte die Lizenzierungskosten minimieren.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat folgende Anwendungsanforderungen für diese Migration gestellt. Anhand dieser Anforderungen wird die beste Migrationsmethode bestimmt:

- Die Anwendung wird in Azure so wichtig bleiben wie bisher. Sie sollte reibungslos laufen und sich mühelos skalieren lassen.
- Die Anwendung darf nicht auf IaaS-Komponenten basieren. Sie sollte für die Verwendung von PaaS- oder serverlosen Diensten ausgelegt sein.
- Die Builds der Anwendung sollten in Clouddiensten ausgeführt werden und Container sollten sich in einer privaten unternehmensweiten Registrierung in der Cloud befinden.
- Die API-Dienst für Fotos von Haustieren sollte in der Praxis präzise und zuverlässig sein, da die von der Anwendung getroffenen Entscheidungen in den Hotels berücksichtigt werden müssen. Haustiere, denen der Zutritt erlaubt ist, dürfen in den Hotels bleiben.
- Um die Anforderungen für eine DevOps-Pipeline zu erfüllen, verwendet Contoso für die Quellcodeverwaltung ein Git-Repository in Azure Repos. Mithilfe automatisierter Builds und Releases wird der Code erstellt und in Azure App Service, Azure Functions und AKS bereitgestellt.
- Für Microservices im Back-End und für die Website im Front-End sind unterschiedliche Pipelines für Continuous Integration/Continuous Development (CI/CD) erforderlich.
- Für die Back-End-Dienste gelten andere Releasezyklen als für die Front-End-Web-App. Zur Erfüllung dieser Anforderung werden zwei verschiedene Pipelines bereitgestellt.
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
- Das Back-End der Website wird mithilfe von Microservices erstellt. Diese Dienste werden für Container bereitgestellt, die in AKS verwaltet werden.
- Container werden mithilfe von Azure DevOps erstellt und mithilfe von Push an Azure Container Registry übertragen.
- Vorerst stellt Contoso die Web-App und den Funktionscode mithilfe von Visual Studio manuell bereit.
- Microservices werden mithilfe eines PowerShell-Skripts bereitgestellt, das Kubernetes-Befehlszeilentools aufruft.

    ![Szenarioarchitektur](./media/contoso-migration-rebuild/architecture.png) _Abbildung 1: Szenarioarchitektur._

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Durch den Einsatz von PaaS- und serverlosen Lösungen für die End-to-End-Bereitstellung verkürzt sich die Verwaltungszeit, die Contoso aufwenden muss, um ein Vielfaches. <br><br> Die Migration zu einer auf Microservices basierenden Architektur bietet Contoso die Möglichkeit, die Lösung ganz einfach im Lauf der Zeit zu erweitern. <br><br> Neue Funktionalität kann online geschaltet werden, ohne dass vorhandene Codebasen von Lösungen beeinträchtigt werden. <br><br> Die Web-App wird mit mehreren Instanzen ohne Single Point of Failure konfiguriert. <br><br> Die automatische Skalierung wird aktiviert, damit die Anwendung unterschiedlich hohe Datenverkehrsvolumen verarbeiten kann. <br><br> Mit dem Wechsel zu PaaS-Diensten kann Contoso veraltete Lösungen, die unter dem Betriebssystem Windows Server 2008 R2 ausgeführt werden, außer Betrieb nehmen. <br><br> Azure Cosmos DB weist eine integrierte Fehlertoleranz auf, die keinen Konfigurationsaufwand seitens Contoso erfordert. Dies bedeutet, dass die Datenschicht kein Single Point of Failover mehr ist. |
| **Nachteile** | Container sind komplexer als andere Migrationsoptionen. Die Lernkurve könnte für Contoso ein Problem darstellen. Der Grad der Komplexität steigt und bietet trotz der Kurve einen hohen Nutzen. <br><br> Das Betriebsteam von Contoso muss eingearbeitet werden, um Azure, Container und Microservices für die Anwendung verstehen und unterstützen zu können. <br><br> Contoso hat noch nicht vollständig DevOps für die gesamte Lösung implementiert. Dies muss Contoso bei der Bereitstellung von Diensten für AKS, Azure Functions und Azure App Service berücksichtigen. |

### <a name="migration-process"></a>Migrationsprozess

1. Contoso stellt Azure Container Registry, AKS und Azure Cosmos DB bereit.
2. Contoso stellt die Infrastruktur für die Bereitstellung bereit, darunter die Azure App Service-Web-App, ein Speicherkonto, Funktionen und API.
3. Sobald die Infrastruktur eingerichtet ist, erstellt Contoso Microservices-Containerimages mithilfe von Azure DevOps, das diese mithilfe von Push an die Containerregistrierung überträgt.
4. Contoso stellt diese Microservices mithilfe eines PowerShell-Skripts in AKS bereit.
5. Abschließend stellt Contoso die Funktion und die Web-App bereit.

    ![Der Migrationsvorgang](./media/contoso-migration-rebuild/migration-process.png) _Abbildung 2: Der Migrationsvorgang._

### <a name="azure-services"></a>Azure-Dienste

| Dienst | BESCHREIBUNG | Kosten |
|---|---|---|
| [AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Vereinfacht die Verwaltung, die Bereitstellung und den Betrieb von Kubernetes. Nutzt einen vollständig verwalteten Orchestrierungsdienst für Kubernetes-Container. | AKS ist ein kostenloser Dienst. Nur die VMs sowie die entsprechenden verbrauchten Speicher- und Netzwerkressourcen müssen bezahlt werden. [Weitere Informationen](https://azure.microsoft.com/pricing/details/kubernetes-service) |
| [Azure-Funktionen](https://azure.microsoft.com/services/functions) | Beschleunigt die Entwicklung mit einer ereignisbasierten, serverlosen Computeumgebung. Die Skalierung erfolgt bedarfsabhängig. | Nur verbrauchte Ressourcen müssen bezahlt werden. Der Plan wird basierend auf dem Ressourcenverbrauch und den Ausführungen pro Sekunde berechnet. [Weitere Informationen](https://azure.microsoft.com/pricing/details/functions) |
| [Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Speichert Images für alle Arten von Containerbereitstellungen. | Die Kosten ergeben sich aus Features, Speicher und Nutzungsdauer. [Weitere Informationen](https://azure.microsoft.com/pricing/details/container-registry) |
| [Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Es können schnell Web-Apps, mobile Apps und API-Apps der Unternehmensklasse auf jeder Plattform erstellt, bereitgestellt und skaliert werden. | App Service-Pläne werden sekundengenau abgerechnet. [Weitere Informationen](https://azure.microsoft.com/pricing/details/app-service/windows) |

## <a name="prerequisites"></a>Voraussetzungen

Für dieses Szenario benötigt Contoso Folgendes:

| Requirements (Anforderungen) | Details |
| --- | --- |
| Azure-Abonnement | <li> Contoso hat in einem früheren Artikel Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <li> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <li> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. |
| Azure-Infrastruktur | <li> Informieren Sie sich, [wie Contoso eine Azure-Infrastruktur einrichtet](./contoso-migration-infrastructure.md). |
| Voraussetzungen für Entwickler | Contoso benötigt die folgenden Tools auf einer Entwicklerarbeitsstation: <li>  [Visual Studio Community 2017: Version 15.5](https://visualstudio.microsoft.com) <li> Aktivieren von .NET-Workload. <li> [Git-Client](https://git-scm.com) <li> [Azure PowerShell](https://azure.microsoft.com/downloads) <li> [Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) <li> [Docker Community Edition (Windows 10) oder Docker Enterprise Edition (Windows Server)](https://docs.docker.com/docker-for-windows/install) für die Verwendung von Windows-Containern festgelegt. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen von AKS und Azure Container Registry.** Contoso stellt mithilfe von PowerShell den verwalteten AKS-Cluster und die Containerregistrierung bereit.
> - **Schritt 2: Erstellen von Docker-Containern:** Contoso richtet fortlaufende Integration (Continuous Integration, CI) für Docker-Container mithilfe von Azure DevOps ein und pusht sie an die Containerregistrierung.
> - **Schritt 3: Bereitstellen von Back-End-Microservices:** Es stellt die restliche Infrastruktur bereit, die von Back-End-Microservices genutzt wird.
> - **Schritt 4: Bereitstellen der Front-End-Infrastruktur:** Contoso stellt die Front-End-Infrastruktur bereit, einschließlich Blob Storage für die Fotos von Haustieren, Azure Cosmos DB und der Maschinelles Sehen-API.
> - **Schritt 5: Migrieren des Back-Ends:** Es stellt Microservices bereit und führt diese in AKS aus, um das Back-End zu migrieren.
> - **Schritt 6: Veröffentlichen des Front-Ends:** Es veröffentlicht die Anwendung SmartHotel360 in Azure App Service und die vom Haustierdienst aufgerufene Funktionen-App.

## <a name="step-1-provision-back-end-resources"></a>Schritt 1: Bereitstellen von Back-End-Ressourcen

Contoso-Administratoren führen ein Bereitstellungsskript zum Erstellen des Managed Kubernetes-Clusters mithilfe von AKS und Azure Container Registry aus. In den Anweisungen für diesen Abschnitt wird das GitHub-Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet. Das Repository enthält die gesamte Software für diesen Teil der Bereitstellung.

### <a name="ensure-prerequisites"></a>Erfüllen der Voraussetzungen

Vor Beginn stellen Contoso-Administratoren sicher, dass auf dem Entwicklungscomputer, den sie für die Bereitstellung verwenden, die erforderliche Software installiert ist. Sie klonen das Repository mithilfe von Git lokal auf dem Entwicklungscomputer:

`git clone https://github.com/Microsoft/SmartHotel360-Backend.git`

### <a name="provision-aks-and-azure-container-registry"></a>Bereitstellen von AKS und Azure Container Registry

Die Contoso-Administratoren führen die Bereitstellung wie folgt durch:

1. Sie öffnen den Ordner mit Visual Studio Code und wechseln zum Verzeichnis `/deploy/k8s`, das das Skript `gen-aks-env.ps1` enthält.

2. Sie führen das Skript zum Erstellen des Managed Kubernetes-Clusters mithilfe von AKS und Azure Container Registry aus.

    ![AKS](./media/contoso-migration-rebuild/aks1.png) _Abbildung 3: Erstellen des verwalteten Kubernetes-Cluster._

3. Bei geöffneter Datei aktualisieren sie den $location-Parameter in `eastus2` und speichern die Datei.

    ![AKS](./media/contoso-migration-rebuild/aks2.png) _Abbildung 4: Speichern der Datei._

4. Sie wählen **Ansicht** > **Terminal** aus, um das integrierte Terminal in Visual Studio Code zu öffnen.

    ![AKS](./media/contoso-migration-rebuild/aks3.png) _Abbildung 5: Das Terminal in Visual Studio Code._

5. In dem in PowerShell integrierten Terminal melden sie sich bei Azure mit dem Befehl `Connect-AzureRmAccount` an. Weitere Informationen finden Sie unter [Erste Schritte mit Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

    ![AKS](./media/contoso-migration-rebuild/aks4.png) _Abbildung 6: Das integrierte PowerShell-Terminal._

6. Sie authentifizieren die Azure CLI, indem der Befehl `az login` ausgeführt wird und die Anweisungen für die Authentifizierung mithilfe eines Webbrowsers befolgt werden. Weitere Informationen zur Anmeldung bei der Azure CLI finden Sie [hier](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).

    ![AKS](./media/contoso-migration-rebuild/aks5.png) _Abbildung 7: Authentifizierung der Azure CLI._

7. Sie führen den folgenden Befehl aus, mit dem der Ressourcengruppenname `ContosoRG`, der Name des AKS-Clusters `smarthotel-aks-eus2` und der neue Registrierungsname übergeben wird.

    `.\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2`

    ![AKS](./media/contoso-migration-rebuild/aks6.png) _Abbildung 8: Ausführung des Befehls._

8. Azure erstellt eine andere Ressourcengruppe, die die Ressourcen für den AKS-Cluster enthält.

    ![AKS](./media/contoso-migration-rebuild/aks7.png) _Abbildung 9: Azure erstellt eine Ressourcengruppe._

9. Nachdem die Bereitstellung abgeschlossen ist, installieren sie das Befehlszeilentool `kubectl`. Das Tool ist bereits in Azure Cloud Shell installiert.

    `az aks install-cli`

10. Contoso überprüft die Verbindung mit dem Cluster, indem es den Befehl `kubectl get nodes` ausführt. Der Knoten weist den gleichen Namen wie die VM in der automatisch erstellten Ressourcengruppe auf.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)
     _Abbildung 10: Die Verbindung mit dem Cluster wird überprüft._

11. Sie führen den folgenden Befehl zum Starten des Kubernetes-Dashboards aus:

    `az aks browse --resource-group ContosoRG --name smarthotelakseus2`

12. Eine Browserregisterkarte wird auf dem Dashboard geöffnet. Hierbei handelt es sich um eine getunnelte Verbindung, die auf die Azure CLI zurückgreift.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)
     _Abbildung 11: Eine getunnelte Verbindung._

## <a name="step-2-configure-the-back-end-pipeline"></a>Schritt 2: Konfigurieren der Back-End-Pipeline

### <a name="create-an-azure-devops-project-and-build"></a>Erstellen eines Azure DevOps-Projekts und -Builds

Contoso erstellt ein Azure DevOps-Projekt, konfiguriert einen CI-Build zum Erstellen des Containers und überträgt ihn dann mithilfe von Push an die Containerregistrierung. In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.

1. Unter `visualstudio.com` erstellen sie eine neue Organisation (`contosodevops360.visualstudio.com`) und konfigurieren sie für die Verwendung von Git.

2. Sie erstellen ein neues Projekt (`SmartHotelBackend`), wobei **Git** für die Versionskontrolle und **Agile** für den Workflow ausgewählt wird.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png) _Abbildung 12: Erstellen eines neuen Projekts._

3. Sie importieren das [GitHub-Repository](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png) _Abbildung 13: Importieren des GitHub-Repositorys._

4. Sie wählen unter **Pipelines** die Option **Build** aus und erstellen mit Azure Repos Git als Quelle aus dem Repository eine neue Pipeline.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png) _Abbildung 14: Eine neue Pipeline wird erstellt._

5. Sie legen fest, dass mit einem leeren Auftrag begonnen wird.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png) _Abbildung 15: Starten mit einem leeren Auftrag._

6. Sie klicken auf **Gehostete Linux-Vorschau** für die Buildpipeline.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png) _Abbildung 16: Einrichten der Buildpipeline._

7. Unter **Phase 1** fügt Contoso einen **Docker Compose**-Task hinzu. Dieser Task erstellt Docker Compose.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png) _Abbildung 17: Docker Compose wird erstellt._

8. Contoso wiederholt den **Docker Compose**-Task und fügt einen weiteren Task hinzu. Hierdurch werden die Container mithilfe von Push an die Containerregistrierung übertragen.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png) _Abbildung 18: Ein weiterer Docker Compose-Task wird hinzugefügt._

9. Contoso wählt den ersten Task für die Erstellung aus und konfiguriert den Build mit dem Azure-Abonnement, der Autorisierung und der Containerregistrierung.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png) _Abbildung 19: Erstellen und Konfigurieren des Builds._

10. Sie geben den Pfad der Datei `docker-compose.yaml` im Ordner `src` des Repositorys an. Sie legen fest, dass Dienstimages erstellt werden und dass das aktuelle Tag eingebunden wird. Wenn die Aktion zu **Dienstimages erstellen** wechselt, ändert sich der Name des Azure DevOps-Tasks in **Dienste automatisch erstellen**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)
     _Abbildung 20: Die Besonderheiten des Tasks._

11. Nun konfigurieren sie den zweiten Docker-Task (für die Übertragung mithilfe von Push). Sie wählen das Abonnement und die Containerregistrierung (`smarthotelacreus2`) aus.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)
     _Abbildung 21: Konfigurieren des zweiten Docker-Tasks._

12. Sie geben den Pfad der Datei `docker-compose.yaml` ein und wählen **Dienstimages mithilfe von Push übertragen** einschließlich des aktuellen Tags. Wenn die Aktion zu **Dienstimages mithilfe von Push übertragen** wechselt, ändert sich der Name des Azure DevOps-Tasks in **Dienste automatisch mithilfe von Push übertragen**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)
     _Abbildung 22: Ändern des Azure DevOps-Tasknamens._

13. Nachdem die Azure DevOps-Tasks konfiguriert wurden, speichern Contoso-Administratoren die Buildpipeline und beginnen mit dem Buildprozess.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)
     _Abbildung 23: Starten des Buildprozesses._

14. Sie wählen den Buildauftrag aus, um den Status zu überprüfen.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)
     _Abbildung 24: Überprüfen des Fortschritts._

15. Wenn der Build fertiggestellt ist, zeigt die Containerregistrierung die neuen Repositorys an, die mit den von den Microservices verwendeten Containern aufgefüllt werden.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)
     _Abbildung 25: Anzeigen neuer Repositorys nach Abschluss des Builds._

### <a name="deploy-the-back-end-infrastructure"></a>Bereitstellen der Back-End-Infrastruktur

Mithilfe des erstellten AKS-Clusters und der Docker-Imagebuilds stellen Contoso-Administratoren nun die restliche Infrastruktur bereit, die von Back-End-Microservices genutzt wird. In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet. Der Ordner `/deploy/k8s/arm` enthält ein einziges Skript zum Erstellen aller Elemente.

Die Bereitstellung erfolgt wie folgt:

1. Sie öffnen eine Developer-Eingabeaufforderung und verwenden den Befehl `az login` als Anmeldung für das Azure-Abonnement.

2. Sie verwenden die Datei `deploy.cmd` zur Bereitstellung der Azure-Ressourcen in der Ressourcengruppe `ContosoRG` und der Region `East US 2`, indem sie den folgenden Befehl eingeben:

    `.\deploy.cmd azuredeploy ContosoRG -c eastus2`

    ![Bereitstellen des Back-Ends](./media/contoso-migration-rebuild/backend1.png) _Abbildung 26: Bereitstellen des Back-Ends._

3. Im Azure-Portal erfassen sie die Verbindungszeichenfolgen für die einzelnen Datenbanken, die später verwendet werden.

    ![Bereitstellen des Back-Ends](./media/contoso-migration-rebuild/backend2.png) _Abbildung 27: Erfassen der Verbindungszeichenfolgen der einzelnen Datenbanken._

### <a name="create-the-back-end-release-pipeline"></a>Erstellen der Back-End-Releasepipeline

Contoso-Administratoren gehen nun wie folgt vor:

- Sie stellen den NGINX-Eingangscontroller bereit, um eingehenden Datenverkehr für die Dienste zuzulassen.
- Sie stellen die Microservices für den AKS-Cluster bereit.
- In einem ersten Schritt aktualisieren sie die Verbindungszeichenfolgen zu den Microservices mithilfe von Azure DevOps. Sie konfigurieren eine neue Azure DevOps-Releasepipeline, um die Microservices bereitzustellen.
- In den Anweisungen in diesem Abschnitt wird das Repository [SmartHotel360-Backend](https://github.com/Microsoft/SmartHotel360-Backend) verwendet.
- Einige der Konfigurationseinstellungen (z.B. Active Directory B2C) werden nicht in diesem Artikel behandelt. Weitere Informationen zu diesen Einstellungen finden Sie im Repository weiter oben.

Sie erstellen die Pipeline:

1. Mithilfe von Visual Studio aktualisieren sie die Datei `/deploy/k8s/config_local.yml` anhand der zuvor notierten Informationen zur Datenbankverbindung.

    ![Datenbankverbindungen](./media/contoso-migration-rebuild/back-pipe1.png) _Abbildung 28: Datenbankverbindungen._

2. Sie öffnen Azure DevOps und wählen im Projekt „SmartHotel360“ **+ Neue Pipeline** in **Releases** aus.

    ![Neue Pipeline](./media/contoso-migration-rebuild/back-pipe2.png) Abbildung 29: Die neue Pipeline.

3. Sie wählen **Leere Stufe** aus, um die Pipeline ohne Vorlage zu starten.
4. Sie geben den Phasen- und Pipelinenamen an.

      ![Phasenname](./media/contoso-migration-rebuild/back-pipe4.png) _Abbildung 30: Der Phasenname._

      ![Pipelinename](./media/contoso-migration-rebuild/back-pipe5.png) _Abbildung 31: Der Pipelinename._

5. Sie fügen ein Artefakt hinzu.

     ![Artefakt hinzufügen](./media/contoso-migration-rebuild/back-pipe6.png) _Abbildung 32: Hinzufügen eines Artefakts._

6. Sie wählen **Git** als Quelltyp aus und geben Projekt, Quelle und Masterbranch für die Anwendung SmartHotel360 an.

    ![Artefakteinstellungen](./media/contoso-migration-rebuild/back-pipe7.png) _Abbildung 33: Die Artefakteinstellungen._

7. Sie wählen den Tasklink aus.

    ![Tasklink](./media/contoso-migration-rebuild/back-pipe8.png) _Abbildung 34: Der Tasklink._

8. Sie fügen eine neue Azure PowerShell-Aufgabe hinzu, sodass sie ein PowerShell-Skript in einer Azure-Umgebung ausführen können.

    ![PowerShell in Azure](./media/contoso-migration-rebuild/back-pipe9.png) _Abbildung 35: Hinzufügen eines neuen PowerShell-Tasks._

9. Sie wählen zunächst das Azure-Abonnement für den Task und anschließend das Skript `deploy.ps1` im Git-Repository aus.

    ![Skript ausführen](./media/contoso-migration-rebuild/back-pipe10.png) _Abbildung 36: Ausführen des Skripts._

10. Sie fügen dem Skript Argumente hinzu. Das Skript löscht den gesamten Clusterinhalt (außer den **eingehenden Daten** und dem **Eingangscontroller**) und stellt die Microservices bereit.

    ![Skriptargumente](./media/contoso-migration-rebuild/back-pipe11.png)
     _Abbildung 37: Hinzufügen von Argumenten zum Skript._

11. Sie legen die bevorzugte Azure PowerShell-Version als neueste fest und speichern die Pipeline.

12. Sie kehren zur Seite **Release** zurück und erstellen manuell ein neues Release.

    ![Neues Release](./media/contoso-migration-rebuild/back-pipe12.png)
     _Abbildung 38: Manuelles Erstellen eines neuen Releases._

13. Nach dem Erstellen wählen sie das Release und anschließend in **Aktionen** die Option **Bereitstellen** aus.

      ![Release bereitstellen](./media/contoso-migration-rebuild/back-pipe13.png)
     _Abbildung 39: Bereitstellen eines Releases._

14. Nach Abschluss der Bereitstellung führen sie mithilfe der Azure Cloud Shell folgenden Befehl aus, um den Status von Diensten zu überprüfen: `kubectl get services`.

## <a name="step-3-provision-front-end-services"></a>Schritt 3: Bereitstellen von Front-End-Diensten

Contoso-Administratoren müssen die von den Front-End-Anwendungen verwendete Infrastruktur bereitstellen. Dazu erstellen sie Folgendes:

- Einen Blobspeichercontainer zum Speichern der Fotos von Haustieren
- Eine Azure Cosmos DB-Datenbank zum Speichern von Dokumenten mit Informationen zu Haustieren
- Die Maschinelles Sehen-API für die Website.

In den Anweisungen für diesen Abschnitt wird das Repository [SmartHotel360-website](https://github.com/microsoft/smartHotel360-website) verwendet.

### <a name="create-blob-storage-containers"></a>Erstellen von Blob Storage-Containern

1. Sie öffnen im Azure-Portal das erstellte Speicherkonto und wählen anschließend **Blobs** aus.
2. Sie erstellen einen neuen Container `Pets`, bei dem die öffentliche Zugriffsebene für den Container festgelegt ist. Benutzer laden ihre Fotos von Haustieren in diesen Container hoch.

    ![Speicherblob](./media/contoso-migration-rebuild/blob1.png) _Abbildung 40: Erstellen eines neuen Containers._

3. Sie erstellen einen zweiten neuen Container namens `settings`. Eine Datei mit allen Front-End-App-Einstellungen wird in diesen Container platziert.

    ![Speicherblob](./media/contoso-migration-rebuild/blob2.png) _Abbildung 41: Erstellen eines zweiten Containers._

4. Sie speichern die Zugriffsdetails für das Speicherkonto zur späteren Verwendung in einer Textdatei.

    ![Speicherblob](./media/contoso-migration-rebuild/blob2.png) _Abbildung 42: Eine Textdatei, in der Zugriffsdetails gespeichert werden._

### <a name="provision-an-azure-cosmos-db-database"></a>Bereitstellen einer Azure Cosmos DB-Datenbank

Contoso-Administratoren stellen eine Azure Cosmos DB-Datenbank bereit, die für Informationen zu Haustieren verwendet werden soll.

1. Sie erstellen eine **Azure Cosmos DB**-Datenbank im Azure Marketplace.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png) _Abbildung 43: Erstellen einer Azure Cosmos DB-Datenbank._

2. Sie geben einen Namen (`contososmarthotel`) an, wählen die SQL-API aus und fügen sie in die Produktionsressourcengruppe `ContosoRG` in der Hauptregion (`East US 2`) ein.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png) _Abbildung 44: Benennen einer Azure Cosmos DB-Datenbank._

3. Contoso fügt eine neue Sammlung zur Datenbank mit Standardkapazität und -durchsatz hinzu.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png) _Abbildung 45: Hinzufügen einer neuen Sammlung zur Datenbank._

4. Sie notieren die Verbindungsinformationen für die Datenbank zur zukünftigen Verwendung.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png) _Abbildung 46: Die Verbindungsinformationen für die Datenbank._

### <a name="provision-the-computer-vision-api"></a>Bereitstellen der Maschinelles Sehen-API

Contoso-Administratoren stellen die Maschinelles Sehen-API bereit. Die API wird von der Funktion zum Auswerten der Bilder aufgerufen, die von den Benutzern hochgeladen wurden.

1. Contoso erstellt im Azure Marketplace eine **Maschinelles Sehen**-Instanz.

     ![Maschinelles Sehen](./media/contoso-migration-rebuild/vision1.png) _Abbildung 47: Eine neue Instanz im Azure Marketplace._

2. Sie stellen die API (`smarthotelpets`) in der Produktionsressourcengruppe `ContosoRG` in der Hauptregion (`East US 2`) bereit.

    ![Maschinelles Sehen](./media/contoso-migration-rebuild/vision2.png) _Abbildung 48: Bereitstellen einer API in einer Produktionsressourcengruppe._

3. Contoso speichert die Verbindungseinstellungen für die API in einer Textdatei zur späteren Verwendung.

     ![Maschinelles Sehen](./media/contoso-migration-rebuild/vision3.png) _Abbildung 49: Speichern der Einstellungen einer API-Verbindung._

### <a name="provision-the-azure-web-app"></a>Bereitstellen der Azure-Web-App

Contoso-Administratoren stellen die Web-App mithilfe des Azure-Portals bereit.

1. Das Unternehmen wählt **Web-App** im Portal aus.

    ![Web-App](./media/contoso-migration-rebuild/web-app1.png) _Abbildung 50: Auswählen der Web-App._

2. Sie geben einen Namen für die Web-App an (`smarthotelcontoso`), führen die App unter Windows aus und platzieren sie in der Produktionsressourcengruppe `ContosoRG`. Sie erstellen eine neue Application Insights-Instanz zur Anwendungsüberwachung.

    ![Name der Web-App](./media/contoso-migration-rebuild/web-app2.png) _Abbildung 51: Der Name der Web-App._

3. Anschließend navigieren sie zur Adresse der Anwendung, um zu überprüfen, ob sie erfolgreich erstellt wurde.

4. Im Azure-Portal erstellen sie einen Stagingslot für den Code. Die Pipeline wird für diesen Slot bereitgestellt. Dadurch wird sichergestellt, dass Code erst in die Produktionsumgebung gelangt, wenn Administratoren ein Release ausführen.

    ![Web-App-Stagingslot](./media/contoso-migration-rebuild/web-app3.png) _Abbildung 52: Ein Web-App-Stagingslot._

### <a name="provision-the-function-app"></a>Bereitstellen der Funktions-App

Contoso-Administratoren stellen im Azure-Portal die Funktions-App bereit.

1. Sie wählen **Funktionen-App** aus.

    ![Erstellen einer Funktions-App](./media/contoso-migration-rebuild/function-app1.png) _Abbildung 53: Auswählen der Funktions-App._

2. Sie geben einen Namen für die Funktions-App an (`smarthotelpetchecker`). Sie platzieren die Funktions-App in der Produktionsressourcengruppe (`ContosoRG`). Sie legen den Hostingort auf **Consumption Plan** (Verbrauchstarif) fest und platzieren die Funktions-App in der Region `East US 2`. Daraufhin wird neben einem neuen Speicherkonto auch eine Application Insights-Instanz für die Überwachung erstellt.

    ![Funktions-App-Einstellungen](./media/contoso-migration-rebuild/function-app2.png) _Abbildung 54: Funktions-App-Einstellungen._

3. Nach der Bereitstellung der Funktions-App navigieren sie zur Adresse der App, um zu überprüfen, ob sie erfolgreich erstellt wurde.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Schritt 4: Einrichten der Front-End-Pipeline

Contoso-Administratoren erstellen zwei verschiedene Projekte für die Front-End-Website.

1. In Azure DevOps erstellen sie ein Projekt `SmartHotelFrontend`.

    ![Front-End-Projekt](./media/contoso-migration-rebuild/function-app1.png) _Abbildung 55: Ein Front-End-Projekt._

2. Sie importieren das Git-Repository [SmartHotel360 front end](https://github.com/Microsoft/SmartHotel360-Website) in das neue Projekt.

3. Für die Funktions-App erstellen sie ein weiteres Azure DevOps-Projekt (`SmartHotelPetChecker`) und importieren das Git-Repository [PetChecker](https://github.com/sonahander/SmartHotel360-PetCheckerFunction) in dieses Projekt.

### <a name="configure-the-web-app"></a>Konfigurieren der Web-App

Contoso-Administratoren konfigurieren nun die Web-App zur Verwendung von Contoso-Ressourcen.

1. Sie stellen eine Verbindung mit dem Azure DevOps-Projekt her und klonen das Repository lokal auf dem Entwicklungscomputer.
2. In Visual Studio öffnet Contoso den Ordner, um alle Dateien im Repository anzuzeigen.

    ![Repository-Dateien](./media/contoso-migration-rebuild/configure-webapp1.png) _Abbildung 56: Anzeigen aller Dateien im Repository._

3. Sie aktualisieren ggf. die Konfigurationsänderungen.

    - Wenn die Web-App gestartet wird, sucht sie nach der App-Einstellung `SettingsUrl`.
    - Diese Variable muss eine URL enthalten, die auf eine Konfigurationsdatei zeigt.
    - Standardmäßig wird die Einstellung als öffentlicher Endpunkt verwendet.

4. Sie aktualisieren die `/config-sample.json/sample.json`-Datei.

    - Dies ist die Konfigurationsdatei für das Web, wenn der öffentliche Endpunkt verwendet wird.
    - Sie bearbeiten die Abschnitte `urls` und `pets_config` mit den Werten für die AKS-API-Endpunkte, die Speicherkonten und die Azure Cosmos DB-Datenbank.
    - Die URLs sollten dem DNS-Namen der neuen Web-App entsprechen, die von Contoso erstellt wird.
    - Für Contoso ist dies `smarthotelcontoso.eastus2.cloudapp.azure.com`.

    ![JSON-Einstellungen](./media/contoso-migration-rebuild/configure-webapp2.png) _Abbildung 57: JSON-Einstellungen._

5. Nach dem Aktualisieren benennen sie die Datei in `smarthotelsettingsurl` um und laden sie in den Blobspeicher hoch, den sie zuvor erstellt haben.

    ![Umbenennen und hochladen](./media/contoso-migration-rebuild/configure-webapp3.png) _Abbildung 58: Umbenennen und Hochladen der Datei._

6. Sie wählen die Datei aus, um die URL abzurufen. Diese URL wird von der Anwendung beim Abrufen der Konfigurationsdatei verwendet.

    ![App-URL](./media/contoso-migration-rebuild/configure-webapp4.png) _Abbildung 59: Die Anwendungs-URL._

7. In der `appsettings.Production.json`-Datei aktualisieren sie die `SettingsURL` auf die URL der neuen Datei.

    ![URL aktualisieren](./media/contoso-migration-rebuild/configure-webapp5.png) _Abbildung 60: Aktualisieren der URL mit der neuen Datei._

### <a name="deploy-the-website-to-azure-app-service"></a>Bereitstellen der Website in Azure App Service

Contoso-Administratoren können die Website jetzt veröffentlichen.

1. Sie öffnen Azure DevOps und wählen im Projekt `SmartHotelFrontend` in **Builds and Releases** (Builds und Releases) die Option **+ Neue Pipeline** aus.
2. Sie wählen **Azure DevOps-Git** als Quelle aus.
3. Sie wählen die Vorlage **ASP.NET Core** aus.
4. Sie überprüfen in der Pipeline, ob die Optionen **Webprojekte veröffentlichen** und **Veröffentlichte Projekte komprimieren** ausgewählt wurden.

    ![Pipelineeinstellungen](./media/contoso-migration-rebuild/vsts-publish-front2.png) _Abbildung 61: Pipelineeinstellungen._

5. Unter **Trigger** aktivieren sie „Continuous Integration“ und fügen den Masterbranch hinzu. Dadurch wird sichergestellt, dass die Buildpipeline jedes Mal startet, wenn die Lösung neuen Code für den Masterbranch committet.

    ![Continuous Integration](./media/contoso-migration-rebuild/vsts-publish-front3.png) _Abbildung 62: Continuous Integration._

6. Sie wählen **Speichern und in Warteschlange einreihen** aus, um einen Buildvorgang zu starten.
7. Nach Abschluss des Buildvorgangs konfigurieren sie eine Releasepipeline mithilfe der **Azure App Service-Bereitstellung**.
8. Sie geben den Phasennamen **Staging** an.

    ![Umgebungsname](./media/contoso-migration-rebuild/vsts-publish-front4.png) _Abbildung 63: Benennen der Umgebung._

9. Sie fügen ein Artefakt hinzu und wählen Build aus, den sie konfiguriert haben.

    ![Artefakt hinzufügen](./media/contoso-migration-rebuild/vsts-publish-front5.png) _Abbildung 64: Hinzufügen eines Artefakts._

10. Sie wählen das Blitzsymbol des Artefakts aus, um „Continuous Deployment“ zu aktivieren.

    ![Continuous Deployment](./media/contoso-migration-rebuild/vsts-publish-front6.png)
    _Abbildung 65: Aktivieren von „Continuous Deployment“._

11. Sie wählen in **Umgebung** unter **Staging** die Option **1 job, 1 task** (1 Auftrag, 1 Aufgabe) aus.
12. Nachdem sie das Abonnement und den Web-App-Namen ausgewählt haben, öffnen sie den Task **Deploy Azure App Service** (Azure App Service bereitstellen). Die Bereitstellung wurde für die Verwendung des Bereitstellungsslots **Staging** konfiguriert. Dadurch wird automatisch Code zur Überprüfung und Genehmigung in diesem Slot erstellt.

     ![Slot](./media/contoso-migration-rebuild/vsts-publish-front7.png)
     _Abbildung 66: Verwenden eines Slots._

13. In der **Pipeline** fügen sie eine neue Phase hinzu.

    ![Neue Umgebung](./media/contoso-migration-rebuild/vsts-publish-front8.png)
     _Abbildung 67: Hinzufügen einer neuen Phase._

14. Sie wählen **Azure App Service-Bereitstellung mit Slot** aus und geben der Umgebung den Namen **Prod**.
15. Sie wählen **1 job, 2 tasks** (1 Auftrag, 2 Aufgaben) und dann das Abonnement, den App Service-Namen und den Slot **Staging** aus.

    ![Umgebungsname](./media/contoso-migration-rebuild/vsts-publish-front10.png)
     _Abbildung 68: Ein Umgebungsname._

16. Sie entfernen **Deploy Azure App Service to Slot** (Azure App Service in Slot bereitstellen) aus der Pipeline. Diese Aufgabe wurde in den vorherigen Schritten dort eingefügt.

    ![Aus Pipeline entfernen](./media/contoso-migration-rebuild/vsts-publish-front11.png)
     _Abbildung 69: Entfernen eines Slots aus der Pipeline._

17. Sie speichern die Pipeline. Sie wählen in der Pipeline **Bedingungen nach der Bereitstellung** aus.

    ![Nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front12.png)
     _Abbildung 70: Bedingungen nach der Bereitstellung._

18. Sie aktivieren **Genehmigungen nach der Bereitstellung** und fügen eine Entwicklungsleitung als genehmigende Person hinzu.

    ![Genehmigung nach der Bereitstellung](./media/contoso-migration-rebuild/vsts-publish-front13.png)
     _Abbildung 71: Hinzufügen eines Genehmigers._

19. Sie starten in der Buildpipeline manuell einen Build. Dadurch wird die neue Releasepipeline ausgelöst, wodurch wiederum die Website im Stagingslot bereitgestellt wird. Bei Contoso lautet die URL für den Slot `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Nach Abschluss des Buildvorgangs und nachdem das Release im Slot bereitgestellt wurde, sendet Azure DevOps für die Genehmigung eine E-Mail an die Entwicklungsleitung.

21. Die Entwicklungsleitung wählt **Genehmigung anzeigen** aus und kann dann die Anforderung im Azure DevOps-Portal genehmigen oder ablehnen.

    ![Genehmigungs-E-Mail](./media/contoso-migration-rebuild/vsts-publish-front14.png)
     _Abbildung 72: Eine Entwicklungsleitung genehmigt eine Anforderung._

22. Die Leitung erstellt einen Kommentar und genehmigt die Anforderung. Dadurch beginnt der Austausch der Slots **Staging** und **Prod**. Zudem wird der Build in die Produktionsumgebung verschoben.

    ![Genehmigen und austauschen](./media/contoso-migration-rebuild/vsts-publish-front15.png)
     _Abbildung 73: Verschieben des Builds in die Produktion._

23. Der Austausch wird durch die Pipeline abgeschlossen.

    ![Austausch abschließen](./media/contoso-migration-rebuild/vsts-publish-front16.png)
     _Abbildung 74: Abschließen des Austausches._

24. Das Team überprüft den Slot **prod**, um sicherzustellen, dass sich die Web-App in der Produktionsumgebung unter `https://smarthotelcontoso.azurewebsites.net/` befindet.

### <a name="deploy-the-petchecker-function-app"></a>Bereitstellen der Funktions-App PetChecker

Contoso-Administratoren stellen die Anwendung wie folgt bereit:

1. Sie klonen das Repository lokal auf dem Entwicklungscomputer, indem sie eine Verbindung mit dem Azure DevOps-Projekt herstellen.
2. In Visual Studio öffnet Contoso den Ordner, um alle Dateien im Repository anzuzeigen.
3. Sie öffnen die Datei `src/PetCheckerFunction/local.settings.json` und fügen die App-Einstellungen für Speicher, Azure Cosmos DB-Datenbank und Maschinelles Sehen-API hinzu.

    ![Funktion bereitstellen](./media/contoso-migration-rebuild/function5.png) _Abbildung 75: Bereitstellen der Funktion._

4. Sie committen den Code, synchronisieren ihn mit Azure DevOps und pushen so ihre Änderungen.
5. Sie fügen eine neue Buildpipeline hinzu und wählen anschließend **Azure DevOps Git** für die Quelle aus.
6. Sie wählen die Vorlage **ASP.NET Core (.NET Framework)** aus.
7. Sie übernehmen die Standardwerte für die Vorlage.
8. In **Trigger** wählen sie **Continuous Integration aktivieren** und dann **Speichern und in Warteschlange einreihen** aus, um einen Buildvorgang zu starten.
9. Nach erfolgreichem Buildvorgang erstellen sie eine Releasepipeline, indem sie **Azure App Service-Bereitstellung mit Slot** hinzufügen.
10. Sie geben der Umgebung den Namen **Prod** und wählen anschließend das Abonnement aus. Sie legen den **App-Typ** auf **Funktions-App** und den App Service-Namen auf `smarthotelpetchecker` fest.

    ![Funktions-App](./media/contoso-migration-rebuild/petchecker2.png)
     _Abbildung 76: Die Funktions-App._

11. Sie fügen einen Artefakt-**Build** hinzu.

    ![Ein Artefakt hinzufügen](./media/contoso-migration-rebuild/petchecker3.png)
     _Abbildung 77: Hinzufügen eines Artefakts._

12. Sie aktivieren **Continuous Deployment-Trigger** und wählen anschließend **Speichern** aus.
13. Sie wählen **Neuen Build in Warteschlange** aus, um die ganze CI/CD-Pipeline auszuführen.
14. Nachdem die Funktion bereitgestellt wurde, wird sie im Azure-Portal mit dem Status **Wird ausgeführt** angezeigt.

    ![Den Funktionsstatus aktualisieren](./media/contoso-migration-rebuild/function6.png)
     _Abbildung 78: Aktualisieren des Funktionsstatus._

15. Sie navigieren zur PetChecker-Anwendung unter `http://smarthotel360public.azurewebsites.net/pets`, um zu überprüfen, ob sie ordnungsgemäß funktioniert.

16. Sie wählen den Avatar aus, um ein Bild hochzuladen.

    ![Zuweisen eines Bilds zu einem Avatar](./media/contoso-migration-rebuild/function7.png)
     _Abbildung 79: Zuweisen eines Bilds zu einem Avatar._

17. Das erste Foto, das überprüft werden soll, ist das eines kleinen Hundes.

    ![Überprüfen eines Fotos.](./media/contoso-migration-rebuild/function8.png)
     _Abbildung 80: Überprüfen eines Fotos._

18. Die Anwendung gibt eine Meldung zur Bestätigung zurück.

    ![Eine Bestätigungsmeldung](./media/contoso-migration-rebuild/function9.png)
     _Abbildung 81: Eine Bestätigungsmeldung._

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso nun die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neuen Datenbanken geschützt sind. [Weitere Informationen](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
- Die Anwendung muss für die Verwendung von SSL mit Zertifikaten aktualisiert werden. Die Containerinstanz sollte erneut bereitgestellt werden, um auf 443 zu antworten.
- Zum Schutz von Geheimnissen für die Service Fabric-Anwendungen sollte Contoso die Verwendung von Key Vault in Erwägung ziehen. [Weitere Informationen](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management)

### <a name="backups-and-disaster-recovery"></a>Sicherungen und Notfallwiederherstellung

- Contoso muss die [Sicherungsanforderungen für Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) überprüfen.
- Contoso sollte die Implementierung von [SQL-Failovergruppen berücksichtigen, um ein regionales Failover für die Datenbank bereitzustellen](https://docs.microsoft.com/azure/sql-database/sql-database-auto-failover-group).
- Contoso kann die [Georeplikation für die Premium-SKU von Azure Container Registry](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication) nutzen.
- Azure Cosmos DB führt automatisch Sicherungen durch. Contoso kann sich über diesen Prozess [informieren](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Nachdem alle Ressourcen bereitgestellt wurden, sollte Contoso Azure-Tags basierend auf seiner [Infrastrukturplanung](./contoso-migration-infrastructure.md#set-up-tagging) zuweisen.
- Die gesamte Lizenzierung ist in die Kosten für die PaaS-Dienste integriert, die Contoso verwendet. Dies wird über EA verrechnet.
- Contoso aktiviert [Azure Cost Management und das Azure-Abrechnungsportal](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde die Anwendung SmartHotel360 in Azure von Contoso neu erstellt. Die lokale VM für das Anwendungs-Front-End wurde in Azure App Service-Web-Apps neu erstellt. Das Back-End der Anwendung wird mithilfe von Microservices erstellt, die für Container bereitgestellt werden, die von AKS verwaltet werden. Die Funktionalität hat Contoso durch eine Anwendung für Fotos von Haustieren verbessert.

## <a name="suggested-skills"></a>Empfohlene Qualifikationen

Microsoft Learn ist ein neuer Lernansatz. Die Bereitschaft zu den neuen Qualifikationen und Aufgaben, die mit der Cloudeinführung verbunden sind, entsteht nicht problemlos. Microsoft Learn bietet einen lohnenderen Ansatz für praktisches Lernen, der Ihnen hilft, Ihre Ziele schneller zu erreichen. Punkte sammeln, zu höheren Stufen aufsteigen und mehr erreichen.

Hier finden Sie einige Beispiele für maßgeschneiderte Lernpfade auf Microsoft Learn, die auf die Anwendung Contoso SmartHotel360 in Azure abgestimmt sind.

<!--docsTest:ignore "Azure Cognitive Vision Services" -->

- **[Bereitstellen einer Website in Azure mithilfe von Azure App Service](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service):** Mit Web-Apps in Azure können Sie Ihre Website leicht veröffentlichen und verwalten, ohne dass Sie mit den zugrunde liegenden Servern, Speicher oder Netzwerkressourcen arbeiten müssen. Stattdessen können Sie sich auf Ihre Websitefeatures konzentrieren und die stabile Azure-Plattform verwenden, um sicheren Zugriff auf Ihre Site bereitzustellen.

- **[Verarbeiten und Klassifizieren von Bildern mit der Bildanalyse von Azure Cognitive Services](https://docs.microsoft.com/learn/paths/classify-images-with-vision-services):** Azure Cognitive Services bietet vorgefertigte Funktionen, um die Funktionalität für maschinelles Sehen in Ihren Anwendungen zu aktivieren. Erfahren Sie, wie Sie die Bildanalyse von Cognitive Services verwenden, um Gesichter zu erkennen, Bilder mit Tags zu versehen und zu klassifizieren und Objekte zu identifizieren.
