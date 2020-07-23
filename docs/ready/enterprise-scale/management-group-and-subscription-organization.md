---
title: Organisation von Verwaltungsgruppen und Abonnements
description: Organisation von Verwaltungsgruppen und Abonnements.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6e317dc33372e32ed175c646426a52e2a93c939f
ms.sourcegitcommit: bcc73d194c6d00c16ae2e3c7fb2453ac7dbf2526
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86194917"
---
# <a name="management-group-and-subscription-organization"></a>Organisation von Verwaltungsgruppen und Abonnements

![Verwaltungsgruppenhierarchie](./media/sub-org.png)

_Abbildung 1: Verwaltungsgruppenhierarchie._

## <a name="define-a-management-group-hierarchy"></a>Definieren einer Verwaltungsgruppenhierarchie

Verwaltungsgruppenstrukturen innerhalb eines Azure AD-Mandanten (Azure Active Directory) unterstützen Organisationszuordnung und sind sorgfältig zu durchdenken, wenn eine Organisation die Azure-Einführung in großem Umfang plant.

**Überlegungen zum Entwurf:**

- Mit Verwaltungsgruppen können Richtlinien- und Initiativenzuweisungen über Azure Policy aggregiert werden.
- Eine Verwaltungsgruppenstruktur kann bis zu [sechs Ebenen](https://docs.microsoft.com/azure/governance/management-groups/overview#hierarchy-of-management-groups-and-subscriptions) unterstützen. Dieser Grenzwert schließt nicht die Stammebene oder die Abonnementebene ein.

**Entwurfsempfehlungen:**

- Halten Sie die Verwaltungsgruppenhierarchie hinreichend flach; sie sollte im Idealfall nicht mehr als drei bis vier Ebenen umfassen. Dadurch werden Verwaltungsaufwand und -komplexität verringert.

- Vermeiden Sie das Duplizieren ihrer Organisationsstruktur in einer tief geschachtelten Verwaltungsgruppenhierarchie. Verwaltungsgruppen sollten für die Richtlinienzuweisung sowie für Abrechnungszwecke verwendet werden. Dafür müssen Verwaltungsgruppen für ihren vorgesehenen Zweck in einer Architektur auf Unternehmensebene verwendet werden: Bereitstellen von Azure-Richtlinien für Workloads, welche dieselbe Sicherheit und Compliance auf derselben Verwaltungsgruppenebene erfordern.

- Erstellen Sie Verwaltungsgruppen unter der Verwaltungsgruppe auf der Stammebene, um die Typen von Workloads (Archetyp) darzustellen, die Sie hosten sowie diejenigen, die auf den jeweiligen Sicherheits-, Compliance-, Konnektivitäts- und Funktionsanforderungen basieren. Auf diese Weise können Sie einen Satz von Azure-Richtlinien auf der Verwaltungsgruppenebene für alle Workloads anwenden, die die gleichen Einstellungen für Sicherheit, Compliance, Konnektivität und Funktionen benötigen.

- Verwenden Sie Ressourcentags, die über Azure Policy erzwungen oder angefügt werden können, um die Verwaltungsgruppenhierarchie abzufragen und horizontal zu durchsuchen. Dies erleichtert das Gruppieren von Ressourcen für die Suche, ohne dass eine komplexe Verwaltungsgruppenhierarchie verwendet werden muss.

- Erstellen Sie eine Sandbox-Verwaltungsgruppe der obersten Ebene, um Benutzern das sofortige Experimentieren mit Azure zu gestatten. Dadurch können Benutzer mit Ressourcen experimentieren, die in Produktionsumgebungen möglicherweise nicht zugelassen sind; außerdem ist die Abgrenzung von Ihren Entwicklungs-, Test- und Produktionsumgebungen sichergestellt.

- Verwenden Sie einen dedizierten Dienstprinzipalnamen (SPN), um Verwaltungsvorgänge für Verwaltungsgruppen, Verwaltungsvorgänge für Abonnements und die Rollenzuweisung auszuführen. Dadurch wird entsprechend den Richtlinien der geringstmöglichen Zugriffsberechtigungen die Anzahl der Benutzer mit erhöhten Rechten reduziert.

- Weisen Sie die Azure RBAC-Rolle `User Access Administrator` im Bereich der Stammverwaltungsgruppe (`/`) zu, um dem SPN den obigen Zugriff auf der Stammebene zu gewähren. Nachdem dem SPN Berechtigungen erteilt wurden, kann die Rolle `User Access Administrator` sicher entfernt werden. Dadurch wird sichergestellt, dass nur der SPN Teil der Rolle `User Access Administrator` ist.

- Weisen Sie die Berechtigung `Contributor` dem oben erwähnten SPN im Bereich der Stammverwaltungsgruppe (`/`) zu, die Vorgänge auf der Mandantenebene zulässt. Dadurch wird sichergestellt, dass der SPN zum Bereitstellen und Verwalten von Ressourcen für ein beliebiges Abonnement in Ihrer Organisation verwendet werden kann.

- Erstellen Sie eine Verwaltungsgruppe `Platform` unter der Stammverwaltungsgruppe, um die Zuweisung allgemeiner Plattformrichtlinien und der rollenbasierten Zugriffssteuerung (RBAC) zu unterstützen. Dadurch wird sichergestellt, dass unterschiedliche Richtlinien auf die für Ihr Azure-Fundament verwendeten Abonnements angewendet werden können, und dass die Abrechnung für gemeinsame Ressourcen in einer Reihe von grundlegenden Abonnements zentralisiert wird.

- Beschränken Sie die Anzahl der Azure Policy-Zuweisungen, die im Bereich der Stammverwaltungsgruppe (`/`) vorgenommen werden. Dadurch wird das Debuggen geerbter Richtlinien in Verwaltungsgruppen auf niedrigeren Ebenen minimiert.

- Erstellen Sie keine Abonnements unter der Stammverwaltungsgruppe. Dadurch wird sichergestellt, dass Abonnements nicht nur den kleinen Satz von Azure-Richtlinien erben, die der Verwaltungsgruppe auf der Stammebene zugewiesen sind, wobei es sich nicht um einen vollständigen Satz handelt, der für eine Workload erforderlich ist.

## <a name="subscription-organization-and-governance"></a>Organisation und Governance von Abonnements

Abonnements sind eine Verwaltungs-, Abrechnungs- und Skalierungseinheit in Azure, die beim Entwerfen für eine umfassende Azure-Einführung eine wichtige Rolle spielt. Dieser Abschnitt unterstützt Sie beim Erfassen von Abonnementanforderungen und Entwurfszielabonnements anhand von kritischen Faktoren wie Umgebungstyp, Eigentum und Governancemodell, Organisationsstruktur und Anwendungsportfolios.

**Überlegungen zum Entwurf:**

- Abonnements fungieren beim Zuweisen von Azure-Richtlinien als Grenzen. Beispielsweise erfordern sichere Workloads wie z. B. PCI-Workloads (Payment Card Industry) in der Regel zusätzliche Richtlinien, um Compliance zu erreichen. Anstatt eine Verwaltungsgruppe zum Gruppieren von Workloads zu verwenden, die PCI-Compliance erfordern, können Sie die gleiche Abgrenzung auch mit einem Abonnement erzielen. Dadurch wird sichergestellt, dass bei einer kleinen Anzahl von Abonnements nicht zu viele Verwaltungsgruppen vorhanden sind.

- Abonnements dienen als Skalierungseinheit, sodass Komponenten-Workloads innerhalb der [Abonnementgrenzen](https://docs.microsoft.com/azure/azure-subscription-service-limits) der Plattform skaliert werden können. Überdenken Sie während der Workload-Entwurfssitzungen unbedingt Ressourcengrenzwerte für Abonnements.

- Abonnements stellen eine Verwaltungsgrenze für Governance und Isolation bereit, wodurch eine klare Trennung von Zuständigkeiten geschaffen wird.

- Es gibt einen manuellen Prozess (zukünftige Automatisierung ist geplant), mit dem ein Azure AD-Mandant so eingeschränkt werden kann, dass er nur Enterprise Agreement-Registrierungsabonnements (EA) verwendet. Dadurch wird die Erstellung von MSDN-Abonnements im Bereich der Stammverwaltungsgruppe verhindert.

**Entwurfsempfehlungen:**

- Behandeln Sie Abonnements als demokratisierte Verwaltungseinheit, die sich an geschäftlichen Anforderungen und Prioritäten orientiert.

- Informieren Sie Abonnementbesitzer über ihre Rollen und Zuständigkeiten:

  - Führen Sie quartalsweise oder halbjährlich eine Zugriffsprüfung in Azure AD Privileged Identity Management aus, damit Berechtigungen bei Versetzungen der Benutzer innerhalb der Kundenorganisation nicht weiterverbreitet werden.

  - Beanspruchen Sie den vollständigen Besitz von Budgetausgaben und Ressourcenverwendung.

  - Gewährleisten Sie die Richtlinienkompatibilität, und beheben Sie ggf. Verstöße.

- Orientieren Sie sich beim Ermitteln von Anforderungen für neue Abonnements an folgenden Grundsätzen:

  - **Skalierungslimits:** Abonnements dienen als Skalierungseinheit, sodass Komponenten-Workloads innerhalb der Abonnementgrenzen der Plattform skaliert werden können. Beispielsweise sollten für große spezialisierte Workloads (z. B. Hochleistungscomputing, IoT und SAP) besser separate Abonnements verwendet werden, um Limits zu vermeiden (z. B. ein Limit von 50 Azure Data Factory-Integrationen).

  - **Verwaltungsgrenze:** Abonnements bilden eine Verwaltungsgrenze für Governance und Isolation, wodurch eine klare Trennung von Zuständigkeiten geschaffen wird. Beispielsweise werden unterschiedliche Umgebungen wie Entwicklung, Test und Produktion im Hinblick auf die Verwaltung häufig voneinander isoliert.

  - **Richtliniengrenze:** Abonnements fungieren als Grenze für die Zuweisung von Azure-Richtlinien. Sichere Workloads wie PCI erfordern im Allgemeinen zusätzliche Richtlinien, um Compliance zu erreichen, und dieser zusätzliche Aufwand muss nicht ganzheitlich berücksichtigt werden, wenn ein separates Abonnement verwendet wird. Zudem können Entwicklungsumgebungen weniger strikte Richtlinienanforderungen als Produktionsumgebungen haben.

  - **Ziel-Netzwerktopologie:** Virtuelle Netzwerke können nicht abonnementübergreifend freigegeben werden. Sie können jedoch eine Verbindung mit verschiedenen Technologien wie Peering virtueller Netzwerke oder ExpressRoute herstellen. Daher muss bei der Entscheidung, ob ein neues Abonnement benötigt wird, unbedingt bedacht werden, welche Workloads miteinander kommunizieren müssen.

- Gruppieren Sie Abonnements in Verwaltungsgruppen in Einklang mit der Verwaltungsgruppenstruktur und den umfassenden Richtlinienanforderungen. Dadurch wird sichergestellt, dass Abonnements mit demselben Satz von Richtlinien und RBAC-Zuweisungen diese von einer Verwaltungsgruppe erben können, wodurch doppelte Zuweisungen vermieden werden.

- Richten Sie ein dediziertes Verwaltungsabonnement in der Verwaltungsgruppe `Platform` zur Unterstützung globaler Verwaltungsfunktionen ein, z. B. Azure Monitor Log Analytics-Arbeitsbereiche und Azure Automation-Runbooks.

- Richten Sie bei Bedarf ein dediziertes Identitätsabonnement in der Verwaltungsgruppe `Platform` ein, um Windows Server Active Directory-Domänencontroller zu hosten.

- Richten Sie ein dediziertes Konnektivitätsabonnement in der Verwaltungsgruppe `Platform` ein, um einen Azure Virtual WAN-Hub, privates DNS, ExpressRoute-Verbindung und andere Netzwerkressourcen zu hosten. Dadurch wird sichergestellt, dass alle grundlegenden Netzwerkressourcen zusammen abgerechnet und von anderen Workloads isoliert werden.

- Vermeiden Sie ein starres Abonnementmodell, und entscheiden Sie sich beim Gruppieren von Abonnements im gesamten Unternehmen stattdessen für eine Reihe flexibler Kriterien. Dadurch wird sichergestellt, dass Sie angesichts von Änderungen der Struktur und der Workloadkomposition Ihrer Organisation neue Abonnementgruppen erstellen können, anstatt einen festgelegten Satz vorhandener Abonnements zu verwenden. Eine Größe ist nicht universell für Abonnements geeignet. Was für eine Geschäftseinheit funktioniert, funktioniert möglicherweise für eine andere nicht. Einige Apps können innerhalb desselben Zielzonenabonnements nebeneinander vorhanden sein, während andere möglicherweise ein eigenes Abonnement benötigen.

## <a name="configure-subscription-quota-and-capacity"></a>Konfigurieren von Abonnementkontingent und -kapazität

Jede Azure-Region enthält eine endliche Anzahl von Ressourcen. Wenn Sie eine Azure-Einführung auf Unternehmensebene mit großen Ressourcenmengen erwägen, stellen Sie sicher, dass eine ausreichende Kapazität und genügend SKUs verfügbar sind und dass die erreichte Kapazität erkannt und überwacht werden kann.

**Überlegungen zum Entwurf:**

- Beachten Sie für jeden von Ihren Workloads benötigten Dienst die Grenzwerte und Kontingente innerhalb der Azure-Plattform.

- Prüfen Sie die Verfügbarkeit der erforderlichen SKUs in ausgewählten Azure-Regionen. So können neue Features beispielsweise nur in bestimmten Regionen verfügbar sein. Die Verfügbarkeit bestimmter SKUs für bestimmte Ressourcen (z. B. VMs) kann in verschiedenen Regionen variieren.

- Beachten Sie, dass Abonnementkontingente keine Kapazitätsgarantien sind und sich auf die jeweilige Region beziehen.

**Entwurfsempfehlungen:**

- Verwenden Sie Abonnements als Skalierungseinheiten, und skalieren Sie Ressourcen und Abonnements nach Bedarf auf. Dadurch wird sichergestellt, dass ihre Workload bei Bedarf die erforderlichen Ressourcen zum Aufskalieren verwenden kann, ohne dass Abonnementlimits auf der Azure-Plattform überschritten werden.

- Verwenden Sie reservierte Instanzen, um reservierte Kapazität in den erforderlichen Regionen zu priorisieren. Dadurch ist gewährleistet, dass ihre Workload über die erforderliche Kapazität verfügt, selbst wenn in einer bestimmten Region ein hoher Bedarf an dieser Ressource besteht.

- Richten Sie ein Dashboard mit benutzerdefinierten Ansichten zum Überwachen der Kapazitätsauslastung ein. Richten Sie Warnungen ein, wenn die Kapazitätsauslastung kritische Werte erreicht (z. B. 90 % CPU-Auslastung).

- Supportanfragen zum Erhöhen des Kontingents nehmen im Rahmen der Abonnementbereitstellung zu (z. B. insgesamt verfügbare VM-Kerne in einem Abonnement). Dadurch wird sichergestellt, dass Ihre Kontingentgrenzen festgelegt sind, bevor Ihre Workloads das Überschreiten der Standardgrenzen fordern.

- Stellen Sie sicher, dass die erforderlichen Dienste und Features innerhalb der ausgewählten Bereitstellungsregionen verfügbar sind.

## <a name="establish-cost-management"></a>Einrichten der Kostenverwaltung

Die Kostentransparenz für eine technische Umgebung ist eine entscheidende Verwaltungsaufgabe, mit der alle großen Organisationen konfrontiert sind. In diesem Abschnitt werden wichtige Aspekte im Zusammenhang mit der Kostentransparenz in großen Azure-Umgebungen erläutert.

**Überlegungen zum Entwurf:**

- Potenzieller Bedarf an Modellen der verbrauchsbasierten Kostenzuteilung in Bezug auf freigegebene PaaS-Ressourcen (Platform-as-a-Service), z. B. Azure App Service-Umgebung und Azure Kubernetes Service, die zum Erreichen einer höheren Dichte freigegeben werden müssen.

- Optimieren Sie die Kosten mithilfe eines Zeitplans zum Herunterfahren für nicht produktionsbezogene Workloads.

- Prüfen Sie die Empfehlungen zur Kostenoptimierung mithilfe von Azure Advisor.

**Entwurfsempfehlungen:**

- Verwenden Sie Azure Cost Management und Abrechnung für die Kostenaggregation, und machen Sie diese für Anwendungsbesitzer verfügbar.

- Verwenden Sie Azure-Ressourcentags zum Kategorisieren und Gruppieren von Kosten. Damit können Sie einen Mechanismus der verbrauchsbasierten Kostenzuteilung für Workloads nutzen, die ein Abonnement gemeinsam nutzen, oder für eine bestimmte Workload, die sich über mehrere Abonnements erstreckt.
