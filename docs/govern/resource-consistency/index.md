---
title: Übersicht über die Disziplin „Ressourcenkonsistenz“
description: Hier wird der Ansatz zur Entwicklung der Disziplin „Ressourcenkonsistenz“ als Teil einer Cloudgovernancestrategie beschrieben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dd6490f3f0898b404201dfabef06a74d77e86d38
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88569279"
---
# <a name="resource-consistency-discipline-overview"></a>Übersicht über die Disziplin „Ressourcenkonsistenz“

„Ressourcenkonsistenz“ ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md) innerhalb des [Cloud Adoption Framework-Governancemodells](../index.md). Dieser Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Richtlinien, die sich auf die Verwaltung des Betriebs einer Umgebung, Anwendung oder Workload beziehen. IT-Betriebsteams übernehmen häufig die Überwachung der Leistung von Anwendungen, Workloads und Ressourcen. Außerdem führen sie häufig Aufgaben aus, die zur Erfüllung von Skalierungsanforderungen, zur Korrektur von Verstößen gegen die Vereinbarung zum Leistungsservicelevel (Service Level Agreement, SLA) und zur proaktiven Vermeidung von SLA-Leistungsverstößen durch automatisierte Wartung erforderlich sind. Innerhalb der fünf Disziplinen der Cloudgovernance stellt die Disziplin „Ressourcenkonsistenz“ sicher, dass Ressourcen derart einheitlich konfiguriert sind, dass sie von IT-Vorgängen erkannt werden können, in Notfallwiederherstellungslösungen eingeschlossen sind und in wiederholbare Betriebsprozesse integriert werden können.

> [!NOTE]
> Die Disziplin „Ressourcenkonsistenz“ ersetzt nicht die vorhandenen IT-Teams, -Prozesse und -Verfahren, mit denen Ihre Organisation cloudbasierte Ressourcen effizient verwalten kann. Der Hauptzweck dieser Disziplin ist es, potenzielle Geschäftsrisiken zu identifizieren und den für die Verwaltung Ihrer Ressourcen in der Cloud zuständigen IT-Mitarbeitern Hilfe bei der Risikominderung zu geben. Bei der Entwicklung von Governancerichtlinien und -prozessen ist darauf zu achten, dass die relevanten IT-Teams in Ihre Planungs- und Überprüfungsprozesse einbezogen werden.

In diesem Abschnitt des Frameworks für die Einführung der Cloud wird beschrieben, wie Sie eine Disziplin „Ressourcenkonsistenz“ als Teil Ihrer Cloudgovernancestrategie entwickeln. Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten die Einbeziehung von und Gespräche mit relevanten Mitgliedern der IT-Teams umfassen, die für die Implementierung und Verwaltung der Ressourcenkonsistenzlösungen Ihrer Organisation verantwortlich sind.

Wenn Ihre Organisation nicht über internes Fachwissen über Strategien der Ressourcenkonsistenz verfügt, können Sie im Rahmen dieser Disziplin externe Berater hinzuziehen. Sie können auch [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting), den Cloudeinführungsdienst [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) oder andere externe Experten für die Cloudeinführung einbeziehen, um zu besprechen, wie sich Ihre cloudbasierten Ressourcen am besten organisieren, nachverfolgen und optimieren lassen.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin „Ressourcenkonsistenz“. Verwenden Sie die [Beispielrichtlinienanweisungen](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für das Definieren Ihrer Ressourcenkonsistenzrichtlinien dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden Schritte enthalten Beispiele und mögliche Optionen, die Sie beim Entwickeln der Disziplin „Ressourcenkonsistenz“ berücksichtigen sollten. Verwenden Sie die einzelnen Schritte als Ausgangspunkt für Diskussionen innerhalb Ihres Cloudgovernanceteams sowie mit den beteiligten Geschäfts- und IT-Teams in Ihrer Organisation, um die Richtlinien und Prozesse festzulegen, die zur Bewältigung von Risiken in Bezug auf die Disziplin „Ressourcenkonsistenz“ erforderlich sind.

|  |  |
|--|--|
| <br> ![Vorlagensymbol](../../_images/govern/process-template.png) | <br> [Vorlage für die Disziplin „Ressourcenkonsistenz“:](./template.md) Laden Sie die Vorlage zur Dokumentation einer Disziplin vom Typ „Ressourcenkonsistenz“ herunter. |
| <br> ![Risikosymbol](../../_images/govern/process-risks.png) | <br> [Geschäftsrisiken:](./business-risks.md) Machen Sie sich mit den Motiven und Risiken vertraut, die häufig mit der Disziplin „Ressourcenkonsistenz“ verbunden sind. |
| <br> ![Metriksymbol](../../_images/govern/process-metrics.png) | <br> [Indikatoren und Metriken:](./metrics-tolerance.md) Indikatoren, um zu verstehen, ob es der richtige Zeitpunkt ist, in die Disziplin „Ressourcenkonsistenz“ zu investieren. |
| <br> ![Einhaltungssymbol](../../_images/govern/process-enforce.png) | <br> [Prozesse zur Einhaltung von Richtlinien:](./compliance-processes.md) Empfohlene Prozesse zur Unterstützung der Richtlinieneinhaltung in der Disziplin „Ressourcenkonsistenz“. |
| <br> ![Einsatzreifesymbol](../../_images/govern/process-maturity.png) | <br> [Einsatzreife:](./discipline-improvement.md) Stimmen Sie die Einsatzreife der Cloudverwaltung mit den Phasen der Cloudeinführung ab.  |
| <br> ![Toolkettensymbol](../../_images/govern/process-toolchain.png) | <br> [Toolkette:](./toolchain.md) Azure-Dienste, die zur Unterstützung der Disziplin „Ressourcenkonsistenz“ implementiert werden können. |

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der Bewertung von [Geschäftsrisiken](./business-risks.md) in einem bestimmten Umfeld.

> [!div class="nextstepaction"]
> [Grundlegendes zu Geschäftsrisiken](./business-risks.md)
