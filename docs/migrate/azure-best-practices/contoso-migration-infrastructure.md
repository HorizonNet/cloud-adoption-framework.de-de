---
title: Bereitstellen einer Migrationsinfrastruktur
description: Erfahren Sie, wie Contoso eine Azure-Infrastruktur für die Migration zu Azure einrichtet.
author: deltadan
ms.author: abuck
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: af6ed897f86978058f83e5c6c6dc600f10fd7072
ms.sourcegitcommit: a7eb2f6c4465527cca2d479edbfc9d93d1e44bf1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94713614"
---
<!-- cSpell:ignore untrust CIDR RRAS CONTOSODC SYSVOL ITIL NSGs ASGs -->

# <a name="deploy-a-migration-infrastructure"></a>Bereitstellen einer Migrationsinfrastruktur

In diesem Artikel wird gezeigt, wie das fiktive Unternehmen Contoso seine lokale Infrastruktur für die Migration vorbereitet, eine Azure-Infrastruktur zur Vorbereitung der Migration einrichtet und sein Geschäft in einer Hybridumgebung betreibt.

Wenn Sie die Migration Ihrer Unternehmensinfrastruktur anhand dieses Beispiels planen, sollten Sie bedenken, dass die vorliegende Beispielarchitektur speziell auf Contoso ausgelegt ist. Bevor Sie wichtige Infrastrukturentscheidungen zum Abonnemententwurf oder zur Netzwerkarchitektur treffen, sollten Sie die geschäftlichen, strukturellen und technischen Anforderungen Ihrer Organisation analysieren.

Ob Sie alle in diesem Artikel beschriebenen Elemente benötigen, hängt von Ihrer Migrationsstrategie ab. Wenn Sie beispielsweise nur cloudnative Anwendungen in Azure erstellen, benötigen Sie möglicherweise eine weniger komplexe Netzwerkstruktur.

## <a name="overview"></a>Übersicht

Bevor die Migration zu Azure erfolgen kann, muss Contoso zunächst eine Azure-Infrastruktur vorbereiten. In der Regel müssen dabei sechs Aspekte berücksichtigt werden:

> [!div class="checklist"]
>
> - **Schritt 1: Azure-Abonnements.** Wie erwirbt das Unternehmen Azure, und wie erfolgt die Interaktion mit der Azure-Plattform und den Azure-Diensten?
> - **Schritt 2: Hybrididentität.** Wie wird der Zugriff auf lokale und Azure-basierte Ressourcen nach der Migration verwaltet und gesteuert? Wie wird die Identitätsverwaltung in die Cloud erweitert oder ausgelagert?
> - **Schritt 3: Notfallwiederherstellung und Ausfallsicherheit.** Wie stellt Contoso die Resilienz seiner Anwendungen und Infrastruktur bei Aus- und Notfällen sicher?
> - **Schritt 4: Netzwerk.** Wie sollte Contoso die Netzwerkinfrastruktur gestalten und das lokale Rechenzentrum mit Azure verbinden?
> - **Schritt 5: Sicherheit.** Wie wird die Hybridbereitstellung von Contoso geschützt?
> - **Schritt 6: Governance.** Wie sorgt Contoso dafür, dass die Bereitstellung die Sicherheits- und Governanceanforderungen erfüllt?

## <a name="before-you-start"></a>Vorbereitung

Bevor mit der Überprüfung der Infrastruktur begonnen wird, sollten Sie einige Hintergrundinformationen zu den relevanten Azure-Funktionen lesen:

- Für den Erwerb des Zugriffs auf Azure stehen mehrere Optionen zur Verfügung. Hierzu zählen beispielsweise Abonnements mit nutzungsbasierter Zahlung, ein Microsoft Enterprise Agreement (EA), eine Lizenzierung nach dem Open License-Verfahren von Microsoft-Handelspartnern oder der Kauf bei Microsoft-Partnern im Rahmen des CSP-Programms (Cloud Solution Provider). Erfahren Sie mehr über [Kaufoptionen](https://azure.microsoft.com/pricing/purchase-options/), und lesen Sie, wie [Azure-Abonnements organisiert sind](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise/).
- Verschaffen Sie sich einen Überblick über die [Identitäts- und Zugriffsverwaltung](https://www.microsoft.com/security/business/identity) in Azure. Informieren Sie sich über [Azure Active Directory (Azure AD) und das Erweitern einer lokalen Active Directory-Instanz in die Cloud](/azure/active-directory/fundamentals/active-directory-whatis).
- Azure bietet eine robuste Netzwerkinfrastruktur mit Optionen für Hybridverbindungen. Verschaffen Sie sich einen Überblick über [Netzwerke und Netzwerkzugriffssteuerung](/azure/security/fundamentals/network-overview).
- Lesen Sie die [Einführung in die Azure-Sicherheit](/azure/security/fundamentals/overview), und erfahren Sie, wie Sie einen Plan für [Azure Governance](/azure/governance/) erstellen.

## <a name="on-premises-architecture"></a>Lokale Architektur

Nachstehend finden Sie eine Darstellung der aktuellen lokalen Infrastruktur von Contoso.

![Diagramm: Architektur von Contoso](./media/contoso-migration-infrastructure/contoso-architecture.png)

_Abbildung 1: Lokale Architektur von Contoso_

- Contoso verfügt über ein Hauptrechenzentrum in New York City, im Osten der USA.
- Außerdem besitzt es drei weitere Zweigstellen in den USA.
- Das Hauptrechenzentrum ist über eine Metro-Ethernet-Glasfaserverbindung mit einer Kapazität von 500 MBit/s mit dem Internet verbunden.
- Jede Niederlassung ist lokal über Verbindungen auf Unternehmensniveau mit dem Internet verbunden, und IPsec-VPN-Tunnel führen zurück zum Hauptrechenzentrum. Bei diesem Ansatz ist das gesamte Netzwerk dauerhaft verbunden und die Internetverbindung optimiert.
- Das Hauptrechenzentrum ist vollständig mit VMware virtualisiert. Contoso verfügt über zwei ESXi 6.5-Virtualisierungshosts, die per vCenter Server 6.5 verwaltet werden.
- Für die Identitätsverwaltung nutzt Contoso Active Directory sowie DNS-Server im internen Netzwerk.
- Die Domänencontroller im Rechenzentrum werden auf virtuellen Computern (Virtual Machines, VMs) von VMware ausgeführt. Die Domänencontroller in lokalen Niederlassungen werden auf physischen Servern ausgeführt.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Schritt 1: Kaufen und Abonnieren von Azure

Contoso muss entscheiden, wie Azure erworben werden soll und wie Abonnements verwaltet sowie Dienste und Ressourcen lizenziert werden.

### <a name="buy-azure"></a>Kauf von Azure

Contoso registriert sich für ein [Enterprise Agreement](https://azure.microsoft.com/overview/sales-number/). Diese Vereinbarung sieht eine Vorauszahlung für Azure vor, für die Contoso Vorteile wie flexible Abrechnungsoptionen und optimierte Preise erhält.

Es folgen die Details:

- Contoso hat eine Schätzung der jährlichen Ausgaben für Azure erstellt. Bei Vertragsabschluss hat Contoso das erste Jahr vollständig bezahlt.
- Contoso muss vor Ablauf des Jahres den Mindestverbrauch nutzen, um keine bereits bezahlten Leistungen verfallen zu lassen.
- Sollte Contoso mehr als die vorab bezahlten Ressourcen verbrauchen, stellt Microsoft die Differenz in Rechnung.
- Alle jenseits der Übertragung anfallenden Kosten werden zu den vertraglich vereinbarten Preisen berechnet. Für Überschreitungen werden keine Strafen fällig.

### <a name="manage-subscriptions"></a>Verwalten von Abonnements

Nach dem Erwerb von Azure muss Contoso herausfinden, wie die Azure-Abonnements verwaltet werden sollen. Contoso verfügt über ein EA und kann somit beliebig viele Azure-Abonnements erstellen. Eine Azure Enterprise Agreement-Registrierung definiert, wie ein Unternehmen Azure-Dienste modelliert und verwendet und legt eine Kernstruktur für die Governance fest.

Als Erstes hat Contoso eine Struktur für die Registrierung definiert (ein so genanntes _Unternehmensgerüst_). Contoso hat das [Azure-Unternehmensgerüst](/azure/cloud-adoption-framework/reference/azure-scaffold) verwendet, um ein Gerüst zu entwerfen.

Für den Augenblick hat sich Contoso für eine funktionale Abonnementverwaltung entschieden:

- Das Unternehmen setzt eine zentrale IT-Abteilung ein, die auch die Kontrolle über das Azure-Budget hat. Diese Gruppe hält als einzige Abonnements.
- Contoso plant, dieses Modell später zu erweitern, sodass weitere Gruppen im Unternehmen als Abteilungen in die Registrierungshierarchie integriert werden können.
- Innerhalb der IT-Abteilung hat Contoso zwei Abonnements strukturiert: `Production` und `Development`.
- Wenn Contoso zukünftig zusätzliche Abonnements benötigt, muss das Unternehmen auch den Zugriff, die Richtlinien und die Konformität für diese Abonnements verwalten. Hierzu führt Contoso [Azure-Verwaltungsgruppen](/azure/governance/management-groups/overview) als zusätzliche Ebene über Abonnements ein.

![Diagramm: Unternehmenshierarchie](./media/contoso-migration-infrastructure/enterprise-structure.png)

_Abbildung 2: Unternehmenshierarchie_

### <a name="examine-licensing"></a>Untersuchen der Lizenzierung

Nach der Konfiguration der Abonnements kann sich Contoso mit der Microsoft-Lizenzierung befassen. Die Lizenzierungsstrategie hängt von den Ressourcen ab, die Contoso zu Azure migrieren möchte, sowie davon, wie virtuelle Computer und Dienste ausgewählt und in Azure bereitgestellt werden.

#### <a name="azure-hybrid-benefit"></a>Azure-Hybridvorteil

Standardimages von in Azure bereitgestellten VMs beinhalten eine Lizenz, und die Softwarenutzung wird Contoso pro Minute in Rechnung gestellt. Contoso ist jedoch seit langem Microsoft-Kunde und hat EAs und Lizenzen im Open License-Programm mit Software Assurance genutzt.

Der Azure-Hybridvorteil stellt eine kostengünstige Migrationsmethode dar. Er ermöglicht Contoso Einsparungen bei Azure-VMs und SQL Server-Workloads durch Umwandlung oder Wiederverwendung von Lizenzen der Windows Server Datacenter- und Standard-Editionen, die durch die Software Assurance (SA) abgedeckt sind. Dadurch kann Contoso einen niedriger angesetzten Computesatz für VMs und SQL Server bezahlen. Weitere Informationen finden Sie unter [Azure-Hybridvorteil](https://azure.microsoft.com/pricing/hybrid-benefit/).

#### <a name="license-mobility"></a>Lizenzmobilität

License Mobility durch Software Assurance bietet Kunden wie Contoso, die einen Microsoft-Volumenlizenzvertrag abgeschlossen haben, die Flexibilität, qualifizierte Serveranwendungen mit aktiver SA in Azure bereitzustellen. Hierdurch entfällt die Notwendigkeit zum Kauf neuer Lizenzen. Ohne anfallende Mobilitätsgebühren können die vorhandenen Lizenzen auf einfache Weise in Azure bereitgestellt werden. Weitere Informationen finden Sie unter [Lizenzmobilität durch Software Assurance für Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="reserved-instances-for-predictable-workloads"></a>Reservierte Instanzen für vorhersehbare Workloads

Vorhersehbare Workloads müssen bei ausgeführten VMs jederzeit verfügbar sein. Hierzu zählen beispielsweise Branchenanwendungen wie etwa ein SAP-ERP-System. Bei unvorhersehbaren Workloads handelt es sich um variable Workloads wie etwa VMs, die bei hoher Nachfrage gestartet und bei geringer Nachfrage heruntergefahren werden.

![Diagramm: reservierte Azure-VM-Instanzen](./media/contoso-migration-infrastructure/reserved-instance.png)

_Abbildung 3: Azure Reserved Virtual Machine Instances_

Für die Verwendung reservierter Instanzen für bestimmte VM-Instanzen, die über längere Zeiträume hinweg benötigt werden, kann Contoso im Gegenzug sowohl einen Rabatt als auch priorisierte Kapazität erhalten. Durch die Verwendung von [Azure Reserved Virtual Machine Instances](https://azure.microsoft.com/pricing/reserved-vm-instances/) in Kombination mit dem Azure-Hybridvorteil kann Contoso gegenüber der regulären nutzungsbasierten Bezahlung bis zu 82 Prozent sparen (Stand April 2018).

## <a name="step-2-manage-hybrid-identity"></a>Schritt 2: Verwalten von Hybrididentitäten

Das Erteilen und Steuern des Benutzerzugriffs auf Azure-Ressourcen mithilfe der Identitäts- und Zugriffsverwaltung ist ein wichtiger Schritt bei der Erstellung einer Azure-Infrastruktur.

Contoso hat sich entschieden, das vorhandene lokale Active Directory in die Cloud zu erweitern, statt ein neues, separates System in Azure aufzubauen. Da Contoso noch nicht Microsoft 365 verwendet, muss eine Azure AD-Instanz bereitgestellt werden. Mit Microsoft 365 würde Contoso bereits über einen Azure AD-Mandanten sowie über ein entsprechendes Verzeichnis verfügen, das als primäre Azure AD-Instanz verwendet werden könnte.

Weitere Informationen zu Identitätsmodellen von Microsoft 365 und zu Azure Active Directory finden Sie [hier](/microsoft-365/enterprise/about-microsoft-365-identity?view=o365-worldwide). Informationen zum Zuordnen oder Hinzufügen eines Azure-Abonnements zu Ihrem Azure Active Directory-Mandanten finden Sie [hier](/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory).

### <a name="create-an-azure-ad-directory"></a>Erstellen eines Azure AD-Verzeichnisses

Contoso verwendet die Azure AD Free-Edition, die in Azure-Abonnements enthalten ist. Die Administratoren von Contoso erstellen ein Azure AD-Verzeichnis:

1. Im [Azure-Portal](https://portal.azure.com) navigieren sie zu **Ressource erstellen** > **Identität** > **Azure Active Directory**.

1. Sie geben in **Verzeichnis erstellen** einen Namen für das Verzeichnis, einen Anfangsdomänennamen und die Region an, in der das Verzeichnis erstellt werden soll.

   ![Screenshot: Auswahloptionen für das Erstellen eines Azure AD-Verzeichnisses](./media/contoso-migration-infrastructure/azure-ad-create.png)

   _Abbildung 4: Erstellen eines Azure AD-Verzeichnisses_

> [!NOTE]
> Das erstellte Verzeichnis hat zunächst einen Domänennamen im Format `domain-name.onmicrosoft.com`. Der Name kann weder geändert noch gelöscht werden. Stattdessen müssen die Administratoren den registrierten Domänenname zu Azure AD hinzufügen.

### <a name="add-the-domain-name"></a>Hinzufügen des Domänennamens

Die Administratoren bei Contoso müssen den Standarddomänennamen als benutzerdefinierten Domänennamen zu Azure AD hinzufügen, um diesen verwenden zu können. Diese Option ermöglicht es ihnen, vertraute Benutzernamen zuzuweisen. Beispielsweise kann sich ein Benutzer mit der E-Mail-Adresse `billg@contoso.com`, anstelle von `billg@contosomigration.onmicrosoft.com` anmelden.

Für die Einrichtung eines benutzerdefinierten Domänennamens müssen die Administratoren den Namen zum Verzeichnis hinzufügen, einen DNS-Eintrag einfügen und den Namen in Azure AD bestätigen.

1. Sie fügen die Domäne unter **Benutzerdefinierte Domänennamen** > **Benutzerdefinierte Domäne hinzufügen** hinzu.
2. Damit ein DNS-Eintrag in Azure verwendet werden kann, müssen sie ihn bei ihrer Domänenregistrierungsstelle registrieren:

    - Sie notieren sich in der Liste **Benutzerdefinierte Domänennamen** die DNS-Informationen zu dem Namen. Das Unternehmen verwendet einen MX-Eintrag.
    - Die Administratoren benötigen Zugriff auf den Namenserver. Sie melden sich bei der Domäne `contoso.com` an und erstellen mithilfe der notierten Informationen einen neuen MX-Eintrag für den von Azure AD bereitgestellten DNS-Eintrag.

3. Nachdem die DNS-Einträge weitergegeben wurden, klicken sie in den Domänendetails auf **Überprüfen**, um den benutzerdefinierten Domänennamen zu überprüfen.

    ![Screenshot: Auswahl für das Azure Active Directory-DNS](./media/contoso-migration-infrastructure/azure-ad-dns.png)

    _Abbildung 5: Überprüfen des Domänennamens_

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Einrichten von Gruppen und Benutzern lokal und in Azure

Nachdem das Azure AD-Verzeichnis nun eingerichtet ist, müssen die Administratoren von Contoso Mitarbeiter den lokalen Active Directory-Gruppen hinzufügen, die mit Azure AD synchronisiert werden sollen. Dabei empfiehlt es sich, lokale Gruppennamen zu verwenden, die mit den Namen von Ressourcengruppen in Azure übereinstimmen. Dies erleichtert die Identifikation von Übereinstimmungen zu Synchronisierungszwecken.

#### <a name="create-resource-groups-in-azure"></a>Erstellen von Ressourcengruppen in Azure

Azure-Ressourcengruppen fassen Azure-Ressourcen zu Gruppen zusammen. Mithilfe einer Ressourcengruppen-ID kann Azure Vorgänge für Ressourcen in der betreffenden Gruppe ausführen.

Ein Azure-Abonnement kann mehrere Ressourcengruppen enthalten. Eine Ressourcengruppe ist nur in einem Abonnement vorhanden. Außerdem kann eine einzelne Ressourcengruppe über mehrere Ressourcen verfügen. Eine Ressource gehört jeweils nur einer Ressourcengruppe an.

Die Administratoren von Contoso richten Azure-Ressourcengruppen wie in der folgenden Tabelle gezeigt ein.

| Resource group | Details |
| --- | --- |
| `ContosoCobRG` | Diese Gruppe enthält alle Ressourcen, die mit der Geschäftskontinuität zusammenhängen. Sie enthält Tresore, die Contoso für die Dienste „Azure Site Recovery“ und „Azure Backup“ verwenden wird. <br><br> Darüber hinaus enthält sie Ressourcen, die für die Migration verwendet werden, darunter Azure Migrate und Azure Database Migration Service. |
| `ContosoDevRG` | Diese Gruppe enthält Entwicklungs-/Testressourcen. |
| `ContosoFailoverRG` | Diese Gruppe dient als Zielzone für Failoverressourcen. |
| `ContosoNetworkingRG` | Diese Gruppe enthält alle Netzwerkressourcen. |
| `ContosoRG` | Diese Gruppe enthält Ressourcen im Zusammenhang mit Produktionsanwendungen und -datenbanken. |

Die Ressourcengruppen werden in folgender Weise erstellt:

1. Sie fügen im Azure-Portal > **Ressourcengruppen** eine Gruppe hinzu.
2. Sie geben für jede Gruppe einen Namen, das Abonnement, zu dem die Gruppe gehört und die Region an.
3. Ressourcengruppen werden in der Liste **Ressourcengruppen** angezeigt.

   ![Screenshot: Liste der Ressourcengruppen](./media/contoso-migration-infrastructure/resource-groups.png)

   _Abbildung 6: Ressourcengruppen_

##### <a name="scale-resource-groups"></a>Skalieren von Ressourcengruppen

Contoso fügt später bei Bedarf weitere Ressourcengruppen hinzu. Das Unternehmen kann beispielsweise für jede Anwendung oder jeden Dienst eine Ressourcengruppe definieren, damit Anwendungen bzw. Dienste unabhängig voneinander verwaltet und geschützt werden können.

#### <a name="create-matching-security-groups-on-premises"></a>Erstellen von übereinstimmenden lokalen Sicherheitsgruppen

In der lokalen Active Directory-Instanz richten die Administratoren von Contoso Sicherheitsgruppen ein, deren Namen mit den Namen der Azure-Ressourcengruppen übereinstimmen.

![Screenshot: lokale Active Directory-Sicherheitsgruppen](./media/contoso-migration-infrastructure/on-premises-ad.png)

_Abbildung 7: Lokale Active Directory-Sicherheitsgruppen_

Zu Verwaltungszwecken erstellen sie eine zusätzliche Gruppe, die allen anderen Gruppen hinzugefügt wird. Dieser Gruppe werden Rechte an allen Ressourcengruppen in Azure erteilt. Der Gruppe wird eine begrenzte Anzahl von globalen Administratoren hinzugefügt.

### <a name="synchronize-active-directory"></a>Synchronisieren von Active Directory

Contoso möchte eine gemeinsame Identität für den Zugriff auf lokale Ressourcen und Ressourcen in der Cloud bereitstellen. Zu diesem Zweck integriert das Unternehmen die lokale Active Directory-Instanz mit Azure AD. Mit diesem Modell können Benutzer und Organisationen eine einzelne Identität für den Zugriff auf lokale Anwendungen und Clouddienste wie Microsoft 365 oder Tausende weitere Websites im Internet nutzen. Administratoren können mithilfe der Gruppen in Active Directory die [rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC)](/azure/role-based-access-control/role-assignments-portal) in Azure implementieren.

Um die Integration zu erleichtern, verwendet Contoso das [Azure AD Connect-Tool](/azure/active-directory/hybrid/whatis-hybrid-identity). Nach der Installation und Konfiguration auf einem Domänencontroller synchronisiert das Tool die lokalen Active Directory-Identitäten mit Azure AD.

### <a name="download-the-tool"></a>Herunterladen des Tools

1. Im Azure-Portal navigieren die Administratoren von Contoso zu **Azure Active Directory** > **Azure AD Connect** und laden die neueste Version des Tools auf den Server herunter, der für die Synchronisierung verwendet werden soll.

    ![Screenshot: Downloadlink für Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

    _Abbildung 8: Herunterladen von Azure AD Connect_

2. Die Administratoren starten die Installation von `AzureADConnect.msi` über die **Express-Einstellungen**. Dies ist die gebräuchlichste Installation, die für Topologien mit einer einzelnen Gesamtstruktur und mit Synchronisierung von Kennworthashes zur Authentifizierung verwendet werden kann.

    ![Screenshot: Azure AD Connect-Assistent](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

    _Abbildung 9: Azure AD Connect-Assistent_

3. In **Mit Azure AD verbinden** geben sie die Anmeldeinformationen für die Verbindungsherstellung mit Azure AD an (im Format `admin@contoso.com` oder `admin@contoso.onmicrosoft.com`).

    ![Screenshot: Seite „Mit Azure AD verbinden“ im Azure AD Connect-Assistenten](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

    _Abbildung 10: Azure AD Connect-Assistent: Mit Azure AD verbinden_

4. Unter **Mit AD DS verbinden** geben sie Anmeldeinformationen für das lokale Verzeichnis an (im Format `CONTOSO\admin` oder `contoso.com\admin`).

    ![Screenshot: Seite „Mit AD DS verbinden“ im Azure AD Connect-Assistenten](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

    _Abbildung 11: Azure AD Connect-Assistent: Herstellen einer Verbindung mit AD DS_

5. In **Bereit zur Konfiguration** wählen sie **Starten Sie den Synchronisierungsvorgang, nachdem die Konfiguration abgeschlossen wurde** aus, um die Synchronisierung sofort zu starten. Anschließend führen sie die Installation durch.

    Beachten Sie Folgendes:

    - Contoso hat eine direkte Verbindung mit Azure. Wenn sich Ihre lokale Active Directory-Instanz hinter einem Proxy befindet, sollten Sie den Artikel [Problembehebung bei Azure AD-Konnektivitätsproblemen](/azure/active-directory/hybrid/tshoot-connect-connectivity) lesen.

    - Nach der ersten Synchronisierung werden lokale Active Directory-Objekte im Azure AD-Verzeichnis sichtbar.

      ![Screenshot: lokale, in Azure Active Directory sichtbare Active Directory-Objekte](./media/contoso-migration-infrastructure/on-premises-ad-groups.png)

      _Abbildung 12: Lokale, in Azure AD sichtbare Active Directory-Objekte_

    - Das IT-Team von Contoso ist in jeder Gruppe vertreten (basierend auf der jeweiligen Rolle).

      ![Screenshot: Gruppenmitgliedschaft](./media/contoso-migration-infrastructure/on-premises-ad-group-members.png)

      _Abbildung 13: Gruppenmitgliedschaft_

### <a name="set-up-rbac"></a>Einrichten von RBAC

Azure [RBAC](/azure/role-based-access-control/role-assignments-portal) ermöglicht eine differenzierte Zugriffsverwaltung für Azure. Mit der RBAC können Sie den Benutzern genau die Zugriffsrechte gewähren, die diese zum Ausführen von Aufgaben benötigen. Sie weisen Benutzern, Gruppen und Anwendungen auf Bereichsebene eine passende RBAC-Rolle zu. Der Bereich einer Rollenzuweisung kann ein Abonnement, eine Ressourcengruppe oder eine einzelne Ressource sein.

Als Nächstes weisen die Administratoren von Contoso den Active Directory-Gruppen, die aus der lokalen Infrastruktur synchronisiert wurden, Rollen zu.

1. In der Ressourcengruppe `ControlCobRG` wählen sie **Zugriffssteuerung (IAM)**  > **Rollenzuweisung hinzufügen** aus.
2. Unter **Rollenzuweisung hinzufügen** > **Rolle** > **Mitwirkender** wählen sie in der Liste die Sicherheitsgruppe `ContosoCobRG` aus. Die Gruppe wird dann in der Liste **Ausgewählte Mitglieder** angezeigt.
3. Sie wiederholen diesen Schritt mit den gleichen Berechtigungen für die anderen Ressourcengruppen (mit Ausnahme von `ContosoAzureAdmins`), indem sie der Sicherheitsgruppe, die der Ressourcengruppe entspricht, Berechtigungen vom Typ **Mitwirkender** erteilen.
4. Der Sicherheitsgruppe `ContosoAzureAdmins` weisen sie die Rolle **Besitzer** zu.

    ![Screenshot: lokale Azure Active Directory-Gruppen](./media/contoso-migration-infrastructure/on-premises-ad-groups.png)

    _Abbildung 14: Zuweisen von Rollen zu Sicherheitsgruppen_

## <a name="step-3-design-for-resiliency"></a>Schritt 3: Entwurf mit Blick auf Resilienz

### <a name="set-up-regions"></a>Einrichten von Regionen

Azure-Ressourcen werden in Regionen bereitgestellt. Regionen sind wiederum in Geografien unterteilt. Anforderungen an Data Residency sowie Datenhoheit, -konformität und -resilienz werden innerhalb der geografischen Grenzen erfüllt.

Eine Region besteht aus mehreren Rechenzentren. Diese Rechenzentren werden innerhalb eines durch Latenz definierten Umkreises bereitgestellt und sind über ein dediziertes regionales Netzwerk mit geringer Latenz verbunden.

Jede Azure-Region ist zwecks Ausfallsicherheit mit einer anderen Region gepaart. Lesen Sie mehr über [Azure-Regionen](https://azure.microsoft.com/global-infrastructure/geographies/), und verstehen Sie, [wie Regionen gepaart werden](/azure/best-practices-availability-paired-regions).

Contoso hat sich aus den folgenden Gründen für `East US 2` (mit Standort in Virginia) als primäre Region und für `Central US` (mit Standort in Iowa) als sekundäre Region entschieden:

- Das Contoso-Rechenzentrum befindet sich in New York, und die Latenz zum nächstgelegenen Rechenzentrum wurde berücksichtigt.
- `East US 2` bietet alle Dienste und Produkte, die Contoso benötigt. Es sind nicht in allen Azure-Regionen dieselben Produkte und Dienste verfügbar. Weitere Informationen finden Sie unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services/).
- `Central US` ist die gepaarte Region für `East US 2` in Azure.

Bei der Planung der Hybridumgebung muss sich Contoso überlegen, wie Ausfallsicherheit und eine Strategie zur Notfallwiederherstellung im Regionsentwurf verwirklicht werden können. Die einfachste Lösung ist eine Bereitstellung in einer einzelnen Region, in der Resilienz mit Azure-Plattformfeatures wie Fehlerdomänen und Regionspaaren gewährleistet wird. Die komplizierteste Lösung wäre eine vollständige Aktiv/Aktiv-Architektur, in der die Clouddienste und die Datenbank in zwei unterschiedlichen Regionen bereitgestellt und von dort aus an Benutzer ausgeliefert werden.

Contoso hat sich für einen Mittelweg entschieden. Das Unternehmen wird Anwendungen und Ressourcen in einer primären Region bereitstellen und eine vollständige Kopie der Infrastruktur in der sekundären Region speichern. Auf diese Weise kann die Kopie eines vollständigen Anwendungsausfalls oder eines regionalen Fehlers als vollständige Sicherung fungieren.

### <a name="set-up-availability"></a>Einrichten von Verfügbarkeit

#### <a name="availability-sets"></a>Verfügbarkeitsgruppen

Verfügbarkeitsgruppen dienen zum Schutz von Anwendungen und Daten bei einem lokalen Hardware- und Netzwerkausfall in einem Rechenzentrum. Verfügbarkeitsgruppen verteilen Azure-VMs auf verschiedene physische Hardwaregeräte innerhalb eines Rechenzentrums.

Fehlerdomänen stellen zugrundeliegende Hardware mit einer gemeinsamen Stromquelle und einem gemeinsamen Netzwerkswitch im Rechenzentrum dar. VMs in einer Verfügbarkeitsgruppe sind über verschiedene Fehlerdomänen verteilt, um Ausfälle aufgrund eines einzelnen Hardware- oder Netzwerkfehlers zu minimieren.

Updatedomänen stellen zugrunde liegende Hardware dar, die gleichzeitig gewartet oder neu gestartet werden kann. Mithilfe von Verfügbarkeitsgruppen werden VMs auch auf mehrere Updatedomänen verteilt. So kann sichergestellt werden, dass mindestens eine Instanz ununterbrochen ausgeführt wird.

Contoso wird Verfügbarkeitsgruppen immer dann implementieren, wenn VM-Workloads Hochverfügbarkeit erfordern. Weitere Informationen finden Sie unter [Verwalten der Verfügbarkeit virtueller Windows-Computer in Azure](/azure/virtual-machines/manage-availability).

#### <a name="availability-zones"></a>Verfügbarkeitszonen

Verfügbarkeitszonen tragen dazu bei, Anwendungen und Daten vor Fehlern zu schützen, die ein gesamtes Rechenzentrum innerhalb einer Region betreffen.

Jede Verfügbarkeitszone stellt einen individuellen physischen Standort in einer Azure-Region dar. Jede Zone besteht aus mindestens einem Datencenter mit eigener Stromversorgung, Kühlung und Netzwerk.

In allen aktivierten Regionen sind mindestens drei separate Zonen vorhanden. Die physische Trennung der Zonen innerhalb einer Region schützt Anwendungen und Daten vor Datencenterausfällen.

Contoso nutzt Verfügbarkeitszonen für Anwendungen mit höheren Anforderungen in puncto Skalierbarkeit, Verfügbarkeit und Resilienz. Weitere Informationen finden Sie unter [Regionen und Verfügbarkeitszonen in Azure](/azure/availability-zones/az-overview).

### <a name="configure-backup"></a>Konfigurieren der Sicherung

#### <a name="azure-backup"></a>Azure Backup

Mithilfe von Azure Backup können Sie Azure VM-Datenträger sichern und wiederherstellen.

Azure Backup ermöglicht automatisierte Sicherungen von VM-Datenträgerimages in Azure Storage. Sicherungen sind anwendungskonsistent. Dadurch wird sichergestellt, dass gesicherte Daten transaktionskonsistent sind und Anwendungen nach der Wiederherstellung gestartet werden können.

Azure Backup unterstützt lokal redundanten Speicher (LRS), um für den Fall eines lokalen Hardwarefehlers mehrere Kopien Ihrer Sicherungsdaten in einem Rechenzentrum replizieren zu können. Bei einem regionalen Ausfall unterstützt Azure Backup auch georedundanten Speicher (GRS). Bei diesem Speichermodus werden Ihre Sicherungsdaten in eine sekundäre gekoppelte Region repliziert.

Azure Backup verschlüsselt Daten bei der Übertragung mit AES-256. Gesicherte ruhende Daten werden mit der [Azure Storage-Verschlüsselung](/azure/storage/common/storage-service-encryption) verschlüsselt.

Contoso verwendet Azure Backup mit GRS auf allen Produktions-VMs, um sicherzustellen, dass die Workloaddaten gesichert werden und sich im Fall einer Unterbrechung schnell wiederherstellen lassen. Weitere Informationen finden Sie unter [Ein Überblick über die Sicherung von Azure-VMs](/azure/backup/backup-azure-vms-introduction).

### <a name="set-up-disaster-recovery"></a>Einrichten der Notfallwiederherstellung

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery sorgt dafür, dass geschäftliche Anwendungen und Workloads während regionaler Ausfälle weiter ausgeführt werden, und trägt so zur Aufrechterhaltung der Geschäftskontinuität bei.

Azure Site Recovery repliziert Azure-VMs ständig von einer primären in eine sekundäre Region und sorgt damit für funktionale Kopien an beiden Standorten. Bei einem Ausfall in der primären Region führt Ihre Anwendung oder Ihr Dienst ein Failover auf die in der sekundären Region replizierten VM-Instanzen aus. Dieses Failover minimiert mögliche Unterbrechungen. Wenn Vorgänge zum normalen Betrieb zurückkehren, kann für Ihre Anwendungen oder Dienste ein Failback zu den VMs in der primären Region ausgeführt werden.

Contoso implementiert [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) für alle Produktions-VMs, die in geschäftskritischen Workloads verwendet werden, und stellt so sicher, dass es während eines Ausfalls in der primären Region nur zu einer minimalen Unterbrechung kommt.

## <a name="step-4-design-a-network-infrastructure"></a>Schritt 4: Entwerfen einer Netzwerkinfrastruktur

Nach der Ausarbeitung des Regionskonzepts kann sich Contoso der Netzwerkstrategie zuwenden. Das Unternehmen muss sich überlegen, wie das lokale Rechenzentrum und Azure miteinander verbunden werden und miteinander kommunizieren sollen und wie die Netzwerkinfrastruktur in Azure gestaltet werden soll. Dazu muss Contoso folgende Schritte ausführen:

- **Planen der Hybridnetzwerk-Konnektivität.** Contoso muss sich überlegen, wie netzwerkübergreifende Verbindungen zwischen der lokalen Umgebung und Azure hergestellt werden sollen.
- **Entwerfen einer Azure-Netzwerkinfrastruktur.** Contoso muss entscheiden, wie Netzwerke über Regionen hinweg bereitgestellt werden sollen. Wie kommunizieren die Netzwerke innerhalb der gleichen Region und regionsübergreifend?
- **Entwerfen und Einrichten von Azure-Netzwerken.** Contoso muss Azure-Netzwerke und Subnetze einrichten und entscheiden, was darin gespeichert werden soll.

### <a name="plan-hybrid-network-connectivity"></a>Planen der Hybridnetzwerk-Konnektivität

Contoso hat [verschiedene Architekturen für das Hybridnetzwerk](/azure/architecture/reference-architectures/hybrid-networking/) zwischen Azure und dem lokalen Rechenzentrum in Erwägung gezogen. Weitere Informationen finden Sie unter [Auswählen einer Lösung zum Herstellen einer Verbindung zwischen einem lokalen Netzwerk und Azure](/azure/architecture/reference-architectures/hybrid-networking/).

Zur Erinnerung: Die lokale Netzwerkinfrastruktur von Contoso besteht zurzeit aus dem Rechenzentrum in New York und lokalen Niederlassungen im Osten der USA. Alle Standorte verfügen über eine Internetverbindung auf Unternehmensniveau. Jede dieser Niederlassungen ist mit dem Rechenzentrum durch einen IPsec-VPN-Tunnel über das Internet verbunden.

![Diagramm: das Netzwerk von Contoso](./media/contoso-migration-infrastructure/contoso-networking.png)

_Abbildung 15: Das Netzwerk von Contoso_

Hier sehen Sie, für welche Implementierung von Hybridkonnektivität sich Contoso entschieden hat:

1. Einrichtung einer neuen Site-to-Site-VPN-Verbindung zwischen dem Contoso-Rechenzentrum in New York und den beiden Azure-Regionen `East US 2` und `Central US`
2. Datenverkehr aus den Niederlassungen, die virtuelle Netzwerke in Azure als Ziel haben, wird durch das Contoso-Hauptrechenzentrum geleitet.
3. Beim Hochskalieren der Azure-Bereitstellung richtet Contoso eine Azure ExpressRoute-Verbindung zwischen dem Rechenzentrum und den Azure-Regionen ein. Contoso behält die Site-to-Site-VPN-Verbindung dann nur noch für Failoverzwecke bei.
    - Erfahren Sie mehr über die [Wahl zwischen einer VPN- und einer ExpressRoute-Hybridlösung](/azure/architecture/reference-architectures/hybrid-networking/).
    - Überprüfen Sie [ExpressRoute-Standorte und -Unterstützung](/azure/expressroute/expressroute-locations-providers).

**Nur VPN:**

![Screenshot: VPN-Verbindung von Contoso](./media/contoso-migration-infrastructure/hybrid-vpn.png)

_Abbildung 16: Das VPN von Contoso_

**VPN und ExpressRoute:**

![Screenshot: VPN- und ExpressRoute-Verbindung von Contoso](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

_Abbildung 17: Contoso-VPN und ExpressRoute_

### <a name="design-the-azure-network-infrastructure"></a>Entwerfen der Azure-Netzwerkinfrastruktur

Die Netzwerkkonfiguration von Contoso muss die Hybrid-Bereitstellung sicher und skalierbar gestalten. Hierfür wählt Contoso einen langfristigen Ansatz und entwirft virtuelle Netzwerke mit dem Augenmerk auf Ausfallsicherheit und Unternehmenstauglichkeit. Weitere Informationen finden Sie unter [Planen virtueller Netzwerke](/azure/virtual-network/virtual-network-vnet-plan-design-arm).

Zur Verbindung der beiden Regionen implementiert Contoso ein Hub-zu-Hub-Netzwerkmodell. Innerhalb der einzelnen Regionen verwendet Contoso ein Hub-and-Spoke-Modell (Nabe und Speiche). Zum Verbinden von Netzwerken und Hubs verwendet Contoso Azure-Netzwerkpeering.

#### <a name="network-peering"></a>Netzwerkpeering

Das [Peering virtueller Netzwerke](/azure/virtual-network/virtual-network-peering-overview) in Azure dient zur Verbindung von virtuellen Netzwerken und Hubs. Globales Peering ermöglicht Verbindungen zwischen virtuellen Netzwerken und Hubs in verschiedenen Regionen. Das lokale Peering erstellt virtuelle Netzwerke in derselben Region.

Das virtuelle Netzwerkpeering bietet mehrere Vorteile:

- Netzwerkdatenverkehr zwischen virtuellen Netzwerken, die mittels Peering verknüpft sind, ist privat.
- Datenverkehr zwischen den virtuellen Netzwerken bleibt innerhalb des Microsoft-Backbone-Netzwerks. Die Kommunikation zwischen den virtuellen Netzwerken kommt ohne öffentliches Internet, Gateways oder Verschlüsselung aus.
- Standardverbindungen mit hoher Bandbreite und geringer Latenz werden mithilfe von Peering zwischen Ressourcen in unterschiedlichen virtuellen Netzwerken hergestellt.

#### <a name="hub-to-hub-model-across-regions"></a>Regionsübergreifendes Hub-zu-Hub-Modell

Contoso wird einen Hub in jeder Region bereitstellen. Bei einem Hub handelt es sich um ein virtuelles Netzwerk in Azure, das als zentraler Konnektivitätspunkt für Ihr lokales Netzwerk fungiert. Verbindungen zwischen den virtuellen Hubnetzwerken werden mithilfe des globalen Peerings für virtuelle Netzwerke in verschiedenen Azure-Regionen erstellt. Der Hub in jeder Region ist mittels Peering mit seinem Partnerhub in der anderen Region verbunden. Der Hub ist mittels Peering mit jedem Netzwerk in seiner Region verbunden und kann Verbindungen mit allen Netzwerkressourcen herstellen.

![Diagramm: globales Peering](./media/contoso-migration-infrastructure/global-peering.png)

_Abbildung 18: Globales Peering_

#### <a name="hub-and-spoke-model-within-a-region"></a>Hub-Spoke-Modell innerhalb einer Region

Innerhalb der einzelnen Regionen stellt Contoso virtuelle Netzwerke, die verschiedenen Zwecken dienen, in Form von Spokenetzwerken über den Regionshub bereit. Virtuelle Netzwerke innerhalb einer Region verwenden Peering, um eine Verbindung mit dem Hub sowie untereinander herzustellen.

#### <a name="design-the-hub-network"></a>Entwerfen des Hubnetzwerks

Für das Hub-Spoke-Modell von Contoso muss noch festgelegt werden, wie Datenverkehr aus dem lokalen Rechenzentrum und aus dem Internet weitergeleitet werden soll. Das Unternehmen hat sich in Bezug auf die Hubs `East US 2` und `Central US` für folgende Routinglösung entschieden:

- Contoso entwirft ein Netzwerk, das Datenverkehr aus dem Internet sowie aus dem Unternehmensnetzwerk über eine VPN-Verbindung zu Azure zulässt.
- Die Netzwerkarchitektur hat zwei Grenzen: eine nicht vertrauenswürdige Front-End-Umkreiszone und eine vertrauenswürdige Back-End-Zone.
- Eine Firewall weist einen Netzwerkadapter in jeder Zone auf und kontrolliert den Zugriff auf die vertrauenswürdigen Zonen.
- Aus dem Internet:
  - Datenverkehr aus dem Internet trifft auf eine öffentliche IP-Adresse mit Lastenausgleich im Umkreisnetzwerk.
  - Dieser Datenverkehr wird durch die Firewall geleitet und unterliegt Firewallregeln.
  - Nachdem die Netzwerk-Zugangskontrollen implementiert sind, wird der Verkehr an den entsprechenden Ort in der vertrauenswürdigen Zone weitergeleitet.
  - Aus dem virtuellen Netzwerk ausgehender Datenverkehr wird über benutzerdefinierte Routen an das Internet weitergeleitet. Der Datenverkehr durchläuft zwangsläufig die Firewall und wird auf Einhaltung der Contoso-Richtlinien geprüft.
- Aus dem Contoso-Rechenzentrum:
  - Eingehender Datenverkehr über Site-to-Site-VPN oder ExpressRoute trifft auf die öffentliche IP-Adresse des Azure-VPN-Gateways.
  - Der Datenverkehr wird durch die Firewall geroutet und unterliegt den Firewallregeln.
  - Nach dem Anwenden von Firewallregeln wird der Datenverkehr an einen internen Lastenausgleich (Standard-SKU) im vertrauenswürdigen Subnetz der internen Zone weitergeleitet.
  - Aus dem vertrauenswürdigen Subnetz ausgehender Datenverkehr, der über VPN an das lokale Rechenzentrum gesendet wird, wird über die Firewall weitergeleitet. Die Regeln werden angewendet, bevor der Datenverkehr über die Site-to-Site-VPN-Verbindung übertragen wird.

### <a name="design-and-set-up-azure-networks"></a>Entwerfen und Einrichten von Azure-Netzwerken

Nach der Einrichtung der Netzwerk- und Routingtopologie ist Contoso jetzt bereit für die Einrichtung von Azure-Netzwerken und -Subnetzen:

<!-- docutune:casing "class-A" "class-B" -->

- Contoso implementiert ein privates Netzwerk der Klasse A in Azure (`10.0.0.0/8`). Dies funktioniert aufgrund des lokalen Rechenzentrums, denn es verfügt zurzeit über einen privaten Adressraum der Klasse B (`172.160.0.0/16`). Das Unternehmen kann sicher sein, dass es keine Überschneidung zwischen Adressbereichen gibt.
- Contoso stellt virtuelle Netzwerke sowohl in der primären als auch in der sekundären Region bereit.
- Dabei verwendet Contoso eine Namenskonvention mit dem Präfix `VNET` und der Regionsabkürzung `EUS2` oder `CUS`. Bei diesem Standard erhalten die Hubnetzwerke die Namen `VNET-HUB-EUS2` (in der Region `East US 2`) und `VNET-HUB-CUS` (in der Region `Central US`).

#### <a name="virtual-networks-in-east-us-2"></a>Virtuelle Netzwerke in `East US 2`

`East US 2` ist die primäre Region, die Contoso zum Bereitstellen von Ressourcen und Diensten verwenden wird. Contoso entwirft Netzwerke in dieser Region auf folgende Weise:

- **Hub:** Das virtuelle Hubnetzwerk in `East US 2` gilt als primäre Verbindung zum lokalen Rechenzentrum.

- **Virtuelle Netzwerke:** Mithilfe der virtuellen Spokenetzwerke in `East US 2` können bei Bedarf Workloads isoliert werden. Neben dem virtuellen Hubnetzwerk richtet Contoso zwei virtuelle Spokenetzwerke in `East US 2` ein:

  - `VNET-DEV-EUS2`. Dieses virtuelle Netzwerk dient als voll funktionsfähiges Netzwerk für Entwicklungsprojekte des Dev/Test-Teams. Es soll als Pilotbereich für die Produktion fungieren und baut in seiner Funktion auf der Produktionsinfrastruktur auf.

  - `VNET-PROD-EUS2`. Azure-IaaS-Produktionskomponenten befinden sich in diesem Netzwerk.

  Jedes virtuelle Netzwerk verfügt über einen eigenen, eindeutigen Adressraum ohne Überlappung. Das Ziel ist es, das Routing ohne Netzwerkadressenübersetzung (Network Address Translation, NAT) zu konfigurieren.

- **Subnetze:** Jedes Netzwerk enthält jeweils ein Subnetz für die einzelnen Logikschichten. Für jedes Subnetz im Produktionsnetzwerk ist ein entsprechendes Subnetz im virtuellen Entwicklungsnetzwerk vorhanden. Darüber hinaus enthält das Produktionsnetzwerk ein Subnetz für Domänencontroller.

In der folgenden Tabelle werden die virtuellen Netzwerke in `East US 2` zusammengefasst.

| Virtuelles Netzwerk | Range | Peer |
| --- | --- | --- |
| `VNET-HUB-EUS2` | `10.240.0.0/20` | `VNET-HUB-CUS2`, `VNET-DEV-EUS2`, `VNET-PROD-EUS2` |
| `VNET-DEV-EUS2` | `10.245.16.0/20` | `VNET-HUB-EUS2` |
| `VNET-PROD-EUS2` | `10.245.32.0/20` | `VNET-HUB-EUS2`, `VNET-PROD-CUS` |

![Diagramm: Hub-Spoke-Modell in der primären Region](./media/contoso-migration-infrastructure/primary-hub-peer.png)

_Abbildung 19: Ein Hub-and-Spoke-Modell_

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Subnetze im Hub-Netzwerk `East US 2 Hub` (`VNET-HUB-EUS2`)

| Subnetz/Zone | CIDR | Verwendbare IP-Adressen |
| --- | --- | --- |
| `IB-UntrustZone` | `10.240.0.0/24`  | 251 |
| `IB-TrustZone`   | `10.240.1.0/24`  | 251 |
| `OB-UntrustZone` | `10.240.2.0/24`  | 251 |
| `OB-TrustZone`   | `10.240.3.0/24`  | 251 |
| `GatewaySubnet`  | `10.240.10.0/24` | 251 |

#### <a name="subnets-in-the-east-us-2-development-network-vnet-dev-eus2"></a>Subnetze im Entwicklungsnetzwerk `East US 2` (`VNET-DEV-EUS2`)

Das Dev-Team verwendet das virtuelle Entwicklungsnetzwerk für Pilotprojekte in der Produktion. Es verfügt über drei Subnetze.

| Subnet | CIDR | Adressen | In Subnetz |
| --- | --- | --- | --- |
| `DEV-FE-EUS2` | `10.245.16.0/22` | 1019 | Front-Ends/Webschicht-VMs |
| `DEV-APP-EUS2` | `10.245.20.0/22` | 1019 | Anwendungsschicht-VMs |
| `DEV-DB-EUS2` | `10.245.24.0/23` | 507 | Datenbank-VMs |

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Subnetze im Produktionsnetzwerk `East US 2` (`VNET-PROD-EUS2`)

Azure-IaaS-Komponenten befinden sich im Produktionsnetzwerk. Jede Logikschicht verfügt über ein eigenes Subnetz. Die Subnetze entsprechen den Subnetzen im Entwicklungsnetzwerk – mit einem zusätzlichen Netzwerk für Domänencontroller.

| Subnetz | CIDR | Adressen | In Subnetz |
| --- | --- | --- | --- |
| `PROD-FE-EUS2` | `10.245.32.0/22` | 1019 | Front-Ends/Webschicht-VMs |
| `PROD-APP-EUS2` | `10.245.36.0/22` | 1019 | Anwendungsschicht-VMs |
| `PROD-DB-EUS2` | `10.245.40.0/23` | 507 | Datenbank-VMs |
| `PROD-DC-EUS2` | `10.245.42.0/24` | 251 | Domänencontroller-VMs |

![Diagramm: Hubnetzwerkarchitektur](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

_Abbildung 20: Hubnetzwerkarchitektur_

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Virtuelle Netzwerke in `Central US` (sekundäre Region)

`Central US` ist die sekundäre Region von Contoso. Die Netzwerkarchitektur wird von Contoso innerhalb dieser Region wie folgt gestaltet:

- **Hub:** Das virtuelle Hubnetzwerk in `Central US` gilt als sekundärer Verbindungspunkt zum lokalen Rechenzentrum. Mit dem virtuellen Spokenetzwerk in `Central US` können Workloads bei Bedarf isoliert werden, die getrennt von anderen Spokes verwaltet werden.

- **Virtuelle Netzwerke:** Contoso richtet zwei virtuelle Netzwerke in `Central US` ein:
  - `VNET-PROD-CUS`: Hierbei handelt es sich um ein Produktionsnetzwerk, das als sekundärer Hub angesehen werden kann.
  - `VNET-ASR-CUS`: In diesem virtuellen Netzwerk werden nach einem Failover von der lokalen Infrastruktur VMs erstellt. Alternativ werden dort Azure-VMs ausgeführt, für die ein Failover von der primären in die sekundäre Region durchgeführt wurde. Dieses Netzwerk ähnelt den Produktionsnetzwerken, verfügt aber über keine Domänencontroller.

  Jedes virtuelle Netzwerk in der Region besitzt einen eigenen Adressraum ohne Überlappungen. Contoso konfiguriert das Routing ohne NAT.

- **Subnetze:** Das Design der Subnetze ähnelt der in `East US 2`.

In der folgenden Tabelle werden die virtuellen Netzwerke in `Central US` zusammengefasst.

| Virtuelles Netzwerk | Range | Peer |
| --- | --- | --- |
| `VNET-HUB-CUS` | `10.250.0.0/20` | `VNET-HUB-EUS2`, `VNET-ASR-CUS`, `VNET-PROD-CUS` |
| `VNET-ASR-CUS` | `10.255.16.0/20` | `VNET-HUB-CUS`, `VNET-PROD-CUS` |
| `VNET-PROD-CUS` | `10.255.32.0/20` | `VNET-HUB-CUS`, `VNET-ASR-CUS`, `VNET-PROD-EUS2` |

![Diagramm: Hub-Spoke-Modell in einem Regionspaar](./media/contoso-migration-infrastructure/paired-hub-peer.png)

_Abbildung 21: Ein Hub-and-Spoke-Modell in einer gekoppelten Region_

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Subnetze im Hubnetzwerk `Central US` (`VNET-HUB-CUS`)

| Subnet | CIDR | Verwendbare IP-Adressen |
| --- | --- | --- |
| `IB-UntrustZone` | `10.250.0.0/24` | 251 |
| `IB-TrustZone` | `10.250.1.0/24` | 251 |
| `OB-UntrustZone` | `10.250.2.0/24` | 251 |
| `OB-TrustZone` | `10.250.3.0/24` | 251 |
| `GatewaySubnet` | `10.250.10.0/24` | 251 |

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Subnetze im Produktionsnetzwerk `Central US` (`VNET-PROD-CUS`)

Neben dem Produktionsnetzwerk in der primären Region (`East US 2`) ist auch ein Produktionsnetzwerk in der sekundären Region (`Central US`) vorhanden.

| Subnetz | CIDR | Adressen | In Subnetz |
| --- | --- | --- | --- |
| `PROD-FE-CUS` | `10.255.32.0/22` | 1019 | Front-Ends/Webschicht-VMs |
| `PROD-APP-CUS` | `10.255.36.0/22` | 1019 | Anwendungsschicht-VMs |
| `PROD-DB-CUS` | `10.255.40.0/23` | 507 | Datenbank-VMs |
| `PROD-DC-CUS` | `10.255.42.0/24` | 251 | Domänencontroller-VMs |

#### <a name="subnets-in-the-central-us-failoverrecovery-network-vnet-asr-cus"></a>Subnetze im Failover-/Wiederherstellungsnetzwerk `Central US` (`VNET-ASR-CUS`)

Das Netzwerk `VNET-ASR-CUS` wird für das Failover zwischen Regionen verwendet. Für Replikation und Failover bei Azure-VMs zwischen den Regionen wird Site Recovery verwendet. Es fungiert darüber hinaus als Contoso-Rechenzentrum mit Azure-Anbindung für geschützte Workloads, die lokal ausgeführt werden, bei einer Notfallwiederherstellung jedoch ein Failover zu Azure ausführen.

Bei `VNET-ASR-CUS` handelt es sich um dasselbe einfache Subnetz wie das virtuelle Produktionsnetzwerk in `East US 2`, das jedoch ohne ein Subnetz für den Domänencontroller auskommt.

| Subnet | CIDR | Adressen | In Subnetz |
| --- | --- | --- | --- |
| `ASR-FE-CUS` | `10.255.16.0/22` | 1019 | Front-Ends/Webschicht-VMs |
| `ASR-APP-CUS` | `10.255.20.0/22` | 1019 | Anwendungsschicht-VMs |
| `ASR-DB-CUS` | `10.255.24.0/23` | 507 | Datenbank-VMs |

![Diagramm: Hubnetzwerkarchitektur](./media/contoso-migration-infrastructure/azure-networks-cus.png)

_Abbildung 22: Hubnetzwerkarchitektur_

#### <a name="configure-peered-connections"></a>Konfigurieren von Verbindungen mit Peering

Der Hub in einer Region wird mittels Peering mit dem Hub in der anderen Region sowie mit allen virtuellen Netzwerken innerhalb der Hubregion verbunden. Dadurch können Hubs kommunizieren und alle virtuellen Netzwerke innerhalb einer Region anzeigen. Beachten Sie, dass durch Peering eine bidirektionale Verbindung erstellt wird. Eine geht vom initiierenden Peer im ersten virtuellen Netzwerk aus, die andere vom zweiten virtuellen Netzwerk.

In einer Hybridbereitstellung muss Datenverkehr, der zwischen Peers übertragen wird, über die VPN-Verbindung zwischen dem lokalen Rechenzentrum und Azure sichtbar sein. Dazu muss Contoso bestimmte Einstellungen für Peeringverbindungen festlegen. Für alle Verbindungen von virtuellen Spokenetzwerken mit dem lokalen Rechenzentrum, die über den Hub verlaufen, muss Contoso die Weiterleitung von Datenverkehr und die Verwendung der VPN-Gateways zulassen.

##### <a name="domain-controller"></a>Domänencontroller

Für die Domänencontroller im Netzwerk `VNET-PROD-EUS2` soll der Datenverkehr sowohl zwischen dem Hub-/Produktionsnetzwerk `EUS2` als auch über die VPN-Verbindung zur lokalen Umgebung fließen. Hierzu müssen die Administratoren von Contoso Folgendes zulassen:

1. **Weitergeleiteten Datenverkehr zulassen** und **Gatewaytransit zulassen** für die Verbindung mit Peering. Im vorliegenden Beispiel ist dies die Verbindung zwischen `VNET-HUB-EUS2` und `VNET-PROD-EUS2`.

    ![Screenshot: ausgewählte Kontrollkästchen zum Zulassen von weitergeleiteten Datenverkehr und zum Zulassen des Gatewaytransits](./media/contoso-migration-infrastructure/peering1.png)

    _Abbildung 23: Eine Verbindung mit Peering_

2. **Weitergeleiteten Datenverkehr zulassen** und **Remotegateways verwenden** für die andere Seite des Peerings (Verbindung zwischen `VNET-PROD-EUS2` und `VNET-HUB-EUS2`).

    ![Screenshot: ausgewählte Kontrollkästchen zum Zulassen von weitergeleiteten Datenverkehr und dem Verwenden von Remotegateways](./media/contoso-migration-infrastructure/peering2.png)

    _Abbildung 24: Eine Verbindung mit Peering_

3. Lokal muss eine statische Route eingerichtet werden, die den weiterzuleitenden lokalen Datenverkehr über den VPN-Tunnel an das virtuelle Netzwerk leitet. Die Konfiguration wird auf dem Gateway abgeschlossen, das den VPN-Tunnel von Contoso zu Azure bereitstellt. Für die statische Route wird der Dienst „Routing and Remote Access Service“ (RRAS) verwendet.

    ![Screenshot: Auswahl für die statische Route](./media/contoso-migration-infrastructure/peering3.png)

    _Abbildung 25: Eine Verbindung mit Peering_

##### <a name="production-networks"></a>Produktionsnetzwerke

Ein Peernetzwerk mit Spokes kann ein Peernetzwerk mit Spokes in einer anderen Region über einen Hub nicht sehen. Damit die Contoso-Produktionsnetzwerke in beiden Regionen füreinander sichtbar sind, müssen die Administratoren von Contoso für `VNET-PROD-EUS2` und `VENT-PROD-CUS` eine direkte Verbindung mit Peering erstellen.

![Diagramm: Erstellen einer direkten Peeringverbindung](./media/contoso-migration-infrastructure/peering4.png)

_Abbildung 26: Erstellen einer direkten Verbindung mit Peering_

### <a name="set-up-dns"></a>Einrichten von DNS

Beim Bereitstellen von Ressourcen in virtuellen Netzwerken bietet sich für die Domänennamenauflösung eine Reihe von Optionen. Sie können die in Azure verfügbare Namensauflösung verwenden oder DNS-Server für die Auflösung bereitstellen. Welche Art der Namensauflösung Sie verwenden, hängt davon ab, wie die Ressourcen miteinander kommunizieren müssen. Hier finden Sie [weitere Informationen](/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#azure-provided-name-resolution) über den Azure DNS-Dienst.

Die Administratoren von Contoso haben entschieden, dass der Azure DNS-Dienst keine gute Wahl für die Hybridumgebung ist. Stattdessen werden sie die lokalen DNS-Server verwenden. Es folgen die Details:

- Da es sich um ein Hybridnetzwerk handelt, müssen alle lokalen VMs sowie alle Azure-VMs Namen auflösen können, damit sie ordnungsgemäß funktionieren. Dies bedeutet, dass benutzerdefinierte DNS-Einstellungen auf alle virtuellen Netzwerke angewendet werden müssen.
- Contoso hat derzeit im Contoso-Rechenzentrum und in den Zweigniederlassungen Domänencontroller bereitgestellt. Die primären DNS-Server sind `contosodc1` (`172.16.0.10`) und `contosodc2` (`172.16.0.1`).
- Nach der Bereitstellung der virtuellen Netzwerke werden die lokalen Domänencontroller für die Verwendung als DNS-Server in den Netzwerken konfiguriert.
- Wenn ein optionales benutzerdefiniertes DNS für das virtuelle Netzwerk angegeben wird, muss die virtuelle IP-Adresse `168.63.129.16` für die rekursiven Resolver in Azure zur Liste hinzugefügt werden. Dazu konfiguriert Contoso die DNS-Servereinstellungen für jedes virtuelle Netzwerk. Die benutzerdefinierten DNS-Einstellungen für das Netzwerk `VNET-HUB-EUS2` würden beispielsweise wie folgt aussehen:

    ![Screenshot: Konfiguration des benutzerdefinierten DNS](./media/contoso-migration-infrastructure/custom-dns.png)

    _Abbildung 27: Ein benutzerdefiniertes DNS_

Neben den lokalen Domänencontrollern implementiert Contoso zur Unterstützung der Azure-Netzwerke noch vier weitere Domänencontroller (jeweils zwei pro Region):

| Region | SL | Virtuelles Netzwerk | Subnet | IP-Adresse |
| --- | --- | --- | --- | --- |
| `East US 2` | `contosodc3` | `VNET-PROD-EUS2` | `PROD-DC-EUS2` | `10.245.42.4` |
| `East US 2` | `contosodc4` | `VNET-PROD-EUS2` | `PROD-DC-EUS2` | `10.245.42.5` |
| `Central US` | `contosodc5` | `VNET-PROD-CUS` | `PROD-DC-CUS` | `10.255.42.4` |
| `Central US` | `contosodc6` | `VNET-PROD-CUS` | `PROD-DC-CUS` | `10.255.42.4` |

Nach der Bereitstellung der lokalen Domänencontroller muss Contoso die DNS-Einstellungen in den Netzwerken beider Regionen aktualisieren, damit die neuen Domänencontroller in den Listen der DNS-Server vorhanden sind.

#### <a name="set-up-domain-controllers-in-azure"></a>Einrichten von Domänencontrollern in Azure

Nach der Aktualisierung der Netzwerkeinstellungen sind die Administratoren von Contoso bereit, die Domänencontroller in Azure zu implementieren.

1. Im Azure-Portal stellen sie eine neue Windows Server-VM im passenden virtuellen Netzwerk bereit.
2. Sie erstellen an jedem Standort [Verfügbarkeitsgruppen](/azure/virtual-machines/windows/tutorial-availability-sets) für die VM. Verfügbarkeitsgruppen stellen sicher, dass das Azure-Fabric die VMs in verschiedene Infrastrukturen in der Azure-Region aufteilt. Mithilfe von Verfügbarkeitsgruppen kann sich Contoso zudem für die SLA (99,95 % Konnektivität) für Azure-VMs qualifizieren.

    ![Screenshot: Erstellung einer Verfügbarkeitsgruppe](./media/contoso-migration-infrastructure/availability-group.png)

    _Abbildung 28: Eine Verfügbarkeitsgruppe_

3. Nach der Bereitstellung des virtuellen Computers öffnen sie die Netzwerkschnittstelle für den virtuellen Computer. Sie legen die private IP-Adresse als statisch fest und geben eine gültige Adresse an.

    ![Screenshot: Verbindung mit der VM-Netzwerkschnittstelle](./media/contoso-migration-infrastructure/vm-nic.png)

    _Abbildung 29: EINE VM-NETZWERKSCHNITTSTELLENVERBINDUNG_

4. Sie fügen einen neuen Datenträger an den virtuellen Computer an. Dieser Datenträger enthält die Active Directory-Datenbank und die SYSVOL-Freigabe.

   Die Größe des Datenträgers bestimmt die unterstützte Anzahl IOPS. Im Laufe der Zeit muss unter Umständen die Datenträgergröße heraufgestuft werden, wenn die Umgebung wächst.

   > [!NOTE]
   > Der Datenträger darf für die Hostzwischenspeicherung nicht über Lese-/Schreibzugriff verfügen. Active Directory-Datenbanken unterstützen dies nicht.

   ![Screenshot: Active Directory-Datenträger](./media/contoso-migration-infrastructure/ad-disk.png)

   _Abbildung 30: Ein Active Directory-Datenträger_

5. Nach dem Hinzufügen des Datenträgers wird über Remotedesktopdienste eine Verbindung mit dem virtuellen Computer hergestellt und der Server-Manager geöffnet.

6. Unter **Datei- und Speicherdienste** führen sie den Assistenten für neue Volumes aus und stellen sicher, dass dem Laufwerk auf der lokalen VM der Buchstabe „F“ oder höher zugewiesen ist.

    ![Screenshot: Assistent für neue Volumes](./media/contoso-migration-infrastructure/volume-wizard.png)

    _Abbildung 31: Assistent für neue Volumes_

7. Im Server-Manager wird die Rolle **Active Directory Domain Services** hinzugefügt. Anschließend wird der virtuelle Computer als Domänencontroller konfiguriert.

    ![Screenshot: Auswahl einer Serverrolle](./media/contoso-migration-infrastructure/server-role.png)

    _Abbildung 32: Hinzufügen der Serverrolle_

8. Nachdem die VM als Domänencontroller konfiguriert und neu gestartet wurde, wird der DNS-Manager geöffnet und der Azure DNS-Resolver für die Weiterleitung konfiguriert. Dies erlaubt dem DC die Weiterleitung von DNS-Abfragen, die er nicht auflösen kann, an das Azure-DNS.

    ![Screenshot: Konfiguration des DNS-Resolvers für die Weiterleitung](./media/contoso-migration-infrastructure/dns-forwarder.png)

    _Abbildung 33: Konfigurieren des Azure DNS-Resolvers_

9. Jetzt werden die benutzerdefinierten DNS-Einstellungen der einzelnen virtuellen Netzwerke mit dem für die Region des virtuellen Netzwerks passenden Domänencontroller aktualisiert. Sie beinhalten die lokalen DCs in der Liste.

### <a name="set-up-active-directory"></a>Einrichten von Active Directory

Active Directory ist ein kritischer Dienst für Netzwerke und muss ordnungsgemäß konfiguriert werden. Die Administratoren von Contoso erstellen Active Directory-Standorte für das Contoso-Rechenzentrum und für die Regionen `East US 2` und `Central US`.

1. Sie erstellen zwei neue Standorte (`AZURE-EUS2`und `AZURE-CUS`) zusammen mit dem Standort des Rechenzentrums (`contoso-datacenter`).
2. Nach dem Erstellen der Standorte werden dort Subnetze erstellt, die den virtuellen Netzwerken und dem Rechenzentrum zugeordnet werden.

    ![Screenshot: Erstellung von Subnetzen im Rechenzentrum](./media/contoso-migration-infrastructure/dc-subnets.png)

    _Abbildung 34: Subnetze des Rechenzentrums_

3. Anschließend werden zwei Standortverknüpfungen erstellt, um alles zu verbinden. Dann sollten die Domänencontroller an ihre Standorte gebracht werden.

    ![Screenshot: Erstellung von Verknüpfungen für das Rechenzentrum](./media/contoso-migration-infrastructure/dc-links.png)

    _Abbildung 35: Verknüpfungen des Rechenzentrums_

4. Nun wird überprüft, ob die Active Directory-Replikationstopologie implementiert ist.

    ![Screenshot: Replikationstopologie des Rechenzentrums](./media/contoso-migration-infrastructure/ad-resolution.png)

    _Abbildung 36: Replikation des Rechenzentrums_

Nachdem alles abgeschlossen wurde, wird eine Liste der Domänencontroller und Standorte im lokalen Active Directory-Verwaltungscenter angezeigt.

![Screenshot: Active Directory-Verwaltungscenter](./media/contoso-migration-infrastructure/ad-center.png)

_Abbildung 37: Das Active Directory-Verwaltungscenter_

## <a name="step-5-plan-for-governance"></a>Schritt 5: Planen der Governance

Azure stellt übergreifend in den Diensten und auf der Azure-Plattform eine Reihe von Governance-Steuerelementen zur Verfügung. Weitere Informationen finden Sie in den [Azure-Governanceoptionen](/azure/governance/).

Bei der Konfiguration der Identitäts- und Zugriffssteuerung hat Contoso bereits mit der Implementierung einiger Governance- und Sicherheitsaspekte begonnen. Allgemein gibt es drei Bereiche, die berücksichtigt werden müssen:

- **Policy:** Von Azure Policy werden Regeln und Auswirkungen auf Ihre Ressourcen angewendet bzw. für diese erzwungen, damit die Ressourcen die Unternehmensanforderungen erfüllen und SLA-konform sind.
- **Sperren:** Azure ermöglicht das Sperren von Abonnements, Ressourcengruppen und weiteren Ressourcen, sodass diese nur von Personen geändert werden können, die dazu berechtigt sind.
- **Tags:** Ressourcen können mithilfe von Tags gesteuert, überwacht und verwaltet werden. Tags fügen Ressourcen Metadaten an, die Informationen über Ressourcen oder Besitzer bereitstellen.

### <a name="set-up-policies"></a>Einrichten von Richtlinien

Der Dienst „Azure Policy“ führt eine Bewertung von Ressourcen durch, indem er überprüft, welche nicht mit den Richtliniendefinitionen konform sind. So kann beispielsweise eine Richtlinie vorhanden sein, die nur bestimmte Arten von virtuellen Computern zulässt oder ein bestimmtes Tag für Ressourcen erfordert.

Richtlinien legen eine Richtliniendefinition fest, und die Richtlinienzuweisung gibt den Umfang an, in dem eine Richtlinie angewendet werden soll. Der Umfang kann von einer Verwaltungsgruppe bis zu einer Ressourcengruppe reichen. Erfahren Sie, wie Sie [Richtlinien erstellen und verwalten](/azure/governance/policy/tutorials/create-and-manage).

Contoso möchte mit zwei Richtlinien beginnen: Eine Richtlinie soll sicherstellen, dass Ressourcen nur in den Regionen `East US 2` und `Central US` bereitgestellt werden können. Eine Richtlinie soll die VM-SKUs auf ausschließlich genehmigte SKUs beschränken. Die Absicht dahinter ist, den Einsatz von teuren VM-SKUs zu verhindern.

#### <a name="limit-resources-to-regions"></a>Einschränken von Ressourcen auf Regionen

Contoso verwendet die integrierte Richtliniendefinition **Zulässige Standorte** zum Einschränken von Ressourcenregionen.

1. Wählen Sie im Azure-Portal **Alle Dienste** aus, und suchen Sie nach **Richtlinie**.
2. Wählen Sie **Zuweisungen** > **Richtlinie zuweisen** aus.
3. Wählen Sie in der Liste der Richtlinien **Zulässige Standorte** aus.
4. Legen Sie **Bereich** auf den Namen des Azure-Abonnements fest, und wählen Sie die zwei Regionen in der Zulassungsliste aus.

    ![Screenshot: per Richtlinie definierte zulässige Standorte](./media/contoso-migration-infrastructure/policy-region.png)

    _Abbildung 38: Per Richtlinie definierte zulässige Standorte_

5. Standardmäßig ist die Richtlinie auf **Ablehnen** festgelegt. Dies bedeutet, dass Bereitstellungsversuche in einem Abonnement, das sich nicht in der Region `East US 2` oder `Central US` befinden, nicht erfolgreich sind. Hier sehen Sie, was passiert, wenn jemand im Contoso-Abonnement versucht, eine Bereitstellung in `West US` einzurichten:

    ![Screenshot: Fehler aus einer fehlgeschlagenen Richtlinie](./media/contoso-migration-infrastructure/policy-failed.png)

    _Abbildung 39: Ein Richtlinienfehler_

#### <a name="allow-specific-vm-skus"></a>Zulassen bestimmter VM-SKUs

Contoso verwendet die integrierte Richtliniendefinition `Allow virtual machine SKUs`, um den Typ der VMs einzuschränken, die im Abonnement erstellt werden können.

![Screenshot: SKU-Auswahl](./media/contoso-migration-infrastructure/policy-sku.png)

_Abbildung 40: Eine SKU-Richtlinie_

#### <a name="check-policy-compliance"></a>Überprüfen der Richtlinienkonformität

Richtlinien treten sofort in Kraft, und Contoso kann Ressourcen auf Konformität überprüfen. Wählen Sie im Azure-Portal den Link **Compliance** aus. Das Compliance-Dashboard wird angezeigt. Sie können einen Drilldown ausführen, um weitere Details zu erhalten.

![Screenshot: Compliancedashboard](./media/contoso-migration-infrastructure/policy-compliance.png)

_Abbildung 41: Richtlinienkonformität_

### <a name="set-up-locks"></a>Einrichten von Sperren

Contoso hat lange das ITIL-Framework für die Verwaltung seiner Systeme verwendet. Einer der wichtigsten Aspekte des Frameworks ist die Änderungssteuerung, und Contoso möchte sicherstellen, dass auch eine Änderungssteuerung in der Azure-Bereitstellung implementiert wird.

Contoso [sperrt Ressourcen](/azure/azure-resource-manager/management/lock-resources). Alle Produktions- oder Failoverkomponenten müssen Teil einer Ressourcengruppe sein, die über eine Schreibschutzsperre verfügt. Dies bedeutet, dass die Sperre zum Ändern oder Löschen von Produktionselementen von einem autorisierten Benutzer entfernt werden muss. Produktionsfremde Ressourcengruppen werden mit einer Sperre vom Typ `CanNotDelete` versehen. Damit können autorisierte Benutzer eine Ressource lesen oder ändern, sie jedoch nicht löschen.

### <a name="set-up-tagging"></a>Einrichten des Tagging

Um Ressourcen beim Hinzufügen nachzuverfolgen, wird es für Contoso zunehmend wichtig, sie einer entsprechenden Abteilung, einem Kunden und einer Umgebung zuzuordnen. Neben der Bereitstellung von Informationen zu Ressourcen und Besitzern ermöglichen Tags die Aggregierung und Gruppierung von Ressourcen sowie die Verwendung dieser Daten zur verbrauchsbasierten Kostenzuteilung.

Contoso muss seine Azure-Ressourcen auf eine Weise visualisieren, die für das Unternehmen sinnvoll ist, etwa als Rolle oder Abteilung. Beachten Sie, dass Ressourcen gleiche Tags aufweisen können, obwohl sie sich nicht in der gleichen Ressourcengruppe befinden. Contoso erstellt eine Taxonomie für Tags, damit alle die gleichen Tags verwenden.

| Tagname | Wert |
| --- | --- |
| `CostCenter` | 12345: Es muss sich um eine in SAP gültige Kostenstelle handeln. |
| `BusinessUnit` | Name der Geschäftseinheit (von SAP). Entspricht `CostCenter`. |
| `ApplicationTeam` | E-Mail-Alias des Teams, das für den Support für die Anwendung zuständig ist. |
| `CatalogName` | Name der Anwendung oder `SharedServices` gemäß dem von der Ressource unterstützten Dienstkatalog. |
| `ServiceManager` | E-Mail-Alias des ITIL-Dienst-Managers für die Ressource. |
| `COBPriority` | Vom Unternehmen für BCDR festgelegte Priorität. Werte von 1–5. |
| `ENV` | `DEV`, `STG` und `PROD` sind die zulässigen Werte. Sie stehen für Entwicklung, Staging und Produktion. |

Beispiel:

![Screenshot: Azure-Tags](./media/contoso-migration-infrastructure/azure-tag.png)

_Abbildung 42: Azure-Tags_

Nach der Tagerstellung erstellt Contoso neue Richtliniendefinitionen und -zuweisungen, um die Verwendung der erforderlichen Tags in der gesamten Organisation zu erzwingen.

## <a name="step-6-consider-security"></a>Schritt 6: Planen der Sicherheit

Sicherheit ist in der Cloud entscheidend, und Azure bietet eine große Bandbreite an Sicherheitstools und -funktionen. Diese unterstützen Sie bei der Erstellung sicherer Lösungen auf der sicheren Azure-Plattform. Unter [Vertrauen Sie Ihrer Cloud](https://azure.microsoft.com/overview/trusted-cloud/) erfahren Sie mehr über das Thema Sicherheit in Azure.

Für Contoso ist eine Reihe von Hauptaspekten zu berücksichtigen:

- [Azure Security Center](/azure/security-center/security-center-introduction) bietet einheitliche Funktionen für die Sicherheitsverwaltung und Azure Advanced Threat Protection für Hybrid Cloud-Workloads. Hiermit können Sie Sicherheitsrichtlinien auf Ihre Workloads anwenden, die Angriffsfläche für Bedrohungen verringern sowie Angriffe erkennen und darauf reagieren.
- Eine [Netzwerksicherheitsgruppe (NSG)](/azure/virtual-network/network-security-groups-overview) filtert den Netzwerkdatenverkehr anhand einer Liste von Sicherheitsregeln, die den Netzwerkdatenverkehr zu Ressourcen, die mit virtuellen Netzwerken in Azure verbunden sind, zulassen oder blockieren.
- [Azure Disk Encryption](/azure/security/fundamentals/encryption-atrest) unterstützt Sie bei der Verschlüsselung der Datenträger Ihrer Windows- und Linux-IaaS-VMs.

### <a name="work-with-the-azure-security-center"></a>Arbeiten mit dem Azure Security Center

Contoso möchte sich schnell einen Überblick über den Sicherheitsstatus seiner neuen Hybrid Cloud-Umgebung (und insbesondere der Azure-Workloads) verschaffen. Daher hat sich Contoso für die Implementierung von Azure Security Center entschieden, zunächst mit diesen Features:

- Zentrale Richtlinienverwaltung
- Kontinuierliche Bewertung
- Umsetzbare Empfehlungen

#### <a name="centralize-policy-management"></a>Zentrale Richtlinienverwaltung

Mit der zentralen Richtlinienverwaltung stellt Contoso dank zentraler Verwaltung von Sicherheitsrichtlinien in der gesamten Umgebung die Erfüllung der Sicherheitsanforderungen sicher. Das Unternehmen kann schnell und einfach eine Richtlinie implementieren, die für alle ihre Azure-Ressourcen gilt.

![Screenshot: Auswahl für eine Sicherheitsrichtlinie](./media/contoso-migration-infrastructure/security-policy.png)

_Abbildung 43: Eine Sicherheitsrichtlinie_

#### <a name="assess-security"></a>Bewerten der Sicherheit

Contoso nutzt die kontinuierliche Sicherheitsbewertung, die die Sicherheit von Computern, Netzwerken, Speichern, Daten und Anwendungen überwacht, um mögliche Sicherheitsprobleme aufzudecken.

Im Security Center werden der Sicherheitszustand der Compute-, Infrastruktur- und Datenressourcen von Contoso sowie der der Azure-Apps und -Dienste analysiert. Die kontinuierliche Bewertung hilft dem Contoso-Betriebsteam dabei, potenzielle Sicherheitsprobleme zu erkennen, z.B. Systeme mit fehlenden Sicherheitsupdates oder ungeschützten Netzwerkports.

Contoso möchte sicherstellen, dass sämtliche virtuellen Computer geschützt sind. Hier ist das Security Center eine große Hilfe. Es überprüft die Integrität von VMs und gibt nach Priorität geordnete, handlungsrelevante Empfehlungen zum Beheben von Sicherheitsrisiken, bevor diese ausgenutzt werden.

![Screenshot: Überwachung von VMs](./media/contoso-migration-infrastructure/monitoring.png)

_Abbildung 44: Überwachung_

### <a name="work-with-nsgs"></a>Arbeiten mit NSGs

Contoso kann mithilfe einer NSG den Netzwerkdatenverkehr auf Ressourcen in einem virtuellen Netzwerk beschränken.

Eine Netzwerksicherheitsgruppe enthält eine Liste mit Sicherheitsregeln, die ein- oder ausgehenden Netzwerkdatenverkehr basierend auf IP-Adresse, Port und Protokoll (für die Quelle bzw. das Ziel) zulassen oder ablehnen. Bei Anwendung auf ein Subnetz gelten Regeln für alle Ressourcen des Subnetzes. Über die Netzwerkschnittstellen hinaus schließt dies auch Instanzen von Azure-Diensten ein, die im Subnetz bereitgestellt sind.

Mit Anwendungssicherheitsgruppen (ASGs) können Sie die Netzwerksicherheit als natürliche Erweiterung einer Anwendungsstruktur konfigurieren. Anhand dieser Gruppen können Sie VMs gruppieren und Netzwerksicherheitsrichtlinien definieren.

ASGs bieten Contoso die Möglichkeit, die Sicherheitsrichtlinie im großen Stil wiederzuverwenden, ohne dass explizite IP-Adressen manuell gewartet werden müssen. Die Plattform übernimmt die komplexe Verarbeitung von expliziten IP-Adressen und mehreren Regelsätzen, damit die Organisation sich auf die Geschäftslogik konzentrieren kann. Contoso kann eine ASG als Quelle und Ziel in einer Sicherheitsregel angeben. Nachdem eine Sicherheitsrichtlinie definiert wurde, kann Contoso virtuelle Computer erstellen und die VM-NICs einer Gruppe zuweisen.

Contoso implementiert eine Mischung aus NSGs und ASGs. Contoso hat Bedenken hinsichtlich der NSG-Verwaltung. Darüber hinaus hat das Unternehmen Bedenken hinsichtlich der übermäßigen Verwendung von NSGs und der zusätzlichen Komplexität für das Betriebspersonal. Contoso geht wie folgt vor:

- Mit Ausnahme der Gatewaysubnetze in den Hubnetzwerken wird für den gesamten ein- und ausgehenden Datenverkehr aller Subnetze (Nord/Süd) eine NSG-Regel festgelegt.
- Alle Firewalls oder Domänencontroller werden sowohl mit Subnetz-NSGs als auch mit NIC-NSGs geschützt.
- Auf alle Produktionsanwendungen werden ASGs angewendet.

Zur Veranschaulichung der Sicherheitskonfiguration hat Contoso ein Modell für seine Anwendungen erstellt.

![Diagramm: Sicherheitsmodell von Contoso](./media/contoso-migration-infrastructure/asg.png)

_Abbildung 45: Sicherheitsmodell_

Die den ASGs zugeordneten NSGs werden mit geringsten Rechten konfiguriert, um sicherzustellen, dass nur zulässige Pakete von einem Teil des Netzwerks an ihr Ziel fließen können.

| Aktion | Name | `Source` | Ziel | Port |
| --- | --- | --- | --- | --- |
| `Allow` | `AllowInternetToFE` | `VNET-HUB-EUS1`/`IB-TrustZone` | `APP1-FE` | 80, 443 |
| `Allow` | `AllowWebToApp` | `APP1-FE` | `APP1-APP` | 80, 443 |
| `Allow` | `AllowAppToDB` | `APP1-APP` | `APP1-DB` | 1433 |
| `Deny`  | `DenyAllInbound` | Any | Any | Any |

### <a name="encrypt-data"></a>Verschlüsseln von Daten

Azure Disk Encryption ist in Azure Key Vault integriert, um die Steuerung und Verwaltung der Datenträgerverschlüsselungsschlüssel und Geheimnisse für ein Abonnement zu erleichtern. Dadurch wird sichergestellt, dass alle ruhenden Daten auf VM-Datenträgern in Azure Storage verschlüsselt sind.

Contoso hat festgelegt, dass für bestimmte VMs Verschlüsselung erforderlich ist. Die Verschlüsselung wird von Contoso auf virtuelle Computer mit Kundendaten, vertraulichen Daten oder persönlichen Daten angewendet.

## <a name="conclusion"></a>Zusammenfassung

In diesem Artikel hat Contoso eine Azure-Infrastruktur und -richtlinie für Azure-Abonnements, die Hybrididentität, die Notfallwiederherstellung, das Netzwerk, die Governance und die Sicherheit eingerichtet.

Nicht jeder Schritt, der hier ausgeführt wird, ist für die Cloudmigration erforderlich. Im vorliegenden Beispiel hat Contoso eine Netzwerkinfrastruktur geplant, die für alle Migrationstypen verwendet werden kann und gleichzeitig sicher, resilient und skalierbar ist.

## <a name="next-steps"></a>Nächste Schritte

Nach dem Einrichten der Azure-Infrastruktur kann Contoso mit der Migration von Workloads in die Cloud beginnen. In der [Übersicht zu Migrationsmustern und -beispielen](./contoso-migration-overview.md#windows-server-workloads) finden Sie eine Auswahl von Szenarios, in denen diese Beispielinfrastruktur als Migrationsziel verwendet wird.
