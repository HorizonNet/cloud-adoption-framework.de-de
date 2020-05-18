---
title: Übersicht über die Disziplin „Identitätsbaseline“
description: Hier wird der Ansatz zur Entwicklung der Disziplin „Identitätsbaseline“ als Teil einer Cloudgovernancestrategie beschrieben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2e171736ccf993d3e7401350008ab542759b703b
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400789"
---
# <a name="identity-baseline-discipline-overview"></a>Übersicht über die Disziplin „Identitätsbaseline“

„Identitätsbaseline“ ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md) innerhalb des [Cloud Adoption Framework-Governancemodells](../index.md). Identität wird zunehmend als primärer Sicherheitsbereich in der Cloud angesehen. Dies ist eine Abkehr vom traditionellen Schwerpunkt der Netzwerksicherheit. Identitätsdienste umfassen die wesentlichen Mechanismen zur Unterstützung der Zugriffssteuerung und -organisation innerhalb von IT-Umgebungen. Und die Disziplin der Identitätsbaseline ergänzt die [Disziplin der Sicherheitsbaseline](../security-baseline/index.md) durch konsequente Anwendung von Authentifizierungs- und Autorisierungsanforderungen im Rahmen der Cloudeinführung.

> [!NOTE]
> Die Disziplin „Identitätsbaseline“ ersetzt nicht die vorhandenen IT-Teams, -Prozesse und -Verfahren, mit denen Ihre Organisation Identitätsdienste verwalten und schützen kann. Der Hauptzweck dieser Disziplin besteht darin, potenzielle identitätsbezogene Geschäftsrisiken zu identifizieren und den IT-Mitarbeitern, die für die Implementierung, Verwaltung und den Betrieb Ihrer Identitätsverwaltungsinfrastruktur verantwortlich sind, eine Anleitung zur Risikominderung zu geben. Bei der Entwicklung von Governancerichtlinien und -prozessen ist darauf zu achten, dass die relevanten IT-Teams in Ihre Planungs- und Überprüfungsprozesse einbezogen werden.

In diesem Abschnitt des CAF-Leitfadens (Cloud Adoption Framework) wird der Ansatz zur Entwicklung einer Disziplin der Identitätsbaseline als Teil Ihrer Cloudgovernancestrategie beschrieben. Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten jedoch die Einbeziehung von und Diskussion mit relevanten Mitgliedern des IT-Teams beinhalten, die für die Implementierung und Verwaltung der Identitätsverwaltungslösungen Ihrer Organisation verantwortlich sind.

Wenn Ihre Organisation nicht über internes Fachwissen in den Bereichen Identität und Sicherheit verfügt, können Sie im Rahmen dieser Disziplin externe Berater hinzuziehen. Sie können auch [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting), den Cloudeinführungsdienst [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) oder andere externe Partner für die Cloudeinführung einbeziehen, um Probleme im Zusammenhang mit dieser Disziplin zu besprechen.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin der Identitätsbaseline. Beispiele für Richtlinienanweisungen finden Sie im Artikel über [Richtlinienanweisungen für Identitätsbaseline](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für die Governancerichtlinien Ihrer Organisation dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden sechs Schritte enthalten Beispiele und mögliche Optionen, die Sie beim Entwickeln der Disziplin „Identitätsbaseline“ berücksichtigen sollten. Verwenden Sie die einzelnen Schritte als Ausgangspunkte für Diskussionen innerhalb Ihres Cloudgovernanceteams sowie mit den beteiligten Geschäfts- und IT-Teams in Ihrer Organisation, um die Richtlinien und Prozesse auszuarbeiten, die zur Bewältigung identitätsbezogener Risiken erforderlich sind.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![Vorlagensymbol](../../_images/govern/process-template.png) <br> [Vorlage für die Disziplin „Identitätsbaseline“:](./template.md) Laden Sie die Vorlage zur Dokumentation einer Disziplin vom Typ „Identitätsbaseline“ herunter. |
| <br> ![Risikosymbol](../../_images/govern/process-risks.png) <br> [Geschäftsrisiken:](./business-risks.md) Machen Sie sich mit den Motiven und Risiken vertraut, die häufig mit der Disziplin „Identitätsbaseline“ verbunden sind. |
| <br> ![Metriksymbol](../../_images/govern/process-metrics.png) <br> [Indikatoren und Metriken:](./metrics-tolerance.md) Indikatoren, um zu verstehen, ob es der richtige Zeitpunkt ist, in die Disziplin „Identitätsbaseline“ zu investieren. |
| <br> ![Einhaltungssymbol](../../_images/govern/process-enforce.png) <br> [Prozesse zur Einhaltung von Richtlinien:](./compliance-processes.md) Empfohlene Prozesse zur Unterstützung der Richtlinieneinhaltung in der Disziplin „Identitätsbaseline“. |
| <br> ![Einsatzreifesymbol](../../_images/govern/process-maturity.png) <br> [Einsatzreife:](./discipline-improvement.md) Stimmen Sie die Einsatzreife der Cloudverwaltung mit den Phasen der Cloudeinführung ab. |
| <br> ![Toolkettensymbol](../../_images/govern/process-toolchain.png) <br> [Toolkette:](./toolchain.md) Azure-Dienste, die zur Unterstützung der Disziplin „Identitätsbaseline“ implementiert werden können. |

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der Bewertung von [Geschäftsrisiken](./business-risks.md) in einem bestimmten Umfeld.

> [!div class="nextstepaction"]
> [Grundlegendes zu Geschäftsrisiken](./business-risks.md)
