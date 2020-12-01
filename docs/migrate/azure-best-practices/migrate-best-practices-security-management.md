---
title: Bewährte Methoden zum Sichern und Verwalten von Workloads, die zu Azure migriert werden
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über Best Practices (bewährte Methoden) zum Abarbeiten, Verwalten und Sichern Ihrer migrierten Workloads zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 35f078aeb04c6fda78470e33e27f332f67bdaeee
ms.sourcegitcommit: 57b757759b676a22f13311640b8856557df36581
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2020
ms.locfileid: "94997470"
---
<!-- docutune:casing "Update Management" -->
<!-- cSpell:ignore FIPS SIEM majeure NSGs -->

# <a name="best-practices-to-secure-and-manage-workloads-migrated-to-azure"></a>Bewährte Methoden zum Sichern und Verwalten von Workloads, die zu Azure migriert werden

Wenn Sie eine Migration zu Azure planen, sollten Sie nicht nur eine Strategie für die Migration selbst entwerfen, sondern müssen auch ein neues Sicherheits- und Verwaltungsmodell konzipieren, das nach der Migration angewendet werden soll. Dieser Artikel enthält Informationen zur Planung sowie bewährte Methoden zum Schutz Ihrer Azure-Bereitstellung nach der Migration. Außerdem finden Sie hier Informationen zu laufenden Aufgaben, mit denen Sie die optimale Ausführung Ihrer Bereitstellung sicherstellen können.

> [!IMPORTANT]
> Die in diesem Artikel beschriebenen Best Practices und Meinungen basieren auf Azure-Plattform- und -Dienstfeatures, die zu dem Zeitpunkt verfügbar waren, zu dem dieser Artikel verfasst wurde. Features und Funktionen ändern sich im Laufe der Zeit.

## <a name="secure-migrated-workloads"></a>Sichern von migrierten Workloads

Nach der Migration besteht die wichtigste Aufgabe darin, die migrierten Workloads vor internen und externen Bedrohungen zu schützen. Folgende Best Practices helfen Ihnen dabei:

- Erfahren Sie, wie Sie die Überwachungsfunktionen, Bewertungen und Empfehlungen von Azure Security Center verwenden.
- Lernen Sie die Best Practices zum Verschlüsseln Ihrer Daten in Azure kennen.
- Schützen Sie Ihre VMs vor Schadsoftware und Angriffen.
- Sorgen Sie für die Sicherheit von Informationen in migrierten Web-Apps.
- Überprüfen Sie, wer nach der Migration auf Ihre Azure-Abonnements und -Ressourcen zugreifen kann.
- Überprüfen Sie Ihre Azure-Überwachungs- und -Sicherheitsprotokolle in regelmäßigen Abständen.
- Verstehen und bewerten Sie die erweiterten Sicherheitsfeatures, die Azure bietet.

Diese bewährten Methoden werden in den folgenden Abschnitten ausführlicher beschrieben.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Bewährte Methode: Befolgen der Azure Security Center-Empfehlungen

Azure-Mandantenadministratoren müssen Sicherheitsfeatures aktivieren, um Workloads vor Angriffen zu schützen. Azure Security Center bietet eine einheitliche Sicherheitsverwaltung. In Security Center können Sie Sicherheitsrichtlinien für Ihre Workloads anwenden, die Angriffsfläche für Bedrohungen verringern sowie Angriffe erkennen und darauf reagieren. Security Center analysiert Ressourcen und Konfigurationen für mehrere Azure-Mandanten und gibt Sicherheitsempfehlungen ab. Im Anschluss folgen einige Beispiele:

- **Zentrale Richtlinienverwaltung:** Stellen Sie die Einhaltung unternehmensspezifischer oder gesetzlicher Sicherheitsvorschriften sicher, indem Sie Sicherheitsrichtlinien für alle Hybridcloud-Workloads zentral verwalten.
- **Laufende Sicherheitsbewertung:** Überwachen Sie den Sicherheitsstatus von Computern, Netzwerken, Speicher- und Datendiensten und Anwendungen, um potenzielle Sicherheitsprobleme aufzudecken.
- **Umsetzbare Empfehlungen:** Beseitigen Sie mit priorisierten, direkt umsetzbaren Sicherheitsempfehlungen Sicherheitslücken, bevor sie von Angreifern ausgenutzt werden können.
- **Priorisierte Warnungen und Vorfälle:** Konzentrieren Sie sich mittels priorisierter Warnungen und Vorfälle auf die größten Bedrohungen.

Zusätzlich zu Bewertungen und Empfehlungen stellt Azure Security Center weitere Sicherheitsfeatures bereit, die für bestimmte Ressourcen aktiviert werden können.

- **Just-in-Time-Zugriff (JIT):** Verringern Sie die Angriffsfläche in Ihrem Netzwerk mit kontrolliertem Just-In-Time-Zugriff auf Verwaltungsports für virtuelle Azure-Computer.
  - Ist der RDP-Port 3389 auf einem virtuellen Computer geöffnet, ist dieser Computer dauerhaft der Gefahr von Aktivitäten durch böswillige Benutzer ausgesetzt. Azure-IP-Adressen sind bekannt, und Hacker prüfen sie immer wieder auf offene 3389-Ports.
  - Beim Just-In-Time-Zugriff werden Netzwerksicherheitsgruppen und Regeln für eingehenden Datenverkehr verwendet, die den Zeitraum begrenzen, für den ein bestimmter Port geöffnet ist.
  - Bei aktiviertem Just-In-Time-Zugriff wird von Security Center überprüft, ob einem Benutzer über die rollenbasierte Zugriffssteuerung Schreibzugriffsberechtigungen für einen virtuellen Computer erteilt wurden. Darüber hinaus können Sie Regeln dafür festlegen, wie Benutzer Verbindungen mit virtuellen Computern herstellen können. Sind die Berechtigungen in Ordnung, wird eine Zugriffsanforderung genehmigt, und Security Center konfiguriert Netzwerksicherheitsgruppen automatisch so, dass für den von Ihnen angegebenen Zeitraum eingehender Datenverkehr an die ausgewählten Ports zugelassen wird. Netzwerksicherheitsgruppen werden nach Ablauf des Zeitraums in ihren vorherigen Zustand zurückversetzt.
- **Adaptive Anwendungssteuerungen:** Halten Sie Software und Schadsoftware von Ihren virtuellen Computern fern, indem Sie mit dynamischen Zulassungslisten steuern, welche Anwendungen auf den Computern ausgeführt werden.
  - Mit adaptiven Anwendungssteuerungen können Sie Anwendungen genehmigen und verhindern, dass Benutzer oder Administratoren, die nicht über die entsprechenden Berechtigungen verfügen, nicht genehmigte oder nicht überprüfte Anwendungen auf Ihren VMs installieren.
    - Sie können Versuche zum Ausführen von schädlichen Anwendungen blockieren oder davor warnen, unerwünschte oder schädliche Anwendungen vermeiden und die Konformität mit der Anwendungssicherheitsrichtlinie Ihrer Organisation sicherstellen.
- **Überwachen der Dateiintegrität:** Stellen Sie die Integrität von Dateien sicher, die auf VMs ausgeführt werden.
  - Probleme auf VMs treten nicht nur nach der Installation von Software auf. Die Änderung einer Systemdatei kann auch zum Ausfall oder zur Leistungsbeeinträchtigung eines virtuellen Computers führen. Die Überwachung der Dateiintegrität untersucht Systemdateien und Registrierungseinstellungen auf Änderungen und benachrichtigt Sie, wenn ein Element aktualisiert wurde.
  - Security Center empfiehlt die Dateien, die Sie überwachen sollten.

**Weitere Informationen**:

- Weitere Informationen zu [Azure Security Center](/azure/security-center/security-center-intro)
- Weitere Informationen zum Just-In-Time-Zugriff für virtuelle Computer finden Sie [hier](/azure/security-center/security-center-just-in-time).
- Erfahren Sie mehr über das [Anwenden von adaptiven Anwendungssteuerungen](/azure/security-center/security-center-adaptive-application).
- [Beginnen Sie](/azure/security-center/security-center-file-integrity-monitoring) mit der Überwachung der Dateiintegrität.

## <a name="best-practice-encrypt-data"></a>Bewährte Methode: Verschlüsseln von Daten

Die Verschlüsselung ist ein wichtiger Bestandteil der Azure-Sicherheitsmaßnahmen. Indem Sie sicherstellen, dass die Verschlüsselung auf allen Ebenen aktiviert ist, können Sie verhindern, dass nicht autorisierte Parteien Zugriff auf vertrauliche Daten erhalten. Dies gilt für Daten während der Übertragung und für ruhende Daten.

### <a name="encryption-for-infrastructure-as-a-service-iaas"></a>Verschlüsselung für Infrastructure-as-a-Service (IaaS)

- **Virtuelle Computer:** Zum Verschlüsseln von IaaS-VM-Datenträgern unter Windows und Linux können Sie Azure Disk Encryption verwenden.
  - Azure Disk Encryption verwendet BitLocker für Windows und dm-crypt für Linux, um Volumeverschlüsselung für die Betriebssystemdatenträger und die regulären Datenträger bereitzustellen.
  - Sie können einen von Azure erstellten Verschlüsselungsschlüssel verwenden oder eigene Verschlüsselungsschlüssel bereitstellen, die in Azure Key Vault geschützt sind.
  - Mit Azure Disk Encryption werden IaaS-VM-Daten im Ruhezustand (auf dem Datenträger) und während des VM-Starts gesichert.
    - Azure Security Center warnt Sie, wenn VMs nicht verschlüsselt sind.
- **Speicher:** Schützen Sie ruhende, in Azure Storage gespeicherte Daten.
  - Daten in Azure Storage-Konten können mithilfe von AES-Schlüsseln verschlüsselt werden, die von Microsoft generiert werden und mit FIPS 140-2 konform sind. Alternativ können auch eigene Schlüssel verwendet werden.
  - Die Azure Storage-Verschlüsselung wird für alle neuen und bereits vorhandenen Speicherkonten aktiviert und kann nicht deaktiviert werden.

### <a name="encryption-for-platform-as-a-service-paas"></a>Verschlüsselung für Platform-as-a-Service (PaaS)

Im Gegensatz zum IaaS-Konzept, bei dem Sie Ihre eigenen virtuellen Computer und Ihre eigene Infrastruktur verwalten, werden beim PaaS-Modell Plattform und Infrastruktur vom Anbieter verwaltet. Dadurch können Sie sich ganz auf die Anwendungslogik und -funktionen konzentrieren. Es gibt sehr viele verschiedene Arten von PaaS-Diensten, daher wird jeder Dienst einzeln hinsichtlich der Sicherheit bewertet. Als Beispiel soll hier die Aktivierung der Verschlüsselung für Azure SQL-Datenbank dienen.

- **Always Encrypted:** Verwenden Sie den Always Encrypted-Assistenten in SQL Server Management Studio, um ruhende Daten zu schützen.
  - Sie erstellen einen Always Encrypted-Schlüssel, um einzelne Spaltendaten zu verschlüsseln.
  - Always Encrypted-Schlüssel können verschlüsselt in den Datenbankmetadaten oder in vertrauenswürdigen Speichern wie Azure Key Vault gespeichert werden.
  - Um dieses Feature verwenden zu können, sind höchstwahrscheinlich Änderungen an der Anwendung erforderlich.
- **Transparent Data Encryption (TDE):** Schützen Sie die Azure SQL-Datenbank mit Echtzeitverschlüsselung und -entschlüsselung der Datenbank, der zugehörigen Sicherungen und der ruhenden Transaktionsprotokolldateien.
  - TDE ermöglicht die Ausführung von Verschlüsselungsaktivitäten ohne Änderungen auf der Anwendungsebene.
  - TDE kann von Microsoft bereitgestellte Verschlüsselungsschlüssel oder Ihren eigenen Schlüssel (Bring Your Own Key, BYOK) verwenden.

**Weitere Informationen**:

- Weitere Informationen zu [Azure Disk Encryption für virtuelle Computer und VM-Skalierungsgruppen](/azure/security/fundamentals/azure-disk-encryption-vms-vmss).
- Aktivieren von [Azure Disk Encryption für virtuelle Windows-Computer](/azure/virtual-machines/windows/disk-encryption-overview).
- Erfahren Sie mehr über die [Azure Storage-Verschlüsselung für ruhende Daten](/azure/storage/common/storage-service-encryption).
- Lesen Sie die [Übersicht über Always Encrypted](/azure/sql-database/sql-database-always-encrypted-azure-key-vault).
- Lesen Sie über [Transparent Data Encryption für SQL-Datenbank und Azure Synapse](/azure/sql-database/transparent-data-encryption-azure-sql).
- Erfahren Sie mehr über [Transparent Data Encryption für Azure SQL-Datenbank mit einem kundenseitig verwalteten Schlüssel](/azure/sql-database/transparent-data-encryption-byok-azure-sql).

## <a name="best-practice-protect-vms-with-antimalware"></a>Bewährte Methode: Schützen von VMs mit Antischadsoftware

Insbesondere auf älteren virtuellen Computern, die zu Azure migriert wurden, ist unter Umständen nicht die richtige Antischadsoftware installiert. Azure bietet eine kostenlose Endpunktlösung, mit der Sie VMs vor Viren, Spyware und anderer Schadsoftware schützen können.

- Microsoft Antimalware für Azure Cloud Services und virtuelle Computer generiert Warnungen, wenn bekannte schädliche oder unerwünschte Software versucht, sich selbst zu installieren.
- Es handelt sich um eine Lösung mit einem einzelnen Agent, die ohne Benutzereingriff im Hintergrund ausgeführt wird.
- In Azure Security Center können Sie ganz einfach diejenigen VMs identifizieren, auf denen kein Endpunktschutz ausgeführt wird, und bei Bedarf Microsoft Antimalware installieren.

  ![Screenshot: Antischadsoftware für virtuelle Computer](./media/migrate-best-practices-security-management/antimalware.png)
  _Abbildung 1: Antischadsoftware für virtuelle Computer_

**Weitere Informationen**:

- Informationen zu Microsoft Antimalware für Azure finden Sie [hier](/azure/security/fundamentals/antimalware).

## <a name="best-practice-secure-web-apps"></a>Bewährte Methode: Sichern von Web-Apps

Bei migrierten Web-Apps können einige Probleme auftreten:

- In vielen älteren Webanwendungen befinden sich vertrauliche Informationen in Konfigurationsdateien. Dateien, die solche Informationen enthalten, können zu Sicherheitsproblemen führen, wenn Anwendungen gesichert werden oder wenn Anwendungscode in die Quellcodeverwaltung eingecheckt oder daraus ausgecheckt wird.
- Wenn Sie Web-Apps migrieren, die sich auf einem virtuellen Computer befinden, verlagern Sie wahrscheinlich diesen Computer aus einer Umgebung mit lokalem Netzwerk und Firewallschutz in eine Umgebung mit Internetzugriff. Stellen Sie sicher, dass Sie eine Lösung einrichten, die dieselben Aufgaben erfüllt wie Ihre lokalen Schutzressourcen.

Azure bietet folgende Lösungen:

- **Azure Key Vault:** Heute unternehmen Web-App-Entwickler Schritte, um sicherzustellen, dass vertrauliche Informationen nicht aus diesen Dateien ausgelesen werden können. Eine Methode zum Sichern von Informationen besteht darin, diese aus den Dateien zu extrahieren und in einem Azure Key Vault zu speichern.
  - Sie können Key Vault verwenden, um Anwendungsgeheimnisse zentral zu speichern und ihre Verteilung zu steuern. So müssen Sicherheitsinformationen nicht mehr in Anwendungsdateien gespeichert werden.
  - Anwendungen können über URIs sicher und ohne benutzerdefinierten Code auf Informationen im Tresor zugreifen.
  - Mit Azure Key Vault können Sie den Zugriff über Azure-Sicherheitssteuerungen sperren und nahtlos ein Schlüsselrollover implementieren. Microsoft kann Ihre Daten weder einsehen noch extrahieren.
- **App Service-Umgebung für Power Apps:** Wenn eine Anwendung, die Sie migrieren möchten, zusätzlichen Schutz benötigt, können Sie eine App Service-Umgebung und eine Web Application Firewall hinzufügen, um die Anwendungsressourcen zu schützen.
  - Die App Service-Umgebung stellt eine vollständig isolierte und dedizierte Umgebung bereit, in der Anwendungen wie Windows- und Linux-Web-Apps, Docker-Container, mobile Apps und Funktions-Apps ausgeführt werden können.
  - Dies ist hilfreich für Anwendungen auf sehr hoher Ebene, die Isolierung und sicheren Netzwerkzugriff erfordern oder viel Arbeitsspeicher benötigen.
- **Web Application Firewall:** Dieses Feature von Azure Application Gateway bietet zentralisierten Schutz für Web-Apps.
  - Es schützt Web-Apps, ohne das dafür Änderungen am Back-End-Code erforderlich sind.
  - Es schützt mehrere Web-Apps gleichzeitig hinter Application Gateway.
  - Die Web Application Firewall kann mithilfe von Azure Monitor überwacht werden. Die Web Application Firewall ist in Azure Security Center integriert.

  ![Diagramm: Azure Key Vault und sichere Web-Apps](./media/migrate-best-practices-security-management/web-apps.png)
  _Abbildung 2: Azure Key Vault_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure Key Vault](/azure/key-vault/general/overview).
- Erfahren Sie mehr über [Web Application Firewall](/azure/application-gateway/waf-overview).
- Lesen Sie eine [Einführung in App Service-Umgebungen](/azure/app-service/environment/intro).
- Erfahren Sie, wie Sie [eine Web-App so konfigurieren, dass sie Geheimnisse aus Key Vault lesen kann](/azure/key-vault/tutorial-web-application-keyvault).

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Bewährte Methode: Überprüfen von Abonnements und Ressourcenberechtigungen

Wenn Sie Ihre Workloads migrieren und in Azure ausführen, können Mitarbeiter mit Workloadzugriff standortunabhängig arbeiten. Ihr Sicherheitsteam sollte den Zugriff auf Ihre Azure-Mandanten und -Ressourcengruppen in regelmäßigen Abständen überprüfen. Azure bietet Lösungen für die Identitätsverwaltung und die Sicherheit der Zugriffssteuerung (z. B. die rollenbasierte Zugriffssteuerung), um Berechtigungen für den Zugriff auf Azure-Ressourcen zu autorisieren.

- Die rollenbasierte Zugriffssteuerung weist Zugriffsberechtigungen für Sicherheitsprinzipale zu. Sicherheitsprinzipale repräsentieren Benutzer, Gruppen (aus Benutzern), Dienstprinzipale (von Anwendungen und Diensten verwendete Identitäten) und verwaltete Identitäten (automatisch von Azure verwaltete Azure Active Directory-Identitäten).
- Die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) kann Sicherheitsprinzipalen Rollen wie Besitzer, Mitwirkender und Leser zuweisen. Das Feature kann auch Rollendefinitionen (eine Sammlung von Berechtigungen) zuweisen, um die Vorgänge zu definieren, die von den Rollen ausgeführt werden können.
- Die rollenbasierte Zugriffssteuerung kann auch Bereiche festlegen, die die Grenze für eine Rolle definieren. Ein Bereich kann auf verschiedenen Ebenen festgelegt werden, z. B. für Verwaltungsgruppen, Abonnements, Ressourcengruppen oder Ressourcen.
- Stellen Sie sicher, dass Administratoren mit Azure-Zugriff nur auf diejenigen Ressourcen zugreifen können, die Sie zulassen möchten. Wenn die vordefinierten Rollen in Azure nicht differenziert genug sind, können Sie benutzerdefinierte Rollen erstellen, um Zugriffsberechtigungen zu trennen und zu begrenzen.

Stellen Sie sicher, dass Administratoren mit Azure-Zugriff nur auf diejenigen Ressourcen zugreifen können, die Sie zulassen möchten. Wenn die vordefinierten Rollen in Azure nicht differenziert genug sind, können Sie benutzerdefinierte Rollen erstellen, um Zugriffsberechtigungen zu trennen und zu begrenzen.

  ![Screenshot: Zugriffssteuerung](./media/migrate-best-practices-security-management/subscription.png)
  _Abbildung 3: Zugriffssteuerung_

**Weitere Informationen**:

- Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung von Azure (RBAC)](/azure/role-based-access-control/overview).
- Erfahren Sie, wie Sie den Zugriff über [die rollenbasierte Zugriffssteuerung und das Azure-Portal](/azure/role-based-access-control/role-assignments-portal) verwalten.
- Erfahren Sie mehr über [benutzerdefinierte Rollen](/azure/role-based-access-control/custom-roles).

## <a name="best-practice-review-audit-and-security-logs"></a>Bewährte Methode: Überprüfen von Überwachungs- und Sicherheitsprotokollen

Azure Active Directory (Azure AD) stellt Aktivitätsprotokolle bereit, die in Azure Monitor angezeigt werden. Die Protokolle erfassen die Vorgänge, die in Azure-Mandanten ausgeführt werden, und sie erfassen auch, wann und von wem sie ausgeführt werden.

- Überwachungsprotokolle zeigen den Verlauf von Aufgaben im Mandanten an. Protokolle für Anmeldeaktivitäten zeigen, wer die Aufgaben ausgeführt hat.
- Der Zugriff auf Sicherheitsberichte richtet sich nach Ihrer Azure AD-Lizenz. Mit den Free- und Basic-Lizenzen erhalten Sie eine Liste mit Risikobenutzern und -anmeldungen. Mit den Premium-Lizenzen erhalten Sie Informationen zu den zugrunde liegenden Ereignissen.
- Sie können Aktivitätsprotokolle zur Langzeitaufbewahrung und für Datenerkenntnisse an mehrere Endpunkte weiterleiten.
- Gewöhnen Sie sich an, die Protokolle zu überprüfen, oder integrieren Sie Ihre SIEM-Tools (Security Information & Event Management), um Anomalien automatisch zu überprüfen. Ohne Premium-Lizenz müssen Sie viele Analyseaktivitäten selbst oder mithilfe Ihres SIEM-Systems ausführen. Zu diesen Aktivitäten gehört die Suche nach risikobehafteten Anmeldungen und Ereignissen sowie weiteren Benutzerangriffsmustern.

  ![Screenshot: Azure AD-Benutzer und -gruppen](./media/migrate-best-practices-security-management/azure-ad.png)
  _Abbildung 4: Azure AD-Benutzer und -Gruppen_

**Weitere Informationen**:

- Erfahren Sie mehr über [Azure AD-Aktivitätsprotokolle in Azure Monitor](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor).
- Erfahren Sie, wie Sie [Aktivitätsberichte im Azure AD-Portal überwachen](/azure/active-directory/reports-monitoring/concept-audit-logs).

## <a name="best-practice-evaluate-other-security-features"></a>Bewährte Methode: Bewerten anderer Sicherheitsfeatures

Azure bietet weitere Sicherheitsfunktionen, die erweiterte Sicherheitsoptionen bereitstellen. Beachten Sie, dass für einige der folgenden bewährten Methoden Add-On-Lizenzen und Premium-Optionen erforderlich sind.

- **Implementieren von Azure AD-Verwaltungseinheiten:** Das Delegieren von Verwaltungsaufgaben zur Unterstützung der Mitarbeiter nur mit grundlegender Azure-Zugriffssteuerung kann schwierig sein. Supportmitarbeitern Zugriff auf die Verwaltung all dieser Gruppen in Azure AD zu gewähren ist hinsichtlich der Sicherheit der Organisation möglicherweise nicht der ideale Ansatz. Mit Verwaltungseinheiten (Administrative Units, AUs) können Sie Azure-Ressourcen in Container unterteilen, ähnlich wie bei lokalen Organisationseinheiten (Organizational Units, OUs). Um Verwaltungseinheiten verwenden zu können, muss der AU-Administrator über eine Azure AD-Premium-Lizenz verfügen. Weitere Informationen finden Sie unter [Verwalten von Verwaltungseinheiten in Azure Active Directory (Vorschau)](/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Verwenden der mehrstufigen Authentifizierung:** Wenn Sie über eine Azure AD-Premium-Lizenz verfügen, können Sie die mehrstufige Authentifizierung in Ihren Administratorkonten aktivieren und erzwingen. Anmeldeinformationen für Konten sind am meisten durch Phishing gefährdet. Böswillige Benutzer mit Anmeldeinformationen für ein Administratorkonto können folgenschwere Aktionen ausführen und beispielsweise alle Ihre Ressourcengruppen löschen. Sie können die mehrstufige Authentifizierung auf verschiedenen Wegen umsetzen, z. B. per E-Mail, mit einer Authentifikator-App und über Textnachrichten. Als Administrator können Sie die Option auswählen, die sich am einfachsten umsetzen lässt. Die mehrstufige Authentifizierung lässt sich in Richtlinien für die Bedrohungsanalyse und den bedingten Zugriff integrieren, um per Zufallsprinzip eine Antwort auf eine Anforderung für die mehrstufige Authentifizierung anzufordern. Erfahren Sie mehr über [Sicherheitsempfehlungen](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) und das [Einrichten der mehrstufigen Authentifizierung](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementieren des bedingten Zugriffs:** In den meisten kleinen und mittelgroßen Organisationen befinden sich Azure-Administratoren und das Supportteam möglicherweise innerhalb derselben geografischen Region. In diesem Fall stammen die meisten Anmeldungen aus den gleichen Gebieten. Wenn die IP-Adressen dieser Standorte einigermaßen statisch sind, sollten keine Administratoranmeldungen aus Bereichen außerhalb dieser Gebiete zu beobachten sein. Für den Fall, dass ein böswilliger Remotebenutzer an die Anmeldeinformationen eines Administrators gelangt, können Sie Sicherheitsfeatures wie etwa den bedingten Zugriff implementieren und mit der mehrstufigen Authentifizierung kombinieren, um Anmeldungen von Remotestandorten zu verhindern. Dadurch lässt sich ggf. auch die Verwendung gefälschter Standorte über zufällige IP-Adressen unterbinden. Erfahren Sie mehr über den [bedingten Zugriff](/azure/active-directory/conditional-access/overview), und [lesen Sie die bewährten Methoden](/azure/active-directory/conditional-access/best-practices) für den bedingten Zugriff in Azure AD.
- **Überprüfen von Berechtigungen von Enterprise-Anwendungen.** Im Laufe der Zeit wählen Administratoren Links von Microsoft und anderen Anbietern aus, ohne sich über die Auswirkungen auf ihre Organisation im Klaren zu sein. Von Links können Einwilligungsbildschirme angezeigt werden, die Azure-Apps Berechtigungen zuweisen. Über solche Links kann auch Lesezugriff auf Azure AD-Daten oder sogar Vollzugriff zur Verwaltung Ihres gesamten Azure-Abonnements gewährt werden. Sie sollten die Anwendungen regelmäßig überprüfen, für die Ihre Administratoren und Benutzer Zugriff auf Azure-Ressourcen gewährt haben. Stellen Sie sicher, dass diese Anwendungen nur über die Berechtigungen verfügen, die erforderlich sind. Darüber hinaus können Sie Benutzern viertel- oder halbjährlich eine E-Mail mit einem Link zu Anwendungsseiten senden, um den Benutzern die Anwendungen ins Bewusstsein zu rufen, denen sie Zugriff auf ihre Organisationsdaten gewährt haben. Weitere Informationen finden Sie unter [Unerwartete Anwendung in der Liste meiner Anwendungen](/azure/active-directory/manage-apps/application-types) sowie unter [Entfernen einer Benutzer- oder Gruppenzuweisung aus einer Unternehmens-App in Azure Active Directory](/azure/active-directory/manage-apps/remove-user-or-group-access-portal).

## <a name="managed-migrated-workloads"></a>Verwalten von migrierten Workloads

In diesem Abschnitt finden Sie einige Empfehlungen für bewährte Methoden im Zusammenhang mit der Azure-Verwaltung:

- Best Practices für Azure-Ressourcengruppen und -Ressourcen, einschließlich intelligenter Benennung, Verhindern von versehentlichem Löschen, Verwalten von Ressourcenberechtigungen und effektivem Markieren von Ressourcen.
- Erhalten Sie einen schnellen Überblick über die Verwendung von Blaupausen zum Erstellen und Verwalten Ihrer Bereitstellungsumgebungen.
- Sehen Sie sich Azure-Beispielarchitekturen an, während Sie Ihre Bereitstellungen nach der Migration erstellen.
- Wenn Sie über mehrere Abonnements verfügen, können Sie diese in Verwaltungsgruppen zusammenfassen und Governanceeinstellungen auf diese Gruppen anwenden.
- Wenden Sie Konformitätsrichtlinien auf Ihre Azure-Ressourcen an.
- Erstellen Sie eine Strategie für Business Continuity & Disaster Recovery (BCDR), um bei Ausfällen Ihre Daten zu sichern, Ihre Umgebung stabil zu halten und für die fortlaufende Ausführung Ihrer Ressourcen zu sorgen.
- Stellen Sie virtuelle Computer in Verfügbarkeitsgruppen zusammen, um für Stabilität und Hochverfügbarkeit zu sorgen. Verwenden Sie verwaltete Datenträger, um die Verwaltung von VM-Datenträgern und Speicher zu vereinfachen.
- Ermöglichen Sie die Diagnoseprotokollierung für Azure-Ressourcen, erstellen Sie Warnungen und Playbooks für die proaktive Problembehandlung, und verwenden Sie das Azure-Dashboard, um eine einheitliche Ansicht der Integrität und des Status Ihrer Bereitstellung zu erhalten.
- Erfahren Sie mehr über Ihren Azure-Supportplan und wie Sie ihn implementieren, profitieren Sie von Best Practices zur Aktualisierung Ihrer virtuellen Computer, und richten Sie Prozesse für das Change Management ein.

## <a name="best-practice-name-resource-groups"></a>Bewährte Methode: Benennen von Ressourcengruppen

Verwenden Sie aussagekräftige Namen für Ihre Ressourcengruppen, die Administratoren und Mitglieder des Supportteams einfach erkennen und erfassen können. Dies trägt erheblich zur Verbesserung der Produktivität und Effizienz bei.

Wenn Sie Ihre lokale Active Directory-Instanz über Azure AD Connect mit Azure AD synchronisieren, empfiehlt es sich gegebenenfalls, die Namen der lokalen Sicherheitsgruppen an die Namen der Ressourcengruppen in Azure anzupassen.

  ![Screenshot: Ressourcengruppennamen](./media/migrate-best-practices-security-management/naming.png)
  _Abbildung 5: Ressourcengruppennamen_

**Weitere Informationen**:

- Erfahren Sie mehr über [Empfohlene Benennungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md).

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Bewährte Methode: Implementieren von Sperren für Ressourcengruppen

Niemand möchte, dass eine Ressourcengruppe verschwindet, weil sie versehentlich gelöscht wurde. Wir empfehlen die Implementierung von Löschsperren, um dies zu verhindern.

  ![Screenshot: Löschsperren](./media/migrate-best-practices-security-management/locks.png)
  _Abbildung 6: Löschsperren_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Sperren von Ressourcen, um unerwartete Änderungen zu verhindern](/azure/azure-resource-manager/resource-group-lock-resources).

## <a name="best-practice-understand-resource-access-permissions"></a>Bewährte Methode: Verstehen der Berechtigungen für den Ressourcenzugriff

Ein Abonnementbesitzer hat Zugriff auf alle Ressourcengruppen und Ressourcen in Ihrem Abonnement.

- Fügen Sie dieser wertvollen Zuweisung nur wenige Benutzer hinzu. Sie müssen die Auswirkungen dieser Art von Berechtigungen genau kennen, um für die Sicherheit und Stabilität Ihrer Umgebung zu sorgen.
- Stellen Sie sicher, dass Sie Ressourcen in geeigneten Ressourcengruppen platzieren:
  - Fassen Sie Ressourcen mit ähnlichem Lebenszyklus zusammen. Im Idealfall sollte es nicht notwendig sein, eine Ressource zu verschieben, wenn Sie eine vollständige Ressourcengruppe löschen müssen.
  - Ressourcen, die eine Funktion oder Workload unterstützen, sollten zur Vereinfachung der Verwaltung gruppiert werden.

**Weitere Informationen**:

- Erfahren Sie mehr über das [Organisieren von Abonnements und Ressourcengruppen](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).

## <a name="best-practice-tag-resources-effectively"></a>Bewährte Methode: Effektives Markieren von Ressourcen

Häufig bietet die alleinige Verwendung eines Ressourcengruppennamens für Ressourcen nicht genügend Metadaten für die effektive Implementierung von Mechanismen wie die interne Abrechnung oder die Verwaltung innerhalb eines Abonnements.

- Es empfiehlt sich daher, mithilfe von Azure-Tags hilfreiche Metadaten hinzuzufügen, die abgefragt und gemeldet werden können.
- Tags sind eine Möglichkeit, Ressourcen mit von Ihnen definierten Eigenschaften logisch zu organisieren. Tags können auf Ressourcengruppen oder direkt auf Ressourcen angewendet werden.
- Tags können auf eine Ressourcengruppe oder auf einzelne Ressourcen angewendet werden. Ressourcengruppentags werden nicht an die Ressourcen in der Gruppe vererbt.
- Sie können die Markierung mithilfe von PowerShell oder Azure Automation automatisieren oder einzelne Gruppen oder Ressourcen markieren.
- Wenn Sie ein System für Anforderungsmanagement und Change Management eingerichtet haben, können Sie ganz einfach die Informationen in der Anforderung verwenden, um Ihre unternehmensspezifischen Ressourcentags aufzufüllen.

  ![Screenshot: Markieren](./media/migrate-best-practices-security-management/tagging.png)
  _Abbildung 7: Markieren_

**Weitere Informationen**:

- Erfahren Sie mehr über [Markierungen und Tageinschränkungen](/azure/azure-resource-manager/management/tag-resources).
- Sehen Sie sich [PowerShell- und CLI-Beispiele für das Einrichten von Tags und das Anwenden von Tags von einer Ressourcengruppe auf die zugehörigen Ressourcen](/azure/azure-resource-manager/management/tag-resources#powershell) an.
- [Lesen](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) Sie Best Practices zum Markieren in Azure.

## <a name="best-practice-implement-blueprints"></a>Bewährte Methode: Implementieren von Blaupausen

Genau wie eine Blaupause, mit der Ingenieure oder Architekten die Entwurfsparameter für ein Projekt skizzieren, ermöglicht es der Azure Blueprints-Dienst Cloudarchitekten und zentralen IT-Gruppen, eine wiederholbare Gruppe von Azure-Ressourcen zu definieren. Dies vereinfacht die Implementierung und Einhaltung der Standards, Muster und Anforderungen einer Organisation. Mit Azure Blueprints können Entwicklungsteams schnell neue Umgebungen entwickeln und erstellen, die die Konformitätsanforderungen der Organisation erfüllen. Diese neuen Umgebungen verfügen über eine Reihe integrierter Komponenten (z. B. Netzwerk), um die Entwicklung und Bereitstellung zu beschleunigen.

- Verwenden Sie Blaupausen, um die Bereitstellung von Ressourcengruppen, Azure Resource Manager-Vorlagen sowie Richtlinien- und Rollenzuweisungen zu orchestrieren.
- Speichern Sie Blaupausen in einem global verteilten Dienst: Azure Cosmos DB. Blaupausenobjekte werden in mehreren Azure-Regionen repliziert. Die Replikation sorgt für kurze Wartezeiten, Hochverfügbarkeit und konsistenten Zugriff auf Blaupausen – unabhängig von der Region, in der Ressourcen durch eine Blaupause bereitgestellt werden.

**Weitere Informationen**:

- [Erfahren Sie mehr](/azure/governance/blueprints/overview) über Blaupausen.
- Sehen Sie sich ein [Beispiel für eine Blaupause zum Beschleunigen von KI im Gesundheitswesen](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) an.

## <a name="best-practice-review-azure-reference-architectures"></a>Bewährte Methode: Überprüfen von Referenzarchitekturen

Das Erstellen sicherer, skalierbarer und verwaltbarer Workloads in Azure kann eine große Herausforderung sein. Angesichts fortlaufender Änderungen kann es schwierig sein, bei verschiedenen Features auf dem Laufenden zu bleiben, um eine optimale Umgebung sicherzustellen. Beim Entwerfen und Migrieren Ihrer Workloads kann es nützlich sein, über eine Referenz zu verfügen, aus der Sie nützliche Informationen erhalten können. Azure und die Azure-Partner haben verschiedene Referenzarchitekturen als Muster für verschiedene Arten von Umgebungen erstellt. Diese Muster bieten Anregungen, aus denen Sie lernen und auf denen Sie aufbauen können.

Die Referenzarchitekturen sind nach Szenario sortiert. Sie enthalten Best Practices und Ratschläge zu Verwaltung, Verfügbarkeit, Skalierbarkeit und Sicherheit. Die App Service-Umgebung stellt eine vollständig isolierte und dedizierte Umgebung bereit, in der Anwendungen wie Windows- und Linux-Web-Apps, Docker-Container, mobile Apps und Funktionen ausgeführt werden können. App Service ergänzt Ihre Anwendung um leistungsfähige Azure-Features, z.B. Sicherheit, Lastenausgleich, automatische Skalierung und automatisierte Verwaltung. Sie können auch die Vorteile der DevOps-Funktionen des Diensts nutzen, z.B. Continuous Deployment über Azure DevOps und GitHub, Paketverwaltung, Stagingumgebungen, benutzerdefinierte Domäne und SSL-Zertifikate. App Service ist hilfreich bei Anwendungen, die Isolierung und sicheren Netzwerkzugriff erfordern, sowie für solche Anwendungen, die eine große Menge an Arbeitsspeicher sowie weitere skalierbare Ressourcen nutzen.

**Weitere Informationen**:

- Erfahren Sie mehr über [Azure-Referenzarchitekturen](/azure/architecture/reference-architectures).
- Sehen Sie sich [Azure-Beispielszenarien](/azure/architecture/example-scenario) an.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Bewährte Methode: Verwalten von Ressourcen mit Azure-Verwaltungsgruppen

Wenn Ihre Organisation über mehrere Abonnements verfügt, müssen Sie Zugriff, Richtlinien und Konformität für diese Abonnements verwalten. Azure-Verwaltungsgruppen stellen einen abonnementübergreifenden Bereich dar. Hier einige Tipps:

- Sie organisieren Abonnements in Containern, die als Verwaltungsgruppen bezeichnet werden, und wenden Governancebedingungen darauf an.
- Alle Abonnements in einer Verwaltungsgruppe erben automatisch die Bedingungen der Verwaltungsgruppe.
- Verwaltungsgruppen ermöglichen unabhängig von der Art Ihrer Abonnements die Verwaltung auf Unternehmensniveau in großem Umfang.
- Sie können z.B. die Richtlinie einer Verwaltungsgruppe anwenden, die die Regionen einschränkt, in denen VMs erstellt werden können. Diese Richtlinie wird auf alle Verwaltungsgruppen, Abonnements und Ressourcen in dieser Verwaltungsgruppe angewandt.
- Sie können eine flexible Struktur aus Verwaltungsgruppen und Abonnements aufbauen, um Ihre Ressourcen für eine einheitliche Richtlinien- und Zugriffsverwaltung in einer Hierarchie zu organisieren.

Das folgende Diagramm zeigt anhand eines Beispiels das Erstellen einer Hierarchie für die Governance unter Verwendung von Verwaltungsgruppen:

  ![Diagramm: Verwaltungsgruppen](./media/migrate-best-practices-security-management/management-groups.png)
  _Abbildung 8: Verwaltungsgruppen_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Organisieren von Ressourcen in Verwaltungsgruppen](/azure/governance/management-groups).

## <a name="best-practice-deploy-azure-policy"></a>Bewährte Methode: Bereitstellen von Azure Policy

Azure Policy ist ein Dienst, mit dem Sie Richtlinien erstellen, zuweisen und verwalten können. Richtlinien erzwingen verschiedene Regeln und Effekte für Ihre Ressourcen, damit diese stets mit Ihren Unternehmensstandards und Vereinbarungen zum Servicelevel konform bleiben.

Azure Policy bewertet Ihre Ressourcen und sucht nach Ressourcen, die nicht mit Ihren Richtlinien konform sind. Sie können beispielsweise eine Richtlinie erstellen, die nur eine bestimmte SKU-Größe für virtuelle Computer in Ihrer Umgebung zulässt. Azure Policy wertet diese Einstellung beim Erstellen und Aktualisieren von Ressourcen sowie beim Überprüfen vorhandener Ressourcen aus. Hinweis: Azure stellt einige integrierte Richtlinien bereit, die Sie zuweisen können. Sie können aber auch eigene Richtlinien erstellen.

  ![Screenshot: Azure Policy](./media/migrate-best-practices-security-management/policy.png)
  _Abbildung 9: Azure Policy_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure Policy](/azure/governance/policy/overview).
- Erfahren Sie mehr über das [Erstellen und Verwalten von Richtlinien zum Durchsetzen der Konformität](/azure/governance/policy/tutorials/create-and-manage).

## <a name="best-practice-implement-a-bcdr-strategy"></a>Bewährte Methode: Implementieren einer BCDR-Strategie

Die Planung von Business Continuity & Disaster Recovery (BCDR) ist eine wichtige Aufgabe, die im Rahmen der Azure-Migrationsplanung durchgeführt werden sollte. Rechtlich gesehen enthalten Ihre Verträge möglicherweise eine Klausel zu _höherer Gewalt_, die Sie bei unabwendbaren Ereignissen wie Wirbelstürmen oder Erdbeben von Verpflichtungen entbindet. Sie haben aber auch Verpflichtungen in der Hinsicht, dass Sie die Ausführung und bei Bedarf die Wiederherstellung von Diensten in einem Notfall sicherstellen müssen. Die Fähigkeit, diese Verpflichtungen zu erfüllen, kann über die Zukunft Ihres Unternehmens entscheiden.

Allgemein gesagt muss Ihre BCDR-Strategie Folgendes berücksichtigen:

- **Datensicherung:** Schützen Sie Ihre Daten, sodass Sie diese nach einem Ausfall einfach wiederherstellen können.
- **Notfallwiederherstellung:** Sorgen Sie für Stabilität und Verfügbarkeit Ihrer Anwendungen nach einem Ausfall.

### <a name="set-up-bcdr"></a>Einrichten von BCDR

Beachten Sie bei der Migration zu Azure Folgendes: Die Azure-Plattform bietet zwar einige integrierte Resilienzfeatures, Ihre Azure-Bereitstellung muss jedoch auch entsprechend gestaltet sein, um von diesen Features profitieren zu können.

- Ihre BCDR-Lösung richtet sich nach den Zielen Ihres Unternehmens und wird durch Ihre Azure-Bereitstellungsstrategie beeinflusst. IaaS-Bereitstellungen (Infrastructure-as-a-Service) und PaaS-Bereitstellungen (Platform as a Service) stellen unterschiedliche Herausforderungen an Ihre Business Continuity & Disaster Recovery-Lösung.
- Die implementierte BCDR-Lösung sollte regelmäßig überprüft werden, um sicherzustellen, dass Ihre Strategie weiterhin sinnvoll ist.

### <a name="back-up-an-iaas-deployment"></a>Sichern einer IaaS-Bereitstellung

In den meisten Fällen wird eine lokale Workload nach der Migration außer Betrieb genommen, und Ihre lokale Strategie für die Sicherung von Daten muss erweitert oder ersetzt werden. Wenn Sie Ihr gesamtes Rechenzentrum zu Azure migrieren, müssen Sie mithilfe von Azure-Technologien oder integrierten Drittanbieterlösungen eine vollständige Sicherungslösung entwerfen und implementieren.

Ziehen Sie für Workloads, die auf Azure-IaaS-VMs ausgeführt werden, folgende Sicherungslösungen in Betracht:

- **Azure Backup:** Azure Backup bietet anwendungskonsistente Sicherungen für Azure-Windows- und -Linux-VMs.
- **Speichermomentaufnahmen:** Dieses Feature erstellt Momentaufnahmen vom Blobspeicher.

#### <a name="azure-backup"></a>Azure Backup

Azure Backup erstellt Datenwiederherstellungspunkte, die in Azure Storage gespeichert werden. Azure Backup kann Azure-VM-Datenträger und Azure File Storage (Vorschau) sichern. Azure Files stellt Dateifreigaben in der Cloud bereit, die über den Server Message Block (SMB) zugänglich sind.

Virtuelle Computer können mithilfe von Azure Backup wie folgt gesichert werden:

- **Direkte Sicherung aus VM-Einstellungen:** Sie können VMs mit Azure Backup direkt über die VM-Optionen im Azure-Portal sichern. Sie können eine VM einmal täglich sichern und den VM-Datenträger bei Bedarf wiederherstellen. Azure Backup erstellt anwendungsabhängige Datenmomentaufnahmen, und es wird kein Agent auf der VM installiert.
- **Direkte Sicherung in einem Recovery Services-Tresor:** Sie können Ihre IaaS-VMs durch Bereitstellen eines Azure Backup-Recovery Services-Tresors sichern. Dies bietet einen einzelnen Speicherort zum Nachverfolgen und Verwalten von Sicherungen und ermöglicht differenzierte Sicherungs- und Wiederherstellungsoptionen. Die Sicherung erfolgt bis zu dreimal am Tag auf Datei- und Ordnerebene. Sie ist nicht anwendungsabhängig, und Linux wird nicht unterstützt. Installieren Sie den MARS-Agent (Microsoft Azure Recovery Services) auf jeder VM, die Sie mit dieser Methode sichern möchten.
- **Schützen von VMs mit Azure Backup Server.** Azure Backup Server ist kostenlos in Azure Backup enthalten. VMs werden im lokalen Azure Backup Server-Speicher gesichert. Danach wird Azure Backup Server in einem Tresor in Azure gesichert. Azure Backup ist anwendungsabhängig und bietet vollständige Granularität für die Häufigkeit und Aufbewahrung von Sicherungen. Sie können Sicherungen auf Anwendungsebene z. B. für SQL Server oder SharePoint ausführen.

Zur Gewährleistung der Sicherheit werden Daten von Azure Backup bei der Übertragung mit AES-256 verschlüsselt. Die Daten werden per HTTPS an Azure gesendet. Gesicherte ruhende Daten in Azure werden mit [Azure Storage-Verschlüsselung](/azure/storage/common/storage-service-encryption) verschlüsselt.

![Screenshot: Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
_Abbildung 10: Azure Backup_

**Weitere Informationen**:

- Weitere Informationen zu [Azure Backup](/azure/backup/backup-overview)
- Planen Sie eine [Sicherungsinfrastruktur für Azure-VMs](/azure/backup/backup-azure-vms-introduction).

#### <a name="storage-snapshots"></a>Speichermomentaufnahmen

Azure-VMs werden als Seitenblobs in Azure Storage gespeichert. Momentaufnahmen erfassen den Blobzustand zu einem bestimmten Zeitpunkt. Als alternative Sicherungsmethode für Azure-VM-Datenträger können Sie eine Momentaufnahme von Speicherblobs erfassen und in ein anderes Speicherkonto kopieren.

Sie können ein vollständiges Blob kopieren oder eine inkrementelle Momentaufnahmekopie verwenden, um nur Deltaänderungen zu kopieren und den Speicherplatz zu reduzieren. Als zusätzliche Vorsichtsmaßnahme können Sie das vorläufige Löschen für Blobspeicherkonten aktivieren. Ist dieses Feature aktiviert, wird ein Blob nicht sofort gelöscht, sondern zum Löschen markiert. Während des Übergangszeitraums kann das Blob wiederhergestellt werden.

**Weitere Informationen**:

- Erfahren Sie mehr über [Azure-Blobspeicher](/azure/storage/blobs/storage-blobs-introduction).
- Erfahren Sie, wie Sie eine [Blobmomentaufnahme erstellen](/azure/storage/blobs/storage-blob-snapshots).
- [Sehen Sie sich ein Beispielszenario](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) für die Sicherung des Blobspeichers an.
- Weitere Informationen zum [vorläufigen Löschen für Blobs](/azure/storage/blobs/storage-blob-soft-delete).
- [Notfallwiederherstellung und erzwungenes Failover (Vorschau) in Azure Storage](/azure/storage/common/storage-disaster-recovery-guidance)

#### <a name="third-party-backup"></a>Sicherungslösungen von Drittanbietern

Zusätzlich können Sie Drittanbieterlösungen verwenden, um Azure-VMs und -Speichercontainer in einem lokalen Speicher oder bei anderen Cloudanbietern zu sichern. Weitere Informationen finden Sie unter den [Sicherungslösungen im Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1).

### <a name="set-up-disaster-recovery-for-iaas-applications"></a>Einrichten der Notfallwiederherstellung für IaaS-Anwendungen

Zusätzlich zum Schutz der Daten muss bei der BCDR-Planung berücksichtigt werden, wie Anwendungen und Workloads bei einem Notfall verfügbar gehalten werden. Ziehen Sie für Workloads, die auf virtuellen Azure-IaaS-Computern und in Azure Storage ausgeführt werden, die Lösungen in den folgenden Abschnitten in Betracht.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery ist der primäre Azure-Dienst, mit dem sichergestellt werden kann, dass virtuelle Azure-Computer im Falle eines Ausfalls online geschaltet und VM-Anwendungen verfügbar gemacht werden können.

Von Site Recovery werden virtuelle Computer aus einer primären Azure-Region in einer sekundären Azure-Region repliziert. Bei einem Notfall führen Sie ein Failover der virtuellen Computer in der primären Region durch und greifen in der sekundären Region weiterhin normal auf sie zu. Wenn der Betrieb wieder normal läuft, können Sie ein Failback der VMs zur primären Region ausführen.

  ![Diagramm: Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)
  _Abbildung 11: Site Recovery_

**Weitere Informationen**:

- Sehen Sie sich [Notfallwiederherstellungsszenarien für Azure-VMs](/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) an.
- Erfahren Sie, wie Sie die [Notfallwiederherstellung für eine Azure-VM nach der Migration einrichten](/azure/site-recovery/azure-to-azure-replicate-after-migration).

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Bewährte Methode: Verwenden von verwalteten Datenträgern und Verfügbarkeitsgruppen

Azure verwendet Verfügbarkeitsgruppen, um VMs logisch zusammenzufassen und in einer Gruppe von anderen Ressourcen zu isolieren. VMs in einer Verfügbarkeitsgruppe werden auf mehrere Fehlerdomänen mit separaten Subsystemen verteilt, die vor lokalen Ausfällen geschützt sind. Die VMs sind auch auf mehrere Updatedomänen verteilt und verhindern gleichzeitige Neustarts aller VMs in der Gruppe.

Verwaltete Azure-Datenträger vereinfachen die Datenträgerverwaltung bei Azure Virtual Machines durch Verwaltung der Speicherkonten, die den VM-Datenträgern zugeordnet sind.

- Verwenden Sie nach Möglichkeit verwaltete Datenträger. Sie müssen nur den gewünschten Speichertyp und die erforderliche Datenträgergröße angeben, und Azure erstellt und verwaltet den Datenträger im Hintergrund für Sie.
- Sie können vorhandene Datenträger in verwaltete Datenträger konvertieren.
- Sie sollten VMs in Verfügbarkeitsgruppen erstellen, um eine hohe Resilienz und Verfügbarkeit zu erzielen. Bei geplanten oder ungeplanten Ausfällen stellen Verfügbarkeitsgruppen sicher, dass mindestens eine VM in der Gruppe verfügbar bleibt.

  ![Diagramm: Verwaltete Datenträger](./media/migrate-best-practices-security-management/managed-disks.png)
  _Abbildung 12: Verwaltete Datenträger_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über verwaltete Datenträger](/azure/virtual-machines/windows/managed-disks-overview).
- Erfahren Sie mehr über das [Konvertieren von Datenträgern in verwaltete Datenträger](/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks).
- Erfahren Sie, wie Sie die [Verfügbarkeit virtueller Windows-Computer in Azure verwalten](/azure/virtual-machines/windows/manage-availability).

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Bewährte Methode: Überwachen der Ressourcennutzung und -leistung

Sie haben Ihre Workloads möglicherweise aufgrund der enormen Skalierungsfunktionen nach Azure verlagert. Die Verlagerung allein bedeutet aber nicht, dass Azure ohne Eingaben Ihrerseits automatisch eine Skalierung implementiert. Zwei Beispiele:

- Wenn Ihre Marketingorganisation einen neuen Werbespot im Fernsehen schaltet, der 300 Prozent mehr Datenverkehr verursacht, könnte dies zu Problemen mit der Verfügbarkeit der Website führen. Ihre frisch migrierte Workload könnte die zugewiesenen Obergrenzen erreichen und abstürzen.
- Im Falle eines verteilten Denial-of-Service-Angriffs (DDoS) auf Ihre migrierte Workload soll keine Skalierung erfolgen. Stattdessen soll die Quelle der Angriffe daran gehindert werden, Ihre Ressourcen zu erreichen.

Für diese beiden Fälle gibt es unterschiedliche Lösungen, aber Sie müssen in beiden Fällen wissen, was passiert. Dazu dient die Überwachung der Nutzung und Leistung.

- Azure Monitor unterstützt Sie dabei, diese Metriken zu ermitteln und mithilfe von Warnungen, automatischer Skalierung, Event Hubs und Logik-Apps auf diese zu reagieren.
- Darüber hinaus können Sie Ihre SIEM-Drittanbieteranwendung integrieren, um die Azure-Protokolle auf Überprüfungs- und Leistungsereignisse zu überwachen.

  ![Screenshot: Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
  _Abbildung 13: Azure Monitor_

**Weitere Informationen**:

- Weitere Informationen finden Sie unter [Azure Monitor](/azure/azure-monitor/overview).
- [Informieren Sie sich über Best Practices](/azure/architecture/best-practices/monitoring) für die Überwachung und Diagnose.
- Erfahren Sie mehr über die [automatische Skalierung](/azure/architecture/best-practices/auto-scaling).
- Erfahren Sie, wie Sie [Azure-Daten an ein SIEM-Tool weiterleiten](/azure/security-center/security-center-export-data-to-siem).

## <a name="best-practice-enable-diagnostic-logging"></a>Bewährte Methode: Aktivieren der Diagnoseprotokollierung

Azure-Ressourcen generieren recht viele Protokollierungsmetrik- und Telemetriedaten. Standardmäßig ist bei den meisten Ressourcentypen die Diagnoseprotokollierung nicht aktiviert. Indem Sie die Diagnoseprotokollierung für Ihre Ressourcen aktivieren, können Sie Protokollierungsdaten abfragen und basierend darauf Warnungen und Playbooks erstellen.

Wenn Sie die Diagnoseprotokollierung aktivieren, verfügt jede Ressource über einen bestimmten Satz von Kategorien. Sie können eine oder mehrere Protokollierungskategorien sowie einen Speicherort für die Protokolldaten auswählen. Protokolle können an Event Hub, Azure Monitor-Protokolle oder ein Speicherkonto gesendet werden.

![Screenshot: Diagnoseprotokollierung](./media/migrate-best-practices-security-management/diagnostics.png)
_Abbildung 14: Diagnoseprotokollierung_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Erfassen und Nutzen von Protokolldaten](/azure/azure-monitor/platform/platform-logs-overview).
- Erfahren Sie, was für die [Diagnoseprotokollierung](/azure/azure-monitor/platform/diagnostic-logs-schema) unterstützt wird.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Bewährte Methode: Einrichten von Warnungen und Playbooks

Wenn die Diagnoseprotokollierung für Azure-Ressourcen aktiviert ist, können Sie damit beginnen, Protokollierungsdaten zu verwenden, um benutzerdefinierte Warnungen zu erstellen.

- Warnungen benachrichtigen Sie proaktiv, wenn bestimmte Bedingungen in Ihren Überwachungsdaten gefunden werden. Dann können Sie die Probleme beheben, bevor Ihre Systembenutzer diese bemerken. Sie können Warnungen zu Metrikwerten, Protokollsuchabfragen, Aktivitätsprotokollereignissen, Plattformintegrität und Websiteverfügbarkeit einrichten.
- Wenn Warnungen ausgelöst werden, können Sie ein Logik-App-Playbook ausführen. Mit einem Playbook können Sie eine Antwort auf eine bestimmte Warnung automatisieren und orchestrieren. Playbooks basieren auf Azure Logic Apps. Sie können Playbooks selbst oder basierend auf Logik-App-Vorlagen erstellen.
- Ein einfaches Beispiel: Sie können eine Warnung erstellen, die ausgelöst wird, wenn für eine Netzwerksicherheitsgruppe ein Portscan ausgeführt wird. Sie können ein Playbook einrichten, das ausgeführt wird und die IP-Adresse der Scanquelle sperrt.
- Ein weiteres Beispiel ist eine Anwendung mit einem Arbeitsspeicherverlust. Wenn die Arbeitsspeichernutzung einen bestimmten Punkt erreicht, kann ein Playbook den Prozess stoppen und neu starten.

  ![Screenshot: Warnungen](./media/migrate-best-practices-security-management/alerts.png)
  _Abbildung 15: Warnungen_

**Weitere Informationen**:

- Erfahren Sie mehr über [Warnungen](/azure/azure-monitor/platform/alerts-overview).
- Informieren Sie sich über [Sicherheitsplaybooks, die auf Security Center-Warnungen reagieren](/azure/security-center/security-center-playbooks).

## <a name="best-practice-use-the-azure-dashboard"></a>Bewährte Methode: Verwenden des Azure-Dashboards

Das Azure-Portal ist eine webbasierte einheitliche Konsole zum Erstellen, Verwalten und Überwachen aller Komponenten – von einfachen Web-Apps bis hin zu komplexen Cloudanwendungen. Es enthält ein anpassbares Dashboard und Optionen für Barrierefreiheit.

- Sie können mehrere Dashboards erstellen und für andere Benutzer freigeben, die Zugriff auf Ihre Azure-Abonnements haben.
- Mit diesem Freigabemodell erhält Ihr Team Einblick in die Azure-Umgebung, sodass die Teammitglieder Systeme in der Cloud proaktiv verwalten können.

  ![Screenshot: Azure-Dashboard](./media/migrate-best-practices-security-management/dashboard.png)
  _Abbildung 16: Azure-Dashboard_

**Weitere Informationen**:

- Erfahren Sie, wie Sie ein [Dashboard erstellen](/azure/azure-portal/azure-portal-dashboards).
- Erfahren Sie mehr über die [Dashboardstruktur](/azure/azure-portal/azure-portal-dashboards-structure).

## <a name="best-practice-understand-support-plans"></a>Bewährte Methode: Verstehen der Supportpläne

Sie müssen zu einem bestimmten Zeitpunkt mit Ihrem Supportteam oder den Microsoft-Supportmitarbeitern zusammenarbeiten. Es ist von entscheidender Bedeutung, eine Reihe von Richtlinien und Verfahren für den Support in Szenarien wie z.B. einer Notfallwiederherstellung einzurichten. Darüber hinaus müssen Ihre Administratoren und Supportmitarbeiter in der Implementierung dieser Richtlinien geschult sein.

- Im unwahrscheinlichen Fall, dass ein Problem mit einem Azure-Dienst sich auf Ihre Workload auswirkt, müssen Ihre Administratoren wissen, wie sie auf möglichst geeignete und effiziente Weise ein Supportticket an Microsoft übermitteln.
- Machen Sie sich mit den verschiedenen Supportplänen vertraut, die für Azure angeboten werden. Diese reichen von Reaktionszeiten für Developer-Instanzen bis hin zu Premier Support mit einer Reaktionszeit von weniger als 15 Minuten.

  ![Screenshot: Supportpläne](./media/migrate-best-practices-security-management/support.png)
  _Abbildung 17: Supportpläne_

**Weitere Informationen**:

- Lesen Sie eine [Übersicht über Azure-Supportpläne](https://azure.microsoft.com/support/options).
- Erfahren Sie mehr über [Vereinbarungen zum Servicelevel (SLAs)](https://azure.microsoft.com/support/legal/sla).

## <a name="best-practice-manage-updates"></a>Bewährte Methode: Verwalten von Updates

Azure-VMs immer mit den neuesten Betriebssystem- und Softwareupdates auf dem neuesten Stand zu halten, ist eine gewaltige Aufgabe. Die Fähigkeit, alle virtuellen Computer sowie die erforderlichen Updates zu ermitteln und diese Updates automatisch zu pushen, ist äußerst wertvoll.

- Sie können die Lösung „Updateverwaltung“ in Azure Automation zum Verwalten von Betriebssystemupdates verwenden. Das gilt für Windows- und Linux-Computer, die in Azure, lokal oder bei anderen Cloudanbietern bereitgestellt werden.
- Verwenden Sie die Updateverwaltung auch, um schnell den Status der verfügbaren Updates auf allen Agent-Computern auszuwerten und die Installation der Updates zu verwalten.
- Sie können die Updateverwaltung für virtuelle Computer direkt in einem Azure Automation-Konto aktivieren. Sie können auch eine einzelne VM über die VM-Seite im Azure-Portal aktualisieren.
- Darüber hinaus können virtuelle Azure-Computer bei System Center Configuration Manager registriert werden. Danach können Sie die Configuration Manager-Workload zu Azure migrieren und Berichterstellung und Softwareupdates über eine einzelne Webschnittstelle abwickeln.

  ![Diagramm: VM-Updates](./media/migrate-best-practices-security-management/updates.png)
  _Abbildung 18: Updates_

**Weitere Informationen**:

- Erfahren Sie mehr über die [Updateverwaltung in Azure](/azure/automation/update-management/overview).
- Erfahren Sie mehr über die [Integration von Configuration Manager mit der Lösung „Updateverwaltung“](/azure/automation/oms-solution-updatemgmt-sccmintegration).
- [Häufig gestellte Fragen](/sccm/core/understand/configuration-manager-on-azure) zu Configuration Manager in Azure.

## <a name="implement-a-change-management-process"></a>Implementieren eines Change Management-Prozesses

Wie bei jedem Produktionssystem kann sich jede Art von Änderung auf Ihre Umgebung auswirken. Ein Change Management-Prozess, in dem Anforderungen gesendet werden müssen, damit Änderungen am Produktionssystem vorgenommen werden können, ist eine wertvolle Ergänzung zu Ihrer migrierten Umgebung.

- Sie können Best Practices-Frameworks für das Change Management erstellen, um bei Administratoren und Supportmitarbeitern das Bewusstsein für solche Prozesse zu schärfen.
- Sie können Azure Automation verwenden, um Unterstützung bei der Konfigurationsverwaltung und Änderungsnachverfolgung für Ihre migrierten Workflows zu erhalten.
- Wenn Sie einen Change Management-Prozess erzwingen, können Sie Überwachungsprotokolle verwenden, um Azure-Änderungsprotokolle mit vorhandenen Änderungsanforderungen zu verknüpfen. Wenn Sie daraufhin eine Änderung bemerken, die ohne entsprechende Änderungsanforderung durchgeführt wurde, können Sie untersuchen, warum der Prozess nicht wie gewünscht funktioniert hat.

Azure bietet in Azure Automation eine Lösung für die Änderungsnachverfolgung:

- Die Lösung verfolgt Änderungen an Windows- und Linux-Software und -Dateien, an Windows-Registrierungsschlüsseln, an Windows-Diensten und an Linux-Daemons nach.
- Änderungen an überwachten Servern werden zur Verarbeitung an Azure Monitor gesendet.
- Auf die empfangenen Daten wird Logik angewendet, und der Clouddienst zeichnet die Daten auf.
- Im Dashboard der Änderungsnachverfolgung können Sie ganz einfach die Änderungen erkennen, die an Ihrer Serverinfrastruktur vorgenommen wurden.

  ![Screenshot: Change Management](./media/migrate-best-practices-security-management/change.png)
  _Abbildung 19: Change Management_

**Weitere Informationen**:

- Erfahren Sie mehr über die [Änderungsnachverfolgung](/azure/automation/automation-change-tracking).
- Erfahren Sie mehr über [Azure Automation-Funktionen](/azure/automation/automation-intro).

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über weitere Best Practices:

- [Best Practices](./migrate-best-practices-networking.md) für Netzwerkfunktionen nach der Migration.
- [Best Practices](./migrate-best-practices-costs.md) für die Kostenverwaltung nach der Migration.
