---
title: Geschäftsausrichtung in der Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Ihre Cloudvorgänge besser verwalten und eine engere Geschäftsausrichtung entwickeln können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 1c1a2bbdb6665246563f9514b55784f48114dee9
ms.sourcegitcommit: 2794cab8eb925103ae22babc704d89f7f7d4f6f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992843"
---
# <a name="create-business-alignment-in-cloud-management"></a>Erstellen der Geschäftsausrichtung in der Cloudverwaltung

In lokalen Umgebungen werden IT-Ressourcen (Anwendungen, virtuelle Computer, VM-Hosts, Datenträger, Server, Geräte und Datenquellen) von der IT-Abteilung verwaltet, um Workloadvorgänge zu unterstützen. Aus IT-Sicht ist eine Workload eine Sammlung von IT-Ressourcen, die einen bestimmten Geschäftsvorgang unterstützen. Zur Unterstützung der Geschäftsvorgänge bietet die IT-Verwaltung Prozesse, die darauf ausgelegt sind, Störungen bei diesen Ressourcen zu minimieren. Beim Wechsel einer Organisation in die Cloud verschieben sich Verwaltung und Betrieb ein wenig und schaffen die Möglichkeit, eine engere Geschäftsausrichtung zu entwickeln.

## <a name="business-vernacular"></a>Geschäftsjargon

Der erste Schritt beim Erstellen der Geschäftsausrichtung ist das Sicherstellen der Begriffsausrichtung. Die IT-Verwaltung hat (wie die meisten Engineeringbereiche) eine Sammlung von Fachausdrücken oder hochtechnischen Begriffen zusammengestellt. Diese Begriffe können zu Verwirrung für Beteiligte im Unternehmen führen und die Zuordnung von Verwaltungsdiensten zum Geschäftswert erschweren.

Glücklicherweise schaffen die Prozesse zur Entwicklung einer Cloud Adoption-Strategie und eines Cloud Adoption-Plans eine optimale Gelegenheit, diese Begriffe neu zuzuordnen. Der Prozess bietet auch Gelegenheiten, die Verpflichtungen gegenüber der operativen Verwaltung in Partnerschaft mit dem Unternehmen zu überdenken. Die folgende Artikelreihe erläutert den neuen Ansatz für drei spezifische Begriffe, die helfen können, die Gespräche zwischen Beteiligten von Unternehmen zu verbessern:

- **[Wichtigkeit](./criticality.md):** Zuordnung von Workloads zu Geschäftsprozessen. Rangfolge der Wichtigkeit zur Fokussierung von Investitionen.
- **[Auswirkung](./impact.md):** Verstehen der Auswirkungen potenzieller Ausfälle, um die Bewertung der Rendite für Cloudverwaltung zu erleichtern.
- **[Verpflichtung](./commitment.md):** Entwickeln echter Partnerschaften durch Erstellen und Dokumentieren von Vereinbarungen mit den Fachbereichen.

> [!NOTE]
> Diesen Begriffen liegen klassische IT-Begriffe wie SLA, RTO und RPO zugrunde. Die Zuordnung bestimmte Geschäfts- und IT-Begriffe wird im Artikel [Verpflichtung](./commitment.md) ausführlicher behandelt.

## <a name="operations-management-workbook"></a>Arbeitsmappe zum Operations Management

Um Entscheidungen, die sich aus diesem Gespräch über die Begriffsausrichtung ergeben, zu erfassen, ist eine [Arbeitsmappe zum Operations Management](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) auf unserer GitHub-Website verfügbar. Diese Arbeitsmappe stellt keine SLA- oder Kostenberechnungen bereit. Sie dient nur zur Erfassung dieser Maßnahmen und zur Prognose der Rendite bei der Schadensvermeidung.

Alternativ können dieselben Workloads und zugehörigen Ressourcen direkt in Azure gekennzeichnet werden, wenn die Lösungen bereits in der Cloud bereitgestellt wurden.

## <a name="next-steps"></a>Nächste Schritte

Beginnen mit dem Erstellen der Geschäftsausrichtung durch Definieren der [Wichtigkeit der Workload](./criticality.md).

> [!div class="nextstepaction"]
> [Definieren der Wichtigkeit der Workload](./criticality.md)
