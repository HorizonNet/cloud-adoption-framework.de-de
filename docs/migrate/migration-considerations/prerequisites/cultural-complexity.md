---
title: 'Vorbereiten auf kulturelle Komplexität: Abstimmen von Rollen und Zuständigkeiten'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Vorbereiten auf kulturelle Komplexität durch Abstimmen von Rollen und Zuständigkeiten
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: bc880e3bb27492b18a8e577911527978c7a4e0d2
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548335"
---
# <a name="prepare-for-cultural-complexity-aligning-roles-and-responsibilities"></a>Vorbereiten auf kulturelle Komplexität: Abstimmen von Rollen und Zuständigkeiten

Grundkenntnisse der Kultur, die für den Betrieb der vorhandenen Rechenzentren erforderlich ist, sind für den Erfolg jeder Migration von großer Bedeutung. In einigen Organisationen ist die Verwaltung von Rechenzentren Aufgabe zentraler IT-Betriebsteams. In diesen zentralen Teams sind die Rollen und Zuständigkeiten innerhalb des Teams klar definiert und bekannt. Bei größeren Unternehmen, insbesondere solchen, die an Complianceanforderungen Dritter gebunden sind, ist die Kultur tendenziell facettenreicher und komplexer. Kulturelle Komplexität kann zu Hindernissen führen, die schwer zu verstehen und nur mit großem Zeitaufwand zu überwinden sind.

In jedem Szenario ist es ratsam, in die Dokumentation von Rollen und Zuständigkeiten zu investieren, die für den Abschluss einer Migration erforderlich sind. Dieser Artikel beschreibt einige der Rollen und Zuständigkeiten, die bei einer Rechenzentrumsmigration zu beachten sind, und dient als Vorlage für die Dokumentation, die für Klarheit während der gesamten Ausführung sorgen kann.

## <a name="business-functions"></a>Geschäftsfunktionen

Bei jeder Migration gibt es einige Schlüsselfunktionen, die am besten vom Unternehmen ausgeführt werden, wann immer dies möglich ist. Häufig ist die IT-Abteilung in der Lage, die folgenden Aufgaben auszuführen. Die Einbeziehung von Mitgliedern des Unternehmens kann jedoch dazu beitragen, Barrieren im späteren Verlauf des Einführungsprozesses zu reduzieren. Darüber hinaus wird so der Beitrag der wichtigsten Beteiligten während des gesamten Migrationsprozesses sichergestellt.

| Prozess | Aktivität | BESCHREIBUNG |
|---------|---------|---------|
| Bewerten | Geschäftsziele | Definieren der gewünschten Geschäftsergebnisse der Migration |
| Bewerten | Prioritäten | Sicherstellen der Ausrichtung auf sich ändernde geschäftliche Prioritäten und Marktbedingungen |
| Bewerten | Begründung | Überprüfen der Annahmen, auf denen geschäftliche Änderungen basieren |
| Bewerten | Risiko | Unterstützen des Cloudeinführungsteams beim Verstehen der Auswirkungen konkreter Geschäftsrisiken |
| Bewerten | Genehmigen | Überprüfen und Genehmigen der geschäftlichen Auswirkungen von Änderungen an der vorgeschlagenen Architektur |
| Optimierung | Änderungsplan | Definieren eines Plans für die Nutzung der Änderung innerhalb des Unternehmens, einschließlich Zeiträumen mit geringen Aktivitäten und Änderungssperren |
| Optimierung | Testen | Abstimmen von Powerusern, die in der Lage sind, Leistung und Funktionalität zu überprüfen |
| Sichern und Verwalten | Auswirkungen der Unterbrechung | Unterstützen des Cloudeinführungsteams beim Quantifizieren der Auswirkungen einer Geschäftsprozessunterbrechung |
| Sichern und Verwalten | Überprüfen der Vereinbarung zum Servicelevel (SLA) | Unterstützen des Cloudeinführungsteams beim Definieren von Vereinbarungen zum Servicelevel und akzeptablen Toleranzen für Unterbrechungen des Geschäftsbetriebs |

Letztlich ist das Cloudeinführungsteam für jede dieser Aktivitäten verantwortlich. Die Festlegung von Zuständigkeiten und regelmäßiger Intervalle mit dem Unternehmen für die Durchführung dieser Aktivitäten in einem festgelegten Rhythmus kann jedoch die Abstimmung der Beteiligten und die Zusammenarbeit mit dem Unternehmen verbessern.

## <a name="common-roles-and-responsibilities"></a>Allgemeine Rollen und Zuständigkeiten

Jeder Prozess im Rahmen der Besprechung der Migrationsprinzipien des Framework für die Cloudeinführung beinhaltet einen Prozessartikel, in dem spezifische Aktivitäten zur Abstimmung von Rollen und Zuständigkeiten beschrieben sind. Aus Gründen der Eindeutigkeit während der Ausführung sollten jeder Aktivität eine einzige verantwortliche Partei sowie alle verantwortlichen Parteien, die zur Unterstützung dieser Aktivitäten erforderlich sind, zugewiesen werden. Die folgende Liste enthält eine Reihe allgemeiner Rollen und Zuständigkeiten, die eine stärkere Auswirkung auf die Durchführung der Migration haben. Diese Rollen sollten in einer frühen Phase der Migration festgelegt werden.

> [!NOTE]
> In der folgenden Tabelle sollte eine verantwortliche Partei mit der Abstimmung von Rollen beginnen. Diese Spalte sollte an die bestehenden Prozesse angepasst werden, um eine effiziente Ausführung zu gewährleisten. Im Idealfall sollte eine einzelne Person als verantwortliche Partei benannt werden.

| Prozess | Aktivität | BESCHREIBUNG | Verantwortliche Partei |
|---------|---------|---------|---------|
| Voraussetzung | Digitale Ressourcen | Anpassen des vorhandenen Bestands an die grundlegenden Annahmen basierend auf den Geschäftsergebnissen | Cloudstrategieteam |
| Voraussetzung | Migrationsbacklog | Priorisieren der Reihenfolge zu migrierender Workloads | Cloudstrategieteam |
| Bewerten | Architecture | Hinterfragen der anfänglichen Annahmen, um die Zielarchitektur auf der Grundlage von Nutzungsmetriken zu definieren | Cloudeinführungsteam |
| Bewerten | Genehmigung | Genehmigen der vorgeschlagenen Architektur | Cloudstrategieteam |
| Migrieren | Replikationszugriff | Zugriff auf vorhandene lokale Hosts und Ressourcen zum Einrichten der Replikationsprozesse | Cloudeinführungsteam |
| Optimierung | Bereit | Überprüfen, ob das System vor dem Höherstufen die Leistungs- und Kostenanforderungen erfüllt | Cloudeinführungsteam |
| Optimierung | Höherstufen | Berechtigungen zum Höherstufen einer Workload in die Produktion und Umleiten des Produktionsdatenverkehrs | Cloudeinführungsteam |
| Sichern und Verwalten | Betriebsübergang | Dokumentieren der Produktionssysteme vor dem Produktionsbetrieb | Cloudeinführungsteam |

> [!CAUTION]
> Bei diesen Aktivitäten haben Berechtigungen und Autorisierung starken Einfluss auf die verantwortliche Partei, die direkten Zugriff auf Produktionssysteme in der bestehenden Umgebung haben muss oder über Möglichkeiten verfügen muss, den Zugriff über andere verantwortliche Akteure zu sichern. Das Festlegen dieser verantwortlichen Partei hat direkten Einfluss auf die Höherstufungsstrategie während der Migrations- und Optimierungsprozesse.

## <a name="next-steps"></a>Nächste Schritte

Wenn das Team einen allgemeinen Überblick über die Rollen und Zuständigkeiten hat, ist es an der Zeit, mit der Vorbereitung der technischen Details der Migration zu beginnen. Grundlegende Kenntnisse in den Bereichen [technische Komplexität und Change Management](./technical-complexity.md) können dazu beitragen, das Cloudeinführungsteam auf die technische Komplexität der Migration vorzubereiten, indem eine Anpassung an einen inkrementellen Change Management-Prozess erfolgt.

> [!div class="nextstepaction"]
> [Technische Komplexität und Change Management](./technical-complexity.md)
