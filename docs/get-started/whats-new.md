---
title: Neues
description: Enthält Informationen zu kürzlich durchgeführten Updates für das Framework für die Einführung der Microsoft Cloud (Microsoft Cloud Adoption Framework) für Azure.
author: JanetCThomas
ms.author: janet
ms.date: 03/27/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: f4dcf7409e9aa8eceb548f0bd54d0decdab7357e
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83620878"
---
<!-- markdownlint-disable MD024 -->

# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Neuerungen beim Framework für die Einführung der Microsoft Cloud für Azure

Hier ist eine Liste mit den Änderungen angegeben, die kürzlich am Framework für die Cloudeinführung vorgenommen wurden.

Dieses Framework wurde in Zusammenarbeit mit Kunden, Partnern und internen Microsoft-Teams entwickelt. Neuer und aktualisierter Inhalt wird veröffentlicht, sobald er verfügbar ist. Mit diesen Releases können Sie die Anleitung zusammen mit uns testen, überprüfen und optimieren. Wir laden Sie ein, als Partner mit uns gemeinsam das Framework für die Cloudeinführung für Azure zu entwickeln.

## <a name="may-15-2020"></a>15. Mai 2020

Basierend auf Feedback haben wir neue Inhalte erstellt, um Ihnen den Einstieg in die Verwendung des Cloud Adoption Frameworks zu erleichtern. Die neuen Leitfäden zu den ersten Schritten helfen Ihnen, im Framework basierend auf den gewünschten Zielvorgaben zu navigieren.

| Artikel | BESCHREIBUNG |
|---|---|
| [Erste Schritte mit dem Cloud Adoption Framework](./index.md) | Beginnen Sie hier, um einen Leitfaden mit ersten Schritten auszuwählen, der für Ihre Zielvorgaben in Bezug auf die Cloudeinführung geeignet ist. Diese gängigen Szenarien bieten eine Roadmap für das Microsoft Cloud Adoption Framework für Azure.|
| [Verstehen und Dokumentieren grundlegender Ausrichtungsentscheidungen](./cloud-concepts.md) | Informieren Sie sich über die anfänglichen Entscheidungen, die von jedem Teammitglied verstanden werden sollten, das an der Cloudeinführung beteiligt ist. |
| [Grundlegendes zur Portfoliohierarchie und deren Ausrichtung](../reference/fundamental-concepts/hosting-hierarchy.md) | Erfahren Sie, wie eine Portfoliohierarchie zeigt, wie Ihre Workloads und die unterstützenden Dienste zusammenpassen. |
| [Wie unterstützen die Azure-Produkte die Portfoliohierarchie?](../reference/fundamental-concepts/hierarchy-azure-tools.md) | Erfahren Sie mehr über die Azure-Tools und -Lösungen, die Ihre Portfoliohierarchie unterstützen. |
| [Verwalten der Organisationsausrichtung](../organize/index.md) | Richten Sie gut ausgestattete Organisationsstrukturen ein, die ein effektives Betriebsmodell für die Cloud sind. |

## <a name="april-14-2020"></a>14. April 2020

Wir haben alle Tools und Vorlagen für die Cloudeinführung an einem Ort zusammengeführt, damit sie leichter zu finden sind.

| Artikel | BESCHREIBUNG |
|----------|-------------|
| [Tools und Vorlagen](../reference/tools-templates.md) | Hier finden Sie die Tools, Vorlagen und Bewertungen, mit deren Hilfe Sie die Cloudeinführung beschleunigen können. |

## <a name="april-4-2020"></a>4\. April 2020

Weitere Iteration der Verfeinerung von Migrationsmethodik und Bereitschaftsmethodik, um das Feedback von Microsoft-Kunden und -Partnern und internen Microsoft-Programmen stärker zu berücksichtigen.

### <a name="migrate-updates"></a>Aktualisierungen in Bezug auf die Migration

| Artikel                                                                                                                 | BESCHREIBUNG                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Migrationsmethodik](../migrate/index.md)                       | Diese Änderungen rationalisieren die Phasen des Migrationsaufwands (Bewertung, Bereitstellung und Freigabe der Workloads). Durch die Änderungen werden auch die Details bezüglich des Backlogs der Migration beseitigt. Das Entfernen dieser Details und der Verweis auf die Methoden „Plan“, „Ready“ und „Adopt“ (Planen, Vorbereiten und Einführen) schafft stattdessen Flexibilität für verschiedene Cloudeinführungsprogramme, um diese besser auf die Methodik abzustimmen.  |
| Aktualisieren des Inhaltsverzeichnisses                       | Die Inhaltsverzeichnisse des Leitfadens zur Azure-Migration und der Prozessverbesserungen wurden aktualisiert, um die Änderungen in der Methodik widerzuspiegeln.  |

### <a name="ready-updates"></a>Aktualisierungen in Bezug auf die Bereitschaft

| Artikel                                                                                                                 | BESCHREIBUNG                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Umgestalten von Zielzonen](../ready/landing-zone/refactor.md)                       | **Neuer Artikel:** Ausgehend von Workshops zur Bereitschaftsmethodik veranschaulicht dieser Artikel die Theorie, mit einer anfänglichen Vorlage zu beginnen, Entscheidungsstrukturen und Refactoring zu nutzen, um die Zielzone zu erweitern, und sich auf einen zukünftigen Zustand der Unternehmensbereitschaft zuzubewegen. |
| [Erweitern der Zielzone](../ready/considerations/index.md)                       | **Neuer Artikel:** Baut auf dem Abschnitt über parallele Iterationen des Artikels zum Refactoring auf, um zu zeigen, wie verschiedene Arten von Zielzonenerweiterungen gemeinsame Prinzipien in die unterstützende Plattform einbetten würden. Der ursprüngliche Inhalt für diese Übersicht wurde in den Knoten [Grundlegende Überlegungen zu Zielzonen](../ready/considerations/basic-considerations.md) im Inhaltsverzeichnis verschoben. |
| [Testgesteuerte Entwicklung (TDD) für Zielzonen](../ready/considerations/test-driven-development.md)                       | **Neuer Artikel:** Der Refactoringansatz wird durch die Einführung eines testgesteuerten Entwicklungszyklus, der die Entwicklung der Zielzone und das Refactoring steuert, erheblich verbessert. |
| [Testgesteuerte Entwicklung (TDD) der Zielzone in Azure](../ready/considerations/azure-test-driven-development.md)                       | **Neuer Artikel:** Azure Governance-Tools bieten eine vielfältige Plattform für TDD-Zyklen oder Rot/Grün-Tests. |
| [Erhöhen der Sicherheit von Zielzonen](../ready/considerations/landing-zone-security.md)                       | **Neuer Artikel:** Übersicht über die bewährten Methoden in diesem Abschnitt, mit einem Rückbezug auf den TDD-Zyklus |
| [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-operations.md)                       | **Neuer Artikel:** Liste der bewährten Methoden in der „Manage“-Methodik, mit einem Übergang zu diesem modularen Ansatz zur Verbesserung von Betrieb, Zuverlässigkeit und Leistung. |
| [Verbessern der Governance von Zielzonen](../ready/considerations/landing-zone-governance.md)                       | **Neuer Artikel:** Liste der bewährten Methoden in der „Govern“-Methodik, mit einem Übergang zu diesem modularen Ansatz zur Verbesserung von Governance, Cost Management und Skalierung. |
| [Auf Unternehmensniveau beginnen](../ready/considerations/enterprise-scale.md)                       | **Neuer Artikel:** Veranschaulichen Sie einen Ansatz, der die Unterschiede im Prozess aufzeigt, wenn ein Kunde mit Zielzonenvorlagen auf Unternehmensniveau beginnt. Dieser Artikel hilft Kunden dabei, die Qualifizierer zu verstehen, die diese Entscheidung unterstützen würden. |
| Aktualisieren des Inhaltsverzeichnisses                       | Das Inhaltsverzeichnis wurde aktualisiert, um die neuen Artikel widerzuspiegeln.  |

## <a name="march-27-2020"></a>27. März 2020

Wir haben einen Leitfaden zu den anfänglichen Abonnements hinzugefügt, die Sie bei der Einführung von Azure erstellen sollten.

### <a name="ready-updates"></a>Aktualisierungen in Bezug auf die Bereitschaft

| Artikel                                                                                                                 | BESCHREIBUNG                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Erstellen Ihrer anfänglichen Azure-Abonnements](../ready/azure-best-practices/initial-subscriptions.md)                       | **Neuer Artikel:** Erstellen Sie Ihre anfänglichen Produktions- und Nichtproduktionsabonnements, und entscheiden Sie, ob Sie Sandboxabonnements sowie ein Abonnement für gemeinsame Dienste erstellen. |
| [Erstellen zusätzlicher Abonnements zum Skalieren Ihrer Azure-Umgebung](../ready/azure-best-practices/scale-subscriptions.md) | Hier erfahren Sie mehr über die Gründe für das Erstellen zusätzlicher Abonnements sowie das Verschieben von Ressourcen zwischen Abonnements, und Sie erhalten Tipps zum Erstellen neuer Abonnements.                                                   |
| [Organisieren und Verwalten mehrerer Azure-Abonnements](../ready/azure-best-practices/organize-subscriptions.md)             | Erstellen Sie eine Verwaltungsgruppenhierarchie, um Ihre Azure-Abonnements zu organisieren, zu verwalten und zu steuern.                                                                                         |

## <a name="march-20-2020"></a>20. März 2020

Wir haben eine ausführliche Anleitung hinzugefügt, in der die Tools, Programme und Inhalte nach Rollen kategorisiert sind, um die erfolgreiche Bereitstellung von Anwendungen in Kubernetes zu fördern – von der Proof of Concept-Phase bis zur Produktion, gefolgt von Skalierung und Optimierung.

### <a name="kubernetes"></a>Kubernetes

| Artikel                                                                                     | BESCHREIBUNG                                                                                                                                                                           |
|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Anwendungsentwicklung und Bereitstellung](../innovate/kubernetes/application-development.md) | **Neuer Artikel:** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Planung der Anwendungsentwicklung, die Konfiguration von CI/CD-Pipelines und die Implementierung von Websitezuverlässigkeits-Engineering (Site Reliability Engineering) für Kubernetes. |
| [Clusterentwurf und Vorgänge](../innovate/kubernetes/cluster-design-operations.md) | **Neuer Artikel:** Enthält Prüflisten, Ressourcen und bewährte Methoden für Clusterkonfiguration, Netzwerkentwurf, zukunftssichere Skalierbarkeit, Geschäftskontinuität und Notfallwiederherstellung für Kubernetes. |
| [Cluster- und Anwendungssicherheit](../innovate/kubernetes/cluster-application-security.md) | **Neuer Artikel:** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Kubernetes-Sicherheit, -Planung, -Produktion und -Skalierung. |

## <a name="march-2-2020"></a>2\. März 2020

<!-- docsTest:ignore "Strategy, Plan, Ready, and Migrate" -->

Als Reaktion auf das erhaltene Feedback zur Kontinuität des Migrationsansatzes in mehreren Abschnitten des Frameworks für die Cloudeinführung, z. B. Strategie, Plan, Bereitschaft und Migration, haben wir die folgenden Aktualisierungen vorgenommen. Diese Aktualisierungen sind so konzipiert, dass Sie die Planungs- und Einführungsverbesserungen während einer Migrationsjourney leichter verstehen.

### <a name="strategy-updates"></a>Aktualisierungen in Bezug auf die Strategie

| Artikel                                                                       | BESCHREIBUNG                                                                                                                                    |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [Ausgewogenheit des Portfolios](../strategy/balance-the-portfolio.md)                 | Dieser Artikel wurde verschoben, damit er zu einem früheren Zeitpunkt der Strategiemethodik erscheint. So erhalten Sie an einem früheren Punkt des Lebenszyklus Einblick in den Denkprozess. |
| [Abstimmen&nbsp;konkurrierender&nbsp;Prioritäten](../strategy/balance-competing-priorities.md) | **Neuer Artikel:** Es wird beschrieben, wie Sie Prioritäten für Methodiken so abstimmen, dass dies Ihrer Strategie nützt.                                         |

### <a name="plan-updates"></a>Aktualisierungen in Bezug auf den Plan

| Artikel                                                                       | BESCHREIBUNG                                                                                                                                                                           |
|-------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Bewährte Methoden&nbsp;für&nbsp;Bewertungen](../plan/contoso-migration-assessment.md) | Dieser Artikel wurde in den neuen Abschnitt „Bewährte Methoden“ der Planmethodik verschoben. So erhalten Sie zu einem früheren Zeitpunkt des Lebenszyklus Einblick in die Bewertung von lokalen Umgebungen. |

### <a name="ready-updates"></a>Aktualisierungen in Bezug auf die Bereitschaft

| Artikel                                                                   | BESCHREIBUNG                                                                                                              |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| [Was&nbsp;ist&nbsp;eine&nbsp;Zielzone?&nbsp;](../ready/landing-zone/index.md)                 | **Neuer Artikel:** Enthält eine Definition des Begriffs „Zielzone“.                                                      |
| [Erste Zielzone](../ready/landing-zone/first-landing-zone.md)         | **Neuer Artikel:** Enthält weitere Informationen zum Vergleich verschiedener Zielzonen.                                                     |
| [CAF-Migrationslandezone](../ready/landing-zone/migrate-landing-zone.md) | Die Definition der Blaupause für das Framework für die Cloudeinführung wurde von der Auswahl der ersten Zielzone getrennt.         |
| [Terraform-Zielzone](../ready/landing-zone/terraform-landing-zone.md) | Wurde in den neuen Abschnitt „Zielzone“ der Bereitschaftsmethodik verschoben, um Terraform in Bezug auf Zielzonen als wichtigere Komponente darzustellen. |

### <a name="migration-updates"></a>Aktualisierungen in Bezug auf die Migration

| Artikel                                                                                          | BESCHREIBUNG                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Übersicht](../migrate/azure-migration-guide/index.md)                                            | Diese Aktualisierung umfasst eine eindeutigere Beschreibung des Leitfadens und eine Verringerung der Schritte.                                                                                                        |
| [Bewerten](../migrate/azure-migration-guide/assess.md)                                             | Der Abschnitt „Hinterfragen der Annahmen“ wurde hinzugefügt, um zu verdeutlichen, wie diese Bewertungsebene zum Ansatz zur inkrementellen Bewertung passt, der in der Planmethodik beschrieben ist. |
| [Klassifizierung bei Bewertungsprozessen](../migrate/migration-considerations/assess/classify.md) | **Neuer Artikel:** Enthält eine Beschreibung der Klassifizierung jeder Ressource und Workload vor der Migration.                                                                    |
| [Migrieren](../migrate/azure-migration-guide/migrate.md)                                           | Als Reaktion auf Feedback bei Tier 1-Konferenzen wurde den Drittanbieter-Tooloptionen ein Verweis auf UnifyCloud hinzugefügt.                                                         |
| [Testen,&nbsp;Optimieren&nbsp;und&nbsp;Höherstufen](../migrate/azure-migration-guide/optimize-and-transform.md)        | Der Titel dieses Artikels wurde an andere Vorschläge zur Prozessverbesserung angepasst.                                                                                           |
| [Übersicht über die Bewertung](../migrate/migration-considerations/assess/index.md)                           | Es wurde eine Aktualisierung durchgeführt, um besser darzustellen, dass es bei der Bewertung in dieser Phase um die Bewertung der technischen Eignung einer bestimmten Workload und die zugehörigen Ressourcen geht.                               |
| [Checkliste für die Planung](../migrate/migration-considerations/prerequisites/planning-checklist.md)    | Aktualisierung zur Verdeutlichung der Wichtigkeit einer Vorgangsausrichtung während der Planung von Migrationsmaßnahmen, um nach der Migration eine gut verwaltete Workload zu erhalten.                  |

<!-- docsTest:ignoreNextStep -->
