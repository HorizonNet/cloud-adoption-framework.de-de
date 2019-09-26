---
title: Einführung in die Betriebsverwaltung
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Grundlegendes zur Betriebsverwaltung im Framework für die Cloudeinführung (Cloud Adoption Framework)
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: manage
ms.openlocfilehash: 96f87583f50783fa0c6a8c947aa8b34ae440fc95
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221441"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Einrichten von Betriebsverwaltungsverfahren in der Cloud

Die Cloudeinführung trägt zum geschäftlichen Nutzen bei. Der tatsächliche geschäftliche Nutzen entsteht jedoch durch einen kontinuierlichen, stabilen Betrieb der in der Cloud bereitgestellten Technologieressourcen. Dieser Abschnitt des Frameworks für die Cloudeinführung führt den Leser durch verschiedene Übergänge in die cloudbasierte Betriebsverwaltung.

## <a name="actionable-best-practices"></a>Umsetzbare bewährte Methoden

Moderne Betriebsverwaltungslösungen bieten eine Multi-Cloud-Sicht auf den Betrieb. Ressourcen, die mit den folgenden empfohlenen Methoden verwaltet werden, können sich in der Cloud, in einem vorhandenen Datencenter oder sogar bei einem konkurrierenden Cloudanbieter befinden. Derzeit umfasst das Framework zwei empfohlene Referenzmethoden, um die Betriebsverwaltung in der Cloud zu verbessern:

- [Azure-Serververwaltung](./azure-server-management/index.md): Onboardingleitfaden für die Integration der cloudbasierten Tools und Dienste, die zur Verwaltung des Betriebs erforderlich sind.
- [Hybridüberwachung](./monitor/index.md): Viele Kunden haben bereits eine beträchtliche Investition in System Center Operations Manager getätigt. Diesen Kunden hilft dieser Leitfaden zur Hybridüberwachung, die cloudnativen Berichtstools mit den Operations Manager-Tools zu vergleichen und gegenüberzustellen. Dieser Vergleich erleichtert die Entscheidung, welche Tools für die Betriebsverwaltung eingesetzt werden sollen.

## <a name="cloud-operations"></a>Cloudvorgänge

Mit beiden Best Practices wird auf eine künftige angestrebte Methodik für die Betriebsverwaltung hingearbeitet.

![CAF-Verwaltungsmethodik](../_images/manage/caf-manage.png)

**Geschäftliche Ausrichtung:** In der Verwaltungsmethodik werden alle Workloads nach Wichtigkeit und Geschäftswert klassifiziert. Diese Klassifizierung kann dann durch eine Auswirkungsanalyse gemessen werden, die den mit Leistungseinbußen oder Betriebsunterbrechungen verbundenen Verlustwert berechnet. Mit diesen konkreten Umsatzauswirkungen können Cloudbetriebsteams mit dem Unternehmen zusammenarbeiten, um eine Zusage zu machen, die Kosten und Leistung in Einklang bringt.

**Disziplinen für den Cloudbetrieb:** Sobald das Unternehmen ausgerichtet ist, ist es viel einfacher, die richtigen Disziplinen des Cloudbetriebs für die einzelnen Workloads nachzuverfolgen und Berichte dazu zu erstellen. Entscheidungen im Zusammenhang mit den einzelnen Disziplinen können in Verpflichtungen resultieren, die für das Unternehmen gut verständlich sind. Dieser kooperative Ansatz macht den Geschäftsbeteiligten zu einem Partner bei der Suche nach dem richtigen Verhältnis zwischen Kosten und Leistung.

- **Bestand und Transparenz:** Eine Betriebsverwaltung benötigt mindestens eine Möglichkeit zur Bestandsaufnahme von Ressourcen sowie zur Schaffung von Transparenz im Hinblick auf den Ausführungszustand der einzelnen Ressourcen.
- **Betriebsbezogene Compliance:** Eine regelmäßige Verwaltung von Konfiguration, Größe, Kosten und Leistung von Ressourcen ist für die Erfüllung der Leistungserwartungen unverzichtbar.
- **Schutz und Wiederherstellung:** Die Minimierung von Betriebsunterbrechungen und die Beschleunigung der Wiederherstellung tragen dazu bei, Leistungsverluste und Umsatzauswirkungen zu vermeiden. Erkennung und Wiederherstellung sind wesentliche Aspekte dieser Disziplin.
- **Plattformbetrieb:** Alle IT-Umgebungen umfassen eine Reihe von gemeinsam genutzten Plattformen. Diese Plattformen können Datenspeicher wie SQL Server oder HDInsight beinhalten. Andere gängige Plattformen sind Containerlösungen wie Kubernetes oder AKS. Unabhängig von den Plattformen liegt der Schwerpunkt bezüglich des Reifegrads des Plattformbetriebs auf der Anpassung von Vorgängen basierend darauf, wie diese gemeinsam genutzten Plattformen bereitgestellt, konfiguriert und durch Workloads genutzt werden.
- **Workloadbetrieb:** Auf der höchsten Stufe der betrieblichen Reife haben Cloudbetriebsteams die Möglichkeit, den Betrieb auf Workloads abzustimmen, die für den geschäftlichen Erfolg entscheidend sind. Bei diesen kritischen Workloads können verfügbare Daten zur Automatisierung der Problembehandlung, der Größenanpassung oder des Schutzes von Workloads auf der Grundlage ihrer Auslastung genutzt werden.

Zusätzliche Anleitungen wie der [Entwurf eines Überprüfungsframeworks (Codename: Cloudentwurfsprinzipien)](https://docs.microsoft.com/azure/architecture/reliability) können dabei helfen, detaillierte architekturbezogene Entscheidungen zu jeder Workload innerhalb der oben genannten Disziplinen zu treffen.

Dieser Abschnitt des Frameworks für die Cloudeinführung baut auf diesen Themen auf, um den Cloudbetrieb in Ihrem Unternehmen zu verbessern.
