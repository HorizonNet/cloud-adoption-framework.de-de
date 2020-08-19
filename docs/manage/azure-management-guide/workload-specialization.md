---
title: Spezialisierte Workloads für die Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit spezialisierten Workloads für Cloudverwaltungsvorgänge vertraut zu machen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 24fcb5842f6151ac6beba8820391078bd64d3050
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88567528"
---
# <a name="workload-specialization-for-cloud-management"></a>Workloadspezialisierung für die Cloudverwaltung

Die Workloadspezialisierung baut auf den unter [Plattformspezialisierung](./platform-specialization.md) erläuterten Konzepten auf.

![Über die Baseline zur Cloudverwaltung hinaus](../../_images/manage/beyond-the-baseline.png)

- **Workloadbetrieb:** Die größte Investition pro Workloadvorgang und der höchste Resilienzgrad. Wir empfehlen Workloadvorgänge für etwa 20 % der Workloads, die den Geschäftswert erzeugen. Diese Spezialisierung ist in der Regel für Workloads von hoher Wichtigkeit oder unternehmenskritische Workloads reserviert.
- **Plattformbetrieb:** Die Betriebsinvestition ist auf viele Workloads verteilt. Verbesserungen der Resilienz betreffen alle Workloads, die die definierte Plattform nutzen. Wir empfehlen Plattformvorgänge für die etwa 20 % der Plattformen, die die höchste Wichtigkeit aufweisen. Diese Spezialisierung ist in der Regel für Workloads von mittlerer bis hoher Wichtigkeit reserviert.
- **Erweiterte Verwaltungsbaseline:** Die relativ niedrigste Betriebsinvestition. Diese Spezialisierung verbessert die Erfüllung der Geschäftsverpflichtungen mit zusätzlichen cloudnativen Betriebstools und Prozessen leicht.

## <a name="high-level-process"></a>Allgemeiner Prozess

Die Workloadspezialisierung besteht aus einer disziplinierten Ausführung der folgenden vier Prozesse in einem iterativen Ansatz. Die einzelnen Prozesse sind unter [Plattformspezialisierung](./platform-specialization.md) näher beschrieben.

- **Verbessern des Systementwurfs:** Verbesserung des Entwurfs spezifischer Workloads, um Unterbrechungen effektiv zu minimieren.
- **Automatisieren der Korrektur:** Einige Verbesserungen sind nicht wirtschaftlich. In solchen Fällen könnte es sinnvoller sein, die Korrektur zu automatisieren und die Auswirkungen von Unterbrechungen zu reduzieren.
- **Skalieren der Lösung:** Während Sie den Systementwurf und die automatisierte Korrektur verbessern, können Sie diese Änderungen über den Dienstkatalog in der gesamten Umgebung skalieren.
- **Fortlaufende Verbesserung:** Verschiedene Überwachungstools können verwendet werden, um schrittweise Verbesserungen zu erkennen. Diese Verbesserungen können im nächsten Durchgang von Systementwurf, Automatisierung und Skalierung behoben werden.

## <a name="cultural-change"></a>Kulturänderung

Eine Workloadspezialisierung löst häufig eine kulturelle Änderung in traditionellen IT-Erstellungsprozessen aus, die sich auf die Bereitstellung einer Verwaltungsbaseline, einer erweiterten Baseline und des Plattformbetriebs konzentrieren. Diese Angebotstypen können über die gesamte Umgebung hinweg skaliert werden. Die Workloadspezialisierung ähnelt in der Ausführung der Plattformspezialisierung. Im Gegensatz zu gängigen Plattformen lässt sich die für einzelne Workloads erforderliche Spezialisierung allerdings häufig nicht skalieren.

Wenn eine Workloadspezialisierung erforderlich ist, wird die Betriebsverwaltung häufig über eine zentralisierte IT-Perspektive hinaus weiterentwickelt. In Cloud Adoption Framework wird als Ansatz die Verteilung von Cloudverwaltungsfunktionen vorgeschlagen.

In diesem Modell werden Betriebsaufgaben wie Überwachung, Bereitstellung, DevOps und andere innovationsorientierte Funktionen in eine spezielle für die Anwendungsentwicklung oder eine Geschäftseinheit zuständige Organisation verlagert. Das Cloudplattformteam und das Kernteam für die Cloudüberwachung erfüllen dabei weiterhin alle Anforderungen der Verwaltungsbaseline in der Umgebung.

Diese zentralisierten Teams leiten und unterweisen auch spezialisierte Workloadteams im Hinblick auf den Betrieb ihrer Workloads. Die tägliche operative Verantwortung liegt jedoch bei einem Cloudverwaltungsteam, das sich außerhalb der IT befindet. Diese Art der dezentralen Steuerung ist einer der wichtigsten Indikatoren für die Ausgereiftheit eines Cloudkompetenzzentrums.

## <a name="beyond-platform-specialization-application-insights"></a>Über die Plattformspezialisierung hinaus: Application Insights

Um einen klar strukturierten Workloadbetrieb zu ermöglichen, sind genauere Angaben zur spezifischen Workload erforderlich. Während der Phase der kontinuierlichen Verbesserung ist Application Insights eine notwendige Ergänzung der Toolkette für die Cloudverwaltung.

| Anforderung                          | Tool                 | Zweck                                                                                |
| ------------------------------------ | -------------------- | -------------------------------------------------------------------------------------- |
| Anwendungsüberwachung               | Application Insights | Überwachung und Diagnose für Apps                                                    |
| Leistung, Verfügbarkeit und Nutzung | Application Insights | Erweiterte Anwendungsüberwachung mit Anwendungsdashboard, Verbundzuordnungen, Nutzung und Ablaufverfolgung |

### <a name="deploy-application-insights"></a>Bereitstellen von Application Insights

1. Wechseln Sie im Azure-Portal zu **Application Insights**.
1. Wählen Sie **+ Hinzufügen** aus, um eine Application Insights-Ressource zur Überwachung Ihrer Live-Web-App zu erstellen.
1. Befolgen Sie die Anweisungen auf dem Bildschirm.

Informationen zum Konfigurieren Ihrer Anwendung für die Überwachung finden Sie in der Dokumentation zu [Azure Monitor Application Insights](/azure/azure-monitor/azure-monitor-app-hub).

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Überwachen der Leistung, Verfügbarkeit und Nutzung

1. Suchen Sie im Azure-Portal nach **Application Insights**.
1. Wählen Sie eine der Application Insights-Ressourcen aus der Liste aus.

Application Insights enthält verschiedene Arten von Optionen zur Überwachung von Leistung, Verfügbarkeit, Nutzung und Abhängigkeiten. Jede dieser Ansichten der Anwendungsdaten bietet klare Einblicke in die Feedbackschleife für kontinuierliche Verbesserungen.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Insights%2FComponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
