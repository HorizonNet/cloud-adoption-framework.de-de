---
title: Messen von Geschäftsergebnissen mit AppDynamics
description: Verwenden von AppDynamics, um zu verstehen, wie sich die Leistung und Benutzererfahrung einer Anwendung auf Geschäftsergebnisse auswirken.
author: BrianBlanchard
ms.author: wayneme
ms.date: 09/18/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: think-tank
ms.openlocfilehash: 502dba2d970f46d8e929755a9c05be270724f501
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447097"
---
<!-- docutune:casing "Movie Tickets Online" -->

# <a name="measure-business-outcomes-with-appdynamics"></a>Messen von Geschäftsergebnissen mit AppDynamics

Die Messung und Quantifizierung erfolgreicher Geschäftsergebnisse ist ein wesentlicher Bestandteil jeder Cloudeinführungsstrategie. Das Verstehen der Leistung und Benutzererfahrung einer Anwendung ist von wesentlicher Bedeutung für die Messung solcher Geschäftsergebnisse. Die genaue Messung der Korrelation zwischen Anwendungsleistung, Benutzererfahrung und geschäftlichen Auswirkungen ist jedoch häufig schwierig, ungenau und zeitaufwändig.

AppDynamics kann für die meisten Anwendungsfälle geschäftliche Erkenntnisse liefern, und viele Organisationen beginnen eine umfassende Cloudeinführungsstrategie mit den folgenden Anwendungsfällen:

- Ein Vergleich zwischen vor und nach der Migration
- Geschäftlicher Zustand
- Releasevalidierung
- Segmentzustand
- User Journeys
- Business Journeys
- Abschlusstrichter

Dieser Leitfaden konzentriert sich darauf, wie Sie die Geschäftsergebnisse eines Vergleichs von vor und nach der Migration messen und wie Sie eine Migration während Ihrer Cloudeinführungs-Journey beschleunigen und deren Risiko reduzieren können.

## <a name="how-appdynamics-works"></a>Funktionsweise von AppDynamics

Vor der Migration wird zusammen mit Ihren Anwendungen ein kleiner, schlanker Agent bereitgestellt. Agents werden zweckgebunden speziell für verschiedene Sprachen wie .NET, Java und Node.js konzipiert. Der Agent sammelt während der Migration Leistungs- und Diagnosedaten und sendet diese an einen Controller, um die Informationen zu korrelieren und zu analysieren. Controller können sich in einer vollständig verwalteten AppDynamics-Umgebung befinden, oder der Kunde kann sie in Azure verwalten. Schlüsselbenutzererfahrungen werden als „Geschäftstransaktionen“ identifiziert, die Ihnen dabei helfen, die Baseline für die normale Anwendungs- oder Geschäftsleistung zu ermitteln. Unabhängig davon, ob es sich um herkömmliche Serverinfrastrukturen, Datenbanken, Middlewarekomponenten, lokal oder in der Cloud handelt, werden alle Anwendungskomponenten und Abhängigkeiten in Echtzeit für die gesamte Anwendung und jede Geschäftstransaktion identifiziert.

![Eine AppDynamics-Flowzuordnung](./media/app-dynamics-flow-map.jpg)

_Abbildung 1: Eine AppDynamics-Flowzuordnung._

## <a name="appdynamics-identifies-business-metrics"></a>AppDynamics identifiziert Geschäftsmetriken

Mit AppDynamics können Sie den Geschäftswert Ihrer Anwendungen definieren, die Schlüsselmetriken ermitteln, die sie erfüllen sollten, um ihren Wert zu behalten, und überprüfen, ob sie ihre Geschäftsergebnisziele erreichen. AppDynamics-Agents sammeln diese Datenpunkte sowie herkömmliche Anwendungsleistungsmetriken wie Reaktionszeit und die Arbeitsspeicherauslastung in Echtzeit, direkt von der Anwendung und ohne jegliche Änderungen am Code.

Geschäftsmetriken sind eng mit den Geschäftsergebnissen verknüpft. Viele Organisationen verfügen über komplexe Metriken, mit denen eindeutige Geschäftsergebnisse gemessen werden, und diese Ergebnisse können von finanziell und agilitätsbezogen bis hin zu Leistungs- und Kundenbindungszielen reichen. AppDynamics sammelt die Metriken, die für Ihre Organisation spezifisch und nützlich sind, und diese Metriken können vor und nach einer Migration zu den aktuellen Geschäftsvorgängen beitragen.

**Beispiel:**

Ein Unternehmen, das Widgets aus einem Online-Marketplace verkauft, hat die folgenden Schlüsselgeschäftstransaktionen in seiner Webanwendung ermittelt:

- Startseite
- In den Warenkorb
- Versand
- Abrechnung
- Bestellung bestätigen

Diese Arten von Geschäftstransaktionen sind gängig für E-Commerce-Anwendungen. Die Journey, die ein Benutzer durch diese Seiten absolviert, ist ein Abschlusstrichter, und er führt direkt zu einem Verkaufsumsatz auf der Unternehmensplattform. Wenn Benutzer die Journey aufgrund von schlechter Seitenleistung oder Fehlern abbrechen, wirkt sich dies direkt auf den zugrunde liegenden Gewinn des Unternehmens aus.

Zusätzlich hat das Unternehmen hat die folgenden Schlüsselgeschäftsmetriken identifiziert:

- Warenkorbsummen
- Kundensegmente
- Kundenstandorte

Das Kombinieren von Anwendungs- und Geschäftsleistungsmetriken hilft, klar zu verdeutlichen, wie die Leistung der Anwendung mit dem zugrunde liegenden Gewinn in Beziehung steht. Dieser Grad von Sichtbarkeit und diese Arten von Erkenntnissen sind während Migrationen von entscheidender Bedeutung.

Konfigurierbare Dashboards sind eines von vielen AppDynamics-Tools, die diese Erkenntnisse visualisieren. In diesem Echtzeitbeispiel sehen wir den gesamten Abschlusstrichter und die Auswirkungen auf die Leistung einzelner Seiten gegenüber Aussteigern, zusammen mit Warenkorbsummen, Kundensegment, -standort und allgemeinen Umsatzdetails.

![AppDynamics-Geschäftsauswirkungs-Dashboard](./media/app-dynamics-business-impact-dashboard.jpg)

_Abbildung 2: AppDynamics-Geschäftsauswirkungs-Dashboard._

## <a name="resources-to-help-identify-business-metrics"></a>Ressourcen zur Ermittlung von Geschäftsmetriken

In den Abschnitten [Strategie](../strategy/index.md) und [Geschäftsergebnisse](../strategy/business-outcomes/index.md) des Frameworks für die Cloudeinführung (Cloud Adoption Framework) finden Sie Anleitungen und Strategien, die Ihnen helfen, Geschäftsergebnisse für Ihre Organisation zu ermitteln.

## <a name="pre--and-post-migration-comparison"></a>Vergleich zwischen vor und nach der Migration

Die Cloud bietet umfassende Vorteile und Potenzial, doch die ersten Schritte einer Migration sind häufig unklar und risikoreich. Eine erfolgreiche Migration muss anhand von mehr Kriterien ausgewertet werden, als der Möglichkeit einer erfolgreichen Bereitstellung. Das Verständnis der Benutzererfahrung und Geschäftsleistung vor und nach der Cloudmigration hilft Ihnen dabei, beides im Bedarfsfall anzupassen und zu stabilisieren. Dies kann bei der Produktion erfolgreicher Geschäftsergebnisse helfen und gleichzeitig den Wert verstärken, den Azure während der Migrations-Journey bietet.

Um auf dem Verständnis aufzubauen, wie AppDynamics Geschäfts- und Anwendungsmetriken bereitstellt, vergleichen Sie diese Metriken vor und nach einer Migration, um deren Erfolg zu bewerten und zu ermitteln, ob die Geschäftsergebnisziele erreicht werden.

**Beispiel:**

Movie Tickets Online, ein fiktiver Onlinetickethändler, arbeiten daran, seine bestehenden Rechenzentren aufzugeben und seine Workloads in Azure zu verlagern. Ihre Kapazitätsprobleme haben zu einer schlechten Leistung bei Geschäftstransaktionen geführt, und sie sehen den Leistungsoptimierungen sowie der Kapazität in Azure gespannt entgegen.

Zusätzlich zur Verbesserung der Leistung möchten sie sicherstellen, dass die Geschäftsergebnisse der Verbesserung ihrer Abschlusstrichter und der Steigerung von Umsätzen erreicht werden. Im Rahmen ihrer Migration haben sie AppDynamics für ihre vorhandenen lokalen Umgebungen bereitgestellt, um deren aktuelle Leistung ganz klar zu verstehen. Als Teil der Cloudbereitstellung kann Movie Tickets Online die native AppDynamics-Integration in Azure verwenden, um Leistung und Geschäftsergebnisse nach der Migration nachzuvollziehen.

In diesem Fall konnten Sie einen Anstieg der Abschlussraten von 48 auf 79 Prozent sowie Verbesserungen bei der zugrunde liegenden Leistung, Reaktionszeit und den Ticketverkaufsvolumen erkennen.

![Vergleich der AppDynamics-Migration](./media/app-dynamics-migration-comparison.jpg)

_Abbildung 3: Vergleich der AppDynamics-Migration._

## <a name="next-steps"></a>Nächste Schritte

AppDynamics bietet Organisationen die einzigartige Möglichkeit, die Geschäftsergebnisse während ihrer Strategie für die Cloudeinführung zu messen. Besuchen Sie [AppDynamics](https://www.appdynamics.com/product/infrastructure-monitoring/cloud-monitoring/microsoft-azure), um mehr über AppDynamics mit Azure zu erfahren.
