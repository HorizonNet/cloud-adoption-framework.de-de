---
title: Verwaltung und Überwachung
description: Untersuchen Sie, wie eine Microsoft Azure Enterprise-Umgebung mit zentralisierter Verwaltung und Überwachung auf Plattformebene im laufenden Betrieb gepflegt wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 605b0041ed4cfab683b031b46a5f8f3a769063b2
ms.sourcegitcommit: 826f2a3f0353bb711917e99d9a17f6198fb41ada
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2020
ms.locfileid: "93024554"
---
# <a name="management-and-monitoring"></a>Verwaltung und Überwachung

## <a name="plan-platform-management-and-monitoring"></a>Planen von Plattformverwaltung und -überwachung

In diesem Abschnitt erfahren Sie, wie eine Azure Enterprise-Umgebung mit zentralisierter Verwaltung und Überwachung auf Plattformebene im laufenden Betrieb gepflegt wird. Konkret erhalten Sie wichtige Empfehlungen für zentrale Teams, wie die operative Sichtbarkeit innerhalb einer umfassenden Azure-Plattform gewährleistet werden kann.

![Diagramm zur Verwaltung und Überwachung](./media/management-and-monitoring.png)

_Abbildung 1: Plattformverwaltung und -überwachung._

<!-- cSpell:ignore syslogs SIEM -->

**Überlegungen zum Entwurf:**

- Verwenden Sie einen Azure Monitor Log Analytics-Arbeitsbereich als administrative Grenze.
- Anwendungszentrierte Plattformüberwachung, die den langsamsten und den kalten Telemetriepfad für Metriken und Protokolle umfasst:
  - Betriebssystemmetriken (z. B. Leistungsindikatoren und benutzerdefinierte Metriken)
  - Betriebssystemprotokolle (z. B. Internetinformationsdienste (IIS), Ereignisablaufverfolgung für Windows und Syslog-Protokolle)
  - Ereignisse zur Ressourcenintegrität
- Protokollieren der Sicherheitsüberwachung und Erreichen eines horizontalen Sicherheitsfokus in der gesamten Azure-Umgebung Ihrer Organisation:
  - Mögliche Integration mit lokalen SIEM-Systemen (Security Information & Event Management) wie ServiceNow, ArcSight oder der Onapsis-Sicherheitsplattform
  - Azure-Aktivitätsprotokolle
  - Azure Active Directory-Prüfberichte (Azure AD)
  - Azure-Diagnosedienste, -protokolle und -metriken; Azure Key Vault-Überwachungsereignisse; NSG-Datenflussprotokolle (Netzwerksicherheitsgruppen) und Ereignisprotokolle
  - Azure Monitor, Azure Network Watcher, Azure Security Center und Azure Sentinel
- Azure-Schwellenwerte für die Datenaufbewahrung und Archivierungsanforderungen:
  - Der Standardaufbewahrungszeitraum für Azure Monitor-Protokolle beträgt 30 Tage, maximal zwei Jahre.
  - Der Standardaufbewahrungszeitraum für Azure AD-Berichte (Premium) beträgt 30 Tage.
  - Der Standardaufbewahrungszeitraum für den Azure-Diagnosedienst beträgt 90 Tage.

- Betriebsanforderungen:
  - Operative Dashboards mit systemeigenen Tools wie Azure Monitor-Protokolle oder Tools von Drittanbietern
  - Steuern privilegierter Aktivitäten mit zentralisierten Rollen
  - [Verwaltete Identitäten für Azure-Ressourcen](/azure/active-directory/managed-identities-azure-resources/overview) für den Zugriff auf Azure-Dienste
  - Ressourcensperren zum Verhindern des Bearbeitens und Löschens von Ressourcen

**Entwurfsempfehlungen:**

- Verwenden Sie einen einzigen [Überwachungsprotokoll-Arbeitsbereich](/azure/azure-monitor/platform/design-logs-deployment) zum zentralen Verwalten von Plattformen, es sei denn, die rollenbasierte Zugriffssteuerung (RBAC), Anforderungen hinsichtlich der Datenhoheit und Datenaufbewahrungsrichtlinien schreiben separate Arbeitsbereiche vor. Die zentralisierte Protokollierung ist entscheidend für die Transparenz, die Betriebsführungsteams benötigen. Die Zentralisierung der Protokollierung ermöglicht Berichte zu den Themen Change Management, Dienstintegrität, Konfiguration und den meisten anderen Aspekten des IT-Betriebs. Das Konvergieren in ein zentralisiertes Arbeitsbereichsmodell verringert den Verwaltungsaufwand und mindert mögliche Lücken für Einblicke.

    Im Zusammenhang mit der Architektur auf Unternehmensebene geht es bei der zentralisierten Protokollierung hauptsächlich um Plattformvorgänge. Diese Betonung schließt nicht die Verwendung desselben Arbeitsbereichs für die VM-basierte Anwendungsprotokollierung aus. Ist ein Arbeitsbereich im ressourcenbezogenen Zugriffssteuerungsmodus konfiguriert, wird präzises RBAC erzwungen, um sicherzustellen, dass App-Teams nur Zugriff auf die Protokolle für ihre Ressourcen haben. In diesem Modell profitieren App-Teams von der Nutzung der vorhandenen Plattforminfrastruktur, da sie ihren Verwaltungsaufwand reduzieren können. Für alle Nicht-Computeressourcen, wie Web-Apps oder Azure Cosmos DB-Datenbanken, können Anwendungsteams ihre eigenen Log Analytics-Arbeitsbereiche verwenden und Diagnosen und Metriken konfigurieren, die hierher weitergeleitet werden sollen.

<!-- docutune:ignore WORM -->

- Exportieren Sie Protokolle in Azure Storage, wenn Protokolle länger als zwei Jahre aufbewahrt werden müssen. Verwenden Sie unveränderlichen Speicher mit WORM-Richtlinie (Write Once, Read Many), um Daten für einen vom Benutzer angegebenen Zeitraum festzulegen, dass sie weder gelöscht noch geändert werden können.
- Verwenden Sie Azure Policy für Zugriffssteuerung und Erstellung von Compliance-Berichten. Mit Azure Policy können organisationsweite Einstellungen erzwungen werden, um die konsistente Richtlinieneinhaltung und die schnelle Erkennung von Verstößen sicherzustellen. Weitere Informationen finden Sie unter [Grundlegendes zu Azure Policy-Auswirkungen](/azure/governance/policy/concepts/effects).
- Überwachen Sie VM-Konfigurationsdrifts auf Gastsystemen mit Azure Policy. Wenn Sie [Gastkonfiguration](/azure/governance/policy/concepts/guest-configuration)-Überwachungsfunktionen über Richtlinien aktivieren, können App-Team-Workloads Funktionen direkt mit geringem Aufwand nutzen.
- Verwenden Sie die [Updateverwaltung in Azure Automation](/azure/automation/update-management/overview) als langfristigen Patchingmechanismus für Windows- und Linux-VMs. Durch die Erzwingung von Konfigurationen für die Updateverwaltung mithilfe von Richtlinien wird sichergestellt, dass alle VMs von der Patchverwaltung erfasst werden und dass Anwendungsteams die Patchbereitstellung für ihre VMs verwalten können. Zudem sind für das zentrale IT-Team Sichtbarkeit und Erzwingung für alle VMs sichergestellt.
- Verwenden Sie Network Watcher, um den Datenverkehrsfluss über [Network Watcher-NSG-Datenflussprotokolle v2](/azure/network-watcher/network-watcher-nsg-flow-logging-overview) proaktiv zu überwachen. [Traffic Analytics](/azure/network-watcher/traffic-analytics) analysiert NSG-Datenflussprotokolle, um umfassende Einblicke in den IP-Datenverkehr in einem virtuellen Netzwerk zu erhalten und wichtige Informationen für die effektive Verwaltung und Überwachung bereitzustellen. Traffic Analytics liefert Informationen wie die folgenden: Hosts und Anwendungsprotokolle mit der meisten Kommunikation, Hostpaare mit der meisten gemeinsamen Kommunikation, erlaubter/blockierter Datenverkehr, ein-/ausgehender Datenverkehr, offene Internetports, die Regeln, die am meisten blockieren, die Datenverkehrsverteilung nach Azure-Rechenzentrum, virtuelles Netzwerk, Subnetze oder nicht autorisierte Netzwerke.
- Verhindern Sie mit Ressourcensperren ein versehentliches Löschen kritischer freigegebener Ressourcen.
- Verwenden Sie [Verweigerungsrichtlinien](/azure/governance/policy/concepts/effects#deny), um Azure AD RBAC-Zuweisungen zu ergänzen. Mit Verweigerungsrichtlinien wird verhindert, dass Ressourcen bereitgestellt und konfiguriert werden, die nicht den definierten Standards entsprechen. Dazu wird verhindert, dass die Anforderung an den Ressourcenanbieter gesendet wird. Durch die Kombination von Verweigerungsrichtlinien und RBAC-Zuweisungen wird sichergestellt, dass die geeigneten Überwachungsmechanismen implementiert werden, um zu erzwingen, *wer* Ressourcen bereitstellen und konfigurieren kann und *welche* Ressourcen bereitgestellt und konfiguriert werden können.
- Schließen Sie Ereignisse für die [Dienst](/azure/service-health/service-health-overview)- und die [Ressourcen](/azure/service-health/resource-health-overview)integrität in die Überwachungslösung für die gesamte Plattform ein. Die Verfolgung der Dienst- und Ressourcenintegrität aus der Plattformperspektive ist ein wichtiger Bestandteil der Ressourcenverwaltung in Azure.
- Senden Sie keine unformatierten Protokolleinträge zurück an lokale Überwachungssysteme. Befolgen Sie stattdessen das Prinzip, dass *aus Azure stammende Daten in Azure verbleiben*. Wenn die lokale SIEM-Integration erforderlich ist, [senden Sie kritische Warnungen](/azure/security-center/continuous-export) anstelle von Protokollen.

## <a name="plan-for-app-management-and-monitoring"></a>Planen der App-Verwaltung und -Überwachung

Zur Erweiterung des vorherigen Abschnitts wird in diesem Abschnitt ein Verbundmodell betrachtet, und es wird erläutert, wie Anwendungsteams diese Workloads operativ verwalten können.

**Überlegungen zum Entwurf:**

- Bei der Anwendungsüberwachung können dedizierte Log Analytics Arbeitsbereiche verwendet werden.
- Für Anwendungen, die auf virtuellen Computern bereitgestellt werden, sollten Protokolle aus Plattformsicht zentral im dedizierten Log Analytics-Arbeitsbereich gespeichert werden. Anwendungsteams können auf die Protokolle zugreifen, die der RBAC unterliegen, die auf ihren Anwendungen oder virtuellen Computern vorhanden sind.
- Leistungs- und Integritätsüberwachung für Apps für IaaS- (Infrastructure-as-a-Service) und PaaS-Ressourcen (Platform-as-a-Service)
- Datenaggregation über alle App-Komponenten hinweg
- [Integritätsmodellierung und -operationalisierung](../..//manage/monitor/cloud-models-monitor-overview.md):
  - Messen der Integrität der Workload und ihrer Subsysteme
  - Ein Ampelmodell zur Darstellung der Integrität
  - Reagieren auf Fehler in App-Komponenten

**Entwurfsempfehlungen:**

- Verwenden Sie einen zentralisierten Azure Monitor Log Analytics-Arbeitsbereich, um Protokolle und Metriken aus IaaS- und PaaS-App-Ressourcen zu erfassen und [den Protokollzugriff mit RBAC zu steuern](/azure/azure-monitor/platform/design-logs-deployment#access-control-overview).
- Verwenden Sie [Azure Monitor-Metriken](/azure/azure-monitor/platform/data-platform-metrics) für zeitkritische Analysen. Metriken in Azure Monitor werden in einer Zeitreihendatenbank gespeichert, die für das Analysieren von Daten mit Zeitstempel optimiert ist. Diese Metriken sind besonders für Warnungen und zur schnellen Problemerkennung geeignet. Metriken liefern Informationen zur Leistung Ihres Systems. Sie müssen jedoch in der Regel mit Protokollen kombiniert werden, damit die Ursachen von Problemen identifiziert werden können.
- Verwenden Sie [Azure Monitor-Protokolle](/azure/azure-monitor/platform/data-platform-logs) für Erkenntnisse und Berichte. Protokolle enthalten verschiedene Typen von Daten, die in Datensätzen mit unterschiedlichen Eigenschaften organisiert sind. Sie sind nützlich, um komplexe Daten aus verschiedenen Quellen zu analysieren, z. B. Leistungsdaten, Ereignisse und Ablaufverfolgungen.
- Verwenden Sie ggf. freigegebene Speicherkonten innerhalb der Zielzone als die Speicherung von Protokollen der Azure-Diagnoseerweiterung.
- Verwenden Sie [Azure Monitor-Warnungen](/azure/azure-monitor/platform/alerts-overview), um operative Warnungen zu generieren. Mit Azure Monitor-Warnungen werden Warnungen für Metriken und Protokolle vereinheitlicht, und für erweiterte Verwaltungs- und Wartungszwecke werden Funktionen wie Aktionsgruppen und intelligente Gruppen verwendet.
