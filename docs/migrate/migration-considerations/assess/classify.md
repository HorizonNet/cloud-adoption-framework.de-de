---
title: Workloadklassifizierung vor der Migration
description: Klassifizieren Sie Ihre Workloads während einer Bewertung, die vor der Migration durchgeführt wird.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/03/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8f912891bf90d0ecef29727d7d7a067d442234fc
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79095390"
---
# <a name="workload-classification-before-migration"></a>Workloadklassifizierung vor der Migration

Bei jeder Iteration des Migrationsprozesses wird mindestens eine Workload migriert und für die Produktion bereitgestellt. Vor diesen Migrationsaktivitäten ist es jeweils wichtig, jede Workload zu klassifizieren. Die Klassifizierung trägt dazu bei, die Anforderungen in Bezug auf Governance, Sicherheit, Betrieb und Datenverwaltung zu verdeutlichen.

Die folgende Anleitung ist eine Erweiterung der empfohlenen Markierungsanforderungen, die im [Artikel zu den Standards für Benennung und Markierung](../../../ready/azure-best-practices/naming-and-tagging.md#metadata-tags) beschrieben sind, indem wichtige [Vorgänge](../../../manage/considerations/criticality.md#criticality-scale) und [Governance](../../../govern/guides/complex/prescriptive-guidance.md#resource-tagging)-Elemente hinzugefügt werden.

In diesem Artikel empfehlen wir Ihnen, Ihre vorhandenen Markierungsstandards um die Bereiche „Wichtigkeit“ und „Vertraulichkeit der Daten“ zu erweitern. Anhand dieser Datenpunkte können andere Teams besser verstehen, für welche Workloads ggf. zusätzliche Aufmerksamkeit oder mehr Support benötigt wird.

## <a name="data-sensitivity"></a>Vertraulichkeit der Daten

Wie im Artikel zur [Datenklassifizierung](../../../govern/policy-compliance/data-classification.md) beschrieben ist, werden bei der Datenklassifizierung die Auswirkungen gemessen, die bei einem Datenleck für das Unternehmen oder seine Kunden entstehen würden. Die Teams für Governance und Sicherheit nutzen die Datenvertraulichkeit bzw. die Datenklassifizierung als Indikator für Sicherheitsrisiken. Während der Bewertung sollte das Cloudeinführungsteam die Datenklassifizierung für jede Workload evaluieren, die für die Migration bestimmt ist, und diese Klassifizierungsinformationen den Unterstützungsteams zur Verfügung stellen. Workloads, bei denen es strikt um „öffentliche Daten“ geht, haben ggf. keinerlei Auswirkung auf Unterstützungsteams. Wenn es um Daten aus dem Bereich „Streng vertraulich“ geht, haben sowohl Governance- als auch Sicherheitsteams meist ein berechtigtes Interesse daran, an der Bewertung der Workload beteiligt zu werden.

Arbeiten Sie zu einem möglichst frühen Zeitpunkt mit Ihren Teams für die Sicherheit und Governance zusammen, um Folgendes zu definieren:

- Eindeutiger Prozess zum Verteilen von Workloads des Backlogs mit vertraulichen Daten
- Kenntnis der erforderlichen Governanceanforderungen und Sicherheitsbaseline für unterschiedliche Vertraulichkeitsebenen von Daten
- Mögliche Auswirkungen der Vertraulichkeit von Daten auf Anforderungen in Bezug auf Abonnemententwurf, Verwaltungsgruppenhierarchien oder Zielzone
- Alle Anforderungen zum Testen der Datenklassifizierung, ggf. mit spezifischen Tools oder definiertem Klassifizierungsbereich

## <a name="mission-criticality"></a>Kritikalität

Wie im Artikel zur [Wichtigkeit von Workloads](../../../manage/considerations/criticality.md) beschrieben, ist die Wichtigkeit (Kritikalität) einer Workload ein Maß dafür, wie stark die Auswirkungen für ein Unternehmen bei einem entsprechenden Ausfall sind. Mit diesem Datenpunkt können Betriebsverwaltungs- und Sicherheitsteams Risiken zu Ausfällen und Sicherheitsverletzungen evaluieren. Während der Bewertung sollte das Cloudeinführungsteam für jede Workload, die für die Migration bestimmt ist, die „Kritikalität“ für das Unternehmen evaluieren und diese Klassifizierungsinformationen den Unterstützungsteams zur Verfügung stellen. Bei Workloads vom Typ „Niedrig“ oder „“Nicht unterstützt“ ergeben sich meist nur geringe Auswirkungen auf die Unterstützungsteams. Wenn es aber um Workloads vom Typ „Unternehmenskritisch“ oder „Kritisch für Geschäftseinheit“ geht, sind die betriebsbezogenen Abhängigkeiten stärker ausgeprägt.

Arbeiten Sie zu einem möglichst frühen Zeitpunkt mit Ihren Teams für die Sicherheit und den Betrieb zusammen, um Folgendes zu definieren:

- Eindeutiger Prozess zum Verteilen von Workloads des Backlogs mit Supportanforderungen
- Kenntnis der Anforderungen an Betriebsverwaltung und Ressourcenkonsistenz für unterschiedliche Kritikalitätsebenen
- Mögliche Auswirkungen der Kritikalität auf Anforderungen in Bezug auf Abonnemententwurf, Verwaltungsgruppenhierarchien oder Zielzone
- Anforderungen in Bezug auf die Dokumentation der Kritikalität, z. B. spezifische Datenverkehrs- oder Nutzungsberichte, Finanzanalysen oder andere Tools

## <a name="next-steps"></a>Nächste Schritte

Nachdem Workloads richtig klassifiziert wurden, ist es deutlich einfacher, die [geschäftlichen Prioritäten aufeinander auszurichten](./business-priorities.md).

> [!div class="nextstepaction"]
> [Ausrichten von geschäftlichen Prioritäten](./business-priorities.md)
