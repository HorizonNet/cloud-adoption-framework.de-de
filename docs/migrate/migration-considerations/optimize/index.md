---
title: Optimieren von migrierten Workloads
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um Ihre migrierten Workloads und Ressourcen für die Höherstufung in die Produktion vorzubereiten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0d83ccc83397153619bc7ca99881c6a2775ab1a3
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81120690"
---
# <a name="release-workloads"></a>Freigeben von Workloads

Nach der Bereitstellung einer Sammlung von Workloads und der zugehörigen unterstützenden Ressourcen in der Cloud müssen die Workloads vorbereitet werden, bevor sie freigegeben werden können. In dieser Phase der Migration werden Auslastungstests und Tests im Unternehmen für die Sammlung von Workloads durchgeführt. Anschließend werden sie optimiert und dokumentiert. Nachdem die Geschäfts- und IT-Teams Workloadbereitstellungen geprüft und genehmigt haben, können die Workloads freigegeben oder für den laufenden Betrieb an Governance-, Sicherheits- und operative Teams übergeben werden.

Ziel der „Freigabe von Workloads“ ist es, migrierte Workloads für die Höherstufung in die Produktion vorzubereiten.

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
