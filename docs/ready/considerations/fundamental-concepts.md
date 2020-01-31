---
title: Grundlegende Konzepte in Azure
description: Lernen Sie grundlegende Konzepte und Begriffe kennen, die in Azure verwendet werden, und erfahren Sie, wie diese Konzepte zusammenhängen.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: d11e69014a9e46f916afb5bc8caf083c930ce725
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76799147"
---
# <a name="azure-fundamental-concepts"></a>Grundlegende Konzepte in Azure

Lernen Sie grundlegende Konzepte und Begriffe kennen, die in Azure verwendet werden, und erfahren Sie, wie diese Konzepte zusammenhängen.

## <a name="azure-terminology"></a>Azure-Terminologie

Es ist hilfreich, die folgenden Definitionen zu kennen, wenn Sie mit der Einführung der Azure-Cloud beginnen:

- **Ressource:** Eine Entität, die von Azure verwaltet wird. Hierzu gehören beispielsweise virtuelle Azure-Computer, virtuelle Netzwerke und Speicherkonten.
- **Abonnement:** Ein logischer Container für Ihre Ressourcen. Jede Azure-Ressource ist nur einem Abonnement zugeordnet. Das Erstellen eines Abonnements ist der erste Schritt beim Einstieg in Azure.
- **Azure-Konto:** Die E-Mail-Adresse, die Sie beim Erstellen eines Azure-Abonnements angeben, ist das Azure-Konto für das Abonnement. Die Partei, die dem E-Mail-Konto zugeordnet ist, ist für die monatlichen Kosten zuständig, die durch die Ressourcen im Abonnement anfallen. Wenn Sie ein Azure-Konto erstellen, geben Sie Kontaktinformationen sowie Abrechnungsinformationen wie z.B. eine Kreditkarte an. Sie können für mehrere Abonnements dasselbe Azure-Konto (E-Mail-Adresse) verwenden. Jedes Abonnement ist nur einem Azure-Konto zugeordnet.
- **Kontoadministrator:** Die Partei, die der E-Mail-Adresse zugeordnet ist, die zum Erstellen eines Azure-Abonnements verwendet wird. Der Kontoadministrator ist für die Begleichung aller Kosten verantwortlich, die durch die Ressourcen des Abonnements verursacht werden.
- **Azure Active Directory (Azure AD):** Der cloudbasierte Identitäts- und Zugriffsverwaltungsdienst von Microsoft. Azure AD ermöglicht Ihren Mitarbeitern die Anmeldung und den Zugriff auf Ressourcen.
- **Azure AD-Mandant:** Eine dedizierte und vertrauenswürdige Instanz von Azure AD. Ein Azure AD-Mandant wird automatisch erstellt, wenn sich Ihre Organisation zum ersten Mal für das Abonnement eines Microsoft-Clouddiensts wie Microsoft Azure, Microsoft Intune oder Office 365 registriert. Ein Azure-Mandant stellt eine einzelne Organisation dar.
- **Azure AD-Verzeichnis:** Jeder Azure AD-Mandant verfügt über ein einzelnes dediziertes und vertrauenswürdiges Verzeichnis. Das Verzeichnis enthält die Benutzer, Gruppen und Apps des Mandanten. Das Verzeichnis wird zum Ausführen von Funktionen zur Identitäts- und Zugriffsverwaltung für Mandantenressourcen verwendet. Einem Verzeichnis können mehrere Abonnements zugeordnet werden, aber jedes Abonnement ist nur einem Verzeichnis zugeordnet.
- **Ressourcengruppen**: Logische Container, in denen verwandte Ressourcen innerhalb eines Abonnements gruppiert werden. Jede Ressource kann nur in einer Ressourcengruppe vorhanden sein. Ressourcengruppen ermöglichen eine präzisere Gruppierung innerhalb eines Abonnements. Sie werden häufig zur Darstellung einer Sammlung von Ressourcen verwendet, die zur Unterstützung einer Workload, Anwendung oder bestimmten Funktion in einem Abonnement erforderlich sind.
- **Verwaltungsgruppen**: Logische Container, die Sie für mindestens ein Abonnement verwenden. Sie können eine Hierarchie mit Verwaltungsgruppen, Abonnements, Ressourcengruppe und Ressourcen definieren, um Zugriff, Richtlinien und Compliance über Vererbung effizient zu verwalten.
- **Region:** Eine Reihe von Azure-Datencentern, die innerhalb eines durch Latenzzeiten definierten Umkreises bereitgestellt werden. Die Datencenter sind über ein dediziertes, regionales Netzwerk mit geringer Latenz verbunden. Die meisten Azure-Ressourcen werden in einer bestimmten Azure-Region ausgeführt.

## <a name="azure-subscription-purposes"></a>Zwecke eines Azure Abonnements

Ein Azure-Abonnement dient verschiedenen Zwecken. Ein Azure-Abonnement ist:

- **Eine rechtsgültige Vereinbarung**. Jedes Abonnement ist einem [Azure-Angebot](https://azure.microsoft.com/support/legal/offer-details) zugeordnet (z.B. „Kostenlose Testversion“ oder „Nutzungsbasierte Zahlung“). Jedes Angebot umfasst einen spezifischen Tarifplan, spezifische Vorteile und zugehörige Nutzungsbedingungen. Sie wählen ein Azure-Angebot aus, wenn Sie ein Abonnement erstellen.
- **Eine Zahlungsvereinbarung**. Wenn Sie ein Abonnement erstellen, geben Sie Zahlungsinformationen für dieses Abonnement an, z.B. eine Kreditkartennummer. Die Kosten, die aufgrund der bereitgestellten Ressourcen in diesem Abonnement anfallen, werden monatlich berechnet und über die angegebene Zahlungsmethode in Rechnung gestellt.
- **Eine Umfangsbegrenzung**. Skalierungsgrenzwerte werden für ein Abonnement definiert. Die Ressourcen des Abonnements dürfen die festgelegten Skalierungsgrenzwerte nicht überschreiten. Beispielsweise gilt eine Beschränkung für die Anzahl virtueller Computer, die Sie in einem einzelnen Abonnement erstellen können.
- **Eine administrative Grenze**. Ein Abonnement kann als Grenze für Verwaltung, Sicherheit und Richtlinien fungieren. Azure bietet auch andere Mechanismen zum Erfüllen dieser Anforderungen, z.B. Verwaltungsgruppen, Ressourcengruppen und rollenbasierte Zugriffssteuerung.

## <a name="azure-subscription-considerations"></a>Überlegungen zu Azure-Abonnements

Wenn Sie ein Azure-Abonnement erstellen, treffen Sie einige wichtige Entscheidungen in Bezug auf das Abonnement:

- **Wer ist für die Bezahlung des Abonnements zuständig?** Die Partei, die der E-Mail-Adresse zugeordnet ist, die Sie beim Erstellen eines Abonnements standardmäßig angeben, ist der Kontoadministrator des Abonnements. Die zu dieser E-Mail-Adresse gehörige Partei ist für die Begleichung aller Kosten zuständig, die durch die Ressourcen des Abonnements verursacht werden.
- **Welches Azure-Angebot interessiert mich?** Jedes Abonnement ist einem bestimmten [Azure-Angebot](https://azure.microsoft.com/support/legal/offer-details) zugeordnet. Sie können das Azure-Angebot auswählen, das Ihre Anforderungen am besten erfüllt. Wenn Sie z. B. beabsichtigen, ein Abonnement zum Ausführen von Nichtproduktionsworkloads zu verwenden, sollten Sie sich für das Angebot „Dev/Test Pay-As-You-Go“ oder „Enterprise Dev/Test“ entscheiden.

> [!NOTE]
> Wenn Sie sich für Azure registrieren, werden ggf. Optionen wie *Azure-Konto erstellen* angezeigt. Sie erstellen ein Azure-Konto, wenn Sie ein Azure-Abonnement erstellen und das Abonnement einem E-Mail-Konto zuordnen.

## <a name="azure-administrative-roles"></a>Azure-Administratorrollen

Azure definiert drei Arten von Rollen für die Verwaltung von Abonnements, Identitäten und Ressourcen:

- Administrator für klassisches Abonnement
- Rollenbasierte Zugriffssteuerung in Azure
- Azure AD-Administrator (Azure Active Directory)

Die Kontoadministratorrolle für ein Azure-Abonnement wird dem E-Mail-Konto zugewiesen, das zum Erstellen des Azure-Abonnements verwendet wird. Der Kontoadministrator ist der Besitzer des Abonnements, an den die Abrechnung erfolgt. Der Kontoadministrator kann die Abonnementdetails im [Azure-Kontocenter](https://account.azure.com/Subscriptions) verwalten.

Standardmäßig wird die Dienstadministratorrolle für ein Abonnement auch dem E-Mail-Konto zugewiesen, das zum Erstellen des Azure-Abonnements verwendet wird. Der Dienstadministrator verfügt über Berechtigungen für das Abonnement, die einem RBAC-basierten Besitzer entsprechen. Der Dienstadministrator besitzt außerdem Vollzugriff auf das Azure-Portal. Der Kontoadministrator kann den Dienstadministrator in ein anderes E-Mail-Konto ändern.

Wenn Sie ein Azure-Abonnement erstellen, können Sie es einem vorhandenen Azure AD-Mandanten zuordnen. Andernfalls wird ein neuer Azure AD-Mandant mit einem zugehörigen Verzeichnis erstellt. Die Rolle „globaler Administrator“ im Azure AD Verzeichnis wird dem E-Mail-Konto zugewiesen, das zum Erstellen des Azure AD Abonnements verwendet wird.

Ein E-Mail-Konto kann mehreren Azure-Abonnements zugeordnet sein. Der Kontoadministrator kann ein Abonnement in ein anderes Konto übertragen.

Eine detaillierte Beschreibung der Rollen in Azure finden Sie unter [Administratorrollen für klassische Abonnements, Azure RBAC-Rollen und Azure AD-Administratorrollen](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

## <a name="subscriptions-and-regions"></a>Abonnements und Regionen

Jede Azure-Ressource ist logisch nur einem Abonnement zugeordnet. Wenn Sie eine Ressource erstellen, wählen Sie aus, in welchem Azure-Abonnement diese bereitgestellt werden soll. Sie können eine Ressource später in ein anderes Abonnement verschieben.

Ein Abonnement ist nicht an eine bestimmte Azure-Region gebunden. Allerdings wird jede Azure-Ressource nur in einer Region bereitgestellt. Sie können über Ressourcen in mehreren Regionen verfügen, die demselben Abonnement zugeordnet sind.

> [!NOTE]
> Die meisten Azure-Ressourcen werden in einer bestimmten Region bereitgestellt. Bestimmte Ressourcentypen werden jedoch als globale Ressourcen betrachtet, beispielsweise Richtlinien, die Sie mithilfe der Azure Policy-Dienste festlegen.

## <a name="related-resources"></a>Zugehörige Ressourcen

Die folgenden Ressourcen bieten detaillierte Informationen über die Konzepte, die in diesem Artikel vorgestellt wurden:

- [Wie funktioniert Azure?](../../getting-started/what-is-azure.md)
- [Ressourcenzugriffsverwaltung in Azure](../../govern/resource-consistency/resource-access-management.md)
- [Übersicht über den Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)
- [Rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) für Azure-Ressourcen](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Was ist Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)
- [Zuordnen oder Hinzufügen eines Azure-Abonnements zu Ihrem Azure Active Directory-Mandanten](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)
- [Topologien für Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies)
- [Abonnements, Lizenzen, Konten und Mandanten für die Microsoft-Cloudangebote](https://docs.microsoft.com/office365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings)

## <a name="next-steps"></a>Nächste Schritte

Nun, da Sie die grundlegenden Azure-Konzepte kennen, geht es als Nächstes um das [Skalieren mit mehreren Azure-Abonnements](../azure-best-practices/scaling-subscriptions.md).

> [!div class="nextstepaction"]
> [Skalieren mit mehreren Azure-Abonnements](../azure-best-practices/scaling-subscriptions.md)
