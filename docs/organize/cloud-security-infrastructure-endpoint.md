---
title: Funktion von Cloudinfrastruktur und Endpunktsicherheit
description: Grundlegendes zur Funktion der Cloudinfrastruktur und Endpunktsicherheit.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 501fda7420de811a6e92de388fa6eb5b981ae324
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88574719"
---
# <a name="function-of-cloud-infrastructure-and-endpoint-security"></a>Funktion von Cloudinfrastruktur und Endpunktsicherheit

Ein Cloudsicherheitsteam, das an der Infrastruktur und Endpunktsicherheit arbeitet, bietet Sicherheitsmaßnahmen, Erkennungs- und Reaktionskontrollen für Infrastruktur- und Netzwerkkomponenten, die von Unternehmensanwendungen und -benutzern verwendet werden.

## <a name="modernization"></a>Modernisierung

Softwaredefinierte Rechenzentren und andere Cloudtechnologien helfen bei der Bewältigung von lange existierender Herausforderungen hinsichtlich der Infrastruktur und Endpunktsicherheit, einschließlich:

- **Ermittlung von Bestands- und Konfigurationsfehlern** ist für in der Cloud gehostete Ressourcen wesentlich zuverlässiger, da sie alle sofort sichtbar sind (im Vergleich zu einem physischen Rechenzentrum).
- **Verwaltung von Sicherheitsrisiken** entwickelt sich zu einem kritischen Teil der generellen Sicherheitsstatusverwaltung.
- Das **Hinzufügen von Containertechnologien**, die von Infrastruktur- und Netzwerkteams verwaltet und gesichert werden sollen, während die Organisation diese Technologie in der Breite einführt. Ein Beispiel finden Sie unter [Containersicherheit in Security Center](/azure/security-center/container-security).
- **Sicherheits-Agent-Konsolidierung** und Toolvereinfachung, um den Wartungs- und Leistungsaufwand von Sicherheits-Agents und -Tools zu verringern.
- **Zulassungslisten von Anwendungen** und interne Netzwerkfilterung lassen sich wesentlich einfacher konfigurieren und für in der Cloud gehostete Server bereitstellen (mithilfe von per Machine Learning generierten Regelsätzen). Azure-Beispiele finden Sie unter [Adaptive Anwendungssteuerung](/azure/security-center/security-center-adaptive-application) und [Adaptive Netzwerkhärtung](/azure/security-center/security-center-adaptive-network-hardening).
- **Automatisierte Vorlagen** zum Konfigurieren der Infrastruktur und Sicherheit lassen sich wesentlich leichter mit softwaredefinierten Rechenzentren in der Cloud verwenden. Ein Azure-Beispiel ist [Azure Blueprints](/azure/governance/blueprints/overview).
- **Just-in-Time (JIT)- und „Just Enough“ (JEA)-Zugriff** ermöglichen die praktische Anwendung der Prinzipien der geringsten Berechtigungen auf privilegierten Zugriff für Server und Endpunkte.
- Die **Benutzeroberfläche** wird zu einem kritischen Aspekt, da Benutzer zunehmend ihre Endpunktgeräte auswählen oder kaufen können.
- **Einheitliche Endpunktverwaltung** ermöglicht das Verwalten des Sicherheitsstatus aller Endpunktgeräte, einschließlich mobiler und herkömmlicher PCs, sowie die Bereitstellung kritischer Geräteintegritätssignale für „Zero Trust“-Zugriffskontrolllösungen.
- **Netzwerksicherheitsarchitekturen** und -kontrollen werden mit der Umstellung auf Cloudanwendungsarchitekturen teilweise geschmälert, bleiben aber eine grundlegende Sicherheitsmaßnahme. Weitere Informationen finden Sie unter [Netzwerksicherheit und -eigenständigkeit](/azure/architecture/framework/security/network-security-containment).

## <a name="team-composition-and-key-relationships"></a>Teamzusammensetzung und wichtige Beziehungen

Cloudinfrastruktur und Endpunktsicherheit interagieren häufig mit den folgenden Rollen:

- IT-Architektur und -Betrieb
- Sicherheitsarchitektur
- Security Operations Center (SOC)
- Complianceteam
- Überwachungsteam

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über die Funktion der [Threat Intelligence](./cloud-security-threat-intelligence.md).
