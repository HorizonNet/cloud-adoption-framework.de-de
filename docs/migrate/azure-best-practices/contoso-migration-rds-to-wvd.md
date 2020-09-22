---
title: Verschieben lokaler Remotedesktopdienste zu Azure mit Windows Virtual Desktop
description: Erfahren Sie, wie Contoso seine lokalen RDS mithilfe von Windows Virtual Desktop zu Azure migriert hat.
author: benstegink
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6c4259f112c74d6f5fb7c24a0ca409e25ff68268
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602659"
---
<!-- docutune:casing Lakeside SysTrack -->
<!-- cSpell:ignore msiexec Logix Robocopy UPDs -->

# <a name="move-on-premises-remote-desktop-services-to-azure-windows-virtual-desktop-scenario"></a>Verschieben lokaler Remotedesktopdienste zu Azure mit Windows Virtual Desktop

Bei Windows Virtual Desktop handelt es sich um einen umfassenden in der Cloud ausgeführten Dienst zur Desktop- und Anwendungsvirtualisierung. Es ist die einzige virtuelle Desktopinfrastruktur (VDI), die eine vereinfachte Verwaltung, Windows 10 Enterprise-Multisessionoptimierungen für Microsoft 365 Apps for Enterprise und Unterstützung für RDS-Umgebungen (Remote Desktop Services, Remotedesktopdienste) bietet. In wenigen Minuten stellen Sie Windows-Desktops und -Anwendungen in Azure bereit, skalieren sie und profitieren von integrierten Funktionen für Sicherheit und Compliance.

| Migrationsoptionen | Ergebnis |
|--- | --- |
| [Azure Migrate](/azure/migrate/migrate-services-overview) | Bewerten und Migrieren lokaler RDS-Umgebungen. <br><br> Ausführen von Workloads mithilfe von Azure Windows Virtual Desktop <br><br> Verwalten von Windows Virtual Desktop mit der [Windows Virtual Desktop-Verwaltungsoberfläche](https://github.com/Azure/RDS-Templates/tree/master/wvd-templates/wvd-management-ux). |

> [!NOTE]
> Dieser Artikel konzentriert sich auf die Verwendung von Windows Virtual Desktop in Azure zum Verschieben einer lokalen RDS-Umgebung zu Azure.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Team von Contoso definiert in enger Zusammenarbeit mit Geschäftspartnern die geschäftlichen Faktoren, die für eine VDI-Migration zu Azure sprechen. Dies umfasst beispielsweise Folgendes:

- **Ende der Lebensdauer der aktuellen Umgebung:** Die Kapazität eines Rechenzentrums ist erschöpft, wenn das Ende seiner Leasedauer erreicht ist oder es stillgelegt wird. Die Migration zur Cloud bietet praktisch unbegrenzte Kapazität. Die aktuelle Software kann auch das Ende ihrer Lebensdauer erreichen, sodass es erforderlich ist, die Software zu aktualisieren, die die aktuelle VDI-Lösung von Contoso ausführt.
- **Multisession-Windows 10-VDI:** Stellt den Contoso-Benutzern den einzigen in der Cloud virtualisierten Multisession-Windows 10-Desktop zur Verfügung, der hochgradig skalierbar, auf dem neuesten Stand und auf jedem Gerät verfügbar ist.
- **Optimieren für Microsoft 365 Apps for Enterprise:** Sorgt für eine optimale Benutzerfreundlichkeit mit Microsoft 365 Apps for Enterprise, wobei Szenarios mit virtuellen Multisession-Desktops Contoso-Benutzern die produktivste virtualisierte Benutzererfahrung bieten.
- **Bereitstellen und Skalieren in Minuten:** Mit einheitlicher Verwaltung im Azure-Portal können in wenigen Minuten moderne und ältere Desktopanwendungen schnell virtualisiert und in der Cloud bereitgestellt werden.
- **Sicher und produktiv in Azure und Microsoft 365:** Eine komplette, intelligente Lösung wird bereitgestellt, die Kreativität und Zusammenarbeit für alle verbessert. Wechseln Sie zu Microsoft 365, und holen Sie sich Office 365, Windows 10 und Enterprise Mobility + Security.

## <a name="rds-on-premises-to-windows-virtual-desktop-in-the-cloud-goals"></a>Ziele des Wechsels von lokalen RDS zu Windows Virtual Desktop in der Cloud

Contoso hat sich unter Berücksichtigung der geschäftlichen Faktoren die folgenden Ziele für die Migration gesetzt:

- Modernisieren der virtuellen Desktopumgebung für die Cloud.
- Profitieren von vorhandenen Microsoft 365-Lizenzen.
- Verbessern der Sicherheit von Unternehmensdaten bei Remotearbeit
- Optimieren der neuen Umgebung für Kosten und Wachstum.

Diese Ziele bestätigen, dass Windows Virtual Desktop die beste Migrationsmethode für Contoso ist, und stützen die Entscheidung für die Verwendung des Diensts.

## <a name="benefits-of-running-windows-virtual-desktop-in-azure"></a>Vorteile der Ausführung von Windows Virtual Desktop in Azure

Mithilfe von Windows Virtual Desktop in Azure kann Contoso seine VDI-Lösung reibungslos ausführen, verwalten und schnell und einfach skalieren. Das Unternehmen kann auch eine optimierte Windows 10-Multisessionumgebung für die Benutzer bereitstellen.

Contoso nutzt seine vorhandenen Microsoft 365-Lizenzen und profitiert dabei von der Skalierung, Leistung, Sicherheit und Innovation von Azure.

Folgende weitere Vorteile sind möglich:

- Zugriff auf Windows Virtual Desktop von einem beliebigem Ort
- Optimierte Microsoft 365 Apps for Enterprise-Umgebung
- Windows Virtual Desktop für Dev/Test-Umgebungen

## <a name="solutions-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess.

### <a name="current-architecture"></a>Aktuelle Architektur

RDS wird in einem lokalen Rechenzentrum bereitgestellt. Microsoft 365 ist lizenziert und wird von der Organisation verwendet.

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Azure Active Directory oder Azure Active Directory Domain Services synchronisieren.
- Windows Virtual Desktop in Azure bereitstellen.
- Lokale RDS-Server zu Azure migrieren.
- Benutzerprofil-Datenträger (User Profile Disks, UPD) in FSLogix-Profilcontainer konvertieren.

  ![Diagramm mit der vorgeschlagenen Architektur](./media/contoso-migration-rds-to-wvd/proposed-architecture.png)
  _Abbildung 1: Vorgeschlagene Architektur._

## <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Windows 10 Enterprise-Multisessionumgebung. <br><br> Cloudbasiert, ermöglicht den Zugriff von jedem beliebigen Standort aus. <br><br> Profitieren Sie von anderen Azure-Diensten wie Azure Files in der Windows Virtual Desktop-Umgebung. <br><br> Optimiert für den modernen Microsoft-Desktop. |
| **Nachteile** | Zur vollständigen Optimierung für Azure muss Contoso für Mehrbenutzersitzungen optimierte Windows 10-Images neu erstellen. <br><br> Windows Virtual Desktop unterstützt keine Benutzerprofil-Datenträger, sodass UPDs in FSLogix-Profilcontainern migriert werden müssen. |

## <a name="migration-process"></a>Migrationsprozess

Mit dem Lakeside-Bewertungstool und Azure Migrate verschiebt Contoso VMs in Azure zu Windows Virtual Desktop. Dafür muss Contoso folgende Schritte ausführen:

- Das Bewertungstool wird für die lokale RDS-Infrastruktur ausgeführt, um die Skalierung der Bereitstellung von Windows Virtual Desktop in Azure einzurichten.
- Die Migration zu Windows Virtual Desktop erfolgt entweder über Multisession-Windows 10 Enterprise oder persistente virtuelle Computer.
- Multisession-Windows Virtual Desktop wird durch Hoch- und Herunterskalieren optimiert, um die Kosten zu verwalten.
- Nach Bedarf werden Anwendungen virtualisiert und Benutzer zugewiesen, um die Windows Virtual Desktop-Umgebung weiterhin zu sichern und zu verwalten.

  ![Diagramm zum Migrationsprozess.](./media/contoso-migration-rds-to-wvd/migration-process-01.png)
  _Abbildung 2: Der Migrationsvorgang._

## <a name="scenario-steps"></a>Szenarioschritte

1. Aktuelle RDS-Umgebung bewerten.
2. Erstellen des VDI und neuer Images in Azure und Migrieren und Beibehalten virtueller Computer in Azure
3. Konvertieren von UPDs in FSLogix-Profilcontainer
4. Persistente VMs in Azure replizieren.

## <a name="step-1-assess-the-current-on-premises-environment"></a>Schritt 1: Bewerten der aktuellen lokalen Umgebung

Contoso stellt den Windows Virtual Desktop-Dienst in der Azure-Region `East US 2` bereit. Windows Virtual Desktop ermöglicht Contoso die Bereitstellung von virtuellen Computern und Hostpools und das Erstellen von Anwendungsgruppen. Außerdem konfiguriert Windows Virtual Desktop eine Verfügbarkeitsgruppe für alle Server in der Windows Virtual Desktop-Lösung. Mit Windows Virtual Desktop kann Contoso eine hochverfügbare VDI-Umgebung erstellen und bei Bedarf schnell hoch- und herunterskalieren.

> [!NOTE]
> Contoso hat während der Bewertung zwei Szenarien überprüft: Multisession-Instanzen (freigegebene Instanzen) von RDS und persistente (oder benutzerdedizierte) virtuelle Computer.

1. Stellen Sie sicher, dass Domänendienste, entweder Active Directory oder Azure Active Directory Domain Services, mit Azure Active Directory (Azure AD) synchronisiert werden. Stellen Sie sicher, dass über das Azure-Abonnement und das virtuelle Netzwerk auf den Domänendienst zugegriffen werden kann, um mit dem Ort verbunden zu sein, an dem Windows Virtual Desktop bereitgestellt wird.

    > [!NOTE]
    > Erfahren Sie mehr über [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-express) für die Synchronisierung lokaler Active Directory-Instanzen mit Azure AD.

    <!-- -->

    > [!NOTE]
    > Erfahren Sie mehr über die Bereitstellung von [Azure Active Directory Domain Services](/azure/active-directory-domain-services/tutorial-create-instance) und die Synchronisierung von Azure AD mit ihnen.

1. Erstellen Sie ein neues Azure Migrate-Projekt.

   ![Screenshot: Erstellen eines neuen Azure Migrate-Projekts](./media/contoso-migration-rds-to-wvd/new-azure-migrate.png)
   _Abbildung 3: Erstellen eines neuen Azure Migrate-Projekts._

1. Wählen Sie die Option zum Bewerten und Migrieren von Servern und anschließend **VDI** aus, und fügen Sie ein Tool hinzu.

   ![Screenshot: Azure Migrate-Ziele von VDI](./media/contoso-migration-rds-to-wvd/azure-migrate-goals-vdi.png)

   _Abbildung 4: Azure Migrate-Ziele._

1. Legen Sie Abonnement, Ressourcengruppe, Projektname und Geografie für die Migrationsauftragsdaten fest.

   ![Screenshot: Hinzufügen von Auftragsdaten zum Azure Migrate-Projekt](./media/contoso-migration-rds-to-wvd/add-a-tool.png)
   _Abbildung 5: Hinzufügen von Auftragsdaten zur Migration._

    > [!IMPORTANT]
    > Dies ist nicht der Speicherort, an dem die neue Windows Virtual Desktop-Umgebung bereitgestellt wird. Nur die Daten, die sich auf das Azure Migrate-Projekt beziehen, werden hier gespeichert.

1. Wählen Sie **Lakeside: SysTrack** als Bewertungstool.

1. Wählen Sie **Azure Migrate: Servermigration** als Migrationstool.

1. Fügen Sie dem Migrationsprojekt die Tools hinzu.

   ![Screenshot: Hinzufügen von Tools zum Projekt](./media/contoso-migration-rds-to-wvd/add-tools.png)
   _Abbildung 6: Hinzufügen von Tools zur Migration._

1. Starten Sie die Bewertung der aktuellen Umgebung, indem Sie im Lakeside-Tool **Bei Azure Migrate registrieren** auswählen.

   ![Screenshot mit der Lakeside-Registrierung bei Azure Migrate](./media/contoso-migration-rds-to-wvd/lakeside-register-with-azure-migrate.png)

   _Abbildung 7: Bewerten der aktuellen Umgebung._

1. Contoso stellt eine Verbindung zwischen Azure Migrate und Lakeside her und akzeptiert alle angeforderten Berechtigungen.

   ![Screenshot mit der Anmeldung zum Herstellen einer Verbindung zwischen Azure und Lakeside](./media/contoso-migration-rds-to-wvd/lakeside-login.png)
   _Abbildung 8: Herstellen einer Verbindung zwischen Azure Migrate und Lakeside._

1. Contoso fährt mit dem Lakeside-Tool fort, um einen neuen Mandanten zu erstellen und mit der Bewertung seiner aktuellen lokalen RDS-Umgebung zu beginnen. Vom Dashboard aus kann Contoso auf das Bereitstellungshandbuch zugreifen, den Bewertungsclient herunterladen, um ihn in der aktuellen Umgebung bereitzustellen, und die von diesen Agents gesammelten Daten überprüfen.

   ![Screenshot mit dem Lakeside-Dashboard](./media/contoso-migration-rds-to-wvd/lakeside-new-tenant-dashboard.png)
   _Abbildung 9: Das Lakeside-Dashboard._
1. Nachdem eine entsprechende Menge an Daten aufgezeichnet wurde, überprüft Contoso die Bewertungsdaten, um den besten Migrationspfad zu bestimmen. Diese Bewertungsdaten umfassen die Bewertungsrohdaten von den Desktopdaten und die nach verschiedenen Benutzerpersonas aufgeschlüsselten Daten. Diese Informationen umfassen Folgendes:

- Anzahl der Benutzer in jeder Persona
- Von den Benutzern verwendete Anwendungen
- Ressourcenverbrauch durch Benutzer
- Durchschnittliche Ressourcenverwendung nach Benutzerpersona
- VDI-Serverleistungsdaten
- Berichte über gleichzeitige Benutzer
- Meistverwendete Softwarepakete

    ![Screenshot mit Lakeside-Dashboardberichten](./media/contoso-migration-rds-to-wvd/lakeside-dashboard-reports.png)
    _Abbildung 10: Lakeside-Dashboardberichte._

Diese Daten werden von Contoso analysiert, um die kostengünstigste Nutzung sowohl gepoolter als auch persönlicher Windows Virtual Desktop-Ressourcen zu ermitteln.

> [!NOTE]
> Außerdem muss Contoso seine Anwendungsserver zu Azure migrieren, um das Unternehmen näher an die Windows Virtual Desktop-Umgebung zu bringen und die Netzwerklatenz für die Benutzer zu verringern.

## <a name="step-2-create-the-windows-virtual-desktop-environment-for-pooled-desktops"></a>Schritt 2: Erstellen der Windows Virtual Desktop-Umgebung für gepoolte Desktops

Mit dem Azure-Portal erstellt Contoso eine Windows Virtual Desktop-Umgebung für gepoolte Ressourcen. Später werden die Migrationsschritte durchgeführt, um derselben Umgebung persönliche Desktops anzufügen.

1. Contoso wählt das richtige Abonnement aus und erstellt einen neuen Windows Virtual Desktop-Hostpool.

   ![Screenshot: Bereitstellung eines Windows Virtual Desktop-Hostpools](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool.png)
  _Abbildung 11: Ein neuer Windows Virtual Desktop-Hostpool._

1. Geben Sie Abonnement, Ressourcengruppe und Region an. Wählen Sie anschließend den Namen für den Hostpool, den Desktoptyp und Standarddesktopbenutzer aus. Der Desktoptyp ist auf **Pooled** (Gepoolt) festgelegt, da Contoso für einige seiner Benutzer mit einer neuen freigegebenen Umgebung beginnt. Für Standarddesktopbenutzer ist kein Eintrag erforderlich. Fahren Sie mit der Konfiguration der virtuellen Computer fort.

   ![Screenshot: Voraussetzungen zum Konfigurieren virtueller Computer](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool-basics-alt.png)
   _Abbildung 12: Voraussetzungen zum Konfigurieren virtueller Computer._

   - Contoso konfiguriert den virtuellen Computer und wählt eine benutzerdefinierte Größe aus, indem es **Größe ändern** auswählt oder die Standardeinstellung verwendet.
   - Windows Virtual Desktop wird als VM-Namenspräfix für diese in einem Pool zusammengefassten Desktops ausgewählt.
   - Da Contoso die gepoolten Server erstellt, um die neue Windows 10-Multisessionfunktion für die VM-Einstellungen zu verwenden, behalten Sie die Einstellung **Katalog** für die Bildquelle bei. Mit dieser Option kann Contoso das Windows 10 Enterprise-Multisessionimage für die virtuellen Computer auswählen.
   - Basierend auf den Personas der Benutzer aus der Lakeside-Bewertung legt Contoso die Gesamtanzahl der Benutzer auf **150** fest.
   - Andere Einstellungen betreffen den Datenträgertyp, ein AD-Domänenbeitritt-UPN-Feld, ein Administratorkennwort, einen optionalen OE-Pfad, dem Computer hinzugefügt werden, das virtuelle Netzwerk und ein Subnetz zum Hinzufügen von Servern.

   ![Screenshot: Konfigurieren virtueller Computer](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool-configure-virtual-machines-alt.png)
   _Abbildung 13: Konfigurieren virtueller Computer._

    > [!NOTE]
    > In diesem Schritt kann Contoso kein neues virtuelles Netzwerk erstellt werden. Vor diesem Schritt sollte Contoso bereits ein virtuelles Netzwerk erstellt haben, das Zugriff auf Active Directory hat.
    <!-- -->
    > [!NOTE]
    > In diesem Schritt kann Contoso kein Benutzerkonto verwenden, für das eine mehrstufige Authentifizierung erforderlich ist. Wenn Contoso die mehrstufige Authentifizierung für seine Benutzer verwenden möchte, muss ein Dienstprinzipal erstellt werden.

1. Contoso führt eine weitere Überprüfung der Windows Virtual Desktop-Einstellungen durch und erstellt die neue Umgebung gepoolter Windows Virtual Desktop-VMs.

   ![Screenshot: Überprüfen und Erstellen virtueller Computer](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool-review-create.png)
   _Abbildung 14: Überprüfen und Erstellen virtueller Computer._

## <a name="step-3-convert-the-upds-to-fslogix-profile-containers"></a>Schritt 3: Konvertieren der UPDs in FSLogix-Profilcontainer

Da Windows Virtual Desktop keine Benutzerprofil-Datenträger (User Profile Disks, UPDs) unterstützt, muss Contoso alle UPDs über das [PowerShell-Modul FSLogixMigration](https://aka.ms/FSLogixMigrationPreviewModule) in FSLogix konvertieren.

<!-- docsTest:casing FSLogixMigration -->

Nachdem Contoso das FSLogixMigration-Modul importiert hat, werden die folgenden PowerShell-Cmdlets ausgeführt, um von UPDs zu FSLogix zu migrieren.

> [!IMPORTANT]
> Die PowerShell-Module für Hyper-V, Active Directory und Pester sind Voraussetzungen für die Ausführung der Cmdlets zum Konvertieren von UPDs in FSLogix.

Eine UDP-Konvertierung:

```powershell
Convert-RoamingProfile -ParentPath "C:\Users\" -Target "\\Server\FSLogixProfiles$" -MaxVHDSize 20 -VHDLogicalSectorSize 512
```

Eine Roamingprofilkonvertierung:

```powershell
Convert-RoamingProfile -ProfilePath "C:\Users\User1" -Target "\\Server\FSLogixProfiles$" -MaxVHDSize 20 -VHDLogicalSectorSize 512 -VHD -IncludeRobocopyDetails -LogPath C:\temp\Log.txt
```

An diesem Punkt hat die Migration die Verwendung in einem Pool zusammengefasster Ressourcen mit Multisession-Windows 10 Enterprise ermöglicht. Contoso kann mit der Bereitstellung der erforderlichen Anwendungen für seine Benutzer beginnen, die Multisession-Windows 10 Enterprise verwenden.

Allerdings muss Contoso die persistenten virtuellen Computer zu Azure migrieren.

## <a name="step-4-replicate-and-persist-vms-to-windows-virtual-desktop"></a>Schritt 4: Replizieren persistenter virtueller Computer zu Windows Virtual Desktop

Der nächste Schritt des Migrationsprozesses für Contoso besteht darin, die persistenten virtuellen Computer zu Windows Virtual Desktop zu migrieren. Dazu navigiert Contoso zurück zum Auftrag „Azure Migrate: Servermigration“, den es zu Beginn des Vorgangs erstellt hat.

1. Contoso beginnt mit der Auswahl von **Ermitteln** in den „Azure Migrate: Servermigration“-Tools.

   ![Screenshot mit dem der Option „Azure Migrate: Servermigration – Ermitteln“](./media/contoso-migration-rds-to-wvd/wvd-persistent-discover.png)
   _Abbildung 15: Ermitteln einer Servermigration._

1. Als Nächstes konvertiert Contoso eine Appliance in seiner Umgebung, die die Replikation der Computer in Windows Virtual Desktop verwaltet. Die Zielregion muss dabei auf `East US 2` festgelegt sein, wo die Windows Virtual Desktop-Umgebung erstellt wurde.

   ![Screenshot: Erstellen einer Appliance zum Verwalten der Replikation](./media/contoso-migration-rds-to-wvd/wvd-persistent-appliance.png)
   _Abbildung 16: Konvertieren einer Appliance._

1. Der Replikationsanbieter wird heruntergeladen, installiert und für das Azure Migrate-Projekt registriert, um die Replikation in Azure zu starten.

   ![Screenshot: Herunterladen und Konfigurieren der Replikation](./media/contoso-migration-rds-to-wvd/wvd-persistent-replication.png)
   _Abbildung 17: Voraussetzungen für die Replikation in Azure._

1. Die Replikation der Hosts in Azure Blob Storage hat nun begonnen. Die Replikation kann weiter fortgesetzt werden, bis Contoso bereit ist, die virtuellen Computer zu testen und in die Produktion zu migrieren.
   - Sobald Computer in Azure ausgeführt werden, stellt Contoso sicher, dass der [Windows Virtual Desktop-VM-Agent](https://aka.ms/WVDVMAgent) auf jedem Computer installiert wird.
   - Im Rahmen der Installation wird das Registrierungstoken für die Windows Virtual Desktop-Umgebung eingegeben, um den Server der richtigen Umgebung zuzuordnen.

1. Das Registrierungstoken kann mithilfe der folgenden Befehle abgerufen werden:

    ```powershell
    Export-RDSRegistrationInfo -TenantName "Contoso" -HostPoolName "ContosoWVD" | Select-Object -ExpandProperty Token > .\registration-token.txt
    ```

    > [!NOTE]
    > Außerdem kann Contoso diesen Prozess durch die Verwendung von `msiexec`-Befehlen und Übergabe des Registrierungstokens als Variable automatisieren.

1. Im letzten Schritt vor der abschließenden Migration verwendet Contoso das Element **Benutzer** in den Azure Windows Virtual Desktop-Einstellungen aus, um die Server ihren jeweiligen Benutzern und Gruppen zuzuordnen.

   ![Screenshot: Zuweisen von Windows Virtual Desktop-Ressourcen zu Benutzern und Gruppen](./media/contoso-migration-rds-to-wvd/wvd-persistent-user-mapping.png)
    _Abbildung 18: Der letzte Schritt vor der abschließenden Migration._

Sobald den Benutzern Hostpools zugewiesen werden, schließt Contoso die Migration dieser Computer ab und fährt fort, die restlichen lokalen VDI-Hosts nach und nach zu Azure zu migrieren.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Jetzt, wo die virtuellen Desktops und Anwendungsserver in Azure ausgeführt werden, muss Contoso die Bereitstellung vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs auf eventuell vorhandene Sicherheitsprobleme. Zur Steuerung des Zugriffs überprüft das Team die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer. Mithilfe von Netzwerksicherheitsgruppen wird sichergestellt, dass nur für die Anwendung zulässiger Datenverkehr diese erreichen kann. Das Team zieht darüber hinaus in Betracht, die Daten über Azure Disk Encryption und Azure Key Vault auf dem Datenträger zu sichern.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Für die Business Continuity & Disaster Recovery (BCDR) sichert Contoso die Daten auf den virtuellen Computern mit Azure Backup, um sie zu schützen. Weitere Informationen finden Sie unter [Ein Überblick über die Sicherung von Azure-VMs](/azure/backup/backup-azure-vms-introduction).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- [Microsoft 365-Lizenzen](https://azure.microsoft.com/pricing/details/virtual-desktop/) werden für die Desktop-Bereitstellungen verwendet.
- Contoso aktiviert [Azure Cost Management und das Azure-Abrechnungsportal](/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.
- Contoso verfügt über eine Lizenzierung für die virtuellen Computer und nutzt den Azure-Hybridvorteil für Anwendungsserver. Contoso wird die vorhandenen virtuellen Azure-Computer konvertieren, um von diesen Preisen zu profitieren.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat Contoso seine RDS-Bereitstellung zu Windows Virtual Desktop (gehostet in Azure) verschoben.
