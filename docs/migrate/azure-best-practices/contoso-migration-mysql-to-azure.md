---
title: Migrieren von MySQL-Datenbanken zu Azure
description: In diesem Artikel erfahren Sie, wie Contoso seine lokalen MySQL-Datenbanken zu Azure migriert hat.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: a23b0355fab1f921935f109ce77c0fd79d49cda5
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86233612"
---
<!-- cSpell:ignore mysqldump InnoDB binlog Navicat -->

# <a name="migrate-mysql-databases-to-azure"></a>Migrieren von MySQL-Datenbanken zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-MySQL-Datenbankplattform zu Azure geplant und durchgeführt hat.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Erhöhen der Verfügbarkeit.** Bei der lokalen MySQL-Umgebung von Contoso sind Probleme mit der Verfügbarkeit aufgetreten. Die Anwendungen, die diesen Datenspeicher nutzen, müssen für das Unternehmen zuverlässiger werden.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, um Kundenanforderungen schneller zu bearbeiten.
- **Steigerung der Flexibilität.**  Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. IT darf nicht zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

| Anforderungen | Details |
| --- | --- |
| **Verfügbarkeit** | Derzeit haben interne Mitarbeiter Schwierigkeiten mit der Hostingumgebung für die MySQL-Instanz. Contoso wünscht eine Verfügbarkeit der Datenbankschicht von nahezu 99,99 Prozent. |
| **Skalierbarkeit** | Der lokale Datenbankhost weist schnell keine Kapazität mehr auf, und Contoso braucht eine Möglichkeit, die Instanzen über die aktuellen Einschränkungen hinaus zu skalieren oder zentral herunterzuskalieren, wenn sich die Geschäftsumgebung ändert, um so Kosten zu sparen. |
| **Leistung** | Die Personalabteilung von Contoso führt täglich, wöchentlich und monatlich verschiedene Berichte aus. Beim Ausführen dieser Berichte treten erhebliche Leistungsprobleme bei der Anwendung für die Mitarbeiter auf. Die Berichte müssen ausgeführt werden, ohne dass sich dies auf die Anwendungsleistung auswirkt. |
| **Sicherheit** | Contoso muss sicher sein, dass nur die internen Anwendungen auf die Datenbank zugreifen können und sie nicht über das Internet sichtbar oder zugänglich ist. |
| **Überwachung** | Contoso verwendet derzeit Tools zum Überwachen der Metriken des MySQL-Datenbankservers und zum Bereitstellen von Benachrichtigungen bei Auftreten von CPU-, Arbeitsspeicher- oder Speicherproblemen. Dieselben Möglichkeiten sollen auch in Azure bereitstehen. |
| **Geschäftskontinuität** | Der Personaldatenspeicher ist ein wichtiger Bestandteil der täglichen Abläufe bei Contoso und die Ausfallzeit im Fall einer Beschädigung oder Wiederherstellung soll auf ein Minimum reduziert werden. |
| **Azure** | Contoso möchte die Anwendung in Azure verschieben, ohne dass sie auf VMs ausgeführt wird. In der Datenschicht soll auf Azure-PaaS-Dienste zurückgegriffen werden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und überprüft Contoso eine Bereitstellungslösung und identifiziert den Migrationsprozess sowie die für die Migration genutzten Tools und Dienste.

### <a name="current-application"></a>Aktuelle Anwendung

In der MySQL-Datenbank werden Mitarbeiterdaten gespeichert, die für alle Belange der Personalabteilung des Unternehmens verwendet werden. Eine [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung wird als Front-End zum Verarbeiten von Personalanfragen der Mitarbeiter verwendet. Contoso hat 100.000 Mitarbeiter weltweit, und daher ist die Betriebszeit sehr wichtig.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

Verwenden von Azure Database Migration Service, um die Datenbank zu einer Azure Database for MySQL-Instanz zu migrieren, und Ändern aller Anwendungen und Prozesse, damit die neue Azure Database for MySQL-Instanz verwendet wird.

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

<!-- TODO: Verify GraphDBMS term -->
<!-- docsTest:ignore ColumnStore GraphDBMS -->

Im Rahmen des Lösungsentwurfs hat Contoso die in Azure verfügbaren Features für das Hosting der MySQL-Daten des Unternehmens geprüft. Die folgenden Überlegungen waren ausschlaggebend für die Entscheidung für Azure.

- Ähnlich wie Azure SQL-Datenbank unterstützt auch Azure Database for MySQL [Firewallregeln](https://docs.microsoft.com/azure/mysql/concepts-firewall-rules).
- Azure Database for MySQL kann mit [Azure Virtual Network](https://docs.microsoft.com/azure/mysql/concepts-data-access-and-security-vnet) verwendet werden, um zu verhindern, dass die Instanz öffentlich zugänglich ist.
- Azure Database for MySQL verfügt über die erforderlichen Compliance- und Datenschutzzertifizierungen, die Contoso für die Prüfer einhalten muss.
- Die Verarbeitungsleistung für Berichte und Anwendung kann durch die Verwendung von Lesereplikaten verbessert werden.
- Der Dienst kann mithilfe von [Private Link](https://docs.microsoft.com/azure/mysql/concepts-data-access-security-private-link) nur für den internen Netzwerkdatenverkehr (kein öffentlicher Zugriff) verfügbar gemacht werden.
- Das Unternehmen hat entschieden, nicht zu Azure Database for MySQL zu wechseln, da möglicherweise in Zukunft das MariaDB ColumnStore- und GraphDBMS-Datenbankmodell verwendet werden soll.
- Abgesehen von den MySQL-Features ist Contoso ein großer Befürworter echter Open-Source-Projekte und entscheidet sich gegen den Einsatz von MySQL.
- Die [Bandbreite und Latenz](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) zwischen der Anwendung und der Datenbank ist je nach ausgewähltem Gateway (ExpressRoute oder Site-to-Site-VPN) ausreichend.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Azure Database for MySQL bietet eine finanziell abgesicherte Vereinbarung zum Service Level (SLA) von 99,99 Prozent für [Hochverfügbarkeit](https://docs.microsoft.com/azure/mysql/concepts-high-availability). <br><br> Azure bietet die Möglichkeit, während Spitzenladezeiten jedes Quartal zentral hoch- oder herunterzuskalieren. Contoso kann durch den Kauf von [reservierter Kapazität](https://docs.microsoft.com/azure/mysql/concept-reserved-pricing) noch weitere Einsparungen erzielen. <br><br> Azure bietet Funktionen zur Point-in-Time-Wiederherstellung und Geowiederherstellung für Azure Database for MySQL. <br><br> |
| **Nachteile** | Contoso ist auf die MySQL-Releaseversionen beschränkt, die in Azure unterstützt werden. Dies sind aktuell die Versionen 10.2 und 10.3. <br><br> Azure Database for MySQL weist einige [Einschränkungen](https://docs.microsoft.com/azure/mysql/concepts-limits) auf, z. B. das Herunterskalieren des Speichers. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Szenarioarchitektur](./media/contoso-migration-mysql-to-azure/architecture.png)
_Abbildung 1: Szenarioarchitektur_

### <a name="migration-process"></a>Migrationsprozess

#### <a name="preparation"></a>Vorbereitung

Bevor Sie die MySQL-Datenbanken migrieren können, müssen Sie sicherstellen, dass diese Instanzen alle Azure-Voraussetzungen für eine erfolgreiche Migration erfüllen.

#### <a name="supported-versions"></a>Unterstützte Versionen

MySQL verwendet das Schema `X.Y.Z` für die Versionsverwaltung. `X` ist die Hauptversion, `Y` die Nebenversion und `Z` die Patchversion.

Azure unterstützt derzeit 10.2.25 und 10.3.16.

Upgrades für Patchupdates werden von Azure automatisch verwaltet. Beispiel: 10.2.21 auf 10.2.23. Upgrades von Neben- und Hauptversionen werden nicht unterstützt. Ein Upgrade von MySQL 10.2 auf MySQL 10.3 wird beispielsweise nicht unterstützt. Wenn Sie von 10.2 auf 10.3 upgraden möchten, führen Sie eine Sicherung und dann die Wiederherstellung auf einem Server aus, der mit der neuen Engine-Version erstellt wurde.

#### <a name="network"></a>Netzwerk

Contoso muss eine Verbindung über das Gateway des virtuellen Netzwerks zwischen der lokalen Umgebung und dem virtuellen Netzwerk einrichten, in dem sich die MySQL-Datenbank befindet. Dadurch kann die lokale Anwendung über das Gateway auf die Datenbank zugreifen, wenn die Verbindungszeichenfolgen aktualisiert werden.

![Migrationsprozess](./media/contoso-migration-mysql-to-azure/migration-process.png)
_Abbildung 2: Der Migrationsprozess_

#### <a name="migration"></a>Migration

Die Administratoren von Contoso migrieren die Datenbank mithilfe von Azure Database Migration Service anhand des [Schritt-für-Schritt-Tutorials für die Migration](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online). Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) von MySQL 5.6 oder 5.7 ausführen.

> [!NOTE]
> MySQL 8.0 wird in Azure Database for MySQL unterstützt, aber das Database Migration Service-Tool unterstützt diese Version noch nicht.

Zusammenfassend müssen die folgenden Schritte ausgeführt werden:

- Sicherstellen, dass alle Voraussetzungen für die Migration erfüllt sind:

  - Die Version der Quelle des MySQL-Datenbankservers muss mit der Version übereinstimmen, die von Azure Database for MySQL unterstützt wird. Azure Database for MySQL unterstützt die MySQL Community-Edition, die InnoDB-Speicher-Engine und die Migration zwischen Quelle und Ziel derselben Version.
  - Aktivieren Sie die binäre Protokollierung in `my.ini` (Windows) oder `my.cnf` (Unix). Tun Sie das nicht, verursacht dies den folgenden Fehler beim Migrations-Assistenten: `Error in binary logging. Variable binlog_row_image has value 'minimal'. Please change it to 'full'. For more information, see https://go.microsoft.com/fwlink/?linkid=873009`.
  - Der Benutzer muss über die `ReplicationAdmin`-Rolle verfügen.
  - Migrieren Sie die Datenbankschemas ohne Fremdschlüssel und Trigger.

- Erstellen Sie ein virtuelles Netzwerk, das über ExpressRoute oder VPN mit Ihrem lokalen Netzwerk verbunden ist.

- Erstellen Sie eine Azure Database Migration Service-Instanz mit einer `Premium`-SKU, die mit dem VNET verbunden ist.

- Vergewissern Sie sich, dass die Instanz über das virtuelle Netzwerk auf die MySQL-Datenbank zugreifen kann. Dazu gehört auch, sicherzustellen, dass alle eingehenden Ports von Azure zu MySQL auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem MySQL gehostet ist, zugelassen werden.

- Erstellen Sie ein neues Database Migration Service-Projekt:

  ![Erstellen eines neuen Database Migration Service-Projekts](./media/contoso-migration-mysql-to-azure/migration-dms-new-project.png)
  _Abbildung 3: Azure-Projekt zur Datenbankmigration_

#### <a name="migration-using-native-tools"></a>Migration mithilfe nativer Tools

Als Alternative zur Verwendung von Azure Database Migration Service kann Contoso gängige Hilfsprogramme und Tools wie MySQL Workbench, mysqldump, Toad oder Navicat zum Herstellen einer Verbindung und zum Migrieren von Daten zu Azure Database for MySQL verwenden.

- Sichern und Wiederherstellen mit mysqldump:
  - Verwenden Sie die Option „exclude-triggers“ in mysqldump. Dadurch wird verhindert, dass Trigger während des Imports ausgeführt werden, und so die Leistung verbessert.
  - Verwenden Sie die Option „single-transaction“, um den Übersetzungsisolationsmodus auf `REPEATABLE READ` zu setzen und eine SQL-Anweisung vom Typ `START TRANSACTION` vor dem Sichern von Daten zu senden.
  - Verwenden Sie die Option „disable-keys“ in mysqldump, um vor dem Laden Fremdschlüsseleinschränkungen zu deaktivieren. Wenn Sie diese entfernen, werden Leistungssteigerungen erzielt.
  - Verwenden Sie Azure Blob Storage zum Speichern der Sicherungsdateien, und führen Sie die Wiederherstellung von dort aus, um den Vorgang zu beschleunigen.
  - Aktualisieren Sie die Anwendungsverbindungszeichenfolgen.
  - Nachdem die Datenbank migriert wurde, muss Contoso die Verbindungszeichenfolgen so aktualisieren, dass sie auf die neue Azure Database for MySQL-Datenbank verweisen.

## <a name="cleanup-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die lokale Datenbank zwecks Aufbewahrung sichern und den lokalen MySQL-Datenbankserver außer Betrieb nehmen.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neue Azure Database for MySQL-Instanz und die Datenbanken geschützt sind. Weitere Informationen finden Sie unter [Sicherheit in Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/concepts-security).
- Insbesondere sollte Contoso die Konfiguration der Firewall und des virtuellen Netzwerks überprüfen.
- Contoso sollte Private Link einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte Azure Advanced Threat Protection aktivieren.

### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Azure Database for MySQL-Instanzen gesichert sind. Mit dieser Funktion können Sicherungen erstellt werden, die im Fall eines regionalen Ausfalls in einer gekoppelten Region verfügbar sind.

> [!IMPORTANT]
> Stellen Sie sicher, dass die Azure Database for MySQL-Ressource über eine Ressourcensperre verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Azure Database for MySQL kann zentral hoch- oder herunterskaliert werden. Daher ist die Überwachung der Leistung von Server und Datenbanken wichtig, um sicherzustellen, dass die Anforderungen erfüllt und gleichzeitig die Kosten minimiert werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Es sind verschiedene Tarife verfügbar. Achten Sie darauf, dass ein passender Tarif für jede Datenworkload ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.
- Verwenden Sie reservierte Kapazitäten, um Kosten zu sparen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso seine MySQL-Datenbanken zu einer Azure Database for MySQL-Instanz migriert hat.
