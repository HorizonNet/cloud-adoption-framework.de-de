---
title: Leitfaden zur Cloudüberwachung
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Übersicht über Azure Monitor und System Center Operations Manager
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 315ba0898f6a301af6f91614290c51244fbf6eb0
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564914"
---
# <a name="cloud-monitoring-guide-introduction"></a>Leitfaden zur Cloudüberwachung: Einführung

Die Cloud hat die Beschaffung und Nutzung von Technologieressourcen durch Unternehmen grundlegend verändert. Früher lagen Besitz und Verantwortung für alle Ebenen der Technologie, von der Infrastruktur bis hin zur Software, beim Unternehmen. Heute bietet die Cloud Unternehmen die Möglichkeit, Ressourcen ganz nach Bedarf bereitzustellen und zu nutzen.

Während die Cloud im Hinblick auf Entwurfsoptionen nahezu unbegrenzte Flexibilität bietet, setzen Unternehmen bei der Einführung von Cloudtechnologien auf eine bewährte und konsistente Methodik. Da jedes Unternehmen unterschiedliche Ziele und Zeitpläne für die Cloudeinführung hat, ist ein allgemeingültiger Ansatz für die Einführung nahezu unmöglich.

![Diagramm der Strategien für die Cloudeinführung](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Diese digitale Transformation bietet auch eine Gelegenheit zur Modernisierung der Infrastruktur, Workloads und Anwendungen. Je nach Geschäftsstrategie und -zielen umfasst die Migration von einem lokalen Standort zum vollständigen Betrieb in der Cloud wahrscheinlich die Einführung eines Hybrid Cloud-Modells. In dieser Phase stehen IT-Teams vor der Herausforderung, schnell einen Mehrwert aus der Cloud zu generieren. Die IT-Teams müssen darüber hinaus wissen, wie die Anwendung oder der Dienst während der Migration zu Azure effektiv überwacht werden kann, und gleichzeitig weiterhin für effektive IT- bzw. DevOps-Prozesse sorgen.

Die betroffenen Teams möchten cloudbasierte SaaS-Tools (Software-as-a-Service) für Überwachung und Verwaltung verwenden. Daher sollten sie genau wissen, was die jeweiligen Dienste und Lösungen leisten, damit sie vollständige Transparenz erzielen und Kosten senken können und sich nicht mehr um die Infrastruktur und Wartung traditioneller softwarebasierter IT-Betriebstools kümmern müssen.

IT-Teams nutzen allerdings häufig lieber die Tools, in die bereits beträchtliche Investitionen getätigt wurden. Diese Herangehensweise unterstützt ihre Dienstvorgangsprozesse, um beide Cloudmodelle überwachen zu können. Das finale Ziel ist ein Übergang zu einem SaaS-basierten Angebot. Die IT bevorzugt diese Herangehensweise nicht nur aufgrund der Planungszeit, der Ressourcen und der Finanzmittel, die für den Wechsel benötigt werden. Es herrscht möglicherweise auch Verwirrung darüber, welche Produkte oder Azure-Dienste sich für den Übergang eignen.

Das Ziel dieses Leitfadens ist die Bereitstellung einer detaillierten Referenz, die IT-Abteilungsleitern von Unternehmen, geschäftlichen Entscheidungsträgern, Anwendungsarchitekten und Anwendungsentwicklern folgende Aspekte nahebringen soll:

* Azure-Überwachungsplattformen mit einer Übersicht und einem Vergleich ihrer Funktionen.
* Die am besten geeignete Lösung für die Überwachung von hybriden und privaten Workloads sowie nativen Azure-Workloads.
* Der empfohlene Ansatz für eine gemeinsame End-to-End-Überwachung von Infrastruktur und Anwendungen. Hierzu gehören praktikable Lösungen für eine Migration dieser gängigen Workloads zu Azure.

Dieser Leitfaden ist keine Anleitung zur Verwendung oder Konfiguration einzelner Azure-Dienste und -Lösungen, er verweist jedoch auf solche Quellen, wenn diese zutreffend oder verfügbar sind. Nach dem Lesen dieses Leitfadens wissen Sie, wie eine Workload unter Verwendung der bewährten Methoden und Muster ordnungsgemäß betrieben wird.

Wenn Sie noch nicht mit Azure Monitor und System Center Operations Manager vertraut sind und sich zunächst über deren spezifische Features und Unterschiede informieren möchten, sehen Sie sich die [Übersicht über unsere Überwachungsplattformen](./platform-overview.md) an.

## <a name="audience"></a>Zielgruppe

Dieser Leitfaden eignet sich insbesondere für Unternehmensadministratoren, Teams in den Bereichen IT-Betrieb, -Sicherheit und -Compliance, Anwendungsarchitekten, Workload-Entwicklungsbesitzer und Workload-Vorgangsbesitzer.

## <a name="how-this-guide-is-structured"></a>Aufbau dieses Leitfadens

Dieser Artikel ist Teil einer Serie. Die folgenden Artikel sollten zusammenhängend und in der richtigen Reihenfolge gelesen werden:

* Einführung (dieser Artikel)
* [Monitoring strategy for cloud deployment models](./cloud-models-monitor-overview.md) (Überwachungsstrategie für Cloudbereitstellungsmodelle)
* [Erfassen der richtigen Daten](./data-collection.md)
* [Warnungen](./alerting.md)

## <a name="products-and-services"></a>Produkte und Dienste

Für die Überwachung und Verwaltung einer Vielzahl von Ressourcen, die in Azure, Ihrem Unternehmensnetzwerk oder von anderen Cloudanbietern gehostet werden, stehen einige Softwarelösungen und Dienste zur Verfügung. Sie lauten wie folgt:

* System Center Operations Manager
* Azure Monitor – enthält jetzt auch Log Analytics und Application Insights
* Azure Policy und Azure Blueprints
* Azure-Automatisierung
* Azure Logic Apps
* Azure Event Hubs

Diese erste Version des Leitfadens behandelt unsere aktuellen Überwachungsplattformen: Azure Monitor und System Center Operations Manager. Außerdem beschreibt er die empfohlene Strategie für die Überwachung der einzelnen Cloudbereitstellungsmodelle. Der Leitfaden enthält außerdem die ersten Überwachungsempfehlungen, beginnend mit Datensammlung und Warnungen.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Monitoring strategy for cloud deployment models](./cloud-models-monitor-overview.md) (Überwachungsstrategie für Cloudbereitstellungsmodelle)
