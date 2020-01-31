---
title: Metriken, Indikatoren und Risikotoleranz für die Identitätsbaseline
description: Metriken, Indikatoren und Risikotoleranz für die Identitätsbaseline
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f5002d278e833873a2077538c848bc5e7f47131d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806032"
---
# <a name="identity-baseline-metrics-indicators-and-risk-tolerance"></a>Metriken, Indikatoren und Risikotoleranz für die Identitätsbaseline

Dieser Artikel unterstützt Sie bei der Quantifizierung der Geschäftsrisikotoleranz im Zusammenhang mit der Identitätsbaseline. Das Definieren von Metriken und Indikatoren ermöglicht das Erstellen eines Geschäftsszenarios, mit dem Sie in die Weiterentwicklung der Disziplin „Identitätsbaseline“ investieren können.

## <a name="metrics"></a>Metriken

Die Identitätsbaseline legt den Schwerpunkt auf das Identifizieren, Authentifizieren und Autorisieren von Personen, Benutzergruppen oder automatisierten Prozessen und bietet ihnen den entsprechenden Zugriff auf Ressourcen in Ihren Cloudbereitstellungen. Im Rahmen der Risikoanalyse sollten Sie Daten zu Ihren Identitätsdiensten sammeln, um zu ermitteln, welches Risiko vorliegt und wie wichtig Investitionen in die Governance der Identitätsbaseline für Ihre geplanten Cloudbereitstellungen ist.

Es folgen Beispiele für nützliche Metriken, die Sie erfassen sollten, um die Risikotoleranz innerhalb der Disziplin „Identitätsbaseline“ zu bewerten:

- **Größe von Identitätssystemen.** Die Gesamtanzahl von Benutzern, Gruppen oder anderen Objekte, die über Ihre Identitätssysteme verwaltet werden.
- **Gesamtgröße der Verzeichnisdienstinfrastruktur.** Die Anzahl von Verzeichnisgesamtstrukturen, Domänen und Mandanten, die von Ihrer Organisation verwendet werden.
- **Abhängigkeit von älteren oder lokalen Authentifizierungsmechanismen.** Die Anzahl von Workloads, die von Legacy- oder Drittanbieter-MFA-Mechanismen (Multi-Factor Authentication, mehrstufige Authentifizierung) abhängig sind.
- **Umfang der in der Cloud bereitgestellten Verzeichnisdienste.** Die Anzahl von Verzeichnisgesamtstrukturen, Domänen und Mandanten, die Sie in der Cloud bereitstellen.
- **In der Cloud bereitgestellte Active Directory-Server.** Die Anzahl von Active Directory-Servern, die in der Cloud bereitgestellt werden.
- **In der Cloud bereitgestellte Organisationseinheiten.** Die Anzahl der in der Cloud bereitgestellten Active Directory-Organisationseinheiten (OUs).
- **Verbundumfang.** Die Anzahl der Identitätsbaselinesysteme, die sich mit den Systemen Ihrer Organisation im Verbund befinden.
- **Benutzer mit erhöhten Rechten.** Die Anzahl von Benutzerkonten mit erhöhten Zugriffsrechten für Ressourcen oder Verwaltungstools.
- **Verwenden der rollenbasierten Zugriffssteuerung.** Die Anzahl von Abonnements, Ressourcengruppen oder einzelnen Ressourcen, die nicht durch die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) über Gruppen verwaltet werden.
- **Authentifizierungsansprüche.** Die Anzahl erfolgreicher und fehlerhafter Versuche zur Benutzerauthentifizierung.
- **Autorisierungsansprüche.** Die Anzahl erfolgreicher und fehlerhafter Versuche von Benutzern, auf Ressourcen zuzugreifen.
- **Kompromittierte Konten.** Die Anzahl von Benutzerkonten, die kompromittiert wurden.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

Risiken im Hinblick auf die Identitätsbaseline beruhen zum größten Teil auf der Komplexität der Identitätsinfrastruktur in Ihrer Organisation. Wenn alle Ihre Benutzer und Gruppen über ein einziges Verzeichnis oder einen einzigen nativen Cloudidentitätsanbieter mit minimaler Integration in andere Dienste verwaltet werden, ist Ihre Risikostufe wahrscheinlich relativ gering. Wenn Ihr Unternehmen jedoch wächst, müssen Ihre Identitätsbaselinesysteme möglicherweise kompliziertere Szenarien wie z.B. mehrere Verzeichnisse unterstützen, um Ihre interne Organisation oder den Verbund mit externen Identitätsanbietern abzubilden. Mit komplexeren Systemen steigt auch das Risiko.

In den frühen Phasen der Cloudeinführung arbeiten Sie mit Ihrem IT-Sicherheitsteam und den Projektbeteiligten des Unternehmens zusammen, um [Geschäftsrisiken](./business-risks.md) im Zusammenhang mit der Identität zu identifizieren, und bestimmen anschließend eine akzeptable Baseline für die Identitätsrisikotoleranz. Dieser Abschnitt des Cloud Adoption Framework enthält einige Beispiele. Die Risiken und Baselines in Ihrem Unternehmen bzw. bei Ihren Bereitstellungen weichen im Detail möglicherweise davon ab.

Legen Sie nach der Einigung auf eine Baseline minimale Benchmarks fest, die eine unzulässige Zunahme der identifizierten Risiken darstellen. Diese Benchmarks fungieren als Auslöser und geben an, wann Sie Maßnahmen zum Behandeln dieser Risiken ergreifen müssen. Im Folgenden wird anhand einiger Beispiele dargestellt, wie identitätsbezogene Metriken (z.B. die oben erwähnten) eine höhere Investition in die Disziplin „Identitätsbaseline“ rechtfertigen können.

- **Trigger durch Anzahl von Benutzerkonten.** Ein Unternehmen mit mehr als _x_ Benutzern, Gruppen oder anderen Objekten, die in Ihren Identitätssystemen verwaltet werden, profitieren von der Investition in die Disziplin „Identitätsbaseline“, um eine effiziente Governance für eine große Anzahl von Konten sicherzustellen.
- **Trigger durch lokale Identitätsabhängigkeiten.** Ein Unternehmen, das die Migration von Workloads zur Cloud plant, die ältere Authentifizierungsfunktionen oder mehrstufige Authentifizierung von Drittanbietern benötigen, sollten in die Disziplin „Identitätsbaseline“ investieren, um Risiken im Zusammenhang mit Refactoring oder der zusätzlichen Cloudinfrastrukturbereitstellung zu mindern.
- **Trigger durch komplexe Verzeichnisdienste.** Ein Unternehmen, das mehr als _x_ einzelne Gesamtstrukturen, Domänen oder Verzeichnismandanten verwaltet, sollte in die Disziplin „Identitätsbaseline“ investieren, um Risiken im Zusammenhang mit der Kontoverwaltung sowie Effizienzprobleme in Bezug auf die Verteilung von Anmeldeinformationen auf mehrere Systeme zu reduzieren.
- **Trigger durch in der Cloud gehostete Verzeichnisdienste.** Ein Unternehmen, das _x_ virtuelle Active Directory-Servercomputer (VMs) in der Cloud hostet oder _x_ Organisationseinheiten (OUs) auf diesen cloudbasierten Servern verwaltet, kann durch die Investition in die Disziplin „Identitätsbaseline“ profitieren, um die Integration in lokale oder andere externe Identitätsdienste zu optimieren.
- **Trigger durch Verbund.** Ein Unternehmen, das einen Identitätsverbund mit _x_ externen Identitätsbaselinesystemen implementiert, kann von einer Investition in die Disziplin „Identitätsbaseline“ profitieren, um eine konsistente, organisationsweite Richtlinie für alle Verbundmitglieder sicherzustellen.
- **Trigger durch erhöhte Zugriffsrechte.** Ein Unternehmen, in dem mehr als _x %_ der Benutzer erweiterte Zugriffsrechte für Verwaltungstools und Ressourcen besitzen, sollte eine Investition in die Disziplin „Identitätsbaseline“ in Betracht ziehen, um das Risiko einer unbeabsichtigten übermäßigen Zugriffsbereitstellung für Benutzer zu mindern.
- **Trigger durch RBAC.** Ein Unternehmen, in dem weniger als _x %_ der Ressourcen die Methoden der rollenbasierten Zugriffssteuerung verwenden, sollte eine Investition in die Disziplin „Identitätsbaseline“ in Betracht ziehen, um optimierte Möglichkeiten für die Zuweisung des Benutzerzugriffs für Ressourcen zu identifizieren.
- **Trigger durch Authentifizierungsfehler.** Ein Unternehmen, in dem bei mehr als _x %_ der Versuche Authentifizierungsfehler auftreten, sollten in die Disziplin „Identitätsbaseline“ investieren, um sicherzustellen, dass die Authentifizierungsmethoden keinen externen Angriffen ausgesetzt sind und dass Benutzer die Methoden der Benutzerauthentifizierung ordnungsgemäß verwenden können.
- **Trigger durch Autorisierungsfehler.** Ein Unternehmen, in dem Zugriffsversuche in mehr als _x %_ der Zeit abgelehnt werden, sollten in die Disziplin „Identitätsbaseline“ investieren, um die Anwendung und Aktualisierung der Zugangssteuerung zu verbessern und potenziell böswillige Zugriffsversuche zu identifizieren.
- **Trigger durch kompromittierte Konten.** Ein Unternehmen mit mehreren kompromittierten Konten sollte in die Disziplin „Identitätsbaseline“ investieren, um sowohl die Sicherheit von Authentifizierungsmechanismen zu erhöhen als auch die Mechanismen zur Minimierung von Risiken im Zusammenhang mit kompromittierten Konten zu verbessern.

Die genauen Metriken und Auslöser, die Sie zum Bemessen der Risikotoleranz verwenden, und die Höhe der Investitionen in die Disziplin „Identitätsbaseline“ sind für Ihre Organisation spezifisch. Die oben genannten Beispiele sollten jedoch eine hilfreiche Diskussionsgrundlage für Ihr Cloudgovernanceteam darstellen.

## <a name="next-steps"></a>Nächste Schritte

Dokumentieren Sie mit der Vorlage [Cloudverwaltung](./template.md) die Metriken und Toleranzindikatoren, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Identitätsbaseline-Beispielrichtlinien als Ausgangspunkt für die Entwicklung von Richtlinien, die bestimmte Geschäftsrisiken behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
