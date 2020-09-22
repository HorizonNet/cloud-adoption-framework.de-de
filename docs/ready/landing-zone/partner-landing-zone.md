---
title: Partneroptionen für die Implementierung von Azure-Zielzonen
description: Erfahren Sie, wie Sie Partnerimplementierungsoptionen für Azure-Zielzonen überprüfen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/07/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6ff7dad3524f00119b161dfc87aaa1a70a2b4e19
ms.sourcegitcommit: 8b82889dca0091f3cc64116f998a3a878943c6a1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89602191"
---
# <a name="evaluate-a-microsoft-partners-azure-landing-zone"></a>Evaluieren der Azure-Zielzone eines Microsoft-Partners

Das Cloud Adoption Framework geht die Cloudeinführung als eine Self-Service-Aktivität an. Ziel ist es, die einzelnen Teams, die die Einführung unterstützen, durch standardisierte Ansätze zu unterstützen. In der Praxis können Sie nicht davon ausgehen, dass ein Self-Service-Ansatz für alle Einführungsmaßnahmen ausreichend ist.

Erfolgreiche Cloudeinführungsprogramme umfassen in der Regel mindestens eine Unterstützungsebene durch Drittanbieter. Viele Cloudeinführungsmaßnahmen erfordern Unterstützung durch einen Systemintegrator (SI) oder Beratungspartner, der Dienste bereitstellt, die die Cloudeinführung beschleunigen. Anbieter verwalteter Dienste (Managed Service Providers, MSPs) bieten einen dauerhaften Wert durch Unterstützung von Zielzonen und Cloudeinführung, bieten aber auch Unterstützung für die Betriebsverwaltung nach der Einführung. Darüber hinaus beteiligen erfolgreiche Cloudeinführungsmaßnahmen tendenziell einen oder mehrere unabhängige Softwareanbieter (ISV), die softwarebasierte Dienste bereitstellen, die die Cloudeinführung beschleunigen. Die umfangreichen Partnerökosysteme aus SIs, ISVs, MSPs und anderen Arten von Microsoft-Partnern haben ihre Angebote an bestimmten Methodiken im Cloud Adoption Framework ausgerichtet. Wenn sich ein Partner an der Bereitschaftsmethodik dieses Frameworks orientiert, bietet er wahrscheinlich eine eigene Implementierungsoption für Azure-Zielzonen an.

Dieser Artikel enthält eine Reihe von Fragen, die Ihnen dabei helfen, ein Verständnis für den Umfang der Implementierungsoptionen für Azure-Zielzonen des Partners zu erhalten.

> [!IMPORTANT]
> Partnerangebote und Implementierungsoptionen für Azure-Zielzonen werden vom Partner definiert, basierend auf dessen umfassender Erfahrung bei der Unterstützung von Kunden bei der Einführung der Cloud.
>
> Partner können sich entschließen, die Implementierung bestimmter Entwurfsbereiche in ihrer anfänglichen Implementierung der Zielzone auszulassen. Sie sollten jedoch in der Lage sein, zu kommunizieren, wann und wie die einzelnen Entwurfsbereiche implementiert werden sowie eine Reihe von Kosten für die Fertigstellung des jeweiligen Entwurfsbereichs, wann immer dies möglich ist.
>
> Andere Partnerlösungen können flexibel genug sein, um mehrere Optionen für jede der folgenden Fragen zu unterstützen. Verwenden Sie diese Fragen, um sicherzustellen, dass Sie Partnerangebote und Self-Service-Optionen gleichwertig vergleichen.

## <a name="find-a-partner"></a>Einen Partner suchen

Wenn Sie einen Partner für die Implementierung Ihrer Azure-Zielzone benötigen, beginnen Sie mit der genehmigten Liste der Cloud Adoption Framework-Partner. Beginnen Sie insbesondere mit Partnern, die [Angebote haben, die sich an der Bereitschaftsmethodik orientieren](https://www.microsoft.com/azure/partners/adopt?filters=ready).

Darüber hinaus wurden alle [Azure Expert Managed Services Provider (MSPs)](https://www.microsoft.com/azure/partners/azureexpertmsp?filters=all) auditiert, um ihre Fähigkeit zu validieren, die jeweilige Methodik des Cloud Adoption Framework bereitzustellen. Ein bestimmter Partner mag zwar eventuell kein angepasstes Angebot besitzen, doch alle Partner haben während der technischen Lieferung ihre Ausrichtung nachgewiesen.

## <a name="validate-a-partner-offer"></a>Validieren eines Partnerangebots

Nachdem ein Partner ausgewählt wurde, verwenden Sie den Rest dieses Artikels, um sich durch die Validierung des Partnerangebots führen zu lassen. Jeder Abschnitt enthält eine Zusammenfassung dessen, wonach Sie suchen sollten, sowie eine Liste mit Fragen, die Sie dem Partner stellen sollten. Die Antworten des jeweiligen Partners auf diese Fragen sollten nicht als richtig oder falsch betrachtet werden. Stattdessen sind die Fragen so konzipiert, dass Sie besser bewerten können, ob das Partnerangebot Ihren Geschäftsanforderungen gerecht wird.

## <a name="platform-development-velocity"></a>Entwicklungsgeschwindigkeit der Plattform

Wie in den [Implementierungsoptionen für Azure-Zielzonen](./implementation-options.md) beschrieben, gibt es zwei generelle Ansätze für die Implementierung von Zielzonen, die darauf basieren, wie Sie Ihre Zielzonen entwickeln möchten.

**Frage an den Partner:** Welche der folgenden Ansätze werden von der Azure-Zielzonenlösung des Partners unterstützt?

- **Klein anfangen und erweitern:** Mit einer schlanken Vorlage beginnen. Die Zielzonenlösung reift im Laufe der Zeit, so wie Ihr gewünschtes Modell für den Betrieb der Cloud klarer wird.
- **Auf Unternehmensniveau beginnen:** Mit einer umfassenderen Referenzimplementierung beginnen. Die Referenzarchitektur basiert auf einem klar definierten Modell für den Betrieb der Cloud, das weniger Iterationen erfordert, um eine ausgereifte Lösung zu erzielen.
- **Sonstige:** Der Partner verfügt über einen modifizierten Ansatz und sollte in der Lage sein, den Ansatz zu beschreiben.

## <a name="design-principles"></a>Entwurfsprinzipien

Alle Azure-Zielzonen müssen den folgenden Satz allgemeiner Entwurfsbereiche berücksichtigen. Wir bezeichnen die Art, in der diese Entwurfsbereiche implementiert werden, als Entwurfsprinzipien. Die folgenden Abschnitte werden Ihnen bei der Validierung der Entwurfsprinzipien helfen, die die Implementierung der Azure-Zielzone definieren.

### <a name="deployment-options"></a>Bereitstellungsoptionen

Partner, die eine Azure-Zielzonenlösung anbieten, unterstützen möglicherweise eine oder mehrere Optionen zum Bereitstellen (oder Ändern/Erweitern der Zielzone) der Lösung in Ihrem Azure-Mandanten.

**Frage an den Partner:** Welchen der folgenden Ansätze unterstützt Ihre Azure-Zielzonenlösung?

- **Automatisierung der Konfiguration:** Stellt die Lösung die Zielzone aus einer Bereitstellungspipeline oder einem Bereitstellungstool bereit?
- **Manuelle Konfiguration:** Ermöglicht die Lösung dem IT-Team, die Zielzone manuell zu konfigurieren, ohne Fehler in den Quellcode der Zielzone einzuführen?

**Frage an den Partner:** Welche der folgenden Implementierungsoptionen für Azure-Zielzonen werden von der Lösung des Partners unterstützt? Eine vollständige Liste der Optionen finden Sie im Artikel [Implementierungsoptionen für Azure-Zielzonen](./implementation-options.md).

### <a name="identity"></a>Identity

Identität ist vielleicht der wichtigste Entwurfsbereich, der in der Partnerlösung evaluiert werden sollte.

**Frage an den Partner:** Welche der folgenden Optionen für die Identitätsverwaltung unterstützt die Partnerlösung?

- **Azure AD:** Die empfohlene bewährte Methode besteht darin, Azure AD und rollenbasierte Zugriffssteuerung zu verwenden, um Identität und Zugriff in Azure zu verwalten.
- **Active Directory:** Wenn dies erforderlich ist, stellt die Partnerlösung eine Option bereit, um Active Directory als IaaS-Lösung (Infrastructure-as-a-Service) bereitzustellen?
- **Identitätsanbieter von Drittanbietern:** Wenn Ihr Unternehmen eine Drittanbieter-Identitätslösung verwendet, bestimmen Sie, ob und wie sich die Azure-Zielzone des Partners in die Drittanbieterlösung integrieren lässt.

### <a name="network-topology-and-connectivity"></a>Netzwerktopologie und -konnektivität

Netzwerk ist wohl der zweitwichtigste Entwurfsbereich, der evaluiert werden sollte. Es gibt verschiedene bewährte Methoden für die Netzwerktopologie und -konnektivität.

**Frage an den Partner:** Welcher der folgenden Ansätze ist in der Azure-Zielzonenlösung des Partners enthalten? Sind von den folgenden Optionen welche mit der Lösung des Partners nicht kompatibel?

- **Virtuelles Netzwerk:** Konfigurieren die Partnerlösung ein virtuelles Netzwerk? Kann seine Topologie so geändert werden, dass sie Ihre technischen oder geschäftlichen Vorgaben erfüllt?
- **Virtuelles privates Netzwerk (VPN):** Ist die VPN-Konfiguration im Entwurf des Partners für die Zielzone enthalten, um die Cloud mit vorhandenen Rechenzentren oder Niederlassungen zu verbinden?
- **Hochgeschwindigkeitskonnektivität:** Ist im Entwurf der Zielzone eine Hochgeschwindigkeitsverbindung wie Azure ExpressRoute enthalten?
- **Peering virtueller Netzwerke:** Umfasst der Entwurf Konnektivität zwischen verschiedenen Abonnements oder virtuellen Netzwerken in Azure?

### <a name="resource-organization"></a>Ressourcenorganisation

Die vernünftige Governance und Betriebsverwaltung der Cloud beginnt mit der Ressourcenorganisation gemäß bewährten Methoden.

**Frage an den Partner:** Berücksichtigt der Partnerentwurf der Zielzone die folgenden Methoden für die Ressourcenorganisation?

- **Benennungsstandards:** Welche [Benennungsstandards](../azure-best-practices/naming-and-tagging.md) hält dieses Angebot ein, und wird dieser Standard automatisch durch eine Richtlinie erzwungen?
- **Markierungsstandards:** Befolgt und erzwingt die Zielzonenkonfiguration bestimmte [Standards für das Markieren von Ressourcen](../azure-best-practices/naming-and-tagging.md#metadata-tags)?
- **Abonnemententwurf:** Welche [Abonnemententwurfsstrategien](../../decision-guides/subscriptions/index.md) werden vom Partnerangebot unterstützt?
- **Verwaltungsgruppenentwurf:** Befolgt das Partnerangebot ein definiertes Muster für die [Azure-Verwaltungsgruppenhierarchie](../azure-best-practices/organize-subscriptions.md), um Abonnements zu organisieren?
- **Ressourcengruppenausrichtung:** Wie werden Ressourcengruppen verwendet, um in der Cloud bereitgestellte Ressourcen zu gruppieren? Werden Ressourcengruppen im Partnerangebot verwendet, um Ressourcen in Workloads, Bereitstellungspaketen oder anderen Organisationsstandards zu gruppieren?

**Frage an den Partner:** Stellt der Partner eine Onboardingdokumentation bereit, um [grundlegende Entscheidungen nachzuverfolgen](../../get-started/cloud-concepts.md) und Mitarbeiter zu schulen? Ein Beispiel für eine solche Dokumentation finden Sie in der [Vorlage für anfängliche Entscheidungen](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/references/initial-decisions-checklist.docx).

### <a name="governance-disciplines"></a>Disziplinen der Governance

Ihre Governanceanforderungen können sich stark auf komplexe Entwürfe von Zielzonen auswirken. Viele Partner bieten ein separates Angebot, um Governancedisziplinen im Anschluss an die Bereitstellung der Zielzonen vollständig zu implementieren. Die folgenden Fragen helfen Ihnen dabei, Klarheit bezüglich der Aspekte der Governance zu schaffen, die in alle Zielzonen integriert werden.

**Frage an den Partner:** Welche Governancetools beinhaltet die Partnerlösung als Teil der Implementierung der Zielzone?

- **Überwachung der Richtliniencompliance:** Umfasst die Zielzonenlösung des Partners definierte Governancerichtlinien sowie Tools und Prozesse zur Überwachung der Compliance? Beinhaltet das Angebot Anpassungen von Richtlinien an Ihre Governanceanforderungen?
- **Erzwingung von Richtlinien:** Umfasst die Zielzonenlösung des Partners automatisierte Erzwingungstools und -prozesse?
- **Cloudplattformgovernance:** Umfasst das Partnerangebot eine Lösung für die Erhaltung der Compliance mit einem allgemeinen Satz von Richtlinien in allen Abonnements? Oder ist der Gültigkeitsbereich auf einzelne Abonnements beschränkt?
- **Nicht zutreffend:** Bei „Klein anfangen“-Ansätzen werden Governanceentscheidungen absichtlich so lange verschoben, bis das Team Workloads mit geringem Risiko in Azure bereitgestellt hat. Dies kann in einem separaten Angebot behandelt werden, nachdem die Zielzonenlösung bereitgestellt wurde.

**Frage an den Partner:** Geht das Partnerangebot über Governancetools hinaus und umfasst auch Prozesse und Methoden, um die folgenden Cloudgovernancedisziplinen bereitzustellen?

- **Kostenverwaltung:** Bereitet das Partnerangebot das Team darauf vor, Ausgaben zu evaluieren, zu überwachen und zu optimieren, bei gleichzeitiger Erzeugung von Kostenverantwortlichkeit bei Workloadteams?
- **Sicherheitsbaseline:** Bereitet das Partnerangebot das Team darauf vor, die Compliance aufrechtzuerhalten, wenn sich Sicherheitsanforderungen ändern und reifen?
- **Ressourcenkonsistenz:** Bereitet das Partnerangebot das Team darauf vor, sicherzustellen, dass alle Ressourcen in der Cloud in relevante Betriebsverwaltungsprozesse integriert werden?
- **Identitätsbaseline:** Bereitet das Partnerangebot das Team darauf vor, Identitäten, Rollendefinitionen und Zuweisungen zu erhalten, nachdem die anfängliche Zielzone bereitgestellt wurde?

### <a name="operations-baseline"></a>Betriebsbaseline

Ihre Anforderungen an die Betriebsverwaltung können die Konfiguration bestimmter Azure-Produkte während der Implementierung der Zielzone beeinflussen. Viele Partner bieten ein separates Angebot, um die Betriebsbaseline und den erweiterten Betrieb zu einem späteren Zeitpunkt in der Cloudeinführungsphase vollständig zu implementieren, aber noch bevor die erste Workload für die produktive Verwendung freigegeben wird. Die Lösung des Partners für die Zielzone kann aber auch standardmäßig eine Konfiguration für eine Reihe von Betriebsverwaltungstools beinhalten.

**Frage an den Partner:** Beinhaltet die Partnerlösung Entwurfsoptionen zur Unterstützung der Cloudbetriebsdisziplinen?

- **Bestand und Transparenz:** Beinhaltet die Zielzone Tools, um sicherzustellen, dass 100 % der Ressourcen zentral überwacht werden?
- **Betriebsbezogene Compliance:** Umfasst die Architektur Tools und automatisierte Prozesse, um Patching oder andere Anforderungen der betriebsbezogenen Compliance zu erzwingen?
- **Schutz und Wiederherstellung:** Umfasst das Partnerangebot Tools und Konfigurationen, um einen Mindeststandard an Sicherung und Wiederherstellung für 100 % der bereitgestellten Ressourcen sicherzustellen?
- **Plattformbetrieb:** Umfasst das Zielzonenangebot Tools oder Prozesse, zur Optimierung von Vorgängen im gesamten Portfolio?
- **Workloadbetrieb:** Umfasst das Zielzonenangebot Tools zum Verwalten workloadspezifischer Betriebsanforderungen und zur Sicherstellung, dass jede Workload gut strukturiert ist?

## <a name="take-action"></a>Ausführen einer Aktion

Nachdem Sie das Angebot oder die Lösung des Partners für Azure-Zielzonen mithilfe der oben genannten Fragen geprüft haben, ist Ihr Team besser vorbereitet, um den Partner auszuwählen, dessen Azure-Zielzone am engsten an Ihrem Modell für den Betrieb der Cloud ausgerichtet ist.

Wenn Sie feststellen, dass ein Self-Service-Ansatz bei der Bereitstellung der Azure-Zielzone besser geeignet ist, überprüfen Sie die [Implementierungsoptionen für Azure-Zielzonen](./implementation-options.md), bzw. sehen Sie sich diese noch mal an, um den auf einer Vorlage basierenden Ansatz für eine Zielzone zu finden, der sich am besten an Ihrem Modell für den Betrieb der Cloud orientiert.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über den Prozess zum Refactoring von Zielzonen.

> [!div class="nextstepaction"]
> [Umgestalten von Zielzonen](./refactor.md)
