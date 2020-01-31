---
title: Festlegen von Prozessen zur Einhaltung von Richtlinien
description: Erfahren Sie, wie Sie Prozesse festlegen, um die Einhaltung von Unternehmensrichtlinien sicherzustellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: bf69c13d80063e44a49d945908e2cc319b90ce3e
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807171"
---
<!-- markdownlint-disable MD026 -->

# <a name="establish-policy-adherence-processes"></a>Festlegen von Prozessen zur Einhaltung von Richtlinien

Nachdem Sie Ihre Cloudrichtlinienanweisungen eingerichtet und ein erstes Entwurfshandbuch geschrieben haben, müssen Sie eine Strategie entwickeln, die sicherstellt, dass die Cloudbereitstellung konform zu Ihren Richtlinienanforderungen bleibt. Diese Strategie muss die fortlaufenden Überprüfungs- und Kommunikationsprozesse Ihres Cloudgovernanceteams einschließen, Kriterien für Handlungen bei Richtlinienverstößen festlegen und die Anforderungen für automatisierte Überwachungs- und Compliancesysteme definieren, die Verstöße erkennen und Aktionen zur Problembehebung auslösen.

Beispiele für die Abstimmung eines Prozesses zur Einhaltung von Richtlinien auf die Cloudgovernanceplanung finden Sie in den Abschnitten zu Unternehmensrichtlinien unter [Nützliche Governance-Vorgehensweisen](../guides/index.md).

## <a name="prioritize-policy-adherence-processes"></a>Priorisieren von Prozessen zur Einhaltung von Richtlinien

Wie viel Aufwand ist bei der Entwicklung von Prozessen erforderlich, um Ihre Richtlinienziele zu unterstützen? Abhängig von der Größe und Reife Ihrer Cloudbereitstellung können der erforderliche Aufwand zum Einrichten von Prozessen für die Einhaltung und die damit verbundenen Kosten stark variieren.

Für kleine Bereitstellungen, die das Entwickeln und Testen von Ressourcen umfassen, sind die Richtlinienanforderungen möglicherweise einfach und erfordern nur die Behandlung weniger dedizierter Ressourcen. Eine ausgereifte, unternehmenskritische Cloudbereitstellung mit hohen Anforderungen an Sicherheit und Leistung erfordert andererseits eventuell ein Team von Mitarbeitern, umfassende interne Prozesse und benutzerdefinierte Überwachungstools, um Ihre Richtlinienziele zu unterstützen.

Als ersten Schritt bei der Definition Ihrer Strategie zur Einhaltung von Richtlinien sollten Sie auswerten, wie die nachfolgend beschriebenen Prozesse Ihre Anforderungen unterstützen können. Ermitteln Sie, wie viel Aufwand sich als Investition in diese Prozesse lohnt, und stellen Sie dann anhand dieser Informationen realistische Budget- und Personalpläne auf, um diese Anforderungen zu erfüllen.

## <a name="establish-cloud-governance-team-processes"></a>Einrichten von Prozessen für das Cloudgovernanceteam

Vor dem Definieren von Auslösern für die Erzwingung der Einhaltung von Richtlinien müssen Sie die allgemeinen Prozesse einrichten, die Ihr Team verwenden soll. Außerdem müssen Sie festlegen, wie Informationen freigegeben und zwischen IT-Mitarbeiter und dem Cloudgovernanceteam eskaliert werden sollen.

### <a name="assign-cloud-governance-team-members"></a>Zuweisen von Mitgliedern zum Cloudgovernanceteam

Ihr Cloudgovernanceteam übernimmt die laufende Unterstützung für die Einhaltung von Richtlinien und behandelt Probleme im Zusammenhang mit Richtlinien, die beim Bereitstellen und im Betrieb Ihrer Cloudressourcen auftreten. Wenn Sie dieses Team zusammenstellen, laden Sie Mitarbeiter ein, die über Fachkenntnisse in den Bereichen verfügen, die unter Ihre definierten Richtlinien und identifizierten Risiken fallen.

Für erste Testbereitstellungen kann dies auf wenige Systemadministratoren beschränkt sein, die für die Einrichtung der Governancegrundlagen verantwortlich sind. Mit zunehmender Reife Ihrer Governanceprozesse sollten Sie die Mitglieder des Cloudunterstützungsteams regelmäßig überprüfen, um sicherzustellen, dass neue potenzielle Risiken und Richtlinienanforderungen ordnungsgemäß behandelt werden können. Identifizieren Sie Mitarbeiter Ihrer IT- und Geschäftsabteilungen mit relevanter Erfahrung oder Interesse an bestimmten Governancebereichen, und binden Sie sie je nach Bedarf dauerhaft oder vorübergehend Ihre Teams ein.

### <a name="reviews-and-policy-iteration"></a>Iterationen von Überprüfungen und Richtlinien

Wenn zusätzliche Ressourcen und Workloads bereitgestellt werden, muss das Cloudgovernanceteam sicherstellen, dass die neuen Workloads oder Ressourcen die Richtlinienanforderungen erfüllen. Werten Sie neue Anforderungen von Workloadentwicklungsteams aus, um sicherzustellen, dass ihre geplanten Implementierungen mit Ihren Entwurfsrichtlinien übereinstimmen, und aktualisieren Sie Ihre Richtlinien, um diese Anforderungen gegebenenfalls zu unterstützen.

Planen Sie, neue potenzielle Risiken auszuwerten, und aktualisieren Sie die Richtlinienanweisungen und Entwurfsleitfäden nach Bedarf. Arbeiten Sie mit IT-Mitarbeitern und Workloadteams zusammen, um neue Azure-Features und -Dienste kontinuierlich auszuwerten. Planen Sie außerdem regelmäßige Überprüfungszyklen in allen fünf Governancedisziplinen, um sicherzustellen, dass die Richtlinie aktuell ist und eingehalten wird.

### <a name="education"></a>Fortbildung

Zur Einhaltung der Richtlinien müssen die IT-Mitarbeiter und Entwickler die Richtlinienanforderungen, die ihre Zuständigkeitsbereiche betreffen, verstehen. Planen Sie Ressourcen für die Dokumentation von Entscheidungen und Anforderungen ein, und informieren Sie alle relevanten Teams über Entwurfshandbücher, die Ihre Richtlinienanforderungen unterstützen.

Wenn sich Richtlinien ändern, aktualisieren Sie regelmäßig die Dokumentation und Schulungsmaterialien, und stellen Sie sicher, dass in den Schulungen der relevanten IT-Mitarbeiter aktualisierte Anforderungen und Anleitungen angesprochen werden.

Auf Ihrem Weg in die Cloud empfiehlt es sich, von Zeit zu Zeit den Rat von Partnern einzuholen und professionelle Schulungsprogramme zu nutzen, um Ihr Team sowohl technisch als auch in Bezug auf Prozesse weiterzubilden. Darüber hinaus werden formale Zertifizierungen häufig als wertvolle Ergänzung Ihres Schulungsportfolios betrachtet und sollten daher in Betracht gezogen werden.

### <a name="establish-escalation-paths"></a>Einrichten von Eskalationspfaden

Wer soll benachrichtigt werden, wenn eine Ressource nicht mehr konform ist? An wen sollen sich IT-Mitarbeiter wenden, wenn sie ein Konformitätsproblem entdecken? Stellen Sie sicher, dass der Eskalationsprozess für das Cloudgovernanceteam klar definiert ist. Stellen Sie sicher, dass diese Kommunikationskanäle immer aktuell bleiben und Änderungen bei den Mitarbeitern und in der Organisation berücksichtigen.

## <a name="violation-triggers-and-actions"></a>Auslöser und Aktionen bei Verstößen

Nachdem Sie Ihr Cloudgovernanceteam und dessen Prozesse definiert haben, müssen Sie explizit definieren, was als Einhaltungsverstoß angesehen wird und die Aktionen auslöst, und was diese Aktionen umfassen sollen.

### <a name="define-triggers"></a>Definieren von Auslösern

Überprüfen Sie für jede Ihrer Richtlinienanweisungen die Anforderungen, um festzustellen, was eine Richtlinienverletzung ausmacht. Generieren Sie Auslöser anhand der Informationen, die Sie bereits im Rahmen der Richtliniendefinition eingerichtet haben.

- **Risikotoleranz:** Erstellen Sie Auslöser bei Verstößen basierend auf Metriken und Risikoindikatoren, die Sie im Rahmen Ihrer [Risikotoleranzanalyse](./risk-tolerance.md) eingerichtet haben.
- **Definierte Richtlinienanforderungen:** Richtlinienanweisungen können Anforderungen an SLA (Service Level Agreement), Business Continuity und Disaster Recovery (BRCD) und Leistung enthalten, die als Grundlage für Konformitätsauslöser verwendet werden sollten.

### <a name="define-actions"></a>Definieren von Aktionen

Jeder Verletzungsauslöser sollte eine entsprechende Aktion aufweisen. Ausgelöste Aktionen sollten immer einen entsprechenden IT-Mitarbeiter oder ein Mitglied des Cloudgovernanceteams benachrichtigen, wenn ein Verstoß auftritt. Diese Benachrichtigung kann in Abhängigkeit vom Typ und Schweregrad der erkannten Verletzung zu einer manuellen Überprüfung des Konformitätsproblems führen oder einen vordefinierten Problembehebungsprozess auslösen.

Einige Beispiele für Auslöser und Aktionen bei Verstößen:

| Cloudgovernancedisziplin | Beispielauslöser | Beispielaktion |
|-----------------------------|----------------|---------------|
| Cost Management | Monatliche Cloudausgaben sind um mehr als 20 % höher als erwartet. | Benachrichtigung des Leiters der Abrechnungsabteilung, der eine Überprüfung der Ressourcennutzung beginnt. |
| Sicherheitsbaseline | Erkennung verdächtiger Benutzeraktivitäten. | Benachrichtigung des IT-Sicherheitsteams und Deaktivierung des verdächtigen Benutzerkontos. |
| Ressourcenkonsistenz | Die CPU-Auslastung für eine Workload übersteigt 90 %. | Benachrichtigung des IT-Betriebsteam und horizontales Hochskalieren mit zusätzlichen Ressourcen zum Verarbeiten der Last. |

## <a name="automation-of-monitoring-and-compliance"></a>Automatisierung der Überwachung und Einhaltung

Nachdem Sie Ihre Auslöser und Aktionen für Verstöße definiert haben, können Sie damit beginnen, optimale Protokollierungs- und Berichterstattungstools und andere Features der Cloudplattform zu planen, die bei der Automatisierung Ihrer Strategie für Überwachung und Einhaltung von Richtlinien helfen.

Hilfe bei der Auswahl des besten Überwachungsmusters für Ihre Bereitstellung finden Sie im [Leitfaden zur Entscheidungsfindung für Protokollierung und Berichterstellung](../../decision-guides/logging-and-reporting/index.md).

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Einhaltung gesetzlicher Bestimmungen in der Cloud.

> [!div class="nextstepaction"]
> [Einhaltung gesetzlicher Bestimmungen](./regulatory-compliance.md)
