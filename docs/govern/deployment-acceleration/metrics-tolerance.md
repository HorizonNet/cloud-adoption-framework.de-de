---
title: Metriken und Indikatoren der Risikotoleranz in der Disziplin „Beschleunigung der Bereitstellung“
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um die Risikotoleranz von Unternehmen im Zusammenhang mit der Disziplin „Beschleunigung der Bereitstellung“ zu quantifizieren.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ed92a62d83092a54aa86c58f7b453768fe71ad1f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220276"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-deployment-acceleration-discipline"></a>Metriken und Indikatoren der Risikotoleranz in der Disziplin „Beschleunigung der Bereitstellung“

Lernen Sie, die Risikotoleranz von Unternehmen im Zusammenhang mit der Disziplin „Beschleunigung der Bereitstellung“ zu quantifizieren. Durch das Definieren von Metriken und Indikatoren können Sie ein Geschäftsszenario erstellen, um in die Ausgereiftheit dieser Disziplin zu investieren.

## <a name="metrics"></a>Metriken

Die Beschleunigung der Bereitstellung konzentriert sich auf Risiken im Hinblick auf die Konfiguration, Bereitstellung, Aktualisierung und Verwaltung von Cloudressourcen. Die folgenden Informationen sind bei der Einführung dieser Cloud Governance-Disziplin hilfreich:

- **Bereitstellungsfehler:** Prozentsatz von Bereitstellungen mit Fehlern oder falsch konfigurierten Ressourcen.
- **Bereitstellungszeit:** Die Zeitspanne, die zum Bereitstellen von Updates auf einem vorhandenen System benötigt wird.
- **Nicht konforme Ressourcen:** Die Anzahl oder der Prozentsatz der Ressourcen, die nicht mit den definierten Richtlinien konform sind.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

Risiken im Zusammenhang mit der Beschleunigung der Bereitstellung beziehen sich hauptsächlich auf die Anzahl und Komplexität der cloudbasierten Systeme, die für Ihr Unternehmen bereitgestellt werden. Mit dem Wachstum der Cloudumgebung erhöht sich auch die Anzahl der bereitgestellten Systeme und die Häufigkeit der Aktualisierung Ihrer Cloudressourcen. Durch die Abhängigkeiten zwischen den Ressourcen wird es immer wichtiger, eine ordnungsgemäße Konfiguration der Ressourcen sicherzustellen und resiliente Systeme zu entwerfen, falls eine oder mehrere Ressourcen unerwartet ausfallen.

Herkömmliche IT-Organisationen in Unternehmen bilden oftmals siloartige Teams für Betrieb, Sicherheit und Entwicklung, die häufig nicht gut zusammenarbeiten, gelegentlich sogar kontraproduktiv oder den anderen feindlich gesinnt sind. Wenn Sie diese Herausforderungen zu einem frühen Zeitpunkt erkennen und wichtige Mitglieder der einzelnen Teams einbinden, können Sie für Flexibilität, aber auch für Sicherheit und eine gute Steuerung bei der Cloudeinführung sorgen. Denken Sie deshalb bei der Entwicklung Ihrer Cloudeinführungsstrategie frühzeitig über eine Organisationskultur mit DevOps- oder [DevSecOps](https://www.microsoft.com/devsecops)-Vorgehensweisen nach.

Identifizieren Sie zusammen mit Ihrem DevSecOps-Team und der Unternehmensführung die [Geschäftsrisiken](./business-risks.md) im Zusammenhang mit der Konfiguration, und bestimmen Sie anschließend eine akzeptable Baseline für die entsprechende Risikotoleranz. Dieser Abschnitt der Anleitungen aus dem Framework für die Cloudeinführung (Cloud Adoption Framework) enthält einige Beispiele. Die Risiken und Baselines in Ihrem Unternehmen bzw. bei Ihren Bereitstellungen weichen im Detail wahrscheinlich davon ab.

Legen Sie nach der Einigung auf eine Baseline minimale Benchmarks fest, die eine unzulässige Zunahme der identifizierten Risiken darstellen. Diese Benchmarks fungieren als Auslöser und geben an, wann Sie Maßnahmen zum Beheben dieser Risiken ergreifen müssen. Im Folgenden wird anhand einiger Beispiele dargestellt, wie konfigurationsbezogene Metriken (z.B. die oben erwähnten) eine höhere Investition in die Disziplin „Beschleunigung der Bereitstellung“ rechtfertigen können.

- **Trigger bei Konfigurationsabweichungen:** Ein Unternehmen, bei dem unerwartete Änderungen an der Konfiguration wichtiger Systemkomponenten oder Fehler bei Bereitstellung oder Systemupdates auftreten, sollte in die Disziplin „Beschleunigung der Bereitstellung“ investieren, um die Hauptursachen und Lösungsschritte zu identifizieren.
- **Trigger bei Nichtkonformität:** Überschreitet die Anzahl der nicht konformen Ressourcen (entweder als Zahlenwert oder als Prozentsatz der Gesamtressourcen) einen definierten Schwellenwert, sollte ein Unternehmen in Verbesserungen der Disziplin „Beschleunigung der Bereitstellung“ investieren, um sicherzustellen, dass die Konfiguration der einzelnen Ressourcen während des gesamten Lebenszyklus der Ressource konform bleibt.
- **Trigger für den Projektzeitplan:** Wenn die Zeit zum Bereitstellen von Unternehmensressourcen und -anwendungen oft einen bestimmten Schwellenwert überschreitet, sollte ein Unternehmen in die Prozesse im Zusammenhang mit der Beschleunigung der Bereitstellung investieren, um automatische Bereitstellungen aus Konsistenz- und Vorhersagbarkeitsgründen einzuführen oder zu verbessern. Bereitstellungszeiten, die in Tagen oder sogar Wochen gemessen werden, weisen in der Regel auf eine suboptimale Strategie für die Beschleunigung der Bereitstellung hin.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die [Vorlage zur Disziplin „Beschleunigung der Bereitstellung“](./template.md) zum Dokumentieren der Metriken und Toleranzindikatoren, die sich am aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Beispielrichtlinien für die Beschleunigung der Bereitstellung als Ausgangspunkt für die Entwicklung Ihrer eigenen Richtlinien, um bestimmte Geschäftsrisiken zu behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
