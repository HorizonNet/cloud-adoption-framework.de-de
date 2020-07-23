---
title: Richtlinien für die CAF-Implementierung auf Unternehmensebene
description: Hier finden Sie Informationen zu den Richtlinien für die CAF-Implementierung auf Unternehmensebene im Microsoft Cloud Adoption Framework für Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 5fee6cc6eefb8529209172d40d6fc3aa73ef8bc3
ms.sourcegitcommit: 08d6d5bda45814745fc181b0a07bcb8c415bf342
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86373168"
---
<!-- cSpell:ignore interdomain VMSS VWAN -->

# <a name="caf-enterprise-scale-implementation-guidelines"></a>Richtlinien für die CAF-Implementierung auf Unternehmensebene

Dieser Abschnitt enthält eine Beschreibung des Einstiegs in die plattformnative Referenzimplementierung auf Unternehmensebene und der Entwurfsziele.

Es gibt drei Kategorien von Aktivitäten, die erforderlich sind, um die Architektur auf Unternehmensebene zu implementieren:

<!-- docsTest:disable -->

1. **Zu erfüllende Anforderungen für die Architektur auf Unternehmensebene:** Diese Kategorie umfasst Aktivitäten, die von den Azure- und Azure AD-Administratoren durchgeführt werden müssen, um eine anfängliche Konfiguration einzurichten. Diese Aktivitäten sind von Natur aus sequenziell, und es handelt sich hauptsächlich um einmalige Aktivitäten.

2. **Aktivieren einer neuen Region („Datei“ > „Neu“ > „Region“):** Diese Aktivitäten sind jeweils erforderlich, wenn die Plattform auf Unternehmensebene auf eine neue Azure-Region erweitert werden muss.

3. **Bereitstellen einer neuen Zielzone („Datei“ > „Neu“ > „Zielzone“):** Hierbei handelt es sich um wiederkehrende Aktivitäten, die erforderlich sind, um eine neue Zielzone zu instanziieren.

<!-- docsTest:enable -->

Für eine Operationalisierung im großen Stil müssen bei diesen Aktivitäten die IaC-Prinzipien (Infrastructure-as-Code) befolgt und Bereitstellungspipelines für die Automatisierung verwendet werden.

## <a name="what-must-be-true-for-a-caf-enterprise-scale-landing-zone"></a>Zu erfüllende Voraussetzungen für eine CAF-Zielzone auf Unternehmensebene

### <a name="enterprise-agreement-ea-enrollment-and-azure-ad-tenants"></a>Enterprise Agreement-Registrierung (EA) und Azure AD-Mandanten

1. Richten Sie den EA-Administrator und das Benachrichtigungskonto ein.

2. Erstellen Sie Abteilungen: business domains/geo-based/org.

3. Erstellen Sie unter einer Abteilung ein EA-Konto.

4. Richten Sie Azure AD Connect für jeden Azure AD-Mandanten ein, wenn die Identität von einem lokalen Standort aus synchronisiert werden soll.

5. Richten Sie keinen ständigen Zugriff auf Azure-Ressourcen und Just-in-Time-Zugriff über Azure AD PIM ein.

### <a name="management-group-and-subscription"></a>Verwaltungsgruppe und Abonnement

1. Erstellen Sie gemäß den Empfehlungen in [diesem Artikel](./management-group-and-subscription-organization.md#define-a-management-group-hierarchy) eine Verwaltungsgruppenhierarchie.

2. Definieren Sie ein Abonnementbereitstellungskriterium zusammen mit den Zuständigkeiten eines Abonnementbesitzers.

3. Erstellen Sie Verwaltungs-, Konnektivitäts- und Identitätsabonnements für Plattformverwaltung, globale Netzwerke und Konnektivitäts- und Identitätsressourcen, z. B. Active Directory-Domänencontroller.

4. Richten Sie ein Git-Repository zum Hosten von IaC und Dienstprinzipalen für die Verwendung mit einer CI/CD-Pipeline für die Plattform ein.

5. Erstellen Sie benutzerdefinierte Rollendefinitionen, und verwalten Sie Berechtigungen mithilfe von Azure AD Privileged Identity Management für Abonnement- und Verwaltungsgruppenbereiche.

6. Erstellen Sie die Azure Policy-Zuweisungen in der unten angegebenen Tabelle für die Zielzonen.

| Name                  | Beschreibung                                                                                   |
|-----------------------|-----------------------------------------------------------------------------------------------|
| [`Deny-PublicEndpoints`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policySetDefinitions-Deny-PublicEndpoints.parameters.json) | Verweigert die Erstellung von Diensten mit öffentlichen Endpunkten in allen Zielzonen. |
| [`Deploy-VM-Backup`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/Landing%20Zones/.AzState/Microsoft.Authorization_policyAssignments-Deploy-VM-Backup.parameters.json) | Stellt sicher, dass die Sicherung konfiguriert ist und für alle VMs in den Zielzonen bereitgestellt wird. |
| [`Deploy-VNet`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Stellt sicher, dass für alle Zielzonen ein VNET bereitgestellt wurde und dass es per Peering mit dem regionalen virtuellen Hub verknüpft ist. |

### <a name="global-networking-and-connectivity"></a>Globale Netzwerke und Konnektivität

1. Ordnen Sie einen geeigneten VNET-CIDR-Bereich für jede Azure-Region zu, in der virtuelle Hubs und VNETs bereitgestellt werden.

2. Falls Sie sich für die Erstellung der Netzwerkressourcen über Azure Policy entscheiden, sollten Sie die unten in der Tabelle angegebenen Richtlinien dem Konnektivitätsabonnement zuweisen. Hierdurch kann von Azure Policy sichergestellt werden, dass die unten in der Liste enthaltenen Ressourcen basierend auf den angegebenen Parametern erstellt werden.
   - Erstellen Sie eine Azure Virtual WAN Standard-Instanz.
   - Erstellen Sie einen virtuellen Azure Virtual WAN-Hub für jede Region. Stellen Sie sicher, dass mindestens ein Gateway (ExpressRoute oder VPN) pro virtuellem Hub bereitgestellt wird.
   - Schützen Sie virtuelle Hubs, indem Sie Azure Firewall auf jedem virtuellen Hub bereitstellen.
   - Erstellen Sie erforderliche Azure Firewall-Richtlinien, und weisen Sie sie sicheren virtuellen Hubs zu.
   - Stellen Sie sicher, dass alle mit einem sicheren virtuellen Hub verbundenen VNETs per Azure Firewall geschützt sind.

3. Führen Sie die Bereitstellung und Konfiguration einer Zone mit privatem Azure-DNS durch.

4. Stellen Sie ExpressRoute-Leitungen mit privatem Azure-Peering bereit. Befolgen Sie die Anleitung unter [Erstellen und Ändern des Peerings für eine ExpressRoute-Verbindung](https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager#private).

5. Verbinden Sie lokale HQs/DCs über ExpressRoute-Leitungen mit virtuellen Azure Virtual WAN-Hubs.

6. Schützen Sie VNET-Datenverkehr für virtuelle Hubs mit NSGs.

7. (Optional:) Richten Sie Verschlüsselung über privates ExpressRoute-Peering ein. Befolgen Sie die Anleitung unter [ExpressRoute-Verschlüsselung: IPsec über ExpressRoute für Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/vpn-over-expressroute).

8. (Optional:) Verbinden Sie Branches über VPN mit dem virtuellen Hub. Befolgen Sie die Anleitung unter [Tutorial: Erstellen einer Site-to-Site-Verbindung per Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-site-to-site-portal).

9. (Optional:) Konfigurieren Sie ExpressRoute Global Reach für das Herstellen von Verbindungen mit lokalen HQs/DCs, wenn mehrere lokale Standorte über ExpressRoute mit Azure verbunden sind. Befolgen Sie die Anleitung unter [Konfigurieren von ExpressRoute Global Reach](https://docs.microsoft.com/azure/expressroute/expressroute-howto-set-global-reach).

Die folgende Liste enthält Azure Policy-Zuweisungen, die beim Implementieren von Netzwerkressourcen für eine Bereitstellung auf Unternehmensebene verwendet werden:

| Name                     | Beschreibung                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-FirewallPolicy`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-FirewallPolicy.parameters.json) | Erstellt eine Firewallrichtlinie. |
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Diese Richtlinie dient zum Bereitstellen eines virtuellen Hubs sowie von Azure Firewall und von VPN-/ExpressRoute-Gateways und zum Konfigurieren der Standardroute zu Azure Firewall in verbundenen VNETs. |
| [`Deploy-VWAN`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vWAN.parameters.json)| Stellt eine Virtual WAN-Instanz bereit. |

### <a name="security-governance-and-compliance"></a>Sicherheit, Governance und Compliance

1. Definieren und wenden Sie ein [Framework für das Zulassen von Diensten](./security-governance-and-compliance.md#service-enablement-framework) an, um sicherzustellen, dass Azure-Dienste die Anforderungen an Unternehmenssicherheit und Governance erfüllen.

2. Erstellen Sie benutzerdefinierte Azure RBAC-Rollendefinitionen.

3. Ermöglichen Sie Azure AD PIM, und ermitteln Sie Azure-Ressourcen für Privileged Identity Management-Vorgänge.

4. Erstellen Sie auf Azure AD beschränkte Gruppen für die Azure-Steuerungsebenenverwaltung von Ressourcen mit Azure AD PIM.

5. Wenden Sie die Richtlinien an, die unten in der ersten Tabelle aufgeführt sind, um sicherzustellen, dass die Azure-Dienste mit den Unternehmensanforderungen konform sind.

6. Definieren Sie eine Benennungskonvention, und erzwingen Sie sie über Azure Policy.

7. Erstellen Sie eine Richtlinienmatrix in allen Bereichen (aktivieren Sie beispielsweise die Überwachung für alle Azure-Dienste per Azure Policy).

Die folgenden Richtlinien sollten verwendet werden, um den Konformitätsstatus unternehmensweit zu erzwingen.

| Name                       | Beschreibung                                                        |
|----------------------------|--------------------------------------------------------------------|
| [`Allowed-ResourceLocation`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyAssignments-Allowed-ResourceLocation.parameters.json)   | Gibt die zulässige Region an, in der Ressourcen bereitgestellt werden können. |
| [`Allowed-RGLocation`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyAssignments-Allowed-RGLocation.parameters.json)         | Gibt die zulässige Region an, in der Ressourcengruppen bereitgestellt werden können. |
| [`Denied-Resources`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyAssignments-Denied-Resources.parameters.json)           | Ressourcen, die für das Unternehmen verweigert werden. |
| [`Deny-AppGW-Without-WAF`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-AppGW-Without-WAF.parameters.json)     | Ermöglicht die Bereitstellung von Anwendungsgateways mit aktivierter WAF. |
| [`Deny-IP-Forwarding`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyAssignments-Deny-IP-Forwarding.parameters.json)         | Verweigert die IP-Weiterleitung. |
| [`Deny-RDP-From-Internet`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyAssignments-Deny-RDP-From-Internet.parameters.json)     | Verweigert RDP-Verbindungen aus dem Internet. |
| [`Deny-Subnet-Without-Nsg`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deny-Subnet-Without-Nsg.parameters.json)    | Verweigert die Subnetzerstellung ohne NSG. |
| [`Deploy-ASC-CE`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-CE.parameters.json)              | Dient zum Einrichten des fortlaufenden Exports von Security Center in Ihren Log Analytics-Arbeitsbereich. |
| [`Deploy-ASC-Monitoring`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyAssignments-Deploy-ASC-Monitoring.parameters.json)      | Aktiviert die Überwachung in Azure Security Center. |
| [`Deploy-ASC-Standard`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-ASC-Standard.parameters.json)        | Stellt sicher, dass Security Center Standard für Abonnements aktiviert ist. |
| [`Deploy-Diag-ActivityLog`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diagnostics-ActivityLog.parameters.json) | Ermöglicht die Verwendung von Aktivitätsprotokollen für die Diagnose und die Weiterleitung an Log Analytics. |
| [`Deploy-Diag-LogAnalytics`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | |
| [`Deploy-VM-Monitoring`](https://github.com/Azure/Enterprise-Scale/blob/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Diagnostics-VM.parameters.json) | Stellt sicher, dass die VM-Überwachung aktiviert ist. |

### <a name="platform-identity"></a>Plattformidentität

1. Falls Sie sich für die Erstellung der Identitätsressourcen über Azure Policy entscheiden, sollten Sie die unten in der Tabelle angegebenen Richtlinien dem Identitätsabonnement zuweisen. Hierdurch kann von Azure Policy sichergestellt werden, dass die unten in der Liste enthaltenen Ressourcen basierend auf den angegebenen Parametern erstellt werden.

2. Stellen Sie die Active Directory-Domänencontroller bereit.

In der folgenden Liste sind Richtlinien aufgeführt, die verwendet werden können, wenn Identitätsressourcen für eine Bereitstellung auf Unternehmensebene implementiert werden.

| Name                         | Beschreibung                                                               |
|------------------------------|---------------------------------------------------------------------------|
| [`DataProtectionSecurityCenter`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState) | Von Azure Security Center automatisch erstellter Datenschutz. |
| [`Deploy-VNet-Identity`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vNet.parameters.json) | Stellt ein VNET zu Hostingzwecken unter dem Identitätsabonnement bereit (Beispiel: DC). |

### <a name="platform-management-and-monitoring"></a>Plattformverwaltung und -überwachung

1. Erstellen Sie Dashboards für Richtlinien-Compliance und Sicherheit, um organisations- und ressourcenbezogene Ansichten zu erhalten.

2. Erstellen Sie einen Workflow für Plattformgeheimnisse (Dienstprinzipale und Automation-Konto) und Schlüsselrollover.

3. Richten Sie die Langzeitarchivierung und -aufbewahrung für Protokolle in Log Analytics ein.

4. Richten Sie Azure Key Vault zum Speichern von Plattformgeheimnissen ein.

5. Falls Sie sich für die Erstellung der Ressourcen für die Plattformverwaltung über Azure Policy entscheiden, sollten Sie die unten in der Tabelle angegebenen Richtlinien dem Verwaltungsabonnement zuweisen. Hierdurch kann von Azure Policy sichergestellt werden, dass die unten in der Liste enthaltenen Ressourcen basierend auf den angegebenen Parametern erstellt werden.

| Name                   | Beschreibung                                                                            |
|------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-LA-Config`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-LA-Config.parameters.json) | Konfiguration des Log Analytics-Arbeitsbereichs. |
| [`Deploy-Log-Analytics`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-Log-Analytics.parameters.json) | Stellt einen Log Analytics-Arbeitsbereich bereit. |

## <a name="file--new--region"></a>**Datei > Neu > Region**

1. Falls Sie sich für die Erstellung der Netzwerkressourcen über Azure Policy entscheiden, sollten Sie die unten in der Tabelle angegebenen Richtlinien dem Konnektivitätsabonnement zuweisen. Hierdurch kann von Azure Policy sichergestellt werden, dass die unten in der Liste enthaltene Ressource basierend auf den angegebenen Parametern erstellt wird.

    - Erstellen Sie unter dem Konnektivitätsabonnement einen neuen virtuellen Hub innerhalb der vorhandenen Virtual WAN-Instanz.
    - Schützen Sie den virtuellen Hub, indem Sie Azure Firewall auf dem virtuellen Hub bereitstellen und vorhandene oder neue Firewallrichtlinien mit Azure Firewall verknüpfen.
    - Stellen Sie sicher, dass alle mit einem sicheren virtuellen Hub verbundenen VNETs per Azure Firewall geschützt sind.

2. Verbinden Sie den virtuellen Hub entweder per ExpressRoute oder VPN mit dem lokalen Netzwerk.

3. Schützen Sie VNET-Datenverkehr für virtuelle Hubs mit NSGs.

4. (Optional:) Richten Sie Verschlüsselung über privates ExpressRoute-Peering ein.

| Name                     | Beschreibung                                                                            |
|--------------------------|----------------------------------------------------------------------------------------|
| [`Deploy-VHub`](https://github.com/Azure/Enterprise-Scale/tree/main/azopsreference/3fc1081d-6105-4e19-b60c-1ec1252cf560/contoso/.AzState/Microsoft.Authorization_policyDefinitions-Deploy-vHUB.parameters.json) | Diese Richtlinie dient zum Bereitstellen eines virtuellen Hubs, von Azure Firewall und von Gateways (VPN/ExpressRoute) sowie zum Konfigurieren der Standardroute zu Azure Firewall in verbundenen VNETs. |

<!-- docsTest:disable -->

## <a name="file---new---landing-zone-for-applications-and-workloads"></a>Datei > Neu > Zielzone für Anwendungen und Workloads

<!-- docsTest:enable -->

1. Erstellen Sie ein Abonnement, und verschieben Sie es unter den Verwaltungsgruppenbereich `Landing Zones`.

2. Erstellen Sie Azure AD-Gruppen für das Abonnement (beispielsweise `Owner`, `Reader` und `Contributor`).

3. Erstellen Sie Azure AD PIM-Berechtigungen für eingerichtete Azure AD-Gruppen.
