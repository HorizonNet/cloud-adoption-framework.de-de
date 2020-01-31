---
title: Grundlegendes zu den Auswirkungen globaler Marktentscheidungen
description: Erläuterung des Konzepts globaler Märkte
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: af3c9d8b155d2c6a5e861e64b6472effbafcbb6d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76798161"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-will-global-market-decisions-affect-the-transformation-journey"></a>Wie wirken sich globale Marktentscheidungen auf die Transformationsjourney aus?

Die Cloud eröffnet ganz neue Möglichkeiten – und zwar auf globaler Ebene. Es gibt sehr viel weniger Hürden für globale Vorgänge, sodass Unternehmen Ressourcen für einen Markt bereitstellen können, ohne große Investitionen in neue Rechenzentren vornehmen zu müssen. Leider führt dies auch zu erheblich mehr Komplexität aus technischer und rechtlicher Sicht.

## <a name="data-sovereignty"></a>Datenhoheit

In vielen geopolitischen Regionen gelten Bestimmungen zur Datenhoheit. Diese Vorschriften schränken ein, wo Daten gespeichert werden können, welche Daten das Ursprungsland verlassen dürfen und welche Daten über Bürger der betreffenden Region erfasst werden dürfen. Bevor Sie eine beliebige cloudbasierte Lösung in einem fremden Land einsetzen, sollten Sie verstehen, wie der jeweilige Cloudanbieter mit dem Thema Datenhoheit umgeht. Weitere Informationen zum Azure-Ansatz für die einzelnen Geografien finden Sie [hier](https://azure.microsoft.com/global-infrastructure/geographies). Weitere Informationen zur Compliance in Azure finden Sie unter [Datenschutz bei Microsoft](https://www.microsoft.com/trustcenter/privacy) im Microsoft Trust Center.

Im weiteren Verlauf dieses Artikels wird davon ausgegangen, dass ein Engagement in einem fremden Land durch eine Rechtsberatung überprüft und genehmigt wurde.

## <a name="business-units"></a>Geschäftseinheiten

Es ist wichtig zu wissen, welche Geschäftseinheiten im Ausland eingesetzt werden und welche Länder betroffen sind. Diese Informationen werden zum Entwerfen von Lösungen für Hosting, Abrechnung und Bereitstellungen für den Cloudanbieter verwendet.

## <a name="employee-usage-patterns"></a>Verwendungsmuster der Mitarbeiter

Es ist wichtig zu verstehen, wie globale Benutzer auf Anwendungen zugreifen, die nicht im Land des jeweiligen Benutzers gehostet werden. Globale WANs (Wide Area Networks) leiten Benutzer basierend auf bestehenden Netzwerkvereinbarungen weiter. In einer herkömmlichen lokalen Umgebung gelten einige Einschränkungen für das WAN-Layout. Diese Einschränkungen können zu einer schlechten Benutzererfahrung führen, wenn sie vor der Cloudeinführung nicht richtig verstanden wurden.

In einem Cloudmodell eröffnet auch das kommerzielle Internet viele neue Optionen. Das Kommunizieren der Verteilung der Mitarbeiter auf die verschiedenen Geografien hilft dem Cloudeinführungsteam beim Entwerfen von WAN-Lösungen, die für eine hohe Benutzerfreundlichkeit sorgen **und** auch die Netzwerkkosten senken können.

## <a name="external-user-usage-patterns"></a>Verwendungsmuster externer Benutzer

Es ist genauso wichtig, die Verwendungsmuster externer Benutzer zu kennen, z. B. von Kunden oder Partnern. Wie die Verwendungsmuster eigener Mitarbeiter können auch die Verwendungsmuster externer Benutzer negative Auswirkungen auf die Leistung von Cloudbereitstellungen haben. Wenn sich sehr viele oder sehr wichtige Benutzer in einem fremden Land befinden, kann es ratsam sein, schon im allgemeinen Lösungsentwurf eine Strategie für die globale Bereitstellung zu planen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Entscheidungen für den globalen Markt getroffen und kommuniziert wurden, kann das Team damit beginnen, anhand dieser Metriken [technische Standards festzulegen](../digital-estate/index.md).
Das Ergebnis ist ein [Transformationsbacklog oder Migrationsbacklog](..//migrate/migration-considerations/prerequisites/technical-complexity.md).

> [!div class="nextstepaction"]
> [Bewerten der digitalen Ressourcen](../digital-estate/index.md)
