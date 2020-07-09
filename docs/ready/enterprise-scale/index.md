---
title: Erste Schritte mit CAF-Zielzonen auf Unternehmensebene
description: Verwenden Sie das Microsoft Cloud Adoption Framework für Azure für die ersten Schritte mit CAF-Zielzonen auf Unternehmensebene.
author: BrianBlanchard
ms.author: brblanch
ms.date: 06/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: cdd5e1bcee951d2437183a8514a944c92c075c93
ms.sourcegitcommit: 4bbd5f6444d033ef1f38dc6f3bad7b914a82f68f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128327"
---
# <a name="start-with-caf-enterprise-scale-landing-zones"></a>Erste Schritte mit CAF-Zielzonen auf Unternehmensebene

Die Unternehmensarchitektur stellt den strategischen Entwurfspfad und den technischen Zielstatus für Ihre Azure-Umgebung dar. Sie wird weiterhin parallel zur Azure-Plattform weiterentwickelt und letztendlich durch die verschiedenen Entwurfsentscheidungen definiert, die Organisationen zum Festlegen ihrer Azure-Journey treffen müssen.

Nicht alle Unternehmen führen Azure auf die gleiche Weise ein, sodass die Unternehmensarchitektur zwischen verschiedenen Organisationen variieren kann. Letztlich können die technischen Überlegungen und Entwurfsempfehlungen der unternehmensweiten Architektur je nach dem Szenario Ihrer Organisation zu unterschiedlichen Kompromissen führen. Gewisse Abweichungen werden erwartet. Wenn jedoch die wichtigsten Empfehlungen befolgt werden, ebnet die resultierende Zielarchitektur für Ihre Organisation den Weg für eine nachhaltigere Skalierung.

## <a name="prescriptive-guidance"></a>Ausführlicher Leitfaden

Die Unternehmensarchitektur bietet eine ausführliche Anleitung sowie bewährte Azure-Methoden. Sie berücksichtigt zudem die Entwurfsprinzipien für die kritischen Entwurfsbereiche für die Azure-Umgebung einer Organisation.

## <a name="qualifiers-should-i-start-with-enterprise-scale"></a>Qualifizierer: Sollte ich auf Unternehmensniveau beginnen?

Die Unternehmensarchitektur ist entwurfsbedingt modular aufgebaut und ermöglicht es Ihnen, mit grundlegenden Zielzonen zu beginnen, die Ihr Anwendungsportfolio unterstützen, unabhängig davon, ob die Anwendungen migriert werden oder neu entwickelt und in Azure bereitgestellt werden. Die Architektur kann unabhängig vom Skalierungspunkt parallel zu Ihren Geschäftsanforderungen skaliert werden.

## <a name="start-with-a-caf-enterprise-scale-landing-zone"></a>Erste Schritte mit einer CAF-Zielzone auf Unternehmensebene

Der unternehmensweite Ansatz zum Erstellen von Zielzonen umfasst drei Assetsätze zur Unterstützung von Cloudteams:

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
