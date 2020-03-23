---
title: Bereitstellen einer Landezone in Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Erfahren Sie, wie Sie in Azure eine Landezone für die Migration bereitstellen.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1727bb9c77298663f30e6205a9a3230ce65be3c1
ms.sourcegitcommit: 5d7e93540a679252f1c7207e62cb2ee7213a6ae9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80069756"
---
<!-- cSpell:ignore vCPUs jumpbox -->

# <a name="deploy-a-migration-landing-zone"></a>Bereitstellen einer Landezone für die Migration

Der Begriff *Landezone für die Migration* beschreibt eine Umgebung, die bereitgestellt und auf das Hosten von Workloads vorbereitet wurde, die von einer lokalen Umgebung nach Azure migriert werden.

## <a name="deploy-the-first-landing-zone"></a>Bereitstellen Ihrer ersten Zielzone

Bevor Sie die Migrationszielzonen-Blaupause im Cloud Adoption Framework verwenden, lesen Sie die folgenden Annahmen, Entscheidungen und Leitlinien für die Implementierung. Wenn diese Anleitung dem gewünschten Cloudeinführungsplan entspricht, kann die [Migrationszielzonen-Blaupause](https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/index) mithilfe der [Bereitstellungsschritte][deploy-sample]bereitgestellt werden.

> [!div class="nextstepaction"]
> [Bereitstellen des Blaupausenbeispiels][deploy-sample]

## <a name="assumptions"></a>Annahmen

Diese anfängliche Zielzone umfasst folgende Annahmen bzw. Einschränkungen. Wenn diese Annahmen Ihren Einschränkungen entsprechen, können Sie die Blaupause zum Erstellen Ihrer ersten Landezone verwenden. Die Blaupause kann auch erweitert werden, sodass Sie eine Landezonenblaupause erstellen können, die Ihre einzigartigen Einschränkungen erfüllt.

- **Grenzwerte für Abonnements**: Bei der Einführung ist nicht damit zu rechnen, dass [Abonnementgrenzwerte](https://docs.microsoft.com/azure/azure-subscription-service-limits) überschritten werden.
- **Compliance**: In dieser Landezone sind keine Complianceanforderungen von Dritten zu beachten.
- **Komponenten der Architektur**: Die Komplexität der Architektur erfordert keine zusätzlichen Produktionsabonnements.
- **Gemeinsam genutzte Dienste**: Es sind keine gemeinsam genutzten Dienste in Azure vorhanden, die erfordern, dass dieses Abonnement wie ein Spoke in einer Hub-and-Spoke-Architektur behandelt wird.
- **Begrenzter Produktionsbereich:** Diese Zielzone könnte Produktionsworkloads hosten. Sie ist jedoch keine geeignete Umgebung für vertrauliche Daten oder unternehmenskritische Workloads.

Wenn diese Annahmen mit Ihren aktuellen Anforderungen in Bezug auf die Einführung übereinstimmen, ist diese Blaupause möglicherweise ein guter Ausgangspunkt zum Erstellen einer Zielzone.

## <a name="decisions"></a>Entscheidungen

Die folgenden Entscheidungen werden in der Blaupause für die Landezone widergespiegelt.

| Komponente                    | Entscheidungen                                                                                         | Alternative Ansätze                                                                                                                                                                                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Migrationstools              | Azure Site Recovery wird bereitgestellt, und ein Azure Migrate-Projekt wird erstellt.                | [Entscheidungsleitfaden zur Wahl von Migrationstools](../../decision-guides/migrate-decision-guide/index.md)                                                                                                                                                                                              |
| Protokollierung und Überwachung       | Ein Operational Insights-Arbeitsbereich und ein Speicherkonto für die Diagnose werden bereitgestellt.                |                                                                                                                                                                                                                                                                                      |
| Netzwerk                      | Es wird ein virtuelles Netzwerk mit Subnetzen für Gateway, Firewall, Jumpbox und Landezone erstellt.  | [Netzwerkentscheidungen](../considerations/networking-options.md)                                                                                                                                                                                                                      |
| Identity                     | Es wird angenommen, dass das Abonnement bereits einer Azure Active Directory-Instanz zugeordnet ist. | [Bewährte Methoden für die Identitätsverwaltung](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) |
| Richtlinie                       | Bei dieser Blaupause wird derzeit davon ausgegangen, dass keine Azure-Richtlinien angewendet werden müssen.                        |                                                                                                                                                                                                                                                                                      |
| Abonnemententwurf          | N/V: wurde für ein einzelnes Produktionsabonnement entworfen.                                              | [Skalieren von Abonnements](../azure-best-practices/scaling-subscriptions.md)                                                                                                                                                                                                            |
| Verwaltungsgruppen            | N/V: wurde für ein einzelnes Produktionsabonnement entworfen.                                              | [Skalieren von Abonnements](../azure-best-practices/scaling-subscriptions.md)                                                                                                                                                                                                            |
| Ressourcengruppen              | N/V: wurde für ein einzelnes Produktionsabonnement entworfen.                                              | [Skalieren von Abonnements](../azure-best-practices/scaling-subscriptions.md)                                                                                                                                                                                                            |
| Daten                         | –                                                                                               | [Auswählen der richtigen Bereitstellungsoption in Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) und [Auswählen des richtigen Datenspeichers](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview)                      |
| Storage                      | –                                                                                               | [Leitfaden zu Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                                       |
| Standards für Benennung und Kennzeichnung | –                                                                                               | [Best Practices zur Benennung und Kennzeichnung](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                                                   |
| Kostenverwaltung              | –                                                                                               | [Nachverfolgen von Kosten](../azure-best-practices/track-costs.md)                                                                                                                                                                                                                             |
| Compute                      | –                                                                                               | [Computeoptionen](../considerations/compute-options.md)                                                                                                                                                                                                                              |

## <a name="customize-or-deploy-a-landing-zone"></a>Anpassen oder Bereitstellen einer Zielzone

Erfahren Sie mehr, und laden Sie ein Referenzbeispiel der Migrationszielzonen-Blaupause für die Bereitstellung oder Anpassung von [Azure Blueprints-Beispielen][deploy-sample] herunter.

> [!div class="nextstepaction"]
> [Bereitstellen des Blaupausenbeispiels][deploy-sample]

Eine Anleitung zu den Anpassungen, die in dieser Blaupause oder der resultierenden Zielzone vorgenommen werden sollten, finden Sie in den [Überlegungen zu Zielzonen](../considerations/index.md).

## <a name="next-steps"></a>Nächste Schritte

Wen Sie Ihre erste Zielzone bereitgestellt haben, können Sie Ihre [Zielzone erweitern](../considerations/index.md).

> [!div class="nextstepaction"]
> [Erweitern der Zielzone](../considerations/index.md)

<!-- links -->

[deploy-sample]: https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/deploy
