---
title: Cloudmigration
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einführung in Inhalte der Cloudmigration
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6bbd3ffe401a3e886ee1f91072a715002ab5e836
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547240"
---
# <a name="cloud-migration-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Cloudmigration im Framework für die Microsoft Cloud-Einführung (Microsoft Cloud Adoption Framework) für Azure

Cloudmigration ist der Prozess der Verschiebung von vorhandenen digitalen Ressourcen in eine Cloudplattform. Bei diesem Ansatz werden vorhandene Ressourcen mit minimalen Veränderungen in der Cloud repliziert. Wenn eine Anwendung oder Workload in der Cloud aktiv ist, werden die Benutzer aus der vorhandenen Lösung in die Cloudlösung übertragen. Die Cloudmigration ist eine Methode zum effektiven Ausgleich des Cloudportfolios. Kurzfristig ist dies häufig der schnellste und agilste Ansatz. Dagegen können mit diesem Ansatz einige der Vorteile der Cloud ohne zusätzliche zukünftige Änderungen nicht genutzt werden. Große und mittelständische Unternehmenskunden nutzen diesen Ansatz, um das Veränderungstempo zu beschleunigen, geplante Kapitalausgaben zu vermeiden und laufende Betriebskosten zu senken.

## <a name="cloud-migration-guidance"></a>Anleitungen zur Cloudmigration

Die Anleitungen in diesem Abschnitt zum Cloud Adoption Framework dienen zwei Zwecken:

- Bereitstellen von umsetzungsfähigen Migrationsleitfäden, die gemeinsame Erfahrungen darstellen, die Kunden häufig machen. Jeder Leitfaden umfasst die Prozesse und Tools, die für eine erfolgreiche Cloudmigration erforderlich sind. Die Designrichtlinien sind zwangsläufig spezifisch für Azure. Alle anderen Empfehlungen in diesen Leitfäden können im Rahmen eines cloudunabhängigen oder Multi-Cloud-Ansatzes angewandt werden.
- Unterstützung der Leser beim Erstellen personalisierter Migrationspläne, die einer Vielzahl von Geschäftsanforderungen gerecht werden können, einschließlich der Migration zu mehreren öffentlichen Clouds, durch detaillierte Anleitungen zur Entwicklung von Prozessen, Rollen und Zuständigkeiten sowie Change Management-Steuerungsprozesse.

Dieser Artikel richtet sich an das Cloudeinführungsteam. Er ist auch für Cloudarchitekten relevant, die eine solide Grundlage für die Cloudmigration entwickeln müssen.

## <a name="intended-audience"></a>Zielpublikum

Die Anleitungen im Cloud Adoption Framework beeinflussen das Geschäft, die Technologie und die Kultur von Unternehmen. Dieser Abschnitt betrifft in erheblichem Maße Anwendungsbesitzer, Change Management-Mitarbeiter (z. B. PMO und agile Managementmitarbeiter), Finanz- und Branchenführer sowie das Cloudeinführungsteam. Zwischen diesen Rollen bestehen verschiedene Abhängigkeiten, die von den Cloudarchitekten anhand dieser Anleitungen unterstützt werden müssen. Die Zusammenarbeit mit diesen Teams kann eine einmalige Aufgabe sein, aber in einigen Fällen wird sie zu wiederkehrenden Interaktionen mit diesen anderen Rollen führen.

Der Cloudarchitekt dient als innovative Führungsperson und Vermittler, um diese Zielgruppen zusammenzubringen. Der Inhalt dieser Sammlung von Anleitungen ist darauf ausgelegt, dem Cloudarchitekten die richtige Kommunikation mit der richtigen Zielgruppe zu erleichtern und die erforderlichen Entscheidungen anzustoßen. Von der Cloud gestützte Unternehmenstransformation hängt von der Rolle des Cloudarchitekten ab, Entscheidungen im gesamten Geschäfts- und IT-Bereich anzuleiten.

**Spezialisierungen des Cloudarchitekten in diesem Abschnitt:** Jeder Abschnitt des Frameworks für die Einführung der Cloud stellt eine andere Spezialisierung oder Variante der Cloudarchitektenrolle dar. Dieser Abschnitt richtet sich an Cloudarchitekten mit Fachkenntnissen in Bezug auf die vorhandene lokale Umgebung und die entsprechenden Auswirkungen auf Migrationsoptionen.

**Aufgabentrennung:** In vielen Unternehmen besteht Aufgabentrennung, um den Zugriff auf Produktionssysteme oder Bereiche der Unternehmensumgebung zu beschränken. In diesem Fall wird der Migrationsprozess komplexer. In einigen Fällen können diese Rollen und Zuständigkeiten erfordern, dass mehrere Cloudarchitekten den gesamten Migrationsprozess abdecken.

**Optionen für Partnerschaften:** In jedem dieser Prozesse lernen die Teams neue Fähigkeiten und Ansätze für die technische Ausführung. Der Ausbau der technischen Fähigkeiten der Teammitglieder ist eine Option bei der Durchführung. Die Einstellung zusätzlicher Mitarbeiter ist eine weitere. Partnerschaften mit Dritten können häufig zu erheblicher Beschleunigung und Risikominderung führen. [Optionen für Partnerschaften](./migration-considerations/assess/partnership-options.md) bietet Entscheidungshilfe bei der Wahl der besten Option.

## <a name="next-steps"></a>Nächste Schritte

Für Leser, die diesem Leitfaden von Anfang bis Ende folgen möchten, tragen diese Inhalte dazu bei, eine Strategie für die robuste Cloudmigration zu entwickeln. Der Leitfaden führt den Leser durch die Theorie und Implementierung einer solchen Strategie.

Es wird empfohlen, dass Leser in einem ersten Schritt den [Leitfaden zur Azure-Migration](./azure-migration-guide/index.md) durcharbeiten, um sich mit den standardmäßigen Tools und Ansätzen für die Migration in einem allgemeinen Anwendungsfall vertraut zu machen. Anschließend können die Basisanleitungen entsprechend den Anforderungen der Leser um [komplexe Migrationsszenarien](./expanded-scope/index.md), [bewährte Methoden für die Azure-Migration](./azure-best-practices/index.md) und [Überlegungen zur Migration](./migration-considerations/index.md) erweitert werden.

> [!div class="nextstepaction"]
> [Leitfaden zur Azure-Migration](./azure-migration-guide/index.md)
