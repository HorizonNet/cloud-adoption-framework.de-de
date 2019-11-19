---
title: 'Geschäftliche Ausrichtung: Cloudverwaltung und -vorgänge'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Geschäftsausrichtung: Cloudverwaltung und -betrieb'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: deeb663a344bb3eb4e8ecc9af307da5ec1348b7a
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565219"
---
# <a name="create-business-alignment-in-cloud-management"></a>Erstellen der Geschäftsausrichtung in der Cloudverwaltung

In lokalen Umgebungen werden IT-Ressourcen (Anwendungen, virtuelle Computer, VM-Hosts, Datenträger, Server, Geräte und Datenquellen) von der IT-Abteilung verwaltet, um Workloadvorgänge zu unterstützen. Aus IT-Sicht ist eine Workload eine Sammlung von IT-Ressourcen, die einen bestimmten Geschäftsvorgang unterstützen. Zur Unterstützung der Geschäftsvorgänge bietet die IT-Verwaltung Prozesse, die darauf ausgelegt sind, Störungen bei diesen Ressourcen zu minimieren. Beim Wechsel einer Organisation in die Cloud verschieben sich Verwaltung und Betrieb ein wenig und schaffen die Möglichkeit, eine engere Geschäftsausrichtung zu entwickeln.

## <a name="business-vernacular"></a>Geschäftsjargon

Der erste Schritt beim Erstellen der Geschäftsausrichtung ist das Sicherstellen der Begriffsausrichtung. Die IT-Verwaltung hat (wie die meisten Engineeringbereiche) eine Sammlung von Fachausdrücken oder hochtechnischen Begriffen zusammengestellt. Diese Begriffe können zu Verwirrung für Beteiligte im Unternehmen führen und die Zuordnung von Verwaltungsdiensten zum Geschäftswert erschweren.

Glücklicherweise schaffen die Prozesse zur Entwicklung einer Cloud Adoption-Strategie und eines Cloud Adoption-Plans eine optimale Gelegenheit, diese Begriffe neu zuzuordnen. Der Prozess bietet auch Gelegenheiten, die Verpflichtungen gegenüber der operativen Verwaltung in Partnerschaft mit dem Unternehmen zu überdenken. Die folgende Artikelreihe erläutert den neuen Ansatz für drei spezifische Begriffe, die helfen können, die Gespräche zwischen Beteiligten von Unternehmen zu verbessern: 

- **[Wichtigkeit](./criticality.md):** Zuordnung von Workloads zu Geschäftsprozessen. Rangfolge der Wichtigkeit zur Fokussierung von Investitionen.
- **[Auswirkung](./impact.md):** Verstehen der Auswirkungen potenzieller Ausfälle, um die Bewertung der Rendite für Cloudverwaltung zu erleichtern.
- **[Verpflichtung](./commitment.md):** Entwickeln echter Partnerschaften durch Erstellen und Dokumentieren von Vereinbarungen *mit dem Unternehmen*.

> [!NOTE]
> Diesen Begriffen liegen klassische IT-Begriffe wie SLA, RTO und RPO zugrunde. Die Zuordnung bestimmte Geschäfts- und IT-Begriffe wird im Artikel [Verpflichtung](./commitment.md) ausführlicher behandelt.

## <a name="ops-management-planning-workbook"></a>Arbeitsmappe zur Planung der Betriebsverwaltung

Um Entscheidungen, die sich aus diesem Gespräch über die Begriffsausrichtung ergeben, zu erfassen, ist eine [Arbeitsmappe zur Betriebsverwaltung](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) auf unserer GitHub-Website verfügbar. Diese Arbeitsmappe stellt keine SLA- oder Kostenberechnungen bereit. Sie dient nur zur Erfassung dieser Maßnahmen und zur Prognose der Rendite bei der Schadensvermeidung.

Alternativ können dieselben Workloads und zugehörigen Ressourcen direkt in Azure gekennzeichnet werden, wenn die Lösungen bereits in der Cloud bereitgestellt wurden.

## <a name="next-steps"></a>Nächste Schritte

Beginnen mit dem Erstellen der Geschäftsausrichtung durch Definieren der [Wichtigkeit der Workload](./criticality.md).

> [!div class="nextstepaction"]
> [Definieren der Wichtigkeit der Workload](./criticality.md)
