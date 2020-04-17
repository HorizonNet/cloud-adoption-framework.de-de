---
title: Cloudbetriebsmodell ist jetzt das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um ausführliche Informationen zur Beschleunigung Ihrer Cloudeinführung zu erhalten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d1ba5e26214a0b60a4fe9fefb23d1dffaf8fa4ed
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "79023868"
---
# <a name="cloud-operating-model-is-now-part-of-the-microsoft-cloud-adoption-framework-for-azure"></a>DAs Cloudbetriebsmodell ist jetzt Bestandteil des Frameworks für die Cloudeinführung (Cloud Adoption Framework) für Microsoft Azure.

Anfang 2018 hat Microsoft das Cloudbetriebsmodell (Cloud Operating Model, COM) veröffentlicht. Das COM war eine Anleitung, die unseren Kunden dabei half, die **Gegenstände** und **Gründe** der digitalen Transformation zu verstehen. Dies hat den Kunden dabei geholfen, ein Gefühl für all die Bereiche zu bekommen, die berücksichtigt werden mussten: Geschäftsstrategie, kulturelle Strategie und technologische Strategie. Im COM nicht enthalten waren die spezifischen _Schrittanleitungen_, sodass sich unsere Kunden gefragt haben, wie sie weiter vorgehen sollten.

Im Oktober 2018 haben wir mit einer Überprüfung aller Modelle begonnen, die sich in der Microsoft-Community vermehrt hatten, sodass wir grob 60 verschiedene Cloudeinführungsmodelle gefunden haben. Ein interdisziplinäres Microsoft-Team wurde eingerichtet, um alles in Form eines einzigen, dedizierten technischen „Produkts“ zusammenzuführen, mit definierten Implementierungen für Dienste, Vertrieb und Marketing. Diese Bemühungen gipfelten in der Erstellung eines einzigen Modells, dem Microsoft Cloud Adoption Framework für Azure (Framework für die Cloudeinführung), entworfen, um Kunden beim Verständnis der **Gegenstände** und **Gründe** zu helfen sowie einheitliche Anleitungen zur **Vorgehensweise** zu bieten, um ihre Cloudeinführung zu beschleunigen. Das Ziel dieses Projekts ist die Erstellung eines One Microsoft-Ansatzes für die Cloudeinführung.

## <a name="using-cloud-operating-model-practices-within-the-cloud-adoption-framework"></a>Die Verwendung von Cloudbetriebsmodell-Methoden innerhalb des Frameworks für die Cloudeinführung

Für einen ähnlichen Ansatz bei COM sollten die Leser mit einem der folgenden Artikel beginnen:

- [Beginnen einer Cloudmigrationsjourney](../getting-started/migrate.md)
- [Innovation durch Einführung der Cloud](../getting-started/innovate.md)
- [Ermöglichen einer erfolgreichen Cloudeinführung](../getting-started/enable.md)

Die zuvor in COM bereitgestellten Anleitungen sind nach wie vor für das Framework für die Cloudeinführung relevant. Die Erfahrung ist anders, aber die Struktur des Frameworks für die Cloudeinführung ist lediglich eine Erweiterung dieser Anleitungen. Um von COM zum Framework für die Cloudeinführung zu wechseln, ist ein Verständnis des Umfangs und der Struktur wichtig. Dieser Übergang wird in den folgenden zwei Abschnitten beschrieben.

## <a name="scope"></a>`Scope`

COM hat einen Umfang erzeugt, der aus den folgenden Komponenten besteht:

![Umfang des Frameworks für die Cloudeinführung](../_images/caf-scope.png)

- **Unternehmensstrategie:** Legen Sie klare Geschäftsziele und -ergebnissen fest, die durch die Einführung der Cloud unterstützt werden sollen.
- **Technologiestrategie:** Passen Sie die allumfassende Strategie, an der sich die Einführung der Cloud orientiert, an Ihre Geschäftsstrategie an.
- **Mitarbeiterstrategie**: Entwickeln Sie eine Strategie für die Schulung der Mitarbeiter, und ändern Sie die Unternehmenskultur, um geschäftlichen Erfolg zu ermöglichen.

Die Umfänge des Cloudbetriebsmodell und des Frameworks für die Cloudeinführung, die auf einer sehr hohen Ebene angelegt sind, sind ähnlich. Unternehmen/Geschäft, Kultur und Technologie sind im gesamten Anleitungswerk und in jeder Methodik innerhalb des Frameworks für die Cloudeinführung abgebildet.

> [!NOTE]
> Der Umfang des Cloud Adoption Framework weist zwei signifikante klare Punkte auf. Im Framework für die Cloudeinführung geht die Geschäftsstrategie über die Dokumentation von Cloudkosten hinaus. Es geht dabei um das Verständnis von Motivationen, gewünschten Ergebnissen, Umsätzen und Cloudkosten, um umsetzbare Pläne und klare geschäftliche Begründungen zu erstellen. Im Framework für die Cloudeinführung geht die Mitarbeiterstrategie über Schulungen hinaus, um Ansätze zu berücksichtigen, die nachweisliche kulturelle Reife erzeugen. Einige Bereiche der Roadmap umfassen Demonstrationen der Auswirkungen von agiler Verwaltung, DevOps-Integration, Kundenempathie und Besessenheit sowie von schlanken Produktentwicklungsansätzen.

## <a name="structure"></a>Struktur

COM enthielt eine Infografik, die die verschiedenen Entscheidungen und Aktionen umriss, die während der Anstrengungen einer Cloudeinführung erforderlich sind. Diese Grafik bot ein definiertes Mittel zur Kommunikation von Folgeschritten und abhängigen Entscheidungen.

Das Framework für die Cloudeinführung befolgt ein ähnliches Modell. Da sich aber die Aktionen und Entscheidungen zu mehreren Entscheidungsstrukturen verzweigt haben, wurde eine einzelne Grafik durch diese Komplexität schnell überfordernd. Um die Anleitungen zu vereinfachen und somit direkter umsetzbar zu machen, wurde die einzelne Grafik in die folgenden Strukturen zerlegt.

Auf Ebene der Unternehmensführung wurde das Framework für die Cloudeinführung zu den folgenden drei Phasen der Einführung und zwei primären Governancerichtlinien vereinfacht.

![Struktur des Frameworks für die Cloudeinführung auf Ebene der Unternehmensführung](../_images/caf-structure.png)

Die drei Phasen der Einführung sind:

- **Planung:** Entwickeln Sie den Businessplan, um die Cloudeinführung in Einklang mit den gewünschten Geschäftsergebnisse zu leiten.
- **Bereit:** Bereiten Sie die Mitarbeiter, die Organisation und die technische Umgebung auf die Ausführung des Einführungsplans vor.
- **Einführung:** Die technische Strategie, die für die Ausführung eines spezifischen Einführungsplans in Einklang mit einem bestimmten Einführungsweg erforderlich ist, um Geschäftsergebnisse zu erzielen.

Die drei Phasen der Cloudeinführung wurden zwei spezifischen Wegen zugeordnet:

- [Migration](../getting-started/migrate.md): Vorhandene Workloads in die Cloud verlagern.
- [Innovation](../getting-started/innovate.md): Vorhandene Workloads modernisieren und neue Produkte und Dienste erstellen.

Zusätzliche Ressourcen, die erforderlich sind, um bei der Cloudeinführung erfolgreich zu sein, finden Sie unter [Ermöglichen einer erfolgreichen Einführung](../getting-started/enable.md).

## <a name="next-steps"></a>Nächste Schritte

Um Ihren Weg fortzusetzen, wo COM aufgehört hat, wählen Sie einen der folgenden Cloudeinführungswege:

- [Erste Schritte bei der Cloudmigration](../getting-started/migrate.md)
- [Erste Schritte bei der cloudaktivierten Innovation](../getting-started/innovate.md)
- [Ermöglichen einer erfolgreichen Einführung](../getting-started/enable.md)
