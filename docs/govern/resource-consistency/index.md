---
title: Übersicht über die Disziplin „Ressourcenkonsistenz“
description: Hier wird der Ansatz zur Entwicklung der Disziplin „Ressourcenkonsistenz“ als Teil einer Cloudgovernancestrategie beschrieben.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 3bfe85e2305f1c844ddf92a14cf298a0a1c30edb
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218168"
---
# <a name="resource-consistency-discipline-overview"></a>Übersicht über die Disziplin „Ressourcenkonsistenz“

„Ressourcenkonsistenz“ ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md) innerhalb des [Cloud Adoption Framework-Governancemodells](../index.md). Dieser Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Richtlinien, die sich auf die Verwaltung des Betriebs einer Umgebung, Anwendung oder Workload beziehen. IT-Betriebsteams übernehmen häufig die Überwachung der Leistung von Anwendungen, Workloads und Ressourcen. Außerdem führen sie häufig Aufgaben aus, die zur Erfüllung von Skalierungsanforderungen, zur Korrektur von Verstößen gegen die Vereinbarung zum Leistungsservicelevel (Service Level Agreement, SLA) und zur proaktiven Vermeidung von SLA-Leistungsverstößen durch automatisierte Wartung erforderlich sind. Innerhalb der fünf Disziplinen der Cloudgovernance stellt die Disziplin „Ressourcenkonsistenz“ sicher, dass Ressourcen derart einheitlich konfiguriert sind, dass sie von IT-Vorgängen erkannt werden können, in Notfallwiederherstellungslösungen eingeschlossen sind und in wiederholbare Betriebsprozesse integriert werden können.

> [!NOTE]
> Die Disziplin „Ressourcenkonsistenz“ ersetzt nicht die vorhandenen IT-Teams, -Prozesse und -Verfahren, mit denen Ihre Organisation cloudbasierte Ressourcen effizient verwalten kann. Der Hauptzweck dieser Disziplin ist es, potenzielle Geschäftsrisiken zu identifizieren und den für die Verwaltung Ihrer Ressourcen in der Cloud zuständigen IT-Mitarbeitern Hilfe bei der Risikominderung zu geben. Bei der Entwicklung von Governancerichtlinien und -prozessen ist darauf zu achten, dass die relevanten IT-Teams in Ihre Planungs- und Überprüfungsprozesse einbezogen werden.

In diesem Abschnitt des Frameworks für die Einführung der Cloud wird beschrieben, wie Sie eine Disziplin „Ressourcenkonsistenz“ als Teil Ihrer Cloudgovernancestrategie entwickeln. Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten jedoch die Einbeziehung von und Gespräche mit relevanten Mitgliedern der IT-Teams umfassen, die für die Implementierung und Verwaltung der Ressourcenkonsistenzlösungen Ihrer Organisation verantwortlich sind.

Wenn Ihre Organisation nicht über internes Fachwissen über Strategien der Ressourcenkonsistenz verfügt, können Sie im Rahmen dieser Disziplin externe Berater hinzuziehen. Sie können auch [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting), den Cloudeinführungsdienst [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) oder andere externe Experten für die Cloudeinführung einbeziehen, um zu besprechen, wie sich Ihre cloudbasierten Ressourcen am besten organisieren, nachverfolgen und optimieren lassen.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin „Ressourcenkonsistenz“. Beispiele für Richtlinienanweisungen finden Sie im Artikel über [Richtlinienanweisungen für Ressourcenkonsistenz](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für die Governancerichtlinien Ihrer Organisation dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden sechs Schritte enthalten Beispiele und mögliche Optionen, die Sie beim Entwickeln der Disziplin „Ressourcenkonsistenz“ berücksichtigen sollten. Verwenden Sie die einzelnen Schritte als Ausgangspunkt für Diskussionen innerhalb Ihres Cloudgovernanceteams sowie mit den beteiligten Geschäfts- und IT-Teams in Ihrer Organisation, um die Richtlinien und Prozesse festzulegen, die zur Bewältigung von Risiken in Bezug auf die Disziplin „Ressourcenkonsistenz“ erforderlich sind.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Vorlage für die Disziplin „Ressourcenkonsistenz“</h3>
                        <p class="x-hidden-focus">Laden Sie die Vorlage zur Dokumentation einer Disziplin vom Typ „Ressourcenkonsistenz“ herunter.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./business-risks.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Geschäftsrisiken</h3>
                        <p class="x-hidden-focus">Machen Sie sich mit den Motiven und Risiken vertraut, die häufig mit der Disziplin „Ressourcenkonsistenz“ verbunden sind.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./metrics-tolerance.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indikatoren und Metriken</h3>
                        <p class="x-hidden-focus">Indikatoren, die Aufschluss darüber geben, ob jetzt der richtige Zeitpunkt ist, in die Disziplin „Ressourcenkonsistenz“ zu investieren.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./compliance-processes.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Prozesse zur Einhaltung von Richtlinien</h3>
                        <p class="x-hidden-focus">Empfohlene Prozesse zur Unterstützung der Richtlinieneinhaltung in der Disziplin „Ressourcenkonsistenz“.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./discipline-improvement.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Einsatzreife</h3>
                        <p class="x-hidden-focus">Stimmen Sie die Einsatzreife der Cloudverwaltung mit den Phasen der Cloudeinführung ab.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./toolchain.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Toolkette</h3>
                        <p class="x-hidden-focus">Azure-Dienste, die zur Unterstützung der Disziplin „Ressourcenkonsistenz“ implementiert werden können.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit der Bewertung von [Geschäftsrisiken](./business-risks.md) in einem bestimmten Umfeld.

> [!div class="nextstepaction"]
> [Grundlegendes zu Geschäftsrisiken](./business-risks.md)
