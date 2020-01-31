---
title: Beschleunigung der Bereitstellung – Metriken, Indikatoren und Risikotoleranz
description: Beschleunigung der Bereitstellung – Metriken, Indikatoren und Risikotoleranz
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 26bbcd201d699c8f58d51bb4f83582417127fcbb
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76804026"
---
# <a name="deployment-acceleration-metrics-indicators-and-risk-tolerance"></a>Beschleunigung der Bereitstellung – Metriken, Indikatoren und Risikotoleranz

Dieser Artikel unterstützt Sie bei der Quantifizierung der Geschäftsrisikotoleranz im Zusammenhang mit der Beschleunigung der Bereitstellung. Das Definieren von Metriken und Indikatoren ermöglicht das Erstellen eines Geschäftsszenarios, mit dem Sie verstärkt auf die Ausgereiftheit der Disziplin „Beschleunigung der Bereitstellung“ setzen können.

## <a name="metrics"></a>Metriken

Die Disziplin zur Beschleunigung der Bereitstellung konzentriert sich auf Risiken im Hinblick auf die Konfiguration, Bereitstellung, Aktualisierung und Verwaltung von Cloudressourcen. Die folgenden Informationen sind bei der Einführung dieser Cloud Governance-Disziplin hilfreich:

- **Bereitstellungsfehler:** Prozentsatz von Bereitstellungen mit Fehlern oder falsch konfigurierten Ressourcen.
- **Bereitstellungszeit:** Die Zeitspanne, die zum Bereitstellen von Updates auf einem vorhandenen System benötigt wird.
- **Nicht konforme Ressourcen:** Die Anzahl oder der Prozentsatz der Ressourcen, die nicht mit den definierten Richtlinien konform sind.

## <a name="risk-tolerance-indicators"></a>Risikotoleranzindikatoren

Risiken im Zusammenhang mit der Beschleunigung der Bereitstellung beziehen sich hauptsächlich auf die Anzahl und Komplexität der cloudbasierten Systeme, die für Ihr Unternehmen bereitgestellt werden. Mit dem Wachstum der Cloudumgebung erhöht sich auch die Anzahl der bereitgestellten Systeme und die Häufigkeit der Aktualisierung Ihrer Cloudressourcen. Durch die Abhängigkeiten zwischen den Ressourcen wird es immer wichtiger, eine ordnungsgemäße Konfiguration der Ressourcen sicherzustellen und resiliente Systeme zu entwerfen, falls eine oder mehrere Ressourcen unerwartet ausfallen.

<!-- "en-us" location is required for the URL below. -->

Herkömmliche IT-Organisationen in Unternehmen bilden oftmals siloartige Teams für Betrieb, Sicherheit und Entwicklung, die häufig nicht gut zusammenarbeiten, gelegentlich sogar kontraproduktiv oder den anderen feindlich gesinnt sind. Wenn Sie diese Herausforderungen zu einem frühen Zeitpunkt erkennen und wichtige Mitglieder der einzelnen Teams einbinden, können Sie für Flexibilität, aber auch für Sicherheit und eine gute Steuerung bei der Cloudeinführung sorgen. Denken Sie daher bei der Entwicklung Ihrer Cloudeinführungsstrategie frühzeitig über eine Organisationskultur mit DevOps- oder [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops)-Vorgehensweisen nach.

Identifizieren Sie zusammen mit Ihrem DevSecOps-Team und der Unternehmensführung die [Geschäftsrisiken](./business-risks.md) im Zusammenhang mit der Konfiguration, und bestimmen Sie anschließend eine akzeptable Baseline für die entsprechende Risikotoleranz. Dieser Abschnitt der Anleitungen aus dem Framework für die Cloudeinführung (Cloud Adoption Framework) enthält einige Beispiele. Die Risiken und Baselines in Ihrem Unternehmen bzw. bei Ihren Bereitstellungen weichen im Detail wahrscheinlich davon ab.

Legen Sie nach der Einigung auf eine Baseline minimale Benchmarks fest, die eine unzulässige Zunahme der identifizierten Risiken darstellen. Diese Benchmarks fungieren als Auslöser und geben an, wann Sie Maßnahmen zum Beheben dieser Risiken ergreifen müssen. Im Folgenden wird anhand einiger Beispiele dargestellt, wie konfigurationsbezogene Metriken (z.B. die oben erwähnten) eine höhere Investition in die Disziplin „Beschleunigung der Bereitstellung“ rechtfertigen können.

- **Trigger bei Konfigurationsabweichungen:** Ein Unternehmen, bei dem unerwartete Änderungen an der Konfiguration wichtiger Systemkomponenten oder Fehler bei Bereitstellung oder Systemupdates auftreten, sollte in die Disziplin „Beschleunigung der Bereitstellung“ investieren, um die Hauptursachen und Lösungsschritte zu identifizieren.
- **Trigger bei Nichtkonformität:** Überschreitet die Anzahl der nicht konformen Ressourcen (entweder als Zahlenwert oder als Prozentsatz der Gesamtressourcen) einen definierten Schwellenwert, sollte ein Unternehmen in Verbesserungen der Disziplin „Beschleunigung der Bereitstellung“ investieren, um sicherzustellen, dass die Konfiguration der einzelnen Ressourcen während des gesamten Lebenszyklus der Ressource konform bleibt.
- **Trigger für den Projektzeitplan:** Wenn die Zeit zum Bereitstellen von Unternehmensressourcen und -anwendungen häufig einen bestimmten Schwellenwert überschreitet, sollte ein Unternehmen in die Prozesse im Zusammenhang mit der Beschleunigung der Bereitstellung investieren und aus Konsistenz- und Verhersagbarkeitsgründen automatische Bereitstellungen einführen (oder optimieren). Bereitstellungszeiten, die in Tagen oder sogar Wochen gemessen werden, weisen in der Regel auf eine suboptimale Strategie für die Beschleunigung der Bereitstellung hin.

## <a name="next-steps"></a>Nächste Schritte

Dokumentieren Sie mit der Vorlage [Cloudverwaltung](./template.md) die Metriken und Toleranzindikatoren, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Nutzen Sie Beispielrichtlinien für die Beschleunigung der Bereitstellung als Ausgangspunkt für die Entwicklung von Richtlinien, die bestimmte Geschäftsrisiken behandeln, die Ihren Plänen für die Einführung der Cloud entsprechen.

> [!div class="nextstepaction"]
> [Überprüfen von Beispielrichtlinien](./policy-statements.md)
