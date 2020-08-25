---
title: Bewerten von Workloads für die Azure Stack Hub-Migration
description: Bewerten Sie Workloads für die Azure Stack Hub-Migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0278ef7006deec80580a6f457863049452c5069d
ms.sourcegitcommit: 76edf563a08ff7dc81c3fc2dc6c8972ab3b4c55b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2020
ms.locfileid: "88236997"
---
# <a name="assess-workloads-for-azure-stack-hub-migration"></a>Bewerten von Workloads für die Azure Stack Hub-Migration

In diesem Artikel wird davon ausgegangen, dass Sie sich für die [Integration von Azure Stack in Ihre Cloudstrategie](./index.md) entschieden sowie einen [Plan für die Azure Stack Hub-Migration](./plan.md) entwickelt haben und dass [Ihre Umgebung für die Migration bereit ist](./ready.md).

Bei der Rationalisierung der digitalen Ressourcen Ihrer Organisation im Rahmen der Planungsmethodik wurden alle Workloads ermittelt und inventarisiert, und es wurden erste Entscheidungen auf Grundlage von quantitativen Daten getroffen. Vor der Bereitstellung der einzelnen Workloads ist es wichtig, die Daten und Entscheidungen anhand von qualitativen Daten zu überprüfen.

## <a name="placement"></a>Platzierung

Der erste Datenpunkt, der berücksichtigt werden muss, ist die Platzierung. Wird die Workload zu Ihrer öffentlichen Cloud, Ihrer privaten Cloud oder zu einer anderen Cloudplattform migriert, etwa einer Sovereign Cloud oder der Azure-Umgebung eines Dienstanbieters?

Anhand der Informationen in den folgenden Abschnitten können Sie Ihre Entscheidungen zur Platzierung überprüfen. Die Informationen helfen auch dabei, Daten an die Oberfläche zu bringen, die während der Bereitstellung Ihrer Workloads von Nutzen sein werden.

## <a name="stakeholder-value"></a>Nutzen und Wert für die Beteiligten

Beurteilen Sie mit Beteiligten aus dem Geschäfts- und IT-Bereich, welchen Nutzen die Migration dieser Workload bietet:

- Geringeres Konfliktpotenzial: kurzfristiger Fokus, begrenzte langfristige Verwendbarkeit
- Höheres Konfliktpotenzial: langfristige Investitionen, einfachere Iteration und Fortsetzung der Modernisierung
- Ein Gleichgewicht zwischen beidem

## <a name="governance-risk-and-compliance"></a>Governance, Risiko und Compliance

Bewerten Sie die Auswirkungen von gesetzlichen Vorgaben sowie Compliance- und Datenschutzanforderungen:

- Welche Daten können in Azure gespeichert werden und welche müssen lokal bleiben?
- Wer kann die zugrunde liegende Plattform verwalten?
- Sind die Daten vom Speicherort abhängig?
- Gilt ein Ablaufdatum für das Speichern der Daten?

## <a name="success-metrics"></a>Erfolgsmetriken

Definieren Sie Erfolgsmetriken und Verfügbarkeitstoleranzen:

- Leistung
- Verfügbarkeit
- Resilienz
- Bereitstellungs- oder Migrationsansatz

## <a name="licensing"></a>Lizenzierung

Bewerten Sie die Auswirkungen von Lizenzierung und Support:

- Gibt es Einschränkungen hinsichtlich der Produktlizenzierung, die die Transformation begrenzen?
- Können die Anwendung oder das Dataset in der neuen Umgebung unterstützt werden?
- Sind Unterstützungserklärungen für Software von Drittanbietern erforderlich?

## <a name="operations-requirements"></a>Betriebsanforderungen

- Vermeiden Sie Doppelarbeit, und optimieren Sie Vereinbarungen zum Service Level (Service Level Agreement, SLA), indem Sie die Korrelation zwischen IT-verwalteten Clouddiensten und anwendungsspezifischen Diensten untersuchen.
- Prüfen Sie, welcher Grad an Automatisierung während der Bereitstellung und Migration von Anwendungen zum Orchestrieren der Bereitstellung von Diensten erforderlich ist.
- Berücksichtigen Sie zur Erfüllung Ihrer Betriebsanforderungen [Skalierbarkeits- und Verfügbarkeitsdienste](https://azure.microsoft.com/blog/azure-stack-iaas-part-six/) wie nutzungsbasierte Bezahlung, VM-Verfügbarkeitsgruppen, VM-Skalierungsgruppen und Netzwerkadapter sowie die Möglichkeit, VMs und Datenträger hinzuzufügen und ihre Größe zu ändern.

## <a name="monitoring"></a>Überwachung

- Überwachen Sie die Systemintegrität, den Betriebsstatus und die Leistung mit klar definierten Metriken, die die Grundlage der SLAs bilden, die Sie Ihren Endbenutzern bieten.
- Überprüfen Sie die Sicherheit und Konformität, und bewerten Sie, wie gut die Cloudumgebung die gesetzlichen Vorgaben und Complianceanforderungen der Anwendung erfüllt.
- Welche Prozesse werden für Sicherung/Wiederherstellung und Replikation/Failover verwendet?
- Finden Sie Datenschutzdienste für Infrastructure-as-a-Service-, Platform-as-a-Service- und Software-as-a-Service-Ressourcen.
- Integrieren Sie mehrere Anbieter, Technologien und Funktionen, um für eine umfassende Schutzstrategie zu sorgen.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
