---
title: Vorbereiten einer Moodle-Migration
description: Erfahren Sie, wie Sie eine Moodle-Migration vorbereiten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 71990470e04f68f78b0bfffc2b1d837c7f0f29ad
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714892"
---
# <a name="how-to-prepare-for-a-moodle-migration"></a>Vorbereiten einer Moodle-Migration

## <a name="pre-migration-tasks"></a>Aufgaben vor der Migration

Das Exportieren von lokalen Daten nach Azure umfasst die folgenden Aufgaben:

- Installieren Sie die Azure-Befehlszeilenschnittstelle.
- Erstellen eines Abonnements
- Erstellen Sie eine Ressourcengruppe.
- Erstellen Sie ein Speicherkonto.
- Sichern der lokalen Daten.
- Herunterladen und Installieren von AzCopy.
- Kopieren archivierter Dateien in Azure-Blobs.

## <a name="install-the-azure-cli"></a>Installieren der Azure CLI

- Installieren Sie Azure CLI auf einem Host in der lokalen Infrastruktur für alle Azure-bezogenen Aufgaben.

  ```bash
   curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
  ```

- Melden Sie sich beim Azure-Konto an.

  ```bash
  az login
  ```

- Der az-Befehl für die Anmeldung: Azure CLI startet wahrscheinlich eine Instanz oder eine Registerkarte in Ihrem Standardwebbrowser und fordert Sie auf, sich mit Ihrem Microsoft-Konto bei Azure anzumelden. Wenn der Browser nicht gestartet wird, öffnen Sie eine neue Seite unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin), und geben Sie den in Ihrem Terminal angezeigten Autorisierungscode ein.

- Um die Befehlszeile zu verwenden, geben Sie folgenden Befehl ein:

  ```bash
  az login -u <username> -p <password>
  ```

## <a name="create-a-subscription"></a>Erstellen eines Abonnements

Überspringen Sie diesen Schritt,wenn Sie ein Abonnement besitzen. Wenn Sie kein Abonnement besitzen, können Sie [eins im Azure-Portal erstellen](https://ms.portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) oder sich für ein Abonnement mit [nutzungsbasierter Bezahlung](https://azure.microsoft.com/offers/ms-azr-0003p/) entscheiden.

- Um ein Abonnement im Azure-Portal zu erstellen, navigieren Sie aus dem Abschnitt **Start** zu **Abonnements**.

  ![Azure-Abonnements.](./images/subscriptions.png)

- Dieser Befehl legt das Abonnement fest:

  ```bash
  az account set --subscription "Subscription Name"

  Example: az account set --subscription "ComputePM LibrarySub"
  ```

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Sobald das Abonnement eingerichtet ist, müssen eine Ressourcengruppe erstellen. Eine Möglichkeit hierzu besteht darin, das Azure-Portal zum Erstellen zu verwenden. Navigieren Sie zum Abschnitt **Start**, suchen Sie nach **Ressourcengruppe**, wählen Sie sie aus, füllen Sie die obligatorischen Felder aus, und wählen Sie dann **Erstellen** aus.

![Ressourcengruppen: Erstellen Sie eine Ressourcengruppe.](./images/resource-group.png)

Alternativ können Sie Azure CLI verwenden, um eine Ressourcengruppe zu erstellen.

- Geben Sie denselben Standardstandort wie in den vorherigen Schritten an.

  ```bash
  az group create -l location -n name -s Subscription_NAME_OR_ID
  ```

- Aktualisieren Sie den Screenshot und den Abonnementnamen mit dem Beispieltestkonto.

  Beispiel: `az group create -l eastus -n manual_migration -s ComputePM LibrarySub`

- Im vorherigen Schritt wird eine Ressourcengruppe als „manual_migration“ erstellt. Verwenden Sie dieselbe Ressourcengruppe wie in den vorherigen Schritten.

Weitere Informationen finden Sie unter [Standort in Azure](https://azure.microsoft.com/global-infrastructure/data-residency/).

## <a name="create-a-storage-account"></a>Speicherkonto erstellen

Der nächste Schritt besteht im [Erstellen eines Speicherkontos](https://ms.portal.azure.com/#create/Microsoft.StorageAccount) in der Ressourcengruppe, die erstellt wurde. Speicherkonten können mit dem Azure-Portal oder der Azure CLI erstellt werden.

- Navigieren Sie zum Erstellen mit dem Portal zu dem Portal, suchen Sie nach dem Speicherkonto, und wählen Sie die Schaltfläche **Hinzufügen** aus. Nachdem Sie die obligatorischen Felder ausgefüllt haben, wählen Sie **Erstellen** aus.

  ![Erstellen eines Speicherkontos.](./images/create-storage-account.png)

- Alternativ können Sie die Azure CLI verwenden:

  ```bash
  az storage account create -n storageAccountName -g resourceGroupName --sku Standard_LRS --kind BlobStorage -l location
  ```

  Ein Beispiel: `az storage account create -n onpremisesstorage -g manual_migration --sku Standard_LRS --kind BlobStorage -l eastus`

- Im vorherigen Befehl gibt `--kind` den Typ des Speicherkontos an. Nachdem das Konto `onpremisesstorage` erstellt wurde, wird es zum Ziel für eine lokale Sicherung.

## <a name="back-up-on-premises-data"></a>Sichern lokaler Daten

- Aktivieren Sie vor dem Sichern lokaler Daten **Wartungsmodus** für die Moodle-Site. Führen Sie auf dem lokalen virtuellen Computer den folgenden Befehl aus:

  ```bash
  sudo /usr/bin/php admin/cli/maintenance.php --enable
  ```

- Führen Sie den folgenden Befehl aus, um den Status der Moodle-Site zu überprüfen:

  ```bash
  sudo /usr/bin/php admin/cli/maintenance.php
  ```

- Führen Sie die Sicherung lokaler Moodle- und moodledata-Dateien, -Konfigurationen und -Datenbanken in ein einzelnes Verzeichnis durch. Im folgenden Diagramm wird dies zusammengefasst:

  ![Die Verzeichnisstruktur der Moodle-Sicherung.](./images/directory-structure.png)

- Um alle Daten zu kopieren, erstellen Sie ein leeres Speicherverzeichnis am gewünschten Speicherort:

  ```bash
  sudo -s
  ```

  Beispielsweise kann der Speicherort `/home/azureadmin` sein.

  ```bash
  cd /home/azureadmin
  mkdir storage
  ```

### <a name="back-up-moodle-and-moodledata"></a>Sichern von Moodle und moodledata

- Das Moodle-Verzeichnis besteht aus HTML-Inhalt der Site. Moodledata enthalten Moodle-Sitedaten.

- Die Befehle zum Kopieren von Moodle und moodledata lauten:

  ```bash
  cp -R /var/www/html/moodle /home/azureadmin/storage/
  cp -R /var/moodledata /home/azureadmin/storage/
  ```

### <a name="backup-php-and-web-server-configurations"></a>Sichern von PHP- und Webserverkonfigurationen

- Kopieren Sie die PHP-Konfigurationsdateien wie `php-fpm.conf`, `php.ini`, `pool.d` und `conf.d` in das Verzeichnis `phpconfig` unter dem Verzeichnis `configuration`.

- Kopieren Sie die ngnix-Konfigurationen wie `nginx.conf` und `sites-enabled/dns.conf` in das Verzeichnis `nginxconfig` unter dem Verzeichnis `configuration`.

  ```bash
  cd /home/azureadmin/storage mkdir configuration
  ```

- Die Befehle zum Kopieren von nginx- und PHP-Konfigurationen lauten:

  ```bash
  cp -R /etc/nginx /home/azureadmin/storage/configuration/nginx
  cp -R /etc/php /home/azureadmin/storage/configuration/php
  ```

### <a name="create-a-backup-of-the-database"></a>Erstellen einer Sicherung der Datenbank

- Wenn Sie mysql-client bereits installiert haben, überspringen Sie den Schritt zu dessen Installation. Wenn Sie noch nicht über mysql-client verfügen, installieren Sie ihn jetzt:

  ```bash
  sudo -s
  ```

- Führen Sie den folgenden Befehl aus, um zu überprüfen, ob mysql-client installiert ist oder nicht:

  ```bash
  mysql -V
  ```

- Wenn mysql-client nicht installiert ist, führen Sie den folgenden Befehl aus:

  ```bash
  sudo apt-get install mysql-client
  ```

- Dieser Befehl gestattet es Ihnen, die Datenbank zu sichern:

  ```bash
  mysqldump -h dbServerName -u dbUserId -pdbPassword dbName > /home/azureadmin/storage/database.sql
  ```

- Ersetzen Sie dbServerName, dbUserId, dbPassword und dbName durch lokale Datenbankdetails.

- Erstellen Sie ein Archivdatei `storage.tar.gz` des Sicherungsverzeichnisses:

  ```bash
  cd /home/azureadmin/ tar -zcvf storage.tar.gz storage
  ```

## <a name="download-and-install-azcopy"></a>Herunterladen und Installieren von AzCopy

Führen Sie die folgenden Befehle aus, um AzCopy zu installieren:

  ```bash
  sudo -s
  wget https://aka.ms/downloadazcopy-v10-linux
  tar -xvf downloadazcopy-v10-linux
  sudo rm /usr/bin/azcopy
  sudo cp ./azcopy_linux_amd64_*/azcopy /usr/bin/
  ```

## <a name="copy-archived-files-to-azure-blob"></a>Kopieren archivierter Dateien in Azure-Blobs

Verwenden Sie AzCopy, um archivierte lokale Dateien in einen Azure-Blob zu kopieren.

- Um AzCopy zu verwenden, generieren Sie zuerst das SAS-Token. Wechseln Sie zu der erstellten **Speicherkontoressource**, und navigieren Sie zu **Shared Access Signature** im linken Bereich.

  ![Ein Beispielspeicherkonto.](./images/storage-account-created.png)

- Wählen Sie **Container** und Kontrollkästchen aus, und legen Sie das Start- und Ablaufdatum des SAS-Tokens fest. Klicken Sie auf **SAS und Verbindungszeichenfolge generieren**.

  ![Generieren eines SAS-Tokens.](images/SAS-token-generation.png)

- Kopieren und speichern Sie das SAS-Token für die zukünftige Verwendung.

- Der Befehl zum Erstellen eines Containers im Speicherkonto:

  ```bash
  az storage container create --account-name <storageAccountName> --name <containerName> --auth-mode login
  ```

  Beispiel: `az storage container create --account-name onpremisesstorage --name migration --auth-mode login`

  `--auth-mode login` bedeutet Authentifizierungsmodus beim Anmelden. Nach der Anmeldung wird der Container erstellt.

- Der Container kann auch über das Azure-Portal erstellt werden. Navigieren Sie zum selben erstellten Speicherkonto, wählen Sie den Container aus, und wählen Sie dann die Schaltfläche **Hinzufügen** aus.

- Nachdem Sie den obligatorischen Containernamen eingegeben haben, wählen Sie die Schaltfläche **Erstellen** aus.

  ![Ein neuer Container.](images/new-container.png)

- Der Befehl zum Kopieren einer Archivdatei in ein Azure-Blob-Konto:

  ```bash
  sudo azcopy copy /home/azureadmin/storage.tar.gz 'https://<storageAccountName>.blob.core.windows.net/<containerName>/<SAStoken>'
  ```

  Beispiel: `azcopy copy /home/azureadmin/storage.tar.gz 'https://onpremisesstorage.blob.core.windows.net/migration/?sv=2019-12-12&ss='`

  ![Ein Archiv im Azure-Blob.](images/archive-in-blob.png)

- Es sollte nun eine Kopie Ihres Archivs im Azure-Blob-Konto vorhanden sein.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit [Moodle-Migrationsaufgaben, -architektur und -vorlage](./migration-arch.md) fort, wo Sie weitere Informationen zum Moodle-Migrationsprozess finden.
