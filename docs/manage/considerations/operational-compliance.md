---
title: Betriebsbezogene Compliance in der Cloudverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie die Compliance in Bezug auf betriebsbezogene Zusagen sicherstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 894208ff08a0100e8d5d8d5d9df3eff592773426
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340977"
---
# <a name="operational-compliance-in-cloud-management"></a>Betriebsbezogene Compliance in der Cloudverwaltung

Die betriebsbezogene Compliance baut auf der Disziplin [Bestand und Transparenz](./inventory.md) auf. Diese Disziplin konzentriert sich als erster umsetzbarer Schritt der Cloudverwaltung auf regelmäßige Telemetrieüberprüfungen und Korrekturmaßnahmen (sowohl proaktiv als auch reaktiv). Diese Disziplin ist der Grundstein, auf dem das Gleichgewicht zwischen Sicherheit, Governance, Leistung und Kosten basiert.

## <a name="components-of-operations-compliance"></a>Komponenten der betriebsbezogenen Compliance

Die Einhaltung betriebsbezogener Zusagen erfordert Analysen, Automatisierung und Korrekturmaßnahmen durch Menschen. Eine effektive betriebsbezogene Compliance erfordert Konsistenz in einigen kritischen Prozessen:

- Ressourcenkonsistenz
- Umgebungskonsistenz
- Konsistenz der Ressourcenkonfiguration
- Konsistenz bei Updates
- Automatisierung von Korrekturmaßnahmen

### <a name="resource-consistency"></a>Ressourcenkonsistenz

Der effektivste Schritt, den ein Cloudverwaltungsteam unternehmen kann, um die betriebsbezogene Compliance sicherzustellen, besteht darin, Konsistenz bei der Organisation und Kennzeichnung von Ressourcen herzustellen. Wenn Ressourcen konsistent organisiert und gekennzeichnet werden, lassen sich alle anderen operativen Aufgaben leichter bewältigen. Detaillierte Informationen zur Ressourcenkonsistenz finden Sie im Artikel zur [Governancephase](../../govern/index.md) des Lebenszyklus einer Cloudeinführung. Die Artikel zu den [ersten Grundlagen für die Governance](../../govern/initial-foundation.md) veranschaulichen, wie mit der Entwicklung der Ressourcenkonsistenz begonnen werden kann.

### <a name="environment-consistency"></a>Umgebungskonsistenz

Das Einrichten konsistenter Umgebungen – auch als „Landezonen“ bezeichnet – ist der zweitwichtigste Schritt auf dem Weg zur betriebsbezogenen Compliance. Wenn Landezonen konsistent sind und mit automatisierten Tools durchgesetzt werden, sind Diagnose und Lösung von betriebsbezogenen Problemen wesentlich weniger komplex. Detaillierte Informationen zur Umgebungskonsistenz finden Sie in der Phase [Bereit](../../ready/index.md) des Lebenszyklus einer Cloudeinführung. Die Aufgaben in dieser Phase helfen beim Einrichten eines wiederholbaren Prozesses zum Definieren und Weiterentwickeln eines konsistenten „Code First“-Ansatzes für die Entwicklung cloudbasierter Umgebungen.

### <a name="resource-configuration-consistency"></a>Konsistenz der Ressourcenkonfiguration

Die Cloudverwaltung baut auf den Ansätzen für Governance und Bereitschaft auf und sollte Prozesse für die fortlaufende Überwachung und Bewertung der Einhaltung von Anforderungen an die Ressourcenkonsistenz enthalten. Wenn sich Workloads ändern oder neue Versionen eingeführt werden, ist es von entscheidender Bedeutung, dass Cloudverwaltungsprozesse alle Konfigurationsänderungen auswerten – dies lässt sich nicht einfach durch Automatisierung erreichen.

Wenn Inkonsistenzen entdeckt werden, lassen sich einige durch Konsistenz bei Updates beheben, andere werden möglicherweise automatisch korrigiert.

### <a name="update-consistency"></a>Konsistenz bei Updates

Stabilität im Ansatz kann zu stabileren Vorgängen führen. Dennoch sind bei Cloudverwaltungsprozessen immer wieder Änderungen erforderlich. Insbesondere sind regelmäßige Patches und Leistungsänderungen unabdingbar, um Unterbrechungen zu reduzieren und die Kosten zu senken.

Einer der vielen Vorteile einer ausgereiften Cloudverwaltungsmethodik besteht darin, sich auf die Stabilisierung und Steuerung notwendiger Änderungen zu konzentrieren.

Jede Cloudverwaltungsbaseline sollte eine Möglichkeit enthalten, notwendige Updates zu planen, zu steuern und ggf. zu automatisieren. Diese Updates sollten mindestens Patches umfassen, können jedoch auch auf Leistung, Größenanpassung und andere Aspekte der Aktualisierung von Ressourcen erstrecken.

### <a name="remediation-automation"></a>Automatisierung von Korrekturmaßnahmen

Als erweiterte Baseline für die Cloudverwaltung können einige Workloads möglicherweise von automatisierten Korrekturmaßnahmen profitieren. Wenn bei einer Workload häufig Probleme auftreten, die sich nicht durch eine Änderung am Code oder an der Architektur lösen lassen, kann eine Automatisierung von Korrekturmaßnahmen die Belastung des Cloudverwaltungsteams verringern und die Benutzerzufriedenheit erhöhen.

Hier lässt sich argumentieren, dass ein Problem, das häufig genug auftritt, um eine Automatisierung zu erfordern, durch die Beseitigung technischer Schulden gelöst werden muss. Wenn eine langfristige Lösung gewünscht ist, sollte dies die Standardoption sein. Eine Reihe von geschäftlichen Szenarien gestalten es schwierig, umfassende Investitionen zur Beseitigung technischer Schulden zu rechtfertigen. Wenn eine solche Beseitigung nicht gerechtfertigt werden kann, Korrekturmaßnahmen aber eine häufige und kostspielige Belastung sind, ist eine automatisierte Korrektur die zweitbeste Lösung.

## <a name="next-steps"></a>Nächste Schritte

[Schutz und Wiederherstellung](./protect.md) sind die nächsten Bereiche, die bei einer Baseline für die Cloudverwaltung zu berücksichtigen sind.

> [!div class="nextstepaction"]
> [Schutz und Wiederherstellung](./protect.md)
