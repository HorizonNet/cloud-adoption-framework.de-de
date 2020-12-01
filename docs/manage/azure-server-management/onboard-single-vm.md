---
title: Aktivieren von Serververwaltungsdiensten auf einem virtuellen Computer
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Azure-Serververwaltungsdienste auf einem virtuellen Computer aktivieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5af275b0309008c1ebcab8c1f3ff9edba2789b2e
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94880363"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Aktivieren von Serververwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung

Erhalten Sie Informationen zum Aktivieren von Serververwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung.

> [!NOTE]
> Erstellen Sie den erforderlichen [Log Analytics-Arbeitsbereich und das Azure Automation-Konto](./prerequisites.md#create-a-workspace-and-automation-account), bevor Sie Azure-Verwaltungsdienste auf einem virtuellen Computer implementieren.

Das Onboarding einzelner virtueller Computer (VMs) in die Azure-Serververwaltungsdienste gestaltet sich im Azure-Portal einfach. Sie können sich mit diesen Diensten vor dem Onboarding vertraut machen. Wenn Sie eine VM-Instanz auswählen, werden alle Lösungen in der Liste der [Verwaltungstools und -dienste](./tools-services.md) im Menü **Vorgänge** oder **Überwachung** angezeigt. Sie wählen eine Lösung aus und folgen dem Assistenten beim Onboarding.

![Screenshot der Einstellungen des virtuellen Computers im Azure-Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Zugehörige Ressourcen

Weitere Informationen zum Onboarding dieser Lösungen auf einzelnen virtuellen Computern finden Sie unter:

- [Onboarding der Lösungen „Updateverwaltung“ und „Änderungsnachverfolgung und Bestand“ für eine VM in Azure](/azure/automation/change-tracking/manage-inventory-vms)
- [Führen Sie das Onboarding von Azure Monitor for VMs durch](/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das bedarfsabhängige Onboarding von virtuellen Azure-Computern mit Azure Policy durchführen.

> [!div class="nextstepaction"]
> [Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement](./onboard-at-scale.md)
