---
title: Azure-Serververwaltungstools und -dienste
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Azure-Serververwaltungstools und -dienste
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5bf6ed10a69f18fcd1fac7c6597c035877e41d21
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839416"
---
# <a name="azure-server-management-tools-and-services"></a>Azure-Serververwaltungstools und -dienste

Wie in der [Übersicht](/azure/architecture/cloud-adoption/operations/azure-server-management/) dieses Abschnitts erläutert, deckt die Suite für die Azure-Serververwaltungsdienste die folgenden Bereiche ab:

- [Migrieren](#migrate)
- [Schützen](#secure)
- [Schützen](#protect)
- [Überwachen](#monitor)
- [Konfigurieren](#configure)
- [Steuern](#govern)

In den folgenden Abschnitten werden diese Verwaltungsbereiche kurz beschrieben und Links zu ausführlichen Inhalten zu den Azure-Hauptdiensten bereitgestellt, die diese Bereiche unterstützen.

## <a name="migrate"></a>Migrieren

Migrationsdienste unterstützen Sie bei der Migration Ihrer Workloads zu Azure. Zur optimalen Anleitung startet der Azure Migrate-Dienst zunächst mit dem Messen der lokalen Serverleistung und dem Bewerten der Eignung für die Migration. Nach der Bewertung durch Azure Migrate können Sie mithilfe von [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) und [Azure Database Migration Service](/azure/dms/dms-overview) die lokalen Computer zu Azure migrieren.

## <a name="secure"></a>Schützen

[Azure Security Center](/azure/security-center/security-center-intro) ist eine umfassende Anwendung für die Sicherheitsverwaltung. Durch das Onboarding in das Security Center können Sie schnell eine Bewertung über den Sicherheits- und Konformitätsstatus Ihrer Umgebung erhalten. Anweisungen zum Onboarding Ihrer Server in das Azure Security Center finden Sie unter [Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Schützen

Zum Schutz Ihrer Daten müssen Sicherung, Hochverfügbarkeit, Verschlüsselung, Autorisierung und damit verbundene betriebliche Probleme geplant werden. Diese Themen werden online ausführlich behandelt, daher konzentrieren wir uns hier auf die Erstellung eines BCDR-Plans (Business Continuity Disaster Recovery). Es werden Verweise auf Dokumentationen einbezogen, die ausführlich beschreiben, wie diese Art von Plan implementiert und bereitgestellt wird.

Wenn Sie Datenschutzstrategien erstellen, sollten Sie Ihre Workloadanwendungen zunächst in verschiedene Ebenen unterteilen, da jede Ebene in der Regel einen eigenen, individuellen Schutzplan erfordert. Weitere Informationen über das Entwerfen von robusten Anwendungen finden Sie unter [Entwerfen robuster Anwendungen für Azure](https://docs.microsoft.com/azure/architecture/resiliency).

Der einfachste Datenschutz sind Sicherungen. Sie sollten nicht nur Daten, sondern auch Serverkonfigurationen sichern, um den Wiederherstellungsprozess im Falle eines Serverausfalls zu beschleunigen. Die Sicherung ist ein wirksamer Mechanismus zur Handhabung versehentlicher Datenlöschung und Ransomwareangriffe. [Azure Backup](https://docs.microsoft.com/azure/backup) kann Ihnen beim Schützen von Daten auf Azure- und lokalen Servern unter Windows oder Linux helfen. Weitere Informationen zu den Funktionen dieses Dienstes und Anleitungen finden Sie in der [Dokumentation zu Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Die Wiederherstellung über eine Sicherung kann sehr lange dauern. Gemäß Branchenstandard dauert dies in der Regel einen Tag. Wenn eine Workload für Hardware- oder Rechenzentrumsausfälle eine Geschäftskontinuität erfordert, sollten Sie die Verwendung der Datenreplikation in Betracht ziehen. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) bietet eine fortlaufende Replikation Ihrer VMs – eine Lösung, die minimalen Datenverlust ermöglicht. Site Recovery unterstützt auch verschiedene Replikationsszenarien, z. B. die Replikation von Azure-VMs zwischen zwei Azure-Regionen, zwischen lokalen Servern oder zwischen lokalen Servern und Azure. Weitere Informationen finden Sie in der [vollständige Matrix der Azure Site Recovery-Replikation](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

Für Ihre Dateiserverdaten ist die [Azure-Dateisynchronisierung](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning) ein weiterer zu berücksichtigender Dienst. Mit diesem Dienst können Sie die Dateifreigaben Ihrer Organisation in Azure Files zentralisieren, ohne auf die Flexibilität, Leistung und Kompatibilität eines lokalen Dateiservers verzichten zu müssen. Befolgen Sie die Anweisungen zur Bereitstellung der Azure-Dateisynchronisierung, um diesen Dienst zu nutzen.

## <a name="monitor"></a>Überwachen

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) bietet einen Überblick über verschiedene Ressourcen, wie Anwendungen, Container und virtuelle Computer. Außerdem werden Daten aus mehreren Quellen erfasst.

- Azure Monitor für VMs ([Insights](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)) bietet eine detaillierte Darstellung der Integrität der virtuellen Computer, von Leistungstrends und Abhängigkeiten. Der Dienst überwacht die Integrität der Betriebssysteme für Ihre virtuellen Azure-Computer, VM-Skalierungsgruppen sowie der Computer in Ihrer lokalen Umgebung.
- Log Analytics ([Protokolle](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)) ist ein Feature von Azure Monitor. Die Rolle von Log Analytics ist ein wesentlicher Bestandteil der Azure-Verwaltungsfunktionen. Es dient als Datenspeicher für die Protokollanalyse und für viele andere Azure-Dienste. Es bietet eine umfangreiche Abfragesprache und eine Analyse-Engine, die Ihnen Einblicke in den Betrieb Ihrer Anwendungen und Ressourcen gibt.
- Das [Azure-Aktivitätsprotokoll](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) ist ebenfalls ein Feature von Azure Monitor. Hiermit können Sie Erkenntnisse zu Ereignissen auf Abonnementebene gewinnen, die in Azure eintreten.

## <a name="configure"></a>Konfigurieren

In diese Kategorie fallen mehrere Dienste. Sie können Sie dabei unterstützen, betriebliche Aufgaben zu automatisieren, Serverkonfigurationen zu verwalten, die Konformität von Updates zu messen, Updates zu planen und Änderungen an Ihren Servern zu erkennen. Diese Dienste sind von zentraler Bedeutung für die Unterstützung der laufenden Vorgänge.

- Die [Updateverwaltung](https://docs.microsoft.com/azure/automation/automation-update-management#viewing-update-assessments) automatisiert die Bereitstellung von Patches in Ihrer Umgebung, einschließlich der Bereitstellung auf Betriebssysteminstanzen, die außerhalb von Azure ausgeführt werden. Sie unterstützt sowohl Windows- als auch Linux-Betriebssysteme und verfolgt wichtige Schwachstellen und Nichtkonformitäten im Betriebssystem, die durch fehlende Patches verursacht werden.
- [Änderungsnachverfolgung und Bestand](https://docs.microsoft.com/azure/automation/change-tracking) bietet einen Einblick in die Software, die in Ihrer Umgebung ausgeführt wird, und zeigt alle aufgetretenen Änderungen an.
- [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) bietet die Möglichkeit, Python- und PowerShell-Skripte oder Runbooks auszuführen, um Aufgaben in Ihrer Umgebung zu automatisieren. Wenn Sie es mit dem [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker) verwenden, können Sie Ihre Runbooks außerdem auf lokale Ressourcen erweitern.
- [Azure Automation State Configuration](https://docs.microsoft.com/azure/automation/automation-dsc-overview) bietet die Möglichkeit, PowerShell DSC-Konfigurationen (Desired State Configuration) direkt aus Azure zu pushen. DSC wiederum bietet die Möglichkeit, Betriebssystem- und Workloadkonfigurationen im Gastbetriebssystem zu überwachen und beizubehalten.

## <a name="govern"></a>Steuern

Die Einführung und Umstellung auf die Cloud stellt neue Herausforderungen an die Verwaltung und erfordert ein Umdenken beim Wechsel von einer operativen Verwaltungsaufgabe hin zu Überwachung und Governance. Das Framework für die Cloudeinführung für Azure beginnt mit [Governance](https://docs.microsoft.com/azure/architecture/cloud-adoption/governance/overview). Es erläutert die Migration in die Cloud, die entsprechende Vorgehensweise sowie die beteiligten Personen.

Der Governanceentwurf für kleine und mittlere Unternehmen unterscheidet sich oft dem für große Unternehmen. Weitere Informationen zu bewährten Governancemethoden für kleine und mittlere Unternehmen finden Sie unter [Governancelösung für kleine bis mittlere Unternehmen](https://docs.microsoft.com/azure/architecture/cloud-adoption/governance/journeys/small-to-medium-enterprise/overview). Weitere Informationen zu bewährten Governancemethoden für große Unternehmen finden Sie unter [Governance Journey für große Unternehmen](https://docs.microsoft.com/azure/architecture/cloud-adoption/governance/journeys/large-enterprise/overview).

## <a name="billing-information"></a>Abrechnungsinformationen

Informationen über die Preisgestaltung für Azure-Verwaltungsdienste finden Sie auf den folgenden Seiten:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Azure-Updateverwaltungsdienst](https://azure.microsoft.com/pricing/details/automation)

- [Dienste für Änderungsnachverfolgung und Bestand](https://azure.microsoft.com/pricing/details/automation)

- [Desired State Configuration](https://azure.microsoft.com/pricing/details/automation)

- [Azure Automation-Dienst](https://azure.microsoft.com/pricing/details/automation)

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Azure-Dateisynchronisierungsdienst](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Die Lösung für die Azure-Updateverwaltung ist kostenlos, es fallen jedoch geringe Kosten für die Datenerfassung an. Als Faustregel gilt, dass die ersten 5 GB pro Monat der Datenerfassung kostenlos sind. Wir beobachten im Allgemeinen, dass jeder Computer etwa 25 MB pro Monat verbraucht. So sind etwa 200 Computer pro Monat kostenlos abgedeckt. Multiplizieren Sie für jeden zusätzlichen Server die Anzahl zusätzlicher Server mit 25 MB pro Monat. Multiplizieren Sie dies mit den Speicherkosten für die Gesamtmenge des benötigten Speichers. [Die Speicherkosten sind hier verfügbar.](https://azure.microsoft.com/pricing/details/storage/) Jeder zusätzliche Server sollte einen nominalen Einfluss auf die Kosten haben.
