---
title: Voraussetzungen für die Migration
description: Hier finden Sie Informationen zu den Voraussetzungen, die Sie bei der Vorbereitung auf die Migration zur Cloud unterstützen und Ihnen dabei helfen, häufige Ursachen für Migrationsfehler zu vermeiden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 500df8bb2ff239a34b2eb87dbe9f6eb2f215c005
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222078"
---
# <a name="prerequisites-for-migration"></a>Voraussetzungen für die Migration

Bevor Sie mit der Migration beginnen, muss die _Umgebung_ Ihres Migrationsziels auf die bevorstehenden Änderungen vorbereitet werden. In diesem Fall bezieht sich die Umgebung auf die technische Grundlage in der Cloud. Umwelt umfasst auch das Geschäftsumfeld und die Einstellung, die die Migration vorantreibt. Ebenso umfasst die Umgebung die Kultur der Teams, die die Änderungen durchführen und die die Ergebnisse erhalten. Mangelnde Vorbereitung auf diese Änderungen ist der häufigste Grund für Fehler bei Migrationen. Diese Artikelreihe führt Sie durch die empfohlenen Voraussetzungen für die Vorbereitung der Umgebung.

## <a name="objective"></a>Ziel

Stellen Sie die geschäftliche, kulturelle und technische Bereitschaft sicher, bevor Sie mit einem iterativen Migrationsplan beginnen.

## <a name="review-business-drivers"></a>Überprüfen der geschäftlichen Faktoren

Bevor Sie mit der Cloudmigration beginnen, lesen Sie die Anleitung [Plan](../../../strategy/index.md) (Planen) und [Ready](../../../ready/index.md) (Bereit) im Cloud Adoption Framework, um sicherzustellen, dass Ihr Unternehmen auf Einführungs- und Migrationsprozesse für die Cloud vorbereitet ist. Überprüfen Sie insbesondere die Unternehmensanforderungen und die erwarteten Ergebnisse, die die Migration unterstützen:

- [Erste Schritte: Beschleunigen der Migration](../../../get-started/migrate.md)
- [„Warum wechseln wir in die Cloud?“](../../../strategy/motivations.md)

## <a name="definition-of-_done_"></a>Definition von _Fertig_.

Die Voraussetzungen sind erfüllt, wenn die folgenden Punkte zutreffen:

- **Geschäftliche Bereitschaft:** Das für die Cloudstrategie zuständige Team hat einen Migrationsbacklog auf hoher Ebene definiert und priorisiert, der den Anteil der digitalen Ressourcen darstellt, die in den nächsten zwei oder drei Releases migriert werden sollen. Das Cloudstrategieteam und das Cloudeinführungsteam haben sich auf eine erste Change Management-Strategie geeinigt.
- **Kulturbereitschaft:** Die Rollen, Aufgaben und Erwartungen der Teams für Cloudeinführung und Cloudstrategie sowie der betroffenen Benutzer wurden hinsichtlich der in den nächsten zwei oder drei Releases zu migrierenden Workloads vereinbart.
- **Technische Bereitschaft:** Die Landezone (oder zugeordneter Hostingbereich in der Cloud), die die migrierten Ressourcen erhält, erfüllt die Mindestanforderungen zum Hosten der ersten migrierten Workload.

> [!CAUTION]
> Die Vorbereitung ist der Schlüssel zum Erfolg einer Migration. Eine zu intensive Vorbereitung kann jedoch zu einer _Analysestarre_ führen, bei der eine zu umfassende Planung den Migrationsaufwand erheblich verzögern kann. Die in diesem Abschnitt definierten Prozesse und Voraussetzungen sollen Ihnen bei der Entscheidungsfindung helfen, aber lassen Sie sich nicht davon abhalten, sinnvolle Fortschritte zu erzielen.
>
> Wählen Sie für Ihre anfängliche Migration eine relativ einfache Workload. Verwenden Sie die in diesem Abschnitt beschriebenen Prozesse zum Planen und Durchführen dieser erstmaligen Migration. Dieser erste Migrationsaufwand wird Ihrem Team schnell die Grundsätze der Cloud vor Augen führen und es zwingen, sich über die Funktionsweise der Cloud zu informieren. Mit zunehmender Erfahrung Ihres Teams integrieren Sie diese Erfahrungen, wenn Sie größere und komplexere Migrationen durchführen.

## <a name="accountability-during-prerequisites"></a>Verantwortlichkeit während der Voraussetzungsphase

Zwei Teams sind für die Bereitschaft in der Voraussetzungsphase verantwortlich:

- **Cloudstrategieteam**: Dieses Team ist verantwortlich für die Identifizierung und Priorisierung der ersten zwei oder drei Workloads als Migrationskandidaten.
- **Cloudeinführungsteam**: Dieses Team ist verantwortlich für die Überprüfung der Bereitschaft der technischen Umgebung und der Durchführbarkeit der Migration der vorgeschlagenen Workloads.

Ein einzelnes Mitglied jedes Teams sollte für jede der drei Definitionen von erfolgten Aussagen im vorherigen Abschnitt als verantwortlich festgelegt werden.

## <a name="responsibilities-during-prerequisites"></a>Zuständigkeiten während der Voraussetzungsphase

Zusätzlich zur Verantwortlichkeit auf hoher Ebene gibt es Maßnahmen, für die eine Person oder Gruppe direkt verantwortlich sein muss. Im Folgenden sind einige dieser Verantwortlichkeiten aufgeführt, die diese Aktivitäten betreffen:

- **Geschäftspriorisierung** Treffen von Geschäftsentscheidungen in Bezug auf die zu migrierenden Workloads und allgemeine Zeitvorgaben. Weitere Informationen finden Sie unter [Geschäftliche Gründe für die Cloudmigration](../../../strategy/motivations.md).
- **Change Management-Bereitschaft** Erstellen und kommunizieren Sie den Plan zur Nachverfolgung technischer Änderungen während der Migration.
- **Ausrichtung der Geschäftskunden** Erstellen Sie einen Plan zur Vorbereitung der Geschäftskundencommunity auf die Durchführung der Migration.
- **Bestandsaufnahme und Analyse des digitalen Bestands** Die Ausführung der zur Bestandsaufnahme und Analyse des digitalen Bestands erforderlichen Tools. Weitere Informationen finden Sie im Framework für die Cloudeinführung in der Diskussion zu [digitalen Ressourcen](../../../digital-estate/index.md).
- **Cloudbereitschaft** Bewerten Sie die Zielbereitstellungsumgebung, um sicherzustellen, dass sie den Anforderungen der ersten wenigen Workloadkandidaten entspricht. Weitere Informationen finden Sie im [Leitfaden für die Azure-Einrichtung](../../../ready/azure-setup-guide/index.md).

Die restlichen Artikel dieser Reihe helfen bei der Durchführung der einzelnen Artikel.

## <a name="next-steps"></a>Nächste Schritte

Mit einem allgemeinen Überblick über die Voraussetzungen sind Sie bereit für die erste Voraussetzung: [Frühe Migrationsentscheidungen](./decisions.md).

> [!div class="nextstepaction"]
> [Frühe Migrationsentscheidungen](./decisions.md)
