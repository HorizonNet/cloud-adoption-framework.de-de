---
title: Übersicht über die Disziplin „Sicherheitsbaseline“
description: Hier wird der Ansatz zur Entwicklung der Disziplin „Sicherheitsbaseline“ als Teil einer Cloudgovernancestrategie beschrieben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 27714dd779a9d0c3624cdce6355a478dbd9168f4
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83620560"
---
# <a name="security-baseline-discipline-overview"></a>Übersicht über die Disziplin „Sicherheitsbaseline“

„Sicherheitsbaseline“ ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md) innerhalb des [Cloud Adoption Framework-Governancemodells](../index.md). Sicherheit ist Bestandteil jeder IT-Bereitstellung, und durch die Cloud ergeben sich besondere Sicherheitsaspekte. Viele Unternehmen unterliegen gesetzlichen Bestimmungen, die den Schutz sensibler Daten zu einer wichtigen organisatorischen Priorität machen, wenn es um Cloudtransformation geht. Die Erkennung potenzieller Sicherheitsbedrohungen für Ihre Cloudumgebung sowie die Einrichtung von Prozessen und Verfahren für den Umgang mit diesen Bedrohungen sollten für jedes IT- oder Cybersicherheitsteam Priorität haben. Mit der Disziplin „Sicherheitsbaseline“ wird sichergestellt, dass technische Anforderungen und Sicherheitseinschränkungen konsistent auf Cloudumgebungen angewendet werden, sobald sich diese Anforderungen stellen.

> [!NOTE]
> Die Disziplin „Sicherheitsbaseline“ ersetzt nicht die vorhandenen IT-Teams, -Prozesse und -Verfahren, die Ihre Organisation zum Schützen von in der Cloud bereitgestellten Ressourcen verwendet. Der Hauptzweck dieser Disziplin ist es, sicherheitsrelevante Geschäftsrisiken zu identifizieren und den für die Sicherheitsinfrastruktur zuständigen IT-Mitarbeitern eine Anleitung zur Risikominderung zu geben. Bei der Entwicklung von Governancerichtlinien und -prozessen ist darauf zu achten, dass die relevanten IT-Teams in Ihre Planungs- und Überprüfungsprozesse einbezogen werden.

In diesem Artikel wird der Ansatz zur Entwicklung einer Disziplin „Sicherheitsbaseline“ als Teil Ihrer Cloud Governance-Strategie beschrieben. Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten jedoch die Einbeziehung von und Diskussion mit relevanten Mitgliedern Ihrer IT- und Sicherheitsteams beinhalten, insbesondere der technischen Führungskräfte, die für die Implementierung von Netzwerk-, Verschlüsselungs- und Identitätsdiensten verantwortlich sind.

Die richtigen Sicherheitsentscheidungen zu treffen, ist entscheidend für den Erfolg Ihrer Cloudbereitstellungen und größeren Geschäftserfolg. Wenn Ihre Organisation nicht über internes Fachwissen im Bereich Cybersicherheit verfügt, können Sie externe Sicherheitsberater als Bestandteil dieser Disziplin einbeziehen. Sie können auch [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting), den Cloudeinführungsdienst [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) oder andere externe Experten für die Cloudeinführung einbeziehen, um Probleme im Zusammenhang mit dieser Disziplin zu besprechen.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin „Sicherheitsbaseline“. Beispiele für Richtlinienanweisungen finden Sie im Artikel über [Richtlinienanweisungen für Sicherheitsbaseline](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für die Governancerichtlinien Ihrer Organisation dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden sechs Schritte enthalten Beispiele und mögliche Optionen, die Sie beim Entwickeln der Disziplin „Sicherheitsbaseline“ berücksichtigen sollten. Verwenden Sie die einzelnen Schritte als Ausgangspunkte für Diskussionen innerhalb Ihres Cloudgovernanceteams sowie mit betroffenen Geschäfts-, IT- und Sicherheitsteams in Ihrer Organisation, um die Richtlinien und Prozesse auszuarbeiten, die zur Bewältigung sicherheitsrelevanter Risiken erforderlich sind.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![Vorlagensymbol](../../_images/govern/process-template.png) | <br> [Vorlage für die Disziplin „Sicherheitsbaseline“:](./template.md) Laden Sie die Vorlage zur Dokumentation einer Disziplin vom Typ „Sicherheitsbaseline“ herunter. |
| <br> ![Risikosymbol](../../_images/govern/process-risks.png) | <br> [Geschäftsrisiken:](./business-risks.md) Machen Sie sich mit den Motiven und Risiken vertraut, die häufig mit der Disziplin „Sicherheitsbaseline“ verbunden sind. |
| <br> ![Metriksymbol](../../_images/govern/process-metrics.png) | <br> [Indikatoren und Metriken:](./metrics-tolerance.md) Indikatoren, um zu verstehen, ob es der richtige Zeitpunkt ist, in die Disziplin „Sicherheitsbaseline“ zu investieren. |
| <br> ![Einhaltungssymbol](../../_images/govern/process-enforce.png) | <br> [Prozesse zur Einhaltung von Richtlinien:](./compliance-processes.md) Empfohlene Prozesse zur Unterstützung der Richtlinieneinhaltung in der Disziplin „Sicherheitsbaseline“. |
| <br> ![Einsatzreifesymbol](../../_images/govern/process-maturity.png) | <br> [Einsatzreife:](./discipline-improvement.md) Stimmen Sie die Einsatzreife der Cloudverwaltung mit den Phasen der Cloudeinführung ab. |
| <br> ![Toolkettensymbol](../../_images/govern/process-toolchain.png) | <br> [Toolkette:](./toolchain.md) Azure-Dienste, die zur Unterstützung der Disziplin „Sicherheitsbaseline“ implementiert werden können. |

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der Bewertung von Geschäftsrisiken in einem bestimmten Umfeld.

> [!div class="nextstepaction"]
> [Grundlegendes zu Geschäftsrisiken](./business-risks.md)
