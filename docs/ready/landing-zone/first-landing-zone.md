---
title: Überlegungen zu Landezonen in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Hier finden Sie Informationen zu Landezonen – den Grundbausteinen jeder Cloudeinführungsumgebung.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b451ec6f58a684bd4fb5998f1915dc79761b7a44
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228585"
---
# <a name="first-landing-zone"></a>Erste Landezone

Infrastructure-as-Code ist bei den meisten Cloudeinführungsaufgaben ein natürlicher Übergang. Die Bereitstellung Ihrer ersten Zielzonen in der Cloud ist ein allgemeiner Ausgangspunkt für den Wechsel in eine codegesteuerte Umgebung. Dieser Artikel hilft Ihnen dabei, den Begriff _Zielzone_ zu verstehen und zu entscheiden, welche Zielzone für Ihre derzeitigen Anforderungen in Bezug auf die Einführung am besten geeignet ist.

## <a name="code-first-approach-to-landing-zones"></a>Code First-Ansatz für Zielzonen

Die folgende Abbildung zeigt verschiedene Optionen für Zielzonen. Die folgenden Optionen helfen Ihnen dabei, jetzt die richtige Zielzone für sich auszuwählen. Außerdem können Sie hiermit eine Vision für Ihre zukünftigen Anforderungen an Zielzonen entwickeln.

![Optionen für Zielzonen](../../_images/ready/landing-zone-options.png)

A. Beginnen Sie mit Code, um konsistente, wiederholbare Zielzonen zu entwickeln. Wenn Sie das Refactoring (oder dem Optimieren des Codes und der Infrastruktur) während des Lernens umsetzen möchten, beginnen Sie mit einer einfachen Codebasis, wie z. B. der Migrationszielzonen-Blaupause von Cloud Adoption Framework. Diese Vorgehensweise beschleunigt eine erfolgreiche Einführung und schafft praktische Lernmöglichkeiten. Diese Art von anfänglicher Zielzone ist jedoch nicht für vertrauliche Daten oder unternehmenskritische Workloads ohne zusätzliches Refactoring konzipiert.

B. Wenn die Akzeptanz zunimmt und die Anforderungen deutlicher identifiziert werden, werden die für die Einführung und die Plattform zuständigen Teams die Zielzonen ausgehend von ihren Erfahrungen umgestalten. Durch die Erweiterung Ihrer Zielzonen werden Umgebungen für komplexere Compliance- oder Architekturanforderungen vorbereitet. Unter [Erweitern der Zielzone](../considerations/index.md) finden Sie Entscheidungshilfen und Links zu bewährten Methoden zur Umgestaltung. Das Erweitern der Zielzone kann bei der Erfüllung von Sicherheits-, Betriebs- und Governanceanforderungen hilfreich sein.

C. Einige Cloudeinführungspläne unterliegen externen Complianceanforderungen. Damit Sie diese einfacher einhalten können, stellt Azure Ihnen einige beispielhafte Azure Blueprints bereit. Einige davon können zu Ihrer ersten Blaupause hinzugefügt werden. Andere enthalten eine bestimmte Implementierung, die als erste Zielzone fungieren kann.

D: Wenn ein Partner kontinuierlich verwaltete Dienste bereitstellt oder vertragliche Verpflichtungen in Bezug auf den Einführungsplan hat, stellt er in der Regel eine eigene Zielzone bereit. Die Verwendung einer Partnerzielzone könnte die Einführung beschleunigen und konsistente Anforderungen an die Betriebsverwaltung gewährleisten. Beachten Sie jedoch die internen Governance- und Sicherheitsanforderungen, um die Ausrichtung sicherzustellen.

E. Einführungsteams mit dem mittelfristigen Ziel (innerhalb von 24 Monaten), **mehr als 1.000 Ressourcen (App-, Infrastruktur- oder Datenressourcen) in der Cloud zu hosten**, finden in NorthStar von Cloud Adoption Framework eine Hilfe für die Plattformarchitektur und Zielzonen. NorthStar ist eine erweiterte Roadmap, die auch die Zielstatus-Plattformarchitektur und Referenzimplementierungen umfasst. Diese Roadmap beinhaltet Aspekte paralleler Methoden, einschließlich Governance und Betrieb, damit Sie sich besser auf eine unternehmenskritische, sichere, komplexe und compliancegesteuerte Einführung vorbereiten können.

## <a name="choosing-a-first-landing-zone"></a>Auswählen Ihrer ersten Zielzone

Die Auswahl der ersten Zielzone hängt von einer Reihe von Variablen ab. In der folgenden Übersicht werden einige Optionen für die ersten Zielzonen zusammen mit Variablen erfasst, die die Entscheidung möglicherweise steuern.

| Zielzone                                 | Erfahrung mit der Cloud  | Skalieren             | Ermittlungszeit | Produktionsbereit | Hybrid             | Sensible Daten     | Unternehmenskritisch   | Kompatibilität         |
|----------------------------------------------|-------------------|-------------------|----------------|------------------|--------------------|--------------------|--------------------|--------------------|
| [CAF-Migration](./migrate-landing-zone.md)     | Cloud-Einsteiger      | < 1.000 Ressourcen    | 1 bis 5 Tage    | Begrenzter Umfang -> | Erweiterung erforderlich | Erweiterung erforderlich | Erweiterung erforderlich | Erweiterung erforderlich |
| [CAF-Terraform](./terraform-landing-zone.md) | Verschiedene Vorlagen | Verschiedene Vorlagen | 10 bis 20 Wochen | Begrenzter Umfang -> | Module verfügbar  | Module verfügbar  | Module verfügbar  | Module verfügbar  |

In der folgenden Tabelle werden die gleichen Zielzonen aus einer etwas anderen Perspektive angezeigt, um technische Entscheidungsprozesse zu unterstützen.

| Zielzone                                 | Hub                          | Spoke    | Cloudmodell | Technologie      |
|----------------------------------------------|------------------------------|----------|-------------|-----------------|--|--|--|
| [CAF-Migration](./migrate-landing-zone.md)     | Refactoring erforderlich            | Enthalten | Nur Azure  | Azure Blueprint |
| [CAF-Terraform](./terraform-landing-zone.md) | Im NorthStar-Modul enthalten | Enthalten | Verwenden mehrerer Clouds  | Terraform       |

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie immer noch nicht sicher sind, welche erste Zielzone Sie auswählen sollen, empfehlen wir Ihnen, mit der [Migrationszielzonen-Blaupause von CAF](./migrate-landing-zone.md) zu beginnen.

> [!div class="nextstepaction"]
> [Migrationszielzonen-Blaupause von CAF](./migrate-landing-zone.md)
