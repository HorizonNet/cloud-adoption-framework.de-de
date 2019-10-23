---
title: Governance, Sicherheit und Konformität in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Es wird beschrieben, wie Sie Governance, Sicherheit und Konformität für Ihre Azure-Umgebung einrichten.
author: tvuylsteke
ms.author: kfollis
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: e4ba8670954371e58b688c36e6623f27708be3ef
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548938"
---
# <a name="governance-security-and-compliance-in-azure"></a>Governance, Sicherheit und Konformität in Azure

Wenn Sie Unternehmensrichtlinien festlegen und Ihre Governancestrategien planen, können Sie Tools und Dienste wie Azure Policy, Azure Blueprints und Azure Security Center verwenden, um die Governanceentscheidungen Ihres Unternehmens durchzusetzen und zu automatisieren. Verwenden Sie vor Beginn Ihrer Governanceplanung das [Governancebenchmarktool](https://cafbaseline.com), um potenzielle Lücken im Cloudgovernanceansatz Ihres Unternehmens zu identifizieren. Weitere Informationen zur Entwicklung von Governanceprozessen finden Sie im [Azure-Governanceleitfaden des Cloud Adoption Framework](../../govern/index.md).

# <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprint](#tab/AzureBlueprints)

Azure Blueprints ermöglicht es Cloudarchitekten und zentralen IT-Gruppen, eine wiederholbare Gruppe von Azure-Ressourcen zu definieren, mit der die Standards, Muster und Anforderungen einer Organisation implementiert und erzwungen werden. Azure Blueprints ermöglicht es Entwicklungsteams, schnell neue Umgebungen zu erstellen und einzurichten und darauf zu vertrauen, dass sie im Rahmen der organisatorischen Compliance mithilfe einer Reihe von integrierten Komponenten (z.B. dem Netzwerk) arbeiten, um die Entwicklung und Bereitstellung zu beschleunigen.

Blaupausen sind eine deklarative Möglichkeit zum Orchestrieren der Bereitstellung mehrerer Ressourcenvorlagen und anderer Artefakte wie etwa:

- Rollenzuweisungen.
- Richtlinienzuweisungen.
- Azure Resource Manager-Vorlagen.
- Ressourcengruppen.

## <a name="create-a-blueprint"></a>Erstellen einer Blaupause

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

## <a name="publish-a-blueprint"></a>Veröffentlichen einer Blaupause

Veröffentlichen Sie wie folgt ein Blaupausenartefakt für Ihr Abonnement:

::: zone target="chromeless"

1. Wechseln Sie zu **Blaupausen > Blaupausendefinitionen**.
1. Wählen Sie die Blaupause aus, die Sie in den vorherigen Schritten erstellt haben.
1. Sehen Sie sich die Blaupausendefinition an, und wählen Sie die Option **Blaupause veröffentlichen**.
1. Geben Sie eine **Version** (z. B. _1.0_) sowie **Änderungshinweise** an, und wählen Sie anschließend **Veröffentlichen** aus.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Wechseln Sie zu [Blaupausen > Blaupausendefinitionen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Wählen Sie die Blaupausendefinition aus, die Sie in den vorherigen Schritten erstellt haben.
1. Sehen Sie sich die Blaupausendefinition an, und wählen Sie die Option **Blaupause veröffentlichen**.
1. Geben Sie eine **Version** (z. B. _1.0_) sowie **Änderungshinweise** an, und wählen Sie anschließend **Veröffentlichen** aus.

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints)
- [Cloud Adoption Framework: Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz](../../decision-guides/resource-consistency/index.md)
- [Standardbasierte Blaupausenbeispiele](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end

# <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

Azure Policy ist ein Dienst, mit dem Sie Richtlinien erstellen, zuweisen und verwalten können. Mit diesen Richtlinien werden unterschiedliche Regeln für Ihre Ressourcen erzwungen, damit diese stets mit Ihren Unternehmensstandards und Vereinbarungen zum Servicelevel konform bleiben. Mit Azure Policy werden Ihre Ressourcen gescannt, um diejenigen zu ermitteln, die nicht mit den von Ihnen implementierten Richtlinien konform sind. Sie können beispielsweise über eine Richtlinie verfügen, die in Ihrer Umgebung nur die Ausführung einer bestimmten VM-Größe zulässt. Wenn Sie diese Richtlinie implementieren, werden damit bereits vorhandene virtuelle Computer in Ihrer Umgebung sowie alle neu bereitgestellten virtuellen Computer ausgewertet. Bei der Richtlinienauswertung werden Konformitätsereignisse generiert, die Sie für die Überwachung und Berichterstellung verwenden können.

Ziehen Sie allgemeine Richtlinien für die folgenden Aufgaben in Betracht:

- Erzwingen von Tags für Ressourcen und Ressourcengruppen
- Einschränken von Regionen für bereitgestellte Ressourcen
- Einschränken von teuren SKUs für spezielle Ressourcen
- Überwachen der Nutzung wichtiger optionaler Features, z. B. verwaltete Azure-Datenträger

::: zone target="chromeless"

## <a name="action"></a>Aktion

Weisen Sie einer Verwaltungsgruppe, einem Abonnement oder einer Ressourcengruppe eine integrierte Richtlinie zu.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

## <a name="apply-a-policy"></a>Anwenden einer Richtlinie

So wenden Sie eine Richtlinie auf eine Ressourcengruppe an:

1. Wechseln Sie zu [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Wählen Sie **Richtlinie zuweisen**.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Cloud Adoption Framework: Leitfaden zur Entscheidungsfindung für die Richtlinienerzwingung](../../decision-guides/policy-enforcement/index.md)

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center ist eine wichtige Komponente Ihrer Governancestrategie. Sie unterstützt Ihre Sicherheit aus den folgenden Gründen optimal:

- Einheitliche Sicherheitsübersicht über Ihre Workloads
- Erfassen, Durchsuchen und Analysieren von Sicherheitsdaten aus verschiedensten Quellen, z.B. Firewalls und anderen Partnerlösungen.
- Umsetzbare Sicherheitsempfehlungen, um Schwachstellen zu beheben, bevor diese ausgenutzt werden können
- Kann für die Anwendung von Sicherheitsrichtlinien auf Ihre gesamten Hybrid Cloud-Workloads genutzt werden, um Konformität mit Sicherheitsstandards sicherzustellen.

Viele Sicherheitsfeatures, z. B. Sicherheitsrichtlinie und Empfehlungen, sind kostenlos verfügbar. Einige der anspruchsvolleren Features wie Just-in-Time-VM-Zugriff und Unterstützung von Hybrid-Workloads sind unter dem Standard-Tarif für Security Center verfügbar. Mit dem Just-in-Time-VM-Zugriff lässt sich die Angriffsfläche des Netzwerks verkleinern, indem der Zugriff auf Verwaltungsports virtueller Azure-Computer kontrolliert wird.

> [!TIP]
> Das Azure Security Center ist standardmäßig in jedem Abonnement aktiviert. Wir empfehlen Ihnen, die Datensammlung von virtuellen Computern zu aktivieren, damit Azure Security Center den Agent installieren und mit dem Erfassen von Daten beginnen kann.

::: zone target="docs"

Wechseln Sie zum [Azure-Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0), um Azure Security Center zu erkunden.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Azure Security Center](https://docs.microsoft.com/azure/security-center)
- [Just-in-Time-VM-Zugriff](https://docs.microsoft.com/azure/security-center/security-center-just-in-time#how-does-just-in-time-access-work)
- [Vergleich: Standard- und Free-Tarif](https://azure.microsoft.com/pricing/details/security-center)
- [Cloud Adoption Framework: Governancedisziplin „Sicherheitsbaseline“](../../govern/security-baseline/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Aktion

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end
