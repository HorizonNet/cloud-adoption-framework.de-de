---
title: Einrichten der Moodle-Controllerinstanz und der Workerknoten
description: Erfahren Sie, wie Sie eine Moodle-Controllerinstanz und Workerknoten einrichten (Azure-Infrastrukturkonfiguration).
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 9a40bc5b34d85a94641e2381c7773621dfe09e9f
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714896"
---
# <a name="how-to-set-up-moodle-controller-instance-and-worker-nodes"></a>Einrichten der Moodle-Controllerinstanz und der Workerknoten

## <a name="virtual-machine-scale-set-instances"></a>VM-Skalierungsgruppeninstanzen

VM-Skalierungsgruppeninstanzen werden mit privaten IP-Adressen zugewiesen, auf die nur mit dem virtuellen Controllercomputer zugegriffen werden kann, der sich im selben virtuellen Netzwerk befindet. Aktivieren Sie das Gateway, um die VM-Skalierungsgruppeninstanz mit einer privaten IP-Adresse zu verbinden, und befolgen Sie [Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse](./vpn-gateway.md), um Gatewayzugriff auf die VM-Skalierungsgruppeninstanz zu erhalten. Bevor Sie auf eine VM-Skalierungsgruppe zugreifen, legen Sie sie auf kennwortaktiviert fest.

So erstellen Sie die private IP-Adresse für eine VM-Skalierungsgruppeninstanz

- Melden Sie sich beim [Azure-Portal](https://ms.portal.azure.com/#home) an, und suchen Sie die erstellte Ressourcengruppe.
- Suchen Sie die VM-Skalierungsgruppenressource, und navigieren Sie zu ihr.
- Wählen Sie im linken Bereich **Instanzen** aus.
- Navigieren Sie zu der Instanz, die ausgeführt wird, und suchen Sie die private IP-Adresse, die ihr zugeordnet ist, im Abschnitt **Übersicht**.

Melden Sie sich bei einer VM-Skalierungsgruppe und dem virtuellen Controllercomputer an, und führen Sie diese Befehle aus:

```bash
 sudo -s
 sudo ssh azureadmin@172.31.X.X
```

172.31.X.X ist die private IP-Adresse der VM-Skalierungsgruppeninstanz.

Melden Sie sich einer VM-Skalierungsgruppeninstanz an. Führen Sie die folgenden Schritte aus:

- Ein Sicherungsverzeichnis wird als „storage/“ in „/home/azureadmin“ extrahiert. Dieses Speicherverzeichnis enthält Moodle, moodledata und ein Konfigurationsverzeichnis sowie eine Datenbank-Sicherungsdatei. Diese werden an die gewünschten Speicherorte kopiert.

- Erstellen Sie ein Sicherungsverzeichnis.

  ```bash
  cd /home/azureadmin/
  mkdir -p backup
  mkdir -p backup/moodle
  ```

- Erstellen Sie zum Konfigurieren von PHP und des Webservers eine Sicherung der PHP- und Webserverkonfigurationen, und legen Sie die PHP-Version auf eine Variable fest.

   ```bash
  _PHPVER=`/usr/bin/php -r "echo PHP_VERSION;" | /usr/bin/cut -c 1,2,3`
  echo $_PHPVER
   ```

  ```bash
  sudo mv /etc/nginx/sites-enabled/*.conf  /home/azureadmin/backup/
  sudo mv /etc/php/$_PHPVER/fpm/pool.d/www.conf /home/azureadmin/backup/www.conf  
  ```

- Kopieren Sie die PHP- und Webserverkonfigurationsdateien.

  ```bash
  sudo cp /moodle/config/nginx/*.conf  /etc/nginx/sites-enabled/
  sudo  cp /moodle/config/php/www.conf /etc/php/$_PHPVER/fpm/pool.d/
  ```

- Installieren Sie fehlende PHP-Erweiterungen, und verwenden Sie eine Azure Resource Manager-Vorlage, um die folgenden PHP-Erweiterungen zu installieren: fpm, cli, curl, zip, pear, mbstring, dev, mcrypt, soap, json, redis, bcmath, gd, mysql, xmlrpc, intl, xml und bz2.

- Um die Liste der lokal installierten PHP-Erweiterungen abzurufen, führen Sie den folgenden Befehl auf einem lokalen virtuellen Computer aus:

  ```bash
  php -m
  ```

- Wenn lokal zusätzliche PHP-Erweiterungen vorhanden sind, die nicht auf dem virtuellen Controllercomputer vorhanden sind, können sie manuell installiert werden.

  ```bash
  sudo apt-get install -y php-<extensionName>
  ```

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit [Fortsetzen nach einer Moodle-Migration](./migration-post.md) fort, wo Sie Informationen zum nächsten Schritt im Moodle-Migrationsprozess finden.
