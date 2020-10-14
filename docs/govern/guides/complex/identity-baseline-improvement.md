---
title: 'Governance in komplexen Unternehmen: Verbessern der Disziplin „Identitätsbaseline“'
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie einem Minimum Viable Product (MVP) für die Governance Steuerungsmechanismen für die Identitätsbaseline hinzufügen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/06/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 1df1e0ae58572beac799f43304018672c9231c47
ms.sourcegitcommit: c2249056464d748a6ce15c82cb35a9f164d8f661
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2020
ms.locfileid: "91108144"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-identity-baseline-discipline"></a>Governanceleitfaden für komplexe Unternehmen: Verbessern der Disziplin „Identitätsbaseline“

In diesem Artikel wird die Lösung weiterentwickelt, indem dem Governance-MVP Steuerungsmechanismen für die Identitätsbaseline hinzugefügt werden.

## <a name="advancing-the-narrative"></a>Fortführen der Geschichte

Die geschäftliche Begründung für die Cloudmigration der zwei Rechenzentren wurde vom CFO genehmigt. Im Rahmen der technischen Machbarkeitsstudie wurden mehrere Hindernisse entdeckt:

- Geschützte Daten und geschäftskritische Anwendungen machen 25 % der Workload in den beiden Rechenzentren aus. Beide lassen sich erst nach einer Modernisierung der aktuellen Governance-Richtlinien für vertrauliche personenbezogene Informationen und geschäftskritische Anwendungen lösen.
- 7 % der Ressourcen in diesen Rechenzentren sind nicht cloudkompatibel. Sie werden vor der Ende des Rechenzentrumsvertrags in ein alternatives Rechenzentrum ausgelagert.
- Bei 15 % der Ressourcen im Rechenzentrum (750 virtuelle Computer) besteht eine Abhängigkeit von Legacyauthentifizierung oder mehrstufiger Authentifizierung von Drittanbietern.
- Die VPN-Verbindung, die bestehende Rechenzentren und Azure verbindet, bietet hinsichtlich Datenübertragungsgeschwindigkeiten oder Latenz keine ausreichende Kapazität, um die Menge der Ressourcen innerhalb der zweijährigen Frist bis zur Stilllegung des Rechenzentrums zu migrieren.

Die zwei ersten Hindernisse werden parallel verwaltet. Dieser Artikel behandelt die Beseitigung des dritten und vierten Hindernisses.

### <a name="expand-the-cloud-governance-team"></a>Erweitern des Cloudgovernanceteams

Das Cloudgovernanceteam wächst. Da zusätzliche Unterstützung bei der Identitätsverwaltung erforderlich ist, nimmt ein Systemadministrator aus dem Identitätsbaselineteam nun an einer wöchentlichen Besprechung teil, um die vorhandenen Teammitglieder über Änderungen auf dem Laufenden zu halten.

### <a name="changes-in-the-current-state"></a>Änderungen des aktuellen Status

Das IT-Team hat die Genehmigung, mit den Plänen von CIO und CFO zur Stilllegung von zwei Rechenzentren fortzufahren. Das Team äußert Bedenken, dass 750 (15 %) der Ressourcen in diesen Rechenzentren an einen anderen Ort außerhalb der Cloud ausgelagert werden müssen.

### <a name="incrementally-improve-the-future-state"></a>Inkrementelles Verbessern des zukünftigen Status

Die neuen Pläne für den zukünftigen Status erfordern eine stabilere Lösung für die Identitätsbaseline, um die 750 virtuellen Computer mit Legacyauthentifizierungsanforderungen zu migrieren. Über diese beiden Rechenzentren hinaus wird erwartet, dass sich diese Herausforderung auf ähnliche Prozentsätze von Ressourcen in anderen Rechenzentren auswirken wird.

Der zukünftige Status erfordert jetzt auch eine Verbindung vom Cloudanbieter zur MPLS-/Mietleitungslösung des Unternehmens.

Die Änderungen des aktuellen und zukünftigen Status bergen neue Risiken, die neue Richtlinienanweisungen erfordern.

## <a name="changes-in-tangible-risks"></a>Änderungen bei konkreten Risiken

**Unterbrechung des Geschäftsbetriebs während der Migration**. Die Migration in die Cloud schafft ein kontrolliertes, zeitlich begrenztes Risiko, das verwaltet werden kann. Das Verlagern alternder Hardware in einen anderen Teil der Welt bringt ein viel höheres Risiko mit sich. Eine Entschärfungsstrategie ist erforderlich, um Unterbrechungen des Geschäftsbetriebs zu vermeiden.

**Bestehende Identitätsabhängigkeiten**. Abhängigkeiten von bestehenden Authentifizierungs- und Identitätsdiensten können die Migration einiger Workloads in die Cloud verzögern oder verhindern. Erfolgt die Rückgabe der zwei Rechenzentren nicht rechtzeitig, fallen Millionen Dollar an Rechenzentren-Leasinggebühren an.

Dieses Unternehmensrisiko lässt sich auf einige technische Risiken erweitern:

- Möglicherweise steht in der Cloud keine Legacyauthentifizierung zur Verfügung, was die Bereitstellung einiger Anwendungen einschränkt.
- Eventuell ist die aktuelle Multi-Factor Authentication-Drittanbieterlösung in der Cloud nicht verfügbar, was die Bereitstellung einiger Anwendungen einschränkt.
- Sowohl die Umstellung auf andere Tools als auch die Auslagerung kann zu Ausfällen oder höheren Kosten führen.
- Die Geschwindigkeit und Stabilität des VPN kann die Migration beeinträchtigen.
- In die Cloud eingehender Datenverkehr kann zu Sicherheitsproblemen in anderen Teilen des globalen Netzwerks führen.

## <a name="incremental-improvement-of-the-policy-statements"></a>Inkrementelle Verbesserungen der Richtlinienanweisungen

Die folgenden Änderungen an der Richtlinie verringern die neuen Risiken und vereinfachen die Implementierung.

- Der gewählte Cloudanbieter muss eine Möglichkeit zur Authentifizierung mithilfe von Legacymethoden bieten.
- Der gewählte Cloudanbieter muss eine Möglichkeit zur Authentifizierung mit der aktuellen Multi-Factor Authentication-Drittanbieterlösung bieten.
- Zwischen dem Cloudanbieter und dem Telekommunikationsanbieter des Unternehmens sollte eine private Hochgeschwindigkeitsverbindung eingerichtet werden, die den Cloudanbieter mit dem globalen Rechenzentrumsnetzwerk verbindet.
- Solange keine ausreichenden Sicherheitsanforderungen implementiert sind, darf kein eingehender öffentlicher Verkehr auf Unternehmensressourcen zugreifen, die in der Cloud gehostet sind. Alle Ports von Quellen außerhalb des globalen WANs sind blockiert.

## <a name="incremental-improvement-of-best-practices"></a>Inkrementelle Verbesserungen von bewährten Methoden

Der Governance-MVP-Entwurf wird so geändert, dass er neue Azure-Richtlinien und eine Implementierung von Active Directory auf einem virtuellen Computer umfasst. Zusammen erfüllen diese beiden Entwurfsänderungen die neuen Richtlinienanweisungen des Unternehmens.

Dies sind die neuen Best Practices:

- **Blaupause für ein sicheres hybrides virtuelles Netzwerk:** Die lokale Seite des Hybridnetzwerks sollte so konfiguriert werden, dass sie Kommunikation zwischen der folgenden Lösung und den lokalen Active Directory-Servern zulässt. Für diese bewährte Methode muss ein Umkreisnetzwerk Active Directory Domain Services über Netzwerkgrenzen hinweg aktivieren.
- **Azure Resource Manager-Vorlagen**:
    1. Definieren Sie eine Netzwerksicherheitsgruppe, um externen Datenverkehr zu blockieren und internen Datenverkehr zuzulassen.
    2. Stellen Sie zwei virtuelle Active Directory-Computer als Paar mit Lastenausgleich auf der Grundlage eines Golden Image bereit. Beim ersten Start führt dieses Image ein PowerShell-Skript aus, um den Domänenbeitritt und die Registrierung bei den Domänendiensten vorzunehmen. Weitere Informationen finden Sie unter [Erweitern von Active Directory Domain Services (AD DS) auf Azure](/azure/architecture/reference-architectures/identity/adds-extend-domain).
- Azure Policy: Wenden Sie die NSG auf alle Ressourcen an.
- Azure Blueprints:
    1. Erstellen Sie eine Blaupause mit dem Namen `active-directory-virtual-machines`.
    2. Fügen Sie der Blaupause jede der Active Directory-Vorlagen und -Richtlinien hinzu.
    3. Veröffentlichen Sie die Blaupause in jeder betroffenen Verwaltungsgruppe.
    4. Wenden Sie die Blaupause auf alle Abonnements an, für die Legacy- oder Multi-Factor Authentication-Drittanbieterauthentifizierung erforderlich ist.
    5. Die Instanz von Active Directory, die in Azure ausgeführt wird, kann nun als Erweiterung der lokalen Active Directory-Lösung verwendet werden, was ihr die Integration des vorhandenen Multi-Factor Authentication-Tools und das Anbieten von anspruchsbasierter Authentifizierung ermöglicht, beides mithilfe vorhandener Active Directory-Funktionen.

## <a name="conclusion"></a>Zusammenfassung

Die Ergänzung des Governance-MVPs um diese Änderungen hilft, viele der in diesem Artikel beschriebenen Risiken abzumildern, wodurch das Cloudeinführungsteam diese Hindernisse schnell hinter sich lassen kann.

## <a name="next-steps"></a>Nächste Schritte

Mit der Fortsetzung der Cloudeinführung und der damit verbundenen Steigerung des Geschäftswerts ändern sich auch die Risiken und Anforderungen an die Cloudgovernance. Die folgenden Artikel behandeln einige Änderungen, die eintreten können. Für das fiktive Unternehmen besteht der nächste Trigger in der Einbeziehung geschützter Daten in den Plan für die Cloudeinführung. Diese Änderung erfordert zusätzliche Sicherheitsmaßnahmen.

> [!div class="nextstepaction"]
> [Verbessern der Disziplin „Sicherheitsbaseline“](./security-baseline-improvement.md)
