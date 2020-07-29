---
title: Verwalten von Workloads, die auf Azure Stack Hub ausgeführt werden
description: Erfahren Sie, wie Sie Workloads verwalten, die auf Azure Stack Hub ausgeführt werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 58d3f1eee0ea3514ccf3b9ee99f30fb7bcef978e
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452765"
---
# <a name="manage-workloads-running-on-azure-stack-hub"></a>Verwalten von Workloads, die auf Azure Stack Hub ausgeführt werden

Die Vorgänge und die Verwaltung von Hybridlösungen auf öffentlichen Plattformen und privaten Cloudplattformen sind komplex und können für Geschäftsvorgänge riskant sein. Da Azure Stack Hub eine eigene private Instanz von Azure ist, die in Ihrem Rechenzentrum ausgeführt wird, wird das Risiko von Hybridvorgängen erheblich reduziert.

Wie in der [Verwaltungsmethodik](../../manage/index.md) des Cloud Adoption Framework erläutert, konzentrieren sich vorgeschlagene Verwaltungsaktivitäten für Vorgänge auf die folgenden grundlegenden Aufgaben. Die gleichen Aufgaben gelten auch für die Operations Management-Teams, die Azure Stack Hub unterstützen.

- **Bestand und Transparenz:** Erstellen Sie einen Ressourcenbestand in mehreren Clouds. Ermöglichen Sie Transparenz im Hinblick auf den Betriebszustand jeder einzelnen Ressource.
- **Betriebsbezogene Compliance:** Richten Sie Kontrollen und Prozesse ein, damit jeder Zustand ordnungsgemäß konfiguriert ist und in einer gut kontrollierten Umgebung ausgeführt wird.
- **Schutz und Wiederherstellung:** Stellen Sie sicher, dass alle verwalteten Ressourcen geschützt sind und mithilfe von Baseline-Verwaltungstools wiederhergestellt werden können.
- **Erweiterte Baseline-Optionen:** Evaluieren Sie allgemeine Ergänzungen zur Baseline, die ggf. zur Erfüllung von Geschäftsanforderungen geeignet sind.
- **Plattformbetrieb:** Erweitern Sie die Baseline zur Verwaltung um einen klar definierten Servicekatalog und zentral verwaltete Plattformen.
- **Workloadbetrieb:** Erweitern Sie die Baseline zur Verwaltung um einen Fokus auf unternehmenskritische Workloads.

## <a name="azure-stack-hub-operations-management-considerations"></a>Überlegungen zur Vorgangsverwaltung von Azure Stack Hub

Einige der Standardaktivitäten der Vorgangsverwaltung erfordern andere technische Überlegungen. Diese Überlegungen werden in den folgenden Artikeln erläutert.

- [Self-Service-Support](https://azure.microsoft.com/blog/azure-stack-iaas-part-five/) für Ihre Kunden, einschließlich Startdiagnose, Screenshots, serielle Protokolle und Metriken
- [Gastverwaltung](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/), einschließlich VM-Erweiterungen, der Möglichkeit zum Ausführen von benutzerdefiniertem Code, Softwareinventur und Änderungsnachverfolgung
- [Geschäftskontinuität](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/) durch VM-Sicherungen und Notfallwiederherstellungsoptionen

## <a name="next-step-integrate-this-strategy-into-your-cloud-adoption-journey"></a>Nächster Schritt: Integrieren dieser Strategie in Ihre Cloudeinführungsjourney

Nachdem Ihre Azure Stack Hub-Migration einen Betriebszustand erreicht hat, können Sie mit der nächsten Iteration von Migrationen beginnen, indem Sie Azure Stack Hub oder andere Migrationsszenarios in der öffentlichen Cloud von Azure verwenden.

- [Planen von Azure Stack Hub-Migrationen](./plan.md)
- [Bereitschaft der Umgebung](./ready.md)
- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
