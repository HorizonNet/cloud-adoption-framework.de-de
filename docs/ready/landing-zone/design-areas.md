---
title: Entwurfsbereich einer gut konzipierten Zielzone
description: Entwurfsbereich einer gut konzipierten Zielzone.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 3c3284f9f04a57e8532c0371197e1af7802e4fca
ms.sourcegitcommit: 5b537035b96ae2b6879a1ea7fd46ceb64626851d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/01/2020
ms.locfileid: "89275364"
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
| Geschäftskontinuität und Notfallwiederherstellung (Business Continuity Disaster Recovery, BCDR) | Resilienz ist der Schlüssel für das reibungslose Funktionieren von Anwendungen. BCDR ist eine wichtige Komponente der Resilienz. BCDR umfasst den Schutz von Daten durch Sicherungen und den Schutz von Anwendungen vor Ausfällen durch Notfallwiederherstellung. | Verwalten |
| Bereitstellungsoptionen | Nutzen Sie die besten Tools und Vorlagen, um Ihre Zielzonen und die zugehörigen Ressourcen bereitzustellen. | Bereit |

## <a name="next-steps"></a>Nächste Schritte

Sie können diese Entwurfsbereiche im Laufe der Zeit implementieren, sodass Sie in Ihr Cloudbetriebsmodell hineinwachsen können. Es gibt jedoch auch vielfältige, wertende Implementierungsoptionen, bei denen in jedem Entwurfsbereich von einer definierten Position ausgegangen wird.

Wenn Sie mit den modularen Entwurfsbereichen vertraut sind, müssen Sie im nächsten Schritt die [Implementierungsoption für Zielzonen](./implementation-options.md) auswählen, die Ihrem Cloudeinführungsplan und den damit verbundenen Anforderungen am besten gerecht wird.

> [!div class="nextstepaction"]
> [Auswählen einer Implementierungsoption](./implementation-options.md)
