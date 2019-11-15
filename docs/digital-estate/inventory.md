---
title: Erfassen von Bestandsdaten für digitale Ressourcen
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Informationen zum Erfassen von Bestandsdaten für ein digitales Umfeld.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 5ecf69235c27fbb45ad109609d8fd733dfc6187c
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753268"
---
# <a name="gather-inventory-data-for-a-digital-estate"></a>Erfassen von Bestandsdaten für digitale Ressourcen

Die Erstellung eines Bestandsverzeichnisses ist der erste Schritt bei der [Planung für digitale Ressourcen](./index.md). Hierzu wird eine Liste mit IT-Ressourcen, die bestimmte Geschäftsfunktionen unterstützen, zur späteren Analyse und Rationalisierung erfasst. In diesem Artikel wird davon ausgegangen, dass für die Planung ein Bottom-up-Analyseansatz am besten geeignet ist. Weitere Informationen finden Sie unter [Enterprise Cloud Adoption: Approaches to digital estate planning](./approach.md) (Enterprise Cloud-Einführung: Ansätze für die Planung digitaler Ressourcen).

## <a name="take-inventory-of-a-digital-estate"></a>Erfassen von Bestandsdaten für ein digitales Umfeld

Die Bestandsdaten zur Unterstützung eines digitalen Umfelds sind abhängig von der gewünschten digitalen Transformation und dem entsprechenden Transformationsprozess.

- **Cloudmigration:**  Wir empfehlen häufig, dass Sie im Rahmen einer Cloudmigration die Bestandsermittlung mithilfe von Überprüfungstools durchführen, die eine zentrale Liste aller virtueller Computer und Server erstellen. Einige Tools können auch Netzwerkzuordnungen und Abhängigkeiten erstellen, was beim Definieren des Workloadabgleichs hilfreich ist.

- **Anwendungsinnovationen:** Auch bei aktivierter Cloud beginnen Anwendungsinnovationen immer mit dem Kunden. Dabei hat es sich bewährt, zunächst die gesamte Benutzererfahrung zu erfassen. Durch den Abgleich dieser Erfassung mit Anwendungen, APIs, Daten und anderen Ressourcen entsteht ein detaillierter Bestand für die Analyse.

- **Dateninnovationen:** Bei cloudfähigen Dateninnovationen liegt der Fokus auf dem Produkt oder Dienst. Eine Bestandsaufnahme umfasst auch eine Zuordnung der Möglichkeiten zur Unterbrechung des Markts sowie der benötigten Funktionen.

- **Sicherheit**: Auf der Grundlage des Bestands können die Ressourcen der Organisation bewertet, geschützt und überwacht werden.

## <a name="accuracy-and-completeness-of-an-inventory"></a>Genauigkeit und Vollständigkeit eines Bestands

Eine Bestandsaufnahme ist selten im ersten Anlauf vollständig. Wir empfehlen dringend, dass das Cloudstrategie-Team Beteiligte und Hauptbenutzer für die Überprüfung der Bestandsaufnahme ausrichtet. Ermitteln Sie nach Möglichkeit mithilfe zusätzlicher Tools wie etwa einer Netzwerk- und Abhängigkeitsanalyse Ressourcen, an die Datenverkehr gesendet wird, die im Bestand aber nicht erfasst wurden.

## <a name="next-steps"></a>Nächste Schritte

Nach Abschluss und Überprüfung der Bestandsaufnahme kann der Bestand rationalisiert werden. Die Rationalisierung des Bestands ist der nächste Schritt bei der Planung für digitale Ressourcen.

> [!div class="nextstepaction"]
> [Rationalisieren der digitalen Ressourcen](./rationalize.md)
