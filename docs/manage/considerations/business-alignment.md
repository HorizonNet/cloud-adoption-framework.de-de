---
title: 'Geschäftsausrichtung: Cloudverwaltung und -betrieb'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Geschäftsausrichtung: Cloudverwaltung und -betrieb'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9c6884d57b9238f58921b14ec3ddbbe3623506af
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558588"
---
# <a name="create-business-alignment-in-cloud-management"></a>Erstellen der Geschäftsausrichtung in der Cloudverwaltung

In lokalen Umgebungen werden IT-Ressourcen (Anwendungen, virtuelle Computer, VM-Hosts, Datenträger, Server, Geräte und Datenquellen) von der IT-Abteilung verwaltet, um Workloadvorgänge zu unterstützen. Aus IT-Sicht ist eine Workload eine Sammlung von IT-Ressourcen, die einen bestimmten Geschäftsvorgang unterstützen. In lokalen Umgebungen stellt die IT-Verwaltung einen Prozessentwurf zur Verfügung, um Störungen dieser IT-Ressourcen zu minimieren und so Unterbrechungen des Supportgeschäftsbetriebs so gering wie möglich zu halten. Beim Wechsel in die Cloud verschieben sich Verwaltung und Betrieb ein wenig und schaffen die Möglichkeit, eine engere Geschäftsausrichtung zu entwickeln.

## <a name="business-vernacular"></a>Geschäftsjargon

Der erste Schritt beim Erstellen der Geschäftsausrichtung ist die Begriffsausrichtung. Die IT-Verwaltung verwendet (wie die meisten Engineeringbereiche) einen umfangreichen Fachjargon oder hochtechnische Begriffe. Diese Begriffe können zu Verwirrung für Beteiligte im Unternehmen führen und die Zuordnung von Verwaltungsdiensten zum Geschäftswert erschweren.

Glücklicherweise schaffen die Prozesse zur Entwicklung einer Cloud Adoption-Strategie und eines Cloud Adoption-Plans eine kreative Situation für die Neuzuordnung von Begriffen. Dabei bietet sich auch eine großartige Gelegenheit, die Verpflichtungen gegenüber der operativen Verwaltung in Partnerschaft mit dem Unternehmen zu überdenken. Die folgende Artikelreihe erläutert den neuen Ansatz für drei spezifische Begriffe, die die Gespräche mit Beteiligten von Unternehmen verbessern können:

- **[Wichtigkeit](./criticality.md)** : Zuordnung von Workloads zu Geschäftsprozessen. Rangfolge der Wichtigkeit zur Fokussierung von Investitionen.
- **[Auswirkung](./impact.md)** : Verstehen der Auswirkungen potenzieller Ausfälle, um die Bewertung der Rendite für Cloudverwaltung zu erleichtern.
- **[Verpflichtung](./commitment.md)** : Entwickeln echter Partnerschaften durch Erstellen und Dokumentieren von Vereinbarungen **mit dem Unternehmen**.

> [!NOTE]
> Unter jedem dieser Begriffe verbergen sich klassische IT-Konzepte wie SLA, RTO und RPO. Die Zuordnung von Geschäfts- und IT-Begriffen wird im Artikel zur Verpflichtung ausführlicher behandelt.

## <a name="ops-management-planning-workbook"></a>Arbeitsmappe zur Planung der Betriebsverwaltung

Um Entscheidungen als Ergebnis dieser Kommunikation zu erfassen, ist eine [Arbeitsmappe zur Betriebsverwaltung](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) in unserem GitHub-Repository verfügbar. Diese Arbeitsmappe stellt keine SLA- oder Kostenberechnungen bereit. Sie dient nur als Leitfaden zur Erfassung dieser Maßnahmen und zur Prognose der Rendite bei der Schadensvermeidung.

Alternativ können dieselben Workloads und zugehörigen Ressourcen direkt in Azure gekennzeichnet werden, wenn die Lösungen bereits in der Cloud bereitgestellt wurden.

## <a name="next-steps"></a>Nächste Schritte

Beginnen mit dem Erstellen der Geschäftsausrichtung durch Definieren der [Wichtigkeit der Workload](./criticality.md).

> [!div class="nextstepaction"]
> [Definieren der Wichtigkeit der Workload](./criticality.md)
