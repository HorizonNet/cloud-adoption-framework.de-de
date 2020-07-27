---
title: Funktion von Cloudinfrastruktur und Endpunktsicherheit
description: Grundlegendes zur Funktion der Cloudinfrastruktur und Endpunktsicherheit.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: bddab3d91ff2587de55e3a5821b8a369bf3dbbe7
ms.sourcegitcommit: 9163a60a28ffce78ceb5dc8dc4fa1b83d7f56e6d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86450610"
---
# <a name="function-of-cloud-infrastructure-and-endpoint-security"></a>Funktion von Cloudinfrastruktur und Endpunktsicherheit

Ein Cloudsicherheitsteam, das an der Infrastruktur und Endpunktsicherheit arbeitet, bietet Sicherheitsmaßnahmen, Erkennungs- und Reaktionskontrollen für Infrastruktur- und Netzwerkkomponenten, die von Unternehmensanwendungen und -benutzern verwendet werden.

## <a name="modernization"></a>Modernisierung

Softwaredefinierte Rechenzentren und andere Cloudtechnologien helfen bei der Bewältigung von lange existierender Herausforderungen hinsichtlich der Infrastruktur und Endpunktsicherheit, einschließlich:

- **Ermittlung von Bestands- und Konfigurationsfehlern** ist für in der Cloud gehostete Ressourcen wesentlich zuverlässiger, da sie alle sofort sichtbar sind (im Vergleich zu einem physischen Rechenzentrum).
- **Verwaltung von Sicherheitsrisiken** entwickelt sich zu einem kritischen Teil der generellen Sicherheitsstatusverwaltung.
- Das **Hinzufügen von Containertechnologien**, die von Infrastruktur- und Netzwerkteams verwaltet und gesichert werden sollen, während die Organisation diese Technologie in der Breite einführt. Ein Beispiel finden Sie unter [Containersicherheit in Security Center](https://docs.microsoft.com/azure/security-center/container-security).
- **Sicherheits-Agent-Konsolidierung** und Toolvereinfachung, um den Wartungs- und Leistungsaufwand von Sicherheits-Agents und -Tools zu verringern.
- **Zulassungslisten von Anwendungen** und interne Netzwerkfilterung lassen sich wesentlich einfacher konfigurieren und für in der Cloud gehostete Server bereitstellen (mithilfe von per Machine Learning generierten Regelsätzen). Azure-Beispiele finden Sie unter [Adaptive Anwendungssteuerung](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application) und [Adaptive Netzwerkhärtung](https://docs.microsoft.com/azure/security-center/security-center-adaptive-network-hardening).
- **Automatisierte Vorlagen** zum Konfigurieren der Infrastruktur und Sicherheit lassen sich wesentlich leichter mit softwaredefinierten Rechenzentren in der Cloud verwenden. Ein Azure-Beispiel ist [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview).
- **Just-in-Time (JIT)- und „Just Enough“ (JEA)-Zugriff** ermöglichen die praktische Anwendung der Prinzipien der geringsten Berechtigungen auf privilegierten Zugriff für Server und Endpunkte.
- Die **Benutzeroberfläche** wird zu einem kritischen Aspekt, da Benutzer zunehmend ihre Endpunktgeräte auswählen oder kaufen können.
- **Einheitliche Endpunktverwaltung** ermöglicht das Verwalten des Sicherheitsstatus aller Endpunktgeräte, einschließlich mobiler und herkömmlicher PCs, sowie die Bereitstellung kritischer Geräteintegritätssignale für „Zero Trust“-Zugriffskontrolllösungen.
- **Netzwerksicherheitsarchitekturen** und -kontrollen werden mit der Umstellung auf Cloudanwendungsarchitekturen teilweise geschmälert, bleiben aber eine grundlegende Sicherheitsmaßnahme. Weitere Informationen finden Sie unter [Netzwerksicherheit und -eigenständigkeit](https://docs.microsoft.com/azure/architecture/framework/security/network-security-containment).

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Cloudinfrastruktur und Endpunktsicherheit interagieren häufig mit den folgenden Rollen:

- IT-Architektur und -Betrieb
- Sicherheitsarchitektur
- Security Operations Center (SOC)
- Complianceteam
- Überwachungsteam

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Funktion der [Threat Intelligence](./cloud-security-threat-intelligence.md).
