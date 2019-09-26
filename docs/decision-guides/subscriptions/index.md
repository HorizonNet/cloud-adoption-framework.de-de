---
title: Leitfaden zur Entscheidungsfindung für Abonnements
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie mehr über Cloudplattformabonnements als Basisdienst in Azure-Migrationen.
author: alexbuckgit
ms.author: abuck
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: a5774cc1f22265c532bc9d885aab354cc1b2d297
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221007"
---
# <a name="subscription-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Abonnements

Ein effektiver Abonnemententwurf hilft Organisationen in der Cloudeinführungsphase dabei, eine Struktur für die Organisationsressourcen in Azure einzurichten.

Jede Ressource in Azure (etwa ein virtueller Computer oder eine Datenbank) wird einem Abonnement zugeordnet. Die Einführung von Azure beginnt mit der Erstellung eines Azure-Abonnements, der Zuordnung dieses Abonnements zu einem Konto und der anschließenden Bereitstellung von Ressourcen für das Abonnement. Eine Übersicht über diese Konzepte finden Sie unter [Azure fundamental concepts](../../ready/considerations/fundamental-concepts.md) (Grundlegende Konzepte in Azure).

Mit zunehmendem Umfang Ihrer digitalen Ressourcen in Azure müssen nach und nach wahrscheinlich weitere Abonnements erstellt werden, um Ihren Bedarf zu decken. In Azure können Sie eine Verwaltungsgruppenhierarchie definieren, um Ihre Abonnements zu strukturieren und mühelos die passende Richtlinie auf die gewünschten Ressourcen anzuwenden. Weitere Informationen finden Sie unter [Scaling with multiple Azure subscriptions](../../ready/considerations/scaling-subscriptions.md) (Skalieren mit mehreren Azure-Abonnements).

Im Anschluss folgen einige einfache Beispiele für die Trennung verschiedener Workloads mithilfe von Verwaltungsgruppen:

- **Produktionsbezogen bzw. nicht produktionsbezogen:** Einige Unternehmen erstellen Verwaltungsgruppen, um Abonnements danach zu trennen, ob sie produktionsbezogen sind oder nicht. Verwaltungsgruppen ermöglichen es diesen Kunden, Rollen und Richtlinien einfacher zu verwalten. Beispielsweise kann ein nicht produktionsbezogenes Abonnement Entwicklern den **Mitwirkender**-Zugriff ermöglichen, aber in der Produktion haben sie nur **Leser**-Zugriff.
- **Interne Dienste bzw. externe Dienste:** Ähnlich wie bei produktionsbezogenen und nicht produktionsbezogenen Workloads haben Unternehmen häufig unterschiedliche Anforderungen, Richtlinien und Rollen für interne und externe kundenorientierte Dienste.

In diesem Entscheidungsleitfaden werden verschiedene Ansätze für die Strukturierung Ihrer Verwaltungsgruppenhierarchie vorgestellt.

## <a name="subscription-design-patterns"></a>Abonnemententwurfsmuster

Da jede Organisation anders ist, sind Azure-Verwaltungsgruppen auf Flexibilität ausgelegt. Orientieren Sie sich bei der Modellierung Ihrer Cloudressourcen am besten an der Hierarchie Ihrer Organisation. Dies vereinfacht das Definieren und Anwenden von Richtlinien auf höheren Hierarchieebenen, und die Vererbung sorgt dafür, dass diese Richtlinien automatisch auf untergeordnete Verwaltungsgruppen der Hierarchie angewendet werden. Abonnements können zwar zwischen verschiedenen Verwaltungsgruppen verschoben werden, es empfiehlt sich jedoch, zu Beginn eine Verwaltungsgruppenhierarchie zu entwerfen, die die voraussichtlichen Anforderungen Ihrer Organisation erfüllt.

Berücksichtigen Sie vor der Fertigstellung Ihres Abonnemententwurfs auch den Einfluss der [Ressourcenkonsistenz](../resource-consistency/index.md) auf Ihre Gestaltungsmöglichkeiten.

> [!NOTE]
> Dank Azure Enterprise Agreements (EAs) können Sie zu Abrechnungszwecken eine weitere Organisationshierarchie definieren. Diese Hierarchie ist von Ihrer Verwaltungsgruppenhierarchie getrennt, die in erster Linie dazu dient, ein Vererbungsmodell bereitzustellen, mit dem Sie komfortabel geeignete Richtlinien und eine Zugriffssteuerung für Ihre Ressourcen implementieren können.

Die folgenden Abonnementmuster spiegeln eine anfängliche Komplexitätszunahme beim Abonnemententwurf wider – gefolgt von einigen erweiterten Hierarchien, die sich ggf. gut für Ihre Organisation eignen:

### <a name="single-subscription"></a>Ein Abonnement

Ein einzelnes Abonnement pro Konto kann für Organisationen ausreichen, die eine kleine Anzahl von in der Cloud gehosteten Ressourcen bereitstellen müssen. Dies ist das erste Abonnementmuster, das Sie zu Beginn Ihres Cloudeinführungsprozesses implementieren. Damit können Sie sich anhand kleiner experimenteller Bereitstellungen oder Proof of Concept-Bereitstellungen mit den Möglichkeiten der Cloud vertraut machen.

### <a name="production-and-nonproduction-pattern"></a>Muster für Produktion und Nichtproduktion

Wenn Sie für die Bereitstellung einer Workload in einer Produktionsumgebung bereit sind, sollten Sie ein weiteres Abonnement hinzufügen. Dadurch stellen Sie sicher, dass Produktionsdaten und andere Ressourcen nicht in Ihre Entwicklungs-/Testumgebungen gelangen. Außerdem können Sie problemlos zwei verschiedene Richtliniensätze auf die Ressourcen in den beiden Abonnements anwenden.

![Abonnementmuster für Produktion und Nichtproduktion](../../_images/ready/basic-subscription-model.png)

### <a name="workload-separation-pattern"></a>Muster zur Trennung von Workloads

Wenn eine Organisation der Cloud neue Workloads hinzufügt, können unterschiedliche Abonnementzuständigkeiten sowie die grundlegende Trennung von Aufgaben dazu führen, dass Produktions- und Nichtproduktionsverwaltungsgruppen mehrere Abonnements enthalten. Dieser Ansatz bietet zwar eine grundlegende Trennung von Workloads, profitiert aber nicht nennenswert vom Vererbungsmodell zur automatischen Anwendung von Richtlinien auf eine Teilmenge Ihrer Abonnements.

![Muster zur Trennung von Workloads](../../_images/ready/management-group-hierarchy.png)

### <a name="application-category-pattern"></a>Auf Anwendungskategorien basierendes Muster

Mit zunehmender Cloudnutzung einer Organisation werden in der Regel weitere Abonnements hinzugefügt, um Anwendungen zu unterstützen, die sich in puncto geschäftliche Bedeutung, Konformitätsanforderungen, Zugriffssteuerung oder Datenschutzanforderungen erheblich unterscheiden. Die Abonnements zur Unterstützung dieser Anwendungskategorien orientieren sich am Muster für Produktion und Nichtproduktion und sind entweder in der Produktions- oder in der Nichtproduktionsverwaltungsgruppe organisiert. Diese Abonnements werden in der Regel vom zentralen IT-Personal betreut und verwaltet.

![Auf Anwendungskategorien basierendes Muster](../../_images/infra-subscriptions/application.png)

Jede Organisation kategorisiert ihre Anwendungen anders. Oftmals werden Abonnements basierend auf bestimmten Anwendungen oder Diensten oder nach Anwendungsarchetypen getrennt. Diese Kategorisierung dient häufig zur Unterstützung von Workloads, die voraussichtlich einen Großteil der begrenzten Ressourcen eines Abonnements beanspruchen, oder zur Trennung unternehmenskritischer Workloads, um sicherzustellen, dass sie nicht mit anderen Workloads um diese begrenzten Ressourcen konkurrieren. In Anschluss folgen einige Workloads, die ein separates Abonnement im Rahmen dieses Musters rechtfertigen:

- Unternehmenskritische Workloads
- Anwendungen, die in Ihrem Unternehmen Teil der Umsatzkosten (Cost Of Goods Sold, COGS) sind. Beispiel: Jede Instanz des Widgets von Unternehmen X enthält ein Azure IoT-Modul, das Telemetriedaten sendet. Dies erfordert unter Umständen ein dediziertes Abonnement zu Buchhaltungs-/Governancezwecken im Rahmen von COGS.
- Anwendungen, die behördlichen Anforderungen wie HIPAA oder FedRAMP unterliegen.

### <a name="functional-pattern"></a>Auf Funktionen basierendes Muster

Beim auf Funktionen basierenden Muster werden die Abonnements und Konten anhand von Geschäftsbereichen wie Finanzen, Vertrieb oder IT-Support unter Verwendung einer Verwaltungsgruppenhierarchie strukturiert.

### <a name="business-unit-pattern"></a>Auf Unternehmenseinheiten basierendes Muster

Beim auf Unternehmenseinheiten basierenden Muster werden Abonnements und Konten auf der Grundlage von Gewinn-und-Verlust-Kategorie, Geschäftseinheit, Abteilung, Profitcenter oder ähnlichen Geschäftsstrukturen unter Verwendung einer Verwaltungsgruppenhierarchie gruppiert.

### <a name="geographic-pattern"></a>Auf geografischen Regionen basierendes Muster

Das auf geografischen Regionen basierende Muster ist für global agierende Organisationen konzipiert und gruppiert Abonnements und Konten auf der Grundlage geografischer Regionen unter Verwendung einer Verwaltungsgruppenhierarchie.

## <a name="mixed-patterns"></a>Gemischte Muster

Verwaltungsgruppenhierarchien können bis zu sechs Ebenen umfassen. Dieses Maß an Flexibilität ermöglicht die Erstellung einer Hierarchie mit mehreren dieser Muster, um den Anforderungen Ihrer Organisation gerecht zu werden. Das folgende Diagramm zeigt beispielsweise eine Organisationshierarchie, in der ein auf Unternehmenseinheiten basierendes Muster mit einem auf geografischen Regionen basierenden Muster kombiniert wird:

![Muster für gemischte Abonnements](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Zugehörige Ressourcen

- [Ressourcenzugriffsverwaltung in Azure](../../govern/resource-consistency/resource-access-management.md)
- [Große Unternehmen: mehrere Governance-Ebenen in großen Unternehmen](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Mehrere geografische Regionen](../regions/index.md)

## <a name="next-steps"></a>Nächste Schritte

„Abonnemententwurf“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die [Übersicht über Leitfäden zur Entscheidungsfindung](../index.md), um mehr über alternative Muster oder Modelle zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
