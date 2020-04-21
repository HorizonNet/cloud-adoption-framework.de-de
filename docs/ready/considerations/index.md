---
title: Erweitern der Zielzone
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie eine Zielzone erweitern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: cbfbadebd635891d680da29091ca572611712e09
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81120795"
---
# <a name="expand-your-landing-zone"></a>Erweitern der Zielzone

Dieser Abschnitt der Bereitschaftsmethodik basiert auf den Prinzipien des [Refactorings der Zielzone](../landing-zone/refactor.md). Wie in diesem Artikel beschrieben, beseitigt ein auf Refactoring beruhender Ansatz für Infrastructure-as-Code Hindernisse für den geschäftlichen Erfolg und minimiert gleichzeitig das Risiko. In dieser Artikelreihe wird davon ausgegangen, dass Sie Ihre erste Zielzone bereitgestellt haben und diese nun entsprechend Ihren Unternehmensanforderungen erweitern möchten.

## <a name="shared-architecture-principles"></a>Gemeinsame Architekturprinzipien

Das Erweitern Ihrer Zielzone ist ein Code First-Ansatz, mit dem Sie die folgenden Prinzipien in die Zielzone und auf breiterer Basis in Ihre gesamte Cloudumgebung einbetten können.

![Gemeinsame Architekturprinzipien](../../_images/ready/shared-principles.png)

[Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview), das [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework) und die Lösungen im [Azure Architecture Center](https://docs.microsoft.com/azure/architecture) beruhen auf den gleichen Architekturprinzipien.

## <a name="applying-these-principles-to-your-landing-zone-improvements"></a>Anwenden dieser Prinzipien auf die Verbesserungen Ihrer Zielzone

Zur Anpassung an die Methoden des Cloud Adoption Framework werden die oben genannten Prinzipien in umsetzbaren Verbesserungen der Zielzone zusammengefasst:

- Grundlegende Überlegungen: Gestalten Sie eine Zielzone um, um das Hosting, die Grundlagen und andere grundlegende Elemente zu optimieren.
- Operative Erweiterungen: Fügen Sie Konfigurationen für das operative Management hinzu, um **Leistung, Zuverlässigkeit und optimalen Betrieb** zu verbessern.
- Governanceerweiterungen: Fügen Sie Governancekonfigurationen hinzu, um **Kosten, Zuverlässigkeit, Sicherheit** und Konsistenz zu verbessern.
- Sicherheitserweiterungen: Fügen Sie **Sicherheitskonfigurationen** hinzu, um den Schutz vertraulicher Daten und kritischer Systeme zu verbessern.

> [!WARNING]
> Einführungsteams, die mittelfristig (innerhalb von 24 Monaten) das Ziel haben, **mehr als 1.000 Ressourcen (Apps, Infrastruktur oder Datenressourcen) in der Cloud zu hosten**, sollten jede dieser Erweiterungen schon in den frühen Phasen ihrer Cloudeinführungsjourney in Erwägung ziehen. Bei allen anderen Einführungsmustern können Erweiterungen der Zielzone als parallele Iteration durchgeführt werden, um frühzeitig geschäftliche Erfolge zu erzielen.

## <a name="next-steps"></a>Nächste Schritte

Bevor Sie Ihre erste Zielzone umgestalten, sollten Sie sich mit der [testgesteuerten Entwicklung von Zielzonen](./test-driven-development.md) vertraut machen.

> [!div class="nextstepaction"]
> [Testgesteuerte Entwicklung von Zielzonen](./test-driven-development.md)
