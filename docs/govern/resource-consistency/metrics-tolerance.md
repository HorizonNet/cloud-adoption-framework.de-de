---
title: Metriken und Indikatoren der Risikotoleranz in der Disziplin „Ressourcenkonsistenz“
description: Verwenden Sie das Cloud Adoption Framework für Azure, um die Geschäftsrisikotoleranz im Zusammenhang mit der Disziplin „Ressourcenkonsistenz“ zu quantifizieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3667bff715ed7f91f4bdabda90e87aad15751a33
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88879352"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-resource-consistency-discipline"></a>Metriken und Indikatoren der Risikotoleranz in der Disziplin „Ressourcenkonsistenz“

Lernen Sie, die Risikotoleranz von Unternehmen im Zusammenhang mit der Disziplin „Ressourcenkonsistenz“ zu quantifizieren. Indem Sie Metriken und Indikatoren definieren, können Sie ein Geschäftsszenario erstellen, um in die Ausgereiftheit dieser Disziplin zu investieren.

## <a name="metrics"></a>Metriken

Ressourcenkonsistenz konzentriert sich auf den Umgang mit Risiken im Zusammenhang mit der Betriebsverwaltung Ihrer Cloudbereitstellungen. Im Rahmen der Risikoanalyse sollten Sie Daten zu Ihren IT-Abläufen sammeln, um zu ermitteln, welches Risiko vorliegt und wie wichtig Investitionen in die Disziplin „Ressourcenkonsistenz“ für Ihre geplanten Cloudbereitstellungen ist.

Jede Organisation verfügt über die verschiedenen Betriebsszenarien, aber die folgenden Elemente stellen nützliche Beispiele für die Metriken dar, die Sie sammeln sollten, wenn Sie die Risikotoleranz innerhalb der Disziplin „Ressourcenkonsistenz“ beurteilen:

- **Cloudressourcen.** Die Gesamtanzahl der in der Cloud bereitgestellten Ressourcen.
- **Unmarkierte Ressourcen.** Die Anzahl der Ressourcen ohne erforderliche Buchhaltung, Auswirkungen auf das Unternehmen oder Organisationstags.
- **Nicht ausgelastete Ressourcen.** Die Anzahl der Ressourcen, bei denen die Arbeitsspeicher-, CPU- oder Netzwerkfunktionen kontinuierlich nicht ausgelastet sind.
- **Ressourcenschwund.** Die Anzahl der Ressourcen, bei denen die Arbeitsspeicher-, CPU- oder Netzwerkfunktionen durch Lasten erschöpft sind.
- **Ressourcenalter.** Die Zeit, seit die Ressource zuletzt bereitgestellt oder geändert wurde.
- **Virtuelle Computer in kritischem Zustand.** Die Anzahl der bereitgestellten virtuellen Computer, auf denen mindestens ein kritischer Fehler entdeckt wurde, der behandelt werden muss, um die normale Funktionsweise wiederherzustellen.
- **Warnungen nach Schweregrad.** Die Gesamtanzahl von Warnungen für eine bereitgestellte Ressource, aufgeschlüsselt nach Schweregrad.
- **Fehlerhafte Netzwerkverbindungen.** Die Anzahl der Ressourcen mit Netzwerkkonnektivitätsproblemen.
- **Fehlerhafte Dienstendpunkte.** Die Anzahl von Problemen mit externen Netzwerkendpunkten.
- **Cloudanbieter-Dienstintegritätsvorfälle.** Die Anzahl von Unterbrechungen oder Leistungsvorfällen, die vom Cloudanbieter verursacht wurden.
- **Vereinbarungen zum Servicelevel.** Hierzu können sowohl Verpflichtungen von Microsoft im Hinblick auf die Verfügbarkeit und Konnektivität von Azure-Diensten als auch Verpflichtungen des Unternehmens gegenüber externen und internen Kunden gehören.
- **Dienstverfügbarkeit.** Der Prozentsatz der tatsächlichen Verfügbarkeit der in der Cloud gehosteten Workloads im Vergleich zur erwarteten Verfügbarkeit.
- **Recovery Time Objective (RTO).** Gibt den maximal zulässigen Zeitraum an, den eine Anwendung nach einem Vorfall nicht verfügbar sein darf.
- **Recovery Point Objective (RPO).** Gibt den maximalen Zeitraum für den Datenverlust an, der bei einem Notfall akzeptabel ist. Wenn Sie Daten beispielsweise in einer einzelnen Datenbank ohne Replikation in anderen Datenbanken speichern und stündliche Sicherungen durchführen, können Daten für bis zu eine Stunde verloren gehen.
- **Mean Time To Recover (MTTR).** Gibt die durchschnittliche Zeit an, die zum Wiederherstellen einer Komponente nach einem Ausfall erforderlich ist.
- **Mean Time Between Failures (MTBF).** Gibt die mittlere Betriebsdauer für die Komponente an, die zwischen Ausfällen zu erwarten ist. Anhand dieser Metrik können Sie berechnen, wie häufig ein Dienst nicht verfügbar sein wird.
- **Sicherungsintegrität.** Die Anzahl von Sicherungen, die aktiv synchronisiert werden.
- **Wiederherstellungsintegrität.** Die Anzahl von Wiederherstellungsvorgängen, die erfolgreich ausgeführt wurden.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

Cloudplattformen bieten eine Reihe von Basisfunktionen, die es Bereitstellungsteams ermöglichen, kleine Bereitstellungen effektiv zu verwalten, ohne umfangreiche zusätzliche Planung oder Prozesse. Infolgedessen stellen kleine Entwicklungs-/Test- oder experimentelle erste Workloads, die eine relativ geringe Anzahl cloudbasierter Ressourcen umfassen, ein geringes Risiko dar und werden wahrscheinlich keine hohen Anforderungen in Bezug auf eine formale Richtlinie für die Ressourcenkonsistenz stellen.

Mit zunehmender Größe Ihrer Cloudumgebung wird auch die Komplexität der Verwaltung Ihrer Ressourcen deutlich schwieriger werden. Mit steigender Anzahl von Ressourcen in der Cloud erhält die Fähigkeit zur Identifizierung des Besitzes von Ressourcen und die nützliche Kontrolle von Ressourcen eine kritische Bedeutung für die Minimierung von Risiken. Wenn zunehmend unternehmenskritische Workloads in der Cloud bereitgestellt werden, wird die Verfügbarkeitsdauer des Diensts kritischer, und die Toleranz für potenzielle Kostenüberschreitungen durch Dienstunterbrechungen nimmt schnell ab.

In den frühen Phasen der Cloudeinführung arbeiten Sie mit Ihrem IT-Betriebsteam und den Projektbeteiligten des Unternehmens zusammen, um [Geschäftsrisiken](./business-risks.md) im Zusammenhang mit der Ressourcenkonsistenz zu identifizieren, und bestimmen anschließend eine akzeptable Baseline für die Risikotoleranz. Dieser Abschnitt des Cloud Adoption Framework enthält einige Beispiele. Die Risiken und Baselines in Ihrem Unternehmen bzw. bei Ihren Bereitstellungen weichen im Detail möglicherweise davon ab.

Legen Sie nach der Einigung auf eine Baseline minimale Benchmarks fest, die eine unzulässige Zunahme der identifizierten Risiken darstellen. Diese Benchmarks fungieren als Auslöser und geben an, wann Sie Maßnahmen zum Beheben dieser Risiken ergreifen müssen. Im Folgenden wird anhand einiger Beispiele dargestellt, wie Betriebsmetriken (z.B. die oben erwähnten) eine höhere Investition in die Disziplin „Ressourcenkonsistenz“ rechtfertigen können.

- **Trigger „Markieren (Tagging) und Benennen“.** Ein Unternehmen mit mehr als *x* Ressourcen, denen erforderliche Markierungsinformationen fehlen die Benennungsstandards nicht einhalten, sollten Investitionen in die Disziplin „Ressourcenkonsistenz“ in Erwägung ziehen, um die Optimierung dieser Standards zu unterstützen und ihre konsistente Anwendung auf in der Cloud bereitgestellte Ressourcen sicherzustellen.
- **Trigger „Überdimensionierte Ressourcen“.** Wenn in einem Unternehmen mehr als *x %* der Ressourcen regelmäßig nur geringe Mengen ihrer verfügbaren Arbeitsspeicher-, CPU- oder Netzwerkfunktionen nutzen, wird vorgeschlagen, in die Disziplin „Ressourcenkonsistenz“ zu investieren, um die Optimierung der Ressourcennutzung für diese Elemente zu optimieren.
- **Trigger „Unterdimensionierte Ressourcen“.** Wenn in einem Unternehmen mehr als *x %* der Ressourcen regelmäßig den größten Teil ihrer verfügbaren Arbeitsspeicher-, CPU- oder Netzwerkfunktionen erschöpfen, wird vorgeschlagen, in die Disziplin „Ressourcenkonsistenz“ zu investieren, um sicherzustellen, dass diese Objekte die notwendigen Ressourcen erhalten, die zur Verhinderung von Dienstunterbrechungen erforderlich sind.
- **Trigger „Ressourcenalter“.** Ein Unternehmen mit mehr als *x* Ressourcen, die in mehr als *y* Monaten nicht aktualisiert wurden, könnte von Investitionen in die Disziplin „Ressourcenkonsistenz“ profitieren, die darauf abzielt sicherzustellen, dass Ressourcen gepatcht und fehlerfrei sind, während gleichzeitig veraltete oder anderweitig nicht verwendete Ressourcen außer Betrieb genommen werden.
- **Trigger für die Vereinbarung zum Servicelevel (SLA).** Ein Unternehmen, das seine mit externen Kunden oder internen Partnern getroffenen Vereinbarungen zum Servicelevel (SLAs) nicht einhalten kann, sollte in die Disziplin „Beschleunigung der Bereitstellung“ investieren, um die Systemausfallzeiten zu reduzieren.
- **Trigger für die Wiederherstellungszeit.** Ein Unternehmen, das die erforderlichen Schwellenwerte für die Wiederherstellungszeit nach einem Systemausfall überschreitet, sollte in die Verbesserung der Disziplin „Beschleunigung der Bereitstellung“ und in das Systemdesign investieren, um Fehler zu reduzieren bzw. ganz zu beseitigen oder die Auswirkungen beim Ausfall einzelner Komponenten abzufedern.
- **Trigger „VM-Integrität“.** Ein Unternehmen, in dem bei mehr als *x %* der VMs kritische Integritätsprobleme auftreten, sollte in die Disziplin „Ressourcenkonsistenz“ investieren, um Probleme zu identifizieren und die VM-Stabilität zu verbessern.
- **Trigger „Netzwerkintegrität“.** Ein Unternehmen, in dem bei mehr als *x %* der Netzwerksubnetze oder -endpunkte Konnektivitätsprobleme auftreten, sollte in die Disziplin „Ressourcenkonsistenz“ investieren, um Netzwerkprobleme zu identifizieren und zu beheben.
- **Trigger „Sicherungsabdeckung“.** Ein Unternehmen mit *x %* unternehmenskritischer Ressourcen ohne vorhandene aktuelle Sicherungen würde von erhöhten Investitionen in die Disziplin „Ressourcenkonsistenz“ profitieren, um eine konsistente Sicherungsstrategie sicherzustellen.
- **Trigger „Sicherungsintegrität“.** Ein Unternehmen, in dem mehr als *x %* der Wiederherstellungsvorgänge fehlschlagen, sollte in die Disziplin „Ressourcenkonsistenz“ investieren, um Probleme mit der Sicherung zu identifizieren und sicherzustellen, dass wichtige Ressourcen geschützt sind.

Die genauen Metriken und Auslöser, die Sie zum Bemessen der Risikotoleranz verwenden, und die Höhe der Investitionen in die Disziplin „Ressourcenkonsistenz“ sind für Ihre Organisation spezifisch. Die oben genannten Beispiele sollten jedoch eine hilfreiche Diskussionsgrundlage für Ihr Cloudgovernanceteam darstellen.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die [Disziplin „Ressourcenkonsistenz“](./template.md) zum Dokumentieren der Metriken und Toleranzindikatoren, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Ressourcenkonsistenz-Beispielrichtlinien als Ausgangspunkt für die Entwicklung eigener Richtlinien, die bestimmte Geschäftsrisiken behandeln, entsprechend Ihren Plänen für die Einführung der Cloud.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
