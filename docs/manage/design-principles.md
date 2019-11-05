---
title: Umsetzen von Entwurfsprinzipien und erweiterten Vorgängen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Umsetzen von Entwurfsprinzipien und erweiterten Vorgängen
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 8ea3610ed65ae45d924ca65ef26d249ed8343d0b
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979966"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Umsetzen von Entwurfsprinzipien und erweiterten Vorgängen

In den ersten drei Fachrichtungen der Cloudverwaltung wird eine Verwaltungsbaseline beschrieben. Als Mindestanforderung muss eine Verwaltungsbaseline eine Standardverpflichtung gegenüber den Fachbereichen vorsehen, um Betriebsunterbrechungen zu minimieren und die Wiederherstellung zu beschleunigen, sollte der Dienst unterbrochen werden. Die meisten Verwaltungsbaselines legen den Schwerpunkt auf die Aufrechterhaltung von „Bestand und Transparenz“, „betriebsbezogener Konformität“ sowie „Schutz und Wiederherstellung“.

Der Zweck einer Verwaltungsbaseline besteht darin, ein stimmiges Angebot zu schaffen, das für alle unterstützten Workloads ein Mindestmaß an geschäftlicher Verpflichtung vorsieht. Diese Baseline für allgemeine, wiederholbare Verwaltungsangebote ermöglicht dem Team, ein äußerst optimiertes Maß an Betriebsführung mit nur minimalen Abweichungen zu gewährleisten. Aber dieses Standardangebot stellt möglicherweise keine ausreichend große Verpflichtung gegenüber dem Unternehmen dar. 

Das Diagramm im nächsten Abschnitt veranschaulicht drei Möglichkeiten, über die Verwaltungsbaseline hinauszugehen.

Die Verwaltungsbaseline muss die Mindestverpflichtung erfüllen, die von 80 Prozent der Workloads mit der geringsten Kritikalität im Portfolio gefordert wird. Die Baseline darf nicht für unternehmenskritische Workloads gelten. Sie darf auch nicht für allgemeine, von Workloads gemeinsam genutzte Plattformen gelten. Diese Workloads erfordern einen Schwerpunkt auf Entwurfsprinzipien und erweiterten Vorgängen.

## <a name="advanced-operations-options"></a>Optionen für erweiterte Vorgänge

Es gibt drei Vorschläge zur besseren Einhaltung von geschäftlichen Verpflichtungen über die Verwaltungsbaseline hinaus, wie im folgenden Diagramm gezeigt:

![Erweiterte Vorgänge](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Optimierte Verwaltungsbaseline

Wie im Azure-Verwaltungsleitfaden beschrieben, werden im Rahmen einer Verwaltungsbaseline cloudnative Tools eingesetzt, um die Betriebszeit zu verbessern und die Wiederherstellungszeiten zu verkürzen. Die Verbesserungen sind signifikant, aber deutlich geringer als bei Workload- oder Plattformspezialisierungen. Der Vorteil einer optimierten Verwaltungsbaseline liegt in der ebenso signifikanten Verringerung von Kosten und Implementierungszeit.

## <a name="management-specialization"></a>Verwaltungsspezialisierung

Aspekte des Workload- und Plattformbetriebs könnten Änderungen an Entwurfs- und Architekturprinzipien erfordern. Diese Änderungen könnten Zeit in Anspruch nehmen und zu erhöhten Betriebskosten führen. Um die Anzahl der Workloads zu reduzieren, die solche Investitionen erfordern, kann eine optimierte Verwaltungsbaseline eine ausreichende Verbesserung zur Erfüllung von Verpflichtungen gegenüber den Fachbereichen bewirken.

Für Workloads, die eine höhere Investition zur Erfüllung von Verpflichtungen gegenüber den Fachbereichen rechtfertigen, ist die Betriebsspezialisierung entscheidend.

## <a name="areas-of-management-specialization"></a>Bereiche der Verwaltungsspezialisierung

Es gibt zwei Spezialisierungsbereiche:

- **Plattformspezialisierung**: Investieren in den laufenden Betrieb einer gemeinsam genutzten Plattform und Verteilen der Investition auf mehrere Workloads.
- **Workloadspezialisierung**: Investieren in den laufenden Betrieb einer bestimmten Workload, was in der Regel für unternehmenskritische Workloads reserviert ist.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Zentrale IT oder Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE)

Entscheidungen für eine Plattform- oder Workloadspezialisierung basieren auf der Kritizität und den Auswirkungen der einzelnen Workloads. Diese Entscheidungen sind jedoch auch ein Indiz größerer kultureller Entscheidungen zwischen den Organisationsmodellen einer zentralen IT und eines CCoE.

Eine Workloadspezialisierung löst häufig eine kulturelle Änderung aus. Sowohl die konventionelle IT als auch die zentrale IT bilden Prozesse aus, die eine skalierbare Unterstützung bieten können. Die Skalierung der Unterstützung ist für wiederholbare Dienste besser realisierbar, die in einer Verwaltungsbaseline, einer erweiterten Baseline oder sogar im Plattformbetrieb angesiedelt sind. Eine Workloadspezialisierung lässt sich häufig nicht skalieren. Dieser Mangel an Skalierbarkeit erschwert es einer zentralisierten IT-Organisation, die notwendige Unterstützung zu leisten, ohne die Grenzen der Skalierbarkeit der Organisation zu erreichen.

Alternativ lässt sich der auf einem Cloudkompetenzzentrum basierende Ansatz durch gezielte Delegierung von Zuständigkeiten und selektive Zentralisierung skalieren. Eine Workloadspezialisierung lässt sich meist besser auf den Ansatz der delegierten Zuständigkeit eines CCoE abstimmen. 

Die natürliche Abstimmung von Rollen in einem CCoE wird wie folgt dargestellt:
- Das Cloudplattformteam hilft beim Aufbau gemeinsamer Plattformen, die von mehreren Cloudeinführungsteams unterstützt werden. 
- Das Cloudautomatisierungsteam erweitert diese Plattformen zu bereitstellbaren Ressourcen in einem Dienstkatalog. 
- Die Cloudverwaltung stellt die Verwaltungsbaseline zentral bereit und unterstützt die Nutzung des Dienstkatalogs. 
- Allerdings trägt der Geschäftsbereich (in Form eines geschäftsbereichsorientierten DevOps- oder Cloudeinführungsteams) die Verantwortung für die täglichen auf Workloads, Pipelines oder Leistung bezogenen Abläufe.

Bei der Koordination von Verwaltungsbereichen können die Modelle der zentralen IT und des CCoE bei minimalem kulturellem Wandel im Allgemeinen auf der Plattformspezialisierung aufsetzen. Das Aufsetzen auf der Workloadspezialisierung könnte für Teams in einer zentralen IT-Organisation etwas komplexer sein.

## <a name="management-specialization-processes"></a>Verwaltungsspezialisierungsprozesse

Im Rahmen jeder Spezialisierung erfolgt der folgende vierstufige Prozess in einem disziplinierten, iterativen Ansatz. Dieser Ansatz erfordert eine Partnerschaft von Experten für Cloudeinführung, Cloudplattformen, Cloudautomatisierung und Cloudverwaltung, um eine funktionierende und überlegte Feedbackschleife zu schaffen.

- **Verbessern des Systementwurfs**: Verbesserung des Entwurfs gängiger Systeme (Plattformen) oder spezifischer Workloads, um Unterbrechungen effektiv zu minimieren.
- **Automatisieren der Korrektur**: Einige Verbesserungen sind nicht wirtschaftlich. In solchen Fällen könnte es sinnvoller sein, die Korrektur zu automatisieren und die Auswirkungen von Unterbrechungen zu reduzieren.
- **Skalieren der Lösung**: Bei verbessertem Systementwurf und automatisierter Korrektur können Sie diese Änderungen über den Dienstkatalog in der gesamten Umgebung skalieren.
- **Fortlaufende Verbesserung**: Sie können verschiedene Überwachungstools einsetzen, um inkrementelle Verbesserungen zu identifizieren, die im nächsten Durchlauf des Entwurfs, der Automatisierung und der Skalierung des Systems berücksichtigt werden.

### <a name="improve-system-design"></a>Verbessern des Systementwurfs

Das Verbessern des Systementwurfs ist der effektivste Ansatz zur Optimierung des Betriebs einer jeden gängigen Plattform. Verbesserungen des Systementwurfs können die Stabilität erhöhen und Betriebsunterbrechungen verringern. Der Entwurf einzelner Systeme wird für die Umgebungssicht nicht berücksichtigt, die das Framework für die Cloudeinführung (Cloud Adoption Framework) einnimmt. Als Ergänzung dieses Frameworks bietet das Azure Architecture Framework bewährte Methoden zur Verbesserung der Resilienz und des Entwurfs eines bestimmten Systems. Sie können diese Entwurfsverbesserungen für den Systementwurf einer Plattform oder einer bestimmten Workload übernehmen.

Das Azure Architecture Framework konzentriert sich auf die Verbesserung von fünf Grundpfeilern des Systementwurfs:

- **Skalierbarkeit:** Skalieren der allgemeinen Plattformressourcen, um eine gestiegene Last zu bewältigen.
- **Verfügbarkeit:** Verringern von Geschäftsunterbrechungen durch Verlängern der potenziellen Betriebszeit.
- **Resilienz:** Verkürzen von Wiederherstellungszeiten und so der Dauer von Unterbrechungen.
- **Sicherheit:** Schützen von Anwendungen und Daten vor externen Bedrohungen.
- **Verwaltung**: Spezifisch für diese allgemeinen Plattformressourcen erfolgende Betriebsprozesse.

Die meisten Betriebsunterbrechungen sind Folge einer Form von technischen Schulden oder einer unzulänglichen Architektur. Bei bestehenden Bereitstellungen können Verbesserungen des Systementwurfs als das Abtragen bestehender technischer Schulden angesehen werden. Bei Neubereitstellungen können Verbesserungen des Systementwurfs als das Vermeiden technischer Schulden verstanden werden. Der nächste Abschnitt, „Automatisierte Korrektur“, befasst sich mit Möglichkeiten, technische Schulden anzugehen, die nicht beseitigt werden können oder sollten.

Um den Systementwurf zu verbessern, erfahren Sie mehr über das [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars). Bei zunehmender Verbesserung Ihres Systementwurfs kehren Sie zu diesem Artikel zurück, um neue Möglichkeiten zur Verbesserung und Skalierung dieser Verbesserungen in Ihrer Umgebung zu finden.

### <a name="automated-remediation"></a>Automatisierte Korrektur

Einige technische Schulden können oder sollten nicht angegangen werden. Grund sind die Kosten ihrer Beseitigung. Sie könnte zwar geplant werden, aber eine lange Projektdauer mit sich bringen. Die Betriebsunterbrechung könnte keine signifikanten Auswirkungen auf den Geschäftsbetrieb haben, oder es geht vorrangig darum, eine schnelle Wiederherstellung zu erreichen, anstatt in Resilienz zu investieren.

Wenn die Beseitigung technischer Schulden nicht das gewünschte Ziel ist, ist die automatisierte Korrektur häufig der gewünschte nächste Schritt. Der gängigste Ansatz für die automatisierte Korrektur ist der Einsatz von Azure Automation und Azure Monitor zur Erkennung von Trends und Bereitstellung automatisierter Korrekturen.

Anleitungen zur automatisierten Korrektur finden Sie unter [Azure Automation und Warnungen](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Skalieren der Lösung mit einem Dienstkatalog

Der Eckpfeiler der Plattformspezialisierung und des Plattformbetriebs ist ein sorgfältig gepflegter Dienstkatalog. Auf diese Weise werden Verbesserungen bei Systementwurf und -korrektur in einer Umgebung skaliert. Das Cloudplattform- und Cloudautomatisierungsteam stimmen sich ab, um wiederholbare Lösungen für die gängigsten Plattformen in jeder Umgebung zu schaffen. Wenn diese Lösungen jedoch nicht konsistent umgesetzt werden, kann die Cloudverwaltung kaum mehr bieten als ein Baselineangebot.

Um die Akzeptanz zu maximieren und den Wartungsaufwand einer optimierten Plattform zu minimieren, sollte die Plattform in einen Dienstkatalog aufgenommen werden. Jede Anwendung im Katalog kann über den Dienstkatalog für den internen Einsatz oder als Marketplace-Angebot für externe Nutzer bereitgestellt werden.

Informationen zur Veröffentlichung in einem Dienstkatalog finden Sie in der Reihe zum [Veröffentlichen in einem Dienstkatalog](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Fortlaufende Verbesserung

Sowohl Plattformspezialisierung als auch Plattformbetrieb hängen von funktionierenden Feedbackschleifen zwischen dem Einführungs-, Plattform-, Automatisierungs- und Verwaltungsteam ab. Die Kopplung dieser Feedbackschleifen mit Daten ermöglicht es jedem Team, kluge Entscheidungen zu treffen. Damit beim Plattformbetrieb langfristige Geschäftsverpflichtungen erfüllt werden, ist es wichtig, für die zentralisierte Plattform spezifische Erkenntnisse zu nutzen. Da Container und SQL Server die beiden am häufigsten verwendeten zentral verwalteten Plattformen sind, sollten Sie mithilfe der folgenden Artikel mit der Datensammlung zur fortlaufenden Verbesserung beginnen: 

- [Containerleistung](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [PaaS-Datenbankleistung](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [IaaS-Datenbankleistung](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
