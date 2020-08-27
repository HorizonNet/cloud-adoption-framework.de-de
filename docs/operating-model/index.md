---
title: Grundlegendes zu Cloudbetriebsmodellen
description: Hier finden Sie grundlegende Informationen zu Cloudbetriebsmodellen sowie zu deren Auswirkungen auf Ihre Cloudeinführungsstrategie.
author: BrianBlanchard
ms.author: brblanch
ms.date: 08/14/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: operating-model
ms.openlocfilehash: 404742da586fbd80c8963e71200cab8501feaff2
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88885591"
---
<!-- docsTest:casing GRC -->
<!-- cspell:ignore reimagine -->

# <a name="understand-cloud-operating-models"></a>Grundlegendes zu Cloudbetriebsmodellen

Die Cloudeinführung ist eine gute Gelegenheit, um sich noch einmal mit dem Betrieb von Technologiesystemen zu befassen. In dieser Artikelreihe werden Cloudbetriebsmodelle und die Aspekte erläutert, die sich auf Ihre Cloudeinführungsstrategie auswirken. Aber zunächst soll der Begriff *Cloudbetriebsmodell* verdeutlicht werden.

## <a name="define-your-operating-model"></a>Definieren Ihres Betriebsmodells

Bevor Sie Ihre Cloudarchitektur bereitstellen, müssen Sie wissen, wie Sie den Cloudbetrieb gestalten möchten. Machen Sie sich Gedanken über Ihre strategische Ausrichtung, Ihre Personalstruktur und Ihre GRC-Anforderungen (Governance, Risiko und Compliance), um Ihr zukünftiges Cloudbetriebsmodell besser definieren zu können. Anschließend können Azure-Zielzonen verwendet werden, um eine Vielzahl von Architektur- und Implementierungsoptionen für die Unterstützung Ihres Betriebsmodells bereitzustellen. Die nächsten Artikel enthalten einige grundlegende Begriffe sowie Beispiele für gängige Betriebsmodelle aus der Praxis. Diese Informationen helfen Ihnen dabei, sich für die passende Azure-Zielzone zu entscheiden.

## <a name="what-is-an-operating-model"></a>Was ist ein Betriebsmodell?

Als es noch keine Cloudtechnologien gab, haben Technologieteams Betriebsmodelle erstellt, um die Vorteile zu definieren, die Technologie für das Unternehmen hat. IT-Betriebsmodelle von Unternehmen umfassen eine Reihe von Faktoren. Einige sind jedoch immer konsistent: *Ausrichtung auf die Geschäftsstrategie, Strukturierung des Personals, Change Management (oder Einführungsprozesse), Betriebsverwaltung, Governance/Compliance und Sicherheit*. Jeder Faktor ist für den langfristigen Technologiebetrieb entscheidend.

Wird der Technologiebetrieb in die Cloud verlagert, sind diese wichtigen Prozesse zwar weiterhin relevant, verändern sich aber wahrscheinlich auf die eine oder andere Weise. Aktuelle Betriebsmodelle konzentrieren sich stark auf physische Ressourcen an physischen Standorten, die größtenteils über Investitionszyklen finanziert werden. Diese Ressourcen dienen zur Unterstützung der Workloads, die das Unternehmen benötigt, um den Geschäftsbetrieb aufrechtzuerhalten. Bei den meisten Betriebsmodellen hat die Stabilität der Workloads Priorität. Hierzu wird in die Stabilität der zugrunde liegenden physischen Ressourcen investiert.

## <a name="how-is-a-cloud-operating-model-different"></a>Was ist bei einem Cloudbetriebsmodell anders?

Redundanz im Hardwarestapel ist ein kontinuierlicher Zyklus. Physische Hardware geht kaputt. Die Leistung verschlechtert sich. Probleme mit der Hardware richten sich nur selten nach den vorhersehbaren Budgetzyklen der Investitionsplanung einer Organisation. Der Cloudbetrieb macht Schluss mit ständigen Hardwaremodernisierungen und nächtlichen Patches, indem er den Fokus auf die digitalen Ressourcen verlagert: Betriebssysteme, Anwendungen und Daten. Durch diese Verlagerung von physischen auf digitale Ressourcen verändert sich auch das Technologiebetriebsmodell.

Die Verlagerung Ihres Betriebsmodell in die Cloud bedeutet, dass sich die gleichen Personen und Prozesse auf eine höhere Betriebsebene konzentrieren können. Wenn sich Ihre Mitarbeiter nicht mehr auf die Uptime von Servern konzentrieren, ändern sich ihre Erfolgsmetriken. Wenn die Sicherheit nicht mehr von den vier Wänden eines Rechenzentrums abhängt, ändert sich Ihr Bedrohungsprofil. Wenn die Beschaffung kein Innovationshindernis mehr darstellt, ändert sich auch die Geschwindigkeit des Change Managements.

Ein *Cloudbetriebsmodell* ist die Gesamtheit von Prozessen und Prozeduren, die definieren, wie Sie Technologie in der Cloud betreiben möchten.

## <a name="purpose-of-a-cloud-operating-model"></a>Zweck eines Cloudbetriebsmodells

Wenn Hardware nicht mehr die grundlegendste Betriebseinheit darstellt, verlagert sich der Schwerpunkt auf die digitalen Ressourcen und die von ihnen unterstützten Workloads. Das Betriebsmodell dient nun also weniger dazu, den Betrieb aufrechtzuerhalten, sondern vielmehr dazu, betriebliche Konsistenz zu gewährleisten.

Mithilfe des [Microsoft Azure Well-Architected Framework](/azure/architecture/framework/) lassen sich Workloadaspekte sehr gut in verschiedene allgemeine Architekturprinzipien zerlegen: Kostenoptimierung, optimaler Betrieb, Leistungseffizienz, Zuverlässigkeit und Sicherheit.

Im Zuge der Umstellung auf eine höhere Betriebsebene helfen diese allgemeinen Architekturprinzipien dabei, den Zweck des Cloudbetriebsmodells neu auszurichten. Wie können wir bei allen Ressourcen und Workloads im Portfolio ein ausgewogenes Verhältnis dieser Architekturprinzipien sicherstellen? Welche Prozesse sind erforderlich, um die Anwendung dieser Prinzipien zu skalieren?

## <a name="reimagine-your-operating-model"></a>Neugestalten Ihres Betriebsmodells

Was bleibt noch zu tun, nachdem Sie Ihr Betriebsmodell aktualisiert haben, um sämtliche Beschaffungs-, Änderungs-, Betriebs- und Schutzaspekte im Zusammenhang mit physischen Ressourcen daraus zu entfernen? Für einige Organisationen stellt das Betriebsmodell nun einen kompletten Neuanfang dar. Bei den meisten Organisationen konnten die Einschränkungen, die sich im Laufe der Jahre entwickelt haben, reduziert werden. In beiden Fällen bietet es sich an, sich Gedanken über die gewünschte Cloudnutzung zu machen.

In diesen Artikeln werden die folgenden Themen behandelt, damit Sie sich Ihr zukünftiges Betriebsmodell besser vorstellen können:

- [Definieren Ihres Cloudbetriebsmodells](./define.md)
- [Vergleichen gängiger Cloudbetriebsmodelle](./compare.md)
- [Implementieren Ihres Betriebsmodells mit Azure-Zielzonen](../ready/landing-zone/implementation-options.md)

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich darüber, wie das Cloud Adoption Framework Sie beim Definieren Ihres Betriebsmodells unterstützt.

> [!div class="nextstepaction"]
> [Vergleichen gängiger Cloudbetriebsmodelle](./compare.md)
