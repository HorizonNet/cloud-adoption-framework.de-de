---
title: Einrichten von Teamstrukturen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Einrichten von Teamstrukturen
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: dbc3c21876f61444f3927fe4c61cf1b4302625b6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031783"
---
# <a name="establish-team-structures"></a>Einrichten von Teamstrukturen

Jede Cloudfunktion ist während einer Cloudeinführung einer oder mehreren Personen zugewiesen und wird von diesen bereitgestellt. Diese Zuweisungen und Teamstrukturen können sich organisch entwickeln oder explizit so entworfen werden, dass sie mit einer bereits definierten Teamstruktur übereinstimmen.

Wenn die Anforderungen an eine Cloudeinführung wachsen, entwickelt sich auch die Notwendigkeit, Gleichgewicht und Strukturen zu schaffen. Dieser Artikel enthält Beispiele für allgemeine Teamstrukturen in den verschiedenen Phasen des Organisationsreifegrads. Die folgende Grafik und die Liste verdeutlichen diese Strukturen auf der Grundlage typischer Entwicklungsstufen. Nutzen Sie diese Beispiele, um die Organisationsstruktur zu ermitteln, die am besten zu Ihren betrieblichen Anforderungen passt.

![Zyklus des Organisationsreifegrads](../_images/ready/org-ready-maturity.png)

Unternehmensstrukturen bewegen sich in der Regel durch ein allgemeines Reifegradmodell, das hier beschrieben wird:

1. [Nur Cloudeinführungsteam](#cloud-adoption-team-only)
2. [MVP – Bewährte Methode](#best-practice-minimum-viable-product-mvp)
3. [Zentrale IT-Abteilung](#central-it)
4. [Strategische Ausrichtung](#strategic-alignment)
5. [Operative Ausrichtung](#operational-alignment)
6. [Cloudkompetenzzentrum (CCoE)](#cloud-center-of-excellence)

Die meisten Unternehmen beginnen mit wenig mehr als einem *Cloudeinführungsteam*. Wir empfehlen jedoch, eine Organisationsstruktur aufzubauen, die mehr an der Struktur [Bewährte Methode: Minimum Viable Product](#best-practice-minimum-viable-product-mvp) ausgerichtet ist.

## <a name="cloud-adoption-team-only"></a>Nur Cloudeinführungsteam

Das Herzstück aller Cloudeinführungsmaßnahmen ist das Cloudeinführungsteam. Dieses Team stößt die technischen Änderungen an, die eine Einführung ermöglichen. Abhängig von den Zielen des Einführungsprojekts kann dieses Team aus vielen Mitgliedern unterschiedlichster Fachrichtungen bestehen, die eine umfassende Palette technischer und geschäftlicher Aufgaben übernehmen.

![Cloudeinführungsteam mit Governance- und Sicherheitsteams](../_images/ready/org-ready-adoption-only.png)

Bei kleinen Einführungsprojekten oder in der Frühphase eines Projekts besteht dieses Team möglicherweise aus nur einer Person. Für größere Projekte und in späteren Phasen ist es üblich, mehrere Cloudeinführungsteams mit jeweils etwa sechs Engineers einzusetzen. Unabhängig von Umfang und Anzahl der Aufgaben ist ein Aspekt bei allen Cloudeinführungsteams gleich: Sie bieten den Mechanismus zum Onboarding von Lösungen in die Cloud. Für einige Unternehmen kann dies eine ausreichende Organisationsstruktur sein. Der Artikel [Cloudeinführungsteam](./cloud-adoption.md) gibt weitere Einblicke in die Struktur, Zusammensetzung oder Funktion des Cloudeinführungsteams.

> [!WARNING]
> Der Einsatz von *nur* einem Cloudeinführungsteam (oder mehreren Cloudeinführungsteams) gilt als *Antimuster* und sollte vermieden werden. Ziehen Sie mindestens [Bewährte Methode: Minimum Viable Product](#best-practice-minimum-viable-product-mvp) in Betracht.

## <a name="best-practice-minimum-viable-product-mvp"></a>Bewährte Methode: Minimum Viable Product (MVP)

Wir empfehlen, zwei Teams einzusetzen, um ein Gleichgewicht zwischen den verschiedenen Aufgaben zur Cloudeinführung zu schaffen. Diese beiden Teams sind für verschiedene Aufgaben während der gesamten Einführung verantwortlich.

- **Cloudeinführungsteam**: Dieses Team ist für technische Lösungen, geschäftliche Ausrichtung, Projektmanagement und den Betrieb der eingeführten Lösungen verantwortlich.
- **Cloudgovernanceteam:** Um das Gleichgewicht zwischen den Cloudeinführungsteams zu gewährleisten, wird ein Cloudgovernanceteam eingesetzt, das dafür verantwortlich ist, dass exzellente Lösungen bereitgestellt werden. Das Cloudgovernanceteam ist für den Plattformreifegrad, Plattformbetrieb, Governance und Automatisierung verantwortlich.

![Cloudeinführung und mit Cloudgovernance als Gegengewicht](../_images/ready/org-ready-best-practice.png)

Dieser bewährte Ansatz gilt als MVP, weil er möglicherweise nicht nachhaltig ist. Jedes Team hat viele Aufgaben, wie in den [RACI-Diagrammen (*Responsible, Accountable, Consulted, Informed*)](./raci-alignment.md) erläutert wird.

In den folgenden Abschnitten wird eine vollständig besetzte, bewährte Organisationsstruktur sowie Ansätze für die Ausrichtung der geeigneten Struktur auf Ihre Organisation beschrieben.

## <a name="central-it"></a>Zentrale IT-Abteilung

Je umfangreicher die Einführung wird, desto schwieriger ist es möglicherweise für das Cloudgovernanceteam, mit dem Innovationsfluss aus mehreren Cloudeinführungsteams Schritt zu halten. Dies gilt insbesondere in Umgebungen mit hohen Anforderungen an Compliance, Betrieb und Sicherheit. In dieser Phase übertragen Unternehmen häufig Cloudzuständigkeiten an das vorhandene zentrale IT-Team. Wenn dieses Team in der Lage ist, Tools, Prozesse und Personen neu zu bewerten, um eine umfangreiche Cloudeinführung besser zu unterstützen, kann es einen signifikanten Mehrwert bieten. Das Einbeziehen von Fachleuten der Bereiche Betrieb, Automatisierung, Sicherheit und Verwaltung zur Modernisierung der zentralen IT kann zu effektiven operativen Innovationen führen.

![Cloudeinführung mit einem zentralen IT-Modell](../_images/ready/org-ready-central-it.png)

Leider kann die Phase, in der die zentrale IT ins Spiel kommt, eine der riskantesten Phasen beim Reifeprozess der Organisation sein. Das zentrale IT-Team muss vom Wachstum überzeugt sein. Wenn das Team die Cloud als Chance für Wachstum und Funktionserweiterung ansieht, kann es während des gesamten Prozesses unschätzbare Beiträge leisten. Wenn dieses Team die Cloudeinführung jedoch primär als Bedrohung für sein eigenes vorhandenes Modell betrachtet, kann es für die Cloudeinführungsteams und deren Geschäftsziele zu einem massiven Hindernis werden. Einige zentrale IT-Teams haben Monate oder sogar Jahre damit zugebracht, die Cloud an den lokalen IT-Verfahren auszurichten, und dabei nur negative Ergebnisse erzielt. Die Einführung der Cloud bedeutet nicht, dass in der zentralen IT alles auf den Kopf gestellt wird, einige Änderungen sind aber notwendig. Wenn in der zentralen IT ein genereller Widerstand gegen Änderungen vorherrscht, wird diese Phase des Reifeprozesses schnell zu einem kulturellen Antimuster.

Cloudeinführungspläne, bei denen der Fokus auf PaaS- (Platform-as-a-Service), DevOps- oder anderen Lösungen liegt, die weniger operative Unterstützung benötigen, zeitigen in dieser Reifephase wahrscheinlich weniger Mehrwert. Ganz im Gegenteil: Bei solchen Lösungen ist die Wahrscheinlichkeit am höchsten, dass sie durch Versuche zur Zentralisierung der IT beeinträchtigt oder sogar blockiert werden. Bei einem höheren Reifegrad, beispielsweise mit einem [Cloudkompetenzzentrum](#cloud-center-of-excellence) (Cloud Center of Excellence, CCoE), lassen sich für diese Arten von Transformationsaktionen vermutlich eher positive Ergebnisse erzielen. Informationen zu den Unterschieden zwischen der zentralen IT in der Cloud und einem CCoE finden Sie im Abschnitt [Cloudkompetenzzentrum](./cloud-center-of-excellence.md).

## <a name="strategic-alignment"></a>Strategische Ausrichtung

Wenn die Investitionen in die Cloudeinführung steigen und einen geschäftlichen Mehrwert generieren, sind die Beteiligten auf geschäftlicher Seite häufig stärker interessiert. Wie die folgende Abbildung zeigt, sorgt ein definiertes Cloudstrategieteam für die Ausrichtung dieser geschäftlichen Beteiligten, um den Mehrwert, der aus den Investitionen in die Cloudeinführung erwächst, zu maximieren.

![Einbinden eines definierten Cloudstrategieteams](../_images/ready/org-ready-strategy-aligned.png)

Wenn der Reifeprozess organisch und als Resultat einer durch die IT geleiteten Cloudeinführung abläuft, erfolgt die strategische Ausrichtung in der Regel durch ein Governance- oder zentrales IT-Team. Bei einer Cloudeinführung unter der Ägide der geschäftlichen Seite wird der Fokus häufig früher auf Betriebsmodell und -organisation gerichtet. Sowohl Geschäftsergebnisse als auch Cloudstrategieteam sollten möglichst frühzeitig im Prozess definiert werden.

## <a name="operational-alignment"></a>Operative Ausrichtung

Um geschäftlichen Mehrwert aus einem Cloudeinführungsprojekt zu erzielen, ist ein stabiler Betrieb erforderlich. Der Betrieb in der Cloud erfordert möglicherweise neue Tools, Prozesse oder Kenntnisse. Wenn ein stabiler IT-Betrieb erforderlich ist, um die gewünschten Geschäftsergebnisse zu erzielen, ist es wichtig, ein definiertes Cloudbetriebsteam einzubinden, wie hier zu sehen.

![Einbinden eines definierten Cloudbetriebsteams](../_images/ready/org-ready-operations-aligned.png)

Der Cloudbetrieb kann durch die vorhandenen IT-Betriebsfunktionen bereitgestellt werden. Es ist jedoch nicht ungewöhnlich, dass der Cloudbetrieb an andere Parteien außerhalb des IT-Betriebs delegiert wird. Anbieter von verwalteten Diensten, DevOps-Teams und IT-Teams einzelner Geschäftseinheiten übernehmen häufig die Zuständigkeiten in Bezug auf den Cloudbetrieb. Das IT-Betriebsteam stellt dann Unterstützung und Leitlinien bereit. Dies ist bei Cloudeinführungsprojekten, bei denen der Fokus vermehrt auf DevOps oder PaaS-Bereitstellungen liegt, immer häufiger zu beobachten.

## <a name="cloud-center-of-excellence"></a>Cloudkompetenzzentrum

Im Stadium des höchsten Reifegrads werden Teams in einem Cloudkompetenzzentrum an einem modernen Betriebsmodell ausgerichtet, bei dem die Cloud an erster Stelle steht. Dieser Ansatz bietet zentrale IT-Funktionen wie Governance, Sicherheit, Plattform und Automatisierung.

![Cloudkompetenzzentrum](../_images/ready/org-ready-ccoe.png)

Der Hauptunterschied zwischen dieser Struktur und einer zentralen IT-Struktur ist der Schwerpunkt auf Self-Service-Funktionen. Die Teams in dieser Struktur sind so organisiert, dass die Steuerung so weit wie möglich delegiert wird. Durch Ausrichten der Governance- und Complianceverfahren an cloudnativen Lösungen entstehen Leitlinien und Schutzmechanismen. Im Gegensatz zum zentralen IT-Modell maximiert der cloudnative Ansatz Innovationen und minimiert den operativen Aufwand. Damit ein solcher Ansatz umgesetzt werden kann, müssen die Führungskräfte von Business- und IT-Abteilung sich über die Modernisierung von IT-Prozessen einig sein. Dieses Modell entwickelt sich wahrscheinlich nicht organisch und erfordert häufig Unterstützung seitens der Geschäftsleitung.

## <a name="next-steps"></a>Nächste Schritte

Nach der Ausrichtung auf einen bestimmen Reifegrad der Organisationsstruktur können Verantwortlichkeiten und Zuständigkeiten anhand von [RACI-Diagrammen](./raci-alignment.md) den einzelnen Teams zugeordnet werden.

> [!div class="nextstepaction"]
> [Ausrichten des geeigneten RACI-Diagramms](./raci-alignment.md)
