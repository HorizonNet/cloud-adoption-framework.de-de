---
title: Entwurfsbereich einer gut konzipierten Zielzone
description: Entwurfsbereich einer gut konzipierten Zielzone.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ff839cb704ce79910fc29d6954712a0337a53e1e
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85077014"
---
# <a name="modular-design-areas-considered-by-all-azure-landing-zones"></a>Modulare Entwurfsbereiche, die von allen Azure-Zielzonen berücksichtigt werden

Jede Implementierungsoption für Azure-Zielzonen bietet einen Bereitstellungsansatz und definierte Entwurfsprinzipien, anhand derer Sie die folgenden Entwurfsbereiche implementieren können. Lesen vor dem Auswählen einer Implementierungsoption diesen Artikel, um sich mit diesen Entwurfsbereichen vertraut zu machen.

> [!NOTE]
> Die folgenden Entwurfsbereiche umfassen die Aspekte, die vor dem Bereitstellen einer Zielzone zu berücksichtigen sind. Dieser Artikel ist absichtlich weder detailliert noch praktisch verfasst, sondern soll lediglich als einfache Referenz dienen. Der nächste Schritt im Artikel zu [Implementierungsoptionen für Zielzonen](./implementation-options.md) liefert wertende Entwurfsprinzipien und praktische Schritte für die Bereitstellung.  

Ungeachtet der Bereitstellungsoption sollte jeder der folgenden Punkte bedacht werden, und es sind Entscheidungen für jeden Entwurfsbereich zu treffen. Diese Entscheidungen wirken sich auf die Plattformgrundlage aus, von der die einzelnen Zielzonen abhängig sind.

| Entwurfsbereiche  | Ziel  | Relevante Methodiken |
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

Wie Sie im nächsten Artikel feststellen werden, können diese Entwurfsbereiche allmählich implementiert werden, sodass Sie in Ihr Cloudbetriebssystem „hineinwachsen“. Es gibt jedoch auch vielfältige, wertende Implementierungsoptionen, bei denen in jedem Entwurfsbereich von einer definierten Position ausgegangen wird.

Wenn Sie mit den modularen Entwurfsbereichen vertraut sind, müssen Sie im nächsten Schritt die [Implementierungsoption für Zielzonen](./implementation-options.md) auswählen, die Ihrem Cloudeinführungsplan und den damit verbundenen Anforderungen am besten gerecht wird.

> [!div class="nextstepaction"]
> [Auswählen einer Implementierungsoption](./implementation-options.md)
