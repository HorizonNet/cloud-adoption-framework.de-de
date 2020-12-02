---
title: Übersicht über die manuelle Moodle-Migration
description: In diesem Artikel werden die Voraussetzungen und allgemeinen Schritte für die manuelle Moodle-Migration aus einer lokalen Umgebung zu Azure beschrieben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/30/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: e3d34cfec94f42873ab109a4ab9cbdc4f3acfc8b
ms.sourcegitcommit: 18f3ee8fcd8838f649cb25de1387b516aa23a5a0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/30/2020
ms.locfileid: "96327796"
---
# <a name="overview-of-moodle-manual-migration"></a>Übersicht über die manuelle Moodle-Migration

[Moodle](https://moodle.org/) ist ein kostenloses Open-Source-Verwaltungssystem für Lernkurse, das in PHP geschrieben wurde. In dieser Anleitung wird erläutert, wie Sie die Moodle-Anwendung aus einer lokalen Umgebung zu Azure migrieren. In dieser Anleitung finden Sie Schritte für zwei verschiedene Ansätze, die jeweils das Azure-Portal oder die Azure CLI verwenden.

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit der Migration beginnen, müssen die folgenden Voraussetzungen erfüllt werden:

- Die lokale Software wurde auf die folgenden Versionen aktualisiert und gepatcht:
  - Ubuntu 18.04 LTS
  - Nginx 1.14
  - Datenbankserver mit MySQL 5.6, 5.7 oder 8.0. In dieser Anleitung wird Azure Database for MySQL verwendet.
  - PHP 7.2, 7.3 oder 7.4.
  - Moodle 3.8 oder Moodle 3
- Ihre Moodle-Website muss sich im **Wartungsmodus** befinden.
- Sie benötigen Zugriff auf die lokale Infrastruktur, um [die Moodle-Bereitstellung und -Konfigurationen (einschließlich der Datenbankkonfigurationen) zu sichern](migration-pre.md#back-up-on-premises-data).
- Die [Azure CLI](migration-pre.md#install-the-azure-cli) und [AzCopy](migration-pre.md#download-and-install-azcopy) müssen lokal installiert sein.
- Sie benötigen außerdem ein [Azure-Abonnement](migration-pre.md#create-a-subscription) und ein [Azure Blob Storage-Konto](migration-pre.md#create-a-storage-account).

## <a name="moodle-migration-process"></a>Moodle-Migrationsprozess

Bei der Migration von Moodle mit einer ARM-Vorlage (Azure Resource Manager) wird die Infrastruktur in Azure erstellt, und dann werden der Moodle-Softwarestapel und zugehörige Abhängigkeiten migriert.

Die Schritte für die Migration von Moodle zu Azure wird in die folgenden drei Phasen unterteilt:

1. [Vor der Migration](migration-pre.md)
1. [Anwendungsmigration](migration-start.md)
1. [Nach der Migration](migration-post.md)

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit der [Vorbereitung einer Moodle-Migration](./migration-pre.md) fort.
