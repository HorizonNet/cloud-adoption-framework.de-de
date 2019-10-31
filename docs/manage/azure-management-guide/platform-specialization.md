---
title: Plattformspezialisierung für die Cloudverwaltung in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Verbessern Sie plattformspezifische Cloudverwaltungsvorgänge.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0386a8c30758cce6c1c3d23bfa73d1f90e919692
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556971"
---
# <a name="platform-specialization-for-cloud-management"></a>Plattformspezialisierung für die Cloudverwaltung

Ähnlich wie bei der optimierten Verwaltungsbaseline ist die Plattformspezialisierung eine Erweiterung, die über die Standardverwaltungsbaseline hinausgeht. Im Folgenden finden Sie ein Visual und eine Aufzählungsliste der Möglichkeiten zum Erweitern der Verwaltungsbaseline. In diesem Artikel wird die Plattformspezialisierungsoption behandelt.

![Über die Cloudverwaltungsbaseline hinaus](../../_images/manage/beyond-the-baseline.png)

- **Workloadbetrieb:** Größte Investition pro Workloadvorgang. Höchster Resilienzgrad. Empfohlen für +/-20 % der Workloads, die den Geschäftswert erzeugen. In der Regel für Workloads von hoher Wichtigkeit oder unternehmenskritische Workloads reserviert.
- **Plattformbetrieb:** Die Betriebsinvestition ist auf viele Workloads verteilt. Verbesserungen der Resilienz betreffen alle Workloads, die die definierte Plattform nutzen. Empfohlen für +/-20 % der Plattformen von höchster Wichtigkeit. In der Regel für Workloads von mittlerer bis hoher Wichtigkeit reserviert.
- **Optimierte Verwaltungsbaseline:** Niedrigste relative Betriebsinvestition. Leicht verbesserte Erfüllung der Geschäftsverpflichtungen mit zusätzlichen cloudnativen Betriebstools und Prozessen.

Workload- und Plattformbetrieb erfordern Änderungen von Entwurfs- und Architekturprinzipien. Diese Änderungen können Zeit in Anspruch nehmen und zu erhöhten Betriebskosten führen. Um die Anzahl der Workloads zu reduzieren, die solche Investitionen erfordern, kann eine optimierte Verwaltungsbaseline eine ausreichende Verbesserung zur Erfüllung der Geschäftsverpflichtungen bewirken.

In der folgenden Tabelle werden einige gängige Prozesse, Tools und potenzielle Auswirkungen beschrieben, die in den optimierten Verwaltungsbaselines der Kunden üblich sind.

|Prozess  |Tool  |Zweck  |Vorgeschlagene Verwaltungsebene  |
|---------|---------|---------|---------|
|Verbessern des Systementwurfs|Azure Architecture Framework|Verbessern des Architekturentwurfs der Plattform, um Vorgänge zu verbessern|
|Automatisieren der Korrektur|Azure-Automatisierung|Reagieren auf erweiterte Plattformdaten mit plattformspezifischer Automatisierung|Plattformbetrieb|
|Dienstkatalog|Center für verwaltete Anwendungen|Bereitstellen eines Self-Service-Katalogs genehmigter Lösungen, die Organisationsstandards erfüllen|Plattformbetrieb|
|Containerleistung|Azure Monitor für Container|Überwachung und Diagnose von Containern|Plattformbetrieb|
|PaaS-Datenleistung|Azure SQL-Analysen|Überwachung und Diagnose für PaaS-DBs|Plattformbetrieb|
|IaaS-Datenleistung|SQL Server-Integritätsprüfung|Überwachung und Diagnose für IaaS-DBs|Plattformbetrieb|

## <a name="high-level-process"></a>Allgemeiner Prozess

Die Plattformspezialisierung besteht aus einer disziplinierten Ausführung der folgenden vier Prozesse in einem iterativen Ansatz. Jeder Prozess wird in den folgenden Abschnitten dieses Artikels ausführlicher erläutert.

- **Verbessern des Systementwurfs:** Verbesserung des Entwurfs gängiger Systeme (oder Plattformen), um Unterbrechungen effektiv zu minimieren.
- **Automatisieren der Korrektur:** Einige Verbesserungen sind nicht wirtschaftlich. In solchen Fällen kann es sinnvoller sein, die Korrektur zu automatisieren und die Auswirkungen von Unterbrechungen zu reduzieren.
- **Skalieren der Lösung:** Bei verbessertem Systementwurf und automatisierter Korrektur können diese Änderungen über den Dienstkatalog in der gesamten Umgebung skaliert werden.
- **Fortlaufende Verbesserung:** Verschiedene Überwachungstools können eingesetzt werden, um schrittweise Verbesserungen zu identifizieren, die im nächsten Prozessschritt beim Systementwurf, der Automatisierung und der Skalierung berücksichtigt werden können.

::: zone target="docs"

## <a name="improve-system-design"></a>Verbessern des Systementwurfs

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Verbessern des Systementwurfs](#tab/SystemsDesign)

::: zone-end

Das Verbessern des Systementwurfs ist der effektivste Ansatz zur Optimierung des Betriebs jeder gängigen Plattform. Durch Verbesserungen des Systementwurfs können die Stabilität erhöht und Betriebsunterbrechungen verringert werden. Der Entwurf einzelner Systeme wird für die Umgebungssicht nicht berücksichtigt, die das Framework für die Cloudeinführung (Cloud Adoption Framework) einnimmt. Als Ergänzung dieses Frameworks bietet das Azure Architecture Framework bewährte Methoden zur Verbesserung der Resilienz und des Entwurfs eines bestimmten Systems. Diese Entwurfsverbesserungen können für den Systementwurf einer Plattform oder einer bestimmten Workload übernommen werden.

Das Azure Architecture Framework konzentriert sich auf die Verbesserung von fünf Grundpfeilern des Systementwurfs:

- **Skalierbarkeit:** Skalieren der allgemeinen Plattformressourcen, um eine gestiegene Last zu bewältigen.
- **Verfügbarkeit:** Verringern von Geschäftsunterbrechungen durch Verlängern der potenziellen Betriebszeit.
- **Resilienz:** Verkürzen von Wiederherstellungszeiten und dadurch der Dauer von Unterbrechungen.
- **Sicherheit**: Schützen von Anwendungen und Daten vor externen Bedrohungen.
- **Verwaltung:** Spezifisch für diese allgemeinen Plattformressourcen erfolgende Betriebsprozesse.

Die meisten Betriebsunterbrechungen sind Folge einer Form von technischen Schulden oder einer unzulänglichen Architektur. Bei bestehenden Bereitstellungen können Verbesserungen des Systementwurfs als das Abtragen bestehender technischer Schulden angesehen werden. Bei Neubereitstellungen können Verbesserungen des Systementwurfs als das Vermeiden technischer Schulden verstanden werden. Der nächste Abschnitt, „Automatisierte Korrektur“, befasst sich mit Möglichkeiten, technische Schulden anzugehen, die nicht beseitigt werden können oder sollten.

Erfahren Sie mehr über das [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars) zum Verbessern des Systementwurfs.

Bei zunehmender Verbesserung des Systementwurfs kehren Sie zu diesem Artikel zurück, um neue Möglichkeiten zur Verbesserung und Skalierung dieser Verbesserungen in Ihrer Umgebung zu finden.

::: zone target="docs"

## <a name="automated-remediation"></a>Automatisierte Korrektur

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Automatisierte Korrektur](#tab/AutomatedRemediation)

::: zone-end

Einige technische Schulden können nicht angegangen werden. Grund sind die Kosten ihrer Beseitigung. Die Beseitigung könnte zwar geplant werden, aber eine lange Projektdauer mit sich bringen. Es könnte sein, dass die Betriebsunterbrechung keine signifikanten Auswirkungen auf den Geschäftsbetrieb hat oder dass es vorrangig darum geht, eine schnelle Wiederherstellung zu erreichen, anstatt in Resilienz zu investieren.

Wenn die Beseitigung technischer Schulden nicht das gewünschte Ziel ist, ist die automatisierte Korrektur häufig der gewünschte nächste Schritt. Der gängigste Ansatz für die automatisierte Korrektur ist der Einsatz von Azure Automation und Azure Monitor zur Erkennung von Trends und Bereitstellung automatisierter Korrekturen.

Anleitungen zur automatisierten Korrektur finden Sie in diesem Artikel zu [Azure Automation und Warnungen](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Skalieren der Lösung mit einem Dienstkatalog

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Skalieren der Lösung mit einem Dienstkatalog](#tab/ServiceCatalog)

::: zone-end

Der Eckpfeiler der Plattformspezialisierung und des Plattformbetriebs ist ein sorgfältig gepflegter Dienstkatalog. Auf diese Weise werden Verbesserungen bei Systementwurf und -korrektur in einer Umgebung skaliert. Das Cloudplattform- und Cloudautomatisierungsteam stimmen sich ab, um wiederholbare Lösungen für die gängigsten Plattformen in jeder Umgebung zu schaffen. Wenn diese Lösungen jedoch nicht konsequent umgesetzt werden, kann die Cloudverwaltung kaum mehr bieten als ein Baselineangebot.

Um die Akzeptanz zu maximieren und den Wartungsaufwand einer optimierten Plattform zu minimieren, sollte die Plattform in einen Dienstkatalog in Azure aufgenommen werden. Jede Anwendung im Katalog kann über den Dienstkatalog für den internen Einsatz oder als Marketplace-Angebot für externe Nutzer bereitgestellt werden.

Anweisungen zur Veröffentlichung in einem Dienstkatalog finden Sie in der Artikelreihe zum [Veröffentlichen in einem Dienstkatalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Bereitstellen von Anwendungen aus dem Dienstkatalog

1. Suchen Sie im Azure-Portal nach **Center für verwaltete Anwendungen (Vorschau)** .
2. Klicken Sie im Navigationsbereich des Portals unter **Durchsuchen** auf **Dienstkataloganwendungen**.
3. Klicken Sie auf **+ Hinzufügen**, um eine Anwendungsdefinition aus dem Dienstkatalog Ihres Unternehmens auszuwählen.

Alle verwalteten Anwendungen, die Sie warten, werden hier angezeigt.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Verwalten von Dienstkataloganwendungen

1. Suchen Sie im Azure-Portal nach **Center für verwaltete Anwendungen (Vorschau)** .
2. Klicken Sie im Navigationsbereich des Portals unter **Dienst** auf **Dienstkataloganwendungen**.

Alle verwalteten Anwendungen, die Sie warten, werden hier angezeigt.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Fortlaufende Verbesserung

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvementtabcontinuousimprovement"></a>[Fortlaufende Verbesserung](#tab/ContinuousImprovement)

::: zone-end

Sowohl Plattformspezialisierung als auch Plattformbetrieb hängen von funktionierenden Feedbackschleifen zwischen dem Einführungs-, Plattform-, Automatisierungs- und Verwaltungsteam ab. Die Kopplung dieser Feedbackschleifen mit Daten ermöglicht jedem Team, kluge Entscheidungen zu treffen. Damit beim Plattformbetrieb langfristige Geschäftsverpflichtungen erfüllt werden können, ist es wichtig, die für die zentralisierte Plattform spezifischen Erkenntnisse zu nutzen. Da Container und SQL Server die beiden am häufigsten verwendeten zentral verwalteten Plattformen sind, finden Sie im Folgenden einige Artikel, die Ihnen den Einstieg in die fortlaufende Verbesserung der Datensammlung erleichtern.

[Azure Monitor für Container – Übersicht](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
[Überwachen von Azure SQL-Datenbank mithilfe von Azure SQL-Analyse (Vorschauversion)](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
[Optimieren der SQL-Umgebung mit der SQL Server-Integritätsüberprüfung-Lösung in Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
