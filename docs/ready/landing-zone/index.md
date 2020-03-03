---
title: Was ist eine Zielzone?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hier finden Sie Informationen zu Landezonen – den Grundbausteinen jeder Cloudeinführungsumgebung.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6db16b50115f2ba145dd4980dc5d57867f438de7
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228358"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-a-landing-zone"></a>Was ist eine Zielzone?

Infrastructure-as-Code ist bei den meisten Cloudeinführungsaufgaben ein natürlicher Übergang. Die Bereitstellung Ihrer ersten Zielzonen in der Cloud ist ein allgemeiner Ausgangspunkt für den Übergang zur Erstellung von Code First-Umgebungen. In diesem Artikel wird der Begriff _Zielzone_ und andere verwandte Begriffe erläutert.

## <a name="landing-zone-definition"></a>Definition der Zielzone

Eine Landezone ist der Grundbaustein jeder Cloudeinführungsumgebung. Der Begriff _Zielzone_ bezieht sich auf ein logisches Konstrukt, das alles erfasst, was „true“ sein muss, um die gewünschte Cloudeinführung zu ermöglichen.

**Bereich:** Eine voll funktionsfähige Zielzone berücksichtigt alle Plattformressourcen, die zur Unterstützung der Anforderungen an eine Cloudeinführung des Kunden erforderlich sind.

**Refactoring:** Bei jeder Iteration der Bereitschaftsmethodik des Frameworks für die Cloudeinführung (Cloud Adoption Framework) wird letztendlich eine voll funktionsfähige Landezone angestrebt. Während jeder Iterationen wird die Codebasis, die die Zielzone definiert, umgestaltet oder erweitert. Nach dem Refactoring kann die Zielzone geändert oder erneut bereitgestellt werden, um neue Anforderungen an die Cloud zu ermöglichen.

**Ziel:** Das Ziel des Zielzonenansatzes besteht darin, einen gemeinsamen Satz einheitlicher Plattformimplementierungen zu erstellen. Diese konsistenten Implementierungen müssen vorhanden sein, um sicherzustellen, dass Ihre Anwendungen bei der Bereitstellung Zugriff auf erforderliche Komponenten haben. Jede Zielzoneniterationen muss entsprechend den Anforderungen des Migrationsplans für die Cloud und der Abonnemententwurfsstrategie entworfen und bereitgestellt werden.

**Grundlegender Zweck:** Der Hauptzweck der Zielzone besteht darin, sicherzustellen, dass die erforderlichen Grundlagen bereits vorhanden sind, wenn eine Anwendung in Azure ausgeführt wird.

## <a name="landing-zone-usage"></a>Nutzung der Zielzone

Bei Zielzonen wird nicht unbedingt zwischen der Einführung von IaaS oder PaaS unterschieden. Allerdings sind Zielzonen speziell für die Unterstützung des Einführungsplans konzipiert, indem die Abonnementstrategie erfüllt wird. Die Unterstützung des Einführungsplans erfordert möglicherweise mehrere Zielzonen mit einer Mischung aus erforderlichen Komponenten.

Zweck und Umfang des Gesamtplans zur Einführung der Cloud bestimmen, welche Grundlagen erforderlich sind. Zusätzliche Anforderungen an Governance, Compliance, Sicherheit und Betriebsverwaltung werden wahrscheinlich den ursprünglichen Umfang der Zielzone erweitern. In frühen Phasen der Einführung können Zielzonen aufgrund von definierten Anforderungen und akzeptablen Risiken weniger Grundlagen umfassen.  Wenn mehrere Zielzonen vorhanden sind, ist es sehr üblich, dass jede Zielzone von Hubs abhängig ist, die die erforderlichen Steuerelemente über ein freigegebenes Dienstmodell bereitstellen.

## <a name="related-terms"></a>Verwandte Begriffe

- **Gemeinsam genutzte Dienste**: Workloads verfügen häufig über gemeinsam genutzte Abhängigkeiten, die von vielen unterschiedlichen Workloads verwendet werden. Der Ansatz der gemeinsam genutzten Dienste verschiebt viele dieser allgemeinen Abhängigkeiten in ein logisches Konstrukt.

- **Hub-and-Spoke-Modell:** Eine Implementierung des Ansatzes der gemeinsam genutzten Dienste ist ein Hub-and-Spoke-Modell. In diesem Modell ist der Hub ein einzelnes logisches Konstrukt für das Hosting aller freigegebenen Dienste. Zielzonen fungieren dann als Spokes, die basierend auf gemeinsamen Abhängigkeiten vom Hub ausgehen.

- **Unabhängige Zielzone:** Einige Ansätze für Zielzonen erfordern nicht ausdrücklich einen dedizierten Hub. Dies tritt am häufigsten auf, wenn alle Produktionsressourcen (Apps, Daten und virtuelle Computer) im Cloudeinführungsplan in einer einzigen Umgebung sicher gehostet, verwaltet und gesteuert werden können.

## <a name="next-steps"></a>Nächste Schritte

Zum Einstieg in die Verwendung von Zielzonen [wählen Sie Ihre erste Zielzone](./first-landing-zone.md).

> [!div class="nextstepaction"]
> [Wählen Ihrer ersten Zielzone](./first-landing-zone.md)
