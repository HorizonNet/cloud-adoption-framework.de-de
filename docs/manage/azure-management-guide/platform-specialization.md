---
title: Spezialisierte Plattformen für die Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um plattformspezifische Cloudverwaltungsvorgänge, z. B. Verbesserung des Systementwurfs und automatisierte Korrekturmaßnahmen, zu optimieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 73b49894ae375e5c5995e33057d29b48a61e57e2
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86190752"
---
# <a name="platform-specialization-for-cloud-management"></a>Plattformspezialisierung für die Cloudverwaltung

Ähnlich wie bei der optimierten Verwaltungsbaseline ist die Plattformspezialisierung eine Erweiterung, die über die Standardverwaltungsbaseline hinausgeht. Die folgende Abbildung und Liste zeigen die Möglichkeiten zum Erweitern der Verwaltungsbaseline. In diesem Artikel werden die Plattformspezialisierungsoptionen behandelt.

![Über die Baseline zur Cloudverwaltung hinaus](../../_images/manage/beyond-the-baseline.png)

- **Workloadbetrieb:** Die größte Investition pro Workloadvorgang und der höchste Resilienzgrad. Wir empfehlen Workloadvorgänge für etwa 20 % der Workloads, die den Geschäftswert erzeugen. Diese Spezialisierung ist in der Regel für Workloads von hoher Wichtigkeit oder unternehmenskritische Workloads reserviert.
- **Plattformbetrieb:** Die Betriebsinvestition ist auf viele Workloads verteilt. Verbesserungen der Resilienz betreffen alle Workloads, die die definierte Plattform nutzen. Wir empfehlen Plattformvorgänge für die etwa 20 % der Plattformen, die die höchste Wichtigkeit aufweisen. Diese Spezialisierung ist in der Regel für Workloads von mittlerer bis hoher Wichtigkeit reserviert.
- **Erweiterte Verwaltungsbaseline:** Die relativ niedrigste Betriebsinvestition. Diese Spezialisierung verbessert die Erfüllung der Geschäftsverpflichtungen mit zusätzlichen cloudnativen Betriebstools und Prozessen leicht.

Workload- und Plattformbetrieb erfordern Änderungen von Entwurfs- und Architekturprinzipien. Diese Änderungen können Zeit in Anspruch nehmen und zu erhöhten Betriebskosten führen. Um die Anzahl der Workloads zu reduzieren, die solche Investitionen erfordern, kann eine optimierte Verwaltungsbaseline eine ausreichende Verbesserung zur Erfüllung geschäftlicher Verpflichtungen bewirken.

In dieser Tabelle werden einige gängige Prozesse, Tools und potenzielle Auswirkungen beschrieben, die in den optimierten Verwaltungsbaselines der Kunden üblich sind.

| Prozess | Tool | Zweck | Vorgeschlagene Verwaltungsebene |
|---|---|---|---|
| Verbessern des Systementwurfs | Microsoft Azure Well-Architected Framework | Verbessern des Architekturentwurfs der Plattform, um Vorgänge zu verbessern | – |
| Automatisieren der Bereinigung | Azure-Automatisierung | Reagieren auf erweiterte Plattformdaten mit plattformspezifischer Automatisierung | Plattformbetrieb |
| Dienstkatalog | Center für verwaltete Anwendungen | Bereitstellen eines Self-Service-Katalogs genehmigter Lösungen, die Organisationsstandards erfüllen | Plattformbetrieb |
| Containerleistung | Azure Monitor für Container | Überwachung und Diagnose von Containern | Plattformbetrieb |
| Platform-as-a-Service (PaaS) – Datenleistung | Azure SQL-Analysen | Überwachung und Diagnose für PaaS-Datenbanken | Plattformbetrieb |
| Infrastructure-as-a-Service (IaaS) – Datenleistung | SQL Server-Integritätsprüfung | Überwachung und Diagnose für IaaS-Datenbanken | Plattformbetrieb |

## <a name="high-level-process"></a>Allgemeiner Prozess

Die Plattformspezialisierung besteht aus einer disziplinierten Ausführung der folgenden vier Prozesse in einem iterativen Ansatz. Jeder Prozess wird in späteren Abschnitten dieses Artikels ausführlicher erläutert.

- **Verbessern des Systementwurfs:** Verbesserung des Entwurfs gängiger Systeme oder Plattformen, um Unterbrechungen effektiv zu minimieren.
- **Automatisieren der Korrektur:** Einige Verbesserungen sind nicht wirtschaftlich. In solchen Fällen könnte es sinnvoller sein, die Korrektur zu automatisieren und die Auswirkungen von Unterbrechungen zu reduzieren.
- **Skalieren der Lösung:** Bei verbessertem Systementwurf und automatisierter Korrektur können diese Änderungen über den Dienstkatalog in der gesamten Umgebung skaliert werden.
- **Fortlaufende Verbesserung:** Verschiedene Überwachungstools können verwendet werden, um schrittweise Verbesserungen zu erkennen. Diese Verbesserungen können im nächsten Durchgang von Systementwurf, Automatisierung und Skalierung behoben werden.

::: zone target="docs"

## <a name="improve-system-design"></a>Verbessern des Systementwurfs

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-design"></a>[Verbessern des Systementwurfs](#tab/SystemsDesign)

::: zone-end

Das Verbessern des Systementwurfs ist der effektivste Ansatz zur Optimierung des Betriebs jeder gängigen Plattform. Durch Verbesserungen des Systementwurfs können die Stabilität erhöht und Betriebsunterbrechungen verringert werden. Der Entwurf einzelner Systeme wird für die Umgebungssicht nicht berücksichtigt, die das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure einnimmt.

Als Ergänzung zu diesem Framework bietet das [Microsoft Azure Well-Architected Framework](https://docs.microsoft.com/azure/architecture/framework) Grundsätze zum Verbessern einer Plattform oder einer bestimmten Workload. Der Schwerpunkt des Frameworks liegt auf der Verbesserung von fünf Säulen der Architekturexzellenz:

- **Kostenoptimierung:** Verwalten der Kosten zur Maximierung des erzielten Werts.
- **Betriebliche Exzellenz:** Verfolgen der operativen Prozesse, die für die Ausführung eines Systems in der Produktion sorgen.
- **Effiziente Leistung:** Skalieren Sie Systeme so, dass Sie in Bezug auf Änderungen der Last flexibel sind.
- **Zuverlässigkeit:** Entwerfen Sie Systeme so, dass sie nach Ausfällen wiederhergestellt und weiterhin ausgeführt werden können.
- **Sicherheit**: Schützen Sie Anwendungen und Daten vor Bedrohungen.

Technische Schulden und architektonische Mängel verursachen die meisten Unterbrechungen des Geschäftsbetriebs. Bei bestehenden Bereitstellungen können Verbesserungen des Systementwurfs als das Abtragen bestehender technischer Schulden angesehen werden. Bei neuen Bereitstellungen können Sie diese Verbesserungen als Vermeidung von technischen Schulden betrachten.

Die folgende Registerkarte **Automatisierte Korrektur** zeigt Wege zur Behebung von technischen Schulden, die nicht behandelt werden können oder sollten.

Erfahren Sie mehr über das [Microsoft Azure Well-Architected Framework](https://docs.microsoft.com/azure/architecture/framework) zum Verbessern des Systementwurfs.

Bei zunehmender Verbesserung des Systementwurfs kehren Sie zu diesem Artikel zurück, um neue Möglichkeiten zur Verbesserung und Skalierung dieser Verbesserungen in Ihrer Umgebung zu finden.

::: zone target="docs"

## <a name="automated-remediation"></a>Automatisierte Korrektur

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediation"></a>[Automatisierte Korrektur](#tab/AutomatedRemediation)

::: zone-end

Einige technische Schulden können nicht angegangen werden. Die Lösung ist möglicherweise zu teuer, um korrigiert zu werden, oder sie ist geplant, hat aber eine lange Projektlaufzeit. Die Unterbrechung des Geschäftsbetriebs hat möglicherweise keine wesentlichen Auswirkungen auf das Geschäft. Oder die Geschäftspriorität könnte in einer schnellen Wiederherstellung bestehen, anstatt in Resilienz zu investieren.

Wenn die Beseitigung technischer Schulden nicht der gewünschte Ansatz ist, ist die automatisierte Korrektur häufig der nächste Schritt. Der gängigste Ansatz für die automatisierte Korrektur ist der Einsatz von Azure Automation und Azure Monitor zur Erkennung von Trends und Bereitstellung automatisierter Korrekturen.

Anleitungen zur automatisierten Korrektur finden Sie unter [Azure Automation und Warnungen](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Skalieren der Lösung mit einem Dienstkatalog

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalog"></a>[Skalieren der Lösung mit einem Dienstkatalog](#tab/ServiceCatalog)

::: zone-end

Der Eckpfeiler der Plattformspezialisierung und des Plattformbetriebs ist ein sorgfältig gepflegter Dienstkatalog. Durch die Verwendung eines Katalogs werden Verbesserungen bei Systementwurf und -korrektur in einer Umgebung skaliert.

Das Cloudplattform- und Cloudautomatisierungsteam stimmen sich ab, um wiederholbare Lösungen für die gängigsten Plattformen in jeder Umgebung zu schaffen. Wenn diese Lösungen jedoch nicht konsistent verwendet werden, kann die Cloudverwaltung kaum mehr bieten als ein Baselineangebot.

Um die Akzeptanz zu maximieren und den Wartungsaufwand einer optimierten Plattform zu minimieren, sollten Sie die Plattform in einen Azure-Dienstkatalog aufnehmen. Jede Anwendung im Katalog kann über den Dienstkatalog für den internen Einsatz oder als Marketplace-Angebot für externe Nutzer bereitgestellt werden.

Anweisungen zur Veröffentlichung in einem Dienstkatalog finden Sie in der Artikelreihe zum [Veröffentlichen in einem Dienstkatalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Bereitstellen von Anwendungen aus dem Dienstkatalog

1. Wechseln Sie im Azure-Portal zu **Center für verwaltete Anwendungen (Vorschau)** .
2. Wählen Sie im Bereich **Durchsuchen** die Option **Dienstkataloganwendungen** aus.
3. Wählen Sie **+ Hinzufügen** aus, um eine Anwendungsdefinition aus dem Dienstkatalog Ihres Unternehmens auszuwählen.

Alle verwalteten Anwendungen, die Sie warten, werden angezeigt.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Verwalten von Dienstkataloganwendungen

1. Wechseln Sie im Azure-Portal zu **Center für verwaltete Anwendungen (Vorschau)** .
1. Wählen Sie im Bereich **Dienst** die Option **Dienstkataloganwendungen** aus.

Alle verwalteten Anwendungen, die Sie warten, werden angezeigt.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Fortlaufende Verbesserung

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvement"></a>[Fortlaufende Verbesserung](#tab/ContinuousImprovement)

::: zone-end

Sowohl Plattformspezialisierung als auch Plattformbetrieb hängen von funktionierenden Feedbackschleifen zwischen dem Einführungs-, Plattform-, Automatisierungs- und Verwaltungsteam ab. Die Kopplung dieser Feedbackschleifen mit Daten unterstützt jedes Team beim Treffen kluger Entscheidungen. Damit beim Plattformbetrieb langfristige Geschäftsverpflichtungen erfüllt werden können, ist es wichtig, die für die zentralisierte Plattform spezifischen Erkenntnisse zu nutzen.

Container und SQL Server sind die beiden am häufigsten verwendeten zentral verwalteten Plattformen. Diese Artikel können Ihnen bei den ersten Schritten mit der fortlaufend verbesserten Datensammlung auf diesen Plattformen helfen:

- [Containerleistung](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [PaaS-Datenbankleistung](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [IaaS-Datenbankleistung](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
