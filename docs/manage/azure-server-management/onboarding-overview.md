---
title: Onboarding zu Azure-Serververwaltungsdiensten
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Onboarding zu Azure-Serververwaltungsdiensten
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 330e297b4fb63eaa376e8b6dac0ccf77c2a16ef4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031379"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Phase 2: Onboarding für Azure-Serververwaltungsdienste

Wenn Sie mit den [Tools](./tools-services.md) und der [Planung](./prerequisites.md) vertraut sind, die an den Azure-Verwaltungsdiensten beteiligt sind, bietet die zweite Phase, für die Sie jetzt bereit sind, eine schrittweise Anleitung für das Onboarding dieser Dienste zur Verwendung mit Ihren Azure-Ressourcen. Beginnen Sie mit der Bewertung dieses Onboardingprozesses, bevor Sie ihn in Ihrer Umgebung allgemein einführen.

> [!NOTE]
> Die in den späteren Abschnitten dieser Anleitung beschriebenen Automatisierungsansätze beziehen sich auf Bereitstellungen, bei denen noch keine Server in der Cloud bereitgestellt wurden. Sie erfordern, dass Sie über die Rolle „Besitzer“ für ein Abonnement verfügen, um alle erforderlichen Ressourcen und Richtlinien zu erstellen. Wenn Sie bereits einen Log Analytics-Arbeitsbereich und Ressourcen des Automation-Kontos erstellt haben, wird empfohlen, diese Ressourcen beim Start der Beispielautomatisierungsskripts in den entsprechenden Parametern zu übergeben.

## <a name="onboarding-processes"></a>Onboardingprozesse

Dieser Abschnitt im Leitfaden behandelt die folgenden Onboardingprozesse sowohl für virtuelle Azure-Computer als auch für lokale Server:

- **Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung über das Portal**. Verwenden Sie diesen Prozess, um sich mit den Azure-Serververwaltungsdiensten vertraut zu machen.
- **Konfigurieren von Verwaltungsdiensten für ein Abonnement über das Portal**. Dieser Prozess hilft Ihnen, die Azure-Umgebung so zu konfigurieren, dass alle neu bereitgestellten virtuellen Computer automatisch Verwaltungsdienste nutzen. Verwenden Sie diesen Ansatz, wenn Sie die Azure-Portalumgebung den Skripts und Befehlszeilen vorziehen.
- **Konfigurieren von Verwaltungsdiensten für ein Abonnement über Azure Automation**. Dieser Prozess ist vollständig automatisiert. Sie müssen nur ein Abonnement erstellen, und die Skripts konfigurieren die Umgebung so, dass sie Verwaltungsdienste für alle neu bereitgestellten virtuellen Computer verwenden. Verwenden Sie diesen Ansatz, wenn Sie mit der Verwendung von PowerShell-Skripts und Azure Resource Manager-Vorlagen vertraut sind oder deren Verwendung erlernen möchten.

Die Verfahren für die einzelnen Ansätze sind unterschiedlich.

> [!NOTE]
> Die Reihenfolge der Onboardingschritte bei der Verwendung des Azure-Portals unterscheidet sich von den automatisierten Onboardingschritten, da das Portal eine einfachere Onboardingerfahrung bietet.

Das folgende Diagramm zeigt das empfohlene Bereitstellungsmodell für Verwaltungsdienste. 

![Diagramm des empfohlenen Bereitstellungsmodells](./media/recommended-deployment.png)

> [!NOTE]
> Wie im vorherigen Diagramm dargestellt, verfügt der Log Analytics-Agent sowohl über eine *auto-enroll*- als auch über eine *opt-in*-Konfiguration für lokale Server. *Auto-enroll* bedeutet, dass die in diesem Arbeitsbereich aktivierten Lösungen automatisch auf den Server angewendet werden, wenn der Log Analytics-Agent auf einem Server installiert und für die Verbindung mit einem Arbeitsbereich konfiguriert ist. *Opt-in* bedeutet, dass die Lösung auch dann nicht angewendet wird, wenn der Agent installiert und mit dem Arbeitsbereich verbunden ist, es sei denn, sie wird der Bereichskonfiguration des Servers im Arbeitsbereich hinzugefügt.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das Onboarding für einen einzelnen virtuelle Computer über das Portal durchführen können, um den Onboardingprozess zu bewerten.

> [!div class="nextstepaction"]
> [Onboarding eines einzelnen virtuellen Azure-Computers für die Auswertung](./onboard-single-vm.md)
