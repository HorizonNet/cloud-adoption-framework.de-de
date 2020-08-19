---
title: Was ist die Datenklassifizierung?
description: Die Datenklassifizierung ermöglicht es Ihnen, Ihre Organisationsdaten zu untersuchen und ihnen einen Wert zuzuweisen, und stellt einen gängigen Ausgangspunkt für die Governance dar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 719bd1ada85fb67b29ba0dc3f93b4dbf7a243a8c
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88573223"
---
# <a name="what-is-data-classification"></a>Was ist die Datenklassifizierung?

Die Datenklassifizierung ermöglicht es Ihnen, Ihre Organisationsdaten zu untersuchen und ihnen einen Wert zuzuweisen, und stellt einen gängigen Ausgangspunkt für die Governance dar. Beim Prozess der Datenklassifizierung werden Daten anhand von Vertraulichkeit und Auswirkungen auf den Geschäftsbetrieb kategorisiert, um Risiken zu ermitteln. Wenn die Daten klassifiziert sind, können Sie sie so verwalten, dass vertrauliche oder wichtige Daten vor Diebstahl oder Verlust geschützt werden.

## <a name="understand-data-risks-then-manage-them"></a>Verstehen der Datenrisiken, um sie zu verwalten

Bevor ein Risiko verwaltet werden kann, muss es verstanden werden. Im Fall der Haftung bei Datenpannen beginnt dieses Verstehen mit der Datenklassifizierung. Datenklassifizierung ist der Vorgang, bei dem jedem Objekt in einer digitalen Ressource ein Metadatenmerkmal zugeordnet wird, das den Datentyp dieses Objekts angibt.

Jede Ressource, die als möglicher Kandidat für die Migration zur Cloud oder Bereitstellung in dieser erkannt wurde, sollte über dokumentierte Metadaten zum Aufzeichnen der Datenklassifizierung, der geschäftlichen Bedeutung und der Verantwortung für Abrechnung verfügen. Diese drei Aspekte der Klassifizierung können zum Verstehen und Mindern von Risiken beitragen.

## <a name="classifications-microsoft-uses"></a>Von Microsoft verwendete Klassifizierungen

In der nachstehenden Liste sind die von Microsoft verwendeten Klassifizierungen aufgeführt. Abhängig von Ihrer Branche und bestehenden Sicherheitsanforderungen gibt es in Ihrer Organisation möglicherweise bereits Standards für Datenklassifizierungen. Wenn kein Standard vorhanden ist, können Sie diese Beispielklassifizierung verwenden, um Ihre digitalen Ressourcen und Ihr Risikoprofil besser zu verstehen.

- **Nicht geschäftlich:** Daten aus Ihrem Privatleben, die nicht zu Microsoft gehören
- **Öffentlich:** Geschäftsdaten, die frei verfügbar sind und für den öffentlichen Gebrauch genehmigt werden
- **Allgemein:** Geschäftsdaten, die nicht für eine öffentliche Zielgruppe bestimmt sind
- **Vertraulich:** Geschäftsdaten, die Microsoft Schaden zufügen könnten, wenn sie zu häufig weitergegeben werden
- **Streng vertraulich:** Geschäftsdaten, die Microsoft großen Schaden zufügen könnten, wenn sie übermäßig freigegeben werden

## <a name="tagging-data-classification-in-azure"></a>Kennzeichnen der Datenklassifizierung in Azure

Ressourcentags sind eine gute Methode zum Speichern von Metadaten. Sie können diese Tags zum Anwenden von Datenklassifizierungen auf bereitgestellte Ressourcen verwenden. Auch wenn das Kennzeichnen von Cloudressourcen keinen Ersatz für eine formale Datenklassifizierung darstellt, ist es ein wertvolles Hilfsmittel für das Verwalten von Ressourcen und das Anwenden von Richtlinien. [Azure Information Protection](/azure/information-protection/what-is-information-protection) ist eine hervorragende Lösung, die Sie bei der Klassifizierung von Daten unterstützt – ganz gleich, ob sich diese in der lokalen Umgebung, in Azure oder an einem anderen Ort befinden. Diese Lösung sollte als Teil einer allgemeinen Klassifizierungsstrategie betrachtet werden.

## <a name="take-action"></a>Ausführen einer Aktion

Versehen Sie Ressourcen mit einer definierten Datenklassifizierung.

- Sehen Sie sich in [einem der umsetzbaren Governanceleitfäden](../guides/index.md) Beispiele für das Anwenden von Tags innerhalb Ihres Portfolios an.
- Lesen Sie den Artikel [Empfohlene Namens- und Kennzeichnungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md#metadata-tags), um einen umfassenderen Kennzeichnungsstandard zu definieren.
- Weitere Informationen zu Tags für Ressourcen in Azure finden Sie unter [Verwenden von Tags zum Organisieren von Azure-Ressourcen und Verwaltungshierarchie](/azure/azure-resource-manager/management/tag-resources).

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie auch den Artikel zum Schützen sensibler Daten aus dieser Artikelreihe. Der nächste Artikel enthält Informationen zum Umgang mit als vertraulich oder streng vertraulich klassifizierten Daten:

> [!div class="nextstepaction"]
> [Schützen von Datenlösungen](/azure/architecture/data-guide/scenarios/securing-data-solutions?bc=%2fazure%2fcloud-adoption-framework%2f_bread%2ftoc.json&toc=%2fazure%2fcloud-adoption-framework%2ftoc.json)
