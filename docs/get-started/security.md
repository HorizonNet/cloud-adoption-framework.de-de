---
title: 'Erste Schritte: Sichern der Unternehmensumgebung'
description: Beginnen Sie mit der Integration der Sicherheit an kritischen Punkten während der Einführung und des Betriebs der Cloud.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 1c9a2faf35a2137e5dd04c23a8cb49c6dd02f5b5
ms.sourcegitcommit: 4da8118cdac560b795d2d413974c85c49b3189fa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2020
ms.locfileid: "90681001"
---
# <a name="get-started-implement-security-across-the-enterprise-environment"></a>Erste Schritte: Implementieren von Sicherheit in der gesamten Unternehmensumgebung

Sicherheit trägt dazu bei, die Vertraulichkeit, Integrität und Verfügbarkeit für ein Unternehmen zu gewährleisten. Sicherheitsmaßnahmen konzentrieren sich in erster Linie auf den Schutz vor potenziellen Auswirkungen auf Vorgänge, die durch interne und externe böswillige und unbeabsichtigte Handlungen verursacht werden.

Dieser Leitfaden zu den ersten Schritten beschreibt die wichtigsten Schritte, mit denen das Geschäftsrisiko durch Cybersicherheitsangriffe gemindert oder vermieden werden kann. Er unterstützt Sie beim schnellen Einrichten wesentlicher Sicherheitspraktiken in der Cloud und dem Integrieren von Sicherheit in Ihren Cloudeinführungsprozess.

Die Schritte in diesem Leitfaden sind für alle Rollen gedacht, die die Sicherheitsgewährleistung für Cloudumgebungen und Zielzonen unterstützen. Zu den Aufgaben gehören unmittelbare Prioritäten bei der Risikominderung, Leitlinien für den Aufbau einer modernen Sicherheitsstrategie, die Operationalisierung des Ansatzes und die Umsetzung dieser Strategie.

Dieser Leitfaden enthält Elemente aus dem gesamten Microsoft Cloud Adoption Framework für Azure:

![Erste Schritte mit der Unternehmenssicherheit](../_images/get-started/security-map.png)

Wenn Sie den Schritten in diesem Leitfaden folgen, können Sie die Sicherheit an wichtigen Punkten in den Prozess integrieren. Ziel ist es, Hindernisse bei der Cloudeinführung zu vermeiden und unnötige Störungen des Geschäftsbetriebs oder der Betriebsabläufe zu reduzieren.

Microsoft hat Funktionen und Ressourcen entwickelt, mit denen Sie die Implementierung dieses Sicherheitsleitfadens in Microsoft Azure beschleunigen können. Auf diese Ressourcen wird innerhalb des Leitfadens verwiesen. Sie sollen Ihnen bei der Einrichtung, Überwachung und Durchsetzung von Sicherheit helfen und werden regelmäßig aktualisiert und überarbeitet.

Das folgende Diagramm zeigt einen ganzheitlichen Ansatz für die Verwendung von Sicherheitsanleitungen und Plattformtools, um Sicherheitstransparenz und Kontrolle über Ihre Cloudressourcen in Azure herzustellen. Dieser Ansatz wird empfohlen.

![Sicherheitsdiagramm](../_images/security/security-diagram.png)

Verwenden Sie diese Schritte zum Planen und Ausführen Ihrer Strategie zur Sicherung Ihrer Cloudressourcen und zur Nutzung der Cloud für die Modernisierung der Sicherheitsabläufe.

## <a name="step-1-establish-essential-security-practices"></a>Schritt 1: Einrichten wichtiger Sicherheitsverfahren

Sicherheit in der Cloud beginnt mit soliden Praktiken. Unabhängig davon, ob Sie bereits in der Cloud arbeiten oder eine zukünftige Einführung planen, ist es wichtig, schnell grundlegende Sicherheitspraktiken einzurichten.

Zusätzlich zur Erfüllung aller expliziten gesetzlichen Complianceanforderungen empfehlen wir die folgenden Schritte, um die größten Sicherheitsherausforderungen anzugehen, mit denen die meisten Unternehmen beim Umstieg auf die Cloud konfrontiert sind.

**Zielvorgaben und unterstützende Anleitungen:**

- **Technisch:** Mindern von Hauptrisiken und Erhöhen der Sichtbarkeit und Kontrolle von Ressourcen durch die Aktivierung von kennwortloser oder mehrstufiger Authentifizierung für Administratoren und durch Aktivieren des Bedrohungsschutzes für Cloudressourcen.

  - [Kennwortlose oder mehrstufige Authentifizierung für Administratoren](/azure/architecture/framework/security/critical-impact-accounts#passwordless-or-multi-factor-authentication-for-admins)
  - [Sicherheitsvorgänge](/azure/architecture/framework/security/security-operations) und [Bedrohungsschutz in Azure Security Center](/azure/security-center/threat-protection)

- **Vorgehensweise:** Ermöglichen schneller Sicherheitsentscheidungen und kontinuierlicher Verbesserung durch die Zuweisung von Sicherheitsrollen und -verantwortlichkeiten und durch die Einrichtung eines Prozesses zur Reaktion auf Incidents.

  - [Klare Verantwortlichkeiten](/azure/architecture/framework/security/governance#clear-lines-of-responsibility), [Zuweisen von Berechtigungen zum Verwalten der Umgebung](/azure/architecture/framework/security/governance#assign-privileges-for-managing-the-environment) und Operationalisieren von Sicherheitsbewertungen <!-- TODO: Improve this and add link to AAF article -->
  - Sicherheitsrollen und Zuständigkeiten <!-- TODO: add link to bookmark -->
  - [Referenzleitfaden für die Reaktion auf Vorfälle](https://aka.ms/irrg)

- **Personen**: Bereitstellung von Schulungen, Tools und Zugangsmöglichkeiten für Sicherheitsteams, die für eine erfolgreiche Bereitstellung und den Betrieb während des Übergangs zur Cloudumgebung erforderlich sind.

  - **Informieren aller Beteiligten über Konzepte**, wie sich Cloud und Cloudsicherheit weiterentwickeln:
    - [Entwicklung der Bedrohungsumgebung, von Rollen und digitalen Strategien](/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
    - [Transformation von Sicherheit, Strategien, Tools und Bedrohungen](/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
  - **Schulen technischer Mitarbeiter** bezüglich technischer Details der Cloudsicherheitsfunktionen für die verwendeten Plattformen. Microsoft bietet umfassende [Azure-Sicherheitsdokumentation](/azure/security).

- **Langfristige architektonische Entscheidungen:** Einrichten einer langfristigen Grundlage, um die richtigen Entscheidungen zu treffen. Es ist schwierig und teuer, diese Grundlage später zu ändern.

  - [Aufbau einer Unternehmenssegmentierungsstrategie und Anpassung der technischen Architekturen an diese Strategie (Netzwerksegmentierung, Identitätssegmentierung usw.)](/azure/architecture/framework/security/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)
  - [Einzelnes Unternehmensverzeichnis](/azure/architecture/framework/security/design-identity#use-a-single-enterprise-directory)
  - [Authentifizierungsstrategie für Dienste](/azure/architecture/framework/security/applications-services#prefer-identity-authentication-over-keys)
  - [Berechtigungszuweisungsstrategie](/azure/architecture/framework/security/critical-impact-accounts#avoid-granular-and-custom-permissions)

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudsicherheitsteam <br><br><br> | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

In diesem ersten Schritt sollten die Governanceteams auch damit beginnen, die Schaffung von Sicherheitsgrundlinien zu koordinieren, die in allen Umgebungen überwacht, verwaltet und durchgesetzt werden können. Weitere Anleitungen zu dieser Einrichtung finden Sie später in Schritt 4.

> [!NOTE]
> Jede Organisation sollte ihre eigenen Mindeststandards definieren. Der Risikostatus und die anschließende Risikotoleranz können je nach Branche, Kultur und anderen Faktoren stark variieren. Beispielsweise könnte eine Bank selbst bei einem geringfügigen Angriff auf ein Testsystem eine mögliche Rufschädigung nicht tolerieren. Einige Organisationen würden dieses Risiko gerne in Kauf nehmen, wenn dadurch ihre digitale Transformation um drei bis sechs Monate beschleunigt würde.

## <a name="step-2-modernize-the-security-strategy"></a>Schritt 2: Modernisieren der Sicherheitsstrategie

Effektive Sicherheit in der Cloud erfordert eine Strategie, die die aktuelle Bedrohungsumgebung und die Art der Cloudplattform widerspiegelt, auf der die Unternehmensressourcen gehostet werden. Eine klare Strategie verbessert die Bemühungen aller Teams, eine sichere und nachhaltige Unternehmenscloudumgebung bereitzustellen. Die Sicherheitsstrategie muss definierte Geschäftsergebnisse ermöglichen, das Risiko auf ein akzeptables Maß reduzieren und Mitarbeiter in die Lage versetzen, produktiv zu sein.

Eine Cloudsicherheitsstrategie stellt allen Teams, die an der Technologie, den Prozessen und der Bereitschaft der Mitarbeiter für diese Einführung arbeiten, Anleitungen bereit. Die Strategie sollte über die Cloudarchitektur und die technischen Fähigkeiten informieren, die Sicherheitsarchitektur und -fähigkeiten lenken und die Ausbildung und Schulung von Teams beeinflussen.

**Ziele:**

Der Strategieschritt sollte zu einem Dokument führen, das leicht an viele Beteiligte innerhalb der Organisation vermittelt werden kann. Zu den Beteiligten können auch Führungskräfte im Führungsteam der Organisation gehören.

Wir empfehlen, die Strategie in einer Präsentation festzuhalten, um eine einfache Diskussion und Aktualisierung zu ermöglichen. Diese Präsentation kann je nach Kultur und Vorlieben durch ein Dokument unterstützt werden.

- **Strategiepräsentation:** Möglicherweise verwenden Sie eine einzige Strategiepräsentation. Sie können aber auch zusammenfassende Versionen für Führungszielgruppen erstellen.

  - **Vollständige Präsentation:** Diese sollte den vollständigen Satz von Elementen für die Sicherheitsstrategie in der Hauptpräsentation oder in optionalen Referenzfolien enthalten.
  - **Executive-Zusammenfassungen:** Versionen zur Verwendung für Führungskräfte und Vorstandsmitglieder enthalten möglicherweise nur kritische Elemente, die für deren Rolle relevant sind, etwa Risikobereitschaft, höchste Prioritäten oder akzeptierte Risiken.

- Sie können auch Motivationen, Ergebnisse und geschäftliche Begründungen in der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) aufzeichnen.

**Bewährte Methoden für das Entwickeln einer Sicherheitsstrategie:**

Erfolgreiche Programme integrieren diese Elemente in ihren Sicherheitsstrategieprozess:

- **Enge Ausrichtung an Geschäftsstrategie:** Die Aufgabe von Sicherheit ist der Schutz des Geschäftswerts. Es ist entscheidend, alle Sicherheitsbemühungen auf diesen Zweck auszurichten und interne Konflikte zu minimieren.

  - **Schaffen eines gemeinsamen Verständnisses** von geschäftlichen, IT- und Sicherheitsanforderungen.
  - **Frühzeitige Integration von Sicherheit in die Cloudeinführung**, um Krisen in letzter Minute aufgrund vermeidbarer Risiken zu verhindern.
  - **Verwenden eines agilen Ansatzes**, um sofort Mindestsicherheitsanforderungen festzulegen und die Sicherheitsgarantien im Laufe der Zeit kontinuierlich zu verbessern.
  - **Fördern einer Änderung der Sicherheitskultur** durch absichtliche proaktive Führungsaktionen.

  Weitere Informationen finden Sie unter [Transformationen, Denkrichtungen und Erwartungen](../strategy/define-security-strategy.md#transformations-mindsets-and-expectations).

- **Modernisieren der Sicherheitsstrategie:** Die Sicherheitsstrategie sollte Überlegungen zu allen Aspekten des modernen technologischen Umfelds, der aktuellen Bedrohungslandschaft und der Ressourcen der Sicherheitscommunity beinhalten.

  - Anpassen an das Modell für die gemeinsame Verantwortlichkeit der Cloud.
  - Einbeziehen aller Cloudtypen und Bereitstellungen in mehreren Clouds.
  - Bevorzugen nativer Cloudsteuerelemente, um unnötige und schädliche Reibung zu vermeiden.
  - Integrieren der Sicherheitscommunity, um mit dem Tempo der Weiterentwicklung bei Angreifern Schritt zu halten.

**Verwandte Ressourcen für zusätzlichen Kontext:**

- [Entwicklung der Bedrohungsumgebung, von Rollen und digitalen Strategien](/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)

- [Transformation von Sicherheit, Strategien, Tools und Bedrohungen](/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)

- Strategieüberlegungen für das Cloud Adoption Framework:

  - [Modernisieren Ihrer Sicherheitsstrategie](../strategy/define-security-strategy.md#modernize-your-security-strategy)
  - [Resilienz bei der Cybersicherheit](../strategy/define-security-strategy.md#cybersecurity-resilience)
  - [Ändern der Sicherheitsbeziehungen und Verantwortlichkeiten durch die Cloud](../strategy/define-security-strategy.md#how-the-cloud-is-changing-security)

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Führungsteam für Sicherheit (Chief Information Security Officer (CISO) oder gleichwertig) | <li> Cloudstrategieteam <li> Cloudsicherheitsteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

**Genehmigung der Strategie:**

Führungskräfte und Geschäftsleiter mit Rechenschaftspflicht für Ergebnisse oder Risiken der Geschäftsbereiche innerhalb der Organisation sollten diese Strategie genehmigen. Diese Gruppe kann je nach Organisation den Vorstand einschließen.

## <a name="step-3-develop-a-security-plan"></a>Schritt 3: Entwickeln Sie einen Sicherheitsplan.

Die Planung setzt die Sicherheitsstrategie in die Tat um, indem sie Ergebnisse, Meilensteine, Zeitpläne und Aufgabenträger definiert. In diesem Plan werden auch die Rollen und Zuständigkeiten der Teams erläutert.

Sicherheitsplanung und Planung der Cloudbereitstellung sollten nicht isoliert voneinander durchgeführt werden. Es ist von entscheidender Bedeutung, das Cloudsicherheitsteam frühzeitig in die Planungszyklen einzubinden, um zu vermeiden, dass Arbeitsunterbrechungen oder erhöhte Risiken durch zu spät erkannte Sicherheitsprobleme auftreten. Die Sicherheitsplanung funktioniert am besten mit fundiertem Wissen und Bewusstsein über den digitalen Bestand und das vorhandene IT-Portfolio, das durch die vollständige Integration in den Cloudplanungsprozess entsteht.

**Zielvorgaben:**

- **Systemsicherheitsplan:** Ein Sicherheitsplan sollte Teil der Hauptplanungsdokumentation für die Cloud sein. Dabei kann es sich um ein Dokument handeln, das die [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx), einen detaillierten Foliensatz oder eine Projektdatei verwendet. Je nach Größe, Kultur und Standardmethoden der Organisation kann es auch eine Kombination dieser Formate sein.

  Der Sicherheitsplan sollte alle diese Elemente enthalten:

  - **Plan für Organisationsfunktionen**, damit die Teams wissen, wie sich die derzeitigen Sicherheitsrollen und -verantwortlichkeiten mit dem Umstieg auf die Cloud verändern werden.

  - **Sicherheitskompetenzplan**, um die Teammitglieder bei der Bewältigung der bedeutenden Veränderungen in Technologie, Rollen und Verantwortlichkeiten zu unterstützen.

  - **Roadmap für technische Sicherheitsarchitektur und -funktionen** als Leitfaden für technische Teams.

    Microsoft stellt Referenzarchitekturen und Technologiefunktionen zur Verfügung, die Sie beim Erstellen Ihrer Architektur und Roadmap unterstützen:

    - [Azure-Komponenten und -Referenzmodell](/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151), um die Planung und den Entwurf von Azure-Sicherheitsrollen zu beschleunigen.

      ![Azure-Verwaltungsmodell](../_images/security/azure-administration-model.png)

      ![Azure RBAC-Modell](../_images/security/azure-rbac-model.png)

    - [Cybersicherheits-Referenzarchitektur von Microsoft](https://aka.ms/mcra) zum Aufbau einer Cybersicherheitsarchitektur für ein hybrides Unternehmen, das sowohl lokale als auch Cloudressourcen umfasst.

    - [SOC-Referenzarchitektur (Security Operations Center)](/security/compass/security-operations-videos-and-decks#part-1-introduction---soc-learnings-strategies-and-technical-integration-2430) zur Modernisierung der Sicherheitserkennung, -reaktion und -wiederherstellung.

    - [Zero-Trust-Referenzarchitektur für Benutzerzugriff](/security/ciso-workshop/ciso-workshop-module-3#part-5-zero-trust-user-access-reference-architecture-842) zur Modernisierung der Zugriffssteuerungsarchitektur für Cloudgenerierung.

    - [Azure Security Center](/azure/security-center) und [Microsoft Cloud Application Security](/cloud-app-security) als Hilfe beim Schützen von Cloudressourcen.

  - **Sicherheitsbewusstsein und Schulungsplan**, damit alle Teams über wichtige grundlegende Sicherheitskenntnisse verfügen.

  - **Kennzeichnung der Ressourcensensitivität** zur Bestimmung sensibler Ressourcen mithilfe einer Taxonomie, die sich an den Auswirkungen auf das Geschäft orientiert. Die Taxonomie wird gemeinsam von Geschäftsbeteiligten, Sicherheitsteams und anderen interessierten Parteien erstellt.

  - **Sicherheitsänderungen am Cloudplan:** Aktualisierung anderer Abschnitte des Cloudeinführungsplans, um die durch den Sicherheitsplan ausgelösten Änderungen zu berücksichtigen.

**Bewährte Methoden für Sicherheitsplanung:**

Ihr Sicherheitsplan ist wahrscheinlich erfolgreicher, wenn die Planung den folgenden Ansatz verwendet:

- **Annehmen einer Hybridumgebung:** Dazu zählen SaaS-Anwendungen (Software-as-a-Service) und lokale Umgebungen. Es umfasst auch mehrere IaaS-Anbieter (Infrastructure-as-a-Service) und ggf. PaaS-Anbieter (Platform-as-a-Service).

- **Einführung agiler Sicherheit:** Einrichten von Mindestsicherheitsanforderungen als erstes und Verschieben aller nichtkritischen Punkte in eine priorisierte Liste der nächsten Schritte. Dies sollte kein herkömmlicher detaillierter Plan für 3 bis 5 Jahre sein. Die Cloud und die Bedrohungsumgebung ändern sich zu schnell, als dass diese Art von Plan sinnvoll wäre. Der Plan sollte sich auf die Entwicklung der Anfangsschritte und des Endzustands konzentrieren:

  - **Schnelle Erfolge** für die unmittelbare Zukunft, die eine hohe Wirkung erzielen, bevor längerfristige Initiativen beginnen. Dieser Zeitrahmen kann je nach Organisationskultur, Standardverfahren und anderen Faktoren 3 bis 12 Monate umfassen.
  - **Klare Vision** des gewünschten Endzustands als Leitfaden für den Planungsprozess jedes Teams (das Erreichen dieses Ziels kann mehrere Jahre dauern).

- **Umfassende Verbreitung des Plans:** Verstärken des Bewusstseins, des Feedbacks und der Unterstützung durch Projektbeteiligte.

- **Erreichen der strategischen Ergebnisse:** Sicherstellen, dass Ihr Plan die in der Sicherheitsstrategie beschriebenen strategischen Ergebnisse ermöglicht und erfüllt.

- **Festlegen von Besitzrecht, Verantwortlichkeit und Fristen:** Sicherstellen, dass die Verantwortlichen für jede Aufgabe ermittelt werden und sich verpflichten, diese Aufgabe in einem bestimmten Zeitrahmen zu erledigen.

- **Berücksichtigen der menschlichen Seite von Sicherheit:** Einbinden von Menschen während dieses Zeitraums der Transformation und neuer Erwartungen durch:

  - **Aktives Unterstützen der Transformation der Teammitglieder** durch klare Kommunikation und Coaching zu den folgenden Themen:
    - Welche Fähigkeiten erlernt werden müssen.
    - Warum die Fähigkeiten erlernt werden müssen (und die damit verbundenen Vorteile).
    - Wie diese Kenntnisse erworben werden (und Ressourcen bereitgestellt werden, um den Kenntniserwerb zu unterstützen).

    Sie können den Plan mithilfe der [Strategie- und Planungsvorlage](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/plan/cloud-adoption-framework-strategy-and-plan-template.docx) dokumentieren. Sie können die Ausbildung Ihrer Teammitglieder auch durch das [Onlinesicherheitstraining von Microsoft](/security/compass/microsoft-security-compass-introduction) unterstützen.

  - **Sorgen für Sicherheitsbewusstsein**, um den Menschen dabei zu helfen, eine echte Verbindung zu ihrem Anteil an der Sicherheit der Organisation herzustellen.

- **Vertrautmachen mit Microsoft-Erkenntnissen und -Anleitungen:** Microsoft hat Einblicke und Perspektiven veröffentlicht, um Ihrer Organisation bei der Planung der Umstellung auf die Cloud und einer modernen Sicherheitsstrategie zu helfen. Das Material umfasst aufgezeichnete Schulungen, Dokumentationen und bewährte Sicherheitsmethoden sowie empfohlene Standards.

  Technische Anleitungen für die Erstellung Ihres Plans und Ihrer Architektur finden Sie in der [Microsoft-Sicherheitsdokumentation](/security).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudsicherheitsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Alle Risikoteams in Ihrer Organisation <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

**Genehmigung des Sicherheitsplans:**

Das Sicherheitsführungsteam (CISO oder Äquivalent) sollte den Plan genehmigen.

## <a name="step-4-secure-new-workloads"></a>Schritt 4: Sichern neuer Workloads

Es ist viel einfacher, in einem sicheren Zustand zu beginnen, als die Sicherheit später in Ihrer Umgebung nachzurüsten. Wir empfehlen dringend, mit einer sicheren Konfiguration zu beginnen, um sicherzustellen, dass Workloads in eine sichere Umgebung migriert und dort entwickelt und getestet werden.

Während der Implementierung der [Zielzone](../ready/landing-zone/index.md) können sich viele Entscheidungen auf Sicherheits- und Risikoprofile auswirken. Das Cloudsicherheitsteam sollte die Konfiguration der Zielzone überprüfen, um sicherzustellen, dass sie den Sicherheitsstandards und -anforderungen der Sicherheitsbaselines Ihrer Organisation entspricht.

**Ziele:**

- Stellen Sie sicher, dass neue Zielzonen die Compliance- und Sicherheitsanforderungen der Organisation erfüllen.

**Hinweis zur Erreichung der Ziele:**

- **Kombinieren von vorhandener Anforderungen und Cloudempfehlungen:** Beginnen Sie mit den empfohlenen Anleitungen, und passen Sie diese dann an Ihre individuellen Sicherheitsanforderungen an. Bei dem Versuch, lokale Richtlinien und Standards durchzusetzen, sind wir auf Herausforderungen gestoßen, da diese sich oft auf veraltete Technologie oder Sicherheitsansätze beziehen.

  Microsoft hat einen Leitfaden veröffentlicht, der Sie bei der Erstellung Ihrer Sicherheitsbaselines unterstützt:
  - [Azure-Sicherheitsstandards für Strategie und Architektur](/security/compass/compass): Strategie- und Architekturempfehlungen zur Gestaltung der Sicherheitshaltung Ihrer Umgebung.
  - [Vergleichstests für die Azure-Sicherheit:](/azure/security/benchmarks/introduction) Spezifische Konfigurationsempfehlungen zum Sichern von Azure-Umgebungen.
  - [Azure-Sicherheitsbaselinetraining](/learn/modules/create-security-baselines).

- **Bereitstellen von Schutzmaßnahmen:** Schutzmaßnahmen sollten die automatisierte Überwachung und Durchsetzung von Richtlinien umfassen. Für diese neuen Umgebungen sollten die Teams bestrebt sein, die Sicherheitsbaselines der Organisation sowohl zu prüfen als auch durchzusetzen. Diese Maßnahmen können dabei helfen, Sicherheitsüberraschungen während der Entwicklung sowie die Continuous Integration und Continuous Deployment (CI/CD) von Workloads zu minimieren.

  Microsoft bietet verschiedene native Funktionen in Azure, um dies zu ermöglichen:
  - [Secure Score](/azure/security-center/secure-score-security-controls): Verwenden Sie eine gewichtete Bewertung Ihres Azure-Sicherheitsstatus, um die Sicherheitsmaßnahmen und -projekte in Ihrer Organisation nachzuverfolgen.
  - [Azure Blueprints](/azure/governance/blueprints/overview): Cloudarchitekten und zentrale IT-Gruppen können eine wiederholbare Gruppe von Azure-Ressourcen definieren, mit der die Standards, Muster und Anforderungen einer Organisation implementiert und erzwungen werden.
  - [Azure Policy](/azure/governance/policy): Dies ist die Grundlage der Sichtbarkeits- und Steuerungsfunktionen, die von den anderen Diensten verwendet werden. Azure Policy ist in [Azure Resource Manager](/azure/azure-resource-manager) integriert, sodass Sie Änderungen prüfen und Richtlinien für jede Ressource in Azure vor, während oder nach ihrer Erstellung durchsetzen können.
  - [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-security.md): Verwenden Sie bewährte Methoden zur Verbesserung der Sicherheit innerhalb einer Zielzone.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudsicherheitsteam | <li> Cloudeinführungsteam <li> Cloudplattformteam <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

## <a name="step-5-secure-existing-cloud-workloads"></a>Schritt 5: Sichern vorhandener Cloudworkloads

Viele Organisationen haben bereits Ressourcen in Unternehmenscloudumgebungen bereitgestellt, ohne die bewährten Sicherheitsmethoden anzuwenden, was zu einem größeren Geschäftsrisiko führte.

Nachdem Sie sichergestellt haben, dass neue Anwendungen und Zielzone den bewährten Sicherheitsmethoden folgen, sollten Sie sich darauf konzentrieren, vorhandene Umgebungen auf den gleichen Standard zu bringen.

**Ziele:**

- Stellen Sie sicher, dass alle vorhandenen Cloudumgebungen und Zielzonen die Compliance- und Sicherheitsanforderungen der Organisation erfüllen.
- Testen Sie die Betriebsbereitschaft von Produktionsbereitstellungen mithilfe von Richtlinien für Sicherheitsbaselines.
- Überprüfen Sie die Einhaltung der Entwurfsanleitungen und Sicherheitsanforderungen für Sicherheitsbaselines.

**Hinweis zur Erreichung der Ziele:**

- Verwenden Sie die gleichen Sicherheitsbaselines, die Sie in [Schritt 4](#step-4-secure-new-workloads) erstellt haben, als idealen Status. Möglicherweise müssen Sie einige Richtlinieneinstellungen so anpassen, dass sie nur überwacht werden, anstatt sie zu erzwingen.
- Gleichen Sie Betriebs- und Sicherheitsrisiken aus. Da diese Umgebungen möglicherweise Produktionssysteme hosten, die kritische Geschäftsprozesse ermöglichen, müssen Sie Sicherheitsverbesserungen möglicherweise schrittweise implementieren, um das Risiko eines Betriebsausfalls zu vermeiden.
- Priorisieren Sie die Erkennung und Behebung von Sicherheitsrisiken nach geschäftlicher Wichtigkeit. Beginnen Sie mit Workloads, die bei einer Gefährdung eine hohe geschäftliche Auswirkung haben, und Workloads mit einem hohen Risiko.

Weitere Informationen finden Sie unter [Identifizieren und Klassifizieren von unternehmenskritischen Anwendungen](/azure/architecture/framework/security/applications-services#identify-and-classify-business-critical-applications).

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudeinführungsteam <li> Cloudstrategieteam <li> Cloudsicherheitsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT-Abteilung |

## <a name="step-6-govern-to-manage-and-improve-security-posture"></a>Schritt 6: Steuern der Verwaltung und Verbesserung des Sicherheitsstatus

Wie alle modernen Disziplinen ist Sicherheit ein iterativer Prozess, der sich auf kontinuierliche Verbesserung konzentrieren sollte. Der Sicherheitsstatus kann auch verfallen, wenn Organisationen den Fokus darauf im Laufe der Zeit nicht aufrechterhalten.

Die konsequente Anwendung von Sicherheitsanforderungen kommt von soliden Governancedisziplinen und automatisierten Lösungen. Nachdem das Cloudsicherheitsteam die Sicherheitsbaselines definiert hat, sollten diese Anforderungen überprüft werden, um sicherzustellen, dass sie in allen Cloudumgebungen einheitlich angewendet (und ggf. durchgesetzt) werden.

**Ziele:**

- Sicherstellen, dass die Sicherheitsbaselines der Organisation auf alle relevanten Systeme angewendet werden. Überprüfen von Anomalien anhand eines [Secure Score](/azure/security-center/secure-score-security-controls) oder eines ähnlichen Mechanismus.
- Dokumentieren Ihrer Richtlinien, Prozessen und Entwurfsanleitungen für Sicherheitsbaselines in der [Vorlage für die Disziplin „Sicherheitsbaseline“](../govern/security-baseline/template.md).

**Hinweis zur Erreichung der Ziele:**

- Verwenden Sie die gleichen Sicherheitsbaselines und Überwachungsmechanismen, die Sie in [Schritt 4](#step-4-secure-new-workloads) als technische Komponenten zur Überwachung der Baselines erstellt haben. Ergänzen Sie diese Baselines durch Personen- und Prozesssteuerungen, um Konsistenz zu gewährleisten.
- Stellen Sie sicher, dass alle Workloads und Ressourcen die [richtigen Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) befolgen. [Erzwingen Sie Kennzeichnungskonventionen mithilfe von Azure Policy](/azure/governance/policy/tutorials/govern-tags) mit einem speziellen Schwerpunkt auf Tags für „Vertraulichkeit der Daten“.
- Sollten Sie noch nicht mit Cloudgovernance vertraut sein, verwenden Sie die Governancemethodik, um [Governancerichtlinien, -prozesse und -disziplinen](../govern/index.md) einzurichten.

<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudsicherheitsteam <li> Cloudkompetenzzentrum (CCoE) oder zentrales IT-Team |

## <a name="next-steps"></a>Nächste Schritte

Mithilfe der Schritte in dieser Anleitung konnten Sie die Strategien, Steuerungen, Prozesse, Fähigkeiten und Kultur implementieren, die für eine konsistente Verwaltung von Sicherheitsrisiken im gesamten Unternehmen erforderlich sind.

Wenn Sie mit dem Betriebsmodus der Cloudsicherheit fortfahren, sollten Sie diese nächsten Schritte in Betracht ziehen:

- Lesen Sie die [Microsoft-Dokumentation zur Sicherheit](/security). Diese dient als technischer Leitfaden, der Sicherheitsexperten bei der Erstellung und Verbesserung von Strategie, Architektur und priorisierten Roadmaps für Cybersicherheit unterstützt.
- Sehen Sie sich die Sicherheitsinformationen für [integrierte Sicherheitskontrollen für Azure-Dienste](/azure/security/fundamentals/security-controls) an.
- Überprüfen Sie die Azure-Sicherheitstools und -dienste unter [In Azure verfügbare Sicherheitsdienste und -technologien](/azure/security/azure-security-services-technologies).
- Besuchen Sie das [Microsoft Trust Center](https://www.microsoft.com/trustcenter/guidance/risk-assessment). Es enthält umfassende Anweisungen, Berichte und zugehörige Dokumentationen, mit denen Sie die Risikobewertungen im Rahmen Ihrer Prozesse zur Einhaltung gesetzlicher Bestimmungen ausführen können.
- Informieren Sie sich über die Tools von Drittanbietern, die verfügbar sind, um Ihre Sicherheitsanforderungen zu erfüllen. Weitere Informationen finden Sie unter [Integrieren von Sicherheitslösungen in Azure Security Center](/azure/security-center/security-center-partner-integration).
