---
title: Risikotoleranzmetriken und -indikatoren in der Disziplin „Sicherheitsbaseline“.
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über die Quantifizierung der Geschäftsrisikotoleranz im Zusammenhang mit der Disziplin „Sicherheitsbaseline“ zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e8c79abc6b3e6af2eb3653fda4fd7891457e9a41
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88878876"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-security-baseline-discipline"></a>Risikotoleranzmetriken und -indikatoren in der Disziplin „Sicherheitsbaseline“

Lernen Sie, die Risikotoleranz von Unternehmen im Zusammenhang mit der Disziplin „Sicherheitsbaseline“ zu quantifizieren. Indem Sie Metriken und Indikatoren definieren, können Sie ein Geschäftsszenario erstellen, um in die Ausgereiftheit dieser Disziplin zu investieren.

## <a name="metrics"></a>Metriken

Bei der Disziplin „Sicherheitsbaseline“ steht im Allgemeinen die Erkennung potenzieller Sicherheitsrisiken in Ihren Cloudbereitstellungen im Mittelpunkt. Im Rahmen der Risikoanalyse sollten Sie Daten zu Ihrer Sicherheitsumgebung sammeln, um zu bestimmen, wie hoch das Risiko ist und wie wichtig Investitionen in Ihre Disziplin „Sicherheitsbaseline“ für Ihre geplanten Cloudbereitstellungen ist.

Jede Organisation weist unterschiedliche Sicherheitsumgebungen und -anforderungen sowie verschiedene potenzielle Quellen von Sicherheitsdaten auf. Es folgen Beispiele für nützliche Metriken, die Sie sammeln sollten, um die Risikotoleranz innerhalb der Disziplin der Sicherheitsbaseline zu bewerten:

- **Datenklassifizierung:** Anzahl der in der Cloud gespeicherten Daten und Dienste, die gemäß den Standards Ihrer Organisation für Datenschutz, Compliance oder Geschäftsauswirkungen nicht klassifiziert sind.
- **Anzahl Speicher für vertrauliche Daten:** Die Anzahl der Speicherendpunkte oder Datenbanken, die sensible Daten enthalten und geschützt werden sollten.
- **Anzahl der Speicher für unverschlüsselte Daten:** Die Anzahl der Speicher für sensible Daten, die nicht verschlüsselt sind.
- **Angriffsfläche:** Wie viele Datenquellen, Dienste und Anwendungen werden insgesamt in der Cloud gehostet? Welcher Prozentsatz dieser Datenquellen wird als sensibel eingestuft? Welcher Prozentsatz dieser Anwendungen und Dienste ist geschäftskritisch?
- **Abgedeckte Standards:** Anzahl der vom Sicherheitsteam definierten Sicherheitsstandards.
- **Abgedeckte Ressourcen:** Bereitgestellte Ressourcen, die durch Sicherheitsstandards abgedeckt sind.
- **Allgemeine Einhaltung von Standards:** Quote der Einhaltung von Sicherheitsstandards.
- **Angriffe nach Schweregrad:** Wie viele koordinierte Versuche, Ihre in der Cloud gehosteten Dienste zu stören, z. B. durch DDoS-Angriffe (Distributed Denial of Service), treten in Ihrer Infrastruktur auf? Wie sieht es mit Umfang und Schweregrad dieser Angriffe aus?
- **Schutz vor Schadsoftware:** Prozentsatz der bereitgestellten virtuellen Computer (VMs), auf denen alle erforderliche Antischad-, Firewall- oder andere Sicherheitssoftware installiert ist.
- **Patchlatenzzeit:** Wie lange ist es her, dass Betriebssystem- und Softwarepatches auf VMs angewendet wurden?
- **Empfehlungen für Sicherheitsintegrität:** Anzahl der Empfehlungen von Sicherheitssoftware als Lösung für Integritätsstandards bereitgestellter Ressourcen, nach Schweregrad geordnet.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

Cloudplattformen bieten eine Reihe von Basisfunktionen, die es kleinen Bereitstellungsteams ermöglichen, grundlegende Sicherheitseinstellungen ohne umfangreiche zusätzliche Planung zu konfigurieren. Infolgedessen stellen kleine Dev/Test- oder experimentelle erste Workloads, die keine sensiblen Daten enthalten, ein relativ geringes Risiko dar und werden wahrscheinlich keine hohen Anforderungen in Bezug auf eine formale Richtlinie für die Sicherheitsbaseline bedeuten. Sobald wichtige Daten oder geschäftskritische Funktionen in die Cloud verschoben werden, steigen die Sicherheitsrisiken, während die Toleranz für diese Risiken schnell abnimmt. Je mehr Ihrer Daten und Funktionen in der Cloud bereitgestellt werden, desto wahrscheinlicher ist es, dass höhere Investitionen in die Disziplin „Sicherheitsbaseline“ erforderlich sind.

In den frühen Phasen der Cloudeinführung arbeiten Sie mit Ihrem IT-Sicherheitsteam und den Projektbeteiligten des Unternehmens zusammen, um [Geschäftsrisiken](./business-risks.md) im Zusammenhang mit der Sicherheit zu identifizieren, und bestimmen anschließend eine akzeptable Baseline für die Sicherheitsrisikotoleranz. Dieser Abschnitt des Cloud Adoption Framework enthält einige Beispiele. Die Risiken und Baselines in Ihrem Unternehmen bzw. bei Ihren Bereitstellungen weichen im Detail möglicherweise davon ab.

Legen Sie nach der Einigung auf eine Baseline minimale Benchmarks fest, die eine unzulässige Zunahme der identifizierten Risiken darstellen. Diese Benchmarks fungieren als Auslöser und geben an, wann Sie Maßnahmen zum Beheben dieser Risiken ergreifen müssen. Im Folgenden wird anhand einiger Beispiele dargestellt, wie Sicherheitsmetriken (z.B. die oben erwähnten) eine höhere Investition in die Disziplin „Sicherheitsbaseline“ rechtfertigen können.

- **Trigger für geschäftskritische Workloads.** Ein Unternehmen, das geschäftskritische Workloads in der Cloud bereitstellt, sollte in die Disziplin „Sicherheitsbaseline“ investieren, um mögliche Unterbrechungen des Diensts oder die Offenlegung sensibler Daten zu verhindern.
- **Trigger für geschützte Daten.** Ein Unternehmen, das Daten in der Cloud hostet, die als vertraulich, privat oder anderweitig rechtlich bedenklich eingestuft werden können. Es ist eine Disziplin „Sicherheitsbaseline“ erforderlich, um sicherzustellen, dass diese Daten nicht verloren gehen, offengelegt oder gestohlen werden.
- **Trigger für externe Angriffe.** Ein Unternehmen, bei dem *x*-mal im Monat schwere Angriffe auf die Netzwerkinfrastruktur stattfinden, kann von der Disziplin „Sicherheitsbaseline“ profitieren.
- **Trigger für Einhaltung von Standards.** Ein Unternehmen, bei dem mehr als *x %* seiner Ressourcen nicht den Sicherheitsstandards entsprechen, sollte in die Disziplin „Sicherheitsbaseline“ investieren, um sicherzustellen, dass Standards in der gesamten IT-Infrastruktur konsistent angewendet werden.
- **Trigger für Größe der Cloudumgebung.** Ein Unternehmen, das mehr als *x* Anwendungen, Dienste oder Datenquellen hostet. Große Cloudbereitstellungen können von Investitionen in die Disziplin „Sicherheitsbaseline“ profitieren, um sicherzustellen, dass ihre gesamte Angriffsfläche angemessen vor unbefugtem Zugriff oder anderen externen Bedrohungen geschützt ist.
- **Trigger für Konformität der Sicherheitssoftware.** Ein Unternehmen, in dem auf weniger als *x %* der bereitgestellten virtuellen Computer die gesamte erforderliche Sicherheitssoftware installiert ist. Mithilfe der Disziplin „Sicherheitsbaseline“ kann sichergestellt werden, dass Software konsistent auf allen Computern installiert ist.
- **Trigger für Patching.** Ein Unternehmen, in dem auf bereitgestellten virtuellen Computern oder Diensten in den letzten *x* Tagen keine Betriebssystem- oder Softwarepatches angewendet wurden. Mithilfe der Disziplin „Sicherheitsbaseline“ kann sichergestellt werden, dass Patches innerhalb eines erforderlichen Zeitplans auf dem neuesten Stand gehalten werden.
- **Sicherheitsorientiert.** Einige Unternehmen haben strenge Anforderungen in Bezug auf Sicherheit und Vertraulichkeit von Daten, selbst für Test- und experimentelle Workloads. Diese Unternehmen müssen in die Disziplin „Sicherheitsbaseline“ investieren, bevor mit Bereitstellungen begonnen werden kann.

Die genauen Metriken und Auslöser, die Sie zum Bemessen der Risikotoleranz verwenden, und die Höhe der Investitionen in die Disziplin „Sicherheitsbaseline“ sind für Ihre Organisation spezifisch, doch sollten die oben genannten Beispiele eine hilfreiche Diskussionsgrundlage für Ihr Cloudgovernanceteam darstellen.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die [Disziplin „Sicherheitsbaseline“](./template.md) zum Dokumentieren der Metriken und Toleranzindikatoren, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Sicherheitsbaseline-Beispielrichtlinien als Ausgangspunkt für die Entwicklung eigener Richtlinien, die bestimmte Geschäftsrisiken behandeln, entsprechend Ihren Plänen für die Einführung der Cloud.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
