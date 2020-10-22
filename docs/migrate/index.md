---
title: Cloudmigration
description: Bereiten Sie sich mithilfe eines iterativen Prozesses zur Bewertung, Migration, Optimierung, Sicherung und Verwaltung von Workloads auf eine erfolgreiche Migration zu Azure vor.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: seo-azure-migrate
ms.openlocfilehash: 8549f6719acdc13e32f005f085c1e99ec1d53b7d
ms.sourcegitcommit: c1d6c1c777475f92a3f8be6def84f1779648a55c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2020
ms.locfileid: "92334917"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Cloudmigration im Cloud Adoption Framework

Der [Cloudeinführungsplan](../plan/index.md) jedes Unternehmens beinhaltet Workloads, die keine umfangreichen Investitionen in die Erstellung neuer Geschäftslogik rechtfertigen. Diese Workloads können mithilfe verschiedener Methoden in die Cloud migriert werden: per Lift & Shift, per Lift & Optimize oder mittels Modernisierung. Jeder diese Methoden wird als Migration betrachtet. In den folgenden Aufgaben werden die iterativen Prozesse zum Bewerten, Migrieren, Optimieren, Schützen und Verwalten dieser Workloads vermittelt.

Zur Vorbereitung auf diese Phase des Cloudeinführungszyklus werden die folgenden Schritte empfohlen:

| <span title="Symbol">&nbsp;</span> | <span title="Beschreibung">&nbsp;</span> |
|--|--|
| <br> :::image type="icon" source="../_images/icons/1.png"::: | <br> [Migrieren Ihrer ersten Workload](./azure-migration-guide/index.md): Machen Sie sich mithilfe des Leitfadens zur Azure-Migration mit den nativen Azure-Tools und dem Ansatz für die Migration vertraut. |
| <br> :::image type="icon" source="../_images/icons/2.png"::: | <br> [Migrationsszenarios](./azure-best-practices/index.md): Nutzen Sie zusätzliche Migrationstools und -ansätze für weitere Migrationsszenarien. |
| <br> :::image type="icon" source="../_images/icons/3.png"::: | <br> [Bewährte Methoden:](./azure-best-practices/index.md) Gehen Sie allgemeine Migrationsanforderungen durch die Anwendung einheitlicher Best Practices an. |
| <br> :::image type="icon" source="../_images/icons/4.png"::: | <br> [Prozessverbesserungen](./migration-considerations/index.md): Die Migration ist stark prozessorientiert. Nutzen Sie diese Prozessverbesserungen, um verschiedene Aspekte Ihrer Migration zu bewerten und weiterzuentwickeln und auf Veränderungen bei den Migrationsaufgaben zu reagieren. |

Diese Migrationsmethodik und die obigen Schritte basieren auf den folgenden Annahmen:

<!-- docutune:casing "Plan, Ready, and Adopt methodologies" -->

- Die Methodik zum Steuern von Migrationssprints steht im Einklang mit Migrationswellen oder -releases, die mithilfe der Methoden „Planung“, „Bereitschaft“ und „Einführung“ definiert werden. Innerhalb jedes Migrationssprints wird ein Batch von Workloads zur Cloud migriert.
- Vor der Migration von Workloads wurde mindestens eine [Zielzone](../ready/index.md) identifiziert, konfiguriert und bereitgestellt, um die Anforderungen des kurzfristigen Cloudeinführungsplan zu erfüllen.
- Migration wird üblicherweise mit den Begriffen _Lift & Shift_ oder _Rehosten_ assoziiert. Diese Methodik und die oben genannten Schritte basieren auf der Überzeugung, dass kein Rechenzentrum (und nur wenige Workloads) mit einem reinen Rehostingansatz migriert werden sollten. Zwar können viele Workloads neu gehostet werden, aber Kunden entscheiden sich häufiger dafür, bestimmte Ressourcen innerhalb der einzelnen Workloads zu modernisieren. Während dieses iterativen Prozesses ist die Balance zwischen Geschwindigkeit und Modernisierung ein gängiger Diskussionspunkt.

## <a name="migration-effort"></a>Migration

Die erforderlichen Aufgaben zum Migrieren von Workloads lassen sich in der Regel in drei Phasen unterteilen: Bewerten von Workloads, Bereitstellen von Workloads und Freigeben von Workloads. In diesem Abschnitt des Cloud Adoption Framework erfahren Sie, wie Sie den größtmöglichen Nutzen aus jeder der Phasen ziehen, die die Migration einer Workload zur Produktion erfordert.

In einer normalen zweiwöchigen Iteration kann ein erfahrenes Migrationsteam diesen Prozess für zwei bis fünf Workloads von geringer bis mittlerer Komplexität durchführen. Für komplexere Workloads (z. B. SAP) können mehrere zweiwöchige Iterationen erforderlich sein, um alle drei Phasen der Migration für eine einzelne Workload abzuschließen. Sowohl die Erfahrung als auch die Komplexität haben erheblichen Einfluss auf die Zeitpläne und die Geschwindigkeit der Migration.

![Cloud Adoption Framework: Migration](../_images/migrate/methodology.png)

Im Folgenden finden Sie einen Überblick über die Phasen des oben dargestellten Prozesses:

- **Bewerten von Workloads:** Bewerten Sie Workloads, um die Kosten, Möglichkeiten zur Modernisierung und Bereitstellungstools auszuwerten. Bei diesem Prozess geht es primär darum, die bei früheren Ermittlungen und Bewertungen getroffenen Annahmen zu validieren bzw. zu prüfen, indem Sie sich die Rationalisierungsoptionen genauer ansehen. In dieser Phase werden auch Benutzermuster und Abhängigkeiten genauer untersucht, um sicherzustellen, dass die Workloads sich nach der Migration als technisch erfolgreich erweisen.
- **Bereitstellen von Workloads:** Nachdem Workloads bewertet wurden, werden die vorhandenen Funktionen dieser Workloads in der Cloud repliziert (oder verbessert). Dies kann einen _Lift & Shift_-Ansatz oder das _Rehosting_ in der Cloud beinhalten. Meistens werden in dieser Phase jedoch viele der Ressourcen modernisiert, die diese Workloads unterstützen, um die Vorteile der Cloud zu nutzen.
- **Freigeben von Workloads:** Nachdem die Funktionen in der Cloud repliziert wurden, können Workloads getestet, optimiert, dokumentiert und für laufende Vorgänge veröffentlicht werden. Kritisch sind während dieses Prozesses die Bewertung der migrierten Workloads und ihre Übergabe an Governance-, operative Management- und Sicherheitsteams für den kontinuierlichen Support.

> [!NOTE]
> In einigen frühen Iterationen der Migration ist es üblich, sich auf eine einzelne Workload zu beschränken. Diese Vorgehensweise sorgt für einen maximalen Erhalt von Qualifikationen und bietet dem Team mehr Zeit zum Experimentieren und Lernen.
> [!NOTE]
> Beim Erstellen einer Migrationsfactory entscheiden sich manche Teams vielleicht, jede der obigen Phasen auf mehrere Teams und mehrere Sprints zu verteilen. Diese Vorgehensweise kann die Wiederholbarkeit verbessern und die Migration beschleunigen.

## <a name="migration-waves-and-iterative-change-management"></a>Migrationswellen und iteratives Change Management

Migrationsiterationen bieten durch die Migration von Ressourcen und Workloads technischen Nutzen. Eine Migrationswelle ist die kleinste Sammlung von Workloads, die einen greif- und messbaren geschäftlichen Mehrwert bieten. Am Ende jeder Iteration sollte ein Bericht über die durchgeführten technischen Aufgaben erstellt werden. Über geschäftliche Veränderungen und die strategische Planung wird jedoch in der Regel auf etwas höherer Ebene entschieden. Während sich das Cloudeinführungsteam um die Migration kümmert, konzentriert sich das Cloudstrategieteam auf die Planung der nächsten ein bis zwei Migrationswellen. Das Cloudstrategieteam verfolgt auch den technischen Fortschritt in Form einer Lernmetrik nach, um die Zeitvorgaben für die geschäftliche Wertschöpfung besser zu verstehen. In dieser Hinsicht sind Migrationswellen die iterative Change Management-Methode zur Nachverfolgung von Geschäftsergebnissen, beteiligten Personen und Zeitplänen.

Wie die Grafik im vorherigen Abschnitt zeigt, bieten Prozesse innerhalb der Methoden [Planung](../plan/index.md) und [Bereitschaft](../ready/index.md) sowie in gewissem Maße innerhalb der Methode [Strategie](../strategy/index.md) des Cloud Adoption Framework Leitlinien für die Planung und Verwaltung der Migrationswellen. Durch die Verwaltung dieser Wellen werden die Migrationsaufgaben priorisiert und definiert, die von den technischen Teams erledigt werden müssen.

## <a name="next-steps"></a>Nächste Schritte

Die oben aufgeführten Schritte und nachfolgende Leitfäden zur Migrationsmethodik können Ihnen bei der Entwicklung von Qualifikationen helfen, die Prozesse innerhalb der einzelnen Migrationssprints verbessern. Der [Leitfaden zur Azure-Migration](./azure-migration-guide/index.md) ist eine kurze Artikelreihe, in der die gängigsten Tools und Ansätze für Ihre erste Migrationswelle erläutert werden.

> [!div class="nextstepaction"]
> [Leitfaden zur Azure-Migration](./azure-migration-guide/index.md)
