---
title: Beweggründe und Geschäftsrisiken in der Disziplin „Beschleunigung der Bereitstellung“
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über Geschäftsrisiken der Disziplin „Beschleunigung der Bereitstellung“ zu informieren, die in der Governancestrategie verwendet werden kann.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6cd6d309b5c44c55d0409b759950662eccb9f50a
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220446"
---
# <a name="motivations-and-business-risks-in-the-deployment-acceleration-discipline"></a>Beweggründe und Geschäftsrisiken in der Disziplin „Beschleunigung der Bereitstellung“

In diesem Artikel werden die Gründe behandelt, die Kunden in der Regel im Rahmen ihrer Cloud Governance-Strategie zur Einrichtung der Disziplin „Beschleunigung der Bereitstellung“ veranlassen. Darüber hinaus werden einige Beispiele für Geschäftsrisiken aufgeführt, die zu Richtlinienanweisungen führen.

<!-- markdownlint-disable MD026 -->

## <a name="relevance"></a>Relevance

Lokale Systeme werden häufig mit Basisimages oder Installationsskripts bereitgestellt. In der Regel ist eine weitere Konfiguration erforderlich, die möglicherweise aus mehreren Schritten besteht oder manuelle Eingriffe erfordert. Diese manuellen Prozesse sind fehleranfällig und verursachen oftmals „Konfigurationsabweichungen“, die eine zeitintensive Problembehandlung und Korrekturmaßnahmen erfordern.

Die meisten Azure-Ressourcen können manuell über das Azure-Portal bereitgestellt und konfiguriert werden. Dieser Ansatz ist möglicherweise für Ihre Anforderungen ausreichend, wenn Sie nur wenige Ressourcen verwalten müssen. Wenn Ihr Ressourcenbestand in der Cloud wächst, sollte Ihr Unternehmen jedoch damit beginnen, Automatisierung in seine Bereitstellungsprozesse zu integrieren, um sicherzustellen, dass seine Cloudressourcen Konfigurationsverschiebungen oder andere durch manuelle Prozesse verursachte Probleme vermeiden. Die Einführung eines DevOps- oder [DevSecOps](https://www.microsoft.com/devsecops)-Ansatzes ist häufig die beste Möglichkeit zum Verwalten Ihrer Bereitstellungen, wenn Ihre Bemühungen zur Cloudeinführung ausgereifter werden.

Ein ausgereifter Plan für die Beschleunigung der Bereitstellung stellt sicher, dass Ihre Cloudressourcen ordnungsgemäß und einheitlich bereitgestellt, aktualisiert und konfiguriert werden und diesen Zustand auch beibehalten. Die Ausgereiftheit der Strategie zur Beschleunigung der Bereitstellung kann auch bei Ihrer [Kostenverwaltungsstrategie](../cost-management/index.md) einen bedeutenden Faktor darstellen. Mit einer automatischen Bereitstellung und Konfiguration Ihrer Cloudressourcen können Sie Ressourcen zentral herunterskalieren oder freigeben, wenn die Nachfrage niedrig oder zeitgebunden ist, sodass Sie Ressourcen nur nach Bedarf bezahlen.

## <a name="business-risk"></a>Geschäftsrisiken

Die Disziplin „Beschleunigung der Bereitstellung“ versucht, auf die folgenden Geschäftsrisiken einzugehen. Überprüfen Sie während der Cloudeinführung jedes einzelne Risiko auf Relevanz:

- **Dienstunterbrechung:** Fehlende vorhersagbare und wiederholbare Bereitstellungsprozesse oder nicht verwaltete Änderungen an Systemkonfigurationen können den normalen Betrieb unterbrechen und zu Produktivitäts- oder Umsatzeinbußen führen.
- **Kostenüberschreitungen:** Unerwartete Änderungen an der Konfiguration von Systemressourcen können das Identifizieren der Hauptursache von Problemen erschweren und die Kosten für Entwicklung, Betrieb und Wartung in die Höhe treiben.
- **Organisatorische Ineffizienz:** Mangelnde Zusammenarbeit zwischen Entwicklungs-, Betriebs- und Sicherheitsteams können zu zahlreichen Herausforderungen bei der effektiven Einführung von Cloudtechnologien und bei der Entwicklung eines einheitlichen Cloud Governance-Modells führen.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die [Vorlage zur Disziplin „Beschleunigung der Bereitstellung](./template.md) zum Dokumentieren von Geschäftsrisiken, die mit dem aktuellen Cloudeinführungsplan wahrscheinlich entstehen.

Sobald ein Verständnis für realistische Geschäftsrisiken hergestellt ist, besteht der nächste Schritt darin, die Risikotoleranz des Unternehmens zu dokumentieren sowie die Indikatoren und Schlüsselmetrik zur Überwachung dieser Toleranz zu erfassen.

> [!div class="nextstepaction"]
> [Metriken, Indikatoren und Risikotoleranz](./metrics-tolerance.md)
