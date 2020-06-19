---
title: Wie unterstützen die Azure-Produkte die Portfoliohierarchie?
description: Wie unterstützen die Azure-Produkte die Portfoliohierarchie?
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ae57f79aeb4976a2c6306728f354ab972f3b33e3
ms.sourcegitcommit: d88c1cc3597a83ab075606d040ad659ac4b33324
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84788114"
---
# <a name="how-do-azure-products-support-the-portfolio-hierarchy"></a>Wie unterstützen die Azure-Produkte die Portfoliohierarchie?

In [Verstehen und Ausrichten der Portfoliohierarchie](./hosting-hierarchy.md) wurde durch eine Reihe von Definitionen für die Portfoliohierarchie und die Rollenzuordnung eine Bereichshierarchie für die meisten Portfolioansätze festgelegt. Wie in diesem Artikel beschrieben, benötigen Sie möglicherweise nicht jede der nachstehend beschriebenen Ebenen oder jeden der nachstehenden _Bereiche_. Die Minimierung der Anzahl der Ebenen reduziert die Komplexität, sodass diese Ebenen nicht alle Anforderung angesehen werden sollten.

In diesem Artikel wird gezeigt, wie jede Ebene oder jeder Bereich der Hierarchie in Azure durch Organisationstools, Bereitstellungs- und Governancetools und einige Lösungen im Microsoft Cloud Adoption Framework für Azure unterstützt wird.

## <a name="organizing-the-hierarchy-in-azure"></a>Organisieren der Hierarchie in Azure

Azure Resource Manager umfasst mehrere organisatorische Ansätze, die bei der Organisation von Objekten auf jeder Ebene der Cloudhierarchie helfen.

Die Schieberegler in der folgenden Abbildung zeigen gängige Varianten in der Ausrichtung. Die grauen Teile der Schieberegler sind üblich, sollten aber nur für bestimmte Geschäftsanforderungen verwendet werden. Die Punkte neben der Abbildung beschreiben eine empfohlene bewährte Methode.

![An der Hierarchie ausgerichtete Ressourcenorganisation](../../_images/ready/hierarchy-with-organizing-tools.png)

- **Portfolio:** Die Unternehmens- oder Geschäftseinheit wird wahrscheinlich keine technischen Ressourcen enthalten, könnte sich aber auf die Kostenentscheidungen auswirken. Die Unternehmens- und Geschäftseinheiten werden in den Stammknoten der Verwaltungsgruppenhierarchie dargestellt.
- **Cloudplattformen:** Jede Umgebung verfügt in der Verwaltungsgruppenhierarchie über einen eigenen Knoten.
- **Zielzonen und Cloudumgebung:** Jede Zielzone wird als Abonnement dargestellt. Ebenso sind Plattformumgebungen in ihren eigenen Abonnements enthalten. Einige Abonnemententwürfe erfordern möglicherweise ein Abonnement pro Cloud oder pro Workload, wodurch sich das Organisationstool jeweils ändern würde.
- **Workloads:** Jede Workload wird als eine Ressourcengruppe dargestellt. Ressourcengruppen werden häufig verwendet, um Lösungen, Bereitstellungen oder andere technische Gruppierungen von Ressourcen darzustellen.
- **Ressourcen:** Jedes Objekt wird grundsätzlich als Ressource in Azure dargestellt.

## <a name="organizing-with-tags"></a>Organisieren mit Tags

Abweichungen von der bewährten Methode sind üblich. Sie können sie aufzeichnen, indem Sie alle Ressourcen kennzeichnen. Verwenden Sie ein Tag, um die einzelnen relevanten Ebenen der Hierarchie darzustellen. Weitere Informationen finden Sie unter [Empfohlene Namens- und Kennzeichnungskonventionen](../../ready/azure-best-practices/naming-and-tagging.md).
