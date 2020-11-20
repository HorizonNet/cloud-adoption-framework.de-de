---
title: Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse
description: Erfahren Sie mehr über das Erstellen eines virtuellen Netzwerkgateways und das Verbinden über eine private IP-Adresse.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: f4b3c36fcbebda0501a05f4b0751832202be9bd2
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714873"
---
# <a name="how-to-create-a-virtual-network-gateway-and-connect-through-a-private-ip"></a>Erstellen eines virtuellen Netzwerkgateways und Verbinden über eine private IP-Adresse

In diesem Dokument wird erläutert, wie Sie ein virtuelles Netzwerkgateway in Azure einrichten.

## <a name="getting-started"></a>Erste Schritte

Erstellen Sie mit den folgenden Schritten im Azure-Portal ein virtuelles Netzwerkgateway:

- Suchen Sie nach **Virtuelles Netzwerkgateway**, und wählen Sie die Option aus.
- Wählen Sie **Erstellen** aus, um ein Fenster zu öffnen.
- Füllen Sie alle Felder wie **Name, Region, Gatewaytyp, SKU,** und **VNet** aus. Behalten Sie die restlichen Standardwerte bei.
- Wählen Sie das virtuelle Netzwerk aus, das den virtuellen Computern zugeordnet ist, die in derselben Ressourcengruppe erstellt wurden.
- Wählen Sie **Erstellen** aus, um die Bereitstellung zu starten.

![Erstellen eines virtuellen Netzwerkgateways.](images/vpn-gateway.png)

- Erstellen Sie ein virtuelles Netzwerkgateway mit diesem Azure CLI-Befehl:

    ```bash
    az network vnet-gateway create -g MyResourceGroup -n MyVnetGateway --public-ip-address MyGatewayIp --vnet MyVnet --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
    ```

## <a name="generate-certificates"></a>Generieren von Zertifikaten

- Öffnen Sie die Windows PowerShell-ISE für die Stamm- und untergeordneten Zertifikate.

- Der Befehl zum Erstellen von Stammzertifikaten:

  ```bash
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
   -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

- Der Befehl zum Erstellen von untergeordneten Zertifikaten:

  ```bash
  New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="export-certificates"></a>Exportieren von Zertifikaten

Wenn Sie die folgenden Schritte ausführen, sollten Sie Zertifikate erfolgreich auf Ihren lokalen Systemen installieren können.

- Öffnen Sie die Microsoft Management Console, um die Zertifikate zu exportieren.
- Wechseln Sie zu **Ausführen**. Geben Sie **MMC** ein, um Zertifikate zu öffnen.
- Wählen Sie unter dem Ordner **Persönlich** die **Zertifikate** aus, um eine Seite zu öffnen.
- Aktualisieren Sie die Seite, um **Stamm- und untergeordnete Zertifikate** zu suchen.

Zertifikattypen:

**So exportieren Sie Stammzertifikate:**

- Wählen Sie das Stammzertifikat aus, klicken Sie auf das Zertifikat, und halten Sie es (oder klicken Sie mit der rechten Maustaste), und wechseln Sie dann zu **Alle Aufgaben**.
- Wählen Sie für ein neues Fenster **Exportieren** aus, und dann **Weiter**.
- Wählen Sie **Nein, privaten Schlüssel nicht exportieren** aus und dann **Weiter**.
- Wählen Sie **Base-64-codiertes X.509 (.cer)** aus und dann **Weiter**.
- Wählen Sie **Durchsuchen und den Pfad** aus, geben Sie einen Namen ein, und wählen Sie **Weiter** aus.
- Diese Meldung wird angezeigt: **Erfolgreich exportiert**.

**So exportieren Sie untergeordnete Zertifikate:**

- Wählen Sie das Clientzertifikat aus, klicken Sie auf das Zertifikat, und halten Sie es (oder klicken Sie mit der rechten Maustaste), und wechseln Sie dann zu **Alle Aufgaben**.
- Wählen Sie für ein neues Fenster **Exportieren** aus, und dann **Weiter**.
- Wählen Sie **Ja**, **Privaten Schlüssel exportieren** und dann **Weiter** aus.
- Wählen Sie **Persönlicher Informationsaustausch**, **PKCS** und dann **Weiter** aus.
- Aktivieren Sie das Kontrollkästchen des Kennworts, und geben Sie das Kennwort an.
- Legen Sie die Verschlüsselung auf TripleDES-SHA1 fest, und wählen Sie **Weiter** aus.
- Wählen Sie **Durchsuchen und den Pfad** aus, geben Sie einen Namen ein, und wählen Sie **Weiter** aus.
- Diese Meldung wird angezeigt: **Erfolgreich exportiert**.
- Öffnen Sie die Stammzertifikatdatei im Editor Ihrer Wahl, und kopieren Sie den Code.

## <a name="configure-the-virtual-network-gateway"></a>Konfigurieren des virtuellen Netzwerkgateways

- Wechseln Sie zu der Ressourcengruppe, in der das virtuelle Netzwerkgateway erstellt wurde.
- Wechseln Sie im linken Bereich zur Point-to-Site-Konfiguration.
- Klicken Sie nun im mittleren Bereich auf „Jetzt konfigurieren“.
- Fügen Sie den Adresspool hinzu (z. B. 192.168.xx.0/24).
- Wählen Sie als **Tunneltyp** den Wert **IKEv2** aus.
- Legen Sie den Authentifizierungstyp auf **Azure-Zertifizierung** fest.
- Fügen Sie den kopierten Stammzertifikatcode in das Portal ein, nennen Sie ihn **Root** (Stamm), und wählen Sie **Speichern** aus.

## <a name="download-and-connect-to-the-vpn-client"></a>Herunterladen und Konfigurieren des VPN-Clients

- Laden Sie den VPN-Client nach dem Speichern der Konfiguration aus dem Portal herunter.
- Öffnen Sie die heruntergeladene VPN-Client-ZIP-Datei, öffnen Sie den Ordner `WindowsAMD64`, und installieren Sie die Datei `VPNClinetsetupAMD64`.
- Wechseln Sie zu **Systemsteuerung\Netzwerk und Internet\Netzwerkverbindungen**, um Ihr installiertes VPN anzuzeigen.
- Klicken Sie mit der rechten Maustaste auf das VPN, und wählen Sie **Verbinden** aus.
- Ein neues Fenster wird angezeigt. Wählen Sie die Schaltfläche **Verbinden** aus, um die Verbindung herzustellen.

Die VPN-Gatewayverbindung ist hergestellt.

## <a name="log-in-to-the-virtual-machine"></a>Melden Sie sich beim virtuellen Computer an.

- Melden Sie sich über den SSH-Schlüssel bei einem virtuellen Computer mit privater IP-Adresse an.

- Führen Sie diesen Befehl aus, um die Kennwortauthentifizierung festzulegen:

  ```bash
  sudo vi /etc/ssh/sshd_config
  ```

- Aktualisieren Sie diese Parameter: Ändern Sie den Kennwortauthentifizierungstyp von **Nein** in **Ja**, suchen Sie nach der kommentierten Benutzeranmeldung (UserLogin), entfernen Sie den Kommentar **#** , und ändern Sie ihn in **Ja**.

- Drücken Sie `ESC`-TASTE, und geben Sie zum Speichern der Änderungen `:wq!` ein.

- Starten Sie die SSHD neu:

  ```bash
  sudo systemctl restart sshd
  ```

- Das Kennwort muss 14 Zeichen lang sein. Legen Sie das Kennwort mit diesem Befehl fest:

  ```bash
  sudo passwd <username>
  ```

  Beispiel: `sudo passwd azureadmin`

Die Kennwortauthentifizierung wurde abgeschlossen.

## <a name="log-in-to-virtual-machine-instance-from-a-controller-virtual-machine"></a>Anmelden bei der virtuellen Computerinstanz von einem virtuellen Controllercomputer aus

- Melden Sie sich bei Ihrem virtuellen Clientcomputer an.

- Führen Sie diese Befehle aus, um eine Verbindung mit dem privaten virtuellen Computer herzustellen:

  ```bash
  sudo ssh <username>@<private_IP>
  ```

Beispiel: `sudo ssh azureadmin@102.xx.xx.xx`

- Befolgen Sie die Aufforderung zur Eingabe des Kennworts.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit [Starten einer manuellen Moodle-Migration](./migration-start.md) fort, wo Sie Informationen zum nächsten Schritt im Moodle-Migrationsprozess finden.
