---
title: Effizientes Organisieren Ihrer Azure-Ressourcen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Bewährte Methoden zur Vereinfachung der Verwaltung Ihrer Azure-Ressourcen durch effiziente Organisation.
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: e47e7e5f8528580d4aa268fd90e7aa838e5f70ba
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239956"
---
# <a name="organize-your-azure-resources"></a>Organisieren Ihrer Azure-Ressourcen

Verwenden Sie die folgenden Features und bewährten Methoden, um kritische Systemressourcen zu schützen. Kennzeichnen von Ressourcen, sodass Sie sie anhand von Werten nachverfolgen können, die sinnvoll für Ihre Organisation sind

<!-- markdownlint-disable MD024 MD025 -->

# <a name="azure-management-groups-and-hierarchytabazuremanagmentgroupsandhierarchy"></a>[Azure-Verwaltungsgruppen und -Hierarchie](#tab/AzureManagmentGroupsAndHierarchy)

Die Organisationsstruktur für Ressourcen in Azure umfasst vier Ebenen: Verwaltungsgruppen, Abonnements, Ressourcengruppen und Ressourcen. In der folgenden Abbildung ist die Beziehung dieser Ebenen dargestellt.

![Diagramm zu den Beziehungen der Verwaltungshierarchie](./media/organize-resources/scope-levels.png)

- **Verwaltungsgruppen**: Hierbei handelt es sich um Container, mit denen Sie Zugriff, Richtlinien und Konformität für mehrere Abonnements verwalten können. Alle Abonnements in einer Verwaltungsgruppe erben automatisch die auf die Verwaltungsgruppe angewendeten Bedingungen.
- **Abonnements**: Unter einem Abonnement werden Benutzerkonten und die von diesen Benutzerkonten erstellten Ressourcen gruppiert. Für jedes Abonnement gelten Einschränkungen oder Kontingente für die Menge an Ressourcen, die Sie erstellen und verwenden können. Organisationen können Abonnements verwenden, um die Kosten und Ressourcen zu verwalten, die von Benutzern, Teams oder Projekten erstellt werden.
- **Ressourcengruppen**: Eine Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen wie Web-Apps, Datenbanken und Speicherkonten bereitgestellt und verwaltet werden.
- **Ressourcen:** Ressourcen sind Instanzen von Diensten, die Sie erstellen. Hierzu zählen beispielsweise virtuelle Computer, Speicher oder SQL-Datenbanken.

## <a name="scope-of-management-settings"></a>Umfang der Verwaltungseinstellungen

Sie können Verwaltungseinstellungen, z. B. Richtlinien und die rollenbasierte Zugriffssteuerung, auf allen Verwaltungsebenen anwenden. Die von Ihnen ausgewählte Ebene bestimmt, wie umfassend die Einstellung angewendet wird. Niedrigere Ebenen erben die Einstellungen von höheren Ebenen. Wenn Sie beispielsweise eine Richtlinie auf ein Abonnement anwenden, wird sie auch auf alle Ressourcengruppen und Ressourcen des Abonnements angewendet.

In der Regel ist es sinnvoll, wichtige Einstellungen auf höheren Ebenen und projektspezifische Anforderungen auf niedrigeren Ebenen anzuwenden. Sie können beispielsweise sicherstellen, dass alle Ressourcen für Ihre Organisation in bestimmten Regionen bereitgestellt werden. Hierfür wenden Sie eine Richtlinie, die die zulässigen Standorte angibt, auf das Abonnement an. Wenn andere Benutzer in Ihrer Organisation neue Ressourcengruppen und Ressourcen hinzufügen, werden die zulässigen Standorte automatisch erzwungen. Weitere Informationen zu Richtlinien finden Sie im Abschnitt zu Governance, Sicherheit und Konformität in diesem Leitfaden.

Zur Planung Ihrer Konformitätsstrategie empfehlen wir die Zusammenarbeit mit Personen in Ihrer Organisation, die über Rollen für die folgenden Bereiche verfügen: „Sicherheit und Konformität“, „IT-Verwaltung“, „Enterprise-Architekt“, „Netzwerk“, „Finanzen“ und „Beschaffung“.

::: zone target="docs"

## <a name="create-a-management-level"></a>Erstellen einer Verwaltungsebene

Sie können eine Verwaltungsgruppe, weitere Abonnements oder Ressourcengruppen erstellen.

### <a name="create-management-group"></a>Erstellen einer Verwaltungsgruppe

Erstellen Sie eine Verwaltungsgruppe, um die Verwaltung von Zugriff, Richtlinien und Konformität für mehrere Abonnements zu vereinfachen.

1. Navigieren Sie zu [Verwaltungsgruppen](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Wählen Sie **Verwaltungsgruppe hinzufügen**.

### <a name="create-subscription"></a>Erstellen des Abonnements

Verwenden Sie Abonnements, um Kosten und Ressourcen zu verwalten, die von Benutzern, Teams oder Projekten verursacht bzw. erstellt werden.

1. Navigieren Sie zu [Abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Wählen Sie **Hinzufügen**.

### <a name="create-resource-group"></a>Ressourcengruppe erstellen

Erstellen Sie eine Ressourcengruppe für Ressourcen wie Web-Apps, Datenbanken und Speicherkonten mit gleichem Lebenszyklus, gleichen Berechtigungen und gleichen Richtlinien.

1. Navigieren Sie zu [Ressourcengruppen](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Wählen Sie **Hinzufügen**.
1. Wählen Sie das **Abonnement** aus, unter dem Sie Ihre Ressourcengruppe erstellen möchten.
1. Geben Sie einen Namen für die **Ressourcengruppe** ein.
1. Wählen Sie eine **Region** für den Standort der Ressourcengruppe aus.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Grundlegendes zur Ressourcenzugriffsverwaltung in Azure](../../govern/resource-consistency/resource-access-management.md)
- [Organisieren Ihrer Ressourcen mit Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview)
- [Einschränkungen bei Abonnementdiensten](https://docs.microsoft.com/azure/azure-subscription-service-limits)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Aktionen

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

1. Wechseln Sie zu **Ressourcengruppen**.
1. Wählen Sie **Hinzufügen**.
1. Wählen Sie das **Abonnement** aus, unter dem Sie Ihre Ressourcengruppe erstellen möchten.
1. Geben Sie einen Namen für die **Ressourcengruppe** ein.
1. Wählen Sie eine **Region** für den Standort der Ressourcengruppe aus.

::: form action="Create[#create/Microsoft.ResourceGroup]" submitText="Create a resource group" :::

::: zone-end

# <a name="naming-standardstabnamingstandards"></a>[Benennungsstandards](#tab/NamingStandards)

Mit einem durchdachten Benennungsstandard lassen sich Ressourcen im Portal, auf einer Rechnung und in Skripts leichter identifizieren. Möglicherweise verwenden Sie bereits Benennungsstandards für Ihre lokale Infrastruktur. Wenn Sie Azure zu Ihrer Umgebung hinzufügen, sollten Sie diese Benennungsstandards für Azure-Ressourcen übernehmen. Benennungsstandards ermöglichen eine effizientere Umgebungsverwaltung auf allen Ebenen. Sie können Azure Policy als Tool verwenden, um für Ihre gesamte Azure-Umgebung Benennungsstandards durchzusetzen.

::: zone target="docs"

Wir empfehlen, den [Leitfaden mit Mustern und Verfahren](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) zu lesen und anzuwenden.

>[!TIP]
>Verwenden Sie möglichst keine Sonderzeichen (`-` oder `_`) als erstes oder letztes Zeichen eines Namens. Diese Zeichen führen bei den meisten Validierungsregeln zu einem Fehler.

::: zone-end

| Entität | `Scope` | Länge | Schreibweise | Gültige Zeichen | Vorgeschlagenes Muster | Beispiel |
| --- | --- | --- | --- | --- | --- | --- |
|Resource group |Subscription |1-90 |Groß-/Kleinschreibung nicht beachten |Alphanumerisch, Unterstrich, Klammern, Bindestrich, Punkt (außer am Ende) und Unicode-Zeichen |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Verfügbarkeitsgruppe |Resource group |1-80 |Groß-/Kleinschreibung nicht beachten |Alphanumerisch, Unterstrich und Bindestrich |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Tag |Zugeordnete Entität |512 (Name), 256 (Wert) |Groß-/Kleinschreibung nicht beachten |Alphanumerisch |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tagstabresourcetags"></a>[Ressourcentags](#tab/ResourceTags)

Tags sind nützlich, um Ihre Ressourcen und Ressourcengruppen schnell identifizieren zu können. Durch Anwenden von Tags können Sie Ihre Azure-Ressourcen logisch nach Kategorien organisieren. Jedes Tag besteht aus einem Namen und einem Wert. So können Sie beispielsweise den Namen „Umgebung“ und den Wert „Produktion“ auf alle Ressourcen in der Produktion anwenden.

Nach dem Anwenden von Tags können Sie alle Ressourcen in Ihrem Abonnement abrufen, die diesen Tagnamen und -wert besitzen. Mit Tags können Sie verwandte Ressourcen aus unterschiedlichen Ressourcengruppen abrufen. Dies ist beim Organisieren von Ressourcen für die Abrechnung oder Verwaltung hilfreich.

Sie können Tags auch für viele andere Dinge verwenden. Sie werden häufig für folgende Aufgaben genutzt:

- **Metadaten und Dokumentation**: Durch Anwenden eines Tags wie „ProjectOwner“ können Administratoren problemlos Details zu den Ressourcen anzeigen, an denen sie arbeiten.
- **Automatisierung**: Unter Umständen verfügen Sie über regelmäßig ausgeführte Skripts, die basierend auf einem Tagwert wie „ShutdownTime“ oder „DeprovisionDate“ eine Aktion durchführen können.
- **Abrechnung**: Tags können in Ihrer Rechnung angezeigt werden. Dadurch können Sie Ihre Rechnung beispielsweise mithilfe von Tags wie „CostCenter“ oder „BillTo“ segmentieren.

Jede Ressource oder Ressourcengruppe kann maximal 15 Tagname-Wert-Paare besitzen. Diese Einschränkung gilt jedoch nur für Tags, die direkt auf die Ressourcengruppe oder auf die Ressource angewendet werden.

Weitere Informationen zum Tagging finden Sie unter [Namenskonventionen für Azure-Ressourcen im Azure Architecture Center](../../ready/azure-best-practices/naming-and-tagging.md#metadata-tags).

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Anwenden eines Ressourcentags

So wenden Sie ein Tag auf eine Ressourcengruppe an:

1. Navigieren Sie zu [Ressourcengruppen](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Wählen Sie eine Ressourcengruppe aus.
1. Wählen Sie **Tags** aus.
1. Geben Sie einen neuen Namen und Wert ein, oder verwenden Sie die Dropdownliste, um einen bereits vorhandenen Namen und Wert auszuwählen.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter [Verwenden von Tags zum Organisieren von Azure-Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Aktion

**Anwenden eines Ressourcentags**:

So wenden Sie ein Tag auf eine Ressourcengruppe an:

1. Navigieren Sie zu **Ressourcengruppen**.
1. Wählen Sie eine Ressourcengruppe aus.
1. Wählen Sie **Tags** aus.
1. Geben Sie einen neuen Namen und Wert ein, oder wählen Sie einen bereits vorhandenen Namen und Wert aus.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups]" submitText="Go to resource groups" :::

::: zone-end
