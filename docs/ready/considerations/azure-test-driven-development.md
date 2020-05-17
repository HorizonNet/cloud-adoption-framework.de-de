---
title: Testgesteuerte Entwicklung (TDD) für Zielzonen in Azure
description: Testgesteuerte Entwicklung (TDD) für Zielzonen in Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b4edc0f0e485c040045bc8c1b7bce6c91f3d13f9
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83221908"
---
# <a name="test-driven-development-tdd-for-landing-zones-in-azure"></a>Testgesteuerte Entwicklung (TDD) für Zielzonen in Azure

Wie im vorhergehenden Artikel über [testgesteuerte Entwicklung für Zielzonen](./test-driven-development.md) beschrieben, beginnen TDD-Zyklen mit einem Test, der die Akzeptanzkriterien eines bestimmten Features validiert, das für die Bereitstellung des Cloudeinführungsplans erforderlich ist. Die Erweiterung oder das Refactoring der Zielzone kann dann getestet werden, um zu bestätigen, dass die Akzeptanzkriterien erfüllt sind. In diesem Artikel wird eine cloudnative Toolkette in Azure vorgestellt, um testgesteuerte Entwicklungszyklen zu automatisieren.

## <a name="azure-tools-to-support-landing-zone-tdd-cycles"></a>Azure-Tools zur Unterstützung der TDD-Zyklen von Zielzonen

![Testgesteuerte Entwicklungstools in Azure](../../_images/ready/azure-tdd-tools.png)

Die Toolkette der Azure-nativen Governanceprodukte und -dienste kann leicht in die testgesteuerte Entwicklung für die Erstellung von Zielzonen integriert werden. Jedes dieser Tools dient einem bestimmten Zweck, wodurch die Entwicklung, das Testen und die Bereitstellung Ihrer Zielzone in Übereinstimmung mit TDD-Zyklen erleichtert wird.

## <a name="microsoft-provided-test-and-deployment-templates-to-accelerate-tdd"></a>Von Microsoft bereitgestellte Test- und Bereitstellungsvorlagen zum Beschleunigen von TDD

Die folgenden Beispiele werden von Microsoft für Governancezwecke zur Verfügung gestellt. Jedes kann jedoch als Test oder Testreihe in einem testgesteuerten Entwicklungszyklus für Zielzonen verwendet werden. Weitere Informationen zu den einzelnen Tools finden Sie im folgenden Abschnitt.

- Azure Blueprints bietet verschiedene [Blaupausenmuster](https://docs.microsoft.com/azure/governance/blueprints/samples), die Richtlinien für Tests und Vorlagen für die Bereitstellung enthalten. Diese Blaupausenmuster können den Entwicklungs-, Bereitstellungs- und Testaufwand in TDD-Zyklen beschleunigen.
- Azure Policy umfasst auch [integrierte Richtlinieninitiativen](https://docs.microsoft.com/azure/governance/policy/samples/built-in-initiatives), die dazu dienen könnten, die vollständige „Definition of Done“ für eine Zielzone zu testen und durchzusetzen. Azure Policy umfasst [integrierte Richtliniendefinitionen](https://docs.microsoft.com/azure/governance/policy/samples/built-in-policies), die individuelle Akzeptanzkriterien innerhalb der „Definition of Done“ erfüllen können.
- Azure Graph enthält fortgeschrittene [Abfragebeispiele](https://docs.microsoft.com/azure/governance/resource-graph/samples/advanced), die für fortgeschrittene Testszenarien verwendet werden können, um zu verstehen, wie die Workloads innerhalb einer Zielzone bereitgestellt werden.
- [Azure Schnellstartvorlagen](https://azure.microsoft.com/resources/templates) stellen Quellcodevorlagen zur Verfügung, um die Bereitstellung der Zielzone und der Workload zu beschleunigen.

Jedes der obigen Beispiele kann als Tool zur Beschleunigung von TDD-Zyklen verwendet werden. Diese Beispiele werden mit den Governancetools in den folgenden Abschnitten ausgeführt, die es Cloudplattformteams ermöglichen, ihren eigenen Quellcode und ihre eigenen Tests zu erstellen.

## <a name="azure-governance-tools-that-can-accelerate-tdd-cycles"></a>Azure Governance-Tools, die TDD-Zyklen beschleunigen können

[Azure Policy](https://docs.microsoft.com/azure/governance/policy): Wenn die Bereitstellungen oder versuchten Bereitstellungen von den Governancerichtlinien abweichen, kann Azure Policy automatische Erkennung, Schutz und Lösung bieten. Aber Azure Policy bietet auch den primären Mechanismus zum Testen von Akzeptanzkriterien in Ihrer „Definition of Done“. In einem TDD-Zyklus kann eine Richtliniendefinition erstellt werden, um ein einzelnes Akzeptanzkriterium zu testen. Ebenso können alle Akzeptanzkriterien zu einer Richtlinieninitiative hinzugefügt werden, die dem gesamten Abonnement zugewiesen wird. Dieser Ansatz sieht einen Mechanismus für „Rot-Tests“ vor, bevor die Zielzone modifiziert wird. Nachdem die Zielzone der"Definition of Done" entspricht, kann sie dazu verwendet werden, die Testkriterien durchzusetzen, um Codeänderungen zu vermeiden, die ein Fehlschlagen des Tests in zukünftigen Versionen verursachen würden.

[Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints): Azure Blueprint gruppiert Richtlinien und andere Bereitstellungstools in einem wiederholbaren Paket, das mehreren Zielzonen zugeordnet werden kann. Blaupausen erweisen sich als nützlich, wenn mehrere Einführungsbemühungen eine gemeinsame „Definition of Done“ aufweisen, die Sie im Laufe der Zeit vielleicht aktualisieren möchten. Sie können auch bei späteren Bemühungen zur Erweiterung und Umgestaltung von Zielzonen bei deren Bereitstellung helfen.

[Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph): Resource Graph bietet eine Abfragesprache zur Erstellung datengesteuerter Tests auf der Grundlage von Informationen über die in einer Zielzone bereitgestellten Ressourcen. Später im Einführungsplan kann dieses Tool auch komplexe Tests definieren, die auf den Interaktionen zwischen den Workloadressourcen und der zugrunde liegenden Cloudumgebung basieren.

[Azure Resource Manager-Vorlagen](https://docs.microsoft.com/azure/azure-resource-manager/templates/overview): Diese Vorlagen stellen den primären Quellcode für jede in Azure bereitgestellte Umgebung zur Verfügung. Wenn Tools von Drittanbietern, wie Terraform, zur Entwicklung von Quellcode verwendet werden, der eine Zielzone vorsieht, generieren die Tools ihre eigenen Vorlagen. Diese Vorlagen werden dann an Azure Resource Manager übermittelt.

[Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview): Resource Manager bietet eine konsistente Plattform für den Aufbau und die Bereitstellung von Funktionen. Diese Plattform verwaltet die Bereitstellung einer Zielzone vom Quellcode aus.

## <a name="next-steps"></a>Nächste Schritte

Bewerten Sie [grundlegende Überlegungen zu Zielzonen](./basic-considerations.md), um mit dem Refactoring Ihrer ersten Zielzone zu beginnen.

> [!div class="nextstepaction"]
> [Grundlegende Überlegungen zu Zielzonen](./basic-considerations.md)
