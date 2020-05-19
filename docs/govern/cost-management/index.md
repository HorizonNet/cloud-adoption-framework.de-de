---
title: Übersicht über die Disziplin „Kostenverwaltung“
description: Hier wird der Ansatz zur Entwicklung einer Disziplin des Typs „Kostenverwaltung“ (Cost Management) als Teil einer Cloudgovernancestrategie beschrieben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e65fc091b5578c2a3fdf8ea0483450526b47f1c5
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400681"
---
# <a name="cost-management-discipline-overview"></a>Übersicht über die Disziplin „Kostenverwaltung“

Die Disziplin „Kostenverwaltung“ (Cost Management) ist eine der [fünf Disziplinen von Cloud Governance](../governance-disciplines.md) innerhalb des [CAF-Governancemodells (Cloud Adoption Framework)](../index.md). Für viele Kunden ist die Kontrolle ihrer Kosten bei der Einführung von Cloudtechnologien ein wichtiges Thema. Das Gleichgewicht zwischen Leistungsanforderungen, Einführungsrhythmus und Kosten der Clouddienste kann eine Herausforderung darstellen. Dies ist besonders relevant bei großen Unternehmenstransformationen, bei denen Cloudtechnologien implementiert werden. In diesem Abschnitt wird der Ansatz zur Entwicklung einer Disziplin „Kostenverwaltung“ als Teil einer Cloud Governance-Strategie beschrieben.

> [!NOTE]
> Die Disziplin „ Kostenverwaltung“ ersetzt nicht die bestehenden Geschäftsteams, Buchhaltungspraktiken und -verfahren, die an der finanziellen Verwaltung der IT-bezogenen Kosten in Ihrem Unternehmen beteiligt sind. Der Hauptzweck dieser Disziplin besteht darin, potenzielle Cloudrisiken im Zusammenhang mit IT-Ausgaben zu identifizieren und den Geschäfts- und IT-Teams, die für die Bereitstellung und Verwaltung von Cloudressourcen verantwortlich sind, eine Anleitung zur Risikominderung zu geben.

Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten jedoch die Einbeziehung von und Diskussion mit relevanten Mitgliedern Ihrer Geschäfts- und IT-Teams beinhalten, insbesondere diejenigen Führungskräften, die für den Besitz, die Verwaltung und die Bezahlung von cloudbasierten Workloads verantwortlich sind.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin „Kostenverwaltung“. Beispiele für Richtlinienanweisungen finden Sie im Artikel über [Richtlinienanweisungen zur Kostenverwaltung](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für die Governancerichtlinien Ihrer Organisation dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden sechs Schritte helfen Ihnen bei der Definition von Governancerichtlinien zur Kostenkontrolle in Ihrer Umgebung.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![Vorlagensymbol](../../_images/govern/process-template.png) | [Vorlage zur Disziplin „Kostenverwaltung“:](./template.md) Laden Sie die Vorlage zur Dokumentation einer Disziplin vom Typ „Kostenverwaltung“ herunter. |
| <br> ![Risikosymbol](../../_images/govern/process-risks.png) | [Geschäftsrisiken:](./business-risks.md) Machen Sie sich mit den Motiven und Risiken vertraut, die häufig mit der Disziplin „Kostenverwaltung“ verbunden sind. |
| <br> ![Metriksymbol](../../_images/govern/process-metrics.png) | [Indikatoren und Metriken:](./metrics-tolerance.md) Indikatoren, um zu verstehen, ob es der richtige Zeitpunkt ist, in die Disziplin „Kostenverwaltung“ zu investieren. |
| <br> ![Einhaltungssymbol](../../_images/govern/process-enforce.png) | [Prozesse zur Einhaltung von Richtlinien:](./compliance-processes.md) Empfohlene Prozesse zur Unterstützung der Richtlinieneinhaltung in der Disziplin „Kostenverwaltung“. |
| <br> ![Einsatzreifesymbol](../../_images/govern/process-maturity.png) | [Einsatzreife:](./discipline-improvement.md) Stimmen Sie die Einsatzreife der Cloudverwaltung mit den Phasen der Cloudeinführung ab. |
| <br> ![Toolkettensymbol](../../_images/govern/process-toolchain.png) | [Toolkette:](./toolchain.md) Azure-Dienste, die zur Unterstützung der Disziplin „Kostenverwaltung“ implementiert werden können. |

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der Bewertung von Geschäftsrisiken in einem bestimmten Umfeld.

> [!div class="nextstepaction"]
> [Grundlegendes zu Geschäftsrisiken](./business-risks.md)

<!-- markdownlint-enable MD033 -->
