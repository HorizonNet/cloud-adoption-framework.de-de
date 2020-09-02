---
title: Verbessern der ersten Grundlage für die Cloud Governance
description: Verwenden Sie das Framework für die Cloudeinführung (Cloud Adoption Framework) für Azure, um zu erfahren, wie Sie die erste Grundlage für die Cloudgovernance inkrementell verbessern.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 86011f103fcdecb12ad1448c028453a9f229113a
ms.sourcegitcommit: 07d56209d56ee199dd148dbac59671cbb57880c0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88881052"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Verbessern der ersten Grundlage für die Cloud Governance

In diesem Artikel wird davon ausgegangen, dass Sie eine [anfängliche Grundlage für die Cloud Governance](./initial-foundation.md) eingerichtet haben. Bei der Implementierung Ihres Cloudeinführungsplans ergeben sich konkrete Risiken aus den vorgeschlagenen Ansätzen, mit denen Teams die Cloud einführen möchten. Da diese Risiken in Unterhaltungen zur Releaseplanung auftreten, verwenden Sie das folgende Raster, um schnell einige bewährte Methoden zu identifizieren, mit denen Sie den Einführungsplan beschleunigen können, um zu verhindern, dass Risiken zu echten Bedrohungen werden.

## <a name="maturity-vectors"></a>Einsatzreifevektoren

Die folgenden bewährten Methoden können jederzeit auf die ursprüngliche Governancegrundlage angewendet werden, um das in der folgenden Tabelle genannte Risiko bzw. den entsprechenden Bedarf zu berücksichtigen.

> [!IMPORTANT]
> Die Organisation der Ressourcen kann sich darauf auswirken, wie diese bewährten Methoden angewendet werden. Es ist wichtig, mit den Empfehlungen zu beginnen, die am besten für die erste Governancegrundlage geeignet sind, die Sie im vorherigen Schritt implementiert haben.

| Risiko/Bedarf | Standardunternehmen | Komplexes Unternehmen |
|---|---|---|
| Vertrauliche Daten in der Cloud | [Verbesserung der Disziplin](./guides/standard/security-baseline-improvement.md) | [Verbesserung der Disziplin](./guides/complex/security-baseline-improvement.md) |
| Unternehmenskritische Anwendungen in der Cloud | [Verbesserung der Disziplin](./guides/standard/resource-consistency-improvement.md) | [Verbesserung der Disziplin](./guides/complex/resource-consistency-improvement.md) |
| Kostenmanagement für die Cloud | [Verbesserung der Disziplin](./guides/standard/cost-management-improvement.md) | [Verbesserung der Disziplin](./guides/complex/cost-management-improvement.md) |
| Verwenden mehrerer Clouds | [Verbesserung der Disziplin](./guides/standard/multicloud-improvement.md) | [Verbesserung der Disziplin](./guides/complex/multicloud-improvement.md) |
| Komplexe/Legacy-Identitätsverwaltung | – | [Verbesserung der Disziplin](./guides/complex/identity-baseline-improvement.md) |
| Mehrere Governance-Ebenen | – | [Verbesserung der Disziplin](./guides/complex/multiple-layers-of-governance.md) |

## <a name="next-steps"></a>Nächste Schritte

Sie können nicht nur bewährte Methoden anwenden, sondern auch die Governancemethodik des Cloud Adoption Framework an konkrete Geschäftsanforderungen anpassen. Nach Befolgung der entsprechenden Empfehlungen müssen Sie die [Unternehmensrichtlinie bewerten, um zusätzliche Anpassungsanforderungen zu verstehen](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Auswerten der Unternehmensrichtlinie](./corporate-policy.md)
