---
title: Häufig gestellte Fragen
description: Häufig gestellte Fragen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: befa3a167d38dc49120255b7ba7f5a992be8d888
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076914"
---
# <a name="faq"></a>Häufig gestellte Fragen

Auf dieser Seite finden sich häufig gestellte Fragen zum Entwerfen auf Unternehmensebene und zur Implementierung bei Contoso.

## <a name="enterprise-scale-design"></a>Entwerfen auf Unternehmensebene

### <a name="where-a-landing-zone-maps-in-azure-in-the-context-of-enterprise-scale"></a>Zuordnung einer Zielzone in Azure im Kontext der Unternehmensebene

Aus Sicht der Unternehmensebene ist ein Abonnement die Zielzone in Azure.

## <a name="contoso-implementation"></a>Implementierung bei Contoso

### <a name="why-enterprise-scale-azure-resource-manager-templates-require-permissions-at-the-tenant-root--scope"></a>Gründe, aus denen Azure Resource Manager-Vorlagen auf Unternehmensebene Berechtigungen im Mandantenstamm/-gültigkeitsbereich benötigen

Die Erstellung von Verwaltungsgruppen erfolgt über eine `put`-Anwendungsprogrammierschnittstelle auf Mandantenebene. Die Voraussetzung für die Verwendung von Beispielvorlagen ist das Erteilen von Berechtigungen im Stammbereich.

### <a name="why-sync-a-fork-with-the-upstream-repo"></a>Gründe für das Synchronisieren einer Verzweigung mit dem Upstream-Repository

Auf diese Weise können Sie steuern, wie oft Sie Patches für Fehler ausführen möchten. Dies ist eine vorläufige Lösung, solange wir die Pipeline-Codebasis als GitHub Actions verpacken. Daher ist dieser Schritt in Zukunft nicht mehr erforderlich.
