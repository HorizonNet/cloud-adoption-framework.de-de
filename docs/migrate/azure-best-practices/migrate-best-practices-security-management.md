---
title: Sichern und Verwalten von zu Azure migrierten Workloads
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über Best Practices (bewährte Methoden) zum Abarbeiten, Verwalten und Sichern Ihrer migrierten Workloads zu informieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8233d262a8f6ea7f2ecd573cf33aff8d46f74f4b
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85077255"
---
<!-- cSpell:ignore FIPS SIEM majeure NSGs -->

# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Best Practices für die Sicherung und Verwaltung von zu Azure migrierten Workloads

Wenn Sie eine Migration zu Azure planen, sollten Sie nicht nur eine Strategie für die Migration selbst entwerfen, sondern müssen auch ein neues Sicherheits- und Verwaltungsmodell konzipieren, das nach der Migration angewendet werden soll. Dieser Artikel beschreibt die Planung sowie Best Practices für die Sicherung Ihrer Azure-Bereitstellung nach der Migration sowie für die fortlaufenden Aufgaben, mit denen Sie die Ausführung Ihrer Bereitstellung auf optimalem Niveau sicherstellen.

> [!IMPORTANT]
> Die in diesem Artikel beschriebenen Best Practices und Meinungen basieren auf Azure-Plattform- und -Dienstfeatures, die zu dem Zeitpunkt verfügbar waren, zu dem dieser Artikel verfasst wurde. Features und Funktionen ändern sich im Laufe der Zeit.

## <a name="secure-migrated-workloads"></a>Sichern von migrierten Workloads

Nach der Migration besteht die wichtigste Aufgabe darin, die migrierten Workloads vor internen und externen Bedrohungen zu schützen. Folgende Best Practices helfen Ihnen dabei:

- [Arbeiten mit dem Azure Security Center](#best-practice-follow-azure-security-center-recommendations): Erfahren Sie, wie Sie die Überwachungsfunktionen, Bewertungen und Empfehlungen von Azure Security Center verwenden.
- [Verschlüsseln Ihrer Daten](#best-practice-encrypt-data): Lernen Sie die Best Practices zum Verschlüsseln Ihrer Daten in Azure kennen.
- [Einrichten der Antischadsoftware](#best-practice-protect-vms-with-antimalware): Schützen Sie Ihre VMs vor Schadsoftware und Angriffen.
- [Sichern von Web-Apps](#best-practice-secure-web-apps): Sorgen Sie für die Sicherheit von Informationen in migrierten Web-Apps.
- [Überprüfen von Abonnements](#best-practice-review-subscriptions-and-resource-permissions): Überprüfen Sie, wer nach der Migration auf Ihre Azure-Abonnements und -Ressourcen zugreifen kann.
- [Arbeit mit Protokollen](#best-practice-review-audit-and-security-logs): Überprüfen Sie Ihre Azure-Überwachungs- und -Sicherheitsprotokolle in regelmäßigen Abständen.
- [Überprüfen anderer Sicherheitsfeatures](#best-practice-evaluate-other-security-features): Verstehen und bewerten Sie die erweiterten Sicherheitsfeatures, die Azure bietet.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Bewährte Methode: Befolgen der Azure Security Center-Empfehlungen

Microsoft unternimmt alle Anstrengungen, um sicherzustellen, dass Azure-Mandantenadministratoren über alle notwendigen Informationen verfügen, um die richtigen Sicherheitsfeatures einzurichten, mit denen Ihre Workloads vor Angriffen geschützt werden. Azure Security Center bietet eine einheitliche Sicherheitsverwaltung. In Security Center können Sie Sicherheitsrichtlinien für Ihre Workloads anwenden, die Angriffsfläche für Bedrohungen verringern sowie Angriffe erkennen und darauf reagieren. Security Center analysiert Ressourcen und Konfigurationen für mehrere Azure-Mandanten und gibt Sicherheitsempfehlungen aus, wie z.B. zu folgenden Themen:

- **Zentrale Richtlinienverwaltung:** Stellen Sie die Einhaltung unternehmensspezifischer oder gesetzlicher Sicherheitsvorschriften sicher, indem Sie Sicherheitsrichtlinien für alle Hybridcloud-Workloads zentral verwalten.
- **Laufende Sicherheitsbewertung:** Überwachen Sie den Sicherheitsstatus von Computern, Netzwerken, Speicher- und Datendiensten und Anwendungen, um potenzielle Sicherheitsprobleme aufzudecken.
- **Umsetzbare Empfehlungen:** Beseitigen Sie mit priorisierten, direkt umsetzbaren Sicherheitsempfehlungen Sicherheitslücken, bevor sie von Angreifern ausgenutzt werden können.
- **Priorisierte Warnungen und Vorfälle:** Konzentrieren Sie sich mittels priorisierter Warnungen und Vorfälle auf die größten Bedrohungen.

Zusätzlich zu Bewertungen und Empfehlungen stellt Azure Security Center weitere Sicherheitsfeatures bereit, die für bestimmte Ressourcen aktiviert werden können.

- **Just-in-Time-Zugriff (JIT):** Verringern Sie die Angriffsfläche in Ihrem Netzwerk mit kontrolliertem Just-in-Time-Zugriff auf Verwaltungsports auf Azure-VMs.
  - Wenn der RDP-Port 3389 auf einem virtuellen Computer geöffnet ist, ist dieser Computer dauerhaft potenziell schädlichen Aktivitäten ausgesetzt. Azure-IP-Adressen sind bekannt, und Hacker prüfen sie immer wieder auf offene 3389-Ports.
  - Beim JIT-Zugriff werden Netzwerksicherheitsgruppen und Regeln für eingehenden Datenverkehr verwendet, die den Zeitraum begrenzen, in dem ein bestimmter Port offen ist.
  - Wenn der JIT-Zugriff aktiviert ist, überprüft Security Center, ob einem Benutzer über die rollenbasierte Zugriffssteuerung Schreibzugriffsberechtigungen für einen virtuellen Computer zugewiesen wurden. Darüber hinaus können Sie Regeln dafür festlegen, wie Benutzer Verbindungen mit VMs herstellen. Wenn die Berechtigungen in Ordnung sind, wird eine Zugriffsanforderung genehmigt, und Security Center konfiguriert Netzwerksicherheitsgruppen automatisch so, dass für den von Ihnen angegebenen Zeitraum eingehender Datenverkehr an die ausgewählten Ports zugelassen wird. Netzwerksicherheitsgruppen werden nach Ablauf des Zeitraums in ihren vorherigen Zustand zurückversetzt.
- **Adaptive Anwendungssteuerungen:** Halten Sie Software und Schadsoftware von Ihren virtuellen Computern fern, indem Sie mit dynamischen Zulassungslisten steuern, welche Apps auf ihnen ausgeführt werden.
  - Mit adaptiven Anwendungssteuerungen können Sie Apps genehmigen und verhindern, dass Benutzer oder Administratoren, die nicht über die entsprechenden Berechtigungen verfügen, nicht genehmigte oder nicht überprüfte Apps auf Ihren VMs installieren.
    - Sie können Versuche zum Ausführen von schädlichen Apps blockieren oder davor warnen, unerwünschte oder schädliche Apps vermeiden und die Konformität mit der App-Sicherheitsrichtlinie Ihrer Organisation sicherstellen.
- **Überwachen der Dateiintegrität:** Stellen Sie die Integrität von Dateien sicher, die auf VMs ausgeführt werden.
  - Probleme auf VMs treten nicht nur nach der Installation von Software auf. Die Änderung einer Systemdatei kann auch zum Ausfall oder zur Leistungsbeeinträchtigung eines virtuellen Computers führen. Die Überwachung der Dateiintegrität untersucht Systemdateien und Registrierungseinstellungen auf Änderungen und benachrichtigt Sie, wenn ein Element aktualisiert wurde.
  - Security Center empfiehlt die Dateien, die Sie überwachen sollten.

**Weitere Informationen**:

- Weitere Informationen zu [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro)
- Erfahren Sie mehr über den [Just-In-Time-Zugriff auf VMs](https://docs.microsoft.com/azure/security-center/security-center-just-in-time).
- Erfahren Sie mehr über das [Anwenden von adaptiven Anwendungssteuerungen](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application).
- [Beginnen Sie](https://docs.microsoft.com/azure/security-center/security-center-file-integrity-monitoring) mit der Überwachung der Dateiintegrität.

## <a name="best-practice-encrypt-data"></a>Bewährte Methode: Verschlüsseln von Daten

Die Verschlüsselung ist ein wichtiger Bestandteil der Azure-Sicherheitsmaßnahmen. Indem Sie sicherstellen, dass die Verschlüsselung auf allen Ebenen aktiviert ist, können Sie verhindern, dass nicht autorisierte Parteien Zugriff auf vertrauliche Daten erhalten. Dies gilt für Daten während der Übertragung und für ruhende Daten.

### <a name="encryption-for-iaas"></a>Verschlüsselung für IaaS

- **Virtuelle Computer:** Zum Verschlüsseln von IaaS-VM-Datenträgern unter Windows und Linux können Sie Azure Disk Encryption verwenden.
  - Disk Encryption verwendet BitLocker für Windows und DM-Crypt für Linux, um Volumeverschlüsselung für die Datenträger für das Betriebssystem und die Daten bereitzustellen.
  - Sie können einen von Azure erstellten Verschlüsselungsschlüssel verwenden oder eigene Verschlüsselungsschlüssel bereitstellen, die in Azure Key Vault geschützt sind.
  - Mit Disk Encryption werden IaaS-VM-Daten im Ruhezustand (auf dem Datenträger) und während des VM-Starts gesichert.
    - Azure Security Center warnt Sie, wenn VMs nicht verschlüsselt sind.
- **Speicher:** Schützen Sie ruhende Daten im Azure-Speicher.
  - Daten in Azure-Speicherkonten können mithilfe von AES-Schlüsseln verschlüsselt werden, die von Microsoft generiert werden und mit FIPS 140-2 konform sind. Alternativ dazu können Sie auch eigene Schlüssel verwenden.
  - Die Speicherdienstverschlüsselung ist für alle neuen und vorhandenen Speicherkonten aktiviert und kann nicht deaktiviert werden.

### <a name="encryption-for-paas"></a>Verschlüsselung für PaaS

Im Gegensatz zum IaaS-Konzept, bei dem Sie VMs und Infrastruktur selbst verwalten, werden in einem PaaS-Modell Plattform und Infrastruktur vom Anbieter verwaltet, sodass Sie sich ganz auf App-Logik und -Funktionen konzentrieren können. Es gibt sehr viele verschiedene Arten von PaaS-Diensten, daher wird jeder Dienst einzeln hinsichtlich der Sicherheit bewertet. Sehen wir uns jetzt als Beispiel an, wie sich die Verschlüsselung für Azure SQL-Datenbank aktivieren lässt.

- **Always Encrypted:** Verwenden Sie den Always Encrypted-Assistenten in SQL Server Management Studio, um ruhende Daten zu schützen.
  - Sie erstellen einen Always Encrypted-Schlüssel, um einzelne Spaltendaten zu verschlüsseln.
  - Always Encrypted-Schlüssel können verschlüsselt in den Datenbankmetadaten oder in vertrauenswürdigen Speichern wie Azure Key Vault gespeichert werden.
  - Für die Verwendung dieses Features sind möglicherweise Änderungen an Apps erforderlich.
- **Transparent Data Encryption (TDE):** Schützen Sie die Azure SQL-Datenbank mit Echtzeitverschlüsselung und -entschlüsselung der Datenbank, der zugehörigen Sicherungen und der ruhenden Transaktionsprotokolldateien.
  - TDE ermöglicht die Ausführung von Verschlüsselungsaktivitäten ohne Änderungen auf der App-Ebene.
  - TDE kann von Microsoft bereitgestellte Verschlüsselungsschlüssel oder Ihren eigenen Schlüssel (Bring Your Own Key, BYOK) verwenden.

**Weitere Informationen**:

- Weitere Informationen zu [Azure Disk Encryption für virtuelle Computer und VM-Skalierungsgruppen](https://docs.microsoft.com/azure/security/fundamentals/azure-disk-encryption-vms-vmss).
- Aktivieren von [Azure Disk Encryption für virtuelle Windows-Computer](https://docs.microsoft.com/azure/virtual-machines/windows/disk-encryption-overview).
- Erfahren Sie mehr über die [Azure-Speicherdienstverschlüsselung für ruhende Daten](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).
- Lesen Sie die [Übersicht über Always Encrypted](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault).
- Lesen Sie über die [Transparente Datenverschlüsselung für SQL-Datenbank und Azure Synapse](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql).
- Erfahren Sie mehr zu [Azure SQL Transparent Data Encryption mithilfe eines kundenseitig verwalteten Schlüssels](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql).

## <a name="best-practice-protect-vms-with-antimalware"></a>Bewährte Methode: Schützen von VMs mit Antischadsoftware

Insbesondere ältere zu Azure migrierte VMs verfügen möglicherweise nicht über die richtige installierte Antischadsoftware. Azure bietet eine kostenlose Endpunktlösung, mit der Sie VMs vor Viren, Spyware und anderer Schadsoftware schützen können.

- Microsoft-Antischadsoftware für Azure generiert Warnungen, wenn bekannte schädliche oder unerwünschte Software versucht, sich selbst zu installieren.
- Es handelt sich um eine Lösung mit einem Agent, die ohne Benutzereingriff im Hintergrund ausgeführt wird.
- In Azure Security Center können Sie ganz einfach diejenigen VMs identifizieren, auf denen kein Endpunktschutz ausgeführt wird, und bei Bedarf Microsoft-Antischadsoftware installieren.

  ![Antischadsoftware für VMs](./media/migrate-best-practices-security-management/antimalware.png)
  _Antischadsoftware für VMs_

**Weitere Informationen**:

- Erfahren Sie mehr zu [Microsoft Antimalware für Azure Cloud Services und Virtual Machines](https://docs.microsoft.com/azure/security/fundamentals/antimalware).

## <a name="best-practice-secure-web-apps"></a>Bewährte Methode: Sichern von Web-Apps

Bei migrierten Web-Apps können einige Probleme auftreten:

- In vielen älteren Webanwendungen befinden sich vertrauliche Informationen in Konfigurationsdateien. Dateien, die solche Informationen enthalten, können zu Sicherheitsproblemen führen, wenn Apps gesichert werden oder wenn App-Code in die Quellcodeverwaltung eingecheckt oder daraus ausgecheckt wird.
- Dazu kommt Folgendes: Wenn Sie Web-Apps migrieren, die sich auf einem virtuellen Computer befinden, verlagern Sie wahrscheinlich diesen Computer aus einer Umgebung mit lokalem Netzwerk und Firewallschutz in eine Umgebung mit Internetzugriff. Stellen Sie sicher, dass Sie eine Lösung einrichten, die dieselben Aufgaben erfüllt wie Ihre lokalen Schutzressourcen.

Azure stellt verschiedene Lösungen bereit:

- **Azure Key Vault:** Heute unternehmen Web-App-Entwickler Schritte, um sicherzustellen, dass vertrauliche Informationen nicht aus diesen Dateien ausgelesen werden können. Eine Methode zum Sichern von Informationen besteht darin, diese aus den Dateien zu extrahieren und in einem Azure Key Vault zu speichern.
  - Sie können Key Vault verwenden, um App-Geheimnisse zentral zu speichern und ihre Verteilung zu steuern. So müssen Sicherheitsinformationen nicht mehr in App-Dateien gespeichert werden.
  - Apps können über URIs sicher auf Informationen im Tresor zugreifen, ohne dafür benutzerdefinierten Code zu benötigen.
  - Mit Azure Key Vault können Sie den Zugriff über Azure-Sicherheitssteuerungen sperren und nahtlos ein Schlüsselrollover implementieren. Microsoft kann Ihre Daten weder einsehen noch extrahieren.
- **App Service-Umgebung:** Wenn eine App, die Sie migrieren möchten, zusätzlichen Schutz benötigt, können Sie eine App Service-Umgebung und Web Application Firewall hinzufügen, um die App-Ressourcen zu schützen.
  - Die Azure App Service-Umgebung stellt eine vollständig isolierte und dedizierte Umgebung bereit, in der App Service-Apps wie Windows- und Linux-Web-Apps, Docker-Container, mobile Apps und Funktionen ausgeführt werden können.
  - Dies ist nützlich für Apps auf sehr hoher Ebene, die Isolierung und sicheren Netzwerkzugriff erfordern oder viel Arbeitsspeicher benötigen.
- **Web Application Firewall:** Dieses Feature von Azure Application Gateway sorgt für zentralisierten Schutz von Web-Apps.
  - Es schützt Web-Apps, ohne das dafür Änderungen am Back-End-Code erforderlich sind.
  - Es schützt mehrere Web-Apps gleichzeitig hinter einem Anwendungsgateway.
  - Web Application Firewall kann mithilfe von Azure Monitor überwacht werden und ist in Azure Security Center integriert.

  ![Sichere Web-Apps](./media/migrate-best-practices-security-management/web-apps.png)
  _Azure Key Vault_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/overview).
- Erfahren Sie mehr über [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/waf-overview).
- Lesen Sie eine [Einführung in App Service-Umgebungen](https://docs.microsoft.com/azure/app-service/environment/intro).
- Erfahren Sie, wie Sie [eine Web-App so konfigurieren, dass sie Geheimnisse aus Key Vault lesen kann](https://docs.microsoft.com/azure/key-vault/tutorial-web-application-keyvault).
- Erfahren Sie mehr über [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/waf-overview).

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Bewährte Methode: Überprüfen von Abonnements und Ressourcenberechtigungen

Wenn Sie Ihre Workloads migrieren und in Azure ausführen, können Mitarbeiter mit Workloadzugriff standortunabhängig arbeiten. Ihr Sicherheitsteam sollte den Zugriff auf Ihre Azure-Mandanten und -Ressourcengruppen in regelmäßigen Abständen überprüfen. Azure bietet Lösungen für die Identitätsverwaltung und die Sicherheit der Zugriffssteuerung (z. B. die rollenbasierte Zugriffssteuerung), um Berechtigungen für den Zugriff auf Azure-Ressourcen zu autorisieren.

- Die rollenbasierte Zugriffssteuerung weist Zugriffsberechtigungen für Sicherheitsprinzipale zu. Sicherheitsprinzipale repräsentieren Benutzer, Gruppen (aus Benutzern), Dienstprinzipale (von Apps und Diensten verwendete Identitäten) und verwaltete Identitäten (automatisch von Azure verwaltete Azure Active Directory-Identitäten).
- Die rollenbasierte Zugriffssteuerung kann Sicherheitsprinzipalen Rollen wie Besitzer, Mitwirkender und Leser zuweisen. Das Feature kann auch Rollendefinitionen (eine Sammlung aus Berechtigungen) zuweisen, die die Vorgänge definieren, die von den Rollen ausgeführt werden können.
- Die rollenbasierte Zugriffssteuerung kann auch Bereiche festlegen, die die Grenze für eine Rolle definieren. Ein Bereich kann auf verschiedenen Ebenen festgelegt werden, z. B. für Verwaltungsgruppen, Abonnements, Ressourcengruppen oder Ressourcen.
- Stellen Sie sicher, dass Administratoren mit Azure-Zugriff nur auf diejenigen Ressourcen zugreifen können, die Sie zulassen möchten. Wenn die vordefinierten Rollen in Azure nicht differenziert genug sind, können Sie benutzerdefinierte Rollen erstellen, um Zugriffsberechtigungen zu trennen und zu begrenzen.

  ![Zugriffssteuerung](./media/migrate-best-practices-security-management/subscription.png)
  _Zugriffssteuerung – IAM_

**Weitere Informationen**:

- [Erfahren Sie mehr](https://docs.microsoft.com/azure/role-based-access-control/overview) über die rollenbasierte Zugriffssteuerung.
- [Erfahren Sie](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal), wie Sie den Zugriff über die rollenbasierte Zugriffssteuerung und das Azure-Portal verwalten.
- Erfahren Sie mehr über [benutzerdefinierte Rollen](https://docs.microsoft.com/azure/role-based-access-control/custom-roles).

## <a name="best-practice-review-audit-and-security-logs"></a>Bewährte Methode: Überprüfen von Überwachungs- und Sicherheitsprotokollen

Azure Active Directory (Azure AD) stellt Aktivitätsprotokolle bereit, die in Azure Monitor angezeigt werden. Die Protokolle erfassen die Vorgänge, die in Azure-Mandanten ausgeführt werden, und sie erfassen auch, wann und von wem sie ausgeführt werden.

- Überwachungsprotokolle zeigen den Verlauf von Aufgaben im Mandanten an. Protokolle für Anmeldeaktivitäten zeigen, wer die Aufgaben ausgeführt hat.
- Der Zugriff auf Sicherheitsberichte richtet sich nach Ihrer Azure AD-Lizenz. In den Tarifen „Free“ und „Basic“ erhalten Sie eine Liste der Benutzer und Anmeldungen, für die ein Risiko vorliegt. In den Editionen „Premium 1“ und „Premium 2“ erhalten Sie zugrunde liegende Ereignisinformationen.
- Sie können Aktivitätsprotokolle zur Langzeitaufbewahrung und für Datenerkenntnisse an mehrere Endpunkte weiterleiten.
- Gewöhnen Sie sich an, die Protokolle zu überprüfen, oder integrieren Sie Ihre SIEM-Tools (Security Information & Event Management), um Anomalien automatisch zu überprüfen. Wenn Sie nicht Premium 1 oder 2 verwenden, müssen Sie viele Analyseaktivitäten selbst oder mithilfe Ihres SIEM-Systems ausführen. Zu diesen Aktivitäten gehört die Suche nach risikobehafteten Anmeldungen und Ereignissen sowie weiteren Benutzerangriffsmustern.

  ![Benutzer und Gruppen](./media/migrate-best-practices-security-management/azure-ad.png)
  _Azure AD-Benutzer und -Gruppen_

**Weitere Informationen**:

- Erfahren Sie mehr über [Azure AD-Aktivitätsprotokolle in Azure Monitor](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor).
- Erfahren Sie, wie Sie [Aktivitätsberichte im Azure AD-Portal überwachen](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs).

## <a name="best-practice-evaluate-other-security-features"></a>Bewährte Methode: Bewerten anderer Sicherheitsfeatures

Azure bietet weitere Sicherheitsfunktionen, die erweiterte Sicherheitsoptionen bereitstellen. Einige dieser Best Practices erfordern Add-On-Lizenzen und Premium-Optionen.

- **Implementieren von Azure AD-Verwaltungseinheiten:** Das Delegieren von Verwaltungsaufgaben zur Unterstützung der Mitarbeiter nur mit grundlegender Azure-Zugriffssteuerung kann schwierig sein. Supportmitarbeitern Zugriff auf die Verwaltung all dieser Gruppen in Azure AD zu gewähren ist hinsichtlich der Sicherheit der Organisation möglicherweise nicht der ideale Ansatz. Mit Verwaltungseinheiten (Administrative Units, AUs) können Sie Azure-Ressourcen in Container unterteilen, ähnlich wie bei lokalen Organisationseinheiten (Organizational Units, OUs). Um Verwaltungseinheiten zu verwenden, muss der AU-Administrator über eine Azure AD-Premium-Lizenz verfügen. [Weitere Informationen](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-administrative-units)
- **Verwenden der mehrstufigen Authentifizierung:** Wenn Sie über eine Azure AD-Premium-Lizenz verfügen, können Sie die mehrstufige Authentifizierung in Ihren Administratorkonten aktivieren und erzwingen. Anmeldeinformationen für Konten sind am meisten durch Phishing gefährdet. Sobald böswillige Benutzer über Anmeldeinformationen für ein Administratorkonto verfügen, gibt es keine Möglichkeit, sie an der Ausführung von folgenschweren Aktionen zu hindern, z. B. am Löschen aller Ihrer Ressourcengruppen. Sie können die mehrstufige Authentifizierung auf verschiedenen Wegen umsetzen, z. B. per E-Mail, mit einer Authentifikator-App und über Textnachrichten. Als Administrator können Sie die Option auswählen, die sich am einfachsten umsetzen lässt. Die mehrstufige Authentifizierung lässt sich in Richtlinien für die Bedrohungsanalyse und den bedingten Zugriff integrieren, um per Zufallsprinzip eine Antwort auf eine Anforderung für die mehrstufige Authentifizierung anzufordern. Erfahren Sie mehr über [Sicherheitsempfehlungen](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) und das [Einrichten der mehrstufigen Authentifizierung](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementieren des bedingten Zugriffs:** In den meisten kleinen und mittelgroßen Organisationen befinden sich Azure-Administratoren und das Supportteam möglicherweise innerhalb derselben geografischen Region. In diesem Fall stammen die meisten Anmeldungen von den gleichen Standorten. Wenn die IP-Adressen dieser Standorte einigermaßen statisch sind, sollten keine Administratoranmeldungen aus Bereichen außerhalb dieser Standorte festzustellen sein. Selbst wenn ein böswilliger Akteur von außerhalb in den Besitz der Anmeldeinformationen eines Administrators gelangt, können Sie Sicherheitsfeatures implementieren (z. B. den bedingten Zugriff in Kombination mit der mehrstufigen Authentifizierung), um Anmeldungen von Remotestandorten oder gefälschten Standorten über zufällige IP-Adressen zu verhindern. [Erfahren Sie mehr](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) über den bedingten Zugriff, und [lesen Sie Best Practices](https://docs.microsoft.com/azure/active-directory/conditional-access/best-practices) für den bedingten Zugriff in Azure AD.
- **Überprüfen von Berechtigungen von Enterprise-Anwendungen:** Im Lauf der Zeit wählen Administratoren Links von Microsoft und anderen Anbietern aus, ohne sich über die Auswirkungen auf ihre Organisation im Klaren zu sein. Links können Zustimmungsbildschirme anzeigen, die Berechtigungen für Azure-Apps zuweisen. Über solche Links kann auch Lesezugriff auf Azure AD-Daten oder sogar Vollzugriff zur Verwaltung Ihres gesamten Azure-Abonnements gewährt werden. Sie sollten die Apps regelmäßig überprüfen, für die Ihre Administratoren und Benutzer Zugriff auf Azure-Ressourcen gewährt haben. Stellen Sie sicher, dass diese Apps nur über die Berechtigungen verfügen, die erforderlich sind. Darüber hinaus können Sie Benutzern viertel- oder halbjährlich eine E-Mail mit einem Link zu App-Seiten senden, um den Benutzern die Apps ins Bewusstsein zu rufen, denen sie Zugriff auf ihre Organisationsdaten gewährt haben. [Erfahren Sie mehr](https://docs.microsoft.com/azure/active-directory/manage-apps/application-types) über Anwendungstypen und darüber, wie Sie App-Zuweisungen in Azure AD [steuern](https://docs.microsoft.com/azure/active-directory/manage-apps/remove-user-or-group-access-portal).

## <a name="managed-migrated-workloads"></a>Verwalten von migrierten Workloads

In diesem Abschnitt empfehlen wir einige Best Practices für die Azure-Verwaltung:

- [Verwalten von Ressourcen](#best-practice-name-resource-groups): Best Practices für Azure-Ressourcengruppen und -Ressourcen, einschließlich intelligenter Benennung, Verhindern von versehentlichem Löschen, Verwalten von Ressourcenberechtigungen und effektivem Markieren von Ressourcen.
- [Verwenden von Blaupausen](#best-practice-implement-blueprints): Erhalten Sie einen schnellen Überblick über die Verwendung von Blaupausen zum Erstellen und Verwalten Ihrer Bereitstellungsumgebungen.
- [Überprüfen von Architekturen](#best-practice-review-azure-reference-architectures): Sehen Sie sich Azure-Beispielarchitekturen an, während Sie Ihre Bereitstellungen nach der Migration erstellen.
- [Einrichten von Verwaltungsgruppen](#best-practice-manage-resources-with-azure-management-groups): Wenn Sie über mehrere Abonnements verfügen, können Sie diese in Verwaltungsgruppen zusammenfassen und Governanceeinstellungen auf diese Gruppen anwenden.
- [Einrichten von Zugriffsrichtlinien](#best-practice-deploy-azure-policy): Wenden Sie Konformitätsrichtlinien auf Ihre Azure-Ressourcen an.
- [Implementieren einer BCDR-Strategie](#best-practice-implement-a-bcdr-strategy): Erstellen Sie eine Strategie für Business Continuity & Disaster Recovery (BCDR), um bei Ausfällen Ihre Daten zu sichern, Ihre Umgebung stabil zu halten und für die fortlaufende Ausführung Ihrer Ressourcen zu sorgen.
- [Verwalten von VMs](#best-practice-use-managed-disks-and-availability-sets): Stellen Sie virtuelle Computer in Verfügbarkeitsgruppen zusammen, um für Stabilität und Hochverfügbarkeit zu sorgen. Verwenden Sie verwaltete Datenträger, um die Verwaltung von VM-Datenträgern und Speicher zu vereinfachen.
- [Überwachen der Ressourcennutzung](#best-practice-monitor-resource-usage-and-performance): Ermöglichen Sie die Diagnoseprotokollierung für Azure-Ressourcen, erstellen Sie Warnungen und Playbooks für die proaktive Problembehandlung, und verwenden Sie das Azure-Dashboard, um eine einheitliche Ansicht der Integrität und des Status Ihrer Bereitstellung zu erhalten.
- [Verwalten von Support und Updates](#best-practice-manage-updates): Erfahren Sie mehr über Ihren Azure-Supportplan und wie Sie ihn implementieren, profitieren Sie von Best Practices zur Aktualisierung Ihrer virtuellen Computer, und richten Sie Prozesse für das Change Management ein.

## <a name="best-practice-name-resource-groups"></a>Bewährte Methode: Benennen von Ressourcengruppen

Mit aussagekräftigen Namen für Ihre Ressourcengruppen, die Administratoren und Mitglieder des Supportteams einfach erkennen und auffinden können, verbessern Sie die Produktivität und Effizienz erheblich.

- Wir empfehlen, die Namenskonventionen für Azure zu befolgen.
- Wenn Sie Ihr lokales Active Directory über Azure AD Connect mit Azure AD synchronisieren, sollten Sie die Namen der lokalen Sicherheitsgruppen an die Namen der Ressourcengruppen in Azure anpassen.

  ![Benennen](./media/migrate-best-practices-security-management/naming.png)
  _Benennen von Ressourcengruppen_

**Weitere Informationen**:

- Erfahren Sie mehr über [Empfohlene Benennungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md).

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Bewährte Methode: Implementieren von Sperren für Ressourcengruppen

Niemand möchte, dass eine Ressourcengruppe verschwindet, weil sie versehentlich gelöscht wurde. Wir empfehlen die Implementierung von Löschsperren, um dies zu verhindern.

  ![Löschsperren](./media/migrate-best-practices-security-management/locks.png) _Löschsperren_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Sperren von Ressourcen, um unerwartete Änderungen zu verhindern](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources).

## <a name="best-practice-understand-resource-access-permissions"></a>Bewährte Methode: Verstehen der Berechtigungen für den Ressourcenzugriff

Ein Abonnementbesitzer hat Zugriff auf alle Ressourcengruppen und Ressourcen in Ihrem Abonnement.

- Fügen Sie dieser wertvollen Zuweisung nur wenige Benutzer hinzu. Sie müssen die Auswirkungen dieser Art von Berechtigungen genau kennen, um für die Sicherheit und Stabilität Ihrer Umgebung zu sorgen.
- Stellen Sie sicher, dass Sie Ressourcen in geeigneten Ressourcengruppe platzieren:
  - Fassen Sie Ressourcen mit ähnlichem Lebenszyklus zusammen. Im Idealfall sollte es nicht notwendig sein, eine Ressource zu verschieben, wenn Sie eine vollständige Ressourcengruppe löschen müssen.
  - Ressourcen, die eine Funktion oder Workload unterstützen, sollten zur Vereinfachung der Verwaltung gruppiert werden.

**Weitere Informationen**:

- Erfahren Sie mehr über das [Organisieren von Abonnements und Ressourcengruppen](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).

## <a name="best-practice-tag-resources-effectively"></a>Bewährte Methode: Effektives Markieren von Ressourcen

Häufig bietet die Verwendung nur eines Ressourcengruppenamens für Ressourcen nicht genügend Metadaten für die effektive Implementierung von Mechanismen wie die interne Abrechnung oder die Verwaltung innerhalb eines Abonnements.

- Als Best Practice sollten Sie Azure-Tags verwenden, um hilfreiche Metadaten hinzuzufügen, die abgefragt und gemeldet werden können.
- Tags sind eine Möglichkeit, Ressourcen mit von Ihnen definierten Eigenschaften logisch zu organisieren. Tags können auf Ressourcengruppen oder direkt auf Ressourcen angewendet werden.
- Tags können auf eine Ressourcengruppe oder auf einzelne Ressourcen angewendet werden. Ressourcengruppentags werden nicht an die Ressourcen in der Gruppe vererbt.
- Sie können die Markierung mithilfe von PowerShell oder Azure Automation automatisieren oder einzelne Gruppen oder Ressourcen markieren. Verwenden Sie einen automatisierten Markierungsansatz oder ein Verfahren per Self-Service. Wenn Sie ein System für Anforderungsmanagement und Change Management eingerichtet haben, können Sie ganz einfach die Informationen in der Anforderung verwenden, um Ihre unternehmensspezifischen Ressourcentags aufzufüllen.

  ![Markieren](./media/migrate-best-practices-security-management/tagging.png)
  _Markieren_

**Weitere Informationen**:

- Erfahren Sie mehr über [Markierungen und Tageinschränkungen](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).
- Sehen Sie sich [PowerShell- und CLI-Beispiele für das Einrichten von Tags und das Anwenden von Tags von einer Ressourcengruppe auf die zugehörigen Ressourcen](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources#powershell) an.
- [Lesen](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) Sie Best Practices zum Markieren in Azure.

## <a name="best-practice-implement-blueprints"></a>Bewährte Methode: Implementieren von Blaupausen

Genau wie eine Blaupause, mit der Ingenieure oder Architekten die Entwurfsparameter für ein Projekt skizzieren, ermöglicht es der Azure Blueprints-Dienst Cloudarchitekten und zentralen IT-Teams, eine wiederholbare Gruppe von Azure-Ressourcen zu definieren, mit der die Standards, Muster und Anforderungen einer Organisation implementiert und durchgesetzt werden. Mit Azure Blueprints können Entwicklungsteams schnell neue Umgebungen erstellen und bereitstellen, die die Konformitätsanforderungen der Organisation erfüllen und über eine Reihe integrierter Komponenten (z. B. Netzwerk) zur Beschleunigung der Entwicklung und Bereitstellung verfügen.

- Verwenden Sie Blaupausen, um die Bereitstellung von Ressourcengruppen, Azure Resource Manager-Vorlagen sowie Richtlinien- und Rollenzuweisungen zu orchestrieren.
- Blaupausen werden in einer global verteilten Azure Cosmos DB-Instanz gespeichert. Blaupausenobjekte werden in mehreren Azure-Regionen repliziert. Die Replikation bietet geringe Latenzen, Hochverfügbarkeit und konsistenten Zugriff auf Blaupausen – unabhängig davon, in welcher Region eine Blaupause Ihre Ressourcen bereitstellt.

**Weitere Informationen**:

- [Erfahren Sie mehr](https://docs.microsoft.com/azure/governance/blueprints/overview) über Blaupausen.
- Sehen Sie sich ein [Beispiel für eine Blaupause zum Beschleunigen von KI im Gesundheitswesen](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) an.

## <a name="best-practice-review-azure-reference-architectures"></a>Bewährte Methode: Überprüfen von Referenzarchitekturen

Das Erstellen sicherer, skalierbarer und verwaltbarer Workloads in Azure kann eine große Herausforderung sein. Angesichts fortlaufender Änderungen kann es schwierig sein, bei verschiedenen Features auf dem Laufenden zu bleiben, um eine optimale Umgebung sicherzustellen. Beim Entwerfen und Migrieren Ihrer Workloads kann es nützlich sein, über eine Referenz zu verfügen, aus der Sie nützliche Informationen erhalten können. Azure und die Azure-Partner haben verschiedene Referenzarchitekturen als Muster für verschiedene Arten von Umgebungen erstellt. Diese Muster bieten Anregungen, aus denen Sie lernen und auf denen Sie aufbauen können.

Die Referenzarchitekturen sind nach Szenario sortiert. Sie enthalten Best Practices und Ratschläge zu Verwaltung, Verfügbarkeit, Skalierbarkeit und Sicherheit.
Die Azure App Service-Umgebung stellt eine vollständig isolierte und dedizierte Umgebung bereit, in der App Service-Apps wie Windows- und Linux-Web-Apps, Docker-Container, mobile Apps und Funktionen ausgeführt werden können. App Service ergänzt Ihre Anwendung um leistungsfähige Azure-Features, z.B. Sicherheit, Lastenausgleich, automatische Skalierung und automatisierte Verwaltung. Sie können auch die Vorteile der DevOps-Funktionen des Diensts nutzen, z.B. Continuous Deployment über Azure DevOps und GitHub, Paketverwaltung, Stagingumgebungen, benutzerdefinierte Domäne und SSL-Zertifikate. App Service ist hilfreich bei Apps, die Isolierung und sicheren Netzwerkzugriff erfordern, sowie für solche Apps, die eine große Menge an Arbeitsspeicher sowie weitere skalierbare Ressourcen nutzen.

**Weitere Informationen**:

- Erfahren Sie mehr über [Azure-Referenzarchitekturen](https://docs.microsoft.com/azure/architecture/reference-architectures).
- Sehen Sie sich [Azure-Beispielszenarien](https://docs.microsoft.com/azure/architecture/example-scenario) an.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Bewährte Methode: Verwalten von Ressourcen mit Azure-Verwaltungsgruppen

Wenn Ihre Organisation über mehrere Abonnements verfügt, müssen Sie Zugriff, Richtlinien und Konformität für diese Abonnements verwalten. Azure-Verwaltungsgruppen stellen einen abonnementübergreifenden Bereich dar.

- Sie organisieren Abonnements in Containern, die als Verwaltungsgruppen bezeichnet werden, und wenden Governancebedingungen darauf an.
- Alle Abonnements in einer Verwaltungsgruppe erben automatisch die Bedingungen der Verwaltungsgruppe.
- Verwaltungsgruppen ermöglichen Ihnen unabhängig von der Art Ihrer Abonnements die Verwaltung auf Unternehmensniveau in großem Umfang.
- Sie können z.B. die Richtlinie einer Verwaltungsgruppe anwenden, die die Regionen einschränkt, in denen VMs erstellt werden können. Diese Richtlinie wird auf alle Verwaltungsgruppen, Abonnements und Ressourcen in dieser Verwaltungsgruppe angewandt.
- Sie können eine flexible Struktur aus Verwaltungsgruppen und Abonnements aufbauen, um Ihre Ressourcen für eine einheitliche Richtlinien- und Zugriffsverwaltung in einer Hierarchie zu organisieren.

Das folgende Diagramm zeigt ein Beispiel zum Erstellen einer Hierarchie für die Governance unter Verwendung von Verwaltungsgruppen.

  ![Verwaltungsgruppen](./media/migrate-best-practices-security-management/management-groups.png) _Verwaltungsgruppen_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Organisieren von Ressourcen in Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="best-practice-deploy-azure-policy"></a>Bewährte Methode: Bereitstellen von Azure Policy

Azure Policy ist ein Dienst in Azure, mit dem Sie Richtlinien erstellen, zuweisen und verwalten können.

- Richtlinien erzwingen verschiedene Regeln und Effekte für Ihre Ressourcen, damit diese stets mit Ihren Unternehmensstandards und Vereinbarungen zum Servicelevel konform bleiben.
- Azure Policy bewertet Ihre Ressourcen und sucht nach Ressourcen, die nicht mit Ihren Richtlinien konform sind.
- Sie können beispielsweise eine Richtlinie erstellen, die nur eine bestimmte SKU-Größe für VMs in Ihrer Umgebung zulässt. Azure Policy wertet diese Einstellung beim Erstellen und Aktualisieren von Ressourcen sowie beim Überprüfen vorhandener Ressourcen aus.
- Azure stellt integrierte Richtlinien bereit, die Sie zuweisen können – oder erstellen Sie eigene Richtlinien.

  ![Azure Policy](./media/migrate-best-practices-security-management/policy.png)
  _Azure Policy_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview).
- Erfahren Sie mehr über das [Erstellen und Verwalten von Richtlinien zum Durchsetzen der Konformität](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage).

## <a name="best-practice-implement-a-bcdr-strategy"></a>Bewährte Methode: Implementieren einer BCDR-Strategie

Die Planung von Business Continuity & Disaster Recovery (BCDR) ist eine wichtige Aufgabe, die Sie bei der Planung der Migration zu Azure durchführen sollten. Rechtlich gesehen enthalten Ihre Verträge möglicherweise eine Klausel zu höherer Gewalt, die Sie bei unabwendbaren Ereignissen wie Wirbelstürmen oder Erdbeben von Verpflichtungen entbindet. Sie haben jedoch auch Verpflichtungen in der Hinsicht, dass Sie die Ausführung und bei Bedarf die Wiederherstellung von Diensten in einem Notfall sicherstellen müssen. Die Fähigkeit, diese Verpflichtungen zu erfüllen, kann über die Zukunft Ihres Unternehmens entscheiden.

Allgemein gesagt muss Ihre BCDR-Strategie Folgendes berücksichtigen:

- **Datensicherung:** Schützen Sie Ihre Daten, sodass Sie diese nach einem Ausfall einfach wiederherstellen können.
- **Notfallwiederherstellung:** Sorgen Sie für Stabilität und Verfügbarkeit Ihrer Apps nach einem Ausfall.

### <a name="set-up-bcdr"></a>Einrichten von BCDR

Bei der Migration zu Azure muss Folgendes unbedingt beachtet werden: Obwohl die Azure-Plattform diese integrierten Resilienzfeatures bietet, müssen Sie Ihre Azure-Bereitstellung so entwerfen, dass sie von den Azure-Features und -Diensten für Hochverfügbarkeit, Notfallwiederherstellung und Sicherung profitiert.

- Ihre BCDR-Lösung richtet sich nach den Zielen Ihres Unternehmens und wird durch Ihre Azure-Bereitstellungsstrategie beeinflusst. IaaS-Bereitstellungen (Infrastructure-as-a-Service) und PaaS-Bereitstellungen (Platform as a Service) stellen unterschiedliche Herausforderungen an Ihre Business Continuity & Disaster Recovery-Lösung.
- Sobald Ihre BCDR-Lösung eingerichtet ist, sollte sie regelmäßig überprüft werden, um sicherzustellen, dass Ihre Strategie weiterhin sinnvoll ist.

### <a name="back-up-an-iaas-deployment"></a>Sichern einer IaaS-Bereitstellung

In den meisten Fällen wird eine lokale Workload nach der Migration außer Betrieb genommen, und Ihre lokale Strategie für die Sicherung von Daten muss erweitert oder ersetzt werden. Wenn Sie Ihr gesamtes Rechenzentrum nach Azure migrieren, müssen Sie mithilfe von Azure-Technologien oder integrierten Drittanbieterlösungen eine vollständige Sicherungslösung entwerfen und implementieren.

Ziehen Sie für Workloads, die auf Azure-IaaS-VMs ausgeführt werden, folgende Sicherungslösungen in Betracht:

- **Azure Backup:** Azure Backup bietet anwendungskonsistente Sicherungen für Azure-Windows- und -Linux-VMs.
- **Speichermomentaufnahmen:** Dieses Feature erstellt Momentaufnahmen vom Blobspeicher.

#### <a name="azure-backup"></a>Azure Backup

Azure Backup erstellt Datenwiederherstellungspunkte, die in Azure Storage gespeichert werden. Azure Backup kann Azure-VM-Datenträger und Azure File Storage (Vorschau) sichern. Azure File Storage stellt Dateifreigaben in der Cloud bereit, auf die über SMB zugegriffen werden kann.

Sie können Azure Backup verwenden, um VMs auf unterschiedliche Weise zu sichern.

- **Direkte Sicherung aus VM-Einstellungen:** Sie können VMs mit Azure Backup direkt über die VM-Optionen im Azure-Portal sichern. Sie können eine VM einmal täglich sichern und den VM-Datenträger bei Bedarf wiederherstellen. Azure Backup erstellt App-bezogene Datenmomentaufnahmen (VSS). Auf der VM wird kein Agent installiert.
- **Direkte Sicherung in einem Recovery Services-Tresor:** Sie können Ihre IaaS-VMs durch Bereitstellen eines Azure Backup-Recovery Services-Tresors sichern. Dies bietet einen einzelnen Speicherort zum Nachverfolgen und Verwalten von Sicherungen und ermöglicht differenzierte Sicherungs- und Wiederherstellungsoptionen. Die Sicherung erfolgt bis zu dreimal am Tag auf Datei- oder Ordnerebene. Sie ist nicht App-bezogen, und Linux wird nicht unterstützt. Installieren Sie den MARS-Agent (Microsoft Azure Recovery Services) auf jedem virtuellen Computer, den Sie mit dieser Methode sichern möchten.
- **Schützen von VMs mit Azure Backup Server:** Azure Backup Server ist kostenlos in Azure Backup enthalten. VMs werden im lokalen Azure Backup Server-Speicher gesichert. Danach wird Azure Backup Server in einem Tresor in Azure gesichert. Backup ist App-bezogen und bietet differenzierte Optionen für die Häufigkeit und Vermerkdauer von Sicherungen. Sie können Sicherungen auf App-Ebene z. B. für SQL Server oder SharePoint ausführen.

Aus Sicherheitsgründen verschlüsselt Azure Backup Daten während der Übertragung mithilfe von AES-256 und sendet sie über HTTPS an Azure. Gesicherte ruhende Daten in Azure werden mithilfe der [Speicherdienstverschlüsselung](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) verschlüsselt.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
_Azure Backup_

**Weitere Informationen**:

- Erfahren Sie mehr über den [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)-Dienst.
- Planen Sie eine [Sicherungsinfrastruktur für Azure-VMs](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction).

#### <a name="storage-snapshots"></a>Speichermomentaufnahmen

Azure-VMs werden als Seitenblobs in Azure Storage gespeichert.

- Momentaufnahmen erfassen den Blobzustand zu einem bestimmten Zeitpunkt.
- Als alternative Sicherungsmethode für Azure-VM-Datenträger können Sie eine Momentaufnahme von Speicherblobs erfassen und in ein anderes Speicherkonto kopieren.
- Sie können ein vollständiges Blob kopieren oder eine inkrementelle Momentaufnahmekopie verwenden, um nur Deltaänderungen zu kopieren und den Speicherplatz zu reduzieren.
- Als zusätzliche Vorsichtsmaßnahme können Sie das vorläufige Löschen für Blobspeicherkonten aktivieren. Wenn dieses Feature aktiviert ist, wird ein Blob nicht sofort gelöscht, sondern zum Löschen markiert. Während des Übergangszeitraums kann das Blob wiederhergestellt werden.

**Weitere Informationen**:

- Erfahren Sie mehr über [Azure Blob Storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).
- Erfahren Sie, wie Sie eine [Blobmomentaufnahme erstellen](https://docs.microsoft.com/azure/storage/blobs/storage-blob-snapshots).
- [Sehen Sie sich ein Beispielszenario](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) für die Sicherung des Blobspeichers an.
- [Lesen Sie mehr](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete) über das vorläufige Löschen.
- [Notfallwiederherstellung und erzwungenes Failover (Vorschau) in Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance)

#### <a name="third-party-backup"></a>Sicherungslösungen von Drittanbietern

Zusätzlich können Sie Drittanbieterlösungen verwenden, um Azure-VMs und -Speichercontainer in einem lokalen Speicher oder bei anderen Cloudanbietern zu sichern. Weitere Informationen finden Sie unter den [Sicherungslösungen im Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1).

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Einrichten der Notfallwiederherstellung für IaaS-Apps

Zusätzlich zum Schutz der Daten muss bei der BCDR-Planung berücksichtigt werden, wie Apps und Workloads bei einem Notfall verfügbar gehalten werden. Ziehen Sie für Workloads, die auf Azure-IaaS-VMs und mit Azure-Speicher ausgeführt werden, folgende Lösungen in Betracht:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery ist der primäre Azure-Dienst, mit dem Sie sicherstellen, dass Azure-VMs online geschaltet und VM-Apps verfügbar gemacht werden können, wenn ein Ausfall auftritt.

Site Recovery repliziert VMs von einer primären in eine sekundäre Azure-Region. Wenn ein Notfall auftritt, führen Sie ein Failover der VMs von der primären Region aus und greifen in der sekundären Region weiterhin normal darauf zu. Wenn der Betrieb wieder normal läuft, können Sie ein Failback der VMs zur primären Region ausführen.

  ![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png) _Site Recovery_

**Weitere Informationen**:

- Sehen Sie sich [Notfallwiederherstellungsszenarien für Azure-VMs](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) an.
- Erfahren Sie, wie Sie die [Notfallwiederherstellung für eine Azure-VM nach der Migration einrichten](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-replicate-after-migration).

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Bewährte Methode: Verwenden von verwalteten Datenträgern und Verfügbarkeitsgruppen

Azure verwendet Verfügbarkeitsgruppen, um VMs logisch zusammenzufassen und in einer Gruppe von anderen Ressourcen zu isolieren. VMs in einer Verfügbarkeitsgruppe werden auf mehrere Fehlerdomänen mit separaten Subsystemen verteilt, die vor lokalen Ausfällen geschützt sind. Die VMs sind auch auf mehrere Updatedomänen verteilt und verhindern gleichzeitige Neustarts aller VMs in der Gruppe.

Verwaltete Azure-Datenträger vereinfachen die Datenträgerverwaltung bei virtuellen Azure-Computern durch Verwaltung der Speicherkonten, die den VM-Datenträgern zugeordnet sind.

- Verwenden Sie nach Möglichkeit verwaltete Datenträger. Sie müssen nur den gewünschten Speichertyp und die erforderliche Datenträgergröße angeben, und Azure erstellt und verwaltet den Datenträger im Hintergrund für Sie.
- Sie können vorhandene Datenträger in verwaltete Datenträger konvertieren.
- Sie sollten VMs in Verfügbarkeitsgruppen erstellen, um eine hohe Resilienz und Verfügbarkeit zu erzielen. Bei geplanten oder ungeplanten Ausfällen stellen Verfügbarkeitsgruppen sicher, dass mindestens eine VM in der Gruppe verfügbar bleibt.

  ![Verwaltete Datenträger](./media/migrate-best-practices-security-management/managed-disks.png)
  _Verwaltete Datenträger_

**Weitere Informationen**:

- Lesen Sie die [Übersicht über verwaltete Datenträger](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).
- Erfahren Sie mehr über das [Konvertieren von Datenträgern in verwaltete Datenträger](https://docs.microsoft.com/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks).
- Erfahren Sie, wie Sie die [Verfügbarkeit virtueller Windows-Computer in Azure verwalten](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Bewährte Methode: Überwachen der Ressourcennutzung und -leistung

Sie haben Ihre Workloads möglicherweise aufgrund der enormen Skalierungsfunktionen nach Azure verlagert. Die Verlagerung allein bedeutet jedoch nicht, dass Azure ohne Eingaben Ihrerseits automatisch eine Skalierung implementiert. Beispiel:

- Wenn Ihre Marketingorganisation einen neuen Werbespot im Fernsehen schaltet, der 300% mehr Datenverkehr verursacht, könnte dies zu Problemen mit der Verfügbarkeit der Website führen. Ihr neu migrierte Workload könnte die zugewiesenen Obergrenzen erreichen und abstürzen.
- Ein weiteres Beispiel wäre ein verteilter Denial-of-Service-Angriff (DDoS) auf Ihre migrierte Workload. In diesem Fall sollten Sie keine Skalierung durchführen, sondern die Quelle der Angriffe daran hindern, Ihre Ressourcen zu erreichen.

Für diese beiden Fälle gibt es unterschiedliche Lösungen, aber Sie müssen in beiden Fällen wissen, was passiert. Dazu dient die Überwachung von Nutzung und Leistung.

- Azure Monitor unterstützt Sie dabei, diese Metriken zu ermitteln, und liefert Antworten mit Warnungen sowie Informationen zur automatischen Skalierung, Event Hubs, Logik-Apps und vielem mehr.
- Zusätzlich zur Azure-Überwachung können Sie Ihre SIEM-Drittanbieteranwendung integrieren, um die Azure-Protokolle auf Überprüfungs- und Leistungsereignisse zu überwachen.

  ![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
  _Azure Monitor_

**Weitere Informationen**:

- Weitere Informationen finden Sie unter [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview).
- [Informieren Sie sich über Best Practices](https://docs.microsoft.com/azure/architecture/best-practices/monitoring) für die Überwachung und Diagnose.
- Erfahren Sie mehr über die [automatische Skalierung](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling).
- Erfahren Sie, wie Sie [Azure-Daten an ein SIEM-Tool weiterleiten](https://docs.microsoft.com/azure/security-center/security-center-export-data-to-siem).

## <a name="best-practice-enable-diagnostic-logging"></a>Bewährte Methode: Aktivieren der Diagnoseprotokollierung

Azure-Ressourcen generieren recht viele Protokollierungsmetrik- und Telemetriedaten.

- Standardmäßig ist bei den meisten Ressourcentypen die Diagnoseprotokollierung nicht aktiviert.
- Indem Sie die Diagnoseprotokollierung für Ihre Ressourcen aktivieren, können Sie Protokollierungsdaten abfragen und basierend darauf Warnungen und Playbooks erstellen.
- Wenn Sie die Diagnoseprotokollierung aktivieren, verfügt jede Ressource über einen bestimmten Satz von Kategorien. Sie können eine oder mehrere Protokollierungskategorien sowie einen Speicherort für die Protokolldaten auswählen. Protokolle können an Event Hub, Azure Monitor-Protokolle oder ein Speicherkonto gesendet werden.

![Diagnoseprotokollierung](./media/migrate-best-practices-security-management/diagnostics.png)
_Diagnoseprotokollierung_

**Weitere Informationen**:

- Erfahren Sie mehr über das [Erfassen und Nutzen von Protokolldaten](https://docs.microsoft.com/azure/azure-monitor/platform/platform-logs-overview).
- [Erfahren Sie](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-schema), was für die Diagnoseprotokollierung unterstützt wird.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Bewährte Methode: Einrichten von Warnungen und Playbooks

Wenn die Diagnoseprotokollierung für Azure-Ressourcen aktiviert ist, können Sie damit beginnen, Protokollierungsdaten zu verwenden, um benutzerdefinierte Warnungen zu erstellen.

- Warnungen benachrichtigen Sie proaktiv, wenn bestimmte Bedingungen in Ihren Überwachungsdaten gefunden werden. Dann können Sie die Probleme beheben, bevor Ihre Systembenutzer diese bemerken. Sie können Warnungen zu Aspekten wie Metrikwerten, Protokollsuchabfragen, Aktivitätsprotokollereignissen, Plattformintegrität und Websiteverfügbarkeit einrichten.
- Wenn Warnungen ausgelöst werden, können Sie ein Logik-App-Playbook ausführen. Mit einem Playbook können Sie eine Antwort auf eine bestimmte Warnung automatisieren und orchestrieren. Playbooks basieren auf Azure Logic Apps. Sie können Playbooks selbst oder basierend auf Logik-App-Vorlagen erstellen.
- Ein einfaches Beispiel: Sie können eine Warnung erstellen, die ausgelöst wird, wenn für eine Netzwerksicherheitsgruppe ein Portscan ausgeführt wird. Sie können ein Playbook einrichten, das ausgeführt wird und die IP-Adresse der Scanquelle sperrt.
- Ein weiteres Beispiel wäre eine App mit Arbeitsspeicherverlust. Wenn die Arbeitsspeichernutzung einen bestimmten Punkt erreicht, kann ein Playbook den Prozess stoppen und neu starten.

  ![Warnungen](./media/migrate-best-practices-security-management/alerts.png)
  _Warnungen_

**Weitere Informationen**:

- Erfahren Sie mehr über [Warnungen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview).
- Informieren Sie sich über [Sicherheitsplaybooks, die auf Security Center-Warnungen reagieren](https://docs.microsoft.com/azure/security-center/security-center-playbooks).

## <a name="best-practice-use-the-azure-dashboard"></a>Bewährte Methode: Verwenden des Azure-Dashboards

Das Azure-Portal ist eine webbasierte einheitliche Konsole zum Erstellen, Verwalten und Überwachen aller Komponenten – von einfachen Web-Apps bis hin zu komplexen Cloudanwendungen. Es enthält ein anpassbares Dashboard und Optionen für Barrierefreiheit.

- Sie können mehrere Dashboards erstellen und für andere Benutzer freigeben, die Zugriff auf Ihre Azure-Abonnements haben.
- Mit diesem Freigabemodell erhält Ihr Team Einblick in die Azure-Umgebung, sodass die Teammitglieder Systeme in der Cloud proaktiv verwalten können.

  ![Azure-Dashboard](./media/migrate-best-practices-security-management/dashboard.png)
  _Azure-Dashboard_

**Weitere Informationen**:

- Erfahren Sie, wie Sie ein [Dashboard erstellen](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards).
- Erfahren Sie mehr über die [Dashboardstruktur](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-structure).

## <a name="best-practice-understand-support-plans"></a>Bewährte Methode: Verstehen der Supportpläne

Sie müssen zu einem bestimmten Zeitpunkt mit Ihrem Supportteam oder den Microsoft-Supportmitarbeitern zusammenarbeiten. Es ist von entscheidender Bedeutung, eine Reihe von Richtlinien und Verfahren für den Support in Szenarien wie z.B. einer Notfallwiederherstellung einzurichten. Darüber hinaus müssen Ihre Administratoren und Supportmitarbeiter in der Implementierung dieser Richtlinien geschult sein.

- Im unwahrscheinlichen Fall, dass ein Problem mit einem Azure-Dienst sich auf Ihre Workload auswirkt, müssen Ihre Administratoren wissen, wie sie auf möglichst geeignete und effiziente Weise ein Supportticket an Microsoft übermitteln.
- Machen Sie sich mit den verschiedenen Supportplänen vertraut, die für Azure angeboten werden. Diese reichen von Reaktionszeiten für Developer-Instanzen bis hin zu Premier Support mit einer Reaktionszeit von weniger als 15 Minuten.

  ![Supportpläne](./media/migrate-best-practices-security-management/support.png)
  _Supportpläne_

**Weitere Informationen**:

- Lesen Sie eine [Übersicht über Azure-Supportpläne](https://azure.microsoft.com/support/options).
- Erfahren Sie mehr über [Vereinbarungen zum Servicelevel (SLAs)](https://azure.microsoft.com/support/legal/sla).

## <a name="best-practice-manage-updates"></a>Bewährte Methode: Verwalten von Updates

Azure-VMs immer mit den neuesten Betriebssystem- und Softwareupdates auf dem neuesten Stand zu halten, ist eine gewaltige Aufgabe. Die Fähigkeit, alle VMs zu ermitteln, herauszufinden, welche Updates erforderlich sind, und diese Updates automatisch aufzuspielen, ist extrem wertvoll.

- Sie können die Updateverwaltung in Azure Automation für Betriebssystemupdates für Ihre Windows- und Linux-Computer verwenden, die in Azure, in lokalen Umgebungen oder bei anderen Cloudanbietern bereitgestellt werden.
- Verwenden Sie die Updateverwaltung auch, um schnell den Status der verfügbaren Updates auf allen Agent-Computern auszuwerten und die Installation der Updates zu verwalten.
- Sie können die Updateverwaltung für virtuelle Computer direkt in einem Azure Automation-Konto aktivieren. Sie können auch eine einzelne VM über die VM-Seite im Azure-Portal aktualisieren.
- Darüber hinaus können Azure-VMs bei System Center Configuration Manager registriert werden. Danach können Sie die Configuration Manager-Workload nach Azure migrieren und Berichterstellung und Softwareupdates über eine einzige Webschnittstelle ausführen.

  ![VM-Updates](./media/migrate-best-practices-security-management/updates.png)
  _Updates_

**Weitere Informationen**:

- Erfahren Sie mehr über die [Updateverwaltung in Azure](https://docs.microsoft.com/azure/automation/automation-update-management).
- Erfahren Sie, wie Sie [Configuration Manager in die Updateverwaltung integrieren](https://docs.microsoft.com/azure/automation/oms-solution-updatemgmt-sccmintegration).
- [Häufig gestellte Fragen](https://docs.microsoft.com/sccm/core/understand/configuration-manager-on-azure) zu Configuration Manager in Azure.

## <a name="implement-a-change-management-process"></a>Implementieren eines Change Management-Prozesses

Wie bei jedem Produktionssystem kann sich jede Art von Änderung auf Ihre Umgebung auswirken. Ein Change Management-Prozess, in dem Anforderungen gesendet werden müssen, damit Änderungen am Produktionssystem vorgenommen werden können, ist eine wertvolle Ergänzung zu Ihrer migrierten Umgebung.

- Sie können Best Practices-Frameworks für das Change Management erstellen, um bei Administratoren und Supportmitarbeitern das Bewusstsein für solche Prozesse zu schärfen.
- Sie können Azure Automation verwenden, um Unterstützung bei der Konfigurationsverwaltung und Änderungsnachverfolgung für Ihre migrierten Workflows zu erhalten.
- Wenn Sie einen Change Management-Prozess erzwingen, können Sie Überwachungsprotokolle verwenden, um Azure-Änderungsprotokolle mit vermutlich (oder nicht) vorhandenen Änderungsanforderungen zu verknüpfen. Das bedeutet Folgendes: Wenn Sie eine Änderung bemerken, die ohne entsprechende Änderungsanforderung durchgeführt wurde, können Sie untersuchen, warum der Prozess nicht wie gewünscht funktioniert hat.

Azure bietet in Azure Automation eine Lösung für die Änderungsnachverfolgung:

- Die Lösung verfolgt Änderungen an Windows- und Linux-Software und -Dateien, an Windows-Registrierungsschlüsseln, an Windows-Diensten und an Linux-Daemons nach.
- Änderungen an überwachten Servern werden zur Verarbeitung an den Azure Monitor-Dienst in der Cloud gesendet.
- Auf die empfangenen Daten wird Logik angewendet, und der Clouddienst zeichnet die Daten auf.
- Im Dashboard der Änderungsnachverfolgung können Sie ganz einfach die Änderungen erkennen, die an Ihrer Serverinfrastruktur vorgenommen wurden.

  ![Change Management](./media/migrate-best-practices-security-management/change.png)
  _Change Management_

**Weitere Informationen**:

- Erfahren Sie mehr über die [Änderungsnachverfolgung](https://docs.microsoft.com/azure/automation/automation-change-tracking).
- Erfahren Sie mehr über [Azure Automation-Funktionen](https://docs.microsoft.com/azure/automation/automation-intro).

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über weitere Best Practices:

- [Best Practices](./migrate-best-practices-networking.md) für Netzwerkfunktionen nach der Migration.
- [Best Practices](./migrate-best-practices-costs.md) für die Kostenverwaltung nach der Migration.
