---
title: Erste Schritte mit Cloud Adoption Framework-Zielzonen auf Unternehmensebene
description: Verwenden Sie das Microsoft Cloud Adoption Framework für Azure für die ersten Schritte mit CAF-Zielzonen auf Unternehmensebene.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 34c8ca965ff323595b7ac0f38814168b646b3ed3
ms.sourcegitcommit: d31a9043d1ae9283ed126bf118ca26d1d18d6948
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88040812"
---
# <a name="start-with-cloud-adoption-framework-enterprise-scale-landing-zones"></a>Erste Schritte mit Cloud Adoption Framework-Zielzonen auf Unternehmensebene

Die Unternehmensarchitektur stellt den strategischen Entwurfspfad und den technischen Zielstatus für Ihre Azure-Umgebung dar. Sie wird weiterhin parallel zur Azure-Plattform weiterentwickelt und durch die verschiedenen Entwurfsentscheidungen definiert, die Organisationen zum Ausarbeiten ihrer Azure-Journey treffen müssen.

Nicht alle Unternehmen wenden Azure auf dieselbe Weise an, sodass die Architektur für Cloud Adoption Framework-Zielzonen für Azure auf Unternehmensebene für Azure von Kunde zu Kunde unterschiedlich ist. Die technischen Überlegungen und Entwurfsempfehlungen der unternehmensweiten Architektur können je nach Szenario Ihrer Organisation zu unterschiedlichen Kompromissen führen. Gewisse Abweichungen werden erwartet. Wenn Sie jedoch die wichtigsten Empfehlungen befolgen, ebnet die resultierende Zielarchitektur für Ihre Organisation den Weg für eine nachhaltigere Skalierung.

## <a name="prescriptive-guidance"></a>Ausführlicher Leitfaden

Die Unternehmensarchitektur bietet eine ausführliche Anleitung sowie bewährte Azure-Methoden. Sie berücksichtig zudem die Entwurfsprinzipien für die kritischen Entwurfsbereiche für die Azure-Umgebung einer Organisation.

## <a name="qualifiers-should-i-start-with-enterprise-scale"></a>Qualifizierer: Sollte ich auf Unternehmensniveau beginnen?

Die Architektur auf Unternehmensebene ist entwurfsbedingt modular aufgebaut. Sie ermöglicht es Ihnen, mit grundlegenden Zielzonen zu beginnen, die Ihr Anwendungsportfolio unterstützen, unabhängig davon, ob die Anwendungen migriert werden oder neu entwickelt und in Azure bereitgestellt werden. Die Architektur kann unabhängig vom Skalierungspunkt parallel zu Ihren Geschäftsanforderungen skaliert werden.

## <a name="start-with-a-cloud-adoption-framework-enterprise-scale-landing-zone"></a>Erste Schritte mit einer Cloud Adoption Framework-Zielzone auf Unternehmensebene

Der unternehmensweite Ansatz zum Erstellen von Zielzonen umfasst drei Assetsätze zur Unterstützung von Cloudteams:

- [Entwurfsrichtlinien:](./design-guidelines.md) Leitfaden zu den wichtigen Entscheidungen, die den Entwurf der Cloud Adoption Framework-Zielzone für Azure auf Unternehmensebene steuern
- [Architektur:](./architecture.md) Konzeptionelle Referenzarchitektur, in der Entwurfsbereiche und bewährte Methoden veranschaulicht werden
- [Implementierungen:](./implementation.md) Azure Resource Manager-Vorlage der Architektur zur Beschleunigung der Einführung

<!-- TODO: Reinstate once template.md is ready.
- [Template](./template.md): A documentation template to quickly capture decisions and any deviation from the suggested architecture or implementation.
-->

## <a name="community"></a>Community

<!-- docsTest:ignore "Cloud Solutions Unit" -->

Dieser Leitfaden wird größtenteils von Microsoft-Architekten und der breit angelegten technischen Community der Cloudlösungseinheit entwickelt. Diese Community aktualisiert diesen Leitfaden regelmäßig, um die bei einer unternehmensweiten Einführung gewonnenen Erkenntnisse zu teilen.

Dieser Leitfaden enthält die gleichen Entwurfsprinzipien wie die Standardmethode „Bereitschaft“. Er erweitert diese Prinzipien, um Themen wie Governance und Sicherheit früher im Planungsprozess zu integrieren. Die Ausweitung des Standardprozesses ist aufgrund einiger natürlicher Annahmen notwendig, die getroffen werden können, wenn eine Einführung umfangreiche Unternehmensänderungen erfordert.

## <a name="next-steps"></a>Nächste Schritte

[Implementieren einer Cloud Adoption Framework-Zielzone auf Unternehmensebene](./implementation.md)
