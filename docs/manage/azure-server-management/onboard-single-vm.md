---
title: Aktivieren von Serververwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aktivieren von Serververwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7ee8cab09fc5ad875240a10d7fe6f632d91432c9
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73751658"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Aktivieren von Serververwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung

Erhalten Sie Informationen zum Aktivieren von Serververwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung.

> [!NOTE]
> Erstellen Sie den erforderlichen [Log Analytics-Arbeitsbereich und das Azure Automation-Konto](./prerequisites.md#create-a-workspace-and-automation-account), bevor Sie Azure-Verwaltungsdienste auf einem virtuellen Computer implementieren.

Das Onboarding einzelner virtueller Computer (VMs) in die Azure-Serververwaltungsdienste gestaltet sich im Azure-Portal einfach. Sie können sich mit diesen Diensten vor dem Onboarding vertraut machen. Wenn Sie eine VM-Instanz auswählen, werden alle Lösungen in der Liste der [Verwaltungstools und -dienste](./tools-services.md) im Menü **Vorgänge** oder **Überwachung** angezeigt. Sie wählen eine Lösung aus und folgen dem Assistenten beim Onboarding.

![Screenshot der Einstellungen des virtuellen Computers im Azure-Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Zugehörige Ressourcen

Weitere Informationen zum Onboarding dieser Lösungen auf einzelnen virtuellen Computern finden Sie unter:

- [Integrieren von Lösungen für die Updateverwaltung, Änderungsnachverfolgung und den Bestand von einem virtuellen Azure-Computer](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Onboarding der Azure-Überwachung für VMs](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das bedarfsabhängige Onboarding von virtuellen Azure-Computern mit Azure Policy durchführen.

> [!div class="nextstepaction"]
> [Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement](./onboard-at-scale.md)
