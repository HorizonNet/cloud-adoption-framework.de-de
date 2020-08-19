---
title: Definieren einer Sicherheitsstrategie
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie eine geschäftlichen Begründung für die Cloudmigration erstellen.
author: MarkSimos
ms.author: mas
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 7f52dfb9c58e619a4d626960ac3115575985253a
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88572645"
---
<!-- cSpell:ignore MarkSimos NIST CISO COVID -->

# <a name="define-a-security-strategy"></a>Definieren einer Sicherheitsstrategie

Die letztendlichen Ziele für eine Sicherheitsorganisation ändern sich nicht mit der Einführung von Clouddiensten, aber die Art und Weise, wie diese Ziele erreicht werden, wird sich ändern. Sicherheitsteams müssen sich nach wie vor darauf konzentrieren, das Geschäftsrisiko durch Angriffe zu reduzieren, und daran arbeiten, dass Vertraulichkeit, Integrität und Verfügbarkeit in allen Informationssystemen und Daten gewährleistet sind.

## <a name="modernize-your-security-strategy"></a>Modernisieren Ihrer Sicherheitsstrategie

Sicherheitsteams müssen Strategien, Architekturen und Technologien modernisieren, während das Unternehmen die Cloud einführt und sie im Laufe der Zeit betreibt. Obwohl der Umfang und die Anzahl der Änderungen zunächst entmutigend erscheinen mögen, erlaubt die Modernisierung des Sicherheitsprogramms der Sicherheit, einige leidige Lasten abzubauen, die mit Legacyansätzen verbunden sind. Ein Unternehmen kann vorübergehend mit Legacystrategien und -tools arbeiten, aber dieser Ansatz ist angesichts des Tempos der Veränderungen in der Cloud und der Bedrohungsumgebung nur schwer aufrechtzuerhalten:

- Sicherheitsteams werden bei der Entscheidungsfindung für die Cloudeinführung wahrscheinlich außen vor bleiben, wenn sie sich auf eine „kurzsichtige“ Sicherheitshaltung besinnen, bei der die Antwort immer mit „Nein“ beginnt (anstatt mit IT- und Betriebsteams zusammenzuarbeiten, um Risiken zu reduzieren und gleichzeitig die Geschäfte zu ermöglichen).
- Sicherheitsteams werden es schwer haben, Cloudangriffe zu entdecken und sich gegen diese zu verteidigen, wenn sie für alle Abwehr- und Überwachungsmaßnahmen nur veraltete, lokale Tools verwenden und sich ausschließlich an die Richtlinie „Nur Netzwerkumkreis“ halten. Die Verteidigung auf Cloudniveau erfordert den Einsatz von cloudnativen Erkennungs- und Automatisierungsfunktionen und die Einführung eines Identitätsbereichs, um die Überwachung und den Schutz von mobilen sowie Cloudobjekten zu unterstützen.

Da diese Transformation erheblich sein kann, empfehlen wir den Sicherheitsteams einen flexiblen Ansatz zur Modernisierung der Sicherheit, bei dem die kritischsten Aspekte der Strategie rasch modernisiert und danach kontinuierlich schrittweise verbessert werden.

### <a name="security-of-the-cloud-and-from-the-cloud"></a>Sicherheit der Cloud und von der Cloud

Wenn Ihr Unternehmen Clouddienste einführt, werden die Sicherheitsteams auf zwei Hauptziele hinarbeiten:

- **Sicherheit \*der\* Cloud (Sichern von Cloudressourcen):** Die Sicherheit sollte in die Planung und den Betrieb von Clouddiensten integriert werden, um sicherzustellen, dass diese zentralen Sicherheitszusicherungen bei allen Ressourcen konsistent angewandt werden.
- **Sicherheit \*von\* der Cloud (Verwenden der Cloud zum Transformieren der Sicherheit):** Das Sicherheitsteam sollte unverzüglich mit der Planung und Erörterung beginnen, wie Cloudtechnologien zur Modernisierung von Sicherheitstools und -prozessen, insbesondere von nativ integrierten Sicherheitstools, verwendet werden können. Immer mehr Sicherheitstools werden in der Cloud gehostet und bieten Funktionen, die in einer lokalen Umgebung schwierig oder unmöglich zu realisieren sind.

Viele Unternehmen beginnen damit, Cloudressourcen als zusätzliches _virtuelles Rechenzentrum_ zu behandeln, das sich sehr gut als Ausgangspunkt für die Sicherheit der Cloud eignet. Bei der Modernisierung von Unternehmen, die Sicherheit aus der Cloud nutzen, werden die meisten schnell feststellen, dass sie diesem Denkmodell entwachsen. Die Sicherung eines softwaredefinierten Rechenzentrums mithilfe von in der Cloud gehosteten Tools ermöglicht Funktionen, die über das hinausgehen, was lokale Modelle bieten können:

- Schnelles Aktivieren und Skalieren von Sicherheitsfunktionen.
- Hocheffektiver Ressourcenbestand und ordnungsgemäße Ermittlung der Sicherheitskonfiguration.
- Kontinuierliche Bewertung der Sicherheitslage und -kontrollen des Unternehmens.
- Erheblich verbesserte Bedrohungserkennung, die riesige Threat Intelligence-Repositorys und eine praktisch unbegrenzte Verarbeitung/Speicherung der Cloud nutzt.

### <a name="the-right-level-of-security-friction"></a>Das richtige Maß an Sicherheitsspannungen

Sicherheit erzeugt natürlich entsprechende Spannungen, die Prozesse verlangsamen. Es ist entscheidend zu erkennen, welche Elemente in Ihren DevOps- und IT-Prozessen fehlerfrei sind und welche nicht:

- **Normale Spannungen:** Ähnlich wie der Widerstand beim Training einen Muskel stärker macht, stärkt die Integration des richtigen Maßes an Sicherheitspannungen das System oder die App, indem zum richtigen Zeitpunkt kritisches Denken erzwungen wird. Dies geschieht in der Regel in Form einer Überlegung, wie und warum ein Angreifer versuchen könnte, eine Anwendung oder ein System während des Entwurfs anzugreifen, sowie durch Überprüfung, Identifizierung und idealerweise Behebung potenzieller Sicherheitsrisiken, die ein Angreifer in Softwarecode, Konfigurationen oder betrieblichen Methoden ausnutzen kann.
- **Fehlerhafte Spannungen:** Verhindern einen größeren Wert, als sie schützen. Dies geschieht häufig, wenn die von Tools generierten Sicherheitsfehler eine hohe „False Positive“-Rate aufweisen (z. B. Fehlalarme) oder wenn der Aufwand zur Entdeckung oder Behebung von Sicherheitsproblemen die möglichen Auswirkungen eines Angriffs bei weitem übersteigt.

### <a name="standalone-and-integrated-responsibilities"></a>Eigenständige und integrierte Verantwortlichkeiten

Die Bereitstellung von Vertraulichkeit, Integrität und Verfügbarkeit erfordert, dass Sicherheitsexperten spezielle Sicherheitsfunktionen ausführen und eng mit anderen Teams in der Organisation zusammenarbeiten:

- **Eindeutige Sicherheitsfunktionen:** Sicherheitsteams führen unabhängige Funktionen aus, die an anderer Stelle in der Organisation nicht gefunden werden, z. B. Sicherheitsvorgänge, Verwaltung von Sicherheitsrisiken und andere Funktionen.
- **Integrieren der Sicherheit in andere Funktionen:** Sicherheitsteams dienen auch als Fachexperten für andere Teams und Funktionen in der Organisation, die Geschäftsinitiativen fördern, Risiken bewerten, Anwendungen entwerfen oder entwickeln und IT-Systeme betreiben. Sicherheitsteams beraten diese Teams mit Fachwissen und Kontext in Bezug auf Angreifer, Angriffsmethoden und -trends, Sicherheitsrisiken, die unbefugten Zugriff ermöglichen könnten, sowie Optionen für Abhilfemaßnahmen oder Problemumgehungen und deren potenzielle Vorteile oder Tücken. Diese Funktion der Sicherheit ähnelt der einer Qualitätsfunktion, da sie an vielen Positionen integriert wird, um einzelne Ergebnisse stärker oder weniger stark zu unterstützen.

Die Wahrnehmung dieser Verantwortlichkeiten bei gleichzeitigem Schritthalten mit dem raschen Wandel in der Cloud und der Transformation des Geschäfts erfordert von den Sicherheitsteams eine Modernisierung ihrer Tools, Technologien und Prozesse.

## <a name="transformations-mindsets-and-expectations"></a>Transformationen, Denkrichtungen und Erwartungen

Viele Unternehmen verwalten eine Kette von mehreren parallelen Transformationen in der Organisation. Diese internen Transformationen beginnen in der Regel, da sich fast alle externen Märkte transformieren, um den neuen Kundenpräferenzen für Mobil- und Cloudtechnologien zu entsprechen. Unternehmen sehen sich häufig der Bedrohung durch neue Startups und der digitalen Transformation traditioneller Konkurrenten ausgesetzt, die den Markt stören können.

![Kette von mehreren parallelen Transformationen in der Organisation](../_images/security/transformation-chain.png)

Der interne Transformationsprozess umfasst in der Regel Folgendes:

- **Digitale Transformation** des Geschäfts, um neue Gelegenheiten zu nutzen und wettbewerbsfähig gegenüber digitalen nativen Startups zu bleiben.
- **Technologietransformation** der IT-Organisation zur Unterstützung der Initiative mit Clouddiensten, modernisierten Entwicklungsmethoden und damit verbundenen Änderungen.
- **Sicherheitstransformation**, um sowohl die Cloud einzuführen als auch gleichzeitig einer immer komplexeren Bedrohungsumgebung zu begegnen.

### <a name="internal-conflict-can-be-costly"></a>Interne Konflikte können kostenintensiv sein

Änderungen erzeugen Stress und Konflikte, die die Entscheidungsfindung zum Erliegen bringen können. Dies gilt insbesondere für die Sicherheit, wo die Verantwortung für das Sicherheitsrisiko häufig bei den fachlichen Ansprechpartnern (Sicherheitsteams) anstatt bei den Objektbesitzern (Geschäftsinhaber) liegt, die für die Geschäftsergebnisse und alle anderen Risikoarten verantwortlich sind. Diese falsch zugeordnete Verantwortlichkeit erfolgt häufig, da alle Beteiligten die Sicherheit fälschlicherweise als technisches oder absolutes Problem betrachten, das es zu lösen gilt, und nicht als dynamisches fortlaufendes Risiko wie Wirtschaftsspionage und andere herkömmliche kriminelle Aktivitäten.

Während dieser Zeit der Transformation muss die Leitung aller Teams aktiv an der Verringerung von Konflikten arbeiten, die sowohl kritische Projekte zum Scheitern bringen als auch Teams dazu veranlassen können, die Minderung von Sicherheitsrisiken zu umgehen. Interner Konflikt zwischen Teams kann zu Folgendem führen:

- **Erhöhtes Sicherheitsrisiko**, z. B. vermeidbare Sicherheitsvorfälle oder erhöhter geschäftlicher Schaden durch Angriffe (insbesondere wenn die Sicherheit zur Frustration bei Teams führt und normale Prozesse umgangen werden, oder wenn veraltete Sicherheitsansätze von Angreifern leicht umgangen werden können).
- **Negative Auswirkungen auf das Geschäft oder den Auftrag**, z. B. wenn Geschäftsprozesse nicht schnell genug aktiviert oder aktualisiert werden, um den Marktanforderungen gerecht zu werden (oft der Fall, wenn Sicherheitsprozesse wichtige Geschäftsinitiativen behindern).

Es ist von entscheidender Bedeutung, sich der Integrität der Beziehungen innerhalb und zwischen den Teams bewusst zu sein, um ihnen zu helfen, sich in der sich verändernden Umgebung zurechtzufinden, die wertvolle Teammitglieder verunsichern und beunruhigen könnte. Geduld, Einfühlungsvermögen und Aufklärung über diese Denkweisen und das positive Potenzial der Zukunft werden Ihren Teams helfen, diese Phase besser zu überstehen und gute Sicherheitsergebnisse für die Organisation zu erzielen.

Führungskräfte können mit konkreten proaktiven Schritten wie den Folgenden die Durchsetzung kultureller Änderungen unterstützen:

- Öffentlich das Verhalten vorleben, das sie von ihren Teams erwarten.
- Transparenz hinsichtlich der Herausforderungen der Veränderungen zeigen, einschließlich der Betonung ihrer eigenen Anpassungsprobleme.
- Regelmäßige Erinnerung der Teams an die Dringlichkeit und Bedeutung der Modernisierung und Integration der Sicherheit.

### <a name="cybersecurity-resilience"></a>Resilienz bei der Cybersicherheit

Viele klassische Sicherheitsstrategien haben sich ausschließlich auf die Verhinderung von Angriffen konzentriert, was für moderne Bedrohungen nicht ausreichend ist. Sicherheitsteams müssen sicherstellen, dass ihre Strategie darüber hinausgeht und auch eine schnelle Angriffserkennung, Reaktion und Wiederherstellung ermöglicht, um die Resilienz zu erhöhen. Organisationen müssen davon ausgehen, dass Angreifer einige Ressourcen gefährden werden (manchmal auch als „angenommene Sicherheitsverletzung“ bezeichnet) und darauf hinarbeiten, dass Ressourcen und technische Entwürfe zwischen Angriffsverhütung und Angriffsmanagement ausgewogen sind (statt des typischen Standardansatzes, nur zu versuchen, Angriffe zu verhindern).

Für viele Organisationen ist dieser Zustand schon Realität, da sie in den letzten Jahren mit der stetigen Zunahme des Aufkommens und der Komplexität der Angriffe fertig geworden sind. Diese Journey beginnt oft mit dem ersten größeren Vorfall, der ein emotionales Ereignis darstellen kann, bei dem die Betroffenen ihr vorheriges Gefühl der Unverwundbarkeit und Sicherheit verlieren. Dieses Ereignis ist zwar nicht so schwerwiegend wie der Verlust von Menschenleben, kann aber ähnliche Emotionen auslösen, die mit Verleugnung beginnen und schließlich in Akzeptanz enden. Diese Annahme des „Versagens“ mag für manche zunächst schwer zu akzeptieren sein, aber sie weist starke Parallelen zu dem bewährten Konstruktionsprinzip der Ausfallsicherheit auf, und die Annahme ermöglicht es Ihren Teams, sich auf eine bessere Definition von Erfolg zu konzentrieren: Resilienz.

Die Funktionen des [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework) dienen als nützlicher Leitfaden dafür, wie Investitionen zwischen den komplementären Aktivitäten der Identifizierung, der Sicherung, der Erkennung, der Reaktion und der Wiederherstellung in einer resilienten Strategie ausgeglichen werden können.

Weitere Informationen zur Resilienz der Cybersicherheit und zu den letztendlichen Zielen von Cybersicherheitskontrollen finden Sie unter [Wie halten Sie das Risiko Ihrer Organisation gering?](/azure/architecture/framework/security/resilience).

### <a name="how-the-cloud-is-changing-security"></a>Auswirkungen der Cloud auf die Sicherheit

Der Wechsel in die Cloud für die Sicherheit ist mehr als nur ein einfacher Technologiewechsel. Es handelt sich um einen Generationswechsel in der Technologie, vergleichbar mit dem Wechsel von Mainframecomputern zu Desktopcomputern und zu Unternehmensservern. Die erfolgreiche Bewältigung dieses Wechsels erfordert einen grundlegenden Wandel hinsichtlich der Erwartungen und der Denkweise der Sicherheitsteams. Wenn Sie die richtigen Denkweisen und Erwartungen übernehmen, werden Konflikte innerhalb Ihrer Organisation verringert und die Effektivität der Sicherheitsteams erhöht.

Diese könnten zwar Teil eines beliebigen Plans zur Modernisierung der Sicherheit sein, doch das schnelle Tempo der Änderungen in der Cloud weist ihrer Einführung eine hohe Priorität zu.

- **Partnerschaft mit gemeinsamen Zielen.** Im Zeitalter der rasanten Entscheidungen und der ständigen Weiterentwicklung der Prozesse kann die Sicherheit nicht mehr einen „kurzsichtigen“ Ansatz übernehmen, wenn es darum geht, Veränderungen der Umgebung zu genehmigen oder abzulehnen. Die Sicherheitsteams müssen eng mit den Geschäfts- und IT-Teams zusammenarbeiten, um gemeinsame Ziele in Bezug auf Produktivität, Zuverlässigkeit und Sicherheit festzulegen, und gemeinsam mit diesen Partnern daran arbeiten, diese Ziele zu erreichen.

  Diese Partnerschaft ist die ultimative Form des „Shift Left“ (Verschiebung in Richtung des Ausgangspunkts) – des Prinzips, Sicherheit früher in die Prozesse zu integrieren, um die Lösung von Sicherheitsfragen einfacher und effektiver zu gestalten. Dies erfordert von allen Beteiligten (Sicherheits-, Geschäfts- und IT-Team) eine Änderung der Kultur, die von jedem Einzelnen verlangt, die Kultur und die Standards anderer Gruppen kennen zu lernen und gleichzeitig andere Gruppen über ihre eigene Kultur und eigene Standards zu informieren.

  Sicherheitsteams haben folgende Aufgaben:

  - **Kennenlernen** der Geschäfts- und IT-Ziele und Erfahren, warum jedes dieser Ziele wichtig ist und wie sie bei ihrer Transformation darüber nachdenken, wie sie erreicht werden können.
  - **Teilen** der Informationen, warum Sicherheit im Kontext dieser Geschäftsziele und Risiken wichtig ist, was andere Teams unternehmen können, um die Sicherheitsziele zu erreichen, und wie sie dabei vorgehen sollten.

  Auch wenn es keine leichte Aufgabe ist, so ist sie doch für die nachhaltige Sicherung der Organisation und ihrer Ressourcen unerlässlich. Diese Partnerschaft wird wahrscheinlich zu gesunden Kompromissen führen, bei denen anfangs nur die minimalen Sicherheits-, Geschäfts- und Zuverlässigkeitsziele erreicht werden können, die sich aber im Laufe der Zeit schrittweise und stetig verbessern.

- **Sicherheit ist ein ständiges Risiko, kein Problem.** Sie können Vergehen nicht „in Luft auflösen“. Im Kern ist Sicherheit nur eine Disziplin des Risikomanagements, die sich auf schädliche Aktionen von Personen und nicht auf natürliche Ereignisse konzentriert. Wie alle Risiken ist auch die Sicherheit kein Problem, das durch eine Lösung behoben werden kann, sondern eine Kombination aus der Wahrscheinlichkeit und den Auswirkungen von Schäden durch ein negatives Ereignis, einen Angriff. Sie ist am ehesten mit herkömmlicher Wirtschaftsspionage und kriminellen Aktivitäten vergleichbar, bei denen Organisationen mit motivierten menschlichen Angreifern konfrontiert sind, die einen finanziellen Anreiz haben, die Organisation erfolgreich anzugreifen.

- **Erfolg bei der Produktivität oder Sicherheit erfordert beides.** Eine Organisation muss sich in der heutigen Umgebung, in der Innovationen erforderlich sind, um nicht in der Bedeutungslosigkeit zu verschwinden, sowohl auf die Sicherheit als auch auf die Produktivität konzentrieren. Wenn die Organisation nicht produktiv ist und keine neuen Innovationen fördert, kann sie ihre Wettbewerbsfähigkeit auf dem Markt verlieren, wodurch sie finanziell geschwächt wird oder schließlich scheitert. Wenn die Organisation nicht sicher ist und die Kontrolle über die Ressourcen an Angreifer verliert, kann sie ihre Wettbewerbsfähigkeit auf dem Markt verlieren, was sie finanziell schwächt und schließlich scheitern lässt.

- **Niemand ist perfekt.** Keine Organisation ist bei der Einführung der Cloud perfekt, nicht einmal Microsoft. Die IT- und Sicherheitsteams von Microsoft haben mit vielen derselben Herausforderungen zu kämpfen, mit denen auch unsere Kunden zu kämpfen haben, z. B. die Ermittlung, wie Programme gut strukturiert werden können, wie ein Gleichgewicht zwischen der Unterstützung von Legacysoftware und der Unterstützung von innovativer Technologie erreicht wird und sogar wie Technologielücken bei Clouddiensten zu schließen sind. Während diese Teams lernen, wie sie die Cloud besser betreiben und sichern können, teilen sie aktiv ihre Erfahrungen über Dokumente wie dieses zusammen mit anderen auf der [IT Showcase-Website](https://www.microsoft.com/itshowcase), während sie unseren Technikerteams und Drittanbietern kontinuierlich Feedback geben, um ihre Angebote zu verbessern.

  Aufgrund unserer Erfahrung empfehlen wir, dass die Teams eher beständig Lernen und sich verbessern, anstatt Perfektion zu erwarten.

- **Gelegenheit bei der Transformation.** Es ist wichtig, die digitale Transformation als eine positive Gelegenheit für die Sicherheit zu betrachten. Obwohl es leicht ist, die potenziellen Nachteile und Risiken dieses Wandels zu erkennen, ist es auch leicht, die große Chance zu verpassen, die Rolle der Sicherheit neu zu definieren und sich einen Platz am Tisch zu verdienen, an dem Entscheidungen getroffen werden. Eine Kooperation mit dem Geschäft kann zu einer erhöhten Förderung der Sicherheit führen, unnötige, sich wiederholende Sicherheitsbemühungen reduzieren und die Arbeit im Sicherheitsbereich angenehmer gestalten, da sie stärker mit der Mission des Unternehmens verbunden ist.

## <a name="adopting-the-shared-responsibility-model"></a>Einführen des Modells der gemeinsamen Verantwortung

Beim Hosten von IT-Diensten in der Cloud werden die Verantwortlichkeiten für den Betrieb und die Sicherheit für Workloads zwischen dem Cloudanbieter und dem Kundenmandanten aufgeteilt, wodurch faktisch eine Partnerschaft mit gemeinsamen Verantwortlichkeiten entsteht. Alle Sicherheitsteams müssen dieses Modell der gemeinsamen Verantwortung studieren und verstehen, um ihre Prozesse, Tools und Qualifikationen an die neue Situation anzupassen. Dadurch wird vermieden, dass unbeabsichtigt Lücken oder Überschneidungen bei Ihrem Sicherheitsstatus entstehen, die zu Sicherheitsrisiken oder verschwendeten Ressourcen führen.

Dieses Diagramm veranschaulicht, wie die Verantwortlichkeiten für die Sicherheit zwischen Cloudanbietern und Cloudkundenorganisationen in einer faktischen Partnerschaft verteilt werden:

![Verteilte Verantwortlichkeiten für die Sicherheitstechnik](../_images/security/security-responsibilities.png)

Da es verschiedene Modelle von Clouddiensten gibt, hängen die Verantwortlichkeiten für jede Workload davon ab, ob sie in einem SaaS- (Software-as-a-Service), PaaS- (Platform-as-a-Service), IaaS- (Infrastructure-as-a-Service) oder in einem lokalen Rechenzentrum gehostet wird.

## <a name="building-security-initiatives"></a>Erstellen von Sicherheitsinitiativen

Dieses Diagramm veranschaulicht die drei primären Sicherheitsinitiativen, denen die meisten Sicherheitsprogramme folgen sollten, um ihre Sicherheitsstrategie und Sicherheitsprogrammziele für die Cloud anzupassen:

![Primäre Sicherheitsinitiativen](../_images/security/primary-security-initiatives.png)

Die Entwicklung eines resilienten Sicherheitsstatus in der Cloud erfordert mehrere parallele, sich ergänzende Ansätze:

- **Vertrauen ist gut – Kontrolle ist besser:** Bei den Verantwortlichkeiten, die der Cloudanbieter wahrnimmt, sollten Organisationen den Ansatz „Vertrauen ist gut – Kontrolle ist besser“ verfolgen. Organisationen sollten die Sicherheitsmethoden ihrer Cloudanbieter und die von ihnen angebotenen Sicherheitskontrollen auswerten, um sicherzustellen, dass der Cloudanbieter die Sicherheitsanforderungen der Organisation erfüllt.

- **Modernisieren der Infrastruktur- und Anwendungssicherheit:** Bei technischen Elementen, die von der Organisation kontrolliert werden, sollten Sie der Modernisierung der Sicherheitstools und den damit verbundenen Qualifikationen Vorrang einräumen, um Deckungslücken für die Sicherung von Ressourcen in der Cloud zu minimieren. Dies setzt sich aus zwei verschiedenen, sich ergänzenden Maßnahmen zusammen:

  - **Sicherheit der Infrastruktur:** Organisationen sollten die Cloud nutzen, um ihren Ansatz zum Schutz und zur Überwachung der gemeinsamen Komponenten zu modernisieren, die von vielen Anwendungen wie Betriebssystemen, Netzwerken und der Containerinfrastruktur verwendet werden. Diese Cloudfunktionen können oft auch die Verwaltung von Infrastrukturkomponenten sowohl in IaaS- als auch in lokalen Umgebungen umfassen. Die Optimierung dieser Strategie ist wichtig, da diese Infrastruktur eine Abhängigkeit von den darauf ausgeführten Anwendungen und Daten darstellt, die häufig kritische Geschäftsprozesse ermöglichen und entscheidende Geschäftsdaten speichern.
  - **Anwendungssicherheit:** Organisationen sollten auch die Art und Weise modernisieren, wie sie die eindeutigen Anwendungen und Technologien sichern, die von ihrer oder für ihre Organisation entwickelt werden. Mit der Einführung agiler DevOps-Prozesse, dem zunehmenden Einsatz von Open-Source-Komponenten und der Einführung von Cloud-APIs und Clouddiensten, die Anwendungskomponenten ersetzen oder Anwendungen miteinander verbinden, verändert sich diese Disziplin zusehends.

    Es ist entscheidend, hier richtig vorzugehen, da diese Anwendungen häufig kritische Geschäftsprozesse ermöglichen und entscheidende Geschäftsdaten speichern.

  - **Moderner Umkreis:** Organisationen sollten über einen umfassenden Ansatz zum Schutz von Daten über alle Workloads hinweg verfügen, Organisationen sollten einen modernen Umkreis von konsistenten, zentral verwalteten Identitätskontrollen einrichten, um ihre Daten, Geräte und Konten zu schützen. Dies wird stark beeinflusst durch eine Zero Trust-Strategie, die in [Modul 3 des CISO-Workshops](/security/ciso-workshop/ciso-workshop-module-3) ausführlich diskutiert wird.

### <a name="security-and-trust"></a>Sicherheit und Vertrauenswürdigkeit

Beachten Sie, dass die Verwendung des Worts *Vertrauen* im Kontext der Sicherheit verwirrend sein kann. In dieser Dokumentation wird auf zwei Arten darauf Bezug genommen, die nützliche Anwendungen dieses Konzepts veranschaulichen:

- [Zero Trust](https://www.microsoft.com/security/business/zero-trust) ist ein in der Branche gebräuchlicher Begriff für einen strategischen Sicherheitsansatz, der davon ausgeht, dass ein Unternehmens- oder Intranetnetzwerk schädlich ist (nicht vertrauenswürdig) und die Sicherheit entsprechend gestaltet.
- [Vertrauen ist gut – Kontrolle ist besser](https://wikipedia.org/wiki/trust,_but_verify) ist ein Ausdruck, der das Wesen zweier unterschiedlicher Organisationen erfasst, die trotz einiger anderer potenziell divergierender Interessen auf ein gemeinsames Ziel hinarbeiten. Damit werden viele der Nuancen der frühen Phasen der Partnerschaft mit einem kommerziellen Cloudanbieter für Organisationen prägnant erfasst.

Ein Cloudanbieter und seine Methoden und Prozesse können verantwortlich sein, vertragliche und rechtliche Anforderungen zu erfüllen, und könnten Vertrauen gewinnen oder verlieren. Ein Netzwerk ist eine nicht lebendige Verbindung, die keine Konsequenzen tragen kann, wenn sie von Angreifern ausgenutzt wird (ähnlich wie Sie eine Straße oder ein Auto nicht für Kriminelle zur Verantwortung ziehen können, die diese benutzen).

## <a name="how-cloud-is-changing-security-relationships-and-responsibilities"></a>Ändern der Sicherheitsbeziehungen und Verantwortlichkeiten durch die Cloud

Wie bei früheren Übergängen zu einer neuen Generation von Technologien wie Desktopcomputing und Unternehmensservercomputing stört der Übergang zum Cloudcomputing seit langem etablierte Beziehungen, Rollen, Verantwortlichkeiten und Qualifikationen. Die Aufgabenbeschreibungen, an die wir uns in den letzten Jahrzehnten gewöhnt haben, lassen sich nicht problemlos auf ein Unternehmen abbilden, das jetzt Cloudfunktionen umfasst. Da die Branche gemeinsam an der Normalisierung eines neuen Modells arbeitet, müssen sich die Organisationen darauf konzentrieren, so viel Klarheit wie möglich zu schaffen, um die Unsicherheit durch Mehrdeutigkeit in dieser Zeit des Wandels zu bewältigen.

Die Sicherheitsteams sind von diesen Veränderungen in den von ihnen unterstützten Geschäfts- und Technologiebereichen ebenso betroffen wie von ihren eigenen internen Modernisierungsbemühungen zur besseren Ausrichtung auf Bedrohungsakteure. Die Angreifer entwickeln sich aktiv weiter und suchen ständig nach den einfachsten Schwachstellen, die bei Personen, Prozessen und Technologien der Organisation ausgenutzt werden können, und die Sicherheit muss Funktionen und Qualifikationen entwickeln, um diese Aspekte anzugehen.

In diesem Abschnitt werden die wichtigsten Beziehungen beschrieben, die sich auf der Journey in die Cloud häufig ändern, einschließlich der Lektionen, die aus der Risikominimierung und der Ergreifung von Verbesserungsmöglichkeiten gelernt wurden:

- **Zwischen Sicherheit und Beteiligten im Unternehmen:** Die Führungskräfte im Sicherheitsbereich werden zunehmend mit der Geschäftsführung zusammenarbeiten müssen, um Organisationen in die Lage zu versetzen, Risiken zu reduzieren. Führungskräfte im Sicherheitsbereich sollten die Entscheidungsfindung in Unternehmen als fachlicher Ansprechpartner für Sicherheitsthemen (SMEs) unterstützen und danach streben, sich zu vertrauenswürdigen Beratern für diese Führungskräfte zu entwickeln. Diese Beziehung wird dazu beitragen, sicherzustellen, dass Unternehmensleiter Sicherheitsrisiken bei ihren Geschäftsentscheidungen berücksichtigen, den Sicherheitsbereich über Geschäftsprioritäten informieren und sicherstellen, dass Sicherheitsinvestitionen neben anderen Investitionen angemessen priorisiert werden.

- **Zwischen Führungskräften des Sicherheitsbereichs und Teammitgliedern:** Die Leitung des Sicherheitsbereichs sollte diese Erkenntnisse der Unternehmensführung an ihre Teams weitergeben, um ihre Investitionsprioritäten zu steuern.

  Indem sie statt auf eine klassischen kurzsichtige Beziehung auf die Zusammenarbeit mit Geschäftsführern und ihren Teams setzen, können die Führungskräfte im Sicherheitsbereich eine kontradiktorische Dynamik vermeiden, die sowohl Sicherheits- als auch Produktivitätsziele behindert.

  Führungskräfte im Sicherheitsbereich sollten bestrebt sein, ihrem Team Klarheit darüber zu verschaffen, wie sie ihre täglichen Entscheidungen hinsichtlich der Kompromisse bei Produktivität und Sicherheit handhaben sollen, da dies für viele in ihren Teams neu sein kann.

- **Zwischen Anwendungs- und Infrastrukturteams (und Cloudanbietern):** Diese Beziehung ist aufgrund der zahlreichen Trends in der IT- und Sicherheitsbranche, die darauf abzielen, die Innovationsgeschwindigkeit und Entwicklerproduktivität zu erhöhen, erheblichen Veränderungen unterworfen.

  Die alten Standards und betrieblichen Funktionen wurden gestört, aber es entstehen immer noch neue Standards und Funktionen, sodass wir empfehlen, die Mehrdeutigkeit zu akzeptieren, mit der aktuellen Denkweise Schritt zu halten und mit dem zu experimentieren, was für Ihre Organisationen funktionieren kann, bis es funktioniert. Es wird nicht empfohlen, in diesem Bereich „abzuwarten“, da dies einen erheblichen Wettbewerbsnachteil Ihrer Organisation bewirken könnte.

  Diese Trends stellen die traditionellen Standards für Rollen und Beziehungen von Anwendungen und Infrastruktur in Frage:

  - **DevOps verbindende Disziplinen:** Im Idealfall entsteht auf diese Weise ein einzelnes, hoch funktionelles Team, das beide Arten von Fachwissen zusammenbringt, um rasch Innovationen zu entwickeln, Updates herauszugeben und Probleme (sicherheitsbezogene und andere) zu lösen. Obwohl es einige Zeit dauern wird, bis dieser Idealzustand erreicht ist, und die Verantwortlichkeiten in der Mitte immer noch sehr unklar sind, profitieren die Organisationen aufgrund dieses kooperativen Ansatzes bereits jetzt von den Vorteilen einer raschen Freigabe. Microsoft empfiehlt, die Sicherheit in diesen Zyklus zu integrieren, um diese Kulturen kennenzulernen, Sicherheitserfahrungen auszutauschen und auf ein gemeinsames Ziel hinzuarbeiten, nämlich die rasche Freigabe sicherer und zuverlässiger Anwendungen.

  ![DevOps verbindende Disziplinen](../_images/security/devops-disciplines.png)

  - **Containerisierung wird zu einer allgemeinen Infrastrukturkomponente:** Anwendungen werden zunehmend von Technologien wie Docker, Kubernetes und ähnlichen Technologien gehostet und orchestriert. Diese Technologien vereinfachen die Entwicklung und Freigabe, indem sie viele Elemente der Einrichtung und Konfiguration des zugrunde liegenden Betriebssystems abstrahieren.

  ![Containerisierungsinfrastruktur](../_images/security/containerization.png)

  Während Container als eine von Entwicklungsteams verwaltete Anwendungsentwicklungstechnologie begannen, entwickelt sie sich zu einer gemeinsamen Infrastrukturkomponente, die sich zunehmend auf Infrastrukturteams verlagert. Dieser Übergang ist bei vielen Organisationen noch im Gange, aber es ist eine natürliche und positive Tendenz, dass viele der aktuellen Herausforderungen am besten mit traditionellen Infrastrukturfähigkeiten wie Netzwerk-, Speicher- und Kapazitätsverwaltung gelöst werden können.

  Infrastrukturteams und Mitglieder der Sicherheitsteams, die sie unterstützen, sollten mit Trainings, Prozessen und Tools ausgestattet werden, die bei der Verwaltung, Überwachung und Sicherung dieser Technologie helfen.

  - **Serverlose und Cloudanwendungsdienste:** Einer der derzeit vorherrschenden Trends in der Branche ist die Verringerung des Zeit- und Entwicklungsaufwands für die Erstellung oder Aktualisierung von Anwendungen.

    ![Serverlose und Cloudanwendungsdienste](../_images/security/serverless-model.png)

    Entwickler verwenden Clouddienste zunehmend auch für Folgendes:

    - Ausführen von Code, anstatt Apps auf virtuellen Computern (VMs) und Servern zu hosten.
    - Bereitstellen von Anwendungsfunktionen, anstatt eigene Komponenten zu entwickeln. Dies hat zu einem _serverlosen_ Modell geführt, das bestehende Clouddienste für allgemeine Funktionen nutzt. Die Anzahl und Vielfalt der Clouddienste (und ihr Innovationstempo) hat auch die Fähigkeit der Sicherheitsteams übertroffen, die Verwendung dieser Dienste auszuwerten und zu genehmigen, sodass sie vor der Wahl stehen, den Entwicklern die Nutzung eines beliebigen Dienstes zu gestatten, zu versuchen, die Entwicklungsteams daran zu hindern, nicht genehmigte Dienste zu verwenden, oder einen besseren Weg zu finden.
    - **Apps ohne Code und Power Apps:** Ein weiterer sich abzeichnender Trend ist der Einsatz von Technologien ohne Code wie Microsoft Power Apps. Diese Technologie ermöglicht es Personen ohne Programmierkenntnisse, Anwendungen zu erstellen, die Geschäftsergebnisse erzielen. Aufgrund dieser geringen Spannung und des hohen Wertpotenzials hat dieser Trend das Potenzial, schnell an Popularität zu gewinnen, und Sicherheitsexperten wären gut beraten, seine Auswirkungen schnell zu verstehen. Die Sicherheitsbemühungen sollten sich auf die Bereiche konzentrieren, in denen eine Person bei der Anwendung einen Fehler machen könnte, d. h. auf den Entwurf der Anwendungs- und Objektberechtigungen über die Bedrohungsmodellierung der Anwendungskomponenten, Interaktionen/Beziehungen und Rollenberechtigungen.

- **Zwischen Entwicklern und Autoren von Open Source-Komponenten:** Die Entwickler steigern auch die Effizienz, indem sie Open Source-Komponenten und -Bibliotheken verwenden, anstatt eigene Komponenten zu entwickeln. Dies bringt einen Mehrwert durch Effizienz, führt aber auch zu Sicherheitsrisiken, indem es eine externe Abhängigkeit schafft und die Anforderung stellt, diese Komponenten ordnungsgemäß zu warten und zu patchen. Die Entwickler gehen effektiv das Risiko von Sicherheits- und anderen Fehlern ein, wenn sie diese Komponenten verwenden, und müssen sicherstellen, dass es einen Plan gibt, der diese Fehler auf demselben Niveau mindert wie Code, den sie entwickeln würden.

- **Zwischen Anwendungen und Daten:** Die Grenze zwischen Daten- und Anwendungssicherheit verschwimmt stellenweise, und neue Bestimmungen machen eine engere Zusammenarbeit zwischen Daten-/Datenschutzteams und Sicherheitsteams erforderlich:

  - **Machine Learning-Algorithmen:** Machine Learning-Algorithmen ähneln insofern den Anwendungen, als sie darauf ausgelegt sind, Daten zu verarbeiten, um ein Ergebnis zu erzeugen. Folgende wichtige Unterschiede bestehen:

    - **Machine Learning mit hohem Wert:** Das maschinelle Lernen verschafft oft einen erheblichen Wettbewerbsvorteil und wird oft als vertrauliches geistiges Eigentum und Geschäftsgeheimnis betrachtet.

    - **Empfindlichkeitseindruck:** Beaufsichtigtes maschinelles Lernen wird mithilfe von Datasets optimiert, die dem Algorithmus Merkmale des Datasets verleihen. Aus diesem Grund kann der optimierte Algorithmus aufgrund des zum Training verwendeten Datasets als vertraulich angesehen werden. Wenn Sie z. B. einen Algorithmus für maschinelles Lernen trainieren würden, um geheime Armeestützpunkte auf einer Karte anhand eines Datasets geheimer Armeestützpunkte zu finden, wäre dies ein vertrauliches Objekt.

    > [!NOTE]
    > Nicht alle Beispiele sind offensichtlich, daher ist es entscheidend, ein Team mit den richtigen Beteiligten aus Data Science-Teams, Beteiligten im Unternehmen, Sicherheitsteams, Datenschutzteams und anderen zusammenzubringen. Diese Teams sollten die Verantwortung haben, gemeinsame Ziele der Innovation und Verantwortung zu erreichen. Sie sollten sich mit allgemeinen Problemen befassen, z. B. wie und wo Kopien von Daten in unsicheren Konfigurationen gespeichert werden sollen, wie Algorithmen zu klassifizieren sind, sowie mit allen Anliegen Ihrer Organisationen.
    >
    > Microsoft hat unsere [Grundsätze für eine verantwortungsvolle KI](https://www.microsoft.com/ai/responsible-ai) veröffentlicht, um unseren eigenen Teams und unseren Kunden einen Leitfaden zu bieten.

    - **Datenbesitz und Datenschutz:** Bestimmungen wie die DSGVO haben die Sichtbarkeit von Datenproblemen und Anwendungen erhöht. Anwendungsteams haben jetzt die Möglichkeit, vertrauliche Daten auf einem Niveau zu kontrollieren, zu schützen und zu verfolgen, das mit der Nachverfolgung von Finanzdaten durch Banken und Finanzinstitute vergleichbar ist. Datenbesitzer und Anwendungsteams müssen ein umfassendes Verständnis darüber entwickeln, welche Daten Anwendungen speichern und welche Kontrollen erforderlich sind.

- **Zwischen Organisationen und Cloudanbietern:** Wenn Unternehmen Workloads in der Cloud hosten, gehen sie mit jedem dieser Cloudanbieter eine Geschäftsbeziehung ein. Die Verwendung von Clouddiensten bringt oft einen geschäftlichen Nutzen wie:

  - **Beschleunigung von Initiativen zur digitalen Transformation** durch Verkürzung der Zeit bis zur Markteinführung neuer Funktionen.

  - **Steigerung des Werts von IT- und Sicherheitsaktivitäten**, indem die Teams sich auf höherwertige (geschäftsorientierte) Aktivitäten konzentrieren können, anstatt sich auf weniger anspruchsvolle Aufgaben konzentrieren zu müssen, die effizienter von Clouddiensten in ihrem Auftrag bereitgestellt werden.

  - **Höhere Zuverlässigkeit und Reaktionsfähigkeit:** Die meisten modernen Clouds weisen auch eine extrem hohe Betriebszeit im Vergleich zu traditionellen lokalen Rechenzentren auf und haben gezeigt, dass sie schnell skaliert werden können (z. B. während der COVID-19-Pandemie) und nach Naturereignissen wie Blitzeinschlägen (durch die viele lokale Äquivalente viel länger ausgefallen wären) eine entsprechende Resilienz bieten.

    Dieser Wechsel in die Cloud ist zwar äußerst vorteilhaft, aber nicht ohne Risiko. Wenn Organisationen Clouddienste einführen, sollten sie auch potenzielle Risikobereiche in Betracht ziehen:

  - **Business Continuity & Disaster Recovery:** Ist der Cloudanbieter finanziell gut aufgestellt und verfügt er über ein Geschäftsmodell, das während der Nutzung des Diensts durch Ihr Unternehmen wahrscheinlich überleben und wachsen wird? Hat der Cloudanbieter Vorkehrungen getroffen, um die Kundenkontinuität zu gewährleisten, falls der Anbieter finanzielle oder andere Ausfälle erleidet, z. B. bei der Bereitstellung ihres Quellcodes für andere Kunden oder bei dessen Freigabe als Open Source?

    Weitere Informationen und Dokumente zur finanziellen Integrität von Microsoft finden Sie unter [Microsoft Investor Relations](https://www.microsoft.com/investor).

  - **Sicherheit**: Befolgt der Cloudanbieter die bewährten Methoden der Branche hinsichtlich der Sicherheit? Wurde dies von unabhängigen Regulierungsbehörden überprüft?

    - [Microsoft Cloud App Security](/cloud-app-security/risk-score) ermöglicht es Ihnen, die Nutzung von über 16.000 Cloud-Apps zu ermitteln, die abhängig von mehr als 70 Risikofaktoren klassifiziert und bewertet werden, um Ihnen laufend Einblicke in die Cloudnutzung, Schatten-IT und das Risiko der Schatten-IT für Ihre Organisation zu gewähren.
    - Das [Microsoft Service Trust-Portal](https://servicetrust.microsoft.com) stellt Kunden Zertifizierungen zur Einhaltung gesetzlicher Bestimmungen, Überwachungsberichte, Penetrationstests und vieles mehr zur Verfügung. Diese Dokumente enthalten viele Details zu internen Sicherheitsmaßnahmen (insbesondere den SOC 2, Typ 2-Bericht und den Systemsicherheitsplan „FedRAMP Moderate“).

  - **Mitbewerber des Unternehmens:** Ist der Cloudanbieter ein bedeutender Mitbewerber in Ihrer Branche? Verfügen Sie über einen ausreichenden Schutz durch den Clouddienstvertrag oder andere Mittel, um Ihr Unternehmen vor potenziell feindlichen Aktionen zu schützen?

    Lesen Sie [diesen Artikel](https://www.cnbc.com/2019/03/16/why-volkswagen-chose-microsoft-azure-over-aws.html), um Kommentare zu erhalten, wie Microsoft den Wettbewerb mit Cloudkunden vermeidet.

  - **Verwenden mehrerer Clouds:** Viele Organisationen verfolgen faktisch oder absichtlich eine Multicloudstrategie. Dies kann ein absichtliches Ziel sein, um die Abhängigkeit von einem einzelnen Anbieter zu verringern oder um auf einzigartige Fähigkeiten zuzugreifen, kann aber auch passieren, wenn Entwickler bevorzugte oder vertraute Clouddienste gewählt haben oder Ihre Organisation ein anderes Unternehmen erworben hat. Unabhängig von den Gründen kann diese Strategie potenzielle Risiken und Kosten mit sich bringen, die es zu bewältigen gilt, einschließlich:

    - **Ausfallzeiten aufgrund mehrerer Abhängigkeiten:** Systeme, die so konzipiert sind, dass sie sich auf mehrere Clouds stützen, sind einem größeren Ausfallrisiko ausgesetzt, da Unterbrechungen bei den Cloudanbietern (oder bei der Nutzung durch Ihr Team) einen Ausfall bzw. eine Unterbrechung Ihres Geschäfts verursachen könnten. Diese erhöhte Systemkomplexität würde auch die Wahrscheinlichkeit von Störungsereignissen erhöhen, da die Teammitglieder ein komplexeres System wahrscheinlich weniger gut verstehen werden.
    - **Verhandlungsstärke:** Größere Organisationen sollten auch erwägen, ob eine Einzelcloudstrategie (gegenseitige Verpflichtung/Partnerschaft) oder eine Multicloudstrategie (Fähigkeit zur Verlagerung von Geschäften) einen größeren Einfluss auf ihre Cloudanbieter erzielt, damit die Featureanforderungen ihrer Organisation priorisiert werden.
    - **Erhöhter Wartungsaufwand:** Die IT- und Sicherheitsressourcen sind bereits jetzt durch ihre bestehende Workload und das Schritthalten mit den Änderungen einer einzelnen Cloudplattform überlastet. Jede zusätzliche Plattform erhöht diesen Zusatzaufwand noch weiter und führt dazu, dass die Teammitglieder von höherwertigen Aktivitäten wie der Rationalisierung technischer Prozesse zur Beschleunigung von Geschäftsinnovationen, der Beratung von Unternehmensgruppen zur effektiveren Nutzung von Technologien usw. abgezogen werden.
    - **Personalfragen und Training:** Organisationen berücksichtigen häufig nicht den Personalbedarf, der für die Unterstützung mehrerer Plattformen erforderlich ist, und das erforderliche Training zur Aufrechterhaltung des Wissens und der Aktualität von neuen Features, die in einem schnellen Tempo veröffentlicht werden.
