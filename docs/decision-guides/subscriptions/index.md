---
title: Leitfaden zur Entscheidungsfindung für Abonnements
description: Grundlegendes zu den Abonnemententwurfsstrategien und der Verwaltungsgruppenhierarchie zum Organisieren Ihrer Azure-Ressourcen
author: alexbuckgit
ms.author: abuck
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: e733280147a16287e92ab93334111950a2583497
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355484"
---
# <a name="subscription-decision-guide"></a>Leitfaden zur Entscheidungsfindung für Abonnements

Ein effektiver Abonnemententwurf hilft Organisationen in der Cloudeinführungsphase dabei, eine Struktur für die Ressourcenorganisation in Azure einzurichten und zu verwalten. Dieser Leitfaden hilft Ihnen bei der Entscheidung, wann zusätzliche Abonnements zu erstellen sind und wie Sie Ihre Verwaltungsgruppenhierarchie erweitern können, um Ihre geschäftlichen Prioritäten zu unterstützen.

## <a name="prerequisites"></a>Voraussetzungen

Die Einführung von Azure beginnt mit der Erstellung eines Azure-Abonnements, der Zuordnung dieses Abonnements zu einem Konto und der anschließenden Bereitstellung von Ressourcen wie virtuellen Computern und Datenbanken für das Abonnement. Eine Übersicht über diese Konzepte finden Sie unter [Azure fundamental concepts](../../ready/considerations/fundamental-concepts.md) (Grundlegende Konzepte in Azure).

- [Erstellen Sie Ihre anfänglichen Abonnements](../../ready/azure-best-practices/initial-subscriptions.md).
- [Erstellen Sie zusätzliche Abonnements](../../ready/azure-best-practices/scale-subscriptions.md), um Ihre Azure-Umgebung zu skalieren.
- [Organisieren und verwalten Sie Ihre Abonnements](../../ready/azure-best-practices/organize-subscriptions.md) mithilfe von Azure-Verwaltungsgruppen.

## <a name="modeling-your-organization"></a>Modellieren Ihrer Organisation

Da jede Organisation anders ist, sind Azure-Verwaltungsgruppen auf Flexibilität ausgelegt. Orientieren Sie sich bei der Modellierung Ihrer Cloudressourcen am besten an der Hierarchie Ihrer Organisation. Dies vereinfacht das Definieren und Anwenden von Richtlinien auf höheren Hierarchieebenen, und die Vererbung sorgt dafür, dass diese Richtlinien automatisch auf untergeordnete Verwaltungsgruppen der Hierarchie angewendet werden. Abonnements können zwar zwischen verschiedenen Verwaltungsgruppen verschoben werden, es empfiehlt sich jedoch, zu Beginn eine Verwaltungsgruppenhierarchie zu entwerfen, die die voraussichtlichen Anforderungen Ihrer Organisation erfüllt.

Berücksichtigen Sie vor der Fertigstellung Ihres Abonnemententwurfs auch den Einfluss der [Ressourcenkonsistenz](../resource-consistency/index.md) auf Ihre Gestaltungsmöglichkeiten.

> [!NOTE]
> Dank Azure Enterprise Agreements (EAs) können Sie zu Abrechnungszwecken eine weitere Organisationshierarchie definieren. Diese Hierarchie ist von Ihrer Verwaltungsgruppenhierarchie getrennt, die in erster Linie dazu dient, ein Vererbungsmodell bereitzustellen, mit dem Sie komfortabel geeignete Richtlinien und eine Zugriffssteuerung für Ihre Ressourcen implementieren können.

## <a name="subscription-design-strategies"></a>Entwurfsstrategien für Abonnements

Berücksichtigen Sie die folgenden Entwurfsstrategien für Abonnements, um Ihren geschäftlichen Prioritäten gerecht zu werden.

### <a name="workload-separation-strategy"></a>Strategie zur Trennung von Workloads

Wenn eine Organisation der Cloud neue Workloads hinzufügt, können unterschiedliche Abonnementzuständigkeiten sowie die grundlegende Trennung von Aufgaben dazu führen, dass Produktions- und Nichtproduktionsverwaltungsgruppen mehrere Abonnements enthalten. Dieser Ansatz bietet zwar eine grundlegende Trennung von Workloads, profitiert aber nicht nennenswert vom Vererbungsmodell zur automatischen Anwendung von Richtlinien auf eine Teilmenge Ihrer Abonnements.

![Strategie zur Trennung von Workloads](../../_images/ready/management-group-hierarchy-v2.png)

### <a name="application-category-strategy"></a>Auf Anwendungskategorien basierende Strategie

Mit zunehmender Cloudnutzung einer Organisation werden in der Regel weitere Abonnements hinzugefügt, um Anwendungen zu unterstützen, die sich in puncto geschäftliche Bedeutung, Konformitätsanforderungen, Zugriffssteuerung oder Datenschutzanforderungen erheblich unterscheiden. Die Abonnements zur Unterstützung dieser Anwendungskategorien orientieren sich an den anfänglichen Produktions- und Nichtproduktionsabonnements und sind entweder in der Produktions- oder in der Nichtproduktionsverwaltungsgruppe organisiert. Diese Abonnements werden in der Regel vom zentralen IT-Personal betreut und verwaltet.

![Auf Anwendungskategorien basierende Strategie](../../_images/infra-subscriptions/application.png)

Jede Organisation kategorisiert ihre Anwendungen anders. Oftmals werden Abonnements basierend auf bestimmten Anwendungen oder Diensten oder nach Anwendungsarchetypen getrennt. Diese Kategorisierung dient häufig zur Unterstützung von Workloads, die voraussichtlich einen Großteil der begrenzten Ressourcen eines Abonnements beanspruchen, oder zur Trennung unternehmenskritischer Workloads, um sicherzustellen, dass sie nicht mit anderen Workloads um diese begrenzten Ressourcen konkurrieren. In Anschluss folgen einige Workloads, die ein separates Abonnement rechtfertigen:

- Unternehmenskritische Workloads
- Anwendungen, die in Ihrem Unternehmen Teil der Umsatzkosten (Cost Of Goods Sold, COGS) sind. Beispiel: Jede Instanz des Widgets von Unternehmen X enthält ein Azure IoT-Modul, das Telemetriedaten sendet. Dies erfordert unter Umständen ein dediziertes Abonnement zu Buchhaltungs-/Governancezwecken im Rahmen von COGS.
- Anwendungen, die behördlichen Anforderungen wie HIPAA oder FedRAMP unterliegen.

### <a name="functional-strategy"></a>Funktionale Strategie

Bei der auf Funktionen basierenden Strategie werden die Abonnements und Konten anhand von Geschäftsbereichen wie Finanzen, Vertrieb oder IT-Support unter Verwendung einer Verwaltungsgruppenhierarchie strukturiert.

### <a name="business-unit-strategy"></a>Auf Unternehmenseinheiten basierende Strategie

Bei der auf Unternehmenseinheiten basierenden Strategie werden Abonnements und Konten auf der Grundlage von Gewinn-und-Verlust-Kategorie, Geschäftseinheit, Abteilung, Profitcenter oder ähnlichen Geschäftsstrukturen unter Verwendung einer Verwaltungsgruppenhierarchie gruppiert.

### <a name="geographic-strategy"></a>Geografische Strategie

Die auf geografischen Regionen basierende Strategie ist für global agierende Organisationen konzipiert und gruppiert Abonnements und Konten auf der Grundlage geografischer Regionen unter Verwendung einer Verwaltungsgruppenhierarchie.

## <a name="mixing-subscription-strategies"></a>Kombinieren von Abonnementstrategien

Verwaltungsgruppenhierarchien können bis zu sechs Ebenen umfassen. Dieses Maß an Flexibilität ermöglicht die Erstellung einer Hierarchie mit mehreren dieser Strategien, um den Anforderungen Ihrer Organisation gerecht zu werden. Das folgende Diagramm zeigt beispielsweise eine Organisationshierarchie, in der eine auf Unternehmenseinheiten basierende Strategie mit einer auf geografischen Regionen basierenden Strategie kombiniert wird.

![Strategie für gemischte Abonnements](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Zugehörige Ressourcen

- [Ressourcenzugriffsverwaltung in Azure](../../govern/resource-consistency/resource-access-management.md)
- [Große Unternehmen: mehrere Governance-Ebenen in großen Unternehmen](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Mehrere geografische Regionen](../../migrate/azure-best-practices/multiple-regions.md)

## <a name="next-steps"></a>Nächste Schritte

„Abonnemententwurf“ ist nur eine der Kernkomponenten der Infrastruktur, die architekturspezifische Entscheidungen während eines Cloudeinführungsprozesses erfordert. Besuchen Sie die [Übersicht über Leitfäden zur Entscheidungsfindung](../index.md), um mehr über zusätzliche Strategien zu erfahren, die bei Entwurfsentscheidungen für andere Arten von Infrastrukturen verwendet werden.

> [!div class="nextstepaction"]
> [Leitfaden zur architekturbezogenen Entscheidungsfindung](../index.md)
