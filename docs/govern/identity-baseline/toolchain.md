---
title: Tools für Identitätsbaseline in Azure
description: Hier erfahren Sie, wie native Azure-Tools zur Weiterentwicklung von Richtlinien und Prozessen beitragen können, die die Disziplin „Identitätsbaseline“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4f1e4d10efa8e45ea552037f55d6775b72e831b2
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88573308"
---
# <a name="identity-baseline-tools-in-azure"></a>Tools für Identitätsbaseline in Azure

Die [Disziplin „Identitätsbaseline“](./index.md) ist eine der [fünf Disziplinen der Cloudgovernance](../governance-disciplines.md). Diese Disziplin konzentriert sich auf Methoden zur Erstellung von Richtlinien, die die Konsistenz und Kontinuität der Benutzeridentitäten gewährleisten, unabhängig davon, welcher Cloudanbieter die Anwendung oder den Workload hostet.

Die folgenden Tools sind im Ermittlungshandbuch zur Hybrididentität enthalten.

**Active Directory (lokal):** Active Directory ist der im Unternehmen am häufigsten zum Speichern und Validieren von Benutzeranmeldeinformationen verwendete Identitätsanbieter.

**Azure Active Directory:** Eine SaaS-Entsprechung (Software-as-a-Service) zu Active Directory, die im Verbund mit einem lokalen Active Directory verwendet werden kann.

**Active Directory (IaaS):** Eine Instanz der Active Directory-Anwendung, die auf einem virtuellen Computer in Azure ausgeführt wird.

Die Identität ist die Steuerebene für IT-Sicherheit. Die Authentifizierung ist für eine Organisation daher der Zugriffsschutz für die Cloud. Organisationen benötigen eine Steuerebene für die Identität, mit der ihre Sicherheit gestärkt und die Cloudanwendungen vor Eindringlingen geschützt werden.

## <a name="cloud-authentication"></a>Cloudauthentifizierung

Die Wahl der richtigen Authentifizierungsmethode ist die erste Hürde für Organisationen, die ihre Anwendungen in die Cloud verschieben möchten.

Wenn Sie diese Methode wählen, übernimmt Azure AD die Anmeldung für Benutzer. In Verbindung mit dem nahtlosen einmaligen Anmelden (SSO) können sich Benutzer bei Cloudanwendungen anmelden, ohne ihre Anmeldeinformationen erneut eingeben zu müssen. Bei der Cloudauthentifizierung können Sie zwischen zwei Optionen wählen:

**Azure AD-Kennworthashsynchronisierung:** Dies ist der einfachste Weg, die Authentifizierung für lokale Verzeichnisobjekte in Azure AD zu ermöglichen. Diese Methode kann auch mit jeder beliebigen anderen Methode als Backupfailover-Authentifizierungsmethode verwendet werden, falls Ihr lokaler Server ausfällt.

**Azure AD-Pass-Through-Authentifizierung:** Es wird eine persistente Kennwortüberprüfung für Azure AD-Authentifizierungsdienste bereitgestellt, indem ein Software-Agent verwendet wird, der auf einem oder mehreren lokalen Servern ausgeführt wird.

<!-- docsTest:ignore "the pass-through authentication method" -->

> [!NOTE]
> Unternehmen mit einer Sicherheitsanforderung zur sofortigen Durchsetzung von lokalen Benutzerkontozuständen, Kennwortrichtlinien und Anmeldezeiten sollten die Verwendung der Pass-Through-Authentifizierungsmethode in Betracht ziehen.

**Verbundauthentifizierung:**

Wenn Sie diese Methode wählen, übergibt Azure AD den Authentifizierungsprozess zur Validierung des Benutzerkennworts an ein separates vertrauenswürdiges Authentifizierungssystem, z. B. an eine lokale Instanz der Active Directory-Verbunddienste (AD FS) oder einen vertrauenswürdigen Drittanbieter von Verbunddiensten.

Der Artikel [Auswählen der richtigen Authentifizierungsmethode für Azure Active Directory](/azure/active-directory/hybrid/choose-ad-authn) enthält eine Entscheidungsstruktur, die Ihnen bei der Auswahl der besten Lösung für Ihr Unternehmen hilft.

Im Folgenden finden Sie eine Tabelle der nativen Tools, die bei der Verfeinerung der Richtlinien und Prozesse beitragen können, die diese Disziplin unterstützen.

<!-- markdownlint-disable MD033 -->
<!-- docsTest:ignore UserPrincipalName SamAccountName "conditional access options" -->

| Aspekt | Kennworthashsynchronisierung + nahtloses einmaliges Anmelden | Passthrough-Authentifizierung + nahtloses einmaliges Anmelden | Verbund mit AD FS |
| --- | --- | --- | --- |
| Wo findet Authentifizierung statt? | In der Cloud | In der Cloud nach einem sicheren Kennwortüberprüfungsaustausch mit dem lokalen Authentifizierungs-Agent | Lokal |
| Welche lokalen Serveranforderungen gibt es über das Bereitstellungssystem hinaus: Azure AD Connect? | Keine | Ein Server für jeden zusätzlichen Authentifizierungs-Agent | Mindestens zwei AD FS-Server <br><br> Mindestens zwei WAP-Server im Umkreisnetzwerk |
| Welche lokalen Anforderungen hinsichtlich Internet und Netzwerk gibt es über das Bereitstellungssystem hinaus? | Keine | [Ausgehender Internetzugriff](/azure/active-directory/hybrid/how-to-connect-pta-quick-start) von den Servern, auf denen Authentifizierung-Agents ausgeführt werden | [Eingehender Internetzugriff](/windows-server/identity/ad-fs/overview/ad-fs-requirements) auf WAP-Server im Umkreisnetzwerk <br><br> Eingehender Netzwerkzugriff auf AD FS-Server von WAP-Servern im Umkreisnetzwerk <br><br> Netzwerklastenausgleich |
| Ist ein SSL-Zertifikat erforderlich? | Nein | Nein | Ja |
| Gibt es eine Systemüberwachungslösung? | Nicht erforderlich | Agent-Status, bereitgestellt von [Azure Active Directory Admin Center](/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication#general-issues) | [Azure AD Connect Health](/azure/active-directory/hybrid/how-to-connect-health-adfs) |
| Erhalten Benutzer einmaliges Anmelden für Cloudressourcen über Geräte, die in die Domäne eingebunden sind und zum Unternehmensnetzwerk gehören? | Ja, mit [nahtlosem einmaligen Anmelden](/azure/active-directory/hybrid/how-to-connect-sso) | Ja, mit [nahtlosem einmaligen Anmelden](/azure/active-directory/hybrid/how-to-connect-sso) | Ja |
| Welche Anmeldetypen werden unterstützt? | Benutzerprinzipalname + Kennwort <br><br> Integrierte Windows-Authentifizierung mit [nahtlosem einmaligen Anmelden](/azure/active-directory/hybrid/how-to-connect-sso) <br><br> [Alternative Anmelde-ID](/azure/active-directory/hybrid/how-to-connect-install-custom) | Benutzerprinzipalname + Kennwort <br><br> Integrierte Windows-Authentifizierung mit [nahtlosem einmaligen Anmelden](/azure/active-directory/hybrid/how-to-connect-sso) <br><br> [Alternative Anmelde-ID](/azure/active-directory/hybrid/how-to-connect-pta-faq) | Benutzerprinzipalname + Kennwort <br><br> SamAccountName + Kennwort <br><br> Integrierte Windows-Authentifizierung <br><br> [Zertifikat- und Smartcard-Authentifizierung](/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication) <br><br> [Alternative Anmelde-ID](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) |
| Wird Windows Hello for Business unterstützt? | [Modell der schlüsselbasierten Vertrauensstellung](/windows/security/identity-protection/hello-for-business/hello-identity-verification) <br><br> [Modell der Zertifikatvertrauensstellung mit Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune) | [Modell der schlüsselbasierten Vertrauensstellung](/windows/security/identity-protection/hello-for-business/hello-identity-verification) <br><br> [Modell der Zertifikatvertrauensstellung mit Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune) | [Modell der schlüsselbasierten Vertrauensstellung](/windows/security/identity-protection/hello-for-business/hello-identity-verification) <br><br> [Modell der Zertifikatvertrauensstellung](/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs) |
| Welche Optionen gibt es für mehrstufige Authentifizierung? | [Azure Multi-Factor Authentication](/azure/multi-factor-authentication) <br><br> [Benutzerdefinierte Steuerelemente mit bedingtem Zugriff*](/azure/active-directory/conditional-access/controls#custom-controls-preview) | [Azure Multi-Factor Authentication](/azure/multi-factor-authentication) <br><br> [Benutzerdefinierte Steuerelemente mit bedingtem Zugriff*](/azure/active-directory/conditional-access/controls#custom-controls-preview) | [Azure Multi-Factor Authentication](/azure/multi-factor-authentication) <br><br> [Azure Multi-Factor Authentication-Server](/azure/active-directory/authentication/howto-mfaserver-deploy) <br><br> [Multi-Factor Authentication von Drittanbietern](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs) <br><br> [Benutzerdefinierte Steuerelemente mit bedingtem Zugriff](/azure/active-directory/conditional-access/controls#custom-controls-preview) |
| Welche Benutzerkontenstatus werden unterstützt? | Deaktivierte Konten <br> (Bis zu 30 Minuten Verzögerung) | Deaktivierte Konten <br><br> Konto gesperrt <br><br> Konto abgelaufen <br><br> Kennwort abgelaufen <br><br> Anmeldestunden | Deaktivierte Konten <br><br> Konto gesperrt <br><br> Konto abgelaufen <br><br> Kennwort abgelaufen <br><br> Anmeldestunden |
| Welche Optionen für bedingten Zugriff gibt es? | [Bedingter Zugriff auf Azure AD](/azure/active-directory/conditional-access/overview) | [Bedingter Zugriff auf Azure AD](/azure/active-directory/conditional-access/overview) | [Bedingter Zugriff auf Azure AD](/azure/active-directory/conditional-access/overview) <br><br> [AD FS-Anspruchsregeln](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator) |
| Wird Blockieren älterer Protokolle unterstützt? | [Ja](/azure/active-directory/conditional-access/concept-baseline-protection) | [Ja](/azure/active-directory/conditional-access/concept-baseline-protection) | [Ja](/windows-server/identity/ad-fs/operations/access-control-policies-w2k12) |
| Können das Logo, das Bild und die Beschreibung auf den Anmeldeseiten angepasst werden? | [Ja, mit Azure AD Premium](/azure/active-directory/customize-branding) | [Ja, mit Azure AD Premium](/azure/active-directory/customize-branding) | [Ja](/azure/active-directory/connect/active-directory-aadconnect-federation-management#customlogo) |
| Welche erweiterten Szenarien werden unterstützt? | [Intelligente Kennwortsperrung](/azure/active-directory/authentication/concept-sspr-howitworks) <br><br> [Berichte über kompromittierte Anmeldeinformationen](/azure/active-directory/reports-monitoring/concept-risk-events) | [Intelligente Kennwortsperrung](/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-smart-lockout) | Authentifizierungssystem mit geringer Wartezeit für mehrere Standorte <br><br> [AD FS-Extranetsperre](/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection) <br><br> [Integration in Identitätssysteme von Drittanbietern](/azure/active-directory/connect/active-directory-aadconnect-federation-compatibility) |

<!-- markdownlint-enable MD033 -->

> [!NOTE]
> Der bedingte Zugriff in Azure AD über benutzerdefinierte Steuerelemente unterstützt zurzeit keine Geräteregistrierung.

## <a name="next-steps"></a>Nächste Schritte

<!-- TODO: The download button for this whitepaper returns 404. -->

<!-- docsTest:ignore "Hybrid Identity Digital Transformation Framework" -->

Das [Whitepaper zum Hybrididentitätsframework für die digitale Transformation](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html) beschreibt Kombinationen und Lösungen für die Auswahl und Integration jeder dieser Komponenten.

Mit dem [Azure AD Connect-Tool](https://aka.ms/aadconnectwiz) können Sie Ihre lokalen Verzeichnisse in Azure AD integrieren.
