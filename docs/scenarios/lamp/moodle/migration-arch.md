---
title: Architektur und Vorlagen für die Moodle-Migration
description: Hier erfahren Sie mehr über die ARM-Vorlagen (Azure Resource Manager) für die Bereitstellung der Azure-Infrastruktur für Moodle sowie die Bereitstellung oder Bearbeitung dieser Vorlagen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/23/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 9d49871341d58d6a9198c9751ed5ed3541b97cca
ms.sourcegitcommit: 1d7b16eb710bed397280fb8f862912c78f2254ee
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/24/2020
ms.locfileid: "95812358"
---
# <a name="moodle-migration-architecture-and-templates"></a>Architektur und Vorlagen für die Moodle-Migration

Die Moodle-Migration umfasst die folgenden Aufgaben:

1. Bereitstellen der Azure-Infrastruktur mit ARM-Vorlagen (Azure Resource Manager)
1. [Herunterladen und Installieren von AzCopy](migration-start.md#download-and-install-azcopy-on-the-controller-vm)
1. [Kopieren des Moodle-Sicherungsarchivs auf die Controller-VM-Instanz](migration-start.md#copy-the-archive-to-the-controller-vm) bei der Azure Resource Manager-Bereitstellung
1. [Migrieren der Moodle-Anwendung und -Konfiguration](migration-start.md#import-the-moodle-database-to-azure)
1. [Einrichten der Moodle-Controllerinstanz und der Workerknoten](azure-infra-config.md)
1. [Konfigurieren von PHP und des Webservers](azure-infra-config.md)

In diesem Artikel werden die Azure-Infrastrukturoptionen für Moodle beschrieben, und es wird erläutert, wie Sie die gewünschten Azure-Ressourcen mithilfe der von Ihnen gewählten ARM-Vorlagen bereitstellen.

## <a name="azure-infrastructure"></a>Azure-Infrastruktur

Das folgende Diagramm zeigt eine Übersicht über die Azure-Infrastrukturressourcen für Moodle:

![Diagramm mit Azure-Infrastrukturressourcen](images/architecture.png)

## <a name="arm-template-options"></a>ARM-Vorlagenoptionen

Sie können entweder eine vollständig konfigurierbare ARM-Vorlage oder eine von mehreren vordefinierten ARM-Vorlagen verwenden, um Moodle-Ressourcen in Azure bereitzustellen. Eine vollständig konfigurierbare Bereitstellung bietet Ihnen am meisten Flexibilität und Auswahlmöglichkeiten für die Bereitstellung. Die vollständig konfigurierbare Vorlage sowie die vordefinierten Vorlagen finden Sie im [Moodle-GitHub-Repository](https://github.com/Azure/Moodle).

Eine vordefinierte Bereitstellungsvorlage verwendet eine von vier vordefinierten Moodle-Größen: minimal, klein bis mittel, groß oder maximal.

- Bei einer *minimalen Bereitstellung* sind nur zwei virtuelle Computer (VMs) erforderlich, sodass sie mit einem kostenlosen Azure-Testabonnement verwendet werden kann. Bei dieser Bereitstellung werden das Network File System (NFS), MySQL und eine kleinere automatisch skalierende Web-Front-End-VM-SKU mit einem virtuellen Kern verwendet. Diese Vorlage verfügt über eine schnelle Bereitstellungszeit von weniger als 30 Minuten.
  
  [![Schaltfläche, die die ARM-Vorlage für eine minimale Moodle-Bereitstellung startet](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-minimal.json)

- Bei einer *kleinen bis mittleren Bereitstellung* werden bis zu 1.000 gleichzeitige Benutzer unterstützt. Bei dieser Bereitstellung werden das NFS ohne Hochverfügbarkeit und MySQL auf acht virtuellen Kernen verwendet. Diese Bereitstellung umfasst keine Optionen wie Elasticsearch oder Redis Cache.
  
  [![Schaltfläche, die die ARM-Vorlage für eine kleine bis mittlere Moodle-Bereitstellung startet](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-small2mid-noha.json)

- Bei einer *großen Bereitstellung mit Hochverfügbarkeit* werden mehr als 2.000 gleichzeitige Benutzer unterstützt. Diese Bereitstellung verwendet Azure Files, MySQL mit 16 virtuellen Kernen und Redis Cache ohne andere Optionen wie Elasticsearch.
  
  [![Schaltfläche, die die ARM-Vorlage für eine große Moodle-Bereitstellung mit Hochverfügbarkeit startet](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-large-ha.json)

- Bei einer *maximalen* Bereitstellung werden Azure Files, MySQL mit der höchsten SKU, Redis Cache, Elasticsearch auf drei VMs und große Speichergrößen sowohl für Datenträger als auch für Datenbanken verwendet.
  
  [![Schaltfläche, die die ARM-Vorlage für eine maximale Moodle-Bereitstellung startet](images/deploy-to-azure.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FMoodle%2Fmaster%2Fazuredeploy-maximal.json)

## <a name="deploy-the-template"></a>Bereitstellen der Vorlage

So stellen Sie eine der vordefinierten ARM-Vorlagen bereit:

1. Klicken Sie im vorherigen Abschnitt auf die Schaltfläche **Deploy to Azure** (In Azure bereitstellen) für die gewünschte Bereitstellung. Dadurch gelangen Sie zum Azure-Portal.
   
1. Füllen Sie im Azure-Portal auf der Seite **Benutzerdefinierte Bereitstellung** die Pflichtfelder **Abonnement**, **Ressourcengruppe**, **Region** und **Öffentlicher SSH-Schlüssel** aus. Weitere Informationen zum Hinzufügen des SSH-Schlüssels finden Sie unter [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) (Generieren eines neuen SSH-Schlüssels und Hinzufügen dieses Schlüssels zu ssh-agent).
   
   :::image type="content" source="images/custom-deployment.png" alt-text="Screenshot: Bildschirm „Benutzerdefinierte Bereitstellung“ in Azure für eine ARM-Vorlage für die Moodle-Bereitstellung" border="false":::
   
1. Klicken Sie auf **Überprüfen + erstellen**.

### <a name="edit-the-template"></a>Bearbeiten der Vorlage

Die vordefinierten ARM-Vorlagen stellen die folgenden Standardsoftwareversionen bereit:

- Ubuntu: 18.04 LTS
- PHP: 7.4
- Moodle: 3.8

Wenn es sich bei Ihrer lokalen PHP- und Moodle-Version nicht um die obige handelt, führen Sie die folgenden Schritte aus, um die Versionen in den Vorlagen entsprechend zu aktualisieren:

1. Klicken Sie im Azure-Portal auf der Seite **Benutzerdefinierte Bereitstellung** für die ARM-Vorlage auf die Option **Vorlage bearbeiten**.
   
1. Fügen Sie im Abschnitt **resources** der Vorlage unter **parameters** Parameter für Ihre Moodle- und PHP-Version hinzu.

   ```json
   "phpVersion":       { "value": "7.2" },
   "moodleVersion":    { "value": "MOODLE_38_STABLE"}
   ```
   
   Für Moodle 3.9 sollte der Wert für `moodleVersion` beispielsweise `MOODLE_39_STABLE` sein.
   
   :::image type="content" source="images/edit-template.png" alt-text="Screenshot: Seite „Vorlage bearbeiten“ für eine ARM-Vorlage für die Bereitstellung von Moodle" border="false":::
   
1. Wählen Sie **Speichern** aus.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den Ressourcen, die mit der ARM-Vorlage in Azure bereitgestellt werden, finden Sie unter [Moodle-Migrationsressourcen](migration-resources.md).
