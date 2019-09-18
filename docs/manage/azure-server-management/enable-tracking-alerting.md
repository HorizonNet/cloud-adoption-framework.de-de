---
title: Aktivieren von Nachverfolgung und Warnungen für kritische Änderungen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aktivieren von Nachverfolgung und Warnungen für kritische Änderungen
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 93449f754e3908e092fa64c55ad62fc604b4ba5b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032041"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Aktivieren von Nachverfolgung und Warnungen für kritische Änderungen

Azure-Änderungsnachverfolgung und Bestand bietet Warnungen zum Konfigurationszustand Ihrer Hybridumgebung und zu allen Änderungen an dieser Umgebung. Sie können wichtige Änderungen an Dateien, Diensten, Software und der Registrierung überwachen, die sich auf Ihre bereitgestellten Server auswirken könnten.

Standardmäßig überwacht der Azure Automation-Inventarisierungsdienst keine Dateien oder Registrierungseinstellungen. Die Lösung enthält eine Liste von Registrierungsschlüsseln, die für die Überwachung empfohlen werden. Um diese Liste anzuzeigen, wechseln Sie zu Ihrem Automation-Konto im Azure-Portal, und wählen Sie **Bestand** > **Einstellungen bearbeiten** aus:

![Screenshot der Ansicht des Automation-Bestands im Azure-Portal](./media/change-tracking1.png)

Weitere Informationen zu den einzelnen Registrierungsschlüsseln finden Sie unter [Änderungsnachverfolgung für Registrierungsschlüssel](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Sie können die einzelnen Schlüssel auswerten und dann durch Auswahl aktivieren. Die Einstellung wird auf alle virtuellen Computer angewendet, die im aktuellen Arbeitsbereich aktiviert sind.

Darüber hinaus können Sie wichtige Dateiänderungen nachverfolgen. Sie können z. B. die Datei „C:\windows\system32\drivers\etc\hosts“ nachverfolgen, da sie vom Betriebssystem zum Zuordnen von Hostnamen und IP-Adressen verwendet wird. Jegliche Änderungen an dieser Datei können zu Konnektivitätsproblemen führen oder den Datenverkehr zu gefährlichen Websites umleiten.

Um das Nachverfolgen von Dateiinhalten für die Datei „hosts“ zu aktivieren, führen Sie die Schritte unter [Aktivieren der Nachverfolgung von Dateiinhalten](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking) aus.

Sie können auch eine Warnung für Änderungen an Dateien hinzufügen, die Sie nachverfolgen. Nehmen Sie z. B. an, dass Sie eine Warnung für Änderungen an der Datei „hosts“ festlegen möchten. Wechseln Sie zunächst zu Log Analytics, indem Sie **Log Analytics** in der Befehlsleiste auswählen oder die Protokollsuche für den verknüpften Log Analytics-Arbeitsbereich öffnen. Nachdem Sie sich in Log Analytics befinden, suchen Sie mit der folgenden Abfrage nach Inhaltsänderungen in der Datei „hosts“:

```kusto
ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
```

![Screenshot des Log Analytics-Abfrage-Editors im Azure-Portal](./media/change-tracking2.png)

Diese Abfrage sucht nach Änderungen am Inhalt von Dateien, die einen Pfad aufweisen, der das Wort „hosts“ enthält. Sie können auch nach einer bestimmten Datei suchen, indem Sie den Pfadparameter ändern. (Beispiel: `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`.)
  
Nachdem die Abfrage die Ergebnisse zurückgegeben hat, wählen Sie **Neue Warnungsregel** aus, um den Editor für Warnungsregeln zu öffnen. Sie können diesen Editor auch über Azure Monitor im Azure-Portal erreichen.

Überprüfen Sie die Abfrage im Editor für Warnungsregeln, und ändern Sie bei Bedarf die Warnungslogik. In diesem Fall soll die Warnung ausgelöst werden, wenn Änderungen an einem Computer in der Umgebung festgestellt werden.

![Screenshot des Log Analytics-Editors für Warnungsregeln im Azure-Portal](./media/change-tracking3.png)

Nachdem die Bedingungslogik festgelegt wurde, können Sie Aktionsgruppen zuweisen, um Aktionen als Reaktion auf die Warnung durchzuführen. In diesem Beispiel werden beim Auslösen der Warnung E-Mails gesendet und es wird ein ITSM-Ticket erstellt. Sie können viele andere nützliche Aktionen ausführen, z. B. das Auslösen einer Azure-Funktion, eines Azure Automation-Runbooks, eines Webhook oder einer Logik-App.

![Screenshot der Zusammenfassung der Beispielwarnungsregel im Azure-Portal](./media/change-tracking4.png)

Nachdem Sie alle Parameter und die Logik festgelegt haben, wenden Sie die Warnung auf die Umgebung an.

## <a name="more-tracking-and-alerting-examples"></a>Weitere Beispiele für Nachverfolgung und Warnungen

Hier folgen einige andere häufige Szenarien für die Nachverfolgung und Warnungen, die Sie in Betracht ziehen sollten:

### <a name="driver-file-changed"></a>Änderungen an der Treiberdatei

Ermitteln Sie, ob Treiberdateien geändert, hinzugefügt oder entfernt wurden. Nützlich für das Nachverfolgen von Änderungen an kritischen Systemdateien.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Bestimmter Dienst beendet

Nützlich für das Nachverfolgen von Änderungen an für das System wichtigen Diensten.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Neue Software installiert

Nützlich für Umgebungen, in denen Softwarekonfigurationen gesperrt werden müssen.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Eine bestimmte Softwareversion ist auf einem Computer installiert oder nicht installiert.

Nützlich für die Bewertung der Sicherheit. Beachten Sie, dass diese Abfrage auf `ConfigurationData` verweist, das die Protokolle für den Bestand enthält und den letzten gemeldeten Konfigurationsstatus und keine Änderungen meldet.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-registry"></a>Bekannte DLL-Änderungen über die Registrierung

Nützlich zum Erkennen von Änderungen an bekannten Registrierungsschlüsseln.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie Updates für Ihre Server verwalten können, indem Sie [Zeitpläne für Updates](./update-schedules.md) mit Azure Automation erstellen.

> [!div class="nextstepaction"]
> [Erstellen von Zeitplänen für Updates](./update-schedules.md)
