---
title: Bestand und Transparenz in Azure
description: Es wird beschrieben, was verwaltet wird (Bestand) und wie sich die verwalteten Workloads und Ressourcen im Laufe der Zeit ändern (Transparenz).
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c9057c84757c49457b46c310d239dc8c49bd50d0
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341221"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Bestand und Transparenz bei der Cloudverwaltung

Die Betriebsverwaltung weist eine klare Abhängigkeit von Daten auf. Eine einheitliche Verwaltung erfordert ein Verständnis dessen, was verwaltet wird (Bestand) und wie sich diese verwalteten Workloads und Ressourcen im Laufe der Zeit ändern (Transparenz). Eindeutige Einblicke in den Bestand und die Transparenz helfen dem Team, die Umgebung effektiv zu verwalten. Alle anderen Betriebsführungsaktivitäten und -prozesse bauen auf diesen beiden Bereichen auf.

Ein paar klassische Aussagen zur Bedeutung von Messungen geben den Ton für diesen Artikel vor:

- Verwalten, worauf es ankommt.
- Sie können nur das verwalten, was Sie messen können.
- Wenn Sie es nicht messen können, ist es möglicherweise unerheblich.

Die Fachrichtung „Bestand und Transparenz“ setzt auf diesen zeitlosen Aussagen auf. Bevor Sie Betriebsführungsprozesse effektiv festlegen können, ist es wichtig, Daten zu sammeln und das richtige Maß an Transparenz für die jeweiligen Teams zu schaffen.

## <a name="common-customer-challenges"></a>Gängige Herausforderungen für Kunden

Wenn Bestands- und Transparenzprozesse nicht konsequent umgesetzt werden, können Betriebsführungsteams unter einem höheren Volumen an Betriebsunterbrechungen, einem längeren Zeitraum bis zur Wiederherstellung und einem höheren Aufwand für die Suche und Behebung von Fehlern leiden. Da sich Änderungen negativ auf Anwendungen mit höherer Priorität und eine größere Anzahl von Ressourcen auswirken, wächst jede dieser Metriken noch schneller an.

Diese Herausforderungen ergeben sich aus einer kleinen Anzahl von Fragen, die nur mittels einheitlicher Daten und Telemetrie beantwortet werden können:

- Inwiefern weicht die aktuelle Leistung von den üblichen Telemetriedaten zur Betriebsleistung ab?
- Welche Ressourcen verursachen die Betriebsunterbrechungen auf Workloadebene?
- Welche Ressourcen müssen korrigiert werden, um zu einer akzeptablen Leistung dieser Workloads oder Geschäftsprozesse zurückzukehren?
- Wann hat die Abweichung eingesetzt? Was war der Auslöser?
- Welche Änderungen wurden an den zugrunde liegenden Ressourcen vorgenommen? Von wem?
- Waren die Änderungen beabsichtigt? Hatten sie einen böswilligen Hintergrund?
- Wie haben sich Änderungen auf die Leistungstelemetriedaten ausgewirkt?

Es ist schwierig, wenn nicht sogar unmöglich, diese Fragen ohne eine umfangreiche, zentralisierte Quelle für Protokolle und Telemetriedaten zu beantworten. Zum Ermöglichen der Cloudverwaltung durch Sicherstellen einer einheitlichen Konfiguration, die für die Zentralisierung der Daten erforderlich ist, muss der Baselinedienst zunächst mit der Definition der Prozesse beginnen. Die Prozesse müssen erfassen, wie eine derartige Konfiguration die Datenerfassung erzwingt, um die Komponenten von Bestand und Transparenz im nächsten Abschnitt zu unterstützen.

## <a name="components-of-inventory-and-visibility"></a>Komponenten von Bestand und Transparenz

Die Schaffung von Transparenz auf jeder Cloudplattform erfordert einige wesentliche Komponenten:

- Zuständigkeit und Transparenz
- Inventory
- Zentrale Protokollierung
- Änderungsnachverfolgung
- Leistungstelemetriedaten

### <a name="responsibility-and-visibility"></a>Zuständigkeit und Transparenz

Wenn Sie die Verpflichtungen für die einzelnen Workloads festlegen, ist [Zuständigkeit für die Verwaltung](./commitment.md#management-responsibility) ein entscheidender Faktor. Durch Delegieren von Zuständigkeit entsteht die Notwendigkeit delegierter Transparenz. Der erste Schritt in Bezug auf Bestand und Transparenz besteht darin, sicherzustellen, dass die Zuständigen Zugang zu den richtigen Daten haben. Bevor Sie cloudbasierte Tools für Transparenz implementieren, stellen Sie sicher, dass jedes Überwachungstool für jedes Betriebsteam mit dem richtigen Zugriff und Geltungsbereich konfiguriert wurde.

### <a name="inventory"></a>Inventory

Wenn niemand weiß, dass eine Ressource existiert, ist es schwierig, sie zu verwalten. Bevor eine Ressource oder Workload verwaltet werden kann, muss sie in einer Bestandsaufnahme erfasst und klassifiziert werden. Der erste technische Schritt zu einem stabilen Betrieb ist die Prüfung des Bestands und dessen Klassifizierung.

### <a name="central-logging"></a>Zentrale Protokollierung

Die zentralisierte Protokollierung ist entscheidend für die Transparenz, die von den Betriebsführungsteams Tag für Tag benötigt wird. Für alle in der Cloud bereitgestellten Ressourcen sollten Protokolle an einem zentralen Ort gespeichert werden. In Azure ist Log Analytics der zentrale Speicherort. Die Zentralisierung der Protokollierung ermöglicht Berichte zu den Themen Change Management, Dienstintegrität, Konfiguration und den meisten anderen Aspekten des IT-Betriebs.

Das Erzwingen der konsequenten Nutzung der zentralen Protokollierung ist der erste Schritt zum Einrichten wiederholbarer Vorgänge. Die Erzwingung kann durch die Unternehmensrichtlinie erreicht werden. Wenn möglich, sollte die Erzwingung jedoch automatisiert werden, um Einheitlichkeit zu gewährleisten.

### <a name="change-tracking"></a>Änderungsnachverfolgung

Änderungen sind die eine Konstante in einer IT-Umgebung. Ein Bewusstsein für und Verständnis von Änderungen in mehreren Workloads ist für einen zuverlässigen Betrieb unerlässlich. Jede Cloudverwaltungslösung muss ein Mittel zum Nachvollziehen des Wann, Wie und Warum technischer Änderungen bieten. Ohne diese Datenpunkte werden Korrekturmaßnahmen erheblich beeinträchtigt.

### <a name="performance-telemetry"></a>Leistungstelemetriedaten

Verpflichtungen gegenüber den Fachbereichen bei Cloudverwaltung werden von Daten gesteuert. Um Verpflichtungen ordnungsgemäß einzuhalten, muss das Cloudbetriebsteam zunächst die Telemetriedaten hinsichtlich Stabilität, Leistung und Betrieb der Workload sowie der Ressourcen zur Unterstützung der Workload verstehen.

Die aktuelle Integrität und der Betrieb von Netzwerk, DNS, Betriebssystemen und anderen grundlegenden Aspekten der IT-Umgebung sind kritische Datenpunkte, die in die allgemeine Integrität jeder Workload einfließen.

## <a name="processes"></a>Prozesse

Vielleicht noch mehr als die Features der Cloudverwaltungsplattform dienen Cloudverwaltungsprozesse zum Einhalten von Betriebsverpflichtungen gegenüber den Fachbereichen. Eine Cloudverwaltungsmethodik sollte mindestens die folgenden Prozesse umfassen:

- **Reaktive Überwachung:** Wer befasst sich, wenn sich Abweichungen negativ auf den Geschäftsbetrieb auswirken, mit diesen Abweichungen? Welche Maßnahmen werden ergriffen, um die Abweichungen zu beheben?
- **Proaktive Überwachung:** Wenn Abweichungen festgestellt werden, der Geschäftsbetrieb aber nicht beeinträchtigt wird, wie und von wem werden diese Abweichungen in Angriff genommen?
- **Berichte zu Verpflichtungen:** Wie wird die Einhaltung von geschäftlichen Verpflichtungen gegenüber den Beteiligten im Unternehmen vermittelt?
- **Budgetüberprüfungen:** Wie sieht der Prozess der Überprüfung dieser Verpflichtungen im Hinblick auf die budgetierten Kosten aus? Wie sieht der Prozess zur Anpassung der bereitgestellten Lösung oder der Verpflichtungen aus, um zu einer Übereinstimmung zu gelangen?
- **Eskalationspfade:** Welche Eskalationspfade sind verfügbar, wenn einer der vorherigen Prozesse nicht den Anforderungen der Fachbereiche entspricht?

Es gibt mehrere weitere Prozesse im Zusammenhang mit Bestand und Transparenz. Die vorhergehende Liste soll das Betriebsteam zum Nachdenken anregen. Die Beantwortung dieser Fragen wird dazu beitragen, einige der notwendigen Prozesse zu entwickeln und wahrscheinlich neue, tiefgreifendere Fragen auszulösen.

## <a name="responsibilities"></a>Aufgaben

Wenn Sie Prozesse zur Betriebsüberwachung entwickeln, ist es ebenso wichtig, Zuständigkeiten für den täglichen Betrieb und die regelmäßige Unterstützung der einzelnen Prozesse festzulegen.

In einer zentralen IT-Organisation bietet die IT das betriebliche Know-how. Die Fachbereiche haben eine beratende Funktion, wenn die Behebung von Problemen erforderlich ist.

In einer Organisation mit Cloudkompetenzzentrum liefert die für den Geschäftsbetrieb zuständige Abteilung das Fachwissen und trägt die Verantwortung für die Steuerung dieser Prozesse. Die IT konzentriert sich auf die Automatisierung und Unterstützung von Teams, die die Umgebung betreiben.

Es gibt jedoch auch allgemeine Zuständigkeiten. Organisationen benötigen häufig eine Mischung von Zuständigkeiten, um Verpflichtungen gegenüber den Fachbereichen zu erfüllen.

## <a name="act-on-inventory-and-visibility"></a>Maßnahmen in Bezug auf Bestand und Transparenz

Unabhängig von der Cloudplattform kommen die fünf Komponenten in Bezug auf Bestand und Transparenz zum Einsatz, um die meisten Betriebsprozesse zu steuern. Alle nachfolgenden Fachrichtungen basieren auf den Daten, die erfasst werden. Die nächsten Artikel dieser Reihe zeigen Wege auf, wie Sie mit diesen Daten umgehen und andere Datenquellen integrieren können.

### <a name="share-visibility"></a>Teilen der Transparenz

Daten ohne entsprechende Maßnahmen bringen wenig Nutzen. Die Cloudverwaltung kann über cloudbasierte Tools und Prozesse hinausgehen. Um umfassendere Prozesse zu unterstützen, muss eine Baseline für die Cloudverwaltung möglicherweise um Berichterstellung, Integration von IT-Service-Management oder Datenzentralisierung erweitert werden. Die Cloudverwaltung muss in verschiedenen Phasen auf dem Weg zur betrieblichen Reife möglicherweise einen oder mehrere der folgenden Punkte berücksichtigen.

### <a name="report"></a>Bericht

Offlineprozesse und die Kommunikation über Verpflichtungen gegenüber den Fachbereichen erfordern oft die Erstellung von Berichten. Die Self-Service- oder regelmäßige Berichterstellung ist möglicherweise eine erforderliche Komponente einer erweiterten Verwaltungsbaseline.

### <a name="it-service-management-itsm-integration"></a>ITSM-Integration (IT-Service-Management)

Die ITSM-Integration ist oft das erste Beispiel für Maßnahmen in Bezug auf Bestand und Transparenz. Wenn Abweichungen von erwarteten Leistungsmustern auftreten, verwendet die ITSM-Integration Warnmeldungen der Cloudplattform, um Tickets in einem separaten Service-Management-Tool zum Einleiten von Abhilfemaßnahmen auszulösen. Einige Betriebsmodelle erfordern ggf. die ITSM-Integration als Aspekt der erweiterten Verwaltungsbaseline.

### <a name="data-centralization"></a>Zentralisierung von Daten

Es gibt eine Vielzahl von Gründen, warum ein Unternehmen mehrere Mandanten innerhalb eines einzigen Cloudanbieters benötigen kann. In diesen Szenarien ist die Zentralisierung der Daten ein notwendiger Bestandteil der erweiterten Baseline zur Verwaltung, da sie bei allen dieser Mandanten oder Umgebungen Transparenz bereitstellen kann.

## <a name="next-steps"></a>Nächste Schritte

Betriebsbezogene Compliance basiert auf Bestandsfunktionen, indem Verwaltungsautomatisierung und -kontrollen zum Einsatz kommen. Erfahren Sie, wie [betriebsbezogene Compliance](./operational-compliance.md) Ihren Prozessen zugeordnet wird.

> [!div class="nextstepaction"]
> [Planen der betriebsbezogenen Compliance](./operational-compliance.md)
