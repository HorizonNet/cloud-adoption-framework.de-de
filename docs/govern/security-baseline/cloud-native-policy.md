---
title: Richtlinie zur cloudnativen Sicherheitsbaseline
description: Sehen Sie sich eine cloudnative Beispielrichtlinie für die Disziplin „Sicherheitsbaseline“ mit ausreichenden Azure-Tools und -Plattformen für die Bewältigung von Geschäftsrisiken an.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5b8459378a4e435bc88b5f7623d08f3f61f52f5c
ms.sourcegitcommit: 949b87bad28d32df84df190160089f01826f3a31
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88195295"
---
# <a name="cloud-native-security-baseline-policy"></a>Richtlinie zur cloudnativen Sicherheitsbaseline

Die [Disziplin „Sicherheitsbaseline“](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Bei dieser Disziplin geht es um allgemeine Sicherheitsthemen, z. B. den Schutz des Netzwerks, von digitalen Ressourcen und von Daten. Wie im [Leitfaden zur Richtlinienüberprüfung](../policy-compliance/cloud-policy-review.md) erläutert, umfasst das Cloud Adoption Framework drei Ebenen von Beispielrichtlinien: cloudnative, Unternehmens- und cloudentwurfsprinzipien-konforme Richtlinien für jede der einzelnen Disziplinen. In diesem Artikel wird die cloudnative Beispielrichtlinie für die Disziplin der Sicherheitsbaseline beschrieben.

> [!NOTE]
> Microsoft ist nicht in der Lage, Unternehmens- oder IT-Richtlinien vorzuschreiben. Dieser Artikel unterstützt Sie bei den Vorbereitungen für eine interne Richtlinienüberprüfung. Es wird davon ausgegangen, dass diese Beispielrichtlinie vor ihrer Verwendung erweitert, überprüft und in Bezug auf Ihre Unternehmensrichtlinie getestet wird. Die Beispielrichtlinie sollte nicht ohne Anpassungen verwendet werden.

## <a name="policy-alignment"></a>Ausrichtung der Richtlinie

Diese Beispielrichtlinie stellt ein cloudnatives Szenario dar, d.h., dass die in Azure bereitgestellten Tools und Plattformen zur Verwaltung von Geschäftsrisiken in Bezug auf eine Bereitstellung ausreichen. In diesem Szenario wird davon ausgegangen, dass eine einfache Konfiguration der Azure-Standarddienste ausreichenden Schutz für die Ressourcen bietet.

## <a name="cloud-security-and-compliance"></a>Sicherheit und Compliance in der Cloud

Sicherheit ist ein wesentlicher Bestandteil aller Azure-Lösungen, die einzigartige Sicherheitsvorteile bieten, die auf globalen Sicherheitsfunktionen, ausgereiften kundenorientierten Kontrollmöglichkeiten und einer sicheren, verstärkten Infrastruktur basieren. Diese leistungsstarke Kombination unterstützt Sie beim Schutz Ihrer Anwendungen und Daten sowie beim Durchsetzen Ihrer Compliance-Maßnahmen und bietet kostengünstige Sicherheit für Organisationen jeder Größe. Dieser Ansatz schafft eine starke Ausgangsposition für jede Sicherheitsrichtlinie, ersetzt jedoch nicht die Notwendigkeit ebenso starker Sicherheitsmaßnahmen in Bezug auf die verwendeten Sicherheitsdienste.

### <a name="built-in-security-controls"></a>Integrierte Sicherheitskontrollen

Eine starke Sicherheitsinfrastruktur lässt sich nur schwer aufrechterhalten, wenn Sicherheitskontrollen nicht intuitiv sind und separat konfiguriert werden müssen. Azure umfasst integrierte Sicherheitskontrollen in einer Vielzahl von Diensten, über die Sie Daten und Workloads schnell schützen und Risiken in Hybridumgebungen steuern können. Mit integrierten Partnerlösungen können Sie darüber hinaus vorhandene Schutzmaßnahmen ganz einfach in die Cloud übertragen.

### <a name="cloud-native-identity-policies"></a>Cloudnative Identitätsrichtlinien

Die Identität entwickelt sich immer mehr zur neuen Grenzsteuerungsebene für die Sicherheit und übernimmt so die Rolle des herkömmlichen netzwerkzentrierten Ansatzes. Umkreisnetzwerke werden immer durchlässiger, und der Schutz durch den Umkreis kann nicht so effektiv sein wie vor dem Aufkommen von BYOD-Geräten (Bring Your Own Device) und Cloudanwendungen. Die Identitätsverwaltung und Zugriffssteuerung in Azure ermöglichen nahtlosen und sicheren Zugriff auf alle Ihre Anwendungen.

Eine cloudnative Beispielrichtlinie für die Identität in allen lokalen und Cloudverzeichnissen kann beispielsweise folgende Anforderungen enthalten:

- Autorisierter Zugriff auf Ressourcen mit rollenbasierter Zugriffssteuerung (RBAC), mehrstufiger Authentifizierung und einmaligem Anmelden (SSO).
- Schnelle Risikominderung von Benutzeridentitäten mit Verdacht auf Kompromittierung.
- Just-in-Time-Zugriff (JIT): gerade genügend Zugriff, der pro Aufgabe gewährt wird, um die Offenlegung von Administratoranmeldeinformationen mit zu vielen Berechtigungen einzuschränken.
- Erweiterte Benutzeridentität und Zugriff auf Richtlinien in mehreren Umgebungen über Azure Active Directory.

Obwohl es wichtig ist, die [Disziplin „Identitätsbaseline“](../identity-baseline/index.md) im Kontext der Disziplin „Sicherheitsbaseline“ zu verstehen, wird die Identitätsbaseline in den [fünf Disziplinen der Cloudgovernance](../index.md) als eigenständige Disziplin behandelt.

### <a name="network-access-policies"></a>Netzwerkzugriffsrichtlinien

Die Netzwerksteuerung beinhaltet die Konfiguration, Verwaltung und Sicherung von Netzwerkelementen wie virtuellen Netzwerken, Lastenausgleich, DNS und Gateways. Die Netzwerkelemente bieten eine Möglichkeit der Kommunikation und Interoperabilität zwischen Diensten. Azure verfügt über eine robuste und sichere Netzwerkinfrastruktur zur Unterstützung der Konnektivitätsanforderungen Ihrer Anwendungen und Dienste. Netzwerkkonnektivität ist zwischen Ressourcen in Azure, zwischen lokalen und in Azure gehosteten Ressourcen und zu und aus dem Internet und Azure möglich.

Eine cloudnative Richtlinie für Netzwerkelemente kann beispielsweise folgende Anforderungen umfassen:

- Hybridverbindungen mit lokalen Ressourcen sind in einer cloudnativen Richtlinie möglicherweise nicht zulässig. Wenn sich eine Hybridverbindung als notwendig erweisen sollte, stellt eine robustere Sicherheitsrichtlinie auf Enterprise-Ebene eine bessere Variante dar.
- Benutzer können sichere Verbindungen mit Azure und innerhalb davon über virtuelle Netzwerke und Netzwerksicherheitsgruppen herstellen.
- Die native Microsoft Azure Firewall schützt Hosts durch Beschränken des Portzugriffs vor schädlichem Netzwerkdatenverkehr. Ein gutes Beispiel für diese Richtlinie ist eine Anforderung, direkten Datenverkehr für einen virtuellen Computer über SSH/RDP zu blockieren oder nicht zu aktivieren.
- Dienste wie Azure Web Application Firewall (WAF) unter Azure Application Gateway und Azure DDoS Protection schützen Anwendungen und stellen die Verfügbarkeit von in Azure ausgeführten virtuellen Computern sicher. Diese Features sollten nicht deaktiviert werden.

### <a name="data-protection"></a>Schutz von Daten

Einer der Schlüssel zum Schutz von Daten in der Cloud ist die Berücksichtigung der möglichen Zustände, in denen Ihre Daten auftreten können. Außerdem sollten Sie die Steuerungsmöglichkeiten beachten, die für jeden Zustand verfügbar sind. Im Rahmen der bewährten Methoden für Datensicherheit und Verschlüsselung in Azure befassen sich die Empfehlungen mit den folgenden Datenzuständen:

- Steuerelemente zur Datenverschlüsselung werden in Diensten von virtuellen Computern, über Speicher bis hin zu SQL-Datenbank erstellt.
- Während Daten zwischen Clouds und Kunden übertragen werden, können sie durch branchenübliche Verschlüsselungsprotokolle geschützt werden.
- Mit Azure Key Vault können Benutzer kryptografische Schlüssel, Kennwörter, Verbindungszeichenfolgen und Zertifikate schützen und verwalten, die von Cloudanwendungen und -diensten verwendet werden.
- Mit Azure Information Protection können vertrauliche Daten in Anwendungen klassifiziert, gekennzeichnet und geschützt werden.

Diese Funktionen sind in Azure integriert, sie erfordern jedoch jeweils Konfigurationsanpassungen, sodass die Kosten höher ausfallen können. Die Orientierung der einzelnen cloudnativen Funktionen an einer [Strategie zur Datenklassifizierung](../policy-compliance/data-classification.md) wird dringend empfohlen.

### <a name="security-monitoring"></a>Sicherheitsüberwachung

Die Sicherheitsüberwachung ist eine proaktive Strategie, bei der Ihre Ressourcen überwacht werden, um Systeme zu erkennen, die nicht den Unternehmensstandards oder bewährten Methoden entsprechen. Azure Security Center bietet eine einheitliche Sicherheitsbaseline und erweiterten Schutz vor Bedrohungen für Hybrid Cloud-Workloads. Mit Security Center können Sie Sicherheitsrichtlinien für Ihre Workloads anwenden, die Angriffsfläche für Bedrohungen verringern sowie Angriffe erkennen und darauf reagieren, beispielsweise:

- Einheitliche Übersicht über die Sicherheit all Ihrer lokalen und cloudbasierten Workloads mit Azure Security Center.
- Kontinuierliche Überwachung und Sicherheitsbewertungen zum Sicherstellen der Konformität und zur Behebung aller Sicherheitsrisiken.
- Interaktive Tools und kontextbezogene Informationen zu Bedrohungen für optimierte Untersuchungen.
- Umfassende Protokollierung und Integration in vorhandenen Sicherheitsinformationen.
- Verringert den Bedarf an teuren, nicht integrierten, einmalig verwendeten Sicherheitslösungen.

### <a name="extend-cloud-native-policies"></a>Erweitern cloudnativer Richtlinien

Durch die Verwendung der Cloud lassen sich einige Sicherheitsbürden verringern. Microsoft bietet physische Sicherheit für Azure-Rechenzentren und trägt zum Schutz der Cloudplattform vor Bedrohungen der Infrastruktur wie z.B. einem DDoS-Angriff bei. Da Microsoft über Tausende von Cybersicherheitsspezialisten verfügt, die sich täglich mit Sicherheitsbelangen beschäftigen, sind die Ressourcen zur Erkennung, Verhinderung oder Minderung von Cyberangriffen beträchtlich. Während sich Unternehmen früher Gedanken darüber machten, ob die Cloud sicher ist, verstehen die meisten jetzt, dass das Ausmaß der Investitionen in Mitarbeiter und spezialisierte Infrastrukturen von Anbietern wie Microsoft die Cloud sicherer macht als die meisten lokalen Rechenzentren.
Durch die Verwendung der Cloud lassen sich einige Sicherheitsbürden verringern. Microsoft bietet physische Sicherheit für Azure-Rechenzentren und trägt zum Schutz der Cloudplattform vor Bedrohungen der Infrastruktur wie z.B. einem DDoS-Angriff bei. Da Microsoft über Tausende von Cybersicherheitsspezialisten verfügt, die sich täglich mit Sicherheitsbelangen beschäftigen, sind die Ressourcen zur Erkennung, Verhinderung oder Minderung von Cyberangriffen beträchtlich. Während sich Unternehmen früher Gedanken darüber machten, ob die Cloud sicher ist, verstehen die meisten jetzt, dass das Ausmaß der Investitionen in Mitarbeiter und spezialisierte Infrastrukturen von Anbietern wie Microsoft die Cloud sicherer macht als die meisten lokalen Rechenzentren.

Selbst bei dieser Investition in die cloudnative Sicherheitsbaseline empfiehlt es sich, die cloudnativen Standardrichtlinien um eine Richtlinie der Sicherheitsbaseline zu erweitern. Es folgen Beispiele für erweiterte Richtlinien, die auch in einer cloudnativen Umgebung berücksichtigt werden sollten:

- **Schützen von virtuellen Computern:** Sicherheit sollte für jede Organisation oberste Priorität haben, und dazu bedarf es mehrerer Vorgänge. Sie müssen den Sicherheitsstatus bewerten, das System vor Sicherheitsbedrohungen schützen und dann bestehende Bedrohungen erkennen und schnell darauf reagieren.
- **Schützen der Inhalte von virtuellen Computern:** Die Einrichtung regelmäßiger automatisierter Sicherungen ist zum Schutz vor Benutzerfehlern unerlässlich. Dies genügt jedoch nicht: Sie müssen außerdem sicherstellen, dass die Sicherungen vor Cyberangriffen geschützt und jederzeit verfügbar sind.
- **Überwachen von Anwendungen:** Dieses Muster umfasst mehrere Aufgaben, z.B. Einblick in den Integritätsstatus der virtuellen Computer, Verständnis der Interaktionen zwischen den virtuellen Computern und Festlegung von Möglichkeiten zur Überwachung der Anwendungen, die auf den virtuellen Computern ausgeführt werden. Alle diese Aufgaben sind unerlässlich, damit die Anwendungen rund um die Uhr ausgeführt werden.
- **Schützen und Überwachen des Datenzugriffs.** Organisationen sollten den gesamten Datenzugriff überwachen und erweiterte Machine Learning-Funktionen nutzen, um Abweichungen von regulären Zugriffsmustern zu erkennen.
- **Durchführen von Failoverübungen:** Für Cloudvorgänge mit geringer Fehlertoleranz muss nach einem Vorfall im Zusammenhang mit der Cybersicherheit oder der Plattform ein Failover oder eine Wiederherstellung ausgeführt werden können. Diese Prozeduren sollten nicht einfach nur dokumentiert, sondern vierteljährlich geübt werden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie sich mit der Beispielrichtlinie für die Sicherheitsbaseline für cloudnative Lösungen vertraut gemacht haben, können Sie nun zum Leitfaden zur Überprüfung von Richtlinien zurückkehren und anhand dieser Beispielrichtlinie eigene Richtlinien für die Cloudeinführung erstellen.

> [!div class="nextstepaction"]
> [Erstellen Ihrer eigenen Richtlinien unter Verwendung des Leitfadens zur Überprüfung von Richtlinien](../policy-compliance/cloud-policy-review.md)
