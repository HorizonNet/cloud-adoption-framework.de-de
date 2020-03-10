---
title: Die fünf Disziplinen der Cloud-Governance
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über Kostenverwaltung, Bereitstellungsbeschleunigung, Identitätsbaseline, Ressourcenkonsistenz und Sicherheitsbaseline zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d50364a621e57b95e26f5686f4d470984530e161
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707678"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Die fünf Disziplinen der Cloud-Governance

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsI">
    <li style="display: flex; flex-direction: column;">
        <div class="cardSize">
            <div class="cardPadding" style="padding-bottom:10px;">
                <div class="card" style="padding-bottom:10px;">
                    <div class="cardText" style="padding-left:0px;">
Jede Änderung von Geschäftsprozessen oder Technologieplattformen birgt Risiken. Cloudgovernanceteams, deren Mitglieder manchmal auch als Cloudverwalter bezeichnet werden, haben die Aufgabe, diese Risiken mit minimaler Unterbrechung der Einführungs- oder Innovationsanstrengungen zu minimieren.<br/><br/>Das Governancemodell des Frameworks zur Cloudeinführung steuert diese Entscheidungen (unabhängig von der ausgewählten Cloudplattform), indem es sich auf die <a href="./corporate-policy.md">Entwicklung der Unternehmensrichtlinien</a> und die <a href="#disciplines-of-cloud-governance">fünf Disziplinen von Cloudgovernance</a> konzentriert. <a href="./guides/index.md">Umsetzbare Entwurfsleitfäden</a> zeigen dieses Modell mithilfe von Azure-Diensten. Im Folgenden werden die Disziplinen des Governancemodells im Framework für die Cloudeinführung erläutert.
                    </div>
                </div>
            </div>
        </div>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="../_images/operational-transformation-govern-highres.png" style="display: flex; flex-direction: column; flex: 1 0 auto;">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardText" style="padding-left:0px;">
    <img src="../_images/operational-transformation-govern-highres.png" alt="Diagram of the Cloud Adoption Framework governance model: Corporate policy and governance disciplines">
    <br>
    <i>Abbildung 1: Diagramm der Unternehmensrichtlinie und der fünf Disziplinen von Cloud Governance.</i>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="disciplines-of-cloud-governance"></a>Disziplinen von Cloud Governance

Für jede Cloudplattform gibt es allgemeine Governancedisziplinen, die als Leitfaden dienen können, um Richtlinien zu formulieren und Toolketten anzupassen. Diese Disziplinen sind ausschlaggebend für Entscheidungen über den richtigen Automatisierungsgrad und die Durchsetzung von Unternehmensrichtlinien auf Cloudplattformen.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsA">
<li style="display: flex; flex-direction: column;">
    <a href="./cost-management/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/cost-management.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Cost Management</h3>
                        <p>Die Kosten sind für Cloudbenutzer ein Hauptanliegen. Entwickeln Sie Richtlinien zur Kostenkontrolle für alle Cloudplattformen.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./security-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/security-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Sicherheitsbaseline</h3>
                        <p>Sicherheit ist ein komplexes Thema, das für jedes Unternehmen einzigartig ist. Sobald die Sicherheitsanforderungen festgelegt sind, wenden Cloudgovernancerichtlinien und -durchsetzung diese Anforderungen auf Netzwerk-, Daten- und Ressourcenkonfigurationen an.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./identity-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/identity-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Identitätsbaseline</h3>
                        <p>Inkonsistenzen bei der Anwendung von Identitätsanforderungen können das Risiko von Sicherheitsverletzungen erhöhen. Die Identitätsbaseline-Disziplin stellt hauptsächlich sicher, dass die Identität bei der Cloudeinführung konsistent angewendet wird.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./resource-consistency/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/resource-consistency.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Ressourcenkonsistenz</h3>
                        <p>Cloudvorgänge hängen von einer konsistenten Ressourcenkonfiguration ab. Durch Governancetools können Ressourcen konsistent konfiguriert werden, um Risiken im Zusammenhang mit Onboarding, Abweichung, Erkennbarkeit und Wiederherstellung zu umgehen.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./deployment-acceleration/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/deployment-acceleration.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Beschleunigung der Bereitstellung</h3>
                        <p>Zentralisierung, Standardisierung und Konsistenz bei Bereitstellungs- und Konfigurationsansätzen verbessern die Governancepraktiken. Wenn diese Aspekte über cloudbasierte Governancetools bereitgestellt werden, schaffen sie einen Cloudfaktor, der die Bereitstellungsaktivitäten beschleunigen kann.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->
