---
title: Effizientes Organisieren Ihrer Azure-Ressourcen
description: Informationen zu bewährten Methoden zur effektiven Organisation Ihrer Azure-Ressourcen, um die Ressourcenverwaltung zu vereinfachen.
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: e623658907c4f6e97574e1e8c0012933a6233e8f
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572900"
---
<!-- cSpell:ignore laraaleite profx fsubscriptions fresource -->

# <a name="organize-your-azure-resources-effectively"></a>Effizientes Organisieren Ihrer Azure-Ressourcen

Die Organisation Ihrer cloudbasierten Ressourcen ist entscheidend für die Sicherung, Verwaltung und Nachverfolgung der mit Ihren Workloads verbundenen Kosten. Definieren Sie zum Organisieren Ihrer Ressourcen eine Verwaltungsgruppenhierarchie, befolgen Sie eine gut durchdachte Namenskonvention, und wenden Sie Ressourcentagging an.

<!-- markdownlint-disable MD024 MD025 -->

## <a name="azure-management-groups-and-hierarchy"></a>[Azure-Verwaltungsgruppen und -Hierarchie](#tab/AzureManagementGroupsAndHierarchy)

Azure bietet vier Verwaltungsebenen: Verwaltungsgruppen, Abonnements, Ressourcengruppen und Ressourcen. In der folgenden Abbildung ist die Beziehung dieser Ebenen dargestellt.

   ![Diagramm, das die Beziehungen zwischen den Ebenen der Verwaltungshierarchie zeigt](./media/organize-resources/scope-levels.png) _Abbildung 1: Wie sich die vier Ebenen des Verwaltungsbereichs zueinander verhalten._

- **Verwaltungsgruppen**: Diese Gruppen sind Container, mit denen Sie Zugriff, Richtlinien und Konformität für mehrere Abonnements verwalten können. Alle Abonnements in einer Verwaltungsgruppe erben automatisch die auf die Verwaltungsgruppe angewendeten Bedingungen.
- **Abonnements**: Ein Abonnement schafft eine logische Zuordnung zwischen Benutzerkonten und den von diesen Benutzerkonten erstellten Ressourcen. Für jedes Abonnement gelten Einschränkungen oder Kontingente für die Menge an Ressourcen, die Sie erstellen und verwenden können. Organisationen können Abonnements verwenden, um die Kosten und Ressourcen zu verwalten, die von Benutzern, Teams oder Projekten erstellt werden.
- **Ressourcengruppen**: Eine Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen wie Web-Apps, Datenbanken und Speicherkonten bereitgestellt und verwaltet werden.
- **Ressourcen:** Ressourcen sind Instanzen von Diensten, die Sie erstellen. Hierzu zählen beispielsweise virtuelle Computer, Speicher oder SQL-Datenbanken.

### <a name="scope-of-management-settings"></a>Umfang der Verwaltungseinstellungen

Sie können Verwaltungseinstellungen, z. B. Richtlinien und die rollenbasierte Zugriffssteuerung, auf allen Verwaltungsebenen anwenden. Die von Ihnen ausgewählte Ebene bestimmt, wie umfassend die Einstellung angewendet wird. Niedrigere Ebenen erben die Einstellungen von höheren Ebenen. Wenn Sie beispielsweise eine Richtlinie auf ein Abonnement anwenden, wird sie auch auf alle Ressourcengruppen und Ressourcen des Abonnements angewendet.

In der Regel ist es sinnvoll, wichtige Einstellungen auf höheren Ebenen und projektspezifische Anforderungen auf niedrigeren Ebenen anzuwenden. Sie könnten beispielsweise sicherstellen, dass alle Ressourcen für Ihre Organisation in bestimmten Regionen bereitgestellt werden. Hierfür wenden Sie eine Richtlinie, die die zulässigen Standorte angibt, auf das Abonnement an. Wenn andere Benutzer in Ihrer Organisation neue Ressourcengruppen und Ressourcen hinzufügen, werden die zulässigen Standorte automatisch erzwungen. Weitere Informationen zu Richtlinien finden Sie im Abschnitt zu Governance, Sicherheit und Konformität in diesem Leitfaden.

Wenn Sie nur über wenige Abonnements verfügen, ist deren unabhängige Verwaltung relativ einfach. Wenn die Anzahl der von Ihnen verwendeten Abonnements steigt, sollten Sie erwägen, eine Verwaltungsgruppenhierarchie zu erstellen, um die Verwaltung Ihrer Abonnements und Ressourcen zu vereinfachen. Weitere Informationen finden Sie unter [Organisieren und Verwalten Ihrer Azure-Abonnements](../azure-best-practices/organize-subscriptions.md).

Arbeiten Sie zur Planung Ihrer Konformitätsstrategie mit Personen in Ihrer Organisation zusammen, die über Rollen in diesen Bereichen verfügen: Sicherheit und Konformität, IT-Verwaltung, Unternehmensarchitektur, Netzwerk, Finanzen und Beschaffung.

::: zone target="docs"

### <a name="create-a-management-level"></a>Erstellen einer Verwaltungsebene

Sie können eine Verwaltungsgruppe, weitere Abonnements oder Ressourcengruppen erstellen.

#### <a name="create-a-management-group"></a>Erstellen einer Verwaltungsgruppe

Erstellen Sie eine Verwaltungsgruppe, um die Verwaltung von Zugriff, Richtlinien und Konformität für mehrere Abonnements zu vereinfachen.

1. Navigieren Sie zu [Verwaltungsgruppen](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Wählen Sie **Verwaltungsgruppe hinzufügen**.

#### <a name="create-a-subscription"></a>Erstellen eines Abonnements

Verwenden Sie Abonnements, um Kosten und Ressourcen zu verwalten, die von Benutzern, Teams oder Projekten verursacht bzw. erstellt werden.

1. Navigieren Sie zu [Abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
2. Wählen Sie **Hinzufügen**.

> [!NOTE]
> Abonnements können auch programmgesteuert erstellt werden. Weitere Informationen finden Sie unter [Programmgesteuertes Erstellen von Azure Enterprise-Abonnements](/azure/azure-resource-manager/management/programmatically-create-subscription?tabs=azure-powershell).

#### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Erstellen Sie eine Ressourcengruppe für Ressourcen wie Web-Apps, Datenbanken und Speicherkonten mit gleichem Lebenszyklus, gleichen Berechtigungen und gleichen Richtlinien.

1. Navigieren Sie zu [Ressourcengruppen](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Wählen Sie **Hinzufügen**.
1. Wählen Sie das **Abonnement** aus, unter dem Sie Ihre Ressourcengruppe erstellen möchten.
1. Geben Sie einen Namen für die **Ressourcengruppe** ein.
1. Wählen Sie eine **Region** für den Standort der Ressourcengruppe aus.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure-Grundlagen](../considerations/fundamental-concepts.md)
- [Erstellen Ihrer anfänglichen Abonnements](../azure-best-practices/initial-subscriptions.md)
- [Erstellen zusätzlicher Azure-Abonnements zum Skalieren Ihrer Azure-Umgebung](../azure-best-practices/scale-subscriptions.md)
- [Organisieren und Verwalten Ihrer Azure-Abonnements](../azure-best-practices/organize-subscriptions.md)
- [Organisieren Ihrer Ressourcen mit Azure-Verwaltungsgruppen](/azure/azure-resource-manager/management-groups-overview)
- [Grundlegendes zur Ressourcenzugriffsverwaltung in Azure](../../govern/resource-consistency/resource-access-management.md)
- [Einschränkungen bei Abonnementdiensten](/azure/azure-resource-manager/management/azure-subscription-service-limits)

::: zone-end

::: zone target="chromeless"

### <a name="actions"></a>Aktionen

**Erstellen einer Verwaltungsgruppe**:

Erstellen Sie eine Verwaltungsgruppe, um die Verwaltung von Zugriff, Richtlinien und Konformität für mehrere Abonnements zu vereinfachen.

1. Navigieren Sie zu **Verwaltungsgruppen**.
1. Wählen Sie **Verwaltungsgruppe hinzufügen**.

::: form action="OpenBlade[#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade]" submitText="Go to Management groups" :::

**Erstellen eines zusätzlichen Abonnements**:

Verwenden Sie Abonnements, um Kosten und Ressourcen zu verwalten, die von Benutzern, Teams oder Projekten verursacht bzw. erstellt werden.

1. Navigieren Sie zu **Abonnements**.
1. Wählen Sie **Hinzufügen**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

**Erstellen einer Ressourcengruppe**:

Erstellen Sie eine Ressourcengruppe für Ressourcen wie Web-Apps, Datenbanken und Speicherkonten mit gleichem Lebenszyklus, gleichen Berechtigungen und gleichen Richtlinien.

1. Navigieren Sie zu **Ressourcengruppen**.
1. Wählen Sie **Hinzufügen**.
1. Wählen Sie das **Abonnement** aus, unter dem Sie Ihre Ressourcengruppe erstellen möchten.
1. Geben Sie einen Namen für die **Ressourcengruppe** ein.
1. Wählen Sie eine **Region** für den Standort der Ressourcengruppe aus.

::: form action="Create[#create/Microsoft.ResourceGroup]" submitText="Create a resource group" :::

::: zone-end

## <a name="naming-standards"></a>[Benennungsstandards](#tab/NamingStandards)

Mit einem durchdachten Benennungsstandard lassen sich Ressourcen im Azure-Portal, in einer Abrechnung und in Automatisierungsskripts leichter identifizieren. Ihre Namensstrategie sollte geschäftliche und operative Details als Bestandteile von Ressourcennamen einbeziehen:

Die unternehmensbezogene Seite dieser Strategie sollte sicherstellen, dass Ressourcennamen die Organisationsinformationen enthalten, die zum Identifizieren der Teams benötigt werden. Verwenden Sie eine Ressource zusammen mit den Geschäftsbesitzern, die für die Ressourcenkosten verantwortlich sind.

Auf der operativen Seite sollte sichergestellt werden, dass die Namen von IT-Teams benötigte Informationen enthalten. Verwenden Sie die Details, die die Workload, Anwendung, Umgebung, Wichtigkeit und andere Informationen identifizieren, die für die Verwaltung von Ressourcen nützlich sind.

Für die verschiedenen Ressourcentypen gelten unterschiedliche [Benennungsregeln und Einschränkungen](/azure/azure-resource-manager/management/resource-name-rules). Weitere Informationen und Empfehlungen, die speziell auf die Unterstützung von Bemühungen zur Einführung von Enterprise Clouds abzielen, finden Sie in der [Anleitung zu Benennung und Tagging](../azure-best-practices/naming-and-tagging.md) für das Framework für die Cloudeinführung (Cloud Adoption Framework).

Die folgende Tabelle enthält Namensmuster für einige Beispieltypen von Azure-Ressourcen.

::: zone target="docs"

>[!TIP]
> Verwenden Sie möglichst keine Sonderzeichen (`-` oder `_`) als erstes oder letztes Zeichen eines Namens. Diese Zeichen führen bei den meisten Validierungsregeln zu einem Fehler.

::: zone-end

| Entität | `Scope` | Länge | Schreibweise | Gültige Zeichen | Vorgeschlagenes Muster | Beispiel |
| --- | --- | --- | --- | --- | --- | --- |
| Resource group | Subscription | 1-90 | Groß-/Kleinschreibung nicht beachten | Alphanumerisch, Unterstrich, Klammern, Bindestrich, Punkt (außer am Ende) und Unicode-Zeichen | `<service short name>-<environment>-rg` | `profx-prod-rg` |
| Verfügbarkeitsgruppe | Resource group | 1-80 | Groß-/Kleinschreibung nicht beachten | Alphanumerisch, Unterstrich und Bindestrich | `<service-short-name>-<context>-as` | `profx-SQL-as` |
| Tag | Zugeordnete Entität | 512 (Name), 256 (Wert) | Groß-/Kleinschreibung nicht beachten | Alphanumerisch | `"Key" : "value"` | `"Department" : "Central IT"` |

## <a name="resource-tags"></a>[Ressourcentags](#tab/ResourceTags)

Tags sind nützlich, um Ihre Ressourcen und Ressourcengruppen schnell identifizieren zu können. Durch Anwenden von Tags können Sie Ihre Azure-Ressourcen logisch nach Kategorien organisieren. Jedes Tag besteht aus einem Namen und einem Wert. So können Sie beispielsweise den Namen „Umgebung“ und den Wert „Produktion“ auf alle Ressourcen in der Produktion anwenden. Tags sollten den Kontext über die zugehörige Workload oder Anwendung der Ressource, betriebliche Anforderungen und Angaben zum Besitzer einbeziehen.

Nach dem Anwenden von Tags können Sie alle Ressourcen in Ihrem Abonnement abrufen, die diesen Tagnamen und -wert besitzen. Wenn Sie Ressourcen für die Abrechnung oder Verwaltung organisieren, können Tags Ihnen dabei helfen, verwandte Ressourcen aus verschiedenen Ressourcengruppen abzurufen.

Sie können Tags auch für viele andere Dinge verwenden. Sie werden häufig für folgende Aufgaben genutzt:

- **Metadaten und Dokumentation**: Durch Anwenden eines Tags wie `projectowner` können Administratoren problemlos Details zu den Ressourcen anzeigen, an denen sie arbeiten.
- **Automatisierung:** Unter Umständen verfügen Sie über regelmäßig ausgeführte Skripts, die basierend auf einem Tagwert wie `shutdowntime` oder `deprovisiondate` eine Aktion durchführen können.
- **Kostenoptimierung:** Sie können den Teams und Mitarbeitern, die für die Kosten verantwortlich sind, Ressourcen zuweisen. In der Azure-Kostenverwaltung und -Abrechnung können Sie das Kostenstellentag als Filter anwenden, um die Gebühren basierend auf der Nutzung eines Teams oder einer Abteilung zu melden.

Jede Ressource oder Ressourcengruppe kann maximal 50 Tagname-Wert-Paare aufweisen. Diese Einschränkung gilt nur für Tags, die direkt auf die Ressourcengruppe oder die Ressource angewendet werden.

Weitere Empfehlungen und Beispiele zur Kennzeichnung finden Sie unter [Empfohlene Namens- und Kennzeichnungskonventionen](../azure-best-practices/naming-and-tagging.md) im Cloud Adoption Framework.

::: zone target="docs"

### <a name="apply-a-resource-tag"></a>Anwenden eines Ressourcentags

So wenden Sie ein Tag auf eine Ressourcengruppe an:

1. Navigieren Sie zu [Ressourcengruppen](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups).
1. Wählen Sie eine Ressourcengruppe aus.
1. Wählen Sie **Tags zuweisen** aus.
1. Geben Sie einen neuen Namen und Wert ein, oder verwenden Sie die Dropdownliste, um einen bereits vorhandenen Namen und Wert auszuwählen.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter [Verwenden von Tags zum Organisieren von Azure-Ressourcen](/azure/azure-resource-manager/management/tag-resources).

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Aktion

**Anwenden eines Ressourcentags**:

So wenden Sie ein Tag auf eine Ressourcengruppe an:

1. Navigieren Sie zu **Ressourcengruppen**.
1. Wählen Sie eine Ressourcengruppe aus.
1. Wählen Sie **Tags** aus.
1. Geben Sie einen neuen Namen und Wert ein, oder wählen Sie einen bereits vorhandenen Namen und Wert aus.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups]" submitText="Go to resource groups" :::

::: zone-end
