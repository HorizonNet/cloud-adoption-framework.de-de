---
title: Strategie für Governance bzw. Compliance
description: Strategie für Governance bzw. Compliance
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4e303d1e179d8ed6f90b5e823381cf8b31827df4
ms.sourcegitcommit: 580a6f66a0d0f3f5b755c68d757a84b2351a432f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/31/2020
ms.locfileid: "87472875"
---
# <a name="governance-or-compliance-strategy"></a>Strategie für Governance bzw. Compliance

Wenn in einem Migrationsprojekt Governance- oder Complianceanforderungen erfüllt werden müssen, muss der Umfang entsprechend erweitert werden. Die folgende Anleitung erweitert den [Azure-Migrationsleitfaden](../azure-migration-guide/index.md) und geht auf verschiedene Herangehensweisen zur Erfüllung von Governance- oder Complianceanforderungen ein.

## <a name="general-scope-expansion"></a>Allgemeine Umfangserweiterung

Anforderungen hinsichtlich Governance oder Compliance wirken sich am meisten auf Aktivitäten zum Erfüllen von Voraussetzungen aus. Während der Bewertung, Migration und Optimierung sind möglicherweise weitere Anpassungen erforderlich.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Die Konfiguration der grundlegenden Azure-Umgebung kann sich erheblich ändern, wenn Anforderungen hinsichtlich Governance oder Compliance ins Spiel kommen. Um zu verstehen, wie sich die Voraussetzungen ändern, müssen Sie die Art der Anforderungen kennen. Vor Beginn einer Migration mit Governance- oder Complianceanforderungen muss eine Vorgehensweise gewählt und in der Cloudumgebung implementiert werden. Im Folgenden finden Sie einige allgemeine Vorgehensweisen, die in Migrationsprozessen häufig zu finden sind:

**Allgemeine Vorgehensweise für die Governance**: Für die meisten Organisationen ist das [Cloud Adoption Framework-Governancemodell](../../govern/guides/index.md) ausreichend. Es besteht aus der Implementierung eines Minimum Viable Product (MVP), gefolgt von zielgerichteten Iterationen der Governancereife, um konkrete Risiken zu beseitigen, die im Einführungsplan identifiziert wurden. Diese Vorgehensweise stellt die mindestens erforderlichen Tools bereit, um eine konsistente Governance einzurichten, und das Team kann diese nachvollziehen. Dann werden die Tools erweitert, um allgemeine Probleme hinsichtlich der Governance zu lösen.

**ISO 27001-Blaupausen für die Compliance:** Wenn Ihre Organisation ISO-Compliancestandards einhalten muss, kann das [Blaupausenbeispiel „ISO 27001: Gemeinsame Dienste“](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared) als effektiveres MVP fungieren. Durch die Blaupause können umfassendere Governanceeinschränkungen bereits frühzeitig im iterativen Prozess zu generiert werden. Das [Blaupausenbeispiel „ISO 27001: App Service-Umgebungs-/SQL-Datenbank-Workload“](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload) baut auf der Blaupause für gemeinsame Dienste auf, um Kontrollen zuzuordnen und eine allgemeine Architektur für eine Anwendungsumgebung bereitzustellen.

**CAF-Zielzone (Cloud Adoption Framework) auf Unternehmensebene:** Es kann sein, dass Sie einen robusteren Ausgangspunkt für die Governance benötigen. In diesem Fall können Sie ggf. die [CAF-Zielzonen auf Unternehmensebene](../../ready/enterprise-scale/index.md) verwenden. Bei der CAF-Zielzone (Cloud Adoption Framework) auf Unternehmensebene stehen Einführungsteams im Fokus, die mittelfristig (innerhalb von 24 Monaten) das Ziel haben, mehr als 1.000 Assets (Anwendungen, Infrastruktur oder Datenassets) in der Cloud zu hosten. Die CAF-Zielzone auf Unternehmensebene ist die *erste Wahl* für komplexe Governanceszenarien für diese umfangreicheren Cloudeinführungsmaßnahmen.

### <a name="partnership-option-to-complete-prerequisites"></a>Partnerschaften zum Erfüllen von Voraussetzungen

**Microsoft Services**: Microsoft Services stellt Lösungsangebote bereit, die am Cloud Adoption Framework-Governancemodell, an Complianceblaupausen oder an Optionen der CAF-Zielzone auf Unternehmensebene ausgerichtet werden können. So können Sie sicherstellen, dass das am besten geeignete Governance- oder Compliancemodell zum Einsatz kommt. Nutzen Sie die Lösung [Secure Cloud Insights](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf), um sich ein datenbasiertes Bild von einer Kundenbereitstellung in Azure zu machen. Diese Lösung überprüft auch den Reifegrad der Azure-Implementierung des Kunden und ermittelt Optimierungsmöglichkeiten für vorhandene Bereitstellungsarchitekturen. Darüber hinaus trägt Secure Cloud Insights zur Senkung von Sicherheits- und Verfügbarkeitsrisiken im Zusammenhang mit der Governance bei. Basierend auf den Erkenntnissen sollten Sie folgende Ansätze ausführen:

- **Cloudgrundlagen**: Bestimmen Sie mithilfe der Lösung [Hybrid Cloud Foundation](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) die wichtigsten Entwürfe, Muster und die Governancearchitektur des Kunden für Azure. Ordnen Sie die Anforderungen des Kunden der jeweils am besten geeigneten Referenzarchitektur zu. Implementieren Sie ein Minimum Viable Product, bestehend aus gemeinsam genutzten Diensten und IaaS-Workloads.
- **Cloudmodernisierung**: Nutzen Sie die umfassende [Cloudmodernisierungslösung](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf), um Anwendungen, Daten und die Infrastruktur zu einer für Unternehmen konzipierten Cloud zu migrieren. Optimierungs- und Modernisierungsmaßnahmen können auch nach der Cloudbereitstellung ergriffen werden.
- **Innovationen in der Cloud**: Binden Sie den Kunden über das [Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) ein. Durch diese Lösung wird ein agiles Konzept zur Erfassung von Geschäftsanforderungen sowie zur Wiederverwendung von Bereitstellungspaketen implementiert (unter Einhaltung von Sicherheits-, Compliance- und Dienstverwaltungsrichtlinien). Außerdem wird sichergestellt, dass die Azure-Plattform mit operativen Prozeduren in Einklang steht.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Während der Bewertung müssen weitere Entscheidungen getroffen werden, um die Prozesse an den erforderlichen Governanceverfahren auszurichten. Das Cloudgovernanceteam stellt allen Mitgliedern des Cloudeinführungsteams vor der Bewertung einer Workload sämtliche Richtlinienanweisungen, Architekturrichtlinien sowie Anforderungen hinsichtlich Governance oder Compliance zur Verfügung.

### <a name="suggested-action-during-the-assessment-process"></a>Empfohlene Aktion während des Bewertungsprozesses

Die Anforderungen an die Bewertung von Governance und Compliance sind zu kundenspezifisch, um allgemeine Richtlinien zu den tatsächlichen Schritten zu erstellen, die während der Bewertung ausgeführt werden. Der Prozess muss Aufgaben und Zeit für die Ausrichtung an Compliance- und Governanceanforderungen beinhalten.

Ausführlichere Informationen zur Governance finden Sie in der Übersicht über die [Disziplinen der Cloudgovernance](../../govern/governance-disciplines.md). Dieser Abschnitt des Cloud Adoption Framework enthält Vorlagen zum Dokumentieren der Richtlinien, Anleitungen und Anforderungen für jede der folgenden Disziplinen:

- [Disziplin „Kostenverwaltung“](../../govern/cost-management/template.md)
- [Disziplin „Sicherheitsbaseline“](../../govern/security-baseline/template.md)
- [Disziplin „Ressourcenkonsistenz“](../../govern/resource-consistency/template.md)
- [Disziplin „Identitätsbaseline“](../../govern/identity-baseline/template.md)
- [Disziplin „Beschleunigung der Bereitstellung“](../../govern/deployment-acceleration/template.md)

Informationen zum Entwickeln von Governancerichtlinien basierend auf dem Cloud Adoption Framework-Governancemodell finden Sie unter [Implementieren einer Cloudgovernancestrategie](../../govern/corporate-policy.md).

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Während der Prozesse zum Optimieren und Höherstufen sollte das Cloudgovernanceteam Zeit investieren, um die Einhaltung von Governance- und Compliancestandards zu testen und zu überprüfen. Im Rahmen dieses Schritts kann das Cloudgovernanceteam auch sehr gut Vorlagen mit zusätzlichen Informationen für zukünftige Projekte zusammenstellen (insbesondere in der Disziplin „Beschleunigung der Bereitstellung“).

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Empfohlene Aktion während des Prozesses der Optimierung und Höherstufung

Der Projektplan muss während dieses Prozesses Zeitfenster enthalten, in denen das Cloudgovernanceteam eine Complianceüberprüfung für jede Workload durchführen kann, für die eine Höherstufung in die Produktion geplant ist.

## <a name="next-steps"></a>Nächste Schritte

Kehren Sie zur Prüfliste zurück, um ggf. weitere Anforderungen in Bezug auf den Umfang der Migration zu evaluieren.

> [!div class="nextstepaction"]
> [Checkliste für bewährte Migrationsmethoden](./index.md)
