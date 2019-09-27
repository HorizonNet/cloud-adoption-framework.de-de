---
title: 'Standardunternehmensleitfaden: Multi-Cloud-Verbesserung'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Standardunternehmensleitfaden: Multi-Cloud-Verbesserung'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2616193b01b252a74ad17a241d97bfd0ebc4860c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223801"
---
# <a name="small-to-medium-enterprise-guide-multicloud-improvement"></a>Leitfaden für kleine bis mittlere Unternehmen: Multi-Cloud-Verbesserung

Dieser Artikel führt die Geschichte durch neue Steuerungen für die Multi-Cloud-Entwicklung fort.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Microsoft ist sich bewusst, dass Kunden unter Umständen mehrere Clouds für bestimmte Zwecke einführen. Der fiktive Kunde in diesem Leitfaden ist dabei keine Ausnahme. Parallel zur Einführung von Azure hat der geschäftliche Erfolg zur Übernahme eines kleinen, aber ergänzenden Unternehmens geführt. Das Unternehmen führt sämtliche IT-Vorgänge bei einem anderen Cloudanbieter aus.

In diesem Artikel wird beschrieben, wie sich die Dinge ändern, wenn die neue Organisation integriert wird. Im Rahmen der Geschichte wird davon ausgegangen, dass dieses Unternehmen alle Governanceiterationen abgeschlossen hat, die in diesem Governanceleitfaden beschrieben wurden.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

In der vorherigen Phase dieser Geschichte hatte das Unternehmen damit begonnen, Produktionsanwendungen über CI/CD-Pipelines aktiv in die Cloud zu pushen.

Seit diesem Zeitpunkt haben sich einige Dinge geändert, die sich auf die Governance auswirken:

- Die Identitäten werden von einer lokalen Instanz von Active Directory gesteuert. Hybrididentitäten werden über die Replikation in Azure Active Directory umgesetzt.
- IT- oder Cloudvorgänge werden hauptsächlich über Azure Monitor und ähnliche Automatisierungen verwaltetet.
- Notfallwiederherstellung und Geschäftskontinuität werden von Azure Vault-Instanzen kontrolliert.
- Für die Überwachung von Sicherheitsverletzungen und Angriffen wird Azure Security Center genutzt.
- Azure Security Center und Azure Monitor werden zusammen für die Überwachung der Governance in der Cloud verwendet.
- Azure Blueprints, Azure Policy und Azure-Verwaltungsgruppen werden verwendet, um die Richtlinienkonformität zu automatisieren.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Das Ziel ist die Integration des übernommenen Unternehmens in den bestehenden Betrieb, wo immer dies möglich ist.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Kosten der Geschäftsübernahme:** Die Übernahme des neuen Unternehmens soll sich in ungefähr fünf Jahren amortisieren. Aufgrund der langsamen Rendite will der Vorstand die Anschaffungskosten so weit wie möglich kontrollieren. Es besteht das Risiko, dass es zu Konflikten zwischen Kostenkontrolle und technischer Integration kommt.

Dieses Unternehmensrisiko lässt sich auf einige technische Risiken erweitern:

- Die Cloudmigration kann zusätzliche Anschaffungskosten verursachen.
- Die neue Umgebung wird möglicherweise nicht ordnungsgemäß gesteuert, sodass es zu Richtlinienverstößen kommen kann.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung:

- Die Überwachung sämtlicher Ressourcen in einer sekundären Cloud muss über die vorhandenen Tools zur Geschäftsverwaltung und Sicherheitsüberwachung erfolgen.
- Alle Organisationseinheiten müssen mit dem bestehenden Identitätsanbieter integriert werden.
- Der primäre Identitätsanbieter sollte die Authentifizierung für Ressourcen in der sekundären Cloud steuern.

## <a name="incremental-improvement-of-governance-practices"></a>Inkrementelle Verbesserung der Governancemethoden

In diesem Abschnitt des Artikels wird der Governance-MVP-Entwurf so geändert, dass er neue Azure-Richtlinien und eine Implementierung von Azure Cost Management umfasst. Zusammen erfüllen diese Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

1. Verbinden der Netzwerke: Dieser Schritt wird von den Netzwerk- und IT-Sicherheitsteams ausgeführt, die dabei vom Cloudgovernanceteam unterstützt werden. Das Hinzufügen einer Verbindung vom MPLS-/Standleitungsanbieters in die neue Cloud schließt Netzwerke ein. Über das Hinzufügen von Routingtabellen und Firewallkonfigurationen werden der Zugriff und der Datenverkehr zwischen den Umgebungen gesteuert.
2. Konsolidieren der Identitätsanbieter: Abhängig von den Workloads, die in der sekundären Cloud gehostet werden, gibt es mehrere Optionen für das Zusammenführen der Identitätsanbieter. Im Folgenden finden Sie einige Beispiele:
    1. Für Anwendungen mit einer Authentifizierung per OAuth 2 können Benutzer von Active Directory in der sekundären Cloud einfach zum vorhandenen Azure AD-Mandanten repliziert werden. Dadurch wird sichergestellt, dass alle Benutzer im Mandanten authentifiziert werden können.
    2. Im anderen Extremfall erlaubt ein Verbund die Übertragung von Organisationseinheiten in das lokale Active Directory und dann in die Azure AD-Instanz.
3. Hinzufügen von Ressourcen zu Azure Site Recovery:
    1. Azure Site Recovery wurde von Anfang an als Hybrid Cloud- oder Multi-Cloud-Tool entwickelt.
    2. Virtuelle Computer in der sekundären Cloud können möglicherweise über dieselben Azure Site Recovery-Prozesse, die auch für lokale Ressourcen verwendet werden, geschützt werden.
4. Fügen Sie Azure Cost Management Ressourcen hinzu.
    1. Azure Cost Management wurde von Anfang an als Multi-Cloud-Tool entwickelt.
    2. Virtuelle Computer in der sekundären Cloud sind bei einigen alten Cloudanbietern eventuell mit Azure Cost Management kompatibel. Es können zusätzliche Kosten anfallen.
5. Hinzufügen von Ressourcen zu Azure Monitor:
    1. Azure Monitor wurde von Anfang an als ein Hybrid Cloud-Tool konzipiert.
    2. Virtuelle Computer in der sekundären Cloud sind möglicherweise mit Azure Monitor-Agents kompatibel, sodass sie für die Überwachung der Abläufe in Azure Monitor eingebunden werden können.
6. Übernehmen von Tools für die Durchsetzung der Governance.
    1. Die Durchsetzung von Governance ist cloudspezifisch.
    2. Die Unternehmensrichtlinien, die im Governanceleitfaden etabliert wurden, sind hingegen nicht cloudspezifisch. Obwohl die Implementierung von Cloud zu Cloud variieren kann, können die Richtlinien auf den sekundären Anbieter angewandt werden.

Die Einführung mehrerer Clouds sollte auf Bereiche beschränkt werden, in denen dies aus technischen oder speziellen geschäftlichen Gründen erforderlich ist. Eine zunehmende Einführung mehrerer Clouds hat nämlich auch eine höhere Komplexität sowie höhere Sicherheitsrisiken zur Folge.

## <a name="conclusion"></a>Zusammenfassung

Diese Artikelserie beschreibt die inkrementelle Entwicklung von bewährten Methoden bei der Governance im Hinblick auf die Erfahrungen dieses fiktiven Unternehmens. Durch das Anfangen im Kleinen – aber mit dem richtigen Fundament – konnte das Unternehmen den Umstieg schnell bewerkstelligen und dennoch die Governance jederzeit im Auge behalten. Der MVP selbst hat den Kunden nicht geschützt. Stattdessen bildet er die Grundlage, um Risiken zu verwalten und Schutzmaßnahmen hinzuzufügen. Von diesem Punkt aus wurden dann Ebenen der Governance angewandt, um die realen Risiken zu verringern. Die hier beschriebene Journey deckt sich natürlich nicht zu 100 % mit den Erfahrungen aller Leser. Sie dient stattdessen eher als ein Muster für die inkrementelle Governance. Den Lesern wird empfohlen, diese bewährten Methoden an ihre eigenen einzigartigen Einschränkungen und Governanceanforderungen anzupassen.
