---
title: 'Governance in komplexen Unternehmen: Verbessern der Disziplin „Kostenverwaltung“'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Sie einem Minimum Viable Product (MVP) für die Governance Kostenkontrollfunktionen hinzufügen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b44f153c9e14f1425aa3bb1374c60243c9a3c326
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709038"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-cost-management-discipline"></a>Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Cost Management“

Dieser Artikel führt die Geschichte fort, indem dem Minimum Viable Product-Governance (MVP) Kostenkontrolle hinzugefügt wird.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Die Einführung hat sich über den im Governance-MVP definierten Toleranzindikator hinaus entwickelt. Die Steigerung in den Ausgaben rechtfertigt jetzt den Aufwand an Zeit seitens des Cloudgovernanceteams für die Überwachung und Kontrolle von Ausgabenmustern.

Als treibende Kraft der Innovation wird IT nicht mehr in erster Linie als Kostenstelle betrachtet. Da die IT-Organisation Mehrwert generiert, stimmen der CIO und CFO überein, dass jetzt die Zeit gekommen ist, die Rolle der IT im Unternehmen zu verändern. Unter anderem will der CFO einen Direktvergütungsansatz bei der cloudbasierten Abrechnung für die kanadische Niederlassung einer der Geschäftseinheiten testen. Eins der beiden stillgelegten Rechenzentren hostete exklusiv Ressourcen für den operativen Betrieb der besagten Geschäftseinheit in Kanada. In diesem Modell werden der kanadischen Niederlassung der Geschäftseinheit die Betriebsausgaben im Zusammenhang mit den gehosteten Ressourcen direkt in Rechnung gestellt. Dieses Modell ermöglicht der IT, sich weniger auf die Verwaltung der Ausgaben anderer als vielmehr auf die Wertschöpfung zu konzentrieren. Bevor dieser Übergang erfolgen kann, müssen jedoch Kostenverwaltungstools implementiert worden sein.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Erzählung hat das IT-Team Produktionsworkloads mit geschützten Daten aktiv nach Azure verschoben.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- 5\.000 Ressourcen wurden aus den beiden zur Stilllegung markierten Rechenzentren entfernt. Auftragswesen und IT-Sicherheit heben nun die Bereitstellung der verbleibenden physischen Ressourcen auf.
- Die Anwendungsentwicklungsteams haben CI/CD-Pipelines implementiert, um einige native Cloudanwendungen bereitzustellen, die erhebliche Auswirkungen auf das Kundenerlebnis haben.
- Das Business Intelligence-Team hat Aggregations-, Zusammenstellungs-, Erkenntnis- und Prognoseprozesse entwickelt, die konkrete Vorteile für den Geschäftsbetrieb bringen. Diese Prognosen ermöglichen jetzt kreative neue Produkte und Dienstleistungen.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Die Cloudlösung sollte um Kostenüberwachung und -berichterstellung erweitert werden. Die Berichterstellung sollte jedoch die direkten Betriebskosten an die Funktionen binden, die die Cloudkosten verbrauchen. Zusätzliche Berichte sollten es der IT-Abteilung ermöglichen, die Ausgaben zu überwachen und technische Hinweise zum Kostenmanagement zu geben. Für die kanadische Zweigstelle wird direkt mit der Abteilung abgerechnet.

## <a name="changes-in-risk"></a>Änderungen des Risikos

**Budgetkontrolle:** Es besteht die grundsätzliche Gefahr, dass Self-Service-Fähigkeiten zu überhöhten und unerwarteten Kosten auf der neuen Plattform führen. Es müssen Governanceprozesse zur Kostenüberwachung und Reduzierung der laufenden Kostenrisiken wirksam sein, um eine kontinuierliche Ausrichtung am Planbudget zu gewährleisten.

Dieses Unternehmensrisiko lässt sich auf einige technische Risiken erweitern:

- Es besteht die Gefahr, dass die Ist-Kosten den Plan übersteigen.
- Geschäftsbedingungen ändern sich. Wenn dieser Fall eintritt, werden einzelne Geschäftsfunktion mehr Clouddienste nutzen müssen als erwartet, was zu Anomalien bei den Ausgaben führt. Es besteht das Risiko, dass diese zusätzlichen Kosten als Überschreitungen angesehen werden, statt als notwendige Anpassung des Plans. Bei Erfolg sollte das kanadische Experiment ein Beitrag zur Korrektur dieses Risikos sein.
- Es besteht die Gefahr überdimensionierter Systeme, die Mehrausgaben verursachen.

## <a name="changes-to-the-policy-statements"></a>Änderungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung.

- Alle Cloudkosten sollten wöchentlich vom Cloudgovernanceteam anhand eines Plans überwacht werden. Berichte zu Abweichungen zwischen den Cloudkosten und dem Plan sind monatlich mit der IT-Leitung und der Finanzabteilung zu teilen. Alle Cloudkosten und Planaktualisierungen sollten monatlich zusammen mit der IT-Leitung und der Finanzabteilung überprüft werden.
- Alle Kosten müssen zum Zweck der Rechnungslegung einer Geschäftsfunktion zugeordnet sein.
- Cloudressourcen sollten fortlaufend auf Optimierungsmöglichkeiten überprüft werden.
- Cloudgovernancetools müssen die Optionen für die Dimensionierung von Ressourcen auf eine genehmigte Liste mit Konfigurationen beschränken. Die Tools müssen sicherstellen, dass alle Ressourcen ermittelbar sind und von der Kostenüberwachungslösung verfolgt werden.
- Während der Bereitstellungsplanung sollten alle erforderlichen Cloudressourcen, die dem Hosten von Produktionsworkloads dienen, dokumentiert werden. Diese Dokumentation kann bei der Verfeinerung der Budgets und bei der Vorbereitung zusätzlicher Automatisierungstools helfen, um den Einsatz teurerer Optionen zu vermeiden. Während dieses Prozesses sollten verschiedene vom Cloudanbieter angebotene Rabattierungstools wie z.B. reservierte Instanzen oder Lizenzkostenreduzierungen in Betracht gezogen werden.
- Alle Besitzer von Anwendungen sind verpflichtet, an Schulungen zu Praktiken zur Optimierung von Workloads teilzunehmen, um die Cloudkosten besser zu kontrollieren.

## <a name="incremental-improvement-of-the-best-practices"></a>Inkrementelle Verbesserungen der bewährten Methoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so verbessert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

1. Nehmen Sie Änderungen im Azure Enterprise-Portal vor, um die Bereitstellung in Kanada dem Abteilungsadministrator in Rechnung zu stellen.
2. Implementieren von Azure Cost Management.
    1. Festlegen des richtigen Zugriffsumfangs, um ihn mit dem Abonnementmuster und dem Ressourcengruppierungsmuster abzustimmen. Unter der Annahme der Angleichung an das in früheren Artikeln definierte Governance-MVP sollte dies Zugriff im Geltungsbereich des **Registrierungskontos** für das Cloudgovernanceteam erfordern, das die Berichterstellung auf hoher Ebene durchführt. Zusätzliche Teams außerhalb der Governance, wie etwa das kanadische Beschaffungsteam, benötigen Zugriff im **Ressourcengruppenumfang**.
    2. Einrichten eines Budgets in Azure Cost Management.
    3. Überprüfen Sie die anfänglichen Empfehlungen, und reagieren Sie entsprechend. Es empfiehlt sich, zur Unterstützung des Berichterstellungsprozesses einen sich wiederholenden Prozess einzurichten.
    4. Konfigurieren Sie Azure Cost Management-Berichterstellung mit anfänglicher und regelmäßiger Ausführung.
3. Aktualisieren von Azure Policy.
    1. Überwachen Sie die Tagging-, Verwaltungsgruppen-, Abonnement- und Ressourcengruppenwerte, um Abweichungen zu identifizieren.
    2. Legen Sie Optionen für die SKU-Größe fest, um die Bereitstellung auf die in der Dokumentation zur Bereitstellungsplanung aufgeführten SKUs zu beschränken.

## <a name="conclusion"></a>Zusammenfassung

Durch das Hinzufügen der oben genannten Prozesse und Änderungen zum Governance-MVP lassen sich viele Risiken im Zusammenhang mit der Kostengovernance umgehen. Gemeinsam schaffen sie die Transparenz, Zuverlässigkeit und Optimierung, die zur Kostenkontrolle erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Mit dem Wachstum der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an Cloud Governance. Für dieses fiktive Unternehmen ist der nächste Schritt die Nutzung dieser Governanceinvestition zur Verwaltung mehrerer Clouds.

> [!div class="nextstepaction"]
> [Große Unternehmen: Multi-Cloud-Entwicklung](./multicloud-improvement.md)
