---
title: Plattformautomatisierung und DevOps
description: Plattformautomatisierung und DevOps
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c8031c619eb419f72852fd8cd70e5540a80930d2
ms.sourcegitcommit: 4bbd5f6444d033ef1f38dc6f3bad7b914a82f68f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128089"
---
# <a name="platform-automation-and-devops"></a>Plattformautomatisierung und DevOps

![Plattformautomatisierung und DevOps](./media/DevOps.png)
_Abbildung 1: Plattformautomatisierung und DevOps_

## <a name="planning-for-a-devops-approach"></a>Planen eines DevOps-Ansatzes

Viele traditionelle Modelle für den IT-Betrieb sind nicht mit der Cloud kompatibel, und die Organisationen müssen betriebliche und organisatorische Veränderungen vornehmen, um die Migrationsziele des Unternehmens zu erreichen. Es wird dringend empfohlen, sowohl für Anwendungsteams als auch für zentrale Teams einen DevOps-Ansatz zu wählen.

**Überlegungen zum Entwurf:**

- Für zentrale Teams sollten CI/CD-Pipelines verwendet werden, um Richtliniendefinitionen, Rollendefinitionen, Richtlinienzuweisungen, Verwaltungsgruppenhierarchien und Abonnements zu verwalten. Diese Pipelines stellen sicher, dass mehrere Abonnements operativ verwaltet werden können, während gleichzeitig ein gewünschter Zustand beibehalten wird.

- Das reine Vorhandensein eines DevOps-Modells führt nicht sofort zu leistungsfähigen DevOps-Teams.

- Investitionen in technische Funktionen und Ressourcen sind von entscheidender Bedeutung.

- Sie können interne und externe DevOps-Rollen und -Funktionen aus einer Vielzahl von Quellen zusammenstellen, die der Strategie Ihrer Organisation entsprechen.

- Für einige Legacy-Apps verfügt das zugehörige App-Team möglicherweise nicht über die technischen Ressourcen, die für die Anpassung an eine DevOps-Strategie erforderlich sind.

<!-- cSpell:ignore PlatformOps SecOps NetOps AppDevOps AppDataOps AppSecOps -->

**Entwurfsempfehlungen:**

Richten Sie ein funktionsübergreifendes DevOps Plattformteam ein, um Ihre unternehmensweite Architektur aufzubauen, zu verwalten und zu warten. Diesem Team sollten Mitglieder aus Ihrem zentralen IT-Team, aus Sicherheits- und Complianceteams sowie aus Geschäftseinheiten angehören, um sicherzustellen, dass ein möglichst umfassendes Spektrum Ihres Unternehmens abgebildet wird. Die nachstehende Liste zeigt einen empfohlenen DevOps-Rollensatz für ein zentrales Plattformteam:

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

- Ermöglicht App-Besitzern das Erstellen und Verwalten von App-Ressourcen über ein DevOps-Modell. Die Liste unten zeigt die empfohlenen DevOps-Rollen für Anwendungsteams:

- **AppDevOps**

  - App-Migration oder -Transformation

  - App-Verwaltung und -Überwachung

  - RBAC (App-Ressourcen)

  - Sicherheitsüberwachung (App-Ressourcen)

  - Kostenverwaltung (App-Ressourcen)

  - Netzwerkverwaltung (App-Ressourcen)

  - In einigen Fällen möchten Sie AppDevOps möglicherweise in feiner abgestuften Rollen aufteilen, z. B. AppDataOps für die Datenbankverwaltung mit traditionellen Datenbankadministratorrollen oder AppSecOps, wenn es sich um Anwendungen mit höheren Sicherheitsanforderungen handelt.

- Stellen Sie eine zentrale App-DevOps-Funktion zur Unterstützung von Apps bereit, für die weder DevOps-Fähigkeiten vorhanden sind noch ein Geschäftsfall vorliegt, um diese Fähigkeiten bereitzustellen (z. B. Legacy-Apps mit minimalem Entwicklungsbedarf).

- Verwenden Sie einen richtliniengestützten Ansatz mit klaren RBAC-Grenzen, um über Anwendungsteams hinweg Konsistenz und Sicherheit zu erzwingen. So wird sichergestellt, dass durch eine Kombination von RBAC-Zuweisungen und Azure Policy ein Ansatz der geringsten Rechte verfolgt wird und die Workloads jederzeit mit den Azure Policy-Zuweisungen konform sind.

- Für eine beschleunigte Einführung von Azure sollte das zentrale Plattformteam einen gemeinsamen Satz mit Vorlagen und Bibliotheken erstellen, auf die die Anwendungsteams zurückgreifen können. Beispielsweise kann ein funktionsübergreifender Leitfaden dazu beitragen, Migrationen durch Fachbereichskompetenz zu unterstützen und eine Ausrichtung auf die gesamte Zielarchitektur auf Unternehmensebene zu gewährleisten.

- Beschränken Sie die Anwendungsteams nicht auf die Verwendung zentraler Artefakte oder Ansätze, da dies die Flexibilität einschränkt. Konsistente Baselinekonfigurationen können über einen richtliniengesteuerten Infrastrukturansatz und RBAC-Zuweisungen erzwungen werden. Dadurch wird sichergestellt, dass App-Teams (Geschäftseinheiten) flexibel genug sind, um Innovationen voranzutreiben, während gleichzeitig ein vordefinierter Satz mit Vorlagen genutzt wird.

- Zwingen Sie die Anwendungsteams nicht, einen zentralen Prozess oder eine zentrale Bereitstellungspipeline für die Instanziierung oder Verwaltung von App-Ressourcen zu verwenden. So ist sichergestellt, dass bestehende Teams, die bereits eine DevOps-Pipeline für die App-Bereitstellung nutzen, weiterhin dieselben Tools einsetzen können. Denken Sie daran, dass Sie weiterhin Azure Policy nutzen können, um Leitlinien festzulegen – unabhängig davon, wie Ressourcen in Azure eingesetzt werden.

## <a name="define-central-and-federated-responsibilities"></a>Definieren von zentralen und dezentralen Zuständigkeiten

Die Verteilung von Rollen, Zuständigkeiten und Vertrauensbeziehungen zwischen zentralen IT-Teams und App-Teams ist von entscheidender Bedeutung für die operativen Veränderungen, die Ihre Organisation bei der Einführung der Cloud im großen Stil durchlaufen müssen.

**Überlegungen zum Entwurf:**

Die zentralen Teams sind bestrebt, die vollständige Kontrolle zu behalten, während App-Besitzer versuchen, die Agilität zu maximieren. Die Balance zwischen diesen Zielen kann erheblichen Einfluss auf den Erfolg der Migration haben.

**Entwurfsempfehlungen:**

Die folgende Liste zeigt eine empfohlene Verteilung der Zuständigkeiten zwischen dem zentralen IT-Team und den Anwendungsteams, die darauf abzielt, Migrations-/Transformationsaktivitäten mit minimalen zentralen Abhängigkeiten zu ermöglichen und gleichzeitig die zentrale Steuerung von Sicherheit und Betriebsfähigkeit im gesamten Unternehmen zu unterstützen.

- **App-Funktionen**

  - App-Migration und/oder -Transformation

  - App-Verwaltung und -Überwachung (App-Ressourcen)

  - Schlüsselverwaltung (App-Schlüssel)

  - RBAC (App-Ressourcen)

  - Sicherheitsüberwachung (App-Ressourcen)

  - Kostenverwaltung (App-Ressourcen)

  - Netzwerkverwaltung (App-Ressourcen)

- **Zentrale Funktionen**

  - Kontrolle über die Architektur

  - Abonnementverwaltung

  - **Platform-as-Code** (Verwaltung von Vorlagen, Skripts und anderen Ressourcen)

  - Richtlinienverwaltung und -erzwingung (ganzheitlich)

  - Plattformverwaltung und -überwachung (ganzheitlich)

  - RBAC (ganzheitlich)

  - Schlüsselverwaltung (zentrale Dienste)

  - Netzwerkverwaltung (Netzwerke, virtuelle Netzwerkappliances und mehr)

  - Sicherheitsüberwachung (ganzheitlich)

  - Kostenverwaltung (ganzheitlich)

Ein Azure-DevOps-Modell, das auf diesen Empfehlungen basiert, bietet die gewünschte Kontrolle für zentrale Teams und die von den Anwendungsteams benötigte Migrationsflexibilität.
