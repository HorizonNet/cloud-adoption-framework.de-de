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
ms.openlocfilehash: 39b9d4781b5caabed5524577be9819e4544ec665
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88567154"
---
<!-- cSpell:ignore mysqldump InnoDB binlog Navicat -->

# <a name="migrate-mysql-databases-to-azure"></a>Migrieren von MySQL-Datenbanken zu Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-MySQL-Datenbankplattform zu Azure geplant und durchgeführt hat.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte. Sie wünschen Folgendes:

- **Erhöhen der Verfügbarkeit.** Bei der lokalen MySQL-Umgebung von Contoso sind Probleme mit der Verfügbarkeit aufgetreten. Die Anwendungen, die diesen Datenspeicher nutzen, müssen für das Unternehmen zuverlässiger werden.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, um Kundenanforderungen schneller zu bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Die IT-Experten müssen schneller reagieren als die Änderungen im Marketplace geschehen, um den Erfolg in einer globalen Wirtschaft zu garantieren. IT darf nicht zum Geschäftshindernis werden.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit derselben Geschwindigkeit mitwachsen.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich folgende Ziele für die Migration gesetzt. Anhand dieser Ziele wird die beste Migrationsmethode bestimmt.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Verfügbarkeit** | Derzeit haben interne Mitarbeiter Schwierigkeiten mit der Hostingumgebung für die MySQL-Instanz. Contoso wünscht eine Verfügbarkeit der Datenbankschicht von nahezu 99,99 Prozent. |
| **Skalierbarkeit** | Die Kapazität des lokalen Datenbankhosts geht schnell zur Neige. Contoso erfordert eine Möglichkeit, seine Instanzen über die derzeitigen Beschränkungen hinaus zu skalieren oder herunterzuskalieren, wenn sich die Geschäftsumgebung ändert, um Kosten zu sparen. |
| **Leistung** | Die Personalabteilung von Contoso führt täglich, wöchentlich und monatlich verschiedene Berichte aus. Beim Ausführen dieser Berichte treten erhebliche Leistungsprobleme bei der Anwendung für die Mitarbeiter auf. Die Berichte müssen ausgeführt werden, ohne dass sich dies auf die Anwendungsleistung auswirkt. |
| **Security** | Contoso muss sicher sein, dass nur die internen Anwendungen auf die Datenbank zugreifen können und sie nicht über das Internet sichtbar oder zugänglich ist. |
| **Überwachung** | Contoso verwendet derzeit Tools zum Überwachen der Metriken des MySQL-Datenbankservers und zum Bereitstellen von Benachrichtigungen bei Auftreten von CPU-, Arbeitsspeicher- oder Speicherproblemen. Das Unternehmen möchte in Azure über dieselben Funktionen verfügen. |
| **Geschäftskontinuität** | Der Personaldatenspeicher ist ein wichtiger Teil der täglichen Abläufe bei Contoso. Die Ausfallzeit muss im Fall einer Beschädigung oder Wiederherstellung weitestgehend minimiert werden. |
| **Azure** | Contoso möchte die Anwendung in Azure verschieben, ohne dass sie auf VMs ausgeführt wird. In der Datenschicht soll auf Azure-PaaS-Dienste (Platform-as-a-Service) zurückgegriffen werden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess. Auch die für die Migration verwendeten Tools und Dienste werden identifiziert.

### <a name="current-application"></a>Aktuelle Anwendung

In der MySQL-Datenbank werden Mitarbeiterdaten gespeichert, die für alle Belange der Personalabteilung des Unternehmens verwendet werden. Eine [LAMP-basierte](https://wikipedia.org/wiki/LAMP_(software_bundle)) Anwendung wird als Front-End zum Verarbeiten von Personalanfragen der Mitarbeiter verwendet. Contoso hat 100.000 Mitarbeiter weltweit, und daher ist die Uptime wichtig.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

Verwenden von Azure Database Migration Service, um die Datenbank zu einer Azure Database for MySQL-Instanz zu migrieren Ändern aller Anwendungen und Prozesse, damit sie die neue Azure Database for MySQL-Instanz verwenden.

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

<!-- TODO: Verify GraphDBMS term -->
<!-- docsTest:ignore ColumnStore GraphDBMS -->

Im Rahmen des Lösungsentwurfs hat Contoso die in Azure verfügbaren Features für das Hosting der MySQL-Daten geprüft. Die folgenden Überlegungen haben dabei im Unternehmen zu der Entscheidung für Azure geführt:

- Ähnlich wie Azure SQL-Datenbank unterstützt auch Azure Database for MySQL [Firewallregeln](/azure/mysql/concepts-firewall-rules).
- Azure Database for MySQL kann mit [Azure Virtual Network](/azure/mysql/concepts-data-access-and-security-vnet) verwendet werden, um zu verhindern, dass die Instanz öffentlich zugänglich ist.
- Azure Database for MySQL verfügt über die erforderlichen Compliance- und Datenschutzzertifizierungen, die Contoso für seine Prüfer einhalten muss.
- Die Verarbeitungsleistung für Berichte und Anwendung wird durch die Verwendung von Lesereplikaten verbessert.
- Der Dienst kann mithilfe von [Azure Private Link](/azure/mysql/concepts-data-access-security-private-link) nur für den internen Netzwerkdatenverkehr (kein öffentlicher Zugriff) verfügbar gemacht werden.
- Contoso hat entschieden, nicht zu Azure Database for MySQL zu wechseln, da möglicherweise in Zukunft das MariaDB ColumnStore- und GraphDBMS-Datenbankmodell verwendet werden soll.
- Abgesehen von den MySQL-Features ist Contoso ein Befürworter echter Open-Source-Projekte und entscheidet sich gegen den Einsatz von MySQL.
- Die [Bandbreite und Wartezeit](/azure/vpn-gateway/vpn-gateway-about-vpngateways) zwischen der Anwendung und der Datenbank ist je nach ausgewähltem Gateway (Azure ExpressRoute oder Site-to-Site-VPN) ausreichend.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
| --- | --- |
| **Vorteile** | Azure Database for MySQL bietet eine finanziell abgesicherte Vereinbarung zum Service Level (SLA) von 99,99 Prozent für [Hochverfügbarkeit](/azure/mysql/concepts-high-availability). <br><br> Azure bietet die Möglichkeit, während Spitzenladezeiten jedes Quartal zentral hoch- oder herunterzuskalieren. Contoso kann durch den Kauf von [reservierter Kapazität](/azure/mysql/concept-reserved-pricing) noch weitere Einsparungen erzielen. <br><br> Azure bietet Funktionen zur Point-in-Time-Wiederherstellung und Geowiederherstellung für Azure Database for MySQL. <br><br> |
| **Nachteile** | Contoso ist auf die MySQL-Releaseversionen beschränkt, die in Azure unterstützt werden. Dies sind aktuell die Versionen 10.2 und 10.3. <br><br> Azure Database for MySQL weist einige [Einschränkungen](/azure/mysql/concepts-limits) auf, z. B. das Herunterskalieren des Speichers. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Diagramm mit der Szenarioarchitektur.](./media/contoso-migration-mysql-to-azure/architecture.png)
_Abbildung 1: Szenarioarchitektur_

### <a name="migration-process"></a>Migrationsprozess

#### <a name="preparation"></a>Vorbereitung

Bevor Sie die MySQL-Datenbanken migrieren können, müssen Sie sicherstellen, dass diese Instanzen alle Azure-Voraussetzungen für eine erfolgreiche Migration erfüllen.

#### <a name="supported-versions"></a>Unterstützte Versionen

MySQL verwendet das Schema X.Y.Z für die Versionsverwaltung. Beispiel: X ist die Hauptversion, Y die Nebenversion und Z die Patchversion.

Azure unterstützt derzeit 10.2.25 und 10.3.16.

Upgrades für Patchupdates werden von Azure automatisch verwaltet. Beispiele sind 10.2.21 bis 10.2.23. Upgrades von Neben- und Hauptversionen werden nicht unterstützt. Ein Upgrade von MySQL 10.2 auf MySQL 10.3 wird beispielsweise nicht unterstützt. Wenn Sie von 10.2 auf 10.3 upgraden möchten, führen Sie eine Sicherung und dann die Wiederherstellung auf einem Server aus, der mit der neuen Engine-Version erstellt wurde.

#### <a name="network"></a>Netzwerk

Contoso muss eine Verbindung über das Gateway des virtuellen Netzwerks zwischen der lokalen Umgebung und dem virtuellen Netzwerk einrichten, in dem sich die MySQL-Datenbank befindet. Durch diese Verbindung kann die lokale Anwendung über das Gateway auf die Datenbank zugreifen, wenn die Verbindungszeichenfolgen aktualisiert werden.

![Diagramm zum Migrationsprozess.](./media/contoso-migration-mysql-to-azure/migration-process.png)
_Abbildung 2: Der Migrationsvorgang._

#### <a name="migration"></a>Migration

Die Administratoren von Contoso migrieren die Datenbank mithilfe von Azure Database Migration Service, indem sie die Schritte im [ausführlichen Migrationstutorial](/azure/dms/tutorial-mysql-azure-mysql-online) befolgen. Sie können Online-, Offline- und Hybridmigrationen (Vorschauversion) von MySQL 5.6 oder 5.7 ausführen.

> [!NOTE]
> MySQL 8.0 wird in Azure Database for MySQL unterstützt. Das Database Migration Service-Tool unterstützt diese Version noch nicht.

Zusammenfassend müssen die folgenden Aufgaben durchgeführt werden:

- Sicherstellen, dass alle Voraussetzungen für die Migration erfüllt sind:
  - Die Version der Quelle des MySQL-Datenbankservers muss mit der Version übereinstimmen, die von Azure Database for MySQL unterstützt wird. Azure Database for MySQL unterstützt die MySQL Community Edition, die InnoDB-Speicher-Engine sowie die Migration zwischen Quellen und Zielen mit derselben Version.
  - Aktivieren Sie die binäre Protokollierung in `my.ini` (Windows) oder `my.cnf` (Unix). Wenn die binäre Protokollierung nicht aktiviert wird, führt dies zu folgendem Fehler im Migrations-Assistenten: „Fehler bei der binären Protokollierung. Die Variable binlog_row_image weist den Wert 'minimal' auf. Ändern Sie diesen in 'full'.“ Weitere Informationen finden Sie auf der [MySQL-Website](https://go.microsoft.com/fwlink/?linkid=873009`).
  - Der Benutzer muss über die `ReplicationAdmin`-Rolle verfügen.
  - Migrieren Sie die Datenbankschemas ohne Fremdschlüssel und Trigger.
- Erstellen Sie ein virtuelles Netzwerk, das über ExpressRoute oder VPN mit Ihrem lokalen Netzwerk verbunden ist.
- Erstellen Sie eine Azure Database Migration Service-Instanz mit einer `Premium`-SKU, die mit dem virtuellen Netzwerk verbunden ist.
- Vergewissern Sie sich, dass die Instanz über das virtuelle Netzwerk auf die MySQL-Datenbank zugreifen kann. Stellen Sie sicher, dass alle eingehenden Ports von Azure zu MySQL auf der virtuellen Netzwerkebene, dem Netzwerk-VPN und dem Computer, auf dem MySQL gehostet ist, zugelassen werden.
- Erstellen Sie ein neues Database Migration Service-Projekt:

  ![Der Screenshot zeigt die Erstellung eines neuen Database Migration Service-Projekts](./media/contoso-migration-mysql-to-azure/migration-dms-new-project.png)
  _Abbildung 3: Azure Database Migration Service-Projekt._

#### <a name="migration-by-using-native-tools"></a>Migration mithilfe nativer Tools

Als Alternative zur Verwendung von Azure Database Migration Service kann Contoso gängige Hilfsprogramme und Tools wie MySQL Workbench, mysqldump, Toad oder Navicat zum Herstellen einer Verbindung und zum Migrieren von Daten zu Azure Database for MySQL verwenden.

- Sichern und Wiederherstellen mit mysqldump:
  - Verwenden Sie die Option „exclude-triggers“ in mysqldump. Dadurch wird verhindert, dass Trigger während des Imports ausgeführt werden, und so die Leistung verbessert.
  - Verwenden Sie die Option „single-transaction“, um den Übersetzungsisolationsmodus auf `REPEATABLE READ` festzulegen und eine SQL-Anweisung vom Typ `START TRANSACTION` vor dem Verwerfen von Daten zu senden.
  - Verwenden Sie die Option „disable-keys“ in mysqldump, um vor dem Laden Fremdschlüsseleinschränkungen zu deaktivieren. Das Entfernen von Einschränkungen führt zu Leistungsverbesserungen.
  - Verwenden Sie Azure Blob Storage zum Speichern der Sicherungsdateien, und führen Sie die Wiederherstellung von dort aus, um den Vorgang zu beschleunigen.
  - Aktualisieren Sie die Anwendungsverbindungszeichenfolgen.
  - Nachdem die Datenbank migriert ist, muss Contoso die Verbindungszeichenfolgen so aktualisieren, dass sie auf die neue Azure Database for MySQL-Datenbank verweisen.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die lokale Datenbank zwecks Aufbewahrung sichern und den lokalen MySQL-Datenbankserver außer Betrieb nehmen.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Contoso muss Folgendes durchführen:

- Sicherstellen, dass die neue Azure Database for MySQL-Instanz und die Datenbanken geschützt sind. Weitere Informationen finden Sie unter [Sicherheit in Azure Database for MySQL](/azure/mysql/concepts-security).
- Die Konfiguration der Firewall und des virtuellen Netzwerks überprüfen.
- Contoso sollte Private Link einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte Azure Advanced Threat Protection aktivieren.

### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung sicherstellen, dass die Azure Database for MySQL-Instanzen gesichert sind. Auf diese Weise können im Falle eines regionalen Ausfalls Sicherungen in Regionspaaren verwendet werden.

> [!IMPORTANT]
> Stellen Sie sicher, dass die Azure Database for MySQL-Ressource über eine Ressourcensperre verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Azure Database for MySQL kann hoch- und herunterskaliert werden. Die Überwachung der Leistung von Server und Datenbanken ist wichtig, um sicherzustellen, dass die Anforderungen erfüllt und gleichzeitig die Kosten minimiert werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Es sind verschiedene Tarife verfügbar. Achten Sie darauf, dass ein passender Tarif für jede Datenworkload ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.
- Verwenden Sie reservierte Kapazitäten, um Kosten zu sparen.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso seine MySQL-Datenbanken zu einer Azure Database for MySQL-Instanz migriert hat.
