---
title: Ausgereifte Teamstrukturen
description: Nutzen Sie diese Beispiele für allgemeine Teamstrukturen, um die Organisationsstruktur zu ermitteln, die während der Cloudeinführung am besten zu Ihren betrieblichen Anforderungen passt.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/18/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 6d9c8d509abbc5516a3070fe03116a588ddeacbf
ms.sourcegitcommit: 011525720bd9e2d9bcf03a76f371c4fc68092c45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88573070"
---
<!-- cSpell:ignore ccoe -->

# <a name="mature-team-structures"></a>Ausgereifte Teamstrukturen

Jede Cloudfunktion ist während einer Cloudeinführung einer oder mehreren Personen zugewiesen und wird von diesen bereitgestellt. Diese Zuweisungen und Teamstrukturen können sich organisch entwickeln oder explizit so entworfen werden, dass sie mit einer bereits definierten Teamstruktur übereinstimmen.

Wenn die Anforderungen an eine Cloudeinführung wachsen, entwickelt sich auch die Notwendigkeit, Gleichgewicht und Strukturen zu schaffen. Sehen Sie sich dieses Video an, um einen Überblick über allgemeine Teamstrukturen in den verschiedenen Phasen des Organisationsreifegrads zu erhalten.

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4wvTS]

<!-- markdownlint-enable MD034 -->

Die folgende Grafik und die Liste verdeutlichen diese Strukturen auf der Grundlage typischer Entwicklungsstufen. Nutzen Sie diese Beispiele, um die Organisationsstruktur zu ermitteln, die am besten zu Ihren betrieblichen Anforderungen passt.

![Zyklus des Organisationsreifegrads](../_images/ready/org-ready-maturity.png)

Unternehmensstrukturen bewegen sich in der Regel durch ein allgemeines Reifegradmodell, das hier beschrieben wird:

1. [Nur Cloudeinführungsteam](#cloud-adoption-team-only)
2. [MVP – Bewährte Methode](#best-practice-minimum-viable-product-mvp)
3. [Zentrales IT-Team](#central-it-team)
4. [Strategische Ausrichtung](#strategic-alignment)
5. [Operative Ausrichtung](#operational-alignment)
6. [Cloudkompetenzzentrum (CCoE)](#cloud-center-of-excellence)

Die meisten Unternehmen beginnen mit wenig mehr als einem *Cloudeinführungsteam*. Es wird jedoch empfohlen, dass Sie eine Organisationsstruktur einrichten, die der Struktur [MVP – Bewährte Methode](#best-practice-minimum-viable-product-mvp) ähnlicher ist.

## <a name="cloud-adoption-team-only"></a>Nur Cloudeinführungsteam

Das Herzstück aller Cloudeinführungsmaßnahmen ist das Cloudeinführungsteam. Dieses Team stößt die technischen Änderungen an, die eine Einführung ermöglichen. Abhängig von den Zielen des Einführungsprojekts kann dieses Team aus vielen Mitgliedern unterschiedlichster Fachrichtungen bestehen, die eine umfassende Palette technischer und geschäftlicher Aufgaben übernehmen.

![Nur Cloudeinführungsteam](../_images/ready/org-ready-adoption-only.png)

Bei kleinen Einführungsprojekten oder in der Frühphase eines Projekts besteht dieses Team möglicherweise aus nur einer Person. Für größere Projekte und in späteren Phasen ist es üblich, mehrere Cloudeinführungsteams mit jeweils etwa sechs Engineers einzusetzen. Unabhängig von Umfang und Anzahl der Aufgaben ist ein Aspekt bei allen Cloudeinführungsteams gleich: Sie bieten den Mechanismus zum Onboarding von Lösungen in die Cloud. Für einige Unternehmen kann dies eine ausreichende Organisationsstruktur sein. Der Artikel [Cloudeinführungsteam](./cloud-adoption.md) gibt weitere Einblicke in die Struktur, Zusammensetzung oder Funktion des Cloudeinführungsteams.

> [!WARNING]
> Der Einsatz von **nur** einem Cloudeinführungsteam (oder mehreren Cloudeinführungsteams) gilt als Antimuster und sollte vermieden werden. Ziehen Sie mindestens [Bewährte Methode: Minimum Viable Product](#best-practice-minimum-viable-product-mvp) in Betracht.

## <a name="best-practice-minimum-viable-product-mvp"></a>Bewährte Methode: Minimum Viable Product (MVP)

![Bewährte Methode: Organisation von Minimum Viable Product (MVP) aus Einführungsteam und Governanceteam, um ein Gleichgewicht zu schaffen](../_images/ready/org-ready-best-practice.png)

Wir empfehlen, zwei Teams einzusetzen, um ein Gleichgewicht zwischen den verschiedenen Aufgaben zur Cloudeinführung zu schaffen. Diese beiden Teams sind für verschiedene Aufgaben während der gesamten Einführung verantwortlich.

- **Cloudeinführungsteam**: Dieses Team ist für technische Lösungen, geschäftliche Ausrichtung, Projektmanagement und den Betrieb der eingeführten Lösungen verantwortlich.
- **Cloudgovernanceteam:** Um das Gleichgewicht zwischen den Cloudeinführungsteams zu gewährleisten, wird ein Cloudgovernanceteam eingesetzt, das dafür verantwortlich ist, dass exzellente Lösungen bereitgestellt werden. Das Cloudgovernanceteam ist für den Plattformreifegrad, Plattformbetrieb, Governance und Automatisierung verantwortlich.

Dieser bewährte Ansatz gilt als MVP, weil er möglicherweise nicht nachhaltig ist. Jedes Team hat viele Aufgaben, wie in den [RACI-Diagrammen (*Responsible, Accountable, Consulted, Informed*)](./raci-alignment.md) erläutert wird.

In den folgenden Abschnitten wird eine vollständig besetzte, bewährte Organisationsstruktur sowie Ansätze für die Ausrichtung der geeigneten Struktur auf Ihre Organisation beschrieben.

## <a name="central-it-team"></a>Zentrales IT-Team

![Zentrales IT-Team](../_images/ready/org-ready-central-it.png)

Je umfangreicher die Einführung wird, desto schwieriger ist es möglicherweise für das Cloudgovernanceteam, mit dem Innovationsfluss aus mehreren Cloudeinführungsteams Schritt zu halten. Dies gilt insbesondere in Umgebungen mit hohen Anforderungen an Compliance, Betrieb und Sicherheit. In dieser Phase übertragen Unternehmen häufig Cloudzuständigkeiten an das vorhandene zentrale IT-Team. Wenn dieses Team Tools, Prozesse und Personen neu bewerten kann, um eine umfangreiche Cloudeinführung besser zu unterstützen, kann es einen signifikanten Mehrwert bieten. Das Einbeziehen von Fachleuten der Bereiche Betrieb, Automatisierung, Sicherheit und Verwaltung zur Modernisierung des zentralen IT-Teams kann zu effektiven operativen Innovationen führen.

Leider kann die Phase, in der das zentrale IT-Team ins Spiel kommt, eine der riskantesten Phasen beim Reifeprozess der Organisation sein. Das zentrale IT-Team muss vom Wachstum überzeugt sein. Wenn das Team die Cloud als Chance für Wachstum und Anpassung ansieht, kann es während des gesamten Prozesses unschätzbare Beiträge leisten. Wenn das zentrale IT-Team die Cloudeinführung jedoch primär als Bedrohung für sein eigenes vorhandenes Modell betrachtet, kann es für die Cloudeinführungsteams und deren Geschäftsziele zu einem massiven Hindernis werden. Einige zentrale IT-Teams haben Monate oder sogar Jahre damit zugebracht, die Cloud an den lokalen IT-Verfahren auszurichten, und dabei nur negative Ergebnisse erzielt. Die Einführung der Cloud bedeutet nicht, dass im zentralen IT-Team alles auf den Kopf gestellt wird, einige signifikante Änderungen sind aber notwendig. Wenn in der zentralen IT ein genereller Widerstand gegen Änderungen vorherrscht, wird diese Phase des Reifeprozesses schnell zu einem kulturellen Antimuster.

Cloudeinführungspläne, bei denen der Fokus auf PaaS- (Platform-as-a-Service), DevOps- oder anderen Lösungen liegt, die weniger operative Unterstützung benötigen, zeitigen in dieser Reifephase wahrscheinlich weniger Mehrwert. Ganz im Gegenteil: Bei solchen Lösungen ist die Wahrscheinlichkeit am höchsten, dass sie durch Versuche zur Zentralisierung der IT beeinträchtigt oder sogar blockiert werden. Bei einem höheren Reifegrad, beispielsweise mit einem [Cloudkompetenzzentrum](#cloud-center-of-excellence) (Cloud Center of Excellence, CCoE), lassen sich für diese Arten von Transformationsaktionen vermutlich eher positive Ergebnisse erzielen. Informationen zu den Unterschieden zwischen der zentralisierten IT in der Cloud und einem CCoE finden Sie im Abschnitt [Cloudkompetenzzentrum](./cloud-center-of-excellence.md).

## <a name="strategic-alignment"></a>Strategische Ausrichtung

![Strategische Ausrichtung](../_images/ready/org-ready-strategy-aligned.png)

Wenn die Investitionen in die Cloudeinführung steigen und einen geschäftlichen Mehrwert generieren, sind die Beteiligten auf geschäftlicher Seite häufig stärker interessiert. Wie die folgende Abbildung zeigt, sorgt ein definiertes Cloudstrategieteam für die Ausrichtung dieser geschäftlichen Beteiligten, um den Mehrwert, der aus den Investitionen in die Cloudeinführung erwächst, zu maximieren.

Wenn der Reifeprozess organisch und als Resultat einer durch die IT geleiteten Cloudeinführung abläuft, erfolgt die strategische Ausrichtung in der Regel durch ein Governance- oder zentrales IT-Team. Bei einer Cloudeinführung unter der Ägide der geschäftlichen Seite wird der Fokus häufig früher auf Betriebsmodell und -organisation gerichtet. Sowohl Geschäftsergebnisse als auch Cloudstrategieteam sollten möglichst frühzeitig im Prozess definiert werden.

## <a name="operational-alignment"></a>Operative Ausrichtung

![Operative Ausrichtung](../_images/ready/org-ready-operations-aligned.png)

Um geschäftlichen Mehrwert aus einem Cloudeinführungsprojekt zu erzielen, ist ein stabiler Betrieb erforderlich. Der Betrieb in der Cloud erfordert möglicherweise neue Tools, Prozesse oder Kenntnisse. Wenn ein stabiler IT-Betrieb erforderlich ist, um die gewünschten Geschäftsergebnisse zu erzielen, ist es wichtig, ein definiertes Cloudbetriebsteam einzubinden, wie hier zu sehen.

Der Cloudbetrieb kann durch die vorhandenen IT-Betriebsfunktionen bereitgestellt werden. Es ist jedoch nicht ungewöhnlich, dass der Cloudbetrieb an andere Parteien außerhalb des IT-Betriebs delegiert wird. Anbieter von verwalteten Diensten, DevOps-Teams und IT-Teams einzelner Geschäftseinheiten übernehmen häufig die Zuständigkeiten in Bezug auf den Cloudbetrieb. Das IT-Betriebsteam stellt dann Unterstützung und Leitlinien bereit. Dies ist bei Cloudeinführungsprojekten, bei denen der Fokus vermehrt auf DevOps oder PaaS-Bereitstellungen liegt, immer häufiger zu beobachten.

## <a name="cloud-center-of-excellence"></a>Cloudkompetenzzentrum

![Cloudkompetenzzentrum (CCoE)](../_images/ready/org-ready-ccoe.png)

Im Stadium des höchsten Reifegrads werden Teams in einem Cloudkompetenzzentrum an einem modernen Betriebsmodell ausgerichtet, bei dem die Cloud an erster Stelle steht. Dieser Ansatz bietet zentralisierte IT-Funktionen wie Governance, Sicherheit, Plattform und Automatisierung.

Der Hauptunterschied zwischen dieser Struktur und der Struktur eines zentralen IT-Teams ist der erhebliche Schwerpunkt auf Self-Service-Funktionen und Demokratisierung. Die Teams in dieser Struktur sind so organisiert, dass die Steuerung so weit wie möglich delegiert wird. Durch Ausrichten der Governance- und Complianceverfahren an cloudnativen Lösungen entstehen Leitlinien und Schutzmechanismen. Im Gegensatz zum Modell des zentralen IT-Teams maximiert der cloudnative Ansatz Innovationen und minimiert den operativen Aufwand. Damit ein solcher Ansatz umgesetzt werden kann, müssen die Führungskräfte von Business- und IT-Abteilung sich über die Modernisierung von IT-Prozessen einig sein. Dieses Modell entwickelt sich wahrscheinlich nicht organisch und erfordert häufig Unterstützung seitens der Geschäftsleitung.

## <a name="next-steps"></a>Nächste Schritte

Nach der Ausrichtung auf einen bestimmen Reifegrad der Organisationsstruktur können Verantwortlichkeiten und Zuständigkeiten anhand von [RACI-Diagrammen](./raci-alignment.md) den einzelnen Teams zugeordnet werden.

> [!div class="nextstepaction"]
> [Ausrichten des geeigneten RACI-Diagramms](./raci-alignment.md)
