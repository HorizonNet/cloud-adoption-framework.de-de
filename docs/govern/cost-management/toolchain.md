---
title: Cost Management-Tools in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Disziplin „Kostenverwaltung“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6f2e08a85df87f7973f19ebd83b71de0f2003189
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220480"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management-Tools in Azure

[Die Disziplin „Cost Management“ (Kostenverwaltung)](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Plänen für Cloudausgaben, zum Zuordnen von Cloudbudgets, zur Überwachung und Durchsetzung von Cloudbudgets, zum Erkennen kostspieliger Abweichungen und zum Anpassen des Cloudgovernanceplans, wenn die tatsächlichen Ausgaben falsch ausgerichtet sind.

Im Folgenden ist eine Liste der nativen Azure-Tools aufgeführt, die zur Ausreifung der Richtlinien und Prozesse beitragen können, die diese Disziplin unterstützen.

<!-- TODO: Content packs are deprecated. -->

| Tool | [Azure portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview)  | [Azure EA-Inhaltspaket](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
| Enterprise Agreement erforderlich?     | Nein         | Nein         | Ja         | Nein         |
| Budgetkontrolle     | Nein         | Ja         | Nein         | Ja         |
| Überwachen der Ausgaben für eine einzelne Ressource    | Ja         | Ja         | Ja         | Nein         |
| Überwachen der Ausgaben für mehrere Ressourcen    | Nein         | Ja        | Ja         | Nein         |
| Steuern der Ausgaben für eine einzelne Ressource     | Ja – manuelle Größenanpassung         | Ja         | Nein         | Ja         |
| Durchsetzen der Ausgaben für mehrere Ressourcen    | Nein         | Ja         | Nein         | Ja         |
| Erzwingen von Kostenmetadaten für Ressourcen    | Nein         | Nein         | Nein         | Ja         |
| Überwachen und Erkennen von Trends     | Ja          | Ja        | Ja         | Nein         |
| Erkennen von Anomalien in den Ausgaben     | Nein         | Ja        | Ja         | Nein        |
| Kommunizieren von Abweichungen     | Nein        | Ja        | Ja        | Nein        |
