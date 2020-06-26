---
title: Bereitstellen einer CAF-Zielzone auf Unternehmensebene in Azure
description: Erfahren Sie, wie Sie in Azure eine Landezone für die Migration bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 0bd70384bbf5bd5c547d8fb364e70e275900b8bf
ms.sourcegitcommit: 9b183014c7a6faffac0a1b48fdd321d9bbe640be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85074969"
---
# <a name="deploy-an-enterprise-scale-landing-zone"></a>Bereitstellen einer Zielzone auf Unternehmensebene

Eine _Zielzone auf Unternehmensebene_ ist eine Umgebung, die mit allen unterstützenden Ressourcen für das Hosten komplexerer Workloads ausgestattet ist. Beginnend mit einer Zielzone auf Unternehmensebene können Sie von der ersten Bereitstellung an unternehmenskritische und sichere Workloads in Übereinstimmung mit Sicherheits-, Governance-, Compliance- und Betriebsanforderungen hosten.

## <a name="approach"></a>Vorgehensweise

Der in der Bereitschaftsmethodik beschriebene Ansatz _Klein anfangen_ beginnt mit einer einzigen Zielzone und bindet umfassendere Unternehmensfeatures ein, während der Cloudeinführungsplan in Richtung Unternehmensebene durchlaufen wird. Durch diesen Ansatz wird ein strukturierter, praktischer Lernpfad geschaffen, der auf die Bedürfnisse der jeweiligen Release- oder Migrationswelle abgestimmt ist. Mit diesem Ansatz könnten die Zielzonen zwar Workloads in der Produktion unterstützen, aber sie sind bei den ersten paar Releases noch nicht wirklich unternehmenstauglich.

Wenn Kunden schneller zur Unternehmensbereitschaft gelangen müssen, ist eine komplexere Architektur erforderlich. Eine einzelne Zielzone auf Unternehmensebene kann isoliert keine Leistung bieten. Eine unternehmensweite Architektur erfordert eine unternehmenstaugliche Umgebung, die unternehmenstaugliche Zielzonen aufweist. Beide Ansätze folgen den gleichen Prinzipien und bewährten Methoden. Aber der unternehmensweite Ansatz setzt mehrere bewährte Methoden mittels einer einzigen JSON-Datei um, die eine GitHub-Aktions- und Bereitstellungspipeline nutzt, um alle Aspekte der Umgebung einschließlich mehrerer Zielzonen bereitzustellen. Diese äußerst wertende Implementierung nutzt die gleiche ARM-Vorlage, Azure Policy und dieselben RBAC-Tools, die in den kleineren Blaupausenansätzen zum Einsatz kommen.

Nach der Bereitstellung folgen beide Ansätze den Infrastructure-as-Code- und testgesteuerten Entwicklungsmodellen, um die Zielzonen so zu erweitern, dass sie die deren künftige Anforderungen erfüllen.

## <a name="deploy-the-first-landing-zone"></a>Bereitstellen Ihrer ersten Zielzone

Bevor Sie den Ansatz und die Implementierung auf Unternehmensebene umsetzen, sollten Sie die folgenden Annahmen, Entscheidungen und Implementierungsleitlinien erneut prüfen. Wenn dieser Leitfaden im Einklang mit Ihrem Cloudeinführungsplan ist, kann die Bereitstellung der unternehmensweiten Umgebung und Zielzone mithilfe der [ unternehmensweiten Implementierung](../enterprise-scale/implementation.md) erfolgen.

> [!div class="nextstepaction"]
> [Implementieren einer Zielzonenlösung auf Unternehmensebene](../enterprise-scale/implementation.md)

## <a name="assumptions"></a>Annahmen

Dieser Ansatz und diese Architektur beruhen auf den folgenden Annahmen. Wenn diese Annahmen mit Ihren Bedürfnissen und Einschränkungen übereinstimmen, können Sie die Implementierung nutzen, um Ihre Umgebung zu konfigurieren und Ihre erste Zielzone bereitzustellen. Nach der Bereitstellung kann die Implementierung durch Erweiterung der Zielzonen und Umgebung benutzerdefiniert angepasst werden, um Ihren künftigen Anforderungen an die Zielzone zu entsprechen.

- **Grenzwerte für Abonnements**: Im Gegensatz zu den anderen Zielzonenoptionen ist diese Architektur nicht durch [Grenzwerte für Abonnements](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits) eingeschränkt.
- **Compliance**: Complianceanforderungen von Dritten werden durch diese Implementierung nicht bereitgestellt, können aber mühelos hinzugefügt werden.
- **Komplexität der Architektur:** Im Gegensatz zu den anderen Optionen gibt es keine Einschränkungen hinsichtlich der Komplexität der Architektur der Workloads, die in dieser Zielzone und Umgebung gehostet werden können.
- **Gemeinsame Dienste**: Gemeinsame Dienste werden in Einklang mit bewährten Methoden von Microsoft konfiguriert.
- **Begrenzter Produktionsbereich:** Diese Standardkonfiguration für Zielzonen wird eher Ihren Anforderungen an das Hosten unternehmenskritischer und sensibler Daten gerecht.
- **Erweiterte Kenntnisse erforderlich:** Die erforderlichen technischen Fähigkeiten sind bei Teams, die diesen Ansatz umsetzen, wesentlich höher. In der [Übersicht zu Zielzonen auf Unternehmensebene](../enterprise-scale/index.md) erfahren Sie mehr über die erforderlichen technischen Fähigkeiten.

Wenn diese Annahmen mit Ihren aktuellen Anforderungen in Bezug auf die Einführung übereinstimmen, ist diese Implementierung möglicherweise ein guter Ausgangspunkt zum Erstellen von Zielzonen und Umgebungen.

## <a name="decisions"></a>Entscheidungen

In den [Implementierungsrichtlinien](../enterprise-scale/implementation-guidelines.md) finden Sie sämtliche Entscheidungen, die die Implementierung auf Unternehmensebene prägen.

## <a name="customize-or-deploy-a-landing-zone"></a>Anpassen oder Bereitstellen einer Zielzone

Ein Beispiel für die Bereitstellung der Implementierung auf Unternehmensebene finden Sie im [Leitfaden für die Implementierung auf Unternehmensebene für Contoso](https://github.com/Azure/Enterprise-Scale/blob/main/docs/reference/contoso/Readme.md).

Informationen zum Anpassen der unternehmensweiten Architektur finden Sie in den [Entwurfsrichtlinien](../enterprise-scale/design-guidelines.md).

## <a name="next-steps"></a>Nächste Schritte

Nach Bereitstellen Ihrer ersten Zielzone können Sie Ihre [Zielzone erweitern](../considerations/index.md).

> [!div class="nextstepaction"]
> [Erweitern der Zielzone](../considerations/index.md)
