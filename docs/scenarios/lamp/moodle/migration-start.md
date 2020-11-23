---
title: Starten einer manuellen Moodle-Migration
description: Erfahren Sie, wie Sie eine manuelle Moodle-Migration starten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 2fbaf59de2effb689d160aa22a41c51ed291b98e
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714871"
---
# <a name="how-to-start-a-manual-moodle-migration"></a>Starten einer manuellen Moodle-Migration

Um eine Moodle-Migration zu starten, melden Sie sich bei [Azure](https://portal.azure.com/) an, nachdem Sie die Bereitstellung abgeschlossen haben. Wechseln Sie zu der erstellten Ressourcengruppe, und suchen Sie alle erstellten Ressourcen. Die folgende Abbildung veranschaulicht, wie Ressourcen erstellt werden:

[Ressourcenübersicht](./images/resource-creation-overview.png)

## <a name="controller-virtual-machine"></a>Virtueller Controllercomputer

- Verwenden Sie einen kostenlosen Open-Source-Terminalemulator oder ein serielles Konsolentool, um sich bei einem Controllercomputer anzumelden.
- Kopieren Sie die öffentliche IP-Adresse des virtuellen Controllercomputers, die als Hostname verwendet werden soll.
- Erweitern Sie im Navigationsbereich **SSH**, wählen Sie **Auth** aus, und suchen Sie die SSH-Schlüsseldatei vom Bereitstellen der Azure-Infrastruktur mit einer Azure Resource Manager-Vorlage.
- Wählen Sie **Open**(Öffnen). Sie werden zur Eingabe des Benutzernamens aufgefordert. Geben Sie **azureadmin** ein, weil dieser Name in der Vorlage hartcodiert ist.

[Die PuTTY-Anmeldungsseite.](./images/putty-login.png)

[PuTTY-Schlüsselkritieren.](./images/putty-key-criteria.png)

- Durchsuchen Sie, wählen Sie den SSH-Schlüssel aus, und klicken Sie auf die Schaltfläche „Öffnen“.

Durchsuchen Sie [PuTTY: allgemeine häufig gestellte Fragen/Problembehandlungsfragen](https://documentation.help/PuTTY/faq.html), um mehr über PuTTY zu erfahren.

Führen Sie nach der Anmeldung den nächsten Satz von Befehlen für die Migration aus.

## <a name="download-and-install-azcopy"></a>Herunterladen und Installieren von AzCopy

Führen Sie die folgenden Befehle zum Installieren von AzCopy aus:

  ```bash
  sudo -s
  wget https://aka.ms/downloadazcopy-v10-linux
  tar -xvf downloadazcopy-v10-linux
  sudo rm /usr/bin/azcopy
  sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
  ```

## <a name="copy-the-backup"></a>Kopieren der Sicherung

So kopieren Sie das Sicherungsarchiv aus einer Azure Resource Manager-Bereitstellung auf die virtuelle Controllercomputerinstanz

- Laden Sie die komprimierte Sicherungsdatei (storage.tar.gz) aus dem Blobspeicher unter „/home/azureadmin/“ auf den virtuellen Controllercomputer herunter.

  ```bash
  sudo -s
  cd /home/azureadmin/
  azcopy copy `https://storageaccount.blob.core.windows.net/container/BlobDirectoryName<SASToken>` `/home/azureadmin/`
  ```

  Beispiel: `azcopy copy 'https://onpremisesstorage.blob.core.windows.net/migration/storage.tar.gz?sv=2019-12-12&ss=' /home/azureadmin/storage.tar.gz`

- Extrahieren Sie den komprimierten Inhalt in ein Verzeichnis.

  ```bash
  d /home/azureadmin
  ar -zxvf storage.tar.gz
  ```

## <a name="how-to-migrate-and-configure-a-moodle-application"></a>Migrieren und Konfigurieren einer Moodle-Anwendung

Sichern Sie vor der Migration die aktuelle Konfiguration. Ein Sicherungsverzeichnis wird als `storage/at/home/azureadmin` extrahiert. Dieses Speicherverzeichnis enthält Moodle, moodledata und Konfigurationsverzeichnisse sowie eine Datenbank-Sicherungsdatei. Diese werden an die gewünschten Speicherorte kopiert.

- Erstellen Sie ein Sicherungsverzeichnis.

  ```bash
  cd /home/azureadmin/
  mkdir -p backup
  mkdir -p backup/moodle
  mkdir -p backup/moodle/html
  ```

- Erstellen einer Sicherung von Moodle- und moodledata-Verzeichnissen.

  ```bash
  mv /moodle/html/moodle /home/azureadmin/backup/moodle/html/moodle
  mv /moodle/moodledata /home/azureadmin/backup/moodle/moodledata
  ```

- Kopieren Sie lokale Moodle- und moodledata-Verzeichnisse an einen freigegebenen Speicherort (`/moodle`).

  ```bash
  cp -rf /home/azureadmin/storage/moodle /moodle/html/
  cp -rf /home/azureadmin/storage/moodledata /moodle/moodledata
  ```

- Importieren Sie die Moodle-Datenbank in Azure. Azure Database for MySQL-Instanzen sind durch eine Firewall geschützt. Standardmäßig werden alle Verbindungen mit dem Server und den Datenbanken im Server abgelehnt. Vor dem erstmaligen Herstellen einer Verbindung mit Azure Database for MySQL müssen Sie die Firewall konfigurieren, um die öffentliche Netzwerk-IP-Adresse oder den IP-Adressbereich des Clientcomputers hinzuzufügen.

  ```bash
  az mysql server firewall-rule create --resource-group myresourcegroup --server mydemoserver --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1
  ```

- Wählen Sie den neuen MySQL-Server und dann **Verbindungssicherheit** aus.

![Auswählen von **Verbindungssicherheit**.](./images/database-connection-security.png)

- Hier können Sie eine IP-Adresse hinzufügen oder Firewallregeln konfigurieren. Wählen Sie **Speichern** aus, nachdem Sie die Regeln erstellt haben.

Sie können jetzt mithilfe des mysql-Befehlszeilentools oder mit dem MySQL-Workbench-Tool eine Verbindung mit dem Server herstellen. Zum Abrufen von Verbindungsinformationen kopieren Sie den **Servernamen** und den **Anmeldenamen des Serveradministrators** von der Seite **MySQL-Serverressource**. Sie können hierzu die Schaltfläche „Kopieren“ neben jedem der Felder auswählen.

![Einrichten einer neuen Verbindung.](images/database-connection.png)

Wenn beispielsweise der Servername `mydemoserver.mysql.database.azure.com` und der Anmeldename des Serveradministrators `myadmin@mydemoserver` lautet:

- Stellen Sie vor dem Importieren einer Datenbank sicher, dass die Details der Azure Database for MySQL Server bereit sind.
- Navigieren Sie zum Azure-Portal, und wechseln Sie zu der erstellten Ressourcengruppe.
- Wählen Sie die Azure Database for MySQL-Serverressource aus.
- Suchen Sie im Übersichtsbereich nach Azure Database for MySQL-Serverdetails wie Servername, Anmeldename des Serveradministrators.
- Setzen Sie das Kennwort zurück, indem Sie links oben auf der Seite auf die Schaltfläche „Kennwort zurücksetzen“ klicken.

Verwenden Sie diese Datenbankserver-Details für die folgenden Befehle:

- Importieren der lokalen Datenbank in Azure Database for MySQL.

- Erstellen Sie eine Datenbank zum Importieren lokaler Datenbanken.

  ```bash
  mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "CREATE DATABASE $moodledbname CHARACTER SET utf8;"
  ```

- Weisen Sie der Datenbank die richtigen Berechtigungen zu.

  ```bash
  mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "GRANT ALL ON $moodledbname.* TO `$server_admin_login_name` IDENTIFIED BY `$admin_password`;"
  ```

- Importieren Sie die Datenbank.

  ```bash
  mysql -h $server_name -u $server_admin_login_name -p$admin_password $moodledbname < /home/azureadmin/storage/database.sql
  ```

- Aktualisieren Sie die Datenbankdetails in der Moodle-Konfigurationsdatei (/moodle/config.php).

Aktualisieren Sie Parameter in „config.php“. Stellen Sie sicher, dass der DNS-Name für diese Aufgabe gespeichert wird:

- Navigieren Sie zum Azure-Portal, und suchen Sie Ihre Ressourcengruppe.

- Suchen Sie die **Öffentliche IP-Adresse des Load Balancers**, und notieren Sie sich den DNS-Namen aus dem Bereich **Übersicht**:

  dbhost, dbname, dbuser, dbpass, dataroot und wwwroot

  ```bash
  cd /moodle/html/moodle/
  nano config.php

- Update the database details, and save the file.

  For example:

  - $CFG->dbhost    = `localhost`;                - Change `localhost` to the server name.
  - $CFG->dbname    = `moodle`;                   - Change `moodle` to the newly created database name.
  - $CFG->dbuser    = `root`;                     - Change `root` to the server admin login name.
  - $CFG->dbpass    = `password`;                 - Change `password` to the server admin login password.
  - $CFG->wwwroot   = `https://on-premises.com`;  - Change `on-premises` to the DNS name.
  - $CFG->dataroot  = `/var/moodledata`;          - Change the path to `/moodle/moodledata`.

The on-premises `dataroot` directory can be stored at any location. After making the changes, save the file. Press `CTRL+O` to save and `CTRL+X` to exit.

Configure directory permissions.

- Set 755 and www-data owner:group permissions to the Moodle directory.

  ```bash
  sudo chmod 755 /moodle/html/moodle sudo chown -R www-data:www-data /moodle/html/moodle
   ```

- Legen Sie 770 und www-data owner:group-Berechtigungen für das Verzeichnis „moodledata“ fest.

  ```bash
  sudo chmod 770 /moodle/moodledata sudo chown -R www-data:www-data /moodle/moodledata
  ```

- Aktualisieren Sie die nginx-Konfigurationsdatei.

  ```bash
  sudo mv /etc/nginx/sites-enabled/*.conf /home/azureadmin/backup/
  cd /home/azureadmin/storage/configuration/
  sudo cp -rf nginx/sites-enabled/*.conf /etc/nginx/sites-enabled/
  ```

- Aktualisieren Sie die PHP-Konfigurationsdatei.

  ```bash
  _PHPVER=`/usr/bin/php -r "echo PHP_VERSION;" | /usr/bin/cut -c 1,2,3`
  echo $_PHPVER
  sudo mv /etc/php/$_PHPVER/fpm/pool.d/www.conf /home/azureadmin/backup/www.conf
  sudo cp -rf /home/azureadmin/storage/configuration/php/$_PHPVER/fpm/pool.d/www.conf /etc/php/$_PHPVER/fpm/pool.d/
  ```

- Installieren Sie fehlende PHP-Erweiterungen. Azure Resource Manager-Vorlagen installieren die folgenden PHP-Erweiterungen: fpm, cli, curl, zip, pear, mbstring, dev, mcrypt, soap, json, redis, bcmath, gd, mysql, xmlrpc, intl, xml und bz2. Um die Liste der lokal installierten PHP-Erweiterungen abzurufen, führen Sie den folgenden Befehl aus:

  ```bash
  php -m
  ```

- Wenn lokal zusätzliche PHP-Erweiterungen vorhanden sind, die nicht auf dem virtuellen Controllercomputer vorhanden sind, können sie manuell installiert werden.

  ```bash
  sudo apt-get install -y php-<extensionName>
  ```

- Aktualisieren Sie den DNS-Namen und den Speicherort des Stammverzeichnisses. Aktualisieren Sie den DNS-Namen der Azure-Cloud mit dem lokalen DNS-Namen. Dieser Befehl öffnet die Konfigurationsdatei:

  ```bash
  nano /etc/nginx/sites-enabled/*.conf
  ```

- Die Azure Resource Manager-Vorlagenbereitstellung legt den nginx-Server auf Port 81 fest. Aktualisieren Sie den Serverport auf 81, wenn er von diesem Wert abweicht.

- Aktualisieren Sie den Servernamen. Wenn beispielsweise server_name „on-premises.com“ ist, aktualisieren Sie „on-premises.com“ mit dem DNS-Namen. In den meisten Fällen kann der DNS-Name bei der Migration unverändert bleiben.

- Aktualisieren Sie den Speicherort des HTML-Stammverzeichnisses. Wenn es beispielsweise `root /var/www/html/moodle;` ist, aktualisieren Sie es auf `root /moodle/html/moodle;`.

- Das lokale Stammverzeichnis kann sich an einem beliebigen Speicherort befinden.

- Drücken Sie nach den Änderungen `CTRL+O`, um die Datei zu speichern, und `CTRL+X` zum Beenden.

- Starten Sie die Webserver neu.

  ```bash
  sudo systemctl restart nginx
  sudo systemctl restart php$_PHPVER-fpm  
  ```

- Beenden Sie die Webserver. Wenn eine Anforderung Azure Load Balancer erreicht, wird sie an VM-Skalierungsgruppeninstanzen umgeleitet, jedoch nicht an den virtuellen Controllercomputer.

  ```bash
  sudo systemctl stop nginx
  sudo systemctl stop php$_PHPVER-fpm  
  ```

## <a name="how-to-copy-configuration-files"></a>Kopieren von Konfigurationsdateien

Kopieren Sie PHP- und Webserverkonfigurationsdateien an einen freigegebenen Speicherort. Konfigurationsdateien können von dem freigegebenen Speicherort aus auf VM-Skalierungsgruppeninstanzen kopiert werden.

So erstellen Sie ein Verzeichnis für die Konfiguration an einem freigegebenen Speicherort:

```bash
mkdir -p /moodle/config
mkdir -p /moodle/config/php
mkdir -p /moodle/config/nginx
```

So kopieren Sie die PHP- und Webserverkonfigurationsdateien in ein Konfigurationsverzeichnis:

```bash
cp /etc/nginx/sites-enabled/* /moodle/config/nginx
cp /etc/php/$_PHPVER/fpm/pool.d/www.conf /moodle/config/php
```

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit [Einrichten einer Moodle-Controllerinstanz und von Workerknoten (Azure-Infrastrukturkonfiguration)](./azure-infra-config.md) fort, wo Sie Informationen zum nächsten Schritt im Moodle-Migrationsprozess finden.
