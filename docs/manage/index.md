---
title: Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die geschäftlichen und technischen Ansätze entwickeln, die Sie für eine effektive Cloudverwaltung benötigen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: operate
layout: LandingPage
ms.openlocfilehash: 70813b7967b6e46f2c1355db98a2171f245224a6
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223863"
---
# <a name="cloud-management-in-the-cloud-adoption-framework"></a>Cloudverwaltung im Framework für die Cloudeinführung

Die Bereitstellung einer [Cloudstrategie ](../strategy/index.md) erfordert eine solide Planung, Bereitschaft und Einführung. Konkrete Geschäftsergebnisse werden jedoch beim laufenden Betrieb der digitalen Ressourcen erzeugt. Ohne einen Plan für zuverlässige, gut verwaltete Vorgänge der Cloudlösungen haben diese Bemühungen jedoch nur einen geringen Nutzen. Die folgenden Übungen unterstützen Sie dabei, die geschäftlichen und technischen Ansätze zu entwickeln, die für die Bereitstellung einer Cloudverwaltung erforderlich sind, die laufende Vorgänge unterstützt.

## <a name="get-started"></a>Erste Schritte

Zur Vorbereitung auf diese Phase des Cloudeinführungszyklus empfiehlt das Framework die folgenden Übungen:

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| ![1](../_images/icons/1.png)     | <br>[Einrichten einer Verwaltungsbasislinie](./azure-management-guide/index.md): Definieren Sie die wichtigen Klassifizierungen, Cloudverwaltungstools und Prozesse, die für die Bereitstellung Ihrer Mindestverpflichtung zur Betriebsverwaltung erforderlich sind.                                |
| ![2](../_images/icons/2.png)     | <br>[Definieren von geschäftlichen Verpflichtungen](./considerations/business-alignment.md): Dokumentieren Sie die unterstützten Workloads, um betriebliche Verpflichtungen beim Unternehmen herzustellen und Investitionen für die Cloudverwaltung für jede Workload zu vereinbaren.                                |
| ![3](../_images/icons/3.png)     | <br>[Erweitern der Verwaltungsbaseline](./best-practices.md): Ausgehend von geschäftlichen Verpflichtungen und Betriebsentscheidungen nutzen Sie die mitgelieferten bewährten Methoden, um die erforderlichen Cloudverwaltungstools zu implementieren.                                |
| ![4](../_images/icons/4.png)      | <br>[Erweiterte Vorgänge und Entwurfsprinzipien](./design-principles.md): Für Plattformen oder Workloads, die ein höheres Maß an Geschäftsverpflichtungen erfordern, ist möglicherweise eine umfassendere Architekturüberprüfung erforderlich, damit die Verpflichtungen in Bezug auf Resilienz und Zuverlässigkeit gewährleistet sind.  |

Mit den oben beschriebenen Schritten erstellen Sie Handlungsansätze, um die Verwaltungsmethoden des Frameworks für die Cloudeinführung bereitzustellen.

<!-- cSpell:ignore CAF -->

![Verwalten der Methoden im Framework für die Cloudeinführung](../_images/manage/caf-manage.png)

Wie im Artikel [Geschäftliche Ausrichtung](./considerations/business-alignment.md) erläutert, sind nicht alle Workloads von entscheidender Bedeutung. Innerhalb eines Portfolios gibt es verschiedene Abstufungen für betriebliche Verwaltungsanforderungen. Die geschäftliche Ausrichtung unterstützt Sie beim Erfassen der geschäftlichen Auswirkungen und beim Aushandeln von Verwaltungskosten für das Unternehmen, um die am besten geeigneten Prozesse und Tools für die operative Verwaltung sicherzustellen.

Die Anleitungen in diesem Abschnitt „Verwalten“ zum Framework für die Cloudeinführung haben zwei Funktionen:

- Sie liefern Beispiele für umsetzbare Vorgehensweisen für die Betriebsverwaltung, die gängige Kundenerfahrungen widerspiegeln.
- Sie unterstützen Sie beim Erstellen personalisierter Verwaltungslösungen basierend auf Geschäftsverpflichtungen.

Diese Inhalte sind für das Cloudbetriebsteam konzipiert. Sie sind auch für Cloudarchitekten relevant, die eine solide Grundlage für den Cloudbetrieb oder Entwurfsprinzipien für die Cloud entwickeln müssen.

Die Inhalte im CAF (Cloud Adoption Framework) beeinflussen das Geschäft, die Technologie und die Kultur von Unternehmen. Dieser Abschnitt des Frameworks für die Cloudeinführung erfordert eine intensive Interaktion mit den Teams für IT-Abläufe und IT-Governance, der Finanzabteilung, Geschäftsbereichsleitern sowie den Netzwerk-, Identitäts- und Cloudeinführungsteams. Verschiedene Abhängigkeiten zwischen diesen Rollen erfordern einen vermittelnden Ansatz der Cloudarchitekten unter Verwendung dieser Leitlinien. Eine solche Vermittlung zwischen den Teams ist selten nur ein einziges Mal erforderlich.

Der Cloudarchitekt dient als innovative Führungsperson und Vermittler, um diese Zielgruppen zusammenzubringen. Diese Anleitungen sind darauf ausgelegt, Cloudarchitekten die richtige Kommunikation mit der richtigen Zielgruppe zu erleichtern, um notwendige Entscheidungen zu fördern. Um eine durch die Cloud ermöglichte Transformation der Geschäftsabläufe umzusetzen, müssen Cloudarchitekten die betroffenen Teams in allen Geschäfts- und IT-Abteilungen bei ihren Entscheidungen unterstützen.

Jeder Abschnitt des Frameworks für die Cloudeinführung stellt eine andere Spezialisierung oder Variante der Rolle des Cloudarchitekten dar. Dieser Abschnitt des Cloud Adoption Frameworks richtet sich beispielsweise an Cloudarchitekten mit Schwerpunkt auf Betrieb und Verwaltung von Bereitstellungslösungen. Innerhalb dieses Frameworks wird dies als _Cloudbetrieb_ oder kollektiv als _Cloudbetriebsteam_ bezeichnet.

Wenn Sie dem Leitfaden vom Anfang bis zum Ende folgen, helfen diese Inhalte Ihnen dabei, eine robuste Cloudbetriebsstrategie zu entwickeln. Sie werden detailliert durch die Theorie und Implementierung einer solchen Strategie geleitet.

Sie können die Methodik auf das [Festlegen klarer Geschäftsverpflichtungen](./considerations/business-alignment.md) anwenden.

<!-- TODO: For a crash course on the theory and quick access to Azure implementation, get started with the [governance guides overview](TODO). Using this guidance, you can start small and iteratively improve your governance needs in parallel with cloud adoption efforts. -->
