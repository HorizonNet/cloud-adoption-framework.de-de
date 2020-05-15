---
title: Einrichten einer ersten Grundlage für die Cloud Governance
description: Verwenden Sie das Cloud Adoption Framework für Azure für Ihre ersten Schritte in die Cloud Governance, indem Sie eine erste Grundlage für die Cloud Governance einrichten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 7ce353a03c57e89800d65edc5cdfbdec8c53d092
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218491"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Einrichten einer ersten Grundlage für die Cloud Governance

Das Einrichten der Cloud Governance erfordert umfassende iterative Maßnahmen. Es ist eine große Herausforderung, ein effektives Gleichgewicht zwischen Geschwindigkeit und Kontrolle zu erreichen, insbesondere bei der Ausführung früher Methoden der Cloudeinführung. Anhand der Governancerichtlinien im Framework für die Cloudeinführung (Cloud Adoption Framework) können Sie ein solches Gleichgewicht über einen agilen Ansatz bei der Einführung sicherstellen.

Dieser Artikel bietet zwei Möglichkeiten, um eine erste Grundlage für die Governance zu schaffen. Beide Möglichkeiten stellen sicher, dass die Governancebeschränkungen skaliert und erweitert werden können, wenn der Einführungsplan implementiert wird und die Anforderungen klarer definiert werden. Standardmäßig nimmt die erste Grundlage eine Position der Isolierung und Kontrolle an. Zudem liegt der Schwerpunkt stärker auf der Ressourcenorganisation und weniger auf der Ressourcenkontrolle. Dieser einfache Ausgangspunkt wird als _Minimum Viable Product (MVP)_ für die Governance bezeichnet. Ziel des MVP ist es, Hindernisse für die Einrichtung einer ersten Governanceposition abzubauen und dann eine schnelle Reifung der Lösung zu ermöglichen, um eine Vielzahl konkreter Risiken zu bewältigen.

## <a name="already-using-the-cloud-adoption-framework"></a>Das Cloud Adoption Framework wird bereits verwendet

Wenn Sie das Cloud Adoption Framework verfolgt haben, haben Sie möglicherweise bereits ein Governance-MVP bereitgestellt. Governance ist ein wichtiger Aspekt jedes Betriebsmodells. Sie ist in jeder Methode des Lebenszyklus der Cloudeinführung präsent. Als solches bietet das [Cloud Adoption Framework](../index.yml) eine Anleitung, die Governance in Aktivitäten in Bezug auf die Implementierung Ihres [Cloudeinführungsplans](../plan/index.md) einführt. Ein Beispiel für diese Governanceintegration ist die Verwendung von Blaupausen zum Bereitstellen einer oder mehrerer Zielzonen, die im Leitfaden zur [Bereitschaftsmethodik](../ready/index.md) zu finden sind. Ein weiteres Beispiel ist die Anleitung zum [horizontalen Skalieren von Abonnements](../ready/azure-best-practices/scale-subscriptions.md). Wenn Sie eine dieser Empfehlungen befolgt haben, sind die folgenden MVP-Abschnitte als einfache Übersicht über Ihre bereits getroffenen Bereitstellungsentscheidungen zu erachten. Wechseln Sie nach einer kurzen Überprüfung zum [Ausreifen der anfänglichen Governancelösung und Anwenden von Kontrollen für bewährte Methoden](./foundation-improvements.md).

## <a name="establish-an-initial-governance-foundation"></a>Einrichten einer ersten Grundlage für die Governance

Im Folgenden werden zwei verschiedene Beispiele für anfängliche Governancegrundlagen (die auch als Governance-MVPs bezeichnet werden) aufgeführt, um eine solide Grundlage für die Governance bei neuen oder bestehenden Bereitstellungen anzuwenden. Wählen Sie das MVP, das am besten zu Ihren Geschäftsanforderungen passt, für die ersten Schritte aus:

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./guides/standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Standardgovernanceleitfaden</h3>
                        <p>Ein für die meisten Organisationen geeigneter Leitfaden auf Grundlage des empfohlenen anfänglichen Modells mit zwei Abonnements, der für Bereitstellungen in mehreren Regionen konzipiert ist, aber nicht für öffentliche Clouds und Sovereign/Government Clouds gilt.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./guides/complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Governanceleitfaden für komplexe Unternehmen</h3>
                        <p>Ein Leitfaden für Unternehmen, die über mehrere unabhängige IT-Geschäftseinheiten verwaltet werden oder öffentliche Clouds und Sovereign/Government Clouds umfassen.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nächste Schritte

Sobald eine Governancegrundlage vorhanden ist, wenden Sie geeignete Empfehlungen an, um die Lösung zu verbessern und sich vor konkreten Risiken zu schützen.

> [!div class="nextstepaction"]
> [Verbessern der anfänglichen Governancegrundlage](./foundation-improvements.md)
