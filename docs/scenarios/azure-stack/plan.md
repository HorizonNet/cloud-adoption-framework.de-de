---
title: Planen Ihrer Azure Stack Hub-Migration
description: Planen Sie Ihre Azure Stack Hub-Migration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 64e1ae5cbe6f6ed31575614551f1dafc3275f1a0
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572662"
---
# <a name="plan-your-azure-stack-hub-migration"></a>Planen Ihrer Azure Stack Hub-Migration

In diesem Artikel wird davon ausgegangen, dass Sie sich mit der [Integration von Azure Stack in Ihre Cloudstrategie](./index.md) auseinandergesetzt haben und dass Ihre Journey den Beispielen in diesem Artikel entspricht.

Vor dem eigentlichen Einstieg in die Migration Ihrer Organisation ist es wichtig, sinnvolle Erwartungen an Azure und Azure Stack Hub festzulegen. Dadurch können Fehler oder Rückschläge im späteren Verlauf des Projekts vermieden werden. Der Schlüssel zu einer erfolgreichen Implementierung ist ein gutes Verständnis davon, wann Azure und wann Azure Stack Hubs eingesetzt werden sollte.

## <a name="digital-estate-alignment"></a>Anpassen der digitalen Ressourcen

Die Ausrichtung der digitalen Ressourcen Ihrer Organisation beginnt mit ein paar einfachen Fragen, die Sie stellen müssen, wenn Sie Ihre [Rationalisierung der digitalen Ressourcen abgeschlossen haben](../../digital-estate/index.md).

- Welche Gründe bestehen für die lokale Verwaltung von Anwendungen und Daten, z. B. gesetzliche Anforderungen, Data Gravity oder Complianceanforderungen?
- Welche spezifischen gesetzlichen oder Complianceanforderungen haben Auswirkungen auf die Entscheidung, im Rechenzentrum zu bleiben?
- Wie wirkt sich der Datenschutz auf die Datenmigration aus?
- Ist die Migration als Modernisierungsjourney definiert?
- Wenn dies der Fall ist: Haben Sie die nächsten Schritte und die Ziele nach der Migration definiert?
- Was sind die Anforderungen zur Vereinbarung zum Servicelevel, zum Recovery Point Objective, zum Recovery Time Objective und zur Verfügbarkeit?

Ihre Antworten auf diese Fragen können für Entscheidungen zum Wert von Azure gegenüber Azure Stack Hub für einige Workloads herangezogen werden.

## <a name="assessment-best-practices"></a>Bewährte Methoden für die Bewertung

Durch die Anwendung der bewährten Methode bei der [Bewertung einer digitalen Ressource mit Azure Migrate](../../plan/contoso-migration-assessment.md) können Sie die Bewertung und Einordnung Ihrer digitalen Workloads und Ressourcen beschleunigen. Diese bewährte Methode bietet Erkenntnisse zu Ihrem gesamten IT-Portfolio. Außerdem hilft sie beim Identifizieren von technischen Anforderungen für Kapazität, Skalierung und Konfiguration, die Ihre Migration beeinflussen können.

Mit den richtigen Bewertungsdaten kann Ihr Cloudeinführungsteam bei der Auswertung von Optionen für Plattformen der öffentlichen oder privaten Cloud in Azure sinnvollere Entscheidungen treffen und klarere Prioritäten festlegen.

## <a name="planning-best-practices"></a>Bewährte Methoden bei der Planung

Die folgenden Ressourcen tragen für Ihr Team zum Verständnis der Unterschiede zwischen Azure und Azure Stack Hub bei:

- [Azure Stack: Übersicht und Roadmap](https://azure.microsoft.com/resources/videos/ignite-2018-azure-stack-overview-and-roadmap/)
- [Azure Stack-Kapazitätsplanung](/azure/azure-stack/capacity-planning)
- [Azure Stack Hub-Rechenzentrumsintegration: exemplarische Vorgehensweise](/azure-stack/operator/azure-stack-customer-journey)
- [Features virtueller Azure Stack-Computer](/azure-stack/user/azure-stack-vm-considerations?view=azs-1910)

Nachdem Sie die beste Plattform für die einzelnen Workloads kennen, können Sie Ihre Entscheidungen in einen [Cloudeinführungsplan](../../plan/template.md) integrieren, um Migrationsvorgänge in öffentliche und private Clouds als einen ausgerichteten Vorgang zu verwalten.

## <a name="next-steps"></a>Nächste Schritte

Anleitungen zu bestimmten Elementen der Cloudeinführungsjourney finden Sie in den folgenden Artikeln:

- [Vorbereiten Ihrer Cloudumgebung für die Azure Stack Hub-Migration](./ready.md)
- [Bewerten von Workloads für Azure Stack Hub](./migrate-assess.md)
- [Bereitstellen von Workloads in Azure Stack Hub](./migrate-deploy.md)
- [Steuern von Azure Stack Hub](./govern.md)
- [Verwalten von Azure Stack Hub](./manage.md)
