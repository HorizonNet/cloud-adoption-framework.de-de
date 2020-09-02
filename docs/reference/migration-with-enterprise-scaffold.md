---
title: Azure-Unternehmensgerüst
description: Das Azure-Unternehmensgerüst ist jetzt das Microsoft Cloud Adoption Framework für Azure. Informieren Sie sich darüber, wie Sie die erforderlichen Governanceanforderungen erfüllen und dafür eine gute Balance in Bezug auf die benötigte Flexibilität erzielen.
author: rdendtler
ms.author: rodend
ms.date: 09/22/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
ROBOTS: NOINDEX
ms.openlocfilehash: f70624744e881778d9a51977a5b33931374623b9
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88885642"
---
<!-- docsTest:disable -->
<!-- cSpell:ignore subscope ITSM Hashi -->

# <a name="azure-enterprise-scaffold-prescriptive-subscription-governance"></a>Azure-Unternehmensgerüst: Präskriptive Abonnementgovernance

> [!NOTE]
> Azure-Unternehmensgerüste wurden in das Microsoft Cloud Adoption Framework integriert. Der Inhalt dieses Artikels wird jetzt im Abschnitt zur [Bereitschaft](../ready/index.md) des neuen Frameworks dargestellt. Dieser Artikel wird Anfang 2020 zurückgezogen. Informationen zur Verwendung des neuen Prozesses finden Sie unter [Übersicht zur Bereitschaft](../ready/index.md), [Azure-Zielzonen](../ready/landing-zone/index.md) und [Überlegungen zur Zielzone](../ready/considerations/index.md).

Immer mehr Unternehmen führen für Mobilität und Flexibilität eine öffentliche Cloud ein. Sie setzen auf die Stärken der Cloud, um Umsatz zu generieren und die Ressourcennutzung im Unternehmen zu optimieren. Microsoft Azure bietet eine Vielzahl von Diensten und Funktionen, die Unternehmen wie Bausteine zusammenstellen können, um ein umfangreiches Spektrum an Workloads und Anwendungen zu berücksichtigen.

Die Entscheidung für Microsoft Azure ist nur der erste Schritt auf dem Weg zur Cloud und ihren Vorteilen. Der zweite Schritt besteht darin, zu erkennen, wie das Unternehmen Azure effektiv einsetzen kann, und die grundlegenden Funktionen zu ermitteln, mit denen folgende Fragen beantwortet werden können:

- Ich mache mir Sorgen um die Datenhoheit – wie kann ich sicherstellen, dass meine Daten und Systeme unsere gesetzlich vorgegebenen Anforderungen erfüllen?
- „Wie erfahre ich, was die einzelnen Ressourcen unterstützen, damit ich sie genau zuordnen und abrechnen kann?“
- Ich möchte sicherstellen, dass bei allem, was wir in der Cloud tun oder bereitstellen, die Sicherheit immer an oberster Stelle steht. Wie erreiche ich das?

Die Vorstellung eines leeren Abonnements ohne Schutzmaßnahmen wirkt abschreckend. und kann Ihre Umstellung auf Azure behindern.

Dieser Artikel bietet einen Ausgangspunkt für technische Experten, die die Notwendigkeit der Governance berücksichtigen und mit der Notwendigkeit der Agilität in Einklang bringen müssen. Es wird das Konzept eines Unternehmensgerüsts vorgestellt, das Organisationen beim sicheren Implementieren und Verwalten ihrer Azure-Umgebungen hilft. Der Artikel stellt das Framework bereit, mit dem sich effektive und effiziente Steuerungsmaßnahmen entwickeln lassen.

## <a name="need-for-governance"></a>Notwendigkeit von Governance

Beim Wechsel zu Azure müssen Sie das Thema Governance früh angehen, um die erfolgreiche Verwendung der Cloud innerhalb des Unternehmens sicherzustellen. Leider führen der zeitliche und bürokratische Aufwand beim Erstellen eines umfassenden Governancesystems dazu, dass sich einige Unternehmensgruppen direkt an Anbieter wenden, ohne die eigene IT-Abteilung einzubeziehen. Durch diesen Ansatz können im Unternehmen Sicherheitsrisiken entstehen, wenn die Ressourcen nicht richtig verwaltet werden. Die Eigenschaften der öffentlichen Cloud &mdash;Agilität, Flexibilität und nutzungsbasierte Preise&mdash; sind wichtig für Unternehmensgruppen, die schnell die Anforderungen von Kunden (intern und extern) erfüllen müssen. Aber die Unternehmens-IT muss sicherstellen, dass Daten und Systeme effektiv geschützt sind.

Beim Bau eines Hauses wird ein Gerüst verwendet, um die Basis der Struktur zu erstellen. Das Gerüst gibt die allgemeine Gliederung vor und bietet Ankerpunkte für den Aufbau permanenterer Systeme. Ein Unternehmensgerüst entspricht einer Reihe von flexiblen Steuerelementen und Azure-Funktionen, die der Umgebung eine Struktur geben, sowie Ankern für die in der öffentlichen Cloud erstellten Dienste. Es bietet den Entwicklern (IT und Unternehmensgruppen) eine Grundlage zum Erstellen und Einbinden von neuen Diensten, wobei eine schnelle Bereitstellung eine große Rolle spielt.

Das Gerüst basiert auf Methoden, die wir bei der Zusammenarbeit mit vielen Kunden verschiedener Größen gesammelt haben. Zu diesen Kunden gehören kleine Organisationen, die Lösungen in der Cloud entwickeln, multinationale Großkonzerne sowie unabhängige Softwarehersteller, die Workloads migrieren und Lösungen in der und für die Cloud entwickeln. Das Unternehmensgerüst wurde speziell so flexibel entwickelt, dass es sowohl herkömmliche IT-Workloads als auch agile Workloads unterstützt, z. B. Entwickler, die Software-as-a-Service-Anwendungen (SaaS) basierend auf Funktionen der Azure-Plattform erstellen.

Das Unternehmensgerüst kann als Basis für jedes neue Abonnement in Azure fungieren. Administratoren können damit sicherstellen, dass Workloads in einer Organisation die minimalen Anforderungen an Governance erfüllen, ohne zu verhindern, dass Unternehmensgruppen und Entwickler schnell ihre eigenen Ziele erreichen. Unsere Erfahrung zeigt, dass dies das Wachstum der öffentlichen Cloud eher beschleunigt als hemmt.

> [!NOTE]
> Microsoft hat eine neue Funktion namens [Azure Blueprints](/azure/governance/blueprints/overview) in der Vorschau bereitgestellt, mit der Sie häufig genutzte Images, Vorlagen, Richtlinien und Skripts über viele Abonnements und Verwaltungsgruppen hinweg packen, verwalten und bereitstellen können. Diese Funktion dient als Brücke zwischen dem Zweck des Gerüsts als Referenzmodell und der Bereitstellung des Modells in Ihrer Organisation.
>
Die folgende Abbildung zeigt die Komponenten des Gerüsts. Das Fundament ist ein gut durchdachter Plan für die Verwaltung von Hierarchien und Abonnements. Die Säulen bestehen aus Resource Manager-Richtlinien und soliden Benennungsstandards. Das restliche Gerüst besteht aus zentralen Azure-Funktionen und -Features, die eine sichere und verwaltbare Umgebung ermöglichen und für die notwendige Vernetzung sorgen.

![Unternehmensgerüst](../_images/reference/scaffold-v2.png)

## <a name="define-your-hierarchy"></a>Definieren der Hierarchie

Das Gerüst basiert auf der Hierarchie der Enterprise Agreement-Registrierung (EA) bis hin zu den Abonnements und Ressourcengruppen sowie auf deren Beziehungen untereinander. Die Registrierung definiert die Form und die Nutzung der Azure-Dienste in Ihrem Unternehmen unter vertraglichen Aspekten. Im Rahmen des Enterprise Agreement können Sie die Umgebung weiter in Abteilungen und Konten und in Abonnements und Ressourcengruppen unterteilen, um Ihre Organisationsstruktur widerzuspiegeln.

![Hierarchy](../_images/reference/agreement.png)

Ein Azure-Abonnement ist die grundlegende Einheit, in der alle Ressourcen enthalten sind. Es definiert zudem einige Einschränkungen in Azure, wie z.B. die Anzahl der Kerne, virtuellen Netzwerke und anderer Ressourcen. Mit Ressourcengruppen lässt sich das Abonnementmodell weiter verfeinern, und die Ressourcen können auf natürlichere Weise gruppiert werden.

Jedes Unternehmen ist anders, und die Hierarchie der oben gezeigten Abbildung lässt sehr viel Flexibilität im Hinblick auf den Aufbau von Azure in Ihrem Unternehmen zu. Die Modellierung Ihrer Hierarchie anhand der Anforderungen Ihres Unternehmens hinsichtlich Abrechnung, Ressourcenverwaltung und Ressourcenzugriff ist die erste – und wichtigste – Entscheidung, die Sie beim Einstieg in die öffentliche Cloud treffen müssen.

### <a name="departments-and-accounts"></a>Abteilungen und Konten

Die drei allgemeinen Muster für EA-Registrierungen sind:

- Das auf **Funktionen** basierende Muster:

  ![Das auf Funktionen basierende Muster](../_images/reference/functional.png)

- Das auf **Unternehmenseinheiten** basierende Muster:

  ![Das auf Unternehmenseinheiten basierende Muster](../_images/reference/business.png)

- Das auf **geografischen Regionen** basierende Muster:

  ![Das auf geografischen Regionen basierende Muster](../_images/reference/geographic.png)

Jedes dieser Muster hat seine Vorteile, Organisationen nutzen aber zunehmend das Muster der **Unternehmenseinheiten**, da dieses sowohl Flexibilität beim Erstellen eines Kostenmodells für die Organisation auch eine große Bandbreite an Steuerungsmöglichkeiten bietet. Die Microsoft-Unternehmensgruppe „Core Engineering and Operations“ hat eine effektive Teilmenge des auf **Unternehmenseinheiten** basierenden Musters erstellt. Die Hierarchieebenen hierbei sind **Federal**, **State** und **Local**. Weitere Informationen finden Sie unter [Organisieren Ihrer Abonnements und Ressourcengruppen](../ready/azure-best-practices/organize-subscriptions.md).

### <a name="azure-management-groups"></a>Azure-Verwaltungsgruppen

Microsoft bietet nun eine weitere Möglichkeit, Ihre Hierarchie zu modellieren: [Azure-Verwaltungsgruppen](/azure/azure-resource-manager/management-groups-overview). Verwaltungsgruppen sind wesentlich flexibler als Abteilungen und Konten und können auf bis zu sechs Ebenen geschachtelt werden. Mit Verwaltungsgruppen können Sie eine Hierarchie erstellen, die nur zur effizienten Verwaltung Ihrer Ressourcen dient und unabhängig von Ihrer Hierarchie für die Abrechnung ist. Verwaltungsgruppen können Ihre Abrechnungshierarchie spiegeln, und viele Unternehmen fangen auch so an. Die Stärke von Verwaltungsgruppen liegt jedoch darin, dass Sie sie zur Modellierung Ihres Unternehmens verwenden, verwandte Abonnements zusammenfassen (unabhängig von ihrer Position in der Abrechnungshierarchie) und gemeinsame Rollen, Richtlinien und Initiativen zuweisen. Beispiele hierfür sind:

- **Produktionsbezogen bzw. nicht produktionsbezogen.** Einige Unternehmen erstellen Verwaltungsgruppen, um Abonnements danach zu trennen, ob sie produktionsbezogen sind oder nicht. Verwaltungsgruppen ermöglichen es diesen Kunden, Rollen und Richtlinien einfacher zu verwalten. Beispielsweise kann ein nicht produktionsbezogenes Abonnement Entwicklern den „Mitwirkender“-Zugriff ermöglichen, aber in der Produktion haben sie nur „Leser“-Zugriff.
- **Interne Dienste bzw. externe Dienste.** Unternehmen haben oft unterschiedliche Anforderungen, Richtlinien und Rollen für interne Dienste beziehungsweise für kundenorientierte Dienste.

Sorgfältig konzipierte Verwaltungsgruppen sind neben Azure Policy und Azure-Initiativen das Rückgrat einer effizienten Governance in Azure.

### <a name="subscriptions"></a>Abonnements

Wenn Sie Ihre Abteilungen und Konten (bzw. Verwaltungsgruppen) festlegen, liegt Ihr Hauptaugenmerk darauf, wie Sie Ihre Azure-Umgebung Ihrer Organisation entsprechend aufteilen. Die eigentliche Arbeit findet hingegen in den Abonnements statt. Daher wirken sich Ihre Entscheidungen hier auf die Sicherheit, Skalierbarkeit und Abrechnung aus. Viele Organisationen nutzen die folgenden Muster als Leitlinien:

- **Anwendung/Dienst:** Abonnements stellen eine Anwendung oder einen Dienst dar (Anwendungsportfolio).
- **Lebenszyklus:** Abonnements stellen einen Lebenszyklus eines Diensts dar (beispielsweise Produktion oder Entwicklung).
- **Abteilung:** Abonnements stellen Abteilungen in der Organisation dar.

Die ersten beiden Muster werden am häufigsten verwendet und sind sehr empfehlenswert. Der Lebenszyklusansatz eignet sich für die meisten Organisationen. In diesem Fall wird allgemein empfohlen, zwei Standardabonnements zu verwenden – `Production` und `Nonproduction` – und die Umgebungen dann mithilfe von Ressourcengruppen weiter zu unterteilen.

### <a name="resource-groups"></a>Ressourcengruppen

Mit Azure Resource Manager können Sie Ressourcen in aussagekräftigen Gruppen für Verwaltung, Abrechnung oder natürliche Affinität organisieren. Ressourcengruppen sind Container für Ressourcen, die einen gemeinsamen Lebenszyklus aufweisen oder gleiche Attribute wie „alle SQL Server“ oder „Anwendung A“ verwenden.

Ressourcengruppen dürfen nicht geschachtelt sein, und Ressourcen dürfen nur zu einer einzigen Ressourcengruppe gehören. Einige Aktionen gelten für alle Ressourcen in einer Ressourcengruppe. Durch das Löschen einer Ressourcengruppe werden beispielsweise alle Ressourcen innerhalb der Ressourcengruppe entfernt. Ähnlich wie bei Abonnements gibt es beim Erstellen von Ressourcengruppen allgemeine Muster: Workloads der „herkömmlichen IT“ und Workloads der „agilen IT“:

- Workloads der „herkömmlichen IT“ werden meist nach Elementen innerhalb des gleichen Lebenszyklus gruppiert (z.B. eine Anwendung). Eine Gruppierung nach Anwendung ermöglicht die Verwaltung einzelner Anwendungen.
- Workloads der „agilen IT“ konzentrieren sich in der Regel auf Cloudanwendungen, die externen Kunden zugänglich sind. Die Ressourcengruppen spiegeln häufig die Ebenen der Bereitstellung (z.B. Webschicht, App-Schicht) und der Verwaltung wider.

> [!NOTE]
> Das Verständnis Ihrer Workloads erleichtert es Ihnen, eine Strategie für Ressourcengruppen zu entwickeln. Diese Muster können nach Bedarf kombiniert werden. Eine Ressourcengruppe für gemeinsame Dienste kann sich beispielsweise im gleichen Abonnement befinden wie „agile“ Ressourcengruppen.

## <a name="naming-standards"></a>Benennungsstandards

Die erste Säule des Gerüsts ist ein konsistenter Benennungsstandard. Mit sorgfältig konzipierten Benennungsstandards können Sie Ressourcen im Portal, auf einer Rechnung und innerhalb von Skripts identifizieren. Wahrscheinlich verwenden Sie bereits Benennungsstandards für die lokale Infrastruktur. Wenn Sie Azure zu Ihrer Umgebung hinzufügen, sollten Sie diese Benennungsstandards für Azure-Ressourcen übernehmen.

> [!TIP]
> Informationen zu Benennungskonventionen:
>
> - Überprüfen und übernehmen Sie nach Möglichkeit den [Leitfaden für die Cloud Adoption Framework-Benennung und -Markierung](../ready/azure-best-practices/naming-and-tagging.md). Dieser Leitfaden hilft Ihnen bei der Entscheidung für einen sinnvollen Benennungsstandard und bietet viele Beispiele.
> - Verwenden von Resource Manager-Richtlinien zum Durchsetzen von Benennungsstandards.
>
> Denken Sie immer daran, dass sich Namen später nur sehr schwer ändern lassen – nehmen Sie sich also jetzt genügend Zeit, damit später keine Probleme auftreten.

Konzentrieren Sie sich bei Ihren Benennungsstandards auf die Ressourcen, die am häufigsten gesucht und verwendet werden. Ressourcengruppen sollten z.B. aus Gründen der Klarheit einem sehr strikten Standard folgen.

### <a name="resource-tags"></a>Ressource Tags

Ressourcentags sind eng an Benennungsstandards gekoppelt. Je mehr Ressourcen den Abonnements hinzugefügt werden, desto wichtiger wird es, diese für Abrechnung, Verwaltung und Betrieb logisch zu kategorisieren. Weitere Informationen finden Sie unter [Verwenden von Tags zum Organisieren von Azure-Ressourcen](/azure/azure-resource-manager/management/tag-resources).

> [!IMPORTANT]
> Tags können persönliche Informationen enthalten und fallen möglicherweise unter die DSGVO. Planen Sie die Verwaltung Ihrer Tags sorgfältig. Allgemeine Informationen zur DSGVO finden Sie im Abschnitt [DSGVO im Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Tags dienen neben der Abrechnung und Verwaltung zu vielen weiteren Zwecken. Sie werden häufig im Rahmen der Automatisierung verwendet (siehe Abschnitt weiter unten). Dies kann bei unzureichender Vorausplanung zu Konflikten führen. Die bewährte Methode besteht darin, alle gängigen Tags auf Unternehmensebene (z. B. ApplicationOwner und CostCenter) zu identifizieren und sie konsistent anzuwenden, wenn Ressourcen automatisiert bereitgestellt werden.

## <a name="azure-policy-and-initiatives"></a>Azure Policy und Azure-Initiativen

Die zweite Säule des Gerüsts ist die Verwendung von [Azure Policy und Azure-Initiativen](/azure/azure-policy/azure-policy-introduction) für das Risikomanagement, indem Regeln (mit Auswirkungen) für die Ressourcen und Dienste in Ihren Abonnements erzwungen werden. Azure-Initiativen sind Sammlungen aus Richtlinien, die alle einem einzigen Ziel dienen. Richtlinien und Initiativen werden dann einem Ressourcenbereich zugewiesen, um die Erzwingung dieser Richtlinien zu starten.

Azure Policy und Azure-Initiativen sind noch leistungsstärker, wenn sie mit den oben beschriebenen Verwaltungsgruppen eingesetzt werden. Verwaltungsgruppen ermöglichen die Zuweisung einer Initiative oder Richtlinie zu einer ganzen Gruppe von Abonnements.

### <a name="common-uses-of-resource-manager-policies"></a>Allgemeine Verwendungsmöglichkeiten von Resource Manager-Richtlinien

Richtlinien und Initiativen sind leistungsfähige Tools im Azure-Toolkit. Mit Richtlinien können Unternehmen Steuerungsmechanismen für Workloads der „herkömmlichen IT“ bereitstellen, um die Stabilität zu gewährleisten, die für branchenspezifische Anwendungen benötigt wird. Gleichzeitig unterstützen die Richtlinien auch „agile“ Workloads, z. B. das Entwickeln von Kundenanwendungen, ohne das Unternehmen zusätzlichen Risiken auszusetzen. Die am häufigsten verwendeten Muster für Richtlinien sind:

- **Geografische Compliance und Datenhoheit.** Die Liste der weltweiten Azure-Regionen wächst kontinuierlich. Unternehmen müssen häufig sicherstellen, dass Ressourcen in einem bestimmten Bereich innerhalb einer geografischen Region bleiben, um gesetzliche Vorschriften zu erfüllen.
- **Vermeidung öffentlich verfügbarer Server.** Azure Policy kann die Bereitstellung bestimmter Ressourcentypen verhindern. Ein gängiges Szenario besteht darin, eine Richtlinie zu erstellen, um das Erstellen einer öffentlichen IP-Adresse innerhalb eines bestimmten Bereichs zu verweigern und so zu verhindern, dass der Server unabsichtlich im Internet verfügbar gemacht wird.
- **Cost Management und Metadaten**. Ressourcentags werden häufig dazu verwendet, wichtige Abrechnungsdaten zu Ressourcen und Ressourcengruppen wie CostCenter, Owner oder anderen hinzuzufügen. Diese Tags sind für eine präzise Abrechnung und Verwaltung der Ressourcen von unschätzbarem Wert. Richtlinien können die Anwendung von Ressourcentags auf alle bereitgestellten Ressourcen erzwingen und vereinfachen damit die Verwaltung.

### <a name="common-uses-of-initiatives"></a>Gängige Nutzungsszenarien für Initiativen

Initiativen bieten Unternehmen die Möglichkeit, logische Richtlinien zu gruppieren und als eine einzelne Entität zu verfolgen. Initiativen unterstützten das Unternehmen dabei, die Anforderungen sowohl von agilen als auch von herkömmlichen Workloads zu erfüllen. Gängige Nutzungsszenarien für Initiativen sind:

- **Aktivieren der Überwachung im Azure Security Center.** Dies ist eine Standardinitiative in Azure Policy und ein ausgezeichnetes Beispiel dafür, was Initiativen eigentlich sind. Diese Initiative aktiviert Richtlinien, die nicht verschlüsselte SQL-Datenbanken, Sicherheitslücken in virtuellen Computern (VMs) und allgemeinere Sicherheitsanforderungen ermitteln.
- **Gesetzesspezifische Initiative.** Unternehmen gruppieren häufig Richtlinien, für die die gleiche gesetzliche Vorschrift gilt (z.B. HIPAA), sodass die Steuerungsmechanismen und die Einhaltung dieser Mechanismen effizient nachverfolgt werden können.
- **Ressourcentypen und SKUs.** Mit einer Initiative zur Einschränkung der bereitstellbaren Ressourcentypen und SKUs können Sie Kosten senken und sicherstellen, dass Ihre Organisation nur solche Ressourcen bereitstellt, die von Ihrem Team aufgrund der vorhandenen Kenntnisse und Verfahren unterstützt werden können.

> [!TIP]
> Es empfiehlt sich, immer Initiativendefinitionen zu verwenden, keine Richtliniendefinitionen. Nachdem Sie eine Initiative zu einem Bereich zugewiesen haben, wie z.B. einem Abonnement oder einer Verwaltungsgruppe, können Sie der Initiative ganz einfach weitere Richtlinien hinzufügen, ohne Zuweisungen ändern zu müssen. So erhalten Sie einen wesentlich besseren Überblick darüber, welche Richtlinien angewendet wurden, und können die Compliance einfacher nachverfolgen.

### <a name="policy-and-initiative-assignments"></a>Richtlinien- und Initiativenzuweisungen

Nachdem Sie Richtlinien erstellt und in logische Initiativen gruppiert haben, müssen Sie eine Richtlinie einem Bereich zuweisen – dabei kann es sich um eine Verwaltungsgruppe, ein Abonnement oder sogar eine Ressourcengruppe handeln. Durch Zuweisungen können Sie auch einen Teilbereich aus der Zuweisung einer Richtlinie ausschließen. Ein Beispiel: Wenn Sie die Erstellung öffentlicher IP-Adressen in einem Abonnement verweigern, können Sie eine Zuweisung mit einem Ausschluss für eine Ressourcengruppe erstellen, die mit Ihrer geschützten DMZ verbunden ist.

In [diesem GitHub-Repository](https://github.com/azure/azure-policy) finden Sie verschiedene Beispiele, die veranschaulichen, wie Azure Policy und Azure-Initiativen auf verschiedene Ressourcen in Azure angewendet werden können.

## <a name="identity-and-access-management"></a>Identitäts- und Zugriffsverwaltung

Eine der ersten und entscheidendsten Fragen, die Sie sich vor dem Einstieg in die öffentliche Cloud stellen sollten, lautet „Wer darf auf die Ressourcen zugreifen und wie dieser Zugriff gesteuert werden kann. Die Steuerung des Zugriffs auf das Azure-Portal und die Ressourcen im Portal ist entscheidend für die langfristige Sicherheit Ihrer Objekte in der Cloud.

Um den Zugriff auf Ihre Ressourcen zu sichern, konfigurieren Sie zuerst Ihren Identitätsanbieter und dann die Rollen und den Zugriff. Azure Active Directory (Azure AD) – verknüpft mit Ihrem lokalen Active Directory – ist die Grundlage von Identitäten in Azure. Azure AD ist jedoch **nicht** dasselbe wie ein lokales Active Directory, und es ist wichtig zu wissen, was ein Azure AD-Mandant ist und wie Mandanten mit Ihrer Registrierung in Verbindung stehen. Lesen Sie die Ausführungen zum [Verwalten des Ressourcenzugriffs in Azure](../govern/resource-consistency/resource-access-management.md) durch, um ein umfassendes Verständnis von Azure AD und lokalen Active Directory-Instanzen zu erlangen. Um Ihre lokale Active Directory-Instanz mit Azure AD zu verbinden und zu synchronisieren, installieren und konfigurieren Sie das [Azure AD Connect-Tool](/azure/active-directory/connect/active-directory-aadconnect) lokal.

![Diagramm der AD-Architektur](../_images/reference/ad-architecture.png)

Als Azure ursprünglich veröffentlicht wurde, waren Zugriffssteuerungen für ein Abonnement sehr einfach: Administrator oder Co-Administrator. Durch den Zugriff auf ein Abonnement im klassischen Modell war Zugriff auf alle Ressourcen im Portal möglich. Dieses Fehlen einer präziseren Steuerung hat zur Zunahme von Abonnements geführt, um eine angemessene Zugriffssteuerung für eine Registrierung bereitzustellen. Diese Zunahme von Abonnements ist nicht mehr erforderlich. Mit der rollenbasierten Zugriffssteuerung (Role-Based Access Control, RBAC) können Sie Benutzer zu Standardrollen zuweisen, die Zugriffsrechte als „Besitzer“, „Mitwirkender“ oder „Leser“ gewähren. Sie können auch selbst Rollen erstellen.

Beim Implementieren des rollenbasierten Zugriffs empfiehlt es sich dringend, folgende Punkte zu beachten:

- Kontrollieren Sie den Administrator/Co-Administrator eines Abonnements sehr genau, da diese Rollen über umfassende Berechtigungen verfügen. Sie müssen das Konto „Abonnementbesitzer“ nur dann als Co-Administrator hinzufügen, wenn der Benutzer klassische Azure-Bereitstellungen verwalten soll.
- Verwenden Sie Verwaltungsgruppen, um [Rollen](/azure/azure-resource-manager/management-groups-overview#management-group-access) für mehrere Abonnements zuzuweisen und so den Aufwand für die Verwaltung auf Abonnementebene zu reduzieren.
- Fügen Sie Azure-Benutzer einer Gruppe (z.B. Besitzer von Anwendung X) in Active Directory hinzu. Verwenden Sie die synchronisierte Gruppe, um Mitgliedern der Gruppe die erforderlichen Rechte zum Verwalten der Ressourcengruppe, die die Anwendung enthält, zu gewähren.
- Befolgen Sie das Prinzip, die **geringsten Rechte** zu gewähren, die zur Erledigung der erwarteten Arbeit erforderlich sind.

> [!IMPORTANT]
> Nutzen Sie die Funktionen [Azure AD Privileged Identity Management](/azure/active-directory/privileged-identity-management/pim-configure) (PIM), Azure [Multi-Factor Authentication](/azure/active-directory/authentication/howto-mfa-getstarted) und [Bedingter Zugriff](/azure/active-directory/conditional-access/overview), um für mehr Sicherheit und Transparenz für alle administrativen Aktivitäten in sämtlichen Azure-Abonnements zu sorgen. Diese Funktionen werden mit einer gültigen Azure AD Premium-Lizenz (je nach Feature) bereitgestellt, um Ihre Identitäten noch besser zu sichern und zu verwalten. Azure AD PIM ermöglicht den Just-in-Time-Verwaltungszugriff mit einem Genehmigungsworkflow sowie die vollständige Überwachung der Aktivierungen und Aktivitäten eines Administrators. Azure Multi-Factor Authentication ist eine weitere wichtige Funktion und ermöglicht eine zweistufige Überprüfung bei der Anmeldung beim Azure-Portal. In Kombination mit den Steuerungsmöglichkeiten des bedingten Zugriffs können Sie das Risiko einer Kompromittierung effektiv senken.

Die Planung und Vorbereitung von Identität und Zugriffssteuerung sowie das Befolgen von [bewährten Methoden beim Azure Identity Management](/azure/security/fundamentals/identity-management-best-practices) stellt eine der besten Strategien für die Risikominderung dar, die Sie anwenden könne, und sollte für jede Bereitstellung als obligatorisch betrachtet werden.

## <a name="security"></a>Sicherheit

Eines der größten Hindernisse bei der Einführung der Cloud sind seit jeher Bedenken wegen der Sicherheit. IT-Risikomanager und für Sicherheitsabteilungen müssen sicherstellen, dass der Schutz und die Sicherheit der Ressourcen in Azure standardmäßig gewährleistet sind. Azure bietet verschiedene Funktionen, mit denen Sie Ressourcen schützen und Bedrohungen dieser Ressourcen erkennen und verhindern können.

### <a name="azure-security-center"></a>Azure Security Center

Das [Azure Security Center](/azure/security-center/security-center-intro) bietet eine einheitliche Ansicht des Sicherheitsstatus aller Ressourcen in Ihrer Umgebung sowie Funktionen für einen erweiterten Schutz vor Bedrohungen. Das Azure Security Center ist eine offene Plattform, über die Microsoft-Partner Softwareanwendungen erstellen können, die eingebunden werden und die Funktionalität erweitern. Die grundlegenden Funktionen von Azure Security Center (kostenloser Tarif) bieten Bewertungen und Empfehlungen, die Ihren Sicherheitsstatus verbessern. Die zahlungspflichtigen Tarife bieten zusätzliche wertvolle Funktionen wie z. B. Just-in-Time-Zugriff und adaptive Anwendungssteuerung (Zulassungslisten).
> [!TIP]
> Azure Security Center ist ein sehr leistungsfähiges Tool, das fortlaufend mit neuen Funktionen verbessert wird, mit denen Sie Bedrohungen erkennen und Ihr Unternehmen schützen können. Es wird dringend empfohlen, Azure Security Center stets zu aktivieren.

### <a name="locks-for-azure-resources"></a>Sperren für Azure-Ressourcen

Je mehr zentrale Dienste Ihre Organisation zu Abonnements hinzufügt, desto wichtiger wird es, eine Unterbrechung des Geschäftsbetriebs zu vermeiden. Eine häufige Unterbrechung tritt auf, wenn ein in einem Azure-Abonnement ausgeführte Skript oder Tool unbeabsichtigt eine Ressource löscht. Mit [Sperren](/azure/azure-resource-manager/resource-group-lock-resources) werden Vorgänge für wertvolle Ressourcen eingeschränkt, bei denen eine Änderung oder Löschung erhebliche Auswirkungen hätte. Sie können Sperren auf Abonnements, Ressourcengruppen oder einzelne Ressourcen anwenden. Wenden Sie Sperren auf grundlegende Ressourcen wie virtuelle Netzwerke, Gateways, Netzwerksicherheitsgruppen und wichtige Speicherkonten an.

### <a name="secure-devops-kit-for-azure"></a>Secure DevOps Kit for Azure

Das „Secure DevOps Kit for Azure“ (AzSK) ist eine Sammlung aus Skripts, Tools, Erweiterungen und Automatisierungen, die ursprünglich intern vom IT-Team von Microsoft erstellt und über [GitHub als Open Source veröffentlicht wurden](https://github.com/azsk/devopskit-docs). Das AzSK erfüllt alle Sicherheitsanforderungen von Azure-Abonnements und -Ressourcen für Teams, indem es eine umfassende Automatisierung und eine nahtlose Integration der Sicherheit in native DevOps-Workflows bietet. So sorgt es für sichere DevOps-Prozesse mit diesen sechs Schwerpunktbereichen:

- Sichern des Abonnements
- Ermöglichen einer sicheren Entwicklung
- Integrieren der Sicherheit in CI/CD
- Fortlaufende Sicherung
- Warnung und Überwachung
- Governance zum Senken von Cloudrisiken

![Übersichtsdiagramm des Secure DevOps Kit for Azure](../_images/reference/secure-devops-kit.png)

Das AzSK umfasst eine Vielzahl von Tools, Skripts und Informationen, die ein wichtiger Bestandteil einer umfangreichen Azure-Governanceplanung sind. Um die Ziele Ihrer Organisation hinsichtlich des Risikomanagements zu unterstützen, ist es von entscheidender Bedeutung, dieses Toolkit in Ihr Gerüst einzubauen.

### <a name="azure-update-management"></a>Azure-Updateverwaltung

Eine der wichtigsten Aufgaben bei der Sicherung Ihrer Umgebung ist Folgendes: Sie müssen sicherstellen, dass immer die neuesten Patches auf Ihre Server aufgespielt werden. Es gibt verschiedene Tools für diesen Zweck. Azure bietet die [Azure-Updateverwaltung](/azure/automation/automation-update-management) für die Identifikation und das Rollout wichtiger Betriebssystempatches. Die Updateverwaltung nutzt dazu Azure Automation (dieser Dienst wird weiter unten in diesem Leitfaden im Abschnitt [Automatisieren](#automate) erläutert).

## <a name="monitor-and-alerts"></a>Überwachung und Warnungen

Das Sammeln und Analysieren von Telemetriedaten, die Einblicke in die Aktivitäten, Leistungsmetriken, Integrität und Verfügbarkeit der Dienste bieten, die Sie in Ihren Azure-Abonnements verwenden, ist von entscheidender Bedeutung bei der proaktiven Verwaltung Ihrer Anwendungen und Infrastruktur und eine grundlegende Anforderung jedes Azure-Abonnements. Jeder Azure-Dienst gibt Telemetriedaten in Form von Aktivitätsprotokollen, Metriken und Diagnoseprotokollen aus.

- **Aktivitätsprotokolle** beschreiben alle Vorgänge, die in den Ressourcen in Ihren Abonnements durchgeführt wurden.
- **Metriken** sind Zahlendaten, die von einer Ressource ausgegeben werden und die Leistung und Integrität einer Ressource beschreiben.
- **Diagnoseprotokolle** werden von einem Azure-Dienst ausgegeben und stellen umfangreiche und in kurzen Abständen erfasste Daten zum Betrieb dieses Diensts bereit.

Sie können diese Daten auf verschiedenen Ebenen betrachten und Aktionen daraus ableiten, und die Daten werden kontinuierlich verbessert. Azure bietet **gemeinsam genutzte**, **grundlegende** und **tiefgreifende** Überwachungsfunktionen für Azure-Ressourcen durch die in der Abbildung unten gezeigten Dienste.

![Überwachung](../_images/reference/monitoring.png)

### <a name="shared-capabilities"></a>Gemeinsam genutzte Funktionen

- **Alerts:** Sie können jedes Protokoll, jedes Ereignis und jede Metrik von Azure-Ressourcen erfassen, aber ohne die Möglichkeit, bei kritischen Bedingungen eine Benachrichtigung zu erhalten und reagieren zu können, sind diese Daten nur für Rückschauen und forensische Analysen zu gebrauchen. Azure Alerts benachrichtigt Sie proaktiv bei Bedingungen, die Sie für all Ihre Anwendungen und die gesamte Infrastruktur definieren können. Sie erstellen Warnungsregeln für Protokolle, Ereignisse und Metriken, die Aktionsgruppen verwenden, um bestimmte Empfängergruppen zu benachrichtigen. Aktionsgruppen ermöglichen auch automatische Korrekturen mithilfe von externen Aktionen wie z.B. Webhooks zum Ausführen von Azure Automation-Runbooks und Azure Functions.

- **Dashboards:** Mit Dashboards können Sie ressourcen- und abonnementübergreifend Überwachungsansichten aggregieren und Daten kombinieren, um einen Einblick in die Telemetriedaten Ihrer Azure-Ressourcen im gesamten Unternehmen zu erhalten. Sie können selbst Ansichten erstellen, konfigurieren und mit für andere Benutzer freigeben. So können Sie beispielsweise ein aus verschiedenen Kacheln für Datenbankadministratoren bestehendes Dashboard erstellen, um Informationen für sämtliche Azure-Datenbankdienste wie etwa Azure SQL-Datenbank, Azure Database for PostgreSQL und Azure Database for MySQL bereitzustellen.

- **Metrik-Explorer:** Metriken sind numerische Werte, die von Azure-Ressourcen generiert werden (z.B. Prozentsatz der CPU-Auslastung oder Datenträger-E/A-Vorgänge) und Erkenntnisse zu Betrieb und Leistung Ihrer Ressourcen bieten. Mit dem Metrik-Explorer können Sie die Metriken, die Sie interessieren, definieren und zur Aggregation und Analyse an Log Analytics senden.

### <a name="core-monitoring"></a>Kernüberwachung

- **Azure Monitor:** Azure Monitor ist der grundlegende Plattformdienst, mit dem Sie Ihre Azure-Ressourcen an einem zentralen Ort verwalten können. Die Azure-Portal-Schnittstelle von Azure Monitor bietet einen zentralen Startpunkt für alle Überwachungsfunktionen in Azure, einschließlich der tiefgreifenden Überwachungsfunktionen von Application Insights, Log Analytics, Network Monitoring, Management Solutions und Service Maps. Mit Azure Monitor können Sie Metriken und Protokolle aus Azure-Ressourcen in Ihrer gesamten Cloudstruktur visualisieren, abfragen, weiterleiten und archivieren und ggf. notwendige Maßnahmen ergreifen. Sie können Daten nicht nur über das Portal, sondern auch über PowerShell-Cmdlets, eine plattformübergreifende Befehlszeilenschnittstelle oder die Azure Monitor-REST-APIs abrufen.

- **Azure Advisor:** Azure Advisor überwacht beständig Telemetriedaten in Ihren Abonnements und Umgebungen. Es empfiehlt außerdem bewährte Methoden zur Kostenoptimierung für Ihre Azure-Ressourcen und zur Verbesserung der Leistung, Sicherheit und Verfügbarkeit Ihrer Anwendungsressourcen.

- **Azure Service Health:** Azure Service Health erkennt Probleme bei Azure-Diensten, die sich auf Ihre Anwendungen auswirken können, und unterstützt Sie bei der Planung von Wartungsfenstern.

- **Aktivitätsprotokoll:** Im Aktivitätsprotokoll werden sämtliche Vorgänge beschrieben, die für Ressourcen in Ihren Abonnements ausgeführt wurden. Sie erhalten ein Überwachungsprotokoll, mit dem Sie das _Was_, _Wer_ und _Wann_ aller Erstellungs-, Aktualisierungs- und Löschvorgänge in Ressourcen ermitteln können. Aktivitätsprotokollereignisse werden auf der Plattform gespeichert und sind 90 Tage verfügbar. Sie können Aktivitätsprotokolle in Log Analytics einspeisen, um eine längere Beibehaltungsdauer sowie tiefgreifendere Abfragen und Analysen über mehrere Ressourcen hinweg zu erzielen.

### <a name="deep-application-monitoring"></a>Umfassende Anwendungsüberwachung

- **Application Insights:** Mit Application Insights können Sie anwendungsspezifische Telemetriedaten sammeln und die Leistung, Verfügbarkeit und Nutzung von Anwendungen in der Cloud oder Ihrer lokalen Umgebung überwachen. Statten Sie zu diesem Zweck Ihre Anwendung mit den unterstützten SDKs für verschiedene Sprachen aus, wie etwa .NET, JavaScript, Java, Node.js, Ruby und Python. Application Insights-Ereignisse werden im gleichen Log Analytics-Datenspeicher erfasst, der die Infrastruktur- und Sicherheitsüberwachung unterstützt, sodass Sie Ereignisse mithilfe einer umfangreichen Abfragesprache über einen bestimmten Zeitraum korrelieren und aggregieren können.

### <a name="deep-infrastructure-monitoring"></a>Umfassende Infrastrukturüberwachung

- **Log Analytics:** Log Analytics spielt eine zentrale Rolle bei der Azure-Überwachung, da er Telemetriedaten und andere Daten aus vielen verschiedenen Quellen sammelt sowie eine Abfragesprache und eine Analyse-Engine bereitstellt, damit Sie Einblicke in die Abläufe Ihrer Anwendungen und Ressourcen erhalten. Sie können entweder über schnelle Protokollsuchen und Ansichten direkt mit Log Analytics-Daten interagieren, oder Sie können Analysetools in anderen Azure-Diensten nutzen, z. B. Application Insights oder Azure Security Center, bei denen die Daten in Log Analytics gespeichert werden.

- **Netzwerküberwachung:** Mit den Netzwerküberwachungsdiensten von Azure erhalten Sie Einblicke in Netzwerkdatenverkehr, Leistung, Sicherheit, Konnektivität und Engpässe. Ein sorgfältig geplanter Netzwerkentwurf sollte die Konfiguration von Azure-Netzwerküberwachungsdiensten wie z.B. Network Watcher und ExpressRoute Monitor umfassen.

- **Verwaltungslösungen:** Verwaltungslösungen sind Pakete mit Logik, Einblicken und vordefinierten Log Analytics-Abfragen für eine Anwendung oder einen Dienst. Log Analytics bildet die Grundlage für die Speicherung und Analyse von Ereignisdaten. Zu den Verwaltungslösungen gehören beispielsweise die Überwachung von Containern und die Azure SQL-Datenbank-Analyse.

- **Dienstzuordnung:** Die Dienstzuordnung bietet eine grafische Darstellung Ihrer Infrastrukturkomponenten sowie der zugehörigen Prozesse und gegenseitigen Abhängigkeiten mit anderen Computern und externen Prozessen. Die Anwendung integriert Ereignisse, Leistungsdaten und Verwaltungslösungen in Log Analytics.

> [!TIP]
> Bevor Sie einzelne Warnungen erstellen, erstellen und verwalten Sie einen Satz freigegebener Aktionsgruppen, die für alle Azure-Warnungen verwendet werden können. So können Sie den Lebenszyklus Ihrer Empfängerlisten, Methoden für die Nachrichtenübermittlung (E-Mail, SMS, Telefonnummern) und Webhooks zu externen Aktionen (Azure Automation-Runbooks, Azure Functions und Logic Apps, ITSM) zentral verwalten.

## <a name="cost-management"></a>Kostenverwaltung

Eine der wichtigsten Veränderungen, die ein Umstieg von der lokalen in die öffentliche Cloud mit sich bringt, ist die Art der Finanzierung: Diese verlagert sich vom Kapitalaufwand (Hardwarekauf) hin zum Betriebsaufwand (Zahlung nur für tatsächlich genutzte Dienste). Dieser Wechsel erfordert auch eine sorgfältigere Verwaltung Ihrer Kosten. Der große Vorteil der Cloud besteht darin, dass Sie die Kosten eines von Ihnen genutzten Diensts grundlegend und positiv beeinflussen können, indem Sie den Dienst einfach deaktivieren oder herunterskalieren, wenn Sie ihn nicht benötigen. Die Verwaltung der Kosten in der Cloud ist eine bewährte Methode, die erfahrene Kunden bereits täglich anwenden.

Microsoft stellt verschiedene Tools zur Verfügung, mit denen Sie Ihre Kosten visualisieren, nachverfolgen und verwalten können. Wir bieten Ihnen auch einen vollständigen Satz APIs, mit denen Sie das Kostenmanagement anpassen und in Ihre eigenen Tools und Dashboards integrieren können. Diese Tools sind locker in zwei Gruppen zusammengefasst: Azure-Portal-Funktionen und externe Funktionen.

### <a name="azure-portal-capabilities"></a>Azure-Portal-Funktionen

Diese Tools stellen Ihnen sofortige Informationen zu Kosten bereit und bieten die Möglichkeit, sofort Aktionen auszuführen.

- **Kosten für Abonnementressourcen:** Die Ansicht [Azure Cost Management](/azure/cost-management-billing/cost-management-billing-overview) im Portal bietet einen schnellen Überblick über Ihre Kosten sowie Informationen zu den täglichen Ausgaben, aufgeschlüsselt nach Ressource oder Ressourcengruppe.
- **Azure Cost Management:** Dadurch können Sie Ihre Azure-Ausgaben sowie Ihre Ausgaben für andere öffentliche Cloudanbieter verwalten und analysieren. Das Produkt bietet sowohl kostenlose als auch kostenpflichtige Tarife sowie eine Vielzahl von Funktionen.
- **Azure-Budgets und Aktionsgruppen:** Herauszufinden, was wie viel kostet, und diese Kosten möglicherweise zu senken, war bis vor Kurzem eine eher manuelle Aufgabe. Mit der Einführung von Azure-Budgets und seinen APIs können Sie jetzt [Aktionen erstellen](https://channel9.msdn.com/Shows/Azure-Friday/Managing-costs-with-the-Azure-Budgets-API-and-Action-Groups), die ausgeführt werden, wenn die Kosten einen Schwellenwert erreichen. Sie könnten z. B. eine „Test“-Ressourcengruppe schließen, wenn sie 100 % ihres Budgets erreicht hat.
- **Azure Advisor:** Das Wissen, was etwas kostet, ist nur die halbe Miete. Wie dieses Wissen umgesetzt wird, steht auf einem ganz anderen Blatt. [Azure Advisor](/azure/advisor/advisor-overview) bietet Empfehlungen zu Aktionen, durch die Sie Geld sparen, die Zuverlässigkeit verbessern oder sogar die Sicherheit erhöhen können.

### <a name="external-cost-management-tools"></a>Externe Kostenmanagementtools

<!-- TODO: Content packs are deprecated. -->

- **Power BI – Azure Consumption Insights:** Möchten Sie selbst Visualisierungen für Ihre Organisation erstellen? Dann ist das Azure Consumption Insights-Inhaltspaket für Power BI das Tool Ihrer Wahl. Mit diesem Inhaltspaket und Power BI können Sie benutzerdefinierte Visualisierungen für Ihre Organisation erstellen, tiefer greifende Kostenanalysen durchführen und weitere Datenquellen zur Erweiterung der Lösung hinzufügen.

- **Azure Consumption-APIs:** Die [Consumption-APIs](/rest/api/consumption) bietet programmgesteuerten Zugriff auf die Kosten- und Nutzungsdaten sowie Informationen zu Budgets, reservierten Instanzen und Marketplace-Gebühren. Diese APIs sind nur für EA-Registrierungen und einige Web Direct-Abonnements zugänglich, bieten Ihnen aber die Möglichkeit, Ihre Kostendaten in Ihre eigenen Tools und Data Warehouses zu integrieren. Sie können auch über die [Azure CLI auf diese APIs zugreifen](/cli/azure/consumption?view=azure-cli-latest).

Kunden, die langfristige und erfahrene Cloudanwender sind, befolgen bestimmte Best Practices:

- **Aktive Überwachung der Kosten.** Organisationen, die bereits über viel Erfahrung mit Azure verfügen, überwachen die Kosten fortlaufend und ergreifen bei Bedarf Maßnahmen. Einige Organisationen setzen sogar dediziertes Personal ein, das Analysen durchführt und Änderungen an der Nutzung vorschlägt. Dies macht sich in dem Moment mehr als bezahlt, wenn ein HDInsight-Cluster ermittelt wird, der bereits seit mehreren Monaten ungenutzt ausgeführt wird.
- **Verwenden von Azure Reserved VM Instances** Ein weiterer wichtiger Faktor für das Kostenmanagement in der Cloud ist die Verwendung des am besten geeigneten Tools für jeden Auftrag. Wenn Sie über eine IaaS-VM verfügen, die rund um die Uhr aktiv bleiben muss, können Sie mit einer reservierten Instanz viel Geld sparen. Um das richtige Gleichgewicht zwischen dem automatischen Herunterfahren von VMs und der Verwendung von reservierten Instanzen zu finden, sind viel Erfahrung und sorgfältige Analysen erforderlich.
- **Effektive Verwendung der Automatisierung.** Viele Workloads müssen nicht jeden Tag ausgeführt werden. Selbst wenn Sie eine VM nur vier Stunden pro Tag abschalten, können Sie 15 % Kosten sparen. Die Automatisierung amortisiert sich sehr schnell.
- **Verwenden von Ressourcentags für mehr Transparenz.** Wie in diesem Artikel bereits ausgeführt, ermöglicht die Verwendung von Ressourcentags eine bessere Kostenanalyse.

Das Kostenmanagement ist eine Fachrichtung, die für die effektive und effiziente Ausführung einer öffentlichen Cloud von entscheidender Bedeutung ist. Erfolgreiche Unternehmen sind in der Lage, ihre Kosten zu kontrollieren und auf den tatsächlichen Bedarf abzustimmen, statt im Übermaß Ressourcen zu erwerben und zu hoffen, dass sich der Bedarf schon einstellen wird.

## <a name="automate"></a>Automatisieren

Einer der vielen Aspekte, mit denen sich der Reifegrad von Organisationen bemessen lässt, die mit Cloudanbietern arbeiten, ist das eingesetzte Maß an Automatisierung. Die Automatisierung ist fortwährender, endloser Prozess und ein Bereich, für dessen Aufbau Sie Ressourcen und Zeit investieren müssen, wenn Ihre Organisation in die Cloud wechselt. Sie erfüllt viele Zwecke, beispielsweise eine konsistente Zuweisung von Ressourcen zur Lösung von Problemen (hier ist die Automatisierung eng mit einem weiteren grundlegenden Gerüstkonzept verzahnt: Vorlagen und DevOps). Die Automatisierung ist das „Bindegewebe“ des Azure-Gerüsts und vernetzt die einzelnen Bereiche miteinander.

Ihnen steht eine Vielzahl von Tools zur Verfügung – von Erstanbietertools wie Azure Automation, Event Grid und Azure CLI bis hin zu einer umfangreichen Menge an Drittanbietertools wie Terraform, Jenkins, Chef und Puppet. Zu den wichtigsten Automatisierungstools gehören Azure Automation, Event Grid und die Azure Cloud Shell.

- **Azure Automation**: Mit dieser cloudbasierten Funktion können Sie Runbooks erstellen (in PowerShell oder Python) und damit Prozesse automatisieren, Ressourcen konfigurieren und sogar Patches aufspielen. [Azure Automation](/azure/automation/automation-intro) bietet eine umfangreiche Palette an plattformübergreifenden Funktionen, die von großer Bedeutung für Ihre Bereitstellung sind, aber aufgrund ihrer Vielzahl hier nicht im Detail erläutert werden können.
- **Event Grid**: Dabei handelt es sich um ein vollständig verwaltetes Ereignisroutingsystem, mit dem Sie auf Ereignisse in Ihrer Azure-Umgebung reagieren können. So wie Azure Automation das Bindegewebe weit entwickelter Cloudorganisationen ist, stellt [Event Grid](/azure/event-grid) das Bindegewebe einer guten Automatisierungslösung dar. Mit Event Grid können Sie eine einfache serverlose Aktion erstellen, die bei jeder Erstellung einer neuen Ressource eine E-Mail an einen Administrator sendet und diese Ressource in einer Datenbank protokolliert. Event Grid kann Sie auch benachrichtigen, wenn eine Ressource gelöscht wurde, und das Element aus der Datenbank entfernen.
- **Azure Cloud Shell**: Dies ist eine interaktive, browserbasierte [Shell](/azure/cloud-shell/overview) für die Verwaltung von Ressourcen in Azure. Sie stellt eine vollständige Umgebung für PowerShell oder Bash bereit, die nach Bedarf gestartet (und für Sie verwaltet) wird, sodass Sie eine konsistente Umgebung erhalten, in der Sie Ihre Skripts ausführen können. Die Azure Cloud Shell bietet Zugriff auf weitere wichtige und bereits installierte Tools zum Automatisieren Ihrer Umgebung: [Azure CLI](/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), [Terraform](/azure/virtual-machines/linux/terraform-install-configure) sowie eine ständig wachsende Liste zusätzlicher [Tools](https://azure.microsoft.com/updates/cloud-shell-new-cli-tools-and-font-size-selection), mit denen Sie Container, Datenbanken (sqlcmd) und vieles mehr verwalten können.

Die Automatisierung ist ein Vollzeitjob und wird sehr schnell zu einer der wichtigsten operativen Aufgaben in Ihrem Cloudteam. Organisationen, die die Automatisierung in den Vordergrund stellen, sind erfolgreicher bei der Verwendung von Azure:

- **Kostenverwaltung:** Organisationen suchen aktiv nach Möglichkeiten und nutzen die Automatisierung, um die Größen ihrer Ressourcen anzupassen, Ressourcen hoch- oder herunterzuskalieren und nicht genutzte Ressourcen zu deaktivieren.
- **Operative Flexibilität:** Mit der Automatisierung (sowie durch Nutzung von Vorlagen und DevOps-Verfahren) erzielen Sie ein Maß an Wiederholbarkeit, das die Verfügbarkeit steigert, die Sicherheit erhöht und es Ihrem Team ermöglicht, sich auf das Lösen von geschäftlichen Problemen zu konzentrieren.

## <a name="templates-and-devops"></a>Vorlagen und DevOps

Wie im Abschnitt zur Automatisierung beschrieben, sollte es das Ziel Ihrer Organisation sein, Ressourcen mithilfe von Vorlagen und Skripts mit Quellcodeverwaltung bereitzustellen und interaktive Konfigurationsaktivitäten in Ihren Umgebungen so weit wie möglich zu reduzieren. Dieser „Infrastruktur als Code“-Ansatz sowie ein strikter DevOps-Prozess für Continuous Deployment kann die Konsistenz sicherstellen und Abweichungen zwischen Ihren Umgebungen minimieren. Nahezu jede Azure-Ressource lässt sich über [Azure Resource Manager und JSON-Vorlagen](/azure/azure-resource-manager/resource-group-template-deploy) bereitstellen – in Kombination mit PowerShell oder der plattformübergreifenden Azure CLI und Tools wie Terraform von HashiCorp (mit erstklassigem Support und Integration in die Azure Cloud Shell).

In Artikeln wie [Best Practices für die Verwendung von Azure Resource Manager-Vorlagen](/archive/blogs/mvpawardprogram/azure-resource-manager) finden Sie eine hervorragende Erörterung von bewährten Methoden und Erfahrungswerten bei der Anwendung von DevOps-Verfahren auf Azure Resource Manager-Vorlagen mit der [Azure DevOps](/azure/devops/user-guide/?view=vsts)-Toolkette. Investieren Sie in den Zeit- und Arbeitsaufwand, der notwendig ist, um einen grundlegenden Satz an Vorlagen zu entwickeln, die genau auf die Anforderungen Ihrer Organisation zugeschnitten sind. Entwickeln Sie außerdem Continuous Delivery-Pipelines mit DevOps-Toolketten (z.B. Azure DevOps, Jenkins, Bamboo, TeamCity und Concourse) speziell für Ihre Produktions- und QA-Umgebungen. Auf GitHub finden Sie eine umfangreiche Bibliothek mit [Azure-Schnellstartvorlagen](https://github.com/azure/azure-quickstart-templates), die Sie als Ausgangspunkt für Ihre eigenen Vorlagen verwenden können – so können Sie mit Azure DevOps im Handumdrehen cloudbasierte Bereitstellungspipelines erstellen.

Beherzigen Sie diese Best Practices: Für Produktionsabonnements oder Ressourcengruppen sollte Ihr Ziel immer sein, RBAC-basierte Sicherheitsfunktionen zu verwenden, um interaktive Benutzer standardmäßig zu deaktivieren. Nutzen Sie zudem auf Dienstprinzipalen basierende automatisierte Continuous Delivery-Pipelines, um sämtliche Ressourcen und den gesamten Anwendungscode bereitzustellen. Administratoren oder Entwickler sollten niemals das Azure-Portal verwenden, um Ressourcen interaktiv zu konfigurieren. DevOps auf diesem Level erfordert gemeinsame Anstrengungen und nutzt alle Konzepte des Azure-Gerüsts. So können Sie für eine konsistente und geschützte Umgebung sorgen, die die Skalierungsanforderungen Ihrer Organisation erfüllt.

> [!TIP]
> Verwenden Sie [verknüpfte Vorlagen](/azure/azure-resource-manager/resource-group-linked-templates), wenn Sie komplexe Azure Resource Manager-Vorlagen entwerfen und entwickeln, um komplexe Ressourcenbeziehungen anhand von monolithischen JSON-Dateien zu organisieren und neu zu gestalten. So können Sie Ressourcen einzeln verwalten, und Ihre Vorlagen lassen sich besser lesen, testen und wiederverwenden.

Azure ist ein Hyperscale-Cloudanbieter. Wenn Sie bei der Umstellung Ihrer Organisation von der Welt der lokalen Server auf die Cloud die gleichen Konzepte befolgen wie Cloudanbieter und Anbieter von SaaS-Anwendungen, ermöglicht Azure es Ihnen, auf effizientere Weise auf geschäftliche Anforderungen zu reagieren.

## <a name="core-network"></a>Kernnetzwerk

Die letzte Komponente des Azure-Gerüsts ist von entscheidender Bedeutung, wenn es darum geht, wie Ihre Organisation sicher auf Azure zugreifen kann. Der Zugriff auf Ressourcen kann intern (innerhalb des Unternehmensnetzwerks) oder extern (über das Internet) erfolgen. Für Benutzer in Ihrer Organisation ist es einfach, versehentlich Ressourcen an der falschen Stelle zu platzieren und so böswilligen Zugriff darauf zu ermöglichen. Wie bei lokalen Geräten müssen Unternehmen die entsprechende Kontrolle implementieren, um sicherzustellen, dass Azure-Benutzer die richtigen Entscheidungen treffen. Für die Abonnementgovernance wurden Hauptressourcen identifiziert, die eine grundlegende Kontrolle des Zugriffs bieten. Zu diesen Hauptressourcen gehören:

- **Virtuelle Netzwerke** sind Containerobjekte für Subnetze. Obwohl dies nicht zwingend notwendig ist, werden sie häufig beim Verbinden von Anwendungen mit internen Unternehmensressourcen verwendet.
- **Benutzerdefinierte Routen** ermöglichen es Ihnen, die Routingtabelle in einem Subnetz zu bearbeiten, sodass Sie Datenverkehr über ein virtuelles Netzwerkgerät oder an ein Remotegateway in einem virtuellen Peernetzwerk senden können.
- **Peering virtueller Netzwerke** ermöglicht es Ihnen, zwei oder mehr virtuelle Netzwerke in Azure nahtlos miteinander zu verbinden und so komplexere Hub-and-Spoke-Entwürfe oder Netzwerke für gemeinsame Dienste zu erstellen.
- **Dienstendpunkte.** In der Vergangenheit nutzten PaaS-Dienste verschiedene Methoden zum Sichern des Zugriffs auf diese Ressourcen aus Ihren virtuellen Netzwerken. Mit Dienstendpunkten können Sie den Zugriff auf aktivierte PaaS-Dienste **nur** auf verbundene Endpunkte beschränken und so die Sicherheit insgesamt erhöhen.
- **Sicherheitsgruppen** sind umfassende Regelsätze, mit denen Sie eingehenden und ausgehenden Datenverkehr an und aus Azure-Ressourcen zulassen oder verweigern können. [Sicherheitsgruppen](/azure/virtual-network/security-overview) bestehen aus Sicherheitsregeln, die mit Folgendem erweitert werden können: **Diensttags** (die häufig verwendete Azure-Dienste wie Azure Key Vault oder Azure SQL-Datenbank definieren) und **Anwendungsgruppen** (die eine Anwendungsstruktur definieren, wie z.B. Web- und App-Server).

> [!TIP]
> Verwenden Sie dazu Diensttags und Anwendungssicherheitsgruppen in Ihren Netzwerksicherheitsgruppen:
>
> - Verbessern Sie die Lesbarkeit Ihrer Regeln, was für das Verständnis der Auswirkungen entscheidend ist.
> - Ermöglichen Sie eine effektive Mikrosegmentierung innerhalb eines größeren Subnetzes, wodurch die Ausdehnung verringert und die Flexibilität erhöht wird.

<!-- TODO: Refactor VDC content below. -->
<!-- docsTest:ignore "Azure Virtual Datacenter" -->

### <a name="azure-virtual-datacenter"></a>Virtuelles Azure-Rechenzentrum

Azure bietet sowohl interne Funktionen als auch Drittanbieterfunktionen aus unserem umfangreichen Partnernetzwerk, die eine effektive Verstärkung Ihrer Sicherheitsposition ermöglichen. Wichtiger noch: Microsoft stellt Ihnen über das [virtuelle Azure-Rechenzentrum (VDC)](./networking-vdc.md) Best Practices und Leitfäden zur Verfügung. Wenn Sie nicht mehr nur eine einzelne Workload, sondern mehrere Workloads verwalten, die Hybridfunktionen nutzen, erhalten Sie mit den Leitfäden aus diesem Rechenzentrum sozusagen das Rezept, mit dem Sie ein flexibles Netzwerk aufbauen können, das mit Ihren Workloads in Azure wächst.

## <a name="next-steps"></a>Nächste Schritte

Governance ist entscheidend für den Erfolg von Azure. In diesem Artikel wird die technische Implementierung eines Unternehmensgerüsts behandelt, auf den umfassenden Prozess und die Beziehungen zwischen den Komponenten wird jedoch nur am Rande eingegangen. Die Richtliniengovernance verläuft von oben nach unten und richtet sich danach, was das Unternehmen erreichen möchte. Natürlich sind beim Erstellen eines Governancemodells für Azure Vertreter aus der IT beteiligt, wichtiger jedoch ist eine nachhaltige Unterstützung durch Führungskräfte von Unternehmensgruppen sowie aus dem Bereich Sicherheits- und Risikomanagement. Bei einem Unternehmensgerüst geht es letztlich um die Minderung von Unternehmensrisiken, um Mission und Ziele der Organisation zu fördern.

Nachdem Sie sich mit der Abonnementgovernance vertraut gemacht haben, ist es an der Zeit, diese Empfehlungen in der Praxis zu erleben. Weitere Informationen finden Sie unter [Bewährte Methoden für die Azure-Bereitschaft](../ready/azure-best-practices/index.md).
