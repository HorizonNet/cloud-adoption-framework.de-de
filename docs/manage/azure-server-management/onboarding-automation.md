---
title: Automatisieren des Onboardings
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Automatisieren des Onboardings
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f5dd418a03dd35ebced1a9c73eb8fe6567339859
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565395"
---
# <a name="automate-onboarding"></a>Automatisieren des Onboardings

Um die Effizienz der Bereitstellung von Azure-Serververwaltungsdiensten zu verbessern, sollten Sie die Automatisierung der Bereitstellung in Betracht ziehen, wie in den vorangegangenen Abschnitten dieser Anleitung beschrieben. Das Skript und die in den folgenden Abschnitten bereitgestellten Beispielvorlagen sind Ausgangspunkte für die Entwicklung eigener automatisierter Onboardingprozesse.

Dieser Leitfaden enthält ein unterstützendes GitHub-Repository mit Beispielcode, [CloudAdoptionFramework](https://aka.ms/caf/manage/automation-samples). Das Repository enthält Beispielskripts und Azure Resource Manager-Vorlagen, die Ihnen bei der Automatisierung der Bereitstellung von Azure-Serververwaltungsdiensten helfen.

Die Beispieldateien veranschaulichen, wie Sie Azure PowerShell-Cmdlets verwenden können, um folgende Aufgaben zu automatisieren:

- Erstellen Sie einen [Log Analytics-Arbeitsbereich](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access). (Oder verwenden Sie einen vorhandenen Arbeitsbereich, wenn er den Anforderungen entspricht. Weitere Informationen finden Sie unter [Arbeitsbereichsplanung](./prerequisites.md#log-analytics-workspace-and-automation-account-planning).)

- Erstellen Sie ein Automation-Konto. (Oder verwenden Sie ein vorhandenes Konto, wenn es den Anforderungen entspricht. Weitere Informationen finden Sie unter [Arbeitsbereichsplanung](./prerequisites.md#log-analytics-workspace-and-automation-account-planning).)

- Verknüpfen Sie das Automation-Konto mit dem Log Analytics-Arbeitsbereich. Dieser Schritt ist beim Onboarding über das Azure-Portal nicht erforderlich.

- Aktivieren Sie die Updateverwaltung und die Änderungsnachverfolgung sowie die Inventarisierung für den Arbeitsbereich.

- Führen Sie das Onboarding für virtuelle Azure-Computer unter Verwendung von Azure Policy durch. Eine Richtlinie installiert den Log Analytics- und den Microsoft Dependency-Agent auf den virtuellen Azure-Computern.

- Führen Sie das Onboarding auf lokalen Servern durch, indem Sie den Log Analytics-Agent auf ihnen installieren.

In diesem Beispiel werden die in der folgenden Tabelle beschriebenen Dateien verwendet. Sie können sie so anpassen, dass sie Ihre eigenen Bereitstellungsszenarien unterstützen.

| Dateiname | BESCHREIBUNG |
|-----------|-------------|
| New-AMSDeployment.ps1 | Das hauptsächliche Orchestrierungsskript, das das Onboarding automatisiert. Es erstellt Ressourcengruppen und Standort-, Arbeitsbereichs- und Automation-Konten, falls diese noch nicht vorhanden sind. Dieses PowerShell-Skript erfordert ein bestehendes Abonnement. |
| Workspace-AutomationAccount.json | Eine Resource Manager-Vorlage, die die Ressourcen des Arbeitsbereichs und des Automatisierungskontos bereitstellt. |
| WorkspaceSolutions.json | Eine Resource Manager-Vorlage, die Ihre gewünschten Lösungen im Log Analytics-Arbeitsbereich ermöglicht. |
| ScopeConfig.json | Eine Resource Manager-Vorlage, die das Abonnementmodell für lokale Server mit der Lösung zur Änderungsnachverfolgung verwendet. Die Verwendung des Abonnementmodells ist optional. |
| Enable-VMInsightsPerfCounters.ps1 | Ein PowerShell-Skript, das VM Insights für Server aktiviert und Leistungsindikatoren konfiguriert. |
| ChangeTracking-Filelist.json | Eine Resource Manager-Vorlage, die die Liste der Dateien definiert, die von der Änderungsnachverfolgung überwacht werden. |

Verwenden Sie den folgenden Befehl, um „New-AMSDeployment.ps1“ auszuführen:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie grundlegende Warnungen einrichten, um Ihr Team über wichtige Managementereignisse und -probleme zu informieren.

> [!div class="nextstepaction"]
> [Einrichten einfacher Warnungen](./setup-alerts.md)
