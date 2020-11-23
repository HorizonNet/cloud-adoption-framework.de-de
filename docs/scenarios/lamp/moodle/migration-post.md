---
title: Fortsetzen nach einer Moodle-Migration
description: Erfahren Sie, wie Sie nach einer Moodle-Migration fortfahren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 8594919772cfccf3dd02769a14d62f64cb1ad995
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714872"
---
# <a name="how-to-follow-up-after-a-moodle-migration"></a>Fortsetzen nach einer Moodle-Migration

## <a name="post-migration-tasks"></a>Aufgaben nach der Migration

Aufgaben nach der Migration sind abschließende Anwendungskonfigurationen, die das Einrichten von Protokollierungszielen, SSL-Zertifikaten sowie geplanten Aufgaben/cron-Aufträge umfassen. Dieser Aufgabenbereich umfasst:

- Konfigurieren von Anwendungen.
- Aktualisieren von Protokollpfaden in VM-Skalierungsgruppeninstanzen.
- Neustarten von Servern in VM-Skalierungsgruppeninstanzen.
- Aktualisieren von Zertifikaten.
- Aktualisieren von Zertifikatspeicherorten.
- Aktualisieren der lokalen HTML-Kopie.
- Neustarten von PHP- und nginx-Servern.
- Zuordnen des DNS-Namens zur Azure Load Balancer-IP-Adresse.

## <a name="controller-virtual-machine-scale-set"></a>VM-Skalierungsgruppe des Controllers

### <a name="log-paths"></a>Protokollpfade

Lokal können andere Protokollpfad-Speicherorte vorhanden sein, die mit den Azure-Protokollpfaden aktualisiert werden müssen. Beispielsweise „/var/log/syslogs/moodle/access.log“ und „/var/log/syslogs/moodle/error.log“.

- Aktualisieren Sie den Speicherort für die Protokolldatei. Dieser Befehl öffnet die Konfigurationsdatei:

  ```bash
  nano /etc/nginx/nginx.conf
  ```

- Ändern Sie den Speicherort für den Protokollpfad.

- Suchen Sie `access_log` und `error_log`, und aktualisieren Sie den Protokollpfad.

- Drücken Sie `CTRL+O` zum Speichern und `CTRL+X` zum Beenden.

### <a name="restart-servers"></a>Neustarten von Servern

Starten Sie die nginx- und php-fpm-Server neu:

  ```bash
  sudo systemctl restart nginx
  sudo systemctl restart php<phpVersion>-fpm
  ```

## <a name="controller-virtual-machine"></a>Virtueller Controllercomputer

### <a name="certificates"></a>Zertifikate

- Um auf Zertifikate zuzugreifen, melden Sie sich beim virtuellen Controllercomputer an.

- Die Zertifikate für Ihre Moodle-Anwendung befinden sich in „/moodle/certs“.

- Kopieren Sie die .crt- und .key-Dateien in „/moodle/certs/“. Die Dateinamen sollten in „nginx.crt“ und „nginx.key“ geändert werden, damit Sie von den konfigurierten nginx-Servern erkannt werden. Abhängig von Ihrer lokalen Umgebung können Sie das Hilfsprogramm SCP oder ein Tool wie WinSCP auswählen, um diese Dateien auf den virtuellen Controllercomputer zu kopieren.

- Der Befehl zum Ändern eines Zertifikatnamens.

  ```bash
  cd /path/to/certs/location
  mv /path/to/certs/location/*.key /moodle/certs/nginx.key
  mv /path/to/certs/location/*.crt /moodle/certs/nginx.crt
  ```

- Sie können außerdem ein selbstsigniertes Zertifikat generieren, das nur zum Testen geeignet ist.

  ```bash
  openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /moodle/certs/nginx.key \
   -out /moodle/certs/nginx.crt \
  -subj "/C=US/ST=WA/L=Redmond/O=IT/CN=mydomain.com"
  ```

- Es wird empfohlen, dass die Zertifikatdateien für den Besitzer schreibgeschützt sind und dass für diese Dateien der Besitzer `www-data:www-data` ist.

  ```bash
  chown www-data:www-data /moodle/certs/nginx.*
   chmod 400 /moodle/certs/nginx.*
  ```

- So aktualisieren Sie den Zertifikatspeicherort und öffnen die Konfigurationsdatei:

  ```bash
  nano /etc/nginx/sites-enabled/*.conf
  ```

- Um den Pfad des Zertifikats zu ändern, suchen Sie nach `ssl_certificate`. Aktualisieren Sie den Pfad des Zertifikats wie folgt:

```bash
   /moodle/certs/moodle/certs/nginx.crt;
   /moodle/certs/nginx.key;
```

- Drücken Sie `CTRL+O`, um die Datei zu speichern, und `CTRL+X` zum Beenden.

### <a name="update-the-local-html-copy"></a>Aktualisieren Sie der lokalen HTML-Kopie

Die lokale Kopie des Inhalts der Moodle HTML-Site (`/moodle/html/moodle`) wird in der VM-Skalierungsgruppe unter`/var/www/html/moodle` serstellt. Die lokale Kopie wird nur aktualisiert, wenn eine Aktualisierung des Zeitstempels vorliegt. Führen Sie den folgenden Befehl von dem virtuellen Controllercomputer aus, um den Zeitstempel zu aktualisieren.

  ```bash
  sudo -s
  /usr/local/bin/update_last_modified_time.moodle_on_azure.sh
  ```

- Jedes Mal, wenn das Skript in der Datei mit dem zuletzt geänderten Zeitstempel (`/moodle/html/moodle/last_modified_time.moodle_on_azure`) ausgeführt wird, wird der Inhalt des Verzeichnisses `/moodle/html/moodle` in der lokalen Kopie aktualisiert (`/var/www/html`).

### <a name="restart-servers"></a>Neustarten von Servern

- Starten Sie die Server `nginx` und `php-fpm` neu.

  ```bash
  sudo systemctl restart nginx
  sudo systemctl restart php<phpVersion>-fpm
  ```

### <a name="map-the-dns-name-to-the-azure-load-balancer-ip"></a>Zuordnen des DNS-Namens zur Azure Load Balancer-IP-Adresse

- Die DNS-Namenszuordnung zur Azure Load BalancerIP-Adresse muss auf Ebene des Hostinganbieters erfolgen.

- Deaktivieren Sie für die Moodle-Website den **Wartungsmodus**.

- Führen Sie den folgenden Befehl auf dem virtuellen Controllercomputer aus:

  ```bash
  sudo /usr/bin/php admin/cli/maintenance.php --disable
  ```

- Um den Status der Moodle-Site zu überprüfen, führen Sie den folgenden Befehl aus:

  ```bash
  sudo /usr/bin/php admin/cli/maintenance.php
  ```

- Klicken Sie auf den DNS-Namen, um die migrierte Moodle-Webseite zu erhalten.

## <a name="frequently-asked-questions-and-troubleshooting"></a>Häufig gestellte Fragen und Problembehandlung

1. Error: Fehler der Datenbankverbindung: Bei Fehlern wie _Fehler bei der Datenbankverbindung_ oder _Mit der angegebenen Datenbank konnte keine Verbindung hergestellt werden_, gibt es einige mögliche Ursachen und Lösungen wie folgt:

    - Ihr Datenbankserver ist nicht installiert oder wird nicht ausgeführt. Um dies für MySQL zu überprüfen, geben Sie den folgenden Befehl ein:

      ```bash
      $telnet database_host_name 3306
      ```

    - Sie sollten eine kryptische Antwort erhalten, die die Versionsnummer des MySQL-Servers enthält.

    - Wenn Sie versuchen, zwei Instanzen von Moodle an unterschiedlichen Ports auszuführen, verwenden Sie die IP-Adresse des Hosts (nicht „localhost“) in der Einstellung `$CFG->dbhost`, beispielsweise `$CFG->dbhost = 127.0.0.1:3308`.

    - Sie haben keine Moodle-Datenbank erstellt oder keinen Benutzer mit den richtigen Berechtigungen für den Zugriff auf die Datenbank zugewiesen.

    - Die Moodle-Datenbankeinstellungen sind nicht richtig. Der Datenbankname, Datenbankbenutzer oder das Datenbankbenutzer-Kennwort in Ihrer Moodle-Konfigurationsdatei `config.php` sind nicht richtig.

    - Überprüfen Sie, ob Ihr MySQL-Benutzername oder -Kennwort Apostrophe oder nicht alphabetische Buchstaben enthält.

2. Error: _500: Interner Serverfehler_: Dieser Fehler kann verschiedene Ursachen haben. Beginnen Sie, indem Sie das Fehlerprotokoll Ihres Webservers überprüfen, das eine umfassendere Erklärung aufweisen sollte. Hier finden Sie einige der bekannten Möglichkeiten:

    - In Ihrer Datei `.htaccess` oder `httpd.conf` liegt ein Syntaxfehler vor. Die Art, in der Anweisungen geschrieben werden, unterscheidet sich abhängig von der verwendeten Datei. Sie können den folgenden Befehl verwenden, um auf Konfigurationsfehler in ihren nginx-Dateien zu testen:

      `nginx -t`

    - Der Webserver wird unter Ihrem eigenen Benutzernamen ausgeführt, und alle Dateien haben eine maximale Berechtigungsstufe von 755. Überprüfen Sie, ob dies für Ihr Moodle-Verzeichnis in der Systemsteuerung festgelegt ist, oder verwenden Sie diesen Befehl, wenn Sie Zugriff auf die Shell haben:

      ```bash
      chmod -R 755 moodle
      ```

3. Error: _403: Unzulässig_.

    Dieser Fehler bedeutet, dass der „memory_limit“-Wert von PHP für das PHP-Skript nicht ausreichend ist. Der „memory_limit“-Wert ist die zulässige Arbeitsspeichergröße, die im obigen Beispiel `64M` beträgt (67108864 Bytes/1024 = 65536 KB, 65536 KB/1024 = 64 MB). Sie müssen den Wert von „memory_limit“ für PHP erhöhen, bis diese Meldung nicht mehr angezeigt wird. Hierfür gibt es zwei Methoden:

    Methode 1: Bei einer gehosteten Installation sollten Sie den Support Ihres Hosts fragen, wie hierfür vorzugehen ist. Viele lassen `.htaccess`-Dateien zu. Wenn dies auf Ihren Host zutrifft, fügen Sie die folgende Zeile in Ihrer Datei `.htaccess` hinzu, oder erstellen Sie eine im Moodle-Verzeichnis, wenn sie noch nicht vorhanden ist:

      ```bash
      php_value memory_limit <value>M
      Example: php_value memory_limit 40M
      ```

    Methode 2: Wenn Sie über einen eigenen Server mit Shellzugriff verfügen, bearbeiten Sie Ihre Datei `php.ini`. Stellen Sie sicher, dass es sich um die richtige handelt, indem Sie Ihre `phpinfo`-Ausgabe überprüfen:

      ```bash
      memory_limit <value>M
      Example: memory_limit 40M
      ```

    Denken Sie daran, dass Sie Ihren Webserver neu starten müssen, damit Änderungen an `php.ini` wirksam werden. Eine Alternative besteht darin, `memory_limit` mit dem Befehl 'memory_limit 0' zu deaktivieren.

4. Anmelden nicht möglich; eingefrorener Anmeldebildschirm.

    Dies kann auch zutreffen, wenn _Timeout Ihrer Sitzung. Melden Sie sich erneut an._ oder _Ein Serverfehler, der sich auf Ihre Anmeldesitzung auswirkt, wurde erkannt. Melden Sie sich erneut an, oder starten Sie Ihren Browser neu._ angezeigt wird. Im Folgenden finden Sie mögliche Gründe und Maßnahmen, die Sie ergreifen können, um dies zu beheben:

    - Überprüfen Sie zunächst, ob es sich bei Ihrem Hauptadministratorkonto, einem anderen manuellen Konto, ebenfalls um ein Problem handelt. Wenn Ihre Benutzer eine externe Authentifizierungsmethode (z. B. LDAP) verwenden, könnte dies das Problem sein. Isolieren Sie die Ursache, und vergewissern Sie sich, dass diese bei Moodle liegt, bevor Sie fortfahren.

    - Überprüfen Sie, ob Ihre Festplatte nicht voll ist, dass Ihr Server freigegeben gehostet wird und dass Sie Ihr Speicherplatzkontingent nicht erreicht haben. Dadurch wird verhindert, dass neue Sitzungen erstellt werden, und niemand kann sich mehr anmelden.

    - Überprüfen Sie sorgfältig die Berechtigungen in Ihrem `moodledata`-Bereich. Der Webserver muss in das Unterverzeichnis `sessions` schreiben können.

5. Schwerwiegender Fehler: _$CFG->dataroot ist nicht schreibbar. Der Administrator muss Verzeichnisberechtigungen korrigieren! Der Vorgang wird beendet._

    - Überprüfen Sie, ob die Moodle- und moodledata-Berechtigungen nur „www-data:www-data“ lauten. Wenn nicht, ändern Sie die Gruppen- und Besitzerberechtigungen. Der folgende Befehl aktualisiert die Berechtigungen:

      ```bash
      sudo chown -R /moodle/moodledata
      ```

6. Es wurde kein Kurs auf oberster Ebene gefunden.

    - Wenn dies unmittelbar nach Ihrem Versuch, Moodle zu installieren, angezeigt wird, bedeutet dies wahrscheinlich, dass die Installation nicht abgeschlossen wurde. Bei einer abgeschlossenen Installation werden Sie kurz vor dem Abschluss nach dem Administratorprofil gefragt und aufgefordert, die Site zu benennen. Überprüfen Sie Ihre Protokolle auf Fehler, und löschen Sie dann die Datenbank, um noch mal zu starten. Wenn Sie das webbasierte Installationsprogramm verwendet haben, versuchen Sie es mit der Befehlszeile 1.

7. Der Anmeldelink ändert sich bei der Anmeldung nicht. Ich bin angemeldet, kann aber nicht frei navigieren. Stellen Sie sicher, dass die URL in Ihrer `$CFG->wwwroot`-Einstellung exakt mit der URL identisch ist, die Sie tatsächlich für den Zugriff auf die Site verwenden.

8. Fehler beim Hochladen einer Datei:

    - Wenn Sie eine _Datei nicht gefunden_-Fehlermeldung beim Hochladen einer Datei erhalten, zeigt dies an, dass auf dem Webserver Argumente mit Schrägstrich nicht aktiviert sind. Versuchen Sie, diese zu aktivieren.

    - Wenn Ihr Webserver keine Argumente mit Schrägstrichen unterstützt, können sie in Moodle deaktiviert werden, indem Sie das Kontrollkästchen **Argumente mit Schrägstrichen verwenden** in „Verwaltung > Websiteverwaltung > Server > HTTP“ deaktivieren.

      > [!WARNING]
      > Das Deaktivieren von Argumenten mit Schrägstrichen führt dazu, dass SCORM-Pakete nicht funktionieren und dass Warnungen mit wegen Argumenten mit Schrägstrichen angezeigt werden.

9. Die Site ist im **Wartungsmodus** eingefroren. In manchen Fällen bleibt Moodle im **Wartungsmodus** hängen, und die Meldung _Diese Site wird gewartet und ist zurzeit nicht verfügbar_ wird angezeigt, obwohl Sie versuchen, sie zu deaktivieren. Wenn Sie Moodle in den **Wartungsmodus** versetzen, erstellt es eine Datei `maintenance.html` im Verzeichnis der Sitedatei `moodledata/maintenance.html`. Um dies zu korrigieren, probieren Sie Folgendes aus:

    - Überprüfen Sie, ob der Webserverbenutzer über Schreibberechtigungen für das Verzeichnis „moodledata“ verfügt.
    - Löschen Sie die Datei `maintenance.html` manuell.

10. Wo Sie die Protokolle finden:

    - Syslog:
      - Entweder ein Fehler- oder ein Zugriffsprotokoll wird generiert, während jemand auf eine Seite zugreift.
      - Sie werden an diesem Speicherort aufgezeichnet: `/var/log/nginx/`.

    - Cron-Protokoll:
      - Der cron-Auftrag wird ausgeführt, und er aktualisiert die lokale Kopie in der Instanz.
      - Der Pfad lautet `/var/log/sitelogs/moodle/cron.log`.
