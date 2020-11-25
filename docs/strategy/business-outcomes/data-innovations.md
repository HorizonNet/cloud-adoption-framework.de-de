---
title: Dateninnovationen
description: Migrieren und modernisieren Sie Ihr Data Warehouse, und erweitern Sie Ihre analytischen Funktionen, um einen neuen Geschäftswert zu erzielen.
author: v-hanki
ms.author: brblanch
ms.date: 07/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 3a12bf2ff26ff28ff7c561badba702bdc064e23d
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996943"
---
# <a name="data-innovations"></a>Dateninnovationen

Viele Unternehmen möchten ihr vorhandenes Data Warehouse in die Cloud migrieren. Motivierende Faktoren dabei sind die folgenden:

- Es muss keine Hardware erworben werden, bzw. es entstehen keine Wartungskosten.
- Es muss keine Infrastruktur verwaltet werden.
- Es kann zu einer sicheren, skalierbaren und kostengünstigen Cloudlösung gewechselt werden.

Der cloudnative Azur-Dienst mit nutzungsbasierter Bezahlung namens Azure Synapse Analytics stellt ein analytisches Datenbankverwaltungssystem für Organisationen zur Verfügung. Azure-Technologien helfen Ihnen, Ihr Data Warehouse nach der Migration zu modernisieren und Ihre analytischen Funktionen zu erweitern, um einen neuen Geschäftswert zu erzielen.

Ein Data Warehouse-Migrationsprojekt beinhaltet viele Komponenten. Dazu gehören Schemas, Daten, ETL-Pipelines (Extrahieren, Transformieren und Laden), Autorisierungsberechtigungen, Benutzer, semantische Zugriffsebenen des BI-Tools und analytische Anwendungen.

Sobald Sie Ihr Data Warehouse zu Azure Synapse Analytics migriert haben, haben Sie die großartige Gelegenheit, andere Technologien im analytischen Ökosystem von Microsoft zu nutzen. So können Sie Ihr Data Warehouse nicht nur modernisieren, sondern auch Erkenntnisse aus anderen analytischen Datenspeichern in Azure zusammenführen.

Sie können die ETL-Verarbeitung so ausweiten, dass Daten eines beliebigen Typs in Azure Data Lake Storage erfasst werden. Mithilfe von Azure Data Factory können Sie sie nach Bedarf vorbereiten und integrieren. So werden vertrauenswürdige und allgemein verständliche Datenassets erzeugt, die von Ihrem Data Warehouse verarbeitet werden können, und auf die Data Scientists und andere Anwendungen zugreifen können. Sie können batchorientierte analytische Echtzeitpipelines erstellen. Sie können auch Machine Learning-Modelle erstellen, die so bereitgestellt werden können, dass sie im Batch, in Echtzeit und bei Bedarf ausgeführt werden.

Außerdem können Sie PolyBase verwenden, um auch Erkenntnisse über Lösungen außerhalb Ihres Data Warehouse zu gewinnen. So vereinfachen Sie den Zugriff auf Erkenntnisse, die über mehrere zugrunde liegenden Analyseplattformen in Azure gewonnen werden. Hierzu werden ganzheitliche integrierte Sichten in einem logischen Data Warehouse erstellt, sodass Sie problemlos auf Streaming, Big Data und herkömmliche Data Warehouse-Einblicke aus BI-Tools und -Anwendungen zugreifen können.

Viele Unternehmen führen bereits seit Jahren Data Warehouses in ihren Rechenzentren aus, damit Benutzer Business Intelligence-Lösungen realisieren können. Mit Data Warehouses werden Daten aus bekannten Transaktionssystemen extrahiert, und die Daten werden bereitgestellt, bereinigt, transformiert und integriert, um Data Warehouses zu füllen.

Anwendungsfälle, Geschäftsfälle und technologische Fortschritte unterstützen Azure Synapse Analytics dabei, Sie bei Ihrer Data Warehouse-Migration zu unterstützen. In den folgenden Abschnitten finden Sie viele dieser Beispiele.

## <a name="use-cases"></a>Anwendungsfälle

- Verbundene Produktinnovationen
- Factory of the Future
- Klinische Analyse
- Complianceanalyse
- Kostenbasierte Analyse
- Optimierung auf verschiedenen Kanälen
- Personalisierung
- Intelligente Lieferkette
- Dynamische Preise
- Beschaffungsanalyse
- Digitaler Kontrollturm
- Risikomanagement
- Kundenanalyse
- Betrugserkennung
- Anspruchsanalyse

## <a name="business-cases"></a>Geschäftsfälle

- Erstellen Sie umfassende Analyselösungen mit einem einzelnen Analysedienst.
- Verwenden Sie das Azure Synapse Analytics-Studio, das einen einheitlichen Arbeitsbereich für Datenvorbereitung, Datenverwaltung, Data Warehousing, Big Data und KI-Aufgaben bereitstellt.
- Erstellen und verwalten Sie die Pipeline mit einer codefreien visuellen Umgebung, automatisieren Sie die Abfrageoptimierung, erstellen Sie Proof of Concepts und verwenden Sie Power BI – alles über denselben Analysedienst.
- Sie können Data Warehouses und Big Data-Analysesysteme übergreifend Einblicke in alle Ihre Daten erhalten.
- Für unternehmenskritische Workloads können Sie die Leistung aller Abfragen mit intelligenter Workloadverwaltung, Workloadisolation und unbegrenzter Parallelität optimieren.
- Bearbeiten und erstellen Sie Power BI-Dashboards direkt in Azure Synapse Analytics.
- Verkürzen Sie die Projektentwicklungszeit für BI- und Machine-Learning-Projekte.
- Geben Sie mit der Integration von Azure Data Share in Azure Synapse Analytics Daten einfach mit wenigen Mausklicks frei.
- Implementieren Sie eine differenzierte Zugriffssteuerung mit Sicherheit auf Spaltenebene und nativer Sicherheit auf Zeilenebene.
- Schützen Sie vertrauliche Daten automatisch in Echtzeit mit dynamischer Datenmaskierung.
- Branchenführende Sicherheit mit integrierten Sicherheitsfeatures wie automatisierter Bedrohungserkennung und Always-On-Datenverschlüsselung.

## <a name="technology-advances"></a>Technologische Fortschritte

- Weder Hardwarekauf noch Wartungskosten, sodass Sie nur für das bezahlen, was Sie nutzen.
- Keine zu verwaltende Infrastruktur, sodass Sie sich auf den Wettbewerb konzentrieren können.
- Hochgradig parallele Verarbeitung von SQL-Abfragen mit dynamischer Skalierbarkeit, wenn Sie sie benötigen, die heruntergefahren oder angehalten wird, wenn sie nicht erforderlich ist.
- Möglichkeit der unabhängigen Skalierung von Speicher und Compute.
- Unnötige kostspielige Upgrades, weil die Stagingbereiche Ihres Data Warehouse zu groß werden, Speicherkapazität fressen und ein Upgrade erzwingen, werden vermieden. Sie können den Stagingbereich beispielsweise zu Azure Data Lake Storage verschieben. Dann können Sie zur Verarbeitung ein ETL-Tool wie Azure Data Factory oder Ihr vorhandenes ETL-Tool nutzen, das in Azure zu geringeren Kosten ausgeführt wird.
- Dies erzwingt kostspielige Hardwareupgrades, die durch die Verarbeitung in Azure mit Azure Data Lake Storage und Azure Data Factory vermieden werden können. Dies ist oftmals eine bessere Lösung als ETL-Workloads mit SQL-Abfrageverarbeitung, die in Ihrem vorhandenen Data Warehouse-DBMS ausgeführt werden. Wenn Stagingdatenvolumes ansteigen, werden von ETL-Prozessen mehr Speicher und Computeleistung für Ihr lokales Data Warehouse benötigt. Dies wiederum beeinflusst die Leistung von Abfrage-, Berichts- und Analyseworkloads.
- Vermeiden Sie das Erstellen teurer Data Marts, die Speicher- und Datenbanksoftwarelizenzen auf lokaler Hardware nutzen. Sie können sie stattdessen in Azure Synapse Analytics erstellen. Dies trifft vor allem dann zu, wenn Ihr Data Warehouse ein Data Vault-Entwurf ist, der häufig eine größere Nachfrage nach Data Marts verursacht.
- Vermeiden Sie die Kosten für die Analyse und das Speichern von Daten mit hoher Datengeschwindigkeit und hohem Datenvolumen auf lokaler Hardware. Wenn Sie beispielsweise von einem Computer generierte Echtzeitdaten wie Clickstreamdaten und IoT-Streamingdaten in Ihrem Data Warehouse analysieren müssen, können Sie Azure Synapse Analytics verwenden.
- Sie können Gebühren für das Speichern von Daten auf teurer Warehousehardware im Rechenzentrum vermeiden, wenn Ihr Data Warehouse größer wird. Mit Azure Synapse Analytics können Sie Ihre Daten zu geringeren Kosten im Cloudspeicher speichern.

## <a name="next-steps"></a>Nächste Schritte

<!-- TODO: More detail needed here. -->

[Demokratisierung von Daten](./data-democratization.md)
