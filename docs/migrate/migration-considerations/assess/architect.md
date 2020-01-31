---
title: Entwerfen von Workloads vor der Migration
description: Entwerfen von Workloads vor der Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b902f4b53784d30cd5de0b0eb77ed943e5e41aab
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802700"
---
# <a name="architect-workloads-prior-to-migration"></a>Entwerfen von Workloads vor der Migration

Dieser Artikel ergänzt die Informationen zum Bewertungsprozess. Es werden Aktivitäten im Zusammenhang mit der Definition der Architektur einer Workload in einer bestimmten Iteration beschrieben. Wie im Artikel zur [inkrementellen Rationalisierung](../../../digital-estate/rationalize.md) beschrieben, werden während jeder Geschäftstransformation, die eine Migration erfordert, einige Überlegungen zur Architektur angestellt. In diesem Artikel werden diese Überlegungen genauer behandelt. Außerdem werden einige Hürden und deren Vermeidung beschrieben und Möglichkeiten zur Beschleunigung von Geschäftswerten anhand dieser Annahmen erläutert. Dieses inkrementelle Modell für die Architektur ermöglicht Teams einen schnelleren Umstieg, sodass Geschäftsergebnisse früher erreicht werden.

## <a name="architecture-assumptions-prior-to-migration"></a>Überlegungen zur Architektur vor der Migration

Die folgenden Annahmen sind für alle Migrationsvorgänge typisch:

- **IaaS:** Es wird allgemein davon ausgegangen, dass die Migration von Workloads in erster Linie das Verschieben von virtuellen Computern aus einem physischen Rechenzentrum über eine IaaS-Migration in Cloudrechenzentrum beinhaltet und nur eine minimale Neuentwicklung oder Neukonfiguration erfordert. Dies wird als _Lift & Shift_-Migration bezeichnet. (Ausnahmen folgen.)
- **Konsistenz der Architektur:** Änderungen an der Kernarchitektur während einer Migration steigern die Komplexität erheblich. Das Debuggen eines geänderten Systems auf einer neuen Plattform beinhaltet unzählige Variablen, die möglicherweise nur schwierig zu isolieren sind. Aus diesem Grund sollten während der Migration nur geringfügige Änderungen an den Workloads vorgenommen werden, die dann auch gründlich getestet werden müssen.
- **Deaktivierungstest:** Migrationsvorgänge und das Hosting von Ressourcen verbrauchen betriebliche Ressourcen und erfordern möglicherweise auch Kapitalausgaben. Es wird vorausgesetzt, dass alle zu migrierenden Workloads daraufhin geprüft wurden, ob sie auch weiterhin genutzt werden. Die Möglichkeit, nicht verwendete Ressourcen außer Kraft zu setzen, führt zu unmittelbaren Kosteneinsparungen.
- **Ändern der Größe von Ressourcen:** Es kann davon ausgegangen werden, dass nur einige der lokalen Ressourcen die zugeordneten Ressourcen vollständig nutzen. Daher sollte die Größe der Ressourcen vor der Migration an die tatsächlichen Nutzungsanforderungen angepasst werden.
- **Anforderungen an Business Continuity & Disaster Recovery (BCDR):** Es wird vorausgesetzt, dass für die Workloads vor der Planung des Releases eine SLA mit dem Unternehmen vereinbart wurde. Diese Anforderungen verringern sehr wahrscheinlich die Anzahl der kleineren Änderungen an der Architektur.
- **Ausfallzeiten während der Migration:** Ebenso können die Ausfallzeiten für die Umstellung der Workloads in die Produktion negative Auswirkungen auf das Geschäft haben. In einigen Fällen erfordern Lösungen, die mit minimalen Ausfallzeiten umgestellt werden müssen, Änderungen an der Architektur. Es wird vorausgesetzt, dass vor der Planung des Releases ein Grundverständnis der Anforderungen von Ausfallzeiten vorhanden ist.

## <a name="roadblocks-that-can-be-avoided"></a>Vermeidbare Hürden

Die aufgeschlüsselten Annahmen können Hindernisse darstellen, die den Vorgang verlangsamen oder zu späteren Problemen führen können. Im Folgenden finden Sie einige Hürden, die Sie vor der Veröffentlichung beachten sollten:

- **Ausgleichen technischer Schulden:** Einige ältere Workloads umfassen ein hohes Maß an technischen Schulden. Dies kann langfristig zu Schwierigkeiten führen und die Hostingkosten bei jedem Cloudanbieter erhöhen. Wenn technische Schulden die Hostingkosten außergewöhnlich steigern, sollten alternative Architekturen in Erwägung gezogen werden.
- **Muster beim Benutzerdatenverkehr:** Bestehende Lösungen hängen möglicherweise von vorhandenen Mustern für das Netzwerkrouting ab. Diese Muster können die Leistung erheblich senken. Darüber hinaus kann die Einführung neuer Hybridlösungen für WANs (Wide Area Network) Wochen oder sogar Monate dauern. Bereiten Sie sich schon frühzeitig bei der Entwicklung einer Architektur auf diese Hürden vor, indem Sie die Datenverkehrsmuster und die Änderungen an Kerndiensten der Infrastruktur berücksichtigen.

## <a name="accelerate-business-value"></a>Beschleunigung von Geschäftswerten

Einige Szenarien erfordern möglicherweise eine andere Architektur, als bei der Strategie für das IaaS-Rehosting angenommen wurde. Im Folgenden finden Sie einige Beispiele:

- PaaS-Alternativen: PaaS-Bereitstellungen können die Hostingkosten und auch die erforderliche Zeit zum Migrieren bestimmter Workloads reduzieren. Eine Liste von Ansätzen, für die ein Wechsel auf PaaS von Vorteil wäre, finden Sie im Artikel zum [Bewerten von Ressourcen](./evaluate.md).
- Skriptgesteuerte Bereitstellungen/DevOps: Wenn es für eine Workload eine DevOps-Bereitstellung oder andere Formen der skriptgesteuerten Bereitstellung gibt, können die Kosten für das Ändern der Skripts möglicherweise niedriger sein als die Kosten für das Migrieren der Ressource.
- Wartungsaufwand: Der Aufwand für die Vorbereitung einer Workload für die Migration kann sehr umfangreich sein. In einigen Fällen ist es sinnvoller, die Lösung zu modernisieren, als die zugrunde liegenden Kompatibilitätsprobleme zu beheben.

In jedem der aufgeführten Szenarien könnte eine alternative Architektur die bessere Lösung sein.

## <a name="next-steps"></a>Nächste Schritte

Nachdem die neue Architektur definiert wurde, können [genaue Kostenschätzungen berechnet werden](./estimate.md).

> [!div class="nextstepaction"]
> [Schätzen der Cloudkosten](./estimate.md)
