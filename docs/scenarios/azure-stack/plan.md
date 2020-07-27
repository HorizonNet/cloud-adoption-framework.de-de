---
title: Planen der Azure Stack Hub-Migration
description: Planen der Azure Stack Hub-Migration
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: fd756ec02305c2bdc9a5c6d106f6b5b4c170c60c
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452752"
---
# <a name="plan-for-azure-stack-hub-migration"></a>Planen der Azure Stack Hub-Migration

In diesem Artikel wird davon ausgegangen, dass Sie sich mit der [Integration von Azure Stack in Ihre Cloudstrategie](./index.md) auseinandergesetzt haben und dass Ihre Journey den Beispielen in diesem Artikel entspricht.

Vor dem eigentlichen Einstieg in die Migration ist es wichtig, sinnvolle Erwartungen an Azure und Azure Stack Hub festzulegen. Dies hilft dabei, Fehler oder Rückschläge zu einem späteren Zeitpunkt in einem Projekt zu vermeiden. Der Schlüssel zu einer erfolgreichen Implementierung ist ein gutes Verständnis davon, wann Azure und wann Azure Stack Hubs eingesetzt werden sollte.

## <a name="digital-estate-alignment"></a>Anpassen der digitalen Ressourcen

Dies beginnt mit einigen einfachen Fragen zum Abschluss der [Rationalisierung Ihrer digitalen Ressourcen](../../digital-estate/index.md).

- Welche Gründe bestehen für die lokale Verwaltung von Anwendungen und Daten, z. B. gesetzliche Anforderungen, Data Gravity oder Complianceanforderungen?
- Welche spezifischen gesetzlichen oder Complianceanforderungen haben Auswirkungen auf die Entscheidung, im Rechenzentrum zu bleiben?
- Wie wirkt sich der Datenschutz auf die Datenmigration aus?
- Ist die Migration als Modernisierungsjourney definiert?
- Wenn dies der Fall ist: Haben Sie die nächsten Schritte und die Ziele nach der Migration definiert?
- Welche Anforderungen gelten für SLA, RPO, RTO und Verfügbarkeit?

Diese Informationen können für Entscheidungen zum Wert von Azure gegenüber Azure Stack Hub für einige Workloads herangezogen werden.

## <a name="assessment-best-practices"></a>Bewährte Methoden für die Bewertung

Die bewährte Methode bei der [Bewertung einer digitalen Ressource mit Azure Migrate](../../plan/contoso-migration-assessment.md) kann die Bewertung und Einordnung Ihrer digitalen Workloads und Ressourcen beschleunigen. Diese bewährte Methode bietet Erkenntnisse zu Ihrem gesamten IT-Portfolio. Außerdem hilft sie beim Identifizieren von technischen Anforderungen für Kapazität, Skalierung und Konfiguration, die Ihre Migration beeinflussen können.

Mit den richtigen Bewertungsdaten kann das Team bei der Auswertung von Optionen für Plattformen der öffentlichen oder privaten Cloud in Azure sinnvollere Entscheidungen treffen und klarere Prioritäten festlegen.

## <a name="planning-best-practices"></a>Bewährte Methoden bei der Planung

Die folgenden Ressourcen tragen zum Verständnis der Unterschiede zwischen Azure und Azure Stack Hub bei:

- [Azure Stack: Übersicht und Roadmap](https://azure.microsoft.com/resources/videos/ignite-2018-azure-stack-overview-and-roadmap/)
- [Azure Stack-Kapazitätsplanung](https://docs.microsoft.com/azure/azure-stack/capacity-planning)
- [Azure Stack Hub-Rechenzentrumsintegration: exemplarische Vorgehensweise](https://docs.microsoft.com/azure-stack/operator/azure-stack-customer-journey)
- [Features von Azure Stack-VMs](https://docs.microsoft.com/azure-stack/user/azure-stack-vm-considerations?view=azs-1910)

Nachdem Sie wissen, welche Plattformen für die einzelnen Workloads an besten geeignet sind, können Sie diese Entscheidungen in einen [Cloudeinführungsplan](../../plan/template.md) integrieren, um Migrationsvorgänge in öffentliche und private Clouds als einen ausgerichteten Vorgang zu verwalten.

## <a name="next-step-prepare-your-environment-for-azure-stack-hub-migrations"></a>Nächster Schritt: Vorbereiten der Umgebung für Azure Stack Hub-Migrationsvorgänge

In den folgenden Artikeln finden Sie Informationen zu bestimmten Aufgaben während der Cloudeinführungsjourney. Der erste Artikel zur [Bereitschaft der Umgebung](./ready.md) wird als nächster Schritt empfohlen.

- [Bereitschaft der Umgebung](./ready.md)
- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
