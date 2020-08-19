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
ms.openlocfilehash: 1de9c21e4d3201ddadae50c85557b4317190b693
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88573699"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management-Tools in Azure

Die [Disziplin „Cost Management“ (Kostenverwaltung)](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Plänen für Cloudausgaben, zum Zuordnen von Cloudbudgets, zur Überwachung und Durchsetzung von Cloudbudgets, zum Erkennen kostspieliger Abweichungen und zum Anpassen des Cloudgovernanceplans, wenn die tatsächlichen Ausgaben falsch ausgerichtet sind.

Im Folgenden ist eine Liste der nativen Azure-Tools aufgeführt, die zur Ausreifung der Richtlinien und Prozesse beitragen können, die diese Disziplin unterstützen.

<!-- TODO: Content packs are deprecated. -->

| Tool | [Azure portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](/azure/cost-management-billing/cost-management-billing-overview)  | [Power BI Desktop-Connector](/power-bi/connect-data/desktop-connect-azure-cost-management) | [Azure Policy](/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
| Budgetkontrolle     | Nein         | Ja         | Nein         | Ja         |
| Überwachen der Ausgaben für eine einzelne Ressource    | Ja         | Ja         | Ja         | Nein         |
| Überwachen der Ausgaben für mehrere Ressourcen    | Nein         | Ja        | Ja         | Nein         |
| Steuern der Ausgaben für eine einzelne Ressource     | Ja, manuelle Größenanpassung         | Ja         | Nein         | Ja         |
| Durchsetzen der Ausgaben für mehrere Ressourcen    | Nein         | Ja         | Nein         | Ja         |
| Erzwingen von Kostenmetadaten für Ressourcen    | Nein         | Nein         | Nein         | Ja         |
| Überwachen und Erkennen von Trends     | Ja          | Ja        | Ja         | Nein         |
| Erkennen von Anomalien in den Ausgaben     | Nein         | Ja        | Ja         | Nein        |
| Kommunizieren von Abweichungen     | Nein        | Ja        | Ja        | Nein        |
