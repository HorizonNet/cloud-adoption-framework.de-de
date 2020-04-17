---
title: Governance für die Einführung der Microsoft Cloud für Azure (Microsoft Cloud Adoption Framework)
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Sie vorhandene Richtlinien bewerten, eine anfängliche Governancegrundlage erstellen und iterativ Governancetools hinzufügen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 75b2269c4db348ab6a110309490187ef44b55f6c
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "77706930"
---
# <a name="governance-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Governance für die Einführung der Microsoft Cloud für Azure (Microsoft Cloud Adoption Framework)

Die Cloud schafft neue Paradigmen für die Technologien, die das Unternehmen unterstützen. Diese neuen Paradigmen verändern auch die Einführung, Verwaltung und Steuerung dieser Technologien. Wenn ganze Datencenter mit einer einzigen, durch einen unbeaufsichtigten Prozess ausgeführten Codezeile zerstört und neu aufgebaut werden können, müssen wir die traditionellen Ansätze überdenken. Das gilt insbesondere für die Governance.

## <a name="get-started-with-cloud-governance"></a>Erste Schritte bei der Cloudgovernance

Cloudgovernance ist ein iterativer Prozess. Bei Organisationen mit vorhandenen Richtlinien zum Steuern lokaler IT-Umgebungen sollte die Cloudgovernance diese Richtlinien ergänzen. Der Grad der Integration von Unternehmensrichtlinien zwischen lokalen Systemen und der Cloud hängt jedoch von der Ausgereiftheit der Cloudgovernance und den digitalen Ressourcen in der Cloud ab. Mit der Änderung der Cloudressourcen im Laufe der Zeit ändern sich auch Cloudgovernanceprozesse und -richtlinien. Die folgenden Aufgaben unterstützen Sie bei der Einrichtung Ihrer anfänglichen Governancegrundlage.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./methodology.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Methodik</h3>
Entwickeln Sie ein Grundverständnis der Methodik, die der Cloudgovernance im Framework für die Cloudeinführung zugrunde liegt, um eine Lösung für den Endzustand zu planen.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./benchmark.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Vergleichstest</h3>
Bewerten Sie den Ist- und Sollzustand, um sich vorstellen zu können, wie das Framework angewendet werden kann.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./initial-foundation.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Anfängliche Governancegrundlage</h3>
Beschränken Sie sich bei Ihren Governancebemühungen zunächst auf eine geringe Anzahl problemlos implementierbarer Governancetools. Diese anfängliche Governancegrundlage wird als MVP (Minimum Viable Product) bezeichnet.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./foundation-improvements.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Verbessern der anfänglichen Governancegrundlage</h3>
Fügen Sie während der gesamten Umsetzung des Cloudeinführungsplans nach und nach Governancekontrollen hinzu, um im Rahmen des gesamten Prozesses materielle Risiken abzudecken.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="objective-of-this-content"></a>Ziel dieses Inhalts

Die Anleitungen in diesem Abschnitt zum Framework für die Cloudeinführung haben zwei Funktionen:

- Sie liefern Beispiele für umsetzbare Governanceleitfäden, die gängige Kundenerfahrungen widerspiegeln. Jedes Beispiel umfasst Geschäftsrisiken, Unternehmensrichtlinien zur Risikominderung und Entwurfsrichtlinien für die Implementierung technischer Lösungen. Die Designrichtlinien sind zwangsläufig spezifisch für Azure. Alle anderen Inhalte in diesen Leitfäden können cloudunabhängig oder im Rahmen eines Multi-Cloud-Ansatzes angewendet werden.
- Sie unterstützen Sie bei der Erstellung personalisierter Governancelösungen, die eine Vielzahl von Geschäftsanforderungen erfüllen. Dies umfasst detaillierte Anleitungen zur Entwicklung von Unternehmensrichtlinien, -prozessen und -tools, um die Governance für mehrere öffentliche Clouds sicherzustellen.

Diese Inhalte sind für das Cloudgovernanceteam konzipiert. Sie sind auch für Cloudarchitekten relevant, die eine solide Grundlage für die Cloudgovernance entwickeln müssen.

## <a name="intended-audience"></a>Zielpublikum

Die Inhalte im CAF (Cloud Adoption Framework) beeinflussen das Geschäft, die Technologie und die Kultur von Unternehmen. Dieser Abschnitt des Frameworks zur Cloudeinführung erfordert eine intensive Interaktion mit den Teams für IT-Sicherheit und IT-Governance, der Finanzabteilung, Geschäftsbereichsleitern sowie den Netzwerk-, Identitäts- und Cloudeinführungsteams. Verschiedene Abhängigkeiten zwischen diesen Rollen erfordern einen vermittelnden Ansatz der Cloudarchitekten unter Verwendung dieser Leitlinien. Eine solche Vermittlung zwischen den Teams ist möglicherweise nur ein einziges Mal erforderlich. In einigen Fällen sind aber auch längerfristige Interaktionen mit diesen anderen Mitarbeitern erforderlich.

Der Cloudarchitekt dient als innovative Führungsperson und Vermittler, um diese Zielgruppen zusammenzubringen. Diese Anleitungen sind darauf ausgelegt, Cloudarchitekten die richtige Kommunikation mit der richtigen Zielgruppe zu erleichtern, um notwendige Entscheidungen zu fördern. Um eine durch die Cloud ermöglichte Transformation der Geschäftsabläufe umzusetzen, müssen Cloudarchitekten die betroffenen Teams in allen Geschäfts- und IT-Abteilungen bei ihren Entscheidungen unterstützen.

**Spezialisierungen des Cloudarchitekten in diesem Abschnitt**: Jeder Abschnitt des Frameworks für die Cloudeinführung stellt eine andere Spezialisierung oder Variante der Rolle des Cloudarchitekten dar. Dieser Abschnitt des Cloud Adoption Frameworks für die Einführung der Cloud richtet sich beispielsweise an Cloudarchitekten mit Schwerpunkt auf Verringerung technischer Risiken. Einige Cloudanbieter bezeichnen diese Spezialisten als *Cloudverwalter*, wir bevorzugen allerdings die Begriffe *Cloudwächter* bzw. kollektiv *Cloudgovernanceteam*. In den einzelnen umsetzbaren Governanceleitfäden zeigen die Artikel, wie sich die Zusammensetzung und Rolle des Cloudgovernanceteams im Lauf der Zeit verändern kann.

## <a name="use-this-guide"></a>Verwenden dieses Leitfadens

Wenn Sie dem Leitfaden vom Anfang bis zum Ende folgen, helfen diese Inhalte Ihnen dabei, parallel zur Cloudimplementierung eine robuste Cloudgovernancestrategie zu entwickeln. Sie werden detailliert durch die Theorie und Implementierung einer solchen Strategie geleitet.

Einen Crashkurs zur Theorie und zum schnellen Einstieg in die Azure-Implementierung finden Sie in der [Übersicht über die Governanceleitfäden](./guides/index.md). Mit diesem Leitfaden können Sie klein anfangen und Ihre Governanceanforderungen parallel zu den Cloudeinführungsprojekten iterativ optimieren.

## <a name="next-steps"></a>Nächste Schritte

Entwickeln Sie ein Grundverständnis der Methodik, die der Cloudgovernance im Framework für die Cloudeinführung zugrunde liegt.

> [!div class="nextstepaction"]
> [Grundlegendes zur Methodik](./methodology.md)
