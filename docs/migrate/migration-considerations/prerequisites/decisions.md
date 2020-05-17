---
title: Entscheidungen, die sich auf die Migration auswirken
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um die richtigen Entscheidungen zu treffen und Ausführungsaktivitäten auszuwählen, die zu einer erfolgreichen Migration beitragen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: dd818e65e6f9064119b27dfb5ea87b8a04bda671
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222129"
---
<!-- cSpell:ignore migrateable -->

# <a name="decisions-that-affect-migration"></a>Entscheidungen, die sich auf die Migration auswirken

Während der Migration wirken sich mehrere Faktoren auf Entscheidungen und Ausführungsaktivitäten aus. In diesem Artikel wird das zentrale Thema dieser Entscheidungen erläutert. Außerdem werden einige Fragen untersucht, die durch die Besprechung von Migrationsprinzipien in diesem Abschnitt des Leitfadens für das Framework für die Cloudeinführung führen.

## <a name="business-outcomes"></a>Geschäftsergebnisse

Das Ziel einer Einführung kann einen wesentlichen Einfluss auf die empfohlene Vorgehensweise zur Ausführung haben.

- **Migration.** Dringende Geschäftsfaktoren, schnelle Einführung oder Kosteneinsparungen sind Beispiele für operative Ergebnisse. Diese Ergebnisse sind von zentraler Bedeutung für Bemühungen, die den Geschäftswert durch transitive Änderungen im IT-Bereich oder Betriebsmodelle steigern. Der Abschnitt „Migration“ des Framework für die Cloudeinführung konzentriert sich stark auf Geschäftsergebnisse, bei denen die Migration im Mittelpunkt steht.
- **Anwendungsinnovationen:** Die Verbesserung des Kundenerlebnisses und der wachsende Marktanteil sind Beispiele für inkrementelle Ergebnisse. Die Ergebnisse resultieren aus einer Sammlung von inkrementellen Änderungen, die sich auf die Bedürfnisse und Wünsche der aktuellen Kunden konzentrieren.
- **Datenbasierte Innovationen:** Neue Produkte oder Dienstleistungen, insbesondere solche, die sich durch die Leistungsfähigkeit von Daten ergeben, sind Beispiele für disruptive Ergebnisse. Diese Ergebnisse stammen von Experimenten und Vorhersagen, bei denen Daten zur Disruption des Status quo auf dem Markt verwendet werden.

Kein Unternehmen würde sich nur eines dieser Ergebnisse zum Ziel setzen. Ohne Betriebsvorgänge gibt es keine Kunden und umgekehrt. Die Cloudeinführung ist da keine Ausnahmen. Unternehmen arbeiten in der Regel daran, jedes dieser Ergebnisse zu erzielen, aber bei dem Versuch, sich auf alle gleichzeitig zu konzentrieren, können die Bemühungen im Einzelnen zu gering ausfallen und zu verlangsamten Fortschritten bei den Arbeiten führen, die den größten Nutzen für Ihre Geschäftsanforderungen bringen könnten.

Diese Voraussetzung bedeutet nicht, dass Sie eines dieser drei Ziele auswählen müssen, sondern dass Sie Ihrem Cloudstrategieteam und Cloudeinführungsteam helfen, eine Reihe von operativen Prioritäten als Leitfaden für die Ausführung in den nächsten drei bis sechs Monaten festzulegen. Zur Festlegung dieser Prioritäten wird eine Rangfolge für die drei einzelnen Optionen _von der wichtigsten_ zu der _am wenigsten wichtigen_ aufgestellt, da sie in Bezug zu den Maßnahmen stehen, zu denen dieses Team in den nächsten ein bis zwei Quartalen beitragen kann.

### <a name="act-on-migration-outcomes"></a>Maßnahmen für Migrationsergebnisse

Wenn operative Ergebnisse den höchsten Stellenwert in der Liste haben, ist dieser Abschnitt zum Cloud Adoption Framework bestens für Ihr Team geeignet. In diesem Abschnitt wird davon ausgegangen, dass Sie Geschwindigkeit und Kosteneinsparungen als primäre KPIs (Key Performance Indicators) priorisieren müssen. In diesem Fall wäre ein Migrationsmodell für die Einführung gut auf die Ergebnisse abgestimmt. Ein auf die Migration ausgerichtetes Modell basiert stark auf einer „Lift & Shift“-Migration von IaaS-Ressourcen (Infrastructure-as-a-Service), damit ein Rechenzentrum ausgeschöpft wird und Kosteneinsparungen erzielt werden. In einem solchen Modell kann eine Modernisierung stattfinden, ist aber ein sekundärer Schwerpunkt, bis das primäre Migrationsziel umgesetzt ist.

### <a name="act-on-application-innovations"></a>Maßnahmen für Anwendungsinnovationen

Wenn Marktanteil und Kundenerlebnis Ihre Hauptantriebe sind, bietet dieser Abschnitt zum Cloud Adoption Framework möglicherweise nicht die beste Anleitung für die Maßnahmen Ihrer Teams. Anwendungsinnovationen erfordern einen Plan, der sich auf die Modernisierung und den Übergang von Workloads konzentriert, unabhängig von der zugrunde liegenden Infrastruktur. In einem solchen Fall können die Anleitungen in diesem Abschnitt informativ sein, sind aber möglicherweise nicht der beste Ansatz zum Treffen grundlegender Entscheidungen.

### <a name="act-on-data-innovations"></a>Maßnahmen für Dateninnovationen

Wenn Daten, Experimente, Forschung und Entwicklung (R&D) oder neue Produkte in den nächsten sechs Monaten bei Ihnen Priorität haben, bietet dieser Abschnitt zum Cloud Adoption Framework möglicherweise nicht die beste Anleitung für die Maßnahmen Ihrer Teams. Jede Maßnahme für Dateninnovationen kann von Leitlinien in Bezug auf die Migration vorhandener Quelldaten profitieren. Der breitere Fokus dieser Maßnahme würde jedoch auf Eingang und Integration zusätzlicher Datenquellen liegen. Eine Erweiterung dieser Anleitungen durch Vorhersagen und neue Erfahrungen ist viel wichtiger als die Migration von IaaS-Ressourcen.

## <a name="effort"></a>Aufwand

Der Migrationsaufwand kann je nach Größe und Komplexität der beteiligten Workloads stark variieren. Eine kleinere Workloadmigration mit ein paar Hundert virtuellen Computern (VMs) ist ein taktischer Prozess, der möglicherweise mithilfe automatisierter Tools wie [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) implementiert wird. Umgekehrt erfordert eine große Unternehmensmigration von Zehntausenden von Workloads einen sehr strategischen Prozess und kann eine umfangreiche Umgestaltung, Neuerstellung und Ersetzung bestehender Anwendungen mit Integration von Platform-as-a-Service (PaaS)- und Software-as-a-Service (SaaS)-Funktionen beinhalten. [Das Identifizieren und Ausgleichen des Umfangs](../../../strategy/balance-the-portfolio.md) Ihrer geplanten Migrationen ist von entscheidender Bedeutung.

Bevor Sie Entscheidungen treffen, die langfristige Auswirkungen auf das aktuelle Migrationsprogramm haben könnten, ist es wichtig, dass Sie sich über die folgenden Entscheidungen einig sind.

### <a name="effort-type"></a>Aufwandstyp

Bei jeder Migration von bedeutender Größe (über 250 virtuelle Computer) werden Ressourcen mithilfe einer Vielzahl von Übergangsoptionen migriert, die anhand von fünf Rationalisierungsmöglichkeiten erläutert werden: _Zuweisen eines neuen Hosts_, _Umgestalten_, _Umstrukturieren_, _Neuerstellen_ und _Ersetzen_.

Einige Workloads werden durch einen Prozess der _Neuerstellung_ oder _Umstrukturierung_ modernisiert, wodurch modernere Anwendungen mit neuen Funktionen und technischen Möglichkeiten entstellt werden. Andere Ressourcen durchlaufen einen Prozess der _Umgestaltung_, z. B. eine Umstellung auf Container oder andere modernere Hosting- und Betriebsansätze, die sich nicht unbedingt auf die Codebasis der Lösungen auswirken. Im Allgemeinen durchlaufen virtuelle Computer und andere Ressourcen, die gut etabliert sind, einen Prozess zum _Zuweisen eines neuen Hosts_, bei dem diese Ressourcen vom Rechenzentrum in die Cloud übergehen. Einige Workloads könnten möglicherweise in die Cloud migriert werden, sollten aber stattdessen durch dienstbasierte (SaaS-basierte) Clouddienste _ersetzt_ werden, die derselben Geschäftsanforderung entsprechen, z. B. durch Verwendung von Office 365 als Alternative zur Migration von Exchange Server-Instanzen.

In den meisten Szenarien erzeugt ein Geschäftsereignis eine zwingende Funktion, die dazu führt, dass ein hoher Prozentsatz der Ressourcen vorübergehend mithilfe des Prozesses zum _Zuweisen eines neuen Hosts_ migriert wird, gefolgt von einem bedeutenderen sekundären Übergang mithilfe einer der anderen Migrationsstrategien, nachdem sie sich in der Cloud befinden. Dieser Prozess wird häufig als ein _Übergang in die Cloud_ bezeichnet.

Während des Prozesses der [Rationalisierung digitaler Ressourcen](../../../digital-estate/calculate.md) werden diese Arten von Entscheidungen auf jede zu migrierende Ressource angewendet. Die zu diesem Zeitpunkt erforderliche Voraussetzung ist jedoch das Aufstellen einer Basisannahme. Welche der fünf Migrationsstrategien passt am besten zu den Geschäftszielen oder Geschäftsergebnissen, die der Grund für diese Migrationsmaßnahme sind? Diese Entscheidung dient als grundlegende Annahme während der gesamten Migration.

### <a name="effort-scale"></a>Aufwandsumfang

Der Umfang der Migration ist die nächste wichtige vorab erforderliche Entscheidung. Die Prozesse, die zum Migrieren von 1.000 Ressourcen erforderlich sind, unterscheiden sich von dem Prozess zum Verschieben von 10.000 Ressourcen. Bevor Sie mit der Migration beginnen, ist es wichtig, die folgenden Fragen zu beantworten:

- **Wie viele Ressourcen unterstützen derzeit die zu migrierenden Workloads?** Ressourcen umfassen Datenstrukturen, Anwendungen, virtuelle Computer und erforderliche IT-Geräte. Es wird empfohlen, für die erste Migration eine relativ kleine Workload auszuwählen.
- **Für wie viele dieser Ressourcen ist eine Migration geplant?** Es ist üblich, dass ein Prozentsatz der Ressourcen während eines Migrationsprozesses beendet wird, da keine weitere Abhängigkeit für Endbenutzer besteht.
- **Welche Top-Down-Schätzungen gibt es für den Umfang migrierbarer Ressourcen?** Schätzen Sie für die zur Migration anstehenden Workloads die Anzahl der unterstützenden Ressourcen wie Anwendungen, virtuelle Computer, Datenquellen und IT-Geräte. Anleitungen zum Identifizieren relevanter Ressourcen finden Sie im Abschnitt [Digitale Ressourcen](../../../digital-estate/index.md) des Framework für die Cloudeinführung.

### <a name="effort-timing"></a>Zeitliche Festlegung des Aufwands

Häufig ist ein zwingendes und zeitkritisches Geschäftsereignis der Grund für Migrationen. Ein üblicher Auslöser ist beispielsweise die Beendigung oder Verlängerung eines Hostingvertrags mit einem Drittanbieter. Zwar gibt es viele mögliche Geschäftsereignisse, die eine Migration erfordern, doch alle haben einen Faktor gemeinsam : ein Enddatum. Es ist wichtig, den zeitlichen Ablauf aller bevorstehenden Geschäftsereignisse zu verstehen, damit Aktivitäten und Geschwindigkeit richtig geplant und überprüft werden können.

## <a name="recap"></a>Zusammenfassung

Dokumentieren Sie vor dem Fortfahren die folgenden Annahmen, und teilen Sie diese dem Cloudstrategieteam und den Cloudeinführungsteams mit:

- Geschäftsergebnisse.
- Rollen, die für die Migrationsprozesse _Bewerten_, _Migrieren_, _Optimieren_ und _Sichern und Verwalten_ dokumentiert und präzisiert sind.
- Definition of Done, für die Migrationsprozesse _Bewerten_, _Migrieren_, _Optimieren_ und _Sichern und Verwalten_ separat dokumentiert und präzisiert.
- Aufwandstyp.
- Aufwandsumfang.
- Zeitliche Festlegung des Aufwands.

## <a name="next-steps"></a>Nächste Schritte

Wenn das Team den Prozess vollständig verstanden hat, ist es an der Zeit, die technischen Voraussetzungen zu überprüfen. Mithilfe der [Planungscheckliste für die Migrationsumgebung](./planning-checklist.md) kann sichergestellt werden, dass die technischen Grundlagen für die Migration bereitstehen.

Wenn das Team den Prozess vollständig verstanden hat, ist es an der Zeit, die technischen Voraussetzungen zu überprüfen. Mithilfe der [Planungscheckliste für die Migration](./planning-checklist.md) kann sichergestellt werden, dass die technischen Grundlagen für die Migration bereitstehen.

> [!div class="nextstepaction"]
> [Überprüfen der Planungscheckliste für die Migration](./planning-checklist.md)
