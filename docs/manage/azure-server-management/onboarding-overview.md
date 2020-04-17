---
title: Onboarding für Azure-Serververwaltungsdienste
description: Enthält eine Beschreibung des Onboardings für Azure-Serververwaltungsdienste mit Informationen für virtuelle Azure-Computer und lokale Server.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: f83678c1a2b3387155b9fa908c54e81670daf8ae
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80426502"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Phase 2: Onboarding für Azure-Serververwaltungsdienste

Nachdem Sie mit den [Tools](./tools-services.md) und der [Planung](./prerequisites.md) für die Azure-Verwaltungsdienste vertraut sind, sind Sie bereit für die zweite Phase. Phase 2 bietet eine schrittweise Anleitung für die Integration dieser Dienste zur Verwendung mit Ihren Azure-Ressourcen. Beginnen Sie mit der Bewertung dieses Onboardingprozesses, bevor Sie ihn in Ihrer Umgebung allgemein einführen.

> [!NOTE]
> Die in den späteren Abschnitten dieser Anleitung beschriebenen Automatisierungsansätze beziehen sich auf Bereitstellungen, bei denen noch keine Server in der Cloud bereitgestellt wurden. Sie erfordern, dass Sie über die Rolle „Besitzer“ für ein Abonnement verfügen, um alle erforderlichen Ressourcen und Richtlinien zu erstellen. Wenn Sie bereits Log Analytics-Arbeitsbereiche und Automation-Konten erstellt haben, wird empfohlen, diese Ressourcen beim Start der Beispielautomatisierungsskripts in den entsprechenden Parametern zu übergeben.

## <a name="onboarding-processes"></a>Onboardingprozesse

Dieser Abschnitt im Leitfaden behandelt die folgenden Onboardingprozesse sowohl für virtuelle Azure-Computer als auch für lokale Server:

- **Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung über das Portal**. Verwenden Sie diesen Prozess, um sich mit den Azure-Serververwaltungsdiensten vertraut zu machen.
- **Konfigurieren von Verwaltungsdiensten für ein Abonnement über das Portal**. Dieser Prozess hilft Ihnen, die Azure-Umgebung so zu konfigurieren, dass alle neu bereitgestellten virtuellen Computer automatisch Verwaltungsdienste nutzen. Verwenden Sie diesen Ansatz, wenn Sie die Azure-Portalumgebung den Skripts und Befehlszeilen vorziehen.
- **Konfigurieren von Verwaltungsdiensten für ein Abonnement über Azure Automation**. Dieser Prozess ist vollständig automatisiert. Erstellen Sie einfach ein Abonnement und die Skripts konfigurieren die Umgebung so, dass sie Verwaltungsdienste für alle neu bereitgestellten virtuellen Computer verwenden. Verwenden Sie diesen Ansatz, wenn Sie mit der Verwendung von PowerShell-Skripts und Azure Resource Manager-Vorlagen vertraut sind oder deren Verwendung erlernen möchten.

Die Verfahren für die einzelnen Ansätze sind unterschiedlich.

> [!NOTE]
> Wenn Sie das Azure-Portal verwenden, unterscheidet sich die Reihenfolge der Onboardingschritte von den automatisierten Onboardingschritten. Das Portal bietet ein einfacheres Onboardingerlebnis.

Das folgende Diagramm zeigt das empfohlene Bereitstellungsmodell für Verwaltungsdienste:

![Diagramm des empfohlenen Bereitstellungsmodells](./media/recommended-deployment.png)

Wie im vorherigen Diagramm dargestellt, verfügt der Log Analytics-Agent sowohl über eine *auto-enroll*- als auch über eine *opt-in*-Konfiguration für lokale Server:

- **Auto-enroll:** Wenn der Log Analytics-Agent auf einem Server installiert und für die Verbindung mit einem Arbeitsbereich konfiguriert ist, werden die in diesem Arbeitsbereich aktivierten Lösungen automatisch auf den Server angewendet.
- **Opt-in:** Auch wenn der Agent installiert und mit dem Arbeitsbereich verbunden ist, wird die Lösung nicht angewendet, es sei denn, sie wird der Bereichskonfiguration des Servers im Arbeitsbereich hinzugefügt.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das Onboarding für einen einzelnen virtuelle Computer über das Portal durchführen können, um den Onboardingprozess zu bewerten.

> [!div class="nextstepaction"]
> [Onboarding eines einzelnen virtuellen Azure-Computers für die Auswertung](./onboard-single-vm.md)
