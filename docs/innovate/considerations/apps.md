---
title: Interagieren über Apps für digitale Innovationen
description: Hier erfahren Sie, wie Sie Anwendungslösungen erstellen, um Daten zu strukturieren und Umgebungen zu schaffen, die das Interesse von Kunden wecken und Innovationen unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: c3886327dcb809d28253ed978dde970b0fecb8af
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94880958"
---
# <a name="engage-via-applications"></a>Interagieren über Apps

Wie in [Demokratisieren von Daten](./data.md) erläutert, sind Daten das neue Öl. Sie sind der Kraftstoff für die meisten Innovationen in der digitalen Wirtschaft. Im Rahmen dieser Analogie sind Anwendungen die Tankstellen und die Infrastruktur, die erforderlich sind, damit dieser Kraftstoff in die richtigen Hände gelangt.

In einigen Fällen reichen die Daten allein aus, um Änderungen voranzutreiben und Kundenanforderungen zu erfüllen. In der Regel erfordert die Lösung von Kundenanforderungen, dass Anwendungen die Daten strukturieren und für Benutzerfreundlichkeit sorgen. Mit Apps interagieren wir mit den Benutzern, und sie sind die Heimat der Prozesse, die erforderlich sind, um auf Auslöser der Kunden zu reagieren. Mit Apps können Kunden Daten bereitstellen und Anleitungen erhalten. In diesem Artikel werden einige Grundsätze erläutert, die Ihnen bei der Ausrichtung der richtigen Anwendungslösung auf der Grundlage der zu validierenden Hypothesen helfen.

![Interagieren über Apps](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Freigegebener Code

Teams, die schneller und präziser auf Kundenfeedback, Marktänderungen und Innovationschancen reagieren können, führen in der Regeln ihre Märkte bei Innovationen an. Das erste Prinzip innovativer Anwendungen wird in der [Übersicht zur Wachstumsmentalität](./learn.md#growth-mindset) unter „Freigeben des Codes“, erläutert. Im Lauf der Zeit ergeben sich Innovationen aus dem kulturellen Fokus. Um Innovationen aufrechtzuerhalten, sind unterschiedliche Perspektiven und Beiträge erforderlich.

Um für Innovationen bereit zu sein, sollte die gesamte Anwendungsentwicklung mit einem Repository für freigegebenen Code beginnen. Das gängigste Tool für die Verwaltung von Coderepositorys ist [GitHub](https://guides.github.com), wo Sie sehr schnell ein Repository für freigegebenen Code erstellen können. Alternativ bietet [Azure Repos](/azure/devops/repos/get-started/what-is-repos?view=azure-devops) einen Satz von Tools zur Versionskontrolle in Azure DevOps Services, mit denen Sie Ihren Code verwalten können. Azure Repos stellt zwei Arten der Versionskontrolle bereit:

- [Git](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git): verteilte Versionskontrolle
- [Team Foundation-Versionskontrolle (TFVC):](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) zentrale Versionskontrolle

## <a name="citizen-developers"></a>Entwickler ohne Programmiererfahrung

Professionelle Entwickler sind eine wichtige Komponente der Innovation. Wenn eine Hypothese bedarfsabhängig korrekt ist, müssen professionelle Entwickler die Lösung für die Skalierung stabilisieren und vorbereiten. Die meisten Prinzipien, auf die in diesem Artikel verwiesen wird, müssen von professionellen Entwicklern unterstützt werden. Leider deuten aktuelle Trends darauf hin, dass nicht genügend professionelle Entwickler für die Nachfrage zur Verfügung stehen. Darüber hinaus können Kosten und Geschwindigkeit der Innovation ungünstiger ausfallen, wenn die strengen Maßstäbe professioneller Entwicklung angewandt werden. Als Reaktion auf diese Herausforderungen sind Entwickler ohne Programmiererfahrung eine Alternative, um den Entwicklungsaufwand zu skalieren und frühe Hypothesetests zu beschleunigen.

Der Einsatz von Entwicklern ohne Programmiererfahrung könnte sinnvoll sein, wenn frühe Hypothesen mithilfe von Tools wie [Power Apps](/powerapps/powerapps-overview) für App-Schnittstellen, [AI Builder](/powerapps/use-ai-builder) für Prozesse und Vorhersagen, [Microsoft Power Automate](/power-automate) für Workflows oder [Power BI](/power-bi) für den Datenverbrauch überprüft werden können.

> [!NOTE]
> Beim Einsatz von Entwicklern ohne Programmiererfahrung zum Testen von Hypothesen sollten einige professionelle Entwickler mit Unterstützung, Überprüfung und Anleitung helfen. Nachdem eine Hypothese bedarfsabhängig überprüft wurde, beschleunigt ein Prozess, der die Anwendung in ein stabileres Programmiermodell überführt, die Rendite der Innovation. Wenn professionelle Entwickler schon früh in die Prozessdefinitionen einbezogen werden, können daraus später sauberere Übergänge resultieren.

## <a name="intelligent-experiences"></a>Intelligente Umgebungen

Intelligente Umgebungen kombinieren die Geschwindigkeit und Skalierung moderner Webanwendungen mit der Intelligenz von Cognitive Services und Bots. Jede einzelne dieser Technologien kann aber möglicherweise ausreichen, um die Anforderungen Ihrer Kunden zu erfüllen. Wenn sie intelligent kombiniert werden, erweitern sie das Spektrum der Anforderungen, die durch eine digitale Erfahrung erfüllt werden können, während gleichzeitig die Budgets für die Entwicklungskosten eingehalten werden.

### <a name="modern-web-apps"></a>Moderne Web-Apps

Wenn eine Anwendung oder Umgebung erforderlich ist, um eine Kundenanforderung zu erfüllen, können moderne Webanwendungen die schnellste Möglichkeit darstellen, diese Anforderung zu erfüllen. Moderne Webumgebungen können interne oder externe Kunden schnell einbinden und eine schnelle Iteration für die Lösung ermöglichen.

### <a name="infusing-intelligence"></a>Implementieren von Intelligenz

Maschinelles Lernen und künstliche Intelligenz stehen den Entwicklern zunehmend zur Verfügung. Die weit verbreitete Verfügbarkeit gängiger APIs mit Vorhersagefunktionen ermöglicht Entwicklern, die Anforderungen des Kunden durch erweiterten Zugriff auf Daten und Vorhersagen besser zu erfüllen.

Durch Hinzufügen von Intelligenz zu einer Lösung können Spracherkennung, Textübersetzung, maschinelles Sehen und sogar visuelle Suche aktiviert werden. Dank dieser erweiterten Funktionen können Entwickler einfacher Lösungen erstellen, die Intelligenz nutzen, um eine interaktive und moderne Umgebung zu schaffen.

### <a name="bots"></a>Bots

Bots bieten eine Benutzeroberfläche, die weniger an die Verwendung eines Computers und mehr an den Umgang mit einer Person erinnern – oder zumindest einem intelligenten Roboter. Sie können verwendet werden, um einfache, sich wiederholende Aufgaben, wie z. B. das Annehmen einer Tischreservierung zum Abendessen oder das Erfassen von Profilinformationen auf automatisierte Systeme zu übertragen, die u. U. keinen direkten Benutzereingriff mehr erfordern. Benutzer kommunizieren mit einem Bot mithilfe von Text, interaktiven Karten und Sprache. Bei einer Botinteraktion kann es sich um eine kurze Frage und Antwort oder auch um eine komplexe Konversation handeln, die auf intelligente Weise Zugriff auf Dienste bereitstellt.

Bots sind mit modernen Webanwendungen vergleichbar: Sie sind über das Internet verfügbar und nutzen APIs zum Senden und Empfangen von Nachrichten. Der Inhalt eines Bots fällt je nach Art des Bot sehr unterschiedlich aus. Moderne Botsoftware basiert auf einem Stapel von Technologien und Tools, um zunehmend komplexe Funktionen auf den unterschiedlichsten Plattformen bereitzustellen. Allerdings kann ein einfacher Bot auch nur eine Nachricht erhalten und an den Benutzer zurückgeben, wobei sehr wenig Code zum Einsatz kommt.

Bots sind zu denselben Dingen wie andere Arten von Software in der Lage: Lesen und Schreiben von Dateien, Verwenden von Datenbanken und APIs und Durchführen von regulären Rechenaufgaben. Was Bots einzigartig macht, ist die Verwendung von Mechanismen, die in der Regel auf die Kommunikation zwischen Menschen beschränkt sind.

## <a name="cloud-native-solutions"></a>Cloudnative Lösungen

Cloudnative Anwendungen sind prinzipiell auf die Cloudskalierung und -leistung ausgerichtet und dafür optimiert. Cloudnative Anwendungen werden in der Regel mithilfe eines Microservices-, serverlosen, ereignisbasierten oder containerbasierten Ansatzes erstellt. In den meisten Fällen nutzen cloudnative Lösungen eine Kombination aus Microservicearchitekturen, verwalteten Diensten und Continuous Delivery, um Zuverlässigkeit und schnellere Markteinführungszeit zu erzielen.

Eine cloudnative Lösung ermöglicht zentralisierten Entwicklungsteams, die Kontrolle über die Geschäftslogik aufrechtzuerhalten, ohne dass monolithische, zentralisierte Lösungen benötigt werden. Diese Art von Lösung erleichtert auch, die Konsistenz zwischen den Eingaben von Entwicklern ohne Programmiererfahrung und modernen Umgebungen zu steuern. Außerdem sind cloudnative Lösungen Innovationsbeschleuniger, indem sie Entwicklern ohne Programmiererfahrung und professionellen Entwicklern die sichere Innovation mit minimalen Hindernissen ermöglichen.

## <a name="innovate-through-existing-solutions"></a>Innovationen durch vorhandene Lösungen

Viele Kundenhypothesen können am besten durch eine modernisierte Version einer vorhandenen Lösung bereitgestellt werden. Wenn die aktuelle Geschäftslogik den Anforderungen des Kunden entspricht (oder sehr nahe kommt), können Sie Innovationen beschleunigen, indem Sie auf einer modernisierten Lösung aufbauen.

Die meisten Formen der Modernisierung, einschließlich eines geringfügigen Refactoring der Anwendung, sind in der [Migrationsmethodik](../../migrate/index.md) innerhalb des Cloud Adoption Framework enthalten. Diese Methodik führt Cloudeinführungsteams durch die Prozesse zum Migrieren einer [digitalen Ressource](../../digital-estate/index.md) zur Cloud. Der [Leitfaden zur Azure-Migration](../../migrate/azure-migration-guide/index.md) bietet einen optimierten Ansatz für dieselbe Methodik, der für eine kleine Anzahl von Workloads oder sogar für eine einzelne Anwendung geeignet ist.

Nach der Migration und Modernisierung einer Lösung gibt es eine Vielzahl von Möglichkeiten, wie diese zur Erstellung neuer innovativer Lösungen für Kundenanforderungen genutzt werden kann. Beispielsweise könnten [Entwickler ohne Programmiererfahrung](#citizen-developers) Hypothesen testen, oder professionelle Entwickler könnten [intelligente Umgebungen](#intelligent-experiences) oder [cloudnative Lösungen](#cloud-native-solutions) erstellen.

### <a name="extend-an-existing-solution"></a>Erweitern einer vorhandenen Lösung

Das Erweitern einer Lösung ist eine gängige Form der Modernisierung. Diese Vorgehensweise kann der schnellste Weg zu Innovationen sein, wenn Folgendes für die Kundenhypothese zutrifft:

- Die vorhandene Geschäftslogik sollte die vorhandene Kundenanforderung erfüllen (oder dem nahekommen).
- Eine verbesserte Benutzerfreundlichkeit würde die Anforderungen einer bestimmten Kundenkohorte besser erfüllen.
- Die Geschäftslogik, die für die MVP-Lösung (Minimum Viable Product) erforderlich ist, wurde zentralisiert – üblicherweise über einen [N-Schichten](/azure/architecture/guide/architecture-styles/n-tier)-, Webdienste-, API- oder [Microservices](/azure/architecture/guide/architecture-styles/microservices)-Entwurf. Dieser Ansatz besteht darin, die vorhandene Lösung mit einer neuen, in der Cloud gehosteten Umgebung zu umschließen. In Azure befände sich diese Lösung wahrscheinlich in Azure App Service.

### <a name="rebuild-an-existing-solution"></a>Neuerstellen einer vorhandenen Lösung

Wenn eine Anwendung nicht einfach erweitert werden kann, ist es möglicherweise erforderlich, die Lösung umzugestalten. Bei diesem Ansatz wird die Workload in die Cloud migriert. Nach der Migration der Anwendung werden Teile davon geändert oder dupliziert, als Webdienste oder [Microservices](/azure/architecture/guide/architecture-styles/microservices), die parallel zur vorhandenen Lösung bereitgestellt werden. Die parallele dienstbasierte Lösung könnte wie eine erweiterte Lösung behandelt werden. Diese Lösung würde einfach die vorhandene Lösung mit einer neuen, in der Cloud gehosteten Umgebung umschließen. In Azure befände sich diese Lösung wahrscheinlich in Azure App Service.

> [!CAUTION]
> Das Refactoring bzw. Neuentwerfen von Lösungen oder Zentralisieren von Geschäftslogik kann, im Gegensatz zu einer Kundenwertquelle, schnell zu einer zeitaufwendigen [technischen Herausforderung](./build.md#reduce-complexity-and-delay-technical-spikes) werden. Dies ist ein Risiko für die Innovation, insbesondere in der Frühphase der Hypothesenvalidierung. Mit etwas Kreativität beim Entwerfen einer Lösung sollte ein Pfad zum MVP vorhanden sein, der kein Refactoring vorhandener Lösungen erfordert. Es ist ratsam, das Refactoring zu verzögern, bis die anfängliche Hypothese bedarfsabhängig überprüft werden kann.

## <a name="operating-model-innovations"></a>Betriebsmodellinnovationen

Zusätzlich zu modernen, innovativen Ansätzen für die App-Erstellung gibt es auch einige bedeutende Neuerungen beim App-Betrieb. Diese Ansätze haben viele organisatorische Veränderungen angeregt. Eine der herausragendsten ist das Betriebsmodell [Cloudkompetenzzentrum](../../organize/cloud-center-of-excellence.md). Wenn die Geschäftsteams vollständig personell ausgestattet und ausgereift sind, können sie ihre eigene betriebliche Unterstützung für eine Lösung bereitstellen.

Der Typ des Self-Service-Betriebsverwaltungsmodells in einem Cloudkompetenzzentrum ermöglicht strengere Kontrollen und schnellere Iterationen innerhalb der Lösungsumgebung. Diese Ziele werden durch Übertragung betrieblicher Kontrolle und Verantwortlichkeit an das Geschäftsteam erreicht.

Wenn Sie versuchen, die globale Nachfrage nach einer vorhandenen Lösung zu skalieren oder zu erfüllen, kann dieser Ansatz ausreichen, um eine Kundenhypothese zu validieren. Nachdem eine Lösung migriert und etwas modernisiert wurde, kann sie vom Geschäftsteam skaliert werden, um verschiedene Hypothesen zu testen. Dies umfasst normalerweise Kundenkohorten, die sich Gedanken über die Leistung, die globale Verteilung und andere Kundenanforderungen machen, die durch IT-Vorgänge beeinträchtigt werden.

## <a name="reduce-overhead-and-management"></a>Reduzierung von Mehraufwand und Verwaltung

Je mehr in einer Lösung verwaltet werden muss, desto langsamer wird die Lösung durchlaufen. Das bedeutet, dass Sie die Innovation beschleunigen können, indem Sie die Auswirkungen von Vorgängen auf die verfügbare Bandbreite reduzieren.

Zur Vorbereitung auf die vielen Iterationen, die für die Bereitstellung einer innovativen Lösung erforderlich sind, ist vorausschauendes Denken wichtig. Minimieren Sie beispielsweise die Betriebsbelastungen frühzeitig im Prozess, indem Sie serverlose Optionen bevorzugen. In Azure könnten serverlose Anwendungsoptionen [Azure App Service](/azure/app-service/overview) oder [Container](/azure/containers) beinhalten.

Parallel bietet Azure serverlose Transaktionsdatenoptionen, die ebenfalls den Mehraufwand reduzieren. Der [Azure-Produktkatalog](/azure) bietet Datenbankoptionen, die Daten ohne eine vollständige Datenplattform hosten.

## <a name="next-steps"></a>Nächste Schritte

Je nach Hypothese und Lösung können die in diesem Artikel erwähnten Prinzipien das Entwerfen von Apps unterstützen, die MVP-Definitionen erfüllen und Benutzer einbinden. Im nächsten Schritt werden die Prinzipien erläutert, die die [Einführung unterstützen](./ci-cd.md) und Möglichkeiten bieten, wie Sie die Anwendung und die Daten den Kunden schneller und effizienter zur Verfügung stellen können.

> [!div class="nextstepaction"]
> [Unterstützen der Einführung](./ci-cd.md)
