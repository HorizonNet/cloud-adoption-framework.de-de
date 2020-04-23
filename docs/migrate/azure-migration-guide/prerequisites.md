---
title: Voraussetzungen für die Migration zu Azure
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich damit vertraut zu machen, wie Sie sich auf die Azure-Migration vorbereiten und welche Voraussetzungen für ein erfolgreiches Migrationsprojekt erfüllt sein müssen.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: a1c100c4c3c9a960867f0666853df742ecf68c3d
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997582"
---
::: zone target="docs"

# <a name="prerequisites-for-migrating-to-azure"></a>Voraussetzungen für die Migration zu Azure

::: zone-end

::: zone target="chromeless"

# <a name="prerequisites"></a>Voraussetzungen

::: zone-end

Die Ressourcen in diesem Abschnitt helfen Ihnen, die aktuelle Umgebung für die Migration zu Azure vorzubereiten.

# <a name="overview"></a>[Übersicht](#tab/Overview)

Gründe für die Migration zu Azure sind die Beseitigung von Risiken im Zusammenhang mit veralteter Hardware, die Reduzierung der Investitionskosten, die Freigabe von Platz im Datencenter und die schnelle Generierung von Rendite (ROI).

- **Entfernen veralteter Hardware.** Möglicherweise werden in Ihrer Infrastruktur lokal oder bei einem Hostinganbieter Anwendungen gehostet, die sich dem Ende des Lebenszyklus oder des Supports nähern. Die Migration in die Cloud ist eine attraktive Lösung: Durch die Möglichkeit der Migration „in unverändertem Zustand“ kann Ihr Team die Herausforderung, den Infrastrukturlebenszyklus auf dem neuesten Stand zu halten, schnell lösen und sich dann auf die langfristige Planung des Anwendungslebenszyklus und die Optimierung in der Cloud konzentrieren.
- **Ende des Supports für Software.** Möglicherweise verfügen Sie über Anwendungen, die von anderer Software oder von anderen Betriebssystemen abhängen, die sich dem Ende des Supports nähern. Indem Sie zu Azure wechseln, stehen möglicherweise erweiterte Supportoptionen für diese Abhängigkeiten oder andere Migrationsoptionen zur Verfügung, die den Refactoringbedarf für den zukünftigen Support Ihrer Anwendungen minimieren. Ein Beispiel finden Sie in den [erweiterten Supportoptionen für Windows Server 2008 und SQL Server 2008](https://azure.microsoft.com/blog/announcing-new-options-for-sql-server-2008-and-windows-server-2008-end-of-support).
- **Reduzieren der Investitionskosten.** Das Hosting Ihrer eigenen Serverinfrastruktur erfordert erhebliche Investitionen in Hardware, Software, Strom und Personal. Die Migration zu einer Cloudlösung kann zu erheblichen Einsparungen bei den Investitionskosten führen. Um die besten Einsparungen bei den Investitionskosten zu erzielen, ist unter Umständen ein Redesign der Lösung erforderlich. Allerdings ist eine Migration „in unverändertem Zustand“ ein großartiger erster Schritt.
- **Freigabe von Platz im Datencenter.** Vielleicht entscheiden Sie sich für Azure, weil Sie Ihre Datencenterkapazität erweitern möchten. Eine Möglichkeit dazu besteht darin, die Cloud als Erweiterung Ihrer lokalen Funktionen zu nutzen.
- **Schnelle Generierung von Rendite.** Der Einsatz von Cloudlösungen macht das Erzielen hoher Erträge zum Kinderspiel, denn das Abrechnungsmodell bietet einen umfassenden Einblick in die Auslastung und fördert die für attraktive Renditen passende Kultur.

Jedes der oben genannten Szenarien kann der Ausgangspunkt für die Erweiterung Ihres Cloudfootprints mit einer anderen Methodik (erneutes Hosten, Überarbeiten, Neuentwerfen, Neuerstellen oder Ersetzen) sein.

## <a name="migration-characteristics"></a>Migrationsmerkmale

In diesem Leitfaden wird davon ausgegangen, dass Ihr digitaler Bestand vor der Migration hauptsächlich aus einer lokal gehosteten Infrastruktur besteht und gehostete geschäftskritische Anwendungen umfassen kann. Nach dem erfolgreichen Abschluss Ihrer Migration mag sich im Vergleich zur vorherigen lokalen Installation scheinbar gar nichts geändert haben; jetzt aber ist die gesamte Infrastruktur in Cloudressourcen gehostet. Alternativ ist der ideale Datenbestand eine Variante Ihres aktuellen Datenbestands, da er Aspekte Ihrer lokalen Infrastruktur mit Komponenten aufweist, die zur Optimierung und Nutzung der Cloudplattform überarbeitet wurden.

Mit Ihrer Migrationsinitiative möchten Sie die folgenden Ziele umsetzen:

- Beseitigung von Altgeräten am Ende ihrer Lebensdauer.
- Verringerung der Investitionskosten.
- Rendite.

> [!NOTE]
> Ein zusätzlicher Vorteil dieser Migrationsreise ist das zusätzliche Softwaresupportmodell für Windows 2008, Windows 2008 R2 und SQL Server 2008 sowie SQL Server 2008 R2. Weitere Informationen finden Sie unter
>
> - [Windows Server 2008 und Windows Server 2008 R2](https://www.microsoft.com/cloud-platform/windows-server-2008).
> - [SQL Server 2008 und SQL Server 2008 R2](https://www.microsoft.com/sql-server/sql-server-2008).

# <a name="understand-migration-approaches"></a>[Grundlegendes zu Migrationsansätzen](#tab/Approach)

Die für die Migration einer Anwendung zu Azure verwendeten Strategie und Tools hängen weitgehend von Ihren Geschäftsmotivationen, Technologieanforderungen und Zeitplänen sowie einem tiefen Verständnis der tatsächlichen Workloads und der zu migrierenden Ressourcen (Infrastruktur, Apps und Daten) ab.

Analysieren Sie vor der Festlegung Ihrer Cloudmigrationsstrategie potenzielle Anwendungen, um deren Kompatibilität mit Cloudhostingtechnologien zu ermitteln. Verwenden Sie den [Leitfaden zur Wahl von Migrationstools](../../decision-guides/migrate-decision-guide/index.md) im Cloud Adoption Framework als Hilfe beim Einstieg.

Eine IaaS-orientierte Migration, bei der Server (zusammen mit den zugehörigen Anwendungen und Daten) in der Cloud unter Verwendung virtueller Computer (VMs) neu gehostet werden, ist oft der einfachste Ansatz zum Verschieben von Workloads in die Cloud. Bedenken Sie aber, dass das richtige Konfigurieren, Schützen und Warten von VMs im Vergleich zum Verwenden von PaaS-Diensten in Azure weitaus mehr Zeit und IT-Kenntnisse erfordert. Wenn Sie die Nutzung von Azure Virtual Machines in Erwägung ziehen, müssen Sie den fortlaufenden Wartungsaufwand berücksichtigen, der für das Patchen, Aktualisieren oder Verwalten der VM-Umgebung erforderlich ist.

Wenn Sie Workloads für die Migration bewerten, sollten Sie die Anwendungen identifizieren, für die zur Ausführung mit PaaS-Technologien wie dem Azure App Service oder Orchestrators wie dem Azure Kubernetes Service keine wesentlichen Änderungen erforderlich werden. Diese Apps sollten die ersten Kandidaten für Modernisierung und Cloudoptimierung sein.

## <a name="learn-more"></a>Weitere Informationen

- [Entscheidungsleitfaden zur Migration mit dem Framework für die Cloudeinführung (Cloud Adoption Framework)](../../decision-guides/migrate-decision-guide/index.md)
- [Die fünf R der Rationalisierung](../../digital-estate/5-rs-of-rationalization.md)

# <a name="planning-checklist"></a>[Checkliste für die Planung](#tab/Checklist)

Bevor Sie mit einer Migration beginnen, müssen Sie einige Voraussetzungen erfüllen. Die genauen Details dieser Aktivitäten hängen von der zu migrierenden Umgebung ab. Im Allgemeinen gilt die folgende Checkliste:

> [!div class="checklist"]
>
> - **Ermitteln der Beteiligten:** Identifizieren Sie die Schlüsselpersonen, die eine Rolle spielen oder am Ergebnis der Migration beteiligt sind.
> - **Ermitteln wichtiger Meilensteine:** Um den Zeitrahmen für die Migration effizient zu planen, identifizieren Sie wichtige Meilensteine, die zu erfüllen sind.
> - **Ermitteln der Migrationsstrategie:** Bestimmen Sie, welche der fünf Phasen der Rationalisierung Sie verwenden möchten.
> - **Bewerten Ihrer technischen Eignung:** Überprüfen Sie die technische Bereitschaft und Eignung für die Migration, und bestimmen Sie, welche Unterstützung Sie ggf. von externen Partnern oder dem Azure-Support benötigen.
> - **Migrationsplanung:** Führen Sie die detaillierten Bewertungen und Planungsschritte aus, die zur Vorbereitung Ihrer Ressourcen (Infrastruktur, Apps und Daten) sowie der Azure-Infrastruktur für die Migration erforderlich sind.
> - **Testen Ihrer Migration:** Überprüfen Sie Ihren Migrationsplan, indem Sie eine Testmigration mit begrenztem Umfang durchführen.
> - **Migrieren Ihrer Dienste:** Führen Sie die eigentliche Migration aus.
> - **Aufgaben nach der Migration:** Erfahren Sie, welche Schritte nach der Migration Ihrer Umgebung zu Azure erforderlich sind.

Angenommen, Sie wählen einen Rehostingansatz für die Migration, dann sind auch die folgenden Aktivitäten relevant:

> [!div class="checklist"]
>
> - **Governanceausrichtung:** Wurde ein Konsens über die Ausrichtung von Governance und Migrationsgrundlage erzielt?
> - **Netzwerk**: Eine Netzwerkstrategie muss ausgewählt werden, die sich an den Anforderungen der IT-Sicherheit orientiert.
> - **Identität:** Eine Hybrididentitätsstrategie sollte auf die Anforderungen eines Identitätsverwaltungs- und Cloudeinführungsplans ausgerichtet werden.

::: zone target="docs"

<!-- markdownlint-disable MD024 -->

## <a name="learn-more"></a>Weitere Informationen

- [Die fünf R der Rationalisierung](../../digital-estate/5-rs-of-rationalization.md)
- [Entscheidungsleitfaden zur Wahl von Migrationstools](../../decision-guides/migrate-decision-guide/index.md)
- [Planungscheckliste für das Framework für die Cloudeinführung (Cloud Adoption Framework)](../migration-considerations/prerequisites/planning-checklist.md)

::: zone-end
