---
title: Beispiele für Richtlinienanweisungen der Ressourcenkonsistenz
description: Beispiele für Richtlinienanweisungen der Ressourcenkonsistenz
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5e997dee318d0d6799167de4f4c61a93c814c548
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807256"
---
# <a name="resource-consistency-sample-policy-statements"></a>Beispiele für Richtlinienanweisungen der Ressourcenkonsistenz

Einzelne Cloudrichtlinienanweisungen sind Anleitungen für den Umgang mit bestimmten Risiken, die während Ihres Risikobewertungsprozesses identifiziert wurden. Diese Anweisungen sollten eine präzise Zusammenfassung der Risiken sowie der Pläne für den Umgang mit diesen bereitstellen. Jede Anweisungsdefinition sollte diese Informationen enthalten:

- **Technisches Risiko:** Eine Zusammenfassung des Risikos, das diese Richtlinie behandelt.
- **Richtlinienanweisung:** Eine klare, zusammenfassende Erläuterung der Richtlinienanforderungen.
- **Entwurfsoptionen:** Direkt umsetzbare Empfehlungen, Spezifikationen oder andere Anleitungen, die IT-Teams und Entwickler bei der Implementierung der Richtlinie verwenden können.

Die folgende Beispielrichtlinienanweisungen beziehen sich auf allgemeine Geschäftsrisiken, die die Ressourcenkonsistenz betreffen. Diese Anweisungen sind Beispiele, auf die Sie sich beim Entwurf von Richtlinienanweisungen beziehen können, um die Anforderungen Ihres Unternehmens zu erfüllen. Diese Beispiele sind nicht restriktiv gemeint, und es gibt immer potenziell mehrere Richtlinienoptionen für den Umgang mit jedem identifizierten Risiko. Arbeiten Sie eng mit den Geschäfts- und IT-Teams zusammen, um die besten Richtlinien für Ihre spezielle Risikogruppe zu identifizieren.

## <a name="tagging"></a>Kennzeichnung (Tagging)

**Technisches Risiko:** Ohne die Zuordnung geeigneter Metadatentags zu den bereitgestellten Ressourcen kann der IT-Betrieb die Unterstützung oder Optimierung von Ressourcen auf Grundlage der erforderlichen Vereinbarung zum Servicelevel, der Wichtigkeit von Geschäftsvorgängen oder der Betriebskosten nicht priorisieren. Dies kann zur fehlerhaften Zuordnung von IT-Ressourcen und potenziellen Verzögerungen bei der Behebung von Vorfällen führen.

**Richtlinienanweisung:** Die folgenden Richtlinien werden implementiert:

- Bereitgestellte Ressourcen sollten mit den folgenden Werten gekennzeichnet werden:
  - Kosten
  - Wichtigkeit
  - SLA
  - Environment
- Mit Governancetools muss die Kennzeichnung (Tagging) im Hinblick auf Kosten, Kritikalität, SLA, Anwendung und Umgebung überprüft werden. Alle Werte müssen sich an vordefinierten Werten ausrichten, die vom Governance-Team verwaltet werden.

**Potenzielle Entwurfsoptionen:** In Azure werden für die meisten Ressourcentypen [Standardmetadatentags der Form „Name-Wert“](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) unterstützt. [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) wird verwendet, um bestimmte Tags im Rahmen der Erstellung von Ressourcen zu erzwingen.

## <a name="ungoverned-subscriptions"></a>Ungeregelte Abonnements

**Technisches Risiko:** Das beliebige Erstellen von Abonnements und Verwaltungsgruppen kann zu isolierten Abschnitten Ihrer Cloudumgebung führen, die nicht ordnungsgemäß Ihren Governance-Richtlinien unterliegen.

**Richtlinienanweisung:** Für die Erstellung neuer Abonnements oder Verwaltungsgruppen für unternehmenskritische Anwendungen oder geschützte Daten ist eine Überprüfung durch das Cloudgovernanceteam erforderlich. Genehmigte Änderungen werden in eine ordnungsgemäße Blaupausenzuweisung integriert.

**Potenzielle Entwurfsoptionen:** Schränken Sie den administrativen Zugriffs auf die [Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups) Ihrer Organisation auf nur genehmigte Governance-Teammitglieder ein, die das Erstellen von Abonnements und den Zugriffssteuerungsprozess kontrollieren.

## <a name="manage-updates-to-virtual-machines"></a>Verwalten von Aktualisierungen für virtuelle Computer

**Technisches Risiko:** Virtuelle Computer (VMs), die nicht auf dem neuesten Stand hinsichtlich neuester Updates und Softwarepatches sind, sind anfällig für Sicherheits- oder Leistungsprobleme, die zu Dienstunterbrechungen führen können.

**Richtlinienanweisung:** Governancetools müssen erzwingen, dass automatische Updates für alle bereitgestellten VMs aktiviert sind. Verstöße müssen von Betriebsmanagementteams überprüft und in Übereinstimmung mit den Betriebsrichtlinien beseitigt werden. Ressourcen, die nicht automatisch aktualisiert werden, müssen in Prozesse des IT-Betriebs einbezogen werden.

**Potenzielle Entwurfsoptionen:** Für in Azure gehostete VMs können konsistente Updateverwaltung bereitstellen, indem Sie die [Updateverwaltungslösung in Azure Automation](https://docs.microsoft.com/azure/automation/automation-update-management) verwenden.

## <a name="deployment-compliance"></a>Bereitstellungscompliance

**Technisches Risiko:** Bereitstellungsskripts und Automatisierungstools, die nicht umfassend vom Cloudgovernanceteam geprüft werden, können zu Ressourcenbereitstellungen führen, die den Richtlinien widersprechen.

**Richtlinienanweisung:** Die folgenden Richtlinien werden implementiert:

- Bereitstellungstools müssen vom Cloudgovernanceteam genehmigt werden, um eine kontinuierliche Governance für bereitgestellte Ressourcen sicherzustellen.
- Bereitstellungsskripts müssen in einem zentralen Repository aufbewahrt werden, das für das Cloudgovernanceteam zur regelmäßigen Überprüfung und Überwachung zugänglich ist.

**Potenzielle Entwurfsoptionen:** Die konsistente Verwendung von [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints) zum Verwalten automatisierter Bereitstellungen ermöglicht konsistente Bereitstellungen von Azure-Ressourcen, die die Governance-Standards und -Richtlinien Ihrer Organisation einhalten.

## <a name="monitoring"></a>Überwachung

**Technisches Risiko:** Nicht ordnungsgemäß implementierte oder inkonsistent instrumentierte Überwachung kann die Erkennung von Integritätsproblemen bei Workloads oder anderen Verstößen gegen die Richtliniencompliance verhindern.

**Richtlinienanweisung:** Die folgenden Richtlinien werden implementiert:

- Mit den Governancetools muss überprüft werden, ob alle Ressourcen in die Überwachung auf Ressourcenschwund, Sicherheit, Compliance und Optimierung einbezogen werden.
- Ferner muss mit den Governancetools überprüft werden, ob für alle Anwendungen und Daten Protokolldaten mit geeignetem Protokolliergrad erfasst werden.

**Potenzielle Entwurfsoptionen:** [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ist der Standardüberwachungsdienst in Azure, und konsistente Überwachung kann durch die Verwendung von [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints) beim Bereitstellen von Ressourcen erzwungen werden.

## <a name="disaster-recovery"></a>Notfallwiederherstellung

**Technisches Risiko:** Ressourcenfehler, -löschungen oder -beschädigungen können zu Unterbrechungen unternehmenskritischer Anwendungen oder Dienste sowie dem Verlust vertraulicher Daten führen.

**Richtlinienanweisung:** Für alle unternehmenskritischen Anwendungen und geschützten Daten müssen Sicherungs- und Wiederherstellungslösungen implementiert sein, um die geschäftlichen Auswirkungen von Ausfällen oder Systemfehlern zu minimieren.

**Potenzielle Entwurfsoptionen:** Der [Azure Site Recovery-Dienst](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) bietet Funktionen für die Sicherung, Wiederherstellung und Replikation, um die Ausfalldauer in BCDR-Szenarien (Business Continuity & Disaster Recovery) zu minimieren.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die in diesem Artikel erwähnten Beispiele als Ausgangspunkt für die Entwicklung von Richtlinien, die bestimmte Geschäftsrisiken behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

Um mit der Entwicklung Ihrer eigenen, benutzerdefinierten Richtlinienanweisungen mit Bezug auf die Ressourcenkonsistenz zu beginnen, laden Sie die [Ressourcenkonsistenzvorlage](./template.md) herunter.

Um die Einführung dieser Disziplin zu beschleunigen, wählen Sie den [umsetzbaren Governanceleitfaden](../guides/index.md) aus, der am besten zu Ihrer Umgebung passt. Ändern Sie dann den Entwurf, um Ihre speziellen Entscheidungen für Unternehmensrichtlinien zu integrieren.

Erstellen Sie anhand der Risiken und Toleranzen einen Prozess, mit dem Sie die Einhaltung der Richtlinie für die Ressourcenkonsistenz steuern und kommunizieren.

> [!div class="nextstepaction"]
> [Festlegen von Prozessen für Richtlinienkonformität](./compliance-processes.md)
