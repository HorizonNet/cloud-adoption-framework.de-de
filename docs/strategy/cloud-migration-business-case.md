---
title: Geschäftliche Begründung für die Cloudmigration
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie mit dem Entwickeln einer geschäftlichen Begründung für die Cloudmigration beginnen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 9ef3c108d330cd52b470c590a48f79c65502a7e6
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80431639"
---
# <a name="build-a-business-justification-for-cloud-migration"></a>Erstellen einer geschäftlichen Begründung für die Cloudmigration

Bei Cloudmigrationen können mit Maßnahmen zur Cloudtransformation frühzeitig Renditebeträge (Return on Investment, ROI) generiert werden. Die Entwicklung einer eindeutigen geschäftlichen Begründung mit greifbaren, relevanten Kosten und Erträgen kann ein komplexer Prozess sein. In diesem Artikel erhalten Sie Informationen dazu, welche Daten Sie zum Erstellen eines Finanzmodells benötigen, das an den Ergebnissen der Cloudmigration ausgerichtet ist. Lassen Sie uns zuerst einige Mythen zur Cloudmigration ausräumen, damit Ihre Organisation einige häufige Fehler vermeiden kann.

## <a name="dispelling-cloud-migration-myths"></a>Ausräumen von Mythen zur Cloudmigration

**Mythos: Die Cloud ist immer günstiger.** Es herrscht allgemein die Auffassung, dass der Betrieb eines Rechenzentrums in der Cloud immer kostengünstiger als der lokale Betrieb ist. Obwohl diese Annahme im allgemeinen zutreffen kann, ist dies nicht immer der Fall. Manchmal sind die Betriebskosten der Cloud höher. Diese höheren Kosten sind auf unzureichende Kostengovernance, falsch ausgerichtete Systemarchitekturen, Prozessduplizierung, ungewöhnliche Systemkonfigurationen oder höhere Personalkosten zurückzuführen. Glücklicherweise können Sie viele dieser Probleme beheben, um frühzeitig eine Rendite zu erzielen. Die Anleitung unter [Erstellen der geschäftlichen Begründung](#build-the-business-justification) enthält Informationen dazu, wie Sie diese Abstimmungsfehler erkennen und vermeiden können. Es kann auch hilfreich sein, wenn Sie sich die hier angegebenen weiteren Informationen zur Ausräumung von Mythen durchlesen.

**Mythos: Alles sollte in die Cloud verlagert werden.** Es gibt einige geschäftliche Faktoren, die dazu führen können, dass Sie eine Hybridlösung wählen. Es ist ratsam, vor der Fertigstellung eines Geschäftsmodells zunächst eine erste quantitative Analyse durchzuführen. Dies ist in den [Artikeln zu digitalen Ressourcen](../digital-estate/5-rs-of-rationalization.md) beschrieben. Weitere Informationen zu den einzelnen quantitativen Faktoren der Rationalisierung finden Sie unter [Die fünf R der Rationalisierung](../digital-estate/5-rs-of-rationalization.md). Bei beiden Ansätzen werden einfach zu beschaffende Bestandsdaten und eine kurze quantitative Analyse verwendet, um Workloads oder Anwendungen zu identifizieren, die zu höheren Kosten in der Cloud führen können. Mit diesen Ansätzen können auch Abhängigkeiten oder Datenverkehrsmuster identifiziert werden, für die eine Hybridlösung erforderlich ist.

**Mythos: Durch die Spiegelung meiner lokalen Umgebung kann ich in der Cloud Kosten sparen.** Es kommt vor, dass Unternehmen beim Planen der digitalen Ressourcen ungenutzte Kapazität ermitteln, die mehr als 50% der bereitgestellten Umgebung ausmacht. Wenn Ressourcen in der Cloud bereitgestellt werden, um die derzeitige Bereitstellung widerzuspiegeln, lassen sich Kosteneinsparungen nur schwer realisieren. Erwägen Sie, die Größe der bereitgestellten Ressourcen zu verringern, um eine Anpassung an die Nutzungsmuster zu erzielen (anstelle der Bereitstellungsmuster).

**Mythos: Serverkosten sind die Grundlage von Geschäftsszenarien für die Cloudmigration.** Manchmal ist diese Annahme zutreffend. Für einige Unternehmen ist es wichtig, die laufenden Investitionskosten für Server zu reduzieren. Dies ist aber von mehreren Faktoren abhängig. Unternehmen mit einem Hardwareaktualisierungszyklus von fünf bis acht Jahren können bei der Cloudmigration meistens keine schnelle Rendite erzielen. Unternehmen mit standardisierten oder erzwungenen Aktualisierungszyklen können den Break-even-Point dagegen schnell erreichen. In beiden Fällen können auch andere Ausgaben die finanziellen Auslöser sein, die eine Migration rechtfertigen. Hier sind einige Beispiele für Kosten angegeben, die häufig übersehen werden, wenn Unternehmen die Kosten nur aus Server- oder VM-Sicht betrachten:

- Die Kosten von Software für Virtualisierung, Server und Middleware können sehr hoch sein. Bei der Nutzung von Cloudanbietern werden einige dieser Kosten beseitigt. Zwei Beispiele für die Reduzierung der Virtualisierungskosten bei Nutzung eines Cloudanbieters sind die Programme [Azure-Hybridvorteil](https://azure.microsoft.com/pricing/hybrid-benefit/#services) und [Azure-Reservierungen](https://azure.microsoft.com/reservations).
- Verluste aufgrund von Ausfällen können die Hardware- oder Softwarekosten schnell übersteigen. Wenn Ihr derzeitiges Rechenzentrum nicht stabil ist, können Sie mit dem Unternehmen zusammenarbeiten, um die Auswirkungen von Ausfällen in Bezug auf die Verkaufschancenkosten oder die tatsächlichen Geschäftskosten zu quantifizieren.
- Umgebungskosten können ebenfalls relevant sein. Für die durchschnittliche amerikanische Familie stellt ein Haus die größte Investition und den größten Kostenpunkt des Budgets dar. Gleiches gilt häufig auch für Datencenter. Kosten für Gebäude, Einrichtungen und Versorgungsleistungen machen einen großen Teil der lokalen Kosten aus. Wenn Datencenter ausgemustert werden, können die entsprechenden Einrichtungen vom Unternehmen anderweitig genutzt werden oder fallen ggf. auch ganz aus den Kosten heraus.

**Mythos: Ein Betriebskostenmodell ist besser als ein Investitionskostenmodell.** Im Artikel mit den [Beispielen für Finanzergebnisse](./business-outcomes/fiscal-outcomes.md) ist beschrieben, dass ein Betriebskostenmodell eine gute Sache ist. Einige Branchen sehen die Betriebskosten jedoch negativ. Hier sind einige Beispiele angegeben, die in Bezug auf die Betriebskosten zu einer stärkeren Integration der Buchhaltung und der Geschäftseinheiten führen:

- Wenn ein Unternehmen Kapitalvermögen im Hinblick auf die Unternehmensbewertung als positiv ansieht, können Investitionskostenreduzierungen ein negatives Ergebnis darstellen. Es ist zwar keine allgemeine Norm, aber diese Auffassung ist in den Bereichen Einzelhandel, Fertigung und Bauwesen häufiger anzutreffen.
- Private Equity-Firmen oder Unternehmen, die auf der Suche nach Kapitalzuflüssen sind, können Erhöhungen der Betriebskosten unter Umständen als negatives Ergebnis ansehen.
- Wenn ein Unternehmen stark auf die Verbesserung der Verkaufsmargen oder die Reduzierung der Umsatzkosten (Cost of Goods Sold, COGS) fixiert ist, sind Betriebskosten ein negatives Ergebnis.

Unternehmen neigen dazu, Betriebskosten positiver als Investitionskosten anzusehen. Dieser Ansatz wird beispielsweise von Unternehmen gewählt, die versuchen, den Cashflow zu verbessern, die Kapitalinvestitionen zu reduzieren oder die Anlagegüter zu verringern.

Bevor Sie eine geschäftliche Begründung bereitstellen, in der es um die Umstellung von Investitionskosten auf Betriebskosten geht, sollten Sie ermitteln, welche Kosten besser für Ihr Unternehmen sind. Die Buchhaltung und der Einkauf können häufig dabei behilflich sein, die Botschaft an die finanziellen Ziele anzupassen.

**Mythos: Die Umstellung auf die Cloud ist wie das Umlegen eines Schalters.** Migrationen stellen eine manuelle, aufwändige technische Transformation dar. Beachten Sie beim Entwickeln einer geschäftlichen Begründung – vor allem unter Zeitdruck – die folgenden Aspekte, die zu einer Verlängerung des benötigten Zeitraums für die Migration von Ressourcen führen können:

- **Einschränkungen der Bandbreite:** Die Menge an Bandbreite zwischen dem aktuellen Datencenter und dem Cloudanbieter ist für die anfallenden Zeitdauern während der Migration verantwortlich.
- **Zeitpläne für Tests:** Das Testen von Anwendungen mit dem Unternehmen, um die Bereitschaft und Leistung sicherzustellen, kann zeitaufwendig sein. Die Abstimmung von Powerusern und Testprozessen ist von entscheidender Bedeutung.
- **Zeitpläne für Migrationen:** Zeit und Aufwand für die Implementierung der Migration können zu einer Erhöhung der Kosten und zu Verzögerungen führen. Die Zuordnung von Mitarbeitern oder Vertragspartnern kann den Prozess ebenfalls verzögern. Der Plan sollte diese Zuteilungen berücksichtigen.

Technische und kulturelle Hindernisse können die Einführung der Cloud verlangsamen. Falls die Zeit ein wichtiger Aspekt der geschäftlichen Begründung ist, besteht die beste Vorgehensweise in einer präzisen Planung. Während der Planung können zwei Ansätze helfen, Zeitplanrisiken auszuräumen:

- Investieren Sie die nötige Zeit und Energie, um sich mit den technischen Einschränkungen der Einführung vertraut zu machen. Zwar ist der Druck, die Umstellung schnell durchzuführen, unter Umständen hoch, aber es ist wichtig, hierfür einen realistischen Zeitplan aufzustellen.
- Falls kulturelle oder personenbezogene Hindernisse bestehen, ergeben sich größere Auswirkungen als bei technischen Einschränkungen. Bei der Einführung der Cloud kommt es zu Änderungen, die erforderlich sind, um die gewünschte Transformation zu erzielen. Leider haben Menschen manchmal Angst vor Veränderungen und benötigen zusätzliche Unterstützung, um den Plan vollständig zu akzeptieren. Ermitteln Sie die wichtigen Mitglieder des Teams, die die Veränderungen ablehnen, und binden Sie diese Personen frühzeitig ein.

Bereiten Sie leitende Projektbeteiligte vor, indem Sie den geschäftlichen Nutzen und die Geschäftsergebnisse eindeutig einander zuordnen, um die Bereitschaft zu erhöhen und die Entschärfung von Zeitplanrisiken zu verbessern. Unterstützen Sie die Projektbeteiligten dabei, die sich aus der Transformation ergebenden Veränderungen besser zu verstehen. Machen Sie von Beginn an klare Aussagen, und setzen Sie realistische Ziele. Falls der Prozess aufgrund von Personen oder Technologien verlangsamt wird, ist die Unterstützung durch die Führungsebene leichter zu erlangen.

## <a name="build-the-business-justification"></a>Formulieren der geschäftlichen Begründung

Mit dem folgenden Prozess wird ein Ansatz zur Entwicklung der geschäftlichen Begründung für Cloudmigrationen definiert. Weitere Informationen zu Berechnungen und Finanzbedingungen finden Sie im Artikel zu [Finanzmodellen](./financial-models.md).

Aus allgemeiner Sicht ist die Formel für die geschäftliche Begründung einfach. Es kann aber durchaus schwierig sein, die spezifischen Datenpunkte abzustimmen, die für die Formel benötigt werden. Bei der geschäftlichen Begründung geht es im Allgemeinen um die Rendite (Return on Investment, ROI), die mit der angestrebten technischen Veränderung verbunden ist. Die generische Formel für die Rendite lautet:

![Return on Investment (ROI) = (Investitionsertrag - Investitionskosten) / Investitionskosten](../_images/strategy/formula-roi.png)

Wenn wir diese Gleichung in ihre Bestandteile zerlegen, ergibt sich ein migrationsspezifischer Blick auf die Formeln, die den Eingabevariablen auf der rechten Seite der Gleichung zugrunde liegen. Die restlichen Abschnitte dieses Artikels enthalten einige Aspekte, die berücksichtigt werden sollten.

## <a name="migration-specific-initial-investment"></a>Migrationsspezifische Erstinvestition

- Cloudanbieter wie Azure bieten Rechner an, mit denen Prognosen in Bezug auf Cloudinvestitionen erstellt werden können. Der [Azure-Preisrechner](https://azure.microsoft.com/pricing/calculator) ist ein Beispiel.
- Einige Cloudanbieter stellen auch Rechner zur Ermittlung von Kostendeltawerten bereit. Ein Beispiel ist der [Gesamtkostenrechner von Azure](https://azure.com/tco).
- Bei anspruchsvolleren Kostenstrukturen können Sie erwägen, eine Übung zur [Planung von digitalen Ressourcen](../digital-estate/index.md) durchzuführen.
- Erstellen Sie eine Schätzung der Kosten für die Migration.
- Schätzen Sie die Kosten für die zu erwartenden Schulungsmaßnahmen. [Microsoft Learn](https://docs.microsoft.com/learn) kann beim Verringern dieser Kosten eine Hilfe darstellen.
- In einigen Unternehmen muss die Zeit, die von vorhandenen Mitarbeitern investiert wird, unter Umständen in die Anfangskosten eingerechnet werden. Hilfe hierzu erhalten Sie von Ihrer Finanzabteilung.
- Besprechen Sie alle weiteren Kosten oder Gemeinkosten mit der Finanzabteilung, um diese zu bewerten.

## <a name="migration-specific-revenue-deltas"></a>Deltawerte für migrationsspezifischen Umsatz

Dieser Aspekt wird von Strategen, die eine geschäftlichen Begründung für die Migration erstellen, häufig übersehen. In einigen Bereichen können durch die Nutzung der Cloud Kosten gesenkt werden. Das letztendliche Ziel jeder Transformation besteht aber darin, langfristig bessere Ergebnisse zu erzielen. Berücksichtigen Sie die nachgelagerten Auswirkungen, um die langfristigen Möglichkeiten zur Verbesserung des Umsatzes zu verstehen. Welche neuen Technologien sind für Ihr Unternehmen nach der Migration verfügbar, die derzeit noch nicht genutzt werden können? Welche Projekte oder Geschäftsziele werden durch Abhängigkeiten oder ältere Technologien verhindert? Welche Programme wurden ausgesetzt und sind mit hohen ausstehenden Investitionskosten für Technologie verbunden?

Nachdem Sie sich mit den Chancen vertraut gemacht haben, die sich durch die Cloud ergeben, können Sie mit dem Unternehmen die Umsatzsteigerungen berechnen, die aufgrund dieser Chancen möglich sind.

## <a name="migration-specific-cost-deltas"></a>Deltawerte für migrationsspezifische Kosten

Berechnen Sie alle Änderungen in Bezug auf die Kosten, die sich aus der vorgeschlagenen Migration ergeben. Weitere Informationen zu den Kostendeltatypen finden Sie im Artikel [Finanzmodelle](./financial-models.md). Cloudanbieter stellen häufig Tools zum Berechnen von Kostendeltawerten bereit. Ein Beispiel ist der [Gesamtkostenrechner von Azure](https://azure.com/tco).

Weitere Beispiele für Kosten, die durch eine Cloudmigration gesenkt werden können:

- Auflösung oder Reduzierung von Datencentern (Umgebungskosten)
- Reduzierung des Energieverbrauchs (Umgebungskosten)
- Aussonderung von Racks (Kostendeckung für physische Ressourcen)
- Vermeidung einer Hardwareaktualisierung (Kostenvermeidung)
- Vermeidung der Verlängerung von Software (Betriebskostenreduzierung oder Kostenvermeidung)
- Anbieterkonsolidierung (Betriebskostenreduzierung und potenzielle Reduzierung von weichen Kosten)

## <a name="when-roi-results-are-surprising"></a>Überraschung bei den Renditeergebnissen

Wenn der ROI einer Cloudmigration nicht Ihren Erwartungen entspricht, kann es hilfreich sein, sich noch einmal die Informationen zu häufigen Mythen am Anfang dieses Artikels anzusehen.

Es ist aber wichtig zu verstehen, dass sich Kosteneinsparungen nicht immer möglich sind. Der Betrieb einiger Anwendungen ist in der Cloud teurer als am lokalen Standort. Diese Anwendungen können die Ergebnisse einer Analyse erheblich verzerren.

Wenn die Rendite unter 20 % liegt, sollten Sie die Durchführung einer Übung zur [Planung der digitalen Ressourcen](../digital-estate/index.md) durchführen und besonders auf die [Rationalisierung](../digital-estate/rationalize.md) achten. Überprüfen Sie während der quantitativen Analyse jede Anwendung, um Workloads zu ermitteln, die zur Verzerrung der Ergebnisse beitragen. Es kann ratsam sein, diese Workloads aus dem Plan herauszunehmen. Wenn Nutzungsdaten verfügbar sind, können Sie ggf. auch die Größe der VMs reduzieren, um sie an die tatsächliche Nutzung anzupassen.

Falls die Rendite immer noch nicht zufriedenstellend ist, können Sie Ihren Microsoft-Vertriebsmitarbeiter um Hilfe bitten oder [einen erfahrenen Partner engagieren](https://azure.microsoft.com/migration/support).

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Erstellen eines Finanzmodells für die Cloudtransformation](./financial-models.md)
