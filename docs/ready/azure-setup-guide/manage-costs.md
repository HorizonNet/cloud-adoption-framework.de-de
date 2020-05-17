---
title: Verwalten von Kosten und Abrechnung für Azure-Ressourcen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit Rechnungen vertraut zu machen und zu erfahren, wie Sie Budgets und Zahlungen für Ihre Azure-Ressourcen einrichten.
author: dchimes
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: d1329175f341ca414cc79d2b2fa480ccdb294036
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223200"
---
<!-- cSpell:ignore dchimes -->

# <a name="manage-costs-and-billing-for-your-azure-resources"></a>Verwalten von Kosten und Abrechnung für Ihre Azure-Ressourcen

Die Kostenverwaltung ist der Prozess, bei dem Sie die Kosten Ihrer Geschäftstätigkeit effektiv planen und steuern. Kostenverwaltungsaufgaben werden in der Regel durch die Finanz-, Management- und App-Teams ausgeführt. Azure Cost Management kann Ihnen helfen, Ihre Planung unter Berücksichtigung der Kosten durchzuführen. Zudem können damit Kosten effektiv analysiert und Maßnahmen zum Optimieren der Cloudausgaben ergriffen werden.

Weitere Informationen zur Integration von Verwaltungsprozessen für die Cloudkosten in Ihrem Unternehmen finden Sie im Artikel des Cloud Adoption Framework zum [Nachverfolgen der Kosten in Geschäftseinheiten, Umgebungen oder Projekten](../azure-best-practices/track-costs.md).

## <a name="manage-your-costs-with-azure-cost-management"></a>Verwalten Ihrer Kosten mit Azure Cost Management

Azure Cost Management bietet verschiedene Funktionen für die Kostenprognose und -verwaltung:

- Die Funktion **Cloudkosten analysieren** unterstützt Sie dabei, Ihre Kosten zu untersuchen und zu analysieren. Sie können aggregierte Kosten für Ihr Konto oder kumulierte Kosten im Zeitverlauf anzeigen.
- Mit der Funktion **Mit Budgets überwachen** können Sie ein Budget erstellen und anschließend Warnungen konfigurieren, um eine Benachrichtigung zu erhalten, bevor das Budget überschritten wird.
- Mit der Funktion **Mit Empfehlungen optimieren** können Sie ungenutzte und nicht ausgelastete Ressourcen ermitteln und entsprechende Maßnahmen für eine optimale Ressourcennutzung ergreifen.
- Die Funktion **Rechnungen und Zahlungen verwalten** sorgt für Transparenz bei Ihren Cloudinvestitionen.

::: zone target="docs"

### <a name="predict-and-manage-costs"></a>Prognostizieren und Verwalten von Kosten

1. Wechseln Sie zu [Kostenverwaltung + Abrechnung](https://portal.azure.com/#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview).
1. Wählen Sie **Cost Management** aus.
1. Sehen Sie sich die Features zum Analysieren und Optimieren von Cloudkosten an.

### <a name="manage-invoices-and-payment-methods"></a>Verwalten von Rechnungen und Zahlungsmethoden

1. Wechseln Sie zu [Kostenverwaltung + Abrechnung](https://portal.azure.com/#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview).
1. Wählen Sie im linken Bereich im Abschnitt **Abrechnung** entweder **Rechnungen** oder **Zahlungsmethoden** aus.

## <a name="billing-and-subscription-support"></a>Support zu Abrechnung und Abonnement

Unser Abrechnungs- und Abonnementsupport steht Azure-Kunden täglich rund um die Uhr zur Verfügung. Sollten Sie Fragen zur Azure-Nutzung haben, erstellen Sie eine Supportanfrage.

### <a name="create-a-support-request"></a>Erstellen einer Supportanfrage

So übermitteln Sie eine neue Supportanfrage:

1. Navigieren Sie zu [Hilfe und Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).
1. Wählen Sie **Neue Supportanfrage** aus.

### <a name="view-a-support-request"></a>Anzeigen einer Supportanfrage

So zeigen Sie Ihre Supportanfragen und deren Status an:

1. Navigieren Sie zu [Hilfe und Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).
1. Wählen Sie **Alle Supportanfragen** aus.

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen finden Sie unter:

- [Dokumentation zur Abrechnungs- und Kostenverwaltung in Azure](https://docs.microsoft.com/azure/billing)
- [Cloud Adoption Framework: Nachverfolgen von Kosten für Geschäftseinheiten, Umgebungen oder Projekte](../azure-best-practices/track-costs.md)
- [Cloud Adoption Framework: Disziplin „Kostenverwaltung“](../../govern/cost-management/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Aktionen

**Prognostizieren und Verwalten von Kosten:**

1. Wechseln Sie zu **Kostenverwaltung + Abrechnung**.
1. Wählen Sie **Cost Management** aus.

**Verwalten von Rechnungen und Zahlungsmethoden:**

1. Wechseln Sie zu **Kostenverwaltung + Abrechnung**.
1. Wählen Sie im linken Bereich im Abschnitt **Abrechnung** entweder **Rechnungen** oder **Zahlungsmethoden** aus.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" ::: form-end

**Support zu Abrechnung und Abonnement:**

Unser Abrechnungs- und Abonnementsupport steht Azure-Kunden täglich rund um die Uhr zur Verfügung. Sollten Sie Fragen zur Azure-Nutzung haben, erstellen Sie eine Supportanfrage.

**Erstellen einer Supportanfrage:**

So übermitteln Sie eine neue Supportanfrage:

1. Navigieren Sie zu **Hilfe und Support**.
2. Wählen Sie **Neue Supportanfrage** aus.

**Anzeigen einer Supportanfrage:** So zeigen Sie Ihre Supportanfragen und deren Status an:

1. Navigieren Sie zu **Hilfe und Support**.
2. Wählen Sie **Alle Supportanfragen** aus.

::: form action="OpenBlade[#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview]" submitText="Go to Help + Support" ::: form-end

::: zone-end
