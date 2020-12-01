---
title: Plattformbetrieb in der Cloudverwaltung
description: Machen Sie sich mit der Abhängigkeit vertraut, die in Ihrer Organisation für häufige Plattformvorgänge bei der Cloudverwaltung besteht.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 30c07aa131b31ea6e410afc6dfa6cc10adac041c
ms.sourcegitcommit: 412b945b3492ff3667c74627524dad354f3a9b85
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2020
ms.locfileid: "94879751"
---
# <a name="platform-operations-in-cloud-management"></a>Plattformbetrieb in der Cloudverwaltung

Eine Cloudverwaltungs-Baseline, die sich über [Bestand und Transparenz](./inventory.md), [betriebsbezogene Compliance](./operational-compliance.md) und [Schutz und Wiederherstellung](./protect.md) erstreckt, kann für die meisten Workloads im IT-Portfolio ein ausreichendes Maß an Cloudverwaltung bieten. Diese Baseline reicht jedoch nur selten aus, um das gesamte Portfolio zu unterstützen. Dieser Artikel basiert auf dem gängigsten nächsten Schritt im Bereich Cloudverwaltung, dem Portfoliobetrieb.

Eine schnelle Analyse der Ressourcen im IT-Portfolio zeigt Muster der unterstützten Workloads auf. Innerhalb dieser Workloads gibt es gemeinsame Plattformen. Abhängig von den bisherigen IT-bezogenen Entscheidungen im Unternehmen können diese Plattformen sehr unterschiedlich sein.

In einigen Organisationen besteht eine starke Abhängigkeit von SQL Server, Oracle oder anderen Open-Source-Datenplattformen. In anderen Unternehmen können die Gemeinsamkeiten sich auf die Hostingplattformen für virtuelle Computer (VMs) oder Container beziehen. In wieder anderen Fällen besteht möglicherweise eine allgemeine Abhängigkeit von Anwendungen oder Enterprise-Resource-Planning-Systemen (ERP) wie SAP oder Oracle.

Das Verständnis dieser Gemeinsamkeiten ermöglicht es dem Cloudverwaltungsteam, sich für diese priorisierten Plattformen auf ein höheres Maß an Support zu spezialisieren.

## <a name="establish-a-service-catalog"></a>Einrichten eines Dienstkatalogs

Ziel des Plattformbetriebs ist es, zuverlässige und wiederholbare Lösungen zu entwickeln, die von einem Cloudeinführungsteam genutzt werden können, um eine Plattform bereitzustellen, die ein höheres Maß an Verpflichtung gegenüber den Fachbereichen ermöglicht. Diese Verpflichtung kann die Wahrscheinlichkeit oder Häufigkeit von Ausfallzeiten verringern und dadurch die Zuverlässigkeit erhöhen. Die Verpflichtung kann auch bei einem Systemausfall den Umfang des Datenverlusts oder die Zeit bis zur Wiederherstellung verringern. Diese Verpflichtung schließt oft laufende, zentralisierte Abläufe zur Unterstützung der Plattform ein.

Wenn das Cloudverwaltungsteam einen höheren Grad an betrieblicher Verwaltung und Spezialisierung in Bezug auf bestimmte Plattformen etabliert, werden diese Plattformen in einen ständig wachsenden Dienstkatalog aufgenommen. Der Dienstkatalog bietet eine Self-Service-Bereitstellung von Plattformen mit einer bestimmten Konfiguration, die dem laufenden Plattformbetrieb gerecht wird. Während des Gesprächs zur geschäftliche Abstimmung können das Cloudverwaltungs- und Cloudstrategieteam Dienstkataloglösungen vorschlagen, um die Zuverlässigkeit, Betriebszeit und Wiederherstellungsverpflichtungen in einem kontrollierten, wiederholbaren Prozess zu verbessern.

Zur Bezugnahme wird ein Dienstkatalog in der Frühphase in einigen Unternehmen als _genehmigte Liste_ bezeichnet. Der Hauptunterschied besteht darin, dass ein Dienstkatalog mit laufenden Betriebsverpflichtungen aus dem Cloudkompetenzzentrum (CCoE) einhergeht. Eine genehmigte Liste ist ähnlich, da sie eine vorab genehmigte Liste von Lösungen enthält, die ein Team in der Cloud verwenden kann. In der Regel gibt es jedoch keinen operativen Vorteil, der mit Anwendungen auf einer genehmigten Liste verbunden ist.

Ähnlich wie bei der Debatte über die zentrale IT und das CCoE ist auch hier der Unterschied eine Frage der Prioritäten. Ein Dienstkatalog geht von guter Absicht aus, bietet jedoch Leitlinien für Betrieb, Governance und Sicherheit, die Innovation beschleunigen. Eine genehmigte Liste hemmt Innovation, bis eine Lösung die Anforderungen an Betrieb, Konformität und Sicherheit erfüllen kann. Beide Lösungen sind praktikabel, erfordern aber, dass ein Unternehmen subtile Priorisierungsentscheidungen trifft, um mehr in Innovation oder Compliance zu investieren.

### <a name="build-the-service-catalog"></a>Erstellen des Dienstkatalogs

Die Cloudverwaltung ist nur selten erfolgreich, wenn ein Dienstleistungskatalog wie in einem Silo isoliert bereitgestellt wird. Die ordnungsgemäße Entwicklung des Katalogs erfordert eine Partnerschaft im gesamten zentralen IT-Team oder dem Cloudkompetenzzentrum (CCoE). Dieser Ansatz ist in der Regel am erfolgreichsten, wenn eine IT-Organisation einen gewissen CCoE-Reifegrad erreicht, kann aber früher umgesetzt werden.

Beim Erstellen des Dienstkatalogs im Rahmen eines CCoE-Modells errichtet das Cloudplattformteam die Plattform im gewünschten Zustand. Das Cloudgovernance- und Cloudsicherheitsteam überprüfen Governance und Konformität innerhalb der Bereitstellung. Das Cloudverwaltungsteam richtet den laufenden Betrieb der Plattform ein. Und das Cloudautomatisierungsteam erstellt ein Paket der Plattform für eine skalierbare, wiederholbare Bereitstellung.

Nachdem die Plattform verpackt ist, kann das Cloudverwaltungsteam sie dem wachsenden Dienstkatalog hinzufügen. Danach kann das Cloudeinführungsteam dieses Paket oder andere im Katalog während der Bereitstellung nutzen. Nachdem die Lösung in Produktion geht, realisiert das Unternehmen die zusätzlichen Vorteile einer verbesserten Betriebsführung bei gleichzeitiger Reduzierung von Betriebsunterbrechungen.

> [!NOTE]
> Der Aufbau eines Dienstkatalogs erfordert viel Aufwand und Zeit von mehreren Teams. Die Verwendung des Dienstkatalogs oder der genehmigten Liste als Steuermechanismus führt zu einer Verlangsamung von Innovation. Wenn Innovation eine Priorität ist, sollten Dienstkataloge parallel zu anderen Implementierungsbemühungen entwickelt werden.

## <a name="define-your-own-platform-operations"></a>Definieren des eigenen Plattformbetriebs

Obwohl Verwaltungstools und -prozesse dazu beitragen können, den Plattformbetrieb zu verbessern, reicht das oft nicht aus, um die gewünschten Zustände an Stabilität und Zuverlässigkeit zu erreichen. Echter Plattformbetrieb erfordert eine Fokussierung auf die Säulen der Architekturexzellenz. Wenn eine Plattform eine höhere Investition in den Betrieb rechtfertigt, berücksichtigen Sie die folgenden fünf Säulen, bevor die Plattform in einen Dienstkatalog aufgenommen wird:

- **Kostenoptimierung:** Verwalten der Kosten zur Maximierung des erzielten Werts.
- **Betriebliche Exzellenz:** Verfolgen der operativen Prozesse, die für die Ausführung eines Systems in der Produktion sorgen.
- **Effiziente Leistung:** Skalieren Sie Systeme so, dass Sie in Bezug auf Änderungen der Last flexibel sind.
- **Zuverlässigkeit:** Entwerfen Sie Systeme so, dass sie nach Ausfällen wiederhergestellt und weiterhin ausgeführt werden können.
- **Sicherheit**: Schützen Sie Anwendungen und Daten vor Bedrohungen.

Das [Microsoft Azure Well-Architected Framework](/azure/architecture/framework) bietet einen Ansatz zur Bewertung spezifischer Workloads hinsichtlich der Einhaltung dieser Vorgaben, um so den Gesamtbetrieb zu verbessern. Diese Eckpfeiler können sowohl für den Plattform- als auch den Workloadbetrieb gelten.

## <a name="get-started-with-specific-platforms"></a>Erste Schritte mit bestimmten Plattformen

Die in den nächsten Abschnitten besprochenen Plattformen sind typischen Azure-Kunden gemeinsam und können eine Investition in den Plattformbetrieb leicht rechtfertigen. Cloudverwaltungsteams orientieren sich in der Regel an ihnen, wenn sie Plattformbetriebsanforderungen oder einen umfassenden Dienstkatalog erstellen.

### <a name="paas-data-operations"></a>PaaS-Datenvorgänge

Daten sind oft die erste Plattform, die Investitionen in den Plattformbetrieb rechtfertigen. Wenn Daten in einer PaaS-Umgebung (Platform as a Service) gehostet werden, neigen die Beteiligten aus den Fachbereichen dazu, eine verkürzte Recovery Point Objective (RPO) zu verlangen, um Datenverlust zu minimieren. Je nach Art der Anwendung können sie auch eine Verkürzung der Recovery Point Objective (RPO) fordern. In beiden Fällen kann die Architektur, die PaaS-basierte Datenlösungen unterstützt, problemlos ein höheres Maß an Verwaltungsunterstützung bieten.

In den meisten Szenarien sind die Kosten für die bessere Einhaltung von Verwaltungsverpflichtungen einfach zu rechtfertigen, selbst bei nicht unternehmenskritischen Anwendungen. Diese Verbesserung des Plattformbetriebs ist so weit gängig, dass viele Cloudverwaltungsteams sie eher als eine verbesserte Baseline anstatt einer echten Verbesserung des Plattformbetriebs betrachten.

### <a name="iaas-data-operations"></a>IaaS-Datenvorgänge

Wenn Daten in einer herkömmlichen IaaS-Lösung (Infrastructure as a Service) gehostet werden, kann der Aufwand für die Verbesserung von RPO und RTO erheblich höher sein. Doch der Wunsch der Beteiligten aus den Fachbereichen, Verwaltungsverpflichtungen besser zu erfüllen, wird selten von einer Entscheidung von PaaS im Vergleich zu IaaS beeinflusst. Wenn überhaupt, kann ein Verständnis der grundlegenden Unterschiede bei der Architektur die Fachbereiche dazu veranlassen, nach PaaS-Lösungen oder Verpflichtungen zu fragen, die dem entsprechen, was für PaaS-Lösungen möglich ist. Die Modernisierung von IaaS-Datenplattformen sollte beim Plattformbetrieb als erster Schritt in Betracht gezogen werden.

Wenn eine Modernisierung nicht möglich ist, priorisieren Cloudverwaltungsteams üblicherweise IaaS-basierte Datenplattformen als ersten erforderlichen Dienst im Dienstkatalog. Indem den Geschäftsbereichen die Wahl zwischen eigenständigen Datenservern und gruppierten, hochverfügbaren Datenlösungen zur Verfügung gestellt wird, wird das Gespräch über die Verpflichtung gegenüber den Fachbereichen wesentlich erleichtert. Ein grundlegendes Verständnis der betrieblichen Verbesserungen und der gestiegenen Kosten hilft dem Unternehmen, die beste Entscheidung über die Geschäftsprozesse und die unterstützenden Workloads zu treffen.

### <a name="other-common-platform-operations"></a>Andere gängige Plattformbetriebsabläufe

Neben Datenplattformen sind Hosts virtueller Computer in der Regel eine gängige Plattform für Betriebsverbesserungen. Am häufigsten investieren Cloudplattform- und Cloudverwaltungsteams in die Verbesserung von VMware-Hosts oder Containerlösungen. Solche Investitionen können die Stabilität und Zuverlässigkeit der Hosts verbessern, die die VMs unterstützen, wodurch wiederum die Workloads unterstützt werden. Der ordnungsgemäße Betrieb auf einem Host oder in einem Container kann die RPO oder RTO mehrerer Workloads verbessern. Dieser Ansatz schafft verbessert die Einhaltung von Verpflichtungen gegenüber den Fachbereichen, verteilt aber die Investitionen. Zusammengenommen machen es die verbesserte Erfüllung von Verpflichtungen und reduzierte Kosten viel einfacher, Verbesserungen bei Cloudverwaltung und Plattformbetrieb zu rechtfertigen.

## <a name="next-steps"></a>Nächste Schritte

Parallel zu den Verbesserungen des Plattformbetriebs konzentrieren sich Cloudverwaltungsteams auch auf die Verbesserung des [Workloadbetriebs](./workload.md) für maximal die oberen 20 Prozent der Produktionsworkloads.

> [!div class="nextstepaction"]
> [Verbessern des Workloadbetriebs](./workload.md)
