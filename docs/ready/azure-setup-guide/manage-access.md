---
title: Verwalten des Zugriffs auf Ihre Azure-Umgebung
description: Hier erfahren Sie, wie Sie mit der rollenbasierten Zugriffssteuerung (RBAC) die Steuerung des Zugriffs auf Ihre Azure-Umgebung einrichten.
author: LijuKodicheraJayadevan
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: efefa348324ab0c9dff86b5d19f7c3f11d9d437d
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223268"
---
<!-- cSpell:ignore LijuKodicheraJayadevan -->

# <a name="manage-access-to-your-azure-environment-with-role-based-access-control"></a>Verwalten des Zugriffs auf Ihre Azure-Umgebung per rollenbasierter Zugriffssteuerung

Die Verwaltung der Personen, die auf Ihre Azure-Ressourcen und -Abonnements zugreifen können, ist ein wichtiger Bestandteil Ihrer Azure-Governancestrategie, und die Zuweisung gruppenbasierter Zugriffsrechte und -privilegien ist eine geeignete Vorgehensweise. Der Umgang mit Gruppen anstelle von einzelnen Benutzern vereinfacht die Wartung von Zugriffsrichtlinien, bietet eine einheitliche teamübergreifende Zugriffsverwaltung und reduziert Konfigurationsfehler. Die rollenbasierte Zugriffssteuerung in Azure (Role-Based Access Control, RBAC) ist das Hauptverfahren zum Verwalten des Zugriffs in Azure.

RBAC bietet eine ausführliche Zugriffsverwaltung für Ressourcen in Azure. Sie können verwalten, welche Benutzer auf welche Azure-Ressourcen zugreifen können, welche Möglichkeiten diese mit den Ressourcen haben und für welche Bereiche Zugriff besteht.

Bei der Planung Ihrer Strategie für die Zugriffssteuerung erteilen Sie Benutzern die geringsten zum Ausführen ihrer Aufgaben erforderlichen Rechte. Die folgende Abbildung zeigt ein vorgeschlagenes Muster für die Zuweisung von RBAC.

![Diagramm mit RBAC-Rollen](./media/manage-access/role-examples.png)

Wenn Sie Ihre Vorgehensweise für die Zugriffssteuerung planen, empfehlen wir die Zusammenarbeit mit Personen in Ihrer Organisation, die über Rollen für die folgenden Bereiche verfügen: „Sicherheit und Konformität“, „IT-Verwaltung“ und „Enterprise-Architekt“.

Das Framework für die Cloudeinführung (Cloud Adoption Framework) bietet zusätzliche Anleitungen zur Verwendung der [ rollenbasierter Zugriffssteuerung](../considerations/roles.md) im Rahmen Ihrer Cloudeinführungsbemühungen.

::: zone target="chromeless"

## <a name="actions"></a>Aktionen

**Gewähren von Zugriff auf Ressourcengruppen:**

So gewähren Sie einem Benutzer Zugriff auf eine Ressourcengruppe:

1. Navigieren Sie zu **Ressourcengruppen**.
1. Wählen Sie eine Ressourcengruppe aus.
1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.
1. Wählen Sie **+Hinzufügen** > **Rollenzuweisung hinzufügen** aus.
1. Wählen Sie eine Rolle aus, und weisen Sie anschließend einem Benutzer, einer Gruppe oder einem Dienstprinzipal Zugriff zu.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups]" submitText="Go to resource groups" ::: form-end

**Gewähren des Zugriffs auf Abonnements:**

So gewähren Sie einem Benutzer Zugriff auf ein Abonnement:

1. Navigieren Sie zu **Abonnements**.
1. Wählen Sie ein Abonnement aus.
1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.
1. Wählen Sie **+Hinzufügen** > **Rollenzuweisung hinzufügen** aus.
1. Wählen Sie eine Rolle aus, und weisen Sie anschließend einem Benutzer, einer Gruppe oder einem Dienstprinzipal Zugriff zu.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to subscriptions" ::: form-end

::: zone-end

::: zone target="docs"

## <a name="grant-resource-group-access"></a>Gewähren von Zugriff auf Ressourcengruppen

So gewähren Sie einem Benutzer Zugriff auf eine Ressourcengruppe:

1. Navigieren Sie zu [Ressourcengruppen](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups).
1. Wählen Sie eine Ressourcengruppe aus.
1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.
1. Wählen Sie **+Hinzufügen** > **Rollenzuweisung hinzufügen** aus.
1. Wählen Sie eine Rolle aus, und weisen Sie anschließend einem Benutzer, einer Gruppe oder einem Dienstprinzipal Zugriff zu.

## <a name="grant-subscription-access"></a>Gewähren des Zugriffs auf Abonnements

So gewähren Sie einem Benutzer Zugriff auf ein Abonnement:

1. Navigieren Sie zu [Abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Wählen Sie ein Abonnement aus.
1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.
1. Wählen Sie **+Hinzufügen** > **Rollenzuweisung hinzufügen** aus.
1. Wählen Sie eine Rolle aus, und weisen Sie anschließend einem Benutzer, einer Gruppe oder einem Dienstprinzipal Zugriff zu.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Was ist die rollenbasierte Zugriffssteuerung (RBAC)?](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Cloud Adoption Framework: Verwenden von rollenbasierter Zugriffssteuerung](../considerations/roles.md)

::: zone-end
