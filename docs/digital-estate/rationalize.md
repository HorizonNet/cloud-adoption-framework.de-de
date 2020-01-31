---
title: Rationalisieren der digitalen Ressourcen
description: Bewerten Sie Ihre digitalen Ressourcen, um zu ermitteln, wie sich diese am besten in der Cloud hosten lassen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: c618e6c1cf83199ae55df44397e07f3755fbb1f8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76804553"
---
# <a name="rationalize-the-digital-estate"></a>Rationalisieren der digitalen Ressourcen

Bei der Rationalisierung der Cloud werden Ressourcen evaluiert, um die beste Vorgehensweise für das Hosten in der Cloud zu ermitteln. Nachdem Sie einen [Ansatz](./approach.md) ermittelt und einen [Bestand](./inventory.md) aggregiert haben, kann die Cloudrationalisierung beginnen. Unter „Cloudrationalisierung“ werden die häufigsten Rationalisierungsoptionen beschrieben.

## <a name="traditional-view-of-rationalization"></a>Herkömmlicher Rationalisierungsansatz

Die Rationalisierung ist leicht verständlich, wenn Sie sich den herkömmlichen Rationalisierungsprozess wie eine komplexe Entscheidungsstruktur vorstellen. Jedes Element der digitalen Ressourcen durchläuft einen Prozess, an dessen Ende eine von fünf möglichen Antworten („die fünf R“) steht. Für kleinere Ressourcenumgebungen funktioniert dieser Prozess gut. Bei größeren Ressourcenumgebungen ist er aber ineffizient und kann zu erheblichen Verzögerungen führen. Wir sehen uns den Prozess nun an, um den Grund dafür zu verdeutlichen. Anschließend stellen wir ein effizienteres Modell vor.

**Bestand:** Ein umfassender Ressourcenbestand – z.B. mit Anwendungen, Software, Hardware, Betriebssystemen und Systemleistungsmetriken – ist erforderlich, um mithilfe von herkömmlichen Modellen eine vollständige Rationalisierung zu erzielen.

**Quantitative Analyse:** In der Entscheidungsstruktur bilden quantitative Fragen die Grundlage der ersten Entscheidungsebene. Häufige Fragen umfassen Folgendes: Wird die Ressource derzeit genutzt? Wenn ja, ist sie optimiert, und hat sie die richtige Größe? Welche Abhängigkeiten bestehen zwischen Ressourcen? Diese Fragen sind für die Klassifizierung des Bestands von entscheidender Bedeutung.

**Qualitative Analyse:** Für die nächsten Entscheidungen wird menschliche Intelligenz in Form einer qualitativen Analyse benötigt. Oft gelten die hier gestellten Fragen nur speziell für die Lösung und können nur von Beteiligten des Unternehmens und Hauptbenutzern beantwortet werden. Diese Entscheidungen verzögern den Prozess normalerweise, wodurch die Dinge erheblich verlangsamt werden. Bei dieser Analyse werden in der Regel 40 bis 80 Vollzeitmitarbeiter-Stunden pro Anwendung verbraucht.

Eine Anleitung zum Erstellen einer Liste mit Fragen zur qualitativen Analyse finden Sie unter [Ansätze für die Planung digitaler Ressourcen](./approach.md).

**Rationalisierungsentscheidung:** In den Händen eines erfahrenen Rationalisierungsteams können anhand der qualitativen und quantitativen Daten klare Entscheidungen getroffen werden. Leider ist die Einstellung und Schulung von Teams mit viel Erfahrung im Bereich der Rationalisierung ein teurer bzw. mehrere Monate dauernder Prozess.

## <a name="rationalization-at-enterprise-scale"></a>Rationalisierung auf Unternehmensebene

Dieser Prozess ist schon bei einer digitalen Ressourcenumgebung mit 50 VMs zeitaufwändig und anspruchsvoll. Sie können sich sicherlich vorstellen, wie hoch dann der Aufwand für die Unternehmenstransformation in einer Umgebung mit Tausenden von VMs und Hunderten von Anwendungen ist. Der erforderliche Mitarbeiteraufwand kann sich leicht auf mehr als 1.500 Vollzeitmitarbeiter-Stunden und neun Monate Planung belaufen.

Die vollständige Rationalisierung ist der gewünschte Endzustand und sicherlich ein anzustrebendes Ziel, aber bezogen auf die erforderliche Zeit und Energie ergibt sich nur selten eine gute Rendite.

Falls die Rationalisierung eine hohe Bedeutung für finanzielle Entscheidungen hat, kann die Inanspruchnahme eines auf Cloudrationalisierung spezialisierten Dienstleistungsunternehmens erwogen werden, um den Prozess zu beschleunigen. Die Durchführung einer vollständigen Rationalisierung kann trotzdem noch teuer und zeitaufwändig sein und zur Verzögerung der Transformation oder von Geschäftsergebnissen führen.

Im weiteren Verlauf dieses Artikels wird ein alternativer Ansatz beschrieben, der als „inkrementelle Rationalisierung“ bezeichnet wird.

## <a name="incremental-rationalization"></a>Inkrementelle Rationalisierung

Die vollständige Rationalisierung von umfassenden digitalen Ressourcen ist risikoanfällig, und aufgrund der Komplexität kann es zu Verzögerungen kommen. Die Annahme beim inkrementellen Ansatz lautet, dass die Belastung für das Unternehmen durch verzögerte Entscheidungen gestaffelt wird, um das Risiko von Engpässen zu vermeiden. Bei diesem Ansatz wird im Laufe der Zeit ein natürliches Modell für die Entwicklung der erforderlichen Prozesse und der Benutzeroberfläche erstellt, damit fundierte Rationalisierungsentscheidungen auf effizientere Weise getroffen werden können.

### <a name="inventory-reduce-discovery-data-points"></a>Bestand: Reduzieren von Ermittlungsdatenpunkten

Nur wenige Organisationen investieren die Zeit, Energie und Kosten, die erforderlich sind, um einen präzisen Echtzeitbestand für die digitalen Ressourcen vorzuhalten. Verlust, Diebstahl, Aktualisierungszyklen und der Einstellungsprozess von Mitarbeitern sind häufige Gründe, um die ausführliche Nachverfolgung der Ressourcen auf Endbenutzergeräten zu rechtfertigen. Die Rendite (Return on Investment, ROI), die sich aus der Verwaltung eines präzisen Servers und Anwendungsbestands in einem herkömmlichen lokalen Datencenter ergibt, ist aber häufig nur gering. Die meisten IT-Organisationen müssen dringendere Probleme als die Nachverfolgung der Nutzung von festen Ressourcen in einem Datencenter lösen.

Bei einer Cloudtransformation korreliert der Bestand direkt mit den Betriebskosten. Für eine korrekte Planung werden genaue Bestandsdaten benötigt. Unglücklicherweise können Entscheidungen aufgrund der aktuell verfügbaren Optionen zum Scannen von Umgebungen um Wochen oder Monate verzögert werden. Glücklicherweise kann die Datensammlung durch einige Tricks beschleunigt werden.

Das Agent-basierte Scannen wird am häufigsten als Verzögerungsgrund genannt. Die stabilen Daten, die für eine herkömmliche Rationalisierung benötigt werden, können oft nur erfasst werden, indem auf jeder Ressource ein Agent ausgeführt wird. Diese Abhängigkeit von Agents führt oft zu einer Verlangsamung des Prozesses, weil unter Umständen Rückmeldungen aus den Bereichen Sicherheit, Betrieb und Verwaltung erforderlich sind.

Bei einem inkrementellen Rationalisierungsprozess kann eine Lösung ohne Agents für eine erste Ermittlung genutzt werden, um schneller erste Entscheidungen treffen zu können. Je nach dem Komplexitätsgrad in der Umgebung ist möglicherweise trotzdem eine agentbasierte Lösung erforderlich. Sie kann jedoch aus dem kritischen Pfad zu Geschäftsänderungen entfernt werden.

### <a name="quantitative-analysis-streamline-decisions"></a>Quantitative Analyse: Optimieren von Entscheidungen

Unabhängig vom Ansatz zur Ermittlung des Bestands kann die quantitative Analyse als Grundlage für erste Entscheidungen und Annahmen dienen. Dies ist vor allem beim Identifizieren der ersten Workload der Fall, oder wenn das Ziel der Rationalisierung ein allgemeiner Kostenvergleich ist. Bei einem inkrementellen Rationalisierungsprozess beschränken das Cloudstrategieteam und die Cloudeinführungsteams die [fünf „R“ der Rationalisierung](./5-rs-of-rationalization.md) auf zwei präzise Entscheidungen und wenden nur diese quantitativen Faktoren an. Dadurch wird die Analyse optimiert, und die Menge an anfänglichen Daten, die für die Laufwerksänderung erforderlich sind, wird verringert.

Wenn sich eine Organisation beispielsweise mitten in einer IaaS-Migration zur Cloud befindet, können Sie davon ausgehen, dass die meisten Workloads entweder außer Betrieb genommen oder neu gehostet werden.

### <a name="qualitative-analysis-temporary-assumptions"></a>Qualitative Analyse: Vorübergehende Annahmen

Indem die Anzahl von potenziellen Ergebnissen reduziert wird, ist es einfacher, eine erste Entscheidung zum zukünftigen Zustand einer Ressource zu treffen. Wenn Sie die Anzahl der Optionen verringern, verringern Sie dadurch auch die Anzahl von Fragen, die vom Unternehmen in dieser frühen Phase beantwortet werden müssen.

Wenn beispielsweise die Optionen in Bezug auf das Rehosting oder Außerbetriebnehmen begrenzt sind, muss sich das Unternehmen während der ersten Rationalisierung nur eine Frage stellen – nämlich, ob die Ressource außer Betrieb genommen werden soll.

„Die Analyse hat ergeben, dass diese Ressource derzeit von keinem Benutzer aktiv verwendet wird. Stimmt dies, oder haben wir etwas übersehen?“ Eine Ja/Nein-Frage dieser Art kann mit einer qualitativen Analyse normalerweise wesentlich einfacher beantwortet werden.

Mit diesem optimierten Ansatz werden Baselines, Finanzpläne, eine Strategie und eine Richtung festgelegt. Bei späteren Aktivitäten durchläuft jede Ressource dann eine weitere Rationalisierung und qualitative Analyse, um weitere Optionen zu evaluieren. Alle Annahmen, die Sie in dieser anfänglichen Rationalisierung vornehmen, werden vorher getestet

## <a name="challenge-assumptions"></a>Anforderungsannahmen

Das Ergebnis des vorherigen Abschnitts ist eine grobe Rationalisierung mit vielen Annahmen. Als Nächstes werden einige dieser Annahmen hinterfragt.

### <a name="retire-assets"></a>Außerbetriebnahme von Ressourcen

In einer herkömmlichen lokalen Umgebung hat das Hosten von kleinen, ungenutzten Ressourcen selten erhebliche Auswirkungen auf die jährlichen Kosten. Mit einigen Ausnahmen macht der Bedarf an Vollzeitmitarbeitern für das Analysieren und Außerbetriebnehmen der jeweiligen Ressource die Kosteneinsparungen, die sich aus dem Beschneiden und Außerbetriebnehmen dieser Ressourcen ergeben, wieder zunichte.

Wenn Sie aber auf ein Cloudabrechnungsmodell umstellen, können durch die Außerbetriebnahme von Ressourcen erhebliche Einsparungen bei den jährlichen Betriebskosten und beim Anschubaufwand für die Migration erzielt werden.

Es ist nicht ungewöhnlich, dass Organisationen mindestens 20% ihrer digitalen Ressourcen außer Betrieb nehmen, nachdem sie eine quantitative Analyse durchgeführt haben. Wir empfehlen, eine weitere qualitative Analyse durchzuführen, bevor die Entscheidung in Bezug auf eine Maßnahme dieser Art getroffen wird. Nach der Bestätigung der Entscheidung kann die Außerbetriebnahme dieser Ressourcen zur ersten guten Rendite bei der Cloudmigration führen. In vielen Fällen ist dies einer der größten Faktoren zur Kosteneinsparung. Daher empfehlen wir, dass das Cloudstrategieteam die Prüfung und Außerbetriebnahme der Ressourcen parallel zur Erstellungsphase des Migrationsprozesses überwacht, um schnell finanzielle Erfolge zu erzielen.

### <a name="program-adjustments"></a>Anpassungen des Programms

Ein Unternehmen führt selten nur einen Transformationsprozess allein durch. Die Wahl zwischen Kostensenkung, Marktwachstum und neuen Umsatzchancen ist meist keine Ja/Nein-Entscheidung. Daher empfehlen wir, dass das Cloudstrategieteam mit der IT-Abteilung zusammenarbeitet, um Ressourcen paralleler Transformationsprozesse zu ermitteln, die sich außerhalb des primären Transformationsprozesses befinden.

Für das in diesem Artikel angegebene Beispiel für die IaaS-Migration gilt Folgendes:

- Bitten Sie das DevOps-Team, Ressourcen zu identifizieren, die bereits Teil einer Bereitstellungsautomatisierung sind, und entfernen Sie diese Ressourcen aus dem Hauptmigrationsplan.

- Bitten Sie die für Daten sowie für Forschung und Entwicklung zuständigen Teams, Ressourcen zu identifizieren, die als Basis für neue Umsatzchancen dienen, und diese aus dem Hauptmigrationsplan zu entfernen.

Diese programmbezogene qualitative Analyse kann schnell durchgeführt werden und sorgt für eine Vereinheitlichung über mehrere Migrationsbacklogs hinweg.

Möglicherweise müssen Sie einige Ressourcen als Ressourcen zum Rehosten weiterhin eine Zeitlang in Erwägung ziehen. Nach der anfänglichen Migration können Sie eine spätere Rationalisierung in Phasen vornehmen.

## <a name="select-the-first-workload"></a>Auswählen der ersten Workload

Die Implementierung der ersten Workload ist für das Testen und den Lernprozess von entscheidender Bedeutung. Es ist die erste Möglichkeit, die Chancen für Umsatzwachstum darzustellen und zu verinnerlichen.

### <a name="business-criteria"></a>Geschäftliche Kriterien

Um die geschäftliche Transparenz sicherzustellen, identifizieren Sie eine Workload, die von einem Mitglied der Geschäftseinheit des Cloudstrategieteams unterstützt wird. Es sollte sich vorzugsweise um eine Workload handeln, an der das Team beteiligt ist und bei der eine hohe Motivation für eine Verlagerung in die Cloud besteht.

### <a name="technical-criteria"></a>Technische Kriterien

Wählen Sie eine Workload aus, die nur über wenige Abhängigkeiten verfügt und als kleine Ressourcengruppe verschoben werden kann. Wir empfehlen, dass Sie eine Arbeitsauslastung mit einem definierten Testpfad auswählen, um die Prüfung zu vereinfachen.

Die erste Workload wird häufig in einer Experimentierumgebung ohne Betriebs- oder Governance-Kapazität bereitgestellt. Es ist wichtig, eine Workload auszuwählen, die mit geschützten Daten nicht interagiert.

### <a name="qualitative-analysis"></a>Qualitative Analyse

Die Cloudeinführungsteams und das Cloudstrategieteam können zusammenarbeiten, um diese kleine Workload zu analysieren. Durch diese Zusammenarbeit wird eine kontrollierte Möglichkeit zum Erstellen und Testen der Kriterien für die qualitative Analyse geschaffen. Aufgrund des geringeren Umfangs können die betroffenen Benutzer überwacht werden, und es kann innerhalb eines Zeitraums von maximal einer Woche eine ausführliche qualitative Analyse durchgeführt werden. Informationen zu häufigen Faktoren bei der qualitativen Analyse finden Sie unter dem jeweiligen Rationalisierungsziel im Artikel [5 Rs of Rationalization](./5-rs-of-rationalization.md) (Die fünf R der Rationalisierung).

### <a name="migration"></a>Migration

Parallel zur laufenden Rationalisierung kann das Cloudeinführungsteam damit beginnen, die kleine Workload zu migrieren, um den Lernprozess in den folgenden wichtigen Bereichen zu fördern:

- Stärken der Fähigkeiten in Bezug auf die Plattform des Cloudanbieters
- Definieren der erforderlichen Kerndienste (und Azure-Standards) für die langfristige Vision
- Entwickeln eines besseren Verständnisses, wie Vorgänge im Verlauf der Transformation geändert werden müssten.
- Verstehen der inhärenten geschäftlichen Risiken und die damit verbundene Toleranz des Unternehmens
- Festlegen einer Baseline oder eines Produkts mit den Governance-Mindestanforderungen gemäß der Risikotoleranz des Unternehmens

## <a name="release-planning"></a>Releaseplanung

Während das Cloudeinführungsteam die Migration oder Implementierung der ersten Workload durchführt, kann das Cloudstrategieteam mit dem Priorisieren der restlichen Anwendungen bzw. Workloads beginnen.

### <a name="power-of-10"></a>Zehn Anwendungen

Der herkömmliche Ansatz für die Rationalisierung versucht, alle vorhersehbaren Anforderungen zu erfüllen. Glücklicherweise wird zum Starten eines Transformationsprozesses meist nicht ein separater Plan für jede Anwendung benötigt. Bei einem inkrementellen Modell ist der Ansatz „Zehn Anwendungen“ ein guter Ausgangspunkt. Hierbei wählt das Cloudstrategieteam die ersten 10 Anwendungen für die Migration aus. Diese zehn Workloads sollten ein Mischung aus einfachen und komplexen Workloads darstellen.

### <a name="build-the-first-backlogs"></a>Erstellen der ersten Backlogs

Die Cloudeinführungsteams und das Cloudstrategieteam können bei der qualitativen Analyse für die ersten zehn Workloads zusammenarbeiten. Hierbei werden das erste mit Priorität versehene Migrationsbacklog und das erste mit Priorität versehene Releasebacklog erstellt. Bei dieser Methode können die Teams den Prozess gemeinsam durchlaufen und haben genügend Zeit, um einen geeigneten Prozess für die qualitative Analyse zu erstellen.

### <a name="mature-the-process"></a>Weiterentwickeln des Prozesses

Nachdem die beiden Teams die Kriterien für die qualitative Analyse vereinbart haben, kann die Bewertung zu einer Aufgabe bei jeder Iteration werden. Zur Erreichung eines Konsenses in Bezug auf die Bewertungskriterien werden normalerweise zwei bis drei Releases benötigt.

Nachdem die Bewertung in die inkrementellen Ausführungsprozesse der Migration verschoben wurde, kann das Cloudeinführungsteam die Bewertung und die Architektur schneller durchlaufen. An diesem Punkt wird das Cloudstrategieteam außerdem abstrahiert, um den Zeitaufwand zu reduzieren. Darüber hinaus kann sich das Cloudstrategieteam auf das Priorisieren der Anwendungen konzentrieren, die noch nicht in einem bestimmten Release enthalten sind. So kann eine enge Abstimmung auf sich ändernde Marktbedingungen sichergestellt werden.

Nicht alle priorisierten Anwendungen sind bereit für die Migration. Die Sequenzierung ändert sich wahrscheinlich, wenn das Team eine eingehendere qualitative Analyse durchführt sowie Geschäftsereignisse und Abhängigkeiten ermittelt, die möglicherweise eine erneute Priorisierung des Backlogs erforderlich machen. Bei einigen Releases wird ggf. eine geringe Anzahl von Workloads gruppiert. Andere enthalten vielleicht auch nur eine einzige Workload.

Das Cloudeinführungsteam führt wahrscheinlich Iterationen durch, bei denen sich keine vollständige Workloadmigration ergibt. Je kleiner die Workload und je kleiner die Anzahl von Abhängigkeiten ist, desto höher ist die Wahrscheinlichkeit, dass eine Workload in einen einzelnen Sprint bzw. eine Iteration passt. Aus diesem Grund empfehlen wir, die ersten Anwendungen im Releasebacklog klein zu halten und auf wenige externe Abhängigkeiten zu beschränken.

## <a name="end-state"></a>Endzustand

Im Laufe der Zeit führen das Cloudeinführungs- und das Cloudstrategieteam eine vollständige Rationalisierung des Bestands gemeinsam durch. Bei diesem inkrementellen Ansatz können die Teams den Rationalisierungsprozess aber immer schneller abarbeiten. Außerdem ergeben sich aus dem Transformationsprozess früher greifbare Geschäftsergebnisse, ohne dass zuerst ein hoher Analyseaufwand anfällt.

In einigen Fällen ist das Finanzmodell möglicherweise zu eng gefasst, um ohne weitere Rationalisierungsmaßnahmen eine Entscheidung treffen zu können. In solchen Fällen benötigen Sie vielleicht einen herkömmlicheren Rationalisierungsansatz.

## <a name="next-steps"></a>Nächste Schritte

Das Ergebnis eines Rationalisierungsprozesses ist ein priorisiertes Backlog mit allen Ressourcen, die von der ausgewählten Transformation betroffen sind. Dieses Backlog kann dann als Grundlage für Kostenmodelle von Clouddiensten dienen.

> [!div class="nextstepaction"]
> [Align cost models with the digital estate](./calculate.md) (Ausrichten von Kostenmodellen auf die digitalen Ressourcen)
