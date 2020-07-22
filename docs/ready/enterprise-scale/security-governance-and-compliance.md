---
title: 'CAF: Sicherheitsgovernance und Compliance auf Unternehmensebene'
description: Erfahren Sie mehr über Sicherheitsgovernance und Compliance auf Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 4cb0baf0a5f64b2720ef9cf8c3a4b6dae6299688
ms.sourcegitcommit: 84d7bfd11329eb4c151c4c32be5bab6c91f376ed
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86235278"
---
# <a name="caf-enterprise-scale-security-governance-and-compliance"></a>CAF: Sicherheitsgovernance und Compliance auf Unternehmensebene

## <a name="define-encryption-and-key-management"></a>Definieren von Verschlüsselung und Schlüsselverwaltung

Verschlüsselung ist ein wichtiger Schritt zur Gewährleistung von Datenschutz, Compliance und Data Residency in Microsoft Azure. Die Verschlüsselung ist auch bei vielen Unternehmen einer der wichtigsten Sicherheitsaspekte. In diesem Abschnitt werden die Entwurfsüberlegungen und -empfehlungen in Bezug auf Verschlüsselung und Schlüsselverwaltung behandelt.

**Überlegungen zum Entwurf:**

- Für Azure Key Vault geltende Abonnement- und Skalierungsgrenzwerte: Key Vault weist Transaktionsgrenzwerte für Schlüssel und Geheimnisse auf. Informationen zum Drosseln von Transaktionen pro Tresor in einem bestimmten Zeitraum finden Sie unter ([Azure-Grenzwerte](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits)).

- Key Vault dient als Sicherheitsgrenze, da Zugriffsberechtigungen für Schlüssel, Geheimnisse und Zertifikate auf Tresorebene gelten. Mithilfe von Zuweisungen von Key Vault-Zugriffsrichtlinien werden Berechtigungen getrennt nach Schlüsseln, Geheimnissen oder Zertifikaten zugewiesen. Sie unterstützen aber keine differenzierten objektbezogenen Berechtigungen wie einen bestimmten Schlüssel, ein bestimmtes Geheimnis oder Zertifikat ([Schlüsselverwaltung](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices)).

- Sie können je nach Bedarf anwendungs- und workloadspezifische Geheimnisse und gemeinsam genutzte Schlüssel isolieren ([Zugriffssteuerung](https://docs.microsoft.com/azure/key-vault/general/best-practices)).

<!-- cSpell:ignore FIPS -->

- Premium-SKUs können optimiert werden, sobald durch Hardwaresicherheitsmodule geschützte Schlüssel erforderlich sind. Die zugrunde liegenden Hardwaresicherheitsmodule (HSMs) sind konform mit FIPS 140-2 Level 2. Von Azure verwaltetes dediziertes HSM für Compliance mit FIPS 140-2 Level 3 mit Berücksichtigung der unterstützten Szenarien.

- Schlüsselrotation und Ablauf von Geheimnissen.

  - Zertifikatbeschaffung und -signierung mit Key Vault ([über Zertifikate](https://docs.microsoft.com/azure/key-vault/certificates/about-certificates))
  - Warnungen/Benachrichtigungen und automatisierte Zertifikatverlängerungen

- Anforderungen an die Notfallwiederherstellung für Schlüssel, Zertifikate und Geheimnisse.

  Replikations- und Failoverfunktionen für den Key Vault-Dienst: ([Verfügbarkeit und Redundanz](https://docs.microsoft.com/azure/key-vault/general/disaster-recovery-guidance)).

- Überwachen der Nutzung von Schlüsseln, Zertifikaten und Geheimnissen.

  Erkennen von nicht autorisiertem Zugriff mithilfe eines Schlüsseltresors oder Log Analytics-Arbeitsbereichs von Azure Monitor: ([Überwachung und Warnung](https://docs.microsoft.com/azure/key-vault/general/alert))

- Delegierte Key Vault-Instanziierung und privilegierter Zugriff: ([sicherer Zugriff](https://docs.microsoft.com/azure/key-vault/general/secure-your-key-vault))

- Anforderungen im Zusammenhang mit der Nutzung benutzerdefinierter Schlüssel für native Verschlüsselungsmechanismen wie Azure-Speicherdienstverschlüsselung (Storage Service Encryption, SSE):
  - [Kundenseitig verwaltete Schlüssel](https://docs.microsoft.com/azure/storage/common/storage-encryption-keys-portal).
  - Vollständige Datenträgerverschlüsselung für virtuelle Computer (VMs).
  - Verschlüsselung von Daten während der Übertragung.
  - Verschlüsselung ruhender Daten.

**Entwurfsempfehlungen:**

- Nutzen Sie ein Azure Key Vault-Verbundmodell, um Beschränkungen des Transaktionsumfangs zu vermeiden.

- Stellen Sie Azure Key Vault mit Richtlinien für vorläufiges und endgültiges Löschen bereit, damit Aufbewahrungsschutz für gelöschte Objekte aktiviert werden kann.

- Befolgen Sie ein Modell der geringsten Rechte, indem Sie die Autorisierung zum permanenten Löschen von Schlüsseln, Geheimnissen und Zertifikaten auf spezielle benutzerdefinierte Azure Active Directory-Rollen beschränken.

- Automatisieren Sie den Prozess zur Verwaltung und Verlängerung von Zertifikaten mit öffentlichen Zertifizierungsstellen, um die Verwaltung zu erleichtern.

- Führen Sie einen automatisierten Prozess für die Rotation von Schlüsseln und Zertifikaten ein.

- Aktivieren Sie den Dienstendpunkt für die Firewall und das virtuelle Netzwerk im Tresor für den Zugriff auf den Schlüsseltresor.

- Verwenden Sie den für die Plattform zentralen Log Analytics-Arbeitsbereich von Azure Monitor, um die Verwendung von Schlüsseln, Zertifikaten und Geheimnissen innerhalb jeder Key Vault-Instanz zu überwachen.

- Delegieren Sie die Instanziierung von Key Vault und den privilegierten Zugriff, indem Sie mithilfe von Azure Policy eine einheitliche, konforme Konfiguration erzwingen.

- Greifen Sie bei Bedarf standardmäßig auf von Microsoft verwaltete Schlüssel für die grundlegende Verschlüsselungsfunktionalität zurück, und nutzen Sie bei Bedarf vom Kunden verwaltete Schlüssel.

- Verwenden Sie keine zentralisierten Key Vault-Instanzen für Anwendungsschlüssel oder -geheimnisse.

- Geben Sie keine Key Vault-Instanzen zwischen Anwendungen frei, um die gemeinsame Nutzung von Geheimnissen in verschiedenen Umgebungen zu vermeiden.

## <a name="planning-for-governance"></a>Planen für Governance

Governance stellt Mechanismen und Prozesse zum Beibehalten der Kontrolle über Ihre Anwendungen und Ressourcen in Azure bereit. Azure Policy ist für die Gewährleistung von Sicherheit und Compliance innerhalb der IT-Umgebung von Unternehmen unerlässlich. Der Dienst kann wichtige Verwaltungs- und Sicherheitskonventionen für alle Dienste auf der Azure-Plattform erzwingen und die rollenbasierte Zugriffssteuerung ergänzen, die regelt, welche Aktionen autorisierte Benutzer ausführen dürfen.

**Überlegungen zum Entwurf:**

- Ermitteln der erforderlichen Azure-Richtlinien

- Erzwingung von Verwaltungs- und Sicherheitskonventionen, wie z. B. Nutzung privater Endpunkte

- Zum Verwalten und Erstellen von Richtlinienzuweisungen können Richtliniendefinitionen in mehreren vererbten Zuweisungsbereichen wiederverwendet werden. Auf Verwaltungsgruppen-, Abonnement- und Ressourcengruppenebene kann es zentralisierte, grundlegende Richtlinienzuweisungen geben.

- Berichterstellung und Überwachung zum Gewährleisten einer durchgängigen Compliance

- Azure Policy weist Grenzwerte auf, wie z. B. die Beschränkung von Definitionen auf einer beliebigen Ebene: ([Richtliniengrenzwerte](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits))

- Richtlinien zur Einhaltung von Vorschriften wie Health Insurance Portability and Accountability Act, Payment Card Industry (PCI), Data Security Standards, Service Organisation Controls (SOC), Trust Service Principals und Kriterien.

**Entwurfsempfehlungen:**

- Bestimmen Sie erforderliche Azure-Tags, und nutzen Sie den Modus zum Anfügen von Richtlinien, um die Nutzung zu erzwingen.

- Ordnen Sie regulatorische und Complianceanforderungen Azure Policy-Definitionen und Zuweisungen gemäß der rollenbasierter Zugriffssteuerung von Azure AD zu.

- Legen Sie Azure Policy-Definitionen in der Stammverwaltungsgruppe auf oberster Ebene fest, damit sie in vererbten Bereichen zugewiesen werden können.

- Verwalten Sie Zuweisungen von Richtlinien auf der höchsten geeigneten Ebene mit Ausschlüssen auf unteren Ebenen, sofern erforderlich.

- Nutzen Sie Azure Policy zum Steuern von Registrierungen von Ressourcenanbietern auf Abonnement- und/oder Verwaltungsgruppenebene.

- Nutzen Sie nach Möglichkeit integrierte Richtlinien, um den betrieblichen Aufwand zu minimieren.

- Weisen Sie die Rolle „Mitwirkender“ in der integrierte Richtlinie einem bestimmten Bereich zu, um Governance auf Anwendungsebene zu ermöglichen.

- Beschränken Sie die Anzahl der Azure Policy-Zuweisungen, die im Bereich der Stammverwaltungsgruppe vorgenommen werden, um eine Verwaltung durch Ausschlüsse in vererbten Bereichen zu vermeiden.

## <a name="define-security-monitoring-and-an-audit-policy"></a>Definieren der Sicherheitsüberwachung und einer Überwachungsrichtlinie

Für ein Unternehmen ist es unerlässlich, einen Einblick in die Vorgänge innerhalb seiner Cloudumgebung zu erhalten. Die Sicherheitsüberwachung und Überwachungsprotokollierung der Dienste auf der Azure-Plattform ist eine wesentliche Komponente eines skalierbaren Frameworks.

**Überlegungen zum Entwurf:**

- Datenaufbewahrungsfristen für Überwachungsdaten: Azure AD-Berichte (Premium) haben einen Aufbewahrungszeitraum von 30 Tagen.

- Langfristige Archivierung von Protokollen wie Azure-Aktivitäts-, VM- und PaaS-Protokollen (Platform-as-a-Service)

- Grundlegende Sicherheitskonfiguration über eine Azure-Gast-VM-Richtlinie

- Notfallpatches für kritische Sicherheitsrisiken

- Patches für VMs, die über längere Zeiträume offline sind

- Anforderungen für Echtzeitüberwachung und Warnungen

- Integrieren von SIEM-Lösung (Security Information and Event Management) in Azure Security Center und Azure Sentinel

- Beurteilung des Sicherheitsrisikos von VMs

**Entwurfsempfehlungen:**

- Nutzen Sie Azure AD-Berichtsfunktionen zum Generieren von Überwachungsberichten zur Zugriffssteuerung.

- Exportieren Sie Azure-Aktivitätsprotokolle zur langfristigen Datenaufbewahrung in Azure Monitor-Protokolle und bei Bedarf in Azure Storage zur langfristigen Speicherung über zwei Jahre hinaus.

- Aktivieren Sie Security Center (Standard-SKU) für alle Abonnements mithilfe von Azure Policy, um Compliance sicherzustellen.

- Überwachen Sie Abweichungen bei Patches des Basisbetriebssystems mittels Azure Monitor-Protokollen und Azure Security Center.

- Nutzen Sie Azure-Richtlinien zur automatischen Bereitstellung von Softwarekonfigurationen mithilfe von VM-Erweiterungen und zur Erzwingung einer konformen VM-Basiskonfiguration.

- Überwachen Sie Abweichungen bei der VM-Sicherheitskonfiguration mittels Azure Policy.

- Verbinden Sie Standardressourcenkonfigurationen mit einem zentralen Log Analytics-Arbeitsbereich von Azure Monitor.

- Verwenden Sie eine Event Grid-basierte Lösung für protokollorientierte Echtzeitwarnungen.

## <a name="plan-for-platform-security"></a>Planen der Plattformsicherheit

Sie müssen eine stabile Sicherheitslage aufrechterhalten, wenn Sie Azure einführen. Neben Sichtbarkeit müssen Sie in der Lage sein, die anfänglichen Einstellungen und Änderungen zu bestimmen, während sich die Azure-Dienste weiterentwickeln. Daher ist die Planung der Plattformsicherheit von großer Bedeutung.

**Überlegungen zum Entwurf:**

- Gemeinsame Verantwortung

- Hochverfügbarkeit und Notfallwiederherstellung

- Einheitliche Sicherheit in allen Azure-Diensten in Bezug auf Datenverwaltungs- und Steuerungsebenenvorgänge

- Mehrmandantenfähigkeit für wichtige Plattformkomponenten – von Hyper-V und den HSMs, die Key Vault zugrunde liegen, bis zu Datenbank-Engines

**Entwurfsempfehlungen:**

- Eine gemeinsame Untersuchung jedes erforderlichen Diensts muss im Kontext Ihrer zugrunde liegenden Anforderungen erfolgen. Wenn Sie Ihre eigenen Schlüssel einsetzen möchte, wird dies möglicherweise nicht von allen in Frage kommenden Diensten unterstützt. Entsprechende Abhilfemaßnahmen müssen umgesetzt werden, damit Inkonsistenzen die gewünschten Ergebnisse nicht beeinträchtigen. Wählen Sie geeignete Regionspaare und Regionen für die Notfallwiederherstellung, die Latenz minimieren.

- Entwickeln Sie einen Plan zum Erstellen einer Zulassungsliste für die Sicherheit, um die Sicherheitskonfiguration, Überwachung und Warnungen von Diensten sowie deren Integration in bestehende Systeme zu beurteilen.

- Legen Sie vor dem Erstellen einer Zulassungsliste für Azure-Dienste einen Plan zur Reaktion auf Vorfälle fest.

- Nutzen Sie Azure AD-Berichtsfunktionen zum Generieren von Überwachungsberichten zur Zugriffssteuerung.

- Stimmen Sie Ihre Sicherheitsanforderungen mit Roadmaps für die Azure-Plattform ab, um bei neu veröffentlichten Sicherheitssteuerungen auf dem Laufenden zu bleiben.

- Setzen Sie ggf. einen Zero-Trust-Ansatz für den Zugriff auf die Azure-Plattform um.

## <a name="service-enablement-framework"></a>Dienstaktivierungsframework

Wenn Geschäftsbereiche die Bereitstellung von Workloads in Azure anfordern, ist ein zusätzlicher Einblick in eine Workload erforderlich, um zu bestimmen, wie ein angemessenes Maß an Governance, Sicherheit und Compliance erreicht werden kann. Wenn ein neuer Dienst benötigt wird, für den noch kein Onboarding durchgeführt wurde, muss der Dienst zugelassen werden. Die folgende Tabelle bietet ein Framework zur Beurteilung der Sicherheitsbereitschaft von Azure-Diensten in Unternehmen:

| Bewertung                    | Category                                                              | Kriterien                                                                                                                                     |
|------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Sicherheit                     | Netzwerkendpunkt                                                      | Verfügt der Dienst über einen öffentlichen Endpunkt, der außerhalb eines virtuellen Netzwerks zugänglich ist?                                                                |
|                              |                                                                       | Werden Endpunkte virtueller Netzwerkdienste unterstützt?                                                                                                      |
|                              |                                                                       | Können Azure-Dienste direkt mit dem Dienstendpunkt interagieren?                                                                              |
|                              |                                                                       | Werden Private Link-Endpunkte unterstützt?                                                                                                           |
|                              |                                                                       | Ist eine Bereitstellung in einem virtuellen Netzwerk möglich?                                                                                                            |
|                              | Verhinderung der Datenexfiltration                                          | Verfügt der PaaS-Dienst im ExpressRoute-Microsoft-Peering über eine separate Border Gateway Protocol-Community? (Anders ausgedrückt, macht er einen Routenfilter für den Dienst verfügbar?) |
|                              |                                                                       | Werden vom Dienst Private Link-Endpunkte unterstützt?                                                                                                       |
|                              | Netzwerkdatenverkehr für Verwaltungs- und Datenebenenvorgänge erzwingen | Ist es möglich, den in den Dienst ein- und ausgehenden Datenverkehr zu inspizieren? Kann mit benutzerdefiniertem Routing ein Tunnel für Datenverkehr erzwungen werden?                                    |
|                              |                                                                       | Nutzen Verwaltungsvorgänge von Azure gemeinsam genutzte öffentliche IP-Adressbereiche?                                                                                 |
|                              |                                                                       | Wird der Verwaltungsdatenverkehr über einen Link-Local-Endpunkt auf dem Host verfügbar gemacht?                                                                |
|                              | Verschlüsselung ruhender Daten                                               | Wird Verschlüsselung standardmäßig angewendet?                                                                                                            |
|                              |                                                                       | Kann Verschlüsselung deaktiviert werden?                                                                                                                  |
|                              |                                                                       | Erfolgt Verschlüsselung mit von Microsoft verwalteten oder vom Kunden verwalteten Schlüsseln?                                                   |
|                              | Datenverschlüsselung während der Übertragung                                            | Ist Datenverkehr an den Dienst auf Protokollebene verschlüsselt (Secure Sockets Layer/Transport Layer Security)?                                                                           |
|                              |                                                                       | Gibt es HTTP-Endpunkte, und können diese deaktiviert werden?                                                                                        |
|                              |                                                                       | Ist die zugrunde liegende Dienstkommunikation ebenfalls verschlüsselt?                                                                                          |
|                              |                                                                       | Erfolgt Verschlüsselung mit von Microsoft verwalteten oder vom Kunden verwalteten Schlüsseln? (Wird BYOK-Verschlüsselung [Bring Your Own Key] unterstützt?)                                                                               |
|                              | Softwarebereitstellung                                                   | Können Anwendungssoftware oder Produkte von Drittanbietern im Dienst bereitgestellt werden?                                                                 |
|                              |                                                                       | Wie wird die Bereitstellung von Software durchgeführt und verwaltet?                                                                                            |
|                              |                                                                       | Können Richtlinien zur Steuerung des Quellcodes oder der Codeintegrität erzwungen werden?                                                                                   |
|                              |                                                                       | Wenn Software bereitstellbar ist, können dann Antischadsoftware, die Verwaltung von Sicherheitsrisiken und Tools zur Überwachung der Sicherheit eingesetzt werden?                                  |
|                              |                                                                       | Stellt der Dienst solche Funktionen nativ bereit? (Beispiel: AKS)                                                                              |
| Identitäts- und Zugriffsverwaltung | Authentifizierung und Zugriffssteuerung                                       | Werden alle Vorgänge auf Steuerungsebene von Azure AD gesteuert? (Gibt es also eine geschachtelte Steuerungsebene wie bei Kubernetes?)                             |
|                              |                                                                       | Welche Methoden sind für den Zugriff auf die Datenebene vorhanden?                                                                                      |
|                              |                                                                       | Kann die Datenebene in Azure AD integriert werden?                                                                                                      |
|                              |                                                                       | Wird bei der Authentifizierung zwischen Azure-Diensten ein MSI/Dienstprinzipal genutzt?                                                         |
|                              |                                                                       | Erfolgt die Authentifizierung zwischen Azure und IaaS (Dienst für virtuelles Netzwerk) über Azure AD?                                                                                   |
|                              |                                                                       | Wie werden in Frage kommende Schlüssel/SAS verwaltet?                                                                                                     |
|                              |                                                                       | Wie kann der Zugriff widerrufen werden?                                                                                                                   |
|                              | Aufgabentrennung                                                 | Trennt der Dienst innerhalb von Azure AD Vorgänge auf Steuerungs- und Datenebene?                                                                |
|                              | Mehrstufige Authentifizierung und bedingter Zugriff                                            | Wird für Interaktionen zwischen Benutzern und Diensten eine mehrstufige Authentifizierung erzwungen?                                                                                            |
| Governance                   | Export und Import von Daten                                                  | Erlaubt der Dienst, Daten sicher und verschlüsselt zu importieren und zu exportieren?                                                                     |
|                              | Datenschutz und -nutzung                                                  | Können Microsoft-Techniker auf die Daten zugreifen?                                                                                                     |
|                              |                                                                       | Wird jede Interaktion des Microsoft-Supports mit dem Dienst überwacht?                                                                               |
|                              | Datenresidenz                                                        | Sind Daten auf die Region der Dienstbereitstellung beschränkt?                                                                                          |
| Operationen (Operations)                   | Überwachung                                                            | Ist der Dienst in Azure Monitor integriert?                                                                                               |
|                              | Sicherungsverwaltung                                                     | Welche Workloaddaten müssen gesichert werden?                                                                                                       |
|                              |                                                                       | Wie werden Sicherungen aufgezeichnet?                                                                                                                    |
|                              |                                                                       | Wie oft können Sicherungen durchgeführt werden?                                                                                                         |
|                              |                                                                       | Wie lange können Sicherungen aufbewahrt werden?                                                                                                        |
|                              |                                                                       | Werden Sicherungen verschlüsselt?                                                                                                                       |
|                              |                                                                       | Erfolgt die Verschlüsselung von Sicherungen mit von Microsoft verwalteten oder vom Kunden verwalteten Schlüsseln?                                                                                             |
|                              | Notfallwiederherstellung                                                     | Wie kann der Dienst regional redundant genutzt werden?                                                                                 |
|                              |                                                                       | Was ist das erreichbare RTO und RPO?                                                                                                          |
|                              | SKU                                                                   | Welche SKUs sind verfügbar? Wie unterscheiden sie sich?                                                                                             |
|                              |                                                                       | Gibt es Features im Zusammenhang mit der Sicherheit für Premium-SKU?                                                                                  |
|                              | Kapazitätsverwaltung                                                   | Wie wird Kapazität überwacht?                                                                                                                   |
|                              |                                                                       | Was ist die Einheit für horizontale Skalierung?                                                                                                        |
|                              | Patch- und Updateverwaltung                                             | Muss der Dienst gepatcht werden oder wird er vom Dienst abstrahiert?                                                                        |
|                              |                                                                       | Wie häufig werden Patches angewendet, und können sie automatisiert werden?                                                                                |
|                              | Audit                                                                 | Werden geschachtelte Vorgänge auf Steuerungsebenen erfasst (z. B. AKS oder Azure Databricks)?                                                                      |
|                              |                                                                       | Werden wichtige Aktivitäten auf Datenebene aufgezeichnet?                                                                                                      |
|                              | Konfigurationsverwaltung                                              | Werden Tags unterstützt und ein `put`-Schema für alle Ressourcen bereitgestellt?                                                                             |
| Compliance von Azure-Diensten     | Dienstnachweis, Zertifizierung und externe Überprüfungen                | Ist der Dienst mit PCI/ISO/SOC konform?                                                                                                        |
|                              | Dienstverfügbarkeit                                                  | In welcher Phase ist der Dienst: private Vorschau/öffentliche Vorschau/allgemeine Verfügbarkeit?                                                                                            |
|                              |                                                                       | In welchen Regionen ist der Dienst verfügbar?                                                                                                    |
|                              |                                                                       | Wie ist das Bereitstellungsmodell des Diensts? (Anders ausgedrückt: handelt es sich um einen regionalen oder globalen Dienst?)                                                      |
|                              | Vereinbarungen zum Servicelevel (Service Level Agreements, SLAs)                                              | Welche SLA gilt für Dienstverfügbarkeit?                                                                                                    |
|                              |                                                                       | Welche SLA gilt für Leistung, sofern zutreffend?                                                                                              |
