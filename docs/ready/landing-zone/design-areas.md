---
title: Entwurfsbereich einer gut konzipierten Zielzone
description: Entwurfsbereich einer gut konzipierten Zielzone.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 2406e3671e6b4945a8fb87eb7ed29dbbbc0584ba
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88566576"
---
<!-- TODO: Refactor terms: "design area", "well-architected" -->

# <a name="design-areas-of-a-well-architected-landing-zone"></a>Entwurfsbereich einer gut konzipierten Zielzone

Jede Implementierungsoption für eine Azure-Zielzone bietet einen Bereitstellungsansatz und definierte Entwurfsprinzipien. Lesen vor dem Auswählen einer Implementierungsoption diesen Artikel, um sich mit diesen Entwurfsbereichen vertraut zu machen, die in der folgenden Tabelle aufgelistet sind.

> [!NOTE]
> Diese Entwurfsbereiche beschreiben, was Sie vor der Bereitstellung einer Zielzone in Betracht ziehen sollten. Verwenden Sie es als einfache Referenz. Informationen zu Entwurfsprinzipien und umsetzbaren Schritten für die Bereitstellung finden Sie in den [Implementierungsoptionen für Zielzonen](./implementation-options.md).  

## <a name="design-areas"></a>Entwurfsbereiche

Unabhängig von der Bereitstellungsoption sollten Sie jeden Entwurfsbereich sorgfältig prüfen. Ihre Entscheidungen beeinflussen das Fundament der Plattform, von dem jede Zielzone abhängt.

| Entwurfsbereiche | Ziel  | Relevante Methodiken |
|---|---|---|
| Unternehmensregistrierung | Für Unternehmenskunden mit einer Azure-Zusage ist die ordnungsgemäße Erstellung und Registrierung eines Mandanten ein wichtiger Schritt. | Bereit |
| Identity | IAM (Identity & Access Management, Identitäts- und Zugriffsverwaltung) ist eine primäre Sicherheitsgrenze in der öffentlichen Cloud. Sie stellt die Grundlage für jede sichere und vollständig kompatible Architektur dar. | Bereit |
| Netzwerktopologie und -konnektivität | Netzwerk- und Konnektivitätsentscheidungen sind ein gleichermaßen wichtiger grundlegender Aspekt jeder Cloudarchitektur. | Bereit |
| Ressourcenorganisation | Bei der Skalierung der Cloudeinführung haben Überlegungen zu Abonnements und zur Verwaltungsgruppenhierarchie Auswirkungen auf Governance, Vorgangsverwaltung und Einführungsmuster. | Steuern |
| Disziplinen der Governance | Automatisieren Sie die Überwachung und Durchsetzung von Sicherheits-, Governance- und Compliance-Richtlinien. | Steuern |
| Betriebsbaseline | Für stabile, laufende Vorgänge in der Cloud ist eine Betriebsbaseline erforderlich, um Transparenz, operative Compliance sowie Schutz- und Wiederherstellungsfunktionen zu gewährleisten. | Verwalten |
| Geschäftskontinuität und Notfallwiederherstellung (Business Continuity Disaster Recovery, BCDR) | BCDR stellt die Grundlage für Zuverlässigkeit und schnelle Wiederherstellung dar. | Verwalten |
| Bereitstellungsoptionen | Nutzen Sie die besten Tools und Vorlagen, um Ihre Zielzonen und die zugehörigen Ressourcen bereitzustellen. | Bereit |

## <a name="next-steps"></a>Nächste Schritte

Sie können diese Entwurfsbereiche im Laufe der Zeit implementieren, sodass Sie in Ihr Cloudbetriebsmodell hineinwachsen können. Es gibt jedoch auch vielfältige, wertende Implementierungsoptionen, bei denen in jedem Entwurfsbereich von einer definierten Position ausgegangen wird.

Wenn Sie mit den modularen Entwurfsbereichen vertraut sind, müssen Sie im nächsten Schritt die [Implementierungsoption für Zielzonen](./implementation-options.md) auswählen, die Ihrem Cloudeinführungsplan und den damit verbundenen Anforderungen am besten gerecht wird.

> [!div class="nextstepaction"]
> [Auswählen einer Implementierungsoption](./implementation-options.md)
