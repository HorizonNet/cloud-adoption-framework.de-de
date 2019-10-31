---
title: 'Betriebsbezogene Compliance: Cloudverwaltung und -betrieb'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Betriebsbezogene Compliance: Cloudverwaltung und -betrieb'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: bb6e4584da87d992f85b6ce90e21081c9c19d7c3
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682544"
---
# <a name="operational-compliance-in-cloud-management"></a>Betriebsbezogene Compliance in der Cloudverwaltung

Die betriebsbezogene Compliance baut auf der Disziplin [Bestand und Transparenz](./inventory.md) auf und ist der erste umsetzbare Schritt der Cloudverwaltung. In dieser Disziplin geht es um regelmäßige Telemetrieüberprüfungen und Korrekturmaßnahmen (sowohl proaktiv als auch reaktiv). Diese Disziplin ist der Grundstein, auf dem das Gleichgewicht zwischen Sicherheit, Governance, Leistung und Kosten basiert.

## <a name="components-of-operations-compliance"></a>Komponenten der betriebsbezogenen Compliance

Die Einhaltung betriebsbezogener Zusagen erfordert Analysen, Automatisierung und Korrekturmaßnahmen durch Menschen. Eine effektive betriebsbezogene Compliance erfordert Konsistenz in einigen kritischen Prozessen:

1. Ressourcenkonsistenz
2. Umgebungskonsistenz
3. Konsistenz der Ressourcenkonfiguration
4. Konsistenz bei Updates
5. Automatisierung von Korrekturmaßnahmen

### <a name="resource-consistency"></a>Ressourcenkonsistenz

Der effektivste Schritt, den ein Cloudverwaltungsteam unternehmen kann, um die betriebsbezogene Compliance sicherzustellen, besteht darin, Konsistenz bei der Organisation und Kennzeichnung von Ressourcen herzustellen. Wenn Ressourcen konsistent organisiert und gekennzeichnet werden, lassen sich alle anderen operativen Aufgaben leichter bewältigen. Detaillierte Informationen zur Ressourcenkonsistenz finden Sie im Artikel zur [Governancephase](../../govern/index.md) des Lebenszyklus einer Cloudeinführung. Die Artikel zu den [ersten Grundlagen für die Governance](../../govern/initial-foundation.md) enthalten Beispiele dafür, wie mit der Entwicklung der Ressourcenkonsistenz begonnen werden kann.

### <a name="environment-consistency"></a>Umgebungskonsistenz

Konsistente Umgebungen – auch als „Landezonen“ bezeichnet – sind der zweitwichtigsten Schritt auf dem Weg zur betriebsbezogenen Compliance. Wenn Landezonen konsistent sind und mit automatisierten Tools durchgesetzt werden, sind Diagnose und Lösung von betriebsbezogenen Problemen wesentlich weniger komplex. Detaillierte Informationen zur Umgebungskonsistenz finden Sie in der Phase [Bereit](../../ready/index.md) des Lebenszyklus einer Cloudeinführung. Die Aufgaben in dieser Phase richten einen wiederholbaren Prozess zum Definieren und Weiterentwickeln eines konsistenten Code First-Ansatzes für die Entwicklung cloudbasierter Umgebungen ein.

### <a name="resource-configuration-consistency"></a>Konsistenz der Ressourcenkonfiguration

Die Cloudverwaltung baut auf den Ansätzen für Governance und Bereitschaft auf und sollte Prozesse für die fortlaufende Überwachung und Bewertung der Einhaltung von Anforderungen an die Ressourcenkonsistenz enthalten. Wenn sich Workloads ändern oder neue Versionen eingeführt werden, ist es von entscheidender Bedeutung, dass Cloudverwaltungsprozesse alle Konfigurationsänderungen auswerten – dies lässt sich nicht einfach durch automatisierte Methoden erreichen.

Wenn Inkonsistenzen entdeckt werden, lassen sich einige durch Konsistenz bei Updates beheben, andere werden möglicherweise automatisch korrigiert.

### <a name="update-consistency"></a>Konsistenz bei Updates

Stabilität sorgt für einen stabilen Betrieb. Dennoch sind bei Cloudverwaltungsprozessen immer wieder Änderungen erforderlich. Insbesondere sind regelmäßige Patches und Leistungsänderungen unabdingbar, um Unterbrechungen zu reduzieren und die Kosten zu senken.

Einer der vielen Vorteile einer ausgereiften Cloudverwaltungsmethodik besteht darin, notwendige Veränderungen zu stabilisieren und zu steuern.

Jede Cloudverwaltungsbaseline sollte eine Möglichkeit enthalten, notwendige Updates zu planen, zu steuern und ggf. zu automatisieren. Diese Updates sollten mindestens Patches umfassen, können jedoch auch auf Leistung, Größenanpassung und andere Aspekte der Aktualisierung von Ressourcen erstrecken.

### <a name="remediation-automation"></a>Automatisierung von Korrekturmaßnahmen

Als erweiterte Baseline für die Cloudverwaltung können einige Workloads möglicherweise von automatisierten Korrekturmaßnahmen profitieren. Wenn bei einer Workload häufig Probleme auftreten, die sich nicht durch eine Änderung am Code oder an der Architektur lösen lassen, kann eine Automatisierung von Korrekturmaßnahmen die Belastung des Cloudverwaltungsteams verringern und die Benutzerzufriedenheit erhöhen.

Hier lässt sich argumentieren, dass ein Problem, das häufig genug auftritt, um eine Automatisierung zu erfordern, durch die Beseitigung technischer Schulden gelöst werden muss. Wenn eine langfristige Lösung gewünscht ist, sollte dies die Standardoption sein. Es gibt jedoch eine Vielzahl von geschäftlichen Szenarien, in denen umfassende Investitionen zur Beseitigung technischer Schulden nur schwer zu rechtfertigen sind. Wenn eine solche Beseitigung nicht gerechtfertigt werden kann, Korrekturmaßnahmen aber eine häufige und kostspielige Belastung sind, ist eine automatisierte Korrektur die zweitbeste Lösung.

## <a name="next-steps"></a>Nächste Schritte

[Schutz und Wiederherstellung](./protect.md) sind die nächsten Bereiche, die bei einer Baseline für die Cloudverwaltung zu berücksichtigen sind.

> [!div class="nextstepaction"]
> [Schutz und Wiederherstellung](./protect.md)
