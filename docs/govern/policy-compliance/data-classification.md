---
title: Was ist die Datenklassifizierung?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Was ist die Datenklassifizierung?
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 86c57efed1be2760aca607197eb8d28f0151097a
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223571"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Was ist die Datenklassifizierung?

Anhand von Datenklassifizierungen können Sie den Wert Ihrer Organisationsdaten ermitteln und zuweisen. Außerdem stellen sie den Startpunkt für die Governance dar. Beim Prozess der Datenklassifizierung werden Daten anhand von Vertraulichkeit und Auswirkungen auf den Geschäftsbetrieb kategorisiert, um Risiken zu ermitteln. Nachdem die Daten klassifiziert wurden, können sie so verwaltet werden, dass vertrauliche oder wichtige Daten vor Diebstahl oder Verlust geschützt werden.

## <a name="understand-data-risks-then-manage-them"></a>Verstehen der Datenrisiken, um sie zu verwalten

Bevor ein Risiko verwaltet werden kann, muss es verstanden werden. Im Fall der Haftung bei Datenpannen beginnt dieses Verstehen mit der Datenklassifizierung. Datenklassifizierung ist der Prozess, in dem jedem Objekt in einer digitalen Ressource ein Metadatenmerkmal zugeordnet wird, das den mit diesem Objekt verknüpften Datentyp identifiziert.

Microsoft empfiehlt, dass es zu einem Objekt, das als möglicher Kandidat für Migration in oder Bereitstellung für die Cloud identifiziert wurde, dokumentierte Metadaten zum Aufzeichnen der Datenklassifizierung, geschäftlichen Bedeutung und Verantwortung für Abrechnung geben sollte. Diese drei Aspekte der Klassifizierung können zum Verstehen und Mindern von Risiken beitragen.

## <a name="microsofts-data-classification"></a>Datenklassifizierung bei Microsoft

In der nachstehenden Liste sind die von Microsoft verwendeten Klassifizierungen aufgeführt. Je nach Ihrer Branche oder vorhandenen Sicherheitsanforderungen gibt es in Ihrer Organisation vielleicht bereits Standards für Datenklassifizierungen. Wenn es keinen Standard gibt, können Sie gerne diese Beispielklassifizierung verwenden, um Ihre digitalen Ressourcen und Ihr Risikoprofil besser zu verstehen.

- **Nicht geschäftlich:** Daten aus Ihrem Privatleben, die nicht zu Microsoft gehören
- **Öffentlich:** Geschäftsdaten, die frei verfügbar sind und für den öffentlichen Gebrauch genehmigt werden
- **Allgemein:** Geschäftsdaten, die nicht für eine öffentliche Zielgruppe bestimmt sind
- **Vertraulich:** Geschäftsdaten, die Microsoft Schaden zufügen könnten, wenn sie übermäßig freigegeben werden
- **Streng vertraulich:** Geschäftsdaten, die Microsoft großen Schaden zufügen könnten, wenn sie übermäßig freigegeben werden

## <a name="tagging-data-classification-in-azure"></a>Kennzeichnen der Datenklassifizierung in Azure

Für die Speicherung von Metadaten wird die Verwendung von Ressourcentags empfohlen. Mithilfe dieser Tags können Datenklassifizierungen auf bereitgestellte Ressourcen angewendet werden. Auch wenn das Kennzeichnen von Cloudressourcen keinen Ersatz für eine formale Datenklassifizierung darstellt, ist es ein wertvolles Hilfsmittel für das Verwalten von Ressourcen und das Anwenden von Richtlinien. [Azure Information Protection](https://docs.microsoft.com/azure/information-protection/what-is-information-protection) ist eine hervorragende Lösung, die Sie bei der Klassifizierung von _Daten_ unterstützt – ganz gleich, ob sich diese in der lokalen Umgebung, in Azure oder an einem anderen Ort befinden. Diese Lösung sollte als Teil einer allgemeinen Klassifizierungsstrategie in Betracht gezogen werden.

Zusätzliche Informationen zu Tags für Ressourcen in Azure finden Sie im Artikel zu [Verwenden von Tags zum Organisieren Ihrer Azure-Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="next-steps"></a>Nächste Schritte

Wenden Sie Datenklassifizierungen im Rahmen eines der handlungsrelevanten Governanceleitfäden an.

> [!div class="nextstepaction"]
> [Auswählen eines umsetzbaren Governanceleitfadens](../guides/index.md)
