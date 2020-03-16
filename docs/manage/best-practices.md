---
title: Einführung in die Betriebsverwaltung
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um sich mit den verschiedenen Übergängen vertraut zu machen, die erfolgen müssen, um die cloudbasierte Betriebsverwaltung zu ermöglichen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d2e6434dc43ae7de4873384901ac73804c3d586d
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092079"
---
# <a name="establish-operational-management-practices-in-the-cloud"></a>Einrichten von Betriebsverwaltungsverfahren in der Cloud

Die Cloudeinführung trägt zum geschäftlichen Nutzen bei. Der tatsächliche geschäftliche Nutzen entsteht jedoch durch einen kontinuierlichen, stabilen Betrieb der in der Cloud bereitgestellten Technologieressourcen. Dieser Abschnitt von Cloud Adoption Framework führt den Leser durch verschiedene Übergänge in die cloudbasierte Betriebsverwaltung.

## <a name="actionable-best-practices"></a>Umsetzbare bewährte Methoden

Moderne Betriebsverwaltungslösungen schaffen eine Multi-Cloud-Sicht auf den Betrieb. Ressourcen, die mit den folgenden Best Practices verwaltet werden, können sich in der Cloud, in einem vorhandenen Rechenzentrum oder sogar bei einem konkurrierenden Cloudanbieter befinden. Derzeit umfasst das Framework zwei bewährte Methoden als Referenz, um die Ausgereiftheit der Betriebsverwaltung in der Cloud zu steuern:

- [Azure-Serververwaltung](./azure-server-management/index.md): Ein Onboardingleitfaden für die Integration der cloudbasierten Tools und Dienste, die zur Verwaltung des Betriebs erforderlich sind.
- [Hybridüberwachung](./monitor/index.md): Viele Kunden haben bereits eine beträchtliche Investition in System Center Operations Manager getätigt. Diesen Kunden kann dieser Leitfaden zur Hybridüberwachung helfen, die cloudnativen Berichtstools mit den Operations Manager-Tools zu vergleichen und gegenüberzustellen. Dieser Vergleich erleichtert die Entscheidung, welche Tools für die Betriebsverwaltung eingesetzt werden sollen.

## <a name="cloud-operations"></a>Cloudvorgänge

Mit beiden bewährten Methoden wird auf eine künftige angestrebte Methodik für die Betriebsverwaltung hingearbeitet, wie in der folgenden Abbildung gezeigt wird:

![Verwalten der Methodik des Frameworks für die Cloudeinführung](../_images/manage/caf-manage.png)

**Geschäftliche Ausrichtung:** In der Verwaltungsmethodik werden alle Workloads nach Wichtigkeit und Geschäftswert klassifiziert. Diese Klassifizierung kann dann durch eine Auswirkungsanalyse gemessen werden, die den mit Leistungseinbußen oder Betriebsunterbrechungen verbundenen Verlustwert berechnet. Mit diesen konkreten Umsatzauswirkungen können Cloudbetriebsteams mit dem Unternehmen zusammenarbeiten, um eine Zusage zu machen, die Kosten und Leistung in Einklang bringt.

**Disziplinen für den Cloudbetrieb:** Nachdem das Unternehmen ausgerichtet wurde, ist es viel einfacher, die richtigen Disziplinen des Cloudbetriebs für die einzelnen Workloads nachzuverfolgen und Berichte dazu zu erstellen. Die Entscheidungen in jeder Disziplin können dann in Zusagebedingungen umgewandelt werden, die für das Unternehmen leicht verständlich sind. Dieser kooperative Ansatz macht den Geschäftsbeteiligten zu einem Partner bei der Suche nach dem richtigen Verhältnis von Kosten und Leistung.

- **Bestand und Transparenz:** Betriebsverwaltung erfordert mindestens ein Mittel zur Bestandsaufnahme von Ressourcen und zur Schaffung von Transparenz über den Ausführungsstatus jeder Ressource.
- **Betriebsbezogene Compliance:** Eine regelmäßige Verwaltung von Konfiguration, Größe, Kosten und Leistung von Ressourcen ist für die Erfüllung der Leistungserwartungen unverzichtbar.
- **Schutz und Wiederherstellung:** Die Minimierung von Betriebsunterbrechungen und die Beschleunigung der Wiederherstellung helfen dem Unternehmen, Leistungsverluste und negative Auswirkungen auf den Umsatz zu vermeiden. Erkennung und Wiederherstellung sind wesentliche Aspekte dieser Disziplin.
- **Plattformbetrieb:** Alle IT-Umgebungen umfassen eine Reihe von gemeinsam genutzten Plattformen. Diese Plattformen können Datenspeicher wie SQL Server oder Azure HDInsight beinhalten. Andere gängige Plattformen sind Containerlösungen wie Azure Kubernetes Service (AKS). Unabhängig von den Plattformen liegt der Schwerpunkt bezüglich des Reifegrads des Plattformbetriebs auf der Anpassung von Vorgängen basierend darauf, wie die gemeinsam genutzten Plattformen bereitgestellt, konfiguriert und durch Workloads genutzt werden.
- **Workloadbetrieb:** Auf der höchsten Stufe der betrieblichen Reife können Cloudbetriebsteams Vorgänge für kritische Workloads optimieren. Bei diesen Workloads können verfügbare Daten zur Automatisierung der Problembehandlung, der Größenanpassung oder des Schutzes von Workloads auf der Grundlage ihrer Auslastung genutzt werden.

Zusätzliche Anleitungen wie der [Entwurf eines Überprüfungsframeworks (Codename: Cloudentwurfsprinzipien)](https://docs.microsoft.com/azure/architecture/framework/resiliency/overview) können dabei helfen, detaillierte architekturbezogene Entscheidungen zu jeder Workload innerhalb der zuvor beschriebenen Disziplinen zu treffen.

Dieser Abschnitt des Cloud Adoption Framework baut auf jedem der vorhergehenden Themen auf, um einen ausgereiften Cloudbetrieb in Ihrem Unternehmen zu fördern.
