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
ms.openlocfilehash: 8de202b5f6f8f0420541792898bf609360e79d28
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86199108"
---
<!-- cSpell:ignore BYOK postgres psql dvdrental -->

# <a name="migrate-postgresql-databases-to-microsoft-azure"></a>Migrieren von PostgreSQL-Datenbanken zu Microsoft Azure

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso die Migration seiner lokalen Open-Source-PostgreSQL-Datenbankplattform zu Azure geplant und durchgeführt hat.

## <a name="business-drivers"></a>Business-Treiber

Das IT Leadership-Team hat eng mit den Geschäftspartnern zusammengearbeitet, um zu verstehen, was das Unternehmen mit dieser Migration erreichen möchte:

- **Big Data:** Contoso verwendet PostgreSQL für mehrere Big Data- und KI-Initiativen und möchte skalierbare wiederholbare Pipelines erstellen, um einen Großteil dieser Analyseworkloads zu automatisieren.
- **Steigerung der Effizienz:** Contoso muss unnötige Verfahren beseitigen und Prozesse für Entwickler und Benutzer optimieren. Die IT-Abteilung muss schnell sein, weder Geld noch Zeit verschwenden und Kundenanforderungen schneller bearbeiten.
- **Steigerung der Flexibilität:** Die Contoso-IT-Abteilung muss schneller auf die Unternehmensanforderungen reagieren. Sie muss in der Lage sein, schneller zu reagieren als Veränderungen im Markt geschehen, und darf nicht zum Geschäftshindernis werden, um in der globalen Wirtschaft erfolgreich zu sein.
- **Skalierung**: Da das Unternehmen erfolgreich wächst, muss die Contoso-IT Systeme bereitstellen, die mit der gleichen Geschwindigkeit wachsen können.
- **Erhöhte Sicherheit:** Contoso ist sich bewusst, dass die lokale Strategie des Unternehmens aufgrund gesetzlicher Überwachungs-, Protokollierungs- und Konformitätsanforderungen angepasst werden muss.

## <a name="migration-goals"></a>Migrationsziele

Das Cloudteam von Contoso hat sich Ziele für die Migration gesetzt, anhand derer es die beste Migrationsmethode bestimmen wird.

| Requirements (Anforderungen) | Details |
| --- | --- |
| **Upgrades** | Contoso möchte sicherstellen, dass neue Patches sofort installiert werden, möchte diese Updates aber nicht verwalten. |
| **Integrationen** | Contoso möchte die Daten in der Datenbank in Daten- und KI-Pipelines für Machine Learning integrieren. |
| **Sichern und Wiederherstellen** | Contoso möchte in der Lage sein, Zeitpunktwiederherstellungen durchzuführen, wenn Datenaktualisierungen fehlschlagen oder aus irgendeinem Grund beschädigt werden. |
| **Azure** | Contoso möchte in der Lage sein, das System zu überwachen und basierend auf der Leistung und Sicherheit Warnungen auszulösen. |
| **Leistung** | In einigen Fällen müssen parallele Datenverarbeitungspipelines in unterschiedlichen geografischen Regionen verwendet und Daten aus diesen Regionen gelesen werden. |

## <a name="solution-design"></a>Lösungsentwurf

Nachdem die Ziele und Anforderungen formuliert wurden, entwirft und prüft Contoso eine Bereitstellungslösung und bestimmt den Migrationsprozess sowie die für die Migration genutzten Tools und Dienste.

### <a name="current-environment"></a>Aktuelle Umgebung

PostgreSQL 9.6.7 wird auf einem physischen Linux-Computer (`sql-pg-01.contoso.com`) im Rechenzentrum von Contoso ausgeführt. Contoso hat bereits ein Azure-Abonnement mit einem virtuellen Site-to-Site-Gateway zum lokalen Netzwerk des Rechenzentrums.

### <a name="proposed-solution"></a>Vorgeschlagene Lösung

- Verwenden von Azure Database Migration Service, um die Datenbank zu einer Azure Database for PostgreSQL-Instanz zu migrieren
- Ändern aller Anwendungen und Prozesse zur Verwendung der neuen Azure Database for PostgreSQL-Instanz
- Erstellen einer neuen Datenverarbeitungspipeline mit Azure Data Factory, die eine Verbindung mit der Azure Database for PostgreSQL-Instanz herstellt

### <a name="database-considerations"></a>Überlegungen zu Datenbanken

Im Rahmen des Lösungsentwurfs hat Contoso die in Azure verfügbaren Features für das Hosting der PostgreSQL-Daten geprüft. Die folgenden Überlegungen haben dabei zu der Entscheidung für Azure geführt.

- Ähnlich wie Azure SQL-Datenbank unterstützt auch Azure Database for PostgreSQL Firewallregeln.
- Azure Database for PostgreSQL kann mit virtuellen Netzwerken verwendet werden, um zu verhindern, dass die Instanz öffentlich zugänglich ist.
- Azure Database for PostgreSQL verfügt über die erforderlichen Compliancezertifizierungen, die Contoso einhalten muss.
- Die Integration in DevOps und Azure Data Factory ermöglicht die Erstellung automatisierter Datenverarbeitungspipelines.
- Die Verarbeitungsleistung kann durch die Verwendung von Lesereplikaten verbessert werden.
- Bring Your Own Key (BYOK) wird für die Datenverschlüsselung unterstützt.
- Der Dienst kann mithilfe von Private Link nur für den internen Netzwerkdatenverkehr (kein öffentlicher Zugriff) verfügbar gemacht werden.
- Die [Bandbreite und Wartezeit](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) zwischen der Anwendung und der Datenbank ist je nach ausgewähltem Gateway (ExpressRoute oder Site-to-Site-VPN) ausreichend.

### <a name="solution-review"></a>Überprüfung der Lösung

Contoso wertet den vorgeschlagen Entwurf durch Erstellen einer Liste mit Vor- und Nachteilen aus.

| Aspekt | Details |
|--- | --- |
| **Vorteile** | Alle derzeit erforderlichen und verwendeten Features sind in Azure Database for PostgreSQL verfügbar. <br><br> |
| **Nachteile** | Contoso muss trotzdem eine manuelle Migration von der Hauptversion von PostgreSQL durchführen. |

## <a name="proposed-architecture"></a>Vorgeschlagene Architektur

![Szenarioarchitektur](./media/contoso-migration-postgresql-to-azure/architecture.png)
_Abbildung 1: Szenarioarchitektur_

### <a name="migration-process"></a>Migrationsprozess

#### <a name="preparation"></a>Vorbereitung

Bevor Sie Ihre PostgreSQL-Datenbanken migrieren können, müssen Sie sicherstellen, dass diese Instanzen alle Azure-Voraussetzungen für eine erfolgreiche Migration erfüllen.

#### <a name="supported-versions"></a>Unterstützte Versionen

Es werden nur Migrationen zur gleichen oder einer höheren Version unterstützt. Beispielsweise wird die Migration von PostgreSQL 9.5 zu Azure Database for PostgreSQL 9.6 oder 10 unterstützt, aber nicht die Migration von PostgreSQL 11 zu PostgreSQL 9.6.

Microsoft strebt in Azure Database for PostgreSQL (Einzelserver) die Unterstützung von _n-2_-Versionen der PostgreSQL-Engine an. Das bedeutet, dass die aktuelle Hauptversion in Azure (_n_) und die beiden vorherigen Hauptversionen ( _-2_) unterstützt werden.

Die aktuellen Updates für unterstützte Versionen finden Sie [hier](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions).

> [!NOTE]
> Automatische Upgrades von Hauptversionen werden nicht unterstützt. Es erfolgt beispielsweise kein automatisches Upgrade von PostgreSQL 9.5 auf PostgreSQL 9.6. Um ein Upgrade auf die nächste Hauptversion durchzuführen, erstellen Sie eine Sicherung der Datenbank, und stellen Sie sie auf einem Server wieder her, der mit der neuen Engine-Version erstellt wurde.

#### <a name="network"></a>Netzwerk

Contoso muss eine Verbindung über das Gateway des virtuellen Netzwerks zwischen der lokalen Umgebung und dem virtuellen Netzwerk einrichten, in dem sich die Azure Database for PostgreSQL-Datenbank befindet. Dadurch kann die lokale Anwendung auf die Datenbank zugreifen, wird aber nicht zur Cloud migriert.

#### <a name="assessment"></a>Bewertung

Contoso muss die aktuelle Datenbank auf Replikationsprobleme überprüfen. Folgendes muss u. a. überprüft werden:

- Die Version der Quelldatenbank muss für die Migration zur Zieldatenbankversion kompatibel sein.
- In allen zu replizierenden Tabellen müssen Primärschlüssel vorhanden sein.
- Datenbanknamen dürfen kein Semikolon (`;`) enthalten.
- Die Migration mehrerer Tabellen mit demselben Namen aber unterschiedlicher Groß-/Kleinschreibung kann zu unvorhersehbarem Verhalten führen.

  ![Migrationsprozess](./media/contoso-migration-postgresql-to-azure/migration-process.png)
  _Abbildung 2: Migrationsprozess_

#### <a name="migration"></a>Migration

Contoso stehen zum Durchführen der Migration die folgenden Optionen zur Verfügung:

- [Sichern und Wiederherstellen](https://docs.microsoft.com/azure/postgresql/howto-migrate-using-dump-and-restore)

- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)

- [Import/Export](https://docs.microsoft.com/azure/postgresql/howto-migrate-using-export-and-import)

Contoso hat sich für die Verwendung von Azure Database Migration Service entschieden, damit das Migrationsprojekt für Upgrades der Hauptversion wiederverwendet werden kann. Da eine einzelne Database Migration Service-Aktivität maximal vier Datenbanken unterstützt, richtet Contoso anhand der folgenden Schritte mehrere Aufträge ein:

Richten Sie zur Vorbereitung ein virtuelles Netzwerk (VNET) ein, um auf die Datenbank zuzugreifen. Zum Erstellen einer VNET-Verbindung mit [VPN-Gateways](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) stehen mehrere Methoden zur Auswahl.

<!-- docsTest:ignore "Azure Database Migration Services" -->

- Erstellen Sie eine Azure Database Migration Service-Instanz:
  - Wählen Sie im [Azure-Portal](https://portal.azure.com) die Option **Ressource erstellen** aus.
  - Suchen Sie nach **Azure Database Migration Service**, und wählen Sie den Eintrag aus.
  - Wählen Sie **+ Hinzufügen**.
  - Wählen Sie das Abonnement und die Ressourcengruppe für den Dienst aus.
  - Geben Sie einen Namen für die Instanz ein.
  - Wählen Sie den Standort aus, der Ihrem Rechenzentrum oder VPN-Gateway am nächsten ist.
  - Wählen Sie als Dienstmodus **Azure** aus.
  - Wählen Sie einen Tarif.
  - Klicken Sie auf **Überprüfen + erstellen**.

    ![Migrationsprozess](./media/contoso-migration-postgresql-to-azure/azure_migration_service_create.png)
    _Abbildung 3: Überprüfen und erstellen_

  - Klicken Sie auf **Erstellen**.

- Erstellen Sie eine Azure Database for PostgreSQL-Instanz.

- Konfigurieren Sie auf dem lokalen Server die Datei `postgresql.conf`.

  - Konfigurieren Sie den Server zum Lauschen an der IP-Adresse, die Azure Database Migration Service für den Zugriff auf den Server und die Datenbanken verwendet.
    - Legen Sie die Variable `listen_addresses` fest.
  - Aktivieren Sie SSL.
    - Legen Sie die Variable `ssl=on` fest.
    - Vergewissern Sie sich, dass Sie für den Server ein öffentlich signiertes SSL-Zertifikat verwenden, das TLS 1.2 unterstützt. Andernfalls gibt das Database Migration Service-Tool einen Fehler aus.
  - Aktualisieren Sie die `pg_hba.conf`-Datei.
    - Fügen Sie spezifische Einträge für die Database Migration Service-Instanz hinzu.
  - Die logische Replikation muss auf dem Quellserver aktiviert werden, indem die Werte in der Datei `postgresql.conf` für jeden Server geändert werden.
    - `wal_level` = `logical`
    - `max_replication_slots` = [mindestens die maximale Anzahl von Datenbanken für die Migration]
      - Wenn Sie z. B. vier Datenbanken migrieren möchten, legen Sie den Wert auf 4 fest.
    - `max_wal_senders` = [Anzahl gleichzeitig ausgeführter Datenbanken]
      - Der empfohlene Wert ist 10.

- Der `User` der Migration muss über die Rolle `REPLICATION` für die Quelldatenbank verfügen.

- Fügen Sie die IP-Adresse der Database Migration Service-Instanz der Datei `PostgreSQLpg_hba.conf` hinzu.

- Exportieren Sie die Datenbankschemas.

  - Führen Sie die folgenden Befehle aus:

    ```cmd
    pg_dump -U postgres -s dvdrental > dvdrental_schema.sql
    ```

  - Kopieren Sie die Datei, verwenden Sie für die Kopie den Namen `dvdrental_schema_foreign.sql`, und entfernen Sie alle Elemente, die sich nicht auf Fremdschlüssel und Auslöser beziehen.
  - Entfernen Sie alle Elemente, die sich auf Fremdschlüssel und Auslöser beziehen, aus der Datei `dvdrental_schema.sql`.

- Importieren Sie das Datenbankschema (Schritt 1):

  ```cmd
    psql -h {host}.postgres.database.azure.com -d dvdrental -U username -f dvdrental_schema.sql
    ```

- Migration:

  - Navigieren Sie im Azure-Portal zu Ihrer Database Migration Service-Ressource.
  - Wenn der Dienst nicht ausgeführt wird, wählen Sie **Dienst starten** aus.
  - Wählen Sie **Neues Migrationsprojekt** aus.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_new_project.png)
    _Abbildung 4: Starten einer neuen Migration_

  - Wählen Sie **Neue Aktivität** > **Onlinedatenmigration** aus.
  - Geben Sie einen Namen ein.
  - Wählen Sie **PostgreSQL** als Quelle aus.
  - Wählen Sie als Ziel **Azure Database for PostgreSQL** aus.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_new_project02.png)
    _Abbildung 5: Ein neues Migrationsprojekt ist hervorgehoben._

  - Wählen Sie **Speichern** aus.
  - Geben Sie die Quellinformationen ein.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_source.png)
    _Abbildung 6: Eingeben der Quellinformationen_

  - Wählen Sie **Speichern** aus.
  - Geben Sie die Zielinformationen ein.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_target.png)
    _Abbildung 7: Auswählen der Zielinformationen_

  - Wählen Sie **Speichern** aus.
  - Wählen Sie die Datenbanken aus, die Sie migrieren möchten. Das Schema für jede Datenbank sollte zuvor migriert worden sein.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_db.png)
    _Abbildung 8: Auswählen von Datenbanken_

  - Wählen Sie **Speichern** aus.
  - Konfigurieren Sie die erweiterten Einstellungen.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_advanced.png)
    _Abbildung 9: Konfigurieren der erweiterten Einstellungen_

  - Wählen Sie **Speichern** aus.
  - Geben Sie einen Namen für die Aktivität ein, und wählen Sie **Ausführen** aus.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_summary.png)
    _Abbildung 10: Benennen und Ausführen der Aktivität_

  - Überwachen der Migration Wenn ein Fehler auftritt, müssen Sie es ggf. nochmal versuchen (z. B. wenn Fremdschlüsselverweise fehlen).
  - Wenn der Wert unter `Full load completed` der Anzahl Ihrer Tabellen entspricht, wählen Sie **Starten der Übernahme** aus.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_complete.png)
    _Abbildung 11: Überwachen der Migration, um die Übernahme zu starten_

  - Beenden Sie alle Transaktionen vom Quellserver.
  - Aktivieren Sie das Kontrollkästchen **Bestätigen**, und wählen Sie dann **Anwenden** aus.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_cutover.png)
    _Abbildung 12: Ausführen der Übernahme_

  - Warten Sie, bis die Übernahme abgeschlossen ist.

    ![„Neues Migrationsprojekt“ ist hervorgehoben.](./media/contoso-migration-postgresql-to-azure/azure_migration_service_finished.png)
    _Abbildung 13: Abschließen der Übernahme_

  > [!NOTE]
  > Die obigen Schritte in Database Migration Service können auch über die [Azure-Befehlszeilenschnittstelle (Azure CLI)](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online) ausgeführt werden.

- Importieren Sie das Datenbankschema (Schritt 2):

  ```cmd
    psql -h {host}.postgres.database.azure.com -d dvdrental -U username -f dvdrental_schema_foreign.sql
    ```

- Konfigurieren Sie alle Anwendungen oder Prozesse neu, die über die lokale Datenbank auf die neue Azure Database for PostgreSQL-Datenbankinstanz verweisen.

- Stellen Sie nach der Migration ggf. sicher, dass regionsübergreifende Lesereplikate eingerichtet sind.

## <a name="clean-up-after-migration"></a>Bereinigung nach der Migration

Nach der Migration muss Contoso die lokale Datenbank zwecks Aufbewahrung sichern und den alten PostgreSQL-Server im Rahmen des Bereinigungsprozesses außer Betrieb nehmen.

## <a name="review-the-deployment"></a>Überprüfen der Bereitstellung

Da die migrierten Ressourcen in Azure enthalten sind, muss Contoso die neue Infrastruktur vollständig operationalisieren und sichern.

### <a name="security"></a>Sicherheit

- Contoso muss sicherstellen, dass die neue Azure Database for PostgreSQL-Instanz und die Datenbanken sicher sind. [Weitere Informationen](https://docs.microsoft.com/azure/postgresql/concepts-security)
- Contoso sollte die [Firewallregeln](https://docs.microsoft.com/azure/postgresql/concepts-firewall-rules) und die Konfigurationseinstellungen des virtuellen Netzwerks überprüfen, um sicherzustellen, dass Verbindungen auf die Anwendungen beschränkt sind, die Zugriff benötigen.
- Contoso sollte für die Datenverschlüsselung [BYOK](https://docs.microsoft.com/azure/postgresql/concepts-data-encryption-postgresql) implementieren.
- Contoso sollte alle Anwendungen aktualisieren, um für Verbindungen mit den Datenbanken [SSL erforderlich](https://docs.microsoft.com/azure/postgresql/concepts-ssl-connection-security) festzulegen.
- Contoso sollte [Private Link](https://docs.microsoft.com/azure/postgresql/concepts-data-access-and-security-private-link) einrichten, damit der gesamte Datenverkehr der Datenbanken innerhalb von Azure und des lokalen Netzwerks bleibt.
- Contoso sollte [Azure Advanced Threat Protection (ATP)](https://docs.microsoft.com/azure/postgresql/concepts-data-access-and-security-threat-protection) aktivieren.
- Contoso sollte die Protokollanalyse konfigurieren, um die Sicherheit sowie relevante Einträge zu überwachen und Warnungen zu erhalten.

### <a name="backups"></a>Backups

Mithilfe der Geowiederherstellung kann sichergestellt werden, dass die Azure Database for PostgreSQL-Datenbanken gesichert sind. Auf diese Weise können Sicherungen im Fall eines regionalen Ausfalls in einer gekoppelten Region genutzt werden.

> [!IMPORTANT]
> Stellen Sie sicher, dass die Azure Database for PostgreSQL-Ressource über eine Ressourcensperre verfügt und nicht gelöscht werden kann. Gelöschte Server können nicht wiederhergestellt werden.

### <a name="licensing-and-cost-optimization"></a>Lizenzierung und Kostenoptimierung

- Azure Database for PostgreSQL kann hoch- und herunterskaliert werden. Die Leistungsüberwachung des Servers und der Datenbanken ist wichtig, um sicherzustellen, dass Ihre Anforderungen erfüllt und die Kosten so gering wie möglich gehalten werden.
- Sowohl für CPU als auch für Speicher können Kosten anfallen. Sie können zwischen verschiedenen Tarifen wählen. Achten Sie darauf, dass ein geeigneter Tarif für die Datenworkloads ausgewählt ist.
- Jedes Lesereplikat wird auf Grundlage der ausgewählten Compute- und Speicheroptionen berechnet.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel wurde beschrieben, wie Contoso seine PostgreSQL-Datenbanken zu einer Azure Database for PostgreSQL-Instanz migriert hat.
