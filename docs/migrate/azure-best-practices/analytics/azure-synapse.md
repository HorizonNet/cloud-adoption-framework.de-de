---
title: Hochverfügbarkeit für Azure Synapse Analytics
description: Verwenden Sie Azure Synapse Analytics-Features, um Anforderungen hinsichtlich Hochverfügbarkeit und Notfallwiederherstellung zu erfüllen.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 93b7a66a1c30ec4975a2cef092b54f56023eed0a
ms.sourcegitcommit: 163e703d9cbf90b26d96087c836a9cbd94fc7e35
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963280"
---
# <a name="high-availability-for-azure-synapse-analytics"></a>Hochverfügbarkeit für Azure Synapse Analytics

Einer der Hauptvorteile einer modernen, cloudbasierten Infrastruktur wie Microsoft Azure ist, dass Features für Hochverfügbarkeit (High Availability, HA) und Notfallwiederherstellung (Disaster Recovery, DR) integriert und einfach zu implementieren und anzupassen sind. Diese Einrichtungen sind oft kostengünstiger als die entsprechende Funktionalität in einer lokalen Umgebung. Die Verwendung dieser integrierten Funktionen bedeutet auch, dass die Sicherungs- und Wiederherstellungsmechanismen im vorhandenen Data Warehouse nicht migriert werden müssen.

In den folgenden Abschnitten werden die Standardfeatures von Azure Synapse Analytics beschrieben, mit denen Anforderungen für Hochverfügbarkeit und Notfallwiederherstellung erfüllt werden.

## <a name="high-availability"></a>Hochverfügbarkeit

Azure Synapse Analytics verwendet Datenbankmomentaufnahmen, um hohe Verfügbarkeit des Warehouse zu gewährleisten. Mit einer Data Warehouse-Momentaufnahme wird ein Wiederherstellungspunkt erstellt, mit dessen Hilfe ein vorheriger Zustand eines Data Warehouse wiederhergestellt oder kopiert werden kann. Da Azure Synapse Analytics ein verteiltes System ist, besteht eine Data Warehouse-Momentaufnahme aus zahlreichen Dateien, die in Azure Storage gespeichert sind. Momentaufnahmen erfassen inkrementelle Änderungen der Daten, die in Ihrem Data Warehouse gespeichert sind.

Azure Synapse Analytics erstellt im Lauf des Tages automatisch Momentaufnahmen, um Wiederherstellungspunkte zu generieren, die für sieben Tage verfügbar sind. Dieser Aufbewahrungszeitraum kann nicht geändert werden. Azure Synapse Analytics unterstützt eine RPO (Recovery Point Objective) von acht Stunden. Sie können das Data Warehouse in der primären Region anhand einer beliebigen Momentaufnahme wiederherstellen, die in den vergangenen sieben Tagen erstellt wurde.

Der Dienst unterstützt auch benutzerdefinierte Wiederherstellungspunkte. Durch das manuelle Auslösen von Momentaufnahmen können Wiederherstellungspunkte eines Data Warehouse vor und nach großen Änderungen erstellt werden. Mit dieser Funktion wird sichergestellt, dass Wiederherstellungspunkte logisch konsistent sind. Die logische Konsistenz bietet zusätzlichen Datenschutz vor Workloadunterbrechungen oder Benutzerfehlern für die schnelle Wiederherstellungszeit.

## <a name="disaster-recovery"></a>Notfallwiederherstellung

Zusätzlich zu den zuvor beschriebenen Momentaufnahmen führt Azure Synapse Analytics auch standardmäßig einmal pro Tag eine Geosicherung in einem gekoppelten Rechenzentrum aus. Die RPO für eine Geowiederherstellung beträgt 24 Stunden. Sie können die Geosicherung auf einem Server in einer beliebigen anderen Region wiederherstellen, in der Azure Synapse Analytics unterstützt wird. Durch eine Geosicherung wird gewährleistet, dass ein Data Warehouse wiederhergestellt werden kann, falls die Wiederherstellungspunkte in der primären Region nicht verfügbar sind.
