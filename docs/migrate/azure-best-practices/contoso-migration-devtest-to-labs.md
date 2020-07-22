---
title: Migrieren einer Dev/Test-Umgebung zu Azure DevTest Labs
description: Hier erfahren Sie, wie Contoso seine lokale Dev/Test-Umgebung mithilfe von Azure DevTest Labs in Azure verschiebt.
author: deltadan
ms.author: abuck
ms.date: 07/1/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: a65e509b2f48ce1dc9066bfc8e52501f555057b1
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199232"
---
<!-- cSpell:ignore vcenter -->

# <a name="migrate-a-devtest-environment-to-azure-devtest-labs"></a>Migrieren einer Dev/Test-Umgebung zu Azure DevTest Labs

In diesem Artikel wird veranschaulicht, wie das fiktive Unternehmen Contoso seine Dev/Test-Umgebung zu Azure DevTest Labs migriert.

## <a name="migration-options"></a>Migrationsoptionen

Beim Verschieben der Dev/Test-Umgebung in Azure stehen Contoso mehrere Optionen zur Verfügung.

| Migrationsoptionen | Ergebnis |
| --- | --- |
| [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | [Bewerten](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) und [Migrieren](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware) lokaler VMs <br><br> Ausführen von Dev/Test-Servern mithilfe von Azure IaaS <br><br> Verwalten von VMs mit [Azure Resource Manager](https://azure.microsoft.com/features/resource-manager/) |
| [DevTest Labs](https://docs.microsoft.com/azure/devtest-labs/devtest-lab-overview) | Schnelles Bereitstellen von Entwicklungs- und Testumgebungen <br><br> Minimieren von Verlusten durch Kontingente und Richtlinien <br><br> Festlegen des automatisierten Herunterfahrens zum Minimieren von Kosten <br><br> Erstellen von Windows- und Linux-Umgebungen |

> [!NOTE]
> Dieser Artikel konzentriert sich auf die Verwendung von DevTest Labs, um eine lokale Dev/Test-Umgebung in Azure zu verschieben. Informieren Sie sich, wie Contoso seine [Dev/Test-Umgebung über Azure Migrate in Azure IaaS](./contoso-migration-devtest-to-iaas.md) verschoben hat.

## <a name="business-drivers"></a>Business-Treiber

Das Führungsteam für die Entwicklung hat festgelegt, was mit dieser Migration erreicht werden soll:

- Ermöglichen des Zugriffs für Entwickler auf DevOps-Tools und Self-Service-Umgebungen
- Zugreifen auf DevOps-Tools für CI/CD-Pipelines und cloudnative Tools für Dev/Test-Vorgänge wie KI, Machine Learning und serverlose Optionen
- Sicherstellen der Governance und Compliance in Dev/Test-Umgebungen
- Einsparen von Kosten durch das Verschieben aller Dev/Test-Umgebungen aus dem Rechenzentrum und durch das Verzichten auf den Kauf von Hardware zum Entwickeln von Software

> [!NOTE]
> Contoso nutzt das [Abonnementangebot „Dev/Test Pay-As-You-Go“](https://azure.microsoft.com/offers/ms-azr-0023p) für seine Umgebungen. Jeder aktive Visual Studio-Abonnent im Team kann die Microsoft-Software, die im Azure Virtual Machines-Abonnement für Dev/Test enthalten ist, ohne zusätzliche Kosten verwenden. Contoso zahlt lediglich die Linux-Rate für ausgeführte VMs. Dies gilt auch für VMs mit SQL Server, SharePoint Server oder anderer Software, die normalerweise zu einem höheren Preis in Rechnung gestellt wird.

<!-- -->

> [!NOTE]
> Azure-Kunden mit einem Enterprise Agreement profitieren auch vom [Azure Dev/Test-Abonnementangebot](https://azure.microsoft.com/offers/ms-azr-0148p). Weitere Informationen zum Erstellen eines Azure Dev/Test-Abonnements mithilfe des Enterprise Agreement-Portals finden Sie in diesem [Video](https://channel9.msdn.com/blogs/ea.azure.com/enabling-and-creating-ea-devtest-subscriptions-through-the-ea-portal).

## <a name="migration-goals"></a>Migrationsziele

Das Entwicklungsteam von Contoso hat sich Ziele für diese Migration gesetzt. Diese Ziele werden verwendet, um die beste Migrationsmethode zu bestimmen:

- Schnelles Bereitstellen von Entwicklungs- und Testumgebungen: Es sollte nur wenige Minuten und keine Monate dauern, um die Infrastruktur zu erstellen, die ein Entwickler zum Schreiben oder Testen von Software benötigt.
- Nach der Migration sollte die Dev/Test-Umgebung von Contoso in Azure im Vergleich zum aktuellen lokalen System über erweiterte Funktionen verfügen.
- Das Betriebsmodell wechselt von der VM-Bereitstellung durch die IT-Abteilung zu DevOps mit Self-Service-Bereitstellung.
- Contoso möchte seine lokalen Dev/Test-Umgebungen möglichst schnell auslagern.
- Alle Entwickler stellen remote und sicher eine Verbindung mit den Dev/Test-Umgebungen her.

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung einschließlich der Azure-Dienste, die für Dev/Test-Vorgänge verwendet werden.

### <a name="current-architecture"></a>Aktuelle Architektur

- Die Dev/Test-VMs für die Anwendungen von Contoso werden über VMware im lokalen Rechenzentrum ausgeführt.
- Diese VMs werden für die Entwicklung und Tests verwendet, bevor Code auf die Produktions-VMs heraufgestuft wird.
- Entwickler behalten ihre eigenen Arbeitsstationen, benötigen für die Arbeit im Homeoffice jedoch neue Lösungen für Remoteverbindungen.

### <a name="proposed-architecture"></a>Vorgeschlagene Architektur

- Contoso verwendet ein [Azure Dev/Test-Abonnement](https://azure.microsoft.com/offers/ms-azr-0023p) zum Reduzieren der Kosten für Azure-Ressourcen. Dieses Abonnement bietet auch in Bezug auf VMs erhebliche Einsparungen, für die keine Lizenzgebühren für Microsoft-Software anfallen.
- DevTest Labs wird zum Verwalten der Umgebungen verwendet. Neue VMs werden in DevTest Labs erstellt, um den Umstieg auf neue Tools für die Entwicklung und Tests in der Cloud zu unterstützen.
- Die lokalen Dev/Test-VMs von Contoso im Rechenzentrum werden nach Abschluss der Migration außer Betrieb gesetzt.
- Entwickler und Tester können für ihre Arbeitsstationen auf Windows Virtual Desktop zugreifen.

![Szenarioarchitektur](./media/contoso-migration-devtest-to-labs/architecture.png)
_Abbildung 1: Szenarioarchitektur_

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Contoso hat entschieden, weiterhin Datenbanken zu verwenden, die auf VMs ausgeführt werden, um die fortlaufende Entwicklung zu unterstützen. Allerdings werden die aktuellen VMs durch neue VMs ersetzt, die in DevTest Labs ausgeführt werden. Zukünftig hat Contoso die Verwendung von PaaS-Diensten wie [Azure SQL-Datenbank](https://docs.microsoft.com/azure/azure-sql/database/sql-database-paas-overview) und [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) zum Ziel.

Aktuelle VMware-Datenbank-VMs werden außer Betrieb gesetzt und durch Azure-VMs in DevTest Labs ersetzt. Die vorhandenen Datenbanken werden mit einfachen Sicherungen und Wiederherstellungen migriert. Wenn Sie das Azure Dev/Test-Abonnementangebot nutzen, fallen für die Windows Server- und SQL Server-Instanzen keine Lizenzgebühren an, wodurch die Computekosten reduziert werden.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Alle aktuellen Entwicklungs-VMs (Anwendung und Datenbank) werden durch neue VMs ersetzt, die in DevTest Labs ausgeführt werden. Dies bedeutet, dass die Funktionen einer speziell erstellten Cloudentwicklungsumgebung genutzt werden können. <br><br> Contoso kann von seiner Investition in das Azure Dev/Test-Abonnement profitieren, um Lizenzgebühren zu sparen. <br><br> Contoso behält die vollständige Kontrolle über die Anwendungs-VMs in Azure. <br><br> Entwickler erhalten Berechtigungen für das Abonnement, wodurch sie neue Ressourcen erstellen können, ohne darauf warten zu müssen, dass die IT auf Ihre Anforderungen reagiert. |
| **Nachteile** | Bei der Migration wird nur die Entwicklung in die Cloud verlagert, und es werden keine PaaS-Dienste verwendet, da weiterhin VMs verwendet werden. Das bedeutet, dass Contoso mit der Unterstützung der Vorgänge einschließlich Sicherheitspatches auf den VMs beginnen muss. Dies wurde bisher von der IT erledigt, sodass eine Lösung für diese neue operative Aufgabe gefunden werden muss. <br><br> Contoso muss neue Anwendungs- und Datenbank-VMs erstellen, um den Prozess zu automatisieren. Das Unternehmen kann also die Vorteile der Erstellung von VMs in der Cloud und der Tools nutzen, die von DevTest Labs bereitgestellt werden, sodass dies trotz eines Nachteils insgesamt zu einem positiven Ergebnis führt. |

### <a name="migration-process"></a>Migrationsprozess

Mit DevTest Labs migriert Contoso seine Entwicklungsanwendungs- und Datenbank-VMs zu neuen Azure-VMs.

- Dabei kann schon die [Azure-Infrastruktur](./contoso-migration-infrastructure.md) einschließlich des virtuellen Entwicklungsnetzwerks verwendet werden.
- Wenn alles vorbereitet ist, wird DevTest Labs von Contoso bereitgestellt und konfiguriert.
- Contoso konfiguriert das virtuelle Entwicklungsnetzwerk, weist eine Ressourcengruppe zu und legt Rechtlinien fest.
- Für Remotearbeiten werden für Entwickler virtuelle Windows-Desktops erstellt.
- In DevTest Labs werden VMs für Entwicklungs- und Migrationsdatenbanken erstellt.

![Migrationsvorgang](./media/contoso-migration-devtest-to-labs/migration-process-devtest-labs.png)
_Abbildung 2: Migrationsvorgang_

## <a name="prerequisites"></a>Voraussetzungen

Für die Ausführung dieses Szenarios benötigt Contoso Folgendes.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Azure Dev/Test-Abonnement** | Contoso erstellt ein [Azure Dev/Test-Abonnement](https://azure.microsoft.com/offers/ms-azr-0023p), um die Kosten um bis zu 80 Prozent zu reduzieren. <br><br> Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free) erstellen. <br><br> Wenn Sie ein kostenloses Konto erstellen, sind Sie der Administrator Ihres Abonnements und können alle Aktionen durchführen. <br><br> Falls Sie ein vorhandenes Abonnement verwenden und nicht der Administrator sind, müssen Sie mit dem Administrator zusammenarbeiten, damit er Ihnen Berechtigungen vom Typ „Besitzer“ oder „Mitwirkender“ zuweist. <br><br> Wenn Sie detailliertere Berechtigungen benötigen, lesen Sie [diesen Artikel](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control). |
| **Azure-Infrastruktur** | [Weitere Informationen](./contoso-migration-infrastructure.md) zur Vorgehensweise von Contoso beim Einrichten einer Azure-Infrastruktur. |

## <a name="scenario-steps"></a>Szenarioschritte

Contoso-Administratoren gehen bei der Ausführung der Migration wie folgt vor:

> [!div class="checklist"]
>
> - **Schritt 1: Bereitstellen eines neuen Azure Dev/Test-Abonnements und Erstellen einer DevTest Labs-Instanz**
> - **Schritt 2: Konfigurieren des virtuellen Entwicklungsnetzwerks, Zuweisen einer Ressourcengruppe und Festlegen von Richtlinien**
> - **Schritt 3: Erstellen von virtuellen Windows 10 Enterprise-Desktops mit mehreren Sitzungen für die Remotearbeit von Entwicklern**
> - **Schritt 4: Erstellen von Formeln und VMs in DevTest Labs für Entwicklungs- und Migrationsdatenbanken**

## <a name="step-1-provision-a-new-azure-devtest-subscription-and-create-a-devtest-labs-instance"></a>Schritt 1: Bereitstellen eines neuen Azure Dev/Test-Abonnements und Erstellen einer DevTest Labs-Instanz

Zunächst muss Contoso über das Azure Dev/Test-Angebot ein neues Abonnement erstellen und dann eine DevTest Labs-Instanz erstellen.

Das Unternehmen geht bei der Einrichtung dieser Komponenten wie folgt vor:

Contoso verwendet den Link zum [Azure Dev/Test-Abonnementangebot](https://azure.microsoft.com/offers/ms-azr-0023p) und stellt ein neues Abonnement bereit, wodurch das Unternehmen in Bezug auf seine Systeme bis zu 80 Prozent einsparen kann. Dieses Angebot ermöglicht es Contoso, Windows 10-Images in Azure für Dev/Test-Vorgänge auszuführen. Das Unternehmen erhält Zugriff auf [Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/overview), um die Verwaltungsfunktionen der Remoteentwickler zu vereinfachen.

![DevTest-Angebot](./media/contoso-migration-devtest-to-labs/devtest-subscription.png)
_Abbildung 3: Azure Dev/Test-Abonnementangebot_

Mit dem neuen bereitgestellten Abonnement kann Contoso das Azure-Portal verwenden, um eine neue DevTest Labs-Instanz zu erstellen. Das neue Lab wird in der Ressourcengruppe `ContosoDevRG` erstellt.

![Erstellen einer DevTest Labs-Instanz mit dem Portal](./media/contoso-migration-devtest-to-labs/new-lab.png)
_Abbildung 4: Erstellen einer neuen DevTest Labs-Instanz_

## <a name="step-2-configure-the-development-virtual-network-assign-a-resource-group-and-set-policies"></a>Schritt 2: Konfigurieren des virtuellen Entwicklungsnetzwerks, Zuweisen einer Ressourcengruppe und Festlegen von Richtlinien

Wenn die DevTest Labs-Instanz erstellt wurde, führt Contoso in den folgenden Schritten Konfigurationen durch:

- Konfigurieren des virtuellen Netzwerks
- Zuweisen einer Ressourcengruppe
- Festlegen von Labrichtlinien

Das Unternehmen geht bei der Einrichtung dieser Komponenten wie folgt vor:

1. Konfigurieren des virtuellen Netzwerks:

    - Im Portal öffnet Contoso die DevTest Labs-Instanz und klickt auf **Configuration and policies** (Konfiguration und Richtlinien):

      ![Konfiguration und Richtlinien](./media/contoso-migration-devtest-to-labs/configure-lab.png)
      _Abbildung 5: DevTest Labs-Instanz: Konfiguration und Richtlinien_

    - Ein Contoso-Mitarbeiter klickt auf **Virtuelle Netzwerke** >  **+ Hinzufügen**, dann auf `vnet-dev-eus2` und anschließend auf **Speichern**. Dadurch kann das Entwicklungs-VNET für VM-Bereitstellungen verwendet werden. Es gibt auch ein virtuelles Netzwerk, das während der Bereitstellung der DevTest Labs-Instanz erstellt wurde.

      ![Virtuelle Netzwerke](./media/contoso-migration-devtest-to-labs/vnets.png)
      _Abbildung 6: Virtuelle Netzwerke_

2. Zuweisen einer Ressourcengruppe:

    - Damit sichergestellt werden kann, dass Ressourcen in der Ressourcengruppe `ContosoDevRG` bereitgestellt werden, wird dies von Contoso dies in den Labeinstellungen konfiguriert. Außerdem wird den Entwicklern die Rolle `Contributor` zugewiesen.

      ![Zuweisen einer Ressourcengruppe](./media/contoso-migration-devtest-to-labs/assign-resource-group.png)
      _Abbildung 7: Zuweisen einer Ressourcengruppe_

    > [!NOTE]
    > Die Rolle „Mitwirkender“ ist eine Rolle auf Administratorebene mit allen Rechten mit der Ausnahme, anderen Benutzern den Zugriff zu ermöglichen. Weitere Informationen finden Sie unter [Was ist die rollenbasierte Zugriffssteuerung in Azure (Azure Role-Based Access Control, Azure RBAC)?](https://docs.microsoft.com/azure/role-based-access-control/overview).

3. Festlegen von Labrichtlinien:

    - Contoso muss sicherstellen, dass Entwickler in den Richtlinien des Teams DevTest Labs verwenden. DevTest Labs wird mit diesen Richtlinien konfiguriert.

    - Das automatische Herunterfahren wird für 19 Uhr und die entsprechende Zeitzone aktiviert.

      ![Automatisches Herunterfahren](./media/contoso-migration-devtest-to-labs/autoshutdown.png)
      _Abbildung 8: Automatisches Herunterfahren_

    - Das automatische Starten ist aktiviert, sodass die VMs in Betrieb sind, wenn die Entwickler online arbeiten. Die VMs werden für die lokale Zeitzone und die Wochentage konfiguriert, an denen die Entwickler arbeiten.

      ![Automatisch Starten](./media/contoso-migration-devtest-to-labs/autostart.png)
      _Abbildung 9: Automatisch starten_

    - Die zulässigen VM-Größen werden konfiguriert, um sicherzustellen, dass große und teure VMs nicht gestartet werden dürfen.

      ![Zulässige VM-Größen](./media/contoso-migration-devtest-to-labs/vm-sizes.png)
      _Abbildung 10: Zulässige VM-Größen_

    - Die Supportnachricht ist konfiguriert.

      ![Supportnachricht](./media/contoso-migration-devtest-to-labs/support.png)
      _Abbildung 11: Supportnachricht_

## <a name="step-3-create-windows-10-enterprise-multi-session-virtual-desktops-for-developers-to-use-from-remote-locations"></a>Schritt 3: Erstellen von virtuellen Windows 10 Enterprise-Desktops mit mehreren Sitzungen für die Remotearbeit von Entwicklern

Contoso muss eine Windows Virtual Desktop-Instanz für Remoteentwickler erstellen.

Contoso erstellt eine Windows 10 Enterprise-VM mit mehreren Sitzungen aus einer Basis:

- Ein Contoso-Mitarbeiter klickt auf **Alle virtuellen Computer**>  **+ Hinzufügen** und wählt dann eine `Windows 10 enterprise multi-session`-Basis aus.

  ![Windows 10-Basis](./media/contoso-migration-devtest-to-labs/windows-10-vm-base.png)
  _Abbildung 12: Windows 10 Enterprise-Basis (mehrere Sitzungen)_

- Im nächsten Schritt wird die Größe des virtuellen Computers zusammen mit den zu installierenden Artefakten konfiguriert. In diesem Fall haben die Entwickler Zugriff auf gängige Entwicklungstools wie Visual Studio Code, Git und Chocolatey.

  ![Artefakte](./media/contoso-migration-devtest-to-labs/artifacts.png)
  _Abbildung 13: Artefakte_

- Die VM-Konfiguration wird auf ihre Richtigkeit überprüft.

  ![Erstellen eines virtuellen Computers aus einer Basis](./media/contoso-migration-devtest-to-labs/vm-from-base.png)
  _Abbildung 14: Erstellen eines virtuellen Computers aus einer Basis_

- Nachdem der virtuelle Computer erstellt wurde, können die Remoteentwickler von Contoso eine Verbindung herstellen und diese Entwicklungsarbeitsstation für ihre Arbeit verwenden. Die ausgewählten Artefakte werden installiert, wodurch die Entwickler beim Konfigurieren ihrer Arbeitsstation Zeit sparen.

  ![Remoteentwickler-VM](./media/contoso-migration-devtest-to-labs/remote-vm.png)
  _Abbildung 15: Remoteentwickler-VM_

## <a name="step-4-create-formulas-and-vms-within-devtest-labs-for-development-and-migrate-databases"></a>Schritt 4: Erstellen von Formeln und VMs in DevTest Labs für Entwicklungs- und Migrationsdatenbanken

Wenn DevTest Labs konfiguriert ist und die Remoteentwicklerarbeitsstation ausgeführt wird, kann sich Contoso auf das Erstellen der VMs für die Entwicklung konzentrieren. Zum Einstieg führt Contoso die folgenden Schritte aus:

Erstellen von Formeln (wiederverwendbare Basis) für Anwendungs- und Datenbank-VMs und Bereitstellen dieser Anwendungs- und Datenbank-VMs mithilfe der Formeln

Erstellen von Formeln für Anwendungs- und Datenbank-VMs:

- Ein Contoso-Mitarbeiter klickt auf **Formeln** >  **+ Hinzufügen** und dann auf eine `Windows 2012 R2 Datacenter`-Basis.

  ![Windows 2012 R2-Basis](./media/contoso-migration-devtest-to-labs/windows-2012-base.png)
  _Abbildung 16: Windows 2012 R2-Basis_

- Im nächsten Schritt wird die Größe des virtuellen Computers zusammen mit den zu installierenden Artefakten konfiguriert. In diesem Fall haben die Entwickler Zugriff auf gängige Entwicklungstools wie Visual Studio Code, Git und Chocolatey.

  ![Windows 2012 R2-Basiskonfiguration](./media/contoso-migration-devtest-to-labs/windows-2012-base-configuration.png)
  _Abbildung 17: Windows 2012 R2-Basiskonfiguration_

- Contoso befolgt zum Erstellen der VM-Datenbankformel die gleichen grundlegenden Schritte und verwendet dieses Mal ein SQL Server 2012-Image für die Basis.

  ![SQL 2012 R2-Basis](./media/contoso-migration-devtest-to-labs/sql-2012-base.png)
  _Abbildung 18: SQL Server 2012-Image_

- Die Formel ist mit der Größe und den Artefakten einschließlich des SQL Server Management Studios konfiguriert, das für die Formel der Datenbankentwicklungs-VM erforderlich ist.

  ![SQL 2012 R2-Basiskonfiguration](./media/contoso-migration-devtest-to-labs/sql-2012-base-configuration.png)
  _Abbildung 19: SQL 2020 R2-Basiskonfiguration_

Informieren Sie sich über die Verwendung von [Formeln](https://docs.microsoft.com/azure/lab-services/devtest-lab-manage-formulas) mit DevTest Labs.

- Contoso hat jetzt die Formeln auf Windows-Basis erstellt, die von den Entwicklern für ihre Anwendungen und Datenbanken verwendet werden.

  ![Konfigurierte Datenbank-VM](./media/contoso-migration-devtest-to-labs/contoso-formulas.png)
  _Abbildung 20: Formeln auf Windows-Basis_

Bereitstellen von Anwendungs- und Datenbank-VMs mithilfe der Formeln:

- Nach Erstellen der Formeln klickt ein Contoso-Mitarbeiter auf **Alle virtuellen Computer** und dann auf die Formel `Windows2012AppDevVmBase`, damit die Konfiguration mit den aktuellen Anwendungsentwicklungs-VMs übereinstimmt.

  ![App-VM](./media/contoso-migration-devtest-to-labs/app-vm.png)
  _Abbildung 21: Anwendungsentwicklungs-VM_

- Der virtuelle Computer wird mit der Größe und den Artefakten konfiguriert, die für diese Anwendungs-VM erforderlich sind.

  ![Konfigurierte App-VM](./media/contoso-migration-devtest-to-labs/app-vm-configuration.png)
  _Abbildung 22: Größen- und Artefaktkonfigurationen für eine VM_

- Im nächsten Schritt wird die Datenbank-VM mithilfe der Formel **SQLDbDevVmBase** bereitgestellt, damit die Konfiguration mit den aktuellen Datenbankentwicklungs-VMs übereinstimmt.

  ![Datenbank-VM](./media/contoso-migration-devtest-to-labs/database-vm.png)
  _Abbildung 23: Datenbank-VM_

- Der virtuelle Computer wird mit der Größe und den erforderlichen Artefakten konfiguriert.

  ![VM-Datenbankkonfiguration](./media/contoso-migration-devtest-to-labs/database-vm-config.png)
  _Abbildung 24: Datenbankkonfigurationen für eine VM_

- Nachdem die ersten VMs erstellt wurden, können Contoso-Entwickler mithilfe der Arbeitsstation von Remoteentwicklern nun mit dem Schreiben von Code in Azure beginnen.

  ![Contoso-VMs](./media/contoso-migration-devtest-to-labs/contoso-vms.png)
  _Abbildung 25: Contoso-VMs_

- Contoso kann jetzt seine Entwicklungsdatenbanken entweder aus Sicherungen oder mithilfe eines Typs der Codegenerierung zum Erstellen des Schemas auf den VMs wiederherstellen. Da das SQL Server Management Studio bereits mithilfe der Artefakte installiert wurde, sind dies einfache Aufgaben, für die keine Tools installiert werden müssen.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Contoso verwendet diese Schritte weiterhin zum Migrieren von VMs zu Azure mithilfe von DevTest Labs. Nachdem jede Migration vollständig durchgeführt wurde, werden alle Entwicklungs-VMs jetzt in DevTest Labs ausgeführt.

Contoso muss jetzt folgende Schritte für die Bereinigung durchführen:

- Entfernen der VMs aus dem vCenter-Inventar
- Entfernen aller VMs aus lokalen Sicherungsaufträgen
- Aktualisieren der internen Dokumentation zum Anzeigen des neuen Speicherorts und der IP-Adressen für die VMs
- Überprüfen sämtlicher Ressourcen, die mit den VMs interagieren, und Aktualisieren sämtlicher relevanter Einstellungen oder Dokumentationen, um die neue Konfiguration widerzuspiegeln.

### <a name="security"></a>Sicherheit

Das Sicherheitsteam von Contoso überprüft die Azure-VMs auf eventuell vorhandene Sicherheitsprobleme. Zur Steuerung des Zugriffs überprüft das Team die Netzwerksicherheitsgruppen (NSGs) für die virtuellen Computer. Mithilfe von Netzwerksicherheitsgruppen wird sichergestellt, dass nur für die Anwendung zulässiger Datenverkehr diese erreichen kann. Das Team zieht darüber hinaus in Betracht, die Daten über Azure Disk Encryption und Azure Key Vault auf dem Datenträger zu sichern. Weitere Informationen finden Sie unter [Bewährte Sicherheitsmethoden für IaaS-Workloads in Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Contoso stellt sicher, dass alle Azure-Entwicklungsressourcen mithilfe dieses Dev/Test-Abonnements erstellt werden, um 80 Prozent zu sparen.
- Die Budgets für alle DevTest Labs werden überprüft, und die Richtlinien für die VM-Typen werden festgelegt, um sicherzustellen, dass die Kostenvorgaben eingehalten werden und versehentlich keine Überbereitstellung erfolgt.
- Contoso aktiviert [Azure Cost Management und das Azure-Abrechnungsportal](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview), um die Überwachung und Verwaltung der Azure-Ressourcen zu unterstützen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat Contoso seine Entwicklungsumgebungen in DevTest Labs verlagert. Außerdem hat das Unternehmen Windows Virtual Desktop als Plattform für Remote- und Vertragsentwickler implementiert.

**Benötigen Sie weitere Hilfe?**

[Erstellen Sie jetzt eine DevTest Labs-Instanz](https://docs.microsoft.com/azure/lab-services/devtest-lab-create-lab) in Ihrem Abonnement, und informieren Sie sich über die Verwendung von [DevTest Labs für Entwickler](https://docs.microsoft.com/azure/lab-services/devtest-lab-developer-lab).
