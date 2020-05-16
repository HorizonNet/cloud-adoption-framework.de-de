---
title: 'Erste Schritte: Sichern der Unternehmensumgebung'
description: Beginnen Sie mit der Integration der Sicherheit an kritischen Punkten während der Einführung und des Betriebs der Cloud.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 3de015250a7fd14e01eb14094e564f51e0425648
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230438"
---
<!-- docsTest:ignore Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template -->

<!-- cSpell:ignore CISO passwordless -->

# <a name="get-started-implementing-security-across-the-enterprise-environment"></a>Erste Schritte: Implementieren von Sicherheit in der gesamten Unternehmensumgebung

Sicherheit ermöglicht das Geschäft durch die Gewährleistung von Vertraulichkeit, Integrität und Verfügbarkeit, wobei der Schwerpunkt auf dem Schutz vor möglichen Auswirkungen auf den Betrieb durch interne und externe böswillige und unbeabsichtigte Handlungen liegt. Diese Roadmap umreißt die wichtigsten Schritte, mit denen das Geschäftsrisiko von Cybersicherheitsangriffen gemindert oder vermieden werden kann, indem schnell wesentliche Sicherheitspraktiken in der Cloud etabliert und die Sicherheit in Ihren Cloudumstellungsprozess integriert wird.

Die Schritte in diesem Leitfaden sind für alle Rollen gedacht, die die Sicherheitsgewährleistung von Cloudumgebungen und Zielzonen unterstützen. Dazu gehören sowohl unmittelbare Prioritäten bei der Risikominderung als auch Leitlinien für den Aufbau einer modernen Sicherheitsstrategie, die Operationalisierung des Ansatzes und die Umsetzung dieser Strategie.

Verschiedene Elemente aus dem gesamten Cloud Adoption Framework sind in diesem Einführungsleitfaden enthalten:

![Erste Schritte mit der Unternehmenssicherheit](../_images/get-started/security-map.png)

Die Befolgung der Schritte in diesem Leitfaden wird Ihnen helfen, Sicherheit an kritischen Punkten im Prozess zu integrieren, um Hindernisse bei der Einführung der Cloud zu vermeiden und unnötige Geschäfts- oder Betriebsunterbrechungen zu verringern.

Microsoft hat Funktionen und Ressourcen entwickelt, die Ihnen dabei helfen können, ihre Implementierung dieses Sicherheitsleitfadens in Microsoft Azure zu beschleunigen (auf den in diesem Dokument verwiesen wird). Diese Ressourcen sollen Ihnen bei der Einrichtung, Überwachung und Durchsetzung von Sicherheit helfen und werden häufig aktualisiert und überarbeitet.

Dieses Diagramm zeigt den ganzheitlichen Ansatz, den Microsoft für die Verwendung von Sicherheitsanleitungen und Plattformtools empfiehlt, um Sicherheitstransparenz und Kontrolle über Ihre Cloudressourcen in Azure herzustellen.

![Sicherheitsdiagramm](../_images/security/security-diagram.png)

Verwenden Sie diese Schritte zur Planung und Ausführung Ihrer Strategie zur Sicherung Ihrer Cloudressourcen und zur Nutzung der Cloud zur Modernisierung der Sicherheitsabläufe:

## <a name="step-1-establish-essential-security-practices"></a>Schritt 1: Einrichten wichtiger Sicherheitsverfahren

Sicherheit in der Cloud beginnt mit soliden Praktiken. Unabhängig davon, ob Sie bereits in der Cloud arbeiten oder eine zukünftige Einführung planen, ist es wichtig, schnell grundlegende Sicherheitspraktiken einzuführen.

Zusätzlich zur Erfüllung aller expliziten Complianceanforderungen empfehlen wir die folgenden Schritte, um die größten Sicherheitsherausforderungen anzugehen, mit denen die meisten Unternehmen konfrontiert sind, wenn sie auf die Cloud umsteigen.

**Zielvorgaben und unterstützende Anleitungen:**

- **Technisch:** Mindern von Hauptrisiken und Erhöhen der Sichtbarkeit und Kontrolle von Ressourcen durch die Aktivierung von kennwortloser oder mehrstufiger Authentifizierung für Administratoren und durch Aktivieren des Bedrohungsschutzes für Cloudressourcen.
  - [Kennwortlose oder mehrstufige Authentifizierung für Administratoren](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#passwordless-or-multi-factor-authentication-for-admins)
  - [Sicherheitsvorgänge](https://docs.microsoft.com/azure/architecture/framework/security/security-operations) und [Bedrohungsschutz in Azure Security Center](https://docs.microsoft.com/azure/security-center/threat-protection)
- **Vorgehensweise:** Ermöglichen schneller Sicherheitsentscheidungen und kontinuierlicher Verbesserung durch die Zuweisung von Sicherheitsrollen und -verantwortlichkeiten und die Einrichtung eines Prozesses zur Reaktion auf Incidents.
  - [Klare Verantwortlichkeiten](https://docs.microsoft.com/azure/architecture/framework/security/governance#clear-lines-of-responsibility), [Zuweisen von Berechtigungen zum Verwalten der Umgebung](https://docs.microsoft.com/azure/architecture/framework/security/governance#assign-privileges-for-managing-the-environment) und Operationalisieren von Sicherheitsbewertungen <!-- TODO: Improve this and add link to AAF article -->
  - Sicherheitsrollen und Zuständigkeiten <!-- TODO: add link to bookmark -->
  - [Referenzleitfaden für die Reaktion auf Vorfälle](https://aka.ms/irrg)
- **Personen**: Bereitstellung von Schulungen, Tools und Zugangsmöglichkeiten für Sicherheitsteams, die für eine erfolgreiche Bereitstellung und den Betrieb während des Übergangs zur Cloudumgebung erforderlich sind.
  - **Informieren aller Beteiligten über Konzepte**, wie sich Cloud und Cloudsicherheit weiterentwickeln:
    - [Entwicklung der Bedrohungsumgebung, von Rollen und digitalen Strategien](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
    - [Transformation von Sicherheit, Strategien, Tools und Bedrohungen](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
  - **Schulen technischer Mitarbeiter** bezüglich technischer Details zu Cloudsicherheitsfunktionen für die verwendeten Plattformen. Microsoft bietet umfassende [Azure-Sicherheitsdokumentation](https://docs.microsoft.com/azure/security).
- **Langfristige architektonische Entscheidungen:** Einrichten einer langfristigen Grundlage, um die richtigen Entscheidungen zu treffen. Es ist sehr schwierig und teuer, diese Grundlage später zu ändern.
  - [Aufbau einer Unternehmenssegmentierungsstrategie und Anpassung der technischen Architekturen an diese Strategie (Netzwerksegmentierung, Identitätssegmentierung usw.).](https://docs.microsoft.com/azure/architecture/framework/security/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)
  - [Einzelnes Unternehmensverzeichnis](https://docs.microsoft.com/azure/architecture/framework/security/identity#single-enterprise-directory)
  - [Authentifizierungsstrategie für Dienste](https://docs.microsoft.com/azure/architecture/framework/security/applications-services#prefer-identity-authentication-over-keys)
  - [Berechtigungszuweisungsstrategie](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#avoid-granular-and-custom-permissions)

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudsicherheitsteam <br><br><br> | <li> Cloudstrategieteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

In diesem ersten Schritt sollten die Governanceteams auch damit beginnen, die Schaffung von Sicherheitsgrundlinien zu koordinieren, die in allen Umgebungen überwacht, verwaltet und durchgesetzt werden können. Weitere Anleitungen zu dieser Einrichtung finden Sie in Schritt 4.

> [!NOTE]
> Jede Organisation sollte ihre eigenen Mindeststandards definieren, da der Risikostatus und die anschließende Risikotoleranz je nach Branche, Kultur und anderen Faktoren stark variieren können. Beispielsweise kann es sein, dass eine Bank selbst bei einem geringfügigen Angriff auf ein Testsystem keinen potenziellen Imageschaden toleriert, wobei einige Organisationen dasselbe Risiko gerne in Kauf nehmen würden, wenn sie ihre digitale Transformation um drei bis sechs Monate beschleunigen würde.

## <a name="step-2-modernize-security-strategy"></a>Schritt 2: Modernisieren der Sicherheitsstrategie

Effektive Sicherheit in der Cloud erfordert eine solide Strategie, die die aktuelle Bedrohungsumgebung und die Art der Cloudplattform widerspiegelt, die die Unternehmensressourcen beherbergt. Eine klare Strategie verbessert die Bemühungen aller Teams, eine sichere und nachhaltige Unternehmenscloudumgebung bereitzustellen, die das Geschäftsrisiko verringert. Die Sicherheitsstrategie muss definierte Geschäftsergebnisse ermöglichen, das Risiko auf ein akzeptables Maß reduzieren und Mitarbeiter in die Lage versetzen, produktiv zu sein.

Eine Cloudsicherheitsstrategie bietet allen Teams, die an der Technologie, den Prozessen und der Bereitschaft der Mitarbeiter für diese Einführung arbeiten, eine klare Anleitung. Die Strategie sollte über die Cloudarchitektur und die technischen Fähigkeiten informieren, die Sicherheitsarchitektur und -fähigkeiten lenken und die Ausbildung und Schulung von Teams beeinflussen.

**Zielvorgaben:**

Der Strategieschritt sollte zu einem Dokument führen, das leicht an viele Beteiligte innerhalb der Organisation vermittelt werden kann, möglicherweise auch an Führungskräfte im Führungsteam der Organisation.

Aus diesem Grund empfahlen wir, die Strategie in einer Präsentation festzuhalten, um eine einfache Diskussion und Aktualisierung zu ermöglichen. Dies kann je nach Kultur und Vorlieben auch durch ein Dokument unterstützt werden.

- **Strategiepräsentation:** Möglicherweise verwenden Sie eine einzige Strategiepräsentation. Sie können aber auch eine zusammenfassende Version für Führungszielgruppen erstellen.
  - **Vollständige Präsentation:** Diese sollte den vollständigen Satz von Elementen für die Sicherheitsstrategie entweder in der Hauptpräsentation oder in optionalen Referenzfolien enthalten.
  - **Executive-Zusammenfassungen:** Versionen zur Verwendung mit Führungskräften und Vorstandsmitgliedern, die nur kritische Elemente enthalten, die für ihre Rolle relevant sind, etwa Risikobereitschaft, höchste Prioritäten oder akzeptierte Risiken.
- Sie können auch Motivationen, Ergebnisse und geschäftliche Begründungen in der [Strategie- und Planvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) aufzeichnen.

**Bewährte Methoden für das Entwickeln einer Sicherheitsstrategie:**

Erfolgreiche Programme integrieren diese Elemente in ihren Sicherheitsstrategieprozess:

- **Enge Ausrichtung an Geschäftsstrategie:** Die Aufgabe von Sicherheit ist der Schutz des Unternehmenswerts, daher ist es entscheidend, alle Sicherheitsbemühungen auf diesen Zweck auszurichten und interne Konflikte zu minimieren.
  - **Schaffen eines gemeinsamen Verständnisses:** Von geschäftlichen, IT- und Sicherheitsanforderungen.
  - **Frühzeitige Integration von Sicherheit in die Cloudeinführung:** Zur Vermeidung von Last-Minute-Krisen durch vermeidbare Risiken.
  - **Agiler Ansatz:** Um sofort Mindestsicherheitsanforderungen festzulegen und die Sicherheitsgarantien im Laufe der Zeit kontinuierlich zu verbessern.
  - **Änderung der Sicherheitskultur:** Durch absichtliche proaktive Führungsaktionen.

Weitere Informationen finden Sie unter [Transformationen, Denkrichtungen und Erwartungen](../strategy/define-security-strategy.md#transformations-mindsets-and-expectations).

- **Modernisieren der Sicherheitsstrategie:** Die Sicherheitsstrategie sollte Überlegungen zu allen Aspekten des modernen technologischen Umfelds, der aktuellen Bedrohungslandschaft und der Ressourcen der Sicherheitscommunity beinhalten.
  - **Anpassen an das Modell für die gemeinsame Verantwortlichkeit** der Cloud.
  - **Einbeziehen aller Cloudtypen und der Verwendung mehrerer Clouds.**
  - **Bevorzugen nativer Cloudsteuerelemente**, um unnötige und schädliche Reibung zu vermeiden.
  - **Integration der Sicherheitscommunity:** Um mit dem Tempo der Entwicklung der Angreifer Schritt zu halten.

**Verwandte Ressourcen für zusätzlichen Kontext:**

- [Entwicklung der Bedrohungsumgebung, von Rollen und digitalen Strategien](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
- [Transformation von Sicherheit, Strategien, Tools und Bedrohungen](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
- Überlegungen zur Cloud Adoption Framework-Strategie:
  - [Modernisieren Ihrer Sicherheitsstrategie](../strategy/define-security-strategy.md#modernize-your-security-strategy)
  - [Resilienz bei der Cybersicherheit](../strategy/define-security-strategy.md#cybersecurity-resilience)
  - [Ändern der Sicherheitsbeziehungen und Verantwortlichkeiten durch die Cloud](../strategy/define-security-strategy.md#how-the-cloud-is-changing-security)

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Führungsteam für Sicherheit (Chief Information Security Officer (CISO) oder gleichwertig) | <li> Cloudstrategieteam <li> Cloudsicherheitsteam <li> Cloudeinführungsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

**Genehmigung der Strategie:** Führungskräfte und Geschäftsleiter mit Rechenschaftspflicht für die Geschäftsergebnisse oder Geschäftsrisiken der Geschäftssparte(n) innerhalb der Organisation (dies kann je nach Organisation den Vorstand einschließen).

## <a name="step-3-develop-a-security-plan"></a>Schritt 3: Entwickeln Sie einen Sicherheitsplan.

Die Planung setzt die Sicherheitsstrategie in die Tat um, indem sie Ergebnisse, Meilensteine, Zeitpläne und Aufgabenträger definiert. In diesem Plan werden auch die Rollen und Zuständigkeiten der Teams erläutert.

Sicherheitsplanung und Planung der Cloudbereitstellung sollten nicht isoliert voneinander durchgeführt werden. Es ist von entscheidender Bedeutung, das Cloudsicherheitsteam frühzeitig in die Planungszyklen einzubinden, um zu vermeiden, dass Arbeitsunterbrechungen oder erhöhte Risiken durch zu spät erkannte Sicherheitsprobleme auftreten. Die Sicherheitsplanung funktioniert am besten mit fundiertem Wissen und Bewusstsein über den digitalen Bestand und das vorhandene IT-Portfolio, das durch die vollständige Integration in den Cloudplanungsprozess entsteht.

**Zielvorgaben:**

- **Systemsicherheitsplan:** Sollte Teil der Hauptplanungsdokumentation für die Cloud sein und kann ein Dokument sein, das die [Strategie- und Planvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), einen detaillierten Foliensatz, eine Projektdatei oder eine Kombination dieser Formate verwendet, je nach Größe, Kultur und Standardverfahren der Organisation.

- Der Sicherheitsplan sollte alle diese Elemente enthalten:

  - **Plan für Organisationsfunktionen:** Damit die Teams wissen, wie sich die derzeitigen Sicherheitsrollen und -verantwortlichkeiten mit dem Umstieg auf die Cloud verändern werden.
    - **Sicherheitskompetenzplan**, um die Teammitglieder bei der Bewältigung der bedeutenden Veränderungen in Technologie, Rollen und Verantwortlichkeiten zu unterstützen.
  - **Roadmap für technische Sicherheitsarchitektur und -funktionen:** Leitfaden für technische Teams.
  Microsoft stellt Referenzarchitekturen und Technologiefunktionen zur Verfügung, die Sie beim Erstellen Ihrer Architektur und Roadmap unterstützen:
    - [Azure-Komponenten und -Referenzmodell](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151), um die Planung und den Entwurf von Azure-Sicherheitsrollen zu beschleunigen.
      ![Azure-Verwaltungsmodell](../_images/security/azure-administration-model.png)
      ![Azure RBAC-Modell](../_images/security/azure-rbac-model.png)
    - [Cybersicherheits-Referenzarchitektur von Microsoft](https://aka.ms/mcra) zum Aufbau einer allgemeinen Cybersicherheitsarchitektur für ein hybrides Unternehmen, das sowohl lokale als auch Cloudressourcen umfasst.
    - [SOC-Referenzarchitektur (Security Operations Center)](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks#part-1-introduction---soc-learnings-strategies-and-technical-integration-2430) zur Modernisierung der Sicherheitserkennung, -reaktion und -wiederherstellung.
    - [Zero-Trust-Referenzarchitektur für Benutzerzugriff](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-3#part-5-zero-trust-user-access-reference-architecture-842) zur Modernisierung der Zugriffssteuerungsarchitektur für Cloudgenerierung.
    - [Azure Security Center](https://docs.microsoft.com/azure/security-center/) und [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/), um Cloudressourcen zu schützen.
  - **Sicherheitsbewusstsein und Schulungsplan:** Damit alle Teams über grundlegende wichtige Sicherheitskenntnisse verfügen.
  - **Kennzeichnung der Ressourcensensitivität:** Bestimmung sensibler Ressourcen mithilfe einer Taxonomie, die sich an den Auswirkungen auf das Geschäft orientiert (die gemeinsam von Geschäftsbeteiligten, Sicherheitsteams und anderen interessierten Parteien erstellt wird).

- **Annehmen einer Hybridumgebung:** Dazu zählen SaaS-Anwendungen (Software-as-a-Service), lokale Umgebungen und mehrere Anbieter von Cloud Infrastructure-as-a-Service und Platform-as-a-Service (falls zutreffend).
- **Aktualisieren des Cloudplans mit Sicherheitsänderungen:** Aktualisierung anderer Abschnitte des Hauptplans zur Einführung der Cloud, um die durch den Sicherheitsplan ausgelösten Änderungen zu berücksichtigen.

**Bewährte Methoden für Sicherheitsplanung:** Ihr Sicherheitsplan ist wahrscheinlich erfolgreicher, wenn die Planung den folgenden Ansatz verwendet:

- **Agile Einführung von Sicherheit:** Einrichten von Mindestsicherheitsanforderungen als erstes und Verschieben aller nichtkritischen Punkte in eine priorisierte Liste der nächsten Schritte.
Dies sollte kein herkömmlicher detaillierter Plan für 3 bis 5 Jahre sein, da sich die Cloud und das Bedrohungsumfeld zu schnell ändern, als dass diese Art von Plan sinnvoll wäre. Der Plan sollte sich auf die Entwicklung der Anfangsschritte und des Endzustands konzentrieren:
  - **Schnelle Erfolge:** Detaillierter Plan für die unmittelbare Zukunft, um schnelle Erfolge zu erzielen und mit längerfristigen Initiativen zu beginnen, die eine hohe Wirkung erzielen. Dieser kann sich je nach Organisationskultur, Standardverfahren und anderen Faktoren auf 3 bis 12 Monate beziehen.
  - **Klare Vision** des gewünschten Endzustands als Leitfaden für den Planungsprozess jedes Teams (das Erreichen dieses Ziels kann mehrere Jahre dauern).
- **Umfassende Verbreitung des Plans:** Um das Bewusstsein von Projektbeteiligten zu erhöhen und Feedback zu erhalten.
- **Erreichen der strategischen Ergebnisse:** Sicherstellen, dass Ihr Plan die in der Sicherheitsstrategie beschriebenen strategischen Ergebnisse ermöglicht und erfüllt.
- **Eigentümerschaft, Verantwortlichkeit und Fristen:** Sicherstellen, dass die Verantwortlichen für jede Aufgabe ermittelt werden und sich verpflichten, diese Aufgabe in einem bestimmten Zeitrahmen zu erledigen.
- **Berücksichtigen der menschlichen Seite von Sicherheit:** Menschen in dieser Zeit des Wandels und der neuen Erwartungen einbeziehen durch:
  - **Aktives Unterstützen der Transformation der Teammitglieder:** Durch klare Kommunikation und Coaching zu den folgenden Themen:
    - Welche Fähigkeiten müssen erlernt werden?
    - Warum diese erlernt werden müssen (und die damit verbundenen Vorteile)
    - Wie diese Kenntnisse erworben werden (und Ressourcen bereitgestellt werden, um den Kenntniserwerb zu unterstützen).
  Dies kann mithilfe der [Strategie- und Planvorlage](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) dokumentiert werden, und Sie können [Onlinesicherheitstraining von Microsoft](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction) nutzen, um die Ausbildung Ihrer Teammitglieder zu unterstützen.
  - **Sorgen für Sicherheitsbewusstsein:** Um Menschen dabei zu helfen, eine echte Verbindung zu ihrem Anteil an der Sicherheit der Organisation herzustellen.
- **Vertrautmachen mit Microsoft-Erkenntnissen und -Anleitungen:** Microsoft hat Einblicke und Perspektiven veröffentlicht, um Ihrem Unternehmen bei der Planung der Umstellung auf die Cloud und eine moderne Sicherheitsstrategie zu helfen, einschließlich aufgezeichneter Schulungen, Dokumentationen und bewährter Sicherheitsmethoden und empfohlener Standards.
  Technische Anleitungen für die Erstellung Ihres Plans und Ihrer Architektur finden Sie in der [Microsoft-Sicherheitsdokumentation](https://docs.microsoft.com/security).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudsicherheitsteam | <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Alle Risikoteams in Ihrer Organisation <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

**Genehmigung des Sicherheitsplans:** Sicherheitsführungsteam (CISO oder Äquivalent).

## <a name="step-4-secure-new-workloads"></a>Schritt 4: Sichern neuer Workloads

Es ist viel einfacher, in einem sicheren Zustand zu beginnen, als die Sicherheit später in Ihrer Umgebung nachzurüsten. Wir empfehlen dringend, mit einer sicheren Konfiguration zu beginnen, um sicherzustellen, dass die Workloads in eine sichere Umgebung migriert und dort entwickelt und getestet werden.

Während der Implementierung der [Zielzone](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone) können sich viele Entscheidungen auf Sicherheits- und Risikoprofile auswirken. Das Cloudsicherheitsteam sollte die Konfiguration der Zielzone überprüfen, um sicherzustellen, dass sie den Sicherheitsstandards und -anforderungen der Sicherheitsbaselines Ihrer Organisation entspricht.

**Zielvorgaben:**

- Stellen Sie sicher, dass neue Zielzonen die Compliance- und Sicherheitsanforderungen der Organisation erfüllen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- **Kombinieren von vorhandener Anforderungen und Cloudempfehlungen:** Beginnen Sie mit den empfohlenen Anleitungen, und passen Sie diese dann an Ihre individuellen Sicherheitsanforderungen an. Bei dem Versuch, lokale Richtlinien und Standards durchzusetzen, sind wir auf Herausforderungen gestoßen, da diese sich oft auf veraltete Technologie oder Sicherheitsansätze beziehen. Microsoft hat einen Leitfaden veröffentlicht, der Sie bei der Erstellung Ihrer Sicherheitsbaselines unterstützt:
  - [Azure-Sicherheitsstandards für Strategie und Architektur](https://docs.microsoft.com/security/compass/compass): Strategie- und Architekturempfehlungen zur Gestaltung der Sicherheitshaltung Ihrer Umgebung.
  - [Vergleichstests für die Azure-Sicherheit:](https://docs.microsoft.com/azure/security/benchmarks/introduction) Spezifische Konfigurationsempfehlungen zum Sichern von Azure-Umgebungen.
  - [Azure-Sicherheitsbaselinetraining](https://docs.microsoft.com/learn/modules/create-security-baselines).
- **Bereitstellen von Schutzmaßnahmen:** Diese sollten über automatisierte Überwachung und Durchsetzung der Richtlinie verfügen. Für diese neuen Umgebungen sollten die Teams bestrebt sein, die Sicherheitsbaselines Ihrer Organisation sowohl zu prüfen als auch durchzusetzen, um Sicherheitsüberraschungen während der Entwicklung sowie die Continuous Integration und Continuous Deployment (CI/CD) von Workloads zu minimieren.
Microsoft bietet verschiedene native Funktionen in Azure, um dies zu ermöglichen:
  - [Secure Score](https://docs.microsoft.com/azure/security-center/secure-score-security-controls): Eine gewichtete Bewertung Ihres Azure-Sicherheitsstatus, die es Ihnen ermöglicht, die Sicherheitsbemühungen und -projekte in Ihrer Organisation nachzuverfolgen.
  - [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview): Cloudarchitekten und zentrale IT-Gruppen können eine wiederholbare Gruppe von Azure-Ressourcen definieren, mit der die Standards, Muster und Anforderungen einer Organisation implementiert und erzwungen werden.
  - [Azure Policy](https://docs.microsoft.com/azure/governance/policy/): Die Grundlage der Sichtbarkeits- und Steuerungsfunktionen, die von diesen anderen Diensten verwendet werden. Azure Policy ist in [Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager) integriert und ermöglicht es Ihnen, Änderungen zu prüfen und Richtlinien für jede Ressource in Azure vor, während oder nach ihrer Erstellung durchzusetzen.
- [Verbessern des Betriebs von Zielzonen](../ready/considerations/landing-zone-security.md): Verwenden Sie bewährte Methoden zur Verbesserung der Sicherheit innerhalb einer bestimmten Zielzone.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudsicherheitsteam | <li> Cloudeinführungsteam <li> Cloudplattformteam <li> Cloudstrategieteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-5-secure-existing-cloud-workloads"></a>Schritt 5: Sichern vorhandener Cloudworkloads

Viele Unternehmen haben bereits Ressourcen in Unternehmenscloudumgebungen bereitgestellt, die die bewährten Sicherheitsmethoden nicht angewendet haben, was zu einem größeren Geschäftsrisiko führte.

Nachdem Sie sichergestellt haben, dass neue Anwendungen und Zielzone den bewährten Sicherheitsmethoden folgen, sollten Sie sich darauf konzentrieren, vorhandene Umgebungen auf den gleichen Standard zu bringen.

**Zielvorgaben:**

- Stellen Sie sicher, dass alle vorhandenen Cloudumgebungen und Zielzonen die Compliance- und Sicherheitsanforderungen des Unternehmens erfüllen.
- Testen Sie die Betriebsbereitschaft von Produktionsbereitstellungen mithilfe von Sicherheitsbaselinerichtlinien.
- Überprüfen Sie die Einhaltung der Richtlinien für den Entwurf der Sicherheitsbaseline und der Sicherheitsanforderungen.

**Leitfaden zur Erreichung der Zielvorgaben:**

- Verwenden Sie die gleichen Sicherheitsbaselines, die Sie in [Schritt 4](#step-4-secure-new-workloads) erstellt haben, als idealen Status. Möglicherweise müssen Sie einige Richtlinieneinstellungen so anpassen, dass sie nur überwacht werden, anstatt sie zu erzwingen.
- Gleichen Sie Betriebs- und Sicherheitsrisiken aus. Da diese Umgebungen möglicherweise Produktionssysteme hosten, die kritische Geschäftsprozesse ermöglichen, müssen Sie Sicherheitsverbesserungen möglicherweise schrittweise implementieren, um das Risiko eines Betriebsausfalls zu vermeiden.
- Priorisieren Sie die Erkennung und Behebung von Sicherheitsrisiken nach der geschäftlichen Wichtigkeit, beginnend mit Workloads, die bei einer Gefährdung eine hohe geschäftliche Auswirkung haben, und Workloads mit einem hohen Risiko.

Weitere Informationen finden Sie unter [Identifizieren und Klassifizieren von unternehmenskritischen Anwendungen](https://docs.microsoft.com/azure/architecture/framework/security/applications-services?toc=/security/compass/toc.json&bc=/security/compass/breadcrumb/toc.json#identify-and-classify-business-critical-applications).

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudeinführungsteam | <li> Cloudeinführungsteam <li> Cloudstrategieteam <li> Cloudsicherheitsteam <li> Cloudgovernanceteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="step-6-govern-to-manage-and-improve-security-posture"></a>Schritt 6: Steuern der Verwaltung und Verbesserung des Sicherheitsstatus

Wie alle modernen Disziplinen ist Sicherheit ein iterativer Prozess, der sich auf kontinuierliche Verbesserung konzentrieren sollte. Der Sicherheitsstatus kann auch verfallen, wenn Organisationen den Fokus darauf im Laufe der Zeit nicht aufrechterhalten.

Die konsequente Anwendung von Sicherheitsanforderungen kommt von soliden Governancedisziplinen und automatisierten Lösungen. Sobald die Sicherheitsbaselines durch das Cloudsicherheitsteam definiert wurden, sollten diese Anforderungen überprüft werden, um sicherzustellen, dass sie in allen Cloudumgebungen einheitlich angewendet (und ggf. durchgesetzt) werden.

**Zielvorgaben:**

- Sicherstellen, dass die Sicherheitsbaselines der Organisation auf alle relevanten Systeme angewandt werden und dass Anomalien anhand eines [Secure Score](https://docs.microsoft.com/azure/security-center/secure-score-security-controls) oder eines ähnlichen Mechanismus überprüft werden.
- Dokumentieren von Document Security Baseline-Richtlinien, Prozessen und Entwurfsanleitungen für Sicherheitsrichtlinien in der [Sicherheitsbaselinevorlage](../govern/security-baseline/template.md).

**Leitfaden zur Erreichung der Zielvorgaben:**

- Verwenden Sie die gleichen Sicherheitsbaselines und Überwachungsmechanismen, die Sie in [Schritt 4](#step-4-secure-new-workloads) als technische Komponenten zur Überwachung der Baselines erstellt haben, ergänzt durch Personen- und Prozesssteuerungen, um Konsistenz zu gewährleisten.
- Achten Sie darauf, dass bei allen Workloads und Ressourcen ordnungsgemäße [Benennungs- und Kennzeichnungskonventionen](../ready/azure-best-practices/naming-and-tagging.md) eingehalten werden, und setzen Sie [Kennzeichnungskonventionen mithilfe von Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) mit einem spezifischen Schwerpunkt auf Tags für „Datensensitivität“ durch.
- Wenn Sie mit Cloudgovernance noch nicht vertraut sind, richten Sie [Governancerichtlinien, -prozesse und -disziplinen](../govern/index.md) mithilfe der Governancemethodik ein.

<!-- markdownlint-disable MD033 -->
<br>

| Verantwortliches Team | Verantwortliche und unterstützende Teams |
| --- | --- |
| <li> Cloudgovernanceteam | <li> Cloudstrategieteam <li> Cloudsicherheitsteam <li> Cloudkompetenzzentrum (Cloud Center of Excellence, CCoE) oder zentrale IT |

## <a name="next-steps"></a>Nächste Schritte

Diese Schritte führen Sie durch die Implementierung der richtigen Strategien, Steuerungen, Prozesse, Fähigkeiten und Kultur, die für eine konsistente Verwaltung von Sicherheitsrisiken im gesamten Unternehmen erforderlich sind.
Wenn Sie den Betriebsmodus der Cloudsicherheit fortsetzen, sollten Sie diese nächsten Schritte in Betracht ziehen, die auf den ersten Schritten in diesem Leitfaden basieren.

- Lesen Sie die [Microsoft-Sicherheitsdokumentation](https://docs.microsoft.com/security), die einen technischen Leitfaden enthält, der Sicherheitsexperten bei der Erstellung und Verbesserung von Strategie, Architektur und priorisierten Roadmaps für Cybersicherheit unterstützt.
- Überprüfen Sie die Sicherheitsinformationen für [integrierte Sicherheitssteuerungen der Azure-Dienste](https://docs.microsoft.com/azure/security/fundamentals/security-controls).
- Überprüfen Sie die Azure-Sicherheitstools und -dienste unter [In Azure verfügbare Sicherheitsdienste und -technologien](https://docs.microsoft.com/azure/security/azure-security-services-technologies).
- Besuchen Sie das [Microsoft Trust Center](https://www.microsoft.com/trustcenter/guidance/risk-assessment), das umfassende Anweisungen, Berichte und zugehörige Dokumentation enthält, mit denen Sie die Risikobewertungen im Rahmen Ihres Migrationsplanungsprozesses ausführen können.
- Informieren Sie sich über die Tools von Drittanbietern, die verfügbar sind, um Ihre Sicherheitsanforderungen zu erfüllen. Weitere Informationen finden Sie unter [Integrieren von Sicherheitslösungen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).
