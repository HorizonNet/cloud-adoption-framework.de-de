---
title: Strategie zur Cloudüberwachung
description: Erfahren Sie, wie eine wirksame Strategie zur Cloudüberwachung definiert werden kann.
author: mgoedtel
ms.author: magoedte
ms.date: 06/18/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: f5fccf07ec3618baf8e9cae391303cbba66313e2
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85090653"
---
# <a name="cloud-monitoring-guide-formulate-a-monitoring-strategy"></a>Leitfaden zur Cloudüberwachung: Formulieren einer Überwachungsstrategie

Während Sie Ihre digitale Transformation hin zur Cloud vollziehen, ist es wichtig, eine wirksame Strategie zur Cloudüberwachung unter Beteiligung von Entwicklern, Betriebspersonal und Infrastrukturtechnikern zu planen und zu entwickeln. Die Strategie sollte bei minimaler Definition wachstumsorientiert sein, sukzessive weiterentwickelt werden und stets auf die Bedürfnisse der Fachbereiche abgestimmt sein. Das Ergebnis ist ein agiles Betriebsmodell, in dessen Mittelpunkt die Fähigkeit des Unternehmens steht, komplexe verteilte Anwendungen, auf die die Fachbereiche angewiesen sind, proaktiv zu überwachen.

## <a name="where-to-start"></a>Einstieg

Um den Weg in die Cloud zu ebnen, greifen Sie auf die Cloud Adoption Framework-Phasen [Strategie](index.md) und [Planen](../plan/index.md) zurück. Durch Überwachung werden Motivationen, Geschäftsergebnisse und Initiativen beeinflusst und gerechtfertigt. Binden Sie Überwachung in die Phasen „Strategie“ und „Planen“, Ihre Initiativen und Projekte ein. Untersuchen Sie beispielsweise, wie im Rahmen des ersten Einführungsprojekts ein frühzeitiges Betriebsmanagement in Azure etabliert wird. Stellen Sie sich vor, wie das Cloudbetriebsmodell aussehen muss, einschließlich Rolle der Überwachung. Der Überwachung ist am besten mit einem dienstorientierten Ansatz als betriebliche Aufgabe gedient, bei der die Zuständigen für die Überwachung als Berater und Anbieter von Fachwissen für Benutzer im IT-Bereich und den Fachbereichen fungieren.  

Es folgen wichtige Bereiche, die eine zuverlässige Überwachungsstrategie maßgeblich beeinflussen:

* Überwachen Sie die Integrität Ihrer Anwendungen auf Grundlage ihrer Komponenten und Beziehung mit anderen Abhängigkeiten. Beginnen Sie mit der Clouddienstplattform, den Ressourcen, dem Netzwerk und schließlich der Anwendung, indem Sie nach Möglichkeit Metriken und Protokolle erfassen. Schließen Sie beim Hybrid Cloud-Modell lokale Cloudinfrastruktur und andere Systeme ein, auf die die Anwendung angewiesen ist.

* Beziehen Sie die Messung der Erfahrung des Endbenutzers in Ihren Plan zur Überwachung der Anwendungsleistung ein, indem Sie die typischen Interaktionen Ihres Kunden mit der Anwendung nachahmen.

* Stellen Sie sicher, dass Sicherheitsanforderungen den Richtlinien Ihres Unternehmens zur Einhaltung von Sicherheitsvorschriften entsprechen.

* Stimmen Sie Benachrichtigungen damit ab, was als relevanter/praktischer Vorfall angesehen wird (d. h. Warnungen und Ausnahmen). Stimmen Sie die Bedeutung von Schweregraden mit Ihrer Matrix für Vorfallpriorität/Notfalleskalation ab.

* Erfassen Sie nur die Metriken und Protokolle, die für Fachbereiche die und IT-Abteilung sinnvoll, messbar und feststellbar sind.

* Definieren Sie einen Plan zur Integration in bestehende ITSM-Lösungen (z. B. Remedy, ServiceNow usw.) zur Generierung von Vorfällen oder vorgelagerten Überwachung. Bestimmen Sie, welche Benachrichtigung weitergeleitet werden sollen, ob eine Ergänzung der Benachrichtigungsinformationen erforderlich ist, um bestimmte Filteranforderungen zu unterstützen, und wie die Konfiguration erfolgen soll.

* Machen Sie sich klar, wer Transparenz braucht, welche Informationen wem angezeigt werden müssen und wie diese entsprechend der Rolle und Zuständigkeit visualisiert werden sollten.

Im Zentrum des Betriebsmanagements muss Ihre IT-Organisation zentrale Governance und strikte Delegierung der Ansätze für Aufbau, Betrieb und Verwaltung von IT-Diensten vorsehen.

### <a name="initial-strategy-goals"></a>Erste strategische Ziele

Als Systemarchitekt oder strategischer Planer müssen Sie möglicherweise eine erste Strategie für das Betriebsmanagement formulieren, bei der Überwachung eine wichtige Rolle spielt. Beachten Sie diese vier Aspekte:

1. Cloudproduktionsdienste verwalten, wenn sie in der Produktion live geschaltet werden, wie z. B. Netzwerke, Anwendungen, Sicherheit und virtuelle Infrastruktur.

2. Begrenzte Ressourcen einsetzen, um Ihre vorhandenen Tools, Fähigkeiten und Fachkenntnisse im Bereich Überwachung zu optimieren, und Überwachungslösungen in der Cloud nutzen, um Komplexität zu reduzieren.

3. Die Prozesse Ihrer Überwachungslösung effizienter gestalten, schneller und reibungsloser nach Maß arbeiten und auch Änderungen schneller vornehmen.

4. Erläutern, wie Ihre Organisation die Überwachung auf Grundlage von Cloudmodellen planen und durchführen wird. Arbeiten Sie auf das Ziel hin, Ihre Anforderungen beim Umstieg der Organisation von IaaS auf PaaS und dann auf SaaS zu reduzieren.  

## <a name="determine-what-you-have"></a>Bestimmen der aktuellen Situation

Als Experte für die Bewältigung von Aufgaben arbeiten Sie möglicherweise eng mit einem Lenkungsausschuss, einem Systemarchitekten und strategischen Planern zusammen. Möglicherweise arbeiten Sie an der Formulierung Ihrer Überwachungsstrategie, indem Sie den Istzustand Ihrer Systemverwaltung bewerten, einschließlich Mitarbeiter, Partner, Fremdvergabe, Tools, Komplexität, Lücken und Risiken. Diese Einschätzung hilft Ihnen, die gefundenen Probleme zu priorisieren und die wichtigsten Möglichkeiten zur Verbesserung der aktuellen Situation auszuwählen. Bestimmen Sie ferner als ein wichtiges Ergebnis die Dienste, Systeme und Daten, die wahrscheinlich lokal bleiben werden. Im Idealfall wünscht die Unternehmensleitung eine Roadmap von Initiativen, jedoch in direktem Verhältnis zum bekannten Planungshorizont. Die Diskussion von Unbekannten ist ebenso wichtig.

## <a name="high-level-modeling"></a>Erstellen eines allgemeinen Modells

Da die Fachbereiche bestimmen, welche Dienste in die Cloud verlagert werden sollen, müssen Sie Ihre Ressourcen sorgfältig einsetzen. Lokal sind Sie für die Überwachung verantwortlich und haben hohe Investitionen getätigt. Beim Umstieg auf SaaS-Dienste entfällt beispielsweise nicht Ihre Verantwortung für die Überwachung. Sie entscheiden, wer Zugriff benötigt, wer Benachrichtigungen empfängt und wer einen Mindestzugriff auf Analysen braucht. [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/) und [Azure Arc](https://azure.microsoft.com/services/azure-arc/) sind Azure-Dienste mit der Flexibilität, Überwachungsszenarien in allen vier Cloudmodellen und nicht nur Ressourcen innerhalb von Azure abzudecken.  
Außerdem müssen Sie, wie nachstehend gezeigt, über die üblichen Cloudmodelle hinausblicken. Wenn Sie in Ihrem Unternehmen Office-Apps einsetzen, die von [Microsoft 365](https://docs.microsoft.com/microsoft-365/?view=o365-worldwide)-Diensten bereitgestellt werden, müssen Sie zusätzlich zum [Azure Security Center](https://docs.microsoft.com/azure/security-center/) die Überwachung von Sicherheit und Compliance mit Microsoft 365 einbeziehen. Dazu gehören Identitäten, Endpunktverwaltung und Geräteüberwachung außerhalb Ihres Unternehmensnetzwerks.

![Diagramm von Cloudmodellen](./media/monitoring-strategy/cloud-models.png)

## <a name="monitoring-informs-strategy"></a>Überwachung beeinflusst Strategie

Überlegen Sie, wo die Fähigkeit zur frühzeitigen Überwachung die *Strategie*  beeinflusst. Viele Entscheidungen hängen von frühen Überwachungsdaten ab, um eine Roadmap für Kompetenzen zu erstellen, die begrenzte Ressourcen lenkt und Vertrauen schafft. Strategien brauchen auch praktische Beiträge aus der Überwachung der Aktivierung von Diensten.

Bedenken Sie die Rolle, die Überwachung bei Strategien zum schrittweisen Schützen und Absichern des digitalen Bestands spielt:

* Aktivitätsprotokolle und Sicherheitsüberwachung werden benötigt, um die Nutzung von Verzeichnissen und die externe gemeinsame Nutzung sensibler Inhalte zu messen, um in einem inkrementellen Ansatz über Schutzfunktionen zu informieren und die richtige Balance bei der Überwachung des Datenschutzes zu erreichen.

* Richtlinien und Baselines bilden die Grundlage für das Optimierungsziel (Migration, Lift & Shift, Neugestaltung) und stärken die Zuversicht, dass Daten und Informationen aus lokalen Umgebungen in Clouddienste migriert werden können.

Im weiteren Verlauf dieses Leitfadens gehen wir auf einige übliche Überwachungsszenarien bzw. Anwendungsfälle ein, die zur Beschleunigung der Einführung beitragen werden.

## <a name="formulate-a-monitoring-architecture"></a>Formulieren einer Überwachungsarchitektur

Definieren Sie Ihre aktuelle und künftige Architektur der Systemverwaltung, die Überwachung für folgende Zwecke umfasst:

* Aufwenden begrenzter Ressourcen zur Konsolidierung Ihrer Investitionen in die Überwachung

* Entscheiden, wie die Überwachung dazu beitragen kann, die künftigen von Ihrem Unternehmen benötigten Dienste zu nutzen: Cloudüberwachung überaus skalierbarer, resilienter und global ausgerichteter Clouddienste

* Abstimmen der Überwachung auf die künftigen Dienste und Ressourcen, die Sie in der Cloud überwachen werden

* Erkennen von Überwachungslücken in den drei Dimensionen: Tiefe, Breite und im gesamten Integritätsmodell

* Modellieren der finanziellen Aspekte, Kosten und Begleitfaktoren für eine Kosten-Nutzen-Analyse

* Lenken der Entscheidungen zu Hybridlösungen, die Sie treffen müssen

Ein Prinzip der Überwachung ist die Sichtbarkeit von Diensten. Damit ein Dienst, eine Ressource oder eine Komponente vollständig sichtbar ist, müssen Sie die drei Seiten dieses Prinzips austarieren:

1. Gründliche Überwachung durch Sammeln aussagekräftiger und relevanter Signale
2. Durchgehende oder breite Überwachung von der untersten Schicht des Stapels bis zur Anwendung
3. Rechts nach links mit Schwerpunkt auf den Integritätsaspekten (Verfügbarkeit, Leistung, Sicherheit und Kontinuität)

![Beispiel mit dreiseitigem Würfel](./media/monitoring-strategy/three-sided-cube.png)

Einige wichtige Fragen lauten:

* Wie gestalten Sie Sicherheitsprotokolle, und wie sichern Sie ihren Zugriff auf Sicherheits- und neue Datenschutzsteuerungen ab?

* Welche Dienste werden global verfügbar sein und können als solche an der Dienstgrenze global überwacht werden?

* Was ist mit den Netzwerkpunkten zwischen Ihrer Netzwerkinfrastruktur und der Netzwerkkonnektivität mit Dienst- und Anwendungsendpunkten, die uns sagt, wann wir oder der Cloudanbieter zuständig sind?

* Was sind die Grenzen von SecOps gegenüber Integrität und Leistung? Wie können wir SecOps Zusammenfassungen von Integrität und Status und umgekehrt den Besitzern der Dienste zur Verfügung stellen?

Hier nun einige Überlegungen zum Zusammensetzen dieser Architektur:

* Ein bei Dienstressourcen beginnender Datenflussansatz, der im Stapel nach oben – Metriken und Protokolldaten, die von der Infrastruktur, IoT-Geräten, mobilen Geräten usw. ausgegeben werden, sind allesamt der Verwaltung unterliegende Elemente – bis hin zu Überwachungstools (Mid-Tier) führt. Bewegen von Daten nach oben und nach außen (ITSM-Tools, globale Überwachung, Security Information and Event Management [SIEM], benutzerdefinierte Ergänzung von Warnungen usw.).

* Ob mit [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-2019) oder anderen Überwachungstools fortgefahren werden soll.

* Die wirtschaftlichen Kosten.

* Wie die Fachbereiche Protokolle und Metriken nutzen. Azure Monitor liefert eine beträchtliche Menge an Protokoll- und Zeitreihendaten für die Leistungs- und Integritätsseite der Überwachung ähnlich den Erfahrungen von SecOps. Protokolle und Metriken sind zwei wichtige Datenkomponenten der Azure Monitor-Architektur. Dies ist aus folgenden Gründen wichtig:

   1. Da Sie komplexe und große Clouddienste einrichten können, reduzieren sich die Kosten für das Problemmanagement. Denn die Analyse, Korrelation und Bestimmung von Problemursachen kann zentral erfolgen, wodurch die Notwendigkeit eines direkten Zugriffs auf Ressourcen verringert und die Sicherheit verbessert wird.

   2. Ähnlich wie ein SIEM-System führt Azure Monitor Computerdaten direkt aus lokalen und Azure-Ressourcen zusammen (einschließlich Aktivitätsprotokollen, Mandanten- und Abonnementdaten sowie sämtlicher Protokolldaten eines REST-Clients) und bietet eine einfache Abfragesprache zur Datenanalyse, die weit über das hinausgeht, was früher möglich war.

Prüfen Sie Ihre Datenflüsse und Tools:

* Quellen und Typen (Telemetrik, Ablaufverfolgungen, zustandsbehaftet, Zeitreihen).

* Tools und Suites (Zeilen): (Spalten: Verfügbarkeit, Kapazität, Sicherheit, Kontinuität und Compliance).

* Die Rolle der globalen Überwachung bzw. der obersten Ebene.

* Die Rolle der ITSM-Integration (IT-Service-Management), die bei bedeutenden Ereignissen ausgelöst wird.

Ziehen Sie in Ihrem Governanceplan eine zentrale Richtlinie für die Bedeutung von Ereignissen in Ihrem gesamten Unternehmen in Betracht, um Warnungen und Benachrichtigungen zu fördern. Dabei handelt es sich um eine der Schlüsselrichtlinien in Ihrer Überwachungsstrategie. Die folgende Tabelle ist ein Beispiel für ein Prioritätsmodell für das Incident Management zur Standardisierung von Ereignissen, Bedeutungen und Warnungen, das für Benachrichtigungen genutzt wird.

![Beispiel einer Matrix für den Schweregrad von Auswirkungen und Priorität](./media/monitoring-strategy/incident-priority-severity-matrix.png)

## <a name="formulate-initiatives"></a>Formulieren von Initiativen

Als Überwachungsexperte oder Systemadministrator haben Sie festgestellt, dass die Cloudüberwachung schneller und einfacher einzurichten ist, was zu kostengünstigen Demos oder Nutzennachweisen führt. Um den Hang, im Demomodus zu verbleiben, zu überwinden, müssen Sie mit der Strategie in ständigem Kontakt bleiben und in der Lage sein, auf die Produktion ausgerichtete Überwachungspläne umzusetzen. Da die Strategie mit vielen Unsicherheiten und Unbekannten behaftet ist, werden Sie nicht alle Überwachungsanforderungen im Voraus kennen. Entscheiden Sie daher über die erste Reihe von Einführungsplänen auf Grundlage dessen, was für die Fachbereiche und IT-Leitung minimal realisierbar ist. Sie können dies eine Kernfähigkeit nennen, *die erforderlich ist, um den Weg einzuschlagen*. Es folgen zwei Beispiele für Initiativen, um die Dinge in Gang zu bringen:

* Initiative 1: *Um Vielfalt und Komplexität unserer derzeitigen Investitionen in die Überwachung zu verringern, investieren wir zunächst in den Aufbau einer Kernfähigkeit, die Azure Monitor nutzt, da die gleichen Fähigkeiten und die gleiche Bereitschaft auch für andere Bereiche der Cloudüberwachung gelten.*

* Initiative 2: *Um zu entscheiden, wie wir unsere Lizenzpläne für den Identitäts-, Zugriffs- und allgemeinen Informationsschutz nutzen, werden wir den Abteilungen für Sicherheit und Datenschutz helfen, eine frühzeitige Aktivitätsüberwachung von Benutzern und Inhalten bei der Migration in die Cloud einzurichten. Dabei werden wir Fragen zu Klassifizierungsbezeichnungen, Verhinderung von Datenverlust, Verschlüsselung und Aufbewahrungsrichtlinien klären.*

### <a name="consider-scale"></a>Maßstab

Berücksichtigen Sie den Maßstab in Ihrer Strategie und wer *Überwachung als Code* definieren und standardisieren wird. Ihre Organisation sollte planen, standardisierte Lösungen unter Nutzung einer Kombination von Tools wie den folgenden zu entwickeln:

* Azure Resource Manager-Vorlagen
* Definitionen und Richtlinien für die Azure Policy-Überwachungsinitiative
* GitHub zur Einrichtung einer Quellcodeverwaltung für Skripts, Code und Dokumentation

### <a name="consider-privacy-and-security"></a>Datenschutz und Sicherheit

In Azure müssen Sie bestimmte Überwachungsdaten absichern, die von Ressourcen und den Aktionen auf Steuerungsebene ausgegeben werden, die in Azure protokolliert werden und Aktivitätsprotokolle genannt werden. Darüber hinaus spezialisierte Protokolle, die Benutzeraktivitäten registrieren, wie z. B. die Azure Active Directory-Anmelde- und Überwachungsprotokolle und, falls integriert, das einheitliche Microsoft 365-Überwachungsprotokoll, da sie sensible Daten enthalten, die unter Umständen datenschutzrechtlich geschützt werden müssen.

Ihre Überwachungsstrategie sollte diese Komponenten enthalten:

* Trennen nicht überwachungsbezogener Daten von Überwachungsdaten

* Beschränken des Zugriffs auf Ressourcen

### <a name="consider-business-continuity"></a>Geschäftskontinuität

Azure Monitor sammelt, indiziert und analysiert in Echtzeit von Computern und Ressourcen generierte Daten, um Ihre Betriebsabläufe und Geschäftsentscheidungen zu unterstützen. In seltenen Fällen kann es vorkommen, dass auf Einrichtungen in einer gesamten Region nicht zugegriffen werden kann, beispielsweise aufgrund von Netzwerkfehlern. Naturkatastrophen können dazu führen, dass eine Region vollständig ausfällt. Indem Sie sich auf diese Dienste in der Cloud verlassen, konzentriert sich Ihre Planung nicht auf Resilienz und Hochverfügbarkeit von Infrastruktur, sondern auf die Planung in diesen Bereichen:

* Verfügbarkeit für die Datenerfassung aus allen Ihren abhängigen Diensten und Ressourcen in Azure, aus Ressourcen in anderen Clouds und aus der lokalen Umgebung.

* Datenverfügbarkeit für Einblicke, Lösungen, Arbeitsmappen und andere Visualisierungen, Warnungen, Integration mit ITSM und anderen Diensten der Steuerungsebene in Azure zur Unterstützung Ihrer betrieblichen Anforderungen.

Erstellen Sie einen Wiederherstellungsplan, der die Wiederherstellung von Daten, Netzwerkausfälle, Fehler abhängiger Dienste und regionsweite Dienstunterbrechungen abdeckt.

### <a name="consider-maturity"></a>Reife

Reife ist ein wichtiger Aspekt in Ihrer Überwachungsstrategie. Wir empfehlen Ihnen, klein anzufangen, Daten zu sammeln und anhand dieser Informationen die Strategie festzulegen. Die ersten Überwachungslösungen, die Sie benötigen werden, sind solche, die die Beobachtbarkeit sicherstellen und reaktionsfähige Prozesse wie Incident- und Problemverwaltung einschließen. Hierzu gehen Sie wie folgt vor:

- Erstellen eines oder mehrerer Log Analytics-Arbeitsbereiche

- Aktivieren von Agents

- Aktivieren von Diagnoseeinstellungen für Ressourcen

- Aktivieren anfänglicher Warnungsregeln

Im Laufe der Zeit gewinnen Sie Vertrauen in die Fähigkeiten von Azure Monitor, da Sie Integritätsindikatoren messen müssen. Dies bedeutet, dass Sie sich verstärkt auf die Erfassung von Protokollen konzentrieren, Einblicke und Metriken aktivieren und nutzen und Protokollsuchabfragen definieren, die die Messung und Berechnung dessen, was positiv/negativ ist, vorantreiben.

Zu Lernzyklen gehört es, Überwachungsdaten und Einblicke in die Hände von Führungskräften gelangen zu lassen und sicherzustellen, dass die gewünschten Benutzer über die Überwachungsdaten verfügen, die sie benötigen. Zu den Lernzyklen zählen die kontinuierliche Abstimmung und Optimierung Ihrer anfänglichen Überwachungspläne zwecks Anpassung, Verbesserung des Diensts und Gestaltung von Einführungsplänen.

![Überwachungs- und Steuerungsstrategie](./media/monitoring-strategy/monitoring-and-control-strategy.png)

<Sup>1</Sup> Die **Wissenspyramide** ist eine häufig genutzte Methode mit Ursprung im Wissensmanagement zum Erläutern der Möglichkeiten, mithilfe einer Komponente aus Aktionen und Entscheidungen von **Zeichen**, **Daten**, **Informationen** zu **Wissen** zu gelangen.

Die Überwachung ist grundlegend für Dienste, die Sie in Azure erstellen. Ihre Strategie kann sich mit diesen vier Disziplinen der modernen Überwachung befassen, um Ihnen dabei zu helfen, ein praktikables Mindestmaß an Überwachung zu definieren und Vertrauen in die einzelnen Schritte zu gewinnen. Die Verlagerung Ihrer Fähigkeiten von reaktiv zu proaktiv und die Skalierung ihrer Reichweite auf Endbenutzer sind dabei nur ein Ziel.

* **Beobachten**: Zunächst sollten Sie die Überwachung vornehmlich zur Beobachtung der Integrität und des Status von Azure-Diensten und -Ressourcen einrichten. Konfigurieren Sie die grundlegende Überwachung, und führen Sie dann eine Automatisierung mit Azure Policy und Azure Resource Manager-Vorlagen durch, um für eine erste Sichtbarkeit der Dienste und ihrer Leistungsgarantie zu sorgen: Verfügbarkeit, Leistung oder Kapazität, Sicherheit und Konformität der Konfiguration. Konfigurieren Sie beispielsweise auf Grundlage einer minimalen machbaren Einrichtung von Azure Monitor die Ressourcen für Überwachung und Diagnose, und richten Sie Benachrichtigungen und Einblicke ein. Beziehen Sie Wissen und Bereitschaft zur Überwachung von Benutzern sowie die Definition und Auslöser von Ereignissen für Dienstaufgaben wie Vorfälle und Probleme ein. Ein Indikator für Reife ist, inwieweit eine Automatisierung erfolgen kann, um unnötige menschliche Kosten für die manuelle Beobachtung von Integrität und Status zu reduzieren. Zu wissen, welche Dienste intakt sind, ist ebenso wichtig wie eine Benachrichtigung zu Diensten, die nicht intakt sind.

* **Messen**: Konfigurieren Sie die Erfassung von Metriken und Protokollen aus allen Ressourcen zur Überwachung auf Symptome/Bedingungen, die problematisch sind und die potenzielle oder tatsächliche Auswirkungen auf die Verfügbarkeit des Diensts oder die Auswirkungen auf die Benutzer des Diensts/der Anwendung aufzeigen. Beispiel:

    * Wenn ich ein Feature in der Anwendung nutze, weist es eine Reaktionsverzögerung auf, meldet es einen Fehler, wenn ich etwas auswähle, oder reagiert es nicht?
    
    * Stellen Sie sicher, dass Dienste SLAs einhalten, indem Sie den Nutzwert des Diensts oder der Anwendung messen.

* **Reagieren**: Ausgehend vom Kontext bekannter Probleme, die sich beobachten und messen lassen, bewerten Sie, was als Fehler, automatische Behebung oder manuelle Reaktion auf Grundlage dessen gilt, was als Vorfall, Problem oder Änderung eingestuft wird.

* **Lernen und Verbessern**: Anbieter und Benutzer, die an Lernzyklen teilnehmen, müssen die tatsächlichen Überwachungsdaten in Form von Einblicken, Berichten und Arbeitsmappen verwerten, um den gewünschten Dienst kontinuierlich zu verbessern und die Konfiguration der Überwachung abzustimmen und zu optimieren. Wichtig ist auch, dass sich die Überwachungskonfiguration parallel zu Änderungen des Diensts verändert (Beispiel: Neu, modifiziert, ausgemustert usw.) und weiterhin im Einklang mit der tatsächlichen Leistungsgarantie des Diensts steht.

Um Ihnen zu helfen, Überwachungspläne mit der Strategie abzustimmen, nutzen Sie die folgende Tabelle, um die verschiedenen möglichen Überwachungsszenarien detaillierter zu kategorisieren. Dazu kommen die fünf **Rs** der Rationalisierung zum Einsatz, die zuvor in der Cloud Adoption Framework-Phase „Planen“ eingeführt wurden. Wenn Sie Systems Center Operations Manager einsetzen, stehen Ihnen Hybrid- und Cloudoptionen zur Verfügung, um Ihre Investition optimal zu nutzen.

|Typ |Überwachungsziel |Beispielziel |
|-----|---------------------|------------------|
| 1 | Nur lokal | System Center Operations Manager. Sie setzen die Überwachung von Diensten, Infrastruktur und Netzwerken bis hin zur Anwendungsschicht in eigenen Rechenzentren ohne Cloudunterstützung fort. |
| 2 | Von lokaler zu cloudbasierter Lösung | Sie setzen weiterhin System Center Operations Manager ein und wenden die Management Packs für Microsoft 365 und Azure an. |
| 3 | Lokal zu/mit Cloud (kooperativ), wobei Dienste sowohl in der Cloud als auch lokal ausgeführt werden | Sie richten eine anfängliche Überwachung mit Azure Monitor ein. Sie verbinden Azure Monitor mit System Center Operations Manager und Warnungsquellen wie Zabbix oder Nagios. Sie stellen Azure Monitor-Überwachungs-Agents im Multi-Homing mit System Center Operations Manager zur gemeinsamen Überwachung bereit.|
| 4 | Hybridmigration | Sie überwachen die Migration, z. B. von Exchange zu Microsoft 365 Exchange Online. Exchange Online Service Health und Dienstnutzung, Sicherheit und Konformität – alles in Microsoft 365. Sie setzen die Überwachung von lokalem Exchange mit System Center Operations Manager schrittweise außer Betrieb, bis die Migration abgeschlossen ist. |
| 5 | Dauerhaft hybrid | System Center Operations Manager, Azure AD, Azure Monitor, Azure Security Center, Intune: eine Palette von Tools für verschiedene digitale Ressourcen. |
| 6 | Cloudnativ |Azure Monitor, Azure Policy, Azure Security Center, Microsoft 365, Azure Service Health, Azure Resource Health usw. |
| 7 | Mandanten im Besitz mehrerer Clouds (Konsolidierung) | Sie zentralisieren die Überwachung vieler Mandanten. Azure Lighthouse, Azure Policy, Azure Monitor und Azure Sentinel. |
| 8 | Ökosystem mit mehreren Clouds |Sie zentralisieren die Überwachung verschiedener Cloudanbieter: Microsoft, Amazon, Google usw. |
| 9 | Anbieter > Benutzer | Sie überwachen Lösungen und Dienste als Cloudanbieter. |

## <a name="formulate-monitoring-requirements"></a>Formulieren von Überwachungsanforderungen

Im Verlauf dieses Prozesses wird deutlich, dass es langfristig noch viel zu tun geben könnte. Schlussendlich dehnt sich Ihre Sichtweise über das Firmennetzwerk hinaus auf die Arbeitsumgebung, auf Geräte und Endpunkte und weiter nach außen zur Grenze mit Identität als Sicherheit aus. Der mit Cloudüberwachung definierte neue Ansatz ist ein starker Motivator im Gegensatz zur auf Rechenzentren und Arbeitsstätten ausgerichteten Denkweise.

Sie können Azure jetzt einsetzen, um nach und nach mit dem Verwalten aller oder einiger Aspekte Ihrer lokalen Ressourcen zu beginnen, sogar für Dienste, die Sie weiterhin lokal betreiben werden. Darüber hinaus sollte die Strategie die Überwachung betreffenden Zuständigkeitsgrenzen in Abstimmung mit der Strategie zur Cloudeinführung des Unternehmens definieren, und zwar basierend auf dem Clouddienstmodell, das Ihr Unternehmen einführt. Sogar für auf IaaS basierende Dienste erhalten Sie Metriken, Protokolle, Sichten und Warnfunktionen über Azure Service Health. In diesem Dienst konfigurieren Sie Benachrichtigungen anhand der Überwachung der Verfügbarkeit Ihrer Azure-Ressourcen mit Resource Health. Bei SaaS-Diensten wie Microsoft 365 ist vieles bereits inbegriffen, weshalb Sie den entsprechenden Zugriff auf Portale, Dashboards, Analysen und Warnungen konfigurieren müssen. Aus Dienstsicht hat ein großer Dienst mit verteilten Komponenten wie Microsoft 365 Exchange Online eine Reihe von Zielen, die nicht nur auf das Beobachten von Integrität und Status beschränkt sind.

| Hauptzielsetzung | Ergebnis |
|-------------------|------------------|
|Integritäts- und Statusüberwachung |Sie können die langfristige Leistungsgarantie des Diensts oder der Komponente, einschließlich Servicelevel, ganzheitlich beobachten, messen, auswerten und verbessern, und zwar für alle diese Aspekte: Verfügbarkeit, Kapazität, Leistung, Sicherheit und Compliance. Ein intaktes System, ein Dienst oder eine Komponente ist online, leistungsfähig, abgesichert und konform. Die Systemüberwachung umfasst Protokolle und ist mit Integritätszuständen und Metriken in Echtzeit zustandsbehaftet.  Sie bietet außerdem Trendberichte, Einblicke und Trends mit Fokus auf Dienstnutzung. |
| Überwachung des Nutzwerts | Sie können die Qualität oder qualitativen Aspekte der Nutzenerbringung eines Systems beobachten, messen, auswerten und verbessern. Die Benutzererfahrung ist ein Typ von Anwendungsfällen in Bezug auf Überwachung. |
| Sicherheitsüberwachung | Sie können den Schutz zur Unterstützung von Cybersicherheitsstrategien und -aufgaben wie Sicherheitsabläufe, Identität und Zugriff, Informationsschutz, Datenschutz, Bedrohungsmanagement und Compliance beobachten, messen, auswerten und verbessern. Nutzen Sie zur Überwachung Azure Security Center und Azure Sentinel sowie Microsoft 365. |
| Kostenüberwachung | Sie können als neues primäres Ziel mit Azure Monitor und Azure Cost Management die Nutzung überwachen und Kosten schätzen. Die Cost Management-APIs bieten die Möglichkeit, Kosten- und Nutzungsdaten mithilfe einer mehrdimensionalen Analyse zu untersuchen. |

| Tertiäre Ziele | Ergebnis |
|---------------------|------------------|
| Aktivitätsüberwachung | Sie können Nutzung, Sicherheit und Compliance anhand von Quellen wie Azure-Aktivitätsprotokollen, Überwachungsprotokollen und dem einheitlichen Microsoft 365-Überwachungsprotokoll für Ereignisse auf Abonnementebene, Aktionen in Bezug auf Ressourcen, Benutzer- und Administratoraktivitäten, Inhalte, Daten und für Ihre Sicherheits- und Complianceanforderungen in Azure und Microsoft 365 beobachten, messen, auswerten und verbessern. |
| Dienstnutzung | Besitzer von Diensten wünschen sich Analysen und Erkenntnisse, um die Nutzung von Azure- und Microsoft 365-Diensten (IaaS, PaaS, SaaS) zu messen, auszuwerten und zu verbessern, und zwar mit Berichten zur Dienstnutzung, Analysen und Einblicken. Stellen Sie sicher, dass in den Plänen angegeben ist, wer Zugriff auf die Administratorportale, Dashboards, Erkenntnisse und Berichte benötigt. |
| Dienst- und Ressourcenintegrität | Sie können die Integrität Ihrer Cloudressourcen sowie Dienstausfälle und Empfehlungen von Microsoft im Auge behalten, um über Vorfälle und Wartungsmaßnahmen informiert zu bleiben. Beziehen Sie Resource Health in die Überwachung der Verfügbarkeit Ihrer Ressourcen ein, und geben Sie bei Änderungen der Verfügbarkeit Warnungen aus. |
| Kapazitäts- und Leistungsüberwachung | Zur Unterstützung der Systemüberwachung benötigen Sie möglicherweise mehr Detailtiefe und Spezialisierung. |
| Änderungs- und Complianceüberwachung | Sie können die Konfigurationsverwaltung von Ressourcen beobachten, messen, auswerten und verbessern, die nun auch Sicherheit in die Definition einbeziehen sollte, und zwar beeinflusst durch den sinnvollen Einsatz von Azure Policy zur Standardisierung von Überwachungskonfigurationen und zur Erzwingung einer Sicherheitshärtung. Protokollieren Sie Daten, um nach wichtigen Änderungen an Ressourcen zu filtern. |
| Identitäts- und Zugriffsüberwachung | Sie können Nutzung und Sicherheit von Active Directory, Azure Active Directory und Identitätsmanagement, das zum Integrieren von Benutzern, Anwendungen, Geräten und anderen Ressourcen unabhängig vom Standort dient, beobachten, messen, auswerten und verbessern. |
| Informationsschutz | Nicht nur Azure Monitor, sondern je nach Plan auch Azure Information Protection (AIP) bieten Nutzungsanalysen, die für die Entwicklung einer zuverlässigen Information Protection-Strategie für Azure und Microsoft entscheidend sind. |
| Datenschutzüberwachung | Organisationen sehen sich mit einem wachsenden Bedarf an Datenschutz konfrontiert, der den Schutz des digitalen Datenbestands, die Klassifizierung von Daten und die Verhinderung von Datenverlust einschließt, um das Risiko von Datenschutzverletzungen und -verstößen zu mindern. Microsoft 365 Information Protection bietet Überwachungsfunktionen, die auch in Azure Monitor integriert werden können. |
| Bedrohungsmanagement und integrierter Schutz vor Bedrohungen | In der Cloud werden die getrennten, herkömmlichen Rollen bei der Sicherheitsüberwachung mit der Systemüberwachung zusammengeführt. Der integrierte Schutz vor Bedrohungen umfasst beispielsweise die Überwachung, um einen optimalen Zero Trust-Zustand schneller zu erreichen. Die Integration von Azure Advanced Threat Protection ermöglicht eine Migration von der Nutzung von System Center Operations Manager zur Überwachung von Active Directory und die Integration Ihrer auf die AD-Sicherheit bezogenen Signale zur Erkennung komplexer Angriffe in Hybridumgebungen. |

## <a name="agile-solution-releases"></a>Freigabe agiler Lösungen

Letztendlich geben Sie Überwachungskonfigurationen oder -lösungen in der Produktion frei. Überlegen Sie sich als IT-Betriebsleiter oder als Leiter eines Überwachungsteams eine standardisierte, einfache Taxonomie, um die Kommunikation mit Benutzern, Führungskräften und IT-Betriebsteams zu verbessern. Ein agiler DevOps-Ansatz stellt sicher, dass die Überwachung den Teams anvertraut wird, die Clouddienste einrichten und betreiben sollen. Traditionelles Projektmanagement funktioniert zwar, doch ist es weder schnell genug, noch wird es in der Regel von Betriebsteams als gängige Praxis akzeptiert.

Nehmen Sie in Ihre Strategie und Ihr Betriebsmodell auf, wie Sie Überwachungspläne, Ziele und Konfigurationen (die Lösungen) vermitteln. Sie können z. B. Azure Boards nutzen:

|Agile-Begriff|Einzuschließende Informationen|Beispiele|
|----------|---------------|--------|
|Epics|Umfassende Überwachung<br>Initiativen der Überwachungsstrategie|Azure-Cloudüberwachung konsolidieren<br> Überwachen der Hybrid Cloud<br> Überwachen der privaten Cloud<br> Zentralen Überwachungsdienst einrichten |
|Features|Individuelle Überwachung<br> Pläne und Projekte|Überwachungsanforderungen<br> Überwachungsnutzer und -anbieter<br> Ziele<br> Tools<br> Zeitplan|
|User Stories und Aufgaben |Das Endergebnis ist eine Überwachungskonfiguration und/oder -lösung.|Netzwerküberwachung (z. B. Express Route)<br> Standardisierte IaaS-VM-Überwachung (z. B. Azure Monitor für VMs, Application Insight, Azure Policy, Einstellungen, Richtlinien, Berichte, Arbeitsbereiche.)|

## <a name="establish-minimum-governance"></a>Festlegen minimaler Governance

Legen Sie so früh wie möglich fest, wie Sie Ihre Investitionen in die Cloudüberwachung regeln möchten. Denken Sie daran, dass Azure Monitor ein *Mandantendienst* mit Einblick in Verwaltungsgruppen und Abonnements ist und Benutzer mit der rollenbasierten Zugriffssteuerung von Azure in ihren Aktionen eingeschränkt werden können.

Legen Sie in Azure-Zugriffsberechtigungen entsprechend der jeweiligen Rolle und Zuständigkeit fest. Es wird empfohlen, den Zugriff auf die Rolle **Leser** für Überwachungsbenutzer so früh wie möglich festzulegen und dann festzulegen, wem die Rolle **Mitwirkender** gewährt wird. 

Bestimmen Sie zunächst die Rollen, die Ressourcengruppen in Azure als Teil Ihres Frameworks für Governance besitzen und verwalten werden:

* Ob ein Überwachungsteam oder ein oder mehrere Administratoren von Ressourcen und Ressourcengruppen privilegierten Zugriff auf die Rolle **Mitwirkender an der Überwachung** haben werden.

* Die Benutzer, denen die Rolle **Mitwirkender an der Überwachung** zugewiesen werden sollte, die Ihnen Zugriff auf Features in Azure Monitor ermöglicht, sowie die Untersuchung von Problemen im Abschnitt „Überwachung“, der zu jeder Azure-Ressource gehört.

* Welche Führungskräfte Zugriff auf andere Azure-Leserrollen wie z. B. **Berichtleseberechtigter** benötigen.

Zusammenfassend lässt sich sagen, dass Ihre Benutzerrollen im Bereich der Überwachung wahrscheinlich einen breiten Zugriff benötigen, im Gegensatz zu Ihren Entwicklern und Systemadministratoren, die nur rollenbasierten Zugriff auf bestimmte Azure-Ressourcen haben müssen. Als zusätzliche Einschränkung sollten Sie sicherstellen, dass Sie Benutzer mit der Rolle „Leser“ vom Zugriff auf sensible Überwachungsdaten wie Sicherheits-, Anmelde- und Benutzeraktivitätsprotokolle ausnehmen.

## <a name="establish-readiness"></a>Etablieren von Bereitschaft

Stellen Sie frühzeitig einen Bereitschaftsplan auf, um Ihren IT-Mitarbeitern zu helfen, neue Kompetenzen, Praktiken und Techniken für die Cloudüberwachung in Azure zu erlernen.  Ziehen Sie den [Leitfaden zur Qualifikationsbereitschaft](suggested-skills.md) für die Überwachung heran, der sowohl grundlegende als auch überwachungsspezifische Anforderungen umfasst.