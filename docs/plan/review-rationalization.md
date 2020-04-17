---
title: Überprüfen der Rationalisierungsentscheidungen
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Rationalisierungsentscheidungen überprüfen und die Kommunikation mit den geschäftlichen Beteiligten erleichtern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 90a6718c028023e1bae101b35fff873dd47e4ab2
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "80427952"
---
# <a name="review-rationalization-decisions"></a>Überprüfen der Rationalisierungsentscheidungen

Während der anfänglichen Phasen der Strategieermittlung und Planung schlagen wir vor, für die digitalen Ressourcen einen Ansatz der [inkrementellen Rationalisierung](../digital-estate/rationalize.md#incremental-rationalization) anzuwenden. Bei diesem Ansatz werden jedoch verschiedene Annahmen zur Entscheidungsfindung herangezogen. Es ist ratsam, diese Entscheidungen durch die für Cloudstrategie und Cloudeinführung zuständigen Teams unter dem Aspekt einer Dokumentation der erweiterten Workloads überprüfen zu lassen. Diese Überprüfung ist außerdem ein guter Zeitpunkt, geschäftliche Stakeholder und den zuständigen Sponsor in Entscheidungen zum zukünftigen Status einzubeziehen.

> [!IMPORTANT]
> Die Rationalisierungsentscheidungen werden während der Bewertungsphase der Migration weiter überprüft. Bei dieser Überprüfung geht es schwerpunktmäßig um eine Bewertung der Rationalisierung aus geschäftlicher Sicht, um die Ressourcen sinnvoll auszurichten.

Greifen Sie bei der Überprüfung von Rationalisierungsentscheidungen auf die folgenden Fragen zurück, um die Kommunikation mit den geschäftlichen Beteiligten zu erleichtern. Die Fragen sind nach der wahrscheinlichen Ausrichtung der Rationalisierung gruppiert.

## <a name="innovation-indicators"></a>Innovationsindikatoren

Wenn die folgenden Fragen nach gemeinsamer Überprüfung mit „Ja“ beantwortet werden, ist die Workload möglicherweise ein besserer Kandidat für Innovationen. Eine solche Workload würde nicht per „Lift & Shift“- oder anhand eines Modernisierungsmodells migriert. Stattdessen würden die Geschäftslogik oder die Datenstrukturen als vollständig neue oder umgestaltete Anwendung neu erstellt. Dieser Ansatz kann arbeitsintensiver und zeitaufwändiger sein. Aber für eine Workload, die bedeutende geschäftliche Umsätze darstellt, ist die Investition gerechtfertigt.

- Sorgen die Anwendungen in dieser Workload für eine Differenzierung im Markt?
- Sind vorgeschlagene oder genehmigte Investitionen geplant, die auf eine Verbesserung des Benutzererlebnisses bei den Anwendungen in dieser Workload abzielen?
- Ermöglichen die Daten in dieser Workload die Bereitstellung neuer Produkt- oder Dienstangebote?
- Sind vorgeschlagene oder genehmigte Investitionen geplant, die auf eine Ausnutzung der mit dieser Workload verknüpften Daten abzielen?
- Können die Auswirkungen der Differenzierung im Markt oder neuer Angebote quantifiziert werden? Falls ja: Rechtfertigt dieser Umsatz die höheren Kosten für Innovationen während der Cloudeinführung?

Die folgenden beiden Fragen können Ihnen dabei helfen, technische Szenarien auf allgemeiner Ebene in die Überprüfung der Rationalisierung einzubeziehen. Wenn eine der beiden Fragen bejaht wird, könnten Möglichkeiten gefunden werden, die durch Innovationen entstehenden Kosten aufzufangen oder zu reduzieren.

- Ändern sich die Datenstrukturen oder die Geschäftslogik während der Cloudeinführung?
- Wird eine vorhandene Pipeline verwendet, um diese Workload in der Produktion bereitzustellen?

Wenn die Antwort auf eine dieser Fragen „Ja“ lautet, sollte das Team erwägen, diese Workload als Innovationskandidaten einzubeziehen. Zumindest sollte das Team diese Workload für eine Architekturüberprüfung kennzeichnen, um Möglichkeiten für eine Modernisierung zu eruieren.

## <a name="migration-indicators"></a>Migrationsindikatoren

Die Migration ist eine schnellere und kostengünstigere Methode zur Einführung der Cloud. Sie nutzt dabei aber keine Möglichkeiten zur Innovation aus. Bevor Sie in Innovationen investieren, beantworten Sie die folgenden Fragen. Sie können Ihnen dabei helfen zu bestimmen, ob ein Migrationsmodell für eine Workload besser anwendbar ist.

- Ist der Quellcode, der in dieser Anwendung verwendet wird, stabil? Gehen Sie davon au, dass der Code während des gesamten Zeitraums dieses Releasezyklus stabil und unverändert bleibt?
- Unterstützt diese Workload zum aktuellen Zeitpunkt Geschäftsprozesse in der Produktion? Ist dies während des gesamten Zeitraums dieses Releasezyklus der Fall?
- Ist die Verbesserung der Stabilität und Leistung dieser Workload ein primäres Ziel für dieses Cloudeinführungsprojekt?
- Ist eine Senkung der mit dieser Workload verbundenen Kosten ein Ziel dieses Projekts?
- Ist die Senkung der operativen Komplexität für diese Workload ein Ziel dieses Projekts?
- Werden Innovationen durch die aktuelle Architektur oder durch IT-Betriebsprozesse begrenzt?

Wenn die Antwort auf eine der oben genannten Fragen „Ja“ lautet, sollten Sie ein Migrationsmodell für diese Workload in Betracht ziehen. Diese Empfehlung gilt auch dann, wenn die Workload ein Kandidat für Innovationen ist.

Geschäftsumsätze können durch Herausforderungen hinsichtlich Komplexität, Kosten, Leistung oder Stabilität im operativen Betrieb beeinträchtigt werden. Mithilfe der Cloud können Sie schnell Verbesserungen im Zusammenhang mit diesen Herausforderungen erzielen. Wo immer möglich, wird empfohlen, den Migrationsansatz zu nutzen, um die Workload zunächst zu stabilisieren. Anschließend können Sie in der stabilen und agilen Cloudumgebung nach Möglichkeiten für Innovationen suchen. Dieser Ansatz sorgt für kurzfristige Ergebnisse und senkt die Kosten, die für die Ausführung von langfristigen Änderungen anfallen.

> [!IMPORTANT]
> Migrationsmodelle umfassen eine inkrementelle Modernisierung. Die Nutzung von PaaS-Architekturen (Platform-as-a-Service) ist ein gängiger Aspekt bei Migrationsaktivitäten. So sind dies auch kleinere Konfigurationsänderungen, die diese Plattformdienste nutzen. Die Grenze der Migration ist als wesentliche Änderung der Geschäftslogik oder der zugrunde liegenden Geschäftsstrukturen definiert. Eine solche Änderung wird als Innovationsaufwand betrachtet.

## <a name="update-the-project-plan"></a>Aktualisieren des Projektplans

Die Kenntnisse und Fähigkeiten, die für ein Migrationsprojekt erforderlich sind, unterscheiden sich von den Kenntnissen und Fähigkeiten, die bei einem Innovationsprojekt benötigt werden. Während der Implementierung eines Cloudeinführungsplans schlagen wir vor, Migrations- und Innovationsprojekte unterschiedlichen Teams zuzuweisen. Jedes Team hat seinen eigenen Iterations-, Release- und Planungsrhythmus. Durch den Einsatz separater Teams erzielen Sie die Flexibilität, die Sie benötigen, um einen einzigen Cloudeinführungsplan auszuführen und gleichzeitig den notwendigen Innovations- und Migrationsprojekten Rechnung zu tragen.

Bei der Verwaltung des Cloudeinführungsplans in Azure DevOps spiegelt sich diese Verwaltung im Ändern des übergeordneten Arbeitselements (Epic) von „Cloudmigration“ zu „Cloudinnovation“ wider. Diese subtile Änderung stellt mit sicher, dass alle am Cloudeinführungsplan Beteiligten schnell die erforderlichen Aufgaben sowie Änderungen an Nachbesserungsaufgaben nachverfolgen können. Diese Nachverfolgung trägt auch dazu bei, die Zuweisungen zu den jeweiligen Cloudeinführungsteams korrekt auszurichten.

Bei umfangreichen und komplexen Einführungsplänen mit mehreren verschiedenen Projekten sollten Sie eine Aktualisierung des Iterationspfads erwägen. Indem der Bereichspfad geändert wird, wird die entsprechende Workload nur dem Team angezeigt, das diesem Bereichspfad zugewiesen ist. Diese Änderung kann dem Cloudeinführungsteam die Arbeit erleichtern, indem die Anzahl der sichtbaren Aufgaben reduziert wird. Sie erhöht aber die Komplexität der Projektmanagementprozesse.

## <a name="next-steps"></a>Nächste Schritte

[Einrichten von Iterationen und Freigabeplänen](./iteration-paths.md), um mit der Planungsarbeit zu beginnen

> [!div class="nextstepaction"]
> [Einrichten von Iterationen und Freigabeplänen](./iteration-paths.md), um mit der Planungsarbeit zu beginnen
