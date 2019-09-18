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
ms.openlocfilehash: 3abc103e09a11af4cb822dde985b96c56bca6242
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026057"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Einrichten von Betriebsverwaltungsverfahren in der Cloud

Die Cloudeinführung ist ein Katalysator für das Steigern des geschäftlichen Nutzens. Der tatsächliche Geschäftswert wird jedoch durch den laufenden, stabilen Betrieb der in der Cloud eingesetzten Technologieressourcen realisiert. Dieser Abschnitt des Cloud Adoption Framework führt den Leser durch verschiedene Übergänge in die cloudbasierte Betriebsverwaltung.

## <a name="actionable-best-practices"></a>Umsetzbare Best Practices

Moderne Betriebsverwaltunglösungen schaffen eine Multi-Cloud-Sicht auf den Betrieb. Ressourcen, die mit den folgenden Best Practices verwaltet werden, können sich in der Cloud, in einem vorhandenen Rechenzentrum oder sogar bei einem konkurrierenden Cloudanbieter befinden. Derzeit umfasst das Framework zwei Best Practices als Referenz, um die Ausgereiftheit der Betriebsverwaltung in der Cloud zu steuern:

* [Azure-Serververwaltung](./azure-server-management/index.md): Onboarding-Leitfaden zur Integration der cloudbasierten Tools und Dienste, die zur Verwaltung des Betriebs erforderlich sind.
* [Hybridüberwachung](./monitor/index.md): Viele Kunden haben bereits eine beträchtliche Investition in System Center Operations Manager getätigt. Diesen Kunden hilft dieser Leitfaden zur Hybridüberwachung, die cloudnativen Berichtstools mit den Operations Manager-Tools zu vergleichen und gegenüberzustellen. Dieser Vergleich erleichtert die Entscheidung, welche Tools für die Betriebsverwaltung eingesetzt werden sollen.

## <a name="cloud-operations"></a>Cloudbetrieb

Mit beiden Best Practices wird auf eine künftige angestrebte Methodik für die Betriebsverwaltung hingearbeitet.

![CAF-Verwaltungsmethodik](../_images/manage/caf-manage.png)

**Geschäftliche Ausrichtung:** In der Verwaltungsmethodik werden alle Workloads nach Wichtigkeit und Geschäftswert klassifiziert. Diese Klassifizierung kann dann durch eine Auswirkungsanalyse gemessen werden, die den mit Leistungseinbußen oder Betriebsunterbrechungen verbundenen Verlustwert berechnet. Mit diesen konkreten Umsatzauswirkungen können Cloudbetriebsteams mit dem Unternehmen zusammenarbeiten, um eine Zusage zu machen, die Kosten und Leistung in Einklang bringt.

**Disziplinen für den Cloudbetrieb:** Sobald das Unternehmen ausgerichtet ist, ist es viel einfacher, die richtigen Disziplinen des Cloudbetriebs für die einzelnen Workloads nachzuverfolgen und Berichte dazu zu erstellen. Die Entscheidungen in jeder Disziplin können dann in Zusagebedingungen umgewandelt werden, die für das Unternehmen leicht verständlich sind. Dieser kooperative Ansatz macht den Geschäftsbeteiligten zu einem Partner bei der Suche nach dem richtigen Verhältnis von Kosten und Leistung.

* Bestand und Transparenz: Betriebsverwaltung erfordert mindestens ein Mittel zur Bestandsaufnahme von Ressourcen und zur Schaffung von Transparenz über den Ausführungsstatus jeder Ressource.
* Betriebsbezogene Konformität: Die Verwaltung von Konfiguration, Größe, Kosten und Leistung von Ressourcen ist normalerweise der Schlüssel zur Aufrechterhaltung der Leistungserwartungen.
* Schutz und Wiederherstellung: Die Minimierung von Betriebsunterbrechungen und die Beschleunigung der Wiederherstellung tragen dazu bei, Leistungsverluste und Umsatzauswirkungen zu vermeiden. Erkennung und Wiederherstellung sind wesentliche Aspekte dieser Disziplin.
* Plattformbetrieb: Alle IT-Umgebungen umfassen eine Reihe von gemeinsam genutzten Plattformen. Diese Plattformen können Datenspeicher wie SQL Server oder HDInsights beinhalten. Andere gängige Plattformen können Containerlösungen wie Kubernetes oder AKS beinhalten. Unabhängig von den Plattformen liegt der Schwerpunkt bezüglich des Reifegrads des Plattformbetriebs auf der Anpassung von Vorgängen basierend darauf, wie diese gemeinsam genutzten Plattformen bereitgestellt, konfiguriert und durch Workloads genutzt werden.
* Workloadbetrieb: Auf der höchsten Stufe der betrieblichen Reife haben Cloudbetriebsteams die Möglichkeit, den Betrieb auf Workloads abzustimmen, die für den Geschäftserfolg entscheidend sind. Für diese hochkritischen Workloads können verfügbare Daten bei der Automatisierung der Problembehandlung, der Größenanpassung oder des Schutzes von Workloads basierend auf deren Auslastung helfen.

Zusätzliche Anleitungen wie der [Entwurf eines Überprüfungsframeworks (Codename: Cloudentwurfsprinzipien)](https://docs.microsoft.com/azure/architecture/reliability) können dabei helfen, detaillierte architekturbezogene Entscheidungen zu jeder Workload innerhalb der oben genannten Disziplinen zu treffen.

Dieser Abschnitt des Frameworks für die Cloudeinführung baut auf jedem dieser Themen auf, um den Cloudbetrieb in Ihrem Unternehmen zu verbessern.
