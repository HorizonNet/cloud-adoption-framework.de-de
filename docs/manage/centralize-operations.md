---
title: Zentralisieren von Verwaltungsvorgängen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Leitfaden zum Zentralisieren von Verwaltungsvorgängen
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b8e4e37ba9a771937b11f08f1abae45de2f818ab
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2019
ms.locfileid: "71806259"
---
# <a name="centralize-management-operations"></a>Zentralisieren von Verwaltungsvorgängen

In den meisten Organisationen werden durch die Verwendung eines einzelnen Azure Active Directory-Mandanten (Azure AD) für alle Benutzer die Verwaltungsvorgänge vereinfacht und die Wartungskosten gesenkt, da alle Verwaltungsaufgaben von bestimmten Benutzern, Benutzergruppen oder Dienstprinzipalen innerhalb des Mandanten durchgeführt werden können. Wir empfehlen Ihnen, nach Möglichkeit nur einen Azure AD-Mandanten für Ihre Organisation zu verwenden.

Allerdings gibt es auch Situationen, in denen eine Organisation mehrere Azure AD-Mandanten verwalten muss. Beispielsweise können für folgende Fälle mehrere Mandanten erforderlich sein:

- Vollständig unabhängige Niederlassungen.
- Unabhängige Tätigkeit in mehreren Regionen.
- Gesetzliche Anforderungen oder Complianceanforderungen.
- Akquisitionen anderer Organisationen (bisweilen zeitlich begrenzt, bis eine langfristige Strategie für die Mandantenkonsolidierung definiert ist).

Falls eine Architektur mit mehreren Mandanten benötigt wird, bietet [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) die Möglichkeit, Verwaltungsvorgänge zu zentralisieren und zu optimieren. Für Abonnements mehrerer Mandanten kann das Onboarding für die [delegierte Azure-Ressourcenverwaltung](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management) durchgeführt werden, damit die festgelegten Benutzer eines verwalteten Mandanten [mandantenübergreifende Verwaltungsfunktionen](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) zentral und skalierbar ausführen können.

Angenommen, Ihre Organisation verfügt über einen einzelnen Mandanten mit dem Namen *Mandant A*. Ihre Organisation beschafft dann zwei weitere Mandanten (*Mandant B* und *Mandant C*), die aus geschäftlichen Gründen separat verwaltet werden müssen.

Ihre Organisation möchte auf allen Mandanten die gleichen Richtliniendefinitionen, Sicherungsmethoden und Sicherheitsprozesse verwenden. Da Sie bereits über Benutzer verfügen (einschließlich Benutzergruppen und Dienstprinzipalen), die für die Durchführung dieser Aufgaben auf Mandant A zuständig sind, können Sie für alle Abonnements auf Mandant B und Mandant C das Onboarding durchführen, damit die gleichen Benutzer von Mandant A diese Aufgaben erledigen können. Mandant A wird dann zum Verwaltungsmandanten für Mandant B und Mandant C.

![Benutzer von Mandant A verwalten Ressourcen auf Mandant B und Mandant C](../_images/manage/enterprise-azure-lighthouse.jpg)

Weitere Informationen finden Sie unter [Azure Lighthouse in Unternehmensszenarien](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
