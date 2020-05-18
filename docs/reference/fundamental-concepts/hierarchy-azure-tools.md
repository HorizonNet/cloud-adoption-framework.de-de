---
title: Wie unterstützen die Azure-Produkte die Portfoliohierarchie?
description: Wie unterstützen die Azure-Produkte die Portfoliohierarchie?
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c4ab25ee9cf9a72f6b5a5750157601510d5d050d
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83230634"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-do-azure-products-support-the-portfolio-hierarchy"></a>Wie unterstützen die Azure-Produkte die Portfoliohierarchie?

In [Verstehen und Ausrichten der Portfoliohierarchie](./hosting-hierarchy.md) wurde durch eine Reihe von Definitionen für die Portfoliohierarchie und die Rollenzuordnung eine Bereichshierarchie für die meisten Portfolioansätze festgelegt. Wie in diesem Artikel beschrieben, benötigen Sie möglicherweise nicht jede der nachstehend beschriebenen Ebenen oder jeden der nachstehenden _Bereiche_. Die Minimierung der Anzahl der Ebenen reduziert die Komplexität, sodass diese Ebenen nicht alle als erforderliche bewährte Methode angesehen werden sollten.

In diesem Artikel wird gezeigt, wie jede Ebene oder jeder Bereich der Hierarchie in Azure durch Organisationstools, Bereitstellungs- und Governancetools und einige Lösungen im Cloud Adoption Framework unterstützt wird.

## <a name="organizing-the-hierarchy-in-azure"></a>Organisieren der Hierarchie in Azure

Azure Resource Manager umfasst mehrere organisatorische Ansätze, die bei der Organisation von Objekten auf jeder Ebene der Cloudhierarchie helfen.

> [!NOTE]
> Die folgenden Schieberegler zeigen gängige Varianten in der Ausrichtung. Die grauen Teile der Gleitschienen sind üblich, sollten aber nur dann verwendet werden, wenn eine bestimmte Geschäftsanforderung dies erfordert. Die Punkte, die der nachstehenden Abbildung folgen, beschreiben nur die vorgeschlagene bewährte Methode.

![An der Hierarchie ausgerichtete Ressourcenorganisation](../../_images/ready/hierarchy-with-organizing-tools.png)

- **Portfolio:** Die Unternehmens- oder Geschäftseinheit wird wahrscheinlich keine technischen Objekte enthalten, könnte sich aber auf die Kostenentscheidungen auswirken. Die Unternehmens- und Geschäftseinheiten sollten in den Stammknoten der Verwaltungsgruppenhierarchie dargestellt werden.
- **Cloudplattformen:** Jede Umgebung sollte über einen eigenen Knoten in der Verwaltungsgruppenhierarchie verfügen.
- **Zielzonen und Plattformumgebungen:** Jede Zielzone sollte als Abonnement dargestellt werden. Ebenso sollten Plattformumgebungen in ihren eigenen Abonnements enthalten sein. Es gibt verschiedene Abonnemententwürfe, die ein Abonnement pro Cloud oder pro Workload erfordern könnten, wodurch sich das Organisationstool für jedes einzelne ändern würde.
- **Workload:** Jede Workload sollte als eine Ressourcengruppe dargestellt werden. Ressourcengruppen werden auch häufig verwendet, um Lösungen, Bereitstellungen oder andere technische Gruppierungen von Objekten darzustellen.
- **Objekt:** Jedes Objekt wird grundsätzlich als Ressource in Azure dargestellt.

### <a name="organize-with-tags"></a>Organisieren mit Tags

Abweichungen von der bewährten Methode sind üblich. Abweichungen von der oben genannten bewährten Methode sollten aufgezeichnet werden, indem alle Objekte mit einem Tag versehen werden, das jede der relevanten Ebenen der Hierarchie repräsentiert. Weitere Informationen finden Sie unter [Empfohlene Namens- und Kennzeichnungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md).
