---
title: Übersicht über die Verwaltung in Azure
description: Erfahren Sie mehr über das Framework für die Cloudeinführung für Azure mit diesen Informationen zu den grundlegenden Tools, die zum Verwalten von Azure-Produktionsumgebungen erforderlich sind.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 37d49948772ca0912dc574ccb299c050eae4aeb4
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341758"
---
# <a name="azure-management-guide-before-you-start"></a>Azure-Verwaltungsleitfaden: Vorbereitung


::: zone target="docs"


> [!NOTE]
> Dieser Leitfaden dient als Ausgangspunkt für Innovationsleitlinien im Cloud Adoption Framework. Er ist auch im Schnellstartcenter von Azure verfügbar. Einen Link zum Schnellstartcenter von Azure finden Sie im Tipp weiter unten in diesem Artikel.

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Vorbereitung

::: zone-end

Der Azure-Verwaltungsleitfaden dient Azure-Kunden als Hilfe beim Erstellen einer Baseline zur Verwaltung, um Einheitlichkeit für alle Ressourcen in Azure zu erzielen. Dieser Leitfaden beschreibt die für jede Azure-Produktionsumgebung erforderlichen grundlegenden Tools – insbesondere für Umgebungen, in denen vertrauliche Daten gespeichert werden. Weitere Informationen, bewährte Methoden und Überlegungen im Zusammenhang mit der Vorbereitung Ihrer Cloudumgebung finden Sie im [Abschnitt zur Bereitschaft des Frameworks für die Cloudeinführung](../index.md).

## <a name="scope-of-this-guide"></a>Geltungsbereich dieses Leitfadens

Dieser Leitfaden zeigt Ihnen, wie Sie Tools für eine Baseline zur Verwaltung einrichten. Außerdem werden Möglichkeiten zum Erweitern der Baseline oder zum Aufbauen von Resilienz über die Baseline hinaus aufgezeigt.

> [!div class="checklist"]
>
> - **Bestand und Transparenz:** Erstellen Sie einen Ressourcenbestand in mehreren Clouds. Ermöglichen Sie Transparenz im Hinblick auf den Betriebszustand jeder einzelnen Ressource.
> - **Betriebsbezogene Compliance:** Richten Sie Kontrollen und Prozesse ein, damit jeder Zustand ordnungsgemäß konfiguriert ist und in einer gut kontrollierten Umgebung ausgeführt wird.
> - **Schutz und Wiederherstellung:** Stellen Sie sicher, dass alle verwalteten Ressourcen geschützt sind und mithilfe von Baseline-Verwaltungstools wiederhergestellt werden können.
> - **Erweiterte Baseline-Optionen:** Evaluieren Sie allgemeine Ergänzungen zur Baseline, die ggf. zur Erfüllung von Geschäftsanforderungen geeignet sind.
> - **Plattformbetrieb:** Erweitern Sie die Baseline zur Verwaltung um einen klar definierten Servicekatalog und zentral verwaltete Plattformen.
> - **Workloadbetrieb:** Erweitern Sie die Baseline zur Verwaltung um einen Fokus auf unternehmenskritische Workloads.

## <a name="management-baseline"></a>Baseline zur Verwaltung

Eine Baseline zur Verwaltung umfasst den Mindestsatz an Tools und Prozessen, der auf jede Ressource einer Umgebung angewendet werden sollte. Mehrere zusätzliche Optionen können in die Baseline zur Verwaltung aufgenommen werden. Die nächsten Artikel enthalten Informationen zur schnelleren Einführung von Cloudverwaltungsfunktionen, da nicht alle verfügbaren Optionen beschrieben werden, sondern nur die benötigten Mindestoptionen.

::: zone target="docs"

> [!TIP]
> Dieser Leitfaden steht im Azure-Portal als interaktive Umgebung zur Verfügung. Navigieren Sie im Azure-Portal zum [Schnellstartcenter von Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade), und wählen Sie dann den **Azure-Verwaltungsleitfaden** aus. Befolgen Sie dann die Schrittanleitungen.

Der nächste Schritt ist [Bestand und Transparenz](./inventory.md).

::: zone-end

::: zone target="chromeless"

Dieser Leitfaden enthält die interaktiven Schritte, mit denen Sie Features nach ihrer Einführung testen können. Nutzen Sie die Brotkrümelnavigation, damit Sie zum Ausgangsort zurückfinden.

::: zone-end
