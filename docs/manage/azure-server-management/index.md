---
title: Übersicht über Azure-Serververwaltungsdienste
description: Hier finden Sie Informationen zum umsetzbaren Plan im Cloud Adoption Framework, der Vorgaben für die Bereitstellung von Serververwaltungsdiensten in Ihrer Umgebung bereitstellt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d39d31dd5c8a8a280deb23be9962835bdaa318b6
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89604132"
---
# <a name="overview-of-azure-server-management-services"></a>Übersicht über Azure-Serververwaltungsdienste

Azure-Serververwaltungsdienste bieten eine konsistente Umgebung für die bedarfsorientierte Serververwaltung. Diese Dienste können sowohl für Linux- als auch für Windows-Betriebssysteme eingesetzt werden. Sie können in Produktions-, Entwicklungs- und Testumgebungen verwendet werden. Die Serververwaltungsdienste unterstützen virtuelle Azure-IaaS-Computer und physische Server sowie virtuelle Computer, die lokal oder in anderen Hostingumgebungen gehostet werden.

Die Azure-Serververwaltungssuite umfasst die Dienste im folgenden Diagramm: ![Diagramm des Azure-Betriebsmodells](./media/operations-diagram.png)

Dieser Abschnitt des Microsoft-Frameworks für die Cloudeinführung stellt einen umsetzbaren Plan mit Vorgaben für die Bereitstellung von Serververwaltungsdiensten in Ihrer Umgebung bereit. Dieser Plan dient zur schnellen Orientierung in Bezug auf diese Dienste und führt Sie schrittweise durch die verschiedenen Verwaltungsphasen für Umgebungen jeder Größenordnung.

Die Informationen wurden der Einfachheit halber in drei Phasen unterteilt:

![Die drei Onboardingphasen der Azure-Serververwaltungssuite](./media/operations-stages.png)

## <a name="why-use-azure-server-management-services"></a>Was spricht für die Verwendung von Azure-Serververwaltungsdiensten?

Azure-Serververwaltungsdienste bieten folgende Vorteile:

- **Native Azure-Dienste:** Die Serververwaltungsdienste sind nativ in Azure Resource Manager integriert. Sie werden kontinuierlich verbessert und um neue Features und Funktionen erweitert.
- **Windows und Linux:** Für Windows- und Linux-Computer steht die gleiche konsistente Verwaltungsumgebung zur Verfügung.
- **Hybrid:** Die Serververwaltungsdienste unterstützen sowohl virtuelle Azure-IaaS-Computer als auch physische und virtuelle Server, die lokal oder in anderen Hostingumgebungen gehostet werden.
- **Sicherheit**: Microsoft kümmert sich mit großem Aufwand um alle Sicherheitsaspekte. Dies dient nicht nur dem Schutz der Azure-Infrastruktur; die resultierenden Technologien und Kompetenzen kommen auch dem Schutz der Kundenressourcen zugute – ganz gleich, wo sich diese befinden.

## <a name="next-steps"></a>Nächste Schritte

Machen Sie sich mit den [Tools, Diensten und Planungsschritten](./prerequisites.md) im Zusammenhang mit der Einführung der Azure-Serververwaltungssuite vertraut.

> [!div class="nextstepaction"]
> [Phase 1: Prerequisite planning for Azure server management services](./prerequisites.md) (Phase 1: Erforderliche Planung für Azure-Serververwaltungsdienste)
