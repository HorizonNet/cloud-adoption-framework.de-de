---
title: Leitfaden zur Entscheidungsfindung für Ressourcenbenennung und -markierung
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie mehr über Ressourcenorganisation und -markierung als Hauptdienst in Azure-Migrationen.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 4d28e0ec6dea61a96e463df8fd2717ed0a8c8f02
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023643"
---
# <a name="resource-naming-and-tagging-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Ressourcenbenennung und -markierung

Die Organisation cloudbasierter Ressourcen ist eine der wichtigsten Aufgaben für die IT-Abteilung, sofern Sie nicht nur über einfache Bereitstellungen verfügen. Die Organisation Ihrer Ressourcen erfüllt drei Hauptaufgaben:

- **Ressourcenverwaltung:** Ihre IT-Teams müssen Ressourcen, die bestimmten Workloads, Umgebungen, Besitzergruppen oder anderen wichtigen Informationen zugeordnet sind, schnell finden. Die Organisation von Ressourcen ist wichtig für die Zuweisung organisatorischer Rollen und Zugriffsberechtigungen für die Ressourcenverwaltung.
- **Automatisierung:** Neben einer Vereinfachung der Ressourcenverwaltung für die IT-Abteilung ermöglicht Ihnen ein angemessenes Organisationsschema die Nutzung der Automatisierung im Rahmen der Ressourcenerstellung, der Betriebsüberwachung und der Erstellung von DevOps-Prozessen.
- **Rechnungsstellung:** Um Unternehmensgruppen auf den Verbrauch von Cloudressourcen aufmerksam zu machen, muss die IT-Abteilung verstehen, welche Workloads und Teams welche Ressourcen verwenden. Um Ansätze wie z.B. die verbrauchsbasierte Kostenzuteilung zu unterstützen, müssen Cloudressourcen dem Besitz und der Nutzung entsprechend organisiert werden.

## <a name="tagging-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Markierungen

![Abbildung der Markierungsoptionen mit zunehmender Komplexität entsprechend den nachstehenden weiterführenden Links](../../_images/decision-guides/decision-guide-resource-tagging.png)

Wechseln Sie zu: [Baselinenamenskonventionen](#baseline-naming-conventions) | [Ressourcenmarkierungsmuster](#resource-tagging-patterns) | [Weitere Informationen](#learn-more)

Ihr Markierungsansatz kann einfach oder komplex sein, wobei der Schwerpunkt von der Unterstützung der IT-Teams, die die Cloudworkloads verwalten, bis zur Integration von Informationen zu sämtlichen Aspekten des Unternehmen reichen kann.

Ein IT-orientierter Markierungsfokus (etwa Markierungen auf der Grundlage von Workload, Funktion oder Umgebung) macht die Überwachung von Ressourcen weniger komplex und vereinfacht Entscheidungen auf der Grundlage operativer Anforderungen erheblich.

Bei Markierungsschemas mit geschäftlichem Fokus (beispielsweise Buchhaltung, Unternehmensbesitz oder geschäftliche Bedeutung) muss unter Umständen mehr Zeit in die Erstellung von Markierungsstandards investiert werden, die die Geschäftsinteressen widerspiegeln und diese Standards langfristig bewahren. Allerdings ist das Ergebnis dieses Prozesses ein Markierungssystem, das eine verbesserte Erfassung der Kosten und des Werts von IT-Ressourcen für das gesamte Unternehmen bietet. Diese Verknüpfung des geschäftlichen Werts einer Ressource mit den Betriebskosten ist einer der ersten Schritte, um die Wahrnehmung der IT als Kostenfaktor in Ihrer Organisation zu verändern.

## <a name="baseline-naming-conventions"></a>Baselinenamenskonventionen

Eine standardisierte Namenskonvention ist der Ausgangspunkt für die Organisation Ihrer in der Cloud gehosteten Ressourcen. Mit einem ordnungsgemäß strukturierten Benennungssystem können Sie Ressourcen sowohl zu Verwaltungs- als auch zu Abrechnungszwecken schnell identifizieren. Wenn in anderen Teilen Ihrer Organisation bereits IT-Namenskonventionen vorhanden sind, wägen Sie ab, ob Sie Ihre Namenskonventionen für die Cloud darauf abstimmen oder separate cloudbasierte Standards einrichten möchten.

Beachten Sie auch, dass unterschiedliche Azure-Ressourcentypen unterschiedliche [Benennungsanforderungen](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions) aufweisen. Ihre Namenskonventionen müssen mit diesen Benennungsanforderungen kompatibel sein.

## <a name="resource-tagging-patterns"></a>Ressourcenmarkierungsmuster

Für eine komplexere Organisation als eine konsistente Namenskonvention bereitstellen kann, unterstützen Cloudplattformen die Möglichkeit zum Markieren von Ressourcen.

*Markierungen* sind Metadatenelemente, die den Ressourcen zugeordnet werden. Markierungen bestehen aus Paaren aus Schlüssel-Wert-Zeichenfolgen. Welche Werte Sie in diese Paare einschließen, bleibt Ihnen überlassen, aber die Anwendung einer konsistenten Menge globaler Markierungen im Rahmen einer umfassenden Benennungs- und Markierungsrichtlinie ist ein wesentlicher Bestandteil einer allgemein gültigen Governancerichtlinie.

Verwenden Sie im Rahmen Ihres Planungsprozesses die folgenden Fragen, um festzustellen, welche Art von Informationen Ihre Ressourcentags unterstützen müssen:

- Müssen Ihre Benennungs- und Markierungsrichtlinien in vorhandene Benennungs- und Organisationsrichtlinien innerhalb Ihres Unternehmens integriert werden?
- Werden Sie ein Abrechnungssystem mit verbrauchsbasierter Kostenzuteilung implementieren? Müssen Sie Ressourcen zu Buchhaltungsinformationen für Abteilungen, Geschäftsbereiche und Teams zuordnen, die über eine einfache Aufschlüsselung auf der Abonnementebene hinausgehen?
- Muss die Markierung Details wie Anforderungen zur Einhaltung gesetzlicher Bestimmungen für eine Ressource darstellen? Wie sieht es mit betriebsbezogenen Details wie Anforderungen an die Betriebszeiten, Zeitpläne für Patches oder Sicherheitsanforderungen aus?
- Welche Tags sind für alle Ressourcen auf Basis der zentralen IT-Richtlinie erforderlich? Welche Tags werden optional sein? Dürfen einzelne Teams eigene benutzerdefinierte Markierungsschemas implementieren?

Die unten aufgeführten allgemeinen Markierungsmuster zeigen beispielhaft, wie das Markieren zum Organisieren von Cloudressourcen verwendet werden kann. Diese Muster sind nicht als exklusiv gedacht und können parallel verwendet werden, wodurch sich mehrere Möglichkeiten der Organisation von Ressourcen auf der Grundlage der Anforderungen Ihres Unternehmens ergeben.

<!-- markdownlint-disable MD033 -->

| Markierungstyp | Beispiele | BESCHREIBUNG |
|-----|-----|-----|
| Funktionen            | app = catalogsearch1 <br/>tier = web <br/>webserver = apache<br/>env = prod <br/>env = staging <br/>env = dev                 | Kategorisieren Sie Ressourcen in Bezug auf ihren Zweck innerhalb einer Workload, auf die Umgebung, in der sie bereitgestellt werden, oder auf andere funktionsbezogene oder operative Details.                                 |
| Classification        | confidentiality=private<br/>sla = 24hours                                 | Klassifiziert eine Ressource danach, wie sie verwendet wird und welche Richtlinien für sie gelten.                               |
| Buchhaltung            | department = finance <br/>project = catalogsearch <br/>region = northamerica | Ermöglicht die Zuordnung der Ressource zu bestimmten Gruppen innerhalb einer Organisation zu Abrechnungszwecken. |
| Partnerschaft           | owner = jsmith <br/>contactalias = catsearchowners<br/>stakeholders = user1;user2;user3<br/>                       | Enthält Informationen dazu, welche Personen (außerhalb der IT) mit der Ressource verknüpft oder in anderer Form von ihr betroffen sind.                      |
| Zweck               | businessprocess=support<br/>businessimpact=moderate<br/>revenueimpact=high   | Richtet Ressourcen an Geschäftsfunktionen aus, um Investitionsentscheidungen besser zu unterstützen.  |

<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zur Benennung und Markierung in Azure finden Sie unter:

- [Namenskonventionen für Azure-Ressourcen](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). In dieser Anleitung finden Sie empfohlene Benennungskonventionen für Azure-Ressourcen.
- [Verwenden von Tags zum Organisieren von Azure-Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags?toc=/azure/billing/TOC.json). Sie können Tags in Azure sowohl auf der Ressourcengruppenebene als auch auf der Ebene einzelner Ressourcen anwenden. So können Sie Abrechnungsberichte anhand der angewendeten Markierungen unterschiedlich detailliert gestalten.

## <a name="next-steps"></a>Nächste Schritte

„Ressourcenmarkierung“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die [Übersicht über Leitfäden zur Entscheidungsfindung](../index.md), um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
