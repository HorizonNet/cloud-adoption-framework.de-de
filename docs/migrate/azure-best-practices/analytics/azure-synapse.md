---
title: Hochverfügbarkeit für Azure Synapse Analytics
description: Verwenden Sie Azure Synapse-Features, um Anforderungen hinsichtlich Hochverfügbarkeit und Notfallwiederherstellung zu erfüllen.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: fb75af110c980a718d1050441d7e64426ffb30a0
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452583"
---
# <a name="high-availability-for-azure-synapse-analytics"></a>Hochverfügbarkeit für Azure Synapse Analytics

Einer der Hauptvorteile einer modernen, cloudbasierten Infrastruktur wie Microsoft Azure ist, dass Features für Hochverfügbarkeit und Notfallwiederherstellung integriert und einfach zu implementieren und anzupassen sind. Diese Einrichtungen sind oft kostengünstiger als die entsprechende Funktionalität in einer lokalen Umgebung. Die Verwendung dieser integrierten Funktionen bedeutet auch, dass die Sicherungs- und Wiederherstellungsmechanismen im vorhandenen Legacy-Data Warehouse nicht migriert werden müssen.

In den folgenden Abschnitten werden die Standardfeatures von Azure Synapse Analytics beschrieben, mit denen Anforderungen für Hochverfügbarkeit und Notfallwiederherstellung erfüllt werden.

## <a name="high-availability-ha"></a>Hochverfügbarkeit

Azure Synapse Analytics verwendet Datenbankmomentaufnahmen, um hohe Verfügbarkeit des Warehouse zu gewährleisten. Mit einer Data Warehouse-Momentaufnahme wird ein Wiederherstellungspunkt erstellt, mit dessen Hilfe ein vorheriger Zustand eines Data Warehouse wiederhergestellt oder kopiert werden kann. Da Azure Synapse Analytics ein verteiltes System ist, besteht eine Data Warehouse-Momentaufnahme aus zahlreichen Dateien, die in Azure Storage gespeichert sind. Momentaufnahmen erfassen inkrementelle Änderungen der Daten, die in Ihrem Data Warehouse gespeichert sind.

Azure Synapse Analytics erstellt im Lauf des Tages automatisch Momentaufnahmen, und die generierten Wiederherstellungspunkte sind für sieben Tage verfügbar. Dieser Aufbewahrungszeitraum kann nicht geändert werden. Azure Synapse Analytics unterstützt eine RPO (Recovery Point Objective) von acht Stunden. Ein Data Warehouse kann in der primären Region anhand einer beliebigen Momentaufnahme wiederhergestellt werden, die in den vergangenen sieben Tagen erstellt wurde.

Es werden auch benutzerdefinierte Wiederherstellungspunkte unterstützt, sodass Momentaufnahmen manuell ausgelöst werden können, um Wiederherstellungspunkte eines Data Warehouse vor und nach großen Änderungen zu erstellen. Diese Funktion gewährleistet die logische Konsistenz von Wiederherstellungspunkten und sorgt somit für zusätzlichen Datenschutz und eine schnelle Wiederherstellung bei Workloadunterbrechungen oder Benutzerfehlern.

## <a name="disaster-recovery-dr"></a>Notfallwiederherstellung

Zusätzlich zu den oben beschriebenen Momentaufnahmen führt Azure Synapse Analytics auch standardmäßig einmal pro Tag eine Geosicherung in einem gekoppelten Rechenzentrum aus. Die RPO für eine Geowiederherstellung beträgt 24 Stunden. Sie können die Geosicherung auf einem Server in einer beliebigen anderen Region wiederherstellen, in der Azure Synapse Analytics unterstützt wird. Durch eine Geosicherung wird gewährleistet, dass ein Data Warehouse wiederhergestellt werden kann, falls die Wiederherstellungspunkte in der primären Region nicht verfügbar sind.
