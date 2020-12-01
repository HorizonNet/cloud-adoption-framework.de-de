---
title: Organisation von Verwaltungsgruppen und Abonnements
description: Organisation von Verwaltungsgruppen und Abonnements.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: think-tank
ms.openlocfilehash: 06ff80acc1da04697fbf42ef0e50ac9768a79e94
ms.sourcegitcommit: d957bfc1fa8dc81168ce9c7d801a8dca6254c6eb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/23/2020
ms.locfileid: "95447216"
---
# <a name="management-group-and-subscription-organization"></a>Organisation von Verwaltungsgruppen und Abonnements

![Diagramm zur Verwaltungsgruppenhierarchie](./media/sub-org.png)

_Abbildung 1: Verwaltungsgruppenhierarchie._

## <a name="define-a-management-group-hierarchy"></a>Definieren einer Verwaltungsgruppenhierarchie

Verwaltungsgruppenstrukturen innerhalb eines Azure AD-Mandanten (Azure Active Directory) unterstützen Organisationszuordnung und sind sorgfältig zu durchdenken, wenn eine Organisation die Azure-Einführung in großem Umfang plant.

**Überlegungen zum Entwurf:**

- Mit Verwaltungsgruppen können Richtlinien- und Initiativenzuweisungen über Azure Policy aggregiert werden.
- Eine Verwaltungsgruppenstruktur kann bis zu [sechs Ebenen](/azure/governance/management-groups/overview#hierarchy-of-management-groups-and-subscriptions) unterstützen. Diese Einschränkung gilt nicht für die Mandantenstammebene oder die Abonnementebene.
- Jeder Prinzipal (Benutzer, Dienstprinzipal) innerhalb eines Azure AD-Mandanten kann neue Verwaltungsgruppen erstellen, da die RBAC-Autorisierung für Verwaltungsgruppenvorgänge nicht standardmäßig aktiviert ist.
- Alle neuen Abonnements werden standardmäßig unter der Stammverwaltungsgruppe platziert.

**Entwurfsempfehlungen:**

- Halten Sie die Verwaltungsgruppenhierarchie hinreichend flach; sie sollte im Idealfall nicht mehr als drei bis vier Ebenen umfassen. Diese Einschränkung reduziert den Mehraufwand und die Komplexität der Verwaltung.
- Vermeiden Sie das Duplizieren ihrer Organisationsstruktur in einer tief geschachtelten Verwaltungsgruppenhierarchie. Verwaltungsgruppen sollten für die Richtlinienzuweisung sowie für Abrechnungszwecke verwendet werden. Für diesen Ansatz müssen Verwaltungsgruppen für ihren vorgesehenen Zweck in einer Architektur auf Unternehmensebene verwendet werden: Zum Bereitstellen von Azure-Richtlinien für Workloads, welche dieselbe Sicherheit und Compliance auf derselben Verwaltungsgruppenebene erfordern.
- Erstellen Sie Verwaltungsgruppen unter der Verwaltungsgruppe auf der Stammebene, um die Typen von Workloads (Archetyp) darzustellen, die Sie hosten sowie diejenigen, die auf den jeweiligen Sicherheits-, Compliance-, Konnektivitäts- und Funktionsanforderungen basieren. Mithilfe dieser Gruppierungsstruktur können Sie Azure-Richtlinien auf Verwaltungsgruppenebene für alle Workloads anwenden, die die gleichen Einstellungen für Sicherheit, Compliance, Konnektivität und Features benötigen.
- Verwenden Sie Ressourcentags, die über Azure Policy erzwungen oder angefügt werden können, um die Verwaltungsgruppenhierarchie abzufragen und horizontal zu durchsuchen. Anschließend können Sie Ressourcen für die Suche gruppieren, ohne dass Sie eine komplexe Verwaltungsgruppenhierarchie verwenden müssen.
- Erstellen Sie eine Sandbox-Verwaltungsgruppe der obersten Ebene, um Benutzern das sofortige Experimentieren mit Azure zu gestatten. Benutzer können dann mit Ressourcen experimentieren, die möglicherweise noch nicht in Produktionsumgebungen zugelassen werden. Die Sandbox bietet Isolation von Ihren Entwicklungs-, Test- und Produktionsumgebungen.
  - Weitere Anleitungen zur Sandbox-Verwaltungsgruppe der obersten Ebene finden Sie in den [Richtlinien für die Implementierung](./implementation-guidelines.md#sandbox-governance-guidance).
- Verwenden Sie einen dedizierten Dienstprinzipalnamen (SPN), um Verwaltungsvorgänge für Verwaltungsgruppen, Verwaltungsvorgänge für Abonnements und die Rollenzuweisung auszuführen. Mithilfe eines SPNs wird die Anzahl der Benutzer mit erhöhten Berechtigungen reduziert und die Richtlinien der geringstmöglichen Berechtigungen werden eingehalten.
- Weisen Sie die Rolle `User Access Administrator` der rollenbasierten Zugriffssteuerung von Azure der Stammverwaltungsgruppe (`/`) zu, um dem SPN den zuvor genannten Zugriff auf der Stammebene zu gewähren. Nachdem dem SPN Berechtigungen erteilt wurden, kann die Rolle `User Access Administrator` sicher entfernt werden. Dadurch ist nur der SPN Teil der Rolle `User Access Administrator`.
- Weisen Sie die Berechtigung `Contributor` dem zuvor erwähnten SPN im Bereich der Stammverwaltungsgruppe (`/`) zu, die Vorgänge auf der Mandantenebene zulässt. Mit dieser Berechtigungsstufe wird sichergestellt, dass der SPN zum Bereitstellen und Verwalten von Ressourcen für ein beliebiges Abonnement in Ihrer Organisation verwendet werden kann.
- Erstellen Sie eine Verwaltungsgruppe `Platform` unter der Stammverwaltungsgruppe, um die Zuweisung allgemeiner Plattformrichtlinien und der rollenbasierten Zugriffssteuerung zu unterstützen. Mit dieser Gruppierungsstruktur wird sichergestellt, dass verschiedene Richtlinien auf die Abonnements angewendet werden können, die für Ihr Azure-Fundament verwendet werden. Außerdem wird sichergestellt, dass die Abrechnung für allgemeine Ressourcen in einer Reihe grundlegender Abonnements zentralisiert wird.
- Beschränken Sie die Anzahl der Azure Policy-Zuweisungen, die im Bereich der Stammverwaltungsgruppe (`/`) vorgenommen werden. Durch diese Einschränkung wird das Debuggen geerbter Richtlinien in Verwaltungsgruppen auf niedrigeren Ebenen minimiert.
- Stellen Sie sicher, dass nur berechtigte Benutzer Verwaltungsgruppen im Mandanten betreiben können, indem Sie die RBAC-Autorisierung in den Einstellungen der Verwaltungsgruppenhierarchie aktivieren.
- Konfigurieren Sie eine standardmäßige, dedizierte Verwaltungsgruppe für neue Abonnements, um sicherzustellen, dass keine Abonnements unter die Stammverwaltungsgruppe platziert werden.

## <a name="subscription-organization-and-governance"></a>Organisation und Governance von Abonnements

Abonnements sind eine Einheit für die Verwaltung, Abrechnung und Skalierung in Azure. Sie spielen eine wichtige Rolle bei der Entwicklung für Azure im großen Stil. Dieser Abschnitt unterstützt Sie beim Erfassen von Abonnementanforderungen und Entwerfen von Zielabonnements anhand wichtiger Faktoren. Zu diesen Faktoren gehören die Art von Umgebung, das Besitzer- und Governancemodell, die Organisationsstruktur sowie Anwendungsportfolios.

**Überlegungen zum Entwurf:**

- Abonnements fungieren beim Zuweisen von Azure-Richtlinien als Grenzen. Sichere Workloads wie Payment Card Industry-Workloads (PCI) erfordern beispielsweise in der Regel zusätzliche Richtlinien, um Compliance herzustellen. Anstatt eine Verwaltungsgruppe zum Gruppieren von Workloads zu verwenden, die PCI-Compliance erfordern, können Sie die gleiche Abgrenzung auch mit einem Abonnement erzielen. Auf diese Weise wird sichergestellt, dass bei einer kleinen Anzahl von Abonnements nicht zu viele Verwaltungsgruppen vorhanden sind.
- Abonnements dienen als Skalierungseinheit, sodass Komponenten-Workloads innerhalb der [Abonnementgrenzen](/azure/azure-subscription-service-limits) der Plattform skaliert werden können. Überdenken Sie während der Workload-Entwurfssitzungen unbedingt Ressourcengrenzwerte für Abonnements.
- Abonnements stellen eine Verwaltungsgrenze für Governance und Isolation bereit, wodurch eine klare Trennung von Zuständigkeiten geschaffen wird.
- Es gibt einen manuellen Prozess (zukünftige Automatisierung ist geplant), mit dem ein Azure AD-Mandant so eingeschränkt werden kann, dass er nur Enterprise Agreement-Registrierungsabonnements (EA) verwendet. Dieser Prozess verhindert die Erstellung von Microsoft Developer Network-Abonnements im Rahmen der Stammverwaltungsgruppe.

**Entwurfsempfehlungen:**

- Behandeln Sie Abonnements als demokratisierte Verwaltungseinheit, die sich an geschäftlichen Anforderungen und Prioritäten orientiert.
- Informieren Sie Abonnementbesitzer über ihre Rollen und Zuständigkeiten:
  - Führen Sie quartalsweise oder halbjährlich eine Zugriffsprüfung in Azure AD Privileged Identity Management aus, damit Berechtigungen bei Versetzungen der Benutzer innerhalb der Kundenorganisation nicht weiterverbreitet werden.
  - Beanspruchen Sie den vollständigen Besitz von Budgetausgaben und Ressourcenverwendung.
  - Gewährleisten Sie die Richtlinienkompatibilität, und beheben Sie ggf. Verstöße.
- Orientieren Sie sich beim Ermitteln von Anforderungen für neue Abonnements an folgenden Grundsätzen:
  - **Skalierungslimits:** Abonnements dienen als Skalierungseinheit, sodass Komponenten-Workloads innerhalb der Abonnementgrenzen der Plattform skaliert werden können. Beispielsweise sollten für große spezialisierte Workloads (z. B. High Performance Computing, IoT und SAP) besser separate Abonnements verwendet werden, um Limits zu vermeiden (z. B. ein Limit von 50 Azure Data Factory-Integrationen).
  - **Verwaltungsgrenze:** Abonnements bilden eine Verwaltungsgrenze für Governance und Isolation, wodurch eine klare Trennung von Zuständigkeiten geschaffen wird. Beispielsweise werden unterschiedliche Umgebungen wie Entwicklung, Test und Produktion im Hinblick auf die Verwaltung häufig voneinander isoliert.
  - **Richtliniengrenze:** Abonnements fungieren als Grenze für die Zuweisung von Azure-Richtlinien. Beispielsweise erfordern sichere Workloads, z. B. PCI-Workloads, in der Regel zusätzliche Richtlinien, um Compliance zu erzielen. Dieser zusätzliche Mehraufwand muss nicht ganzheitlich berücksichtigt werden, wenn ein separates Abonnement verwendet wird. Zudem können Entwicklungsumgebungen weniger strikte Richtlinienanforderungen als Produktionsumgebungen aufweisen.
  - **Ziel-Netzwerktopologie:** Virtuelle Netzwerke können nicht abonnementübergreifend freigegeben werden. Sie können jedoch eine Verbindung mit verschiedenen Technologien wie Peering virtueller Netzwerke oder Azure ExpressRoute herstellen. Berücksichtigen Sie, welche Workloads miteinander kommunizieren müssen, wenn Sie entscheiden, ob Sie ein neues Abonnement benötigen.
- Gruppieren Sie Abonnements in Verwaltungsgruppen in Einklang mit der Verwaltungsgruppenstruktur und den umfassenden Richtlinienanforderungen. Durch die Gruppierung wird sichergestellt, dass Abonnements mit denselben Richtlinien und RBAC-Zuweisungen diese von einer Verwaltungsgruppe erben können, wodurch doppelte Zuweisungen vermieden werden.
- Richten Sie ein dediziertes Verwaltungsabonnement in der Verwaltungsgruppe `Platform` zur Unterstützung globaler Verwaltungsfunktionen ein, z. B. Azure Monitor Log Analytics-Arbeitsbereiche und Azure Automation-Runbooks.
- Richten Sie bei Bedarf ein dediziertes Identitätsabonnement in der Verwaltungsgruppe `Platform` ein, um Windows Server Active Directory-Domänencontroller zu hosten.
- Richten Sie ein dediziertes Konnektivitätsabonnement in der Verwaltungsgruppe `Platform` ein, um einen Azure Virtual WAN-Hub, privates DNS (Domain Name System), ExpressRoute-Verbindung und andere Netzwerkressourcen zu hosten. Mit einem dedizierten Abonnement wird sichergestellt, dass alle grundlegenden Netzwerkressourcen zusammen abgerechnet und von anderen Workloads isoliert werden.
- Vermeiden Sie ein starres Abonnementmodell, und entscheiden Sie sich beim Gruppieren von Abonnements im gesamten Unternehmen stattdessen für eine Reihe flexibler Kriterien. Mithilfe dieser Flexibilität wird sichergestellt, dass Sie angesichts von Änderungen der Struktur und der Workloadkomposition Ihrer Organisation neue Abonnementgruppen erstellen können, anstatt festgelegte vorhandene Abonnements zu verwenden. Eine Größe eignet sich nicht für alle Abonnements. Was für eine Geschäftseinheit funktioniert, funktioniert womöglich nicht für eine andere. Einige Anwendungen können innerhalb des gleichen Zielzonenabonnements gleichzeitig vorhanden sein, während andere unter Umständen ein eigenes Abonnement erfordern.

## <a name="configure-subscription-quota-and-capacity"></a>Konfigurieren von Abonnementkontingent und -kapazität

Jede Azure-Region enthält eine endliche Anzahl von Ressourcen. Wenn Sie eine Azure-Einführung auf Unternehmensebene mit großen Ressourcenmengen erwägen, stellen Sie sicher, dass eine ausreichende Kapazität und genügend SKUs verfügbar sind und dass die erreichte Kapazität erkannt und überwacht werden kann.

**Überlegungen zum Entwurf:**

- Beachten Sie für jeden von Ihren Workloads benötigten Dienst die Grenzwerte und Kontingente innerhalb der Azure-Plattform.
- Prüfen Sie die Verfügbarkeit der erforderlichen SKUs in ausgewählten Azure-Regionen. So können neue Features beispielsweise nur in bestimmten Regionen verfügbar sein. Die Verfügbarkeit bestimmter SKUs für bestimmte Ressourcen (z. B. VMs) kann in verschiedenen Regionen variieren.
- Beachten Sie, dass Abonnementkontingente keine Kapazitätsgarantien sind und sich auf die jeweilige Region beziehen.

**Entwurfsempfehlungen:**

- Verwenden Sie Abonnements als Skalierungseinheiten, und skalieren Sie Ressourcen und Abonnements nach Bedarf auf. Ihre Workload kann dann bei Bedarf die erforderlichen Ressourcen zum horizontalen Hochskalieren verwenden, ohne Abonnementlimits in der Azure-Plattform zu erreichen.
- Verwenden Sie reservierte Instanzen, um reservierte Kapazität in den erforderlichen Regionen zu priorisieren. Ihre Workload verfügt dann über die erforderliche Kapazität, selbst wenn in einer spezifischen Region ein hoher Bedarf an dieser Ressource besteht.
- Richten Sie ein Dashboard mit benutzerdefinierten Ansichten zum Überwachen der Kapazitätsauslastung ein. Richten Sie Warnungen ein, wenn die Kapazitätsauslastung kritische Werte erreicht (z. B. 90 % CPU-Auslastung).
- Supportanfragen zum Erhöhen des Kontingents nehmen im Rahmen der Abonnementbereitstellung zu (z. B. insgesamt verfügbare VM-Kerne in einem Abonnement). Mit diesem Ansatz wird sichergestellt, dass Ihre Kontingentgrenzen festgelegt sind, bevor Ihre Workloads das Überschreiten der Standardgrenzen fordern.
- Stellen Sie sicher, dass die erforderlichen Dienste und Features innerhalb der ausgewählten Bereitstellungsregionen verfügbar sind.

## <a name="establish-cost-management"></a>Einrichten der Kostenverwaltung

Die Kostentransparenz für eine technische Umgebung ist eine entscheidende Verwaltungsaufgabe, mit der alle großen Organisationen konfrontiert sind. In diesem Abschnitt werden wichtige Aspekte im Zusammenhang mit der Kostentransparenz in großen Azure-Umgebungen erläutert.

**Überlegungen zum Entwurf:**

- Potenzieller Bedarf an Modellen der verbrauchsbasierten Kostenzuteilung in Bezug auf freigegebene PaaS-Ressourcen (Platform-as-a-Service), z. B. Azure App Service-Umgebung und Azure Kubernetes Service, die zum Erreichen einer höheren Dichte freigegeben werden müssen.
- Optimieren Sie die Kosten mithilfe eines Zeitplans zum Herunterfahren für nicht produktionsbezogene Workloads.
- Prüfen Sie die Empfehlungen zur Kostenoptimierung mithilfe von Azure Advisor.

**Entwurfsempfehlungen:**

- Verwenden Sie Azure Cost Management + Billing für die Kostenaggregation. Stellen Sie diese den Anwendungsbesitzern zur Verfügung.
- Verwenden Sie Azure-Ressourcentags zum Kategorisieren und Gruppieren von Kosten. Indem Sie Tags verwenden, können Sie einen Mechanismus der verbrauchsbasierten Kostenzuteilung für Workloads nutzen, die ein Abonnement gemeinsam nutzen, oder für eine bestimmte Workload, die sich über mehrere Abonnements erstreckt.
