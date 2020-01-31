---
title: Bereitstellen des Cloudeinführungsplans für Azure DevOps
description: Bereitstellen der Vorlage für den Cloudeinführungsplan
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: a7e4dfda94b15a1e589ffadc9b13db57f4a70ef7
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76800116"
---
# <a name="cloud-adoption-plan-and-azure-devops"></a>Cloudeinführungsplan und Azure DevOps

Azure DevOps ist der Satz cloudbasierter Tools für Azure-Kunden, die iterative Projekte verwalten. Es enthält darüber hinaus Tools für die Verwaltung von Bereitstellungspipelines und andere wichtige Elemente von DevOps. 

In diesem Artikel erfahren Sie, wie Sie mithilfe der Vorlage für den Cloudeinführungsplan schnell einen Backlog für Azure DevOps bereitstellen können. Diese Vorlage richtet die Maßnahmen zur Einführung der Cloud auf einen standardisierten Prozess aus, der auf den Vorgaben im Framework für die Cloudeinführung (Cloud Adoption Framework) basiert.

## <a name="create-your-cloud-adoption-plan"></a>Erstellen Ihres Cloudeinführungsplans

Um den Cloudeinführungsplan bereitzustellen, öffnen Sie den [Azure DevOps-Demo-Generator](https://aka.ms/adopt/plan/generator). Dieses Tool stellt die Vorlage für Ihren Azure DevOps-Mandanten bereit. Zur Verwendung des Tools sind die folgenden Schritte erforderlich:

1. Stellen Sie sicher, dass das Feld **Ausgewählte Vorlage** auf **Cloudeinführungsplan** festgelegt ist. Wenn dies nicht der Fall ist, wählen Sie **Vorlage auswählen** aus, um die richtige Vorlage auszuwählen.
2. Wählen Sie Ihre Azure DevOps-Organisation im Dropdown-Listenfeld **Organisation auswählen** aus.
3. Geben Sie einen Namen für das neue Projekt ein. Dieser Name wird für den Cloudeinführungsplan verwendet, wenn er in Ihrem Azure DevOps-Mandanten bereitgestellt wird.
4. Wählen Sie **Projekt erstellen** aus, um basierend auf der Planvorlage ein neues Projekt in Ihrem Mandanten zu erstellen. Eine Statusanzeige zeigt Ihren Fortschritt bei der Bereitstellung des Projektes an.
5. Wenn die Bereitstellung abgeschlossen ist, wählen Sie **Zu Projekt navigieren** aus, um Ihr neues Projekt anzuzeigen.

Nachdem Ihr Projekt erstellt wurde, lesen Sie weitere Artikel in dieser Serie, um zu erfahren, wie Sie die Vorlage an Ihren Cloudeinführungsplan anpassen können.

Zusätzliche Unterstützung und Anleitung zu diesem Tool finden Sie unter [Azure DevOps Services-Demo-Generator](https://docs.microsoft.com/azure/devops/demo-gen/?toc=/azure/devops/demo-gen/toc.json&bc=/azure/devops/demo-gen/breadcrumb/toc.json&view=azure-devops).

## <a name="bulk-edit-the-cloud-adoption-plan"></a>Massenbearbeitung des Cloudeinführungsplans

Wenn das Planprojekt bereitgestellt wurde, können Sie es mithilfe von Microsoft Excel ändern. Neue Workloads oder Ressourcen lassen sich wesentlich einfacher mit Excel im Plan erstellen, als mithilfe der Azure DevOps-Browsererfahrung.

Um Ihre Arbeitsstation für die Massenbearbeitung vorzubereiten, lesen Sie [Massenhinzufügen oder -bearbeiten von Arbeitselementen mit Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="use-the-cloud-adoption-plan"></a>Verwenden des Cloudeinführungsplans

Der Cloudeinführungsplan organisiert die Aktivitäten nach Aktivitätsarten:

- **Epics:** Ein *Epic* repräsentiert eine vollständige Phase des Lebenszyklus der Cloudeinführung.
- **Funktionen:** Features werden verwendet, um bestimmte Ziele innerhalb einer Phase zu organisieren. Beispielsweise wäre die Migration einer bestimmten Workload ein Feature.
- **User Storys:** User Storys gruppieren Arbeit in logische Sammlungen von Aktivitäten, die auf einem bestimmten Ziel basieren.
- **Aufgaben:** Aufgaben stellen die eigentlich zu erledigenden Arbeiten dar.

Auf jeder Ebene werden die Aktivitäten dann basierend auf den Abhängigkeiten sequenziert. Aktivitäten sind mit Artikeln im Cloud Adoption Framework verknüpft, um das vorliegende Ziel oder die Aufgabe zu verdeutlichen.

Die übersichtlichste Darstellung des Cloudeinführungsplans stammt aus der **Epics** Backlog-Ansicht. Hilfe beim Wechseln in die [Epics](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops#view-a-backlog-or-portfolio-backlog) Backlog-Ansicht finden Sie im Artikel zum **Anzeigen eines Backlogs**. Anhand dieser Ansicht können Sie die Arbeiten, die erforderlich sind, um die aktuelle Phase des Einführungslebenszyklus abzuschließen, einfach planen und verwalten.

> [!NOTE]
> Der aktuelle Status des Cloudeinführungsplans ist stark auf die Migrationsmaßnahmen ausgerichtet. Aufgaben im Zusammenhang mit Governance, Innovation oder Betriebsabläufen müssen manuell aufgefüllt werden.

## <a name="align-the-cloud-adoption-plan"></a>Ausrichten des Cloudeinführungsplans

Die Übersichtsseiten für die Strategie- und Planungsphasen des Lebenszyklus der Cloudeinführung verweisen jeweils auf die [Strategie- und Planungsvorlage des Cloud Adoption Framework](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Diese Vorlage organisiert die Entscheidungen und Datenpunkte, die die Vorlage für den Cloudeinführungsplan auf Ihre spezifischen Einführungspläne abstimmen. Wenn dies noch nicht geschehen ist, sollten Sie die Übungen zu [Strategie](../strategy/index.md) und [Planung](../plan/index.md) durchführen, bevor Sie Ihr neues Projekt ausrichten.

Die folgenden Artikel bieten Informationen zur Ausrichtung des Cloudeinführungsplans:

- [Workloads](./workloads.md): Ausrichten von Features innerhalb des Epics „Cloudmigration“, um jede zu migrierende oder zu modernisierende Workload zu erfassen. Fügen Sie diese Features hinzu, und ändern Sie sie, um den Aufwand für die Migration Ihrer 10 wichtigsten Workloads zu erfassen.
- [Ressourcen](./assets.md): Jede Ressource (VM, Anwendung oder Daten) wird durch die User Storys für jede Workload repräsentiert. Fügen Sie diese User Storys hinzu, und ändern Sie sie, um sie an Ihren digitalen Ressourcen anzupassen.
- [Rationalisierung](./review-rationalization.md): Da jede Workload definiert ist, können die anfänglichen Annahmen zu dieser Workload hinterfragt werden. Dies kann zu Änderungen an den Aufgaben für jede Ressource führen.
- [Releasepläne erstellen](./iteration-paths.md): Iterationspfade erstellen Releasepläne, indem sie den Aufwand an verschiedene Releases und Iterationen ausrichten.
- [Zeitachse festlegen](./timelines.md): Durch die Definition von Start- und Enddatum für jede Iteration wird eine Zeitachse für die Verwaltung des gesamten Projekts erstellt.

Diese fünf Artikel helfen bei allen Anpassungsaufgaben, die erforderlich sind, um mit der Verwaltung von Einführungsmaßnahmen zu beginnen. Mit dem nächste Schritt beginnen Sie mit der Ausrichtungsübung.

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der Ausrichtung Ihres Planprojekts, indem Sie [Workloads definieren und priorisieren](./workloads.md).

> [!div class="nextstepaction"]
> [Definieren und Priorisieren von Workloads](./workloads.md)
