---
title: Erforderliche Planung für Azure-Serververwaltungsdienste
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erforderliche Tools und Planung für Azure-Serververwaltungsdienste
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a684880537fa4dc2d7a56e93b9a6e35a94425dae
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834660"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Phase 1: Erforderliche Planung für Azure-Serververwaltungsdienste

In dieser Phase lernen Sie die Suite mit Diensten für die Azure-Serververwaltung kennen und planen die Bereitstellung der für die Implementierung dieser Verwaltungslösungen erforderlichen Ressourcen.

## <a name="understand-the-tools-and-services"></a>Grundlegendes zu den Tools und Diensten

In [Azure-Serververwaltungstools und -dienste](./tools-services.md) finden Sie eine detaillierte Übersicht über die Verwaltungsbereiche, die an laufenden Azure-Vorgängen beteiligt sind, und die Azure-Dienste und -Tools, die Sie in diesen Bereichen unterstützen. Mehrere dieser Dienste müssen zusammen verwendet werden, um Ihre Verwaltungsanforderungen zu erfüllen. Auf diese Tools wird in diesem Leitfaden häufig verwiesen.

In den folgenden Abschnitten wird die erforderliche Planung und Vorbereitung der Verwendung dieser Tools und Dienste erläutert.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Planung des Log Analytics-Arbeitsbereichs und Automation-Kontos

Viele der Dienste, die Sie für das Onboarding der Azure-Verwaltungsdienste nutzen werden, erfordern einen Log Analytics-Arbeitsbereich und ein verknüpftes Azure Automation-Konto.

Ein [Log Analytics-Arbeitsbereich](/azure/azure-monitor/learn/quick-create-workspace) ist eine spezifische Umgebung für das Speichern von Azure Monitor-Protokolldaten. Jeder Arbeitsbereich verfügt über ein eigenes Datenrepository und eine eigene Konfiguration. Datenquellen und Lösungen sind so konfiguriert, dass sie ihre Daten in bestimmten Arbeitsbereichen speichern. Azure-Überwachungslösungen erfordern, dass alle Server mit einem Arbeitsbereich verbunden sind, damit ihre Protokolldaten gespeichert und abgerufen werden können.

Einige der Verwaltungsdienste erfordern ein [Azure Automation-Konto](/azure/automation/automation-intro). Mit diesem Konto und den Funktionen von Azure Automation können Sie Azure-Dienste und andere öffentliche Systeme integrieren, um Ihre Serververwaltungsprozesse bereitzustellen, zu konfigurieren und zu verwalten.

Die folgenden Azure-Serververwaltungsdienste erfordern einen verknüpften Log Analytics-Arbeitsbereich und ein Automation-Konto, um zu funktionieren:

- [Azure-Updateverwaltung](/azure/automation/automation-update-management)
- [Änderungsnachverfolgung und Bestand](/azure/automation/change-tracking)
- [Hybrid-Runbook-Worker](/azure/automation/automation-hybrid-runbook-worker)
- [Desired State Configuration](/azure/virtual-machines/extensions/dsc-overview)

Die zweite Phase dieses Leitfadens konzentriert sich auf die Bereitstellung von Diensten und Automatisierungsskripten. Es zeigt Ihnen, wie Sie einen Log Analytics-Arbeitsbereich und ein Automation-Konto erstellen. In diesem Leitfaden erfahren Sie auch, wie Sie mithilfe von Azure Policy sicherstellen, dass neue virtuelle Computer mit dem richtigen Arbeitsbereich verbunden sind.

Bei den in diesem Leitfaden behandelten Beispiele wird von einer Bereitstellung ausgegangen, bei der noch keine Server in der Cloud bereitgestellt sind. Weitere Informationen zu den Prinzipien und Überlegungen bei der Planung Ihrer Arbeitsbereiche finden Sie unter [Verwalten von Protokolldaten und Arbeitsbereichen in Azure Monitor](/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Überlegungen zur Planung

Beachten Sie bei der Vorbereitung der Arbeitsbereiche und Konten, die Sie für das Onboarding von Verwaltungsdiensten erstellen, die folgenden Themen zu Problemen:

- **Azure-Geografien und Einhaltung gesetzlicher Bestimmungen**. Azure-Regionen sind in *Geografien* unterteilt. Eine [Azure-Geografie](https://azure.microsoft.com/global-infrastructure/geographies/) sorgt dafür, dass Anforderungen an Datenresidenz, Datenhoheit, Compliance und Ausfallsicherheit innerhalb geografischer Grenzen erfüllt werden. Wenn Ihre Workloads der Datenhoheit oder anderen Compliance-Anforderungen unterliegen, müssen der Arbeitsbereich und die Automation-Konten in Regionen innerhalb derselben Azure-Geographie wie die Workloadressourcen bereitgestellt werden, die sie unterstützen.
- **Anzahl von Arbeitsbereichen**. Als ein Leitprinzip erstellen Sie die minimale Anzahl von Arbeitsbereichen, die pro Azure-Geografie erforderlich sind. Es wird mindestens ein Arbeitsbereich für jede Azure-Geographie empfohlen, in der sich Ihre Compute- oder Speicherressourcen befinden. Diese erste Ausrichtung trägt dazu bei, künftige regulatorische Probleme bei der Migration von Daten in verschiedene Geografien zu vermeiden.
- **Datenaufbewahrung und Obergrenzen**. Möglicherweise müssen Sie beim Erstellen von Arbeitsbereichen oder Automation-Konten auch Datenaufbewahrungsrichtlinien oder Anforderungen an die Datenobergrenze berücksichtigen. Weitere Informationen zu diesen Prinzipien und zusätzliche Überlegungen bei der Planung Ihrer Arbeitsbereiche finden Sie unter [Verwalten von Protokolldaten und Arbeitsbereichen in Azure Monitor](/azure/azure-monitor/platform/manage-access).
- **Regionszuordnung**. Das Verknüpfen eines Log Analytics-Arbeitsbereich und eines Azure Automation-Kontos wird nur zwischen bestimmten Azure-Regionen unterstützt. Wenn beispielsweise der Log Analytics-Arbeitsbereich in der Region *EastUS* gehostet wird, muss das verknüpfte Automation-Konto in der Region *EastUS2* erstellt werden, um mit Verwaltungsdiensten verwendet zu werden. Wenn Sie über ein Automation-Konto verfügen, das in einer anderen Regionen erstellt wurde, kann dafür keine Verknüpfung mit einem Arbeitsbereich in *EastUS* (USA, Osten) erstellt werden. Die Wahl der Bereitstellungsregion kann die Anforderungen an die Azure-Geografie erheblich beeinflussen. Entscheiden Sie mithilfe der [Regionszuordnungstabelle](/azure/automation/how-to/region-mappings), welche Region Ihre Arbeitsbereiche und Automation-Konten hosten soll.
- **Multihoming für Arbeitsbereiche**. Der Log Analytics-Agent unterstützt Multihoming in einigen Szenarien, für den Agent gelten jedoch mehrere Einschränkungen und Probleme, wenn er in dieser Konfiguration ausgeführt wird. Sofern Microsoft die Verwendung von Multihoming für Ihr Szenario nicht empfohlen hat, raten wir von der Konfiguration von Multihoming auf dem Log Analytics-Agent ab.

## <a name="resource-placement-examples"></a>Beispiele für die Platzierung von Ressourcen

Es gibt mehrere verschiedene Modelle für die Auswahl des Abonnements, in dem Sie den Log Analytics-Arbeitsbereich und das Automation-Konto platzieren. Kurz gesagt: Sie sollten den Arbeitsbereichs und die Automation-Konten in ein Abonnement platzieren, das dem Team gehört, das für die Implementierung der Updateverwaltungs-, Änderungsnachverfolgungs- und Inventurdienste verantwortlich ist.

Die folgenden Beispiele veranschaulichen einige Möglichkeiten für die Bereitstellung von Arbeitsbereichen und Automation-Konten.

### <a name="placement-by-geography"></a>Platzierung nach Geografie

Für kleine und mittlere Umgebungen mit einem einzigen Abonnement und mehreren hundert Ressourcen über mehrere Azure-Geografien hinweg erstellen Sie in jeder Geografie einen Log Analytics-Arbeitsbereich und ein Azure Automation-Konto.

Sie können in jeder Ressourcengruppe ein Paar aus Arbeitsbereich und Azure Automation-Konto erstellen und dieses Paar in der entsprechenden Geografie für die virtuellen Computer bereitstellen. Wenn Ihre Richtlinien zur Datenkonformität nicht vorschreiben, dass sich die Ressourcen in bestimmten Regionen befinden, können Sie alternativ ein Paar zur Verwaltung aller virtuellen Computer erstellen. Es wird außerdem empfohlen, die Paare aus Arbeitsbereich und Automation-Konto in getrennten Ressourcengruppen zu platzieren, um eine präzisere rollenbasierte Zugriffssteuerung (RBAC) zu ermöglichen.

Das Beispiel im folgenden Diagramm enthält ein Abonnement mit zwei Ressourcengruppen, die sich jeweils in einer anderen Geografie befinden.

![Arbeitsbereichsmodell für kleine bis mittlere Umgebungen](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Platzierung in einem Verwaltungsabonnement

Für größere Umgebungen, die mehrere Abonnements umfassen und über eine zentrale IT-Abteilung verfügen, die für die Überwachung und Compliance zuständig ist, erstellen Sie Paare aus Arbeitsbereich und Automation-Konto in einem IT-Verwaltungsabonnement. In diesem Modell speichern VM-Ressourcen in einer Geografie ihre Daten im Arbeitsbereich der entsprechenden Geografie im IT-Verwaltungsabonnement. Anwendungsteams, die Automatisierungsaufgaben ausführen müssen, aber keine Verknüpfung von Arbeitsbereich und Automation-Konto benötigen, können ein separates Automation-Konto ihren eigenen Anwendungsabonnements erstellen.

![Arbeitsbereichsmodell für große Umgebungen](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Dezentralisierte Platzierung

In einem alternativen Modell für große Umgebungen kann die Verantwortung für die Anwendung von Patches und die Verwaltung beim Anwendungsentwicklerteam liegen. In diesem Fall sollten Sie die Arbeitsbereich- und Automation-Konto-Paare in den Abonnements des Anwendungsteams neben den anderen Ressourcen platzieren.

  ![Arbeitsbereich-Konto-Modell für dezentrale Umgebungen](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Erstellen eines Arbeitsbereichs und Automation-Kontos

Nachdem Sie entschieden haben, wie Arbeitsbereich-Konto-Paare am besten platziert und organisiert werden, müssen Sie sicherstellen, dass Sie diese Ressourcen erstellt haben, bevor Sie mit dem Onboardingprozess beginnen. In den Automation-Beispielen weiter unten in diesem Leitfaden wird ein Paar aus einem Arbeitsbereich und einem Automation-Konto für Sie erstellt. Wenn Sie jedoch nicht über ein vorhandenes Paar aus Arbeitsbereich und Automation-Konto verfügen, müssen Sie eines erstellen, wenn Sie das Onboarding über das Portal durchführen möchten.

Informationen zum Erstellen eines Log Analytics-Arbeitsbereichs über das Azure-Portal finden Sie unter [Erstellen eines Arbeitsbereichs](/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). Erstellen Sie anschließend ein entsprechendes Automation-Konto für jeden Arbeitsbereich, indem Sie die Schritte in [Erstellen eines Azure Automation-Kontos](/azure/automation/automation-quickstart-create-account) ausführen.

> [!NOTE]
> Wenn Sie ein Automation-Konto über das Azure-Portal erstellen, wird standardmäßig versucht, ausführende Konten sowohl für Ressourcen des Azure Resource Manager-Bereitstellungsmodells als auch des klassischen Bereitstellungsmodells zu erstellen. Wenn Sie keine klassischen virtuellen Computer in Ihrer Umgebung verwenden und nicht der Co-Admin im Abonnement sind, erstellt das Portal ein „Ausführen als“-Konto für Resource Manager, generiert bei der Bereitstellung des klassischen „Ausführen als“-Kontos jedoch einen Fehler. Wenn Sie nicht beabsichtigen, klassische Ressourcen zu unterstützen, können Sie diesen Fehler ignorieren.
>
> Ausführende Konten können auch mithilfe von [PowerShell](/azure/automation/manage-runas-account#create-run-as-account-using-powershell) erstellt werden.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie das [Onboarding Ihrer Server](./onboarding-overview.md) zu Azure-Verwaltungsdiensten durchgeführt wird.

> [!div class="nextstepaction"]
> [Onboarding zu Azure-Serververwaltungsdiensten](./onboarding-overview.md)
