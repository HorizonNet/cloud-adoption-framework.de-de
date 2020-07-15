---
title: Häufig gestellte Fragen
description: Häufig gestellte Fragen.
author: alexbuckgit
ms.author: abuck
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 049a2849e2569caaf4940ba98bf67e6f3056be61
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86235142"
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
