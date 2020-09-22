---
title: Azure-Serververwaltungsdienste
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich über die Bereiche der Suite mit den Azure-Serververwaltungsdiensten zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d9c59cf935d122581465fa5d96ffd05bc4e39dd8
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89604027"
---
# <a name="azure-server-management-tools-and-services"></a>Azure-Serververwaltungstools und -dienste

Wie in der [Übersicht](./index.md) zu diesem Leitfaden erläutert, deckt die Suite der Azure-Serververwaltungsdienste die folgenden Bereiche ab:

- Migrieren
- Sicher
- Schützen
- Überwachen
- Konfigurieren
- Steuern

In den folgenden Abschnitten werden diese Verwaltungsbereiche kurz beschrieben und Links zu ausführlichen Inhalten zu den Azure-Hauptdiensten bereitgestellt, die diese Bereiche unterstützen.

## <a name="migrate"></a>Migrieren

Migrationsdienste unterstützen Sie bei der Migration Ihrer Workloads zu Azure. Zur optimalen Anleitung startet der Azure Migrate-Dienst zunächst mit dem Messen der lokalen Serverleistung und dem Bewerten der Eignung für die Migration. Nach der Bewertung durch Azure Migrate können Sie mithilfe von [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) und [Azure Database Migration Service](/azure/dms/dms-overview) die lokalen Computer zu Azure migrieren.

## <a name="secure"></a>Sicher

[Azure Security Center](/azure/security-center/security-center-intro) ist eine umfassende Anwendung für die Sicherheitsverwaltung. Durch das Onboarding in das Security Center können Sie schnell eine Bewertung über den Sicherheits- und Konformitätsstatus Ihrer Umgebung erhalten. Anweisungen zum Onboarding Ihrer Server in das Azure Security Center finden Sie unter [Konfigurieren von Azure-Verwaltungsdiensten für ein Abonnement](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Schützen

Zum Schutz Ihrer Daten müssen Sicherung, Hochverfügbarkeit, Verschlüsselung, Autorisierung und damit verbundene betriebliche Probleme geplant werden. Diese Themen werden ausführlich online behandelt, daher konzentrieren wir uns hier auf die Erstellung eines BCDR-Plans (Business Continuity & Disaster Recovery). Es werden Verweise auf Dokumentationen einbezogen, die ausführlich beschreiben, wie diese Art von Plan implementiert und bereitgestellt wird.

Wenn Sie Datenschutzstrategien erstellen, sollten Sie zunächst überlegen, Ihre Workloadanwendungen in ihre verschiedenen Ebenen aufzuteilen. Dieser Ansatz hilft, da jede Ebene in der Regel einen eigenen, individuellen Schutzplan erfordert. Weitere Informationen über das Entwerfen von robusten Anwendungen finden Sie unter [Entwerfen robuster Anwendungen für Azure](/azure/architecture/resiliency).

Der einfachste Datenschutz sind Sicherungen. Sie sollten nicht nur Daten, sondern auch Serverkonfigurationen sichern, um den Wiederherstellungsprozess im Falle eines Serverausfalls zu beschleunigen. Die Sicherung ist ein wirksamer Mechanismus zur Handhabung versehentlicher Datenlöschung und Ransomwareangriffe. [Azure Backup](/azure/backup) kann Ihnen beim Schützen von Daten auf Azure- und lokalen Servern unter Windows oder Linux helfen. Weitere Informationen darüber, was Backup leisten kann, und Anleitungen dazu finden Sie in der [Übersicht zum Azure Backup-Dienst](/azure/backup/backup-overview).

Wenn eine Workload für Hardware- oder Rechenzentrumsausfälle eine Geschäftskontinuität in Echtzeit erfordert, sollten Sie die Verwendung der Datenreplikation in Betracht ziehen. [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) bietet eine fortlaufende Replikation Ihrer VMs – eine Lösung, die minimalen Datenverlust ermöglicht. Site Recovery unterstützt u. a. auch folgende Replikationsszenarien:

- Replikation von Azure-VMs zwischen zwei Azure-Regionen.
- Replikation zwischen lokalen Servern.
- Replikation zwischen lokalen Servern und Azure.

Weitere Informationen finden Sie in der [vollständige Matrix der Azure Site Recovery-Replikation](/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

Für Ihre Dateiserverdaten ist die [Azure-Dateisynchronisierung](/azure/storage/files/storage-sync-files-planning) ein weiterer zu berücksichtigender Dienst. Dieser Dienst unterstützt Sie dabei, die Dateifreigaben Ihrer Organisation in Azure Files zu zentralisieren, ohne auf die Flexibilität, Leistung und Kompatibilität eines lokalen Dateiservers verzichten zu müssen. Befolgen Sie die Anweisungen zur Bereitstellung der Azure-Dateisynchronisierung, um diesen Dienst zu nutzen.

## <a name="monitor"></a>Überwachen

[Azure Monitor](/azure/azure-monitor/overview) bietet einen Überblick über verschiedene Ressourcen, wie Anwendungen, Container und virtuelle Computer. Außerdem werden Daten aus mehreren Quellen erfasst:

- [Azure Monitor für VMs](/azure/azure-monitor/insights/vminsights-overview) bietet eine detaillierte Darstellung der Integrität der virtuellen Computer, von Leistungstrends und Abhängigkeiten. Der Dienst überwacht die Integrität der Betriebssysteme für Ihre virtuellen Azure-Computer, VM-Skalierungsgruppen sowie der Computer in Ihrer lokalen Umgebung.
- [Log Analytics](/azure/azure-monitor/log-query/log-query-overview) ist ein Feature von Azure Monitor. Die Rolle von Log Analytics ist ein wesentlicher Bestandteil der Azure-Verwaltungsfunktionen. Es dient als Datenspeicher für die Protokollanalyse und für viele andere Azure-Dienste. Es bietet eine umfangreiche Abfragesprache und eine Analyse-Engine, die Ihnen Einblicke in den Betrieb Ihrer Anwendungen und Ressourcen gibt.
- Das [Azure-Aktivitätsprotokoll](/azure/azure-monitor/platform/activity-logs-overview) ist ebenfalls ein Feature von Azure Monitor. Hiermit können Sie Erkenntnisse zu Ereignissen auf Abonnementebene gewinnen, die in Azure eintreten.

## <a name="configure"></a>Konfigurieren

In diese Kategorie fallen mehrere Dienste. Diese können Ihnen bei Folgendem helfen:

- Automatisieren von operativen Aufgaben
- Verwalten von Serverkonfigurationen
- Messen der Updatekonformität
- Planen von Updates
- Löschen von Änderungen an Ihren Servern

Diese Dienste sind von zentraler Bedeutung für die Unterstützung der laufenden Vorgänge:

- Die [Updateverwaltung](/azure/automation/automation-update-management) automatisiert die Bereitstellung von Patches in Ihrer Umgebung, einschließlich der Bereitstellung auf Betriebssysteminstanzen, die außerhalb von Azure ausgeführt werden. Sie unterstützt sowohl Windows- als auch Linux-Betriebssysteme und verfolgt wichtige Schwachstellen und Nichtkonformitäten im Betriebssystem, die durch fehlende Patches verursacht werden.
- [Änderungsnachverfolgung und Bestand](/azure/automation/change-tracking) bietet einen Einblick in die Software, die in Ihrer Umgebung ausgeführt wird, und hebt alle aufgetretenen Änderungen hevor.
- [Azure Automation](/azure/automation/automation-intro) bietet die Möglichkeit, Python- und PowerShell-Skripte oder Runbooks auszuführen, um Aufgaben in Ihrer Umgebung zu automatisieren. Wenn Sie die Automatisierung mit dem [Hybrid Runbook Worker](/azure/automation/automation-hybrid-runbook-worker) verwenden, können Sie Ihre Runbooks außerdem auf lokale Ressourcen erweitern.
- [Azure Automation State Configuration](/azure/automation/automation-dsc-overview) bietet die Möglichkeit, PowerShell DSC-Konfigurationen (Desired State Configuration) direkt aus Azure zu pushen. Mit DSC können Sie auch Konfigurationen für Gastbetriebssysteme und Workloads überwachen und beibehalten.

## <a name="govern"></a>Steuern

Die Einführung und der Wechsel in die Cloud stellt neue Anforderungen an die Verwaltung. Sie erfordert ein Umdenken beim Wechsel von einer operativen Verwaltungsaufgabe hin zu Überwachung und Governance. Das Cloud Adoption Framework beginnt mit [Governance](../../govern/index.md). Das Framework erläutert die Migration in die Cloud, die entsprechende Vorgehensweise sowie die beteiligten Personen.

Der Governance-Entwurf für Standardorganisationen unterscheidet sich oft von dem für komplexe Unternehmen. Weitere Informationen zu bewährten Governancemethoden für ein Standardunternehmen finden Sie im [Governanceleitfaden für Standardunternehmen](../../govern/guides/standard/index.md). Weitere Informationen zu bewährten Governancemethoden für ein komplexes Unternehmen finden Sie im [Governanceleitfaden für komplexe Unternehmen](../../govern/guides/complex/index.md).

## <a name="billing-information"></a>Abrechnungsinformationen

Informationen über die Preisgestaltung für Azure-Verwaltungsdienste finden Sie auf den folgenden Seiten:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Azure Automation](https://azure.microsoft.com/pricing/details/automation), einschließlich:
  - Desired State Configuration
  - Azure-Updateverwaltungsdienst
  - Azure-Dienste für Änderungsnachverfolgung und Bestand

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Azure-Dateisynchronisierungsdienst](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Die Lösung für die Azure-Updateverwaltung ist kostenlos, es fallen jedoch geringe Kosten für die Datenerfassung an. Als Faustregel gilt, dass die ersten 5 GB pro Monat der Datenerfassung kostenlos sind. Wir beobachten im Allgemeinen, dass jeder Computer etwa 25 MB pro Monat verbraucht. So sind etwa 200 Computer pro Monat kostenlos abgedeckt. Multiplizieren Sie für weitere Server die Anzahl zusätzlicher Server mit 25 MB pro Monat. Multiplizieren Sie dann das Ergebnis mit dem Speicherpreis für den zusätzlichen Speicher, den Sie benötigen. Informationen zu Kosten finden Sie unter [Übersicht über die Preise für Azure Storage](https://azure.microsoft.com/pricing/details/storage). Jeder zusätzliche Server sollte in der Regel einen nominalen Einfluss auf die Kosten haben.
