---
title: Sicherheitsgovernance und Compliance auf Unternehmensebene
description: Erfahren Sie mehr über Sicherheitsgovernance und Compliance auf Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 4aedbeddc5b8376871f73862ef4121302e2696a1
ms.sourcegitcommit: 34346be9ec66c64d6d7ae24651adbbec1fdbf985
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90534186"
---
# <a name="enterprise-scale-security-governance-and-compliance"></a>Sicherheitsgovernance und Compliance auf Unternehmensebene

Dieser Artikel befasst sich mit der Definition der Begriffe Verschlüsselung, Schlüsselverwaltung, Sicherheitsüberwachung und Auditrichtlinie und mit der Planung der Governance und der Plattformsicherheit. Am Ende des Artikels finden Sie eine Tabelle, in der ein Rahmenwerk beschrieben wird, um die Sicherheitsbereitschaft von Azure-Diensten in Unternehmen zu bewerten.

## <a name="define-encryption-and-key-management"></a>Definieren von Verschlüsselung und Schlüsselverwaltung

Die Verschlüsselung ist ein wichtiger Schritt zur Gewährleistung von Datenschutz, Compliance und Data Residency in Microsoft Azure. Sie ist auch bei vielen Unternehmen einer der wichtigsten Sicherheitsaspekte. In diesem Abschnitt werden Entwurfsaspekte und -empfehlungen in Bezug auf Verschlüsselung und Schlüsselverwaltung behandelt.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

- Für Azure Key Vault geltende Abonnement- und Skalierungsgrenzwerte: Key Vault weist Transaktionsgrenzwerte für Schlüssel und Geheimnisse auf. Informationen zum Drosseln von Transaktionen pro Tresor in einem bestimmten Zeitraum finden Sie unter [Azure-Grenzwerte](/azure/azure-resource-manager/management/azure-subscription-service-limits).

- Key Vault dient als Sicherheitsgrenze, da Zugriffsberechtigungen für Schlüssel, Geheimnisse und Zertifikate auf Tresorebene gelten. Mit Zuweisungen von Schlüsseltresor-Zugriffsrichtlinien können separate Berechtigungen für Schlüssel, Geheimnisse oder Zertifikate gewährt werden. Sie unterstützen keine differenzierten Berechtigungen auf Objektebene, wie z. B. für bestimmte Schlüssel, Geheimnisse oder die [Schlüsselverwaltung für Zertifikate](/azure/security/fundamentals/data-encryption-best-practices).

- Sie können je nach Bedarf anwendungs- und workloadspezifische Geheimnisse und gemeinsam genutzte Schlüssel isolieren ([Zugriffssteuerung](/azure/key-vault/general/best-practices)).

<!-- cSpell:ignore FIPS -->

- Sie können Premium-SKUs optimieren, für die durch Hardwaresicherheitsmodule geschützte Schlüssel erforderlich sind. Die zugrunde liegenden Hardwaresicherheitsmodule (HSMs) sind konform mit FIPS 140-2 Level 2. Verwalten Sie ein dediziertes Azure-HSM für die Compliance mit FIPS 140-2 Level 3 unter Berücksichtigung der unterstützten Szenarios.

- Schlüsselrotation und Ablauf von Geheimnissen.

  - Zertifikatbeschaffung und -signierung mit [Key Vault-Zertifikaten](/azure/key-vault/certificates/about-certificates)
  - Warnungen/Benachrichtigungen und automatisierte Zertifikatverlängerungen

- Anforderungen an die Notfallwiederherstellung für Schlüssel, Zertifikate und Geheimnisse.

  Replikations- und Failoverfunktionen für den Key Vault-Dienst: [Verfügbarkeit und Redundanz](/azure/key-vault/general/disaster-recovery-guidance)

- Überwachen der Nutzung von Schlüsseln, Zertifikaten und Geheimnissen.

  Erkennen von nicht autorisiertem Zugriff mithilfe eines Schlüsseltresors oder Log Analytics-Arbeitsbereichs von Azure Monitor: [Überwachung und Warnung](/azure/key-vault/general/alert)

- Delegierte Key Vault-Instanziierung und privilegierter Zugriff: [sicherer Zugriff](/azure/key-vault/general/secure-your-key-vault)

- Anforderungen für die Nutzung benutzerdefinierter Schlüssel für native Verschlüsselungsmechanismen wie die Azure Storage-Verschlüsselung:
  - [Kundenseitig verwaltete Schlüssel](/azure/storage/common/storage-encryption-keys-portal).
  - Vollständige Datenträgerverschlüsselung für virtuelle Computer (VMs).
  - Verschlüsselung von Daten während der Übertragung.
  - Verschlüsselung ruhender Daten.

### <a name="design-recommendations"></a>Entwurfsempfehlungen

- Nutzen Sie ein Azure Key Vault-Verbundmodell, um Beschränkungen des Transaktionsumfangs zu vermeiden.

- Stellen Sie Azure Key Vault mit Richtlinien für vorläufiges und endgültiges Löschen bereit, damit Aufbewahrungsschutz für gelöschte Objekte aktiviert werden kann.

- Befolgen Sie das Modell der geringsten Berechtigung, indem Sie die Autorisierung zum permanenten Löschen von Schlüsseln, Geheimnissen und Zertifikaten auf spezielle benutzerdefinierte Azure Active Directory-Rollen (Azure AD) beschränken.

- Automatisieren Sie den Prozess zur Verwaltung und Verlängerung von Zertifikaten mit öffentlichen Zertifizierungsstellen, um die Verwaltung zu erleichtern.

- Führen Sie einen automatisierten Prozess für die Rotation von Schlüsseln und Zertifikaten ein.

- Aktivieren Sie den Dienstendpunkt für die Firewall und das virtuelle Netzwerk im Tresor für den Zugriff auf den Schlüsseltresor.

- Verwenden Sie den für die Plattform zentralen Log Analytics-Arbeitsbereich von Azure Monitor, um die Verwendung von Schlüsseln, Zertifikaten und Geheimnissen innerhalb jeder Key Vault-Instanz zu überwachen.

- Delegieren Sie die Instanziierung von Key Vault und den privilegierten Zugriff, und erzwingen Sie mithilfe von Azure Policy eine einheitliche, konforme Konfiguration.

- Greifen Sie bei Bedarf standardmäßig auf von Microsoft verwaltete Schlüssel für die grundlegende Verschlüsselungsfunktionalität zurück, und nutzen Sie bei Bedarf vom Kunden verwaltete Schlüssel.

- Verwenden Sie keine zentralisierten Key Vault-Instanzen für Anwendungsschlüssel oder -geheimnisse.

- Geben Sie keine Key Vault-Instanzen zwischen Anwendungen frei, um die gemeinsame Nutzung von Geheimnissen in verschiedenen Umgebungen zu vermeiden.

## <a name="plan-for-governance"></a>Planen der Governance

Governance stellt Mechanismen und Prozesse zum Beibehalten der Kontrolle über Ihre Anwendungen und Ressourcen in Azure bereit. Azure Policy ist für die Gewährleistung von Sicherheit und Compliance innerhalb der IT-Umgebung von Unternehmen unerlässlich. Der Dienst kann wichtige Verwaltungs- und Sicherheitskonventionen für alle Dienste auf der Azure-Plattform erzwingen und die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) ergänzen, die regelt, welche Aktionen autorisierte Benutzer ausführen dürfen.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

- Bestimmen Sie, welche Azure-Richtlinien erforderlich sind.

- Erzwingung von Verwaltungs- und Sicherheitskonventionen, wie z. B. die Nutzung privater Endpunkte

- Verwalten und erstellen Sie Richtlinienzuweisungen mithilfe von Richtliniendefinitionen, die in mehreren vererbten Zuweisungsbereichen wiederverwendet werden können. Auf Verwaltungsgruppen-, Abonnement- und Ressourcengruppenebene können Sie zentralisierte, grundlegende Richtlinienzuweisungen durchführen.

- Gewährleisten Sie die kontinuierliche Compliance mit Complianceberichten und -auditing.

- Machen Sie sich mit den Grenzen von Azure Policy vertraut, wie z. B. die Beschränkung von Definitionen auf einen beliebigen Umfang: [Richtliniengrenzen](/azure/azure-resource-manager/management/azure-subscription-service-limits).

- Informieren Sie sich über gesetzliche Compliancerichtlinien. Diese können Vorschriften wie Health Insurance Portability and Accountability Act, Payment Card Industry (PCI), Data Security Standards und Service Organizational Control Trust Service-Prinzipien und -Kriterien sein.

### <a name="design-recommendations"></a>Entwurfsempfehlungen

- Bestimmen Sie erforderliche Azure-Tags, und nutzen Sie den Modus zum Anfügen von Richtlinien, um die Nutzung zu erzwingen.

- Ordnen Sie gesetzliche Vorschriften und Complianceanforderungen Azure Policy-Definitionen und Azure AD-RBAC-Zuweisungen zu.

- Legen Sie Azure Policy-Definitionen in der obersten Stammverwaltungsgruppe fest, damit sie in vererbten Bereichen zugewiesen werden können.

- Verwalten Sie Zuweisungen von Richtlinien auf der höchsten geeigneten Ebene mit Ausschlüssen auf unteren Ebenen, sofern erforderlich.

- Nutzen Sie Azure Policy zum Steuern von Registrierungen von Ressourcenanbietern auf Abonnement- und/oder Verwaltungsgruppenebene.

- Nutzen Sie nach Möglichkeit integrierte Richtlinien, um den betrieblichen Aufwand zu minimieren.

- Weisen Sie die in der Richtlinie integrierte Rolle „Mitwirkender“ einem bestimmten Bereich zu, um Governance auf Anwendungsebene zu ermöglichen.

- Beschränken Sie die Anzahl der Azure Policy-Zuweisungen, die im Bereich der Stammverwaltungsgruppe vorgenommen werden, um eine Verwaltung durch Ausschlüsse in vererbten Bereichen zu vermeiden.

## <a name="define-security-monitoring-and-an-audit-policy"></a>Definieren der Sicherheitsüberwachung und einer Überwachungsrichtlinie

Unternehmen benötigen Einblicke in die Vorgänge innerhalb ihres Cloudbestands. Die Sicherheitsüberwachung und Überwachungsprotokollierung der Dienste auf der Azure-Plattform ist eine wesentliche Komponente eines skalierbaren Frameworks.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

- Datenaufbewahrungsdauer für Auditdaten: Azure AD Premium-Berichte werden 30 Tage lang aufbewahrt.

- Langfristige Archivierung von Protokollen wie Azure-Aktivitätsprotokollen, VM- und PaaS-Protokollen (Platform-as-a-Service)

- Grundlegende Sicherheitskonfiguration über eine Azure-Gast-VM-Richtlinie

- Notfallpatches für kritische Sicherheitsrisiken

- Patches für VMs, die über längere Zeiträume offline sind

- Anforderungen für Echtzeitüberwachung und Warnungen

- Integrieren von SIEM-Lösung (Security Information and Event Management) in Azure Security Center und Azure Sentinel

- Beurteilung des Sicherheitsrisikos von VMs

### <a name="design-recommendations"></a>Entwurfsempfehlungen

- Nutzen Sie Azure AD-Berichtsfunktionen zum Generieren von Überwachungsberichten zur Zugriffssteuerung.

- Exportieren Sie Azure-Aktivitätsprotokolle für die langfristige Datenaufbewahrung in Azure Monitor Logs. Exportieren Sie sie in Azure Storage, falls eine langfristige Aufbewahrung von über zwei Jahren erforderlich ist.

- Aktivieren Sie Security Center Standard für alle Abonnements, und verwenden Sie Azure Policy, um die Compliance sicherzustellen.

- Überwachen Sie Abweichungen bei Patches des Basisbetriebssystems mittels Azure Monitor Logs und Azure Security Center.

- Nutzen Sie Azure-Richtlinien zur automatischen Bereitstellung von Softwarekonfigurationen mithilfe von VM-Erweiterungen und zur Erzwingung einer konformen VM-Basiskonfiguration.

- Überwachen Sie Abweichungen bei der VM-Sicherheitskonfiguration mittels Azure Policy.

- Verbinden Sie Standardressourcenkonfigurationen mit einem zentralen Log Analytics-Arbeitsbereich von Azure Monitor.

- Verwenden Sie eine Azure Event Grid-basierte Lösung für protokollorientierte Echtzeitwarnungen.

## <a name="plan-for-platform-security"></a>Planen der Plattformsicherheit

Sie müssen einen stabile Sicherheitsstatus aufrechterhalten, wenn Sie Azure einführen. Neben Sichtbarkeit müssen Sie in der Lage sein, die anfänglichen Einstellungen und Änderungen zu bestimmen, während sich die Azure-Dienste weiterentwickeln. Daher ist die Planung der Plattformsicherheit von großer Bedeutung.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

- Geteilte Verantwortung

- Hochverfügbarkeit und Notfallwiederherstellung

- Einheitliche Sicherheit in allen Azure-Diensten in Bezug auf Datenverwaltungs- und Steuerungsebenenvorgänge

- Mehrinstanzenfähigkeit für wichtige Plattformkomponenten (Hyper-V, die Key Vault zugrunde liegenden HSMs sowie Datenbank-Engines)

### <a name="design-recommendations"></a>Entwurfsempfehlungen

- Führen Sie im Kontext ihrer zugrunde liegenden Anforderungen eine gemeinsame Untersuchung der erforderlichen Dienste durch. Wenn Sie Ihre eigenen Schlüssel einsetzen möchte, wird dies möglicherweise nicht von allen in Frage kommenden Diensten unterstützt. Implementieren Sie eine geeignete Risikominderung, damit Inkonsistenzen die gewünschten Ergebnisse nicht beeinträchtigen. Wählen Sie geeignete Regionspaare und Regionen für die Notfallwiederherstellung, die Latenz minimieren.

- Entwickeln Sie einen Plan zum Erstellen einer Zulassungsliste für die Sicherheit, um die Sicherheitskonfiguration, Überwachung und Warnungen von Diensten sowie deren Integration in bestehende Systeme zu beurteilen.

- Legen Sie vor dem Erstellen einer Zulassungsliste für Azure-Dienste einen Incident-Response-Plan fest.

- Nutzen Sie Azure AD-Berichtsfunktionen zum Generieren von Überwachungsberichten zur Zugriffssteuerung.

- Stimmen Sie Ihre Sicherheitsanforderungen mit Roadmaps für die Azure-Plattform ab, damit immer die neu veröffentlichten Sicherheitskontrollen verwendet werden.

- Setzen Sie ggf. einen Zero-Trust-Ansatz für den Zugriff auf die Azure-Plattform um.

<!-- docsTest:ignore "and conditional access" -->

## <a name="azure-security-benchmarks"></a>Vergleichstests für die Azure-Sicherheit

Der Azure Security-Vergleichstest enthält eine Sammlung von wirkungsvollen Sicherheitsempfehlungen, mit denen Sie den Großteil der von Ihnen in Azure genutzten Dienste sichern können. Sie können diese Empfehlungen als „allgemein“ oder „organisatorisch“ betrachten, da sie auf die meisten Azure-Dienste anwendbar sind. Die Empfehlungen des Azure Security-Vergleichstest werden anschließend für jeden Azure-Service angepasst. Diese individuelle Anleitung ist dann in den Artikeln über die Dienstempfehlungen enthalten.

In der Dokumentation zum Azure Security-Vergleichstest werden Sicherheitskontrollen und Dienstempfehlungen angegeben.

- [Sicherheitskontrollelement](https://docs.microsoft.com/azure/security/benchmarks/overview): Die Empfehlungen des Azure Security-Vergleichstests werden nach Sicherheitskontrollelementen kategorisiert. Sicherheitskontrollelemente stellen von Anbietern unabhängige allgemeine Sicherheitsanforderungen dar, wie z. B. Netzwerksicherheit und Datenschutz. Jedes Sicherheitskontrollelement enthält eine Reihe von Sicherheitsempfehlungen und Anweisungen, mit denen Sie diese Empfehlungen implementieren können.
- [Sicherheitsempfehlungen](https://docs.microsoft.com/azure/security/benchmarks/security-baselines-overview): Wenn verfügbar, enthalten die Empfehlungen des Vergleichstests für Azure-Dienste auch Empfehlungen des Azure Security-Vergleichstests, die speziell auf diesen Dienst zugeschnitten sind.

## <a name="service-enablement-framework"></a>Dienstaktivierungsframework

Wenn Geschäftsbereiche die Bereitstellung von Workloads in Azure anfordern, ist ein zusätzlicher Einblick in eine Workload erforderlich, um zu bestimmen, wie ein angemessenes Maß an Governance, Sicherheit und Compliance erreicht werden kann. Wenn ein neuer Dienst erforderlich ist, müssen Sie diesen genehmigen. Die folgende Tabelle bietet ein Framework zur Beurteilung der Sicherheitsbereitschaft von Azure-Diensten in Unternehmen:

| Bewertung                    | Category                                                              | Kriterien                                                                                                                                     |
|------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Sicherheit                     | Netzwerkendpunkt                                                      | Verfügt der Dienst über einen öffentlichen Endpunkt, der außerhalb eines virtuellen Netzwerks zugänglich ist?                                                                |
|                              |                                                                       | Werden Endpunkte virtueller Netzwerkdienste unterstützt?                                                                                                      |
|                              |                                                                       | Können Azure-Dienste direkt mit dem Dienstendpunkt interagieren?                                                                              |
|                              |                                                                       | Werden Azure Private Link-Endpunkte unterstützt?                                                                                                           |
|                              |                                                                       | Ist eine Bereitstellung in einem virtuellen Netzwerk möglich?                                                                                                            |
|                              | Verhinderung der Datenexfiltration                                          | Verfügt der PaaS-Dienst im Azure ExpressRoute-Microsoft-Peering über eine separate BGP-Community (Border Gateway Protocol)? Macht ExpressRoute einen Routenfilter für den Dienst verfügbar? |
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
|                              |                                                                       | Wenn Software bereitstellbar ist, können dann Antischadsoftware-Funktionen, die Verwaltung von Sicherheitsrisiken und Tools zur Überwachung der Sicherheit eingesetzt werden?                                  |
|                              |                                                                       | Bietet der Dienst diese Funktionen nativ (z. B. über Azure Kubernetes Service)?                                                                              |
| Identitäts- und Zugriffsverwaltung | Authentifizierung und Zugriffssteuerung                                       | Werden alle Vorgänge auf Steuerungsebene von Azure AD gesteuert? Gibt es eine geschachtelte Steuerungsebene wie bei Azure Kubernetes Service?                             |
|                              |                                                                       | Welche Methoden sind für den Zugriff auf die Datenebene vorhanden?                                                                                      |
|                              |                                                                       | Kann die Datenebene in Azure AD integriert werden?                                                                                                      |
|                              |                                                                       | Wird bei der Authentifizierung zwischen Azure-Diensten ein MSI/Dienstprinzipal genutzt?                                                         |
|                              |                                                                       | Erfolgt die Authentifizierung zwischen Azure und IaaS (vom Dienst zum virtuellen Netzwerk) über Azure AD?                                                                                   |
|                              |                                                                       | Wie werden anwendbare Schlüssel oder Shared Access Signatures verwaltet?                                                                                                     |
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
|                              |                                                                       | Erfolgt die Sicherungsverschlüsselung mit von Microsoft verwalteten oder kundenseitig verwalteten Schlüsseln?                                                                                             |
|                              | Notfallwiederherstellung                                                     | Wie kann der Dienst regional redundant genutzt werden?                                                                                 |
|                              |                                                                       | Wie lauten das erreichbare Recovery Time Objective und Recovery Point Objective?                                                                                                          |
|                              | SKU                                                                   | Welche SKUs sind verfügbar? Wie unterscheiden sie sich?                                                                                             |
|                              |                                                                       | Gibt es Features im Zusammenhang mit der Sicherheit für Premium-SKU?                                                                                  |
|                              | Kapazitätsverwaltung                                                   | Wie wird Kapazität überwacht?                                                                                                                   |
|                              |                                                                       | Was ist die Einheit für horizontale Skalierung?                                                                                                        |
|                              | Patch- und Updateverwaltung                                             | Muss der Dienst manuell aktualisiert werden, oder erfolgen Updates automatisch?                                                                        |
|                              |                                                                       | Wie häufig werden Updates angewendet? Können sie automatisiert werden?                                                                                |
|                              | Audit                                                                 | Werden Vorgänge in der geschachtelten Steuerungsebene erfasst (z. B. in Azure Kubernetes Service oder Azure Databricks)?                                                                      |
|                              |                                                                       | Werden wichtige Aktivitäten auf Datenebene aufgezeichnet?                                                                                                      |
|                              | Konfigurationsverwaltung                                              | Werden Tags unterstützt und ein `put`-Schema für alle Ressourcen bereitgestellt?                                                                             |
| Compliance von Azure-Diensten     | Dienstnachweis, Zertifizierung und externe Überprüfungen                | Ist der Dienst mit PCI/ISO/SOC konform?                                                                                                        |
|                              | Dienstverfügbarkeit                                                  | Befindet sich der Dienst in der privaten oder öffentlichen Vorschauversion, oder ist er allgemein verfügbar?                                                                                            |
|                              |                                                                       | In welchen Regionen ist der Dienst verfügbar?                                                                                                    |
|                              |                                                                       | Wie ist das Bereitstellungsmodell des Diensts? Handelt es sich um einen regionalen oder um einen globalen Dienst?                                                      |
|                              | Vereinbarungen zum Servicelevel (Service Level Agreements, SLAs)                                              | Welche SLA gilt für Dienstverfügbarkeit?                                                                                                    |
|                              |                                                                       | Welche SLA gilt für Leistung, sofern zutreffend?                                                                                              |
