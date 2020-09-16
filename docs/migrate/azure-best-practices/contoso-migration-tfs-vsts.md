---
title: Umgestalten einer Team Foundation Server-Bereitstellung zu Azure DevOps Services
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie Ihre lokale Bereitstellung von Team Foundation Server umgestalten, indem Sie sie zu Azure DevOps Services in Azure migrieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6cd92a5a089507fde1d770308f93d9547452389e
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602995"
---
<!-- cSpell:ignore contosodev contosodevmigration contosomigration onmicrosoft visualstudio sourceconnectionstring smarthotelcontainer identitymaplog CONTOSOTFS DACPAC SQLDB SQLSERVERNAME INSTANCENAME sqlpackage SSDT azuredevopsmigration validateonly ImportType -->

# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Umgestalten einer Team Foundation Server-Bereitstellung zu Azure DevOps Services

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso seine lokale Visual Studio Team Foundation Server-Bereitstellung durch eine Migration zu Azure DevOps Services in Azure umgestaltet. Das Contoso-Entwicklungsteam hat in den letzten fünf Jahren Team Foundation Server für die Zusammenarbeit im Team und die Quellcodeverwaltung verwendet. Nun möchte das Team für Entwicklungen und Tests sowie für die Quellcodeverwaltung auf eine cloudbasierte Lösung umsteigen. Azure DevOps Services spielt eine wichtige Rolle bei der Migration des Contoso-Teams zu einem Azure DevOps-Modell und der Entwicklung neuer cloudnativer Anwendungen.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam von Contoso arbeitet eng mit den jeweiligen Geschäftspartnern zusammen, um zukünftige Ziele zu identifizieren. Die Partner haben sich nicht im Detail mit Entwicklungstools und -technologien befasst, das Team hat jedoch die folgenden Punkte zusammengefasst:

- **Software**: Unabhängig vom Kerngeschäft handelt es sich bei allen Unternehmen nun um Softwareunternehmen, einschließlich Contoso. Die Unternehmensführung ist interessiert daran, wie die IT das Unternehmen bei neuen Vorgehensweisen für Benutzer und neuen Erfahrungen seiner Kunden unterstützen kann.
- **Effizienz**: Contoso muss Prozesse optimieren und unnötige Verfahren für Entwickler und Benutzer entfernen. So kann das Unternehmen im Hinblick auf die Anforderungen der Kunden effizienter Ergebnisse liefern. Das Unternehmen benötigt eine schnell agierende IT, die weder Zeit noch Geld verschwendet.
- **Flexibilität**: Die IT-Abteilung von Contoso muss schneller auf geschäftliche Anforderungen reagieren, um in einer globalen Wirtschaft erfolgreich zu sein. Sie muss in der Lage sein, schneller auf Änderungen auf dem Markt zu reagieren. Die IT darf nicht im Weg stehen oder zum Geschäftshindernis werden.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration zu Azure DevOps Services gesetzt:

- Das Team benötigt ein Tool, um die Daten in die Cloud zu migrieren. Wenige manuelle Prozesse sollten erforderlich sein.
- Arbeitselementdaten und der Verlauf für das letzte Jahr müssen migriert werden.
- Das Team möchte keinen neuen Benutzernamen und Kennwörter einrichten. Alle aktuellen Systemzuweisungen müssen beibehalten werden.
- Für die Quellcodeverwaltung möchte das Team von der Team Foundation-Versionskontrolle (Team Foundation Version Control, TFVC) auf Git umstellen.
- Der Übergang zu Git stellt eine „abgespeckte Migration“ dar, bei der nur die neueste Version des Quellcodes importiert wird. Er wird während einer Downtime durchgeführt, in der alle Aufgaben bei der Migration der Codebasis angehalten werden. Dem Team ist bewusst, dass nach der Umstellung nur der aktuelle Masterbranchverlauf zur Verfügung steht.
- Das Team macht sich Sorgen wegen der Änderung und möchte vor einer vollständigen Migration Tests durchführen. Das Team möchte auch nach dem Umstieg auf Azure DevOps Services weiterhin auf Team Foundation Server zugreifen können.
- Das Team verfügt über mehrere Sammlungen und möchte mit einer Sammlung beginnen, die nur wenige Projekte enthält, um den Prozess besser zu verstehen.
- Dem Team ist bewusst, dass Team Foundation Server-Sammlungen in einem direkten Verhältnis zu Azure DevOps Services-Organisationen stehen, sodass sie über mehrere URLs verfügen. Dies entspricht dem aktuellen Modell einer Trennung von Codebasen und Projekten.

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Contoso migriert seine Team Foundation Server-Projekte in die Cloud und hostet Projekte oder die Quellcodeverwaltung nicht mehr lokal.
- Team Foundation Server wird zu Azure DevOps Services migriert.
- Contoso verfügt derzeit über eine Team Foundation Server-Sammlung namens `ContosoDev`, die zu einer Azure DevOps Services-Organisation namens `contosodevmigration.visualstudio.com` migriert werden soll.
- Die Projekte, Arbeitselemente, Fehler und Iterationen aus dem letzten Jahr werden zu Azure DevOps Services migriert.
- Contoso verwendet seine Azure Active Directory-Instanz (Azure AD), die bei der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) zu Beginn der Migrationsplanung eingerichtet wird.

![Diagramm der vorgeschlagenen Architektur](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

1. Eine umfangreiche Vorbereitung ist erforderlich. Zunächst muss Contoso ein Upgrade seiner Team Foundation Server-Implementierung auf ein unterstütztes Niveau vornehmen. Contoso führt zurzeit Team Foundation Server 2017 Update 3 aus, für die Datenbankmigration muss jedoch eine unterstützte 2018-Version mit den neuesten Updates ausgeführt werden.
1. Nach dem Upgrade führt Contoso das Team Foundation Server-Migrationstool aus und überprüft dessen Sammlung.
1. Contoso erstellt eine Gruppe von Vorbereitungsdateien und führt anschließend zu Testzwecken einen Migrationsprobelauf durch.
1. Anschließend wird eine weitere Migration durchgeführt, dieses Mal jedoch eine vollständige Migration, die Arbeitselemente, Fehler, Sprints und Code beinhaltet.
1. Nach der Migration migriert Contoso seinen Code von TFVC nach Git.

![Diagramm des Contoso-Migrationsprozesses](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Voraussetzungen

Zum Ausführen dieses Szenarios muss Contoso die folgenden Voraussetzungen erfüllen:

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure-Abonnement** | Contoso hat in einem früheren Artikel dieser Reihe Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. <br><br> Falls Sie präzisere Berechtigungen benötigen, helfen Ihnen die Informationen unter [Verwalten des Site Recovery-Zugriffs mit rollenbasierter Zugriffssteuerung (Role-Based Access Control, RBAC)](/azure/site-recovery/site-recovery-role-based-linked-access-control) weiter. |
| **Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie unter [Bereitstellen einer Migrationsinfrastruktur](./contoso-migration-infrastructure.md) beschrieben. |
| **Lokale Team Foundation Server-Instanz** | Die lokale Instanz muss entweder Team Foundation Server 2018 Upgrade 2 ausführen, oder im Rahmen dieses Vorgangs muss ein Upgrade durchgeführt werden. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Erstellen eines Azure Storage-Kontos.** Dieses Speicherkonto wird beim Migrationsvorgang verwendet.
> - **Schritt 2: Durchführen eines Upgrades von Team Foundation Server**. Contoso führt ein Upgrade seiner Bereitstellung auf Team Foundation Server 2018 Upgrade 2 durch.
> - **Schritt 3: Überprüfen der Team Foundation Server-Sammlung**. Contoso überprüft die Team Foundation Server-Sammlung als Vorbereitung auf die Migration.
> - **Schritt 4: Erstellen der Migrationsdateien**. Contoso erstellt die Migrationsdateien mit dem Team Foundation Server-Migrationstool.

## <a name="step-1-create-an-azure-storage-account"></a>Schritt 1: Erstellen eines Azure-Speicherkontos

1. Die Contoso-Administratoren erstellen im Azure-Portal ein Speicherkonto (`contosodevmigration`).
1. Das Konto wird in der sekundären Region platziert, die das Unternehmen für das Failover verwendet (`Central US`). Ein allgemeines Standardkonto mit lokal redundantem Speicher wird verwendet.

    ![Screenshot des Bereichs „Speicherkonto erstellen“](./media/contoso-migration-tfs-vsts/storage1.png)

**Benötigen Sie weitere Hilfe?**

- [Einführung in Azure Storage](/azure/storage/common/storage-introduction)
- [Informationen zu Azure-Speicherkonten](/azure/storage/common/storage-create-storage-account)

<!-- docsTest:casing "Server Configuration Wizard" "Configure Features Wizard" "Detach Team Project Collection Wizard" -->

## <a name="step-2-upgrade-team-foundation-server"></a>Schritt 2: Durchführen eines Upgrades von Team Foundation Server

Die Contoso-Administratoren führen ein Upgrade der Team Foundation Server-Instanz auf Team Foundation Server 2018 Update 2 durch. Vor der Durchführung führen sie folgende Schritte aus:

- Herunterladen von [Team Foundation Server 2018 Update 2](https://visualstudio.microsoft.com/downloads)
- Überprüfen der [Hardwareanforderungen](/azure/devops/server/requirements)
- Lesen der [Versionshinweise](/visualstudio/releasenotes/tfs2018-relnotes) und der [Upgradehinweise](/azure/devops/server/upgrade/get-started#before-you-upgrade-to-tfs-2018)

Das Upgrade wird wie folgt durchgeführt:

1. Zum Einstieg sichern die Administratoren ihre Team Foundation Server-Instanz, die auf einem virtuellen VMware-Computer ausgeführt wird, und erstellen eine VMware-Momentaufnahme.

    ![Screenshot des Bereichs „Erste Schritte“ für ein Upgrade von Team Foundation Server](./media/contoso-migration-tfs-vsts/upgrade1.png)

1. Das Team Foundation Server-Installationsprogramm wird gestartet, und sie wählen den Speicherort der Installation aus. Für das Installationsprogramm ist Internetzugriff erforderlich.

    ![Screenshot der Team Foundation Server-Installationsseite in Visual Studio](./media/contoso-migration-tfs-vsts/upgrade2.png)

1. Nach Abschluss der Installation wird der Serverkonfigurations-Assistent gestartet.

    ![Screenshot des Konfigurations-Assistenten für Team Foundation Server 2018 Update 2](./media/contoso-migration-tfs-vsts/upgrade3.png)

1. Nach der Überprüfung führt der Serverkonfigurations-Assistent das Upgrade durch.

     ![Screenshot des Upgradestatus-Bereichs des Team Foundation Server-Konfigurations-Assistenten](./media/contoso-migration-tfs-vsts/upgrade4.png)

1. Die Administratoren überprüfen die Team Foundation Server-Installation anhand von Projekten, Arbeitselementen und Code.

     ![Screenshot des Product Backlog-Bereichs zum Überprüfen der Team Foundation Server-Installation](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Einige Team Foundation Server-Upgrades müssen den Featurekonfigurations-Assistenten ausführen, wenn das Upgrade abgeschlossen ist. [Weitere Informationen](/azure/devops/reference/configure-features-after-upgrade?utm_campaign=vstsdataimportguide&utm_medium=guide&utm_source=ms&view=vsts)

**Benötigen Sie weitere Hilfe?**

Erfahren Sie mehr über [Upgrades von Team Foundation Server](/azure/devops/server/upgrade/get-started).

## <a name="step-3-validate-the-team-foundation-server-collection"></a>Schritt 3: Überprüfen der Team Foundation Server-Sammlung

Die Contoso-Administratoren führen das Team Foundation Server-Migrationstool für die `contosodev`-Sammlungsdatenbank aus, um diese vor der Migration zu überprüfen.

1. Sie laden das [Team Foundation Server-Migrationstool](https://www.microsoft.com/download/details.aspx?id=54274) herunter, und installieren es. Dabei ist es wichtig, dass die Version für das ausgeführte Team Foundation Server-Update heruntergeladen wird. Die Version kann in die Verwaltungskonsole eingecheckt werden.

    ![Screenshot des Team Foundation Server-Bereichs zum Überprüfen der Produktversion](./media/contoso-migration-tfs-vsts/collection1.png)

1. Das Tool zur Überprüfung wird ausgeführt, indem die URL der Projektsammlung wie im folgenden Befehl angezeigt angegeben wird:

    `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

    Im Tool wird ein Fehler angezeigt.

    ![Screenshot eines Überprüfungsfehlers im Team Foundation Server-Migrationstool](./media/contoso-migration-tfs-vsts/collection2.png)

1. Die Administratoren finden die Protokolldateien im Ordner `Logs`, direkt vor dem Speicherort des Tools. Eine Protokolldatei wird für jede wichtige Überprüfung generiert. `TfsMigration.log` enthält die wichtigsten Informationen.

    ![Screenshot des Speicherorts der Protokolldatei in Team Foundation Server](./media/contoso-migration-tfs-vsts/collection3.png)

1. Sie finden diesen Eintrag, der mit der Identität im Zusammenhang steht.

    ![Screenshot mit dem Fehler, der während der Identitätsüberprüfung aufgetreten ist](./media/contoso-migration-tfs-vsts/collection4.png)

1. Sie führen `TfsMigrator validate /help` in der Befehlszeile aus und sehen, dass der Befehl `/tenantDomainName` erforderlich zu sein scheint, um Identitäten zu überprüfen.

     ![Screenshot mit dem Befehl, der zum Überprüfen von Identitäten erforderlich ist](./media/contoso-migration-tfs-vsts/collection5.png)

1. Sie führen den Überprüfungsbefehl erneut aus und schließen diesen Wert und ihren Azure AD-Namen ein: `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![Screenshot der Eingabeaufforderung mit dem richtigen Befehl](./media/contoso-migration-tfs-vsts/collection7.png)

1. Die Administratoren geben im angezeigten Azure AD-Anmeldefenster die Anmeldeinformationen eines globalen Administratorbenutzers ein.

     ![Screenshot des Azure AD-Anmeldefensters mit Administratoranmeldeinformationen](./media/contoso-migration-tfs-vsts/collection8.png)

1. Die Überprüfung ist bestanden, was vom Tool bestätigt wird.

    ![Screenshot: Überprüfung erfolgreich](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-build-the-migration-files"></a>Schritt 4: Erstellen der Migrationsdateien

Nach Abschluss der Überprüfung können die Contoso-Administratoren mithilfe des Team Foundation Server-Migrationstools die Migrationsdateien erstellen.

1. Sie führen den Vorbereitungsschritt im Tool aus.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Screenshot des Vorbereitungsbefehls im Team Foundation Server-Migrationstool](./media/contoso-migration-tfs-vsts/prep1.png)

    Im Vorbereitungsschritt wird Folgendes ausgeführt:
    - Die Sammlung wird überprüft, um eine Liste aller Benutzer abzurufen, und anschließend wird das Identitätszuordnungsprotokoll (`IdentityMapLog.csv`) aufgefüllt.
    - Die Verbindung mit Azure AD wird vorbereitet, um nach einer Übereinstimmung für jede Identität zu suchen.
    - Contoso hat Azure AD schon bereitgestellt und mit Azure AD Connect synchronisiert, sodass es mit dem Vorbereitungsbefehl möglich sein sollte, die entsprechenden Identitäten zu finden und als **Aktiv** zu markieren.

1. Eine Azure AD-Anmeldeseite wird angezeigt, und die Administratoren geben die Anmeldeinformationen eines globalen Administratorbenutzers ein.

    ![Screenshot des Azure AD-Anmeldefensters mit Administratoranmeldeinformationen](./media/contoso-migration-tfs-vsts/prep2.png)

1. Die Vorbereitung ist abgeschlossen, und das Tool meldet, dass die Importdateien erfolgreich generiert wurden.

    ![Screenshot des Migrationstools, der anzeigt, dass die Sammlungsüberprüfung erfolgreich war](./media/contoso-migration-tfs-vsts/prep3.png)

1. Die Administratoren sehen jetzt, dass sowohl die Datei *IdentityMapLog.csv* als auch die Datei *import.json* in einem neuen Ordner erstellt wurden.

    ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep4.png)

1. Die Datei `import.json` enthält Importeinstellungen. Sie enthält Informationen wie den Namen der gewünschten Organisation und Details zum Speicherkonto. Die meisten Felder werden automatisch aufgefüllt. Einige Felder erfordern eine Benutzereingabe. Die Administratoren öffnen die Datei und fügen den Namen der Azure DevOps Services-Organisation hinzu, die erstellt werden soll: `contosodevmigration`. Bei diesem Namen lautet die Azure DevOps Services-URL von Contoso `contosodevmigration.visualstudio.com`.

    ![Screenshot mit dem Namen der Azure DevOps Services-Organisation](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > Die Organisation muss vor Beginn der Migration erstellt werden. Sie kann geändert werden, wenn die Migration abgeschlossen ist.

1. Die Administratoren überprüfen die Protokolldatei zur Identitätszuordnung, die die Konten anzeigt, die beim Import in Azure DevOps Services eingefügt werden.

    - Aktive Identitäten beziehen sich auf Identitäten, die nach dem Import zu Benutzern in Azure DevOps Services werden.
    - In Azure DevOps Services werden diese Identitäten lizenziert, und nach der Migration werden sie als Benutzer in der Organisation angezeigt.
    - Diese Identitäten werden in der Datei in der Spalte **Erwarteter Importstatus** als **Aktiv** markiert.

    ![Screenshot der Protokolldatei zur Identitätszuordnung, die die Konten anzeigt, die in Azure DevOps Services eingefügt werden sollen](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Schritt 5: Migrieren zu Azure DevOps Services

Wenn die Vorbereitung abgeschlossen ist, können sich die Contoso-Administratoren auf die Migration konzentrieren. Nach der Migration erfolgt der Wechsel von TFVC zu Git für die Versionskontrolle.

Bevor sie loslegen, planen die Administratoren Ausfallzeiten mit dem Entwicklungsteam, damit sie planen können, wann sie die Sammlung für die Migration offline schalten.

Dies ist der ausgeführte Migrationsprozess:

1. **Trennen der Sammlung**. Die Identitätsdaten für die Sammlung befinden sich in der Konfigurationsdatenbank der Team Foundation Server-Instanz, solange die Sammlung angefügt und online ist.

    Wenn eine Sammlung von der Team Foundation Server-Instanz getrennt wird, wird eine Kopie dieser Identitätsdaten erstellt und mit der Sammlung für den Transport gepackt. Ohne diese Daten kann der Identitätsteil des Imports nicht ausgeführt werden.

    Wir empfehlen, die Sammlung getrennt zu lassen, bis der Import abgeschlossen ist, da beim Import aufgetretene Änderungen nicht importiert werden können.

1. **Generieren einer Sicherung**. Der nächste Schritt besteht darin, eine Sicherung zu generieren, die in Azure DevOps Services importiert werden kann. Die Datenschichtanwendungs-Pakete (Data-Tier Application Package, DACPAC) stellen ein SQL Server-Feature dar, mit dem Datenbankänderungen in eine einzelne Datei gepackt und auf anderen SQL-Instanzen bereitgestellt werden können.

    Die Sicherung kann auch direkt in Azure DevOps Services wiederhergestellt werden und wird als Verpackungsmethode verwendet, um Sammlungsdaten zur Cloud zu migrieren. Contoso verwendet das Tool `sqlpackage.exe`, um die DACPAC-Datei zu generieren. Dieses Tool ist in SQL Server Data Tools enthalten.

1. **Hochladen in den Speicher**. Nachdem die DACPAC-Datei erstellt wurde, laden die Administratoren sie in Azure Storage hoch. Nach dem Upload erhalten sie eine Shared Access Signature (SAS), damit das Team Foundation Server-Migrationstool auf den Speicher zugreifen kann.
1. **Ausfüllen der Importfelder**. Contoso kann anschließend die fehlenden Felder in der Importdatei ausfüllen, einschließlich der DACPAC-Einstellung. Die Administratoren legen fest, dass ein _Probeimport_ ausgeführt werden soll, um vor der vollständigen Migration zu überprüfen, ob alles ordnungsgemäß funktioniert.
1. **Ausführen eines Probeimports**. Ein Probeimport unterstützt sie beim Testen der Sammlungsmigration. Probeläufe weisen eine begrenzte Lebensdauer auf und werden daher gelöscht, bevor eine Produktionsmigration ausgeführt wird. Sie werden nach einer festgelegten Dauer automatisch gelöscht. Die nach Abschluss des Imports versendete E-Mail über die erfolgreiche Durchführung enthält einen Hinweis, der Contoso darüber informiert, wann der Probelauf gelöscht wird. Das Team berücksichtigt dies und plant entsprechend.
1. **Abschließen der Produktionsmigration**. Nach Abschluss der Probemigration führen die Contoso-Administratoren die endgültige Migration durch, indem sie die Datei `import.json` aktualisieren und den Import wiederholen.

<!-- docsTest:casing "Team Foundation Server Administration Console" -->

### <a name="detach-the-collection"></a>Trennen der Sammlung

Bevor die Sammlung getrennt wird, erstellen die Contoso-Administratoren eine lokale Sicherung der SQL Server-Instanz und eine VMware-Momentaufnahme der Team Foundation Server-Instanz.

1. In der Team Foundation Server-Verwaltungskonsole wählen die Administratoren die Sammlung aus, die sie trennen möchten: **ContosoDev**.

    ![Screenshot des Abschnitts „Teamprojektsammlungen“ der Foundation Server-Verwaltungskonsole](./media/contoso-migration-tfs-vsts/migrate1.png)

1. Sie wählen die Registerkarte **Allgemein** und anschließend die Option **Sammlung trennen** aus.

    ![Screenshot des Abschnitts „Sammlung trennen“ der Foundation Server-Verwaltungskonsole](./media/contoso-migration-tfs-vsts/migrate2.png)

1. Im Assistenten zum **Trennen von Teamprojektsammlungen** stellen die Administratoren unter **Wartungsmeldung** eine Meldung für Benutzer bereit, die versuchen, eine Verbindung mit Projekten in der Sammlung herzustellen.

    ![Screenshot des Bereichs „Wartungsnachricht“ im Assistenten zum Trennen von Teamprojektsammlungen](./media/contoso-migration-tfs-vsts/migrate3.png)

1. Im Bereich **Trennstatus** wird der Fortschritt überwacht. Wenn der Prozess abgeschlossen ist, wählen sie **Weiter** aus.

    ![Screenshot des Bereichs „Trennstatus“ im Assistenten zum Trennen von Teamprojektsammlungen](./media/contoso-migration-tfs-vsts/migrate5.png)

1. Wenn die Überprüfungen abgeschlossen sind, wählen sie unter **Bereitschaftsprüfungen** die Option **Trennen** aus.

    ![Screenshot des Bereichs „Bereitschaftsprüfungen“ im Assistenten zum Trennen von Teamprojektsammlungen](./media/contoso-migration-tfs-vsts/migrate4.png)

1. Wenn die Sammlung erfolgreich getrennt wurde, wählen sie **Schließen** aus, um die Ausführung abzuschließen.

    ![Screenshot des Bereichs „Vollständig“ im Assistenten zum Trennen von Teamprojektsammlungen](./media/contoso-migration-tfs-vsts/migrate6.png)

    Auf die Sammlung wird in der Team Foundation Server-Verwaltungskonsole nicht mehr verwiesen.

    ![Screenshot der Team Foundation Server-Verwaltungskonsole, der anzeigt, dass die Sammlung nicht mehr aufgelistet wird](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Generieren eines DACPAC

Die Contoso-Administratoren erstellen eine Sicherung bzw. eine DACPAC-Datei für den Import in Azure DevOps Services.

- Die Administratoren verwenden das Hilfsprogramm `sqlpackage.exe` in SQL Server Data Tools (SSDT), um die DACPAC-Datei zu erstellen. Es sind mehrere Versionen von `sqlpackage.exe` in SQL Server Data Tools installiert, die sich in Ordnern mit Namen wie `120`, `130` und `140` befinden. Es ist wichtig, die richtige Version zu verwenden, um die DACPAC-Datei vorzubereiten.

- Bei Team Foundation Server 2018-Importen muss *sqlpackage.exe* aus dem Ordner *140* oder höher verwendet werden. Bei `CONTOSOTFS` befindet sich diese Datei im folgenden Ordner: `C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140`

Die DACPAC-Datei wird von den Contoso-Administratoren wie folgt generiert:

1. Sie öffnen eine Eingabeaufforderung und navigieren zum Speicherort von `sqlpackage.exe`. Zum Generieren der DACPAC-Datei führen sie den folgenden Befehl aus:

    `SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory`

    ![Screenshot der Eingabeaufforderung, der den Befehl zum Erstellen der DACPAC-Datei anzeigt](./media/contoso-migration-tfs-vsts/backup1.png)

    Die folgende Meldung wird angezeigt:

    ![Screenshot der Eingabeaufforderung, der eine Meldung anzeigt, dass die Datenbank erfolgreich extrahiert und in einer DACPAC-Datei gespeichert wurde](./media/contoso-migration-tfs-vsts/backup2.png)

1. Contoso überprüft die Eigenschaften der DACPAC-Datei.

    ![Screenshot mit den DACPAC-Dateieigenschaften für die Überprüfung](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="upload-the-file-to-storage"></a>Hochladen der Datei in den Speicher

Nachdem die Administratoren die DACPAC-Datei erstellt haben, laden sie sie in das Azure-Speicherkonto hoch.

1. Contoso [lädt den Azure Storage-Explorer](https://azure.microsoft.com/features/storage-explorer) herunter und installiert ihn.

    ![Screenshot von „Download Storage Explorer free“ (Storage-Explorer kostenlos herunterladen)](./media/contoso-migration-tfs-vsts/backup5.png)

1. Im Storage-Explorer stellen die Administratoren eine Verbindung mit ihrem Abonnement her und suchen anschließend nach dem Speicherkonto, das sie für die Migration erstellt haben (`contosodevmigration`), und wählen es aus. Contoso erstellt einen neuen Blobcontainer: `azuredevopsmigration`.

    ![Screenshot des Links „BLOB-Container erstellen“ im Storage-Explorer](./media/contoso-migration-tfs-vsts/backup6.png)

1. Im Bereich **Dateien hochladen** in der Dropdownliste **BLOB-Typ** geben die Administratoren **Block-BLOB** für die hochgeladene DACPAC-Datei an.

    ![Screenshot des Bereichs „Dateien hochladen“ im Storage-Explorer](./media/contoso-migration-tfs-vsts/backup7.png)

1. Nachdem die Datei hochgeladen wurde, wählen sie den Dateinamen und anschließend die Option **SAS generieren** aus. Sie erweitern im Speicherkonto die Liste **BLOB-Container** und wählen den Container mit den Importdateien und anschließend **Shared Access Signature abrufen** aus.

    ![Screenshot des Links „Shared Access Signature abrufen“ im Storage-Explorer](./media/contoso-migration-tfs-vsts/backup8.png)

1. Im Bereich **Shared Access Signature** akzeptieren sie die Standardeinstellungen und wählen anschließend **Erstellen** aus. Dies gewährt 24 Stunden lang Zugriff.

    ![Screenshot des Bereichs „Shared Access Signature“ im Storage-Explorer](./media/contoso-migration-tfs-vsts/backup9.png)

1. Sie kopieren die Shared Access Signature-URL, damit sie vom Team Foundation Server-Migrationstool verwendet werden kann.

    ![Screenshot der URL der Shared Access Signature im Storage-Explorer](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> Die Migration muss innerhalb des zulässigen Zeitfensters erfolgen. Anderenfalls laufen die Berechtigungen ab. SAS-Schlüssel dürfen *nicht* über das Azure-Portal generiert werden. Schlüssel, die über das Portal generiert werden, sind kontobezogen und funktionieren nicht beim Import.

### <a name="fill-in-the-import-settings"></a>Ausfüllen der Importeinstellungen

In einem vorherigen Schritt haben die Contoso-Administratoren einen Teil der Importspezifikationsdatei *import.json* ausgefüllt. Nun muss das Unternehmen die übrigen Einstellungen hinzufügen.

Sie öffnen die Datei *import.json* und füllen die folgenden Felder aus:

- **Standort**: Sie geben den Speicherort des SAS-Schlüssels ein, der oben generiert wurde.
- **Dacpac:** Sie geben den Namen der DACPAC-Datei ein, die zuvor in das Speicherkonto hochgeladen wurde, einschließlich der Erweiterung *.dacpac*.
- **ImportType:** Sie geben **DryRun** ein.

![Screenshot der Datei „import.json mit ausgefüllten Feldern](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="perform-a-dry-run-migration"></a>Ausführen eines Probeimports

Die Contoso-Administratoren führen eine Probemigration durch, um sicherzustellen, dass alles wie erwartet funktioniert.

1. Sie öffnen eine Eingabeaufforderung und navigieren zum Speicherort von `TfsMigrator` (`C:\TFSMigrator`).
1. Anschließend möchten sie sicherstellen, dass die Datei ordnungsgemäß formatiert ist und dass der SAS-Schlüssel funktioniert. Sie überprüfen die Importdatei mithilfe des folgenden Befehls:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    Die Überprüfung gibt einen Fehler zurück, der angibt, dass der SAS-Schlüssel eine längere Dauer bis zum Ablauf benötigt.

    ![Screenshot der Eingabeaufforderung, der einen Validierungsfehler anzeigt](./media/contoso-migration-tfs-vsts/test1.png)

1. Sie erstellen mithilfe des Azure Storage-Explorers einen neuen SAS-Schlüssel, bei dem die Dauer bis zum Ablauf auf sieben Tage festgelegt ist.

    ![Screenshot des Storage-Explorer-Bereichs „Shared Access Signature“, der das Ablaufdatum anzeigt](./media/contoso-migration-tfs-vsts/test2.png)

1. Die Administratoren aktualisieren die Datei `import.json` und führen den Befehl wird erneut aus. Dieses Mal wird die Überprüfung erfolgreich abgeschlossen.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Screenshot der Eingabeaufforderung mit der Meldung, dass die Überprüfung erfolgreich abgeschlossen wurde](./media/contoso-migration-tfs-vsts/test3.png)

1. Sie führen den Probelauf mithilfe des folgenden Befehls aus:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

    Eine Meldung wird angezeigt, in der sie aufgefordert werden, zu bestätigen, dass sie die Migration fortsetzen möchten. Beachten Sie, dass die bereitgestellten Daten nach dem Probelauf für eine Dauer von sieben Tagen gespeichert werden.

    ![Screenshot der Meldung, in der Contoso aufgefordert wird, zu bestätigen, dass die Migration fortgesetzt werden soll](./media/contoso-migration-tfs-vsts/test4.png)

1. Das Azure AD-Anmeldefenster wird geöffnet. Die Contoso-Administratoren melden sich bei Azure AD mit Administratorberechtigungen an.

    ![Screenshot des Azure AD-Anmeldefensters in Visual Studio](./media/contoso-migration-tfs-vsts/test5.png)

    Eine Meldung wird angezeigt mit dem Hinweis, dass der Import erfolgreich gestartet wurde.

    ![Screenshot: Import erfolgreich gestartet](./media/contoso-migration-tfs-vsts/test6.png)

1. Nach ca. 15 Minuten wechseln die Administratoren zur Website und sehen die folgenden Informationen:

     ![Screenshot: Sammlung wird wiederhergestellt](./media/contoso-migration-tfs-vsts/test7.png)

1. Nach Abschluss der Migration meldet sich ein Contoso-Entwicklungsleiter bei Azure DevOps Services an, um zu überprüfen, ob der Probelauf ordnungsgemäß durchgeführt wurde. Nach der Authentifizierung benötigt Azure DevOps Services einige Details zum Bestätigen der Organisation.

    ![Screenshot des Azure DevOps Services-Fensters, das zusätzliche Informationen vom Contoso-Team anfordert](./media/contoso-migration-tfs-vsts/test8.png)

    Der Entwicklungsleiter sieht, dass die Projekte erfolgreich migriert wurden. Ein Hinweis oben auf der Seite warnt, dass das Probekonto nach 15 Tagen gelöscht wird.

    ![Screenshot der Azure DevOps Services-Oberfläche mit einer Warnmeldung, dass das Probekonto innerhalb von 15 Tagen gelöscht wird.](./media/contoso-migration-tfs-vsts/test9.png)

1. Der Entwicklungsleiter öffnet eines der Projekte und wählt **Arbeitselemente** > **Mir zugewiesen** aus. Auf dieser Seite wird überprüft, ob die Arbeitselementdaten zusammen mit der Identität erfolgreich migriert wurden.

    ![Screenshot des Azure DevOps Services-Bereichs „Arbeitselemente“, in dem alle migrierten Projekte angezeigt werden](./media/contoso-migration-tfs-vsts/test10.png)

1. Außerdem überprüft der Entwicklungsleiter andere Projekte und Code, um sicherzustellen, dass der Quellcode und der Verlauf migriert wurden.

    ![Screenshot des Azure DevOps Services-Bereich „Verlauf“, der anzeigt, dass der gesamte Code und der Verlauf migriert wurden](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Ausführen der Produktionsmigration

Wenn der Probelauf abgeschlossen ist, fahren die Contoso-Administratoren mit der Produktionsmigration fort. Contoso löscht den Probelauf, aktualisiert die Importeinstellungen und führt den Import erneut aus.

1. Im Azure DevOps Services-Portal löscht Contoso die Organisation für den Probelauf.
1. Es aktualisiert die Datei `import.json`, um **ImportType** auf **ProductionRun** festzulegen.

    ![Screenshot des Azure DevOps Services-Portals, wobei das Feld „ImportType“ auf „ProductionRun“ festgelegt ist](./media/contoso-migration-tfs-vsts/full1.png)

1. Wie auch beim Probelauf wird die Migration durch Ausführen des folgenden Befehls gestartet:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`.

    Eine Meldung wird angezeigt, in der die Administratoren aufgefordert werden, die Migration zu bestätigen. Sie weist darauf hin, dass Daten bis zu sieben Tage lang an einem sicheren Speicherort als Stagingbereich gespeichert werden können.

    ![Screenshot einer Azure DevOps Services-Warnmeldung, dass die migrierten Daten bis zu sieben Tage lang aufbewahrt werden können](./media/contoso-migration-tfs-vsts/full2.png)

1. Im Azure AD-Anmeldefenster geben die Administratoren eine Contoso-Administratoranmeldung an.

    ![Screenshot des Azure AD-Anmeldefensters in Visual Studio](./media/contoso-migration-tfs-vsts/full3.png)

    Eine Meldung wird angezeigt mit dem Hinweis, dass der Import erfolgreich gestartet wurde.

    ![Screenshot einer Azure DevOps Services-Meldung, dass der Import erfolgreich gestartet wurde](./media/contoso-migration-tfs-vsts/full4.png)

1. Nach ca. 15 Minuten wechseln die Administratoren zur Website und sehen die folgenden Informationen:

    ![Screenshot: Daten werden in die Cloud kopiert](./media/contoso-migration-tfs-vsts/full5.png)

1. Nach Abschluss der Migration meldet sich ein Entwicklungsleiter bei Azure DevOps Services an, um zu überprüfen, ob die Migration ordnungsgemäß durchgeführt wurde. Nach der Anmeldung kann der Entwicklungsleiter erkennen, dass Projekte migriert wurden.

    ![Screenshot: Projekte wurden migriert](./media/contoso-migration-tfs-vsts/full6.png)

1. Der Entwicklungsleiter öffnet eines der Projekte und wählt **Arbeitselemente** > **Mir zugewiesen** aus. Dies weist darauf hin, dass die Arbeitselementdaten zusammen mit der zugehörigen Identität migriert wurden.

    ![Screenshot: Arbeitselementdaten und die Identität wurden migriert](./media/contoso-migration-tfs-vsts/full7.png)

1. Der Entwicklungsleiter überprüft, ob andere Arbeitselementdaten migriert wurden

    ![Screenshot, der zusätzliche Arbeitselementdaten auflistet, die bestätigt werden müssen](./media/contoso-migration-tfs-vsts/full8.png)

1. Außerdem überprüft der Entwicklungsleiter andere Projekte und Code, um sicherzustellen, dass der Quellcode und der Verlauf migriert wurden.

    ![Screenshot, der zusätzliche Projekt- und Quellcodemigrationen auflistet, die bestätigt werden müssen](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Migrieren der Quellcodeverwaltung von TFVC nach Git

Nachdem die Migration abgeschlossen ist, möchten die Administratoren von Contoso die Quellcodeverwaltung von TFVC zu Git verschieben. Die Administratoren müssen den Quellcode, der sich derzeit in der Azure DevOps Services-Organisation befindet, als Git-Repositorys in dieselbe Organisation importieren.

1. Im Azure DevOps Services-Portal öffnet Contoso eines der TFVC-Repositorys (`$/PolicyConnect`) und überprüft dieses.

    ![Screenshot des Repositorys „$/PolicyConnect“ im Azure DevOps Services-Portal](./media/contoso-migration-tfs-vsts/git1.png)

1. Sie wählen in der Quelldropdownliste **$/PolicyConnect** **Repository importieren** aus.

    ![Screenshot des Links „Repository importieren“ im Azure DevOps Services-Portal](./media/contoso-migration-tfs-vsts/git2.png)

1. In der Dropdownliste **Quelltyp** wählen sie **TFVC** aus. Im Feld **Pfad** geben sie den Pfad zum Repository an und wählen anschließend **Importieren** aus. Das Kontrollkästchen **Verlauf migrieren**  wird nicht deaktiviert.

    ![Screenshot des Bereichs „Aus TFVC importieren“](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > Aufgrund der Unterschiede bei der Speicherung von Versionskontrollinformationen in TFVC und Git empfehlen wir, dass Contoso seinen Repositoryverlauf *nicht* migriert. Dies ist auch der Ansatz, den Microsoft verfolgt hat, als Windows und andere Produkte von der zentralen Versionskontrolle zu Git migriert wurden.

1. Nach dem Import überprüfen die Administratoren den Code.

    ![Screenshot, der bestätigt, dass der Import erfolgreich war](./media/contoso-migration-tfs-vsts/git4.png)

1. Das Unternehmen wiederholt den Prozess für das zweite Repository (`$/smarthotelcontainer`).

    ![Screenshot des Bereichs „Aus TFVC importieren“ für das zweite Repository](./media/contoso-migration-tfs-vsts/git5.png)

1. Nach der Überprüfung der Quelle durch den Entwicklungsleiter ist die Migration zu Azure DevOps Services fertiggestellt. Azure DevOps Services wird jetzt zur Quelle für die gesamte Entwicklung in Teams, die an der Migration beteiligt sind.

    ![Screenshot: Migration zu Azure DevOps Services ist abgeschlossen](./media/contoso-migration-tfs-vsts/git6.png)

**Benötigen Sie weitere Hilfe?**

Weitere Informationen finden Sie unter [Importieren von Repositorys aus TFVC in Git](/azure/devops/repos/git/import-from-TFVC?view=vsts).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nachdem die Migration abgeschlossen wurde, muss das Contoso-Team folgende Schritte ausführen:

- Informationen zu zusätzlichen Importaktionen finden Sie im Artikel mit den Schritten [nach dem Import](/azure/devops/articles/migration-post-import?view=vsts).
- Sie müssen die TFVC-Repositorys entweder löschen oder in den schreibgeschützten Modus versetzen. Die Codebasen dürfen nicht verwendet werden, für deren Verlauf kann jedoch auf diese verwiesen werden.

## <a name="post-migration-training"></a>Schulungen nach der Migration

Das Contoso-Team muss Schulungen zu Azure DevOps Services und Git für die beteiligten Teammitglieder bereitstellen.
