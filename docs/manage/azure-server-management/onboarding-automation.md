---
title: Automatisieren des Onboardings und der Warnungskonfiguration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Automatisieren des Onboardings und der Warnungskonfiguration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 242c8a1a054507c3b1134b1126ea95e3ead74d84
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221373"
---
# <a name="automate-onboarding"></a>Automatisieren des Onboardings

Um die Effizienz der Bereitstellung von Azure-Serververwaltungsdiensten zu verbessern, sollten Sie die Bereitstellung von Verwaltungsdiensten mithilfe der in den vorangegangenen Abschnitten dieser Anleitung beschriebenen Empfehlungen automatisieren. Das Skript und die in den folgenden Abschnitten bereitgestellten Beispielvorlagen sind Ausgangspunkte für die Entwicklung eigener automatisierter Onboardingprozesse.

## <a name="onboarding-by-using-automation"></a>Durchführen des Onboardings mithilfe der Automatisierung

Dieser Leitfaden enthält ein unterstützendes GitHub-Repository mit Beispielcode, [CloudAdoptionFramework](https://aka.ms/caf/manage/automation-samples), das Beispielskripte und Azure Resource Manager-Vorlagen enthält, die Ihnen bei der Automatisierung der Bereitstellung von Azure-Serververwaltungsdiensten helfen.

Diese Beispieldateien veranschaulichen, wie Sie Azure PowerShell-Cmdlets verwenden können, um folgende Aufgaben zu automatisieren:

1. Erstellen Sie einen [Log Analytics-Arbeitsbereich](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access) (oder verwenden Sie einen vorhandenen Arbeitsbereich, wenn er den Anforderungen entspricht&mdash;siehe [Arbeitsbereichsplanung](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

2. Erstellen Sie ein Automatisierungskonto (oder verwenden Sie ein bestehendes Konto, wenn es die Anforderungen erfüllt&mdash;siehe [Arbeitsbereichsplanung](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

3. Verknüpfen Sie das Automatisierungskonto mit dem Log Analytics-Arbeitsbereich (nicht erforderlich, wenn das Onboarding über das Portal durchgeführt wird).

4. Aktivieren Sie die Updateverwaltung und die Änderungsnachverfolgung sowie die Inventarisierung für den Arbeitsbereich.

5. Führen Sie das Onboarding für virtuelle Azure-Computer unter Verwendung von Azure Policy durch. (Eine Richtlinie installiert den Log Analytics- und den Dependency-Agent auf den virtuellen Azure-Computern.)

6. Führen Sie das Onboarding auf lokalen Servern durch, indem Sie den Log Analytics-Agent auf ihnen installieren.

Die in der folgenden Tabelle beschriebenen Dateien werden in diesem Beispiel verwendet und können angepasst werden, um Ihre eigenen Bereitstellungsszenarien zu unterstützen.

| Dateiname | BESCHREIBUNG |
|-----------|-------------|
| New-AMSDeployment.ps1 | Das hauptsächliche Orchestrierungsskript, das das Onboarding automatisiert. Dieses PowerShell-Skript erfordert ein bestehendes Abonnement, erstellt aber Ressourcengruppen, Standorte, Arbeitsbereiche und Automatisierungskonten, wenn sie nicht vorhanden sind. |
| Workspace-AutomationAccount.json | Eine Resource Manager-Vorlage, die die Ressourcen des Arbeitsbereichs und des Automatisierungskontos bereitstellt. |
| WorkspaceSolutions.json | Eine Resource Manager-Vorlage, die Ihre gewünschten Lösungen im Log Analytics-Arbeitsbereich ermöglicht. |
| ScopeConfig.json | Eine Resource Manager-Vorlage, die das Abonnementmodell für lokale Server mit der Lösung zur Änderungsnachverfolgung verwendet. Die Verwendung des Abonnementmodells ist optional. |
| Enable-VMInsightsPerfCounters.ps1 | Ein PowerShell-Skript, das VMInsight für Server aktiviert und Leistungsindikatoren konfiguriert. |
| ChangeTracking-Filelist.json | Eine Resource Manager-Vorlage, die die Liste der Dateien definiert, die von der Änderungsnachverfolgung überwacht werden. |

Sie können „New-AMSDeployment.ps1“ mit dem folgenden Befehl ausführen:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie grundlegende Warnungen einrichten, um Ihr Team über wichtige Managementereignisse und -probleme zu informieren.

> [!div class="nextstepaction"]
> [Einrichten einfacher Warnungen](./setup-alerts.md)
