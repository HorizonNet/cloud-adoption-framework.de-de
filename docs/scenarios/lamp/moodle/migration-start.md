---
title: Manuelle Schritte für die Migration von Moodle
description: Mithilfe der in diesem Artikel beschriebenen Schritte können Sie das lokale Sicherungsarchiv von Moodle in Azure-Ressourcen importieren und die Moodle-Anwendung konfigurieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/23/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 95c030bfb0d87a960d7ac158c82cc09a8bed5d95
ms.sourcegitcommit: 1d7b16eb710bed397280fb8f862912c78f2254ee
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2020
ms.locfileid: "95812223"
---
# <a name="moodle-manual-migration-steps"></a>Manuelle Schritte für die Migration von Moodle

In diesem Artikel werden die Schritte zum Importieren des lokalen Moodle-Archivs in Azure Database for MySQL und zum anschließenden Konfigurieren der Azure Moodle-Anwendung beschrieben.

Stellen Sie sicher, dass Sie alle Schritte der folgenden Artikel durchgeführt haben, bevor Sie mit diesem Prozess beginnen:
- [Vorbereiten einer Moodle-Migration](migration-pre.md)
- [Architektur und Vorlagen für die Moodle-Migration](migration-arch.md)
- [Erstellen eines Gateways für virtuelle Netzwerke und Herstellen einer Verbindung mit VMs](vpn-gateway.md)

Sobald die Bereitstellung der ARM-Vorlage (Azure Resource Manager) abgeschlossen ist, melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an, navigieren Sie zur Ressourcengruppe, die von der Vorlage erstellt wurde, und zeigen Sie alle erstellten Infrastrukturressourcen an. Die erstellten Ressourcen sollten der folgenden Abbildung ähneln, je nachdem, welche ARM-Vorlage Sie verwendet haben.

![Screenshot: In der Ressourcengruppe für die Moodle-Migration erstellte Infrastrukturressourcen](images/resource-creation-overview.png)

## <a name="copy-the-moodle-archive"></a>Kopieren des Moodle-Archivs

Kopieren Sie das Moodle-Sicherungsarchiv aus Azure Blob Storage auf der Controller-VM (virtueller Computer).

### <a name="sign-in-to-the-controller-virtual-machine"></a>Anmelden bei der Controller-VM

1. Verwenden Sie einen kostenlosen Open-Source-Terminalemulator oder ein serielles Konsolentool wie [PuTTY](https://www.putty.org/), um sich bei einer Controller-VM anzumelden.
   
1. Geben Sie in der **PuTTY-Konfiguration** die öffentliche IP-Adresse der Controller-VM als **Hostname** ein.
   
1. Erweitern Sie im linken Navigationsbereich **SSH**.
   
   ![Screenshot: PuTTY-Konfigurationsseite](images/putty-configuration.png)
   
1. Klicken Sie auf **Auth**, und suchen Sie nach der SSH-Schlüsseldatei, die Sie zum Bereitstellen der Azure-Infrastruktur mit der ARM-Vorlage verwendet haben.
   
1. Wählen Sie **Open**(Öffnen). Geben Sie als Benutzername **azureadmin** ein, weil dieser Name in der Vorlage hartcodiert ist.
   
   ![Screenshot: SSH-Authentifizierungseinstellungen auf der PuTTY-Konfigurationsseite](images/putty-ssh-key.png)
   
Weitere Informationen über PuTTY finden Sie in den [Häufig gestellten Fragen zu PuTTY](https://documentation.help/PuTTY/faq.html).

### <a name="download-and-install-azcopy-on-the-controller-vm"></a>Herunterladen und Installieren von AzCopy auf der Controller-VM

Führen Sie die folgenden Befehle zum Installieren von AzCopy aus, nachdem Sie sich bei der Controller-VM angemeldet haben:

  ```bash
  sudo -s
  wget https://aka.ms/downloadazcopy-v10-linux
  tar -xvf downloadazcopy-v10-linux
  sudo rm /usr/bin/azcopy
  sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
  ```

### <a name="copy-the-archive-to-the-controller-vm"></a>Kopieren des Archivs auf die Controller-VM

1. Führen Sie die folgenden Befehle aus, um die komprimierte `storage.tar.gz`-Sicherungsdatei aus Azure Blob Storage in das Verzeichnis `/home/azureadmin/` der Controller-VM herunterzuladen:
   
   ```bash
   sudo -s
   cd /home/azureadmin/
   azcopy copy 'https://<storageaccount>.blob.core.windows.net/container/BlobDirectoryName<SAStoken>' '/home/azureadmin/'
   ```
   
   Fügen Sie Ihr eigenes Speicherkonto und Ihre SAS-Tokenwerte ein. Beispiel:
   
   `azcopy copy 'https://onpremisesstorage.blob.core.windows.net/migration/storage.tar.gz?sv=2019-12-12&ss=' /home/azureadmin/storage.tar.gz`
   
1. Extrahieren Sie die komprimierte Datei in ein Verzeichnis.
   
   ```bash
   d /home/azureadmin
   ar -zxvf storage.tar.gz
   ```

### <a name="back-up-the-current-configuration"></a>Sichern der aktuellen Konfiguration

Sichern Sie vor der Migration die aktuelle Konfiguration. Das Sicherungsverzeichnis wird als `storage`-Verzeichnis unter `home/azureadmin` extrahiert. Dieses `storage`-Verzeichnis enthält `moodle`, `moodledata` und Konfigurationsverzeichnisse sowie eine Datenbanksicherungsdatei, die Sie in gewünschte Speicherorte kopieren.

1. Erstellen Sie ein Sicherungsverzeichnis:
   
   ```bash
   cd /home/azureadmin/
   mkdir -p backup
   mkdir -p backup/moodle
   mkdir -p backup/moodle/html
   ```
   
1. Erstellen Sie Sicherungen der Verzeichnisse `moodle` und `moodledata`:
   
   ```bash
   mv /moodle/html/moodle /home/azureadmin/backup/moodle/html/moodle
   mv /moodle/moodledata /home/azureadmin/backup/moodle/moodledata
   ```
   
1. Kopieren Sie die Verzeichnisse `moodle` und `moodledata` an einen gemeinsamen Speicherort in `/moodle`:
   
   ```bash
   cp -rf /home/azureadmin/storage/moodle /moodle/html/
   cp -rf /home/azureadmin/storage/moodledata /moodle/moodledata
   ```

## <a name="import-the-moodle-database-to-azure"></a>Importieren der Moodle-Datenbank in Azure

Stellen Sie eine Verbindung mit dem Azure Database for MySQL-Server her, und importieren Sie das lokale Moodle-Datenbankarchiv in Azure Database for MySQL.

### <a name="connect-to-the-mysql-server"></a>Herstellen einer Verbindung mit dem MySQL-Server

Azure Database for MySQL-Instanzen sind durch eine Firewall geschützt. Alle Verbindungen mit dem Server und den Datenbanken auf dem Server werden standardmäßig verweigert. Bevor Sie zum ersten Mal eine Verbindung mit Azure Database for MySQL herstellen, konfigurieren Sie die Firewall, um den Zugriff auf die öffentliche IP-Adresse oder den IP-Adressbereich der Controller-VM zuzulassen.

Sie können die Firewall mithilfe der Azure CLI oder über das Azure-Portal konfigurieren.

Führen Sie den folgenden Azure CLI-Befehl aus, und ersetzen Sie die Platzhalter dabei durch Ihre eigenen Werte:

```azurecli
az mysql server firewall-rule create --resource-group <myresourcegroup> --server <mydemoserver> --name <AllowMyIP> --start-ip-address <192.168.0.1> --end-ip-address <192.168.0.1>
```

Alternativ können Sie im Azure-Portal den Azure Database for MySQL-Server aus Ihren bereitgestellten Moodle-Infrastrukturressourcen auswählen. Klicken Sie auf der Serverseite im linken Navigationsbereich auf **Verbindungssicherheit**.

Dort können Sie zulässige IP-Adressen hinzufügen und Firewallregeln konfigurieren. Wählen Sie **Speichern** aus, nachdem Sie die Regeln erstellt haben.

![Screenshot: Verbindungssicherheitsbereich für den Azure Database for MySQL-Server](images/database-connection-security.png)

Nun können Sie mithilfe des [mysql](https://dev.mysql.com/doc/refman/8.0/en/mysql.html)-Befehlszeilentools oder mit [MySQL Workbench](https://dev.mysql.com/doc/workbench/en/) eine Verbindung mit dem MySQL-Server herstellen.

![Screenshot: Anzeige zum Einrichten einer neuen Verbindung mit MySQL Workbench](images/database-connection.png)

Verbindungsinformationen finden Sie im Azure-Portal auf der Seite **Übersicht** Ihres MySQL-Servers. Verwenden Sie die Kopierschaltflächen neben den einzelnen Feldern, um den **Servernamen** und den **Anmeldenamen des Serveradministrators** zu kopieren.

Der Servername kann beispielsweise `mydemoserver.mysql.database.azure.com` und der Anmeldename des Serveradministrators kann `myadmin@mydemoserver` lauten.

Sie benötigen außerdem das Kennwort. Wenn Sie das Kennwort zurücksetzen müssen, klicken Sie in der Menüleiste auf **Kennwort zurücksetzen**.

Verwenden Sie diese Datenbankserverinformationen für die folgenden Abschnitte.

### <a name="import-the-moodle-database-to-azure-database-for-mysql"></a>Importieren der Moodle-Datenbank in Azure Database for MySQL

1. Erstellen Sie eine MySQL-Datenbank, in die die lokale Datenbank importiert werden soll:
   
   ```bash
   mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "CREATE DATABASE $moodledbname CHARACTER SET utf8;"
   ```
   
1. Weisen Sie der Datenbank die entsprechenden Berechtigungen zu:
   
   ```bash
   mysql -h $server_name -u $server_admin_login_name -p$admin_password -e "GRANT ALL ON $moodledbname.* TO '$server_admin_login_name' IDENTIFIED BY '$admin_password';"
   ```
   
1. Importieren Sie die Datenbank:
   
   ```bash
   mysql -h $server_name -u $server_admin_login_name -p$admin_password $moodledbname < /home/azureadmin/storage/database.sql
   ```

## <a name="update-configurations"></a>Updatekonfigurationen

Nachdem Sie das lokale Moodle-Datenbankarchiv in Azure Database for MySQL importiert haben, nehmen Sie nach Bedarf Änderungen an den folgenden Konfigurationen auf der Controller-VM vor:

- Aktualisieren Sie die Moodle-Konfigurationsdatei.
- Konfigurieren Sie die Verzeichnisberechtigungen.
- Konfigurieren Sie die PHP- und nginx-Webserver.
- Aktualisieren Sie den DNS-Namen und andere Variablen.
- Installieren Sie fehlende PHP-Erweiterungen.
- Führen Sie einen Neustart durch, und beenden Sie dann die Webserver.
- Kopieren Sie die Konfigurationsdateien in einen gemeinsamen Speicherort für den Kopiervorgang in VM-Skalierungsgruppen.

### <a name="update-the-moodle-config-file"></a>Aktualisieren der Moodle-Konfigurationsdatei

Aktualisieren Sie die Parameter der Datenbankdetails in der Moodle-Konfigurationsdatei `/moodle/config.php`.

So rufen Sie den DNS-Namen für diesen Task ab:

1. Wählen Sie im Azure-Portal die **öffentliche IP-Adresse des Lastenausgleichs** Ihrer bereitgestellten Moodle-Infrastrukturressourcen aus.
   
1. Klicken Sie auf der Seite **Übersicht** auf das Kopiersymbol neben dem **DNS-Namen**.
   
So aktualisieren Sie die Datei `config.php`:

1. Geben Sie die folgenden Befehle ein, um `config.php` und `nano` im Editor zu bearbeiten:
   
   ```bash
   cd /moodle/html/moodle/
   nano config.php
   ```
   
1. Ändern Sie die Datenbankdetails in der Datei mithilfe der Werte, die Sie aus dem Azure-Portal kopiert haben:
   
   ```php
   $CFG->dbhost    = 'localhost';                // Change 'localhost' to the server name.
   $CFG->dbname    = 'moodle';                   // Change 'moodle' to the newly created database name.
   $CFG->dbuser    = 'root';                     // Change 'root' to the server admin login name.
   $CFG->dbpass    = 'password';                 // Change 'password' to the server admin login password.
   $CFG->wwwroot   = 'https://on-premises.com';  // Change 'on-premises' to the DNS name.
   $CFG->dataroot  = '/var/moodledata';          // Change the path to '/moodle/moodledata'.
   ```
   
1. Nachdem Sie die Änderungen vorgenommen haben drücken Sie STRG + O zum Speichern der Datei und STRG + X zum Schließen des Editors.

Sie können das lokale Verzeichnis `dataroot` an einem beliebigen Speicherort speichern.

### <a name="configure-directory-permissions"></a>Konfigurieren von Verzeichnisberechtigungen

- Weisen Sie dem Verzeichnis `moodle` die Berechtigungen „755“ und „www-data owner:group“ zu.
  
  ```bash
  sudo chmod 755 /moodle/html/moodle sudo chown -R www-data:www-data /moodle/html/moodle
  ```
  
- Weisen Sie dem Verzeichnis `moodledata` die Berechtigungen „770“ und „www-data owner:group“ zu.
  
  ```bash
  sudo chmod 770 /moodle/moodledata sudo chown -R www-data:www-data /moodle/moodledata
  ```
  
### <a name="update-web-config-files"></a>Aktualisieren der Webkonfigurationsdateien

Sichern und aktualisieren Sie die nginx-Datei `conf`:

```bash
sudo mv /etc/nginx/sites-enabled/*.conf /home/azureadmin/backup/
cd /home/azureadmin/storage/configuration/
sudo cp -rf nginx/sites-enabled/*.conf /etc/nginx/sites-enabled/
```

Sichern und aktualisieren Sie die PHP-Datei `www.conf`:

```bash
_PHPVER='/usr/bin/php -r "echo PHP_VERSION;" | /usr/bin/cut -c 1,2,3'
echo $_PHPVER
sudo mv /etc/php/$_PHPVER/fpm/pool.d/www.conf /home/azureadmin/backup/www.conf
sudo cp -rf /home/azureadmin/storage/configuration/php/$_PHPVER/fpm/pool.d/www.conf /etc/php/$_PHPVER/fpm/pool.d/
```

### <a name="update-nginx-configuration-variables"></a>Aktualisieren von nginx-Konfigurationsvariablen

Ändern Sie den DNS-Namen für die Azure-Cloud in den DNS-Namen der lokalen Moodle-Anwendung.

1. Öffnen Sie die nginx-Konfigurationsdatei:
   
   ```bash
   nano /etc/nginx/sites-enabled/*.conf
   ```
   
1. Bei der Bereitstellung der ARM-Vorlage wird der nginx-Server auf Port 81 festgelegt. Ändern Sie den Wert von `SERVER_PORT` in der Datei in „81“, wenn er noch nicht „81“ ist.
   
1. Ändern Sie `server_name`. Ersetzen Sie beispielsweise bei `server_name on-premises.com` die Zeichenfolge `on-premises.com` durch den DNS-Namen. In den meisten Fällen wird der DNS-Name bei der Migration nicht geändert.
   
1. Aktualisieren Sie den Speicherort des HTML-Verzeichnisses `root`. Ändern Sie z.B. den Pfad `root /var/www/html/moodle;` in `root /moodle/html/moodle;`.
   
   Das lokale Stammverzeichnis kann sich an einem beliebigen Speicherort befinden.
   
1. Nachdem Sie die Änderungen vorgenommen haben drücken Sie STRG + O zum Speichern der Datei und STRG + X zum Schließen.

### <a name="install-any-missing-php-extensions"></a>Installieren fehlender PHP-Erweiterungen

Die ARM-Bereitstellungsvorlagen installieren die folgenden PHP-Erweiterungen: fpm, cli, curl, zip, pear, mbstring, dev, mcrypt, soap, json, redis, bcmath, gd, mysql, xmlrpc, intl, xml und bz2. Wenn die lokale Moodle-Anwendung PHP-Erweiterungen aufweist, die nicht auf der Controller-VM installiert sind, können Sie diese manuell installieren.

Führen Sie den folgenden Befehl aus, um die Liste der PHP-Erweiterungen in der lokalen Anwendung abzurufen:

```bash
php -m
```

Führen Sie den folgenden Befehl aus, um fehlende Erweiterungen zu installieren:

```bash
sudo apt-get install -y php-<extension>
```

### <a name="restart-and-stop-the-web-servers"></a>Neustarten und Beenden der Webserver

1. Starten Sie die Webserver neu.
   
   ```bash
   sudo systemctl restart nginx
   sudo systemctl restart php$_PHPVER-fpm
   ```
   
1. Beenden Sie die Webserver.
   
   ```bash
   sudo systemctl stop nginx
   sudo systemctl stop php$_PHPVER-fpm
   ```

Wenn eine Anforderung bei Azure Load Balancer eingeht, wird diese nun an VM-Skalierungsgruppeninstanzen umgeleitet, und nicht an die Controller-VM.

### <a name="copy-configuration-files"></a>Kopieren von Konfigurationsdateien

Kopieren Sie PHP- und Webserver-Konfigurationsdateien in einen gemeinsamen Speicherort, damit sie später in VM-Skalierungsgruppeninstanzen kopiert werden können.

Führen Sie den folgenden Befehl aus, um das Verzeichnis für Konfigurationsdateien an einem gemeinsamen Standort zu erstellen:

```bash
mkdir -p /moodle/config
mkdir -p /moodle/config/php
mkdir -p /moodle/config/nginx
```

Führen Sie den folgenden Befehl aus, um die PHP- und Webserver-Konfigurationsdateien in das gemeinsame Verzeichnis zu kopieren:

```bash
cp /etc/nginx/sites-enabled/* /moodle/config/nginx
cp /etc/php/$_PHPVER/fpm/pool.d/www.conf /moodle/config/php
```

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit den nächsten Schritten des Moodle-Migrationsprozesses im Artikel [Einrichten der Moodle-Controllerinstanz und -Workerknoten](azure-infra-config.md) fort.
