---
title: Unterstützen der Einführung durch digitale Innovationen
description: Nutzen Sie das Reifemodell der Innovationsmethodik, um die Migration möglichst reibungslos zu gestalten und gleichzeitig die weitere Anwendung von Best Practices zu gewährleisten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 1599c6b2e4df791e1fafd5d2c7a7b4849c11bc98
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88878298"
---
# <a name="empower-adoption-with-digital-invention"></a>Unterstützen der Einführung durch digitale Innovationen

Der ultimative Test der Innovation ist die Reaktion des Kunden auf Ihre Erfindung. Hat sich die Hypothese als wahr erwiesen? Verwenden Kunden die Lösung? Wird sie den Anforderungen des gewünschten Prozentsatzes von Benutzern gerecht? Das Wichtigste: Kommen sie wieder? Alle diese Fragen können erst nach der Bereitstellung der MVP-Lösung (Minimum Viable Product) gestellt werden. In diesem Artikel konzentrieren wir uns auf die Disziplin der Unterstützung der Einführung.

## <a name="reduce-friction-that-affects-adoption"></a>Verringern von Reibungen, die sich auf die Einführung auswirken

Einige Hauptreibungspunkte bei der Einführung können durch eine Kombination aus Technologie und Prozessen minimiert werden. Für Leser mit Kenntnissen von Continuous Integration (CI) und Continuous Deployment (CD) oder DevOps-Prozessen wird das Folgende sehr vertraut sein. Dieser Artikel schafft einen Ausgangspunkt für Cloudeinführungsteams, der Innovation und Feedbackschleifen anregt. Künftig könnten sich auf der Grundlage dieses Ausgangspunkts stabilere CI/CD- oder DevOps-Ansätze entwickeln, wenn die Produkte und Teams ausgereift sind.

Wie unter [Messen der Auswirkungen für Kunden](./measure.md) beschrieben, erfordert die positive Validierung jeder Hypothese Iterationen und Entschlossenheit. Während eines beliebigen Innovationszyklus werden Sie weit mehr Niederlagen als Siege erleben. Dies entspricht dem erwarteten Verhalten. Wenn jedoch Kundenanforderung, Hypothese und Lösung bedarfsabhängig ausgerichtet werden, ändert sich die Welt rasch. Dieser Artikel zielt darauf ab, die [technischen Spitzen](./build.md#reduce-complexity-and-delay-technical-spikes) zu minimieren, die die Innovation bremsen, aber dennoch sicherzustellen, dass Sie einige solide bewährte Methoden anwenden. Auf diese Weise kann das Team Entwürfe für einen zukünftigen Erfolg entwickeln und dabei die aktuellen Anforderungen der Kunden erfüllen.

## <a name="empower-adoption-the-maturity-model"></a>Unterstützung der Einführung: Das Reifegradmodell

Das Hauptziel der [Innovationsmethodik](./index.md) ist das Schaffen von Kundenpartnerschaften und Beschleunigen von Feedbackschleifen, was zu Marktinnovationen führen wird. In der folgenden Abbildung und den folgenden Abschnitten werden die anfänglichen Implementierungen beschrieben, die diese Methodik unterstützen.

![Unterstützung der Einführung: das Reifemodell](../../_images/innovate/empower-adoption-maturity.png)

- [Freigegebene Lösung](#shared-solution): Richten Sie ein zentrales Repository für alle Aspekte der Lösung ein.
- [Feedbackschleifen](#feedback-loops): Stellen Sie sicher, dass Feedbackschleifen durch Iterationen konsistent verwaltet werden können.
- [Continuous Integration](#continuous-integration): Erstellen und konsolidieren Sie die Lösung regelmäßig.
- [Zuverlässiges Testen](#reliable-testing): Überprüfen Sie die Lösungsqualität und die erwarteten Änderungen, um die Zuverlässigkeit ihrer Testmetriken sicherzustellen.
- [Lösungsbereitstellung](#solution-deployment): Stellen Sie Lösungen bereit, damit das Team Änderungen schnell für Kunden freigeben kann.
- [Integrierte Messung](#integrated-measurements): Fügen Sie der Feedbackschleife Lernmetriken für eine klare Analyse durch das gesamte Team hinzu.

Um technische Spitzen zu minimieren, setzen Sie voraus, dass die Reife in den einzelnen Prinzipien anfänglich niedrig ist. Planen Sie jedoch definitiv voraus durch Orientierung an Tools und Prozessen, die sich präziser werdenden Hypothesen anpassen können. In Azure ermöglichen [GitHub](https://guides.github.com) und [Azure DevOps](/azure/devops) kleinen Teams, mit geringen Reibungsverlusten zu beginnen. Diese Teams könnten wachsen und Tausende von Entwicklern einbeziehen, die gemeinsam an skalierten Lösungen arbeiten und Hunderte von Kundenhypothesen testen. Im restlichen Teil dieses Artikels wird der Ansatz „Groß planen, klein beginnen“ zur Unterstützung der Einführung zu jedem dieser Prinzipien veranschaulicht.

## <a name="shared-solution"></a>Freigegebene Lösung

Wie unter [Messen der Auswirkungen für Kunden](./measure.md) beschrieben, erfordert die positive Validierung jeder Hypothese Iterationen und Entschlossenheit. Während eines beliebigen Innovationszyklus werden Sie weit mehr Niederlagen als Siege erleben. Dies entspricht dem erwarteten Verhalten. Wenn jedoch Kundenanforderung, Hypothese und Lösung bedarfsabhängig ausgerichtet werden, ändert sich die Welt rasch.

Zum Skalieren von Innovationen gibt es kein wertvolleres Tool als eine freigegebene Codebasis für die Lösung. Leider gibt es keine zuverlässige Möglichkeit, vorherzusagen, mit welcher Iteration oder welchem MVP die gewinnende Kombination erzielt wird. Daher ist es nie zu früh, eine freigegebene Codebasis oder ein Repository einzurichten. Dies ist die einzige [technische Spitze](./build.md#reduce-complexity-and-delay-technical-spikes), die nie verzögert werden sollte. Wenn das Team verschiedene MVP-Lösungen durchläuft, ermöglicht ein freigegebenes Repository mühelose Zusammenarbeit und beschleunigte Entwicklung. Wenn Änderungen der Lösung Lernmetriken beeinträchtigen, können Sie mit der Versionskontrolle ein Rollback auf eine frühere, effektivere Version der Lösung durchführen.

Das gängigste Tool für die Verwaltung von Coderepositorys ist [GitHub](https://guides.github.com). Damit lässt sich in wenigen Schritten ein gemeinsam genutztes Coderepository erstellen. Außerdem kann das Feature [Azure Repos](/azure/devops/repos/get-started/what-is-repos?view=azure-devops) von Azure DevOps zum Erstellen eines [Git](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git)- oder [TFVC](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc)-Repositorys verwendet werden.

## <a name="feedback-loops"></a>Feedbackschleifen

Den Kunden zu einem Teil der Lösung zu machen, ist der Schlüssel zum Aufbau von Kundenpartnerschaften während Innovationszyklen. Dies wird teilweise durch [Messen der Auswirkungen für Kunden](./measure.md) erreicht. Der Dialog und direkte Tests mit dem Kunden sind erforderlich. Beides generiert Feedback, das effektiv verwaltet werden muss.

Jeder Feedbackpunkt ist eine potenzielle Lösung für die Kundenanforderung. Noch wichtiger ist, dass jedes direkte Feedback eines Kunden eine Chance zur Verbesserung der Partnerschaft ist. Wenn Feedback es in eine MVP-Lösung schafft, stoßen Sie mit dem Kunden darauf an. Selbst wenn manches Feedback nicht umsetzbar ist, signalisiert schon das Eingestehen der Entscheidung, dem Feedback keine Priorität einzuräumen, eine [Wachstumsmentalität](./learn.md#growth-mindset) und einen Schwerpunkt auf [fortlaufendem Lernen](./learn.md#continuous-learning).

[Azure DevOps](/azure/devops) bietet Möglichkeiten, [Feedback anzufordern, bereitzustellen und zu verwalten](/azure/devops/project/feedback). Jedes dieser Tools zentralisiert Feedback, sodass das Team Feedback umsetzen und Folgeaktivitäten im Dienste einer transparenten Feedbackschleife leisten kann.

## <a name="continuous-integration"></a>Continuous Integration

Wenn Einführungen skaliert werden und eine Hypothese sich bedarfsabhängig einer echten Innovation annähert, wächst die Anzahl der zu testenden kleineren Hypothesen schnell. Für präzise Feedbackschleifen und reibungslose Einführungsprozesse ist wichtig, dass jede dieser Hypothesen integriert wird und die primäre Hypothese hinter der Innovation unterstützt. Dies bedeutet, das Sie auch schnell agieren müssen, um innovativ zu sein und zu wachsen, was voraussetzt, dass mehrere Entwickler Varianten der Kernhypothese testen. Für Entwicklungsaktivitäten in einer späteren Phase benötigen Sie möglicherweise mehrere Teams von Entwicklern, die jeweils auf eine gemeinsam genutzte Lösung hin arbeiten. Continuous Integration ist der erste Schritt hin zur Verwaltung aller sich bewegenden Teile.

In Continuous Integration werden Codeänderungen häufig in den Hauptbranch zusammengeführt. Automatisierte Build- und Testprozesse stellen sicher, dass der Code im Hauptbranch immer Produktionsqualität aufweist. Dies garantiert, dass Entwickler zusammenarbeiten, um gemeinsam genutzte Lösungen zu entwickeln, die exakte und zuverlässige Feedbackschleifen bieten.

Azure DevOps und [Azure Pipelines](/azure/devops/pipelines) bieten mit nur wenigen Schritten Continuous Integration-Funktionen für GitHub oder eine Vielzahl anderer Repositorys. Erfahren Sie mehr über [Continuous Integration](/azure/devops/learn/what-is-continuous-integration), oder führen Sie die [praktischen Übungseinheiten](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration) aus, um weitere Informationen zu erhalten. Lösungsarchitekturen sind verfügbar, die die Erstellung Ihrer [CI/CD-Pipelines über Azure DevOps](https://azure.microsoft.com/solutions/devops) beschleunigen können.

## <a name="reliable-testing"></a>Zuverlässiges Testen

Fehler in einer Lösung können falsch positive oder falsch negative Ergebnisse erzeugen. Unerwartete Fehler können leicht zur Fehlinterpretation von Benutzerakzeptanzmetriken führen. Sie können auch zu negativem Feedback von Kunden führen, das den Test ihrer Hypothese nicht richtig wiedergibt.

Während der frühen Iterationen einer MVP-Lösung werden Fehler erwartet; Early Adopters könnten sie vielleicht sogar gern verzeihen. In frühen Releases finden in der Regel keine Akzeptanztests statt. Ein Aspekt des Entwickelns von Lösungen mit Blick auf die Kundenanforderungen ist jedoch die Validierung von Anforderung und Hypothese. Beides kann mit Komponententests auf Codeebene und manuellen Akzeptanztests vor der Bereitstellung durchgeführt werden. Zusammen tragen sie zur Zuverlässigkeit des Testens bei. Sie sollten eine klar definierte Reihe von Build-, Komponenten- und Akzeptanztests automatisieren. Diese stellen zuverlässige Metriken im Zusammenhang mit präziseren Anpassungen an die Hypothese und die resultierende Lösung sicher.

Das Feature [Azure Test Plans](/azure/devops/test/track-test-status?view=azure-devops) bietet Tools zum Entwickeln und Einsetzen von Testplänen während der manuellen oder automatisierten Testausführung.

## <a name="solution-deployment"></a>Bereitstellung von Lösungen

Der wichtigste Aspekt bei der Unterstützung der Einführung ist Ihre Möglichkeit, die Freigabe einer Lösung für Kunden zu steuern. Durch Bereitstellen einer Self-Service- oder automatisierten Pipeline zum Freigeben einer Lösung für Kunden beschleunigen Sie die Feedbackschleife. Indem Sie Kunden ermöglichen, schnell mit Änderungen in der Lösung zu interagieren, laden Sie sie ein, am Prozess teilzunehmen. Dieser Ansatz löst auch schnelleres Testen von Hypothesen aus, was Annahmen und potenzielle Überarbeitungen reduziert.

Es gibt mehrere Methoden zum Bereitstellen von Lösungen. Die drei gängigsten sind:

- **Continuous Deployment** ist der fortgeschrittenste Ansatz, weil er automatisch Codeänderungen in der Produktionsumgebung bereitstellt. Für ausgereifte Teams, die ausgereifte Hypothesen testen, kann Continuous Deployment äußerst wertvoll sein.
- In den frühen Phasen der Entwicklung könnte **Continuous Delivery** besser geeignet sein. Bei Continuous Delivery werden Codeänderungen automatisch in einer produktionsähnlichen Umgebung bereitgestellt. Entwickler, Geschäftsentscheidungsträger und andere Teammitglieder können diese Umgebung verwenden, um zu überprüfen, ob ihre Arbeit produktionsbereit ist. Sie können mit dieser Methode auch eine Hypothese mit Kunden ohne Auswirkung auf die laufenden Geschäftsaktivitäten testen.
- Die **manuelle Bereitstellung** ist der am wenigsten ausgereifte Ansatz für die Releaseverwaltung. Wie der Name schon sagt, stellt ein Teammitglied die neuesten Codeänderungen manuell bereit. Dieser Ansatz ist fehleranfällig, unzuverlässig und wird von den meisten erfahrenen Technikern als Antimuster betrachtet.

Während der ersten Iteration einer MVP-Lösung ist die manuelle Bereitstellung trotz der vorherigen Bewertung üblich. Wenn die Lösung sehr vage und das Kundenfeedback unbekannt ist, besteht ein erhebliches Risiko, dass die gesamte Lösung (oder sogar die Kernhypothese) zurückgesetzt wird. Hier ist die allgemeine Regel für die manuelle Bereitstellung: keine Kundenprüfung, keine Automatisierung der Bereitstellung.

Eine frühe Investition kann zu Zeitverlust führen. Noch wichtiger ist, dass sie zu Abhängigkeiten von der Releasepipeline führen kann, die das Team gegen eine frühe Wende resistenter machen. Nach den ersten Iterationen, oder wenn Kundenfeedback einen potenziellen Erfolg suggeriert, sollte schnell ein fortgeschritteneres Bereitstellungsmodell eingeführt werden.

In jeder Phase der Hypothesenvalidierung bieten Azure DevOps und [Azure Pipelines](/azure/devops/pipelines) Continuous Delivery- und Continuous Deployment-Funktionen. Erfahren Sie mehr über [Continuous Delivery](/azure/devops/learn/what-is-continuous-delivery), oder sehen Sie sich die [praktische Übung](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment) an. Lösungsarchitekturen können die Erstellung Ihrer [CI/CD-Pipelines über Azure DevOps](https://azure.microsoft.com/solutions/devops) auch beschleunigen.

## <a name="integrated-measurements"></a>Integrierte Messungen

Beim [Messen der Auswirkungen für Kunden](./measure.md) ist es wichtig, dass Sie verstehen, wie Kunden auf Änderungen in der Lösung reagieren. Diese als *Telemetriedaten* bezeichneten Daten bieten Einblicke in die Aktionen, die ein Benutzer (oder eine Kohorte von Benutzern) beim Arbeiten mit der Lösung durchführte. Aus diesen Daten kann einfach eine quantitative Validierung der Hypothese gewonnen werden. Diese Metriken können dann verwendet werden, um die Lösung anzupassen und differenziertere Hypothesen zu generieren. Diese subtileren Änderungen tragen dazu bei, die anfängliche Lösung in nachfolgenden Iterationen ausreifen zu lassen, sodass die Einführung schließlich bedarfsabhängig wiederholt wird.

In Azure bietet [Azure Monitor](/azure/azure-monitor/overview) die Tools und die Schnittstelle zum Erfassen und Überprüfen der Daten aus den Kundenerfahrungen. Sie können diese Beobachtungen und Einblicke verwenden, um den Rückstand mithilfe von [Azure Boards](/azure/devops/boards) zu verbessern.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie sich mit den Tools und Prozessen vertraut gemacht haben, die zur Unterstützung der Einführung erforderlich sind, ist es an der Zeit, eine erweiterte Innovationsdisziplin kennenzulernen: [Interagieren mit Geräten](./devices.md). Diese Disziplin kann die Barrieren zwischen physischer und digitaler Umgebung reduzieren, sodass Ihre Lösung noch einfacher angenommen werden kann.

> [!div class="nextstepaction"]
> [Interagieren mit Geräten](./devices.md)
