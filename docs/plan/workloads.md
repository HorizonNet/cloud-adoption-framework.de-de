---
title: Priorisierung und Definition von Workloads für die Cloudeinführung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um zu erfahren, wie Sie Workloads für einen Cloudeinführungsplan priorisieren und definieren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 9f374bbe149e132fde4c44a8c0ecd9246615bac0
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140619"
---
# <a name="prioritize-and-define-workloads-for-a-cloud-adoption-plan"></a>Priorisierung und Definition von Workloads für einen Cloudeinführungsplan

Die Festlegung klarer, umsetzbarer Prioritäten ist eines der Geheimnisse einer erfolgreichen Cloudeinführung. Die Versuchung ist groß, Zeit in die Definition aller Workloads zu investieren, die bei der Cloudeinführung möglicherweise beeinflusst werden könnten. Diese Vorgehensweise ist jedoch vor allem in der frühen Phase des Einführungsprozesses kontraproduktiv.

Stattdessen empfehlen wir, dass sich Ihr Team darauf konzentriert, die ersten 10 Workloads gründlich zu priorisieren und zu dokumentieren. Nachdem die Implementierung des Einführungsplans begonnen hat, kann das Team eine Liste der nächsten 10 Workloads mit höchster Priorität führen. Dieser Ansatz bietet genügend Informationen, um für die nächsten Iterationen zu planen.

Die Beschränkung des Plans auf 10 Workloads fördert die Flexibilität und die Ausrichtung der Priorisierung als Änderung der Geschäftskriterien. Dieser Ansatz lässt dem Cloudeinführungsteam auch Spielraum, um das Einschätzen zu lernen und zu verfeinern. Aber vor allem macht er eine aufwändige Planung als Hindernis für einen effektiven Geschäftswandel überflüssig.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-workload"></a>Was ist eine Workload?

Im Rahmen einer Cloudeinführung ist eine Workload eine Sammlung von IT-Ressourcen (Server, VMs, Anwendungen, Daten oder Appliances), die gemeinsam einen definierten Prozess unterstützen. Workloads können mehrere Prozesse unterstützen. Workloads können auch von anderen freigegebenen Ressourcen oder größeren Plattformen abhängen. Allerdings sollten die Grenzen einer Workload bezüglich der abhängigen Ressourcen und der von der Workload abhängigen Prozesse klar definiert sein. Häufig können Workloads durch Überwachung des Netzwerkdatenverkehrs zwischen IT-Ressourcen visualisiert werden.

## <a name="prerequisites"></a>Voraussetzungen

Die strategischen Eingaben aus der Liste der Voraussetzungen erleichtern die Erledigung der folgenden Aufgaben wesentlich. Hilfe bei der Zusammenstellung der Daten, die in diesem Artikel besprochen werden, finden Sie unter [Voraussetzungen](./prerequisites.md).

## <a name="initial-workload-prioritization"></a>Anfängliche Workloadpriorisierung

Während des Prozesses der [inkrementellen Rationalisierung](../digital-estate/rationalize.md) sollte sich Ihr Team auf einen 10er-Ansatz, d. h. auf 10 Prioritätsworkloads einigen. Diese Workloads dienen als anfängliche Grenze für die Einführungsplanung.

Wenn die Entscheidung gegen eine Rationalisierung der digitalen Ressourcen fällt, sollten Cloudeinführungsteams und Cloudstrategieteam sich auf eine Liste von zehn Anwendungen einigen, die als erster Schwerpunkt der Migration dienen. Außerdem sollten diese 10 Workloads eine Mischung aus einfachen Workloads (weniger als 10 Ressourcen in einer eigenständigen Bereitstellung) und komplexeren Workloads darstellen. Mit diesen 10 Workloads beginnt die Workloadpriorisierung.

> [!NOTE]
> Der 10er-Ansatz dient als erste Grenze für die Planung zur Konzentration von Energie und Investitionen in der Frühphasenanalyse. Die Analyse und Definition von Workloads führt jedoch wahrscheinlich zu Änderungen in der Liste der Prioritätsworkloads.

## <a name="add-workloads-to-your-cloud-adoption-plan"></a>Hinzufügen von Workloads zu Ihrem Cloudeinführungsplan

Im vorherigen Artikel, [Cloudeinführungsplan und Azure DevOps](./template.md), haben Sie einen Cloudeinführungsplan in Azure DevOps erstellt.

Die Workloads in der Liste des 10er-Ansatzes können jetzt in Ihrem Cloudeinführungsplan dargestellt werden. Die einfachste Möglichkeit hierzu ist die Massenbearbeitung in Microsoft Excel. Um Ihre Arbeitsstation für die Massenbearbeitung vorzubereiten, lesen Sie [Massenhinzufügen oder -bearbeiten von Arbeitselementen mit Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

In Schritt 5 dieses Artikels werden Sie angewiesen, **Eingabeliste** auszuwählen. Wählen Sie stattdessen **Abfrageliste** aus. Wählen Sie dann aus der Dropdownlist **Abfrage auswählen** die Abfrage **Workloadvorlage** aus. Diese Abfrage lädt alle Arbeitselemente im Zusammenhang mit der Migration eines einzelnen Workloads in Ihre Tabellenkalkulation.

Sobald die Arbeitselemente der Workloadvorlage geladen sind, können Sie beginnen, mit diesen Schritten neue Workloads hinzuzufügen:

1. Kopieren Sie alle Elemente mit dem Tag **Workloadvorlage** aus der Spalte ganz rechts.
2. Fügen Sie die kopierten Zeilen unterhalb des letzten Zeilenelements in die Tabelle ein.
3. Ändern Sie die Titelzelle für das neue Feature von **Workloadvorlage** in den Namen des neuen Workloads.
4. Fügen Sie die neue Workloadnamenszelle in die Tagspalte für alle Zeilen unterhalb des neuen Features ein. Achten Sie darauf, dass Sie die Tags oder den Namen der Zeilen, die sich auf das eigentliche **Workloadvorlage**-Feature beziehen, nicht ändern. Sie benötigen diese Arbeitselemente, wenn Sie die nächste Workload dem Cloudeinführungsplan hinzufügen.
5. Fahren Sie mit Schritt 8 in den Anweisungen zur Massenbearbeitung zum Veröffentlichen der Tabellenkalkulation fort. In diesem Schritt werden alle Arbeitselemente erstellt, die für die Migration Ihres Workloads erforderlich sind.

Wiederholen Sie die Schritte 1 bis5 für jeden Workload in der 10er-Ansatz-Liste.

## <a name="define-workloads"></a>Definieren von Workloads

Nachdem die anfänglichen Prioritäten definiert und die Workloads dem Plan hinzugefügt sind, kann jede dieser Workloads durch eine tiefere qualitative Analyse definiert werden. Bevor Sie einen Workload in den Cloudeinführungsplan aufnehmen, versuchen Sie, die folgenden Datenpunkte für jede Workload bereitzustellen.

### <a name="business-inputs"></a>Geschäftseingaben

| Datenpunkt | BESCHREIBUNG | Eingabe |
|---|---|---|
| Workloadname | Wie wird diese Workload genannt? |         |
| Workloadbeschreibung | Aufgabe der Workload in einem Satz |         |
| Motivationen für den Wechsel in die Cloud | Welche Cloudeinführungsmotive betrifft diese Workload? |         |
| Primärer Sponsor | Wer von den betroffenen Beteiligten ist der primäre Sponsor, der die zuvor genannten Motive anfordert? |         |
| Geschäftseinheit | Welche Geschäftseinheit ist für die Kosten dieser Workload verantwortlich? |         |
| Geschäftsprozesse | Welche Geschäftsprozesse werden von Änderungen dieser Workload betroffen sein? |         |
| Unternehmensteams | Welche Unternehmensteams werden von geschäftlichen Änderungen betroffen sein? |         |
| Beteiligte im Unternehmen | Gibt es Führungskräfte, deren Bereich von Änderungen betroffen sein wird? |         |
| Geschäftsergebnisse | Wie wird das Unternehmen den Erfolg dieser Maßnahme messen? |         |
| Metriken | Welche Metriken werden zum Nachverfolgen des Erfolgs verwendet? |         |
| Kompatibilität | Gibt es Complianceanforderungen von Drittanbietern für diese Workload? |         |
| Anwendungsbesitzer | Wer ist verantwortlich für die geschäftlichen Auswirkungen von Anwendungen, die dieser Workload zugeordnet sind? |         |
| Vom Unternehmen ausgeschlossene Zeiträume | Lässt das Unternehmen zu bestimmten Zeiten keine Änderung zu? |         |
| Geografische Regionen | Sind bestimmte geografische Regionen von diesem Workload betroffen? |         |

### <a name="technical-inputs"></a>Technische Eingaben

| Datenpunkt | BESCHREIBUNG | Eingabe |
|---|---|---|
| Einführungsansatz | Ist diese Einführung ein Kandidat für Migration oder Innovation? |         |
| Für die Anwendung Verantwortliche | Listen Sie die für Leistung und Verfügbarkeit dieses Workloads verantwortlichen Parteien auf. |         |
| SLAs | Listen Sie alle Vereinbarungen zum Servicelevel (RTO/RPO-Anforderungen) auf. |         |
| Wichtigkeit | Listen Sie die Wichtigkeit der aktuellen Anwendung auf. |         |
| Datenklassifizierung | Listen Sie die Klassifizierung der Vertraulichkeit der Daten auf. |         |
| Geografische Betriebsregionen | Listen Sie alle geografischen Regionen auf, in denen die Workload gehostet wird oder gehostet werden soll. |         |
| Anwendungen | Geben Sie eine Anfangsliste oder die Anzahl der Anwendungen an, die in dieser Workload enthalten sind. |         |
| VMs | Geben Sie eine Anfangsliste oder die Anzahl von VMs oder Servern an, die in der Workload enthalten sind. |         |
| Datenquellen | Geben Sie eine Anfangsliste oder eine Anzahl von Datenquellen an, die in der Workload enthalten sind. |         |
| Abhängigkeiten | Listen Sie alle Ressourcenabhängigkeiten auf, die nicht in der Workload enthalten sind. |         |
| Geografische Benutzerdatenverkehrs-Regionen | Listen Sie geografische Regionen auf, in denen in signifikantem Maße Benutzerdatenverkehr auftritt. |         |

## <a name="confirm-priorities"></a>Prioritäten bestätigen

Basierend auf den zusammengetragenen Daten sollten sich das Cloudstrategieteam und das Cloudeinführungsteam treffen, um die Prioritäten neu zu bewerten. Die Klärung von Geschäftsdatenpunkte fordert möglicherweise einen Wechsel der Prioritäten. Technische Komplexität oder Abhängigkeiten können zu Änderungen in Bezug auf Besetzungszuordnungen, Zeitpläne oder Abfolge technischer Maßnahmen führen.

Nach einer Überprüfung sollten beide Teams mühelos die daraus resultierenden Prioritäten bestätigen können. Dieser Satz von dokumentierten, überprüften und bestätigten Prioritäten ist der priorisierte Cloudeinführungsrückstand.

## <a name="next-steps"></a>Nächste Schritte

Für jede Workload im priorisierten Cloudeinführungsrückstand ist das Team nun bereit, [Ressourcen auszurichten](./assets.md).

> [!div class="nextstepaction"]
> [Ausrichten von Ressourcen für priorisierte Workloads](./assets.md)
