---
title: Identitäts- und Zugriffsverwaltung
description: Untersuchen Sie Entwurfsüberlegungen und Empfehlungen zur Identitäts- und Zugriffsverwaltung in einer Unternehmensumgebung.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 464e20686a9e61157f350491c97396345fe9ad95
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447352"
---
# <a name="identity-and-access-management"></a>Identitäts- und Zugriffsverwaltung

Die Identität stellt die Grundlage für einen hohen Prozentsatz an Sicherheitszusicherungen dar. Sie ermöglicht Zugriff auf Grundlage ihrer Authentifizierung und von Autorisierungssteuerungen in Clouddiensten, um Daten und Ressourcen zu schützen und zu bestimmen, welche Anforderungen zulässig sind.

IAM (Identity & Access Management, Identitäts- und Zugriffsverwaltung) stellt die Grenzsicherheit in der öffentlichen Cloud dar. Sie muss als die Grundlage jeder sicheren und vollständig konformen öffentlichen Cloudarchitektur behandelt werden. Azure bietet eine umfassende Reihe von Diensten, Tools und Referenzarchitekturen, die es Organisationen wie hier beschrieben ermöglichen, äußerst sichere, betriebseffiziente Umgebungen einzurichten.

In diesem Abschnitt werden Entwurfsüberlegungen und Empfehlungen zur Identitäts- und Zugriffsverwaltung (IAM) in einer Unternehmensumgebung untersucht.

## <a name="why-we-need-identity-and-access-management"></a>Gründe für eine Identitäts- und Zugriffsverwaltung

Die IT-Landschaft in Unternehmen wird zunehmend komplexer und heterogener. Um Compliance und Sicherheit für diese Umgebung zu gewährleisten, ermöglicht IAM den gewünschten Personen aus den richtigen Gründen zur gewünschten Zeit den Zugriff auf die gewünschten Ressourcen.

### <a name="plan-for-identity-and-access-management"></a>Planen der Identitäts- und Zugriffsverwaltung

Unternehmen arbeiten für den betrieblichen Zugriff in der Regel mit einem Ansatz der geringsten Rechte. Dieses Modell sollte so auf Azure übertragen werden, dass die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) von Azure Active Directory (Azure AD) und benutzerdefinierte Rollendefinitionen zum Einsatz kommen. Die Planung, wie der Zugriff auf Ressourcen in Azure und auf Datenebene geregelt werden soll, ist von entscheidender Bedeutung. Jeder Entwurf für IAM und RBAC muss regulatorische, sicherheitstechnische und betriebliche Anforderungen erfüllen, ehe er akzeptiert werden kann.

Die Identitäts- und Zugriffsverwaltung ist ein mehrstufiger Prozess, der eine sorgfältige Planung für die Integration von Identitäten und andere Sicherheitsaspekte wie die Sperrung veralteter Authentifizierungsverfahren und die Planung für moderne Kennwörter umfasst. Die Stagingplanung umfasst auch die Auswahl der Identitäts- und-Zugriffsverwaltung für B2B (Business-to-Business) oder B2C (Business-to-Consumer). Auch wenn diese Anforderungen variieren, gibt es allgemeingültige Entwurfsüberlegungen und -empfehlungen, die für eine Unternehmenszielzone zu berücksichtigen sind.

![Diagramm, das die Identitäts- und Zugriffsverwaltung zeigt.](./media/iam.png)

_Abbildung 1: Identitäts- und Zugriffsverwaltung._

**Überlegungen zum Entwurf:**

- Beim Aufstellen eines Frameworks zu IAM und Governance gibt es Grenzen hinsichtlich der Anzahl von benutzerdefinierten Rollen und Rollenzuweisungen, die berücksichtigt werden müssen. Weitere Informationen finden Sie unter [Grenzwerte für rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC)](/azure/azure-resource-manager/management/azure-subscription-service-limits#role-based-access-control-limits).
- Es gilt ein Grenzwert von 2.000 benutzerdefinierten RBAC-Rollenzuweisungen pro Abonnement.
- Pro Verwaltungsgruppe gilt ein Grenzwert von 500 benutzerdefinierten RBAC-Rollenzuweisungen.
- Ressourcenbesitz: zentralisiert oder im Verbund:
  - Gemeinsam genutzte Ressourcen oder jeder Aspekt der Umgebung, der eine Sicherheitsgrenze implementiert oder erzwingt, wie z. B. das Netzwerk, müssen zentral verwaltet werden. Diese Anforderung ist Teil vieler regulatorischer Bestimmungen. Sie ist die Standardmethode für jede Organisation, die Zugriff auf vertrauliche oder kritische Geschäftsressourcen gewährt oder verweigert.
  - Das Verwalten von Anwendungsressourcen, die keine Sicherheitsgrenzen oder andere Aspekte verletzen, die zur Aufrechterhaltung von Sicherheit und Compliance erforderlich sind, kann an Anwendungsteams delegiert werden. Durch die Möglichkeit für Benutzer, Ressourcen innerhalb einer sicher verwalteten Umgebung bereitzustellen, können Unternehmen die Agilitätsvorteile der Cloud ausnutzen und gleichzeitig die Verletzung kritischer Sicherheits- oder Governancegrenzen verhindern.

<!-- docutune:ignore Azure-AD-only Azure-AD-managed -->

**Entwurfsempfehlungen:**

- Verwenden Sie nach Möglichkeit Azure AD [RBAC](/azure/role-based-access-control/overview), um den Zugriff auf Ressourcen auf Datenebene zu verwalten. Beispiele sind Azure Key Vault, ein Speicherkonto oder eine SQL-Datenbank.
- Stellen Sie für alle Benutzer mit Zugriffsrechten für Azure-Umgebungen über Azure AD Richtlinien für bedingten Zugriff bereit. Dadurch steht ein weiterer Mechanismus zur Verfügung, um eine kontrollierte Azure-Umgebung vor unberechtigtem Zugriff zu schützen.
- Erzwingen Sie für alle Benutzer mit Zugriffsrechten für die Azure-Umgebungen eine mehrstufige Authentifizierung. Die Erzwingung der mehrstufigen Authentifizierung ist eine Anforderung vieler Complianceframeworks. Sie senkt das Risiko des Diebstahls von Anmeldeinformationen und des nicht autorisierten Zugriffs erheblich.
- Setzen Sie [Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-configure) ein, um einen ständigen Zugriff zu unterbinden und das Prinzip der geringsten Rechte umzusetzen. Ordnen Sie die Rollen Ihrer Organisation dem erforderlichen Mindestzugriff zu. Azure AD PIM kann entweder als Erweiterung vorhandener Tools und Prozesse dienen, wie beschrieben native Azure-Tools nutzen oder beides nach Bedarf nutzen.
- Verwenden Sie in Azure AD PIM beim Gewähren von Zugriff auf Ressourcen für Ressourcen auf Azure-Steuerungsebene reine Azure AD-Gruppen.
  - Fügen Sie lokale Gruppen zur reinen Azure AD-Gruppe hinzu, wenn bereits ein Gruppenverwaltungssystem vorhanden ist.
- Nutzen Sie Azure AD PIM-Zugriffsüberprüfungen, um Ressourcenberechtigungen regelmäßig zu prüfen. Zugriffsüberprüfungen sind Teil vieler Complianceframeworks. Infolgedessen werden viele Organisationen bereits über ein Verfahren verfügen, um diese Anforderung zu erfüllen.
- Integrieren Sie Azure AD-Protokolle in [Azure Monitor](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor), das für die Plattform von zentraler Bedeutung ist. Azure Monitor ermöglicht eine einzige Quelle für die Wahrheit für Protokoll- und Überwachungsdaten in Azure und gibt Unternehmen cloudnative Optionen an die Hand, um die Anforderungen an Sammlung und Aufbewahrung von Protokollen zu erfüllen.
- Wenn Anforderungen in Bezug auf Datenhoheit bestehen, können benutzerdefinierte Benutzerrichtlinien zu deren Erzwingung bereitgestellt werden.
- Nutzen Sie innerhalb des Azure AD-Mandanten benutzerdefinierte RBAC-Rollendefinitionen unter Berücksichtigung der folgenden Schlüsselrollen:

| Role | Verwendung | Aktionen | Keine Aktionen |
|---|---|---|---|
| Azure-Plattformbesitzer (z. B. integrierte Rolle „Besitzer“)               | Verwaltung des Lebenszyklus von Verwaltungsgruppen und Abonnements                                                           | `*`                                                                                                                                                                                                                  |                                                                                                                                                                                         |
| Netzwerkverwaltung (NetOps)        | Plattformweite globale Konnektivitätsverwaltung: virtuelle Netzwerke, UDRs, NSGs, NVAs, VPN, Azure ExpressRoute und andere            | `*/read`, `Microsoft.Authorization/*/write`, `Microsoft.Network/vpnGateways/*`, `Microsoft.Network/expressRouteCircuits/*`, `Microsoft.Network/routeTables/write`, `Microsoft.Network/vpnSites/*`                              |                                                                                                                                                                               |
| SecOps       | Sicherheitsadministratorrolle mit horizontaler Sicht auf die gesamte Azure-Umgebung und die Bereinigungsrichtlinie von Azure Key Vault | `*/read`, `*/register/action`, `Microsoft.KeyVault/locations/deletedVaults/purge/action`, `Microsoft.Insights/alertRules/*`, `Microsoft.Authorization/policyDefinitions/*`, `Microsoft.Authorization/policyAssignments/*`, `Microsoft.Authorization/policySetDefinitions/*`, `Microsoft.PolicyInsights/*`, `Microsoft.Security/*` |                                                                            |
| Abonnementbesitzer                 | Delegierte Rolle für Abonnementbesitzer, die von der Rolle „Besitzer“ für das Abonnement abgeleitet ist                                       | `*`                                                                                                                                                                                                                  | `Microsoft.Authorization/*/write`, `Microsoft.Network/vpnGateways/*`, `Microsoft.Network/expressRouteCircuits/*`, `Microsoft.Network/routeTables/write`, `Microsoft.Network/vpnSites/*` |
| Anwendungsbesitzer (DevOps/AppOps) | Die dem Anwendungs-/Betriebsteam auf Ressourcengruppenebene zugewiesene Rolle „Mitwirkender“                                 | `*`                                                                                                                                                                                                                   | `Microsoft.Authorization/*/write`, `Microsoft.Network/publicIPAddresses/write`, `Microsoft.Network/virtualNetworks/write`, `Microsoft.KeyVault/locations/deletedVaults/purge/action`                                         |

- Nutzen Sie den JIT-Zugriff (Just-in-Time) von Azure Security Center für alle IaaS-Ressourcen (Infrastructure-as-a-Service), um Schutz auf Netzwerkebene für den kurzlebigen Zugriff von Benutzern auf IaaS-VMs zu aktivieren.
- Nutzen Sie mit Azure AD verwaltete Identitäten für Azure-Ressourcen, um eine Authentifizierung auf Basis von Benutzernamen und Kennwörtern zu vermeiden. Da viele Sicherheitsverletzungen bei Ressourcen in öffentlichen Clouds ihren Ursprung im Diebstahl von Anmeldeinformationen haben, die in Code oder andere Textquellen eingebettet sind, verringert die Erzwingung verwalteter Identitäten für den programmgesteuerten Zugriff das Risiko dieser Form von Diebstahl erheblich.
- Nutzen Sie privilegierte Identitäten für Automatisierungsrunbooks, die erhöhte Zugriffsberechtigungen erfordern. Automatisierte Workflows, die kritische Sicherheitsgrenzen verletzen, müssen mithilfe derselben Tools und Richtlinien geregelt werden, die auch für Benutzer mit gleichwertigen Berechtigungen gelten.
- Fügen Sie Azure-Ressourcenbereichen keine Benutzer direkt hinzu. Fügen Sie stattdessen Benutzer zu definierten Rollen hinzu, die dann wiederum Ressourcenbereichen zugewiesen werden. Mit direkten Benutzerzuweisungen wird eine zentralisierte Verwaltung umgangen, wodurch sich der Verwaltungsaufwand erheblich erhöht, der erforderlich ist, um unautorisierten Zugriff auf geschützte Daten zu verhindern.

### <a name="plan-for-authentication-inside-a-landing-zone"></a>Planen der Authentifizierung innerhalb einer Zielzone

Eine wichtige Entwurfsentscheidung, die eine Organisation bei der Einführung von Azure treffen muss, ist, ob die bestehende lokale Identitätsdomäne auf Azure ausgedehnt oder ob eine ganz neue Domäne eingerichtet werden soll. Authentifizierungsanforderungen innerhalb der Zielzone sollten sorgfältig bewertet und in Bereitstellungspläne für Active Directory Domain Services (AD DS) in Windows Server, für Azure AD Domain Services (Azure AD DS) oder für beide Dienste integriert werden. Die meisten Azure-Umgebungen nutzen mindestens Azure AD für die Authentifizierung bei der Azure-Fabric und lokale AD DS-Hostauthentifizierung und -Gruppenrichtlinienverwaltung.

**Überlegungen zum Entwurf:**

- Erwägen Sie zentralisierte und delegierte Zuständigkeiten für die Verwaltung innerhalb der Zielzone bereitgestellter Ressourcen.
- Anwendungen, die auf Domänendiensten beruhen und ältere Protokolle verwenden, können [Azure AD DS](/azure/active-directory-domain-services) verwenden.

**Entwurfsempfehlungen:**

- Arbeiten Sie mit zentralisierten und delegierten Zuständigkeiten für die Verwaltung innerhalb der Zielzone bereitgestellter Ressourcen basierend auf Rollen- und Sicherheitsanforderungen.
- Privilegierte Vorgänge wie die Erstellung von Dienstprinzipalobjekten, die Registrierung von Anwendungen in Azure AD und der Bezug von und der Umgang mit Zertifikaten oder Platzhalterzertifikaten erfordern besondere Genehmigungen. Berücksichtigen Sie, welche Benutzer mit solchen Anforderungen umgehen werden und wie sie ihre Konten mit der erforderlichen Sorgfalt sichern und überwachen können.
- Wenn es in einer Organisation ein Szenario gibt, in dem auf eine Anwendung mit integrierter Windows-Authentifizierung remote über Azure AD zugegriffen werden muss, sollten Sie [Azure AD-Anwendungsproxy](/azure/active-directory/manage-apps/application-proxy) verwenden.
- Es besteht ein Unterschied zwischen Azure AD, Azure AD DS und dem unter Windows Server ausgeführten Dienst AD DS. Beurteilen Sie Ihre Anwendungsbedürfnisse, und ermitteln und dokumentieren Sie den jeweils verwendeten Authentifizierungsanbieter. Planen Sie für alle Anwendungen entsprechend.
- Werten Sie die Kompatibilität von Workloads für AD DS unter Windows Server und für Azure AD DS aus.
- Stellen Sie sicher, dass Ihr Netzwerkentwurf Ressourcen, die AD DS unter Windows Server für die lokale Authentifizierung und Verwaltung benötigen, den Zugriff auf die entsprechenden Domänencontroller erlaubt.
  - Erwägen Sie für AD DS unter Windows Server Umgebungen mit gemeinsamen Diensten, die eine lokale Authentifizierung und Hostverwaltung im Kontext eines größeren unternehmensweiten Netzwerks bieten.
- Stellen Sie Azure AD DS innerhalb der primären Region bereit, da dieser Dienst nur in ein Abonnement aufgenommen werden kann.
- Nutzen Sie für die Authentifizierung bei Azure-Diensten verwaltete Identitäten anstelle von Dienstprinzipalen. Dieser Ansatz senkt das Risiko des Diebstahls von Anmeldeinformationen.
