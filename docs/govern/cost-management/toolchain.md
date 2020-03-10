---
title: Cost Management-Tools in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Governancedisziplin „Kostenverwaltung“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 70014352d4b7f64f5c73a0fda96ef453f1a77176
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77708783"
---
# <a name="cost-management-tools-in-azure"></a>Cost Management-Tools in Azure

[Cost Management](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Plänen für Cloudausgaben, zum Zuordnen von Cloudbudgets, zur Überwachung und Durchsetzung von Cloudbudgets, zum Erkennen kostspieliger Abweichungen und zum Anpassen des Cloudgovernanceplans, wenn die tatsächlichen Ausgaben falsch ausgerichtet sind.

Im Folgenden ist eine Liste der nativen Azure-Tools aufgeführt, die zur Ausreifung der Richtlinien und Prozesse beitragen können, die diese Governancedisziplin unterstützen.

| Tool | [Azure portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Azure EA-Inhaltspaket](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
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
