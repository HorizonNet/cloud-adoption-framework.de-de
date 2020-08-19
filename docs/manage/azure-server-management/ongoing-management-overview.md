---
title: Kontinuierliche Verwaltung und Sicherheit
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie sich auf die Vorgänge und Sicherheitskonfigurationen konzentrieren, die Ihren laufenden Betrieb unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: adeda043b1631caf19975163c3433f7aa9bef12a
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88571880"
---
# <a name="phase-3-ongoing-management-and-security"></a>Phase 3: Kontinuierliche Verwaltung und Sicherheit

Nach dem Onboarding der Azure-Serververwaltungsdienste müssen Sie sich auf die Vorgänge und Sicherheitskonfigurationen konzentrieren, die Ihren laufenden Betrieb unterstützen. Wir beginnen mit der Sicherung Ihrer Umgebung, indem wir das Azure Security Center überprüfen. Anschließend werden Richtlinien konfiguriert, um die Konformität Ihrer Server sicherzustellen und allgemeine Aufgaben zu automatisieren. Dieser Abschnitt enthält die folgenden Themen:

- **[Behandeln von Sicherheitsempfehlungen](#address-security-recommendations)** Das Azure Security Center unterbreitet Vorschläge zur Verbesserung der Sicherheit Ihrer Umgebung. Wenn Sie diese Empfehlungen implementieren, werden die Auswirkungen in einer Sicherheitsbewertung widergespiegelt.
- **[Aktivieren der Gastkonfigurationsrichtlinie](./guest-configuration-policy.md)** Verwenden Sie das Feature zur Gastkonfiguration von Azure Policy, um die Einstellungen innerhalb eines virtuellen Computers zu überprüfen. So können Sie z. B. überprüfen, ob Zertifikate in Kürze ablaufen werden.
- **[Nachverfolgung und Warnung bei kritischen Änderungen](./enable-tracking-alerting.md)** Bei der Problembehandlung ist die erste Frage: „Was hat sich geändert?“. In diesem Abschnitt erfahren Sie, wie Sie Änderungen verfolgen und Warnungen ausgeben, um entscheidende Komponenten proaktiv zu überwachen.
- **[Erstellen von Zeitplänen für Updates](./update-schedules.md)** Planen Sie die Installation von Updates, um sicherzustellen, dass alle Server über die neuesten Updates verfügen.
- **[Allgemeine Azure Policy-Beispiele](./common-policies.md)** In diesem Artikel werden Beispiele für allgemeine Verwaltungsrichtlinien zur Verfügung gestellt.

## <a name="address-security-recommendations"></a>Behandeln von Sicherheitsempfehlungen

Das Azure Security Center ist der zentrale Punkt, an dem Sie die Sicherheit für Ihre Umgebung verwalten können. Es werden eine Gesamtbewertung und gezielte Empfehlungen angezeigt.

Es wird empfohlen, die Empfehlungen dieses Diensts zu überprüfen und zu implementieren. Informationen zu den zusätzlichen Vorteilen von Azure Security Center finden Sie unter [Befolgen der Azure Security Center-Empfehlungen](/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie das Feature für die [Gastkonfiguration von Azure Policy aktivieren](./guest-configuration-policy.md).

> [!div class="nextstepaction"]
> [Gastkonfigurationsrichtlinie](./guest-configuration-policy.md)
