---
title: Betriebsbezogene Compliance in Azure
description: Es wird beschrieben, wie Sie einen stabilen Geschäftsbetrieb durch die betriebsbezogene Compliance sicherstellen, indem Sie die Wahrscheinlichkeit von Ausfällen oder Sicherheitsrisiken verringern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 18c3c81fdd756e90e729387c7030c64e8a87a056
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356451"
---
<!-- cSpell:ignore WSUS -->

# <a name="operational-compliance-in-azure"></a>Betriebsbezogene Compliance in Azure

Die _betriebsbezogene Compliance_ ist die zweite Disziplin in jeder Cloudverwaltungsbaseline.

![Baseline zur Cloudverwaltung](../../_images/manage/management-baseline.png)

Durch das Verbessern der betriebsbezogenen Compliance reduziert sich die Wahrscheinlichkeit eines Ausfalls durch Konfigurationsabweichungen oder die Wahrscheinlichkeit von Sicherheitsrisiken durch nicht ordnungsgemäß gepatchte Systeme.

In dieser Tabelle wird für jede Umgebung auf Unternehmensniveau der empfohlene Mindestwert für eine Verwaltungsbaseline aufgeführt.

|Prozess  |Tool  |Zweck  |
|---------|---------|---------|
|Patchverwaltung|Updateverwaltung|Verwaltung und Zeitplanung von Updates|
|Durchsetzung von Richtlinien|Azure Policy|Richtliniendurchsetzung zum Sicherstellen der Compliance von Umgebung und Gastsystemen|
|Umgebungskonfiguration|Azure Blueprint|Automatisierte Compliance für Kerndienste|
|Ressourcenkonfiguration|Desired State Configuration|Automatisierte Konfiguration für das Gastbetriebssystem und einige Aspekte der Umgebung|

::: zone target="docs"

## <a name="update-management"></a>Updateverwaltung

::: zone-end
::: zone target="chromeless"

## <a name="update-management"></a>[Updateverwaltung](#tab/UpdateManagement)

::: zone-end

Verwenden Sie für Computer, die mit der Updateverwaltung verwaltet werden, die folgenden Konfigurationen, um Bewertungen und Updatebereitstellungen durchzuführen:

- Microsoft Monitoring Agent (MMA) für Windows oder Linux
- PowerShell Desired State Configuration (DSC) für Linux
- Azure Automation – Hybrid Runbook Worker
- Microsoft Update oder Windows Server Update Services (WSUS) für Windows-Computer

Weitere Informationen finden Sie unter [Updateverwaltungslösung](https://docs.microsoft.com/azure/automation/automation-update-management).

> [!WARNING]
> Bevor Sie die Updateverwaltung verwenden, müssen Sie virtuelle Computer oder ein ganzes Abonnement in Log Analytics und Azure Automation integrieren.
>
> Es gibt zwei Ansätze für das Onboarding:
>
> - [Einzelne VM](../../manage/azure-server-management/onboard-single-vm.md)
> - [Ganzes Abonnement](../../manage/azure-server-management/onboard-at-scale.md)
>
> Sie sollten einem folgen, bevor Sie mit der Updateverwaltung fortfahren.

### <a name="manage-updates"></a>Verwalten von Updates

So wenden Sie eine Richtlinie auf eine Ressourcengruppe an:

1. Wechseln Sie zu [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Wählen Sie **Automation-Konten** und dann eines der aufgeführten Konten aus.
1. Wechseln Sie zu **Konfigurationsverwaltung**.
1. **Inventar**, **Change Management** und **State Configuration** können zum Steuern des Zustands und der betriebsbezogenen Compliance der verwalteten VMs verwendet werden.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Azure Policy

::: zone-end
::: zone target="chromeless"

## <a name="azure-policy"></a>[Azure Policy](#tab/AzurePolicy)

::: zone-end

Azure Policy wird während der gesamten Governanceprozesse eingesetzt. Es ist auch in Cloudverwaltungsprozessen äußerst wertvoll. Mit Azure Policy können Sie Azure-Ressourcen überprüfen und korrigieren sowie Einstellungen auf einem Computer überprüfen. Für die Überprüfung verwenden Sie die Erweiterung und den Client Guest Configuration. Die Erweiterung überprüft über den Client u. a. die folgenden Einstellungen:

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

## <a name="azure-blueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

::: zone-end

Mit Azure Blueprints können Cloudarchitekten und zentrale IT-Gruppen einen wiederholbaren Satz von Azure-Ressourcen definieren. Diese Ressourcen implementieren die Standards, Muster und Anforderungen eines Unternehmens und halten diese ein.

Mit Azure Blueprints können Entwicklungsteams schnell neue Umgebungen erstellen und aufrüsten. Teams können sich auch darauf verlassen, dass die Erstellung im Rahmen der Compliance in Organisationen erfolgt. Dazu verwenden sie eine Reihe von integrierten Komponenten, z. B. Netzwerke, um die Entwicklung und Bereitstellung zu beschleunigen.

Blaupausen sind eine deklarative Möglichkeit zum Orchestrieren der Bereitstellung mehrerer Ressourcenvorlagen und anderer Artefakte wie etwa:

- Rollenzuweisungen.
- Richtlinienzuweisungen.
- Azure Resource Manager-Vorlagen.
- Ressourcengruppen.

Durch Anwenden einer Blaupause können Sie die betriebsbezogene Compliance in einer Umgebung durchsetzen, wenn diese Durchsetzung nicht vom Cloudgovernanceteam durchgeführt wird.

### <a name="create-a-blueprint"></a>Erstellen einer Blaupause

So erstellen Sie eine Blaupause

::: zone target="chromeless"

1. Wechseln Sie zu **Blaupausen – Erste Schritte**.
1. Wählen Sie im Bereich **Blaupause erstellen** die Option **Erstellen** aus.
1. Filtern Sie die Liste mit den Blaupausen, um die gewünschte Blaupause auszuwählen.
1. Geben Sie im Feld **Name der Blaupause** den Namen der Blaupause ein.
1. Wählen Sie **Speicherort der Definition** und dann den entsprechenden Speicherort aus.
1. Wählen Sie **Weiter: Artefakte >>** , und sehen Sie sich die Artefakte an, die in der Blaupause enthalten sind.
1. Wähen Sie **Entwurf speichern** aus.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Wechseln Sie zu [Blaupausen – Erste Schritte](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. Wählen Sie im Bereich **Blaupause erstellen** die Option **Erstellen** aus.
1. Filtern Sie die Liste mit den Blaupausen, um die gewünschte Blaupause auszuwählen.
1. Geben Sie im Feld **Name der Blaupause** den Namen der Blaupause ein.
1. Wählen Sie **Speicherort der Definition** und dann den entsprechenden Speicherort aus.
1. Wählen Sie **Weiter: Artefakte >>** , und sehen Sie sich die Artefakte an, die in der Blaupause enthalten sind.
1. Wähen Sie **Entwurf speichern** aus.

::: zone-end

### <a name="publish-a-blueprint"></a>Veröffentlichen einer Blaupause

So veröffentlichen Sie Blaupausenartefakte für Ihr Abonnement:

::: zone target="chromeless"

1. Wechseln Sie zu **Blaupausen > Blaupausendefinitionen**.
1. Wählen Sie die Blaupause aus, die Sie in den vorherigen Schritten erstellt haben.
1. Überprüfen Sie die Blaupausendefinition, und wählen Sie anschließend **Blaupause veröffentlichen** aus.
1. Geben Sie in das Feld **Version** eine Version wie „1.0“ ein.
1. Geben Sie im Feld **Änderungshinweise** Ihre Hinweise ein.
1. Wählen Sie **Veröffentlichen**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Wechseln Sie zu [Blaupausen > Blaupausendefinitionen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Wählen Sie die Blaupause aus, die Sie in den vorherigen Schritten erstellt haben.
1. Überprüfen Sie die Blaupausendefinition, und wählen Sie anschließend **Blaupause veröffentlichen** aus.
1. Geben Sie in das Feld **Version** eine Version wie „1.0“ ein.
1. Geben Sie im Feld **Änderungshinweise** Ihre Hinweise ein.
1. Wählen Sie **Veröffentlichen**.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Cloud Adoption Framework: Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz](../../decision-guides/resource-consistency/index.md)
- [Standardbasierte Blaupausenbeispiele](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
