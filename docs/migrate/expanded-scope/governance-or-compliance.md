---
title: Strategie für Governance bzw. Compliance
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Strategie für Governance bzw. Compliance
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6c1ac4000f5b79d6b177e8703f5e58b6dd9c9e56
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022733"
---
# <a name="governance-or-compliance-strategy"></a>Strategie für Governance bzw. Compliance

Wenn in einem Migrationsprojekt Anforderungen an Governance oder Compliance bestehen, muss der Umfang erweitert werden. Die folgende Anleitung erweitert den Umfang des [Azure-Migrationsleitfadens](../azure-migration-guide/index.md), um verschiedene Vorgehensweisen für Governance- oder Complianceanforderungen zu erläutern.

## <a name="general-scope-expansion"></a>Erweiterung des allgemeinen Umfangs

Anforderungen hinsichtlich Governance oder Compliance wirken sich am meisten auf Aktivitäten zum Erfüllen von Voraussetzungen aus. Während der Bewertung, Migration und Optimierung sind möglicherweise weitere Anpassungen erforderlich.

## <a name="suggested-prerequisites"></a>Empfohlene Voraussetzungen

Die Konfiguration der grundlegenden Azure-Umgebung kann sich erheblich ändern, wenn Anforderungen hinsichtlich Governance oder Compliance ins Spiel kommen. Um zu verstehen, wie sich die Voraussetzungen ändern, müssen Sie die Art der Anforderungen kennen. Vor Beginn einer Migration, die Governance oder Compliance erfordert, muss eine Vorgehensweise ausgewählt und in die Cloudumgebung implementiert werden. Im Folgenden finden Sie einige allgemeine Vorgehensweisen, die in Migrationsprozessen häufig zu finden sind:

**Allgemeine Vorgehensweise für die Governance**: Für die meisten Organisationen ist das [Cloud Adoption Framework-Governancemodell](../../govern/guides/index.md) ausreichend. Dieses besteht aus der Implementierung eines Minimum Viable Product (MVP, mindestens überlebensfähiges Produkt), gefolgt von zielgerichteten Iterationen der Governancereife, um konkrete Risiken anzugehen, die im Einführungsplan identifiziert wurden. Diese Vorgehensweise stellt die mindestens erforderlichen Tools bereit, um eine konsistente Governance einzurichten, und das Team kann diese nachvollziehen. Dann werden die Tools erweitert, um allgemeine Probleme hinsichtlich der Governance zu lösen.

**ISO 27001-Blaupausen für die Compliance**: Für Kunden, die Compliancestandards gemäß ISO einhalten müssen, kann das [Blaupausenbeispiel „ISO 27001: Gemeinsame Dienste“](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared/index) als effektiveres MVP dienen, um umfassendere Governanceeinschränkungen bereits frühzeitig im iterativen Prozess zu generieren. Das [Blaupausenbeispiel „ISO 27001: App Service-Umgebungs-/SQL-Datenbank-Workload“](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload) baut auf dieser Blaupause auf, um Kontrollen zuzuordnen und eine allgemeine Architektur für eine Anwendungsumgebung bereitzustellen. Wenn weitere Blaupausen für die Compliance veröffentlicht werden, werden wir hier auch auf diese verweisen.

**Virtuelles Rechenzentrum**: Ein robusterer Ausgangspunkt für die Governance kann erforderlich sein. Ziehen Sie in solchen Fällen das [virtuelle Azure-Rechenzentrum](../../reference/vdc.md) (Virtual Datacenter, VDC) in Betracht. Dieser Ansatz wird häufig bei einer unternehmensweiten Einführung vorgeschlagen, insbesondere bei einem Umfang von über 10.000 Ressourcen. Er ist im Allgemeinen auch die erste Wahl für komplexe Governanceszenarien, wenn eine der folgenden Anforderungen erfüllt sein muss: umfangreiche Complianceanforderungen von Drittanbietern, tiefgreifendes Fachwissen oder Parität mit ausgereiften IT-Governancerichtlinien und Complianceanforderungen.

### <a name="partnership-option-to-complete-prerequisites"></a>Partnerschaften zum Erfüllen von Voraussetzungen

**Microsoft Services**: Microsoft Services stellt Lösungsangebote bereit, die am Cloud Adoption Framework-Governancemodell, an Complianceblaupausen oder an Optionen des virtuellen Rechenzentrums ausgerichtet werden können, um sicherzustellen, dass das am besten geeignete Modell für Governance bzw. Compliance zum Einsatz kommt. Nutzen Sie das Lösungsangebot [Secure Cloud Insights (SCI)](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf), um ein datengesteuertes Bild einer Kundenbereitstellung in Azure zu erhalten und den Reifegrad der Azure-Implementierung des Kunden zu überprüfen. Gleichzeitig lässt sich ermitteln, ob vorhandene Bereitstellungsarchitekturen optimiert und Sicherheits- und Verfügbarkeitsrisiken hinsichtlich der Governance eliminiert werden können. Basierend auf den Erkenntnissen sollten Sie folgende Ansätze ausführen:

- **Cloudgrundlagen**: Legen Sie mithilfe des Lösungsangebots [Hybrid Cloud Foundation (HCF)](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) die wichtigsten Entwürfe, Muster und die Governancearchitektur des Kunden für Azure fest. Ordnen Sie die Anforderungen des Kunden der jeweils am besten geeigneten Referenzarchitektur zu. Implementieren Sie ein Minimum Viable Product, bestehend aus gemeinsam genutzten Diensten und IaaS-Workloads.
- **Cloudmodernisierung**: Nutzen Sie das Lösungsangebot [Cloud Modernization](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) (Cloudmodernisierung) als umfassende Vorgehensweise zum Verschieben von Anwendungen, Daten und Infrastrukturen in eine unternehmensfähige Cloud sowie zum Optimieren und Modernisieren, sobald sich alle Elemente in der Cloud befinden.
- **Innovationen in der Cloud**: Begeistern Sie Ihre Kunden mit einem innovativen und einzigartigen Cloudkompetenzzentrum: [Cloud Center of Excellence (CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf). Mit diesem Lösungsansatz lässt sich eine moderne IT-Organisation aufbauen, in der Kunden Agilität bei DevOps-Prozessen erzielen und jederzeit das Steuer in der Hand behalten. So implementieren Sie eine agile Verfahrensweise, um Geschäftsanforderungen zu erfassen, Bereitstellungspakete im Rahmen von Sicherheits-, Compliance- und Dienstverwaltungsrichtlinien wiederzuverwenden und die Azure-Plattform gemäß operativen Prozeduren zu verwalten.

## <a name="assess-process-changes"></a>Änderungen am Bewertungsprozess

Während der Bewertung müssen weitere Entscheidungen getroffen werden, um die Prozesse an den erforderlichen Governanceverfahren auszurichten. Das Cloudgovernanceteam muss allen Mitgliedern des Cloudeinführungsteams sämtliche Richtlinienanweisungen, Architekturrichtlinien sowie Anforderungen hinsichtlich Governance und Compliance vor der Bewertung einer Workload zur Verfügung stellen.

### <a name="suggested-action-during-the-assess-process"></a>Empfohlene Aktion während des Bewertungsprozesses

Die Anforderungen an die Bewertung von Governance und Compliance sind zu kundenspezifisch, um allgemeine Richtlinien zu den tatsächlichen Schritten zu erstellen, die während der Bewertung ausgeführt werden. Es wird jedoch empfohlen, dass der Prozess Aufgaben und eine zeitliche Planung für die „Ausrichtung an Compliance-/Governanceanforderungen“ enthält. Weitere Informationen zu diesen Anforderungen finden Sie unter den folgenden Links:

Detaillierte Informationen zur Governance finden Sie in der [Übersicht über die fünf Disziplinen der Cloudgovernance](../../govern/governance-disciplines.md). Der Abschnitt zum Cloud Adoption Framework enthält auch Vorlagen zum Dokumentieren von Richtlinien, Anleitungen und Anforderungen für jede der fünf Disziplinen:

- [Kostenmanagement](../../govern/cost-management/template.md)
- [Sicherheitsbaseline](../../govern/security-baseline/template.md)
- [Ressourcenkonsistenz]../../govern/resource-consistency/template.md)
- [Identitätsbaseline]../../govern/identity-baseline/template.md)
- [Beschleunigung der Bereitstellung](../../govern/deployment-acceleration/template.md)

Anleitungen zum Entwickeln von Governancerichtlinien basierend auf dem Cloud Adoption Framework-Governancemodell finden Sie unter [Implementieren einer Cloudgovernancestrategie](../../govern/corporate-policy.md).

## <a name="optimize-and-promote-process-changes"></a>Änderungen am Prozess zum Optimieren und Höherstufen

Während der Prozesse zum Optimieren und Höherstufen empfiehlt es sich, dass das Cloudgovernanceteam Zeit investiert, um die Einhaltung von Governance- und Compliancestandards zu testen und zu überprüfen. Dieser Schritt ist auch ein guter Zeitpunkt, um Prozesse einzuführen, mit denen das Cloudgovernanceteam Vorlagen zusammenstellen kann, mit denen sich in zukünftigen Projekten die [Bereitstellung beschleunigen](../../govern/deployment-acceleration/index.md) lässt.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Empfohlene Aktion während des Prozesses der Optimierung und Höherstufung

In diesem Prozess sollte der Projektplan Zeitpunkte enthalten, zu denen das Cloudgovernanceteam eine Complianceüberprüfung für jede Workload durchführen kann, die für die Höherstufung in die Produktion geplant ist.

## <a name="next-steps"></a>Nächste Schritte

Der letzte Punkt auf der [Checkliste für den erweiterten Umfang](./index.md) empfiehlt dem Leser, zur Checkliste zurückzukehren und weitere Anforderungen in Bezug auf den Umfang der Migration erneut zu evaluieren.

> [!div class="nextstepaction"]
> [Checkliste für erweiterten Umfang](./index.md)
