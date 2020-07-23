---
title: Enterprise Agreement-Registrierung und Azure Active Directory-Mandanten
description: Unternehmensregistrierung und Azure Active Directory-Mandanten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: eee2f462490a8c69c0c772b11f8877380e790c7b
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194696"
---
# <a name="enterprise-agreement-enrollment-and-azure-active-directory-tenants"></a>Enterprise Agreement-Registrierung und Azure Active Directory-Mandanten

## <a name="planning-for-enterprise-enrollment"></a>Planen der Unternehmensregistrierung

Eine Enterprise Agreement-Registrierung (EA) stellt die Geschäftsbeziehung zwischen Microsoft und der Art und Weise dar, wie Ihre Organisation Azure verwendet. Sie bildet die Grundlage für die Abrechnung für alle Ihre Abonnements und wirkt sich auf die Verwaltung Ihrer digitalen Ressourcen aus. Ihre EA-Registrierung wird über ein Azure-Unternehmensportal verwaltet. Eine Registrierung bildet häufig die Hierarchie einer Organisation ab, einschließlich ihrer Abteilungen, Konten und Abonnements. Diese Hierarchie stellt Kostenerfassungsgruppen innerhalb einer Organisation dar.

![Azure EA-Hierarchien](./media/ea.png)
_Abbildung 1: Eine Azure EA-Registrierungshierarchie._

- Mithilfe von Abteilungen werden Kosten in logische Gruppierungen segmentiert, und ein Budget bzw. Kontingent wird auf Abteilungsebene festgelegt (Hinweis: Das Kontingent dient zu Berichterstattungszwecken und wird nicht strikt erzwungen).

- Konten sind Organisationseinheiten im Azure Enterprise-Portal, über die Abonnements verwaltet und Berichte aufgerufen werden können.

- Abonnements sind die kleinste Einheit im Azure Enterprise-Portal. Dabei handelt es sich um Container für Azure-Dienste, die vom Dienstadministrator verwaltet werden. Hier stellt Ihre Organisation Azure-Dienste bereit.

- Über EA-Registrierungsrollen sind Benutzer mit ihrer funktionalen Rolle verknüpft. Die folgenden Rollen sind vorhanden:
  - Unternehmensadministrator
  - Abteilungsadministrator
  - Kontobesitzer
  - Dienstadministrator
  - Benachrichtigungskontakt

**Überlegungen zum Entwurf:**

- Die Registrierung stellt eine hierarchische Organisationsstruktur bereit, mit der die Verwaltung von Abonnements gesteuert wird.

- Mehrere Umgebungen können auf EA-Kontoebene getrennt werden, um die ganzheitliche Abgrenzung zu unterstützen.

- Einer einzelnen Registrierung können mehrere Administratoren zugewiesen werden.

- Jedes Abonnement muss ein Kontobesitzer zugeordnet sein.

- Jeder Kontobesitzer wird zum Abonnementbesitzer für alle Abonnements, die unter dem betreffenden Konto bereitgestellt werden.

- Ein Abonnement kann jeweils nur zu einem Konto gehören.

- Ein Abonnement kann entsprechend bestimmten Kriterien gesperrt werden.

**Entwurfsempfehlungen:**

- Verwenden Sie für alle Kontotypen nur den Authentifizierungstyp `Work or school account`. Vermeiden Sie die Verwendung des Kontotyps `Microsoft account (MSA)`.

- Richten Sie die Kontakt-E-Mail-Adresse für Benachrichtigungen ein, um sicherzustellen, dass Benachrichtigungen an das entsprechenden Gruppenpostfach gesendet werden.

- Weisen Sie jedem Konto ein Budget zu, und richten Sie eine Warnung für das betreffende Budget ein.

- Eine Organisation kann über eine Vielzahl von Strukturen verfügen, z. B. nach Funktionen, Abteilungen, geografischer Verteilung, Matrix oder Teamstruktur. Verwenden Sie die Organisationsstruktur, um Ihre Organisationsstruktur auf Ihre Registrierungshierarchie abzubilden.

- Erstellen Sie eine neue Abteilung für IT, wenn Geschäftsbereiche über unabhängige IT-Funktionen verfügen.

- Beschränken und minimieren Sie die Anzahl der Kontobesitzer innerhalb der Registrierung, um die Verbreitung von Administratorzugriff auf Abonnements und zugehörige Azure-Ressourcen zu vermeiden.

- Wenn mehrere Azure AD-Mandanten (Azure Active Directory) verwendet werden, vergewissern Sie sich, dass der Kontobesitzer dem Mandanten zugeordnet ist, in dem auch die Abonnements für das Konto bereitgestellt sind.

- Richten Sie Enterprise Dev/Test-/Produktionsumgebungen auf EA-Kontoebene ein, um die ganzheitliche Abgrenzung zu fördern.

- Ignorieren Sie keine E-Mails mit Benachrichtigungen, die an die E-Mail-Adresse des Benachrichtigungskontos gesendet werden. Microsoft sendet wichtige EA-weite Mitteilungen an dieses Konto.

- Ein EA-Konto darf in Azure AD nicht verschoben oder umbenannt werden.

- Besuchen Sie in regelmäßigen Abständen das EA-Portal, um zu überprüfen, welche Benutzer Zugriff haben, und vermeiden Sie nach Möglichkeit die Verwendung eines Microsoft-Kontos.

## <a name="define-azure-ad-tenants"></a>Definieren von Azure AD-Mandanten

Ein Azure AD Mandanten ermöglich die Identitäts- und Zugriffsverwaltung. Diese ist ein wichtiger Bestandteil Ihrer Sicherheitsvorkehrungen, mit denen Sie sicherstellen, dass authentifizierte und autorisierte Benutzer nur Zugriff auf die Ressourcen haben, für die Sie Zugriffsberechtigungen besitzen. Azure AD bietet diese Dienste nicht nur für in Azure bereitgestellte Anwendungen und Dienste, sondern auch für Dienste und Anwendungen, die außerhalb von Azure bereitgestellt werden (z. B. lokal oder in Drittanbieter-Clouds). Azure AD wird auch von SaaS-Anwendungen (Software-as-a-Service) wie Microsoft 365 und Azure Marketplace verwendet. Organisationen, die bereits lokale Active Directory-Instanzen verwenden, können Ihre vorhandene Infrastruktur nutzen und die Authentifizierung durch die Integration mit Azure AD auf die Cloud ausweiten. Jedes Azure AD-Verzeichnis verfügt über mindestens eine Domäne. Einem Verzeichnis können viele Abonnements zugeordnet sein, jedoch nur ein Azure AD-Mandant.

Während der Azure AD Entwurfsphase sind grundlegende Sicherheitsfragen zu beantworten, z. B. wie Ihre Organisation Anmeldeinformationen verwaltet und wie Benutzerzugriff, Anwendungszugriff und programmgesteuerter Zugriff gesteuert werden.

**Überlegungen zum Entwurf:**

- Mehrere Azure AD-Mandanten können in derselben Registrierung aktiv sein.

**Entwurfsempfehlungen:**

- Verwenden Sie das nahtlose einmalige Anmelden von Azure AD entsprechend der ausgewählten [Planungstopologie](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies).

- Verfügt Ihre Organisation über keine Identitätsinfrastruktur, beginnen Sie mit der Implementierung einer auf Azure AD beschränkten Identitätsbereitstellung. Eine solche Bereitstellung mit [Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services) und [Microsoft Enterprise Mobility + Security](https://docs.microsoft.com/mem/intune/fundamentals/what-is-intune) bietet End-to-End-Schutz für SaaS-Anwendungen, Unternehmensanwendungen und für Geräte.

- Die mehrstufige Authentifizierung stellt eine weitere Sicherheitsebene und eine zweite Authentifizierungsbarriere dar. Erzwingen Sie die [mehrstufige Authentifizierung](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) und [Richtlinien für bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) für alle privilegierten Konten, um die Sicherheit zu erhöhen.

- Planen und implementieren Sie [Notfallzugriffs-](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-emergency-access) oder Break-Glass-Konten, um eine mandantenweite Kontensperrung zu vermeiden.

- Verwenden Sie [Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) für die Identitäts- und Zugriffsverwaltung.

- Wenn Dev/Test/Produktion aus Identitätssicht isolierte Umgebungen sein sollen, trennen Sie sie auf Mandantenebene über mehrere Mandanten.

- Erstellen Sie keinen neuen Azure AD-Mandanten, es sei denn, dies ist aufgrund der Identitäts- und Zugriffsverwaltung und wegen vorhandener Prozesse zwingend erforderlich.
