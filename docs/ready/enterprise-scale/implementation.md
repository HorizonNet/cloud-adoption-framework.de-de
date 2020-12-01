---
title: Implementieren von Cloud Adoption Framework-Zielzonen auf Unternehmensebene in Azure
description: Informieren Sie sich über die Optionen zum Implementieren des Cloud Adoption Framework für die Azure-Architektur auf Unternehmensniveau.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: ea900edf52de19b8340f43db1a48218780969652
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447284"
---
# <a name="implement-cloud-adoption-framework-enterprise-scale-landing-zones-in-azure"></a>Implementieren von Cloud Adoption Framework-Zielzonen auf Unternehmensebene in Azure

Wenn Geschäftsanforderungen eine vielfältige Anfangsimplementierung von Zielzonen verlangen, mit vollständiger Integration von Governance, Sicherheit und Vorgängen von Anfang an, verwenden Sie die hier aufgelisteten Beispieloptionen auf Unternehmensebene. Mit diesem Ansatz können Sie das Microsoft Azure-Portal oder Infrastructure-as-Code zum Einrichten und Konfigurieren Ihrer Umgebung verwenden. Sie können auch zwischen dem Portal und Infrastructure-as-Code wechseln (empfohlen), sobald Ihre Organisation dafür bereit ist.

## <a name="example-implementation"></a>Beispielimplementierung

In der folgenden Tabelle sind Beispiele für modulare Implementierungen aufgeführt.

| Beispielbereitstellung  | BESCHREIBUNG  | GitHub-Repository | Bereitstellen in Azure |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Unternehmensweite Grundlage | Dies ist die empfohlene Grundlage für die unternehmensweite Einführung. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/wingtip/README.md) | [Beispiel in Azure bereitstellen](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fes-foundation.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fwingtip%2FarmTemplates%2Fportal-es-foundation.json) |
| Unternehmensweites Virtual WAN | Fügen Sie ein Virtual WAN-Netzwerkmodul zur unternehmensweiten Grundlage hinzu. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md) | [Beispiel in Azure bereitstellen](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fes-vwan.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fcontoso%2FarmTemplates%2Fportal-es-vwan.json) |
| Hub-and-Spoke auf Unternehmensebene | Fügen Sie der unternehmensweiten Grundlage ein Hub-and-Spoke-Netzwerkmodul hinzu. | [Beispiel auf GitHub](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/adventureworks/README.md) |[Beispiel in Azure bereitstellen](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fadventureworks%2FarmTemplates%2Fes-hubspoke.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FEnterprise-Scale%2Fmain%2Fdocs%2Freference%2Fadventureworks%2FarmTemplates%2Fportal-es-hubspoke.json) |

## <a name="next-steps"></a>Nächste Schritte

Diese Beispiele bieten eine einfache Bereitstellungsoption zur Unterstützung des kontinuierlichen Lernens für den unternehmensweiten Ansatz. Bevor Sie diese Beispiele in einer Produktionsversion auf Unternehmensniveau verwenden, sollten Sie sich zunächst die [Architektur auf Unternehmensniveau](./architecture.md) ansehen.
