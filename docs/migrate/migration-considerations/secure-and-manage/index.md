---
title: Sichern und Verwalten
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Tools für sichere Überwachung und Verwaltung
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c03e6d25734a487c317fa9c6904a799dfd53f631
ms.sourcegitcommit: 72df8c1b669146285a8680e05aeceecd2c3b2e83
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/02/2019
ms.locfileid: "74681788"
---
# <a name="secure-monitoring-and-management-tools"></a>Tools für sichere Überwachung und Verwaltung

Nach Abschluss einer Migration sollten die migrierten Ressourcen durch kontrollierte IT-Abläufe verwaltet werden. Dieser Artikel stellt keine Abweichung von den bewährten Methoden für den Betrieb dar. Stattdessen sollte das Folgende als praktikable Mindestanforderung zur Sicherung und Verwaltung migrierter Ressourcen betrachtet werden, entweder aus Sicht der IT-Abläufe oder unabhängig davon, wenn die IT-Abläufe online gehen.

## <a name="monitoring"></a>Überwachung

Unter *Überwachung* wird das Erfassen und Analysieren von Daten verstanden, um die Leistung, Integrität und Verfügbarkeit Ihrer geschäftlichen Workload und der Ressourcen, von denen sie abhängt, zu bestimmen. Azure umfasst mehrere Dienste, die eine bestimmte Rolle oder Aufgabe im Überwachungsbereich ausführen. Zusammen bieten diese Dienste eine umfassende Lösung für das Sammeln, Übertragen und Analysieren von Telemetriedaten aus Ihren Workloadanwendungen und den zugrunde liegenden Azure-Ressourcen, die sie unterstützen. Erhalten Sie Einsicht in die Integrität und Leistung Ihrer Apps, Infrastruktur und Daten in Azure mit Cloudüberwachungstools wie Azure Monitor, Log Analytics und Application Insights. Verwenden Sie diese Cloudüberwachungstools, um Maßnahmen zu ergreifen und Integrationen in Ihre Lösungen zur Dienstverwaltung durchzuführen:

- **Kernüberwachung** Unter der Kernüberwachung versteht man die grundlegende, erforderliche Überwachung aller Azure-Ressourcen. Diese Dienste benötigen nur eine minimale Konfiguration und sammeln die von den Premium-Überwachungsdiensten genutzten Telemetriedaten.
- **Umfassende Anwendungs- und Infrastrukturüberwachung** Azure-Dienste bieten umfassende Funktionen für das Sammeln und Analysieren von Überwachungsdaten auf einer tieferen Ebene. Diese Dienste bauen auf der Kernüberwachung auf und nutzen allgemeine Funktionen in Azure. Sie bieten leistungsstarke Analysen der gesammelten Daten und somit einzigartige Einblicke Ihre Anwendungen und Infrastrukturen.

Erfahren Sie mehr über [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) zur Überwachung migrierter Ressourcen.

## <a name="security-monitoring"></a>Sicherheitsüberwachung

Verlassen Sie sich auf die einheitliche Sicherheitsüberwachung und die erweiterte Benachrichtigung bei Bedrohungen über Ihre hybride Cloudworkloads hinweg von Azure Security Center. Das Security Center bietet umfassende Einblicke in sowie die Kontrolle über die Sicherheit von Cloudanwendungen in Azure. Erkennen Sie Bedrohungen frühzeitig, und ergreifen Sie Maßnahmen, um gegen sie vorzugehen. Reduzieren Sie außerdem die Risiken, indem Sie den adaptiven Bedrohungsschutz aktivieren. Dank integrierter Dashboards erhalten Sie sofort Einblick in Sicherheitswarnungen und -lücken, die Aufmerksamkeit erfordern. Das Azure Security Center kann bei vielen Funktionen helfen, einschließlich:

- **Zentrale Richtlinienüberwachung** Stellen Sie die Einhaltung unternehmensspezifischer oder gesetzlicher Sicherheitsvorschriften sicher, indem Sie die Hybridcloud-Workloads übergreifenden Sicherheitsrichtlinien zentral verwalten.
- **Laufende Sicherheitsbewertung** Überwachen Sie die Sicherheit von Computern, Netzwerken, Speicher- und Datendiensten und Anwendungen, um potenzielle Sicherheitsprobleme aufzudecken.
- **Umsetzbare Empfehlungen** Beheben Sie Sicherheitsrisiken, bevor sie von Angreifern ausgenutzt werden können. Integrieren Sie priorisierte und umsetzbare Sicherheitsempfehlungen.
- **Erweiterter Cloudschutz** Reduzieren Sie Bedrohungen mithilfe eines Just-in-Time-Zugriffs auf Verwaltungsports und Sicherheitslisten, um Anwendungen zu steuern, die auf Ihren VMs ausgeführt werden.
- **Priorisierte Warnungen und Vorfälle** Konzentrieren Sie sich mittels priorisierter Warnungen und Vorfälle auf die größten Bedrohungen.
- **Integrierte Sicherheitslösungen** Sammeln, durchsuchen und analysieren Sie Sicherheitsdaten aus verschiedensten Quellen (einschließlich verbundener Partnerlösungen).

Weitere Informationen zum Sichern von migrierten Ressourcen finden Sie unter [Azure Security Center](https://docs.microsoft.com/azure/security-center).

## <a name="service-health-monitoring"></a>Überwachung der Dienstintegrität

Mit Azure Service Health werden personalisierte Benachrichtigungen und Anleitungen bereitgestellt, wenn bei Ihnen Probleme mit Azure-Diensten auftreten. Dieser Dienst kann Sie benachrichtigen, die Auswirkungen von Problemen verdeutlichen und Sie über die Lösung eines Problem auf dem Laufenden halten. Er kann Sie auch bei der Vorbereitung auf geplante Wartungsmaßnahmen und Änderungen unterstützen, die sich u.U. auf die Verfügbarkeit Ihrer Ressourcen auswirken.

- **Dashboard zur Dienstintegrität:** Überprüfen Sie die allgemeine Integrität Ihrer Azure-Dienste und -Regionen, und erhalten Sie detaillierte Aktualisierungen zu aktuellen Dienstproblemen, anstehenden geplanten Wartungsarbeiten und Dienstübergängen.
- **Warnungen zur Dienstintegrität:** Konfigurieren Sie Warnungen, mit denen Sie und Ihre Teams über ein Dienstproblem (etwa einen Ausfall oder eine anstehende geplante Wartung) benachrichtigt werden.
- **Verlauf der Dienstintegrität:** Sehen Sie sich frühere Dienstprobleme an, und laden Sie offizielle Zusammenfassungen und Berichte von Microsoft herunter.

Erfahren Sie mehr über [Azure Service Health ](https://docs.microsoft.com/azure/service-health), um stets die Integrität Ihrer migrierten Ressourcen im Blick zu haben.

## <a name="protect-assets-and-data"></a>Schützen von Ressourcen und Daten

Azure Backup bietet eine Möglichkeit, VMs, Dateien und Daten zu schützen. Azure Backup kann bei vielen Funktionen helfen, einschließlich:

- Sichern von virtuellen Computern
- Sichern von Dateien
- Sichern von SQL Server-Datenbanken
- Wiederherstellen von geschützten Ressourcen

Weitere Informationen zum Schützen migrierter Ressourcen finden Sie unter [Azure Backup](https://docs.microsoft.com/azure/backup).

## <a name="optimize-resources"></a>Optimieren von Ressourcen

Azure Advisor ist Ihr personalisierter Berater zu Best Practices in Azure. Azure Advisor analysiert Ihre Konfigurationen und Ihre Nutzungstelemetriedaten und bietet Empfehlungen zum Optimieren Ihrer Azure-Ressourcen im Hinblick auf Hochverfügbarkeit, Sicherheit, Leistung und Kosten. Die Inlineaktionen des Advisor helfen Ihnen, schnell und einfach Empfehlungen umzusetzen und Ihre Bereitstellungen zu optimieren.

- **Best Practices in Azure:** Optimieren Sie migrierte Ressourcen im Hinblick auf Hochverfügbarkeit, Sicherheit, Leistung und Kosten.
- **Ausführliche Anweisungen:** Mit Quicklinks können Sie Empfehlungen effizient umsetzen.
- **Warnungen für neue Empfehlungen:** Bleiben Sie im Hinblick auf neue Empfehlungen auf dem Laufenden, etwa bei zusätzlichen Möglichkeiten zum richtigen Dimensionieren von VMs und zur Kostensenkung.

Erfahren Sie mehr darüber, wie Sie mit [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) Ihre migrierten Ressourcen optimieren können.

## <a name="suggested-skills"></a>Empfohlene Qualifikationen

Microsoft Learn ist ein neuer Lernansatz. Die Bereitschaft zu den neuen Qualifikationen und Aufgaben, die mit der Cloudeinführung verbunden sind, entsteht nicht problemlos. Microsoft Learn bietet einen lohnenderen Ansatz für praktisches Lernen, der Ihnen hilft, Ihre Ziele schneller zu erreichen. Punkte sammeln, zu höheren Stufen aufsteigen und mehr erreichen.

Hier sehen Sie ein Beispiel für einen angepassten Lernpfad in Microsoft Learn, der auf den Abschnitt „Sichern und Verwalten“ des Cloud Adoption Framework abgestimmt ist: 

[Schützen Ihrer Clouddaten:](https://docs.microsoft.com/learn/paths/secure-your-cloud-data/) Azure ist auf Sicherheit und Konformität ausgelegt. Erfahren Sie, wie Sie die integrierten Dienste nutzen können, um Ihre App-Daten sicher zu speichern. So stellen Sie sicher, dass nur autorisierte Dienste und Clients darauf zugreifen können.
