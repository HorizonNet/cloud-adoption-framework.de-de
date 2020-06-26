---
title: Implementierungsrichtlinien
description: Implementierungsrichtlinien.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 124fbd45892f7d9e6b410de304d3843a418c9b0d
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85076886"
---
<!-- cSpell:ignore interdomain VMSS -->

# <a name="implementation-guidelines"></a>Implementierungsrichtlinien

Dieser Abschnitt erleichtert Ihnen den Einstieg in die Arbeit mit der plattformnativen Referenzimplementierung auf Unternehmensebene. Außerdem werden Entwurfsziele, aktueller Entwurf, häufig gestellte Fragen und bekannte Probleme erläutert.

Es müssen zwei Gruppen von Aktivitäten ausgeführt werden, um die Architektur auf Unternehmensebene zu implementieren. Die erste Gruppe bezieht sich auf die Unternehmensebene. Sie umfasst Aktivitäten, die von den Azure Active Directory-Administratoren ausgeführt werden müssen, um eine anfängliche Konfiguration einzurichten. Diese sind von Natur aus sequenziell, und es handelt sich hauptsächlich um einmalige Aktivitäten. Zur zweiten Gruppe zählen **Datei** > **Neu** > **Region** und **Datei** > **Neu** > **Zielzone**. Dabei handelt es sich um wiederkehrende Aktivitäten, die zum Instanziieren einer Zielzone erforderlich sind, und sie benötigen Benutzereingaben, um den Workflow zu starten, mit dem die Ressourcenerstellung in Azure AD koordiniert werden. Um eine Operationalisierung im großen Stil vorzunehmen, müssen diese Aktivitäten dem Prinzip von _Infrastructure-as-Code (IaC)_ und der Automatisierung mit Bereitstellungspipelines folgen.

Einige der Tabellen unten enthalten leere Spalten. In diesen Spalten können Sie Werte und Notizen eingeben, die spezifisch für Ihre Umgebung sind.

## <a name="what-must-be-true-for-an-enterprise-scale-landing-zone"></a>Zu erfüllende Voraussetzungen für eine Zielzone auf Unternehmensebene

### <a name="enterprise-agreement-ea-enrollment-and-azure-ad-tenants"></a>Enterprise Agreement-Registrierung (EA) und Azure AD-Mandanten

| activities | Erforderliche Parameter | Beispielkonfiguration für Unternehmensebene |
|---|---|---|
| 1. Richten Sie den EA-Administrator und das Benachrichtigungskonto ein. | | |
| 2. Erstellen Sie Abteilungen/Geschäftsdomänen/geobasierte/Organisationshierarchie. | | |
| 3. Erstellen Sie ein EA-Konto, und weisen Sie das Budget zu. | | |
| 4. Richten Sie Azure AD Connect für jeden Azure AD-Mandanten ein, wenn die Identität von einem lokalen Standort aus synchronisiert werden soll. | | |
| 5. Richten Sie keinen ständigen Zugriff auf Azure-Ressourcen und Just-in-Time-Zugriff über Azure AD Privileged Identity Management (PIM) ein. | | |

### <a name="management-group-and-subscription"></a>Verwaltungsgruppe und Abonnement

| activities | Erforderliche Parameter | Beispielkonfiguration für Unternehmensebene |
|---|---|---|
| 1. Erstellen Sie eine Verwaltungsgruppenhierarchie (idealerweise mit höchstens drei oder vier Ebenen). | | |
| 2. Erstellen Sie eine Sandbox-Verwaltungsgruppe der obersten Ebene, um Benutzern das Experimentieren mit Azure zu ermöglichen. | | |
| 3. Veröffentlichen Sie ein Abonnementbereitstellungskriterium zusammen mit den Zuständigkeiten eines Abonnementbesitzers (möglicherweise als Wiki). | | |
| 4. Erstellen Sie Verwaltungs- und Konnektivitätsabonnements für Plattformverwaltung und globale Netzwerk- und Konnektivitätsressourcen. | | |
| 5. Richten Sie ein Git-Repository und einen Dienstprinzipal für die Verwendung mit einer CI/CD-Pipeline der Plattform. | | |
| 6. Erstellen Sie benutzerdefinierte Rollendefinitionen, und verwalten Sie Berechtigungen mithilfe von Azure AD Privileged Identity Management für Abonnement- und Verwaltungsgruppenbereiche. | | |

### <a name="global-networking-and-connectivity"></a>Globale Netzwerke und Konnektivität

<!-- markdownlint-disable MD033 -->
<!-- cSpell:ignore vwan vhub -->
<!-- docsTest:ignore "Standard virtual WAN" -->

| activities | Erforderliche Parameter | Beispielkonfiguration für Unternehmensebene |
|---|---|---|
| 1. Weisen Sie für jede Azure-Region, in der virtuelle Azure Virtual WAN-Hubs und virtuelle Netzwerke bereitgestellt werden, einen entsprechenden CIDR-Bereich (klassenloses domänenübergreifendes Routing) für virtuelle Netzwerke zu. | Ein CIDR-Bereich pro Region | Europa, Norden: `10.0.0.0/16` <br> Europa, Westen: `10.1.0.0/16` <br> USA, Osten: `10.2.0.0/16` |
| 2. Erstellen Sie ein standardmäßiges virtuelles WAN im Konnektivitätsabonnement. | Name des virtuellen WAN <br> Azure-Region | Name des virtuellen WAN: `contoso-vwan` <br> Azure-Region: `North Europe` |
| 3. Erstellen Sie einen virtuellen Hub für jede Region. Stellen Sie sicher, dass mindestens ein Gateway (ExpressRoute oder VPN) pro virtuellen Hub bereitgestellt wird. | Name des virtuellen WAN <br> Name des virtuellen Hubs <br> Region des virtuellen Hubs <br> Adressraum des virtuellen Hubs <br> ExpressRoute-Gateway <br> VPN-Gateway | Virtuelles WAN: `contoso-vwan` <br> Region des virtuellen Hubs: `North Europe` <br> Name des virtuellen Hubs: `vhub-neu` <br> Adressraum des virtuellen Hubs: `10.0.0.0/16` <br> ExpressRoute-Gateway: ja (1 Skalierungseinheit) <br> VPN-Gateway: nein |
| 4. Sichern Sie virtuelle Hubs mit Azure Firewall Manager, indem Sie Azure Firewall in jedem virtuellen Hub bereitstellen.                                                        | Name des virtuellen Hubs                           | Name des virtuellen Hubs: `vhub-neu`                       |
| 5. Erstellen Sie erforderliche Firewallrichtlinien im Konnektivitätsabonnement, und weisen Sie diese sicheren virtuellen Hubs zu.                                                 | Name der Azure Firewall-Richtlinie <br> Eingangs-/Ausgangsregeln von Firewallrichtlinien | Name der Firewallrichtlinie: `contoso-global-fw-policy` <br> Ausgangsregeln zulassen für `*.microsoft.com`  |
| 6. Stellen Sie mithilfe von Azure Firewall Manager sicher, dass alle mit einem sicheren virtuellen Hub verbundenen virtuellen Netzwerke durch die Azure Firewall geschützt sind.                                                | Name des virtuellen Hubs <br> Internetdatenverkehr – Datenverkehr von virtuellen Netzwerken | Name des virtuellen Hubs: `vhub-neu` <br> Internetdatenverkehr – Datenverkehr von virtuellen Netzwerken – über Azure Firewall senden |
| 7. Stellen Sie eine Zone mit privatem Azure-DNS im globalen Konnektivitätsabonnement bereit, und konfigurieren Sie sie.                                                             | Name der privaten DNS-Zone               | Name der privaten DNS-Zone: `azure.contoso.com` |
| 8. Stellen Sie ExpressRoute-Leitungen mit privatem Peering bereit.                                                                                                 | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private) | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private) |
| 9. Verbinden Sie lokale HQs/DCs über ExpressRoute-Leitungen mit Azure Virtual Hub.                                                                                | Autorisierungsschlüssel <br> Name des virtuellen Hubs | Autorisierungsschlüssel: `xxxxxxxx` <br> Virtueller Hub: `vhub-neu` |
| 10. (Optional): Richten Sie Verschlüsselung über privates ExpressRoute-Peering ein.                                                                                         | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/virtual-wan/vpn-over-expressroute) | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/virtual-wan/vpn-over-expressroute) |
| 11. (Optional): Verbinden Sie Branches über VPN mit dem virtuellen Hub.                                                                                                | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-site-to-site-portal) | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-site-to-site-portal) |
| 12. Schützen Sie den mithilfe von NSGs Datenverkehr aus dem virtuellen Netzwerk über virtuelle Hubs hinweg.                                                                                                             | Eingangsregeln <br> Ausgangsregeln | Eingangsregeln <br> Ausgangsregeln |
| 13. Konfigurieren Sie ExpressRoute Global Reach für das Herstellen von Verbindungen mit lokalen HQs/DCs, wenn mehrere lokale Standorte über ExpressRoute mit Azure verbunden sind. | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/expressroute/expressroute-howto-set-global-reach) | [Anweisungen befolgen gemäß Artikel](https://docs.microsoft.com/azure/expressroute/expressroute-howto-set-global-reach) |

<!-- markdownlint-enable MD033 -->

### <a name="security-governance-and-compliance"></a>Sicherheit, Governance und Compliance

| activities | Erforderliche Parameter | Beispielkonfiguration für Unternehmensebene |
|---|---|---|
| 1. Definieren und wenden Sie ein Dienstwhitelists-Framework an, um sicherzustellen, dass Azure-Dienste die Anforderungen an Unternehmenssicherheit und -governance erfüllen (siehe Anhang). | | |
| 2. Erstellen Sie benutzerdefinierte Rollendefinitionen für die rollenbasierte Zugriffssteuerung (RBAC). | | |
| 3. Aktivieren Sie PIM, und ermitteln Sie Azure-Ressourcen, um PIM zu erleichtern. | | |
| 4. Erstellen Sie auf Azure AD beschränkte Gruppen für die Azure-Steuerungsebenenverwaltung von Ressourcen mit PIM. | | |
| 5. Wenden Sie Azure Policy an, um sicherzustellen, dass Azure-Dienste den Unternehmensanforderungen entsprechen. | | |
| 6. Definieren Sie eine Benennungskonvention, und erzwingen Sie sie über Azure Policy. | | |
| 7. Erstellen Sie eine Richtlinienmatrix in allen Bereichen (aktivieren Sie z. B. die Überwachung für alle Azure-Dienste). | | |
| 8. Wenden Sie Azure-Richtlinien in Bezug auf Netzwerk, Sicherheit und Überwachung an (siehe Liste unten mit Beispielrichtlinien). | | |

### <a name="platform-management-and-monitoring"></a>Plattformverwaltung und -überwachung

| activities | Erforderliche Parameter | Beispielkonfiguration für Unternehmensebene |
|---|---|---|
| 1. Erstellen Sie Dashboards für Richtlinien-Compliance und Sicherheit, um organisations- und ressourcenbezogene Ansichten zu erhalten. | | |
| 2. Erstellen Sie einen Workflow für Plattformgeheimnisse (Dienstprinzipale und Automation-Konto) und Schlüsselrollover. | | |
| 3. (Optional:) Richten Sie ein organisationsweites VM-Katalogimage ein. | | |
| 4. Richten Sie die langfristige Archivierung und Aufbewahrung von Protokollen in Azure Monitor-Protokollen ein. | | |
| 5. Richten Sie Business Continuity & Disaster Recovery für Schlüsseltresore ein, in denen Plattformgeheimnisse gespeichert werden | | |
| 6. Stellen Sie mithilfe von Azure Firewall Manager sicher, dass alle mit einem sicheren virtuellen Hub verbundenen virtuellen Netzwerke durch die Azure Firewall geschützt sind. | | |

In der Tabelle unten sind Azure-Beispielrichtlinien zum Erzwingen typischer Netzwerk-, Sicherheits- und Überwachungskontrollen im Verwaltungsgruppenbereich aufgelistet.

| Kategorie   | Richtlinie | |------------|--------------------------------------------------------------------------------------------------_| | Netzwerk    | 1. (Vorschau:) Container Registry sollte einen VNET-Dienstendpunkt verwenden.                   | |            | 2. Eine benutzerdefinierte Richtlinie für IPSec/Internetschlüsselaustausch (IKE) muss auf alle Gatewayverbindungen in virtuellen Azure-Netzwerken angewendet werden. | |            | 3. App Service sollte einen VNET-Dienstendpunkt verwenden (nur interne Apps).                | |            | 4. Azure-VPN-Gateways dürfen keine SKU verwenden.                            | |            | 5. Azure Cosmos DB sollte einen VNET-Dienstendpunkt verwenden.                                 | |            | 6. Beim Erstellen virtueller Netzwerke Network Watcher bereitstellen.                                      | |            | 7. Event Hub sollte einen VNET-Dienstendpunkt verwenden.                                       | |            | 8. Gatewaysubnetze dürfen nicht mit einer Netzwerksicherheitsgruppe konfiguriert werden.                        | |            | 9. Key Vault sollte einen VNET-Dienstendpunkt verwenden.                                       | |            | 10. Netzwerkschnittstellen müssen die IP-Weiterleitung deaktivieren.                                              | |            | 11. Service Bus sollte einen VNET-Dienstendpunkt verwenden.                                    | |            | 12. SQL Server sollte einen VNET-Dienstendpunkt verwenden.                                     | |            | 13. Speicherkonten sollten einen VNET-Dienstendpunkt verwenden.                               | |            | 14. Subnetze sollten einer Netzwerksicherheitsgruppe zugeordnet werden.                                   | |            | 15. Nicht geschützte Netzwerkendpunkte in Azure Security Center überwachen.                          | | Sicherheit   | 1. [Vorschau]: Bereitstellung von Microsoft Monitoring Agent überwachen – VM-Image (Betriebssystem) nicht aufgelistet.                         | |            | 2. [Vorschau]: Bereitstellung von Microsoft Monitoring Agent in VMSS überwachen – VM-Image (Betriebssystem) nicht aufgelistet.                 | |            | 3. [Vorschau]: Bereitstellung des Azure Monitor Log Analytics-Agents überwachen – VM-Image (Betriebssystem) nicht aufgelistet.                      | |            | 4. [Vorschau]: Bereitstellung des Azure Monitor Log Analytics-Agents in VMSS überwachen – VM-Image (Betriebssystem) nicht aufgelistet.              | |            | 5. [Vorschau]: Azure Monitor Log Analytics-Arbeitsbereich für VM überwachen – Berichtskonflikt.                             | |            | 6. [Vorschau]: Bereitstellen des Microsoft Dependency-Agents für Linux-VMs.                                              | |            | 7. [Vorschau]: Bereitstellen des Microsoft Dependency-Agents für Windows-VMs.                                            | |            | 8. [Vorschau]: Azure Monitor Log Analytics-Agent für Linux-VMs bereitstellen.                                           | |            | 9. [Vorschau]: Azure Monitor Log Analytics-Agent für Windows-VMs bereitstellen.                                         | |            | 10. Das Aktivitätsprotokoll muss mindestens ein Jahr lang aufbewahrt werden.                                        | |            | 11. Überwachen der Diagnoseeinstellung.                                                                     | |            | 12. Das Azure Monitor-Protokollprofil muss Protokolle für die Kategorien `write`, `delete` und `action` erfassen. | |            | 13. Azure Monitor muss Aktivitätsprotokolle aus allen Regionen erfassen.                                  | |            | 14. Azure Monitor-Lösung „Sicherheit und Überwachung“ muss bereitgestellt werden.                                 | |            | 15. Azure-Abonnements benötigen ein Protokollprofil für das Aktivitätsprotokoll.                               | |            | 16. Diagnoseeinstellungen für Batch-Konto in Event Hub bereitstellen,                                    | |            | 17. Diagnoseeinstellungen für Batch-Konto in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                      | |            | 18. Diagnoseeinstellungen für Data Lake Analytics in Event Hub bereitstellen.                              | |            | 19. Diagnoseeinstellungen für Data Lake Analytics in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                | |            | 20. Diagnoseeinstellungen für Data Lake Storage gen1 in Event Hub bereitstellen.                           | |            | 21. Diagnoseeinstellungen für Data Lake Storage gen1 in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.             | |            | 22. Diagnoseeinstellungen für Event Hub in Event Hub bereitstellen.                                        | |            | 23. Diagnoseeinstellungen für Event Hub in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                          | |            | 24. Diagnoseeinstellungen für Key Vault in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                          | |            | 25. Diagnoseeinstellungen für Logic Apps in Event Hub bereitstellen.                                       | |            | 26. Diagnoseeinstellungen für Logic Apps in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                         | |            | 27. Diagnoseeinstellungen für Netzwerksicherheitsgruppen bereitstellen.                                       | |            | 28. Diagnoseeinstellungen für Suchdienste in Event Hub bereitstellen.                                  | |            | 29. Diagnoseeinstellungen für Suchdienste in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                    | |            | 30. Diagnoseeinstellungen für Service Bus in Event Hub bereitstellen.                                      | |            | 31. Diagnoseeinstellungen für Service Bus in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                        | |            | 32. Diagnoseeinstellungen für Stream Analytics in Event Hub bereitstellen.                                 | |            | 33. Diagnoseeinstellungen für Stream Analytics in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                   | |            | 34. Der Azure Monitor Log Analytics-Agent sollte in VM-Skalierungsgruppen installiert werden.                    | |            | 35. Der Azure Monitor Log Analytics-Agent sollte auf VMs installiert werden.                              | | Überwachung | 36. [Vorschau]: Bereitstellung von Microsoft Dependency-Agent überwachen – VM-Image (Betriebssystem) nicht aufgelistet.                        | |            | 37. [Vorschau]: Bereitstellung von Microsoft Dependency-Agent in VMSS überwachen – VM-Image (Betriebssystem) nicht aufgelistet.                | |            | 38. [Vorschau]: Bereitstellung des Azure Monitor Log Analytics-Agents überwachen – VM-Image (Betriebssystem) nicht aufgelistet.                     | |            | 39. [Vorschau]: Bereitstellung des Azure Monitor Log Analytics-Agents in VMSS überwachen – VM-Image (Betriebssystem) nicht aufgelistet.             | |            | 40. [Vorschau]: Azure Monitor Log Analytics-Arbeitsbereich für VM überwachen – Berichtskonflikt.                            | |            | 41. [Vorschau]: Bereitstellen des Microsoft Dependency-Agents für Linux-VMs.                                             | |            | 42. [Vorschau]: Bereitstellen des Microsoft Dependency-Agents für Windows-VMs.                                           | |            | 43. [Vorschau]: Azure Monitor Log Analytics-Agent für Linux-VMs bereitstellen.                                          | |            | 44. [Vorschau]: Azure Monitor Log Analytics-Agent für Windows-VMs bereitstellen.                                        | |            | 45. Das Aktivitätsprotokoll muss mindestens ein Jahr lang aufbewahrt werden.                                        | |            | 46. Überwachen der Diagnoseeinstellung.                                                                     | |            | 47. Das Azure Monitor-Protokollprofil muss Protokolle für die Kategorien `write`, `delete` und `action` erfassen. | |            | 48. Azure Monitor muss Aktivitätsprotokolle aus allen Regionen erfassen.                                  | |            | 49. Azure Monitor-Lösung `security and audit` muss bereitgestellt werden.                                 | |            | 50. Azure-Abonnements benötigen ein Protokollprofil für das Aktivitätsprotokoll.                               | |            | 51. Diagnoseeinstellungen für Batch-Konto in Event Hub bereitstellen,                                    | |            | 52. Diagnoseeinstellungen für Batch-Konto in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                      | |            | 53. Diagnoseeinstellungen für Data Lake Analytics in Event Hub bereitstellen.                              | |            | 54. Diagnoseeinstellungen für Data Lake Analytics in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                | |            | 55. Diagnoseeinstellungen für Data Lake Storage gen1 in Event Hub bereitstellen.                           | |            | 56. Diagnoseeinstellungen für Data Lake Storage gen1 in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.             | |            | 57. Diagnoseeinstellungen für Event Hub in Event Hub bereitstellen.                                        | |            | 58. Diagnoseeinstellungen für Event Hub in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                          | |            | 59. Diagnoseeinstellungen für Key Vault in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                          | |            | 60. Diagnoseeinstellungen für Logic Apps in Event Hub bereitstellen.                                       | |            | 61. Diagnoseeinstellungen für Logic Apps in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                         | |            | 62. Diagnoseeinstellungen für Netzwerksicherheitsgruppen bereitstellen.                                       | |            | 63. Diagnoseeinstellungen für Suchdienste in Event Hub bereitstellen.                                  | |            | 64. Diagnoseeinstellungen für Suchdienste in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                    | |            | 65. Diagnoseeinstellungen für Service Bus in Event Hub bereitstellen.                                      | |            | 66. Diagnoseeinstellungen für Service Bus in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                        | |            | 67. Diagnoseeinstellungen für Stream Analytics in Event Hub bereitstellen.                                 | |            | 68. Diagnoseeinstellungen für Stream Analytics in Azure Monitor Log Analytics-Arbeitsbereich bereitstellen.                   | |            | 69. Der Azure Monitor Log Analytics-Agent sollte in VM-Skalierungsgruppen installiert werden.                    | |            | 70. Der Azure Monitor Log Analytics-Agent sollte auf VMs installiert werden.                              | | Key Vault  | 71. [Vorschau]: Zulässige Zertifikatschlüsseltypen verwalten.                                              | |            | 72. [Vorschau]: Zulässige Kurvennamen für ECC-Zertifikate (Kryptografie für elliptische Kurve) verwalten.           | |            | 73. [Vorschau]: Aktionstrigger für Zertifikatlebensdauer verwalten.                                       | |            | 74. [Vorschau]: Gültigkeitsdauer von Zertifikaten verwalten.                                                | |            | 75. [Vorschau]: Durch nicht integrierte Zertifizierungsstelle ausgestellte Zertifikate verwalten.                                 | |            | 76. [Vorschau]: Durch integrierte Zertifizierungsstelle ausgestellte Zertifikate verwalten.                                    | |            | 77. [Vorschau]: Zertifikate verwalten, die innerhalb einer angegebenen Anzahl von Tagen ablaufen.      | |            | 78. [Vorschau]: Mindestschlüsselgröße für RSA-Zertifikate verwalten.                                      | |            | 79. Bereitstellen von Diagnoseeinstellungen für Key Vault in Event Hub.                                        | |            | 80. In Key Vault müssen Diagnoseprotokolle aktiviert sein.                                               | |            | 81. Aktivieren von „Vorläufiges Löschen“ für Key Vault.                                                             |

## <a name="file--gt-new--gt-region-and-file--gt-new--gt-landing-zone"></a>**Datei -&gt; Neu -&gt; Region** und **Datei -&gt; Neu -&gt; Zielzone**

### <a name="file--gt-new--gt-region"></a>Datei -&gt; Neu -&gt; Region

1. Erstellen Sie innerhalb des Konnektivitätsabonnements einen neuen virtuellen Hub im vorhandenen Azure Virtual WAN.

2. Sichern Sie den virtuellen Hub mit Azure Firewall Manager, indem Sie eine Azure Firewall im virtuellen Hub bereitstellen und vorhandene oder neue Firewallrichtlinien mit Azure Firewall verknüpfen.

3. Stellen Sie mithilfe von Azure Firewall Manager sicher, dass alle mit einem sicheren virtuellen Hub verbundenen virtuellen Netzwerke durch die Azure Firewall geschützt sind.

4. Verbinden Sie den virtuellen Hub mithilfe von ExpressRoute oder über ein VPN mit dem lokalen Standort.

5. (Optional:) Richten Sie Verschlüsselung über privates ExpressRoute-Peering ein.

6. Schützen Sie Datenverkehr aus virtuellen Netzwerken über virtuelle Hubs hinweg mit Netzwerksicherheitsgruppen.

### <a name="file--gt-new--gt-landing-zone-for-applications-and-workloads"></a>Datei -&gt; Neu -&gt; Zielzone für Anwendungen und Workloads

1. Erstellen Sie ein Abonnement, und weisen Sie die anfordernde Person als Abonnementbesitzer zu.

2. Weisen Sie das Abonnement innerhalb der Verwaltungsgruppenhierarchie zu.

3. Legen Sie ein Budget und Warnbenachrichtigungen fest.

4. Richten Sie eine E-Mail-Adresse und Telefonnummer für den Sicherheitsansprechpartner ein.

5. Erstellen Sie Azure AD-Gruppen für Abonnementbesitzer, Leser, Mitwirkenden und weitere.

6. Erstellen Sie Azure AD PIM-Berechtigungen für eingerichtete Azure AD-Gruppen.

7. Stellen Sie den CIDR-Bereich für das virtuelle Netzwerk bereit, wenn virtuelle Netzwerkverbindungen erforderlich sind.

8. Führen Sie ein Peering des virtuellen Netzwerks mit dem regionalen virtuellen Hub aus.

9. Stellen Sie erforderliche gemeinsam genutzte Dienste bereit (z. B. Domänencontroller).

10. Weisen Sie erforderliche Richtlinien für den Abonnementbereich gemäß der von der Organisation definierten Richtlinienmatrix zu.

\* Optional für Sandboxabonnements.

In der Tabelle unten finden Sie eine Liste von Azure-Beispielrichtlinien, mit denen typische Unternehmenskontrollen im Abonnementbereich erzwungen werden.

| Category          | Richtlinie                                                                                                 |
|-------------------|--------------------------------------------------------------------------------------------------------|
| Ressource und Tags | 1. Allowed locations (Zulässige Speicherorte)                                                                                   |
|                   | 2. Zulässige Speicherorte für Ressourcengruppen                                                               |
|                   | 3. Zulässige Ressourcentypen                                                                              |
|                   | 4. Verwendung benutzerdefinierter RBAC-Regeln überwachen                                                                    |
|                   | 5. Es dürfen keine benutzerdefinierten Abonnementbesitzerrollen vorhanden sein.                                                    |
|                   | 6. Not allowed resource types (Unzulässige Ressourcentypen)                                                                          |
|                   | 7. Tag zu Ressourcengruppen hinzufügen                                                                        |
|                   | 8. Tag zu Ressourcen hinzufügen                                                                              |
|                   | 9. Tag von der Ressourcengruppe erben, falls nicht vorhanden                                                    |
|                   | 10. Tag und zugehörigen Wert erzwingen                                                                          |
|                   | 11. Tag und zugehörigen Wert für Ressourcengruppen erzwingen                                                       |
| Compute           | 12. Zulässige VM-SKUs                                                                       |
|                   | 13. VMs überwachen, für die keine Notfallwiederherstellung konfiguriert ist                                        |
|                   | 14. Virtuelle Computer überwachen, die keine verwalteten Datenträger verwenden                                                            |
|                   | 15. Bereitstellen der standardmäßigen Microsoft IaaS-Antischadsoftware-Erweiterung (Infrastructure-as-a-Service) für Windows Server                              |
|                   | 16. In VM-Skalierungsgruppen sollten Diagnoseprotokolle aktiviert sein.                                    |
|                   | 17. Microsoft Antimalware für Azure sollte für die automatische Aktualisierung von Schutzsignaturen konfiguriert sein. |
|                   | 18. Die Microsoft Antimalware-Erweiterung für Windows muss auf Windows-Servern bereitgestellt werden.                          |
|                   | 19. Es dürfen nur genehmigte VM-Erweiterungen installiert werden                                                    |
|                   | 20. Automatische Patches für Betriebssystemimages in VM-Skalierungsgruppen erzwingen                                  |
|                   | 21. Nicht angefügte Datenträger müssen verschlüsselt werden                                                               |
|                   | 22. Netzwerkschnittstellen dürfen keine öffentlichen IP-Adressen aufweisen.                                                      |
|                   | 23. VMs müssen mit einem genehmigten virtuellen Netzwerk verbunden sein.                                |
|                   | 24. Virtuelle Netzwerke sollten ein angegebenes Gateway für virtuelle Netzwerke verwenden.                                      |
