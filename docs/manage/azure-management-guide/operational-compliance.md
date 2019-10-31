---
title: Betriebsbezogene Compliance in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Gewährleistung von Geschäftsstabilität durch die Steigerung der betriebsbezogenen Compliance
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7073df6b697da49429d4086d9f8f3f113583e52d
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557090"
---
# <a name="operational-compliance-in-azure"></a>Betriebsbezogene Compliance in Azure

Die betriebsbezogene Compliance ist die zweite Disziplin in jeder Cloudverwaltungsbaseline.

![Baseline zur Cloudverwaltung](../../_images/manage/management-baseline.png)

Durch das Verbessern der betriebsbezogenen Compliance reduziert sich die Wahrscheinlichkeit eines Ausfalls durch Konfigurationsabweichungen oder die Wahrscheinlichkeit von Sicherheitsrisiken durch nicht ordnungsgemäß gepatchte Systeme.

In der folgenden Tabelle wird für jede Umgebung auf Unternehmensniveau der empfohlene Mindestwert für die einzelnen Verwaltungsbaselines aufgeführt.

|Prozess  |Tool  |Zweck  |
|---------|---------|---------|
|Patchverwaltung|Updateverwaltung|Verwaltung und Zeitplanung von Updates|
|Durchsetzung von Richtlinien|Azure Policy|Richtliniendurchsetzung zum Sicherstellen der Compliance von Umgebung und Gastsystemen|
|Umg.- Konfiguration|Azure Blueprint|Automatisierte Compliance für Kerndienste|

::: zone target="docs"

## <a name="update-management"></a>Updateverwaltung

::: zone-end
::: zone target="chromeless"

## <a name="update-managementtabupdatemanagement"></a>[Updateverwaltung](#tab/UpdateManagement)

::: zone-end

Verwenden Sie für Computer, die mit der Updateverwaltung verwaltet werden, die folgenden Konfigurationen, um Bewertungen und Updatebereitstellungen durchzuführen:

- Microsoft Monitoring Agent (MMA) für Windows oder Linux
- PowerShell Desired State Configuration (DSC) für Linux
- Automation Hybrid Runbook Worker
- Microsoft Update oder Windows Server Update Services (WSUS) für Windows-Computer

Weitere Informationen finden Sie unter [Updateverwaltungslösung](https://docs.microsoft.com/azure/automation/automation-update-management).

> [!WARNING]
> Bevor Sie die Updateverwaltung verwenden, müssen Sie VMs oder ein ganzes Abonnement in Log Analytics und Azure Automation integrieren.
> Es gibt zwei Ansätze für das Onboarding; einer davon muss befolgt werden, bevor Sie mit der Updateverwaltung fortfahren.
>
> - [Einzelne VM](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
> - [Ganzes Abonnement](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)

### <a name="manage-updates"></a>Verwalten von Updates

So wenden Sie eine Richtlinie auf eine Ressourcengruppe an:

1. Wechseln Sie zu [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Wählen Sie eines der aufgelisteten **Automation-Konten** aus.
3. Suchen Sie in der Portalnavigation den Abschnitt **Konfigurationsverwaltung**.
4. „Inventar“, „Change Management“ und „State Configuration“ können jeweils zum Steuern des Zustands und der betriebsbezogenen Compliance der verwalteten VMs verwendet werden.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Azure Policy

::: zone-end
::: zone target="chromeless"

## <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

::: zone-end

Azure Policy wird während der gesamten Governanceprozesse eingesetzt. Es ist jedoch auch in Cloudverwaltungsprozessen äußerst wertvoll. Mit Azure Policy können Sie nicht nur Azure-Ressourcen überprüfen und korrigieren, sondern auch die Einstellungen auf einem Computer überprüfen. Für die Überprüfung verwenden Sie die Erweiterung und den Client Guest Configuration. Die Erweiterung überprüft über den Client u. a. die folgenden Einstellungen:

- Betriebssystemkonfiguration
- Die Konfiguration oder das Vorhandensein der Anwendung
- Umgebungseinstellungen

Derzeit führt die Azure Policy-Gastkonfiguration nur eine Überprüfung der Einstellungen auf dem Computer durch. Es werden keine Konfigurationen angewandt.

::: zone target="chromeless"

### <a name="action"></a>Aktion

Weisen Sie einer Verwaltungsgruppe, einem Abonnement oder einer Ressourcengruppe eine integrierte Richtlinie zu.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

### <a name="apply-a-policy"></a>Anwenden einer Richtlinie

So wenden Sie eine Richtlinie auf eine Ressourcengruppe an:

1. Wechseln Sie zu [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Wählen Sie **Richtlinie zuweisen**.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Azure Policy: Gastkonfiguration](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration)
- [Cloud Adoption Framework: Leitfaden zur Entscheidungsfindung für die Richtlinienerzwingung](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprint

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

::: zone-end

Azure Blueprints ermöglicht es Cloudarchitekten und zentralen IT-Gruppen, eine wiederholbare Gruppe von Azure-Ressourcen zu definieren, mit der die Standards, Muster und Anforderungen einer Organisation implementiert und erzwungen werden. Azure Blueprints ermöglicht es Entwicklungsteams, schnell neue Umgebungen zu erstellen und einzurichten und darauf zu vertrauen, dass sie im Rahmen der organisatorischen Compliance mithilfe einer Reihe von integrierten Komponenten (z.B. dem Netzwerk) arbeiten, um die Entwicklung und Bereitstellung zu beschleunigen.

Blaupausen sind eine deklarative Möglichkeit zum Orchestrieren der Bereitstellung mehrerer Ressourcenvorlagen und anderer Artefakte wie etwa:

- Rollenzuweisungen.
- Richtlinienzuweisungen.
- Azure Resource Manager-Vorlagen.
- Ressourcengruppen.

Durch Anwenden einer Blaupause können Sie die betriebsbezogene Compliance in einer Umgebung durchsetzen, falls dies noch nicht vom Cloudgovernanceteam übernommen wurde.

### <a name="create-a-blueprint"></a>Erstellen einer Blaupause

So erstellen Sie eine Blaupause

::: zone target="chromeless"

1. Wechseln Sie zu **Blaupausen – Erste Schritte**.
1. Wählen Sie im Abschnitt **Blaupause erstellen** die Option **Erstellen** aus.
1. Filtern Sie die Liste mit den Blaupausen, um die gewünschte Blaupause auszuwählen.
1. Geben Sie unter **Name der Blaupause** den Namen ein, und wählen Sie den entsprechenden **Definitionsspeicherort** aus.
1. Klicken Sie unten auf der Seite auf **Weiter: Artefakte >>** , und sehen Sie sich die Artefakte an, die in der Blaupause enthalten sind.
1. Klicken Sie auf **Entwurf speichern**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Wechseln Sie zu [Blaupausen – Erste Schritte](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. Wählen Sie im Abschnitt **Blaupause erstellen** die Option **Erstellen** aus.
1. Filtern Sie die Liste mit den Blaupausen, um die gewünschte Blaupause auszuwählen.
1. Geben Sie unter **Name der Blaupause** den Namen ein, und wählen Sie den entsprechenden **Definitionsspeicherort** aus.
1. Klicken Sie unten auf der Seite auf **Weiter: Artefakte >>** , und sehen Sie sich die Artefakte an, die in der Blaupause enthalten sind.
1. Klicken Sie auf **Entwurf speichern**.

::: zone-end

### <a name="publish-a-blueprint"></a>Veröffentlichen einer Blaupause

So veröffentlichen Sie Blaupausenartefakte für Ihr Abonnement:

::: zone target="chromeless"

1. Wechseln Sie zu **Blaupausen > Blaupausendefinitionen**.
1. Wählen Sie die Blaupause aus, die Sie in den vorherigen Schritten erstellt haben.
1. Sehen Sie sich die Blaupausendefinition an, und wählen Sie die Option **Blaupause veröffentlichen**.
1. Geben Sie eine **Version** (z. B. „1.0“) sowie **Änderungshinweise** an, und wählen Sie anschließend **Veröffentlichen** aus.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Wechseln Sie zu [Blaupausen > Blaupausendefinitionen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Wählen Sie die Blaupause aus, die Sie in den vorherigen Schritten erstellt haben.
1. Sehen Sie sich die Blaupausendefinition an, und wählen Sie die Option **Blaupause veröffentlichen**.
1. Geben Sie eine **Version** (z. B. „1.0“) sowie **Änderungshinweise** an, und wählen Sie anschließend **Veröffentlichen** aus.

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Cloud Adoption Framework: Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz](../../decision-guides/resource-consistency/index.md)
- [Standardbasierte Blaupausenbeispiele](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
