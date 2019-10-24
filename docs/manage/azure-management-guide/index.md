---
title: 'Azure-Verwaltungsleitfaden: Vorbereitung'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hier erfahren Sie, wie Sie Ihre Azure-Vorgänge mit einer Schritt-für-Schritt-Anleitung verwalten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 58a01e02abad2de68fac9a94d2a2aa3ad22d32a1
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769141"
---
::: zone target="docs"

# <a name="azure-management-guide-before-you-start"></a>Azure-Verwaltungsleitfaden: Vorbereitung

> [!NOTE]
> Dieser Leitfaden dient als Ausgangspunkt für Innovationsleitlinien im Cloud Adoption Framework. Er ist auch im Azure Quickstart Center verfügbar. Einen Link zum Azure Quickstart Center finden Sie im Tipp weiter unten in diesem Artikel.

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Vorbereitung

::: zone-end

Der Azure-Verwaltungsleitfaden unterstützt aktive Azure-Kunden bei der Erstellung einer Baseline zur Verwaltung, um die Ressourcenkonsistenz in Azure zu gewährleisten. Dieser Leitfaden beschreibt die für jede Azure-Produktionsumgebung erforderlichen grundlegenden Tools – insbesondere für Umgebungen, in denen vertrauliche Daten gespeichert werden. Weitere Informationen, bewährte Methoden und Überlegungen im Zusammenhang mit der Vorbereitung Ihrer Cloudumgebung finden Sie im [Abschnitt zur Bereitschaft des Frameworks für die Cloudeinführung](../index.md).

## <a name="scope-of-this-guide"></a>Geltungsbereich dieses Leitfadens

Dieser Leitfaden zeigt Ihnen, wie Sie Tools für eine Baseline zur Verwaltung einrichten. Außerdem werden Möglichkeiten zum Erweitern der Baseline oder zum Aufbauen von Resilienz über die Baseline hinaus aufgezeigt.

> [!div class="checklist"]
>
> - **Bestand und Transparenz:** Erstellen Sie einen Ressourcenbestand in mehreren Clouds. Ermöglichen Sie Transparenz im Hinblick auf den Betriebszustand jeder einzelnen Ressource.
> - **Betriebsbezogene Compliance:** Richten Sie Kontrollen und Prozesse ein, damit jeder Zustand ordnungsgemäß konfiguriert ist und in einer gut kontrollierten Umgebung ausgeführt wird.
> - **Schutz und Wiederherstellung:** Stellen Sie sicher, dass alle verwalteten Ressourcen geschützt sind und mithilfe von Baseline-Verwaltungstools wiederhergestellt werden können.
> - **Erweiterte Baseline-Optionen:** Bewerten Sie allgemeine Ergänzungen zur Baseline, die den Geschäftsanforderungen entsprechen können.
> - **Plattformbetrieb:** Erweitern Sie die Baseline zur Verwaltung um einen klar definierten Servicekatalog und zentral verwaltete Plattformen.
> - **Workloadbetrieb:** Erweitern Sie die Baseline zur Verwaltung um einen Fokus auf unternehmenskritische Workloads.

## <a name="management-baseline"></a>Baseline zur Verwaltung

Eine Baseline zur Verwaltung ist der Mindestsatz an Tools und Prozessen, der auf jede Ressource in der Umgebung angewendet werden sollte. Mehrere zusätzliche Optionen können in die Baseline zur Verwaltung aufgenommen werden. Die nächsten Artikel beschleunigen Cloudverwaltungsfunktionen, indem sie sich auf die notwendigen Mindestoptionen anstelle aller verfügbaren Optionen konzentrieren.

::: zone target="docs"

> [!TIP]
> Dieser Leitfaden steht im Azure-Portal als interaktive Umgebung zur Verfügung. Navigieren Sie im Azure-Portal zum [Azure Quickstart Center](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade), und wählen Sie den **Azure-Verwaltungsleitfaden** aus. Befolgen Sie dann die Schrittanleitungen.

Nächste Schritte: [Bestand und Transparenz](./inventory.md)

::: zone-end

::: zone target="chromeless"

Dieser Leitfaden enthält die interaktiven Schritte, mit denen Sie Features nach ihrer Einführung testen können. Nutzen Sie die Brotkrümelnavigation, damit Sie zum Ausgangsort zurückfinden.

::: zone-end
