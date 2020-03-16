---
title: Sammeln von Überwachungsdaten in der Cloud
description: Es wird beschrieben, wie Sie die Integrität und Verfügbarkeit Ihrer Cloudlösung beobachten, um die richtigen Überwachungsdaten zu sammeln.
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 3b537caf193601057da458b07cb62bdba64a7b6b
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341105"
---
# <a name="cloud-monitoring-guide-collect-the-right-data"></a>Leitfaden zur Cloudüberwachung: Erfassen der richtigen Daten

Dieser Artikel beschreibt einige Überlegungen zum Sammeln von Überwachungsdaten in einer Cloudanwendung.

Um den Zustand und die Verfügbarkeit Ihrer Cloudlösung zu beobachten, müssen Sie die Überwachungstools so konfigurieren, dass sie unter Verwendung von Metriken eine Menge von Signalen sammeln, die auf vorhersehbaren Fehlerzuständen basieren. Diese Signale sind die Symptome des Fehlers, nicht die Ursache. Die Überwachungstools verwenden Metriken und für erweiterte Diagnose und Grundursachenanalyse auch Protokolle.

Planen Sie die Überwachung und Migration sorgfältig. Starten Sie mit dem Einbeziehen des Besitzers des Überwachungsdiensts, des Verantwortlichen für den Betriebsablauf und anderer beteiligter Personen während der Planungsphase und beteiligen Sie sie am gesamten Entwicklungs- und Freigabezyklus. Im Mittelpunkt steht die Entwicklung einer Überwachungskonfiguration, die auf den folgenden Kriterien basiert:

- Wie setzt sich der Dienst zusammen? Werden diese Abhängigkeiten aktuell überwacht? Sind in diesem Fall mehrere Tools beteiligt? Gibt es eine Möglichkeit der Konsolidierung, ohne Risiken einzugehen?
- Was ist die SLA des Diensts, und wie kann ich sie messen und melden?
- Wie sollte das Dienstdashboard aussehen, wenn ein Vorfall auftritt? Wie sollte das Dienstdashboard für den Besitzer des Diensts und das Team, das den Dienst unterstützt, aussehen?
- Welche Metriken produziert die Ressource, die ich überwachen muss?  
- Wie werden der Besitzer des Diensts, Supportteams und andere Personen die Protokolle durchsuchen?

Ihre Antworten auf diese Fragen bestimmen zusammen mit den Kriterien für die Warnungen, wie Sie die Überwachungsplattform nutzen werden. Wenn Sie von einer bestehenden Überwachungsplattform oder einem Satz von Überwachungstools migrieren, nutzen Sie die Migration als Gelegenheit, die von Ihnen gesammelten Signale neu zu bewerten. Dies gilt insbesondere jetzt, da mehrere Kostenfaktoren bei der Migration oder Integration in eine cloudbasierte Überwachungsplattform wie Azure Monitor zu berücksichtigen sind. Denken Sie daran, dass die Überwachung von Daten handlungsrelevant sein muss. Sie müssen optimierte Daten gesammelt haben, um Ihnen umfassende Übersicht über den allgemeinen Zustand des Diensts zu bieten. Die zum Identifizieren realer Vorfälle definierte Instrumentierung sollte so einfach, vorhersehbar und zuverlässig wie möglich sein.

## <a name="develop-a-monitoring-configuration"></a>Entwickeln einer Überwachungskonfiguration

Der Besitzer und das Team des Überwachungsdiensts folgen in der Regel einem allgemeinen Satz von Aktivitäten, um eine Überwachungskonfiguration zu entwickeln. Diese Aktivitäten beginnen bei der ersten Planung und reichen über Tests und Validierungen in einer Nichtproduktionsumgebung bis hin zum Einsatz in der Produktionsumgebung. Überwachungskonfigurationen werden aus bekannten Fehlermodi, Testergebnissen simulierter Ausfälle und Erfahrungen mehrerer Personen in dem Unternehmen (Service Desk, Betrieb, Ingenieure und Entwickler) abgeleitet. Solche Konfigurationen gehen davon aus, dass der Dienst bereits vorhanden ist, zur Cloud migriert wird und nicht neu strukturiert wurde.

Überwachen Sie die Integrität und Verfügbarkeit dieser Dienste in einem frühen Stadium des Entwicklungsprozesses, um Ergebnisse in Servicelevelqualität zu erhalten. Wenn Sie den Entwurf dieses Diensts oder dieser Anwendung nachträglich überwachen, werden Ihre Ergebnisse weniger erfolgreich sein.

Um eine schnellere Lösung des Vorfalls zu erreichen, beachten Sie die folgenden Empfehlungen:

- Definieren Sie für jede Dienstkomponente ein Dashboard.
- Verwenden Sie Metriken, um die weitere Diagnose zu erleichtern, eine Lösung oder eine Problemumgehung für das Problem zu finden, wenn eine Grundursache nicht ermittelt werden kann.
- Nutzen Sie die Drilldownfunktionen des Dashboards, oder unterstützen Sie das Anpassen der Ansicht, um sie zu verfeinern.
- Wenn ausführliche Protokolle erforderlich sind, sollten Metriken das Präzisieren der Suchkriterien unterstützen. Wenn die Metriken nicht hilfreich waren, sollten Sie diese für den nächsten Incident verbessern.

Die Übernahme dieses Prinzipienleitfadens kann Ihnen zu Einblicken nahezu in Echtzeit und einem besseren Dienstmanagement verhelfen.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Warnstrategie](./alerting.md)
