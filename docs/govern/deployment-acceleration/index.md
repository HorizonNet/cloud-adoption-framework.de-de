---
title: Übersicht über die Disziplin der Beschleunigung der Bereitstellung
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um die Beschleunigung der Bereitstellung im Hinblick auf Cloudgovernance zu verstehen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 369e12abcf0325ed44719ccb76bf0032b611f8f1
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220429"
---
# <a name="deployment-acceleration-discipline-overview"></a>Übersicht über die Disziplin der Beschleunigung der Bereitstellung

„Beschleunigung der Bereitstellung“ ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md) innerhalb des [CAF-Governancemodells (Cloud Adoption Framework)](../index.md). Diese Disziplin konzentriert sich auf das Festlegen von Richtlinien, mit denen die Ressourcenkonfiguration bzw. -bereitstellung gesteuert wird. Innerhalb der fünf Disziplinen der Cloudgovernance umfasst die Disziplin „Beschleunigung der Bereitstellung“ die Bereitstellung, Konfigurationsanpassung und Wiederverwendbarkeit von Skripts. Zu diesem Zweck können manuelle Aktivitäten oder vollständig automatisierte DevOps-Aktivitäten zum Einsatz kommen. In beiden Fällen bleiben die Richtlinien größtenteils gleich. Während diese Disziplin im Lauf der Zeit ausgereifter wird, kann das Cloudgovernanceteam als Partner bei DevOps- und Bereitstellungsstrategien über wiederverwendbare Ressourcen Bereitstellungen beschleunigen und Hindernisse bei der Cloudeinführung entfernen.

In diesem Artikel wird der Prozess zur Beschleunigung der Bereitstellung beschrieben, den ein Unternehmen bei der Planung, Erstellung, Einführung und Umsetzung der Implementierung einer Cloudlösung durchlaufen muss. Es ist unmöglich, alle Anforderungen für Unternehmen in einem einzigen Dokument zu berücksichtigen. Daher werden in jedem Abschnitt dieses Artikels minimal erforderliche und mögliche Aktivitäten vorgeschlagen. Ziel dieser Aktivitäten ist es, Sie beim Aufbau eines [Richtlinien-MVP](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy) und bei der Einrichtung eines Frameworks für die [inkrementelle Verbesserung der Richtlinie](../policy-compliance/index.md#incremental-policy-growth) zu unterstützen. Das Cloudgovernanceteam muss entscheiden, wie viel in diese Aktivitäten zur Verbesserung der Position im Hinblick auf die Beschleunigung der Bereitstellung investiert werden soll.

> [!NOTE]
> Die Disziplin der Beschleunigung der Bereitstellung ersetzt nicht die vorhandenen IT-Teams, -Prozesse und -Verfahren, mit denen Ihr Unternehmen cloudbasierte Ressourcen effizient bereitstellen und konfigurieren kann. Der Hauptzweck dieser Disziplin ist es, potenzielle Geschäftsrisiken zu identifizieren und den für die Verwaltung Ihrer Ressourcen in der Cloud zuständigen IT-Mitarbeitern Hilfe bei der Risikominderung zu geben. Bei der Entwicklung von Governancerichtlinien und -prozessen ist darauf zu achten, dass die relevanten IT-Teams in Ihre Planungs- und Überprüfungsprozesse einbezogen werden.

Die Hauptzielgruppe für diesen Leitfaden sind die Cloudarchitekten Ihrer Organisation und andere Mitglieder Ihres Cloudgovernanceteams. Die Entscheidungen, Richtlinien und Prozesse, die sich aus dieser Disziplin ergeben, sollten jedoch die Einbeziehung von und Diskussion mit relevanten Mitgliedern Ihrer Geschäfts- und IT-Teams beinhalten, insbesondere mit den Führungskräften, die für die Bereitstellung und Konfiguration von cloudbasierten Workloads verantwortlich sind.

## <a name="policy-statements"></a>Richtlinienanweisungen

Umsetzbare Richtlinienanweisungen und die daraus resultierenden Architekturanforderungen bilden die Grundlage für eine Disziplin der Beschleunigung der Bereitstellung. Beispiele für Richtlinienanweisungen finden Sie im Artikel über [Richtlinienanweisungen zur Beschleunigung der Bereitstellung](./policy-statements.md). Diese Beispiele können als Ausgangspunkt für die Governancerichtlinien Ihrer Organisation dienen.

> [!CAUTION]
> Die Beispielrichtlinien basieren auf allgemeinen Kundenerfahrungen. Zur besseren Anpassung dieser Richtlinien an spezifische Anforderungen zur Cloud Governance führen Sie die folgenden Schritte aus, um Richtlinienanweisungen zu erstellen, die Ihre individuellen Geschäftsanforderungen erfüllen.

## <a name="develop-governance-policy-statements"></a>Entwickeln von Richtlinienanweisungen für Governance

Die folgenden sechs Schritte helfen Ihnen dabei, Governancerichtlinien zum Steuern der Bereitstellung und Konfiguration von Ressourcen in Ihrer Cloudumgebung zu definieren.

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
                        <h3>Vorlage zur Disziplin „Beschleunigung der Bereitstellung“</h3>
                        <p class="x-hidden-focus">Laden Sie die Vorlage zum Dokumentieren einer Disziplin vom Typ „Beschleunigung der Bereitstellung“ herunter.</p>
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
                        <p class="x-hidden-focus">Machen Sie sich mit den Motiven und Risiken vertraut, die häufig mit der Disziplin „Beschleunigung der Bereitstellung“ verbunden sind.</p>
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
                        <p class="x-hidden-focus">Indikatoren, die Aufschluss darüber geben, ob jetzt der richtige Zeitpunkt ist, in die Disziplin „Beschleunigung der Bereitstellung“ zu investieren.</p>
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
                        <p class="x-hidden-focus">Empfohlene Prozesse zur Unterstützung der Richtlinieneinhaltung in der Disziplin „Beschleunigung der Bereitstellung“.</p>
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
                        <p class="x-hidden-focus">Azure-Dienste, die zur Unterstützung der Disziplin „Beschleunigung der Bereitstellung“ implementiert werden können.</p>
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

<!-- markdownlint-enable MD033 -->
