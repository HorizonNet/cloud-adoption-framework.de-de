---
title: Beschleunigung der Bereitstellung – Beispiele für Richtlinienanweisungen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Beschleunigung der Bereitstellung – Beispiele für Richtlinienanweisungen
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a307c29a640332fdf82a69ec06eab27589f77304
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566351"
---
# <a name="deployment-acceleration-sample-policy-statements"></a>Beschleunigung der Bereitstellung – Beispiele für Richtlinienanweisungen

Einzelne Cloudrichtlinienanweisungen sind Anleitungen für den Umgang mit bestimmten Risiken, die bei Ihrem Risikobewertungsprozess identifiziert wurden. Diese Anweisungen sollten eine präzise Zusammenfassung der Risiken sowie der Pläne für den Umgang mit diesen bereitstellen. Jede Anweisungsdefinition sollte diese Informationen enthalten:

- **Technisches Risiko:** Eine Zusammenfassung des Risikos, das diese Richtlinie behandelt.
- **Richtlinienanweisung:** Eine klare, zusammenfassende Erläuterung der Richtlinienanforderungen.
- **Entwurfsoptionen:** Direkt umsetzbare Empfehlungen, Spezifikationen oder andere Anleitungen, die IT-Teams und Entwickler bei der Implementierung der Richtlinie verwenden können.

Die folgende Beispielrichtlinienanweisungen beziehen sich auf allgemeine konfigurationsbezogene Geschäftsrisiken. Diese Anweisungen sind Beispiele, auf die Sie sich beim Entwurf von Richtlinienanweisungen beziehen können, um die Anforderungen Ihres Unternehmens zu erfüllen. Diese Beispiele sind nicht restriktiv gemeint, und es gibt immer potenziell mehrere Richtlinienoptionen für den Umgang mit jedem identifizierten Risiko. Arbeiten Sie eng mit den Geschäfts- und IT-Teams zusammen, um die besten Richtlinien für Ihre spezielle Risikogruppe zu identifizieren.

## <a name="reliance-on-manual-deployment-or-configuration-of-systems"></a>Verwenden der manuellen Bereitstellung oder Konfiguration von Systemen

**Technisches Risiko:** Wenn Sie sich bei der Bereitstellung oder Konfiguration auf manuelle Eingriffe verlassen, steigt nicht nur die Fehlerwahrscheinlichkeit. Es leiden auch Wiederholbarkeit und Vorhersagbarkeit von Systembereitstellung und -konfiguration. In der Regel werden Systemressourcen auf diesem Weg auch langsamer bereitgestellt.

**Richtlinienanweisung:** Alle Ressourcen, die in der Cloud bereitgestellt werden, sollten nach Möglichkeit mithilfe von Vorlagen oder Automatisierungsskripts bereitgestellt werden.

**Potenzielle Entwurfsoptionen:** [Azure Resource Manager-Vorlagen](https://docs.microsoft.com/azure/azure-resource-manager/template-deployment-overview) stellen für die Bereitstellung von Ressourcen in Azure das Konzept „Infrastructure-as-Code“ bereit. Sie können aber auch [Terraform](https://docs.microsoft.com/azure/terraform/terraform-overview) als konsistentes lokales und cloudbasiertes Bereitstellungstool verwenden.

## <a name="lack-of-visibility-into-system-issues"></a>Mangelnde Transparenz von Systemproblemen

**Technisches Risiko:** Aufgrund unzureichender Überwachungs- und Diagnosemöglichkeiten für Geschäftssysteme können die Mitarbeiter im Betrieb Probleme vor einem Systemausfall nicht identifizieren und beseitigen. Der Zeitaufwand für das ordnungsgemäße Beheben eines Ausfalls steigt damit erheblich.

**Richtlinienanweisung:** Die folgenden Richtlinien werden implementiert:

- Wichtige Metriken und Diagnosemaßnahmen werden für alle Produktionssysteme und Komponenten identifiziert. Überwachungs- und Diagnosetools werden auf diese Systeme angewendet und regelmäßig von Mitarbeitern im Betrieb überwacht.
- Der Betrieb kann auch den Einsatz von Überwachungs- und Diagnosetools in produktionsfernen Umgebungen wie Staging und Qualitätskontrolle erwägen, um Systemprobleme bereits zu identifizieren, bevor sie in der Produktionsumgebung auftreten.

**Potenzielle Entwurfsoptionen:** [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor) mit Log Analytics und Application Insights stellt Tools zum Sammeln und Analysieren von Telemetriedaten bereit, damit Sie die Leistung Ihrer Anwendungen besser verstehen und proaktiv Probleme identifizieren können, die sich auf die Anwendungen und die zugehörigen Ressourcen auswirken. Darüber hinaus werden im [Azure-Aktivitätsprotokoll](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) alle auf Plattformebene vorgenommenen Änderungen erfasst, weshalb das Protokoll auf nicht konforme Änderungen überwacht/überprüft werden muss.

## <a name="configuration-security-reviews"></a>Sicherheitsüberprüfungen der Konfiguration

**Technisches Risiko:** Im Laufe der Zeit kann sich durch neue Sicherheitsbedrohungen oder -risiken das Risiko eines unberechtigten Zugriffs auf sichere Ressourcen erhöhen.

**Richtlinienanweisung:** Cloud Governance-Prozesse müssen eine monatliche Überprüfung durch Konfigurationsverwaltungsteams umfassen, um böswillige Akteure oder Nutzungsmuster zu identifizieren, die durch die Konfiguration der Cloudressourcen verhindert werden sollten.

**Potenzielle Entwurfsoptionen:** Etablieren Sie monatliche Besprechungen zur Sicherheitsüberprüfung, an denen sowohl Mitglieder des Governanceteams als auch IT-Mitarbeiter teilnehmen, die für die Konfiguration von Anwendungen und Ressourcen in der Cloud verantwortlich sind. Überprüfen Sie vorhandene Sicherheitsdaten und -metriken, um Lücken in der aktuellen Richtlinie für die Beschleunigung der Bereitstellung und bei den entsprechenden Tools zu definieren. Aktualisieren Sie dann die Richtlinie, um neue Risiken zu beheben.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die in diesem Artikel erwähnten Beispiele als Ausgangspunkt für die Entwicklung von Richtlinien, die bestimmte Geschäftsrisiken behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

Laden Sie die Vorlage [Identitätsbaseline](../identity-baseline/template.md) herunter, um mit der Entwicklung eigener, benutzerdefinierter Richtlinienanweisungen im Zusammenhang mit der Identitätsverwaltung zu beginnen.

Um die Einführung dieser Disziplin zu beschleunigen, wählen Sie den [umsetzbaren Governanceleitfaden](../guides/index.md) aus, der am besten zu Ihrer Umgebung passt. Ändern Sie dann den Entwurf, um Ihre speziellen Entscheidungen für Unternehmensrichtlinien zu integrieren.

Erstellen Sie anhand der Risiken und Toleranzen einen Prozess, mit dem Sie die Einhaltung der Richtlinie für die Beschleunigung der Bereitstellung steuern und kommunizieren.

> [!div class="nextstepaction"]
> [Festlegen von Prozessen für Richtlinienkonformität](./compliance-processes.md)
