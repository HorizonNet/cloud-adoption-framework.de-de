---
title: Richtlinien für die Implementierung auf Unternehmensebene
description: Hier finden Sie Informationen zu den Richtlinien für die Implementierung auf Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 078ac0e661b946d9fb493dff0b1d2ee087777726
ms.sourcegitcommit: 826f2a3f0353bb711917e99d9a17f6198fb41ada
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2020
ms.locfileid: "93024605"
---
<!-- cSpell:ignore interdomain VMSS VWAN -->

# <a name="enterprise-scale-implementation-guidelines"></a>Richtlinien für die Implementierung auf Unternehmensebene

Dieser Artikel enthält eine Beschreibung des Einstiegs in die plattformnative Referenzimplementierung auf Unternehmensebene und der Entwurfsziele.

Zum Implementieren der Architektur auf Unternehmensebene müssen Sie die Aktivitäten in die folgenden Kategorien unterteilen:

<!-- docutune:disable -->

1. **Zu erfüllende Anforderungen für die Architektur auf Unternehmensebene:** Hierzu gehören Aktivitäten, die von den Azure- und Azure Active Directory-Administratoren durchgeführt werden müssen, um eine anfängliche Konfiguration einzurichten. Diese Aktivitäten sind von Natur aus sequenziell, und es handelt sich hauptsächlich um einmalige Aktivitäten.

2. **Aktivieren einer neuen Region („Datei“ > „Neu“ > „Region“):** Hierzu gehören Aktivitäten, die erforderlich dafür sind, die Plattform auf Unternehmensebene in eine neue Azure-Region zu erweitern.

3. **Bereitstellen einer neuen Zielzone („Datei“ > „Neu“ > „Zielzone“):** Hierbei handelt es sich um wiederkehrende Aktivitäten, die erforderlich sind, um eine neue Zielzone zu instanziieren.

<!-- docutune:enable -->

Für eine Operationalisierung im großen Stil müssen bei diesen Aktivitäten die IaC-Prinzipien (Infrastructure-as-Code) befolgt und mithilfe von Bereitstellungspipelines automatisiert werden.

## <a name="what-must-be-true-for-an-enterprise-scale-landing-zone"></a>Zu erfüllende Voraussetzungen für eine Zielzone auf Unternehmensebene

In den folgenden Abschnitten werden die Schritte zum Abschließen dieser Aktivitätskategorie im Microsoft Cloud Adoption Framework für Azure aufgeführt.

### <a name="enterprise-agreement-enrollment-and-azure-ad-tenants"></a>Enterprise Agreement-Registrierung und Azure AD-Mandanten

1. Richten Sie den EA-Administrator und das Benachrichtigungskonto ein.

2. Erstellen Sie Abteilungen: business domains/geo-based/org.

3. Erstellen Sie unter einer Abteilung ein EA-Konto.

4. Richten Sie Azure AD Connect für jeden Azure AD-Mandanten ein, wenn die Identität von einem lokalen Standort aus synchronisiert werden soll.

5. Richten Sie keinen ständigen Zugriff auf Azure-Ressourcen und Just-in-Time-Zugriff über Azure AD Privileged Identity Management (PIM) ein.

### <a name="management-group-and-subscription"></a>Verwaltungsgruppe und Abonnement

1. Erstellen Sie eine Verwaltungsgruppenhierarchie, indem Sie die Empfehlungen unter [Organisieren von Verwaltungsgruppen und Abonnements](./management-group-and-subscription-organization.md#define-a-management-group-hierarchy) befolgen.

2. Definieren Sie die Kriterien für die Abonnementbereitstellung und die Zuständigkeiten eines Abonnementbesitzers.

3. Erstellen Sie Verwaltungs-, Konnektivitäts- und Identitätsabonnements für Plattformverwaltung, globale Netzwerke und Konnektivitäts- und Identitätsressourcen, z. B. Active Directory-Domänencontroller.

4. Richten Sie ein Git-Repository zum Hosten von IaC und Dienstprinzipale für die Verwendung mit einer Plattformpipeline für Continuous Integration und Continuous Deployment (CI/CD) ein.

5. Erstellen Sie benutzerdefinierte Rollendefinitionen, und verwalten Sie Berechtigungen mithilfe von Azure AD Privileged Identity Management für Abonnement- und Verwaltungsgruppenbereiche.

6. Erstellen Sie die Azure Policy-Zuweisungen in der folgenden Tabelle für die Zielzonen.

  | Name                  |     Beschreibung                                                                                     |
  |-----------------------|-----------------------------------------------------------------------------------------------|
  | [`Deny-PublicEndpoints`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policySetDefinitions-Deny-PublicEndpoints.parameters.json) | Verweigert die Erstellung von Diensten mit öffentlichen Endpunkten in allen Zielzonen. |
  | [`Deploy-VM-Backup`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/Landing%20Zones%20(landingzones)/.AzState/Microsoft.Authorization_policyAssignments-Deploy-VM-Backup.parameters.json) | Stellt sicher, dass die Sicherung konfiguriert ist und für alle VMs in den Zielzonen bereitgestellt wird. |
  | [`Deploy-VNet`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Stellen Sie sicher, dass für alle Zielzonen ein virtuelles Netzwerk bereitgestellt wurde und dass es per Peering mit dem regionalen virtuellen Hub verknüpft ist. |

#### <a name="sandbox-governance-guidance"></a>Leitfaden zur Sandbox-Governance

Wie unter [wichtigen Entwurfsbereich „Organisation von Verwaltungsgruppen und Abonnements“](./management-group-and-subscription-organization.md) ausführlich beschrieben, sollte für Abonnements innerhalb der Hierarchie der Sandbox-Verwaltungsgruppe ein Ansatz mit weniger restriktiven Richtlinien verwendet werden. Da diese Abonnements von Benutzern innerhalb des Unternehmens zum Experimentieren und zum Entwickeln von Innovationen mit Azure-Produkten und -Diensten verwendet werden sollten, die in Ihrer Zielzonenhierarchie möglicherweise noch nicht erlaubt sind, sollte geprüft werden, ob ihre Ideen/Konzepte funktionieren, bevor sie in eine formale Entwicklungsumgebung überführt werden.

Allerdings müssen für diese Abonnements in der Hierarchie der Sandbox-Verwaltungsgruppe noch einige Schutzmaßnahmen angewendet werden, um sicherzustellen, dass sie nur in der richtigen Weise verwendet werden, z. B. für Innovation, Test neuer Azure-Dienste/-Produkte/-Features, Prüfung der Ideenfindung. 

**Daher empfehlen wir Folgendes:**

1. Erstellen Sie die Azure Policy-Zuweisungen in der folgenden Tabelle im Bereich der Sandbox-Verwaltungsgruppe.

  | Name                  |     BESCHREIBUNG                                                                                     | Hinweise zur Zuweisung |
  |-----------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------|
  | [`Deny-VNET-Peering-Cross-Subscription`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState) | Verhindert, dass VNET-Peeringverbindungen zu anderen VNETs außerhalb des Abonnements erstellt werden. | Stellen Sie sicher, dass diese Richtlinie nur der Bereichsebene der Sandbox-Verwaltungsgruppenhierarchie zugewiesen wird. |
  | [`Denied-Resources`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Denied-Resources.parameters.json)           | Ressourcen, deren Erstellung in den Sandbox-Abonnements verweigert wird. Dadurch wird verhindert, dass Hybridverbindungsressourcen erstellt werden *z. B. VPN/ExpressRoute/VirtualWAN* | Wählen Sie bei der Zuweisung dieser Richtlinie die folgenden Ressourcen aus, um die Erstellung folgender Komponenten zu verweigern: VPN-Gateways: `microsoft.network/vpngateways`, P2S-Gateways: `microsoft.network/p2svpngateways`, virtuelle WANs: `microsoft.network/virtualwans`, virtuelle WAN-Hubs: `microsoft.network/virtualhubs`, ExpressRoute-Leitungen: `microsoft.network/expressroutecircuits`, ExpressRoute-Gateways: `microsoft.network/expressroutegateways`, ExpressRoute-Ports: `microsoft.network/expressrouteports`, ExpressRoute-Querverbindungen: `microsoft.network/expressroutecrossconnections` und lokale Netzwerkgateways: `microsoft.network/localnetworkgateways`. | 
  | [`Deploy-Budget-Sandbox`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState) | Stellt sicher, dass für jedes Sandbox-Abonnement ein Budget vorhanden ist und E-Mail-Warnungen aktiviert sind. Das Budget erhält den Namen `default-sandbox-budget` in jedem Abonnement. | Wenn die Standardwerte der Parameter während der Zuweisung der Richtlinie nicht geändert werden, wird ein Budget (`default-sandbox-budget`) mit einem Währungsschwellenwert von 1000 erstellt und bei 90% und 100% des Budgetschwellenwerts eine E-Mail-Warnung an die Eigentümer und Mitwirkenden des Abonnements (basierend auf der RBAC-Rollenzuweisung) gesendet. |

### <a name="global-networking-and-connectivity"></a>Globale Netzwerke und Konnektivität

1. Ordnen Sie einen geeigneten CIDR-Bereich des virtuellen Netzwerks für jede Azure-Region zu, in der virtuelle Hubs und virtuelle Netzwerke bereitgestellt werden.

2. Falls Sie sich für die Erstellung der Netzwerkressourcen über Azure Policy entscheiden, sollten Sie die in der folgenden Tabelle angegebenen Richtlinien dem Konnektivitätsabonnement zuweisen. Hierdurch kann von Azure Policy sichergestellt werden, dass die in der folgenden Liste enthaltenen Ressourcen basierend auf den angegebenen Parametern erstellt werden.
   - Erstellen Sie eine Azure Virtual WAN Standard-Instanz.
   - Erstellen Sie einen virtuellen Azure Virtual WAN-Hub für jede Region. Stellen Sie sicher, dass mindestens ein Gateway (Azure ExpressRoute oder VPN) pro virtuellen Hub bereitgestellt wird.
   - Schützen Sie virtuelle Hubs, indem Sie Azure Firewall auf jedem virtuellen Hub bereitstellen.
   - Erstellen Sie erforderliche Azure Firewall-Richtlinien, und weisen Sie sie sicheren virtuellen Hubs zu.
   - Stellen Sie sicher, dass alle virtuellen Netzwerke durch Azure Firewall geschützt werden, die mit einem sicheren virtuellen Hub verbunden sind.

3. Führen Sie die Bereitstellung und Konfiguration einer Zone mit privatem Azure-DNS durch.

4. Stellen Sie ExpressRoute-Leitungen mit privatem Azure-Peering bereit. Befolgen Sie die Anleitung unter [Erstellen und Ändern des Peerings für eine ExpressRoute-Verbindung](/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private).

5. Verbinden Sie lokale HQs/DCs über ExpressRoute-Leitungen mit virtuellen Azure Virtual WAN-Hubs.

6. Schützen Sie den Datenverkehr zwischen virtuellen Netzwerken und virtuellen Hubs mit Netzwerksicherheitsgruppen.

7. (Optional) Richten Sie die Verschlüsselung über privates ExpressRoute-Peering ein. Befolgen Sie die Anleitung unter [ExpressRoute-Verschlüsselung: IPsec über ExpressRoute für Virtual WAN](/azure/virtual-wan/vpn-over-expressroute).

8. (Optional) Verbinden Sie Zweigstellen über VPN mit dem virtuellen Hub. Befolgen Sie die Anleitung unter [Tutorial: Erstellen einer Site-to-Site-Verbindung per Azure Virtual WAN](/azure/virtual-wan/virtual-wan-site-to-site-portal).

9. (Optional) Konfigurieren Sie ExpressRoute Global Reach für das Herstellen von Verbindungen mit lokalen HQs/DCs, wenn mehrere lokale Standorte über ExpressRoute mit Azure verbunden sind. Befolgen Sie die Anleitung unter [Konfigurieren von ExpressRoute Global Reach](/azure/expressroute/expressroute-howto-set-global-reach).

Die folgende Liste enthält Azure Policy-Zuweisungen, die Sie zum Implementieren von Netzwerkressourcen für eine Bereitstellung auf Unternehmensebene verwenden:

| Name                     | Beschreibung                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-FirewallPolicy`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-FirewallPolicy.parameters.json) | Erstellt eine Firewallrichtlinie. |
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Diese Richtlinie stellt einen virtuellen Hub, Azure Firewall und VPN/ExpressRoute-Gateways bereit. Außerdem konfiguriert sie die Standardroute für mit Azure Firewall verbundene virtuelle Netzwerke. |
| [`Deploy-VWAN`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vWAN.parameters.json)| Stellt eine Virtual WAN-Instanz bereit. |

### <a name="security-governance-and-compliance"></a>Sicherheit, Governance und Compliance

1. Definieren und wenden Sie ein [Framework für das Zulassen von Diensten](./security-governance-and-compliance.md#service-enablement-framework) an, um sicherzustellen, dass Azure-Dienste die Anforderungen an Unternehmenssicherheit und Governance erfüllen.

2. Erstellen Sie benutzerdefinierte Definitionen für die rollenbasierte Zugriffssteuerung.

3. Aktivieren Sie Azure AD-PIM, und ermitteln Sie Azure-Ressourcen, um PIM zu unterstützen.

4. Erstellen Sie auf Azure AD beschränkte Gruppen für die Azure-Steuerungsebenenverwaltung von Ressourcen mit Azure AD PIM.

5. Wenden Sie die Richtlinien an, die in der folgenden Tabelle aufgeführt werden, um sicherzustellen, dass die Azure-Dienste den Unternehmensanforderungen entsprechen.

6. Definieren Sie eine Benennungskonvention, und erzwingen Sie sie über Azure Policy.

7. Erstellen Sie eine Richtlinienmatrix in allen Bereichen (aktivieren Sie beispielsweise die Überwachung für alle Azure-Dienste per Azure Policy).

Die folgenden Richtlinien sollten verwendet werden, um den Konformitätsstatus unternehmensweit zu erzwingen.

| Name                       | Beschreibung                                                        |
|----------------------------|--------------------------------------------------------------------|
| [`Allowed-ResourceLocation`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Allowed-ResourceLocation.parameters.json)   | Gibt die zulässige Region an, in der Ressourcen bereitgestellt werden können. |
| [`Allowed-RGLocation`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Allowed-RGLocation.parameters.json)         | Gibt die zulässige Region an, in der Ressourcengruppen bereitgestellt werden können. |
| [`Denied-Resources`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Denied-Resources.parameters.json)           | Ressourcen, die für das Unternehmen verweigert werden |
| [`Deny-AppGW-Without-WAF`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deny-AppGW-Without-WAF.parameters.json)     | Lässt die Aktivierung von mit Azure Web Application Firewall bereitgestellten Anwendungsgateways zu |
| [`Deny-IP-Forwarding`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Deny-IP-Forwarding.parameters.json)         | Verweigert die IP-Weiterleitung |
| [`Deny-RDP-From-Internet`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Deny-RDP-From-Internet.parameters.json)     | Verweigert RDP-Verbindungen über das Internet |
| [`Deny-Subnet-Without-Nsg`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deny-Subnet-Without-Nsg.parameters.json)    | Verweigert die Erstellung von Subnetzen ohne Netzwerksicherheitsgruppe |
| [`Deploy-ASC-CE`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-CE.parameters.json)              | Dient zum Einrichten des fortlaufenden Exports von Azure Security Center in Ihren Log Analytics-Arbeitsbereich |
| [`Deploy-ASC-Monitoring`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyAssignments-Deploy-ASC-Monitoring.parameters.json)      | Aktiviert die Überwachung in Security Center |
| [`Deploy-ASC-Standard`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Standard.parameters.json)        | Stellt sicher, dass Security Center Standard für Abonnements aktiviert ist. |
| [`Deploy-Diag-ActivityLog`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diagnostics-ActivityLog.parameters.json) | Ermöglicht die Verwendung von Aktivitätsprotokollen für die Diagnose und die Weiterleitung an Log Analytics. |
| [`Deploy-Diag-LogAnalytics`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | |
| [`Deploy-VM-Monitoring`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diagnostics-VM.parameters.json) | Stellt sicher, dass die VM-Überwachung aktiviert ist. |

### <a name="platform-identity"></a>Plattformidentität

1. Wenn Sie die Identitätsressourcen über Azure Policy erstellen, weisen Sie die in der folgenden Tabelle aufgeführten Richtlinien dem Identitätsabonnement zu. Dadurch stellt Azure Policy sicher, dass die Ressourcen in der folgenden Liste anhand der angegebenen Parameter erstellt werden.

2. Stellen Sie die Active Directory-Domänencontroller bereit.

In der folgenden Liste werden Richtlinien aufgeführt, die Sie verwenden können, wenn Sie Identitätsressourcen für eine Bereitstellung auf Unternehmensebene implementieren.

| Name                         | BESCHREIBUNG                                                               |
|------------------------------|---------------------------------------------------------------------------|
| [`DataProtectionSecurityCenter`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/) | Der automatisch von Security Center erstellte Datenschutz |
| [`Deploy-VNet-Identity`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Stellt ein virtuelles Netzwerk zu Hostingzwecken im Identitätsabonnement bereit (z. B. DC). |

### <a name="platform-management-and-monitoring"></a>Plattformverwaltung und -überwachung

1. Erstellen Sie Dashboards für Richtlinien-Compliance und Sicherheit, um organisations- und ressourcenbezogene Ansichten zu erhalten.

2. Erstellen Sie einen Workflow für Plattformgeheimnisse (Dienstprinzipale und Automation-Konto) und Schlüsselrollover.

3. Richten Sie die Langzeitarchivierung und -aufbewahrung für Protokolle in Log Analytics ein.

4. Richten Sie Azure Key Vault zum Speichern von Plattformgeheimnissen ein.

5. Wenn Sie die Plattformverwaltungsressourcen mit Azure Policy erstellen, weisen Sie die in der folgenden Tabelle aufgeführten Richtlinien dem Verwaltungsabonnement zu. Hierdurch kann von Azure Policy sichergestellt werden, dass die in der folgenden Liste enthaltenen Ressourcen basierend auf den angegebenen Parametern erstellt werden.

| Name                   | Beschreibung                                                                            |
|------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-LA-Config`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-LA-Config.parameters.json) | Konfiguration des Log Analytics-Arbeitsbereichs. |
| [`Deploy-Log-Analytics`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | Stellt einen Log Analytics-Arbeitsbereich bereit. |

## <a name="file--new--region"></a>Datei > Neu > Region

1. Wenn Sie die Netzwerkressourcen über Azure Policy erstellen, weisen Sie die in der folgenden Tabelle aufgeführten Richtlinien dem Konnektivitätsabonnement zu. Hierdurch kann von Azure Policy sichergestellt werden, dass die in der folgenden Liste enthaltenen Ressourcen basierend auf den angegebenen Parametern erstellt werden.

    - Erstellen Sie unter dem Konnektivitätsabonnement einen neuen virtuellen Hub innerhalb der vorhandenen Virtual WAN-Instanz.
    - Schützen Sie den virtuellen Hub, indem Sie Azure Firewall auf dem virtuellen Hub bereitstellen und vorhandene oder neue Firewallrichtlinien mit Azure Firewall verknüpfen.
    - Stellen Sie sicher, dass alle virtuellen Netzwerke durch Azure Firewall geschützt werden, die mit einem sicheren virtuellen Hub verbunden sind.

2. Verbinden Sie den virtuellen Hub entweder per ExpressRoute oder VPN mit dem lokalen Netzwerk.

3. Schützen Sie den Datenverkehr des virtuellen Netzwerks über virtuelle Hubs mithilfe von Netzwerksicherheitsgruppen.

4. (Optional) Richten Sie die Verschlüsselung über privates ExpressRoute-Peering ein.

| Name                     | BESCHREIBUNG                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560%20(3fc1081d-6105-4e19-b60c-1ec1252cf560)/contoso%20(contoso)/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Diese Richtlinie stellt einen virtuellen Hub, Azure Firewall und Gateways (VPN/ExpressRoute) bereit. Außerdem konfiguriert sie die Standardroute für mit Azure Firewall verbundene virtuelle Netzwerke. |

<!-- docutune:disable -->

## <a name="file--new--landing-zone-for-applications-and-workloads"></a>Datei > Neu > Zielzone für Anwendungen und Workloads

<!-- docutune:enable -->

1. Erstellen Sie ein Abonnement, und verschieben Sie es unter den Verwaltungsgruppenbereich `Landing Zones`.

2. Erstellen Sie Azure AD-Gruppen für das Abonnement (beispielsweise `Owner`, `Reader` und `Contributor`).

3. Erstellen Sie Azure AD PIM-Berechtigungen für eingerichtete Azure AD-Gruppen.
