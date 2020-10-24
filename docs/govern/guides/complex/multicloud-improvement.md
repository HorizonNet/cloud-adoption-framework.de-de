---
title: 'Governance in komplexen Unternehmen: Multi-Cloud-Verbesserung'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über mehrere Clouds sowie über die Integration von Multi-Cloud-Organisationen für komplexe Unternehmen zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: eebf235af6d824213de04078ce4802212af85056
ms.sourcegitcommit: c2249056464d748a6ce15c82cb35a9f164d8f661
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91107903"
---
# <a name="governance-guide-for-complex-enterprises-multicloud-improvement"></a>Governanceleitfaden für komplexe Unternehmen: Multi-Cloud-Verbesserung

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Microsoft ist sich bewusst, dass Kunden unter Umständen mehrere Clouds für bestimmte Zwecke einführen. Das fiktive Unternehmen in diesem Leitfaden bildet da keine Ausnahme. Parallel zur Einführung von Azure hat der geschäftliche Erfolg zur Übernahme eines kleinen, aber ergänzenden Unternehmens geführt. Das Unternehmen führt sämtliche IT-Vorgänge bei einem anderen Cloudanbieter aus.

In diesem Artikel wird beschrieben, wie sich die Dinge ändern, wenn die neue Organisation integriert wird. Im Rahmen der Geschichte wird davon ausgegangen, dass dieses Unternehmen alle Governanceiterationen abgeschlossen hat, die in diesem Governanceleitfaden beschrieben wurden.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Lösung hatte das Unternehmen damit begonnen, Kostenkontrollen und Kostenüberwachung zu implementieren, da Cloudausgaben Teil der regulären Betriebskosten des Unternehmens werden.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Die Identität wird von einer lokalen Instanz von Active Directory kontrolliert. Hybrididentitäten werden über die Replikation in Azure Active Directory umgesetzt.
- Der IT- oder Cloudbetrieb wird hauptsächlich von Azure Monitor und verwandten Automatisierungsfunktionen verwaltet.
- Business Continuity & Disaster Recovery (BCDR) wird von Azure Recovery Services-Tresoren gesteuert.
- Für die Überwachung von Sicherheitsverletzungen und Angriffen wird Azure Security Center genutzt.
- Azure Security Center und Azure Monitor werden zusammen für die Überwachung der Governance in der Cloud verwendet.
- Azure Blueprints, Azure Policy und Verwaltungsgruppen werden verwendet, um die Richtlinienkonformität zu automatisieren.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Das Ziel ist die Integration des übernommenen Unternehmens in den bestehenden Betrieb, wo immer dies möglich ist.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Kosten der Geschäftsübernahme:** Die Übernahme des neuen Unternehmens soll sich in ungefähr fünf Jahren amortisieren. Aufgrund der langsamen Rendite will der Vorstand die Anschaffungskosten so weit wie möglich kontrollieren. Es besteht die Gefahr von Konflikten zwischen Kostenkontrolle und technischer Integration.

Dieses Unternehmensrisiko lässt sich auf einige technische Risiken erweitern:

- Es besteht die Gefahr, dass die Migration in die Cloud zusätzliche Anschaffungskosten verursacht.
- Es besteht außerdem die Gefahr, dass die neue Umgebung nicht ordnungsgemäß verwaltet ist oder es zu Richtlinienverstößen kommt.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung.

- Die Überwachung sämtlicher Ressourcen in einer sekundären Cloud muss über die vorhandenen Tools zur Geschäftsverwaltung und Sicherheitsüberwachung erfolgen.
- Alle Organisationseinheiten müssen mit dem bestehenden Identitätsanbieter integriert werden.
- Der primäre Identitätsanbieter sollte die Authentifizierung für Ressourcen in der sekundären Cloud steuern.

## <a name="incremental-improvement-of-best-practices"></a>Inkrementelle Verbesserungen von bewährten Methoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so verbessert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management + Billing umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

1. Verbinden der Netzwerke: Vom Netzwerk- und IT-Sicherheitsteam mit Unterstützung durch Governance durchgeführt.
    1. Das Hinzufügen einer Verbindung vom MPLS- oder Mietleitungsanbieter zur neuen Cloud bewirkt die Integration der Netzwerke. Über das Hinzufügen von Routingtabellen und Firewallkonfigurationen werden der Zugriff und der Datenverkehr zwischen den Umgebungen gesteuert.
2. Konsolidieren der Identitätsanbieter: Abhängig von den Workloads, die in der sekundären Cloud gehostet werden, gibt es mehrere Optionen für das Zusammenführen der Identitätsanbieter. Im Folgenden finden Sie einige Beispiele:
    1. Für Anwendungen mit einer Authentifizierung per OAuth 2 können Benutzer von Active Directory in der sekundären Cloud einfach zum vorhandenen Azure AD-Mandanten repliziert werden.
    2. Im anderen Extremfall würde ein Partnerverbund zwischen den zwei lokalen Identitätsanbietern die Replikation der Benutzer aus den neuen Active Directory-Domänen nach Azure ermöglichen.
3. Hinzufügen von Ressourcen zu Azure Site Recovery:
    1. Azure Site Recovery wurde von Anfang an als Hybrid Cloud- und Multi-Cloud-Tool entwickelt.
    2. Virtuelle Computer in der sekundären Cloud können möglicherweise über die gleichen Azure Site Recovery-Prozesse geschützt werden, die auch für lokale Ressourcen verwendet werden.
4. Fügen Sie Azure Cost Management + Billing entsprechende Ressourcen hinzu.
    1. Azure Cost Management + Billing wurde von Anfang an als Multi-Cloud-Tool entwickelt.
    2. Virtuelle Computer in der sekundären Cloud sind bei einigen Cloudanbietern eventuell mit Azure Cost Management + Billing kompatibel. Es können zusätzliche Kosten anfallen.
5. Hinzufügen von Ressourcen zu Azure Monitor:
    1. Azure Monitor wurde von Anfang an als ein Hybrid Cloud-Tool konzipiert.
    2. Virtuelle Computer in der sekundären Cloud sind möglicherweise mit Azure Monitor-Agents kompatibel, sodass sie für die Überwachung der Abläufe in Azure Monitor eingebunden werden können.
6. Tools für die Durchsetzung von Governance.
    1. Die Durchsetzung von Governance ist cloudspezifisch.
    2. Die Unternehmensrichtlinien, die im Governanceleitfaden etabliert wurden, sind hingegen nicht cloudspezifisch. Obwohl die Implementierung von Cloud zu Cloud variieren kann, können die Richtlinienanweisungen auf den sekundären Anbieter angewandt werden.

Die Einführung mehrerer Clouds sollte auf Bereiche beschränkt werden, in denen dies aus technischen oder speziellen geschäftlichen Gründen erforderlich ist. Je mehr Clouds eingeführt werden, desto mehr steigen auch Komplexität und Sicherheitsrisiken.

## <a name="next-steps"></a>Nächste Schritte

In vielen großen Unternehmen können sich die fünf Disziplinen der Cloud-Governance als Einführungshindernisse erweisen. Der nächste Artikel enthält einige zusätzliche Überlegungen dazu, wie Governance zu einer Gemeinschaftsaufgabe gemacht werden kann, um den langfristigen Erfolg in der Cloud zu sichern.

> [!div class="nextstepaction"]
> [Mehrere Governance-Ebenen](./multiple-layers-of-governance.md)
