---
title: Zentralisieren von Verwaltungsvorgängen
description: Es wird beschrieben, wie Sie Verwaltungsvorgänge zentralisieren, indem Sie für alle Benutzer nur einen Azure Active Directory-Mandanten verwenden. Mit der zentralisierten Verwaltung werden Verwaltungsvorgänge vereinfacht und Wartungskosten reduziert.
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 03920802d2ee483154f789a6f353fd1642ccaf98
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094455"
---
# <a name="centralize-management-operations"></a>Zentralisieren von Verwaltungsvorgängen

In den meisten Organisationen werden durch Verwendung eines einzelnen Azure Active Directory-Mandanten (Azure AD) für alle Benutzer Verwaltungsvorgänge vereinfacht und Wartungskosten reduziert. Dies liegt daran, dass alle Verwaltungsaufgaben von bestimmten Benutzern, Benutzergruppen oder Dienstprinzipalen innerhalb dieses Mandanten ausgeführt werden können. 

Sie sollten nach Möglichkeit nur einen Azure AD-Mandanten für Ihre Organisation verwenden. Allerdings erfordern manche Situationen, dass eine Organisation aus folgenden Gründen mehrere Azure AD-Mandanten verwalten muss:

- Es gibt vollständig unabhängige Niederlassungen.
- Sie sind unabhängig in mehreren Regionen tätig.
- Bestimmte gesetzliche Anforderungen oder Complianceanforderungen gelten.
- Es gibt Akquisitionen anderer Organisationen (bisweilen zeitlich begrenzt, bis eine langfristige Strategie für die Mandantenkonsolidierung definiert ist).

Falls eine mehrinstanzenfähige Architektur benötigt wird, bietet [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) die Möglichkeit, Verwaltungsvorgänge zu zentralisieren und zu optimieren. Abonnements mehrerer Mandanten können für die [delegierte Azure-Ressourcenverwaltung](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management) integriert werden. Mit dieser Option können angegebene Benutzer im verwaltenden Mandanten [mandantenübergreifende Verwaltungsfunktionen](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) zentral und skalierbar ausführen.

Angenommen, Ihre Organisation verfügt über einen einzelnen Mandanten mit dem Namen *Mandant A*. Die Organisation beschafft dann zwei weitere Mandanten, *Mandant B* und *Mandant C*, die aus geschäftlichen Gründen separat verwaltet werden müssen.

Ihre Organisation möchte auf allen Mandanten die gleichen Richtliniendefinitionen, Sicherungsmethoden und Sicherheitsprozesse verwenden. Da Sie bereits über Benutzer verfügen (einschließlich Benutzergruppen und Dienstprinzipalen), die für die Durchführung dieser Aufgaben auf Mandant A zuständig sind, können Sie für alle Abonnements auf Mandant B und Mandant C das Onboarding durchführen, damit die gleichen Benutzer von Mandant A diese Aufgaben erledigen können. Mandant A wird dann zum Verwaltungsmandanten für Mandant B und Mandant C.

![Benutzer von Mandant A verwalten Ressourcen auf Mandant B und Mandant C](../_images/manage/enterprise-azure-lighthouse.jpg)

Weitere Informationen finden Sie unter [Azure Lighthouse in Unternehmensszenarien](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
