---
title: Überlegungen zu Landezonen in Azure
description: Verwenden Sie das Framework für die Cloudeinführung für Azure, um mehr über Zielzonen – den Grundbausteinen jeder Cloudeinführungsumgebung – zu erfahren.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/09/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 335c323ce5669d82c5751a0ee58867b3c792b3fd
ms.sourcegitcommit: 71a4f33546443d8c875265ac8fbaf3ab24ae8ab4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/20/2020
ms.locfileid: "86479760"
---
# <a name="landing-zone-considerations"></a>Überlegungen zu Landezonen

Eine Landezone ist der Grundbaustein jeder Cloudeinführungsumgebung. Der Begriff _Landezone_ bezeichnet eine Umgebung, die zum Hosten von Workloads in einer Cloudumgebung wie Azure bereitgestellt und vorbereitet wurde. Bei jeder Iteration der Bereitschaftsmethodik des Frameworks für die Cloudeinführung (Cloud Adoption Framework) wird letztendlich eine voll funktionsfähige Landezone angestrebt.

![Überlegungen zu Landezonen](../../_images/ready/landing-zone-considerations.png)
_Abbildung 1: Überlegungen zu Landezonen._

Diese Abbildung zeigt die wichtigsten Überlegungen bei der Implementierung einer Landezonenbereitstellung. Die Überlegungen können in drei Kategorien unterteilt werden: Hosting, Azure-Grundlagen und Governance.

## <a name="hosting-considerations"></a>Überlegungen zum Hosting

Landezonen stellen eine Struktur für Hostingoptionen bereit. Die Struktur wird explizit über Governancekontrollen oder organisch durch die Einführung von Diensten innerhalb der Landezone erstellt. Die Informationen in den folgenden Artikeln helfen Ihnen beim Treffen von Entscheidungen, die in die Blaupause oder in andere Automatisierungsskripts zur Erstellung Ihrer Landezone einfließen:

- [Entscheidungen zum Computeentwurf](./compute-options.md): Richten Sie Computeoptionen auf den Zweck der Landezone aus, um die operative Komplexität zu minimieren. Diese Entscheidung kann mithilfe von Automatisierungstoolketten wie Azure Policy-Initiativen und Landezonen erzwungen werden.
- [Entscheidungen zum Speicherentwurf](./storage-options.md): Wählen Sie die richtige Azure Storage-Lösung für Ihre Workloadanforderungen aus.
- [Entscheidungen zum Netzwerkentwurf](./networking-options.md): Wählen Sie die Netzwerkdienste, -tools und -architekturen aus, die die Workload-, Governance- und Konnektivitätsanforderungen Ihrer Organisation unterstützen.
- [Entscheidungen zum Datenbankentwurf](./data-options.md): Hier erfahren Sie, welche Datenbanktechnologie am besten für Ihre Workloadanforderungen geeignet ist.

## <a name="azure-fundamentals"></a>Azure-Grundlagen

Jede Landezone ist Teil einer umfassenderen Lösung zur Strukturierung von Ressourcen innerhalb einer Cloudumgebung. Bei den Azure-Grundlagen handelt es sich um die Grundbausteine einer Struktur.

- [Grundlegende Konzepte in Azure](./fundamental-concepts.md): Lernen Sie grundlegende Konzepte und Begriffe kennen, die zum Organisieren von Ressourcen in Azure verwendet werden, und erfahren Sie, wie diese Konzepte zusammenhängen.
- [Leitfaden zur Entscheidungsfindung bei der Ressourcenkonsistenz](../../decision-guides/resource-consistency/index.md): Nachdem Sie sich mit den einzelnen Grundlagen vertraut gemacht haben, können Sie den Leitfaden zur Entscheidungsfindung für die Ressourcenstrukturierung heranziehen, um Entscheidungen zur Gestaltung der Landezone zu treffen.

## <a name="governance-considerations"></a>Governanceüberlegungen

Die Governancemethodik des Frameworks für die Cloudeinführung (Cloud Adoption Framework) bietet einen Prozess für die allgemeine Umgebungssteuerung. In zahlreichen Anwendungsfällen müssen Sie möglicherweise Governanceentscheidungen für jede einzelne Zielzone treffen. In vielen Szenarien werden Governancebaselines zwar ganzheitlich eingerichtet, aber für einzelne Zielzonen erzwungen. Dies gilt für die ersten Landezonen, die eine Organisation bereitstellt.

Die folgenden Artikel unterstützen Sie beim Treffen governancebezogener Entscheidungen zur Landezone. Sie können jede Entscheidung in Ihre Governancebaselines einbeziehen.

- **Kostenanforderungen:** Abhängig von den Beweggründen für die Cloudeinführung und den betrieblichen Verpflichtungen, die für diese Umgebung bestehen, müssen möglicherweise verschiedene Kostenverwaltungskonfigurationen für die Landezone geändert werden.
- **Überwachungsentscheidungen:** Abhängig von den betrieblichen Anforderungen für eine Landezone können verschiedene Überwachungstools bereitgestellt werden. Der Artikel zu Überwachungsentscheidungen unterstützt Sie bei der Ermittlung der hierfür am besten geeigneten Tools.
- **Rollenbasierte Zugriffssteuerung.** Die [rollenbasierte Zugriffssteuerung](../considerations/roles.md) (Role-Based Access Control, RBAC) in Azure ermöglicht eine präzise gruppenbasierte Zugriffsverwaltung für Ressourcen, deren Struktur auf Benutzerrollen basiert.
- **Richtlinienentscheidungen.** [Azure Blueprints-Beispiele](https://docs.microsoft.com/azure/governance/blueprints/samples) bieten vorgefertigte Complianceblaupausen, die jeweils vordefinierte Richtlinieninitiativen enthalten. Richtlinienentscheidungen dienen zur Ermittlung der am besten geeigneten Blaupause oder Richtlinieninitiative, basierend auf Ihren Anforderungen und Einschränkungen.
- **Schaffen von [Hybrid Cloud-Konsistenz](./hybrid-consistency.md).** Erstellen Sie Hybrid Cloud-Lösungen, mit denen Ihre Organisation sowohl von den Vorteilen innovativer Cloudfeatures als auch von vielen praktischen Features der lokalen Verwaltung profitiert.
