---
title: Korrigieren von Ressourcen vor der Migration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Korrigieren inkompatibler Ressourcen vor der Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 54621d366f0ae0a3e2e3504532ace183bc7f49c4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839076"
---
# <a name="remediate-assets-prior-to-migration"></a>Korrigieren von Ressourcen vor der Migration

Während der Bewertung der Migration versucht das Team, alle Konfigurationen zu ermitteln, die eine Ressource inkompatibel mit dem ausgewählten Cloudanbieter machen könnten. Das *Korrigieren* ist ein Prüfpunkt während der Migration, mit dem sichergestellt werden soll, dass solche Inkompatibilitäten gelöst wurden. In diesem Artikel werden einige allgemeine Korrekturaufgaben als Referenz beschrieben. Außerdem wird ein grundlegender Prozess definiert, mit dem entschieden wird, ob eine Korrektur eine nachhaltige Investition wäre.

## <a name="common-remediation-tasks"></a>Häufige Korrekturaufgaben

In jeder Unternehmensumgebung gibt es technische Schulden. Einige davon sind fehlerfrei und erwartbar. Architekturentscheidungen, die sich gut für eine lokale Umgebung eigneten, sind auf einer Cloudplattform möglicherweise ungeeignet. Auf beiden Fällen sind möglicherweise Korrekturaufgaben erforderlich, um die Ressourcen für die Migration vorzubereiten. Im Folgenden finden Sie einige Beispiele:

- **Kleinere Hostupgrades:** Manchmal muss ein veralteter Host vor der Replikation aktualisiert werden.
- **Kleinere Upgrades beim Gastbetriebssystem:** Wahrscheinlicher ist es, dass ein Betriebssystem vor der Replikation Patches oder Upgrades benötigt.
- **Änderungen an der SLA:** Sicherung und Wiederherstellung ändern sich auf einer Cloudplattform ganz erheblich. Daher ist es wahrscheinlich, dass kleinere Änderungen an den Sicherungsprozessen von Ressourcen erforderlich sind, damit sie auch in der Cloud weiterhin funktionieren.
- **PaaS-Migration:** In einigen Fällen ist möglicherweise auch eine PaaS-Bereitstellung einer Datenstruktur oder Anwendung erforderlich, um die Bereitstellung zu beschleunigen. Zur Vorbereitung der Lösung auf die PaaS-Bereitstellung sind möglicherweise kleinere Änderungen erforderlich.
- **PaaS-Codeänderungen:** Es ist nicht ungewöhnlich, dass für benutzerdefinierte Anwendungen geringfügige Codeänderungen erforderlich sind, um sie für PaaS vorzubereiten. Beispiele sind u. a. Methoden, die auf lokale Datenträger schreiben oder den arbeitsspeicherinternen Sitzungsstatus nutzen.
- **Änderungen an der Anwendungskonfiguration:** Bei migrierten Anwendungen sind möglicherweise Änderungen an Variablen erforderlich, dies umfasst z. B. Netzwerkpfade zu abhängigen Ressourcen, Änderungen der Dienstkonten oder Updates von abhängigen IP-Adressen.
- **Geringfügige Änderungen an Netzwerkpfaden:** Möglicherweise müssen Routingmuster geändert werden, damit der Datenverkehr der Benutzer ordnungsgemäß zu den neuen Ressourcen umgeleitet wird.
    > [!NOTE]
    > Hierbei handelt es sich noch nicht um das Routing zu den neuen Ressourcen für die Produktion, sondern lediglich um die Konfiguration für das ganz allgemeine ordnungsgemäße Routing zu den Ressourcen.

## <a name="large-scale-remediation-tasks"></a>Umfangreichere Korrekturaufgaben

Wenn ein Rechenzentrum ordentlich verwaltet, gepatcht und aktualisiert wird, sind vermutlich nur wenige Korrekturmaßnahmen erforderlich. In großen Unternehmen sind Umgebungen, die umfangreiche Korrekturen erfordern, eher die Regel. Dies gilt besonders in Organisationen, die Ihre IT in großem Umfang verkleinert haben, über ältere verwaltete Dienstumgebungen verfügen oder zahlreiche Übernahmen und Fusionen vollzogen haben. In all diesen Umgebungen kann die Korrektur einen großen Teil des Migrationsaufwands einnehmen. Wenn die folgenden Korrekturaufgaben häufig auftreten und negative Auswirkungen auf die Geschwindigkeit oder Konsistenz der Migration haben, kann es ratsam sein, die Korrektur zu einer eigenständigen Aufgabe mit einem eigenen Team zu machen (ähnlich der parallelen Durchführung von Cloudeinführung und Cloudgovernance).

- **Häufige Hostupgrades:** Wenn sehr viele Hosts aktualisiert werden müssen, um die Migration einer Workload abschließen zu können, kommt es beim Migrationsteam wahrscheinlich zu Verzögerungen. Es kann ratsam sein, die betroffenen Anwendungen einzeln zu korrigieren, bevor sie in geplante Releases eingebunden werden.
- **Häufige Upgrades des Gastbetriebssystems:** In großen Unternehmen gibt es häufig Server, auf denen veraltete Versionen von Linux oder Windows ausgeführt werden. Abgesehen von den offensichtlichen Sicherheitsrisiken durch ein veraltetes Betriebssystem kommt es auch zu Problemen durch Inkompatibilität, die eine Migration der betreffenden Workloads verhindern können. Wenn für eine große Anzahl von VMs Korrekturen am Betriebssystem erforderlich sind, kann es ratsam sein, diese Aufgabe als separate Iteration auszuführen.
- **Umfassende Codeänderungen:** Ältere benutzerdefinierte Anwendungen erfordern unter Umständen deutlich mehr Änderungen, um sie für die PaaS-Bereitstellung vorzubereiten. Wenn dies der Fall ist, kann es sinnvoll sein, sie vollständig aus dem Migrationsbacklog zu entfernen und in einem separaten Programm zu bearbeiten.

## <a name="decision-framework"></a>Entscheidungsrahmen

Die Korrektur kleinerer Workloads kann unter Umständen sehr einfach sein. Aus diesem Grund empfiehlt es sich, für die erste Migration eine kleinere Workload auszuwählen. Wenn Ihr Migrationsaufwand zunimmt und Sie mit größeren Workloads beginnen, kann sich die Korrektur zu einem zeitaufwendigen und teuren Prozess entwickeln. So kann z. B. der Aufwand für eine Migration von Windows Server 2003 mit einem Pool von mehr als 5.000 virtuellen Computern und deren Ressourcen eine Migration um Monate verzögern. Wenn solche umfangreichen Korrekturen notwendig sind, sollten Sie für Ihre Entscheidungen die folgenden Fragen beantworten:

- Wurden alle von der Korrektur betroffenen Workloads ermittelt und im Migrationsbacklog erfasst?
- Führt bei den nicht betroffenen Workloads eine Migration zu einer ähnlichen Rendite (ROI)?
- Können die betroffenen Ressourcen im ursprünglichen Zeitrahmen für die Migration korrigiert werden? Welche Auswirkungen hätten Änderungen am Zeitrahmen auf die Rendite?
- Ist es wirtschaftlich sinnvoll, die Ressourcen parallel zur Migration zu korrigieren?
- Gibt es genügend Bandbreite für die Mitarbeiter, um Korrektur und Migration durchzuführen? Sollte ein Partner für eine oder beide Aufgaben engagiert werden?

Falls diese Fragen keine positiven Antworten liefern, sollten eventuell einige alternative Ansätze, die über eine grundlegende Strategie für das IaaS-Rehosting hinausgehen, in Betracht gezogen werden:

- **Containerisierung:** Einige Objekte können in einer Containerumgebung ausgeführt werden, ohne dass eine Korrektur erforderlich ist. Dies könnte zu einer verminderten Leistung führen und löst natürlich keine Sicherheits- oder Complianceprobleme.
- **Automatisierung:** Je nach Workload und den Korrekturanforderungen können Skripts für die Bereitstellung auf neuen Ressourcen über einen DevOps-Ansatz möglicherweise rentabler sein.
- **Neuerstellung:** Wenn die Kosten für die Korrektur sehr hoch sind und der Geschäftswert ebenfalls hoch ist, könnte eine Neuerstellung oder eine ganz neue Architektur für diese Workload besser geeignet sein.

## <a name="next-steps"></a>Nächste Schritte

Nach Abschluss der Korrektur können die [Replikationsaktivitäten](./replicate.md) ausgeführt werden.

> [!div class="nextstepaction"]
> [Replizieren von Ressourcen](./replicate.md)
