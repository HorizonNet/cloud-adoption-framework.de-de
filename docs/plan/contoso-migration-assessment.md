---
title: Bewerten lokaler Workloads für die Azure-Migration
description: Anhand eines anschaulichen Beispiels wird beschrieben, wie Sie eine lokale Anwendung für die Migration zu Azure bewerten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: bc1753821e61ee0a7af74bc720a56ec8962ecded
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214581"
---
<!-- docsTest:disable TODO -->

<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc OSTICKETWEB OSTICKETMYSQL smarthotelapp ctypes ctypeslib prereqs -->

# <a name="assess-on-premises-workloads-for-migration-to-azure"></a>Bewerten lokaler Workloads für die Migration zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso eine lokale App für die Migration zu Azure bewertet. In diesem Beispielszenario wird die lokale App SmartHotel360 von Contoso derzeit unter VMware ausgeführt. Contoso bewertet virtuelle Computer der App mit dem Azure Migrate-Dienst und die SQL Server-Datenbank der App mit dem Datenmigrations-Assistenten.

## <a name="overview"></a>Übersicht

Contoso erwägt die Migration zu Azure und muss anhand einer technischen und finanziellen Bewertung ermitteln, ob seine lokalen Workloads gute Kandidaten für die Cloudmigration sind. Das Contoso-Team möchte vor allem die Computer- und Datenbankkompatibilität für die Migration bewerten. Die Kapazität und die Kosten für die Ausführung der Ressourcen von Contoso in Azure sollen geschätzt werden.

Als Einstieg und zum besseren Verständnis der beteiligten Technologie bewertet Contoso zwei seiner lokalen Apps. Dies ist in der folgenden Tabelle zusammengefasst. Das Unternehmen führt eine Bewertung der Migrationsszenarien durch, in denen ein neuer Host zugewiesen wird und die Apps für die Migration umgestaltet werden. Weitere Informationen zum Zuweisen eines neuen Hosts und Umgestalten finden Sie in der [Übersicht mit Contoso-Migrationsbeispielen](../migrate/azure-best-practices/contoso-migration-overview.md).

<!-- markdownlint-disable MD033 -->

| App-Name | Plattform | App-Ebenen | Details |
| --- | --- | --- | --- |
| SmartHotel360 <br><br> (Verwaltung der Reiseanforderungen von Contoso) | Wird mit einer SQL Server-Datenbank unter Windows ausgeführt | App mit zwei Schichten. Die Front-End-ASP.NET-Website wird auf einer VM (**WEBVM**) und die SQL Server-Instanz auf einer anderen VM (**SQLVM**) ausgeführt. | VMs sind VMware, die auf einem mit vCenter Server verwalteten ESXi-Host ausgeführt werden. <br><br> Sie können die Beispiel-App von [GitHub](https://github.com/Microsoft/SmartHotel360) herunterladen. |
| osTicket <br><br> (Service Desk-App von Contoso) | Wird auf Linux/Apache mit MySQL PHP (LAMP) ausgeführt | App mit zwei Schichten. Eine Front-End-PHP-Website wird auf einer VM (**OSTICKETWEB**) und die MySQL-Datenbank auf einer anderen VM (**OSTICKETMYSQL**) ausgeführt. | Die App wird von Kundendienst-Apps verwendet, um Probleme für die internen Mitarbeitern und externen Kunden zu verfolgen. <br><br> Sie können das Beispiel von [GitHub](https://github.com/osTicket/osTicket) herunterladen. |

<!-- markdownlint-enable MD033 -->

## <a name="current-architecture"></a>Aktuelle Architektur

In diesem Diagramm ist die aktuelle lokale Infrastruktur von Contoso dargestellt:

![Aktuelle Contoso-Architektur](../migrate/azure-best-practices/media/contoso-migration-assessment/contoso-architecture.png)

- Contoso verfügt über ein zentrales Rechenzentrum. Das Rechenzentrum befindet sich in New York City, im Osten der USA.
- Contoso verfügt in den USA über drei weitere Niederlassungen.
- Das zentrale Rechenzentrum ist über eine auf Glasfaser basierende Metro-Ethernet-Verbindung (500 MBit/s) mit dem Internet verbunden.
- Jede Niederlassung ist lokal über Business-Class-Verbindungen mit dem Internet verbunden, und IPsec-VPN-Tunnel führen zurück zum zentralen Rechenzentrum. Aufgrund dieser Anordnung ist das gesamte Netzwerk von Contoso dauerhaft verbunden, und die Internetverbindung wird optimiert.
- Das Hauptrechenzentrum ist vollständig mit VMware virtualisiert. Contoso verfügt über zwei ESXi 6.5-Virtualisierungshosts, die mit vCenter Server 6.5 verwaltet werden.
- Contoso nutzt Active Directory für die Identitätsverwaltung. Contoso verwendet im internen Netzwerk DNS-Server.
- Die Domänencontroller im Rechenzentrum werden auf VMware-VMs ausgeführt. Die Domänencontroller in lokalen Niederlassungen werden auf physischen Servern ausgeführt.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team von Contoso hat eng mit den Geschäftspartnern des Unternehmens zusammengearbeitet, um zu verstehen, was mit dieser Migration erreicht werden soll:

- **Unternehmenswachstum.** Contoso wächst. Aus diesem Grund hat der Druck auf die lokalen Systeme und die Infrastruktur des Unternehmens zugenommen.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und die Prozesse für seine Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, damit die Kundenanforderungen in kürzerer Zeit erfüllt werden können.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Sie muss schneller reagieren können, als sich die Gegebenheiten des Markts ändern, damit das Unternehmen auf dem globalen Markt Erfolg hat. Die IT-Abteilung von Contoso darf keine Hindernisse in den Weg stellen und keine Geschäftsabläufe blockieren.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.

## <a name="assessment-goals"></a>Bewertungsziele

Das Cloudteam von Contoso hat sich Ziele für die Migrationsbewertungen gesetzt:

- Nach der Migration sollten die Apps in Azure die gleichen Leistungsmerkmale aufweisen, über die sie in der lokalen VMware-Umgebung von Contoso derzeit verfügen. Die Umstellung auf die Cloud bedeutet nicht, dass die Leistung der App weniger wichtig ist.
- Contoso muss die Kompatibilität seiner Anwendungen und Datenbanken in Bezug auf die Azure-Anforderungen verstehen. Außerdem muss Contoso mit den Hostingoptionen in Azure vertraut sein.
- Die Datenbankverwaltung von Contoso sollte nach dem Verlagern von Apps in die Datenbank reduziert werden.
- Contoso möchte nicht nur verstehen, welche Migrationsoptionen verfügbar sind, sondern auch über die Infrastrukturkosten nach der Verlagerung in die Cloud Bescheid wissen.

## <a name="assessment-tools"></a>Bewertungstools

Contoso nutzt Microsoft-Tools für seine Migrationsbewertung. Die Tools sind an den Zielen des Unternehmens ausgerichtet und sollten Contoso alle benötigten Informationen liefern.

| Technologie | BESCHREIBUNG | Kosten |
| --- | --- | --- |
| [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso nutzt den Datenmigrations-Assistenten, um Kompatibilitätsprobleme zu bewerten und zu erkennen, die ggf. die Datenbankfunktionalität des Unternehmens in Azure beeinträchtigen können. Mit dem Datenmigrations-Assistenten wird die Featureparität zwischen SQL-Quellen und -Zielen bewertet. Er stellt Empfehlungen zu Verbesserungen der Leistung und Zuverlässigkeit bereit. | Der Datenmigrations-Assistent ist ein kostenloses Tool, das heruntergeladen werden kann. |
| [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | Contoso nutzt den Azure Migrate-Dienst, um seine VMware-VMs zu bewerten. Azure Migrate bewertet die Eignung der Computer für die Migration. Der Dienst stellt Schätzungen zur Größe und zu den Kosten für die Ausführung in Azure bereit. | Ab Mai 2018 ist Azure Migrate ein kostenloser Dienst. |
| [Dienstzuordnung](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-service-map) | Für Azure Migrate wird eine Dienstzuordnung verwendet, um Abhängigkeiten zwischen Computern anzuzeigen, die das Unternehmen migrieren möchte. | Die Dienstzuordnung ist Teil von Azure Monitor-Protokollen. Derzeit kann Contoso die Dienstzuordnung 180 Tage lang nutzen, ohne dass Gebühren anfallen. |

In diesem Szenario lädt Contoso den Datenmigrations-Assistenten herunter und führt ihn aus, um die lokale SQL Server-Datenbank für seine Reise-App zu bewerten. Contoso verwendet Azure Migrate mit Zuordnung von Abhängigkeiten, um die App-VMs zu bewerten, bevor die Migration zu Azure migriert wird.

## <a name="assessment-architecture"></a>Architektur für die Bewertung

![Architektur für Migrationsbewertung](../migrate/azure-best-practices/media/contoso-migration-assessment/migration-assessment-architecture.png)

- Contoso ist ein fiktiver Name für ein typisches Unternehmen.
- Contoso verfügt über ein lokales Rechenzentrum (**contoso-datacenter**) und lokale Domänencontroller (**CONTOSODC1**, **CONTOSODC2**).
- VMware-VMs befinden sich auf VMware ESXi-Hosts mit Version 6.5 (**contosohost1**, **contosohost2**).
- Die VMware-Umgebung wird per vCenter Server 6.5 verwaltet (**vcenter.contoso.com** auf einer VM).
- Die Reise-App SmartHotel360 weist die folgenden Merkmale auf:
  - Die App ist auf zwei VMware-VMs angeordnet (**WEBVM** und **SQLVM**).
  - Die VMs befinden sich auf dem VMware ESXi-Host **contosohost1.contoso.com**.
  - Die VMs werden mit SP1 auf Windows Server 2008 R2 Datacenter ausgeführt.
- Die VMware-Umgebung wird mit einem vCenter Server (**vcenter.contoso.com**) verwaltet, der auf einer VM ausgeführt wird.
- Service Desk-App „osTicket“:
  - Die App ist auf zwei VMs angeordnet (**OSTICKETWEB** und **OSTICKETMYSQL**).
  - Auf den VMs wird Ubuntu Linux Server 16.04-LTS ausgeführt.
  - Auf **OSTICKETWEB** werden Apache 2 und PHP 7.0 ausgeführt.
  - Auf **OSTICKETMYSQL** wird MySQL 5.7.22 ausgeführt.

## <a name="prerequisites"></a>Voraussetzungen

Contoso und andere Benutzer müssen für diese Bewertung die folgenden Voraussetzungen erfüllen:

- Berechtigungen „Besitzer“ oder „Mitwirkender“ für das Azure-Abonnement oder für eine Ressourcengruppe im Azure-Abonnement.
- Eine lokale vCenter Server-Instanz mit Version 6.5, 6.0 oder 5.5.
- Ein Konto mit Lesezugriff für vCenter Server bzw. Berechtigungen für die Kontoerstellung.
- Berechtigungen zum Erstellen einer VM auf der vCenter Server-Instanz mit einer OVA-Vorlage.
- Mindestens einen ESXi-Host mit Version 5.5 oder höher.
- Mindestens zwei lokale VMware-VMs (mit Ausführung einer SQL Server-Datenbank auf einer VM).
- Berechtigungen zum Installieren von Azure Migrate-Agents auf jeder VM.
- Die VMs sollten über eine direkte Internetverbindung verfügen.
  - Sie können den Internetzugriff auf die [erforderlichen URLs](https://docs.microsoft.com/azure/migrate/concepts-collector) beschränken.
  - Wenn Ihre virtuellen Computer nicht mit dem Internet verbunden sind, muss das Azure [Log Analytics-Gateway](https://docs.microsoft.com/azure/azure-monitor/platform/gateway) darauf installiert sein, und Agent-Datenverkehr muss damit weitergeleitet werden.
- Der vollqualifizierte Domänenname (Fully Qualified Domain Name, FQDN) des virtuellen Computers, auf dem die SQL Server-Instanz ausgeführt wird, für die Datenbankbewertung.
- Für die Windows Firewall auf der SQL Server-VM sollten externe Verbindungen über TCP-Port 1433 (Standard) zugelassen sein. Dieses Setup ermöglicht die Verbindungsherstellung für den Datenmigrations-Assistenten.

## <a name="assessment-overview"></a>Bewertungsübersicht

Hier ist angegeben, wie Contoso die Bewertung durchführt:

> [!div class="checklist"]
>
> - **Schritt 1: Herunterladen und Installieren des Datenmigrations-Assistenten.** Contoso bereitet den Datenmigrations-Assistenten auf die Bewertung der lokalen SQL Server-Datenbank vor.
> - **Schritt 2: Bewerten der Datenbank mithilfe des Datenmigrations-Assistenten.** Contoso führt die Datenbankbewertung aus und analysiert sie.
> - **Schritt 3: Vorbereiten der VM-Bewertung mit Azure Migrate.** Contoso richtet die lokalen Konten ein und passt die VMware-Einstellungen an.
> - **Schritt 4: Ermitteln der lokalen virtuellen Computer mit Azure Migrate.** Contoso erstellt einen virtuellen Azure Migrate-Collector-Computer. Anschließend führt Contoso den Collector aus, um die VMs für die Bewertung zu ermitteln.
> - **Schritt 5: Vorbereiten der Abhängigkeitsanalyse mit Azure Migrate.** Contoso installiert Azure Migrate-Agents auf den virtuellen Computern, damit das Unternehmen die Zuordnung der Abhängigkeiten zwischen virtuellen Computern anzeigen kann.
> - **Schritt 6: Bewerten der virtuellen Computer mit Azure Migrate.** Contoso überprüft die Abhängigkeiten, gruppiert die virtuellen Computern und führt die Bewertung durch. Nach Abschluss der Bewertung wird sie von Contoso als Vorbereitung auf die Migration analysiert.

    > [!NOTE]
    > Assessments shouldn't just be limited to using tooling to discover information about your environment. You should also schedule time to speak to business owners, end users, and other members of the IT department to fully understand of what is happening in the environment and understand factors that tooling cannot tell you. 

## <a name="step-1-download-and-install-data-migration-assistant"></a>Schritt 1: Herunterladen und Installieren des Datenmigrations-Assistenten

1. Contoso lädt den Datenmigrations-Assistenten über das [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) herunter.
    - Der Datenmigrations-Assistent kann auf jedem Computer installiert werden, mit dem eine Verbindung mit der SQL Server-Instanz hergestellt werden kann. Es ist nicht erforderlich, dass Contoso ihn auf dem SQL Server-Computer ausführt.
    - Der Datenmigrations-Assistent sollte nicht auf dem SQL Server-Hostcomputer ausgeführt werden.
2. Contoso führt die heruntergeladene Setupdatei (DownloadMigrationAssistant.msi) aus, um die Installation zu starten.
3. Auf der Seite **Fertigstellen** wählt Contoso die Option **Launch Microsoft Data Migration Assistant** (Microsoft-Datenmigrations-Assistenten starten) aus, bevor der Assistent beendet wird.

## <a name="step-2-run-and-analyze-the-database-assessment-for-smarthotel360"></a>Schritt 2: Ausführen und Analysieren der Datenbankbewertung für SmartHotel360

Contoso kann jetzt eine Bewertung durchführen, um seine lokale SQL Server-Datenbank für die App SmartHotel360 zu analysieren.

1. Im Datenmigrations-Assistenten wählt Contoso **Neu** > **Bewertung** aus und vergibt für die Bewertung dann einen Projektnamen.

2. Für **Quellservertyp** wählt Contoso **SQL Server** und für **Zielservertyp** wählt Contoso **SQL Server auf virtuellen Azure-Computern**

    ![Datenmigrations-Assistent – Auswählen der Quelle](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-1.png)

    > [!NOTE]
    > Derzeit unterstützt der Datenmigrations-Assistent die Bewertung für die Migration einer verwalteten Azure SQL-Datenbank-Instanz nicht. Als Problemumgehung verwendet Contoso SQL Server auf einer Azure-VM als angenommenes Ziel für die Bewertung.

3. Unter **Zielversion auswählen** wählt Contoso „SQL Server 2017“ als Zielversion aus. Contoso muss diese Version auswählen, weil sie von der verwalteten SQL-Datenbank-Instanz verwendet wird.

4. Contoso wählt Berichte aus, um Informationen zur Kompatibilität und zu neuen Features zu erhalten:

    - Unter **Kompatibilitätsprobleme** werden Informationen zu Änderungen angezeigt, die die Migration ggf. verhindern oder für die vor der Migration eine kleinere Anpassung erforderlich ist. Mit diesem Bericht erhält Contoso Informationen zu allen derzeit verwendeten Features, die als veraltet eingestuft wurden. Die Probleme sind nach Kompatibilitätsgrad angegeben.
    - Unter **Empfehlung zu neuen Features** werden Informationen zu neuen Features auf der SQL Server-Zielplattform angezeigt, die nach der Migration für die Datenbank verwendet werden können. Empfehlungen zu neuen Features befinden sich unter den Überschriften **Leistung**, **Sicherheit** und **Speicher**.

    ![Datenmigrations-Assistent – Kompatibilitätsprobleme und neue Features](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-2.png)

5. Unter **Mit Server verbinden** gibt Contoso den Namen der VM, auf der die Datenbank ausgeführt wird, und die Anmeldeinformationen für den Zugriff auf diese VM an. Contoso wählt die Option **Serverzertifikat vertrauen** aus, um sicherzustellen, dass die VM auf SQL Server zugreifen kann. Anschließend wählt Contoso die Option **Verbinden**.

    ![Datenmigrations-Assistent – Mit Server verbinden](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-3.png)

6. Unter **Quelle hinzufügen** fügt Contoso die Datenbank hinzu, die bewertet werden soll, und wählt dann **Weiter**, um die Bewertung zu starten.

7. Die Bewertung wird erstellt.

    ![Datenmigrations-Assistent – Erstellen der Bewertung](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-4.png)

8. Unter **Ergebnisse überprüfen** zeigt Contoso die Ergebnisse der Bewertung an.

### <a name="analyze-the-database-assessment"></a>Analysieren der Datenbankbewertung

Die Ergebnisse werden angezeigt, sobald sie verfügbar sind. Wenn Contoso Probleme behebt, muss es die Option **Bewertung neu starten** auswählen, um die Bewertung erneut durchzuführen.

1. Im Bericht **Kompatibilitätsprobleme** überprüft Contoso mögliche Probleme für jeden Kompatibilitätsgrad. Kompatibilitätsgrade sind den SQL Server-Versionen wie folgt zugeordnet:

    - 100: SQL Server 2008/Azure SQL-Datenbank
    - 110: SQL Server 2012/Azure SQL-Datenbank
    - 120: SQL Server 2014/Azure SQL-Datenbank
    - 130: SQL Server 2016/Azure SQL-Datenbank
    - 140: SQL Server 2017/Azure SQL-Datenbank

    ![Datenmigrations-Assistent – Bericht zu Kompatibilitätsproblemen](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-5.png)

2. Im Bericht **Featureempfehlungen** zeigt Contoso die Leistungs-, Sicherheits- und Speicherfeatures an, die von der Bewertung nach der Migration empfohlen werden. Es werden verschiedene Features empfohlen, z.B. In-Memory-OLTP, Columnstore-Indizes, Stretch Database, Always Encrypted, dynamische Datenmaskierung und Transparent Data Encryption.

    ![Datenmigrations-Assistent – Bericht mit Featureempfehlungen](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-6.png)

    > [!NOTE]
    > Contoso sollte [Transparent Data Encryption für alle SQL Server-Datenbanken aktivieren](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017). Dies ist noch wichtiger, wenn sich eine Datenbank in der Cloud befindet, als wenn sie lokal gehostet wird. Transparent Data Encryption sollte erst nach der Migration aktiviert werden. Wenn Transparent Data Encryption bereits aktiviert ist, muss Contoso das Zertifikat bzw. den asymmetrischen Schlüssel in die Masterdatenbank des Zielservers verschieben. Erfahren Sie, wie Sie [eine per Transparent Data Encryption geschützte Datenbank auf eine andere SQL Server-Instanz verschieben](https://docs.microsoft.com/sql/relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server?view=sql-server-2017).

3. Contoso kann die Bewertung im JSON- oder CSV-Format exportieren.

> [!NOTE]
> Gehen Sie für umfangreichere Bewertungen wie folgt vor:
>
> - Führen Sie mehrere Bewertungen gleichzeitig durch, und zeigen Sie den Status der Bewertungen auf der Seite **Alle Bewertungen** an.
> - Fassen Sie die Bewertungen in einer [SQL Server-Datenbank](https://docs.microsoft.com/sql/dma/dma-consolidatereports?view=ssdt-18vs2017) zusammen.
> - Fassen Sie die Bewertungen in einem [Power BI-Bericht](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport?view=ssdt-18vs2017) zusammen.

## <a name="step-3-prepare-for-vm-assessment-by-using-azure-migrate"></a>Schritt 3: Vorbereiten der VM-Bewertung mit Azure Migrate

Contoso muss ein VMware-Konto erstellen, das von Azure Migrate zum automatischen Ermitteln von VMs für die Bewertung verwendet werden kann. Außerdem muss das Unternehmen überprüfen, ob es über Rechte zum Erstellen einer VM verfügt, die Ports notieren, die geöffnet sein müssen, und die Einstellungsebene für Statistiken festlegen.

### <a name="set-up-a-vmware-account"></a>Einrichten eines VMware-Kontos

Für die VM-Ermittlung ist ein Konto mit Lesezugriff in vCenter Server mit den folgenden Eigenschaften erforderlich:

- **Benutzertyp:** Mindestens ein Benutzer mit Lesezugriff.
- **Berechtigungen:** Aktivieren Sie für das Datencenterobjekt das Kontrollkästchen **Propagate to Child Objects** (An untergeordnete Objekte weitergeben). Wählen Sie für **Rolle** die Option **Schreibgeschützt**.
- **Details:** Der Benutzer wird auf Datencenterebene zugewiesen und hat Zugriff auf alle Objekte im Datencenter.
- Um den Zugriff einzuschränken, weisen Sie den untergeordneten Objekten (vSphere-Hosts, Datenspeicher, virtuelle Computer und Netzwerke) die Rolle **No access** (Kein Zugriff) mit **Propagate to child object** (An untergeordnetes Objekt weitergeben) zu.

### <a name="verify-permissions-to-create-a-vm"></a>Überprüfen der Berechtigungen für die Erstellung einer VM

Contoso vergewissert sich, dass es über Berechtigungen zum Erstellen einer VM per Import einer Datei im OVA-Format verfügt. Informieren Sie sich, wie Sie [eine Rolle mit Berechtigungen erstellen und zuweisen](https://kb.vmware.com/s/article/1023189?other.KM_Utility.getArticleLanguage=1&r=2&other.KM_Utility.getArticleData=1&other.KM_Utility.getArticle=1&ui-comm-runtime-components-aura-components-siteforce-qb.Quarterback.validateRoute=1&other.KM_Utility.getGUser=1).

### <a name="verify-ports"></a>Überprüfen der Ports

Die Contoso-Bewertung verwendet Abhängigkeitszuordnung. Für die Abhängigkeitszuordnung muss ein Agent auf VMs installiert werden, auf die zugegriffen wird. Der Agent muss über den TCP-Port 443 jeder VM jeweils eine Verbindung mit Azure herstellen können. Informieren Sie sich über die [Verbindungsanforderungen](https://docs.microsoft.com/azure/log-analytics/log-analytics-concept-hybrid).

## <a name="step-4-discover-vms"></a>Schritt 4: VMs ermitteln

Zum Ermitteln von VMs erstellt Contoso ein Azure Migrate-Projekt. Contoso lädt die Collector-VM herunter und richtet sie ein. Anschließend führt Contoso den Collector aus, um die zugehörigen lokalen VMs zu ermitteln.

### <a name="create-a-project"></a>Erstellen eines Projekts

Richten Sie wie folgt ein neues Azure Migrate-Projekt ein:

1. Wählen Sie im Azure-Portal **Alle Dienste** aus, und suchen Sie nach **Azure Migrate**.

1. Wählen Sie unter **Dienste** die Option **Azure Migrate** aus.

1. Wählen Sie in der **Übersicht** unter **Server ermitteln, bewerten und migrieren** die Option **Server bewerten und migrieren** aus.

    ![Azure Migrate – Erstellen eines Migrationsprojekts](../migrate/azure-best-practices/media/contoso-migration-assessment/assess-migrate.png)

1. Wählen Sie unter **Erste Schritte** die Option **Tools hinzufügen** aus.

1. Wählen Sie unter **Projekt migrieren** Ihr Azure-Abonnement aus, und erstellen Sie bei Bedarf eine Ressourcengruppe.

1. Geben Sie unter **Projektdetails* den Projektnamen und die geografische Region an, in der Sie das Projekt erstellen möchten. USA, Asien, Europa, Australien, Vereinigtes Königreich, Kanada, Indien und Japan werden unterstützt.

    - Die geografische Region des Projekts dient nur zum Speichern der Metadaten, die von den lokalen VMs erfasst werden.
    - Beim Ausführen einer Migration kann eine beliebige Zielregion ausgewählt werden.

1. Wählen Sie **Weiter** aus.

1. Wählen Sie unter **Bewertungstool auswählen** Folgendes aus: **Azure Migrate: Server Assessment** (Azure Migrate-Serverbewertung) > **Weiter**.

    ![Azure Migrate: Bewertungstool](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-tool.png)

1. Wählen Sie unter **Migrationstool auswählen** die Option **Hinzufügen eines Migrationstools vorerst überspringen** >  und anschließend **Weiter** aus.

1. Überprüfen Sie die Einstellungen unter **Überprüfen + Tools hinzufügen**, und wählen Sie anschließend **Tools hinzufügen** aus.

1. Warten Sie einige Minuten, bis das Azure Migrate-Projekt bereitgestellt wurde. Sie werden zur Projektseite weitergeleitet. Sollte das Projekt nicht angezeigt werden, können Sie auf dem Azure Migrate-Dashboard unter **Server** darauf zugreifen.

### <a name="download-the-collector-appliance"></a>Herunterladen der Collectorappliance

1. Klicken Sie unter **Migrationsziele** > **Server** > **Azure Migrate: Server Assessment** (Azure Migrate-Serverbewertung) auf **Ermitteln**.

1. Wählen Sie unter **Computer ermitteln** > **Sind Ihre Computer virtualisiert?** die Option **Ja, mit VMware vSphere Hypervisor** aus.

1. Wählen Sie **Herunterladen** aus, um die OVA-Vorlagendatei herunterzuladen.

     ![Azure Migrate: Collector herunterladen](../migrate/azure-best-practices/media/contoso-migration-assessment/download-ova-v2.png)

### <a name="verify-the-collector-appliance"></a>Überprüfen der Collectorappliance

Vor der Bereitstellung der VM überprüft Contoso, ob die OVA-Datei sicher ist:

1. Auf dem Computer, auf dem die Datei heruntergeladen wurde, öffnet Contoso ein Eingabeaufforderungsfenster mit Administratorrechten.

2. Contoso führt den folgenden Befehl aus, um den Hash für die OVA-Datei zu generieren:

    `C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]`

    **Beispiel:**

    ```C:\>CertUtil -HashFile C:\AzureMigrate\AzureMigrate.ova SHA256```

3. Der generierte Hash sollte mit den Hashwerten übereinstimmen, die im Abschnitt [Überprüfen der Sicherheit](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#verify-security) des Tutorials [Bewerten von virtuellen VMware-Computern für die Migration](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) aufgeführt sind.

### <a name="create-the-collector-appliance"></a>Erstellen der Collectorappliance

Jetzt kann Contoso die heruntergeladene Datei auf die vCenter Server-Instanz importieren und die Collectorappliance-VM bereitstellen:

1. In der Konsole des vSphere-Clients wählt Contoso **Datei** > **Deploy OVF Template** (OVF-Vorlage bereitstellen).

    ![vSphere-Webclient – Bereitstellen der OVF-Vorlage](../migrate/azure-best-practices/media/contoso-migration-assessment/vcenter-wizard.png)

2. Im Assistenten für die Bereitstellung der OVF-Vorlage wählt Contoso die Option **Quelle** und gibt dann den Speicherort der OVA-Datei an.

3. Unter **Name and Location** (Name und Speicherort) gibt Contoso einen Anzeigenamen für die Collector-VM an. Anschließend wählt das Unternehmen den Bestandsspeicherort aus, unter dem die VM gehostet werden soll. Außerdem gibt Contoso den Host bzw. den Cluster an, auf bzw. in dem die Collectorappliance ausgeführt werden soll.

4. Unter **Speicher** gibt Contoso den Speicherort an. Unter **Datenträgerformat** wählt Contoso aus, wie der Speicher bereitgestellt werden soll.

5. Unter **Netzwerkzuordnung** gibt Contoso das Netzwerk an, über das die Collector-VM verbunden werden soll. Das Netzwerk benötigt Internetkonnektivität, um Metadaten an Azure zu senden.

6. Contoso überprüft die Einstellungen und wählt dann **Power on after deployment** > **Finish** (Nach Bereitstellung einschalten > Fertig stellen). Wenn die Appliance erstellt wird, wird eine Meldung mit dem Hinweis angezeigt, dass der Vorgang erfolgreich abgeschlossen wurde.

### <a name="run-the-collector-to-discover-vms"></a>Ausführen des Collectors zum Ermitteln virtueller Computer

Contoso führt jetzt den Collector aus, um VMs zu ermitteln. Derzeit unterstützt der Collector nur **Englisch (USA)** als Sprache des Betriebssystems und der Collectoroberfläche.

1. In der Konsole des vSphere-Clients wählt Contoso die Option **Konsole öffnen**. Contoso gibt die Einstellungen für das Akzeptieren der Lizenzbedingungen und für Kennwörter für den virtuellen Collectorcomputer an.

2. Contoso wählt auf dem Desktop die Verknüpfung mit dem **Konfigurations-Manager für Microsoft Azure-Appliances** aus.

    ![Konsole des vSphere-Clients – Collectorverknüpfung](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-shortcut-v2.png)

3. Contoso wählt im Azure Migrate-Collector die Option **Erforderliche Komponenten einrichten** aus. Contoso akzeptiert die Lizenzbedingungen und liest die Drittanbieterinformationen.

4. Der Collector überprüft, ob die VM über Internetzugriff verfügt, die Uhrzeit synchronisiert ist und der Collectordienst ausgeführt wird. (Der Collectordienst wird standardmäßig auf der VM installiert.) Contoso installiert auch das VMware vSphere-VDDK (Virtual Disk Development Kit).

    > [!NOTE]
    > Es wird vorausgesetzt, dass die VM über direkten Internetzugriff ohne Proxy verfügt.

    ![Azure Migrate-Collector – Überprüfen der erforderlichen Komponenten](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-verify-prereqs-v2.png)

5. Melden Sie sich bei Ihrem **Azure**-Konto an, und wählen Sie das Abonnement- und Migrationsprojekt aus, das Sie zuvor erstellt haben. Geben Sie auch einen Namen für die **Appliance** ein, damit Sie sie im Azure-Portal identifizieren können.

6. Unter **vCenter Server-Details angeben** gibt Contoso den Namen (FQDN) oder die IP-Adresse der vCenter Server-Instanz und die schreibgeschützten Anmeldeinformationen für die Ermittlung ein.

7. Contoso wählt einen Bereich für die VM-Ermittlung aus. Der Collector kann nur virtuelle Computer ermitteln, die sich innerhalb des angegebenen Bereichs befinden. Der Bereich kann auf einen bestimmten Ordner, ein Rechenzentrum oder einen Cluster festgelegt werden.

    ![vCenter Server-Details angeben](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-connect-vcenter.png)

8. Der Collector beginnt nun mit der Ermittlung und Erfassung von Informationen zur Contoso-Umgebung.

    ![Sammlungsfortschritt anzeigen](../migrate/azure-best-practices/media/contoso-migration-assessment/migrate-discovery.png)

### <a name="verify-vms-in-the-portal"></a>Überprüfen virtueller Computer im Portal

Nachdem der Collectorvorgang abgeschlossen wurde, überprüft Contoso, ob die VMs im Portal angezeigt werden:

1. Im Azure Migrate-Projekt wählt Contoso **Server** > **Ermittelte Server** aus. Contoso überprüft, ob die zu ermittelnden VMs angezeigt werden.

    ![Azure Migrate – Ermittelte Computer](../migrate/azure-best-practices/media/contoso-migration-assessment/discovery-complete.png)

2. Derzeit sind auf den Computern keine Azure Migrate-Agents installiert. Contoso muss die Agents installieren, um die Abhängigkeiten anzuzeigen.

    ![Azure Migrate – Agent-Installation erforderlich](../migrate/azure-best-practices/media/contoso-migration-assessment/machines-no-agent.png)

## <a name="step-5-prepare-for-dependency-analysis"></a>Schritt 5: Vorbereiten der Abhängigkeitsanalyse

Zum Anzeigen von Abhängigkeiten zwischen VMs, die bewertet werden sollen, lädt Contoso die Agents herunter und installiert sie auf den App-VMs. Contoso installiert für seine Apps Agents auf allen VMs – sowohl für Windows als auch für Linux.

### <a name="take-a-snapshot"></a>Erstellen einer Momentaufnahme

Contoso erstellt vor der Installation der Agents eine Momentaufnahme, damit eine Kopie der VMs vorhanden ist, bevor sie geändert werden.

![Momentaufnahme eines Computers](../migrate/azure-best-practices/media/contoso-migration-assessment/snapshot-vm.png)

### <a name="download-and-install-the-vm-agents"></a>Herunterladen und Installieren der VM-Agents

1. Unter **Computer** wählt Contoso den Computer aus. In der Spalte **Abhängigkeiten** wählt Contoso die Option **Installation erforderlich**.

2. Im Bereich **Computer ermitteln** führt Contoso folgende Schritte aus:
    - Der Microsoft Monitoring Agent (MMA) und der Microsoft Dependency-Agent werden für jeden virtuellen Windows-Computer heruntergeladen.
    - Der MMA und der Dependency-Agent werden für jeden virtuellen Linux-Computer heruntergeladen.

3. Contoso kopiert die ID und den Schlüssel des Arbeitsbereichs. Contoso benötigt für die MMA-Installation die Arbeitsbereichs-ID und den zugehörigen Schlüssel.

    ![Agent-Download](../migrate/azure-best-practices/media/contoso-migration-assessment/download-agents.png)

### <a name="install-the-agents-on-windows-vms"></a>Installieren der Agents auf den Windows-VMs

Contoso führt die Installation auf jeder VM durch.

#### <a name="install-the-mma-on-windows-vms"></a>Installieren des MMA auf den Windows-VMs

1. Contoso doppelklickt auf den heruntergeladenen Agent.

2. Unter **Zielordner** behält Contoso den Standardordner für die Installation bei und wählt dann **Weiter**.

3. Unter **Agent-Setupoptionen** wählt Contoso **Connect the agent to Azure Log Analytics** (Agent mit Azure Log Analytics verbinden) > **Weiter**.

    ![Microsoft Monitoring Agent-Setup – Agent-Setupoptionen](../migrate/azure-best-practices/media/contoso-migration-assessment/mma-install.png)

4. Unter **Azure Log Analytics** fügt Contoso die Angaben zur Arbeitsbereichs-ID und zum zugehörigen Schlüssel ein, die im Portal kopiert wurden.

    ![Microsoft Monitoring Agent-Setup – Azure Log Analytics](../migrate/azure-best-practices/media/contoso-migration-assessment/mma-install2.png)

5. Unter **Bereit zur Installation** installiert Contoso den MMA.

#### <a name="install-the-dependency-agent-on-windows-vms"></a>Installieren des Abhängigkeits-Agents unter Windows-VMs

1. Contoso doppelklickt auf den heruntergeladenen Dependency-Agent.

2. Contoso akzeptiert die Lizenzbedingungen und wartet, bis die Installation abgeschlossen wurde.

    ![Einrichtung des Dependency-Agents: Installation](../migrate/azure-best-practices/media/contoso-migration-assessment/dependency-agent.png)

### <a name="install-the-agents-on-linux-vms"></a>Installieren des Agents auf Linux-VMs

Contoso führt die Installation auf jeder VM durch.

#### <a name="install-the-mma-on-linux-vms"></a>Installieren des MMA auf Linux-VMs

1. Contoso installiert die Python-Bibliothek „ctypes“ auf jeder VM mit dem folgenden Befehl:

    `sudo apt-get install python-ctypeslib`

1. Contoso muss den Befehl zur Installation des MMA-Agents als Root-Benutzer ausführen. Um zum Root-Benutzer zu werden, führt Contoso den folgenden Befehl aus und gibt dann das Kennwort für den Root-Benutzer ein:

    `sudo -i`

1. Contoso installiert den MMA:

    - Contoso gibt die Arbeitsbereichs-ID und den Schlüssel für den Befehl ein.
    - Die Befehle sind für 64-Bit.
    - Die Arbeitsbereichs-ID und der Primärschlüssel befinden sich im Log Analytics-Arbeitsbereich im Azure-Portal. Wählen Sie **Einstellungen** und dann die Registerkarte **Verbundene Quellen**.
    - Führen Sie die folgenden Befehle aus, um den Log Analytics-Agent herunterzuladen, die Prüfsumme zu überprüfen und den Agent anschließend zu installieren und das Onboarding dafür durchzuführen:

        `wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w 6b7fcaff-7efb-4356-ae06-516cacf5e25d -s k7gAMAw5Bk8pFVUTZKmk2lG4eUciswzWfYLDTxGcD8pcyc4oT8c6ZRgsMy3MmsQSHuSOcmBUsCjoRiG2x9A8Mg==`

#### <a name="install-the-dependency-agent-on-linux-vms"></a>Installieren des Abhängigkeits-Agents auf Linux-VMs

Nach der MMA-Installation installiert Contoso den Dependency-Agent auf den virtuellen Linux-Computern:

1. Der Dependency-Agent wird mithilfe von „InstallDependencyAgent-Linux64.bin“ auf den Linux-Computern installiert. Hierbei handelt es sich um ein Shellskript mit einer selbstextrahierenden Binärdatei. Contoso führt die Datei mit „sh“ aus oder fügt der Datei selbst Ausführungsberechtigungen hinzu.

2. Contoso installiert den Dependency-Agent für Linux als Root-Benutzer:

    `wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin && sudo sh InstallDependencyAgent-Linux64.bin -s`

## <a name="step-6-run-and-analyze-the-vm-assessment"></a>Schritt 6: Durchführen und Analysieren der VM-Bewertung

Contoso kann jetzt die Abhängigkeiten der Computer überprüfen, und eine Gruppe erstellen. Anschließend wird die Bewertung für die Gruppe durchgeführt.

### <a name="verify-dependencies-and-create-a-group"></a>Überprüfen von Abhängigkeiten und Erstellen einer Gruppe

1. Contoso wählt die Option **Abhängigkeiten anzeigen**, um zu ermitteln, welche Computer analysiert werden sollen.

    ![Azure Migrate – Anzeigen von Computerabhängigkeiten](../migrate/azure-best-practices/media/contoso-migration-assessment/view-machine-dependencies.png)

2. Für SQLVM werden in der Abhängigkeitsübersicht die folgenden Informationen angezeigt:

    - Prozessgruppen bzw. Prozesse mit aktiven Netzwerkverbindungen auf der SQLVM für den angegebenen Zeitraum (standardmäßig eine Stunde)
    - Eingehende (Client) und ausgehende TCP-Verbindungen (Server) zu bzw. von allen abhängigen Computern.
    - Abhängige Computer mit installierten Azure Migrate-Agents werden als separate Felder angezeigt
    - Für Computer ohne installierte Agents werden Informationen zum Port und zur IP-Adresse angezeigt

3. Für Computer, auf denen der Agent installiert ist (WEBVM), wählt Contoso das Feld für den entsprechenden Computer aus, um weitere Informationen anzuzeigen. Diese Informationen umfassen den FQDN, das Betriebssystem und die MAC-Adresse.

    ![Azure Migrate – Anzeigen der Gruppenabhängigkeiten](../migrate/azure-best-practices/media/contoso-migration-assessment/sqlvm-dependencies.png)

4. Contoso wählt die VMs aus, die der Gruppe hinzugefügt werden sollen (SQLVM und WEBVM). Contoso hält die STRG-TASTE gedrückt, während es auf mehrere virtuelle Computer klickt, um sie auszuwählen.

5. Contoso wählt **Gruppe erstellen** und gibt dann einen Namen ein (**smarthotelapp**).

    > [!NOTE]
    > Sie können den Zeitbereich erweitern, um detailliertere Abhängigkeiten anzuzeigen. Sie können eine bestimmte Dauer oder das Start- und Enddatum auswählen.

### <a name="run-an-assessment"></a>Durchführen einer Bewertung

1. Unter **Gruppen** öffnet Contoso die Gruppe (**smarthotelapp**) und wählt dann die Option **Bewertung erstellen**.

    ![Azure Migrate – Erstellen einer Bewertung](../migrate/azure-best-practices/media/contoso-migration-assessment/run-vm-assessment.png)

2. Um die Bewertung anzuzeigen, wählt Contoso **Verwalten** > **Bewertungen**.

Contoso verwendet die Standardeinstellungen für Bewertungen, aber Sie können die [Einstellungen auch anpassen](https://docs.microsoft.com/azure/migrate/how-to-modify-assessment).

### <a name="analyze-the-vm-assessment"></a>Analysieren der VM-Bewertung

Eine Azure Migrate-Bewertung enthält Informationen dazu, ob die lokalen VMs mit Azure kompatibel sind, welche Größenanpassung für die Azure-VM richtig ist und welche geschätzten monatlichen Azure-Kosten anfallen.

![Azure Migrate – Bewertungsbericht](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-overview.png)

#### <a name="review-confidence-rating"></a>Prüfen der Zuverlässigkeitsstufe

![Azure Migrate – Bewertungsanzeige](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-display.png)

Eine Bewertung verfügt über eine Zuverlässigkeitsstufe, die zwischen 1 und 5 Sternen liegt (1 Stern ist die niedrigste und 5 Sterne die höchste Stufe).

- Die Zuverlässigkeitsstufe wird einer Bewertung auf der Grundlage der Verfügbarkeit von Datenpunkten zugeordnet, die zum Berechnen der Bewertung erforderlich sind.
- Anhand dieses Werts können Sie die Zuverlässigkeit der von Azure Migrate bereitgestellten Größenempfehlungen besser einschätzen.
- Zuverlässigkeitsstufen sind nützlich, wenn Sie die _leistungsbasierte Größenanpassung_ verwenden. Unter Umständen verfügt Azure Migrate nicht über genügend Datenpunkte für die nutzungsbasierte Größenanpassung. Bei der Größenanpassung vom Typ _Wie lokal_ wird die Zuverlässigkeit immer mit 5 Sternen bewertet, da Azure Migrate über alle Datenpunkte verfügt, die zum Bestimmen der VM-Größe erforderlich sind.
- Die Zuverlässigkeitsstufe für die Bewertung ist abhängig davon, wie viele Datenpunkte verfügbar sind (in Prozent):

   | Verfügbarkeit von Datenpunkten | Zuverlässigkeitsstufe |
   | --- | --- |
   | 0 % bis 20 % | 1 Stern |
   | 21 % bis 40 % | 2 Sterne |
   | 41 % bis 60 % | 3 Sterne |
   | 61 % bis 80 % | 4 Sterne |
   | 81 % bis 100 % | 5 Sterne |

#### <a name="verify-azure-readiness"></a>Überprüfen der Azure-Bereitschaft

![Azure Migrate – Bewertungsbereitschaft](../migrate/azure-best-practices/media/contoso-migration-assessment/azure-readiness.png)

Im Bewertungsbericht sind die in der Tabelle zusammengefassten Informationen enthalten. Azure Migrate benötigt die folgenden Informationen, um die leistungsbasierte Größenanpassung anzeigen zu können. Falls die Informationen nicht erfasst werden können, ist die Bewertung der Größenanpassung ggf. nicht genau.

- Nutzungsdaten für CPU und Arbeitsspeicher.
- Lese/Schreib-IOPS-Wert und Durchsatz für jeden Datenträger, der an die VM angefügt ist.
- Netzwerk-E/A-Informationen für jeden Netzwerkadapter, der an die VM angefügt ist.

<!-- markdownlint-disable MD033 -->

| Einstellung | Anzeige | Details |
| --- | --- | --- |
| **Azure-VM-Bereitschaft** | Gibt an, ob die VM für die Migration bereit ist. | Mögliche Status: <li> Bereit für Azure <li> Bereit mit Bedingungen <li> Nicht bereit für Azure <li> Bereitschaft unbekannt <br><br> Wenn eine VM nicht bereit ist, werden in Azure Migrate einige Lösungsschritte angezeigt. |
| **Azure-VM-Größe** | Für VMs, die bereit sind, stellt Azure Migrate eine Empfehlung zur Größe der Azure-VM bereit. | Die Empfehlung für die Größenanpassung richtet sich nach den Bewertungseigenschaften: <li> Wenn Sie die leistungsbasierte Größenanpassung verwendet haben, wird bei der Größenanpassung der Leistungsverlauf der VMs berücksichtigt. <li> Wenn Sie die Größenanpassung vom Typ _Wie lokal_ verwendet haben, basiert die Größenanpassung auf der Größe des lokalen virtuellen Computers, <li> und es werden keine Nutzungsdaten verwendet. |
| **Vorgeschlagenes Tool** | Da auf den Azure-Computern die Agents ausgeführt werden, prüft Azure Migrate die Prozesse, die im Computer ausgeführt werden. Es wird ermittelt, ob der Computer ein Datenbankcomputer ist. | |
| **VM-Informationen** | Im Bericht werden die Einstellungen für die lokale VM angezeigt, z.B. Betriebssystem, Starttyp und Informationen zu Datenträger und Speicher. | |

<!-- markdownlint-enable MD033 -->

#### <a name="review-monthly-cost-estimates"></a>Überprüfen der geschätzten monatlichen Kosten

In dieser Ansicht werden die Compute- und Speichergesamtkosten für die Ausführung der VMs in Azure angezeigt. Außerdem werden für jeden Computer die Details angezeigt.

![Azure Migrate – Azure-Kosten](../migrate/azure-best-practices/media/contoso-migration-assessment/azure-costs.png)

- Kostenschätzungen werden anhand der Größenempfehlungen für einen Computer berechnet.
- Die geschätzten monatlichen Kosten für Compute und Speicher werden für alle virtuellen Computer in der Gruppe aggregiert.

## <a name="clean-up-after-assessment"></a>Bereinigen nach der Bewertung

- Nachdem die Bewertung abgeschlossen ist, behält Contoso die Azure Migrate-Appliance für zukünftige Auswertungen bei.
- Contoso deaktiviert die VMware-VM. Contoso nutzt sie dann erneut, wenn weitere VMs ausgewertet werden.
- Contoso behält das Projekt **Contoso-Migration** in Azure bei. Das Projekt wird derzeit in der Ressourcengruppe **ContosoFailoverRG** in der Azure-Region „USA Osten“ bereitgestellt.
- Für die Collector-VM gilt eine 180-Tage-Evaluierungslizenz. Wenn dieser Zeitraum abgelaufen ist, muss Contoso den Collector herunterladen und wieder einrichten.

## <a name="conclusion"></a>Zusammenfassung

In diesem Szenario bewertet Contoso die Datenbank seiner App SmartHotel360 mit dem Tool für die Bewertung der Datenmigration. Das Unternehmen bewertet die lokalen VMs, indem es den Azure Migrate-Dienst verwendet. Contoso überprüft die Bewertungen, um sicherzustellen, dass die lokalen Ressourcen für die Migration zu Azure bereit sind.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Contoso diese Workload als einen potenziellen Migrationskandidaten bewertet hat, kann es damit beginnen, seine lokale Infrastruktur und seine Azure-Infrastruktur für die Migration vorzubereiten. Ein Beispiel dazu, wie Contoso diese Vorgänge ausführt, finden Sie im Abschnitt „Framework für die Cloudeinführung (Cloud Adoption Framework) – Bewährte Migrationsmethoden“ des Artikels [Bereitstellen der Azure-Infrastruktur](../migrate/azure-best-practices/contoso-migration-infrastructure.md).
