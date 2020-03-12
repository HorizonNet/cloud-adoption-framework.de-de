---
title: Optimieren von migrierten Workloads
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um Ihre migrierten Workloads und Ressourcen für die Höherstufung in die Produktion vorzubereiten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b59245a8665355b34c3f599d8515ceeb93eb7315
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094097"
---
# <a name="optimize-migrated-workloads"></a>Optimieren von migrierten Workloads

Nachdem eine Workload und ihre unterstützenden Ressourcen in die Cloud migriert wurden, muss sie vorbereitet werden, bevor sie in die Produktion höhergestuft werden kann. In diesem Prozess bereiten die Aktivitäten die Workload vor, skalieren die abhängigen Ressourcen und bereiten das Geschäft darauf vor, wann die migrierte cloudbasierte Workload in die Produktionsumgebung wechselt.

Ziel der Optimierung ist es, eine migrierte Workload für die Höherstufung in die Produktionsumgebung vorzubereiten.

## <a name="definition-of-done"></a>Definition von *Fertig*.

Der Optimierungsprozess ist abgeschlossen, wenn eine Workload richtig konfiguriert, skaliert und in der Produktionsumgebung bereitgestellt wurde.

## <a name="accountability-during-optimization"></a>Verantwortlichkeit während der Optimierungsphase

Das Cloudeinführungsteam ist für den gesamten Optimierungsprozess verantwortlich. Mitglieder des Cloudstrategieteams, des Cloudbetriebsteams und des Cloudgovernanceteams sollten im Rahmen dieses Prozesses jedoch ebenfalls mit Aktivitäten betraut werden.

## <a name="responsibilities-during-optimization"></a>Zuständigkeiten während der Optimierungsphase

Zusätzlich zur Verantwortlichkeit auf hoher Ebene gibt es Maßnahmen, für die eine Person oder Gruppe direkt verantwortlich sein muss. Im Folgenden sind einige Aktivitäten aufgeführt, die eine Zuordnung zu verantwortlichen Personen erfordern:

- **Geschäftsbezogene Tests** Beheben aller Kompatibilitätsprobleme, die verhindern, dass die Workload ihre Migration in die Cloud abschließt.
  - Hauptbenutzer aus dem Unternehmen sollten sich intensiv an den Tests der migrierten Workload beteiligen. Je nach angestrebtem Optimierungsgrad können mehrere Testzyklen erforderlich sein.
- **Geschäftsbezogener Änderungsplan** Die Entwicklung eines Plans für die Benutzereinführung, Änderungen an Geschäftsprozessen, Unternehmens-KPIs oder Lernmetriken als Ergebnis des Migrationsaufwands.
- **Vergleichstest und Optimierung** Studie zu den geschäftsbezogenen und automatisierten Tests für Leistungsvergleiche. Basierend auf der Nutzung optimiert das Cloudeinführungsteam die Skalierung der bereitgestellten Ressourcen, um Kosten und Leistung mit den erwarteten Anforderungen der Produktionsumgebung in Einklang zu bringen.
- **Bereit für die Produktion** Bereiten Sie die Workload und die Umgebung für die Unterstützung der laufenden Nutzung der Workload in der Produktionsumgebung vor.
- **Höherstufen** Umleiten des Produktionsdatenverkehrs zur migrierten und optimierten Workload. Diese Aktivität stellt den Abschluss eines Freigabezyklus dar.

Zusätzlich zu den Hauptaktivitäten gibt es einige parallele Aktivitäten, die bestimmte Zuweisungen und Ausführungspläne erfordern:

- **Außer Betrieb setzen** Generell können durch eine Migration Kosteneinsparungen realisiert werden, wenn die bisherigen Produktionsressourcen außer Betrieb gesetzt und ordnungsgemäß beseitig werden.
- **Retrospektive** Jedes Release bietet die Möglichkeit zu intensiveren Lernvorgängen und zur Einführung einer Wachstumsorientierung. Nach Abschluss der einzelnen Freigabezyklen sollte das Cloudeinführungsteam die während der Migration verwendeten Prozesse bewerten, um Verbesserungen zu ermitteln.

## <a name="next-steps"></a>Nächste Schritte

Mit einem allgemeinen Überblick über die Optimierungsprozesse sind Sie bereit, den Prozess zu starten, indem Sie einen [geschäftsbezogenen Änderungsplan für die Kandidatenworkload erstellen](./business-change-plan.md).

> [!div class="nextstepaction"]
> [Geschäftsbezogener Änderungsplan](./business-change-plan.md)
