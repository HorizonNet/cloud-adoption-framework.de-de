---
title: Einrichten einfacher Warnungen
description: Es wird beschrieben, wie Sie mit den Azure-Serververwaltungsdiensten Warnungen und Benachrichtigungen einrichten, die Ihnen dabei helfen, Ihre IT-Teams über alle Probleme auf dem Laufenden zu halten.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 3525b8d84ee6dd54072a4fed401114578de7fcb3
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094474"
---
# <a name="set-up-basic-alerts"></a>Einrichten einfacher Warnungen

Ein wichtiger Faktor bei der Ressourcenverwaltung ist die Benachrichtigung bei auftretenden Problemen. Warnungen benachrichtigen Sie auf Basis von Triggern aus Metriken, Protokollen oder auf Dienstintegritätsproblemen proaktiv über kritische Zustände. Im Rahmen des Onboarding der Azure-Serververwaltungsdienste können Sie Warnungen und Benachrichtigungen einrichten, die Ihnen helfen können, Ihre IT-Teams über alle Probleme auf dem Laufenden zu halten.

## <a name="azure-monitor-alerts"></a>Azure Monitor-Warnungen

Azure Monitor bietet [Warnungsfunktionen](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview), um Sie per E-Mail oder Messaging über auftretende Probleme zu informieren. Diese Funktionen basieren auf einer gemeinsamen Datenüberwachungsplattform, die Protokolle und Metriken enthält, die von Ihren Servern und anderen Ressourcen generiert werden. Durch die Verwendung eines allgemeinen Toolsatzes in Azure Monitor können Sie Daten analysieren, die aus mehreren Ressourcen kombiniert wurden, und damit Warnungen auslösen. Diese Trigger können Folgendes umfassen:

- Metrikwerte
- Protokollsuchabfragen
- Aktivitätsprotokollereignisse
- Integrität der zugrunde liegenden Azure-Plattform
- Tests für die Verfügbarkeit von Websites

In der [Liste der Azure Monitor-Datenquellen](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) finden Sie eine ausführlichere Beschreibung der Quellen von Überwachungsdaten, die von diesem Dienst gesammelt wurden.

Ausführliche Informationen zum manuellen Erstellen und Verwalten von Warnungen über das Azure-Portal finden Sie in der [Azure Monitor-Dokumentation](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Automatisierte Bereitstellung empfohlener Warnungen

In diesem Leitfaden wird empfohlen, einen Satz von 15 Warnungen für die Überwachung der grundlegenden Infrastruktur zu erstellen. Sie finden die Bereitstellungsskripts im [GitHub-Repository – Azure-Warnungstoolkit](https://github.com/Microsoft/manageability-toolkits).

Dieses Paket erstellt Warnungen für:

- Wenig freier Speicherplatz
- Wenig verfügbarer Arbeitsspeicher
- Hohe CPU-Auslastung
- Unerwartetes Herunterfahren
- Beschädigte Dateisysteme
- Allgemeine Hardwarefehler

Das Paket verwendet als Beispiel Serverhardware von HP. Ändern Sie die Einstellungen in der zugehörigen Konfigurationsdatei, um Ihre OEM-Hardware widerzuspiegeln. Sie können der Konfigurationsdatei auch weitere Leistungsindikatoren hinzufügen. Führen Sie zum Bereitstellen des Pakets die Datei „New-CoreAlerts.ps1“ aus.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr über Abläufe und Sicherheitsmechanismen, die Ihren laufenden Betrieb unterstützen.

> [!div class="nextstepaction"]
> [Kontinuierliche Verwaltung und Sicherheit](./ongoing-management-overview.md)
