---
title: 'Cloudinnovation: Erstellen mit Blick auf die Kundenanforderungen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Sie Lösungen mit Blick auf die Kundenanforderungen erstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5faaaf5b4c6b4c766c47dc6331723bed31e02d8e
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558300"
---
# <a name="build-with-customer-empathy"></a>Erstellen von Lösungen mit Blick auf die Kundenanforderungen

„Not macht erfinderisch“. Dieses Sprichwort verdeutlicht die Unverwüstlichkeit des menschlichen Geistes und unseren natürlichen Erfindungsdrang. Wie im Oxford English Dictionary erläutert wird: „Wenn der Bedarf für etwas zwingend erforderlich wird, ist man gezwungen, Wege zu finden, dieses Ziel umzusetzen oder zu erreichen“. Nur wenige würden diese universellen Wahrheiten über Erfindungsreichtum leugnen. Wie in der [innovativen Methodik](./index.md) beschrieben, erfordert Innovation jedoch ein Gleichgewicht zwischen **Erfindung** neuer und **Übernahme** vorhandener Technologien.

In Fortführung dieser Analogie stammen Innovationen aus einem größeren Bereich. *Kundenanforderungen sind ein wichtiger treibender Faktor für Innovationen.* Die Entwicklung einer Lösung, die Innovationen vorantreibt, erfordert einen berechtigten Kundenbedarf – einen Bedarf, der den Kunden dazu bringt, zurückzukehren, um kritische Kundenherausforderungen zu lösen. Diese Lösungen basieren auf den Bedürfnissen eines Kunden und nicht auf seinen Wünschen oder Launen. Um die wahren Bedürfnisse von Kunden zu ermitteln, beginnen wir mit Empathie – einem tiefen Verständnis für die Erfahrungen des Kunden. Empathie ist eine unterentwickelte soziale Kompetenz bei vielen Engineers, Produktmanagern und sogar Führungskräften. Glücklicherweise haben die vielfältigen Interaktionen und das rasante Tempo bei der Entwicklung der Rolle des Cloudarchitekten wahrscheinlich bereits den Anstoß dazu gegeben, dieses Einfühlungsvermögen zu entwickeln.

Warum ist Empathie so wichtig? Von der ersten Veröffentlichung eines Minimum Viable Product (MVP) bis hin zur allgemeinen Verfügbarkeit einer marktgerechten Lösung ermöglicht uns die Kundenempathie, die Erfahrungen des Kunden zu verstehen und zu teilen. Diese Empathie hilft uns dabei, eine bessere Lösung zu entwickeln. Noch wichtiger ist, dass Empathie uns besser positioniert, Lösungen zu **erfinden**, die die **Übernahme** von Technologien fördern. In einer digitalen Wirtschaft können diejenigen, die sich am schnellsten in die Kundenbedürfnisse einfühlen können, eine bessere Zukunft erschaffen, die den Markt neu definiert und anführt.

## <a name="how-to-build-with-empathy"></a>Entwickeln von Lösungen mit Empathie

Planung ist naturgemäß eine Übung zur Definition von Annahmen. Je mehr wir planen, desto mehr Annahmen werden sich in die Grundlage einer guten Idee einschleichen. Im Allgemeinen neigen Annahmen dazu, ein Produkt der Selbstempathie zu sein – mit anderen Worten: „Was würde ich wollen, wenn ich in dieser Position wäre“? Das Beginnen mit der Erstellungsphase minimiert die Zeit, in der Annahmen in eine Lösung einfließen können. Dies beschleunigt auch die Feedbackschleife durch echte Kunden, löst frühere Lernmöglichkeiten aus und stärkt die Empathie.

> [!CAUTION]
> Die richtige Definition dessen, was erstellt werden soll, kann schwierig sein und erfordert etwas Übung. Wenn Sie etwas zu schnell erstellen, kann es sein, dass die Lösung nicht den Kundenanforderungen entspricht. Wenn Sie zu viel Zeit damit verbringen, die anfänglichen Kundenbedürfnisse und Kundenlösungsanforderungen zu verstehen, kann der Markt den Bedarf decken, bevor Sie die Chance haben, überhaupt eine Lösung zu erstellen. In beiden Szenarien kann die Lernchance deutlich verzögert oder verringert werden. Manchmal können die Daten sogar beschädigt werden.

Die innovativsten Lösungen der Geschichte begannen mit einem intuitiven Glauben. Dieses Bauchgefühl beruht sowohl auf der vorhandenen Expertise als auch auf Beobachtungen aus erster Hand. Wir beginnen mit der Erstellung einer Lösung, da dies schnelles Testen dieser Intuition ermöglicht. Von dort aus können wir ein tieferes Verständnis und ein klareres Maß an Empathie entwickeln. Bei jeder Iteration oder Freigabe einer Lösung kommt das Gleichgewicht durch das Erstellen von MVPs zustande, die die Kundenempathie zeigen.

Um diesen Balanceakt zu unterstützen, werden in den folgenden beiden Abschnitten die Konzepte des Erstellens einer Lösung mit Empathie und des Definierens eines MVP erläutert.

### <a name="define-a-customer-focused-hypothesis"></a>Definieren einer kundenorientierten Hypothese

Das Erstellen einer Lösung mit Empathie bedeutet, dass Sie eine Lösung basierend auf definierten Hypothesen erstellen, die einen bestimmten Kundenbedarf veranschaulichen. Die folgenden Schritte helfen Ihnen, eine Hypothese zu formulieren, die zum Erstellen einer Lösung mit Empathie führt.

1. Beim Erstellen einer Lösung mit Empathie steht der Kunde immer im Mittelpunkt. Dies kann viele Formen annehmen. Sie können auf einen Kundenarchetypen, eine bestimmte Person oder sogar auf ein Bild eines Kunden inmitten des Problems verweisen, das Sie lösen möchten. Darüber hinaus können Kunden intern (Mitarbeiter oder Partner) oder extern (Konsumenten oder Geschäftskunden) sein. Diese Definition des Kunden ist die erste Hypothese, die getestet wird: Können Sie diesem spezifischen Kunden helfen?
2. An zweiter Stelle steht das Verständnis der Kundenerfahrung. Mit Empathie eine Lösung zu erstellen bedeutet, dass die Erfahrung des Kunden nachvollziehbar ist und die Herausforderung verstanden wird. Dies ist die nächste zu testende Hypothese: Können wir diesem spezifischen Kunden bei dieser zu bewältigenden Herausforderung helfen?
3. Drittens geht es darum, eine einfache Lösung für eine einzelne Herausforderung zu definieren. Das übergreifende Vertrauen auf Fachwissen von Personen und zu Prozessen und Technologiethemen führt zu einer möglichen Lösung. Dies ist die vollständige zu testende Hypothese: Können wir diesem spezifischen Kunden bei dieser zu bewältigenden Herausforderung mit der vorgeschlagenen Lösung helfen?
4. Der letzte Schritt beim Erstellen einer Lösung mit Empathie ist die Wertaussage. Welchen langfristigen Wert möchten Sie für diese Kunden bereitstellen? Die Antwort auf diese Frage ergibt Ihre vollständige Hypothese: Wie wird sich das Leben von Kunden verbessern, wenn sie die vorgeschlagene Lösung nutzen, um diese zu bewältigende Herausforderung anzugehen?

Der letzte Schritt ist der Höhepunkt einer durch Empathie gesteuerten Hypothese. Dabei werden die Zielgruppe, das Problem, die Lösung und die Metrik definiert, anhand derer eine Verbesserung vorgenommen werden muss, in deren Zentrum der Kunde steht. Während der Measure- und Lernphasen sollte jede Hypothese getestet werden. Änderungen beim Kunden, bei der Problemstellung oder bei der Lösung werden erwartet, wenn das Team mehr Empathie für den angesprochenen Kundenstamm entwickelt.

> [!CAUTION]
> Das Ziel besteht darin, eine Lösung mit Kundenempathie zu _erstellen_, nicht mit Kundenempathie zu _planen_. Es ist leicht, in endlosen Zyklen der Planung und Optimierung stecken zu bleiben, um die perfekte Aussage zur Kundenempathie zu finden. Bevor Sie mit der Entwicklung einer solchen Aussage beginnen, lesen Sie die folgenden beiden Abschnitte zum Definieren und Erstellen eines MVP.

Sobald die Kernannahmen nachgewiesen werden können, konzentrieren sich die späteren Iterationen auf Wachstumstests zusätzlich zu den Empathietests. Sobald eine Lösung mit Empathie erstellt, getestet und überprüft wurde, können wir damit beginnen, den angesprochenen Markt im richtigen Maßstab zu verstehen. Dies kann durch eine Erweiterung einer der oben genannten Standardhypothesenformeln erreicht werden. Schätzen Sie auf der Grundlage der verfügbaren Daten die Größe des Gesamtmarkts (d.h. die Anzahl der potenziellen Kunden). Schätzen Sie von dort aus den Prozentsatz des Gesamtmarkts, der eine ähnliche Herausforderung erfährt und an dieser Lösung interessiert sein könnte, wenn sie die Herausforderung lösen kann. Dies ist Ihr angesprochener Markt. Die nächste zu testende Hypothese lautet: Wie wird sich das Leben von _x %_ von Kunden verbessern, wenn sie die vorgeschlagene Lösung nutzen, um diese zu bewältigende Herausforderung anzugehen? Eine kleine Auswahl von Kunden wird wichtige Indikatoren aufzeigen, die einen prozentualen Einfluss auf die betroffenen Kunden anzeigen.

### <a name="define-a-solution-to-test-the-hypothesis"></a>Definieren einer Lösung zum Testen der Hypothese

Bei jeder Iteration einer Feedbackschleife aus Erstellen, Messen und Lernen wird der Versuch, eine Lösung mit Empathie zu erstellen, durch ein MVP (Minimum Viable Product) definiert.

Ein Minimum Viable Product (MVP) ist die kleinste Einheit des Aufwands (Erfindung, Engineering, Anwendungsentwicklung oder Datenarchitektur), um genügend Anteile einer Lösung zu schaffen, um _mit dem Kunden_ zu lernen. Das Ziel jedes MVP besteht darin, einige oder alle der vorherigen Hypothese zu testen und Feedback direkt vom Kunden zu erhalten. Das Ergebnis ist keine elegante Anwendung mit allen Funktionen, die erforderlich sind, um Ihre Branche zu verändern. Das gewünschte Ergebnis jeder Iteration ist eine Lernmöglichkeit: eine Chance, eine Hypothese eingehender zu testen.

Eine gängige Methode, um sicherzustellen, dass ein Produkt minimal ist, ist das Festlegen eines Zeitrahmens bei der Lösungserstellung. Stellen Sie sicher, dass das Entwicklungsteam glaubt, dass die Lösung in einer einzigen Iteration erstellt werden kann, um einen schnellen Test zu ermöglichen. Um die Verwendung von Geschwindigkeit, Iterationen und Releases zur Definition der minimalen Mittel besser zu verstehen, lesen Sie [Planen von Geschwindigkeit, Iterationen, Release und Iterationspfaden](../../plan/iteration-paths.md).

### <a name="reduce-complexity-and-delay-technical-spikes"></a>Reduzieren der Komplexität und Verzögern von technische Spitzen

Die [Innovationsdisziplinen](./invention.md) der [innovativen Methodik](./index.md) beschreiben die Funktionalität, die häufig benötigt wird, um eine ausgereifte innovative oder skalierungsfähige MVP-Lösung bereitzustellen. Verwenden Sie diese Disziplinen als langfristigen Leitfaden für die Einbindung von Features. Verwenden Sie sie auch als Vorsichtshinweis bei der frühen Prüfung des Kundennutzens und der -empathie in Ihrer Lösung.

Die Featurebreite und die verschiedenen Innovationsdisziplinen können nicht alle in einer einzigen Iteration erstellt werden. Häufig werden mehrere Releases für eine MVP-Lösung benötigt, um die Komplexität mehrerer Disziplinen einzubeziehen. Abhängig von der Investition in die Entwicklung kann es mehrere parallele Teams geben, die in verschiedenen Disziplinen arbeiten, um mehrere Hypothesen zu testen. Auch wenn es ratsam ist, die architektonische Ausrichtung zwischen diesen Teams zu koordinieren, ist es unklug, komplexe integrierte Lösungen zu versuchen, bevor Werthypothesen validiert werden können.

Komplexität wird am besten anhand der Häufigkeit oder Menge von **technischen Spitzen** erkannt. Technische Spitzen sind Bemühungen, technische Lösungen zu schaffen, die nicht einfach mit Kunden getestet werden können. Wenn Kundenwert und Kundenempathie nicht getestet werden, stellen technische Spitzen ein Risiko für Innovationen dar und sollten nach Möglichkeit minimiert werden. Für die Arten von ausgereiften, getesteten Lösungen, die bei einem Migrationsansatz zu finden sind, können technische Spitzen während der gesamten Umsetzung häufig auftreten. Allerdings verzögern sie das Testen von Hypothesen in Innovationsbemühungen und sollten nach Möglichkeit zurückgestellt werden.

Für jede MVP-Definition wird ein konsequenter Vereinfachungsansatz vorgeschlagen. Unermüdliche Vereinfachung ist die Entfernung von allen Aspekten, die nicht zu Ihrer Fähigkeit beitragen, die Hypothese zu bestätigen. Um die Komplexität zu minimieren, verringern Sie Integrationen und Features, die zum Testen der Hypothese nicht erforderlich sind.

### <a name="build-a-minimum-viable-product-mvp"></a>Erstellen eines MVP (Minimum Viable Product)

Bei jeder Iterationen kann eine MVP-Lösung viele verschiedene Formen annehmen. Eine häufige Anforderung besteht lediglich darin, dass das Ergebnis das Messen und Testen der Hypothese ermöglicht. Diese einfache Anforderung initiiert den wissenschaftlichen Prozess und ermöglicht es dem Team, mit Empathie eine Lösung zu entwickeln. Um diese kundenorientierte Ausrichtung zu erreichen, kann sich ein anfängliches MVP auf nur eine der [Disziplinen der Innovation](./invention.md) stützen.

In einigen Fällen ist der schnellste Weg zur Innovation die vorübergehende vollständige Vermeidung dieser Disziplinen, bis das Cloud Adoption-Team überzeugt ist, dass die Hypothese sorgfältig überprüft wurde. Von einem Technologieunternehmen wie Microsoft stammend, mag diese Empfehlung kontraintuitiv klingen. Das Ziel dieser Aussage ist es, zu betonen, dass die Kundenbedürfnisse und nicht eine bestimmte Technologieentscheidung die höchste Priorität in einer MVP-Lösung haben sollten.

Im Allgemeinen besteht eine MVP-Lösung aus einer einfachen Web-App oder Datenlösung mit minimalen Funktionen und begrenztem Feinschliff. Für Unternehmen, die über professionelle Entwicklungskompetenz verfügen, ist dies oft der schnellste Weg zum Lernen und Iterieren. Nachfolgend werden einige andere Ansätze aufgeführt, die ein Team beim Erstellen eines MVP anwenden kann:

- Ein Vorhersagealgorithmus, der in 99 % der Fälle falsch ist, aber spezifische gewünschte Ergebnisse zeigt.
- Ein IoT-Gerät, das nicht sicher in Produktionsumgebungen kommunizieren würde, aber den Mehrwert von Daten in nahezu Echtzeit innerhalb eines Prozesses aufzeigen kann.
- Eine Anwendung, die von einem Citizen Developer entwickelt wurde, um eine Hypothese zu testen oder kleinere Anforderungen zu erfüllen.
- Ein manueller Prozess, der die Vorteile der zu verfolgenden Anwendung erneut erstellt.
- Ein Drahtmodell oder Video, das detailliert genug ist, um dem Kunden die Interaktion zu ermöglichen.

Die Entwicklung eines MVP sollte keine großen Entwicklungsinvestitionen erfordern. Vorzugsweise sollten die Investitionen so weit wie möglich eingeschränkt werden, um die Anzahl der Hypothesen, die gleichzeitig getestet werden, zu minimieren. Dann wird die Lösung in jeder Iteration und mit jedem Release bewusst in Richtung einer skalierbaren Lösung verbessert, die mehrere Innovationsdisziplinen darstellt.

### <a name="accelerate-mvp-development"></a>Beschleunigen der MVP-Entwicklung

Die Markteinführungszeit ist entscheidend für den Erfolg jeder Innovation. Schnellere Releases führen zu schnellerem Lernen. Schnelleres Lernen führt zu Produkten, die schneller skalierbar sind. Manchmal kann dieser Prozess durch herkömmliche Anwendungsentwicklungszyklen verlangsamt werden. Häufiger jedoch werden Innovationen durch das verfügbare Fachwissen eingeschränkt. Budgets, Mitarbeiterzahl und Verfügbarkeit der Mitarbeiter können die Anzahl der neuen Innovationen, die ein Team bewältigen kann, begrenzen.

Personalengpässe und der Wunsch, Lösungen mit Empathie zu erstellen, haben einen schnell wachsenden Trend zu Citizen Developers ausgelöst. Diese Entwickler verringern Risiken und bieten Skalierbarkeit innerhalb der professionellen Entwicklungscommunity einer Organisation. Citizen Developer sind Experten im Hinblick auf die Kundenerfahrung, aber sie sind nicht als Engineers ausgebildet. Diese Personen verwenden Prototyptools oder einfachere Entwicklungstools, die von professionellen Entwicklern möglicherweise abgelehnt werden. Diese neue Generation von geschäftsorientierten Entwicklern erstellt MVP-Lösungen und testet Theorien. Wenn dieser Prozess gut aufeinander abgestimmt ist, kann er Produktionslösungen schaffen, die zwar einen Mehrwert bieten, aber keine effektiv ausreichende Skalierungshypothese bestehen. Sie können auch als Überprüfung eines Prototyps verwendet werden, bevor der Skalierungsaufwand beginnt.

Im Rahmen eines jeden Innovationsplans wird empfohlen, dass Cloud Adoption-Teams ihr Portfolio diversifizieren, um die Bemühungen von Citizen Developern zu berücksichtigen. Durch die Skalierung der Entwicklungsbemühungen können bei reduzierter Investition mehr Hypothesen aufgestellt und getestet werden. Wenn eine Hypothese validiert und ein Marktbedarf identifiziert ist, können professionelle Entwickler die Lösung mithilfe moderner Entwicklungstools härten und skalieren.

### <a name="final-build-gate-customer-pain"></a>Letztes Erstellungshindernis für die Lösung: Unbehagen des Kunden

Wenn die Kundenempathie stark ist, sollte ein klares Problem leicht zu erkennen sein. Das Unbehagen des Kunden sollte offensichtlich sein. Während der Erstellung des Projekts entwickelt das Cloud -Adoption-Team eine Lösung, um eine Hypothese basierend auf einem Pain Point des Kunden zu testen. Wenn die Hypothese klar definiert ist, der Pain Point aber nicht, dann basiert die Lösung nicht wirklich auf Kundenempathie. In diesem Szenario ist das Erstellen der Lösung nicht der richtige Ausgangspunkt. Investieren Sie stattdessen zunächst in den Aufbau von Empathie und das Lernen von echten Kunden. Der beste Ansatz für das Aufbauen von Empathie und das Überprüfen von Unbehagen ist einfach: Hören Sie den Kunden zu. Investieren Sie Zeit in Treffen mit und Beobachtung von Kunden, bis Sie einen häufig auftretenden Pain Point identifizieren können. Sobald der Pain Point verstanden ist, kann dieser Ansatz eine hypothetische Lösung zur Behandlung dieses Unbehagens testen.

## <a name="when-not-to-apply-this-approach"></a>Unter welchen Umständen dieser Ansatz nicht angewendet werden sollte

Es gibt viele gesetzliche, Compliance- und Branchenanforderungen, die einen alternativen Ansatz erfordern können. Wenn die öffentliche Freigabe einer Entwicklungslösung das Risiko für den Zeitpunkt des Patentschutzes, den Schutz des geistigen Eigentums, die Weitergabe von Kundendaten oder die Verletzung etablierter Complianceanforderungen mit sich bringt, dann ist dieser Ansatz möglicherweise nicht geeignet. Wenn vermeintliche Risiken wie diese bestehen, wenden Sie sich an einen Rechtsbeistand, bevor Sie einen gezielten Ansatz für die Releaseverwaltung anwenden.

## <a name="references"></a>Referenzen

Einige der Konzepte in diesem Artikel bauen auf Themen auf, die in _[The Lean Startup](http://theleanstartup.com/book) (Eric Ries, Crown Business, 2011)_ beschrieben werden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem eine MVP-Lösung erstellt wurde, können der Empathiewert und der Skalierungswert gemessen werden. Erfahren Sie, wie Sie die [Auswirkungen für Kunden berechnen](./measure.md).

> [!div class="nextstepaction"]
> [Berechnen der Auswirkungen für Kunden](./measure.md)
