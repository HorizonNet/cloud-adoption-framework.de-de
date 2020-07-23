---
title: CAF Business Continuity & Disaster Recovery auf Unternehmensebene
description: Erfahren Sie mehr über Business Continuity & Disaster Recovery auf Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 5e397ed17e9596933629c3d6375546df1e0d9a31
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194781"
---
# <a name="caf-enterprise-scale-business-continuity-and-disaster-recovery"></a>CAF Business Continuity & Disaster Recovery auf Unternehmensebene

## <a name="planning-for-business-continuity-and-disaster-recovery"></a>Planung für Business Continuity & Disaster Recovery

Erfassen Sie Anforderungen an die Notfallwiederherstellung (Disaster Recovery, DR), sodass Sie geeignete Funktionen auf Plattformebene entwerfen können, die von den Anwendungsworkloads zur Erfüllung ihrer spezifischen Anforderungen an Wiederherstellungszeit (Recovery Time Objective, RTO) und Wiederherstellungspunkt (Recovery Point Objective, RPO) genutzt werden können.

**Überlegungen zum Entwurf:**

- Anforderungen an die Anwendungs- und Datenverfügbarkeit und die Verwendung von Aktiv/Aktiv- und Aktiv/Passiv-Verfügbarkeitsmustern (z. B. Anforderungen an Workload-RTO und -RPO)

- Business Continuity und DR für PaaS-Dienste (Plattorm-as-a-Service) und Verfügbarkeit von nativen DR- und Hochverfügbarkeitsfunktionen

- Unterstützung von Bereitstellungen in mehreren Regionen zu Failoverzwecken, wobei Komponenten aus Leistungsgründen nah beieinander platziert werden

- Anwendungsbetrieb mit verringerter Funktionalität oder eingeschränkter Leistung im Falle eines Ausfalls

- Workloadeignung für Verfügbarkeitszonen oder Verfügbarkeitsgruppen

  - Datenfreigabe und Abhängigkeiten zwischen Zonen

  - Auswirkungen von Verfügbarkeitszonen auf Updatedomänen im Vergleich zu Verfügbarkeitsgruppen und Prozentsatz der Workloads, die gleichzeitig gewartet werden können

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

**Entwurfsempfehlungen:**

- Verwenden Sie Azure Site Recovery für Szenarien zur Notfallwiederherstellung von VMs von Azure zu Azure, um Workloads regionsübergreifend zu replizieren.

  Site Recovery bietet integrierte Plattformfunktionen für VM-Workloads, um das geforderte Ziel niedriger RPO/RTO-Werte per Echtzeitreplikation und Wiederherstellungsautomatisierung zu erfüllen. Zusätzlich bietet der Dienst die Möglichkeit, Wiederherstellungstestläufe ohne Auswirkung auf die Workloads in der Produktion auszuführen.

- Verwenden Sie native PaaS-Dienstfunktionen für die Notfallwiederherstellung.

  Die integrierten Features bieten eine einfache Lösung für die komplexe Aufgabe der Konfiguration von Replikation und Failover in einer Workloadarchitektur, indem sowohl der Entwurf als auch die Bereitstellungsautomatisierung vereinfacht werden. Eine Organisation, die einen Standard für die von ihr genutzten Dienste definiert hat, kann außerdem die Dienstkonfiguration mithilfe von Azure Policy überwachen und erzwingen.

- Verwenden Sie native Azure-Funktionen für die Sicherung.

  Dank Azure Backup und PaaS-native Sicherungsfeatures ist es nicht erforderlich, Sicherungssoftware und Infrastrukturkomponenten von Drittanbietern zu verwalten. Wie bei anderen nativen Funktionen können Sicherungskonfigurationen mit Azure Policy festgelegt, überwacht und erzwungen werden, um sicherzustellen, dass die Dienste stets den Anforderungen des Unternehmens entsprechen.

- Verwenden Sie mehrere Regionen und Peeringstandorte für ExpressRoute-Verbindungen.

  Eine redundante hybride Netzwerkarchitektur kann bei einem Ausfall einer Azure-Region oder eines Peering-Anbieterstandorts dazu beitragen, eine unterbrechungsfreie, standortübergreifende Konnektivität zu gewährleisten.

- Informationen zur Auswahl von Standorten für den Disaster Recovery-Entwurf Ihrer Organisation finden Sie in der Dokumentation zu [Azure-Regionspaaren](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

- Verwenden Sie gekoppelte Azure-Regionen, wenn Sie Business Continuity und DR planen.

- Geplante Azure-Systemupdates werden zur Minimierung von Downtime und den Auswirkungen von Fehlern und logischen Ausfällen im seltenen Fall eines fehlerhaften Updates sequenziell (nicht gleichzeitig) ausgeführt.

- Bei einem weitreichenden Ausfall hat bei jedem Regionspaar die Wiederherstellung einer der Regionen Priorität. Für Anwendungen, die in Regionspaaren bereitgestellt sind, wird die priorisierte Wiederherstellung einer der Regionen garantiert. Wenn eine Anwendung in nicht gekoppelten Regionen bereitgestellt ist, kann sich die Wiederherstellung verzögern. Im schlimmsten Fall werden die bevorzugten Regionen als letzte wiederhergestellt.

- Vermeiden Sie Überschneidungen bei den IP-Adressbereichen für Produktions- und DR-Standorte.

  Entwerfen Sie nach Möglichkeit eine Business Continuity- & DR-Netzwerkarchitektur, die eine gleichzeitige Konnektivität mit allen Standorten ermöglicht. Bei DR-Netzwerken, die auf die gleichen klassenlosen Routingblöcke zwischen Domänen zurückgreifen (z. B. bei Produktionsnetzwerken), wird ein Prozess für ein Netzwerkfailover benötigt, der bei einem Anwendungsausfall das Anwendungsfailover erschweren und verzögern kann.
