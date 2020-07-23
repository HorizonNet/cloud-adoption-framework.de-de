---
title: Migrieren von MariaDB-Datenbanken zu Azure
description: In diesem Artikel erfahren Sie, wie Contoso seine lokalen MariaDB-Datenbanken zu Azure migriert hat.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 84bd6cbef97428aacb81d4d6136439a1c9c1f3f6
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199234"
---
<!-- TODO: Verify GraphDBMS term -->
<!-- cSpell:ignore ColumnStore GraphDBMS mysqldump Navicat phpMyAdmin -->

# <a name="migrate-mariadb-databases-to-azure"></a>Migrieren von MariaDB-Datenbanken zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-MariaDB-Datenbankplattform zu Azure geplant und durchgeführt hat.

Contoso zieht die Verwendung von MariaDB gegenüber MySQL aus mehreren Gründe vor. Dazu gehören die unzähligen Speicher-Engines, die Cache- und Indexleistung, die Open-Source-Unterstützung mit Features und Erweiterungen sowie die ColumnStore-Unterstützung für Analysen. Das Ziel der Migration ist es, MariaDB weiterhin zu verwenden, ohne sich Gedanken über die Verwaltung der dafür benötigten Umgebung zu machen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Erhöhen der Verfügbarkeit.** Bei der lokalen MariaDB-Umgebung von Contoso sind Probleme mit der Verfügbarkeit aufgetreten. Die Anwendungen, die diesen Datenspeicher nutzen, müssen für das Unternehmen zuverlässiger werden.

- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden, und Kundenanforderungen schneller bearbeiten.

- **Steigerung der Flexibilität.**  Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. IT darf nicht im Weg stehen oder zum Geschäftshindernis werden.

- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich Ziele für die Migration gesetzt, anhand derer die beste Migrationsmethode bestimmt wird.

| Anforderungen | Details |
| --- | --- |
| **Verfügbarkeit** | Derzeit haben interne Mitarbeiter Schwierigkeiten mit der Hostingumgebung für die MariaDB-Instanz. Contoso wünscht eine Verfügbarkeit der Datenbankschicht von nahezu 99,99 Prozent. |
| **Skalierbarkeit** | Der lokale Datenbankhost weist schnell keine Kapazität mehr auf, und Contoso braucht eine Möglichkeit, die Instanzen über die aktuellen Einschränkungen hinaus zu skalieren oder zentral herunterzuskalieren, wenn sich die Geschäftsumgebung ändert, um so Kosten zu sparen. |
| **Leistung** | Die Personalabteilung von Contoso muss täglich, wöchentlich und monatlich mehrere Berichte ausführen. Beim Ausführen dieser Berichte werden erhebliche Leistungsprobleme bei der Anwendung für die Mitarbeiter festgestellt. Die Berichte müssen ausgeführt werden, ohne dass sich dies auf die Anwendungsleistung auswirkt. |
| **Sicherheit** | Contoso muss sicher sein, dass nur die internen Anwendungen auf die Datenbank zugreifen können und sie nicht über das Internet sichtbar oder zugänglich ist. |
| **Überwachung** | Contoso verwendet derzeit Tools zum Überwachen der Metriken von MariaDB und zum Bereitstellen von Benachrichtigungen bei Auftreten von CPU-, Arbeitsspeicher- oder Speicherproblemen. Dieselben Möglichkeiten sollen auch in Azure bereitstehen. |
| **Geschäftskontinuität** | Der Personaldatenspeicher ist ein wichtiger Bestandteil der täglichen Abläufe bei Contoso und die Ausfallzeit im Fall einer Beschädigung oder Wiederherstellung soll minimiert werden. |
| **Azure** | Contoso möchte die Anwendung in Azure verschieben, ohne dass sie auf VMs ausgeführt wird. In den Anforderungen von Contoso ist angegeben, dass in der Datenschicht auf Azure-PaaS-Dienste zurückgegriffen werden soll. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Tools und Dienste.

### <a name="current-application"></a>Aktuelle Anwendung

MariaDB hostet Mitarbeiterdaten, die für alle Belange der Personalabteilung des Unternehmens verwendet werden. Eine [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung wird als Front-End zum Verarbeiten von Personalanfragen der Mitarbeiter verwendet. Contoso hat 100.000 Mitarbeiter weltweit, und daher ist die Betriebszeit für die Datenbanken sehr wichtig.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Bewerten der Umgebungen hinsichtlich Migrationskompatibilität.
- Verwenden gängiger Open-Source-Tools zum Migrieren von Datenbanken zur Azure Database for MariaDB-Instanz.
- Ändern aller Anwendungen und Prozesse, damit sie die neue Azure Database for MariaDB-Instanz verwenden.

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso die in Azure verfügbaren Features für das Hosting der MariaDB-Datenbanken geprüft. Die folgenden Überlegungen waren ausschlaggebend für die Entscheidung für Azure.

- Ähnlich wie Azure SQL unterstützt auch Azure Database for MariaDB [Firewallregeln](https://docs.microsoft.com/azure/mariadb/concepts-firewall-rules).
- Azure Database for MariaDB kann mit [Azure Virtual Network](https://docs.microsoft.com/azure/mariadb/concepts-data-access-security-vnet) verwendet werden, um zu verhindern, dass die Instanz öffentlich zugänglich ist.
- Azure Database for MariaDB verfügt über die erforderlichen Compliance- und Datenschutzzertifizierungen, die Contoso für die Prüfer einhalten muss.
- Die Verarbeitungsleistung für Berichte und Anwendung wird durch die Verwendung von Lesereplikaten verbessert.
- Der Dienst kann mithilfe von [Private Link](https://docs.microsoft.com/azure/mariadb/concepts-data-access-security-private-link) nur für den internen Netzwerkdatenverkehr (kein öffentlicher Zugriff) verfügbar gemacht werden.
- Das Unternehmen hat entschieden, nicht zu Azure Database for MySQL zu wechseln, da möglicherweise in Zukunft das MariaDB ColumnStore- und GraphDBMS-Datenbankmodell verwendet werden soll.
- Die [Bandbreite und Latenz](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) zwischen der Anwendung und der Datenbank ist je nach ausgewähltem Gateway (ExpressRoute oder Site-to-Site-VPN) ausreichend.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Azure Database for MariaDB bietet eine finanziell abgesicherte Vereinbarung zum Service Level (SLA) von 99,99 Prozent für [Hochverfügbarkeit](https://docs.microsoft.com/azure/mariadb/concepts-high-availability). <br><br> Azure bietet die Möglichkeit, während Spitzenladezeiten jedes Quartal zentral hoch- oder herunterzuskalieren. Contoso kann durch den Kauf von [reservierter Kapazität](https://docs.microsoft.com/azure/mariadb/concept-reserved-pricing) noch weitere Einsparungen erzielen. <br><br> Azure bietet Funktionen zur Point-in-Time-Wiederherstellung und Geowiederherstellung für Azure Database for MariaDB. <br><br> |
| **Nachteile** | Contoso ist auf die MariaDB-Releaseversionen beschränkt, die in Azure unterstützt werden. Dies sind aktuell die Versionen 10.2 und 10.3. <br><br> Azure Database for MariaDB weist einige [Einschränkungen](https://docs.microsoft.com/azure/mariadb/concepts-limits) auf, z. B. das Herunterskalieren des Speichers. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Szenarioarchitektur](./media/contoso-migration-mariadb-to-azure/architecture.png)
_Abbildung 1: Szenarioarchitektur_

### <a name="migration-process"></a>Migrationsprozess

#### <a name="preparation"></a>Vorbereitung

Bevor Sie die MariaDB-Datenbanken migrieren können, müssen Sie sicherstellen, dass diese Instanzen alle Azure-Voraussetzungen für eine erfolgreiche Migration erfüllen.

Unterstützte Versionen:

- MariaDB verwendet das Benennungsschema „X.Y.Z“. X ist die Hauptversion, Y die Nebenversion und Z die Patchversion.
- Azure unterstützt derzeit 10.2.25 und 10.3.16.
- Upgrades für Patchupdates werden von Azure automatisch verwaltet. Beispiel: 10.2.21 auf 10.2.23. Upgrades von Neben- und Hauptversionen werden nicht unterstützt. Ein Upgrade von MariaDB 10.2 auf MariaDB 10.3 wird beispielsweise nicht unterstützt. Wenn Sie von 10.2 auf 10.3 upgraden möchten, führen Sie eine Datenbanksicherung und dann die Wiederherstellung auf einem Server aus, der mit der Engine-Zielversion erstellt wurde.

Netzwerk:

Contoso muss eine Verbindung über das Gateway des virtuellen Netzwerks zwischen der lokalen Umgebung und dem virtuellen Netzwerk einrichten, in dem sich die MariaDB-Datenbank befindet. Dadurch kann die lokale Anwendung über das Gateway auf die Datenbank zugreifen, wenn die Verbindungszeichenfolgen aktualisiert werden.

  ![Migrationsprozess](./media/contoso-migration-mariadb-to-azure/migration-process.png) _Abbildung 2: Der Migrationsprozess_

#### <a name="migration"></a>Migration

Da MariaDB sehr große Ähnlichkeit mit MySQL hat, können dieselben gängigen Hilfsprogramme und Tools wie MySQL Workbench, mysqldump, Toad oder Navicat zum Herstellen einer Verbindung und zum Migrieren von Daten zu Azure Database for MariaDB verwendet werden.

Contoso hat zum Migrieren seiner Datenbanken die folgenden Schritte ausgeführt.

- Ermitteln Sie die lokale MariaDB-Version, indem Sie die folgenden Befehle ausführen und die Ausgabe beobachten. In den meisten Fällen sollte Ihre Version in Bezug auf das Schema und die Datensicherung keine große Rolle spielen. Wenn Sie Features auf Anwendungsebene verwenden, sollten Sie sicherstellen, dass diese Anwendungen mit der Zielversion in Azure kompatibel sind.

  ```cmd
    mysql -h localhost -u root -P
  ```

  ![Migrationsprozess](./media/contoso-migration-mariadb-to-azure/mariadb_version.png)
  _Abbildung 4: Ermitteln der lokalen MariaDB-Version_

- Erstellen Sie eine neue MariaDB-Instanz in Azure:

  - Öffnen Sie das [Azure-Portal](https://portal.azure.com).
  - Wählen Sie **Ressource hinzufügen** aus.
  - Suchen Sie nach `MariaDB`.

    ![Migrationsprozess](./media/contoso-migration-mariadb-to-azure/azure-mariadb-create.png)
    _Abbildung 4: Neue MariaDB-Instanz in Azure_

  - Klicken Sie auf **Erstellen**.
  - Wählen Sie Ihr Abonnement und die Ressourcengruppe aus.
  - Wählen Sie einen Servernamen und einen Standort aus.
  - Wählen Sie die Zielversion aus (10.2 oder 10.3).
  - Wählen Sie Compute und Speicher aus.
  - Geben Sie einen Administratorbenutzername und ein Kennwort ein.
  - Klicken Sie auf **Überprüfen + erstellen**.

    ![Migrationsprozess](./media/contoso-migration-mariadb-to-azure/azure_mariadb_create.png)
    _Abbildung 5: Überprüfen und Erstellen_

  - Klicken Sie auf **Erstellen**.
  - Notieren Sie sich den Serverhostnamen, den Benutzernamen und das Kennwort.
  - Wählen Sie **Verbindungssicherheit** aus.
  - Wählen Sie **Client-IP hinzufügen** aus (die IP-Adresse, von der Sie die Datenbank anschließend wiederherstellen).
  - Wählen Sie **Speichern** aus.

- Führen Sie die folgenden Befehle aus, um die Datenbank mit dem Namen `Employees` zu exportieren. Wiederholen Sie dies für jede Datenbank:

    ```cmd
    mysqldump -h localhost -u root -p -–skip-triggers -–single-transaction –-extended-insert -–order-by-primary -–disable-keys Employees > Employees.sql
    ```

- Stellen Sie die Datenbank wieder her. Setzen Sie den Endpunkt für Ihre Azure Database for MariaDB-Instanz und den Benutzernamen ein.

  ```cmd
  mysql -h {name}.mariadb.database.azure.com -u user@{name} -p –ssl
  create database employees;
  use database employees;
  source employees.sql;
  ```

- Überprüfen Sie mithilfe von phpMyAdmin oder einem ähnlichen Tool (MySQL Workbench, Toad und Navicat), die Wiederherstellung, indem Sie die Anzahl der Datensätze in jeder Tabelle prüfen.
- Aktualisieren Sie alle Anwendungsverbindungszeichenfolgen, sodass Sie auf die migrierte Datenbank verweisen.
- Testen Sie alle Anwendungen auf ordnungsgemäßen Betrieb.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach einer überprüften erfolgreichen Migration muss Contoso die Sicherungsdateien der lokalen Datenbank zu Aufbewahrungszwecken sichern und speichern. Nehmen Sie den lokalen MariaDB-Server außer Betrieb.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neue Azure Database for MariaDB-Instanz und die Datenbanken geschützt sind. [Weitere Informationen](https://docs.microsoft.com/azure/mariadb/concepts-security)
- Contoso muss die [Firewallregeln](https://docs.microsoft.com/azure/mariadb/concepts-firewall-rules) und die Konfigurationseinstellungen des virtuellen Netzwerks überprüfen, um sicherzustellen, dass Verbindungen auf die Anwendungen beschränkt sind, die Zugriff benötigen.
- Contoso muss Anforderungen für ausgehende IP-Adressen konfigurieren, um Verbindungen mit den [Gateway-IP-Adressen](https://docs.microsoft.com/azure/mariadb/concepts-connectivity-architecture) von MariaDB zuzulassen.
- Contoso muss alle Anwendungen zur Verwendung von [SSL](https://docs.microsoft.com/azure/mariadb/concepts-ssl-connection-security)-Verbindungen mit den Datenbanken aktualisieren.
- Contoso sollte [Private Link](https://docs.microsoft.com/azure/mariadb/concepts-data-access-security-private-link) einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte [Azure Advanced Threat Protection (ATP)](https://docs.microsoft.com/azure/mariadb/concepts-data-access-and-security-threat-protection) aktivieren.
- Contoso muss die Protokollanalyse konfigurieren, um die Sicherheit zu überwachen und Warnungen zu relevanten Einträgen zu erhalten.

### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Azure Database for MariaDB-Datenbanken gesichert sind. Mit dieser Funktion können Sicherungen erstellt werden, die im Fall eines regionalen Ausfalls in einer gekoppelten Region verfügbar sind.

> [!IMPORTANT]
> Stellen Sie sicher, dass die Azure Database for MariaDB-Ressource über eine [Ressourcensperre](https://docs.microsoft.com/azure/azure-resource-manager/management/lock-resources) verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Azure Database for MariaDB kann zentral hoch- oder herunterskaliert werden. Daher ist die Leistungsüberwachung von Server und Datenbanken wichtig, um sicherzustellen, dass die Anforderungen erfüllt und gleichzeitig die Kosten möglichst gering gehalten werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Sie können zwischen verschiedenen Tarifen wählen. Achten Sie darauf, dass ein passender Tarif für die Datenworkloads ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.
- Verwenden Sie reservierte Kapazitäten, um Kosten zu sparen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso seine MariaDB-Datenbanken zu einer Azure Database for MariaDB-Instanz migriert hat.
