---
title: Cloudmigration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cloudmigration im Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: 3734a9b692dd345f45ee6a2987abf773b3391c63
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224380"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Cloudmigration im Cloud Adoption Framework

Jeder [Cloudeinführungsplan](../plan/index.md) eines Unternehmens beinhaltet Workloads, die keine umfangreichen Investitionen in die Erstellung neuer Geschäftslogik rechtfertigen. Diese Workloads können mithilfe verschiedener Methoden in die Cloud migriert werden: per Lift & Shift, per Lift & Optimize oder mittels Modernisierung. Jeder diese Methoden wird als Migration betrachtet. In den folgenden Aufgaben werden die iterativen Prozesse zum Bewerten, Migrieren, Optimieren, Schützen und Verwalten dieser Workloads vermittelt.

## <a name="getting-started"></a>Erste Schritte

Zur Vorbereitung auf diese Phase des Cloudeinführungslebenszyklus empfiehlt das Framework die folgenden fünf Aufgaben:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/prerequisites.md?tabs=Checklist">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Voraussetzung für die Migration</h3>
Vergewissern Sie sich, dass eine Landezone bereitgestellt wurde und zum Hosten der ersten Workloads bereit ist, die zu Azure migriert werden. Sollten noch keine Strategie und noch kein Plan für die Cloudeinführung vorliegen, vergewissern Sie sich, dass beides in Arbeit ist.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Migrieren Ihrer ersten Workload</h3>
Orientieren Sie sich bei der Migration Ihrer ersten Workload am Leitfaden zur Azure-Migration. So können Sie sich mit den erforderlichen Tools und Vorgehensweisen für die Skalierung Ihrer Einführung vertraut machen.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./expanded-scope/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Erweiterte Migrationsszenarien</h3>
Nutzen Sie die Checkliste für die Cloudmigration mit erweitertem Umfang, um Szenarien zu ermitteln, in denen Sie Ihre zukünftige Zustandsarchitektur, Ihre Migrationsprozesse, Ihre Landezonenkonfiguration oder Ihre Entscheidungen im Zusammenhang mit Migrationstools anpassen müssen.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Bewährte Methoden</h3>
Überprüfen Sie sämtliche Änderungen anhand des Abschnitts für bewährte Methoden, um die ordnungsgemäße Implementierung spezifischer Migrationsansätze für erweiterten Umfang bzw. für Workloads/für die Architektur zu gewährleisten.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/5.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Prozessverbesserungen</h3>
Die Migration ist stark prozessorientiert. Nutzen Sie den Abschnitt mit den Überlegungen zur Migration, um verschiedene Aspekte Ihrer Prozesse zu bewerten und weiterzuentwickeln und auf Veränderungen bei den Migrationsaufgaben zu reagieren.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="iterative-migration-process"></a>Iterativer Migrationsprozess

Die Migration zur Cloud umfasst im Grunde vier einfache Phasen: Bewerten, Migrieren, Optimieren und Schützen/Verwalten. In diesem Abschnitt des Frameworks für die Cloudeinführung erfahren Sie, wie Sie den größtmöglichen Nutzen aus der jeweiligen Prozessphase ziehen und diese Phasen auf Ihren Cloudeinführungsplan abstimmen. Die folgende Grafik zeigt diese Phasen in einem iterativen Ansatz:

![Cloud Adoption Framework-Migrationsmodell](../_images/operational-transformation-migrate.png)

## <a name="creating-a-balanced-cloud-portfolio"></a>Erstellen eines ausgewogenen Cloudportfolios

Jedes ausgewogene Technologieportfolio verfügt über eine Mischung von Ressourcen in verschiedenen Zuständen. Einige Anwendungen sind für die Deaktivierung vorgesehen und werden nur minimal unterstützt. Andere Anwendungen oder Ressourcen werden in einem Wartungszustand unterstützt, aber die Features dieser Lösungen sind stabil. Für neuere Geschäftsprozesse werden sich ändernde Marktbedingungen wahrscheinlich zu einer kontinuierlichen Verbesserung oder Modernisierung der Features führen. Wenn sich Möglichkeiten zur Erschließung neuer Umsatzquellen ergeben, werden neue Anwendungen oder Ressourcen in die Umgebung eingeführt. In jeder Phase des Lebenszyklus einer Ressource ändern sich die Auswirkungen einer Investition auf Umsatz und Gewinn. Je später die Phase im Lebenszyklus, desto unwahrscheinlicher ist es, dass ein neues Feature oder ein Modernisierungsaufwand zu einer hohen Rendite (Return on Investment, ROI) führt.

Die Cloud bietet verschiedene Einführungsmechanismen mit jeweils ähnlichen Investitions- und Renditegraden. Die Erstellung von cloudnativen Anwendungen kann die Betriebskosten erheblich senken. Sobald eine cloudnative Anwendung freigegeben ist, kann die Entwicklung neuer Features und Lösungen schneller erfolgen. Die Modernisierung einer Anwendung kann zu ähnlichen Vorteilen führen, indem sie Legacyeinschränkungen hinsichtlich lokaler Entwicklungsmodelle beseitigt. Leider sind diese beiden Ansätze arbeitsintensiv und hängen von der Größe, der Qualifikation und der Erfahrung der Softwareentwicklungsteams ab. Häufig ist die Arbeit falsch organisiert. Personen mit der Qualifikation und dem Talent zum Modernisieren von Anwendungen würden eher neue Anwendungen entwickeln. In einem arbeitsintensiven Markt können große Modernisierungsprojekte zu einem Problem hinsichtlich Mitarbeiterzufriedenheit und Talent führen. In einem ausgewogenen Portfolio sollte dieser Ansatz Anwendungen vorbehalten bleiben, die signifikante Featureverbesserungen erhalten würden, wenn sie an einem lokalen Standort verbleiben.

## <a name="envision-an-end-state"></a>Planen des Endzustands

Eine effektive Umsetzung erfordert ein Ziel. Versuchen Sie, eine grobe Vorstellung vom Endzustand zu bekommen, bevor Sie den ersten Schritt machen. Diese Infografik zeigt einen Ausgangspunkt bestehend aus vorhandenen Anwendungen, Daten und einer Infrastruktur, der den digitalen Bestand definiert. Während des Migrationsprozesses wird jede Ressource über eine der Optionen auf der rechten Seite übertragen.

## <a name="migration-implementation"></a>Migrationsimplementierung

Diese Artikel beschreiben zwei Wege, jeweils mit einem ähnlichen Ziel, d. h. einen Großteil der bestehenden Ressourcen nach Azure zu migrieren. Die Geschäftsergebnisse und der aktuelle Zustand werden jedoch die für den Weg dorthin erforderlichen Prozesse erheblich beeinflussen. Diese kleinen Abweichungen führen zu zwei völlig unterschiedlichen Ansätzen, um einen ähnlichen Endzustand zu erreichen.

![Cloud Adoption Framework-Migrationsmodell](../_images/operational-transformation-migrate.png)

Um die inkrementelle Ausführung während des Übergangs in den Endzustand zu steuern, unterteilt dieses Modell die Migration in zwei zentrale Bereiche.

**Migrationsvorbereitung:** Einrichten eines groben Migrationsbacklogs, der größtenteils auf dem aktuellen Zustand und den gewünschten Ergebnissen basiert.

- **Geschäftsergebnisse:** Die wichtigsten Geschäftsziele, die diese Migration fördern.
- **Schätzung des digitalen Bestands:** Eine grobe Schätzung der Anzahl und des Zustands der zu migrierenden Workloads.
- **Rollen und Zuständigkeiten:** Eine klare Definition der Teamstruktur, der Trennung von Zuständigkeiten und der Zugriffsanforderungen.
- **Change Management-Anforderungen:** Der Rhythmus, die Prozesse und die Dokumentation, die zum Überprüfen und Genehmigen von Änderungen erforderlich sind.

Diese ersten Eingaben prägen den Migrationsbacklog. Die Ausgabe des Migrationsbacklogs ist eine priorisierte Liste von Anwendungen, die in die Cloud migriert werden sollen. Diese Liste beeinflusst die Ausführung des Cloudmigrationsprozesses. Im Laufe der Zeit wird sie auch immer größer werden und einen Großteil der Dokumentation enthalten, die für das Change Management erforderlich ist.

**Migrationsprozess:** Jede Cloudmigrationsaktivität ist in einem der folgenden Prozesse enthalten, da sie sich auf den Migrationsbacklog bezieht.

- **Bewerten:** Bewerten Sie eine bestehende Ressource, und erstellen Sie einen Plan für die Migration der Ressource.
- **Migrieren:** Replizieren Sie die Funktionalität einer Ressource in der Cloud.
- **Optimieren:** Gleichen Sie Leistung, Kosten, Zugriff und Betriebskapazität einer Cloudressource aus.
- **Sichern und Verwalten:** Stellen Sie sicher, dass ein Cloudressource für den laufenden Betrieb bereit ist.

Die bei der Entwicklung eines Migrationsbacklogs gesammelten Informationen bestimmen die Komplexität und den Aufwand, der innerhalb des Cloudmigrationsprozesses bei jeder Iteration und für jedes Release der Funktionalität erforderlich ist.

## <a name="transition-to-the-end-state"></a>Übergang in den Endzustand

Ziel ist eine reibungslose und teilautomatisierte Migration in die Cloud. Der Migrationsprozess verwendet die von einem Cloudanbieter bereitgestellten Tools, um Ressourcen in der Cloud schnell zu replizieren und bereitzustellen. Nach der Überprüfung leitet eine einfache Netzwerkänderung die Benutzer zur Cloudlösung um. Für viele Anwendungsfälle ist die Technologie zur Erreichung dieses Ziels weitgehend verfügbar. Es gibt Beispielfälle, die die Geschwindigkeit demonstrieren, mit der 10.000 virtuelle Computer in Azure repliziert werden können.

Allerdings ist weiterhin ein inkrementeller Migrationsansatz erforderlich. In den meisten Umgebungen muss die lange Liste der zu migrierenden virtuellen Computer in kleinere Arbeitseinheiten unterteilt werden, damit eine Migration erfolgreich sein kann. Es gibt viele Faktoren, die die Anzahl der virtuellen Computer begrenzen, die in einem bestimmten Zeitraum migriert werden können. Die Geschwindigkeit des ausgehenden Netzwerks ist eine der wenigen technischen Einschränkungen. Die meisten Einschränkungen ergeben sich aus der Fähigkeit des Unternehmens, Änderungen zu überprüfen und anzupassen.

Der inkrementelle Migrationsansatz des Cloud Adoption Frameworks hilft bei der Erstellung eines inkrementellen Plans, der technische und kulturelle Einschränkungen widerspiegelt und dokumentiert. Ziel dieses Modells ist es, die Migrationsgeschwindigkeit zu maximieren und gleichzeitig den Aufwand für IT und Unternehmen zu minimieren. Nachfolgend finden Sie zwei Beispiele für eine inkrementelle Migrationsausführung basierend auf dem Migrationsbacklog.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./azure-migration-guide/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Leitfaden zur Azure-Migration</h3>
                        <p><b>Erzählerische Zusammenfassung:</b> Dieser Kunde migriert weniger als 1.000 virtuelle Computer. Weniger als zehn unterstützte Anwendungen befinden sich im Besitz eines Anwendungsbesitzers, der nicht der IT-Organisation angehört. Die restlichen Anwendungen, virtuellen Computer und zugehörigen Daten sind im Besitz von Mitgliedern des Cloudeinführungsteams und werden von diesen unterstützt. Mitglieder des Cloudeinführungsteams haben administrativen Zugriff auf die Produktionsumgebungen im bestehenden Rechenzentrum.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./expanded-scope/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Leitfaden zum komplexen Szenario</h3>
                        <p><b>Erzählerische Zusammenfassung:</b> Die Migration dieses Kunden ist hinsichtlich Geschäft, Kultur und Technologie komplex. Dieser Leitfaden enthält mehrere bestimmte Herausforderungen hinsichtlich der Komplexität und Methoden zur Bewältigung dieser Herausforderungen.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

Diese beiden Lösungen stellen zwei extreme Erfahrungswerte für Kunden dar, die in die Cloudmigration investieren. Die meisten Unternehmen spiegeln eine Kombination der beiden oben genannten Szenarien wider. Nach der Durchsicht der Lösung können Sie mit dem Cloud Adoption Framework-Migrationsmodell die Migrationskommunikation beginnen und die Basislösungen weiter an Ihre Bedürfnisse anpassen.

## <a name="next-steps"></a>Nächste Schritte

Wählen Sie eine dieser Lösungen aus:

> [!div class="nextstepaction"]
> [Leitfaden zur Azure-Migration](./azure-migration-guide/index.md)
>
> [Leitfaden zum erweiterten Umfang](./expanded-scope/index.md)
