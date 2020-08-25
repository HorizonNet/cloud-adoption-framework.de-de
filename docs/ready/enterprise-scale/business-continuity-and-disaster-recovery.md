---
title: Business Continuity & Disaster Recovery auf Unternehmensebene
description: Erfahren Sie mehr über Business Continuity & Disaster Recovery auf Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 93975a3064f6d7056bcbe09aad17c60d9fa2cc06
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572781"
---
# <a name="enterprise-scale-business-continuity-and-disaster-recovery"></a>Business Continuity & Disaster Recovery auf Unternehmensebene

Ihre Organisation oder Ihr Unternehmen muss geeignete Funktionen auf Plattformebene entwerfen, die die Workloads der Anwendungen zur Erfüllung ihrer spezifischen Anforderungen nutzen können. Diese Anwendungsworkloads haben insbesondere Anforderungen in Bezug auf Recovery Time Objective (RTO) und Recovery Point Objective (RPO). Stellen Sie sicher, dass Sie die Anforderungen an die Notfallwiederherstellung (Disaster Recovery, DR) erfassen, um die Funktionen für diese Workloads angemessen zu entwerfen.

## <a name="design-considerations"></a>Überlegungen zum Entwurf

Berücksichtigen Sie die folgenden Faktoren:

- Anforderungen an die Anwendungs- und Datenverfügbarkeit und die Verwendung von Aktiv/Aktiv- und Aktiv/Passiv-Verfügbarkeitsmustern (z. B. Anforderungen an Workload-RTO und -RPO)

- Business Continuity & Disaster Recovery für PaaS-Dienste (Plattorm-as-a-Service) und Verfügbarkeit von nativen DR- und Hochverfügbarkeitsfunktionen

- Unterstützung von Bereitstellungen in mehreren Regionen zu Failoverzwecken, wobei Komponenten aus Leistungsgründen nah beieinander platziert werden

- Anwendungsbetrieb mit verringerter Funktionalität oder eingeschränkter Leistung im Falle eines Ausfalls

- Workloadeignung für Verfügbarkeitszonen oder Verfügbarkeitsgruppen

  - Datenfreigabe und Abhängigkeiten zwischen Zonen

  - Die Auswirkungen von Verfügbarkeitszonen auf Updatedomänen im Vergleich zu Verfügbarkeitsgruppen und Prozentsatz der Workloads, die gleichzeitig gewartet werden können

  - Unterstützung für bestimmte SKUs für virtuelle Computer (VM) mit Verfügbarkeitszonen

  - Verwendung von Verfügbarkeitszonen bei Nutzung von Microsoft Azure Disk Storage Ultra erforderlich

- Konsistente Sicherungen für Anwendungen und Daten

  - VM-Momentaufnahmen und Verwendung von Azure Backup und Recovery Services-Tresoren

  - Abonnementlimits schränken die Anzahl von Recovery Services-Tresoren und die Größe jedes Tresors ein

  - Georeplikation und DR-Funktionen für PaaS-Dienste

- Netzwerkkonnektivität bei einem Failover

  - Bandbreitenkapazitätsplanung für Azure ExpressRoute

  - Gekoppelte Failoverregionen

  - Routing von Datenverkehr bei regionalen Ausfällen, Zonen- oder Netzwerkausfällen

- Geplantes und ungeplantes Failover

  - Anforderung konsistenter IP-Adressen und potenzielle Notwendigkeit der Verwaltung von IP-Adressen nach Failover und Failback

  - Verwalten von DevOps-Entwicklerfunktionen

- Azure Key Vault-Notfallwiederherstellung für Anwendungsschlüssel, Zertifikate und Geheimnisse

## <a name="design-recommendations"></a>Entwurfsempfehlungen

Im Folgenden finden Sie bewährte Methoden für Ihren Entwurf:

- Verwenden Sie Azure Site Recovery für Szenarien zur Notfallwiederherstellung von VMs von Azure zu Azure. Auf diese Weise können Sie Workloads regionsübergreifend replizieren.

  Site Recovery bietet integrierte Plattformfunktionen für VM-Workloads, um das geforderte Ziel niedriger RPO/RTO-Werte per Echtzeitreplikation und Wiederherstellungsautomatisierung zu erfüllen. Zusätzlich bietet der Dienst die Möglichkeit, Wiederherstellungstestläufe ohne Auswirkung auf die Workloads in der Produktion auszuführen.

- Verwenden Sie native PaaS-Dienstfunktionen für die Notfallwiederherstellung.

  Die integrierten Features bieten eine einfache Lösung für die komplexe Aufgabe der Konfiguration von Replikation und Failover in einer Workloadarchitektur, indem sowohl der Entwurf als auch die Bereitstellungsautomatisierung vereinfacht werden. Eine Organisation, die einen Standard für die von ihr genutzten Dienste definiert hat, kann außerdem die Dienstkonfiguration mithilfe von Azure Policy überwachen und erzwingen.

- Verwenden Sie native Azure-Funktionen für die Sicherung.

  Dank Azure Backup und PaaS-native Sicherungsfeatures ist es nicht erforderlich, Sicherungssoftware und Infrastrukturkomponenten von Drittanbietern zu verwalten. Wie bei anderen nativen Features können Sie mit Azure Policy Sicherungskonfigurationen festlegen, überwachen und erzwingen. Dadurch wird sichergestellt, dass die Dienste weiterhin den Anforderungen der Organisation entsprechen.

- Verwenden Sie mehrere Regionen und Peeringstandorte für ExpressRoute-Verbindungen.

  Eine redundante hybride Netzwerkarchitektur kann bei einem Ausfall einer Azure-Region oder eines Peering-Anbieterstandorts dazu beitragen, eine unterbrechungsfreie, standortübergreifende Konnektivität zu gewährleisten.

- Informationen zur Auswahl von Standorten für den Entwurf der Notfallwiederherstellung Ihrer Organisation finden Sie in den [Azure-Regionspaaren](/azure/best-practices-availability-paired-regions).

- Verwenden Sie gekoppelte Azure-Regionen, wenn Sie Business Continuity und DR planen.

- Azure führt geplante Systemupdates für Regionspaare nacheinander und nicht gleichzeitig aus. Dadurch lassen sich Downtime, die Auswirkungen von Fehlern und logische Ausfälle im seltenen Fall eines fehlerhaften Updates minimieren.

- Bei einem weitreichenden Ausfall hat bei jedem Regionspaar die Wiederherstellung einer der Regionen Priorität. Für Anwendungen, die in Regionspaaren bereitgestellt sind, wird die priorisierte Wiederherstellung einer der Regionen garantiert. Wenn eine Anwendung in Regionen bereitgestellt wird, die nicht zu Regionspaaren gehören, kann es im schlimmsten Fall zu einer Verzögerung der Wiederherstellung kommen. Es ist möglich, dass die bevorzugte Region zuletzt wiederhergestellt wird.

- Vermeiden Sie Überschneidungen bei den IP-Adressbereichen für Produktions- und DR-Standorte.

  Entwerfen Sie nach Möglichkeit eine Business Continuity- & DR-Netzwerkarchitektur, die eine gleichzeitige Konnektivität mit allen Standorten ermöglicht. Bei DR-Netzwerken, die auf die gleichen klassenlosen Routingblöcke zwischen Domänen zurückgreifen (z. B. bei Produktionsnetzwerken), wird ein Prozess für ein Netzwerkfailover benötigt, der bei einem Anwendungsausfall das Anwendungsfailover erschweren und verzögern kann.

