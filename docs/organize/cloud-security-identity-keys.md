---
title: Funktion von Identitäts- und Schlüsselverwaltung in der Cloud
description: Grundlegendes zur Funktion der Identitäts- und Schlüsselverwaltung in der Cloud.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 04/30/2020
ms.openlocfilehash: b23cc2be9398a3512de95b5e2312b30764de8695
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230258"
---
# <a name="function-of-identity-and-key-management-in-the-cloud"></a>Funktion von Identitäts- und Schlüsselverwaltung in der Cloud

Das Hauptziel eines Sicherheitsteams, das an der Identitätsverwaltung arbeitet, besteht darin, die Authentifizierung und Autorisierung von Menschen, Diensten, Geräten und Anwendungen bereitzustellen. Die Schlüssel- und Zertifizierungsverwaltung bietet sichere Verteilung und sicheren Zugriff auf das Schlüsselmaterial für kryptografische Vorgänge (die häufig ähnliche Ergebnisse wie die Identitätsverwaltung unterstützen).

## <a name="modernization"></a>Modernisierung

Die Modernisierung der Datenidentitäts- und Schlüsselverwaltung wird wie folgt strukturiert:

- Die Disziplinen der Identitäts- und Schlüssel-/Zertifizierungsverwaltung nähern sich an, da beide Zusicherungen für Authentifizierung und Autorisierung bereitstellen, um sichere Kommunikation zu ermöglichen.
- Identitätskontrollen entwickeln sich zum primären Sicherheitsumkreis für Cloudanwendungen.
- Die schlüsselbasierte Authentifizierung für Clouddienste wird durch die Identitätsverwaltung ersetzt, weil es schwierig ist, den Zugriff auf diese Schlüssel zu speichern und sicher bereitzustellen.
- Die kritische Wichtigkeit, positive Lektionen, die von lokalen Identitätsarchitekturen wie einzelne Identität, Einmaliges Anmelden (Single Sign-On, SSO) und nativer Anwendungsintegration gelernt wurden, mitzunehmen.
- Die kritische Wichtigkeit, häufige Fehler lokaler Architekturen zu vermeiden, die diese häufig stark verkompliziert haben, was den Support erschwert und Angriffe vereinfacht. Dazu gehören:
  - Ausgedehnte Gruppen und Organisationseinheiten.
  - Ausgedehnter Satz von Verzeichnissen und Identitätsverwaltungssystemen von Drittanbietern.
  - Fehlende klare Standardisierung und Besitz der Anwendungsidentitätsstrategie.
- Angriffe zum Diebstahl von Anmeldeinformationen bleiben eine Bedrohung mit großen Auswirkungen und von hoher Wahrscheinlichkeit, die es zu abzumildern gilt.
- Dienstkonten und Anwendungskonten bleiben weiterhin eine der größten Herausforderungen, deren Lösung jedoch leichter wird. Identitätsteams sollten die Cloudfunktionen, die dies lösen, aktiv nutzen, so z. B. [verwaltete Identitäten von Azure AD](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Identitäts- und Schlüsselverwaltungsteams müssen starke Beziehungen mit den folgenden Rollen aufbauen:

- IT-Architektur und -Betrieb
- Sicherheitsarchitektur und -betrieb
- Entwicklungsteams
- Datensicherheitsteams
- Datenschutzteams
- Juristische Teams
- Compliance-/Risikomanagementteams

## <a name="next-steps"></a>Nächste Schritte

Machen Sie sich mit der Funktion der [Infrastruktur und Endpunktsicherheit](./cloud-security-infrastructure-endpoint.md) vertraut.
