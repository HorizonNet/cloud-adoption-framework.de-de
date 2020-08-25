---
title: Grundlegendes zu Cloudbetriebsfunktionen
description: Grundlegendes zur Bildung von Cloudbetriebsfunktionen und der angemessenen Besetzung Ihres Teams.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 5762688ddd367e6f01e7276d9d9079aaf27f56da
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88569976"
---
# <a name="cloud-operations-functions"></a>Cloudbetriebsfunktionen

Ein Betriebsteam konzentriert sich auf die Überwachung, Reparatur sowie die Behebung von Problemen im Zusammenhang mit herkömmlichen IT-Vorgängen und -Ressourcen. In der Cloud werden viele dieser Investitionskosten und Betriebsaktivitäten auf den Cloudanbieter übertragen, was es der IT-Abteilung ermöglicht, sich weiterzuentwickeln und einen erheblichen Mehrwert zu schaffen.

Die für die Bereitstellung von Cloudbetriebsfunktionen erforderlichen Qualifikationen können bereitgestellt werden durch:

- IT-Abläufe
- Anbieter für die Auslagerung der IT-Abläufe
- Clouddienstanbieter
- Cloudgestützte Dienstanbieter
- Anwendungsspezifische Betriebsteams
- Betriebsteams für Geschäftsanwendungen
- DevOps-Teams

> [!IMPORTANT]
> Die für den Betrieb der Cloud zuständigen Personen oder Teams sind in der Regel dafür verantwortlich, reaktive Änderungen an der Konfiguration während der Wartung vorzunehmen. Sie sind wahrscheinlich auch für proaktive Konfigurationsänderungen zuständig, um Störungen der Betriebsabläufe zu minimieren. Je nach Cloudbetriebsmodell der Organisation können diese Änderungen über Infrastructure-as-Code, Azure Pipelines oder direkte Konfiguration im Portal bereitgestellt werden. Da das Betriebsteam wahrscheinlich über erweiterte Berechtigungen verfügen wird, ist es äußerst wichtig, dass diejenigen, die diese Rolle ausfüllen, die [bewährten Methoden der Identitäts- und Zugriffssteuerung](/azure/security/benchmarks/security-control-identity-access-control) befolgen, um unbeabsichtigten Zugriff oder Änderungen in der Produktion zu minimieren.

## <a name="preparation"></a>Vorbereitung

- [Verwalten von Ressourcen in Azure](/learn/paths/manage-resources-in-azure/): Es wird beschrieben, wie Sie die Azure CLI und das Webportal verwenden, um cloudbasierte Ressourcen zu erstellen, zu verwalten und zu steuern.
- [Azure-Netzwerkdienste](/learn/modules/intro-to-azure-networking/): Erlernen Sie die Grundlagen von Azure-Netzwerken, und erfahren Sie, wie die Resilienz verbessert und die Latenz verringert werden kann.

Lesen Sie Folgendes:

- [Geschäftsergebnisse](../strategy/business-outcomes/index.md)
- [Finanzmodelle](../strategy/financial-models.md)
- [Gründe für die Cloudeinführung](../strategy/motivations.md)
- [Geschäftsrisiken](../govern/policy-compliance/risk-tolerance.md)
- [Rationalisierung der digitalen Ressourcen](../digital-estate/index.md)

## <a name="minimum-scope"></a>Mindestumfang

Die Aufgaben der Mitglieder des Cloudbetriebsteams umfassen die Bereitstellung einer maximalen Workloadleistung sowie minimaler Betriebsunterbrechungen innerhalb eines vereinbarten Betriebskostenbudgets.

- Bestimmen der Wichtigkeit der Workload, der Auswirkung von Unterbrechungen oder von Leistungseinbußen.
- Einrichten von vom Unternehmen genehmigten Kosten- und Leistungszusagen.
- Überwachen und Betreiben von Cloudworkloads.

## <a name="deliverables"></a>Ergebnisse

- Verwalten des Ressourcen- und Workloadbestands
- Überwachen der Leistung von Workloads
- Verwalten der betriebsbezogenen Compliance
- Schützen von Workloads und zugeordneter Ressourcen
- Wiederherstellung von Ressourcen im Falle der Leistungsbeeinträchtigung oder der Unterbrechung des Geschäftsbetriebs.
- Ausgereifte Funktionen der Kernplattformen
- Kontinuierliche Verbesserung der Workloadleistung
- Verbesserung der Budget- und Designanforderungen von Workloads, um die Verpflichtungen gegenüber dem Unternehmen zu erfüllen

### <a name="meeting-cadence"></a>Rhythmus von Besprechungen

Das Cloudbetriebsteam sollte an der Release- und Cloudkompetenzzentrums-Planung beteiligt sein, um Feedback bereitzustellen und sich auf die betrieblichen Anforderungen vorzubereiten.

## <a name="out-of-scope"></a>Nicht betreffende Organisationen

Traditionelle IT-Vorgänge, die sich auf die Aufrechterhaltung der Vorgänge im aktuellen Zustand für technische Ressourcen auf niedriger Ebene konzentrieren, gehören nicht zum Aufgabebereich des Cloudbetriebsteams. Faktoren wie Speicher, CPU, Arbeitsspeicher, Netzwerkgeräte, Server und VM-Hosts erfordern kontinuierliche Wartung, Überwachung, Reparatur und Problembehebung, um den Spitzenbetrieb aufrechtzuerhalten. In der Cloud werden viele dieser Kapitalkosten und Betriebsaktivitäten auf den Cloudanbieter übertragen.

## <a name="next-steps"></a>Nächste Schritte

Da Einführung und Abläufe einer Skalierung unterliegen, ist es wichtig, bewährte Methoden für die Governance zu definieren und zu automatisieren, die vorhandene IT-Anforderungen erweitern. Der Aufbau eines Cloudkompetenzzentrums ist ein wichtiger Schritt zur Skalierung der Bemühungen für Cloudeinführung, Cloudbetrieb und Cloudgovernance.

Weitere Informationen:

- Funktionen des [Cloudkompetenzzentrums (CCoE, Cloud Center of Excellence)](../organize/cloud-center-of-excellence.md).
- [Antimuster in Unternehmen: Silos und Machtbereiche](../organize/fiefdoms-silos.md).

Es wird beschrieben, wie Sie Teams übergreifend Zuständigkeiten zuordnen, indem Sie eine so genannte RACI-Matrix entwickeln und damit bestimmen, welche Teams verantwortlich sind (responsible), rechenschaftspflichtig sind (accountable), konsultiert werden (consulted) und zu informieren sind (informed). Herunterladen und Ändern der [RACI-Vorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/organize/raci-template.xlsx).
