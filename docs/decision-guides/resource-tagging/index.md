---
title: Leitfaden zur Entscheidungsfindung für Ressourcenbenennung und -markierung
description: Hier erfahren Sie mehr über Ansätze und Optionen für Benennung und Tags, wenn Sie cloudbasierte Ressourcen im Rahmen des Frameworks für die Cloudeinführung (Cloud Adoption Framework) für Azure organisieren.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: f9ca594839cbd1e5d5ff641c81b083d30cd4481b
ms.sourcegitcommit: 670dd77efe02ed20275732248e0fa2aae2196805
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2020
ms.locfileid: "91620837"
---
# <a name="resource-naming-and-tagging-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Ressourcenbenennung und -markierung

Die Organisation cloudbasierter Ressourcen ist eine wichtige Aufgabe für die IT-Abteilung, sofern Sie nicht nur über einfache Bereitstellungen verfügen. Aus den folgenden Gründen sollten Sie Benennungs- und Taggingstandards zum Organisieren Ihrer Ressourcen verwenden:

- **Ressourcenverwaltung:** Ihre IT-Teams müssen Ressourcen, die bestimmten Workloads, Umgebungen, Besitzergruppen oder anderen wichtigen Informationen zugeordnet sind, schnell finden können. Die Organisation von Ressourcen ist wichtig für die Zuweisung organisatorischer Rollen und Zugriffsberechtigungen für die Ressourcenverwaltung.
- **Kostenmanagement und -optimierung:** Um Unternehmensgruppen auf den Verbrauch von Cloudressourcen aufmerksam zu machen, muss die IT-Abteilung verstehen, welche Ressourcen und Workloads die einzelnen Teams verwenden. In den folgenden Themen werden kostenbezogene Tags verwendet:

  - [Cloudbuchhaltungsmodelle](../../strategy/cloud-accounting.md)
  - [ROI-Berechnungen](../../strategy/financial-models.md#return-on-investment)
  - [Nachverfolgung der Kosten](../../ready/azure-best-practices/track-costs.md)
  - [Budgets](/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Warnungen](/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Nachverfolgung und Berichterstellung für wiederkehrende Ausgaben](../../govern/cost-management/compliance-processes.md)
  - [Optimierungen nach der Implementierung](../../govern/cost-management/discipline-improvement.md#operate-and-post-implementation)
  - [Taktiken zur Kostenoptimierung](../../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-best-practices)
- **Operatives Management:** Die Transparenz von geschäftlichen Verpflichtungen und Vereinbarungen zum Servicelevel (Service Level Agreement, SLA) für das operative Managementteam ist ein wichtiger Aspekt des laufenden Betriebs. Für eine gute Verwaltung ist die Verwendung von Tags für die [Kritikalität für das Unternehmen](../../manage/considerations/criticality.md) unabdingbar.
- **Sicherheit**: Die Klassifizierung von Daten und der Auswirkungen auf die Sicherheit ist ein wichtiger Datenpunkt für das Team, wenn Sicherheitsverletzungen oder andere Sicherheitsprobleme auftreten. Für einen sicheren Betrieb ist die Verwendung von Tags für die [Datenklassifizierung](../../govern/policy-compliance/data-classification.md) erforderlich.
- **Governance und Einhaltung gesetzlicher Bestimmungen:** Die Aufrechthaltung der Konsistenz zwischen Ressourcen hilft Ihnen, Abweichungen von vereinbarten Richtlinien zu erkennen. In diesem [Artikel zur Grundlage für die Governance](../../govern/guides/complex/prescriptive-guidance.md#resource-tagging) wird gezeigt, wie eines der unten beschriebenen Muster bei der Bereitstellung von Governancemethoden helfen kann. Ähnliche Muster sind zum Auswerten der Einhaltung gesetzlicher Bestimmungen mithilfe von Tags verfügbar.
- **Automatisierung:** Neben einer Vereinfachung der Ressourcenverwaltung für die IT-Abteilung ermöglicht Ihnen ein angemessenes Organisationsschema die Nutzung der Automatisierung im Rahmen der Ressourcenerstellung, der Betriebsüberwachung und der Erstellung von DevOps-Prozessen.
- **Workloadoptimierung:** Mithilfe von Tags lassen sich Muster identifizieren und allgemeine Probleme beheben. Ein Tag kann auch dabei helfen, die zur Unterstützung einer einzelnen Workload erforderlichen Ressourcen zu identifizieren. Das Tagging aller zugeordneten Ressourcen jeder Workload ermöglicht genauere Analysen Ihrer unternehmenskritischen Workloads und somit fundierte architekturbezogene Entscheidungen.

## <a name="tagging-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Markierungen

![Abbildung der Taggingoptionen mit zunehmender Komplexität entsprechend den nachstehenden weiterführenden Links](../../_images/decision-guides/decision-guide-resource-tagging.png)

Wechseln Sie zu: [Baselinenamenskonventionen](#baseline-naming-conventions) | [Ressourcenmarkierungsmuster](#resource-tagging-patterns) | [Weitere Informationen](#learn-more)

Ihr Markierungsansatz kann einfach oder komplex sein, wobei der Schwerpunkt von der Unterstützung der IT-Teams, die die Cloudworkloads verwalten, bis zur Integration von Informationen zu sämtlichen Aspekten des Unternehmen reichen kann.

Ein IT-orientierter Fokus für die Verwendung von Tags (etwa Tags auf der Grundlage von Workload, Anwendung, Funktion oder Umgebung) vereinfacht sowohl die Überwachung von Ressourcen als auch Entscheidungen auf der Grundlage operativer Anforderungen.

Bei Markierungsschemas mit geschäftlichem Fokus (beispielsweise Buchhaltung, Unternehmensbesitz oder geschäftliche Bedeutung) muss unter Umständen mehr Zeit in die Erstellung von Markierungsstandards investiert werden, die die Geschäftsinteressen widerspiegeln und diese Standards langfristig bewahren. Mit dieser Investition wird ein Markierungssystem erzielt, das eine verbesserte Nachverfolgbarkeit für die Kosten und den Wert der IT-Ressourcen für das gesamte Unternehmen bietet. Diese Verknüpfung des geschäftlichen Werts einer Ressource mit den Betriebskosten ist einer der ersten Schritte, um die Wahrnehmung der IT als Kostenfaktor in Ihrer Organisation zu verändern.

## <a name="baseline-naming-conventions"></a>Baselinenamenskonventionen

Eine standardisierte Namenskonvention ist der Ausgangspunkt für die Organisation Ihrer in der Cloud gehosteten Ressourcen. Mit einem ordnungsgemäß strukturierten Benennungssystem können Sie Ressourcen sowohl zu Verwaltungs- als auch zu Abrechnungszwecken schnell identifizieren. Wenn in anderen Teilen Ihrer Organisation bereits IT-Namenskonventionen vorhanden sind, wägen Sie ab, ob Sie Ihre Namenskonventionen für die Cloud darauf abstimmen oder separate cloudbasierte Standards einrichten möchten.

> [!NOTE]
> [Benennungsregeln und -einschränkungen](/azure/azure-resource-manager/management/resource-name-rules) unterscheiden sich je nach Azure-Ressource. Ihre Namenskonventionen müssen diesen Regeln entsprechen.

## <a name="resource-tagging-patterns"></a>Ressourcenmarkierungsmuster

Für eine komplexere Organisation als eine konsistente Namenskonvention bereitstellen kann, unterstützen Cloudplattformen die Möglichkeit zum Markieren von Ressourcen.

Tags sind Metadatenelemente, die an Ressourcen angefügt werden. Markierungen bestehen aus Paaren aus Schlüssel-Wert-Zeichenfolgen. Welche Werte Sie in diese Paare einschließen, bleibt Ihnen überlassen, aber die Anwendung einer konsistenten Menge globaler Markierungen im Rahmen einer umfassenden Benennungs- und Markierungsrichtlinie ist ein wesentlicher Bestandteil einer allgemein gültigen Governancerichtlinie.

Verwenden Sie im Rahmen Ihres Planungsprozesses die folgenden Fragen, um festzustellen, welche Art von Informationen Ihre Ressourcentags unterstützen müssen:

- Müssen Ihre Benennungs- und Markierungsrichtlinien in vorhandene Benennungs- und Organisationsrichtlinien innerhalb Ihres Unternehmens integriert werden?
- Werden Sie ein Abrechnungssystem mit verbrauchsbasierter Kostenzuteilung implementieren? Müssen Sie Ressourcen zu Buchhaltungsinformationen für Abteilungen, Geschäftsbereiche und Teams zuordnen, die über eine einfache Aufschlüsselung auf der Abonnementebene hinausgehen?
- Muss die Markierung Details wie Anforderungen zur Einhaltung gesetzlicher Bestimmungen für eine Ressource darstellen? Wie sieht es mit betriebsbezogenen Details wie Anforderungen an die Betriebszeiten, Zeitpläne für Patches oder Sicherheitsanforderungen aus?
- Welche Tags sind für alle Ressourcen basierend auf der zentralisierten IT-Richtlinie erforderlich? Welche Tags werden optional sein? Dürfen einzelne Teams eigene benutzerdefinierte Markierungsschemas implementieren?

Die unten aufgeführten allgemeinen Markierungsmuster zeigen beispielhaft, wie das Markieren zum Organisieren von Cloudressourcen verwendet werden kann. Diese Muster sind nicht als exklusiv gedacht und können parallel verwendet werden, wodurch sich mehrere Möglichkeiten der Organisation von Ressourcen auf der Grundlage der Anforderungen Ihres Unternehmens ergeben.

<!-- cSpell:ignore catalogsearch northamerica jsmith contactalias catsearchowners businessprocess businessimpact revenueimpact -->

| Markierungstyp | Beispiele | BESCHREIBUNG |
|--|--|--|
| Funktionen | `app` = `catalogsearch1` <br> `tier` = `web` <br> `webserver` = `apache` <br> `env` = `prod` <br> `env` = `staging` <br> `env` = `dev` | Kategorisieren Sie Ressourcen in Bezug auf ihren Zweck innerhalb einer Workload, auf die Umgebung, in der sie bereitgestellt werden, oder auf andere funktionsbezogene oder operative Details. |
| Klassifizierung | `confidentiality` = `private` <br> `SLA` = `24hours` | Klassifiziert eine Ressource danach, wie sie verwendet wird und welche Richtlinien für sie gelten. |
| Buchhaltung | `department` = `finance` <br> `program` = `business-initiative` <br> `region` = `northamerica` | Ermöglicht die Zuordnung einer Ressource zu bestimmten Gruppen innerhalb einer Organisation zu Abrechnungszwecken. |
| Partnerschaft | `owner` = `jsmith` <br> `contactalias` = `catsearchowners` <br> `stakeholders` = `user1;user2;user3` | Enthält Informationen dazu, welche Personen (außerhalb der IT) mit der Ressource verknüpft oder in anderer Form von ihr betroffen sind. |
| Zweck | `businessprocess` = `support` <br> `businessimpact` = `moderate` <br> `revenueimpact` = `high` | Richtet Ressourcen an Geschäftsfunktionen aus, um Investitionsentscheidungen besser zu unterstützen. |

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zur Benennung und Markierung in Azure finden Sie unter:

- [Namenskonventionen für Azure-Ressourcen](../../ready/azure-best-practices/naming-and-tagging.md). In dieser Anleitung finden Sie empfohlene Benennungskonventionen für Azure-Ressourcen.
- [Verwenden von Tags zum Organisieren von Azure-Ressourcen und Verwaltungshierarchie](/azure/azure-resource-manager/management/tag-resources). Sie können Tags in Azure sowohl auf der Ressourcengruppenebene als auch auf der Ebene einzelner Ressourcen anwenden. So können Sie Abrechnungsberichte anhand der angewendeten Markierungen unterschiedlich detailliert gestalten.

## <a name="next-steps"></a>Nächste Schritte

„Ressourcenmarkierung“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die Übersicht über Leitfäden zur architekturbezogenen Entscheidungsfindung, um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
