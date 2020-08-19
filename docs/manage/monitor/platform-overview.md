---
title: Übersicht über Cloudüberwachungsplattformen
description: Verschaffen Sie sich einen allgemeinen Überblick über zwei Überwachungsplattformen, um sich damit vertraut zu machen, wie jeweils grundlegende Überwachungsfunktionen bereitgestellt werden.
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: d8ab1c31744d3e714d62018bccabd747136f454c
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88571200"
---
<!-- cSpell:ignore opsman ITSM -->

# <a name="cloud-monitoring-guide-monitoring-platforms-overview"></a>Leitfaden zur Cloudüberwachung: Übersicht über Überwachungsplattformen

Microsoft bietet eine Reihe von Überwachungsfunktionen für zwei Produkte: System Center Operations Manager war ursprünglich für lokale Umgebungen vorgesehen und wurde auf die Cloud und Azure Monitor erweitert. Dieses Feature wurde für die Cloud entwickelt, kann jedoch auch zum Überwachen lokaler Systeme verwendet werden. Diese beiden Angebote bieten grundlegende Überwachungsdienste wie Warnungen, Verfolgung der Betriebszeit von Diensten, Überwachung des Zustands von Anwendungen und Infrastrukturen, Diagnosen und Analysen.

Viele Organisationen nutzen die neuesten Verfahren für DevOps-Flexibilität und Cloudinnovationen für die Verwaltung ihrer heterogenen Umgebungen. Sie sind aber auch hinsichtlich ihrer Möglichkeiten besorgt, angemessene und verantwortungsvolle Entscheidungen für die Überwachung dieser Workloads treffen zu können.

Dieser Artikel bietet eine allgemeine Übersicht über unsere Überwachungsplattformen, um zu erläutern, wie jede der beiden Plattformen grundlegende Überwachungsfunktionen bereitstellt.

## <a name="the-story-of-system-center-operations-manager"></a>Die Geschichte von System Center Operations Manager

Im Jahr 2000 sind wir mit Microsoft Operations Manager 2000 in den Bereich Operations Management eingestiegen. Im Jahr 2007 haben wir eine überarbeitete Version des Produkts, System Center Operations Manager, auf den Markt gebracht. Sie bot mehr als nur die einfache Überwachung eines Windows-Servers und konzentrierte sich auf die stabile End-to-End-Überwachung von Diensten und Anwendungen, einschließlich heterogene Plattformen, Netzwerkgeräte und anderen Anwendungs- und Dienstabhängigkeiten. Es handelt sich um eine etablierte, unternehmensweite Überwachungsplattform für lokale Umgebungen, die in dieser Branche in derselben Klasse wie IBM Tivoli oder HP Operations Manager angeordnet ist. Sie ist gewachsen, um die Überwachung von Compute- und Plattformressourcen zu unterstützen, die in Azure, Amazon Web Services (AWS) und unter anderen Cloudanbietern ausgeführt werden.

## <a name="the-story-of-azure-monitor"></a>Die Geschichte von Azure Monitor

Als Azure 2010 auf den Markt kam, wurden Clouddienste mit dem Azure-Diagnose-Agent überwacht, mit dem Diagnosedaten von Azure Ressourcen erfasst werden konnten. Diese Funktion galt als allgemeines Überwachungstool und nicht als Überwachungsplattform für Unternehmen.  

Application Insights wurde eingeführt, um den Änderungen in der Branche, d.h. der zunehmenden Nutzung von Clouddiensten, mobilen und IoT-Geräten sowie von DevOps-Verfahren Rechnung zu tragen. Es wuchs von der Anwendungsleistungsüberwachung in Operations Manager zu einem Dienst in Azure, der eine umfassende Überwachung von in vielfältigen Sprachen geschriebenen Webanwendungen ermöglicht. In 2015 wurde die Vorschauversion von Application Insights für Visual Studio angekündigt, und der spätere Name lautete einfach Application Insights. Der Dienst sammelt Informationen zur Anwendungsleistung, zu Anforderungen und Ausnahmen sowie Ablaufverfolgungen.

2015 wurde von Azure Operational Insights allgemein zur Verfügung gestellt. Dieser Dienst umfasste den Analysedienst Log Analytics, der Daten von Computern in Azure, in lokalen Umgebungen oder anderen Cloudumgebungen sammelte und durchsuchte und außerdem mit System Center Operations Manager verbunden war. Es wurden Intelligence Packs mit verschiedenen vorkonfigurierten Verwaltungs- und Überwachungskonfigurationen angeboten, die eine Sammlung von Abfrage- und Analyselogik, Visualisierungen und Datenerfassungsregeln für Szenarien wie Sicherheitsüberwachung, Integritätsbewertungen und die Verwaltung von Warnungen umfassten. Azure Operational Insights wurde später in Log Analytics umbenannt.  

Im Jahr 2016 wurde die Vorschau von Azure Monitor auf der Konferenz Microsoft Ignite vorgestellt. Es bot ein einheitliches Framework zum Erfassen von Plattformmetriken und Ressourcendiagnoseprotokollen sowie Aktivitätsprotokollereignissen auf Abonnementebene von jedem Azure-Dienst, der das Framework nutzt. Bisher verfügte jeder Azure-Dienst über eine eigene Überwachungsmethode.

Auf der Ignite-Konferenz im Jahr 2018 gaben wir dann bekannt, dass die Marke Azure Monitor um mehrere verschiedene Dienste erweitert wurde, die ursprünglich als eigenständige Funktionen entwickelt wurden:

- Der ursprüngliche **Azure Monitor** zum Erfassen von Plattformmetriken, Ressourcendiagnoseprotokollen und Aktivitätsprotokollen nur für Azure Platform-Ressourcen.
- **Application Insights** für die Anwendungsüberwachung.
- **Log Analytics** als primäre Funktion für die Erfassung und Analyse von Protokolldaten.
- Ein neuer **einheitlicher Warnungsdienst**, in dem die Warnungsmechanismen von allen anderen zuvor erwähnten Diensten zusammengeführt sind.  
- **Azure Network Watcher** für die Überwachung, Diagnose und Anzeige von Metriken für Ressourcen in einem virtuellen Netzwerk.

## <a name="the-story-of-operations-management-suite-oms"></a>Die Geschichte von Operations Management Suite (OMS)

Operations Management Suite (OMS) war von 2015 bis April 2018 eine Bündelung der folgenden Azure-Verwaltungsdienste zu Lizenzzwecken:

- Application Insights
- Azure-Automatisierung
- Azure Backup
- Operational Insights (später in Log Analytics umbenannt)
- Site Recovery

Die Funktionen der Dienste, die Teil von OMS waren, blieben nach der Einstellung von OMS unverändert. Sie wurden unter Azure Monitor neu ausgerichtet.

## <a name="infrastructure-requirements"></a>Infrastrukturanforderungen

### <a name="operations-manager"></a>Operations Manager

Operations Manager benötigt eine umfangreiche Infrastruktur und Wartung zur Unterstützung einer Verwaltungsgruppe. Diese bildet eine grundlegende Funktionseinheit. Eine Verwaltungsgruppe besteht mindestens aus einem oder mehreren Verwaltungsservern, einer SQL Server-Instanz, die die Betriebsdatenbank und die Reporting-Data Warehouse-Datenbank hostet, sowie Agents. Die Komplexität eines Konzepts für eine Verwaltungsgruppe hängt von mehreren Faktoren ab, z. B. dem Umfang der zu überwachenden Workloads und der Anzahl der Geräte oder Computer, die die Workloads unterstützen. Wenn Sie Hochverfügbarkeit und Standortresilienz benötigen, wie es bei Überwachungsplattformen für Unternehmen üblich ist, können die Infrastrukturanforderungen und die damit verbundene Wartung erheblich zunehmen.

![Diagramm zur Operations Manager-Verwaltungsgruppe](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor ist ein SaaS-Angebot (Software-as-a-Service), bei dem die gesamte unterstützende Infrastruktur in Azure ausgeführt und von Microsoft verwaltet wird. Dabei werden Überwachungs-, Analytics- und Diagnosefunktionen im großen Stil durchführt. Es ist in allen nationalen Clouds nicht verfügbar. Die zentralen Komponenten der Infrastruktur (Collectors, Metriken und Protokollspeicher und Analysen), die Azure Monitor unterstützen, werden von Microsoft verwaltet.  

![Diagramm zu Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Datensammlung

<!-- markdownlint-disable MD024 -->

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agents

Operations Manager sammelt nur Daten direkt von Agents, die auf [Windows-Computern](/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent) installiert sind. Er kann Daten aus dem Operations Manager SDK übernehmen, aber dieser Ansatz wird in der Regel für Partner verwendet, die das Produkt durch benutzerdefinierte Anwendungen erweitern, und nicht zur Erfassung von Überwachungsdaten. Er kann Daten von anderen Quellen wie [Linux-Computern](/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) und Netzwerkgeräten erfassen. Dazu werden spezielle Module verwendet, die auf dem Windows-Agent ausgeführt werden, der über eine Remoteverbindung auf diese anderen Geräte zugreift.

![Diagramm zum Operations Manager-Agent](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

Der Operations Manager-Agent kann Daten aus mehreren Datenquellen auf dem lokalen Computer sammeln, z. B. Ereignisprotokoll, benutzerdefinierte Protokolle und Leistungsindikatoren. Er kann auch Skripte ausführen, die Daten vom lokalen Computer oder von externen Quellen sammeln können. Sie können benutzerdefinierte Skripts schreiben, um Daten zu sammeln, die nicht mit anderen Mitteln erfasst werden können oder von einer Vielzahl von Remotegeräten stammen, die anderweitig nicht überwacht werden können.

#### <a name="management-packs"></a>Management Packs

Operations Manager führt die gesamte Überwachung mit Workflows (Regeln, Monitore und Objektermittlungen) durch. Diese Workflows werden in einem [Management Pack](/system-center/scom/manage-overview-management-pack?view=sc-om-2019) zusammengefasst und an Agents verteilt. Für eine Vielzahl von Produkten und Diensten, die vordefinierte Regeln und Monitore enthalten, sind Management Packs verfügbar. Sie können auch Ihr eigenes Management Pack für eigene Anwendungen und benutzerdefinierte Szenarien erstellen.

#### <a name="monitoring-configuration"></a>Überwachungskonfiguration

Management Packs können Hunderte von Regeln, Monitoren und Objektermittlungsregeln enthalten. Ein Agent führt alle diese Überwachungseinstellungen, die durch Ermittlungsregeln bestimmt werden, aus allen entsprechenden Management Packs aus. Jede Instanz der einzelnen Überwachungseinstellungen wird unabhängig voneinander ausgeführt und reagiert sofort auf die von ihr erfassten Daten. Auf diese Weise kann Operations Manager eine Warnung nahezu in Echtzeit ausgeben und den aktuellen Integritätszustand der überwachten Ressourcen ermitteln.

So kann beispielsweise ein Monitor im Abstand von wenigen Minuten einen Leistungsindikator abfragen. Wenn dieser Indikator einen Schwellenwert überschreitet, wird sofort der Integritätszustand seines Zielobjekts festgelegt, wodurch sofort eine Warnung in der Verwaltungsgruppe ausgelöst wird. Eine geplante Regel kann auf die Erstellung eines bestimmten Ereignisses achten und sofort eine Warnung auslösen, wenn dieses Ereignis im lokalen Ereignisprotokoll erstellt wird.

Da die Überwachungseinstellungen voneinander und von den einzelnen Datenquellen isoliert sind, steht Operations Manager vor der Herausforderung, Daten zwischen mehreren Quellen zu korrelieren. Es ist auch schwierig, auf Daten zu reagieren, nachdem diese gesammelt wurden. Sie können Workflows ausführen, die auf die Operations Manager-Datenbank zugreifen. Dieses Szenario ist jedoch nicht gängig und wird typischerweise für eine begrenzte Anzahl von Workflows für spezielle Zwecke verwendet.

![Diagramm zur Operations Manager-Verwaltungsgruppe](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Datenquellen

Azure Monitor sammelt Daten aus einer Vielzahl von Quellen, einschließlich der Azure-Infrastruktur und Plattformressourcen, Agents auf Windows- und Linux-Computern und Überwachungsdaten aus dem Azure-Speicher. Jeder REST-Client kann Protokolldaten über eine API in Azure Monitor schreiben, und Sie können benutzerdefinierte Metriken für Ihre Webanwendungen definieren. Einige Metrikdaten können je nach Verwendung an verschiedene Speicherorte weitergeleitet werden. Sie können die Daten z.B. für eine „schnellstmögliche“ Warnung oder für eine langfristige Trendanalyse verwenden, die in Verbindung mit anderen Protokolldaten gesucht wird.

#### <a name="monitoring-solutions-and-insights"></a>Überwachungslösungen und Insights

Überwachungslösungen nutzen die Protokollplattform in Azure Monitor, um die Überwachung für eine bestimmte Anwendung oder einen bestimmten Dienst bereitzustellen. Sie definieren in der Regel die Datensammlung von Agents oder von Azure-Diensten und bieten Protokollabfragen und Ansichten zur Analyse dieser Daten. Normalerweise stellen sie keine Warnungsregeln bereit. Das bedeutet, dass Sie basierend auf den erfassten Daten selbst Warnungskriterien definieren müssen.

Insights, z. B. Azure Monitor für Container und Azure Monitor für VMs, nutzt die Protokolle und die Metrikplattform von Azure Monitor, um eine maßgeschneiderte Überwachungslösung für eine Anwendung oder einen Dienst im Azure-Portal anzubieten. Sie können neben der kundenspezifischen Analyse der gesammelten Daten auch Bedingungen für die Integritätsüberwachung und Warnungen bereitstellen.

#### <a name="monitoring-configuration"></a>Überwachungskonfiguration

Azure Monitor trennt die Datensammlung von für diese Daten ergriffenen Maßnahmen und unterstützt so verteilte Microservices in einer Cloudumgebung. Er konsolidiert Daten aus mehreren Quellen in einer gemeinsamen Datenplattform und ermöglicht Analyse-, Visualisierungs- und Warnungsfunktionen auf der Grundlage dieser gesammelten Daten.

Die von Azure Monitor gesammelten Daten werden entweder als Protokolle oder Metriken gespeichert, und verschiedene Funktionen von Azure Monitor hängen von diesen Daten ab. Metriken enthalten numerische Werte in Zeitreihen, die sich gut für eine Warnung nahezu in Echtzeit und eine schnelle Erkennung von Problemen eignen. Protokolle enthalten Text oder numerische Daten und können mithilfe einer leistungsfähigen Abfragesprache abgefragt werden. Dies ist insbesondere bei der Durchführung komplexer Analysen hilfreich.

Da Azure Monitor die Datensammlung von für diese Daten ergriffenen Maßnahmen trennt, ist es unter Umständen nicht möglich, Warnungen in nahezu Echtzeit bereitzustellen. Um Warnungen zu Protokolldaten zu erhalten, werden Abfragen nach einem Wiederholungszeitplan ausgeführt, der in der Warnung definiert ist. Durch dieses Verhalten kann Azure Monitor Daten aus allen überwachten Quellen einfach korrelieren, und Sie haben die Möglichkeit, Daten auf verschiedene Weise interaktiv zu analysieren. Dies ist besonders hilfreich für die Ursachenanalyse und die Identifizierung von Bedingungen, die Probleme verursachen können.

## <a name="health-monitoring"></a>Systemüberwachung

### <a name="operations-manager"></a>Operations Manager

Management Packs in Operations Manager beinhalten ein Dienstmodell, das die Komponenten der zu überwachenden Anwendung und deren Beziehung zueinander beschreibt. Monitore bestimmen den aktuellen Integritätszustand jeder Komponente basierend auf Daten und Skripts auf dem Agent. Integritätszustände werden mithilfe von Rollups ausgeführt, sodass der zusammengefasste Integritätszustand der überwachten Computer und Anwendungen angezeigt werden kann.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor bietet keine vom Benutzer definierbare Methode zur Implementierung eines Dienstmodells oder von Monitoren, die den aktuellen Integritätszustand von Dienstkomponenten anzeigen. Da Überwachungslösungen auf den Standardfeatures von Azure Monitor basieren, ermöglichen sie keine Überwachung auf Zustandsebene. Die folgenden Features von Azure Monitor können hilfreich sein:

- **Application Insights:** Erstellt eine Verbundübersicht Ihrer Webanwendung und gibt für jede Anwendungskomponente oder Abhängigkeit einen Integritätszustand an. Dies umfasst Warnungsstatus und ein Drill-Down für eine detailliertere Diagnose der Anwendung.

- **Azure Monitor für VMs**: Ermöglicht eine Zustandsüberwachung für Azure-Gast-VMs ähnlich wie Operations Manager bei der Überwachung von virtuellen Windows- und Linux-Computern. Es bewertet die Integrität der wichtigsten Betriebssystemkomponenten hinsichtlich Verfügbarkeit und Leistung, um den aktuellen Integritätszustand zu ermitteln. Wenn festgestellt wird, dass die Gast-VM anhaltende Probleme hinsichtlich Ressourcenauslastung, Festplattenkapazität oder im Zusammenhang mit den wichtigsten Betriebssystemfunktionen aufweist, wird eine Warnung generiert, um Sie über diesen Zustand zu informieren.

- **Azure Monitor für Container**: Überwacht die Leistung und den Zustand von Azure Kubernetes Service oder Azure Container Instances. Das Feature erfasst anhand der Metrik-API die in Kubernetes verfügbaren Speicher- und Prozessormetriken von Controllern, Knoten und Containern. Es erfasst auch Containerprotokolle und Bestandsdaten über Container und ihre Images. Vordefinierte Integritätskriterien, die auf den erfassten Leistungsdaten basieren, helfen Ihnen zu erkennen, ob ein Ressourcenengpass oder ein Kapazitätsproblem vorliegt. Sie können auch die Gesamtleistung oder die Leistung eines bestimmten Kubernetes-Objekttyps (Pod, Knoten, Controller oder Container) verstehen.

## <a name="analyze-data"></a>Daten analysieren

### <a name="operations-manager"></a>Operations Manager

Operations Manager bietet vier grundlegende Möglichkeiten, Daten nach der Erfassung zu analysieren:

- **Integritäts-Explorer**: Unterstützt Sie beim Herausfinden, welche Monitore ein Problem mit dem Integritätszustand melden, und beim Überprüfen von Informationen zum Monitor und den möglichen Ursachen für damit verbundene Aktionen.

- **Ansichten**: Vordefinierte Visualisierungen der erfassten Daten, z.B. ein Diagramm der Leistungsdaten oder eine Liste der überwachten Komponenten und ihres aktuellen Integritätszustands. Diagrammansichten stellen das Dienstmodell einer Anwendung visuell dar.

- **Berichte**: Ermöglichen es Ihnen, die im Operations Manager Data Warehouse gespeicherten historischen Daten zusammenzufassen. Sie können die Daten anpassen, auf denen Sichten und Berichte basieren. Es gibt jedoch keine Funktion, mit der eine komplexe oder interaktive Analyse der gesammelten Daten möglich ist.

- **Operations Manager-Befehlsshell**: Erweitert Windows PowerShell um eine zusätzliche Reihe von Cmdlets und kann die erfassten Daten abfragen und visualisieren. Dazu zählen Diagramme und andere Visualisierungen, nativ mit PowerShell oder mit der HTML-basierten Webkonsole von Operations Manager.

### <a name="azure-monitor"></a>Azure Monitor

Mit der leistungsstarken Analyseengine von Azure Monitor können Sie interaktiv mit Protokolldaten arbeiten und diese mit anderen Überwachungsdaten für Trend- und andere Datenanalysen kombinieren. Über Ansichten und Dashboards können Sie Abfragedaten auf unterschiedliche Weise aus dem Azure-Portal visualisieren und in Power BI importieren. Überwachungslösungen umfassen Abfragen und Ansichten, um die von ihnen gesammelten Daten darzustellen. Insights wie Application Insights, Azure Monitor für VMs und Azure Monitor für Container beinhalten kundenspezifische Visualisierungen zur Unterstützung interaktiver Überwachungsszenarien.

## <a name="alerting"></a>Warnungen

### <a name="operations-manager"></a>Operations Manager

Operations Manager erstellt Warnungen als Reaktion auf vordefinierte Ereignisse, wenn ein Leistungsschwellenwert erreicht wird und wenn sich der Integritätszustand einer überwachten Komponente ändert. Damit können Warnungen vollständig verwaltet werden, sodass Sie festlegen können, wie die Warnungen aufgelöst werden sollen. Anschließend können Sie sie verschiedenen Operatoren oder System Engineers zuweisen. Sie können Benachrichtigungsregeln festlegen, die bestimmen, bei welchen Warnungen proaktive Benachrichtigungen gesendet werden sollen.

Die Management Packs enthalten verschiedene vordefinierte Warnungsregeln für verschiedene kritische Zustände in der zu überwachenden Anwendung. Sie können diese Regeln an die spezifischen Anforderungen Ihrer Umgebung anpassen oder entsprechende benutzerdefinierte Regeln erstellen.

### <a name="azure-monitor"></a>Azure Monitor

Mit Azure Monitor können Sie Warnungen für das Überschreiten eines Schwellenwerts durch eine Metrik oder auf Grundlage des Ergebnisses einer geplanten Abfrage erstellen. Auf Metriken basierende Warnungen können nahezu in Echtzeit Ergebnisse erzielen, während geplante Abfragen eine längere Antwortzeit haben, abhängig von der Geschwindigkeit der Datenerfassung und -indizierung. Mit Protokollabfragewarnungen in Azure Monitor können Sie Daten über alle in mehreren Arbeitsbereichen gespeicherten Daten hinweg analysieren, anstatt sie auf einen bestimmten Agent zu beschränken. Diese Warnungen umfassen auch Daten aus einer bestimmten Application Insights-Anwendung, indem eine arbeitsbereichsübergreifende Abfrage verwendet wird.

Überwachungslösungen beinhalten zwar Warnungsregeln, aber in der Regel erstellen Sie diese auf der Grundlage Ihrer eigenen Anforderungen.

## <a name="workflows"></a>Workflows

### <a name="operations-manager"></a>Operations Manager

Management Packs in Operations Manager enthalten Hunderte von individuellen Workflows und legen fest, welche Daten gesammelt werden und welche Aktionen mit diesen Daten durchgeführt werden müssen. So kann beispielsweise eine Regel im Abstand von wenigen Minuten einen Leistungsindikator abfragen und die Ergebnisse zur Analyse speichern. Ein Monitor könnte den gleichen Leistungsindikator abfragen und seinen Wert mit einem Schwellenwert vergleichen, um den Integritätszustand eines überwachten Objekts zu bestimmen. Eine andere Regel könnte ein Skript ausführen, um einige Daten auf einem Agent-Computer zu sammeln und zu analysieren, und eine Warnung auslösen, wenn ein bestimmter Wert zurückgegeben wird.

Die Workflows im Operations Manager sind voneinander unabhängig, sodass die Analyse über mehrere überwachte Objekte hinweg schwierig ist. In diesen Überwachungsszenarien können Daten erst nach der Sammlung verwendet werden. Das ist zwar möglich, kann aber schwierig sein und ist nicht gängig.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor trennt die Datensammlung von Aktionen und Analysen, die anhand dieser Daten durchgeführt werden. Agents und andere Datenquellen schreiben Protokolldaten in einen Log Analytics-Arbeitsbereich und Metrikdaten in die Metrikdatenbank, ohne dass eine Analyse dieser Daten durchgeführt wird oder Informationen darüber vorliegen, wie diese verwendet werden könnten. Monitor führt anhand der gespeicherten Daten Warnungen und andere Aktionen durch, sodass Sie Daten aus allen Quellen analysieren können.

## <a name="extend-the-base-platform"></a>Erweitern der Basisplattform

### <a name="operations-manager"></a>Operations Manager

Operations Manager implementiert die gesamte Überwachungslogik in einem Management Pack, das Sie entweder selbst erstellen oder von uns oder einem Partner beziehen. Wenn Sie ein Management Pack installieren, erkennt es automatisch Komponenten der Anwendung oder des Dienstes auf verschiedenen Agents und stellt geeignete Regeln und Monitore bereit. Das Management Pack enthält Integritätsdefinitionen, Warnungsregeln, Regeln für die Leistungs- und Ereigniserfassung sowie Ansichten, um eine vollständige Überwachung zu ermöglichen, die den Infrastrukturdienst oder die Anwendung unterstützt.

Das Operations Manager SDK ermöglicht es Operations Manager, sich in Überwachungsplattformen von Drittanbietern oder in ITSM-Software (IT Service Management) zu integrieren. Das SDK wird auch von einigen Management Packs von Partnern verwendet, um die Überwachung von Netzwerkgeräten zu unterstützen und benutzerdefinierte Präsentationserfahrungen wie das Squared Up HTML5-Dashboard oder Integration in Microsoft Office Visio bereitzustellen.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor sammelt Metriken und Protokolle von Azure-Ressourcen mit wenig bis gar keiner Konfiguration. Überwachungslösungen fügen Logik für die Überwachung einer Anwendung oder eines Diensts hinzu, arbeiten aber weiterhin innerhalb der Standardprotokollabfragen und Ansichten in Monitor. Analyseanwendungen wie Application Insights und Azure Monitor für VMs nutzen die Monitor-Plattform zur Datensammlung und -verarbeitung. Außerdem bieten Sie zusätzliche Tools für die Visualisierung und Analyse der Daten. Mithilfe der wichtigsten Funktionen von Monitor, z. B. Protokollabfragen und Warnungen, können Sie die von Insights gesammelten Daten mit anderen Daten kombinieren.

Monitor unterstützt mehrere Methoden, um Überwachungs- oder Verwaltungsdaten von Azure oder externen Ressourcen zu sammeln. Sie können dann Daten aus den Metrik- oder Protokollspeichern extrahieren und an Ihre ITSM- oder Überwachungstools weiterleiten. Sie können auch administrative Aufgaben mithilfe der Azure Monitor-Rest-API ausführen.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Überwachungsstrategie für Cloudbereitstellungsmodelle](./cloud-models-monitor-overview.md)
