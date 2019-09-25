---
title: Cost Management-Tools in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cost Management-Tools in Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3b301f8dfcc50539f4325901cd32553368a0da55
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222640"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management-Tools in Azure

[Cost Management](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Plänen für Cloudausgaben, zum Zuordnen von Cloudbudgets, zur Überwachung und Durchsetzung von Cloudbudgets, zum Erkennen kostspieliger Abweichungen und zum Anpassen des Cloudgovernanceplans, wenn die tatsächlichen Ausgaben falsch ausgerichtet sind.

Im Folgenden ist eine Liste der nativen Azure-Tools aufgeführt, die zur Ausreifung der Richtlinien und Prozesse beitragen können, die diese Governancedisziplin unterstützen.

| Tool | [Azure-Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Azure EA-Inhaltspaket](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Enterprise Agreement erforderlich?     | Nein         | Nein         | Ja         | Nein         |
|Budgetkontrolle     | Nein         | Ja         | Nein         | Ja         |
|Überwachen der Ausgaben für eine einzelne Ressource    | Ja         | Ja         | Ja         | Nein         |
|Überwachen der Ausgaben für mehrere Ressourcen    | Nein         | Ja        | Ja         | Nein         |
|Steuern der Ausgaben für eine einzelne Ressource     | Ja – manuelle Größenanpassung         | Ja         | Nein         | Ja         |
|Durchsetzen der Ausgaben für mehrere Ressourcen    | Nein         | Ja         | Nein         | Ja         |
|Erzwingen von Kostenmetadaten für Ressourcen    | Nein         | Nein         | Nein         | Ja         |
|Überwachen und Erkennen von Trends     | Ja          | Ja        | Ja         | Nein         |
|Erkennen von Anomalien in den Ausgaben     | Nein         | Ja        | Ja         | Nein        |
|Kommunizieren von Abweichungen     | Nein        | Ja        | Ja        | Nein        |
