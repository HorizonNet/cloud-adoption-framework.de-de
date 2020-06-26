---
title: Implementieren von Zielzonen auf Unternehmensebene in Azure
description: Prüfen Sie Optionen zur Implementierung der Architektur auf Unternehmensebene.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b804810e23213dc6ebedbe94aa9ea7c1af91cc8e
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076869"
---
# <a name="implement-enterprise-scale-landing-zones-in-azure"></a>Implementieren von Zielzonen auf Unternehmensebene in Azure

Wenn Geschäftsanforderungen eine vielfältige Anfangsimplementierung von Zielzonen verlangen, mit vollständiger Integration von Governance, Sicherheit und Vorgängen von Anfang an, schlägt Microsoft das Befolgen der Beispieloptionen für die Unternehmensebene auf dieser Seite vor. Bei diesem Ansatz können Sie das Microsoft Azure-Portal oder Infrastructure-as-Code zum Einrichten und Konfigurieren Ihrer Umgebung verwenden. Sie können auch zwischen dem Portal und Infrastructure-as-Code wechseln (empfohlen), sobald Ihre Organisation dafür bereit ist. Wie bei anderen Infrastructure-as-Code-Ansätze in Microsoft Azure benötigen Sie Kenntnisse in Bezug auf Azure Resource Manager-Vorlagen und GitHub.

## <a name="example-implementation"></a>Beispielimplementierung

In der folgenden Tabelle sind Beispiele für modulare Implementierungen aufgeführt.

| Beispielbereitstellung  | BESCHREIBUNG  | GitHub-Repository | Bereitstellen in Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Unternehmensweite Grundlage | Dies ist die empfohlene Grundlage für die unternehmensweite Einführung. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Beispiel in Azure bereitstellen](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzOps%2Fmain%2Ftemplate%2Fux-foundation.json) |
| Unternehmensweites Virtual WAN | Fügen Sie ein Virtual WAN-Netzwerkmodul zur unternehmensweiten Grundlage hinzu. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Beispiel in Azure bereitstellen](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzOps%2Fmain%2Ftemplate%2Fux-vwan.json) |
| Hub-and-Spoke auf Unternehmensebene | Fügen Sie der unternehmensweiten Grundlage ein Hub-and-Spoke-Netzwerkmodul hinzu. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) | <!-- [Deploy example to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkrnese%2FAzureDeploy%2Fmaint%2FARM%2Fdeployments%2Fe2e.json) --> In Kürze verfügbar |

## <a name="next-steps"></a>Nächste Schritte

Bei diesen Beispielen handelt es sich um eine einfache Bereitstellungsoption zur Unterstützung des kontinuierlichen Lernens für den unternehmensweiten Ansatz. Bevor Sie diese Beispiele in einer Produktionsversion auf Unternehmensebene nutzen, sollten Sie sich zunächst die [Architektur auf Unternehmensebene](./architecture.md) ansehen.
