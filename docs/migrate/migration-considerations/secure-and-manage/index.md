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
ms.openlocfilehash: 652637905f9de09972eed199f85245e99fb60e29
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022587"
---
# <a name="secure-monitoring-and-management-tools"></a>Tools für sichere Überwachung und Verwaltung

Nach Abschluss einer Migration sollten die migrierten Ressourcen durch kontrollierte IT-Abläufe verwaltet werden. Dieser Artikel ist nicht darauf ausgerichtet, eine Abweichung von den bewährten betrieblichen Methoden zu empfehlen. Stattdessen sollte das Folgende als praktikable Mindestanforderung zur Sicherung und Verwaltung migrierter Ressourcen betrachtet werden, entweder aus Sicht der IT-Abläufe oder unabhängig davon, wenn die IT-Abläufe online gehen.

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

## <a name="protect-assets-and-data"></a>Schützen von Ressourcen und Daten

Azure Backup bietet eine Möglichkeit, VMs, Dateien und Daten zu schützen. Azure Backup kann bei vielen Funktionen helfen, einschließlich:

- Sichern von virtuellen Computern
- Sichern von Dateien
- Sichern von SQL Server-Datenbanken
- Wiederherstellen von geschützten Ressourcen

Weitere Informationen zum Schützen migrierter Ressourcen finden Sie unter [Azure Backup](https://docs.microsoft.com/azure/backup).
