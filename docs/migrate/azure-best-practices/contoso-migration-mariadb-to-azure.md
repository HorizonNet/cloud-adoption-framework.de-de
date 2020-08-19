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
ms.openlocfilehash: 4cc1aeed8df6c546722ac70977e08f6619f41f21
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88570741"
---
<!-- TODO: Verify GraphDBMS term -->
<!-- cSpell:ignore ColumnStore GraphDBMS mysqldump Navicat phpMyAdmin -->

# <a name="migrate-mariadb-databases-to-azure"></a>Migrieren von MariaDB-Datenbanken zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-MariaDB-Datenbankplattform zu Azure geplant und durchgeführt hat.

Contoso verwendet aus folgenden Gründen MariaDB anstelle von MySQL:

- Unzählige Speicher-Engines.
- Cache- und Indexleistung.
- Open-Source-Unterstützung mit Features und Erweiterungen.
- Analytics ColumnStore-Unterstützung.

Das Migrationsziel des Unternehmens ist es, MariaDB weiterhin zu verwenden, ohne sich Gedanken über die Verwaltung der dafür benötigten Umgebung zu machen.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte. Sie wünschen Folgendes:

- **Erhöhen der Verfügbarkeit.** Bei der lokalen MariaDB-Umgebung von Contoso sind Probleme mit der Verfügbarkeit aufgetreten. Die Anwendungen, die diesen Datenspeicher nutzen, müssen für das Unternehmen zuverlässiger werden.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, um Kundenanforderungen schneller zu bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. IT darf nicht im Weg stehen oder zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit derselben Geschwindigkeit mitwachsen.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Verfügbarkeit** | Derzeit haben interne Mitarbeiter Schwierigkeiten mit der Hostingumgebung für die MariaDB-Instanz. Contoso wünscht eine Verfügbarkeit der Datenbankschicht von nahezu 99,99 Prozent. |
| **Skalierbarkeit** | Die Kapazität des lokalen Datenbankhosts geht schnell zur Neige. Contoso erfordert eine Möglichkeit, seine Instanzen über die derzeitigen Beschränkungen hinaus zu skalieren oder herunterzuskalieren, wenn sich die Geschäftsumgebung ändert, um Kosten zu sparen. |
| **Leistung** | Die Personalabteilung von Contoso muss täglich, wöchentlich und monatlich mehrere Berichte ausführen. Beim Ausführen dieser Berichte werden erhebliche Leistungsprobleme bei der Anwendung für die Mitarbeiter festgestellt. Die Berichte müssen ausgeführt werden, ohne dass sich dies auf die Anwendungsleistung auswirkt. |
| **Security** | Contoso muss sicher sein, dass nur die internen Anwendungen auf die Datenbank zugreifen können und sie nicht über das Internet sichtbar oder zugänglich ist. |
| **Überwachung** | Contoso verwendet derzeit Tools zum Überwachen der Metriken der MariaDB-Datenbank und zum Bereitstellen von Benachrichtigungen bei Auftreten von CPU-, Arbeitsspeicher- oder Speicherproblemen. Das Unternehmen möchte in Azure über dieselben Funktionen verfügen. |
| **Geschäftskontinuität** | Der Personaldatenspeicher ist ein wichtiger Teil der täglichen Abläufe bei Contoso. Die Ausfallzeit muss im Fall einer Beschädigung oder Wiederherstellung minimiert werden. |
| **Azure** | Contoso möchte die Anwendung in Azure verschieben, ohne dass sie auf VMs ausgeführt wird. In den Anforderungen von Contoso ist angegeben, dass in der Datenschicht auf Azure-PaaS-Dienste (Platform-as-a-Service) zurückgegriffen werden soll. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess. Auch die für die Migration verwendeten Tools und Dienste werden identifiziert.

### <a name="current-application"></a>Aktuelle Anwendung

In der MariaDB-Datenbank werden Mitarbeiterdaten gehostet, die für alle Belange der Personalabteilung des Unternehmens verwendet werden. Eine [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung wird als Front-End zum Verarbeiten von Personalanfragen der Mitarbeiter verwendet. Contoso hat 100.000 Mitarbeiter weltweit, und daher ist die Betriebszeit für die Datenbanken wichtig.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Bewerten der Umgebungen hinsichtlich Migrationskompatibilität.
- Verwenden gängiger Open-Source-Tools zum Migrieren von Datenbanken zur Azure Database for MariaDB-Instanz.
- Ändern aller Anwendungen und Prozesse, damit sie die neue Azure Database for MariaDB-Instanz verwenden.

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso die in Azure verfügbaren Features für das Hosting der MariaDB-Datenbanken geprüft. Die folgenden Überlegungen haben dabei im Unternehmen zu der Entscheidung für Azure geführt:

- Ähnlich wie Azure SQL-Datenbank unterstützt auch Azure Database for MariaDB [Firewallregeln](/azure/mariadb/concepts-firewall-rules).
- Azure Database for MariaDB kann mit [Azure Virtual Network](/azure/mariadb/concepts-data-access-security-vnet) verwendet werden, um zu verhindern, dass die Instanz öffentlich zugänglich ist.
- Azure Database for MariaDB verfügt über die erforderlichen Compliance- und Datenschutzzertifizierungen, die Contoso für seine Prüfer einhalten muss.
- Die Verarbeitungsleistung für Berichte und Anwendung wird durch die Verwendung von Lesereplikaten verbessert.
- Der Dienst kann mithilfe von [Azure Private Link](/azure/mariadb/concepts-data-access-security-private-link) nur für den internen Netzwerkdatenverkehr (kein öffentlicher Zugriff) verfügbar gemacht werden.
- Contoso hat entschieden, nicht zu Azure Database for MySQL zu wechseln, da möglicherweise in Zukunft das MariaDB ColumnStore- und GraphDBMS-Datenbankmodell verwendet werden soll.
- Die [Bandbreite und Wartezeit](/azure/vpn-gateway/vpn-gateway-about-vpngateways) zwischen der Anwendung und der Datenbank ist je nach ausgewähltem Gateway (Azure ExpressRoute oder Site-to-Site-VPN) ausreichend.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Azure Database for MariaDB bietet eine finanziell abgesicherte Vereinbarung zum Service Level (SLA) von 99,99 Prozent für [Hochverfügbarkeit](/azure/mariadb/concepts-high-availability). <br><br> Azure bietet die Möglichkeit, während Spitzenladezeiten jedes Quartal zentral hoch- oder herunterzuskalieren. Contoso kann durch den Kauf von [reservierter Kapazität](/azure/mariadb/concept-reserved-pricing) noch weitere Einsparungen erzielen. <br><br> Azure bietet Funktionen zur Point-in-Time-Wiederherstellung und Geowiederherstellung für Azure Database for MariaDB. <br><br> |
| **Nachteile** | Contoso ist auf die MariaDB-Releaseversionen beschränkt, die in Azure unterstützt werden. Dies sind aktuell die Versionen 10.2 und 10.3. <br><br> Azure Database for MariaDB weist einige [Einschränkungen](/azure/mariadb/concepts-limits) auf, z. B. das Herunterskalieren des Speichers. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Diagramm mit der Szenarioarchitektur.](./media/contoso-migration-mariadb-to-azure/architecture.png)
_Abbildung 1: Szenarioarchitektur_

### <a name="migration-process"></a>Migrationsprozess

#### <a name="preparation"></a>Vorbereitung

Bevor Sie die MariaDB-Datenbanken migrieren können, müssen Sie sicherstellen, dass diese Instanzen alle Azure-Voraussetzungen für eine erfolgreiche Migration erfüllen.

Unterstützte Versionen:

- MariaDB verwendet das Benennungsschema „X.Y.Z“. Beispiel: X ist die Hauptversion, Y die Nebenversion und Z die Patchversion.
- Azure unterstützt derzeit 10.2.25 und 10.3.16.
- Upgrades für Patchupdates werden von Azure automatisch verwaltet. Beispiele sind 10.2.21 bis 10.2.23. Upgrades von Neben- und Hauptversionen werden nicht unterstützt. Ein Upgrade von MariaDB 10.2 auf MariaDB 10.3 wird beispielsweise nicht unterstützt. Wenn Sie von 10.2 auf 10.3 upgraden möchten, führen Sie eine Datenbanksicherung und dann die Wiederherstellung auf einem Server aus, der mit der Engine-Zielversion erstellt wurde.

Netzwerk:

Contoso muss eine Verbindung über das Gateway des virtuellen Netzwerks zwischen der lokalen Umgebung und dem virtuellen Netzwerk einrichten, in dem sich die MariaDB-Datenbank befindet. Durch diese Verbindung kann die lokale Anwendung über das Gateway auf die Datenbank zugreifen, wenn die Verbindungszeichenfolgen aktualisiert werden.

  ![Diagramm zum Migrationsprozess.](./media/contoso-migration-mariadb-to-azure/migration-process.png)
  _Abbildung 2: Der Migrationsvorgang._

#### <a name="migration"></a>Migration

Da MariaDB große Ähnlichkeit mit MySQL hat, kann Contoso dieselben gängigen Hilfsprogramme und Tools wie MySQL Workbench, mysqldump, Toad oder Navicat zum Herstellen einer Verbindung und zum Migrieren von Daten zu Azure Database for MariaDB verwenden.

Contoso hat zum Migrieren seiner Datenbanken die folgenden Schritte ausgeführt.

- Ermitteln Sie die lokale MariaDB-Version, indem Sie die folgenden Befehle ausführen und die Ausgabe beobachten. In den meisten Fällen sollte Ihre Version in Bezug auf das Schema und die Datensicherung keine große Rolle spielen. Wenn Sie Features auf Anwendungsebene verwenden, stellen Sie sicher, dass diese Anwendungen mit der Zielversion in Azure kompatibel sind.

  ```cmd
    mysql -h localhost -u root -P
  ```

  ![Screenshot zum Ermitteln der lokalen MariaDB-Version.](./media/contoso-migration-mariadb-to-azure/mariadb_version.png)
  _Abbildung 3: Ermitteln der lokalen MariaDB-Version_

- Erstellen Sie eine neue MariaDB-Instanz in Azure:

  - Öffnen Sie das [Azure-Portal](https://portal.azure.com).
  - Wählen Sie **Ressource hinzufügen** aus.
  - Suchen Sie nach `MariaDB`.

    ![Screenshot zeigt eine neue MariaDB-Instanz in Azure.](./media/contoso-migration-mariadb-to-azure/azure-mariadb-create.png)
    _Abbildung 4: Neue MariaDB-Instanz in Azure_

  - Klicken Sie auf **Erstellen**.
  - Wählen Sie Ihr Abonnement und die Ressourcengruppe aus.
  - Wählen Sie einen Servernamen und einen Standort aus.
  - Wählen Sie Ihre Zielversion aus (10.2 oder 10.3).
  - Wählen Sie Compute und Speicher aus.
  - Geben Sie einen Administratorbenutzername und ein Kennwort ein.
  - Klicken Sie auf **Überprüfen + erstellen**.

    ![Screenshot zeigt den Bildschirm zum Erstellen des MariaDB-Servers.](./media/contoso-migration-mariadb-to-azure/azure_mariadb_create.png)
    _Abbildung 5: Überprüfen und Erstellen_

  - Klicken Sie auf **Erstellen**.
  - Notieren Sie sich den Serverhostnamen, den Benutzernamen und das Kennwort.
  - Wählen Sie **Verbindungssicherheit** aus.
  - Wählen Sie **Client-IP hinzufügen** aus (die IP-Adresse, von der aus Sie die Datenbank wiederherstellen).
  - Wählen Sie **Speichern** aus.

- Führen Sie die folgenden Befehle aus, um die Datenbank mit dem Namen `Employees` zu exportieren. Wiederholen Sie dies für jede Datenbank:

    ```cmd
    mysqldump -h localhost -u root -p -–skip-triggers -–single-transaction –-extended-insert -–order-by-primary -–disable-keys Employees > Employees.sql
    ```

- Stellen Sie die Datenbank wieder her. Setzen Sie den Endpunkt für Ihre Azure Database for MariaDB-Instanz und den Benutzernamen ein:

  ```cmd
  mysql -h {name}.mariadb.database.azure.com -u user@{name} -p –ssl
  create database employees;
  use database employees;
  source employees.sql;
  ```

- Überprüfen Sie mithilfe von phpMyAdmin oder einem ähnlichen Tool (z. B. MySQL Workbench, Toad und Navicat) die Wiederherstellung, indem Sie die Anzahl der Datensätze in jeder Tabelle prüfen.
- Aktualisieren Sie alle Anwendungsverbindungszeichenfolgen, sodass Sie auf die migrierte Datenbank verweisen.
- Testen Sie alle Anwendungen auf ordnungsgemäßen Betrieb.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach einer überprüften erfolgreichen Migration muss Contoso die Sicherungsdateien der lokalen Datenbank zu Aufbewahrungszwecken sichern und speichern. Nehmen Sie den lokalen MariaDB-Server außer Betrieb.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Contoso muss Folgendes durchführen:

- Sicherstellen, dass die neue Azure Database for MariaDB-Instanz und die Datenbanken geschützt sind. Weitere Informationen finden Sie unter [Sicherheit in Azure Database for MariaDB](/azure/mariadb/concepts-security).
- Die [Firewallregeln](/azure/mariadb/concepts-firewall-rules) und die Konfigurationseinstellungen des virtuellen Netzwerks überprüfen, um sicherzustellen, dass Verbindungen auf die Anwendungen beschränkt sind, die Zugriff benötigen.
- Contoso muss Anforderungen für ausgehende IP-Adressen konfigurieren, um Verbindungen mit den [Gateway-IP-Adressen](/azure/mariadb/concepts-connectivity-architecture) von MariaDB zuzulassen.
- Contoso muss alle Anwendungen zur Verwendung von [SSL](/azure/mariadb/concepts-ssl-connection-security)-Verbindungen mit den Datenbanken aktualisieren.
- Contoso sollte [Private Link](/azure/mariadb/concepts-data-access-security-private-link) einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte [Azure Advanced Threat Protection (ATP)](/azure/mariadb/concepts-data-access-and-security-threat-protection) aktivieren.
- Die Protokollanalyse konfigurieren, um die Sicherheit sowie relevante Einträge zu überwachen und Warnungen zu senden.

### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Azure Database for MariaDB-Datenbanken gesichert sind. Auf diese Weise können im Falle eines regionalen Ausfalls Sicherungen in Regionspaaren verwendet werden.

> [!IMPORTANT]
> Stellen Sie sicher, dass die Azure Database for MariaDB-Ressource über eine [Ressourcensperre](/azure/azure-resource-manager/management/lock-resources) verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Azure Database for MariaDB kann hoch- und herunterskaliert werden. Die Leistungsüberwachung des Servers und der Datenbanken ist wichtig, um sicherzustellen, dass Ihre Anforderungen erfüllt und die Kosten so gering wie möglich gehalten werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Sie können zwischen verschiedenen Tarifen wählen. Achten Sie darauf, dass ein passender Tarif für die Datenworkloads ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.
- Verwenden Sie reservierte Kapazitäten, um Kosten zu sparen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso seine MariaDB-Datenbanken zu einer Azure Database for MariaDB-Instanz migriert hat.
