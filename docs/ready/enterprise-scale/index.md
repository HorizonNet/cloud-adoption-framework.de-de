---
title: Beginnen mit Zielzonen auf Unternehmensebene
description: Beginnen mit Zielzonen auf Unternehmensebene
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: d2218a84cda97c42a98327a9902009a47f8839b5
ms.sourcegitcommit: d88c1cc3597a83ab075606d040ad659ac4b33324
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84792199"
---
# <a name="start-with-enterprise-scale-landing-zones"></a>Beginnen mit Zielzonen auf Unternehmensebene

Die Unternehmensarchitektur stellt den strategischen Entwurfspfad und den technischen Zielstatus für die Azure-Umgebung des Kunden dar. Sie wird weiterhin parallel zur Azure-Plattform weiterentwickelt und letztendlich durch die verschiedenen Entwurfsentscheidungen definiert, die Organisationen zum Festlegen ihrer Azure-Journey treffen müssen.

Nicht alle Unternehmen führen Azure auf die gleiche Weise ein, sodass die Unternehmensarchitektur zwischen Kunden variieren kann. Letztlich können die technischen Überlegungen und Entwurfsempfehlungen der unternehmensweiten Architektur je nach Kundenszenario zu unterschiedlichen Kompromissen führen. Gewisse Abweichungen werden erwartet. Wenn jedoch die wichtigsten Empfehlungen befolgt werden, ebnet die resultierende Zielarchitektur für den Kunden den Weg für eine nachhaltigere Skalierung.

## <a name="prescriptive-guidance"></a>Ausführlicher Leitfaden

Die Unternehmensarchitektur bietet eine ausführliche Anleitung sowie bewährte Azure-Methoden. Sie berücksichtig zudem die Entwurfsprinzipien für die kritischen Entwurfsbereiche für die Azure-Umgebung des Kunden.

## <a name="qualifiers-should-i-start-with-enterprise-scale"></a>Qualifizierer: Sollte ich auf Unternehmensniveau beginnen?

Die Unternehmensarchitektur ist entwurfsbedingt modular aufgebaut und ermöglicht es den Kunden, mit grundlegenden Zielzonen zu beginnen, die ihr Anwendungsportfolio unterstützen, unabhängig davon, ob die Anwendungen migriert werden oder neu entwickelt und in Azure bereitgestellt werden. Die Architektur kann unabhängig vom Skalierungspunkt parallel zu den Geschäftsanforderungen des Kunden skaliert werden.

## <a name="start-with-an-enterprise-scale-landing-zone"></a>Beginnen mit einer Zielzone auf Unternehmensebene

Der unternehmensweite Ansatz zum Erstellen von Zielzonen umfasst vier Assetsätze zur Unterstützung von Cloudteams:

- [Entwurfsrichtlinien:](./design-guidelines.md) Leitfaden zu den wichtigen Entscheidungen, die den Entwurf der CAF-Zielzone auf Unternehmensebene steuern
- [Architektur:](./architecture.md) Konzeptionelle Referenzarchitektur, in der Entwurfsbereiche und bewährte Methoden veranschaulicht werden
- [Implementierungen:](./implementation.md) Azure Resource Manager-Vorlage der Architektur zur Beschleunigung der Einführung

<!-- TODO: Reinstate once template.md is ready. 
- [Template](./template.md): A documentation template to quickly capture decisions and any deviation from the suggested architecture or implementation.
-->

## <a name="community"></a>Community

<!-- docsTest:ignore "Cloud Solutions Unit" -->

Dieser Leitfaden wird größtenteils von Microsoft-Architekten und der breit angelegten technischen Community der Cloudlösungseinheit entwickelt. Diese Community aktualisiert diesen Leitfaden regelmäßig, um die bei einer unternehmensweiten Einführung gewonnenen Erkenntnisse zu teilen.

Dieser Leitfaden enthält zwar die gleichen Entwurfsprinzipien wie die Standardmethode „Bereitschaft“, erweitert aber diese Prinzipien, um Themen wie Governance und Sicherheit früher im Planungsprozess zu integrieren. Die Ausweitung des Standardprozesses ist aufgrund einiger natürlicher Annahmen notwendig, die getroffen werden können, wenn eine Einführung umfangreiche Unternehmensänderungen erfordert.

## <a name="next-steps"></a>Nächste Schritte

[Implementieren einer CAF-Zielzone auf Unternehmensebene](./implementation.md)

> [!div class="nextstepaction"]
> [Implementieren einer CAF-Zielzone auf Unternehmensebene](./implementation.md)
