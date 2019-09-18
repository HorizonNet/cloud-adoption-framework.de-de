---
title: Einrichten einfacher Warnungen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einrichten einfacher Warnungen
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5b11a97e78d5fcd1b2a2cc866f5a7062bc6a2977
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032044"
---
# <a name="set-up-basic-alerts"></a>Einrichten einfacher Warnungen

Ein wichtiger Faktor bei der Ressourcenverwaltung ist die Benachrichtigung bei auftretenden Problemen. Mit Warnungen werden Sie proaktiv über kritische Zustände benachrichtigt. Sie können auf Triggern von Metriken, Protokollen oder Dienstintegritätsproblemen basieren. Im Rahmen des Onboarding der Azure-Serververwaltungsdienste können Sie Warnungen und Benachrichtigungen einrichten, die Ihnen helfen können, Ihre IT-Teams über alle Probleme auf dem Laufenden zu halten.

## <a name="azure-monitor-alerts"></a>Azure Monitor-Warnungen

Azure Monitor bietet [Warnungsfunktionen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview), um Sie per E-Mail oder Messaging über auftretende Probleme zu informieren. Diese Funktionen basieren auf einer gemeinsamen Datenüberwachungsplattform, die Protokolle und Metriken enthält, die von Ihren Servern und anderen Ressourcen generiert werden. Diese Plattform ermöglicht es Ihnen, Daten aus verschiedenen Ressourcen zu analysieren, indem Sie einen allgemeinen Satz von Tools in Azure Monitor verwenden, mit denen Sie Warnungen auslösen können. Diese Trigger können Folgendes umfassen:

- Metrikwerte
- Protokollsuchabfragen
- Aktivitätsprotokollereignisse
- Integrität der zugrunde liegenden Azure-Plattform
- Tests für die Verfügbarkeit von Websites

In der [Liste der Azure Monitor-Datenquellen](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) finden Sie eine ausführlichere Beschreibung der Quellen von Überwachungsdaten, die von diesem Dienst gesammelt wurden.

Ausführliche Informationen zum manuellen Erstellen und Verwalten von Warnungen über das Portal finden Sie in der [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Automatisierte Bereitstellung empfohlener Warnungen

In diesem Leitfaden wird empfohlen, einen Satz von 15 Warnungen für die Überwachung der grundlegenden Infrastruktur zu aktivieren. Sie finden die Bereitstellungsskripts im [GitHub-Repository – Azure-Warnungstoolkit](https://github.com/Microsoft/manageability-toolkits).

Dieses Paket erstellt Warnungen für wenig freien Speicherplatz, wenig verfügbaren Arbeitsspeicher, hohe CPU-Auslastung, unerwartetes Herunterfahren, beschädigte Dateisysteme und häufige Hardwarefehler. Das Paket verwendet als Beispiel Serverhardware von HP. Sie sollten die Einstellungen in der zugehörigen Konfigurationsdatei so ändern, dass sie Ihrer OEM-Hardware entsprechen. Sie können der Konfigurationsdatei auch weitere Leistungsindikatoren hinzufügen. Führen Sie zum Bereitstellen des Pakets die Datei „New-CoreAlerts.ps1“ aus.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über Abläufe und Sicherheitsmechanismen, die Ihren laufenden Betrieb unterstützen.

> [!div class="nextstepaction"]
> [Kontinuierliche Verwaltung und Sicherheit](./ongoing-management-overview.md)
