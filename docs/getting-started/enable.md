---
title: Ermöglichen von Kundenerfolg während einer Cloudeinführungsjourney
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ermöglichen des Kundenerfolgs im gesamten Verlauf einer Cloudeinführungsjourney
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: overview
layout: LandingPage
ms.openlocfilehash: f2892dbfab86da07db2441aea7757846903ff7e9
ms.sourcegitcommit: 3669614902627f0ca61ee64d97621b2cfa585199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2019
ms.locfileid: "73656593"
---
# <a name="enable-success-during-a-cloud-adoption-journey"></a>Ermöglichen des Erfolgs während einer Cloudeinführungsjourney

Das Framework für die Cloudeinführung (Cloud Adoption Framework) ist ein kostenloses Self-Service-Tool, das die Leser durch verschiedene Cloudeinführungsmaßnahmen leitet. Das Framework hilft Kunden dabei, Geschäftsziele erfolgreich umzusetzen, die durch Microsoft Azure ermöglicht werden können. In diesem Inhalt wird jedoch auch berücksichtigt, dass der Leser sich möglicherweise mit vielfältigen geschäftlichen, kulturellen oder technischen Herausforderungen auseinandersetzen muss, die manchmal eine cloudneutrale Position erfordern. Daher beginnt jeder Abschnitt dieser Anleitung zunächst mit einem Azure-Ansatz, auf den eine cloudneutrale Theorie folgt, die sich über viele geschäftliche und technische Entscheidungen hinweg skalieren lässt.

In diesem Framework ist „Enablement“ (Befähigung, Ermöglichen) ein Kernthema. In der folgenden Prüfliste sind grundlegende Cloudeinführungsprinzipien aufgelistet, die sicherstellen, dass eine Einführungsjourney sowohl von der IT-Abteilung als auch von der Geschäftsleitung als erfolgreich eingestuft wird:

- **Planung:** Festlegen klarer [Geschäftsergebnisse](../strategy/business-outcomes/index.md), eines klar definierten [Plans für digitale Ressourcen](../digital-estate/index.md) und weithin verstandener [Einführungsbacklogs](../migrate/migration-considerations/prerequisites/migration-backlog-review.md).
- **Bereit:** Sicherstellen der Bereitschaft der Mitarbeiter durch [Qualifikationen und Lernpläne](../ready/technical-skills.md).
- **Betrieb:** Definieren Sie ein verwaltbares Betriebsmodell, um die Aktivitäten während und lange nach der Einführung zu steuern.
  - **[Organisation](../organize/index.md):** Richten Sie Mitarbeiter und Teams so aus, dass sie einen reibungslosen Cloudbetrieb und eine problemlose Einführung sicherstellen.
  - **Governance:** Definieren geeigneter [Governancedisziplinen](../govern/index.md) zur konsequenten Anwendung von Kostenmanagement-, Risikominderungs-, Compliance- und Sicherheitsbaselines über die gesamte Cloudeinführung hinweg.
  - **Verwalten:** Fortlaufende [Betriebsverwaltung](../manage/index.md) des IT-Portfolios, um Unterbrechungen der Geschäftsprozesse zu minimieren und die Stabilität des IT-Portfolios zu gewährleisten.
  - **Support:** Ausrichten der [Optionen für Partnerschaften und Unterstützung](../migrate/migration-considerations/assess/partnership-options.md).

## <a name="additional-tools"></a>Weitere Tools

Zusätzlich zum Framework für die Cloudeinführung (Cloud Adoption Framework) deckt Microsoft zusätzliche Themen ab, die den Erfolg ermöglichen. In diesem Artikel werden einige gängige Tools vorgestellt, die den Erfolg über den Rahmen des Frameworks für die Cloudeinführung hinaus deutlich verbessern können. Die Schaffung von Cloudgovernance, resilienten Architekturen, technischen Qualifikationen und einem DevOps-Ansatz sind für den Erfolg jeder Cloudeinführungsmaßnahme wichtig. Dem Leser wird empfohlen, ein Lesezeichen für diese Seite anzulegen, um sie während der gesamten Cloudeinführungsreise als Ressource zu nutzen.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsH">
<li style="display: flex; flex-direction: column;">
    <a href="../govern/guides/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Cloud Adoption Framework governance model" src="../_images/operational-transformation-govern-highres.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Cloud Governance</h3>
                        <p>Verstehen von Geschäftsrisiken, Zuordnen der richtigen Richtlinien und Prozesse zu diesen Risiken. Mithilfe von Cloudgovernancetools und den fünf Disziplinen der Cloud Governance können Sie Risiken minimieren und die Wahrscheinlichkeit des Erfolgs verbessern. Cloudgovernance hilft Ihnen, die Kosten zu steuern, Konsistenz zu schaffen, die Sicherheit zu verbessern und die Bereitstellung zu beschleunigen.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/framework/resiliency/overview" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Resilient architecture" src="https://docs.microsoft.com/azure/architecture/resiliency/images/redundancy.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Zuverlässige Architektur (Resilienz)</h3>
                        <p>Die Erstellung einer zuverlässigen Anwendung in der Cloud unterscheidet sich von der herkömmlichen Anwendungsentwicklung. Früher haben Sie wahrscheinlich höherwertige Hardware angeschafft, um zentral hochzuskalieren. In einer Cloudumgebung wird jedoch nicht zentral hochskaliert, sondern horizontal. Es geht nicht darum, Fehler vollständig zu verhindern, sondern darum, die Auswirkungen einer einzelnen fehlerhaften Komponente zu minimieren.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="../ready/technical-skills.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Build Technical Skills" src="https://docs.microsoft.com/media/learn/Product/Learn/learningpath_graphic.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Entwickeln von technischen Fähigkeiten</h3>
                        <p>Das beste Tool zur Unterstützung bei einer erfolgreichen Cloudeinführung ist ein gut ausgebildetes Team. Erweitern Sie die Qualifikationen der vorhandenen Mitglieder geschäftlicher und technischer Teams mithilfe gezielter Lernpfade.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/devops/learn/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Learn DevOps" src="https://docs.microsoft.com/azure/devops/learn/_img/learn-devops.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>DevOps-Ansatz</h3>
                        <p>Der historische Wandel von Microsoft ist fest verwurzelt in einen wachstumsorientierten Ansatz hinsichtlich der Geschäftskultur und einen DevOps-Ansatz bezogen auf die technische Umsetzung. Beide Ansätze sind im gesamten Framework für die Cloudeinführung eingebettet. Um die DevOps-Einführung zu beschleunigen, lesen Sie die DevOps-Lerninhalte.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Architecture Center" src="https://docs.microsoft.com/azure/architecture/example-scenario/data/media/architecture-data-warehouse.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Azure Architecture Center</h3>
                        <p>Architekturlösungen, Referenzarchitekturen, Beispielszenarien, bewährte Methoden und Cloudentwurfsmuster zur Unterstützung bei der die Architektur von Lösungen, die in Azure ausgeführt werden.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://azure.microsoft.com/pricing/calculator/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Pricing Calculator" src="../_images/calculator-preview.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Azure-Preisrechner</h3>
                        <p>Berechnen der Kosten für verschiedene zum Erstellen und Migrieren einer ausgewählten Lösung erforderliche Azure-Komponenten.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Nächste Schritte

Bewaffnet mit einem Verständnis der wichtigsten Aspekte des Frameworks für die Cloudeinführung, wird die Erfolgswahrscheinlichkeit von [Migrationsmaßnahmen](./migrate.md) oder [Innovationsschritten](./innovate.md) umso höher sein.

> [!div class="nextstepaction"]
> [Migrieren](./migrate.md)
>
> [Innovation](./innovate.md)
