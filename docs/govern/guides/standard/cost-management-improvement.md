---
title: 'Governance für Standardunternehmen: Verbessern der Disziplin „Cost Management“'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Sie einem Minimum Viable Product (MVP) für die Governance Kostenkontrollfunktionen hinzufügen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1c25a98eaa63e6cd6f71ac571ec4e006ad7c4946
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219936"
---
# <a name="standard-enterprise-governance-guide-improve-the-cost-management-discipline"></a>Governanceleitfaden für Standardunternehmen: Verbessern der Disziplin „Cost Management“

Dieser Artikel führt die Geschichte fort, indem dem Governance-MVP Kostenkontrolle hinzugefügt wird.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

<!-- docsTest:ignore DR -->

Die Einführung hat sich über den im Governance-MVP definierten Kostentoleranzindikator hinaus entwickelt. Das ist gut so, denn dies korrespondiert mit Migrationen aus dem Datencenter „DR“. Die Steigerung in den Ausgaben rechtfertigt jetzt den Aufwand an Zeit seitens des Cloudgovernanceteams.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Lösung hatte die IT 100 % des DR-Datencenters außer Betrieb genommen. Die Anwendungsentwicklungs- und BI-Teams sind für Produktionsdatenverkehr bereit.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Das Migrationsteam hat mit der Migration von VMs aus dem Produktionsdatencenter begonnen.
- Die Anwendungsentwicklungsteams übertragen aktiv Produktionsanwendungen über CI/CD-Pipelines in die Cloud. Diese Anwendungen können als Reaktion auf Benutzeranforderungen skaliert werden.
- Das Business Intelligence-Team der IT-Abteilung hat verschiedene Predictive Analytics-Tools in der Cloud bereitgestellt. Die Menge der Daten, die in der Cloud aggregiert werden, wächst beständig.
- All dieses Wachstum unterstützt überzeugende Geschäftsergebnisse. Allerdings haben die Kosten begonnen, sich zu vervielfachen. Die prognostizierten Budgets wachsen schneller als erwartet. Der CFO benötigt verbesserte Ansätze für das Kostenmanagement.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Die Cloudlösung soll um Kostenüberwachung und -berichterstellung erweitert werden. Die IT dient nach wie vor als Kostenverrechnungsstelle. Das bedeutet, dass die Vergütung für Clouddienste weiterhin aus der IT-Beschaffung stammt. Die Berichterstellung sollte jedoch die direkten Betriebskosten an die Funktionen binden, die die Cloudkosten verbrauchen. Dieses Modell wird als _Showback_-Modell für die Cloudbuchhaltung bezeichnet.

Die Änderungen des aktuellen und zukünftigen Status bergen neue Risiken, die neue Richtlinienanweisungen erfordern.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Budgetkontrolle:** Es besteht die grundsätzliche Gefahr, dass Self-Service-Fähigkeiten zu überhöhten und unerwarteten Kosten auf der neuen Plattform führen. Es müssen Governanceprozesse zur Kostenüberwachung und Reduzierung der laufenden Kostenrisiken wirksam sein, um eine kontinuierliche Ausrichtung am Planbudget zu gewährleisten.

Dieses Unternehmensrisiko lässt sich auf einige technische Risiken erweitern:

- Die Ist-Kosten können den Plan übersteigen.
- Geschäftsbedingungen ändern sich. Wenn dieser Fall eintritt, werden einzelne Geschäftsfunktion mehr Clouddienste nutzen müssen als erwartet, was zu Anomalien bei den Ausgaben führt. Es besteht die Gefahr, dass diese zusätzlichen Ausgaben als Überschüsse betrachtet werden, im Gegensatz zu einer notwendigen Anpassung des Plans.
- Systeme könnten überdimensioniert sein, was zu Ausgabenüberschüssen führen kann.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung.

- Alle Cloudkosten sollten wöchentlich vom Governance-Team anhand eines Plans überwacht werden. Berichte zu Abweichungen zwischen den Cloudkosten und dem Plan sind monatlich mit der IT-Leitung und der Finanzabteilung zu teilen. Alle Cloudkosten und Planaktualisierungen sollten monatlich zusammen mit der IT-Leitung und der Finanzabteilung überprüft werden.
- Alle Kosten müssen zum Zweck der Rechnungslegung einer Geschäftsfunktion zugeordnet sein.
- Cloudressourcen sollten fortlaufend auf Optimierungsmöglichkeiten überprüft werden.
- Cloudgovernancetools müssen die Optionen für die Dimensionierung von Ressourcen auf eine genehmigte Liste mit Konfigurationen beschränken. Die Tools müssen sicherstellen, dass alle Ressourcen ermittelbar sind und von der Kostenüberwachungslösung verfolgt werden.
- Während der Bereitstellungsplanung sollten alle erforderlichen Cloudressourcen, die dem Hosten von Produktionsworkloads dienen, dokumentiert werden. Diese Dokumentation kann bei der Verfeinerung der Budgets und bei der Vorbereitung zusätzlicher Automatisierungen helfen, um den Einsatz teurerer Optionen zu vermeiden. Dabei sollten verschiedene vom Cloudanbieter angebotene Diskontierungstools, z.B. reservierte Instanzen oder Lizenzkostenreduzierungen, in Betracht gezogen werden.
- Alle Besitzer von Anwendungen sind verpflichtet, an Schulungen zu Praktiken zur Optimierung von Workloads teilzunehmen, um die Cloudkosten besser zu kontrollieren.

## <a name="incremental-improvement-of-the-best-practices"></a>Inkrementelle Verbesserungen der bewährten Methoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so geändert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

1. Implementieren von Azure Cost Management.
    1. Legen Sie den richtigen Zugriffsumfang fest, um ihn an das Abonnementmuster und die Disziplin „Ressourcenkonsistenz“ anzupassen. Unter der Annahme der Angleichung an das in früheren Artikeln definierte Governance-MVP erfordert dies Zugriff des Umfangs **Registrierungskonto** für das Cloudgovernanceteam, das die Berichtserstellung auf hoher Ebene durchführt. Weitere Teams außerhalb von Governance benötigen möglicherweise Zugriff des Umfangs **Ressourcengruppe**.
    1. Einrichten eines Budgets in Azure Cost Management.
    1. Überprüfen Sie die anfänglichen Empfehlungen, und reagieren Sie entsprechend. Nutzen Sie einen regelmäßiger Prozess zur Unterstützung der Berichterstellung.
    1. Konfigurieren Sie die Azure Cost Management-Berichterstellung mit anfänglicher und regelmäßiger Ausführung.
2. Aktualisieren von Azure Policy
    1. Überwachen Sie die Tagging-, Verwaltungsgruppen-, Abonnement- und Ressourcengruppenwerte, um Abweichungen zu identifizieren.
    1. Legen Sie Optionen für die SKU-Größe fest, um die Bereitstellung auf die in der Dokumentation zur Bereitstellungsplanung aufgeführten SKUs zu beschränken.

## <a name="conclusion"></a>Zusammenfassung

Durch Hinzufügen dieser Prozesse und Änderungen zum Governance-MVP lassen sich viele Risiken im Zusammenhang mit der Kostengovernance beseitigen. Gemeinsam schaffen sie die Transparenz, Zuverlässigkeit und Optimierung, die zur Kostenkontrolle erforderlich sind.

## <a name="next-steps"></a>Nächste Schritte

Mit der Fortsetzung der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an die Cloudgovernance. Für das fiktive Unternehmen in diesem Leitfaden ist der nächste Schritt die Nutzung dieser Governanceinvestition zur Verwaltung mehrerer Clouds.

> [!div class="nextstepaction"]
> [Multi-Cloud-Entwicklung](./multicloud-improvement.md)
