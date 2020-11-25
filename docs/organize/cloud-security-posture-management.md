---
title: Funktion der Verwaltung des Cloudsicherheitsstatus
description: Grundlegendes zur Funktion der Verwaltung des Cloudsicherheitsstatus.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 96bb73571c0f876f90f2e3132cb8751232bae653
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94996314"
---
<!-- docsTest:casing TVM -->

# <a name="function-of-cloud-security-posture-management"></a>Funktion der Verwaltung des Cloudsicherheitsstatus

Das Hauptziel eines Cloudsicherheitteams, das an der Statusverwaltung arbeitet, besteht darin, den Sicherheitsstatus der Organisation fortlaufend zu melden und zu verbessern, indem es sich auf die Unterbindung des potenziellen Erfolgs eines Angreifers konzentriert.

## <a name="modernization"></a>Modernisierung

Die Statusverwaltung besteht aus eine Reihe neuer Funktionen, die viele bisher nur imaginierte oder versuchte Ideen realisieren, die vor der Einführung der Cloud schwierig oder unmöglich waren oder mit einem extrem hohen manuellen Aufwand einhergingen. Einige der Elemente der Statusverwaltung lassen sich auf Zero Trust, Beseitigung des Umkreisnetzwerks, kontinuierliche Überwachung und manuelle Bewertung von Risiken durch beratende Experten zurückführen.

Die Statusverwaltung führt hierfür einen strukturierten Ansatz ein, wobei Folgendes verwendet wird:

- **Zero Trust-basierte Zugriffssteuerung:** Dabei wird die aktive Bedrohungsstufe bei Entscheidungen zur Zugriffssteuerung berücksichtigt.
- **Risikobewertung in Echtzeit:** Um Transparenz zu den wichtigsten Risiken zu bieten.
- **Bedrohungs- und Sicherheitsrisikoverwaltung (TVM)** , um eine ganzheitliche Sicht der Angriffsfläche und des Risikos von Organisationen zu ermöglichen und diese in die Entscheidungsfindung zum Betrieb und Engineering zu integrieren.
- **Ermitteln von Freigaberisiken:** Um die Exposition von Daten des unternehmerischen geistigen Eigentums in sowohl sanktionierten als auch nicht sanktionierten Clouddiensten zu verstehen.
- **Verwaltung des Cloudsicherheitsstatus**, um Vorteile der Cloudinstrumentierung zu nutzen, um Sicherheitsverbesserungen zu überwachen und zu priorisieren.
- **Technische Richtlinie:** Anwenden von Sicherungen, um die Standards und Richtlinien der Organisation auf technischen Systemen zu überwachen und dort zu erzwingen. Siehe Azure Policy und [Azure Blueprints](/azure/governance/blueprints/overview).
- Systeme und Architekturen sowie spezifische Anwendungen zur **Bedrohungsmodellierung**.

**Resultierende Disziplin:** Die Sicherheitsstatusverwaltung unterbricht viele Normen der Sicherheitsorganisation auf positive Weise mit diesen neuen Funktionen und kann Zuständigkeiten zwischen Rollen verlagern oder neue Rollen erzeugen.

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Die Sicherheitsstatusverwaltung ist eine sich entwickelnde Funktion, sodass es sich dabei um ein dediziertes Team handeln kann, oder sie kann auch von anderen Teams bereitgestellt werden.

Die Sicherheitsstatusverwaltung sollte eng mit den folgenden Teams zusammenarbeiten:

- Threat Intelligence-Team
- Informationstechnologie
- Compliance- und Risikomanagementteams
- Geschäftsführer und SMEs
- Sicherheitsarchitektur und -betrieb
- Überwachungsteam

## <a name="next-steps"></a>Nächste Schritte

Sehen Sie sich die Funktion der [Vorbereitung auf Cloudsicherheitsvorfälle](./cloud-security-incident-preparation.md) an.
