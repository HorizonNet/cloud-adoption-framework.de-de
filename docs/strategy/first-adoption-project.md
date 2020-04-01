---
title: Erstes Cloudeinführungsprojekt
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit den Prozessen für die Cloudeinführung und den Betrieb von in der Cloud gehosteten Workloads vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 063fc4074a7b5972b6b2938abdcb90937412e832
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353545"
---
<!-- markdownlint-disable MD026 -->

# <a name="first-cloud-adoption-project"></a>Erstes Cloudeinführungsprojekt

Die Planung der Cloudeinführung ist mit einer Lernkurve und Zeitaufwand verbunden. Selbst für erfahrene Teams nimmt die richtige Planung viel Zeit in Anspruch: Zeit, um die Projektbeteiligten aufeinander abzustimmen, Zeit, um Daten zu sammeln und zu analysieren, Zeit, um langfristige Entscheidungen zu überprüfen, und Zeit, um Menschen, Prozesse und Technologien aufeinander abzustimmen. Bei den produktivsten Einführungsbemühungen wächst die Planung parallel zur Einführung weiter und verbessert sich mit jedem Release und jeder Workloadmigration in die Cloud. Es ist wichtig, den Unterschied zwischen einem Cloudeinführungsplan und einer Cloudeinführungsstrategie zu kennen. Sie benötigen eine klar definierte Strategie, um die Implementierung eines Cloudeinführungsplans zu vereinfachen und zu unterstützen.

Das Cloud Adoption Framework für Azure beschreibt die Prozesse für die Cloudeinführung und den Betrieb von Workloads, die in der Cloud gehostet werden. Für jeden Prozesse in den Phasen „Definieren der Strategie“, „Plan“, „Bereit“, „Einführung“ und „Betrieb“ müssen technischen, geschäftlichen und operativen Fähigkeiten geringfügig erweitert werden. Einige dieser Fähigkeiten können durch gezieltes Lernen erworben werden. Viele dieser Fähigkeiten werden jedoch am effektivsten durch praktische Erfahrungen erworben.

Der Beginn eines ersten Einführungsprozesses parallel zur Entwicklung des Plans bietet einige Vorteile:

- Aufbau einer wachstumsorientierten Mentalität, die das Lernen und Erforschen fördert
- Bereitstellung einer Möglichkeit für das Team, die notwendigen Fähigkeiten zu entwickeln
- Schaffung von Situationen, die neue Ansätze für die Zusammenarbeit aufzeigen
- Bestimmung von Qualifikationslücken und Anforderungen an potenzielle Partnerschaften
- Bereitstellung konkreter Beiträge für den Plan

## <a name="first-project-criteria"></a>Kriterien für das erste Projekt

Ihr erstes Einführungsprojekt sollte mit Ihren [Beweggründen](./motivations.md) für die Einführung der Cloud übereinstimmen. Soweit möglich, sollte Ihr erstes Projekt auch Fortschritte in Richtung eines definierten [Geschäftsergebnisses](./business-outcomes/business-outcome-template.md) nachweisen.

## <a name="first-project-expectations"></a>Erwartungen an das erste Projekt

Beim ersten Einführungsprojekt Ihres Teams wird wahrscheinlich eine Art Produktionsbereitstellung entstehen. Dies ist jedoch nicht immer der Fall. Definieren Sie frühzeitige entsprechende Erwartungen. Hier sind einige sinnvolle Erwartungen formuliert:

- Dieses Projekt bietet die Möglichkeit zum Lernen.
- Dieses Projekt kann zu einer Produktionsbereitstellung führen, erfordert aber wahrscheinlich zunächst zusätzlichen Aufwand.
- Das Ergebnis dieses Projekts ist eine Reihe klarer Anforderungen an eine längerfristige Produktionslösung.

## <a name="first-project-examples"></a>Beispiele für das erste Projekt

Zur Unterstützung der obigen Kriterien enthält diese Liste ein Beispiel für ein erstes Projekt für jede Kategorie von Beweggründen:

- **Wichtige Unternehmensereignisse:** Wenn ein wichtiges Unternehmensereignis der primäre Beweggrund ist, könnte die Implementierung eines Tools wie [Azure Site Recovery](../migrate/azure-migration-guide/migrate.md?tabs=Tools#azure-site-recovery) ein gutes erstes Projekt sein. Während der Migration können Sie dieses Tool zur schnellen Migration von Rechenzentrumsressourcen verwenden. Im ersten Projekt könnten Sie es jedoch ausschließlich als reines Tool für die Notfallwiederherstellung einsetzen, um die Abhängigkeit von Notfallwiederherstellungsressourcen im Rechenzentrum zu reduzieren.

- **Beweggründe für Migration:** Wenn eine Migration der primäre Beweggrund ist, ist es ratsam, mit der Migration einer unkritischen Workload zu beginnen. Für die Migration Ihrer ersten Workload können der [Leitfaden für die Azure-Einrichtung](../ready/azure-setup-guide/index.md) und der [Leitfaden zur Azure-Migration](../migrate/azure-migration-guide/index.md) als Anleitung herangezogen werden.

- **Beweggründe für Innovation:** Wenn Innovationen der primäre Beweggrund sind, könnte die Erstellung einer gezielten Entwicklungs-/Testumgebung ein ideales erstes Projekt sein.

Weitere Beispiele für erste Einführungsprojekte sind unter anderem:

- **Business Continuity & Disaster Recovery (BCDR):** Neben Azure Site Recovery können Sie mehrere BCDR-Strategien als erstes Projekt implementieren.
- **Nicht produktionsbezogen:** Stellen Sie eine nicht produktionsbezogene Instanz einer Workload bereit.
- **Archiv:** Cold Storage kann eine Belastung für Rechenzentrumsressourcen sein. Die Migration dieser Daten in die Cloud kann schnell zum Erfolg führen.
- **Ende des Supports (EOS):** Die Migration von Ressourcen, die das Ende des Supports erreicht haben, ist eine weitere schnelle Möglichkeit, die technischen Qualifikationen zu erweitern. Außerdem könnten so Kosten durch teure Supportverträge oder Lizenzierungskosten vermieden werden.
- **Virtuelle Desktopschnittstelle (VDI):** Das Erstellen von virtuellen Desktops für Remotemitarbeiter kann schnell zum Erfolg führen. In einigen Fällen könnte dieses erste Einführungsprojekt auch die Abhängigkeit von teuren privaten Netzwerken zugunsten einer öffentlichen Internetverbindung reduzieren.
- **Dev/Test:** Entfernen Sie Dev/Test aus lokalen Umgebungen, um Entwicklern Kontrolle, Flexibilität und Self-Service-Kapazitäten zu bieten.
- **Einfache Apps (weniger als fünf):** Modernisieren und migrieren Sie eine einfache App, um schnell Entwickler- und Betriebsexpertise aufzubauen.
- **Leistungslabs:** Wenn Sie eine Labumgebung mit hoher Leistung benötigen, können Sie diese Labs mit der Cloud für kurze Zeit schnell und kostengünstig bereitstellen.
- **Datenplattform:** Erstellen Sie einen Data Lake mit skalierbarer Computeressource für Analyse-, Berichterstellungs- oder Machine Learning-Workloads, und migrieren Sie unter Verwendung von Sicherungs-/Wiederherstellungsmethoden oder mithilfe von Datenmigrationsdiensten zu verwalteten Datenbanken.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über Strategien zum [Abwägen konkurrierender Prioritäten](./balance-competing-priorities.md).

> [!div class="nextstepaction"]
> [Ausgewogenheit konkurrierender Prioritäten](./balance-competing-priorities.md)
