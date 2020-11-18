---
title: Grundlegendes zu Clouddatenfunktionen
description: Grundlegendes zu Clouddatenfunktionen, einschließlich der Quelle der Funktionalität, des Umfangs und der Ergebnisse.
author: v-hanki
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 07/14/2020
ms.openlocfilehash: 1ded8b088d866bcb8d00f14dbe6286266313f63e
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94712322"
---
# <a name="cloud-data-functions"></a>Clouddatenfunktionen

An einer Analysekonversation sind mehrere Zielgruppen beteiligt, einschließlich des typischen Verkäufers, des Datenbankarchitekten und des Infrastrukturteams. Außerdem umfassen Analyselösungen Influencer, Empfehlungsgeber und Entscheidungsträger der Rollen Unternehmensarchitektur, Data Science, Business Analytics und Geschäftsführung.

Azure Synapse Analytics ermöglicht es dem gesamten Unternehmen, vom IT-Mitarbeiter bis zum Business Analyst, an Analyselösungen zusammenzuarbeiten und die Clouddatenfunktionen zu verstehen. In den folgenden Abschnitten werden diese Rollen ausführlicher erörtert.

## <a name="database-administrators-and-architects"></a>Datenbankadministratoren und -architekten

Datenbankadministratoren und -architekten sind zuständig für Integration und Routing von Datenquellen in ein zentrales Repository. Diese Experten kümmern sich auch um die für das System erforderliche Verwaltung und Leistung sowie um die Barrierefreiheit und Effizienz der Abfrage- und Analysemodellierung für diese Daten.

Mithilfe von Azure Synapse Analytics können Datenbankadministratoren ihren zunehmenden Zuständigkeiten für Data Warehouses und Data Lakes gerecht werden. Sie können vertraute Sprachen und Tools (z. B. T-SQL) verwenden, um beliebig viele Workloads auszuführen. Sie können Ressourcen zuweisen, um kritische Workloads basierend auf intelligenter Workloadpriorität, Workloadisolation und erweiterten Parallelitätsfunktionen zu erweitern.

## <a name="infrastructure-teams"></a>Infrastrukturteams

Diese Teams beschäftigen sich mit der Bereitstellung und Architektur der zugrunde liegenden Computeressourcen, die für große Analysesysteme benötigt werden. In vielen Fällen verwalten sie die Übergänge zwischen rechenzentrumsbasierten und cloudbasierten Systemen sowie die aktuellen Anforderungen für die Interoperabilität zwischen beiden Systemen. Notfallwiederherstellung, Geschäftskontinuität und Hochverfügbarkeit sind häufige Probleme.

Mit Azure Synapse Analytics können IT-Experten die Daten ihrer Organisation effizienter schützen und verwalten. Sie können die Big Data-Verarbeitung sowohl mit On-Demand- als auch mit bereitgestelltem Computing ermöglichen. Durch die enge Integration mit Azure Active Directory hilft der Dienst, den Zugriff auf Clouddienste und Hybridkonfigurationen zu schützen. IT-Experten können Datenschutzanforderungen mithilfe der Datenmaskierung und der Sicherheit auf Zeilen- und Spaltenebene erzwingen.

## <a name="enterprise-architects-and-data-engineers"></a>Unternehmensarchitekten und Datentechniker

Diese Teams sind dafür verantwortlich, komplexe Lösungen mit Komponenten zusammenzustellen, die die Integration über eine breite Palette von Datentools und Lösungen umfassen. Dazu gehören:

- Strukturierte und unstrukturierte Daten
- Transformation
- Speichern und Abrufen
- Analysemodellierung
- Nachrichtenbasierte Middleware
- Data Marts
- Georedundanz und Datenkonsistenz
- Dashboarding und Berichterstellung

 Unternehmensarchitekten und Datentechniker sind im Allgemeinen damit beschäftigt, effektive Architekturen zu erstellen, die auf integrierte Weise arbeiten. Solche Architekturen bewahren Leistung, Verfügbarkeit, einfache Verwaltung, Flexibilität/Erweiterbarkeit und Durchführbarkeit.

Mithilfe von Azure Synapse Analytics können Datentechniker die Schritte vereinfachen, die zum Zusammenführen mehrerer Datentypen aus unterschiedlichen Quellen wie Streaming-, Transaktions- und Geschäftsdaten erforderlich sind. Sie können eine codefreie visuelle Umgebung nutzen, um eine Verbindung mit Datenquellen herzustellen und Daten im Data Lake zu erfassen, zu transformieren und zu platzieren.

## <a name="data-scientists"></a>Datenanalysten

Data Scientists unterliegt die Erstellung erweiterter Modelle für große Mengen kritischer, aber oftmals verschiedenartiger Daten. Ihre Arbeit umfasst die Übersetzung der Anforderungen des Unternehmens in die technologischen Anforderungen für die Normalisierung und Transformation von Daten. Sie erstellen statistische und andere Analysemodelle und stellen sicher, dass branchenspezifische Teams die Analysen erhalten, die sie für die Betriebsabläufe benötigen.

Mithilfe von Azure Synapse Analytics können Data Scientists innerhalb weniger Minuten einen Proof of Concept erstellen und End-to-End-Lösungen erstellen oder anpassen. Sie können Ressourcen nach Anforderung bereitstellen oder vorhandene Ressourcen bedarfsgesteuert über große Datenmengen abfragen. Sie können ihre Arbeit in einer Vielzahl von Sprachen durchführen, darunter T-SQL, R, Python, Scala, .NET und Spark SQL.

## <a name="business-analysts"></a>Business Analysts

Diese Teams erstellen und verwenden Dashboards, Berichte und andere Formen der Datenvisualisierung, um schnelle Erkenntnisse über den Betrieb zu gewinnen. Häufig verfügt jede branchenspezifische Abteilung über dedizierte Business Analysts, die Informationen und Analysen aus spezialisierten Anwendungen sammeln und verpacken. Diese spezialisierten Apps können für Kreditkarten, Einzelhandelsbanking, kommerzielles Banking, Finanzverwaltung, Marketing und andere Organisationen sein.

Mithilfe von Azure Synapse Analytics können Business Analysts sicher auf Datasets zugreifen und mithilfe von Power BI Dashboards erstellen. Sie können Daten auch innerhalb und außerhalb der eigenen Organisation über Azure Data Share sicher freigeben.

## <a name="executives"></a>Führungskräfte

Führungskräfte sind verantwortlich für das Festlegen der Strategie, und sie stellen sicher, dass strategische Initiativen sowohl in IT- als auch in branchenspezifischen Abteilungen effektiv umgesetzt werden. Die Lösungen müssen kostengünstig sein, Unterbrechungen für das Unternehmen verhindern, bei Wachstum oder geänderten Anforderungen eine einfache Erweiterbarkeit ermöglichen und Ergebnisse für das Unternehmen liefern.
