---
title: 'Cloudinnovation: Einbinden durch Anwendungen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Einführung in Cloudinnovation: Einbinden durch Anwendungen'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 3db2349e3c1da7c80f3089ea187a3de72d006d1f
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683283"
---
# <a name="engage-through-applications"></a>Einbinden durch Anwendungen

Wie im Artikel zum [Demokratisieren von Daten](./data.md) erläutert, sind Daten das neue Öl. Sie sind der Kraftstoff für die meisten Innovationen in der digitalen Wirtschaft. Im Rahmen dieser Analogie sind Anwendungen die Tankstellen und die Infrastruktur, die erforderlich sind, damit dieser Kraftstoff in die richtigen Hände gelangt.

In einigen Fällen reichen die Daten aus, um Änderungen voranzutreiben und die Kundenanforderungen zu erfüllen. In der Regel erfordert die Lösung für Kundenanforderungen, dass Anwendungen die Daten strukturieren und für Benutzerfreundlichkeit sorgen. Mit Anwendungen binden wir den Benutzer ein. Sie sind die Heimat der Prozesse, die erforderlich sind, um auf Auslöser der Kunden zu reagieren. Mit ihnen stellen Kunden Daten bereit und erhalten Anleitungen. In diesem Artikel werden einige Grundsätze erläutert, die Ihnen bei der Ausrichtung der richtigen Anwendungslösung auf Grundlage der zu validierenden Hypothesen helfen.

![Einbinden durch Apps](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Freigegebener Code

Teams, die schneller und präziser auf Kundenfeedback, Marktänderungen und Innovationschancen reagieren können, führen ihre Märkte innovativ. Das erste Prinzip innovativer Anwendungen wird in der [Übersicht zur Wachstumsmentalität](./learn.md#growth-mindset), „Freigeben des Codes“, erläutert. Innovation kann auf Dauer nur von einem kulturellen Fokus ausgehen. Um Innovationen aufrechtzuerhalten, sind unterschiedliche Perspektiven und Beiträge erforderlich.

Um für Innovationen bereit zu sein, sollte die gesamte Anwendungsentwicklung mit einem Repository für freigegebenen Code beginnen. Das gängigste Tool für die Verwaltung von Coderepositorys ist [GitHub](https://guides.github.com/), wo ein Repository für freigegebenen Code mit wenigen Klicks erstellt werden kann. Alternativ kann das Feature [Azure Repos](/azure/devops/repos/get-started/what-is-repos?view=azure-devops) von Azure DevOps zum Erstellen eines [Git](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git)- oder [Team Foundation](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc)-Repositorys verwendet werden.

## <a name="citizen-developers"></a>Entwickler ohne Programmiererfahrung

Professionelle Entwickler sind eine wichtige Komponente der Innovation. Wenn eine Hypothese bedarfsabhängig korrekt ist, müssen professionelle Entwickler die Lösung für die Skalierung stabilisieren und vorbereiten. Die meisten Prinzipien, auf die in diesem Artikel verwiesen wird, müssen von professionellen Entwicklern unterstützt werden. Leider deuten aktuelle Trends darauf hin, dass nicht genügend professionelle Entwickler zur Verfügung stehen. Außerdem können Kosten und Geschwindigkeit der Innovation ungünstiger sein, wenn die strengen Maßstäbe professioneller Entwicklung angewandt werden. Entwickler ohne Programmiererfahrung sind eine Alternative, um den Entwicklungsaufwand zu skalieren und frühe Hypothesetests zu beschleunigen.

Entwickler ohne Programmiererfahrung können ein sinnvoller Ansatz sein, wenn frühe Hypothesen mithilfe von Tools wie [PowerApps](https://docs.microsoft.com/powerapps/powerapps-overview) für App-Schnittstellen, [AI Builder](/powerapps/use-ai-builder) für Prozesse und Vorhersagen, [Microsoft Flow](https://docs.microsoft.com/flow) für Workflows oder [Power BI](https://docs.microsoft.com/power-bi) für den Datenverbrauch überprüft werden können.

> [!NOTE]
> Beim Einsatz von Entwicklern ohne Programmiererfahrung zum Testen von Hypothesen sollten professionelle Entwickler mit Unterstützung, Prüfung und Anleitung helfen. Sobald eine Hypothese bedarfsabhängig überprüft wird, beschleunigt ein Prozess, der die Anwendung in ein stabileres Programmiermodell überführt, die Rendite der Innovation. Wenn professionelle Entwickler in frühe Prozessdefinitionen einbezogen werden, können daraus später sauberere Übergänge resultieren.

## <a name="intelligent-experiences"></a>Intelligente Umgebungen

Intelligente Umgebungen kombinieren die Geschwindigkeit und Skalierung moderner Webanwendungen mit der Intelligenz von Cognitive Services und Bots. Jedes einzelne kann aber möglicherweise ausreichen, um die Anforderungen Ihrer Kunden zu erfüllen. In der Kombination wird das Spektrum von Anforderungen erweitert, die durch eine digitale Umgebung erfüllt werden können, aber die Entwicklungsinvestitionen können dennoch in Grenzen gehalten werden.

### <a name="modern-web-apps"></a>Moderne Web-Apps

Wenn eine Anwendung oder Umgebung erforderlich ist, um eine Kundenanforderung zu erfüllen, können moderne Webanwendungen die schnellste Möglichkeit bieten, diese Anforderung zu erfüllen. Moderne Webumgebungen können interne oder externe Kunden schnell einbinden und eine schnelle Iteration für die Lösung ermöglichen.

### <a name="infusing-intelligence"></a>Implementieren von Intelligenz

Maschinelles Lernen und künstliche Intelligenz stehen Entwicklern zunehmend zur Verfügung. Die weit verbreitete Verfügbarkeit gängiger APIs mit Vorhersagefunktionen ermöglicht Entwicklern, die Anforderungen des Kunden durch erweiterten Zugriff auf Daten und Vorhersagen besser zu erfüllen.

Durch Hinzufügen von Intelligenz zu einer Lösung können Spracherkennung, Textübersetzung, maschinelles Sehen und sogar visuelle Suche aktiviert werden. Dank dieser erweiterten Funktionen können Entwickler einfacher Lösungen erstellen, die Intelligenz nutzen, um eine interaktive und moderne Umgebung zu schaffen.

### <a name="bots"></a>Bots

Bots bieten eine Benutzeroberfläche, die weniger an die Verwendung eines Computers und mehr an den Umgang mit einer Person erinnern – oder zumindest einem intelligenten Roboter. Sie können verwendet werden, um einfache, sich wiederholende Aufgaben, z.B. das Aufnehmen einer Tischreservierung zum Abendessen oder das Erfassen von Profilinformationen auf automatisierte Systeme zu übertragen, die u.U. keinen direkten Benutzereingriff mehr erfordern. Benutzer kommunizieren mit einem Bot mithilfe von Text, interaktiven Karten und Spracheingabe/-ausgabe. Bei einer Botinteraktion kann es sich um eine kurze Frage und Antwort oder auch um eine komplexe Konversation handeln, die auf intelligente Weise den Zugriff auf Dienste bereitstellt.

Bots sind mit modernen Webanwendungen im Internet vergleichbar, die APIs zum Senden und Empfangen von Nachrichten verwenden. Der Inhalt eines Bots fällt je nach Art des Bot sehr unterschiedlich aus. Moderne Botsoftware basiert auf einen Stapel von Technologien und Tools, um zunehmend komplexe Funktionen auf einer Vielzahl von Plattformen bereitzustellen. Allerdings kann ein einfacher Bot auch nur eine Nachricht erhalten und an den Benutzer zurückgeben, wobei sehr wenig Code zum Einsatz kommt.

Bots sind zu denselben Dingen wie andere Arten von Software in der Lage – Lesen und Schreiben von Dateien, Verwenden von Datenbanken und APIs und Durchführen von regulären Berechnungsaufgaben. Was Bots einzigartig macht, ist die Verwendung von Mechanismen, die in der Regel auf die Kommunikation zwischen Menschen beschränkt sind.

## <a name="cloud-native-solutions"></a>Cloudnative Lösungen

Cloudnative Anwendungen werden von Grund auf neu erstellt. Cloudnative Anwendungen sind für Cloudskalierung und Leistung optimiert. Cloudnative Anwendungen werden in der Regel mithilfe eines Microservices-, serverlosen, ereignisbasierten oder containerbasierten Ansatzes erstellt. In den meisten Fällen nutzen cloudnative Lösungen eine Kombination aus Microservicesarchitekturen, verwalteten Diensten und Continuous Delivery, um Zuverlässigkeit und schnellere Markteinführungszeit zu erzielen.

Eine cloudnative Lösung ermöglicht zentralisierten Entwicklungsteams, die Kontrolle über die Geschäftslogik aufrechtzuerhalten, ohne dass monolithische zentralisierte Lösungen benötigt werden. Diese Art von Lösung erleichtert auch, die Konsistenz zwischen Entwicklern ohne Programmiererfahrung und modernen Umgebungen zu steuern. Außerdem sind cloudnative Lösungen Innovationsbeschleuniger, indem sie Entwicklern ohne Programmiererfahrung und professionellen Entwicklern die sichere Innovation mit minimalen Blockierungen ermöglichen.

## <a name="innovate-through-existing-solutions"></a>Innovationen durch vorhandene Lösungen

Viele Kundenhypothesen können am besten durch eine modernisierte Version einer vorhandenen Lösung bereitgestellt werden. Wenn die aktuelle Geschäftslogik den Anforderungen des Kunden entspricht (oder wirklich nahe kommt), können Sie Innovationen beschleunigen, indem Sie auf einer modernisierten Lösung aufbauen.

Die meisten Formen der Modernisierung, einschließlich eines geringfügigen Refactoring der Anwendung, sind in der [Migrationsmethodik](../../migrate/index.md) innerhalb des Cloud Adoption Framework enthalten. Diese Methodik führt Cloudeinführungsteams durch die Prozesse zum Migrieren einer [digitalen Ressource](../../digital-estate/index.md) in die Cloud. Der [Leitfaden zur Azure-Migration](../../migrate/azure-migration-guide/index.md) bietet einen optimierten Ansatz für dieselbe Methodik, der für eine kleine Anzahl von Workloads oder sogar für eine einzelne Anwendung geeignet ist.

Nach der Migration und Modernisierung gibt es eine Vielzahl von Möglichkeiten, wie die Lösung zur Erstellung neuer innovativer Lösungen für Kundenanforderungen genutzt werden könnte. Beispielsweise könnten [Entwickler ohne Programmiererfahrung](#citizen-developers) Hypothesen testen, oder professionelle Entwickler könnten [intelligente Umgebungen](#intelligent-experiences) oder [cloudnative Lösungen](#cloud-native-solutions) erstellen.

### <a name="extend-an-existing-solution"></a>Erweitern einer vorhandenen Lösung

Das Erweitern einer Lösung ist eine gängige Form der Modernisierung. Diese Vorgehensweise kann der schnellste Weg zu Innovationen sein, wenn Folgendes für die Kundenhypothese zutrifft:

- Die vorhandene Geschäftslogik sollte die vorhandene Kundenanforderung erfüllen (oder dem nahekommen).
- Eine verbesserte Benutzerfreundlichkeit würde die Anforderungen einer bestimmten Kundenkohorte besser erfüllen.
- Die Geschäftslogik, die für die MVP-Lösung erforderlich ist, wurde zentralisiert, üblicherweise über einen [N-Schichten](/azure/architecture/guide/architecture-styles/n-tier)-, Webdienste-, API- oder [Microservices](/azure/architecture/guide/architecture-styles/microservices)-Entwurf. Dieser Ansatz besteht darin, die vorhandene Lösung mit einer neuen, in der Cloud gehosteten Umgebung zu umschließen. In Azure befände sich diese Lösung wahrscheinlich in Azure App Services.

### <a name="rebuild-an-existing-solution"></a>Neuerstellen einer vorhandenen Lösung

Wenn eine Anwendung nicht einfach erweitert werden kann, ist es möglicherweise erforderlich, die Lösung umzugestalten. Bei diesem Ansatz wird die Workload in die Cloud migriert. Nach der Migration werden Teile der Anwendung geändert oder dupliziert, als Webdienste oder [Microservices](/azure/architecture/guide/architecture-styles/microservices), die parallel zur vorhandenen Lösung bereitgestellt werden. Die parallele dienstbasierte Lösung könnte wie eine erweiterte Lösung behandelt werden. Diese Lösung würde einfach die vorhandene Lösung mit einer neuen, in der Cloud gehosteten Umgebung umschließen. In Azure befände sich diese Lösung wahrscheinlich in Azure App Services.

> [!CAUTION]
> Das Refactoring bzw. Neuentwerfen von Lösungen oder Zentralisieren von Geschäftslogik kann, im Gegensatz zu einer Kundenwertquelle, schnell zu einer zeitaufwändigen [technischen Spitze](./build.md#reduce-complexity-and-delay-technical-spikes) werden. Dies ist ein Risiko für die Innovation, insbesondere in der Frühphase der Hypothesenvalidierung. Mit etwas Kreativität beim Entwerfen einer Lösung sollte ein Pfad zum MVP vorhanden sein, der kein Refactoring vorhandener Lösungen erfordert. Es ist ratsam, das Refactoring zu verzögern, bis die anfängliche Hypothese bedarfsabhängig überprüft werden kann.

## <a name="operating-model-innovations"></a>Betriebsmodellinnovationen

Zusätzlich zu modernen Innovationsansätzen für die Erstellung von Apps gab es Innovationen in Bezug auf den Einsatz von Apps. Die Ansätze haben viele organisatorische Bewegungen angeregt. Eine der herausragendsten ist eine Bewegung zu [Cloudkompetenzzentrum](../../organize/cloud-center-of-excellence.md)-Betriebsmodellen. Wenn die Geschäftsteams vollständig personell ausgestattet und ausgereift sind, können sie ihre eigene betriebliche Unterstützung für eine Lösung bereitstellen.

Der Typ des Self-Service-Betriebsverwaltungsmodells in einem Cloudkompetenzzentrum ermöglicht strengere Kontrollen und schnellere Iterationen innerhalb der Lösungsumgebung. Dies wird durch Übertragung betrieblicher Kontrolle und Verantwortlichkeit an das Geschäftsteam erreicht.

Wenn das Ziel darin besteht, die globale Nachfrage nach einer vorhandenen Lösung zu skalieren oder zu erfüllen, kann dieser Ansatz ausreichen, um eine Kundenhypothese zu validieren. Nach Migration und leichter Modernisierung könnte das Geschäftsteam Lösungen skalieren, um eine Vielzahl von Hypothesen hinsichtlich Kundenkohorten bezüglich Leistung, globaler Verteilung oder anderer Kundenanforderungen zu testen, die durch IT-Vorgänge behindert werden.

## <a name="reduce-overhead-and-management"></a>Reduzierung von Mehraufwand und Verwaltung

Je mehr in einer Lösung verwaltet werden muss, desto langsamer wird die Lösung durchlaufen. Beschleunigen Sie die Innovation, indem Sie die Auswirkungen reduzieren, die Vorgänge auf die verfügbare Geschwindigkeit haben.

Zur Vorbereitung auf die vielen Iterationen, die für die Bereitstellung einer innovativen Lösung erforderlich sind, ist vorausschauendes Denken wichtig. Minimieren Sie die Betriebsbelastungen frühzeitig im Prozess, indem Sie serverlose Optionen bevorzugen.

In Azure könnten serverlose Anwendungsoptionen [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) oder [Container](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql) beinhalten.

Parallel bietet Azure serverlose Transaktionsdatenoptionen, die ebenfalls den Mehraufwand reduzieren. Die [Liste der Datenbankprodukte](https://docs.microsoft.com/azure/#pivot=products&panel=databases) stellt Optionen zum Hosten von Daten bereit, ohne dass eine vollständige Datenplattform erforderlich ist.

## <a name="next-steps"></a>Nächste Schritte

Je nach Hypothese und Lösung können die in diesem Artikel erwähnten Prinzipien das Entwerfen von Apps unterstützen, die MVP-Definitionen erfüllen und Benutzer einbinden. Im nächsten Schritt werden die Prinzipien erläutert, die die [Einführung unterstützen](./ci-cd.md), und Sie erfahren, wie Sie die Anwendung und die Daten schneller den Kunden zur Verfügung stellen können.

> [!div class="nextstepaction"]
> [Unterstützen der Einführung](./ci-cd.md)
