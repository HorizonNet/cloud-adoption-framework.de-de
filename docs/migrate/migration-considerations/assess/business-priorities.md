---
title: Geschäftliche Prioritäten während eines Transformationsprozesses
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie während eines langen Transformationsprozesses die richtige geschäftliche Abstimmung aufrechterhalten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: df41ee9dfe94d0279f8a0c29982e8aff2dd83782
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312049"
---
# <a name="business-priorities-maintaining-alignment"></a>Geschäftliche Prioritäten: Ausrichten auf die Beibehaltung

*Transformation* wird häufig als eine drastische oder spontane Änderung definiert. Auf Boardebene kann die Änderung wie eine erhebliche Transformation erscheinen. Für diejenigen aber, die den Änderungsprozess in einer Organisation schrittweise durchlaufen, ist der Begriff Transformation etwas irreführend. Im Kern wird Transformation besser als eine Reihe sorgfältig ausgeführter Übergänge von einem Zustand in einen anderen beschrieben.

Die Zeitspanne, die für die Rationalisierung oder den Übergang einer Workload benötigt wird, variiert je nach technischer Komplexität. Selbst wenn dieser Prozess schnell auf eine einzelne Workload oder eine Gruppe von Anwendungen angewendet werden kann, dauert es einige Zeit, bis wesentliche Änderungen innerhalb einer Benutzerbasis umgesetzt sind. Es braucht länger, bis sich Änderungen über verschiedene Ebenen bestehender Geschäftsprozesse fortsetzen. Wenn erwartet wird, dass die Transformation Verhaltensmuster von Kunden prägt, kann es länger dauern, bis signifikante Ergebnisse erzielt werden.

Leider wartet der Markt nicht, bis ein Übergang in einem Unternehmen erfolgt ist. Die Verhaltensmuster von Kunden ändern sich von selbst – und das oft unerwartet. Die Wahrnehmung eines Unternehmens und seiner Produkte auf dem Markt kann durch soziale Medien oder die Positionierung eines Wettbewerbers beeinflusst werden. Schnelle und unerwartete Marktänderungen machen es erforderlich, dass Unternehmen flexibel sind und schnell reagieren.

Die Fähigkeit zum Ausführen von Prozessen und technischen Übergängen erfordert konsistente und stabile Maßnahmen. Um auf die Marktbedingungen zu reagieren, sind schnelle Entscheidungen und flexible Aktionen erforderlich. Da sich diese beiden widersprechen, kann es leicht geschehen, dass die Ausrichtung von Prioritäten nicht mehr stimmt. Dieser Artikel beschreibt Methoden, mit denen die Ausrichtung von Übergangen während der Migration beibehalten werden kann.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-business-and-technical-priorities-stay-aligned-during-a-migration"></a>Wie können geschäftliche und technische Prioritäten während einer Migration aufeinander abgestimmt bleiben?

Das Cloudeinführungsteam und das Cloudgovernanceteam konzentrieren sich auf die Ausführung der aktuellen Iteration und des aktuellen Release. Iterationen ermöglichen technische Arbeiten in beständigen Schritten und vermeiden so kostspielige Unterbrechungen, die sonst den Fortschritt der Migrationsmaßnahmen verlangsamen würden. Releases stellen sicher, dass sich der technische Aufwand und die Energie weiterhin auf die Geschäftsziele der Workloadmigration konzentrieren. Ein Migrationsprojekt kann viele Releases über einen längeren Zeitraum erfordern. Bis zur Fertigstellung haben sich die Marktbedingungen wahrscheinlich erheblich geändert.

Parallel dazu konzentriert sich das Cloudstrategieteam auf die Umsetzung des geschäftsbezogenen Änderungsplans und die Vorbereitung auf das nächste Release. Das Cloudstrategieteam blickt in der Regel mindestens ein Release voraus, überwacht die sich ändernden Marktbedingungen und passt das Migrationsbacklog entsprechend an. Dieser Schwerpunkt auf der Transformationsverwaltung und Plananpassung führt zu natürlichen Abänderungen in Bezug auf die technische Arbeit. Wenn sich geschäftliche Prioritäten ändern, liegt deren Umsetzung nur ein Release zurück, sodass für technische und geschäftliche Flexibilität gesorgt ist.

## <a name="business-alignment-questions"></a>Fragen zur geschäftlichen Ausrichtung

Die folgenden Fragen können dem Cloudstrategieteam helfen, das Migrationsbacklog zu gestalten und zu priorisieren, damit sichergestellt ist, dass die Transformationsmaßnahmen optimal auf die aktuellen Geschäftsanforderungen abgestimmt sind.

- Hat das Cloudeinführungsteam eine Liste mit Workloads erstellt, die für die Migration bereit sind?
- Hat das Cloudeinführungsteam aus dieser Liste mit Workloads einen einzelnen Kandidaten für eine erste Migration ausgewählt?
- Verfügen das Cloudeinführungsteam und das Cloudgovernanceteam über alle notwendigen Daten in Bezug auf die Workload und die Cloudumgebung, um erfolgreich zu sein?
- Bietet die ausgewählte Workload im nächsten Release die Auswirkungen auf das Geschäft mit der größten Relevanz?
- Gibt es andere Workloads, die sich besser für die Migration eignen?

## <a name="tangible-actions"></a>Konkrete Aktionen

Während der Umsetzung des geschäftsbezogenen Änderungsplans überwacht das Cloudstrategieteam die positiven und negativen Ergebnisse. Wenn diese Beobachtungen technische Änderungen erforderlich machen, werden die Anpassungen als Arbeitselemente in das Releasebacklog aufgenommen, damit sie in der nächsten Iteration priorisiert werden.

Bei Marktänderungen arbeitet das Cloudstrategieteam mit dem Unternehmen zusammen, um zu ermitteln, wie am besten auf die Änderungen reagiert wird. Wenn diese Reaktion eine Änderung der Migrationsprioritäten erfordert, wird das Migrationsbacklog entsprechend angepasst. Dadurch werden Workloads, die bisher eine niedrigere Priorität hatten, höhergestuft.

## <a name="next-steps"></a>Nächste Schritte

Auf der Grundlage entsprechend ausgerichteter geschäftlicher Prioritäten kann das Cloudeinführungsteam mit dem [Bewerten von Workloads](./evaluate.md) zum Aufstellen von Architektur- und Migrationsplänen beginnen.

> [!div class="nextstepaction"]
> [Bewerten von Workloads](./evaluate.md)
