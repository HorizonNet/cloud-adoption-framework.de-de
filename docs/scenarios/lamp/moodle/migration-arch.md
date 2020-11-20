---
title: Moodle-Migrationsaufgaben, -architektur und -vorlage
description: Erfahren Sie mehr über die Aufgabe und Architektur sowie die Vorlage, die an einer Moodle-Migration beteiligt sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: f3e5d88e894289e615ac0573d6c640832b8ed028
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714886"
---
# <a name="moodle-migration-tasks-architecture-and-template"></a>Moodle-Migrationsaufgaben, -architektur und -vorlage

## <a name="moodle-migration-task-outline"></a>Übersicht der Moodle-Migrationsaufgabe

Moodle-Migrationen umfassen die folgenden Aufgaben:

- Bereitstellen der Azure-Architektur mit Azure Resource Manager-Vorlagen
- Herunterladen und Installieren von AzCopy
- Kopieren des Sicherungsarchivs aus der Azure Resource Manager-Bereitstellung auf die virtuelle Computerinstanz des Controllers
- Migration von Moodle-Anwendung und -Konfiguration
- Einrichten der Moodle-Controllerinstanz und der Workerknoten
- Konfigurieren von PHP und des Webservers.

## <a name="deploy-azure-infrastructure-with-azure-resource-manager-templates"></a>Bereitstellen der Azure-Architektur mit Azure Resource Manager-Vorlagen

- Wenn Sie eine Azure Resource Manager-Vorlage verwenden, um die Infrastruktur in Azure bereitzustellen, stehen Ihnen einige Optionen zur Verfügung. Das folgende Diagramm bietet eine Übersicht der Infrastrukturressourcen.

![Azure-Infrastrukturressourcen.](images/architecture.png)

Eine vollständig konfigurierbare Bereitstellung bietet mehr Flexibilität und Auswahlmöglichkeiten für Bereitstellungen. Eine vordefinierte Bereitstellungsgröße verwendet eine von vier vordefinierten Moodle-Größen. Die vier vordefinierten Vorlagenoptionen sind Minimal, Klein-bis-Mittel, Groß und Maximal. Sie sind im [Moodle GitHub-Repository](https://github.com/Azure/Moodle) verfügbar.

- [Minimal](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-minimal.json): Diese Bereitstellung verwendet NFS, MySQL und kleinere Web-Front-End-VM-SKUs mit automatischer Skalierung (ein virtueller Kern), die schnellere Bereitstellungszeiten bieten (weniger als 30 Minuten) und aktuell nur zwei virtuelle Computer erfordern, die in ein kostenloses Azure-Testabonnement passen.

- [Klein-bis-Mittel](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-small2mid-noha.json): Unterstützt bis zu 1.000 gleichzeitige Benutzer. Diese Bereitstellung verwendet NFS (keine Hochverfügbarkeit) und MySQL (acht virtuelle Kerne) ohne andere Optionen wie elastische Suche oder Redis Cache.

- [Groß (Hochverfügbarkeit)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-large-ha.json): Unterstützt mehr als 2.000 gleichzeitige Benutzer. Diese Bereitstellung verwendet Azure Files, MySQL (16 virtuelle Kerne) und Redis Cache ohne andere Optionen wie elastische Suche.

- [Maximum](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-maximal.json): Diese maximale Bereitstellung verwendet Azure Files, MySQL mit der höchsten SKU, Redis Cache, elastische Suche (drei virtuelle Computer) und große Speichergrößen (sowohl Datenträger als auch Datenbanken).

Wählen Sie **Start** aus, um eine der vordefinierten Vorlagen bereitzustellen. Hierdurch gelangen Sie zum Azure-Portal, wo Sie obligatorische Felder wie **Abonnement**, **Ressourcengruppen**, [**SSH-Schlüssel**](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) und **Region** eintragen müssen.

![Benutzerdefinierte Bereitstellung: Stellen Sie aus einer benutzerdefinierten Vorlage bereit.](images/custom-deployment.png)

Mit den obigen vordefinierten Vorlagen werden die Standardversionen bereitgestellt.

```bash
Ubuntu: 18.04-LTS
PHP: 7.4
Moodle: 3.8
```

Wenn die PHP- und Moodle-Versionen gegenüber der lokalen Version im Rückstand sind, aktualisieren Sie die Versionen mit den folgenden Schritten:

- Wählen Sie auf der Seite **Benutzerdefinierte Bereitstellung** die Option **Vorlage bearbeiten** aus.

![Vorlage bearbeiten: Bearbeiten Sie Ihre Azure Resource Manager-Vorlage.](images/edit-template.png)

- Fügen Sie im Abschnitt **Ressourcen** dem Block **Parameter** die Moodle- und PHT-Versionen hinzu.

    ```json
    "phpVersion":       { "value": "7.2" },
    "moodleVersion":    { "value": "MOODLE_38_STABLE"}
    ```

- Für Moodle 3.9 sollte der Wert `MOODLE_39_STABLE` sein.

- Wählen Sie **Speichern**, um Ihre Änderungen zu speichern.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit [Moodle-Migrationsressourcen](./migration-resources.md) fort, wo Sie weitere Informationen zum Moodle-Migrationsprozess finden.
