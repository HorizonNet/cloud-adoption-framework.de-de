---
title: Implementieren von CAF-Zielzonen auf Unternehmensebene in Azure
description: Prüfen Sie Optionen zur Implementierung der CAF-Architektur auf Unternehmensebene.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 164a52dc11673e454ff7ad63fc7c4ddc4617395d
ms.sourcegitcommit: 9662234674e663bc7d4bc134d303520cb146bd95
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87560439"
---
# <a name="implement-caf-enterprise-scale-landing-zones-in-azure"></a>Implementieren von CAF-Zielzonen auf Unternehmensebene in Azure

Wenn Geschäftsanforderungen eine vielfältige Anfangsimplementierung von Zielzonen verlangen, mit vollständiger Integration von Governance, Sicherheit und Vorgängen von Anfang an, verwenden Sie die hier aufgelisteten Beispieloptionen auf Unternehmensebene. Mit diesem Ansatz können Sie das Microsoft Azure-Portal oder Infrastructure-as-Code zum Einrichten und Konfigurieren Ihrer Umgebung verwenden. Sie können auch zwischen dem Portal und Infrastructure-as-Code wechseln (empfohlen), sobald Ihre Organisation dafür bereit ist.

## <a name="example-implementation"></a>Beispielimplementierung

In der folgenden Tabelle sind Beispiele für modulare Implementierungen aufgeführt.

| Beispielbereitstellung  | BESCHREIBUNG  | GitHub-Repository | Bereitstellen in Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Unternehmensweite Grundlage | Dies ist die empfohlene Grundlage für die unternehmensweite Einführung. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Beispiel in Azure bereitstellen](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fes-foundation.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fportal-es-foundation.json) |
| Unternehmensweites Virtual WAN | Fügen Sie ein Virtual WAN-Netzwerkmodul zur unternehmensweiten Grundlage hinzu. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Beispiel in Azure bereitstellen](https://ms.portal.azure.com/?feature.customportal=false#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fes-vwan.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fportal-es-vwan.json) |
| Hub-and-Spoke auf Unternehmensebene | Fügen Sie der unternehmensweiten Grundlage ein Hub-and-Spoke-Netzwerkmodul hinzu. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) | <!-- [Deploy example to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkrnese%2FAzureDeploy%2Fmaint%2FARM%2Fdeployments%2Fe2e.json) --> In Kürze verfügbar |

## <a name="next-steps"></a>Nächste Schritte

Diese Beispiele bieten eine einfache Bereitstellungsoption zur Unterstützung des kontinuierlichen Lernens für den unternehmensweiten Ansatz. Bevor Sie diese Beispiele in einer Produktionsversion auf Unternehmensebene nutzen, sollten Sie sich zunächst die [Architektur auf Unternehmensebene](./architecture.md) ansehen.
