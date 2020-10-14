---
title: Azure-Sicherheit – bewährte Methoden
description: Erfahren Sie, welche bewährten Sicherheitsmethoden Microsoft für Azure empfiehlt.
author: JanetCThomas
ms.author: mas
ms.date: 09/18/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: d66e0c59d7c3e55a97ae4cee7c07ea0ec4ee7a74
ms.sourcegitcommit: 81246e185cee53fed591c4bafd56cde7d58e26f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898249"
---
# <a name="azure-security-best-practices"></a>Azure-Sicherheit – bewährte Methoden

Dies sind die wichtigsten bewährten Sicherheitsmethoden, die Microsoft für Azure auf der Grundlage dessen empfiehlt, was wir von Kunden und in unseren eigenen Umgebungen gelernt haben.

Eine Videopräsentation dieser bewährten Methoden finden Sie in der [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/video-hub/top-10-best-practices-for-azure-security/m-p/1698837).

## <a name="1-people-educate-teams-about-the-cloud-security-journey"></a>1. Personen: Schulen von Teams über den Weg zur Cloudsicherheit

*Das Team muss sich darüber im Klaren sein, auf welchem Weg es sich befindet.*

**Was**: Schulen Sie Ihre Sicherheits- und IT-Teams über den Weg zur Cloudsicherheit und die damit verbundenen Änderungen, einschließlich:

- Änderungen wegen Bedrohungen in der Cloud
- Das Modell der gemeinsamen Zuständigkeit und seine Auswirkungen auf die Sicherheit
- Änderungen der Kultur- und Rollenverantwortlichkeit, die in der Regel mit der Cloudeinführung verbunden sind

**Grund**: Die Umstellung auf die Cloud ist eine bedeutende Änderung, die einen Wechsel der Denkweise und des Ansatzes in puncto Sicherheit erfordert. Wenngleich sich die Ergebnisse der Sicherheit für die Organisation nicht ändern, ändert sich in der Cloud oft die beste Methode, dies zu erreichen – manchmal signifikant.

In vielerlei Hinsicht ähnelt die Umstellung auf die Cloud dem Umzug von einem Eigenheim in ein Luxusapartment-Hochhaus. Sie verfügen immer noch über eine grundlegende Infrastruktur (Sanitärinstallation, Elektrizität usw.) und führen ähnliche Aktivitäten durch (soziale Kontakte, Kochen, TV und Internet usw.), aber es gibt oft einen Unterschied hinsichtlich dessen, was das Gebäude sonst noch so bietet (Fitnessstudio, Restaurants usw.), wer diese Angebote bereitstellt und verwaltet, und Ihrer täglichen Routine.

**Wer**: Alle Personen in der Sicherheits- und IT-Organisation mit Sicherheitszuständigkeiten (von CIO/CISO bis zu technischen Experten) sollten mit diesem Kontext und den Änderungen vertraut sein.

**Vorgehensweise**: Bieten Sie Teams den Kontext, der für eine erfolgreiche Bereitstellung und den Betrieb während des Übergangs zur Cloudumgebung erforderlich ist.
Microsoft hat Lektionen veröffentlicht, die wir von unseren Kunden und unserer eigenen IT-Organisation bei der Migration in die Cloud gelernt haben:

- Wie [Cloudsicherheitsfunktionen](../organize/cloud-security.md) sich in der Sicherheitsorganisation weiterentwickeln
- [Entwicklung der Bedrohungsumgebung, von Rollen und digitalen Strategien](/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
- [Transformation von Sicherheit, Strategien, Tools und Bedrohungen](/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
- [Erkenntnisse von Microsoft aus der Erfahrung, eine Hyperscalecloudumgebung zu sichern](/security/compass/microsoft-security-compass-introduction#microsoft-security-practices-1349), die Ihnen auf dem Weg nützen können.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [GS-4: Ausrichten von Organisationsrollen, Zuständigkeiten und Verantwortlichkeiten](/azure/security/benchmarks/security-controls-v2-governance-strategy#gs-3-align-organization-roles-responsibilities-and-accountabilities).

## <a name="2-people-educate-teams-on-cloud-security-technology"></a>2. Personen: Schulen der Teams in Cloudsicherheitstechnologie

*Personen müssen wissen, welchen Weg sie gehen.*

**Was**: Stellen Sie sicher, dass Ihren Teams Zeit für technische Schulungen zum Sichern von Cloudressourcen bleibt, einschließlich:

- Cloudtechnologie und Cloudsicherheitstechnologie
- Empfohlene Konfigurationen und bewährte Methoden
- Wo sie mehr technische Details als nötig lernen können

**Grund**: Technische Teams benötigen Zugriff auf technische Informationen, um fundierte Sicherheitsentscheidungen treffen zu können. Technische Teams sind in der Lage, neue Technologien in der Praxis zu erlernen, aber die Menge der Details in der Cloud übersteigt häufig ihre Möglichkeit, das Lernen in ihre tägliche Routine zu integrieren.

Die Strukturierung der dedizierten Zeit für technisches Lernen trägt dazu bei, dass Personen Zeit haben, Vertrauen in ihre Fähigkeit zu gewinnen, die Cloudsicherheit zu bewerten und zu überlegen, wie sie ihre bestehenden Qualifikationen und Prozesse anpassen können. Selbst die talentiertesten speziellen militärischen Einsatzteams benötigen Schulungen und Informationen, um ihr Bestes geben zu können.

**Wer**: Alle Rollen (in Sicherheits- und IT-Abteilungen), die direkt mit der Cloudtechnologie interagieren, sollten Zeit für technisches Lernen über Cloudplattformen und deren Absicherung aufwenden.

Darüber hinaus sollten sich Sicherheits- und IT-Technik-Manager (und häufig Projektmanager) mit einigen technischen Details zum Sichern von Cloudressourcen vertraut machen (da ihnen dies hilft, Cloudinitiativen effektiver zu leiten und zu koordinieren).

**Vorgehensweise**: Sorgen Sie dafür, dass technische Sicherheitsfachleute Zeit für eine eigenverantwortliche Schulung zur Absicherung von Cloudressourcen finden. Es ist zwar nicht immer realisierbar, aber ermöglichen Sie idealerweise den Zugang zu formalen Schulungen mit erfahrenen Kursleitern und praktischen Übungseinheiten.

> [!Important]
> Identitätsprotokolle sind wichtig, um den Zugriff in der Cloud zu steuern, haben jedoch in der lokalen Sicherheit häufig keine Priorität. Daher sollten Sicherheitsteams sich darauf konzentrieren, mit diesen Protokollen vertraut zu werden.

Microsoft bietet umfassende Ressourcen, die technische Experten beim Sichern von Azure-Ressourcen und Berichten der Konformität unterstützen:

 - Azure Security
    - AZ-500-[Lernpfad](/learn/certifications/exams/az-500?tab=tab-learning-paths) (und Zertifizierung)
   - [Vergleichstest für die Azure-Sicherheit (Azure Security Benchmark, ASB)](/azure/security/benchmarks/) – empfohlene bewährte Methoden und Steuerungen für die Azure-Sicherheit
     - [Sicherheitsbaselines für Azure](/azure/security/benchmarks/security-baselines-overview) – Anwendung von ASB für einzelne Azure-Dienste
   - [Bewährte Methoden für Microsoft-Sicherheit](/security/compass/microsoft-security-compass-introduction) – Videos und Dokumentation
- Azure – Compliance
   - [Tutorial: Verbessern der Einhaltung gesetzlicher Vorschriften](/azure/security-center/security-center-compliance-dashboard) – Auswertung mit Azure Security Center
 - Identitätsprotokolle und Sicherheit 
   - [Website mit Dokumentation zur Azure-Sicherheit](/azure/security/)
   - Azure AD-Authentifizierung – [YouTube-Serie](https://www.youtube.com/playlist?list=PLLasX02E8BPD5vC2XHS_oHaMVmaeHHPLy) 
   - [Securing Azure environments with Azure Active Directory](https://azure.microsoft.com/resources/securing-azure-environments-with-azure-active-directory/) (Sichern von Azure-Umgebungen mit Azure Active Directory) 

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [GS-4: Ausrichten von Organisationsrollen, Zuständigkeiten und Verantwortlichkeiten](/azure/security/benchmarks/security-controls-v2-governance-strategy#gs-3-align-organization-roles-responsibilities-and-accountabilities)

## <a name="3-process-assign-accountability-for-cloud-security-decisions"></a>3. Prozess: Zuweisen von Verantwortlichkeit für Cloudsicherheitsentscheidungen

*Wenn niemand dafür verantwortlich ist, Sicherheitsentscheidungen zu treffen, werden sie nicht getroffen.*

**Was**: Legen Sie fest, wer für die einzelnen Sicherheitsentscheidungen für die Azure-Unternehmensumgebung verantwortlich ist.

**Grund**: Die eindeutige Verantwortung für Sicherheitsentscheidungen beschleunigt die Cloudeinführung *und* erhöht die Sicherheit. Ist sie nicht zugewiesen, führt dies in der Regel zu Friktionen, da sich niemand als autorisiert betrachtet, Entscheidungen zu treffen, niemand weiß, wer um eine Entscheidung gebeten werden soll, und niemand einen Anreiz dafür sieht, für eine fundierte Entscheidung zu recherchieren. Diese Friktionen beeinträchtigen häufig Geschäftsziele, Entwicklerzeitpläne, IT-Ziele und Sicherheitszusicherungen mit folgenden Konsequenzen:

- Stockende Projekte, die auf die Sicherheitsgenehmigung warten 
- Unsichere Bereitstellungen, die nicht auf die Sicherheitsgenehmigung warten konnten 

**Wer**: Die Führungskräfte im Sicherheitsbereich bestimmen, welche Teams oder Einzelpersonen für Sicherheitsentscheidungen zur Cloud verantwortlich sind.

**Vorgehensweise**: Legen Sie Gruppen (oder Einzelpersonen) fest, die dafür verantwortlich sind, wichtige Sicherheitsentscheidungen zu treffen.

Dokumentieren Sie diese Verantwortlichen und ihre Kontaktinformationen, und informieren Sie die Sicherheits-, IT- und Cloudteams darüber, um sicherzustellen, dass alle Rollen sie problemlos kontaktieren können.

Dies sind die typischen Bereiche, in denen Sicherheitsentscheidungen erforderlich sind, und die Teams, die üblicherweise die Entscheidungen treffen.

| Entscheidung         | BESCHREIBUNG           | Typisches Team  |
| ------------- |-------------| -----|
| Netzwerksicherheit | Konfiguration und Wartung von Azure Firewall, virtuellen Netzwerkgeräten (und zugehörigem Routing), WAFs, NSGs, ASGs usw. |    *In der Regel das Team für [Infrastruktur- und Endpunktsicherheit](../organize/cloud-security-infrastructure-endpoint.md) mit Konzentration auf Netzwerksicherheit*  |
| Netzwerkverwaltung | Unternehmensweite Zuordnung zu virtuellem Netzwerk und Subnetz  | *Üblicherweise das bestehende Netzwerkbetriebsteam in der [zentralen IT-Abteilung](../organize/central-it.md)* |
| Serverendpunktsicherheit | Überwachen und Korrigieren der Serversicherheit (Patching, Konfiguration, Endpunktsicherheit usw.)  | *In der Regel das Team der [zentralen IT-Abteilung](../organize/central-it.md) und das Team für [Infrastruktur- und Endpunktsicherheit](../organize/cloud-security-infrastructure-endpoint.md) gemeinsam* |
| Überwachung und Reaktion auf Incidents | Untersuchen und Beheben von Sicherheitsvorfällen in SIEM oder Quellkonsole (Azure Security Center, Azure AD Identity Protection usw.) | *Üblicherweise das Team für [Sicherheitsvorgänge](../organize/cloud-security-operations-center.md)* |
| Richtlinienverwaltung | Festlegen von Anweisungen für die Verwendung der rollenbasierten Zugriffssteuerung (Role Based Access Control, RBAC), Azure Security Center, Administrator-Schutzstrategie und Azure Policy zum Steuern von Azure-Ressourcen | *In der Regel die Teams für [Richtlinien und Standards](../organize/cloud-security-policy-standards.md) + [Sicherheitsarchitektur](../organize/cloud-security-architecture.md) gemeinsam* |
| Identitätssicherheit und -standards | Festlegen von Anweisungen für Azure AD-Verzeichnisse, PIM/PAM-Verwendung, MFA, Kennwort-/Synchronisierungskonfiguration, Anwendungsidentitätsstandards | *In der Regel die Teams für [Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md) + [Richtlinien und Standards](../organize/cloud-security-policy-standards.md) + [Sicherheitsarchitektur](../organize/cloud-security-architecture.md) gemeinsam*  |

> [!Note]
>- Stellen Sie sicher, dass Entscheidungsträger in ihrem Bereich der Cloud über die entsprechende Ausbildung verfügen, um dieser Verantwortung gerecht zu werden.
>- Stellen Sie sicher, dass Entscheidungen in Richtlinien und Standards dokumentiert werden, um Unterlagen bereitzustellen und die Organisation langfristig zu unterstützen.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [GS-4: Ausrichten von Organisationsrollen, Zuständigkeiten und Verantwortlichkeiten](/azure/security/benchmarks/security-controls-v2-governance-strategy#gs-3-align-organization-roles-responsibilities-and-accountabilities)

## <a name="4-process-update-incident-response-ir-processes-for-cloud"></a>4. Prozess: Aktualisieren von Prozessen für die Reaktion auf Vorfälle (Incident Response, IR) für die Cloud

*Sie haben mitten in der Krise keine Zeit zur Krisenplanung.*

**Was**: Aktualisieren Sie Prozesse, und bereiten Sie Analysten auf die Reaktion auf Sicherheitsvorfälle auf Ihrer Azure-Cloudplattform vor (einschließlich sämtlicher [nativer Tools zur Bedrohungserkennung](../get-started/security.md#step-1-establish-essential-security-practices), die Sie übernommen haben). Aktualisieren Sie Prozesse, bereiten Sie das Team vor, und üben Sie mit simulierten Angriffen, damit es bei der Untersuchung von Vorfällen, ihrer Behebung und der Erkennung von Bedrohungen beste Leistung bietet.

**Grund**: Aktive Angreifer stellen ein unmittelbares Risiko für die Organisation dar, das schnell zu einer schwer kontrollierbaren Situation werden kann, sodass Sie schnell und effektiv auf Angriffe reagieren müssen. Dieser Prozess der Reaktion auf Vorfälle (IR) muss für Ihre gesamte Infrastruktur einschließlich aller Cloudplattformen, die Unternehmensdaten, Systeme und Konten hosten, wirksam sein.

Trotz Ähnlichkeiten in vielerlei Hinsicht bestehen wichtige technische Unterschiede zwischen lokalen Systemen, die vorhandene Prozesse unterbrechen können, und Cloudplattformen – in der Regel, weil Informationen in einer anderen Form verfügbar sind. Wenn es darum geht, schnell auf eine unbekannte Umgebung zu reagieren, können Sicherheitsanalysten möglicherweise auch vor Herausforderungen stehen, die sie bremsen können (insbesondere, wenn sie nur für klassische lokale Architekturen und Netzwerk-/Datenträgerforensikansätze geschult wurden).

**Wer**: Die Modernisierung der IR-Prozesse wird in der Regel durch das Team für [Sicherheitsvorgänge](../organize/cloud-security-operations-center.md) eingeleitet, mit Unterstützung des Fachwissens anderer Gruppen.

- *Förderung*: Diese Prozessmodernisierung wird in der Regel vom Direktor für Sicherheitsvorgänge oder einer entsprechenden Person gefördert.
- *Ausführung*: Die Anpassung vorhandener Prozesse (oder ihre erstmalige Niederschrift) ist eine gemeinsame Arbeit, die die Folgenden einbezieht:  
  - **[Sicherheitsvorgänge](../organize/cloud-security-operations-center.md)** : Incident Management-Team oder -Führungskräfte – leiten Aktualisierungen zur Integration wichtiger externer Projektbeteiligter, einschließlich Rechts- und Kommunikations-/Public Relations-Teams.
  - **[Sicherheitsvorgänge](../organize/cloud-security-operations-center.md)** : Sicherheitsanalysten – verfügen über Fachkenntnisse zur Untersuchung und Selektierung von technischen Vorfällen.
  - **[Zentrale IT-Abteilung](../organize/central-it.md)** : verfügt über Fachkenntnisse zur Cloudplattform (direkt über das Cloudkompetenzzentrum oder über externe Berater).

**Vorgehensweise**: Aktualisieren Sie Prozesse, und bereiten Sie das Team vor, damit es weiß, was beim Auffinden eines aktiven Angreifers zu tun ist.

- **Prozesse und Playbooks**: Passen Sie vorhandene Untersuchungen, Wiederherstellungs- und Bedrohungserkennungsprozesse den Unterschieden in der Funktionsweise von Cloudplattformen an (neue/verschiedene Tools, Datenquellen, Identitätsprotokolle usw.).

- **Bildung**: Schulen Sie Analysten in der gesamten Cloudtransformation, in technischen Details zur Funktionsweise der Plattform und über neue/aktualisierte Prozesse, damit sie die Unterschiede kennen und wissen, wo sie finden, was sie benötigen.

_**Schwerpunktbereiche**_: Obwohl viele Details in den Ressourcenlinks beschrieben werden, sollten Sie Ihre Schulungs- und Planungsmaßnahmen auf diese Schwerpunktbereiche konzentrieren:

- **Modell der gemeinsamen Verantwortung und Cloudarchitekturen**: Für einen Sicherheitsanalysten ist Azure ein softwaredefiniertes Rechenzentrum, das viele Dienste bereitstellt, z. B. virtuelle Computer (vertraut) und andere, die sich stark von der lokalen Umgebung unterscheiden, wie z. B. Azure SQL Azure Functions usw., wo sich die besten Daten in den Dienstprotokollen oder den spezialisierten Diensten zur Bedrohungserkennung befinden und nicht in Protokollen für das zugrunde liegende Betriebssystem/die zugrunde liegenden VMs (die von Microsoft betrieben werden und mehreren Kunden dienen). Analysten müssen diesen Kontext verstehen und in Ihre täglichen Workflows integrieren, damit sie wissen, welche Daten zu erwarten sind, wo sie zu finden sind und in welchem Format sie vorliegen.
- **Endpunkt-Datenquellen**: Das Abrufen von Erkenntnissen und Daten für Angriffe und Schadsoftware auf Servern, die in der Cloud gehostet werden, ist mit nativen Clouderkennungstools wie Azure Security Center und EDR-Systemen im Gegensatz zu herkömmlichen Ansätzen des direkten Datenträgerzugriffs häufig schneller, einfacher und präziser. Direkte Datenträgerforensik ist nicht nur für Szenarios verfügbar, in denen sie möglich und für rechtliche Schritte erforderlich ist ([Computerforensik in Azure](/azure/architecture/example-scenario/forensics/)), sondern häufig die effizienteste Methode, um Angriffe zu erkennen und zu untersuchen.
- **Netzwerk- und Identitätsdatenquellen**: Viele Funktionen von Cloudplattformen verwenden die Identität in erster Linie für die Zugriffssteuerung, etwa für den Zugriff auf das Azure-Portal (auch wenn weitgehend Netzwerkzugriffssteuerungen eingesetzt werden). Dies erfordert, dass Analysten ein Verständnis der Cloudidentitätsprotokolle entwickeln, um ein umfassendes Bild der Angreiferaktivität (und legitimer Benutzeraktivität) zur Untersuchung und Behebung von Vorfällen erhalten. Identitätsverzeichnisse und -protokolle unterscheiden sich auch von der lokalen Umgebung, da sie in der Regel auf SAML-, OAuth- und OIDC- sowie Cloudverzeichnissen statt auf LDAP, Kerberos, NTLM und Active Directory basieren, die häufig lokal anzutreffen sind.
- **Praktische Übungen**: Simulierte Angriffe und Antworten können den Aufbau eines „Muskelgedächtnisses“ der Organisation und der technischen Bereitschaft Ihrer Sicherheitsanalysten, Bedrohungserkenner, Incident Manager und anderer Projektbeteiligte in Ihrer Organisation fördern. Das Lernen in der Praxis und die Anpassung ist ein natürlicher Bestandteil der Reaktion auf Vorfälle, aber Sie sollten minimieren, was Sie in einer Krise lernen müssen.

**Wichtige Ressourcen:**

- [Referenzleitfaden für die Reaktion auf Vorfälle](https://aka.ms/IRRG) (Incident Response Reference Guide, IRRG)
- Anleitung zum [Entwickeln Ihres eigenen Prozesses für die Reaktion auf Sicherheitsvorfälle](https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/)
- [Protokollierung und Warnung in Azure](/azure/security/fundamentals/log-audit)
- Bewährte Methoden für Microsoft-Sicherheit
  - [Transformation von Sicherheit, Strategien, Tools und Bedrohungen](/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
  - [Sicherheitsvorgänge](/security/compass/security-operations-videos-and-decks)
- Erkenntnisse von Microsoft aus dem Operationszentrum für Cyberabwehr (Cyber Defense Operations Center, CDOC)
  - [Insgesamt gelernte Lektionen](https://www.microsoft.com/security/blog/2019/02/21/lessons-learned-from-the-microsoft-soc-part-1-organization/)
  - [Vorfalluntersuchung](https://www.microsoft.com/security/blog/2019/12/23/ciso-series-lessons-learned-from-the-microsoft-soc-part-3b-a-day-in-the-life/)
  - [Vorfallbehebung](https://www.microsoft.com/security/blog/2020/05/04/lessons-learned-microsoft-soc-part-3c/)

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [IR-1: Vorbereitung – Aktualisieren des Prozesses zur Reaktion auf Vorfälle für Azure](/azure/security/benchmarks/security-controls-v2-incident-response#ir-1-preparation--update-incident-response-process-for-azure).

## <a name="5-process-establish-security-posture-management"></a>5. Prozess: Einrichten der Sicherheitsstatusverwaltung

*Lernen Sie sich zunächst selbst kennen.*

**Was**: Stellen Sie sicher, dass Sie den Sicherheitsstatus Ihrer Azure-Umgebung aktiv verwalten durch:

- Zuweisen des klaren Besitzes von Zuständigkeiten für
  - Überwachung des Sicherheitsstatus
  - Mindern von Risiken für Ressourcen
- Automatisieren und Vereinfachen dieser Aufgaben

**Grund**: Durch das schnelle Ermitteln und Beheben allgemeiner Sicherheitsrisiken wird das Risiko für Ihre Organisation wesentlich verringert.

Das softwaredefinierte Wesen von Cloudrechenzentren ermöglicht die kontinuierliche Überwachung von Sicherheitsrisiken (Softwaresicherheitsanfälligkeiten, Sicherheitsfehlkonfigurationen usw.) mit umfangreicher Ressourceninstrumentierung. Mit der Geschwindigkeit, mit der Entwickler und IT-Teams virtuelle Computer, Datenbanken und andere Ressourcen bereitstellen können, entsteht auch das Bedürfnis, sicherzustellen, dass die Ressourcen sicher konfiguriert und aktiv überwacht werden.

Diese neuen Funktionen bieten neue Möglichkeiten, aber damit ihr Wert erkannt wird, muss die Verantwortlichkeit für ihre Verwendung zugewiesen werden. Bei der konsistenten Ausführung für sich schnell entwickelnde Cloudvorgänge müssen auch die menschlichen Prozesse so einfach und automatisiert wie möglich bleiben. Weitere Informationen finden Sie in [Prinzipien für den Sicherheitsentwurf](/azure/architecture/framework/security/security-principles) unter „Fördern der Einfachheit“.

> [!Note]
 >Das Ziel der Vereinfachung und Automatisierung ist nicht, Aufträge loszuwerden, sondern Menschen die Belastung sich wiederholender Aufgaben abzunehmen, damit sie sich auf höherwertigere menschliche Aktivitäten wie das Engagement in IT- und DevOps-Teams und deren Schulung konzentrieren können.

**Wer**: Dies ist in der Regel in zwei Gruppen von Zuständigkeiten unterteilt:

- **[Sicherheitsstatusverwaltung](../organize/cloud-security-posture-management.md)** : Diese neuere Funktion ist oft eine Weiterentwicklung vorhandener Sicherheitsrisikoverwaltungs- oder Governancefunktionen. Dies umfasst das Überwachen des gesamten Sicherheitsstatus mithilfe von Secure Score von Azure Security Center und anderer Datenquellen, die aktive Zusammenarbeit mit Ressourcenbesitzern, um Risiken zu verringern, und das Melden von Risiken an die Führungskräfte im Sicherheitsbereich.
- **Wiederherstellung der Sicherheit**: Weisen Sie die Verantwortung für die Behebung dieser Risiken den Teams zu, die für die Verwaltung dieser Ressourcen zuständig sind.
Dies sollten entweder die DevOps-Teams sein, die ihre eigenen Anwendungsressourcen verwalten, oder die technologiespezifischen Teams in der **[zentralen IT-Abteilung](../organize/central-it.md)** :

  - _**Compute- und App-Ressourcen:**_
    - **App Services**: Anwendungsentwicklungs-/Sicherheitsteam(s)
    -   **Container**: Anwendungsentwicklung und/oder Infrastruktur-/IT-Betrieb
    - **VMs/Skalierungsgruppen/Compute**: IT-/Infrastrukturbetrieb
  - _**Daten- und Speicherressourcen:**_
    - **SQL/Redis/Data Lake Analytics/Data Lake Store**: Datenbankteam
    - **Speicherkonten**: Speicher-/Infrastrukturteam
  - _**Identitäts- und Zugriffsressourcen:**_
    - **Abonnements**: Identitätsteam(s)
    - **Schlüsseltresor**: Identitäts- oder Informations-/Datensicherheitsteam
  - _**Netzwerkressourcen**_: Netzwerksicherheitsteam
  - _**IoT-Sicherheit**_: IoT-Betriebsteam

**Vorgehensweise**: Sicherheit ist die Aufgabe aller, aber es wissen noch nicht alle, wie wichtig sie ist, was zu tun und wie es zu tun ist.

- Weisen Sie Ressourcenbesitzern die Verantwortung für das Sicherheitsrisiko zu, genau so, wie sie für Verfügbarkeit, Leistung, Kosten und andere Erfolgsfaktoren verantwortlich sind.
- Unterstützen Sie Ressourcenbesitzer, indem Sie ihnen klar machen, warum das Sicherheitsrisiko für Ihre Ressourcen wichtig ist, was sie tun sollten, um Risiken zu verringern, und wie sie dies mit minimalem Produktivitätsverlust implementieren können.

> [!IMPORTANT]
> Die Erläuterungen, warum welche Ressourcen wie gesichert werden, sind häufig für verschiedene Ressourcentypen und Anwendungen ähnlich, aber es ist wichtig, dass Sie sie mit dem in Zusammenhang bringen, was die einzelnen Teams bereits wissen und sie beschäftigt. Sicherheitsteams sollten vertrauenswürdige Ratgeber und Partner ihrer IT- und DevOps-Kollegen sein und diesen Teams zum Erfolg verhelfen.  

**Tools**: [Secure Score](/azure/security-center/security-center-secure-score) in Azure Security Center bietet für eine Vielzahl von Ressourcen in Azure eine Bewertung der wichtigsten Sicherheitsinformationen. Dies sollte Ihr Ausgangspunkt bei der Statusverwaltung sein, der durch benutzerdefinierte Azure-Richtlinien und andere Mechanismen nach Bedarf ergänzt werden kann.

**Häufigkeit**: Richten Sie ein Intervall (in der Regel monatlich) ein, um die Azure-Sicherheitsbewertung zu prüfen und Initiativen mit bestimmten Optimierungszielen zu planen. Die Häufigkeit kann bei Bedarf gesteigert werden.

> [!Tip]
 > Machen Sie vielleicht aus der Aktivität ein Spiel, um das Engagement zu steigern, indem Sie z. B. unterhaltsame Wettbewerbe veranstalten und Preisen für die DevOps-Teams in Aussicht stellen, die ihre Bewertung am meisten steigern.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [GS-3: Definieren der Strategie für die Sicherheitsstatusverwaltung](/azure/security/benchmarks/security-controls-v2-governance-strategy#gs-2-define-security-posture-management-strategy).

## <a name="6-technology-require-passwordless-or-multi-factor-authentication-mfa"></a>6. Technologie: Kennwortlose oder mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) fordern

*Würden Sie um die Sicherheit Ihres Unternehmens wetten, dass professionelle Angreifer das Kennwort Ihres Administrators nicht erraten oder stehlen können?*

**Was**: Legen Sie fest, dass alle Administratoren mit potenziell kritischen Auswirkungen die kennwortlose oder mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) verwenden müssen.

**Grund**: Ebenso wie die einfachen Haustürschlüssel das Haus nicht vor einem modernen Einbrecher schützen, können Kennwörter keine Konten vor häufigen Angriffe schützen, wie sie heutzutage vorkommen. Technische Details werden unter [Your Pa$$word doesn't matter](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984) (Ihr Ke$$wort spielt keine Rolle) beschrieben.

MFA war zwar einmal ein mühseliger zusätzlicher Schritt, aber heute verbessern kennwortlose Ansätze die Anmeldeerfahrung mithilfe biometrischer Ansätze wie der Gesichtserkennung in Windows Hello und auf mobilen Geräten (wo Sie sich weder ein Kennwort merken noch es eingeben müssen). Darüber hinaus erinnern sich Zero Trust-Ansätze an vertrauenswürdige Geräte, was die Aufforderung zu lästigen Out-of-Band-MFA-Aktionen reduziert (siehe [Anmeldehäufigkeit von Benutzern](/azure/active-directory/conditional-access/howto-conditional-access-session-lifetime#user-sign-in-frequency)).

**Wer**: Die Kennwort- und MFA-Initiative wird in der Regel von [Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md) und/oder [Sicherheitsarchitektur](../organize/cloud-security-architecture.md) geleitet.

- *Förderung*: Dies wird in der Regel von CISO, CIO oder vom Director of Identity gefördert.
- *Ausführung*: Dies ist eine gemeinsame Arbeit, die die Folgenden einbezieht:
  - Das [Richtlinien und Standards](../organize/cloud-security-policy-standards.md)-Team stellt klare Anforderungen auf.
  - [Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md) oder [zentrale IT-Abteilung](../organize/central-it.md) implementieren die Richtlinie.
  - Die [Sicherheitskonformitätsverwaltung](../organize/cloud-security-compliance-management.md) überwacht die Einhaltung.

**Vorgehensweise**: Implementieren Sie die kennwortlose oder MFA-Authentifizierung, schulen Sie Administratoren (bei Bedarf) in ihrer Verwendung, und fordern Sie Administratoren mit geschriebenen Richtlinien zur Einhaltung auf. Dies kann durch eine oder mehrere der folgenden Technologien erreicht werden:

- [Kennwortlos (Windows Hello)](/windows/security/identity-protection/hello-for-business/hello-identity-verification)
- [Kennwortlos (Authenticator-App)](/azure/active-directory/authentication/howto-authentication-phone-sign-in)
- [Azure Multifactor Authentication](/azure/active-directory/authentication/howto-mfa-userstates)
- Drittanbieter-MFA-Lösung

> [!Note]
> Da die MFA auf SMS-Basis nun mit relativ kleinem Aufwand von Angreifern umgangen werden kann, konzentrieren Sie sich auf kennwortlose und stärkere MFA.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [ID-4: Verwenden stärkerer Authentifizierungssteuerungen für den gesamten Azure Active Directory-basierten Zugriff](/azure/security/benchmarks/security-controls-v2-identity-management#id-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access).

## <a name="7-technology-integrate-native-firewall-and-network-security"></a>7. Technologie: Integrieren von nativer Firewall und Netzwerksicherheit

*Vereinfachen Sie den Schutz von Systemen und Daten vor Netzwerkangriffen.*

**Was**: Vereinfachen Sie Ihre Netzwerksicherheitsstrategie und -wartung, indem Sie Azure Firewall, Azure Web App Firewall (WAF) und Entschärfung verteilter Denial-of-Service-Angriffe (Distributed Denial of Service, DDoS) in Ihren Ansatz zur Netzwerksicherheit integrieren.

**Grund**: Die Vereinfachung ist wichtig für die Sicherheit, da dadurch die Wahrscheinlichkeit des Auftretens von Risiken durch Verwirrung, Fehlkonfigurationen und andere menschliche Fehler reduziert wird. Weitere Informationen finden Sie in [Prinzipien für den Sicherheitsentwurf](/azure/architecture/framework/security/security-principles) unter „Fördern der Einfachheit“.

Firewalls und WAFs sind wichtige grundlegende Sicherheitssteuerungen zum Schutz von Anwendungen vor schädlichem Datenverkehr, aber deren Einrichtung und Wartung können komplex sein und in beträchtlichem Maße Zeit und Aufmerksamkeit des Sicherheitsteams beanspruchen (ähnlich dem Hinzufügen angepasster Zusatzteile zu einem Auto). Die nativen Azure-Funktionen können Implementierung und Betrieb von Firewalls, Web Application Firewalls, Entschärfung verteilter Denial-of-Service-Angriffe (DDoS) und mehr vereinfachen.

Auf diese Weise kann Ihr Team Zeit finden, sich mit höherwertigen Sicherheitsaufgaben wie dem Auswerten der Sicherheit von Azure-Diensten, Automatisieren von Sicherheitsvorgängen und Integrieren der Sicherheit in Anwendungen und IT-Lösungen befassen.

**Wer**:

- *Förderung*: Dieses Update der Netzwerksicherheitsstrategie wird in der Regel von den Führungskräften im Sicherheitsbereich und/oder IT-Führungskräften gefördert.
- *Ausführung*: Die Integration dieser Komponenten in Ihre Cloudnetzwerk-Sicherheitsstrategie ist eine gemeinsame Arbeit, die die Folgenden einbezieht:  
  - **[Sicherheitsarchitektur](../organize/cloud-security-architecture.md)** : Richten Sie die Cloudnetzwerk-Sicherheitsarchitektur mit Cloudnetzwerk- und Cloudnetzwerksicherheits-Leads ein.
  - **Cloudnetzwerkleads** ([Zentrale IT-Abteilung](../organize/central-it.md)) + **Cloudnetzwerksicherheits-Leads** ([Infrastruktursicherheits-Team](../organize/cloud-security-infrastructure-endpoint.md))
    - Einrichten der Cloudnetzwerksicherheits-Architektur mit Sicherheitsarchitekten
    - Konfigurieren von Firewall-, NSG- und WAF-Funktionen und Arbeiten an WAF-Regeln mit Anwendungsarchitekten
  - **Anwendungsarchitekten**: Arbeiten mit der Netzwerksicherheit zum Erstellen und Verfeinern von WAF-Regelsätzen und DDoS-Konfigurationen, um die Anwendung ohne Unterbrechung der Verfügbarkeit zu schützen.

**Vorgehensweise**: Organisationen, die ihren Betrieb vereinfachen möchten, haben zwei Möglichkeiten:

- **Erweitern vorhandener Funktionen und Architekturen**: Viele Organisationen entscheiden sich häufig dafür, die Verwendung vorhandener Firewallfunktionen zu erweitern, sodass sie vorhandene Investitionen in Fertigkeiten und Prozessintegration nutzen können, insbesondere am Anfang der Cloudeinführung.
- **Integrieren nativer Sicherheitssteuerungen**: Immer mehr Organisationen beginnen mit der Verwendung nativer Steuerelemente, um die Komplexität der Integration von Drittanbieterfunktionen zu vermeiden. Diese Organisationen sind in der Regel bestrebt, das Risiko einer Fehlkonfiguration von Lastenausgleich, benutzerdefinierten Routen, Firewall/WAF selbst und Verzögerungen bei der Übergabe zwischen verschiedenen technischen Teams zu vermeiden.
 Diese Option ist besonders für Organisationen überzeugend, die Infrastruktur als Codeansätze integrieren, da sie die integrierten Funktionen leichter automatisieren und instrumentieren können als Funktionen von Drittanbietern.

Dokumentation zu den nativen Netzwerksicherheitsfunktionen von Azure finden Sie unter:

- [Azure Firewall](/azure/firewall/overview)
- [Azure Web Application Firewall (WAF)](/azure/web-application-firewall/)
- [Azure DDoS Protection](/azure/virtual-network/ddos-protection-overview)

[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?page=1&search=firewall) umfasst zahlreiche Firewalldrittanbieter.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [NS-4: Schützen von Anwendungen und Diensten vor externen Netzwerkangriffen](/azure/security/benchmarks/security-controls-v2-network-security#ns-4-protect-applications-and-services-from-external-network-attacks).

## <a name="8-technology-integrate-native-threat-detection"></a>8. Technologie: Integrieren der nativen Bedrohungserkennung

*Vereinfachen Sie die Erkennung von Angriffen auf Azure-Systeme und -Daten und die Antwort darauf.*

**Was**: Vereinfachen Sie die Strategie der Erkennung von Bedrohungen und der Antwort darauf, indem Sie native Bedrohungserkennungsfunktionen in Ihre Sicherheitsvorgänge und SIEM integrieren.

**Grund**: Sicherheitsvorgänge sollen die Auswirkungen von aktiven Angreifern verringern, die Zugriff auf die Umgebung erhalten, gemessen an der durchschnittlichen Zeit zur Bestätigung (MTTA) und Behebung (MTTR) von Vorfällen. Dies erfordert sowohl Genauigkeit als auch Geschwindigkeit in allen Elementen der Antwort auf Vorfälle, sodass die Qualität der Tools und die Effizienz der Prozessausführung wichtig sind.

Es ist schwierig, hohe Bedrohungen mithilfe vorhandener Tools und Ansätze zu erkennen, die für die lokale Bedrohungserkennung entwickelt wurden. Dies liegt an Unterschieden in der Cloudtechnologie und ihrem schnellen Änderungstempo. Nativ integrierte Erkennungen bieten von den Cloudanbietern verwaltete Branchenlösungen, die mit aktuellen Bedrohungen und Cloudplattformänderungen Schritt halten können.

Mit diesen nativen Lösungen können sich Teams für Sicherheitsvorgänge auch auf die Untersuchung und Behebung von Vorfällen konzentrieren, anstatt Zeit damit zu verschwenden, zu versuchen, Warnungen aus unbekannten Protokolldaten zu erstellen, Tools zu integrieren und Wartungsaufgaben durchzuführen.

**Wer**: Dies wird in der Regel durch das Team für [Sicherheitsvorgänge](../organize/cloud-security-operations-center.md) gesteuert.

- *Förderung*: Dies wird in der Regel vom Direktor für Sicherheitsvorgänge (oder einer entsprechenden Person) gefördert.
- *Ausführung*: Die Integration der nativen Bedrohungserkennung ist eine gemeinsame Arbeit, die die Folgenden einbezieht:
  - **[Sicherheitsvorgänge](../organize/cloud-security-operations-center.md)** : Integrieren Sie Warnungen in SIEM- und Vorfalluntersuchungsprozesse, schulen Sie Analysten in Cloudwarnungen und deren Bedeutung und in der Verwendung der nativen Cloudtools.
  - **[Vorbereitung auf Vorfälle](../organize/cloud-security-incident-preparation.md)** : Integrieren Sie Cloudvorfälle in praktische Übungen, und stellen Sie sicher, dass praktische Übungen durchgeführt werden, um die Teambereitschaft zu fördern.
  - **[Threat Intelligence](../organize/cloud-security-threat-intelligence.md)** : Erforschen und integrieren Sie Informationen zu Cloudangriffen, um Teams mit Kontext und Intelligenz zu informieren.
  - **[Sicherheitsarchitektur](../organize/cloud-security-architecture.md)** : Integrieren Sie native Tools in die Dokumentation zur Sicherheitsarchitektur.
  - **[Richtlinien und Standards](../organize/cloud-security-policy-standards.md)** : Legen Sie Standards und Richtlinien für die Aktivierung nativer Tools in der gesamten Organisation fest. Überwachen Sie die Einhaltung.
  - **[Infrastruktur und Endpunkt](../organize/cloud-security-infrastructure-endpoint.md)**  /  **[Zentrale IT-Abteilung](../organize/central-it.md)** : Konfigurieren und aktivieren Sie Erkennungen und integrieren Sie sie als Codelösungen in Automatisierung und Infrastruktur.

**Vorgehensweise**: Aktivieren Sie die [Bedrohungserkennung in Azure Security Center](/azure/security-center/threat-protection) für alle Ressourcen, die Sie verwenden, und lassen Sie die einzelnen Teams diese wie oben beschrieben in ihre Prozesse integrieren.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [LT-1: Aktivieren der Bedrohungserkennung für Azure-Ressourcen](/azure/security/benchmarks/security-controls-v2-logging-threat-detection#lt-1-enable-threat-detection-for-azure-resources).

## <a name="9-architecture-standardize-on-a-single-directory-and-identity"></a>9. Architektur: Standardisieren eines einzelnen Verzeichnisses und einer einzelnen Identität

*Niemand möchte mit mehreren Identitäten und Verzeichnissen umgehen.*

**Was**: Standardisieren Sie ein einzelnes Azure AD-Verzeichnis und eine einzelne Identität für jede Anwendung und jeden Benutzer in Azure (für alle Unternehmensidentitätsfunktionen).

> [!Note]
>Diese bewährte Vorgehensweise bezieht sich speziell auf Unternehmensressourcen. Verwenden Sie für Partnerkonten [Azure AD B2B](/azure/active-directory/external-identities/what-is-b2b), damit Sie keine Konten in Ihrem Verzeichnis erstellen und verwalten müssen. Verwenden Sie [Azure AD B2C](/azure/active-directory-b2c/), um Kunden-/Bürgerkonten zu verwalten.

**Grund**: Mehrere Konten und Identitätsverzeichnisse sorgen für unnötige Friktionen und Verwirrung in täglichen Workflows für Produktivitätsbenutzer, Entwickler, IT- und Identitätsadministratoren, Sicherheitsanalysten und andere Rollen.

Das Verwalten mehrerer Konten und Verzeichnisse schafft auch einen Anreiz für schlechte Sicherheitsverfahren, wie z. B. die erneute Verwendung desselben Kennworts für verschiedene Konten, und erhöht die Wahrscheinlichkeit veralteter/verlassener Konten, auf die Angreifer abzielen können.

Obwohl es manchmal einfacher erscheint, schnell ein benutzerdefiniertes Verzeichnis (basierend auf LDAP usw.) für eine bestimmte Anwendung oder Arbeitsauslastung zu erstellen, fallen dadurch viel mehr Integrations- und Wartungsaufgaben für Einrichtung und Verwaltung an. Dies ähnelt in vielerlei Hinsicht der Entscheidung, einen zusätzlichen Azure-Mandanten einzurichten oder eine zusätzliche lokale Active Directory-Gesamtstruktur, statt die im Unternehmen vorhandene zu verwenden. Weitere Informationen finden Sie auch in [Prinzipien für den Sicherheitsentwurf](/azure/architecture/framework/security/security-principles) unter „Fördern der Einfachheit“.

**Wer**: Dies ist häufig ein teamübergreifender Aufwand, der durch [Sicherheitsarchitektur](../organize/cloud-security-architecture.md)- oder [Identitäts- und Schlüsselverwaltungs](../organize/cloud-security-identity-keys.md)-Teams gesteuert wird.

- *Förderung*: Dies wird in der Regel durch [Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md) und [Sicherheitsarchitektur](../organize/cloud-security-architecture.md) gefördert (obwohl einige Organisationen möglicherweise eine Förderung durch CISO oder CIO benötigen).
- *Ausführung*: Dies ist eine gemeinsame Arbeit, die die Folgenden einbezieht:
  -  **[Sicherheitsarchitektur](../organize/cloud-security-architecture.md)** : Wird in Dokumente und Diagramme zu Sicherheit und IT-Architektur integriert
  - **[Richtlinien und Standards](../organize/cloud-security-policy-standards.md)** : Dokumentieren der Richtlinie und Überwachung auf Einhaltung
  - **[Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md)** oder **[Zentrale IT-Abteilung](../organize/central-it.md)** , um die Richtlinie durch Aktivieren von Funktionen und Unterstützen von Entwicklern mit Konten, Schulungen usw. zu implementieren.
  - **Anwendungsentwickler** und/oder **[Zentrale IT-Abteilung](../organize/central-it.md)** : Verwenden von Identitäten in Anwendungen und Azure-Dienstkonfigurationen (Zuständigkeiten variieren basierend auf der Stufe der DevOps-Einführung)

**Vorgehensweise**: Verfolgen Sie einen pragmatischen Ansatz, der mit den neuen „Greenfield“-Funktionen beginnt (heute wachsend), und bereinigen Sie dann Herausforderungen mit dem „Brownfield“ vorhandener Anwendungen und Dienste als Folgeaufgabe:

- **Greenfield**: Richten Sie eine klare Richtlinie ein, dass alle Unternehmensidentitäten in Zukunft ein einzelnes Azure AD-Verzeichnis mit einem einzelnen Konto für jeden Benutzer verwenden sollen, und implementieren Sie sie.

- **Brownfield**: Viele Organisationen verfügen häufig über mehrere veraltete Verzeichnisse und Identitätssysteme. Befassen Sie sich mit ihnen, wenn die Kosten für die laufende Verwaltungsfriktion die Investition in ihre Bereinigung überschreiten. Identitätsverwaltungs- und Synchronisierungslösungen können zwar einige dieser Probleme minimieren, aber ihnen fehlt eine tiefgreifende Integration von Sicherheits- und Produktivitätsfeatures, die Benutzern, Administratoren und Entwicklern eine nahtlose Benutzererfahrung ermöglichen.

Die ideale Zeit zum Konsolidieren Ihrer Identitätsverwendung ist wie folgt während der Anwendungsentwicklung:

- Modernisieren von Anwendungen für die Cloud
- Aktualisieren von Cloudanwendungen mit DevOps-Prozessen

Es gibt zwar gute Gründe für ein separates Verzeichnis im Fall extrem unabhängiger Geschäftseinheiten oder gesetzlicher Anforderungen, aber in allen anderen Fällen sollten mehrere Verzeichnisse vermieden werden.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [ID-1: Standardisieren von Azure Active Directory als zentrales Identitäts- und Authentifizierungssystem](/azure/security/benchmarks/security-controls-v2-identity-management#id-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system).

> [!IMPORTANT]
> Die einzige Ausnahme von der Einzelkontenregel besteht darin, dass privilegierte Benutzer (einschließlich IT-Administratoren und Sicherheitsanalysten) über separate Konten für Standardbenutzeraufgaben und administrative Aufgaben verfügen sollten.
>
> Weitere Informationen finden Sie unter Azure-Sicherheitsvergleichstest [Privilegierter Zugriff](/azure/security/benchmarks/security-controls-v2-privileged-access).

## <a name="10-architecture-use-identity-based-access-control-instead-of-keys"></a>10. Architektur: Verwenden der identitätsbasierten Zugriffssteuerung (anstelle von Schlüsseln)

**Was**: Verwenden Sie nach Möglichkeit Azure AD-Identitäten anstelle der schlüsselbasierten Authentifizierung (Azure-Dienste, Anwendungen, APIs usw.).

**Grund**: Die schlüsselbasierte Authentifizierung kann für die Authentifizierung bei Clouddiensten und APIs verwendet werden, erfordert jedoch eine sichere Verwaltung von Schlüsseln. Dies ist eine Herausforderung für eine gute Leistung (insbesondere im großen Stil). Die sichere Schlüsselverwaltung ist schwierig für Personen wie Entwickler und Infrastrukturexperten, die keine Sicherheitsexperten sind, und sie führen sie oft nicht sicher durch, was häufig zu erheblichen Sicherheitsrisiken für die Organisation führt.

Die identitätsbasierte Authentifizierung überwindet viele dieser Herausforderungen mit ausgereiften Funktionen für Geheimnisrotation, Lebenszyklusverwaltung, administrative Delegierung und vieles mehr.

**Wer**: Dies ist häufig ein teamübergreifender Aufwand, der durch [Sicherheitsarchitektur](../organize/cloud-security-architecture.md)- oder [Identitäts- und Schlüsselverwaltungs](../organize/cloud-security-identity-keys.md)-Teams gesteuert wird.

- *Förderung*: Dies wird in der Regel durch [Sicherheitsarchitektur](../organize/cloud-security-architecture.md) oder [Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md) gefördert (obwohl einige Organisationen möglicherweise eine Förderung durch CISO oder CIO benötigen).
- *Ausführung*: Dies ist eine gemeinsame Arbeit, die die Folgenden einbezieht:
  - **[Sicherheitsarchitektur](../organize/cloud-security-architecture.md)** : Wird in Dokumente und Diagramme zu Sicherheit und IT-Architektur integriert
  - **[Richtlinien und Standards](../organize/cloud-security-policy-standards.md)** : Dokumentieren der Richtlinie und Überwachung auf Einhaltung
  - **[Identitäts- und Schlüsselverwaltung](../organize/cloud-security-identity-keys.md)** oder **[Zentrale IT-Abteilung](../organize/central-it.md)** , um die Richtlinie durch Aktivieren von Funktionen und Unterstützen von Entwicklern mit Konten, Schulungen usw. zu implementieren.
  - **App-Entwickler** und/oder **[Zentrale IT-Abteilung](../organize/central-it.md)** : Verwenden von Identitäten in Anwendungen und Azure-Dienstkonfigurationen (Zuständigkeiten variieren basierend auf der Stufe der DevOps-Einführung)

**Vorgehensweise**: Die Verwendung der identitätsbasierten Authentifizierung in der Organisation als Präferenz und Gewohnheit zu etablieren, setzt die Befolgung eines Prozesses und Aktivierung einer Technologie voraus.

**Im Prozess wird wie folgt vorgegangen:**

1. **Richten Sie Richtlinien** und Standards ein, die die standardmäßige identitätsbasierte Authentifizierung und akzeptable Ausnahmen eindeutig beschreiben.
2.  **Schulen** Sie Entwickler- und Infrastrukturteams in den Gründen zur Verwendung des neuen Ansatzes und darin, was und wie sie es tun müssen.
3.  **Implementieren** Sie Änderungen auf pragmatische Weise – beginnend mit neuen „Greenfield“-Funktionen, die jetzt und in Zukunft eingeführt werden (neue Azure-Dienste, neue Anwendungen), und führen Sie dann eine Bereinigung vorhandener „Brownfield“-Konfigurationen durch.
4.  **Überwachen** Sie die Einhaltung, und führen Sie mit Entwickler- und Infrastrukturteams Korrekturen durch.

**Die Technologien:** Verwenden Sie für Konten, die nicht für Personen, sondern z. B. für Dienste oder Automatisierung bestimmt sind, [verwaltete Identitäten](/azure/active-directory/managed-identities-azure-resources/overview). Verwaltete Identitäten in Azure können sich bei Azure-Diensten und -Ressourcen authentifizieren, die die Azure AD-Authentifizierung unterstützen. Die Authentifizierung wird durch vordefinierte Zugriffszuweisungsregeln aktiviert, sodass hart codierte Anmeldeinformationen im Quellcode oder in Konfigurationsdateien vermieden werden.

Für Dienste, die keine verwalteten Identitäten unterstützen, können Sie stattdessen mit Azure AD [Dienstprinzipale](/azure/active-directory/develop/app-objects-and-service-principals) mit eingeschränkten Berechtigungen auf Ressourcenebene erstellen. Sie sollten Dienstprinzipale mit Zertifikatanmeldeinformationen und Fallback auf geheime Clientschlüssel konfigurieren. In beiden Fällen kann [Azure Key Vault](/azure/key-vault/general/overview) in Verbindung mit verwalteten Azure-Identitäten verwendet werden, damit die Laufzeitumgebung (z. B. eine Azure-Funktion) die Anmeldeinformationen aus dem Schlüsseltresor abrufen kann.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [ID-2: Sicheres und automatisches Verwalten von Anwendungsidentitäten](/azure/security/benchmarks/security-controls-v2-identity-management#id-2-manage-application-identities-securely-and-automatically).

## <a name="11-architecture-establish-a-single-unified-security-strategy"></a>11. Architektur: Einrichten einer einzelnen vereinheitlichten Sicherheitsstrategie 

*Alle müssen in der gleichen Richtung rudern, damit das Boot vorwärts fährt.*

**Was**: Stellen Sie sicher, dass sich alle Teams an einer einzigen Strategie orientieren, die Unternehmenssysteme und -daten gleichermaßen aktiviert und sichert.

**Grund**: Wenn Teams isoliert arbeiten, ohne sich an einer gemeinsamen Strategie zu orientieren, könnten sie unabsichtlich gegeneinander arbeiten, sodass vermeidbare Friktionen das Erreichen ihrer Ziele bremsen.

Ein Beispiel dafür, das sich in vielen Organisationen konsistent abgespielt hat, ist die Segmentierung von Ressourcen:

- Das *Netzwerksicherheitsteam* entwickelt eine Strategie zum Segmentieren eines „flachen Netzwerks“, um die Sicherheit zu erhöhen (häufig basierend auf physischen Standorten, zugewiesenen IP-Adressen/-Adressbereichen oder Ähnlichem).
- Das *Identitätsteam* entwickelt basierend auf seinem Wissen über die Organisation eine separate Strategie für Gruppen und Active Directory-Organisationseinheiten (OEs).
- *Anwendungsteams* finden die Arbeit mit diesen Systemen häufig schwierig, da sie mit begrenztem Input zu und eingeschränktem Verständnis von Geschäftsvorgängen, Zielen und Risiken entwickelt wurden.

In Organisationen, in denen dies geschieht, erleben Teams häufig Konflikte wegen Firewallausnahmen, was sich sowohl auf die Sicherheit (Ausnahmen werden normalerweise genehmigt) als auch die Produktivität (die Bereitstellung wird für wichtige Anwendungsfunktionen verlangsamt) negativ auswirkt.

Wenngleich die Sicherheit durch Erzwingen kritischer Überlegungen eine heilsame Friktion bewirken kann, schafft dieser Konflikt nur eine kontraproduktive Friktion, die das Erreichen von Zielen erschwert. Weitere Informationen finden Sie unter *Das richtige Niveau der Sicherheitsfriktion* unter [Definieren einer Sicherheitsstrategie](../strategy/define-security-strategy.md#modernize-your-security-strategy).

**Wer**:
- *Förderung*: Die in der Regel von CIO, CISO und CTO gemeinsam (häufig mit Unterstützung einiger allgemeiner Elemente durch die Unternehmensführung) geförderte und von Vertretern der einzelnen Teams verfochtene vereinheitlichte Strategie.
- *Ausführung*: Die Sicherheitsstrategie muss von allen Benutzern implementiert werden. Daher sollte sie Input von allen Teams integrieren, um Verantwortung, Buy-In und Erfolgswahrscheinlichkeit zu erhöhen.
  - **[Sicherheitsarchitektur](../organize/cloud-security-architecture.md)** : Bestimmt den Aufwand für das Erstellen der Sicherheitsstrategie und daraus resultierender Architektur, das aktive Sammeln von Feedback von Teams und das Dokumentieren in Präsentationen, Dokumenten und Diagrammen für die verschiedenen Zielgruppen.
   - **[Richtlinien und Standards](../organize/cloud-security-policy-standards.md)** : Erfasst die entsprechenden Elemente in Standards und Richtlinien und überwacht dann die Einhaltung.
  - **Alle technischen IT- und Sicherheitsteams**: Stellen Inputanforderungen auf, richten daran die Unternehmensstrategie aus und implementieren sie.
   - **Anwendungsbesitzer und -entwickler**: Lesen und verstehen die Strategiedokumentation, die für sie relevant ist (idealerweise die auf ihre Rolle zugeschnittenen Richtlinien).

**Vorgehensweise**:

Erstellen und implementieren einer Sicherheitsstrategie für die Cloud, die den Input und die aktive Teilnahme aller Teams einschließt. Das Format der Prozessdokumentation variiert zwar, sollte jedoch immer Folgendes umfassen:

- **Aktiver Input von Teams**: Strategien scheitern in der Regel, wenn Personen in der Organisation sie nicht akzeptieren. Im Idealfall versammeln Sie alle Teams im gleichen Raum, damit sie die Strategie gemeinsam erarbeiten. In den Workshops, die wir mit Kunden durchführen, stellen wir häufig fest, dass Organisationen faktisch in Silos gearbeitet haben und Personen sich in diesen Meetings häufig überhaupt zum ersten Mal trafen. Wir stellen auch fest, dass die Einbeziehung eine Voraussetzung ist. Wenn einige Teams nicht eingeladen werden, muss dieses Meeting in der Regel wiederholt werden, bis alle Beteiligten teilnehmen (oder das Projekt geht nicht voran).
- **Klar dokumentiert und kommuniziert**: Alle Teams sollten mit der Sicherheitsstrategie (im Idealfall eine Sicherheitskomponente der gesamten Technologiestrategie) vertraut sein, die Gründe für die Integration der Sicherheit kennen und wissen, worauf es bei der Sicherheit ankommt und wie erfolgreiche Sicherheit aussieht. Sie sollte bestimmte Anleitungen für Anwendungs- und Entwicklungsteams enthalten, damit sie eine klar priorisierte Anleitung erhalten können, ohne dass sie Zeit für das Lesen nicht relevanter Teile der Anleitung vergeuden müssen.
- **Stabil, aber flexibel**: Strategien sollten relativ konsistent und stabil bleiben, aber die Architekturen und die Dokumentation müssen möglicherweise geändert werden, um Klarheit zu schaffen und die dynamische Natur der Cloud zu berücksichtigen. Beispielsweise würde das Herausfiltern von schädlichem externem Datenverkehr auch dann ein strategischer Imperativ bleiben, wenn Sie von der Verwendung einer Drittanbieterfirewall der nächsten Generation zur Azure-Firewall wechseln und Diagramme/Anleitungen für die Vorgehensweise anpassen würden.
- **Beginnen Sie mit Segmentierung**: Im Rahmen der Einführung in die Cloud befassen sich Ihre Teams mit vielen großen und kleinen Strategiethemen, aber Sie müssen irgendwo anfangen. Sie sollten die Sicherheitsstrategie mit der Segmentierung von Unternehmensressourcen beginnen, da es sich hierbei um eine grundlegende Entscheidung handelt, die sich zu einem späteren Zeitpunkt nur schwer ändern ließe und sowohl geschäftlichen Input als auch viele technische Teams erfordert.

Microsoft hat eine Anleitung zum Anwenden einer Segmentierungsstrategie auf Azure in [diesem Video](/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) und Dokumente zur [Unternehmenssegmentierung](/security/compass/governance#enterprise-segmentation-strategy) und zum [Ausrichten der Netzwerksicherheit daran](/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy) veröffentlicht.

Das Cloud Adoption Framework enthält Anleitungen, die Ihre Teams bei Folgendem unterstützen:

- **[Zusammenstellen eines Cloudstrategieteams](../get-started/team/cloud-strategy.md)** : Im Idealfall sollte die Sicherheit in eine vorhandene Cloudstrategie integriert werden.
- **[Erstellen oder Modernisieren einer Sicherheitsstrategie](../strategy/define-security-strategy.md)** : Um Geschäfts- und Sicherheitsziele in der aktuellen Ära von Clouddiensten und modernen Bedrohungen zu erfüllen.

Lesen Sie auch den Vergleichstest für die Azure-Sicherheit [Governance und Strategie](/azure/security/benchmarks/security-controls-v2-governance-strategy).