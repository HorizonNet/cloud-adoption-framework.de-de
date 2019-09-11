---
title: Leitfaden für Tests von Geschäftsabläufen (UAT) während der Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ein Prozess innerhalb der Cloudmigration, der sich auf die Aufgaben der Migration von Workloads in die Cloud konzentriert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0f1ba39ae283b1ab2fdb276310a9490af6bf87b7
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836632"
---
# <a name="guidance-for-business-testing-uat-during-migration"></a>Leitfaden für Tests von Geschäftsabläufen (UAT) während der Migration

Benutzerakzeptanztests während einer Unternehmenstransformation werden traditionell als eine IT-Funktion angesehen und können nur von der IT-Abteilung orchestriert werden. Allerdings wird diese Funktion häufig am effektivsten als eine Unternehmensfunktion ausgeführt. Die IT-Abteilung unterstützt dann diese Unternehmensaktivität, indem die Tests ermöglicht, Testpläne entwickelt und Tests nach Möglichkeit automatisiert werden. Obwohl die IT-Abteilung oft als Ersatz die Tests durchführen kann, sind die Beobachtungen realer Benutzer, die versuchen, eine neue Lösung im Kontext eines realen oder replizierten Geschäftsprozesses zu nutzen, unersetzlich.

> [!NOTE]
> Wenn automatisierte Tests verfügbar sind, stellen diese eine wesentlich effektivere und effizientere Möglichkeit zum Testen eines Systems dar. Allerdings liegt der Schwerpunkt von Cloudmigrationen häufig auf Legacysystemen oder zumindest stabilen Produktionssystemen. Oft werden diese Systeme nicht durch umfassende und gut gepflegte automatisierte Tests verwaltet. In diesem Artikel wird davon ausgegangen, dass zum Zeitpunkt der Migration keine solchen Tests verfügbar sind.

Statt automatisierter Tests können als zweite Möglichkeit Tests der Prozess- und Technologieänderungen durch Poweruser ausgeführt werden. Poweruser sind Personen, die gewöhnlich einen realen Prozess ausführen, der Interaktionen mit einem Technologietool oder einem Satz von Tools erfordert. Es kann sich dabei um einen externen Kunden handeln, der eine E-Commerce-Website für den Erwerb von Waren oder Dienstleistungen nutzt. Poweruser können auch eine Gruppe von Mitarbeitern sein, die einen Geschäftsprozess ausführen, z.B. als ein Call Center, das Kunden bedient und deren Erfahrungen aufzeichnet.

Das Ziel dieser Tests von Geschäftsabläufen ist es, eine Überprüfung durch Poweruser zu erhalten, um zu bestätigen, dass die neue Lösung den Erwartungen entspricht und Geschäftsprozesse nicht beeinträchtigt werden. Wird dieses Ziel nicht erreicht, dienen die Tests als Feedbackschleife, mit der definiert werden kann, wie und warum die Workload nicht den Erwartungen entspricht.

## <a name="business-activities-during-business-testing"></a>Unternehmensaktivitäten während der Tests von Geschäftsabläufen

Während der Tests von Geschäftsabläufen wird die erste Iteration manuell direkt mit Kunden durchgeführt. Dies ist die unverfälschteste, aber auch zeitaufwendigste Form einer Feedbackschleife.

- **Identifizieren von Powerusern.** Das Unternehmen hat in der Regel bessere Kenntnis über die Poweruser, die von einer technischen Änderung am stärksten betroffen sind.
- **Ausrichten und Vorbereiten von Powerusern.** Stellen Sie sicher, dass Poweruser die Geschäftsziele, die gewünschten Ergebnisse und die erwarteten Änderungen an Geschäftsprozessen verstehen. Bereiten Sie die Poweruser und deren Verwaltungsstruktur auf den Testprozess vor.
- **Aktive Teilnahme an der Interpretation der Feedbackschleife.** Helfen Sie den IT-Mitarbeitern, die Auswirkungen der verschiedenen Feedbackpunkte von Powerusern zu verstehen.
- **Klären der Prozessänderung.** Wenn die Transformation eine Änderung der Geschäftsprozesse auslösen kann, teilen Sie die Änderung und alle nachfolgenden Auswirkungen mit.
- **Priorisieren von Feedback.** Helfen Sie dem IT-Team bei der Priorisierung von Feedback basierend auf den Geschäftsauswirkungen.

Manchmal kann die IT-Abteilung Analysten oder Produktbesitzer einsetzen, die als Stellvertreter für die einzelnen Aktivitäten im Rahmen der Tests von Geschäftsabläufen fungieren können. Eine Beteiligung des Unternehmens wird jedoch dringend angeraten und wahrscheinlich zu positiven Geschäftsergebnissen führen.

## <a name="it-activities-during-business-testing"></a>IT-Aktivitäten während der Tests von Geschäftsabläufen

Die IT-Abteilung ist einer der Empfänger der Ergebnisse von Tests der Geschäftsabläufe. Die Feedbackschleifen, die sich während der Tests von Geschäftsabläufen ergeben, werden schließlich zu Arbeitselementen, die technische Änderungen oder Prozessänderungen definieren. Als Empfänger wird von der IT-Abteilung erwartet, dass sie bei der Umsetzung, der Sammlung von Feedback und der Verwaltung der daraus resultierenden technischen Maßnahmen hilft. Die von der IT-Abteilung während der Tests von Geschäftsabläufen ausgeführten typischen Aktivitäten umfassen Folgendes:

- Bereitstellung der Struktur und Logistik für Tests von Geschäftsabläufen.
- Hilfe bei der Umsetzung während der Tests.
- Bereitstellung eines Mittels und Verfahrens zur Aufzeichnung von Feedback.
- Unterstützung des Unternehmens bei der Priorisierung und Überprüfung von Feedback.
- Entwicklung von Plänen für Aktionen zu technischen Änderungen.
- Identifizieren vorhandener automatisierter Tests, mit denen die Tests von Powerusern optimiert werden können.
- Im Fall von Änderungen, die wiederholte Bereitstellungen oder Tests erfordern können: Untersuchen der Testprozesse, Definieren von Benchmarks und Erstellen einer Automatisierung zur weiteren Optimierung der Tests durch Poweruser.

## <a name="next-steps"></a>Nächste Schritte

In Verbindung mit Tests von Geschäftsabläufen kann die [Optimierung migrierter Ressourcen](./optimize.md) die Kosteneffizienz und Workloadleistung verbessern.

> [!div class="nextstepaction"]
> [Benchmarking und Größenänderung von Cloudressourcen](./optimize.md)
