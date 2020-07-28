---
title: Analyselösungen für Exadata
description: Verwenden Sie das Cloud Adoption Framework für Azure, um mehr über Analyselösungen mit Exadata zu erfahren.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9f2812dcdc09e0ff0a5403003384faa997b185ca
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452590"
---
<!-- cSpell:ignore Exadata SSMA -->

# <a name="analytics-solutions-for-exadata"></a>Analyselösungen für Exadata

## <a name="migrating-an-oracle-data-warehouse-schema-to-azure-synapse-analytics"></a>Migrieren eines Oracle-Data Warehouse-Schemas zu Azure Synapse Analytics

Beim Schema gibt es diverse Unterschiede zwischen einem Oracle-Data Warehouse und Azure Synapse Analytics. Diese schließen unter anderem Datenbanken, Datentypen und einige Oracle-Datenbankobjekttypen ein, die in Azure Synapse Analytics nicht unterstützt werden.

Wenn Sie ein Oracle-Data Warehouse zu Azure Synapse migrieren, werden Sie genau wie bei anderen Datenbankverwaltungssystemen feststellen, dass in Oracle mehrere separate Datenbanken vorhanden sind, während in Azure Synapse nur eine einzelne Datenbank vorhanden ist. Daher ist unter Umständen eine neue Benennungskonvention (beispielsweise eine Verkettung von Oracle-Schemanamen und -Tabellennamen) erforderlich, um Tabellen und Sichten aus der Stagingdatenbank, aus der Produktionsdatenbank und aus den Data Mart-Datenbanken Ihres Oracle-Data Warehouse zu Azure Synapse zu migrieren.

Darüber hinaus werden diverse Oracle-Datenbankobjekte nicht unterstützt. Beispiele wären etwa Oracle-Bitmapindizes, funktionsbasierte Indizes und Domänenindizes. Gleiches gilt für gruppierte Oracle-Tabellen, Trigger auf Zeilenebene, benutzerdefinierte Datentypen und gespeicherte PL/SQL-Prozeduren. Diese Objekte können durch Abfragen verschiedener Oracle-Systemkatalogtabellen und -sichten ermittelt werden. In einigen Fällen lässt sich das Problem umgehen. In Azure Synapse können beispielsweise andere Indextypen oder Partitionierungen verwendet werden, um die nicht unterstützten Indextypen in Oracle zu umgehen. Unter Umständen können anstelle von gruppierten Oracle-Tabellen auch materialisierte Sichten verwendet werden, und von Migrationstools wie SQL Server Migration Assistant für Oracle kann zumindest ein Teil von PL/SQL übersetzt werden.

Darüber hinaus müssen bei der Schemamigration auch Datentypunterschiede für Spalten berücksichtigt werden. Die Spalten in Ihrem Oracle-Data Warehouse-Schema und in Ihrem Data Mart-Schema, für die keine Zuordnung zu Datentypen in Azure Synapse vorhanden ist, können durch Abfragen des Oracle-Katalogs ermittelt werden. Für einige dieser Fälle ist eine Umgehungslösung verfügbar.

Hinsichtlich der Verwaltung oder Verbesserung der Leistung Ihres Schemas nach der Migration sollten Sie sich die aktuell verwendeten Leistungsmechanismen (etwa die Oracle-Indizierung) ansehen. Bitmapindizes, die häufig von Abfragen in Oracle genutzt werden, können beispielsweise darauf hindeuten, dass im migrierten Schema in Azure Synapse ein nicht gruppierter Index erstellt werden sollte. In Azure Synapse empfiehlt es sich unter anderem, zu verknüpfende Daten mithilfe der Datenverteilung auf dem gleichen Verarbeitungsknoten zu platzieren und sicherzustellen, dass die zu verknüpfenden Datentypen der Spalten identisch sind. Dadurch wird die Verknüpfungsverarbeitung optimiert, indem weniger Daten transformiert werden müssen. Für Azure Synapse muss häufig nicht jeder Oracle-Index migriert werden, da andere Features zur Verfügung stehen, um eine hohe Leistung zu erzielen. Hierzu zählen die parallele Abfrageverarbeitung, In-Memory-Daten, die Zwischenspeicherung von Resultsets sowie Datenverteilungsoptionen zur Verringerung von E/A-Vorgängen.

Es gibt verschiedene Tools, die Sie bei der Migration eines Oracle-Data Warehouse oder Data Marts zu Azure Synapse unterstützen. Zu diesen Tools zählt beispielsweise SQL Server Migration Assistant (SSMA) für Oracle. Dieses Tool wurde entwickelt, um die Migration von Tabellen, Sichten und Daten aus vorhandenen Oracle-Umgebungen zu automatisieren. Von SSMA werden unter anderem Indextypen und Datenverteilungen für Azure Synapse-Zieltabellen empfohlen und Datentypzuordnungen während der Migration angewendet. SSMA eignet sich gut für kleinere Tabellen, ist bei sehr großen Datenmengen jedoch nicht die effizienteste Methode.

## <a name="next-steps"></a>Nächste Schritte

<!-- TODO: Add actionable next step -->
