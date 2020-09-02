---
title: 'Kostenmanagement: Prozesse für Richtlinienkonformität'
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um sich über einen Ansatz für die Erstellung von Prozessen zu informieren, die eine Disziplin vom Typ „Kostenmanagement“ unterstützen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3e1a6b1b562242c77e6c3e35b43eb2e464736673
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88883806"
---
# <a name="cost-management-policy-compliance-processes"></a>Kostenmanagement: Prozesse für Richtlinienkonformität

In diesem Artikel wird ein Ansatz zum Erstellen von Prozessen erläutert, die eine wirksame [Disziplin vom Typ „Kostenmanagement“](./index.md) unterstützen. Die wirksame Governance der Cloud beginnt mit sich wiederholenden manuellen Prozessen zur Unterstützung der Richtlinieneinhaltung. Dies erfordert die regelmäßige Einbeziehung des Cloudgovernanceteams sowie interessierter Geschäftsbeteiligter, um Richtlinien zu überprüfen und zu aktualisieren und die Einhaltung von Richtlinien sicherzustellen. Darüber hinaus können viele laufende Überwachungs- und Durchsetzungsprozesse automatisiert oder durch Werkzeuge ergänzt werden, um den Kontrolloverhead zu reduzieren und schneller auf Abweichungen von der Richtlinie reagieren zu können.

## <a name="planning-review-and-reporting-processes"></a>Planungs-, Prüfungs- und Berichterstellungsprozesse

Die besten Tools für das Kostenmanagement in der Cloud sind nur so gut wie die Prozesse und Richtlinien, durch die sie unterstützt werden. Nachstehend sind eine Reihe von Beispielprozessen ausgeführt, die häufig im Rahmen der Disziplin „Kostenmanagement“ verwendet werden. Beim Planen der Prozesse, die Ihnen die fortgesetzte Aktualisierung der Kostenrichtlinie aufgrund von geschäftlichen Änderungen und Feedback von den Geschäftsteams (gemäß dem Kostengovernanceleitfaden) erlauben, können Sie diese Beispiele als Ausgangspunkt verwenden.

**Anfängliche Risikobewertung und Planung:** Im Rahmen der ersten Einführung der Disziplin „Kostenmanagement“ identifizieren Sie Ihre Kerngeschäftsrisiken und Toleranzen im Zusammenhang mit den Cloudkosten. Verwenden Sie diese Informationen, um budget- und kostenbezogene Risiken mit Mitgliedern Ihrer Geschäftsteams zu besprechen und einen grundlegenden Satz von Richtlinien zur Minimierung dieser Risiken zu entwickeln, um Ihre erste Governancestrategie zu formulieren.

**Bereitstellungsplanung**: Legen Sie vor der Bereitstellung von Ressourcen ein prognostiziertes, auf erwarteter Cloudzuweisung basierendes Budget fest. Stellen Sie sicher, dass Besitzer- und Kostenabrechnungsinformationen für die Bereitstellung dokumentiert sind.

**Jährliche Planung**: Führen Sie jährlich eine Rollupanalyse für alle bereitgestellten und bereitzustellenden Ressourcen durch. Richten Sie die Budgets an Geschäftseinheiten, Abteilungen, Teams und anderen entsprechenden Einheiten aus, um eine Einführung nach dem Self-Service-Prinzip zu ermöglichen. Stellen Sie sicher, dass der Leiter jeder Abrechnungseinheit das Budget kennt und Ausgaben nachverfolgen kann.

Dies ist der Zeitpunkt für eine Vorabverpflichtung oder einen Kauf im voraus, um Rabatte zu maximieren. Es ist ratsam, die jährliche Budgetierung mit dem Geschäftsjahr des Cloudanbieters abzustimmen, um weiteren Nutzen aus Jahresend-Rabattoptionen zu ziehen.

**Vierteljährliche Planung**: Überprüfen Sie Budgets einmal pro Quartal mit jedem Abrechnungseinheitenleiter, um Vorhersage und tatsächliche Ausgaben abzustimmen. Wenn Änderungen des Plans oder unerwartete Ausgabenmuster auftreten, stimmen Sie das Budget darauf ab und weisen Sie es neu zu.

Dieser vierteljährliche Planungsprozess ist auch ein guter Zeitpunkt, um die aktuelle Zusammensetzung Ihres Cloudgovernanceteams auf Wissenslücken im Zusammenhang mit aktuellen oder zukünftigen Geschäftsplänen zu überprüfen. Laden Sie relevante Mitarbeiter und Workloadbesitzer ein, an Überprüfungen und Planungen teilzunehmen, entweder als zeitlich begrenzte Berater oder als ständige Mitglieder Ihres Teams.

**Aus- und Weiterbildung:** Bieten Sie zweimonatlich Schulungen an, um sicherzustellen, dass Geschäfts- und IT-Mitarbeiter auf dem neuesten Stand der Richtlinienanforderungen für Cost Management sind. Im Rahmen dieses Prozesses überprüfen und aktualisieren Sie alle Unterlagen, Anleitungen oder andere Trainingsmaterialien, um sicherzustellen, dass sie mit den neuesten Unternehmensrichtlinien übereinstimmen.

**Monatliche Berichterstellung**: Berichten Sie monatlich über das Verhältnis zwischen tatsächlichen Ausgaben und Vorhersage. Unterrichten Sie Abrechnungsleiter über unerwartete Abweichungen.

Diese grundlegenden Prozesse tragen dazu bei, Ausgaben abzustimmen und eine Grundlage für die Disziplin „Kostenmanagement“ zu bilden.

## <a name="processes-for-ongoing-monitoring"></a>Prozesse zur fortlaufenden Überwachung

Eine erfolgreiche Strategie für das Kostenmanagement hängt vom Einblick in vergangene, aktuelle und geplante zukünftige cloudbezogene Ausgaben ab. Ohne die Möglichkeit, die relevanten Metriken und Daten Ihrer bestehenden Kosten zu analysieren, können Sie keine Veränderungen bei den Risiken und keine Verstöße gegen Ihre Risikotoleranzen erkennen. Für die oben genannten laufenden Governanceprozesse sind Qualitätsdaten erforderlich, um eine entsprechende Änderung der Richtlinie zu gewährleisten und Ihre Infrastruktur vor wechselnden Geschäftsanforderungen und wechselnder Cloudnutzung besser zu schützen.

Stellen Sie sicher, dass Ihre IT-Teams automatisierte Systeme für die Überwachung Ihrer Cloudausgaben und zur Verwendung für nicht geplante Abweichungen von erwarteten Kosten implementiert haben. Richten Sie Berichterstellungs- und Warnsysteme ein, um die schnelle Erkennung und Minderung potenzieller Verstöße gegen Richtlinien sicherzustellen.

## <a name="compliance-violation-triggers-and-enforcement-actions"></a>Auslöser bei Complianceverstößen und Durchsetzungsmaßnahmen

Wenn Verstöße festgestellt werden, sollten Sie Durchsetzungsmaßnahmen ergreifen, um eine erneute Einhaltung der Richtlinien zu erreichen. Sie können die meisten Auslöser bei Verstößen mit den unter [Kostenmanagement-Toolkette für Azure](./toolchain.md) beschriebenen Tools automatisieren.

Hier einige Beispiele für Trigger:

- **Monatliche Budgetabweichungen**: Erörtern Sie Abweichungen bei den monatlichen Ausgaben, die das Verhältnis zwischen Vorhersage und tatsächlichen Ausgaben um 20% überschreiten, mit dem Abrechnungseinheitenleiter. Zeichnen Sie Auflösungen und Änderungen in der Prognose auf.
- **Geschwindigkeit der Einführung**: Jede Abweichung auf Abonnementebene, die 20% überschreitet, löst eine Prüfung mit dem Abrechnungseinheitenleiter aus. Zeichnen Sie Auflösungen und Änderungen in der Prognose auf.

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie die [Vorlage zur Disziplin „Kostenmanagement“](./template.md) zum Dokumentieren der Prozesse und Auslöser, die sich an dem aktuellen Cloudeinführungsplan orientieren.

Anleitungen zur Ausführung von Kostenmanagementrichtlinien in Abstimmung mit Einführungsplänen finden Sie unter [Verbesserung der Disziplin „Kostenmanagement“](./discipline-improvement.md).

> [!div class="nextstepaction"]
> [Verbesserung der Disziplin „Kostenmanagement“](./discipline-improvement.md)
