---
title: 'Leitfaden zur Cloudüberwachung: Warnungen'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Auswahlhilfe: Verwendung von Azure Monitor oder System Center Operations Manager in Microsoft Azure'
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: b605aad4400ef531022392ceb786ab5467812f5f
ms.sourcegitcommit: 5d865c3a3f105986bda83ff84f8cc29def030334
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/11/2019
ms.locfileid: "73912501"
---
# <a name="cloud-monitoring-guide-alerting"></a>Leitfaden zur Cloudüberwachung: Warnungen

Seit Jahren kämpfen IT-Organisationen gegen das Phänomen der „Alarmmüdigkeit“, das durch die in einem Unternehmen bereitgestellten Überwachungstools verursacht wird. Viele Systeme erzeugen eine große Anzahl von Warnungen, die häufig als bedeutungslos betrachtet werden. Aufgrund der Flut an Daten werden die relevanten Warnungen entweder übersehen oder ignoriert. Als Folge haben IT- und Entwicklungsabteilungen Schwierigkeiten, die internen oder externen Kunden zugesagte Servicequalität zu erfüllen. Es ist wichtig, den Zustand Ihrer Infrastruktur und Anwendungen zu verstehen, um die Zuverlässigkeit sicherzustellen. Sie müssen Ursachen schnell identifizieren, um die Leistungsminderung und Beeinträchtigung des Diensts zu minimieren oder die Auswirkungen von Vorfällen zu verringern oder die Anzahl der Vorfälle zu reduzieren.

## <a name="successful-alerting-strategy"></a>Wirkungsvolle Warnungsstrategie

*Sie können kein Problem beheben, von dem Sie nicht wissen, dass es vorhanden ist.*

Die Ausgabe von Warnungen bei wichtigen Faktoren ist entscheidend. Unterstützt wird dies durch das Erfassen und Messen der richtigen Metriken und Protokolle. Sie benötigen auch ein Überwachungstool, das in der Lage ist, die Speicherung, Aggregation, Visualisierung und Analyse durchzuführen sowie eine automatische Reaktion einzuleiten, wenn die Bedingungen erfüllt sind. Eine Verbesserung des Einblicks in Ihre Dienste und Anwendungen können Sie nur erreichen, wenn Sie deren Zusammensetzung vollständig verstehen. Sie ordnen diese Zusammensetzung in eine detaillierte Überwachungskonfiguration zu, die von der Überwachungsplattform angewendet wird. Diese Konfiguration beinhaltet die vorhersehbaren Fehlerzustände (die Symptome und nicht die Ursache des Fehlers), für die eine Warnung sinnvoll ist.

Berücksichtigen Sie die folgenden Grundsätze, um festzustellen, ob ein Symptom ein geeigneter Kandidat für Warnungen ist:

- **Handelt es sich tatsächlich um ein Problem?** Ist das Ereignis symptomatisch für ein echtes Problem oder ein Problem, das die Gesamtintegrität der Anwendung beeinflusst? Ist es beispielsweise relevant, ob eine Ressource eine hohe CPU-Auslastung aufweist? Oder dass eine bestimmte SQL-Abfrage, die auf einer SQL-Datenbankinstanz für diese Ressource ausgeführt wird, über einen längeren Zeitraum eine hohe CPU-Auslastung zeigt? Da die Bedingung der CPU-Auslastung ein echtes Problem darstellt, sollten Sie diesbezüglich eine Warnung ausgeben. Sie müssen das Team jedoch nicht benachrichtigen, da es nicht hilft, auf die Ursache der Bedingung hinzuweisen. Eine Warnung und Benachrichtigung zur Auslastung durch den SQL-Abfrageprozess hingegen ist relevant und kann zu entsprechenden Maßnahmen führen.
- **Ist das Problem dringend?** Handelt es sich um ein echtes Problem, das umgehend Aufmerksamkeit erfordert? Falls ja, muss das verantwortliche Team sofort benachrichtigt werden.
- **Sind Ihre Kunden betroffen?** Sind Benutzer des Diensts oder der Anwendung durch das Problem betroffen?
- **Sind weitere abhängige Systeme betroffen?** Gibt es Warnungen von abhängigen Komponenten, die miteinander in Verbindung stehen und möglicherweise korreliert werden könnten, um eine Benachrichtigung verschiedener Teams zu vermeiden, die alle am selben Problem arbeiten?

Stellen Sie diese Fragen, wenn Sie zu Beginn eine Überwachungskonfiguration entwickeln. Testen und validieren Sie die Annahmen in einer Nichtproduktionsumgebung, und fahren Sie dann mit der Bereitstellung in der Produktionsumgebung fort. Die Überwachungskonfigurationen werden aus bekannten Fehlermodi, den Testergebnissen simulierter Ausfälle und Erfahrungen verschiedener Teammitglieder abgeleitet.

Nach der Freigabe Ihrer Überwachungskonfiguration können Sie viel darüber erfahren, was funktioniert und was nicht. Berücksichtigen Sie ein hohes Warnungsvolumen, durch die Überwachung unbemerkte, aber von den Endbenutzern wahrgenommene Probleme und welche Maßnahmen sich bewährten, die im Rahmen dieser Bewertung ergriffen wurden. Identifizieren Sie Änderungen, die zur Verbesserung der Dienstbereitstellung implementiert werden sollen, als Teil eines kontinuierlichen, kontinuierlichen Optimierungsprozesses. Es geht nicht nur um die Bewertung von überflüssigen oder verpassten Warnungen, sondern auch um eine effiziente Überwachung der Workload. Es geht um die Effektivität Ihrer Warnungsrichtlinien, Prozesse und der gesamten Kultur, um festzustellen, ob sich Ihre Ergebnisse verbessern.

Sowohl System Center Operations Manager als auch Azure Monitor unterstützen Warnungen, die auf statischen oder dynamischen Schwellwerten sowie auf den daraufhin eingerichteten Maßnahmen basieren. Beispiele hierfür sind Warnungen für E-Mails, SMS und Sprachanrufe für einfache Benachrichtigungen. Beide Dienste unterstützen auch die ITSM-Integration (IT Service Management), um das Erstellen von Incidents zu automatisieren und über einen Webhook für eine Eskalation an das richtige Supportteam oder ein beliebiges anderes System zur Warnungsverwaltung zu sorgen.

Nach Möglichkeit können Sie einen von mehreren Diensten verwenden, um Wiederherstellungsaktionen zu automatisieren. Dazu gehören System Center Orchestrator, Azure Automation, Azure Logic Apps oder Autoskalierung bei flexiblen Workloads. Die Benachrichtigung der verantwortlichen Teams ist zwar die häufigste Maßnahme bei Warnungen, aber auch die Automatisierung von Korrekturmaßnahmen könnte geeignet sein. Diese Automatisierung kann dazu beitragen, den gesamten Incident Management-Prozess zu optimieren. Die Automatisierung dieser Wiederherstellungsaufgaben kann auch das Risiko von menschlichen Fehlern reduzieren.

## <a name="azure-monitor-alerting"></a>Azure Monitor-Warnungen

Wenn Sie Azure Monitor exklusiv verwenden, befolgen Sie diese Richtlinien, wenn Sie Geschwindigkeit, Kosten und Speichervolumen in Erwägung ziehen.

Abhängig vom Feature und der verwendeten Konfiguration können Sie Überwachungsdaten in sechs Repositorys speichern:

- **Azure Monitor-Metrikdatenbank**: Eine Zeitreihendatenbank, die hauptsächlich für die Metriken der Azure Monitor-Plattform verwendet wird, in die aber auch Metrikdaten von Application Insights gespiegelt werden. Bei Informationen in dieser Datenbank wird am schnellsten gewarnt.

- **Application Insights-Protokollspeicher**: Eine Datenbank, die die meisten Application Insights-Telemetriedaten in Protokollform speichert.

- **Azure Monitor-Protokollspeicher**: Der primäre Speicher für Azure-Protokolldaten. Andere Tools können Daten an diesen Speicher leiten und in den Protokollen von Azure Monitor analysiert werden. Abfragen von Protokollwarnungen weisen aufgrund der Erfassung und Indizierung eine höhere Wartezeit auf. Diese Wartezeit beträgt in der Regel 5-10 Minuten, kann aber unter bestimmten Umständen höher sein.

- **Aktivitätsprotokollspeicher**: Wird für alle Aktivitätsprotokoll- und Dienstintegritätsereignisse verwendet. Eine dedizierte Warnungserstellung ist möglich. Dieser Speicher enthält Ereignisse auf Abonnementebene, die für Objekte in Ihrem Abonnement auftreten, wie sie von außen wahrgenommen werden. Ein Beispiel könnte sein, wenn eine Richtlinie festgelegt wird oder auf eine Ressource zugegriffen oder diese gelöscht wird.

- **Azure Storage**: Universeller Speicher, der von der Azure-Diagnose und anderen Überwachungstools unterstützt wird. Es ist eine kostengünstige Option zur Langzeitaufbewahrung der Überwachungstelemetriedaten. Für in diesem Dienst gespeicherte Daten werden keine Warnungen unterstützt.

- **Event Hubs**: Wird im Allgemeinen verwendet, um Daten in lokale Tools oder Partnertools für Überwachung bzw. ITSM zu streamen.

Azure Monitor verfügt über vier Arten von Warnungen, die auf gewisse Weise an das Repository gebunden sind, in denen die Daten gespeichert werden:

- [Metrikwarnung](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric): Warnungen zu Daten in der Azure Monitor-Metrikdatenbank. Warnungen werden ausgelöst, wenn ein überwachter Wert einen benutzerdefinierten Schwellwert überschreitet. Es wird erneut eine Warnung ausgelöst, wenn der Wert in den Zustand „Normal“ zurückkehrt.

- [Protokollabfragewarnung](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query): Verfügbar für Warnmeldungen zu Inhalten in den Application Insights- oder Azure-Protokollspeichern. Das Auslösen von Warnungen basierend auf arbeitsbereichsübergreifenden Abfragen ist ebenfalls möglich.

- [Aktivitätsprotokollwarnung](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log): Warnungen zu Elementen im Aktivitätsprotokollspeicher mit Ausnahme von Service Health-Daten.

- [Service Health-Warnung](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications?toc=%2fazure%2fservice-health%2ftoc.json): Ein besonderer Warnungstyp, der ausschließlich für Service Health-Probleme verwendet wird, die aus dem Aktivitätsprotokollspeicher stammen, etwa Ausfälle und anstehende geplante Wartungsarbeiten. Beachten Sie, dass dieser Warnungstyp über [Azure Service Health](https://docs.microsoft.com/azure/service-health/service-health-overview), einen Begleitdienst von Azure Monitor, konfiguriert wird.

### <a name="enable-alerting-through-partner-tools"></a>Aktivieren von Warnungen über Partnertools

Wenn Sie eine externe Warnungslösung verwenden, sollten Sie möglichst viele Daten über Azure Event Hubs umleiten, da dies der schnellste Übertragungsweg aus Azure Monitor ist. Die Erfassung von Daten in Event Hubs ist kostenpflichtig. Wenn die Kosten im Vordergrund stehen (und nicht die Geschwindigkeit), können Sie Azure Storage als kostengünstigere Alternative verwenden. Stellen Sie einfach sicher, dass Ihre Überwachungs- oder ITSM-Tools Azure Storage lesen können, um die Daten zu extrahieren.

Azure Monitor bietet Unterstützung für die Integration mit anderen Überwachungsplattformen und ITSM-Software wie ServiceNow. Sie können die Azure-Warnungen verwenden und dennoch Aktionen außerhalb von Azure auslösen, wie es für Ihren Incident Management- oder DevOps-Prozess erforderlich ist. Wenn Sie Warnungen in Azure Monitor auslösen und erforderliche Maßnahmen als Reaktion auf diese Warnungen automatisieren möchten, können Sie mithilfe von Azure Functions, Azure Logic Apps oder Azure Automation basierend auf Ihrem Szenario und Ihren Anforderungen automatisierte Aktionen starten.

### <a name="specialized-azure-monitoring-offerings"></a>Spezielle Azure-Überwachungsangebote

[Verwaltungslösungen](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) speichern zugehörige Daten in der Regel im Azure-Protokollspeicher. Die beiden Ausnahmen sind Azure Monitor für VMs und Azure Monitor für Container. In der folgenden Tabelle wird das Warnungserlebnis basierend auf dem jeweiligen Datentyp und dem Speicherort beschrieben.

Lösung| Datentyp | Warnungsverhalten
:---|:---|:---
Azure Monitor für Container | Berechnete durchschnittliche Leistungsdaten von Knoten und Pods werden in den Metrikspeicher geschrieben. | Erstellen Sie Metrikwarnungen, wenn Sie basierend auf Abweichungen der im Zeitverlauf gemessenen aggregierten Nutzungsleistung benachrichtigt werden möchten.
|| Anhand von Perzentilen aus Knoten, Controllern, Containern und Pods berechnete Leistungsdaten werden in den Protokollspeicher geschrieben. Containerprotokolle und Bestandsinformationen werden ebenfalls in den Protokollspeicher geschrieben. | Erstellen Sie Protokollabfragewarnungen, wenn Sie basierend auf Abweichungen der gemessenen Auslastung von Clustern und Containern benachrichtigt werden möchten. Protokollabfragewarnungen können auch basierend auf Podphasen- und Statusknotenzählungen konfiguriert werden.
Azure Monitor für VMs | Metriken zu Integritätskriterien werden in den Metrikspeicher geschrieben. | Warnungen werden generiert, wenn sich der Integritätsstatus von „Fehlerfrei“ in „Fehlerhaft“ ändert. Diese Warnung unterstützt nur Aktionsgruppen, die zum Senden von SMS- oder E-Mail-Benachrichtigungen konfiguriert sind.
|| Zuordnungsdaten und Leistungsprotokolldaten zum Gastbetriebssystem werden in den Protokollspeicher geschrieben. | Es werden Protokollabfragewarnungen erstellt.

### <a name="fastest-speed-driven-by-cost"></a>Höchste Geschwindigkeit bei gleichzeitiger Kosteneffizienz

Einer der wichtigsten Faktoren bei der Entscheidung für einen Dienst stellt in Bezug auf die Warnungserstellung und eine schnelle Problembehebung die Latenzzeit dar. Wenn Sie Warnungen nahezu in Echtzeit (unter fünf Minuten) benötigen, sollten Sie zunächst überprüfen, ob Warnmeldungen zu Ihrer Telemetrie dort vorliegen oder abgerufen werden können, wo sie standardmäßig gespeichert wird. Im Allgemeinen ist diese Strategie auch die kostengünstigste Option, da das verwendete Tool bereits Daten an diesen Speicherort sendet.

Allerdings gibt es einige wichtige Hinweise zu dieser Regel.

**Telemetriedaten zum Gastbetriebssystem** werden auf verschiedene Weise im System erfasst.

- Die schnellste Methode, um Warnungen zu diesen Daten auszulösen, besteht darin, sie als benutzerdefinierte Metriken zu importieren. Verwenden Sie dazu die Azure-Diagnoseerweiterung und dann eine Metrikwarnung. Einige benutzerdefinierte Metriken befinden sich jedoch aktuell in der Vorschau und sind [kostenintensiver als andere Optionen](https://azure.microsoft.com/pricing/details/monitor).

- Die günstigste, aber langsamste Methode ist die, Daten an den Azure Kusto-Protokollspeicher zu senden. Die Ausführung des Log Analytics-Agents auf der VM ist die beste Möglichkeit, alle Gastbetriebssystemmetriken und Protokolldaten in diesem Speicher abzurufen.

- Sie können Daten an beide Speicher senden, indem Sie sowohl die Erweiterung als auch den Agent auf derselben VM ausführen. Sie können dann schnell Warnungen auslösen, aber die Gastbetriebssystemdaten auch in komplexeren Suchvorgängen kombiniert mit anderen Telemetrieanwendungen verwenden.

**Importieren von lokalen Daten**: Wenn Sie versuchen, Abfragen über lokale und Azure-Computer hinweg zu stellen und zu überwachen, können Sie mit dem Log Analytics-Agent Daten des Gastbetriebssystems erfassen. Sie können dann ein Feature namens [Protokolle zu Metriken](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) verwenden, um diese Metriken in den Metrikenspeicher zu integrieren. Bei dieser Methode wird ein Teil des Erfassungsvorgangs im Azure-Protokollspeicher umgangen, und die Daten sind deshalb früher in der Metrikdatenbank verfügbar.

### <a name="minimize-alerts"></a>Minimieren von Warnungen

Wenn Sie eine Lösung wie Azure Monitor für VMs verwenden und die standardmäßigen Integritätskriterien zur Überwachung der Leistung für Sie akzeptabel sind, sollten Sie keine sich überschneidenden Metrik- oder Protokollabfragewarnungen erstellen, die auf denselben Leistungsindikatoren basieren.

Wenn Sie Azure Monitor nicht für VMs verwenden, erleichtern Sie die Erstellung von Warnungen und die Verwaltung von Benachrichtigungen, indem Sie die folgenden Funktionen näher untersuchen:

> [!NOTE]
> Diese Features gelten nur für Metrikwarnungen, d.h. die Warnungen basieren auf Daten, die an die Azure Monitor-Metrikdatenbank gesendet werden. Diese Funktionen gelten nicht für die anderen Warnungstypen. Wie bereits erwähnt, ist das Hauptziel von Metrikwarnungen die Geschwindigkeit. Wenn es nicht entscheidend ist, dass eine Warnung in weniger als fünf Minuten ausgelöst wird, können Sie stattdessen Protokollabfragewarnungen verwenden.

- [Dynamische Schwellwerte](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds): Dynamische Schwellwerte überprüfen die Aktivität der Ressource über einen festgelegten Zeitraum und erstellen Ober- und Untergrenzen für das „Normalverhalten“. Wenn die überwachte Metrik diese Schwellwerte unter- oder überschreitet, erhalten Sie eine Warnung.

- [Multisignalwarnungen](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts): Sie können eine Metrikwarnung erstellen, die eine Kombination aus zwei verschiedenen Eingaben für zwei verschiedene Ressourcentypen verwendet. Wenn Sie z. B. einen Alarm auslösen möchten, wenn die CPU-Auslastung einer VM über 90 Prozent beträgt und die Nachrichten in einer bestimmten Azure Service Bus-Warteschlange zur Einspeisung in diese VM eine bestimmte Anzahl überschreiten, können Sie dies ohne Erstellung einer Protokollabfrage erreichen. Diese Funktion funktioniert nur für zwei Signale. Wenn Sie eine komplexere Abfrage verwenden möchten, müssen Sie Ihre Metrikdaten im Azure Monitor-Protokollspeicher erfassen und eine Protokollabfrage erstellen.

- [Warnungen zu mehreren Ressourcen](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts): Azure Monitor ermöglicht die Verwendung einer einzelnen Metrikwarnungsregel, die auf alle VM-Ressourcen angewendet wird. Mit diesem Feature können Sie Zeit sparen, da Sie nicht für jede VM einzeln Warnungen erstellen müssen. Der Preis für diesen Warnungstyp ist gleich. Unabhängig davon, ob Sie 50 Warnungen zur Überwachung der CPU-Auslastung für 50 VMs oder eine Warnung zur Überwachung der CPU-Auslastung für alle 50 VMs erstellen, fallen für Sie die gleichen Kosten an. Sie können diese Art von Warnungen auch in Kombination mit dynamischen Schwellenwerten verwenden.

Bei einer gemeinsamen Verwendung dieser Features können Sie Zeit sparen, indem Sie die Anzahl von Warnungsbenachrichtigungen und die Verwaltung der zugrunde liegenden Warnungen minimieren.

### <a name="alerts-limitations"></a>Einschränkungen für Warnungen

Beachten Sie unbedingt die [Einschränkungen](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) bezüglich der Anzahl der Warnungen, die Sie erstellen können. Einige Grenzwerte (aber nicht alle) können auf Wunsch erhöht werden. Wenden Sie sich hierzu an den Support.

### <a name="best-query-experience"></a>Optimales Abfrageverhalten

Wenn Sie nach Trends in Ihrem gesamten Datenbestand suchen, ist es sinnvoll, sämtliche Ihrer Daten in Azure-Protokolle zu importieren – es sei denn, die Daten befinden sich bereits in Application Insights. Sie können Abfragen über beide Arbeitsbereiche hinweg erstellen, deshalb ist eine Verschiebung von Daten zwischen diesen Tools nicht erforderlich. Sie können außerdem Aktivitätsprotokoll- und Service Health-Daten in Ihren Log Analytics-Arbeitsbereich importieren. Sie bezahlen für diese Erfassung und Speicherung, aber alle Ihre Daten werden zur Analyse und Abfrage an einem Ort gesammelt. Dieser Ansatz gibt Ihnen auch die Möglichkeit, komplexe Abfragebedingungen zu erstellen und bei diesen zu warnen.
