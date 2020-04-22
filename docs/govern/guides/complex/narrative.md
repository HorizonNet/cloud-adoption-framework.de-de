---
title: 'Governance in komplexen Unternehmen: Unterstützende Geschichte'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um im Rahmen der Cloudeinführung für Ihr komplexes Unternehmen einen Governance-Anwendungsfall einzurichten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: da021a6e1a4467189d20d3cb05e7ccdbb0b5a3b6
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80995402"
---
<!-- cSpell:ignore CDO's CIO's -->

# <a name="governance-guide-for-complex-enterprises-the-supporting-narrative"></a>Governanceleitfaden für komplexe Unternehmen: Unterstützende Geschichte

Die folgende Geschichte schildert einen Anwendungsfall für die [Governance während der Journey zur Cloudeinführung eines komplexen Unternehmens](./index.md). Bevor Sie die Empfehlungen in diesem Leitfaden umsetzen, müssen Sie die Annahmen und die Logik verstehen, die in dieser Geschichte dargestellt werden. So können Sie die Governancestrategie besser auf die Journey zur Cloudeinführung in Ihrer eigenen Organisation ausrichten.

## <a name="back-story"></a>Hintergrund

Bei der Interaktion mit diesem Unternehmen verlangen Kunden nach mehr Benutzerfreundlichkeit. Die aktuelle Oberfläche führte zum Marktzerfall und hat den Vorstand zur Einstellung eines Chief Digital Officer (CDO) veranlasst. Der CDO arbeitet mit den Abteilungen für Marketing und Vertrieb, um eine digitale Transformation voranzutreiben und ein besseres Benutzererlebnis zu ermöglichen. Darüber hinaus habe mehrere Unternehmenseinheiten vor kurzem Data Scientists eingestellt, um Daten zu pflegen und zahlreiche manuelle Funktionen durch Lernen und Vorhersagen zu verbessern. Die IT-Abteilung unterstützt diese Aktivitäten so umfassend wie möglich. Es gibt jedoch „Schatten-IT-Aktivitäten“, die außerhalb der erforderlichen Governance- und Sicherheitskontrollen stattfinden.

Außerdem hat die IT-Organisation ihre eigenen Herausforderungen zu meistern. Die Finanzabteilung plant Kürzungen des IT-Budgets in den nächsten fünf Jahren, die ab diesem Jahr zu Einschnitten in den Ausgaben führen. Im Gegensatz dazu zwingen DSGVO und andere Anforderungen an die Datenhoheit die IT-Abteilung zu Investitionen in Ressourcen in weiteren Ländern, um Daten lokalisieren zu lassen. In zwei der bestehenden Rechenzentren sind Hardwareaktualisierungen überfällig, was zu Problemen bei der Zufriedenheit von Mitarbeitern und Kunden führt. Für drei weitere Rechenzentren sind Hardwareaktualisierungen im Rahmen der Ausführung des Fünf-Jahres-Plans erforderlich. Der Leiter der Finanzabteilung (CFO) drängt die Leiterin der IT-Abteilung (CIO) dazu, die Cloud als Alternative für diese Rechenzentren in Betracht zu ziehen, um Kapital freizugeben.

Die CIO hat innovative Ideen, die dem Unternehmen helfen können, ist jedoch zusammen mit ihren Teams damit ausgelastet, akute Brände zu löschen und Kosten zu kontrollieren. Bei einem Mittagessen mit dem CDO und einem der Leiter einer Unternehmenseinheit konnte die CIO im Gespräch über die Cloudmigration das Interesse der beiden Kollegen wecken. Die drei Führungskräfte möchten sich mithilfe der Cloud gegenseitig dabei unterstützen, ihre Geschäftsziele zu erreichen, und haben die Untersuchungs- und die Planungsphase der Cloudeinführung eingeleitet.

## <a name="business-characteristics"></a>Geschäftsmerkmale

Das Unternehmen besitzt das folgende Geschäftsprofil:

- Vertrieb und Betrieb erstrecken sich geografisch über mehrere Bereiche mit Kunden in mehreren globalen Märkten.
- Das Unternehmen ist durch eine Übernahme gewachsen und in drei Unternehmenseinheiten tätig, die auf dem Zielkundenstamm beruhen. Die Budgetierung entspricht einer komplexen Matrix für Unternehmenseinheiten und Funktionen.
- Das Unternehmen betrachtet den größten Teil der IT als Kostenverursacher oder Kostenstelle.

## <a name="current-state"></a>Aktueller Status

Aktuell befinden sich IT und Cloudbetrieb des Unternehmens in folgendem Zustand:

- Die IT betreibt auf der ganzen Welt mehr als 20 Rechenzentren in Privatbesitz.
- Aufgrund des natürlichen Wachstums und mehrere geografische Regionen gibt es nur wenige IT-Teams mit eindeutigen Anforderungen für Datenhoheit und Compliance für eine einzelne Geschäftseinheit innerhalb einer bestimmten geografischen Region.
- Jedes Rechenzentrum ist über einer Reihe regionaler Standleitungen verbunden und erstellt so ein lose gekoppeltes globale WAN.
- Die IT hat die Cloud eingeführt, indem alle E-Mail-Konten der Endbenutzer zu Office 365 migriert wurden. Diese Migration wurde vor mehr als sechs Monaten abgeschlossen. Seit damals wurden nur wenige IT-Ressourcen in der Cloud bereitgestellt.
- Das primäre Entwicklungsteam des CDO arbeitet in einer Dev/Test-Kapazität, um die nativen Cloudfunktionen kennenzulernen.
- Eine Unternehmenseinheit experimentiert mit Big Data in der Cloud. Das BI-Team innerhalb der IT ist an diesen Bestrebungen beteiligt.
- Die vorhandene IT-Governancerichtlinie sieht vor, dass personenbezogene Kundeninformationen und Finanzdaten auf Ressourcen zu hosten sind, die dem Unternehmen direkt gehören. Diese Richtlinie blockiert den Einstieg in die Cloud für unternehmenskritische Apps oder geschützte Daten.
- IT-Investitionen werden größtenteils durch Kapitalkosten gesteuert. Diese Investitionen werden jährlich geplant und umfassen häufig Pläne für die laufende Wartung sowie festgelegte Aktualisierungszyklen von drei bis fünf Jahren, je nach Rechenzentrum.
- Die meisten Investitionen in Technologie, die dem Jahresplan nicht entsprechen, werden durch Schatten-IT-Aktivitäten getätigt. Dieser Aufwand wird normalerweise von Unternehmenseinheiten verwaltet und durch die Betriebskosten der Unternehmenseinheit abgedeckt.

## <a name="future-state"></a>Zukünftiger Status

Die folgenden Änderungen werden in den nächsten Jahren erwartet:

- Die CIO leitet eine Maßnahme zum Modernisieren der Richtlinie zu personenbezogenen Informationen und Finanzdaten, um zukünftige Ziele zu unterstützen. Zwei Mitgliedern des IT-Governanceteams sind in diese Bemühungen involviert.
- Der IT-Abteilungsleiter möchte die Cloudmigration als richtungsweisend verstanden wissen, um die Konsistenz und Stabilität für alle Geschäftseinheiten und geografischen Regionen zu verbessern. Allerdings muss der zukünftige Status externe Complianceanforderungen berücksichtigen, die eine Abkehr von den bestehenden Ansätzen bestimmter IT-Teams erfordern.
- Wenn die frühen Experimente in den Bereichen App-Entwicklung und BI erfolgsversprechend sind, sollen in den nächsten 24 Monaten jeweils kleine Produktionslösungen in der Cloud freigegeben werden.
- Die CIO und der CFO haben einen Architekten und den Vice President of Infrastructure beauftragt, eine Kostenanalyse und eine Machbarkeitsstudie anzufertigen. Diese Bemühungen werden entscheiden, ob das Unternehmen in den nächsten 36 Monaten 5.000 Ressourcen in die Cloud verschieben kann und soll. Durch eine erfolgreiche Migration kann die CIO zwei Rechenzentren aufgeben und damit die Kosten im Laufe des Fünf-Jahres-Plans um mehr als 100 Millionen US-Dollar senken. Wenn drei bis vier Rechenzentren ähnliche Ergebnisse erzielen können, ist das Budget wieder in den schwarzen Zahlen und ermöglicht der CIO die Unterstützung weiterer innovativer Initiativen.
    ![Lokale Kosten im Vergleich zu Azure-Kosten zeigen eine Rendite von 100 Millionen USD in den nächsten fünf Jahren.](../../../_images/govern/calculator-enterprise.png)
- Neben diesen Kosteneinsparungen plant das Unternehmen, die Verwaltung einiger IT-Investitionen zu ändern, indem die gebundenen Kapitalkosten als Betriebskosten innerhalb der IT umdefiniert werden. Diese Änderung ermöglicht mehr Kostenkontrolle, sodass die IT weitere geplante Aufwendungen beschleunigen kann.

## <a name="next-steps"></a>Nächste Schritte

Das Unternehmen hat eine Unternehmensrichtlinie zur Gestaltung der Governance-Implementierung entwickelt. Die Unternehmensrichtlinie steuert zahlreiche technische Entscheidungen.

> [!div class="nextstepaction"]
> [Anfängliche Unternehmensrichtlinie ansehen](./initial-corporate-policy.md)
