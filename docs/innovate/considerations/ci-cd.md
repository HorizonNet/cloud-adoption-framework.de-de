---
title: 'Cloudinnovation: Unterstützen der Einführung'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Einführung in die Cloudinnovation: Unterstützen der Einführung'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 0c6f55ec7f82756658fc67fb9412d7d83d503b97
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683244"
---
# <a name="empower-adoption"></a>Unterstützen der Einführung

Der ultimative Test der Innovation ist die Reaktion des Kunden auf Ihre Erfindung. Hat sich die Hypothese als wahr erwiesen? Verwenden Kunden die Lösung? Wird sie den Anforderungen des gewünschten Prozentsatzes von Benutzern gerecht? Das Wichtigste: Kommen sie wieder? Alle diese Fragen können erst nach der Bereitstellung der MVP-Lösung gestellt werden. In diesem Artikel konzentrieren wir uns auf die Disziplin der Unterstützung der Einführung.

## <a name="reducing-friction-to-adoption"></a>Reduzieren der Schwierigkeiten bei der Einführung

Es gibt einige Hauptreibungspunkte bei der Einführung, die durch eine Kombination aus Technologie und Prozessen minimiert werden können. Lesern, die mit CI/CD- oder DevOps-Prozessen vertraut sind, wird das Folgende sehr bekannt vorkommen. Der Schwerpunkt dieses Artikels ist, einen Ausgangspunkt für Cloudeinführungsteams zu schaffen, der Innovation und Feedbackschleifen anregt. Langfristig könnten aus diesem Ausgangspunkt stabilere CI/CD- oder DevOps-Ansätze entstehen, wenn die Produkte und Teams ausgereift sind.

Wie unter [Messen der Auswirkungen für Kunden](./measure.md) beschrieben, erfordert die positive Validierung jeder Hypothese Iterationen und Entschlossenheit. Während eines beliebigen Innovationszyklus werden Sie mehr Niederlagen als Siege erleben. Dies entspricht dem erwarteten Verhalten. Wenn jedoch Kundenanforderung, Hypothese und Lösung bedarfsabhängig ausgerichtet werden, ändert sich die Welt rasch. Dieser Artikel zielt darauf ab, die [technische Spitze](./build.md#reduce-complexity-and-delay-technical-spikes) zu minimieren, die die Innovation bremsen würde, aber sicherzustellen, dass einige solide bewährte Methoden angewandt werden. Auf diese Weise kann das Team Entwürfe für einen zukünftigen Erfolg entwickeln, aber die aktuellen Anforderungen der Kunden erfüllen.

## <a name="empowering-adoption---maturity-model"></a>Unterstützung der Einführung – Reifemodell

Das Hauptziel der [Innovationsmethodik](./index.md) ist das Schaffen von Kundenpartnerschaften und Beschleunigen von Feedbackschleifen, was zu Marktinnovationen führen wird.
In der folgenden Abbildung und den folgenden Inhaltsabschnitten werden die anfänglichen Implementierungen beschrieben, die die Methodik unterstützen.

![Unterstützung der Einführung – Reifemodell](../../_images/innovate/empower-adoption-maturity.png)

- [Freigegebene Lösung](#shared-solution): Richten Sie ein zentrales Repository für alle Aspekte der Lösung ein.
- [Feedbackschleifen](#feedback-loops): Stellen Sie sicher, dass Feedbackschleifen durch Iterationen konsistent verwaltet werden können.
- [Continuous Integration](#continuous-integration): Erstellen und konsolidieren Sie die Lösung regelmäßig.
- [Zuverlässiges Testen](#reliable-testing): Überprüfen Sie die Lösungsqualität und erwartete Änderungen, um Sicherungsmaßnahmen zu steuern.
- [Lösungsbereitstellung](#solution-deployment): Bereitstellung einer Lösung, um dem Team zu ermöglichen, Änderungen schnell für Kunden freizugeben.
- [Integrierte Messung](#integrated-measurements): Fügen Sie der Feedbackschleife Lernmetriken für eine klare Analyse durch das gesamte Team hinzu.

Um technische Spitzen zu minimieren, gehen Sie davon aus, dass die Reife in den einzelnen Prinzipien anfänglich niedrig ist. Planen Sie jedoch voraus durch Orientierung an Tools und Prozessen, die sich präziser werdenden Hypothesen anpassen können. In Azure ermöglicht die Kombination von [GitHub](https://guides.github.com) und [Azure DevOps](https://docs.microsoft.com/azure/devops) kleinen Teams, mit geringen Reibungsverlusten zu beginnen. Daraus können Tausende von Entwicklern resultieren, die gemeinsam an skalierten Lösungen arbeiten, die Hunderte von Kundenhypothesen testen. Im restlichen Teil dieses Artikels wird der Ansatz zur Unterstützung der Einführung, groß zu planen und klein zu beginnen, zu jedem dieser Prinzipien veranschaulicht.

## <a name="shared-solution"></a>Freigegebene Lösung

Wie unter [Messen der Auswirkungen für Kunden](./measure.md) beschrieben, erfordert die positive Validierung jeder Hypothese Iterationen und Entschlossenheit. Während eines beliebigen Innovationszyklus werden Sie mehr Niederlagen als Siege erleben. Dies entspricht dem erwarteten Verhalten. Wenn jedoch Kundenanforderung, Hypothese und Lösung bedarfsabhängig ausgerichtet werden, ändert sich die Welt rasch.

Zum Skalieren von Innovationen gibt es kein wertvolleres Tool als eine freigegebene Codebasis für die Lösung. Leider gibt es keine Möglichkeit, vorherzusagen, mit welcher Iteration oder welchem MVP die gewinnende Kombination erzielt wird. Daher ist es nie zu früh, eine freigegebene Codebasis oder ein Repository einzurichten. Dies ist die einzige [technische Spitze](./build.md#reduce-complexity-and-delay-technical-spikes), die nie verzögert werden sollte. Wenn das Team verschiedene MVP-Lösungen durchläuft, sorgt ein freigegebenes Repository für mühelose Zusammenarbeit und beschleunigte Entwicklung. Wenn Änderungen an der Lösung negative Auswirkungen auf Lernmetriken haben, kann die Versionskontrolle ein Rollback zur vorherigen, effektiveren Version der Lösung ermöglichen.

Das gängigste Tool für die Verwaltung von Coderepositorys ist [GitHub](https://guides.github.com), wo ein Repository für freigegebenen Code mit wenigen Klicks erstellt werden kann. Außerdem kann das Feature [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) von Azure DevOps zum Erstellen eines [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git)- oder [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc)-Repositorys verwendet werden.

## <a name="feedback-loops"></a>Feedbackschleifen

Der Schlüssel zum Schaffen von Kundenpartnerschaften während Innovationszyklen ist, den Kunden zu einem Teil der Lösung zu machen. Dies erfolgt auf Armeslänge durch [Messen der Auswirkungen für Kunden](./measure.md). Genauer gesagt, sind der Dialog und direkte Tests mit dem Kunden erforderlich. Beides führt zu einem Feedback, das verwaltet werden muss.

Jeder Feedbackpunkt ist eine potenzielle Lösung für die Kundenanforderung. Noch wichtiger ist, dass jedes direkte Feedback von einem Kunden eine Chance zur Verbesserung der Partnerschaft ist. Wenn Feedback es in eine MVP-Lösung schafft, stoßen Sie mit dem Kunden darauf an. Selbst wenn das Feedback nicht umsetzbar ist, signalisiert schon das Eingestehen der Entscheidung, dem Feedback keine Priorität einzuräumen, eine [Wachstumsmentalität](./learn.md#growth-mindset) und einen Schwerpunkt auf [fortlaufendem Lernen](./learn.md#continuous-learning).

[Azure DevOps](https://docs.microsoft.com/azure/devops) bietet Möglichkeiten, [Feedback anzufordern, bereitzustellen und zu verwalten](https://docs.microsoft.com/azure/devops/project/feedback). Jedes dieser Tools zentralisiert Feedback, damit das Team Feedback umsetzen und darüber berichten kann, sodass die Feedbackschleife transparent wird.

## <a name="continuous-integration"></a>Continuous Integration

Wenn Einführungen skaliert werden und eine Hypothese sich bedarfsabhängig einer echten Innovation annähert, wächst die Anzahl der zu testenden kleineren Hypothesen schnell. Für präzise Feedbackschleifen und reibungslose Einführungsprozesse ist wichtig, dass jede dieser Hypothesen integriert wird und die primäre Hypothese hinter der Innovation unterstützt. Leider müssen Sie sich auch schnell bewegen, um innovativ zu sein und zu wachsen, was voraussetzt, dass mehrere Entwickler Varianten der Kernhypothese testen. Für Entwicklungsaktivitäten in einer späteren Phase ist es möglicherweise erforderlich, dass mehrere Teams von Entwicklern jeweils auf eine gemeinsam genutzte Lösung hin arbeiten. Continuous Integration ist der erste Schritt hin zur Verwaltung der verschiedenen sich bewegenden Teile.

In Continuous Integration werden Codeänderungen häufig in den Hauptbranch zusammengeführt. Mithilfe von automatisierten Build- und Testprozessen wird sichergestellt, dass der Code im Hauptbranch immer Produktionsqualität aufweist. Dadurch wird sichergestellt, dass Entwickler zusammenarbeiten, um gemeinsam genutzte Lösungen zu entwickeln, die exakte und zuverlässige Feedbackschleifen bieten.

Azure DevOps und [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) bieten mit wenigen Klicks Continuous Integration-Funktionen für GitHub oder eine Vielzahl anderer Repositorys.
Erfahren Sie mehr über [Continuous Integration](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration), oder führen Sie die [praktischen Übungseinheiten](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration) aus, um weitere Informationen zu erhalten. Es gibt auch Lösungsarchitekturen, die die Erstellung Ihrer [CI/CD-Pipelines mithilfe von Azure DevOps](https://azure.microsoft.com/solutions/devops) beschleunigen.

## <a name="reliable-testing"></a>Zuverlässiges Testen

Fehler in einer Lösung können falsch positive oder falsch negative Ergebnisse erzeugen. Unerwartete Fehler können leicht zur Fehlinterpretation von Benutzerakzeptanzmetriken führen. Dies kann auch zu negativem Feedback von Kunden führen, das den Test ihrer Hypothese nicht richtig wiedergibt.

Während der frühen Iterationen einer MVP-Lösung werden Fehler erwartet, Early Adopters verzeihen sie vielleicht sogar gern. In frühen Releases finden wahrscheinlich keine Akzeptanztests statt. Ein Aspekt des Entwickelns von Lösungen mit Blick auf die Kundenanforderungen ist jedoch die Validierung von Anforderung und Hypothese. Beides kann mit Komponententests auf Codeebene und manuellen Akzeptanztests vor der Bereitstellung durchgeführt werden. Zusammen tragen sie zur Zuverlässigkeit des Testens bei. Langfristig sollte eine klar definierte Reihe von Build-, Komponenten- und Akzeptanztests automatisiert werden, um zuverlässige Metriken zu gewährleisten, die sich auf eine präzisere Optimierung von Hypothese und resultierender Lösung beziehen.

[Azure Test Plans](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) bietet Tools zum Entwickeln und Einsetzen von Testplänen während der manuellen oder automatisierten Testausführung.

## <a name="solution-deployment"></a>Bereitstellung von Lösungen

Der wichtigste Aspekt bei der Unterstützung der Einführung ist die Möglichkeit, die Freigabe einer Lösung für Kunden zu steuern. Das Bereitstellen einer Self-Service- oder automatisierten Pipeline zum Freigeben einer Lösung für Kunden beschleunigt die Feedbackschleife. Kunden zu ermöglichen, schnell mit Änderungen in der Lösung zu interagieren, lädt sie ein, am Prozess teilzunehmen. Außerdem ermöglicht dies schnellere Tests von Hypothesen, was Annahmen und potenzielle Überarbeitung reduziert.

Es gibt mehrere Ansätze für die Lösungsbereitstellung. Im Folgenden werden die drei gängigsten Ansätze erläutert:

- Der fortgeschrittenste Ansatz, **Continuous Deployment**, stellt Codeänderungen automatisch in der Produktionsumgebung bereit. Für ausgereifte Teams, die ausgereifte Hypothesen testen, kann Continuous Deployment äußerst wertvoll sein.
- In den frühen Phasen der Entwicklung könnte **Continuous Delivery** besser geeignet sein. Bei Continuous Delivery werden Codeänderungen automatisch in einer produktionsähnlichen Umgebung bereitgestellt. Entwickler, Geschäftsentscheidungsträger und andere Teammitglieder können diese Umgebung verwenden, um zu überprüfen, ob ihre Arbeit produktionsbereit ist. Sie kann auch verwendet werden, um eine Hypothese mit Kunden ohne Auswirkung auf die laufenden Geschäftsaktivitäten zu testen.
- Die **manuelle Bereitstellung** ist der am wenigsten fortgeschrittene Ansatz für die Releaseverwaltung. Wie der Name schon sagt, würde ein Teammitglied die neuesten Codeänderungen manuell bereitstellen. Dieser Ansatz ist fehleranfällig, unzuverlässig und wird von den meisten erfahrenen Technikern als Antimuster betrachtet.

Während der ersten Iteration einer MVP-Lösung ist die manuelle Bereitstellung trotz der oben beschriebenen Einwände ein gängiger Ansatz. Wenn die Lösung sehr vage und das Kundenfeedback unbekannt ist, besteht ein erhebliches Risiko, dass die gesamte Lösung (oder sogar die Kernhypothese) zurückgesetzt wird. Die allgemeine Regel für die manuelle Bereitstellung lautet: Keine Kundenprüfung, keine Automatisierung der Bereitstellung. Eine frühe Investition kann zu Zeitverlust führen. Noch wichtiger ist, dass sie zu Abhängigkeiten von der Releasepipeline führen kann, die das Team gegen eine frühe Wende resistenter machen würde. Nach den ersten Iterationen, oder wenn Kundenfeedback einen potenziellen Erfolg suggeriert, sollte schnell ein fortgeschritteneres Bereitstellungsmodell eingeführt werden.

In jeder Phase der Hypothesenvalidierung bieten Azure DevOps und [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) Continuous Delivery- und Continuous Deployment-Funktionen mit wenigen Klicks. Erfahren Sie mehr über [Continuous Delivery](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery), oder führen Sie die [praktischen Übungseinheiten](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment) aus, um weitere Informationen zu erhalten. Lösungsarchitekturen können die Erstellung Ihrer [CI/CD-Pipelines mithilfe von Azure DevOps](https://azure.microsoft.com/solutions/devops) auch beschleunigen.

## <a name="integrated-measurements"></a>Integrierte Messungen

Beim [Messen der Auswirkungen für Kunden](./measure.md), ist es wichtig, zu verstehen, wie Kunden auf Änderungen in der Lösung reagieren. Diese als Telemetriedaten bezeichneten Daten bieten Einblicke in die Aktionen, die ein Benutzer (oder eine Kohorte von Benutzern) bei der Verwendung der Lösung durchführte. Aus diesen Daten kann einfach eine quantitative Validierung der Hypothese gewonnen werden. Diese Metriken können dann verwendet werden, um die Lösung anzupassen und differenziertere Hypothesen zu generieren. Diese subtileren Änderungen tragen dazu bei, die anfängliche Lösung in nachfolgenden Iterationen ausreifen zu lassen, sodass die Einführung schließlich bedarfsabhängig wiederholt wird.

In Azure bietet [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) die Tools und die Schnittstelle zum Erfassen und Überprüfen der Daten aus den Kundenerfahrungen. Diese Beobachtungen und Einblicke können verwendet werden, um den Rückstand mithilfe von [Azure Boards](https://docs.microsoft.com/azure/devops/boards) zu verbessern.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie mit den Tools und Prozessen vertraut sind, die zur Unterstützung der Einführung erforderlich sind, ist es an der Zeit, eine erweiterte Innovationsdisziplin kennenzulernen, [Interagieren mit Geräten](./devices.md). Dies kann die Barrieren zwischen physischer und digitaler Umgebung reduzieren, sodass Ihre Lösung noch einfacher angenommen werden kann.

> [!div class="nextstepaction"]
> [Interagieren mit Geräten](./devices.md)
