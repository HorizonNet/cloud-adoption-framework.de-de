---
title: Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4ebf0bf17fafcd495414d32fe04882c36634d4e2
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836548"
---
# <a name="enable-management-services-on-a-single-vm-for-evaluation"></a>Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung

Erhalten Sie Informationen zum Aktivieren von Verwaltungsdiensten auf einem einzelnen virtuellen Computer zur Auswertung.

> [!NOTE]
> Erstellen Sie den erforderlichen [Log Analytics-Arbeitsbereich und das Azure Automation-Konto](./prerequisites.md#create-a-workspace-and-automation-account), bevor Sie das Onboarding von virtuellen Computern für Azure-Verwaltungsdienste durchführen.

Das Onboarding einzelner virtueller Computer (VMs) in die Azure-Serververwaltungsdienste gestaltet sich im Azure-Portal einfach. Das Portal ermöglicht es Ihnen, sich mit diesen Diensten vertraut zu machen, bevor Sie das Onboarding mit ihnen für Ihre virtuellen Computer durchführen. Wenn Sie eine VM-Instanz auswählen, werden alle Lösungen, die in der Liste der [Verwaltungstools und -dienste](./tools-services.md) beschrieben werden, entweder im Menü **Vorgänge** oder im Menü **Überwachung** angezeigt. Sie können die einzelnen Lösungen auswählen und dem Assistenten beim Onboarding folgen.

![Screenshot der Einstellungen des virtuellen Computers im Azure-Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Zugehörige Ressourcen

Weitere Informationen zum Onboarding einzelner VMs in den einzelnen Lösungen finden Sie unter:

- [Integrieren von Lösungen für die Updateverwaltung, Änderungsnachverfolgung und den Bestand von einem virtuellen Azure-Computer](/azure/automation/automation-onboard-solutions-from-vm)
- [Onboarding der Azure-Überwachung für VMs](/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das bedarfsabhängige Onboarding von virtuellen Azure-Computern mit Azure Policy durchführen.

> [!div class="nextstepaction"]
> [Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement](./onboard-at-scale.md)
