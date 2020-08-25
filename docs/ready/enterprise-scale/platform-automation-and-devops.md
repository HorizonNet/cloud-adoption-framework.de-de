---
title: Plattformautomatisierung und DevOps
description: Plattformautomatisierung und DevOps
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c914d971b97e72d1b5e303fdec7a0df17351b423
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88574413"
---
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

- Für einige Legacy-Apps verfügt das zugehörige App-Team möglicherweise nicht über die technischen Ressourcen, die für die Anpassung an eine DevOps-Strategie erforderlich sind.

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

- **AppDevOps** Ermöglicht App-Besitzern das Erstellen und Verwalten von App-Ressourcen über ein DevOps-Modell. Die folgende Liste zeigt die empfohlenen DevOps-Rollen für Anwendungsteams:

  - App-Migration oder -Transformation

  - App-Verwaltung und -Überwachung

  - RBAC (App-Ressourcen)

  - Sicherheitsüberwachung (App-Ressourcen)

  - Kostenverwaltung (App-Ressourcen)

  - Netzwerkverwaltung (App-Ressourcen)

  - In einigen Fällen möchten Sie AppDevOps vielleicht in differenziertere Rollen aufteilen, z. B. AppDataOps für die Datenbankverwaltung oder AppSecOps für sicherheitsrelevantere Apps.

  - Stellen Sie eine zentrale App-DevOps-Funktion zur Unterstützung von Apps bereit, für die weder DevOps-Fähigkeiten vorhanden sind noch ein Geschäftsfall vorliegt, um diese Fähigkeiten bereitzustellen (z. B. Legacy-Apps mit minimalem Entwicklungsbedarf).

  - Verwenden Sie einen richtliniengestützten Ansatz mit klaren RBAC-Grenzen, um über Anwendungsteams hinweg Konsistenz und Sicherheit zu erzwingen. So wird sichergestellt, dass durch eine Kombination von RBAC-Zuweisungen und Azure Policy ein Ansatz der geringsten Rechte verfolgt wird und die Workloads jederzeit mit den Azure Policy-Zuweisungen konform sind.

  - Für eine beschleunigte Einführung von Azure sollte das zentrale Plattformteam einen gemeinsamen Satz mit Vorlagen und Bibliotheken erstellen, auf die die Anwendungsteams zurückgreifen können. Beispielsweise kann ein funktionsübergreifender Leitfaden dazu beitragen, Migrationen durch Fachbereichskompetenz zu unterstützen und eine Ausrichtung auf die gesamte Zielarchitektur auf Unternehmensebene zu gewährleisten.

  - Beschränken Sie die Anwendungsteams nicht auf die Verwendung zentraler Artefakte oder Ansätze, da dies ihre Flexibilität einschränkt. Sie können konsistente Baselinekonfigurationen über einen richtliniengesteuerten Infrastrukturansatz und RBAC-Zuweisungen erzwingen. Dadurch wird sichergestellt, dass App-Teams (Geschäftseinheiten) flexibel genug sind, um Innovationen voranzutreiben, während gleichzeitig ein vordefinierter Satz mit Vorlagen genutzt wird.

  - Zwingen Sie die Anwendungsteams nicht, einen zentralen Prozess oder eine zentrale Bereitstellungspipeline für die Instanziierung oder Verwaltung von App-Ressourcen zu verwenden. Bestehende Teams, die bereits eine DevOps-Pipeline für die App-Bereitstellung nutzen, sollten weiterhin dieselben Tools einsetzen können. Denken Sie daran, dass Sie weiterhin Azure Policy nutzen können, um Leitlinien festzulegen – unabhängig davon, wie Ressourcen in Azure eingesetzt werden.

## <a name="define-central-and-federated-responsibilities"></a>Definieren von zentralen und dezentralen Zuständigkeiten

Die Verteilung von Rollen, Zuständigkeiten und Vertrauensbeziehungen zwischen zentralen IT-Teams und App-Teams ist von entscheidender Bedeutung für die operativen Veränderungen, die Ihre Organisation bei der Einführung der Cloud im großen Stil durchlaufen müssen.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

Die zentralen Teams sind bestrebt, die vollständige Kontrolle zu behalten, während App-Besitzer versuchen, die Agilität zu maximieren. Die Balance zwischen diesen Zielen kann erheblichen Einfluss auf den Erfolg der Migration haben.

### <a name="design-recommendations"></a>Entwurfsempfehlungen

Die folgende Liste enthält eine empfohlene Verteilung der Zuständigkeiten zwischen dem zentralen IT-Team und den Anwendungsteams. Sie sind bestrebt, Migrations- und Transformationsaktivitäten mit minimalen zentralen Abhängigkeiten zu ermöglichen. Gleichzeitig möchten Sie die zentralisierte Governance von Sicherheit und Betriebsfähigkeit für die gesamte Umgebung unterstützen.

- **App-Funktionen**

  - App-Migration und -Transformation

  - App-Verwaltung und -Überwachung (App-Ressourcen)

  - Schlüsselverwaltung (App-Schlüssel)

  - RBAC (App-Ressourcen)

  - Sicherheitsüberwachung (App-Ressourcen)

  - Kostenverwaltung (App-Ressourcen)

  - Netzwerkverwaltung (App-Ressourcen)

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
