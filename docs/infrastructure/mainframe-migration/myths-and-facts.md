---
title: 'Mainframemigration: Mythen und Fakten'
description: Hier erfahren Sie, wie Sie Mainframe-Mythen von Fakten trennen und die Mainframe-Workloads evaluieren, die am besten für Azure geeignet sind.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e07879cfe8b40f9b0482d804aa6073c7ad79f3e0
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83217607"
---
<!-- cSpell:ignore njray nanra chargebacks IPLs -->

# <a name="mainframe-myths-and-facts"></a>Mainframe: Mythen und Fakten

Mainframes ragen aus der historischen Entwicklung von Computern deutlich heraus und besitzen weiterhin ihre Berechtigung für hochspezifische Workloads. Man ist sich allgemein einige, dass Mainframes eine bewährte Plattform mit schon lange etablierten Betriebsverfahren darstellen, die sie zu zuverlässigen und robusten Umgebungen machen. Software wird basierend auf der Nutzung ausgeführt, gemessen in Millionen Anweisungen/Sek. (MIPS), und es stehen umfassende Nutzungsberichte zur Verfügung für eventuelle Gebührenrückerstattungen.

Die Zuverlässigkeit, Verfügbarkeit und Verarbeitungsleistung von Mainframes haben beinahe mythische Ausmaße angenommen. Um die Mainframe-Workloads zu evaluieren, die am besten für Azure geeignet sind, sollten Sie zuerst die Mythen von den Fakten trennen.

## <a name="myth-mainframes-never-go-down-and-have-a-minimum-of-five-9s-of-availability"></a>Mythos: Mainframes fallen nie aus und besitzen eine Verfügbarkeit von mindestens fünf 9en (99,999 %).

Mainframe-Hardware und -Betriebssysteme werden als zuverlässig und stabil angesehen. Aber die Realität sieht so aus, dass Ausfallzeiten für Wartung und Neustarts, auch als „Initial Program Load“ (oder IPLs) bezeichnet, eingeplant werden müssen. Wenn Sie diese Aufgaben berücksichtigen, besitzt eine Mainframelösung oft eher über eine Verfügbarkeit von zwei oder drei 9en, was der von Intel-basierten High-End-Servern entspricht.

Mainframes bleiben auch anfällig für Notfälle und Katastrophen wie jeder andere Server auch und erfordern unterbrechungsfreie Stromversorgungssysteme (UPS), um diese Arten von Ausfällen abzufangen.

## <a name="myth-mainframes-have-limitless-scalability"></a>Mythos: Mainframes besitzen unbegrenzte Skalierbarkeit.

Die Skalierbarkeit eines Mainframes hängt von der Kapazität seiner Systemsoftware ab, z. B. dem Customer Informationen Control System (CICS) und der Kapazität neuer Instanzen von Mainframe-Engines und -Speichern. Einige große Unternehmen, die Mainframes verwenden, haben ihr CICS hinsichtlich der Leistung angepasst und sind ansonsten den Möglichkeiten des größten verfügbaren Mainframes entwachsen.

## <a name="myth-intel-based-servers-are-not-as-powerful-as-mainframes"></a>Mythos: Intel-basierte Servern sind nicht so leistungsfähig wie Mainframes.

Die neuen Intel-basierten Systeme mit hoher Core-Dichte haben so viel Rechenkapazität wie Mainframes.

## <a name="myth-the-cloud-cant-accommodate-mission-critical-applications-for-large-companies-such-as-financial-institutions"></a>Mythos: Die Cloud kann unternehmenskritische Anwendungen für große Unternehmen wie Finanzinstitute nicht aufnehmen.

Es mag zwar vereinzelte Fälle geben, in denen Cloudlösungen nicht ausreichen, aber dies liegt normalerweise daran, dass die Anwendungsalgorithmen nicht verteilt werden können. Diesen wenigen Beispiele sind die Ausnahmen, nicht die Regel.

## <a name="summary"></a>Zusammenfassung

Azure bietet im Vergleich dazu eine alternative Plattform, die in der Lage ist, gleichwertige Mainframefunktionen und -features bereitzustellen, und dies bei wesentlich geringeren Kosten. Darüber hinaus sind die Gesamtbetriebskosten (TCO) des abonnementbasierten und nutzungsabhängigen Kostenmodells der Cloud weit niedriger als bei Mainframecomputern.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Wechseln von Mainframes zu Azure](./migration-strategies.md)
