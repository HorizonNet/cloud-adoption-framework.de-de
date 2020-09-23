---
title: Neues
description: Enthält Informationen zu kürzlich durchgeführten Updates für das Framework für die Einführung der Microsoft Cloud (Microsoft Cloud Adoption Framework) für Azure.
author: JanetCThomas
ms.author: janet
ms.date: 08/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: a8f3afe5e08e415fc4fb08e1036dd559a66747ba
ms.sourcegitcommit: 4e12d2417f646c72abf9fa7959faebc3abee99d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90775580"
---
<!-- docutune:casing "internal Microsoft teams" OneMigrate -->
<!-- cSpell:ignore MSPs Teradata Netezza Exadata mlops -->

# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Neuerungen beim Framework für die Einführung der Microsoft Cloud für Azure

Hier ist eine Liste mit den Änderungen angegeben, die kürzlich am Framework für die Cloudeinführung vorgenommen wurden.

Dieses Framework wurde in Zusammenarbeit mit Kunden, Partnern und internen Microsoft-Teams entwickelt. Neuer und aktualisierter Inhalt wird veröffentlicht, sobald er verfügbar ist. Mit diesen Releases können Sie die Anleitung zusammen mit uns testen, überprüfen und optimieren. Wir laden Sie ein, als Partner gemeinsam mit uns das Cloud Adoption Framework zu entwickeln.

## <a name="august-25-2020"></a>25. August 2020

Diese Veröffentlichung bietet eine bessere Definition und bessere Entscheidungskriterien für die Implementierung von Zielzonen.

### <a name="operating-model"></a>Betriebsmodell

Eine der wichtigsten Aspekte beim Entwurf und der Implementierung von Zielzonen ist das Betriebsmodell. Die Art und Weise, wie Sie in der Cloud arbeiten möchten, hat einen direkten Einfluss auf die Architektur und die zu implementierenden Optionen. Die folgenden Artikel helfen Ihnen dabei, Ihr Zielbetriebsmodell mit einigen wenigen, in der Cloud gängigen Modellen auszurichten. Ordnen Sie diese dann der am besten geeigneten Implementierung zu, um damit zu beginnen.

| Artikel | Beschreibung |
|---|---|
| [Vergleichen gängiger Betriebsmodelle](../operating-model/compare.md) | Dieser Artikel ist der primäre Leitfaden für den Vergleich von Betriebsmodellen und die Wahl einer Vorgehensweise. |
| [Grundlegendes zu Cloudbetriebsmodellen](../operating-model/index.md) | Einführung zu Importentscheidungen bezüglich Ihres Betriebsmodells. |
| [Definieren Ihres Betriebsmodells mit CAF](../operating-model/define.md) | Das Cloud Adoption Framework ist eine schrittweise Anleitung zum Erstellen Ihrer Umgebung und zur Einführung der Cloud innerhalb des von Ihnen gewählten Betriebsmodells. In diesem Artikel wird ein Bezugsrahmen geschaffen, um zu vermitteln, wie die verschiedenen Methodiken die Entwicklung Ihres Betriebsmodells unterstützen. |
| [Nutzungsbedingungen](../operating-model/terms.md) | Begriffe, die wahrscheinlich auftreten werden, wenn Ihr Betriebsmodell mit Ansprechpartnern diskutiert wird. Diese Begriffe werden von Architekten oder technischen Fachleuten nicht so häufig verwendet, aber sie werden sich in diesen Unterhaltungen als wichtig erweisen. |

### <a name="azure-landing-zones-additional-implementation-options"></a>Azure-Zielzonen: Zusätzliche Implementierungsoptionen

Das Konzept und die Implementierungsoptionen hinter den Azure-Zielzonen wurden zusammen mit den führenden Microsoft-Partnern erstellt. Dieses Release erkennt das bestehende geistige Eigentum (IP) an, das diese Partner nutzen, um die Einführung der Cloud zu beschleunigen.

| Artikel | Beschreibung |
|---|---|
| [Zielzonen von Partnern](../ready/landing-zone/partner-landing-zone.md) | Prüfen und vergleichen Sie die Angebote Ihres Partners für Azure-Zielzonen. |
| [Optionen für die Implementierung](../ready/landing-zone/implementation-options.md) | Aktualisiert, um Optionen für Partnerzielzonen zu den bestehenden Implementierungsoptionen für Azure-Zielzonen hinzuzufügen. |
| [Referenzimplementierungen auf Unternehmensebene](../ready/enterprise-scale/implementation.md) | Aktualisiert, um eine Hub-and-Spoke-Referenzimplementierung zu Referenzimplementierungen auf Unternehmensebene hinzuzufügen. |

> [!NOTE]
> In den Artikeln über die neue Partnerzielzone wird nicht angegeben, wie ein Partner eine Zielzone definieren oder implementieren soll. Stattdessen soll es einer komplexen Unterhaltung Struktur verleihen, sodass Sie das Angebot des Partners besser verstehen können. Diese Liste von Fragen und minimalen Auswertungskriterien kann auch zum Vergleich von Angeboten potenzieller Partner verwendet werden. Sie wird auch von einigen Partnern genutzt, um den Wert ihrer Implementierungsoptionen für die Azure-Zielzone eindeutiger zu kommunizieren.

## <a name="july-17-2020"></a>17. Juli 2020

Im Rahmen dieses Releases werden einige neue Szenarios hinzugefügt, die die Umsetzung der Cloudeinführung erleichtern.

**Migrationsszenarios:**

Die neue [Übersichtsseite zu Migrationsszenarien](../scenarios/index.md) basiert auf der Methodik für Migrationen, um zu zeigen, wie Azure das #OneMigrate-Versprechen umsetzt. Außerdem stehen Ansätze zur Verfügung, mehrere Szenarios von direkten oder Drittanbietern zu Azure zu migrieren. Dazu gehören drei neue Migrationsszenarios:

| Artikel | BESCHREIBUNG |
|--|--|
| [Windows Virtual Desktop](../scenarios/wvd/index.md) | Es ermöglicht Produktivitätssteigerungen und beschleunigt die Migration verschiedener Workloads, um die Endbenutzererfahrung zu unterstützen. |
| [Azure Stack](../scenarios/azure-stack/index.md) | Hier erhalten Sie Informationen zum Bereitstellen von Azure in Ihrem Rechenzentrum mithilfe von Azure Stack Hub. |

**Analysen im Cloud Adoption Framework:**

Das Microsoft Cloud Adoption Framework umfasst ab sofort auch Analyselösungen. In diesen neuen Themen liegt der Fokus auf den Best Practices für das Umsetzen von Analyselösungen während der Cloudeinführung.

| Artikel | BESCHREIBUNG |
|--|--|
| [Analytics-Lösungen](../migrate/azure-best-practices/analytics/analytics-solutions-overview.md) | In diesem Artikel erhalten Sie Informationen zur Migration von lokalen Legacyumgebungen einschließlich Teradata, Netezza und Exadata zur Modernisierung von Analyselösungen. |
| [Hochverfügbarkeit für Azure Synapse Analytics](../migrate/azure-best-practices/analytics/azure-synapse.md) | Hier erhalten Sie Informationen zu einem der wichtigsten Vorteile einer modernen, cloudbasierten Infrastruktur, der integrierten Hochverfügbarkeit und Notfallwiederherstellung. |
| [Datendefinitionssprachen (DDLs) für die Schemamigration](../migrate/azure-best-practices/analytics/schema-migration-ddl.md) | Hier erhalten Sie Informationen zu den Datenbankobjekten und zugehörigen Prozessen bei der Vorbereitung einer Migration vorhandener Daten. |

**Künstliche Intelligenz (KI) im Cloud Adoption Framework:**

KI-Lösungen und Best Practices sind ab sofort im Microsoft Cloud Adoption Framework integriert. Diese KI-Lösungen unterstützen Sie bei der Beschleunigung von Innovationen mithilfe von Vorhersagen zu den Anforderungen von Kunden. Außerdem können Geschäftsprozesse automatisiert, Informationen erhoben und neue Möglichkeiten für die Kundenbindung erschlossen werden. Zudem kann die Servicequalität insgesamt während der Cloudeinführung verbessert werden.

| Artikel | BESCHREIBUNG |
|--|--|
| [Verantwortungsbewusste künstliche Intelligenz](../strategy/responsible-ai.md) | Hier erhalten Sie Informationen zu KI-Prinzipien, die bei der Implementierung von KI-Lösungen berücksichtigt werden sollten. Außerdem erfahren Sie, wie Sie eine Strategie für verantwortungsbewusste künstliche Intelligenz etablieren. |
| [Azure-Innovationsleitfaden: Innovationen mit KI](../innovate/innovation-guide/predict.md) | Hier erhalten Sie Informationen zu Innovationen mit KI. Außerdem finden Sie die für Ihre Implementierungsanforderungen am besten geeigneten Lösungen. |
| [Künstliche Intelligenz (KI) im Cloud Adoption Framework](../innovate/ai/index.md) | Das Cloud Adoption Framework ist ein präskriptives Framework, das die Tools, Programme und Inhalte (Best Practices, Konfigurationsvorlagen und Architekturleitfäden) bietet, mit denen Sie die Einführung von KI und cloudnativen Methoden im großen Stil vereinfachen können. |
| [MLOps mit Azure Machine Learning](../manage/mlops-machine-learning.md) | Hier erhalten Sie Informationen zu Best Practices zu MLOps mit Azure Machine Learning. |
| [Innovationen mit KI](../innovate/best-practices/predict.md) | Hier erhalten Sie Informationen zu KI-Lösungen (Machine Learning, KI-Anwendungen und -Agents, Wissensgewinnung) und zu Best Practices, die digitale Erfindungen beschleunigen können. |

## <a name="june-15-2020"></a>15. Juni 2020

Die ordnungsgemäße Konfiguration der Cloudumgebung ist häufig das erste und gängigste technische Hindernis während der Cloudeinführung. Der Schwerpunkt dieser Veröffentlichung liegt im Wesentlichen auf Anleitungen, mit denen Sie Bereitstellung von Cloudumgebungen beschleunigen können. Zur Überwindung dieses gängigen Hindernisses werden im Cloud Adoption Framework **Azure-Zielzonen** eingeführt.

| Artikel | BESCHREIBUNG |
|--|--|
| [Azure-Zielzonen](../ready/landing-zone/index.md) | Azure-Zielzonen erstellen eine gängige Gruppe von Entwurfsbereichen und Implementierungsoptionen, mit denen das Erstellen von Umgebungen gemäß dem Cloudeinführungsplan und dem Cloudbetriebsmodell beschleunigt wird. In diesem neuen Artikel werden Azure-Zielzonen eindeutiger erläutert. |
| [Azure-Zielzonen: Entwurfsbereiche](../ready/landing-zone/design-areas.md) | Alle Azure-Zielzonen haben eine gemeinsame Gruppe von acht Entwurfsbereichen. Vor dem Bereitstellen einer der Azure-Zielzonen sollten Kunden beim Treffen wichtiger Entscheidungen jeden dieser Entwürfe untersuchen. |
| [Azure-Zielzonen: Optionen für die Implementierung](../ready/landing-zone/implementation-options.md) | Wählen Sie die beste Implementierungsoption für Azure-Zielzonen aus, je nach Ihrem Cloudeinführungsplan und dem Cloudbetriebsmodell. |

Die vorhandenen CAF-Blaupausendefinitionen und CAF-Terraform-Module bieten Ihnen einen Ausgangspunkt für die Implementierung von Azure-Zielzonen. Einige Kunden benötigen jedoch eine umfassendere Implementierungsoption, die den Anforderungen von Cloudeinführungsplänen auf Unternehmensebene gerecht wird. In dieser Version wird den Implementierungsoptionen für Azure-Zielzonen die Option für **CAF-Zielzonen auf Unternehmensebene** hinzugefügt, um diese Anforderung zu erfüllen. Im Folgenden sind einige Artikel aufgelistet, die Ihnen den Einstieg in die Arbeit mit der CAF-Architektur auf Unternehmensebene und mit Referenzimplementierungen erleichtern.

| Artikel | BESCHREIBUNG |
|--|--|
| [Übersicht zur Unternehmensebene](../ready/enterprise-scale/index.md) | Übersicht über die Skalierung auf Unternehmensebene |
| [Implementieren von CAF-Zielzonen auf Unternehmensebene](../ready/enterprise-scale/implementation.md) | Schnelle Implementierungsoptionen und GitHub-Beispiele |
| [Architektur auf Unternehmensebene](../ready/enterprise-scale/architecture.md) | Verstehen der Architektur hinter der Unternehmensebene |
| [Entwurfsprinzipien für die Unternehmensebene](../ready/enterprise-scale/design-principles.md) | Erfahren Sie mehr über architekturbezogene Entwurfsprinzipien, an denen sich Entscheidungen während der Implementierung orientieren, um zu bewerten, ob dieser Ansatz für Ihr Cloudbetriebsmodell geeignet ist. |
| [Entwurfsrichtlinie für die Unternehmensebene](../ready/enterprise-scale/design-guidelines.md) | Bewerten Sie die Richtlinien für die Unternehmensebene, ob diese den gängigen Entwurfsbereichen von Azure-Zielzonen gerecht werden. |
| [Implementierungsrichtlinien](../ready/enterprise-scale/implementation-guidelines.md) | Untersuchen Sie die Aktivitäten, die vor dem Bereitstellen für eine Implementierung auf Unternehmensebene erforderlich sind. |

Partner sind ein wichtiger Aspekt der erfolgreichen Cloudeinführung. Im Verlauf der gesamten Anleitung zum Cloud Adoption Framework haben wir Referenzen hinzugefügt, die verdeutlichen, welche wichtige Rolle diese Partner spielen und wie Kunden Partner besser einbinden können. Eine Liste der validierten CAF-Partner finden Sie unter den [Angeboten CAF-orientierter Partner](https://aka.ms/adopt/partneroffers) sowie unter [Azure Expert Managed Service Provider (MSPs)](https://www.microsoft.com/azure/partners/azureexpertmsp?filters=all) und [Advanced Specialist-Partner](https://www.microsoft.com/azure/partners/advspec).

## <a name="may-15-2020"></a>15. Mai 2020

Basierend auf Feedback haben wir neue Inhalte erstellt, um Ihnen den Einstieg in die Verwendung des Cloud Adoption Frameworks zu erleichtern. Die neuen Leitfäden zu den ersten Schritten helfen Ihnen, im Framework basierend auf den gewünschten Zielvorgaben zu navigieren. Wir haben auch eine neue Angebotsseite erstellt, um Ihnen das Auffinden von Anleitungen, Tools, Lernmodulen und Programmen zu erleichtern, die eine erfolgreiche Cloudeinführungsjourney unterstützen.

| Artikel | BESCHREIBUNG |
|--|--|
| [Cloud Adoption Framework für Azure](../index.yml) | Die Angebotsseite für das Cloud Adoption Framework wurde umgestaltet, um Ihnen das Auffinden von Anleitungen, Tools, Lernmodulen und Programmen zu erleichtern, die eine erfolgreiche Cloudeinführungsjourney unterstützen. |
| [Erste Schritte mit dem Cloud Adoption Framework](./index.md) | Wählen Sie einen Leitfaden mit ersten Schritten aus, der für Ihre Cloudeinführungsziele geeignet ist. Diese gängigen Szenarien bieten eine Roadmap für das Microsoft Cloud Adoption Framework für Azure. |
| [Verstehen und Dokumentieren grundlegender Ausrichtungsentscheidungen](./cloud-concepts.md) | Informieren Sie sich über die anfänglichen Entscheidungen, die von jedem Teammitglied verstanden werden sollten, das an der Cloudeinführung beteiligt ist. |
| [Grundlegendes zur Portfoliohierarchie und deren Ausrichtung](../reference/fundamental-concepts/hosting-hierarchy.md) | Erfahren Sie, wie eine Portfoliohierarchie zeigt, wie Ihre Workloads und die unterstützenden Dienste zusammenpassen. |
| [Wie unterstützen die Azure-Produkte die Portfoliohierarchie?](../reference/fundamental-concepts/hierarchy-azure-tools.md) | Erfahren Sie mehr über die Azure-Tools und -Lösungen, die Ihre Portfoliohierarchie unterstützen. |
| [Verwalten der Organisationsausrichtung](../organize/index.md) | Richten Sie gut ausgestattete Organisationsstrukturen ein, die ein effektives Betriebsmodell für die Cloud sind. |

## <a name="april-14-2020"></a>14. April 2020

Wir haben alle Tools und Vorlagen für die Cloudeinführung an einem Ort zusammengeführt, damit sie leichter zu finden sind.

| Artikel | BESCHREIBUNG |
|--|--|
| [Tools und Vorlagen](../reference/tools-templates.md) | Hier finden Sie die Tools, Vorlagen und Bewertungen, mit deren Hilfe Sie die Cloudeinführung beschleunigen können. |

## <a name="april-4-2020"></a>4\. April 2020

Weitere Iteration der Verfeinerung von Migrationsmethodik und Bereitschaftsmethodik, um das Feedback von Microsoft-Kunden und -Partnern und internen Microsoft-Programmen stärker zu berücksichtigen.

**Updates zur Migrationsmethodik:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Migrationsmethodik](../migrate/index.md) | Diese Änderungen rationalisieren die Phasen des Migrationsaufwands (Bewertung, Bereitstellung und Freigabe der Workloads). Durch die Änderungen werden auch die Details bezüglich des Backlogs der Migration beseitigt. Das Entfernen dieser Details und der Verweis auf die Methoden „Plan“, „Ready“ und „Adopt“ (Planen, Vorbereiten und Einführen) schafft stattdessen Flexibilität für verschiedene Cloudeinführungsprogramme, um diese besser auf die Methodik abzustimmen. |

**Updates zur Bereitschaftsmethodik:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Umgestalten von Zielzonen](../ready/landing-zone/refactor.md) | **Neuer Artikel:** Ausgehend von Workshops zur Bereitschaftsmethodik veranschaulicht dieser Artikel die Theorie, mit einer anfänglichen Vorlage zu beginnen, Entscheidungsstrukturen und Refactoring zu nutzen, um die Zielzone zu erweitern, und sich auf einen zukünftigen Zustand der Unternehmensbereitschaft zuzubewegen. |
| [Erweitern der Zielzone](../ready/considerations/index.md) | **Neuer Artikel:** Baut auf dem Abschnitt über parallele Iterationen des Artikels zum Refactoring auf, um zu zeigen, wie verschiedene Arten von Zielzonenerweiterungen gemeinsame Prinzipien in die unterstützende Plattform einbetten würden. Der ursprüngliche Inhalt für diese Übersicht wurde in den Knoten [Grundlegende Überlegungen zu Zielzonen](../ready/considerations/basic-considerations.md) im Inhaltsverzeichnis verschoben. |
| [Testgesteuerte Entwicklung (TDD) für Zielzonen](../ready/considerations/test-driven-development.md) | **Neuer Artikel:** Der Refactoringansatz wird durch die Einführung eines testgesteuerten Entwicklungszyklus, der die Entwicklung der Zielzone und das Refactoring steuert, erheblich verbessert. |
| [Testgesteuerte Entwicklung (TDD) der Zielzone in Azure](../ready/considerations/azure-test-driven-development.md) | **Neuer Artikel:** Azure Governance-Tools bieten eine vielfältige Plattform für TDD-Zyklen oder Rot/Grün-Tests. |
| [Erhöhen der Sicherheit von Zielzonen](../ready/considerations/landing-zone-security.md) | **Neuer Artikel:** Übersicht über die bewährten Methoden in diesem Abschnitt, mit einem Rückbezug auf den TDD-Zyklus |
| [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-operations.md) | **Neuer Artikel:** Liste der bewährten Methoden in der „Manage“-Methodik, mit einem Übergang zu diesem modularen Ansatz zur Verbesserung von Betrieb, Zuverlässigkeit und Leistung. |
| [Verbessern der Governance von Zielzonen](../ready/considerations/landing-zone-governance.md) | **Neuer Artikel:** Liste der bewährten Methoden in der „Govern“-Methodik, mit einem Übergang zu diesem modularen Ansatz zur Verbesserung von Governance, Cost Management und Skalierung. |
| [Auf Unternehmensniveau beginnen](../ready/enterprise-scale/index.md) | **Neuer Artikel:** Veranschaulichen Sie einen Ansatz, der die Unterschiede im Prozess aufzeigt, wenn ein Kunde mit CAF-Zielzonenvorlagen auf Unternehmensniveau beginnt. Dieser Artikel hilft Kunden dabei, die Qualifizierer zu verstehen, die diese Entscheidung unterstützen würden. |

## <a name="march-27-2020"></a>27. März 2020

Wir haben einen Leitfaden zu den anfänglichen Abonnements hinzugefügt, die Sie bei der Einführung von Azure erstellen sollten.

**Updates zum Abonnementleitfaden:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Erstellen Ihrer anfänglichen Azure-Abonnements](../ready/azure-best-practices/initial-subscriptions.md) | **Neuer Artikel:** Erstellen Sie Ihre anfänglichen Produktions- und Nichtproduktionsabonnements, und entscheiden Sie, ob Sie Sandboxabonnements sowie ein Abonnement für gemeinsame Dienste erstellen. |
| [Erstellen zusätzlicher Abonnements zum Skalieren Ihrer Azure-Umgebung](../ready/azure-best-practices/scale-subscriptions.md) | Hier erfahren Sie mehr über die Gründe für das Erstellen zusätzlicher Abonnements sowie das Verschieben von Ressourcen zwischen Abonnements, und Sie erhalten Tipps zum Erstellen neuer Abonnements. |
| [Organisieren und Verwalten mehrerer Azure-Abonnements](../ready/azure-best-practices/organize-subscriptions.md) | Erstellen Sie eine Verwaltungsgruppenhierarchie, um Ihre Azure-Abonnements zu organisieren, zu verwalten und zu steuern. |

## <a name="march-20-2020"></a>20. März 2020

Wir haben eine ausführliche Anleitung hinzugefügt, in der die Tools, Programme und Inhalte nach Rollen kategorisiert sind, um die erfolgreiche Bereitstellung von Anwendungen in Kubernetes zu fördern – von der Proof of Concept-Phase bis zur Produktion, gefolgt von Skalierung und Optimierung.

**Kubernetes:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Anwendungsentwicklung und Bereitstellung](../innovate/kubernetes/application-development.md) | **Neuer Artikel:** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Planung der Anwendungsentwicklung, die Konfiguration von CI/CD-Pipelines und die Implementierung von Websitezuverlässigkeits-Engineering (Site Reliability Engineering) für Kubernetes. |
| [Clusterentwurf und Vorgänge](../innovate/kubernetes/cluster-design-operations.md) | **Neuer Artikel:** Enthält Prüflisten, Ressourcen und bewährte Methoden für Clusterkonfiguration, Netzwerkentwurf, zukunftssichere Skalierbarkeit, Geschäftskontinuität und Notfallwiederherstellung für Kubernetes. |
| [Cluster- und Anwendungssicherheit](../innovate/kubernetes/cluster-application-security.md) | **Neuer Artikel:** Enthält Prüflisten, Ressourcen und bewährte Methoden für die Kubernetes-Sicherheit, -Planung, -Produktion und -Skalierung. |

## <a name="march-2-2020"></a>2\. März 2020

<!-- docutune:casing "Strategy, Plan, Ready, and Migrate" -->

Als Reaktion auf das erhaltene Feedback zur Kontinuität des Migrationsansatzes in mehreren Abschnitten des Frameworks für die Cloudeinführung, z. B. Strategie, Plan, Bereitschaft und Migration, haben wir die folgenden Aktualisierungen vorgenommen. Diese Aktualisierungen sind so konzipiert, dass Sie die Planungs- und Einführungsverbesserungen während einer Migrationsjourney leichter verstehen.

**Updates zur Strategiemethodik:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Ausgewogenheit des Portfolios](../strategy/balance-the-portfolio.md) | Dieser Artikel wurde verschoben, damit er zu einem früheren Zeitpunkt der Strategiemethodik erscheint. So erhalten Sie an einem früheren Punkt des Lebenszyklus Einblick in den Denkprozess. |
| [Abstimmen&nbsp;konkurrierender&nbsp;Prioritäten](../strategy/balance-competing-priorities.md) | **Neuer Artikel:** Es wird beschrieben, wie Sie Prioritäten für Methodiken so abstimmen, dass dies Ihrer Strategie nützt. |

**Updates zur Planmethodik:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Bewährte Methoden&nbsp;für&nbsp;Bewertungen](../plan/contoso-migration-assessment.md) | Dieser Artikel wurde in den neuen Abschnitt „Bewährte Methoden“ der Planmethodik verschoben. So erhalten Sie zu einem früheren Zeitpunkt des Lebenszyklus Einblick in die Bewertung von lokalen Umgebungen. |

**Updates zur Bereitschaftsmethodik:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Was&nbsp;ist&nbsp;eine&nbsp;Zielzone?&nbsp;](../ready/landing-zone/index.md) | **Neuer Artikel:** Enthält eine Definition des Begriffs „Zielzone“. |
| Erste Landezone | **Neuer Artikel:** Enthält weitere Informationen zum Vergleich verschiedener Zielzonen. |
| [Zielzone für CAF-Migration](../ready/landing-zone/migrate-landing-zone.md) | Hiermit wurde die Blaupausendefinition von der Auswahl der ersten Zielzone getrennt. |
| [CAF-Terraform-Module](../ready/landing-zone/terraform-landing-zone.md) | Wurde in den neuen Abschnitt „Zielzone“ der Bereitschaftsmethodik verschoben, um Terraform in Bezug auf Zielzonen als wichtigere Komponente darzustellen. |

**Updates zur Migrationsmethodik:**

| Artikel | BESCHREIBUNG |
|--|--|
| [Übersicht](../migrate/azure-migration-guide/index.md) | Diese Aktualisierung umfasst eine eindeutigere Beschreibung des Leitfadens und eine Verringerung der Schritte. |
| [Bewerten](../migrate/azure-migration-guide/assess.md) | Der Abschnitt „Hinterfragen der Annahmen“ wurde hinzugefügt, um zu verdeutlichen, wie diese Bewertungsebene zum Ansatz zur inkrementellen Bewertung passt, der in der Planmethodik beschrieben ist. |
| [Klassifizierung bei Bewertungsprozessen](../migrate/migration-considerations/assess/classify.md) | **Neuer Artikel:** Enthält eine Beschreibung der Klassifizierung jeder Ressource und Workload vor der Migration. |
| [Migrieren](../migrate/azure-migration-guide/migrate.md) | Als Reaktion auf Feedback bei Tier 1-Konferenzen wurde den Drittanbieter-Tooloptionen ein Verweis auf UnifyCloud hinzugefügt. |
| [Testen,&nbsp;Optimieren&nbsp;und&nbsp;Höherstufen](../migrate/azure-migration-guide/optimize-and-transform.md) | Der Titel dieses Artikels wurde an andere Vorschläge zur Prozessverbesserung angepasst. |
| [Übersicht über die Bewertung](../migrate/migration-considerations/assess/index.md) | Es wurde eine Aktualisierung durchgeführt, um besser darzustellen, dass es bei der Bewertung in dieser Phase um die Bewertung der technischen Eignung einer bestimmten Workload und die zugehörigen Ressourcen geht. |
| [Checkliste für die Planung](../migrate/migration-considerations/prerequisites/planning-checklist.md) | Aktualisierung zur Verdeutlichung der Wichtigkeit einer Vorgangsausrichtung während der Planung von Migrationsmaßnahmen, um nach der Migration eine gut verwaltete Workload zu erhalten. |

<!-- docutune:ignoreNextStep -->
