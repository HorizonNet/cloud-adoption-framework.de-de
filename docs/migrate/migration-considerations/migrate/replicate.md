---
title: Welche Rolle spielen Replikation und Synchronisierung im Migrationsprozess?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ein Prozess innerhalb der Cloudmigration, der sich auf die Aufgaben der Migration von Workloads in die Cloud konzentriert.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 62c12796abf8921c13cebe471fe555d012bab15c
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549132"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-role-does-replication-play-in-the-migration-process"></a>Welche Rolle spielt die Replikation im Migrationsprozess?

Lokale Rechenzentren sind mit physischen Ressourcen wie Servern, Appliances und Netzwerkgeräten gefüllt. Ein Server ist jedoch nur eine physische Hülle. Der eigentliche Wert ergibt sich durch den Binärcode, der auf dem Server ausgeführt wird. Die Anwendungen und Daten sind der Zweck für das Rechenzentrum. Dies sind die primären Binärdateien, die migriert werden müssen. Unterstützt werden diese Anwendungen und Datenspeicher durch andere digitale Ressourcen und Binärquellen, wie Betriebssysteme, Netzwerkrouten, Dateien und Sicherheitsprotokolle.

Die Replikation stellt die eigentliche Basis der Migration dar. Es ist der Prozess des Kopierens einer zum jeweiligen Zeitpunkt gültigen Version verschiedener Binärdateien. Die binären Momentaufnahmen werden dann auf eine neue Plattform kopiert und auf neuer Hardware bereitgestellt. Dazu wird ein Prozess verwendet, der als *Seeding* bezeichnet wird. Bei ordnungsgemäßer Ausführung sollte sich die per Seeding hinzugefügte Kopie der Binärdatei genauso verhalten wie die ursprüngliche Binärdatei auf der alten Hardware. Die Momentaufnahme der Binärdatei ist jedoch sofort veraltet und entspricht nicht mehr der Originalquelle. Um die neue Binärdatei und die alte Binärdatei auf einem Stand zu halten, wird mit einem Prozess, der als *Synchronisierung* bezeichnet wird, die auf der neuen Plattform gespeicherte Kopie kontinuierlich aktualisiert. Die Synchronisierung wird fortgesetzt, bis die Ressource entsprechend dem ausgewählten Höherstufungsmodell hochgestuft wurde. An diesem Punkt wird die Synchronisierung abgebrochen.

## <a name="required-prerequisites-to-replication"></a>Erforderliche Voraussetzungen für die Replikation

Vor der Replikation müssen die *neue Plattform* und die Hardware für den Empfang der Binärdateikopien vorbereitet werden. Im Artikel zu [Voraussetzungen](../prerequisites/index.md) sind die Mindestanforderungen an die Umgebung beschrieben, um eine sichere, zuverlässige und leistungsfähige Plattform für den Empfang der Binärdateireplikate zu erstellen.

Die *Quellbinärdateien* müssen ebenfalls für die Replikation und Synchronisierung vorbereitet werden. Die Artikel zur Bewertung, Architektur und Problembehandlung befassen sich jeweils mit den Aktionen, mit denen sichergestellt wird, dass die Quellbinärdatei für die Replikation und Synchronisierung bereit ist.

Eine *Toolkette*, die der neuen Plattform und den Quellbinärdateien entspricht, muss implementiert werden, um die Replikations- und Synchronisierungsprozesse auszuführen und zu verwalten. Im Artikel über [Replikationsoptionen](./replicate-options.md) werden verschiedene Tools beschrieben, die zu einer Migration zu Azure beitragen können.

## <a name="replication-risks---physics-of-replication"></a>Replikationsrisiken – Physikalische Grundlagen der Replikation

Beim Planen der Replikation einer Binärquelle an einem neuen Ziel sind einige wesentliche Grundsätze während der Planung und Ausführung zu berücksichtigen.

- **Lichtgeschwindigkeit.** Bei der Übertragung großer Datenmengen sind Glasfaserkabel immer noch die schnellste Option. Leider können diese Kabel Daten nur mit zwei Dritteln der Lichtgeschwindigkeit übertragen. Das bedeutet, dass es keine Methode zur sofortigen oder unbegrenzten Replikation von Daten gibt.
- **Geschwindigkeit der WAN-Pipeline.** Folgenreicher als die Geschwindigkeit der Datenverschiebung ist die Uplinkbandbreite, die das Datenvolumen pro Sekunde definiert, das über das bestehende WAN eines Unternehmens in das Zielrechenzentrum übertragen werden kann.
- **Geschwindigkeit der WAN-Erweiterung.** Wenn es das Budget erlaubt, kann der WAN-Lösung eines Unternehmens zusätzliche Bandbreite hinzugefügt werden. Es kann jedoch Wochen oder Monate dauern, bis zusätzliche Glasfaserverbindungen beschafft, bereitgestellt und integriert sind.
- **Geschwindigkeit von Datenträgern.** Wenn Daten schneller übertragen werden könnten und es keine Begrenzung der Bandbreite zwischen der Binärquelle und dem Zielort gäbe, würden immer noch die Gesetze der Physik eine Beschränkung darstellen. Daten können nur so schnell repliziert werden, wie sie von Quelldatenträgern gelesen werden können. Das Lesen jeder Eins oder Null von jedem rotierenden Datenträger in einem Rechenzentrum braucht Zeit.
- **Geschwindigkeit der menschlichen Berechnungen.** Datenträger und Licht sind schneller als menschliche Entscheidungsprozesse. Wenn eine Gruppe von Menschen zusammenarbeiten und gemeinsam Entscheidungen treffen muss, lassen die Ergebnisse noch länger auf sich warten. Die Replikation kann niemals Verzögerungen ausgleichen, die sich durch das menschliche Denken ergeben.

Jedes dieser physikalischen Gesetze birgt die folgenden Risiken, die sich häufig auf Migrationspläne auswirken:

- **Replikationszeit.** Fortschrittliche Replikationstools können die grundlegenden physikalischen Gesetze nicht außer Kraft setzen &mdash; die Replikation erfordert Zeit und Bandbreite. Pläne sollten realistische Zeitvorgaben enthalten, die dem Zeitraum entsprechen, der für die Replikation von Binärdateien benötigt wird. Die *insgesamt verfügbare Migrationsbandbreite* ist die Menge an Aufwärtsbandbreite, gemessen in Megabit pro Sekunde (Mbit/s) oder Gigabit pro Sekunde (GBit/s), die nicht durch andere Geschäftsanforderungen mit höherer Priorität belegt ist. Der *Gesamtspeicher für die Migration* ist der gesamte Speicherplatz, gemessen in Gigabyte oder Terabyte, der benötigt wird, um eine Momentaufnahme aller zu migrierenden Ressourcen zu speichern. Eine erste Schätzung der Zeit kann berechnet werden, indem der *Gesamtspeicher für die Migration* durch die *insgesamt verfügbare Migrationsbandbreite* dividiert wird. Beachten Sie die Konvertierung von Bits in Bytes. Eine genauere Berechnung der Zeit finden Sie im folgenden Absatz „Kumulativer Effekt von Datenträgerabweichungen“.
- **Kumulativer Effekt von Datenträgerabweichungen.** Vom Zeitpunkt der Replikation bis zur Höherstufung einer Ressource in die Produktion müssen die Quell- und Zielbinärdateien synchronisiert bleiben. Eine *Abweichung* der Binärdateien verbraucht zusätzliche Bandbreite, da alle Änderungen an der Binärdatei wiederkehrend repliziert werden müssen. Während der Synchronisierung müssen alle Abweichungen der Binärdateien in die Berechnung des Gesamtspeichers für die Migration einbezogen werden. Je länger es dauert, eine Ressource in die Produktion hochzustufen, desto mehr kumulative Abweichungen treten auf. Je mehr Ressourcen synchronisiert werden, desto mehr Bandbreite wird gebraucht. Da jede Ressource in synchronisiertem Zustand gehalten wird, geht ein weiterer Teil der insgesamt verfügbaren Migrationsbandbreite verloren.
- **Zeit bis zur Geschäftsänderung.** Wie im vorherigen Absatz, „Kumulativer Effekt von Datenträgerabweichungen“, erwähnt, hat die Synchronisationszeit eine kumulative negative Auswirkung auf die Migrationsgeschwindigkeit. Die Priorisierung des Migrationsbacklogs und die erweiterte Vorbereitung für den [geschäftsbezogenen Änderungsplan](../optimize/business-change-plan.md) sind für die Migrationsgeschwindigkeit von entscheidender Bedeutung. Der wichtigste Test für die geschäftliche und technische Anpassung während einer Migration ist das Tempo der Höherstufung. Je schneller eine Ressource in die Produktion hochgestuft werden kann, desto weniger Auswirkungen haben Datenträgerabweichungen auf die Bandbreite und desto mehr Bandbreite/Zeit kann der Replikation der nächsten Workload zugewiesen werden.

## <a name="next-steps"></a>Nächste Schritte

Nach Abschluss der Replikation können die [Stagingaktivitäten](./stage.md) beginnen.

> [!div class="nextstepaction"]
> [Stagingaktivitäten während einer Migration](./stage.md)
