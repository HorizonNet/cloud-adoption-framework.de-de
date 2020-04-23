---
title: Auswirkungen von globalen Marktentscheidungen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich damit vertraut zu machen, wie sich globale Marktentscheidungen auf die Transformationsjourney in die Cloud auswirken können.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: b4c39b0a55485335e65bee9a5e6be2fe5fe22279
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997758"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-will-global-market-decisions-affect-the-transformation-journey"></a>Wie wirken sich globale Marktentscheidungen auf die Transformationsjourney aus?

Die Cloud eröffnet ganz neue Möglichkeiten – und zwar auf globaler Ebene. Es gibt sehr viel weniger Hürden für globale Vorgänge, sodass Unternehmen Ressourcen für einen Markt bereitstellen können, ohne große Investitionen in neue Rechenzentren vornehmen zu müssen. Leider führt dies auch zu erheblich mehr Komplexität aus technischer und rechtlicher Sicht.

## <a name="data-sovereignty"></a>Datenhoheit

In vielen geopolitischen Regionen gelten Bestimmungen zur Datenhoheit. Diese Vorschriften schränken ein, wo Daten gespeichert werden können, welche Daten das Ursprungsland verlassen dürfen und welche Daten über Bürger der betreffenden Region erfasst werden dürfen. Bevor Sie eine beliebige cloudbasierte Lösung in einem fremden Land einsetzen, sollten Sie verstehen, wie der jeweilige Cloudanbieter mit dem Thema Datenhoheit umgeht. Weitere Informationen zum Azure-Ansatz für die einzelnen Geografien finden Sie unter [Azure-Geografien](https://azure.microsoft.com/global-infrastructure/geographies). Weitere Informationen zur Compliance in Azure finden Sie unter [Datenschutz bei Microsoft](https://www.microsoft.com/trust-center/privacy) im Microsoft Trust Center.

Im weiteren Verlauf dieses Artikels wird davon ausgegangen, dass ein Engagement in einem fremden Land durch eine Rechtsberatung überprüft und genehmigt wurde.

## <a name="business-units"></a>Geschäftseinheiten

Es ist wichtig zu wissen, welche Geschäftseinheiten im Ausland eingesetzt werden und welche Länder betroffen sind. Diese Informationen werden zum Entwerfen von Lösungen für Hosting, Abrechnung und Bereitstellungen für den Cloudanbieter verwendet.

## <a name="employee-usage-patterns"></a>Verwendungsmuster der Mitarbeiter

Es ist wichtig zu verstehen, wie globale Benutzer auf Anwendungen zugreifen, die nicht im Land des jeweiligen Benutzers gehostet werden. Globale WANs (Wide Area Networks) leiten Benutzer basierend auf bestehenden Netzwerkvereinbarungen weiter. In einer herkömmlichen lokalen Umgebung gelten einige Einschränkungen für das WAN-Layout. Diese Einschränkungen können zu einer schlechten Benutzererfahrung führen, wenn sie vor der Cloudeinführung nicht richtig verstanden wurden.

In einem Cloudmodell eröffnet auch das kommerzielle Internet viele neue Optionen. Das Kommunizieren der Verteilung der Mitarbeiter auf die verschiedenen Geografien hilft dem Cloudeinführungsteam beim Entwerfen von WAN-Lösungen, die für eine hohe Benutzerfreundlichkeit sorgen **und** auch die Netzwerkkosten senken können.

## <a name="external-user-usage-patterns"></a>Verwendungsmuster externer Benutzer

Es ist genauso wichtig, die Verwendungsmuster externer Benutzer zu kennen, z. B. von Kunden oder Partnern. Wie die Verwendungsmuster eigener Mitarbeiter können auch die Verwendungsmuster externer Benutzer negative Auswirkungen auf die Leistung von Cloudbereitstellungen haben. Wenn sich sehr viele oder sehr wichtige Benutzer in einem fremden Land befinden, kann es ratsam sein, schon im allgemeinen Lösungsentwurf eine Strategie für die globale Bereitstellung zu planen.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über die [erforderlichen Qualifikationen in der Strategiephase](./suggested-skills.md) der Cloudeinführungsjourney.

> [!div class="nextstepaction"]
> [Für die Strategie relevante Qualifikationen](./suggested-skills.md)
