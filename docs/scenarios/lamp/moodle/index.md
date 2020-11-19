---
title: Übersicht über eine manuelle Moodle-Migration
description: Hier finden Sie eine Übersicht über eine manuelle Moodle-Migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 729304a79e26ef5461b2186a14b73d48cd11b45b
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94714400"
---
# <a name="overview-of-a-manual-moodle-migration"></a>Übersicht über eine manuelle Moodle-Migration

In diesem Dokument wird erläutert, wie Sie eine Moodle-Anwendung aus einer lokalen Umgebung zu Azure migrieren. Für jeden Schritt gibt es zwei Ansätze:

- Bei einem Ansatz können Sie das Azure-Portal verwenden.
- Beim anderen Ansatz können Sie die gleichen Aufgaben mit der Befehlszeile unter Verwendung der Azure CLI ausführen.

## <a name="prerequisites"></a>Voraussetzungen

Wenn die Versionen des lokal bereitgestellten Softwarestapels nicht den in diesem Leitfaden unterstützten Versionen entsprechen, wird erwartet, dass die lokalen Versionen auf die in diesem Handbuch aufgeführten Versionen aktualisiert/gepatcht werden.

- Zugriff auf die lokale Infrastruktur ist erforderlich, damit ein Backup der Moodle-Bereitstellung und -Konfigurationen (einschließlich der Datenbankkonfigurationen) erstellt werden können.
- Vor der Migration sollten ein Azure-Abonnement und ein Azure Blob Storage-Konto erstellt werden.
- Öffnen Sie die Azure CLI und AzCopy für die Verwendung im gesamten Prozess.
- Legen Sie für die Moodle-Website den **Wartungsmodus** fest.

Dieser Migrationsleitfaden unterstützt die folgenden Softwareversionen:

- Ubuntu 18.04 LTS
- Nginx 1.14
- Datenbankserver mit MySQL 5.6, 5.7 oder 8.0. In diesem Leitfaden wird Azure Database for MySQL verwendet.
- PHP 7.2, 7.3 oder 7.4.
- Moodle 3.8 und 3

## <a name="when-to-use-azure-resource-manager-template-for-moodle-migrations"></a>Verwenden von Azure Resource Manager-Vorlagen für die Moodle-Migration

Bei der Migration von Moodle mit einer Azure Resource Manager-Vorlage wird die Infrastruktur in Azure erstellt. Nach der Erstellung der Infrastruktur werden der Moodle-Softwarestapel und zugehörige Abhängigkeiten migriert.

## <a name="moodle-migration-tasks"></a>Moodle-Migrationsaufgaben

Die Schritte zum Migrieren einer Moodle-Anwendung zu Azure werden in die folgenden drei Aufgaben unterteilt:

1. Vor der Migration
1. Die praktischen Schritte zum Migrieren der Anwendung
1. Nach der Migration

## <a name="next-steps"></a>Nächste Schritte

Unter [Vorbereiten auf eine Moodle-Migration](./migration-pre.md) finden Sie vorläufige Informationen zum Moodle-Migrationsprozess.
