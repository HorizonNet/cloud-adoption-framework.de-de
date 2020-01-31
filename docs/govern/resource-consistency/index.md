---
title: Übersicht über die Disziplin „Ressourcenkonsistenz“
description: Übersicht über die Disziplin „Ressourcenkonsistenz“
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 864a5d3679d80663337b1b73748ab2af6628ef7d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806100"
---
# <a name="resource-consistency-discipline-overview"></a>Übersicht über die Disziplin „Ressourcenkonsistenz“

„Ressourcenkonsistenz“ ist eine der [fünf Disziplinen von Cloudgovernance](../governance-disciplines.md) innerhalb des [CAF-Governancemodells (Cloud Adoption Framework)](../index.md). Dieser Disziplin konzentriert sich auf Möglichkeiten zum Einrichten von Richtlinien, die sich auf die Verwaltung des Betriebs einer Umgebung, Anwendung oder Workload beziehen. IT-Betriebsteams bieten häufig eine Überwachung der Leistung von Anwendungen, Workloads und Ressourcen. Darüber führen sie auch häufig Aufgaben aus, die zur Erfüllung von Skalierungsanforderungen erforderlich sind, sowie zur Korrektur von Verstößen gegen die Vereinbarung zum Leistungsservicelevel (Service Level Agreement, SLA) und zur proaktiven Vermeidung von SLA-Leistungsverstößen durch automatisierte Wartung. Innerhalb der fünf Disziplinen der Cloudgovernance ist die Ressourcenkonsistenz eine Disziplin, die sicherstellt, dass Ressourcen derart einheitlich konfiguriert sind, dass sie von IT-Abläufen erkannt werden können, in Notfallwiederherstellungslösungen eingeschlossen sind und in wiederholbare Betriebsprozesse aufgenommen werden können.

> [!NOTE]
> Die Governance der Ressourcenkonsistenz ersetzt nicht die vorhandenen IT-Teams, -Prozesse und -Verfahren, mit denen Ihr Unternehmen cloudbasierte Ressourcen effizient verwalten kann. Der Hauptzweck dieser Disziplin ist es, potenzielle Geschäftsrisiken zu identifizieren und den für die Verwaltung Ihrer Ressourcen in der Cloud zuständigen IT-Mitarbeitern Hilfe bei der Risikominderung zu geben. Bei der Entwicklung von Governancerichtlinien und -prozessen ist darauf zu achten, dass die relevanten IT-Teams in Ihre Planungs- und Überprüfungsprozesse einbezogen werden.

In diesem Abschnitt des Frameworks für die Einführung der Cloud wird beschrieben, wie Sie eine Disziplin „Ressourcenkonsistenz“ als Teil Ihrer Cloudgovernancestrategie entwickeln. Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten jedoch die Einbeziehung von und Diskussion mit relevanten Mitgliedern des IT-Teams beinhalten, die für die Implementierung und Verwaltung der Ressourcenkonsistenz Ihrer Organisation verantwortlich sind.

Wenn Ihre Organisation nicht über internes Fachwissen zu Strategien der Ressourcenkonsistenz verfügt, können Sie im Rahmen dieser Disziplin externe Berater hinzuziehen. Sie können auch [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services), den Cloudeinführungsdienst [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) oder andere externe Experten für die Cloudeinführung einbeziehen, um zu besprechen, wie sich Ihre cloudbasierten Ressourcen am besten organisieren, nachverfolgen und optimieren lassen.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin „Ressourcenkonsistenz“. Beispiele für Richtlinienanweisungen finden Sie im Artikel über [Richtlinienanweisungen für Ressourcenkonsistenz](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für die Governancerichtlinien Ihrer Organisation dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden sechs Schritte enthalten Beispiele und mögliche Optionen, die bei der Entwicklung der Governance der Ressourcenkonsistenz zu berücksichtigen sind. Verwenden Sie die einzelnen Schritte als Ausgangspunkte für Diskussionen innerhalb Ihres Cloudgovernanceteams sowie mit den beteiligten Geschäfts- und IT-Teams in Ihrer Organisation, um die Richtlinien und Prozesse festzulegen, die zur Bewältigung von Ressourcenkonsistenzrisiken erforderlich sind.

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
                        <h3>Vorlage für Ressourcenkonsistenz</h3>
                        <p class="x-hidden-focus">Laden Sie die Vorlage zur Dokumentation einer Disziplin vom Typ „Ressourcenkonsistenz“ herunter.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li><li style="display: flex; flex-direction: column;">
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
                        <p class="x-hidden-focus">Abstimmung der Einsatzreife der Cloudverwaltung mit den Phasen der Cloudeinführung.</p>
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
