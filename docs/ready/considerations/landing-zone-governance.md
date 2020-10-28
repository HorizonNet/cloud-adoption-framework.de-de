---
title: Verbessern der Governance von Zielzonen
description: Verbessern der Governance von Zielzonen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 52a09591b5c7dcaaa5aa60495dce84eb8c646a76
ms.sourcegitcommit: 6aa14b15efc9bd351b75f8a3d7ebbac3d575275b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/27/2020
ms.locfileid: "92689946"
---
# <a name="improve-landing-zone-governance"></a>Verbessern der Governance von Zielzonen

Die Governance der Zielzone ist die kleinste Einheit der Gesamtgovernance. Die Einrichtung einer soliden Governancegrundlage in Ihren ersten Zielzonen wird den Umfang des später im Einführungslebenszyklus erforderlichen Refactorings verringern. Die Verbesserung der Governance von Zielzonen wird Kostenkontrollen integrieren, grundlegende Tools einrichten, die eine Skalierung ermöglichen, und es dem Cloudgovernanceteam erleichtern, die fünf Disziplinen der Cloudgovernance zu erfüllen.

## <a name="landing-zone-governance-best-practices"></a>Bewährte Methoden für die Governance von Zielzonen

- **Anfängliche Zielgovernance:** Der Artikel zur Einrichtung einer [anfänglichen Governancegrundlage](../../govern/guides/complex/index.md) unterstützt Sie dabei, die ersten Zielzonen mit anfänglichen Governancetools auszustatten. Diese Methoden werden bei der Skalierung von Einführung und Governance sowie bei der Implementierung eines soliden Cost Managements helfen. Dieses Ansatz beginnt mit: Ressourcenorganisation, Richtliniendefinitionen, RBAC-Rollen und Blaupausendefinitionen.
- **[Standards für Benennung und Kennzeichnung](../azure-best-practices/naming-and-tagging.md):** Stellen Sie eine konsistente Benennung und Markierung sicher, die die Grundlage für die Einführung solider Governancemethoden bilden.
- **[Nachverfolgen von Kosten für Workloads](../azure-best-practices/track-costs.md):** Beginnen Sie mit der Nachverfolgung der Kosten in Ihrer ersten Zielzone. Bewerten Sie, wie Sie die Konsistenz über mehrere Workloads und Rollen hinweg anwenden werden.
- **[Skalieren mit mehreren Abonnements](../azure-best-practices/scale-subscriptions.md):** Bewerten Sie, wie diese und andere Zielzonen skaliert werden, wenn mehrere Abonnements zur Voraussetzung werden.
- **[Organisieren von Abonnements](../azure-best-practices/organize-subscriptions.md):** Erfahren Sie, wie Sie mehrere Abonnements organisieren und verwalten.

## <a name="four-steps-to-improve-overall-governance"></a>Vier Schritte zur Verbesserung der Gesamtgovernance

Die [Govern-Methodik](../../govern/index.md) bietet einen allgemeinen Leitfaden für die Erstellung von Governancerichtlinien, -prozessen und -disziplinen. Wir werden die grundlegende Struktur dieser Methodik und die folgenden Schritte aus dieser Methodik verwenden, um die Zielzonengovernance und die Governance in allen Zielzonen zu verbessern.

1. [Grundlegendes zur Methodik](../../govern/methodology.md): Verstehen Sie die grundlegende Methodik, um den Endzustand des Governanceentwurfs zu lenken.
2. [Vergleichstest](../../govern/benchmark.md): Bewerten Sie sowohl den gegenwärtigen als auch den zukünftigen Zustand, um eine Vision zu entwickeln und Maßnahmen zu ergreifen.
3. [Anfängliche Governancegrundlage](../../govern/initial-foundation.md): Kleiner, leicht zu implementierender Satz von Governancetools zum Einrichten einer ersten Grundlage für alle Zielzonen.
4. [Verbessern der Governancegrundlage](../../govern/foundation-improvements.md): Fügen Sie iterativ Governancekontrollen hinzu, um die Governance aller Zielzonen zu stärken.

## <a name="next-steps"></a>Nächste Schritte

Die Cloudeinführung wird sich mit jeder Welle oder Freigabe neuer Workloads weiter ausweiten. Um diesen Anforderungen immer einen Schritt voraus zu sein, sollten Cloudplattformteams in regelmäßigen Abständen die bewährten Methoden für zusätzliche Zielzonen überprüfen.

> [!div class="nextstepaction"]
> [Weitere bewährte Methoden für Zielzonen](../azure-best-practices/index.md)
