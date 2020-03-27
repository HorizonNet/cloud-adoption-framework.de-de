---
title: Neues
description: Enthält Informationen zu kürzlich durchgeführten Updates für das Framework für die Einführung der Microsoft Cloud (Microsoft Cloud Adoption Framework) für Azure.
author: JanetCThomas
ms.author: janet
ms.date: 03/09/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c7b3a4d946eac1b5296f4d37d50872105ce756ea
ms.sourcegitcommit: 25cd1b3f218d0644f911737a6d5fd259461b2458
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/24/2020
ms.locfileid: "80225954"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Neuerungen beim Framework für die Einführung der Microsoft Cloud für Azure

Hier ist eine Liste mit den Änderungen angegeben, die kürzlich am Framework für die Cloudeinführung vorgenommen wurden.

Dieses Framework wurde in Zusammenarbeit mit Kunden, Partnern und internen Microsoft-Teams entwickelt. Neuer und aktualisierter Inhalt wird veröffentlicht, sobald er verfügbar ist. Mit diesen Releases können Sie die Anleitung zusammen mit uns testen, überprüfen und optimieren. Wir laden Sie ein, als Partner mit uns gemeinsam das Framework für die Cloudeinführung für Azure zu entwickeln.

## <a name="march-20-2020"></a>20. März 2020

Wir haben eine ausführliche Anleitung hinzugefügt, in der die Tools, Programme und Inhalte nach Rollen kategorisiert sind, um die erfolgreiche Bereitstellung von Anwendungen in Kubernetes zu fördern – von der Proof of Concept-Phase bis zur Produktion, gefolgt von Skalierung und Optimierung.

### <a name="kubernetes"></a>Kubernetes

| Artikel                                                                                     | BESCHREIBUNG                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Anwendungsentwicklung und Bereitstellung](../innovate/kubernetes/application-development.md) | **Neuer Artikel** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Planung der Anwendungsentwicklung, die Konfiguration von DevOps-Pipelines und die Implementierung von Websitezuverlässigkeits-Engineering (Site Reliability Engineering) für Kubernetes. |
| [Clusterentwurf und Vorgänge](../innovate/kubernetes/cluster-design-operations.md) | **Neuer Artikel** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Bereiche Clusterkonfiguration, Netzwerkentwurf, zukunftssichere Skalierbarkeit, Geschäftskontinuität und Notfallwiederherstellung für Kubernetes. |
| [Cluster- und Anwendungssicherheit](../innovate/kubernetes/cluster-application-security.md) | **Neuer Artikel** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Kubernetes-Sicherheit, -Planung, -Produktion und -Skalierung. |

## <a name="march-2-2020"></a>2\. März 2020

Als Reaktion auf das erhaltene Feedback zur Kontinuität des Migrationsansatzes in mehreren Abschnitten des Frameworks für die Cloudeinführung, z. B. Strategie, Plan, Bereitschaft und Migration, haben wir die folgenden Aktualisierungen vorgenommen. Diese Aktualisierungen sind so konzipiert, dass Sie die Planungs- und Einführungsverbesserungen während einer Migrationsjourney leichter verstehen.

### <a name="strategy-updates"></a>Aktualisierungen in Bezug auf die Strategie

| Artikel                                                                       | BESCHREIBUNG                                                                                                                                    |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [Ausgewogenheit des Portfolios](../strategy/balance-the-portfolio.md)                 | Dieser Artikel wurde verschoben, damit er zu einem früheren Zeitpunkt der Strategiemethodik erscheint. So erhalten Sie an einem früheren Punkt des Lebenszyklus Einblick in den Denkprozess. |
| [Abstimmen&nbsp;konkurrierender&nbsp;Prioritäten](../strategy/balance-competing-priorities.md) | **Neuer Artikel**: Es wird beschrieben, wie Sie Prioritäten für Methodiken so abstimmen, dass dies Ihrer Strategie nützt.                                         |

### <a name="plan-updates"></a>Aktualisierungen in Bezug auf den Plan

| Artikel                                                             | BESCHREIBUNG                                                                                                                                                                           |
|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Bewährte Methoden&nbsp;für&nbsp;Bewertungen](../plan/contoso-migration-assessment.md) | Dieser Artikel wurde in den neuen Abschnitt „Bewährte Methoden“ der Planmethodik verschoben. So erhalten Sie zu einem früheren Zeitpunkt des Lebenszyklus Einblick in die Bewertung von lokalen Umgebungen. |

### <a name="ready-updates"></a>Aktualisierungen in Bezug auf die Bereitschaft

| Artikel                                                                   | BESCHREIBUNG                                                                                                              |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| [Was&nbsp;ist&nbsp;eine&nbsp;Zielzone?&nbsp;](../ready/landing-zone/index.md)                 | **Neuer Artikel**: Enthält eine Definition des Begriffs „Zielzone“.                                                                          |
| [Erste Zielzone](../ready/landing-zone/first-landing-zone.md)         | **Neuer Artikel**: Enthält weitere Informationen zum Vergleich verschiedener Zielzonen.                                                     |
| [Bereitstellen einer Zielzone für die Migration](../ready/landing-zone/migrate-landing-zone.md)     | Die Definition der Blaupause für das Framework für die Cloudeinführung wurde von der Auswahl der ersten Zielzone getrennt.         |
| [Terraform-Zielzone](../ready/landing-zone/terraform-landing-zone.md) | Wurde in den neuen Abschnitt „Zielzone“ der Bereitschaftsmethodik verschoben, um Terraform in Bezug auf Zielzonen als wichtigere Komponente darzustellen. |

### <a name="migration-updates"></a>Aktualisierungen in Bezug auf die Migration

| Artikel                                                                                          | BESCHREIBUNG                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Übersicht](../migrate/azure-migration-guide/index.md)                                            | Diese Aktualisierung umfasst eine eindeutigere Beschreibung des Leitfadens und eine Verringerung der Schritte.                                                                                                        |
| [Bewerten](../migrate/azure-migration-guide/assess.md)                                             | Der Abschnitt „Hinterfragen der Annahmen“ wurde hinzugefügt, um zu verdeutlichen, wie diese Bewertungsebene zum Ansatz zur inkrementellen Bewertung passt, der in der Planmethodik beschrieben ist. |
| [Klassifizierung bei Bewertungsprozessen](../migrate/migration-considerations/assess/classify.md) | **Neuer Artikel**: Enthält eine Beschreibung der Klassifizierung jeder Ressource und Workload vor der Migration.                                                                    |
| [Migrieren](../migrate/azure-migration-guide/migrate.md)                                           | Als Reaktion auf Feedback bei Tier 1-Konferenzen wurde den Drittanbieter-Tooloptionen ein Verweis auf UnifyCloud hinzugefügt.                                                         |
| [Testen,&nbsp;Optimieren&nbsp;und&nbsp;Höherstufen](../migrate/azure-migration-guide/optimize-and-transform.md)        | Der Titel dieses Artikels wurde an andere Vorschläge zur Prozessverbesserung angepasst.                                                                                           |
| [Übersicht über die Bewertung](../migrate/migration-considerations/assess/index.md)                           | Es wurde eine Aktualisierung durchgeführt, um besser darzustellen, dass es bei der Bewertung in dieser Phase um die Bewertung der technischen Eignung einer bestimmten Workload und die zugehörigen Ressourcen geht.                               |
| [Checkliste für die Planung](../migrate/migration-considerations/prerequisites/planning-checklist.md)    | Aktualisierung zur Verdeutlichung der Wichtigkeit einer Vorgangsausrichtung während der Planung von Migrationsmaßnahmen, um nach der Migration eine gut verwaltete Workload zu erhalten.                  |
