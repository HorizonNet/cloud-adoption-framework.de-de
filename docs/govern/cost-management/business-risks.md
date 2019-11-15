---
title: 'Kostenverwaltung: Motivationen und Geschäftsrisiken'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Kostenverwaltung: Motivationen und Geschäftsrisiken'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 49fcfb3558da82e34f33f54c4e36780606b1e47d
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753253"
---
# <a name="cost-management-motivations-and-business-risks"></a>Kostenverwaltung: Motivationen und Geschäftsrisiken

In diesem Artikel werden die Gründe beschrieben, warum Kunden typischerweise eine Disziplin „Kostenverwaltung“ in ihre Cloud Governance-Strategie integrieren. Darüber hinaus werden einige Beispiele für Geschäftsrisiken aufgeführt, die zu Richtlinienanweisungen führen.

<!-- markdownlint-disable MD026 -->

## <a name="is-cost-management-relevant"></a>Ist Kostenverwaltung relevant?

Im Hinblick auf die Kostenkontrolle führt die Einführung der Cloud zu einem Paradigmenwechsel. Die Kostenverwaltung in einer traditionellen lokalen Welt basiert auf Aktualisierungszyklen, Rechenzentrumseinkäufen, Hostverlängerungen und Problemen der laufenden Wartung. Sie können alle diese Kosten prognostizieren, planen und verfeinern und mit den jährlichen Investitionsbudgets abstimmen.

Bei der Kostenverwaltung im Zusammenhang mit Cloudlösungen neigen viele Unternehmen dazu, einen reaktiven Ansatz zu verfolgen. In vielen Fällen kaufen Unternehmen im Voraus eine bestimmte Menge von Clouddiensten bzw. verpflichten sich zur deren Nutzung. Bei diesem Modell wird davon ausgegangen, dass die Maximierung von Rabatten, basierend darauf, wie viel das Unternehmen für die Ausgaben bei einem bestimmten Cloudanbieter plant, die Wahrnehmung eines proaktiven, geplanten Kostenzyklus schafft. Diese Wahrnehmung lässt sich allerdings nur dann umsetzen, wenn das Unternehmen auch eine ausgereifte Disziplin „Kostenverwaltung“ implementiert.

Die Cloud bietet Self-Service-Funktionen, die in herkömmlichen lokalen Rechenzentren bisher unbeachtet waren. Diese neuen Funktionen befähigen Unternehmen, agiler, weniger restriktiv und offener für die Einführung neuer Technologien zu sein. Der Nachteil der Self-Service-Funktionen besteht jedoch darin, dass Endbenutzer unwissentlich die zugewiesenen Budgets überschreiten können. Umgekehrt kann es bei denselben Benutzern zu unerwarteten Planänderungen kommen, wodurch die prognostizierte Menge an Clouddiensten nicht benötigt werden. Die Möglichkeit einer Verschiebung in beide Richtungen rechtfertigt Investitionen in eine Disziplin „Kostenverwaltung“ innerhalb des Governanceteams.

## <a name="business-risk"></a>Geschäftsrisiken

Mit der Disziplin „Kostenverwaltung“ wird versucht, die wichtigsten Geschäftsrisiken im Zusammenhang mit den Kosten für das Hosting von cloudbasierten Workloads anzugehen. Arbeiten Sie mit Ihrem Unternehmen zusammen, um diese Risiken zu identifizieren und auf Relevanz zu überwachen, um sie bei der Planung und Implementierung Ihrer Cloudbereitstellungen zu berücksichtigen.

Die Risiken werden je nach Organisation unterschiedlich sein, aber die folgenden allgemeinen kostenbezogenen Risiken können als Ausgangspunkt für Diskussionen innerhalb Ihres Cloudgovernanceteams verwendet werden:

- **Budgetkontrolle:** Wird die Budgetkontrolle vernachlässigt, kann dies zu überhöhten Ausgaben bei einem Cloudanbieter führen.
- **Auslastungsverluste:** Nicht genutzte Vorabkäufe oder Vorabverpflichtungen können zu Investitionsverlusten führen.
- **Anomalien bei der Nutzung:** Unerwartete Spitzen in beide Richtungen können ein Hinweis auf unsachgemäße Nutzung sein.
- **Überdimensionierte Ressourcen:** Wenn Ressourcen in einer Konfiguration bereitgestellt werden, die die Anforderungen einer Anwendung oder eines virtuellen Computers (virtual machine, VM) übersteigen, kann dies zu Verschwendung führen.

## <a name="next-steps"></a>Nächste Schritte

Dokumentieren Sie mit der [Cloudverwaltungsvorlage](./template.md) die Geschäftsrisiken, die wahrscheinlich durch den aktuellen Cloudeinführungsplan entstehen.

Sobald Sie mit realistischen Geschäftsrisiken vertraut sind, besteht der nächste Schritt darin, die Risikotoleranz des Unternehmens zu dokumentieren sowie die Indikatoren und Schlüsselmetriken zur Überwachung dieser Toleranz zu erfassen.

> [!div class="nextstepaction"]
> [Grundlegendes zu Indikatoren, Metriken und Risikotoleranz](./metrics-tolerance.md)
