---
title: Leitfaden zur Cloudüberwachung – Überwachungsstrategie für Cloudbereitstellungsmodelle
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Auswahlhilfe: Verwendung von Azure Monitor oder System Center Operations Manager in Microsoft Azure'
author: MGoedtel
ms.author: magoedte
ms.date: 10/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 5988cbb16e47a603af85eac97078b7dc0a00e295
ms.sourcegitcommit: d37c4443e9acaa381ea74ee3fc50e3b99f13f22a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "72001886"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Leitfaden zur Cloudüberwachung: Überwachungsstrategie für Cloudbereitstellungsmodelle

Dieser Artikel enthält unsere empfohlene Überwachungsstrategie für jedes der Cloud-Bereitstellungsmodelle, basierend auf den folgenden Kriterien:

- Sie müssen weiterhin Operations Manager oder eine andere Unternehmensüberwachungsplattform nutzen, weil diese in Ihre IT-Betriebsabläufe integriert sind, Sie viel Wissen und Know-how darin investiert haben sind oder bestimmte Funktionen in Azure Monitor noch nicht verfügbar sind.
- Sie müssen Workloads sowohl lokal als auch in der öffentlichen Cloud oder nur in der Cloud überwachen.
- Ihre Cloudmigrationsstrategie umfasst die Modernisierung von IT-Abläufen und den Wechsel zu unseren Diensten und Lösungen für die Cloudüberwachung.
- Möglicherweise verfügen Sie über kritische Systeme, die per Air Gap oder physisch voneinander isoliert sind, in einer privaten Cloud oder auf physischer Hardware gehostet werden und überwacht werden müssen.

Unsere Strategie umfasst die Unterstützung von Überwachungsinfrastruktur (Rechen-, Speicher- und Serverworkloads), Anwendungen (Endbenutzer, Ausnahmen und Clients) und Netzwerkressourcen, um eine vollständige dienstorientierte Überwachungsperspektive zu bieten.

## <a name="azure-cloud-monitoring"></a>Azure-Cloudüberwachung

Azure Monitor ist der native Plattformdienst, mit dem Sie Ihre Azure-Ressourcen an einem zentralen Ort verwalten können. Der Dienst ist für Cloudlösungen konzipiert, die auf Azure basieren und eine Geschäftsfunktion unterstützen, die auf VM-Workloads oder komplexen Architekturen basiert, in denen Microservices und andere Plattformressourcen verwendet werden. Er überwacht alle Ebenen des Stapels, beispielsweise Mandantendienste wie Azure Active Directory Domain Services, sowie Ereignisse auf Abonnementebene und Azure Service Health. Außerdem überwacht er Infrastrukturressourcen wie virtuelle Computer, Speicher- und Netzwerkressourcen sowie Ihre Anwendung auf der obersten Ebene. Durch die Überwachung jeder dieser Abhängigkeiten und das Erfassen der richtigen Signale, die jede dieser Abhängigkeiten ausgeben kann, können Sie sicherstellen, dass die Anwendungen und die wichtigsten Infrastrukturkomponenten überwacht werden können.

In der folgenden Tabelle sind die empfohlenen Ansätze zur Überwachung der einzelnen Ebenen des Stapels zusammengefasst.

<!-- markdownlint-disable MD033 -->

Ebene | Resource | `Scope` | Methode
---|---|---|----
Anwendung | Webbasierte Anwendung, die auf der .NET-, .NET Core-, Java-, JavaScript- und Node.js-Plattform auf einem virtuellen Azure-Computer, bei Azure App Services, Azure Service Fabric, Azure Functions und Azure Cloud Services ausgeführt wird | Überwachen einer Livewebanwendung, um automatisch Leistungsanomalien zu erkennen, Codeausnahmen und -probleme zu erkennen und Analysedaten zum Benutzerverhalten zu erfassen. |  Azure Monitor (Application Insights)
Azure-Ressourcen – PaaS | 1. Azure-Datenbankdienste (z. B. SQL oder MySQL) | 1. Azure-Datenbank für SQL-Leistungsmetriken. | 1. Aktivieren der Diagnoseprotokollierung zum Streamen von SQL-Daten an Azure Monitor-Protokolle.
Azure-Ressourcen – IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. Netzwerksicherheitsgruppen<br/> 4. Azure Traffic Manager<br/> 5. Virtual Machine<br/> 6. Azure Kubernetes Service/Azure Container Instances | 1. Kapazität, Verfügbarkeit und Leistung.<br/> 2. Leistungs- und Diagnoseprotokolle (Aktivitäten, Zugriff, Leistung und Firewall)<br/> 3. Überwachung von Ereignissen bei der Anwendung von Regeln und Regelzähler für die Häufigkeit der Anwendung von Regeln zum Ablehnen oder Zulassen<br/> 4. Überwachung der Verfügbarkeit des Endpunktstatus.<br/> 5. Überwachung von Kapazität, Verfügbarkeit und Leistung in VM-Gastbetriebssystemen. Zuordnung von auf den virtuellen Computern gehosteten App-Abhängigkeiten, einschließlich der Sichtbarkeit aktiver Netzwerkverbindungen zwischen Servern, der Latenz für eingehende und ausgehende Verbindungen und der Ports in jeder über TCP verbundenen Architektur.<br/> 6. Überwachung von Kapazität, Verfügbarkeit und Leistung von Workloads, die auf Containern und Containerinstanzen ausgeführt werden. | 1. Speichermetriken für Blob Storage<br/> 2. Aktivieren der Diagnoseprotokollierung Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle.<br/> 3. Aktivieren der Diagnoseprotokollierung von Netzwerksicherheitsgruppen und Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle<br/> 4. Aktivieren der Diagnoseprotokollierung von Traffic Manager-Endpunkten und Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle<br/> 5. Aktivieren von Azure Monitor für VMs<br/> 6. Aktivieren von Azure Monitor für Container
Netzwerk| Kommunikation zwischen dem virtuellen Computer und einem oder mehreren Endpunkten (ein anderer virtueller Computer, ein vollqualifizierter Domänenname, ein URI oder eine IPv4-Adresse). | Überwachung von Änderungen der Erreichbarkeit, Latenz und Netzwerktopologie zwischen der VM und dem Endpunkt. | Azure Network Watcher
Azure-Abonnement | Azure Service Health und grundlegende Dienstintegrität | <li> Für einen Dienst oder eine Ressource durchgeführte Verwaltungsmaßnahmen.<br/><li> Die Dienstintegrität eines Azure-Diensts hat sich verschlechtert, oder er ist nicht verfügbar.<br/><li> Bei einer Azure-Ressource vom Azure-Dienst erkannte Integritätsprobleme.<br/><li> Mit der Azure-Autoskalierung durchgeführte Vorgänge zeigen einen Fehler oder eine Ausnahme an. <br/><li> Mit Azure Policy durchgeführte Vorgänge zeigen an, dass eine zulässige oder abgelehnte Aktion ausgeführt wurde.<br/><li> Datensatz der in Azure Security Center generierten Warnungen. |Im Aktivitätsprotokoll für Überwachung und Warnungen unter Verwendung von Azure Resource Manager bereitgestellt.
Azure-Mandant|Azure Active Directory || Aktivieren der Diagnoseprotokollierung und Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Überwachen der Hybrid Cloud

In vielen Organisationen muss die Cloud schrittweise eingeführt werden, und das Hybrid Cloud-Modell ist der häufigste erste Schritt in diesem Projekt. Sie wählen sorgfältig die geeigneten Anwendungen und Infrastrukturkomponenten aus, um mit der Migration zu beginnen, ohne die Geschäftsabläufe zu unterbrechen. Viele IT-Entscheidungsträger sind jedoch verwirrt, weil wir zwei Überwachungsplattformen anbieten, die dieses Cloudmodell unterstützen – sie sind nicht sicher, welche zur Unterstützung ihrer Ziele hinsichtlich der Geschäfts- und IT-Ziele am besten geeignet ist. Wir werden im Folgenden einige Faktoren untersuchen, um diese Unsicherheit zu beseitigen, und Ihnen wichtige Informationen zu den Plattformen zur Verfügung stellen, sodass Sie entscheiden können, welche Plattform Sie einsetzen sollten.

Folgende wichtige technische Aspekte müssen berücksichtigt werden:

* Sie möchten Daten von Azure-Ressourcen sammeln, die die Workload unterstützen, und diese Daten an Ihre vorhandenen lokalen Tools oder Managed Service Provider-Tools weiterleiten.

* Sie müssen Ihre aktuellen Investitionen in System Center Operations Manager weiter nutzen und das System zur Überwachung von IaaS- und PaaS-Ressourcen konfigurieren, die in Azure ausgeführt werden. Optional (da Sie basierend auf Ihren Anforderungen zwei Umgebungen mit unterschiedlichen Eigenschaften überwachen) bestimmen Sie, ob die Integration mit Azure Monitor Ihre Strategie unterstützt.

* Im Rahmen Ihrer Modernisierungsstrategie, mit der Sie Abläufe in einem einzigen Tool standardisieren möchten, um Kosten und Komplexität zu reduzieren, verwenden Sie Azure Monitor zur Überwachung der Ressourcen in Azure und in Ihrem Unternehmensnetzwerk.

In der folgenden Tabelle werden die Anforderungen zusammengefasst, die für Azure Monitor und System Center Operations Manager bei der Überwachung des Hybrid Cloud-Modells basierend auf einem gemeinsamen Satz von Kriterien gelten.

|Anforderung | Azure Monitor | Operations Manager |
|:--|:---|:---|
|Infrastrukturanforderungen | **Nein** | **Ja**<br> Erfordert mindestens einen Verwaltungsserver sowie eine SQL Server-Instanz, um die operative Datenbank und die Reporting-Data Warehouse-Datenbank zu hosten. Wird komplexer, wenn Hochverfügbarkeit und Notfallwiederherstellung erforderlich sind oder Computer in mehreren Standorten, nicht vertrauenswürdige Systeme sowie weitere komplexe Entwurfsüberlegungen ins Spiel kommen.|
|Eingeschränkte Konnektivität: kein Internet<br> oder isoliertes Netzwerk | **Nein** | **Ja** | 
|Eingeschränkte Konnektivität: kontrollierter Internetzugang | **Ja** | **Ja** |
|Eingeschränkte Konnektivität: häufige Unterbrechungen | **Ja** | **Ja** |
|Konfigurierbare Integritätsüberwachung | **Nein** | **Ja** |
| Web-App-Verfügbarkeitstest (isoliertes Netzwerk) | **Ja, eingeschränkt**<br> Azure Monitor bietet eingeschränkte Unterstützung in diesem Bereich und erfordert benutzerdefinierte Firewallausnahmen. | **Ja** | 
| Web-App-Verfügbarkeitstest (global verteilt) | **Nein** | **Ja** |
|Überwachen von VM-Workloads | **Ja, eingeschränkt**<br> Kann IIS- und SQL Server-Fehlerprotokolle, Windows-Ereignisse und Leistungsindikatoren erfassen. Erfordert die Erstellung benutzerdefinierter Abfragen, Warnungen und Visualisierungen. | **Ja**<br> Unterstützt die Überwachung der meisten Serverworkloads mit verfügbaren Management Packs. Erfordert entweder den Windows-Agent von Log Analytics oder den Operations Manager-Agent auf der VM und die Rückmeldung an die Verwaltungsgruppe im Unternehmensnetzwerk.|
|Überwachen von Azure-IaaS | **Ja** | **Ja**<br> Unterstützt die Überwachung der meisten Infrastrukturkomponenten im Unternehmensnetzwerk. Verfolgt Verfügbarkeitsstatus, Metriken und Warnungen für virtuelle Azure-Computer, SQL und Speicher über das Azure-Management Pack.|
|Überwachen von Azure-PaaS | **Ja** | **Ja, eingeschränkt**<br> Richtet sich danach, was im Azure Management Pack unterstützt wird. | 
|Überwachen des Azure-Diensts | **Ja**<br> | **Ja**<br> Management Packs bieten zwar derzeit keine native Überwachung der Integrität des Azure-Diensts, Sie können aber benutzerdefinierte Workflows erstellen, um Integritätswarnungen zum Azure-Dienst abzufragen. Verwenden Sie die Azure-REST-API, um Warnungen über Ihr vorhandenes Benachrichtigungssystem zu erhalten.|
|Moderne Webanwendungsüberwachung | **Ja** | **Nein** |
|Legacy-Webanwendungsüberwachung | **Ja, eingeschränkt je nach SDK**<br> Unterstützt die Überwachung älterer Versionen von .NET- und Java-Webanwendungen. | **Ja, eingeschränkt** |
|Überwachen von Azure Kubernetes Service-Containern | **Ja** | **Nein** |
|Überwachen von Docker-/Windows-Containern | **Ja** | **Nein** | 
|Überwachung der Netzwerkleistung | **Ja** | **Ja, eingeschränkt**<br> Unterstützt Verfügbarkeitsprüfungen und sammelt grundlegende Statistiken von Netzwerkgeräten mithilfe des SNMP-Protokolls aus dem Unternehmensnetzwerk.|
|Interaktive Datenanalyse | **Ja** | **Nein**<br> Basiert auf vordefinierten oder benutzerdefinierten Berichten von SQL Server Reporting Services, Visualisierungslösungen von Drittanbietern oder benutzerdefinierten Power BI-Implementierungen. Für das Operations Manager-Data Warehouse gibt es Skalierungs- und Leistungseinschränkungen. Integration mit Azure Monitor-Protokollen als Alternative für die Anforderungen der Datenaggregation. Die Integration erfolgt durch die Konfiguration des Log Analytics-Connectors.| 
|End-to-End-Diagnose, Analyse der Grundursache und rechtzeitige Problembehandlung | **Ja** | **Ja, eingeschränkt**<br> Unterstützt die End-to-End-Diagnose und Problembehandlung nur für lokale Infrastrukturen und Anwendungen. Verwendet andere System Center-Komponenten oder Partnerlösungen.|
|Interaktive Visualisierungen (Dashboards) | **Ja** | **Ja, eingeschränkt**<br> Stellt grundlegende Dashboards über die HTLM5-Webkonsole oder über eine erweiterte Benutzeroberfläche von Partnerlösungen wie Squared Up oder Savision bereit. |
|Integration in IT- oder DevOps-Tools | **Ja** | **Ja, eingeschränkt** |

### <a name="collect-and-stream-monitoring-data-to-third-party-or-on-premises-tools"></a>Sammeln und Streamen von Überwachungsdaten an Tools von Drittanbietern oder lokale Tools

Um Metriken und Protokolle von Azure-Infrastruktur- und Plattformressourcen zu sammeln, müssen Sie die Azure-Diagnoseprotokolle für diese Ressourcen aktivieren. Darüber hinaus können Sie mit Azure-VMs Metriken und Protokolle vom Gastbetriebssystem sammeln, indem Sie die Erweiterung der Azure-Diagnose aktivieren. Um die von Ihren Azure-Ressourcen ausgegebenen Diagnosedaten an Ihre lokalen Tools oder Ihren Anbieter von verwalteten Diensten weiterzuleiten, konfigurieren Sie [Event Hubs](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-stream-event-hubs) so, dass die Daten an diese Ziele gestreamt werden. 

### <a name="monitor-with-system-center-operations-manager"></a>Überwachung mit System Center Operations Manager

System Center Operations Manager war ursprünglich als lokale Lösung für die Überwachung von Anwendungen, Workloads und Infrastrukturkomponenten in einer IT-Umgebung konzipiert, wurde dann mit Funktionen für die Cloudüberwachung weiterentwickelt und lässt sich heute in Azure, Office 365 und Amazon Web Services (AWS) integrieren. Das System kann diese unterschiedlichen Umgebungen mit dafür konzipierten und aktualisierten Management Packs überwachen.  

Sowohl Kunden, die beträchtliche Investitionen in Operations Manager getätigt haben, um eine umfassende, eng in ihre IT-Service-Management-Prozesse und -Tools integrierte Überwachung zu erzielen, als auch Kunden, die gerade erst mit der Nutzung von Azure beginnen, fragen sich verständlicherweise Folgendes:

* Kann Operations Manager weiterhin einen Mehrwert bieten und ist es aus geschäftlicher Sicht sinnvoll?

* Sind die Features von Operations Manager für unsere IT-Organisation geeignet?

* Lässt sich durch die Integration von Operations Manager in Azure Monitor die kostengünstige und umfassende Überwachungslösung erzielen, die wir benötigen? 

Wenn Sie bereits in Operations Manager investiert haben, müssen Sie sich nicht auf die Planung einer Migration konzentrieren, um das System sofort auszutauschen. Mit Azure oder anderen Cloudanbietern, die als Erweiterung Ihres eigenen lokalen Netzwerks fungieren, kann Operations Manager die Gast-VMs und Azure-Ressourcen so überwachen, als befänden diese sich in Ihrem Unternehmensnetzwerk. Dafür ist eine zuverlässige Netzwerkverbindung zwischen Ihrem Netzwerk und dem virtuellen Azure-Netzwerk erforderlich, die genügend Bandbreite bietet. 

Um die in Azure ausgeführten Workloads zu überwachen, benötigen Sie Folgendes:

* Das [Azure-Management Pack](https://www.microsoft.com/download/details.aspx?id=50013), um die Leistungsmetriken zu erfassen, die von Azure-Diensten wie Web- und Workerrollen, Application Insights-Verfügbarkeitstests (Webtests), Service Bus usw. ausgegeben werden. Das Management Pack nutzt die Azure-REST-API, um die Verfügbarkeit und Leistung dieser Ressourcen zu überwachen. Für einige Arten von Azure-Diensten sind im Azure-Management Pack keine Metriken oder vordefinierte Monitore vorhanden, diese Dienste können aber über die im Management Pack für ermittelte Dienste definierten Beziehungen dennoch überwacht werden.

* Das [Management Pack für Azure SQL-Datenbank](https://www.microsoft.com/download/details.aspx?id=38829) zum Überwachen der Verfügbarkeit und Leistung von Azure SQL-Datenbanken und Azure SQL-Datenbankservern mithilfe der Azure-REST-API und T-SQL-Abfragen in SQL Server-Systemsichten.

* Um das Gastbetriebssystem und die auf der VM ausgeführten Workloads wie SQL Server, IIS oder Apache Tomcat zu überwachen, müssen Sie das Management Pack herunterladen und importieren, das die Anwendung, den Dienst und das Betriebssystem unterstützt.

Im Management Pack wird definiert, wie die einzelnen Abhängigkeiten und Komponenten überwacht werden. Für beide Azure-Management Packs müssen einige Konfigurationsschritte in Azure und Operations Manager ausgeführt werden, damit mit der Überwachung dieser Ressourcen begonnen werden kann. 

Auf Anwendungsebene bietet Operations Manager grundlegende Funktionen zur Überwachung der Anwendungsleistung für einige ältere Versionen von .NET und Java. Wenn bestimmte Anwendungen innerhalb Ihrer Hybrid Cloud-Umgebung offline oder vom Netzwerk isoliert ausgeführt werden, sodass sie nicht mit einem öffentlichen Clouddienst kommunizieren können, ist die Application Performance Monitoring-Komponente (APM) von Operations Manager in einigen Szenarien möglicherweise eine gangbare Option. Verwenden Sie Azure Monitor Application Insights für nicht auf Legacyplattformen ausgeführte Anwendungen. Diese können lokal oder in einer öffentlichen Cloud gehostet werden, die die Kommunikation mit Azure über eine Firewall ermöglicht. Dies ermöglicht eine detaillierte Überwachung auf Codeebene mit erstklassiger Unterstützung für ASP.NET, ASP.NET Core, Java, JavaScript und Node.js.

Sie sollten für jede Webanwendung, auf die von einer externen Seite aus zugegriffen werden kann, eine Art synthetischer Transaktion aktivieren, die als [Verfügbarkeitsüberwachung]( https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability) bezeichnet wird. Es ist wichtig zu wissen, ob Ihre Anwendung oder ein kritischer HTTP/HTTPS-Endpunkt, auf den sich die Anwendung stützt, verfügbar und reaktionsfähig ist. Mit der Verfügbarkeitsüberwachung von Application Insights können Sie die Tests in mehreren Azure-Rechenzentren durchführen und erhalten so einen Einblick in die Integrität Ihrer Anwendung aus globaler Perspektive.

Operations Manager kann zwar in Azure gehostete Ressourcen überwachen, aber Azure Monitor bietet einige Vorteile, da die Stärken von Azure Monitor die Beschränkungen von Operations Manager aufheben und eine stabile Grundlage für die Unterstützung der Migration von Operations Manager bilden. Im Folgenden beleuchten wir diese Vorteile im Einzelnen und bieten Empfehlungen für die Integration von Azure Monitor in die Überwachungsstrategie für Ihre Hybridumgebung.  

#### <a name="disadvantage-of-using-operations-manager-by-itself"></a>Nachteile der alleinigen Nutzung von Operations Manager

1. Überwachungsdaten werden in Operations Manager im Allgemeinen mithilfe von Ansichten analysiert. Diese sind in Management Packs vordefiniert, auf die über die Konsole, von SQL Server Reporting Services-Berichten (SSRS) oder aus von Endbenutzern definierten Ansichten heraus zugegriffen werden kann. Eine Ad-hoc-Analyse der Daten ist standardmäßig nicht möglich. Die Berichterstellung von Operations Manager ist nicht flexibel, und das Data Warehouse, das für die Langzeitaufbewahrung der Überwachungsdaten sorgt, ist nicht besonders skalierungs- oder leistungsfähig. Außerdem sind Kenntnisse im Schreiben von T-SQL-Anweisungen, Entwickeln einer Power BI-Lösung oder Verwenden von Drittanbieterlösungen notwendig, um die Anforderungen für die verschiedenen Personas in der IT-Organisation zu unterstützen. 

2. Warnungen in Operations Manager bieten keine Unterstützung für komplexe Ausdrücke, enthalten aber Korrelationslogik, um unnötige Warnungen und Gruppenwarnungen zu reduzieren und deren Beziehung zueinander anzuzeigen, damit die Grundursache eines Problems ermittelt werden kann. 

#### <a name="advantage-of-operations-manager--azure-monitor"></a>Vorteile von Operations Manager und Azure Monitor

1. Azure Monitor-Protokolle heben die Einschränkungen von Operations Manager auf und ergänzen die Data Warehouse-Datenbank von Operations Manager, sodass wichtige Leistungs- und Protokolldaten erfasst werden können. Azure Monitor ermöglicht eine bessere Analyse, bietet mehr Leistung bei der Abfrage großer Datenmengen sowie eine bessere Aufbewahrung als die Data Warehouse-Datenbank von Operations Manager. Mit der zugehörigen Abfragesprache können Sie wesentlich komplexere und anspruchsvollere Abfragen erstellen, und Sie können Abfragen für mehrere Terabyte an Daten innerhalb weniger Sekunden ausführen. Außerdem können Sie die Daten schnell in Kreisdiagramme, Zeitdiagramme und viele andere Visualisierungen umwandeln. Sie müssen in Operations Manager nicht mehr mit Berichten arbeiten, die auf SQL Server Reporting Services, benutzerdefinierten SQL-Abfragen oder anderen Workarounds zur Analyse dieser Daten basieren.

2. Sorgen Sie für verbesserte Warnungen, indem Sie die Warnungsverwaltungslösung von Azure Monitor implementieren. In der Operations Manager-Verwaltungsgruppe generierte Warnungen können an den Log Analytics-Arbeitsbereich in Azure Monitor weitergeleitet werden. Sie können das Abonnement, das für die Weiterleitung von Warnungen von Operations Manager an die Azure Monitor-Protokolle genutzt wird, so konfigurieren, dass nur bestimmte Warnungen weitergeleitet werden. Beispielsweise können Sie nur Warnungen weiterleiten, die Ihren Kriterien für die Abfrage entsprechen, um so die Problemverwaltung für Trends und die Untersuchung der Grundursache von Ausfällen oder Problemen über eine zentrale Konsole zu steuern. Darüber hinaus können Sie andere Protokolldaten aus Application Insights oder anderen Quellen korrelieren, um Erkenntnisse zu gewinnen, auf deren Basis Sie die Benutzerfreundlichkeit verbessern, die Betriebszeit erhöhen und die Zeit zur Behebung von Incidents verkürzen können.

3. Überwachen Sie die cloudnative Infrastruktur und die cloudnativen Anwendungen über eine einfache oder mehrschichtige Architektur in Azure, und verwenden Sie Operations Manager zum Überwachen der lokalen Infrastruktur. Dies umfasst eine oder mehrere VMs, mehrere VMs in einer Verfügbarkeitsgruppe oder VM-Skalierungsgruppe oder eine containerbasierte Anwendung, die in einer in Windows Server- oder Linux-Containern ausgeführten AKS-Instanz (Azure Kubernetes Service) bereitgestellt ist.

4. Verwenden Sie die System Center Operations Manager-Integritätsprüfungslösung, um die Risiken und die Integrität Ihrer System Center Operations Manager-Verwaltungsgruppe in regelmäßigen Abständen proaktiv zu bewerten. Damit können Sie alle benutzerdefinierten Funktionen, die Sie Ihrer Verwaltungsgruppe hinzugefügt haben, ersetzen oder ergänzen.

5. Zusammen mit dem Zuordnungsfeature von Azure Monitor für VMs können Sie auf diese Weise standardmäßige Konnektivitätsmetriken von Netzwerkverbindungen zwischen Ihren Azure-VMs und lokalen VMs überwachen. Diese Metriken beinhalten die Antwortzeit, die Anforderungen pro Minute, den Datenverkehrsdurchsatz und Links. Sie können Verbindungsfehler identifizieren, Problembehandlungen, Überprüfungen der Migration und Sicherheitsanalysen durchführen und die allgemeine Architektur des Diensts überprüfen. Mit der Zuordnungsfunktion können Anwendungskomponenten in Windows- und Linux-Systemen automatisch erkannt und die Kommunikation zwischen Diensten zugeordnet werden. Dadurch können Sie bisher unbekannte Verbindungen und Abhängigkeiten ermitteln, die Migration zu Azure planen und überprüfen sowie unsichere Aspekte bei der Behebung von Vorfällen minimieren.

6. Überwachen Sie mit dem Netzwerkleistungsmonitor die Netzwerkverbindung zwischen folgenden Elementen:

   - Ihrem Unternehmensnetzwerk und Azure

   - Unternehmenskritische Anwendungen mit mehreren Ebenen und Microservices

   - Benutzerstandorten und webbasierten Anwendungen (HTTP/HTTPS)

   Diese Strategie bietet Einblicke in die Netzwerkschicht, ohne dass SNMP erforderlich ist. Außerdem kann die Hop-by-Hop-Topologie von Routen zwischen dem Quell- und dem Zielendpunkt auf einer interaktiven Topologiekarte dargestellt werden. Diese Vorgehensweise ist besser als der Versuch, das gleiche Ergebnis mit der Netzwerküberwachung in Operations Manager oder anderen derzeit in Ihrer Umgebung verwendeten Netzwerküberwachungstools zu erzielen.

### <a name="monitor-with-azure-monitor"></a>Überwachung mit Azure Monitor

Eine Migration zur Cloud stellt Sie zwar vor einige Herausforderungen, bietet aber auch eine Vielzahl neuer Möglichkeiten. Durch die Migration von einem oder mehreren lokalen Tools für die unternehmensweite Überwachung kann Ihre Organisation nicht nur Kapital- und Betriebskosten senken, sondern auch von den Vorteilen profitieren, die eine Cloudüberwachungsplattform wie Azure Monitor für die Cloud bietet. Überprüfen Sie Ihre Überwachungs- und Warnungsanforderungen, die Konfiguration vorhandener Überwachungstools und die mögliche Verlagerung von Workloads in die Cloud, und konfigurieren Sie Azure Monitor, sobald Ihr Plan fertig ist. 

- Überwachen Sie die hybride Infrastruktur und die hybriden Anwendungen über eine einfache oder mehrschichtige Architektur, in der Komponenten von Azure, anderen Cloudanbietern und Ihrem Unternehmensnetzwerk gehostet werden. Dies umfasst eine oder mehrere VMs, mehrere VMs in einer Verfügbarkeitsgruppe oder VM-Skalierungsgruppe oder eine containerbasierte Anwendung, die in einer in Windows Server- oder Linux-Containern ausgeführten AKS-Instanz (Azure Kubernetes Service) bereitgestellt ist. 

- Aktivieren Sie Azure Monitor für VMs und Container sowie Application Insights, um Probleme zwischen Infrastruktur und Anwendungen zu erkennen und zu diagnostizieren. Um eine genauere Analyse und Korrelation der Daten durchzuführen, die von den die Anwendung unterstützenden Komponenten oder Abhängigkeiten gesammelt werden, müssen Sie Azure Monitor-Protokolle verwenden.

- Erstellen Sie intelligente Warnungen, die auf wichtige Anwendungen und Dienstkomponenten angewendet werden können, reduzieren Sie unnötige Warnungen mit dynamischen Schwellenwerten für komplexe Signale, und nutzen Sie eine auf Machine Learning-Algorithmen basierende Warnungsaggregierung, um Probleme schnell zu identifizieren.

 - Definieren Sie eine Bibliothek mit Abfragen sowie Dashboards, um die Anforderungen der verschiedenen Personas in der IT-Organisation zu unterstützen.

- Definieren Sie Standards und Methoden für die Überwachung zwischen den Hybrid- und Cloudressourcen, eine Überwachungsbaseline für jede Ressource, Warnungsschwellenwerte usw.  

- Konfigurieren Sie die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC), um Benutzern und Gruppen nur den Zugriff zu gewähren, den sie zum Arbeiten mit Überwachungsdaten aus Ressourcen benötigen, für deren Verwaltung sie zuständig sind. 

- Schließen Sie Automatisierungs- und Self-Service-Funktionen ein, sodass jedes Team selbst Überwachungs- und Warnungskonfigurationen nach Bedarf erstellen, optimieren und aktivieren kann. 

## <a name="private-cloud-monitoring"></a>Überwachen der privaten Cloud

Durch Verwendung von System Center Operations Manager wird eine ganzheitliche Überwachung von Azure Stack ermöglicht. Insbesondere können Sie die Workloads überwachen, die im Mandanten, auf Ressourcenebene, auf den virtuellen Computern und in der Infrastruktur ausgeführt werden, die Azure Stack (physische Server und Netzwerkswitches) hostet. Eine ganzheitliche Überwachung ist außerdem durch eine Kombination der in Azure Stack enthaltenen [Funktionen zur Infrastrukturüberwachung](/azure/azure-stack/azure-stack-monitor-health) möglich. Mithilfe dieser Funktionen können Sie die Integrität und Warnungen für eine Azure Stack-Region und den [Azure Monitor-Dienst](/azure/azure-stack/user/azure-stack-metrics-azure-data) in Azure Stack anzeigen. Dort werden für die meisten Dienste grundlegende Infrastrukturmetriken und Protokolle bereitgestellt.

Wenn Sie bereits in Operations Manager investiert haben, sollten Sie die Verfügbarkeit und den Integritätszustand von Azure Stack-Bereitstellungen mit dem Management Pack von Azure Stack überwachen. Dies umfasst Regionen, Ressourcenanbieter, Updates, Aktualisierungsläufe, Skalierungseinheiten, Einheitsknoten, Infrastrukturrollen und deren Instanzen (logische Einheiten bestehend aus den Hardwareressourcen). Das Management Pack verwendet die REST-APIs des Integritäts- und des Updateressourcenanbieters, um mit Azure Stack zu kommunizieren. Die physischen Server und Speichergeräte können Sie mit den Management Packs der OEM-Anbieter (z. B. von Lenovo, Hewlett Packard oder Dell) überwachen. Operations Manager kann über das SNMP-Protokoll die Netzwerkswitches nativ überwachen, um grundlegende Statistiken zu sammeln. Die Überwachung der Workloads des Mandanten ist mit dem Azure-Management Pack durch Ausführung zweier grundlegender Schritte möglich. Konfigurieren Sie zunächst das Abonnement, das überwacht werden soll, und fügen Sie dann die Monitore für dieses Abonnement hinzu.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Erfassen der richtigen Daten](./data-collection.md)
