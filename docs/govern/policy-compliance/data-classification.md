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
ms.openlocfilehash: ffa318f44a6fe3a856598581ca7cc2de37fbd6f5
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997359"
---
<!-- markdownlint-disable MD026 -->

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

Ressourcentags sind eine gute Methode zum Speichern von Metadaten. Sie können diese Tags zum Anwenden von Datenklassifizierungen auf bereitgestellte Ressourcen verwenden. Auch wenn das Kennzeichnen von Cloudressourcen keinen Ersatz für eine formale Datenklassifizierung darstellt, ist es ein wertvolles Hilfsmittel für das Verwalten von Ressourcen und das Anwenden von Richtlinien. [Azure Information Protection](https://docs.microsoft.com/azure/information-protection/what-is-information-protection) ist eine hervorragende Lösung, die Sie bei der Klassifizierung von _Daten_ unterstützt – ganz gleich, ob sich diese in der lokalen Umgebung, in Azure oder an einem anderen Ort befinden. Diese Lösung sollte als Teil einer allgemeinen Klassifizierungsstrategie betrachtet werden.

Weitere Informationen zu Tags für Ressourcen in Azure finden Sie unter [Verwenden von Tags zum Organisieren von Azure-Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).

## <a name="next-steps"></a>Nächste Schritte

Wenden Sie Datenklassifizierungen im Rahmen eines der handlungsrelevanten Governanceleitfäden an.

> [!div class="nextstepaction"]
> [Auswählen eines umsetzbaren Governanceleitfadens](../guides/index.md)
