---
title: Erweitern der Zielzone
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie eine Zielzone erweitern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 39c036d0e57fc2b5ac8b45df7d065a950405eced
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94995141"
---
# <a name="expand-your-landing-zone"></a>Erweitern der Zielzone

Dieser Abschnitt der Bereitschaftsmethodik basiert auf den Prinzipien des [Refactorings der Zielzone](../landing-zone/refactor.md). Wie in diesem Artikel beschrieben, beseitigt ein auf Refactoring beruhender Ansatz für Infrastructure-as-Code Hindernisse für den geschäftlichen Erfolg und minimiert gleichzeitig das Risiko. In dieser Artikelreihe wird davon ausgegangen, dass Sie Ihre erste Zielzone bereitgestellt haben und diese nun entsprechend Ihren Unternehmensanforderungen erweitern möchten.

## <a name="shared-architecture-principles"></a>Gemeinsame Architekturprinzipien

Das Erweitern Ihrer Zielzone ist ein Code First-Ansatz, mit dem Sie die folgenden Prinzipien in die Zielzone und auf breiterer Basis in Ihre gesamte Cloudumgebung einbetten können.

![Gemeinsame Architekturprinzipien](../../_images/ready/shared-principles.png)
_Abbildung 1: Gemeinsame Architekturprinzipien_

[Azure Advisor](/azure/advisor/advisor-overview), das [Microsoft Azure Well-Architected Framework](/azure/architecture/framework) und die Lösungen in [Azure Architecture Center](/azure/architecture) beruhen auf den gleichen Architekturprinzipien.

## <a name="applying-these-principles-to-your-landing-zone-improvements"></a>Anwenden dieser Prinzipien auf die Verbesserungen Ihrer Zielzone

Zur Anpassung an die Methoden des Cloud Adoption Framework werden die oben genannten Prinzipien in umsetzbaren Verbesserungen der Zielzone zusammengefasst:

- Grundlegende Überlegungen: Gestalten Sie eine Zielzone um, um das Hosting, die Grundlagen und andere grundlegende Elemente zu optimieren.
- Operative Erweiterungen: Fügen Sie Konfigurationen für das operative Management hinzu, um **bessere Leistung und Zuverlässigkeit und einen optimalen Betrieb** zu gewährleisten.
- Governanceerweiterungen: Fügen Sie Governancekonfigurationen hinzu, um **Kosten, Zuverlässigkeit, Sicherheit** und Konsistenz zu verbessern.
- Sicherheitserweiterungen: Fügen Sie **Sicherheitskonfigurationen** hinzu, um den Schutz vertraulicher Daten und kritischer Systeme zu verbessern.

> [!WARNING]
> Einführungsteams, die mittelfristig (innerhalb von 24 Monaten) das Ziel haben, **mehr als 1.000 Ressourcen (Anwendungen, Infrastruktur oder Datenressourcen) in der Cloud zu hosten**, sollten jede dieser Erweiterungen schon in den frühen Phasen ihrer Cloudeinführungsjourney in Erwägung ziehen. Bei allen anderen Einführungsmustern können Erweiterungen der Zielzone als parallele Iteration durchgeführt werden, um frühzeitig geschäftliche Erfolge zu erzielen.

## <a name="next-steps"></a>Nächste Schritte

Bevor Sie Ihre erste Zielzone umgestalten, sollten Sie sich mit der [testgesteuerten Entwicklung von Zielzonen](./test-driven-development.md) vertraut machen.

> [!div class="nextstepaction"]
> [Testgesteuerte Entwicklung von Zielzonen](./test-driven-development.md)
