---
title: Erhöhen der Sicherheit von Zielzonen
description: Erhöhen der Sicherheit von Zielzonen
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: be340d1566fce58012cd63c6efc90fd2e0636260
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81122019"
---
<!-- cSpell:ignore SIEM -->

# <a name="improve-landing-zone-security"></a>Erhöhen der Sicherheit von Zielzonen

Wenn Workloads oder die Zielzone, in der sie gehostet werden, den Zugriff auf vertrauliche Daten oder unternehmenskritische Systeme erfordern, ist es wichtig, die Daten und Ressourcen zu schützen. Die Verbesserung der Sicherheit von Zielzonen baut auf dem [testgesteuerten Entwicklungsansatz für Zielzonen](./test-driven-development.md) auf, indem die Zielzone erweitert oder umgestaltet wird, um den erhöhten Sicherheitsanforderungen gerecht zu werden.

## <a name="landing-zone-security-best-practices"></a>Bewährte Sicherheitsmethoden für Zielzonen

Die folgende Liste von Referenzarchitekturen und bewährten Methoden enthält Beispiele für Möglichkeiten zur Verbesserung der Sicherheit für Zielzonen:

- [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-get-started?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json): Führen Sie das Onboarding für ein Abonnement in Security Center durch.
- [Azure Sentinel:](https://docs.microsoft.com/azure/sentinel/quickstart-onboard?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) Führen Sie das Onboarding für Azure Sentinel durch, um eine **Lösung für Security Information & Event Management (SIEM)** und für die **Sicherheitsorchestrierung mit automatisierter Reaktion (Security Orchestration Automated Response, SOAR)** bereitzustellen.
- [Sicherheit von Netzwerkgrenzen](../../reference/networking-vdc.md): Verschiedene Referenzmuster für die Entwicklung eines Netzwerks, ähnlich der Vorgehensweise beim Sichern der Netzwerkgrenze in einem Rechenzentrum.
- [Sichere Netzwerkarchitektur](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json): Referenzarchitektur für die Implementierung eines Umkreisnetzwerks und einer sicheren Netzwerkarchitektur.
- [Identitätsverwaltung und Zugriffssteuerung](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json): Eine Reihe von bewährten Methoden für die Implementierung der Identität und des Zugriffs zum Sichern einer Zielzone in Azure.
- [Methoden für die Netzwerksicherheit](https://docs.microsoft.com/azure/security/fundamentals/network-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json): Bietet zusätzliche bewährte Methoden zum Sichern des Netzwerks.
- [Betriebssicherheit](https://docs.microsoft.com/azure/security/fundamentals/operational-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) bietet bewährte Methoden zum Erhöhen der Betriebssicherheit in Azure.
- [Sicherheitsbaseline](../../govern/guides/complex/security-baseline-improvement.md#incremental-improvement-of-the-best-practices): Beispiel für die Entwicklung einer von der Governance gesteuerten Sicherheitsbaseline zur Durchsetzung von Sicherheitsanforderungen.

## <a name="test-driven-development-cycle"></a>Testgesteuerter Entwicklungszyklus

Bevor irgendwelche Sicherheitsverbesserungen in Angriff genommen werden, ist es wichtig, die „Definition of Done“ und alle „Akzeptanzkriterien“ zu verstehen. Weitere Informationen finden sich in den Artikeln [Testgesteuerte Entwicklung von Zielzonen](./test-driven-development.md) und [Testgesteuerte Entwicklung in Azure](./azure-test-driven-development.md).

![Testgesteuerter Entwicklungsprozess für Cloudzielzonen](../../_images/ready/test-driven-development-process.png)

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie den [Betrieb von Zielzonen verbessern](./landing-zone-operations.md), um entscheidende Anwendungen zu unterstützen.

> [!div class="nextstepaction"]
> [Verbessern des Betriebs von Zielzonen](./landing-zone-operations.md)
