---
title: Organisieren und Verwalten mehrerer Azure-Abonnements
description: Verwenden Sie das Cloud Adoption Framework für Azure, um zu erfahren, wie Sie eine Verwaltungsgruppenhierarchie erstellen, um die Verwaltung Ihrer Abonnements und Ressourcen zu vereinfachen.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 0e9115387360b46015114d6069fcedb9afb43d58
ms.sourcegitcommit: 568037e0d2996e4644c11eb61f96362a402759ec
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/16/2020
ms.locfileid: "84799652"
---
# <a name="organize-and-manage-multiple-azure-subscriptions"></a>Organisieren und Verwalten mehrerer Azure-Abonnements

Wenn Sie nur über wenige Abonnements verfügen, ist deren unabhängige Verwaltung relativ einfach. Sobald die Anzahl Ihrer Abonnements zunimmt, sollten Sie jedoch zur Verwaltung der Abonnements und Ressourcen eine Verwaltungsgruppenhierarchie erstellen.

## <a name="azure-management-groups"></a>Azure-Verwaltungsgruppen

Azure-Verwaltungsgruppen ermöglichen eine effiziente Verwaltung von Zugriff, Richtlinien und Compliance für die Abonnements einer Organisation. Jede Verwaltungsgruppe ist ein Container für ein oder mehrere Abonnements.

Verwaltungsgruppen werden in einer einzigen Hierarchie angeordnet. Sie definieren diese Hierarchie in Ihrem Azure AD-Mandanten, um sie an der Struktur und den Anforderungen Ihrer Organisation auszurichten. Die oberste Ebene wird als _Stammverwaltungsgruppe_ bezeichnet. Sie können bis zu sechs Ebenen von Verwaltungsgruppen in der Hierarchie definieren. Jedes Abonnement gehört nur zu einer einzigen Verwaltungsgruppe.

Der Verwaltungsbereich von Azure umfasst vier Ebenen:

- Verwaltungsgruppen
- Abonnements
- Ressourcengruppen
- Ressourcen

Alle Zugriffsrichtlinien oder anderen Richtlinien, die auf einer bestimmten Hierarchieebene angewendet werden, werden von den darunter liegenden Ebenen geerbt. Ein Ressourcen- oder Abonnementbesitzer kann eine geerbte Richtlinie nicht ändern. Diese Einschränkung trägt zur Verbesserung der Governance bei.

> [!NOTE]
> Eine Tagvererbung wird derzeit noch nicht unterstützt, aber in Kürze verfügbar sein.

Mit diesem Vererbungsmodell können Sie die Abonnements in Ihrer Hierarchie so anordnen, dass jedes Abonnement die entsprechenden Richtlinien und Sicherheitsvorgaben erfüllt.

![Vier Bereichsebenen zum Organisieren Ihrer Azure-Ressourcen](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Jede Zugriffs- oder Richtlinienzuweisung in der Stammverwaltungsgruppe gilt für alle Ressourcen im Verzeichnis. Überlegen Sie sorgfältig, welche Elemente Sie in diesem Bereich definieren. Fügen Sie nur die Zuordnungen hinzu, über die Sie verfügen müssen.

## <a name="create-your-management-group-hierarchy"></a>Erstellen Ihrer Verwaltungsgruppenhierarchie

Beim Definieren Ihrer Verwaltungsgruppenhierarchie erstellen Sie als Erstes die Stammverwaltungsgruppe. Anschließend verschieben Sie alle vorhandenen Abonnements im Verzeichnis in die Stammverwaltungsgruppe. Neue Abonnements werden immer in der Stammverwaltungsgruppe erstellt. Sie können sie später in eine andere Verwaltungsgruppe verschieben.

Wenn Sie ein Abonnement in eine vorhandene Verwaltungsgruppe verschieben, erbt es die Richtlinien und Rollenzuweisungen aus der darüber liegenden Verwaltungsgruppenebene. Nachdem Sie mehrere Abonnements für Ihre Azure-Workloads eingerichtet haben, können Sie weitere Abonnements für die Azure-Dienste erstellen, die mit anderen Abonnements gemeinsam genutzt werden.

Wenn Sie davon ausgehen, dass Ihre Azure-Umgebung wächst, sollten Sie jetzt Verwaltungsgruppen für Produktion und Nichtproduktion erstellen und geeignete Richtlinien und Zugriffssteuerungen auf der Verwaltungsgruppenebene anwenden. Neue Abonnements erben die entsprechenden Kontrollen, wenn Sie den Verwaltungsgruppen hinzugefügt werden.

![Beispiel für eine Verwaltungsgruppenhierarchie](../../_images/ready/management-group-hierarchy-v2.png)

## <a name="example-use-cases"></a>Beispiele für Anwendungsfälle

Im Anschluss folgen einige einfache Beispiele für die Trennung verschiedener Workloads mithilfe von Verwaltungsgruppen:

- **Produktions- und Nichtproduktionsworkloads:** Verwenden Sie Verwaltungsgruppen, um die Verwaltung verschiedener Rollen und Richtlinien für Produktions- und Nichtproduktionsabonnements zu vereinfachen. Beispielsweise können Nichtproduktionsabonnements Entwicklern Zugriff für Mitwirkende gewähren, während sie in der Produktion nur Lesezugriff haben.
- **Interne Dienste und externe Dienste:** Unternehmen haben oft unterschiedliche Anforderungen, Richtlinien und Rollen für interne Dienste und externe kundenorientierte Dienste.

## <a name="related-resources"></a>Zugehörige Ressourcen

In den folgenden Ressourcen erfahren Sie mehr über das Organisieren und Verwalten Ihrer Azure-Ressourcen.

- [Organisieren Ihrer Ressourcen mit Azure-Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups)
- [Erhöhen der Zugriffsrechte zum Verwalten aller Azure-Abonnements und Verwaltungsgruppen](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin)
- [Verschieben von Azure-Ressourcen in eine andere Ressourcengruppe oder ein anderes Abonnement](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription)

## <a name="next-steps"></a>Nächste Schritte

Sehen Sie sich die [empfohlenen Namens- und Kennzeichnungskonventionen](./naming-and-tagging.md) an, die Sie beim Bereitstellen Ihrer Azure-Ressourcen befolgen sollten.

> [!div class="nextstepaction"]
> [Empfohlene Namens- und Kennzeichnungskonventionen](./naming-and-tagging.md)
