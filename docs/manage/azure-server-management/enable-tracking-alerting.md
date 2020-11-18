---
title: Nachverfolgung und Warnungen für kritische Änderungen
description: Aktivieren Sie die Nachverfolgung und Warnungen für kritische Änderungen in Ihrer Hybridumgebung per „Azure-Änderungsnachverfolgung und Bestand“.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7a37a812964bb595e426341d002a0e326d86013e
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94712050"
---
<!-- cSpell:ignore HKEY kusto -->

# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Aktivieren von Nachverfolgung und Warnungen für kritische Änderungen

Azure-Änderungsnachverfolgung und Bestand bietet Warnungen zum Konfigurationszustand Ihrer Hybridumgebung und zu Änderungen an dieser Umgebung. Es kann wichtige Änderungen an Dateien, Diensten, Software und der Registrierung melden, die sich auf Ihre bereitgestellten Server auswirken könnten.

Standardmäßig überwacht der Azure Automation-Inventarisierungsdienst keine Dateien oder Registrierungseinstellungen. Die Lösung enthält eine Liste von Registrierungsschlüsseln, die für die Überwachung empfohlen werden. Um diese Liste anzuzeigen, wechseln Sie zu Ihrem Automation-Konto im Azure-Portal, und wählen Sie anschließend **Bestand** > **Einstellungen bearbeiten** aus.

![Screenshot der Ansicht des Automation-Bestands im Azure-Portal](./media/change-tracking1.png)

Weitere Informationen zu den einzelnen Registrierungsschlüsseln finden Sie unter [Änderungsnachverfolgung für Registrierungsschlüssel](/azure/automation/automation-change-tracking#registry-key-change-tracking). Wählen Sie einen beliebigen Schlüssel zur Auswertung aus und aktivieren Sie ihn dann. Die Einstellung wird auf alle virtuellen Computer angewendet, die im aktuellen Arbeitsbereich aktiviert sind.

Sie können den Dienst auch verwenden, um wichtige Dateiänderungen zu verfolgen. Sie können z. B. die Datei „C:\windows\system32\drivers\etc\hosts“ nachverfolgen, da sie vom Betriebssystem zum Zuordnen von Hostnamen und IP-Adressen verwendet wird. Änderungen an dieser Datei können zu Konnektivitätsproblemen führen oder den Datenverkehr zu gefährlichen Websites umleiten.

Um das Nachverfolgen von Dateiinhalten für die Datei „hosts“ zu aktivieren, führen Sie die Schritte unter [Aktivieren der Nachverfolgung von Dateiinhalten](/azure/automation/change-tracking-file-contents#enable-file-content-tracking) aus.

Sie können auch eine Warnung für Änderungen an Dateien hinzufügen, die Sie nachverfolgen. Nehmen Sie z. B. an, dass Sie eine Warnung für Änderungen an der Datei „hosts“ festlegen möchten. Wählen Sie **Log Analytics** in der Befehlsleiste oder die Protokollsuche für den verknüpften Log Analytics-Arbeitsbereich aus. Verwenden Sie in Log Analytics die folgende Abfrage, um nach Änderungen an der Datei „hosts“ zu suchen:

  ```kusto
  ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
  ```

![Screenshot des Log Analytics-Abfrage-Editors im Azure-Portal](./media/change-tracking2.png)

Diese Abfrage sucht nach Änderungen am Inhalt von Dateien, deren Pfad das Wort „hosts“ enthält. Sie können auch nach einer bestimmten Datei suchen, indem Sie den Pfadparameter ändern. (Beispiel: `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`.)

Nachdem die Abfrage die Ergebnisse zurückgegeben hat, wählen Sie **Neue Warnungsregel** aus, um den Editor für Warnungsregeln zu öffnen. Sie können diesen Editor auch über Azure Monitor im Azure-Portal erreichen.

Überprüfen Sie die Abfrage im Editor für Warnungsregeln, und ändern Sie bei Bedarf die Warnungslogik. In diesem Fall soll die Warnung ausgelöst werden, wenn Änderungen an einem Computer in der Umgebung festgestellt werden.

![Screenshot des Log Analytics-Editors für Warnungsregeln im Azure-Portal](./media/change-tracking3.png)

Nachdem die Bedingungslogik festgelegt wurde, können Sie Aktionsgruppen zuweisen, um Aktionen als Reaktion auf die Warnung durchzuführen. In diesem Beispiel werden beim Auslösen der Warnung E-Mails gesendet und es wird ein ITSM-Ticket erstellt. Sie können viele andere nützliche Aktionen ausführen, z. B. das Auslösen einer Azure-Funktion, eines Azure Automation-Runbooks, eines Webhook oder einer Logik-App.

![Screenshot der Zusammenfassung der Beispielwarnungsregel im Azure-Portal](./media/change-tracking4.png)

Nachdem Sie alle Parameter und die Logik festgelegt haben, wenden Sie die Warnung auf die Umgebung an.

## <a name="tracking-and-alerting-examples"></a>Beispiele für Nachverfolgung und Warnungen

In diesem Abschnitt werden weitere häufige Szenarien für Nachverfolgung und Warnungen vorgestellt, die Sie möglicherweise verwenden möchten.

### <a name="driver-file-changed"></a>Änderungen an der Treiberdatei

Ermitteln Sie mithilfe der folgenden Abfrage, ob Treiberdateien geändert, hinzugefügt oder entfernt wurden. Sie ist nützlich für das Nachverfolgen von Änderungen an kritischen Systemdateien.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Bestimmter Dienst beendet

Verwenden Sie die folgende Abfrage, um Änderungen an für das System wichtigen Diensten zu verfolgen.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Neue Software installiert

Verwenden Sie die folgende Abfrage für Umgebungen, in denen Softwarekonfigurationen gesperrt werden müssen.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Eine bestimmte Softwareversion ist auf einem Computer installiert oder nicht installiert.

Verwenden Sie die folgende Abfrage, um die Sicherheit zu bewerten. Diese Abfrage verweist auf `ConfigurationData`, das die Protokolle für den Bestand enthält und den letzten gemeldeten Konfigurationsstatus und keine Änderungen bereitstellt.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-the-registry"></a>Bekannte DLL-Änderungen über die Registrierung

Verwenden Sie die folgende Abfrage, um Änderungen an bekannten Registrierungsschlüsseln zu erkennen.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Azure Automation [Zeitpläne für Updates](./update-schedules.md) erstellen kann, um Updates für Ihre Server zu verwalten.

> [!div class="nextstepaction"]
> [Erstellen von Zeitplänen für Updates](./update-schedules.md)
