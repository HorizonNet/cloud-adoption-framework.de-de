---
title: Einführung in den Leitfaden zur Azure-Migration
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die Dienste Ihrer Organisation effizient zu Azure migrieren.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 4ef888e26089a2262fadeb93ec33ed063bcbf753
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80636504"
---
# <a name="azure-migration-guide-before-you-start"></a>Leitfaden zur Azure-Migration: Vorbereitung

Die [Migrationsmethodik des Frameworks für die Cloudeinführung (Cloud Adoption Framework)](../index.md) leitet Leser durch einen iterativen Prozess der Migration einer Workload oder einer kleinen Sammlung von Workloads pro Release. In jeder Iteration wird der Prozess der Bewertung, Migration, Optimierung und Höherstufung verfolgt, um sicherzustellen, dass die Workloads den Produktionsanforderungen entsprechen können. Mit diesem cloudunabhängigen Prozess kann eine Migration zu einem beliebigen Cloudanbieter durchgeführt werden.

Diese Anleitung veranschaulicht eine vereinfachte Version dieses Prozesses bei der Migration von der lokalen Umgebung zu **Azure**.

::: zone target="docs"

> [!TIP]
> Dieser Leitfaden steht im Azure-Portal als interaktive Umgebung zur Verfügung. Navigieren Sie im Azure-Portal zum [Azure Quickstart Center](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade), wählen Sie **Migrieren Ihrer Umgebung zu Azure** aus, und befolgen Sie dann die Schritt-für-Schritt-Anleitung.

::: zone-end

## <a name="migration-tools"></a>[Migrationstools](#tab/MigrationTools)

Diese Anleitung ist der empfohlene Weg für Ihre erste Migration zu Azure, da er Sie mit der Methodik und den bei der Migration zu Azure am häufigsten verwendeten cloudnativen Tools vertraut macht. Diese Tools werden auf den folgenden Seiten vorgestellt:

> [!div class="checklist"]
>
> - **Bewertung der technischen Eignung jeder Workload:** Überprüfen Sie die technische Bereitschaft und Eignung für die Migration.
> - **Migrieren Ihrer Dienste** Führen Sie die tatsächliche Migration durch, indem Sie lokale Ressourcen in Azure replizieren.
> - **Verwalten von Kosten und Abrechnung:** Informationen zu den Tools, die zum Steuern der Kosten in Azure erforderlich sind.
> - **Optimieren und Höherstufen:** Optimieren Sie das Gleichgewicht zwischen Kosten und Leistung, bevor Sie Ihre Workload in die Produktion bringen.
> - **Unterstützung** Erhalten Sie für die Aktivitäten während oder nach der Migration Hilfe oder Unterstützung.

Es wird davon ausgegangen, dass bereits eine Zielzone bereitgestellt wurde, und zwar gemäß den bewährten Methoden in der [Bereitschaftsmethodik des Frameworks für die Cloudeinführung](../../ready/index.md).

## <a name="when-to-use-this-guide"></a>[Verwendung dieses Leitfadens](#tab/WhenToUseThisGuide)

Während die in diesem Leitfaden behandelten Tools eine Vielzahl von Migrationsszenarien unterstützen, konzentriert sich dieser Leitfaden auf Maßnahmen mit begrenztem Umfang und _minimaler Komplexität_. Zur Ermittlung, ob dieser Migrationsleitfaden für Ihr Projekt geeignet ist, prüfen Sie, ob die folgenden Bedingungen für Ihre Situation gelten:

- Die Workloads für die anfängliche Migration sind nicht unternehmenskritisch und enthalten keine sensiblen Daten.
- Sie migrieren eine homogene Umgebung.
- Es müssen nur wenige Geschäftseinheiten ausgerichtet werden, um die Migration abzuschließen.
- Sie planen keine Automatisierung der gesamten Migration.
- Sie migrieren eine geringe Anzahl von Servern.
- Die Abhängigkeitszuordnung der zu migrierenden Komponenten ist einfach zu definieren.
- Ihre Branche verfügt über minimale gesetzliche Anforderungen, die für diese Migration relevant sind.

Wenn eine dieser Bedingungen nicht auf Ihre Situation zutrifft, sollten Sie stattdessen die [bewährten Methoden für die Cloudmigration](../azure-best-practices/index.md) berücksichtigen. Außerdem empfehlen wir Ihnen, Unterstützung von einem unserer Microsoft-Teams oder -Partner anzufordern, um komplexere Migrationen durchzuführen. Kunden, die mit Microsoft oder zertifizierten Partnern zusammenarbeiten, sind in diesen Szenarien erfolgreicher. Weitere Informationen zur Anforderung von Unterstützung finden Sie in diesem Leitfaden.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Weitere Informationen finden Sie unter

- [Bewährte Methoden für die Cloudmigration](../azure-best-practices/index.md)

::: zone-end
