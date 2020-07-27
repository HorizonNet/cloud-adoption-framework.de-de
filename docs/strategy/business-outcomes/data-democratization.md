---
title: Demokratisierung von Daten
description: Statten Sie Unternehmen mit Dateninnovation und einem zentralen Datenrepository als alleingültige Datenquelle aus.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/22/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: d54276568938919f4da117208a5f25154ac9115b
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452619"
---
# <a name="data-democratization"></a>Demokratisierung von Daten

Durch Dateninnovation und einen modernen Datenbestand kann das gesamte Unternehmen vom Projektbeteiligten aus dem IT-Bereich bis hin zum Datenprofi Aktionen über dieses zentrale Datenrepository ausführen, das zur alleingültigen Datenquelle wird.

Heute verfügen viele Unternehmen schon seit langem über Data Warehouses für Analysezwecke in ihren Rechenzentren, um die Entscheidungsfindung in verschiedenen Bereichen ihres Unternehmens zu unterstützen. Solche Systeme werden insbesondere von den Vertriebs-, Marketing- und Finanzabteilungen zum Erstellen von Standardberichten und Dashboards genutzt. Darüber hinaus werden Business Analysts beauftragt, Ad-hoc-Abfragen und -Analysen von Daten in Data Marts durchzuführen, die für mehrdimensionale Analysen mithilfe von Self-Service-Business Intelligence-Tools (BI) konzipiert sind.  

Azure Synapse Analytics ist ein einzelner Dienst für nahtlose Zusammenarbeit und beschleunigten Erkenntnisgewinn.

**Data Warehousing**: *Datenbankadministratoren* unterstützen die Verwaltung von Data Lakes und Data Warehouses, wobei Workloads intelligent optimiert und Daten automatisch gesichert werden.

**Datenintegration**: *Data Engineers* nutzen eine codefreie Umgebung, um problemlos mehrere Quellen und Datentypen zu verbinden.

**Big Data und Machine Learning**: *Data Scientists* erstellen schnell Proofs of Concept und stellen Ressourcen bei Bedarf bereit, wobei sie in der Sprache Ihrer Wahl arbeiten (T-SQL, Python, Scala, .NET, SparkSQL).

**Verwaltung und Sicherheit**: *IT-Profis* schützen und verwalten Daten effizienter, erfüllen Datenschutzanforderungen und sichern den Zugriff auf Cloud- und Hybridkonfigurationen.

**Business Intelligence**: *Business Analysts* greifen auf sichere Weise auf Datasets zu, erstellen Dashboards und geben Daten innerhalb und außerhalb ihrer Organisation frei.

Ein Beispiel einer klassischen Data Warehouse-Architektur ist in Abbildung 1 dargestellt. Hier werden bekannte strukturierte Daten aus wichtigen Transaktionsverarbeitungssystemen extrahiert, in einen Stagingbereich kopiert, aus dem sie bereinigt werden, transformiert und in Produktionstabellen in einem Data Warehouse integriert. Häufig werden hier historische Transaktionsdaten über mehrere Jahre inkrementell aufgebaut, um die Daten zur Verfügung zu stellen, die erforderlich sind, um Veränderungen beim Umsatz, das Kaufverhalten von Kunden und die Kundensegmentierung im zeitlichen Verlauf zu verstehen und eine jährliche Finanzberichterstattung und -analyse als Hilfe bei der Entscheidungsfindung bereitzustellen. Von dort aus werden Teilmengen von Daten in Data Marts extrahiert, um Aktivitäten zu analysieren, die mit einem bestimmten Geschäftsprozess in Zusammenhang stehen, und so die Entscheidungsfindung in einem bestimmten Teil des Unternehmens zu unterstützen.

![Klassisches Data Warehouse: die wichtigsten Datenquellen für ein Data Warehouse sind Datenbanken für Transaktionsanwendungen](../../_images/analytics/the-classic-data-warehouse.png)

Damit ein Unternehmen effizient arbeiten kann, werden alle Arten von Daten für unterschiedliche Fähigkeiten und Rollen benötigt. Sie brauchen Rohdaten, die bereinigt wurden, damit Data Scientists Machine Learning-Modelle erstellen können. Sie benötigen bereinigte und strukturierte Daten, damit ein Data Warehouse eine zuverlässige Leistung für Geschäftsanwendungen und Dashboards bietet. Vor allem müssen Sie in der Lage sein, in wenigen Minuten und nicht in Tagen von Rohdaten zu Erkenntnissen zu gelangen. Diese Fähigkeit kann nur Azure Synapse bieten. Azure Synapse ist der einzige Analysedienst weltweit, der über ein natives, integriertes Business Intelligence-Tool mit Power BI verfügt, das es ermöglicht, innerhalb von Minuten von Rohdaten zu einem Dashboard mit Erkenntnissen zu gelangen, und das alles mit nur einem Dienst innerhalb einer einzigen Schnittstelle.

## <a name="next-steps"></a>Nächste Schritte

<!-- TODO: More detail needed here. -->

Clouddatenteam
