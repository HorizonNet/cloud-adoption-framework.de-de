---
title: Migrieren von PostgreSQL-Datenbanken zu Microsoft Azure
description: Hier erfahren Sie, wie Contoso seine lokalen PostgreSQL-Datenbanken zu Azure migriert hat.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: b279577e4be2e841e0e2ae5700ec2833882cb56d
ms.sourcegitcommit: 26aee3c6f596bb8a9f1e16af93cdf94e41a61dee
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87400495"
---
<!-- cSpell:ignore BYOK postgres psql dvdrental -->

# <a name="migrate-postgresql-databases-to-microsoft-azure"></a>Migrieren von PostgreSQL-Datenbanken zu Microsoft Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-PostgreSQL-Datenbankplattform zu Azure geplant und durchgeführt hat.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte. Sie wünschen Folgendes:

- **Automatisieren von Big Data.** Contoso verwendet PostgreSQL für verschiedene Big Data- und KI-Initiativen. Das Unternehmen benötigt skalierbare wiederholbare Pipelines, um viele dieser analytischen Workloads zu automatisieren.
- **Effizienzsteigerung.** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein und darf weder Geld noch Zeit verschwenden, um Kundenanforderungen schneller zu bearbeiten.
- **Steigerung der Flexibilität.** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Sie muss schneller reagieren als Veränderungen im Markt geschehen und darf nicht zum Geschäftshindernis werden, um in der globalen Wirtschaft erfolgreich zu sein.
- **Skalierung.** Da das Unternehmen erfolgreich wächst, muss die IT-Abteilung von Contoso Systeme bereitstellen, die mit der gleichen Geschwindigkeit mitwachsen können.
- **Sicherheit erhöhen.** Contoso ist sich bewusst, dass die lokale Strategie des Unternehmens aufgrund gesetzlicher Überwachungs-, Protokollierungs- und Konformitätsanforderungen angepasst werden muss.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich Ziele für die Migration gesetzt, anhand derer es die beste Migrationsmethode bestimmen wird.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Upgrades** | Contoso möchte sicherstellen, dass neue Patches sofort installiert werden, wenn sie verfügbar sind, das Unternehmen möchte diese Updates aber nicht verwalten. |
| **Integrationen** | Contoso möchte die Daten in der Datenbank in Daten- und KI-Pipelines für maschinelles Lernen integrieren. |
| **Sichern und Wiederherstellen** | Contoso möchte in der Lage sein, Zeitpunktwiederherstellungen durchzuführen, wenn Fehler bei Datenaktualisierungen auftreten oder diese aus irgendeinem Grund beschädigt sind. |
| **Azure** | Contoso möchte das System überwachen und basierend auf der Leistung und Sicherheit Warnungen auslösen. |
| **Leistung** | In einigen Fällen müssen parallele Datenverarbeitungspipelines in unterschiedlichen geografischen Regionen verwendet und Daten aus diesen Regionen gelesen werden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess. Auch die für die Migration verwendeten Tools und Dienste werden identifiziert.

### <a name="current-environment"></a>Aktuelle Umgebung

PostgreSQL 9.6.7 wird auf einem physischen Linux-Computer (`sql-pg-01.contoso.com`) im Rechenzentrum von Contoso ausgeführt. Contoso verfügt bereits über ein Azure-Abonnement mit einem virtuellen Site-to-Site-Gateway zum lokalen Netzwerk des Rechenzentrums.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Verwenden von Azure Database Migration Service, um die Datenbank zu einer Azure Database for PostgreSQL-Instanz zu migrieren
- Ändern aller Anwendungen und Prozesse zur Verwendung der neuen Azure Database for PostgreSQL-Instanz
- Erstellen einer neuen Datenverarbeitungspipeline mit Azure Data Factory, die eine Verbindung mit der Azure Database for PostgreSQL-Instanz herstellt

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso die in Azure verfügbaren Features für das Hosting der PostgreSQL-Daten geprüft. Die folgenden Überlegungen haben dabei im Unternehmen zu der Entscheidung für Azure geführt:

- Ähnlich wie Azure SQL-Datenbank unterstützt auch Azure Database for PostgreSQL Firewallregeln.
- Azure Database for PostgreSQL kann mit virtuellen Netzwerken verwendet werden, um zu verhindern, dass die Instanz öffentlich zugänglich ist.
- Azure Database for PostgreSQL verfügt über die erforderlichen Compliancezertifizierungen, die Contoso einhalten muss.
- Die Integration in DevOps und Azure Data Factory ermöglicht die Erstellung automatisierter Datenverarbeitungspipelines.
- Die Verarbeitungsleistung kann durch die Verwendung von Lesereplikaten verbessert werden.
- Bring Your Own Key (BYOK) wird für die Datenverschlüsselung unterstützt.
- Der Dienst kann mithilfe von Azure Private Link nur für den internen Netzwerkdatenverkehr (kein öffentlicher Zugriff) verfügbar gemacht werden.
- Die [Bandbreite und Wartezeit](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) zwischen der Anwendung und der Datenbank ist je nach ausgewähltem Gateway (Azure ExpressRoute oder Site-to-Site-VPN) ausreichend.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso bewertet den vorgeschlagen Entwurf anhand einer Liste mit Vor- und Nachteilen.

| Aspekt | Details |
|--- | --- |
| **Vorteile** | Alle derzeit erforderlichen und verwendeten Features sind in Azure Database for PostgreSQL verfügbar. <br><br> |
| **Nachteile** | Contoso muss trotzdem eine manuelle Migration von der Hauptversion von PostgreSQL durchführen. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Diagramm der Szenarioarchitektur.](./media/contoso-migration-postgresql-to-azure/architecture.png)

_Abbildung 1: Szenarioarchitektur_

### <a name="migration-process"></a>Migrationsprozess

#### <a name="preparation"></a>Vorbereitung

Bevor Contoso seine PostgreSQL-Datenbanken migrieren kann, muss sichergestellt sein, dass seine Instanzen alle Azure-Voraussetzungen für eine erfolgreiche Migration erfüllen.

#### <a name="supported-versions"></a>Unterstützte Versionen

Es werden nur Migrationen zur gleichen oder einer höheren Version unterstützt. Beispielsweise wird die Migration von PostgreSQL 9.5 zu Azure Database for PostgreSQL 9.6 oder 10 unterstützt, aber nicht die Migration von PostgreSQL 11 zu PostgreSQL 9.6.

Microsoft strebt in Azure Database for PostgreSQL (Einzelserver) die Unterstützung von _n-2_-Versionen der PostgreSQL-Engine an. Das bedeutet, dass die aktuelle Hauptversion in Azure (_n_) und die beiden vorherigen Hauptversionen ( _-2_) unterstützt werden.

Aktuelle Informationen zu unterstützten Versionen finden Sie unter [Unterstützte PostgreSQL-Hauptversionen](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions).

> [!NOTE]
> Automatische Upgrades von Hauptversionen werden nicht unterstützt. Es erfolgt beispielsweise kein automatisches Upgrade von PostgreSQL 9.5 auf PostgreSQL 9.6. Um ein Upgrade auf die nächste Hauptversion durchzuführen, erstellen Sie eine Sicherung der Datenbank, und stellen Sie sie auf einem Server wieder her, der mit der neuen Engine-Version erstellt wurde.

#### <a name="network"></a>Netzwerk

Contoso muss eine Verbindung über das Gateway des virtuellen Netzwerks zwischen der lokalen Umgebung und dem virtuellen Netzwerk einrichten, in dem sich die Azure Database for PostgreSQL-Datenbank befindet. Mithilfe dieser Verbindung kann die lokale Anwendung auf die Datenbank zugreifen, wird aber nicht zur Cloud migriert.

#### <a name="assessment"></a>Bewertung

Contoso muss die aktuelle Datenbank auf Replikationsprobleme überprüfen. Folgendes muss u. a. überprüft werden:

- Die Version der Quelldatenbank muss für die Migration zur Zieldatenbankversion kompatibel sein.
- In allen zu replizierenden Tabellen müssen Primärschlüssel vorhanden sein.
- Datenbanknamen dürfen kein Semikolon (`;`) enthalten.
- Die Migration mehrerer Tabellen mit demselben Namen und unterschiedlicher Groß-/Kleinschreibung kann zu unvorhersehbarem Verhalten führen.

  ![Diagramm zum Migrationsprozess](./media/contoso-migration-postgresql-to-azure/migration-process.png)
  _Abbildung 2: Der Migrationsvorgang._

#### <a name="migration"></a>Migration

Contoso stehen zum Durchführen der Migration verschiedene Optionen zur Verfügung:

- [Sichern und Wiederherstellen](https://docs.microsoft.com/azure/postgresql/howto-migrate-using-dump-and-restore)
- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)
- [Import/Export](https://docs.microsoft.com/azure/postgresql/howto-migrate-using-export-and-import)

Contoso hat sich für die Verwendung von Azure Database Migration Service entschieden, damit das Migrationsprojekt für Upgrades der Hauptversion wiederverwendet werden kann. Da eine einzelne Database Migration Service-Aktivität maximal vier Datenbanken unterstützt, richtet Contoso mithilfe der folgenden Schritte mehrere Aufträge ein.

Zur Vorbereitung wird ein virtuelles Netzwerk eingerichtet, um auf die Datenbank zuzugreifen. Zum Erstellen einer virtuellen Netzwerkverbindung mit [VPN-Gateways](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) stehen mehrere Methoden zur Auswahl.

<!-- docsTest:ignore "Azure Database Migration Services" -->

### <a name="create-an-azure-database-migration-service-instance"></a>Erstellen einer Instanz von Azure Database Migration Service

1. Wählen Sie im [Azure-Portal](https://portal.azure.com) die Option **Ressource erstellen** aus.
1. Suchen Sie nach **Azure Database Migration Service**, und wählen Sie den Eintrag aus.
1. Wählen Sie **+ Hinzufügen**.
1. Wählen Sie das Abonnement und die Ressourcengruppe für den Dienst aus.
1. Geben Sie einen Namen für die Instanz ein.
1. Wählen Sie den Standort aus, der dem Contoso-Rechenzentrum oder dem VPN-Gateway am nächsten ist.
1. Wählen Sie als Dienstmodus **Azure** aus.
1. Wählen Sie einen Tarif.
1. Klicken Sie auf **Überprüfen + erstellen**.

    ![Screenshot des Bildschirms zum Erstellen des Migrationsdiensts](./media/contoso-migration-postgresql-to-azure/azure_migration_service_create.png)
    _Abbildung 3: Überprüfen und erstellen_

1. Klicken Sie auf **Erstellen**.

### <a name="create-an-azure-database-for-postgresql-instance"></a>Erstellen einer Azure Database for PostgreSQL-Instanz

1. Konfigurieren Sie auf dem lokalen Server die Datei `postgresql.conf`.

1. Konfigurieren Sie den Server zum Lauschen an der IP-Adresse, die Azure Database Migration Service für den Zugriff auf den Server und die Datenbanken verwendet.
    - Legen Sie die Variable `listen_addresses` fest.
1. Aktivieren Sie SSL.
    1. Legen Sie die Variable `ssl=on` fest.
    1. Überprüfen Sie, ob Contoso für den Server ein öffentlich signiertes SSL-Zertifikat verwendet, das TLS 1.2 unterstützt. Andernfalls gibt das Database Migration Service-Tool einen Fehler aus.
1. Aktualisieren Sie die `pg_hba.conf`-Datei.
    - Fügen Sie spezifische Einträge für die Database Migration Service-Instanz hinzu.
1. Die logische Replikation muss auf dem Quellserver aktiviert werden, indem die Werte in der Datei `postgresql.conf` für jeden Server geändert werden.
    1. `wal_level` = `logical`
    1. `max_replication_slots` = [mindestens die maximale Anzahl von Datenbanken für die Migration]
        - Wenn Contoso beispielsweise vier Datenbanken migrieren möchte, muss der Wert auf 4 festgelegt werden.
    1. `max_wal_senders` = [Anzahl gleichzeitig ausgeführter Datenbanken]
        - Der empfohlene Wert ist 10.

1. Der `User` der Migration muss über die Rolle `REPLICATION` für die Quelldatenbank verfügen.

1. Fügen Sie die IP-Adresse der Database Migration Service-Instanz der Datei `PostgreSQLpg_hba.conf` hinzu.

1. Zum Exportieren der Datenbankschemas sind folgende Befehle auszuführen:

    ```cmd
    pg_dump -U postgres -s dvdrental > dvdrental_schema.sql
    ```

1. Kopieren Sie die Datei, verwenden Sie für die Kopie den Namen `dvdrental_schema_foreign.sql`, und entfernen Sie alle Elemente, die sich nicht auf Fremdschlüssel und Auslöser beziehen.
1. Entfernen Sie alle Elemente, die sich auf Fremdschlüssel und Auslöser beziehen, aus der Datei `dvdrental_schema.sql`.

1. Importieren Sie das Datenbankschema (Schritt 1):

      ```cmd
        psql -h {host}.postgres.database.azure.com -d dvdrental -U username -f dvdrental_schema.sql
      ```

### <a name="migration"></a>Migration

1. Im Azure-Portal navigiert Contoso zu seiner Database Migration Service-Ressource.
1. Wenn der Dienst nicht gestartet wird, wählen Sie **Dienst starten** aus.
1. Wählen Sie **Neues Migrationsprojekt** aus.

    ![Screenshot: Option „Neues Migrationsprojekt“ hervorgehoben](./media/contoso-migration-postgresql-to-azure/azure_migration_service_new_project.png)

    _Abbildung 4: Starten einer neuen Migration_

1. Wählen Sie **Neue Aktivität** > **Onlinedatenmigration** aus.
1. Geben Sie einen Namen ein.
1. Wählen Sie **PostgreSQL** als Quelle aus.
1. Wählen Sie als Ziel **Azure Database for PostgreSQL** und anschließend **Speichern** aus.

    ![Screenshot mit dem Bereich „Neues Migrationsprojekt“](./media/contoso-migration-postgresql-to-azure/azure_migration_service_new_project02.png)

    _Abbildung 5: Ein neues Migrationsprojekt ist hervorgehoben._

1. Geben Sie die Quellinformationen ein, und wählen Sie **Speichern** aus.

    ![Screenshot: Eingeben von Quellinformationen](./media/contoso-migration-postgresql-to-azure/azure_migration_service_source.png)
    _Abbildung 6: Eingeben der Quellinformationen_

1. Geben Sie die Zielinformationen ein, und wählen Sie **Speichern** aus.

    ![Screenshot: Auswählen von Zielinformationen](./media/contoso-migration-postgresql-to-azure/azure_migration_service_target.png)
    _Abbildung 7: Auswählen der Zielinformationen_

1. Wählen Sie die zu migrierenden Datenbanken aus. Das Schema für jede Datenbank sollte zuvor migriert worden sein. Klicken Sie dann auf **Speichern**.

    ![Screenshot: Auswählen von Datenbanken](./media/contoso-migration-postgresql-to-azure/azure_migration_service_db.png)
    _Abbildung 8: Auswählen von Datenbanken_

1. Konfigurieren Sie die erweiterten Einstellungen, und wählen Sie anschließend **Speichern**.

    ![Screenshot: Konfigurieren erweiterter Einstellungen](./media/contoso-migration-postgresql-to-azure/azure_migration_service_advanced.png)
    _Abbildung 9: Konfigurieren der erweiterten Einstellungen_

1. Geben Sie einen Namen für die Aktivität ein, und wählen Sie **Ausführen** aus.

    ![Screenshot: Benennen und Ausführen der Aktivität](./media/contoso-migration-postgresql-to-azure/azure_migration_service_summary.png)
    _Abbildung 10: Benennen und Ausführen der Aktivität_

1. Überwachen der Migration Wiederholen Sie den Vorgang, wenn ein Fehler auftritt. Dies kann etwa der Fall sein, wenn Fremdschlüsselverweise fehlen.
1. Wenn `Full load completed` der Anzahl Ihrer Tabellen entspricht, wählen Sie **Starten der Übernahme** aus.

    ![Screenshot: Überwachen der Migration, um die Übernahme zu starten](./media/contoso-migration-postgresql-to-azure/azure_migration_service_complete.png)
    _Abbildung 11: Überwachen der Migration, um die Übernahme zu starten_

1. Beenden Sie alle Transaktionen vom Quellserver.
1. Aktivieren Sie das Kontrollkästchen **Bestätigen**, und wählen Sie dann **Anwenden** aus.

    ![Screenshot: Ausführen der Übernahme](./media/contoso-migration-postgresql-to-azure/azure_migration_service_cutover.png)
    _Abbildung 12: Ausführen der Übernahme_

1. Warten Sie, bis die Übernahme abgeschlossen ist.

    ![Screenshot: Abschließen der Übernahme](./media/contoso-migration-postgresql-to-azure/azure_migration_service_finished.png)
    _Abbildung 13: Abschließen der Übernahme_

      > [!NOTE]
      > Die vorherigen Schritte in Database Migration Service können auch über die [Azure-Befehlszeilenschnittstelle (Azure CLI)](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online) ausgeführt werden.
    
1. Importieren Sie das Datenbankschema (Schritt 2):

      ```cmd
        psql -h {host}.postgres.database.azure.com -d dvdrental -U username -f dvdrental_schema_foreign.sql
      ```

1. Konfigurieren Sie alle Anwendungen oder Prozesse neu, die über die lokale Datenbank auf die neue Azure Database for PostgreSQL-Datenbankinstanz verweisen.

1. Nach der Migration stellt Contoso sicher, dass bei Bedarf auch regionsübergreifende Lesereplikate eingerichtet werden, nachdem die Migration abgeschlossen ist.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die lokale Datenbank zwecks Aufbewahrung sichern und den alten PostgreSQL-Server im Rahmen des Bereinigungsprozesses außer Betrieb nehmen.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso seine neue Infrastruktur vollständig operationalisieren und schützen.

### <a name="security"></a>Sicherheit

Contoso muss Folgendes durchführen:

- Sicherstellen, dass die neue Azure Database for PostgreSQL-Instanz und die Datenbanken geschützt sind. Weitere Informationen finden Sie unter [Sicherheit in Azure Database for PostgreSQL – Einzelserver](https://docs.microsoft.com/azure/postgresql/concepts-security).
- Die [Firewallregeln](https://docs.microsoft.com/azure/postgresql/concepts-firewall-rules) und die Konfigurationseinstellungen des virtuellen Netzwerks überprüfen, um sicherzustellen, dass Verbindungen auf die Anwendungen beschränkt sind, die Zugriff benötigen.
- Contoso sollte für die Datenverschlüsselung [BYOK](https://docs.microsoft.com/azure/postgresql/concepts-data-encryption-postgresql) implementieren.
- Contoso muss alle Anwendungen zur Verwendung von [SSL](https://docs.microsoft.com/azure/postgresql/concepts-ssl-connection-security)-Verbindungen mit den Datenbanken aktualisieren.
- Contoso sollte [Private Link](https://docs.microsoft.com/azure/postgresql/concepts-data-access-and-security-private-link) einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte [Azure Advanced Threat Protection (ATP)](https://docs.microsoft.com/azure/postgresql/concepts-data-access-and-security-threat-protection) aktivieren.
- Contoso sollte die Protokollanalyse konfigurieren, um die Sicherheit sowie relevante Einträge zu überwachen und Warnungen zu erhalten.

### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Azure Database for PostgreSQL-Datenbanken gesichert sind. Auf diese Weise können im Falle eines regionalen Ausfalls Sicherungen in Regionspaaren verwendet werden.

> [!IMPORTANT]
> Stellen Sie sicher, dass die Azure Database for PostgreSQL-Ressource über eine Ressourcensperre verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Azure Database for PostgreSQL kann hoch- und herunterskaliert werden. Die Leistungsüberwachung des Servers und der Datenbanken ist wichtig, um sicherzustellen, dass alle Anforderungen erfüllt sind und die Kosten so gering wie möglich gehalten werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Sie können zwischen verschiedenen Tarifen wählen. Achten Sie darauf, dass ein passender Tarif für die Datenworkloads ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso seine PostgreSQL-Datenbanken zu einer Azure Database for PostgreSQL-Instanz migriert hat.
