---
title: Übersicht über Azure-Serververwaltungsdienste
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einführung in Azure-Serververwaltungsdienste
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4d1ada9d47e54f4b0d3828ce93b2d55f3eda8a34
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026334"
---
# <a name="overview-of-azure-server-management-services"></a>Übersicht über Azure-Serververwaltungsdienste

Azure-Serververwaltungsdienste bieten Kunden eine konsistente Umgebung für die bedarfsorientierte Serververwaltung. Diese Dienste sind sowohl für Linux- als auch für Windows-Betriebssysteme geeignet und können in Produktions-, Entwicklungs- und Testumgebungen verwendet werden. Darüber hinaus unterstützen sie virtuelle Azure-IaaS-Computer und physische Server sowie virtuelle Computer, die entweder lokal oder in anderen Hostingumgebungen gehostet werden. 

Die Azure-Serververwaltungssuite umfasst die im folgenden Diagramm gezeigten Dienste. 

![Diagramm des Azure-Betriebsmodells](./media/operations-diagram.png)

Dieser Abschnitt des Microsoft-Frameworks für die Cloudeinführung stellt einen umsetzbaren Plan mit Vorgaben für die Bereitstellung von Serververwaltungsdiensten in Ihrer Umgebung bereit. Dieser Plan dient zur schnellen Orientierung in Bezug auf diese Dienste und führt Sie schrittweise durch die verschiedenen Verwaltungsphasen für Umgebungen jeder Größenordnung.

Die Informationen wurden der Einfachheit halber in drei Phasen unterteilt:

![Die drei Onboardingphasen der Azure-Serververwaltungssuite](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-management-services"></a>Gründe für die Verwendung von Azure-Verwaltungsdiensten

Azure-Verwaltungsdienste bieten folgende Vorteile:

- **Native Azure-Dienste:** Die Verwaltungsdienste sind nativ in Azure Resource Manager integriert. Sie werden kontinuierlich verbessert und um neue Features und Funktionen erweitert.
- **Windows und Linux:** Für Windows- und Linux-Computer steht die gleiche konsistente Verwaltungsumgebung zur Verfügung.
- **Hybrid:** Die Verwaltungsdienste unterstützen sowohl virtuelle Azure-IaaS-Computer als auch physische und virtuelle Server, die lokal oder in anderen Hostingumgebungen gehostet werden.
- **Sicherheit.** Microsoft kümmert sich mit großem Aufwand um alle Sicherheitsaspekte. Dies dient nicht nur dem Schutz der Azure-Cloudinfrastruktur; die resultierenden Technologien und Kompetenzen kommen auch dem Schutz der Kundenressourcen zugute – ganz gleich, wo sich diese befinden.

## <a name="next-steps"></a>Nächste Schritte

Machen Sie sich mit den [Tools, Diensten und Planungsschritten](./prerequisites.md) im Zusammenhang mit der Einführung der Azure-Serververwaltungssuite vertraut.

> [!div class="nextstepaction"]
> [Phase 1: Prerequisite planning for Azure server management services](./prerequisites.md) (Phase 1: Erforderliche Planung für Azure-Serververwaltungsdienste)
