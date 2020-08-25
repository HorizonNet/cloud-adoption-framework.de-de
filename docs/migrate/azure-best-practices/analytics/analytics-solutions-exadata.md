---
title: Azure Synapse Analytics-Migration für Oracle-Data Warehouse
description: Verwenden Sie das Cloud Adoption Framework für Azure, um mehr über die Migration eines Oracle-Data Warehouse-Schemas zu Azure Synapse Analytics zu erfahren.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0c89967ac5cb815ad771e6a9ee70cad2f97056db
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88570826"
---
<!-- cSpell:ignore Exadata SSMA -->

# <a name="azure-synapse-analytics-solutions-and-migration-for-an-oracle-data-warehouse"></a>Azure Synapse Analytics-Lösungen und Migration für ein Oracle-Data Warehouse

Ein Oracle-Data Warehouse-Schema unterscheidet sich in mehrfacher Hinsicht von Azure Synapse Analytics. Zu den Unterschieden gehören Datenbanken, Datentypen und eine Reihe von Oracle-Datenbankobjekttypen, die in Azure Synapse nicht unterstützt werden.

Wie bei anderen Datenbankmanagementsystemen auch, werden Sie bei der Migration eines Oracle-Data Warehouse zu Azure Synapse feststellen, dass Oracle über mehrere, separate Datenbanken und Azure Synapse nur über eine Datenbank verfügt. Möglicherweise müssen Sie eine neue Benennungskonvention (z. B. eine Verkettung von Oracle-Schemanamen und -Tabellennamen) verwenden, um Tabellen und Sichten aus der Stagingdatenbank, aus der Produktionsdatenbank und aus den Data Mart-Datenbanken Ihres Oracle-Data Warehouse zu Azure Synapse zu migrieren.

In Azure Synapse werden mehrere Oracle-Datenbankobjekte nicht unterstützt. Zu den Datenbankobjekten, die in Azure Synapse nicht unterstützt werden, gehören Oracle-Bitmapindizes, funktionsbasierte Indizes, Domänenindizes, Oracle-Clustertabellen, Trigger auf Zeilenebene, benutzerdefinierte Datentypen und gespeicherte PL/SQL-Prozeduren. Diese Objekte können durch Abfragen verschiedener Oracle-Systemkatalogtabellen und -sichten ermittelt werden. In einigen Fällen können Sie Problemumgehungen verwenden. In Azure Synapse können Sie z. B. die Partitionierung oder andere Indextypen verwendet werden, um die nicht unterstützten Indextypen in Oracle zu umgehen. Möglicherweise können Sie anstelle von gruppierten Oracle-Tabellen auch materialisierte Sichten verwenden, und mit Migrationstools wie SQL Server Migration Assistant für Oracle kann zumindest ein Teil von PL/SQL übersetzt werden.

Wenn Sie ein Oracle-Data Warehouse-Schema migrieren, müssen Sie auch Datentypunterschiede in Spalten berücksichtigen. Die Spalten in Ihrem Oracle-Data Warehouse- und Data Mart-Schema, für die keine Zuordnung zu Datentypen in Azure Synapse vorhanden ist, können durch Abfragen des Oracle-Katalogs ermittelt werden. Für einige dieser Fälle können Sie eine Umgehungslösung verwenden.

Um die Leistung Ihres Schemas nach der Migration beizubehalten oder zu verbessern, sollten Sie die derzeit verwendeten Leistungsmechanismen (z. B. die Oracle-Indizierung) in Betracht ziehen. Beispielsweise könnten die von Oracle-Abfragen häufig verwendeten Bitmapindizes darauf hinweisen, dass die Erstellung eines nicht gruppierten Index im migrierten Schema in Azure Synapse vorteilhaft wäre.

Eine geeignete Methode bei Azure Synapse umfasst die Verwendung der Datenverteilung, um die zu verknüpfenden Daten auf demselben Verarbeitungsknoten zusammenzustellen. Eine weitere bewährte Methode bei Azure Synapse ist die Sicherstellung, dass die Datentypen der zu verknüpfenden Spalten identisch sind. Die Verwendung von identisch verknüpften Spalten optimiert die Verknüpfungsverarbeitung, da weniger Daten für den Abgleich transformiert werden müssen. In Azure Synapse ist es oft nicht erforderlich, jeden Oracle-Index zu migrieren, da andere Features eine hohe Leistung bieten. Stattdessen können Sie die parallele Abfrageverarbeitung, In-Memory-Daten, die Zwischenspeicherung von Resultsets sowie Datenverteilungsoptionen zur Verringerung von E/A-Vorgängen verwenden.

SSMA für Oracle kann Ihnen helfen, ein Oracle-Data Warehouse oder -Data Mart zu Azure Synapse zu migrieren. SSMA wurde entwickelt, um den Prozess der Migration von Tabellen, Sichten und Daten aus einer bestehenden Oracle-Umgebung zu automatisieren. Von SSMA werden unter anderem Indextypen und Datenverteilungen für Azure Synapse-Zieltabellen empfohlen und Datentypzuordnungen während der Migration angewendet. SSMA eignet sich gut für kleinere Tabellen, ist bei sehr großen Datenmengen jedoch nicht die effizienteste Methode.
