---
title: Anforderungen beim Höherstufen einer migrierten Ressource in die Produktion
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit den häufigen Aufgaben und Standardvoraussetzungen für das Höherstufen einer migrierten Ressource in die Produktion vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7082380e7b64160071f4304bc5ca3a4d341df24b
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88884673"
---
# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>Was ist erforderlich, um eine migrierte Ressource in die Produktion höher zu stufen?

Eine Höherstufung in die Produktion kennzeichnet den Abschluss der Migration einer Workload in die Cloud. Nachdem die Ressource und alle zugehörigen Abhängigkeiten höher gestuft wurden, wird der Produktionsdatenverkehr umgeleitet. Durch die Umleitung des Datenverkehrs werden die lokalen Ressourcen ausgesondert, sodass sie außer Betrieb genommen werden können.

Der Prozess der Höherstufung variiert je nach der Workloadarchitektur. Es gibt jedoch mehrere konsistente Voraussetzungen und ein paar allgemeine Aufgaben. In diesem Artikel werden sie jeweils beschrieben; er kann als eine Art Checkliste vor der Höherstufung verwendet werden.

## <a name="prerequisite-processes"></a>Erforderliche Prozesse

Jeder der folgenden Prozesse sollte vor der Produktionsbereitstellung ausgeführt, dokumentiert und überprüft werden:

- **[Bewerten](../assess/index.md):** Die Workload wurde im Hinblick auf Cloudkompatibilität bewertet.
- **[Entwerfen](../assess/architect.md):** Die Struktur der Workload wurde entsprechend dem ausgewählten Cloudanbieter entworfen.
- **[Replizieren](../migrate/replicate.md):** Die Ressourcen wurden in die Cloudumgebung repliziert.
- **[Bereitstellen](../migrate/stage.md):** Die replizierten Ressourcen wurden in einer bereitgestellten Instanz der Cloudumgebung wiederhergestellt.
- **[Geschäftsbezogene Tests](./business-test.md):** Die Workload wurde von Geschäftskunden vollständig getestet und überprüft.
- **[Geschäftsbezogener Änderungsplan](./business-change-plan.md):** Das Unternehmen hat einen Plan für die Änderungen freigegeben, die in Übereinstimmung mit der Produktionshöherstufung ausgeführt werden müssen. Er sollte einen Einführungsplan für Benutzer, Änderungen an Geschäftsvorgängen, Benutzer, für die Schulungen erforderlich sind, und Zeitachsen für verschiedene Aktivitäten enthalten.
- **[Bereit](./ready.md):** Normalerweise müssen vor der Höherstufung mehrere technische Änderungen vorgenommen werden.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Bewährte Methoden zum Ausführen vor der Höherstufung

Die folgenden technischen Änderungen müssen wahrscheinlich abgeschlossen und als Teil des Höherstufungsprozesses dokumentiert werden:

- **Domänenausrichtung.** Einige Unternehmensrichtlinien erfordern getrennte Domänen für Staging und Produktion. Stellen Sie sicher, dass alle Ressourcen mit der richtigen Domäne verknüpft sind.
- **Benutzerrouting.** Überprüfen Sie, ob Benutzer über die richtigen Netzwerkrouten auf die Workload zugreifen; überprüfen Sie konsistente Leistungserwartungen.
- **Identitätsausrichtung.** Überprüfen Sie, ob die Benutzer, die an die Anwendung umgeleitet werden, über geeignete Berechtigungen innerhalb der Domäne zum Hosten der Anwendung verfügen.
- **Leistung.** Führen Sie eine letzte Überprüfung der Workloadleistung durch, um Überraschungen zu minimieren.
- **Überprüfung von Business Continuity & Disaster Recovery (BCDR).** Überprüfen Sie, ob geeignete Sicherungs- und Wiederherstellungsprozesse wie erwartet funktionieren.
- **Datenklassifizierung.** Überprüfen Sie die Datenklassifizierung, um sicherzustellen, dass geeignete Schutzmaßnahmen und Richtlinien implementiert wurden.
- **Überprüfung durch den Chief Information Security Officer (CISO).** Überprüfen Sie, ob der Information Security Officer die Workload, Geschäftsrisiken, Risikotoleranz und Risikominderungsstrategien geprüft hat.

## <a name="final-step-promote"></a>Letzter Schritt: Höherstufen

Workloads erfordern unterschiedliche Ebenen von detaillierten Überprüfungs- und Höherstufungsprozessen. Die Neuausrichtung des Netzwerks dient jedoch als allgemeiner letzter Schritt für alle Höherstufungsreleases. Wenn alles andere bereit ist, aktualisieren Sie DNS-Datensätze oder IP-Adressen zum Weiterleiten von Datenverkehr an die migrierte Workload.

## <a name="next-steps"></a>Nächste Schritte

Die Höherstufung einer Workload signalisiert den Abschluss einer Release. Allerdings müssen – parallel zur Migration – ausgesonderte Ressourcen [außer Betrieb genommen](./decommission.md) werden, sodass sie dem Dienst nicht mehr zur Verfügung stehen.

> [!div class="nextstepaction"]
> [Außerbetriebnahme ausgesonderter Ressourcen](./decommission.md)
