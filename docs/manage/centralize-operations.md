---
title: Zentralisieren von Verwaltungsvorgängen
description: Es wird beschrieben, wie Sie Verwaltungsvorgänge zentralisieren, indem Sie für alle Benutzer nur einen Azure Active Directory-Mandanten verwenden. Mit der zentralisierten Verwaltung werden Verwaltungsvorgänge vereinfacht und Wartungskosten reduziert.
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 6814fb5ecfb91068979226ebf0163ea6d54ec3eb
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94880040"
---
# <a name="centralize-management-operations"></a>Zentralisieren von Verwaltungsvorgängen

In den meisten Organisationen werden durch Verwendung eines einzelnen Azure Active Directory-Mandanten (Azure AD) für alle Benutzer Verwaltungsvorgänge vereinfacht und Wartungskosten reduziert. Dies liegt daran, dass alle Verwaltungsaufgaben von bestimmten Benutzern, Benutzergruppen oder Dienstprinzipalen innerhalb dieses Mandanten ausgeführt werden können.

Sie sollten nach Möglichkeit nur einen Azure AD-Mandanten für Ihre Organisation verwenden. Allerdings erfordern manche Situationen, dass eine Organisation aus folgenden Gründen mehrere Azure AD-Mandanten verwalten muss:

- Es gibt vollständig unabhängige Niederlassungen.
- Sie sind unabhängig in mehreren Regionen tätig.
- Bestimmte gesetzliche Anforderungen oder Complianceanforderungen gelten.
- Es gibt Akquisitionen anderer Organisationen (bisweilen zeitlich begrenzt, bis eine langfristige Strategie für die Mandantenkonsolidierung definiert ist).

Falls eine mehrinstanzenfähige Architektur benötigt wird, bietet [Azure Lighthouse](/azure/lighthouse/overview) die Möglichkeit, Verwaltungsvorgänge zu zentralisieren und zu optimieren. Abonnements mehrerer Mandanten können für die [delegierte Azure-Ressourcenverwaltung](/azure/lighthouse/concepts/azure-delegated-resource-management) integriert werden. Mit dieser Option können angegebene Benutzer im verwaltenden Mandanten [mandantenübergreifende Verwaltungsfunktionen](/azure/lighthouse/concepts/cross-tenant-management-experience) zentral und skalierbar ausführen.

Angenommen, Ihre Organisation verfügt über einen einzelnen Mandanten, `Tenant A`. Die Organisation beschafft dann zwei weitere Mandanten, `Tenant B` und `Tenant C`, die aus geschäftlichen Gründen separat verwaltet werden müssen.

Ihre Organisation möchte auf allen Mandanten die gleichen Richtliniendefinitionen, Sicherungsmethoden und Sicherheitsprozesse verwenden. Da Sie bereits über Benutzer verfügen (einschließlich Benutzergruppen und Dienstprinzipalen), die für die Durchführung dieser Aufgaben auf `Tenant A` zuständig sind, können Sie für alle Abonnements auf `Tenant B` und `Tenant C` das Onboarding durchführen, damit die gleichen Benutzer von `Tenant A` diese Aufgaben erledigen können. `Tenant A` wird dann zum Verwaltungsmandanten für `Tenant B` und `Tenant C`.

![Benutzer von Mandant A verwalten Ressourcen auf Mandant B und Mandant C](../_images/manage/enterprise-azure-lighthouse.jpg)

Weitere Informationen finden Sie unter [Azure Lighthouse in Unternehmensszenarien](/azure/lighthouse/concepts/enterprise).
