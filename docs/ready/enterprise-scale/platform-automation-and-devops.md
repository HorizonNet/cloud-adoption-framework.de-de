---
title: Plattformautomatisierung und DevOps
description: Plattformautomatisierung und DevOps
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 8e6e052c86964ae11d32a491c36d5ee4e1457e0d
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447267"
---
<!-- docutune:casing PlatformOps AppDevOps AppDataOps AppSecOps -->

# <a name="platform-automation-and-devops"></a>Plattformautomatisierung und DevOps

![Diagramm: Plattformautomatisierung und DevOps](./media/DevOps.png)

_Abbildung 1: Plattformautomatisierung und DevOps_

## <a name="planning-for-a-devops-approach"></a>Planen eines DevOps-Ansatzes

Viele traditionelle Modelle für den IT-Betrieb sind nicht mit der Cloud kompatibel, und die Organisationen müssen betriebliche und organisatorische Veränderungen vornehmen, um die Migrationsziele des Unternehmens zu erreichen. Sie sollten sowohl für Anwendungsteams als auch für zentrale Teams einen DevOps-Ansatz wählen.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

- Für zentrale Teams sollten Sie für Continuous Integration und Continuous Deployment Pipelines verwenden. Verwenden Sie die Pipelines zur Verwaltung von Richtliniendefinitionen, Rollendefinitionen, Richtlinienzuweisungen, Verwaltungsgruppenhierarchien und Abonnements. Diese Pipelines tragen dazu bei, sicherzustellen, dass Sie mehrere Abonnements operativ verwalten können und gleichzeitig einem gewünschten Zustand entsprechen.

- Die reine Anwendung eines DevOps-Modells führt nicht sofort zu leistungsfähigen DevOps-Teams.

- Investitionen in technische Funktionen und Ressourcen sind von entscheidender Bedeutung.

- Sie können interne und externe DevOps-Rollen und -Funktionen aus einer Vielzahl von Quellen zusammenstellen, die der Strategie Ihrer Organisation entsprechen.

- Für einige Legacyanwendungen verfügt das zugehörige Anwendungsteam möglicherweise nicht über die Entwicklungsressourcen, die für die Anpassung an eine DevOps-Strategie erforderlich sind.

<!-- cSpell:ignore PlatformOps SecOps NetOps AppDevOps AppDataOps AppSecOps -->

### <a name="design-recommendations"></a>Entwurfsempfehlungen

Richten Sie ein funktionsübergreifendes DevOps Plattformteam ein, um Ihre unternehmensweite Architektur aufzubauen, zu verwalten und zu warten. Diesem Team sollten Mitglieder aus Ihrem zentralen IT-Team, aus Sicherheits- und Complianceteams sowie aus Geschäftseinheiten angehören, um sicherzustellen, dass ein möglichst umfassendes Spektrum Ihres Unternehmens abgebildet wird. Die folgende Liste zeigt einen empfohlenen DevOps-Rollensatz für ein zentrales Plattformteam:

- **PlatformOps** (Platform Operations) für:

  - Abonnementbereitstellung und Delegierung der erforderlichen Richtlinien für Netzwerk-, Identitäts- und Zugriffsverwaltung

  - Plattformverwaltung und -überwachung (ganzheitlich)

  - Kostenverwaltung (ganzheitlich)

  - Platform-as-Code (Verwaltung von Vorlagen, Skripts und anderen Ressourcen)

  - Verantwortlich für den gesamten Betrieb von Microsoft Azure innerhalb des Azure Active Directory-Mandanten (Verwaltung von Dienstprinzipalen, Graph-API-Registrierung und Definition von Rollen)

- **SecOps** (Security Operations)

  - Rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) (ganzheitlich)

  - Schlüsselverwaltung (für zentrale Dienste, SMTP und Domänencontroller)

  - Richtlinienverwaltung und -erzwingung (ganzheitlich)

  - Sicherheitsüberwachung (ganzheitlich)

- **NetOps** (Network Operations)

  - Netzwerkverwaltung (ganzheitlich)

- **AppDevOps.** Ermöglichen Sie Anwendungsbesitzern das Erstellen und Verwalten von Anwendungsressourcen über ein DevOps-Modell. Die folgende Liste zeigt die empfohlenen DevOps-Rollen für Anwendungsteams:

  - Anwendungsmigration oder -transformation

  - Anwendungsverwaltung und -überwachung

  - RBAC (Anwendungsressourcen)

  - Sicherheitsüberwachung (Anwendungsressourcen)

  - Kostenverwaltung (Anwendungsressourcen)

  - Netzwerkverwaltung (Anwendungsressourcen)

  - In einigen Fällen sollten Sie AppDevOps in differenziertere Rollen unterteilen, z. B. AppDataOps für die Datenbankverwaltung oder AppSecOps für sicherheitsrelevantere Anwendungen.

  - Stellen Sie eine zentrale Anwendungs-DevOps-Funktion zur Unterstützung von Anwendungen bereit, für die weder DevOps-Funktionen vorhanden sind noch ein Geschäftsszenario vorliegt, um diese Funktionen bereitzustellen (z. B. Legacyanwendungen mit minimalen Entwicklungsfunktionen).

  - Verwenden Sie einen richtliniengestützten Ansatz mit klaren RBAC-Grenzen, um über Anwendungsteams hinweg Konsistenz und Sicherheit zu erzwingen. So wird sichergestellt, dass durch eine Kombination von RBAC-Zuweisungen und Azure Policy ein Ansatz der geringsten Rechte verfolgt wird und die Workloads jederzeit mit den Azure Policy-Zuweisungen konform sind.

  - Für eine beschleunigte Einführung von Azure sollte das zentrale Plattformteam einen gemeinsamen Satz mit Vorlagen und Bibliotheken erstellen, auf die die Anwendungsteams zurückgreifen können. Beispielsweise kann ein funktionsübergreifender Leitfaden dazu beitragen, Migrationen durch Fachbereichskompetenz zu unterstützen und eine Ausrichtung auf die gesamte Zielarchitektur auf Unternehmensebene zu gewährleisten.

  - Beschränken Sie die Anwendungsteams nicht auf die Verwendung zentraler Artefakte oder Ansätze, da dies ihre Flexibilität einschränkt. Sie können konsistente Baselinekonfigurationen über einen richtliniengesteuerten Infrastrukturansatz und RBAC-Zuweisungen erzwingen. Dadurch wird sichergestellt, dass Anwendungsteams (Geschäftseinheiten) flexibel genug für Innovationen sind, gleichzeitig aber eine vordefinierte Reihe von Vorlagen nutzen können.

  - Zwingen Sie die Anwendungsteams nicht, einen zentralen Prozess oder eine zentrale Bereitstellungspipeline für die Instanziierung oder Verwaltung von Anwendungsressourcen zu verwenden. Bestehende Teams, die bereits eine DevOps-Pipeline für die Anwendungsbereitstellung verwenden, sollten weiterhin dieselben Tools einsetzen können. Denken Sie daran, dass Sie dennoch Azure Policy nutzen können, um Schutzrichtlinien festzulegen – unabhängig davon, wie Ressourcen in Azure bereitgestellt werden.

## <a name="define-central-and-federated-responsibilities"></a>Definieren von zentralen und dezentralen Zuständigkeiten

Die Verteilung von Rollen, Zuständigkeiten und Vertrauensbeziehungen zwischen den zentralen IT-Teams und Anwendungsteams ist von entscheidender Bedeutung für die operativen Veränderungen, die Ihre Organisation bei der Einführung der Cloud im großen Stil durchlaufen muss.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

Die zentralen Teams möchten die vollständige Kontrolle behalten, während Anwendungsbesitzer die Flexibilität maximieren möchten. Die Balance zwischen diesen Zielen kann erheblichen Einfluss auf den Erfolg der Migration haben.

### <a name="design-recommendations"></a>Entwurfsempfehlungen

Die folgende Liste enthält eine empfohlene Verteilung der Zuständigkeiten zwischen dem zentralen IT-Team und den Anwendungsteams. Sie sind bestrebt, Migrations- und Transformationsaktivitäten mit minimalen zentralen Abhängigkeiten zu ermöglichen. Gleichzeitig möchten Sie die zentralisierte Governance von Sicherheit und Betriebsfähigkeit für die gesamte Umgebung unterstützen.

- **Anwendungsfunktionen**

  - Anwendungsmigration und -transformation

  - Anwendungsverwaltung und -überwachung (Anwendungsressourcen)

  - Schlüsselverwaltung (Anwendungsschlüssel)

  - RBAC (Anwendungsressourcen)

  - Sicherheitsüberwachung (Anwendungsressourcen)

  - Kostenverwaltung (Anwendungsressourcen)

  - Netzwerkverwaltung (Anwendungsressourcen)

- **Zentrale Funktionen**

  - Kontrolle über die Architektur

  - Abonnementverwaltung

  - Platform-as-Code (Verwaltung von Vorlagen, Skripts und anderen Ressourcen)

  - Richtlinienverwaltung und -erzwingung (ganzheitlich)

  - Plattformverwaltung und -überwachung (ganzheitlich)

  - RBAC (ganzheitlich)

  - Schlüsselverwaltung (zentrale Dienste)

  - Netzwerkverwaltung (einschließlich Netzwerken und virtuellen Netzwerkgeräten)

  - Sicherheitsüberwachung (ganzheitlich)

  - Kostenverwaltung (ganzheitlich)

Ein Azure-DevOps-Modell, das auf diesen Empfehlungen basiert, bietet die gewünschte Kontrolle für zentrale Teams und die von den Anwendungsteams benötigte Migrationsflexibilität.
