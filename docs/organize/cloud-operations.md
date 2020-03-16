---
title: Funktionen für den Cloudbetrieb
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit Funktionen für den Cloudbetrieb vertraut zu machen und dafür zu sorgen, dass IT-Vorgänge optimiert werden und zu zusätzlichem Nutzen führen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 75077ee51cb5962c6553032e071fe0cc54505f6a
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092731"
---
# <a name="cloud-operation-capabilities"></a>Funktionen für den Cloudbetrieb

Die Unternehmenstransformation kann durch die Cloudeinführung ermöglicht werden. Erträge werden jedoch nur dann realisiert, wenn die in der Cloud bereitgestellten Workloads entsprechend den Leistungserwartungen funktionieren. Da zusätzliche Workloads Cloudtechnologien einführen, ist eine zusätzliche Betriebskapazität erforderlich.

Traditionelle IT-Vorgänge mussten sich auf die Aufrechterhaltung der Vorgänge im aktuellen Zustand für eine Vielzahl von technischen Ressourcen auf niedriger Ebene konzentrieren. Faktoren wie Speicher, CPU, Arbeitsspeicher, Netzwerkgeräte, Server und VM-Hosts erfordern eine kontinuierliche Wartung, um den Spitzenbetrieb aufrechtzuerhalten. Die Finanzierungspläne enthalten oft hohe Ausgaben im Zusammenhang mit jährlichen oder periodischen Aktualisierungen dieser Ressourcen auf niedriger Ebene.

 Die Humanressourcen im operativen Bereich würden sich auch stark auf die Überwachung, Reparatur und Bereinigung von Problemen im Zusammenhang mit diesen Ressourcen konzentrieren. In der Cloud werden viele dieser Kapitalkosten und Betriebsaktivitäten auf den Cloudanbieter übertragen. Dies eröffnet den IT-Abläufen die Möglichkeit, sich zu verbessern und einen erheblichen Mehrwert zu schaffen.

## <a name="possible-sources-for-this-capability"></a>Mögliche Quellen für diese Funktionen

Die für die Bereitstellung von Funktionen für den Cloudbetrieb erforderlichen Qualifikationen könnten bereitgestellt werden durch:

- IT-Abläufe
- Anbieter für die Auslagerung der IT-Abläufe
- Clouddienstanbieter
- Cloudgestützte Dienstanbieter
- Anwendungsspezifische Betriebsteams
- Betriebsteams für Geschäftsanwendungen
- DevOps-Teams

## <a name="key-responsibilities"></a>Wichtige Zuständigkeiten

Die Aufgaben der Verantwortlichen für die Bereitstellung der Funktionen für den Cloudbetrieb sind die Bereitstellung einer maximalen Workloadleistung und minimaler Betriebsunterbrechungen innerhalb der vereinbarten Betriebskosten.

### <a name="strategic-tasks"></a>Strategische Aufgaben

- Überprüfen der [Geschäftsergebnisse](../strategy/business-outcomes/index.md), [Finanzmodelle](../strategy/financial-models.md), [Motivationen für die Cloudeinführung](../strategy/motivations.md), [Geschäftsrisiken](../govern/policy-compliance/risk-tolerance.md) und der [Rationalisierung der digitalen Ressourcen](../digital-estate/index.md).
- Bestimmen der Wichtigkeit der Workload, der Auswirkung von Unterbrechungen oder von Leistungseinbußen.
- Einrichten von vom Unternehmen genehmigten Kosten-/Leistungszusagen.
- Überwachen und Betreiben von Cloudworkloads.

### <a name="technical-tasks"></a>Technische Aufgaben

- Verwalten des Ressourcen- und Workloadbestands.
- Überwachen der Leistung von Workloads.
- Verwalten der betriebsbezogenen Compliance.
- Schützen von Workloads und zugeordneten Ressourcen.
- Wiederherstellung von Ressourcen im Falle der Leistungsbeeinträchtigung oder der Unterbrechung des Geschäftsbetriebs.
- Ausgereifte Funktionen der Kernplattformen.
- Kontinuierliche Verbesserung der Workloadleistung.
- Verbesserung der Budget- und Designanforderungen von Workloads, um die Verpflichtungen gegenüber dem Unternehmen zu erfüllen.

## <a name="meeting-cadence"></a>Rhythmus von Besprechungen

Diejenigen, die Funktionen für den Cloudbetrieb ausführen, sollten an der Release- und Cloudkompetenzzentrums-Planung beteiligt sein, um Feedback bereitzustellen und sich auf die betrieblichen Anforderungen vorzubereiten.

## <a name="next-steps"></a>Nächste Schritte

Da Einführung und Abläufe einer Skalierung unterliegen, ist es wichtig, bewährte Methoden für die Governance zu definieren und zu automatisieren, die vorhandene IT-Anforderungen erweitern. Der Aufbau eines [Cloudkompetenzzentrums](./cloud-center-of-excellence.md) ist ein wichtiger Schritt zur Skalierung der Bemühungen für Cloudeinführung, Cloudbetrieb und Cloudgovernance.

> [!div class="nextstepaction"]
> [Einrichten eines Cloudkompetenzzentrums](./cloud-center-of-excellence.md)
