---
title: Umgestalten einer Team Foundation Server-Bereitstellung zu Azure DevOps Services in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: In diesem Artikel erfahren Sie, wie Contoso seine lokale TFS-Bereitstellung durch Migration zu Azure DevOps Services in Azure umgestaltet.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 3c87bfbd8fe920d0469da8b3e60da59da07158ed
ms.sourcegitcommit: 0b6939f65a1e5653149301e9aa14db9a1f67825f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2019
ms.locfileid: "74557024"
---
# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Umgestalten einer Team Foundation Server-Bereitstellung zu Azure DevOps Services

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso seine lokale Team Foundation Server-Bereitstellung (TFS) durch Migration zu Azure DevOps Services in Azure umgestaltet. Das Contoso-Entwicklungsteam hat in den letzten fünf Jahren TFS für die Zusammenarbeit im Team und die Quellcodeverwaltung verwendet. Nun möchte es für Entwicklungen und Tests sowie für die Quellcodeverwaltung auf eine cloudbasierte Lösung umsteigen. Azure DevOps Services spielt eine wichtige Rolle bei der Migration zu einem Azure DevOps-Modell und der Entwicklung neuer nativer Cloud-Apps.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Führungsteam arbeitet eng mit den jeweiligen Unternehmen zusammen, um zukünftige Ziele zu identifizieren. Die Geschäftspartner haben sich nicht im Detail mit Entwicklungstools und -technologien befasst, haben jedoch die folgenden Punkte zusammengefasst:

- **Software:** Unabhängig vom Kerngeschäft handelt es sich bei allen Unternehmen nun um Softwareunternehmen, einschließlich Contoso. Die Unternehmensführung ist interessiert daran, wie die IT dem Unternehmen bei neuen Vorgehensweisen für Benutzer und Benutzererfahrungen seiner Kunden unterstützen kann.
- **Effizienz**: Contoso muss Prozesse optimieren und unnötige Verfahren für Entwickler und Benutzer entfernen. Nur so kann das Unternehmen im Hinblick auf die Anforderungen der Kunden effizienter Ergebnisse liefern. Das Unternehmen benötigt eine schnell agierende IT, die ohne Zeit- oder Geldverschwendung auskommt.
- **Flexibilität**: Die IT von Contoso muss auf geschäftliche Anforderungen reagieren und dabei schneller als im Marketplace, um Erfolg in einer globalen Wirtschaft zu garantieren. Die IT darf kein Stolperstein für das Unternehmen sein.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration zu Azure DevOps Services gesetzt:

- Das Team benötigt ein Tool, um die Daten in die Cloud zu migrieren. Wenige manuelle Prozesse sollten erforderlich sein.
- Arbeitselementdaten und der Verlauf für das letzte Jahr müssen migriert werden.
- Neue Benutzernamen und Kennwörter sollen nicht eingerichtet werden müssen. Alle aktuellen Systemzuweisungen müssen beibehalten werden.
- Für die Quellcodeverwaltung soll eine Umstellung von der Team Foundation-Versionskontrolle (Team Foundation Version Control, TFVC) auf Git durchgeführt werden.
- Die Umstellung auf Git stellt eine „abgespeckte Migration“ dar, bei der nur die neueste Version des Quellcodes importiert wird. Sie wird während einer Ausfallzeit durchgeführt, in der alle Aufgaben bei der Migration der Codebasis angehalten werden. Allen Beteiligten ist bewusst, dass nur der aktuelle Masterbranchverlauf nach der Migration zur Verfügung steht.
- Die Teammitglieder machen sich Sorgen über die Änderung und möchten vor einer vollständigen Migration Tests durchführen. Sie möchten auch nach dem Umstieg auf Azure DevOps Services weiterhin auf TFS zugreifen können.
- Sie verfügen über mehrere Sammlungen und möchten mit einer Sammlung beginnen, die nur wenige Projekte enthält, um den Prozess besser zu verstehen.
- Es ist ihnen bewusst, dass TFS-Sammlungen in einem direkten Verhältnis zu Azure DevOps Services-Organisationen stehen, sodass sie über mehrere URLs verfügen. Dies entspricht jedoch ihrem aktuellen Modell einer Trennung von Codebasen und Projekten.

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Contoso migriert seine TFS-Projekte in die Cloud und hostet Projekte oder die Quellcodeverwaltung nicht mehr lokal.
- TFS wird zu Azure DevOps Services migriert.
- Contoso verfügt derzeit über eine TFS-Sammlung namens `ContosoDev`, die zu einer Azure DevOps Services-Organisation namens `contosodevmigration.visualstudio.com` migriert werden soll.
- Die Projekte, Arbeitselemente, Fehler und Iterationen aus dem letzten Jahr werden zu Azure DevOps Services migriert.
- Contoso verwendet Azure Active Directory, das bei der [Bereitstellung der Azure-Infrastruktur](./contoso-migration-infrastructure.md) zu Beginn der Migrationsplanung eingerichtet wird.

![Szenarioarchitektur](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Migrationsprozess

Contoso wird den Migrationsprozess wie folgt abschließen:

1. Dies erfordert viele Vorbereitungsschritte. Zunächst muss Contoso ein Upgrade für seine TFS-Implementierung auf eine unterstützte Ebene durchführen. Contoso führt zurzeit TFS 2017 Update 3 aus, für die Datenbankmigration muss jedoch eine unterstützte 2018-Version mit den neuesten Updates ausgeführt werden.
2. Nach dem Upgrade führt Contoso das TFS-Migrationstool aus und überprüft die Sammlung.
3. Contoso erstellt eine Gruppe von Vorbereitungsdateien und führt probeweise eine Migration zu Testzwecken durch.
4. Anschließend wird eine weitere Migration durchgeführt, dieses Mal jedoch eine vollständige Migration, die Arbeitselemente, Fehler, Sprints und Code beinhaltet.
5. Nach der Migration migriert Contoso seinen Code von TFVC nach Git.

![Migrationsprozess](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes.

<!-- markdownlint-disable MD033 -->

**Anforderungen** | **Details**
--- | ---
**Azure-Abonnement** | Contoso hat in einem früheren Artikel dieser Reihe Abonnements erstellt. Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/pricing/free-trial) erstellen.<br/><br/> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen.<br/><br/> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist.<br/><br/> Wenn Sie detailliertere Berechtigungen benötigen, lesen Sie [diesen Artikel](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Azure-Infrastruktur** | Contoso richtet die Azure-Infrastruktur ein, wie in [Azure infrastructure for migration (Azure-Infrastruktur für die Migration)](./contoso-migration-infrastructure.md) beschrieben.
**Lokaler TFS-Server** | Lokal muss entweder TFS 2018 Upgrade 2 ausgeführt werden, oder das Upgrade muss während dieses Vorgangs erfolgen.

## <a name="scenario-steps"></a>Szenarioschritte

Contoso geht bei der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Erstellen eines Azure-Speicherkontos.** Dieses Speicherkonto wird beim Migrationsvorgang verwendet.
> - **Schritt 2: Upgrade von TFS.** Contoso aktualisiert seine Bereitstellung auf TFS 2018 Upgrade 2.
> - **Schritt 3: Überprüfen der Sammlung.** Contoso überprüft die TFS-Sammlung als Vorbereitung auf die Migration.
> - **Schritt 4: Erstellen der Vorbereitungsdatei.** Contoso erstellt die Migrationsdateien mit dem TFS-Migrationstool.

## <a name="step-1-create-a-storage-account"></a>Schritt 1: Speicherkonto erstellen

1. Die Contoso-Administratoren erstellen im Azure-Portal ein Speicherkonto (**contosodevmigration**).
2. Das Konto wird in die sekundäre Region platziert, die das Unternehmen für das Failover zu „USA, Mitte“ verwendet. Ein allgemeines Standardkonto mit lokal redundantem Speicher wird verwendet.

    ![Speicherkonto](./media/contoso-migration-tfs-vsts/storage1.png)

**Benötigen Sie weitere Hilfe?**

- [Einführung in Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction)
- [Informationen zu Azure-Speicherkonten](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)

## <a name="step-2-upgrade-tfs"></a>Schritt 2: Upgrade von TFS

Die Contoso-Administratoren aktualisieren den TFS-Server auf TFS 2018 Update 2. Vor der Durchführung:

- Contoso lädt [TFS 2018 Update 2](https://visualstudio.microsoft.com/downloads) herunter.
- Das Unternehmen überprüft die [Hardwareanforderungen](/azure/devops/server/requirements) und geht die [Anmerkungen zu dieser Version](https://docs.microsoft.com/visualstudio/releasenotes/tfs2018-relnotes) und [Upgradegotchas](/azure/devops/server/upgrade/get-started#before-you-upgrade-to-tfs-2018) durch.

Das Upgrade wird wie folgt durchgeführt:

1. Zunächst wird der TFS-Server (ausgeführt auf einer VMware-VM) gesichert, und eine VMware-Momentaufnahme wird erstellt.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png)

2. Das TFS-Installationsprogramm wird gestartet, und der Installationsspeicherort wird ausgewählt. Für das Installationsprogramm ist Internetzugriff erforderlich.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png)

3. Nach Abschluss der Installation wird der Serverkonfigurations-Assistent gestartet.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png)

4. Nach der Überprüfung führt der Assistent das Upgrade durch.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png)

5. Contoso überprüft die TFS-Installation anhand von Projekten, Arbeitselementen und Code.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Einige TFS-Upgrades müssen den Featurekonfigurations-Assistenten ausführen, wenn das Upgrade abgeschlossen ist. [Weitere Informationen](https://docs.microsoft.com/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts)

**Benötigen Sie weitere Hilfe?**

Informationen zum Durchführen von Upgrades für TFS finden Sie [hier](/azure/devops/server/upgrade/get-started).

## <a name="step-3-validate-the-tfs-collection"></a>Schritt 3: Überprüfen der TFS-Sammlung

Die Contoso-Administratoren führen das TFS-Migrationstool für die ContosoDev-Sammlungsdatenbank aus, um diese vor der Migration zu überprüfen.

1. Sie laden das [TFS-Migrationstool](https://www.microsoft.com/download/details.aspx?id=54274) herunter und entpacken es. Es muss unbedingt die Version für das ausgeführte TFS-Update heruntergeladen werden. Die Version kann in die Verwaltungskonsole eingecheckt werden.

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. Das Tool zur Überprüfung wird ausgeführt, indem die URL der Projektsammlung angegeben wird:

        `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

3. Im Tool wird ein Fehler angezeigt.

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

4. Eine Suche nach den Protokolldateien wurde durchgeführt, die sich im Ordner `Logs`, direkt vor dem Speicherort des Tools, befinden. Eine Protokolldatei wird für jede wichtige Überprüfung generiert. `TfsMigration.log` enthält die wichtigsten Informationen.

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

5. Sie suchen diesen Eintrag im Zusammenhang mit der Identität.

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

6. Sie führen `TfsMigrator validate /help` in der Befehlszeile aus und sehen, dass der Befehl `/tenantDomainName` erforderlich zu sein scheint, um Identitäten zu überprüfen.

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

7. Sie führen den Überprüfungsbefehl erneut aus und schließen diesen Wert, zusammen mit ihrem Azure AD-Namen, ein: `TfsMigrator validate /collection: http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

8. Eine Azure AD-Anmeldeseite wird angezeigt, und die Administratoren geben die Anmeldeinformationen eines globalen Administratorbenutzers ein.

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

9. Die Überprüfung ist bestanden, was vom Tool bestätigt wird.

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-create-the-migration-files"></a>Schritt 4: Erstellen der Migrationsdateien

Nach Abschluss der Überprüfung können die Contoso-Administratoren mithilfe des TFS-Migrationstools die Migrationsdateien erstellen.

1. Das Unternehmen führt den Vorbereitungsschritt im Tool aus.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep1.png)

    Bei der Vorbereitung werden folgende Schritte ausgeführt:
    - Die Sammlung wird überprüft, um eine Liste aller Benutzer abzurufen, und das Identitätszuordnungsprotokoll (**IdentityMapLog.csv**) wird aufgefüllt.
    - Die Verbindung mit Azure Active Directory wird vorbereitet, um nach einer Übereinstimmung für jede Identität zu suchen.
    - Contoso hat Azure AD schon bereitgestellt und mit Azure AD Connect synchronisiert, sodass es bei der Vorbereitung möglich sein sollte, die entsprechenden Identitäten zu finden und als aktiv zu markieren.

2. Eine Azure AD-Anmeldeseite wird angezeigt, und die Administratoren geben die Anmeldeinformationen eines globalen Administratorbenutzers ein.

    ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep2.png)

3. Die Vorbereitung ist abgeschlossen, und das Tool meldet, dass die Importdateien erfolgreich generiert wurden.

    ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep3.png)

4. Die Administratoren können jetzt sehen, dass sowohl die Datei „IdentityMapLog.csv“ als auch die Datei „import.json“ in einem neuen Ordner erstellt wurden.

    ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep4.png)

5. Die Datei „import.json“ enthält Importeinstellungen. Sie enthält Informationen wie den Namen der gewünschten Organisation und Informationen zum Speicherkonto. Die meisten Felder werden automatisch aufgefüllt. Einige Felder erfordern eine Benutzereingabe. Contoso öffnet die Datei und fügt den Namen der Azure DevOps Services-Organisation hinzu, der erstellt werden soll: **contosodevmigration**. Bei diesem Namen lautet die Azure DevOps Services-URL **contosodevmigration.visualstudio.com**.

    ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > Die Organisation muss vor der Migration erstellt werden und kann nach Abschluss der Migration geändert werden.

6. Die Protokolldatei zur Identitätszuordnung enthält die Konten, die beim Import in Azure DevOps Services eingefügt werden.

    - Aktive Identitäten beziehen sich auf Identitäten, die nach dem Import zu Benutzern in Azure DevOps Services werden.
    - In Azure DevOps Services werden diese Identitäten lizenziert, und nach der Migration werden sie als Benutzer in der Organisation angezeigt.
    - Diese Identitäten werden in der Datei in der Spalte **Erwarteter Importstatus** als **Aktiv** markiert.

    ![Vorbereiten](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Schritt 5: Migrieren zu Azure DevOps Services

Ist die Vorbereitung abgeschlossen, können sich die Contoso-Administratoren nun auf die Migration konzentrieren. Nach der Ausführung der Migration erfolgt der Wechsel von TFVC zu Git für die Versionskontrolle.

Bevor sie mit der Verwendung beginnen, planen die Administratoren Ausfallzeiten mit dem Entwicklungsteam, um die Sammlung für die Migration offline zu schalten. Der Migrationsprozess umfasst folgende Schritte:

1. **Trennen der Sammlung.** Identitätsdaten für die Sammlung befinden sich in der Konfigurationsdatenbank des TFS-Servers, solange die Sammlung angefügt und online ist. Wenn eine Sammlung vom TFS-Server getrennt wird, wird eine Kopie dieser Identitätsdaten erstellt und mit der Sammlung für den Transport gepackt. Ohne diese Daten kann der Identitätsteil des Imports nicht ausgeführt werden. Es wird empfohlen, die Sammlung getrennt zu lassen, bis der Import abgeschlossen ist, da anderenfalls nicht die beim Import aufgetretenen Änderungen importiert werden können.
2. **Generieren einer Sicherung.** Der nächste Schritt des Migrationsvorgangs besteht darin, eine Sicherung zu generieren, die in Azure DevOps Services importiert werden kann. Datenschichtanwendungs-Pakete (Data-Tier Application Package, DACPAC) stellen ein SQL Server-Feature dar, mit dem Datenbankänderungen in eine einzelne Datei gepackt und auf anderen SQL-Instanzen bereitgestellt werden können. Diese können auch direkt in Azure DevOps Services wiederhergestellt werden und werden daher als Verpackungsmethode verwendet, um Sammlungsdaten zur Cloud zu migrieren. Contoso verwendet das Tool „SqlPackage.exe“, um die DACPAC-Datei zu generieren. Dieses Tool ist in SQL Server Data Tools enthalten.
3. **Hochladen in den Speicher.** Nachdem die DACPAC-Datei erstellt wurde, wird sie in Azure Storage hochgeladen. Nach dem Upload wird sie mit einer Shared Access Signature (SAS) versehen, damit das TFS-Migrationstool auf den Speicher zugreifen kann.
4. **Ausfüllen der Importfelder.** Contoso kann danach die fehlenden Felder in der Importdatei ausfüllen, einschließlich der DACPAC-Einstellung. Für den Einstieg legt das Unternehmen fest, dass ein **Probeimport** ausgeführt werden soll, um vor der vollständigen Migration zu überprüfen, dass alles ordnungsgemäß funktioniert.
5. **Ausführen eines Probelaufs.** Durch einen Probelauf von Importen kann die Migration von Sammlungen getestet werden. Probeläufe weisen eine begrenzte Lebensdauer auf und werden gelöscht, bevor eine Produktionsmigration ausgeführt wird. Sie werden nach einer festgelegten Dauer automatisch gelöscht. Ein Hinweis zu dem Zeitpunkt, an dem der Probelauf gelöscht wird, wird in der E-Mail über die erfolgreiche Durchführung angegeben, nachdem der Importvorgang abgeschlossen ist. Berücksichtigen Sie dies, und passen Sie Ihre Planung entsprechend an.
6. **Durchführen der Produktionsmigration.** Nach Abschluss der Probelaufmigration führen die Contoso-Administratoren die endgültige Migration durch, indem sie die Datei **import.json** aktualisieren und den Import wiederholen.

### <a name="detach-the-collection"></a>Trennen der Sammlung

Vor dem Trennen der Sammlung erstellen die Contoso-Administratoren eine lokale SQL Server-Sicherung und eine VMware-Momentaufnahme des TFS-Servers.

1. In der TFS-Verwaltungskonsole wählt Contoso die Sammlung aus, die getrennt werden soll (**ContosoDev**).

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate1.png)

2. Unter **Allgemein** wählt Contoso **Sammlung trennen** aus.

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate2.png)

3. Im Assistenten zum Trennen von Teamprojektsammlungen wird unter **Wartungsmeldung** eine Meldung für Benutzer angezeigt, die versuchen, eine Verbindung mit Projekten in der Sammlung herzustellen.

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate3.png)

4. Unter **Trennstatus** überwacht Contoso den Status und wählt **Weiter** aus, wenn der Prozess abgeschlossen ist.

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate4.png)

5. Wenn die Überprüfungen abgeschlossen sind, wählt Contoso unter **Bereitschaftsprüfungen** die Option **Trennen** aus.

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate5.png)

6. Contoso wählt **Schließen** aus, um den Vorgang zu beenden.

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate6.png)

7. Auf die Sammlung wird nicht mehr in der TFS-Verwaltungskonsole verwiesen.

    ![Migrieren](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Generieren eines DACPAC

Contoso erstellt eine Sicherung (DACPAC) für den Import in Azure DevOps Services.

- SqlPackage.exe in SQL Server Data Tools wird verwendet, um die DACPAC-Datei zu erstellen. Es sind mehrere Versionen von SqlPackage.exe in SQL Server Data Tools installiert, die sich im Ordner mit Namen wie etwa „120“, „130“ und „140“ befinden. Es ist wichtig, die richtige Version zu verwenden, um die DACPAC-Datei vorzubereiten.
- Bei TFS 2018-Importen muss SqlPackage.exe aus dem Ordner „140“ oder höher verwendet werden. Bei CONTOSOTFS befindet sich diese Datei im folgenden Ordner: **C:\Programme (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140**.

Die DACPAC-Datei wird von den Contoso-Administratoren wie folgt generiert:

1. Contoso öffnet eine Eingabeaufforderung und navigiert zum Speicherort von „SQLPackage.exe“. Contoso gibt den folgenden Befehl ein, um die DACPAC-Datei zu generieren:

    ``` console
    SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory
    ```

    ![Backup](./media/contoso-migration-tfs-vsts/backup1.png)

2. Nachdem der Befehl ausgeführt wurde, wird die folgende Meldung angezeigt.

    ![Backup](./media/contoso-migration-tfs-vsts/backup2.png)

3. Sie überprüfen die Eigenschaften der DACPAC-Datei.

    ![Backup](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a>Aktualisieren der Datei im Speicher

Nachdem die DACPAC-Datei erstellt wurde, wird es von Contoso in Azure Storage hochgeladen.

1. Contoso [lädt den Azure Storage-Explorer](https://azure.microsoft.com/features/storage-explorer) herunter und installiert ihn.

    ![Hochladen](./media/contoso-migration-tfs-vsts/backup5.png)

2. Contoso stellt eine Verbindung mit dem jeweiligen Abonnement her und sucht das Speicherkonto, das das Unternehmen für die Migration erstellt hat (**contosodevmigration**). Contoso erstellt einen neuen Blobcontainer: **azuredevopsmigration**.

    ![Hochladen](./media/contoso-migration-tfs-vsts/backup6.png)

3. Contoso gibt die DACPAC-Datei für den Upload als Blockblob an.

    ![Hochladen](./media/contoso-migration-tfs-vsts/backup7.png)

4. Nachdem die Datei hochgeladen wurde, wählt Contoso den Dateinamen und dann **SAS generieren** aus. Contoso erweitert die Blobcontainer im Speicherkonto, wählt den Container mit den Importdateien und dann **Shared Access Signature abrufen** aus.

    ![Hochladen](./media/contoso-migration-tfs-vsts/backup8.png)

5. Contoso übernimmt die Standardwerte und wählt **Erstellen** aus. Dies gewährt 24 Stunden lang Zugriff.

    ![Hochladen](./media/contoso-migration-tfs-vsts/backup9.png)

6. Contoso kopiert die Shared Access Signature-URL, damit sie vom TFS-Migrationstool verwendet werden kann.

    ![Hochladen](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> Die Migration muss innerhalb des zulässigen Zeitfensters erfolgen. Anderenfalls laufen die Berechtigungen ab.
> SAS-Schlüssel dürfen nicht über das Azure-Portal generiert werden. Schlüssel, die auf diese Weise generiert werden, sind kontobezogen und funktionieren nicht beim Import.

### <a name="fill-in-the-import-settings"></a>Ausfüllen der Importeinstellungen

In einem vorherigen Schritt haben die Contoso-Administratoren einen Teil der Importspezifikationsdatei (import.json) ausgefüllt. Nun muss das Unternehmen die übrigen Einstellungen hinzufügen.

Contoso öffnet die Datei „import.json“ und füllt die folgenden Felder aus:

- **Standort:** Speicherort des SAS-Schlüssels, der oben generiert wurde.
- **Dacpac:** Hier wird der Name der DACPAC-Datei festgelegt, die Sie in das Speicherkonto hochgeladen haben. Schließen Sie die Erweiterung „DACPAC“ ein.
- **ImportType:** Dieser wird vorerst auf DryRun festgelegt.

![Importieren von Einstellungen](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="do-a-dry-run-migration"></a>Ausführen einer Probelaufmigration

Die Contoso-Administratoren beginnen mit einer Probelaufmigration, um sicherzustellen, dass alles wie erwartet funktioniert.

1. Contoso öffnet eine Eingabeaufforderung und navigiert zum Speicherort von „TfsMigration“ (`C:\TFSMigrator`).
2. Im ersten Schritt überprüft Contoso die Importdatei. Anschließend sollte sichergestellt werden, dass die Datei ordnungsgemäß formatiert ist und dass der SAS-Schlüssel funktioniert.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

3. Die Überprüfung gibt einen Fehler zurück, der besagt, dass der SAS-Schlüssel eine längere Ablaufzeit benötigt.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test1.png)

4. Contoso erstellt mithilfe des Azure Storage-Explorers einen neuen SAS-Schlüssel, bei dem der Ablauf auf sieben Tage festgelegt ist.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test2.png)

5. Contoso aktualisiert die Datei `import.json` und führt die Überprüfung erneut aus. Dieses Mal wird diese erfolgreich abgeschlossen.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Probelauf](./media/contoso-migration-tfs-vsts/test3.png)

6. Contoso startet den Probelauf:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

7. Eine Meldung wird ausgegeben, um die Migration zu bestätigen. Beachten Sie die Zeitspanne, für die die bereitgestellten Daten nach dem Probelauf beibehalten werden.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test4.png)

8. Das Azure AD-Anmeldefenster wird angezeigt und sollte mit der Contoso-Administratoranmeldung durchgeführt werden.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test5.png)

9. Eine Meldung zeigt Informationen zum Import an.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test6.png)

10. Nach etwa 15 Minuten rufen sie die URL auf und sehen die folgenden Informationen:

     ![Probelauf](./media/contoso-migration-tfs-vsts/test7.png)

11. Nach Abschluss der Migration meldet sich ein Contoso-Entwicklungsleiter bei Azure DevOps Services an, um zu überprüfen, ob der Probelauf ordnungsgemäß durchgeführt wurde. Nach der Authentifizierung benötigt Azure DevOps Services einige Details zum Bestätigen der Organisation.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test8.png)

12. In Azure DevOps Services kann der Entwicklungsleiter sehen, dass die Projekte zu Azure DevOps Services migriert wurden. In einer Benachrichtigung wird darauf hingewiesen, dass die Organisation in 15 Tagen gelöscht wird.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test9.png)

13. Der Entwicklungsleiter öffnet eines der Projekte und navigiert zu **Arbeitselemente** > **Mir zugewiesen**. Dies weist darauf hin, dass die Arbeitselementdaten zusammen mit der zugehörigen Identität migriert wurden.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test10.png)

14. Außerdem überprüft der Entwicklungsleiter andere Projekte und Code, um sicherzustellen, dass der Quellcode und der Verlauf migriert wurden.

    ![Probelauf](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Ausführen der Produktionsmigration

Wenn der Probelauf abgeschlossen ist, fahren die Contoso-Administratoren mit der Produktionsmigration fort. Contoso löscht den Probelauf, aktualisiert die Importeinstellungen und führt den Import erneut aus.

1. Im Azure DevOps Services-Portal löscht Contoso die Probelauforganisation.
2. Es aktualisiert die Datei „import.json“, um **ImportType** auf **ProductionRun** festzulegen.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full1.png)

3. Contoso startet die Migration so wie für den Probelauf: `TfsMigrator import /importFile:C:\TFSMigrator\import.json`.
4. Eine Meldung wird angezeigt, um die Migration zu bestätigen, und die darauf hinweist, dass Daten bis zu sieben Tage lang an einem sicheren Speicherort als Stagingbereich gespeichert werden können.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full2.png)

5. Bei der Azure AD-Anmeldung geben die Administratoren eine Contoso-Administratoranmeldung an.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full3.png)

6. Eine Meldung zeigt Informationen zum Import an.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full4.png)

7. Nach etwa 15 Minuten rufen sie die URL auf und sehen die folgenden Informationen:

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full5.png)

8. Nach Abschluss der Migration meldet sich ein Contoso-Entwicklungsleiter bei Azure DevOps Services an, um zu überprüfen, ob die Migration ordnungsgemäß durchgeführt wurde. Nach der Anmeldung kann er erkennen, dass Projekte migriert wurden.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full6.png)

9. Der Entwicklungsleiter öffnet eines der Projekte und navigiert zu **Arbeitselemente** > **Mir zugewiesen**. Dies weist darauf hin, dass die Arbeitselementdaten zusammen mit der zugehörigen Identität migriert wurden.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full7.png)

10. Der Entwicklungsleiter überprüft zur Bestätigung andere Arbeitselementdaten.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full8.png)

11. Außerdem überprüft der Entwicklungsleiter andere Projekte und Code, um sicherzustellen, dass der Quellcode und der Verlauf migriert wurden.

    ![Bereitstellung](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Migrieren der Quellcodeverwaltung von TFVC nach Git

Nach Abschluss der Migration möchte Contoso eine Migration von TFVC nach Git für die Quellcodeverwaltung durchführen. Contoso muss den Quellcode, der sich derzeit in der Azure DevOps Services-Organisation befindet, als Git-Repositorys in dieselbe Organisation importieren.

1. Im Azure DevOps Services-Portal öffnet Contoso eines der TFVC-Repositorys ( **$/PolicyConnect**) und überprüft dieses.

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. Contoso wählt die Dropdownliste **Quelle** > **Import** aus.

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. Unter **Quelltyp** wählt Contoso **TFVC** aus und gibt den Pfad zum Repository an. Das Unternehmen hat sich dazu entschlossen, nicht den Verlauf zu migrieren.

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > Aufgrund der Unterschiede bei der Speicherung von Versionskontrollinformationen in TFVC und Git wird Contoso davon abgeraten, den Verlauf zu migrieren. Dies ist auch der Ansatz, den Microsoft verfolgt hat, als Windows und andere Produkte von der zentralen Versionskontrolle zu Git migriert wurden.

4. Nach dem Import überprüfen die Administratoren den Code.

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. Es wiederholt den Prozess für das zweite Repository ( **$/SmartHotelContainer**).

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. Nach der Überprüfung der Quelle bestätigt der Entwicklungsleiter, dass die Migration zu Azure DevOps Services fertiggestellt ist. Azure DevOps Services wird jetzt zur Quelle für die gesamte Entwicklung in Teams, die an der Migration beteiligt sind.

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)

**Benötigen Sie weitere Hilfe?**

Weitere Informationen zum Importieren aus TFVC finden Sie [hier](https://docs.microsoft.com/azure/devops/repos/git/import-from-TFVC?view=vsts).

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach Abschluss der Migration muss Contoso die folgenden Schritte durchführen:

- Informationen zu zusätzlichen Importaktionen finden Sie im Artikel mit den Schritten [nach dem Import](https://docs.microsoft.com/azure/devops/articles/migration-post-import?view=vsts).
- Löschen Sie entweder die TFVC-Repositorys, oder versetzen Sie sie in den schreibgeschützten Modus. Die Codebasen dürfen nicht verwendet werden, für deren Verlauf kann jedoch auf diese verwiesen werden.

## <a name="post-migration-training"></a>Schulungen nach der Migration

Contoso muss Schulungen zu Azure DevOps Services und Git für die beteiligten Teammitglieder bereitstellen.
