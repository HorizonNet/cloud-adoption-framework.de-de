---
title: Leitfaden zur Cloudüberwachung – Überwachungsstrategie für Cloudbereitstellungsmodelle
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Auswahlhilfe: Verwendung von Azure Monitor oder System Center Operations Manager in Microsoft Azure'
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: badf03f3616de8e6612221282aa24996f0b6e8f8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221129"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Leitfaden zur Cloudüberwachung: Überwachungsstrategie für Cloudbereitstellungsmodelle

Dieser Artikel enthält unsere empfohlene Überwachungsstrategie für jedes der Cloud-Bereitstellungsmodelle, basierend auf den folgenden Kriterien:

- Sie müssen Operations Manager oder eine andere Unternehmensüberwachungsplattform kontinuierlich nutzen. Dies ist auf die Integration in Ihre IT-Betriebsabläufe, Ihr Wissen und Ihr Know-how zurückzuführen oder darauf, dass bestimmte Funktionen in Azure Monitor noch nicht verfügbar sind.
- Sie müssen Workloads sowohl lokal als auch in der öffentlichen Cloud oder nur in der Cloud überwachen.
- Ihre Cloudmigrationsstrategie umfasst die Modernisierung von IT-Abläufen und den Wechsel zu unseren Diensten und Lösungen für die Cloudüberwachung.
- Möglicherweise verfügen Sie über kritische Systeme, die per Air Gap oder physisch voneinander isoliert sind, in einer privaten Cloud oder auf physischer Hardware gehostet werden und überwacht werden müssen.

Unsere Strategie umfasst die Unterstützung von Überwachungsinfrastruktur (Rechen-, Speicher- und Serverworkloads), Anwendungen (Endbenutzer, Ausnahmen und Clients) und Netzwerkressourcen, um eine vollständige dienstorientierte Überwachungsperspektive zu bieten.

## <a name="azure-cloud-monitoring"></a>Azure-Cloudüberwachung

Azure Monitor ist der Plattformdienst, mit dem Sie Ihre Azure-Ressourcen an einem zentralen Ort verwalten können. Der Dienst ist für Cloudlösungen konzipiert, die auf Azure basieren und eine Geschäftsfunktion unterstützen, die auf VM-Workloads oder komplexen Architekturen basiert, in denen Microservices und andere Plattformressourcen verwendet werden. Er überwacht alle Ebenen des Stapels, beispielsweise Mandantendienste wie Azure Active Directory Domain Services, sowie Ereignisse auf Abonnementebene und Azure Service Health. Außerdem überwacht er Infrastrukturressourcen wie virtuelle Computer, Speicher- und Netzwerkressourcen sowie Ihre Anwendung auf der obersten Ebene. Durch die Überwachung jeder dieser Abhängigkeiten und das Erfassen der richtigen Signale, die jede dieser Abhängigkeiten ausgeben kann, können Sie sicherstellen, dass die Anwendungen und die wichtigsten Infrastrukturkomponenten überwacht werden können.

In der folgenden Tabelle sind die empfohlenen Ansätze zur Überwachung der einzelnen Ebenen des Stapels zusammengefasst.

<!-- markdownlint-disable MD033 -->

Ebene | Resource | `Scope` | Methode
---|---|---|----
Anwendung | Webbasierte Anwendung, die auf der .NET-, .NET Core-, Java-, JavaScript- und Node.js-Plattform auf einem virtuellen Azure-Computer, bei Azure App Services, Azure Service Fabric, Azure Functions und Azure Cloud Services ausgeführt wird | Überwachung einer Live-Webanwendung zur automatischen Erkennung von Leistungsanomalien, zur Ermittlung von Codeausnahmen und -problemen und zur Erfassung von Telemetriedaten zur Benutzerfreundlichkeit. |  Application Insights
Container | Azure Kubernetes Service/Azure Container Instances | Überwachung von Kapazität, Verfügbarkeit und Leistung von Workloads, die auf Containern und Containerinstanzen ausgeführt werden. | Azure Monitor für Container
Gastbetriebssystem | Linux und Windows-VM-Betriebssystem | Überwachung von Kapazität, Verfügbarkeit und Leistung. Zuordnung der auf den virtuellen Computern gehosteten Abhängigkeiten, einschließlich der Sichtbarkeit aktiver Netzwerkverbindungen zwischen Servern, der Wartezeiten für eingehende und ausgehende Verbindungen und der Ports in jeder TCP-verbundenen Architektur. | Azure Monitor für VMs
Azure-Ressourcen – PaaS | Azure-Datenbankdienste (z. B. SQL oder MySQL) | Azure-Datenbank für SQL-Leistungsmetriken. | Aktivieren der Diagnoseprotokollierung zum Streamen von SQL-Daten an Azure Monitor-Protokolle.
Azure-Ressourcen – IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. Azure Key Vault<br/> 4. Netzwerksicherheitsgruppen<br/> 5. Azure Traffic Manager | 1. Kapazität, Verfügbarkeit und Leistung.<br/> 2. Leistungs- und Diagnoseprotokolle (Aktivitäten, Zugriff, Leistung und Firewall)<br/> 3. Überwachung, wann und von wem auf Ihre Schlüsseltresore zugegriffen wurde.<br/> 4. Überwachung von Ereignissen bei der Anwendung von Regeln und Regelzähler für die Häufigkeit der Anwendung von Regeln zum Ablehnen oder Zulassen<br/>5. Überwachung der Verfügbarkeit des Endpunktstatus. | 1. Speichermetriken für Blob Storage<br/> 2. Aktivieren der Diagnoseprotokollierung Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle.<br/> 3. Aktivieren Sie die Diagnoseprotokollierung, konfigurieren Sie das Streaming zu den Azure Monitor-Protokollen, und aktivieren Sie die [Azure Key Vault-Analyse-Lösung](https://docs.microsoft.com/azure/azure-monitor/insights/azure-key-vault). <br/> 4. Aktivieren der Diagnoseprotokollierung von Netzwerksicherheitsgruppen und Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle<br/> 5. Aktivieren der Diagnoseprotokollierung von Traffic Manager-Endpunkten und Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle
Netzwerk| Kommunikation zwischen dem virtuellen Computer und einem oder mehreren Endpunkten (ein anderer virtueller Computer, ein vollqualifizierter Domänenname, ein URI oder eine IPv4-Adresse). | Überwachung von Änderungen der Erreichbarkeit, Latenz und Netzwerktopologie zwischen der VM und dem Endpunkt. | Azure Network Watcher
Azure-Abonnement | Azure Service Health und grundlegende Dienstintegrität | <li> Für einen Dienst oder eine Ressource durchgeführte Verwaltungsmaßnahmen.<br/><li> Die Dienstintegrität eines Azure-Diensts hat sich verschlechtert, oder er ist nicht verfügbar.<br/><li> Bei einer Azure-Ressource vom Azure-Dienst erkannte Integritätsprobleme.<br/><li> Mit der Azure-Autoskalierung durchgeführte Vorgänge zeigen einen Fehler oder eine Ausnahme an. <br/><li> Mit Azure Policy durchgeführte Vorgänge zeigen an, dass eine zulässige oder abgelehnte Aktion ausgeführt wurde.<br/><li> Datensatz der in Azure Security Center generierten Warnungen. |Im Aktivitätsprotokoll für Überwachung und Warnungen unter Verwendung von Azure Resource Manager bereitgestellt.
Azure-Mandant|Azure Active Directory || Aktivieren der Diagnoseprotokollierung und Konfigurieren des Streamings von Daten an Azure Monitor-Protokolle.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Überwachen der Hybrid Cloud

In diesem Abschnitt stehen in Kürze umfassende Empfehlungen zu diesem Cloudmodell bereit.  

## <a name="private-cloud-monitoring"></a>Überwachen der privaten Cloud

Durch Verwendung von System Center Operations Manager wird eine ganzheitliche Überwachung von Azure Stack ermöglicht. Insbesondere können Sie die Workloads überwachen, die im Mandanten, auf Ressourcenebene, auf den virtuellen Computern und in der Infrastruktur ausgeführt werden, die Azure Stack (physische Server und Netzwerkswitches) hostet. Eine ganzheitliche Überwachung ist außerdem durch eine Kombination der in Azure Stack enthaltenen [Funktionen zur Infrastrukturüberwachung](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) möglich. Mithilfe dieser Funktionen können Sie die Integrität und Warnungen für eine Azure Stack-Region und den [Azure Monitor-Dienst](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) in Azure Stack anzeigen. Dort werden für die meisten Dienste grundlegende Infrastrukturmetriken und Protokolle bereitgestellt.

Wenn Sie bereits in Operations Manager investiert haben, sollten Sie die Verfügbarkeit und den Integritätszustand von Azure Stack-Bereitstellungen mit dem Management Pack von Azure Stack überwachen. Dies umfasst Regionen, Ressourcenanbieter, Updates, Aktualisierungsläufe, Skalierungseinheiten, Einheitsknoten, Infrastrukturrollen und deren Instanzen (logische Einheiten bestehend aus den Hardwareressourcen). Das Management Pack verwendet die REST-APIs des Integritäts- und des Updateressourcenanbieters, um mit Azure Stack zu kommunizieren. Die physischen Server und Speichergeräte können Sie mit den Management Packs der OEM-Anbieter (z. B. von Lenovo, Hewlett Packard oder Dell) überwachen. Operations Manager kann über das SNMP-Protokoll die Netzwerkswitches nativ überwachen, um grundlegende Statistiken zu sammeln. Die Überwachung der Workloads des Mandanten ist mit dem Azure-Management Pack durch Ausführung zweier grundlegender Schritte möglich. Konfigurieren Sie zunächst das Abonnement, das überwacht werden soll, und fügen Sie dann die Monitore für dieses Abonnement hinzu.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Erfassen der richtigen Daten](./data-collection.md)
