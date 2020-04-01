---
title: Neues
description: Enthält Informationen zu Updates für das Framework für die Einführung der Microsoft Cloud (Microsoft Cloud Adoption Framework).
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: a3e316d49acaaee00d5ecd10efac9aa15c2dbd49
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353678"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework"></a>Neuerungen beim Framework für die Einführung der Microsoft Cloud

## <a name="fulfilling-the-vision"></a>Erfüllen der Vision

Das Framework ist jetzt allgemein verfügbar. Wir bauen dieses Framework jedoch weiterhin in Zusammenarbeit mit Kunden, Partnern und internen Teams aktiv auf. Um Partnerschaften zu ermutigen, werden Inhalte veröffentlicht, sobald diese verfügbar sind. Diese öffentlichen Releases ermöglichen es, die Anleitungen zu testen, zu validieren und schrittweise zu optimieren.

Wichtige Änderungen sind in den folgenden Versionshinweisen angegeben.

## <a name="migration-update-03022020"></a>Migrationsupdate: 02.03.2020

Mit diesem Release wird auf Feedback zur Kontinuität des Migrationsansatzes mithilfe mehrerer Methodiken, z. B. Strategie, Planung, Bereitschaft und Migration, reagiert. Das Ziel dieses Release besteht darin, Lesern das Verständnis der fortlaufenden Optimierung in Bezug auf die Planung und Einführung zu erleichtern, während Kunden mit der Migrationsjourney beschäftigt sind. Für dieses Release wurden die folgenden Änderungen vorgenommen:

### <a name="new-articles"></a>Neue Artikel

- [Ausgewogenheit konkurrierender Prioritäten](../strategy/balance-competing-priorities.md) Enthält eine Beschreibung der Ausgewogenheit von Prioritäten bei den einzelnen Methodiken in Bezug auf Kundenstrategien.
- [Klassifizierung bei Bewertungsprozessen](../migrate/migration-considerations/assess/classify.md): Enthält eine Beschreibung der Klassifizierung jeder Ressource und Workload vor der Migration.

### <a name="restructure-landing-zone-process"></a>Prozess zum Umstrukturieren der Zielzone

Die erste Zielzone stammt aus dem Leitfaden zur Bereitschaft und dient als eigener Abschnitt. Mit diesem Ansatz können wir das Konzept von Zielzonen und Zielzonenoptionen weiter ausführen. Dies hat auch zur Erstellung von einigen neuen Artikeln geführt:

- [Was ist eine Zielzone?](../ready/landing-zone/index.md): Enthält eine Definition des Begriffs „Zielzone“.
- [Erste Zielzone](../ready/landing-zone/first-landing-zone.md): Enthält weitere Informationen zum Vergleich verschiedener Zielzonen.
- [Bereitstellen einer Zielzone für die Migration](../ready/landing-zone/migrate-landing-zone.md): Wurde in den vorherigen Artikel zur Blaupause für die Migrationszielzone verschoben, um die Definition der CAF-Blaupause von der Auswahl der ersten Zielzone zu trennen, damit weitere Zielzonenoptionen möglich sind.
- Artikel zu [Terraform-Zielzonen](../ready/landing-zone/terraform-landing-zone.md): Wurde aus dem Abschnitt „Erweiterter Bereich“ der Bereitschaftsmethodik in den neuen Abschnitt „Zielzone“ der Methodik verschoben, um Terraform in Bezug auf Zielzonen als wichtige Komponente darzustellen.
- Die grundlegenden Aspekte von Zielzonen wurden im Inhaltsverzeichnis unter „Grundlegende Überlegungen zu Zielzonen“ zusammengefasst.
- Die bewährten Methoden zum Thema „Sicherheit“ wurden aus der Migrationsmethodik in den neuen Zielzonenabschnitt „Verbessern der Sicherheit von Zielzonen (sensible Daten)“ verschoben, um Lesern diese Anleitung zu einem früheren Zeitpunkt zur Verfügung zu stellen.

### <a name="refinements-to-the-azure-migration-guide"></a>Verbesserungen des Leitfadens zur Azure-Migration

Die Datenverkehrsmuster von Benutzern weisen darauf hin, dass dieser Abschnitt eher von Implementierern und Architekten bei der erstmaligen Migration genutzt wird. Zur besseren Unterstützung dieser Zielgruppe wurde die Schwerpunktsetzung des Migrationsleitfadens geändert, um besser das ursprünglich beabsichtigte Ziel zu erreichen, Leser über die Tools für eine erstmalige Migration zu informieren.

- [Übersicht](../migrate/azure-migration-guide/index.md): Klarere Beschreibung des Leitfadens mit einer verringerten Anzahl von Schritten.
- [Bewerten](../migrate/azure-migration-guide/assess.md): Verbesserte Darstellung, dass es bei der Bewertung in dieser Phase um die Bewertung der technischen Eignung einer bestimmten Workload und die zugehörigen Ressourcen geht. Der Abschnitt „Hinterfragen der Annahmen“ wurde hinzugefügt, um zu verdeutlichen, womit diese Bewertungsebene interagiert (erste Erwähnung des Ansatzes zur inkrementellen Bewertung in der Planmethodik).
- [Migration](../migrate/azure-migration-guide/migrate.md): Als Reaktion auf Feedback bei Tier 1-Konferenzen wurde den Drittanbieter-Tooloptionen ein Verweis auf UnifyCloud hinzugefügt.
- [Testen, Optimieren und Höherstufen](../migrate/azure-migration-guide/optimize-and-transform.md): Ausrichtung des Titels dieses Artikels auf andere Vorschläge zur Prozessverbesserung.

### <a name="refinements-to-migration-process-improvements"></a>Verbesserungen bei der Optimierung des Migrationsprozesses

- [Übersicht über die Bewertung](../migrate/migration-considerations/assess/index.md): Verbesserte Darstellung, dass es bei der Bewertung in dieser Phase um die Bewertung der technischen Eignung einer bestimmten Workload und die zugehörigen Ressourcen geht.
- [Checkliste für die Planung](../migrate/migration-considerations/prerequisites/planning-checklist.md): Verdeutlichung der Wichtigkeit einer Vorgangsausrichtung während der Planung von Migrationsmaßnahmen, um nach der Migration eine gut verwaltete Workload zu erhalten.

### <a name="placement-of-related-articles"></a>Platzierung verwandter Artikel

Alle unten angegebenen Artikellisten wurden verschoben. Der Datenverkehr wird an den neuen Speicherort umgeleitet.

- Artikel zu den [bewährten Methoden für die Bewertung](../plan/contoso-migration-assessment.md): Wurde aus dem Abschnitt „Bewährte Methoden“ der Migrationsmethodik in den neuen Abschnitt „Bewährte Methode“ der Planmethodik verschoben. Dank dieser Verschiebung wird Benutzern die Bewertung von lokalen Umgebungen zu einem früheren Zeitpunkt des Lebenszyklus präsentiert.
- Artikel zur [Ausgewogenheit des Portfolios](../strategy/balance-the-portfolio.md): Wurde aus dem Abschnitt „Erweiterter Bereich“ der Migrationsmethodik in die Strategiemethodik verschoben. Hierdurch stoßen Leser zu einem früheren Zeitpunkt des Lebenszyklus auf diesen Denkansatz.

### <a name="alignment-of-the-changes"></a>Angleichung von Änderungen

- [Sicherstellen der Umgebungsbereitschaft für den Cloudeinführungsplan](../ready/index.md): Die vier Schritte der Übersicht zur Bereitschaft wurden aktualisiert, damit sie den optimierten Prozess widerspiegeln.
- [Übersicht über die Migration](../migrate/index.md): Die Schritte der Übersicht zur Migration wurden aktualisiert, damit sie den optimierten Prozess widerspiegeln.
- [Grafik zur Migrationsmethodik](../migrate/index.md): Die Grafik der Methodik wurde aktualisiert, um die Änderungen widerzuspiegeln.
- [Übersichtsgrafik](../index.md): Die Übersichtsgrafik wurde aktualisiert, um die Änderungen widerzuspiegeln.
