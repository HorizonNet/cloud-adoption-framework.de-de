---
title: Verwalten von in Azure Stack Hub ausgeführten Workloads
description: Erfahren Sie, wie Sie Workloads verwalten, die auf Azure Stack Hub ausgeführt werden.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 487bb83f8b9550253e856a92bbcc7eed6f5832a3
ms.sourcegitcommit: 76edf563a08ff7dc81c3fc2dc6c8972ab3b4c55b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2020
ms.locfileid: "88237031"
---
# <a name="manage-workloads-that-run-on-azure-stack-hub"></a>Verwalten von in Azure Stack Hub ausgeführten Workloads

Die Vorgänge und die Verwaltung von Hybridlösungen auf öffentlichen Plattformen und privaten Cloudplattformen sind komplex und können für Geschäftsvorgänge riskant sein. Da Azure Stack Hub die private Azure-Instanz Ihrer Organisation darstellt, die in Ihrem Rechenzentrum ausgeführt wird, wird das Risiko von Hybridvorgängen erheblich reduziert.

Wie in der [Verwaltungsmethodik](../../manage/index.md) des Cloud Adoption Framework erläutert, konzentrieren sich vorgeschlagene Operations Management-Aktivitäten auf die folgenden grundlegenden Aufgaben. Dieselben Aufgaben gelten auch für die Operations Management-Teams, die Azure Stack Hub unterstützen.

- **Bestand und Transparenz**: Erstellen Sie einen Ressourcenbestand in mehreren Clouds. Ermöglichen Sie Transparenz im Hinblick auf den Betriebszustand jeder einzelnen Ressource.
- **Betriebsbezogene Compliance**: Richten Sie Kontrollen und Prozesse ein, damit jeder Zustand ordnungsgemäß konfiguriert ist und in einer gut kontrollierten Umgebung ausgeführt wird.
- **Schutz und Wiederherstellung**: Stellen Sie sicher, dass alle verwalteten Ressourcen geschützt sind und mithilfe von Baseline-Verwaltungstools wiederhergestellt werden können.
- **Erweiterte Baseline-Optionen:** Evaluieren Sie allgemeine Ergänzungen zur Baseline, die ggf. zur Erfüllung von Geschäftsanforderungen geeignet sind.
- **Plattformbetrieb**: Erweitern Sie die Baseline zur Verwaltung um einen klar definierten Servicekatalog und zentral verwaltete Plattformen.
- **Workloadbetrieb**: Erweitern Sie die Baseline zur Verwaltung um einen Fokus auf unternehmenskritische Workloads.

## <a name="considerations-for-azure-stack-hub-operations-management"></a>Überlegungen zum Operations Management mit Azure Stack Hub

Einige der Standardaktivitäten der Vorgangsverwaltung erfordern andere technische Überlegungen. Diese Überlegungen werden in den folgenden Artikeln erläutert.

- [Self-Service-Support](https://azure.microsoft.com/blog/azure-stack-iaas-part-five/) für Ihre Kunden, einschließlich Startdiagnose, Screenshots, serielle Protokolle und Metriken
- [Gastverwaltung](https://azure.microsoft.com/blog/azure-stack-iaas-part-one/), einschließlich VM-Erweiterungen, der Möglichkeit zum Ausführen von benutzerdefiniertem Code, Softwareinventur und Änderungsnachverfolgung
- [Geschäftskontinuität](https://azure.microsoft.com/blog/azure-stack-iaas-part-four/) durch VM-Sicherungen und Notfallwiederherstellungsoptionen

## <a name="next-steps"></a>Nächste Schritte

Sobald Ihre Azure Stack Hub-Migration einen betriebsbereiten Zustand erreicht hat, können Sie die nächste Iteration von Migrationen mithilfe von Azure Stack Hub oder anderen Migrationsszenarios in der öffentlichen Azure-Cloud beginnen.

- [Planen der Azure Stack Hub-Migration](./plan.md)
- [Bereitschaft der Umgebung](./ready.md)
- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
