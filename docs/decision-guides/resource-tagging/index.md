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
ms.openlocfilehash: 638f8dad1d7f284104765b28fe53561d98e02b56
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83399815"
---
<!-- cSpell:ignore catalogsearch northamerica jsmith contactalias catsearchowners businessprocess businessimpact revenueimpact -->

# <a name="resource-naming-and-tagging-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Ressourcenbenennung und -markierung

Die Organisation cloudbasierter Ressourcen ist eine wichtige Aufgabe für die IT-Abteilung, sofern Sie nicht nur über einfache Bereitstellungen verfügen. Aus den folgenden Gründen sollten Sie Benennungs- und Taggingstandards zum Organisieren Ihrer Ressourcen verwenden:

- **Ressourcenverwaltung:** Ihre IT-Teams müssen Ressourcen, die bestimmten Workloads, Umgebungen, Besitzergruppen oder anderen wichtigen Informationen zugeordnet sind, schnell finden können. Die Organisation von Ressourcen ist wichtig für die Zuweisung organisatorischer Rollen und Zugriffsberechtigungen für die Ressourcenverwaltung.
- **Kostenmanagement und -optimierung:** Um Unternehmensgruppen auf den Verbrauch von Cloudressourcen aufmerksam zu machen, muss die IT-Abteilung verstehen, welche Ressourcen und Workloads die einzelnen Teams verwenden. In den folgenden Themen werden kostenbezogene Tags verwendet:

  - [Cloudbuchhaltungsmodelle](../../strategy/cloud-accounting.md)
  - [ROI-Berechnungen](../../strategy/financial-models.md#return-on-investment)
  - [Nachverfolgung der Kosten](../../ready/azure-best-practices/track-costs.md)
  - [Budgets](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Warnungen](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Nachverfolgung und Berichterstellung für wiederkehrende Ausgaben](../../govern/cost-management/compliance-processes.md)
  - [Optimierungen nach der Implementierung](../../govern/cost-management/discipline-improvement.md#operate-and-post-implementation)
  - [Taktiken zur Kostenoptimierung](../../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)
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

Bei Markierungsschemas mit geschäftlichem Fokus (beispielsweise Buchhaltung, Unternehmensbesitz oder geschäftliche Bedeutung) muss unter Umständen mehr Zeit in die Erstellung von Markierungsstandards investiert werden, die die Geschäftsinteressen widerspiegeln und diese Standards langfristig bewahren. Allerdings ist das Ergebnis dieses Prozesses ein Markierungssystem, das eine verbesserte Erfassung der Kosten und des Werts von IT-Ressourcen für das gesamte Unternehmen bietet. Diese Verknüpfung des geschäftlichen Werts einer Ressource mit den Betriebskosten ist einer der ersten Schritte, um die Wahrnehmung der IT als Kostenfaktor in Ihrer Organisation zu verändern.

## <a name="baseline-naming-conventions"></a>Baselinenamenskonventionen

Eine standardisierte Namenskonvention ist der Ausgangspunkt für die Organisation Ihrer in der Cloud gehosteten Ressourcen. Mit einem ordnungsgemäß strukturierten Benennungssystem können Sie Ressourcen sowohl zu Verwaltungs- als auch zu Abrechnungszwecken schnell identifizieren. Wenn in anderen Teilen Ihrer Organisation bereits IT-Namenskonventionen vorhanden sind, wägen Sie ab, ob Sie Ihre Namenskonventionen für die Cloud darauf abstimmen oder separate cloudbasierte Standards einrichten möchten.

> [!NOTE]
> [Benennungsregeln und -einschränkungen](https://docs.microsoft.com/azure/azure-resource-manager/management/resource-name-rules) unterscheiden sich je nach Azure-Ressource. Ihre Namenskonventionen müssen diesen Regeln entsprechen.

## <a name="resource-tagging-patterns"></a>Ressourcenmarkierungsmuster

Für eine komplexere Organisation als eine konsistente Namenskonvention bereitstellen kann, unterstützen Cloudplattformen die Möglichkeit zum Markieren von Ressourcen.

Tags sind Metadatenelemente, die an Ressourcen angefügt werden. Markierungen bestehen aus Paaren aus Schlüssel-Wert-Zeichenfolgen. Welche Werte Sie in diese Paare einschließen, bleibt Ihnen überlassen, aber die Anwendung einer konsistenten Menge globaler Markierungen im Rahmen einer umfassenden Benennungs- und Markierungsrichtlinie ist ein wesentlicher Bestandteil einer allgemein gültigen Governancerichtlinie.

Verwenden Sie im Rahmen Ihres Planungsprozesses die folgenden Fragen, um festzustellen, welche Art von Informationen Ihre Ressourcentags unterstützen müssen:

- Müssen Ihre Benennungs- und Markierungsrichtlinien in vorhandene Benennungs- und Organisationsrichtlinien innerhalb Ihres Unternehmens integriert werden?
- Werden Sie ein Abrechnungssystem mit verbrauchsbasierter Kostenzuteilung implementieren? Müssen Sie Ressourcen zu Buchhaltungsinformationen für Abteilungen, Geschäftsbereiche und Teams zuordnen, die über eine einfache Aufschlüsselung auf der Abonnementebene hinausgehen?
- Muss die Markierung Details wie Anforderungen zur Einhaltung gesetzlicher Bestimmungen für eine Ressource darstellen? Wie sieht es mit betriebsbezogenen Details wie Anforderungen an die Betriebszeiten, Zeitpläne für Patches oder Sicherheitsanforderungen aus?
- Welche Tags sind für alle Ressourcen basierend auf der zentralen IT-Richtlinie erforderlich? Welche Tags werden optional sein? Dürfen einzelne Teams eigene benutzerdefinierte Markierungsschemas implementieren?

Die unten aufgeführten allgemeinen Markierungsmuster zeigen beispielhaft, wie das Markieren zum Organisieren von Cloudressourcen verwendet werden kann. Diese Muster sind nicht als exklusiv gedacht und können parallel verwendet werden, wodurch sich mehrere Möglichkeiten der Organisation von Ressourcen auf der Grundlage der Anforderungen Ihres Unternehmens ergeben.

<!-- markdownlint-disable MD033 -->
<!-- docsTest:disable -->

| Markierungstyp | Beispiele | BESCHREIBUNG |
|-----|-----|-----|
| Funktionen | app&nbsp;=&nbsp;catalogsearch1 <br> tier&nbsp;=&nbsp;web <br> webserver&nbsp;=&nbsp;apache <br> env&nbsp;=&nbsp;prod <br> env&nbsp;=&nbsp;staging <br> env&nbsp;=&nbsp;dev | Kategorisieren Sie Ressourcen in Bezug auf ihren Zweck innerhalb einer Workload, auf die Umgebung, in der sie bereitgestellt werden, oder auf andere funktionsbezogene oder operative Details. |
| Klassifizierung | confidentiality&nbsp;=&nbsp;private <br> SLA&nbsp;=&nbsp;24hours | Klassifiziert eine Ressource danach, wie sie verwendet wird und welche Richtlinien für sie gelten. |
| Buchhaltung | department&nbsp;=&nbsp;finance <br> program&nbsp;=&nbsp;business-initiative <br> region&nbsp;=&nbsp;northamerica | Ermöglicht die Zuordnung einer Ressource zu bestimmten Gruppen innerhalb einer Organisation zu Abrechnungszwecken. |
| Partnerschaft | owner&nbsp;=&nbsp;jsmith <br> contactalias&nbsp;=&nbsp;catsearchowners <br> stakeholders&nbsp;=&nbsp;user1;user2;user3 | Enthält Informationen dazu, welche Personen (außerhalb der IT) mit der Ressource verknüpft oder in anderer Form von ihr betroffen sind. |
| Zweck | businessprocess&nbsp;=&nbsp;support <br> businessimpact&nbsp;=&nbsp;moderate <br> revenueimpact&nbsp;=&nbsp;high | Richtet Ressourcen an Geschäftsfunktionen aus, um Investitionsentscheidungen besser zu unterstützen. |

<!-- docsTest:enable -->
<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zur Benennung und Markierung in Azure finden Sie unter:

- [Namenskonventionen für Azure-Ressourcen](../../ready/azure-best-practices/naming-and-tagging.md). In dieser Anleitung finden Sie empfohlene Benennungskonventionen für Azure-Ressourcen.
- [Verwenden von Tags zum Organisieren von Azure-Ressourcen und Verwaltungshierarchie](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources). Sie können Tags in Azure sowohl auf der Ressourcengruppenebene als auch auf der Ebene einzelner Ressourcen anwenden. So können Sie Abrechnungsberichte anhand der angewendeten Markierungen unterschiedlich detailliert gestalten.

## <a name="next-steps"></a>Nächste Schritte

„Ressourcenmarkierung“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die [Übersicht über Leitfäden zur Entscheidungsfindung](../index.md), um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
