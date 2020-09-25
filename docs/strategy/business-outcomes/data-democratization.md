---
title: Demokratisierung von Daten
description: Optimieren Sie Ihr Unternehmen mit Dateninnovationen und einem zentralen Datenrepository.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/22/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 81beb5d31a39b6c61c4d9c26649cd55a9c86b16b
ms.sourcegitcommit: 4e12d2417f646c72abf9fa7959faebc3abee99d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90774254"
---
# <a name="data-democratization"></a>Demokratisierung von Daten

Viele Unternehmen verfügen über Data Warehouses in ihren Rechenzentren, die verschiedenen Teilen des Unternehmens beim Analysieren von Daten und Treffen von Entscheidungen helfen. Vertriebs-, Marketing- und Finanzabteilungen verlassen sich bei der Erstellung von Standardberichten und -dashboards auf diese Systeme. Darüber hinaus beschäftigen Unternehmen Business Analysts, die Ad-hoc-Abfragen und Analysen für Daten in Data Marts ausführen. Diese Data Marts verwenden Self-Service-Business-Intelligence-Tools, um mehrdimensionale Analysen durchzuführen.

Ein Unternehmen, das Dateninnovationen und einen modernen Datenbestand nutzt, kann eine große Bandbreite von Mitwirkenden unterstützen, von Beteiligten im IT-Bereich bis hin zu Datenexperten und weiteren Personen. Diese können dieses Repository mit zentralisierten Daten, das häufig als „Single Source of Truth“ bezeichnet wird, als Handlungsgrundlage verwenden.

Azure Synapse Analytics ist ein einzelner Dienst für nahtlose Zusammenarbeit und schnelleren Erkenntnisgewinn. Damit Sie diesen Dienst besser verstehen, sollten Sie sich zunächst mit den verschiedenen Rollen und Fertigkeiten im Zusammenhang mit einem typischen Datenbestand befassen:

**Data Warehousing**: *Datenbankadministratoren* unterstützen die Verwaltung von Data Lakes und Data Warehouses, wobei Workloads intelligent optimiert und Daten automatisch gesichert werden.

**Datenintegration**: *Data Engineers* nutzen eine codefreie Umgebung, um problemlos mehrere Quellen und Datentypen zu verbinden.

**Big Data und maschinelles Lernen**: *Data Scientists* erstellen schnell Proofs of Concept und stellen Ressourcen nach Bedarf bereit. Dabei arbeiten sie in der Sprache ihrer Wahl (z. B. T-SQL, Python, Scala, .NET oder Spark SQL).

**Verwaltung und Sicherheit:** *IT-Profis* schützen und verwalten Daten effizienter, setzen Datenschutzanforderungen durch und sichern den Zugriff auf Cloud- und Hybridkonfigurationen.

**Business Intelligence**: *Business Analysts* greifen sicher auf Datasets zu, erstellen Dashboards und geben Daten innerhalb und außerhalb ihrer Organisation frei.

Das folgende Diagramm zeigt ein Beispiel für eine klassische Data-Warehouse-Architektur. Hier werden bekannte strukturierte Daten aus wichtigen Transaktionsverarbeitungssystemen extrahiert und in einen Stagingbereich kopiert. Dort werden sie bereinigt, transformiert und in Produktionstabellen in einem Data Warehouse integriert. Häufig werden hier historische Transaktionsdaten für mehrere Jahre inkrementell gespeichert. So werden die Daten zur Verfügung gestellt, die erforderlich sind, um Änderungen beim Umsatz, dem Kaufverhalten von Kunden und der Kundensegmentierung im zeitlichen Verlauf zu verstehen. Ebenfalls bereitgestellt werden eine jährliche Finanzberichterstattung und -analyse als Hilfe bei der Entscheidungsfindung.

Von dort werden Teilmengen von Daten in Data Marts extrahiert, um Aktivitäten in Zusammenhang mit einem bestimmten Geschäftsprozess zu analysieren. Dies ist hilfreich bei der Entscheidungsfindung in bestimmten Teilen des Unternehmens.

![Diagramm des klassischen Data Warehouse](../../_images/analytics/the-classic-data-warehouse.png)

Damit ein Unternehmen effizient arbeiten kann, benötigt es alle Arten von Daten zu den oben beschriebenen verschiedenen Fertigkeiten und Rollen. Sie brauchen Rohdaten, die bereinigt wurden, damit Data Scientists Machine Learning-Modelle erstellen können. Sie benötigen bereinigte und strukturierte Daten, damit ein Data Warehouse eine zuverlässige Leistung für Geschäftsanwendungen und Dashboards bietet. Vor allem müssen Sie in der Lage sein, in wenigen Minuten und nicht in Tagen von Rohdaten zu Erkenntnissen zu gelangen.

Azure Synapse Analytics verfügt mit Power BI über ein natives, integriertes Business-Intelligence-Tool. Dadurch können Sie basierend auf Rohdaten in nur wenigen Minuten ein Dashboard mit Erkenntnissen vollständig erstellen und müssen dafür nur einen Dienst über eine einzige Schnittstelle verwenden.
