---
title: Funktion von Identitäts- und Schlüsselverwaltung in der Cloud
description: Grundlegendes zur Funktion der Identitäts- und Schlüsselverwaltung in der Cloud.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 7942cc63341b3f15f770d6f23dca3e56bc606b65
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88574736"
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
- Dienstkonten und Anwendungskonten bleiben weiterhin eine der größten Herausforderungen, deren Lösung jedoch leichter wird. Identitätsteams sollten die Cloudfunktionen, die dies lösen, aktiv nutzen, so z. B. [verwaltete Identitäten von Azure AD](/azure/active-directory/managed-identities-azure-resources/overview).

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
