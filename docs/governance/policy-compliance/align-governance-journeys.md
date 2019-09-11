---
title: Ausrichten Ihres Cloud Governance-Entwurfshandbuchs an der Unternehmensrichtlinie
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ausrichten Ihres Cloud Governance-Entwurfshandbuchs an der Unternehmensrichtlinie
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 2804030fda17638fc86bc6265841abdd56903d0d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837080"
---
<!---
I've established policies. How to help developers adopt these policies?
Draft an architecture design guide.

[Aspirational statement] If you're using Azure, you can use one of ours as a starting point. The choose one of the following 6 as a starting point and mold it to fit your policies.
--->

# <a name="align-your-cloud-governance-design-guide-with-corporate-policy"></a>Ausrichten Ihres Cloud Governance-Entwurfshandbuchs an der Unternehmensrichtlinie

Nachdem Sie [Cloudrichtlinien definiert](define-policy.md) haben, die auf Ihren [identifizierten Risiken](understanding-business-risk.md) basieren, müssen Sie handlungsrelevante Leitfäden generieren, die an diese Richtlinien für Ihre IT-Mitarbeiter und Entwickler angepasst sind, damit sie sich darauf beziehen können. Durch Erstellen eines Entwurfshandbuchs für die Cloudgovernance können Sie basierend auf den Richtlinienanweisungen, die Sie für jede der fünf [Governancedisziplinen](../governance-disciplines.md) generiert haben, bestimmte strukturelle, technologische und prozessbezogene Optionen angeben.

Ein Entwurfshandbuch zur Cloud-Governance sollte die Architekturoptionen und Entwurfsmuster für jede der zentralen Infrastrukturkomponenten von Cloudbereitstellungen einrichten, die Ihre Richtlinienanforderungen am besten erfüllen. Neben diesen sollten Sie eine allgemeine Erläuterung der Technologie, Tools und Prozesse liefern, die jede dieser Entwurfsentscheidungen unterstützen werden.

Obwohl Ihre Risikoanalyse und Richtlinienanweisungen zu einem gewissen Grad unabhängig von der Cloudplattform sein können, sollte Ihr Entwurfshandbuch plattformspezifische Implementierungsdetails für Ihre IT und Entwickler enthalten. Konzentrieren Sie sich auf die Architektur, Tools und Features Ihrer gewählten Plattform, wenn Sie Ihre Entwurfsentscheidung treffen und einen Leitfaden bereitstellen.

Während Cloud-Entwurfshandbücher einige der technischen Details berücksichtigen sollten, die mit den einzelnen Infrastrukturkomponenten verbunden sind, sollen sie keine umfangreichen technischen Dokumente oder Spezifikationen sein. Stellen Sie sicher, dass Ihre Handbücher Ihre Richtlinienanweisungen behandeln, und geben Sie die Entwurfsentscheidungen in einem Format an, das für Ihre Mitarbeiter einfach zu verstehen ist und zur Referenz verwendet werden kann.

<!-- markdownlint-enable MD033 -->

## <a name="using-the-actionable-governance-guides"></a>Verwenden der umsetzbaren Governanceleitfäden

Wenn Sie planen, die Azure-Plattform für Ihre Cloudeinführung zu nutzen, bietet das Cloud Adoption Framework [umsetzbare Governanceleitfäden](../journeys/index.md), um den inkrementellen Ansatz des Governancemodells für das Cloud Adoption Framework zu veranschaulichen. Diese beschreibenden Leitfäden decken einen Bereich von allgemeinen Einführungsszenarien ab, darunter die Geschäftsrisiken, Toleranzanforderungen und Richtlinienanweisungen, die in die Erstellung eines Minimum Viable Product (MVP) für die Governance einbezogen wurden. Diese Leitfäden stellen eine Synthese aus realen Benutzererfahrungen beim Prozess der Cloudeinführung in Azure dar.

Während es bei jeder Cloudeinführung eindeutige Ziele, Prioritäten und Herausforderungen gibt, sollten diese Beispiele eine gute Vorlage für die Umwandlung Ihrer Richtlinie in einen Leitfaden liefern. Wählen Sie das Ihrer Situation am besten entsprechende Szenario als Ausgangspunkt aus, und passen Sie es an Ihre spezifischen Richtlinienanforderungen an.

## <a name="next-steps"></a>Nächste Schritte

Nach Abschluss des Entwurfsleitfadens richten Sie Prozesse zur Einhaltung von Richtlinien ein, um die Richtlinienkonformität sicherzustellen.

> [!div class="nextstepaction"]
> [Festlegen von Prozessen zur Einhaltung von Richtlinien](./processes.md)
