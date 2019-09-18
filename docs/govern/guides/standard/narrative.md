---
title: 'Standardunternehmensleitfaden: Die Geschichte hinter der Governancestrategie'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diese Geschichte schildert einen Anwendungsfall für die Governance während der Journey zur Cloudeinführung eines Standardunternehmens.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 434a4d0238a4633210d31013e9787c3a0a92fc7a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032258"
---
# <a name="standard-enterprise-guide-the-narrative-behind-the-governance-strategy"></a>Standardunternehmensleitfaden: Die Geschichte hinter der Governancestrategie

Die folgende Geschichte schildert einen Anwendungsfall für die Governance während der [Journey zur Cloudeinführung eines Standardunternehmens](./index.md). Vor der Implementierung der Vorgehensweise ist es wichtig, die Annahmen und die Logik zu verstehen, die in dieser Geschichte dargestellt werden. So können Sie die Governancestrategie besser auf die Journey in Ihrer eigenen Organisation ausrichten.

## <a name="back-story"></a>Hintergrund

Die Unternehmensleitung stellte Anfang des Jahres Pläne vor, um dem Business mit verschiedenen Ansätzen neue Impulse zu geben. Sie macht Druck, damit das Kundenerlebnis verbessert wird und das Unternehmen Marktanteile gewinnt. Sie möchte auch neue Produkte und Dienste anbieten, die das Unternehmen als Vordenker und Vorreiter in der Branche positionieren. Parallel dazu hat die Unternehmensleitung Verfahren initiiert, um Ressourcenverschwendung und unnötige Kosten zu vermeiden. Diese Aktionen scheinen auf den ersten Blick einschüchternd, zeigen aber, dass bei diesem Ansatz so viel Kapital wie möglich auf zukünftiges Wachstum konzentriert wird.

In der Vergangenheit war der CIO des Unternehmens von diesen strategischen Gesprächen ausgeschlossen. Da aber die Zukunftsvision untrennbar mit technischem Wachstum verbunden ist, wird die IT-Abteilung an der Entwicklung und Ausarbeitung dieser großen Pläne beteiligt. Die IT muss nun Lösungen und Support auf neue Weise bereitstellen. Das Team ist auf diese Veränderungen nicht vorbereitet und wird wahrscheinlich mit der Lernkurve zu kämpfen haben.

## <a name="business-characteristics"></a>Geschäftsmerkmale

Das Unternehmen besitzt das folgende Geschäftsprofil:

- Alle Vertriebs- und Betriebsprozesse werden in einem einzigen Land ausgeführt, es ist nur ein geringer Prozentsatz an globalen Kunden vorhanden.
- Das Unternehmen wird als einzelne Geschäftseinheit geführt, den einzelnen Funktionen – z.B. Vertrieb, Marketing, Betrieb und IT – sind Budgets zugeordnet.
- Das Unternehmen betrachtet den größten Teil der IT als Kostenverursacher oder Kostenstelle.

## <a name="current-state"></a>Aktueller Status

Aktuell weisen IT und Cloudbetrieb des Unternehmens folgenden Status auf:

- Die IT-Abteilung betreibt zwei gehostete Infrastrukturumgebungen. Eine Umgebung enthält Produktionsassets. Die zweite Umgebung enthält Funktionen für die Notfallwiederherstellung und einige Dev/Test-Assets. Diese Umgebungen werden von zwei verschiedenen Anbietern gehostet. Die IT bezeichnet diese beiden Rechenzentren als „Prod“ bzw. „DR“.
- Die IT hat die Cloud eingeführt, indem alle E-Mail-Konten der Endbenutzer zu Office 365 migriert wurden. Diese Migration wurde vor sechs Monaten abgeschlossen. Es wurden nur wenige andere IT-Ressourcen in der Cloud bereitgestellt.
- Die Anwendungsentwicklungsteams arbeiten in einer Dev/Test-Funktion, um die nativen Cloudfunktionen kennenzulernen.
- Das BI-Team (Business Intelligence) experimentiert mit Big Data in der Cloud und einer kuratierten Zusammenstellung der Daten auf neuen Plattformen.
- Das Unternehmen hat eine nicht sehr strikt formulierte Richtlinie, dass personenbezogene Informationen von Kunden und Finanzdaten nicht in der Cloud gehostet werden dürfen, was unternehmenskritische Anwendungen in den aktuellen Bereitstellungen einschränkt.
- IT-Investitionen werden größtenteils durch Kapitalkosten gesteuert. Diese Investitionen werden jährlich geplant. In den vergangenen Jahren umfassten die Investitionen wenig mehr als die grundlegenden Wartungsanforderungen.

## <a name="future-state"></a>Zukünftiger Status

Die folgenden Änderungen werden in den nächsten Jahren erwartet:

- Der CIO überprüft die Richtlinie zu personenbezogenen Informationen und Finanzdaten, damit diese den zukünftigen Status unterstützt.
- Die Teams für Anwendungsentwicklung und Business Intelligence möchten in den nächsten 24 Monaten cloudbasierte Lösungen in die Produktion bringen – basierend auf der Vision in Bezug auf Kundenbindung und neue Produkte.
- In diesem Jahr schließt das IT-Team die Außerbetriebnahme der Workloads für die Notfallwiederherstellung im Rechenzentrum „DR“ ab, in dem 2.000 VMs in die Cloud migriert werden. Durch diese Maßnahme wird in den nächsten fünf Jahren mit einer Kostenersparnis von 25 Mio. USD gerechnet.
    ![Lokale Kosten im Vergleich zu Azure-Kosten zeigen eine Rendite von 25 Millionen USD in den nächsten fünf Jahren.](../../../_images/govern/calculator-small-to-medium-enterprise.png)
- Das Unternehmen plant, einige IT-Investitionen zu ändern, indem die gebundenen Kapitalkosten als Betriebskosten innerhalb der IT umdefiniert werden. Diese Änderung ermöglicht mehr Kostenkontrolle, sodass die IT weitere geplante Aufwendungen beschleunigen kann.

## <a name="next-steps"></a>Nächste Schritte

Das Unternehmen hat eine Unternehmensrichtlinie zur Gestaltung der Governance-Implementierung entwickelt. Die Unternehmensrichtlinie steuert zahlreiche technische Entscheidungen.

> [!div class="nextstepaction"]
> [Anfängliche Unternehmensrichtlinie ansehen](./initial-corporate-policy.md)
