---
title: Workloadspezialisierung für die Cloudverwaltung in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verbessern von workloadpezifischen Cloudverwaltungsvorgängen
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 51bdf23ccb2262202dfa095c5e9b57f727d11d3b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556988"
---
# <a name="workload-specialization-for-cloud-management"></a>Workloadspezialisierung für die Cloudverwaltung

Die Workloadspezialisierung baut auf den unter [Plattformspezialisierung](./platform-specialization.md) erläuterten Konzepten auf.

![Über die Baseline zur Cloudverwaltung hinaus](../../_images/manage/beyond-the-baseline.png)

- **Workloadbetrieb:** Größte Investition pro Workloadvorgang. Höchster Resilienzgrad. Empfohlen für die ca. 20 % der Workloads, die Geschäftswert erzeugen. In der Regel für Workloads von hoher Wichtigkeit oder unternehmenskritische Workloads reserviert.
- **Plattformbetrieb:** Die Betriebsinvestition ist auf viele Workloads verteilt. Verbesserungen der Resilienz betreffen alle Workloads, die die definierte Plattform nutzen. Empfohlen für die ca. 20 % der Plattformen, die die höchste Wichtigkeit aufweisen. In der Regel für Workloads von mittlerer bis hoher Wichtigkeit reserviert.
- **Erweiterte Verwaltungsbaseline:** Niedrigste relative Betriebsinvestition. Leicht verbesserte Erfüllung der Geschäftsverpflichtungen mit zusätzlichen cloudnativen Betriebstools und Prozessen.

## <a name="high-level-process"></a>Allgemeiner Prozess

Die Workloadspezialisierung besteht aus einer disziplinierten Ausführung der folgenden vier Prozesse in einem iterativen Ansatz. Die einzelnen Prozesse sind im Artikel [Plattformspezialisierung](./platform-specialization.md) näher beschrieben.

- **Verbessern des Systementwurfs:** Verbesserung des Entwurfs spezifischer Workloads, um Unterbrechungen effektiv zu minimieren.
- **Automatisieren der Korrektur:** Einige Verbesserungen sind nicht wirtschaftlich. In solchen Fällen kann es sinnvoller sein, die Korrektur zu automatisieren und die Auswirkungen von Unterbrechungen zu reduzieren.
- **Skalieren der Lösung:** Bei verbessertem Systementwurf und automatisierter Korrektur können diese Änderungen über den Dienstkatalog in der gesamten Umgebung skaliert werden.
- **Fortlaufende Verbesserung:** Es können verschiedene Überwachungstools eingesetzt werden, um inkrementelle Verbesserungen zu identifizieren, die im nächsten Durchlauf des Entwurfs, der Automatisierung und der Skalierung des Systems berücksichtigt werden können.

## <a name="cultural-change"></a>Kulturänderung

Eine Workloadspezialisierung löst häufig eine kulturelle Änderung aus. In der traditionellen IT werden Prozesse erstellt, die sich auf die Bereitstellung einer Verwaltungsbaseline, einer erweiterten Baseline und des Plattformbetriebs konzentrieren. Diese Angebotstypen können über die gesamte Umgebung hinweg skaliert werden. Die Workloadspezialisierung ähnelt in der Ausführung der Plattformspezialisierung. Im Gegensatz zu gängigen Plattformen lässt sich die für einzelne Workloads erforderliche Spezialisierung allerdings häufig nicht skalieren.

Wenn eine Workloadspezialisierung erforderlich ist, wird die Betriebsverwaltung häufig über eine zentrale IT-Perspektive hinaus weiterentwickelt. Im Cloud Adoption Framework wird als Ansatz die Verteilung von Cloudverwaltungsfunktionen vorgeschlagen.

In diesem Modell werden Betriebsaufgaben wie Überwachung, Bereitstellung, DevOps und andere innovationsorientierte Funktionen in eine spezielle für die Anwendungsentwicklung oder eine Geschäftseinheit zuständige Organisation verlagert. Das Cloudplattformteam und das Kernteam für die Cloudüberwachung erfüllen dabei weiterhin alle Anforderungen der Verwaltungsbaseline in der Umgebung. Diese zentralisierten Teams leiten und unterweisen auch spezialisierte Workloadteams im Hinblick auf den Betrieb ihrer Workloads. Die tägliche operative Verantwortung liegt jedoch bei einem Cloudverwaltungsteam, das sich außerhalb der IT befindet. Diese Art der dezentralen Steuerung ist einer der wichtigsten Indikatoren für die Ausgereiftheit eines Cloud Center of Excellence.

## <a name="beyond-platform-specialization---application-insights"></a>Über die Plattformspezialisierung hinaus – Application Insights

Um einen klar strukturierten Workloadbetrieb zu ermöglichen, sind genauere Angaben zur spezifischen Workload erforderlich. Während der Phase der kontinuierlichen Verbesserung ist Application Insights eine notwendige Ergänzung der Toolkette für die Cloudverwaltung.

|Anwendungsüberwachung|Application Insights|Überwachung und Diagnose für Apps| |Leistung, Verfügbarkeit, Nutzung|Application Insights|Erweiterte Anwendungsüberwachung mit App-Dashboard, Verbundzuordnungen, Nutzung und Ablaufverfolgung|

### <a name="deploy-application-insights"></a>Bereitstellen von Application Insights

1. Suchen Sie im Azure-Portal nach **Application Insights**.
2. Klicken Sie auf **+ Hinzufügen**, um eine Application Insights-Ressource zur Überwachung Ihrer Live-Web-App zu erstellen.
3. Befolgen Sie die Anweisungen auf dem Bildschirm.

Informationen zum Konfigurieren Ihrer Anwendung für die Überwachung finden Sie in der Dokumentation zu [Azure Monitor Application Insights](https://docs.microsoft.com/azure/azure-monitor/azure-monitor-app-hub).

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Überwachen der Leistung, Verfügbarkeit und Nutzung

1. Suchen Sie im Azure-Portal nach **Application Insights**.
2. Wählen Sie eine der Application Insights-Ressourcen aus der Liste aus.

Das Navigationsmenü von Application Insights enthält eine Vielzahl von Optionen zum Überwachen von Leistung, Verfügbarkeit, Nutzung und Abhängigkeiten. Jede dieser Ansichten der Anwendungsdaten bietet klare Einblicke in die Feedbackschleife für kontinuierliche Verbesserungen.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
