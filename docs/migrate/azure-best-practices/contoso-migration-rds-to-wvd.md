---
title: Verschieben lokaler Remotedesktopdienste zu Azure mit Windows Virtual Desktop
description: Erfahren Sie, wie Contoso seine lokalen RDS (Remote Desktop Services, Remotedesktopdienste) mithilfe von Windows Virtual Desktop zu Azure migrierte.
author: benstegink
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 70c86f5bf1f15cb81d7dc8fefc1195bd21366798
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199104"
---
<!-- cSpell:ignore benstegink msiexec Logix Lakeside SysTrack Robocopy UPD UPDs -->

# <a name="move-on-premises-remote-desktop-services-to-azure-windows-virtual-desktop-scenario"></a>Verschieben lokaler Remotedesktopdienste zu Azure mit Windows Virtual Desktop

Bei Windows Virtual Desktop handelt es sich um einen umfassenden in der Cloud ausgeführten Dienst zur Desktop- und Anwendungsvirtualisierung. Es ist die einzige virtuelle Desktopinfrastruktur (VDI), die eine vereinfachte Verwaltung, Multisession-Windows 10 Enterprise, Optimierungen für Microsoft 365 Apps for Enterprise und Unterstützung für Remotedesktopdienste-Umgebungen bietet. In wenigen Minuten stellen Sie Windows-Desktops und -Anwendungen in Azure bereit, skalieren sie und profitieren von integrierten Funktionen für Sicherheit und Compliance.

| Migrationsoptionen | Ergebnis |
|--- | --- |
| [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | Bewerten und Migrieren lokaler RDS-Umgebungen. <br><br> Ausführen von Workloads mithilfe von Azure Windows Virtual Desktop. <br><br> Verwalten von Windows Virtual Desktop mit der [Windows Virtual Desktop-Verwaltungsoberfläche](https://github.com/Azure/RDS-Templates/tree/master/wvd-templates/wvd-management-ux). |

Bei Windows Virtual Desktop handelt es sich um einen umfassenden in der Cloud ausgeführten Dienst zur Desktop- und Anwendungsvirtualisierung. Es ist die einzige VDI, die eine vereinfachte Verwaltung, Multisession-Windows 10 Enterprise, Optimierungen für Microsoft 365 Apps for Enterprise und Unterstützung für RDS-Umgebungen bietet. In wenigen Minuten stellen Sie Windows-Desktops und -Anwendungen in Azure bereit, skalieren sie und profitieren von integrierten Funktionen für Sicherheit und Compliance.

> [!NOTE]
> Dieser Artikel konzentriert sich auf die Verwendung des Windows Virtual Desktop-Azure-Diensts zum Verschieben einer lokalen RDS-Umgebung in Azure.

## <a name="business-drivers"></a>Business-Treiber

Das IT-Team von Contoso definiert in enger Zusammenarbeit mit Geschäftspartnern die geschäftlichen Faktoren, die für eine VDI-Migration zu Azure sprechen. Dazu können folgende Faktoren zählen:

- **Ende der Lebensdauer der aktuellen Umgebung:** Die Kapazität eines Rechenzentrums ist erschöpft, wenn das Ende seiner Leasedauer erreicht ist oder es stillgelegt wird. Die Migration zur Cloud bietet praktisch unbegrenzte Kapazität. Die aktuelle Software kann auch das Ende ihrer Lebensdauer erreichen, sodass es erforderlich ist, die Software zu aktualisieren, die die aktuelle VDI-Lösung von Contoso ausführt.
- **Multisession-Windows 10-VDI:** Stellt den Contoso-Benutzern den einzigen in der Cloud virtualisierten Multisession-Windows 10-Desktop zur Verfügung, der hochgradig skalierbar, auf dem neuesten Stand und auf jedem Gerät verfügbar ist.
- **Optimieren für Microsoft 365 Apps for Enterprise:** Sorgt für eine optimale Benutzerfreundlichkeit mit Microsoft 365 Apps for Enterprise, wobei Szenarios mit virtuellen Multisession-Desktops Contoso-Benutzern die produktivste virtualisierte Benutzererfahrung bieten.
- **Bereitstellen und Skalieren in Minuten:** Mit einheitlicher Verwaltung im Azure-Portal können in wenigen Minuten moderne und ältere Desktopanwendungen schnell virtualisiert und in der Cloud bereitgestellt werden.
- **Sicher und produktiv in Azure und Microsoft 365:** Eine komplette, intelligente Lösung wird bereitgestellt, die Kreativität und Zusammenarbeit für alle verbessert. Wechseln Sie zu Microsoft 365, und holen Sie sich Office 365, Windows 10 und Enterprise Mobility + Security.

## <a name="rds-on-premises-to-windows-virtual-desktop-in-the-cloud-goals"></a>Ziele des Wechsels von lokalen RDS zu Windows Virtual Desktop in der Cloud

Contoso hat sich unter Berücksichtigung der geschäftlichen Faktoren die folgenden Ziele für die Migration gesetzt:

- Modernisieren der virtuellen Desktopumgebung für die Cloud.
- Profitieren von vorhandenen Microsoft 365-Lizenzen.
- Verbessern der Sicherheit von Unternehmensdaten bei Remotearbeit.
- Optimieren der neuen Umgebung für Kosten und Wachstum.

Diese Ziele bestätigen, dass Windows Virtual Desktop die beste Migrationsmethode für Contoso ist, und stützen die Entscheidung für die Verwendung des Diensts.

## <a name="benefits-of-running-windows-virtual-desktop-in-azure"></a>Vorteile der Ausführung von Windows Virtual Desktop in Azure

Mit Windows Virtual Desktop in Azure kann Contoso nun seine VDI-Lösung schnell und einfach nahtlos ausführen, verwalten und skalieren sowie eine optimierte Windows 10-Multisessionumgebung für seine Benutzer bereitstellen.

Bei Nutzung der Skalierung, Leistung, Sicherheit und Innovation von Azure kann Contoso die vorhandenen Microsoft 365-Lizenzen einsetzen.

Folgende weitere Vorteile sind möglich:

- Zugriff auf Windows Virtual Desktop von beliebigem Ort
- Optimierte „Microsoft 365 Apps for Enterprise“-Umgebung
- Windows Virtual Desktop für Dev/Test-Umgebungen

## <a name="solutions-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess.

### <a name="current-architecture"></a>Aktuelle Architektur

RDS wird in einem lokalen Rechenzentrum bereitgestellt, und Microsoft 365 ist lizenziert und wird von der Organisation verwendet.

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Azure Active Directory oder Azure Active Directory Domain Services synchronisieren. Azure AD DS mit Azure AD.
- Windows Virtual Desktop in Azure bereitstellen.
- Lokale RDS-Server zu Azure migrieren.
- Benutzerprofil-Datenträger (User Profile Disks, UPD) in FSLogix-Profilcontainer konvertieren.

  ![Vorgeschlagene Architektur](./media/contoso-migration-rds-to-wvd/proposed-architecture.png)
  _Abbildung 1: Vorgeschlagene Architektur._

## <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Windows 10 Enterprise-Multisessionumgebung. <br><br> Cloudbasiert, ermöglicht den Zugriff von jedem beliebigen Standort aus. <br><br> Profitieren Sie von anderen Azure-Diensten wie Azure Files in der Windows Virtual Desktop-Umgebung. <br><br> Optimiert für den modernen Microsoft-Desktop. |
| **Nachteile** | Zur vollständigen Optimierung für Azure muss Contoso für Mehrbenutzersitzungen optimierte Windows 10-Images neu erstellen. <br><br> Windows Virtual Desktop unterstützt keine Benutzerprofil-Datenträger, sodass diese in FSLogix-Profilcontainern migriert werden müssen. |

## <a name="migration-process"></a>Migrationsprozess

Mit dem Lakeside-Bewertungstool und Azure Migrate verschiebt Contoso VMs in Azure zu Windows Virtual Desktop.

- Als ersten Schritt führt Contoso das Bewertungstool für seine lokale RDS-Infrastruktur aus, um die Skalierung der Bereitstellung von Windows Virtual Desktop in Azure einzurichten.
- Die Migration zu Windows Virtual Desktop erfolgt entweder über Multisession-Windows 10 Enterprise oder persistente virtuelle Computer.
- Multisession-Windows Virtual Desktop wird durch Hoch- und Herunterskalieren optimiert, um die Kosten zu verwalten.
- Nach Bedarf werden Anwendungen virtualisiert und Benutzer zugewiesen, um die Windows Virtual Desktop-Umgebung weiterhin zu sichern und zu verwalten.

  ![Migrationsvorgang](./media/contoso-migration-rds-to-wvd/migration-process-01.png)
  _Abbildung 2: Der Migrationsvorgang._

## <a name="scenarios-steps"></a>Schritte für das Szenario

1. Aktuelle RDS-Umgebung bewerten.
2. VDI, neue Images und persistente VMS in Azure erstellen und migrieren.
3. Benutzerprofil-Datenträger (User Profile Disks, UPD) in FSLogix-Profilcontainer konvertieren.
4. Persistente VMs in Azure replizieren.

## <a name="step-1-assess-the-current-on-premises-environment"></a>Schritt 1: Bewerten der aktuellen lokalen Umgebung

Contoso stellt den Windows Virtual Desktop-Dienst in der Azure-Region `East US 2` bereit. Der Windows Virtual Desktop-Dienst ermöglicht die Bereitstellung von VMs, Hostpools und das Erstellen von Anwendungsgruppen. Außerdem konfiguriert der Windows Virtual Desktop-Dienst eine Verfügbarkeitsgruppe für alle Server in der Windows Virtual Desktop-Lösung. Mit dem Windows Virtual Desktop-Dienst kann Contoso sowohl eine hoch verfügbare VDI-Umgebung erstellen als auch schnell nach Bedarf hoch- und herunterskalieren.

> [!NOTE]
> Zwei Szenarien überprüft Contoso während der Bewertung: Multisession-Instanzen (freigegebene Instanzen) von RDS und persistente (oder benutzerdedizierte) virtuelle Computer.

- Zunächst muss sichergestellt werden, dass Domänendienste (Active Directory oder Azure AD DS) mit Azure AD synchronisiert werden, und dass über das Azure-Abonnement und das virtuelle Netzwerk auf den Domänendienst zugegriffen werden kann, um mit dem Ort verbunden zu sein, an dem Windows Virtual Desktop bereitgestellt wird.

> [!NOTE]
> Erfahren Sie mehr über [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express) für die Synchronisierung lokaler Active Directory-Instanzen mit Azure AD.

<!-- -->

> [!NOTE]
> Erfahren Sie mehr über die Bereitstellung von [Azure Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/tutorial-create-instance) und die Synchronisierung von Azure AD mit ihnen.

- Erstellen Sie ein neues Azure Migrate-Projekt.

  ![Ein neues Azure Migrate-Projekt](./media/contoso-migration-rds-to-wvd/new-azure-migrate.png)
  _Abbildung 3: Erstellen eines neuen Azure Migrate-Projekts._

- Wählen Sie die Option zum Bewerten und Migrieren von Servern, wählen Sie `VDI` aus, und fügen Sie ein Tool hinzu.

  ![Azure Migrate-Ziele der VDI](./media/contoso-migration-rds-to-wvd/azure-migrate-goals-vdi.png)
  _Abbildung 4: Azure Migrate-Ziele._

- Legen Sie Abonnement, Ressourcengruppe, Projektname und Geografie für die Migrationsauftragsdaten fest.

  ![Hinzufügen eines Tools zum Azure Migrate-Projekt](./media/contoso-migration-rds-to-wvd/add-a-tool.png)
  _Abbildung 5: Hinzufügen von Auftragsdaten zur Migration._

> [!IMPORTANT]
> An diesem Ort wird die neue Windows Virtual Desktop-Umgebung nicht bereitgestellt, da nur die Daten, die sich auf das Azure Migrate-Projekt beziehen, hier gespeichert werden.

- Wählen Sie **Lakeside: SysTrack** als Bewertungstool.

- Wählen Sie **Azure Migrate: Servermigration** als Migrationstool.

- Fügen Sie dem Migrationsprojekt die Tools hinzu.

  ![Überprüfen und Hinzufügen der Tools](./media/contoso-migration-rds-to-wvd/add-tools.png)
  _Abbildung 6: Hinzufügen von Tools zur Migration._

- Starten Sie die Bewertung der aktuellen Umgebung, indem Sie klicken, um sich mit Azure Migrate im Lakeside-Tool zu registrieren.

  ![Lakeside-Registrierung mit Azure Migrate](./media/contoso-migration-rds-to-wvd/lakeside-register-with-azure-migrate.png)
  _Abbildung 7: Bewerten der aktuellen Umgebung._

- Contoso stellt eine Verbindung zwischen Azure Migrate und Lakeside her und akzeptiert alle angeforderten Berechtigungen.

  ![Anmelden zum Herstellen einer Verbindung zwischen Azure Migrate und Lakeside](./media/contoso-migration-rds-to-wvd/lakeside-login.png)
  _Abbildung 8: Herstellen einer Verbindung zwischen Azure Migrate und Lakeside._

- Contoso fährt mit dem Lakeside-Tool fort, um einen neuen Mandanten zu erstellen und mit der Bewertung seiner aktuellen lokalen RDS-Umgebung zu beginnen. Vom Dashboard aus kann Contoso auf das Bereitstellungshandbuch zugreifen, den Bewertungsclient herunterladen, um ihn in der aktuellen Umgebung bereitzustellen, und die von diesen Agents gesammelten Daten überprüfen.

  ![Lakeside-Dashboard](./media/contoso-migration-rds-to-wvd/lakeside-new-tenant-dashboard.png)
  _Abbildung 9: Das Lakeside-Dashboard._

- Nachdem Contoso eine angemessene Menge an Daten aufgezeichnet hat, werden die Bewertungsdaten überprüft, um den besten Migrationspfad zu ermitteln. Mit diesen Bewertungsdaten verfügt Contoso über die Bewertungsrohdaten aus den Desktops und die nach verschiedenen Benutzerrollen aufgeschlüsselten Daten. Dies umfasst Informationen wie:
  - Anzahl der Benutzer in jeder Rolle
  - Anwendungen, die von einzelnen Benutzern verwendet werden
  - Ressourcenverbrauch je Benutzer
  - Durchschnittliche Ressourcenauslastung nach Benutzerrolle
  - VDI-Serverleistungsddaten
  - Berichte über gleichzeitige Benutzer
  - Meistverwendete Softwarepakete

    ![Lakeside-Dashboardberichte](./media/contoso-migration-rds-to-wvd/lakeside-dashboard-reports.png)
    _Abbildung 10: Lakeside-Dashboardberichte._

Diese Daten werden von Contoso analysiert, um die kostengünstigste Nutzung sowohl in einem Pool zusammengefasster Windows Virtual Desktop-Ressourcen als auch persönlicher Windows Virtual Desktop-Ressourcen zu ermitteln.

> [!NOTE]
> Außerdem muss Contoso seine Anwendungsserver zu Azure migrieren, um sie näher an die Windows Virtual Desktop-Umgebung zu bringen und die Netzwerklatenz für die Benutzer zu verringern.

## <a name="step-2-create-the-windows-virtual-desktop-environment-for-pooled-desktops"></a>Schritt 2: Erstellen der Windows Virtual Desktop-Umgebung für gepoolte Desktops

Mit dem Azure-Portal erstellt Contoso eine Windows Virtual Desktop-Umgebung für die Benutzer für in einem Pool zusammengefasste Ressourcen. Später werden die Migrationsschritte durchgeführt, um persönliche Desktops derselben Umgebung anzufügen.

- Contoso wählt das richtige Abonnement aus und erstellt einen neuen Windows Virtual Desktop-Hostpool.

  ![Bereitstellen eines Windows Virtual Desktop-Hostpools](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool.png)
  _Abbildung 11: Ein neuer Windows Virtual Desktop-Hostpool._

- Sie geben Abonnement, Ressourcengruppe und Region an. Als nächstes wählen sie den Namen für den Hostpool, den Desktoptyp und Standarddesktopbenutzer. Der Desktoptyp wird auf „In Pool“ festgelegt, da Contoso für einige seiner Benutzer mit einer neuen freigegebenen Umgebung beginnt. Für Standarddesktopbenutzer ist kein Eintrag erforderlich. Sie fahren damit fort, die virtuellen Computer zu konfigurieren.

  ![Migrationsvorgang](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool-basics-alt.png)
  _Abbildung 12: Voraussetzungen zum Konfigurieren virtueller Computer._

- An diesem Punkt konfiguriert Contoso die VM, beginnend mit der Auswahl einer benutzerdefinierten Größe durch Klicken auf „Größe ändern“, oder die Standardeinstellung wird übernommen.
- Windows Virtual Desktop wird als VM-Namenspräfix für diese in einem Pool zusammengefassten Desktops ausgewählt.
- Da Contoso die in einem Pool zusammengefassten Server erstellt, um die neue Windows 10-Multisessionfunktionalität für die VM-Einstellungen zu verwenden, wird „Katalog“ als Imagequelle festgelegt, sodass sie das Windows 10 Enterprise-Multisessionimage für die virtuellen Computer auswählen können.
- Basierend auf den Rollen der Benutzer aus der Lakeside-Bewertung legt Contoso die Gesamtanzahl der Benutzer auf 150 fest.
- Andere Einstellungen betreffen den Datenträgertyp, ein AD-Domänenbeitritt-UPN-Feld, ein Administratorkennwort, einen optionalen OE-Pfad, dem Computer hinzugefügt werden, das virtuelle Netzwerk und ein Subnetz zum Hinzufügen von Servern.

![Konfigurieren virtueller Computer](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool-configure-virtual-machines-alt.png)
_Abbildung 13: Konfigurieren virtueller Computer._

> [!NOTE]
> In diesem Schritt kann Contoso kein neues virtuelles Netzwerk erstellt werden. Bevor sie diesen Schritt erreichen, sollten sie bereits ein virtuelles Netzwerk erstellt haben, das Zugriff auf Active Directory hat.

<!-- -->

> [!NOTE]
> In diesem Schritt kann Contoso kein Benutzerkonto verwenden, für das Multi-Factor Authentication erforderlich ist. Wenn sie planen, Multi-Factor Authentication für ihre Benutzer zu verwenden, müssen sie zu diesem Zweck einen Dienstprinzipal erstellen.

- Contoso führt eine weitere Überprüfung der Windows Virtual Desktop-Einstellungen durch und erstellt die neue Umgebung in einem Pool zusammengefasster Windows Virtual Desktop-VMs.

  ![Überprüfen und Erstellen virtueller Computer](./media/contoso-migration-rds-to-wvd/wvd-new-host-pool-review-create.png)
  _Abbildung 14: Überprüfen und Erstellen virtueller Computer._

## <a name="step-3-convert-the-upds-to-fslogix-profile-containers"></a>Schritt 3: Konvertieren der UPDs in FSLogix-Profilcontainer

Da Windows Virtual Desktop keine Benutzerprofil-Datenträger (UPDs) unterstützt, muss Contoso alle UPDs über das [PowerShell-Modul FSLogixMigration](https://aka.ms/FSLogixMigrationPreviewModule) in FSLogix konvertieren.

<!-- docsTest:ignore FSLogixMigration -->

Nachdem Contoso das FSLogixMigration-Modul importiert hat, führen sie die folgenden PowerShell-Cmdlets aus, um von UPDs zu FSLogix zu migrieren.

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

## <a name="step-4-replicate-and-persistent-vms-to-windows-virtual-desktop"></a>Schritt 4: Replizieren persistenter VMs zu Windows Virtual Desktop

Der nächste Schritt des Migrationsprozesses für Contoso besteht darin, die persistenten VMs zu Windows Virtual Desktop zu migrieren. Zu diesem Zweck navigieren sie zurück zu dem Auftrag „Azure Migrate: Servermigration“, den sie zu Beginn des Vorgangs erstellt haben.

- Contoso beginnt mit der Auswahl von **Ermitteln** in den „Azure Migrate: Servermigration“-Tools.

  ![Azure Migrate: Servermigration – Ermitteln](./media/contoso-migration-rds-to-wvd/wvd-persistent-discover.png)
  _Abbildung 15: Ermitteln einer Servermigration._

- Als nächstes konvertieren sie eine Appliance in ihre Umgebung, die die Replikation der Computer in Windows Virtual Desktop verwaltet. Sie stellen sicher, dass die Zielregion auf `East US 2` festgelegt ist, wo ihre Windows Virtual Desktop-Umgebung erstellt wurde.

  ![Erstellen einer Appliance zum Verwalten der Replikation](./media/contoso-migration-rds-to-wvd/wvd-persistent-appliance.png)
  _Abbildung 16: Konvertieren einer Appliance._

- Der Replikationsanbieter wird heruntergeladen, installiert und für das Azure Migrate-Projekt registriert, um die Replikation in Azure zu starten.

  ![Herunterladen und Konfigurieren der Replikation](./media/contoso-migration-rds-to-wvd/wvd-persistent-replication.png)
  _Abbildung 17: Voraussetzungen für die Replikation in Azure._

- Die Replikation der Hosts in Azure-Blobspeicher wird nun gestartet, und Contoso kann die Replikation fortsetzen, bis sie bereit sind, die VMs zu testen und dann in die Produktionsumgebung zu migrieren.
- Sobald Computer in Azure ausgeführt werden, stellt Contoso sicher, dass der [Windows Virtual Desktop-VM-Agent](https://aka.ms/WVDVMAgent) auf jedem Computer installiert wird.
- Im Rahmen der Installation geben sie das Registrierungstoken für die Windows Virtual Desktop-Umgebung ein, um den Server der richtigen Umgebung zuzuordnen.

Das Registrierungstoken kann folgendermaßen abgerufen werden:

```powershell
Export-RDSRegistrationInfo -TenantName "Contoso" -HostPoolName "ContosoWVD" | Select-Object -ExpandProperty Token > .\registration-token.txt
```

> [!NOTE]
> Außerdem kann Contoso diesen Prozess durch die Verwendung von `msiexec`-Befehlen und Übergabe des Registrierungstokens als Variable automatisieren.

Im letzten Schritt vor der abschließenden Migration verwendet Contoso das Benutzerelement in den Azure Windows Virtual Desktop-Einstellungen, um die Server ihren jeweiligen Benutzern und Gruppen zuzuordnen.

  ![Zuweisen von Windows Virtual Desktop-Ressourcen zu Benutzern und Gruppen](./media/contoso-migration-rds-to-wvd/wvd-persistent-user-mapping.png) _Abbildung 18: Der letzte Schritt vor der abschließenden Migration._

Sobald den Benutzern Hostpools zugewiesen werden, schließt Contoso die Migration dieser Computer ab und fährt fort, die restlichen lokalen VDI-Hosts nach und nach zu Azure zu migrieren.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Jetzt, wo die virtuellen Desktops und Anwendungsserver in Azure ausgeführt werden, muss Contoso die Bereitstellung vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs auf eventuell vorhandene Sicherheitsprobleme. Zur Steuerung des Zugriffs überprüft das Team die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer. Mithilfe von Netzwerksicherheitsgruppen wird sichergestellt, dass nur für die Anwendung zulässiger Datenverkehr diese erreichen kann. Das Team zieht darüber hinaus in Erwägung, die Daten mit Azure Disk Encryption und Key Vault zu sichern.

Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery

Für die Geschäftskontinuität und Notfallwiederherstellung (Business Continuity and Disaster Recovery, BCDR) sichert Contoso die Daten auf den virtuellen Computern mit dem Azure Backup-Dienst, um die Daten zu schützen. Weitere Informationen finden Sie unter [Ein Überblick über die Sicherung von Azure-VMs](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- [Microsoft 365-Lizenzen](https://azure.microsoft.com/pricing/details/virtual-desktop/) werden für die Desktop-Bereitstellungen verwendet.
- Contoso aktiviert [Azure Cost Management und das Azure-Abrechnungsportal](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.
- Contoso verfügt über eine Lizenzierung für die VMs und nutzt den Azure-Hybridvorteil für Anwendungsserver. Contoso wird die vorhandenen virtuellen Azure-Computer konvertieren, um von diesen Preisen zu profitieren.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel verschob Contoso seine RDS-Bereitstellung auf den in Azure gehosteten Windows Virtual Desktop-Dienst.
